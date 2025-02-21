# 16 Nyquist-Rate D/A Converters

In this chapter, a variety of methods are discussed for realizing integrated Nyquist-rate digital-to-analog converters (DAC). Nyquist-rate D/A converters can be roughly categorized into four main types: decoder-based, binaryweighted, thermometer-code, and hybrid. Oversampling D/A converters are discussed separately in Chapter 18 due to their importance and because they are best described using many signal processing concepts.

## 16.1 DECODER-BASED CONVERTERS

Perhaps the most straightforward approach for realizing an N-bit D/A converter is to create $2^{\mathrm{N}}$ reference signals and pass the appropriate signal to the output, depending on the digital input word. We refer to such D/A converters as decoder-based converters.

### 16.1.1 Resistor-String Converters

Key Point: Decoder-based D/A converters operate by creating a set of analog reference levels and selecting one by turning on appropriate switches selected by an input digital code.

One of the first integrated MOS 8 -bit D/A converters was based on selecting one tap of a segmented resistor string by a switch network [Hamadé, 1978]. ${ }^{1}$ The switch network was connected in a tree-like decoder, as in the 3-bit D/A converter shown in Fig. 16.1. Notice that there will be one, and only one, low-impedance path between the resistor string and the input of the buffer, and that path is determined by the digital input word, $\mathrm{B}_{\text {in }}$. In a CMOS implementation, transmission gates might be used rather than n -channel switches. However, when only n -channel pass transistors are used, the transistor-tree decoder can be laid out quite compactly since no contacts are required in the tree. Also, an n-channel-only approach is not much different in speed than a CMOS transmission-gate implementation; a transmission-gate approach has extra drain and source capacitance to ground, but this extra capacitance is offset by the reduced switch resistance, which is due to the parallel combination of $p$-channel and n -channel transistors. In addition, a transmission-gate implementation can operate closer to the positive voltage supply.

With a resistor-string approach, if we assume the buffer's offset voltage does not depend on its input voltage, the $\mathrm{D} / \mathrm{A}$ converter has guaranteed monotonicity since any tap on the resistor string must have a lower voltage than its upper, neighbor tap. Also, the accuracy of this D/A depends on the matching precision of R in the resistor string. Although this resistor-matching precision depends on the type of resistors used, the use of polysilicon resistors can result in up to approximately 10 bits of accuracy.

The delay through the switch network is the major limitation on speed. However, in a multiplying D/A, the delay through the resistor string would also be a major source of delay since $\mathrm{V}_{\text {ref }}$ would become a second input signal. A useful technique for estimating the settling-time behavior in RC type circuits (i.e., circuits that have only real-axis poles) is the zero-value time-constant approach described in Section 4.2.4 [Sedra, 1991].

[^0]image_name:Fig. 16.1 Resistor-string 3-bit D/A converter with a transmission-gate, tree-like decoder
description:The circuit is a 3-bit digital-to-analog converter (DAC) using a resistor string and transmission gate tree-like decoder. The switches are controlled by the digital inputs b1, b2, and b3, and their complements. The buffer provides low output impedance for driving loads.

Fig. 16.1 Resistor-string 3-bit D/A converter with a transmission-gate, tree-like decoder.

Specifically, the dominant high-frequency time constant is estimated as the sum of the individual time constants due to each of the capacitances when all other capacitances are set to zero (i.e., replaced with open circuits). To find the individual time constant for a given capacitance, independent voltage sources are replaced with ground (independent current sources are opened), and the resistance seen by that capacitor is determined.

#### EXAMPLE 16.1

Show that an estimate of the time constant for a network of $n$ resistors, each of size $R$ in series, with capacitive loading $C$ at each node (see Fig. 16.2), is given by $\tau=R C\left(n^{2} / 2\right)$. How much settling time is required for the output to settle to 0.1 percent of its final value?

#### Solution

The zero-value time-constant due to the first capacitor on the left is simply RC. The second capacitor from the left has an individual time constant of 2 RC and so on. Thus, the dominant high-frequency time constant, $\tau$, is estimated as

$$
\tau \cong R C(1+2+\cdots+n)
$$

The sum from 1 to $n$ can be shown to be equal to $n(n+1) / 2$ and, thus, for a large $n$, the dominant time constant
image_name:Fig. 16.2 Estimating the time constant for n resistors and capacitors in series.
description:The diagram labeled "Fig. 16.2 Estimating the time constant for n resistors and capacitors in series" illustrates a series circuit composed of multiple resistors (R) and capacitors (C). The circuit is shown as a chain of resistor-capacitor pairs connected in series, with the number of pairs represented by 'n'. The input voltage \( V_{in} \) is a step function, starting at \( V_p \) at time \( t = 0 \), indicating that the input voltage suddenly jumps to \( V_p \) at the initial moment.

On the right side of the diagram, the output voltage \( V_{out} \) is depicted as an increasing curve, which suggests an exponential charging behavior typical of RC circuits. The graph shows \( V_{out} \) rising from zero towards its final value, following the equation \( V_{out} \approx (1 - e^{-t/\tau}) V_p \), where \( \tau \) is the time constant.

The time constant \( \tau \) for this series configuration is estimated as \( \tau \approx RC \left( \frac{n^2}{2} \right) \), which is derived from the sum of the individual time constants for each RC pair. This formula accounts for the cumulative effect of the resistors and capacitors in series, emphasizing that the overall time constant increases with the square of the number of pairs, \( n^2 \), divided by 2.

In summary, the diagram provides a visual representation of the step response of a series RC circuit with multiple stages, highlighting how the time constant is influenced by the number of resistor-capacitor pairs in the circuit. The exponential rise of \( V_{out} \) is a key feature, demonstrating the typical behavior of an RC charging circuit over time.

Fig. 16.2 Estimating the time constant for n resistors and capacitors in series.
can be estimated by

$$
\tau \cong \operatorname{RC}\left(\frac{\mathrm{n}^{2}}{2}\right)
$$

Using this time constant to estimate the output voltage charging behavior, we have

$$
\mathrm{V}_{\text {out }} \cong\left(1-\mathrm{e}^{-(t / \tau)}\right) \mathrm{V}_{\mathrm{p}}
$$

Thus, for $\mathrm{V}_{\text {out }}$ to equal $0.999 \mathrm{~V}_{\mathrm{p}}$, we find that a time of about $7 \tau$ is needed.

In a higher-speed implementation, logic can be used for the decoder, and a single bus is connected to a single resistor-string node, as shown in Fig. 16.3. This approach takes more area for the decoder and also results in a large capacitive loading on the single bus because the $2^{\mathrm{N}}$ transistors' junctions are connected to the bus. However, if the digital decoder is pipelined, the $\mathrm{D} / \mathrm{A}$ can be moderately fast.

### 16.1.2 Folded Resistor-String Converters

