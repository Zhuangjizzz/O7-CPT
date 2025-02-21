# 17 Nyquist-Rate A/D Converters

Architectures for realizing analog-to-digital (A/D) converters can be roughly divided into three categories (Table 17.1)-low-to-medium speed, medium speed, and high speed. In this chapter, design details are discussed for these different approaches except for oversampling converters. Oversampling converters are best described using many signal processing concepts and are therefore discussed separately in Chapter 18.

Before proceeding, it should be noted that when discussing the design of A/D converters, we usually ignore the 0.5 LSB offset present in the A/D transfer characteristic. Such a simplification is made so as not to complicate the concepts presented. Many of the converter architectures described make extensive use of switched capacitor circuits and comparators; the reader is referred to those chapters for more detail on those circuits.

## 17.1 INTEGRATING CONVERTERS

Integrating A/D converters is a popular approach for realizing high-accuracy data conversion on very slowmoving signals. These types of converters have very low offset and gain errors in addition to being highly linear. A further advantage of integrating converters is the small amount of circuitry required in their implementation. One application that has traditionally made use of integrating converters is measurement instruments such as voltage or current meters.

A simplified diagram for a dual-slope integrating converter is shown in Fig. 17.1. Dual-slope refers to this converter performing its conversion in two phases, (I) and (II), in the following manner (Fig. 17.2):

Phase (I) Phase (I) is a fixed time interval of length $\mathrm{T}_{1}$ determined by running the counter for $2^{\mathrm{N}}$ clock cycles. Thus, we have

$$
\begin{equation*}
\mathrm{T}_{1}=2^{\mathrm{N}} \mathrm{~T}_{\mathrm{clk}} \tag{17.1}
\end{equation*}
$$

where $T_{\text {clk }}$ is the period for one clock cycle. During this interval, switch $S_{1}$ is connected to $-V_{\text {in }}$ such that $V_{x}$ ramps up proportional to the magnitude of $\mathrm{V}_{\mathrm{in}}$. Assuming $\mathrm{V}_{\mathrm{x}}$ is initially equal to zero (due to a pulse on $\mathrm{S}_{2}$ ), and

Table 17.1 Different A/D converter architectures.

| Low-to-Medium Speed, <br> High Accuracy | Medium Speed, <br> Medium Accuracy | High Speed, <br> Low-to-Medium Accuracy |
| :--- | :--- | :--- |
| Integrating | Successive approximation | Flash |
| Oversampling | Algorithmic | Two-step |
|  |  | Interpolating |
|  |  | Folding |
|  |  | Pipelined |
|  |  | Time-interleaved |

that $\mathrm{V}_{\text {in }}$ is constant, we have the following relationship for $\mathrm{V}_{\mathrm{x}}$ :

$$
\begin{equation*}
\mathrm{V}_{\mathrm{x}}(\mathrm{t})=-\int_{0}^{\mathrm{t}} \frac{\left(-\mathrm{V}_{\mathrm{in}}\right)}{\mathrm{R}_{1} \mathrm{C}_{1}} \mathrm{~d} \tau=\frac{\mathrm{V}_{\mathrm{in}}}{\mathrm{R}_{1} \mathrm{C}_{1}} t \tag{17.2}
\end{equation*}
$$

Thus, at the end of phase (I), the value of $V_{x}$ is equal to $V_{i n} T_{1} / R_{1} C_{1}$.
Phase (II) Phase (II) occurs for a variable amount of time, $\mathrm{T}_{2}$, as shown in Fig. 17.2 for three different input voltages. At the beginning of this phase, the counter is reset and switch $S_{1}$ is connected to $V_{\text {ref }}$, resulting in a constant slope for the decaying voltage at $\mathrm{V}_{\mathrm{x}}$. To obtain the digital output value, the counter simply counts until $\mathrm{V}_{\mathrm{x}}$ is less than zero, at which point that count value equals the digitized value of the input signal, $\mathrm{V}_{\mathrm{in}}$. Thus, assuming the digital output count is normalized so that the largest count is unity, the counter output, $\mathrm{B}_{\text {out }}$, can be defined to be

$$
\begin{equation*}
\mathrm{B}_{\text {out }}=\mathrm{b}_{1} 2^{-1}+\mathrm{b}_{2} 2^{-2}+\cdots+\mathrm{b}_{\mathrm{N}-1} 2^{-(\mathrm{N}-1)}+\mathrm{b}_{\mathrm{N}} 2^{-\mathrm{N}} \tag{17.3}
\end{equation*}
$$

image_name:Fig. 17.1 Integrating (dual slope) A/D converter.
description:The circuit is an integrating (dual slope) A/D converter. It uses a dual-slope integration method to convert an analog input voltage (-Vin) into a digital output (Bout). The integration period is controlled by switches S1 and S2, and the output is determined by a counter that measures the time it takes for the integrated voltage to reach zero.

Fig. 17.1 Integrating (dual slope) A/D converter.
image_name:Fig. 17.2
description:The graph in Fig. 17.2 represents the operation of an integrating (dual slope) A/D converter for three different input voltages (-Vin1, -Vin2, -Vin3). It is a time-domain waveform with the x-axis labeled as 'Time' and the y-axis labeled as 'Vx'. The graph is divided into two phases: Phase (I) and Phase (II).

1. **Phase (I):** During this phase, the voltage Vx increases linearly from zero to a peak value. The slope of the line is determined by the input voltage (-Vin). There are three different slopes shown, corresponding to three different input voltages (-Vin1, -Vin2, -Vin3), with -Vin3 having the steepest slope and -Vin1 the shallowest. The duration of this phase is marked as T1.

2. **Phase (II):** This phase begins at the peak of each line from Phase (I) and shows a constant negative slope, indicating a linear decrease in Vx back to zero. The slopes in this phase are constant and identical for all three input voltages, representing the discharge phase of the integration process. The time taken for Vx to return to zero is marked as T2, which varies for each input voltage.

3. **Key Features:**
- The graph demonstrates how different input voltages affect the time it takes for the integrated voltage to reach zero during Phase (II).
- The peak values during Phase (I) correspond to the magnitude of the input voltages.
- T1 is constant across all three scenarios, while T2 varies, demonstrating the dual-slope method's dependence on the input voltage.

4. **Annotations:**
- The graph is annotated with labels for each phase and the input voltages.
- The transition between phases is marked with a vertical dashed line, indicating the point where the integration switches from charging to discharging.

This graph effectively illustrates the dual-slope integration process by showing the relationship between input voltage and the integration time required to return to zero, a crucial aspect of the A/D conversion method used in this circuit.

Fig. 17.2 Operation of the integrating converter for three different input voltages.
and we have

$$
\begin{equation*}
T_{2}=2^{N} B_{\text {out }} T_{c l k}=\left(b_{1} 2^{N-1}+b_{2} 2^{N-2}+\cdots+b_{N-1} 2+b_{N}\right) T_{c l k} \tag{17.4}
\end{equation*}
$$

To see why this count gives the correct value, we find the equation for $\mathrm{V}_{\mathrm{x}}$ during phase (II) to be given by

$$
\begin{align*}
V_{x}(t) & =-\int_{T_{1}}^{t} \frac{V_{\text {ref }}}{R_{1} C_{1}} d \tau+V_{x}\left(T_{1}\right) \\
& =\frac{-V_{\text {ref }}}{R_{1} C_{1}}\left(t-T_{1}\right)+\frac{V_{\text {in }} T_{1}}{R_{1} C_{1}} \tag{17.5}
\end{align*}
$$

Since $V_{x}$ equals zero when $t=T_{1}+T_{2}$, we can write

$$
\begin{equation*}
0=\frac{-\mathrm{V}_{\mathrm{ref}} \mathrm{~T}_{2}}{\mathrm{R}_{1} \mathrm{C}_{1}}+\frac{\mathrm{V}_{\mathrm{in}} \mathrm{~T}_{1}}{\mathrm{R}_{1} \mathrm{C}_{1}} \tag{17.6}
\end{equation*}
$$

and thus $T_{2}$ is related to $T_{1}$ by the following relationship:

$$
\begin{equation*}
\mathrm{T}_{2}=\mathrm{T}_{1}\left(\frac{\mathrm{~V}_{\mathrm{in}}}{\mathrm{~V}_{\mathrm{ret}}}\right) \tag{17.7}
\end{equation*}
$$

Combining (17.7) with (17.1) and (17.4), we find

$$
\begin{equation*}
B_{\text {out }}=b_{1} 2^{-1}+b_{2} 2^{-2}+\cdots+b_{N-1} 2^{-(N-1)}+b_{N} 2^{-N}=\frac{V_{\text {in }}}{V_{\text {ref }}} \tag{17.8}
\end{equation*}
$$

as expected.

Key Point: Dual-slope integrating conversion proceeds first by integrating the input for a fixed time period, then applying a known input to the integrator and measuring the time required for the integrator output to return to zero.

From (17.8), we see that in a dual-slope conversion (i.e., two phases), the digital output does not depend on the time constant, $\mathrm{R}_{1} \mathrm{C}_{1}$. In fact, the value of this time constant need only be stable during a single conversion for proper operation. However, $\mathrm{R}_{1}$ and $\mathrm{C}_{1}$ should be chosen such that a reasonable large peak value of $\mathrm{V}_{\mathrm{x}}$ is obtained without clipping to reduce noise effects. It is also possible to perform a single-slope conversion where only one integration phase is needed, however the integration time would then be a function of the time-constant value, $\mathrm{R}_{1} \mathrm{C}_{1}$, and a gain error would most likely occur.

Although a dual-slope converter does not suffer from gain error, it can have an offset error due to opamp offset and other factors. Such an offset error can be calibrated out by going to a quad-slope conversion. In a quad-slope conversion, a dual-slope conversion is performed twice: once with the input connected to ground (or other known dc quantity), and then with the input connected to the signal to be converted, $\mathrm{V}_{\mathrm{in}}$. A subtraction of the two output words causes the offset error to be reduced to zero.

Key Point: Dual-slope conversion does not require accuracy in defining the integration time constant. Offset errors can be calibrated by performing an additional conversion using a known dc input quantity.

The conversion speed for these types of converters is quite slow. For example, in a dual-slope converter, the worst-case conversion speed occurs when $\mathrm{V}_{\text {in }}$ equals $\mathrm{V}_{\text {ref }}$. In this case, the number of clock cycles to perform a conversion is $2^{\mathrm{N}+1}$. Thus for a 16 -bit converter with a clock frequency equal to 1 MHz , the worst-case conversion rate is around 7.6 Hz .

Finally, it should be mentioned that by a careful choice for $T_{1}$, certain frequency components superimposed on the input signal can be significantly attenuated. Note that this converter effectively "integrates and dumps" the input signal. If we relax the assumption that $\mathrm{V}_{\text {in }}$ is constant in (17.2), we see that before being converted $\mathrm{V}_{\text {in }}$ is actually integrated over a time window $T_{1}$ in duration,

$$
\begin{equation*}
\int_{0}^{T_{1}} \frac{V_{\text {in }}(\tau)}{R_{1} C_{1}} d \tau \tag{17.9}
\end{equation*}
$$

which is equivalent to convolution by a rectangular time function. Since the Fourier transform of a rectangular pulse is a " $\sin (\mathrm{x}) / x$ " type response, we have an effective input filter with a transfer function,

$$
\begin{equation*}
|H(f)|=\left|\frac{\sin \left(\pi \mathrm{fT}_{1}\right)}{\left(\pi \mathrm{fT} \mathrm{~T}_{1}\right)}\right| \tag{17.10}
\end{equation*}
$$

Therefore, integrating converters have a low-pass response, with nulls at all integer multiples of $f=1 / T_{1}$.

Key Point: Integrating converters inherently filter the input with a $\sin x / x$ frequency response.

#### EXAMPLE 17.1

If the input signal, $\mathrm{V}_{\mathrm{in}}$, is a dc level with power line noise of 60 Hz superimposed on it, choose $\mathrm{T}_{1}$ to filter out the power line noise.

#### Solution

Write $\mathrm{V}_{\text {in }}$ as

$$
\begin{equation*}
V_{\text {in }}=V_{\text {in(ideal) }}+V_{\text {in(60 Hz) }} \tag{17.11}
\end{equation*}
$$

where $\mathrm{V}_{\text {in(ideal) }}$ is the desired dc signal level and $\mathrm{V}_{\mathrm{in}(60 \mathrm{~Hz})}$ is the interfering 60 Hz noise; or mathematically,

$$
\begin{equation*}
V_{i n(60 H z)}=A \sin (120 \pi t+\phi) \tag{17.12}
\end{equation*}
$$

where A and $\phi$ are arbitrary magnitude and phase values. Now substituting this relationship for $\mathrm{V}_{\text {in }}$ into (17.2), we have

$$
\begin{equation*}
V_{x}\left(T_{1}\right)=-\int_{0}^{T_{1}} \frac{\left(-V_{\text {in }}\right)}{R_{1} C_{1}} d \tau=-\int_{0}^{T_{1}} \frac{\left(-V_{\text {in (ideal })}\right)}{R_{1} C_{1}} d \tau-\int_{0}^{T_{1}} \frac{\left(-V_{\text {in }(60 H z)}\right)}{R_{1} C_{1}} d \tau \tag{17.13}
\end{equation*}
$$

However, the last term in (17.13) can be shown to equal zero when $T_{1}$ is an integer multiple of $1 /(60 \mathrm{~Hz})$ (i.e., 16.67 ms ). In this way, the peak value, $\mathrm{V}_{\mathrm{x}}\left(\mathrm{T}_{1}\right)$, remains correct so that the conversion is performed without error. Note that for this same value of $\mathrm{T}_{1}$, the harmonics of 60 Hz are also suppressed (i.e., $120 \mathrm{~Hz}, 180 \mathrm{~Hz}, 240$ Hz , etc.). The converter's frequency response is shown in Fig. 17.3 with $T_{1}=1 /(60 \mathrm{~Hz})$. Note that full suppression is achieved at harmonics of 60 Hz , as expected.

In fact, other frequencies are also attenuated but not fully suppressed as are the harmonics of $1 / T_{1}$. Note the $-20 \mathrm{~dB} /$ decade slope in Fig. 17.3, so that higher frequencies are attenuated more.

#### EXAMPLE 17.2

It is desired to build a 16 -bit two-slope integrating $A / D$ such that a maximum input signal of $\mathrm{V}_{\text {in }}=3 \mathrm{~V}$ results in the peak voltage of $\mathrm{V}_{\mathrm{x}}$ being 4 V . In addition, input noise signals at 50 Hz and harmonics should be significantly attenuated. Find the required RC time constant and clock rate. Also, find the attenuation of a noise signal around 1 kHz superimposed on the input signal.

#### Solution

Since 50 Hz and harmonics are to be rejected, we choose
image_name:Fig. 17.3 Magnitude response of the effective input filter
description:The graph is a Bode plot illustrating the magnitude response of an effective input filter for an integrating-type converter. The x-axis represents frequency in hertz, displayed on a logarithmic scale, ranging from 10 Hz to 300 Hz. The y-axis represents the magnitude |H(f)| in decibels (dB), ranging from 0 dB to -40 dB.

The plot shows a series of attenuations and peaks. The magnitude response starts at 0 dB at low frequencies and decreases, following a general slope of -20 dB per decade, as indicated by the dashed line. This slope represents the general trend of attenuation as frequency increases.

Significant features include:
- A pronounced dip in magnitude at 60 Hz, where the response reaches a minimum, showing significant attenuation.
- Subsequent peaks and valleys occur at harmonic frequencies, specifically at 120 Hz, 180 Hz, 240 Hz, and 300 Hz, with the magnitude of these peaks decreasing progressively.

This pattern indicates that the filter effectively attenuates signals at 50 Hz and its harmonics, while allowing some periodic increase in response at higher harmonics, though at reduced levels. The design is likely intended to reject power line noise and its harmonics efficiently.

Fig. 17.3 Magnitude response of the effective input filter for an integrating-type converter with $T_{1}=1 /(60 \mathrm{~Hz})$

$$
\begin{equation*}
\mathrm{T}_{1}=\frac{1}{50}=20 \mathrm{~ms} \tag{17.14}
\end{equation*}
$$

Thus, for a 16-bit converter, we require a clock frequency of

$$
\begin{equation*}
\mathrm{f}_{\mathrm{clk}}=\frac{1}{\mathrm{~T}_{\mathrm{clk}}}=\frac{2^{16}}{\mathrm{~T}_{1}}=3.28 \mathrm{MHz} \tag{17.15}
\end{equation*}
$$

To find the RC time constant needed, we note that at the end of phase (I), $\mathrm{V}_{\mathrm{x}}$ is given by

$$
\begin{equation*}
\mathrm{V}_{\mathrm{x}}=\frac{\mathrm{V}_{\mathrm{in}} \mathrm{~T}_{1}}{\mathrm{R}_{1} \mathrm{C}_{1}} \tag{17.16}
\end{equation*}
$$

and using the values of $\mathrm{V}_{\mathrm{x}}=4 \mathrm{~V}, \mathrm{~V}_{\mathrm{in}}=3 \mathrm{~V}$, and $\mathrm{T}_{1}=20 \mathrm{~ms}$ results in

$$
\begin{equation*}
\mathrm{R}_{1} \mathrm{C}_{1}=15 \mathrm{~ms} \tag{17.17}
\end{equation*}
$$

Finally, the attenuation of a $1-\mathrm{kHz}$ signal is infinite since it is a harmonic of 50 kHz . However, as seen in (17.10), attenuation is reduced halfway between harmonics, so we find the gain for an input signal at 975 Hz to be

$$
\begin{equation*}
|\mathrm{H}(\mathrm{f})|=\left|\frac{\sin (\pi \times 975 \mathrm{~Hz} \times 20 \mathrm{~ms})}{\pi \times 975 \mathrm{~Hz} \times 20 \mathrm{~ms}}\right|=16.3 \times 10^{-3} \tag{17.18}
\end{equation*}
$$

which implies the attenuation is 36 dB .

## 17.2 SUCCESSIVE-APPROXIMATION CONVERTERS

Successive-approximation A/D converters are one of the most popular approaches for realizing A/D converters due to their amazing versatility. They can provide reasonably quick conversion time, or they can be used for
relatively high accuracy, and can operate with very low power in either case. Fundamentally, these benefits arise because successive-approximation converters require only modest circuit complexity, in the simplest cases requiring only a single comparator, a bank of capacitors with switches, and a small amount of digital control logic.

To understand the basic operation of successive-approximation converters, knowledge of the search algorithm referred to as a "binary search" is helpful. As an example of a binary search, consider the game of guessing a random number from 1 to 128 where one can ask only questions that have a "yes/no" response. The first question might be, "Is the number greater than 64 ?" If the answer is yes, then the second question asks whether the number is greater than 96 . However, if the first answer is no, then the second question asks whether the number is greater than 32. The third question divides the search space in two once again and the process is repeated until the random number is determined. In general, a binary search divides the search space in two each time, and the desired data can be found in N steps for a set of organized data of size $2^{\mathrm{N}}$.
image_name:Fig. 17.4
description:The flow graph depicted in Fig. 17.4 represents the successive-approximation approach used in analog-to-digital conversion. The process begins with the 'Start' block, indicating the initiation of the successive approximation procedure. The input to the system is a signed analog voltage, denoted as \( V_{in} \).

1. **Main Components:**
- **Sample Block:** The process starts with sampling the input voltage \( V_{in} \) and initializing the digital-to-analog converter (D/A) output \( V_{D/A} \) to 0. The index \( i \) is also initialized to 1.
- **Comparator:** A decision block compares \( V_{in} \) with \( V_{D/A} \).
- **Binary Decision Blocks:** Two paths emerge from the comparison:
- If \( V_{in} > V_{D/A} \), the bit \( b_i \) is set to 1.
- If \( V_{in} \leq V_{D/A} \), the bit \( b_i \) is set to 0.
- **Update Blocks:** Depending on the outcome, \( V_{D/A} \) is updated:
- If \( b_i = 1 \), \( V_{D/A} \) is increased by \( V_{ref}/2^{i+1} \).
- If \( b_i = 0 \), \( V_{D/A} \) is decreased by \( V_{ref}/2^{i+1} \).
- **Index Increment Block:** The index \( i \) is incremented by 1.
- **Loop Condition Block:** Checks if \( i \) is greater than or equal to \( N \), where \( N \) is the resolution of the converter.

2. **Flow of Information or Control:**
- The process begins with the sampling of \( V_{in} \) and setting initial conditions.
- A loop iteratively compares \( V_{in} \) with \( V_{D/A} \), adjusts \( V_{D/A} \) based on the comparison, and increments the index \( i \).
- This loop continues until the resolution limit \( N \) is reached, ensuring that the binary representation of \( V_{in} \) is determined.

