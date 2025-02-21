# Chapter6 FILTERS

## 6.1 Introduction

With only the techniques of transistors and op-amps it is possible to delve into a number of interesting areas of linear (as contrasted with digital) circuitry. We believe that it is important to spend some time doing this now, in order to strengthen understanding of some of these difficult concepts (transistor behavior, feedback, op-amp limitations, etc.) before introducing more new devices and techniques and getting into the large area of digital electronics. Therefore, in this chapter we treat the topic of filters, and particularly active filters. The latter use resistors and capacitors, in combination with amplifiers (usually op-amps), to produce filters with well-defined frequency response. As we'll see, these filters (along with the classic $L C$ passive filters that they can emulate) can be much sharper than the simple $R C$ filters we saw in Chapter 1.

The three following chapters will continue with additional topics in analog electronics: Chapter 7 (Oscillators and timers), Chapter 8 (Low-noise techniques), and Chapter 9 (Voltage regulation and power conversion). Then, following two chapters on digital logic, we revisit analog electronics, happily harmonized with the intervening digital teachings, in Chapter 12 (Logic interfacing), Chapter 13 (Digital meets analog), and Chapter 15 (Microcontrollers).

## 6.2 Passive filters

In Chapter 1 we began a discussion of filters made from resistors and capacitors. Those simple $R C$ filters produced gentle highpass or lowpass gain characteristics, with a $6 \mathrm{~dB} /$ octave falloff well beyond the -3 dB point. By cascading highpass and lowpass filters, we showed how to obtain bandpass filters, again with gentle $6 \mathrm{~dB} /$ octave "skirts." Such filters are sufficient for many purposes, especially if the signal being rejected by the filter is far removed in frequency from the desired signal passband. Some examples are bypassing of radiofrequency signals in audio circuits, "blocking" capacitors for elimination of dc levels, and separation of modulation from a communications "carrier."

### 6.2.1 Frequency response with RC filters

Often, however, filters with flatter passbands and steeper skirts are needed. This happens whenever signals must be filtered from other interfering signals nearby in frequency. The obvious next question is whether or not (by cascading a number of identical lowpass filters, say) we can generate an approximation to the ideal "brick-wall" lowpass frequency response, as in Figure 6.1.
image_name:Figure 6.1
description:The graph depicted in Figure 6.1 is a frequency response curve representing an ideal brick-wall lowpass filter. This type of graph is typically referred to as a magnitude response plot, often used to illustrate how a filter affects the amplitude of different frequency components of a signal.

1. **Type of Graph and Function:** The graph is a frequency response plot, showing the relationship between the input and output voltage ratio (V_out/V_in) of a filter across different frequencies.

2. **Axes Labels and Units:**
- The vertical axis is labeled as V_out/V_in, representing the ratio of output voltage to input voltage. This axis is dimensionless, typically expressed in a linear scale.
- The horizontal axis represents frequency, labeled with a cutoff frequency point at f_0. The units for frequency are typically in hertz (Hz), although the specific unit is not marked on this graph.

3. **Overall Behavior and Trends:**
- The graph shows a flat passband where the ratio V_out/V_in is equal to 1, indicating that frequencies below the cutoff frequency (f_0) are passed through the filter without attenuation.
- At the cutoff frequency (f_0), the response drops sharply to zero, illustrating the ideal "brick-wall" characteristic where frequencies above f_0 are completely attenuated.

4. **Key Features and Technical Details:**
- The graph has a distinct 'knee' at the cutoff frequency f_0, beyond which the response abruptly falls to zero.
- There are no gradual slopes or roll-off regions; the transition from passband to stopband is instantaneous in this ideal representation.

5. **Annotations and Specific Data Points:**
- The graph includes a marked cutoff frequency point at f_0, where the transition from passband to stopband occurs.
- The magnitude of the passband is constant at 1, indicating no gain or loss in this ideal scenario.

Figure 6.1. Ideal brick-wall lowpass filter.
We know already that simple cascading won't work, because each section's input impedance will seriously load the previous section, degrading the response. But with buffers between each section (or by arranging to have each section of much higher impedance than the one preceding it), it would seem possible. Nonetheless, the answer is no. Cascaded $R C$ filters do produce a steep ultimate falloff, but the "knee" of the curve of response versus frequency is not sharpened. We might restate this as "many soft knees do not a hard knee make." To make the point graphically, we plotted some graphs of gain response (i.e., $V_{\text {out }} / V_{\text {in }}$ ) versus frequency for lowpass filters constructed from $1,2,4,8$, 16, and 32 identical $R C$ sections, perfectly buffered (Figure 6.2).

The first graph shows the effect of cascading several $R C$ sections, each with its 3 dB point at unit frequency. As more sections are added, the overall 3 dB point is pushed downward in frequency, as you could easily have predicted. ${ }^{1}$ To compare filter characteristics fairly, the rolloff

[^68]image_name:A
description:The graph labeled 'A' is a linear plot depicting the amplitude response (V_out/V_in) versus frequency for lowpass filters constructed from multiple identical RC sections, specifically 1, 2, 4, 8, 16, and 32 sections. The x-axis represents frequency in Hertz (Hz), ranging from 0 to 3 Hz, while the y-axis represents the amplitude response, ranging from 0 to 1.

**Overall Behavior and Trends:**
- The graph shows a series of curves, each corresponding to a different number of RC sections (n = 1, 2, 4, 8, 16, 32).
- As the number of sections increases, the curves become steeper, indicating a more rapid decrease in amplitude response with increasing frequency.
- Each curve starts at an amplitude response of 1 at 0 Hz and decreases as frequency increases.

**Key Features and Technical Details:**
- The -3 dB point is marked with a dashed horizontal line at approximately 0.707 on the amplitude response axis.
- With more sections, the -3 dB point shifts to a lower frequency, demonstrating that the overall cutoff frequency decreases as more sections are added.
- The curves exhibit a typical lowpass filter behavior where higher frequencies are attenuated more.

**Annotations and Specific Data Points:**
- Each curve is labeled with the corresponding number of sections (n).
- The -3 dB line helps in identifying the cutoff frequency for each configuration.

This graph effectively illustrates how cascading more RC sections in a lowpass filter configuration affects the frequency response, resulting in a steeper roll-off and a lower cutoff frequency as the number of sections increases.
image_name:B
description:Graph B in Figure 6.2 is a linear plot illustrating the amplitude response (V_out/V_in) versus normalized frequency for lowpass filters composed of multiple identical RC sections. The x-axis represents the normalized frequency, while the y-axis indicates the amplitude response, both ranging from 0 to 3 and 0 to 1, respectively. The graph features several curves, each corresponding to a different number of RC sections (n = 1, 2, 4, 8, 16, 32).

The key trend observed is that as the number of sections (n) increases, the roll-off becomes steeper, indicating a sharper transition from passband to stopband. Each curve starts at an amplitude of 1 at low frequencies, gradually decreasing as frequency increases. The -3 dB point, marked by a dashed horizontal line at approximately 0.707 on the y-axis, serves as a reference for comparing the filters' cutoff frequencies.

Notably, the curves for higher numbers of sections (e.g., n = 32) show a more pronounced decrease in amplitude at lower normalized frequencies compared to those with fewer sections (e.g., n = 1). This behavior reflects the increased selectivity and sharper cutoff characteristic of filters with more sections. The graph effectively demonstrates how cascading more RC sections enhances the filter’s ability to attenuate frequencies beyond the desired cutoff.
image_name:C
description:The graph labeled 'C' is a Bode plot representing the amplitude response of lowpass filters constructed from multiple cascaded RC sections. The plot is logarithmic, both in the frequency and amplitude axes, which is typical for Bode plots.

**Axes Labels and Units:**
- The x-axis is labeled "Normalized Frequency (log scale)" and represents frequency on a logarithmic scale.
- The y-axis is labeled "Amplitude Response V_out / V_in" and represents the gain of the filter, also on a logarithmic scale.

**Overall Behavior and Trends:**
- The graph shows several curves, each representing a different number of cascaded RC sections, denoted by 'n'. The curves are plotted for n = 1, 2, 4, 8, 16, and 32.
- As the number of cascaded sections increases, the roll-off of the filter becomes steeper, indicating a faster attenuation of higher frequencies.
- The curves start at a normalized amplitude of 1 (0 dB) at low frequencies and gradually decrease as the frequency increases.

**Key Features and Technical Details:**
- The -3 dB point, which is the cutoff frequency, is normalized to 1 for all curves. This normalization allows for a fair comparison of the roll-off characteristics of the filters.
- The curves show that with more sections, the filter has a sharper transition band and greater attenuation in the stopband.

**Annotations and Specific Data Points:**
- Each curve is labeled with the corresponding number of sections (n = 1, 2, 4, 8, 16, 32).
- The plot clearly demonstrates the effect of increasing the number of sections on the filter's frequency response, highlighting the trade-off between complexity and performance in filter design.

Figure 6.2. Frequency responses of multisection $R C$ filters. Graphs $A$ and $B$ are linear plots, whereas $C$ is logarithmic. The filter responses in $B$ and $C$ have been normalized (or scaled) for 3 dB attenuation at unit frequency.
frequencies of the individual sections should be adjusted so that the overall 3 dB point is always at the same frequency. For this reason, the other graphs in Figure 6.2 are all "normalized" in frequency, meaning that the -3 dB point (or breakpoint, however defined) is at a frequency of 1 radian per second (or at 1 Hz ). To determine the response of a filter whose breakpoint is set at some other frequency, simply multiply the values on the frequency axis by the actual breakpoint frequency $f_{\mathrm{c}}$. In general, we will also stick with the log-log graph of frequency response when talking about filters because it tells the most about the frequency response. It lets you see the approach to the ultimate rolloff slope, and it permits you to read off accurate values of attenuation. In this case (cascaded $R C$ sections), the normalized graphs in Figures 6.2B and 6.2C demonstrate the soft knee characteristic of passive $R C$ filters.

It's interesting to look also at the phase shift of an $R C$ lowpass cascade, again adjusted to put the overall 3 dB points at unit frequency; these are plotted in Figure 6.3. The lagging phase shift reaches $90^{\circ} \times n$ asymptotically, for $n$ cascaded sections, as you might expect (recall the smooth transition from $0^{\circ}$ to $90^{\circ}$ lagging phase shift of a single $R C$ section, Figure 1.104). Perhaps non-intuitively, however, the phase shift at the 3 dB point grows progressively with larger cascades. Phase-shift characteristics are important, as we'll see presently, because they determine the filter's in-band waveform distortion.

#### A. Degradation of ultimate attenuation: non-ideal capacitors

Unlike ideal capacitors, real capacitors exhibit some extra "parasitic" elements - most prominently an effective series resistance (ESR) and an effective series inductance (ESL). So at very high frequencies (where the capacitor's ESR becomes comparable to the capacitive reactance $1 / \omega C$ ) a real $R C$ filter stops rolling off. We modeled this by using SPICE (see Appendix J) for the cascaded multisection $R C$ filter, see Figure 6.4. For this comparison we assumed that you want to do some $R C$ filtering of a dc rail that supplies a low-level stage, to suppress higher frequency switching noise, coupled signals, and the like. So we gave ourselves a "budget" of $100 \Omega$ total series resistance (consistent with a load current of a few milliamps); and we limited ourselves to $20 \mu \mathrm{~F}$ total capacitance (to maintain reasonable physical size). Then we ran simulations of three filters: a single $100 \Omega, 20 \mu \mathrm{~F} R C$ stage; a 2-section filter with $50 \Omega$ and $10 \mu \mathrm{~F}$ in each section; and a 4-section filter with $25 \Omega$ and $5 \mu \mathrm{~F}$ in each section. We ran plots of the response of these three filters, first with perfect capacitors (no ESR), then
with realistic ESR values, taken from capacitor datasheets (e.g., $1 \Omega$ for a $5 \mu \mathrm{~F}$ electrolytic capacitor rated at 100 V ).

You can see the effect of the series resistance, namely a loss of ultimate attenuation at high frequencies, where the impedance of the capacitors asymptotes to the ESR value, rather than continuing to fall as $1 / f$. Nevertheless, it is clear that spreading the total capacitance into several filter sections makes good sense.
image_name:Figure 6.3
description:Figure 6.3 is a Bode plot illustrating the phase shift versus frequency for multisection RC lowpass filters. The graph displays phase shift on the vertical axis, measured in degrees, and normalized frequency on the horizontal axis, presented on a logarithmic scale ranging from 0.1 to 100.

The plot contains four curves, each representing a different number of filter sections (n = 1, 2, 4, and 8). As the number of sections increases, the phase shift becomes more negative at a given frequency, indicating a greater delay introduced by the filter.

1. **Type of Graph and Function**: This is a Bode plot focusing on phase shift.

2. **Axes Labels and Units**: The vertical axis is labeled "Phase Shift (degrees)," and the horizontal axis is labeled "Normalized Frequency (log scale)." The phase shift ranges from 0 to -700 degrees, and the frequency is plotted on a logarithmic scale from 0.1 to 100.

3. **Overall Behavior and Trends**: All curves show a downward trend, indicating increasing phase shift with increasing frequency. The phase shift begins near 0 degrees at low frequencies and becomes more negative as frequency increases. The curves asymptotically approach a maximum negative phase shift value as frequency continues to rise.

4. **Key Features and Technical Details**: Each curve represents a different number of filter sections, with n = 1 having the least negative phase shift and n = 8 having the most. The phase shift increases more rapidly with frequency for higher values of n.

5. **Annotations and Specific Data Points**: The curves are annotated with their respective n values (1, 2, 4, and 8), showing how the phase shift behavior changes with the number of sections in the filter. The vertical line at a normalized frequency of 1 serves as a reference point for comparing phase shifts across different curves.

Figure 6.3. Phase shift versus frequency for the multisection $R C$ lowpass filters of Figure 6.2C.
image_name:Figure 6.4
description:The graph in Figure 6.4 is a Bode plot depicting the attenuation (in decibels) versus frequency (in Hertz) for cascaded RC lowpass filters. The x-axis represents frequency, ranging from 10 Hz to 100 kHz, plotted on a logarithmic scale. The y-axis indicates attenuation in decibels, ranging from 0 dB to -120 dB.

The plot compares the performance of ideal (dotted lines) and real (solid lines) RC filters with different numbers of sections: 1, 2, and 4 sections. The real capacitors include some irreducible series resistance, which affects the attenuation characteristics.

1. **Overall Behavior and Trends:**
- As frequency increases, the attenuation also increases for both ideal and real filters.
- The ideal filters (dotted lines) show a consistent increase in attenuation with frequency, whereas the real filters (solid lines) show less attenuation due to the series resistance.
- The curves for the 1, 2, and 4 section filters demonstrate that more sections result in greater attenuation at higher frequencies.

2. **Key Features and Technical Details:**
- The 1-section real filter shows less attenuation than the ideal filter across the frequency range.
- The 2-section and 4-section filters show progressively higher attenuation, with the real filters deviating more significantly from the ideal as the number of sections increases.
- The curves exhibit a steeper slope with more sections, indicating sharper roll-off characteristics.

3. **Annotations and Specific Data Points:**
- Each curve is labeled with the number of sections (1, 2, or 4) to distinguish between them.
- The gridlines and labels on the axes provide a clear reference for assessing the attenuation levels at specific frequencies.
image_name:Figure 6.2C
description:
[
name: R1, type: Resistor, ports: {N1: Vin, N2: N1}
name: C1, type: Capacitor, ports: {Np: N1, Nn: GND}
name: R2, type: Resistor, ports: {N1: N1, N2: N2}
name: C2, type: Capacitor, ports: {Np: N2, Nn: GND}
name: R3, type: Resistor, ports: {N1: N2, N2: N3}
name: C3, type: Capacitor, ports: {Np: N3, Nn: GND}
name: R4, type: Resistor, ports: {N1: N3, N2: Vout}
name: C4, type: Capacitor, ports: {Np: Vout, Nn: GND}
]
extrainfo:The diagram shows the attenuation versus frequency for multisection RC lowpass filters. The circuit is a cascade of RC sections, demonstrating increased attenuation with more sections. The plot compares ideal and real filters, highlighting the effect of series resistance in capacitors.

Figure 6.4. Real capacitors include some irreducible series resistance, which limits the ultimate attenuation of $R C$ filters. This SPICE simulation compares ideal (dotted curves) and real (solid curves) cascaded $R C$ lowpass filters.

### 6.2.2 Ideal performance with LC filters

As we pointed out in Chapter 1, filters made with inductors and capacitors can have very sharp responses (§1.7.14). We discussed the parallel $L C$ resonant circuit as an example, as
well as the series $L C$ trap. And we showed a dramatic comparison of an $R C$ and an $L C$ lowpass filter, each with the same 1 MHz cutoff frequency (Figure 1.112). By including inductors in the design, it is possible to create filters with any desired flatness of passband combined with sharpness of transition and steepness of falloff outside the band. Figure 6.5 shows an example of a telephone filter and its stunning bandpass characteristics. ${ }^{2}$

Obviously the inclusion of inductors into the design brings about some magic that cannot be performed without them. In the terminology of network analysis, that magic consists of the use of "off-axis poles" (see Chapter $1 x$ ). Even so, the complexity of the filter increases according to the required flatness of passband and steepness of falloff outside the band, accounting for the large number of components used in the preceding filter. The transient response and phase-shift characteristics are also generally degraded as the amplitude response is improved to approach the ideal brick-wall characteristic.

### 6.2.3 Several simple examples

The impressive Orchard and Sheahan filter of Figure 6.5 is a frighteningly complex design, showing what can be done with sophisticated classic $L C$ filter synthesis. ${ }^{3}$ But you don't have to be a filter wizard to make "good enough" filters ${ }^{4}$ that solve most of the problems you are likely to

[^69]image_name:Figure 6.5 Left
description:
[
name: RS, type: Resistor, value: 10k, ports: {N1: Vin, N2: N1}
name: Inductor1, type: Inductor, value: 97.5, ports: {N1: N1, N2: N2}
name: Capacitor1, type: Capacitor, value: 5725, ports: {Np: Vin, Nn: N1}
name: Capacitor2, type: Capacitor, value: 16, ports: {Np: N1, Nn: N3}
name: Capacitor3, type: Capacitor, value: 16, ports: {Np: N2, Nn: N4}
name: Capacitor4, type: Capacitor, value: 5236, ports: {Np: N3, Nn: N4}
name: Inductor2, type: Inductor, value: 605, ports: {N1: N2, N2: N5}
name: Capacitor5, type: Capacitor, value: 4979, ports: {Np: N4, Nn: N5}
name: Inductor3, type: Inductor, value: 143, ports: {N1: N5, N2: N6}
name: Capacitor6, type: Capacitor, value: 16, ports: {Np: N5, Nn: N7}
name: Capacitor7, type: Capacitor, value: 16, ports: {Np: N6, Nn: N8}
name: Capacitor8, type: Capacitor, value: 5025, ports: {Np: N7, Nn: N8}
name: Inductor4, type: Inductor, value: 583, ports: {N1: N6, N2: N9}
name: Capacitor9, type: Capacitor, value: 5025, ports: {Np: N8, Nn: N9}
name: Inductor5, type: Inductor, value: 143, ports: {N1: N9, N2: N10}
name: Capacitor10, type: Capacitor, value: 16, ports: {Np: N9, Nn: N11}
name: Capacitor11, type: Capacitor, value: 16, ports: {Np: N10, Nn: N12}
name: Capacitor12, type: Capacitor, value: 5236, ports: {Np: N11, Nn: N12}
name: Inductor6, type: Inductor, value: 605, ports: {N1: N10, N2: N13}
name: Capacitor13, type: Capacitor, value: 4979, ports: {Np: N12, Nn: N13}
name: Inductor7, type: Inductor, value: 97.5, ports: {N1: N13, N2: N14}
name: Capacitor14, type: Capacitor, value: 16, ports: {Np: N13, Nn: N15}
name: Capacitor15, type: Capacitor, value: 5725, ports: {Np: N14, Nn: Vout}
name: RL, type: Resistor, value: 10k, ports: {N1: N14, N2: Vout}
]
extrainfo:This circuit is an LC bandpass filter with sharp frequency response characteristics. It consists of multiple inductors and capacitors arranged in a complex network, aimed at filtering specific frequency bands. The resistors RS and RL are used to model the source and load resistances respectively.

image_name:Figure 6.5 Right
description:The graph depicted is a Bode plot showcasing the frequency response of an LC bandpass filter. The x-axis represents frequency in kilohertz (kHz), ranging from 12 kHz to 22 kHz. The y-axis indicates relative attenuation in decibels (dB), spanning from 0 dB to 80 dB.

The overall behavior of the graph is characteristic of a bandpass filter, with a sharp V-shaped curve. The attenuation is highest at the lower and upper frequency extremes and decreases significantly in the mid-frequency range, indicating the passband of the filter.

Key features of the graph include a minimum attenuation point at approximately 17 kHz, where the attenuation approaches 0 dB. This point represents the center frequency or resonance frequency of the filter, where the signal is least attenuated and the filter is most effective at passing signals.

The steep slopes on either side of the resonance frequency indicate a narrow bandwidth, demonstrating the filter's sharp frequency selectivity. The rapid increase in attenuation beyond the passband edges highlights the filter's ability to effectively reject frequencies outside the desired range.

No specific annotations or markers are present on the graph, but the curve's symmetry around the center frequency is evident, illustrating the balanced nature of the bandpass characteristic.

Figure 6.5. Left: An unusually good $L C$ bandpass filter (inductances in mH , capacitances in pF ). Right: measured response of the filter circuit. The admirably sharp frequency response comes at the expense of degraded phase response; see discussion in $\S 6.2 .5$. The 0 dB value in the response curve corresponds to $\sim 9 \mathrm{~dB}$ of loss, assuming 10 k source and load impedances.
encounter. Here we show three simple filters that we used in recent designs at our radiotelescope observatory.

#### A. Sinewave from digital square wave

With digital electronics it is very easy to make and manipulate pulses or square waves of precise frequency. But at our observatory we wanted sine waves, not square waves. Figure 6.6 shows a simple way to produce a sinewave output from a fixed-frequency square wave, namely the use of a tuned series $L C$. It behaves like a very low impedance at resonance ${ }^{5}\left(f_{0}=1 / 2 \pi \sqrt{L C}\right)$, rising on either side (asymptotically as $1 / f$ at low frequencies, and as $f$ at high frequencies).
image_name:Figure 6.6
description:
[
name: HC04, type: Inverter, ports: {In: Vin, Out: N1}
name: 47Ω, type: Resistor, value: 47Ω, ports: {N1: N1, N2: N2}
name: 47pF, type: Capacitor, value: 47pF, ports: {Np: N1, Nn: GND}
name: L1, type: Inductor, value: 100μH, ports: {N1: N2, N2: N3}
name: C1, type: Capacitor, value: 270pF, ports: {Np: N3, Nn: N4}
name: 100Ω, type: Resistor, value: 100Ω, ports: {N1: N4, N2: GND}
name: RL, type: Resistor, value: 50Ω, ports: {N1: N4, N2: GND}
]
extrainfo:The circuit converts a 1.0 MHz square wave into a sine wave using a series LC bandpass filter. The LC filter is tuned to resonate at 1.0 MHz, which allows it to pass the fundamental frequency while attenuating the harmonics. The output is suitable for driving a 50Ω load.

Figure 6.6. A series $L C$ bandpass filter converts a square wave into a sinewave suitable for driving a $50 \Omega$ load.

Here we chose the product $L C$ for resonance at 1.0 MHz , and the value of $L$ such that its impedance at 3 MHz (the next frequency component of a 1 MHz square wave, which has only odd harmonics) is large compared with the $50 \Omega$ load impedance. For $L_{1}=100 \mu \mathrm{H}$, the reactance at 3 MHz is $X_{\mathrm{L}}=2 \pi f L \approx 2 \mathrm{k} \Omega$ 。

Figure 6.7 shows the measured performance. The slight bowing of the square wave is due to loading by the filter

[^70]image_name:Figure 6.7
description:The graph titled 'Figure 6.7' displays a time-domain waveform comparison between the input and output of a series LC bandpass filter. The horizontal axis represents time, with a scale of 400 nanoseconds per division, indicating the temporal behavior of the signals.

**Lower Trace (Input):**
- The lower trace shows the square wave input to the filter, with a vertical scale of 5 volts per division. The waveform is characterized by sharp transitions between high and low voltage levels, typical of a square wave. Each division in the vertical axis represents 5 volts, illustrating the amplitude of the input signal.

**Upper Trace (Output):**
- The upper trace displays the sine wave output of the filter, with a vertical scale of 1 volt per division. The waveform is sinusoidal, indicating that the filter has successfully extracted the fundamental frequency component of the input square wave. The amplitude of the sine wave is smaller compared to the input square wave, as shown by the 1 volt per division scale.

**Overall Behavior and Trends:**
- The transition from a square wave to a sine wave indicates the filter's bandpass characteristics, allowing only the fundamental frequency to pass while attenuating higher harmonics. The slight bowing of the output sine wave, as mentioned in the context, suggests some loading effects by the filter.

**Key Features and Technical Details:**
- The input square wave has sharp edges, while the output sine wave is smooth and periodic, demonstrating the filter's ability to remove high-frequency components. The presence of a 50-ohm load is noted, affecting the output waveform.

**Annotations and Specific Data Points:**
- The graph is annotated with voltage scales for both traces, emphasizing the difference in amplitude between the input and output signals. The annotations also indicate the load condition and the nature of the signals (sine output and square wave input).

Figure 6.7. Input (lower trace) and output (upper trace) of the series $L C$ bandpass (sinewave) filter of Figure 6.6, loaded with $50 \Omega$. Vertical: $1 \mathrm{~V} /$ div (top trace), $5 \mathrm{~V} / \mathrm{div}$ (bottom trace). Horizontal: $400 \mathrm{~ns} / \mathrm{div}$.
and $50 \Omega$ load. We included a simple $R C$ prefilter to slow the rise time, because the very fast edges of the square wave coupled through the parasitic shunt capacitance of the inductor to cause small notches on the sinewave output. The " $3 \times$ 'HC04" designation refers to the type of digital logic component we used; see Chapter 10.

#### B. "Spur" removal

An elegant technique known as phase-locked loop (PLL) frequency synthesis, discussed later in Chapter 13 (§§13.13.6A and 13.13.6B), permits you to generate a desired precise frequency of your choosing, beginning with a standard "reference" frequency, for example 10.0 MHz . Figure 6.8 shows a portion of a 78.0 MHz PLL synthesizer we built, in block diagram form. The basic idea is to use a voltage-tunable oscillator (VCO), and compare an integer subdivision of its desired output frequency with a different subdivision of the reference frequency such that those frequencies will agree when the output frequency is correct. A frequency error produces a correction signal to steer the

VCO toward the correct oscillation frequency. Here we divided the 10 MHz reference by 50 (producing 200 kHz ), to be compared with the VCO's output after division by 390; those divided frequencies will agree when the VCO is oscillating at 78.0 MHz .
image_name:Figure 6.8
description:
[
name: R1, type: Resistor, value: 10k, ports: {N1: φ-detec, N2: loop filter}
name: R2, type: Resistor, value: 20k, ports: {N1: loop filter, N2: C1}
name: C1, type: Capacitor, value: 1µF, ports: {Np: C1, Nn: GND}
name: C2, type: Capacitor, value: 330pF, ports: {Np: loop filter, Nn: L1}
name: L1, type: Inductor, value: 1.8mH, ports: {N1: L1, N2: GND}
]
extrainfo:The circuit is a phase-locked loop (PLL) oscillator with a JFET VCO and a loop filter. The reference frequency is 10 MHz, divided by 50 to 200 kHz, and compared with the VCO output divided by 390. The loop filter consists of R1, R2, and C1, and a 200 kHz trap is formed by C2 and L1.

Figure 6.8. A series LC "trap" suppresses spurs at the 200 kHz reference frequency in this phase-locked loop (PLL) oscillator.

We engineered a simple but quite good JFET oscillator (shown later, in Figure 7.29), with its output energy almost entirely at its central frequency. It was so "clean" that the dominant undesired component of its output was a bit of residual energy at $78.0 \mathrm{MHz} \pm 0.2 \mathrm{MHz}$, caused by the 200 kHz internal comparison frequency. The simple cure here was to put a series $L C$ trap, tuned to 200 kHz , across the analog tuning voltage, as shown. The three other components ( $R_{1} R_{2} C_{1}$ ) form the classic PLL loop filter, as we'll see in §13.13.

#### C. Anti-alias lowpass filter

An analog waveform can be digitized, by sampling its amplitude periodically and converting each sample to a numeric quantity. We'll see later (Chapter 13, e.g., Figure 13.60) that the process can introduce artifacts, both from the finite accuracy with which the amplitudes are quantized, and from the finite rate at which those samples are taken. These artifacts can be suppressed, to any required degree, by adequate choice of quantization depth (amplitude accuracy) and rate (sampling frequency).

The important fact, for this filter example, is that the signal being digitized must not contain signals whose frequency exceeds half the sampling rate $f_{\mathrm{S}}$; this is known as
the Nyquist criterion. ${ }^{6}$ The usual way this is accomplished is by passing the predigitized signals through a lowpass "anti-aliasing" filter, whose cutoff ensures thorough attenuation of signals above the Nyquist frequency $f_{\mathrm{S}} / 2$. This usually requires a sharp filter cutoff, because otherwise you would have to go to a much higher sampling rate to escape signals that pass through the soft cutoff; furthermore you want a filter that is flat throughout the desired signal passband.

In this radiotelescope receiver example (Figure 6.9) we use a mixer (a device that multiplies two signals together to produce its output) to convert a 2 MHz band of signal frequencies centered on 78 MHz (the "IF" band) to a band centered on dc (known as "baseband"). A mixer can do this sort of frequency shifting, because the product of two sinusoids is a pair of waves at the sum and difference frequencies: $\cos \left(\omega_{1} t\right) \cos \left(\omega_{2} t\right)=\frac{1}{2}\left\{\cos \left(\omega_{1}-\omega_{2}\right) t+\right.$ $\left.\cos \left(\omega_{1}+\omega_{2}\right) t\right\}$. Here the signal band drives one input to the mixer, and a fixed oscillator at 78 MHz (the "local oscillator," or LO) drives the other input. The difference frequency at the output of the mixer is the baseband, ${ }^{7}$ in which the band from dc to 1 MHz contains the signals we want to digitize in this example. ${ }^{8}$

Here we amplified the baseband, then passed it through a serious anti-aliasing filter, specifically a " 7 -section $L C$ Chebyshev lowpass filter with 1.0 MHz cutoff frequency and 0.1 dB peak-to-peak ripple."9 We designed the filter with a weird input and output impedance ( $378 \Omega$ ) to take advantage of standard value tunable inductors. The filter removes signal components above 1 MHz , and this filtered baseband is then amplified (again) and digitized (by the device labeled ADC - analog-to-digital-converter) at a sampling rate of 2.5 Msps (megasamples/s). The corresponding Nyquist frequency of 1.25 MHz is well into the stopband of the very sharp lowpass filter; in fact, the calculated and measured performance are in close agreement, demonstrating that the input signals are reduced by 20 dB at that
${ }^{6}$ Violating this rule produces aliasing, the creation, in the digitized output, of nonexistent in-band frequency components; see §13.5.1B.
7 The sum frequency, centered on 156 MHz , is discarded in subsequent filtering.
${ }^{8}$ So we can Fourier transform them to get a radio spectrum. More precisely, the baseband contains frequencies from " -1 MHz " to +1 MHz , which a single mixer folds into a single dc -1 MHz band; but we recover the unfolded baseband by using a pair of mixers, driven with sine and cosine LO signals. The pair of filtered baseband signals, commonly called $I$ and $Q$ (for in-phase and quadrature), are individually digitized to create the complex input time series to the (complex) Discrete Fourier Transform.
${ }^{9}$ This is the filter we used for the linear swept response of Figure 1.112.
image_name:Figure 6.9
description:
[
name: R1, type: Resistor, value: 378, ports: {N1: Node1, N2: Node2}
name: L1, type: Inductor, value: 91.3µH, ports: {N1: Node2, N2: Node3}
name: L2, type: Inductor, value: 101µH, ports: {N1: Node3, N2: Node4}
name: L3, type: Inductor, value: 91.3µH, ports: {N1: Node4, N2: Node5}
name: C1, type: Capacitor, value: 532pF, ports: {N1: Node2, N2: GND}
name: C2, type: Capacitor, value: 944pF, ports: {N1: Node3, N2: GND}
name: C3, type: Capacitor, value: 944pF, ports: {N1: Node4, N2: GND}
name: C4, type: Capacitor, value: 532pF, ports: {N1: Node5, N2: GND}
name: R2, type: Resistor, value: 378, ports: {N1: Node5, N2: GND}
name: ADC, type: Other, ports: {N1: Node5, N2: Output}
]
extrainfo:The circuit diagram shows a 7-section LC lowpass filter designed to prevent aliasing in a radioastronomy receiver by eliminating signal frequencies above 1.25 MHz. The filter uses a Chebyshev design with a 0.1 dB ripple and a cutoff frequency of 1.0 MHz. It is followed by an ADC that digitizes the baseband output at 2.5 Msps.

Figure 6.9. A sharp 7 -section $L C$ lowpass filter prevents aliasing in this radioastronomy receiver by eliminating any signal frequencies above the Nyquist frequency ( 1.25 MHz , or half the sampling rate). We built 126 of these puppies; see the photograph in Figure 1.111.
frequency and that the worst-case aliased signals (at 1.5 MHz ) are reduced by an additional 16 dB . This is stunning performance for a filter that is easily designed and constructed, especially when compared with an $R C$ filter of similar component count, where the attenuation at $1.25 f_{\mathrm{c}}$ is just 1.6 dB relative to that at $f_{\mathrm{c}}$; Figures 6.10 and 6.11 make the comparison graphically.
image_name:Figure 6.10
description:The graph in Figure 6.10 is a Bode plot comparing the frequency response of two different types of 7-pole filters: a Chebyshev filter and an RC filter. The x-axis represents frequency in megahertz (MHz), ranging from 0 to 2 MHz. The y-axis represents the response in decibels (dB), ranging from 0 dB to -60 dB.

The plot features two curves. The first curve, labeled 'Chebyshev 7-pole, 0.1dB,' shows a sharp cutoff characteristic of a Chebyshev filter. It maintains a flat response near 0 dB up to just below 1 MHz, after which it sharply drops, indicating a rapid attenuation of signals beyond the cutoff frequency.

The second curve, labeled 'RC 7-pole,' demonstrates a much softer roll-off compared to the Chebyshev filter. It begins to attenuate more gradually starting below 0.5 MHz and continues to decrease at a slower rate than the Chebyshev filter.

Key features include the steep slope of the Chebyshev filter after 1 MHz, reflecting its abrupt cutoff capability, and the more gradual slope of the RC filter, indicating a softer roll-off. The Chebyshev filter's performance is highlighted by its ability to provide significant attenuation beyond the cutoff frequency compared to the RC filter, which is more gradual in its attenuation.

Figure 6.10. The abrupt cutoff of the 7 -section $L C$ filter of Figure 6.9 compared with the soft rolloff of a 7 -section $R C$ filter with the same 1 MHz cutoff.

#### D. Passive differential filter

Most high-frequency ADCs have differential inputs, see §13.6.2, and many require a low input-signal source impedance, terminated in many cases by a differential capacitor. We discussed low-impedance high-frequency differential-output amplifiers in §5.17, where, for example, Figure 5.102 shows a differential lowpass filter consisting of two $50 \Omega$ resistors and a 100 pF capacitor, as specified for the AD9225 25 MSps ADC (see also Figure 13.28).
image_name:Figure 6.11
description:The graph in Figure 6.11 is a linear frequency response plot comparing two types of filters: an RC 7-pole filter and a Chebyshev 7-pole filter with 0.1 dB ripple. The x-axis represents frequency in megahertz (MHz), ranging from 0 to 2 MHz. The y-axis represents the response in linear scale, ranging from 0 to 1.

**Overall Behavior and Trends:**
- The RC 7-pole filter shows a gradual decrease in response as frequency increases, starting from a normalized response of 1 at 0 MHz and steadily declining past 1 MHz.
- The Chebyshev 7-pole filter, on the other hand, exhibits a small ripple in the passband, with a response starting at 1, showing slight variations around 1 MHz due to the ripple, before a steep decline in response after 1 MHz.

**Key Features and Technical Details:**
- The RC filter maintains a relatively smooth transition with no ripple, indicating a more gentle roll-off characteristic.
- The Chebyshev filter is characterized by its ripple in the passband, which is specified as 0.1 dB. This ripple is visible as small oscillations around the normalized response of 1 before the cutoff frequency.
- Both filters show significant attenuation beyond 1 MHz, with the Chebyshev filter having a sharper roll-off compared to the RC filter.

**Annotations and Specific Data Points:**
- The graph is annotated with labels for each filter type, indicating their characteristics.
- The Chebyshev filter's ripple and sharper cutoff make it suitable for applications requiring a steeper roll-off and minimal passband variation, while the RC filter offers a smoother transition without ripple.

Figure 6.11. The same filter pair of Figure 6.10, here plotted on a linear scale. The Chebyshev's passband "ripple" (of $+0 \mathrm{~dB} /-0.1 \mathrm{~dB}$, or $\pm 0.6 \%$ in amplitude) is more easily seen, but the details of stopband attenuation are lost.

Frequently you'll want an anti-alias filter between the amplifier and the ADC input. For example, if the sampling frequency is 25 MHz , you may want a steep rolloff input filter starting at 10 MHz . Texas Instruments has a nice application note describing how to convert a single-ended filter to differential form (SLWA053B: Design of differential filters for high-speed signal chains, available at www.ti.com).

### 6.2.4 Enter active filters: an overview

The synthesis of filters from passive components ( $R, L$, and $C$ ) is a highly developed subject, with a rich literature of traditional handbooks (e.g., the authoritative work by Zverev; see Appendix N), now supplemented by elegant software tools that make such designs a routine task. However, inductors as circuit elements frequently leave much to be desired. They are often bulky and expensive, and they depart from the ideal by being "lossy," i.e., by having
significant series resistance, as well as other "pathologies" such as nonlinearity, distributed winding capacitance, and susceptibility to magnetic pickup of interference. Furthermore, the inductances needed for low-frequency filters may dictate unmanageably large components. Finally, classic filters made with $L$ 's and $C$ 's are not electrically tunable.

What is needed is a way to make inductorless filters with the characteristics of ideal RLC filters. Ideally we might hope for tunability, either by an analog tuning voltage or a varying pulse frequency.

By using op-amps as part of the filter design, we can synthesize any RLC filter characteristic without using inductors. Such inductorless filters are known as active filters because of the inclusion of an active element (the amplifier). We'll see another class of active filter - the switched capacitor filter - that adds MOSFET switches to produce, in effect, a frequency-tunable resistor. These deliver performance similar to that of the standard active filter (sometimes called a "continuous-time" filter), but with the added feature of precise tuning of its characteristic frequency breakpoints (with an externally applied clocking frequency) over a wide range. (This tunability comes at a price, though, namely some switching noise and a reduced dynamic range; see §6.3.6.)

Active filters can be used to make lowpass, highpass, bandpass, and band-reject filters, with a choice of filter types according to the important features of the response, e.g., maximal flatness of passband, steepness of skirts, or uniformity of time delay versus frequency (more on this shortly). In addition, "allpass filters" with flat amplitude response but tailored phase versus frequency can be made (they're also known as "delay equalizers"), as well as the opposite - a filter with constant phase shift but tailored amplitude response.

#### A. Negative-impedance converter, gyrator, and generalized impedance converter

Three interesting circuit elements that should be mentioned in any overview are the negative-impedance converter (NIC), the gyrator, and the generalized impedance converter ${ }^{10}$ (GIC). These devices can mimic the properties of inductors while using only resistors and capacitors in addition to op-amps.

Once you can do that, you can build inductorless filters with the ideal properties of any RLC filter, thus providing at least one way to make active filters.

[^71]
#### B. Negative-impedance converter

The NIC converts an impedance to its negative, whereas the gyrator converts an impedance to its inverse. The following exercises will help you discover for yourself how that works out.

Exercise 6.1. Show that the circuit in Figure 6.12 is a negativeimpedance converter, in particular that $Z_{\text {in }}=-Z$. Hint: apply some input voltage $V$ and compute the input current $I$. Then take the ratio to find $Z_{\text {in }}=V / I$.
image_name:Figure 6.12
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Zin, InN: InN, OutP: Out, OutN:}
name: R1, type: Resistor, value: R, ports: {N1: InP, N2: Out}
name: R2, type: Resistor, value: R, ports: {N1: Out, N2: InN}
name: Z, type: Other, ports: {N1: InN, N2: GND}
]
extrainfo:The circuit is a negative-impedance converter (NIC), which converts an impedance to its negative. The input impedance Zin is equal to -Z. The circuit uses an operational amplifier (A1) and two resistors (R) to achieve this conversion.