To reduce the amount of digital decoding and large capacitive loading, a folded resistor-string $D / A$ can be used, as shown in Fig. 16.4 [Abrial, 1988]. This approach makes the decoding very similar to that for a digital memory, which reduces the total decoding area. To convert a digital input in this 4 -bit example, the most significant bits, $\left\{b_{1}, b_{2}\right\}$, determine the single word line to be selected (all others will remain low). This operation connects a block of four adjacent resistor nodes to the four-bit lines. One of these bit lines is then connected to the output buffer by the bit-line decoder. Notice that the total number of transistor junctions on the output line is now $2 \sqrt{2^{\mathrm{N}}}$ because a set of transistors is connected directly to the output line and another set is connected to the chosen bit line. Thus, for a 10-bit converter, this approach would have a capacitive load of 64 junctions, as opposed to 1,024 junctions when we use the digital-decoding approach shown in Fig. 16.3. Unfortunately, the increase in speed is not equal to this large ratio since, when a word line goes high, all the bit lines must be pulled to new voltage levels - not just the one bit line connected to the output buffer.

### 16.1.3 Multiple Resistor-String Converters

In this variation, a second tapped resistor string is connected between buffers whose inputs are two adjacent nodes of the first resistor string, as shown in Fig. 16.5 [Holloway, 1984]. In the shown 6-bit example, the three
image_name:Fig. 16.3 Resistor-string 3-bit D/A converter with digital decoding
description:This circuit is a 3-bit digital-to-analog converter (DAC) using a resistor string and a 3 to 1 of 8 decoder. The resistors are equally sized and connected between Vref and GND. The decoder selects one of the 8 taps on the resistor string based on the 3-bit input (b1, b2, b3). The selected voltage is buffered by an operational amplifier to produce the output Vout.

Fig. 16.3 Resistor-string 3-bit D/A converter with digital decoding.

MSBs determine which two adjacent nodes of the first resistor string are connected to the two intermediate buffers. The second resistor string linearly interpolates between the two adjacent voltages from the first resistor string. Finally, the output is determined by the lower LSBs where extra logic must take into account that sometimes the top intermediate buffer has the higher voltage, whereas at other times it has the lower voltage. This approach requires only $2 \times 2^{\mathrm{N} / 2}$ resistors, making it suitable for higher-resolution, low-power applications. This approach also has guaranteed monotonicity, assuming the opamps have matched, voltage-insensitive offset voltages. However, the opamps must be fast and low noise, which can be achieved using a BiCMOS process. Another point to note here is that, since the second resistor string is used to decode only the lower-order bits, the matching requirements of the second resistor string are not nearly as severe as those for the first string.

#### EXAMPLE 16.2

Assume that the first resistor string of a 10 -bit, multiple-R-string, D/A converter must match to 0.1 percent, and that the first string realizes the top 4 bits. What is the matching requirement of the second resistor string, which realizes the lower 6 bits?

#### Solution

Errors in the first resistor string correspond directly to errors in the overall D/A output. However, since the second resistor string forms the lower LSB bits ( 6 bits, in this case), errors in the matching of these resistors
image_name:Fig. 16.4
description:The circuit is a 4-bit folded resistor-string digital-to-analog converter (DAC). It consists of a 2 to 1 of 4 decoder for the top 2 bits (b1, b2) and another 2 to 1 of 4 decoder for the lower 2 bits (b3, b4). The resistors are arranged in a matrix to form word and bit lines, controlled by the decoders. The output is amplified by an operational amplifier to produce Vout.

Fig. 16.4 A 4-bit folded resistor-string D/A converter.
cause an error only in the LSB portion of the output voltage. As a result, the second resistor string need match only to

$$
\begin{equation*}
2^{4} \times 0.1 \%=1.6 \% \tag{16.1}
\end{equation*}
$$

### 16.1.4 Signed Outputs

In applications where negative output voltages are required, the bottom of the resistor string can be connected to $-\mathrm{V}_{\text {ref }}$. This requires a negative power supply, and the circuit needed to realize a dual power supply with exactly matched voltages is nontrivial since any error in matching will result in an offset error. Many papers on D/A converters assume that $-\mathrm{V}_{\text {ret }}$ is available but do not explain how it was obtained. If it is obtained off chip, the cost is significantly higher. One possibility is to use a switched-capacitor gain amplifier, as shown in Fig. 16.6, where a negative output can be realized by changing the clock phases of the input switches so an inverting amplifier is realized [Martin, 1987]. Another possibility is to sense the center tap of the resistor string and adjust $-\mathrm{V}_{\text {ref }}$ to get the center tap voltage equal to zero volts.
image_name:Fig. 16.5 Multiple R-string 6-bit D/A converter.
description:The circuit is a 6-bit D/A converter using a multiple R-string configuration. It utilizes two operational amplifiers and a string of equal-sized resistors to convert a digital signal to an analog output.

Fig. 16.5 Multiple R-string 6-bit D/A converter.

## 16.2 BINARY-SCALED CONVERTERS

Key Point: Binary-scaled D/A converters combine binary-weighted circuit quantities (currents, resistors, capacitors, etc.) under digital control to realize an analog quantity. Such techniques are generally hardware-efficient, but can be subject to significant nonlinearities.

The most popular approach for realizing at least some portion of D/A converters is to combine an appropriate set of signals that are all related in a binary fashion. This binary array of signals might be currents (in resistor or current approaches), but binary-weighted arrays of charge are also commonly used. In this section, resistor approaches are first discussed, followed by charge redistribution and current mode. Monotonicity is not guaranteed under such schemes since totally disparate sets of components are used to translate neighboring digital code words into analog voltages or currents, and large DNL is generally observed when large portions of the binary-weighted array are switched on and off. For example, this mismatch effect is usually the largest in a binary-array converter when the MSB is changed, resulting in the largest DNL at this location.

### 16.2.1 Binary-Weighted Resistor Converters

Binary-weighted resistor converters are popular for a bipolar technology so that bipolar differential pairs can be used for current switches. The basic architecture for a 4-bit converter is shown in Fig. 16.7.

If $b_{i}$ is a 1 , then the current to the $i$ th resistor comes from the virtual ground of the opamp; otherwise, it comes from ground. Therefore, we have

$$
\begin{align*}
V_{\text {out }} & =-R_{F} V_{\text {ref }}\left(-\frac{b_{1}}{2 R}-\frac{b_{2}}{4 R}-\frac{b_{3}}{8 R}-\ldots\right) \\
& =\left(\frac{R_{F}}{R} V_{\text {ref }}\right) B_{\text {in }} \tag{16.2}
\end{align*}
$$

where

$$
\begin{equation*}
B_{i n}=b_{1} 2^{-1}+b_{2} 2^{-2}+b_{3} 2^{-3}+\cdots \tag{16.3}
\end{equation*}
$$