3. **Labels, Annotations, and Key Indicators:**
- The diagram includes annotations such as \( V_{in} \), \( V_{D/A} \), \( b_i \), and \( V_{ref} \), which are crucial for understanding the conversion process.
- The loop condition \( i \geq N \) serves as a termination point for the conversion process.

4. **Overall System Function:**
- The successive-approximation approach is designed to convert an analog input voltage \( V_{in} \) into a digital output by iteratively refining the approximation of \( V_{in} \). Each iteration narrows down the possible range of \( V_{in} \) by adjusting \( V_{D/A} \) based on the comparison results, ultimately resulting in a precise digital representation of the analog input after \( N \) iterations.

Fig. 17.4 Flow graph for the successive-approximation approach.
image_name:Fig. 17.4
description:The diagram labeled "Fig. 17.4" illustrates a block diagram of a successive-approximation analog-to-digital converter (ADC). The primary components and their functions are as follows:

1. **Sample and Hold (S/H) Circuit**: This block receives the analog input voltage \( V_{in} \) and samples it. The sampled value is held constant during the conversion process to ensure accuracy.

2. **Comparator**: The comparator has two inputs; one from the S/H circuit and the other from the output of the Digital-to-Analog (D/A) Converter. It compares the input voltage \( V_{in} \) with the feedback voltage \( V_{D/A} \) from the D/A converter. The comparator outputs a signal indicating whether \( V_{in} \) is greater or less than \( V_{D/A} \).

3. **Successive-Approximation Register (SAR) and Control Logic**: This block receives the comparator's output and adjusts the digital approximation of \( V_{in} \) accordingly. It generates a sequence of binary outputs \( b_1, b_2, \ldots, b_N \) which refine the approximation of the input voltage.

4. **D/A Converter**: This block converts the binary output from the SAR into an analog voltage \( V_{D/A} \). The \( V_{D/A} \) is fed back to the comparator to be compared with \( V_{in} \).

5. **Reference Voltage \( V_{ref} \)**: The D/A converter uses a reference voltage \( V_{ref} \) to scale the output voltage \( V_{D/A} \).

6. **Digital Output \( B_{out} \)**: After several iterations, the SAR outputs a digital word \( B_{out} \) that represents the analog input \( V_{in} \).

**Flow of Information**:
- The analog input \( V_{in} \) is sampled and held by the S/H circuit.
- The comparator compares \( V_{in} \) with \( V_{D/A} \) and sends the result to the SAR.
- The SAR adjusts its digital output based on the comparator's feedback and sends this digital approximation to the D/A converter.
- The D/A converter generates a new \( V_{D/A} \) based on the SAR's output.
- This process iterates until the SAR determines the digital output \( B_{out} \) that best approximates \( V_{in} \).

**Overall System Function**:
The system's primary function is to convert an analog signal \( V_{in} \) into a digital representation \( B_{out} \) using successive approximation. This method involves iteratively refining the digital output by comparing the input voltage with the D/A converter's output, allowing for accurate digital conversion with moderate speed and low power consumption.

Fig. 17.5 D/A converter-based successive-approximation converter.

Key Point: Successive-approximation $A / D$ converters are very versatile, capable of moderately high speed or accuracy with relatively low power. They are relatively simple circuits, in the simplest cases requiring only a single comparator, a bank of capacitors and switches, and a small digital logic circuit. Their biggest drawback is that they operate iteratively and therefore require many clock cycles to perform a single conversion.

Successive-approximation converters apply a binary search algorithm to determine the closest digital word to match an input signal. Specifically, in the first period, after possibly the reset period, the MSB, $b_{1}$, is determined. In the second period, the next bit, $b_{2}$, is determined, followed by $b_{3}$ and so on until all $N$ bits are determined. Thus, in its most straightforward implementation, a successive-approximation converter requires N clock cycles to complete an N -bit conversion. A flow graph for a signed conversion using a successive-approximation approach is shown in Fig. 17.4. Here, the signed output is in offset-binary coding and the input signal is assumed to be within $\pm 0.5 \mathrm{~V}_{\text {ret }}$. The flow graph for a unipolar conversion is only slightly different and is left as an exercise for the reader. The major drawback of successive-approximation converters is that, because their principle of operation is an iterative search, they require multiple clock cycles for each input conversion. This limits their conversion frequency to far below the circuit's maximum clock frequency, particularly when high resolution is sought since more iterations are required.

### 17.2.1 D/A-Based Successive Approximation

The block diagram for a unipolar successive-approximation A/D converter that uses a D/A converter is shown in Fig. 17.5. The successive-approximation register (SAR) and control logic are entirely digital and perform the necessary binary search. At the end of the conversion, the digital value in the SAR results in the voltage $\mathrm{V}_{\mathrm{D} / \mathrm{A}}$ being within $0.5 \mathrm{~V}_{\mathrm{LSB}}$ of the input signal. With this type of architecture, the $\mathrm{D} / \mathrm{A}$ converter typically determines the accuracy and speed of the $\mathrm{A} / \mathrm{D}$ converter. Note that a sample and hold is required at the input so that the value to be converted does not change during the conversion time.

#### EXAMPLE 17.3

Consider the case where $\mathrm{V}_{\text {ret }}=1 \mathrm{~V}, \mathrm{~V}_{\text {in }}=0.354 \mathrm{~V}$, and a 3-bit conversion is performed. Find intermediate $\mathrm{D} / \mathrm{A}$ values and the final output.

#### Solution

In this case, $\mathrm{V}_{\mathrm{LSB}}=0.125 \mathrm{~V}$.

In cycle $1: B_{\text {out }}=100$ so that $V_{D / A}=0.5 \mathrm{~V}$. Since $V_{\text {in }}<V_{D / A}, b_{1}$ is set to 0 .
In cycle 2: $B_{\text {out }}=010$ so that $V_{D / A}=0.25 \mathrm{~V}$. Since $V_{\text {in }}>V_{D / A}, b_{2}$ is set to 1.
In cycle 3 : $B_{\text {out }}=011$ so that $V_{D / A}=0.375 \mathrm{~V}$. Since $V_{\text {in }}<V_{D / A}, b_{3}$ is set to 0 .
Therefore, the resulting output is the last value of $B_{\text {out }}$, which is 010 . Although the final quantization error is $0.831 \mathrm{~V}_{\text {LSB }}$, it is greater than $\pm 0.5 \mathrm{~V}_{\mathrm{LSB}}$ because we have not accounted for the 0.5 LSB offset as discussed at the beginning of this chapter.

### 17.2.2 Charge-Redistribution A/D

The straightforward approach of using a separate $\mathrm{D} / \mathrm{A}$ converter and setting it equal to the input voltage (within one LSB) can be modified to the flow graph shown in Fig. 17.6. Here, the error signal V equals the difference between the input signal, $\mathrm{V}_{\mathrm{in}}$, and the $\mathrm{D} / \mathrm{A}$ output, $\mathrm{V}_{\mathrm{D} / \mathrm{A}}$. As a result, V is always compared to ground, as seen at the top of the flow graph, and the goal is to set this error difference within one LSB of zero.

One of the first switched-capacitor analog systems using this approach is a charge-redistribution MOS A/D converter [McCreary, 1975]. With such a converter, the sample and hold, D/A converter, and the difference portion of the comparator are all combined into a single circuit. The unipolar case is shown in Fig. 17.7 and operates as follows:

1. Sample mode: In the first step, all the capacitors are charged to $\mathrm{V}_{\text {in }}$ while the comparator is being reset to its threshold voltage through $\mathbf{S}_{2}$, In this step, note that the capacitor array is performing the sample-andhold operation.
2. Hold mode: Next, the comparator is taken out of reset by opening $\mathbf{s}_{2}$, and then all the capacitors are switched to ground. This causes $\mathrm{V}_{\mathrm{x}}$, which was originally zero, to change to $-\mathrm{V}_{\mathrm{in}}$, thereby holding the input signal, $\mathrm{V}_{\mathrm{in}}$, on the capacitor array. (This step is sometimes merged with the first bit time during bit cycling.) Finally, $s_{1}$ is switched so that $\mathrm{V}_{\text {ref }}$ can be applied to the capacitor array during bit cycling.
3. Bit cycling: Next, the largest capacitor (i.e., the 16 C capacitor in this example) is switched to $\mathrm{V}_{\text {ref }} . \mathrm{V}_{\mathrm{x}}$ now goes to $\left(-\mathrm{V}_{\text {in }}+\mathrm{V}_{\text {ref }} / 2\right)$. If $\mathrm{V}_{\mathrm{x}}$ is negative, then $\mathrm{V}_{\text {in }}$ is greater than $\mathrm{V}_{\text {ref }} / 2$, and the MSB capacitor is left connected to $V_{\text {ref }}$. Also $b_{1}$ is considered to be a 1 . Otherwise, the MSB capacitor is reconnected to ground and $b_{1}$ is taken to be 0 . This process is repeated $N$ times, with a smaller capacitor being switched each time, until the conversion is finished.

To get an exact division by two, note that an additional unit capacitor of size C has been added so that the total capacitance is $2^{\mathrm{N}} \mathrm{C}$ rather than $\left(2^{\mathrm{N}}-1\right) \mathrm{C}$. Also, the capacitor bottom plates should be connected to the $\mathrm{V}_{\text {ref }}$ side, not to the comparator side, to minimize the parasitic capacitance at node $\mathrm{V}_{\mathrm{x}}$. Although parasitic capacitance at $\mathrm{V}_{\mathrm{x}}$ does not cause any conversion errors with an ideal comparator, it does attenuate the voltage $\mathrm{V}_{\mathrm{x}}$.

A signed $A / D$ conversion can be realized by adding a $-\mathrm{V}_{\text {ref }}$ input. If $\mathrm{V}_{\mathrm{x}}$ is less than zero at the first step, then proceed as in the unipolar case using $\mathrm{V}_{\text {ref }}$. Otherwise, if $\mathrm{V}_{\mathrm{x}}$ is greater than zero, use $-\mathrm{V}_{\text {ref }}$ and test for $\mathrm{V}_{\mathrm{x}}$ greater than zero when deciding whether to leave the capacitors connected to $-V_{\text {ret }}$ or not

Key Point: The accuracy of successive-approximation converters is often determined by that of the D/A converter. In the case of charge-redistribution converters, this role is played by a bank of comparators whose matching is important.
at each bit cycling.
image_name:Fig. 17.6
description:The diagram is a flow graph representing a modified successive approximation process for a charge-redistribution converter. It begins with the "Start" block, indicating the initiation of the process. The next block is labeled "Sample," where the input voltage \( V_{\text{in}} \) is sampled, and the index \( i \) is initialized to 1. This represents the start of the bit cycling process.

The flow then proceeds to a decision block that checks whether the voltage \( V \) is greater than zero. This condition determines the subsequent path:

1. **If \( V > 0 \):**
- The bit \( b_i \) is set to 1.
- The voltage \( V \) is updated to \( V - V_{\text{ref}}/2^{i+1} \), effectively subtracting a fraction of the reference voltage based on the current bit position.
- The index \( i \) is incremented by 1.

2. **If \( V \leq 0 \):**
- The bit \( b_i \) is set to 0.
- The voltage \( V \) is updated to \( V + V_{\text{ref}}/2^{i+1} \), adding a fraction of the reference voltage.
- The index \( i \) is incremented by 1.

After updating the voltage and the index, the process checks whether \( i \) has exceeded \( N \), the total number of bits. If \( i \leq N \), the process loops back to the decision block to continue with the next bit. If \( i > N \), the process terminates at the "Stop" block.

The flow graph effectively describes a binary search algorithm used in analog-to-digital conversion, where each bit decision is based on comparing the current voltage with zero and adjusting the voltage accordingly. The process continues until all bits have been determined, resulting in a digital approximation of the input voltage.

Fig. 17.6 Flow graph for a modified successive approximation (divided remainder).

#### EXAMPLE 17.4

Find intermediate node voltages at $\mathrm{V}_{\mathrm{x}}$ during the operation of the 5 -bit charge-redistribution converter shown in Fig. 17.7 when $\bigvee_{\text {in }}=1.23 \mathrm{~V}$ and $\bigvee_{\text {ref }}=5 \mathrm{~V}$. Assume a parasitic capacitance of 8 C exists on the node at $\bigvee_{\mathrm{x}}$.

#### Solution

First, $\mathrm{V}_{\mathrm{x}}=0$ during sample mode. Next, during hold mode, all capacitors are switched and the charge on $\mathrm{V}_{\mathrm{x}}$ is shared between the 32 C total converter capacitance and the parasitic 8 C capacitance, resulting in

$$
\begin{equation*}
\mathrm{V}_{\mathrm{x}}=\frac{32}{32+8} \times-\mathrm{V}_{\mathrm{in}}=-0.984 \mathrm{~V} \tag{17.19}
\end{equation*}
$$

image_name:1. Sample mode
description:The circuit is a 5-bit unipolar charge-redistribution A/D converter. During sample mode, Vx is approximately 0. The capacitors are configured to sample the input voltage Vin. During hold mode, the capacitors are switched to redistribute charge. During bit cycling, the switches b1 to b5 are used to determine the digital output by comparing Vx to a reference voltage Vref.
image_name:2. Hold mode
descriptionThis is a 5-bit unipolar charge-redistribution A/D converter. The circuit operates in three modes: sample, hold, and bit cycling. Each bit cycling step adjusts the voltage at node Vx based on the input voltage Vin and reference voltage Vref. The SAR (Successive Approximation Register) is used to determine the digital output by comparing voltages.
image_name:3. Bit cycling
description:This circuit is a 5-bit unipolar charge-redistribution A/D converter. It uses capacitors and switches to sample and hold the input voltage, then performs bit cycling to convert the analog signal to a digital output using a Successive Approximation Register (SAR) logic.

Fig. 17.7 A 5-bit unipolar charge-redistribution A/D converter.

During the first bit cycling, $b_{1}$ is switched, resulting in

$$
\begin{equation*}
\mathrm{V}_{\mathrm{x}}=-0.984+\frac{16}{40} \times 5 \mathrm{~V}=1.016 \mathrm{~V} \tag{17.20}
\end{equation*}
$$

Since this result is greater than zero, switch $b_{1}$ is reversed back to ground and $\mathrm{V}_{\mathrm{x}}$ returns to -0.984 V . Thus, $b_{1}=0$.

Next, $b_{2}$ is switched, and we have

$$
\begin{equation*}
\mathrm{V}_{\mathrm{x}}=-0.984+\frac{8}{40} \times 5 \mathrm{~V}=0.016 \mathrm{~V} \tag{17.21}
\end{equation*}
$$

It is also greater than zero, so $\mathrm{b}_{2}=0$, and $\mathrm{V}_{\mathrm{x}}$ is set back to -0.984 V by switching $\mathrm{b}_{2}$ back to ground.
When $b_{3}$ is next switched, we have

$$
\begin{equation*}
\mathrm{V}_{\mathrm{x}}=-0.984+\frac{4}{40} \times 5=-0.484 \mathrm{~V} \tag{17.22}
\end{equation*}
$$

Since this result is less than zero, $b_{3}=1$, and switch $b_{3}$ is left connected to $V_{\text {ref }}$.
Next, $\mathrm{b}_{4}$ is switched, resulting in

$$
\begin{equation*}
\mathrm{V}_{\mathrm{x}}=-0.484+\frac{2}{40} \times 5=-0.234 \mathrm{~V} \tag{17.23}
\end{equation*}
$$

which is also less than zero, so $b_{4}=1$, and this switch is left connected to $V_{\text {ref }}$.
Finally, $\mathrm{b}_{5}$ is switched, resulting in

$$
\begin{equation*}
\mathrm{V}_{\mathrm{x}}=-0.234+\frac{1}{40} \times 5=-0.109 \mathrm{~V} \tag{17.24}
\end{equation*}
$$

which is also less than zero, so $b_{5}=1$.
Therefore, the output is given by $B_{\text {out }}=00111$ and voltage $V_{x}$ is within a $V_{\text {LSB }}$ of ground $\left(\mathrm{V}_{\text {LSB }}=5 / 32 \mathrm{~V}\right)$.

The same structure as the unipolar case can be used to realize a signed $\mathrm{A} / \mathrm{D}$ conversion while using only a single $\mathrm{V}_{\text {ref }}$ if a slightly modified switching arrangement is used. Referring to Fig. 17.8, and assuming $\mathrm{V}_{\text {in }}$ is between $\pm \mathrm{V}_{\text {ref }} / 2$, the conversion proceeds as follows:

1. Sample mode: In the first step, all the capacitors, except for the largest capacitor, are charged to $\mathrm{V}_{\mathrm{in}}$ while the comparator is being reset to its threshold voltage. For the signed case, the largest capacitor is now connected to $\mathrm{V}_{\text {ref }} / 2$.
2. Hold mode: Next, the comparator is first taken out of reset, and then all the capacitors, except the largest one, are switched to ground. This causes $\mathrm{V}_{\mathrm{x}}$, which was originally zero, to change to $-\mathrm{V}_{\mathrm{in}} / 2$. At the end of this step, the sign of the input signal is determined by looking at the comparator output.
3. Bit cycling: Next, the largest capacitor (i.e., the 16 C capacitor in this example) is switched to ground if, and only if, $\mathrm{V}_{\mathrm{x}}$ is larger than zero (i.e., when $\mathrm{V}_{\text {in }}$ is less than zero). Specifically, if $\mathrm{V}_{\mathrm{x}}$ is less than zero, then $\mathrm{V}_{\mathrm{in}}$ is positive and $\mathrm{b}_{1}$ is set to 1 , and conversion proceeds as in the unipolar case, starting with $b_{2}$, until conversion is completed. However, if $V_{x}$ is larger than zero, $b_{1}$ is set to 0 , the largest capacitor is switched to ground, causing $\mathrm{V}_{\mathrm{x}}$ to become $-\mathrm{V}_{\text {in }} / 2-\mathrm{V}_{\text {ref }} / 4$ (which is a negative value), and conversion proceeds as in the unipolar case, starting with $\mathrm{b}_{2}$. Once conversion is completed, some digital recoding may be required to obtain the desired output code.
This approach for realizing signed $A / D s$ has the disadvantage that $V_{\text {in }}$ has been attenuated by a factor of two, which makes noise more of a problem for high-resolution A/Ds. Also, any error in the MSB capacitor now causes both an offset and a sign-dependent gain error. The latter causes integral nonlinearity errors.
image_name:1. Sample mode
description:This circuit diagram represents a 5-bit signed charge-redistribution A/D converter in sample mode. It uses a combination of capacitors and switches to sample the input voltage (Vin) and hold it for conversion. The OpAmp is used to drive the SAR (Successive Approximation Register) for the conversion process. The capacitors are arranged in a binary-weighted configuration to facilitate the charge redistribution process.
image_name:2. Hold Mode
description:The circuit is a 5-bit signed charge-redistribution A/D converter in hold mode. It uses a combination of capacitors and switches to sample and hold the input voltage, Vin, and reference voltage, Vref/2, for conversion. The operational amplifier is used to drive the SAR (Successive Approximation Register) logic.
image_name:3. Bit cycling
description:The circuit is a 5-bit signed charge-redistribution A/D converter in bit cycling mode. It utilizes capacitors and switches to perform analog-to-digital conversion, controlled by a successive approximation register (SAR). The circuit operates in different modes: sample, hold, and bit cycling, adjusting the voltage Vx accordingly. This setup allows for precise voltage sampling and conversion.

Fig. 17.8 A 5-bit signed charge-redistribution A/D converter.
image_name:Fig. 17.9 Resistor-capacitor hybrid A/D converter
description:The circuit in Fig. 17.9 is a resistor-capacitor hybrid A/D converter. It uses a combination of resistor strings and capacitor arrays to perform analog-to-digital conversion. The circuit initially charges capacitors to Vin while resetting the comparator, and then performs successive approximation to find adjacent resistor nodes with voltages larger than the input.

Fig. 17.9 Resistor-capacitor hybrid A/D converter.

### 17.2.3 Resistor-Capacitor Hybrid

A combination of the resistor-string and capacitor-array approaches in a hybrid A/D converter, similar to the hybrid D/A converter [Fotouhi, 1979], is shown in Fig. 17.9.

The first step is to charge all the capacitors to $\mathrm{V}_{\text {in }}$ while the comparator is being reset. Next, a successiveapproximation conversion is performed to find the two adjacent resistor nodes that have voltages larger and smaller than $\mathrm{V}_{\mathrm{in}}$. One bus will be connected to one node while the other is connected to the other node. All of the capacitors are connected to the bus having the lower voltage. A successive approximation using the capacitor-array network is then done. Starting with the largest capacitor, a capacitor is switched to the adjacent resistor-string node having a larger voltage. If the comparator output is a 1 , it is switched back and $b_{i}$ is a 0 . Otherwise, the switch is left as is and $b_{i}$ is a 1 . Since the resistor string is monotonic, this type of converter is guaranteed monotonic if the capacitor array is monotonic.

