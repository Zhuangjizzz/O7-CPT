# 19 Phase-Locked Loops
Practically all digital and radio frequency circuits and most analog circuits require a precision oscillator. Unfortunately, integrated circuit oscillators are not, on their own, suitable for use as frequency- or time-references in highperformance circuits. A major problem is that their frequency of oscillation is not known precisely. Furthermore, the jitter of integrated circuit oscillators (which can be thought of as random fluctuations in frequency) is too high for many applications. Therefore, integrated circuit oscillators are most often inserted into a phase locked loop where their operating frequency and phase is continuously compared against a precise external time-reference and automatically tuned to maintain a constant frequency and phase. The process is analogous to generating a precise on-chip voltage or current based on an externally-supplied reference. In summary, a phase-locked loop is a circuit that uses an external timing reference to measure and generate on-chip frequencies and times accurately.

It is natural to wonder why, if a precise time-reference is available, a phase locked loop is required at all. Why not simply use the time-reference (usually itself a clock) directly? One reason is that the required frequency may be different than that of the reference. This is frequently the case since timing references are commonly derived from precision resonators trimmed to a fixed frequency. For low cost, these resonators are often in the range of $1-200$ MHz . The generation of a different and/or variable-frequency precision clock from a fixed-frequency reference is referred to as clock synthesis or frequency synthesis and is a major application of phase-locked loops.

In some cases, the timing reference is supplied by another integrated circuit with which the circuit under design must communicate. Frequency variations can be caused by changes in temperature, supply voltage or aging of components, or can be introduced intentionally to reduce radiated emissions. Phase-locked loops are required to ensure the two circuits track each other very accurately, both in frequency and phase, so that they may communicate with each other reliably. Finally, phase-locked loops are sometimes used to frequency-tune circuits such as filters.

## 19.1 BASIC PHASE-LOCKED LOOP ARCHITECTURE

The basic architecture of a phase-locked loop (PLL) is shown in Fig. 19.1. It usually consists of a phase detector, a low-pass filter called the loop filter, a voltage controlled oscillator (VCO), and a clock divider circuit configured in a loop. The phase detector is a circuit that normally has an output voltage or current with an average value proportional to the phase difference between the input (reference) signal and the output of the VCO. The loop filter is used to extract the average value from the output of the phase detector. This average value is then used to drive the VCO, whose output frequency changes in response to changes in $\mathrm{V}_{\text {cntt }}$. Since the reference input is usually at a lower frequency than the VCO output clock, a clock divider circuit is used to reduce the output clock frequency prior to comparison by the phase detector. The negative feedback of the loop results in the input signal being synchronized with the output of the divider. This basic architecture is called an integer-NPLL since, in a stable steady-state, the divider output and input reference will have the same frequency implying that the VCO output frequency must be exactly an integer multiple N of the input frequency.
image_name:Fig. 19.1 The basic architecture of a phase-locked loop.
description:The block diagram represents the basic architecture of a phase-locked loop (PLL), a control system that generates an output signal whose phase is related to the phase of an input signal. The main components and their functions are as follows:

1. **Phase Detector**: This component receives two input signals: the reference input signal \( V_{in} \) and the feedback signal \( V_{div} \) from the divider. It compares the phase of these two signals and produces an output that is proportional to their phase difference, either as a current \( I_{pd} \) or voltage \( V_{pd} \).

2. **Loop Filter**: The output from the phase detector is fed into the loop filter. This filter processes the phase difference signal to remove high-frequency noise and generates a control voltage \( V_{cntl} \) that is used to adjust the VCO.

3. **Voltage-Controlled Oscillator (VCO)**: The VCO takes the control voltage \( V_{cntl} \) from the loop filter and produces an oscillating output signal \( V_{osc} \). The frequency of this output signal is controlled by the input voltage \( V_{cntl} \), allowing the system to lock the output frequency to the input frequency.

4. **Divider (\( \div N \))**: The VCO output \( V_{osc} \) is fed into a frequency divider, which reduces the frequency by a factor of \( N \). The divided signal \( V_{div} \) is then fed back into the phase detector for comparison with the reference input.

**Flow of Information**:
- The reference input signal \( V_{in} \) and the feedback signal \( V_{div} \) are compared in the phase detector.
- The phase detector produces an output signal proportional to the phase difference, which is filtered by the loop filter.
- The loop filter's output \( V_{cntl} \) controls the VCO, adjusting its output frequency.
- The VCO output \( V_{osc} \) is divided by the divider and fed back to the phase detector, completing the feedback loop.

**Overall System Function**:
The PLL synchronizes the output frequency of the VCO with the frequency of the input reference signal. The negative feedback loop ensures that the phase difference between the input and the divided VCO output is minimized, locking the frequencies together. This architecture is known as an integer-N PLL because the VCO output frequency is an integer multiple \( N \) of the input frequency, allowing precise frequency synthesis and stabilization.

Fig. 19.1 The basic architecture of a phase-locked loop.

A PLL is a negative feedback system, similar to a negative feedback amplifier. In a negative feedback amplifier, two voltages or currents are subtracted and the loop's large gain ensures that their difference is made small. In a phase-locked loop, the objective is to make the difference between the phase of the VCO output and a reference input clock very small. Hence, at the PLL input these two quantities are subtracted by the phase detector and the result is applied to a large gain through the loop filter and VCO to ensure that in a stable steady-state the difference is small.

### 19.1.1 Voltage-Controlled Oscillator

A key component of PLLs is the VCO, a circuit with an oscillatory output (i.e., sinusoid or other clock signal) whose frequency depends upon an input control voltage, $\mathrm{V}_{\text {cntt }}$. Hence, assuming the VCO output is a sinusoidal voltage slowly varying with time, it can be represented by the equation

$$
\begin{equation*}
\mathrm{V}_{\text {osc }}(\mathrm{t})=\mathrm{E} \sin \left[\omega_{0} \mathrm{t}+\phi(\mathrm{t})\right] \tag{19.1}
\end{equation*}
$$

where $\omega_{0}$ is the oscillator's nominal or free-running frequency, and the oscillator's instantaneous phase is $\phi(\mathrm{t})$. The oscillator's instantaneous frequency is the rate of change of $\left[\omega_{0} t+\phi(t)\right]$ in units of rad $/ \mathrm{sec}$.

$$
\begin{equation*}
\omega_{\text {inst }}(\mathrm{t})=\frac{\mathrm{d}\left[\omega_{0} \mathrm{t}+\phi(\mathrm{t})\right]}{\mathrm{dt}}=\omega_{0}+\frac{\mathrm{d} \phi(\mathrm{t})}{\mathrm{dt}} \tag{19.2}
\end{equation*}
$$

Hence, if the oscillator phase $\phi(\mathrm{t})$ is constant, the instantaneous frequency is equal to the free-running frequency, $\omega_{\text {inst }}(\mathrm{t})=\omega_{0}$.

Now define the deviation in the VCO's instantaneous frequency from its free running frequency,

$$
\begin{equation*}
\omega(t)=\omega_{\text {inst }}(t)-\omega_{0} \tag{19.3}
\end{equation*}
$$

Of course, $\omega(\mathrm{t})$ is dependent on the VCO control voltage $\mathrm{V}_{\mathrm{cnt1}}(\mathrm{t})$. Clearly from (19.2), $\omega(\mathrm{t})$ is linearly related to the phase.

$$
\begin{equation*}
\omega(\mathrm{t})=\frac{\mathrm{d} \phi(\mathrm{t})}{\mathrm{dt}} \tag{19.4}
\end{equation*}
$$

If we integrate both sides of (19.4), we have

$$
\begin{equation*}
\phi(\mathrm{t})=\phi(0)+\int_{0}^{\mathrm{t}} \omega(\tau) \mathrm{d} \tau \tag{19.5}
\end{equation*}
$$

image_name:Fig. 19.2
description:The block diagram in Fig. 19.2 illustrates the operation of a clock divider with a division ratio of N=4.

1. **Main Components:**
- **Divider Block:** The central component is a block labeled as "÷ 4 Divider." It is responsible for dividing the frequency of the input signal by a factor of four.
- **Input Voltage (V_osc):** This is the input signal to the divider, represented by a waveform labeled as V_osc.
- **Output Voltage (V_div):** This is the output signal from the divider, represented by a waveform labeled as V_div.

2. **Flow of Information or Control:**
- The input signal V_osc enters the divider block. This signal has a period of T_0, as indicated on the waveform.
- The divider processes the input signal and outputs V_div, which has a period of 4T_0. This indicates that the frequency of the output signal is one-fourth of the input frequency, achieving the division by four.

3. **Labels, Annotations, and Key Indicators:**
- The time period of the input signal V_osc is labeled as T_0, and the time interval between two rising edges of the input waveform is shown as Δt.
- The output waveform V_div is shown to have a period of 4T_0, demonstrating the division effect.
- The time axis is marked with t = 0 at the starting point of the waveforms.

4. **Overall System Function:**
- The primary function of this system is to take an oscillating input signal (V_osc) and reduce its frequency by a factor of four, producing an output signal (V_div) with a longer period. This is achieved through the use of the divider block, which effectively counts the input cycles and outputs a signal at a reduced frequency. This type of system is typically used in digital circuits where lower frequency clock signals are needed.
image_name:
description:The graph illustrates the operation of a clock divider with a division ratio of N=4. It is a time-domain waveform showing two signals: the input voltage to the divider, \( V_{osc} \), and the divided output voltage, \( V_{div} \).

1. **Type of Graph and Function:**
- This is a time-domain waveform graph depicting the behavior of a clock signal as it passes through a divider.

2. **Axes Labels and Units:**
- The horizontal axis represents time \( t \), starting from \( t = 0 \).
- The vertical axis shows voltage levels for both \( V_{osc} \) and \( V_{div} \).

3. **Overall Behavior and Trends:**
- The \( V_{osc} \) signal is a periodic waveform with a period denoted as \( T_0 \). It shows a square wave pattern with equal high and low states.
- The \( V_{div} \) signal is also a square wave but with a period of \( 4T_0 \), indicating it is four times the period of \( V_{osc} \).
- The waveform starts at \( t=0 \) and shows that the output \( V_{div} \) changes state only after every four cycles of the input \( V_{osc} \).

4. **Key Features and Technical Details:**
- The input \( V_{osc} \) signal completes four cycles within the duration \( 4T_0 \).
- The output \( V_{div} \) signal completes one cycle in the same duration \( 4T_0 \).
- The time delay \( \Delta t \) is noted at the beginning of the waveform, showing the initial phase difference between \( V_{osc} \) and \( V_{div} \).

5. **Annotations and Specific Data Points:**
- The diagram includes a block labeled "/4 Divider" indicating the division operation.
- Arrows and labels such as \( T_0 \) and \( 4T_0 \) are used to denote the periods of the signals.
- The graph clearly shows how the clock divider reduces the frequency by a factor of four, as indicated by the longer period of \( V_{div} \) compared to \( V_{osc} \).

Fig. 19.2 The operation of a clock divider with a division ratio of $\mathrm{N}=4$.

Key Point: The instantaneous frequency deviation of a VCO from its free-running frequency is the derivative of its instantaneous phase. Hence, its instantaneous phase is the integral of the instantaneous frequency deviation.
and we see that the instantaneous phase is the integral of the instantaneous frequency deviation. Taking the Laplace transform of both sides of (19.4), we have

$$
\begin{equation*}
\phi(s)=\frac{\omega(s)}{s} \tag{19.6}
\end{equation*}
$$

where $\phi(\mathrm{s})$ and $\omega(\mathrm{s})$ are the Laplace transforms of $\phi(\mathrm{t})$ and $\omega(\mathrm{t})$ respectively. Equation (19.6) will be used to model the relationship between the VCO's input control voltage and the phase of its output signal. To arrive at a linear model, assume that $\omega(\mathrm{t})$ is proportional to the control voltage with a constant of proportionality $\mathrm{K}_{\mathrm{osc}}$ that has units $\mathrm{rad} /(\mathrm{sec} \cdot \mathrm{V})$.

$$
\begin{equation*}
\omega(\mathrm{t})=\mathrm{K}_{\mathrm{osc}} \mathrm{~V}_{\mathrm{cnt1}}(\mathrm{t}) \tag{19.7}
\end{equation*}
$$

Even when the relationship is nonlinear, (19.7) can still be used as a small-signal model where $\mathrm{K}_{\text {osc }}$ relates small changes in $\mathrm{V}_{\mathrm{cnt}}(\mathrm{t})$ to the resulting changes in $\omega(\mathrm{t})$.

### 19.1.2 Divider

An ideal clock divider with a division ratio N will produce a cyclic output with each period corresponding to exactly N periods of the input. This is illustrated in Fig. 19.2 for $\mathrm{N}=4$. The result is that the divider's instantaneous output frequency is exactly $(1 / \mathrm{N})$ times that of is input, which in PLLs is the VCO output. Furthermore, the divider's output phase, $\phi_{\text {div }}(\mathrm{t})$, is also exactly $(1 / \mathrm{N})$ times that of is input, $\phi(\mathrm{t})$. To see this, note that the phase of the VCO output $\mathrm{V}_{\text {osc }}$ is the time delay $\Delta \mathrm{t}$ between that clock's rising edge and some reference time, $t=0$, normalized with respect to a period, $T_{0}$.

$$
\begin{equation*}
\phi=2 \pi \frac{\Delta t}{\mathrm{~T}_{0}} \tag{19.8}
\end{equation*}
$$

Assuming the divider output is synchronized with that of the VCO output, its phase is determined by the same time delay, $\Delta \mathrm{t}$, but normalized with respect to the longer period, $\mathrm{NT}_{0}$.

$$
\begin{equation*}
\phi_{\text {div }}=2 \pi \frac{\Delta \mathrm{t}}{\mathrm{NT}_{0}}=\frac{\phi}{\mathrm{N}} \tag{19.9}
\end{equation*}
$$

Equation (19.9) provides a linear model for the divider, which in terms of Laplace transforms is simply

$$
\begin{equation*}
\phi_{\text {div }}(\mathrm{s})=\frac{\phi(\mathrm{s})}{\mathrm{N}} \tag{19.10}
\end{equation*}
$$

### 19.1.3 Phase Detector

The role of the phase detector is to produce a signal whose average value is proportional to the difference between the phase of the reference input, $\theta_{\text {in }}$, and the feedback clock signal, $\theta_{\text {div }}$. This is analogous to the subtraction performed at the input of a feedback amplifier. There are many possibilities for the phase detector: a simple exclusive-OR gate, a sample and hold, an analog multiplier, or a combination of digital circuits such as D flip-flops. All accept two clock signals as inputs and produce an output whose average value provides the requisite phase information.

#### EXAMPLE 19.1

What is the gain of an analog multiplier phase detector?

#### Solution

In this example, the input signal, $\mathrm{V}_{\mathrm{in}}$, is assumed to be a sinusoid with a known amplitude. The phase detector is realized as an analog multiplier having a relationship given by

$$
\begin{equation*}
V_{p d}=K_{M} V_{i n} V_{\text {div }} \tag{19.11}
\end{equation*}
$$

where $\mathrm{V}_{\text {div }}$ is the divider output, $\mathrm{V}_{\mathrm{pd}}$ is the phase-detector output, and $\mathrm{K}_{\mathrm{M}}$ is a multiplication constant. Let the input signal be described by a sinusoid having

$$
\begin{equation*}
V_{\text {in }}=E_{\text {in }} \sin (\omega t) \tag{19.12}
\end{equation*}
$$

and the output of the divider is given by a sinusoid where

$$
\begin{equation*}
\mathrm{V}_{\text {div }}=\mathrm{E}_{\text {div }} \sin \left(\omega \mathrm{t}-\phi_{\mathrm{d}}+90^{\circ}\right)=\mathrm{E}_{\text {div }} \cos \left(\omega \mathrm{t}-\phi_{\mathrm{d}}\right) \tag{19.13}
\end{equation*}
$$

The argument $\phi_{\mathrm{d}}$ represents the phase difference between the input signal and the output of the oscillator. The reason for the $90^{\circ}$ offset is so that when $\phi_{\mathrm{d}}=0$ the average output of the phase detector (an analog multiplier in this example) is zero. The combination of an analog multiplier followed by a low-pass filter performs what is commonly known as the correlation function on analog signals. When the input signal and the VCO output have a $90^{\circ}$ phase difference (i.e., $\phi_{d}=0$ ), they are uncorrelated and the output of the low-pass filter will be zero. From this $90^{\circ}$ phase offset, if the phase difference changes so that the two waveforms are more in phase (i.e., $\phi_{d}>0$ ), then the correlation and, therefore, the output of the low-pass filter will be positive. For example, from (19.13), if $\phi_{d}=90^{\circ}$, then the output of the oscillator and the input signal would be exactly in phase, and the average output of the phase detector is found to be the amplitudes of the two sinusoids multiplied together and divided by two, resulting in

$$
\begin{equation*}
\mathrm{V}_{\mathrm{cntl}}=\mathrm{K}_{\mathrm{lp}} \mathrm{~K}_{\mathrm{M}} \frac{\mathrm{E}_{\mathrm{in}} \mathrm{E}_{\text {div }}}{2} \tag{19.14}
\end{equation*}
$$

This situation is approximately shown in Fig. 19.3 where $\phi_{d}$ is taken slightly smaller than $90^{\circ}$ to distinguish the two waveforms. Also shown is the output of the multiplier, $\mathrm{V}_{\mathrm{pd}}$, for the case of $\mathrm{E}_{\mathrm{in}}=\mathrm{E}_{\mathrm{div}}=1 \mathrm{~V}$, and
image_name:Fig. 19.3
description:The graph in Fig. 19.3 is a time-domain waveform plot depicting the behavior of three signals: the input signal (V_in), the oscillator output (V_osc), and the phase detector output (V_pd).

1. **Type of Graph and Function:**
- This is a time-domain waveform plot showing sinusoidal waveforms.

2. **Axes Labels and Units:**
- The x-axis represents time, presumably in arbitrary units, as no specific unit is indicated.
- The y-axis represents voltage in volts, ranging from -1 to 1.

3. **Overall Behavior and Trends:**
- The graph shows two sinusoidal waveforms (V_in and V_osc) that are slightly out of phase, with V_in leading V_osc.
- The third waveform, V_pd, has a frequency double that of V_in and V_osc, indicating that it is the result of a multiplication process, typical in phase detectors.
- The amplitudes of V_in and V_osc are similar, while V_pd has a smaller amplitude.

4. **Key Features and Technical Details:**
- V_in and V_osc are nearly in phase, but a small phase difference is present, as indicated in the context.
- V_pd, being the output of the phase detector, reflects the phase difference and is at twice the frequency of the input signals.
- The peaks and troughs of V_pd occur at the zero crossings of V_in and V_osc.

5. **Annotations and Specific Data Points:**
- The plot includes annotations for each waveform, indicating their respective labels: V_in, V_osc, and V_pd.
- No specific numerical values are provided for other key data points, but the graph visually conveys the phase relationship and frequency characteristics effectively.

Fig. 19.3 The output of the phase detector in Example 19.1 when the input signal and the oscillator are nearly in phase.
image_name:Fig. 19.3
description:The graph depicted in Fig. 19.3 is a time-domain waveform plot illustrating the phase relationship between an input signal \( V_{in} \) and an oscillator output \( V_{osc} \). The x-axis represents time, while the y-axis represents voltage. The graph shows three sinusoidal waveforms:

1. **\( V_{in} = \sin(\omega t) \):** This waveform is a reference sinusoidal input signal with a phase angle of zero degrees.

2. **\( V_{osc} = \sin(\omega t + 90^\circ) \):** This waveform represents the oscillator output, which is phase-shifted by 90 degrees relative to \( V_{in} \).

3. **\( V_{osc} = \sin(\omega t + 90^\circ \pm \frac{\pi}{8}) \):** These waveforms show slight phase shifts from the 90-degree phase-shifted oscillator output, indicating additional phase adjustments by \( \pm \frac{\pi}{8} \).

The graph effectively illustrates the phase relationships and shifts between these waveforms. The sinusoidal waves are periodic and maintain a consistent frequency across the time axis. The waveforms are annotated with their respective equations, clarifying the phase differences. The visual representation highlights the phase alignment and potential interference or correlation between the input and oscillator signals.

Fig. 19.4 The relative phase angles of the input signal and the output of the oscillator.
$\mathrm{K}_{\mathrm{M}}=1 \mathrm{~V}^{-1}$. Here, it is seen that the output is at twice the frequency of the input signal and that it has an offset voltage of approximately $1 / 2 \mathrm{~V}$. This corresponds closely to the maximum possible output of the low-pass filter. On the other hand, if the phase changes so as to make the two waveforms more out of phase, then the correlation between them and the output of the low-pass filter will be negative. Shown in Fig. 19.4 are some examples of the different waveforms. It is readily seen that $\phi_{d}>0$ corresponds to the waveforms that are more in phase.

These statements can be quantified analytically. The output of the phase detector is given by

$$
\begin{equation*}
V_{p d}=K_{M} V_{\text {in }} V_{\text {div }}=K_{M} E_{\text {in }} E_{\text {div }} \sin (\omega t) \cos \left(\omega t-\phi_{d}\right) \tag{19.15}
\end{equation*}
$$

Using the trigonometric identity

$$
\begin{equation*}
\sin (A) \cos (B)=\frac{1}{2}[\sin (A+B)+\sin (A-B)] \tag{19.16}
\end{equation*}
$$

we have

$$
\begin{equation*}
\mathrm{V}_{\mathrm{pd}}=\mathrm{K}_{\mathrm{M}} \frac{\mathrm{E}_{\mathrm{in}} \mathrm{E}_{\mathrm{div}}}{2}\left[\sin \left(\phi_{\mathrm{d}}\right)+\sin \left(2 \omega \mathrm{t}-\phi_{\mathrm{d}}\right)\right] \tag{19.17}
\end{equation*}
$$

The low-pass filter removes the second term at twice the frequency of the input signal. ${ }^{1}$ The signal $\mathrm{V}_{\text {ontt }}$ is therefore given by

$$
\begin{equation*}
\mathrm{V}_{\mathrm{cntl}}=\mathrm{K}_{\mathrm{lp}} \mathrm{~K}_{\mathrm{M}} \frac{\mathrm{E}_{\mathrm{in}} \mathrm{E}_{\mathrm{div}}}{2} \sin \left(\phi_{\mathrm{d}}\right) \tag{19.18}
\end{equation*}
$$

Note that $\mathrm{V}_{\mathrm{cnt1}}$ is either a dc value or a slowly varying signal, assuming that the frequency of the input signal is constant or slowly varying. For small $\phi_{\mathrm{d}}$, we can approximate (19.18) as

$$
\begin{equation*}
\mathrm{V}_{\mathrm{cnt}} \cong \mathrm{~K}_{\mathrm{lp}} \mathrm{~K}_{\mathrm{M}} \frac{\mathrm{E}_{\mathrm{in}} \mathrm{E}_{\mathrm{div}}}{2} \phi_{\mathrm{d}}=\mathrm{K}_{\mathrm{lp}} \mathrm{~K}_{\mathrm{pd}} \phi_{\mathrm{d}} \tag{19.19}
\end{equation*}
$$