Figure 6.12. Negative-impedance converter.
The NIC therefore converts a capacitor to a "backward" inductor:

$$
\begin{equation*}
Z_{\mathrm{C}}=1 / j \omega C \rightarrow Z_{\text {in }}=j / \omega C, \tag{6.1}
\end{equation*}
$$

i.e., it is inductive in the sense of generating a current that lags the applied voltage, but its impedance has the wrong frequency dependence (it goes down, instead of up, with increasing frequency).

#### C. Gyrator

The gyrator, on the other hand, converts a capacitor to a true inductor:

$$
\begin{equation*}
Z_{\mathrm{C}}=1 / j \omega C \rightarrow Z_{\text {in }}=j \omega C R^{2} \tag{6.2}
\end{equation*}
$$

i.e., an inductor with inductance $L=C R^{2}$.
image_name:Figure 6.13
description:
[
name: NIC1, type: Other, ports: {N1: Vin, N2: N1}
name: R1, type: Resistor, value: R, ports: {N1: N1, N2: N2}
name: R2, type: Resistor, value: R, ports: {N1: N2, N2: N3}
name: NIC2, type: Other, ports: {N1: N3, N2: GND}
name: R3, type: Resistor, value: R, ports: {N1: N3, N2: GND}
name: Z, type: Other, ports: {N1: N3, N2: GND}
]
extrainfo:The circuit diagram represents a gyrator configuration using Negative Impedance Converters (NICs) to simulate inductance. The input impedance is given by Zin = R^2/Z, indicating the transformation of the impedance Z through the gyrator configuration.

Figure 6.13. Gyrator implemented with NICs.
The existence of the gyrator makes it intuitively reasonable that inductorless filters can be built to mimic any filter
using inductors by simply replacing each inductor with a gyrated capacitor. ${ }^{11}$ The use of gyrators in just that manner is perfectly OK ; and in fact the telephone filter illustrated previously, though designed as a classic $L C$ filter, was implemented with gyrators (in a configuration known as a Riordan gyrator, which looks different from Figure 6.13). In addition to simple gyrator substitution into pre-existing RLC designs, it is possible to synthesize many other filter configurations.

Exercise 6.2. Show that the circuit in Figure 6.13 is a gyrator, in particular that $Z_{\text {in }}=R^{2} / Z$. Hint: you can analyze it as a set of voltage dividers, beginning at the right.

#### D. Generalized impedance converter

The configuration of Figure 6.14 is known as a generalized impedance converter ${ }^{12}$ (GIC); it multiplies the impedance attached at $Z_{5}$ by the factor $Z_{1} Z_{3} / Z_{2} Z_{4}$. So, for example, if you put a capacitor at $Z_{4}$, and resistors everywhere else, you get an inductor whose value is $L=\left(R_{1} R_{3} R_{5} / R_{2}\right) C$; that is, it becomes a gyrator. But you can do more amusing things with a GIC: for example, if you put capacitors at $Z_{3}$ and $Z_{5}$, you wind up with a frequency-dependent negative resistor (FDNR). Filter implementations with GICimplemented FDNRs have been popular in the audio design field, where it is claimed that they have superior noise and distortion characteristics compared with something like a Sallen-and-Key filter (next section). The field of inductorless filter design is both lively and rich with detail, with new designs appearing in the journals every month.

#### Performance limits

As with any op-amp circuit, the performance of gyrators and GICs at high frequencies depends on the op-amp's bandwidth (and other characteristics). So a GIC configured as an inductor (capacitor at $Z_{4}$, resistors elsewhere) will stop looking like an inductor at frequencies greater than a few percent of the op-amp's bandwidth $f_{\mathrm{T}}$. The simulation results in Figure 6.15 show the kind of behavior you'll see. Roughly speaking, the nearly perfect inductor (at low frequencies) becomes something approximating a capacitor at high frequencies, with a resonance in between. ${ }^{13}$ This may look ugly, on this extended graph; but notice that the "inductor" appears to have an astonishingly high quality factor

[^72]image_name:Figure 6.14
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Out(A2), InN: Out(A1), OutP: Out(A1), OutN:}
name: A2, type: OpAmp, value: A2, ports: {InP: InP(A2), InN: Out(A1), Out: Out(A2)}
name: Z1, type: Resistor, value: Z1, ports: {N1: InP(A1), N2: Out(A2)}
name: Z2, type: Resistor, value: Z2, ports: {N1: Out(A2), N2: Out(A1)}
name: Z3, type: Resistor, value: Z3, ports: {N1: Out(A1), N2: InP(A2)}
name: Z4, type: Capacitor, value: Z4, ports: {Np: InP(A2), Nn: GND}
name: Z5, type: Resistor, value: Z5, ports: {N1: InP(A1), N2: GND}
]
extrainfo:This is a generalized impedance converter circuit. The circuit behaves like an inductor if Z4 is a capacitor and the rest are resistors. The inductance value is given by the formula L = (Z1 * Z3 * Z5 * C4) / Z2.

Figure 6.14. Generalized impedance converter. If $Z_{4}$ is a capacitor, the circuit behaves like an inductor, with value as shown. From A. Antoniou, IEE Proc., 116, 1838-1850 (1969).
$Q$ of about $2 \times 10^{5}$ at 1 kHz if you assume that the $4.6 \mathrm{~m} \Omega$ impedance floor on the graph properly represents the inductor's loss (i.e., equivalent series resistance, ESR). (In reality there are other losses, so realizable $Q$ values are in the range of $1000 \ldots$ still pretty darn good for an inductor that's a fraction of a henry !). And, for the highest-bandwidth op$\mathrm{amp}\left(f_{\mathrm{T}}=50 \mathrm{MHz}\right.$ ) the capacitance is just 2.3 pF ; you could never make a 160 mH inductor with such a tiny "winding capacitance," nor with such a high self-resonant frequency.

Gyrators are used in real-world filters: in an App Note, Texas Instruments suggests using multiple GIC stages to make anti-alias filters. ${ }^{14}$ And Stanford Research Systems uses four GIC stages acting as an $R+L C$ ladder to make an 8-zero 9-pole elliptical lowpass filter for their SR830 DSPbased lock-in amplifier, "so that all frequency components greater than half the sampling frequency are attenuated by at least 96 dB ." The A/D samples at 256 kHz and the filter passes signals from dc to 102 kHz ; they've allowed themselves a $25 \%$ frequency margin to get the attenuation down to $96 \mathrm{~dB} .{ }^{15}$ The full schematic of the filter is included in the

[^73]image_name:Figure 6.15
description:The graph is a Bode plot showing the impedance (Z) in ohms on the vertical axis against frequency in hertz on the horizontal axis. The vertical axis is logarithmic, ranging from 10 ohms to 1 megaohm, while the horizontal axis is also logarithmic, spanning from 10 Hz to 1 MHz.

Overall Behavior and Trends:
- **Inductive Region:** Starting from a low frequency, the impedance is initially inductive. At 1 kHz, the quality factor (Q) is approximately 1000, and the graph indicates an inductive behavior with an impedance around 159 mH.
- **Resonant Peaks:** The graph exhibits several resonant peaks at 17 kHz, 56 kHz, and 262 kHz, where the impedance sharply increases. These peaks suggest resonant frequencies where the circuit's impedance is maximized.
- **Capacitive Region:** Beyond the last peak at 262 kHz, the impedance begins to decrease, indicating a capacitive behavior. This transition is marked by a change in slope and a noted frequency of 410 kHz.

Key Features and Technical Details:
- **Resonant Frequencies and Peaks:**
- **17 kHz:** This is the first noted peak, suggesting a significant increase in impedance at this frequency.
- **56 kHz:** A second peak occurs, marked by another sharp rise in impedance.
- **262 kHz:** The highest peak is observed here, indicating a major resonant frequency.
- **Self-Resonant Frequencies (f<sub>r</sub>):**
- At 262 kHz, the plot indicates self-resonant frequencies with corresponding capacitances:
- **f<sub>r</sub> = 50 MHz, ~2.3 pF**
- **f<sub>r</sub> = 5 MHz, ~500 pF**
- **f<sub>r</sub> = 0.5 MHz, ~500 pF**

Annotations and Specific Data Points:
- **Damping with Series R:** The plot suggests using a series resistor to dampen the resonant peaks.
- **Transition to Capacitive Behavior:** Marked at 410 kHz, the circuit transitions from inductive to capacitive, with the impedance dropping off.
- **Initial Impedance:** The graph starts at an impedance of 4.6 mΩ at very low frequencies.

This Bode plot effectively illustrates the transition from inductive to capacitive behavior in the circuit, with key resonant frequencies and the impact of finite op-amp bandwidth on the impedance characteristics.

Figure 6.15. Finite op-amp bandwidth degrades the ideal GIC inductor, which becomes capacitive at frequencies beginning at a small fraction of $f_{\mathrm{T}}$, as seen in these plots derived from SPICE simulations. When compared with a physical inductor, with its winding capacitance and self-resonant frequency, the GIC inductor's analogous capacitance and self-resonant frequency (which depend on the op-amp's bandwidth) can be significantly better, as suggested in these plots (which, however, are predicated on the use of an ideal capacitor).
instrument's wonderfully informative manual - a hallmark of all SRS products.

#### E. Sallen-and-Key filter

Figure 6.16 shows an example of a simple and even partly intuitive filter topology, an example of which we saw earlier in §4.3.6. These are known as Sallen-and-Key filters, after the inventors. ${ }^{16}$ The unity-gain amplifier can be an op-amp connected as a follower, or just an emitter follower or source follower. The particular filters shown are 2-pole lowpass and highpass filters. Taking the example of the lowpass filter (Figure 6.16A), note that it would be simply two cascaded $R C$ lowpass filter sections, except for the fact that the bottom of the first capacitor is bootstrapped by the output. It is easy to see that at very high frequencies it falls off just like a cascaded $R C$, because the output is essentially

[^74]zero. As the output rises at decreasing frequency, however, the bootstrap action tends to reduce the attenuation, giving a sharper knee. Of course, such hand-waving cannot substitute for honest analysis, which luckily has already been done for a prodigious variety of nice filters. We will come back to active filter circuits in $\S 6.3$, after a short introduction to filter performance parameters and filter types.
image_name:A. lowpass
description:
[
name: R1, type: Resistor, value: R, ports: {N1: input, N2: X1}
name: R2, type: Resistor, value: R, ports: {N1: X1, N2: In}
name: C1, type: Capacitor, value: C, ports: {Np: X1, Nn: GND}
name: C2, type: Capacitor, value: C, ports: {Np: In, Nn: GND}
name: A1, type: OpAmp, value: +1, ports: {InP: In, InN: GND, OutP: output}
]
extrainfo:This is a Sallen-and-Key lowpass filter circuit. It uses resistors and capacitors to create a frequency-dependent network, and an operational amplifier to buffer the output.
image_name:B. highpass
description:
[
name: C1, type: Capacitor, value: C, ports: {Np: LOAD1, Nn: X1}
name: R1, type: Resistor, value: R, ports: {N1: X1, N2: GND}
name: C2, type: Capacitor, value: C, ports: {Np: X1, Nn: In}
name: R2, type: Resistor, value: R, ports: {N1: In, N2: GND}
name: A1, type: OpAmp, value: +1, ports: {InP: In, InN: GND, Out: Out}
name: Load1, type: Other, ports: {N1: LOAD1, N2: GND}
name: Load2, type: Other, ports: {N1: Out, N2: GND}
]
extrainfo:This is a Sallen-and-Key highpass filter configuration. The circuit includes two capacitors and two resistors forming the filter, with an operational amplifier providing feedback.

Figure 6.16. Sallen-and-Key lowpass and highpass active filters. The ultimate performance of these simple-looking filters is affected by the non-zero output impedance of the follower, see Figure 6.36.

### 6.2.5 Key filter performance criteria

There are some standard terms that keep appearing when we talk about filters and try to specify their performance. It is worth getting it all straight at the beginning.

#### A. Frequency domain

The most obvious characteristic of a filter is its gain versus frequency, typified by the sort of lowpass characteristic shown in Figure 6.17.