### 17.2.4 Speed Estimate for Charge-Redistribution Converters

The major limitation on speed with charge redistribution converters is often due to the RC time constants of the capacitor array and switches. To estimate this time, consider the simplified model of a capacitor array being reset,
as shown in Fig. 17.10. Here, $R, R_{s 1}$, and $R_{s 2}$ represent the switch-on resistances of the bit line, $s 1$ and $s 2$ switches, respectively. Although this circuit is easily simulated using SPICE to find its settling time, it is useful to have a rough estimate of the charging time to speed up the design process. As in Section 16.1, the zero-value timeconstant approach [Sedra, 1991] can be used to obtain an estimate of the high-frequency time constant by summing individual time constants due to each capacitor. For example, the individual time constant due to the capacitance $2 C$ equals $\left(R_{s 1}+R+R_{s 2}\right) 2 C$. Following such an approach, the zero-value time constant for the circuit shown in Fig. 17.10 is equal to

$$
\begin{equation*}
\tau_{\text {eq }}=\left(R_{s 1}+R+R_{s 2}\right) 2^{N} C \tag{17.25}
\end{equation*}
$$

For better than 0.5 -LSB accuracy, we need

$$
\begin{equation*}
e^{-T / \tau_{\text {eq }}}<\frac{1}{2^{N+1}} \tag{17.26}
\end{equation*}
$$

where $T$ is the charging time. This equation can be simplified to

$$
\begin{equation*}
\mathrm{T}>\tau_{\mathrm{eq}}(\mathrm{~N}+1) \ln (2)=0.69(\mathrm{~N}+1) \tau_{\mathrm{eq}} \tag{17.27}
\end{equation*}
$$

It has been observed that (17.27) gives results about 30 percent higher than those obtained by simulating the actual RC network shown in Fig. 17.10. So while (17.27) can be used to roughly determine the maximum sampling rate, the final design should be simulated using accurate transistor models. Finally, although this result is not the same for all charge-redistribution A/D converters (for example, the size of the switches going to the larger capacitors may be increased to reduce their on resistance), the basic approach can be modified for most chargeredistribution $\mathrm{A} / \mathrm{D}$ converters.

### 17.2.5 Error Correction in Successive-Approximation Converters

With the best matching accuracy of on-chip elements being about 0.1 percent, one is limited to successiveapproximation converters having 10 -bit accuracy specifications without some sort of calibration. One errorcorrection technique that has been used to obtain 16-bit linear converters is shown in Fig. 17.11 [Lee, 1984]. In this approach, the MSB array is realized using binary-weighted capacitors that determine, for example, the first 10 bits.
image_name:Fig. 17.10
description:The circuit is a simplified model of a capacitor array during the sampling time, used in a charge-redistribution A/D converter with error correction.

Fig. 17.10 Simplified model of a capacitor array during the sampling time.
image_name:Fig. 17.11
description:The circuit is a charge-redistribution A/D converter with error correction, featuring a capacitor array and a sub-dac for the final 6 bits. It includes a cal-dac for calibration, addressing non-monotonic behavior. The successive-approximation register, control, accumulator, and data register are integral components.

Fig. 17.11 A charge-redistribution A/D converter with error correction.

For a 16-bit converter, the final 6 bits are determined using an additional capacitor and a resistor string referred to as a sub-dac. Although this combination of an MSB capacitor array and an LSB resistor string is not inherently monotonic, it can be easily autocalibrated at start-up by adding a second resistor string referred to as a cal-dac.

Calibration is done by measuring the errors of each capacitor, starting with the largest capacitor, calculating the correction terms required, and then storing the correction terms in a data register as $\mathrm{DV}_{\mathrm{ei}}$. During a regular successive approximation operation, whenever a particular capacitor is used, its error is cancelled by adding the value stored in the data register to that stored in an accumulator register, which contains the sum of the correction terms for all of the other capacitors currently connected to $\mathrm{V}_{\text {ref }}$. No correction terms are measured for the resistor sub-dac; its accuracy is not critical since it only determines the remaining LSBs.

The error terms are found starting with the MSB capacitor, $\mathrm{C}_{1}$. It is connected to ground and all of the other capacitors are connected to $\mathrm{V}_{\text {ret }}$ while the comparator is reset. Next, the comparator is taken out of reset mode, all of the other capacitors are switched to ground, and $C_{1}$ is switched to $V_{\text {ref }}$. Defining $C_{\text {total }}$ to be the sum of all the capacitors in the array, the ideal value of $C_{1}$ is $C_{\text {total }} / 2$. However, in practice $C_{1}$ varies from its ideal value, and thus, $\mathrm{C}_{1}$ can be written as

$$
\begin{equation*}
\mathrm{C}_{1} \equiv\left(\mathrm{C}_{\text {total }} / 2\right)+\Delta \mathrm{C}_{1} \tag{17.28}
\end{equation*}
$$

where $\Delta \mathrm{C}_{1}$ is the capacitance error (either positive or negative). As a result, the simplified model shown in Fig. 17.12 (a) occurs after the switches are reversed. Here, the remaining capacitance equals $\left(\mathrm{C}_{\text {total }} / 2\right)-\Delta \mathrm{C}_{1}$ to make the total capacitance correct. With the above switch operation, $\mathrm{V}_{\mathrm{x}}$ would remain zero if $\Delta \mathrm{C}_{1}$ equals zero. However, when $\Delta \mathrm{C}_{1}$ is not zero, the resulting voltage, $\mathrm{V}_{\mathrm{x}}$, is twice the error voltage, defined as $\mathrm{V}_{\mathrm{el}}$, that would be introduced during a normal successive approximation when $\mathrm{C}_{1}$ alone is switched to $\mathrm{V}_{\text {ref }}$. A digital representation
image_name:Fig. 17.12 Equivalent models for determining capacitance errors
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: b1, Nn: Vref}
name: C2, type: Capacitor, value: C2, NB, ports: {Np: "b2-N,sN", Nn: Vref}
name: OpAmp, type: OpAmp, ports: {InP: GND, InN: Vx, OutP: Out}
name: Switch, type: Switch, ports: {N1: Out, N2: Vx}
]
extrainfo:The circuit is used for determining capacitance errors during calibration for C1 and C2. It involves switching capacitors to Vref and measuring the voltage Vx.

$$
\mathrm{C}_{1}=\left(\frac{\mathrm{C}_{\text {total }}}{2}\right)+\Delta \mathrm{C}_{1}
$$

$$
\mathrm{C}_{2, \mathrm{NB}}=\left(\frac{\mathrm{C}_{\text {total }}}{2}\right)-\Delta \mathrm{C}_{1}
$$

(a)
image_name:Fig. 17.12
description:The circuit is used for determining capacitance errors during calibration for C1 and C2. It involves switching capacitors to Vref and measuring the voltage Vx. The equations for C2 and C3,NB are provided to calculate their values based on Ctotal and the errors ΔC1 and ΔC2.

(b)

Fig. 17.12 Equivalent models for determining capacitance errors. (a) During calibration for $\mathrm{C}_{1}$. (b) During calibration for $\mathrm{C}_{2}$.
of $\mathrm{V}_{\mathrm{el}}$, defined as $\mathrm{DV}_{\mathrm{el}}$, is obtained by doing a successive approximation using the cal-dac shown in Fig. 17.11 and then dividing the resulting digital value by 2 to obtain $\mathrm{DV}_{\mathrm{e} 1}$. This digital correction term, $\mathrm{DV}_{\mathrm{e} 1}$, is stored in the data register for use during regular conversion.

To obtain the similar correction term for $\mathrm{C}_{2}$, defined as $\mathrm{DV}_{\mathrm{e} 2}$, the model in Fig. 17.12(b) is used. Here, the switch procedure is to always leave the $b_{1}$ switch grounded while the comparator is reset, the $b_{2}$ switch is grounded, and the remaining switches $b_{3-N}, s_{N}$ are connected to $V_{\text {ref }}$. Next, the $b_{2}$ and $b_{3-N}, s_{N}$ switches are all reversed (i.e., $b_{2}$ set to $V_{\text {ret }}$ and the others grounded). Note, however, that even if $\Delta C_{2}$ equals zero, the measured value of $V_{x}$ will be equivalent to $-D V_{e 1}$, since $-\Delta C_{1}$ is assumed to be part of $C_{3, \mathrm{NB}}$. Therefore, the error voltage that would be due only to $C_{2}$ can be calculated by digitizing $V_{x}$, as before, but then subtracting off $D V_{e 1}$ using digital circuitry. Mathematically,

$$
\begin{equation*}
D V_{e 2}=\frac{1}{2}\left(D V_{\mathrm{x} 2}-D V_{e 1}\right) \tag{17.29}
\end{equation*}
$$

A similar procedure is used for the other capacitors. Specifically, $\mathrm{DV}_{\mathrm{xi}}$ is found by connecting all capacitors smaller than $C_{i}$ to $V_{\text {ref }}$, and connecting $C_{i}$ and all larger capacitors to ground while the comparator is reset. Next, the comparator is taken out of reset mode, all capacitors smaller than $C_{i}$ are switched to ground, $C_{i}$ is switched to $V_{\text {ref }}$, and all capacitors larger than $C_{i}$ are left connected to ground. $D V_{x i}$ is then found using the cal-dac and successive approximation. $\mathrm{DV}_{\mathrm{ei}}$ is finally calculated using the formula

$$
\begin{equation*}
D V_{e i}=\frac{1}{2}\left(D V_{x i}-\sum_{j=1}^{i-1} D V_{e j}\right) \tag{17.30}
\end{equation*}
$$

and stored in the ${ }_{j}$ th word of the data register.
During a regular conversion, normal successive approximation is performed with the MSB capacitor array; however, appropriate correction voltages are either added or subtracted using the cal-dac and $\mathrm{C}_{\mathrm{NB}}$ capacitor. The proper correction voltage is determined through the use of a digital accumulator that stores the sum of all digital errors of those MSB capacitors deemed to be a 1 (i.e., connected to $V_{\text {ref }}$ ). In other words, when the $i$ th bit is being tested, $\mathrm{DV}_{\text {ei }}$ is added to the digital accumulator that is driving the cal-dac. If the ith bit is determined to be a 0 , then the digital accumulator returns to its previous value; otherwise, it maintains its new accumulated value.

Finally, normal successive approximation is performed using the sub-dac to determine the final LSBs. With this approach, a digital addition must be performed during each bit cycle, and a small amount of digital RAM is required ( 10 bytes in the case of a 10-bit MSB array).

Finally, it should be mentioned that similar error correction techniques have also been described to account for capacitor inaccuracies (for example, [Tan, 1990]).

### 17.2.6 Multi-Bit Successive-Approximation

The successive-approximation converters we have seen so far divide their search space into two on each clock cycle by performing a single comparison. The search can be accelerated by performing multiple comparisons on each clock cycle, and dividing the search space up into smaller regions. For example, if we are trying to guess the value of a random number in the range 1 to 128 , in addition to asking the question "Is the number greater than 64?," imagine that we can simultaneously ask "Is the number greater than 32 ?" and "Is the number greater than 96 ?," With the answers to all three of these questions, we can divide the search space into a quarter: We will know if the number is in the range $1-32,33-64,65-96$, or $97-128$. Hence, we have effectively performed the first two iterations of a binary search. In an analog circuit, this can be done by operating three comparators in parallel. The result is that we require only one-half the number of clock cycles to perform an A/D conversion, hence potentially doubling the converter's sampling rate. However, note that doing so required three comparators (and likely three capacitor banks) instead of only one. A flow graph depicting multi-bit successive-approximation is shown in Fig. 17.13. Naturally, the approach can be extended to perform any number of bits per iteration, but in order to find $L$ bits on each clock cycle, the number of comparisons required $2^{\llcorner }-1$ grows exponentially. Therefore, the number of bits is usually restricted to at most a few.

## 17.3 ALGORITHMIC (OR CYCLIC) A/D CONVERTER

Key Point: Algorithmic converters are similar to successive-approximation converters, except that instead of an accurate D/A converter or capacitor bank, these converters require an accurate gain of two in order to perform the iterative search for a digital code that represents the analog input.

An algorithmic converter operates in much the same way as a succes-sive-approximation converter. However, whereas a successive-approximation converter halves the reference voltage in each cycle, an algorithmic converter doubles the error voltage while leaving the reference voltage unchanged. The flow graph for a signed algorithmic conversion is shown in Fig. 17.14.

### 17.3.1 Ratio-Independent Algorithmic Converter

The block diagram for an algorithmic converter is shown in Fig. 17.15 [McCharles, 1977; Li, 1984]. This converter requires a small amount of analog circuitry because it repeatedly uses the same circuitry to perform its conversion cyclically in time.

One of the difficulties in realizing a high-precision algorithmic converter is building an accurate multiply-by-two gain amp. Fortunately, it is possible to realize the gain amp so that it does not rely on any capacitor matching if four clock cycles are taken for the multiply-by-two operation. The operation of the multiply-by-two gain amp is shown in Fig. 17.16. Although this gain-amp circuitry is shown using single-ended circuits for simplicity, fully differential circuits are normally used.

The basic idea of this gain amp is to sample the input signal twice using the same capacitor. During the second sampling, the charge from the first capacitor is stored on a second capacitor whose size is unimportant. After the second sampling, both charges are recombined into the first capacitor which is then connected between the opamp input and output.
image_name:Fig. 17.13
description:The diagram in Fig. 17.13 is a flow graph representing a 2-bit per iteration successive approximation process for analog-to-digital conversion (ADC). It illustrates the steps and decision points involved in converting an analog signal into a digital output in a systematic manner.

1. **Main Components:**
- **Start and Stop Blocks:** Indicate the beginning and end of the process.
- **Sample Block:** Captures the input voltage, \( V_{in} \), and initializes the iteration index \( i \) to 1.
- **Decision Blocks:** Compare the sampled voltage \( V \) against scaled reference voltages \( V_{ref} \), guiding the bit assignment and voltage adjustment.
- **Assignment Blocks:** Assign binary values to the bits \( b_i, b_{i+1} \) based on comparisons.
- **Update Blocks:** Modify the voltage \( V \) based on the assigned bits and reference voltage adjustments.

2. **Flow of Information or Control:**
- The process begins by sampling the input voltage \( V = V_{in} \).
- The sampled voltage is compared against \( \frac{V_{ref}}{2^{i+1}} \) and \( -\frac{V_{ref}}{2^{i+1}} \) to determine the binary output bits \( b_i, b_{i+1} \).
- Depending on the results of these comparisons, the bits are assigned values (\( 11, 10, 01, \) or \( 00 \)) and the voltage \( V \) is updated accordingly.
- The index \( i \) is then incremented by 2, and the process repeats until \( i > N \), where \( N \) is the total number of bits.

3. **Labels, Annotations, and Key Indicators:**
- The input is labeled as "Signed input," indicating that the process can handle negative voltages.
- Each decision and update block is annotated with mathematical expressions showing how the voltage \( V \) is adjusted.
- Bit assignments are explicitly shown with binary representations.

4. **Overall System Function:**
- This flow graph outlines a method for performing a 2-bit per iteration successive approximation ADC. The system efficiently converts an analog voltage into a digital value by iteratively sampling, comparing, and adjusting the input voltage. Each iteration refines the approximation of the input signal, ultimately producing a digital representation of the analog input. The use of 2-bit per iteration allows for faster conversion compared to single-bit approaches.

Fig. 17.13 Flow graph for a 2-bit per iteration successive approximation.

#### EXAMPLE 17.5

Consider the multiply-by-two gain circuitry shown in Fig. 17.16. Assuming the opamp has an input offset designated as $\mathrm{V}_{\text {off }}$, find the values of $\mathrm{V}_{\mathrm{C}_{1}}, \mathrm{~V}_{\mathrm{C}_{2}}$, and $\mathrm{V}_{\text {out }}$ at the end of each of the phases shown.

#### Solution

During phase one, the opamp output, $\mathrm{V}_{\text {out }}$, is connected to the negative opamp input, resulting in

$$
\begin{equation*}
V_{\text {out }}=V_{\text {off }} \tag{17.31}
\end{equation*}
$$

and the voltages across the two capacitors are

$$
\begin{gather*}
\mathrm{V}_{\mathrm{C} 1}=\mathrm{V}_{\mathrm{err}}-\mathrm{V}_{\text {off }}  \tag{17.32}\\
\mathrm{V}_{\mathrm{C} 2}=0-\mathrm{V}_{\text {off }}=-\mathrm{V}_{\text {off }} \tag{17.33}
\end{gather*}
$$

image_name:Fig. 17.14
description:The block diagram in Fig. 17.14 represents a flow graph for an algorithmic and pipelined converter approach. It begins with a "Start" block, indicating the initiation of the process. The first operation is to sample the input voltage, labeled as \( V = V_{in} \), with an initial index \( i = 1 \). This is done in the "Sample \( V = V_{in}, i = 1 \)" block.

The next decision block checks if the sampled voltage \( V \) is greater than zero (\( V > 0 \)). If the condition is true (Yes branch), the binary output \( b_i \) is set to 1. If false (No branch), \( b_i \) is set to 0. This decision point determines the subsequent voltage transformation.

For the Yes branch, the voltage is updated according to the formula \( V \rightarrow 2(V - V_{ref}/4) \). For the No branch, the voltage is updated as \( V \rightarrow 2(V + V_{ref}/4) \). These transformations adjust the voltage based on whether the current sampled voltage is positive or not, incorporating a reference voltage \( V_{ref} \).

Following the voltage transformation, the index \( i \) is incremented by 1 (\( i \rightarrow i + 1 \)).

The process then checks if the index \( i \) has exceeded a predefined number \( N \) (\( i > N \)). If \( i \) is greater than \( N \) (Yes branch), the process stops. If not (No branch), the process loops back to the decision block to check the updated voltage \( V \) again.

This flow graph effectively describes a repetitive sampling and decision-making process typical of algorithmic converters, where successive approximations are made to refine the output based on the input voltage and reference voltage.

Fig. 17.14 Flow graph for the algorithmic and pipelined converter approach.

At the end of phase two, we have

$$
\begin{equation*}
V_{C 1}=0-V_{\text {off }}=-V_{\text {off }} \tag{17.34}
\end{equation*}
$$

implying that its charge change was

$$
\begin{equation*}
\Delta Q_{C 1}=C_{1}\left(V_{\text {err }}-V_{\text {off }}-\left(-V_{\text {off }}\right)\right)=C_{1} V_{\text {err }} \tag{17.35}
\end{equation*}
$$

All this charge is placed on $\mathrm{C}_{2}$, resulting in

$$
\begin{equation*}
\mathrm{V}_{\mathrm{C} 2}=-\mathrm{V}_{\mathrm{off}}+\left(\frac{\mathrm{C}_{1}}{\mathrm{C}_{2}}\right) \mathrm{V}_{\mathrm{err}} \tag{17.36}
\end{equation*}
$$

and $V_{\text {out }}=\left(C_{1} / C_{2}\right) V_{\text {err }}$.
At the end of phase three, $\mathrm{V}_{\mathrm{C} 2}$ remains unchanged since one side of it has been opened. Also, $\mathrm{V}_{\mathrm{C} 1}=\mathrm{V}_{\text {err }}-\mathrm{V}_{\text {off }}$ and $\mathrm{V}_{\text {out }}=\mathrm{V}_{\text {off }}$ as in phase one.
image_name:Fig. 17.15 Algorithmic converter.
description:The system block diagram labeled "Fig. 17.15 Algorithmic converter" represents an algorithmic analog-to-digital converter (ADC) system. It consists of the following main components:

1. **Input Voltage (V_in):** This is the initial input signal to the system. It is connected to a node labeled V_i, which acts as the input to the comparator.

2. **Comparator (Cmp):** The comparator is used to compare the input voltage V_i against a reference voltage. It outputs a binary signal (b_i) based on this comparison. If V_i is greater than the reference, the output is typically a high signal; otherwise, it is low.

3. **MDAC (Multiplying Digital-to-Analog Converter):** This block processes the output of the comparator. It consists of a summing junction and an amplifier. The summing junction takes the comparator's output and either adds or subtracts a fraction (V_ref/4) of the reference voltage (V_ref) based on the comparator's decision. The resulting signal is then multiplied by 2 using an amplifier, producing the next stage input voltage V_{i+1}.

4. **Feedback Loop:** The output V_{i+1} is fed back into the input node V_i, creating a feedback loop that allows the system to iteratively process the input signal. This feedback mechanism is crucial for the algorithmic conversion process.

