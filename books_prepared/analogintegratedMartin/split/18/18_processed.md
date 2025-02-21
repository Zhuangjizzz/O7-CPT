# 18 Oversampling Converters

Key Point: Oversampling converters relax the requirements placed on the analog circuitry at the expense of more complicated digital circuitry.

Oversampling $\mathrm{A} / \mathrm{D}$ and $\mathrm{D} / \mathrm{A}$ converters are popular for high-resolution medium-to-low-speed applications such as high-quality digital audio and baseband signal processing in some wireless systems. A major reason for their popularity is that oversampling converters relax the requirements placed on the analog circuitry at the expense of more complicated digital circuitry. This tradeoff became desirable with the advent of deep submicron CMOS technologies as complicated high-speed digital circuitry became more easily realized in less area, but the realization of high-resolution analog circuitry was complicated by the low power-supply voltages and poor transistor output impedance caused by short-channel effects. With oversampling data converters, the analog components have reduced requirements on matching tolerances and amplifier gains. Oversampling converters also simplify the requirements placed on the analog anti-aliasing filters for $\mathrm{A} / \mathrm{D}$ converters and smoothing filters for D/A converters. For example, usually only a first- or second-order anti-aliasing filter is required for A/D converters, which can often be realized very inexpensively. Furthermore, a sample-and-hold is usually not required at the input of an oversampling $A / D$ converter.

In this chapter, the basics of oversampling converters are discussed first. We shall see that extra bits of resolution can be extracted from converters that sample much faster than the Nyquist rate. Furthermore, this extra resolution can be obtained with lower oversampling rates by spectrally shaping the quantization noise through the use of feedback. The use of shaped quantization noise applied to oversampling signals is commonly referred to as delta-sigma $(\Delta \Sigma)$ modulation. ${ }^{1}$ Simple first- and second-order $\Delta \Sigma$ modulators are discussed, followed by a discussion of typical system architectures for $\Delta \Sigma$ data converters. Next, two popular approaches for realizing decimation filters are described. Descriptions of some modern approaches are then described along with some practical considerations. The chapter concludes with an example design of a third-order $\Delta \Sigma$ A/D converter.

## 18.1 OVERSAMPLING WITHOUT NOISE SHAPING

In this section, the advantage of sampling at higher than the Nyquist rate is discussed. Here, we shall see that extra dynamic range can be obtained by spreading the quantization noise power over a larger frequency range. However, we shall see that the increase in dynamic range is only 3 dB for every doubling of the sample rate. To obtain much higher dynamic-range improvements as the sampling rate is increased, noise shaping through the use of feedback can be used and is discussed in the next section.

[^2]image_name:Fig. 18.1 Quantizer and its linear model
description:The system block diagram labeled "Fig. 18.1 Quantizer and its linear model" consists of two main parts: the quantizer and its corresponding linear model.

1. **Main Components:**
- **Quantizer Block:** This is represented on the left side of the diagram. The quantizer takes an input signal \( x(n) \) and outputs a signal \( y(n) \). Inside the quantizer block, there is a staircase-like graph, illustrating the quantization process where the continuous input values are mapped to discrete output levels.
- **Linear Model:** On the right side of the diagram, the quantizer is modeled linearly. The input \( x(n) \) is shown as an arrow leading to a summation point, where it is combined with a quantization error \( e(n) \) to produce the output \( y(n) \). The equation \( e(n) = y(n) - x(n) \) is provided to indicate that the error is the difference between the quantized output and the original input.

2. **Flow of Information or Control:**
- The input signal \( x(n) \) flows into the quantizer block, where it undergoes quantization, resulting in the output \( y(n) \). This output is then modeled linearly by adding the quantization error \( e(n) \) to the input \( x(n) \) to recreate the output \( y(n) \).

3. **Labels, Annotations, and Key Indicators:**
- The quantizer block is labeled clearly with input \( x(n) \) and output \( y(n) \) signals.
- The linear model includes a summation point labeled with \( + \), showing the addition of quantization error \( e(n) \).
- The equation \( e(n) = y(n) - x(n) \) is annotated to provide a mathematical representation of the quantization error.

4. **Overall System Function:**
- The primary function of this diagram is to illustrate the quantization process and its modeling. The quantizer converts the input signal into a quantized output by mapping it to discrete levels, introducing a quantization error. The linear model represents this process by adding the quantization error to the input to achieve the quantized output. This model helps in analyzing and understanding the effect of quantization in digital signal processing systems.

Fig. 18.1 Quantizer and its linear model.
image_name:Fig. 18.2 Assumed spectral density of quantization noise
description:The graph in Fig. 18.2 represents the assumed spectral density of quantization noise. This is a frequency-domain plot with the horizontal axis labeled as frequency \( f \) and the vertical axis labeled as \( S_e(f) \), which denotes the spectral density of the quantization error.

1. **Type of Graph and Function:**
- This is a spectral density plot, showing the distribution of quantization noise power across different frequencies.

2. **Axes Labels and Units:**
- The horizontal axis represents frequency \( f \), with significant points marked at \(-\frac{f_s}{2}\), 0, and \(\frac{f_s}{2}\), where \( f_s \) is the sampling frequency.
- The vertical axis represents the spectral density \( S_e(f) \).

3. **Overall Behavior and Trends:**
- The graph is characterized by a constant level of spectral density across the frequency range from \(-\frac{f_s}{2}\) to \(\frac{f_s}{2}\). This indicates that the quantization noise is uniformly distributed over this frequency band.

4. **Key Features and Technical Details:**
- The spectral density has a constant height, denoted as \( k_x = \left( \frac{\Delta}{\sqrt{12}} \right) \sqrt{\frac{1}{f_s}} \), where \( \Delta \) is the quantization step size. This formula indicates the magnitude of the noise power density.
- The plot is essentially a rectangular shape, indicating a flat noise spectrum, which is typical for white noise.

5. **Annotations and Specific Data Points:**
- The graph includes an annotation for the height of the spectral density, providing the formula for \( k_x \).
- The frequency range is explicitly marked from \(-\frac{f_s}{2}\) to \(\frac{f_s}{2}\), emphasizing the Nyquist frequency range for digital signals.

Fig. 18.2 Assumed spectral density of quantization noise.

### 18.1.1 Quantization Noise Modelling

We begin by modelling a quantizer as adding quantization error $\mathrm{e}(\mathrm{n})$, as shown in Fig. 18.1. The output signal, $y(n)$, is equal to the closest quantized value of $\mathbf{x}(\mathrm{n})$. The quantization error is the difference between the input and output values. This model is exact if one recognizes that the quantization error is not an independent signal but may be strongly related to the input signal, $\mathbf{x}(\mathrm{n})$. This linear model becomes approximate when assumptions are made about the statistical properties of $e(n)$, such as $e(n)$ being an independent white-noise signal. However, even though approximate, it has been found that this model leads to a much simpler understanding of $\Delta \Sigma$ and with some exceptions is usually reasonably accurate.

### 18.1.2 White Noise Assumption

If $x(n)$ is very active, $e(n)$ can be approximated as an independent random number uniformly distributed between $\pm \Delta / 2$, where $\Delta$ equals the difference between two adjacent quantization levels. Thus, the quantization noise power equals $\Delta^{2} / 12$ (from Section 15.3) and is independent of the sampling frequency, $f_{s}$. Also, the spectral density of $\mathrm{e}(\mathrm{n}), \mathrm{S}_{\mathrm{e}}(\mathrm{f})$, is white (i.e., a constant over frequency) and all its power is within $\pm \mathrm{f}_{\mathrm{s}} / 2$ (a two-sided definition of power).

Assuming white quantization noise, the spectral density of the quantization noise, $\mathrm{S}_{\mathrm{e}}(\mathrm{f})$ appears as shown in Fig. 18.2.

Key Point: Quantization with a step size "LSB" can be modeled as an additive quantization noise uniformly distributed between $-L S B / 2$ and $+L S B / 2$ with a white power spectrum and total power of $\operatorname{LSB}^{2} / 12$.

The spectral density height is calculated by noting that the total noise power is $\Delta^{2} / 12$ and, with a two-sided definition of power, equals the area under $S_{e}(f)$ within $\pm f_{s} / 2$, or mathematically,

$$
\begin{equation*}
\int_{-\mathrm{s}_{\mathrm{s}} / 2}^{\mathrm{f}_{\mathrm{s}} / 2} \mathrm{~S}_{\mathrm{e}}^{2}(\mathrm{f}) \mathrm{df}=\int_{-\mathrm{f}_{\mathrm{s}} / 2}^{\mathrm{f}_{\mathrm{s}} / 2} \mathrm{k}_{\mathrm{x}}^{2} \mathrm{df}=\mathrm{k}_{\mathrm{x}}^{2} \mathrm{f}_{\mathrm{s}}=\frac{\Delta^{2}}{12} \tag{18.1}
\end{equation*}
$$

Solving this relation gives

$$
\begin{equation*}
\mathrm{k}_{\mathrm{x}}=\left(\frac{\Delta}{\sqrt{12}}\right) \sqrt{\frac{1}{\mathrm{f}_{\mathrm{s}}}} \tag{18.2}
\end{equation*}
$$

#### EXAMPLE 18.1

Find the output and quantization errors for two different quantizers, as shown in Fig. 18.3, when the input values are

$$
\begin{equation*}
x(n)=\{0.01,0.31,-0.11,0.80,0.52,-0.70\} \tag{18.3}
\end{equation*}
$$

Also find the expected power and the power density height, $S_{e}^{2}(\mathrm{f})$, of the quantization noise when the sampling frequency is normalized to $2 \pi \mathrm{rad} /$ sample.

#### Solution

The output and quantization noise values for this example are given in Table 18.1. Note that although the output signals, $y(n)$, are well-defined values, the quantization error values can be approximated as uniformly distributed random numbers since the input signal is quite active.

Recalling that the quantization noise power is given by

$$
\begin{equation*}
\mathrm{P}_{\mathrm{e}}=\frac{\Delta^{2}}{12} \tag{18.4}
\end{equation*}
$$

then the expected noise powers of the two quantizers are

$$
\begin{equation*}
\mathrm{P}_{\mathrm{I}}=\frac{0.5^{2}}{12}=0.0208 \mathrm{~W} \tag{18.5}
\end{equation*}
$$

image_name:Quantizer I (Five-level quantizer)
description:The graph titled "Quantizer I (Five-level quantizer)" represents a step function used in signal processing to approximate continuous signal values into discrete levels. This is a piecewise constant function that maps an input signal \( x(n) \) to a quantized output \( y(n) \) using five discrete levels.

Type of Graph and Function:
- The graph is a step function used for quantization, which is a process in signal processing where continuous amplitude values are mapped to discrete levels.

Axes Labels and Units:
- The horizontal axis is labeled \( x(n) \), representing the input signal values.
- The vertical axis is labeled \( y(n) \), representing the quantized output levels.
- The quantization step size \( \Delta \) is given as 0.5.

Overall Behavior and Trends:
- The graph shows a staircase pattern with five levels.
- As the input \( x(n) \) increases, the output \( y(n) \) jumps to the nearest quantization level.
- The levels are centered around 0, with steps at -1.0, -0.5, 0.0, 0.5, and 1.0.

Key Features and Technical Details:
- The quantization levels are equally spaced with a step size \( \Delta = 0.5 \).
- The function is constant within intervals of \( x(n) \), specifically between \(-0.75\) to \(-0.25\), \(-0.25\) to \(0.25\), \(0.25\) to \(0.75\), and so on.
- Each step represents a range of input values that are mapped to a single output level.

Annotations and Specific Data Points:
- The graph indicates critical transition points at \( x(n) = -0.75, -0.25, 0.25, 0.75 \) where the output level changes.
- Each step is labeled with its corresponding output value \( y(n) \).

This quantizer is used to reduce the precision of signal representation, introducing quantization noise as a trade-off for fewer bits required to represent the signal.
image_name:Quantizer II (Two-level quantizer)
description:The graph for "Quantizer II (Two-level quantizer)" is a step function representing a two-level quantizer. The horizontal axis is labeled as \(x(n)\), which represents the input signal values, while the vertical axis is labeled as \(y(n)\), representing the quantized output values. The quantization step size \(\Delta\) is 2.0.

Type of Graph and Function
This is a piecewise constant function graph, specifically a step function, depicting the behavior of a two-level quantizer.

Axes Labels and Units
- **Horizontal Axis (x(n))**: Represents the input values of the signal, with no specific units provided.
- **Vertical Axis (y(n))**: Represents the quantized output values, ranging from -1.0 to 1.0, also with no specific units.

Overall Behavior and Trends
The graph shows that the quantizer outputs a value of 1.0 for all input values \(x(n)\) greater than or equal to 0, and outputs -1.0 for all input values \(x(n)\) less than 0. This binary behavior is characteristic of a two-level quantizer, which simplifies the input signal to just two possible output levels.

Key Features and Technical Details
- The transition between the two levels occurs at \(x(n) = 0\), which is the threshold for quantization.
- The quantizer has a step size \(\Delta = 2.0\), indicating the range of input values that map to the same quantized output level.

Annotations and Specific Data Points
There are no specific annotations or data points marked on the graph beyond the axes labels and quantization levels. The graph effectively illustrates the simple binary decision-making process of the two-level quantizer, mapping any positive or zero input to 1.0 and any negative input to -1.0.

Fig. 18.3 Two example quantizers.

#### Table 18.1 Example signal values and quantization noise for two quantizers.

|  | Quantizer I <br> (Five Levels) |  |  | Quantizer II <br> (Two Levels) |  |
| ---: | ---: | ---: | ---: | ---: | ---: |
| $\mathbf{x}(\mathbf{n})$ | $\mathbf{y ( n )}$ | $\mathbf{e ( n )}$ |  | $\mathbf{y ( n )}$ | $\mathbf{e ( n )}$ |
| 0.01 | 0.0 | -0.01 |  | 1 | 0.99 |
| 0.31 | 0.5 | 0.19 |  | 1 | 0.69 |
| -0.11 | 0.0 | 0.11 |  | -1 | -0.89 |
| 0.80 | 1.0 | 0.2 |  | 1 | 0.20 |
| 0.52 | 0.5 | -0.02 |  | 1 | 0.48 |
| -0.70 | -0.5 | 0.2 |  | -1 | -0.30 |

$$
\begin{equation*}
\mathrm{P}_{\mathrm{II}}=\frac{2^{2}}{12}=0.333 \mathrm{~W} \tag{18.6}
\end{equation*}
$$

where we note that these values are not affected by normalizing the sampling frequency. Also note that the two power estimates for $P_{I}$ and $P_{I I}$ correspond to rms power levels of 0.144 and 0.577 , respectively.

For the power density, we note that the power is spread evenly between $\pm f_{s} / 2$, resulting in a density of

$$
\begin{equation*}
S_{e}^{2}(f)=\frac{P_{e}}{f_{s}} \tag{18.7}
\end{equation*}
$$

which results in

$$
\begin{align*}
& S_{\mathrm{el}}^{2}(\mathrm{f})=\left(\frac{0.0208}{2 \pi}\right)=0.00331 \frac{\mathrm{~W}}{\mathrm{rad} / \mathrm{sample}}  \tag{18.8}\\
& \mathrm{~S}_{\mathrm{elI}}^{2}(\mathrm{f})=\left(\frac{0.333}{2 \pi}\right)=0.053 \frac{\mathrm{~W}}{\mathrm{rad} / \mathrm{sample}} \tag{18.9}
\end{align*}
$$

### 18.1.3 Oversampling Advantage

Oversampling occurs when the signals of interest are bandlimited to $f_{0}$ yet the sample rate is at $f_{s}$, where $f_{s}>2 f_{0}$ ( $2 f_{0}$ being the Nyquist rate or, equivalently, the minimum sampling rate for signals bandlimited to $f_{0}$ ). We define the oversampling ratio, OSR, as

$$
\begin{equation*}
\mathrm{OSR} \equiv \frac{\mathrm{f}_{\mathrm{s}}}{2 \mathrm{f}_{0}} \tag{18.10}
\end{equation*}
$$

After quantization, since the signals of interest are all below $f_{0}, y_{1}(n)$ is filtered by $H(f)$ to create the signal $y_{2}(n)$, as shown in Fig. 18.4. This filter eliminates quantization noise (together with any other signals) greater than $\mathrm{f}_{0}$.

Assuming the input signal is a sinusoidal wave, its maximum peak value without clipping is $2^{\mathrm{N}}(\Delta / 2)$. For this maximum sinusoidal wave, the signal power, $P_{s}$, has a power equal to

$$
\begin{equation*}
P_{s}=\left(\frac{\Delta 2^{N}}{2 \sqrt{2}}\right)^{2}=\frac{\Delta^{2} 2^{2 N}}{8} \tag{18.11}
\end{equation*}
$$

image_name:(a)
description:The system block diagram labeled as (a) represents an oversampling system without noise shaping. It consists of two main components: an N-bit quantizer and a filter denoted by H(f).

1. **Main Components:**
- **N-bit Quantizer:** This block receives the input signal, u(n), and quantizes it into discrete levels. The output of this block is y₁(n), which contains quantization noise due to the conversion process.
- **Filter H(f):** This block processes the quantized signal y₁(n). The filter is characterized by its frequency response, which is shown in part (b) of the figure. It is a brick-wall filter that allows frequencies below f₀ to pass while attenuating frequencies above f₀.

2. **Flow of Information or Control:**
- The input signal u(n) is fed into the N-bit quantizer. The quantized output, y₁(n), is then passed to the filter H(f).
- The filter processes y₁(n), removing quantization noise and any other signals with frequencies greater than f₀. The output of the filter is y₂(n).

3. **Labels, Annotations, and Key Indicators:**
- The input and output signals are labeled as u(n), y₁(n), and y₂(n).
- The filter's frequency response is depicted in part (b) as a rectangular response with a cutoff frequency of f₀, showing that it has a gain of 1 for frequencies between -f₀ and f₀ and zero outside this range.

4. **Overall System Function:**
- The primary function of this system is to process an input signal, quantize it, and then filter out unwanted noise and signals above a certain frequency. The N-bit quantizer introduces quantization noise, which is then attenuated by the filter H(f). The system is designed to retain signal components below the cutoff frequency f₀ while reducing the power of quantization noise in the output signal y₂(n).
image_name:(b)
description:The graph in Fig. 18.4(b) is a frequency response plot, specifically illustrating the magnitude response of a low-pass filter with a brick-wall characteristic.

1. **Type of Graph and Function:**
- This is a magnitude frequency response graph.
- The function depicted is a brick-wall low-pass filter.

2. **Axes Labels and Units:**
- The horizontal axis represents frequency \( f \), with units typically in hertz (Hz).
- The vertical axis represents the magnitude \(|H(f)|\) of the filter response, which is unitless as it is a ratio.
- The graph is linear in terms of both axes.

3. **Overall Behavior and Trends:**
- The graph shows a rectangular shape, indicating a sharp cutoff at the frequency \( f_0 \).
- The magnitude is constant and equal to 1 (unity gain) for frequencies between \(-f_0\) and \(f_0\), and drops to 0 outside this range.

4. **Key Features and Technical Details:**
- The cutoff frequency is clearly marked at \( f_0 \) and \(-f_0\).
- The filter passes all frequencies in the range \(-f_0\) to \(f_0\) without attenuation, while completely attenuating frequencies outside this range.
- There are no peaks or valleys; the transition from passband to stopband is instantaneous, characteristic of an ideal filter.

5. **Annotations and Specific Data Points:**
- The graph is symmetric around the origin, indicating the filter's response is even.
- The passband gain is 1, and the stopband gain is 0.
- The Nyquist frequency \( \frac{f_s}{2} \) is marked on the axis, indicating the maximum frequency that can be accurately represented given the sampling frequency \( f_s \).

Fig. 18.4 (a) A possible oversampling system without noise shaping. (b) The brick-wall response of the filter to remove much of the quantization noise.

The power of the input signal within $\mathrm{y}_{2}(\mathrm{n})$ remains the same as before since we assumed the signal's frequency content is below $f_{0}$. However, the quantization noise power is reduced to

$$
\begin{equation*}
P_{e}=\int_{-f_{s} / 2}^{f_{\mathrm{s}} / 2} S_{e}^{2}(f)|H(f)|^{2} d f=\int_{-f_{0}}^{f_{0}} k_{x}^{2} d f=\frac{2 f_{0}}{f_{s}} \frac{\Delta^{2}}{12}=\frac{\Delta^{2}}{12}\left(\frac{1}{\mathrm{OSR}}\right) \tag{18.12}
\end{equation*}
$$

Therefore, doubling OSR (i.e., sampling at twice the rate) decreases the quantization noise power by one-half or, equivalently, 3 dB (or, equivalently, 0.5 bits).

We can also calculate the maximum SQNR (in dB ) to be the ratio of the maximum sinusoidal power to the quantization noise power in the signal $\mathrm{y}_{2}(\mathrm{n})$. Mathematically, we have through the use of (18.11) and (18.12)

$$
\begin{equation*}
\mathrm{SQNR}_{\max }=10 \log \left(\frac{\mathrm{P}_{\mathrm{s}}}{\mathrm{P}_{\mathrm{e}}}\right)=10 \log \left(\frac{3}{2} 2^{2 \mathrm{~N}}\right)+10 \log (\mathrm{OSR}) \tag{18.13}
\end{equation*}
$$

which is also equal to

Key Point: Oversampling a signal at OSR times the Nyquist rate, without spectrally shaping the quantization noise, results in a SNR enhancement of $10 \log (O S R) d B$.

$$
\begin{equation*}
\mathrm{SQNR}_{\max }=6.02 \mathrm{~N}+1.76+10 \log (\mathrm{OSR}) \tag{18.14}
\end{equation*}
$$

The first term is the SQNR due to the N -bit quantizer while the OSR term is the SQNR enhancement obtained from oversampling. Here we see that straight oversampling gives a SQNR improvement of $3 \mathrm{~dB} /$ octave or, equivalently, 0.5 bits/octave. The reason for this SQNR improvement through the use of oversampling is that when quantized samples are averaged together, the signal portion adds linearly, whereas the noise portion adds as the square root of the sum of the squares. Note that this enhancement also takes place with respect to other types of noise, such as thermal noise in circuits. Hence, oversampling generally improves overall signal to noise ratio (SNR) by $10 \log (\mathrm{OSR})$.

[^0]:    1. In fact, the resistor-string $D / A$ was used to realize an $A / D$ converter in the reference.
[^1]:    1. Strictly speaking, because each stage produces one of three digital output codes $(00,01$, or 11$)$, they are actually $\log _{2}(3)=1.585$-bit stages, but in practice they are always referred to simply as 1.5 -bit stages.
[^2]:    1. Delta-sigma modulation is also sometimes referred to as sigma-delta modulation.

#### EXAMPLE 18.2

Consider a sampled dc signal, $\mathrm{V}_{\mathrm{s}}$, of value 1 V where the measured voltage, $\mathrm{V}_{\text {meas }}$, is $\mathrm{V}_{\mathrm{s}}$ plus a noise signal, $\mathrm{V}_{\text {noise }}$. Assume $\mathrm{V}_{\text {noise }}$ is a random signal uniformly distributed between $\pm \sqrt{3}$. What is the SNR for $\mathrm{V}_{\text {meas }}$ when looking at individual values? If eight samples of $\mathrm{V}_{\text {meas }}$ are averaged together, roughly what is the new SNR? To illustrate the results, use eight typical samples for $\mathrm{V}_{\text {meas }}$ of $\{0.94,-0.52,-0.73,2.15,1.91,1.33,-0.31,2.33\}$.

#### Solution

Referencing signals to $1 \Omega$, we calculate the power of $V_{s}$ and $V_{\text {noise }}$ to both be 1 watt. Thus the SNR for $V_{\text {meas }}$ is 0 dB when looking at individual $\mathrm{V}_{\text {meas }}$ values. Note that it is difficult to see the signal value of 1 V in the example $V_{\text {meas }}$ samples since the SNR is so poor.

If eight samples are averaged, we are realizing a modest low-pass filter, resulting in the oversampling ratio being approximately equal to 8 (this is a rough estimate since a brick-wall filter is not being used). Since each octave of oversampling results in a $3-\mathrm{dB}$ SNR improvement, the averaged value should have a SNR of around 9 dB . Note that averaging the eight given $\mathrm{V}_{\text {meas }}$ samples results in 0.8875 , which more closely represents the signal value of 1 V .

The reason oversampling improves the SNR here is that by summing eight measured values, the eight signal values add linearly to $8 \mathrm{~V}_{\mathrm{rms}}$ (or 64 watts) while the eight noise values add to $\sqrt{8} \mathrm{~V}_{\mathrm{rms}}$ (or 8 watts), since the noise values are assumed to be independent.

#### EXAMPLE 18.3

Given that a 1-bit A/D converter has a $6-\mathrm{dB}$ SQNR, what sample rate is required using oversampling (no noise shaping) to obtain a $96-\mathrm{dB}$ SQNR (i.e., 16 bits) if $\mathrm{f}_{0}=25 \mathrm{kHz}$ ? (Note that the input into the $\mathrm{A} / \mathrm{D}$ converter has to be very active for the white-noise quantization model to be valid-a difficult arrangement when using a 1 bit quantizer with oversampling without noise shaping.)

#### Solution

Oversampling (without noise shaping) gives 3 dB /octave where 1 octave implies doubling the sampling rate. We require 90 dB divided by 3 dB /octave, or 30 octaves. Thus, the required sampling rate, $\mathrm{f}_{\mathrm{s}}$, is