Thus, the output of the low-pass filter is approximately proportional to the phase difference between the output of the oscillator and the input signal, assuming the $90^{\circ}$ offset bias is ignored. This approximation is used in analyzing the PLL to obtain a linear model. The constant of proportionality is called $\mathrm{K}_{\mathrm{pd}}$ and is given by

$$
\begin{equation*}
\mathrm{K}_{\mathrm{pd}}=\mathrm{K}_{\mathrm{M}} \frac{\mathrm{E}_{\mathrm{in}} \mathrm{E}_{\mathrm{div}}}{2} \tag{19.20}
\end{equation*}
$$

Note that with this analog-multiplier phase detector, $\mathrm{K}_{\mathrm{pd}}$ is a function of the input amplitude and divider output amplitude. As we shall soon see, $\mathrm{K}_{\mathrm{pd}}$ affects loop dynamics, and thus we see the need for having known values for $\mathrm{E}_{\text {in }}$ and $\mathrm{E}_{\text {div }}$.

The output of the phase detector may be a voltage as in Example 19.1, but in CMOS circuits is commonly a current, either single-ended or differential. When the output is a current whose average value ${ }^{2}$ is $I_{p d}$, the gain of the phase detector is a constant $\mathrm{K}_{\mathrm{pd}}$ with units $\mathrm{A} / \mathrm{rad}$.

$$
\begin{equation*}
\mathrm{I}_{\mathrm{pd}}=\mathrm{K}_{\mathrm{pd}} \phi_{\mathrm{d}}=\mathrm{K}_{\mathrm{pd}}\left(\phi_{\mathrm{in}}-\phi_{\mathrm{div}}\right) \tag{19.21}
\end{equation*}
$$

#### EXAMPLE 19.2

A charge-pump phase detector is shown in general form in Fig. 19.5. The phase detector logic is designed so that logic-high pulses are generated on $P_{u}$ when the reference clock leads the feedback clock, $\phi_{\mathrm{d}}>0$, and pulses are generated on $P_{d}$ when the reference clock is lagging, $\phi_{d}<0$. A typical arrangement of logic is shown in Fig. 19.6. Find the gain of such a phase detector $K_{p d}$ in units $A / r a d$.
image_name:Fig. 19.5 General charge-pump phase detector
description:The phase detector logic generates two outputs, Pu and Pd, based on the inputs Vin and Vdiv. The switches S1 and S2 control the flow of the current Ich depending on the phase difference. The current Ipd flows through the loop filter based on the states of S1 and S2.

Charge-pump phase detector
Fig. 19.5 General charge-pump phase detector.

#### Solution

This phase comparator either sources or sinks current in the low-pass loop filter, depending on the output of the sequential phase-detector logic. When $S_{1}$ is closed, $I_{c h}$ flows into the low-pass filter; when $S_{2}$ is closed, $I_{c h}$ flows out of the low-pass filter. The sequential phase-detector logic generates two outputs, $P_{u}$ and $P_{d}$, depending on its inputs, $\mathrm{V}_{\text {in }}$ and $\mathrm{V}_{\text {div }}$. These are normally digital signals from the PLL input and the VCO, respectively. ${ }^{3}$ Although there are many possibilities for the sequential phase detector, the one we will consider is controlled by the leading edges of $V_{\text {in }}$ and $V_{\text {osc }}$. If $V_{\text {in }}$ goes high before $V_{o s c}$, then $P_{u}$ will be high during the time that the signals are different. This will inject some charge into the loop filter to speed up the VCO. Similarly, if $\mathrm{V}_{\text {osc }}$ goes low before $V_{i n}$, then $P_{d}$ will be high during the time the inputs are different, $S_{2}$ will be closed, and charge will be subtracted from the loop filter, which decreases the VCO frequency. When the leading edges are coincident, the two inputs are phase aligned. In this case, ideally both $P_{u}$ and $P_{d}$ are always low, both $S_{1}$ and $S_{2}$ are always open so no charge is injected to or removed from the loop filter, and the loop has reached steady-state. In practical sequential phase detectors, both $P_{u}$ and $P_{d}$ may go high for a few gate delays when the input waveforms are coincident, but this time is usually short enough that it has very little effect on the dc output of the loop filter, and its effect is largely eliminated by capacitors in the loop filter. The falling edges of both $\mathrm{V}_{\text {in }}$ and $\mathrm{V}_{\text {osc }}$ have no effect on $P_{\mathrm{u}}$ and $P_{\mathrm{d}}$, which are both zero at this time. This makes the PLL insensitive to the duty cycles of the waveform. Typical waveforms are shown in Fig. 19.6.

To solve for the phase detector gain, note that the output current $I_{p d}$ averaged over any single period of the reference clock $V_{i n}$ is given by the charge pump current $I_{c h}$ scaled by the fraction of a period over which the phase detector outputs $P_{u}$ and $P_{d}$ are active.

$$
\begin{equation*}
\overline{\mathrm{I}_{\mathrm{pd}}}=\mathrm{I}_{\mathrm{ch}} \frac{\phi_{\mathrm{d}}}{2 \pi} \tag{19.22}
\end{equation*}
$$

[^1]image_name:Fig. 19.6 Phase-detector logic and corresponding waveforms
description:The graph in Fig. 19.6 illustrates the phase-detector logic and corresponding waveforms for a phase-locked loop (PLL) system. It combines both a schematic diagram of the logic circuit and the resulting waveforms over time.

Type of Graph and Function:
- **Type:** Schematic and time-domain waveform.
- **Function:** Shows the operation of a phase detector within a PLL, including logic gate interactions and resulting signal behavior.

Axes Labels and Units:
- **Horizontal Axis:** Represents time (no specific units provided, but typically in seconds or milliseconds for such diagrams).
- **Vertical Axes:** Different signals are represented:
- **V_in:** Input reference clock signal.
- **V_div:** Divided clock signal.
- **P_u:** Phase detector output for the up signal.
- **P_d:** Phase detector output for the down signal.
- **I_pd:** Output current from the phase detector.

Overall Behavior and Trends:
- **V_in and V_div:** Both signals are square waves. V_in is the reference clock, while V_div is the feedback from the PLL, typically at the same frequency but with a possible phase difference.
- **P_u and P_d:** These are pulse signals. P_u is active (high) when V_in leads V_div, and P_d is active when V_div leads V_in.
- **I_pd:** The output current waveform follows the activation of P_u and P_d, with positive pulses corresponding to P_u and negative pulses to P_d.

Key Features and Technical Details:
- **Phase Difference (φ_d):** The diagram shows the phase difference between V_in and V_div, indicated by the width of the P_u pulse.
- **Current Pulse Width (I_ch):** The current pulse width is equal to the active duration of P_u or P_d, scaled by the charge pump current I_ch.
- **Reset Logic:** The schematic includes flip-flops (FF1 to FF4) and logic gates that determine the reset conditions and pulse generation for P_u and P_d.

Annotations and Specific Data Points:
- **Annotations:** The diagram annotates the phase difference (φ_d) and the corresponding period (2π) for the signals.
- **Pulse Widths:** The width of the P_u and P_d pulses are critical in determining the average output current I_pd, as shown in the equation provided in the context.

This diagram effectively demonstrates the logic and timing interactions within a PLL phase detector, highlighting how phase differences translate into control signals for the loop.

Fig. 19.6 Phase-detector logic and corresponding waveforms.

Fig. 19.7 Loop filter for charge-pump phase detectors.
image_name:Fig. 19.7 Loop filter for charge-pump phase detectors
description:This circuit is a loop filter for a charge-pump phase detector in a PLL. It consists of a current source I_pd, a resistor R, and two capacitors C1 and C2. The filter averages the phase detector output and influences the dynamics of the loop by controlling the VCO control signal V_cntl.

Combining (19.21) and (19.22) yields the phase detector gain,

$$
\begin{equation*}
\mathrm{K}_{\mathrm{pd}}=\frac{\mathrm{I}_{\mathrm{ch}}}{2 \pi} \tag{19.23}
\end{equation*}
$$

### 19.1.4 Loop Filer

The loop filter plays several key roles in a PLL. It averages out the quickly-varying components of the phase detector output. We shall see that it also influences the dynamics of the loop by determining how the VCO control signal, $\mathrm{V}_{\mathrm{cntt}}$, responds to variations in the phase difference represented by $\mathrm{I}_{\mathrm{pd}}$.

In most PLLs, the loop filter is first or second order. For example, a common first-order low-pass loop filter has a transfer function given by

$$
\begin{equation*}
\mathrm{K}_{1 \mathrm{p}} \mathrm{H}_{\mathrm{lp}}(\mathrm{~s})=\mathrm{K}_{\mathrm{lp}} \frac{1+\mathrm{s} / \omega_{z}}{\mathrm{~s}}=\mathrm{K}_{\mathrm{lp}}\left(\frac{1}{\mathrm{~s}}+\frac{1}{\omega_{\mathrm{z}}}\right) \tag{19.24}
\end{equation*}
$$

A loop filter of the form (19.24) may be thought of as comprising the sum of a proportional and an integral path. Many loop filters will include additional higher-order poles and zeros, but the most important PLL design parameters are captured by (19.24).

The loop filter gain constant $\mathrm{K}_{1 \mathrm{p}}$ has units of $\Omega \cdot \mathrm{rad} / \mathrm{s}=\mathrm{F}^{-1}$ when the phase detector output is a current and $\mathrm{rad} / \mathrm{s}$ when the phase detector output is a voltage.

#### EXAMPLE 19.3

Find the loop filter transfer function that relates the current $I_{p d}$ and control voltage $V_{c n t 1}$ in Fig. 19.7.

#### Solution

It is assumed that there is no current flowing out of the loop filter into the control terminal of the VCO, as shown in Fig. 19.7. Hence, all current must flow through the parallel impedances $\left(R+1 /\left(\mathrm{sC}_{1}\right)\right)$ and $1 /\left(\mathrm{sC}_{2}\right)$. The loop filter transfer function is

$$
\begin{equation*}
\mathrm{K}_{\mathrm{lp}} \mathrm{H}_{\mathrm{lp}}(\mathrm{~s})=\frac{\mathrm{V}_{\mathrm{cnt1}}(\mathrm{~s})}{\mathrm{I}_{\mathrm{pd}}(\mathrm{~s})}=\frac{1}{\mathrm{~s}\left(\mathrm{C}_{1}+\mathrm{C}_{2}\right)} \cdot \frac{1+\mathrm{sRC}_{1}}{1+\mathrm{sR}\left(\frac{\mathrm{C}_{1} \mathrm{C}_{2}}{\mathrm{C}_{1}+\mathrm{C}_{2}}\right)} \tag{19.25}
\end{equation*}
$$

In practice, the capacitor $C_{2}$ is there only to suppress voltage spikes that would otherwise arise across $R$ from transient currents, hence its value is generally much smaller than $C_{1}$. Assuming that $\left(C_{1}+C_{2}\right) \cong C_{1}$ and neglecting the high frequency pole at $\left(C_{1}+C_{2}\right) /\left(\mathrm{RC}_{1} \mathrm{C}_{2}\right)$,

$$
\begin{equation*}
\mathrm{K}_{\mathrm{lp}} \mathrm{H}_{\mathrm{lp}}(\mathrm{~s})=\frac{\mathrm{V}_{\mathrm{cnt1}}(\mathrm{~s})}{\mathrm{I}_{\mathrm{pd}}(\mathrm{~s})} \cong \frac{1}{\mathrm{C}_{1}}\left(\frac{1+\mathrm{sRC}_{1}}{\mathrm{~s}}\right) \tag{19.26}
\end{equation*}
$$

Casting (19.26) into the general model of (19.24), we have for a charge-pump loop filter,

$$
\begin{gather*}
\mathrm{K}_{1 \mathrm{p}}=1 / \mathrm{C}_{1}  \tag{19.27}\\
\omega_{\mathrm{z}}=1 /\left(\mathrm{RC}_{1}\right) \tag{19.28}
\end{gather*}
$$

The loop filter in Fig. 19.7 is often combined with the charge pump phase comparator in Fig. 19.5. When $\mathrm{S}_{1}$ is closed, $\mathrm{I}_{\mathrm{ch}}$ flows into the low-pass filter, increasing the control voltage into the VCO; when $\mathrm{S}_{2}$ is closed, $\mathrm{I}_{\mathrm{ch}}$ flows out of the low-pass filter, decreasing the control voltage of the VCO. When both switches are open, the top plates of $C_{1}$ and $C_{2}$ are open circuited and the output voltage remains constant in the steady state. The resistor, $R$, has been included to realize a zero in the low-pass filter's transfer function. It provides an output component proportional to the input current, while the capacitor integrates the input current. Since the two are in series, the sum of the proportional and integral terms are seen at $\mathrm{V}_{\mathrm{cnt1}}$.

### 19.1.5 The PLL in Lock

To understand phase-locked loops, a simple example will be considered. Assume a division ratio $\mathrm{N}=1$ so that $\phi_{\text {div }}=\phi$. Furthermore, assume an input signal frequency initially equal to the free-running frequency of the VCO, the system is initially in lock with $\phi_{\mathrm{d}}=0$, and the output of the low-pass filter $\mathrm{V}_{\mathrm{cnt1}}$ is also equal to zero. Next, assume the input frequency slowly increases. This will cause it to lead the VCO output, which corresponds to a phase difference $\phi_{\mathrm{d}}=\phi_{\text {in }}-\phi>0$. After a short time (roughly the time constant of the low-pass filter) the output of the low-pass filter will go positive. Since the two waveforms are now assumed to be at slightly different frequencies, the phase difference, and therefore the output of the low-pass filter, will slowly continue to increase. However, the frequency of the VCO is proportional to its control voltage, so the increase in the low-pass filter's output will cause the VCO's frequency to increase until it is the same as that of the input signal again, which will keep the two signals in synchrony (i.e., locked). Of course, the opposite would occur if the input signal's frequency decreased. Specifically, the average output of the phase detector would become negative, which, after being averaged by the low-pass filter, would drive the oscillator to a lower frequency until it is again identical to the frequency of the input signal and the two waveforms are again synchronized. It is readily seen here that the phase-locked loop stays in lock because of the negative feedback of the loop in which the phase of the oscillator's output is subtracted from the phase of the input signal.

The argument is easily extended to the case $\mathrm{N} \neq 1$. The divider ensures that the oscillator output is at a phase and frequency N -times greater than the clock that is fed back to the phase detector. Negative feedback and high dc gain around the loop force the two phases at the inputs of the phase detector to be equal. Hence, it is seen that a PLL in lock produces an output clock at a frequency precisely N -times greater than the reference input that tracks phase changes in the reference input.
image_name:Fig. 19.8
description:The block diagram represents a linearized small-signal model of a Phase-Locked Loop (PLL) when in lock. The main components and the flow of information through the system are as follows:

1. **Main Components:**
- **Phase Detector (PD):** The input phase \( \phi_{in}(s) \) is compared with the divided output phase \( \phi_{div}(s) \) using a summing junction. The output of the phase detector is \( \phi_d(s) \), which is the phase difference.
- **Gain Block \( K_{pd} \):** This block represents the gain of the phase detector, outputting either a current \( I_{pd} \) or voltage \( V_{pd} \).
- **Loop Filter \( K_{lp}H_{lp}(s) \):** This component filters the output of the phase detector to produce a control voltage \( V_{cntl} \).
- **Voltage-Controlled Oscillator (VCO) \( K_{osc}/s \):** Converts the control voltage \( V_{cntl} \) into an output phase \( \phi(s) \).
- **Divider \( 1/N \):** Divides the oscillator output phase \( \phi(s) \) by \( N \) to produce \( \phi_{div}(s) \), which is fed back to the phase detector.

2. **Flow of Information or Control:**
- The input phase \( \phi_{in}(s) \) is compared with the feedback phase \( \phi_{div}(s) \) at the summing junction, generating the phase error signal \( \phi_d(s) \).
- This error signal is amplified by the phase detector gain block \( K_{pd} \), resulting in \( I_{pd} \) or \( V_{pd} \).
- The loop filter \( K_{lp}H_{lp}(s) \) processes this signal to produce the control voltage \( V_{cntl} \).
- The VCO uses \( V_{cntl} \) to adjust its output phase \( \phi(s) \), which is then divided by \( N \) and fed back as \( \phi_{div}(s) \).

3. **Labels, Annotations, and Key Indicators:**
- The diagram includes transfer functions and gain annotations such as \( K_{pd} \), \( K_{lp}H_{lp}(s) \), and \( K_{osc}/s \), which indicate the characteristics of each block.
- The feedback loop is clearly indicated from the output phase \( \phi(s) \) back to the input of the phase detector.

4. **Overall System Function:**
- The PLL system locks the output phase \( \phi(s) \) to be \( N \) times the input phase \( \phi_{in}(s) \). It ensures that any phase difference is minimized through feedback control, maintaining the output frequency at \( N \) times the reference frequency while tracking phase changes. The linearized model allows for analysis of the system's dynamic response to small perturbations in phase and frequency.

Fig. 19.8 A signal-flow graph for the linearized small-signal model of a PLL when in lock.

## 19.2 LINEARIZED SMALL-SIGNAL ANALYSIS

Key Point: Once a PLL is in lock, its dynamic response to input phase and frequency changes can be well approximated by a linear model, as long as these changes are slow and small about their operating or bias point.

The dynamics of a PLL will be of great interest to the designer. Specifically, is the loop stable? How does it settle when perturbed from its locked point? How is noise generated within the loop translated to its output? How can the loop be designed to ensure a certain dynamic behavior? As with feedback amplifiers, linear analysis is a useful tool to answer these questions. However, the phaselocked loop is a highly nonlinear system. Fortunately, once a PLL is in lock, its dynamic response to input phase and frequency changes can be well approximated by a linear model, as long as these changes are slow and small about their operating or bias point.

Using the relationships described in Section 19.1, a linear model for a phase-locked loop can be developed. It should be noted that this is a small-signal model in that it relates changes about an operating point. In other words, the phase variable represents changes in phase from reference signals that were identical to the true signals at the beginning of the analysis. Similarly, any frequency variables, which will be introduced shortly, also represent changes from the original frequencies at the beginning of the analysis. A signal-flow graph for the linearized small-signal model is shown in Fig. 19.8.

It is now possible to analyze the signal flow graph of Fig. 19.8 to determine transfer functions that relate small perturbations in the various signals around the loop. For example, straightforward feedback analysis reveals that the transfer function relating small changes in the input phase $\phi(\mathrm{s})$ to the phase difference $\phi_{\mathrm{d}}(\mathrm{s})$ is given by

$$
\begin{equation*}
\frac{\phi_{\mathrm{d}}(\mathrm{~s})}{\phi_{\mathrm{in}}(\mathrm{~s})}=\frac{1}{1+\mathrm{L}(\mathrm{~s})} \tag{19.29}
\end{equation*}
$$

where $L(s)$ is the loop gain,

$$
\begin{equation*}
\mathrm{L}(\mathrm{~s})=\frac{\mathrm{K}_{\mathrm{pd}} \mathrm{~K}_{\mathrm{lp}} \mathrm{~K}_{\mathrm{osc}} \mathrm{H}_{\mathrm{lp}}(\mathrm{~s})}{\mathrm{Ns}} \tag{19.30}
\end{equation*}
$$

Substituting (19.30) into (19.29),

$$
\begin{equation*}
\frac{\phi_{\mathrm{d}}(\mathrm{~s})}{\phi_{\mathrm{in}}(\mathrm{~s})}=\frac{\mathrm{s}}{\mathrm{~s}+\mathrm{K}_{\mathrm{pd}} \mathrm{~K}_{\mathrm{lp}} \mathrm{~K}_{\mathrm{osc}} \mathrm{H}_{\mathrm{lp}}(\mathrm{~s}) / \mathrm{N}} \tag{19.31}
\end{equation*}
$$

Equation (19.31) is general in that it applies to almost every phase-locked loop. Differences between one PLL and another are determined only by what is used for the low-pass filter (which determines $\mathrm{H}_{\mathrm{lp}}(\mathrm{s})$ ), the phase detector (which determines $\mathrm{K}_{\mathrm{pd}}$ ), or the oscillator (which determines $\mathrm{K}_{\mathrm{osc}}$ ).

### 19.2.1 Second-Order PLL Model

Assume the loop filter has the transfer function given in (19.24). Define the loop constant in units rad/s,

$$
\begin{equation*}
\omega_{\mathrm{plI}}=\sqrt{\frac{\mathrm{K}_{\mathrm{pd}} \mathrm{~K}_{\mathrm{p}} \mathrm{~K}_{\mathrm{osc}}}{\mathrm{~N}}} \tag{19.32}
\end{equation*}
$$

Substituting (19.24) and (19.32) into (19.30) and (19.31) and rearranging results in

$$
\begin{align*}
\mathrm{L}(\mathrm{~s}) & =\frac{\omega_{\mathrm{pll}}^{2}}{\mathrm{~s}^{2}} \cdot\left(1+\frac{\mathrm{s}}{\omega_{\mathrm{z}}}\right)  \tag{19.33}\\
\frac{\phi_{\mathrm{d}}(\mathrm{~s})}{\phi_{\mathrm{in}}(\mathrm{~s})} & =\frac{1}{\omega_{\mathrm{plI}}^{2}} \cdot \frac{\mathrm{~s}^{2}}{\left(1+\frac{\mathrm{s}}{\omega_{\mathrm{z}}}+\frac{\mathrm{s}^{2}}{\omega_{\mathrm{plI}}^{2}}\right)} \tag{19.34}
\end{align*}
$$

The dc gain of (19.34) is zero which signifies that the phase difference between the input and divider output will eventually settle to zero.

We can also relate small changes in the phase of the input and output clock.

$$
\begin{equation*}
H(s)=\frac{\phi(s)}{\phi_{\text {in }}(s)}=\frac{N\left(1+s / \omega_{z}\right)}{1+\frac{s}{\omega_{z}}+\frac{s^{2}}{\omega_{\mathrm{plI}}^{2}}} \tag{19.35}
\end{equation*}
$$

The transfer function $\mathrm{H}(\mathrm{s})$ may be referred to as the phase transfer function or jitter transfer function of the PLL. The de gain of $\mathrm{H}(\mathrm{s})$ is N . This implies that when the input phase changes by a small amount, $\Delta \phi_{\text {in }}$, the output phase changes (after an initial transient) by $N \Delta \phi$. Since the output frequency is N -times larger, this means that the input and output clocks are tracking one another.

In the case of a first-order loop filter both (19.34) and (19.35) are second-order transfer functions and the PLL is a second-order system. Equating the denominator with the general form $1+s /\left(\omega_{r} Q\right)+s^{2} / \omega_{r}^{2}$ reveals that the loop has a resonant frequency $\omega_{\mathrm{r}}=\omega_{\mathrm{pll}}$ and a Q -factor ${ }^{4}$ given by

$$
\begin{equation*}
\mathrm{Q}=\frac{\omega_{\mathrm{z}}}{\omega_{\mathrm{plI}}} \tag{19.36}
\end{equation*}
$$