5. **Shift Register:** The binary output from the comparator (b_i) is stored in a shift register. This component collects the sequence of bits generated during the conversion process and outputs the final digital representation of the analog input signal.

6. **Output:** The final digital output of the system is taken from the shift register, representing the digitized version of the input analog signal.

**Flow of Information:**
- The input voltage V_in is applied to the system and compared to a reference voltage by the comparator.
- The comparator outputs a binary signal b_i, which is used by the MDAC to adjust the input voltage for the next iteration.
- The MDAC processes the signal, amplifies it, and feeds it back into the system, creating a loop that iteratively refines the conversion.
- The shift register collects the binary outputs from each iteration, forming the final digital output.

**Overall System Function:**
This algorithmic converter is designed to convert an analog input voltage into a corresponding digital output. The iterative process of comparison, adjustment, and feedback allows for precise conversion, with the shift register compiling the sequence of binary decisions into a complete digital representation of the input signal.

Fig. 17.15 Algorithmic converter.

Finally, at the end of phase four, $\mathrm{C}_{2}$ is discharged to the same value it had in phase 1, resulting in $\mathrm{V}_{\mathrm{C} 2}=-\mathrm{V}_{\text {off }}$ and its change in charge being

$$
\begin{equation*}
\Delta \mathrm{Q}_{\mathrm{C} 2}=\mathrm{C}_{2}\left(\frac{\mathrm{C}_{1}}{\mathrm{C}_{2}}\right) \mathrm{V}_{\mathrm{err}}=\mathrm{C}_{1} \mathrm{~V}_{\mathrm{err}} \tag{17.37}
\end{equation*}
$$

All of this charge is placed back on $C_{1}$, resulting in

$$
\begin{equation*}
\mathrm{V}_{\mathrm{C} 1}=2 \mathrm{~V}_{\mathrm{err}}-\mathrm{V}_{\mathrm{off}} \tag{17.38}
\end{equation*}
$$

and the output voltage being the desired result of $\mathrm{V}_{\text {out }}=2 \mathrm{~V}_{\text {err }}$. Note that this final result is independent of the sizes of $\mathrm{C}_{1}, \mathrm{C}_{2}$, and the offset value, $\mathrm{V}_{\text {off }}$.

## 17.4 PIPELINED A/D CONVERTERS

Pipelined converters, like successive-approximation and algorithmic converters, perform an iterative search for a digital code that accurately reflects the analog input signal. However, rather than perform the iterations with a single analog circuit, pipelined converters have a separate analog stage dedicated to performing each iteration. Signal flow in a pipelined converter is diagrammed in Fig. 17.17. All of the analog stages operate on every clock cycle, each operating on a different input sample. Since N iterations are performed simultaneously, the pipelined converter operates N -times faster than algorithmic converters and is capable of

Key Point: Pipelined $A / D$ converters are similar to algorithmic converters, but employ multiple circuits working on successive input samples simultaneously. Hence, they can complete a conversion on every clock cycle, providing higher throughput than algorithmic converters, but with the same latency.
outputting one conversion on every clock cycle. Therefore, pipelined converters are generally applied when higher speed is desired than is achievable with algorithmic converters. Although N input samples are being processed in parallel, N clock cycles are required for each input sample to proceed through the entire pipeline. Hence, there is a latency of $N$ clock cycles through pipelined converters, just as in algorithmic and successive approximation converters.
image_name:Sample remainder and cancel input-offset voltage
description:The circuit samples the remainder and cancels input-offset voltage using capacitors C1 and C2, an operational amplifier (Q1), and a comparator (Cmp). The input voltage Verr is processed through the op-amp and capacitors to produce an output for comparison.

1. Sample remainder and cancel input-offset voltage.
image_name:Fig. 17.16
description:The circuit samples the remainder and cancels input-offset voltage using capacitors C1 and C2, an operational amplifier (Q1), and a comparator (Cmp). The input voltage Verr is processed through the op-amp and capacitors to produce an output for comparison.

2. Transfer charge $Q_{1}$ from $C_{1}$ to $C_{2}$.
image_name:Fig. 17.16
description:The circuit is designed to sample the input voltage Verr and process it through capacitors C1 and C2, an operational amplifier, and a comparator. It transfers charge between the capacitors and cancels input-offset voltage, producing an output for comparison. It is part of a multiply-by-two gain circuitry for an algorithmic converter that does not rely on capacitor matching.

3. Sample input signal with $C_{1}$ again, after storing charge $Q_{1}$ on $C_{2}$.
image_name:Multiply-by-two gain circuitry
description:The circuit is a multiply-by-two gain circuitry for an algorithmic converter that does not depend on capacitor matching. It samples the input voltage Verr, processes it through capacitors C1 and C2, an operational amplifier, and a comparator. The circuit transfers charge between the capacitors, cancels input-offset voltage, and produces an output for comparison. The output voltage is twice the input voltage, Vout = 2 * Verr.

4. Combine $Q_{1}$ and $Q_{2}$ on $C_{1}$, and connect $C_{1}$ to output.

Fig. 17.16 Multiply-by-two g ain circuitry for an algo rithmic converter that does not depend on capacitor matching.
image_name:Fig. 17.17
description:The diagram illustrates the signal flow in a pipelined Analog-to-Digital (A/D) converter, specifically focusing on the sequential processing of input signals through multiple stages. The diagram is structured to show three primary stages: Stage #1, Stage #2, and Stage #3, with the possibility of additional stages extending beyond Stage #3, as indicated by ellipses.

Main Components:
1. **Stages:**
- Each stage is represented by a vertical column of blocks. The stages are labeled as Stage #1, Stage #2, Stage #3, and potentially more.
- Each block within a stage is responsible for processing a specific input signal at a given time.

2. **Input Signals:**
- The input signals are labeled as \( V_{in}(k) \), \( V_{in}(k+1) \), \( V_{in}(k+2) \), etc., representing a sequence of input samples over time.
- These signals are processed sequentially through the pipeline stages.

Flow of Information:
- The diagram shows a vertical flow of time, indicating that signals are processed in a time-sequential manner.
- Each input signal \( V_{in}(k) \), \( V_{in}(k+1) \), \( V_{in}(k+2) \), etc., enters Stage #1 and moves horizontally to the next stages (Stage #2, Stage #3, etc.) as time progresses.
- The arrows between blocks indicate the direction of signal flow from one stage to the next.

Labels and Annotations:
- The input signals are clearly labeled with their respective time indices (e.g., \( V_{in}(k) \), \( V_{in}(k+1) \)).
- Stages are labeled numerically to indicate the order of processing.

Overall System Function:
- The primary function of this pipelined A/D converter is to process multiple input signals in a sequential and parallel manner, allowing for efficient conversion of analog signals to digital form.
- Each stage processes a different sample of the input signal at any given time, enabling high throughput by overlapping the processing of different samples across multiple stages.
- This pipelined approach reduces latency and increases the conversion speed compared to single-stage converters, making it suitable for high-speed applications.

Fig. 17.17 The signal flow in a pipelined A/D converter.
image_name:Fig. 17.18
description:The diagram represents a one-bit-per-stage pipelined A/D converter stage. It includes a comparator (Cmp) and a multiplying digital-to-analog converter (MDAC) with a gain of 2. The input voltage range is from -Vref/2 to Vref/2. The output of the comparator (bi) determines the next stage's input (Vi+1). The graph illustrates the transfer characteristics of the stage.
image_name:Fig. 17.17
description:The graph depicted in Fig. 17.17 illustrates the signal flow in a pipelined analog-to-digital converter (A/D converter). It is a schematic diagram rather than a traditional graph with axes, focusing on the operational flow of signals through the converter stages.

1. **Type of Graph and Function:**
- This is a block diagram representing the function and signal flow in a pipelined A/D converter stage.

2. **Axes Labels and Units:**
- There are no traditional axes with labels or units as it is a schematic representation. Instead, it shows signal paths and operational blocks.

3. **Overall Behavior and Trends:**
- The diagram shows the flow of an input voltage \( V_i \) through a comparator (Cmp) and a multiplying digital-to-analog converter (MDAC) block. The input voltage \( V_i \) is compared to a reference voltage to generate a digital output \( b_i \) and an intermediate analog output \( V_{i+1} \).

4. **Key Features and Technical Details:**
- **Comparator (Cmp):** Compares the input voltage \( V_i \) against a reference voltage and outputs a digital bit \( b_i \).
- **MDAC Block:** Consists of a summing amplifier and a gain stage (indicated by the multiplication symbol \( \times 2 \)). It adjusts the analog signal based on the comparator's output and the reference voltage \( V_{\text{ref}} \).
- **Voltage Range:** The input voltage \( V_i \) is expected to be within the range \( -V_{\text{ref}}/2 < V_i < V_{\text{ref}}/2 \).

5. **Annotations and Specific Data Points:**
- The diagram includes reference voltage levels \( V_{\text{ref}}/4 \) and \( V_{\text{ref}} \) used within the MDAC block.
- The output voltage \( V_{i+1} \) is shown to vary linearly with \( V_i \) in the range from \( -V_{\text{ref}}/2 \) to \( +V_{\text{ref}}/2 \), with a doubling effect due to the gain stage.

Overall, the diagram provides a clear representation of how a one-bit-per-stage pipelined converter processes an input signal, leveraging a comparator and MDAC to achieve efficient analog-to-digital conversion.

Fig. 17.18 One-bit pipelined converter stage that accepts inputs in the range $-\mathrm{V}_{\text {ref }} / 2<\mathrm{V}_{\mathrm{i}}<\mathrm{V}_{\text {ref }} / 2$.

### 17.4.1 One-Bit-Per-Stage Pipelined Converter

The operations performed in each stage of a one-bit-per-stage pipelined converter are the same as those for the algorithmic converter shown in Fig. 17.14. Each stage accepts an input from the previous stage, compares it to a reference threshold, and uses a multiplying D/A converter (MDAC) to form a residue signal as follows:

$$
\begin{equation*}
\mathrm{V}_{\mathrm{i}+1}=2\left[\mathrm{~V}_{\mathrm{i}}+\left(\mathrm{b}_{\mathrm{i}}-0.5\right) \mathrm{V}_{\mathrm{ref}} / 2\right] \tag{17.39}
\end{equation*}
$$

The block diagram of a single stage is in Fig. 17.18. It's functionality is very similar to that of the algorithmic converter in Fig. 17.15 except rather than returning the resulting Since a single comparison is performed in each stage, each finds a single bit of the result, $b_{i}$. However, since each stage is operating on a different input sample, these digital bits must be realigned using shift registers of varying lengths, as shown in Fig. 17.19. The result of the conversion may be interpreted as a N -bit quantized estimate of the original input sample within the range $\pm \mathrm{V}_{\text {ref }} / 2$,

$$
\begin{equation*}
\hat{V}_{i n}=V_{\text {ref }} \sum_{i=1}^{N}\left(b_{i}-0.5\right) 2^{-i} \tag{17.40}
\end{equation*}
$$

Finally, note that the final residue signal $\mathrm{V}_{\mathrm{N}+1}$ is not used by any subsequent stage so there is no need to generate it. Hence the final MDAC may be omitted and the last stage is simply a 1-bit $\mathrm{A} / \mathrm{D}$ converter (comparator) generating $b_{N}$.
image_name:Fig. 17.19 A one-bit-per-stage pipelined A/D converter
description:The system block diagram illustrates a one-bit-per-stage pipelined Analog-to-Digital (A/D) converter. This type of converter processes an input voltage \( V_{in} \) through a series of stages, each contributing one bit to the final digital output.

Main Components:
1. **1-bit Stage Blocks:**
- These are the primary processing units in the pipeline. Each stage receives an analog input voltage, processes it, and generates a digital bit output (\( b_i \)).
- The stages are responsible for generating intermediate residue voltages (\( V_2, V_3, \ldots, V_N \)) that are passed to the next stage in the pipeline.

2. **1-bit A/D Converter (Comparator):**
- The final stage is a simple 1-bit A/D converter that acts as a comparator. It generates the last bit (\( b_N \)) of the digital output.

3. **Shift Register (N-1-bit):**
- This component collects the bits generated by each stage (\( Q_1, D_1, \ldots, Q_{N-1}, D_{N-1} \)) and shifts them to produce the final digital output sequence (\( b_1, b_2, \ldots, b_{N-1} \)).

Flow of Information:
- **Input:** The input voltage \( V_{in} = V_1 \) is fed into the first 1-bit stage.
- **Processing:** Each 1-bit stage processes its input voltage to produce a digital bit and a residue voltage, which is passed to the next stage.
- **Output:** The final stage outputs the last bit \( b_N \) directly, while other bits are shifted through the register to form the complete digital output sequence \( b_1, b_2, \ldots, b_N \).

Labels and Annotations:
- **\( V_{in} = V_1 \):** Denotes the initial input voltage to the pipeline.
- **\( V_2, V_3, \ldots, V_N \):** Intermediate residue voltages between stages.
- **\( b_1, b_2, \ldots, b_N \):** Output digital bits.

Overall System Function:
The primary function of this pipelined A/D converter is to digitize an analog input voltage by processing it through multiple stages, each contributing a single bit to the final digital output. The pipeline architecture allows for high-speed conversion by enabling simultaneous processing of multiple samples at different stages. The shift register ensures proper sequencing of the output bits to form a coherent digital representation of the input signal.

Fig. 17.19 A one-bit-per-stage pipelined A/D converter [Martin, 1981].

#### EXAMPLE 17.6

Consider the operation of a 3-bit, one-bit-per-stage pipelined converter with $\mathrm{V}_{\text {ret }}=1 \mathrm{~V}$. Find all of the residue voltages, $\mathrm{V}_{\mathrm{i}}$, and the final output digital code for a sampled input voltage of $\mathrm{V}_{\mathrm{in}}=240 \mathrm{mV}$.

#### Solution

The input signal is given, $\mathrm{V}_{1}=\mathrm{V}_{\mathrm{in}}=240 \mathrm{mV}$. The comparator in the first pipelined stage will output a positive result, $b_{1}=1$. It will, therefore, subtract $V_{\text {ref }} / 4=250 \mathrm{mV}$ from its input and multiply the result by two.

$$
V_{2}=2\left(V_{1}-V_{\text {ref }} / 4\right)=-20 \mathrm{mV}
$$

Since $\mathrm{V}_{2}<0$, in the next clock cycle the comparator of the second pipelined stage will produce a logic low result, $\mathrm{b}_{2}=0$, causing $\mathrm{V}_{\text {ref }} / 4$ to be added for the next residue.

$$
V_{3}=2\left(V_{2}+V_{\text {ref }} / 4\right)=460 \mathrm{mV}
$$

Finally, the third stage will output a high logic level resulting in a final output code of $b_{1} b_{2} b_{3}=101$ equivalent to a quantized input of $\hat{V}_{\text {in }}=187.5 \mathrm{mV}$.

A problem with the one-bit-per-stage pipelined architecture is that any comparator offset results in irreparable errors. In order for a one bit per stage pipelined converter to have $10-\mathrm{mV}$ resolution, the first stage comparator must have better than $10-\mathrm{mV}$ accuracy, the second stage accuracy must be better than 20 mV , the third stage better than 40 mV , and so on. The accuracy requirements diminish as one proceeds along the pipeline since later stages are acting on amplified residue signals, so their impact on the converter's overall accuracy is divided by all of the preceding gain stages when input-referred. Nevertheless, the limitations imposed by comparator offsets mean that the one bit per stage pipeline architecture is rarely used.

#### EXAMPLE 17.7

Repeat Example 17.6, but this time assume that the comparator in the second stage has an offset of 30 mV .

#### Solution

As in Example 17.6, the comparator in the first pipelined stage will output a positive result, $b_{1}=1$, resulting in $\mathrm{V}_{2}=-20 \mathrm{mV}$. This time, however, the second stage comparator offset will cause the second pipelined stage to produce a logic high result, $\mathrm{b}_{2}=1$, causing $\mathrm{V}_{\mathrm{ref}} / 4$ to be subtracted for the next residue.

$$
\mathrm{V}_{3}=2\left(\mathrm{~V}_{2}-\mathrm{V}_{\mathrm{ref}} / 4\right)=-540 \mathrm{~V}
$$

This residue is outside the range $\pm \mathrm{V}_{\text {ref }} / 2$ and therefore results in an excess error in the converter's final result. The final stage will output a logic low resulting in the output code: $\mathrm{b}_{1} \mathrm{~b}_{2} \mathrm{~b}_{3}=110$ or $\mathrm{V}_{\mathrm{in}}=375 \mathrm{mV}$, a less accurate result than the output produced without offset in Example 17.6.

### 17.4.2 1.5 Bit Per Stage Pipelined Converter

Adding a second comparator to each stage of a pipelined converter results in the $1.5-$ bit $^{1}$ stage architecture shown in Fig. 17.20 [Lewis, 1992]. Each stage effectively performs a 3-level quantization of its input,

$$
\begin{equation*}
V_{i, x}=\left(b_{i, 0}-0.5\right) \frac{V_{\text {ref }}}{4}+\left(b_{i, 1}-0.5\right) \frac{V_{\text {ref }}}{4}=\left(b_{i, 0}+b_{i, 1}-1\right) \frac{V_{\text {ref }}}{4} \tag{17.41}
\end{equation*}
$$

This estimate is then subtracted from the input and scaled by $2 \times$ to form the residue $\mathrm{V}_{i+1}$. Equation (17.41) shows that both $b_{i, 0}$ and $b_{i, 1}$ contribute $\pm V_{\text {ref }} / 4$ to the residue and therefore they are weighted equally in determining the converter's digital output. The final stage of is typically a simple two-bit $\mathrm{A} / \mathrm{D}$, since no residue is needed. Assuming the final stage has a two-bit output whose MSB and LSB are $b_{N-1,1}$ and $b_{N-1,0}$ respectively, the final quantized signal is

$$
\begin{equation*}
\hat{V}_{i n}=\frac{V_{\mathrm{ref}}}{2}\left(\sum_{\mathrm{i}=1}^{\mathrm{N}-2}\left(\mathrm{~b}_{\mathrm{i}, 0}+\mathrm{b}_{\mathrm{i}, 1}-1\right) 2^{-\mathrm{i}}+\mathrm{b}_{\mathrm{N}-1,1} 2^{\mathrm{N}-2}+\mathrm{b}_{\mathrm{N}-1,0} 2^{\mathrm{N}-1}\right) \tag{17.42}
\end{equation*}
$$

The output bits of all stages are converted into the final output code by addition with the proper binary weighting, as in (17.42). Of course, prior to addition, the outputs of all stages must be delayed by varying length shift registers to realign the bits in time, as shown in Fig. 17.21.

[^1]image_name:MDAC
description:This is a 1.5-bit pipelined ADC stage with redundancy to mitigate comparator offsets. The MDAC (Multiplying Digital-to-Analog Converter) is used to generate the output voltage Vi+1 by combining the comparator outputs bi,1 and bi,0 with weighted voltages. The graph illustrates the ideal and offset-affected input-output relationships.
image_name:(a)
description:The graph labeled "(a)" is a plot depicting the ideal input-output relationship for a 1.5-bit pipelined converter stage. It is a piecewise linear function that maps the input voltage $V_i$ to the output voltage $V_{i+1}$.

1. **Type of Graph and Function:**
- This is a piecewise linear graph that represents the transfer characteristic of an analog-to-digital converter stage.

2. **Axes Labels and Units:**
- The horizontal axis is labeled $V_i$, representing the input voltage.
- The vertical axis is labeled $V_{i+1}$, representing the output voltage.
- The voltage is marked in terms of $V_{\text{ref}}$, the reference voltage, with divisions at $\pm V_{\text{ref}}/2$, $\pm V_{\text{ref}}/4$, and $\pm V_{\text{ref}}/8$.

3. **Overall Behavior and Trends:**
- The graph consists of three linear segments that create a zigzag pattern.
- For $V_i$ between $-V_{\text{ref}}/2$ and $V_{\text{ref}}/2$, the output $V_{i+1}$ changes linearly, indicating a proportional relationship.
- The slope of each segment is positive, showing that as $V_i$ increases, $V_{i+1}$ also increases.

4. **Key Features and Technical Details:**
- The middle segment of the graph is centered around $V_i = 0$ and extends between $-V_{\text{ref}}/4$ and $V_{\text{ref}}/4$ on the output axis.
- The outer segments extend to $\pm V_{\text{ref}}/2$ on the output axis.
- The transitions between segments occur at $V_i = \pm V_{\text{ref}}/8$.