$$
f_{s}=2^{30} \times 2 f_{0} \cong 54,000 \mathrm{GHz}!
$$

This example shows why noise shaping is needed to improve the SQNR faster than $3 \mathrm{~dB} /$ octave, since $54,000 \mathrm{GHz}$ is highly impractical.

### 18.1.4 The Advantage of 1-Bit D/A Converters

While oversampling improves the signal-to-noise ratio, it does not improve linearity. For example, if a 16-bit linear converter is desired while using a 12 -bit converter with oversampling, the 12 -bit converter must have an integral nonlinearity error less than $1 / 2^{4}$ LSB (here, LSB refers to that for a 12-bit converter). In other words, the component accuracy would have to match better than 16-bit accuracy (i.e., $100 \times\left(1 / 2^{16}\right)=0.0015$ percent

Key Point: One-bit D/A converters are inherently linear. Hence, when combined with a high oversampling ratio, they can provide a good signal to quantization noise and distortion ratio.
accuracy). Thus, some sort of auto calibration or laser trimming must be used to obtain the required linearity. However, as we saw in Example 18.3, with a high enough sampling rate, the output from a 1-bit converter can be filtered to obtain the equivalent of a 16-bit converter. The advantage of a 1 -bit $D / A$ is that it is inherently linear. ${ }^{2}$ This linearity is a result of a 1-bit D/A converter having only two output values and, since two points define a straight line, no trimming or calibration is required. This inherent linearity is one of the major motivations for making use of oversampling techniques with 1-bit converters. In fact, the reader may be aware that many audio converters use 1-bit converters for realizing 16- to 18-bit linear converters (with noise shaping). In fact, 20-bit linearity has been reported without the need for any trimming [Leopold, 1991]. Finally, it should be mentioned that there are other advantages when using oversampling techniques, such as a reduced requirement for analog anti-aliasing and smoothing filters.

## 18.2 OVERSAMPLING WITH NOISE SHAPING

In this section, the advantage of noise shaping the quantization noise through the use of feedback is discussed. Here, we shall see a much more dramatic improvement in dynamic range when the input signal is oversampled as compared to oversampling the input signal with no noise shaping. Although this section illustrates the basic principles with reference to $\mathrm{A} / \mathrm{D}$ converters, much of it applies directly to $\Delta \Sigma \mathrm{D} / \mathrm{A}$ converters as well.

The system architecture of a $\Delta \Sigma$ oversampling $\mathrm{A} / \mathrm{D}$ converter is shown in Fig. 18.5. The first stage is a con-tinuous-time anti-aliasing filter and is required to band-limit the input signal to frequencies less than one-half the oversampling frequency, $\mathrm{f}_{\mathrm{s}}$. When the oversampling ratio is large, the anti-aliasing filter can often be quite simple, such as a simple RC low-pass filter. Following the anti-aliasing filter, the continuous-time signal, $\mathbf{x}_{\mathrm{c}}(\mathrm{t})$, is sampled by a sample and hold. This signal is then processed by the $\Delta \Sigma$ modulator, which converts the analog signal into a noise-shaped low-resolution digital signal. The third block in the system is a decimator. It converts the oversampled low-resolution digital signal into a high-resolution digital signal at a lower sampling rate usually equal to twice the frequency of the desired bandwidth of the input signal. The decimation filter can be conceptually thought of as a low-pass filter followed by a down sampler, although in many systems the decimation is performed in a number of stages. It should be mentioned that in many realizations where the $\Delta \Sigma$ modulator is realized using switched-capacitor circuitry, a separate sample-and-hold is not required, as the continuous-time signal
image_name:Fig. 18.5 Block diagram of an oversampling A/D converter
description:The block diagram represents an oversampling analog-to-digital (A/D) converter, which is designed to convert an analog input signal into a digital output. The system consists of several key components that work together to achieve this conversion process.

1. **Main Components:**
- **Anti-aliasing Filter:** This is the first block in the system, receiving the continuous-time input signal \(x_{in}(t)\). Its function is to remove high-frequency components from the signal to prevent aliasing during the sampling process.
- **Sample and Hold:** The filtered signal \(x_{c}(t)\) is then passed to the sample and hold circuit, which samples the continuous-time signal at a rate \(f_s\) and holds it to produce a discrete-time signal \(x_{sh}(t)\).
- **Delta-Sigma Modulator (ΔΣ mod):** This block receives the sampled signal \(x_{sh}(t)\) and performs noise shaping and quantization. It outputs a digital signal \(x_{dsm}(n)\) at the same sampling rate \(f_s\).
- **Digital Low-Pass Filter:** The digital signal \(x_{dsm}(n)\) is then processed by a digital low-pass filter, which removes quantization noise outside the signal band, resulting in \(x_{lp}(n)\).
- **Decimation Filter:** This consists of a downsampling operation (denoted by OSR, Oversampling Ratio) that reduces the sampling rate of the signal \(x_{lp}(n)\) to twice the frequency of the desired bandwidth \(2f_0\). The output is the final digital signal \(x_s(n)\).

2. **Flow of Information or Control:**
- The process begins with the continuous analog signal \(x_{in}(t)\), which flows through the anti-aliasing filter to become \(x_{c}(t)\).
- The sample and hold block samples this filtered signal, converting it into a discrete-time signal \(x_{sh}(t)\) at the sampling frequency \(f_s\).
- The discrete-time signal is then modulated by the Delta-Sigma modulator, producing a quantized digital signal \(x_{dsm}(n)\).
- The digital low-pass filter processes \(x_{dsm}(n)\) to remove out-of-band noise, resulting in \(x_{lp}(n)\).
- Finally, the decimation filter reduces the sampling rate of \(x_{lp}(n)\) to obtain the output signal \(x_s(n)\) at \(2f_0\).

3. **Labels, Annotations, and Key Indicators:**
- The diagram is clearly labeled with the function of each block and the signal at each stage (e.g., \(x_{in}(t)\), \(x_{c}(t)\), \(x_{sh}(t)\), \(x_{dsm}(n)\), \(x_{lp}(n)\), \(x_s(n)\)).
- The sampling frequency \(f_s\) is indicated at relevant stages.
- The decimation filter is highlighted with a dashed line, indicating its composite nature of filtering and downsampling.

4. **Overall System Function:**
- The primary function of this oversampling A/D converter is to accurately convert an analog signal into a digital signal while minimizing noise and distortion. The anti-aliasing filter, sample and hold, and Delta-Sigma modulator ensure high-quality sampling and noise shaping. The digital low-pass filter and decimation process refine the signal, ensuring that the final output \(x_s(n)\) is a high-fidelity digital representation of the original analog input \(x_{in}(t)\).

Fig. 18.5 Block diagram of an oversampling A/D converter.
2. This assumes that second-order errors due to imperfections such as signal-dependent power supply, or reference voltages, or memory in the $\mathrm{D} / \mathrm{A}$ converter are not present.
is inherently sampled by the switches and input capacitors of the SC $\Delta \Sigma$. In the next few sections the operation of the various building blocks will be described in greater detail.

### 18.2.1 Noise-Shaped Delta-Sigma Modulator

A general noise-shaped delta-sigma ( $\Delta \Sigma$ ) modulator and its linear model are shown in Fig. 18.6. This arrangement is known as an interpolative structure and is analogous to an amplifier realized using an opamp and feedback. In this analogy, the feedback reduces the effect of the noise of the output stage of the opamp in the closedloop amplifier's output signal at low frequencies when the opamp gain is high. At high frequencies, when the opamp's gain is low, the noise is not reduced. Note that the quantizer here is shown for the general case where many output levels occur. While many oversampling converters make use of 1-bit quantizers (i.e., only two output levels) due to reasons already discussed, there is certainly no reason to restrict ourselves to such implementations. Multibit oversampling converters are discussed in detail in Section 18.8.

Treating the linear model shown in Fig. 18.6(b) as having two independent inputs (which is an approximation), we can derive a signal transfer function, $\mathrm{S}_{\mathrm{TF}}(\mathrm{Z})$, and a noise transfer function, $\mathrm{N}_{T F}(\mathrm{Z})$.

$$
\begin{align*}
& S_{T F}(z) \equiv \frac{Y(z)}{U(z)}=\frac{H(z)}{1+H(z)}  \tag{18.15}\\
& N_{T F}(z) \equiv \frac{Y(z)}{E(z)}=\frac{1}{1+H(z)} \tag{18.16}
\end{align*}
$$

Note that the zeros of the noise transfer function, $N_{T F}(z)$, will be equal to the poles of $\mathrm{H}(\mathrm{z})$. In other words, when $H(z)$ goes to infinity, we see by (18.16) that $\mathrm{N}_{T F}(\mathrm{z})$ will go to zero. We can also write the output signal as the combination of the input signal and the noise signal, with each being filtered by the corresponding transfer function. In the frequency domain, we have

$$
\begin{equation*}
Y(z)=S_{T F}(z) U(z)+N_{T F}(z) E(z) \tag{18.17}
\end{equation*}
$$

image_name:(a)
description:The diagram labeled as (a) illustrates a general Delta-Sigma (ΔΣ) modulator, which is typically used in analog-to-digital conversion processes to shape quantization noise.

1. **Main Components:**
- **Adder/Subtractor Node (+):** This block receives the input signal \( u(n) \) and the feedback signal from the output \( y(n) \). It performs subtraction of the feedback signal from the input signal.
- **Transfer Function Block \( H(z) \):** This block processes the output of the adder. It represents the filter with a transfer function \( H(z) \), which is crucial for shaping the noise.
- **Quantizer:** This block receives the filtered signal \( x(n) \) from \( H(z) \) and converts it into a discrete level, introducing quantization noise.

2. **Flow of Information or Control:**
- The input signal \( u(n) \) is fed into the adder, where it is combined with the feedback signal from the output \( y(n) \).
- The result of this subtraction is processed by the filter \( H(z) \), producing the signal \( x(n) \).
- The signal \( x(n) \) is then quantized by the Quantizer block, producing the output \( y(n) \).
- The output \( y(n) \) is fed back to the adder, creating a feedback loop that is essential for noise shaping.

3. **Labels, Annotations, and Key Indicators:**
- The input is labeled as \( u(n) \), the intermediate signal after \( H(z) \) is labeled as \( x(n) \), and the output is labeled as \( y(n) \).
- The feedback path is clearly indicated, showing the subtraction operation at the adder.

4. **Overall System Function:**
- The primary function of this ΔΣ modulator is to shape the spectrum of quantization noise by placing it within a feedback loop. The transfer function \( H(z) \) is designed to attenuate quantization noise within a specific frequency band, allowing the system to improve the signal-to-noise ratio in the desired band. This is achieved by the feedback mechanism, which continuously adjusts the input to the quantizer based on the output, thereby controlling the noise characteristics effectively.

(a)
image_name:(a)
description:The diagram represents a general ΔΣ (Delta-Sigma) modulator, which is an interpolator structure used to shape the spectrum of quantization noise. This modulator is designed to improve the signal-to-noise ratio by attenuating quantization noise within a specific frequency band through a feedback mechanism.

1. **Main Components:**
- **Adder/Subtractor (Σ):** Positioned at the input, it receives the input signal \( u(n) \) and subtracts the feedback signal \( y(n) \). This operation generates the error signal that drives the modulator.
- **Transfer Function Block \( H(z) \):** This block processes the error signal to shape the noise spectrum. It is crucial for attenuating noise within the desired frequency band.
- **Second Adder (Σ):** This component adds the quantization noise \( e(n) \) to the processed signal \( x(n) \) to produce the output signal \( y(n) \).
- **Feedback Loop:** The output \( y(n) \) is fed back to the input subtractor, forming a closed-loop system that continuously adjusts to minimize quantization noise.

2. **Flow of Information or Control:**
- The input signal \( u(n) \) enters the system and is immediately combined with the feedback signal \( y(n) \) via the first adder/subtractor. The result is passed through the transfer function \( H(z) \), which shapes the signal.
- The output of \( H(z) \), denoted \( x(n) \), is then combined with the quantization noise \( e(n) \) in the second adder to produce the final output \( y(n) \).
- The feedback loop ensures that \( y(n) \) is continuously subtracted from \( u(n) \), allowing the system to dynamically adjust and control noise characteristics.

3. **Labels, Annotations, and Key Indicators:**
- \( u(n) \): Input signal.
- \( x(n) \): Intermediate signal after processing by \( H(z) \).
- \( e(n) \): Quantization noise added to the signal.
- \( y(n) \): Output signal, which is also used as feedback.

4. **Overall System Function:**
- The primary function of the ΔΣ modulator is to shape the quantization noise spectrum by placing it within a feedback loop. The transfer function \( H(z) \) is specifically designed to attenuate noise in a desired frequency band, thus enhancing the signal-to-noise ratio. This is achieved through the feedback mechanism, which allows the system to continuously adjust the input to the quantizer based on the output, effectively controlling the noise characteristics within the system.

(b)

Fig. 18.6 A modulator and its linear model: (a) a general $\Delta \Sigma$ modulator (interpolator structure); (b) linear model of the modulator showing injected quantization noise.

Key Point: To shape the spectrum of a quantization noise source, it is placed within a feedback loop whose response is designed to attenuate the quantization noise in the band of interest.

To noise-shape the quantization noise in a useful manner, we choose $H(z)$ such that its magnitude is large from 0 to $f_{0}$ (i.e., over the frequency band of interest). With such a choice, the signal transfer function, $\mathrm{S}_{\mathrm{TF}}(\mathrm{Z})$, will approximate unity over the frequency band of interest very similarly to an opamp in a unity-gain feedback configuration. Furthermore, the noise transfer function, $\mathrm{N}_{\mathrm{TF}}(\mathbf{z})$, will approximate zero over the same band. Thus, the quantization noise is reduced over the frequency band of interest while the signal itself is largely unaffected. The high-frequency noise is not reduced by the feedback as there is little loop gain at high frequencies. However, additional post filtering can remove the out-of-band quantization noise with little effect on the desired signal.

Before choosing specific functions for $\mathrm{H}(\mathrm{z})$, note that the maximum level of the in-band input signal, $\mathrm{u}(\mathrm{n})$, must remain within the maximum levels of the feedback signal, $\mathrm{y}(\mathrm{n})$; otherwise the large gain in $\mathrm{H}(\mathrm{z})$ will cause the signal $x(n)$ to saturate. For example, if a 1-bit quantizer having output levels of $\pm 1$ is used, the input signal must also remain within $\pm 1$ for frequencies where the gain of $H(z)$ is large. In fact, for many modulators the input signal needs to be significantly smaller than the bounds of the quantizer output levels to keep the modulator stable. ${ }^{3}$ However, the maximum level of the input signal, $u(n)$, for frequencies where the gain of $H(z)$ is small will not necessarily cause the signal $x(n)$ to saturate. In other words, the maximum level of the out-ofband input signal can be quite a bit larger than the feedback levels (see Problem 18.6).

### 18.2.2 First-Order Noise Shaping

Key Point: Using a single integrator inside a $\Delta \Sigma$ modulator feedback loop places a zero at dc in the noise transfer function providing firstorder noise shaping for low-pass signals.

To realize first-order noise shaping, the noise transfer function, $\mathrm{N}_{\mathrm{TF}}(\mathbf{z})$, should have a zero at dc (i.e., $\mathbf{z}=1$ ) so that the quantization noise is high-pass filtered. Since the zeros of $N_{T F}(z)$ are equal to the poles of $H(z)$, we can obtain first-order noise shaping by letting $H(z)$ be a discrete-time integrator (i.e., have a pole at z = 1). ${ }^{4}$ Specifically,

$$
\begin{equation*}
H(z)=\frac{1}{z-1} \tag{18.18}
\end{equation*}
$$

A block diagram for such a choice is shown in Fig. 18.7.
Time Domain View From a time domain point of view, if the feedback is operating correctly and the system is stable, then the signal $x(n)$ is bounded (i.e., $\neq \infty$ ). Since the integrator has infinite dc gain, the average value of the discrete-time integrator's input must exactly equal zero (i.e., average value of $u(n)-y(n)$ equals zero). This result implies that the average value (i.e., dc value) of $u(n)$ must equal the average value (i.e., dc value) of $y(n)$.
image_name:Fig. 18.7 A first-order noise-shaped interpolative modulator
description:The diagram represents a first-order noise-shaped interpolative modulator, which is a type of sigma-delta modulator used in digital signal processing. The system comprises the following key components:

1. **Summing Junctions:**
- There are two summing points in the system. The first summing junction takes the input signal \( u(n) \) and subtracts the feedback signal \( y(n) \). This difference is then passed to the next block.
- The second summing junction adds the output of the first summing junction with the feedback signal \( y(n) \) passed through a delay element.

2. **Integrator (\( z^{-1} \)):**
- The output of the second summing junction is fed into a discrete-time integrator, represented by the block \( z^{-1} \). This block accumulates the input signal over time, effectively performing integration in the discrete-time domain.

3. **Quantizer:**
- The integrator's output \( x(n) \) is fed into a quantizer block. The quantizer converts the continuous range of input values into discrete levels, introducing quantization noise.
- The output of the quantizer is the signal \( y(n) \), which is also fed back as a negative feedback loop to the first summing junction.

4. **Feedback Loop:**
- The feedback loop is critical for shaping the noise and ensuring system stability. It takes the output \( y(n) \) and feeds it back to the input of the first summing junction.

**Flow of Information:**
- The input signal \( u(n) \) enters the system and is combined with the feedback signal \( y(n) \) at the first summing junction.
- The result is then processed through the second summing junction and the integrator \( z^{-1} \), producing \( x(n) \).
- \( x(n) \) is quantized, resulting in the output \( y(n) \), which is also used as feedback.

**Overall System Function:**
- The primary function of this modulator is to shape the quantization noise and improve the signal-to-noise ratio (SNR) by pushing the noise to higher frequencies, where it can be filtered out more easily. This is achieved through the feedback mechanism and the integration process, which together help maintain stability and prevent overloading of the quantizer.

Fig. 18.7 A first-order noise-shaped interpolative modulator.
3. A modulator is defined to be stable if the input to the quantizer does not become so large as to cause the quantizer error to become greater than $\pm \Delta / 2$ (which is referred to as overloading the quantizer). See Section 18.7.
4. A continuous-time integrator can also be used, but discrete-time integrators are more popular in integrated realizations as they are less sensitive to sampling jitter and have better distortion characteristics.

Again, the similarity of this configuration and an opamp having unity-gain feedback is emphasized. The open-loop transfer function of an opamp is closely approximated by a first-order integrator having very large gain at low frequencies.

#### EXAMPLE 18.4

Find the output sequence and state values for a dc input, $u(n)$, of $1 / 3$ when a two-level quantizer of $\pm 1.0$ is used (threshold at zero) and the initial state for $\mathrm{x}(\mathrm{n})$ is 0.1 .

#### Solution

The output sequence and state values are given in Table 18.2.
Note that the average of $y(n)$ exactly equals $1 / 3$ as expected. However, also note that the output pattern is periodic, which implies that the quantization noise is not random in this example. (However, the result is much more satisfying than applying $1 / 3$ directly into a 1-bit quantizer using straight oversampling, which would give all 1 s as its output.)

Frequency Domain View From a frequency domain view, the signal transfer function, $\mathrm{S}_{\mathrm{TF}}(\mathrm{z})$, is given by

$$
\begin{equation*}
S_{T F}(z)=\frac{Y(Z)}{U(Z)}=\frac{1 /(Z-1)}{1+1 /(Z-1)}=Z^{-1} \tag{18.19}
\end{equation*}
$$

and the noise transfer function, $\mathrm{N}_{\mathrm{TF}}(\mathrm{Z})$, is given by

$$
\begin{equation*}
N_{T F}(z)=\frac{Y(z)}{E(z)}=\frac{1}{1+1 /(z-1)}=\left(1-z^{-1}\right) \tag{18.20}
\end{equation*}
$$

We see here that the signal transfer function is simply a delay, while the noise transfer function is a discrete-time differentiator (i.e., a high-pass filter).

To find the magnitude of the noise transfer function, $\left|N_{T F}(f)\right|$, we let $Z=e^{j \omega T}=e^{j 2 \pi t / f_{s}}$ and write the following:

$$
\begin{align*}
N_{T F}(f) & =1-e^{-j 2 \pi \tau / f_{s}}=\frac{e^{j \pi f / f_{s}}-e^{-j \pi t / f_{s}}}{2 j} \times 2 j \times e^{-j \pi t / f_{s}}  \tag{18.21}\\
& =\sin \left(\frac{\pi f}{f_{s}}\right) \times 2 j \times e^{-j \pi f / f_{s}}
\end{align*}
$$

Table 18.2 First-order modulator example.

| $\mathbf{n}$ | $\mathbf{x}(\mathbf{n})$ | $\mathbf{x}(\mathbf{n}+\mathbf{1})$ | $\mathbf{y ( n )}$ | $\mathbf{e ( n )}$ |
| :---: | :---: | :---: | :---: | :---: |
| 0 | 0.1 | -0.5667 | 1.0 | 0.9 |
| 1 | -0.5667 | 0.7667 | -1.0 | -0.4333 |
| 2 | 0.7667 | 0.1 | 1.0 | 0.2333 |
| 3 | 0.1 | -0.5667 | 1.0 | 0.9 |
| 4 | -0.5667 | 0.7667 | -1.0 | -0.4333 |
| 5 | $\ldots$ | $\cdots$ | $\cdots$ | $\cdots$ |

Taking the magnitude of both sides, we have the high-pass function

$$
\begin{equation*}
\left|N_{T F}(f)\right|=2 \sin \left(\frac{\pi f}{f_{s}}\right) \tag{18.22}
\end{equation*}
$$

Now the quantization noise power over the frequency band from 0 to $f_{0}$ is given by

$$
\begin{equation*}
P_{e}=\int_{-f_{0}}^{f_{0}} S_{e}^{2}(f)\left|N_{T F}(f)\right|^{2} d f=\int_{-f_{0}}^{f_{0}}\left(\frac{\Delta^{2}}{12}\right) \frac{1}{f_{s}}\left[2 \sin \left(\frac{\pi f}{f_{s}}\right)\right]^{2} d f \tag{18.23}
\end{equation*}
$$

and making the approximation that $f_{0}<<f_{s}$ (i.e., OSR $>>1$ ), so that we can approximate $\sin \left((\pi f) / f_{s}\right)$ to be $(\pi f) / f_{s}$, we have

$$
\begin{equation*}
\mathrm{P}_{\mathrm{e}} \cong\left(\frac{\Delta^{2}}{12}\right)\left(\frac{\pi^{2}}{3}\right)\left(\frac{2 \mathrm{f}_{0}}{\mathrm{f}_{\mathrm{s}}}\right)^{3}=\frac{\Delta^{2} \pi^{2}}{36}\left(\frac{1}{\mathrm{OSR}}\right)^{3} \tag{18.24}
\end{equation*}
$$

Assuming the maximum signal power is the same as that obtained before in (18.11), the maximum SNR for this case is given by

$$
\begin{equation*}
\mathrm{SQNR}_{\max }=10 \log \left(\frac{\mathrm{P}_{\mathrm{s}}}{\mathrm{P}_{\mathrm{e}}}\right)=10 \log \left(\frac{3}{2} 2^{2 \mathrm{~N}}\right)+10 \log \left[\frac{3}{\pi^{2}}(\mathrm{OSR})^{3}\right] \tag{18.25}
\end{equation*}
$$

or, equivalently,

$$
\begin{equation*}
\mathrm{SQNR}_{\max }=6.02 \mathrm{~N}+1.76-5.17+30 \log (\mathrm{OSR}) \tag{18.26}
\end{equation*}
$$

Key Point: First-order noise shaping permits SQNR to increase by 1.5 bits/octave with respect to oversampling ratio, or 9 dB for every doubling of OSR.

We see here that doubling the OSR gives an SQNR improvement for a first-order modulator of 9 dB or, equivalently, a gain of 1.5 bits/octave. This result should be compared to the 0.5 bits/octave when oversampling with no noise shaping.

### 18.2.3 Switched-Capacitor Realization of a First-Order A/D Converter

It is possible to realize a first-order modulator using switched-capacitor (SC) techniques. An example of a firstorder modulator where a 1-bit quantizer is used in the feedback loop is shown in Fig. 18.8. Here, the $\Delta \Sigma$ modulator consists of both analog and digital circuitry. It should be mentioned that the two input capacitances to the discrete-time integrator in Fig. 18.8 can be combined to one capacitance, as shown in Fig. 18.9 [Boser, 1988]. However, such an approach does not easily allow scaling of the feedback signal relative to the input signal.

### 18.2.4 Second-Order Noise Shaping

The modulator shown in Fig. 18.10 realizes second-order noise shaping (i.e., the noise transfer function, $\mathrm{N}_{T F}(\mathrm{z})$, is a second-order high-pass function). For this modulator, the signal transfer function is given by

$$
\begin{equation*}
S_{T F}(f)=z^{-1} \tag{18.27}
\end{equation*}
$$

image_name:Fig. 18.8(a)
description:The block diagram in Fig. 18.8 represents a second-order noise-shaping modulator. The primary components of this system include an adder, a delay element, a feedback loop with a digital-to-analog converter (D/A), and a quantizer.