image_name:Fig. 16.6
description:The circuit is a switched-capacitor gain amplifier using an op-amp to realize a signed output from a unipolar DAC output. The bit b1 is used as the sign bit.

Fig. 16.6 Using an SC gain amplifier to realize a signed output from a unipolar (positive) D/A converter output: $b_{1}$ high causes a negative output.
image_name:Fig. 16.7 Binary-weighted 4-bit resistor D/A converter.
description:The circuit is a binary-weighted 4-bit resistor D/A converter. It uses switches controlled by bits b1 to b4 to connect resistors 2R, 4R, 8R, and 16R to a reference voltage -Vref, forming a weighted sum at the input of an op-amp. The op-amp amplifies this sum to produce the output voltage Vout. The feedback resistor RF sets the gain of the op-amp.

Fig. 16.7 Binary-weighted 4-bit resistor D/A converter.

Although this approach does not require many resistors or switches, it does have some disadvantages. The resistor and current ratios are on the order of $2^{\mathrm{N}}$, which may be large, depending on N . This large current ratio requires that the switches also be scaled so that equal voltage drops appear across them for widely varying current levels. Also, monotonicity is not guaranteed. Finally, this approach is prone to glitches for high-speed operation, as discussed on page 633.

### 16.2.2 Reduced-Resistance-Ratio Ladders

To reduce the large resistor ratios in a binary-weighted array, signals in portions of the array can be scaled by introducing a series resistor, as shown in Fig. 16.8. Here, note that the voltage node, $\mathrm{V}_{\mathrm{A}}$, is equal to one-fourth the reference voltage, $\mathrm{V}_{\text {ref }}$, as a result of inserting the series resistor of value $3 R$. Also note that an additional $4 R$ resistor was added (to ground) such that resistance seen to the right of the $3 R$ resistor equals R. Straightforward analysis shows that this converter has the same relationship to the binary digital signals as in the previous binary-weighted case, but with one-fourth the resistance ratio. Note, however, the current ratio has remained unchanged. Finally, note that, by repeating this procedure recursively to a binary-weighted ladder, one arrives at a structure commonly referred to as an $R$-2R ladder, described next.

### 16.2.3 R-2R-Based Converters

A very popular architecture for D/A converters uses R-2R ladders. These ladders are useful for realizing binaryweighted currents with a small number of components and with a resistance ratio of only 2 , independent of the number of bits, N .

Consider the R-2R ladder network shown in Fig. 16.9. Analysis gives

$$
\begin{gather*}
R_{4}^{\prime}=2 R \\
R_{4}=2 R \| 2 R=R  \tag{16.4}\\
R_{3}^{\prime}=R+R_{4}=2 R \\
R_{3}=2 R \| R_{3}^{\prime}=R
\end{gather*}
$$

image_name:Fig. 16.8 Reduced-resistance-ratio 4-bit D/A converter.
description:This is a reduced-resistance-ratio 4-bit D/A converter using an R-2R ladder network. The switches b1 to b4 control the binary inputs, and the resistors form the ladder network. The op-amp is used for summing the currents and providing the output voltage Vout. The reference voltage is -Vref.

Fig. 16.8 Reduced-resistance-ratio 4-bit D/A converter.
image_name:Fig. 16.9 R-2R resistance ladder
description:This circuit is an R-2R ladder network used in a 4-bit digital-to-analog converter (DAC). The resistors form a ladder network, and the current sources (I1 to I4) correspond to the binary inputs. The reference voltage is Vref, and the ladder divides this voltage to produce the analog output.

Fig. 16.9 R-2R resistance ladder.
and so on. Thus, $\mathbf{R}_{\mathbf{i}}^{\prime}=2 \mathrm{R}$ for all i . This result gives the following current relationships:

$$
\begin{equation*}
I_{1}=\frac{V_{\text {ref }}}{2 R} \tag{16.5}
\end{equation*}
$$

Also, the voltage at node 2 is one-half the voltage at node 1 , giving

$$
\begin{equation*}
I_{2}=\frac{V_{\text {ref }}}{4 R} \tag{16.6}
\end{equation*}
$$

At node 3, the voltage divides in half once again, therefore

$$
\begin{equation*}
I_{3}=\frac{V_{\text {ref }}}{8 R} \tag{16.7}
\end{equation*}
$$

and so on.
Thus, the R-2R ladder can be used to obtain binary-weighted currents while using only a single-size resistor. (The resistors of size $2 R$ are made out of two resistors of size R , to improve matching properties.) As a result, this R-2R approach usually gives both a smaller size and a better accuracy than a binary-sized approach.

A 4-bit D/A converter that uses an R-2R ladder is shown in Fig. 16.10. For this R-2R-based circuit, we see that

Key Point: $R$-2R ladder D/A converters produce binary-weighted currents without the need for a complete array of binary-weighted resistors. Instead, only 2:1 component ratios are needed, a significant savings for high-resolution converters.

$$
\begin{equation*}
I_{r}=V_{\text {ref }} /(2 R) \tag{16.8}
\end{equation*}
$$

and

$$
\begin{equation*}
V_{\text {out }}=R_{F} \sum_{i=1}^{N} \frac{b_{i} I_{r}}{2^{i-1}}=V_{\text {ref }}\left(\frac{R_{F}}{R}\right) \sum_{i=1}^{N} \frac{b_{i}}{2^{i}} \tag{16.9}
\end{equation*}
$$

However, as already mentioned, although the resistance ratio has been reduced, the current ratio through the switches is still large, and thus the switch sizes are usually scaled in size to accommodate the widely varying current levels. One approach to reduce this current ratio is shown in Fig. 16.11, where equal currents flow through all the switches. However, this configuration is typically slower since the internal nodes of the R-2R ladder now exhibit some voltage swings (as opposed to the configuration in Fig. 16.10 where internal nodes all remain at fixed voltages).
image_name:Fig. 16.10 4-bit R-2R based D/A converter
description:This is a 4-bit R-2R ladder digital-to-analog converter. The circuit uses switches controlled by binary inputs (b1, b2, b3, b4) to determine the current path through the R-2R ladder network, which then converts the digital input into an analog output voltage (Vout). The operational amplifier provides the necessary gain and buffering for the output.

Fig. 16.10 4-bit R-2R based D/A converter.

### 16.2.4 Charge-Redistribution Switched-Capacitor Converters

Key Point: Charge-redistribution switchedcapacitor D/A converters sample a fixed reference voltage onto a binary-weighted capacitor array whose effective capacitance is determined by the input digital code. The sampled charge is then applied to a switched-capacitor gain stage to produce the analog output voltage.

The basic idea here is to simply replace the input capacitor of an SC gain amplifier by a programmable capacitor array (PCA) of binary-weighted capacitors, as shown in Fig. 16.12. As in the SC gain amplifier, the shown circuit is insensitive to opamp inputoffset voltage, 1/f noise, and finite-amplifier gain. Also, an additional sign bit can be realized by interchanging the clock phases (shown in parentheses) for the input switches.