5. **Annotations and Specific Data Points:**
- The graph is symmetric around the origin, indicating that the converter handles both positive and negative inputs similarly.
- No specific numerical values or annotations are provided beyond the reference voltage divisions.
image_name:(b)
description:The graph labeled (b) is a piecewise linear function representing the input-output relationship of a 1.5-bit pipelined converter stage in the presence of comparator offset. The graph plots the input voltage $V_i$ on the horizontal axis and the output voltage $V_{i+1}$ on the vertical axis. Both axes are marked with reference voltage levels, specifically $+V_{\text{ref}}/2$, $+V_{\text{ref}}/4$, $-V_{\text{ref}}/4$, and $-V_{\text{ref}}/2$.

The graph consists of three distinct linear segments, each with a positive slope, indicating a proportional relationship between the input and output voltages. The central segment is horizontally shifted slightly due to the presence of comparator offsets, denoted as $\varepsilon_0$ and $\varepsilon_1$. These offsets cause the central segment to deviate from the ideal alignment, introducing small horizontal shifts in the transition points between segments.

Key features of the graph include:
- The central segment, which ideally should pass through the origin, is shifted horizontally, indicating the effect of the comparator offsets.
- Transition points at $V_{\text{ref}}/8$ and $-V_{\text{ref}}/8$ are displaced by the offsets $\varepsilon_0$ and $\varepsilon_1$.
- The graph illustrates how the output voltage $V_{i+1}$ varies linearly with the input voltage $V_i$ within each segment, but with shifts due to the offsets.

This graph is crucial for understanding how comparator offsets affect the linearity and accuracy of the pipelined converter stage, highlighting the robustness of the 1.5-bit architecture in compensating for such offsets.

Fig. 17.20 A 1.5-bit pipelined converter stage that accepts inputs in the range $-\mathrm{V}_{\text {ref }} / 2<\mathrm{V}_{\mathrm{i}}<\mathrm{V}_{\text {ref }} / 2$. (a) The ideal input-output relationship. (b) The input-output relationship in the presence of comparator offset.

Although the 1.5 bit per stage architecture entails some digital decoding logic, its redundancy makes the converter robust to comparator offsets. The impact of random comparator offsets $\varepsilon_{0}, \varepsilon_{1}$ on the pipeline stage's input-output relationship is shown in Fig. 17.20(b). Intuitively the offsets will, for some input levels, introduce an error of $\pm V_{\text {ref }} / 4$ into $V_{i, x}$ which is reflected in the values of $b_{i, 0}$ and $b_{i, 1}$. They also result in an error of $\mp \mathrm{V}_{\text {ref }} / 2$ in $\mathrm{V}_{\mathrm{i}+1}$, which is captured by the output bits of subsequent stages in the pipeline. When all bits are combined by the decoder (17.42)

Key Point: Introducing redundancy between successive stages in a pipelined converter permits simple digital correction of any offset in the comparators of each stage.
the errors cancel, as long as $\left|\varepsilon_{0,1}\right|<\mathrm{V}_{\text {ref }} / 4$ so that the residue remains within the range $\pm \mathrm{V}_{\text {ref }} / 2$. This argument is inductive; comparator offsets in all 1.5 bit stages are cancelled by subsequent stages. Only offsets in the final stage are left uncanceled. Fortunately, such offsets influence only the converter's 2 LSBs, and are therefore rarely a significant limitation in the design of pipelined converters.

Errors introduced in the MDAC generally limit the performance of pipelined converters. For example, mismatch resulting in errors the DAC voltages $\pm \mathrm{V}_{\text {ref }} / 4$, inaccuracy in the $2 \times$ gain, and thermal noise in the MDAC appear in the residue $V_{i+1}$ but not the comparator outputs $b_{i, 0}$ and $b_{i, 1}$, and are therefore not cancelled. The impact of such errors is greatest at the start of the pipeline, in stage 1 where they influence the converter's most significant bits. Therefore, the first stage is normally designed to be the larger and consume more

Key Point: Pipelined $A / D$ converter performance is limited by nonlinearities and noise in the MDAC, and inaccuracy in the interstage gain, none of which are cancelled by simple digital correction.
power than subsequent stages in order to minimize its mismatch and noise.
image_name:Fig. 17.21 A 1.5-bit-per-stage pipelined A/D converter
description:The diagram illustrates a 1.5-bit-per-stage pipelined analog-to-digital (A/D) converter, which is a multi-stage system designed to convert an analog input voltage \( V_{in} = V_1 \) into a digital output. The system is organized into several key components and stages, each contributing to the conversion process.

Main Components:
1. **1.5-bit Stages:**
- Each stage processes the input voltage and generates a residue voltage (e.g., \( V_2, V_3, \ldots, V_{N-1} \)).
- Each stage also produces a 1.5-bit digital output (e.g., \( b_{1,1}b_{1,0}, b_{2,1}b_{2,0}, \ldots, b_{N-2,1}b_{N-2,0} \)).

2. **Shift Register (N-2-deep):**
- Captures and shifts the digital outputs from each stage (e.g., \( Q_1, D_1, Q_{N-3}, D_{N-3}, \ldots \)).

3. **2-bit A/D Converter:**
- The final stage that converts the last residue voltage \( V_{N-1} \) into a 2-bit digital output.

4. **Digital Decoder:**
- Combines the outputs from all stages into a final digital output \( b_1, b_2, \ldots, b_N \), using weighted summation (e.g., \( 2^{-2}, 2^{-3}, 2^{N+1} \)).

Flow of Information or Control:
- The analog input voltage \( V_{in} \) enters the first 1.5-bit stage.
- Each stage processes the input voltage, generates a digital output, and passes a residue voltage to the next stage.
- The digital outputs from each stage are fed into a shift register, which organizes them for input to the digital decoder.
- The final 2-bit A/D converter processes the last residue voltage, contributing its output to the digital decoder.
- The digital decoder then combines all the digital outputs to form the final digital output, utilizing weighted summation to ensure proper bit significance.

Labels, Annotations, and Key Indicators:
- The stages are labeled with their respective outputs (e.g., \( V_2, V_3, \ldots, V_{N-1} \)).
- The digital outputs from each stage are labeled with their bit significance (e.g., \( b_{1,1}b_{1,0}, b_{2,1}b_{2,0} \)).
- The digital decoder's output is labeled with the final bit sequence \( b_1, b_2, \ldots, b_N \).

Overall System Function:
The primary function of this pipelined A/D converter is to efficiently convert an analog input signal into a digital output using a staged approach. Each 1.5-bit stage refines the conversion, passing residue voltages to subsequent stages, while the digital outputs are organized and combined by the shift register and digital decoder to form the final digital representation. This architecture allows for high-speed conversion with reduced complexity in each stage, leveraging the pipeline effect for enhanced performance.

Fig. 17.21 A 1.5-bit-per-stage pipelined A/D converter.

#### EXAMPLE 17.8

Consider the operation of a 3-bit, 1.5-bit-per-stage pipelined converter. Take $\mathrm{V}_{\text {ret }}=1 \mathrm{~V}$ and $\mathrm{V}_{\text {in }}=150 \mathrm{mV}$. Find the residue voltage, $\mathrm{V}_{2}$, the digital codes at the outputs of each stage, and the final digital output after decoding. Then, repeat the exercise assuming the upper comparator of stage 1 has an offset of 30 mV .

#### Solution

In the absence of comparator offset, the digital outputs of stage 1 will be $b_{1,1}=1$ and $b_{1,0}=1$ and the DAC output is $\mathrm{V}_{1, \mathrm{x}}=\mathrm{V}_{\text {ret }} / 4=250 \mathrm{mV}$ and a residue of

$$
\mathrm{V}_{2}=2\left(\mathrm{~V}_{1}-\mathrm{V}_{1 \mathrm{x}}\right)=-200 \mathrm{mV}
$$

This is input to the final stage, a 2-bit $\mathrm{A} / \mathrm{D}$ having a full-scale range of $\pm \mathrm{V}_{\text {ref }} / 2= \pm 500 \mathrm{mV}$. Its binary output is $(01)_{2}$. Hence, the digital code at the output of the decoder is computed as follows:

| $\mathrm{b}_{1,1}:$ | 1 |
| ---: | :---: |
| $\mathrm{~b}_{1,0}:$ | 1 |
| $\mathrm{~b}_{2,1} \mathrm{~b}_{2,0}:$ | 01 |
| $\mathrm{~b}_{1} \mathrm{~b}_{2} \mathrm{~b}_{3}:$ | 101 |

Next, consider what happens if the upper comparator of the first stage has a $30-\mathrm{mV}$ offset, sufficient to cause a error in its output: $\mathrm{b}_{1,1}=0$. As a result, $\mathrm{V}_{1, \mathrm{x}}=0$ and the residue becomes

$$
V_{2}=300 \mathrm{mV}
$$

The binary output of the final-stage 2-bit A/D therefore becomes $(11)_{2}$. The following addition is performed by the decoder:

\begin{aligned} $\mathrm{b}_{1,1}: & 0 \\ \mathrm{~b}_{1,0}: & 1 \\ \mathrm{~b}_{2,1} \mathrm{~b}_{2,0}: & 11 \\$\hline $\mathrm{~b}_{1} \mathrm{~b}_{2} \mathrm{~b}_{3}: & 101\end{aligned}

The error in the first stage is captured by the following stage resulting in the same decoder output as in the ideal case.

### 17.4.3 Pipelined Converter Circuits

Key Point: Switching part of the sampling capacitor into the feedback network provides the interstage gain with a higher feedback factor, and hence higher bandwidth, than a conventional switched-capacitor gain circuit.

The most common implementation of the 1.5 bit stage is shown in Fig. 17.22 [Sutarja, 1988], although fully-differential implementations are used in most high-performance applications. In the first clock phase, the input $\mathrm{V}_{\mathrm{i}}$ is sampled on the total capacitance 2C, Fig. 17.22(a). Then in the second clock phase, Fig. 17.22(b), one-half of the total capacitance is switched to become the feedback capacitance. Reusing the sampling capacitance in this way realizes a gain of 2 with a feedback factor of $\beta=1 / 2$ in Fig. 17.22(b). In a conventional switched-capacitor gain stage, a separate feedback capacitance C is used in addition to the 2 C input sampling capacitance resulting in the lower feedback factor $\beta=1 / 3$ and, hence, lower closed-loop bandwidth and a lower maximum clock frequency.

The other one-half of the sampling capacitance is split into two $\mathrm{C} / 2$ capacitors and reused as a charge redistribution D/A converter during the second clock phase, Fig. 17.22(b). The 1.5 -bit code $b_{i, 1}, b_{i, 0}$ serves as the digital input to the $\mathrm{D} / \mathrm{A}$ and introduces a net change of $\pm \mathrm{V}_{\text {ref }} / 2$ or 0 at the output, $\mathrm{V}_{\mathrm{i}+1}$.
image_name:(a)
description:This circuit is part of a 1.5-bit per stage pipelined ADC. It includes sampling capacitors and an operational amplifier configured for gain and signal transfer.
image_name:(b)
description:The circuit diagram is a part of a pipelined ADC stage using a multiplying digital-to-analog converter (MDAC) configuration. It operates in two phases: in the first phase, the input is sampled onto the capacitors; in the second phase, the input is transferred to the output with a gain of two, and the comparator output bits determine the subtracted signal. The capacitors labeled C/2 are used for charge redistribution.

Fig. 17.22 MDAC for the 1.5 bit per stage pipelined converter during two clock phases: (a) input is sampled onto all capacitors; (b) the input is transferred to the output with a gain of two and the comparator output bits $b_{i, 0}$ and $b_{i, 1}$ determine the subtracted signal.
image_name:Fig. 17.23
description:The diagram in Fig. 17.23 represents a general k-bit stage in a pipelined Analog-to-Digital (A/D) converter.

1. **Main Components:**
- **Sample and Hold (S/H) Block:** This block receives the input signal \( V_i \) and holds it stable for processing.
- **k-bit Sub-A/D Converter:** This block converts the held analog signal into a k-bit digital signal.
- **k-bit Sub-D/A Converter:** This block converts the k-bit digital signal back into an analog signal, \( V_{i,x} \).
- **Summation Block (+):** This block subtracts the analog output \( V_{i,x} \) from the held input signal.
- **Amplifier Block (\( 2^k \)):** This block amplifies the result of the summation by a factor of \( 2^k \) to produce the output \( V_{i+1} \).

2. **Flow of Information or Control:**
- The input signal \( V_i \) is first sampled and held by the S/H block.
- The sampled signal is then fed into the k-bit sub-A/D converter, producing a k-bit digital output.
- This digital output is sent to the k-bit sub-D/A converter, which generates an analog signal \( V_{i,x} \).
- The summation block subtracts \( V_{i,x} \) from the original held input, effectively creating a residue signal.
- This residue signal is then amplified by the factor \( 2^k \) in the amplifier block, resulting in the output signal \( V_{i+1} \).

3. **Labels, Annotations, and Key Indicators:**
- The input and output signals are labeled as \( V_i \) and \( V_{i+1} \) respectively.
- The amplification factor is indicated as \( 2^k \), denoting the gain applied to the residue signal.

4. **Overall System Function:**
- The primary function of this k-bit stage in a pipelined A/D converter is to process the input signal in stages, resolving k bits per stage. The sampled input signal is converted to digital, then back to analog to create a residue signal. This residue is amplified, allowing the next stage to process another set of bits, thus building up the complete digital representation of the input signal over multiple stages.

Fig. 17.23 A general $k$-bit stage in a pipelined A/D converter.

### 17.4.4 Generalized k-Bit-Per-Stage Pipelined Converters

More than one bit can be resolved per stage by increasing the interstage gain and number of comparators per stage. The signal flow is similar to that illustrated in Fig. 17.13 for a 2-bit per iteration successive approximation converter. A generalized k-bit stage is shown in Fig. 17.23. Nonlinearities in the k-bit sub-A/D converter can be digitally corrected by adding additional comparators, similar to the 1.5 bit per stage architecture [Lewis, 1992]. The advantages of the k-bit-per-stage architecture are that fewer stages are needed, which can reduce area and/or power consumption compared with the 1.5 bit per stage. Also, for a given resolution, there are fewer stages for the input signal to traverse through the pipeline, so there are fewer clock cycles of latency in each conversion.

The circuit shown in Fig. 17.22 can be modified to accommodate k bits per stage with $\mathrm{k} \geq 2$ by dividing the input sampling capacitor into smaller unitsized devices. The required interstage gain is greater than 2 , so a smaller fraction of the sampling capacitance is switched into the feedback network in the second clock phase. Hence, the feedback factor $\beta$ is reduced and closed loop bandwidth is decreased compared with the 1.5 -bit stage (assuming the same opamp is used).

The major limitations on converter accuracy remains the accuracy of the inter-

Key Point: Multiple bits can be resolved in each stage, with digital correction, in order to reduce the number of opamps in a pipelined converter and decrease the number of clock cycles required for each conversion.
stage gain, linearity of the sub-D/A converter, and noise in the MDAC circuit. Again, accuracy requirements are most stringent in the first stage where errors influence the most significant bits.

## 17.5 FLASH CONVERTERS

Flash converters are the standard approach for realizing very-high-speed converters. The input signal in a flash converter is fed to $2^{\mathrm{N}}$ comparators in parallel, as shown in Fig. 17.24. Each comparator is also connected to a different node of a resistor string. Any comparator connected to a resistor string node where $\mathrm{V}_{\mathrm{ri}}$ is larger than $\mathrm{V}_{\mathrm{in}}$ will have a 1 output while those connected to nodes with $\mathrm{V}_{\mathrm{ri}}$ less than $\mathrm{V}_{\mathrm{in}}$ will have 0 outputs. Such an output code word is commonly referred to as a thermometer code since it looks quite similar to the mercury bar in a thermometer. Note that the top and bottom resistors in the resistor string have been chosen to create a 0.5 LSB offset in an A/D converter.

Key Point: Flash converters are generally capable of the fastest conversion speeds of any $A / D$ architecture. However, their power consumption grows dramatically with the required resolution so they are usually reserved for converters where high speed and low or modest resolution is sought.
image_name:Fig. 17.24 A 3-bit flash A/D converter
description:This is a 3-bit flash A/D converter. It uses a resistor ladder network to create reference voltages for the comparators. Each comparator compares the input voltage Vin to a reference voltage. The outputs of the comparators are processed by a series of NAND gates to detect transitions and perform error detection. The (2^N-1) to N encoder converts the comparator outputs to N digital outputs. This architecture provides fast conversion speeds suitable for high-speed applications with low to moderate resolution.

Fig. 17.24 A 3-bit flash A/D converter.
The NAND gate that has a 0 input connected to its inverting input and a 1 input connected to its noninverting input detects the transition of the comparator outputs from 1 s to 0 s , and will have a 0 output. All other NAND-gate outputs will be 1 , resulting in simpler encoding. It also allows for error detection by checking for more than one 0 output, which occurs during a bubble error (see the next subsection) and, perhaps, error correction.

Flash $\mathrm{A} /$ Ds are fast but the number of comparators grows exponentially with the resolution N , so they typically take up a large area and are very power hungry, even for modest N - especially when they are clocked fast. One way to realize a small clocked CMOS comparator is by using a CMOS inverter, as shown in Fig. 17.25 [Dingwall, 1979].

When $\phi$ is high, the inverter is set to its bistable operating point, where its input voltage equals its output voltage (i.e., its threshold voltage). Normally with an odd number of inverters, a ring oscillator is formed; however, in the case of a single CMOS inverter, the inverter operates as a single stage opamp with only one pole (no nondominant poles), so stability is guaranteed. With this inverter set to its threshold voltage, the other side of C is charged to $\mathrm{V}_{\mathrm{ri}}$. When $\phi$ goes low, the inverter is free to fall either high or low depending on its input voltage. At the same time, the other side of C is pulled to the input voltage, $\mathrm{V}_{\mathrm{in}}$. Since the inverter side of the capacitor is floating, C must keep its original charge, and therefore the inverter's input will change by the voltage difference between $\mathrm{V}_{\mathrm{ri}}$ and $\mathrm{V}_{\mathrm{in}}$. Since the inverter's input was at its bistable point, the difference between $\mathrm{V}_{\mathrm{ri}}$ and $\mathrm{V}_{\mathrm{in}}$ will determine which direction the inverter's output will fall. However, it should be mentioned that this simple comparator suffers from poor power supply rejection, which is often a critical design specification in fast converters. Using fully differential inverters helps alleviate this shortcoming.

image_name:Fig. 17.25 A clocked CMOS comparator.
description:The circuit is a clocked CMOS comparator. It uses a CMOS inverter and a latch to compare input voltages V_ri and V_in. The capacitor C is used to stabilize the input before the inverter. The latch is clocked with the signal phi to capture the comparator's output, which is then sent to decoding logic.

Fig. 17.25 A clocked CMOS comparator.

### 17.5.1 Issues in Designing Flash A/D Converters

We discuss here some important design issues that should be addressed when building high-speed flash $A / D$ converters.

Input Capacitive Loading The large number of comparators connected to $\mathrm{V}_{\mathrm{in}}$ results in a large parasitic load at the node $\mathrm{V}_{\mathrm{in}}$. Such a large capacitive load often limits the speed of the flash converter and usually requires a strong and power-hungry buffer to drive $\mathrm{V}_{\mathrm{in}}$. We shall see that this large capacitive loading can be reduced by going to an interpolating architecture.

Resistor-String Bowing Any input currents to the comparators cause errors in the voltages of the nodes of the resistor string. These errors usually necessitate the bias current in the resistor string being two orders of magnitude greater than the input currents of the comparators. This is particularly significant if bipolar comparators are used. The errors are greatest at the center node of the resistor string and thus considerable improvement can be obtained by using additional circuitry to force the center tap voltage to be correct.

Comparator Latch-to-Track Delay Another consideration that is often overlooked is the time it takes a comparator latch to come from latch mode to track mode when a small input signal of the opposite polarity from the previous period is present. This time can be minimized by keeping the time constants of the internal nodes of the latch as small as possible. This is sometimes achieved by keeping the gain of the latches small, perhaps only two to four. In many cases, the differential internal nodes might be shorted together temporarily as a reset just after latch time.

Signal and/or Clock Delay Even very small differences in the arrival of clock or input signals at the different comparators can cause errors. To see this, consider a $250-\mathrm{MHz}, 1-\mathrm{V}$ peak-input sinusoid. This signal has a maximum slope of $1570 \mathrm{~V} / \mu \mathrm{s}$ at the zero crossing. If this signal is being encoded by an 8 -bit $\mathrm{A} / \mathrm{D}$ converter with $\mathrm{V}_{\text {ref }}=2 \mathrm{~V}$ (i.e., the sinusoid covers the whole range), then it would only take 5 ps to change through 1 LSB . This time is roughly about the same time it takes a signal to propagate $500 \mu \mathrm{~m}$ in metal interconnect. If there is clock skew between comparators greater than this, the converter will have more than 1 LSB error. One means of easing this problem is to precede the converter by a sample-and-hold circuit. However, high-speed sample-and-hold circuits can be more difficult to realize than the flash converter itself. In addition, the clock and $\mathrm{V}_{\text {in }}$ should be routed together with the delays matched [Gendai, 1991]. It should also be noted that the delay differences may not be caused just by routing differences, but could also be caused by different capacitive loads, or by phase differences between the comparator preamplifiers at high frequencies.
image_name:Fig. 17.26 Using three-input NAND gates to remove single bubble errors.
description:The system block diagram in Fig. 17.26 illustrates a method for using three-input NAND gates to remove single bubble errors in a flash analog-to-digital converter (ADC). This setup is crucial for ensuring accuracy in digital signal conversion by mitigating errors that may arise during the process.