The passband is the region of frequencies that are relatively unattenuated by the filter. Most often the passband is considered to extend to the -3 dB point, but with certain filters (most notably the "equiripple" types) the end of the passband may be defined somewhat differently. Within the passband the response may show variations or ripples, defining a ripple band, as shown. The cutoff frequency, $f_{c}$, is the end of the passband. The response of the filter then drops off through a transition region (also colorfully known as the skirt of the filter's response) to a stopband, the region of significant attenuation. The stopband may be defined by some minimum attenuation, e.g., 40 dB .

Along with the gain response, the other parameter of importance in the frequency domain is the phase shift of the
image_name:A.
description:The graph labeled "A" is a Bode plot illustrating the frequency response of a filter. It is a log-log plot with the x-axis representing the logarithm of frequency and the y-axis representing the logarithm of gain.

1. **Axes Labels and Units:**
- The x-axis is labeled "log frequency," indicating a logarithmic scale for frequency.
- The y-axis is labeled "log gain," also indicating a logarithmic scale for gain.

2. **Overall Behavior and Trends:**
- The graph shows three main regions: the passband, the transition region (skirt), and the stopband.
- In the passband, the gain is relatively constant but exhibits a ripple effect, forming a ripple band.
- At the cutoff frequency \( f_c \), the gain begins to decrease sharply, marking the start of the transition region.
- Beyond the transition region, the graph enters the stopband, where the gain is significantly attenuated.

3. **Key Features and Technical Details:**
- **Passband:** The region where the gain is nearly constant but with small oscillations due to ripples.
- **Ripple Band:** The vertical extent of these oscillations.
- **Cutoff Frequency \( f_c \):** The frequency at which the gain starts to drop off sharply.
- **Transition Region (Skirt):** The area between the passband and stopband where the gain decreases.
- **Stopband:** The region of significant attenuation, where the gain remains low.

4. **Annotations and Specific Data Points:**
- The cutoff frequency \( f_c \) is marked on the graph.
- The ripple band and transition region are annotated to highlight their significance in the filter's response.
image_name:B.
description:The graph labeled 'B' is a plot of Phase Shift versus Frequency. It is a linear graph, meaning both axes are scaled linearly. The x-axis represents frequency in a linear scale, while the y-axis represents phase shift.

Overall Behavior and Trends:
- **General Shape:** The graph shows a non-linear increase in phase shift as the frequency increases.
- **Trends:** Initially, at lower frequencies, the phase shift is minimal. As the frequency increases, the phase shift begins to rise more sharply, indicating a positive correlation between frequency and phase shift.

Key Features and Technical Details:
- **Initial Phase Shift:** At low frequencies, the phase shift starts near zero.
- **Increasing Phase Shift:** As frequency increases, the phase shift increases at an accelerating rate.
- **No Oscillations or Peaks:** The graph does not exhibit oscillations or peaks; it is a smooth, continuous curve.

Annotations and Specific Data Points:
- There are no specific markers or annotations such as cutoff frequencies or phase margins indicated on this graph.

This graph is useful for understanding how the phase shift of a system changes with frequency, which is crucial in filter design and analysis to ensure signal integrity and minimal distortion.
image_name:C.
description:The graph labeled 'C' is a plot of Time Delay versus Frequency. This graph is presented on a linear scale for both axes. The x-axis represents frequency, measured in a linear scale, while the y-axis represents time delay.

Overall Behavior and Trends:
The graph displays a non-linear relationship between frequency and time delay. Initially, as frequency increases, the time delay remains relatively constant. This indicates that at lower frequencies, the time delay is stable. However, as the frequency continues to increase, the time delay exhibits a peak, suggesting a region where the delay is maximized. Following this peak, the time delay decreases, indicating that at higher frequencies, the delay reduces.

Key Features and Technical Details:
- **Initial Constant Delay:** At lower frequencies, the time delay is stable and shows little change.
- **Peak:** There is a noticeable peak in the time delay at a certain frequency, indicating a maximum delay.
- **Decreasing Delay:** After the peak, the time delay decreases as frequency continues to increase.

Annotations and Specific Data Points:
There are no specific numerical values or annotations provided on the graph, but the behavior suggests a typical characteristic of certain filters where time delay varies with frequency.

Figure 6.17. Filter characteristics versus frequency.
output signal relative to the input signal. In other words, we are interested in the complex response of the filter, which usually goes by the name of $\mathbf{H}(\mathbf{s})$, where $\mathbf{s}=j \omega$, and $\mathbf{H}$ and $\mathbf{s}$ are complex. Phase is important because a signal entirely within the passband of a filter will emerge with its waveform distorted if the time delay of different frequencies in going through the filter is not constant. Constant time delay corresponds to a phase shift increasing linearly with frequency ( $\Delta t=-d \phi / d \omega=-\frac{1}{2 \pi} d \phi / d f$ ); hence the term linear-phase filter applied to a filter that is ideal in this respect. Figure 6.18 shows a typical graph of amplitude response and phase shift for a lowpass filter that is definitely not a linear-phase filter. Graphs of phase shift versus frequency are best plotted on a linear frequency axis.

#### B. Time domain

As with any ac circuit, filters can be described in terms of their time-domain properties: rise time, overshoot, ringing, and settling time. This is of particular importance where steps or pulses may be present. Figure 6.19 shows a typical lowpass-filter step response. Here, rise time is, as usual, the time required to go from $10 \%$ to $90 \%$ of the final value. Of greater interest is the settling time, which is the time required to get within some specified amount of the final value and stay there. The delay time is the time duration from the input step to the output reaching
image_name:Figure 6.18
description:The graph in Figure 6.18 is a dual-axis plot representing the amplitude response and phase shift of an 8-pole Chebyshev lowpass filter with a 2 dB passband ripple.

**Type of Graph and Function:**
This is a frequency response graph, showing both amplitude and phase characteristics of the filter.

**Axes Labels and Units:**
- The x-axis is labeled 'Normalized Frequency' and uses a linear scale ranging from 0 to 2.
- The left y-axis is labeled 'Amplitude Response' on a linear scale ranging from 0 to 1.0.
- The right y-axis is labeled 'Phase Shift' with units in radians, ranging from 0 to 4π.

**Overall Behavior and Trends:**
- The amplitude response starts at 1.0 at a normalized frequency of 0 and exhibits oscillations (ripples) as the frequency increases, characteristic of the Chebyshev filter's passband ripple.
- The amplitude decreases sharply after the cutoff frequency, indicating the transition to the stopband.
- The phase response starts at 0 radians and increases gradually, then drops sharply around the cutoff frequency, eventually stabilizing around 4π radians.

**Key Features and Technical Details:**
- The ripple in the amplitude response is due to the 2 dB passband ripple specification, which is typical for Chebyshev filters.
- The cutoff frequency is where the amplitude response leaves the ripple band and begins to decrease sharply.
- The phase shift shows a significant change around the cutoff frequency, a common trait in filter phase responses.

**Annotations and Specific Data Points:**
- The amplitude response curve is marked with 'amplitude,' and the phase response curve is marked with 'phase.'
- There are no specific numerical values marked for cutoff frequencies or other critical points, but the behavior is consistent with typical Chebyshev filter characteristics.

Figure 6.18. Phase shift (lagging) and amplitude response for an 8 -pole Chebyshev lowpass filter ( 2 dB passband ripple). The normalization shown is conventional: 0 dB corresponds to the top of the ripple band, and the cutoff (or "critical") frequency is the frequency at which the response leaves the ripple band. The filter's actual dc gain is unity ( 0 dB ); for even-order filters (like this one) the ripple rises from dc, whereas for odd-order filters the ripple drops from dc.
$50 \%$ of its final value. ${ }^{17}$ Overshoot and ringing are selfexplanatory terms for some undesirable properties of filters. The phase-shifting characteristics of filters imply a corresponding time delay, which you sometimes see plotted (or tabulated) as group delay versus frequency. ${ }^{18}$

### 6.2.6 Filter types

Suppose you want a lowpass filter with flat passband and sharp transition to the stopband. The ultimate rate of falloff, well into the stopband, will always be $6 \mathrm{ndB} /$ octave, where $n$ is the number of "poles." You need one capacitor (or inductor) for each pole, so the required ultimate rate of falloff of filter response determines, roughly, the complexity of the filter.

Now, assume that you have decided to use a 6-pole lowpass filter. You are guaranteed an ultimate rolloff of $36 \mathrm{~dB} /$ octave at high frequencies. It turns out that the filter design can now be optimized for maximum flatness of passband response, at the expense of a slow transition from passband to stopband. Alternatively, by allowing some

[^75]
[^0]:    ${ }^{14}$ Assuming care is taken in the wiring layout to maintain the low 0.2 pF capacitance of the HOLD signal.

[^1]:    ${ }^{15}$ Making this quantitative, the LF412's maximum quiescent current is 6.5 mA , thus 195 mW dissipation when run from $\pm 15 \mathrm{~V}$ supplies. In a DIP-8 package that produces a $22^{\circ} \mathrm{C}$ temperature rise (the thermal resistance $\left.R_{\Theta J A}=115^{\circ} \mathrm{C} / \mathrm{W}\right)$, with a consequent quadrupling of the specified $I_{\mathrm{B}}=200 \mathrm{pA}$ (max). If the op-amp were driving a load, you'd have yet more dissipation. To put this in perspective, though, note that the driving impedance seen at the op-amp's input would have to be greater than $1 \mathrm{M} \Omega$ in order for this current-induced error to exceed the 1 mV (typ) input offset-voltage error.

[^2]:    ${ }^{16}$ In the previous edition of this book we awarded that honor to the MAX400M, with its specified worst-case $V_{\text {OS }}$ of $10 \mu \mathrm{~V}$. With confi-

[^3]:    dence we added that "we expect to see further incremental improvements in this area." That confidence was evidently misplaced: the Maxim website now says of the MAX400 "This product was manufactured for Maxim by an outside wafer foundry using a process that is no longer available. It is not recommended for new designs. The datasheet remains available for existing users." Sic transit...

[^4]:    ${ }^{17}$ In fact, if noise is of primary concern you could substitute the $\times 4$ quieter INA103 instrumentation amplifier at the front-end, paying the price in input offset current: a whopping $1 \mu \mathrm{~A}$ (thus $\pm 350 \mu \mathrm{~V}$ ) of static offset voltage created by the $350 \Omega$ differential source resistance here.

[^5]:    18 We've simplified it slightly: the input stage of Widlar's original LM101 used a pnp differential pair, but it was configured as a common-base amplifier driven by an $n p n$ follower pair.

[^6]:    ${ }^{19}$ National Semiconductor App Note AN-1485: The Effect of Heavy Loads on the Accuracy and Linearity of Operational Amplifier Circuits

[^7]:    ${ }^{20}$ See "Active Feedback Improves Amplifier Phase Accuracy," by J. Wong, EDN Magazine, 17 Sept 1987; reprinted as Analog Devices AN-107. Wong credits the idea to Soliman in a 1979 paper, and Soliman credits the idea to Brackett and Sedra in a 1976 paper. But Wong's paper is the most useful reference for understanding the configuration of Figure 5.25.
${ }^{21}$ In SPICE simulations we found that the peaking increased to $\sim 7 \mathrm{~dB}$ for the LF412 model configured for $G=2$; this can be tamed by adding a compensation capacitor $C_{c}$ across feedback resistor $R_{2}$. Choosing $C_{c}$ to match the op-amp's $f_{\mathrm{T}}$ (i.e., $C_{c}=1 / 2 \pi f_{\mathrm{T}} R_{2}$ ) reduced the peaking to 4 dB , at the expense of tripling the (pretty small) phase error. In his article, James Wong warns that the technique may result in an unstable amplifier for low gains, below $G=5$ for example. He shows also how the technique can be further improved if $A_{2}$ is made from two amplifiers.

[^8]:    22 We went back to the bench and measured a handful of LF412 dual opamps. Among different specimens the $f_{\mathrm{T}}$ values ranged over $\pm 20 \%$, but within any single part the $f_{\mathrm{T}}$ 's of its two op-amps matched typically to $0.1 \%$, with one outlier showing a $1.5 \%$ mismatch.

[^9]:    ${ }^{23}$ Or sometimes called "double-terminated", as in Figure 12.110. We suggest trying your amplifier of choice, taking care to terminate the second op-amp with $150 \Omega$.

[^10]:    ${ }^{24}$ Playfully named "Zer $\varnothing$-Crossover" amplifiers, or ZCOs.

[^11]:    ${ }^{27}$ It's unusual to see plots (or even tabulated values) of open-loop output impedance on datasheets; and in cases where a graph is shown, it rarely extends to very low frequencies. It is likely that other op-amps, including some with conventional (follower) output stages, also exhibit a rise in open-loop output impedance at very low frequencies. This is rarely of concern, though, owing to the very high loop gain down there.

[^12]:    ${ }^{30}$ In $\S 8.6 .3$ we show a discrete op-amp circuit where both of these goals are achieved.

[^13]:    ${ }^{31}$ A phrase lifted from a student's reply in an end-of-course questionnaire: "This course was not superficial enough for me."
32 There was traditionally a problem peculiar to MOSFETs, which has been largely solved through process improvements. MOS transistors

[^14]:    are susceptible to a unique debilitating effect that neither FETs nor bipolar transistors have. It turns out that sodium-ion impurity migration and/or phosphorus polarization effects in the gate insulating layer can cause offset voltage drifts under closed-loop conditions, in extreme cases as much as 0.5 mV over a period of years. The effect is increased for elevated temperatures and for a large applied differential-input signal, with some datasheets showing a typical 5 mV change of $V_{\mathrm{OS}}$ over 3000 hours of operation at $125^{\circ} \mathrm{C}$ with 2 V across the input. This sodium-ion disease can be alleviated by introducing phosphorus into the gate region. Texas Instruments, for example, uses a phosphorusdoped polysilicon gate in its "LinCMOS" series of op-amps (TLC270series) and comparators (TLC339 and TLC370-series). These popular inexpensive parts come in a variety of packages and speed/power selections and maintain respectable offset voltages with time ( $50 \mu \mathrm{~V}$ eventual offset drift per volt of differential input).

[^15]:    ${ }^{33}$ Many op-amps can do this, but without saying so. That's because their pullup transistor and drivers work all the way down to the negative

[^16]:    rail, without sourcing current to the output. Some require a minimum pull-down current, e.g., 0.5 mA for the OPA364.

[^17]:    ${ }^{35}$ Well, not exactly: if the noise power density were truly to continue rising as $1 / f$, the integral would diverge at zero frequency (dc). For Figure 5.54 we set the low frequency limit to be 0.01 Hz .
${ }^{36}$ How to determine the corner frequency? See the discussion in §8.13.4.
${ }^{37}$ The LT1012 and OPA277 are BJT parts, and the TLC2272 is a CMOS op-amp. The ' 2272 boasts a miniscule 60 pA max bias current, far better than the '277's 1 nA , but not much better than the '1012's amazing 100 pA .

[^18]:    38 Note 13 on the LMC6482 datasheet says "Guaranteed limits are dictated by tester limitations and not device performance. Actual performance is reflected in the typical value." That's illuminating, but not entirely helpful for the designer of a mass-production instrument.

[^19]:    ${ }^{39}$ Based on nice techniques worked out by Paul Grohe and Bob Pease at National Semiconductor. See Paul Rako's article "Measuring Nanoamperes" (EDN, 26 April 2007), and two riffs by Pease from his series in Electronic Design: "What's All This Teflon Stuff, Anyhow?" (14 Feb 1991) and "What's All This Femtoampere Stuff, Anyhow" (2 Sept 1993). Nicely readable versions currently available at http://electronicdesign.com/ test-amp-measurement/whats-all-teflon-stuff-anyhow and.../whats-all-femtoampere-stuff-anyhow.

[^20]:    ${ }^{40}$ The LT1677 listed in Table 8.3a is an exception. Its datasheet has a graph labelled "Input Bias Current Over the Common Mode Range," showing that the bottom 1.4 V and top 0.7 V of the common-mode range suffer from high bias currents. The op-amp's offset voltage is also degraded in these regions. But, hey, we warned you about that in §5.9.1!

[^21]:    ${ }^{41}$ Datasheets for the closely similar OP-97 and LT1097 make the same error, evidently corrected in that of the later LT6010 (the recommended successor to the LT1012).

[^22]:    42 Three-legged, or four? We've found that city folks don't know why it is that milking stools have three legs, whereas barstools have four. Those with rural upbringing can tell you, in a flash.

[^23]:    ${ }^{43}$ Yeah, OK, but read carefully: on page 10 of the datasheet you'll see that there are $\sim 1 \mathrm{mV}$ shifts of offset voltage when the input is within 1.5 V of the rail! A powerful incentive to use inverting mode!

[^24]:    ${ }^{44}$ Manufacturers use different voltage levels ( $2 \mathrm{Vpp}, 3 \mathrm{Vrms}, 10 \mathrm{~V}$ peak, and 20 Vpp ), different loads ( $100 \Omega, 600 \Omega, 2 \mathrm{k}, 10 \mathrm{k}$ and open circuit), different common-mode voltages, different analyzer filters, and even different gains for their measurements.

[^25]:    ${ }^{45} \mathrm{OK}$, we plead guilty-as-charged to that conclusion favored by all academics - "needs more study (and a grant proposal is in the mail)."

[^26]:    ${ }^{46}$ If you're considering piezo positioners for a precision application, be aware that they exhibit some nonlinearity and hysteresis when driven from a voltage source. These issues are said to be ameliorated when the drive signal is quantified by charge instead of voltage. See Chapter $3 x$ for a precision current-drive circuit that circumvents this problem and makes fast linear piezo steps.

[^27]:    47 Unlike an earlier generation of synchronous amplifiers that were also called "chopper amplifiers," but that had bandwidth limited to a fraction of the chopping clock frequency.

[^28]:    ${ }^{48}$ Some old high-voltage types that require external (correction-signal) capacitors may still be available.

[^29]:    52 Some parts warn that for high source impedances the bias current may change dramatically as a function of input capacitance! For example, the input current of an LMP2021 with $R_{\mathrm{S}}=1 \mathrm{G} \Omega$ varies from -25 to +25 pA for an input shunt capacitance $C_{\mathrm{s}}$ ranging from 2 to 500 pF . Note that such input currents create large offsets with such high source resistances: 25 pA into $1 \mathrm{G} \Omega$ is 25 mV . A graph in the datasheet shows that the input current $I_{\mathrm{B}}$ goes through zero for $C_{\mathrm{S}}=22 \mathrm{pF}$. Other manufacturer's parts show similar effects. In a transimpedance amplifier with high $R_{\mathrm{F}}$, using a large feedback capacitor $C_{\mathrm{F}}$ can dramatically reduce the bias-current error.

[^30]:    ${ }^{54}$ At 10 Hz , who knows about higher frequencies?!
${ }^{55}$ The curious part number reminds us old timers of a favorite vacuum tube of yesteryear.

[^31]:    ${ }^{56}$ In the good ol' days, manufacturers proudly published their circuits. Nowadays it's far less common - for example, circuit diagrams are absent from the service manual for the Agilent 34410A (successor to the 34401A). Happily, some manufacturers (e.g., Stanford Research Systems) continue to display their circuit ingenuity, with full schematics and parts lists.
57 A further trick is to average many such calibrate-measure cycles (up to 2 minutes' worth, in the 34420A) to beat down the scatter.

[^32]:    58 All have $20 \%$ "overrange," e.g., $\pm 12 \mathrm{~V}$ on the " 10 V " range.

[^33]:    ${ }^{59}$ It's necessary that $Q_{1}$ 's $V_{\mathrm{GS}}$ at 0.7 mA be less than $Q_{2}$ 's $V_{\mathrm{GS}}$ at 1.4 mA , because the difference is $Q_{1}$ 's $V_{\mathrm{DS}}$ operating voltage. It's likely that Agilent has an incoming batch inspection to ensure that this condition is met.

[^34]:    ${ }^{60}$ For single-ended amplifiers we would want the current-source noise $i_{\mathrm{n}}$ to be less than $e_{\mathrm{n}}(\mathrm{amp}) g_{m}$. We can use the expression $e_{\mathrm{n}}(\mathrm{ref}) / e_{\mathrm{n}}(\mathrm{amp})=g_{m} R_{\mathrm{S}}$ to determine the allowable voltage noise in the current-source reference. For this circuit that ratio is 37 , thus only $11 \mathrm{nV} / \sqrt{\mathrm{Hz}}$ for a noise contribution comparable to that of the $0.3 \mathrm{nV} / \sqrt{\mathrm{Hz}} \mathrm{JFET}$. The MC1403 reference is about $20 \times$ worse than this. Evidently the Agilent engineers are relying on the matched noise currents in the two JFETs to cancel to better than 5\%, enforced by the $1 \%$ current-mirror resistors. At frequencies above about 10 Hz , however, the 10 nF capacitor defeats this cancellation.

[^35]:    ${ }^{61}$ We'll see the strain gauge again, in connection with analog-to-digital converters, in §13.9.11C (Figure 13.67). A similar biased bridge arrangement is used in the platinum resistance temperature detector (RTD), which is the sensor used in the microcontroller-based thermal controller in $\S 15.6$.

[^36]:    ${ }^{62}$ You can define an effective current-source output capacitance $C_{\text {eff }}=I_{\text {out }} / S$ (where $S$ is the output slew rate) as a way to characterize this shortcoming.

[^37]:    ${ }^{64}$ You've got to keep source impedances quite low in order not to degrade such a low $e_{\mathrm{n}}$; even a $100 \Omega$ resistor has an open-circuit voltage noise of $1.3 \mathrm{nV} / \sqrt{\mathrm{Hz}}$. See Chapter 8 .

[^38]:    ${ }^{65}$ And the overall resistor scaling is typically good to only $\pm 20 \%$ of the nominal value on the datasheet: absolute resistance value is sacrificed on the altar of resistor ratio matching.

[^39]:    ${ }^{66}$ Some manufacturers specify half that value, i.e., the impedance with both terminals tied together; the datasheet usually tells you which they mean.

[^40]:    ${ }^{67}$ There's another way to boost $V_{\mathrm{CM}}$ without such compromise, by using a second op-amp to cancel the common-mode signal; see Figure 7.27 in the previous edition of this book. We are unaware of any commercial difference amplifiers that use this trick.

[^41]:    ${ }^{70}$ At least at dc. At higher frequencies it again becomes important to

[^42]:    ${ }^{71}$ More precisely, it includes an on-chip resistor, ratio matched to $R_{\mathrm{f}}$, to produce an overall guaranteed gain of $100.0 \pm 0.25 \%$.
${ }^{72}$ The datasheet separates out the front-end and second-stage contributions, $1 \mathrm{nV} / \sqrt{\mathrm{Hz}}$ and $65 \mathrm{nV} / \sqrt{\mathrm{Hz}}$, respectively. From these you can calculate the input-referred noise $e_{\mathrm{n}}(\mathrm{RTI})=$ $\left\{e_{\mathrm{n}}(\text { in })^{2}+\left[e_{\mathrm{n}}(\text { out }) / G\right]^{2}+4 k T R_{\mathrm{g}}\right\}^{1 / 2}$. The last term is the square of the Johnson noise voltage $e_{\mathrm{n}}=0.13 \sqrt{R_{\mathrm{g}}} \mathrm{nV} / \sqrt{\mathrm{Hz}}$.

[^43]:    ${ }^{73}$ Put another way, the cable's capacitance degrades the CMRR by creating differential phase shifts between the two signals, owing to their unbalanced source impedances.
${ }^{74}$ Instruments for measuring very low currents - "electrometers" and "source measure units" - include guard outputs and (usually) special BNC-like "triax" connectors for use with triaxial shielded cables.

[^44]:    ${ }^{75}$ Highland Technology's V490 VME Multi-Range Digitizer.
${ }^{76}$ The gain-setting resistors are chosen from standard "E96" $1 \%$ resistor values, so the actual gains differ from round-number values (with $\pm 1 \%$ tolerance they would never be perfect, anyway). This front end would form part of a data-acquisition system, with overall gain and offset data held in software, from a calibration procedure carried out by relays $K_{1}$ and $K_{2}$.

[^45]:    ${ }^{77}$ Larkin sings the praises of Fujitsu FTR-B3GA4.5Z DPDT relays, with their sub-picofarad capacitances.

[^46]:    78 They're rated at 500 V , and come in three small package styles (TO-92, SOT23, and SOT89 with tab). The alternative BSS126 from Infineon is rated at 600 V , and costs less ( $\$ 0.15$ in small quantities). It comes only in the SOT-23 package, whereas the LND150 is available in three package styles, including a 1.5 W TO-243 small power package.
${ }^{79}$ Be sure to check that the op-amp does not suffer from phase reversal (see, e.g., §4.6.6), if you care about the output during input overdrive. A robust cure is to use a pair of input clamp diodes, as in Figure 5.81.

[^47]:    ${ }^{80}$ And a momentary $500 \mathrm{~V}, 250 \mathrm{~W}$ surge in $R_{1}$, which should be a bulkcomposition type, or several SMT resistors in series, to handle both the voltage and the energy transient; see Chapter $1 x$.

[^48]:    ${ }^{81}$ See also related material in the second edition, pp. 422-428.

[^49]:    ${ }^{82}$ L. Vestergaard Hau, S. E. Harris, Z. Dutton, and C. H. Behroozi, "Light speed reduction to 17 metres per second in an ultracold atomic gas," Nature 397 594-598 (1999).
${ }^{83}$ A smallish voltage, but already an uncomfortably large power dissipation $(\sim 75 \mathrm{~W})$, requiring a temperature stabilized oil bath.

[^50]:    84 The AD8227 variant allows $V_{\mathrm{CM}}$ to the negative rail, so you could run it single supply; but you pay a price in larger $V_{\mathrm{OS}}$ and $I_{\mathrm{B}}$, and its CMRR degrades at a lower frequency.

[^51]:    ${ }^{85}$ Some of these have back-to-back clamp diodes across the inputs (true also of some op-amps and comparators), for which the damage is

[^52]:    ${ }^{86}$ To achieve low input currents with the C configuration, LTC uses superbeta BJTs with base-current cancellation in some of the listed parts $\left(I_{\mathrm{B}} \approx 50 \mathrm{pA}\right)$; Analog Devices does even better using JFETs, but with greater offset and noise. Some of the TI/Burr-Brown INAs listed as A types may in fact use the C configuration; their datasheets are silent on the circuit details.
${ }^{87}$ BJT-input amplifiers are prone to RFI upset, because their inputs are forward-biased base-emitter (diode) junctions. And RFI is a real problem in these low-level circuits with inputs from remote sensors. Better to use a JFET-input amplifier if you are bedeviled by RFI.

[^53]:    ${ }^{88}$ Because they contain only a few MOSFETs, current sources, and current mirrors, devices of configuration F can be quite inexpensive. For example, the AD8293 (an AZ with fixed $G=80$ or 160) sells for only \$0.97 (qty 100).

[^54]:    ${ }^{89}$ Some E types (e.g., the AD8130, a variant of the AD8129 in Table 5.8) are specified and characterized only for $G=1$. These are especially useful as differential line receivers, etc., but they are generally limited in swing, typically in the range of 3 to 4 Vpp (the AD8237, with its flying switched capacitors, is an exception). See also $\S 12.10$ for a discussion of differential signaling in the digital context.

[^55]:    ${ }^{90}$ Which may not be evident from the datasheets, which sometimes omit spectral noise plots.

[^56]:    ${ }^{91}$ Or you can power the output from a split supply, staying within that total supply range.
92 See, for example, Dollar and Howe, "The Highly Adaptive SDM Hand: Design and Performance Evaluation", International Journal of Robotics Research 29, (5), 585-597 (2010), available at the web page of The Harvard BioRobotics Laboratory: biorobotics.harvard. edu.

[^57]:    ${ }^{95}$ See also the parts listed under "single-ended to differential" in Table 5.10 (page 375).

[^58]:    100 You can look at this another way: the manufacturer's recommended gain-setting resistor values are chosen such that a small amount of peaking is exploited to extend the amplifier's natural bandwidth.
${ }^{101}$ Many parts (the D and E configurations) let you add feedback capacitors to reduce the bandwidth. With some parts this may introduce instability at low gains, but with others it may improve the stability, especially when larger resistor values are used.

[^59]:    102 Omit the small bypass capacitor shown, if this mode of operation is anticipated.
${ }^{103}$ A member of the hard-to-Google corporate name club, which includes AND Displays, and ON Semiconductor. (Try it: you'll get more than ten billion Google hits for "AND" or "ON.")

[^60]:    ${ }^{104}$ Repeating some important advice: when designing with high-speed ICs, it's particularly important to pay attention to special instructions in the datasheet; the AD9255, for example, devotes nearly a full page to a discussion of input $R$ 's and $C$ 's.
${ }^{105}$ Except when operating at low gain: here that would require $G \leq 1$, so that the AD8139's input terminals are brought up to 1 V or more by the $R_{\mathrm{f}} R_{\mathrm{g}}$ divider. See the discussion in $\S 5.17 .1$.

[^61]:    106 Other differential amplifiers whose feedback inputs can operate at or near ground are indicated with $\mathbf{w}$ or $\mathbf{v}$ in Table 5.10 (page 375), and include the LTC1992, LTC6605, LTC6601, LTC6404, THS4508, and THS4511. These parts span the bandwidth range from 3 MHz to 2000 MHz .

[^62]:    107 But sometimes a little bit of noise can be a good thing, as it can improve ADC linearity and dynamic range by way of "dithering." See, for example, The Art of Digital Audio by John Watkinson (3rd ed., 2001); or Vanderkooy and Lipshitz "Dither in digital audio," J. Audio Eng. Soc., 35, (12), 966-975, (1987).

[^63]:    108 And perhaps read the helpful Analog Devices MT-076 "Differential Driver Analysis."

[^64]:    ${ }^{109}$ Some parts (for example the THS4008 and THS4511) even specify " $V_{S-}=0$ " and "input referenced to ground" as the operating condition for their specifications.
${ }^{110}$ For the latter you can substitute the improved LT1013/1014, which eschew that nasty habit and provide better performance overall; but no such solution is available for differential amplifiers.

[^65]:    111 Taking the example of the LMH6553 and LMH6552 CFB amplifiers, these are specified with $R_{\mathrm{f}}=274 \Omega$ and $357 \Omega$, at which the respective bandwidths are 900 and 1500 MHz , and the slew rates are 2300 and $3800 \mathrm{~V} / \mu \mathrm{s}$. These specs are for $G=1$, but with CFB op-amps you can dramatically increase their gain without losing too much bandwidth. For example the 1500 MHz LMH6552 claims to have 800 MHz of bandwidth still at $G=4$. For higher gain you may prefer not to reduce $R_{\mathrm{i}}$ much, but rather to increase $R_{\mathrm{f}}$. With CFB amplifiers a primary effect of increasing $R_{\mathrm{f}}$ is to reduce the slew rate proportionally; but, hey, you had plenty to begin with! Increasing $R_{\mathrm{f}}$ with CFB does cause an increase in noise.

[^66]:    112 The AD8351 (not in our table, but similar to the AD8352), offers 3 GHz bandwidth with $13 \mathrm{~V} / \mathrm{ns}$ slew rate and 2 Vpp capability to nearly 2 GHz .

[^67]:    115 Throughout the book we use $f_{\mathrm{T}}$ as shorthand for the proper term gainbandwidth product (GBP, GBW, or GBWP), which is the extrapolated unity-gain crossover frequency.

[^68]:    ${ }^{1}$ This downward shift in rolloff frequency is sometimes called the "shrinkage factor"; for a cascade of $n$ identical and buffered $R C$ lowpass sections, the 3 dB frequency is given by $f_{3 \mathrm{~dB}}(n) / f_{3 \mathrm{~dB}}(1)=\sqrt{2^{1 / n}-1}$.

[^69]:    ${ }^{2}$ Not shown is its less-than-stunning in-band-phase characteristics: $495^{\circ}$ phase lag at 16.5 kHz , rising nonlinearly (writhing might be a better term) to $1270^{\circ}$ at 19.5 kHz . Fortunately, phase has little effect upon audio intelligibility.
${ }^{3}$ Based on Figures 11 and 12 from Orchard, H. J., and Sheahan, D. F., "Inductorless Bandpass Filters, "IEEE Journal of Solid-State Circuits, Vol. SC-5, No. 3 (1970), where the designers illustrated an activefilter implementation of this passive-element design. The essence of their paper was that you could implement such an $L C$ filter with better performance and smaller size by replacing the real inductors with gyrators (§6.2.4C). In their implementation the inductors were implemented with inductorless "Riordan gyrators," with each $\pi$-inductor (set of three inductors, including the floating inductor) requiring one quad op-amp, nine resistors and two capacitors. The authors state that inductor Q's greater than 1000 are practical, with the available op-amp gainbandwidth product being the primary limitation. Their 1970-technology gyrator implementation (occupying one cubic inch) was far superior to what was possible with conventional inductors. Interested readers may wish to read R. H. S. Riordan, "Simulated inductors using differential amplifiers," Electronic. Letters 3, pp. 50-51 (Feb. 1967).
${ }^{4}$ Better is the enemy of good enough. (Proverb attributed, variously, to the Soviet Admiral Sergei Gorshkov, to Carl von Clausewitz, and to Voltaire.)

[^70]:    5 Where it would have zero impedance were it not for losses in the inductor and capacitor.

[^71]:    ${ }^{10}$ Also known as a generalized immittance converter.

[^72]:    ${ }^{11}$ Most gyrator implementations are ground referenced; they can replace an inductor that is returned to ground, but not a floating inductor.
${ }^{12}$ Or, equivalently, a generalized immittance converter.
${ }^{13}$ The peaking can be eliminated by adding a resistor in series with the gyrator's capacitor, roughly equal to its reactance at the peaking frequency.

[^73]:    ${ }^{14}$ Application Note AB-026A, by Rick Downs (TI document sbaa001, 1991).
${ }^{15}$ According to SRS, "The architecture of the filter is based on a singly terminated passive $L C$ ladder filter. $L$ 's are simulated with active gyrators formed by op-amp pairs. Passive $L C$ ladder filters have the special characteristic of being very tolerant of variations in component values. Because no section of the ladder is completely isolated from the other, a change in value of any single component affects the entire ladder. The design of the $L C$ ladder however, is such that the characteristics of the rest of the ladder will shift to account for the change in such a

[^74]:    way as to minimize its effect on the ladder. Not only does this loosen the requirement for extremely high accuracy resistors and capacitors, but it also makes the filter extremely stable despite wide temperature variations. As such, the anti-aliasing filter used in the SR830 does not ever require calibration to meet its specifications."
${ }^{16}$ R. P. Sallen and E. L. Key, "A practical method of designing RC active filters," IRE Trans. Circuit Theory, 2 (1), 74-85 (1955).

[^75]:    ${ }^{17}$ Sometimes $t_{\mathrm{d}}$ is defined to $10 \%$ (rather than $50 \%$ ) output.
18 That term comes from wave analysis in dispersive materials, where one distinguishes phase velocity and group velocity. The latter refers to the speed with which a group of frequencies, together making up a characteristic wave shape, moves through the medium. The group delay is the analogous quantity, expressed as a time delay $T_{\mathrm{g}}$, for a signal passing through a filter. The connection between phase shift and group delay is $T_{\mathrm{g}}=-d \phi / d \omega=-\frac{1}{2 \pi} d \phi / d f$.

image_name:Figure 6.19
description:The graph depicted is a time-domain waveform illustrating the response of a filter, specifically a simple RC lowpass filter, to a step input. The graph shows the output voltage $V_{\text{out}}$ on the vertical axis, expressed as a percentage of the final value $V_F$, and time on the horizontal axis.

1. **Type of Graph and Function:**
- This is a time-domain response graph for a lowpass filter.

2. **Axes Labels and Units:**
- The vertical axis is labeled $V_{\text{out}}$ and represents the output voltage as a percentage of the final value $V_F$.
- The horizontal axis is labeled 'Time' with no specific units provided, but it is implied to be in seconds or a relevant time unit for RC circuits.

3. **Overall Behavior and Trends:**
- The graph shows an initial rapid rise in output voltage from 0% to about 90% of $V_F$, characterized by a rise time $t_r$.
- Following the rise, the waveform overshoots the final value by approximately ±15%.
- After the overshoot, the waveform exhibits ringing, which gradually diminishes as it approaches the final value.
- The settling time $t_s$ is marked, indicating the time taken for the output to settle within ±5% of the final value.

4. **Key Features and Technical Details:**
- **Rise Time ($t_r$):** The time taken for the output to rise from 10% to 90% of the final value.
- **Delay Time ($t_d$):** The time at which the output reaches 50% of the final value.
- **Overshoot:** The peak value exceeds the final steady-state value by ±15%.
- **Ringing:** Oscillations following the overshoot.
- **Settling Time ($t_s$):** The time required for the output to remain within ±5% of the final value.

5. **Annotations and Specific Data Points:**
- The graph is annotated with markers indicating the rise time $t_r$, delay time $t_d$, and settling time $t_s$.
- The overshoot and ringing are clearly labeled, providing insight into the dynamic behavior of the filter.

Figure 6.19. Time-domain filter characteristics. A simple $R C$ lowpass filter, for example, would have no overshoot or ringing, and would be characterized by a rise time of $t_{\mathrm{r}}=2.2 R C\left(\approx 0.35 / f_{3 \mathrm{~dB}}\right)$, a delay time of $t_{\mathrm{d}}=0.69 R C$, and a settling time (to $1 \%$ ) of $t_{\mathrm{s}}=4.6 R C$.
ripple in the passband characteristic, the transition from pass-band to stopband can be steepened considerably. A third criterion that may be important is the ability of the filter to pass signals within the passband without distortion of their waveforms caused by phase shifts. You may also care about rise time, overshoot, and settling time. Generally speaking, you've got to make tradeoffs among these characteristics - a filter with a sharp cutoff will exhibit poor time-domain properties such as ringing and phase shifts.

There are filter designs available to optimize each of these characteristics, or combinations of them. In fact, rational filter selection will not be carried out as just described; rather, it normally begins with a set of requirements on passband flatness, attenuation at some frequency outside the passband, and whatever else matters. You will then choose the best design for the job, using the number of poles necessary to meet the requirements. ${ }^{19}$ In the next few sections we introduce the three popular classics - the Butterworth filter (maximally flat passband), the Chebyshev filter (steepest transition from passband to stopband), and the Bessel filter (maximally flat time delay). Each of these filter responses can be produced with a variety of different filter circuits, some of which we discuss later. They are

[^0]all available in lowpass, highpass, bandpass, and band-stop (notch) versions. ${ }^{20}$

#### A. Butterworth and Chebyshev filters

The Butterworth filter produces the flattest passband response, at the expense of steepness in the transition region from passband to stopband. As you will see later, it has only mediocre phase and transient characteristics. The amplitude response is given by

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}}=\frac{1}{\left[1+\left(f / f_{\mathrm{c}}\right)^{2 n}\right]^{\frac{1}{2}}} \tag{6.3}
\end{equation*}
$$

where $n$ is the order of the filter (number of poles). Increasing the number of poles flattens the passband response and steepens the stopband falloff, as shown in Figure 6.20.
image_name:Figure 6.20
description:The graph in Figure 6.20 is a Bode plot representing the amplitude response of a normalized lowpass Butterworth filter. The x-axis is labeled "Normalized Frequency" and uses a logarithmic scale ranging from 0.1 to 10. The y-axis is labeled "Amplitude Response V_out/V_in" and also uses a logarithmic scale, ranging from 0.001 to 1.

The graph depicts several curves, each representing a different order of the Butterworth filter, denoted by "n." The orders shown are n=1, 2, 4, 8, 16, and 32.

The general behavior of the graph shows that all curves start at an amplitude response of 1 (0 dB) at low frequencies, indicating a flat passband. As the frequency approaches the cutoff frequency (normalized to 1), the amplitude response begins to decrease, marking the transition to the stopband.

Key features of the graph include:
- **Order n=1**: This curve has the most gradual roll-off, indicating a gentle transition from passband to stopband.
- **Higher Orders (n=2, 4, 8, 16, 32)**: As the order increases, the roll-off becomes steeper. For example, n=32 has a very sharp transition, indicating a much steeper slope in the stopband.
- The cutoff frequency, where the amplitude response begins to drop, is around the normalized frequency of 1 for all curves.

Annotations on the graph indicate the order of each filter curve, showing how higher-order filters provide better attenuation characteristics in the stopband while maintaining a flat passband. The graph effectively illustrates the trade-off between filter order and the sharpness of the cutoff transition in Butterworth filters.

Figure 6.20. Normalized lowpass Butterworth filter response curves. Note the improved attenuation characteristics for the higher-order filters.

The Butterworth filter trades off everything else for maximum flatness of response. It starts out extremely flat at zero frequency and bends over near the cutoff frequency $f_{\mathrm{c}}$ (which is usually the -3 dB point).

In most applications, all that really matters is that the wiggles in the passband response be kept less than some amount, say 1 dB . The Chebyshev filter responds to this reality by allowing some ripples throughout the passband, with greatly improved sharpness of the knee (compared with the "maximally flat" Butterworth, for example). A Chebyshev filter is specified in terms of its number of poles

[^1]and passband ripple. By allowing greater passband ripple, you get a sharper knee. The amplitude is given by
\$\$

$$
\begin{equation*}
\frac{V_{\mathrm{out}}}{V_{\mathrm{in}}}=\frac{1}{\left[1+\varepsilon^{2} C_{n}^{2}\left(f / f_{\mathrm{c}}\right)\right]^{\frac{1}{2}}} \tag{6.4}
\end{equation*}
$$

\$\$
where $C_{n}$ is the Chebyshev polynomial of the first kind of degree $n$, and $\varepsilon$ is a constant that sets the passband ripple. Like the Butterworth (but in even greater degree), the Chebyshev has phase and transient characteristics that are far from ideal.
image_name:A
description:The graph labeled 'A' is a Bode plot comparing the amplitude responses of several 6-pole lowpass filters, including Chebyshev, Butterworth, Bessel, and RC filters. The plot is divided into two parts: the top graph uses a logarithmic scale, while the bottom graph uses a linear scale.

**Type of Graph and Function:**
- The graph is a Bode plot showing the amplitude response, \( \frac{V_{\text{out}}}{V_{\text{in}}} \), of various filters as a function of normalized frequency.

**Axes Labels and Units:**
- The x-axis represents the normalized frequency, which is dimensionless.
- The y-axis represents the amplitude response, \( \frac{V_{\text{out}}}{V_{\text{in}}} \), also dimensionless.
- The top graph uses a logarithmic scale for the amplitude response, ranging from 0.001 to 1.
- The bottom graph uses a linear scale for the amplitude response, ranging from 0 to 1.

**Overall Behavior and Trends:**
- All filter responses start at an amplitude of 1 at low frequencies and decrease as the frequency increases.
- The Chebyshev filter exhibits a ripple in the passband due to its design, showing slight oscillations before the cutoff frequency.
- The Butterworth filter demonstrates a smooth, maximally flat passband with no ripples.
- The Bessel filter has a more gradual roll-off compared to the others, indicating a slower transition from passband to stopband.
- The RC filter shows the steepest initial drop-off, indicating the least effective transition among the filters shown.

**Key Features and Technical Details:**
- The Chebyshev filter is marked with a 0.5 dB ripple, indicating its passband ripple characteristic.
- The -3 dB point is annotated, showing the cutoff frequency where the output is reduced to 70.7% of the input.
- The graphs illustrate the trade-offs between different filter designs in terms of passband ripple and roll-off steepness.

**Annotations and Specific Data Points:**
- The Chebyshev filter's ripple in the passband is approximately 0.5 dB, corresponding to a 6% variation.
- The -3 dB point is shown, which is a standard reference for cutoff frequency in filter design.

Overall, the graphs provide a clear comparison of how these filters behave in terms of amplitude response across a range of frequencies, highlighting the differences in design and performance characteristics.
image_name:B
description:The graph labeled 'B' is a Bode plot displaying the amplitude response of several 6-pole lowpass filters, specifically Chebyshev (0.5 dB ripple), Butterworth, Bessel, and RC filters. This plot is presented on a linear scale.

**Axes Labels and Units:**
- The x-axis represents the normalized frequency, ranging from 0 to 3.
- The y-axis shows the amplitude response, \( \frac{V_{\text{out}}}{V_{\text{in}}} \), ranging from 0 to 1.

**Overall Behavior and Trends:**
- The graph shows how each filter's amplitude response decreases as the frequency increases.
- The Chebyshev filter with a 0.5 dB ripple exhibits a ripple in the passband, evident by the oscillations near the top of the amplitude response.
- The Butterworth filter displays a smooth curve with no ripples, highlighting its "maximally flat" characteristic in the passband.
- The Bessel filter shows a gentler roll-off compared to the others, indicating its superior phase characteristics.
- The RC filter has the steepest roll-off, indicating a less selective filter compared to the others.

**Key Features and Technical Details:**
- The Chebyshev filter reaches the -3 dB point at a lower normalized frequency compared to the Butterworth and Bessel filters, indicating a sharper cutoff.
- The Butterworth filter maintains a flat response up to its cutoff frequency, after which it declines more rapidly than the Bessel but less sharply than the Chebyshev.
- The Bessel filter, while having the least sharp cutoff, offers the best phase response, which is not directly visible in this amplitude plot but is implied by its gentle slope.
- The RC filter has the least desirable characteristics, with a rapid drop-off in amplitude response.

**Annotations and Specific Data Points:**
- The graph includes annotations for the -3 dB point and the 0.5 dB ripple, indicating the extent of the ripple in the Chebyshev filter's passband.
- The Chebyshev filter's ripple is labeled as 0.5 dB = 6%, marking the variation in amplitude within the passband.

Figure 6.21. Comparison of some common 6-pole lowpass filters. The same filters are plotted on both linear and logarithmic scales. The actual gains of the filters are shown, rather than the "topadjusted" 0 dB convention.

Figure 6.21 presents graphs comparing the responses of Chebyshev and Butterworth 6-pole lowpass filters. As you can see, they're both tremendous improvements over a 6pole $R C$ filter.

As a practical reality, the Butterworth, with its "maximally flat" passband, may not be as attractive as it might
appear, since you are always accepting some variation in passband response anyway (with the Butterworth it is a gradual rolloff near $f_{\mathrm{c}}$, whereas with the Chebyshev it is a set of equal-amplitude ripples spread throughout the passband). Furthermore, active filters constructed with components of finite tolerance will deviate from the predicted response, which means that a real Butterworth filter will exhibit some passband ripple anyway. The graph in Figure 6.22 illustrates the effects of worst-case variations in resistor and capacitor values on filter response.
image_name:Figure 6.22
description:**Type of Graph and Function:**
The graph is a frequency response plot, showing the gain in decibels (dB) as a function of frequency. This is typical for analyzing the performance of filters, such as Butterworth or Chebyshev filters.

**Axes Labels and Units:**
- The x-axis is labeled "Frequency" and is on a linear scale. The unit of frequency is not explicitly mentioned, but it is typically in hertz (Hz) for such plots.
- The y-axis is labeled "Gain (dB)," indicating the output gain of the filter in decibels.

**Overall Behavior and Trends:**
- The graph shows a roll-off in gain as the frequency increases, a characteristic feature of low-pass filters.
- The gain starts around 0 dB at low frequencies, indicating unity gain or no amplification.
- As frequency increases, the gain decreases sharply, showing a transition from the passband to the stopband.

**Key Features and Technical Details:**
- The graph illustrates the effect of component tolerance on filter performance with two shaded regions.
- The inner shaded region corresponds to a 1% tolerance in resistor and capacitor values, while the outer shaded region corresponds to a 5% tolerance.
- Both regions show deviations from the ideal filter response, with the 5% tolerance causing more significant deviations.
- The shaded areas indicate variations in the cutoff frequency and the slope of the roll-off, affecting the sharpness and position of the transition band.

**Annotations and Specific Data Points:**
- The graph does not provide specific numerical values for cutoff frequencies or the exact point of -3 dB, but the trend and shaded areas indicate how component tolerances affect these values.
- The regions of deviation suggest that the real-world implementation of the filter will have a range of possible responses, depending on the exact tolerances of the components used.

Overall, this graph highlights the impact of component tolerances on the performance of active filters, showing that higher tolerances lead to greater deviations from the ideal filter response, particularly in the transition region between the passband and stopband.

Figure 6.22. The effect of component tolerance on active-filter performance.

Viewed in this light, the Chebyshev is a very rational filter design. It manages to improve the situation in the transition region by spreading equal-size ripples ${ }^{21}$ throughout the passband, the number of ripples increasing with the order of the filter. Even with rather small ripples (as little as 0.1 dB ) the Chebyshev filter offers considerably improved sharpness of the knee compared with the Butterworth. To make the improvement quantitative, suppose that you need a filter with flatness to 0.1 dB within the passband and 20 dB attenuation at a frequency $25 \%$ beyond the top of the passband. By actual calculation, that will require a 19-pole Butterworth, but only an 8-pole Chebyshev.

The idea of accepting some passband ripple in exchange for improved steepness in the transition region, as in the equiripple Chebyshev filter, is carried to its logical limit in the so-called elliptic (or Cauer) filter by trading ripple in both passband and stopband for an even steeper transition region than that of the Chebyshev filter. ${ }^{22}$ Such a filter does the job, if you are satisfied with an amplitude characteristic that reaches and maintains some minimum attenuation throughout the stopband (rather than continuing to fall

[^2]off with a $6 n \mathrm{~dB} /$ octave ultimate slope). The payback is a simpler filter, with better phase and amplitude characteristics (see below). With computer-aided design techniques, the design of elliptic filters is as straightforward as for the classic Butterworth and Chebyshev filters.
image_name:Figure 6.23
description:The graph in Figure 6.23 is a Bode plot, specifically representing the frequency response of a lowpass filter. It is plotted with the gain on the vertical axis and frequency on the horizontal axis, both on a logarithmic scale.

Axes Labels and Units:
- **Vertical Axis (Gain):** The gain is measured in decibels (dB) and is on a logarithmic scale. It shows the range from maximum gain (max) to minimum gain (min) in the passband, and a specified gain level in the stopband (G_stop).
- **Horizontal Axis (Frequency):** The frequency is also on a logarithmic scale, indicating the range from zero to higher frequencies, with specific markers for f_cutoff and f_stop.

Overall Behavior and Trends:
- **Passband:** Within the passband, the gain fluctuates between a maximum and minimum level, indicating ripple. This ripple is a characteristic of certain filter designs, like Chebyshev filters.
- **Transition Band:** The gain begins to decrease sharply after the cutoff frequency (f_cutoff), marking the transition from the passband to the stopband.
- **Stopband:** After the stop frequency (f_stop), the gain stabilizes at a lower level (G_stop) with some ripple, indicating the attenuation level in the stopband.

Key Features and Technical Details:
- **Ripple in Passband:** The gain oscillates within a defined ripple range in the passband, which is visually represented by a shaded area.
- **Cutoff Frequency (f_cutoff):** This is the frequency at which the response starts to leave the passband.
- **Stop Frequency (f_stop):** This is the frequency at which the response fully enters the stopband.
- **Stopband Gain (G_stop):** The gain level in the stopband is constant, indicating the minimum attenuation level.

Annotations and Specific Data Points:
- The graph includes annotations for maximum and minimum gain in the passband (G_pass) and a specific gain level in the stopband (G_stop).
- The transition from the passband to the stopband is marked by vertical dashed lines at f_cutoff and f_stop.
- The ripple is indicated by arrows in the passband and stopband, showing the allowable range of gain fluctuations.

Figure 6.23. Specifying filter frequency-response parameters.
Figure 6.23 shows how you specify filter frequency response graphically. In this case (a lowpass filter) you indicate the allowable range of filter gain (i.e., the ripple) in the passband, the minimum frequency at which the response leaves the passband, the maximum frequency at which the response enters the stopband, and the minimum attenuation in the stopband. As an example, Figure 6.24 compares the responses for Chebyshev and elliptic lowpass filter implementations to meet a specified performance, here requiring an 11-pole Chebyshev or a 6-pole elliptic (to meet the same specifications with a Butterworth would require a 32 -pole implementation!). The simpler elliptic filter has the better phase characteristics, but its response does not continue to fall off monotonically with frequency once it has reached the specified stopband attenuation.

#### B. Bessel filter

As we've suggested, the amplitude versus frequency response of a filter does not tell the whole story. A filter characterized by a flat amplitude response may exhibit rapidly changing phase shifts, which produce unequal time delays for signals within its passband. The result is that a signal in the passband will suffer distortion of its waveform. In situations where the shape of the waveform is paramount, a linear-phase filter (or constant-time-delay filter) is desirable. A filter whose phase shift varies linearly with frequency is equivalent to a constant time delay for signals within the passband; i.e., the waveform is not distorted. The
image_name:Figure 6.24
description:The graph in Figure 6.24 is a Bode plot illustrating the frequency response of a lowpass filter, specifically a 6-pole elliptic filter. The x-axis represents frequency in kilohertz (kHz), ranging from 1 kHz to 100 kHz, using a logarithmic scale. The y-axis represents attenuation in decibels (dB), ranging from 0 dB to -100 dB.

Overall Behavior and Trends:
- **Passband:** From DC to approximately 10 kHz, the filter exhibits a 2 dB ripple band, indicating slight variations in attenuation within this range. The attenuation remains close to 0 dB, suggesting minimal signal loss.
- **Transition Region:** Around 10 kHz, the filter begins to transition sharply into the stopband. This area is marked by a steep decline in attenuation, characteristic of elliptic filters which provide a rapid roll-off.
- **Stopband:** Beyond 12 kHz, the attenuation reaches -50 dB and continues to decrease, indicating effective suppression of frequencies in this range. The stopband shows ripple effects, typical in elliptic filters, with attenuation levels fluctuating but remaining significantly below the passband level.

Key Features and Technical Details:
- **Ripple:** The passband ripple is specified as 2 dB, which is a measure of how much the attenuation varies within the passband.
- **Stopband Attenuation:** The graph indicates that the attenuation is at least 50 dB down for frequencies above 12 kHz.
- **Elliptic Filter Characteristics:** The dashed curve represents the performance of the elliptic filter, showing both passband and stopband ripple, which is a defining feature of such filters that allows for a steeper roll-off compared to other filter types like Chebyshev or Butterworth.

Annotations and Specific Data Points:
- Annotations on the graph highlight the 2 dB ripple band in the passband up to 10 kHz and the 50 dB attenuation level above 12 kHz.
- The graph demonstrates the elliptic filter’s ability to meet stringent performance specifications with fewer poles compared to Chebyshev or Butterworth filters, as noted in the context.

Figure 6.24. Lowpass filter example: a 6-pole elliptic filter with both passband and stopband ripple (dashed curve) meets the performance specifications shown here, whereas you would need an 11-pole Chebyshev (which has ripple only in its passband) or a 32-pole Butterworth ("maximally flat" - no ripple in passband or stopband) to do as well.

Bessel filter (also called the Thomson filter) ${ }^{23}$ has maximally flat time delay within its passband in analogy with the Butterworth, which has maximally flat amplitude response.

To see the kind of improvement in time-domain performance you get with the Bessel filter, look at Figure 6.25 for a comparison of phase shift and time delay versus frequency for the Bessel filter compared with two classic filters that exhibit more abrupt frequency characteristics (Butterworth and Chebyshev). The poor time-delay performance of the Butterworth (and to a greater extent of the Chebyshev) gives rise to effects such as waveform distortion and overshoot when driven with pulse signals - see Figure 6.26. On the other hand, the price you pay for the Bessel's constancy of time delay is an amplitude response with even less steepness than that of the Butterworth or Chebyshev in the transition region between passband and stopband. An important point: adding sections to a Bessel filter (i.e., making it of higher order) does not significantly increase the steepness of transition into the stopband; it does, however, improve the phase linearity (constancy of time delay), as well as increasing the ultimate rate of falloff, reaching the usual $6 n \mathrm{~dB} /$ octave asymptotic limit (look ahead to Figure 6.30).

23 That's the legendary German mathematician Friedrich Bessel (17841846) who, though not a practicing circuit designer, developed the mathematics. The label Bessel-Thomson recognizes Thomson's application to filters: Thomson, W. E., "Delay Networks having Maximally Flat Frequency Characteristics," Proceedings of the Institution of Electrical Engineers, Part III, 96 44, pp. 487-490 (1949).
image_name:Bessel Phase Shift
description:The diagram consists of two main sections labeled A and B, each comparing phase shift and time delay characteristics of three types of lowpass filters: Bessel, Butterworth, and Chebyshev. Each filter type is further divided into configurations with 2, 4, and 8 poles.

**Section A: Phase Shift vs. Frequency**
- **Axes:**
- **Horizontal Axis:** Frequency, ranging from 0 to 2.5 kHz, with a vertical line indicating the cutoff frequency at 1 kHz.
- **Vertical Axis:** Phase shift in degrees, ranging from 0 to -700 degrees.
- **Bessel Filter:**
- Shows a gradual phase shift increase as the frequency approaches 1 kHz.
- The phase shift is less steep compared to the other filters, indicating better phase linearity.
- 2-pole, 4-pole, and 8-pole configurations show progressively steeper phase shifts.
- **Butterworth Filter:**
- Displays a more pronounced phase shift, especially beyond the cutoff frequency.
- The 8-pole configuration shows the most significant phase shift.
- **Chebyshev Filter (1dB):**
- Exhibits the steepest phase shift among the three filters.
- The 8-pole configuration is particularly steep, indicating less linearity in phase response.

**Section B: Time Delay vs. Frequency**
- **Axes:**
- **Horizontal Axis:** Frequency, ranging from 0 to 2.5 kHz, with a vertical line indicating the cutoff frequency at 1 kHz.
- **Vertical Axis:** Time delay in milliseconds.
- **Bessel Filter:**
- Shows a relatively flat time delay across the frequency range, with minor increases near the cutoff frequency.
- The 8-pole configuration has a slightly higher time delay.
- **Butterworth Filter:**
- Displays a peak in time delay around the cutoff frequency, especially pronounced in the 8-pole configuration.
- **Chebyshev Filter (1dB):**
- Has the most significant peaks in time delay at the cutoff frequency, with the 8-pole configuration showing a sharp peak.

Overall, the Bessel filter provides the most linear phase response and consistent time delay, making it suitable for applications requiring minimal phase distortion. The Butterworth and Chebyshev filters offer sharper cutoffs at the expense of increased phase shift and time delay variability.
image_name:Butterworth Phase Shift
description:The image contains two sets of graphs, labeled A and B, each illustrating different characteristics of three types of lowpass filters: Bessel, Butterworth, and Chebyshev (1dB). Each filter type is configured with a cutoff frequency of 1 kHz, marked by a vertical line on the graphs.

Graph A: Phase Shift vs. Frequency
- **Type of Graph:** Phase shift plot
- **Axes Labels and Units:**
- **Horizontal Axis:** Frequency in kHz, ranging from 0 to 2.5 kHz.
- **Vertical Axis:** Phase shift in degrees, ranging from 0 to -700 degrees.
- **Overall Behavior and Trends:**
- Each filter type shows a different rate of phase shift as the frequency increases.
- **Bessel Filter:** Displays a more gradual phase shift, with the 8-pole filter having the most significant shift.
- **Butterworth Filter:** Exhibits a more pronounced phase shift, especially for the 8-pole configuration, which shows a steep decrease.
- **Chebyshev Filter:** Also shows a significant phase shift, with a sharper decrease compared to the Bessel filter.
- **Key Features and Technical Details:**
- The phase shift increases with the number of poles in each filter type.
- The 8-pole filters have the most significant phase shift across all types.

Graph B: Time Delay vs. Frequency
- **Type of Graph:** Time delay plot
- **Axes Labels and Units:**
- **Horizontal Axis:** Frequency in kHz, ranging from 0 to 2.5 kHz.
- **Vertical Axis:** Time delay in milliseconds, ranging from 0 to 4 ms.
- **Overall Behavior and Trends:**
- **Bessel Filter:** Shows a relatively flat time delay across frequencies, with a slight increase for higher poles.
- **Butterworth Filter:** Exhibits a peak in time delay around the cutoff frequency, especially noticeable in the 8-pole filter.
- **Chebyshev Filter:** Displays a pronounced peak in time delay at the cutoff frequency, with the 8-pole filter reaching the highest delay.
- **Key Features and Technical Details:**
- The time delay peaks are more pronounced in the Butterworth and Chebyshev filters compared to the Bessel filter.
- The 8-pole configurations show the most significant time delay peaks across all filter types.
image_name:Chebyshev Phase Shift
description:The graph titled "Chebyshev Phase Shift" is part of a set of diagrams comparing phase shift and time delay for different lowpass filter types (Bessel, Butterworth, and Chebyshev) configured with a cutoff frequency of 1 kHz.

Type of Graph and Function:
This is a phase shift versus frequency graph for Chebyshev lowpass filters, showing how the phase shift varies with frequency for different pole configurations (2, 4, and 8 poles).

Axes Labels and Units:
- **Horizontal Axis:** Frequency in kilohertz (kHz), ranging from 0 to 2.5 kHz.
- **Vertical Axis:** Phase Shift in degrees, ranging from 0 to -700 degrees.
- The frequency axis is linear, with a vertical line at 1 kHz indicating the cutoff frequency.

Overall Behavior and Trends:
- The phase shift increases (becomes more negative) with frequency for all pole configurations.
- The 8-pole filter shows the steepest increase in phase shift, indicating a more rapid phase change compared to the 2-pole and 4-pole filters.
- As the number of poles increases, the phase shift becomes more pronounced at lower frequencies.

Key Features and Technical Details:
- The graph illustrates the typical behavior of Chebyshev filters, which are known for their ripple in the passband and sharper cutoff characteristics.
- At the cutoff frequency (1 kHz), the phase shift is significant for all pole configurations, with the 8-pole filter reaching nearly -700 degrees.

Annotations and Specific Data Points:
- Each line is labeled with the corresponding pole number (2, 4, and 8 poles), providing a clear comparison of how the phase shift changes with different filter orders.
- The vertical line at 1 kHz serves as a reference for the cutoff frequency, a critical point in filter design.

This graph provides insight into the phase distortion introduced by Chebyshev filters, which is an important consideration in applications where phase linearity is critical.
image_name:Bessel Time Delay
description:The graph titled "Bessel Time Delay" is part of a set of diagrams comparing phase shift and time delay characteristics for different lowpass filter types: Bessel, Butterworth, and Chebyshev. Each filter type is represented with different pole configurations (2-pole, 4-pole, 8-pole).

**Type of Graph and Function:**
The graph is a time delay versus frequency plot, specifically for Bessel filters. It is designed to show how time delay varies across different frequencies for lowpass filters with a focus on Bessel characteristics.

**Axes Labels and Units:**
- The horizontal axis represents Frequency, measured in kilohertz (kHz), ranging from 0 to 2.5 kHz.
- The vertical axis represents Time Delay, measured in milliseconds (msec), ranging from 0 to 0.5 msec.
- The frequency axis is linear, with a vertical reference line marking the cutoff frequency at 1 kHz.

**Overall Behavior and Trends:**
- The Bessel filter shows a relatively flat time delay response across the frequency range.
- As the number of poles increases (from 2 to 8 poles), the time delay slightly increases, but the response remains smooth and consistent.
- The 8-pole Bessel filter has the highest time delay, but it still maintains a gradual slope, indicating minimal distortion in the time domain.

**Key Features and Technical Details:**
- The time delay is most constant for the 2-pole configuration and increases with more poles, yet it remains well-behaved compared to other filter types like Butterworth and Chebyshev, which show peaks in time delay.
- The cutoff frequency is clearly marked at 1 kHz, where the characteristics of the filter are often analyzed.

**Annotations and Specific Data Points:**
- The graph includes annotations for each pole configuration (2, 4, 8 poles), clearly indicating their respective time delay curves.
- The vertical reference line at 1 kHz serves as a critical marker for evaluating filter performance at the cutoff frequency.

This graph highlights the Bessel filter's advantage in maintaining a flat time delay, which is beneficial for applications requiring minimal phase distortion.
image_name:Butterworth Time Delay
description:The graph titled "Butterworth Time Delay" is a part of a comparative analysis of three different lowpass filter designs: Bessel, Butterworth, and Chebyshev, each with varying pole configurations (2, 4, and 8 poles). The analysis is presented in two subplots labeled A and B, focusing on phase shift and time delay respectively.

### Subplot A: Phase Shift vs. Frequency
- **Type of Graph:** Line graph showing phase shift in degrees vs. frequency in kilohertz (kHz).
- **Axes Labels and Units:**
- Horizontal axis: Frequency (kHz), ranging from 0 to 2.5 kHz.
- Vertical axis: Phase Shift (degrees), ranging from 0 to -700 degrees.
- **Overall Behavior and Trends:**
- The phase shift increases negatively with frequency for all filter designs.
- Bessel filters show the least phase shift, followed by Butterworth and Chebyshev, which have more pronounced shifts as frequency increases.
- For each filter type, the phase shift becomes more significant with an increase in the number of poles.
- **Key Features and Technical Details:**
- A vertical line at 1 kHz marks the cutoff frequency for comparison.
- The Bessel filter maintains the flattest phase response, which is desirable for applications requiring minimal phase distortion.

### Subplot B: Time Delay vs. Frequency
- **Type of Graph:** Line graph showing time delay in milliseconds (msec) vs. frequency in kilohertz (kHz).
- **Axes Labels and Units:**
- Horizontal axis: Frequency (kHz), ranging from 0 to 2.5 kHz.
- Vertical axis: Time Delay (msec), ranging from 0 to 4 msec.
- **Overall Behavior and Trends:**
- The time delay increases with frequency and peaks near the cutoff frequency for Butterworth and Chebyshev filters.
- The Butterworth filter exhibits a noticeable peak in time delay, especially for higher pole numbers, with the 8-pole configuration showing the highest peak.
- The Bessel filter, in contrast, maintains a more consistent and lower time delay across frequencies.
- **Key Features and Technical Details:**
- The vertical line at 1 kHz serves as a reference for the cutoff frequency.
- Chebyshev filters show the most significant peaks in time delay, indicating more phase distortion near the cutoff frequency.
- The Butterworth filter's time delay increases significantly with more poles, indicating a trade-off between filter sharpness and time-domain performance.
image_name:Chebyshev Time Delay
description:The graph consists of two main sections labeled A and B, each illustrating different characteristics of lowpass filters. Each section contains three subplots corresponding to Bessel, Butterworth, and Chebyshev filters, respectively.

### Section A: Phase Shift vs. Frequency
- **Axes and Units**:
- **X-Axis**: Frequency in kilohertz (kHz), ranging from 0 to 2.5 kHz.
- **Y-Axis**: Phase shift in degrees, ranging from 0 to -700 degrees.
- The vertical line marks the cutoff frequency at 1 kHz.
- **Behavior**:
- **Bessel Filter**: The phase shift curves for 2, 4, and 8 pole configurations show a gradual decrease, maintaining a more linear relationship compared to the other filters.
- **Butterworth Filter**: The phase shift curves are more pronounced, especially for higher pole numbers, indicating a steeper phase shift as the frequency approaches the cutoff.
- **Chebyshev Filter (1dB)**: Exhibits the steepest phase shift among the three filters, with higher pole configurations showing more dramatic decreases.

### Section B: Time Delay vs. Frequency
- **Axes and Units**:
- **X-Axis**: Frequency in kilohertz (kHz), ranging from 0 to 2.5 kHz.
- **Y-Axis**: Time delay in milliseconds (msec), with different scales for each subplot.
- The vertical line marks the cutoff frequency at 1 kHz.
- **Behavior**:
- **Bessel Filter**: Shows a relatively constant time delay across frequencies, with slight increases at higher frequencies, especially for 8 pole configurations.
- **Butterworth Filter**: Displays a significant peak in time delay at the cutoff frequency, with the peak height increasing with the number of poles.
- **Chebyshev Filter (1dB)**: Features the most pronounced peaks in time delay at the cutoff frequency, with sharp increases and decreases, particularly noticeable in higher pole configurations.

Key Observations:
- The Bessel filter maintains a more consistent phase shift and time delay, showcasing its strength in preserving waveform shape.
- The Butterworth filter balances between phase linearity and sharpness in cutoff, with noticeable peaks in time delay.
- The Chebyshev filter provides the sharpest cutoff characteristics, at the expense of significant phase and time delay variations, especially around the cutoff frequency.

Figure 6.25. A. Phase shift vs. frequency for three lowpass filter types, each configured with a cutoff frequency of 1 kHz (vertical line). B. Time delay vs. frequency for the adjacent filters; note change of vertical-scale units and linear frequency axis. If you like normalized units, use $f / f_{\mathrm{c}}$ for the horizontal axes, and $t_{\mathrm{d}} / T$ for the time delay.

There are numerous filter designs that attempt to improve on the Bessel's good time-domain performance by compromising some of the constancy of time delay for improved rise time and amplitude-versus-frequency characteristics. The Gaussian filter has phase characteristics nearly as good as those of the Bessel, with improved step response. In another class there are interesting filters that allow uniform ripples in the passband time delay (in analogy with the Chebyshev's ripples in its amplitude response)
and yield approximately constant time delays even for signals well into the stopband; these are sometimes called simply "linear phase" filters, characterized with a parameter that sets the phase ripple (e.g., $0.5^{\circ}$ ) within the passband. Another approach to the problem of making filters with uniform time delays is to use allpass filters (also known as delay equalizers). These have constant amplitude response with frequency, with a phase shift that can be tailored to individual requirements. Thus they can be used to
improve the time-delay constancy of any filter, including Butterworth and Chebyshev types.
image_name:Bessel
description:The image contains three time-domain waveform graphs, each representing the response to a 1 V step input at t=0 for three different types of lowpass filters: Bessel, Butterworth, and Chebyshev.

