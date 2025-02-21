# 15 Data Converter Fundamentals

In this chapter, fundamental aspects of analog-to-digital (A/D) and digital-to-analog (D/A) converters are presented without regard for their internal architecture or circuit design. In effect, converters are treated in this chapter as black boxes such that only their input-output relationships are discussed. Internal architectures and circuits techniques for realizing data converters are discussed in following chapters.

Before proceeding, it is useful to make the distinction between two main types of data converters.

Key Point: In Nyquist-rate converters, there is a one-to-one correspondence between input and output values. Oversampling converters increase SNR by operating much faster than the input signal's Nyquist rate and filtering out quantization noise outside of the signal bandwidth.

Nyquist-Rate Converters We loosely define Nyquist-rate data converters as those converters that generate a series of output values in which each value has a one-to-one correspondence with a single input value. For example, a Nyquist-rate D/A converter would generate a series of analog output levels, where each level is a result of a single B-bit input word. However, it should be noted that Nyquist-rate converters are seldom used at the Nyquist rate due to the difficulty in realizing practical anti-aliasing and reconstruction filters. In most cases, Nyquist rate converters operate at 1.5 to 10 times the Nyquist rate (i.e., 3 to 20 times the input signal's bandwidth).

Oversampling Converters Oversampling con verters are those converters that operate much faster than the input signal's Nyquist rate (typically 10 to 512 times faster) and increase the output's signal-to-noise ratio (SNR) by filtering out quantization noise that is not in the signal's bandwidth. In A/D converters, this filtering is performed digitally, whereas in D/A converters, analog filtering is used. Most often, oversampling converters use noise shaping to place much of the quantization noise outside the input signal's bandwidth (see Chapter 18).

This distinction is made here since much of the descriptions that follow refer more closely to Nyquist-rate converters than to oversampling converters.

## 15.1 IDEAL D/A CONVERTER

Consider the block diagram of an N -bit $\mathrm{D} / \mathrm{A}$ converter shown in Fig. 15.1. Here, $\mathrm{B}_{\text {in }}$ is defined to be an N -bit digital signal (or word) such that

$$
\begin{equation*}
\mathrm{B}_{\mathrm{in}}=\mathrm{b}_{1} 2^{-1}+\mathrm{b}_{2} 2^{-2}+\cdots+\mathrm{b}_{\mathrm{N}} 2^{-\mathrm{N}} \tag{15.1}
\end{equation*}
$$

where $b_{i}$ equals 1 or 0 (i.e., $b_{i}$ is a binary digit). We also define $b_{1}$ as the most significant bit (MSB) and $b_{N}$ as the least significant bit (LSB). Furthermore, we have assumed here that $\mathrm{B}_{\text {in }}$ represents a positive value, resulting in a unipolar D/A converter. A unipolar D/A converter produces an output signal of only one polarity. In contrast, signed converters produce output signals of either positive or negative polarity, depending on a sign bit (usually $b_{1}$ ). Extending the following concepts to the signed case is straightforward but requires knowledge of the type of digital representation used (i.e., sign magnitude, offset binary, or 2's complement). Signed codes are discussed in Section 15.4.
image_name:Fig. 15.1
description:The block diagram labeled "Fig. 15.1" represents a Digital-to-Analog (D/A) converter system. The main components of this system are as follows:

1. **D/A Converter Block**: This is the central component of the diagram. It receives digital input signals and an analog reference signal, and it outputs an analog signal. The D/A converter's primary function is to convert the digital input into an analog output, using the reference voltage as a scaling factor.

2. **Input Signals**:
- **$B_{in}$**: This is the digital input signal to the D/A converter. It consists of a series of digital bits that represent a numerical value to be converted into an analog signal.
- **$V_{ref}$**: This is the analog reference signal supplied to the D/A converter. It serves as a reference voltage that determines the scale of the analog output.

3. **Output Signal**:
- **$V_{out}$**: This is the analog output signal produced by the D/A converter. It is the result of converting the digital input, $B_{in}$, using the reference voltage, $V_{ref}$.

**Flow of Information**:
- The digital input signal ($B_{in}$) flows into the D/A converter block from the left side.
- The reference voltage ($V_{ref}$) is also fed into the D/A converter from below.
- The D/A converter processes these inputs to produce an analog output signal ($V_{out}$), which exits the block on the right side.

**Overall System Function**:
The primary function of this system is to convert a digital signal into an analog signal. The digital input ($B_{in}$) is converted into an analog output ($V_{out}$) by the D/A converter, with the conversion process being influenced by the reference voltage ($V_{ref}$). This setup allows for the precise generation of analog signals based on digital inputs, which is essential in various applications such as audio processing, instrumentation, and control systems.

Fig. 15.1 A block diagram representing a D/A converter.

The analog output signal, $\mathrm{V}_{\text {out }}$, is related to the digital signal, $\mathrm{B}_{\text {in }}$, through an analog reference signal, $\mathrm{V}_{\text {ref }}$. For simplicity, we assume that both $\mathrm{V}_{\text {out }}$ and $\mathrm{V}_{\text {ret }}$ are voltage signals, although, in general, they may be other physical quantities, such as current or charge. The relationship between these three signals for a unipolar D/A converter is given by

$$
\begin{equation*}
\mathrm{V}_{\text {out }}=\mathrm{V}_{\text {ref }}\left(\mathrm{b}_{1} 2^{-1}+\mathrm{b}_{2} 2^{-2}+\cdots+\mathrm{b}_{\mathrm{N}} 2^{-\mathrm{N}}\right)=\mathrm{V}_{\text {ref }} \mathrm{B}_{\text {in }} \tag{15.2}
\end{equation*}
$$

It is useful to define $\mathrm{V}_{\mathrm{LSB}}$ to be the voltage change when one LSB changes, or, mathematically,

$$
\begin{equation*}
V_{\mathrm{LSB}} \equiv \frac{\mathrm{~V}_{\mathrm{ref}}}{2^{\mathrm{N}}} \tag{15.3}
\end{equation*}
$$

Also useful (particularly in measuring errors) is the definition of a new "unit," namely, LSB units, which are in fact unitless.

$$
\begin{equation*}
1 \mathrm{LSB}=\frac{1}{2^{N}} \tag{15.4}
\end{equation*}
$$

The transfer curve for an ideal 2-bit D/A converter is shown in Fig. 15.2. Note here that, although only a finite number of analog values occur at the output, for an ideal D/A converter, the output signals are well-defined values. Also note that the maximum value of $\mathrm{V}_{\text {out }}$ is not $\mathrm{V}_{\text {ref }}$ but rather $\mathrm{V}_{\text {ref }}\left(1-2^{-\mathrm{N}}\right)$, or equivalently, $\mathrm{V}_{\text {ref }}-\mathrm{V}_{\text {LSB }}$. Finally, as we can see from (15.2), a multiplying D/A converter is realized by simply allowing the reference signal, $\mathrm{V}_{\text {ref }}$, to be a varying input signal along with the digital input, $\mathrm{B}_{\mathrm{in}}$. Such an arrangement results in

Key Point: Data converters translate between digital binary codes and analog voltages or currents. In an ideal converter, the binary codes correspond to analog signal quantities that are precisely equally spaced.
$V_{\text {out }}$ being proportional to the multiplication of the input signals, $B_{\text {in }}$ and $V_{\text {ref }}$.

#### EXAMPLE 15.1

An 8-bit $\mathrm{D} / \mathrm{A}$ converter has $\mathrm{V}_{\text {ret }}=5 \mathrm{~V}$. What is the output voltage when $\mathrm{B}_{\text {in }}=10110100$ ? Also, find $\mathrm{V}_{\text {LSB }}$.
image_name:Fig. 15.2 Input-output transfer curve for an ideal 2-bit D/A converter
description:The graph is a transfer curve for an ideal 2-bit Digital-to-Analog (D/A) converter. It is a staircase plot showing the relationship between the digital input and the analog output.

1. **Type of Graph and Function:**
- This is a transfer curve graph for a 2-bit D/A converter, which maps digital input codes to corresponding analog output values.

2. **Axes Labels and Units:**
- The vertical axis is labeled as \( \frac{V_{\text{out}}}{V_{\text{ref}}} \), representing the ratio of output voltage to the reference voltage.
- The horizontal axis represents the digital input codes, ranging from '00' to '11' in binary.

3. **Overall Behavior and Trends:**
- The graph shows a linear increase in output voltage with increasing digital input codes. Each step corresponds to a binary input increment.
- The curve is a staircase shape, indicating discrete levels of output voltage for each binary input.

4. **Key Features and Technical Details:**
- The graph has four steps corresponding to the binary inputs '00', '01', '10', and '11'.
- The output voltage increases in equal steps, with each step representing an increment of \( \frac{1}{4} \) of the reference voltage \( V_{\text{ref}} \).
- The dotted line extends beyond the last step, indicating the theoretical continuation of the linear relationship.
- The graph highlights that \( V_{\text{LSB}} = \frac{1}{4}V_{\text{ref}} \), which is the smallest voltage change corresponding to a one-bit change in the input.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for each binary input code ('00', '01', '10', '11') and the corresponding output levels.
- A specific note indicates that \( V_{\text{LSB}} = \frac{1}{4} \) of \( V_{\text{ref}} \), which equals 1 Least Significant Bit (LSB).

Fig. 15.2 Input-output transfer curve for an ideal 2-bit D/A converter.

#### Solution

We can find the decimal equivalent of $\mathrm{B}_{\text {in }}$ using (15.1)

$$
\begin{equation*}
\mathrm{B}_{\text {in }}=2^{-1}+2^{-3}+2^{-4}+2^{-6}=0.703125 \tag{15.5}
\end{equation*}
$$

Then, using (15.2), we find

$$
\begin{equation*}
\mathrm{V}_{\text {out }}=\mathrm{V}_{\text {ref }} \mathrm{B}_{\text {in }}=3.516 \mathrm{~V} \tag{15.6}
\end{equation*}
$$

and

$$
\begin{equation*}
V_{\text {LSB }}=5 / 256=19.5 \mathrm{mV} \tag{15.7}
\end{equation*}
$$

## 15.2 IDEAL A/D CONVERTER

image_name:Fig. 15.3 A block diagram representing an A/D converter
description:The block diagram in Fig. 15.3 represents an Analog-to-Digital (A/D) converter system. The main component of this system is a block labeled "A/D," which stands for the analog-to-digital converter. This block is responsible for converting an analog input voltage into a digital output word.

Main Components:
- **A/D Converter Block:** This is the central component that performs the conversion of analog signals to digital form.

Flow of Information or Control:
- **Analog Input (V_in):** The analog input voltage, denoted as \( V_{\text{in}} \), enters the A/D converter block from the left side. This represents the signal that needs to be digitized.
- **Reference Voltage (V_ref):** The reference voltage, \( V_{\text{ref}} \), is supplied to the A/D converter from below. This reference voltage is crucial for determining the scale and resolution of the conversion process.
- **Digital Output (B_out):** The output of the A/D converter is a digital word, denoted as \( B_{\text{out}} \), which exits the block on the right side. This represents the binary equivalent of the analog input signal.

Labels, Annotations, and Key Indicators:
- The diagram includes labels for \( V_{\text{in}} \), \( V_{\text{ref}} \), and \( B_{\text{out}} \) to indicate the input and output points as well as the reference signal.

Overall System Function:
The primary function of this A/D converter system is to transform an analog input signal into a corresponding digital output. The reference voltage \( V_{\text{ref}} \) is used to calibrate the conversion process, ensuring that the digital output accurately represents the analog input within the specified resolution and range. This conversion is essential for interfacing analog signals with digital systems, enabling further processing, storage, or transmission in digital form.

Fig. 15.3 A block diagram representing an A/D converter.
image_name:Fig. 15.4 Input-output transfer curve for a 2-bit A/D converter
description:The graph titled "Fig. 15.4 Input-output transfer curve for a 2-bit A/D converter" is a step function representing the relationship between the analog input voltage \( V_{\text{in}} \) and the digital output \( B_{\text{out}} \) for a 2-bit analog-to-digital converter.

Type of Graph and Function:
This is a step function graph, commonly used to illustrate the quantization process in A/D converters.

Axes Labels and Units:
- **Horizontal Axis (X-axis):** Represents the normalized analog input voltage \( V_{\text{in}}/V_{\text{ref}} \), ranging from 0 to 1.
- **Vertical Axis (Y-axis):** Represents the digital output \( B_{\text{out}} \), which can take on discrete values corresponding to the binary outputs 00, 01, 10, and 11.

Overall Behavior and Trends:
The graph shows a series of discrete steps, each corresponding to a range of input voltages that map to a specific digital output. The steps increase in value as the input voltage increases, reflecting the quantization levels of the 2-bit converter.

Key Features and Technical Details:
- The step size corresponds to 1 LSB (Least Significant Bit), which is defined as \( V_{\text{LSB}} = \frac{1}{4}V_{\text{ref}} \).
- The input voltage \( V_{\text{in}} \) is divided into four regions: 0 to \( \frac{1}{4}V_{\text{ref}} \), \( \frac{1}{4}V_{\text{ref}} \) to \( \frac{1}{2}V_{\text{ref}} \), \( \frac{1}{2}V_{\text{ref}} \) to \( \frac{3}{4}V_{\text{ref}} \), and \( \frac{3}{4}V_{\text{ref}} \) to \( V_{\text{ref}} \).
- The digital output \( B_{\text{out}} \) changes from 00 to 11 as the input voltage increases through these regions.

Annotations and Specific Data Points:
- The graph includes annotations for each transition point, indicating the input voltage at which the digital output changes.
- A dashed line indicates the ideal linear relationship between \( V_{\text{in}} \) and \( B_{\text{out}} \), highlighting the quantization error.

This graph effectively demonstrates the quantization process in a 2-bit A/D converter, showing how continuous input voltages are mapped to discrete digital outputs, with each step representing a quantization level defined by the converter's resolution.

Fig. 15.4 Input-output transfer curve for a 2-bit A/D converter.

The block diagram representation for an A/D converter is shown in Fig. 15.3, where $B_{\text {out }}$ is the digital output word while $\mathrm{V}_{\text {in }}$ and $\mathrm{V}_{\text {ref }}$ are the analog input and reference signals, respectively. Also, we define $V_{\text {LSB }}$ to be the signal change corresponding to a single LSB change as in the D/A case.

For an $\mathrm{A} / \mathrm{D}$ converter, the following equation relates these signals,

$$
\mathrm{V}_{\mathrm{ref}}\left(\mathrm{~b}_{1} 2^{-1}+\mathrm{b}_{2} 2^{-2}+\cdots+\mathrm{b}_{\mathrm{N}} 2^{-\mathrm{N}}\right)=\mathrm{V}_{\mathrm{in}} \pm \mathrm{V}_{\mathrm{x}}
$$

where

$$
\begin{equation*}
-\frac{1}{2} \mathrm{~V}_{\mathrm{LSB}} \leq \mathrm{V}_{\mathrm{x}}<\frac{1}{2} \mathrm{~V}_{\mathrm{LSB}} \tag{15.8}
\end{equation*}
$$

Note that there is now a range of valid input values that produce the same digital output word. This signal ambiguity produces what is known as quantization error. Also, note that no quantization error occurs in the case of a D/A converter since the output signals are well defined. ${ }^{1}$

As in the D/A case, a transfer curve for an A/D converter can be sketched as shown in Fig. 15.4 for a 2-bit converter. Note that the transitions along the $\mathrm{V}_{\text {in }}$ axis are offset by $1 / 2 \mathrm{~V}_{\mathrm{LSB}}$, so that the midpoints of the staircase curve fall precisely on the equivalent D/A transfer curve. Here, we define the transition voltages at $V_{i j}$, where the subscript $i j$ indicates the upper $B_{\text {out }}$ value of the transition. For example, $\mathrm{V}_{01}$ is shown in Fig. 15.4 as the voltage (normalized with respect to $\mathrm{V}_{\text {ref }}$ ) for the transition from 00 to 01 .

Finally, it should be noted that the relation shown in (15.8) holds only if the input signal remains within 1 LSB of the two last transition voltages. Specifically, for the 2-bit transfer curve

1. Of course, quantization errors will occur if a 6-bit D/A converter is used to convert a 10-bit digital signal, but in this case, the quantization error occurs in the conversion from a 10-bit digital signal to a 6-bit digital signal.
shown in Fig. 15.4, $\mathrm{V}_{\text {in }}$ should remain less than $7 / 8 \mathrm{~V}_{\text {ref }}$ and greater than $-1 / 8 \mathrm{~V}_{\text {ref }}$. Otherwise, the quantizer is said to be overloaded since the magnitude of the quantization error would be larger than $\mathrm{V}_{\mathrm{LSB}} / 2$.

## 15.3 QUANTIZATION NOISE

As mentioned in Section 15.2，quantization errors occur even in ideal A/D converters. In this section, we model these errors as being equivalent to an additive noise source and then find the power of this noise source. Consider the setup shown in Fig. 15.5, where both N -bit converters are ideal.

Since we have

$$
\begin{equation*}
V_{Q}=V_{1}-V_{i n} \tag{15.9}
\end{equation*}
$$

we can rearrange this equation as

$$
\begin{equation*}
V_{1}=V_{i n}+V_{Q} \tag{15.10}
\end{equation*}
$$

Although this rearrangement is trivial, it has important implications because (15.10) shows that the quantized signal, $\mathrm{V}_{\mathrm{l}}$, can be modelled as the input signal, $\mathrm{V}_{\mathrm{in}}$, plus some additive quantization noise signal, $\mathrm{V}_{\mathrm{Q}}$. Note that (15.10) is exact because no approximations have been made here. The quantization noise modelling becomes approximate once some assumptions are made about the statistical properties of $\mathrm{V}_{\mathrm{Q}}$.

### 15.3.1 Deterministic Approach

To gain an understanding of some of the properties of the quantization noise signal, $\mathrm{V}_{\mathrm{Q}}$, we will investigate its behavior when the input is a particular function. Specifically, let us assume the input signal, $\mathrm{V}_{\mathrm{in}}$, in Fig. 15.5 is a ramp. Such an input signal results in the output from the $\mathrm{D} / \mathrm{A}, \mathrm{V}_{1}$, appearing as a staircase, as shown in Fig. 15.6, assuming no overloading occurs. Taking the difference between these two signals gives us the noise signal, $\mathrm{V}_{\mathrm{Q}}$, which is a

Key Point: As long as it is not overloaded, the ideal quantizer introduces an additive quantization noise less than 1/2 of an LSB in magnitude.
image_name:Fig. 15.5
description:The system block diagram in Fig. 15.5 illustrates a circuit designed to investigate quantization noise behavior. The main components of the system are as follows:

1. **A/D Converter (Analog to Digital Converter):** This block receives the input signal $V_{in}$, which is a ramp signal. The A/D converter digitizes the analog input signal, producing a digital output signal labeled as 'B'.

2. **D/A Converter (Digital to Analog Converter):** The digital signal 'B' from the A/D converter is fed into the D/A converter. This block converts the digital signal back into an analog signal, producing an output $V_1$.

3. **Summing Junction:** The system includes a summing junction where the analog output $V_1$ from the D/A converter is subtracted from the original input signal $V_{in}$. The result of this subtraction is the quantization noise signal $V_Q$.

**Flow of Information:**
- The input signal $V_{in}$ enters the A/D converter, where it is digitized.
- The digital output 'B' is then sent to the D/A converter, which converts it back to an analog signal $V_1$.
- The signal $V_1$ is fed into a summing junction, where it is subtracted from the original input $V_{in}$ to produce the quantization noise $V_Q$.

**Overall System Function:**
- The primary function of this system is to demonstrate the behavior of quantization noise. By comparing the original input signal with the reconstructed output from the D/A converter, the system isolates the quantization error as the output $V_Q$. This error is limited to within ±1/2 of the least significant bit (LSB) of the quantizer, assuming no overloading occurs. The system effectively illustrates how quantization introduces noise into a signal processing chain.

Quantization noise

Fig. 15.5 A circuit to investigate quantization noise behavior.
image_name:Fig. 15.5
description:The diagram labeled "Fig. 15.5" consists of two separate graphs illustrating the behavior of quantization noise in a signal processing circuit.

Left Graph:
1. **Type of Graph and Function:**
- This is a time-domain waveform showing the input and output signals of a digital-to-analog converter (DAC).

2. **Axes Labels and Units:**
- The horizontal axis represents time, labeled as "t (Time)".
- The vertical axis represents voltage, with no specific units given.
- Two signals are shown: $V_{in}$ (dotted line) and $V_1$ (solid stepped line).

3. **Overall Behavior and Trends:**
- The graph shows a ramp input signal $V_{in}$, which is a continuous increasing linear function over time.
- The output signal $V_1$ is a stepped approximation of the input, indicating quantization.
- The steps in $V_1$ reflect the discrete levels of the quantizer, showing how the continuous input is approximated.

4. **Key Features and Technical Details:**
- The steps in $V_1$ illustrate the quantization process, where each step represents a discrete level of the quantizer.
- There is a noticeable delay between the input $V_{in}$ and the quantized output $V_1$.

Right Graph:
1. **Type of Graph and Function:**
- This is another time-domain waveform focusing on the quantization error signal $V_Q$.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as "t (Time)".
- The vertical axis represents voltage, labeled as $V_Q$.
- The voltage scale is marked with $\frac{1}{2} V_{LSB}$ and $-\frac{1}{2} V_{LSB}$, indicating the limits of the quantization noise.

3. **Overall Behavior and Trends:**
- The graph shows an oscillating waveform of $V_Q$, demonstrating the quantization noise.
- The waveform oscillates between $\frac{1}{2} V_{LSB}$ and $-\frac{1}{2} V_{LSB}$, indicating the bounded nature of the quantization error.

4. **Key Features and Technical Details:**
- The oscillation period is marked as $T$, showing the periodic nature of the quantization error.
- The average of $V_Q$ over time is zero, as indicated by its symmetrical oscillation around the horizontal axis.

5. **Annotations and Specific Data Points:**
- The graph emphasizes the limits of the quantization noise, constrained between $\frac{1}{2} V_{LSB}$ and $-\frac{1}{2} V_{LSB}$.
image_name:Fig. 15.6
description:The graph in Fig. 15.6 consists of two parts, each illustrating different aspects of quantization noise behavior when a ramp signal is applied to the circuit.

**Left Graph:**
1. **Type of Graph and Function:**
- This is a time-domain waveform graph showing the input and quantized output signals.
2. **Axes Labels and Units:**
- The x-axis represents time, labeled as 't (Time)'.
- The y-axis represents voltage, with the input voltage $V_{in}$ and the quantized output $V_1$.
3. **Overall Behavior and Trends:**
- The input signal $V_{in}$ is a smooth, continuous ramp signal depicted with a dashed line.
- The quantized output $V_1$ is a staircase waveform, indicating discrete steps that approximate the continuous input ramp.
- The steps occur at regular intervals, corresponding to the quantization levels.
4. **Key Features and Technical Details:**
- The quantized output exhibits a stepwise increase as time progresses, reflecting the quantization process.
- Each step corresponds to a change of one least significant bit (LSB) in the digital representation.
5. **Annotations and Specific Data Points:**
- The graph does not provide specific numerical values for the voltage levels or time intervals.

**Right Graph:**
1. **Type of Graph and Function:**
- This is also a time-domain waveform graph showing the quantization error signal $V_Q$.
2. **Axes Labels and Units:**
- The x-axis represents time, labeled as 't (Time)'.
- The y-axis represents voltage, specifically the quantization error $V_Q$.
3. **Overall Behavior and Trends:**
- The error signal $V_Q$ oscillates between $+1/2 V_{LSB}$ and $-1/2 V_{LSB}$, forming a triangular waveform.
- The waveform is periodic with a constant period $T$.
4. **Key Features and Technical Details:**
- The amplitude of the error signal is limited to $
± 1/2 V_{LSB}$, indicating the bounds of quantization noise.
- The average value of the quantization error is zero, as the waveform is symmetric about the time axis.
5. **Annotations and Specific Data Points:**
- The period $T$ of the waveform is marked on the graph, but no specific numerical values are provided for $T$ or $V_{LSB}$.

Overall, these graphs illustrate how quantization introduces discrete steps in the output signal and generates a bounded error signal that oscillates around zero, demonstrating the inherent noise in the quantization process.

Fig. 15.6 Applying a ramp signal to the circuit in Fig. 15.5.
result of quantization error. Note that the quantization signal, $\mathrm{V}_{\mathrm{Q}}$, is limited to $\pm \mathrm{V}_{\mathrm{LSB}} / 2$ and will be so limited for all input signals (not just ramps). Clearly, the average of $\mathrm{V}_{\mathrm{Q}}$ is zero. However, the rms value of the noise signal, $\mathrm{V}_{\mathrm{Q}(\mathrm{rms})}$, is given by

$$
\begin{align*}
& V_{Q(r m s)}= {\left[\frac{1}{T} \int_{-T / 2}^{T / 2} V_{Q}^{2} d t\right]^{1 / 2}=\left[\frac{1}{T} \int_{-T / 2}^{T / 2} V_{\mathrm{LsB}}^{2}\left(\frac{-t}{T}\right)^{2} \mathrm{dt}\right]^{1 / 2} } \\
&=\left[\frac{\mathrm{V}_{\mathrm{LSB}}^{2}}{\mathrm{~T}^{3}}\left(\left.\frac{\mathrm{t}^{3}}{3}\right|_{-\mathrm{T} / 2} ^{\mathrm{T} / 2}\right]^{1 / 2}\right.  \tag{15.11}\\
& \mathrm{V}_{\mathrm{Q}(\mathrm{rss})}=\frac{\mathrm{V}_{\mathrm{LSB}}}{\sqrt{12}} \tag{15.12}
\end{align*}
$$

Thus, we see that the rms power of the quantization noise source is proportional to the size of $\mathrm{V}_{\mathrm{LSB}}$, which is determined by the number of bits, N , in the converter.

### 15.3.2 Stochastic Approach

The preceding deterministic approach was presented as a simple example to see some properties of the quantization noise signal. However, to deal with the more general input case, a stochastic approach is typically used. In a stochastic approach, we assume that the input signal is varying rapidly such that the quantization error signal, $\mathrm{V}_{\mathrm{Q}}$, is a random variable uniformly distributed between $\pm \mathrm{V}_{\mathrm{LSB}} / 2$. The probability density function for such an error signal, $\mathrm{f}_{\mathrm{Q}}(\mathrm{x})$, will be a constant value, as shown in Fig. 15.7.

The average value of the quantization error, $\mathrm{V}_{\mathrm{Q}(\mathrm{avg})}$, is found to be zero as follows:

$$
\begin{equation*}
V_{Q(a v g)}=\int_{-\infty}^{\infty} x f_{Q}(x) d x=\frac{1}{V_{\mathrm{LSB}}}\left(\int_{-V_{\mathrm{LSB}} / 2}^{V_{\mathrm{LSB} / 2}} x d x\right)=0 \tag{15.13}
\end{equation*}
$$

In a similar fashion, the rms value of the quantization error is given by

$$
\begin{equation*}
V_{Q(\mathrm{~ms})}=\left[\int_{-\infty}^{\infty} x^{2} f_{e}(x) d x\right]^{1 / 2}=\left[\frac{1}{V_{\mathrm{LSB}}}\left(\int_{-\mathrm{V}_{\mathrm{LSB}} / 2}^{\mathrm{V}_{\mathrm{LSB} / 2}} x^{2} d x\right)\right]^{1 / 2}=\frac{\mathrm{V}_{\mathrm{LSB}}}{\sqrt{12}} \tag{15.14}
\end{equation*}
$$

which is the same result as (15.12), which is found using the deterministic ramp input signal. The fact that these two results are identical should come as no surprise since randomly chosen samples from the sawtooth waveform in the deterministic case would also have a uniformly distributed probability density function. In general, the rms quantization noise power equals $\mathrm{V}_{\mathrm{LSB}} / \sqrt{12}$ when the quantization noise signal is uniformly distributed over the interval $\pm \mathrm{V}_{\mathrm{LSB}} / 2$.
image_name:Fig. 15.7 Assumed probability density function for the quantization error
description:The graph in Fig. 15.7 represents the assumed probability density function (PDF) for the quantization error, denoted as \( f_Q(x) \). This is a type of probability distribution graph.

1. **Type of Graph and Function:**
- The graph is a probability density function (PDF) for quantization error.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( x \) and represents the quantization error. The units are not specified but are typically in volts when dealing with voltage levels like \( V_{LSB} \).
- The vertical axis represents the probability density \( f_Q(x) \).

3. **Overall Behavior and Trends:**
- The graph shows a uniform distribution over the interval \( \left[-\frac{V_{LSB}}{2}, \frac{V_{LSB}}{2}\right] \), indicating that the quantization error is equally likely to be any value within this range.

4. **Key Features and Technical Details:**
- The height of the PDF is \( \frac{1}{V_{LSB}} \), ensuring that the total area under the curve equals 1, which is a requirement for all probability density functions.
- The distribution is centered around zero, reflecting the assumption that the quantization error is unbiased.

5. **Annotations and Specific Data Points:**
- The edges of the distribution are marked at \( -\frac{V_{LSB}}{2} \) and \( \frac{V_{LSB}}{2} \).
- An annotation indicates that the integral of the PDF over the entire range equals 1, confirming it is a valid probability density function.

Fig. 15.7 Assumed probability density function for the quantization error, $\mathrm{V}_{\mathrm{Q}}$.

Recalling that the size of $\mathrm{V}_{\text {LSB }}$ is halved for each additional bit and assuming that $\mathrm{V}_{\text {ret }}$ remains constant, we see from (15.14) that the noise power decreases by 6 dB for each additional bit in the $\mathrm{A} / \mathrm{D}$ converter. Thus, given an input signal waveform, a formula can be derived giving the best possible signal-to-noise ratio (SNR) for a given number of bits in an ideal A/D converter.

For example, assuming $\mathrm{V}_{\text {in }}$ is a sawtooth of height $\mathrm{V}_{\text {ref }}$ (or equivalently, a random signal uniformly distributed between 0 and $\mathrm{V}_{\text {ref }}$ ) and considering only the ac power of the signal, the signal-to-quantization noise ratio (SQNR) is given by

$$
\begin{align*}
\text { SQNR } & =20 \log \left(\frac{V_{\text {in(rms }}}{\mathrm{V}_{\mathrm{Q}(\mathrm{rms})}}\right)=20 \log \left(\frac{\mathrm{~V}_{\text {ref }} / \sqrt{12}}{\mathrm{~V}_{\mathrm{LSB}} / \sqrt{12}}\right)  \tag{15.15}\\
& =20 \log \left(2^{\mathrm{N}}\right)=6.02 \mathrm{NdB}
\end{align*}
$$

This represents the best possible SNR achievable for a data converter with N-bits of resolution since only the quantization noise of an ideal converter is considered. For example, a 10-bit A/D converter has a best possible SNR of about 60 dB .

Alternatively, a more common SNR formula is to assume $\mathrm{V}_{\text {in }}$ is a sinusoidal waveform between 0 and $\mathrm{V}_{\text {ref }}$. Thus, the ac power of the sinusoidal wave is $\mathrm{V}_{\mathrm{ref}} /(2 \sqrt{2})$, which results in

$$
\begin{align*}
\text { SQNR } & =20 \log \left(\frac{\mathrm{~V}_{\mathrm{in}(\mathrm{rms})}}{\left.\mathrm{V}_{\mathrm{Q}(\mathrm{rms}}\right)}\right. \\
& =20 \log \left(\frac{\mathrm{~V}_{\mathrm{ref}} /(2 \sqrt{2})}{\mathrm{V}_{\mathrm{LSB}} /(\sqrt{12})}\right)  \tag{15.16}\\
& =20 \log \left(\sqrt{\frac{3}{2}} 2^{\mathrm{N}}\right) \\
\text { SQNR } & =6.02 \mathrm{~N}+1.76 \mathrm{~dB}
\end{align*}
$$

In other words, a sinusoidal signal has 1.76 dB more ac power than a random signal uniformly distributed between the same peak levels.

Note that (15.16) gives the best possible SNR for an N-bit A/D converter. However, the idealized SNR decreases from this best possible value for reduced input signal levels. For example, Fig. 15.8 shows a plot of the idealized SNR for a 10-bit A/D converter versus the sinusoidal input signal amplitude. However, it should be noted that these SNR values could be improved through the use of oversampling techniques if the input signal's bandwidth is lower than the Nyquist rate. Oversampling will be discussed in

Key Point: Quantization noise may be modeled as a random quantity uniformly distributed between -LSB/2 and $+L S B / 2$. For a sinusoidal input, this results in a maximum SNR of $6.02 N+1.76 d B$ for an ideal $N$-bit converter.
detail in Chapter 18, where the design of oversampling converters is presented.

#### EXAMPLE 15.2

A $200-\mathrm{mV}_{\mathrm{pp}}$ sinusoidal signal is applied to an ideal 12-bit $\mathrm{A} / \mathrm{D}$ converter for which $\mathrm{V}_{\mathrm{ref}}=5 \mathrm{~V}$. Find the SNR of the digitized output signal.
image_name:Fig. 15.8
description:The graph depicted is a plot of Signal-to-Noise Ratio (SNR) in decibels (dB) versus the input signal amplitude in decibels relative to full scale (dBFS) for a 10-bit analog-to-digital (A/D) converter. The x-axis represents the input voltage \( V_{in} \) in dBFS, ranging from -60 to 0 dBFS, and the y-axis represents the SNR in dB, ranging from 0 to 60 dB.

The graph exhibits a linear relationship, where the SNR increases as the input signal amplitude increases. The line starts at the origin, indicating that at very low input levels, the SNR is also low. As the input amplitude approaches 0 dBFS (which corresponds to the full-scale input where \( V_{pp} = V_{ref} \)), the SNR reaches its maximum value.

The line is annotated with the label 'Best possible SNR' at the top right, indicating the maximum achievable SNR for this converter when the input signal is at full scale. This point corresponds to the highest SNR value on the graph, near 60 dB.

This graph illustrates the ideal performance of the converter, showing that the best SNR is achieved when the input signal utilizes the full dynamic range of the converter, aligning with the theoretical maximum SNR for a 10-bit converter.

Fig. 15.8 Idealized SNR versus sinusoidal input signal a mplitude for a 10-bit A/D converter. The 0 -dBFS input signal amplitude corresponds to a peak-to-peak voltage equaling "Full-Scale," in this case $V_{\text {ref }}$.

#### Solution

First, we use (15.16) to find the maximum SNR if a full-scale sinusoidal waveform of $\pm 2.5 \mathrm{~V}$ were applied to the input.

$$
\begin{equation*}
\mathrm{SNR}_{\text {max }}=6.02 \times 12+1.76=74 \mathrm{~dB} \tag{15.17}
\end{equation*}
$$

However, since the input is only a $\pm 100-\mathrm{mV}$ sinusoidal waveform that is 28 dB below full scale, the SNR of the digitized output is

$$
\begin{equation*}
\mathrm{SNR}=74-28=46 \mathrm{~dB} \tag{15.18}
\end{equation*}
$$

## 15.4 SIGNED CODES

In many applications, it is necessary to create a converter that operates with both positive and negative analog signals, resulting in the need for both positive and negative digital representations. Typically, the analog signal is bounded by $\pm 0.5 \mathrm{~V}_{\text {ref }}$, such that its full-scale range is the same magnitude as in the unipolar case. Some common signed digital representations are sign magnitude, 1's complement, offset binary, and 2's complement, as shown in Table 15.1 for the 4-bit case. Note from Table 15.1 that all positive number representations are the same except for the offset-binary case, where the MSB is complemented.

Sign Magnitude

For negative numbers in the sign-magnitude case, all the bits are the same as for the positive number representation, except that the MSB is complemented. For example, the sign-magnitude representation for 5 is 0101 , whereas for -5 it is 1101 . However, note that this approach results in two representations for the number 0 , and thus only $2^{N}-1$ numbers are represented.

Table 15.1 Some 4-bit signed digital representations.

| Number | Normalized <br> number | Sign <br> magnitude | 1's <br> complement | Offset <br> binary | $\mathbf{2} \mathbf{s}$ <br> complement |
| :---: | :---: | :---: | :---: | :---: | :---: |
| +7 | $+7 / 8$ | 0111 | 0111 | 1111 | 0111 |
| +6 | $+6 / 8$ | 0110 | 0110 | 1110 | 0110 |
| +5 | $+5 / 8$ | 0101 | 0101 | 1101 | 0101 |
| +4 | $+4 / 8$ | 0100 | 0100 | 1100 | 0100 |
| +3 | $+3 / 8$ | 0011 | 0011 | 1011 | 0011 |
| +2 | $+2 / 8$ | 0010 | 0010 | 1010 | 0010 |
| +1 | $+1 / 8$ | 0001 | 0001 | 1001 | 0001 |
| +0 | +0 | 0000 | 0000 | 1000 | 0000 |
| $(-0)$ | $(-0)$ | $(1000)$ | $(11111)$ |  |  |
| -1 | $-1 / 8$ | 1001 | 1110 | 0111 | 1111 |
| -2 | $-2 / 8$ | 1010 | 1101 | 0110 | 1110 |
| -3 | $-3 / 8$ | 1011 | 1100 | 0101 | 1101 |
| -4 | $-4 / 8$ | 1100 | 1011 | 0100 | 1100 |
| -5 | $-5 / 8$ | 1101 | 1010 | 0011 | 1011 |
| -6 | $-6 / 8$ | 1110 | 1001 | 0010 | 1010 |
| -7 | $-7 / 8$ | 1111 | 1000 | 0001 | 1001 |
| -8 | $-8 / 8$ |  |  | 0000 | 1000 |

I's Complement

In 1's-complement representation, negative numbers are represented as the complement of all the bits for the equivalent positive number. For example, here, 5 is once again 0101 , whereas -5 is now 1010 . It should be noted that the 1 's-complement case also has two representations for 0 , and thus only $2^{\mathrm{N}}-1$ numbers are represented.

Offset Binary

The offset-binary representation is obtained by assigning 0000 to the most negative number and then counting up, as in the unipolar case. In other words, this system can be thought of as simply a unipolar representation counting from 0 to $2^{\mathrm{N}}$, but where the decimal numbers represented are offset by $2^{\mathrm{N}-1}$, or equivalently, the decimal counts are from $-2^{\mathrm{N}-1}$ to $2^{\mathrm{N}-1}$. For example, the offset-binary code for the number 5 in the 4 -bit case is the same as the unipolar code for the number 13 , which is 1101 , since $13=5+2^{4-1}$. The offset-binary code for -5 is the same as the unipolar code for 3 , which is 0011 . Note that the offset-binary code does not suffer from redundancy, and all sixteen numbers are uniquely represented. Also, this code has the advantage that it is closely related to the unipolar case through a simple offset.

Finally, the unipolar relationship for a D/A converter given in (15.2) is easily modified to the signed case, with offset-binary representation as

$$
\begin{equation*}
\mathrm{V}_{\text {out }}=\mathrm{V}_{\text {ref }}\left(\mathrm{b}_{1} 2^{-1}+\mathrm{b}_{2} 2^{-2}+\cdots+\mathrm{b}_{\mathrm{N}} 2^{-\mathrm{N}}\right)-0.5 \mathrm{~V}_{\text {ref }} \tag{15.19}
\end{equation*}
$$

Note here that the output signal is now bounded by $\pm 0.5 \mathrm{~V}_{\text {ref }}$.

2's Complement

Finally, the 2 's-complement representation is obtained from the offset-binary number by simply complementing the MSB. For the 4-bit example, 5 becomes 0101 in 2's complement (the same as in sign magnitude and in 1's complement), whereas -5 is now 1011 . It should be mentioned that the 2 's-complement code for negative numbers can also be obtained by adding 1 LSB to the equivalent 1's-complement code.

The main advantage of 2 's-complement coding is that addition of both positive and negative numbers is performed using straightforward addition, and no extra hardware is required. Also, the subtraction of two numbers, $A-B$, can be easily performed by complementing all the bits for $B$ (i.e., forming the 1 's-complement equivalent) and then adding this result to A at the same time as adding a single LSB in order to create the 2 'scomplement equivalent of -B. Adding a single LSB is easily accomplished in hardware by setting the carry-in bit high in the overall adder. Thus, subtraction requires only a small amount of extra hardware. Finally, if many numbers are being added using 2's-complement codes, no overflow hardware is required as long as the final result is within the digital code range (even if intermediate results go well out of range). For these reasons, 2'scomplement codes are the most popular representation for signed numbers when arithmetic operations are to be performed.

### EXAMPLE 15.3

Show that, when adding $2 / 8,7 / 8$, and $-3 / 8$ together as 2 's-complement numbers, the final result is correct although an intermediate result is incorrect.

### Solution

The addition of $2 / 8$ and $7 / 8$ is given by

$$
\begin{equation*}
0010+0111=1001 \tag{15.20}
\end{equation*}
$$

which corresponds to $-7 / 8$ (note that this temporary result is two steps past $7 / 8$ when thinking of a 2 'scomplement code as being circular). Although this intermediate result is incorrect since overflow occurred, we simply carry on and add $-3 / 8$ to find the final answer.

$$
\begin{equation*}
1001+1101=0110 \tag{15.21}
\end{equation*}
$$

Thus, the final result of $6 / 8$ is correct, although a temporary overflow occurred, as we just saw.

## 15.5 PERFORMANCE LIMITATIONS

In this section, some commonly used terms describing the performance of data converters are defined. Before proceeding, definitions are required for determining the transfer responses of both $D / A$ and $A / D$ converters. The transfer response of a D/A converter is defined to be the analog levels that occur for each of the digital input words. Similarly, the transfer response of an A/D converter can be defined as the mid-points of the quantization intervals for each of the digital output words. However, since transitions are easier to measure than midpoint values, $\mathrm{A} / \mathrm{D}$ converter errors are often measured in terms of the analog transition point values, $\mathrm{V}_{\mathrm{i}}$, and we use that approach here.

### 15.5.1 Resolution

The resolution of a converter is defined to be the number of distinct analog levels corresponding to the different digital words. Thus, an N -bit resolution implies that the converter can resolve $2^{\mathrm{N}}$ distinct analog levels. Resolution is not necessarily an indication of the accuracy of the converter, but instead it usually refers to the number of digital input or output bits.

### 15.5.2 Offset and Gain Error

In a $\mathrm{D} / \mathrm{A}$ converter, the offset error, $\mathrm{E}_{\mathrm{off}}$, is defined to be the output that occurs for the input code that should produce zero output, or mathematically,

$$
\begin{equation*}
\mathrm{E}_{\text {off }(\mathrm{D} / \mathrm{A})}=\left.\frac{\mathrm{V}_{\text {out }}}{\mathrm{V}_{\mathrm{LSB}}}\right|_{0 \ldots 0} \tag{15.22}
\end{equation*}
$$

where the offset error is in units of LSBs. Similarly, for an A/D converter, the offset error is defined as the deviation of $\mathrm{V}_{0 \ldots 01}$ from 1/2 LSB, or mathematically,

$$
\begin{equation*}
\mathrm{E}_{\mathrm{off}(\mathrm{~A} / \mathrm{D})}=\frac{\mathrm{V}_{0 \ldots 01}}{\mathrm{~V}_{\mathrm{LSB}}}-\frac{1}{2} \mathrm{LSB} \tag{15.23}
\end{equation*}
$$

The gain error is defined to be the difference at the full-scale value between the ideal and actual curves when the offset error has been reduced to zero. For a $\mathrm{D} / \mathrm{A}$ converter, the gain error, $\mathrm{E}_{\text {gain }(\mathrm{D} / \mathrm{A})}$, in units of LSBs, is given by

$$
\begin{equation*}
\mathrm{E}_{\text {gain }(\mathrm{D} / \mathrm{A})}=\left(\left.\frac{\mathrm{V}_{\text {out }}}{\mathrm{V}_{\mathrm{LSB}}}\right|_{1 \ldots 1}-\left.\frac{\mathrm{V}_{\text {out }}}{\mathrm{V}_{\mathrm{LSB}}}\right|_{0 \ldots 0}\right)-\left(2^{\mathrm{N}}-1\right) \tag{15.24}
\end{equation*}
$$

For an $A / D$ converter, the equivalent gain error, $\mathrm{E}_{\text {gain }(\mathrm{A} / \mathrm{D})}$ (in units of LSBs), is given by

$$
\begin{equation*}
E_{g a i n(A / D)}=\left(\frac{V_{1 \ldots 1}}{V_{\text {LSB }}}-\frac{V_{0 \ldots 01}}{V_{\text {LSB }}}\right)-\left(2^{N}-2\right) \tag{15.25}
\end{equation*}
$$

Graphical illustrations of gain and offset errors are shown in Fig. 15.9.

### 15.5.3 Accuracy and Linearity

The absolute accuracy of a converter is defined to be the difference between the expected and actual transfer responses. The absolute accuracy includes the offset, gain, and linearity errors.

The term relative accuracy is sometimes used and is defined to be the accuracy after the offset and gain errors have been removed. It is also referred to as the maximum integral nonlinearity error (described shortly) and we will refer to it as such.

Accuracy can be expressed as a percentage error of full-scale value, as the effective number of bits, or as a
image_name:Fig. 15.9
description:The graph in Fig. 15.9 is a linear plot illustrating the offset and gain errors in a 2-bit Digital-to-Analog Converter (DAC).

1. **Type of Graph and Function:**
- This is a linear plot showing the relationship between the binary input \( B_{in} \) and the output voltage \( V_{out} \) normalized to the reference voltage \( V_{ref} \).

2. **Axes Labels and Units:**
- The horizontal axis represents the binary input \( B_{in} \) with possible values of 00, 01, 10, and 11 (or 100 in parentheses to indicate full scale for a 2-bit DAC).
- The vertical axis represents the normalized output voltage \( \frac{V_{out}}{V_{ref}} \), with markings at intervals of 0, 1/4, 1/2, 3/4, and 1.

3. **Overall Behavior and Trends:**
- The ideal transfer function is represented by a dashed line, which is a straight line passing through the origin and indicates a perfect linear relationship without errors.
- The solid line represents the actual transfer function, which deviates from the ideal line due to offset and gain errors.

4. **Key Features and Technical Details:**
- **Offset Error:** This is shown as a vertical shift at the origin, indicating that the actual output does not start from zero when the input is zero.
- **Gain Error:** This is depicted as the difference in slope between the ideal and actual lines, indicating that the actual output does not increase as quickly as it should in response to increasing input.

5. **Annotations and Specific Data Points:**
- The graph highlights the offset error with a vertical arrow at the origin.
- The gain error is indicated by the divergence between the ideal and actual lines as the input increases.

This graph effectively demonstrates how both offset and gain errors can impact the linearity and accuracy of a DAC's output, illustrating the importance of these parameters in precision applications.

Fig. 15.9 Illustrating offset and gain err ors for a 2-bit D/A converter.
fraction of an LSB. For example, a 12-bit accuracy implies that the converter's error is less than the full-scale value divided by $2^{12}$.

Note that a converter may have 12-bit resolution with only 10-bit accuracy, or 10-bit resolution with 12-bit accuracy. An accuracy greater than the resolution means that the converter's transfer response is very precisely controlled (better than the number of bits of resolution).

Key Point: Integral nonlinearity (INL) is a popular measure of accuracy that specifies the deviation of a converter's inputoutput relationship away from the ideal, or least-squares fit, linear relationship.

Integral Nonlinearity (INL) Error After both the offset and gain errors have been removed, the integral nonlinearity (INL) error is defined to be the deviation from a straight line. However, what straight line should be used? A conservative measure of nonlinearity is to use the endpoints of the converter's transfer response to define the straight line. An alternative definition is to find the best-fit straight line such that the maximum difference (or perhaps the mean squared error) is minimized. These two definitions are illustrated in Fig. 15.10. One should be aware that, in this book, we define INL values for each digital word (and thus these values can be plotted for a single converter), whereas others sometimes define the term "INL" as the maximum magnitude of the INL values (or equivalently, as the relative accuracy). Typically INL is measured by slowly sweeping the converter input over its full-scale range; hence it is a measure of the converter's accuracy only at low input signal frequencies.

Key Point: Both DNL and INL are measured at dc or very low input frequencies. They are therefore referred to as measures of static nonlinearity.

Differential Nonlinearity (DNL) Error In an ideal converter, each analog step size is equal to 1 LSB. In other words, in a D/A converter, each output level is 1 LSB from adjacent levels, whereas in an A/D, the transition values are precisely 1 LSB apart. Differential nonlinearity (DNL) is defined as the variation in analog step sizes away from 1 LSB (typically, once gain and offset errors have been removed). Thus, an ideal converter has its maximum differential nonlinearity of 0 for all digital values, whereas a converter
with a maximum differential nonlinearity of 0.5 LSB has its step sizes varying from 0.5 LSB to 1.5 LSB. Once again, as in the INL case, we define DNL values for each digital word, whereas others sometimes refer to DNL as the maximum magnitude of the DNL values. Like INL, DNL is a measure of dc or low-frequency accuracy. Hence, both are referred to as measures of static nonlinearities.

Monotonicity A monotonic D/A converter is one in which the output always increases as the input increases. In other words, the slope of the D/A converter's transfer response is of only one sign. If the maximum DNL error is less than 1 LSB , then a $\mathrm{D} / \mathrm{A}$ converter is guaranteed to be monotonic. However, many monotonic converters may have a maximum DNL greater than 1 LSB . Similarly, a converter is guaranteed to be monotonic if the maximum INL is less than 0.5 LSB.

Missing Codes Although monotonicity is appropriate for $\mathrm{D} / \mathrm{A}$ converters, the equivalent term for $\mathrm{A} / \mathrm{D}$ converters is missing codes. An A/D converter is guaranteed not to have any missing codes if the maximum DNL error is less than 1 LSB or if the maximum INL error is less than 0.5 LSB.
image_name:Fig. 15.10 Integral nonlinearity error in a 2-bit D/A converter
description:The graph depicted is a plot showing the integral nonlinearity (INL) error in a 2-bit digital-to-analog (D/A) converter. It is a linear graph with both axes labeled. The x-axis represents the binary input \( B_{in} \), with values ranging from 00 to 11, indicating the 2-bit binary input levels. The y-axis represents the output voltage \( V_{out} \) normalized to the reference voltage \( V_{ref} \), with fractional values ranging from 0 to 1.

The plot features a bold, curved line illustrating the actual output of the D/A converter. Dashed lines represent the ideal linear output and the best-fit linear approximation. The integral nonlinearity error is indicated by arrows showing the deviation of the actual output from the ideal linear output at specific points.

The graph specifically highlights two types of INL errors: the endpoint error and the best-fit error. The endpoint error is shown by an arrow pointing vertically between the actual output and the ideal linear endpoint line, while the best-fit error is shown by another arrow indicating the deviation from the best-fit line.

Overall, the graph demonstrates how the actual output voltage deviates from the expected linear response in a 2-bit D/A converter, illustrating the concept of integral nonlinearity error, which is critical for understanding the accuracy and performance of the converter.

Fig. 15.10 Integral nonlinearity error in a 2-bit D/A converter.

A/D Conversion Time and Sampling Rate In an A/D converter, the conversion time is the time taken for the converter to complete a single measurement including acquisition time of the input signal. On the other hand, the maximum sampling rate is the speed at which samples can be continuously converted and is typically the inverse of the conversion time. However, one should be aware that some converters have a large latency between the input and the output due to pipelining or multiplexing, yet they still maintain a high sampling rate. For example, a pipelined 12-bit A/D converter may have a conversion time of 2 ns (i.e., a sampling rate of 500 MHz ) yet a latency from input to output of 24 ns .

D/A Settling Time and Sampling Rate In a D/A converter, the settling time is defined as the time it takes for the converter to settle to within some specified amount of the final value (usually 0.5 LSB ). The sampling rate is the rate at which samples can be continuously converted and is typically the inverse of the settling time.

Sampling-Time Uncertainty Both A/D and D/A converters have limited accuracy when their sampling instances are ill defined. To quantify this sampling time uncertainty, also known as aperture jitter, for sinusoidal waveforms, consider a full-scale signal, $V_{i n}$, applied to an $N$-bit, signed, $A / D$ converter with frequency $f_{i n}$. Mathematically,

$$
\begin{equation*}
V_{\text {in }}=\frac{V_{\text {ref }}}{2} \sin \left(2 \pi f_{i n} t\right) \tag{15.26}
\end{equation*}
$$

Since the rate of change (or slope) of $\mathrm{V}_{\text {in }}$ at the peak of a sinusoidal waveform is small, sampling time uncertainty is less of a problem near the peak values. However, the maximum rate of change for this waveform occurs at the zero crossing and can be found by differentiating $V_{\text {in }}$ with respect to time and setting $t=0$. At the zero crossing, we find that

$$
\begin{equation*}
\left.\frac{\Delta \mathrm{V}}{\Delta \mathrm{t}}\right|_{\max }=\pi \mathrm{f}_{\mathrm{in}} \mathrm{~V}_{\mathrm{ref}} \tag{15.27}
\end{equation*}
$$

If $\Delta \mathrm{t}$ represents some sampling-time uncertainty, and if we want to keep $\Delta \mathrm{V}$ less than $1 \mathrm{~V}_{\mathrm{LSB}}$, we see that

$$
\begin{equation*}
\Delta t<\frac{V_{\text {LSB }}}{\pi f_{i n} V_{\text {ref }}}=\frac{1}{2^{N} \pi f_{i n}} \tag{15.28}
\end{equation*}
$$

For example, an 8 -bit converter sampling a full-scale $250-\mathrm{MHz}$ sinusoidal signal must keep its sampling-time uncertainty under 5 ps to maintain 8 -bit accuracy. Also, the same 5-ps time accuracy is required for a 16-bit converter operating on a full-scale, $1-\mathrm{MHz}$ signal.

Key Point: Uncertainty in the sampling times of a converter, called aperture jitter, can be a significant performance limitation at high input signal frequencies.

Dynamic Range In general terms, the dynamic range of a converter is the ratio of the maximum to minimum signal amplitudes that it can meaningfully process. A popular metric quantifying dynamic range is the maximum achievable signal-to-noise and distortion ratio (SNDR) specified as the ratio of the rms value of an input sinusoidal signal to the rms output noise plus the distortion measured when that same sinusoid is present at the output. In order to obtain the rms output noise plus distortion, the sinusoidal signal must first be eliminated from the measured output. In a D/A converter, the output sinusoid can be eliminated by using a spectrum analyzer and ignoring the power at that particular frequency. For an A/D converter, a similar approach can be taken by using an FFT and eliminating the fundamental of the output, or a least-mean-squared fit can be used to find the amplitude and phase of a sinusoid at the input signal's frequency and then subtracting the best-fit sinusoid from the output signal. Dynamic range can also be expressed as an effective number of bits $\left(N_{\text {eff }}\right)$ by computing the resolution of an ideal
converter whose SQNR presented in (15.16) is exactly the same as the SNDR of the converter under test. Specifically, assuming SNDR is measured with a single-tone sinusoidal input,

$$
\begin{equation*}
\mathrm{N}_{\mathrm{eff}}=\frac{\text { SNDR }-1.76 \mathrm{~dB}}{6.02} \text { bits } \tag{15.29}
\end{equation*}
$$

Substitution of a measured SNDR into (15.29) will generally result in a fractional number of bits (for example, a converter may have 8.7 effective bits) which is perfectly fine since $\mathrm{N}_{\text {eff }}$ is merely a performance metric relating a converter's performance to that of a fictitious ideal quantizer. Note that if measured properly, SNDR includes quantization noise and it therefore can not exceed the SQNR in (15.16), so that $\mathrm{N}_{\text {eff }}<\mathrm{N}$ for any N -bit converter.

Key Point: The most common measure of accuracy at high input signal frequencies is dynamic range, often quantified by the maximum achievable signal-to-noise and distortion ratio (SNDR). This may be expressed in $d B$, or as an effective number of bits. A converter's effective resolution bandwidth specifies the band over which SNDR is within 3 dBof its highest value.

It should be noted that this approach often results in a dynamic range measurement that is a function of the frequency of the sinusoidal input. Hence, it is a more realistic way of measuring the performance of a converter than extrapolating the nonlinearity performance found using dc inputs. For example, if an 8 -bit, $200-\mathrm{MHz}, \mathrm{A} / \mathrm{D}$ converter has a bandlimited preamplifier or a slew-rate limited sample and hold, dc inputs may show full 8 -bit performance even at the maximum sample rate of 200 Msample/s. However, a high-frequency, sinusoidal input, at, say, 40 MHz , will require the input stage to track a rapidly varying signal and may result in only 6-bit performance. To capture this limitation, the efffective resolution bandwidth is specified as the bandwidth over which a converter's peak SNDR is within 3 dB of its best value, or equivalently the bandwidth over which $\mathrm{N}_{\text {eff }}$ is within 0.5 bits of its peak value.

Finally, it should be mentioned that the distortion level (or nonlinearity performance) of some converters remains at a fixed level and is not a function of the input signal level. Thus, as the input signal level is decreased, the signal-to-distortion ratio decreases. This behavior occurs because the distortion level is often determined by component matching and thus is fixed once the converter is realized. However, in some converters, the distortion level decreases as the input signal level is decreased, which is often a desirable property to have. For example, most 1-bit oversampling converters have this desirable property since they do not rely on component matching and their distortion level is often a result of weak nonlinear effects at the input stage.

#### EXAMPLE 15.4

Consider a 3-bit $\mathrm{D} / \mathrm{A}$ converter in which $\mathrm{V}_{\text {ref }}=4 \mathrm{~V}$, with the following measured voltage values:

$$
\{0.011: 0.507: 1.002: 1.501: 1.996: 2.495: 2.996: 3.491\}
$$

1. Find the offset and gain errors in units of LSBs.
2. Find the INL (endpoint) and DNL errors (in units of LSBs).
3. Find the effective number of bits of absolute accuracy.
4. Find the effective number of bits of relative accuracy.

#### Solution

We first note that 1 LSB corresponds to $\mathrm{V}_{\text {ref }} / 2^{3}=0.5 \mathrm{~V}$.

1. Since the offset voltage is 11 mV , and since 0.5 V corresponds to 1 LSB , we see that the offset error is given by

$$
\begin{equation*}
\mathrm{E}_{\mathrm{off}(\mathrm{D} / \mathrm{A})}=\frac{0.011}{0.5}=0.022 \mathrm{LSB} \tag{15.30}
\end{equation*}
$$

For the gain error, from (15.25) we have

$$
\begin{equation*}
\mathrm{E}_{\operatorname{gain}(\mathrm{D} / \mathrm{A})}=\left(\frac{3.491-0.011}{0.5}\right)-\left(2^{3}-1\right)=-0.04 \mathrm{LSB} \tag{15.31}
\end{equation*}
$$

2. For INL and DNL errors, we first need to remove both offset and gain errors in the measured D/A values. The offset error is removed by subtracting 0.022 LSB off each value, whereas the gain error is eliminated by subtracting off scaled values of the gain error. For example, the new value for 1.002 (scaled to 1 LSB) is given by

$$
\begin{equation*}
\frac{1.002}{0.5}-0.022+\left(\frac{2}{7}\right)(0.04)=1.993 \tag{15.32}
\end{equation*}
$$

Thus, the offset-free, gain-free, scaled values are given by

$$
\{0.0: 0.998: 1.993: 2.997: 3.993: 4.997: 6.004: 7.0\}
$$

Since these results are in units of LSBs, we calculate the INL errors as the difference between these values and the ideal values, giving us

INL errors: $\quad\{0:-0.002:-0.007:-0.003:-0.007:-0.003: 0.004: 0\}$
For DNL errors, we find the difference between adjacent offset-free, gain-free, scaled values to give
DNL errors: $\quad\{-0.002:-0.005: 0.004:-0.004: 0.004: 0.007:-0.004\}$
3. For absolute accuracy, we find the largest deviation between the measured values and ideal values, which, in this case, occurs at 0 V and is 11 mV . To relate this $11-\mathrm{mV}$ value to effective bits, 11 mV should correspond to 1 LSB when $\mathrm{V}_{\text {ref }}=4 \mathrm{~V}$. In other words, we have the relationship

$$
\begin{equation*}
\frac{4 \mathrm{~V}}{2^{N_{\mathrm{eff}}}}=11 \mathrm{mV} \tag{15.33}
\end{equation*}
$$

which results in an absolute accuracy of $\mathrm{N}_{\mathrm{abs}}=8.5$ bits.
4. For relative accuracy, we use the INL errors found in part 2, whose maximum magnitude is 0.007 LSB , or equivalently, 3.5 mV . We relate this $3.5-\mathrm{mV}$ value to effective bits in the same manner as in part 3 , resulting in a relative accuracy of $\mathrm{N}_{\mathrm{rel}}=10.2$ bits.

#### EXAMPLE 15.5

A full-scale sinusoidal waveform is applied to a 12 -bit $\mathrm{A} / \mathrm{D}$ converter, and the output is digitally analyzed. If the fundamental has a normalized power of 1 W while the remaining power is $0.5 \mu \mathrm{~W}$, what is the effective number of bits for the converter?

#### Solution

In this case, the signal-to-noise and distortion ratio is found to be

$$
\begin{equation*}
\text { SNDR }=10 \log \left(\frac{1}{0.5 \times 10^{-6}}\right)=63 \mathrm{~dB} \tag{15.34}
\end{equation*}
$$

Substituting this SNDR value into (15.29), we find

$$
\begin{equation*}
N_{\text {eff }}=\frac{63-1.76}{6.02}=10.2 \text { effective bits } \tag{15.35}
\end{equation*}
$$

## 15.6 KEY POINTS

- In Nyquist-rate converters, there is a one-to-one correspondence between input and output values. Oversampling converters increase SNR by operating much faster than the input signal's Nyquist rate and filtering out quantization noise outside of the signal bandwidth. [p. 606]
- Data converters translate between digital binary codes and analog voltages or currents. In an ideal converter, the binary codes correspond to analog signal quantities that are precisely equally spaced. [p. 607]
- As long as it is not overloaded, the ideal quantizer introduces an additive quantization noise less than $1 / 2$ of an LSB in magnitude. [p. 609]
- Quantization noise may be modeled as a random quantity uniformly distributed between $-\mathrm{LSB} / 2$ and $+\mathrm{LSB} / 2$. For a sinusoidal input, this results in a maximum SNR of $6.02 \mathrm{~N}+1.76 \mathrm{~dB}$ for an ideal N -bit converter. [p. 611]
- Integral nonlinearity (INL) is a popular measure of accuracy that specifies the deviation of a converter's inputoutput relationship away from the ideal, or least-squares fit, linear relationship. [p. 616]
- Both DNL and INL are measured at dc or very low input frequencies. They are therefore referred to as measures of static nonlinearity. [p. 616]
- Uncertainty in the sampling times of a converter, called aperture jitter, can be a significant performance limitation at high input signal frequencies. [p. 617]
- The most common measure of accuracy at high input signal frequencies is dynamic range, often quantified by the maximum achievable signal-to-noise and distortion ratio (SNDR). This may be expressed in dB , or as an effective number of bits. A converter's effective resolution bandwidth specifies the band over which SNDR is within 3 dB of its highest value. [p. 618]