It should be mentioned here that, as in the SC gain amplifier, carefully generated clock waveforms are required to minimize the voltage dependency of clock feed-through, and a deglitching capacitor should be used. Also, the digital codes should be changed only when the input side of the capacitors are connected to ground, and thus the switching time is dependent on the sign bit, which requires some extra digital complexity.
image_name:Fig. 16.11 R-2R ladder D/A converter
description:The circuit is an R-2R ladder D/A converter. It converts digital signals into analog output using resistors and current sources. The operational amplifier is used to buffer the output.

Fig. 16.11 R-2R ladder D/A converter with equal currents through the switches.
image_name:Fig. 16.12 Binary-array charge-redistribution D/A converter
description:The circuit is a binary-array charge-redistribution D/A converter. It uses capacitors and switches to convert a digital signal into an analog voltage output. The operational amplifier is used to buffer the output. The capacitors are arranged in a binary-weighted configuration to perform charge redistribution.

Fig. 16.12 Binary-array charge-redistribution D/A converter.

### 16.2.5 Current-Mode Converters

Current-mode D/A converters are very similar to resistor-based converters, but are intended for higher-speed applications. The basic idea is to switch currents to either the output or to ground, as shown in Fig. 16.13. Here, the output current is converted to a voltage through the use of $R_{F}$, and the upper portion of each current source always remains at ground potential. Implementations of current-mode D/A converters are more fully discussed in Section 16.3, where thermometer codes are introduced.

### 16.2.6 Glitches

Glitches are a major limitation during high-speed operation for converters that have digital logic, $\left\{\mathrm{b}_{1}, \mathrm{~b}_{2}, \ldots, \mathrm{~b}_{\mathrm{N}}\right\}$, directly related to switching signals. Glitches are mainly the result of different delays occurring when switching different signals. For example, when the digital input code changes from $0111 \ldots 1$ to $1000 \ldots 0$, all of the $\mathrm{N}-1$ LSBs turn off and the MSB turns on. However, it is possible that the currents due to the LSB switches will turn off slightly before the MSB current, causing the current to temporarily fall to zero. Alternatively, if the LSB switches
image_name:Fig. 16.13 Binary-weighted current-mode D/A converter
description:This circuit is a binary-weighted current-mode digital-to-analog converter (DAC). It uses current sources weighted by binary values and an operational amplifier to convert digital signals into analog output.

Fig. 16.13 Binary-weighted current-mode D/A converter.
image_name:I1
description:The graph is a time-domain waveform illustrating the behavior of currents in a binary-weighted current-mode digital-to-analog converter (DAC). It consists of three separate plots, each depicting a step change in current over time (t).

1. **Type of Graph and Function:**
- The graph type is a time-domain waveform, showing current versus time.

2. **Axes Labels and Units:**
- The horizontal axis is labeled 't' representing time.
- The vertical axes are labeled 'I1', 'I2', and 'I1 + I2', representing different current values.

3. **Overall Behavior and Trends:**
- Each plot shows a step function behavior, where the current suddenly increases to a certain level and remains constant.
- **I1 Plot:** The current I1 starts at zero and steps up to a higher constant value.
- **I2 Plot:** The current I2 also starts at zero and steps up, but it appears slightly delayed compared to I1.
- **I1 + I2 Plot:** This plot shows the combined effect of I1 and I2, with the current stepping up to a value equal to the sum of I1 and I2.

4. **Key Features and Technical Details:**
- The step change in each current indicates a digital switching action typical in DACs.
- The plots demonstrate how the MSB current (I1) and the sum of LSB currents (I2) interact.
- The delay between the step changes in I1 and I2 can cause glitches if not properly synchronized.

5. **Annotations and Specific Data Points:**
- No numerical values or specific annotations are provided, but the step nature of the plots is clear.

This graph is crucial for understanding the timing and synchronization challenges in binary-weighted DACs, as any mismatch in timing can lead to glitches in the output signal.
image_name:I2
description:The diagram consists of three time-domain waveforms and a circuit schematic. Each waveform is plotted with time \( t \) on the horizontal axis and current on the vertical axis. The currents are represented as \( I_1 \), \( I_2 \), and \( I_1 + I_2 \).

1. **Waveform for \( I_1 \):**
- The first graph shows a step function for the current \( I_1 \). It starts at zero and steps up to a constant positive value at a certain time.
- The waveform is characterized by a sharp transition from zero to the positive value, indicating a sudden increase in current.

2. **Waveform for \( I_2 \):**
- The second graph also depicts a step function for the current \( I_2 \). Similar to \( I_1 \), it starts at zero and steps up to a constant positive value.
- The timing of the step may differ slightly from \( I_1 \), which is crucial in analyzing glitches in DACs.

3. **Waveform for \( I_1 + I_2 \):**
- The third graph shows the sum of \( I_1 \) and \( I_2 \). It begins at zero and steps up to a value that is the sum of the two individual currents.
- The waveform reflects the combined effect of the two step inputs, highlighting any potential glitches due to timing mismatches.

4. **Circuit Schematic:**
- The right side of the diagram illustrates a binary-weighted current-mode DAC circuit.
- It includes two current sources labeled \( I_1 \) and \( I_2 \), which feed into an operational amplifier (OpAmp) circuit.
- The OpAmp is configured with a feedback resistor \( R_f \), and the output voltage \( V_{out} \) is taken from the output of the OpAmp.

This diagram is used to analyze glitches in the DAC output due to timing mismatches between \( I_1 \) and \( I_2 \). The glitches occur when the transition times of \( I_1 \) and \( I_2 \) do not perfectly align, causing a temporary deviation in the output current and thus the output voltage.
image_name:I1 + I2
description:The diagram consists of three time-domain waveforms labeled \(I_1\), \(I_2\), and \(I_1 + I_2\), alongside a schematic of a binary-weighted current-mode digital-to-analog converter (DAC). Each waveform is plotted against time \(t\) on the horizontal axis, with current on the vertical axis.

1. **\(I_1\) Waveform:**
- **Type:** Step function.
- **Behavior:** The waveform starts at zero and steps up to a constant positive value, remaining steady thereafter.
- **Axes:** The vertical axis represents current \(I_1\), and the horizontal axis represents time \(t\).

2. **\(I_2\) Waveform:**
- **Type:** Step function.
- **Behavior:** Similar to \(I_1\), this waveform begins at zero and steps up to a constant positive value, but the timing of this step is slightly delayed compared to \(I_1\).
- **Axes:** The vertical axis represents current \(I_2\), and the horizontal axis represents time \(t\).

3. **\(I_1 + I_2\) Waveform:**
- **Type:** Composite step function.
- **Behavior:** This waveform combines the effects of \(I_1\) and \(I_2\). It initially follows \(I_1\), stepping up from zero, and then increases further when \(I_2\) steps up, resulting in a higher final current level.
- **Axes:** The vertical axis represents the combined current \(I_1 + I_2\), and the horizontal axis represents time \(t\).