**1. Bessel Filter:**
- **Graph Type:** Time-domain waveform.
- **Axes:**
- **X-axis:** Time in milliseconds (ms), ranging from 0 to 6 ms.
- **Y-axis:** Output Voltage in volts (V), ranging from 0 to 1.2 V.
- **Overall Behavior:**
- The Bessel filter shows a smooth rise in output voltage with minimal overshoot and no oscillations.
- The response is characterized by a gradual rise to a steady-state value of 1 V.
- **Key Features:**
- The graph includes responses for 2-pole, 4-pole, and 8-pole filters.
- As the number of poles increases, the rise time becomes slightly slower, but the response remains smooth.

**2. Butterworth Filter:**
- **Graph Type:** Time-domain waveform.
- **Axes:**
- **X-axis:** Time in milliseconds (ms), ranging from 0 to 6 ms.
- **Y-axis:** Output Voltage in volts (V), ranging from 0 to 1.2 V.
- **Overall Behavior:**
- The Butterworth filter exhibits a faster rise in output voltage compared to the Bessel filter but shows noticeable overshoot and slight oscillations before settling.
- **Key Features:**
- Responses for 2-pole, 4-pole, and 8-pole filters are shown.
- Higher pole counts lead to more pronounced overshoot and oscillations.

**3. Chebyshev Filter:**
- **Graph Type:** Time-domain waveform.
- **Axes:**
- **X-axis:** Time in milliseconds (ms), ranging from 0 to 6 ms.
- **Y-axis:** Output Voltage in volts (V), ranging from 0 to 1.2 V.
- **Overall Behavior:**
- The Chebyshev filter displays the fastest initial rise in voltage, followed by significant overshoot and oscillations.
- The response takes longer to settle to the steady-state value of 1 V.
- **Key Features:**
- Includes responses for 2-pole, 4-pole, and 8-pole filters.
- The oscillations are more pronounced with higher pole counts, with the 8-pole filter showing the most significant overshoot and ringing.