1. **Main Components:**
- **Adder:** The input signal \( u(n) \) is first fed into an adder, which subtracts the feedback signal from the input.
- **Delay Element (\( z^{-1} \)):** The output of the adder is passed through a delay element, which is a part of the filter \( H(z) \). This delay introduces a unit sample delay to the signal.
- **Quantizer:** The delayed signal is then quantized. The quantizer converts the analog signal into a digital signal, \( y(n) \).
- **1-bit D/A Converter:** The output from the quantizer is fed back through a 1-bit digital-to-analog converter, which converts the digital signal back to an analog form to be subtracted from the input signal.

2. **Flow of Information or Control:**
- The input signal \( u(n) \) is combined with the feedback signal from the 1-bit D/A in the adder. The resultant error signal is then passed through the delay element \( z^{-1} \).
- The delayed signal is quantized by the quantizer. The quantizer's output is the digital output \( y(n) \), which is also fed back into the system.
- The feedback loop, comprising the 1-bit D/A converter, provides a feedback signal that is subtracted from the input signal at the adder to complete the loop.

3. **Labels, Annotations, and Key Indicators:**
- The system is labeled with input \( u(n) \) and output \( y(n) \) signals.
- The feedback path is clearly indicated, showing the conversion from digital back to analog.
- The filter \( H(z) \) is denoted, indicating its role in shaping the noise.

4. **Overall System Function:**
- This system is designed to perform second-order noise shaping. The arrangement of the components allows for high-pass filtering of quantization noise, effectively pushing the noise to higher frequencies where it can be more easily filtered out. The use of feedback and the quantizer enables the system to convert an analog input signal into a digital output with reduced noise in the desired frequency band.

image_name:Fig. 18.8(b) switched-capacitor implementation
description:This is a first-order A/D modulator using a switched-capacitor implementation. The circuit performs analog-to-digital conversion by integrating the input signal and comparing it to a reference voltage. The output is latched on the falling edge of φ2, and the switches are controlled by clock phases φ1 and φ2.

Fig. 18.8 First-order A/D modulator: (a) block diagram; (b) switched-capacitor implementation.
image_name:Fig. 18.9
description:This circuit is a first-order A/D modulator using a switched-capacitor implementation. It integrates the input signal and compares it to a reference voltage. The output is latched on the falling edge of φ2, with switches controlled by clock phases φ1 and φ2.
Fig. 18.9 First-order A/D modulator using only one input capacitance to the discrete-time integrator.

image_name:Fig. 18.10 Second-order ΔΣ modulator
description:The diagram illustrates a second-order Delta-Sigma (ΔΣ) modulator, which is a type of analog-to-digital converter used to achieve high-resolution digital signals from analog inputs. The primary components and their interactions are as follows:

1. **Input Signal (u(n))**: The process begins with the input signal, denoted as u(n), which is fed into the system.

2. **Summing Junctions**: There are two summing junctions at the beginning of the diagram. The first one subtracts the feedback signal from the input signal, u(n). The output of this summing junction is then fed into a delay block.

3. **Delay Blocks (z⁻¹)**: Two delay blocks are present in the system, representing discrete-time delay elements. They are used to store the previous output state, which is crucial for implementing the integrative behavior required for noise shaping in ΔΣ modulators.

4. **Feedback Loops**: The system features feedback loops that take the output signal, y(n), and feed it back into the summing junctions. This feedback is essential for the noise shaping properties of the ΔΣ modulator, allowing the system to push quantization noise out of the band of interest.

5. **Quantizer**: Following the second delay block, the signal is fed into a quantizer. The quantizer converts the continuous-time signal into a discrete-time digital signal, which is the primary output of the modulator, y(n).

6. **Output Signal (y(n))**: The output of the quantizer is the digital representation of the input analog signal, with improved resolution due to the noise shaping properties of the system.

**Overall System Function**: The second-order ΔΣ modulator uses its integrative and feedback properties to shape the quantization noise away from the frequency band of interest. By doing so, it achieves a high-resolution digital output from an analog input signal. The combination of summing junctions, delay elements, feedback loops, and the quantizer work together to perform this function effectively.

Fig. 18.10 Second-order $\Delta \Sigma$ modulator.
and the noise transfer function is given by

$$
\begin{equation*}
N_{T F}(f)=\left(1-z^{-1}\right)^{2} \tag{18.28}
\end{equation*}
$$

Additionally, the magnitude of the noise transfer function can be shown to be given by

$$
\begin{equation*}
\left|N_{T F}(f)\right|=\left[2 \sin \left(\frac{\pi f}{f_{s}}\right)\right]^{2} \tag{18.29}
\end{equation*}
$$

resulting in the quantization noise power over the frequency band of interest being given by

$$
\begin{equation*}
\mathrm{P}_{\mathrm{e}} \cong \frac{\Delta^{2} \pi^{4}}{60}\left(\frac{1}{\mathrm{OSR}}\right)^{5} \tag{18.30}
\end{equation*}
$$

Again, assuming the maximum signal power is that obtained in (18.11), the maximum SQNR for this case is given by

$$
\begin{equation*}
\mathrm{SQNR}_{\max }=10 \log \left(\frac{\mathrm{P}_{\mathrm{s}}}{\mathrm{P}_{\mathrm{e}}}\right)=10 \log \left(\frac{3}{2} 2^{2 \mathrm{~N}}\right)+10 \log \left[\frac{5}{\pi^{4}}(\mathrm{OSR})^{5}\right] \tag{18.31}
\end{equation*}
$$

or, equivalently,

$$
\begin{equation*}
\mathrm{SQNR}_{\max }=6.02 \mathrm{~N}+1.76-12.9+50 \log (\mathrm{OSR}) \tag{18.32}
\end{equation*}
$$

Key Point: Second-order noise shaping increases SQNR by 15 dB for each doubling of OSR, or equivalently by 1.5 bits/octave.

We see here that doubling the OSR improves the SQNR for a second-order modulator by 15 dB or, equivalently, a gain of 2.5 bits/octave.

The realization of the second-order modulator using switched-capacitor techniques is left as an exercise for the interested reader.

### 18.2.5 Noise Transfer-Function Curves

The general shape of zero-, first-, and second-order noise-shaping curves are shown in Fig. 18.11. Note that over the band of interest (i.e., from 0 to $f_{0}$ ), the noise power decreases as the noise-shaping order increases. However, the out-of-band noise increases for the higher-order modulators.
image_name:Fig. 18.11
description:The graph in Fig. 18.11 is a Bode plot representing different noise transfer functions (NTFs) for zero-, first-, and second-order noise shaping in a digital signal processing context. The x-axis is labeled with frequency \( f \), ranging from 0 to \( f_s \) (the sampling frequency), with a midpoint marked as \( \frac{f_s}{2} \). The y-axis represents the magnitude of the noise transfer function \( |N_{TF}(f)| \).

The graph displays three curves:

1. **No Noise Shaping:** This is represented by a flat line across the frequency range, indicating a constant noise level throughout.

2. **First-Order Noise Shaping:** This curve starts at the same level as the flat line at \( f = 0 \), rises to a peak before \( \frac{f_s}{2} \), and then descends symmetrically back to the baseline at \( f_s \). This indicates that the noise is reduced in the frequency band of interest and increased outside of it.

3. **Second-Order Noise Shaping:** This curve follows a similar pattern to the first-order curve but with a more pronounced peak and steeper slopes. It starts at the baseline at \( f = 0 \), rises to a higher peak than the first-order curve, and then descends back to the baseline at \( f_s \). This suggests even greater noise reduction within the band of interest but more significant noise increase outside of it.

The overall behavior indicates that higher-order noise shaping results in more effective noise reduction within the desired frequency band, though it also increases out-of-band noise. This is a common trade-off in noise shaping techniques used in digital signal processing systems.

Fig. 18.11 Some different noise-shaping transfer functions.

#### EXAMPLE 18.5

Given that a 1-bit A/D converter has a $6-\mathrm{dB}$ SQNR, what sample rate is required to obtain a $96-\mathrm{dB}$ SNR (or 16 bits) if $\mathrm{f}_{0}=25 \mathrm{kHz}$ for straight oversampling as well as first- and second-order noise shaping?

#### Solution

Oversampling with No Noise Shaping From Example 18.3, straight oversampling requires a sampling rate of 54,000 GHz.

First-Order Noise Shaping First-order noise shaping gives $9 \mathrm{~dB} /$ octave where 1 octave is doubling the OSR. Since we lose 5 dB , we require 95 dB divided by $9 \mathrm{~dB} /$ octave, or 10.56 octaves. Thus, the required sampling rate, $f_{s}$, is

$$
f_{s}=2^{10.56} \times 2 f_{0} \cong 75 \mathrm{MHz}
$$

This compares very favorably with straight oversampling, though it is still quite high.
Second-Order Noise Shaping Second-order noise shaping gives $15 \mathrm{~dB} /$ octave, but loses 13 dB . Thus we required 103 dB divided by $15 \mathrm{~dB} /$ octave, resulting in a required sampling rate of only 5.8 MHz . However, this simple calculation does not take into account the reduced input range for a second-order modulator needed for stability.

### 18.2.6 Quantization Noise Power of 1-Bit Modulators

Assuming the output of a 1 -bit modulator is $\pm 1$, then one can immediately determine the total power of the output signal, $y(n)$, to be a normalized power of 1 watt. Since $y(n)$ consists of both signal and quantization noise, it is clear that the signal power can never be greater than 1 watt. In fact, as alluded to earlier, the signal level is often limited to well below the $\pm 1$ level in higher-order modulators to maintain stability. For example, assuming that the maximum peak signal level is

Key Point: The input signal power is often limited to well below the maximum quantizerswing to ensure stability, resulting in reduced SQNR.
only $\pm 0.25$, then the maximum signal power is 62.5 mW (referenced to a $1 \Omega$ load). This would imply a signal power approximately 12 dB less than is predicted by (18.11) and a corresponding reduction in the SQNR estimates that follow from (18.11). Since the signal power plus quantization noise power equals 1 W , in this example the maximum signal power is about 12 dB below the total quantization noise power. Fortunately, as we saw above, the quantization noise power is mostly in a different frequency region than the signal power and can therefore be filtered out. Note, however, that the filter must have a dynamic range capable of accommodating the full power of $y(n)$ at its input. For a $\Delta \Sigma A / D$ converter, the filtering would be done by digital filters following the quantizer.

### 18.2.7 Error-Feedback Structure

Before leaving this section, it is of interest to look at another structure for realizing a delta-sigma modulator-an error-feedback structure, as shown in Fig. 18.12 [Anastassiou, 1989]. Using a linear model for the quantizer, it is not difficult to show that this error-feedback structure has a signal transfer function, $\mathrm{S}_{\mathrm{TF}}(\mathrm{z})$, equal to unity while
image_name:Fig. 18.12
description:The diagram in Fig. 18.12 represents an error-feedback structure of a general Delta-Sigma (ΔΣ) modulator. The primary components of this system include:

1. **Summation Blocks:**
- The first summation block receives the input signal \(u(n)\) and a feedback signal, producing the intermediate signal \(x(n)\).
- The second summation block takes the output of the quantizer and subtracts it from \(x(n)\) to produce the error signal \(e(n)\).

2. **Quantizer:**
- The quantizer processes the signal \(x(n)\) and outputs a quantized version, \(y(n)\). This is typically a non-linear block that introduces quantization noise.

3. **Feedback Path with Transfer Function \(G(z) - 1\):**
- The feedback path includes a block labeled \(G(z) - 1\), which processes the error signal \(e(n)\) and feeds it back to the first summation block.

**Flow of Information:**
- The input signal \(u(n)\) enters the system at the first summation block, where it is combined with the feedback signal from the \(G(z) - 1\) block.
- The result, \(x(n)\), is then quantized by the quantizer, producing the output \(y(n)\).
- The quantized output is subtracted from \(x(n)\) in the second summation block to generate the error signal \(e(n)\).
- The error signal \(e(n)\) is processed by the \(G(z) - 1\) block and fed back to the first summation block.

**Overall System Function:**
- The primary function of this error-feedback ΔΣ modulator is to achieve noise shaping. By having the signal transfer function \(\mathrm{S}_{\mathrm{TF}}(z)\) equal to unity and the noise transfer function \(N_{TF}(z)\) equal to \(G(z)\), the system effectively shapes the quantization noise, pushing it out of the band of interest. This is particularly beneficial in applications requiring high precision, such as in digital audio or communications systems.

**Labels and Annotations:**
- Inputs and outputs are clearly labeled as \(u(n)\), \(x(n)\), \(e(n)\), and \(y(n)\), which helps in understanding the flow and transformation of signals through the system.

Fig. 18.12 The error-feedback structure of a general $\Delta \Sigma$ modulator.
the noise transfer function, $N_{T F}(z)$, equals $G(z)$. Thus for a first-order modulator, $G(z)=1-z^{-1}$, or in other words, the block $(G(z)-1)$ is simply $-z^{-1}$.

Unfortunately, a slight coefficient error can cause significant noise-shaping degradation with this errorfeedback structure. For example, in a first-order case, if the delayed signal becomes $-0.99 z^{-1}$ (rather than $-z^{-1}$ ), then $G(z)=1-0.99 z^{-1}$, and the zero is moved off dc. Such a shift of the zero will result in the quantization noise not being fully nulled at dc and therefore would not be suitable for high oversampling ratios. Thus, this structure is not well suited to analog implementations where coefficient mismatch occurs. In contrast, an interpolative structure has the advantage that the zeros of the noise transfer function remain at dc as long as $\mathrm{H}(\mathrm{z})$ has infinite gain at dc. This high gain at dc can usually be obtained in analog implementations by using opamps with large open-loop gains and does not rely on component matching. The error feedback structure is discussed here because it is useful for analysis purposes and can work well for fully digital implementations (such as in D/A converters) where no coefficient mismatches occur.

A second-order modulator based on the error-feedback structure is shown in Fig. 18.13. For this case we have

$$
\begin{equation*}
G(z)-1=z^{-1}\left(z^{-1}-2\right) \tag{18.33}
\end{equation*}
$$

implying that

$$
\begin{align*}
\mathrm{G}(\mathrm{z}) & =1-2 \mathrm{z}^{-1}+\mathrm{z}^{-2} \\
& =\left(1-\mathrm{z}^{-1}\right)^{2} \tag{18.34}
\end{align*}
$$

which is identical to (18.28), and we see that second-order noise shaping is obtained. In practical realizations, one might have to take into account additional details such as preventing overflow and reducing complexity. For these more advanced topics, the reader is referred to [Temes, 1996].
image_name:Fig. 18.13
description:The system block diagram in Fig. 18.13 represents the error-feedback structure of a second-order Delta-Sigma (ΔΣ) modulator. This architecture is used in oversampled analog-to-digital (A/D) converters to shape quantization noise and improve signal-to-noise ratio (SNR).

Main Components:
1. **Adder (Σ)**: The diagram includes two summing nodes (adders). The first adder combines the input signal \(u(n)\) with the feedback signal.
2. **Delay Elements (\(z^{-1}\))**: There are two delay blocks in the feedback path. These introduce a unit delay in the signals, implementing the z-transform delay operation.
3. **Gain Block (2)**: This block amplifies the delayed signal by a factor of 2, which is part of the feedback loop.
4. **Quantizer**: The central block in the diagram is a quantizer, which converts the analog signal \(x(n)\) into a digital signal \(y(n)\). The quantizer is typically a non-linear element that introduces quantization noise into the system.
5. **Error Signal (e(n))**: The second adder calculates the error signal \(e(n)\) by subtracting the feedback from the quantizer output.

Flow of Information or Control:
- The input signal \(u(n)\) enters the system through the first adder, where it is combined with a feedback signal.
- The result \(x(n)\) is passed to the quantizer, which outputs the digital signal \(y(n)\).
- The quantizer output \(y(n)\) is fed back, and the error signal \(e(n)\) is computed by subtracting the feedback signal from \(x(n)\).
- The error signal \(e(n)\) is then delayed and amplified by a factor of 2, forming part of the feedback loop that shapes the noise.

Labels, Annotations, and Key Indicators:
- The input is labeled \(u(n)\), the output is \(y(n)\), and intermediate signals are labeled \(x(n)\) and \(e(n)\).
- Delay elements are labeled with \(z^{-1}\) to indicate their function in the z-domain.
- The gain block is labeled with a "2" to indicate the amplification factor.

Overall System Function:
The primary function of this second-order ΔΣ modulator is to perform noise shaping on the input signal. The feedback loop, consisting of delay elements and a gain block, modifies the quantization noise characteristics, pushing the noise to higher frequencies where it can be more easily filtered out. This enhances the SNR of the A/D conversion process, making it suitable for high-resolution digital audio and other precision applications.

Fig. 18.13 The error-feedback structure of a second-order $\Delta \Sigma$ modulator.

## 18.3 SYSTEM ARCHITECTURES

In this section, we look at typical system architectures for oversampled $A / D$ and $D / A$ converters.

### 18.3.1 System Architecture of Delta-Sigma A/D Converters

The system architecture for a typical $\Delta \Sigma$ oversampling A/D converter is shown in Fig. 18.14, and some example signal spectra are shown in Fig. 18.15. In the case of digital audio, various sampling frequencies might be $f_{s}=5.6448 \mathrm{MHz}, f_{0}=44.1 \mathrm{kHz}$, which represent an oversampling ratio of 128 . Here, the input signal, $x_{c}(t)$, is sampled and held, ${ }^{5}$ resulting in the signal $x_{\text {sh }}(t)$. This sampled-and-held signal is then applied to an $A / D \Delta \Sigma$ modulator, which has as its output a 1-bit digital signal $\mathrm{x}_{\mathrm{dsm}}(\mathrm{n})$. This 1-bit digital signal is assumed to be linearly related to the input signal $\mathrm{x}_{\mathrm{c}}(\mathrm{t})$ (accurate to many bits of resolution), although it includes a large amount of out-of-band quantization noise. To remove this out-of-band quantization noise, a digital decimation filter is used as shown. Conceptually, one can think of the decimation process as first reducing the quantization noise through the use of a digital low-pass filter, resulting in the multi-bit signal $x_{1 p}(n)$. Note that this low-pass filter will also remove any higher-frequency signal content that was originally on the input signal, $\mathrm{x}_{\mathrm{c}}(\mathrm{t})$, and thus also acts as an anti-aliasing filter to limit signals to one-half the final output sampling rate, $2 \mathrm{f}_{0}$, as opposed to the anti-aliasing filter at the input, which needed to only limit signals to frequencies less than $f_{s} / 2$. By contrast, in a Nyquist-rate $A / D$ converter, where $f_{s}$ is only slightly greater than $2 f_{0}$, the analog anti-aliasing filter must have a very sharp cutoff to prevent unwanted signal content (including thermal noise) from aliasing into the band of interest. Hence, oversampling A/D converters require additional digital lowpass filtering, but less analog antialiasing filtering-often an desirable trade-off in integrated circuits.

Next, $x_{1 p}(n)$ is resampled at $2 f_{0}$ to obtain $x_{s}(n)$ by simply keeping samples at a submultiple of the oversampling rate and throwing away the rest. In Fig. 18.15 an oversampling rate of only 6 is shown for clarity as opposed to the more typical values of 64 or 128 that are used in many commercial applications. This decimation process does not result in any loss of information, since the bandwidth of the original signal was assumed to be $f_{0}$. In other words, the signal $x_{10}(n)$ has redundant information since it is an oversampled signal where all of its spectral information

Key Point: Oversampling A/D converters require additional digital low-pass filtering, but less analog anti-aliasing filteringoften andesirable trade-off in integrated circuits.
lies well below $\pi$, and by throwing away samples, the spectral information is spread over 0 to $\pi$. Finally, it should be noted that there is no need to actually create the signal $x_{1 p}(n)$, and much digital circuit complexity can be saved by combining the digital low-pass filter with the resampling block to directly
image_name:Fig. 18.14 Block diagram of an oversampling A/D converter
description:The block diagram of an oversampling A/D converter consists of several key components that work together to convert an analog input signal into a digital output signal. The system is divided into two main sections: Analog and Digital.

1. **Main Components:**
- **Anti-aliasing Filter:** This is the first block that the input signal \( x_{in}(t) \) encounters. It is responsible for removing high-frequency components from the signal to prevent aliasing during sampling. The output of this block is \( x_{c}(t) \).
- **Sample and Hold:** This block captures the filtered analog signal at discrete time intervals, producing \( x_{sh}(t) \). It operates at a sampling frequency \( f_s \).
- **Delta-Sigma Modulator (ΔΣ Mod):** This block processes the sampled signal \( x_{sh}(t) \) to produce a high-frequency, low-resolution digital output \( x_{dsm}(n) \). The modulator shapes the quantization noise, pushing it out of the band of interest.
- **Digital Low-pass Filter:** Part of the decimation filter block, it removes the out-of-band noise shaped by the delta-sigma modulator, resulting in \( x_{lp}(n) \).
- **Decimation Filter (OSR):** The oversampling ratio (OSR) block reduces the sampling rate by discarding samples, effectively downsampling the signal to produce \( x_{s}(n) \) at a frequency of \( 2f_0 \).

2. **Flow of Information or Control:**
- The analog signal \( x_{in}(t) \) flows through the anti-aliasing filter, becoming \( x_{c}(t) \).
- This filtered signal is then discretely captured by the sample and hold block, producing \( x_{sh}(t) \).
- The delta-sigma modulator processes \( x_{sh}(t) \) to create a high-frequency digital signal \( x_{dsm}(n) \).
- The digital low-pass filter refines \( x_{dsm}(n) \) by removing unwanted noise, resulting in \( x_{lp}(n) \).
- Finally, the decimation filter reduces the data rate, outputting the final digital signal \( x_{s}(n) \).

3. **Labels, Annotations, and Key Indicators:**
- The diagram is labeled with the type of signal at each stage (e.g., \( x_{in}(t) \), \( x_{c}(t) \), \( x_{sh}(t) \), etc.).
- The sampling frequency \( f_s \) is indicated at the sample and hold and delta-sigma modulator stages.
- The oversampling ratio (OSR) is noted in the decimation filter block.

4. **Overall System Function:**
- The primary function of this oversampling A/D converter is to convert an analog input signal into a digital output signal with reduced noise and aliasing effects. The use of oversampling and noise shaping via the delta-sigma modulator allows for a more precise digital representation of the analog signal, with the digital low-pass and decimation filters ensuring that the final output is at the desired sampling rate and free from unwanted noise.

Fig. 18.14 Block diagram of an oversampling A/D converter.
5. This sample-and-hold block is often inherent in the switched-capacitor modulator. Thus, the signal $X_{s h}(t)$ may never physically exist in many realizations.
image_name:x_c(t)
description:The diagram illustrates the signals and spectra at various stages in an oversampling A/D converter process. It is divided into time-domain waveforms on the left and frequency-domain representations on the right.

Time-Domain Waveforms:
1. **$x_c(t)$**:
- **Type:** Continuous time waveform.
- **Description:** This is a sinusoidal waveform representing the continuous-time input signal.
- **Axes:**
- Horizontal: Time ($t$)
- Vertical: Amplitude

2. **$x_{sh}(t)$**:
- **Type:** Sample-and-hold waveform.
- **Description:** A stepped waveform indicating the sample-and-hold operation on the continuous signal, showing discrete time samples.
- **Axes:**
- Horizontal: Time ($t$)
- Vertical: Amplitude

3. **$x_{dsm}(n)$**:
- **Type:** Discrete sequence.
- **Description:** Represents the output from the delta-sigma modulator, with values alternating between +1 and -1.
- **Axes:**
- Horizontal: Sample index ($n$)
- Vertical: Amplitude

4. **$x_{lp}(n)$**:
- **Type:** Low-pass filtered discrete sequence.
- **Description:** A smoothed version of the delta-sigma modulated signal, showing the effects of low-pass filtering.
- **Axes:**
- Horizontal: Sample index ($n$)
- Vertical: Amplitude

5. **$x_s(n)$**:
- **Type:** Downsampled sequence.
- **Description:** The final downsampled signal showing fewer samples, representing the digital output at a lower sampling rate.
- **Axes:**
- Horizontal: Sample index ($n$)
- Vertical: Amplitude

Frequency-Domain Representations:
1. **$X_c(f)$**:
- **Description:** Frequency spectrum of the continuous input signal, centered around a frequency $f_0$.
- **Axes:**
- Horizontal: Frequency ($f$)
- Vertical: Amplitude

2. **$X_{sh}(f)$**:
- **Description:** Spectrum after sample-and-hold, showing replicas of the original spectrum at multiples of the sampling frequency $f_s$.
- **Axes:**
- Horizontal: Frequency ($f$)
- Vertical: Amplitude

3. **$X_{dsm}(\omega)$**:
- **Description:** Spectrum of the delta-sigma modulated signal, showing noise shaping with a broad peak.
- **Axes:**
- Horizontal: Angular frequency ($\omega$)
- Vertical: Amplitude

4. **$X_{lp}(\omega)$**:
- **Description:** Spectrum after low-pass filtering, showing reduced high-frequency components.
- **Axes:**
- Horizontal: Angular frequency ($\omega$)
- Vertical: Amplitude

5. **$X_s(\omega)$**:
- **Description:** Final spectrum of the downsampled signal, showing a repeated pattern due to downsampling.
- **Axes:**
- Horizontal: Angular frequency ($\omega$)
- Vertical: Amplitude