4. **Schematic:**
- The schematic on the right shows a DAC circuit with current sources \(I_1\) and \(I_2\) feeding into an operational amplifier (OpAmp) with a feedback resistor \(R_f\). The output voltage \(V_{out}\) is taken from the OpAmp's output.

**Overall Behavior and Trends:**
- The waveforms illustrate the step changes in current as each binary-weighted current source is activated. The combination of \(I_1\) and \(I_2\) into \(I_1 + I_2\) demonstrates how the DAC generates a higher current output when both sources are active.

**Key Features:**
- The step changes in \(I_1\) and \(I_2\) are critical for understanding how glitches can occur if the timing of these steps is not perfectly synchronized, as described in the context.
image_name:Binary-weighted current-mode D/A converter
description:This circuit is a binary-weighted current-mode digital-to-analog converter (DAC). It uses current sources weighted by binary values and an operational amplifier to convert digital signals into analog output. The diagram also illustrates glitches that occur due to timing mismatches between the MSB and LSB currents.

Fig. 16.14 Glitches. $\mathrm{I}_{1}$ represents the MSB current, and $\mathrm{I}_{2}$ represents the sum of the $\mathrm{N}-1 \mathrm{LSB}$ currents. Here, the MSB current turns off slightly early, causing a glitch of zero current.
turn off slightly after the MSB current, the current will temporarily go to its maximum value. In either case, a glitch occurs at the output unless these two delays are exactly matched, which is highly unlikely since the branches have different currents. This glitch phenomenon is illustrated in Fig. 16.14.

The glitch disturbance can be reduced by limiting the bandwidth (by placing a capacitor across the resistor $R_{f}$ in Fig. 16.14), but this approach slows down the circuit. Another approach is to use a sample and hold on the output signal. Finally, the most popular way to reduce glitches is to modify some or all of the digital word from a binary code to a thermometer code, as discussed next.

## 16.3 THERMOMETER-CODE CONVERTERS

Key Point: Thermometer-code converters employ an array of $2 \mathrm{~N}-1$ unitary equallysized signal quantities. A digital thermometer code selects the appropriate number of these unitary signal quantities, summing them to produce the analog output with guaranteed monotonicity and better static linearity than binary-weighted converters.

Another method for realizing a $\mathrm{D} / \mathrm{A}$ converter is to digitally recode the input value to a thermometer-code equivalent. A thermometer code differs from a binary one in that a thermometer code has $2^{\mathrm{N}}-1$ digital inputs to represent $2^{\mathrm{N}}$ different digital values. Clearly, a thermometer code is not a minimal representation since a binary code requires only N digital inputs to represent $2^{\mathrm{N}}$ input values. However, as we will see, a thermometer-based converter does have advantages over its binary counterpart, such as low DNL errors, guaranteed monotonicity, and reduced glitching noise.

Typically, in a thermometer-code representation, the number of 1 s represents the decimal value. For example, with a 3-bit binary input, the decimal value 4 is binary coded as 100 while its thermometer equivalent is 0001111. The codes for the remaining values in this 3-bit example are shown in Table 16.1.

One method to realize a $\mathrm{D} / \mathrm{A}$ converter with the use of a thermometer-code input is to build $2^{\mathrm{N}}-1$ equal-sized resistors and switches attached to the virtual ground of an opamp, as shown in Fig. 16.15. Note that monotonicity is guaranteed here since, when the binary input changes to the next higher number, one more digital value in the thermometer code goes high, causing additional current to be drawn out of the virtual ground and forces the opamp output to go some amount higher (never lower). This is not necessarily the case for a binary-array D/A converter since mismatches between elements may cause the output to go lower even though the digital input value is increased.

Table 16.1 Thermometer-code representations for 3-bit binary values.

| Decimal | Binary |  |  | Thermometer Code |  |  |  |  |  |  |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
|  | $b_{1}$ | $b_{2}$ | $b_{3}$ | $d_{1}$ | $\mathrm{d}_{2}$ | $d_{3}$ | $d_{4}$ | $d_{5}$ | $d_{6}$ | $\mathrm{d}_{7}$ |
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| 1 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 1 |
| 2 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 1 |
| 3 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 1 | 1 | 1 |
| 4 | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 | 1 |
| 5 | 1 | 0 | 1 | 0 | 0 | 1 | 1 | 1 | 1 | 1 |
| 6 | I | 1 | 0 | 0 | 1 | 1 | 1 | 到 | 1 | 1 |
| 7 | 1 | 1 | 1 |  | 1 | 1 | 到 | 到 | 1 | 1 |

Perhaps more importantly, a D/A converter based on a thermometer code greatly minimizes glitches, as compared to binary-array approaches, since banks of resistors are never exchanged at slightly different times when the output should change by only 1 LSB. It should also be mentioned here that latches can be used in the binary-to-thermometer code conversion such that no glitches occur in the digital thermometer-code words and pipelining can be also used to maintain a high throughput speed.

It is also of interest to note that the use of a thermometer code does not increase the size of the analog circuitry compared to a binary-weighted approach. In a 3-bit binary-weighted approach, the resistor values of $R, 2 R$, and $4 R$ are needed for a total resistance of $7 R$. This total value is the same as for the 3 -bit thermom-eter-code approach shown in Fig. 16.15, and since resistors are created on an integrated circuit using area that is proportional to their size, each approach requires the same area (ignoring interconnect). The same argument can be used to show that the total area required by the transistor switches is the same since transistors are usually size-scaled in binary-weighted designs to account for the various current densities. All transistor switches in a thermometer-code approach are of equal sizes since they all pass equal currents. Finally, it should be mentioned that a thermometer-code charge-redistribution D/A can also be realized, as shown in Fig. 16.16.
image_name:Fig. 16.15 A 3-bit thermometer-based D/A converter.
description:This is a 3-bit thermometer-based D/A converter. The circuit uses a binary-to-thermometer code conversion to control switches connected to resistors, forming a resistor ladder network. The output is processed through an operational amplifier to generate the analog output voltage Vout.

Fig. 16.15 A 3-bit thermometer-based D/A converter.
image_name:Fig. 16.16 Thermometer-code charge-redistribution D/A converter
description:This circuit is a thermometer-code charge-redistribution D/A converter. It uses a network of capacitors and switches to perform digital-to-analog conversion. The capacitors are charged and discharged in a sequence determined by the thermometer code, and an operational amplifier processes the resulting voltage to produce the analog output Vout. The top capacitors are connected to ground, and the bottom capacitors are connected to Vref.

Fig. 16.16 Thermometer-code charge-redistribution D/A converter.

### 16.3.1 Thermometer-Code Current-Mode D/A Converters