These graphs illustrate the trade-offs between time-domain performance and frequency-domain characteristics for each filter type, with Bessel offering the smoothest time response, Butterworth a balance, and Chebyshev prioritizing frequency characteristics at the expense of time-domain stability.
image_name:Butterworth
description:The graph is a time-domain waveform illustrating the response of three different types of 1 kHz lowpass filters—Bessel, Butterworth, and Chebyshev—to a 1 V step input at t = 0 ms. Each filter type is represented in a separate subplot, and within each subplot, responses for 2-pole, 4-pole, and 8-pole configurations are shown.

**Axes Labels and Units:**
- The x-axis represents time in milliseconds (ms), ranging from 0 to 6 ms.
- The y-axis represents output voltage in volts (V), ranging from 0 to 1.2 V.

**Overall Behavior and Trends:**
- **Bessel Filter:** Shows the smoothest response with minimal overshoot. As the number of poles increases, the rise time becomes slightly faster, but the waveforms remain smooth without significant oscillations.
- **Butterworth Filter:** Exhibits a moderate level of overshoot and oscillation compared to the Bessel filter. The 8-pole configuration shows more pronounced overshoot and oscillation than the 2-pole and 4-pole configurations.
- **Chebyshev Filter (1dB):** Displays the most significant overshoot and ringing among the three filters. The 8-pole configuration has the highest overshoot and oscillation, while the 2-pole configuration is less pronounced but still shows more oscillation than the Butterworth.

**Key Features and Technical Details:**
- **Bessel Filter:** Characterized by its linear phase response, leading to minimal distortion in the time domain. The waveforms rise smoothly to the steady-state value of 1 V with negligible overshoot.
- **Butterworth Filter:** Known for its flat amplitude response in the frequency domain, it sacrifices some time-domain performance, resulting in overshoot and ringing. The 8-pole configuration particularly highlights these effects.
- **Chebyshev Filter:** Optimized for a sharp cutoff in the frequency domain, it results in significant time-domain distortion. The overshoot exceeds 1.2 V, and oscillations are evident and prolonged, especially in the 8-pole configuration.

**Annotations and Specific Data Points:**
- Each subplot is labeled with the filter type, and the number of poles is annotated on each curve. The curves demonstrate how increasing the number of poles affects the time-domain response, with more poles generally leading to faster rise times but increased overshoot and oscillations, particularly in the Butterworth and Chebyshev filters.
image_name:Chebyshev (1dB)
description:The graph titled "Chebyshev (1dB)" is a time-domain waveform showing the response of Chebyshev lowpass filters to a 1 V step input at time t=0. This graph is part of a series comparing different filter types: Bessel, Butterworth, and Chebyshev.

1. **Type of Graph and Function:**
- The graph is a time-domain response plot, illustrating how the output voltage of a Chebyshev filter changes over time after a step input.

2. **Axes Labels and Units:**
- The x-axis represents time in milliseconds (ms), ranging from 0 to 6 ms.
- The y-axis represents output voltage in volts (V), ranging from 0 to 1.2 V.

3. **Overall Behavior and Trends:**
- The graph shows the response curves for 2-pole, 4-pole, and 8-pole Chebyshev filters.
- All curves initially rise sharply as the filters respond to the step input, reaching a peak slightly above 1 V.
- After the initial rise, the curves exhibit oscillations, which are more pronounced as the number of poles increases.
- The 8-pole filter shows the most significant overshoot and oscillations, while the 2-pole filter has the least.

4. **Key Features and Technical Details:**
- The Chebyshev filter is known for its ripple in the passband, which is evident in the oscillatory behavior of the output.
- The peak voltage exceeds 1 V due to overshoot, a characteristic of Chebyshev filters.
- The settling time, or the time it takes for the output to stabilize near 1 V, increases with the number of poles.

5. **Annotations and Specific Data Points:**
- Each curve is labeled with the number of poles (2, 4, 8), indicating the filter order.
- The graph highlights the trade-off between filter sharpness and time-domain performance, as higher-order filters have more oscillations and longer settling times.

Figure 6.26. Response to a 1 V step input at $t=0$, for the three 1 kHz lowpass filters of the previous figures.

#### C. Filter comparison

In spite of the preceding comments about the Bessel filter's frequency response, it still has vastly superior properties in the time domain compared with the Butterworth and Chebyshev. The Chebyshev, with its highly desirable amplitude-versus-frequency characteristics, actually has the poorest time-domain performance of the three. The Butterworth is in between in both frequency- and time-
domain properties. Table 6.1 on the next page and Figures 6.26 and 6.27 give more information about timedomain performance for these three kinds of filters to complement the frequency-domain graphs presented earlier. They make it clear that the Bessel is a desirable filter when performance in the time domain is important.
image_name:Figure 6.27
description:Figure 6.27 is a time-domain waveform graph comparing the step response of three different 8-pole lowpass filters: Chebyshev, Butterworth, and Bessel, all normalized to a 1 Hz cutoff frequency. The x-axis represents time in seconds, ranging from 0 to 5 seconds, while the y-axis represents the amplitude response, ranging from 0 to 1.2.

The graph shows three distinct curves:

1. **8-pole Chebyshev (1 dB ripple):** This curve is characterized by a rapid rise and significant overshoot, peaking at around 1.2 amplitude before oscillating and eventually settling. The overshoot is noted as 0.3% above the normalized level.

2. **8-pole Butterworth:** This curve rises more gradually compared to the Chebyshev filter and exhibits a moderate overshoot, with less oscillation.

3. **8-pole Bessel:** This curve demonstrates the smoothest transition with minimal overshoot and oscillation, settling quickly compared to the other two filters.

Overall, the Bessel filter shows the best time-domain performance with the least overshoot and fastest settling time, making it desirable for applications where time-domain response is critical. The Chebyshev filter, while providing a sharper cutoff in the frequency domain, exhibits the most overshoot and oscillation in the time domain. The Butterworth filter offers a balance between the two, with moderate overshoot and oscillations.

Figure 6.27. Step-response comparison for 8-pole lowpass filters normalized to 1 Hz cutoff frequency.

### 6.2.7 Filter implementation

We'll see in the next section how to implement these classic filters with R's, C's, and op-amps. These are called active filters, and have the advantage of requiring no inductors. This is good, because inductors tend to be bulky, imperfect, and not inexpensive.

However, for use at frequencies above roughly 100 kHz , it is often preferable to build passive filters like the antialias lowpass filter example we showed in Figure 6.9. You have two choices: you can build your own, or you can buy what you need. To make your own, you can use any of numerous design tables (we give a set in Appendix E) or filter-design software (see §6.3.8) to calculate the $L$ and $C$ values for the particular filter you want. If you are making only a few, you may wish to use slug-tuned inductors (adjusted with an inductance meter or bridge), and either $1 \%$ capacitors or hand-trimmed pairs of paralleled capacitors, to get the precision you need.

Alternatively, you can just throw money at the problem: there are dozens of manufacturers of standard and custom filters, and they are happy to build anything you want. At the low end of the frequency spectrum (say below 100 MHz ) they will use lumped elements ( $L$ 's and $C$ 's); above that you'll get coaxial or cavity filters. If the filter you want is a standard unit (e.g., in the MiniCircuits Labs catalog), it will be inexpensive and generally

Table 6.1 Time-domain Performance Comparison for Lowpass Filters ${ }^{a}$

| Type | $f_{3 \mathrm{~dB}}$ <br> (Hz) | Poles | Step risetime (0-90\%) <br> (s) | Overshoot (\%) | Settling time |  | Stopband attenuation |  |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
|  |  |  |  |  | $\text { to } 1 \%$ <br> (s) | to 0.1\% <br> (s) | $\begin{array}{r} f=2 f_{\mathrm{C}} \\ (\mathrm{~dB}) \end{array}$ | $\begin{gathered} f=10 f_{\mathrm{C}} \\ (\mathrm{~dB}) \end{gathered}$ |
| $\begin{aligned} & \text { Bessel } \\ & (-3 \mathrm{~dB} \text { at } \\ & \left.f_{\mathrm{c}}=1 \mathrm{~Hz}\right) \end{aligned}$ | 1.0 | 2 | 0.4 | 0.4 | 0.6 | 1.1 | 10 | 36 |
|  | 1.0 | 4 | 0.5 | 0.8 | 0.7 | 1.2 | 13 | 66 |
|  | 1.0 | 6 | 0.6 | 0.6 | 0.7 | 1.2 | 14 | 92 |
|  | 1.0 | 8 | 0.7 | 0.3 | 0.8 | 1.2 | 14 | 114 |
| $\begin{gathered} \text { Butterworth } \\ (-3 \mathrm{~dB} \text { at } \\ \left.f_{\mathrm{C}}=1 \mathrm{~Hz}\right) \end{gathered}$ | 1.0 | 2 | 0.4 | 4 | 0.8 | 1.7 | 12 | 40 |
|  | 1.0 | 4 | 0.6 | 11 | 1.0 | 2.8 | 24 | 80 |
|  | 1.0 | 6 | 0.9 | 14 | 1.3 | 3.9 | 36 | 120 |
|  | 1.0 | 8 | 1.1 | 16 | 1.6 | 5.1 | 48 | 160 |
| $\begin{gathered} \text { Chebyshev } \\ 0.5 \mathrm{~dB} \text { ripple } \\ (-0.5 \mathrm{~dB} \text { at } \\ \left.f_{\mathrm{C}}=1 \mathrm{~Hz}\right) \end{gathered}$ | 1.39 | 2 | 0.4 | 11 | 1.1 | 1.6 | 8 | 37 |
|  | 1.09 | 4 | 0.7 | 18 | 3.0 | 5.4 | 31 | 89 |
|  | 1.04 | 6 | 1.1 | 21 | 5.9 | 10.4 | 54 | 141 |
|  | 1.02 | 8 | 1.4 | 23 | 8.4 | 16.4 | 76 | 193 |
| Chebyshev <br> 2dB ripple <br> (-2dB at <br> $f_{\mathrm{C}}=1 \mathrm{~Hz}$ ) | 1.07 | 2 | 0.4 | 21 | 1.6 | 2.7 | 15 | 44 |
|  | 1.02 | 4 | 0.7 | 28 | 4.8 | 8.4 | 37 | 96 |
|  | 1.01 | 6 | 1.1 | 32 | 8.2 | 16.3 | 60 | 148 |
|  | 1.01 | 8 | 1.4 | 34 | 11.6 | 24.8 | 83 | 200 |
| Notes: (a) a design procedure for these filters is presented in the section "VCVS circuits." |  |  |  |  |  |  |  |  |

delivered from stock. Otherwise you will pay at least a hundred dollars, and wait at least a few weeks. Some manufacturers we've used are Lark Engineering, Mini-Circuits Laboratories, Trilithic (Cir-Q-Tel), and TTE.

## 6.3 Active-filter circuits

A lot of ingenuity has been used in inventing clever active circuits, each of which can be used to generate response functions such as the Butterworth, Chebyshev, etc. You might wonder why the world needs more than one activefilter circuit. The reason is that various circuit realizations excel in one or another desirable property, so there is no all-around best circuit.

Active filters can be built using discrete op-amps as the active elements. ${ }^{24}$ In that case you must provide the resistors and capacitors that set the filter characteristics. These passive components must generally be accurate and stable, particularly in filters with sharp frequency characteristics. An attractive alternative is to take advantage of the rich variety of IC active filters, in which most of the hard work has been done, including the on-chip integration of matched passive components.

[^3]Active filters come in two basic varieties: "continuoustime" filters, and switched-capacitor filters. Continuoustime filters are analog circuits made from op-amps, resistors, and capacitors; the filter characteristics are set by the component values and, of course, the circuit configuration. The thing just sits there and acts like a filter. Switchedcapacitor filters use a capacitor combined with a MOSFET switch, turned on and off by an externally applied clocking signal, to substitute for the input resistor in the classic op-amp integrator. The effective resistor value is set by the clocking frequency. A typical switched-capacitor filter uses several such integrators in combination with additional opamps to implement the desired filter function. ${ }^{25}$ Switchedcapacitor filters have the advantages of being simply tuned over a wide range (by the applied clocking frequency), of maintaining stable characteristics, and of being particularly easy to fabricate as ICs. However, they are generally noisier (i.e., with smaller dynamic range), have higher distortion, and can introduce switching artifacts such as aliasing and clock feedthrough.

Some of the features to look for in active filters are (a) small numbers of parts, both active and passive, (b) ease

[^4]of adjustability, (c) small spread of parts values, especially the capacitor values, (d) undemanding use of the op-amp, especially requirements on slew rate, bandwidth, and output impedance, (e) the ability to make high- $Q$ filters, (f) electrical tunability, and (g) sensitivity of filter characteristics to component values and op-amp gain (in particular, the gain-bandwidth product, $f_{\mathrm{T}}$ ). In many ways, the last feature is one of the most important. A filter that requires parts of high precision is difficult to adjust, and it will drift as the components age; in addition, there is the nuisance that it requires components of good initial accuracy. The VCVS circuit probably owes most of its popularity to its simplicity and its low parts count, but it suffers from high sensitivity to component variations. By comparison, recent interest in more complicated filter realizations is motivated by the benefits of insensitivity of filter properties to small component variability.

In this section we present several circuits for lowpass, highpass, and bandpass active filters. We begin with the popular VCVS, or controlled-source type, then show the state-variable designs available as ICs from several manufacturers, and finally mention the twin-T sharp rejection filter.

Most of the new active-filter ICs being introduced are of the switched-capacitor type, owing to their ease of use, small size, low cost, excellent stability, and (in some cases) complete absence of required external components. We conclude the chapter with a discussion of them.

### 6.3.1 VCVS circuits

The voltage-controlled voltage-source (VCVS) filter, also known simply as a controlled-source filter, was devised by Sallen and Key (and introduced in simplified form in §6.2.4E). It's a variation of the simpler unity-gain circuit shown earlier (Figure 6.16), in which the unity-gain follower is replaced with a noninverting amplifier of gain greater than unity. Figure 6.28 shows the circuits for lowpass, highpass, and bandpass realizations. The resistors at the outputs of the op-amps create a noninverting voltage amplifier of voltage gain $K$, with the remaining $R$ 's and $C$ 's contributing the frequency response properties for the filter. These are 2 -pole filters, and they can be Butterworth, Bessel, etc., by suitable choice of component values, as we show later. Any number of VCVS 2-pole sections may be cascaded to generate higher-order filters. When that is done, the individual filter sections are, in general, not identical. In fact, each section represents a quadratic polynomial factor of the $n$ th-order polynomial describing the overall filter.
image_name:A. low-pass filter
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: X1}
name: R2, type: Resistor, value: R2, ports: {N1: X1, N2: InP(A1)}
name: R3, type: Resistor, value: (K-1)R, ports: {N1: Out(A1), N2: InN(A1)}
name: R4, type: Resistor, value: R, ports: {N1: InN(A1), N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: X1, Nn: InP(A1)}
name: C2, type: Capacitor, value: C2, ports: {Np: InP(A1), Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Out(A1)}
]
extrainfo:This is a VCVS-based low-pass filter circuit. It uses an op-amp (A1) with feedback resistors and capacitors to achieve the desired filtering characteristics. The circuit is designed to allow low-frequency signals to pass while attenuating high-frequency signals.
image_name:B. high-pass filter
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: LOAD, Nn: X1}
name: R1, type: Resistor, value: R1, ports: {N1: X1, N2: InP}
name: R2, type: Resistor, value: R2, ports: {N1: InP, N2: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: InP, Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: InP, InN: InN, OutP: Out}
name: R, type: Resistor, value: R, ports: {N1: InN, N2: GND}
name: R, type: Resistor, value: (K-1)R, ports: {N1: Out, N2: InN}
]
extrainfo:This is a high-pass filter circuit using a VCVS (Voltage Controlled Voltage Source) configuration. The circuit includes capacitors and resistors to define the frequency response, and an op-amp for gain. The filter is designed to allow high frequencies to pass while attenuating low frequencies.
image_name:C. bandpass filter
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: LOAD, N2: X1}
name: C1, type: Capacitor, value: C1, ports: {Np: X1, Nn: X1}
name: R3, type: Resistor, value: R3, ports: {N1: X1, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: X1, N2: InP(A1)}
name: C2, type: Capacitor, value: C2, ports: {Np: X1, Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Out(A1)}
name: R, type: Resistor, value: R, ports: {N1: InN(A1), N2: GND}
name: R, type: Resistor, value: (K-1)R, ports: {N1: Out(A1), N2: InN(A1)}
]
extrainfo:The circuit diagram is a bandpass filter using a VCVS (Voltage Controlled Voltage Source) configuration. It includes resistors and capacitors to set the frequency response and an operational amplifier for gain. The filter is designed to allow a specific band of frequencies to pass while attenuating frequencies outside this range.

Figure 6.28. VCVS active-filter circuits.

There are design equations and tables in most standard filter handbooks for all the standard filter responses, usually including separate tables for each of a number of ripple amplitudes for Chebyshev filters. In the next section we present an easy-to-use design table for VCVS filters of Butterworth, Bessel, and Chebyshev responses ( 0.5 dB and 2 dB passband ripple for Chebyshev filters) for use as lowpass or highpass filters. Bandpass and band-reject filters can be made from combinations of these.

### 6.3.2 VCVS filter design using our simplified table

To use Table 6.2 to make a lowpass or a highpass filter, begin by deciding which filter response you need. As we mentioned earlier, the Butterworth may be attractive if maximum flatness of passband is desired, the Chebyshev gives the fastest rolloff from passband to stopband (at the expense of some ripple in the passband), and the Bessel provides the best phase characteristics, i.e., constant signal delay in the passband, with correspondingly good step
response. The frequency responses for all types are shown in the accompanying graphs (Figure 6.30).

#### Table 6.2 VCVS Lowpass Filters

| $\frac{\mathscr{0}}{\circ}$ | Butterworth K | Bessel |  | Chebyshev ( 0.5 dB ) |  | Chebyshev (2dB) |  |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
|  |  | $c$ | K | $c$ | K | $c$ | K |
| 2 | 1.586 | 1.272 | 1.268 | 1.231 | 1.842 | 0.907 | 2.114 |
| 4 | 1.152 | 1.432 | 1.084 | 0.597 | 1.582 | 0.471 | 1.924 |
|  | 2.235 | 1.606 | 1.759 | 1.031 | 2.660 | 0.964 | 2.782 |
| 6 | 1.068 | 1.607 | 1.040 | 0.396 | 1.537 | 0.316 | 1.891 |
|  | 1.586 | 1.692 | 1.364 | 0.768 | 2.448 | 0.730 | 2.648 |
|  | 2.483 | 1.908 | 2.023 | 1.011 | 2.846 | 0.983 | 2.904 |
| 8 | 1.038 | 1.781 | 1.024 | 0.297 | 1.522 | 0.238 | 1.879 |
|  | 1.337 | 1.835 | 1.213 | 0.599 | 2.379 | 0.572 | 2.605 |
|  | 1.889 | 1.956 | 1.593 | 0.861 | 2.711 | 0.842 | 2.821 |
|  | 2.610 | 2.192 | 2.184 | 1.006 | 2.913 | 0.990 | 2.946 |

To construct an $n$-pole filter (for $n$ an even integer), you will need to cascade $n / 2$ VCVS sections. Within each section, $R_{1}=R_{2}=R$, and $C_{1}=C_{2}=C$. As is usual in op-amp circuits, $R$ will typically be chosen in the range 10 k to 100 k . (It is best to avoid small resistor values, because the rising open-loop output impedance of the op-amp at high frequencies adds to the resistor values and upsets calculations.) Then all you need to do is set the gain, $K$, of each stage according to the table entries. For an $n$-pole filter there are $n / 2$ entries, one for each section.

#### A. Butterworth lowpass filters

If the filter is a Butterworth, all sections have the same values of $R$ and $C$, given simply by $R C=1 / 2 \pi f_{\mathrm{c}}$, where $f_{\mathrm{c}}$ is the desired -3 dB frequency of the entire filter. To make a 6-pole lowpass Butterworth filter, for example, you cascade three of the lowpass sections shown previously, with gains of $1.07,1.59$, and 2.48 (preferably in that order, to avoid dynamic range problems), and with identical $R$ 's and $C$ 's to set the 3 dB point.

#### B. Bessel and Chebyshev lowpass filters

To make a Bessel or Chebyshev filter with the VCVS, the situation is only slightly more complicated. Again we cascade several 2-pole VCVS filters, with prescribed gains for each section. Within each section we again use $R_{1}=R_{2}=R$ and $C_{1}=C_{2}=C$. However, unlike the situation with the Butterworth, the $R C$ products for the different sections are different and must be scaled by the normalizing factor $c_{\mathrm{n}}$ (given for each section in Table 6.2 on this page) according
to $R C=1 / 2 \pi c_{\mathrm{n}} f_{\mathrm{c}}$. Here $f_{\mathrm{c}}$ is again the -3 dB point for the Bessel filter, whereas for the Chebyshev filter it defines the end of the passband, i.e., it is the frequency at which the amplitude response falls out of the ripple band on its way into the stopband. For example, the response of a Chebyshev lowpass filter with 0.5 dB ripple and $f_{\mathrm{c}}=100 \mathrm{~Hz}$ will be flat within +0 dB to -0.5 dB from dc to 100 Hz , with 0.5 dB attenuation at 100 Hz and a rapid falloff for frequencies greater than 100 Hz . Values are given for Chebyshev filters with 0.5 dB and 2.0 dB passband ripple; the latter have a somewhat steeper transition into the stopband (Figure 6.30).
image_name:Figure 6.29
description:
[
name: C1, type: Capacitor, value: 10nF, ports: {Np: InP(A1), Nn: GND}
name: C2, type: Capacitor, value: 10nF, ports: {Np: X1, Nn: Out(A1)}
name: RA, type: Resistor, value: RA, ports: {N1: X2, N2: InP(A1)}
name: RB, type: Resistor, value: RB, ports: {N1: X1, N2: Out(A1)}
name: RGA, type: Resistor, value: 10k, ports: {N1: InN(A1), N2: GND}
name: RGB, type: Resistor, value: 10k, ports: {N1: InN(A2), N2: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Out(A1)}
name: A2, type: OpAmp, value: A2, ports: {InP: InP(A2), InN: InN(A2), OutP: Out(A2)}
]
extrainfo:This is a 4-pole VCVS lowpass filter with a cutoff frequency of 100 Hz. The filter characteristics are described for different resistor values for Bessel, Butterworth, and Chebyshev filter types. The diagram includes standard 1% resistor values for precise filter design.
image_name:4-pole lowpass f_c = 100 Hz
description:The image shows a circuit diagram of a 4-pole lowpass filter with a cutoff frequency \( f_c = 100 \, \text{Hz} \). The circuit is implemented using a Voltage-Controlled Voltage Source (VCVS) configuration and includes two operational amplifiers labeled \( A1 \) and \( A2 \). Each op-amp is part of an active filter stage.

Circuit Components:
- **Capacitors**: Two capacitors \( C1 \) and \( C2 \) are present in each stage, both with a value of \( 10 \, \text{nF} \). They are connected to ground.
- **Resistors**: Several resistors are used in the circuit, labeled as \( R_A, R_B, R_{GA}, \) and \( R_{GB} \). Each op-amp stage has feedback resistors and ground connections.

Connections:
- **Input and Output**: The input signal enters at \( \text{InP}(A1) \) and the output is taken from \( \text{Out}(A2) \).
- **Feedback**: The feedback loop involves resistors and capacitors, providing the necessary filtering characteristics.

Table of Resistor Values:
The image includes a table listing resistor values for different filter types:
- **Bessel Filter**:
- \( R_A = 110 \, \text{k}\Omega \)
- \( R_{GA} = 845 \, \Omega \)
- \( R_B = 100 \, \text{k}\Omega \)
- \( R_{GB} = 7.68 \, \text{k}\Omega \)
- Gain = 1.91
- **Butterworth Filter**:
- \( R_A = 158 \, \text{k}\Omega \)
- \( R_{GA} = 1.54 \, \text{k}\Omega \)
- \( R_B = 158 \, \text{k}\Omega \)
- \( R_{GB} = 12.4 \, \text{k}\Omega \)
- Gain = 2.57
- **Chebyshev Filter (0.5 dB)**:
- \( R_A = 267 \, \text{k}\Omega \)
- \( R_{GA} = 5.76 \, \text{k}\Omega \)
- \( R_B = 154 \, \text{k}\Omega \)
- \( R_{GB} = 16.5 \, \text{k}\Omega \)
- Gain = 4.21