Observe that if $\omega_{\mathrm{z}}$ is allowed to increase indefinitely (i.e. the zero is eliminated from the loop filter making it a pure integration, $\mathrm{K}_{\mathrm{Ip}} / \mathrm{s}$ ) the poles of (19.35) approach the unit circle; hence, the zero is required to ensure stability of the PLL.

If $\omega_{\mathrm{z}} \gg \omega_{\text {pII }}$ the loop will be underdamped resulting in poor tracking behavior. For example, in Fig. 19.9 a large overshoot is observed in the transient step response for the case $\mathrm{Q}=1.8$. This implies greater delay in obtaining lock and larger transient discrepancies between the input and output phase. Furthermore, considerable peaking is observed in the magnitude response; this is called jitter peaking and is generally undesirable since noise in the PLL will be amplified within a certain frequency band.

image_name:(a)
description:The graph labeled "(a)" is a time-domain step response plot for a closed-loop phase-locked loop (PLL) system, illustrating how the system responds to a step input for different values of the quality factor, Q. The horizontal axis represents time, while the vertical axis represents the step response amplitude. The graph is plotted on a linear scale.

Key features of the graph include:

- Three distinct curves, each corresponding to a different Q value: Q = 1.8, Q = 0.5, and Q = 0.1. These curves show how the system's response changes with varying damping.

- For Q = 1.8, the curve exhibits a significant overshoot, indicating a highly underdamped system. The response initially rises well above the final steady-state value before oscillating and eventually settling.

- For Q = 0.5, the overshoot is present but significantly reduced compared to Q = 1.8. The system still oscillates but stabilizes more quickly, reflecting a critically damped or slightly underdamped response.

- For Q = 0.1, the response is overdamped, with no overshoot. The curve rises smoothly and gradually approaches the steady-state value without oscillations.

This graph visually demonstrates the trade-offs in PLL design between speed of response and overshoot, with Q = 0.5 often being a preferred compromise for achieving a balance between fast response and minimal overshoot.
image_name:(b)
description:The graph labeled as "(b)" is a time-domain step response plot for a second-order phase-locked loop (PLL) model. The x-axis represents time, while the y-axis represents the step response magnitude. Three curves are depicted, each corresponding to a different Q-factor: Q = 1.8, Q = 0.5, and Q = 0.1.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph showing the step response of a PLL system.

2. **Axes Labels and Units:**
- The x-axis is labeled "Time," indicating the progression of time during the step response.
- The y-axis is labeled "Step Response," representing the magnitude of the response over time.
- No specific units or scales are provided, but it is implied that the graph is on a linear scale.

3. **Overall Behavior and Trends:**
- For Q = 1.8, the response shows a large overshoot, indicating an underdamped system with considerable oscillation before settling.
- For Q = 0.5, the overshoot is present but reduced, suggesting a more critically damped response with less oscillation.
- For Q = 0.1, the response is overdamped with no overshoot, indicating a slower rise to the steady state without oscillation.

4. **Key Features and Technical Details:**
- The Q = 1.8 curve peaks significantly higher than the others, showing the maximum overshoot.
- The Q = 0.5 curve has a moderate peak, balancing between speed and stability.
- The Q = 0.1 curve rises gradually with no peak, emphasizing stability over speed.
- These characteristics highlight the trade-off between transient response speed and stability as the Q-factor varies.

5. **Annotations and Specific Data Points:**
- Each curve is annotated with its respective Q-factor value to clearly differentiate the responses.
- The graph visually demonstrates the impact of different Q-factors on the time-domain behavior of the PLL system.

Fig. 19.9 Closed-loop PLL responses for the second-order model, H(s), with equivalent bandwidth but different Q : (a) time-domain step response; (b) frequency-domain jitter transfer function magnitude response

With $\mathrm{Q}=0.5$ although overshoot and jitter peaking are still present, they are greatly reduced. ${ }^{5}$ This is a popular design choice, resulting in a closed-loop response with $\omega_{\mathrm{z}}=\omega_{\text {pII }} / 2$ and coincident real poles at $-\omega_{\text {pII }}$.

$$
\begin{equation*}
H(s)=\frac{N\left(1+s / \omega_{\mathrm{z}}\right)}{\left(1+s / \omega_{\mathrm{pII}}\right)^{2}} \tag{19.37}
\end{equation*}
$$

The 3-dB bandwidth of (19.37) is

$$
\begin{equation*}
\omega_{3 \mathrm{~dB}}=2.5 \omega_{\mathrm{pII}} \tag{19.38}
\end{equation*}
$$

Key Point: The design of a secondorder PLL with $Q=0.5$ provides good transient settling behavior without excessive spreading of the loop filter time constants. $A$ design with $Q=0.1$ offers even better tracking behavior, but generally demands a larger loop-filter time constant for the same loop bandwidth.

Another possibility is to take $\mathrm{Q} \ll 0.5$ providing further improvements in transient response and reduced jitter peaking. For example, with $Q=0.1\left(\omega_{z}=0.1 \omega_{\text {pII }}\right)$ less than 0.1 dB of jitter peaking is observed in the magnitude response. With $\mathrm{Q} \ll 0.5$, the PLL secondorder response can be approximated as $1+\mathrm{s} /\left(\omega_{\mathrm{pII}} \mathrm{Q}\right)+\mathrm{s}^{2} / \omega_{\mathrm{pII}}^{2} \cong$ $\left(1+\mathrm{S} / \omega_{\mathrm{pII}} \mathrm{Q}\right)\left(1+\mathrm{s} Q / \omega_{\mathrm{pII}}\right)$. Since $\omega_{0} \mathrm{Q}=\omega_{\mathrm{plI}} Q=\omega_{z}$, the first term is equal to $\left(1+\mathrm{S} / \omega_{\mathrm{z}}\right)$ which cancels the zero in the numerator of (19.35). With finite $\mathrm{Q} \ll 0.5$ the cancellation is approximate and the closed-loop PLL response may be estimated from a first-order model,

$$
\begin{equation*}
\mathrm{H}(\mathrm{~s}) \cong \frac{\mathrm{N}}{1+\frac{\mathrm{S} \omega_{z}}{\omega_{\mathrm{plI}}^{2}}} \tag{19.39}
\end{equation*}
$$

[^3]having a $3-\mathrm{dB}$ bandwidth
\$\$

$$
\begin{equation*}
\omega_{3 \mathrm{~dB}}=\omega_{\mathrm{pII}}^{2} / \omega_{\mathrm{z}}=\omega_{\mathrm{pII}} / \mathrm{Q} \tag{19.40}
\end{equation*}
$$

$$
and a settling time constant
$$

$$
\begin{equation*}
\tau \cong \frac{\omega_{\mathrm{z}}}{\omega_{\mathrm{plI}}^{2}}=\frac{\mathrm{Q}}{\omega_{\mathrm{plI}}} \tag{19.41}
\end{equation*}
$$

\$\$

Comparing two PLLs with the same closed-loop bandwidth, one with $\mathrm{Q}=0.1$ and the other with $\mathrm{Q}=0.5$, with see that the design with $Q=0.1$ offers better tracking behavior, but results in a value of $\omega_{z}$ approximately 20 times smaller. This low-frequency zero demands a relatively large time-constant in the loop filter, often requiring off-chip components.

#### EXAMPLE 19.4

Sketch the bode plot of an open-loop second-order PLL response, $L(s)$. What is the phase margin with $\mathrm{Q}=0.5$ and $Q=0.1$ ?

#### Solution

The open-loop response $\mathrm{L}(\mathrm{s})$ in (19.33) has two poles at the origin-one from the loop filter and the other from the VCO whose output phase is the integral of its frequency. It also has one zero at $-\omega_{z}$. A bode plot is sketched in Fig. 19.10. The phase response is given by $-180^{\circ}+\operatorname{atan}\left(\omega / \omega_{z}\right)$ and the phase margin is simply atan $\left(\omega_{\mathrm{t}} / \omega_{z}\right)$. Using (19.33) and solving for $\left|L\left(j \omega_{\mathrm{t}}\right)\right|^{2}=1$, it may be shown that

$$
\begin{equation*}
\omega_{\mathrm{t}}=\frac{\omega_{\mathrm{pll}}}{\sqrt{2}} \cdot \sqrt{\frac{1}{\mathrm{Q}^{2}}+\sqrt{\frac{1}{\mathrm{Q}^{4}}+4}} \tag{19.42}
\end{equation*}
$$

and the phase margin is

$$
\begin{equation*}
\text { Phase Margin }=\operatorname{atan}\left(\frac{1}{\sqrt{2} \mathrm{Q}} \cdot \sqrt{\frac{1}{\mathrm{Q}^{2}}+\sqrt{\frac{1}{\mathrm{Q}^{4}}+4}}\right) \tag{19.43}
\end{equation*}
$$

Substitution into (19.43) reveals a phase margin of $76^{\circ}$ when $Q=0.5$. With $Q \ll 1$, (19.42) simplifies to $\omega_{\mathrm{t}} \cong \omega_{\text {pII }} / Q=\omega_{\text {pII }}^{2} / \omega_{\mathrm{z}}$ and the phase margin becomes

$$
\begin{equation*}
\text { Phase Margin } \cong \operatorname{atan}\left(\frac{\omega_{\text {pII }}^{2}}{\omega_{\mathrm{z}}^{2}}\right)=\operatorname{atan}\left(\frac{1}{Q^{2}}\right) \tag{19.44}
\end{equation*}
$$

Equation (19.44) reveals a phase margin very close to $90^{\circ}$ when $Q=0.1$. Note that in practice, additional poles in the PLL (for example, introduced by the capacitor $\mathrm{C}_{2}$ in the charge-pump loop filter of Fig. 19.7) will reduce the phase margin from these values.

### 19.2.2 Limitations of the Second-Order Small-Signal Model

A significant limitation of any continuos-time linear PLL model is that it fails to accurately predict loop behavior at high frequencies. For example, the analysis so far suggests that a PLL can be designed to have an arbitrarily large loop bandwidth. This is untrue. The problem is that a continuous-time model is being applied to a discrete-time
image_name:Fig. 19.10 Bode plot of open loop second-order PLL response, L(s).
description:The Bode plot in Fig. 19.10 illustrates the open-loop response of a second-order Phase-Locked Loop (PLL) system, denoted as L(s). This plot consists of two graphs: a magnitude plot on the left and a phase plot on the right.

Magnitude Plot (Left)
- **Type of Graph:** Logarithmic Bode magnitude plot.
- **Axes Labels and Units:**
- The vertical axis represents the magnitude of the open-loop transfer function |L(jω)| in decibels (dB).
- The horizontal axis indicates the angular frequency (ω) on a logarithmic scale.
- **Overall Behavior and Trends:**
- The magnitude plot starts at 0 dB and decreases.
- Initially, the slope is -40 dB/decade until it reaches the frequency ω_z.
- After ω_z, the slope changes to -20 dB/decade, indicating a reduction in the rate of decrease.
- **Key Features and Technical Details:**
- The plot shows a transition at ω_z, which is a zero frequency.
- Another significant frequency, ω_PLL, is marked where the slope changes.
- ω_t is the frequency where the magnitude continues to decrease at -20 dB/decade.

Phase Plot (Right)
- **Type of Graph:** Logarithmic Bode phase plot.
- **Axes Labels and Units:**
- The vertical axis represents the phase angle ∠L(jω) in degrees.
- The horizontal axis indicates the angular frequency (ω) on a logarithmic scale.
- **Overall Behavior and Trends:**
- The phase starts at -180° and increases towards 0° as frequency increases.
- There is a noticeable phase margin at ω_t.
- **Key Features and Technical Details:**
- The plot shows key phase angles at -90°, -135°, and -180° with dotted lines.
- The phase margin is indicated at ω_t, representing the difference between the phase angle and -180°.

Annotations and Specific Data Points:
- The plot includes annotations for the frequencies ω_z, ω_PLL, and ω_t.
- The phase margin is explicitly marked, highlighting its importance in stability analysis.

This Bode plot provides critical insights into the stability and frequency response of the PLL system, illustrating how the system's gain and phase shift vary with frequency.

Fig. 19.10 Bode plot of open loop second-order PLL response, L(s).
system. Specifically, the phase detector in Example 19.2 takes periodic snapshots of the phase difference between the divider output and reference input. Hence, it is a discrete-time block operating at the reference frequency. In practice, this means that loop bandwidths are restricted to significantly less than the reference frequency. Intuitively, this is obvious since phase changes can not be tracked faster than they can appear at the input. Several cycles of the reference input must be provided to allow the loop filer to average out the signal from the phase detector and adjust the VCO control input accordingly. Hence, the loop bandwidth is limited to at most roughly $1 / 20$ th to $1 / 10$ th of the reference frequency. This is a significant limitation since we often wish to maximize the bandwidth over which the output clock effectively tracks the reference. Furthermore, higher loop bandwidths permit the use of smaller components in the loop filter.

#### EXAMPLE 19.5

A PLL is to operate with a reference clock frequency of 10 MHz and an output frequency of 200 MHz . Design a loop filter for the charge-pump phase comparator so that the loop bandwidth is approximately $1 / 20$ th of the reference clock frequency and $\mathrm{Q}=0.1$. Assume the VCO has $\mathrm{K}_{\mathrm{osc}}=2 \pi \times 10^{7} \mathrm{rad} / \mathrm{Vs}$ and the charge-pump current is $\mathrm{I}_{\mathrm{ch}}=20 \mu \mathrm{~A}$.

#### Solution

From (19.32) and (19.40), it is known that with $Q \ll 0.5$ the loop bandwidth is approximately

$$
\begin{align*}
\omega_{3 \mathrm{~dB}} & \cong \frac{\omega_{\mathrm{pll}}}{Q}=\frac{1}{Q} \sqrt{\frac{K_{\mathrm{pd}} K_{\mathrm{lp}} K_{\mathrm{osc}}}{N}}  \tag{19.45}\\
& \Rightarrow K_{\mathrm{lp}}=\frac{\mathrm{Q}^{2} \omega_{3 \mathrm{~dB}}^{2} N}{K_{\mathrm{pd}} K_{\mathrm{osc}}}
\end{align*}
$$

Substituting (19.23) and (19.27) for a charge-pump PLL into (19.45) and rearranging,

$$
\begin{equation*}
\mathrm{C}_{1}=\frac{\mathrm{I}_{\mathrm{ch}} \mathrm{~K}_{\mathrm{osc}}}{2 \pi \mathrm{Q}^{2} \omega_{3 \mathrm{~dB}}^{2} \mathrm{~N}} \tag{19.46}
\end{equation*}
$$

In this example with $\omega_{3 \mathrm{~dB}}=2 \pi \cdot 10 \mathrm{MHz} / 20$, substitution of the known values into (19.46) yields a value very close to $C_{1}=100 \mathrm{pF}$. Also from (19.40), with $Q$ « 0.5 it is known that $\omega_{z} \cong \omega_{3 \mathrm{~dB}} Q^{2}$. Hence, using (19.28) for a charge-pump loop filter reveals,

$$
\begin{equation*}
R=\frac{1}{C_{1} \omega_{3 d B} Q^{2}} \tag{19.47}
\end{equation*}
$$

which in this example yields in a resistor value of $R=314 \mathrm{k} \Omega$.

The need for $\mathrm{C}_{2}$ in the loop filter circuit of Fig. 19.7 is revealed by Example 19.5. Consider what would happen in the absence of $C_{2}$ when the charge pump is active; all of the current $I_{c h}=20 \mu \mathrm{~A}$ would be driven through the series branch $R$ and $C_{1}$ generating a voltage of 6.28 V across the resistor $R$. Such a large voltage will likely cause some of the transistors in the charge pump to turn off, disturbing the dynamics of the loop.

With $\mathrm{C}_{2}$ in place as shown in Fig. 19.7, these large voltage transients will be suppressed since the voltage across $\mathrm{C}_{2}$ can not change instantaneously. The resulting loop filter transfer function is repeated here from (19.25).

$$
\begin{equation*}
\mathrm{K}_{1 \mathrm{p}} \mathrm{H}_{1 \mathrm{p}}(\mathrm{~s})=\frac{1}{\mathrm{~s}\left(\mathrm{C}_{1}+\mathrm{C}_{2}\right)} \cdot \frac{1+\mathrm{sRC}_{1}}{1+\mathrm{sR}\left(\frac{\mathrm{C}_{1} \mathrm{C}_{2}}{\mathrm{C}_{1}+\mathrm{C}_{2}}\right)} \tag{19.48}
\end{equation*}
$$

Comparing (19.48) and (19.26) reveals that the addition of $\mathrm{C}_{2}$ has two effects:

- $\mathrm{K}_{\mathrm{lp}}$ is decreased, but this effect will be small if $\mathrm{C}_{2}$ is taken much smaller than $\mathrm{C}_{1}$
- a real pole is introduced at a frequency $\left(C_{1}+C_{2}\right) /\left(R C_{1} C_{2}\right)>\omega_{z}$

The additional pole makes the closed-loop system third-order and reduces the phase margin somewhat compared to the results obtained in Example 19.4 for a second-order loop. However, placing the new pole at approximately 2 times the loop bandwidth, $2 \omega_{3 \mathrm{~dB}}$, provides the desired glitch-suppression without much effect on the settling time or jitter peaking of the loop. For example, with $\mathrm{Q}=0.5$ this corresponds to selecting $\mathrm{C}_{2}$ equal to one-tenth to oneeighth the value of $C_{1}$. With $Q=0.1$, the value of $C_{2}$ should be roughly $1 / 250$ th the value of $C_{1}$.

#### EXAMPLE 19.6

Select a capacitor value $\mathrm{C}_{2}$ for the loop filter designed in Example 19.5.

#### Solution

Since the loop is designed with $\mathrm{Q}=0.1$, a value of $\mathrm{C}_{2}=\mathrm{C}_{1} / 250 \cong 0.4 \mathrm{pF}$ is chosen.

Example 19.5 and Example 19.6 also illustrate the practical challenge of designing for a very small value of Q : it leads to large component values and large spreads in component values.

#### EXAMPLE 19.7

Repeat the design in Example 19.5 but with $Q=0.5$.

#### Solution

The design is performed by initially using the second-order model and ignoring $\mathrm{C}_{2}$. Once $\mathrm{C}_{1}$ and R are chosen, a value for $\mathrm{C}_{2}$ is calculated under the assumption that it will have only a small effect on the loop bandwidth. For $Q=0.5$, using (19.32) and (19.38),

$$
\begin{align*}
\omega_{3 \mathrm{~dB}} & \cong 2.5 \omega_{\mathrm{plI}}=2.5 \sqrt{\frac{\mathrm{~K}_{\mathrm{pd}} \mathrm{~K}_{\mathrm{lp}} \mathrm{~K}_{\mathrm{osc}}}{\mathrm{~N}}} \\
& \Rightarrow \mathrm{~K}_{\mathrm{lp}}=\frac{\omega_{3 \mathrm{~dB}}^{2} \mathrm{~N}}{(2.5)^{2} \mathrm{~K}_{\mathrm{pd}} \mathrm{~K}_{\mathrm{osc}}} \tag{19.49}
\end{align*}
$$

Again substituting (19.23) and (19.27) for a charge-pump PLL into (19.49) and rearranging,

$$
\begin{equation*}
C_{1}=\frac{(2.5)^{2} I_{\mathrm{ch}} \mathrm{~K}_{\mathrm{osc}}}{2 \pi \omega_{3 \mathrm{~dB}}^{2} \mathrm{~N}} \tag{19.50}
\end{equation*}
$$

The known values, including $\omega_{3 \mathrm{~dB}}=2 \pi \cdot 10 \mathrm{MHz} / 20$, substituted into (19.50) yields a capacitance of $\mathrm{C}_{1}=6.25 \mathrm{pF}$. Combining (19.38) and $\mathrm{Q}=\omega_{\mathrm{z}} / \omega_{\mathrm{pII}}$, we see that $\omega_{\mathrm{z}}=Q \omega_{3 \mathrm{~dB}} / 2.5$ which, for a charge-pump loop filter, implies

$$
\begin{equation*}
R=\frac{2.5}{C_{1} \omega_{3 \mathrm{~dB}} Q} \tag{19.51}
\end{equation*}
$$

The numerical result in this case is $\mathrm{R}=255 \mathrm{k} \Omega$. Finally, a value of $\mathrm{C}_{2}=\mathrm{C}_{1} / 10=0.625 \mathrm{fF}$ is used to suppress glitches while placing the additional pole beyond the loop bandwidth.

Notice that the component values in Example 19.7 with $Q=0.5$ are much more readily integrated than those in Example 19.5 and Example 19.6 which use $Q=0.1$. The trade-off is increased overshoot and jitter peaking in the closed-loop PLL response.

### 19.2.3 PLL Design Example

Although the details of a PLL design procedure will depend, of course, on which aspects of the system are specified, the following points provide basic direction.

- The ratio between the desired output frequency and the input reference frequency sets the divider ratio, N .
- The VCO gain constant $\mathrm{K}_{\text {osc }}$ is usually determined by circuit design considerations in the VCO, but generally must be large enough to allow the VCO to cover the expected variations in its free-running frequency and desired output frequency.
- When minimal jitter peaking or fast settling of the loop are important design specifications, a value of $\mathrm{Q} « 0.5$ is desired, with $\mathrm{Q}=0.1$ being a reasonable choice. However, $\mathrm{Q}=0.5$ will usually result in loop filer component values that are easier to realize.
- When a high-quality (low-noise) input reference clock is available, a high loop bandwidth is desirable. However, the loop bandwidth is limited to at most one-tenth of the input reference frequency to ensure robust stability.
- Once the loop bandwidth is specified, choose $\omega_{\mathrm{pII}}=0.4 \omega_{3 \mathrm{~dB}}$ for $\mathrm{Q}=0.5^{6}$, or take $\omega_{\mathrm{pII}}=Q \omega_{3 \mathrm{~dB}}$ for Q «0.5 ${ }^{7}$.
- With N and $\mathrm{K}_{\text {osc }}$ determined as described, $\mathrm{K}_{p d}$ and $\mathrm{K}_{\mathrm{lp}}$ are chosen to give the desired value of $\omega_{\mathrm{plI}}=\sqrt{\mathrm{K}_{\mathrm{pd}} \mathrm{K}_{\mathrm{lp}} \mathrm{K}_{\mathrm{osc}} / \mathrm{N}^{8}}$. In a charge-pump PLL, this amounts to choosing $\mathrm{I}_{\mathrm{ch}}=2 \pi \mathrm{~K}_{\mathrm{pd}}{ }^{9}$ and $\mathrm{C}_{1}$ ( $\cong 1 / \mathrm{K}_{\mathrm{Ip}}$ neglecting $\mathrm{C}_{2}{ }^{10}$ ). The designer has one degree of freedom here which is used to influence the

[^4]image_name:Fig. 19.11 A general integer-N PLL architecture.
description:The diagram represents a general integer-N Phase-Locked Loop (PLL) architecture. This system is used to synchronize an output oscillator frequency with a reference frequency. Here is a detailed breakdown of the components and their interactions:

1. **Main Components:**
- **Input Divider (÷ M):** This block divides the input frequency \( f_{in} \) by a factor of M, producing \( \frac{f_{in}}{M} \).
- **Phase Detector:** This component compares the divided input frequency \( \frac{f_{in}}{M} \) with the feedback frequency from the output. It generates an error signal proportional to the phase difference.
- **Loop Filter:** The error signal from the phase detector is passed through the loop filter, which smooths the signal and determines the dynamic response of the PLL. The output of the loop filter is a control voltage \( V_{cntl} \).
- **Voltage-Controlled Oscillator (VCO):** The VCO takes the control voltage \( V_{cntl} \) and adjusts its output frequency \( f_{osc} \) accordingly.
- **Feedback Divider (÷ N):** This block divides the VCO output frequency \( f_{osc} \) by a factor of N, feeding it back to the phase detector.

2. **Flow of Information or Control:**
- The input frequency \( f_{in} \) is divided by M and sent to the phase detector.
- The VCO output frequency \( f_{osc} \) is divided by N and also sent to the phase detector.
- The phase detector compares these two frequencies and outputs an error signal.
- The loop filter processes this error signal to produce a control voltage \( V_{cntl} \).
- The VCO adjusts its frequency \( f_{osc} \) based on \( V_{cntl} \), closing the loop.

3. **Labels, Annotations, and Key Indicators:**
- The output frequency is described by the equation \( f_{osc} = \frac{N}{M} f_{in} \), indicating the relationship between the input and output frequencies.
- The diagram shows the flow of signals with arrows, indicating the direction of signal processing and feedback.

4. **Overall System Function:**
- The primary function of this integer-N PLL is to lock the VCO output frequency to be a multiple of the input frequency. By adjusting the division factors M and N, the system can produce an output frequency that is a rational multiple of the input frequency, \( \frac{N}{M} f_{in} \). This architecture is commonly used in frequency synthesis, clock generation, and modulation/demodulation applications.

Fig. 19.11 A general integer-N PLL architecture.
size of the loop filter components, the power consumption in the phase detector, and the noise in the loop filter (since a smaller resistor value will generally reduce noise in the loop filter).

- Take $\omega_{\mathrm{z}}=Q \omega_{\text {pII }}{ }^{11}$. In a charge-pump PLL, this amounts to choosing $R=1 / \omega_{\mathrm{z}} \mathrm{C}_{1}{ }^{12}$.
- In a charge-pump PLL, an additional pole is introduced by the glitch-suppression capacitor $\mathrm{C}_{2}$. With $\mathrm{Q}=0.5$, select $C_{2}$ between one-tenth and one-eighth the value of $C_{1}$. With $Q=0.1$, the value of $C_{2}$ should be roughly $1 / 250$ th the value of $\mathrm{C}_{1}$.

#### EXAMPLE 19.8

Design a charge-pump PLL that accepts a fixed 40 MHz reference and can produce an output clock frequency anywhere in the range 1.4 GHz to 1.6 GHz in 20 MHz steps. For each output frequency, a different division ratio is used. In order to cover the full range of output frequencies while the control voltage changes by only $2 \mathrm{~V}, \mathrm{~K}_{\text {osc }}$ is chosen to be $2 \pi \cdot 10^{8} \mathrm{rad} / \mathrm{s} \cdot V$. Select the value of $I_{\mathrm{ch}}$ and the loop filter components $C_{1}, R$, and $C_{2}$.

#### Solution

The output frequency is N -times higher than the input frequency, so changing the division ratio N allows the output frequency to be placed at different integer multiples of the input reference. Hence, this architecture is called an integer- $\boldsymbol{N P L L}$. When the output frequency must be set with a resolution finer than the available reference signal, an additional divider is applied to the input to reduce its frequency. The general architecture is shown in Fig. 19.11 and produces an output frequency of $(\mathrm{N} / \mathrm{M}) \mathrm{f}_{\mathrm{in}}$.

In this case, since the output frequency resolution requirement is 20 MHz , a divide-by-2 $(\mathrm{M}=2)$ is applied to the $40-\mathrm{MHz}$ input. To cover the full range of output frequencies, N must be programmable to any integer from 70 to 80 . A value of $Q=0.5$ is selected and, assuming the input reference has very low noise, the loop bandwidth is set to one-tenth of $20 \mathrm{MHz}: \omega_{3 \mathrm{~dB}}=2 \pi \cdot 2 \mathrm{MHz}$. Hence,

$$
\omega_{\mathrm{pII}}=0.4 \omega_{3 \mathrm{~dB}}=2 \pi \cdot 800 \mathrm{kHz}
$$

[^5]12. equation (19.28)

Combining equations (19.23), (19.27), and (19.32) and rearranging yields

$$
\begin{equation*}
\frac{\mathrm{I}_{\mathrm{ch}}}{\mathrm{C}_{1}}=\omega_{\mathrm{pll}}^{2} \frac{2 \pi \mathrm{~N}}{\mathrm{~K}_{\mathrm{osc}}} \tag{19.52}
\end{equation*}
$$

Substituting the values in this example, $\mathrm{I}_{\mathrm{ch}} / \mathrm{C}_{1} \cong 20 \cdot 10^{6} \mathrm{~V} / \mathrm{s}$. A reasonable choice is $\mathrm{I}_{\mathrm{ch}}=100 \mu \mathrm{~A}$ and $\mathrm{C}_{1}=5 \mathrm{pF}$. The resistor must then be chosen to place a zero at $\omega_{\mathrm{z}}=Q \omega_{\mathrm{pII}}=2 \pi \cdot 400 \mathrm{kHz}$. Hence, $R=1 /\left(\omega_{z} C_{1}\right) \cong 80 \mathrm{k} \Omega$. Finally, with $Q=0.5$, a good choice is to select $C_{2}=C_{1} / 10=0.5 \mathrm{pF}$.

## 19.3 JITTER AND PHASE NOISE

Key Point: Jitter is a measure of random variations in the timing phase of a clock signal and phase noise is its frequency-domain representation. They present fundamental limitations on the accuracy of time references.

Key Point: The absolute jitter of a clock, $\tau_{k}$ is a discrete-time sequence giving the displacement of its transition times away from their ideal values.

Unlike most analog signals on integrated circuits where the value of a voltage or current bears the information, the important aspects of a clock waveform are the times at which it transitions across some particular threshold. Jitter is the random variation in these times and phase noise is the frequency-domain representation of jitter. Since jitter and phase noise arise from thermal and other noise processes present in all circuits, they represent fundamental limitations on the accuracy of any on-chip time reference making them central to PLL design.

A typical clock signal is illustrated in Fig. 19.12. The transition times are labeled $t_{k}$. These may be the times when a logic signal changes state or when current switches from one branch to another. For this example only the rising transitions are considered, but in a real circuit either the rising transitions, falling transitions, or both may be of interest. For an ideal clock the transitions are equally spaced so that $t_{k}=k T_{0}$ where $T_{0}$ is the clock period. In any practical clock, however, the transitions are displaced
from their ideal times.
Specifically, let the deviation in the transition times from their ideal values be a discrete-time sequence $\tau_{k}$.

$$
\begin{equation*}
\mathrm{t}_{\mathrm{k}}=\mathrm{k} \mathrm{~T}_{0}+\tau_{\mathrm{k}} \tag{19.53}
\end{equation*}
$$

The sequence $\tau_{\mathrm{k}}$ is the absolute jitter of the clock in time units. It can also be normalized to radians.

$$
\begin{equation*}
\phi_{\mathrm{k}}=\tau_{\mathrm{k}} \cdot\left(2 \pi / \mathrm{T}_{0}\right) \tag{19.54}
\end{equation*}
$$

Absolute jitter is a useful analytical tool. However, it is not directly measured in a lab since doing so requires access to an "ideal" clock.

#### EXAMPLE 19.9

Find the absolute jitter of a sinusoid of amplitude A and angular frequency $\omega_{0}$ in additive white noise $n(t)$ with variance $\sigma_{n}^{2}$.

#### Solution

The sinusoid may be described as follows:
image_name:Fig. 19.12
description:The graph in Fig. 19.12 illustrates the concept of absolute jitter by comparing an ideal clock waveform to a practical one.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph showing two periodic signals: an ideal clock waveform and a practical clock waveform.

2. **Axes Labels and Units:**
- The horizontal axis represents time (t) in arbitrary units, with specific time points marked as \( t_0, t_1, t_2, \) and \( t_3 \).
- The vertical axis represents the amplitude of the waveform but is not explicitly labeled with units.

3. **Overall Behavior and Trends:**
- The ideal waveform is a perfect square wave with consistent periods marked as \( T_0 \), starting at \( t_0 = 0 \), \( t_1 = T_0 \), \( t_2 = 2T_0 \), and \( t_3 = 3T_0 \).
- The practical waveform shows the same square wave but with slight variations in the timing of the transitions, illustrating the effect of jitter.

4. **Key Features and Technical Details:**
- The ideal waveform has sharp transitions at every \( T_0 \) interval.
- The practical waveform deviates slightly from the ideal, with transition times marked as \( t_0 = 0 + \tau_0 \), \( t_1 = T_0 + \tau_1 \), \( t_2 = 2T_0 + \tau_2 \), and \( t_3 = 3T_0 + \tau_3 \), where \( \tau \) represents the jitter.
- This deviation is the primary focus, highlighting how the practical clock's transitions are disturbed from the nominal values.

5. **Annotations and Specific Data Points:**
- The graph clearly marks the nominal transition times and the adjusted times due to jitter, making it easy to visualize the impact of noise or other disturbances on the clock signal.
- The periods \( T_0, T_1, T_2 \) are indicated, with \( T_1 \) and \( T_2 \) representing the slightly altered periods in the practical waveform due to jitter effects.

Fig. 19.12 Illustration of absolute jitter in a practical clock waveform.

$$
\begin{equation*}
\mathrm{v}(\mathrm{t})=\mathrm{A} \sin \left(\omega_{0} \mathrm{t}\right)+\mathrm{n}(\mathrm{t}) \tag{19.55}
\end{equation*}
$$

Assuming the noise n is much smaller than the amplitude of oscillation, $\sigma_{\mathrm{n}}$ « A , the transition times of $\mathrm{v}(\mathrm{t})$ are disturbed only slightly from their nominal values $\mathrm{kT}_{0}$. The amount of disturbance can be estimated from the slope of the sinusoid around the transition times, $A \omega_{0}$, and samples of the noise, $n(t)$, labeled $n_{k}$.

$$
\begin{equation*}
\tau_{\mathrm{k}} \cong \frac{\mathrm{n}_{\mathrm{k}}}{\mathrm{~A} \omega_{0}} \tag{19.56}
\end{equation*}
$$

The discrete-time noise process, $\mathrm{n}_{\mathrm{k}}$, is white with variance $\sigma_{\mathrm{n}}^{2}$. Hence, absolute jitter is also a discrete-time white noise process with variance

$$
\begin{equation*}
\sigma_{\tau}^{2}=\frac{\sigma_{n}^{2}}{A^{2} \omega_{0}^{2}} \tag{19.57}
\end{equation*}
$$

At high frequencies $\omega_{0}$ and when the sinusoid has high amplitude A , the jitter is reduced because the sinusoid will have a high slope around its zero-crossings. Expressed in radians, the effect of frequency is cancelled.

$$
\begin{equation*}
\sigma_{\phi}^{2}=\sigma_{\tau}^{2} \cdot\left(\frac{2 \pi}{T_{0}}\right)^{2}=\frac{\sigma_{n}^{2}}{A^{2}} \tag{19.58}
\end{equation*}
$$

Fig. 19.13 A noise source resistance introduces jitter.
i(t)
image_name:Fig. 19.13
description:
[
name: I(t), type: CurrentSource, ports: {Np: V(t), Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: V(t), N2: Node2}
name: C, type: Capacitor, value: C, ports: {Np: V(t), Nn: GND}
]
extrainfo:The circuit consists of a current source connected to a resistor and a capacitor in series, with both the resistor and capacitor connected to ground.

$\mathrm{v}(\mathrm{t})$
image_name:Fig. 19.13
description:The function graph depicted in Fig. 19.13 is a time-domain waveform. The x-axis likely represents time, although no specific units or scale are provided, and the y-axis represents voltage, denoted as \( v(t) \). The waveform exhibits a jagged, irregular pattern, indicating fluctuations in voltage over time.

Overall Behavior and Trends:
- The waveform displays a series of sharp peaks and valleys, suggesting rapid changes in voltage.
- There is no obvious periodicity, implying a non-repetitive or noise-like signal.
- The general trend of the waveform is difficult to ascertain due to its erratic nature, but it seems to maintain a relatively constant amplitude range.

Key Features and Technical Details:
- The waveform does not appear to have any distinct zero crossings, maxima, or minima labeled.
- There are no clear annotations or reference lines to indicate specific voltage levels or time intervals.

Annotations and Specific Data Points:
- The graph lacks numerical values for key data points, making precise analysis challenging.
- No additional markers or reference lines are present to indicate significant features such as cutoff frequencies or phase shifts.

This waveform may represent the voltage across the capacitor in the given circuit, affected by jitter introduced by the current source, as mentioned in the context. The erratic nature of the waveform aligns with the concept of jitter, which introduces variability in the timing of the signal.

#### EXAMPLE 19.10

In Fig. 19.13, assume $i(t)$ is an ideal sinusoidal current source with amplitude $1 \mathrm{~mA}, \mathrm{R}=1 \mathrm{k} \Omega$, and $\mathrm{C}=1 \mathrm{pF}$. Find the variance of absolute jitter at $v(\mathrm{t})$ when the signal is at a frequency 1 MHz . Also find the variance when the signal is at 1 GHz .

#### Solution

The voltage $\mathrm{v}(\mathrm{t})$ will be in exactly the form of $(19.55)$ where $\mathrm{n}(\mathrm{t})$ is the gaussian-distributed voltage noise arising from the thermal noise of $R$. The variance of $n(t)$ is

$$
\begin{equation*}
\sigma_{n}^{2}=\frac{k T}{C} \tag{19.59}
\end{equation*}
$$

which, at a temperature of 300 K has an rms value of $64.4 \mu \mathrm{~V}$. The amplitude, A , of the sinusoid in (19.55) depends upon the oscillation frequency f . At 1 MHz , the amplitude will be very close to $(1 \mathrm{~mA})(1 \mathrm{k} \Omega)=1 \mathrm{~V}$. Hence, by substitution into (19.57),

$$
\sigma_{\tau}^{2}=\frac{(64.4 \mu \mathrm{~V})^{2}}{(1 \mathrm{~V})^{2}\left(2 \pi 10^{6}\right)^{2}}=(10.2 \mathrm{ps})^{2}
$$

At 1 GHz , the amplitude at $\mathrm{v}(\mathrm{t})$ is attenuated by the lowpass RC filter so that $\mathrm{A}=0.157 \mathrm{~V}$. Hence,

$$
\sigma_{\tau}^{2}=\frac{(64.4 \mu \mathrm{~V})^{2}}{(0.157 \mathrm{~V})^{2}\left(2 \pi 10^{9}\right)^{2}}=(0.065 \mathrm{ps})^{2}
$$

Note that although in time units there is less jitter in the 1 GHz case, the jitter expressed in radians is actually higher at 1 GHz because of the reduced amplitude at $\mathrm{v}(\mathrm{t})$.

Phase noise is the frequency-domain representation of absolute jitter. Thus, we define $\mathrm{S}_{\phi}(\mathrm{f})$, the phase noise of a clock signal with random jitter, as the power spectral density of the sequence $\phi_{\mathrm{k}}{ }^{13}$ Recall that a voltage noise spectral density specifies the power of a voltage signal in any 1-Hz-wide bin of frequency spectrum, and hence has units of $V^{2} / H z$. Similarly, $S_{\phi}(f)$ specifies the power of $\phi_{k}$ in $\mathrm{rad}^{2}$ within any $1-\mathrm{Hz}$-wide frequency bin, and hence has units of $\mathrm{rad}^{2} / \mathrm{Hz}$. Furthermore, the variance of $\phi_{k}$ is given by the integral of $S_{\phi}(f)$ over all frequencies. Since it is customary to quantify jitter in units of time rather than radians, this is usually expressed as follows:

[^6]image_name:(a)
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: Vo, G: X}
name: Rd, type: Resistor, value: Rd, ports: {N1: Vo, N2: VDD}
name: Vs, type: VoltageSource, value: Vs, ports: {Np: X, Nn: Vbias}
name: Vbias, type: VoltageSource, value: Vbias, ports: {Np: Vbias, Nn: GND}
]
extrainfo:This is a common source amplifier circuit with an NMOS transistor (Q1) and a load resistor (Rd). The circuit includes a voltage source (Vs) for the input signal and a bias voltage source (Vbias). The small-signal model includes a voltage-controlled current source (gm1Vgs1) and a parallel resistor (Rd||ro1) representing the output resistance.
image_name:(b)
description:The circuit diagram (b) represents a small-signal equivalent model including transistor noise sources for a common source amplifier. The NMOS transistor Q1 is biased with Vbias and has a load resistor Rd connected to the drain. The input signal is provided by Vs.

Fig. 19.14 (a) Common source amplifier in Example 19.11. (b) Small-signal equivalent, including transistor noise sources.

$$
\begin{equation*}
\sigma_{\tau}^{2}=\left(\frac{T_{0}}{2 \pi}\right)^{2} \int_{0}^{1 / 2 T_{0}} S_{\phi}(f) d f \tag{19.60}
\end{equation*}
$$

Taking the square root of both sides gives the root-mean-square (rms) absolute jitter.

$$
\begin{equation*}
\sigma_{\tau}=\frac{T_{0}}{2 \pi} \sqrt{\int_{0}^{1 / 2 T_{0}} S_{\phi}(f) d f} \tag{19.61}
\end{equation*}
$$

Equations (19.60) and (19.61) are key relationships between absolute jitter in the time-domain and phase noise.

#### EXAMPLE 19.11

Consider the common source amplifier in Fig. 19.14(a). Transistor $\mathrm{Q}_{1}$ is biased in saturation by dc source $\mathrm{V}_{\text {bias }}$ and $\mathrm{v}_{\mathrm{s}}$ is a noiseless small-signal sinusoid of amplitude $\left|\mathrm{V}_{\mathrm{s}}\right|$. Estimate the phase noise at the output including thermal noise of the resistor and transistor as well as flicker noise.

#### Solution

The small-signal equivalent circuit is shown in Fig. 19.14(b). The voltage noise source $\mathrm{v}_{\mathrm{n} 1}$ models the flicker noise of the transistor $Q_{1}$ and has a noise spectral density,

$$
V_{n 1}^{2}(f)=\frac{K}{W L C_{o x} f}
$$

The current noise source $i_{n}$ includes the thermal noise of both the transistor and resistor,

$$
\mathrm{i}_{\mathrm{n}}^{2}(\mathrm{f})=4 \mathrm{kT}\left(\frac{2}{3}\right) \mathrm{g}_{\mathrm{m}}+\frac{4 \mathrm{kT}}{\mathrm{R}_{\mathrm{d}}}
$$

The resulting voltage at $\mathrm{v}_{0}$ takes on the form of (19.55)—a sinusoidal voltage in additive noise. The sinusoidal component has amplitude $\left|V_{s}\right| g_{m 1}\left(R_{d}| | r_{01}\right)$. The voltage noise spectral density at $v_{0}$ is obtained by a routine noise circuit analysis of Fig. 19.14(b).

$$
v_{o, n}^{2}(f)=\left[\frac{K}{W L C_{o x}} g_{m 1}^{2}\left(R_{d}| | r_{01}\right)^{2}+4 k T\left(\frac{2}{3}\right) g_{m}\left(R_{d}| | r_{o 1}\right)^{2}+\frac{4 k T}{R_{d}}\left(R_{d}| | r_{o 1}\right)^{2}\right]
$$

Assuming that the zero-crossings of the sinusoidal waveform at $\mathrm{v}_{0}$ are disturbed only a small amount by the noise, the approximation in (19.56) may be applied. In terms of phase,

$$
\phi_{\mathrm{k}} \cong \frac{\mathrm{n}_{\mathrm{k}}}{\left|\mathrm{~V}_{\mathrm{s}}\right|}
$$

where $n_{k}$ is the sampled noise voltage $v_{o, n}$. Therefore, the phase noise is,

$$
S_{\phi}(f)=\frac{\left(R_{d}| | r_{o 1}\right)^{2}}{\left|V_{s}\right|^{2}}\left[\frac{K}{W L C_{o x}} g_{m 1}^{2}+4 k T\left(\frac{2}{3}\right) g_{m}+\frac{4 k T}{R_{d}}\right]
$$

Note that it has a $1 / \mathrm{f}$ component and a white component. ${ }^{14}$

### 19.3.1 Period Jitter

Several other measures of jitter are also possible. A jittered clock will have a time-varying period, as shown in Fig. 19.12,

$$
\begin{equation*}
T_{k}=t_{k+1}-t_{k}=T_{0}+\tau_{k+1}-\tau_{k} \tag{19.62}
\end{equation*}
$$

The deviation of the period away from its nominal value of $\mathrm{T}_{0}$ is the period jitter, also sometimes referred to as the cycle jitter.

$$
\begin{equation*}
J_{k}=T_{k}-T_{0}=\tau_{k+1}-\tau_{k} \tag{19.63}
\end{equation*}
$$

Equation (19.63) reveals that period jitter is obtained by passing the absolute jitter sequence, $\tau_{\mathrm{k}}$, through a discrete-time $(z-1)$ filter. Hence, its variance is the integral of phase noise filtered by a $(z-1)$ filter.

$$
\begin{equation*}
\sigma_{J}^{2}=\left(\frac{T_{0}}{\pi}\right)^{2} \int_{0}^{1 / 2 \mathrm{~T}_{0}} \sin ^{2}\left(\pi \mathrm{fT}_{0}\right) \mathrm{S}_{\phi}(\mathrm{f}) \mathrm{df} \tag{19.64}
\end{equation*}
$$

The term $\sin ^{2}\left(\pi \mathrm{fT}_{0}\right)$ in the integrand of $(19.64)$ is due to the $(z-1)$ filter.
Period jitter is more easily measured in a lab than the absolute jitter, since no reference is required. Furthermore, the period jitter is of significant practical importance in digital systems where the maximum permissible logic delays will depend on the period jitter of the synchronizing clock.

[^7]
### 19.3.2 P-Cycle Jitter

The idea of period jitter is easily extended by considering variations in the duration of P consecutive clock cycles from its ideal value, $\mathrm{PT}_{0}$.

$$
\begin{equation*}
J(P)_{k}=t_{k+P}-t_{k}-P T_{0}=\tau_{k+P}-\tau_{k} \tag{19.65}
\end{equation*}
$$

Called the P-cycle period jitter or simply $P$-cycle jitter, $\mathrm{J}(\mathrm{P})_{\mathrm{k}}$ is obtained by passing the absolute jitter sequence, $\tau_{\mathrm{k}}$, through a discrete-time $\left(z^{P}-1\right)$ filter. Hence, its variance is the integral of phase noise filtered by a $\left(z^{p}-1\right)$ filter.