A thermometer-code-based current-mode D/A converter, shown in Fig. 16.17, has been the basis for a variety of designs (see, for example, [Miki, 1986; Chi, 1986; and Letham, 1987]). Here, thermometer-code decoders are used for both the row and column decoders, resulting in inherent monotonicity and good DNL errors. Current is switched to the output when both row and column lines for a cell are high. Also, in high-speed applications, the output feeds directly into an off-chip $50-\Omega$ or $75-\Omega$ resistor, rather than an output opamp. Note that cascode current sources are used here to reduce current-source variation due to voltage changes in the output signal, $\mathrm{V}_{\text {out }}$.

Note the need here for precisely timed edges of $\mathrm{d}_{\mathrm{i}}$ and $\overline{\mathrm{d}}_{\mathrm{i}}$. If both logic levels are high simultaneously, $\mathrm{V}_{\text {out }}$ is shorted to ground. If both logic levels are low at the same time, the drain of $Q_{3}$ is pulled low and the circuit
image_name:Fig. 16.17 Thermometer-code current-mode D/A converter
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: Vout, G: di_bar}
name: Q2, type: NMOS, ports: {S: GND, D: Vout, G: Vb}
name: Q3, type: NMOS, ports: {S: Vout, D: GND, G: di}
name: Q4, type: NMOS, ports: {S: Vout, D: GND, G: Vb}
name: Current Sources, type: CurrentSource, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a thermometer-code current-mode D/A converter. Q1 and Q2 form a current switch, while Q3 and Q4 implement a cascode current source. All current sources are of equal value. The circuit uses row and column decoders for selecting the current sources in the array.
image_name:
description:The diagram represents a thermometer-code current-mode Digital-to-Analog Converter (DAC) system. It primarily consists of the following components:

1. **Current Sources:**
- Multiple identical current sources are arranged in parallel. Each current source is connected to a switch controlled by a logic signal. These current sources ensure uniform current distribution across the circuit.

2. **Current Switch (Q1 and Q2):**
- Transistors Q1 and Q2 form a current switch that directs the current either to the output or to ground, depending on the logic levels of the control signals \( \overline{d_i} \) and \( d_i \).

3. **Cascode Current Source (Q3 and Q4):**
- Transistors Q3 and Q4 are configured as a cascode current source to increase the output impedance and reduce the variation in current due to changes in output voltage \( V_{out} \).

4. **Logic Control Signals:**
- The signals \( \overline{d_i} \) and \( d_i \) are crucial for the operation of the current switch. They must be precisely timed to avoid short-circuiting the output to ground or pulling the drain of Q3 low.

5. **Bias Voltages:**
- Bias voltages are applied to the gates of Q3 and Q4 to maintain proper operation of the cascode current source.

6. **Decoders (Row and Column):**
- The system includes a row decoder and a column decoder. These decoders select which current source in the array is active based on the input digital code.

7. **I-Source Array:**
- The I-Source array is a matrix of current sources that are selectively activated by the decoders.

8. **Output Voltage \( V_{out} \):**
- The output voltage is taken from the node where the current sources are connected, and it is influenced by the selected current paths through the row and column decoders.

Flow of Information:
- The digital input code is processed by the row and column decoders to select specific current sources in the I-Source array.
- The selected current sources direct current through the current switch formed by Q1 and Q2.
- The cascode current source formed by Q3 and Q4 ensures stable output by maintaining high output impedance.
- The output voltage \( V_{out} \) is generated based on the combined effect of the activated current sources and the logic control signals.

Overall System Function:
The primary function of this system is to convert a thermometer-coded digital input into an analog output voltage. The precise control of current switching and cascode stabilization ensures accurate and stable DAC operation, which is crucial for high-speed and high-precision applications.

Fig. 16.17 Thermometer-code current-mode D/A converter. $\mathrm{Q}_{1}$ and $\mathrm{Q}_{2}$ form the current switch, whereas $\mathrm{Q}_{3}$ and $\mathrm{Q}_{4}$ implement a cascode current source.
takes longer to respond. To avoid the use of two logic driving levels, the gate of $Q_{2}$ should be connected to a dc bias voltage, as described in the next approach.

### 16.3.2 Single-Supply Positive-Output Converters

The architecture for a fast single-supply positive-output D/A (often used in video RAMs, which are known as RAMDACs) is shown in Fig. 16.18 [Colles, 1988]. Here, a matched feedback loop is used to set up accurate known current-source biasing. (Note that the opamp input connections appear reversed but are correct due to signal inversion by $\mathrm{Q}_{4}$.) Also, to maintain accurate current matching that is independent of $\mathrm{V}_{\text {out }}$, one side of each differential current-steering pair is connected to $\mathrm{V}_{\text {bias }}$, rather than to the inversion of the bit signal. For example, when the current is steered to the output through $\mathrm{Q}_{2}$, the drain-source voltage across the current source, $\mathrm{Q}_{3}$, remains mostly constant if $\mathrm{V}_{\text {out }}$ stays near zero, such that $\mathrm{Q}_{2}$ remains in the active region. Thus, $\mathrm{Q}_{2}$ and $\mathrm{Q}_{3}$ effectively form a cascode current source when they drive current to the output.

To maximize speed in this converter, the voltage swing at the common connections of the current switches (for example, $Q_{1}, Q_{2}$, and $Q_{3}$ ) should be small. To keep this swing small, this common connection should be at a voltage where the output transistors are just turned off when the current is steered to ground. It should also be noted that when
image_name:Fig. 16.18 A single-supply positive-output D/A converter
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: d1, G: Vbias}
name: Q2, type: NMOS, ports: {S: d1, D: d2, G: Vbias}
name: Q3, type: NMOS, ports: {S: d2, D: Vout, G: Vbias}
name: Q4, type: NMOS, ports: {S: Vout, D: VDD, G: Vbias}
name: Rref, type: Resistor, value: Rref, ports: {N1: d1, N2: GND}
name: 50 Ω, type: Resistor, value: 50 Ω, ports: {N1: Vout, N2: GND}
name: OpAmp, type: OpAmp, value: Vref, ports: {InP: Vref, InN: d1, OutP: VDD}
]
extrainfo:This circuit is a single-supply positive-output digital-to-analog converter (DAC). It uses a cascode current source formed by Q2 and Q3 to drive current to the output. The design maximizes speed by minimizing voltage swing at the common connections of the current switches. The circuit does not require two logic driving signals and can be clocked at maximum rate without precise timing.

Fig. 16.18 A single-supply positive-output D/A converter.
a switch is turning on or off, the switching feedthrough from the digital input connected to the grounding transistor (for example, $\mathbf{Q}_{1}$ ) actually enhances the switching. Finally, note that this design does not use two logic driving signals, $\mathrm{d}_{\mathrm{i}}$ and $\overline{\mathrm{d}}_{\mathrm{i}}$, and can therefore be clocked at the maximum rate without the need for precisely timed edges.