The diagram effectively illustrates how different resistor values are used to achieve specific filter characteristics, such as Bessel, Butterworth, and Chebyshev, with the given cutoff frequency.

Figure 6.29. VCVS lowpass filter example. Resistor values shown are the nearest standard 1\% values (known as "E96").

#### An example

As an illustration, Figure 6.29 shows a VCVS implementation of a 4-pole lowpass filter with $f_{\mathrm{c}}=100 \mathrm{~Hz}$; resistor values for three filter characteristics are listed, calculated as just described. We used a similar filter (6-pole Butterworth, $f_{\mathrm{c}}=90 \mathrm{~Hz}$ ) to create a precision $50-70 \mathrm{~Hz}$ sinewave from a digital square wave that was referenced to a crystal oscillator; the output was amplified and used to drive an astronomical telescope. ${ }^{26}$

#### C. Highpass filters

To make a highpass filter, use the highpass configuration shown previously, i.e., with the $R$ 's and $C$ 's interchanged. For Butterworth filters, everything else remains unchanged (use the same values for $R, C$, and $K$ ). For the Bessel and Chebyshev filters, the $K$ values remain the same, but the

[^5]image_name:A
description:The graph labeled "A" is a Bode plot depicting the amplitude response of Butterworth filters with varying pole numbers (n = 2, 4, 6, 8). The x-axis represents the normalized frequency on a logarithmic scale ranging from 0.1 to 10. The y-axis represents the amplitude response (V_out/V_in) on a logarithmic scale, ranging from 0.001 to 1.

**Overall Behavior and Trends:**
- The Butterworth filter is characterized by a maximally flat amplitude response in the passband, with no ripples, making it ideal for applications requiring a smooth response.
- As the pole number increases, the roll-off rate becomes steeper beyond the cutoff frequency, providing better attenuation of frequencies in the stopband.

**Key Features:**
- The cutoff frequency is normalized to 1, where the amplitude response is approximately 0.707 (or -3 dB point).
- For n = 2, the response begins to drop off gently after the cutoff frequency, while n = 8 shows a much sharper decline.
- The transition from passband to stopband becomes more abrupt with higher pole numbers, indicating increased selectivity.

**Annotations and Specific Data Points:**
- The graph includes annotations for each pole number, showing the distinct curves for n = 2, 4, 6, and 8.
- The Butterworth filter's characteristic smooth curve is evident, with each curve labeled accordingly for clarity.
image_name:B
description:The graph labeled "B" is a Bode plot representing the amplitude response of Bessel filters with varying pole numbers. The plot is set on a logarithmic scale for both axes. The x-axis is labeled "Normalized Frequency" and spans from 0.1 to 10, while the y-axis is labeled "Amplitude Response V_out/V_in" and ranges from 0.001 to 1.

This graph illustrates the frequency response of Bessel filters with different numbers of poles (n = 2, 4, 6, 8). Each curve represents a filter with a specific number of poles, showing how the amplitude response changes with frequency.

**Overall Behavior and Trends:**
- The curves depict a smooth roll-off as frequency increases, characteristic of Bessel filters which are known for their maximally flat group delay.
- As the number of poles increases, the roll-off becomes steeper, indicating a sharper transition from passband to stopband.

**Key Features and Technical Details:**
- All curves start at an amplitude response of 1 at low frequencies and decrease as frequency increases.
- The cutoff frequency, where the amplitude response begins to significantly decline, is around the normalized frequency of 1.
- There is no ripple in the passband, maintaining a flat response until the cutoff.

**Annotations and Specific Data Points:**
- The graph is annotated with the number of poles (n = 2, 4, 6, 8) for each curve, providing insight into how the filter order affects the filter's performance.

This graph is useful for understanding the trade-offs in filter design, particularly in applications where phase linearity is crucial, such as in audio processing and communications.
image_name:C
description:The graph labeled "C" is a normalized frequency response plot for a Chebyshev filter with a 0.5 dB ripple. This plot is a Bode plot, which is commonly used to represent the amplitude response of filters.

1. **Type of Graph and Function:**
- This is a Bode plot showing the amplitude response of a Chebyshev filter.

2. **Axes Labels and Units:**
- The x-axis represents the normalized frequency on a logarithmic scale, ranging from 0.1 to 10.
- The y-axis represents the amplitude response \( V_{out}/V_{in} \) also on a logarithmic scale, ranging from 0.001 to 1.

3. **Overall Behavior and Trends:**
- The graph shows the frequency response for different pole numbers (n = 2, 4, 6, 8), with each line representing a different pole count.
- As the frequency increases past the cutoff frequency (normalized to 1), the amplitude response decreases sharply.
- The attenuation becomes steeper with higher pole numbers, indicating a faster roll-off.

4. **Key Features and Technical Details:**
- The Chebyshev filter exhibits a ripple in the passband, which is characteristic of this type of filter. In this plot, the ripple is set to 0.5 dB.
- The cutoff frequency is normalized to a value of 1, where the response begins to drop off.
- The graph shows that higher pole counts lead to a sharper transition between the passband and stopband.

5. **Annotations and Specific Data Points:**
- The graph is annotated with the pole numbers (n = 2, 4, 6, 8) next to each corresponding line.
- The passband ripple is specified in the plot title as 0.5 dB.
image_name:D
description:The graph labeled "D" is a Bode plot illustrating the normalized frequency response of Chebyshev filters with a 2.0 dB ripple. The plot is a log-log graph with the x-axis representing the normalized frequency (on a logarithmic scale from 0.1 to 10) and the y-axis representing the amplitude response (V_out/V_in) on a logarithmic scale from 0.001 to 1.0.

Overall Behavior and Trends:
- The plot shows the frequency response curves for Chebyshev filters with different pole numbers (n = 2, 4, 6, 8).
- The amplitude response starts near unity at low frequencies and decreases as the frequency increases, indicative of a highpass filter characteristic.
- Each curve exhibits ripples in the passband region due to the Chebyshev filter design, which allows for a sharper cutoff at the expense of passband ripples.

Key Features and Technical Details:
- The ripple in the passband is set at 2.0 dB, which is reflected in the amplitude fluctuations before the cutoff frequency.
- As the order of the filter (n) increases, the transition from passband to stopband becomes steeper, enhancing the filter's selectivity.
- The curves demonstrate that higher-order filters provide better attenuation in the stopband while maintaining the desired passband characteristics.

Annotations and Specific Data Points:
- The graph includes annotations for each filter order (n = 2, 4, 6, 8), indicating the respective curves.
- The unity gain point is marked at a normalized frequency of 1.0, where the amplitude response begins to decrease significantly.
- The gridlines help in estimating the cutoff frequencies and the rate of attenuation beyond the passband.

Figure 6.30. Normalized frequency response graphs for the 2-, 4-, 6-, and 8-pole filters in Table 6.2. The Butterworth and Bessel filters are normalized to 3 dB attenuation at unit frequency, whereas the Chebyshev filters are normalized to 0.5 dB and 2 dB attenuations. As explained earlier, the top of the ripple band in the Chebyshev plots has been set to unity.
normalizing factors $c_{\mathrm{n}}$ must be inverted, i.e., for each section the new $c_{\mathrm{n}}$ equals $1 /\left(c_{\mathrm{n}}\right.$ listed in Table 6.2 on the preceding page).

A bandpass filter can be made by cascading overlapping lowpass and highpass filters. A band-reject filter can be made by summing the outputs of nonoverlapping lowpass and highpass filters. However, such cascaded filters won't work well for high- $Q$ filters (extremely sharp bandpass filters) because there is great sensitivity to the component values in the individual (uncoupled) filter sections. In such cases a high- $Q$ single-stage bandpass circuit (e.g., the VCVS bandpass circuit illustrated previously, or the state-variable and biquad filters in the next section) should be used instead. Even a single-stage 2-pole filter can produce a response with an extremely sharp peak. Information on such filter design is available in the standard references.

#### D. Generalizing the Sallen-and-Key filter

A design simplification in these Sallen-and-Key (or VCVS) filter circuits was the use of identical resistor and capacitor values within each 2-pole filter stage; but with that simplification came a set of oddball amplifier gains, as seen in the "Gain" column in Figure 6.29.

Often you want to set the filter's gain, for example to prevent saturation, or so that you can change the filter characteristics (by a change of component value) without altering the gain. When you constrain the gain, however, you have to relax the component ratio constraint. You can learn all about this in a pair of nice Application Notes by James Karki from TI. ${ }^{27}$ The bottom line is that (just as with the preceding VCVS circuits) you can create any filter

[^6]characteristic, using amplifier stages with your choice of gain, providing you are willing to adjust the resistor and capacitor ratios.

Following Karki's analysis, we can write down summary formulas for the transition frequency $f_{\mathrm{c}}$ and $Q$ of a 2-pole Sallen-Key section in which the component ratios can take on arbitrary values. Following the naming convention $^{28}$ of Figure 6.28A, we define parameters $m, n$, and $\tau$ (which will make the final results prettier):

$$
m=R_{1} / R_{2}, n=C_{1} / C_{2}, \text { and } \tau=R_{2} C_{2}
$$

With these definitions, a 2-pole filter section has a transition frequency

$$
\begin{equation*}
f_{c}=\frac{1}{2 \pi \tau \sqrt{m n}} \tag{6.5}
\end{equation*}
$$

and a $Q$ (sharpness of transition, or peakiness) of

$$
\begin{equation*}
Q=\frac{\sqrt{m n}}{1+m+m n(1-K)} \tag{6.6}
\end{equation*}
$$

These results alone are not enough for you to design higher-order filter cascades with canonical filter shapes (Chebyshev, etc.); for that you can consult the tables in Karki's App Note SLOA049B, or (for more fun) use a filter-design program. But these expressions demonstrate the point that you can trade off one set of constraints for another. Note particularly the attractive case of unity gain ( $K=1$ ), for which the gain elements can be wideband unitygain buffer ICs, or simple discrete-transistor followers. ${ }^{29}$

Revisiting the earlier constraint we used with the VCVS table (i.e., $R_{1}=R_{2}=R, C_{1}=C_{2}=C$ ), these formulas reduce to the simple forms

$$
\begin{equation*}
f_{c}=\frac{1}{2 \pi R C}, \quad Q=\frac{1}{3-K} \tag{6.7}
\end{equation*}
$$

for which the circuit goes unstable $(Q \rightarrow \infty)$ when $K=3$. Note that such a circuit, with the gain $K$ further constrained to unity (i.e., a follower, as we illustrated in Figure 6.16 to introduce the idea of an active filter) produces a pretty anemic filter, with a $Q$ of just one half.

#### E. Summary

VCVS filters minimize the number of components needed (two poles per op-amp) and offer the additional advantages of noninverting gain, low output impedance, small

[^7]spread of component values, easy adjustability of gain, and the ability to operate at high gain or high $Q$. They suffer from sensitivity to component values and amplifier gain, and they don't lend themselves well to applications where a tunable filter of stable characteristics is needed. And they require op-amps whose bandwidth ( $f_{\mathrm{T}}$, or GBW) is much higher than $f_{\mathrm{c}}$ of the filter. ${ }^{30}$ Some of these drawbacks are nicely remedied in the state-variable and biquad filters.

Exercise 6.3. Design a 6-pole Chebyshev lowpass VCVS filter with a 0.5 dB passband ripple and 100 Hz cutoff frequency $f_{\mathrm{c}}$. What is the attenuation at $1.5 f_{\mathrm{c}}$ ?

### 6.3.3 State-variable filters

The 2-pole filter shown in Figure 6.31 is far more complex than the VCVS circuits, but it is popular because of its improved stability and ease of adjustment. It is called a state-variable filter and was originally available as an IC from National (the AF100 and AF150, now discontinued); you can get it from Burr-Brown/TI (the UAF42), and a closely similar part is made by Maxim (MAX274-5). Because it is a manufactured module, all components except $R_{\mathrm{G}}, R_{\mathrm{Q}}$, and the two $R_{\mathrm{F}}$ 's are built in. Among its nice properties is the availability of highpass, lowpass, and bandpass outputs from the same circuit; also, its frequency can be tuned while maintaining constant $Q$ (or, alternatively, constant bandwidth) in the bandpass characteristic. As with the VCVS realizations, multiple stages can be cascaded to generate higher-order filters. The frequency can be made adjustable with a dual pot for the $R_{\mathrm{F}}$ pair. But, given the inverse $(1 / R)$ frequency tuning, you may prefer a linear scheme like that shown in Figure 6.34, where you could use either a dual pot or a dual multiplying DAC (see §6.3.3C).

Extensive design formulas and tables are provided by the manufacturers for the use of these convenient ICs. They show how to choose the external resistor values to make Butterworth, Bessel, and Chebyshev filters for a wide range of filter orders, with lowpass, highpass, bandpass, or bandreject responses. Among the nice features of these hybrid ICs is integration of the capacitors into the module, ${ }^{31}$ so that only external resistors need be added.

[^8]image_name:Figure 6.31
description:
[
name: RG, type: Resistor, value: RG, ports: {N1: input, N2: InN(A1)}
name: R2, type: Resistor, value: 10k, ports: {N1: InN(A1), N2: out(A2)}
name: R3, type: Resistor, value: 100k, ports: {N1: out(A2), N2: InN(A2)}
name: RF, type: Resistor, value: RF, ports: {N1: HP, N2: InN(A2)}
name: RQ, type: Resistor, value: RQ, ports: {N1: InP(A1), N2: GND}
name: CF, type: Capacitor, value: 1000pF, ports: {Np: InN(A2), Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: HP, OutN: GND}
name: A2, type: OpAmp, value: A2, ports: {InP: InN(A2), InN: out(A2), OutP: LP, OutN: GND}
name: A3, type: OpAmp, value: A3, ports: {In: HP, OutP: BP, OutN: GND}
]
extrainfo:The circuit is a state-variable active filter used as a bandpass filter. The center frequency is set by RF, and RQ and RG determine the quality factor Q. The circuit is designed for sharp bandpass filtering with low component sensitivity.

Figure 6.31. State-variable active filter.

#### A. Bandpass filters

The state-variable circuit, in spite of its large number of components, is a good choice for sharp (high- $Q$ ) bandpass filters. It has low component sensitivities, does not make great demands on op-amp bandwidth, and is easy to tune. For example, in the circuit of Figure 6.31 used as a bandpass filter, the two resistors $R_{\mathrm{F}}$ set the center frequency, and $R_{\mathrm{Q}}$ and $R_{\mathrm{G}}$ together determine the $Q$ and band-center gain:

$$
\begin{align*}
& R_{\mathrm{F}}=5.03 \times 10^{7} / f_{0} \quad \text { ohms }  \tag{6.8}\\
& R_{\mathrm{Q}}=10^{5} /(3.48 Q+G-1) \quad \text { ohms }  \tag{6.9}\\
& R_{\mathrm{G}}=3.16 \times 10^{4} Q / G \quad \text { ohms } \tag{6.10}
\end{align*}
$$

So you could make a tunable-frequency, constant- $Q$ filter by using a 2 -section variable resistor (pot) for $R_{\mathrm{F}}$. Alternatively, you could make $R_{\mathrm{Q}}$ adjustable, producing a fixedfrequency, variable- $Q$ (and, unfortunately, variable-gain) filter.
image_name:Figure 6.32
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Out(A1), N2: InN(A1)}
name: RQ, type: Resistor, value: RQ, ports: {N1: InN(A1), N2: InP(A1)}
name: RG, type: Resistor, value: RG, ports: {N1: InP(A1), N2: input}
name: R, type: Resistor, value: R, ports: {N1: Out(A1), N2: InP(A2)}
name: R, type: Resistor, value: R, ports: {N1: Out(A2), N2: InN(A4)}
name: RF, type: Resistor, value: RF, ports: {N1: Out(A2), N2: InN(A3)}
name: RF, type: Resistor, value: RF, ports: {N1: Out(A4), N2: InN(A4)}
name: C, type: Capacitor, value: C, ports: {Np: Out(A3), Nn: InN(A3)}
name: C, type: Capacitor, value: C, ports: {Np: Out(A4), Nn: InN(A4)}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: InN(A1), OutP: Out(A1), OutN: GND}
name: A2, type: OpAmp, value: A2, ports: {InP: InP(A2), InN: GND, OutP: Out(A2), OutN: GND}
name: A3, type: OpAmp, value: A3, ports: {InP: Out(A2), InN: InN(A3), OutP: Out(A3), OutN: GND}
name: A4, type: OpAmp, value: A4, ports: {InP: Out(A2), InN: InN(A4), OutP: Out(A4), OutN: GND}
]
extrainfo:The circuit is a state-variable bandpass filter with independently settable gain and Q. It uses four op-amps and allows for tuning the bandwidth without affecting the midband gain. The center frequency is determined by the formula f0 = 1/(2πRFC). The circuit is designed to produce a bandpass output.

Figure 6.32. A filter with independently settable gain and $Q$.

Exercise 6.4. Calculate resistor values in Figure 6.32 to make a bandpass filter with $f_{0}=1 \mathrm{kHz}, Q=50$, and $G=10$.

Figure 6.32 shows a useful variant of the state-variable bandpass filter. The bad news is that it uses four op-amps; the good news is that you can adjust the bandwidth (i.e., $Q$ ) without affecting the midband gain. In fact, both $Q$ and gain are set with a single resistor each. The $Q$, gain, and center frequency are completely independent and are given by these simple equations:

$$
\begin{align*}
f_{0} & =1 / 2 \pi R_{\mathrm{F}} C  \tag{6.11}\\
Q & =R_{1} / R_{\mathrm{Q}}  \tag{6.12}\\
G & =R_{1} / R_{\mathrm{G}}  \tag{6.13}\\
R & \approx 10 \mathrm{k} \quad \text { (noncritical, matched) } . \tag{6.14}
\end{align*}
$$

Biquad filter
A close relative of the state-variable filter is the so-called biquad filter, shown in Figure 6.33. This circuit also uses three op-amps and can be constructed from the statevariable ICs mentioned earlier. It has the interesting property that you can tune its frequency ( via $R_{\mathrm{F}}$ ) while maintaining constant bandwidth (rather than constant $Q$ ). Here are the design equations:

$$
\begin{align*}
f_{0} & =1 / 2 \pi R_{\mathrm{F}} C,  \tag{6.15}\\
\mathrm{BW} & =1 / 2 \pi R_{\mathrm{B}} C,  \tag{6.16}\\
G & =R_{\mathrm{B}} / R_{\mathrm{G}} . \tag{6.17}
\end{align*}
$$

The $Q$ is given by $f_{0} / \mathrm{BW}$ and equals $R_{\mathrm{B}} / R_{\mathrm{F}}$. As the center frequency is varied (via $R_{\mathrm{F}}$ ), the $Q$ varies proportionately, keeping the bandwidth $f_{0} / Q$ constant.
image_name:Figure 6.33
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: Out(A2), InN: GND, OutP: Out(A1), OutN:}
name: A2, type: OpAmp, value: A2, ports: {InP: GND, InN: InV(A2), OutP: Out(A2), OutN:}
name: A3, type: OpAmp, value: A3, ports: {In: Out(A2), OutP: Out, OutN:}
name: RF1, type: Resistor, value: RF, ports: {N1: Out(A1), N2: InV(A1)}
name: RF2, type: Resistor, value: RF, ports: {N1: Out(A1), N2: InV(A3)}
name: RB, type: Resistor, value: RB, ports: {N1: InV(A2), N2: Out(A1)}
name: RG, type: Resistor, value: RG, ports: {N1: input, N2: InV(A2)}
name: R, type: Resistor, value: R, ports: {N1: Out(A2), N2: Out}
name: C1, type: Capacitor, value: C, ports: {Np: Out(A1), Nn: Out(A2)}
name: C2, type: Capacitor, value: C, ports: {Np: Out(A2), Nn: GND}
]
extrainfo:The circuit is a biquad active filter with three operational amplifiers (A1, A2, A3). It uses resistors RF, RB, RG, and R, and capacitors C to achieve filtering. The center frequency is determined by RF and C, while the bandwidth is controlled by RB. The filter maintains constant bandwidth as the center frequency varies. The output is taken from A3.

Figure 6.33. Biquad active filter.
When you design a biquad filter from scratch (rather than with an active-filter IC that already contains most of the parts), the general procedure goes something like this.
(1) Choose an op-amp whose bandwidth $f_{\mathrm{T}}$ is at least 10 to 20 times $G f_{0}$.
(2) Pick a round-number capacitor value in the vicinity of $C=10 / f_{0} \mu \mathrm{~F}$, where $f_{0}$ is in Hz .
(3) Use the desired center frequency to calculate the corresponding $R_{\mathrm{F}}$ from eq'n 6.15 .
(4) Use the desired bandwidth to calculate $R_{\mathrm{B}}$ from eq'n 6.16.
(5) Use the desired band-center gain to calculate $R_{\mathrm{G}}$ from eq'n 6.17.

You may have to adjust the capacitor value if the resistor values become awkwardly large or small. For instance, in a high- $Q$ filter you may need to increase $C$ somewhat to keep $R_{\mathrm{B}}$ from becoming too large (or you can use the T-network trick described in $\S 4.5 .5$ ). Note that $R_{\mathrm{F}}, R_{\mathrm{B}}$, and $R_{\mathrm{G}}$ each act as op-amp loads, and so they ought not to become less than, say, 5k. When juggling component values, you may find it easier to satisfy requirement (1) by decreasing integrator gain (increase $R_{\mathrm{F}}$ ) and simultaneously increasing the inverter-stage gain (increase the 10k feedback resistor).

As an example, suppose we want to make a filter with the same characteristics as in Exercise 6.4 on page 411. We would begin by provisionally choosing $C=0.01 \mu \mathrm{~F}$. Then we find $R_{\mathrm{F}}=15.9 \mathrm{k}\left(f_{0}=1 \mathrm{kHz}\right)$ and $R_{\mathrm{B}}=796 \mathrm{k}(Q=50$; $\mathrm{BW}=20 \mathrm{~Hz})$. Finally, $R_{\mathrm{G}}=79.6 \mathrm{k}(G=10)$.

Exercise 6.5. Design a biquad bandpass filter with $f_{0}=60 \mathrm{~Hz}$, $\mathrm{BW}=1 \mathrm{~Hz}$, and $G=100$.

#### B. Higher-order bandpass filters

As with our earlier lowpass and highpass filters, it is possible to build higher-order bandpass filters with approximately flat bandpass and steep transition to the stopband.

You do this by cascading several lower-order bandpass filters, the combination tailored to realize the desired filter type (Butterworth, Chebyshev, or whatever). As before, the Butterworth is "maximally flat," whereas the Chebyshev sacrifices passband flatness for steepness of skirts. Both the VCVS and state-variable/biquad bandpass filters just considered are second-order (two pole). As you increase the filter sharpness by adding sections, you generally degrade the transient response and phase characteristics. The "bandwidth" of a bandpass filter is defined as the width between -3 dB points, except for equiripple filters, for which it is the width between frequencies at which the response falls out of the passband ripple channel.

You can find tables and design procedures for constructing complex filters in standard books on active filters, or in the datasheets for active-filter ICs. There are also some very nice filter-design programs, including shareware and
freeware versions that run on standard PCs and workstations.
image_name:Figure 6.34
description:
[
name: k, type: Resistor, value: k, ports: {N1: GND, N2: Node1}
name: RF, type: Resistor, value: RF, ports: {N1: Node2, N2: Node3}
name: OpAmp, type: OpAmp, ports: {InP: Node1, InN: Node2, OutP: Node3}
]
extrainfo:The circuit diagram is a state-variable active filter with tunable frequency. It uses an operational amplifier with feedback resistors for filtering applications. The resistor 'k' is connected to ground, and the feedback resistor 'RF' is connected to the output of the op-amp.

Figure 6.34. Tuning the frequency of the state-variable active filter. The op-amp buffer can be omitted if strict linearity with pot rotation is not needed.

#### C. Electronic tunability

Sometimes you want electrical tunability (or switchability) so you can change filter characteristics under control of a signal (rather than having to turn the shaft on a variable resistor). An example might be an anti-alias lowpass filter that precedes a digitizer, in which the digitizing rate $f_{\text {samp }}$ can be varied over some range. In that case the filter's $f_{\mathrm{c}}$ must be set to follow the Nyquist frequency, $f_{\mathrm{c}} \approx f_{\text {samp }} / 2$ (see $\S \S 6.2 .3 \mathrm{C}, 6.3 .7 \mathrm{~A}$, and 13.5.1B). In active-filter circuits like the VCVS you can do this, to a limited extent, by using analog switches to select among a small set of fixed resistors, each of which substitutes for one of the resistors in the filter. But the state variable filters provide a particularly convenient way to accomplish both switchability and continuous tuning, in one of several ways.
Digital potentiometer As we discussed in §3.4.3E, you can get convenient ICs that contain a long string of matched resistors, with MOSFET switches to select the voltage-divider tap (by means of digital control ${ }^{32}$ ). So you can effectively alter the value of a programming resistor (e.g., $R_{\mathrm{F}}$ in Figure 6.31) by preceding it with such a digital voltage divider (with a unity-gain follower, if needed to drive a low-value $R_{\mathrm{F}}$ ); see Figure 6.34. By using a dual digital pot ${ }^{33}$ you could adjust the pair of $R_{\mathrm{F}}$ 's simultaneously, as would be needed to tune $f_{0}$ in that bandpass circuit. Digital pots come with as many as 1024 taps, and they come in both linear and log spacing, so you can achieve pretty accurate electronic control. Digital pots do not provide particularly accurate overall resistance values (typically $\pm 20 \%$ ), but they do guarantee accurate and stable control of divider ratio ( $1 \%$ or

[^9]better); i.e., the resistors that make up the string are well matched. That is why they work well in this application, in which only the ratio is important.
Multiplying DAC Another way to effectively vary $R_{\mathrm{F}}$ in the state-variable filter is to use a multiplying DAC (digital-to-analog converter), rather than a programmable divider, to scale the op-amp's voltage output. The MDAC outputs a voltage (or a current, in some models) that is proportional to the product of an analog input voltage and a digital input quantity. Compared with the digital pot, the MDAC method provides higher resolution (finer step size), faster response, and (often) wider voltage range.
Analog switch If only a discrete set of filter parameters is desired, you can just use a set of MOSFET analog multiplexers to select among a preselected group of programming resistors. Don't forget to consider the effects of finite $R_{\mathrm{ON}}$.
Integrated switchability There are a few active-filter ICs that provide for programmable cutoff frequency, by a digital code you apply to a set of programming pins. You don't get continuous control, but you sure save a lot of work (and a lot of parts). In this class are the LTC1564 (8-pole elliptic lowpass), which lets you select the cutoff frequency from 10 kHz to 150 kHz in 10 kHz steps, and the MAX270 (dual 2-pole lowpass), which lets you select the cutoff frequency among 128 steps going from 1 kHz to 25 kHz .

#### Electronic tuning alternatives: switched-capacitor filters and DSP

The above techniques achieve electronic tunability by presenting the continuous-time filter with an effectively variable set of programming resistors. When thinking about electronic tuning, it's wise to consider switched-capacitor filters and digital signal processing (DSP), in both of which electronic tunability is inherent. These are discussed later in this chapter (§6.3.6 and 6.3.7).

#### D. Multiple-feedback active filter

In addition to the VCVS (Sallen-and-Key) and statevariable (or biquad) active-filter circuit configurations, there's another active-filter circuit that's commonly used. It's called the "multiple-feedback" (MFB) active filter (also known as the "infinite-gain multiple-feedback"), and is shown in Figure 6.35. Here the op-amp is configured as an integrator, rather than as a voltage amplifier (or follower). Designing an MFB filter is no more difficult than designing a VCVS, and you can find nice filter software that supports both configurations, for example at the very fine website of

Uwe Beis (see §6.3.8). You can get nice MFB filter ICs, for example the LTC1563, an inexpensive (\$2.30) linearfilter IC using the MFB configuration, convenient for making anti-alias filters, etc. The ' $1563-2$ version makes 4 - and 5-pole Butterworth filters, from 256 Hz to 360 kHz , and the -3 version makes Bessel filters. The ICs use internal 27 pF to 54 pF capacitors trimmed to $3 \%$, combined with your external 7 k to $10 \mathrm{M} 1 \%$ resistors. The datasheet is especially instructive.
image_name:Figure 6.35
description:
[
name: R, type: Resistor, value: R, ports: {N1: in, N2: X1}
name: R, type: Resistor, value: R, ports: {N1: X1, N2: out}
name: R/2, type: Resistor, value: R/2, ports: {N1: X1, N2: InN(A1)}
name: C, type: Capacitor, value: C, ports: {Np: out, Nn: InN(A1)}
name: 4C, type: Capacitor, value: 4C, ports: {Np: X1, Nn: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: out, OutN: GND}
]
extrainfo:The circuit is a multiple-feedback (MFB) active filter in a 2-pole lowpass configuration with a cutoff frequency of 1 kHz. It uses resistors and capacitors to set the frequency response, and an op-amp to provide gain and feedback.

$$
\left.\begin{array}{l}
R=20 \mathrm{k} \\
C=5.6 \mathrm{nF}
\end{array}\right\} f_{\mathrm{C}}=1 \mathrm{kHz}
$$

Figure 6.35. Multiple-feedback (MFB) active filter, here shown in a 2-pole lowpass configuration.

This configuration has an interesting advantage compared with the VCVS: as you go to high frequencies, approaching the bandwidth $f_{\mathrm{T}}$ of the op-amp, the degrading effects of rising op-amp output impedance are less severe. We ran SPICE simulations of VCVS and MFB 2pole Butterworth lowpass filters (Figures 6.36 and 6.37), which show this effect nicely. We set the cutoff frequency at 4 kHz , well below the LF411's unity-gain frequency $\left(f_{\mathrm{T}}\right)$ of 4 MHz . In the VCVS configuration the op-amp's rising $Z_{\text {out }}$ allows input signal to couple to the output through the first capacitor, a path that is absent in the MFB configuration. ${ }^{34}$ In many applications, however, this is not a serious worry. And the effect is reduced as the resistor values of the filter are increased, as shown in Figure 6.36. The VCVS configuration is alive and well, and remains popular. ${ }^{35}$