$$
\begin{equation*}
\sigma_{J(\mathrm{P})}^{2}=\left(\frac{\mathrm{T}_{0}}{\pi}\right)^{2} \int_{0}^{1 / 2 \mathrm{~T}_{0}} \sin ^{2}\left(\pi \mathrm{fPT}_{0}\right) \mathrm{S}_{\phi}(\mathrm{f}) \mathrm{df} \tag{19.66}
\end{equation*}
$$

Period jitter is a special case of the P -cycle jitter where $P=1$. Measurements of $\sigma_{J(P)}$ for different values of P are easily done in a lab and reveal much information about the spectral properties of phase noise due to the differently shaped filters applied in (19.66) for different values of P .

### 19.3.3 Adjacent Period Jitter

Yet another measurement of jitter is obtained by looking at the difference between the duration of each period and the following period.

$$
\begin{equation*}
J_{k+1}-J_{k} \tag{19.67}
\end{equation*}
$$

The so-called adjacent period jitter, also sometimes called cycle-to-cycle jitter, is therefore mathematically obtained by passing the period jitter $J_{k}$ through yet another $(z-1)$ filter or equivalently by passing the absolute jitter through a $(z-1)^{2}$ filter. Hence, it is related to phase noise by the following integral,

$$
\begin{equation*}
\sigma_{C}^{2}=\left(\frac{2 T_{0}}{\pi}\right)^{2} \int_{0}^{1 / 2 T_{0}} \sin ^{4}\left(\pi f T_{0}\right) S_{\phi}(f) d f \tag{19.68}
\end{equation*}
$$

#### EXAMPLE 19.12

What is the rms period jitter of the sinusoid in additive white noise from Example 19.9?

#### Solution

Again assuming the noise is much smaller than the amplitude of oscillation, $\sigma_{n}$ « A , it was shown in Example 19.9 that the absolute jitter is also white. Hence, the phase noise is constant. Combining (19.57) and (19.60) therefore yields

$$
\begin{equation*}
S_{\phi}(f)=\left(\frac{8 \pi^{2}}{T_{0}}\right)\left(\frac{\sigma_{n}^{2}}{A^{2} \omega_{0}^{2}}\right)=\frac{2 T_{0} \sigma_{n}^{2}}{A^{2}} \tag{19.69}
\end{equation*}
$$

Integration in (19.64) gives the variance of the period jitter.

$$
\begin{equation*}
\sigma_{J}^{2}=\frac{2 \sigma_{n}^{2}}{A^{2} \omega_{0}{ }^{2}} \tag{19.70}
\end{equation*}
$$

The rms period jitter is the square root of (19.70).

#### EXAMPLE 19.13

A clock's zero crossings are modulated by a sinusoidal disturbance at a frequency $f_{m}$ so that

$$
\begin{equation*}
\phi_{\mathrm{k}}=\Phi_{0} \sin \left(2 \pi \mathrm{f}_{\mathrm{m}} \mathrm{t}\right) \tag{19.71}
\end{equation*}
$$

What is the resulting rms absolute jitter, period jitter, and adjacent period jitter?

#### Solution

The phase noise $S_{\phi}^{2}(f)$ will have a discrete spectral tone at $f_{m}$.

$$
S_{\phi}(f)=\frac{\Phi_{0}^{2}}{2} \delta\left(f-f_{m}\right)
$$

Key Point: Periodic variations in the phase of a clock result in discrete tones in phase noise spectra and are called spurs.

Discrete tones in phase noise spectra are called spurs because on a plot of $S_{\phi}^{2}(\mathrm{f})$ versus frequency they appear as vertical spikes. The integral in (19.60) is easily evaluated to give the absolute jitter,

$$
\begin{equation*}
\sigma_{\tau}^{2}=\left(\frac{T_{0}}{2 \pi}\right)^{2}\left(\frac{\Phi_{0}^{2}}{2}\right)=\frac{1}{8}\left(\frac{T_{0} \Phi_{0}}{\pi}\right)^{2} \tag{19.72}
\end{equation*}
$$

The period jitter is reduced slightly by the extra term in the integrand of (19.64) because the change in absolute jitter from one transition to the next is less than the total range over which it deviates.

$$
\begin{equation*}
\sigma_{J}^{2}=\frac{1}{2}\left(\frac{T_{0} \Phi_{0}}{\pi}\right)^{2} \sin ^{2}\left(\pi \mathrm{f}_{\mathrm{m}} \mathrm{~T}_{0}\right) \tag{19.73}
\end{equation*}
$$

Note that if the phase modulation is slow (i.e. $f_{m} T_{0}$ « $)$ the period jitter is small since $\phi_{k}$ varies very little from one cycle to the next. The same is true of adjacent period jitter.

$$
\begin{equation*}
\sigma_{C}^{2}=2\left(\frac{T_{0} \Phi_{0}}{\pi}\right)^{2} \sin ^{4}\left(\pi f_{m} T_{0}\right) \tag{19.74}
\end{equation*}
$$

### 19.3.4 Other Spectral Representations of Jitter

Phase noise is the spectral representation of the phase of an oscillatory waveform, but this is difficult to observe in practice since it requires a perfect time-reference. It is much easier to observe the spectrum of the oscillatory waveform itself. Let us denote the power spectral density of a clock waveform (e.g. $\mathrm{v}(\mathrm{t})$ in Example 19.10) $\mathrm{S}_{\mathrm{v}}(\mathrm{f}$ ).
image_name:(a)
description:The graph labeled as (a) is a plot of power spectral density (PSD), denoted as \( S_v(f) \), versus frequency \( f \). This graph illustrates the effect of jitter on the spectral distribution of an oscillatory waveform.

1. **Type of Graph and Function:**
- This is a frequency-domain graph showing power spectral density.

2. **Axes Labels and Units:**
- The x-axis represents frequency \( f \) in hertz (Hz).
- The y-axis represents the power spectral density \( S_v(f) \).
- The scale appears to be linear for both axes.

3. **Overall Behavior and Trends:**
- The graph shows three curves representing different levels of jitter: "no jitter," "some jitter," and "more jitter."
- The curve labeled "no jitter" is a sharp peak at the frequency \( 1/T_0 \), indicating a pure sinusoidal waveform with power concentrated at a single frequency.
- As jitter increases ("some jitter" and "more jitter"), the curves broaden, indicating that power is spread over a wider range of frequencies around \( 1/T_0 \), which suggests increased phase noise.

4. **Key Features and Technical Details:**
- The peak of the "no jitter" curve is located precisely at \( 1/T_0 \), which is the carrier frequency.
- With "some jitter," the peak is still centered around \( 1/T_0 \) but with a wider base, indicating some frequency spread.
- The "more jitter" curve shows an even broader distribution, representing significant frequency spread due to increased jitter.

5. **Annotations and Specific Data Points:**
- The graph is annotated with labels for "no jitter," "some jitter," and "more jitter," highlighting the impact of jitter on the PSD.
- The central frequency \( 1/T_0 \) acts as a reference point for the spectral distribution.
image_name:(b)
description:The graph in Fig. 19.15 (b) is a plot of the normalized power spectral density, denoted as \( \mathfrak{L}(\Delta f) \), against the frequency offset \( \Delta f \). This type of graph is typically used to represent phase noise or jitter in oscillatory systems.

Axes Labels and Units:
- **Horizontal Axis (x-axis):** Represents the frequency offset \( \Delta f \), which is the deviation from the carrier frequency. The units are typically in hertz (Hz).
- **Vertical Axis (y-axis):** Represents the normalized power spectral density \( \mathfrak{L}(\Delta f) \). The units are usually in a logarithmic scale, such as decibels relative to the carrier power (dBc/Hz).

Overall Behavior and Trends:
- The graph shows a decreasing trend as \( \Delta f \) increases. This indicates that the power spectral density is highest near the carrier frequency and diminishes as the frequency offset increases.
- The curve starts at a high value when \( \Delta f \) is near zero and gradually falls off, suggesting an exponential or power-law decay.

Key Features and Technical Details:
- The peak at \( \Delta f = 0 \) signifies the carrier frequency where the power is most concentrated.
- The decay of the curve represents the spreading of power due to phase noise or jitter, which causes energy to distribute over a range of frequencies.
- The shape of the curve can indicate the nature and severity of the jitter; a steeper decline suggests less jitter, while a more gradual slope indicates more significant jitter.

Annotations and Specific Data Points:
- There are no specific numerical values or annotations provided on the graph. However, the shape and slope of the curve are critical for understanding the level of phase noise present in the system.

Fig. 19.15 (a) The power spectral densities of oscillatory waveforms with and without jitter. (b) The normalized power spectral density, $\mathfrak{L}(\Delta f)$.

Clearly it will be concentrated around the oscillating frequency, $\omega_{0}$, sometimes called the carrier frequency. A pure sinusoid with no variation it its period (hence, no jitter) will of course have only a single tone at ( $1 / \mathrm{T}_{0}$ ). A practical signal, however, will have power in a range of frequencies around the carrier, as shown in Fig. 19.15.

Signals with more jitter will have more power in the tails of $S_{v}(f)$. However, the power in those tails is also proportional to the squared amplitude of the oscillating waveform. Hence, to obtain a measure of jitter, $\mathrm{S}_{\mathrm{v}}(\mathrm{f})$ may be normalized with respect to the total power in the signal, which for a sinusoid is $A^{2} / 2$. Shifting the resulting spectrum down to dc gives the following alternative spectral representation of jitter:

$$
\begin{equation*}
\mathcal{L}(\Delta f)=\frac{\mathrm{S}_{\mathrm{v}}\left(\frac{1}{\mathrm{~T}_{0}}+\Delta \mathrm{f}\right)}{\mathrm{A}^{2} / 2} \tag{19.75}
\end{equation*}
$$

image_name:The units of L(Δf) are Hz^-1
description:The image contains a mathematical statement about the units of \( \mathcal{L}(\Delta f) \). It states that the units are \( \text{Hz}^{-1} \), but it is more common to plot its logarithm \( 10\log_{10}(\mathcal{L}(\Delta f)) \) in units of dBc/Hz. This indicates a preference for using a logarithmic scale when representing the spectrum, which is typical in signal processing to better visualize variations over a wide range of values. The term dBc/Hz refers to decibels relative to the carrier per Hertz, a common unit in spectral density measurements.
the "c" denotes that $\mathcal{L}(\Delta f)$ has been normalized with respect to the total power in the "carrier." The argument $\Delta f$ is called the offset frequency since $\mathcal{L}(\Delta f)$ represents the signal spectrum at a frequency offset from the carrier by $\Delta \mathrm{f} \mathrm{Hz}$.

Strictly speaking, the relationship between $\mathcal{L}(\Delta \mathrm{f})$ and $\mathrm{S}_{\phi}(\mathrm{f})$ is very complex but the following simple approximation may be applied to spectral components where $S_{\phi}(f)$ is very small. ${ }^{15}$

$$
\begin{equation*}
\mathcal{L}(\Delta f) \approx \frac{S_{\phi}(\Delta f)}{2}, \quad S_{\phi}(\Delta f) \ll 1 \tag{19.76}
\end{equation*}
$$

The factor of two in (19.76) arises because the definition of $\mathcal{L}(\Delta f)$ in (19.75) ignores one of the sidebands of $\mathrm{S}_{\mathrm{v}}(\mathrm{f})$. We shall see that practical oscillators always have very large phase noise at small offset frequencies, as suggested by Fig. 19.15. Hence, (19.76) is only applied to large offset frequencies where it becomes a reasonable approximation. Combining (19.75) and (19.76) allows one to estimate the phase noise of a signal by looking only at its spectrum. Because of this equality, phase noise plots of $S_{\phi}(f)$ are often also shown logarithmically with units labelled $\mathrm{dBc} / \mathrm{Hz}$, although its units are more accurately written $10 \log _{10}\left(\mathrm{rad}^{2} / \mathrm{Hz}\right)$.

[^8]
### 19.3.5 Probability Density Function of Jitter

When designing a digital system the critical path must have a delay shorter than the smallest possible clock period. Hence, the probability density function (PDF) of $\tau_{\mathrm{k}}$ and its derivatives are also important measures of clock purity. Note that spectral representations of jitter can not generally be used to estimate the $\operatorname{PDF}$ of $\tau_{\mathrm{k}}$.

#### EXAMPLE 19.14

Find the PDF of $\tau_{\mathrm{k}}$ for a sinusoid with amplitude A and angular frequency $\omega_{0}$ in additive white gaussian noise, $n(t)$, with variance $\sigma_{n}^{2}$.

#### Solution

The sinusoid may be described as:

$$
\begin{equation*}
v(t)=A \sin \left(\omega_{0} t\right)+n(t) \tag{19.77}
\end{equation*}
$$

As in Example 19.9, assuming the noise n is much smaller than the amplitude of oscillation, $\sigma_{\mathrm{n}}$ « A , the absolute jitter is linearly related to $\mathrm{n}_{\mathrm{k}}$ by the slope of the sinusoid around its zero crossings.

$$
\tau_{\mathrm{k}} \cong \frac{\mathrm{n}_{\mathrm{k}}}{\mathrm{~A} \omega_{0}}
$$

Since $\mathrm{n}_{\mathrm{k}}$ is gaussian-distributed, absolute jitter is also gaussian-distributed with the following PDF:

$$
\begin{equation*}
f_{\tau}(t)=\frac{1}{\sigma_{\tau} \sqrt{2 \pi}} \exp \left(\frac{t^{2}}{2 \sigma_{\tau}^{2}}\right) \tag{19.78}
\end{equation*}
$$

where $\sigma_{\tau}$ is given by (19.57).

If the absolute jitter $\tau_{\mathrm{k}}$ has a Gaussian distribution, the period jitter, P-cycle jitter, and adjacent period jitter are all also Gaussian-distributed since they are linear derivatives of $\tau_{\mathrm{k}}$ given by (19.63), (19.65) and (19.67).

#### EXAMPLE 19.15

It is desired to drive a digital system with a clock period that is always at least 1 ns . The clock has a nominal period $\mathrm{T}_{0}=1.1 \mathrm{~ns}$ and a gaussian jitter distribution. If the rms period jitter is 5 ps , with what probability will any particular clock period be less than 1 ns ?

#### Solution

The clock period will be less than 1 ns whenever the period jitter $J_{k}<-0.1 \mathrm{~ns}$. The PDF of $J_{k}$ is,

$$
f_{J}(t)=\frac{1}{\left(5 \cdot 10^{-12}\right) \sqrt{2 \pi}} \exp \left(-\frac{t^{2}}{5 \cdot 10^{-25}}\right)
$$

image_name:(a)
description:The graph labeled "(a)" depicts a Gaussian distribution, which is a common representation of random noise-induced jitter in clock signals.

1. **Type of Graph and Function:**
- This is a probability density function (PDF) graph, specifically illustrating a Gaussian (normal) distribution.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as "t," representing time, though specific units are not marked, it is implied to be in seconds or a subunit like picoseconds (ps) given the context.
- The vertical axis is labeled as "f(t)," indicating the probability density function value at time "t."
- The scale appears to be linear.

3. **Overall Behavior and Trends:**
- The graph shows a symmetrical bell-shaped curve centered around the mean value, which is typical for Gaussian distributions.
- The curve rises smoothly to a peak at the center and then symmetrically falls off on both sides, indicating the highest probability density at the mean and decreasing probability density as you move away from the center.

4. **Key Features and Technical Details:**
- The peak of the curve represents the mean of the distribution, where the jitter is most likely to occur.
- The width of the curve is determined by the standard deviation, which in this context is 5 ps, indicating how much the periods vary around the mean.
- The tails of the curve extend towards infinity in both directions, although they approach zero, representing the decreasing probability of extreme jitter values.

5. **Annotations and Specific Data Points:**
- There are no specific annotations or markers on the graph, but the mean and standard deviation are critical parameters for understanding the distribution.
- The context provides that we are interested in the area under the curve to the left of -100 ps, which corresponds to the probability of the clock period being less than 1 ns.
image_name:(b)
description:The graph labeled (b) represents a sinusoidal jitter distribution. This type of graph is typically used to illustrate how a system's timing can vary due to sinusoidal influences, which is a common scenario in clock signal analysis.

1. **Type of Graph and Function:**
- This is a probability density function (PDF) graph showing a sinusoidal jitter distribution.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as "t," representing time. The scale is linear.
- The vertical axis is labeled as "f(t)," representing the probability density function.

3. **Overall Behavior and Trends:**
- The graph has a distinctive U-shape, indicating a sinusoidal distribution. It begins at a high value on the left, decreases to a minimum at the center, and then increases again symmetrically on the right.
- This shape suggests that the probability density is lower at the mean value and higher at the extremes, which is typical for sinusoidal distributions.

4. **Key Features and Technical Details:**
- The graph is symmetric about the vertical axis, indicating that the jitter is equally likely to be positive or negative.
- The central point, where the graph reaches its minimum, represents the mean of the distribution.
- The peaks at both ends suggest that the jitter has significant components at these extremes.

5. **Annotations and Specific Data Points:**
- There are no specific numerical data points or annotations provided in the graph. However, the shape itself is indicative of the nature of the sinusoidal jitter.

This sinusoidal distribution can be used to model situations where the jitter is influenced by periodic or cyclic factors, affecting the timing of clock signals in a predictable manner.

Fig. 19.16 Jitter PDFs: (a) Gaussian distribution; (b) sinusoidal jitter distribution.

Hence, the probability that the clock period is less than 1 ns is given by the integral of $f_{J}(t)$ over the range $-\infty$ to -100 ps.

$$
\int_{-\infty}^{-10^{-10} \mathrm{~s}} \mathrm{f}_{\mathrm{J}}(\mathrm{t}) \cdot \mathrm{dt}=2.75 \cdot 10^{-89}
$$

Gaussian distributions are common when jitter arises due to random noise. This is because noise processes are generally the superposition of many independent noise events, hence the law of large numbers tends to give the resulting jitter an approximately gaussian distribution. However, other jitter distributions arise when outside interference is a major contributor. For example, Fig. 19.16 compares a gaussian jitter distribution to the jitter PDF observed in the presence of sinusoidal phase modulation. In practice, local variations in supply voltage, digital data patterns, and electromagnetic interference from neighboring signals are often superimposed on random circuit noise to produce a complex PDF. Measurement equipment may then be able to decompose the observed jitter PDF into its constituent parts providing clues to the underlying sources of jitter.

## 19.4 ELECTRONIC OSCILLATORS

In this section, the basics of electronic oscillators are presented. Oscillators come in a variety of different types, but the two major classifications are those that directly create sinusoidal outputs as opposed to those with square (or triangular) wave outputs. Sinusoidal-output oscillators are usually realized using some kind of frequencyselective or tuned circuit in a feedback configuration, whereas square-wave-output oscillators are usually realized using a nonlinear feedback circuit such as a relaxation oscillator or a ring counter. Sinusoidal oscillators realized using tuned circuits can be further classified into RC circuits, switched-capacitor circuits, LC circuits, and crystal oscillators. A table showing the classification of oscillators is shown in Fig. 19.17.

The two most common oscillators implemented on integrated circuits are ring oscillators and LC oscillators. Unless precise off-chip components are included in the oscillator circuits, their frequency of operation is poorlycontrolled in the presence of process, temperature, and supply voltage variations. Hence, integrated circuit oscillators are nearly always designed with a mechanism for tuning their operating frequency. The actuator used for tuning is generally the voltage at some node in the oscillator circuit, so these circuits are called voltage-controlled oscillators (VCOs).
image_name:Fig. 19.17 Classification of oscillators
description:The system block diagram titled "Fig. 19.17 Classification of oscillators" provides a hierarchical overview and a specific example of oscillators used in electronic circuits.

Main Components:
1. **Classification Tree:**
- The diagram begins with a high-level classification of oscillators into two main categories: **Tuned oscillators** and **Nonlinear oscillators**.
- **Tuned oscillators** are further divided into four types: **RC oscillators, SC oscillators, LC oscillators,** and **Crystal oscillators**.
- **Nonlinear oscillators** include **Relaxation oscillators** and **Ring oscillators**.

2. **Ring Oscillator Example:**
- The lower part of the diagram provides a detailed schematic of a **Ring Oscillator** with five stages.
- It consists of five inverting amplifiers (or inverters) connected in a loop, denoted by **V1, V2, V3, V4,** and **V5**.

Flow of Information or Control:
- The signal flow begins at **V1**, passes through each inverter **V2, V3, V4, V5**, and loops back to the start at **V1**.
- Each inverter introduces a phase shift, and the cumulative phase shift around the loop is a multiple of 360 degrees, which is necessary for oscillation.
- The propagation delay through each inverter is denoted by **T_d**, and the total delay through all inverters is **nT_d**, where **n** is the number of inverters.

Labels, Annotations, and Key Indicators:
- The waveform diagrams below the inverter schematic illustrate the phase relationships and time delays between the signals at each stage (**V1** to **V5**).
- **T_d** represents the time delay introduced by each inverter, and **nT_d** is the total delay for the signal to complete one loop.

Overall System Function:
- The primary function of the diagram is to classify different types of oscillators and illustrate the working principle of a ring oscillator.
- In a ring oscillator, the oscillation frequency is determined by the number of stages (inverters) and the delay of each stage. This type of oscillator is often used in integrated circuits due to its simplicity and ease of integration.
image_name:Fig. 19.18 Ring oscillator with n=5
description:The circuit is a 5-stage ring oscillator, which is a type of nonlinear oscillator. It consists of five inverters connected in a loop. The output of each inverter serves as the input to the next, and the last inverter feeds back to the first. The waveform diagrams show the phase shift and propagation delay across each stage, contributing to the oscillation frequency.
image_name:Fig. 19.18 Ring oscillator with n=5
description:The diagram illustrates a ring oscillator circuit and its corresponding waveform outputs. It is divided into two main sections: a classification chart of oscillators and a schematic representation of a ring oscillator with its waveforms.

1. **Classification of Oscillators:**
- The top part of the diagram presents a classification tree of oscillators. Oscillators are divided into two categories: Tuned Oscillators and Nonlinear Oscillators.
- Under Tuned Oscillators, the types include RC (Resistor-Capacitor) oscillators, SC (Switched Capacitor) oscillators, LC (Inductor-Capacitor) oscillators, and Crystal oscillators.
- Nonlinear Oscillators are further divided into Relaxation oscillators and Ring oscillators.

2. **Ring Oscillator Schematic:**
- The middle section shows a schematic of a ring oscillator consisting of five inverting amplifiers connected in a feedback loop. Each amplifier is represented as a triangle with a circle at its output, indicating the signal flow from one stage to the next.
- The inverters are labeled from $V_1$ to $V_5$, with $V_1$ being the input and also the output after the feedback loop.