### 16.3.3 Dynamically Matched Current Sources

The use of dynamic techniques with current switching is a method for realizing very well-matched current sources (up to 16-bit accuracy) for audio-frequency D/A converters [Schouwenaars, 1988].

This approach was used to design a 16-bit audio-frequency D/A converter, where the 6 MSB were realized using a thermometer code. Since the accuracy requirements are reduced for the remaining bits, a binary array was used in their implementation. The basic idea for realizing 63 accurately matched current sources for the 6 MSBs is illustrated in Fig. 16.19. Here, we want to set all the currents $\mathrm{I}_{\mathrm{di}}$ to the same precise value, independent of transistor mismatches and charge injection. To accomplish this high degree of matching, each current source $\mathrm{I}_{\mathrm{di}}$ is periodically calibrated with the use of a single reference current source, $\mathrm{I}_{\mathrm{ref}}$, through the use of the shift register. In other words, once calibration is accomplished on $\mathrm{I}_{\mathrm{d} 1}$, the same current source, $\mathrm{I}_{\mathrm{ref}}$, is used to set the next current source, $\mathrm{I}_{\mathrm{d} 2}$, to the same value as $\mathrm{I}_{\mathrm{d} 1}$, and so on. Before proceeding to see how this calibration is accomplished, it is worth mentioning that the values of $\mathrm{I}_{\mathrm{di}}$ need not precisely equal $\mathrm{I}_{\mathrm{ref}}$ but do need to accurately match each other. Therefore, any common errors in the calibration stage are not a problem. Also, note that 64 current sources are calibrated, even though only 63 are required for the 6 MSB . This extra current source is needed so that the D/A converter can continuously operate, even when one of the current sources is being calibrated.

The method for calibrating and using one of the current sources is shown in Fig. 16.20, for $\mathrm{I}_{\mathrm{dl}}$. During calibration, the current source is connected to the reference current $I_{r e f}$, while $Q_{1}$ is configured in a diode-connected mode. This places whatever voltage is necessary across the parasitic $C_{g s}$ so that $I_{d 1}$ equals $I_{r e f}$. When $S_{1}$ is opened, $I_{d 1}$ remains nearly equal to $I_{r e t}$, assuming the drain-source voltage of $Q_{1}$ doesn't change and the clock feedthrough and charge injection of $S_{1}$ are small. During regular system use, the gate voltage (and therefore current) is determined by the voltage stored on the parasitic capacitance, $C_{g s}$.
image_name:Fig. 16.19 Dynamically matching current sources for 6 MSB
description:
[
name: I_ref, type: CurrentSource, ports: {Np: VDD, Nn: Shift_register}
name: I_d1, type: CurrentSource, ports: {Np: Switch_network, Nn: GND}
name: I_d2, type: CurrentSource, ports: {Np: Switch_network, Nn: GND}
name: I_d3, type: CurrentSource, ports: {Np: Switch_network, Nn: GND}
name: I_d4, type: CurrentSource, ports: {Np: Switch_network, Nn: GND}
name: I_d5, type: CurrentSource, ports: {Np: Switch_network, Nn: GND}
name: I_64, type: CurrentSource, ports: {Np: Switch_network, Nn: GND}
]
extrainfo:The circuit diagram illustrates a dynamically matching current source system for a 6 MSB DAC. It uses a shift register to control switches that route current from multiple current sources (I_d1 to I_64) to a switch network, which then interfaces with a D/A converter. The reference current I_ref is used to calibrate the system.

Fig. 16.19 Dynamically matching current sources for 6 MSB.
image_name:Fig. 16.20
description:The circuit diagram illustrates a dynamically setting current source system for a 6 MSB DAC. It uses a shift register to control switches that route current from multiple current sources to a switch network, interfacing with a D/A converter. The reference current I_ref is used for calibration. The NMOS transistor Q1 is used to control the flow of current, and the capacitor C_gs is likely used for stability or filtering purposes.

Calibration
image_name:Fig. 16.20 Dynamically setting a current source, I_{d1}
description:The circuit diagram illustrates a dynamically setting current source system for a 6 MSB DAC. It uses a shift register to control switches that route current from multiple current sources to a switch network, interfacing with a D/A converter. The reference current I_ref is used for calibration. The NMOS transistor Q1 is used to control the flow of current, and the capacitor C_gs is likely used for stability or filtering purposes. Selecting and summing current signals can provide high-speed D/A conversion. Output-impedance enhancement techniques may be needed to ensure the currents remain constant with respect to variations in output voltage. Calibration may also be used to ensure matching. A major limitation in matching the 64 current sources is due to the differences in clock feedthrough and charge injection.

Regular usage

Fig. 16.20 Dynamically setting a current source, $\mathrm{I}_{\mathrm{d} 1}$.

Key Point: Selecting and summing current signals can provide high-speed $D / A$ conversion. Output-impedance enhancement techniques may be needed to ensure the currents remain constat with respect to variations in output voltage. Calibration may also be used to ensure matching.

A major limitation in matching the 64 current sources is due to the differences in clock feedthrough and charge injection of the switches $\mathrm{S}_{\mathrm{i}}$. Since mismatches will always exist between different switches, the best way to keep all current sources equal is to minimize the total amount of clock feedthrough and charge injection. These nonideal effects can be minimized by having the capacitance $\mathrm{C}_{\mathrm{gs}}$ and bias voltage $\mathrm{V}_{\mathrm{GS}}$ large. ( A large $\mathrm{V}_{\mathrm{Gs}}$ voltage implies that any voltage difference will cause a smaller percentage current deviation.) To accomplish these requirements, the current source $0.9 \mathrm{I}_{\text {ref }}$ was added in parallel to $\mathrm{Q}_{1}$, so that $\mathrm{Q}_{1}$ needs only to source a current near $0.1 \mathrm{I}_{\mathrm{ref}}$. With such an arrangement, a large, low-transconductance device can be used (a $\mathrm{W} / \mathrm{L}=1 / 8 \mathrm{might}$ be used).

Finally, each current source must be recalibrated before the leakage currents (on the order of $10 \mathrm{pA} / \mu \mathrm{m}^{2}$ of junction area) on $\mathrm{C}_{\mathrm{gs}}$ cause the current source to deviate by 0.5 LSB . Fortunately, having a large $\mathrm{C}_{\mathrm{GS}}$ and $\mathrm{V}_{\mathrm{GS}}$ has the added benefit of extending this calibration interval (every 1.7 ms in [Schouwenaars, 1988]).

Many other additional details are described in [Schouwenaars, 1988]. For example, during calibration, a p -channel-input common-gate amplifier is added to the diode-connected loop. This is typically done in dynamic switched-current circuits to control the drain-source voltage of $Q_{1}$ (i.e., to keep it constant independent of the actual current and to keep it matched to its value during regular use) and to speed up the circuit by decreasing the effect of parasitic capacitances on the large $I_{\text {ref }}$ bus. Also, dummy switches are connected to $S_{1}$ to help minimize clock feedthrough by partially cancelling the charge injected.