Key Features:
- The diagram highlights the transformation of the signal from continuous to discrete form and the associated spectral changes at each stage.
- Noise shaping is evident in the delta-sigma modulation stage, which spreads quantization noise over a wider frequency range.
- The low-pass filtering stage smooths the signal, removing high-frequency noise components before downsampling.
image_name:x_sh(t)
description:The diagram illustrates the signals and their corresponding frequency spectra at different stages of an oversampling A/D converter. It includes both time-domain waveforms and frequency-domain representations.

1. **Signals in Time Domain:**
- **$x_c(t)$:** This is a continuous-time signal depicted as a smooth sinusoidal waveform. It represents the original analog signal before sampling.
- **$x_{sh}(t)$:** Following $x_c(t)$, this signal is a staircase approximation of the sinusoid, indicating the sample-and-hold process. It retains the overall shape of $x_c(t)$ but in a stepped manner.
- **$x_{dsm}(n)$:** This is a discrete-time signal representing the output of the delta-sigma modulator. It consists of high-frequency components with values alternating between +1 and -1, indicative of the quantization noise shaping.
- **$x_{lp}(n)$:** This signal is a low-pass filtered version of $x_{dsm}(n)$. It appears smoother and approximates the original sinusoidal shape, representing the decimated output.
- **$x_s(n)$:** This is the final downsampled signal, showing a reduced sample rate and retaining the sinusoidal shape.

2. **Frequency Domain Representations:**
- **$X_c(f)$:** The spectrum of the continuous-time signal $x_c(t)$ shows a single frequency component at $f_0$, with no harmonics visible.
- **$X_{sh}(f)$:** The spectrum of $x_{sh}(t)$ is similar to $X_c(f)$ but with additional spectral replicas around multiples of the sampling frequency $f_s$ due to the sample-and-hold process.
- **$X_{dsm}(\omega)$:** This spectrum shows a broadened frequency response due to the noise shaping of the delta-sigma modulator, with a distinct peak at $2\pi f_0/f_s$ and noise pushed to higher frequencies.
- **$X_{lp}(\omega)$:** The low-pass filtered spectrum of $x_{lp}(n)$ shows a reduction in high-frequency noise, focusing energy around $2\pi f_0/f_s$.
- **$X_s(\omega)$:** The final spectrum of the downsampled signal $x_s(n)$ displays periodicity with components at multiples of $\pi$, indicating the discrete nature of the final digital signal.

Overall, this diagram effectively demonstrates the transformation of an analog signal through oversampling and noise shaping, highlighting the role of each stage in preserving signal integrity while reducing noise.
image_name:x_dsm(n)
description:The diagram titled "x_dsm(n)" illustrates the signals and spectra in an oversampling A/D converter, focusing on the behavior of different signals throughout the conversion process. The figure is divided into two main sections: time-domain waveforms on the left and their corresponding frequency spectra on the right.

1. **Type of Graph and Function:**
- The graph is a combination of time-domain waveforms and frequency-domain spectra, showcasing the process of oversampling and noise shaping in a delta-sigma modulator.

2. **Axes Labels and Units:**
- The time-domain graphs on the left have time (t) or sample number (n) on the horizontal axis and amplitude on the vertical axis.
- The frequency-domain graphs on the right have frequency (f or ω) on the horizontal axis and amplitude on the vertical axis.

3. **Overall Behavior and Trends:**
- The first row shows an analog input signal $x_c(t)$ as a continuous waveform and its sampled version $x_{sh}(t)$ as a stepped waveform, indicating the sample-and-hold process.
- The second row illustrates $x_{dsm}(n)$, showing a discrete sequence of values, typically ±1, representing the output from the delta-sigma modulator.
- The third row shows $x_{lp}(n)$, a low-pass filtered version of the modulated signal, as a smoother waveform.
- The fourth row presents $x_s(n)$, the final downsampled signal, as a sequence of discrete samples.

4. **Key Features and Technical Details:**
- In the frequency domain, $X_c(f)$ and $X_{sh}(f)$ show the original and sampled signal spectra, with main components at $f_0$ and mirrored images around $f_s$.
- $X_{dsm}(ω)$ displays a noise-shaped spectrum, spreading quantization noise over a wider bandwidth.
- $X_{lp}(ω)$ represents the low-pass filtered spectrum, focusing energy around the original signal frequency.
- $X_s(ω)$ shows the spectrum of the downsampled signal, with repeated spectral images across the frequency axis.

5. **Annotations and Specific Data Points:**
- Key frequencies are marked, such as $f_0$, $f_s$, and $2πf_0/f_s$.
- The frequency spectra indicate the presence of spectral images and the effect of oversampling and filtering on the signal.

This detailed view illustrates how oversampling and noise shaping via the delta-sigma modulator enhance the digital representation of analog signals, reducing noise and improving signal fidelity in the final output.
image_name:x_lp(n)
description:The graph labeled "x_lp(n)" in the provided diagram illustrates a discrete-time signal and its frequency spectrum as part of an oversampling A/D converter process.

Type of Graph and Function:
The graph consists of a time-domain waveform on the left and its corresponding frequency spectrum on the right. The time-domain graph shows the sampled signal, while the frequency-domain graph represents its spectral components.

Axes Labels and Units:
- **Time-Domain (Left):**
- Horizontal Axis: Labeled as "n," representing discrete time indices.
- Vertical Axis: Represents amplitude, with no specific units provided.
- **Frequency-Domain (Right):**
- Horizontal Axis: Labeled with angular frequency "ω," ranging from 0 to 2π.
- Vertical Axis: Represents amplitude or magnitude of frequency components, with no specific units provided.

Overall Behavior and Trends:
- **Time-Domain:**
- The signal "x_lp(n)" appears as a discrete approximation of a continuous waveform, resembling a sinusoidal shape. The signal is sampled at regular intervals, indicated by vertical lines.
- The waveform shows periodic behavior, suggesting it is a low-pass filtered version of a previous signal.

- **Frequency-Domain:**
- The spectrum "X_lp(ω)" shows distinct peaks at specific frequency intervals, indicating the presence of dominant frequency components.
- The spectrum is centered around the origin, with significant components at multiples of the sampling frequency.

Key Features and Technical Details:
- **Time-Domain:**
- The signal is a low-pass filtered version, meaning high-frequency components have been attenuated.
- The sampling points are evenly spaced, suggesting uniform sampling.

- **Frequency-Domain:**
- The spectral peaks suggest that the signal contains harmonics or multiple frequency components, likely due to the oversampling process.
- The peaks are symmetric around the origin, typical for real-valued signals.

Annotations and Specific Data Points:
- The time-domain graph is annotated with discrete time indices (1, 2, 3, ...), showing the progression of the sampled signal.
- The frequency-domain graph shows peaks at specific intervals, but no numerical values are provided for these frequencies.

Overall, the graph "x_lp(n)" illustrates a discrete-time, low-pass filtered signal and its frequency spectrum, highlighting the effects of oversampling and filtering in the A/D conversion process.
image_name:x_s(n)
description:The diagram represents various stages in an oversampling A/D converter, illustrating both time-domain and frequency-domain representations of signals at different stages of the conversion process.

Time-Domain Graphs:
1. **$x_c(t)$:**
- **Type:** Analog signal.
- **Description:** A continuous sinusoidal waveform representing the original analog input signal.
- **Axis:** Time (t) on the horizontal axis, amplitude on the vertical axis.

2. **$x_{sh}(t)$:**
- **Type:** Sample-and-Hold signal.
- **Description:** A stepped waveform resulting from the sample-and-hold process, where the continuous signal is sampled at discrete intervals and held constant between samples.
- **Axis:** Time (t) on the horizontal axis, amplitude on the vertical axis.

3. **$x_{dsm}(n)$:**
- **Type:** Delta-Sigma Modulated signal.
- **Description:** A high-frequency digital signal with values alternating between +1 and -1, representing the quantized output of the delta-sigma modulator.
- **Axis:** Sample number (n) on the horizontal axis, quantized levels on the vertical axis.

4. **$x_{lp}(n)$:**
- **Type:** Low-Pass filtered signal.
- **Description:** A smoother waveform representing the low-pass filtered version of the delta-sigma modulated signal.
- **Axis:** Sample number (n) on the horizontal axis, amplitude on the vertical axis.

5. **$x_s(n)$:**
- **Type:** Downsampled signal.
- **Description:** A lower frequency waveform representing the final downsampled digital signal, which has been decimated from the low-pass filtered signal.
- **Axis:** Sample number (n) on the horizontal axis, amplitude on the vertical axis.

Frequency-Domain Graphs:
1. **$X_c(f)$:**
- **Description:** Frequency spectrum of the original analog signal, showing a peak at the fundamental frequency $f_0$.
- **Axis:** Frequency (f) on the horizontal axis, amplitude on the vertical axis.

2. **$X_{sh}(f)$:**
- **Description:** Frequency spectrum of the sample-and-hold signal, showing the original peak at $f_0$ and additional spectral images around the sampling frequency $f_s$.
- **Axis:** Frequency (f) on the horizontal axis, amplitude on the vertical axis.

3. **$X_{dsm}(\omega)$:**
- **Description:** Frequency spectrum of the delta-sigma modulated signal, showing a wide frequency spread due to noise shaping.
- **Axis:** Angular frequency ($\omega$) on the horizontal axis, amplitude on the vertical axis.

4. **$X_{lp}(\omega)$:**
- **Description:** Frequency spectrum of the low-pass filtered signal, showing reduced high-frequency components.
- **Axis:** Angular frequency ($\omega$) on the horizontal axis, amplitude on the vertical axis.

5. **$X_s(\omega)$:**
- **Description:** Frequency spectrum of the downsampled signal, showing multiple spectral images due to aliasing from the downsampling process.
- **Axis:** Angular frequency ($\omega$) on the horizontal axis, amplitude on the vertical axis.

Overall Behavior and Trends:
- The process begins with a continuous analog signal, which is sampled and held, then delta-sigma modulated to a high-frequency digital signal. This signal is then low-pass filtered to remove high-frequency noise, and finally downsampled to produce a digital signal suitable for further processing.
- In the frequency domain, the original signal's spectrum is progressively modified, with noise shaping in the delta-sigma modulator and filtering in the low-pass stage, culminating in a downsampled spectrum with potential aliasing artifacts.
image_name:X_c(f)
description:The graph titled \( X_c(f) \) is part of a series of diagrams illustrating the signals and spectra in an oversampling A/D converter. This specific graph is a frequency domain representation of a signal.

1. **Type of Graph and Function:**
- The graph is a frequency spectrum plot, showing the distribution of signal power across different frequencies.

2. **Axes Labels and Units:**
- The horizontal axis represents frequency \( f \) in hertz (Hz).
- The vertical axis represents the amplitude or power of the signal, although specific units are not labeled.
- The frequency axis includes markers at \( f_0 \) and \( f_s \), indicating the fundamental frequency and sampling frequency, respectively.

3. **Overall Behavior and Trends:**
- The graph shows a series of spectral lines, indicating discrete frequency components of the signal.
- The primary spectral component is centered at \( f_0 \), suggesting this is the main frequency of interest.
- There are additional components at multiples of the sampling frequency \( f_s \), which are typical in oversampled signals due to aliasing effects.

4. **Key Features and Technical Details:**
- The spectrum has a triangular shape centered at \( f_0 \), which may represent the bandwidth of the signal or a filter response.
- Sidebands or additional peaks are visible around \( f_s \), indicating the presence of harmonics or aliasing components.

5. **Annotations and Specific Data Points:**
- The graph includes markers at \( f_0 \) and \( f_s \), which are critical for understanding the signal's behavior in the frequency domain.
- No specific numerical values are provided for the amplitude, but the symmetry and distribution of the spectral lines are key to understanding the signal's characteristics.

Overall, the graph \( X_c(f) \) illustrates the frequency components of an oversampled signal, highlighting the main frequency \( f_0 \) and the effects of sampling at \( f_s \). This insight is crucial for understanding the performance and design considerations in oversampling A/D converters.
image_name:X_sh(f)
description:The graph labeled "X_sh(f)" is part of a larger diagram illustrating the signals and spectra in an oversampling A/D converter system. It appears to be a frequency-domain representation of a signal after sample-and-hold processing, which is a critical step in the conversion process.

Type of Graph and Function:
- The graph is a frequency-domain plot, likely a spectrum, showing the distribution of signal energy across frequencies.

Axes Labels and Units:
- The horizontal axis represents frequency, labeled as 'f'.
- The vertical axis represents amplitude or magnitude of the signal.
- The frequencies are marked with key points like \( f_0 \) and \( f_s \), indicating fundamental and sampling frequencies.

Overall Behavior and Trends:
- The spectrum shows a distinct peak at the fundamental frequency \( f_0 \), which is typical for a periodic signal.
- There may be additional components or replicas at the sampling frequency \( f_s \) and its multiples, indicating the presence of aliasing or harmonics due to the sampling process.

Key Features and Technical Details:
- The peak at \( f_0 \) suggests the presence of the original signal's frequency component.
- Additional peaks at \( f_s \) and its harmonics are visible, illustrating the effects of sampling.
- The presence of these peaks highlights the importance of filtering to remove unwanted frequency components.

Annotations and Specific Data Points:
- The graph includes annotations for \( f_0 \) and \( f_s \), providing reference points for understanding the frequency content.
- These annotations help in identifying the key frequencies involved in the signal's spectrum post sample-and-hold operation.

The graph effectively demonstrates how the sample-and-hold operation affects the frequency content of the signal, emphasizing the need for subsequent filtering to achieve a clean digital representation.
image_name:X_dsm(ω)
description:The diagram presents a series of graphs representing signals and their spectra in an oversampling A/D converter process. These graphs illustrate the transformation of a continuous-time signal through various stages of sampling and modulation.

1. **Types of Graphs and Functions:**
- The left column displays time-domain waveforms, while the right column shows corresponding frequency-domain spectra.
- The graphs include sampled signals, quantized signals, and their frequency representations.

2. **Axes Labels and Units:**
- The time-domain graphs (left column) have the horizontal axis labeled as time (t or n), representing continuous or discrete time, respectively.
- The frequency-domain graphs (right column) have the horizontal axis labeled as frequency (f or ω), indicating the frequency components of the signals.
- Vertical axes represent amplitude for both time and frequency domains.

3. **Overall Behavior and Trends:**
- **Time-Domain:**
- The first graph shows a continuous-time signal $x_c(t)$, a sinusoidal waveform.
- The second graph $x_{sh}(t)$ depicts a sample-and-hold version of the signal, with a step-like appearance.
- The third graph $x_{dsm}(n)$ represents a delta-sigma modulated signal with discrete amplitude levels of ±1.
- The fourth graph $x_{lp}(n)$ shows a low-pass filtered version, smoothing the signal.
- The fifth graph $x_s(n)$ represents the final downsampled signal.
- **Frequency-Domain:**
- The spectra show the frequency components with peaks at specific frequencies.
- $X_c(f)$ and $X_{sh}(f)$ have peaks centered around $f_0$.
- $X_{dsm}(ω)$ shows a broader spectrum due to noise shaping.
- $X_{lp}(ω)$ and $X_s(ω)$ illustrate the effects of filtering and downsampling.

4. **Key Features and Technical Details:**
- The delta-sigma modulated signal $x_{dsm}(n)$ shows quantized levels, indicating noise shaping.
- The frequency spectrum $X_{dsm}(ω)$ highlights the presence of noise shaping, with energy spread over a wider frequency range.
- Low-pass filtering is evident in $X_{lp}(ω)$, where high-frequency components are attenuated.
- The final downsampled signal $x_s(n)$ and its spectrum $X_s(ω)$ demonstrate reduced bandwidth and resolution.

5. **Annotations and Specific Data Points:**
- Specific frequencies such as $f_0$, $f_s$, and $2πf_0/f_s$ are marked, indicating key points in the frequency domain.
- The spectra show mirrored components due to the sampling process.
- The time-domain graphs are annotated with sample indices and amplitude levels, providing a clear view of the signal transformations.

This detailed analysis of the oversampling A/D converter process highlights the various stages and transformations of the signal, emphasizing the role of delta-sigma modulation and filtering in achieving high-resolution digital representation.
image_name:X_lp(ω)
description:The graph labeled "X_lp(ω)" is a frequency-domain plot, likely representing the spectrum of a low-pass filtered signal in an oversampling A/D converter system.

1. **Type of Graph and Function:**
- This is a frequency-domain graph, possibly a magnitude spectrum plot. It shows the frequency response of a low-pass filtered signal.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as frequency (ω), which is typically in radians per second. The scale is linear, extending from 0 to 2π.
- The vertical axis represents amplitude or magnitude, though specific units are not provided.

3. **Overall Behavior and Trends:**
- The graph shows a series of peaks at discrete frequency intervals, indicating the presence of harmonics or specific frequency components.
- The primary peak is centered around the origin, suggesting a low-pass characteristic where lower frequencies are emphasized.
- Additional peaks are symmetrically located around multiples of 2π, indicating periodicity in the frequency domain.

4. **Key Features and Technical Details:**
- The primary peak at the origin (0 frequency) suggests the retention of low-frequency components, typical of a low-pass filter.
- The presence of additional peaks at 2π intervals suggests that higher frequency components are present but likely attenuated compared to the central peak.
- This pattern is typical in oversampling systems where noise shaping might push quantization noise to higher frequencies.

5. **Annotations and Specific Data Points:**
- The graph does not include specific numerical annotations or data points, but the periodic peaks at multiples of 2π are noteworthy.
- The central peak is the most significant, indicating the dominance of low-frequency content in the filtered signal.

This graph is part of a larger set depicting various stages of signal processing in an oversampling A/D converter, illustrating how signals are transformed in both time and frequency domains.
image_name:X_s(ω)
description:The graph titled "X_s(ω)" is a frequency domain representation of a signal in an oversampling analog-to-digital (A/D) converter process. The graph is part of a series of plots illustrating different stages of signal processing, specifically focusing on the frequency spectrum of the downsampled signal.

1. **Type of Graph and Function:**
- The graph is a frequency spectrum plot, showing how the signal's energy is distributed across different frequencies.

2. **Axes Labels and Units:**
- The x-axis is labeled as "ω" (omega), representing angular frequency.
- The y-axis does not have a specific label but typically represents amplitude or magnitude in such plots.
- The x-axis has markers at intervals of π, indicating significant points in the frequency domain.

3. **Overall Behavior and Trends:**
- The graph shows a series of spikes at regular intervals (π, 2π, 4π, etc.), indicating harmonics or spectral components at these frequencies.
- The regular spacing suggests a periodic signal in the frequency domain, typical for sampled signals.

4. **Key Features and Technical Details:**
- The spikes at π, 2π, 4π, and so on, imply that the signal has significant components at these frequencies.
- The pattern suggests a comb-like structure, which is often seen in downsampled signals due to aliasing effects.
- This frequency representation helps in understanding how the signal behaves after being processed by the oversampling A/D converter.

5. **Annotations and Specific Data Points:**
- The graph does not have specific numerical annotations, but the regular pattern and spacing provide insight into the frequency content of the signal.
- The presence of these spikes at regular intervals is crucial for analyzing the effects of oversampling and downsampling in the A/D conversion process.

Fig. 18.15 Signals and spectra in an oversampling A/D converter.
produce the downsampled signal $\mathrm{x}_{\mathrm{s}}(\mathrm{n})$, as discussed in Section 18.4. The final signal, $\mathrm{x}_{\mathrm{s}}(\mathrm{n})$, would typically have 16-bit resolution in digital audio applications.

Key Point: The linearity of oversampled A/D converters depends more strongly on the linearity of its internal $D / A$ converter than on its internal quantizer.

It is of interest to look at what element most strongly affects the linearity of this oversampling $\mathrm{A} / \mathrm{D}$ system. Returning to the $\Delta \Sigma$ modulator, note that an internal 1-bit D/A converter is used whose output signal is combined with the input signal such that, over the frequency band of interest, these two signals are nearly the same. As a result, the overall linearity of this $\Delta \Sigma$ modulator converter depends strongly on the linearity of its internal D/A converter. For example, with a nonlinear internal D/A converter and a slow linear ramp input signal, the low-frequency content of the D/A converter's output would essentially equal that ramp. However, the low-frequency content of the digital input to the D/A converter would be a nonlinear ramp to account for the D/A converter's nonlinearity. Since the remaining digital circuitry is linear, the overall linearity of this oversampling A/D converter is most strongly dependent on realizing a linear $\mathrm{D} / \mathrm{A}$ converter inside the $\Delta \Sigma$ modulator. In fact, nonlinearities in the internal A/D converter (if it was multi-bit) have only a small effect on the linearity of the overall converter, since the high gain in the feedback loop compensates for that nonlinearity.

### 18.3.2 System Architecture of Delta-Sigma D/A Converters

Most of the discussion so far has focused on $\Delta \Sigma \mathrm{A} / \mathrm{D}$ converters, but much of it also applies to $\Delta \Sigma \mathrm{D} / \mathrm{A}$ converters, with a few qualifications. A high-resolution oversampling D/A converter using a 1-bit converter can be realized as shown in the block diagram in Fig. 18.16. Some illustrative signals that might occur in this system are shown in Fig. 18.17. The digital input signal, $x_{s}(n)$, is a multi-bit signal and has an equivalent sample rate of $2 f_{0}$, where $f_{0}$ is slightly greater than the highest input signal frequency. For example, in a compact disc audio application, a 16-bit input signal is used with a frequency band of interest from 0 to 20 kHz while the sample rate, $2 \mathrm{f}_{0}$, is 44.1 kHz . Note, however, that $\mathrm{X}_{\mathrm{s}}(\mathrm{n})$ is actually just a series of numbers and thus its shown frequency spectrum has normalized the sample rate to $2 \pi$. Next, the input signal is upsampled to an equivalent higher sampling rate, $\mathrm{f}_{\mathrm{s}}$, resulting in the upsampled signal $x_{s 2}(n)$. In the example shown, the oversampling rate is only six (i.e., $f_{s}=6 \times 2 f_{0}$ ), while in typical audio applications, $f_{s}$ is often near a $5-\mathrm{MHz}$ rate (i.e., oversampling rate of 128). However, $x_{s 2}(n)$ has large images left in its signal so an interpolation filter is used to create the multi-bit digital signal, $\mathrm{x}_{\mathrm{lp}}(\mathrm{n})$, by digitally filtering out the images. This interpolation filter is effectively a digital brick-wall-type filter that passes 0 to $\left(2 \pi f_{0}\right) / f_{s}$ and rejects all other signals. The resulting signal, $\mathrm{x}_{1 \mathrm{p}}(\mathrm{n})$, is then applied to a fully digital $\Delta \Sigma$ modulator that produces a 1-bit output signal, $x_{d s m}(n)$, which has a large amount of shaped quantization noise. As discussed earlier, the main reason for going to a 1-bit digital signal is so that a 1-bit $\mathrm{D} / \mathrm{A}$ converter can now be used to create $\mathrm{x}_{\mathrm{da}}(\mathrm{t})$, which has excellent linearity properties but still a large amount of out-of-band quantization noise. Finally, the desired output signal, $\mathrm{x}_{\mathrm{c}}(\mathrm{t})$, can be obtained by using an analog filter to filter out this out-of-band quantization noise. The analog filter may be a combination of switched-capacitor and continuous-time filtering.

Some points to note here are that while oversampling allows the use of a 1-bit D/A converter, which can have excellent linearity, the use of oversampling also relaxes some of the analog-smoothing filter specifications. For example, if a 16 -bit converter was used at the Nyquist rate, $2 \mathrm{f}_{0}$, the analog-smoothing filter would have to remove the images in the signal instead of a precise digital interpolation filter removing these images. This specification can be very demanding, as in a digital-audio application, where a near $96-\mathrm{dB}$ attenuation is required at 24 kHz , while up to 20 kHz should pass with unity gain. With the use of an oversampling approach, the digital interpolation filter is faced with this strict specification rather than an analog smoothing filter. In fact, oversampling is often used in audio applications with multi-bit D/A converters just to reduce this analog-smoothing filter's complexity.

Another point to note is that the order of the analog lowpass filter should be at least one order higher than that of the $\Delta \Sigma$ modulator. The reason for this choice is that if the analog filter's order is equal to that of the modulator, the slope of the rising quantization noise will match the filter's falling attenuation, and thus the resulting quantization noise will be approximately a constant spectral density up to one-half the sampling rate (i.e., $f_{s} / 2$ ). By having a higher-order analog filter, the

Key Point: Oversampling D/A converters require a very linear but low-resolution internal D/A converter, and an analog smoothing filter whose order should be at least one greater than that of the noise shaping andmust have sufficient dynamicrange to accommodate both signal and large quantization noise power at its input.
image_name:Fig. 18.16 Block diagram of a 1-bit oversampling D/A converter
description:The block diagram of a 1-bit oversampling D/A converter consists of several key components that work together to convert a digital signal into an analog output. Here's a detailed description of the system:

1. **Main Components:**
- **OSR (Oversampling Ratio):** This block increases the sampling rate of the input digital signal \( x_s(n) \), which is initially at a rate of \( 2f_0 \). The oversampling ratio is defined as \( \frac{f_s}{2f_0} \), where \( f_s \) is the new sampling frequency.
- **Interpolation (Low-Pass) Filter:** This block smooths the oversampled signal \( x_{s2}(n) \) and prepares it for further processing by removing high-frequency components. The output is \( x_{lp}(n) \).
- **ΔΣ Modulator:** This digital block receives the filtered signal \( x_{lp}(n) \) and performs noise shaping, producing a 1-bit digital output \( x_{dsm}(n) \). This process helps in reducing quantization noise in the band of interest.
- **1-bit D/A Converter:** This component converts the 1-bit digital signal \( x_{dsm}(n) \) into an analog signal \( x_{da}(t) \).
- **Analog Low-Pass Filter:** The final block in the chain, it smooths the analog signal \( x_{da}(t) \), removing high-frequency quantization noise and outputting the final analog signal \( x_c(t) \).