[^10]image_name:Figure 6.36
description:The graph in Figure 6.36 is a Bode plot that illustrates the gain (in decibels) versus frequency (in hertz) for a VCVS (voltage-controlled voltage source) 4 kHz low-pass 2-pole Butterworth filter using an LF411 op-amp with a unity-gain frequency of 4 MHz. The x-axis represents frequency on a logarithmic scale, ranging from 100 Hz to 10 MHz, while the y-axis represents gain in decibels, ranging from 0 dB to -100 dB.

The plot shows three curves corresponding to different resistor values: 1.8kΩ, 18kΩ, and 180kΩ. Each curve demonstrates the filter's behavior as the resistor value changes. At lower frequencies, all curves start with a gain of 0 dB, indicating no attenuation in the passband.

As frequency increases, the gain begins to decrease, indicating the onset of the filter's cutoff region. The cutoff frequency is around 4 kHz, consistent with the design of a 2-pole Butterworth filter, which provides a smooth transition from passband to stopband.

The graph shows that the attenuation increases with frequency beyond the cutoff, but the rate of attenuation and the high-frequency behavior are affected by the resistor values. The curve for 1.8kΩ shows the least attenuation at high frequencies, while the 180kΩ curve exhibits the most significant attenuation, indicating that larger resistor values improve high-frequency attenuation by reducing the effect of the op-amp's rising output impedance.

Overall, the plot highlights how increasing resistor values can mitigate the degradation of high-frequency attenuation in the VCVS configuration, which is crucial for maintaining filter performance in various applications.

Figure 6.36. The rising closed-loop output impedance of the opamp degrades the high-frequency attenuation in the VCVS (Sallen-and-Key) configuration, by allowing some input signal to couple to the output through the input resistor and feedback capacitor ( $R_{1}$ and $C_{1}$ in Figure 6.28). Larger resistor values reduce the effect. See also Figure 6.37.
image_name:Figure 6.36
description:The graph in Figure 6.36 is a Bode plot displaying the gain (in decibels) versus frequency (in hertz) for different configurations of a 4kHz lowpass filter. The filter is a 2-pole Butterworth type, using an LF411 operational amplifier with a transition frequency (f_T) of 4MHz.

**Axes Labels and Units:**
- The x-axis represents frequency, ranging from 100 Hz to 10 MHz, on a logarithmic scale.
- The y-axis represents gain, ranging from 0 dB to -100 dB.

**Overall Behavior and Trends:**
- The graph shows a typical lowpass filter response, with the gain starting at 0 dB at low frequencies and decreasing as frequency increases.
- The transition from passband to stopband is smooth, with a notable attenuation slope starting around 4 kHz.

**Key Features and Technical Details:**
- The VCVS configuration with a resistor value of 18k exhibits a gain peak around 1 MHz, indicating a degradation in high-frequency attenuation due to rising op-amp output impedance.
- The VCVS configuration with an added buffer shows improved performance, maintaining better attenuation beyond 1 MHz.
- The MFB configuration with a resistor value of 28k shows consistent attenuation, with less impact from the op-amp's output impedance.

**Annotations and Specific Data Points:**
- The graph includes annotations for the different configurations: VCVS (R=18k), VCVS with buffer, and MFB (R=28k).
- A reference line indicates the improved attenuation performance of the VCVS with buffer and MFB configurations compared to the standard VCVS configuration at higher frequencies.

Figure 6.37. The stopband attenuation of the MFB configuration is not much affected by rising op-amp output impedance (e.g., as seen in Figure 4.53), compared with that of the VCVS. However, you can mitigate the effect in the VCVS by using a second opamp to create a buffered output from the signal at the op-amp's noninverting input.

### 6.3.4 Twin-T notch filters

The passive $R C$ network shown in Figure 6.38 has infinite attenuation at a frequency $f_{c}=1 / 2 \pi R C$. Infinite attenuation is uncharacteristic of $R C$ filters in general; this one works by effectively adding two signals that have been shifted $180^{\circ}$ out of phase at the cutoff frequency. It requires
good matching of components to obtain a good null at $f_{\mathrm{c}}$. It is called a twin-T, and it can be used to remove an interfering signal, such as 60 Hz powerline pickup. The problem is that it has the same "soft" cutoff characteristics as all passive $R C$ networks, except, of course, near $f_{\mathrm{c}}$, where its response drops like a rock. For example, a twin-T driven by a perfect voltage source is down 10 dB at twice (or half) the notch frequency and 3 dB at four times (or one-fourth) the notch frequency. One trick to improve its notch characteristic is to "activate" it in the manner of a Sallen-and-Key filter (Figure 6.39). This technique looks good in principle, but it is generally disappointing in practice, owing to the impossibility of maintaining a good filter null. As the filter notch becomes sharper (more gain in the bootstrap), its null becomes less deep.
image_name:Figure 6.38. Passive twin-T notch filter
description:
[
name: R1, type: Resistor, value: R, ports: {N1: in, N2: X1}
name: R2, type: Resistor, value: R, ports: {N1: X1, N2: out}
name: C1, type: Capacitor, value: 2C, ports: {Np: X1, Nn: GND}
name: C2, type: Capacitor, value: C, ports: {Np: in, Nn: X2}
name: C3, type: Capacitor, value: C, ports: {Np: X2, Nn: out}
name: R3, type: Resistor, value: R/2, ports: {N1: X2, N2: GND}
]
extrainfo:The circuit is a passive twin-T notch filter designed to attenuate a specific frequency. It consists of resistors and capacitors arranged in a 'T' configuration to create a notch filter.

Figure 6.38. Passive twin-T notch filter.
image_name:Figure 6.38. Passive twin-T notch filter
description:
[
name: R1, type: Resistor, value: R, ports: {N1: in, N2: X1}
name: R2, type: Resistor, value: R, ports: {N1: X1, N2: InP(A1)}
name: C1, type: Capacitor, value: C, ports: {Np: in, Nn: X2}
name: C2, type: Capacitor, value: C, ports: {Np: X2, Nn: out}
name: C3, type: Capacitor, value: 2C, ports: {Np: X1, Nn: X2}
name: R3, type: Resistor, value: R/2, ports: {N1: X2, N2: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: InP(A1), InN: GND, OutP: out}
name: A2, type: OpAmp, value: A2, ports: {InP: InP(A2), InN: GND, OutP: bootstrap}
]
extrainfo:The circuit is a passive twin-T notch filter designed to attenuate a specific frequency. It consists of resistors and capacitors arranged in a 'T' configuration to create a notch filter. The circuit includes two operational amplifiers (A1 and A2) to enhance the filter's performance. The bootstrap connection helps stabilize the circuit.

Figure 6.39. Bootstrapped twin-T.
Twin-T filters are available as prefab modules, going from 1 Hz to 50 kHz , with notch depths of about 60 dB (with some deterioration at high and low temperatures). They are easy to make from components, but resistors and capacitors of good stability and low temperature coefficient should be used to get a deep and stable notch. One of the components should be made trimmable.

The twin-T filter works fine as a fixed-frequency notch, but it is a horror to make tunable, because three resistors must be simultaneously adjusted while maintaining constant ratio. However, the remarkably simple $R C$ circuit of Figure 6.40A, which behaves just like the twin-T, can be
adjusted over a significant range of frequency (at least two octaves) with a single potentiometer. Like the twin-T (and most active filters) it requires some matching of components; in this case, the three capacitors must be identical, and the fixed resistor must be exactly six times the bottom (adjustable) resistor. The notch frequency is then given by

$$
f_{\text {notch }}=1 / 2 \pi C \sqrt{3 R_{1} R_{2}} .
$$

Figure 6.40B shows an implementation that is tunable from 25 Hz to 100 Hz . The 50 k trimmer is adjusted (once) for maximum depth of notch.
image_name:A
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: in, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: GND, N2: GND}
name: 6(R1+R2), type: Resistor, value: 6(R1+R2), ports: {N1: in, N2: out}
name: C, type: Capacitor, value: C, ports: {Np: in, Nn: GND}
name: C, type: Capacitor, value: C, ports: {Np: out, Nn: GND}
name: C, type: Capacitor, value: C, ports: {Np: in, Nn: out}
name: 50k, type: Resistor, value: 50k, ports: {N1: in, N2: trim}
name: 464k, type: Resistor, value: 464k, ports: {N1: trim, N2: out}
name: 1.0k, type: Resistor, value: 1.0k, ports: {N1: freq, N2: GND}
name: 20k, type: Resistor, value: 20k, ports: {N1: GND, N2: GND}
name: 60.4k, type: Resistor, value: 60.4k, ports: {N1: GND, N2: GND}
name: 0.1μF, type: Capacitor, value: 0.1μF, ports: {Np: in, Nn: GND}
name: 0.1μF, type: Capacitor, value: 0.1μF, ports: {Np: GND, Nn: GND}
name: 0.1μF, type: Capacitor, value: 0.1μF, ports: {Np: GND, Nn: out}
]
extrainfo:The circuit diagram (A) shows a bridged differentiator tunable-notch filter with a notch frequency given by the formula: f_notch = 1 / (2πC√3R1R2). Diagram (B) implements a tunable filter from 25 Hz to 100 Hz using a 50k trimmer for notch depth adjustment.
image_name:B
description:
[
name: 50k, type: Resistor, value: 50k, ports: {N1: in, N2: N1}
name: 464k, type: Resistor, value: 464k, ports: {N1: N1, N2: out}
name: 0.1µF, type: Capacitor, value: 0.1µF, ports: {N1: in, N2: N2}
name: 0.1µF, type: Capacitor, value: 0.1µF, ports: {N1: N2, N2: N1}
name: 0.1µF, type: Capacitor, value: 0.1µF, ports: {N1: N2, N2: out}
name: 20k, type: Resistor, value: 20k, ports: {N1: N2, N2: N3}
name: 1.0k, type: Resistor, value: 1.0k, ports: {N1: N3, N2: GND}
name: 60.4k, type: Resistor, value: 60.4k, ports: {N1: N3, N2: GND}
]
extrainfo:This is a bridged differentiator tunable-notch filter that can be tuned from 25 Hz to 100 Hz. The circuit uses a combination of resistors and capacitors to achieve a notch filter with infinite attenuation at the notch frequency, assuming perfect matching of component values.

Figure 6.40. Bridged differentiator tunable-notch filter. The implementation in (B) tunes from 25 Hz to 100 Hz .

As with the passive twin-T, this filter (known as a bridged differentiator) has a gently sloping attenuation away from the notch and infinite attenuation (assuming perfect matching of component values) at the notch frequency. It, too, can be "activated" by bootstrapping the wiper of the pot with a voltage gain somewhat less than unity (as in Figure 6.39). Increasing the bootstrap gain toward unity narrows the notch, but also leads to an undesirable response peak on the high-frequency side of the notch, along with a reduction in ultimate attenuation.

### 6.3.5 Allpass filters

Allpass? Allpass?! Whatever can that be? And why would you want such a thing, when a piece of wire does as well (and probably better)?

Allpass filters, also known as delay equalizers or phase equalizers, are filters with flat amplitude response, but with a phase shift that varies with frequency. They are used to compensate for phase shifts (or time delays) in some signal path.
image_name:Figure 6.41
description:
[
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: LOAD, OutP: OUT(A1), OutN: , Vdd: , -Vdd:}
name: R, type: Resistor, value: R, ports: {N1: LOAD, N2: GND}
name: C, type: Capacitor, value: C, ports: {Np: LOAD, Nn: InN(A1)}
]
extrainfo:The circuit is an allpass filter, also known as a delay equalizer or phase equalizer. It has a flat amplitude response and a phase shift that varies with frequency. The phase shift is leading when Δθ = 2 tan⁻¹(1/ωRC) and lagging if R and C are interchanged, Δθ = -2 tan⁻¹(ωRC).
image_name:
description:### Type of Graph and Function:
The graph is a phase response plot, typically used in analyzing allpass filters or phase equalizers. It shows the phase shift introduced by the filter as a function of frequency.

Axes Labels and Units:
- **Horizontal Axis (x-axis):** Represents the normalized frequency, labeled as \(2\pi fRC\), where \(f\) is frequency, \(R\) is resistance, and \(C\) is capacitance. The scale is logarithmic, spanning from 0.01 to 100.
- **Vertical Axis (y-axis):** Represents phase shift in degrees, ranging from -180° to 180°. The scale is linear.

Overall Behavior and Trends:
- The graph shows two phase response curves:
- The upper curve represents the phase shift when \(\Delta \theta = 2 \tan^{-1}(1/\omega RC)\), indicating a leading phase shift.
- The lower curve represents the phase shift when \(\Delta \theta = -2 \tan^{-1}(\omega RC)\), indicating a lagging phase shift.
- Both curves start at 0° phase shift at low frequencies and approach asymptotic limits of ±180° at high frequencies.

Key Features and Technical Details:
- **Leading Phase Shift Curve:**
- Begins at 0° and increases towards 180° as frequency increases.
- The transition region where phase shift changes rapidly is around \(2\pi fRC = 1\).
- **Lagging Phase Shift Curve:**
- Begins at 0° and decreases towards -180° as frequency increases.
- Similarly, the transition region is around \(2\pi fRC = 1\).

Annotations and Specific Data Points:
- The graph includes annotations indicating the leading and lagging nature of the phase shifts.
- There is a note that interchanging \(R\) and \(C\) will switch the behavior from leading to lagging phase shift and vice versa.
- The mathematical expressions \(\Delta \theta = 2 \tan^{-1}(1/\omega RC)\) and \(\Delta \theta = -2 \tan^{-1}(\omega RC)\) are provided to describe the phase shift for leading and lagging conditions, respectively.

This graph effectively illustrates the phase behavior of an allpass filter, demonstrating how the phase shift varies with frequency and the impact of component interchange on the phase response.

Figure 6.41. Allpass filter, also known as a delay equalizer, or phase equalizer.

Figure 6.41 shows the basic circuit configuration. Intuitively, it's easy to see that the circuit behaves like an inverter at low frequencies (where no signal is coupled to the noninverting input) and a follower at high frequencies (recall the optional inverter of §4.3.1A). By writing a few equations you can convince yourself that the circuit behaves as described in the figure. Interchanging $R$ and $C$ produces a similar characteristic, but with lagging (rather than leading) phase shifts between the extremes of inverting and following. The phase shift can be tuned by making $R$ variable; but note that a small value of $R$ makes the circuit's input impedance small at high frequencies (where the reactance of $C$ goes to zero).

Figure 6.42 shows a variant that extends the range of phase shift to a full $360^{\circ}$. The downside is that you have to adjust two components simultaneously (e.g., the pair of equal-value resistors) to change its tuning. This can be done nicely, though, by using a digital dual potentiometer (an "EEpot") of the sort described in §3.4.3E.

### 6.3.6 Switched-capacitor filters

One drawback to these state-variable or biquad filters is the need for accurately matched capacitors. If you build the
image_name:Figure 6.42
description:The graph in Figure 6.42 is a phase response plot of an all-pass filter, which is designed to provide a full 360° phase shift. The graph is a Bode plot focusing specifically on the phase shift characteristics of the filter.

1. **Type of Graph and Function:**
- The graph is a Bode phase plot.

2. **Axes Labels and Units:**
- The horizontal axis represents the normalized frequency, denoted as \(2\pi fRC\), on a logarithmic scale. The unit is dimensionless since it is a product of angular frequency and the RC time constant.
- The vertical axis represents the phase shift in degrees, ranging from +180° to -180°.

3. **Overall Behavior and Trends:**
- The phase shift starts at +180° at low frequencies and decreases monotonically to -180° as the frequency increases.
- This behavior indicates a continuous phase shift across the frequency range, characteristic of an all-pass filter.

4. **Key Features and Technical Details:**
- The phase shift is symmetrical around 0°, providing a full 360° phase shift range.
- The plot passes through 0° phase shift at a normalized frequency of approximately 1, where \(\omega RC = 1\).
- The phase shift formula provided is \(\Delta \theta = -2 \arctan \left( \frac{1}{3}(\omega RC - \frac{1}{\omega RC}) \right)\), which describes the phase behavior mathematically.

5. **Annotations and Specific Data Points:**
- There are no specific markers or annotations on the graph itself, but the mathematical expression of the phase shift is provided next to the circuit diagram.
- The circuit diagram above the graph shows the configuration of the all-pass filter using operational amplifiers and passive components, indicating how the phase shift is achieved.

Figure 6.42. Allpass filter with a full $360^{\circ}$ phase shifting range. (Genin, R., Proc. IEEE, 56, 1746 (1968).)
circuit from op-amps, you've got to get pairs of stable capacitors (not electrolytic, tantalum, or high- $\kappa$ ceramic), perhaps matched better than $1 \%$ for optimum performance. You also have to make a lot of connections, since the circuits use at least three op-amps and six resistors for each 2-pole section. Alternatively, you can buy a filter IC, letting the manufacturer figure out how to integrate matched 1000 pF ( $\pm 0.5 \%$ ) capacitors into an IC. Semiconductor manufacturers have solved those problems, but at a price: the UAF42 and MAX274 "Universal Active Filter" ICs (mentioned earlier), implemented with hybrid or laser-trim technology, cost about \$8-\$16 apiece. These "continuoustime" filters also do not lend themselves to easy tunability.

#### A. Switched-capacitor integrator

There's another way to implement the integrators that are needed in the state-variable or biquad filter configurations. The basic idea is to use MOSFET analog switches, clocked from an externally applied square wave at some high frequency (typically 100 times faster than the analog signals of interest), as shown in Figure 6.43. In the figure, the funny triangular object is a digital inverter, which turns the square wave upside down so that the two MOS switches are closed on opposite halves of the square wave.

The circuit is easy to analyze: when $S_{1}$ is closed, $C_{1}$ charges to $V_{\text {in }}$, i.e., holding charge $C_{1} V_{\text {in }}$. On the alternate half of the cycle, $C_{1}$ discharges into the virtual ground, transferring its charge to $C_{2}$. The voltage across $C_{2}$ therefore changes by an amount $\Delta V=\Delta Q / C_{2}=V_{\mathrm{in}} C_{1} / C_{2}$. Note
image_name:A
description:
[
name: S1, type: Switch, ports: {N1: Vin, N2: C1}
name: S2, type: Switch, ports: {N1: C1, N2: C2}
name: C1, type: Capacitor, value: C1, ports: {Np: C1, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: Vout, Nn: OutN(A1)}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: C2, OutP: Vout, OutN: OutN(A1)}
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: InN(A1)}
name: C, type: Capacitor, value: C, ports: {Np: Vout, Nn: InN(A1)}
]
extrainfo:The circuit diagram A represents a switched-capacitor integrator, which uses two switches, S1 and S2, to alternate the charging and discharging of capacitor C1, transferring charge to C2. The operational amplifier A1 integrates the input voltage Vin, producing an output voltage Vout proportional to the integral of Vin. The relationship is given by Vout = f0 * (C1/C2) * ∫Vin dt, where f0 is the frequency of the square wave controlling the switches. The equivalent resistance R is 1/(f0*C1). The circuit diagram B represents a conventional integrator using a resistor R and capacitor C, with Vout = (1/RC) * ∫Vin dt.
image_name:B
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: R, type: Resistor, value: R, ports: {N1: Vin, N2: InN(A1)}
name: C, type: Capacitor, value: C, ports: {Np: InN(A1), Nn: Vout}
name: A1, type: OpAmp, value: A1, ports: {InP: GND, InN: InN(A1), OutP: Vout}
]
extrainfo:The circuit diagram B is a conventional integrator. The input voltage Vin is integrated over time, producing an output voltage Vout proportional to the integral of Vin. The equation governing the output is Vout = (1/RC) ∫Vin dt.

Figure 6.43. A. Switched-capacitor integrator. B. conventional integrator.
that the output-voltage change during each cycle of the fast square wave is proportional to $V_{\text {in }}$ (which we assume changes only a small amount during one cycle of square wave), i.e., the circuit is an integrator! It is easy to show that the integrators obey the equations in the figure.

Exercise 6.6. Derive the equations in Figure 6.43.
Exercise 6.7. Here's another way to understand the switchedcapacitor integrator: calculate the average current that flows through $S_{2}$ into the virtual ground. You should find that it is proportional to $V_{\text {in }}$. Therefore, the combination of $S_{1}, C_{1}$, and $S_{2}$ behaves like a resistor, forming a classic integrator. What is the value of that equivalent resistance, in terms of $f_{0}$ and $C_{1}$ ? Use that to arrive at the equation in the figure, $V_{\text {out }}=f_{0}\left(C_{1} / C_{2}\right) \int V_{\text {in }} d t$.

#### B. Advantages of switched-capacitor filters

There are two important advantages to using switched capacitors instead of conventional integrators. First, as hinted earlier, it can be less expensive to implement on silicon: the integrator gain depends only on the ratio of two capacitors, not on their individual values. In general, it is easy to make a matched pair of anything on silicon, but very hard to make a similar component (resistor or capacitor) of precise value and high stability. As a result, monolithic switched-capacitor filter ICs are inexpensive - TI's universal switched-capacitor filter (the MF10) costs \$3.50
(compared with $\$ 16$ for the conventional UAF42), and furthermore it gives you two filters in one package.

The second advantage of switched-capacitor filters is the ability to tune the filter's characteristic frequency (e.g., the center frequency of a bandpass filter, or the -3 dB point of a lowpass filter) by merely changing the frequency of the square-wave ("clock") input. ${ }^{36}$ This is because the characteristic frequency of a state-variable or biquad filter is proportional to (and depends only on) the integrator gain.

#### C. Switched-capacitor filter configurations

Switched-capacitor filters are available in both dedicated and "universal" configurations. The former are prewired with on-chip components to form lowpass filters of the desired type (Butterworth, Bessel, Elliptic), whereas the latter have various intermediate inputs and outputs brought out so you can connect external components to make anything you want. The price you pay for universality is a larger IC package and the need for external resistors. For example, LTC's self-contained LTC1069-6 8-pole elliptic lowpass filter comes in an 8-pin package (about \$9), compared with their LTC1164 quad 2-pole universal filter which requires 12 external resistors to implement a comparable filter and comes in a 24-pin package (about \$15). Figure 6.44 shows just how easy it is to use the dedicated type. Look ahead to $\S 7.1 .5 \mathrm{~A}$ to see an elegant and simple sinewave generator that uses a tracking switched-capacitor filter acting on a square wave at a fraction of the clock frequency (Figures 7.18 and 7.19).
image_name:Figure 6.44
description:
[
name: LTC1069-6, type: Other, ports: {N1: sig in, N2: sig out, N3: CLK, N4: G, N5: +5V, N6: -5V}
]
extrainfo:The circuit is a switched-capacitor lowpass filter using the LTC1069-6 IC. It requires no external components and has an 8th-order elliptic response with ±0.1 dB passband ripple, more than 40 dB attenuation at 1.3 times the 3 dB frequency. The clock frequency is 250 kHz, and the output is a lowpass filtered signal with a 3 dB cutoff frequency of 5 kHz.

Figure 6.44. Switched capacitor dedicated lowpass filter, requiring no external components. The 8th-order elliptic response has $\pm 0.1 \mathrm{~dB}$ passband ripple, and is more than 40 dB down at $1.3 f_{3 \mathrm{~dB}}$.

Both dedicated and universal switched-capacitor filters use as the basic building block the 2-pole statevariable configuration, with switched-capacitor integrators replacing the resistor-fed op-amp integrators of the classic continuous-time state-variable active filter; see Fig-

[^11]ure 6.45. The universal filter ICs come with one to four such sections, which can be cascaded to form a higherorder filter (with each section implementing a quadratic term in the factored filter equation), or they can be used independently for multiple simultaneous channels (which must, however, share the common clocking input). The manufacturer's datasheets (or software or both) make filter design easy with these universal filter ICs. ${ }^{37}$ And no design is needed at all for the dedicated filter - you just connect it up, and off you go.
image_name:Figure 6.45
description:
[
name: inv, type: Inverter, ports: {In: inv input, Out: node1}
name: Σ, type: OpAmp, ports: {InP: node1, InN: node2, OutP: HP, AP, or N out}
name: S1, type: Switch, ports: {N1: node1, N2: node2}
name: S, type: Switch, ports: {N1: node2, N2: GND}
name: Integrator1, type: OpAmp, ports: {InP: node2, InN: GND, OutP: BP out}
name: Integrator2, type: OpAmp, ports: {InP: BP out, InN: GND, OutP: LP out}
]
extrainfo:This circuit is a universal second-order switched-capacitor building block capable of providing lowpass, highpass, bandpass, allpass, and notch filtering. It uses an inverter, an operational amplifier for summing, and two integrators. The outputs are labeled for highpass, allpass, notch, bandpass, and lowpass filtering.

Figure 6.45. "Universal" second-order switched-capacitor building block. It can provide lowpass, highpass, bandpass, allpass, and notch, as determined by external connections. With its on-chip capacitors, the only external components required are a few resistors.

#### D. Drawbacks of switched-capacitor filters

Now for the bad news: switched-capacitor filters have three annoying characteristics, all related and caused by the presence of the periodic clocking signal. First, there is clock feedthrough, the presence of some output signal (typically about 10 mV to 25 mV ) at the clock frequency, independent of the input signal. Usually this doesn't matter, because it is far removed from the signal band of interest. If clock feedthrough is a problem, a simple $R C$ filter at the output usually gets rid of it.

The second problem is more subtle: if the input signal has any frequency components near the clock frequency, they will be "aliased" down into the passband. To state it precisely, any input signal energy at a frequency that differs from the clock frequency by an amount corresponding to a frequency in the passband will appear (unattenuated!) in the passband. For example, if you use a MAX7400 (dedicated 8-pole elliptic lowpass) as a 1 kHz lowpass filter (i.e., set $f_{\text {clock }}=100 \mathrm{kHz}$ ), any input signal energy in the

[^12]range of $99-101 \mathrm{kHz}$ will appear in the output band of dc1 kHz . No filter at the output can remove it! You must make sure the input signal doesn't have energy near the clock frequency. If this isn't naturally the case, you can usually use a simple $R C$ filter, because the clock frequency is typically quite far removed from the passband. The use of filter ICs with a high clock-to-corner frequency ratio (e.g., 100:1 instead of $25: 1$ or $50: 1$ ) simplifies input anti-alias filter design. You can get some nice filter ICs with 1000:1 clock ration from Mixed Signal Integration, for example their MSHN series. ${ }^{38}$ A high clock ratio also reduces the "staircase" output waveform from these filters.

The third undesirable effect in switched-capacitor filters is a general reduction in signal dynamic range (an increase in the "noise floor") that is due to incomplete cancellation of MOSFET switch charge injection (see §3.4.2E). This manifests itself as a raised noise floor within the bandpass. Typical filter ICs have claimed dynamic ranges of $80-90 \mathrm{~dB}$. In addition to reduced dynamic range (compared with continuous-time filters), switched-capacitor filters tend to have more distortion than you would expect, especially for output signals near the supply rails.

Like any linear circuit, switched-capacitor filters (and their op-amp analogs) suffer from amplifier errors such as input offset voltage and $1 / f$ low-frequency noise. These can be a problem if, for example, you wish to lowpass filter some low-level signal without introducing errors or fluctuations in its average dc value. A nice solution is provided by the clever folks at Linear Technology, who dreamed up the LTC1062 "DC accurate lowpass filter" (or the MAX280, with improved offset voltage). Figure 6.46 shows how you use it. The basic idea is to put the filter outside the dc path, letting the low-frequency signal components couple passively to the output; the filter grabs onto the signal line only at higher frequencies, where it rolls off the response by shunting the signal to ground. The result is zero dc error, and switched-capacitor-type noise only in the vicinity of the rolloff ${ }^{39}$ (Figure 6.47). You can cascade a pair of these filters to make higher-order filters, or a tunable sharp bandpass filter. The datasheet also shows you how to make a tunable notch filter.

Switched-capacitor filter ICs are widely available from manufacturers such as Linear Technology, TI, and Maxim. Typically you can put the cutoff (or band center) anywhere in the range of dc to a few tens of kilohertz, as set by the clock frequency. The characteristic frequency

[^13]image_name:Figure 6.46
description:
[
name: R1, type: Resistor, value: 25.8k, ports: {N1: sig in, N2: FB}
name: C1, type: Capacitor, value: 10nF, ports: {Np: FB, Nn: GND}
name: IC1, type: Other, ports: {N1: FB, N2: OUT, N3: CLK, N4: V+, N5: V-, N6: G}
name: OpAmp1, type: OpAmp, ports: {InP: OUT, InN: GND, OutP: Vout, OutN: GND}
]
extrainfo:The circuit is a lowpass filter using the LTC1062 IC. The cutoff frequency is determined by the clock frequency f_CLK, with f_3dB = f_CLK/100. The IC is powered by a dual supply of +5V and -5V.

Figure 6.46. LTC1062 "dc-accurate" lowpass filter. The external clock input must swing rail-to-rail (add a small series resistor to protect the input); alternatively you can enable the internal oscillator by connecting a capacitor from CLK to ground.
image_name:Figure 6.47
description:The graph in Figure 6.47 is a plot showing the output noise voltage spectrum of the LTC1062 lowpass filter. It is a frequency response graph with a logarithmic scale on the x-axis representing frequency in Hertz (Hz), ranging from 0.1 Hz to 10 kHz. The y-axis represents the output noise voltage in microvolts per square root Hertz (µV/√Hz), with a linear scale ranging from 0 to 50 µV/√Hz.

The graph displays three distinct peaks, each corresponding to a different cutoff frequency (f_C). These peaks illustrate the output noise voltage levels at different cutoff frequencies of the filter:

1. **First Peak:** Occurs at a cutoff frequency of 10 Hz, reaching a maximum noise voltage of approximately 42 µV/√Hz.
2. **Second Peak:** Occurs at a cutoff frequency of 100 Hz, with a maximum noise voltage of about 18 µV/√Hz.
3. **Third Peak:** Occurs at a cutoff frequency of 1 kHz, reaching a maximum noise voltage of around 6 µV/√Hz.

Each peak represents the noise performance of the filter at the given cutoff frequency, showing how the output noise voltage decreases as the cutoff frequency increases. The peaks are sharp, indicating narrow bandwidths around each cutoff frequency. This behavior is typical for switched-capacitor filters, where the noise is concentrated around specific frequencies determined by the clock frequency and its harmonics.

Figure 6.47. LTC1062 output noise spectra (see the datasheet).
is a fixed multiple of the clock, usually $50 f_{\text {clk }}$ or $100 f_{\text {clk }}$. Most switched-capacitor filter ICs are intended for lowpass, bandpass, or notch (band-stop) use, though you can configure the universal type as highpass filters. Note that clock feedthrough and discrete (clock-frequency) output waveform quantization effects are particularly bothersome in the latter case, since they're both in-band.

### 6.3.7 Digital signal processing

Our discussion of electronic filters in this chapter would be seriously incomplete without an introduction to the widespread technique of digital signal processing (DSP), also known as discrete-time signal processing. Contemporary systems that include microprocessors favor digitalfiltering methods for their flexibility and performance. Digital signal processing is the manipulation of signals in the digital domain, in which a signal (for example, a speech waveform) has been converted to a sequence of
numbers representing its sampled amplitude values at equally spaced intervals of time. The "manipulations" can be any of the things we've seen in the purely analog domain - filtering, combining, attenuation or amplification, nonlinear compression and clipping, and so on; but they can include also additional sophisticated operations made possible by the power of computation, such as coding, error correction, encryption, spectral analysis, speech synthesis and analysis, image processing, adaptive filtering, and lossless compression and storage.

We'll have much to say about digitizing and processing in Chapters 13 ("Digital meets analog") and 15 ("Microcontrollers"), when we'll have, respectively, the electronic tools for conversion between analog voltages and their digital representation, and the means to process those digital quantities. Here we would like simply to introduce the application of DSP to filtering and give a glimpse of its capabilities, particularly when compared with the analog filters we've seen. We'll stick to one-dimensional filters; that is, the filtering of "one-dimensional" signals such as speech (as contrasted with two-dimensional images), which are characterized by some voltage waveform $V(t)$ evolving in time.

#### A. Sampling

We mentioned earlier that a digitized representation of a continuous waveform involves sampling at a discrete set of (nearly always) uniformly spaced times, with a discrete set of (usually) uniformly spaced quantized amplitudes. These determine the fidelity of the quantization - in frequency (from the sampling rate, obeying the Nyquist sampling criterion, see Figure 13.60) and in dynamic range and noise (from the quantization precision); see §13.5.1. There's a lot to say about these; but at the most basic level you've got to sample at least twice the rate of the highest-frequency component that's in the input, and you've got to have enough precision in the $n$-bit amplitude quantization to preserve the dynamic range you want. Put compactly,

$$
\begin{aligned}
f_{\text {samp }} & \geq 2 f_{\text {sig }}(\max ), \\
\text { dynamic range } & =6 n \mathrm{~dB} .
\end{aligned}
$$

Assuming you're beginning with an analog waveform, the sampling is done with an analog-to-digital converter (ADC), preceded by an anti-alias lowpass filter (LPF), if needed, to ensure that the waveform being digitized contains no signals of significance above the Nyquist frequency $f_{\text {samp }} / 2$.

#### B. Filtering

The sequence of adequately sampled amplitudes (call it $x_{n}$, for the $n$th sample) represents the input signal. We
want to do a filtering operation on the sequence, for example a lowpass filter. There are two broad classes of DSP filters: finite-impulse-response (FIR) and infinite-impulseresponse (IIR). The FIR is easiest to understand - each output sample is simply a weighted sum of some number of input samples (see Figure 6.48):

$$
y_{i}=\sum_{k=-\infty}^{\infty} a_{k} x_{i-k}
$$

where the $x_{i}$ are the input signal amplitudes, the $a_{k}$ are the weights, and the $y_{i}$ are the output of the filter. In real life there will be only a finite number of weights, and so the sum will run only over a finite set of input values, as in the figure. Speaking crudely, the set of coefficients is an approximation to the inverse Fourier transform of the desired filter function.
image_name:Figure 6.48
description:The system block diagram in Figure 6.48 represents a Finite Impulse Response (FIR) digital filter. This type of filter is nonrecursive and processes digital signals by applying a set of coefficients to the input samples to produce an output.

**Main Components:**
1. **Input Samples (x):** The diagram shows a series of input samples labeled from the past to the future: \( x_{i-3}, x_{i-2}, x_{i-1}, x_{i}, x_{i+1}, x_{i+2}, x_{i+3} \). These represent discrete signal amplitudes at various time intervals.
2. **Coefficients (a):** Each input sample is associated with a weight or coefficient: \( a_{-3}, a_{-2}, a_{-1}, a_{0}, a_{1}, a_{2}, a_{3} \). These coefficients are used to scale the input samples.
3. **Summation Block (+):** The scaled input samples are combined in a summation block to produce the output \( y_{i} \).

**Flow of Information:**
- The input samples \( x_{i-3} \) to \( x_{i+3} \) are multiplied by their respective coefficients \( a_{3} \) to \( a_{-3} \).
- These products are then summed together in the summation block to yield the filtered output \( y_{i} \).
- The data moves from left to right, indicating the progression of time from the future to the past, with the current sample \( x_{i} \) being central.

**Labels, Annotations, and Key Indicators:**
- The diagram is annotated with directional arrows indicating the flow of data and time, labeled as "the future," "now," and "the past."
- The output is labeled as \( y_{i} \) and is identified as the filtered output.

**Overall System Function:**
The primary function of this FIR filter is to process a sequence of input signal samples by applying a set of predefined coefficients, effectively filtering the signal. The use of future samples in the computation allows the filter to achieve desired frequency response characteristics by considering both past and future inputs, a feature unique to digital filters. This process results in an output that is a weighted sum of the input samples, providing the desired filtering effect.

Figure 6.48. Finite impulse response (nonrecursive) digital filter.

Note an interesting - and important - feature of such a filter: its output is formed of samples both past and $f u$ ture. That is, it can generate an output that would appear to violate causality (effect must follow cause), but which is permitted here because the output signal has an overall delay with respect to the input. This ability to see into the future (a boast that no analog filter can make) allows digital filters to implement frequency- and phase-response characteristics that cannot be achieved with the (causal) analog filters we've seen up to this point.

The IIR filter differs in allowing the output to be included, with some weighting factor, along with the inputs in the weighted sum; this is sometimes called a recursive filter. The simplest example might be

$$
y_{i}=b y_{i-1}+(1-b) x_{i}
$$

which happens to be the discrete approximation to a continuous-time $R C$ lowpass filter, in which the weighting factor $b$ is given by $b=e^{-t_{\mathrm{s}} / R C}$, where $t_{\mathrm{s}}$ is the sampling interval. Of course, the situation is not identical to an analog
lowpass filter operating on an analog waveform because of the discrete nature of the sampled waveform.

Both FIR and IIR implementations have their pros and cons. FIR filters are generally preferred because they are simple to understand, easy to implement, unconditionally stable (no feedback), and they can be (and usually are) designed as linear-phase filters (i.e., the time delay is constant, independent of frequency). IIR filters are more economical, however, requiring fewer coefficients and therefore less memory and calculation. They also are easily derived from the corresponding classic analog filter; and they are particularly well suited to applications requiring high selectivity, for example, notch filters. However, they require more bits of arithmetic precision to prevent instabilities and "idle tones," and they are more difficult to code.

#### C. An example: IIR lowpass

As a simple numerical example, suppose you want to filter a set of numbers representing a signal, with a lowpass 3 dB point at $f_{3 \mathrm{~dB}}=1 / 20 t_{\mathrm{s}}$, equivalent to a single-section $R C$ lowpass filter of the same breakpoint. Here the time constant equals the time for 20 successive samples. Then $A=0.95123$, and so the output is given by

$$
y_{i}=0.95123 y_{i-1}+0.04877 x_{i}
$$

The approximation to a real lowpass filter becomes better as the time constant becomes long compared with the time between samples, $t_{\mathrm{s}}$.

You would probably use a filter like this to process data that are already in the form of discrete samples, e.g., an array of data in a computer. In that case the recursive filter becomes a trivial arithmetic pass once through the data.

#### D. An example: FIR lowpass

An ideal lowpass filter has unit response up to its cutoff frequency $f_{\mathrm{c}}$ and zero response for higher frequencies. That is, the response curve is rectangular, a "brick-wall" filter. To first order, the FIR coefficients $a_{k}$ are the rectangle's Fourier transform, namely a $(\sin x) / x$ function (or sinc function), in which the scaling of the argument depends on the ratio of the cutoff frequency to the sampling frequency, namely,

$$
\begin{equation*}
a_{k} \propto \frac{\sin \left(2 \pi k f_{\mathrm{n}}\right)}{2 \pi k f_{\mathrm{n}}} \tag{6.18}
\end{equation*}
$$

where the integers $k$ go from $-\infty$ to $\infty$, and $f_{\mathrm{n}}$ is the normalized cutoff frequency, defined as $f_{\mathrm{n}}=f_{\mathrm{c}} / f_{\mathrm{s}}$.

In a real-world implementation, of course, you get only a finite number of $k$ 's, say $N$ of them. So the question: what set of truncated filter coefficients $a_{k}$, where $k$ goes only from $-N / 2$ to $N / 2$, best approximates the ideal lowpass filter? This turns out to be more complicated than you
might at first imagine. Among other things, it depends on what you mean by "best."

If you simply truncate the $a_{k}$ series, discarding coefficients beyond the length of your FIR sample string, the resulting filter's frequency response will exhibit large bumps in the stopband attenuation; that is, degraded rejection around those frequencies. This is exactly analogous to the problem of "spectral leakage" in digital spectrum analysis, or of diffraction sidelobes in optics, and the fix is the same: here you taper the coefficients $a_{k}$ by multiplying them by a "window function" that goes smoothly toward zero at the ends (in spectrum analysis you multiply the incoming digitized signal amplitudes by an analogous windowing function, and in optics you "apodize" the aperture with a mask whose opacity increases toward the edges). The effect is to reduce greatly the stopband ripple, at the expense of a more gradual transition from passband to stopband (in spectral analysis the effect is greatly reduced spectral leakage into adjacent frequency bins, at the expense of broader bin width; in optics the sidelobes are attenuated, at the expense of decreased resolution in the form of a broader "point-spread function"). Typical window functions have names like Hamming, Hanning, and Blackman-Harris. There's no "best" window - it's always a tradeoff between the steepness of transition to the stopband versus the worst-case attenuation in the stopband. But most of the time it doesn't really matter a whole lot which of the standard windows you use. ${ }^{40}$

A second aspect of "best" is to choose a cutoff frequency $f_{\mathrm{n}}$ for which at least some of the coefficients are exactly zero; that way you can omit the multiply and add operations corresponding to those taps. This occurs, for example, with the choice $f_{\mathrm{n}}=0.25$ (a sampling rate four times the cutoff frequency), for which the coefficients in eq'n 6.18 become

$$
\begin{equation*}
a_{k} \propto \frac{\sin (\pi k / 2)}{\pi k / 2} \tag{6.19}
\end{equation*}
$$

and therefore all the coefficients with even $k$ (except $a_{0}$ ) are zero. You get a small bonus, also, by using a filter length $N$ that is a multiple of 4 ; that makes the end coefficients (at $k= \pm N / 2$ ) vanish, because their index $k$ is then even.

Because a cutoff frequency of half the sampling frequency (i.e., $f_{\mathrm{n}}=0.5$ ) is the maximum allowed by the Nyquist sampling theorem, a filter whose cutoff is at $f_{\mathrm{n}}=0.25$ is known as a "half-band" filter. Figures 6.49 and 6.50 show the response of half-band filters with $N=8,16$, 32 , and 64 , where the coefficients have been calculated

[^14]image_name:Figure 6.49
description:The graph in Figure 6.49 is a plot of the frequency response of half-band FIR digital filters on a linear scale. The x-axis represents the normalized frequency \( f / f_{\text{samp}} \), ranging from 0 to 0.5, where \( f_{\text{samp}} \) is the sampling frequency. The y-axis represents the output-to-input voltage ratio \( V_{\text{out}} / V_{\text{in}} \), ranging from 0 to 1.

This graph shows the behavior of half-band filters with different orders \( N = 8, 16, 32, \) and \( 64 \). Each curve represents a different filter order, with higher orders resulting in sharper transitions from passband to stopband. The curves are labeled with their respective \( N \) values.

The general trend observed is that as the filter order \( N \) increases, the transition band becomes steeper, indicating a more selective filter. The cutoff frequency, where the response begins to drop significantly, is around \( f_{\text{n}} = 0.25 \), typical for half-band filters.

Key features include:
- The filter with \( N = 8 \) has the broadest transition region, indicating less selectivity.
- As \( N \) increases to 16, 32, and 64, the transition region narrows, showing increased filter selectivity.
- All curves start at a normalized frequency of 0 with a gain of 1, indicating full passband transmission.
- The curves approach zero gain as the normalized frequency approaches 0.5, indicating effective stopband attenuation.

No specific annotations or numerical data points are marked on the graph, but the trends and differences between filter orders are clearly visible.

Figure 6.49. Half-band FIR digital filter response, plotted on a linear scale. A filter of order $N$ requires $N / 2+1$ coefficients.
image_name:Figure 6.49
description:### Type of Graph and Function:
The graph is a frequency response plot of half-band FIR digital filters, specifically showing attenuation in decibels (dB) versus normalized frequency (f/fsamp). It is plotted on a linear scale.

Axes Labels and Units:
- **X-axis:** Normalized Frequency \((f/f_{samp})\), ranging from 0.1 to 0.5.
- **Y-axis:** Attenuation in decibels (dB), ranging from 0 to -80 dB.

Overall Behavior and Trends:
The graph illustrates the attenuation characteristics of half-band FIR filters of different orders (N = 8, 16, 32, 64). Each curve starts with minimal attenuation at lower frequencies and shows increased attenuation as the normalized frequency approaches 0.5. The transition from passband to stopband becomes sharper with increasing filter order.

Key Features and Technical Details:
- **Filter Order Impact:** As the filter order increases, the transition band becomes narrower, and the attenuation in the stopband is more pronounced. For instance, the curve for N = 64 shows a very steep transition compared to N = 8.
- **Stopband Performance:** All curves approach zero gain as the normalized frequency nears 0.5, indicating effective stopband attenuation.

Annotations and Specific Data Points:
- The graph includes annotations indicating the filter order for each curve (N = 8, 16, 32, 64), which helps distinguish the performance differences related to filter complexity.
- No specific numerical data points or gridlines are marked, but the trends and transitions are clearly visible.

Figure 6.50. The half-band filters of Figure 6.49, plotted on a loglog scale to reveal the stopband response.
according to eq'n 6.19 , weighted by a Hamming window. The latter is a raised cosine, given approximately by

$$
\begin{equation*}
w(k)=0.54+0.46 \cos (2 \pi k / N) \tag{6.20}
\end{equation*}
$$

A final step is to normalize the coefficients (by multiplying each by the same factor) so that their sum is 1 , giving the filter unit gain at dc. The recipe, then, is to choose an $N$ (preferably a multiple of 4 ); then, for each positive odd $k$ up to $N / 2$, calculate the sinc function of equation (6.19) and multiply it by the Hamming coefficient of eq'n 6.20 to get the (not yet normalized) $a_{k}$. Note that the coefficients are symmetric $\left(a_{-k}=a_{k}\right)$, and that the $a_{0}$ term will be 1.0 (because both $\operatorname{sinc}(0)$ and $w(0)$ have value unity). The final step is to normalize these coefficients by dividing each by their sum.

Because the even coefficients are zero, the resultant filters, though requiring $N$ stages of memory, need approximately half that number of coefficients (those with odd subscripts, plus $a_{0}$ ), namely $5,9,17$, and 33 , respectively. You can check our recipe by calculating the coefficients for
the lowest-order filter in the figures ( $N=8$ ); you should get

$$
\begin{aligned}
a_{0} & =+0.497374 \\
a_{1}=a_{-1} & =+0.273977 \\
a_{2}=a_{-2} & =0 \\
a_{3}=a_{-3} & =-0.022664 \\
a_{4}=a_{-4} & =0
\end{aligned}
$$

#### An aside: window tradeoffs

We used a Hamming window as the coefficient multiplier for the filters of Figures 6.49 and 6.50, partly out of laziness (it's easy to calculate), and partly because it's a reasonably good window in terms of stopband attenuation ( $\sim 60 \mathrm{~dB}$ ). But, as we remarked above, you can produce better stopband attenuation at the expense of transition-region steepness. This is nicely illustrated in Figure 6.51, where we've redone the $N=32$ half-band lowpass FIR filter using three different window functions. The Blackman-Harris windows are a sum of two or three sinusoidal terms, weighted to produce the minimum sidelobe level. The exact form is

$$
w(k)=a_{0}+a_{1} \cos (2 \pi k / N)+a_{2} \cos (4 \pi k / N)+a_{3} \cos (6 \pi k / N)
$$

where the $a$ 's are given by $\left[a_{0}, a_{1}, a_{2}, a_{3}\right]=[0.42323$, $0.49755,0.07922,0]$ (3-term) and [0.35875, 0.48829, $0.14128,0.01168]$ (4-term). These windows produce impressive stopband attenuation ( $\sim 85 \mathrm{~dB}$ and $\sim 105 \mathrm{~dB}$ ), as compared with the Hamming's $\sim 55 \mathrm{~dB}$, but with correspondingly softer transition regions. It's worth noting that these are calculated responses, and will be realized in practice only if the FIR multiply and add operations are done with adequate arithmetic precision, and if the upstream ADC has correspondingly accurate linearity.
image_name:Figure 6.51
description:The graph depicted in Figure 6.51 is a frequency response plot of half-band FIR lowpass filters of order \( N=32 \), showcasing the performance of three different window functions: Hamming, Blackman-Harris 3-term, and Blackman-Harris 4-term. The x-axis represents the normalized frequency \( (f/f_{\text{samp}}) \), ranging from 0.1 to 0.5. The y-axis indicates attenuation in decibels (dB), with a scale from 0 dB to -120 dB.

Graph Type and Function
This is a frequency response graph, specifically a magnitude plot showing the attenuation characteristics of different window functions used in FIR filters.

Axes Labels and Units
- **X-axis:** Normalized Frequency \((f/f_{\text{samp}})\), linear scale, ranging from 0.1 to 0.5.
- **Y-axis:** Attenuation in decibels (dB), linear scale, from 0 dB to -120 dB.

Overall Behavior and Trends
The graph illustrates the attenuation performance of the three window functions. All curves start with minimal attenuation at lower frequencies and increase sharply as the frequency approaches the cutoff region around 0.3 \( f/f_{\text{samp}} \). Beyond this point, the attenuation increases significantly, showing the transition to the stopband.

Key Features and Technical Details
- **Hamming Window:** Exhibits a steep transition with moderate stopband attenuation, reaching around -55 dB.
- **Blackman-Harris 3-term and 4-term Windows:** These windows show softer transitions compared to the Hamming window but achieve much higher stopband attenuation, approximately -85 dB for the 3-term and -105 dB for the 4-term.
- The Blackman-Harris curves exhibit ripples in the stopband, especially noticeable beyond 0.35 \( f/f_{\text{samp}} \).

Annotations and Specific Data Points
- The graph includes annotations identifying the different window functions.
- Notable points include the transition region around 0.3 \( f/f_{\text{samp}} \) and the varying levels of stopband attenuation achieved by each window function. The Blackman-Harris windows provide superior attenuation performance compared to the Hamming window, as indicated by the deeper dips in their respective curves.

Figure 6.51. Half-band FIR lowpass filters of order $N=32$, with three choices of coefficient window function. Note the change of vertical scale compared with those of Figures 6.49 and 6.50.

#### E. Implementation

You could set up a DSP filter with discrete hardware - shift registers, multipliers, accumulators, and the like - the stuff of Chapters 10 and 11. But any such attempt would seem quaint by current standards, where general-purpose processors (microprocessors and microcontrollers) let you do the same tasks, and with greater flexibility. Even better, there is a class of digital signal processor chips, optimized for the sort of multiply-accumulate operations you need to do, and generally arranged for efficient flow of lots of data in and out. An example is the TMS320 series from TI, which includes (at time of writing) chips like the TMS320C64xx, which can do a 1k-point fast Fourier transform (FFT) in about $1 \mu \mathrm{~s}$ (!), or a 32 -coefficient FIR on a 10,000 -point data set in $108 \mu \mathrm{~s}$. At the other end of the performance scale, the tiny QF1D512 from Quickfilter Technology is an inexpensive stand-alone chip that performs up to a 512-tap FIR filter on 12- to 24-bit serial data (at audio rates), with 32-bit programmable coefficients. It costs less than $\$ 2$ in small quantities and comes with free design software; you can also get a variety of evaluation kits.

### 6.3.8 Filter miscellany

#### A. Linearity

In some filtering applications it is essential to maintain a high degree of amplitude linearity, even as the filter attenuates some frequencies more than others. This is necessary, for example, in high-quality audio reproduction. For such applications you should use op-amps designed for low distortion (which will be prominently featured on the datasheet), with adequate bandwidth, slew rate, and loop gain; some examples are the LT1115, OPA627, and AD8599; see Table 5.4 on page 310 and the discussion of high-speed op-amps and design issues in $\S 5.8$, and further discussion in Chapter $4 x$. Perhaps less obvious, it's important to choose passive components of good linearity. The primary hazards lying in wait here are the "high- $\kappa$ " ceramic capacitors (which can exhibit astonishing variations of capacitance with applied voltage), and electrolytic capacitors (with their memory effect caused by dielectric absorption - see the discussion in Chapter $l x$. Use film capacitors (ideally polypropylene) or NPO/C0G ceramic.

And for $L C$ (passive) filters it's essential to choose inductors wound on magnetic material of good linearity (a problem that is absent for air-core inductors; the latter are available in reasonable sizes for inductances up to $\sim 1 \mathrm{mH}$ or so).

#### B. Filter-design software

It used to be hard to design filters - but no more! There's plenty of software out there, and it's easy to use. You can set up your passband and stopband requirements for a continuous-time filter (cutoff frequency, stopband frequency, ripple and attenuation, etc.), and the software obliges with a recitation of how many sections will be required, according to the circuit configuration (Sallen-and-Key, state variable, biquad, or MFB) and filter function (Bessel, Butterworth, Chebyshev, elliptic). Then it will draw the circuit, and give you plots of amplitude, phase, and time delay as functions of frequency. And similarly for switched-capacitor filters or digital filters.

Here are some filter design resources we've found useful. Most of these are free (but you have to pay for MMICAD, and for Filter Solutions and Filter Light).

- LC filters:
- http://www-users.cs.york.ac.uk/ fisher/lcfilter/
- MMICAD (Optotek)
- Analog active filters
- FilterPro (TI)
- FilterCAD (LTC)
- ADI Analog Filter Wizard
- http://www.beis.de/Elektronik/Filter/Filter.html
- Digital filters:
- http://www-users.cs.york.ac.uk/ fisher/mkfilter/
- All types
- Filter Solutions, Filter Light, and Filter Free (http://www.nuhertz.com/filter/)

## Review of Chapter 6

An A-to-J summary of what we have learned in Chapter 6. This summary reviews basic principles and facts in Chapter 6, but it does not cover application circuit diagrams and practical engineering advice presented there.

### ๆA. Filter Overview.

This chapter deals with signals in the frequency domain: by filter we mean a circuit with some deliberate passband and attenuation characteristics (both amplitude and phase) versus frequency. For some applications the filter's timedomain behavior is important also, i.e., the filter's transient response (overshoot and settling time) to a voltage-step input, and its in-band fidelity to an input waveform.

### IB. Filter Characteristics.

There are the basic shapes - lowpass, highpass, bandpass, and band-stop (notch). There's also the all-pass (or delay equalizer), which has a flat amplitude response, but a varying phase; and there are comb filters that pass (or block) an array of equally spaced frequencies. Important frequencydomain parameters include flatness of response in the passband, depth of attenuation in the stopband, and steepness of falling response in the transition region between. In the time-domain you care about overshoot, settling time, and linearity of phase across the passband (i.e., constancy of time delay).

### qC. Filter Implementations.

Filters can be built (a) entirely with passive components ( $R$, $L$, and $C$ ); (b) with $R$ 's and $C$ 's, assisted with op-amps; (c) with $C$ 's alone, combined with periodically-clocked analog switches; or (d) with digital processing of the ADCsampled input waveform. These are called passive filters, active filters, switched-capacitor filters, and digital filters, respectively. The term continuous-time filter is sometimes applied to filters of type (a) and (b), and discrete-time filter to (c) and (d). The order of a filter is equal to the number of $C$ 's plus the number of $L$ 's (or equivalent, if implemented digitally). An $n$th order lowpass filter has an ultimate rolloff of $6 n \mathrm{~dB} /$ octave ( $20 n \mathrm{~dB} /$ decade $)$.

### ID. Passive RC Filters.

Passive $R C$ filters ( $\S 6.2 .1$ ) are the simplest, and good enough for applications such as blocking dc, suppressing high-frequency power-supply noise, or removing signals far from the band of interest. But $R C$ filters, regardless of order, have a soft transition region (Figure 6.2) and are unsuited to separating signals that are nearby in frequency.

Their transfer function is far from the ideal "brick-wall" filter response (see for example Figure 6.11).

### ПE. Passive LC Filters.

Perhaps surprisingly, combining inductors with capacitors allows you to make all manner of very sharp filters ( $\S 6.2 .2$; see for example Figure 6.5). The classic filter shapes, all implementable with $L C$ filters, are the Butterworth (maximally flat passband), the Chebyshev (sharpest transition region, at the cost of amplitude ripple in the passband), and the Bessel (maximally flat time-delay in the passband). The performance characteristics of these filter types are compared in Table 6.1 and Figures 6.20, 6.21, 6.25-6.27, and 6.30 .

### IF. Active Filters.

Inductors are non-ideal in several respects (size, linearity, electrical losses; see Chapter $1 x$; but the combination of a capacitor and an op-amp (plus several resistors), in a configuration known as a gyrator ( 86.2 .4 C ), creates an electrical equivalent of an inductor. So you can make an inductorless filter that mimics any $L C$ filter, by simply substituting gyrators for the inductors. More generally, you can make such active filters (\$6.3) with various configurations of opamps, capacitors, and resistors that need not incorporate explicit gyrators.

### IIG. Active Filter Circuits.

In §6.3.1 we showed how to design the simple and popular VCVS active filter, with tabulated data (Table 6.2) for 2nd-order to 8th-order lowpass or highpass filters, with Butterworth, Chebyshev, or Bessel response. Better performance and tunability is gotten with the state-variable and biquad active filters (\$6.3.3), which require three op-amps for each 2nd-order section. These latter filter topologies are well suited for bandpass filters; see §6.3.3A, where explicit design equations are given. You can get nice state-variable ICs that include the op-amps and capacitors, and can be configured as lowpass, highpass, band-pass, or band-reject, requiring only a few external resistors to set the characteristic cutoff frequencies; examples are the UAF42 and the MAX274. The world is awash with active-filter implementations; some others seen in Chapter 6 include the Sallen-and-Key filter (Figure 6.16), a state-variable variant with independently settable gain and $Q$-factor (Figure 6.32), and the multiple-feedback filter (Figure 6.35).

### IH. Notch Filters.

In contrast to their generally "soft" frequency characteristics, the $R C$ filter known as a twin-T (\$6.3.4) produces a
deep notch (limited only by component imperfection and mismatching). The twin-T is hard to tune (it requires three tracking adjustable resistors). But a similar $R C$ notch filter (the bridged-differentiator, Figure 6.40) allows a modest range of tunability ( $5: 1$ or so) with a single pot.

### |ll. Switched-capacitor Filters.

An op-amp combined with a pair of capacitors and a pair of analog switches forms a discrete approximation to a continuous-time integrator (Figure 6.43). This is the building block of the switched-capacitor filter (§6.3.6), easily incorporated into an IC, and conveniently tuned by varying the externally-applied switching frequency. The downside is the production of artifacts related to the switching operation: clock feedthrough, aliasing, and limited dynamic range.

### ПJ. Digital Filters and DSP.

With ubiquitous embedded microcontrollers and accompanying ADCs, it's natural to implement filtering operations with the machinery of digital signal processing (DSP, §6.3.7). If the signals to be filtered are in the form of ana-
log voltages, they first must be digitized (sampled at regular intervals and converted to a stream of numbers), taking care to sample at a high enough rate (at least twice the highest frequency present in the signal, $\left.f_{\mathrm{samp}} \geq 2 f_{\operatorname{sig}(\max )}\right)$ and with sufficient amplitude accuracy ( $n$-bit quantization yields $6 n \mathrm{~dB}$ dynamic range) to retain adequate fidelity. (If the input signal is already digitized, no sampling is needed, and digital filtering is particularly convenient.)

The stream of numbers representing the successive sampled and digitized signal voltages (call them $x_{i}$ ) is then subjected to a digital filtering operation. Easiest to understand is the finite-impulse-response (FIR) filter, where each output signal amplitude $y_{i}$ is formed from a weighted sum of a finite number $N$ of input samples; i.e., $y_{i}=\sum a_{k} x_{i-k}$, with $k$ going from $-N / 2$ to $N / 2$. If the sum is permitted to include output samples, you've got a recursive filter, also known as an infinite-impulse-response filter. See Figure 6.49 for an example of an FIR lowpass filter. There's plenty of complexity, and plenty of math, in the business of digital filtering; this specialty appeals to EEs who are really applied mathematicians in disguise (you know who you are!).