3. **Waveform Outputs:**
- The bottom section displays the waveforms at each node ($V_1$ to $V_5$) of the ring oscillator. These waveforms are periodic and demonstrate the propagation of a square wave through the inverter stages.
- The waveform at $V_1$ shows a complete period labeled as $nT_d$, representing the total delay through all stages.
- The waveform at $V_2$ is delayed by $T_d$ compared to $V_1$, indicating the time delay introduced by each inverter.
- This delay continues through $V_3$, $V_4$, and $V_5$, showing the cumulative effect of the inverters.

4. **Key Features and Technical Details:**
- The ring oscillator operates by having an odd number of inverting stages, which ensures a phase shift of 180 degrees plus an additional 180 degrees from the feedback loop, resulting in oscillation.
- The frequency of oscillation is determined by the number of stages and the delay per stage ($T_d$).
- The diagram emphasizes the periodic nature of the waveforms and the inherent delay in the propagation of the signal through the ring.

Overall, the diagram provides a comprehensive view of how a ring oscillator functions, from its classification among other oscillators to the specific details of its operation and waveform characteristics.
Fig. 19.18 Ring oscillator with $\mathrm{n}=5$.

### 19.4.1 Ring Oscillators

One of the most popular ways of realizing digital-output MOS VCOs is to use a ring oscillator and add voltage control to it. A ring oscillator is realized by placing an odd number of open-loop inverting amplifiers in a feedback loop. The simplest type of amplifier that can be used is a simple digital inverter, as shown in Fig. 19.18.
image_name:(a)
description:
[
name: (a), type: Inverter, ports: {In: V1, Out: V1}
]
extrainfo:The diagram shows a ring oscillator configuration with a single inverting amplifier connected in a feedback loop, forming a basic oscillator circuit.
image_name:(b)
description:
[
name: G_mV1, type: VoltageControlledCurrentSource, value: G_mV_1, ports: {Np: V1, Nn: GND}
name: R_o, type: Resistor, value: R_o, ports: {N1: V1, N2: GND}
name: C, type: Capacitor, value: C, ports: {Np: V1, Nn: GND}
]
extrainfo:The circuit diagram (b) represents a small-signal model with a voltage-controlled current source G_mV_1 connected to the node V1. The resistor R_o and capacitor C are also connected to the same node V1, with all components referenced to ground.
Fig. 19.19 (a) A single inverting amplifier, $\mathrm{n}=1$, with its input tied to its output. (b) A corresponding small-signal model.

Imagine that, at start-up, some voltage in the circuit transitions from a low-voltage to a high-voltage state. Each half-period, the transition will propagate around the loop with an inversion. For example, assume the output of the first inverter changes to 1 . This change will propagate through all five inverters in a time of $T_{0} / 2$, at which time the output of the first inverter will change to 0 ; after an additional time of $\mathrm{T}_{0} / 2$, the first inverter's output will change back to 1 , and so on. Assuming each inverter has a delay of $T_{d}$ and that there are n inverters, the halfperiod of oscillation is

$$
\begin{equation*}
\frac{\mathrm{T}_{0}}{2}=\mathrm{n} \mathrm{~T}_{\mathrm{d}} \tag{19.79}
\end{equation*}
$$

Thus,

$$
\begin{equation*}
\mathrm{f}_{0}=\frac{1}{\mathrm{~T}_{0}}=\frac{1}{2 \mathrm{nT} \mathrm{~T}_{\mathrm{d}}} \tag{19.80}
\end{equation*}
$$

Fig. 19.18 illustrates the case $\mathrm{n}=5$. By making the delay of the inverters voltage controlled, a VCO can be realized.

#### EXAMPLE 19.16

What is the behavior of a ring with only $\mathrm{n}=1$ inverter, as shown in Fig. 19.19(a)?

#### Solution

Based upon (19.80) and the preceding discussion, one might think that the circuit will oscillate at a frequency $\mathrm{f}_{0}=1 /\left(2 \mathrm{~T}_{\mathrm{d}}\right)$. But the first-order small-signal model of an inverting amplifier in Fig. 19.19(b) is clearly an undriven single-time constant circuit whose solution is an exponential decay,

$$
v_{1}(t)=v_{1}(0) \exp \left(-\frac{t}{R_{01} C_{1}}\right)
$$

When the inverting amplifier is a simple digital CMOS inverter, this analysis is accurate and there are no oscillations, as one may readily verify in the lab. The voltage quickly settles to a dc value between ground and the supply. In fact, this can be a useful bias circuit for establishing a dc voltage precisely equal to the trip point of the inverter, where $\mathrm{v}_{\text {out }}=\mathrm{v}_{\text {in }}$.

If the inverting amplifier has other internal nodes not represented by the small-signal schematic in Fig. 19.19(b), it will have a higher-order response and the solution is more complex.

Fig. 19.20 The two stable states of a CMOS latch, $\mathrm{n}=2$.
image_name:Fig. 19.20
description:
[
name: Inverter1, type: Inverter, ports: {In: 1, Out: 0}
name: Inverter2, type: Inverter, ports: {In: 0, Out: 1}
]
extrainfo:The circuit diagram represents two stable states of a CMOS latch. Each state consists of two inverters connected in a feedback loop.

Example 19.16 illustrates a shortcoming of the simple time-domain interpretation of ring oscillators illustrated in Fig. 19.18. A ring oscillator is actually a feedback circuit, and in order for it to exhibit oscillations it should be unstable.

Applying the first-order model of the inverting amplifier in Fig. 19.19(b) to a general ring oscillator with n identical stages, the loop gain can be found by breaking the loop at any point:

$$
\begin{equation*}
L(s)=\left(\frac{G_{m} R_{o}}{1+s R_{0} C}\right)^{n} \tag{19.81}
\end{equation*}
$$

Assuming $G_{m} R_{o}$ » 1 , each inverter has approximately $90^{\circ}$ phase shift at its unity-gain frequency. Hence, as long as there are 3 or more inverters, it is guaranteed that the loop gain will still be greater than unity when the phase shift around the loop becomes greater than $180^{\circ}$. But, with $\mathrm{n}=1$ there is only $90^{\circ}$ phase shift at the loop's unitygain frequency so the system is stable.

#### EXAMPLE 19.17

What is the behavior of a ring of inverters with $\mathrm{n}=2$ ?

#### Solution

It is a bistable circuit meaning it has two stable operating points as shown in Fig. 19.20. This is desirable behavior when used as a basic digital latch. No other operating points are stable, so immediately upon startup the circuit will settle into one of these two states and rest there until forced into some other state. The circuit will not oscillate.

Positive-feedback loops as in Example 19.17 are also unstable but do not oscillate. They can be thought of as negative feedback loops with an additional $180^{\circ}$ phase shift at dc. Hence, the node voltages simply diverge exponentially until the stages are saturated resulting in a latch-up of the ring. Therefore, if single-ended inverting amplifiers are used, it is required that n is odd.

In many integrated ring oscillators, fully differential inverters are used to obtain better power-supply insensitivity. When this is done, an even number of inverters can be used and the inversion required around the loop can be achieved by simply interchanging the outputs of the last inverter before feeding them back to the input, as shown in Fig. 19.21. This has a very important advantage: the outputs of the middle inverters will have a quadrature phase relationship compared with the last inverters (assuming all inverters and their loads are carefully matched) [Buchwald, 1991]. These quadrature outputs are very useful in many communication applications such as quadrature modulators and some clock-extraction circuits.

An example of realizing a fully differential inverter with a programmable delay is shown in Fig. 19.22, where the current-source loads are made voltage programmable. Assuming the current-source loads are proportional to $\mathrm{V}_{\mathrm{cnt1}}$ with a constant of proportionality of $\mathrm{K}_{\text {bias }}$, we have
image_name:Fig. 19.21
description:**Main Components:**
- **Differential Inverters:** The diagram in Fig. 19.21 consists of a series of three fully differential inverters connected in a loop configuration. Each inverter is represented with a differential input and output, marked with plus (+) and minus (-) signs.
- **Output Nodes:** There are two outputs labeled as \( V_{out} \) and \( V_{out} \) (quadrature), indicating that the system provides both direct and quadrature outputs.

**Flow of Information or Control:**
- **Signal Flow:** The signal flows sequentially through the series of inverters, forming a closed-loop ring oscillator. The output of each inverter feeds into the next, and the last inverter's output loops back to the first, completing the ring.
- **Quadrature Output:** The system provides a quadrature output, which is typically 90 degrees out of phase with the main output, useful in communication applications for modulation and demodulation.

**Labels, Annotations, and Key Indicators:**
- **Annotations:** The diagram includes labels indicating the differential nature of the inputs and outputs, as well as the quadrature output.
- **Reference Points:** The figure is labeled as Fig. 19.21, with a description noting the use of fully differential inverters for improved power-supply rejection.

**Overall System Function:**
- **Ring Oscillator Function:** The primary function of this system is to act as a ring oscillator. The differential inverters create a feedback loop that generates oscillations. The fully differential design helps improve power-supply rejection, making the system more robust in varying power conditions.
- **Applications:** This setup is particularly useful in applications requiring quadrature signals, such as in quadrature modulators and clock-extraction circuits. The differential nature of the design enhances signal integrity and reduces noise susceptibility.
image_name:Fig. 19.22
description:The circuit is a fully differential inverter with programmable delay, using PMOS transistors and current sources to control the delay. It is designed to improve power-supply rejection. The CMFB circuitry is not shown.

Fig. 19.22 A fully differential inverter with a programmable delay. CMFB circuitry not shown.

$$
\begin{equation*}
\mathrm{I}_{\mathrm{B}}=\mathrm{K}_{\mathrm{bias}} \mathrm{~V}_{\mathrm{cnt1}} \tag{19.82}
\end{equation*}
$$

The delay of each inverter is proportional to the unity-gain frequency of that inverter. In other words,

$$
\begin{equation*}
\tau_{\text {inv }} \propto \frac{C_{L}}{g_{m}} \tag{19.83}
\end{equation*}
$$

where $C_{L}$ is the load capacitance of the inverter and $g_{m}$ is the transconductance of the drive transistors of the inverter. Since $\mathrm{g}_{\mathrm{m}} \propto \sqrt{\mathrm{I}_{\mathrm{B}}}$, we know that the delay is proportional to $1 / \sqrt{\mathrm{I}_{\mathrm{B}}} \propto 1 / \sqrt{\mathrm{V}_{\mathrm{cnt1}}}$ and therefore, $\mathrm{f}_{\text {osc }} \propto \sqrt{\mathrm{V}_{\text {cntl }}}$. Thus, the relationship between the oscillation frequency and the control voltage is not very linear. In a PLL, this nonlinearity implies that $\mathrm{K}_{\text {osc }}$ is a function of $\mathrm{f}_{\text {osc }}$ and, therefore, so is the loop bandwidth and settling time. The major reason for this nonlinearity is that at higher frequencies, the voltage changes at the outputs of each stage increase in amplitude because $I_{B}$ increases.

It is possible to realize a ring-oscillator VCO with good voltage-to-frequency linearity if one ensures that the voltage changes of the delay elements are independent of the oscillation frequency [Kim, 1990; Young, 1992; Reynolds, 1994]. A differential delay stage where this linearization has been realized is shown in Fig. 19.23 [Young, 1992], along with the biasing circuitry that is used to control the voltage swings. Each stage consists of a differential amplifier with p -channel input resistors and resistive loads. The resistive loads realized using n -channel transistors biased in the triode region. Their resistance is adjusted by the bias circuit so that when all of $I_{b}$ is flowing through them, they will have $\mathrm{V}_{\text {ref }}$ across them, where $\mathrm{V}_{\text {ref }}$ is obtained from a temperature-independent voltage reference. This is achieved by using a replica of the delay cell in the bias circuit. The replica consists of $Q_{3}, Q_{4}, R_{3}$, and $R_{4}$. In the replica, all of $I_{b}$ flows through $Q_{3}$ and $R_{3}$, so $Q_{4}$ and $R_{4}$ could have been eliminated from the circuit-they have been included in the figure for clarity only. Recalling that $R_{3}$ is actually realized by an n-channel transistor, it is seen that the negative feedback loop including the opamp will cause the voltage across $R_{3}$ to be equal to $V_{\text {ref }}$ when $I_{b}$ is going through it. Since the output of the opamp is also used to control the resistance of all the triode-region resistances used for the delay cells of the ring oscillator, they will also have
image_name:Fig. 19.23 A differential delay cell having resistive loads consisting of n-channel transistors.
description:The circuit is a differential delay cell with resistive loads consisting of n-channel transistors. It includes a bias stage and a delay stage, with feedback control to maintain Vref across R3. The opamp A1 helps in maintaining the reference voltage across the bias stage.

Fig. 19.23 A differential delay cell having resistive loads consisting of $n$-channel transistors.
image_name:V_out (quadrature)
description:The circuit is a quadrature voltage output configuration using four operational amplifiers connected in series. The outputs are connected to two voltage sources labeled as Vout (quadrature) and Vout, which are likely used to provide phase-shifted outputs for applications like oscillators or signal processing.

Fig. 19.24 Modifying the ring oscillator of Fig. 19.21 to achieve a doubling of frequency.
$V_{\text {ref }}$ across them when $I_{b}$ flows through them. Next, if the VCO frequency changes because of a change in $V_{\text {cnt }}$, and therefore in $I_{b}$, the bias loop will change the resistance of the delay-stage loads so the maximum voltages across them will still equal $\mathrm{V}_{\text {ref }}$. Assuming the capacitive loads of each stage are constant (a good assumption), the delay of each stage will be inversely proportional to $I_{b}$. This makes the frequency of oscillation proportional to $I_{b}$. In an interesting modification of the ring oscillator of Fig. 19.21, two multipliers have been added in Fig. 19.24. This modification achieves a doubling in the output frequency while still realizing two quadrature outputs [Buchwald, 1992]. Indeed, if quadrature outputs are not required, it is possible to connect the two multiplier outputs to an additional third multiplier. This achieves another doubling of frequency, but there is now only a single output. Another interesting variation of a ring oscillator is described in [Razavi, 1994], where the outputs of
image_name:(a)
description:This is a CMOS LC-oscillator circuit with two NMOS transistors forming a cross-coupled pair. Inductors and capacitors create a resonant tank circuit. The circuit is designed to provide oscillations with a frequency determined by the LC components.
image_name:(b)
description:
[
name: g_m·(-V1), type: VoltageControlledCurrentSource, ports: {Np: V1, Nn: GND}
name: R_o, type: Resistor, value: R_o, ports: {N1: V1, N2: GND}
name: L, type: Inductor, value: L, ports: {N1: V1, N2: GND}
name: C, type: Capacitor, value: C, ports: {Np: V1, Nn: GND}
]
extrainfo:This is a differential small-signal half-circuit of a CMOS LC-oscillator. It includes a voltage-controlled current source, a resistor, an inductor, and a capacitor connected to ground, forming a resonant circuit.

Fig. 19.25 (a) A simple CMOS LC-oscillator and (b) its differential small-signal half-circuit.
a three-stage oscillator are combined in a novel manner to obtain a single output with a period equal to only two inverter delays.

### 19.4.2 LC Oscillators

LC oscillators are an example of tuned oscillators. Whereas ring oscillators use active amplifier stages to provide the $180^{\circ}$ phase shift required for loop instability, tuned oscillators insert a tuned (resonant) circuit into a feedback loop to provide the phase shift. In the case of an LC oscillator, the resonance is provided by a parallel LC combination.

A simple LC oscillator is shown in Fig. 19.25(a) and its small-signal differential half-circuit is in Fig. 19.25(b) where $\mathrm{R}_{0}$ models the output resistance of the transistors as well as any losses associated with the inductor and/or capacitor. Note the similarity with the one-stage ring shown in Fig. 19.19(b). The parallel RC network in the one-stage ring provides only $90^{\circ}$ phase shift making it stable; the second-order resonant LC tank in Fig. 19.25 provides the additional phase shift required for oscillation. The inductors provide a dc bias voltage to the transistor gates and drains ensuring they are in saturation. The frequency of oscillation is the resonant frequency of the tank.

$$
\begin{equation*}
f_{0}=\frac{1}{2 \pi \sqrt{L C}} \tag{19.84}
\end{equation*}
$$

At resonance, the LC tank has infinite impedance. At that single frequency, the circuit reduces to only $R_{0}$ in parallel with the transconductor, equivalent to $\left(R_{0} \|-1 / g_{m}\right)$. If the negative resistance is larger than $R_{0}$, upon startup the amplitude of oscillations at $f_{0}$ increases exponentially. If, however, the resistance $R_{0}$ is larger than $\left(1 / g_{m}\right)$ the response decays and the circuit will not oscillate. Hence, to ensure oscillation, the transistors are sized and biased to ensure

$$
\begin{equation*}
\mathrm{g}_{\mathrm{m}}>\frac{1}{\mathrm{R}_{0}} \tag{19.85}
\end{equation*}
$$

This small-signal analysis is applicable at startup and is therefore useful in finding conditions for oscillation, but the large swings present after oscillations start render it inaccurate (as it predicts the oscillation amplitude grows without bound).

The implementation of the passive tank circuit is critical to the design of an integrated LC oscillator. The capacitors will generally be a combination of parasitic capacitances, varactors to enable tuning of $\mathrm{f}_{0}$, and perhaps
image_name:(a)
description:The image consists of two parts labeled (a) and (b), representing different aspects of a planar integrated inductor fabricated on an integrated circuit.

1. **Identification of Components and Structure:**
- **Part (a):** This shows a 3D representation of a planar integrated inductor on a silicon (Si) substrate. The inductor is formed by laying spiral metal traces above the silicon substrate. These traces are typically made from the metal used for interconnecting transistors in integrated circuits. The spiral design helps in achieving the inductance required for the circuit.
- **Part (b):** This is a schematic representation of the inductor's equivalent circuit. It includes an inductor (L) with a series resistance (R_s) and parasitic capacitances to ground (C_p1 and C_p2).

2. **Connections and Interactions:**
- **Part (a):** The spiral metal trace is shown as a continuous line that forms the inductor. The trace is connected to the silicon substrate, which acts as a ground plane, through parasitic capacitances.
- **Part (b):** The schematic shows the inductor (L) connected in series with a resistor (R_s), representing the series resistance of the metal trace. The parasitic capacitances (C_p1 and C_p2) are connected from the input (V1) and output (V2) nodes to ground, indicating how the inductor interacts with the silicon substrate and other components in the circuit.

3. **Labels, Annotations, and Key Features:**
- The silicon substrate is labeled in part (a), indicating the base material for the integrated circuit.
- In part (b), the components are labeled with standard electrical symbols and notations, including the inductor (L), series resistance (R_s), and parasitic capacitances (C_p1 and C_p2). The ground connections are marked as 'GND'.
- The input and output nodes are labeled as V1 and V2, respectively, showing the points of connection for the inductor within a larger circuit.

Overall, the image provides a comprehensive view of both the physical layout and electrical characteristics of a planar integrated inductor used in integrated circuits.
image_name:(b)
description:
[
name: L, type: Inductor, value: LR, ports: {N1: V1, N2: l_r}
name: RS, type: Resistor, ports: {N1: V2, N2: l_r}
name: Cp1, type: Capacitor, ports: {Np: V1, Nn: GND}
name: Cp2, type: Capacitor, ports: {Np: V2, Nn: GND}
]
extrainfo:The circuit is an LC tank circuit with parasitic capacitances Cp1 and Cp2 connected to ground. The inductor L has a series resistance Rs, forming an RLC circuit.

Fig. 19.26 (a) A planar integrated inductor may be fabricated on an integrated circuit using the metal intended to interconnect transistors by laying spiral traces above the silicon substrate. (b) Its series resistance, $R_{s}$, and parasitic capacitances to ground, $C_{p 1}$ and $C_{p 2}$, should be included in any circuit simulations involving the inductor.
metal-metal capacitors in series with switches for coarse tuning of $\mathrm{f}_{0}$. CMOS inductors are formed with spirals of the metal used for interconnect, as pictured in Fig. 19.26(a). They are restricted to inductance values of up to a few nH for a spiral several hundred $\mu \mathrm{m}$ per side-considerably smaller than what is possible with discrete inductors due to their smaller physical size and the constraints of modern CMOS fabrication process which preclude the use of magnetic cores. Electrically, inductors behave similar to the model in Fig. 19.26(b). In addition to the desired inductance, $L$, parasitic capacitances to ground and resistive losses must be considered.

Several considerations may influence the designer's choice of whether to use a ring or LC oscillator. The operating frequency of a ring oscillator depends upon the frequency response of the loop (19.81). As a result, it may be tuned over a very wide range of frequencies, up to a decade or more, by changing the biasing of the transistors. By contrast, a LC oscillator's resonant frequency (19.84) can only be influenced by changing the value of the passive components in the tank making it difficult to realize a tuning range of 2:1 or more. However, the insensitivity of an LC oscillator to changes in transistor biasing also means that its oscillations will be more stable (hence, have less jitter) in the presence of temperature and supply voltage variations than those of a ring oscillator. At frequencies within roughly a decade of the maximum $f_{T}$ of the MOS devices, the power consumption of a ring oscillator can become very high since the individual stages in the ring are required to operate with very high bandwidth. Hence, LC oscillators are generally preferred a frequencies approaching the speed limits of a given CMOS technology. However, at low frequencies the required value of the passive inductor is relatively large so the metal spiral requires a large footprint. As a result, LC-oscillators tend to be larger in circuit area than ring oscillators, a fact which almost completely precludes their use around 1-GHz and below. Finally, ring oscillators generally start oscillating more quickly upon power-up than their LC counterparts. In summary, LC oscillators are preferred when high operating frequency or high spectral purity are required; otherwise ring oscillators offer advantages in area and tuning range.

### 19.4.3 Phase Noise of Oscillators

Phase noise in oscillators is a fundamental fact of life. Since a lossless oscillator does not exist (that would imply perpetual motion), every oscillator requires some active circuitry to sustain the oscillations and the active circuitry must introduce noise. The specific mechanisms by which device noise becomes phase noise can be subtle and are only recently becoming well understood. However, the phenomenological facts of phase noise are well established, and are sufficient to permit a basic understanding and design of integrated circuit oscillators and PLLs.
image_name:(a)
description:The graph labeled "(a)" depicts the pole-zero plot of a closed-loop amplifier system in the complex plane. This type of graph is used to analyze the stability and frequency response of control systems.

1. **Type of Graph and Function:**
- This is a pole-zero plot in the complex plane, typically used in control theory and signal processing to assess system stability.

2. **Axes Labels and Units:**
- The horizontal axis represents the real part of the complex frequency, while the vertical axis represents the imaginary part. Units are typically in radians per second.

3. **Overall Behavior and Trends:**
- The plot shows two poles marked as '×' in the right-half plane. This indicates an unstable system, as poles in the right-half plane lead to exponentially increasing oscillations over time.

4. **Key Features and Technical Details:**
- The presence of poles in the right-half plane suggests that the system will have oscillations with amplitudes that increase exponentially, leading to system instability unless corrective measures are taken.
- These poles are critical as they determine the system's response to inputs, and their location in the right-half plane is indicative of an unstable feedback loop.