1. **Main Components:**
- **Resistor Ladder Network:** This component is on the left side of the diagram. It provides a series of reference voltages (V_ri) to the comparators, creating a voltage gradient across the ladder.
- **Comparators:** These are arranged vertically next to the resistor ladder. Each comparator receives the input voltage (V_in) and a reference voltage (V_ri) from the resistor ladder. The comparators compare these voltages and output a digital signal indicating whether V_in is higher or lower than the reference voltage.
- **Three-Input NAND Gates:** The outputs of the comparators are fed into a series of three-input NAND gates. These gates are used to process the comparator outputs and help eliminate single bubble errors, which are errors that can occur when only one comparator incorrectly changes state.
- **(2^N−1) to N Encoder:** This block receives the processed signals from the NAND gates and converts them into N digital outputs. This encoding is necessary to translate the thermometer code from the comparators into a binary code suitable for digital systems.

2. **Flow of Information or Control:**
- The input voltage (V_in) is fed into each comparator, along with a corresponding reference voltage (V_ri) from the resistor ladder.
- The comparators output a digital signal based on the comparison between V_in and V_ri.
- These outputs are then processed by the three-input NAND gates to remove any single bubble errors, ensuring a more reliable digital signal.
- The processed signals are sent to the (2^N−1) to N encoder, which converts them into N digital outputs.

3. **Labels, Annotations, and Key Indicators:**
- The diagram is labeled with V_in, V_ri, and indicates the presence of N digital outputs from the encoder.
- The use of three-input NAND gates is specifically highlighted as a method for error correction.

4. **Overall System Function:**
- The primary function of this system is to convert an analog voltage input into a digital output while minimizing errors, specifically single bubble errors, during the conversion process. The arrangement of comparators, NAND gates, and an encoder ensures that the digital output is both accurate and reliable.

Fig. 17.26 Using three-input NAND gates to remove single bubble errors.

Substrate and Power-Supply Noise For $\mathrm{V}_{\text {ref }}=1 \mathrm{~V}$ and an 6-bit converter, only 15.6 mV of noise injection would cause a 1 LSB error. On an integrated circuit having a clock signal in the hundreds or even thousands of MHz , it is difficult to keep power-supply noise below 100 mV . This power-supply noise can easily couple through the circuitry or substrate, resulting in errors. To minimize this problem, the clocks must be shielded from the substrate and from analog circuitry. Also, running differential clocks closely together will help prevent the signals from being coupled into the substrate or to critical circuit nodes through the air. Also, analog power supplies should be separated from digital power supplies. Specifically, it is advisable to have analog power supplied to the comparator preamps while using digital power for the latch stages. On-chip power-supply bypass capacitors are a necessity. It is also necessary to make sure the power-supply bypass circuitry doesn't resonate with the circuit packaging parasitics. Small resistors in series with the by-pass capacitors can help dampen any such resonance.

Bubble Error Removal The outputs of the comparators should be a thermometer code with a single transition. However, sometimes a lone 1 will occur within the string of 0 s (or a 0 within the string of 1 s ) due to comparator metastability, noise, cross talk, limited bandwidth, etc. These bubbles usually occur near the transition point of the thermometer code. Fortunately, these bubbles can usually be removed with little extra complexity by replacing the two-input NAND gates shown in Fig. 17.24 with three-input NAND gates, as shown as shown in Fig. 17.26 [Steyaert, 1993]. With this modification, there must now be two 1 s immediately above a 0 in determining the transition point in the thermometer code. However, this circuit will not eliminate the problem of a stray 0 being two places away from the transition point, which may cause a large decoding error. Another digital approach for reducing the effect of bubble errors is to allow bubble errors in the lower 2 LSBs but have the remaining MSBs determined by looking for transitions between every fourth comparator [Gendai, 1991]. With this approach, bubble errors that occur within four places of the transition point do not cause any large errors. An alternate approach to reduce the effect of distant bubble errors is to create two encoders (one AND type and one OR type) rather than a single encoder [Ito, 1994]. When an unexpected output pattern occurs at the NAND outputs, the errors in two different encoders tend to be equal in magnitude but opposite in sign. Thus, the final output is taken as the average of the two encoder outputs, which is performed by adding the two outputs and dropping the LSB (to divide by two).

An alternative method to remove bubble errors that does not increase power dissipation is shown in Fig. 17.27. Here, extra transistors have been added to the inputs of the slave latches, which are driven by the comparator master latches [van Valburg, 1992]. These extra transistors make the value stored in a slave latch not just a function of its master latch, but also a function of the two adjacent master latches. If a bubble occurs, the outputs from the two adjacent master latches are the same, but different from the center master latch. In this case,
image_name:Fig. 17.27
description:The circuit is a bubble-error voting circuit that uses additional transistors to ensure that the slave latch's output is determined by its master latch and two adjacent master latches. This prevents errors without increasing power dissipation.

Fig. 17.27 Bubble-error voting circuit that does not increase the power dissipation.
the values from the adjacent master latches overrule the center master latch. Note that with this approach, the power dissipation is not increased because the added transistors make use of existing current in the slave latch. Alternatively, this same voting scheme can be implemented entirely in digital form.

Flashback An additional source of error is flashback. Flashback is caused by clocked comparators, which are almost always used. When clocked comparators are switched from track to latch mode, or vice versa, there is major charge glitch at the inputs to the latch. If there is no preamplifier, this will cause major errors due to the unmatched impedances at the comparator inputs (one input goes to the resistor string-the other to the input signal). To minimize this effect, most modern comparators have one or two stages of continuous-time buffering and/or preamplification. For example, a bipolar comparator is shown in Fig. 17.28. Notice that it has a buffer, a low-gain preamp, and another buffer before the track-and-latch circuitry. Also notice that in the positive feedback latch the feedback is taken from the emitter-follower outputs, which minimizes the capacitances of the internal nodes of the latch. A CMOS comparator may be used with the same topology, although the source-follower buffers are usually omitted.

Another technique sometimes used to minimize the effects of flashback is to match the input impedances as much as is possible. For example, it is possible to implement a second matched resistor string, with the nodes of the comparators that were originally connected to $\mathrm{V}_{\text {in }}$ now being connected to it, and the end nodes of the string connected together to $\mathrm{V}_{\mathrm{in}}$. This approach matches impedances and also minimizes the resistor-string bowing due to the comparator input currents. Unfortunately, it does result in different delays for $\mathrm{V}_{\text {in }}$ reaching the various comparators, and unless these are matched to the routing of the clock signals, these different delays may not be tolerable.

## 17.6 TWO-STEP A/D CONVERTERS

Two-step (or subranging) converters are used for high-speed medium-accuracy A/D converters. They offer several advantages over their flash counterparts. Specifically, two-step converters require less silicon area, dissipate less power, have less capacitive loading, and the voltages the comparators need to resolve are less stringent than for flash equivalents. The throughput of two-step converters approaches that of flash converters, although they do have a larger latency.
image_name:Clocked comparator with a preamplifier
description:The circuit diagram represents a clocked comparator with a preamplifier. It includes a continuous-time preamp section and a track and latch section. The preamp section uses differential pairs to amplify the input signals (Vin and Vref). The track and latch section is controlled by the switches Trk and Ltch, which manage the timing and hold operations of the comparator. The comparator outputs are labeled as Q and Q-bar.

Fig. 17.28 Clocked comparator with a preamplifier to reduce flashback.
image_name:Fig. 17.29
description:The block diagram represents an 8-bit two-step analog-to-digital (A/D) converter. This converter is structured as a two-stage pipeline, with each stage responsible for converting a part of the input signal into digital form.

Main Components:
1. **4-bit MSB A/D Converter**: This block takes the analog input signal \( V_{in} \) and converts it into the first four most significant bits (MSBs) of the digital output, labeled as \( b_1, b_2, b_3, b_4 \).

2. **4-bit D/A Converter**: The digital output from the 4-bit MSB A/D is fed into this digital-to-analog converter, which reconstructs an analog signal \( V_1 \) from the 4-bit digital data.

3. **Summation Node**: The original input \( V_{in} \) is subtracted by the reconstructed analog signal \( V_1 \) to obtain the quantization error \( V_q \).

4. **Gain Amplifier**: This block amplifies the quantization error \( V_q \) by a factor of 16 to produce an amplified error signal.

5. **4-bit LSB A/D Converter**: The amplified error signal is then converted by this block into the lower four bits \( b_5, b_6, b_7, b_8 \) of the digital output.

Flow of Information:
- The input signal \( V_{in} \) is first processed by the 4-bit MSB A/D converter to determine the first four bits of the output.
- The resulting digital signal is then converted back into an analog signal \( V_1 \) by the 4-bit D/A converter.
- The summation node computes the quantization error \( V_q \) by subtracting \( V_1 \) from \( V_{in} \).
- This error is amplified by the gain amplifier and passed to the 4-bit LSB A/D converter, which determines the lower four bits of the output.

Labels and Annotations:
- The diagram clearly labels the output of each conversion stage, showing the division into first and lower four bits.
- The gain amplifier is annotated with a gain value of 16, indicating the level of amplification applied to the quantization error.

Overall System Function:
The primary function of this two-step A/D converter is to efficiently convert an analog input signal into an 8-bit digital output. The first stage handles the most significant bits, while the second stage refines the conversion by processing the amplified quantization error to determine the least significant bits. This approach allows for high-resolution conversion with reduced complexity compared to a single-step converter of equivalent bit depth.

Fig. 17.29 An 8-bit two-step A/D converter.

The block diagram for a two-step converter is shown in Fig. 17.29. In fact, a two-step converter may be thought of as a special case of a pipelined converter with only two pipeline stages. The example of Fig. 17.29 shows two 4 bit stages with no redundancy resulting in a 8 -bit output. The 4-bit MSB A/D determines the first four MSBs. To determine the remaining LSBs, the quantization error (residue) is found by reconverting the 4-bit digital signal to an analog value using the 4-bit $\mathrm{D} / \mathrm{A}$ and subtracting that value from the input signal. To ease the requirements in the circuitry for finding the remaining LSBs, the quantization error is first multiplied by 16 using the gain amplifier, and the LSBs are determined using the 4-bit LSB A/D. With this approach, rather than requiring 256 comparators as in an 8-bit flash converter, only 32 comparators are required for a two-step A/D converter. However, this straightforward approach would require all components to be at least 8 -bit accurate. To significantly ease the accuracy requirements of the 4-bit MSB A/D converter, digital error correction is commonly used.

### 17.6.1 Two-Step Converter with Digital Error Correction

The block diagram for a two-step converter with digital error correction is shown in Fig. 17.30. Its operation is directly analogous to that of the 1.5 bit per stage pipeline converter. The ranges of the 4-bit and 5-bit stages overlap, and hence inaccuracies in the first A/D converter can be cancelled by the second. To see how this correction works and why a second-stage 5-bit converter is needed (rather than 4-bit), consider the quantization error that occurs in an ideal converter. Defining $\mathrm{V}_{\mathrm{LSB}}=\mathrm{V}_{\text {ref }} / 2^{8}$ (i.e., always relative to 8-bit accuracy), we have for an ideal 8-bit converter,

Key Point: Two-step converters may be considered a special case of pipelined converters where only 2 pipelined stages are needed. As with pipelined converters, digital error correction greatly relaxes the requirements on the first stage.

$$
\begin{equation*}
\mathrm{V}_{\mathrm{ref}} \mathrm{~B}_{\mathrm{out}}=\mathrm{V}_{\mathrm{in}}+\mathrm{V}_{\mathrm{q}} \quad \text { where } \quad-\frac{1}{2} \mathrm{~V}_{\mathrm{LSB}}<\mathrm{V}_{\mathrm{q}}<\frac{1}{2} \mathrm{~V}_{\mathrm{LSB}} \tag{17.43}
\end{equation*}
$$

However, for a nonideal 8-bit converter with an absolute accuracy of 0.5 LSB , we have

$$
\begin{equation*}
\mathrm{V}_{\text {ref }} \mathrm{B}_{\text {out }}=\mathrm{V}_{\text {in }}+\mathrm{V}_{\mathrm{q}} \quad \text { where } \quad-\mathrm{V}_{\mathrm{LSB}}<\mathrm{V}_{\mathrm{q}}<\mathrm{V}_{\mathrm{LSB}} \tag{17.44}
\end{equation*}
$$

In other words, the maximum quantization signal is now twice that of the ideal case.
Similarly, for an ideal 4-bit A/D converter, we have (keeping the 8-bit definition of $\mathrm{V}_{\mathrm{LSB}}$ ),

$$
\begin{equation*}
\mathrm{V}_{\text {ref }} \mathrm{B}_{\text {out }}=\mathrm{V}_{\text {in }}+\mathrm{V}_{\mathrm{q}} \quad \text { where } \quad-8 \mathrm{~V}_{\mathrm{LSB}}<\mathrm{V}_{\mathrm{q}}<8 \mathrm{~V}_{\mathrm{LSB}} \tag{17.45}
\end{equation*}
$$

Thus in the ideal case, the value of $\mathrm{V}_{\mathrm{q}}$ can be determined (to 8-bit accuracy) using a 4-bit $\mathrm{A} / \mathrm{D}$ converter since $\mathrm{V}_{\mathrm{q}}$ must be within $16 \mathrm{~V}_{\text {LSB }}$. However, for the nonideal case where the 4-bit MSB flash converter has an absolute accuracy of $8 \mathrm{~V}_{\mathrm{LSB}}$, the quantization error, $\mathrm{V}_{\mathrm{q}}$, is now bounded within $32 \mathrm{~V}_{\mathrm{LSB}}$. Thus, in the case of a non-ideal 4-bit MSB converter, a 5-bit LSB converter must be used; otherwise $\mathrm{V}_{\mathrm{q}}$ may go out of range. Note that the gain amplifier of 8 is used to amplify the quantization error back to maximum signal levels to ease the requirements of the 5-bit LSB converter. Finally, to determine $\mathrm{V}_{\mathrm{in}}$, we see that the digital value of $\mathrm{V}_{\mathrm{q}}$ has been found to within
image_name:Fig. 17.30
description:The system block diagram represents an 8-bit two-step Analog-to-Digital (A/D) converter with digital error correction, as outlined in Fig. 17.30. The primary function of this system is to convert an analog input voltage, \( V_{in} \), into an 8-bit digital output with enhanced accuracy through a two-step conversion process.

Main Components:
1. **Sample and Hold (S/H) Circuits:**
- **S/H1:** Captures the input voltage \( V_{in} \) to stabilize it for conversion. It is 8-bit accurate.
- **S/H2 and S/H3:** Used to hold intermediate signals during the conversion process, also 8-bit accurate.

2. **4-bit MSB A/D Converter:**
- Converts the most significant bits (MSB) of the sampled input into a 4-bit digital signal. It is 4-bit accurate.

3. **4-bit D/A Converter:**
- Converts the 4-bit digital output from the MSB A/D back into an analog signal, \( V_1 \), for further processing. It is 8-bit accurate.

4. **Subtractor:**
- Computes the quantization error \( V_q \) by subtracting \( V_1 \) from \( V_{in} \).

5. **Gain Amplifier:**
- Amplifies the quantization error \( V_q \) by a factor of 8 to match the signal levels required for the next stage.

6. **5-bit LSB A/D Converter:**
- Converts the amplified quantization error into a 5-bit digital signal. It is 5-bit accurate.

7. **Digital Delay:**
- Aligns the timing of the MSB and LSB digital outputs for correct processing.

8. **Error Correction Block:**
- Combines the 4-bit MSB and 5-bit LSB outputs to produce a final 8-bit digital output, correcting any errors introduced in the conversion process.

Flow of Information:
- The input voltage \( V_{in} \) is first sampled by S/H1.
- The sampled signal is converted by the 4-bit MSB A/D converter.
- The digital output is converted back to analog by the 4-bit D/A converter, resulting in \( V_1 \).
- The subtractor calculates the error \( V_q \) by subtracting \( V_1 \) from \( V_{in} \).
- The error \( V_q \) is amplified and held by S/H3 before being converted by the 5-bit LSB A/D converter.
- The digital delay ensures the 4-bit MSB and 5-bit LSB outputs are synchronized.
- The error correction block integrates the two digital signals to yield the final 8-bit output.

Overall System Function:
The system effectively divides the conversion process into two steps: a coarse conversion by the 4-bit MSB A/D and a fine conversion of the residual error by the 5-bit LSB A/D. This two-step approach, along with digital error correction, enhances the accuracy of the final 8-bit digital output, overcoming limitations of a single-step conversion process.

Fig. 17.30 An 8-bit two-step A/D converter with digital error correction.
$0.5 \mathrm{~V}_{\text {LSB }}$ and the digital value of $\mathrm{V}_{1}$ is known to the same accuracy since we assumed the $\mathrm{D} / \mathrm{A}$ converter to be 8bit accurate (and the digital word applied to the $\mathrm{D} / \mathrm{A}$ converter is known). Therefore, we find $\mathrm{V}_{\mathrm{in}}$ from the relation

$$
\begin{equation*}
V_{i n}-V_{1}=V_{q} \tag{17.46}
\end{equation*}
$$

Specifically, $\mathrm{V}_{\text {in }}$ is found by properly combining the digital equivalents of $\mathrm{V}_{1}$ and $\mathrm{V}_{\mathrm{q}}$.
In summary, the MSB A/D need only be accurate to $1 / 2^{4}=1 / 16$. The only components that need 0.5 LSB accuracy at the 8 -bit level are S/Hs 1 and 2 , the $\mathrm{D} / \mathrm{A}$, and the subtraction circuit. For a more detailed treatment of a two-step A/D converter, the reader is referred to a 10 -bit 75 MHz implementation (with integrated $\mathrm{S} / \mathrm{H}$ ), described in [Petschacher, 1990].

Besides the difficulty in realizing the $\mathrm{S} / \mathrm{H}$ circuits, another major limitation is the difficulty of designing a high-speed, accurate (to 0.5 LSB at the 5 -bit level) gain amplifier. In fact, due to difficulties in realizing highspeed circuits with gain, often fewer bits are determined in the first stage of a two-step converter to reduce the amplification required. For example, a two-step converter where the first stage resolves only 1 bit is described in [Verbruggen, 2009] achieving very low power.

#### EXAMPLE 17.9

For the two-step 8-bit A/D converter shown in Fig. 17.30, what is the maximum voltage range at $\mathrm{V}_{\mathrm{q}}$ when the converter's full-scale input is $\pm 2.5 \mathrm{~V}$ in the case where the 4 -bit MSB A/D converter is (a) 8 -bit accurate and (b) 4-bit accurate? Assume all other components are ideal.

#### Solution

With a full-scale peak-to-peak input voltage of 5 V applied to an 8 -bit $\mathrm{A} / \mathrm{D}$ converter, we have

$$
\begin{equation*}
\mathrm{V}_{\mathrm{LSB}}=\frac{5}{2^{8}}=19.5 \mathrm{mV} \tag{17.47}
\end{equation*}
$$

For an ideal 4-bit $\mathrm{A} / \mathrm{D}$ converter, we have from (17.45) the maximum voltage range of $\mathrm{V}_{\mathrm{q}}$ is $16 \mathrm{~V}_{\mathrm{LSB}}$, or equivalently, 312 mV .
(a) If we go to the trouble to make the 4-bit $\mathrm{A} / \mathrm{D}$ converter have an absolute accuracy of $0.5 \mathrm{~V}_{\mathrm{LSB}}$ (i.e., 8 -bit accurate), then $\mathrm{V}_{\mathrm{q}}$ becomes bounded between $\pm 8.5 \mathrm{~V}_{\mathrm{LSB}}$. In other words, the maximum range of $\mathrm{V}_{\mathrm{q}}$ would now be $17 \mathrm{~V}_{\mathrm{LSB}}$, or equivalently, 332 mV . Note that the input range of the LSB converter is $8 \times 332 \mathrm{mV}=2.7 \mathrm{~V}$ (a little more than half of the input range of the overall converter), so more gain could be used in this case.
(b) In the case of a 4-bit accurate MSB converter, $\mathrm{V}_{\mathrm{q}}$ is bounded between $\pm 16 \mathrm{~V}_{\mathrm{LSB}}$, implying that the maximum range of $\mathrm{V}_{\mathrm{q}}$ is $32 \mathrm{~V}_{\mathrm{LSB}}$, or equivalently, 618 mV . After the gain of 8 , the input range of the LSB converter becomes $8 \times 618 \mathrm{mV}=4.9 \mathrm{~V}$ (the same as the input range of the overall converter).