2. **Flow of Information or Control:**
- The process begins with the digital input signal \( x_s(n) \), which is oversampled by the OSR block to increase its sampling frequency to \( f_s \).
- The oversampled signal \( x_{s2}(n) \) is then passed through the interpolation filter to remove unwanted high-frequency components, resulting in \( x_{lp}(n) \).
- The ΔΣ modulator takes \( x_{lp}(n) \) and applies noise shaping, producing a high-frequency 1-bit signal \( x_{dsm}(n) \).
- The 1-bit D/A converter transforms this digital signal into an analog signal \( x_{da}(t) \).
- Finally, the analog low-pass filter smooths \( x_{da}(t) \), resulting in the continuous analog output \( x_c(t) \).

3. **Labels, Annotations, and Key Indicators:**
- The diagram labels the signals at each stage: \( x_s(n), x_{s2}(n), x_{lp}(n), x_{dsm}(n), x_{da}(t), x_c(t) \).
- The oversampling ratio (OSR) is clearly defined as \( \frac{f_s}{2f_0} \).
- Blocks are marked to indicate whether they handle digital or analog signals.

4. **Overall System Function:**
- The primary function of this system is to convert a digital signal into an analog signal using oversampling and noise shaping techniques. By oversampling and applying a ΔΣ modulator, the system reduces quantization noise in the desired frequency band. The 1-bit D/A conversion followed by analog filtering ensures a smooth and accurate analog output signal suitable for various applications in audio and communication systems.

Fig. 18.16 Block diagram of a 1-bit oversampling D/A converter.
image_name:Fig. 18.16
description:The block diagram in Fig. 18.16 represents a 1-bit oversampling Digital-to-Analog (D/A) converter system. The primary function of this system is to convert a digital signal into an analog signal using oversampling and noise shaping techniques. Here's a detailed description of the diagram:

Main Components:
1. **Input Digital Signal (x_s(n))**: The process begins with a digital input signal, represented as a sequence of discrete samples.
2. **Oversampling Process (x_s2(n))**: The input digital signal is oversampled, which involves increasing the sampling rate to spread quantization noise over a wider frequency band. This is shown as the transition from x_s(n) to x_s2(n).
3. **Low-pass Filter (x_lp(n))**: After oversampling, the signal passes through a low-pass filter. This filter is crucial for removing high-frequency components introduced by oversampling, resulting in a smoother signal x_lp(n).
4. **ΔΣ Modulator (x_dsm(n))**: The filtered signal is then processed by a Delta-Sigma (ΔΣ) modulator, which shapes the quantization noise to push it out of the frequency band of interest. This is depicted as x_dsm(n).
5. **1-bit D/A Converter (x_da(t))**: The modulated signal is converted from digital to analog form using a 1-bit D/A converter, producing x_da(t).
6. **Analog Filter**: Finally, the analog signal passes through an analog filter, which strongly attenuates high-frequency noise and ensures that the output signal is smooth and suitable for practical applications.

Flow of Information or Control:
- The flow begins with the digital input signal x_s(n) and progresses through the oversampling process to x_s2(n).
- The oversampled signal is filtered to become x_lp(n), which is then modulated by the ΔΣ modulator to produce x_dsm(n).
- The 1-bit D/A conversion transforms x_dsm(n) into an analog signal x_da(t).
- The final output is achieved after the analog filtering, resulting in x_c(t), which is a smooth analog signal.

Labels, Annotations, and Key Indicators:
- The diagram includes frequency domain representations for each stage, showing how the spectral density of the signals changes through the process.
- Annotations like (1), (2), and (3) indicate the sequential steps of the conversion process.
- Frequency labels such as f_0 and f_s are used to denote the baseband frequency and the sampling frequency, respectively.

Overall System Function:
The system's primary function is to convert a digital signal into a high-quality analog signal by employing oversampling and noise shaping techniques. The arrangement of the blocks ensures that quantization noise is minimized in the desired frequency band, and the final analog output is smooth and accurate, making it suitable for audio and communication applications.
image_name:Fig. 18.17
description:The diagram labeled as "Fig. 18.17" presents a series of plots illustrating signals and their spectra in an oversampling D/A converter system. The graph is split into two columns, with the left column depicting time-domain signals and the right column showing their corresponding frequency spectra.

1. **Time-Domain Signals (Left Column):**
- **Top Plot:** The signal \( x_s(n) \) is shown as a discrete-time signal with samples at specific intervals, marked by vertical lines. The dotted line suggests a continuous waveform that the samples follow. The signal is sampled at a rate that exceeds the Nyquist rate to allow oversampling.
- **Second Plot:** \( x_{lp}(n) \) represents a low-pass filtered version of the original sampled signal \( x_s(n) \). The discrete samples are more densely packed, indicating a smoother transition between them.
- **Third Plot:** \( x_{dsm}(n) \) shows a delta-sigma modulated signal, characterized by high-frequency switching between discrete levels. This modulation is used to shape the noise and push it out of the band of interest.
- **Fourth Plot:** \( x_{da}(t) \) is the analog signal after D/A conversion, with a continuous waveform that closely resembles the original signal shape.
- **Bottom Plot:** \( x_c(t) \) is the final continuous-time output signal, which is smooth and free from the high-frequency components seen in \( x_{dsm}(n) \).

2. **Frequency Spectra (Right Column):**
- **Top Plot:** \( X_s(\omega) \) displays the spectrum of the sampled signal \( x_s(n) \), showing repeated spectral replicas due to sampling, spaced at intervals of \( 2\pi \).
- **Second Plot:** \( X_{s2}(\omega) \) represents the spectrum of the oversampled signal, with spectral replicas spaced more closely, indicating a higher sampling rate.
- **Third Plot:** \( X_{lp}(\omega) \) shows the spectrum after low-pass filtering, with only the fundamental frequency component remaining and higher frequencies attenuated.
- **Fourth Plot:** \( X_{dsm}(\omega) \) illustrates the spectrum of the delta-sigma modulated signal, with a broad noise shaping curve that pushes quantization noise to higher frequencies.
- **Fifth Plot:** \( X_{da}(f) \) is the spectrum of the D/A converted signal, showing a strong peak at the desired frequency \( f_0 \) and reduced noise at higher frequencies.
- **Bottom Plot:** \( X_c(f) \) displays the final frequency spectrum, with a clear peak at \( f_0 \) and minimal high-frequency content, indicating effective filtering.

**Overall Behavior and Trends:**
- The time-domain plots transition from discrete, high-frequency components to smooth, continuous signals as the system processes the signal through various stages.
- The frequency spectra demonstrate the reduction of high-frequency noise and the preservation of the desired frequency components through oversampling and filtering techniques.

**Key Features and Technical Details:**
- The oversampling process increases the sampling rate, allowing for more effective noise shaping.
- Delta-sigma modulation is used to push quantization noise out of the band of interest.
- The final analog filter ensures the removal of high-frequency noise, resulting in a clean output signal at \( f_0 \).

Fig. 18.17 Signals and spectra in an oversampling D/A converter.
spectral density of the output signal's quantization noise will have a bandwidth similar to the analog filter's bandwidth, which is around $f_{0}$.

Finally, note that the analog filter must be able to strongly attenuate high-frequency noise, as much of the quantization noise is centered around $f_{s} / 2$, and this analog filter should be linear so it does not modulate the noise back to the frequency band of interest. In many applications, the realization of these filters, especially if they are integrated, is nontrivial.

## 18.4 DIGITAL DECIMATION FILTERS

There are many techniques for realizing digital decimation filters in oversampling $\mathrm{A} / \mathrm{D}$ converters. In this section, we discuss two popular approaches - multi-stage and single-stage.

### 18.4.1 Multi-Stage

One method for realizing decimation filters is to use a multi-stage approach, as shown in Fig. 18.18. Here, the first-stage FIR filter, $\mathrm{T}_{\text {sinc }}(\mathrm{z})$, removes much of the quantization noise such that its output can be downsampled to four times the Nyquist rate (i.e., $8 \mathrm{f}_{0}$ ). This lower-rate output is applied to the second-stage filter, which may be either an IIR filter, as shown in Fig. 18.18(a), or a cascade of FIR filters, as shown in Fig. 18.18(b).

The sinc ${ }^{L+1}$ FIR filter is a cascade of $L+1$ averaging filters where the transfer function of a single averaging filter, $T_{\text {avg }}(z)$, is given by

$$
\begin{equation*}
T_{\mathrm{avg}}(z)=\frac{Y(z)}{U(z)}=\frac{1}{M} \sum_{i=0}^{M-1} z^{-i} \tag{18.35}
\end{equation*}
$$

and $M$ is the integer ratio of $f_{s}$ to $8 f_{0}$ (i.e., $8 f_{0}=f_{s} / M$ ). Note that the impulse response of this filter is finite, implying it is an FIR-type filter. In addition, all of its impulse response coefficients are symmetric (in fact, they are all equal), and thus it is also a linear-phase filter. ${ }^{6}$ Finally, note that the $1 / \mathrm{M}$ multiplication term is easily realized by changing the location of the fractional bits when M is chosen to be a power of two.

As an illustration of a series of averaging filters reducing quantization noise, consider an average-of-four filter (i.e., $M=4$ ) operating on the output of the 1-bit signal in Example 18.4. Since the output 1-bit sequence is $\{1,1,-1,1,1,-1,1,1,-1, \ldots\}$, the first averaged output, $\mathrm{x}_{\mathrm{lp} 1}(\mathrm{n})$, would be given by

$$
\mathrm{x}_{\mathrm{lp} \mathrm{l}}(\mathrm{n})=\{0.5,0.5,0.0,0.5,0.5,0.0, \ldots\}
$$

To obtain more attenuation of the quantization noise, the signal $\mathrm{x}_{\mathrm{pl} 1}(\mathrm{n})$ can also be applied to a running-average-of-four filter, giving $\mathrm{x}_{\mathrm{lp} 2}(\mathrm{n})$ as

$$
x_{\mathrm{lp} 2}(n)=\{0.375,0.375,0.25,0.375,0.375,0.25, \ldots\}
$$

image_name:(a)
description:The system block diagram labeled "(a)" consists of a multi-stage decimation filter system with the following components:

1. **Lth-order ΔΣ Modulator:**
- This block is the initial stage of the system, labeled as an Lth-order Delta-Sigma (ΔΣ) modulator. It processes the input signal at a sampling rate of \( f_s \). The ΔΣ modulator is typically used to shape quantization noise and improve signal resolution.

2. **sinc\(^{L+1}\) FIR Filter:**
- The output from the ΔΣ modulator is fed into a Finite Impulse Response (FIR) filter characterized by a sinc\(^{L+1}\) response. This block is denoted as \( T_{\text{sinc}}(z) \). The FIR filter performs decimation, reducing the data rate from \( f_s \) to \( 8f_0 \). The sinc filter is used to suppress out-of-band noise and improve the signal-to-noise ratio.

3. **IIR Filter:**
- The output of the sinc FIR filter is then passed to an Infinite Impulse Response (IIR) filter, marked as \( T_{\text{IIR}}(z) \). This stage further processes the signal, reducing the rate from \( 8f_0 \) to \( 2f_0 \). IIR filters are used for their efficient implementation and ability to achieve sharper cutoffs compared to FIR filters.

**Flow of Information:**
- The signal flow is unidirectional, beginning at the ΔΣ modulator, moving through the sinc FIR filter, and finally through the IIR filter. Each stage reduces the data rate and refines the signal by attenuating noise and unwanted frequency components.

**Overall System Function:**
- The primary function of this system is to perform multi-stage decimation on a high-rate digital signal. Starting with noise shaping in the ΔΣ modulator, the system progressively reduces the data rate while filtering out noise and preserving the desired signal characteristics. This arrangement is particularly useful in digital signal processing applications where high-resolution and low-noise signals are required.

(a)
image_name:(b)
description:The system block diagram labeled "(b)" illustrates a multi-stage decimation process used to reduce the data rate of a high-rate digital signal while preserving its essential characteristics. The diagram consists of the following main components:

1. **Lth-order ΔΣ Modulator:**
- This block is the starting point of the system, where a high-rate digital signal is input. The modulator shapes the noise in the signal, preparing it for subsequent decimation and filtering stages.
- The input signal rate is denoted as \( f_s \).

2. **Sinc\(^{L+1}\) FIR Filter \( T_{sinc}(z) \):**
- Following the ΔΣ modulator, the signal passes through a Sinc\(^{L+1}\) finite impulse response (FIR) filter. This filter is responsible for initial decimation and anti-aliasing, reducing the signal rate to \( 8f_0 \).

3. **Halfband FIR Filters \( H_1(z) \) and \( H_2(z) \):**
- These two filters further decimate the signal. \( H_1(z) \) reduces the rate to \( 4f_0 \), and \( H_2(z) \) brings it down to \( 2f_0 \). Each halfband filter is designed to allow a portion of the frequency spectrum to pass while attenuating others, providing effective decimation with minimal distortion.

4. **Sinc Compensation FIR Filter \( H_3(z) \):**
- The final stage involves a sinc compensation FIR filter. This filter compensates for any distortion introduced by the initial sinc filtering, ensuring that the desired signal characteristics are preserved at the final output rate of \( 2f_0 \).

5. **Flow of Information:**
- The signal flows sequentially from the ΔΣ modulator through each filtering stage. The progression of the data rate from \( f_s \) to \( 2f_0 \) is clearly marked above each block, indicating the decimation process.

6. **Overall System Function:**
- The primary function of this system is to perform efficient multi-stage decimation on a digital signal. It starts with noise shaping in the ΔΣ modulator and progressively reduces the data rate through a series of FIR filters. The system is designed to minimize noise and distortion, making it suitable for high-resolution digital signal processing applications.

(b)

Fig. 18.18 Multi-stage decimation filters: (a) sinc followed by an IIR filter; (b) sinc followed by halfband filters.
6. A linear-phase filter results in all frequency components being delayed by the same amount and is therefore desirable in applications where phase distortion is unwanted (such as hi-fi audio).
and repeating this process to get $x_{1 p 3}(n)$ would give

$$
x_{1 \mathrm{p} 3}(\mathrm{n})=\{0.344,0.344,0.313,0.344,0.344,0.313, \ldots\}
$$

Note the convergence of these sequences to a series of all samples equalling $1 / 3$ as expected.
To show that the frequency response of an averaging filter, $\mathrm{T}_{\text {avg }}(z)$, has a sinc-type behavior, it is useful to rewrite (18.35) as

$$
\begin{equation*}
M Y(z)=\left(\sum_{i=0}^{M-1} z^{-i}\right) U(z)=\left(1+z^{-1}+z^{-2}+\cdots+z^{-(M-1)}\right) U(z) \tag{18.36}
\end{equation*}
$$

which can also be rewritten as

$$
\begin{align*}
M Y(z) & =\left(z^{-1}+z^{-2}+\cdots+z^{-M}\right) U(z)+\left(1-z^{-M}\right) U(z)  \tag{18.37}\\
& =M z^{-1} Y(z)+\left(1-z^{-M}\right) U(z)
\end{align*}
$$

Finally, we group together $Y(z)$ terms and find the transfer function of this averaging filter can also be written in the recursive form as

$$
\begin{equation*}
\mathrm{T}_{\mathrm{avg}}(\mathrm{z})=\frac{\mathrm{Y}(\mathrm{z})}{\mathrm{U}(\mathrm{z})}=\frac{1}{\mathrm{M}}\left(\frac{1-\mathrm{z}^{-\mathrm{M}}}{1-\mathrm{z}^{-1}}\right) \tag{18.38}
\end{equation*}
$$

The frequency response for this filter is found by substituting $z=e^{j \omega}$, which results in

$$
\begin{equation*}
\mathrm{T}_{\mathrm{avg}}\left(\mathrm{e}^{\mathrm{j} \omega}\right)=\frac{\operatorname{sinc}\left(\frac{\omega \mathrm{M}}{2}\right)}{\operatorname{sinc}\left(\frac{\omega}{2}\right)} \tag{18.39}
\end{equation*}
$$

where $\operatorname{sinc}(\mathrm{x}) \equiv \sin (\mathrm{x}) / \mathrm{x}$.
A cascade of $L+1$ averaging filters has the response $T_{\text {sinc }}(z)$ given by

$$
\begin{equation*}
\mathrm{T}_{\text {sinc }}(\mathrm{z})=\frac{1}{\mathrm{M}^{\mathrm{L}+1}}\left(\frac{1-\mathrm{z}^{-\mathrm{M}}}{1-\mathrm{Z}^{-1}}\right)^{\mathrm{L}+1} \tag{18.40}
\end{equation*}
$$

The reason for choosing to use $L+1$ of these averaging filters in cascade is similar to the argument that the order of the analog low-pass filter in an oversampling $\mathrm{D} / \mathrm{A}$ converter should be higher than the order of the $\Delta \Sigma$ modulator. Specifically, the slope of the attenuation for this low-pass filter should be greater than the rising quantization noise, so that the resulting noise falls off at a relatively low frequency. Otherwise, the noise would be integrated over a very large bandwidth, usually causing excessive total noise.

An efficient way to realize this cascade-of-averaging filters is to write (18.40) as

$$
\begin{equation*}
\mathrm{T}_{\text {sinc }}(\mathrm{z})=\left(\frac{1}{1-\mathrm{z}^{-1}}\right)^{\mathrm{L}+1}\left(1-\mathrm{z}^{\mathrm{M}}\right)^{\mathrm{L}+1} \frac{1}{\mathrm{M}^{\mathrm{L}+1}} \tag{18.41}
\end{equation*}
$$

and thus realize it as shown in Fig. 18.19 [Candy, 1992]. A point to note here is that at first glance it appears as though this circuit will not operate properly due to a dc input causing saturation of the discrete-time integrators.
image_name:(a)
description:The system block diagram labeled "(a)" illustrates the realization of the transfer function \(\mathrm{T}_{\text{sinc}}(z)\) as a cascade of integrators and differentiators. This configuration is designed to perform filtering with downsampling occurring after all filtering operations.

1. **Main Components:**
- **Integrators:** The first section of the diagram consists of a series of integrators. Each integrator is represented by a feedback loop with a delay element \(z^{-1}\). The integrators accumulate the input signal over time.
- **Differentiators:** Following the integrators, there is a series of differentiators. Each differentiator is depicted with a delay element \(z^{-M}\), where \(M\) represents the downsampling factor. These blocks differentiate the accumulated signal from the integrators.
- **Summation Points:** Several summation points are present in the diagram, depicted as circles with a plus sign. These are used to combine input signals and feedback from the delay elements.

2. **Flow of Information or Control:**
- The input signal enters the system and passes through the first summation point before being fed into the integrators.
- Each integrator takes the current input and adds it to the delayed version of the previous input, effectively integrating the signal.
- After the integration stage, the signal flows into the differentiators, where each differentiator subtracts the delayed version of the signal (by \(M\) samples) from the current input.
- The final output is taken after the last differentiator, with downsampling by a factor of \(M\) occurring at the output stage.

3. **Labels, Annotations, and Key Indicators:**
- The diagram is labeled with "Integrators" and "Differentiators" to indicate the function of each section.
- The downsampling factor \(f_s/M\) is noted at the output, indicating that the output rate is reduced by this factor.

4. **Overall System Function:**
- The primary function of this system is to perform sinc filtering on the input signal with subsequent downsampling. The cascade of integrators smooths the input, while the differentiators restore the signal dynamics. The downsampling reduces the output data rate, suitable for applications requiring lower sample rates after filtering. This method ensures that the filtering is completed before any reduction in sample rate, preserving the integrity of the filtered signal.
image_name:(b)
description:The diagram labeled "(b)" illustrates a system for realizing the function \( \mathrm{T}_{\text{sinc}}(z) \) as a cascade of integrators and differentiators. This version is designed for efficiency by performing downsampling before the differentiators.

Main Components:
1. **Integrators:** The first section of the diagram consists of integrator blocks that include a summation point and a delay element \( z^{-1} \). These integrators operate at a high clock rate (\( f_s \)).
2. **Downsampling:** After the integrators, downsampling is performed by a factor of \( M \), reducing the sampling rate to \( f_s/M \).
3. **Differentiators:** Following the downsampling, the differentiator blocks also consist of a summation point and a delay element \( z^{-1} \). These operate at the reduced clock rate \( f_s/M \).

Flow of Information or Control:
- **Input Signal:** The input signal enters the system and passes through a series of integrators.
- **Integration Process:** Each integrator accumulates the input signal, with the delay elements providing feedback, effectively summing past inputs.
- **Downsampling:** The signal is then downsampled, which reduces the data rate before it is passed to the differentiators.
- **Differentiation Process:** The differentiators subtract the delayed version of the signal from the current input, effectively calculating differences between successive samples.
- **Output Signal:** The processed signal is then output from the system.

Labels, Annotations, and Key Indicators:
- The labels \( f_s \) and \( f_s/M \) indicate the clock rates at which different sections of the system operate.
- The use of arrows and summation points clearly define the flow of signals and the operations performed at each stage.

Overall System Function:
The primary function of this system is to efficiently compute the sinc function \( \mathrm{T}_{\text{sinc}}(z) \) by using a cascade of integrators and differentiators. By performing downsampling before the differentiators, the system reduces the computational load, making it more efficient while maintaining the desired signal processing characteristics. This setup is particularly effective in digital signal processing applications where efficient filtering and rate reduction are required.

Fig. 18.19 Realizing $\mathrm{T}_{\text {sinc }}(z)$ as a cascade of integrators and differentiators: (a) downsampling performed after all the filtering; (b) a more efficient method where downsampling is done before the differentiators.

Fortunately, such a result does not occur when 2's-complement arithmetic is used due to its wrap-around characteristic. Specifically, although the dc levels at the integrator outputs may be incorrect, the differentiators compare the present sample with that of M samples past while rejecting the dc component. Thus, as long as this difference is properly maintained (as it would be using 2 's-complement arithmetic) the correct calculation is performed.

Referring once again to Fig. 18.18, the purpose of the filters following the $\mathrm{T}_{\text {sinc }}(z)$ filter is twofold. One reason for their use is to remove any higher-frequency input signals (in effect, a sharp anti-aliasing filter) before the signal is downsampled to the final Nyquist rate (i.e., $2 \mathrm{f}_{0}$ ). In other words, while the $T_{\text {sinc }}(z)$ filter is good at filtering out the quantization noise, it is not sharp enough to act as a reasonable anti-aliasing filter for input signals slightly higher than $f_{0}$. A second reason is to compensate for the frequency drop in the passband caused by the $T_{\text {sinc }}(z)$ filter. This anti-aliasing and sinc-compensation filter might be realized using a single IIR filter, as shown in Fig. 18.18(a). Alternatively, a few halfband FIR filters might be used together with a separate sinc-compensation FIR filter, as shown in Fig. 18.18(b). A halfband FIR filter has a passband from 0 to $\pi / 2$, while its stopband is from $\pi / 2$ to $\pi$ with every second coefficient being zero [Vaidyanathan, 1993]. Thus, with a high enough filter order, its output can be downsampled by a factor of two. It has also been shown that in some applications, these halfband and sinc-compensation filters can be realized using no general multi-bit multipliers [Saramaki, 1990].

### 18.4.2 Single Stage

Another approach for realizing decimation filters is to use a relatively highorder FIR filter. For example, in [Dattorro, 1989], a 2048 tap FIR filter was used to decimate 1 -bit stereo outputs from two $\Delta \Sigma$ modulators, each having an oversampling ratio of 64 . While this FIR order seems high, note that no multi-bit multiplications are needed, since the input signal is simply 1-bit, so all multiplications are trivial. In addition, the output need only be calculated at the Nyquist rate (intermediate samples would be discarded anyway) such

Key Point: In single-stage decimation, one filter operates on alow-resolution noise-shaped signal providing the decimated output. Because of the high filter order, several time-interleaved filters may be used in parallel.
that 2048 additions are required during one clock cycle at the Nyquist rate. However, if only one accumulator is used to perform all 2048 additions, the clock rate of that accumulator would
be 2048 times the Nyquist rate. For example, if the Nyquist rate is 48 kHz , the single accumulator would have to be clocked at 98.3 MHz . To overcome this high clock rate, 32 separate FIR filters are realized (with shared coefficients) in a time-interleaved fashion, with each FIR having 2048 coefficients and each producing an output at a clock rate of 1.5 kHz . In this way, each of the 32 FIR filters uses a single accumulator operating at 3 MHz (i.e., 2048 times 1.5 kHz ). The coefficient ROM values were shared between the FIR filters (as well as in the two stereo channels), and the ROM size can also be halved if coefficients are duplicated, as in the case of linear-phase FIR filtering.

Finally, it is also possible to reduce the number of additions by grouping together input bits. For example, if four input bits are grouped together, then a 16 -word ROM lookup table can be used rather than using three additions. With such a grouping of input bits, each of the 32 FIR filters would require only 512 additions.

## 18.5 HIGHER-ORDER MODULATORS