5. **Annotations and Specific Data Points:**
- There are no specific numerical values or additional annotations provided in the plot, but the key takeaway is the position of the poles which is crucial for understanding the system's tendency to oscillate unstably.
image_name:(b)
description:The graph labeled (b) represents a pole-zero plot on the complex plane, which is used to analyze the stability of a closed-loop amplifier. This specific plot shows poles that have moved from the right-half plane to the real axis, indicating a stabilization of the system.

1. **Type of Graph and Function:**
- This is a pole-zero plot, a common tool in control systems and signal processing to represent the roots of the characteristic equation of a system.

2. **Axes Labels and Units:**
- The horizontal axis represents the real part of the complex frequency, while the vertical axis represents the imaginary part.
- Units are typically in radians per second, but specific units are not labeled on this plot.

3. **Overall Behavior and Trends:**
- Initially, the poles are located in the right-half plane, which is indicative of an unstable system with oscillations that have exponentially increasing amplitude.
- As the system stabilizes, the poles move towards the real axis, suggesting that the oscillation amplitude saturates and the loop gain is reduced.

4. **Key Features and Technical Details:**
- The movement of poles from the right-half plane to the real axis is crucial as it signifies the transition from instability to stability.
- This movement is often associated with nonlinear effects or saturation in the system, which reduces the effective loop gain.

5. **Annotations and Specific Data Points:**
- The plot does not include specific numerical values or annotations beyond the symbolic representation of poles and their movement.
- The movement of poles is shown with arrows, indicating the direction of stabilization.
image_name:(c)
description:The graph labeled '(c)' is a frequency response graph that depicts the magnitude of the transfer function \(|G(j2\pi f)|\) as a function of frequency \(f\). This graph is likely a part of a Bode plot or a similar frequency response analysis.

1. **Type of Graph and Function:**
- The graph is a frequency response plot showing the magnitude of a transfer function.

2. **Axes Labels and Units:**
- The horizontal axis represents frequency \(f\), with a specific emphasis on the frequency \(f_0\). The axis seems to use a linear scale but has a break indicating a focus on a specific frequency range.
- The vertical axis represents the magnitude \(|G(j2\pi f)|\) of the transfer function.

3. **Overall Behavior and Trends:**
- The graph shows a sharp peak at the frequency \(f_0\). This peak indicates a resonant frequency where the system exhibits maximum response.
- The graph's shape is symmetric around \(f_0\), suggesting a band-pass characteristic centered at this frequency.

4. **Key Features and Technical Details:**
- The peak at \(f_0\) suggests that this is a critical frequency where the system's gain is maximized.
- The sharpness of the peak indicates a narrow bandwidth, which is typical for systems with high selectivity at the resonant frequency.

5. **Annotations and Specific Data Points:**
- There is a break in the horizontal axis, indicating that the graph focuses on the vicinity of \(f_0\) and may not show the entire frequency range.
- The exact value of \(f_0\) is not specified, but it is marked as the central frequency of interest.
image_name:(d)
description:The graph labeled (d) is a Bode plot, specifically showing the magnitude response of a system. The x-axis represents the frequency deviation (Δf) from a central frequency (f₀) on a logarithmic scale, while the y-axis represents the magnitude |G(j2π(f₀ + Δf))|, also on a logarithmic scale, typically in decibels (dB).

Overall Behavior and Trends:
- The graph shows a linear decrease in magnitude with increasing frequency deviation.
- This decrease follows a slope of -20 dB per decade, indicating a first-order system behavior in this frequency range.

Key Features and Technical Details:
- The plot starts at a higher magnitude when Δf is small and decreases as Δf increases, following the linear trend.
- The slope of -20 dB/decade is a typical characteristic of a single-pole roll-off in frequency response.

Annotations and Specific Data Points:
- The slope of -20 dB/decade is explicitly marked on the graph, highlighting the rate of decrease in gain with frequency.
- No specific cutoff frequencies or resonance peaks are marked, but the consistent slope suggests a simple low-pass filter characteristic beyond a certain frequency range.

This graph is used to illustrate the behavior of an oscillator or amplifier system as it transitions from stable to oscillatory behavior, showing how the gain decreases with frequency deviation from the central frequency.
image_name:
description:The provided diagram consists of four sub-figures labeled (a), (b), (c), and (d), each illustrating different aspects of an unstable closed-loop amplifier's behavior and frequency response.

1. **Sub-figure (a):**
- **Type of Graph:** Pole-zero plot.
- **Axes Labels and Units:** The plot is on the complex plane with the horizontal axis representing the real part and the vertical axis representing the imaginary part of the poles.
- **Overall Behavior and Trends:** It shows poles located in the right-half plane, indicating instability and oscillatory behavior with exponentially increasing amplitude.
- **Key Features:** Two poles are marked on the right side, suggesting potential for oscillations.

2. **Sub-figure (b):**
- **Type of Graph:** Modified pole-zero plot.
- **Axes Labels and Units:** Similar to (a), on the complex plane.
- **Overall Behavior and Trends:** As the system stabilizes, the poles move to the imaginary axis, represented by the arrow pointing to the new pole position at \(j2\pi f_0\).
- **Key Features:** The poles now lie on the imaginary axis, indicating sustained oscillations at frequency \(f_0\).

3. **Sub-figure (c):**
- **Type of Graph:** Frequency response plot.
- **Axes Labels and Units:** The horizontal axis is frequency \(f\), and the vertical axis is the magnitude of the gain \(|G(j2\pi f)|\).
- **Overall Behavior and Trends:** The graph shows a peak at \(f_0\), indicating resonance at this frequency.
- **Key Features:** The plot features a resonance peak at \(f_0\), with a sharp rise and fall around this frequency, suggesting a high Q-factor.

4. **Sub-figure (d):**
- **Type of Graph:** Logarithmic frequency response plot.
- **Axes Labels and Units:** The horizontal axis is the frequency deviation \(\Delta f\), and the vertical axis is the magnitude of the gain \(|G(j2\pi(f_0 + \Delta f))|\).
- **Overall Behavior and Trends:** Shows a slope of -20 dB/decade, indicating how the gain decreases with increasing frequency deviation from \(f_0\).
- **Key Features:** The plot highlights the roll-off rate of the system's frequency response beyond the resonance peak.

5. **Additional Graph (Below):**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The horizontal axis is time \(t\), and the vertical axis is amplitude.
- **Overall Behavior and Trends:** Illustrates the oscillation behavior over time, with an initially increasing amplitude that eventually saturates.
- **Key Features:** The waveform shows exponential growth initially, followed by a constant amplitude oscillation, indicating a saturation effect that stabilizes the oscillations.

Fig. 19.27 Unstable poles of a closed-loop amplifier: (a) poles in the right-half plane give rise to oscillations with an exponentially increasing amplitude; (b) as the oscillation amplitude saturates, loop gain is reduced and the poles effectively move to the real axis; (c) the frequency response around the pole frequency; (d) on a logarithmic scale.

The phase noise of integrated circuit oscillators may be characterized as follows.

$$
\begin{equation*}
S_{\phi, \text { osc }}(f)=h_{0}+\frac{h_{2}}{f^{2}}+\frac{h_{3}}{f^{3}} \tag{19.86}
\end{equation*}
$$

Although a rigorous treatment to derive the three terms in (19.86) is very involved, their existence can be qualitatively understood by simple arguments. The small signal analysis of a ring or LC oscillator will generally reveal that it has poles in the right half plane, as in Fig. 19.27(a), so its impulse response is oscillation with an exponen-tially-growing envelope. The amplitude of these oscillations eventually saturates. Although saturation is a nonlinear phenomena, the result is similar to what occurs in a linear system with poles precisely on the imaginary axis as shown in Fig. 19.27(b): The oscillations are sustained with constant amplitude. The frequency response of such a linear model $G\left(j 2 \pi\left(f_{0}+\Delta f\right)\right)$ for small offset frequencies $\Delta f$ will be roughly constant except for the pole term.

$$
\begin{equation*}
\mathrm{G}\left(\mathrm{j} 2 \pi\left(\mathrm{f}_{0}+\Delta \mathrm{f}\right)\right)=\left(\frac{1}{1-\mathrm{j}\left(\mathrm{f}_{0}+\Delta \mathrm{f}\right) / \mathrm{j} \mathrm{f}_{0}}\right) \cdot(\ldots)=\left(\frac{-\mathrm{f}_{0}}{\Delta \mathrm{f}}\right) \cdot(\ldots) \tag{19.87}
\end{equation*}
$$

Noise sources within the oscillator are shaped by $\mid G\left(\left.j 2 \pi\left(f_{0}+\Delta f\right)\right|^{2}\right.$, which from (19.87) is proportional to $1 / \Delta f^{2}$. The discussion so far explains $1 / \Delta f^{2}$-shaping of noise sources in $\mathcal{L}(\Delta f)$, but in practice such shaping is also observed in the phase noise spectrum, as predicted by (19.76).
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: LOAD1, G: Vin+}
name: M2, type: NMOS, ports: {S: P, D: LOAD2, G: Vin-}
name: In, type: CurrentSource, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential pair with NMOS transistors M1 and M2, driven by a current source In. The gates of M1 and M2 receive differential input signals Vin+ and Vin-, respectively. The common source node is connected to ground.
image_name:(b)
description:The block diagram labeled "(b)" represents a system focusing on the up-conversion of noise sources in an oscillator circuit. Here’s a detailed breakdown of the diagram:

1. **Main Components:**
- **Mixer (Multiplier):** This block is represented by a circle with an 'X' inside, indicating its function to mix or multiply signals. It receives two inputs: one from the noise source and another from a sinusoidal signal.
- **Oscillator:** This block follows the mixer and is responsible for generating a periodic waveform. It is depicted as a rectangular block and is the primary component shaping the output signal.

2. **Flow of Information or Control:**
- **Inputs to the Mixer:** The mixer receives an input from a noise source denoted as \(i_n^2(f)\), which is indicative of noise power spectral density. Additionally, it receives a sinusoidal input from an unspecified source, likely representing the fundamental frequency of oscillation.
- **Mixer to Oscillator Connection:** The output of the mixer feeds directly into the oscillator block. This connection suggests that the mixed signal, which includes noise components, is used to modulate the oscillator.
- **Oscillator Output:** The oscillator outputs a signal \(S_{\phi}(f)\), representing the phase noise spectrum. This output is shaped by the characteristics of the oscillator, including its inherent noise shaping properties.

3. **Labels, Annotations, and Key Indicators:**
- **Noise Characteristics:** The diagram includes annotations showing noise characteristics such as \(1/f\) and \(1/f^3\), indicating the frequency dependence of the noise power spectral density and its impact on the phase noise spectrum.
- **Dashed Lines:** These may indicate feedback paths or additional signal paths influencing the oscillator's behavior, though their exact nature is not explicitly defined in the diagram.

4. **Overall System Function:**
- The primary function of this system is to demonstrate how noise sources within an oscillator are up-converted and shaped by the oscillator's response. The mixer combines noise with a periodic signal, and the oscillator processes this mixed signal to produce an output where the phase noise characteristics are dominant. The annotations of \(1/f\) and \(1/f^3\) suggest a focus on understanding how different noise components influence the oscillator's phase noise.

Fig. 19.28 Up-conversion of noise sources by switching in an oscillator.
image_name:Fig. 19.28
description:The system block diagram in Fig. 19.28 illustrates the process of noise up-conversion by switching in an oscillator circuit. The main components of this system include an oscillator labeled 'G', a mixer, and a summing node.

1. **Main Components:**
- **Oscillator (G):** This block represents the oscillator, which is responsible for generating a periodic signal. The oscillator's function is to process the incoming mixed signal and shape the noise characteristics in the output.
- **Mixer:** This component combines the periodic signal from the oscillator with noise components. It is depicted in the diagram with an 'X' symbol, indicating the mixing operation.
- **Summing Node:** This node is shown as a circle with a '+' sign, indicating that it adds the incoming signals to produce an output.

2. **Flow of Information or Control:**
- **White Noise Input:** White noise is introduced into the circuit at two points. One path leads directly into the oscillator, while another path leads into the summing node.
- **1/f Noise Input:** This noise component is mixed with the oscillator's periodic signal, as indicated by the mixer block. The mixed signal is then fed back into the oscillator.
- **Signal Flow:** The mixed signal from the mixer is fed into the oscillator, which processes it. The oscillator's output is then directed to the summing node where it is combined with the white noise input.

3. **Labels, Annotations, and Key Indicators:**
- The diagram includes annotations for noise components: 'White Noise', '1/f Noise', and outputs labeled with terms like \(h_0\), \(h_2/f^2\), and \(h_3/f^3\). These indicate different noise shaping characteristics in the oscillator's response.

4. **Overall System Function:**
- The primary function of this system is to demonstrate how noise sources within an oscillator are up-converted and shaped by the oscillator's response. The mixer combines noise with a periodic signal, and the oscillator processes this mixed signal to produce an output where the phase noise characteristics are dominant. The annotations of \(1/f\) and \(1/f^3\) suggest a focus on understanding how different noise components influence the oscillator's phase noise. This setup is used to analyze the impact of various noise sources on the frequency stability and phase noise of the oscillator's output.

Fig. 19.29 Major sources of phase noise in integrated circuit oscillations.

Hence, white noise introduced within the oscillator's closed feedback loop is shaped by the oscillator's response giving rise to the $h_{2} / f^{2}$ term in (19.86). Some sources of noise are switched by the oscillations resulting in an up-conversion of their noise spectral density to the carrier frequency before being shaped by the oscillator response. A classic example is illustrated in Fig. 19.28 where noise is introduced by the tail current transistor in a differential pair with oscillating inputs. Flicker noise up-converted in this way, and then spectrally shaped by the closed-loop oscillator response gives rise to the $h_{3} / f^{3}$ term in (19.86). Finally, it was shown in Example 19.9 that additive white noise superimposed on a sinusoid gives rise to white phase noise. This is the situation when white noise is introduced immediately following an oscillator core, for example by a buffer, and the resulting phase noise is modeled by $\mathrm{h}_{0}$ in (19.86). The superposition of these three effects is diagrammed in Fig. 19.29.

A logarithmic plot of phase noise based on (19.86) is sketched in Fig. 19.30. The corner frequency $f_{c}$ marks the transition between the $1 / f^{2}$-dominated region and the $1 / f^{3}$-dominated region and is given by the frequency at
image_name:Fig. 19.30 Typical phase noise of an integrated circuit oscillator.
description:The graph in Fig. 19.30 is a logarithmic plot depicting the phase noise of an integrated circuit oscillator. It is a Bode plot, which is commonly used to represent frequency response characteristics in terms of phase noise.

**Axes Labels and Units:**
- The vertical axis represents the phase noise power spectral density, denoted as $S_{\phi, \text{osc}}(f)$, in decibels (dB).
- The horizontal axis represents the frequency ($f$) in hertz (Hz).
- The scale on the horizontal axis is logarithmic, which is typical for Bode plots to cover a wide range of frequencies.

**Overall Behavior and Trends:**
- The graph shows a downward slope, indicating a decrease in phase noise as frequency increases.
- Initially, the phase noise decreases at a rate of -30 dB/decade.
- After reaching the corner frequency $f_c$, the slope changes, and the phase noise decreases at a reduced rate of -20 dB/decade.

**Key Features and Technical Details:**
- The corner frequency $f_c$ is a critical point on the graph where the behavior of the phase noise changes. It marks the transition between the $1/f^3$-dominated region and the $1/f^2$-dominated region.
- The graph highlights two distinct regions of phase noise behavior:
- **Region 1 (left of $f_c$):** Characterized by a steeper slope of -30 dB/decade, indicative of the $1/f^3$ phase noise model.
- **Region 2 (right of $f_c$):** Characterized by a gentler slope of -20 dB/decade, indicative of the $1/f^2$ phase noise model.

**Annotations and Specific Data Points:**
- The graph is annotated with the slopes (-30 dB/decade and -20 dB/decade) to emphasize the change in phase noise behavior across the corner frequency $f_c$.
- The corner frequency $f_c$ is marked with a dashed vertical line, although its numerical value is not provided in the graph.

Fig. 19.30 Typical phase noise of an integrated circuit oscillator.
image_name:Fig. 19.31
description:The graph in Fig. 19.31 is a time-domain waveform illustrating the accumulation of jitter over multiple cycles. It depicts a periodic waveform, likely a clock signal, with a period denoted by $T_0$. The horizontal axis represents time ($t$), marked in increments of the period $T_0$ (e.g., $t_0 = 0$, $t_1 = T_0$, $t_2 = 2T_0$, $t_3 = 3T_0$, $t_4 = 4T_0$). The vertical axis is not explicitly labeled but represents the signal amplitude.

The waveform shows a regular square wave pattern with rising and falling edges. Overlaid on this waveform are multiple iterations of the signal, each slightly displaced from the previous, illustrating the increase in jitter over time. The displacement becomes more pronounced with each cycle, indicating the cumulative nature of jitter.

Above each cycle, annotations $
abla^2_{J(1)}$, $
abla^2_{J(2)}$, $
abla^2_{J(3)}$, and $
abla^2_{J(4)}$ are marked, corresponding to the variance of jitter for each cycle. These annotations suggest that jitter variance increases as the waveform progresses through each period $T_0$. The graph effectively demonstrates how jitter accumulates, impacting the timing precision of the signal over multiple cycles.

Fig. 19.31 The accumulation of jitter over multiple cycles.
which these two terms contribute equally to $S_{\phi}$.

$$
\begin{equation*}
\mathrm{f}_{\mathrm{c}}=\frac{\mathrm{h}_{3}}{\mathrm{~h}_{2}} \tag{19.88}
\end{equation*}
$$

A potentially troubling aspect of the phase noise model in (19.86) is that the close-in phase noise terms $1 / \mathrm{f}^{2}$ and $1 / \mathrm{f}^{3}$ cause the integrals in (19.60), (19.64), (19.66), and (19.68) to diverge. The absolute jitter (19.60) of an oscillator does, in fact, diverge-another reason that it is a mostly analytical tool. However, the period, P-cycle, and adjacent period jitter of an oscillator may be measured in a lab and are finite, in contrast to the model's predictions. Hence, the simple phase noise model of (19.86) is considered inaccurate at very small offset frequencies, f . The problem is that defining phase noise as the noise spectral density of $\phi_{\mathrm{k}}$ is strictly valid only if phase is a stationary random process. In fact, it is not [Gardner, 2005]. When observed over long periods of time (on the order of seconds) this non-stationarity causes analytical problems, so phase noise is not usually considered below a few Hertz. When using (19.64), (19.66) and (19.68) to estimate jitter a lower integration limit of a few Hertz is therefore applied [Liu, 2004]. Above this limit the phase noise model of (19.86) is reliable and can be integrated to accurately estimate jitter.

To understand the unboundedness of the absolute jitter of an oscillator, consider how the P-cycle jitter evolves for increasing P. As shown in Fig. 19.31, as P increases, the variance of the oscillator's P-th consecutive zero crossing time increases. Qualitatively, this is because disturbances in the state of the oscillator due to internal noise persist, circulating around its closed feedback loop. Hence, the jitter becomes a superposition of noise contributions for

Fig. 19.32 The evolution of P-cycle jitter over time.
image_name:Fig. 19.32
description:The graph in Fig. 19.32 is a logarithmic plot depicting the relationship between the P-cycle jitter standard deviation, \( \sigma_{J(P)} \), and the cycle count \( P \). Both axes are on a logarithmic scale. The horizontal axis represents \( \log(P) \), where \( P \) is the number of cycles, while the vertical axis represents \( \log(\sigma_{J(P)}) \), the logarithm of the jitter's standard deviation.

The graph shows a clear linear trend with two distinct segments. Initially, as \( P \) increases, the slope of the line is 0.5, indicating that the jitter standard deviation grows at a sub-linear rate with respect to \( P \). This suggests that for lower values of \( P \), the effect of phase noise is less pronounced.

At a critical point \( \log(P_c) \), marked on the horizontal axis, the slope changes to 1. This indicates a linear relationship between \( \log(\sigma_{J(P)}) \) and \( \log(P) \) beyond this point, meaning the jitter standard deviation grows proportionally with \( P \). This change in slope signifies that as \( P \) continues to increase, more low-frequency phase noise is included, thus increasing the jitter.

The graph clearly illustrates how the P-cycle jitter evolves over time, with the transition from a sub-linear to a linear growth pattern as \( P \) increases, emphasizing how internal noise disturbances accumulate over cycles.

all past time and grows without bound. ${ }^{16}$ Looking at the expression for P -cycle jitter in (19.66), with small P the $\sin ^{2}\left(\pi \mathrm{fP} \mathrm{T}_{0}\right)$ term in the integrand filters out low-frequency phase noise, $\mathrm{S}_{\phi}(\mathrm{f})$. As P increases, more low-frequency phase noise is included in the integral and the resulting P -cycle jitter therefore grows.

A logarithmic plot of $\sigma_{J(P)}$ versus $P$ is sketched in Fig. 19.32 [Liu, 2004]. The $h_{2} / f^{2}$ component of phase noise causes P -cycle jitter to increase in proportion to $\sqrt{P}$. Including only this term in (19.66), it may be shown that

$$
\begin{equation*}
\sigma_{J(P)}=\sqrt{\mathrm{h}_{2} \mathrm{~T}_{0}^{3}} \cdot \sqrt{\mathrm{P}} \tag{19.89}
\end{equation*}
$$

Once $N$ becomes large enough for frequencies below $f_{c}$ to have a significant effect, the $h_{3} / f^{3}$ term causes P-cycle jitter to grow approximately in direct proportion to P with the transition between the two behaviors at

$$
\begin{equation*}
\mathrm{P}_{\mathrm{c}} \cong \frac{1}{25 \mathrm{~T}_{0} \mathrm{f}_{\mathrm{c}}} \tag{19.90}
\end{equation*}
$$

Equations (19.89) and (19.90) allow for estimates of the phase-noise profile of an integrated oscillator, Fig. 19.30, from the time-domain measurements in Fig. 19.32.

#### EXAMPLE 19.18

The P-cycle jitter of a VCO operating at 1.5 GHz is observed for different P to obtain a plot like Fig. 19.32 with $P_{c}=30$. The P -cycle jitter over 10 cycles $(P=10)$ is 2.0 ps rms . Estimate the phase noise of the VCO using the model in (19.86) but neglecting the white-phase noise term $h_{0}$, which is only important at very high frequencies.

#### Solution

Substituting $P=10, \sigma_{J(10)}=2 \mathrm{ps}$, and $T_{0}=\left(1 / 1.5 \cdot 10^{9}\right) \mathrm{s}$ into (19.89) yields an estimate of the phase noise model parameter $h_{2} \cong 1350 \mathrm{rad}^{2} \cdot \mathrm{~Hz}$. Using (19.90) with $P_{c}=30$ yields $f_{c} \cong 2 \mathrm{MHz}$. Finally, substitution into (19.88) yields $\mathrm{h}_{3} \cong 2.7 \cdot 10^{9} \mathrm{rad}^{2} \cdot \mathrm{~Hz}^{2}$. Hence, the phase noise of the VCO may be modeled as follows:

$$
\begin{equation*}
\mathrm{S}_{\phi, \text { osc }}(\mathrm{f})=\frac{1350 \mathrm{rad}^{2} \cdot \mathrm{~Hz}}{\mathrm{f}^{2}}+\frac{2.7 \cdot 10^{9} \mathrm{rad}^{2} \cdot \mathrm{~Hz}^{2}}{\mathrm{f}^{3}} \tag{19.91}
\end{equation*}
$$

[^9]image_name:Fig. 19.33 Linear model of an integer-N PLL showing noise sources
description:The block diagram in Fig. 19.33 represents a linear model of an integer-N Phase-Locked Loop (PLL), highlighting various noise sources that contribute to phase noise and jitter.

Main Components:
1. **Phase Detector (PD):** The input phase $\phi_{in}$ is compared with the feedback signal. The phase detector output is proportional to the phase difference and is represented by $K_{pd}$, the phase detector gain.

2. **Loop Filter:** The output from the phase detector is processed through a loop filter characterized by $K_{lp}H_{lp}(s)$, where $K_{lp}$ is the gain and $H_{lp}(s)$ is the transfer function of the filter. This block shapes the control signal that adjusts the VCO.

3. **Voltage-Controlled Oscillator (VCO):** The control signal from the loop filter, along with noise $v_n$ and $V_n$, influences the VCO. The VCO's output frequency is modulated by these inputs, represented by $K_{osc}/s$, where $K_{osc}$ is the VCO gain.

4. **Frequency Divider:** The output of the VCO is fed back through a frequency divider with a division ratio of $1/N$. This feedback signal is compared with the input reference signal in the phase detector.

5. **Noise Sources:**
- **$v_n$ and $V_n$:** Represent noise introduced within the loop filter circuitry.
- **$\phi_{vco}$ and $S_{\phi,osc}$:** Account for intrinsic VCO noise.
- **$\phi_n$ and $S_{\phi,n}$:** Represent noise on the input reference.

Flow of Information or Control:
- The input reference phase $\phi_{in}$ and the feedback signal from the divider are compared in the phase detector, generating a signal that is proportional to the phase difference.
- This signal is filtered and amplified by the loop filter, which shapes the control voltage applied to the VCO.
- The VCO output frequency is adjusted according to this control signal and is also influenced by the noise sources $v_n$ and $V_n$.
- The VCO output is divided by $1/N$ and fed back to the phase detector, closing the loop.

Labels, Annotations, and Key Indicators:
- **$K_{pd}$:** Phase detector gain.
- **$K_{lp}H_{lp}(s)$:** Loop filter transfer function.
- **$K_{osc}/s$:** VCO transfer function.
- **$1/N$:** Divider ratio.
- **Noise Sources:** $v_n$, $V_n$, $\phi_{vco}$, $S_{\phi,osc}$, $\phi_n$, $S_{\phi,n}$ are annotated to indicate their impact on the system.

Overall System Function:
The primary function of this PLL is to synchronize the output phase $\phi$ with the input reference phase $\phi_{in}$, despite the presence of noise. The arrangement of components and signal flow ensures that the output frequency tracks the input reference frequency, while the loop filter and feedback mechanism work to minimize the effect of noise on the system's performance. The model illustrates how different noise sources contribute to jitter and phase noise within the PLL.

Fig. 19.33 Linear model of an integer-N PLL showing noise sources.

## 19.5 JITTER AND PHASE NOISE IN PLLS

There are several sources of jitter in a PLL. Notably:

- Jitter on the input reference, $\phi_{\text {in }}$
- Jitter inherent in the VCO
- Noise generated by circuitry in the loop filter
- Noise generated by circuitry in the divider

Since the jitter in any practical PLL is relatively small, its propagation through and within the loop can be analyzed using a linear small-signal model. The noise sources listed above are introduced at various points in the loop, as shown in the linear model block diagram in Fig. 19.33. In order for that diagram to be general, all noise in the phase detector and loop filter must be modeled by the single output-referred noise voltage, $\mathrm{v}_{\mathrm{n}}$, and the additional jitter introduced by the divider is modeled by the additive term $\phi_{n}$. Also labeled in Fig. 19.33 are the power spectral densities of all the random signals: the noise spectral density $V_{n}$, and the phase noise spectra $S_{\phi, \text { in }}, S_{\phi, n}$, $S_{\phi, \text { osc }}$, and $S_{\phi}$. Each noise source's contribution to the PLL output phase noise is filtered by a different response.

### 19.5.1 Input Phase Noise and Divider Phase Noise

Both the input reference phase noise and divider phase noise appear at the input and are therefore filtered by the PLL's jitter transfer function,

$$
\begin{equation*}
\mathrm{H}(\mathrm{~s})=\frac{\mathrm{K}_{\mathrm{pd}} \mathrm{~K}_{\mathrm{lp}} \mathrm{~K}_{\mathrm{osc}} \mathrm{H}_{\mathrm{lp}}(\mathrm{~s}) / \mathrm{s}}{1+\mathrm{L}(\mathrm{~s})} \tag{19.92}
\end{equation*}
$$

where L(s) is the PLL's open loop gain given by (19.30). For the special case of a 2 nd order PLL, (19.92) becomes (19.35).

Since the loop filter $\mathrm{H}_{\mathrm{lp}}(\mathrm{s})$ is lowpass, $\mathrm{H}(\mathrm{s})$ will also be lowpass. A dc gain of N arises because the output frequency is N -times higher than the input; hence, a phase variation of $\Delta \phi_{\text {in }}$ rad at the input that is perfectly tracked at the output becomes a $N \Delta \phi_{\text {in }}$ rad phase change with respect to the higher output frequency. Hence, any slow variations in the timing of the input clock will be faithfully reproduced in the output clock-exactly what one would expect from a phase-locked system. However, very fast variations in the input clock phase, those that lie beyond the PLL's closed-loop bandwidth, are not tracked. Rather, they are attenuated by the lowpass $|\mathrm{H}(\mathrm{f})|^{2}$.

### 19.5.2 VCO Phase Noise

The VCO phase noise is filtered by a highpass response straightforwardly obtained from the signal flow graph of Fig. 19.33.

$$
\begin{equation*}
\mathrm{H}_{\mathrm{osc}}(\mathrm{~s})=\frac{1}{1+\mathrm{L}(\mathrm{~s})} \tag{19.93}
\end{equation*}
$$

At high frequency, $|L(f)|^{2} \approx 0$ and VCO phase noise appears unaltered at the output, $\mathrm{H}_{\mathrm{osc}}(\mathrm{s}) \approx 1$. However, at low frequency the loop gain is large and VCO phase noise is attenuated. At first sight, it may appear strange that the VCO's inherent phase noise somehow disappears when enclosed within a PLL.

The PLL senses variations in the VCO's output phase and adjusts the input $\mathrm{V}_{\mathrm{cnt1}}$ to counter those variations in an effort to keep the output phase-locked to the input. Hence, slow natural variations in the VCO's phase are completely canceled by the loop. On the other hand, the loop is unable to respond to very fast variations, which appear identically in the high-frequency portion of $S_{\phi, \text { osc }}(f)$ and $S_{\phi}(f)$.

#### EXAMPLE 19.19

A VCO with a phase noise given by $S_{\phi, v c o}(f)=h_{2} / f^{2}$ is placed within an ideal second-order PLL. What is the resulting phase noise at the output?

#### Solution

For a second-order PLL, the open-loop gain $L(s)$ is specified in (19.33). Substitution into (19.93) yields the transfer function from VCO phase noise to the PLL output.

$$
\begin{equation*}
H_{\mathrm{osc}}(\mathrm{~s})=\frac{\mathrm{s}^{2}}{\mathrm{~s}^{2}+\frac{\omega_{\mathrm{plI}}}{\mathrm{Q}} \mathrm{~s}+\omega_{\mathrm{plI}}^{2}} \tag{19.94}
\end{equation*}
$$

The output phase noise is given by,

$$
\begin{align*}
S_{\phi}(f) & =S_{\phi, o s c}(f)\left|H_{o s c}(f)\right|^{2} \\
& =\frac{h_{2}}{f^{2}} \cdot \frac{f^{4}}{\left(f^{2}+\frac{\omega_{\mathrm{pll}}}{2 \pi Q} f+\frac{\omega_{\text {pII }}^{2}}{4 \pi^{2}}\right)^{2}}  \tag{19.95}\\
& =\frac{h_{2} f^{2}}{\left(f^{2}+\frac{\omega_{\mathrm{pll}}}{2 \pi Q}+\frac{\omega_{\text {pII }}^{2}}{4 \pi^{2}}\right)^{2}}
\end{align*}
$$

This is a bandpass spectrum with a peak around $\omega_{\text {pII }}$. If (19.95) is substituted into (19.60) with the upper limit of integration approximated as infinite $\left(1 / 2 \mathrm{~T}_{0} \approx \infty\right)$ a very simple expression is obtained for absolute jitter.

$$
\begin{equation*}
\sigma_{\tau}^{2}=\frac{\mathrm{h}_{2} \mathrm{QT}_{0}^{2}}{2 \omega_{\mathrm{plI}}} \tag{19.96}
\end{equation*}
$$

image_name:Fig. 19.34
description:The graph in Fig. 19.34 is a Bode plot representing the normalized transfer functions from noise sources within a Phase-Locked Loop (PLL) to the output phase noise. The plot consists of multiple curves, each depicting a different transfer function's magnitude response over frequency.

1. **Axes Labels and Units:**
- The x-axis represents frequency, though specific units are not provided, it is typically in hertz (Hz) for such plots.
- The y-axis represents the magnitude of phase transfer functions, likely in decibels (dB), given the typical use of Bode plots.

2. **Overall Behavior and Trends:**
- The solid line labeled \(|H(f)|\) shows a flat response at low frequencies, indicating a constant transfer function magnitude, and then begins to roll off at higher frequencies.
- The dashed line \(|H_{n}(f)|\) starts at a lower magnitude and increases with frequency, indicating that the transfer function magnitude grows as frequency increases.
- Another curve, \(|H_{osc}(f)|\), appears to start at a higher magnitude at low frequencies and decreases as the frequency increases.

3. **Key Features and Technical Details:**
- The plot shows a crossover point where the curves \(|H(f)|\) and \(|H_{n}(f)|\) intersect, which may indicate a frequency of interest or a boundary between different operational regimes.
- The solid line \(|H(f)|\) suggests a low-pass filter characteristic, while the dashed line \(|H_{n}(f)|\) suggests a high-pass filter characteristic.
- The curve \(|H_{osc}(f)|\) may represent a bandpass or notch filter characteristic, depending on its exact shape and context.

4. **Annotations and Specific Data Points:**
- The graph includes labeled curves, but no specific numerical values or annotations for cutoff frequencies or gain levels are provided. The precise crossover frequency or other critical points would typically be determined from additional data or context.

Fig. 19.34 Normalized transfer functions from noise sources within a PLL to the output phase noise.

This expression reveals that the PLL loop bandwidth (approximately equal to $\omega_{\mathrm{pIII}} / \mathrm{Q}$ ) should be maximized in order to minimize the contribution of VCO phase noise to a PLL's output jitter.

### 19.5.3 Loop Filter Noise

Looking at Fig. 19.33, the loop filter noise $\mathrm{V}_{\mathrm{n}}$ is filtered by the following response:

$$
\begin{equation*}
\mathrm{H}_{\mathrm{n}}(\mathrm{~s})=\frac{\mathrm{K}_{\mathrm{osc}} / \mathrm{s}}{1+\mathrm{L}(\mathrm{~s})} \tag{19.97}
\end{equation*}
$$

At high frequencies due to the lowpass $\mathrm{H}_{\mathrm{lp}}, \mathrm{H}_{\mathrm{n}} \approx \mathrm{K}_{\mathrm{osc}} / \mathrm{s} \approx 0$. At low frequencies, $\mathrm{H}_{\mathrm{n}}(\mathrm{s}) \approx \mathrm{N} / \mathrm{K}_{\mathrm{pd}} \mathrm{K}_{1 \mathrm{p}} \mathrm{H}_{\mathrm{lp}}(\mathrm{s})$. Typically, the combination of the phase detector and loop filter $\mathrm{K}_{\mathrm{pd}} \mathrm{K}_{\mathrm{lp}} \mathrm{H}_{\mathrm{lp}}(\mathrm{s})$ has very high gain at dc to ensure precise phase locking of the input and output in steady-state, so $\mathrm{H}_{n}$ is also very small at dc. For example, in the case of an ideal charge-pump loop filter $\mathrm{H}_{1 \mathrm{p}}$ has a pole at dc, so that $\mathrm{H}_{\mathrm{n}}(0)=0$. Hence, noise introduced in the loop fil-

Key Point: PLL loop bandwidth sets the cutoff frequency below which VCO phase noise is attenuated and above which input reference (and divider) phase noise is attenuated.
ter appears bandpass-filtered in the output phase noise.

Typical PLL responses $|H(f)|,\left|H_{\text {osc }}(f)\right|$, and $\left|H_{n}(f)\right|$ are sketched in Fig. 19.34. The PLL loop bandwidth sets the cutoff frequency below which VCO phase noise is attenuated and above which input reference (and divider) phase noise is attenuated.

Fig. 19.35 Equivalent circuit for the noise analysis of a charge-pump loop filter.
image_name:Fig. 19.35
description:[{'name': 'C1', 'type': 'Capacitor', 'value': 'C1', 'ports': {'Np': 'X2', 'Nn': 'GND'}}, {'name': 'C2', 'type': 'Capacitor', 'value': 'C2', 'ports': {'Np': 'V_n^2(f)', 'Nn': 'GND'}}, {'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'X1', 'N2': 'V_n^2(f)'}}, {'name': 'V_R^2(f)', 'type': 'Voltage Source', 'value': '4kTR', 'ports': {'Np': 'X2', 'Nn': 'X1'}}
extrainfo:The circuit is an equivalent circuit for noise analysis of a charge-pump loop filter, showing the thermal noise voltage across the resistor R.

#### EXAMPLE 19.20

Consider the charge-pump PLL designed in Example 19.8 and consider its operation with $\mathrm{N}=75$ using the VCO in Example 19.18. Assume the $20-\mathrm{MHz}$ PLL input (after the $\mathrm{M}=2$ divider) has a phase noise modeled by (19.86) with $\mathrm{h}_{0}=10^{-14} \mathrm{rad}^{2} / \mathrm{Hz}, \mathrm{h}_{2}=10^{-9} \mathrm{rad}^{2} \cdot \mathrm{~Hz}$, and $\mathrm{h}_{3} \approx 0$. What is the phase noise of the PLL output due to the reference input, loop filter resistor, and VCO?

#### Solution

The contribution of the reference input to the PLL output phase noise is given by

$$
\mathrm{S}_{\phi, \mathrm{in}}(\mathrm{f})=\left(8 \cdot 10^{-16}+\frac{7 \cdot 10^{-11}}{\mathrm{f}^{2}}\right) \mathrm{rad}^{2} / \mathrm{Hz}
$$

filtered by $|H(f)|^{2}$. If $C_{2}$ is neglected, $H(s)$ is given by (19.35) with the values of $\omega_{\mathrm{pll}}$ and $\omega_{z^{\prime}}$ being those chosen in Example 19.8: $2 \pi \cdot 800 \mathrm{kHz}$ and $2 \pi \cdot 400 \mathrm{kHz}$ respectively.

The loop filter resistor R results in thermal noise at the control voltage node, $\mathrm{V}_{\mathrm{cnt1}}$. Its noise spectral density may be determined by a noise circuit analysis of Fig. 19.35 resulting in

$$
\begin{equation*}
V_{n}^{2}(f)=4 k T R\left(\frac{C_{e q}}{C_{2}}\right)^{2}\left(\frac{1}{1+f^{2} R^{2} C_{e q}^{2}}\right) \tag{19.98}
\end{equation*}
$$

where $C_{\text {eq }}=C_{1} C_{2} /\left(C_{1}+C_{2}\right)$. Maintaining the 2nd-order model, this noise is then bandpass filtered by

$$
\begin{equation*}
H_{n}(s)=\frac{K_{\mathrm{osc}} s}{s^{2}+\frac{\omega_{\mathrm{pll}}}{Q} s+\omega_{\mathrm{plI}}^{2}} \tag{19.99}
\end{equation*}
$$

where $Q=0.5$ from Example 19.8.
Finally, from Example 19.18 the VCO phase noise modeled by (19.91) is filtered by $\left|\mathrm{H}_{\mathrm{osc}}(\mathrm{f})\right|^{2}$ with $\mathrm{H}_{\mathrm{osc}}$ as in (19.94).

The total output phase noise is the superposition of all contributors.

$$
\begin{equation*}
S_{\phi}(\mathrm{f})=\mathrm{S}_{\phi, \mathrm{in}}(\mathrm{f})|\mathrm{H}(\mathrm{f})|^{2}+\mathrm{V}_{n}^{2}(\mathrm{f})\left|\mathrm{H}_{\mathrm{n}}(\mathrm{f})\right|^{2}+\mathrm{S}_{\phi, \mathrm{osc}}(\mathrm{f})\left|\mathrm{H}_{\mathrm{osc}}(\mathrm{f})\right|^{2} \tag{19.100}
\end{equation*}
$$

A plot of all three phase noise contributors and their sum is shown in Fig. 19.36. Note that at low frequencies, the total output phase noise is equal to the input reference phase noise because the other noise contributors are filtered out by the PLL. Similarly, at high frequencies only the VCO phase noise contributes. In this example, thermal noise in the loop filter plays an insignificant role in the total output phase noise-a typical result. The jitter of the PLL output will be dominated by the high-frequency VCO noise contributions which span a much wider range of frequencies than the input-dominated portion of the phase noise spectrum and, hence, contribute much more to the integral in (19.60).
image_name:Fig. 19.36
description:The graph in Fig. 19.36 is a log-log plot depicting the phase noise contributions to the output of a Phase-Locked Loop (PLL) from three sources: the input reference, the loop filter resistor, and the Voltage-Controlled Oscillator (VCO). The x-axis represents frequency in hertz (Hz), ranging from 10^0 to 10^8, while the y-axis represents the output phase noise in 10log10(rad^2/Hz), ranging from -150 to -50.

The graph shows three distinct curves:

1. **VCO Contribution (Dashed Line):** This line starts at a lower phase noise level at low frequencies and increases linearly with frequency, indicating that the VCO phase noise dominates at high frequencies.

2. **Loop Filter Resistor Contribution (Dash-Dot Line):** This curve shows a peak around 10^5 Hz, indicating that the thermal noise from the loop filter resistor is most significant around this frequency range but is otherwise relatively insignificant.

3. **Input Reference Contribution (Solid Line):** This curve remains relatively flat, showing a consistent contribution across the frequency range, but it is generally lower than the VCO contribution at high frequencies.

4. **Total Phase Noise (Thick Solid Line):** This line represents the total phase noise contribution, which is a combination of all three sources. It starts high at low frequencies, dips around 10^3 Hz, and then rises again, peaking slightly around 10^5 Hz before gradually decreasing. This indicates that the total phase noise is dominated by the VCO noise at high frequencies.

Overall, the graph highlights that at low frequencies, the input reference is the main contributor to phase noise, while at high frequencies, the VCO noise becomes the dominant factor. The loop filter resistor plays a minimal role in the overall phase noise across most frequencies.

Fig. 19.36 Phase noise contributions of the input reference, loop filter resistor, and VCO to the output of the PLL in Example 19.20.

## 19.6 KEY POINTS

- The instantaneous frequency deviation of a VCO from its free-running frequency is the derivative of its instantaneous phase. Hence, its instantaneous phase is the integral of the instantaneous frequency deviation. [p. 740]
- Once a PLL is in lock, its dynamic response to input phase and frequency changes can be well approximated by a linear model, as long as these changes are slow and small about their operating or bias point. [p. 748]
- The design of a second-order PLL with $\mathrm{Q}=0.5$ provides good transient settling behavior without excessive spreading of the loop filter time constants. A design with $\mathrm{Q}=0.1$ offers even better tracking behavior, but generally demands a larger loop-filter time constant for the same loop bandwidth. [p. 750]
- Due to the discrete-time nature of the PLL, its loop bandwidth is limited by stability considerations to at most roughly $1 / 20$ th to $1 / 10$ th of the reference frequency, a fact not predicted by the continuous-time linear model. [p. 752]
- Jitter is a measure of random variations in the timing phase of a clock signal and phase noise is its fre-quency-domain representation. They present fundamental limitations on the accuracy of time references. [p. 756]
- The absolute jitter of a clock, $\tau_{\mathrm{k}}$, is a discrete-time sequence giving the displacement of its transition times away from their ideal values. [p. 756]
- Periodic variations in the phase of a clock result in discrete tones in phase noise spectra and are called spurs. [p. 762]
- PLL loop bandwidth sets the cutoff frequency below which VCO phase noise is attenuated and above which input reference (and divider) phase noise is attenuated. [p. 779]

[^0]:    7. A figure of 2 was used in the reference but 1.5 appears to be a more practical choice.
[^1]:    3. This PLL is only used when the VCO output and the reference input are both digital signals or have been converted to digital signals by a limiter.
[^2]:    4. For those more familiar with damping factor, $\zeta$, of a second-order transfer function, note that $\zeta=1 / 2 \mathrm{Q}$.
[^3]:    5. Although an all-pole system with $\mathrm{Q}=0.5$ will have no transient overshoot or peaking in its magnitude response, the closed loop PLL $H(s)$ has a zero which introduces both even when $Q \leq 0.5$.
[^4]:    6. equation (19.38)
7. equation (19.40)
8. equation (19.32)
9. equation (19.23)
10. equation (19.27)
[^5]:    11. equation (19.36)
[^6]:    13. Specifically, $\mathrm{S}_{\phi}(\mathrm{f})$ is the one-sided power spectral density of $\phi_{\mathrm{k}}$, defined over the range $0 \leq \mathrm{f} \leq 1 / 2 \mathrm{~T}_{0}$ and obtained from the discrete-time Fourier transform of the autocorrelation of $\phi_{k}$.
[^7]:    14. Strictly speaking, $\phi_{\mathrm{k}}$ is a discrete-time random process; hence, there may be some aliasing of the white noise in $\mathrm{V}_{\mathrm{o}, \mathrm{n}}$ causing the phase noise to be larger than this. Naturally, the white noise is assumed to be eventually bandlimited by some capacitance at $\mathrm{v}_{0}$ ensuring it has finite power.
[^8]:    15. Each component of $S_{\phi}(f)$ gives rise to spectral content at a multiplicity of offset frequencies in $\mathcal{L}(\Delta f)$, the amplitudes of which are related by Bessel functions. If the phase modulation of the carrier is very small, a linear approximation is possible that ignores all but the first (largest) sideband in $\mathcal{L}(\Delta f)$ arising from each component of $S_{\phi}(f)$.
[^9]:    16. This is analogous to a random-walk process: a person beginning at a fixed point takes a step (randomly) in any direction. Over time, their mean position remains equal to their starting point since their direction of travel is random, but the variance of their position continues to grow as they may (with finite probability) wind up very far from the their starting point.