## 17.7 INTERPOLATING A/D CONVERTERS

Key Point: The large capacitive input presented by flash A/D converters can be reduced by using fewer input amplifiers and interpolating between them to create the missing intermediate values.

Interpolating converters make use of input amplifiers, as shown in Fig. 17.31. These input amplifiers behave as linear amplifiers near their threshold voltages but are allowed to saturate once their differential inputs become moderately large. As a result, noncritical latches need only determine the sign of the amplifier outputs since the differences between the input signal and threshold voltages have been amplified. Also, the number of input amplifiers attached to $\mathrm{V}_{\mathrm{in}}$ is significantly reduced by interpolating between adjacent outputs of these amplifiers. While this approach is often combined with a "folding" architecture [van de Grift, 1987; van Valburg, 1992], the interpolating architecture has also been used quite successfully by itself [Goodenough, 1989; Steyaert, 1993].
image_name:Fig. 17.31 A 4-bit interpolating A/D converter
description:This is a 4-bit interpolating A/D converter with an interpolating factor of 4. It uses multiple operational amplifiers to interpolate between input signals. The reference voltage is set at 1V. The output is processed through digital logic to produce a 4-bit output.

Fig. 17.31 A 4-bit interpolating A/D converter (interpolating factor of 4).

To further understand this interpolation approach, some possible signals for the input-amplifier outputs, $\mathrm{V}_{1}$ and $\mathrm{V}_{2}$, as well as their interpolated values are shown in Fig. 17.32. As can be seen in the figure, the logic levels are assumed to be zero and five volts, with the input comparators having a maximum gain of about -10 . Also, here the latch threshold is near the midpoint of the two logic levels (or about 2.5 volts). As $\mathrm{V}_{\mathrm{in}}$ increases, the latch for $V_{1}$ is first triggered, followed by $V_{2 a}$ and so on until $V_{2}$. As a result, more reference levels have been created between $\mathrm{V}_{1}$ and $\mathrm{V}_{2}$. It should be noted here that for good linearity, the interpolated signals need only cross the latch threshold at the correct points, while the rest of the interpolated signals responses are of secondary importance. One way to create such correct crossing points is to ensure that $\mathrm{V}_{1}$ and $\mathrm{V}_{2}$ are linear between their own thresholds. In Fig. 17.32, this linear region corresponds to $0.25<\mathrm{V}_{\text {in }}<0.5$.

For fast operation, it is important that the delays to each of the latches are made to equal each other as much as possible. Since the latch comparators have similar input capacitances associated with them, the delays can be made nearly equal by adding extra series resistors, as shown in Fig. 17.33. These series resistors equalize the impedances seen by each latch comparator looking back into the resistive string, assuming the input-amplifier outputs are low impedance [van de Plassche, 1988].

As mentioned earlier, the main benefit of an interpolating architecture is the reduction in the number of differential pairs attached to the input signal, $\mathrm{V}_{\mathrm{in}}$. Such a reduction results in a lower input capacitance (which is quite
image_name:Fig. 17.32 Possible transfer responses for the input-comparator output signals, V1 and V2, and theil interpolated signals
description:The graph in Fig. 17.32 illustrates possible transfer responses for input-comparator output signals, specifically $V_1$, $V_2$, and their interpolated signals ($V_{2a}$, $V_{2b}$, $V_{2c}$). The graph is a plot of voltage transfer characteristics, depicting how the output voltage varies with the input voltage ($V_{in}$).

1. **Type of Graph and Function:**
- This is a voltage transfer characteristic graph, which is typically used to show the relationship between input and output voltages in a comparator or amplifier circuit.

2. **Axes Labels and Units:**
- The x-axis represents the input voltage ($V_{in}$) in volts, ranging from 0 to 1 volt.
- The y-axis represents the output voltage in volts, ranging from 0 to 5 volts.

3. **Overall Behavior and Trends:**
- The graph shows a set of curves that start at the top left (5 volts output) and curve downward to the bottom right (0 volts output), indicating a decreasing relationship between input and output voltages.
- The curves represent different possible responses, with $V_1$ and $V_2$ being the outermost curves and the interpolated signals ($V_{2a}$, $V_{2b}$, $V_{2c}$) lying in between.
- All curves pass through a region near the middle of the graph where the output voltage crosses a dashed line labeled "Latch threshold," indicating a critical point for comparator operation.

4. **Key Features and Technical Details:**
- The graph shows a smooth transition for each curve from high to low output voltage as $V_{in}$ increases.
- The "Latch threshold" line is a key feature, suggesting a voltage level where the latch comparator changes state.
- The curves are labeled with arrows indicating the direction of the response from $V_1$ to $V_2$ and their interpolated variations.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for each curve ($V_1$, $V_{2a}$, $V_{2b}$, $V_{2c}$, $V_2$) with arrows pointing in the direction of decreasing output voltage.
- The "Latch threshold" is annotated with a dashed line horizontally across the graph, representing a significant voltage level for the operation of the latch comparator.
image_name:Fig. 17.33 Adding series resistors to equalize delay times to the latch comparators.
description:The diagram shows possible transfer responses for the input-comparator output signals, V1 and V2, and their interpolated signals. It illustrates how the signals V1, V2, V2a, V2b, V2c, and their interpolated versions respond to varying input voltage (Vin) with respect to a latch threshold. The graph is plotted with Vin on the x-axis and voltage on the y-axis, ranging from 0 to 5 volts.

Fig. 17.32 Possible transfer responses for the input-comparator output signals, $\mathrm{V}_{1}$ and $\mathrm{V}_{2}$, and theil interpolated signals.
image_name:Fig. 17.33
description:The circuit diagram shows a series of resistors and latches connected to two operational amplifiers, V1 and V2, which are used to compare input voltages of 0.25V and 0.5V against Vin. The output from the op-amps is fed through a network of resistors to a series of latches, which produce outputs labeled 4 to 8.

Fig. 17.33 Adding series resistors to equalize delay times to the latch comparators.
high for a flash converter), a slightly reduced power dissipation, and a lower number of accurate reference voltages that need to be created. Finally, it should be mentioned that circuit techniques other than resistive strings can be used to realize this interpolative approach. In [Steyaert, 1993], current mirrors were used to interpolate eight times between comparators. In another implementation, two stages of interpolation using capacitors were realized [Kusumoto, 1993].

### EXAMPLE 17.10

Using current mirrors, show how one can interpolate two current outputs, $I_{1}$ and $I_{2}$, by three. What reduction in input capacitance of the converter would be expected over a traditional flash architecture?

### Solution

If interpolating by three, it is desired to create two new currents, $I_{2 a}, I_{2 b}$ such that

$$
\begin{equation*}
\mathrm{I}_{2 \mathrm{a}}=\frac{2}{3} \mathrm{I}_{1}+\frac{1}{3} \mathrm{I}_{2} \tag{17.48}
\end{equation*}
$$

image_name:Fig. 17.34
description:The circuit is designed to interpolate between two current outputs, I1 and I2, by creating two new currents, I2a and I2b, using a series of resistors to divide the current. The resistors are sized to achieve the desired interpolation ratios. The design reduces input capacitance compared to a traditional flash architecture by requiring fewer inputs.

Fig. 17.34 Interpolating by three between two current outputs.

$$
\begin{equation*}
I_{2 b}=\frac{1}{3} I_{1}+\frac{2}{3} I_{2} \tag{17.49}
\end{equation*}
$$

These output currents can be realized as shown in Fig. 17.34. These four currents can be converted back to voltages to send to the latches. Alternatively, the currents can be directly sent to latches which make use of current inputs.

Since we are interpolating by three here, this converter would require one-third the number of input amplifiers in relation to a traditional flash converter. Thus, the input capacitance for this interpolated approach would be one-third of that for a flash.

## 17.8 FOLDING A/D CONVERTERS

We just saw that the number of input amplifiers can be reduced through the use of an interpolating architecture. However, the number of latch comparators remains at $2^{\mathrm{N}}$ for an N -bit converter. This large number of latch comparators can be significantly reduced through the use of a folding architecture. A folding A/D converter is similar in operation to a two-step (or subranging) converter in that a group of LSBs are found separately from a group of MSBs. However, whereas a two-step converter requires an accurate D/A converter, a

Key Point: A folding architecture requires fewer latches than a flash converter. It does so similar to a two-step converter, but uses analog preprocessing instead of an accurate D/A converter and gain amplifier.
folding converter determines the LSB set more directly through the use of analog preprocessing while the MSB set is determined at the same time.

As an example, consider the 4 -bit folding converter shown in Fig. 17.35. Defining the folding rate to be the number of output transitions for a single folding block as $\mathrm{V}_{\text {in }}$ is swept over its input range, we see that the folding rate here is four. This folding rate determines how many bits are required in the MSB converter. The operation of this converter is as follows. The MSB converter determines whether the input signal, $\mathrm{V}_{\mathrm{in}}$, is in one of four voltage regions (i.e., between 0 and $1 / 4,1 / 4$ and $1 / 2,1 / 2$ and $3 / 4$, or $3 / 4$ and 1 ). Although the MSB converter is shown separately, these bits are usually determined by combining appropriate signals within the folding blocks. To determine the $2 \mathrm{LSBs}, \mathrm{V}_{1}$ to $\mathrm{V}_{4}$ produce a thermometer code for each of the four MSB regions. Note, however, that the four LSB latches are also used for different MSB regions and the thermometer code is inverted when $\mathrm{V}_{\text {in }}$ is between either $1 / 4$ and $1 / 2$ or $3 / 4$ and 1 . For example, as $\mathrm{V}_{\text {in }}$ increases from 0 to $1 / 4$, the thermometer code changes as $0000,0001,0011,0111,1111$. However, as $\mathrm{V}_{\text {in }}$ continues to increase to $1 / 2$, the code changes as 1110 , $1100,1000,0000$. Also, note that latch comparators can be used for the LSB set since the transitions are amplified by the folding blocks. In summary, folding reduces the number of latch comparators needed as compared to a flash
image_name:Fig. 17.35 A 4-bit folding A/D converter
description:The diagram illustrates a 4-bit folding A/D converter with a folding rate of four. The system is designed to convert an analog input voltage (\(V_{\text{in}}\)) into a 4-bit digital output. The key components and their functions are as follows:

1. **2-bit MSB A/D Converter**: This block handles the most significant bits (MSB) of the conversion process. It is responsible for determining the two highest order bits (\(b_1\) and \(b_2\)) of the output digital signal. The reference voltage for this converter is set at 1V (\(V_{\text{ref}} = 1 \text{V}\)).

2. **Folding Blocks**: There are four folding blocks, each associated with a different set of reference voltages (\(V_r\)). These blocks are responsible for transforming the input voltage into a waveform that can be easily compared with a threshold to determine the digital output.
- **Folding Block 1**: Processes \(V_{\text{in}}\) with reference voltages \(\frac{4}{16}, \frac{8}{16}, \frac{12}{16}, \frac{16}{16}\).
- **Folding Block 2**: Processes \(V_{\text{in}}\) with reference voltages \(\frac{3}{16}, \frac{7}{16}, \frac{11}{16}, \frac{15}{16}\).
- **Folding Block 3**: Processes \(V_{\text{in}}\) with reference voltages \(\frac{2}{16}, \frac{6}{16}, \frac{10}{16}, \frac{14}{16}\).
- **Folding Block 4**: Processes \(V_{\text{in}}\) with reference voltages \(\frac{1}{16}, \frac{5}{16}, \frac{9}{16}, \frac{13}{16}\).

3. **Latches**: Each folding block is followed by a latch, which captures the output of the folding block once it crosses a certain threshold. The latch outputs are denoted as \(V_1, V_2, V_3,\) and \(V_4\).

4. **Digital Logic**: This block processes the signals from the latches to produce the final digital output bits \(b_3\) and \(b_4\). The digital logic combines the outputs from the folding blocks and latches to determine the lower order bits of the digital output.

5. **Folding Block Responses**: On the right side of the diagram, the responses of each folding block are shown as graphs. These graphs illustrate how the output of each folding block varies with the input voltage \(V_{\text{in}}\), and how it crosses the threshold at specific reference voltages.

**Overall System Function**: The folding A/D converter reduces the number of comparators needed compared to a traditional flash converter by using folding blocks to process the input voltage in segments. This design allows for a more efficient conversion by folding the input signal and using fewer comparators to achieve the same resolution. The combination of folding blocks, latches, and digital logic enables the system to generate a 4-bit digital representation of the analog input voltage efficiently.
image_name:Folding block responses
description:The diagram illustrates the responses of folding blocks in a 4-bit folding A/D converter with a folding rate of four. The main focus is on the behavior of the folding block responses (V1, V2, V3, V4) and their interaction with the input voltage (Vin).

1. **Type of Graph and Function:**
- The graphs are response curves of folding blocks, showing voltage responses (V1, V2, V3, V4) as a function of input voltage (Vin).
- These are time-domain waveform graphs.

2. **Axes Labels and Units:**
- The x-axis represents the input voltage (Vin) in volts, ranging from 0 to 1 V.
- The y-axis represents the output voltage (V) of each folding block, also in volts, ranging from 0 to 1 V.
- Specific threshold levels are marked on each graph.

3. **Overall Behavior and Trends:**
- Each graph shows a periodic waveform with peaks at specific fractions of the reference voltage (Vref).
- The waveforms exhibit a folding behavior, repeating every 1/4 of the input range.
- The response curves rise to a peak and then fall back to zero, repeating this pattern.

4. **Key Features and Technical Details:**
- **V1 Response:** Peaks at Vin = 4/16, 8/16, 12/16.
- **V2 Response:** Peaks at Vin = 3/16, 7/16, 11/16, 15/16.
- **V3 Response:** Peaks at Vin = 2/16, 6/16, 10/16, 14/16.
- **V4 Response:** Peaks at Vin = 1/16, 5/16, 9/16, 13/16.
- Each response has a clearly defined threshold level, above which the output voltage is considered valid.

5. **Annotations and Specific Data Points:**
- Threshold lines are marked on each graph, indicating the voltage level that the folding block must exceed to register a response.
- The periodic nature of the responses aligns with the described folding rate, reducing the number of comparators needed compared to a full flash converter.

Fig. 17.35 A 4-bit folding A/D converter wit h a folding rate of four. (The MS B converter would usually be realized by combining some folding block signals.)
converter. For example, in a flash 4-bit converter, 16 latches would be required whereas only eight are needed in the 4 -bit folding example of Fig. 17.35. Specifically, four latches are used for the MSB converter and the other four are shown explicitly. In general, the savings can be greater (see Problem 17.29).

The folding blocks can be realized using cross-coupled differential pairs, as seen in the simplified bipolar circuit shown in Fig. 17.36. Here, four sets of differential-pair transistors are connected in such a way as to realize the input-output response shown in Fig. 17.36(b). The output signal $\mathrm{V}_{\text {out }}$ is related to the voltages $\mathrm{V}_{\mathrm{a}}$ and $\mathrm{V}_{\mathrm{b}}$ in an "or" type fashion. In other words, $\mathrm{V}_{\text {out }}$ is low only if both $\mathrm{V}_{\mathrm{a}}$ and $\mathrm{V}_{\mathrm{b}}$ are low; otherwise, $\mathrm{V}_{\text {out }}$ is high. With regard to the behavior of $V_{a}$ and $V_{b}$, note that $V_{b}$ remains low whenever $V_{i n}$ is less than $V_{r 3}$ or greater than $V_{r 4}$. However, $V_{a}$ remains low whenever $V_{i n}$ is greater than $V_{r 2}$ or less than $V_{r 1}$. Also, the cross coupling of adjacent differential pairs causes $V_{a}$ to go high when $V_{i n}$ is between $V_{r 1}$ and $V_{r 2}$, while $V_{b}$ goes high when $V_{\text {in }}$ is between $V_{r 3}$ and $V_{r 4}$. Such behaviors for $V_{a}$ and $V_{b}$ give rise to the folding output for $V_{o u t}$, as shown.
image_name:(a)
descriptionThe circuit is a folding block with a folding rate of four, designed to increase the frequency of the output signal compared to the input signal. The behavior of the circuit is such that Va goes high when Vin is between Vr1 and Vr2, while Vb goes high when Vin is between Vr3 and Vr4. This results in a folding output for Vout.
image_name:(b)
description:The graph in part (b) is a voltage transfer characteristic graph that depicts the input-output response of a folding block with a folding rate of four. The horizontal axis represents the input voltage $V_{in}$, while the vertical axis represents the output voltage $V_{out}$. The graph is plotted on a linear scale for both axes.

1. **Axes Labels and Units:**
- **Horizontal Axis:** $V_{in}$ (Input Voltage)
- **Vertical Axis:** $V_{out}$ (Output Voltage)

2. **Overall Behavior and Trends:**
- The graph shows a periodic waveform with two distinct peaks within the range of $V_{in}$. The waveform indicates a folding pattern, where the output voltage alternates between high and low states as the input voltage increases.
- The output voltage is high when the input voltage is between $V_{r1}$ and $V_{r2}$, as well as between $V_{r3}$ and $V_{r4}$. It is low outside these ranges.

3. **Key Features and Technical Details:**
- **Peaks:** The graph exhibits two prominent peaks, corresponding to the ranges where $V_{out}$ is high.
- **Valleys:** There are two low regions where the output voltage decreases significantly, corresponding to the regions where $V_{in}$ is less than $V_{r1}$, between $V_{r2}$ and $V_{r3}$, and greater than $V_{r4}$.
- **Critical Values:**
- The output voltage reaches a maximum value of $V_{CC} - V_{BE}$.
- The minimum output voltage is $V_{CC} - V_{BE} - I_b R_1$.

4. **Annotations and Specific Data Points:**
- The graph is annotated with critical input voltage points $V_{r1}$, $V_{r2}$, $V_{r3}$, and $V_{r4}$, which define the transition points for the folding behavior of the circuit.

This graph illustrates the folding mechanism, where the output voltage frequency is higher than the input frequency, demonstrating the folding rate's multiplying effect on the input signal frequency.

Fig. 17.36 A folding block with a folding-rate of four. (a) A possible single-ended circuit realization; (b) input-output response.

Some points worth mentioning here are that for full-scale input signals, the output signal from a folding block is at a much higher frequency than the input signal. In fact, the frequency of the folding block's output signal is equal to the multiplication of the frequency of the input signal times the folding rate. This multiplying effect limits the practical folding rate used in high-speed converters. Also, it should be mentioned that the circuit shown is a single-ended version, and differential circuits are almost always used in practical implementations.

Another point to note here is that while the folding approach reduces the number of latch comparators, a large input capacitance similar to that for a flash converter is also present with the folding circuit shown. In fact, flash converters have similar input stages of differential pairs of transistors for each comparator, but they are, of course, not cross coupled. Since the number of differential pairs in each folding block equals the folding rate, and the input signal goes to one side of each differential pair, it can be shown that the number of transistors driven by the input signal equals $2^{\mathrm{N}}$ - the same number as for a flash converter. To reduce this large input capacitance, folding converters also make use of an interpolating architecture. With an interpolate-by-two technique applied to the 4 bit example, the resulting architecture would be that shown in Fig. 17.37. Note that a new inverted signal $\bar{V}_{4}$ is required to connect the top folding block to the bottom one. Although the creation of this inverted signal is needed in a single-ended version, no extra circuitry is required in a differential version since it can be accomplished by simply cross-coupling the differential output wires.

Key Point: Folding is often combined with interpolation so that both the number of latches and the number of input amplifier differential pairs is reduced.

In [van Valburg, 1992], in order to realize a very-high-speed 8-bit converter, four folding blocks each with a folding rate of eight were used. Assuming $V_{\text {ref }}=1 \mathrm{~V}$, then the difference between reference voltages of adjacent inputs of a folding block was $1 / 8 \mathrm{~V}$. Each adjacent folding block was offset by $1 / 32 \mathrm{~V}$, giving zero crossings at each $1 / 32 \mathrm{~V}$. By interpolating between each adjacent folding block using four 8-tap resistor strings, zero crossings every $1 / 256 \mathrm{~V}$ were obtained (i.e., an 8-bit converter with 32 latch comparators connected to the interpolating resistor strings). The MSBs were realized by taking appropriate outputs from selected differential pairs and summing them separately to realize additional folding amplifiers with reduced folding rates. The converter also included circuitry to prevent bubble errors, as shown in Fig. 17.27. Other examples of folding converters are given in [van de Grift, 1987, and Colleran, 1993]. In addition, folding converters have been used in the internal operation of a two-step converter [Vorenkamp, 1992].
image_name:Fig. 17.37
description:The system block diagram in Fig. 17.37 represents a 4-bit folding A/D converter with a folding rate of four and an interpolate-by-two feature. The main components of this system include:

1. **2-bit MSB A/D Converter**: This block is responsible for determining the two most significant bits (MSBs) of the digital output. It operates with a reference voltage \( V_{ref} = 1 \text{ V} \).

2. **Folding Blocks**: There are two folding blocks in the diagram, each receiving the input voltage \( V_{in} \). These blocks perform the folding operation, which essentially maps a range of input voltages into a smaller range by folding the signal multiple times. The folding block outputs are labeled as \( V_1, V_2, V_3, \) and \( V_4 \).

3. **Latches**: Each folding block output is connected to a latch, which holds the signal for further processing.

4. **Digital Logic**: This block processes the latched signals and generates the two least significant bits (LSBs) \( b_3 \) and \( b_4 \) of the digital output.

5. **Resistors (R)**: These are used for voltage division and signal conditioning between the folding blocks and latches.

6. **Voltage Reference Points (\( V_r \))**: These reference voltages are used by the folding blocks to determine the thresholds for folding.

**Flow of Information**:
- The input voltage \( V_{in} \) is fed into the folding blocks, which fold the input signal based on the reference voltages \( V_r \).
- The outputs of the folding blocks (\( V_1, V_2, V_3, V_4 \)) are then latched and sent to the digital logic.
- The digital logic processes these signals to produce the LSBs \( b_3 \) and \( b_4 \).
- Simultaneously, the MSB A/D converter determines the MSBs \( b_1 \) and \( b_2 \) based on the input signal.

**Labels and Annotations**:
- The diagram includes graphs showing the folding block responses, indicating how the input voltage \( V_{in} \) relates to the threshold voltages.
- Reference voltages for folding are indicated as fractional values of \( V_{ref} \).

**Overall System Function**:
The primary function of this system is to convert an analog input voltage \( V_{in} \) into a 4-bit digital output. The use of folding blocks allows for a reduction in the number of comparators needed by effectively folding the input signal, while the digital logic and MSB converter work together to produce the complete digital output.
image_name:Folding-block responses
description:The graph titled "Folding-block responses" consists of four subplots, each representing the response of a folding block in a 4-bit folding A/D converter circuit. Each subplot shows a waveform with specific characteristics and thresholds.

1. **Type of Graph and Function:**
- The graph is a time-domain representation of voltage waveforms, showing the response of folding blocks to input voltage \( V_{in} \).

2. **Axes Labels and Units:**
- The x-axis represents the input voltage \( V_{in} \) in volts, with key increments marked as fractions of 16 (e.g., \( \frac{4}{16}, \frac{8}{16}, \frac{12}{16} \)).
- The y-axis represents the output voltage of each folding block in volts, ranging from 0 to 1 volt.

3. **Overall Behavior and Trends:**
- Each subplot shows a periodic waveform with peaks and valleys.
- The waveforms are sinusoidal-like, indicating a folding operation where the signal is folded back at specific intervals.
- The periodicity of the waveforms aligns with the input voltage thresholds marked on each graph.

4. **Key Features and Technical Details:**
- Each subplot has a threshold line indicating the point at which the output voltage reaches a significant level.
- The threshold levels are aligned with specific input voltage values, which are fractions of 16. These thresholds are critical for determining the digital output bits \( b_1, b_2, b_3, \) and \( b_4 \).
- The waveforms show a folding rate of four, meaning the waveform completes a cycle four times within the input voltage range from 0 to 1 volt.
- The response of each folding block is offset by different voltage levels, as indicated by the different threshold markers.

5. **Annotations and Specific Data Points:**
- The subplots are annotated with threshold lines and specific voltage fractions, indicating critical points for the conversion process.
- For example, the first subplot (\( V_1 \)) has thresholds at \( \frac{4}{16}, \frac{8}{16}, \frac{12}{16} \), and the second subplot (\( V_2 \)) at \( \frac{3}{16}, \frac{7}{16}, \frac{11}{16}, \frac{15}{16} \).
- These annotations help in understanding how the folding converter determines the most significant bits (MSBs) and least significant bits (LSBs) in the digital output.

Fig. 17.37 A 4-bit folding A/D converter with a folding rate of four and an interpolate-by-two. (The MSB converter would usually be realized by combining some folding-block signals.)
image_name:Fig. 17.37
description:The circuit is a 4-bit folding A/D converter with a folding rate of four and interpolation by two. It uses NPN transistors and current sources to determine the most significant bits (MSBs) and least significant bits (LSBs) in the digital output. The current sources provide biasing for the transistors, and the resistors are used to set voltage levels.

Fig. 17.38 Using the $\mathrm{V}_{1}$ folding block to also determine the top two MSBs.

### EXAMPLE 17.11

In Fig. 17.35, show how the two MSBs can be derived using internal signals from the folding blocks.

### Solution

The MSB, $b_{1}$ is determined by the input signal being above or below $\mathrm{V}_{\text {ret }} / 2$. Looking at Fig. 17.35, we see that the input is compared to the appropriate signal, $(8 / 16) \mathrm{V}_{\text {ref }}$ in the top folding block, producing $\mathrm{V}_{1}$. As a result, the MSB is easily obtained by using the collector current of the transistor connected to $\mathrm{V}_{\mathrm{r} 2}$ in the top folding block. Similarly, the top folding block uses references $4 / 16$ and $12 / 16$, which are needed to determine the second bit, $b_{2}$. In fact, the signal $\mathrm{V}_{1}$ can be used directly as the second bit, $b_{2}$, as seen in Fig. 17.35. Thus, the top two bits, $b_{1}$ and $b_{2}$, can be determined using the top folding block, as shown in Fig. 17.38.

## 17.9 TIME-INTERLEAVED A/D CONVERTERS

Very-high-speed A/D conversions can be realized by operating many A/Ds in parallel [Black, 1980]. The system architecture for a four-channel A/D is shown in Fig. 17.39. Here, $\phi_{0}$ is a clock at four times the rate of $\phi_{1}$ to $\phi_{4}$. Additionally, $\phi_{1}$ to $\phi_{4}$ are delayed with respect to each other by the period of $\phi_{0}$, such that each converter will get successive samples of the input signal, $\mathrm{V}_{\mathrm{in}}$, sampled at the rate of $\phi_{0}$. In this way, the four $A / D$ converters operate at one-quarter the rate of the input sampling frequency.

Key Point: Time-interleaved A/D converters permit high sampling frequency using several lower-rate $A / D$ converters and several phase-shifted clocks.

With this approach, the input $\mathrm{S} / \mathrm{H}$ making use of $\phi_{0}$ is critical, while the remaining four $\mathrm{S} / \mathrm{H}$ converters can have considerable jitter since the signal is already sampled at that point. Thus, sometimes the input $\mathrm{S} / \mathrm{H}$ is realized in a different technology, such as GaAs, while the remaining S/H circuits could be realized in silicon. An example of a 1 GHz 6-bit A/D converter using time interleaving and GaAs S/H circuits is described in [Poulton, 1987], where four bipolar converters operating at 250 MHz were used.

Key Point: A major limitation on the performance of time-interleaved converters is mismatch through the parallel signal paths in either their dc offset, gain, or sampling time. If they can be accurately quantified, sucherrors can be cancelled digitally.

It is also essential that the different $\mathrm{S} / \mathrm{H}$ and $\mathrm{A} / \mathrm{D}$ converter signal paths are extremely well matched, as mismatches will produce tones. For example, consider a m -way time-interleaved converter where one converter has a dc offset of, say, 100 mV . Such a system will produce every m -th digital word different from the other $(m-1)$ and hence tones at $f_{s} / m$ and its harmonics. These tones are independent of the input signal frequency or amplitude, and in fact will be present even if the input is zero. Another source of error arises when the different $\mathrm{S} / \mathrm{H}$ and $\mathrm{A} / \mathrm{D}$ converter circuits present different signal gains. In this case, since the gain is changing periodically, the input signal is effectively being multiplied by a periodic signal. Hence, with a sinusoidal input at $f_{i n}$ the output will contain harmonics at $\mathrm{kf}_{\mathrm{s}} / \mathrm{m} \pm \mathrm{f}_{\mathrm{in}}$ for integers k . Because these are intermodulation products, their frequency and amplitude depends upon the input signal frequency and amplitude. Mismatch between the bandwidth of the parallel signal paths results in frequency-dependent gain mismatch and all of the attendant error tones. Such nonideal behavior can be disastrous for many applications since the tones may reside well within the frequency of interest. A sketch of the output spectrum in the presence of offset and gain mismatches is
image_name:Fig. 17.39 A four-channel time-interleaved A/D converter with clock waveforms shown.
description:The system block diagram represents a four-channel time-interleaved Analog-to-Digital (A/D) converter with clock waveforms shown. This system is designed to increase the effective sampling rate of A/D conversion by interleaving multiple A/D converters.

1. **Main Components:**
- **Sample-and-Hold (S/H) Circuits:** There are five S/H blocks, each associated with a clock signal (ϕ0 to ϕ4). The first S/H block processes the input signal \( V_{in} \), while the remaining four S/H blocks prepare the signal for each of the four A/D converters.
- **N-bit A/D Converters:** There are four parallel A/D converters, each receiving input from its corresponding S/H circuit. These converters digitize the sampled analog signals into digital form.
- **Digital Multiplexer (Dig. mux):** This block combines the digital outputs from the four A/D converters into a single digital output stream.

2. **Flow of Information or Control:**
- The input signal \( V_{in} \) is first sampled by the initial S/H circuit, synchronized with the clock signal ϕ0.
- The sampled signal is then distributed to the four parallel S/H circuits, each controlled by a separate clock signal (ϕ1 to ϕ4). These clock signals are staggered in time to allow interleaving of the sampling process.
- Each S/H circuit feeds its output to an N-bit A/D converter, which converts the analog signal to digital form.
- The digital outputs from all four A/D converters are fed into the digital multiplexer, which interleaves them into a single digital output stream.

3. **Labels, Annotations, and Key Indicators:**
- The clock signals (ϕ0 to ϕ4) are annotated, showing their timing relationship and how they control the sampling and conversion process.
- The diagram includes waveforms to illustrate the timing of the clock signals, indicating their phase relationship and interleaving functionality.

4. **Overall System Function:**
- The primary function of this system is to increase the effective sampling rate by interleaving the operation of four A/D converters. By using staggered clock signals, the system can sample and convert the input signal at a higher rate than a single A/D converter could achieve. This technique is useful in applications requiring high-speed data acquisition without the need for a single high-speed converter.
image_name:Clock waveforms
description:The diagram represents a four-channel time-interleaved analog-to-digital (A/D) converter system, showing the clock waveforms associated with each channel. The system is designed to process an input signal \( V_{in} \) through multiple parallel paths, each consisting of a sample-and-hold (S/H) circuit followed by an N-bit A/D converter. The outputs from these converters are then combined through a digital multiplexer (Dig. mux) to produce a digital output.

**Type of Graph and Function:**
This is a block diagram illustrating the architecture of a time-interleaved A/D converter system with associated clock waveforms.

**Axes Labels and Units:**
There are no specific axes labels or units, as this is a schematic diagram. However, the clock signals \( \phi_0, \phi_1, \phi_2, \phi_3, \phi_4 \) are shown on the right side as time-domain waveforms.

**Overall Behavior and Trends:**
The diagram shows how the input signal \( V_{in} \) is split into four parallel paths, each synchronized with a distinct clock signal. The clock waveforms \( \phi_0 \) through \( \phi_4 \) are shown as square waves, with \( \phi_0 \) having a higher frequency compared to the others. The remaining clock signals \( \phi_1 \) to \( \phi_4 \) are staggered in time, indicating they are out of phase with each other to enable time-interleaving.

**Key Features and Technical Details:**
- **Sample-and-Hold (S/H) Circuits:** Each channel begins with an S/H circuit that captures the input signal at specific intervals dictated by the clock signal.
- **N-bit A/D Converters:** Following the S/H circuits, the signal is digitized by N-bit A/D converters.
- **Digital Multiplexer (Dig. mux):** The outputs from the A/D converters are fed into a digital multiplexer, which combines the signals into a single digital output stream.
- **Clock Signals:** The clock waveforms \( \phi_0 \) to \( \phi_4 \) are crucial for timing the sampling in each channel. \( \phi_0 \) appears to control the overall sampling rate, while \( \phi_1 \) to \( \phi_4 \) manage the timing for each individual channel.

**Annotations and Specific Data Points:**
- The clock waveforms are depicted with clear square waves, showing the timing relationship between each channel.
- The diagram emphasizes the role of clock signals in managing the interleaving process to increase the effective sampling rate of the system.

This diagram is essential for understanding how time-interleaved A/D converters work to handle higher sampling rates by distributing the sampling task across multiple channels, each operating at a lower rate.

Fig. 17.39 A four-channel time-interleaved A/D converter with clock waveforms shown.
presented in Fig. 17.40 with the sources of the various tones identified. Fortunately, if the mismatches between signal paths can be accurately identified they can be cancelled digitally as in Fig. 17.41. Even when cancelled, offset and gain mismatches increase the dynamic range that the constituent $A / D$ converters must be able to handle without nonlinearity.
image_name:Fig. 17.40
description:The graph in Fig. 17.40 is a frequency spectrum diagram representing the output of a 4-way time-interleaved A/D converter. The x-axis is labeled with frequency values, ranging from 0 to $f_s/2$, where $f_s$ is the Nyquist frequency. Key frequency points are marked, including $f_{in}$, $f_s/4$, $f_s/2$, and their respective offsets.

The y-axis is not explicitly labeled with units, but it typically represents amplitude or power in such spectral diagrams. The graph displays several distinct peaks:

1. **Input Signal Peak at $f_{in}$:** This peak represents the primary input signal frequency.
2. **Average DC Offset at 0:** A smaller peak is observed at 0, indicating the presence of a DC offset.
3. **DC Offset Mismatch Peaks:** These are additional peaks at $f_s/4$ and $f_s/2$, caused by mismatches in the DC offset across the channels.
4. **Gain Mismatch Peaks:** Peaks are also noted at $f_s/4 - f_{in}$ and $f_s/4 + f_{in}$, as well as $f_s/2 - f_{in}$, indicating gain mismatches.

Overall, the diagram illustrates how offset and gain mismatches introduce additional tones into the spectrum, which are critical to address for accurate signal conversion. The presence of these mismatches necessitates digital correction to improve the dynamic range and linearity of the A/D conversion process.

Fig. 17.40 Spectrum at the output of a 4-way time-interleaved A/D converter with offset and gain mismatches up to the converter's Nyquist frequency, $\mathrm{f}_{\mathrm{s}} / 2$.
image_name:Fig. 17.41 A four-channel time-interleaved A/D converter with digital correction for gain and offset mismatch.
description:The diagram illustrates a four-channel time-interleaved Analog-to-Digital (A/D) converter system designed to correct gain and offset mismatches digitally. The system is composed of several key components and processes the input signal (Vin) through a series of stages to produce a corrected digital output.

Main Components:
1. **Sample and Hold (S/H) Circuits:**
- There are five S/H circuits, one for the initial sampling (S/H with φ0) and four for each channel (S/H with φ1 to φ4).
- These circuits sample the input signal (Vin) and hold it steady for conversion.

2. **Analog Correction Blocks:**
- Each channel has an analog correction block that adjusts for offset (α1 to α4) and gain mismatches (β1 to β4) before conversion.

3. **N-bit A/D Converters:**
- Each channel is equipped with an N-bit A/D converter that converts the analog signal into a digital format.

4. **Digital Correction Blocks:**
- After conversion, digital correction blocks apply further corrections to the digital signal by subtracting the offset (−α1 to −α4) and dividing by the gain factor (1/β1 to 1/β4).

5. **Digital Multiplexer (Dig. mux):**
- This component combines the digitally corrected outputs from all four channels into a single digital output stream.

Flow of Information or Control:
- The input signal (Vin) is initially sampled by the first S/H circuit (controlled by φ0).
- The sampled signal is distributed to four parallel channels, each with its own S/H circuit (φ1 to φ4), which further sample and hold the signal for their respective paths.
- In each channel, analog correction is applied to address offset and gain mismatches.
- The corrected analog signal is then converted to digital format by the N-bit A/D converters.
- Digital correction is subsequently applied to the digital signal, ensuring that any remaining offset and gain errors are corrected.
- The corrected digital signals from all channels are combined by the digital multiplexer to produce a single coherent digital output.

Labels, Annotations, and Key Indicators:
- Each S/H circuit is labeled with its respective control signal (φ0 to φ4).
- Offset correction factors (α1 to α4) and gain correction factors (β1 to β4) are annotated at relevant points in the diagram.
- The digital correction process is clearly marked with operations for offset subtraction and gain division.

Overall System Function:
The primary function of this system is to convert an analog input signal into a digital output while correcting for any offset and gain mismatches that occur due to the time-interleaving of the A/D converters. This correction process enhances the accuracy and dynamic range of the conversion, ensuring a high-quality digital representation of the input signal.

Fig. 17.41 A four-channel time-interleaved A/D converter with digital correction for gain and offset mismatch.

## 17.10 KEY POINTS

- Dual-slope integrating conversion proceeds first by integrating the input for a fixed time period, then applying a known input to the integrator and measuring the time required for the integrator output to return to zero. [p. 648]
- Dual-slope conversion does not require accuracy in defining the integration time constant. Offset errors can be calibrated by performing an additional conversion using a known dc input quantity. [p. 648]
- Integrating converters inherently filter the input with a sin $x / x$ frequency response. [p. 649]
- Successive-approximation A/D converters are very versatile, capable of moderately high speed or accuracy with relatively low power. They are relatively simple circuits, in the simplest cases requiring only a single comparator, a bank of capacitors and switches, and a small digital logic circuit. Their biggest drawback is that they operate iteratively and therefore require many clock cycles to perform a single conversion. [p. 652]
- The accuracy of successive-approximation converters is often determined by that of the D/A converter. In the case of charge-redistribution converters, this role is played by a bank of comparators whose matching is important. [p. 653]
- Algorithmic converters are similar to successive-approximation converters, except that instead of an accurate D/A converter or capacitor bank, these converters require an accurate gain of two in order to perform the iterative search for a digital code that represents the analog input. [p. 662]
- Pipelined A/D converters are similar to algorithmic converters, but employ multiple circuits working on successive input samples simultaneously. Hence, they can complete a conversion on every clock cycle, providing higher throughput than algorithmic converters, but with the same latency. [p. 665]
- Introducing redundancy between successive stages in a pipelined converter permits simple digital correction of any offset in the comparators of each stage. [p. 670]
- Pipelined A/D converter performance is limited by nonlinearities and noise in the MDAC, and inaccuracy in the interstage gain, none of which are cancelled by simple digital correction. [p. 670]
- Switching part of the sampling capacitor into the feedback network provides the interstage gain with a higher feedback factor, and hence higher bandwidth, than a conventional switched-capacitor gain circuit. [p. 672]
- Multiple bits can be resolved in each stage, with digital correction, in order to reduce the number of opamps in a pipelined converter and decrease the number of clock cycles required for each conversion. [p. 673]
- Flash converters are generally capable of the fastest conversion speeds of any A/D architecture. However, their power consumption grows dramatically with the required resolution so they are usually reserved for converters where high speed and low or modest resolution is sought. [p. 673]
- Two-step converters may be considered a special case of pipelined converters where only 2 pipelined stages are needed. As with pipelined converters, digital error correction greatly relaxes the requirements on the first stage. [p. 679]
- The large capacitive input presented by flash $\mathrm{A} / \mathrm{D}$ converters can be reduced by using fewer input amplifiers and interpolating between them to create the missing intermediate values. [p. 680]
- A folding architecture requires fewer latches than a flash converter. It does so similar to a two-step converter, but uses analog preprocessing instead of an accurate D/A converter and gain amplifier. [p. 683]
- Folding is often combined with interpolation so that both the number of latches and the number of input amplifier differential pairs is reduced. [p. 686]
- Time-interleaved $\mathrm{A} / \mathrm{D}$ converters permit high sampling frequency using several lower-rate $\mathrm{A} / \mathrm{D}$ converters and several phase-shifted clocks. [p. 687]
- A major limitation on the performance of time-interleaved converters is mismatch through the parallel signal paths in either their dc offset, gain, or sampling time. If they can be accurately quantified, such errors can be cancelled digitally. [p. 688]