Key Point: Noise shaping with order $L>2$ offers the potential for further improvements in SQNR of $6 L+3 \mathrm{~dB}$ /octave or $L+0.5$ bits/octave with respect to oversampling ratio.

In general, it can be shown that an Lth-order noise-shaping modulator improves the SQNR by $6 \mathrm{~L}+3 \mathrm{~dB} /$ octave, or equivalently, $L+0.5$ bits/octave. In this section, we look at two approaches for realizing higher-order modulators-interpolative and MASH. The first approach is typically a single high-order structure with feedback from the quantized signal. The second approach consists of a cascade of lowerorder modulators, where the latter modulators are used to cancel the noise errors introduced by the earlier modulators.

### 18.5.1 Interpolative Architecture

Key Point: Interpolative higherorder modulators permit the arbitrary placement of noise transfer function zeros, offering improved SQNR performance compared to the placement of all zeros at dc, especially for relatively low OSR. However, it is nontrivial to guarantee stability for such structures, and they are therefore often combined with multi-bit internal quantizers.

As discussed earlier, when compared to the error-feedback structure, the interpolative structure of Fig. 18.6(a) is much better suited to analog implementations of modulators due to its reduced sensitivity. One of the first approaches for realizing higher-order interpolative modulators was presented in [Chao, 1990]. It used a filtering structure very similar to a direct-form filter structure; however, a direct-form-type structure made it sensitive to component variations, which can cause the zeros of the noise transfer function to move off the unit circle. To improve component sensitivity, resonators can be used together with a modified interpolative structure, as shown in Fig. 18.20 [Ferguson, 1991]. Note here that a single 1-bit D/A signal is still used for feedback, and therefore its linearity will
u(n)
image_name:Fig. 18.20 A block diagram of a fifth-order modulator
description:The block diagram in Fig. 18.20 represents a fifth-order modulator, designed to improve component sensitivity and enhance dynamic range performance. Here’s a detailed breakdown of the system:

Main Components:
1. **Summing Nodes (+):** There are multiple summing nodes throughout the diagram, which combine input signals with feedback signals.
2. **Integrators (∫):** Five integrators are present, each represented by a triangle with an integral symbol, indicating that they perform integration of the input signals over time.
3. **Feedback Paths:** There are feedback loops associated with coefficients \( f_1 \) and \( f_2 \), which are crucial for placing zeros in the noise transfer function.
4. **Gain Coefficients (\( a_1, a_2, a_3, a_4, a_5 \)):** These are applied to the feedback and feedforward paths, controlling the influence of each path on the overall signal.
5. **Capacitors (\( c_1, c_2, c_3, c_4, c_5 \)):** These are used to store charge and influence the timing and frequency response of the integrators.
6. **Comparator:** The output of the final integrator is fed into a comparator, which likely converts the analog signal into a digital format for feedback.

Flow of Information or Control:
- **Input Signal Flow:** The input signal enters the system and is immediately combined with feedback signals at the first summing node.
- **Integration Sequence:** The combined signal is passed through a series of integrators, each further modifying the signal by integrating it over time.
- **Feedback Loops:** Feedback is taken from the output of certain integrators, weighted by coefficients \( f_1 \) and \( f_2 \), and fed back into earlier summing nodes. This feedback helps in shaping the noise transfer function.
- **Output and Feedback:** The final output is taken from the comparator, which also feeds back into the system, ensuring stability and linearity.

Labels, Annotations, and Key Indicators:
- **Gain Coefficients (\( a_1, a_2, a_3, a_4, a_5 \)):** These are crucial for tuning the system's response and are applied at various points in the signal path.
- **Feedback Coefficients (\( f_1, f_2 \)):** These are annotated along the feedback paths, indicating their role in zero placement in the noise transfer function.

Overall System Function:
The primary function of this fifth-order modulator is to modulate an input signal while minimizing noise and distortion through strategic placement of zeros in the noise transfer function. By employing resonators and a modified interpolative structure, this design achieves better dynamic range performance compared to traditional direct-form structures. The use of feedback loops and integrators ensures that the system maintains stability and high linearity, crucial for high-fidelity signal processing.

Fig. 18.20 A block diagram of a fifth-order modulator.
be excellent. The resonators in this structure are due to the feedback signals associated with $f_{1}$ and $f_{2}$, resulting in the placement of zeros in the noise transfer function spread over the frequency-of-interest band. Such an arrangement gives better dynamic range performance than placing all the zeros at dc as we have been assuming thus far.

Unfortunately, it is possible for modulators of order two or more to go unstable, especially when large input signals are present. When they go unstable, they may never return to stability even when the large input signals go away. Guaranteeing stability for an interpolative modulator is nontrivial and is discussed further in Section 18.7. In particular, the use of multi-bit internal quantizers improves stability and is therefore often used in combination with higher-order interpolative architectures.

### 18.5.2 Multi-Stage Noise Shaping (MASH) Architecture

Another approach for realizing modulators is to use a cascade-type structure where the overall higher-order modulator is constructed using lower-order ones. The advantage of this approach is that since the lower-order modulators are more stable, the overall system should remain stable. Such an arrangement has been called MASH (Multi-stAge noise SHaping) [Matsuya, 1987].

The arrangement for realizing a second-order modulator using two first-order modulators is shown in Fig. 18.21. The basic approach is to pass along the first section's quantization error, $\mathrm{e}_{1}(\mathrm{n})$, to another modulator and combine the outputs of both modulators in such a way that the first section's quantization noise is removed completely. The output is then left with only the second section's quantization noise, which has been filtered twice - once by the second modulator and once by the post digital circuitry. Assuming linear models for the quantizers, straightforward linear analysis for the first stage gives

$$
\begin{align*}
\mathrm{X}_{1}(\mathrm{z}) & =\mathrm{S}_{\mathrm{TF} 1}(\mathrm{z}) \mathrm{U}(\mathrm{z})+\mathrm{N}_{\mathrm{TF} 1}(\mathrm{z}) \mathrm{E}_{1}(\mathrm{z}) \\
& =\mathrm{z}^{-1} \mathrm{U}(\mathrm{z})+\left(1-\mathrm{z}^{-1}\right) \mathrm{E}_{1}(\mathrm{z}) \tag{18.42}
\end{align*}
$$

image_name:Fig. 18.21
description:The system block diagram in Fig. 18.21 illustrates a second-order MASH (Multi-stage Noise Shaping) modulator, which is composed of two first-order modulators. This system processes an input signal, \( u(n) \), and outputs a four-level digital signal, \( y(n) \).

Main Components:
1. **First-Order Modulator (Upper Section):**
- **Adder/Subtractor Blocks:** These are used to combine the input signal \( u(n) \) and feedback signals.
- **Delay Element (\( z^{-1} \)):** This block introduces a unit delay in the signal path.
- **Amplifier with Feedback:** The amplifier has a gain of +1 and generates the quantization error \( e_1 \).
- **1-bit D/A Converter:** Converts the digital output back to an analog signal for feedback.

2. **Second-Order Modulator (Lower Section):**
- **Adder/Subtractor Blocks:** These combine the error signal \( e_1(n) \) from the first modulator with feedback signals.
- **Delay Element (\( z^{-1} \)):** Another unit delay is introduced in this stage.
- **Amplifier with Feedback:** This amplifier has a gain of +2 and generates the quantization error \( e_2 \).
- **1-bit D/A Converter:** Similar to the first stage, it converts the digital output to an analog signal for feedback.

3. **Output Stage:**
- **Adder/Subtractor Blocks:** Combine the outputs from both modulators to produce the final output \( y(n) \).
- **Delay Elements and Transfer Functions:** These are used to shape the signal and noise transfer functions, \( S_{TF1}, N_{TF1}, S_{TF2}, N_{TF2} \), as annotated in the diagram.

Flow of Information or Control:
- The input signal \( u(n) \) is processed by the first modulator, where it is combined with feedback and delayed. The resulting signal \( X_1(z) \) is a function of the input and the first quantization error \( E_1(z) \).
- The error signal \( e_1(n) \) is then fed into the second modulator, which similarly processes it through addition, delay, and amplification to produce \( X_2(z) \), a function of \( E_1(z) \) and \( E_2(z) \).
- The outputs from both modulators are combined in the digital domain to produce the final output \( y(n) \).

Labels, Annotations, and Key Indicators:
- The diagram is annotated with transfer functions \( S_{TF1}, N_{TF1}, S_{TF2}, N_{TF2} \) which define the signal and noise transfer characteristics of the system.
- The gain values of the amplifiers and the presence of delay elements are clearly indicated.

Overall System Function:
The primary function of this MASH modulator is to convert an analog input signal into a digital output while shaping the noise in such a way that it minimizes the impact of quantization errors. By using a cascade of two first-order modulators, the system achieves higher order noise shaping, improving the signal-to-noise ratio in the desired frequency band.

Fig. 18.21 A second-order MASH modulator using two first-order modulators. Note that the output, $y(n)$, is a four-level signal.
and for the second stage

$$
\begin{align*}
\mathrm{X}_{2}(\mathrm{z}) & =\mathrm{S}_{\mathrm{TF} 2}(\mathrm{z}) \mathrm{E}_{1}(\mathrm{z})+\mathrm{N}_{\mathrm{TF} 2}(\mathrm{z}) \mathrm{E}_{2}(\mathrm{z}) \\
& =\mathrm{z}^{-1} \mathrm{E}_{1}(\mathrm{z})+\left(1-\mathrm{z}^{-1}\right) \mathrm{E}_{2}(\mathrm{z}) \tag{18.43}
\end{align*}
$$

The MASH output is then formed by passing the two digital outputs $x_{1}$ and $x_{2}$ through digital filters intended to match $S_{T F 2}$ and $N_{T F 1}$ respectively.

$$
\begin{align*}
\mathrm{Y}(\mathrm{Z})= & \hat{\mathrm{S}}_{\mathrm{TF} 2}(\mathrm{Z}) \mathrm{X}_{1}(\mathrm{z})+\hat{\mathrm{N}}_{\mathrm{TF} 1}(\mathrm{z}) \mathrm{X}_{2}(\mathrm{z}) \\
= & \hat{\mathrm{S}}_{\mathrm{TF} 2}(\mathrm{Z}) \mathrm{S}_{\mathrm{TF} 1}(\mathrm{z}) \mathrm{U}(\mathrm{z})+\left[\hat{\mathrm{S}}_{\mathrm{TF} 2}(\mathrm{z}) \mathrm{N}_{\mathrm{TF} 1}(\mathrm{z})+\hat{\mathrm{N}}_{\mathrm{TF} 1}(\mathrm{z}) \mathrm{S}_{\mathrm{TF} 2}(\mathrm{Z})\right] \mathrm{E}_{1}(\mathrm{z})  \tag{18.44}\\
& +\hat{\mathrm{N}}_{\mathrm{TF} 1}(\mathrm{z}) \mathrm{N}_{\mathrm{TF} 2}(\mathrm{z}) \mathrm{E}_{2}(\mathrm{z})
\end{align*}
$$

If $\hat{N}_{\mathrm{TF}_{1} 1}(\mathrm{Z})=\mathrm{N}_{\mathrm{TF}_{1}}(\mathrm{Z})$ and $\hat{\mathrm{S}}_{\mathrm{TF} 2}(\mathrm{Z})=\mathrm{S}_{\mathrm{TF}_{2}}(\mathrm{Z})$ then the entire second term disappears resulting in

$$
\begin{equation*}
\mathrm{Y}(\mathrm{z})=\hat{\mathrm{S}}_{\mathrm{TF} 2}(\mathrm{Z}) \mathrm{S}_{\mathrm{TF} 1}(\mathrm{z}) \mathrm{U}(\mathrm{z})+\hat{\mathrm{N}}_{\mathrm{TF} 1}(\mathrm{z}) \mathrm{N}_{\mathrm{TF} 2}(\mathrm{z}) \mathrm{E}_{2}(\mathrm{z}) \tag{18.45}
\end{equation*}
$$

so that the only quantization noise remaining is $\mathrm{E}_{2}$ shaped by both $\mathrm{N}_{T F_{1}}$ and $\mathrm{N}_{\mathrm{TF} 2}$. In the case of Fig. 18.21, this implies second-order noise shaping using two first-order modulators.

$$
\begin{equation*}
Y(z)=z^{-2} U(z)-\left(1-z^{-1}\right)^{2} E_{2}(z) \tag{18.46}
\end{equation*}
$$

Key Point: Multi-stage noise shaping (MASH) oversampling converters cascade lower order modulators to realize high-order noise shaping. Since the constituent stages are each first- or second-order, it is easy to ensure stability. However, MASH converters require digital filtering whose coefficients are matched to those of analog circuitry.

The approach can be generalized and extended to accommodate cascading more than two modulators. Thus, a MASH approach has the advantage that higher-order noise filtering can be achieved using lower-order modulators. The lower-order modulators are much less susceptible to instability as compared to an interpolator structure having a high order with a single feedback. Unfortunately, MASH or cascade approaches are sensitive to finite opamp gain, bandwidth and mismatches causing gain errors. Such errors cause the analog integrators to have finite gain and pole frequencies (see Section 18.7.5), making it difficult to ensure $N_{T F_{1}}(\mathrm{Z})=N_{T F_{1}}(\mathrm{z})$ and $\hat{S}_{T F_{2}}(\mathrm{Z})=\mathrm{S}_{\mathrm{TF} 2}(\mathrm{Z})$ precisely as required for cancellation of the quantization noise $\mathrm{E}_{1}(\mathrm{z})$ in (18.44). In the above example, this would cause firstorder noise to leak through from the first modulator and hence reduce dynamic range performance.

In order to mitigate the mismatch problem, the first stage may be chosen to be a higher-order modulator such that any leak-through of its noise has less effect than if this first modulator was first-order. For example, a third-order modulator would be realized using a second-order modulator for the first stage and a first-order modulator for the second stage.

Another approach to combat errors in MASH architectures is to cancel these errors digitally by appropriately modifying the digital filters $\hat{\mathrm{N}}_{\mathrm{TF} 1}$ and $\hat{\mathrm{S}}_{\mathrm{TF} 2}$ in Fig. 18.21. For example, test signals may be injected and later cancelled digitally while using them to precisely identify $\mathrm{N}_{\mathrm{TF} 1}$ and $\mathrm{S}_{\mathrm{TF} 2}$ and match them with $\hat{\mathrm{N}}_{\mathrm{TF} 1}$ and $\hat{S}_{\mathrm{TF} 2}$ [Kiss, 2000]. Also, it is very important to minimize errors due to input-offset voltages that might occur because of clock feedthrough or opamp input-offset voltages. Typically, in practical realizations additional circuit design techniques will be employed to minimize these effects.

Finally, note that the use of this MASH approach results in the digital output signal, $y(n)$, being a four-level signal (rather than two-level) due to the combination of the original two-level signals. Such a four-level signal would require a linear four-level D/A converter in a D/A application. For A/D applications, it makes the FIR decimation filter slightly more complex.

## 18.6 BANDPASS OVERSAMPLING CONVERTERS

As we have seen, oversampling converters have the advantage of high linearity through the use of 1-bit conversion and reduced anti-aliasing and smoothing-filter requirements. However, at first glance some signals do not appear to easily lend themselves to oversampling approaches such as modulated radio signals. Such signals have information in only a small amount of bandwidth, say 10 kHz , but have been modulated by some higher-frequency carrier signal, say 1 MHz . For such applications, one can make use of bandpass oversampling converters.

In low-pass oversampling converters, the transfer function $\mathrm{H}(\mathrm{z})$ in Fig. 18.6 is chosen such that it has a high gain near dc , and thus quantization noise is small around dc. In a similar way, bandpass oversampling converters are realized by choosing $\mathrm{H}(\mathrm{z})$ such that it has a high gain near some frequency value, $\mathrm{f}_{\mathrm{c}}$, [Schreier, 1989]. With such an approach, the quantization noise is small around $f_{c}$, and thus most of the quantization noise can be removed through the use of a narrow bandpass filter of total width $\mathrm{f}_{\Delta}$ following the modulator. Thus, in the case of a bandpass $A / D$ converter intended for digital radio, post narrowband digital filtering would remove quantization noise as well as adjacent radio channels. In addition, further digital circuitry would also perform the necessary demodulation of the signal.

An important point here is that the oversampling ratio for a bandpass converter is equal to the ratio of the sampling rate, $f_{s}$, to two times the width of the narrow-band filter, $2 f_{\Delta}$, and it does not depend on the value of $f_{c}$. For example, consider a bandpass oversampling converter with a sampling rate of $f_{s}=4 \mathrm{MHz}$, which is intended to convert a $10-\mathrm{kHz}$ signal bandwidth centered around 1 MHz ( or $\mathrm{f}_{\mathrm{c}}=\mathrm{f}_{\mathrm{s}} / 4$ ). In this case, $\mathrm{f}_{\Delta}=10 \mathrm{kHz}$, resulting in the oversampling ratio being equal to

$$
\begin{equation*}
\mathrm{OSR}=\frac{\mathrm{f}_{\mathrm{s}}}{2 \mathrm{f}_{\Delta}}=200 \tag{18.47}
\end{equation*}
$$

To obtain a high gain in $H(z)$ near $f_{c}$, a similar approach to the low-pass case is taken. In a first-order lowpass oversampling converter, $\mathrm{H}(\mathrm{z})$ is chosen such that it has a pole at dc (i.e., $\mathrm{z}=1$ ) and such that the noise transfer function, $N_{T F}(z)$, has a zero at dc. In a second-order bandpass oversampling converter with $f_{c}=f_{s} / 4, H(z)$ is chosen such that it has poles at $\mathrm{e}^{ \pm \mathrm{ji/2}}= \pm \mathrm{j}$. In other words, $\mathrm{H}(\mathrm{z})$ is a resonator that has an infinite gain at the frequency $f_{s} / 4$. The zeros of the noise transfer function for this type of second-order oversampling converter are shown in Fig. 18.22, together with a similar low-pass case.

A block diagram for the example bandpass modulator is shown in Fig. 18.23, where one can derive $H(z)$ to be given by

$$
\begin{equation*}
H(z)=\frac{z}{z^{2}+1} \tag{18.48}
\end{equation*}
$$

image_name:Fig. 18.22(a)
description:The graph depicted in Fig. 18.22 is a pole-zero plot on the z-plane, commonly used in digital signal processing to analyze the frequency response of a system.

Axes Labels and Units:
- **Axes**: The plot is represented in the complex z-plane, with the horizontal axis being the real part and the vertical axis being the imaginary part.
- **Units**: The units are dimensionless as it is a complex plane representation.

Overall Behavior and Trends:
- The plot features a unit circle which is a typical characteristic of z-plane diagrams, indicating the boundary of stability for discrete-time systems.
- The zeros are marked on the unit circle, which affect the frequency response of the system.

Key Features and Technical Details:
- **Zeros**: The plot shows zeros on the unit circle at specific frequency points, which are crucial for shaping the noise transfer function.
- **fs/4 = 1 MHz**: A zero is located on the unit circle at this frequency, indicating a point where the system has no gain.
- **fs/2**: Another zero is located here, representing the Nyquist frequency.
- **2f0**: This point is marked on the unit circle, suggesting another zero at twice the fundamental frequency.
- **Annotations**:
- **fs = 4 MHz**: The sampling frequency of the system is indicated.
- **f0 = 10 kHz**: The fundamental frequency of the system is noted.
- **dc**: Direct current (zero frequency) is marked, typically indicating the starting point of frequency analysis.

Annotations and Specific Data Points:
- The plot is annotated with arrows pointing towards the zeros, emphasizing their positions on the unit circle.
- The zeros are critical for determining the stopband of the noise transfer function, effectively shaping how noise is attenuated or amplified at specific frequencies.

This plot is essential for understanding the behavior of oversampling converters, particularly in how they manage noise across different frequency bands. The placement of zeros at these specific points helps in designing systems that have desired noise shaping characteristics, such as minimizing noise at certain critical frequencies like fs/4 and fs/2.

(a) $\mathrm{OSR}=\frac{\mathrm{f}_{\mathrm{s}}}{2 \mathrm{f}_{0}}=200$
image_name:Fig. 18.22(b) Noise-transfer-function zeros for oversampling converters
description:The graph in Fig. 18.22 is a z-plane plot, which is used to illustrate the placement of zeros in the noise-transfer function for oversampling converters. This type of graph is crucial for understanding how noise is shaped in digital signal processing, particularly in oversampling modulators.

**Axes Labels and Units:**
- The graph does not explicitly label axes with units, as it is a z-plane plot. However, it is understood that the plot represents complex frequency with real and imaginary components typically normalized to the unit circle.

**Overall Behavior and Trends:**
- The plot depicts a circular shape, representing the unit circle in the z-plane. This circle is fundamental in digital signal processing for analyzing system stability and frequency response.

**Key Features and Technical Details:**
- The zeros of the noise-transfer function are marked on the circle.
- Key frequency points are annotated:
- **fs/4 = 1 MHz:** This point is crucial for noise shaping, where noise is minimized.
- **fs/2:** Represents the Nyquist frequency, a critical threshold in digital sampling.
- **fs = 4 MHz:** The sampling frequency of the system.
- **fΔ = 10 kHz:** A specific frequency of interest for the system.
- The zeros are strategically placed on the circle to achieve desired noise shaping characteristics, minimizing noise at fs/4 and fs/2.

**Annotations and Specific Data Points:**
- The plot includes annotations indicating zero placements with circles labeled as 'zero.'
- Arrows indicate the direction of frequency increase and specific frequency points are labeled for clarity.

This z-plane plot is essential for designing oversampling converters with specific noise shaping characteristics, allowing engineers to minimize noise at critical frequencies and enhance system performance.

(b) $\operatorname{OSR}=\frac{\mathrm{f}_{\mathrm{s}}}{2 \mathrm{f}_{\Delta}}=200$

Fig. 18.22 Noise-transfer-function zeros for oversampling converters: (a) first-order low-pass; (b) second-order bandpass.
image_name:Fig. 18.23
description:The system block diagram labeled "Fig. 18.23" illustrates a second-order bandpass oversampling modulator designed to shape quantization noise away from the frequency \( f_s / 4 \). This modulator is part of a digital signal processing system used to enhance signal quality by minimizing noise at critical frequencies.

Main Components:
1. **Input \( u(n) \):** The system receives a discrete-time input signal \( u(n) \).
2. **Summing Junctions:** There are two summing junctions in the feedback loop. The first summing junction subtracts the feedback signal from the input \( u(n) \). The second summing junction is part of the internal feedback within the block \( H(z) \).
3. **Delay Elements \( z^{-1} \):** Two delay elements are used within the block \( H(z) \), providing a one-sample delay to the signals.
4. **Quantizer:** The quantizer block converts the continuous input signal into a discrete output signal \( y(n) \) by mapping the input to a finite set of levels.
5. **Feedback Loop:** The system includes a feedback loop that routes the output \( y(n) \) back to the input summing junction, effectively shaping the noise.

Flow of Information or Control:
- The input signal \( u(n) \) enters the system and is first processed by the initial summing junction, where the feedback signal is subtracted.
- The resulting signal is then passed through the block \( H(z) \), which contains two delay elements \( z^{-1} \). These elements introduce delays that are crucial for the noise shaping characteristics of the modulator.
- The processed signal from \( H(z) \) is then fed into the quantizer, which outputs the discrete signal \( y(n) \).
- The output \( y(n) \) is fed back into the system, closing the loop and influencing the input to the summing junction, thereby shaping the quantization noise.

Labels, Annotations, and Key Indicators:
- **\( H(z) \):** Represents the transfer function of the filter block, which is responsible for the bandpass characteristics and noise shaping.
- **\( z^{-1} \):** Indicates the delay elements within the filter block.
- **Quantizer:** Depicted with a staircase symbol, indicating the quantization process.

Overall System Function:
The primary function of this system is to perform oversampling and noise shaping to improve the dynamic range and signal quality of the input signal. By strategically placing zeros and poles, the modulator shapes the quantization noise to minimize its presence at critical frequencies, particularly moving it away from \( f_s / 4 \). This results in enhanced performance for applications requiring high precision and low noise levels.

Fig. 18.23 A second-order bandpass oversampling modulator that shapes the quantization noise away from $\mathrm{f}_{\mathrm{s}} / 4$.

Note that this second-order example has poles at $\pm \mathrm{j}$, and therefore the noise transfer function, $\mathrm{N}_{\mathrm{TF}}(\mathrm{z})$, has only one zero at $j$ and another zero at $-j$. For this reason, the dynamic range increase of a second-order bandpass converter equals that of a first-order low-pass converter that also has only one zero at dc. Specifically, the dynamic range increase of a second-order bandpass converter is 1.5 bits/octave or, equivalently, $9 \mathrm{~dB} /$ cctave. To obtain the equivalent dynamic range increase of a second-order low-pass converter (i.e., $15 \mathrm{~dB} /$ octave), a fourth-order bandpass converter would have to be used. The first design of an integrated bandpass oversampling A/D converter was presented in [Jantzi, 1993].

## 18.7 PRACTICAL CONSIDERATIONS

### 18.7.1 Stability

As with any feedback-type system, delta-sigma modulators have the potential to go unstable. A stable modulator is defined here as one in which the input (or inputs) to the quantizer (or quantizers) remains bounded such that the quantization does not become overloaded. An overloaded quantizer is one in which the input signal goes beyond the quantizer's normal range, resulting in the quantization error becoming greater than $\pm \Delta / 2$.