## 16.4 HYBRID CONVERTERS

Key Point: A hybrid converter combines different D/A architectures to realize different portions of the converter design.

Combining the techniques discussed in Sections 16.1-16.3 for realizing different portions of a D/A converter results in hybrid designs. Hybrid designs are an extremely popular approach for designing converters because they combine the advantages of different approaches. For example, it is quite common to use a thermometer-code approach for the top few MSBs while using a binary-scaled technique for the lower LSBs. In this way, glitching is significantly reduced and accuracy is high for the MSB where it is needed most. However, in the LSBs where glitching and accuracy requirements are much reduced, valuable circuit area is saved with a binary-scaled approach. This section discusses some useful hybrid designs.

### 16.4.1 Resistor-Capacitor Hybrid Converters

It is possible to combine tapped resistor strings with switched-capacitor techniques in a number of different ways. In one approach, an SC binary-weighted D/A converter has its capacitors connected to adjacent nodes of a resistorstring D/A converter, as shown in Fig. 16.21 [Yang, 1989]. Here, the top 7 bits determine which pair of voltages across a single resistor is passed on to the 8 -bit capacitor array. For example, if the top 7 bits are 0000001, then switches $S_{1}$ and $S_{2}$ would be closed, while the other $S_{i}$ switches would remain open. The capacitor array then performs an 8 -bit interpolation between the pair of voltages by connecting the capacitors associated with a 1 to the higher voltage and the capacitors associated with a 0 to the lower voltage. This approach gives guaranteed monotonicity, assuming the capacitor array is accurate to only 8 bits. The converter in [Yang, 1989] has 15-bit monotonicity, without trimming, and 100-kHz sampling frequencies for a very-low-power $10-\mathrm{mW}$ realization.

### 16.4.2 Segmented Converters

The segmented D/A converter is a popular example of a hybrid converter [Schoeff, 1979; Grebene, 1984; Schouwenaars, 1988]. A 6-bit segmented D/A converter is shown in Fig. 16.22. In this approach, the two MSB currents are
image_name:Fig. 16.21
description:This circuit is a 15-bit resistor-capacitor hybrid D/A converter. It uses a combination of resistors, capacitors, and switches to convert digital signals into analog outputs. The diagram also shows the timing signals \( \phi_1 \) and \( \phi_2 \) for controlling the switches.
image_name:
description:The diagram is a schematic of a resistor-capacitor hybrid D/A converter. It features a combination of resistors, capacitors, switches, and an operational amplifier to achieve digital-to-analog conversion.

**Type of Diagram:**
- Schematic of a digital-to-analog converter (DAC).

**Components and Connections:**
- **Resistors (R1 to R128):** These are arranged in a series, with switches (S0 to S128) connected across them to control the current path.
- **Capacitors (CAO, CA7, CAB, CB, CC):** These are used for charge storage and transfer. Capacitor values are given as multiples of a unit capacitance C (e.g., CAO = C, CA7 = 64C, CAB = 128C, CB = 256C, CC = 256C).
- **Switches (S0 to S128):** These are controlled by clock phases (φ1, φ2, φA0, φA7, φA8, φB0, φB7, φB8) to route the current and charge.
- **Operational Amplifier:** The output from the capacitive network is fed into an op-amp to produce the analog output voltage (V_out).

**Clock Phases:**
- The diagram includes timing signals (φ1, φ2) that control the switches, ensuring proper sequencing of charge transfer.
- Additional clock phases (φAi, φBi) are shown, which likely control specific segments of the conversion process.

**Bit Segmentation:**
- The converter is segmented into two parts: a 7-bit segment and an 8-bit segment, as indicated by the arrows at the bottom of the diagram. This segmentation helps in reducing glitches and improving monotonicity.

**Overall Functionality:**
- The converter uses a combination of resistor ladder network and capacitive charge redistribution to perform digital-to-analog conversion.
- The segmentation and use of thermometer coding for MSB currents help minimize glitches, enhancing the converter's performance.

**Key Features:**
- The use of multiple clock phases indicates a pipelined or sequential operation, crucial for timing the conversion process correctly.
- The schematic emphasizes the importance of precise control over the switching and charge redistribution to achieve accurate conversion.

Fig. 16.21 One example of a 15-bit resistor-capacitor hybrid D/A converter.
obtained in one segment from three equal current sources using thermometer coding. High bits are switched to the output, whereas low bits are switched to ground. As discussed in Section 16.3, the use of a thermometer code for the MSB currents greatly minimizes glitches. For the four LSBs, one additional current source from the MSB segment is diverted where it is divided into binary-weighted currents, which are also switched to either ground or the output. Although this four-LSB segment is not guaranteed to be monotonic, its accuracy requirements are very relaxed, since it is used only for the LSBs.
image_name:Fig. 16.22 A 6-bit segmented D/A converter
description:The circuit is a 6-bit segmented D/A converter. It uses a combination of thermometer code for the 2 MSBs and a binary-weighted current divider for the 4 LSBs. The OpAmp1 provides a reference voltage Vref, and OpAmp2 is used to buffer the output voltage Vout. The resistors form a ladder network to divide the current appropriately for the digital-to-analog conversion.

Fig. 16.22 A 6-bit segmented D/A converter.

## 16.5 KEY POINTS

- Decoder-based D/A converters operate by creating a set of analog reference levels and selecting one by turning on appropriate switches selected by an input digital code. [p. 623]
- Binary-scaled D/A converters combine binary-weighted circuit quantities (currents, resistors, capacitors, etc.) under digital control to realize an analog quantity. Such techniques are generally hardware-efficient, but can be subject to significant nonlinearities. [p. 628]
- R-2R ladder D/A converters produce binary-weighted currents without the need for a complete array of binaryweighted resistors. Instead, only 2:1 component ratios are needed, a significant savings for high-resolution converters. [p. 631]
- Charge-redistribution switched-capacitor D/A converters sample a fixed reference voltage onto a binaryweighted capacitor array whose effective capacitance is determined by the input digital code. The sampled charge is then applied to a switched-capacitor gain stage to produce the analog output voltage. [p. 632]
- Thermometer-code converters employ an array of $2 \mathrm{~N}-1$ unitary equally-sized signal quantities. A digital thermometer code selects the appropriate number of these unitary signal quantities, summing them to produce the analog output with guaranteed monotonicity and better static linearity than binary-weighted converters. [p. 634]
- Selecting and summing current signals can provide high-speed D/A conversion. Output-impedance enhancement techniques may be needed to ensure the currents remain constat with respect to variations in output voltage. Calibration may also be used to ensure matching. [p. 640]
- A hybrid converter combines different D/A architectures to realize different portions of the converter design. [p. 640]