Unfortunately, the stability of higher-order 1-bit modulators is not well understood as they include a highly nonlinear element (a 1-bit quantizer), resulting in the system being stable for one input but unstable for another. As a general rule of thumb, keeping the peak frequency response gain of the noise-transfer function, $\mathrm{N}_{\mathrm{TF}}(\mathrm{z})$, less than 1.5 often results in a stable modulator [Chao, 1990]. ${ }^{7}$ In mathematical terms,

$$
\begin{equation*}
\left|\mathrm{N}_{\mathrm{TF}}\left(\mathrm{e}^{\mathrm{j} \omega}\right)\right| \leq 1.5 \quad \text { for } 0 \leq \omega \leq \pi \tag{18.49}
\end{equation*}
$$

Key Point: The stability of 1-bit modulators is not well understood, but as a rule of thumb keeping the peak magnitude response of the noise transfer function below 1.5 often results in a stable modulator.
should be satisfied for a 1-bit quantizer. It should be noted that this stability criterion has little rigorous justification and that there does not presently exist any necessary and sufficient stability criterion for $\Delta \Sigma$ modulators having arbitrary inputs. There is, however, a rigorous 1-norm stability test (which is sufficient but not necessary), but it is often too conservative, as it eliminates many "stable" modulators [Anastassiou, 1989]. Hence, extensive simulations are used to confirm the stability of integrated circuit modulators. For a summary of stability tests for $\Delta \Sigma$ modulators, the reader is referred to [Schreier, 1993].

It should be mentioned here that the stability of a modulator is also related to the maximum input signal level with respect to the 1-bit feedback as well as the poles of the noise transfer function. Specifically, a modulator can be made more stable by placing the poles of the system closer to the noise-transfer-function

[^0]zeros. Also, a more stable modulator allows a larger maximum input signal level. However, this stability comes at a dynamic-range penalty since less of the noise power will then occur at out-of-band frequencies, but instead the noise will be greater over the in-band frequencies.

Since the stability issues of higher-order modulators are not well understood (particularly for arbitrary inputs), additional circuitry for detecting instability is often included, such as looking for long strings of 1 s or 0 s occurring. Alternatively, the signal amplitude at the input of the comparator might be monitored. If predetermined amplitude thresholds are exceeded for a specified number of consecutive clock cycles, then it is assumed that the converter has gone (or is going) unstable. In this case, the circuit is changed to make it more stable. One possibility is to turn on switches across the integrating capacitors of all integrators for a short time. This resets all integrator outputs to zero. A second alternative is to change the modulator into a second- or even first-order modulator temporarily by using only the first one or two integrators and resetting other integrators. Another possibility is to eliminate the comparator temporarily and feed back the input signal to the comparator. This changes the modulator into a stable filter.

Modulators having multi-bit internal quantization exhibit improved stability over their 1-bit counterparts, and are therefore often used in higher order modulators and at low OSR. When used for A/D conversion, they require highlinearity DACs. Fortunately, a number of architectures have been proposed to lessen the linearity requirements on the DACs, as described in Section 18.8.

### 18.7.2 Linearity of Two-Level Converters

Key Point: Multi-bit internal quantization improves stability and therefore is often used in high order modulators with low OSR. In A/D converters, it is combined with linearity enhancement techniques for the feedback DAC.

It was stated earlier that 1-bit D/A converters are inherently linear since they need only produce two output values and two points define a straight line. However, as usual, practical issues limit the linearity of D/A converters-even those having only two output levels. It should be pointed out here that most of the linearity issues discussed below are also applicable to multi-level converters, but we restrict our attention to two-level converters for clarity.

One limitation is when the two output levels somehow become functions of the low-frequency signal they are being used to create. For example, if the two voltage levels are related to power supply voltages, then these powersupply voltages might slightly rise and fall as the circuit draws more or less power. Since typically the amount of power drawn is related to the low-frequency signal being created, distortion will occur. A mechanism whereby this occurs is if a different amount of charge is being taken from the voltage references when a 1 is being output from the 1-bit $\mathrm{D} / \mathrm{A}$ converter, as opposed to when a 0 is being output from the $\mathrm{D} / \mathrm{A}$ converter. A somewhat more subtle but similar mechanism can occur due to the clock feedthrough of the input switches. This feedthrough is dependent on the gate voltages driving the input switches and therefore on the power-supply voltages connected to the drivers of the input switches. It is possible that these voltages can change when more 1 s than 0 s are being output by the D/A converter, having well-regulated power-supply voltages on the drivers for the input switches is very important. A similar argument can be made about any clock jitter in the converter. Thus, for high linearity it is important that the two output levels and associated clock jitter not be a function of the low-frequency input signal.

A more severe linearity limitation occurs if there is memory between output levels. For example, consider the ideal and typical output signals for a two-level D/A converter, shown in Fig. 18.24. The area for each symbol is defined to be the integral of the waveform over that symbol's time period. Notice that for the typical output signal, the area is dependent on the past symbol and that difference is depicted using $\delta_{i}$. As an illustrative example, consider the average voltage for three periodic patterns corresponding to average voltages of $0,1 / 3$, and $-1 / 3$ when $V_{1}$ and $V_{2}$ are $\pm 1$ volt.

In the ideal case, both $\delta_{1}$ and $\delta_{2}$ are zero as the waveform is memoryless. Thus, the three periodic patterns 0 , $1 / 3$, and $-1 / 3$ result in the following averages:
image_name:Fig. 18.24
description:The graph shown in Fig. 18.24 is a time-domain waveform representing the output of a nonreturn-to-zero (NRZ) 1-bit digital-to-analog converter (D/A converter). The waveform is plotted with voltage on the vertical axis, labeled as \( V_1 \) and \( V_2 \), and time on the horizontal axis, although specific time units are not provided. The waveform depicts two types of signals: an 'ideal' waveform indicated by a dashed line and a 'typical' waveform represented by a solid line.

Graph Details:
1. **Type of Graph and Function:**
- This is a time-domain waveform graph illustrating the behavior of an NRZ D/A converter output.

2. **Axes Labels and Units:**
- **Vertical Axis:** Voltage levels, indicated as \( V_1 \) and \( V_2 \).
- **Horizontal Axis:** Time, though specific units are not mentioned.

3. **Overall Behavior and Trends:**
- The waveform alternates between two voltage levels, representing binary states (1 and -1).
- For the 'ideal' waveform, transitions between voltage levels are instantaneous, maintaining a constant level until the next transition.
- The 'typical' waveform shows slight deviations from the ideal, with overshoots and undershoots at transitions, indicating non-ideal behavior such as ringing or settling time issues.

4. **Key Features and Technical Details:**
- The graph shows binary symbols (1 and -1) along with the associated areas for symbols, labeled as \( A_1 + \delta_1 \), \( A_1 \), \( A_0 + \delta_2 \), and \( A_0 \), where \( \delta_1 \) and \( \delta_2 \) represent deviations from the ideal area.
- The waveform is periodic, with each cycle corresponding to a sequence of binary symbols.
- The 'typical' waveform exhibits ringing effects, which are deviations from the 'ideal' waveform.

5. **Annotations and Specific Data Points:**
- Annotations indicate the ideal and typical waveforms.
- The binary sequence and corresponding areas for symbols are marked below the waveform, indicating the specific area deviation for each symbol transition. This highlights the impact of non-ideal factors on the output signal.

This graph effectively demonstrates the differences between an ideal and a typical NRZ D/A converter output, emphasizing the effects of non-ideal behavior such as overshoot and ringing on the waveform.

Fig. 18.24 A nonreturn-to-zero (NRZ) 1-bit D/A converter typical output.

$$
\begin{aligned}
0: & \{1,-1,1,-1,1,-1,1,-1, \ldots\} \rightarrow \overline{\mathrm{v}_{\mathrm{a}}(\mathrm{t})}=\frac{\mathrm{A}_{1}+\mathrm{A}_{0}}{2} \\
1 / 3: & \{1,1,-1,1,1,-1,1,1,-1, \ldots\} \rightarrow \overline{\mathrm{v}_{\mathrm{b}}(\mathrm{t})}=\frac{2 \mathrm{~A}_{1}+\mathrm{A}_{0}}{3} \\
-1 / 3: & \{-1,-1,1,-1,-1,1,-1,-1,1, \ldots\} \rightarrow \overline{\mathrm{v}_{\mathrm{c}}(\mathrm{t})}=\frac{\mathrm{A}_{1}+2 \mathrm{~A}_{0}}{3}
\end{aligned}
$$

By calculating the differences, $\overline{\mathrm{v}_{\mathrm{b}}(\mathrm{t})}-\overline{\mathrm{v}_{\mathrm{a}}(\mathrm{t})}$ and $\overline{\mathrm{V}_{\mathrm{a}}(\mathrm{t})}-\overline{\mathrm{v}_{\mathrm{c}}(\mathrm{t})}$, and noting that they are identical, we conclude that $\overline{\mathrm{v}_{\mathrm{a}}(\mathrm{t})}, \overline{\mathrm{v}_{\mathrm{b}}(\mathrm{t})}$, and $\overline{\mathrm{v}_{\mathrm{c}}(\mathrm{t})}$ lie along a straight line and therefore this memoryless $\mathrm{D} / \mathrm{A}$ converter is perfectly linear.

In the typical waveform case, the three periodic patterns result in the following averages:

$$
\begin{aligned}
& 0: \quad\{1,-1,1,-1, \ldots\} \rightarrow \overline{\mathrm{v}_{\mathrm{d}}(\mathrm{t})}=\frac{\mathrm{A}_{1}+\mathrm{A}_{0}+\delta_{1}+\delta_{2}}{2}=\overline{\mathrm{v}_{\mathrm{a}}(\mathrm{t})}+\frac{\delta_{1}+\delta_{2}}{2} \\
& 1 / 3: \quad\{1,1,-1, \ldots\} \rightarrow \overline{\mathrm{v}_{\mathrm{e}}(\mathrm{t})}=\frac{2 \mathrm{~A}_{1}+\mathrm{A}_{0}+\delta_{1}+\delta_{2}}{3}=\overline{\mathrm{v}_{\mathrm{b}}(\mathrm{t})}+\frac{\delta_{1}+\delta_{2}}{3} \\
& -1 / 3: \quad\{-1,-1,1, \ldots\} \rightarrow \overline{\mathrm{v}_{\mathrm{f}}(\mathrm{t})}=\frac{\mathrm{A}_{1}+2 \mathrm{~A}_{0}+\delta_{1}+\delta_{2}}{3}=\overline{\mathrm{v}_{\mathrm{c}}(\mathrm{t})}+\frac{\delta_{1}+\delta_{2}}{3}
\end{aligned}
$$

Now, these three averages do not lie on a straight line except when $\delta_{1}=-\delta_{2}$. Thus, one way to obtain high linearity is to match falling and rising signals - a very difficult task since they are typically realized with different types of devices.

A better way to obtain linearity without matching rising and falling signals of the $\mathrm{D} / \mathrm{A}$ converter is to use some sort of memoryless coding sc heme. For example, consider the return-to-zero coding scheme shown in Fig. 18.25. It is not difficult to see here that since the area of one output bit does not depend on any previous bits, the coding scheme is memoryless and the output signal will remain linear. Naturally, other memoryless schemes can also be used, such as using two levels of opposite signs but ensuring that the signal settles to ground between samples.

It is of interest to see how this memoryless coding is applied in oversampling A/D converters. Presently, most oversampling $\mathrm{A} / \mathrm{D}$ converters are realized using a switched-capacitor technology for linearity reasons. Switched capacitor circuits naturally realize memoryless levels as long as enough time is left for settling on each clock phase. In other words, switched-capacitor circuits implement memoryless coding since capacitors are charged on one clock phase and discharged on the next. For the same reason, the first stage of filtering in oversampling D/A
image_name:Fig. 18.25
description:**Type of Graph and Function:**
The graph is a time-domain waveform illustrating a return-to-zero (RZ) coding scheme. This is a type of digital signal representation where each bit is represented by a pulse that returns to zero before the next bit is sent.

**Axes Labels and Units:**
- The vertical axis represents voltage levels, labeled as \( V_1 \) and \( V_2 \). These are likely in volts, though units are not explicitly mentioned.
- The horizontal axis represents time, with no specific units or scale provided. The time intervals correspond to the duration of each bit or symbol.

**Overall Behavior and Trends:**
The waveform alternates between two voltage levels, \( V_1 \) and \( V_2 \), with each bit or symbol clearly defined. The waveform returns to zero between each symbol, characteristic of the RZ coding scheme. The waveform shows periodic behavior, with consistent pulse shapes for each bit.

**Key Features and Technical Details:**
- The waveform consists of a series of pulses, each representing a binary digit (either 1 or -1).
- The pulses rise sharply from \( V_1 \) to \( V_2 \) and then fall back to zero before the next pulse begins.
- The ideal waveform is shown as a dashed line, indicating the expected shape of the pulse, while the solid line represents a typical waveform, which may have slight deviations from the ideal.
- Binary values are annotated below the waveform, with '1' represented by a positive pulse and '-1' by a negative pulse.
- Areas labeled \( A_1 \) and \( A_0 \) indicate the area under the pulse for each symbol, which is important for understanding the energy or power associated with each bit.

**Annotations and Specific Data Points:**
- The graph includes annotations such as "Ideal" and "Typical" to distinguish between the theoretical waveform and a more realistic one that might occur in practice.
- The binary sequence is clearly marked below the waveform, providing a direct correlation between the waveform and the digital data it represents.

Fig. 18.25 A return-to-zero (RZ) coding scheme, which is one example of a memoryless coding scheme.
converters is often realized using switched-capacitor filters, which is followed by continuous-time filtering. However, some type of memoryless coding should be used when high linearity is desired from a 1-bit D/A output either fed directly to a continuous-time filter in an oversampling $\mathrm{D} / \mathrm{A}$ or used in the internal operation of a contin-uous-time oversampling A/D converter.

### 18.7.3 Idle Tones

Consider the case of applying a dc level of $1 / 3$ to a first-order $\Delta \Sigma$ modulator having a 1 -bit quantizer with output levels of $\pm 1$ (as in Example 18.4). With such an input, the output of the modulator will be a periodic sequence of two 1 s and one -1 . In other words,

$$
\begin{equation*}
\mathrm{y}(\mathrm{n})=\{1,1,-1,1,1,-1,1,1, \ldots\} \tag{18.50}
\end{equation*}
$$

This output periodic pattern is three cycles long and its power is concentrated at dc and $f_{s} / 3$. Although the output pattern is periodic, the post low-pass filter will eliminate the high-frequency content such that only the dc level of $1 / 3$ remains.

Now consider applying a dc level of $(1 / 3+1 / 24)=3 / 8$ to the same modulator. For this case, the output sequence becomes

$$
\begin{equation*}
y(n)=\{1,1,-1,1,1,-1,1,1,-1,1,1,-1,1,1,1,-1,1,1,-1, \ldots\} \tag{18.51}
\end{equation*}
$$

The period of this output pattern is now 16 cycles long and has some power at $f_{s} / 16$. With an oversampling ratio of eight (i.e., $f_{0}=f_{s} / 16$ ), the post low-pass filter will not attenuate the signal power at $f_{s} / 16$ since that frequency is just within the frequency band of interest. In other words, a dc level of $3 / 8$ into this modulator will produce the correct dc output signal but have a superimposed $f_{s} / 16$ signal on it even when using a brick-wall type low-pass filter.

While the preceding example shows a tone occurring at $f_{s} / 16$, it is not difficult to find other cases that would produce frequency tones at much lower frequencies, say $\mathrm{f}_{\mathrm{s}} / 256$. Such low-frequency tones will not be filtered out by the next stage low-pass filter and can lead to annoying tones in the audible range. ${ }^{8}$ In addition, although a firstorder modulator was used in the above example, it has been shown that annoying audible tones exist even in higher-order modulators [Norsworthy, 1993]. Finally, it should be mentioned that these tones might not lie at a single frequency but instead be short-term periodic patterns. In other words, a tone appearing near 1 kHz might actually be a signal varying between 900 Hz and 1.1 kHz in a random-like fashion.
image_name:Fig. 18.26 Adding dithering to a delta-sigma modulator
description:The system block diagram titled "Fig. 18.26 Adding dithering to a delta-sigma modulator" illustrates the process of incorporating dithering into a delta-sigma modulation system. The primary components and their functions are as follows:

1. **Main Components:**
- **Adder/Subtractor:** The diagram begins with an adder/subtractor where the input signal \( u(n) \) is combined with a feedback signal. This block serves to integrate the input signal with feedback for error correction.
- **Transfer Function Block \( H(z) \):** Following the adder, the signal passes through a block labeled \( H(z) \), which represents a filter or transfer function. This block shapes the signal in the frequency domain, typically to enhance certain frequencies and suppress others.
- **Dither Signal Adder:** A second adder is used to incorporate a "Dither signal" into the modulated signal. Dithering involves adding a small amount of noise to reduce quantization errors and idle tones.
- **Quantizer:** The signal, now combined with dither, enters the quantizer. The quantizer converts the continuous range of input values into discrete levels, effectively digitizing the signal.

2. **Flow of Information or Control:**
- The input signal \( u(n) \) enters the system and is combined with the feedback loop signal at the first adder.
- The modified signal is then processed by the transfer function block \( H(z) \), which shapes the signal.
- The dither signal is added to the processed signal, and this combination is fed into the quantizer.
- The quantized output \( y(n) \) is produced, which is also fed back to the initial adder to form a feedback loop, essential for delta-sigma modulation.

3. **Labels, Annotations, and Key Indicators:**
- The diagram is clearly labeled with input \( u(n) \) and output \( y(n) \) signals.
- The "Dither signal" label indicates the introduction of noise for dithering purposes.
- The quantizer is depicted with a stepped line, symbolizing the discretization process.

4. **Overall System Function:**
- The primary function of this system is to perform delta-sigma modulation with added dithering. The addition of the dither signal helps to minimize idle tones and quantization errors by randomizing the quantization noise. The feedback loop ensures that the system maintains stability and accuracy in signal processing, while the transfer function \( H(z) \) shapes the frequency response of the system.

Fig. 18.26 Adding dithering to a delta-sigma modulator. Note that the dithered signal is also noise shaped.

### 18.7.4 Dithering

One way to reduce the amount of idle tones in modulators is through the use of dithering. The term dithering here refers to the act of introducing some random (or pseudo-random) signal into a modulator.

Key Point: The nonlinear dynamics of 1-bit oversampling modulators can result in idle tones within the signal band when applying dc or slowlyvarying inputs. An additive pseudo-random dither signal can break up the tones but raises the noise floor.

Assuming the random signal to be introduced has a white-noise type spectrum, then the most suitable place to add the dithering signal is just before the quantizer, as shown in Fig. 18.26. The reason for adding it at this location is so that the dithering signal becomes noise shaped in the same manner as the quantization noise, and thus a large amount of dithering can be added. Typically, the dithering signal is realized using some sort of pseudo-random number generator with only a few bits of resolution, but its total noise power is comparable to the quantization noise power. Thus, the use of dithering in a $\mathrm{D} / \mathrm{A}$ converter would require a small additional digital adder, while a small $\mathrm{D} / \mathrm{A}$ converter would be needed in an oversampling A/D converter.

It should be noted that the use of dither to reduce idle tones is not an attempt to add noise to mask out the tones but instead breaks up the tones so that they never occur. However, since the noise power of the dithering signal is similar to the quantization noise power, the use of dithering adds about 3 dB extra in-band noise and often requires rechecking the modulator's stability.

### 18.7.5 Opamp Gain

A switched-capacitor integrator with a finite opamp gain, $A$, results in the integrator having a transfer function (see Problem 14.6) of

$$
\begin{equation*}
\frac{V_{0}(z)}{V_{i}(z)}=-\left(\frac{C_{1}}{C_{2}}\right)\left(\frac{1}{z\left(1+\frac{C_{1}}{C_{2} A}\right)-1}\right) \tag{18.52}
\end{equation*}
$$

Assuming $\mathrm{C}_{2} \approx \mathrm{C}_{1}$ as is typical in oversampled converters, the pole has moved to the left of $\mathbf{z}=1$ by an amount $1 / A$. With this knowledge, we can determine the new NTF zeros due to finite opamp gain by substituting $\mathbf{z}-1$ with $\mathbf{Z}-(1-1 / A)$. In other words, we substitute all ideal integrators with damped integrators and recalculate the transfer functions. Such an approach results in the NTF zeros, which were located at $\mathbf{Z}=1$ for a low-pass design, to be moved to $\mathbf{Z}=(1-1 / A)$. Thus, the shaped quantization noise does not drop to zero at dc but instead levels off near dc. Such a zero near $Z=1$ results in the $3-\mathrm{dB}$ break frequency being approximately equal to $1 / \mathrm{A} \mathrm{rad} /$ sample. Now, we note that the frequency band of interest, $f_{0}$, should be greater than $1 / A \mathrm{rad} / \mathrm{sample}$ since the shaped quantization noise is flat below that level. In other words, if $f_{0}$ is below where the quantization noise flattens
out, then we are not obtaining any further noise-shaping benefits. Thus, any further doubling of the oversampling ratio will only improve the SNR by $3 \mathrm{~dB} /$ octave. Finally, we can write the following requirement:

$$
\begin{equation*}
\frac{f_{0}}{f_{s}}>\frac{1 / A}{2 \pi} \tag{18.53}
\end{equation*}
$$

and recalling that $O S R=f_{s} /\left(2 f_{0}\right)$, we can rearrange this to

$$
\begin{equation*}
\mathrm{A}>\frac{\mathrm{OSR}}{\pi} \tag{18.54}
\end{equation*}
$$

Of course, some approximations have been made here, such as having the two capacitors of the integrator equal (that is $\mathrm{C}_{2} \approx \mathrm{C}_{1}$ ) and having the $3-\mathrm{dB}$ break point being sharp, as well as allowing noise to be flat from dc to $f_{0}$ (rather than shaped). In summary, designers will typically ensure that the opamp gain is at least twice the oversampling ratio, which is not usually a difficult requirement.

In addition, the above analysis only applies to modulators having a single D/A feedback and does not apply to MASH or cascade modula-

Key Point: Opamps in analog oversampling modulators should have a dc gain at least twice the oversampling ratio, which is not usually a difficult requirement. An exception is MASH modulators where higher gains may be required to ensure digital and analog transfer functions are matched.
tors, where larger opamp gains are often required to aid matching between digital and analog signal paths.

## 18.8 MULTI-BIT OVERSAMPLING CONVERTERS

Although 1-bit oversampling converters have the advantage that they can realize highly linear data conversion, they also have some disadvantages. For example, 1-bit oversampling modulators are prone to instability due to the high degree of nonlinearity in the feedback. Another disadvantage is the existence of idle tones, as previously discussed. Additionally, in oversampling D/A converters, the use of a 1-bit D/A converter results in a large amount of out-of-band quantization noise, which must be significantly attenuated using analog circuitry. Such a task often requires relatively high-order analog filtering (recall that the low-pass filter should be at least one order higher than the modulator order). Also, the dynamic range of the analog filter may have to be significantly higher than the converter's dynamic range since the filter's input must cope with power of both the quantization noise and signal itself. Since the quantization noise may be up to 15 dB larger in level than the signal level, such an extension in the dynamic range makes the realization of analog filters for oversampling D/A converters nontrivial. The use of a multi-bit $\mathrm{D} / \mathrm{A}$ converter can significantly reduce this large amount of quantization noise, but care must be taken to ensure that the multi-bit converter remains linear. Typically, a multi-bit oversampling system would be similar to that shown in Fig. 18.16, except that an M-bit quantizer would be used in the digital modulator, and its output would drive an M-bit D/A converter. This section will briefly discuss some multi-bit oversampling converter architectures that employ methods so that the overall system remains highly linear.

### 18.8.1 Dynamic Element Matching

One approach for realizing a multi-bit D/A converter intended for oversampling systems is that of dynamic element matching [Carley, 1989]. With this approach, a thermometer-code D/A converter is realized, and randomization is used to effectively spread the nonlinearity over the whole frequency range. For example, a 3-bit D/A converter using dynamic element matching is shown in Fig. 18.27. Here, the 8 -line randomizer makes use of

Key Point: Dynamic element matching randomizes the use of analog elements in a D/A to eliminate the tones that would otherwise result from mismatches, making instead spec-trally-shaped noise. It enables the use of multi-bit D/As in highly linear oversampling converters.
image_name:Fig. 18.27 Dynamic element matching 3-bit D/A converter
description:The circuit is a 3-bit D/A converter using dynamic element matching. It includes a thermometer-type decoder and an eight-line randomizer to distribute signals to eight unit capacitors. The capacitors are summed to produce the analog output.

Fig. 18.27 Dynamic element matching 3-bit D/A converter.
a pseudo-random code to distribute the thermometer lines equally to each of the unit capacitances, C. Using the simplest randomization approaches, the mismatch "noise" from this multi-bit converter is not shaped by any feedback loop and therefore appears more white than high-pass filtered [Carley, 1989].

Dynamic element matching has been extended to include noise shaping the nonlinearity introduced by the D/A [Leung, 1992; Galton, 1997]. These approaches enable much lower oversampling ratios and can be used while maintaining high linearity with a reasonably coarse DAC mismatch. They are currently the most popular approach to mitigating D/A nonlinearity errors in oversampling converters. Some examples are [Chen, 1995; Adams, 1995; Baird, 1995].

### 18.8.2 Dynamically Matched Current Source D/A Converters

Another method of maintaining high linearity in an oversampling D/A system is through the use of a highly linear $\mathrm{D} / \mathrm{A}$ converter operating at the fast oversampling rate. Such high linearity has been achieved using dynamically matched current sources similar to those described in Section 16.3.3 [Schouwenaars, 1991].

### 18.8.3 Digital Calibration A/D Converter

One way to make use of a multi-bit $\mathrm{D} / \mathrm{A}$ converter in an oversampling $\mathrm{A} / \mathrm{D}$ modulator is to have a calibration cycle where digital circuitry is used to model the static nonlinearity of the D/A converter, as shown in Fig. 18.28 [Larson, 1988]. With this approach, the multi-bit digital signal $\mathrm{x}_{2}(\mathrm{n})$ creates $2^{N}$ output levels at $\mathrm{x}_{1}(\mathrm{n})$, which are consistent in time but not necessarily linearly related to $x_{2}(n)$. However, the feedback loop of the modulator forces the in-band frequency of $x_{1}(n)$ to very closely equal $u(n)$, and thus $x_{1}(n)$ is still linearly related to $u(n)$. Through the use of the digital correction circuitry, the signal $y(n)$ also equals $x_{1}(n)$ if its nonlinearity equals that of the D/A converter. To realize this digital correction circuitry, a $2^{\mathrm{N}}$ word look-up RAM is used where the size of each RAM word is at least equal to the desired linearity. For example, if a 4 -bit D/A converter is used and 18 bits of linearity is desired, then the digital correction circuitry consists of a 16-word RAM, each of length 18 bits or greater (or equivalently, a 288bit RAM). Furthermore, this RAM size can be reduced by digitizing only the difference between the desired linearity and the expected linearity of the D/A converter [Sarhang-Nejad, 1993]. For example, if the D/A converter is
image_name:Fig. 18.28 Digitally corrected multi-bit A/D modulator.
description:The system block diagram represents a digitally corrected multi-bit A/D modulator. The primary function of this system is to enhance the linearity of an analog-to-digital conversion process through digital correction techniques.

Main Components:
1. **Adder/Subtractor Block (+):**
- Inputs: The primary input signal \( u(n) \) and a feedback signal \( x_1(n) \).
- Function: Computes the difference between the input signal and the feedback signal, producing an error signal that is fed to the next block.

2. **Filter Block \( H(z) \):**
- Input: Receives the error signal from the adder/subtractor.
- Function: Processes the error signal, typically applying noise shaping or filtering to improve signal quality before quantization.

3. **Quantizer (N bit):**
- Input: Receives the filtered signal from \( H(z) \).
- Function: Converts the analog signal into an \( N \)-bit digital signal \( x_2(n) \).

4. **Nonlinear D/A Converter (\( N_L \)):**
- Input: Receives the digital signal \( x_2(n) \) from the quantizer.
- Function: Converts the digital signal back into an analog signal, which is then used for feedback correction.

5. **Digital Correction Block (\( N_L \)):**
- Input: Takes the \( x_2(n) \) signal for correction.
- Function: Applies digital correction to the quantized signal to compensate for any nonlinearities introduced by the D/A conversion.
- Output: Produces the corrected digital output \( y(n) \).

Flow of Information or Control:
- The input signal \( u(n) \) is first combined with a feedback signal \( x_1(n) \) in the adder/subtractor, producing an error signal.
- This error signal is filtered by \( H(z) \), which shapes the noise and conditions the signal for quantization.
- The filtered signal is quantized into \( N \) bits by the quantizer, resulting in \( x_2(n) \).
- The quantized signal \( x_2(n) \) is used in two ways: it is fed into the nonlinear D/A converter for feedback purposes and into the digital correction block.
- The nonlinear D/A converter outputs an analog signal used as feedback \( x_1(n) \) to the initial adder/subtractor.
- Simultaneously, the digital correction block corrects \( x_2(n) \) to produce the final output \( y(n) \).

Labels, Annotations, and Key Indicators:
- **\( u(n) \):** Input signal.
- **\( x_1(n) \):** Feedback signal from the nonlinear D/A converter.
- **\( x_2(n) \):** Quantized digital signal.
- **\( y(n) \):** Corrected digital output.
- **Digital Correction:** Indicates the block responsible for compensating for nonlinearities.

Overall System Function:
The system is designed to improve the linearity of a multi-bit A/D modulator by employing digital correction techniques. The combination of feedback from the nonlinear D/A converter and digital correction ensures that the output signal \( y(n) \) closely matches the desired linearity, minimizing distortion and enhancing the accuracy of the analog-to-digital conversion process.

Fig. 18.28 Digitally corrected multi-bit A/D modulator.
expected to have a linearity of at least 9 bits, then the RAM need only have a word length of 10 bits for 18 -bit overall linearity.

The calibration of the digital correction circuitry can be accomplished by reconfiguring the $\Delta \Sigma \mathrm{A} / \mathrm{D}$ modulator to a single-bit system. Next, the input to this 1-bit converter is one of the 4 -bit $\mathrm{D} / \mathrm{A}$ converter levels to be calibrated. In other words, the multi-bit converter's input is held constant while its output is applied to the 1-bit A/D modulator for many clock cycles. The resulting 1-bit signal is digitally low-pass filtered and gives the desired digital equivalent value of that particular dc level for the D/A converter. This procedure is repeated 16 times to find all the 16 words of RAM.

Finally, it should be mentioned that a similar approach can be used to improve the linearity of a multi-bit oversampling D/A converter, except in this case the digital correction circuit would be in the feedback portion of the digital modulator.

### 18.8.4 A/D with Both Multi-Bit and Single-Bit Feedback

Another very interesting alternative architecture uses both multi-bit feedback and single-bit feedback [Hairapetian, 1994]. A third-order example of this $\mathrm{A} / \mathrm{D}$ is shown in Fig. 18.29. If one assumes that the errors due to the quantization of the 1-bit $\mathrm{A} / \mathrm{D}$ and 5-bit $\mathrm{A} / \mathrm{D}$ are $\mathrm{Q}_{1}$, and $\mathrm{Q}_{5}$, respectively, and also that the 5-bit $\mathrm{D} / \mathrm{A}$ injects errors due to its nonlinearity given by $Q_{d}$, then by applying a linear analysis to the system of Fig. 18.29 it can be shown that

$$
\begin{align*}
U_{s}(z)= & U(z) z^{-1}+Q_{1}(z) \frac{\left(1-z^{-1}\right)^{2}}{1-0.5 z^{-1}}-Q_{5}(z) \frac{z^{-1}\left(1-z^{-1}\right)^{-2}}{1-0.5 z^{-1}} \\
& -Q_{d}(z) \frac{z^{-1}\left(1-z^{-1}\right)^{-2}}{1-0.5 z^{-1}} \tag{18.55}
\end{align*}
$$

After digital signal processing, the digital output signal, $Y(z)$, is given by

$$
\begin{equation*}
Y(z)=U(z) z^{-1}+2 Q_{5}(z)\left(1-z^{-1}\right)^{3}-2 Q_{d}(z) z^{-1}\left(1-z^{-1}\right)^{2} \tag{18.56}
\end{equation*}
$$

It is seen that, based on the assumption of perfect integrators, the quantization noise due to the 1-bit $\mathrm{A} / \mathrm{D}$ is cancelled exactly, the quantization noise due to the 5-bit A/D undergoes third-order noise shaping, and the noise due to the nonlinearity of the 5 -bit $\mathrm{D} / \mathrm{A}$ converter undergoes second-order shaping. Of course, if the integrators are not perfect, then the cancellation of the quantization noise of the 1-bit $\mathrm{A} / \mathrm{D}$ will not be perfect, but any errors in the cancellation still undergo second-order noise shaping. It can be shown that the stability characteristics of this system are very similar to those of a second-order $\Delta \Sigma \mathrm{A} / \mathrm{D}$ converter. It should also be noted that the digital signal processing required does not require any multiplications, but that multi-bit signals must be processed by the following decimator, which complicates its realization.
image_name:Fig. 18.29 An A/D architecture that uses both multi-bit and single-bit feedback.
description:The block diagram represents an analog-to-digital (A/D) architecture that utilizes both multi-bit and single-bit feedback mechanisms. The system is designed to perform oversampling and noise shaping, characteristic of delta-sigma (ΔΣ) converters.

Main Components:
1. **Input Signal (U(z))**: The input to the system is denoted as U(z), which is processed through the architecture.
2. **Summing Junctions**: There are several summing junctions in the diagram that combine signals. The first summing junction takes the input U(z) and subtracts feedback signals.
3. **Delay Elements (z^-1)**: These are used to introduce unit delays in the signal path, contributing to the noise shaping properties of the system.
4. **A/D Converters**:
- **5-bit A/D Converter**: Converts the analog signal to a 5-bit digital signal.
- **1-bit A/D Converter**: Converts the analog signal to a 1-bit digital signal, providing a simpler but potentially less accurate conversion.
5. **D/A Converters**:
- **5-bit D/A Converter**: Converts the digital signal back to analog for feedback purposes.
- **1-bit D/A Converter**: Converts the digital signal back to analog for feedback purposes.
6. **Feedback Path**: The system includes feedback paths involving both the 5-bit and 1-bit converters.
7. **Gain Blocks**: Gain blocks labeled as 1/2 and 5 are used to scale signals appropriately within the system.
8. **Noise Shaping Block (2(1-z^-1)^2)**: This block is responsible for shaping the noise characteristics of the system, enhancing its performance by reducing quantization noise in the signal band.
9. **Output Signal (Us(z))**: The processed output signal is denoted as Us(z).

Flow of Information or Control:
- The input signal U(z) enters the system and is processed through a series of summing junctions and delay elements. The feedback loops, facilitated by the 5-bit and 1-bit converters, modify the input signal by subtracting the feedback signals.
- The processed signal is then converted to digital form by the A/D converters. The digital signals are fed back through the D/A converters to form feedback loops that help in noise shaping.
- The gain blocks adjust the signal levels to maintain the desired system performance.
- The noise shaping block further processes the signal to minimize quantization noise.
- The final output, Us(z), represents the digitally converted and processed signal.

Labels, Annotations, and Key Indicators:
- **V1, V2, V3**: These labels indicate intermediate signals within the processing chain.
- **Q5 - Q1**: Represents the difference between the quantized outputs of the 5-bit and 1-bit converters.
- **C(z) and Y(z)**: Intermediate signals used in the noise shaping process.

Overall System Function:
The primary function of this A/D architecture is to convert analog signals to digital form while employing noise shaping techniques to enhance accuracy and reduce quantization noise. The use of both multi-bit and single-bit feedback paths allows the system to balance complexity and performance, making it suitable for applications requiring high precision and oversampling capabilities.

Fig. 18.29 An A/D architecture that uses both multi-bit and single-bit feedback.

## 18.9 THIRD-ORDER A/D DESIGN EXAMPLE

In this section, a design example is presented for a third-order oversampled switched-capacitor $\mathrm{A} / \mathrm{D}$ converter. In this example, all the zeros of the noise transfer function (NTF) are placed at $\mathbf{z}=1$ (i.e., dc) so that the converter could be used for various oversampling ratios. In other words, the zeros are not spread over the frequency band of interest, as that would restrict the converter's usefulness to a particular oversampling ratio.

Since all the zeros are assumed to be at $\mathbf{z}=1$, the NTF has the following form:

$$
\begin{equation*}
\operatorname{NTF}(z)=\frac{(z-1)^{3}}{D(z)} \tag{18.57}
\end{equation*}
$$

To find the poles of the system, given by the roots of $D(z)$, we need to ensure modulator stability while shaping as much quantization noise away from dc as possible. To ensure modulator stability, recall that a heuristic approach is to restrict the peak NTF magnitude response to less than 1.5 . However, to shape the quantization noise away from dc, we wish to make the NTF as large as possible outside the frequency band of interest. Thus, the best NTF choice would be one which has a flat gain of 1.4 at high frequencies. Such a high-pass filter is obtained (i.e., no peaking in the NTF) when the poles are placed in a Butterworth configuration, as shown in Fig. 18.30. Thus, the

Fig. 18.30 Pole and zero locations for the third-order NTF.
image_name:Fig. 18.30
description:The graph in Fig. 18.30 is a pole-zero plot on the z-plane, which is commonly used in digital signal processing to represent the locations of poles and zeros of a transfer function.

1. **Type of Graph and Function:**
- This is a pole-zero plot on the z-plane.

2. **Axes Labels and Units:**
- The plot is centered on the complex plane with the real axis (horizontal) and the imaginary axis (vertical). The unit circle is shown, which is a common reference in z-plane plots.
- The frequency points are marked as \( \omega = 0 \), \( \omega = \pi/2 \), and \( \omega = \pi \).

3. **Overall Behavior and Trends:**
- The plot shows the distribution of zeros and poles for a third-order Noise Transfer Function (NTF).
- Zeros are located at the origin (\( \omega = 0 \)), which indicates high-pass characteristics as they block DC components.
- The poles are arranged in a Butterworth configuration, indicating a maximally flat frequency response within the passband.

4. **Key Features and Technical Details:**
- **Zeros:** Three zeros are located at the origin (\( \omega = 0 \)), emphasizing the high-pass nature of the filter.
- **Poles:** The poles are located on the unit circle, distributed symmetrically, indicating a Butterworth high-pass filter design. This arrangement helps achieve a flat gain at high frequencies.
- The Butterworth poles are positioned to ensure stability and a smooth transition in the frequency response.

5. **Annotations and Specific Data Points:**
- The plot includes annotations for the zeros and poles, with specific references to their locations and the type of filter they represent (Butterworth).
- The unit circle is a significant marker, indicating the boundary for stability in digital filters.

denominator is found using digital filter software to design a third-order high-pass digital filter where the passband is adjusted until the peak NTF is less than 1.4 (i.e., $\left|\operatorname{NTF}\left(\mathrm{e}^{\mathrm{j} \omega}\right)\right|<1.4$ ). Specifically, with a passband edge at $\mathrm{f}_{\mathrm{s}} / 20$, a third-order Butterworth high-pass filter has a peak gain equal to 1.37 , and thus the $\operatorname{NTF}(z)$ is given by

$$
\begin{equation*}
\operatorname{NTF}(z)=\frac{(z-1)^{3}}{z^{3}-2.3741 z^{2}+1.9294 z-0.5321} \tag{18.58}
\end{equation*}
$$

By rearranging (18.16), we can find $H(z)$ in term of $\operatorname{NTF}(z)$, resulting in

$$
\begin{equation*}
\mathrm{H}(\mathrm{z})=\frac{1-\operatorname{NTF}(z)}{\operatorname{NTF}(z)} \tag{18.59}
\end{equation*}
$$

which, for the function given in (18.58), results in

$$
\begin{equation*}
H(z)=\frac{0.6259 z^{2}-1.0706 z+0.4679}{(z-1)^{3}} \tag{18.60}
\end{equation*}
$$

Next, a suitable implementation structure is chosen. In this case, a cascade-of-integrators structure was used, as shown in Fig. 18.31. The $\alpha_{\mathrm{i}}$ coefficients are included for dynamic-range scaling and are initially set to $\alpha_{2}=\alpha_{3}=1$, while the last term, $\alpha_{1}$, is initially set equal to $\beta_{1}$. By initially setting $\alpha_{1}=\beta_{1}$, we are allowing the input signal to have a power level similar to that of the feedback signal, $y(n)$. In other words, if $\alpha_{1}$ were initially set equal to one and $\beta_{1}$ were quite small, then the circuit would initially be stable for only small input-signal levels.

Coefficient values for $\beta_{i}$ are then found by deriving the transfer function from the 1-bit $\mathrm{D} / \mathrm{A}$ output to $\mathrm{V}_{3}$ and equating that function to $-H(z)$ in (18.60). Specifically, assuming $\alpha_{2}=\alpha_{3}=1$, we find the following $H(z)$ :

$$
\begin{equation*}
H(z)=\frac{z^{2}\left(\beta_{1}+\beta_{2}+\beta_{3}\right)-z\left(\beta_{2}+2 \beta_{3}\right)+\beta_{3}}{(z-1)^{3}} \tag{18.61}
\end{equation*}
$$

Equating (18.61) with (18.60), we find an initial set of coefficients to be

$$
\begin{array}{rrl}
\alpha_{1}=0.0232, & \alpha_{2}=1.0, & \alpha_{3}=1.0 \\
\beta_{1}=0.0232, & \beta_{2}=0.1348, & \beta_{3}=0.4679 \tag{18.62}
\end{array}
$$

It is then necessary to perform dynamic-range scaling. Dynamic scaling is necessary to ensure that all nodes have approximately the same power level, so that all nodes will clip near the same level, and there will be no unnecessarily large noise gains from nodes with small signal levels. Here, dynamic-range scaling was accomplished by simulating the system in Fig. 18.31 with the coefficients just given and an input sinusoidal wave with a peak value of 0.7 at a frequency of $\pi / 256 \mathrm{rad} / \mathrm{sample}$. Following the simulation, the maximum values at nodes $\mathrm{V}_{1}, \mathrm{~V}_{2}, \mathrm{~V}_{3}$ were found to be $0.1256,0.5108$, and 1.004 , respectively. To increase the output level of a node by a
image_name:Fig. 18.31
description:The system block diagram in Fig. 18.31 represents a third-order sigma-delta modulator using a cascade-of-integrators structure. This diagram is designed to perform analog-to-digital conversion with noise shaping, typically used in high-resolution audio applications.

1. **Main Components:**
- **Integrators:** There are three integrators in the system, each represented by a block containing a summation point and a delay element (denoted as \(z^{-1}\)). These integrators accumulate the input signal and feedback signals, shifting them in time.
- **Summation Points:** Each integrator is preceded by a summation point that combines the input signal or feedback signals with the output of the previous stage.
- **Quantizer:** This component converts the analog signal into a digital signal, effectively reducing the signal to a 1-bit digital output.
- **1-bit D/A Converter:** Converts the digital output back into an analog signal for feedback purposes.

2. **Flow of Information or Control:**
- The input signal \(u(n)\) enters the first summation point, where it is combined with a feedback signal weighted by \(\beta_1\).
- The output from the first summation point is integrated and passed to the next stage, V1, where it is combined with another feedback signal weighted by \(\beta_2\).
- This process repeats for the second integrator, passing its output V2 to the third integrator, where it combines with a feedback signal weighted by \(\beta_3\).
- The output of the third integrator, V3, is fed into the quantizer.
- The quantized output \(y(n)\) is then converted back to an analog signal via the 1-bit D/A converter to be used as feedback for the integrators.

3. **Labels, Annotations, and Key Indicators:**
- The coefficients \(\alpha_1, \alpha_2, \alpha_3\) are used for dynamic-range scaling.
- The feedback coefficients \(\beta_1, \beta_2, \beta_3\) determine the influence of the output on each integrator.
- Nodes V1, V2, V3 are labeled to indicate the signal levels at each stage of integration.

4. **Overall System Function:**
- The primary function of this system is to perform sigma-delta modulation, which is a method of oversampling and noise shaping to achieve high-resolution digital output from an analog input. The cascade-of-integrators structure helps in distributing the quantization noise over a broader frequency range, allowing for better signal-to-noise ratio in the desired signal band.

Fig. 18.31 The cascade-of-integrators structure used to realize the third-order modulator. Note that $\alpha_{i}$ coefficients are used for dynamic-range scaling and are initially set to $\alpha_{1}=\beta_{1}$ and $\alpha_{2}=\alpha_{3}=1$.
image_name:Fig. 18.31
description:The circuit is a third-order modulator using a cascade-of-integrators structure. It includes dynamic-range scaling with coefficients α and β. The modulator uses switched-capacitor techniques for implementation.
image_name:Fig. 18.32
description:The circuit is a switched-capacitor realization of a third-order modulator. It uses a cascade-of-integrators structure with dynamic range scaling coefficients. The structure helps in distributing quantization noise over a broader frequency range.

Fig. 18.32 A switched-capacitor realization of the third-order modulator example.
factor k, the input branches should be multiplied by k, while the output branches should be divided by k. For example, the maximum value of node $\mathrm{V}_{1}$ is increased to unity by multiplying both $\alpha_{1}$ and $\beta_{1}$ by $1 / 0.1256$ and dividing $\alpha_{2}$ by $1 / 0.1256$. Similarly, node $V_{2}$ is scaled by dividing $0.1256 \alpha_{2}$ and $\beta_{2}$ by 0.5108 and multiplying $\alpha_{3}$ by 0.5108 . Node $V_{3}$ was left unchanged, as its maximum value was already near unity. Such a procedure results in the following final values for the coefficients.

$$
\begin{array}{lll}
\alpha^{\prime}{ }_{1}=0.1847, & \alpha^{\prime}{ }_{2}=0.2459, & \alpha^{\prime}=0.5108 \\
\beta^{\prime}=0.1847, & \beta^{\prime}{ }_{2}=0.2639, & \beta_{3}^{\prime}=0.4679 \tag{18.63}
\end{array}
$$

Finally, the block diagram of Fig. 18.31 can be realized by the switched-capacitor circuit shown in Fig. 18.32 to obtain the final oversampled A/D converter.

## 18.10 KEY POINTS

- Oversampling converters relax the requirements placed on the analog circuitry at the expense of more complicated digital circuitry. [p. 696]
- Quantization with a step size "LSB" can be modeled as an additive quantization noise uniformly distributed between $-\mathrm{LSB} / 2$ and $+\mathrm{LSB} / 2$ with a white power spectrum and total power of LSB2/12. [p. 697]
- Oversampling a signal at OSR times the Nyquist rate, without spectrally shaping the quantization noise, results in a SNR enhancement of $10 \log (\mathrm{OSR}) \mathrm{dB}$. [p. 700]
- One-bit D/A converters are inherently linear. Hence, when combined with a high oversampling ratio, they can provide a good signal to quantization noise and distortion ratio. [p. 702]
- To shape the spectrum of a quantization noise source, it is placed within a feedback loop whose response is designed to attenuate the quantization noise in the band of interest. [p. 704]
- Using a single integrator inside a DS modulator feedback loop places a zero at dc in the noise transfer function providing first-order noise shaping for low-pass signals. [p. 704]
- First-order noise shaping permits SQNR to increase by 1.5 bits/octave with respect to oversampling ratio, or 9 dB for every doubling of OSR. [p. 706]
- Second-order noise shaping increases SQNR by 15 dB for each doubling of OSR, or equivalently by 1.5 bits/ octave. [p. 708]
- The input signal power is often limited to well below the maximum quantizer swing to ensure stability, resulting in reduced SQNR. [p. 709]
- Oversampling A/D converters require additional digital low-pass filtering, but less analog anti-aliasing filtering-often an desirable trade-off in integrated circuits. [p. 711]
- The linearity of oversampled $\mathrm{A} / \mathrm{D}$ converters depends more strongly on the linearity of its internal $\mathrm{D} / \mathrm{A}$ converter than on its internal quantizer. [p. 712]
- Oversampling D/A converters require a very linear but low-resolution internal D/A converter, and an analog smoothing filter whose order should be at least one greater than that of the noise shaping and must have sufficient dynamic range to accommodate both signal and large quantization noise power at its input. [p. 713]
- In a multi-stage decimation filter, an initial lowpass filter removes much of the quantization noise. Its output is then downsampled so that the remaining filtering can be performed at a lower clock frequency. [p. 715]
- In single-stage decimation, one filter operates on a low-resolution noise-shaped signal providing the decimated output. Because of the high filter order, several time-interleaved filters may be used in parallel. [p. 717]
- Noise shaping with order $\mathrm{L}>2$ offers the potential for further improvements in SQNR of $6 \mathrm{~L}+3 \mathrm{~dB} /$ octave or $\mathrm{L}+0.5$ bits/octave with respect to oversampling ratio. [p. 718]
- Interpolative higher-order modulators permit the arbitrary placement of noise transfer function zeros, offering improved SQNR performance compared to the placement of all zeros at dc, especially for relatively low OSR. However, it is nontrivial to guarantee stability for such structures, and they are therefore often combined with multi-bit internal quantizers. [p. 718]
- Multi-stage noise shaping (MASH) oversampling converters cascade lower order modulators to realize highorder noise shaping. Since the constituent stages are each first- or second-order, it is easy to ensure stability. However, MASH converters require digital filtering whose coefficients are matched to those of analog circuitry. [p. 720]
- The stability of 1-bit modulators is not well understood, but as a rule of thumb keeping the peak magnitude response of the noise transfer function below 1.5 often results in a stable modulator. [p. 722]
- Multi-bit internal quantization improves stability and therefore is often used in high order modulators with low OSR. In A/D converters, it is combined with linearity enhancement techniques for the feedback DAC. [p. 723]
- The nonlinear dynamics of 1-bit oversampling modulators can result in idle tones within the signal band when applying dc or slowly-varying inputs. An additive pseudo-random dither signal can break up the tones but raises the noise floor. [p. 726]
- Opamps in analog oversampling modulators should have a dc gain at least twice the oversampling ratio, which is not usually a difficult requirement. An exception is MASH modulators where higher gains may be required to ensure digital and analog transfer functions are matched. [p. 727]
- Dynamic element matching randomizes the use of analog elements in a $\mathrm{D} / \mathrm{A}$ to eliminate the tones that would otherwise result from mismatches, making instead spectrally-shaped noise. It enables the use of multi-bit D/As in highly linear oversampling converters. [p. 727]
