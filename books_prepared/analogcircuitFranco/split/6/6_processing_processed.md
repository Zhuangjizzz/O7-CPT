# 5.4 VOLTAGE COMPARATORS

After the op amp, the voltage comparator is probably the most popular high-gain amplifier. Its function is to compare two analog inputs $v_{P}$ and $v_{N}$ and yield a binaryvalued output such as

$$
\begin{array}{ll}
v_{O}=V_{O L} & \text { for } v_{P}<v_{N} \\
v_{O}=V_{O H} & \text { for } v_{P}>v_{N} \tag{5.43b}
\end{array}
$$

where $V_{O L}$ and $V_{O H}$ are prescribed logic levels such as the familiar TTL/CMOScompatible voltages $V_{O L}=0 \mathrm{~V}$ and $V_{O H}=5 \mathrm{~V}$. Aptly called a decision circuit, the comparator can also be viewed as a 1-bit analog-to-digital converter. Figure 5.20a shows the comparator's circuit symbol, whereas Fig. 5.20b shows the voltage transfer curve (VTC) implied by Eq. (5.43). As we know, the slope of a VTC represents gain, so the VTC of Fig. $5.20 b$ implies an amplifier having infinite gain and saturating at $V_{O L}$ and $V_{O H}$.

Infinite gain is physically impossible, so the VTC of a real-life comparator is more likely as in Fig. 5.20c, where we estimate voltage gain as

$$
\begin{equation*}
a \cong \frac{V_{O H}-V_{O L}}{V_{I H}-V_{I L}} \tag{5.44}
\end{equation*}
$$

with $V_{I L}$ and $V_{I H}$ representing the values of $v_{I}$ at which $a=1 \mathrm{~V} / \mathrm{V}$. Accordingly, Eq. (5.43) changes to

$$
\begin{array}{ll}
v_{O}=V_{O L} & \text { for } v_{P}<\left(v_{N}+V_{I L}\right) \\
v_{O}=V_{O H} & \text { for } v_{P}>\left(v_{N}+V_{I H}\right) \tag{5.45b}
\end{array}
$$

Moreover, we have

$$
\begin{equation*}
v_{O}=a\left(v_{P}-v_{N}\right) \quad \text { for }\left(v_{N}+V_{I L}\right)<v_{P}<\left(v_{N}+V_{I H}\right) \tag{5.45c}
\end{equation*}
$$

image_name:(a)
description:
[
name: OpAmp, type: OpAmp, ports: {InP: vP, InN: vN, OutP: vO}
]
extrainfo:The circuit diagram (a) represents a voltage comparator using an OpAmp. The voltage transfer characteristics (VTC) are shown in diagrams (b) and (c), illustrating the ideal and real-life behavior of the comparator, respectively. The real-life VTC shows a transition region between VIL and VIH, indicating the gain and non-idealities of the comparator.
image_name:(b)
description:The graph labeled (b) is an idealized Voltage Transfer Characteristic (VTC) for a voltage comparator. This is a piecewise linear graph that represents the output voltage \( v_O \) as a function of the difference between the positive and negative input voltages \( v_P - v_N \).

1. **Type of Graph and Function:**
- The graph is a Voltage Transfer Characteristic (VTC) plot.

2. **Axes Labels and Units:**
- The horizontal axis represents the difference in input voltages \( v_P - v_N \). No specific units are provided, but it typically would be in volts (V).
- The vertical axis represents the output voltage \( v_O \), also typically in volts (V).

3. **Overall Behavior and Trends:**
- The graph shows a step-like behavior. When \( v_P - v_N < 0 \), the output voltage \( v_O \) is at a low value \( V_{OL} \).
- When \( v_P - v_N > 0 \), the output voltage \( v_O \) jumps to a high value \( V_{OH} \).
- The transition between these two states is instantaneous in the idealized graph, showing no slope or gradual change.

4. **Key Features and Technical Details:**
- The graph has two distinct horizontal lines indicating the output levels: \( V_{OL} \) (low output voltage) and \( V_{OH} \) (high output voltage).
- The transition point is exactly at \( v_P - v_N = 0 \), where the output switches from \( V_{OL} \) to \( V_{OH} \).

5. **Annotations and Specific Data Points:**
- The graph clearly marks the levels \( V_{OL} \) and \( V_{OH} \) on the vertical axis, but no specific numerical values are given.
- There are no additional annotations or reference lines on this idealized graph.
image_name:(c)
description:The graph labeled (c) is a Voltage Transfer Characteristic (VTC) curve for a real-life voltage comparator. This graph is plotted with the horizontal axis representing the voltage difference \( v_P - v_N \), and the vertical axis representing the output voltage \( v_O \). Both axes are likely in volts, though specific units are not explicitly labeled.

1. **Type of Graph and Function:**
- This is a VTC graph, which represents the output voltage behavior of a voltage comparator as a function of the input voltage difference.

2. **Axes Labels and Units:**
- **Horizontal Axis:** \( v_P - v_N \), likely in volts.
- **Vertical Axis:** \( v_O \), likely in volts.

3. **Overall Behavior and Trends:**
- The graph shows a transition region between two constant voltage levels.
- For \( v_P - v_N < V_{IL} \), the output voltage \( v_O \) is at a low level \( V_{OL} \).
- For \( v_P - v_N > V_{IH} \), the output voltage \( v_O \) is at a high level \( V_{OH} \).
- Between \( V_{IL} \) and \( V_{IH} \), the output voltage increases linearly, indicating a region of linear gain.

4. **Key Features and Technical Details:**
- **Low Output Voltage Level (\( V_{OL} \))**: The output voltage is constant at this level for \( v_P - v_N < V_{IL} \).
- **High Output Voltage Level (\( V_{OH} \))**: The output voltage is constant at this level for \( v_P - v_N > V_{IH} \).
- **Linear Region**: Between \( V_{IL} \) and \( V_{IH} \), the output voltage \( v_O \) increases linearly, representing the comparator's gain.

5. **Annotations and Specific Data Points:**
- The graph annotates the points \( V_{IL} \) and \( V_{IH} \), marking the beginning and end of the linear gain region.
- These points illustrate the threshold voltages where the output transitions between \( V_{OL} \) and \( V_{OH} \).

FIGURE 5.20 (a) Circuit symbol for the voltage comparator. (b) Idealized VTC, and (c) real-life VTC.

It is apparent that the real-life VTC of Fig. 5.20c is only an approximation to the ideal VTC of Fig. 5.20b. However, the closer $V_{I L}$ and $V_{I H}$ are to each other, the higher the gain and the closer the VTC to ideal.

As a high-gain amplifier, the voltage comparator bears strong similarities to the op amp (in fact, we use the same circuit symbol for both). However, they differ in two important respects:

- Op amps are intended to operate with negative feedback, whereas comparators are not. In Chapter 7 we shall see that in order to stave off possible oscillation, an op amp is equipped with a frequency-compensation network which, in its simplest form, consists of a mere capacitance, such as $C_{c}$ in Figs. 5.1, 5.13 and 5.16. In Chapter 6 we shall see that $C_{c}$ slows down the dynamics of the op amp considerably. Comparators, on the other hand, do not need to be frequency compensated because voltage comparison does not involve negative feedback (in fact, a compensation capacitance would only slow down the comparator unnecessarily). Freed of compensation requirements, comparators operate at full speed (voltage-comparator dynamics are investigated in Chapter 6).
- The output saturation voltages of op amps are not digitally compatible (for instance, a 741 op amp powered from $\pm 15-\mathrm{V}$ supplies saturates at about $\pm 13 \mathrm{~V}$, a far cry from TTL/CMOS logic levels). Conversely, voltage-comparator output stages are designed with this type of compatibility in mind.

If speed and logic compatibility are not of concern, then an op amp can indeed be used as a voltage comparator. However, most comparator applications require specialized circuits that have been optimized for this specific operation. To get a feel, let us examine some typical bipolar and CMOS voltage-comparator realizations.

### The LM339 Voltage Comparator

This popular bipolar comparator, available in a quad package from most analog IC manufacturers, is depicted in simplified form in Fig. 5.21. We identify the following blocks:

- The 1 st or input stage consists of the EC pair $Q_{2}{ }^{-} Q_{3}$ and the active load $Q_{5}{ }^{-}$ $Q_{6} . Q_{2}$ and $Q_{3}$ are buffered by the voltage followers $Q_{1}$ and $Q_{4}$ to achieve very low input bias currents ( 25 nA according to the data sheets). Also, thanks to the additional $V_{E B}$ drop introduced by each buffer, the IVR extends all the way down to ground potential. (In fact, $v_{P}$ and $v_{N}$ can be driven few tenths of a volt below ground without causing malfunction.) The function of the diodes is to provide protection against excessive reverse bias as well as more rapid turn off for $Q_{2}$ and $Q_{3}$. Using half-circuit analysis we readily find the (loaded) gain of this stage as

$$
\begin{equation*}
a_{1}=\frac{v_{b 7}}{v_{p}-v_{n}}=\frac{r_{\pi 2}}{r_{e 1}+r_{\pi 2}} g_{m 3}\left(r_{o 3} / / r_{o 6} / / r_{\pi 7}\right) \cong g_{m 3} r_{\pi 7} \tag{5.46}
\end{equation*}
$$

image_name:FIGURE 5.21 Simplified circuit schematic of the LM339 voltage comparator.
description:The circuit is a simplified schematic of the LM339 voltage comparator. It includes multiple stages with transistors and diodes for amplification and protection, and current sources for biasing.

FIGURE 5.21 Simplified circuit schematic of the LM339 voltage comparator.

- The 2nd or intermediate stage consists of the CE amplifier $Q_{7}$. Its function is to provide additional voltage gain, which we estimate as

$$
\begin{equation*}
a_{2}=-\frac{v_{b 8}}{v_{b 7}} \cong-g_{m 7} r_{\pi 8} \tag{5.47}
\end{equation*}
$$

- The 3rd or output stage consists of the so-called open collector CE transistor $Q_{8}$. The reason for leaving the collector uncommitted is so that the user can configure it externally for the desired logic levels at the output. The simplest form is to use a pull-up resistor $R_{P U}$, in which case the circuit yields $V_{O L}=V_{C E 8(\text { sat) }} \cong 0.2 \mathrm{~V}$ when $Q_{8}$ is driven in saturation, and $V_{O H}=V_{C C}$ when $Q_{8}$ is driven in cutoff. With $V_{C C}=5 \mathrm{~V}$ the circuit yields TTL/CMOS logic levels of about 0 V and 5 V . The gain of this stage is estimated as

$$
\begin{equation*}
a_{3}=-\frac{v_{o}}{v_{b 8}} \cong-g_{m 8} R_{P U} \tag{5.48}
\end{equation*}
$$

- The dc biasing circuit, shown in Fig. 5.22, consists of the multiple-output current mirror $Q_{9}$ through $Q_{12}$, along with the stabilized current reference $I_{R E F}$, which in turn is shared among all four comparators on the chip. The current $I_{R E F}$ is replicated by $Q_{10}$ to bias the $Q_{2}-Q_{3}$ pair, and by $Q_{11}$ to actively load $Q_{7}$. Moreover, $Q_{12}$ forms a Widlar current source synthesizing a $7-\mu \mathrm{A}$ current that subsequently divides between the two collectors to provide the $3.5-\mu \mathrm{A}$ bias currents for the $Q_{1}$ and $Q_{4}$ buffers.
image_name:FIGURE 5.22
description:
[
name: Q9, type: PNP, ports: {C: X1, B: X1, E: VCC}
name: Q10, type: PNP, ports: {C: LOAD1, B: X1, E: X1}
name: Q11, type: PNP, ports: {C: LOAD2, B: X1, E: VCC}
name: Q12, type: PNP, ports: {C: LOAD3, B: X1, E: X2}
name: IREF, type: CurrentSource, value: 100 μA, ports: {Np: X1, Nn: GND}
name: R, type: Resistor, value: 9.9 kΩ, ports: {N1: VCC, N2: X2}
]
extrainfo:The circuit diagram represents the DC biasing circuitry of the 339 voltage comparator. It includes a stabilized current reference IREF of 100 μA. Transistor Q12 forms a Widlar current source that provides 3.5 μA bias currents for the Q1 and Q4 buffers.

FIGURE 5.22 The dc biasing circuitry of the 339 voltage comparator.

EXAMPLE 5.5 (a) Assuming $\beta_{p}=150, \beta_{n}=200, V_{C C}=5 \mathrm{~V}$, and $R_{P U}=2.4 \mathrm{k} \Omega$, estimate the 339 comparator's gain for $v_{O}$ half way between $V_{O H}$ and $V_{O L}$.
(b) Estimate the input bias current as well as the difference $V_{I H}-V_{I L}$.
(c) Check with PSpice and comment on your findings.

#### Solution

(a) For $v_{O}=1 / 2\left(V_{O H}+V_{O L}\right)=1 / 2(5+0.2)=2.6 \mathrm{~V}$ we have $I_{C 8}=(5-2.6) / 2.4=$ 1 mA . Using Eqs. (5.46) through (5.48),

$$
\begin{aligned}
& a_{1} \cong \frac{0.05}{26} \beta_{7} \frac{26}{0.1}=\frac{\beta_{7}}{2}=100 \mathrm{~V} / \mathrm{V} \\
& a_{2} \cong-\frac{0.1}{26} \beta_{8} \frac{26}{1}=-\frac{\beta_{8}}{10}=-20 \mathrm{~V} / \mathrm{V} \\
& a_{3} \cong-\frac{R_{P U}}{26 \Omega}=-92.3 \mathrm{~V} / \mathrm{V}
\end{aligned}
$$

The overall gain is $a=a_{1} \times a_{2} \times a_{3}=100 \times 20 \times 92.3 \cong 185 \mathrm{~V} / \mathrm{mV}$.
(b) $I_{B}=I_{B 1}=I_{E 1} /\left(\beta_{1}+1\right)=\left(3.5 \mu \mathrm{~A}+I_{B 2}\right) /\left(\beta_{1}+1\right)=[3.5 \mu \mathrm{~A}+(50 \mu \mathrm{~A}) /$ $\left.\left(\beta_{2}+1\right)\right] /\left(\beta_{1}+1\right)=25.4 \mathrm{nA}$. By Eq. (5.44), $V_{I H}-V_{I L}=\left(V_{O H}-V_{O L}\right) / a=$ $(5-0.2) /\left(185 \times 10^{3}\right) \cong 26 \mu \mathrm{~V}$.
(c) The circuit of Fig. 5.23a utilizes a 339 macro-model to display the VTC (see Appendix 5A).
From Fig. $5.23 b$ we find $V_{I L} \cong 23 \mu \mathrm{~V}, V_{I H} \cong 52 \mu \mathrm{~V}, V_{O L} \cong 0.25 \mathrm{~V}$, and $V_{O H}=5 \mathrm{~V}$. By Eq. (5.44), the gain is $a \cong(5-0.25) /\left[(52-23) 10^{-6}\right] \cong 183 \mathrm{~V} / \mathrm{mV}$. We also observe that the simulated VTC is shifted toward the right by about $37 \mu \mathrm{~V}$. This represents the input offset voltage $V_{O S}$ of the 339 macro-model for the given value of $R_{P U}$. Due primarily to mismatches between the two halves of its input stage, an actual 339 is likely to exhibit a much higher $V_{\text {os }}$. You can easily search the Web for the LM339 data sheets, which list the following typical values at room temperature: $a=200 \mathrm{~V} / \mathrm{mV}, V_{O S}=2 \mathrm{mV}, I_{B}=25 \mathrm{nA}$, and $I_{O S}=5 \mathrm{nA}$. The above calculations indicate that $I_{B}$ strongly depends on $\beta_{p}, a_{1}$ on $\beta_{n}$, and $a_{2}$ on $R_{P U}$.
image_name:(a)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: RPU, type: Resistor, value: 2.4kΩ, ports: {N1: VCC, N2: Vo}
name: LM339, type: OpAmp, value: LM339, ports: {InP: Vi, InN: GND, OutP: Vo}
]
extrainfo:The circuit is a voltage comparator using an LM339 op-amp with a pull-up resistor RPU to VCC, comparing the input voltage Vi to ground.

(a)
image_name:(b)
description:The graph is a Voltage Transfer Characteristic (VTC) curve for a voltage comparator using an LM339 op-amp. It shows the relationship between the input voltage difference \( v_P - v_N \) and the output voltage \( v_O \).

1. **Type of Graph and Function:**
- This is a VTC graph, illustrating the output response of a voltage comparator.

2. **Axes Labels and Units:**
- The x-axis represents the input voltage difference \( v_P - v_N \) in microvolts (µV), ranging from -60 µV to 60 µV.
- The y-axis represents the output voltage \( v_O \) in volts (V), ranging from 0 V to 5 V.
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The graph shows a sharp transition in the output voltage as the input voltage difference crosses a certain threshold.
- For input voltage differences less than approximately 20 µV, the output voltage remains low, close to 0 V.
- As the input voltage difference increases beyond approximately 20 µV, the output voltage rapidly rises to 5 V, indicating a switch from low to high output.

4. **Key Features and Technical Details:**
- The transition region is very steep, characteristic of a comparator's switching behavior.
- The threshold point, where the output begins to switch from low to high, is around 20 µV.
- The output voltage reaches its maximum value of 5 V, indicating a rail-to-rail output swing.

5. **Annotations and Specific Data Points:**
- Significant markers or reference lines are not explicitly shown, but the steep transition is a critical feature of this graph.
- The graph effectively illustrates the comparator's function of switching output states based on input voltage levels.

FIGURE 5.23 (a) PSpice circuit to display (b) the VTC of the 339 voltage comparator.

### A CMOS Voltage Comparator

The circuit of Fig. 5.24 is the complementary version of the CMOS amplifier of Fig. 5.13, but without the compensation network $R_{c}-C_{c}$, which is unnecessary in voltage comparison. The circuit is also equipped with an output inverter to boost the gain as well as to provide a rail-to-rail output swing, or $V_{O L}=V_{S S}$ and $V_{O H}=V_{D D}$. If necessary, the channel widths $W_{9}$ and $W_{10}$ can be made suitably large to boost the output current-drive capabilities.
image_name:FIGURE 5.24 CMOS voltage comparator
description:
[
name: M1, type: NMOS, ports: {S: P1, D: X1, G: vP}
name: M2, type: NMOS, ports: {S: P1, D: X2, G: vN}
name: M3, type: PMOS, ports: {S: VDD, D: X1, G: X1}
name: M4, type: PMOS, ports: {S: VDD, D: X2, G: X1}
name: M5, type: PMOS, ports: {S: VDD, D: X3, G: X2}
name: M6, type: NMOS, ports: {S: VSS, D: X3, G: X4}
name: M7, type: NMOS, ports: {S: VSS, D: X4, G: X4}
name: M8, type: NMOS, ports: {S: X4, D: X4, G: IREF}
name: M9, type: PMOS, ports: {S: VDD, D: VO, G: X3}
name: M10, type: NMOS, ports: {S: VSS, D: VO, G: X3}
name: IREF, type: CurrentSource, ports: {Np: VDD, Nn: X4}
]
extrainfo:This is a CMOS voltage comparator circuit with an output inverter for boosting gain and providing rail-to-rail output swing. It uses a complementary configuration with PMOS and NMOS transistors. The circuit is designed for high gain and speed, but lacks a compensation network as it is unnecessary for voltage comparison.

FIGURE 5.24 CMOS voltage comparator.

### Comparators with Hysteresis

High gain and high speed, generally desirable in voltage comparators, may be counterproductive in the case of noisy inputs. To illustrate, consider the circuit of Fig. $5.25 a$, which uses a comparator to count the zero crossings of a slow varying signal $v_{I}$ afflicted by noise. This noise will cause the comparator to make multiple transitions when $v_{I}$ is in the vicinity of 0 V , thus leading to false counts. (You may find the amount of noise exaggerated, but keep in mind that with very high gain it may take only a few tens of micro-volts of noise to span the range from $V_{I L}$ to $V_{I H}$ and vice versa, so the rendition of the figure has been exaggerated only to facilitate its visualization.)

Also referred to as chatter, the unwanted output transitions can be eliminated if we incorporate hysteresis as depicted in Fig. 5.25b. Here, the comparator exhibits two VTCs, depending on the output state: when $v_{O}=V_{O L}$ the comparator trips when $v_{I}$ raises to $V_{T H}$, and when $v_{O}=V_{O H}$ it trips when $v_{I}$ drops to $V_{T L}$. If the voltage difference $V_{T H}-V_{T L}$, aptly called the hysteresis width, exceeds the maximum peak-topeak amplitude of the input noise, then chatter will be eliminated, as exemplified in Fig. 5.25b. Hysteresis is introduced via positive feedback, either externally by the user $^{7}$ or internally by the IC designer. Here we are interested in the latter.

Figure 5.26 shows a popular CMOS realization of the comparator-withhysteresis concept. Ignoring $M_{5}$ and $M_{6}$ for a moment, we observe that the $M_{4}-M_{7}$ mirror steers $i_{D 2}$ toward the output node $v_{0}$, whereas the $M_{3}-M_{8}$ and $M_{9}-M_{10}$ mirrors steer $i_{D 1}$ away from node $v_{O}$. Consequently, the circuit acts as a differential amplifier with small-signal gain $a=v_{o} /\left(v_{p}-v_{n}\right)=g_{m 1}\left(r_{o 7} / / r_{o 10}\right)$ and a VTC of the type of Fig. 5.20c (see also Fig. 4.66).
image_name:(a)
description:
[
name: V1, type: VoltageSource, ports: {Np: vI, Nn: GND}
name: U1, type: Inverter, ports: {In: vI, Out: vO}
]
extrainfo:The circuit diagram (a) shows a comparator circuit without hysteresis. It consists of a voltage source V1 providing input voltage vI and an inverter U1 that outputs vO. The diagram illustrates comparator chatter, where the output switches rapidly as the input crosses the threshold.
image_name:(b)
description:The graph in figure (b) depicts the behavior of a CMOS comparator with hysteresis. It is a time-domain waveform graph that illustrates how the output voltage \( v_O \) responds to changes in the input voltage \( v_I \) over time.

**Axes Labels and Units:**
- The horizontal axis represents time \( t \), though specific units are not provided, it typically implies seconds or milliseconds in such contexts.
- The vertical axis represents voltage \( v_O \), with key voltage levels marked as \( V_{OH} \) for high output voltage and \( V_{OL} \) for low output voltage.

**Overall Behavior and Trends:**
- The graph shows a waveform where the output voltage \( v_O \) switches between \( V_{OH} \) and \( V_{OL} \) in response to the input voltage \( v_I \).
- The input voltage \( v_I \) is depicted as a sinusoidal or noisy waveform that crosses two threshold levels, \( V_{TH} \) (upper threshold) and \( V_{TL} \) (lower threshold).
- The comparator output remains high \( V_{OH} \) when \( v_I \) exceeds \( V_{TH} \), and low \( V_{OL} \) when \( v_I \) falls below \( V_{TL} \).

**Key Features and Technical Details:**
- The hysteresis effect is evident as the output does not switch states at the same input voltage level. Instead, it requires \( v_I \) to exceed \( V_{TH} \) to switch from low to high, and to fall below \( V_{TL} \) to switch from high to low.
- This behavior eliminates chatter or rapid switching that might occur if the comparator were sensitive to small fluctuations around a single threshold level.

**Annotations and Specific Data Points:**
- The graph includes horizontal lines marking \( V_{TH} \) and \( V_{TL} \), indicating the hysteresis band.
- The waveform shows clear transitions at these threshold levels, demonstrating the stability provided by the hysteresis mechanism.

FIGURE 5.25 Illustrating (a) comparator chatter, and (b) its elimination via hysteresis.
image_name:FIGURE 5.26
description:
[
name: M1, type: NMOS, ports: {S: P1, D: x3, G: vN}
name: M2, type: NMOS, ports: {S: P1, D: x4, G: vP}
name: M3, type: PMOS, ports: {S: VDD, D: x3, G: x4}
name: M4, type: PMOS, ports: {S: VDD, D: x4, G: x3}
name: M5, type: PMOS, ports: {S: x3, D: x3, G: x4}
name: M6, type: PMOS, ports: {S: x4, D: x4, G: x3}
name: M7, type: PMOS, ports: {S: VDD, D: vO, G: x4}
name: M8, type: PMOS, ports: {S: VDD, D: x3, G: x3}
name: M9, type: NMOS, ports: {S: x2, D: x2, G: x1}
name: M10, type: NMOS, ports: {S: P1, D: vO, G: x2}
name: M11, type: NMOS, ports: {S: x1, D: x1, G: x1}
name: M12, type: NMOS, ports: {S: P1, D: VSS, G: x2}
name: I_REF, type: CurrentSource, ports: {Np: x1, Nn: x2}
]
extrainfo:This is a CMOS comparator with hysteresis featuring cross-coupled PMOS transistors M5 and M6, which provide the hysteresis by introducing a flip-flop action. The circuit is powered by VDD and VSS, with input nodes vN and vP, and an output node vO.

FIGURE 5.26 CMOS comparator with hysteresis.

Consider now the effect of having $M_{5}$ and $M_{6}$ present. Viewed as two cross-coupled inverters, these transistors introduce a flip-flop action that keeps the loads seen by $M_{1}$ and $M_{2}$ unbalanced. It is precisely this imbalance that causes hysteresis. To see how, refer to the reduced renditions of Fig. 5.27, where the cross-coupled FETs $M_{5}$ and $M_{6}$ are assumed to have $W / L$ ratios that are $m(m>1)$ times as large as those of the diode-connected FETs $M_{3}$ and $M_{4}$. We make the following observations:

- For $v_{I}$ sufficiently negative as in Fig. 5.27a, $M_{1}$ is off, so $M_{3}$ and $M_{5}$ are also off. All of $I_{S S}$ flows though $M_{2}$, causing $v_{O 2}$ to be low. This forces $M_{5}$ in the ohmic region, thus pulling $v_{O 1}$ to $V_{D D}$. With $v_{S G 6}=0, M_{6}$ is also off, resulting in $i_{D 4}=i_{D 2}=I_{S S}$.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: VO1, G: VI}
name: M2, type: NMOS, ports: {S: GND, D: VO2, G: P}
name: M3, type: PMOS, ports: {S: VDD, D: VO1, G: VO1}
name: M4, type: PMOS, ports: {S: VDD, D: VO2, G: VO2}
name: M5, type: PMOS, ports: {S: VDD, D: VO1, G: VO2}
name: M6, type: PMOS, ports: {S: VDD, D: VO2, G: VO1}
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: VSS}
]
extrainfo:The circuit is a differential amplifier with NMOS input pair M1 and M2. The PMOS transistors M3, M4, M5, and M6 form the active load. For vI << 0, M1 is off, M2 is on, leading to VO1 being pulled to VDD and VO2 being low. ISS flows through M2.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: VO1, D: P, G: VI}
name: M2, type: NMOS, ports: {S: VO2, D: P, G: GND}
name: M3, type: PMOS, ports: {S: VDD, D: VO1, G: VO1}
name: M4, type: PMOS, ports: {S: VDD, D: VO2, G: VO2}
name: M5, type: PMOS, ports: {S: VDD, D: VO1, G: P}
name: M6, type: PMOS, ports: {S: VDD, D: VO2, G: P}
name: VI, type: VoltageSource, ports: {Np: VI, Nn: GND}
name: ISS, type: CurrentSource, ports: {Np: P, Nn: VSS}
]
extrainfo:The circuit is a differential pair with active load, where M1 and M2 form the differential pair and M3 to M6 form the active load. The current source ISS provides the bias current. The circuit operates with a positive input voltage VI, causing M1 to conduct and M2 to turn off, resulting in VO1 being lower than VO2.

FIGURE 5.27 The central part of the circuit of Fig. 5.26 for the cases (a) $v_{l} \ll 0$ and (b) $v_{l} \gg 0$.

- Raising $v_{I}$ will gradually turn on $M_{1}$ at the expense of $M_{2}$ becoming less conductive. Since $M_{1}$ sees the (small) ohmic resistance of $M_{5}$ as load, $v_{O 1}$ will drop some.
- For $v_{I}=0, I_{S S}$ splits equally between $M_{1}$ and $M_{2}$. However, since $k_{5}=m k_{4}$, $m>1$, it follows that $v_{O 1}$ is higher than $v_{O 2}$. In other words, the circuit is unbalanced because $M_{5}$ is still in the triode region whereas $M_{4}$ is saturated.
- To make the circuit trip we need to raise $v_{I}$ to the value $V_{I H}\left(V_{I H}>0\right)$ that will pull $M_{5}$ out of the triode region and into saturation. This value is found via KVL and the familiar FET formula as

$$
\begin{aligned}
V_{I H} & =V_{G S 1}-V_{G S 2}=V_{O V 1}-V_{O V 2} \cong \sqrt{2 I_{D 1} / k_{1}}-\sqrt{2 I_{D 2} / k_{2}} \\
& =\sqrt{2 / k_{1}}\left(\sqrt{I_{D 1}}-\sqrt{I_{D 2}}\right)
\end{aligned}
$$

(For simplicity all FETs are assumed to have $\lambda=0$.) Substituting $I_{D 1}=I_{D 5}=$ $m I_{D 4}=m I_{D 2}$, along with $I_{D 1}+I_{D 2}=I_{S S}$, we finally get, after suitable manipulation,

$$
\begin{equation*}
V_{I H} \cong \sqrt{\frac{2 I_{S S}}{(m+1) k_{1}}}(\sqrt{m}-1) \tag{5.49}
\end{equation*}
$$

- For $v_{I}$ sufficiently positive as in Fig. $5.27 b$ the roles of the various FET pairs are interchanged, so we exploit the symmetry of the circuit to state that in order to make it trip in the opposite direction we now need to lower $v_{I}$ to the value $V_{I L}\left(V_{I L}<0\right)$ such that

$$
\begin{equation*}
V_{I L}=-V_{I H} \tag{5.50}
\end{equation*}
$$

EXAMPLE 5.6 (a) Assuming $k_{n}^{\prime}=2.5 k_{p}^{\prime}=100 \mu \mathrm{~A} / \mathrm{V}^{2}$ and $L=1 \mu \mathrm{~m}$ for all FETs in the circuits of Fig. 5.27, estimate $V_{I H}$ and $V_{I L}$ if $I_{S S}=25 \mu \mathrm{~A}$ and all FETs have $W=10 \mu \mathrm{~m}$, except for $M_{3}$ and $M_{4}$, which have $W_{3}=W_{4}=6 \mu \mathrm{~m}$. What are the values of $I_{D 1}$ and $I_{D 2}$ for $v_{I}=V_{I H}$ ? For $v_{I}=V_{I L}$ ?
(b) Verify the circuits of Fig. 5.27 via PSpice. Assume $\pm 2.5-\mathrm{V}$ power supplies, along with $V_{t n}=-V_{t p}=0.75 \mathrm{~V}$ and $\lambda_{n}^{\prime}=\lambda_{p}^{\prime}=0.05 \mu \mathrm{~m} / \mathrm{V}$. Compare with the calculated values, and comment.

#### Solution

(a) Applying Eqs. (5.49) and (5.50) with $m=10 / 6$ we get

$$
V_{I H} \cong \sqrt{\frac{2 \times 25}{(10 / 6+1)(10 / 1) 100}}(\sqrt{10 / 6}-1) \cong 40 \mathrm{mV}=-V_{I L}
$$

Imposing $I_{D 1}=(10 / 6) I_{D 2}$ and $I_{D 1}+I_{D 2}=25 \mu \mathrm{~A}$ we readily get, for $v_{I}=$ $V_{I H}, I_{D 1} \cong 15.6 \mu \mathrm{~A}$ and $I_{D 2} \cong 9.4 \mu \mathrm{~A}$. For $v_{I}=V_{I L}$ the roles are reversed, so $I_{D 1} \cong 9.4 \mu \mathrm{~A}$ and $I_{D 2} \cong 15.6 \mu \mathrm{~A}$.
image_name:Figure 5.28
description:
[
name: M1, type: NMOS, ports: {S: P, D: V01, G: VI}
name: M2, type: NMOS, ports: {S: P, D: V02, G: GND}
name: M3, type: PMOS, ports: {S: VDD, D: V01, G: V01}
name: M4, type: PMOS, ports: {S: VDD, D: V02, G: V02}
name: M5, type: PMOS, ports: {S: VDD, D: V01, G: V02}
name: M6, type: PMOS, ports: {S: VDD, D: V02, G: V01}
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: IREF, type: CurrentSource, value: 25uA, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a comparator with hysteresis, using NMOS and PMOS transistors in a differential configuration. It operates between VDD (2.5V) and VSS (-2.5V) with a reference current of 25 µA. The input voltage VI is compared to generate output voltages at nodes V01 and V02.

FIGURE 5.28 PSpice circuit to investigate the hysteresis of the comparator of Example 5.6.
image_name:(a)
description:The graph labeled as "(a)" is a hysteresis plot showing the transfer characteristics of a comparator circuit. It is a voltage versus voltage graph, specifically plotting the difference in output voltages \( v_{O1} - v_{O2} \) on the vertical axis against the input voltage \( v_{I} \) on the horizontal axis.

1. **Type of Graph and Function:**
- This is a hysteresis plot, typical in comparator circuits to illustrate the switching behavior as the input voltage varies.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( v_{I} \) with units in millivolts (mV), ranging from -200 mV to 200 mV.
- The vertical axis is labeled \( v_{O1} - v_{O2} \) with units in volts (V), ranging from -2 V to 2 V.
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The graph exhibits a characteristic hysteresis loop, indicating that the output voltage difference depends not only on the current input voltage but also on the previous state.
- As \( v_{I} \) increases, the output voltage difference transitions from a high state to a low state, and as \( v_{I} \) decreases, it transitions back to a high state, forming a loop.

4. **Key Features and Technical Details:**
- The width of the hysteresis loop indicates the voltage range over which the comparator switches states.
- The critical switching points are symmetric around the origin, with a noticeable change in the output voltage difference occurring at approximately ±35.7 mV, consistent with the context provided.

5. **Annotations and Specific Data Points:**
- No specific annotations or markers are present on the graph, but the loop's width is significant for understanding the comparator's hysteresis behavior.
- The graph visually demonstrates the snapping action described, where the transition between states occurs abruptly at the threshold voltages.
image_name:(b)
description:The graph labeled (b) is a detailed view of the transfer characteristics of a comparator with hysteresis, specifically focusing on the snapping action as the input voltage $v_I$ is varied. This is a voltage transfer characteristic plot.

1. **Axes Labels and Units:**
- The x-axis represents the input voltage $v_I$ in millivolts (mV), ranging from 30 mV to 40 mV.
- The y-axis represents the output voltages $v_{O1}$ and $v_{O2}$ in volts (V), ranging from 1.0 V to 2.5 V.

2. **Overall Behavior and Trends:**
- The graph shows a sharp transition between the output voltages as the input voltage crosses certain threshold values, indicative of hysteresis behavior.
- As $v_I$ increases, $v_{O1}$ remains high until approximately 35.7 mV, at which point it sharply drops to a lower voltage level.
- Conversely, $v_{O2}$ remains low and then sharply rises as $v_I$ reaches the same threshold, indicating a complementary behavior between $v_{O1}$ and $v_{O2}$.

3. **Key Features and Technical Details:**
- The critical threshold voltage where the snapping action occurs is approximately 35.7 mV, which is the hysteresis point where the output voltages switch states.
- This behavior demonstrates the bistable nature of the comparator, where the output depends on both the current and past input conditions.

4. **Annotations and Specific Data Points:**
- The graph includes annotations indicating the positions of $v_{O1}$ and $v_{O2}$, highlighting their behavior as the input voltage is varied.
- The plot provides a visual representation of the hysteresis loop, showing the distinct switching behavior of the comparator circuit.

FIGURE 5.29 Transfer characteristics of the comparator of Fig. 5.28: (a) hysteresis and (b) detail.
(b) Using the PSpice circuit of Fig. 5.28 we readily obtain the plots of Fig. 5.29, from which we find $V_{I H}=-V_{I L}=35.7 \mathrm{mV}$. This value differs from 40 mV because our hand calculations are based on $\lambda=0$. Figure $5.29 b$ provides an expanded view of the snapping action taking place as $v_{I}$ is raised to $V_{I H}$. Once $M_{1}$ pulls $M_{5}$ out of the triode region, $v_{O 1}$ drops more rapidly until $M_{6}$ turns on. At this point $M_{6}$ pulls $v_{O 2}$ toward $V_{D D}$ as fast as it can. This, in turn, shuts off $M_{5}$, causing a final and more rapid drop in $v_{O I}$. It is apparent that because of the flip-flop action provided by $M_{5}$ and $M_{6}, v_{O 1}$ and $v_{O 2}$ coexist only in complementary form (one is high whereas the other is low, and vice versa).

#### Solution

(a) Assuming $V_{B E}=0.7 \mathrm{~V}$, use Ohm's law to calculate $R=(5-0.7) / 0.25=$ $17.2 \mathrm{k} \Omega$.
(b) With $V_{C C}=6 \mathrm{~V}$ we get $I_{R E F}=I_{B I A S} \cong(6-0.7) / 17.2=0.308 \mathrm{~mA}$, indicating a percentage increase of $100(0.308-0.25) / 0.25 \cong 23 \%$, quite a change!
(a) Let the FETs of Fig. $5.30 b$ have $V_{t}=0.75 \mathrm{~V}$ and $k^{\prime}=125 \mu \mathrm{~A} / \mathrm{V}^{2}$. Assuming $V_{D D}=5 \mathrm{~V}$, specify $R$ and $W / L$ so that both FETS draw $100 \mu \mathrm{~A}$ with $V_{O V}=0.25 \mathrm{~V}$.
(b) Estimate the percentage change in $I_{R E F}$ if $V_{D D}$ is raised from 5 V to 6 V .
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: VBE, E: GND}
name: Q2, type: NPN, ports: {C: VBE, B: VBE, E: GND}
name: R, type: Resistor, value: R, ports: {N1: VCC, N2: VBE}
]
extrainfo:The circuit diagram (a) is a bipolar power-supply-based current reference. It uses two NPN transistors (Q1 and Q2) and a resistor (R) to establish a bias current (IBIAS) and a reference current (IREF). The voltage across the base-emitter junctions (VBE) of the transistors is maintained by the resistor R connected to VCC. The circuit is grounded at GND.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: VGS, G: VCS}
name: M2, type: NMOS, ports: {S: GND, D: IRE, G: VGS}
name: R, type: Resistor, value: R, ports: {N1: VDD, N2: VCS}
]
extrainfo:The circuit is a MOS-based current reference with NMOS transistors M1 and M2. Resistor R is used to set the bias current IBIAS. The voltage VGS is formed between the gate and source of M1 and M2, with M1 and M2 sharing the same gate voltage. The current IREF is drawn from the drain of M2.
image_name:(c)
description:
[
name: R, type: Resistor, value: R, ports: {N1: VDD, N2: d1s1}
name: M1, type: NMOS, ports: {S: GND, D: d1s1, G: d1s1}
name: M2, type: NMOS, ports: {S: d1s1, D: IREFF, G: d1s1}
name: M3, type: PMOS, ports: {S: VDD, D: d1s1, G: d1s1}
]
extrainfo:The circuit diagram (c) shows a MOS-based current reference with a PMOS and two NMOS transistors. The PMOS (M3) sources current from VDD to the node d1s1, which is shared by the NMOS transistors M1 and M2. M1 is configured as a diode-connected transistor, setting the gate-source voltage for M2, which mirrors the current to IREF. The resistor R sets the bias current IBIAS.

FIGURE 5.30 Power-supply-based current references: (a) bipolar, and (b) MOS. (c) All MOS version.

#### Solution

(a) Since $V_{G S}=0.75+0.25=1 \mathrm{~V}$, Ohm's law gives $R=(5-1) / 0.1=40 \mathrm{k} \Omega$. Moreover, imposing $0.1=(0.125 / 2) \times(W / L) \times 0.25^{2}$ gives $W / L=25.6$.
(b) From part (a) we have $k=k^{\prime}(W / L)=0.125 \times 25.6=3.2 \mathrm{~mA} / \mathrm{V}^{2}$. Imposing

$$
I_{B I A S}=\frac{6-0.75-\sqrt{2 I_{B I A S} /\left(3.2 \times 10^{-3}\right)}}{40 \times 10^{3}}
$$

and solving by iteration gives $I_{R E F}=I_{B I A S} \cong 124 \mu \mathrm{~A}$, indicating a $24 \%$ increase, quite a change!

The above examples indicate a fairly strong dependence of $I_{R E F}$ upon the supply voltage. As an example, the biasing scheme of the 741 op amp of Fig. 5.4 gives, for $\pm 15-\mathrm{V}$ supplies, $I_{R E F}=(30-1.4) / 39=733 \mu \mathrm{~A}$. However, should the user opt for a pair of $\pm 9-\mathrm{V}$ supply batteries, $I_{R E F}$ would drop to $(18-1.4) / 39=426 \mu \mathrm{~A}$, causing appreciable changes in most small-signal parameters. In the following we shall explore ways to reduce the dependence of $I_{R E F}$ on the power supply.

#### Solution

(a) We have $V_{B E}=0.026 \ln \left(125 \times 10^{-6} / 10^{-15}\right)=0.664 \mathrm{~V}$ so $R=0.664 / 0.25=$ $2.66 \mathrm{k} \Omega$. By the $18-\mathrm{mV}$ rule of thumb, $V_{B E 2}=V_{B E}+18 \mathrm{mV}=0.682 \mathrm{~V}$. So, $R_{B I A S}=(5-0.682-0.664] /(0.25 / 2)=29.2 \mathrm{k} \Omega$. With $V_{C C}=6 \mathrm{~V}$ we get $\left.I_{B A S} \cong[6-2 \times 0.67)\right] / 29.2=159 \mu \mathrm{~A}, V_{B E}=0.026 \ln \left(159 \times 10^{-6} / 10^{-15}\right)=$ 0.670 V , and $I_{R E F}=0.670 / 2.66=252.5 \mu \mathrm{~A}$. This represents an increase in $I_{R E F}$ of $100(252.5-250) / 250 \cong 1 \%$, quite an improvement over the $23 \%$ increase of Example 5.7!
(b) From Example 5.8 we have $V_{G S}=0.75+0.25=1 \mathrm{~V}$, so $R=1 / 0.1=10 \mathrm{k} \Omega$ and $\left.R_{B I A S}=[5-1-1)\right] /(0.1)=30 \mathrm{k} \Omega$. As we raise $V_{D D}$ from 5 V to 6 V we expect the change in $V_{G S 2}$ to be negligible compared to the change in $V_{D D}$, so we write $I_{B A A S} \cong\left[6-0.75-\left(2 I_{B A A S} / 3.2\right)^{1 / 2}-1\right] / 30$. Solving by iterations gives $I_{B I A S}=0.132 \mathrm{~mA}$. Consequently, $V_{G S}=0.75+(2 \times 0.132 / 3.2)^{1 / 2}=$ 1.037 V and $I_{R E F}=1.037 / 10=103.7 \mu \mathrm{~A}$, indicating a $3.7 \%$ increase in $I_{R E F}$, an appreciable improvement over $24 \%$ of Example 5.8!

#### EXAMPLE 5.10

(a) Assuming $m_{p}=2$ in the circuit of Fig. 5.32a, specify $m_{n}$ and $R$ for the roomtemperature values $\Delta V_{B E}=75 \mathrm{mV}$ and $I_{R E F}=0.25 \mathrm{~mA}$.
(b) Assuming $m_{p}=1$ and $k_{1}=1.25 \mathrm{~mA} / \mathrm{V}^{2}$ in the circuit of Fig. $5.32 b$, specify $m_{n}$ and $R$ for $\Delta V_{G S}=0.3 \mathrm{~V}$ and $I_{R E F}=0.1 \mathrm{~mA}$.

#### Solution

(a) Use Eq. (5.53) to impose $75=26 \ln \left(2 m_{n}\right)$. This gives $m_{n} \cong 9$. Moreover, $R=75 / 0.25=300 \Omega$.
(b) Use Eq. (5.55) to impose $0.3=\sqrt{2 \times 0.1 / 1.25}\left(1-1 / \sqrt{m_{n}}\right)$. Then, $m_{n}=16$ and $R=0.3 / 0.1=3 \mathrm{k} \Omega$.

Equations (5.54) and (5.56) imply a supply-independent $I_{R E F}$. In practice, because of base-width modulation in the BJTs and channel-length modulation in the FETs, $I_{\text {REF }}$ will depend on the supply voltage somewhat. To get an idea, refer to the small-signal equivalent of Fig. 5.33, and use the test method to find the change $i$
image_name:FIGURE 5.33
description:
[
name: r_o3, type: Resistor, value: r_o3, ports: {N1: V, N2: v1}
name: r_1, type: Resistor, value: r_1, ports: {N1: v1, N2: GND}
name: m_p, type: CurrentControlledCurrentSource, ports: {Np: V, Nn: v1}
name: G_m2, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: v2}
name: r_4, type: Resistor, value: r_4, ports: {N1: V, N2: v2}
name: R_o2, type: Resistor, value: R_o2, ports: {N1: v2, N2: GND}
name: v, type: VoltageSource, value: v, ports: {Np: V, Nn: GND}
]
extrainfo:The circuit is a small-signal model to analyze power-supply dependence of a reference current. It includes resistors, a current-controlled current source, a voltage-controlled current source, and a voltage source. The circuit is grounded at multiple points and uses a dependent current source to model transistor behavior.

FIGURE 5.33 Small-signal model to find the power-supply dependence of a mismatch-based reference current.
experienced by $I_{R E F}$ due to a change $v$ in the power supply. Here, the diode-connected transistors $Q_{1} / M_{1}$ and $Q_{4} / M_{4}$ are modeled by their (small) ac resistances $r_{1} \cong 1 / g_{m 1}$ and $r_{4} \cong 1 / g_{m 4}$, the mirror transistor $Q_{3} / M_{3}$ is modeled by a dependent source $m_{p} i$ with parallel resistance $r_{03}$, and the degeneration resistance $R$ has been absorbed into the model for transistor $Q_{2} / M_{2}$ by letting

$$
G_{m 2} \cong g_{m 2} /\left(1+g_{m 2} R\right) \quad R_{o 2} \cong r_{o 2}\left(1+g_{m 2} R\right)
$$

(for simplicity we are ignoring $M_{2}$ 's body effect). Using nodal analysis along with KVL we get

$$
\frac{v-v_{1}}{r_{o 3}}+m_{p} i=\frac{v_{1}}{r_{1}} \quad i=G_{m 2} v_{1}+\frac{v-r_{4} i}{R_{o 2}}
$$

Typically $r_{o 3} \gg r_{1}$ and $r_{4} / R_{o 2} \ll 1$, so the above expressions simplify as

$$
\frac{v}{r_{o 3}}+m_{p} i \cong \frac{v_{1}}{r_{1}} \cong g_{m 1} v_{1} \quad i \cong G_{m 2} v_{1}+\frac{v}{R_{o 2}}
$$

Eliminating $v_{1}$, collecting, and simplifying, we get

$$
\begin{equation*}
\frac{i}{v}=\frac{1+\left(g_{m 2} / g_{m 1}\right) \times\left(r_{o 2} / r_{o 3}\right)}{R_{o 2}\left(1-m_{p} G_{m 2} / g_{m 1}\right)} \tag{5.57}
\end{equation*}
$$

It is apparent that the larger $R_{o 2}$ the less dependent the current from the supply voltage. If desired, we can reduce this dependence further by cascoding $Q_{2}$ and $M_{2}$.

#### EXercise 5.2

Derive Eq. (5.57). Hence, show that in the bipolar case Eq. (5.57) can be expressed as

$$
\frac{i}{v}=\frac{\left(1+V_{A n} / V_{A p}\right) \times\left[1+1 /\left(g_{m 2} R\right)\right]}{R_{o 2}}
$$

where $V_{A n}$ and $V_{A p}$ are the Early voltages of the $n p n$ and the $p n p$ BJTs, respectively.
(a) If all BJTs of Example 5.10a have $V_{A}=50 \mathrm{~V}$, estimate the percentage change in $I_{R E F}$ brought about by a 1-V change in $V_{C C}$.
(b) If all FETs of Example $5.10 b$ have $\lambda=1 /(20 \mathrm{~V})$, estimate the percentage change in $I_{R E F}$ brought about by a 1-V change in $V_{D D}$.

#### Solution

(a) We have $g_{m 2}=I_{R E F} / V_{T}=0.25 / 26=1 /(104 \Omega), r_{o 2}=V_{A} / I_{R E F}=50 / 0.25=$ $200 \mathrm{k} \Omega$, and $R_{o 2}=200(1+300 / 104)=777 \mathrm{k} \Omega$. Using the expression of Exercise 5.2,

$$
\frac{i}{v}=\frac{(1+50 / 50) \times[1+1 /(300 / 104)]}{777}=\frac{1}{288 \mathrm{k} \Omega}
$$

Letting $\Delta I_{R E F}=(1 \mathrm{~V}) /(288 \mathrm{k} \Omega)=3.47 \mu \mathrm{~A}$ indicates a per-volt change of $100(3.47 / 250) \cong 1.4 \%$.
(b) We have $g_{m 1}=(2 \times 1.25 \times 0.1)^{1 / 2}=0.5 \mathrm{~mA} / \mathrm{V}, g_{m 2}=(2 \times 16 \times 1.25 \times$ $0.1)^{1 / 2}=2 \mathrm{~mA} / \mathrm{V}=4 g_{m 1}, r_{o 2}=r_{o 3}=20 / 0.1=200 \mathrm{k} \Omega, G_{m 2}=2 /(1+2 \times 3)=$ $1 /(3.5 \mathrm{k} \Omega)$, and $R_{o 2}=200(1+2 \times 3)=1.4 \mathrm{M} \Omega$. By Eq. (5.57),

$$
\frac{i}{v}=\frac{1+(4) \times(1)}{1400[1-1 \times(1 / 3.5) / 0.5)]}=\frac{1}{120 \mathrm{k} \Omega}
$$

Letting $\Delta I_{R E F}=(1 \mathrm{~V}) /(120 \mathrm{k} \Omega)=8.3 \mu \mathrm{~A}$ indicates a per-volt change of $8.3 \%$.

### Startup Circuits

The circuits of Fig. 5.32 are said to be self-biased or bootstrapped because each mirror biases and is in turn biased by the other. In particular, if one of the mirrors fails to turn on, so will the other and the circuit will remain in this unwanted state indefinitely. We therefore need a mechanism that, once the circuit receives power, will turn on at least one of the mirrors, forcing the circuit to evolve toward the desired state and remain there. Aptly referred to as startup circuit, in its simplest form it consists of a large resistance $R_{\text {startup }}$ to inject a small startup current into one of the mirrors. This is shown in Fig. 5.34a for the bipolar case. (It goes without saying that such a current must be much smaller than $I_{R E F}$ in order to avoid introducing an intolerable error.)

A more elegant approach is a startup circuit that intervenes only when the reference is in the unwanted state, but goes dormant once the reference has reached the desired state. In the CMOS example of Fig. $5.34 b$ the diode-connected transistors $M_{7}$ and $M_{8}$ form a voltage divider to provide a suitable gate bias for $M_{9}$. Should $M_{1}$ be off, $V_{G S 9}$ is designed to be high enough to turn on $M_{9}$ and thus force both mirrors out of the cutoff state. Once $M_{1}$ turns fully on, $V_{G S 9}$ is designed to drop below $V_{t 9}$ so as to turn $M_{9}$ off, leaving the rest of the circuit undisturbed.

Since the current $I_{R E F}$ is used internally, provision must be made for its replication to the outside. In Fig. 5.34 this function is provided by $Q_{5} / M_{5}$ when the stabilized current is to be sourced to an external load, and by $Q_{6} / M_{6}$ when it is to be sunk from an external load.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: X2, B: X2, E: GND}
name: Q2, type: NPN, ports: {C: X2, B: X2, E: GND}
name: Q3, type: PNP, ports: {C: X1, B: X2, E: VCC}
name: Q4, type: PNP, ports: {C: X1, B: X2, E: VCC}
name: Q5, type: PNP, ports: {C: I5, B: X1, E: VCC}
name: Q6, type: NPN, ports: {C: I6, B: X2, E: GND}
name: Rstartup, type: Resistor, value: Rstartup, ports: {N1: X2, N2: X1}
name: R, type: Resistor, value: R, ports: {N1: X3, N2: GND}
]
extrainfo:The circuit diagram (a) is a bipolar mismatch-based current reference with a start-up circuit. It uses transistors Q1 to Q6 and resistors Rstartup and R to establish a reference current IREF. The circuit incorporates positive feedback, which may lead to instability if the loop gain exceeds unity.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X3, G: X1}
name: M2, type: NMOS, ports: {S: X3, D: X2, G: X1}
name: M3, type: PMOS, ports: {S: VDD, D: X2, G: X3}
name: M4, type: PMOS, ports: {S: VDD, D: X2, G: X2}
name: M5, type: PMOS, ports: {S: VDD, D: X2, G: X2}
name: M6, type: NMOS, ports: {S: X3, D: GND, G: X2}
name: M7, type: PMOS, ports: {S: VDD, D: X1, G: X1}
name: M8, type: NMOS, ports: {S: GND, D: X1, G: X1}
name: M9, type: NMOS, ports: {S: X3, D: X2, G: X1}
name: R, type: Resistor, value: R, ports: {N1: X2, N2: GND}
]
extrainfo:The circuit is a CMOS mismatch-based current reference with a start-up circuit. It uses positive feedback, which may lead to instability if the loop gain exceeds unity.

FIGURE 5.34 Mismatch-based current references with start-up circuit examples: (a) bipolar and (b) CMOS.

A final caveat is in order, namely, the circuits of Fig. 5.34 incorporate positive feedback, a situa-tion that may lead to instability if the loop gain exceeds unity (more on this in Chapter 7). With reference to Fig. 5.33 we observe that the current $i$ is first amplified to $m_{p} i$ by $Q_{3}$, then it is converted to $v_{1} \cong r_{1} m_{p} i \cong m_{p} i / g_{m 1}$ by $Q_{1}$, and finally it is returned by $Q_{2}$ as $G_{m 2} v_{1} \cong\left(m_{p} G_{m 2} / g_{m 1}\right) i$, so the overall amplification experienced by $i$ around the loop, aptly called the loop gain $T$, is $T=m_{p} G_{m 2} / g_{m 1}$. To avert instability we must ensure that $T<1$ (indeed, Example $5.11 a$ has $T=0.257 \mathrm{~A} / \mathrm{A}$, and Example $5.11 b$ has $T=0.571 \mathrm{~A} / \mathrm{A}$.)

#### Solution

We have $\Delta V_{B E}=V_{T} \ln \left(m_{p} \times m_{n}\right)=26 \ln (1 \times 8)=54 \mathrm{mV}, R_{1}=\Delta V_{B E} / I_{E 2} \cong$ $54 / 0.1=0.54 \mathrm{k} \Omega$, and $R=1 / 0.1=10 \mathrm{k} \Omega$. We also have $V_{B E 1}=V_{T} \ln \left[\left(0.1 \times 10^{-3}\right) /\right.$ $\left.\left(2 \times 10^{-15}\right)\right]=640.5 \mathrm{mV}$. Use Eq. (5.60) to impose

$$
(1+1) \frac{R_{2}}{0.54} \ln (1 \times 8)=\frac{1,205-640.5}{26}+4-1.5
$$

and get $R_{2}=3.14 \mathrm{k} \Omega$. By Eq. (5.61) we have $V_{B G}=1.205+(4-1.5) 0.026=$ 1.27 V . Finally, use Eq. (5.62) to impose $5.0=\left(1+R_{3} / R_{4}\right) 1.27$ and get $R_{3} / R_{4}=$ 2.94. Use $R_{4}=10 \mathrm{k} \Omega$ and $R_{3}=29.4 \mathrm{k} \Omega$.
image_name:FIGURE 5.36 Thermal variation of a bandgap reference.
description:The graph in Figure 5.36 is a plot depicting the thermal variation of a bandgap reference voltage, denoted as \( V_{BG} \), as a function of temperature \( T \).

1. **Type of Graph and Function:**
- This is a line graph showing how the bandgap reference voltage changes with temperature.

2. **Axes Labels and Units:**
- The x-axis represents temperature \( T \) in degrees Celsius (°C), ranging from -50°C to 100°C.
- The y-axis represents the bandgap reference voltage \( V_{BG} \) in volts (V), with values ranging from approximately 1.265 V to 1.270 V.

3. **Overall Behavior and Trends:**
- The graph shows a slight parabolic shape, indicating that \( V_{BG} \) increases to a peak and then decreases as temperature moves away from a central point.
- The peak occurs at a specific temperature \( T_0 \), which is marked on the graph.

4. **Key Features and Technical Details:**
- The peak voltage \( V_{BG} \) is around 1.270 V, occurring at the temperature \( T_0 \).
- The voltage decreases slightly as the temperature moves away from \( T_0 \) both in the negative and positive direction on the temperature scale.

5. **Annotations and Specific Data Points:**
- The graph is annotated with \( T_0 \) at the peak, which is the temperature where \( V_{BG} \) reaches its maximum value.
- The curve is symmetric around \( T_0 \), showing that the temperature coefficient \( \text{TC}(V_{BG}) \) is zero at this point, as suggested in the context.

This graph illustrates the dependence of the bandgap reference voltage on temperature, highlighting the stability around the temperature \( T_0 \).

FIGURE 5.36 Thermal variation of a bandgap reference.

One last observation is in order. Equation (5.60) provides the value of $K$ necessary to achieve $\mathrm{TC}\left(V_{B G}\right)=0$ at a specific temperature $T_{0}$, typically ambient temperature. Since $K$ depends on $V_{B E 1}$ and $V_{T}$, themselves functions of temperature, $\operatorname{TC}\left(V_{B G}\right)$ will depart from zero at temperatures other than $T_{0}$. As depicted in Fig. 5.36, the plot of $V_{B G}$ as a function of $T$ exhibits a curvature ${ }^{1}$ typical of this class of references. (The student is encouraged to look up the literature ${ }^{1-3}$ for clever curvature-correction techniques designed to compensate for this higher-order effect.)

#### Solution

We have $\Delta V_{E B}=26 \ln (10 \times 1)=59.9 \mathrm{mV}, R_{1}=\Delta V_{E B} / I_{E 2}=\Delta V_{E B} /\left(I_{E 1} / 10\right)=$ $\left(59.9 \times 10^{-3}\right) /\left(10 \times 10^{-6}\right)=5.99 \mathrm{k} \Omega$, and $V_{E B 1}=V_{T} \times \ln \left[\left(100 \times 10^{-6}\right) / 10^{-15}\right]=$ 658.5 mV . The calculation of $K$ yields

$$
(10+1) \frac{R_{2}}{5.99} \ln (10 \times 1)=\frac{1,205-658.5}{26}+4-1.5
$$

This gives $R_{2}=5.56 \mathrm{k} \Omega$ and $m_{p} R_{2}=55.6 \mathrm{k} \Omega$.

## 5.6 CURRENT-MODE INTEGRATED CIRCUITS

The voltages and currents in a linear circuit are mathematically equivalent because the laws governing voltages admit counterpart laws governing currents, and vice versa (familiar examples of this equivalence, known as duality, are Kirchhoff's voltage/ current laws, the node/loop methods, and the Thévenin/Norton theorems). However, transistors, the basic ingredients of today's electronics, are nonlinear devices that process voltage and current differently. Specifically, the exponential characteristics of BJTs and the quadratic characteristics of FETs indicate inherently wider dynamic ranges for currents than for voltages: for instance, a 10 -to-1 ( 20 dB ) change in the overdrive voltage of a FET results a $100-$ to-1 $(40 \mathrm{~dB})$ change in the channel current. It also turns out that the manipulation of currents in a physical circuit is inherently faster than the manipulation of voltages: this is so because stray inductances, which
oppose rapid changes in mesh currents, are of far lesser consequence than stray capacitances, which oppose rapid changes in node voltages (these aspects will be investigated in great detail in Chapter 6). These advantages in both range and speed provide a strong motivation for current-mode circuits, that is, circuits emphasizing the manipulation of currents over voltages. (Interestingly, the engineering community has traditionally favored the voltage viewpoint, as signified by the fact that voltage-mode circuits have reached commercial maturity and popularity well ahead of current-mode circuits, a classic example being the op amp, a voltage-in/voltage-out block. The development of current-mode analog ICs has been delayed also by technological reasons, such as the ability to fabricate monolithic pnp BJTs of comparable quality to their $n p n$ counterparts.) In this section we investigate current-mode circuits such as transconductors, current conveyors (CCs), operational transconductance amplifiers (OTAs), current feedback amplifiers (CFAs), and Gilbert Cells.

### Transconductors

A transconductor is a voltage-in/current-out circuit. To prevent loading, a transconductor should exhibit sufficiently high (ideally infinite) resistances both at the input and at the output terminals. The simplest transconductor is the transistor itself. However, transistors operate over only one quadrant of their $i_{C}-v_{B E}$ or $i_{D}-v_{G S}$ characteristics. To cope with this drawback, we bias the transistor at a specified operating point in the active region, and we then achieve four-quadrant operation by effecting variations, both positive and negative, about this point. But we need to keep these variations suitably small in order to ensure approximately linear circuit operation, this being the basis of small-signal models.

We can achieve much more versatility and flexibility if we manage to (a) establish the operating point right at the origin of the $i-v$ characteristic, and (b) lift the small-signal constraint altogether. A circuit meeting meets both demands is shown in Fig. 5.38 (though the version shown is bipolar, a CMOS version is readily obtained by replacing each BJT with a MOSFET of the corresponding type). We make the following observations:

- In order to handle emitter currents of either polarity, the class AB pair $Q_{1}-Q_{2}$ is used, with $Q_{1}$ sourcing current to and $Q_{2}$ sinking current from the circuitry external to node $E$ (this is similar to the push-pull output stages of Chapter 4).
- The emitter followers $Q_{3}-Q_{4}$ generate the pair of junction voltage drops needed to bias the $Q_{1}-Q_{2}$ pair for class AB operation. They also provide a Darlington function to raise the input resistance as well as lower the input bias current of node $B$. It is apparent that $Q_{1}$ through $Q_{4}$ form a voltage buffer with approximately unity gain, as depicted in the simplified equivalent circuit at the right. Assuming matched voltage drops $V_{E B 3}=V_{B E 1}$ and $V_{B E 4}=V_{E B 2}$, we thus have

$$
\begin{equation*}
v_{E}=v_{B} \tag{5.63}
\end{equation*}
$$

- The Wilson current mirrors $Q_{5}-Q_{6}-Q_{7}$ and $Q_{10}-Q_{9}-Q_{8}$ replicate the collector currents of $Q_{1}$ and $Q_{2}$, respectively, and convey them to the output node $C$, where they are subtracted from each other to give the output current $i_{C}=i_{7}-i_{8}=i_{1}-i_{2}$.
image_name:Bipolar transcoductor
description:
[
name: Q1, type: NPN, ports: {C: C, B: E, E: E}
name: Q2, type: NPN, ports: {C: E, B: B, E: V_EE}
name: Q3, type: NPN, ports: {C: E, B: B, E: B}
name: Q4, type: NPN, ports: {C: B, B: B, E: V_EE}
name: Q5, type: PNP, ports: {C: V_CC, B: E, E: B}
name: Q6, type: PNP, ports: {C: V_CC, B: B, E: C}
name: Q7, type: PNP, ports: {C: C, B: C, E: E}
name: Q8, type: PNP, ports: {C: V_EE, B: E, E: C}
name: Q9, type: PNP, ports: {C: V_EE, B: C, E: B}
name: Q10, type: PNP, ports: {C: V_EE, B: B, E: E}
name: I3, type: CurrentSource, value: I3, ports: {Np: V_CC, Nn: E}
name: I4, type: CurrentSource, value: I4, ports: {Np: B, Nn: V_EE}
]
extrainfo:The circuit is a bipolar transconductor utilizing Wilson current mirrors for current replication. The output current is the difference between the collector currents of Q1 and Q2, i.e., iC = i1 - i2. The output resistance at node C is influenced by the Wilson mirror resistances.
image_name:simplified circuit representation
description:
[
name: Q1, type: NPN, ports: {C: C, B: E, E: GND}
name: Q2, type: NPN, ports: {C: E, B: B, E: GND}
name: Q3, type: NPN, ports: {C: E, B: B, E: GND}
name: Q4, type: NPN, ports: {C: B, B: B, E: GND}
name: Q5, type: PNP, ports: {C: C, B: VCC, E: E}
name: Q6, type: PNP, ports: {C: VCC, B: VCC, E: C}
name: Q7, type: PNP, ports: {C: C, B: VCC, E: GND}
name: Q8, type: PNP, ports: {C: GND, B: VEE, E: C}
name: Q9, type: PNP, ports: {C: VEE, B: VEE, E: GND}
name: Q10, type: PNP, ports: {C: B, B: VEE, E: GND}
name: I3, type: CurrentSource, value: I3, ports: {Np: VCC, Nn: B}
name: I4, type: CurrentSource, value: I4, ports: {Np: B, Nn: VEE}
]
extrainfo:The circuit is a bipolar transconductor using Wilson current mirrors to replicate and subtract collector currents. The output current i_C is equal to the emitter current i_E. The output node C has an output resistance determined by the parallel combination of Wilson mirror resistances.
image_name:circuit symbol
description:
[
name: Q1, type: NPN, ports: {C: C, B: B, E: E}
name: Q2, type: NPN, ports: {C: E, B: B, E: VEE}
name: Q3, type: PNP, ports: {C: B, B: E, E: VCC}
name: Q4, type: PNP, ports: {C: VCC, B: B, E: B}
name: Q5, type: NPN, ports: {C: VCC, B: B, E: C}
name: Q6, type: NPN, ports: {C: VCC, B: C, E: C}
name: Q7, type: NPN, ports: {C: C, B: C, E: E}
name: Q8, type: PNP, ports: {C: E, B: C, E: VEE}
name: Q9, type: PNP, ports: {C: VEE, B: C, E: VEE}
name: Q10, type: PNP, ports: {C: B, B: VEE, E: VEE}
name: I3, type: CurrentSource, value: I3, ports: {Np: VCC, Nn: B}
name: I4, type: CurrentSource, value: I4, ports: {Np: B, Nn: VEE}
]
extrainfo:The circuit is a bipolar transconductor using Wilson current mirrors to replicate and subtract collector currents. It uses NPN and PNP transistors to manage current flow from VCC to VEE, with outputs at node C.

FIGURE 5.38 Bipolar transcoductor, simplified circuit representation, and circuit symbol used sometimes.

But, applying KCL at the voltage-buffer supernode we have, assuming negligible base currents, $i_{1}=i_{2}+i_{E}$, or $i_{1}-i_{2}=i_{E}$. Eliminating the difference $i_{1}-i_{2}$ gives

$$
\begin{equation*}
i_{C}=i_{E} \tag{5.64}
\end{equation*}
$$

Finally, the output resistance at node $C$ is the parallel combination of the Wilsonmirror resistances $R_{c 7} \cong\left(\beta_{o 7} / 2\right) r_{o 7}$ and $R_{c 8} \cong\left(\beta_{o 8} / 2\right) r_{o 8}$. Using subscripts $n$ and $p$ as usual, we write

$$
\begin{equation*}
R_{c} \cong\left(\frac{\beta_{o n}}{2} r_{o n}\right) / /\left(\frac{\beta_{o p}}{2} r_{o p}\right) \tag{5.65}
\end{equation*}
$$

It is apparent that the transconductor can be regarded as a form of idealized transistor having (a) zero B-E voltage drop, (b) much higher input and output resistances than an ordinary transistor (this, thanks to the Darlington circuitry at the input and the Wilson circuitry at the output), and (c) full four-quadrant operation (for instance, if we terminate node $E$ on a resistive load to ground, $i_{E}$ and $i_{C}$ will flow out of the transconductor for $v_{B}>0$, but into the transconductor for $v_{B}<0$ ). Also called macro transistor, diamond transistor, and Current Conveyor II +, the transconductor shown can be used in its own right in the basic configurations of CC, CB , and CE , or as a building block for other current-mode ICs.

### Current-Feedback Amplifiers (CFAs)

Feeding node $C$ of the transconductor of Fig. 5.38 to another voltage buffer as in Fig. 5.39 turns it into a voltage-output circuit. Called current-feedback amplifier (CFA), the circuit replaces the conventional op amp in certain high-speed applications. To investigate this circuit, refer to the simplified equivalent of Fig. 5.40a, explicitly showing the net equivalent resistance $R_{e q}$ of node $C$ toward ground. With an eye on Fig. 5.39, we use inspection to find this resistance as

$$
\begin{equation*}
R_{e q}=R_{c 7} / / R_{c 8} / / / R_{b 13} / / R_{b 14} \tag{5.66}
\end{equation*}
$$

where $R_{c}$ and $R_{b}$ denote resistances seen looking into collectors and bases. Also by inspection we have

$$
\begin{equation*}
v_{O}=R_{e q} i_{N} \tag{5.67}
\end{equation*}
$$

Turning next to the typical feedback interconnection of Fig. 5.40b, we sum currents into node $v_{N}$ to get

$$
i_{N}+\frac{0-v_{N}}{R_{1}}+\frac{v_{O}-v_{N}}{R_{2}}=0
$$

image_name:FIGURE 5.39 Current-feedback amplifier
description:
[
name: Q1, type: NPN, ports: {C: VN, B: VP, E: C}
name: Q2, type: NPN, ports: {C: C, B: VN, E: VEE}
name: Q3, type: PNP, ports: {C: VN, B: VP, E: VEE}
name: Q4, type: PNP, ports: {C: VP, B: VCC, E: VEE}
name: Q5, type: PNP, ports: {C: VCC, B: VP, E: VN}
name: Q6, type: PNP, ports: {C: VCC, B: VN, E: C}
name: Q7, type: NPN, ports: {C: VCC, B: C, E: VEE}
name: Q8, type: NPN, ports: {C: C, B: VN, E: VEE}
name: Q9, type: NPN, ports: {C: VEE, B: C, E: VEE}
name: Q10, type: PNP, ports: {C: VEE, B: VN, E: C}
name: Q11, type: NPN, ports: {C: VCC, B: C, E: VO}
name: Q12, type: NPN, ports: {C: VO, B: C, E: VEE}
name: Q13, type: PNP, ports: {C: VO, B: C, E: VEE}
name: Q14, type: PNP, ports: {C: C, B: VO, E: VEE}
name: I3, type: CurrentSource, value: I3, ports: {Np: VCC, Nn: VP}
name: I4, type: CurrentSource, value: I4, ports: {Np: VP, Nn: VEE}
name: I13, type: CurrentSource, value: I13, ports: {Np: VCC, Nn: VO}
name: I14, type: CurrentSource, value: I14, ports: {Np: VO, Nn: VEE}
]
extrainfo:The circuit is a current-feedback amplifier with multiple NPN and PNP transistors forming a complex feedback loop. The circuit uses current sources I3, I4, I13, and I14 to control the biasing of the transistors. The amplifier operates between VCC and VEE, with the input at VP and the output at VO. The transistors are arranged to provide amplification and feedback, with Q1 to Q14 forming the core of the amplifier.

FIGURE 5.39 Current-feedback amplifier.
image_name:FIGURE 5.39 Current-feedback amplifier. (a)
description:
[
name: Q5, type: PNP, ports: {C: VCC, B: X1, E: X1}
name: Q7, type: PNP, ports: {C: VCC, B: X1, E: C}
name: Q10, type: NPN, ports: {C: X2, B: X2, E: VEE}
name: Q8, type: NPN, ports: {C: X2, B: C, E: VEE}
name: C, type: Capacitor, value: C, ports: {Np: C, Nn: VO}
name: Req, type: Resistor, value: Req, ports: {N1: C, N2: GND}
name: X1, type: OpAmp, ports: {InP: VP, InN: VN, OutP: X1}
name: X1, type: Buffer, ports: {In: C, Out: VO}
]
extrainfo:The circuit is a current-feedback amplifier with multiple NPN and PNP transistors forming a complex feedback loop. The circuit uses current sources I3, I4, I13, and I14 to control the biasing of the transistors. The amplifier operates between VCC and VEE, with the input at VP and the output at VO. The transistors are arranged to provide amplification and feedback, with Q1 to Q14 forming the core of the amplifier.

(a)
image_name:(a)
description:
[
name: V_I, type: VoltageSource, value: V_I, ports: {Np: V_I, Nn: GND}
name: R_1, type: Resistor, value: R_1, ports: {N1: V_N, N2: GND}
name: R_2, type: Resistor, value: R_2, ports: {N1: V_O, N2: V_N}
name: OpAmp, type: OpAmp, ports: {InP: V_P, InN: V_N, OutP: V_O}
name: Req, type: CurrentControlledVoltageSource, value: Req, ports: {N1: GND, N2: V_O}
]
extrainfo:The circuit is a current-feedback amplifier with a voltage gain given by the equation A = (1 + R2/R1) / (1 + R2/Req). It operates between VCC and VEE, with the input at V_I and the output at V_O. The amplifier utilizes a feedback loop for amplification and control.

(b)

FIGURE 5.40 (a) Simplified circuit equivalent of the CFA. (b) CFA symbol and interconnection for operation as a noninverting amplifier.

Letting $v_{N}=v_{P}=v_{I}$, solving for $i_{N}$, and inserting into Eq. (5.67) gives the closed-loop voltage gain

$$
\begin{equation*}
A=\frac{v_{O}}{v_{I}}=\left(1+\frac{R_{2}}{R_{1}}\right) \frac{1}{1+R_{2} / R_{e q}} \tag{5.68}
\end{equation*}
$$

In a well-designed circuit $R_{2}$ is on the order of $10^{3} \Omega$ whereas $R_{e q}$ is on the order of $10^{5} \sim 10^{6} \Omega$, so $R_{2} \ll R_{e q}$. Under this condition, $A$ tends to the expression already familiar from op amps,

$$
\begin{equation*}
A \cong 1+\frac{R_{2}}{R_{1}} \tag{5.69}
\end{equation*}
$$

The unique advantages of CFAs compared to ordinary op amps (also called voltagefeedback amplifiers or VFAs) are fast dynamics. These advantages, not immediately obvious from the present discussion but stemming from current-mode operation, will be addressed in Chapter 6.

### CFA-Derived Voltage-Feedback Amplifiers

Another important application of the transconductor of Fig. 5.38 is as a building block for high-speed voltage-feedback amplifiers (VFAs). The VFA of Fig. 5.41 is obtained from the CFA of Fig. 5.39 by using a third voltage buffer $\left(Q_{15}{ }^{-} Q_{16^{-}} Q_{17}{ }^{-} Q_{18}\right)$ to turn node $v_{N}$ into a high resistance input, and by inserting a resistance $R$ between the outputs of the first buffer and this new buffer to generate the control current previously denoted as $i_{N}$. This current (assumed to flow from left to right) is now
image_name:Figure 5.41 CFA-derived VFA
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: Q3-Q4, E: Q2-Q16}
name: Q2, type: NPN, ports: {C: Q1-Q15, B: Q3-Q4, E: Q10}
name: Q3, type: NPN, ports: {C: Q1-Q15, B: VP, E: Q2-Q16}
name: Q4, type: NPN, ports: {C: VP, B: VCC, E: Q3-Q4}
name: Q5, type: NPN, ports: {C: VCC, B: Q1-Q15, E: Q3-Q4}
name: Q6, type: NPN, ports: {C: VCC, B: Q7-Q14, E: Q13}
name: Q7, type: NPN, ports: {C: Q6-Q11, B: Q7-Q14, E: Q8}
name: Q8, type: NPN, ports: {C: Q7-Q14, B: Q9, E: Q12}
name: Q9, type: NPN, ports: {C: Q8, B: Q7-Q14, E: VEE}
name: Q10, type: NPN, ports: {C: Q2-Q16, B: Q3-Q4, E: VEE}
name: Q11, type: NPN, ports: {C: VCC, B: Q7-Q14, E: VO}
name: Q12, type: NPN, ports: {C: Q8, B: Q7-Q14, E: VO}
name: Q13, type: NPN, ports: {C: Q6-Q11, B: Q7-Q14, E: VO}
name: Q14, type: NPN, ports: {C: Q6-Q11, B: Q7-Q14, E: Q8}
name: Q15, type: NPN, ports: {C: Q1-Q15, B: Q16, E: R}
name: Q16, type: NPN, ports: {C: Q2-Q16, B: Q15, E: R}
name: Q17, type: NPN, ports: {C: Q18, B: Q15, E: VCC}
name: Q18, type: NPN, ports: {C: Q17, B: C, E: VN}
name: I3, type: CurrentSource, ports: {Np: VCC, Nn: Q5}
name: I4, type: CurrentSource, ports: {Np: VP, Nn: Q10}
name: I13, type: CurrentSource, ports: {Np: VCC, Nn: Q11}
name: I14, type: CurrentSource, ports: {Np: Q8, Nn: Q9}
name: I17, type: CurrentSource, ports: {Np: VCC, Nn: Q17}
name: I18, type: CurrentSource, ports: {Np: VCC, Nn: Q8}
name: R, type: Resistor, value: R, ports: {N1: Q15, N2: Q16}
]
extrainfo:The circuit is a CFA-derived VFA amplifier designed for high-speed voltage feedback applications. It includes multiple NPN transistors and current sources to achieve high open-loop voltage gain. The voltage gain is given by a = Req/R, where Req is the equivalent resistance at node C.

FIGURE 5.41 CFA-derived VFA.
$\left(v_{P}-v_{N}\right) / R$, and is conveyed to node $C$, where it produces the voltage $R_{e q}\left(v_{P}-v_{N}\right) / R$. This voltage is then buffered to the output node to give $v_{o}$, so the open-loop voltage gain of the resulting op amp is

$$
\begin{equation*}
a=\frac{v_{O}}{v_{P}-v_{N}}=\frac{R_{e q}}{R} \tag{5.70}
\end{equation*}
$$

Again, a well-designed circuit has $a \gg 1$. Owing to its inherently fast current-mode operation, this op amp type is especially suited to high-speed applications.

### Differential-Input Transconductors

The transconductor's versatility can be enhanced appreciably if we configure it to respond to differential-type inputs. In the popular rendition of Fig. 5.42, called operational transconductance amplifier (OTA), this feature is achieved by means of the differential pair $Q_{1}-Q_{2}$. To ensure high CMRR, the pair is biased via the high output-resistance Wilson mirror $Q_{3}-Q_{4}-Q_{5}$. $Q_{2}$ 's current is replicated and conveyed to the output node by the Wilson mirror $Q_{9}-Q_{10}{ }^{-} Q_{11} ; Q_{1}$ 's current is first replicated by the mirror $Q_{6}-Q_{7}-Q_{8}$, and then conveyed to the output node by the mirror $Q_{12^{2}}-Q_{13}-Q_{14}$, where it gets subtracted from that conveyed by $Q_{9}-Q_{10}{ }^{-} Q_{11}$. Ignoring the diodes $D_{1}$ and $D_{2}$ for the time being, we adapt Eq. (4.73) to write

$$
\begin{equation*}
i_{o}=i_{C 11}-i_{C 12}=i_{C 2}-i_{C 1}=I \times \tanh \left(\frac{v_{P}-v_{N}}{2 V_{T}}\right) \tag{5.71}
\end{equation*}
$$

image_name:FIGURE 5.42 Operational transconductance amplifier (OTA)
description:
[
name: Q1, type: NPN, ports: {C: Q3_B, B: vN, E: Q3_C}
name: Q2, type: NPN, ports: {C: Q3_B, B: vP, E: Q3_C}
name: Q3, type: PNP, ports: {C: Q4_C, B: Q1_C, E: Q5_C}
name: Q4, type: NPN, ports: {C: Q3_C, B: Q5_C, E: VEE}
name: Q5, type: NPN, ports: {C: Q3_E, B: Q4_C, E: VEE}
name: Q6, type: PNP, ports: {C: VCC, B: Q8_B, E: Q7_C}
name: Q7, type: PNP, ports: {C: Q6_E, B: Q8_B, E: Q8_C}
name: Q8, type: NPN, ports: {C: Q7_E, B: Q6_B, E: Q3_B}
name: Q9, type: PNP, ports: {C: VCC, B: Q11_B, E: Q10_C}
name: Q10, type: PNP, ports: {C: Q9_E, B: Q11_B, E: Q11_C}
name: Q11, type: NPN, ports: {C: Q10_E, B: Q9_B, E: io}
name: Q12, type: PNP, ports: {C: VCC, B: Q14_B, E: Q13_C}
name: Q13, type: NPN, ports: {C: Q12_E, B: Q14_B, E: VEE}
name: Q14, type: NPN, ports: {C: Q13_E, B: Q12_B, E: io}
name: D1, type: Diode, ports: {Na: vN, Nc: VA}
name: D2, type: Diode, ports: {Na: VA, Nc: vP}
]
extrainfo:This circuit is an Operational Transconductance Amplifier (OTA). It uses multiple NPN and PNP transistors to create a differential amplifier with current mirrors. The input differential pair is Q1 and Q2, and the output is taken at node io. The diodes D1 and D2 are connected between the input nodes vN and vP, and VA. The circuit is powered by VCC and VEE.

FIGURE 5.42 Operational transconductance amplifer (OTA).
where $I$ is the current supplied by the user to bias the $Q_{1}-Q_{2}$ pair. The plot of $i_{0}$ versus the difference $v_{P}-v_{N}$ is the familiar $s$-shaped curve of Fig. 4.44. This curve is nonlinear, but if we restrict the input voltage within the range $\left|v_{P}-v_{N}\right| \ll 4 V_{T}$ ( $\cong 100 \mathrm{mV}$ ), then the small-signal approximation allows us to retain only the first term in the series expansion $\tanh x=x-x^{3} / 3+\cdots$ and write

$$
\begin{equation*}
i_{o}=\frac{I}{2 V_{T}}\left(v_{p}-v_{n}\right) \tag{5.72}
\end{equation*}
$$

We make some important observations:

- In small-signal operation, the transconductance gain

$$
\begin{equation*}
G_{m}=\frac{i_{o}}{v_{p}-v_{n}}=\frac{I}{2 V_{T}} \tag{5.73}
\end{equation*}
$$

is linearly proportional to the bias current $I$, so it can be programmed externally by the user. In fact, BJTs easily allow for current ranges in excess of five decades ( $>100 \mathrm{~dB}$ ), making OTAs particularly suited to a variety of programmable circuits ${ }^{7,8}$ such as programmable amplifiers, programmable oscillators, and programmable filters, especially in wide-dynamic range applications like audio and electronic music.
image_name:(a)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: R1, type: Resistor, value: 10kΩ, ports: {N1: V1, N2: vB1}
name: R2, type: Resistor, value: 44Ω, ports: {N1: vB1, N2: GND}
name: Q1, type: NPN, ports: {C: VCC, B: vB1, E: P}
name: Q2, type: NPN, ports: {C: VCC, B: vB2, E: P}
name: R3, type: Resistor, value: 10kΩ, ports: {N1: vB2, N2: GND}
name: R4, type: Resistor, value: 44Ω, ports: {N1: vB2, N2: GND}
name: I, type: CurrentSource, value: 1mA, ports: {Np: P, Nn: GND}
name: VCC, type: VoltageSource, value: 15V, ports: {Np: VCC, Nn: GND}
name: VEE, type: VoltageSource, value: -15V, ports: {Np: GND, Nn: VEE}
]
extrainfo:The circuit is a differential pair with a current source bias. It uses NPN transistors Q1 and Q2, with resistors R1 and R2 setting the base voltage for Q1, and R3 and R4 setting the base voltage for Q2. The circuit is powered by VCC and VEE, providing a total voltage swing of 30V. The input is a differential signal applied across vB1 and vB2. The output is taken from the emitter node P.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: VB1, E: P}
name: Q2, type: NPN, ports: {C: VCC, B: VB2, E: P}
name: R1, type: Resistor, value: 10kΩ, ports: {N1: VI, N2: VB1}
name: R2, type: Resistor, value: 0.5kΩ, ports: {N1: VB1, N2: GND}
name: R3, type: Resistor, value: 10kΩ, ports: {N1: VB2, N2: GND}
name: R4, type: Resistor, value: 0.5kΩ, ports: {N1: VB2, N2: GND}
name: I, type: CurrentSource, value: 1mA, ports: {Np: P, Nn: VEE}
name: VCC, type: VoltageSource, value: 15V, ports: {Np: VCC, Nn: GND}
name: VEE, type: VoltageSource, value: -15V, ports: {Np: VEE, Nn: GND}
name: D1, type: NPN, ports: {C: A, B: VB1, E: P}
name: D2, type: NPN, ports: {C: A, B: VB2, E: P}
name: RA, type: Resistor, value: 13kΩ, ports: {N1: VCC, N2: A}
]
extrainfo:The circuit in diagram (b) is a differential amplifier with a predistorting input diode network. It is designed to handle a ±10V triangular input signal. The diodes D1 and D2 are used for predistortion to improve linearity.

FIGURE 5.43 PSpice circuits to investigate distortion in a differential pair configured for a $\pm 10-\mathrm{V}$ triangular input: (a) without and (b) with the predistorting input diode network.

- The small-signal constraint may be a drawback in certain applications. The effect of exceeding this constraint is depicted via the PSpice circuit of Fig. 5.43a, which uses input voltage dividers to scale a $\pm 10-\mathrm{V}$ triangular signal to an input difference $v_{B 1}-v_{B 2}$ of about $\pm 44-\mathrm{mV}$. Since 44 mV is not much smaller than $4 V_{T}(\cong 100 \mathrm{mV})$, the resulting current difference $i_{C 1}-i_{C 2}$ is a noticeably distorted triangle. (The shaded waveforms of Fig. 5.44 show the undistorted input voltage as well as the distorted output current.)
- If we wish an undistorted current waveform, the input voltage must be predistorted according to the inverse of the hyperbolic tangent function. An approximation to this function is achieved by means of the diode-connected BJT pair $D_{1}-D_{2}$ of Fig. 5.43b. Its effect, depicted in Fig. 5.44 via the solid traces, is
image_name:(a)
description:The graph labeled "(a)" in Figure 5.44 is a time-domain waveform comparing two different voltage waveforms over a period of 2 milliseconds. The x-axis represents time in milliseconds (ms), ranging from 0 to 2 ms, while the y-axis represents the voltage difference $v_{B1} - v_{B2}$ in millivolts (mV), ranging from -50 mV to 50 mV.

The graph displays two waveforms: a shaded trace and a solid trace. The shaded trace represents the undistorted input voltage, while the solid trace represents the predistorted voltage after processing by a diode-connected BJT pair to achieve an undistorted current waveform.

Both waveforms exhibit a triangular shape, indicating periodic linear increases and decreases in voltage. The peaks of the waveforms occur at approximately 0.5 ms, 1.0 ms, and 1.5 ms, with the voltage reaching around +50 mV and -50 mV at these points.

The solid trace is slightly stretched compared to the shaded trace, particularly noticeable at the peaks, where the voltage values extend to about ±60 mV. This stretching aligns with the described function of the diode-connected BJT pair, which modifies the input peaks to achieve the desired undistorted current waveform.

Overall, the graph illustrates the effect of predistortion on the voltage waveform to compensate for distortions in the output current, as intended by the circuit design in Figure 5.43b.
image_name:(b)
description:The graph labeled "(b)" is a time-domain waveform plot depicting the difference in current ($i_{C1} - i_{C2}$) over time. The x-axis represents time in milliseconds (ms) ranging from 0 to 2 ms, while the y-axis represents the current difference in milliamperes (mA) with a range from -1 to 1 mA.

The waveform is a distorted triangular shape, characterized by linear segments with sharp peaks and valleys. The general trend shows periodic oscillations, with peaks occurring approximately at 0.5 ms and 1.5 ms and valleys at 1.0 ms and 2.0 ms, indicating a repeating cycle every 1 ms.

There are two traces on the graph: a shaded trace and a solid trace. The shaded trace represents the distorted output current waveform from the circuit in Fig. 5.43a, while the solid trace shows the waveform after predistortion applied by the diode-connected BJT pair in Fig. 5.43b. The solid trace is less distorted, indicating the effectiveness of the predistortion in achieving a more linear current waveform.

Key features of the waveform include:
- Periodicity with a period of 1 ms.
- Peaks at approximately ±1 mA, occurring at 0.5 ms and 1.5 ms.
- Valleys at approximately 0 mA, occurring at 1.0 ms and 2.0 ms.

The graph effectively illustrates the improvement in waveform linearity through the predistortion technique, as seen by the solid trace compared to the shaded trace.

FIGURE 5.44 Waveforms for the PSpice circuits of Fig. 5.43 (the shaded traces pertain to the circuit of Fig. 5.43a, the solid traces to that of Fig. 5.43b.)
to stretch in approximately inverse hyperbolic-tangent fashion the input peaks from about $\pm 44 \mathrm{mV}$ to about $\pm 60 \mathrm{mV}$, the values required for an undistorted current waveform.

### Variable Transconductance Multipliers

The OTA of Fig. 5.42 is said to be an analog multiplier because, according to Eq. (5.72), $i_{o}$ is proportional to the product $I \times\left(v_{p}-v_{n}\right)$. While the difference $v_{p}-v_{n}$ can assume either polarity, the current $I$ must always flow out of the differential pair $(I \geq 0)$, so the OTA is said to be a two-quadrant multiplier. Applications such as communications require full four-quadrant analog multiplication. This function is implemented using the current-mode circuit of Fig. 5.45. Popularly known as the Gilbert Cell for its inventor Barrie Gilbert, ${ }^{8}$ this most elegant current-mode circuit consists of (a) two emitter-coupled (EC) differential pairs $Q_{1}-Q_{2}$ and $Q_{3}{ }^{-} Q_{4}$ driven by the same voltage $v_{X}$ but in phase opposition to each other, so their output currents subtract pair-wise, and $(b)$ a third EC pair $\left(Q_{5}-Q_{6}\right)$ designed to steer the bias current $I$ to the two differential pairs in ratios controlled by the voltage $v_{Y}$. Depending on the polarity of $v_{Y}$, the output of one pair will prevail over that of the other, allowing the output current difference $i_{O 1}-i_{O 2}$ to attain either polarity and thus provide four-quadrant operation.

To obtain a relationship between the output currents and the input voltages we use KCL to write

$$
i_{O 1}-i_{O 2}=\left(i_{C 1}+i_{C 3}\right)-\left(i_{C 2}+i_{C 4}\right)=\left(i_{C 1}-i_{C 2}\right)-\left(i_{C 4}-i_{C 3}\right)
$$

image_name:Figure 5.45 The Gilbert Cell
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: X1, E: VX-}
name: Q2, type: NPN, ports: {C: X1, B: VX-, E: VY+}
name: Q3, type: NPN, ports: {C: VK-, B: X2, E: VY+}
name: Q4, type: NPN, ports: {C: VCC, B: VK+, E: X2}
name: Q5, type: NPN, ports: {C: VY+, B: VY-, E: P}
name: Q6, type: NPN, ports: {C: VY+, B: VY-, E: P}
name: I, type: CurrentSource, value: I, ports: {Np: P, Nn: VEE}
]
extrainfo:The circuit is a Gilbert Cell, which is a type of four-quadrant multiplier. It utilizes differential pairs of NPN transistors to achieve multiplication of input signals. The output current difference is controlled by the voltage inputs VX and VY.

FIGURE 5.45 The Gilbert Cell.

Assuming negligible base currents, we adapt Eq. (5.71) and write

$$
i_{O 1}-i_{O 2}=i_{C 5} \tanh \left(\frac{v_{X}}{2 V_{T}}\right)-i_{C 6} \tanh \left(\frac{v_{X}}{2 V_{T}}\right)=\left(i_{C 5}-i_{C 6}\right) \tanh \left(\frac{V_{X}}{2 V_{T}}\right)
$$

that is,

$$
\begin{equation*}
i_{O 1}-i_{O 2}=I \tanh \left(\frac{V_{Y}}{2 V_{T}}\right) \tanh \left(\frac{V_{X}}{2 V_{T}}\right) \tag{5.74}
\end{equation*}
$$

We identify three classes of applications for the cell:

- Both inputs are of the small-signal type, that is, $\left|v_{x}\right| \ll 4 V_{T}$ and $\left|v_{y}\right| \ll 4 V_{T}$, so we approximate $\tanh x \cong x$ and write

$$
\begin{equation*}
i_{o 1}-i_{o 2} \cong I \times \frac{v_{x}}{2 V_{T}} \times \frac{v_{y}}{2 V_{T}} \tag{5.75}
\end{equation*}
$$

Clearly, in this mode the cell operates as a true four-quadrant multiplier.

- One of the inputs $\left(v_{x}\right)$ is a small-signal continuous wave such as a sine wave, while the other input $\left(v_{Y}\right)$ is a square wave of sufficient magnitude to overdrive the $Q_{5}-Q_{6}$ pair so as to turn one of its BJTs off. Then, for $v_{Y}>0, Q_{6}$ is off and $Q_{5}$ steers all of $I$ to the $Q_{1}-Q_{2}$ pair to give $i_{o 1}-i_{o 2}=+I v_{x} /\left(2 V_{T}\right)=+g_{m} v_{x}$. Conversely, for $v_{Y}<0, Q_{5}$ is off and $Q_{6}$ steers all of $I$ to the $Q_{3}-Q_{4}$ pair to give $i_{o 1}-i_{o 2}=-I v_{x} /\left(2 V_{T}\right)=-g_{m} v_{x}$, the negative sign stemming from the anti-phase connection at the input. In this capacity the cell finds application in communications as modulator/detector.
- Both inputs are of the large-signal type. Then, when $v_{X}$ and $v_{Y}$ have the same polarity the cell gives $i_{O 1}-i_{O 2}=I-0=I$, whereas when $v_{X}$ and $v_{Y}$ have opposite polarities it gives $i_{O 1}-i_{O 2}=0-I=-I$. This function is similar to the exclusive-or function of digital circuits. In this capacity the cell finds application as phase detector in phase-locked loop systems.

As in the case of OTAs, the small-signal constraint can be a serious limitation in certain multiplier applications, so provisions must be made to accommodate larger input magnitudes while still assuring accurate multiplication. Shown in Fig. 5.46 is a popular Gilbert Cell application meeting the above requirements. We make the following observations:

- The $Q_{5}-Q_{6}$ pair exploits emitter degeneration via $R_{Y}$ to expand its input signal range by the desired amount. Again ignoring base currents, we apply KCL, Ohm's law, and KVL to write

$$
\begin{aligned}
i_{C 5}-i_{C 6} & =\left(I_{Y}+\frac{v_{E 5}-v_{E 6}}{R_{Y}}\right)-\left(I_{Y}+\frac{v_{E 6}-v_{E 5}}{R_{Y}}\right)=2 \frac{v_{E 5}-v_{E 6}}{R_{Y}} \\
& =\frac{\left(v_{Y 1}-v_{B E 5}\right)-\left(v_{Y 2}-v_{B E 6}\right)}{0.5 R_{Y}}
\end{aligned}
$$

Regrouping and using $v_{B E}=V_{T} \ln \left(i_{C} / I_{s}\right)$ we get

$$
i_{C 5}-i_{C 6}=\frac{\left(v_{Y 1}-v_{Y 2}\right)-\left(v_{B E 5}-v_{B E 6}\right)}{0.5 R_{Y}}=\frac{\left(v_{Y 1}-v_{Y 2}\right)-V_{T} \ln \left(i_{C 5} / i_{C 6}\right)}{0.5 R_{Y}}
$$

image_name:Figure 5.46 Four-quadrant analog multiplier
description:
[
name: Q1, type: NPN, ports: {C: vO1, B: vX-, E: X1}
name: Q2, type: NPN, ports: {C: vO1, B: vX-, E: X1}
name: Q3, type: NPN, ports: {C: vO2, B: vX+, E: X2}
name: Q4, type: NPN, ports: {C: vO2, B: vX+, E: X2}
name: Q5, type: NPN, ports: {C: vX+, B: vY1, E: P3}
name: Q6, type: NPN, ports: {C: vX+, B: vY2, E: P4}
name: Q7, type: NPN, ports: {C: vX-, B: vX1, E: P1}
name: Q8, type: NPN, ports: {C: vX-, B: vX2, E: P2}
name: Q9, type: NPN, ports: {C: VA, B: vX-, E: VK-}
name: Q10, type: NPN, ports: {C: VA, B: vX+, E: VK-}
name: R, type: Resistor, value: R, ports: {N1: VCC, N2: vO1}
name: R, type: Resistor, value: R, ports: {N1: VCC, N2: vO2}
name: RX, type: Resistor, value: RX, ports: {N1: P1, N2: P2}
name: RY, type: Resistor, value: RY, ports: {N1: P3, N2: P4}
name: IX, type: CurrentSource, value: IX, ports: {Np: P1, Nn: VEE}
name: IY, type: CurrentSource, value: IY, ports: {Np: P3, Nn: VEE}
]
extrainfo:The circuit is a four-quadrant analog multiplier. It uses pairs of NPN transistors to perform voltage-to-current conversions. The Q5-Q6 pair and Q7-Q8 pair are used for this purpose with emitter degeneration resistors RY and RX, respectively. The output currents iO1 and iO2 are derived from the voltage differences across these pairs.

FIGURE 5.46 Four-quadrant analog multiplier.

In a well-designed circuit the last numerator term is negligible (see Problem 5.39), so we approximate

$$
\begin{equation*}
i_{C 5}-i_{C 6}=\frac{v_{Y 1}-v_{Y 2}}{0.5 R_{Y}} \tag{5.76}
\end{equation*}
$$

indicating that the emitter-degenerated $Q_{5}-Q_{6}$ pair acts as a linear voltage-to-current (V-I) converter.

- Likewise, the $Q_{7}-Q_{8}$ pair is a V-I converter giving $i_{C 7}-i_{C 8}=\left(v_{X 1}-v_{X 2}\right) /\left(0.5 R_{X}\right)$ and driving the diode-connected pair $Q_{9}{ }^{-} Q_{10}$. Using KVL and $v_{B E}=V_{T} \ln \left(i_{C} / I_{s}\right)$ we have

$$
\begin{aligned}
v_{X} & =v_{E 10}-v_{E 9}=\left(V_{A}-v_{B E 10}\right)-\left(V_{A}-v_{B E 9}\right)=v_{B E 9}-v_{B E 10} \\
& =V_{T} \ln \frac{i_{C 9}}{i_{C 10}}=V_{T} \ln \frac{i_{C 7}}{i_{C 8}}
\end{aligned}
$$

But, KCL gives $i_{C 7}=I_{X}+\left(v_{X 1}-v_{X 2}\right) / R_{X}$ and $i_{C 8}=I_{X}-\left(v_{X 1}-v_{X 2}\right) / R_{X}$, so

$$
v_{X}=V_{T} \ln \frac{I_{X}+\left(v_{X 1}-v_{X 2}\right) / R_{X}}{I_{X}-\left(v_{X 1}-v_{X 2}\right) / R_{X}}=V_{T} \ln \frac{1+\left(v_{X 1}-v_{X 2}\right) /\left(R_{X} I_{X}\right)}{1-\left(v_{X 1}-v_{X 2}\right) /\left(R_{X} I_{X}\right)}
$$

Using the identity $\ln [(1+x) /(1-x)]=2 \tan ^{-1} x$, which holds for $|x|<1$, we have

$$
\begin{equation*}
v_{X}=2 V_{T} \tan ^{-1} \frac{v_{X 1}-v_{X 2}}{R_{X} I_{X}} \tag{5.77}
\end{equation*}
$$

- Substituting Eqs. (5.76) and (5.77) into Eq. (5.74) we get

$$
i_{O 1}-i_{O 2}=\left(i_{C 5}-i_{C 6}\right) \tanh \frac{v_{X}}{2 V_{T}}=\frac{v_{Y 1}-v_{Y 2}}{0.5 R_{Y}} \tanh \frac{2 V_{T} \tan ^{-1}\left[\left(v_{X 1}-v_{X 2}\right) /\left(R_{X} I_{X}\right)\right]}{2 V_{T}}
$$

that is,

$$
\begin{equation*}
i_{O 1}-i_{O 2}=\frac{v_{Y 1}-v_{Y 2}}{0.5 R_{Y}} \times \frac{v_{X 1}-v_{X 2}}{R_{X} I_{X}} \tag{5.78}
\end{equation*}
$$

It is apparent that the tanh function and its inverse $\tanh ^{-1}$ cancel each other out to leave only the argument $\left(v_{X 1}-v_{X 2}\right) /\left(2 R_{X}\right)$. In words, the $X$-input is first processed by the $Q_{9}-Q_{10}$ diodes in $\tanh ^{-1}$ fashion to generate a predistorted signal $v_{x}$; the $Q_{1}-Q_{2}$ and $Q_{3}{ }^{-} Q_{2}$ pairs then process $v_{X}$ in tanh fashion to generate an overall undistorted output. The output is, in turn, modulated by the $Y$-input.

- In actual application the output current difference $i_{O 1}-i_{O 2}$ is converted to a voltage. In the rendition of Fig. 5.46 this I-V conversion is achieved by terminating the cell's outputs on a pair of matched resistances $R$ to give the double-ended output voltage

$$
\begin{equation*}
v_{O}=v_{O 2}-v_{O 1}=R\left(i_{O 1}-i_{O 2}\right)=\frac{R}{0.5 R_{X} R_{Y} I_{X}} \times\left(v_{X 1}-v_{X 2}\right) \times\left(v_{Y 1}-v_{Y 2}\right) \tag{5.79}
\end{equation*}
$$

If a single-ended voltage-type output is desired, then the I-V conversion can be implemented via an op amp configured as a differential amplifier. ${ }^{7}$ Alternatively, if a single-ended current output is desired, then we can use three Wilson current mirrors in the manner of the OTA of Fig. 5.42.

## 5.7 FULLY DIFFERENTIAL OPERATIONAL AMPLIFIERS

A common way of encoding analog information electronically is via single-ended voltages such as ground-referenced potentials. A classic example is the inverting amplifier of Fig. 5.47a, whose input $v_{I}$ and output $v_{O}$ are both referenced to ground potential. For large $a$, they are related as $v_{O}=\left(-R_{2} / R_{1}\right) v_{I}$. In actual application the circuit is likely to be part of a larger system, where it may be subject to various
image_name:(a)
description:
[
name: VI, type: VoltageSource, value: VI, ports: {Np: vI, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: VI, N2: vN}
name: R2, type: Resistor, value: R2, ports: {N1: vN, N2: vO}
name: a, type: OpAmp, value: a, ports: {InP: vP, InN: vN, Out: vO}
]
extrainfo:The circuit diagram (a) is a classic inverting amplifier configuration using an operational amplifier. The input voltage source VI is connected to the inverting input of the op-amp through resistor R1. Resistor R2 provides feedback from the output to the inverting input. The non-inverting input is grounded. The op-amp amplifies the voltage difference between its inputs, providing an output voltage vO that is inverted and scaled by the ratio of R2 to R1.
image_name:(b)
description:
[
name: V_I, type: VoltageSource, ports: {Np: v_I, Nn: GND}
name: R_1, type: Resistor, value: R_1, ports: {N1: v_I, N2: v_N}
name: R_2, type: Resistor, value: R_2, ports: {N1: v_N, N2: v_O}
name: a, type: OpAmp, value: a, ports: {InP: v_P, InN: v_N, OutP: v_O, OutN: GND}
]
extrainfo:The circuit is an inverting amplifier with interference noise model and stray elements included. It uses a voltage source V_I and resistors R_1 and R_2, with an operational amplifier labeled 'a'. The input voltage v_I is connected to the inverting input of the op-amp through R_1, and the feedback is provided by R_2.

FIGURE 5.47 Basic op amp circuit: (a) idealized situation, and (b) in actual application, showing the stray elements of its interconnections.
image_name:(a)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: X1, Nn: GND}
name: V2, type: VoltageSource, value: V2, ports: {Np: X2, Nn: X1}
name: R1, type: Resistor, value: R1, ports: {N1: VN, N2: X2}
name: R2, type: Resistor, value: R2, ports: {N1: VO, N2: VN}
name: A, type: OpAmp, value: A, ports: {InP: VP, InN: VN, OutP: VO, OutN: GND}
]
extrainfo:The circuit is an inverting amplifier with interference noise model and stray elements included. It uses a voltage source V_I and resistors R_1 and R_2, with an operational amplifier labeled 'a'. The input voltage v_I is connected to the inverting input of the op-amp through R_1, and the feedback is provided by R_2.
image_name:(b)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: X1, Nn: V1}
name: V2, type: VoltageSource, value: V2, ports: {Np: X2, Nn: X3}
name: R1, type: Resistor, value: R1, ports: {N1: X2, N2: VN}
name: R1, type: Resistor, value: R1, ports: {N1: X3, N2: VP}
name: R2, type: Resistor, value: R2, ports: {N1: VN, N2: VO}
name: R2, type: Resistor, value: R2, ports: {N1: VP, N2: GND}
name: A, type: OpAmp, value: A, ports: {InP: VP, InN: VN, OutP: VO, OutN: GND}
]
extrainfo:The circuit is an inverting amplifier with interference noise model and stray elements included. It uses a voltage source V_I and resistors R_1 and R_2, with an operational amplifier labeled 'a'. The input voltage v_I is connected to the inverting input of the op-amp through R_1, and the feedback is provided by R_2.

FIGURE 5.48 (a) Interference noise model for the inverting amplifier of Fig. 5.47. (b) Interconnecting the op amp as a difference amplifier to reject $v_{1}$, and using balanced input lines to cancel out the $v_{2}$ noise sources.
forms of interference noise that might obfuscate its useful signals. To begin with, the ground interconnection, far from being a perfect conductor, exhibits distributed resistance, inductance, and capacitance, and is shared with other subcircuits in the system. As the currents of the other circuits flow back and forth on the ground line, as illustrated via the lumped model of Fig. 5.47b, they produce undesirable voltage drops along the distributed line impedance. Also shown are stray mutual inductances and stray internode capacitances, which provide additional paths through which the surrounding circuits can inject interference noise into the line. We model the cumulative effect of all noise sources with a single ground noise source $v_{1}$ as in Fig. 5.48a. Interference noise pickup from neighboring circuits affects also the signal line connecting the source to the amplifier, so we model this via the line noise source $v_{2}$.

Given the noise drops along the ground line, the very concept of reference node becomes blurred. For the sake of discussion let us arbitrarily pick node $v_{P}$ as our ground reference, as depicted in Fig. 5.48a. Then, using KVL we find $v_{O}=\left(-R_{2} / R_{1}\right) \times\left(v_{1}+v_{I}+v_{2}\right)$, indicating that both noise sources get amplified by the same amount as the useful signal $v_{I}$. This is unacceptable especially in high-gain applications, where the input signal strength may be comparable to that of noise. The best way to dispose of ground noise is to treat $v_{1}$ as a commonmode signal and use a differential amplifier with a high common-mode rejection ratio (CMRR) to reject it. As depicted in Fig. 5.48b, this requires lifting node $v_{P}$ off ground and driving it by means of an additional dedicated line as well as an additional $R_{1}-R_{2}$ pair, as shown. This second line will of course pick up noise just like the preexisting line, but if the two lines are identical and are laid out in close proximity to each other so as to form what is aptly referred to as balanced lines, then noise pickup will be identical on the two lines and the circuit will give $^{7} v_{O}=\left(R_{2} / R_{1}\right)\left[\left(v_{1}+v_{2}\right)-\left(v_{1}+v_{I}+v_{2}\right)\right]=\left(-R_{2} / R_{1}\right) v_{I}$. Summarizing, $v_{1}$ is rejected thanks to the amplifier's CMRR, and the $v_{2}$ sources simply cancel each other out thanks to line balance.

### Fully Differential Amplifier Concepts

The classic differential amplifier of Fig. $5.48 b$ processes the input differentially but still yields a single-ended output. In today's mixed-mode ICs, where analog circuits are fabricated alongside inherently noisy digital circuits and are powered at low supply voltages, the combination of low signal amplitudes and high interference noise makes double-ended signal transmission mandatory both at the input and at the output ports. The workhorse of this class of circuits is the fully differential op amp shown symbolically in Fig. 5.49a. Also called fully balanced op amp, it responds to a differential input just like an ordinary op amp, to give $v_{O P}=a\left(v_{P}-v_{N}\right)$. However, unlike the common op amp, it has also a second, balanced output, $v_{O N}=a\left(v_{N}-v_{P}\right)=$ $-v_{O P}$, Additionally, it comes with a control input for the user to specify the commonmode output voltage $V_{O C(\mathrm{set})}$, as we shall see shortly.

Beside the noise-immunity advantages of balanced transmission, the fully differential op amp offers also (a) wider output signal swing and (b) reduced second-harmonic distortion. To see how, rewrite the outputs in more general forms accounting for inherent circuit nonlinearities, namely, $v_{O P}=a\left(v_{P}-v_{N}\right)+b\left(v_{P}-v_{N}\right)^{2}+c\left(v_{P}-v_{N}\right)^{3} \ldots$ and $v_{O N}=a\left(v_{N}-v_{P}\right)+b\left(v_{N}-v_{P}\right)^{2}+c\left(v_{N}-v_{P}\right)^{3} \ldots$ Then, the differential output reduces, after simplification, to $v_{O P}-v_{O N}=2 a\left(v_{P}-v_{N}\right)+2 c\left(v_{P}-v_{N}\right)^{3} \ldots$, indicating a differential output signal swing twice as large as that of the individual single-ended outputs, as well as a cancellation of the second-harmonic components.

The fully differential op amp is configured for negative-feedback operation with two identical networks as depicted in Fig. 5.49b for the resistive case. (Both networks are of the negative-feedback type as each connects from one of the outputs to the input of the opposite polarity.) For the purpose of illustration, the external inputs $v_{I P}$ and $v_{I N}$ have been decomposed in terms of their differential-mode and commonmode components

$$
\begin{equation*}
v_{I D}=v_{I P}-v_{I N} \quad v_{I C}=\frac{v_{I P}+v_{I N}}{2} \tag{5.80a}
\end{equation*}
$$

image_name:(a)
description:
[
name: VIC, type: VoltageSource, value: VIC, ports: {Np: VIC, Nn: GND}
name: VID/2, type: VoltageSource, value: VID/2, ports: {Np: VIN, Nn: VIC}
name: VID/2, type: VoltageSource, value: VID/2, ports: {Np: VIP, Nn: VIC}
name: VOC(set), type: VoltageSource, value: VOC(set), ports: {Np: VOC, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: VIN, N2: VN}
name: R1, type: Resistor, value: R1, ports: {N1: VIP, N2: VP}
name: R2, type: Resistor, value: R2, ports: {N1: VN, N2: VON}
name: R2, type: Resistor, value: R2, ports: {N1: VP, N2: VOP}
name: OpAmp1, type: OpAmp, value: a, ports: {InP: VP, InN: VN, OutP: VOP, OutN: VON}
name: OpAmp2, type: OpAmp, value: a, ports: {InP: VN, InN: VP, OutP: VON, OutN: VOP}
]
extrainfo:The circuit is a fully differential operational amplifier configuration. It uses two identical negative-feedback networks. The input differential voltage is split into two components, VIN and VIP, and the output differential voltage is represented by VOP and VON. The resistors R1 and R2 set the gain of the amplifier. The circuit also includes common-mode voltage sources VIC and VOC(set) for biasing.
image_name:(b)
description:
[
name: VIC, type: VoltageSource, value: VIC, ports: {Np: VIC, Nn: GND}
name: VID/2, type: VoltageSource, value: VID/2, ports: {Np: VIN, Nn: VIC}
name: VID/2, type: VoltageSource, value: VID/2, ports: {Np: VIP, Nn: VIC}
name: R1, type: Resistor, value: R1, ports: {N1: VIN, N2: VN}
name: R1, type: Resistor, value: R1, ports: {N1: VIP, N2: VP}
name: R2, type: Resistor, value: R2, ports: {N1: VN, N2: VOP}
name: R2, type: Resistor, value: R2, ports: {N1: VP, N2: VON}
name: OpAmp, type: OpAmp, ports: {InP: VP, InN: VN, OutP: VOP, OutN: VON}
name: VOC(set), type: VoltageSource, value: VOC(set), ports: {Np: VOC, Nn: GND}
]
extrainfo:The circuit is a fully differential op-amp configuration used for balanced amplifier operation. It employs negative feedback through R1 and R2 resistors to control gain, and uses voltage sources to set common-mode and differential-mode components.

FIGURE 5.49 Fully differential op amp: (a) symbol and labels, and (b) interconnection for operation as a fully balanced amplifier.

Likewise, the differential-mode and common-mode components at the output are

$$
\begin{equation*}
v_{O D}=v_{O P}-v_{O N} \quad v_{O C}=\frac{v_{O P}+v_{O N}}{2} \tag{5.80b}
\end{equation*}
$$

If the open-loop gain $a$ is sufficiently large, the differential-mode components are related as

$$
\begin{equation*}
v_{O D}=\frac{R_{2}}{R_{1}} v_{I D} \tag{5.81}
\end{equation*}
$$

(Note that since the single-ended output signals have opposite phases, as shown, the differential output swing $v_{O D}$ is twice as wide.) We also observe that whereas $v_{I C}$ is established by the input sources, $v_{O C}$ is unspecified and as such it needs to be set externally by the user.

### Fully Differential Bipolar Op Amp

Figure 5.50 shows how the folded-cascode bipolar structure of Fig. $4.71 a$ can be turned into a fully differential op amp. The first important change is in $Q_{5}$, formerly diode connected but now operated as a current-sink active load, just like $Q_{6}$. This
image_name:Figure 5.50
description:
[
name: Q1, type: NPN, ports: {C: X1, B: vP, E: P}
name: Q2, type: NPN, ports: {C: X2, B: vN, E: P}
name: Q3, type: PMOS, ports: {S: VCC, D: X1, G: VB34}
name: Q4, type: PMOS, ports: {S: VCC, D: X2, G: VB34}
name: Q5, type: NPN, ports: {C: X4, B: vEA, E: VEE}
name: Q6, type: NPN, ports: {C: X3, B: vEA, E: VEE}
name: Q7, type: PMOS, ports: {S: VCC, D: X3, G: VB78}
name: Q8, type: PMOS, ports: {S: VCC, D: X4, G: VB78}
name: I, type: CurrentSource, value: I, ports: {Np: P, Nn: VEE}
name: R, type: Resistor, value: R, ports: {N1: vOP, N2: vON}
name: ×1, type: Buffer, ports: {In: X1, Out: vOP}
name: ×1, type: Buffer, ports: {In: X2, Out: vON}
name: EA, type: OpAmp, ports: {InP: vOP, InN: vON, Out: VOC(set)}
]
extrainfo:This circuit is a fully differential bipolar operational amplifier with a folded-cascode structure. It includes current mirrors and differential pairs to achieve high gain and common-mode rejection. The circuit utilizes PMOS and NPN transistors for amplification and buffering, with biasing provided by VB78 and VB34.

FIGURE 5.50 Simplified fully differential bipolar op amp.
results in a perfectly symmetric structure. (To avoid cluttering, the details of the biasing network have been omitted, so only the base-bias voltages $V_{B 78}$ and $V_{B 34}$ are shown (also, in actual implementation, $Q_{5}$ and $Q_{6}$ are likely to be cascoded to raise the gain, but here we are focusing only on the basics.) The high-resistance collector nodes of the $Q_{3}-Q_{5}$ and $Q_{4}-Q_{6}$ pairs are buffered via unity-gain push-pull stages to give $v_{O P}$ and $v_{O N}$. The other important feature is the matched $R-R$ pair and the error amplifier EA, forming what is referred to as the common-mode feedback network (CMFN). Its function is to properly center $v_{O P}$ and $v_{O N}$ up or down the permissible output voltage range (OVR), usually halfway in order to maximize the output voltage swing. Specifically, the resistance pair synthesizes the voltage $\left(v_{O P}+v_{O N}\right) / 2$, which the EA then compares against the externally supplied voltage $V_{O C(s e t)}$, and adjusts its output $v_{E A}$ to force $\left(v_{O P}+v_{O N}\right) / 2$ to approach $V_{O C(\text { set })}$. To see how, recall that $v_{O P}$ and $v_{O N}$ are the voltages at which the pull-up actions by $Q_{3}$ and $Q_{4}$ balance, respectively, the pull-down actions by $Q_{5}$ and $Q_{6}$. So, raising/lowering $v_{E A}$ makes pull-down stronger/ weaker than pull-up, shifting $v_{O P}$ and $v_{O N}$ down/up the OVR. In control-theory parlance, the negative-feedback loop comprising the $R-R$ pair, the $E A$, the $Q_{5}-Q_{6}$ pair, and the buffers is said to form a servo loop.

### Fully Differential CMOS Op Amps

Figure 5.51 shows how the folded-cascode CMOS op amp of Fig. 5.17 can be turned into a fully differential type (again, the details of the biasing network have been omitted, so only the gate-bias voltages $V_{G 78}$ and $V_{G 56}$ are shown). To ensure balanced outputs, $M_{5}$ and $M_{7}$, formerly diode connected, are now operated as current sources.
image_name:Figure 5.51
description:
[
name: M1, type: NMOS, ports: {S: VSS, D: vN, G: vP}
name: M2, type: NMOS, ports: {S: VSS, D: vON, G: vN}
name: M3, type: NMOS, ports: {S: VSS, D: vOP, G: vON}
name: M4, type: NMOS, ports: {S: VSS, D: vOP, G: VG34}
name: M5, type: PMOS, ports: {S: VDD, D: vON, G: VG56}
name: M6, type: PMOS, ports: {S: VDD, D: vOP, G: VG56}
name: M7, type: PMOS, ports: {S: VDD, D: vON, G: VG78}
name: M8, type: PMOS, ports: {S: VDD, D: vOP, G: VG78}
name: M9, type: NMOS, ports: {S: VSS, D: VSS, G: vN}
name: M10, type: NMOS, ports: {S: VSS, D: VSS, G: vON}
name: M11, type: NMOS, ports: {S: VSS, D: vP, G: VG11}
name: M12, type: PMOS, ports: {S: VDD, D: vOP, G: VOC(set)}
name: M13, type: PMOS, ports: {S: VDD, D: vOP, G: VOC(set)}
name: M14, type: PMOS, ports: {S: VDD, D: vON, G: VOC(set)}
name: M15, type: PMOS, ports: {S: VDD, D: vON, G: VOC(set)}
name: M16, type: NMOS, ports: {S: VSS, D: vOP, G: vOP}
name: I1, type: CurrentSource, ports: {Np: VDD, Nn: vOP}
name: I2, type: CurrentSource, ports: {Np: VDD, Nn: vON}
]
extrainfo:The circuit is a fully differential CMOS operational amplifier of the folded-cascode type. The CMFN network is composed of transistors M12 through M16, ensuring balanced outputs. The biasing network details are omitted, with only gate-bias voltages VG78 and VG56 shown. Transistors M5 and M7 operate as current sources instead of diode-connected, contributing to balanced output.

FIGURE 5.51 Fully-differential CMOS op amp of the folded-cascode type.

Moreover, the CMFN is the all-transistor network made up of $M_{12}$ through $M_{16}$. To see how it functions, consider the following:

- Start out assuming $v_{P}=v_{N}$, so $v_{O P}=v_{O N}$. Also, assume $v_{O P}=v_{O N}=V_{O C(\mathrm{set})}$, so the two $I$ sources split equally between the SC pairs to give $I_{D 12}=I_{D 13}=0.5 I$ and $I_{D 14}=I_{D 15}=0.5 I$. The diode-connected FET $M_{16}$ draws $I_{D 16}=I_{D 13}+I_{D 14}=I$, which $M_{9}$ and $M_{10}$ then mirror to provide, respectively, the bias currents for $M_{3}$ and $M_{4}$ (refer also to Fig. 5.16). As we know, $v_{O P}$ and $v_{O N}$ represent the voltages at which the pull-up actions by $M_{5}$ and $M_{6}$ balance, respectively, the pull-down actions by $M_{3}$ and $M_{4}$.
- Suppose now that for some reason $v_{O P}$ and $v_{O N}$ try to rise above $V_{O C(\text { set })}$. Then, $M_{12}$ and $M_{15}$ will become less conductive, while $M_{13}$ and $M_{14}$ will conduct more, thus raising $I_{D 16}$. By mirror action this will raise $I_{D 9}$ and $I_{D 10}$ and thus boost the pulldown action by $M_{3}$ and $M_{4}$, with the result of forcing $v_{O P}$ and $v_{O N}$ to drop back to $V_{O C(\mathrm{set})}$. By symmetric reasoning, if $v_{O P}$ and $v_{O N}$ try to drop below $V_{O C(\mathrm{set})}, M_{13}$ and $M_{14}$ will conduct less, decreasing $I_{D 16}$ and thus reducing the pull-down action by $M_{3}$ and $M_{4}$. The pull-up action by $M_{5}$ and $M_{6}$ will now prevail, forcing $v_{O P}$ and $v_{O N}$ to rise back to $V_{O C(\text { set })}$.
- Let us now apply an ac signal across the inputs so as to generate the symmetric swings $v_{O P}=V_{O C(\mathrm{set})}+v_{O D} / 2$ and $v_{O N}=V_{O C(\mathrm{set})}-v_{O D} / 2$. These swings will imbalance the differential pairs to give $i_{D 15}=0.5 I-i$ and $i_{D 14}=0.5 I+i$, and $i_{D 12}=0.5 I+i$ and $i_{D 13}=0.5 I-i$, for some current change $i$. However, $M_{16}$ still draws

$$
i_{D 16}=i_{D 13}+i_{D 14}=0.5 I-i+0.5 I+i=I
$$

indicating that the servo loop provided by the CMFN keeps the value of $\left(v_{O P}+v_{O N}\right) / 2$ near $V_{O C(\mathrm{set})}$ regardless of the ac signals present. Of course this holds true so long as none of the transistors is forced out of its active region.

Find the small-signal gain $v_{o d} / v_{i d}$ of the op amp of Fig. 5.51, assuming the parameters of Example 5.4. Compare with the example and comment.

#### Solution

The circuit of Fig. 5.51 is perfectly symmetric about the vertical axis running down from node $V_{G 78}$, so we work with the half-circuit ac equivalent of Fig. 5.52. By inspection, $R_{o}=R_{d 5} / / R_{d 3}$, where $R_{d 5}$ and $R_{d 3}$ are the ac resistances seen looking into the drains of $M_{5}$ and $M_{3}$. Using again inspection we write

$$
R_{o}=\left[r_{o 5}+r_{o 7}+\left(g_{m 5}+g_{m b 5}\right) r_{o 5} r_{o 7}\right] / /\left[r_{o 3}+\left(r_{o 9} / / r_{o 1}\right)+\left(g_{m 3}+g_{m b 3}\right) r_{o 3}\left(r_{o 9} / / r_{o 1}\right)\right]
$$

This is formally identical to Eq. (5.39), so we recycle Example 5.4 to write $R_{o} \cong$ $5.22 \mathrm{M} \Omega$. We also have $i_{1}=g_{m 1}\left(v_{i d} / 2\right)=(0.4 \mathrm{~mA} / \mathrm{V}) \times\left(v_{i d} / 2\right)$. Following the line of reasoning of Example 5.4 we can state that most of $i_{1}$ flows out of $M_{3}$, so

$$
-\frac{v_{o d}}{2} \cong-R_{o} i_{1}=-g_{m 1} R \frac{v_{o d}}{2}
$$

image_name:FIGURE 5.52
description:
[
name: vid/2, type: VoltageSource, value: vid/2, ports: {Np: vid/2, Nn: GND}
name: M1, type: PMOS, ports: {S: GND, D: d1s3, G: vid/2}
name: M5, type: PMOS, ports: {S: GND, D: vod/2, G: d1s3}
name: M3, type: NMOS, ports: {S: GND, D: d1s3, G: GND}
name: ro7, type: Resistor, value: ro7, ports: {N1: GND, N2: vod/2}
name: ro9, type: Resistor, value: ro9, ports: {N1: d1s3, N2: GND}
name: Ro, type: Resistor, value: Ro, ports: {N1: vod/2, N2: GND}
]
extrainfo:This circuit is a half-circuit equivalent of an op-amp, showing a differential pair with PMOS and NMOS transistors. The circuit demonstrates the flow of current i1 from the voltage source through M1 and M3, with the output voltage taken across Ro.

FIGURE 5.52 Half-circuit equivalent of the op amp of Fig. 5.51.

Consequently, $v_{o d} / v_{i d}=g_{m 1} R_{o} \cong 0.4 \times 5,220=2,088 \mathrm{~V} / \mathrm{V}$. The single-ended signal $v_{o}$ of Example 5.4 now splits between the two opposite halves $v_{o p}$ and $v_{o n}$, so the gain is unchanged.

Figure 5.53 shows how the two-stage CMOS op amp of Fig. 5.13 can be turned into a fully differential type (again, the biasing details have been omitted for simplicity). In this rendition the CMFN is now the complementary of that of Fig. 5.51 because it is designed to adjust the current of a $p$ MOSFET, namely, the tail current supplied by $M_{9}$ (evidently there are various different ways of designing a CMFN).
image_name:Figure 5.53
description:
[
name: M1, type: NMOS, ports: {S: GND, D: vP, G: vN}
name: M2, type: NMOS, ports: {S: GND, D: vOP, G: vP}
name: M3, type: NMOS, ports: {S: GND, D: vN, G: VG34}
name: M4, type: NMOS, ports: {S: GND, D: vP, G: VG34}
name: M5, type: NMOS, ports: {S: VSS, D: vOP, G: vP}
name: M6, type: PMOS, ports: {S: VDD, D: vOP, G: vP}
name: M7, type: NMOS, ports: {S: GND, D: vON, G: vON}
name: M8, type: NMOS, ports: {S: GND, D: V68, G: vON}
name: M9, type: PMOS, ports: {S: VDD, D: V68, G: vON}
name: M10, type: NMOS, ports: {S: VSS, D: VG1011, G: vOP}
name: M11, type: NMOS, ports: {S: VSS, D: VG1011, G: vOP}
name: M12, type: PMOS, ports: {S: VDD, D: vOP, G: VOC(set)}
name: M13, type: PMOS, ports: {S: VDD, D: vOP, G: VOC(set)}
name: M14, type: PMOS, ports: {S: VDD, D: vOP, G: VOC(set)}
name: M15, type: PMOS, ports: {S: VDD, D: vOP, G: VOC(set)}
name: M16, type: PMOS, ports: {S: VDD, D: vOP, G: vOP}
name: Rc, type: Resistor, value: Rc, ports: {N1: vN, N2: vP}
name: Cc, type: Capacitor, value: Cc, ports: {Np: vN, Nn: vP}
]
extrainfo:This is a fully differential two-stage CMOS operational amplifier. It includes a common-mode feedback network for differential operation. The circuit is designed to expand the input voltage range by biasing specific transistors at the edge of saturation.

FIGURE 5.53 Fully-differential CMOS op amp of the two-stage type.

#### EXpanding the Input Voltage Range

If we specify $V_{G 34}$ in the folded-cascode op amp of Fig. 5.51 so as to bias the $M_{9}-M_{10}$ pair right at the edge of saturation $\left(V_{D S 9}=V_{O V 9}\right.$ and $\left.V_{D S 10}=V_{O V 10}\right)$, then, the input voltage range (IVR) is specified by Eq. (5.41). For instance, suppose we have a singlesupply system with $V_{S S}=0$ and $V_{D D}=3 \mathrm{~V}$, and let $\left|V_{t 1}\right|=0.75 \mathrm{~V}$ and $V_{O V}=0.25 \mathrm{~V}$ throughout. Then, the common-mode input voltage $v_{I C}=1 / 2\left(v_{P}+v_{N}\right)$ is such that

$$
\begin{aligned}
& v_{I C(\min )}=V_{S S}+V_{O V 9}-\left|V_{t \mid}\right|=0+0.25-0.75=-0.5 \mathrm{~V} \\
& v_{I C(\max )}=V_{D D}-V_{O V 11}-V_{O V 1}-\left|V_{t 1}\right|=3-0.25-0.25-0.75=1.75 \mathrm{~V}
\end{aligned}
$$

While the lower limit is quite desirable because it allows us to lower the inputs all the way down to the ground rail, and even $0.5-\mathrm{V}$ below, without causing any malfunction, the upper limit is generally too restrictive, especially in a low-supply situation such as the $3-\mathrm{V}$ case considered here. Ideally we want the IVR to extend from rail to rail and possibly beyond by, say, a $0.5-\mathrm{V}$ margin (from -0.5 V to 3.5 V in our example). Were we to use the dual op amp realization by interchanging $p$ MOSFETs and $n$ MOSFETs as well as interchanging the power supplies (see Fig. P5.21), then the $n$-type input pair would exhibit the dual constraints $v_{I C(\min )}=1.25 \mathrm{~V}$ and $v_{I C(\max )}=$ 3.5 V . In other words, while a $p$-type input stage works well near $V_{S S}$ but goes off near $V_{D D}$, an $n$-type works well near $V_{D D}$ but goes off near $V_{S S}$, just the opposite.

The above considerations provide the basis for the ingenious solution of Fig. 5.54, which uses both input-stage types to get the best of both. (The CMFN, not shown to
image_name:FIGURE 5.54
description:
[
name: M11p, type: PMOS, ports: {S: VDD, D: x2, G: VG11p}
name: M1n, type: NMOS, ports: {S: x3, D: x2, G: vP}
name: M2n, type: NMOS, ports: {S: x3, D: x1, G: vN}
name: M1p, type: PMOS, ports: {S: x3, D: x4, G: vP}
name: M2p, type: PMOS, ports: {S: x3, D: x1, G: vN}
name: M11n, type: NMOS, ports: {S: x7, D: VSS, G: VG11n}
name: M7, type: PMOS, ports: {S: VDD, D: x1, G: VG78}
name: M8, type: PMOS, ports: {S: VDD, D: x1, G: VG78}
name: M5, type: PMOS, ports: {S: VDD, D: x2, G: VG56}
name: M6, type: PMOS, ports: {S: VDD, D: x1, G: VG56}
name: M3, type: NMOS, ports: {S: x5, D: VON, G: VG34}
name: M4, type: NMOS, ports: {S: x6, D: VOP, G: VG34}
name: M9, type: NMOS, ports: {S: x5, D: x6, G: VG910}
name: M10, type: NMOS, ports: {S: x5, D: x6, G: VG910}
]
extrainfo:The circuit uses complementary input stages with NMOS and PMOS pairs to achieve rail-to-rail input voltage range (IVR). The design aims to optimize performance near both VSS and VDD. The circuit includes bias voltages VG11p, VG11n, VG78, VG56, VG34, and VG910 to control the gates of various transistors.

FIGURE 5.54 Using two complementary input stages $\left(M_{1 n}-M_{2 n}\right.$ and $M_{1 \rho}-M_{2 p}$ ) to achieve a rail-to-rail IVR (CMFN not shown).
avoid cluttering the schematic, can be made to adjust either $V_{G 78}$ or $V_{G 910}$, or both.) Assuming again $V_{t n}=-V_{t p}=0.75 \mathrm{~V}$ and $V_{O V}=0.25 \mathrm{~V}$ throughout, we note the following:

- For $v_{I C}<V_{S S}+V_{O V 11 n}+V_{t n}\left(=1 \mathrm{~V}\right.$ for $\left.V_{S S}=0\right)$ the $M_{1 n}-M_{2 n}$ pair is off whereas the $M_{1 p}-M_{2 p}$ pair is fully operational, so we rewrite Eq. (5.38) as $G_{m}=g_{m 1 p}$.
- Raising $v_{I C}$ above 1 V will gradually turn on the $M_{1 n}-M_{2 n}$ pair until both pairs are fully operational once we pass the $1.25-\mathrm{V}$ mark. For $1.25 \mathrm{~V} \leq v_{I C} \leq 1.75 \mathrm{~V}$ the two pairs work in tandem, giving $G_{m}=g_{m 1 p}+g_{m 1 n}$.
- Raising $v_{I C}$ above 1.75 V will gradually turn off the $M_{1 p}-M_{2 p}$ pair while the $M_{1 n}-M_{2 n}$ pair continues to be fully operational.
- For $v_{I C}>V_{D D}-V_{O V 11 p}-\left|V_{t p}\right|\left(=2 \mathrm{~V}\right.$ for $\left.V_{D D}=3 \mathrm{~V}\right)$ the $M_{1 p}-M_{2 p}$ pair is totally off, so the circuit gives $G_{m}=g_{m 1 n}$.
- So long as the $M_{7}-M_{8}$ and the $M_{9}-M_{19}$ pairs are biased at the edge of saturation, the output voltage swing (OVS) will extend to within two $V_{O V}$ of either supply rail. If a true rail-to-rail OVS is desired, then an ad-hoc output stage is required, such as the CS push-pull output stage of Section 4.11.

Shown in Fig. 5.55 is the bipolar version of Fig. 5.54. To maximize the IVR, $V_{B 34}$ is set to bias the $Q_{9}-Q_{10}$ pair slightly above the edge of saturation, say at $V_{C E 9}=V_{C E 10} \cong$ 0.25 V . Likewise, $V_{B 56}$ is set so that $V_{E C 7}=V_{E C 8} \cong 0.25 \mathrm{~V}$. Then, assuming B-E voltage drops of 0.65 V , we have $v_{I C(\min )}=V_{E E}+2 \times 0.25-0.65=V_{E E}-0.15 \mathrm{~V}$
image_name:Figure 5.55
description:
[
name: Q11p, type: PMOS, ports: {S: x2, D: vb11p, G: vp}
name: Q11n, type: NMOS, ports: {S: x4, D: vb11n, G: x4}
name: Q1n, type: NMOS, ports: {S: vp, D: x2, G: x3}
name: Q2n, type: NMOS, ports: {S: x4, D: x1, G: x3}
name: Q1p, type: PMOS, ports: {S: x3, D: vp, G: x4}
name: Q2p, type: PMOS, ports: {S: x4, D: x4, G: x4}
name: Q7, type: PMOS, ports: {S: vcc, D: x2, G: vb78}
name: Q8, type: PMOS, ports: {S: vcc, D: x1, G: vb78}
name: Q5, type: PMOS, ports: {S: x2, D: x1, G: vb56}
name: Q6, type: PMOS, ports: {S: x1, D: vop, G: vb56}
name: Q3, type: NMOS, ports: {S: x1, D: x6, G: vb34}
name: Q4, type: NMOS, ports: {S: x1, D: x6, G: vb34}
name: Q9, type: NMOS, ports: {S: x6, D: vee, G: vb910}
name: Q10, type: NMOS, ports: {S: x6, D: vee, G: vb910}
]
extrainfo:This circuit diagram represents a bipolar operational amplifier with rail-to-rail input voltage range (IVR). The circuit includes multiple PMOS and NMOS transistors configured to maximize the IVR. The bias voltages V_B34, V_B56, and V_B910 are set to avoid saturation of the transistors near the supply rails. The circuit is designed to handle input offset voltage issues near the lower end of the IVR.

FIGURE 5.55 Bipolar op amp of with a rail-to-rail IVR (CMFN not shown).
and $v_{I C(\max )}=V_{D D}+0.15 \mathrm{~V}$. In some embodiments the $Q_{7}-Q_{8}$ and $Q_{9}-Q_{10}$ pairs are replaced by resistor pairs ${ }^{1}$ to develop the voltage drops of about 0.25 V that are required to prevent the input pairs from saturating in the vicinity of the supply rails.

A notorious issue with the op amps of Figs. 5.54 and 5.55 is that near the lower end of the IVR the input offset voltage of the $p$-type pair dominates, whereas near the upper end that of the $n$-type pair dominates. So, as $v_{I C}$ changes from one end to the other of the IVR, the net input offset voltage will generally change in magnitude and possibly in polarity, depending on the magnitudes and directions of the individual mismatches. In the bipolar case also the input bias current may pose problems: at the lower end it coincides with the base current of the $p$-type pair, flowing out of the op amp, but at the higher end it coincides with that of the $n$-type pair, flowing into the op amp. At intermediate IVR values both pairs are on and the base currents of the $p$-type pair tend to cancel those of the $n$-type pair. Consequently, input bias-current magnitude and direction are strong functions of $v_{I C}$.

## 5.8 SWITCHED-CAPACITOR CIRCUITS

Traditionally, electronic systems have been designed using off-the-shelf analog and digital ICs, along with passive components such as resistors and capacitors, all mounted on a common medium such as a printed-circuit board (PCB). Nowadays, for reasons of cost, miniaturization, power consumption, and reliability, the trend is to integrate both analog and digital functions on the same silicon chip to create circuits aptly called mixed-signal ICs. Given that digital electronics is dominated by CMOS technology, analog functions must be implemented using exclusively the components most easily available in this technology, namely, MOSFETs and capacitors (to keep die size within reason, capacitances must be limited to a few tens of picofarads or less). Resistors and larger capacitors must therefore be avoided altogether. Figure 5.56 shows the conceptual structure of these two basic components (the shaded capacitances represent parasitics that will be discussed later). The type of capacitor shown is referred to as double-polysilicon capacitor because it is made up of two polysilicon layers, the same material type as the gate (being of the $n^{+}$type, these layers can for all purposes be regarded as metal plates).

The most common applications of the MOSFET are amplification and switching. We have already investigated switching in the design of the logic gates of Chapter 3, and amplification in the design of CMOS op amps such as the cascode op amp of Fig. 5.17. A unique advantage of CMOS op amps is that they exhibit the virtually infinite input resistances presented by the gate terminals of the input FETs. This makes it possible to drive the op amp with voltages stored in on-chip capacitors with very small leakage. Also, the reason for cascoding is to raise the resistance levels in order to achieve high dc gain. If we were to apply resistive feedback around such an op amp, output loading by the external resistances would be so severe as to invalidate the high-gain advantages accrued via cascoding. Mercifully, capacitive feedback (as opposed to resistive feedback) loads down the op amp only during transients. Once steady state is achieved, capacitors act as open circuits, thus preserving high dc gains. Another important advantage of cascode op amps, not immediately obvious at this
image_name:FIGURE 5.56
description:The image labeled as "FIGURE 5.56" illustrates the conceptual structure of an n-channel MOSFET and a double-poly capacitor, highlighting parasitic capacitances.

1. **Identification of Components and Structure:**
- The top section of the diagram shows a cross-sectional view of an n-MOSFET on a p-type substrate. Key components include:
- **Source/Drain (S/D) and Drain/Source (D/S):** These terminals are marked on either side of the n+ regions, which are doped areas in the silicon substrate.
- **Gate (G):** Positioned above the channel, separated by a thin oxide layer.
- **Body (B):** The p-type substrate itself, also labeled.
- **Parasitic Capacitances:**
- **Overlap Capacitances (C_ov):** Between the gate and the source/drain.
- **Junction Capacitances (C_j):** Associated with the n+ regions and the substrate.
- To the right, a double-poly capacitor is shown with:
- **Top Plate (X) and Bottom Plate (Y):** Representing the two conductive layers separated by an insulating layer.
- **Parasitic Capacitances:**
- **Top-plate Capacitance (C_top):** Between the top plate and the substrate.
- **Bottom-plate Capacitance (C_btm):** Between the bottom plate and the substrate.

2. **Connections and Interactions:**
- **MOSFET:**
- The gate controls the channel (Q_n) formed between the source and drain, allowing current to flow when a voltage is applied.
- The overlap and junction capacitances affect the switching characteristics and frequency response of the MOSFET.
- **Double-Poly Capacitor:**
- Capacitive interactions between the plates and the substrate are highlighted by the parasitic capacitances, which influence the effective capacitance and potential signal loss.

3. **Labels, Annotations, and Key Features:**
- The diagram includes annotations for each capacitance (C_ov, C_j, C_top, C_btm) and key regions (n+, p- substrate).
- Arrows and component symbols are used to indicate the direction of current flow and the location of capacitive elements.
- The lower part of the image provides simplified schematic representations of the MOSFET and capacitor, with the same labels for consistency.

This diagram provides a detailed view of the parasitic elements in an n-MOSFET and a double-poly capacitor, emphasizing the impact of these parasitic capacitances on device performance.
image_name:n MOSFET
description:
[
name: Cov, type: Capacitor, value: Cov, ports: {Np: G, Nn: S/D}
name: Cov, type: Capacitor, value: Cov, ports: {Np: G, Nn: D/S}
name: Cj, type: Capacitor, value: Cj, ports: {Np: S/D, Nn: B}
name: Cj, type: Capacitor, value: Cj, ports: {Np: D/S, Nn: B}
name: Ctop, type: Capacitor, value: Ctop, ports: {Np: X, Nn: B}
name: Cbtm, type: Capacitor, value: Cbtm, ports: {Np: Y, Nn: B}
name: C, type: Capacitor, value: C, ports: {Np: X, Nn: Y}
name: NMOS, type: NMOS, ports: {S: S/D, D: D/S, G: G}
]
extrainfo:The diagram illustrates a conceptual structure of an n-channel MOSFET and a double-poly capacitor. It shows the parasitic overlap capacitances (Cov) and parasitic top-plate/bottom-plate capacitances (Ctop and Cbtm). The NMOS transistor is connected with its source and drain labeled as S/D and D/S, respectively, and the gate labeled as G. The capacitors are connected to various nodes, including the body node labeled as B.
image_name:double-poly capacitor
description:
[
name: Cov, type: Capacitor, value: Cov, ports: {Np: G, Nn: S/D}
name: Cov, type: Capacitor, value: Cov, ports: {Np: G, Nn: D/S}
name: Cj, type: Capacitor, value: Cj, ports: {Np: S/D, Nn: B}
name: Cj, type: Capacitor, value: Cj, ports: {Np: D/S, Nn: B}
name: Qn, type: NMOS, ports: {S: S/D, D: D/S, G: G}
name: Ctop, type: Capacitor, value: Ctop, ports: {Np: X, Nn: B}
name: C, type: Capacitor, value: C, ports: {Np: X, Nn: Y}
name: Cbtm, type: Capacitor, value: Cbtm, ports: {Np: Y, Nn: B}
]
extrainfo:The diagram illustrates the conceptual structure of an NMOS transistor and a double-poly capacitor, highlighting parasitic capacitances. The NMOS transistor is connected with overlap capacitances (Cov) and junction capacitances (Cj) at its source/drain terminals. The double-poly capacitor consists of a main capacitance (C) and parasitic top-plate (Ctop) and bottom-plate (Cbtm) capacitances. These components are typically used in mixed-signal IC design to manage capacitive loading and improve stability.

FIGURE 5.56 Conceptual structure of an $n$ MOSFET and a double-poly capacitor, showing the parasitic overlap capacitances $C_{o V}$ and parasitic top-plate/bottom-plate capacitances $C_{\text {top }}$ and $C_{b t m}$.
juncture but to be investigated in great detail in Chapter 7, is that capacitive loading reinforces their ability to stave off the possibility of oscillation, a feature not available in most other op amp types. In summary, the on-chip components available to the mixed-signal IC designer are (a) CMOS op amps, especially cascode types, (b) small capacitors (on the order of picofarads or less), and (c) MOSFET switches. Let us now address the switched-capacitor concept.

### The Switched Capacitor

Figure 5.57 shows a basic switched-capacitor arrangement, along with the gate drive for the two FETs. We make the following observations:

- When $\phi$ is high, $M_{1}$ is on while $M_{2}$ is off because $\bar{\phi}$ is low. $M_{1}$ charges $C$ toward $v_{1}$, and when $v_{C}$ comes within $v_{O V 1}$ of $v_{1}, M_{1}$ enters the triode region, where it approximates a resistance $r_{D S 1}$ as in Fig. 5.58a. If $\phi$ is kept high for a duration sufficiently longer than the time constant $\tau_{1}=r_{D S 1} C$, we can say that by the time $\phi$ returns low we practically have $v_{C}=v_{1}$.
- When $\bar{\phi}$ is high the situation reverses as in Fig. $5.58 b$, so now $M_{2}$ charges $C$ toward $v_{2}$. Assuming $\bar{\phi}$ is kept high long enough compared to $\tau_{2}=r_{D S 2} C$ to fully
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: ϕ}
name: M2, type: NMOS, ports: {S: GND, D: X, G: ϕ̅}
name: C, type: Capacitor, value: C, ports: {Np: X, Nn: GND}
name: V1, type: VoltageSource, value: v1, ports: {Np: V1, Nn: GND}
name: V2, type: VoltageSource, value: v2, ports: {Np: V2, Nn: GND}
]
extrainfo:The circuit is a basic switched capacitor circuit with non-overlapping clock drive. M1 and M2 are NMOS transistors used to charge and discharge the capacitor C between two voltage sources V1 and V2. The clock signals ϕ and ϕ̅ control the switching of M1 and M2, respectively, allowing charge transfer between V1 and V2 through the capacitor C.
image_name:(b)
description:The graph in figure (b) consists of two time-domain waveforms, each representing a clock signal, labeled \( \phi \) and \( \bar{\phi} \), respectively. These waveforms are essential for controlling the operation of switched-capacitor circuits.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform depicting clock signals.

2. **Axes Labels and Units:**
- The horizontal axis represents time \( t \), although specific units are not provided, it is typically in seconds or milliseconds.
- The vertical axis represents voltage levels, with two distinct levels marked as \( V_H \) (high voltage) and \( V_L \) (low voltage).

3. **Overall Behavior and Trends:**
- Both waveforms exhibit a square wave pattern, alternating between high \( V_H \) and low \( V_L \) voltage levels.
- The waveform for \( \phi \) shows a high state for a duration \( T_S \), followed by a low state of the same duration, repeating periodically.
- The waveform for \( \bar{\phi} \) is complementary to \( \phi \), meaning when \( \phi \) is high, \( \bar{\phi} \) is low, and vice versa.

4. **Key Features and Technical Details:**
- The period of the waveform \( \phi \) is marked as \( T_S \), indicating the duration of one complete cycle.
- Both waveforms are non-overlapping, which is crucial for preventing short circuits in switched-capacitor circuits.
- The high and low voltage levels \( V_H \) and \( V_L \) are consistent across both waveforms, ensuring reliable switching.

5. **Annotations and Specific Data Points:**
- The graph indicates the non-overlapping nature of the clock signals, a key feature for the proper operation of the circuit described in the context.
- The consistent voltage levels \( V_H \) and \( V_L \) suggest that the system is designed to operate within these bounds for effective charge transfer.

(b)

FIGURE 5.57 (a) Basic switched capacitor and (b) non-overlapping clock drive.
charge $C$ to $v_{2}$, we can say that by the time $\bar{\phi}$ returns low there has been a charge transfer $\Delta Q$ from $v_{1}$ to $v_{2}$ such that

$$
\begin{equation*}
\Delta Q=C\left(v_{1}-v_{2}\right) \tag{5.82}
\end{equation*}
$$

(This, assuming $v_{1}>v_{2}$. If $v_{1}<v_{2}$, then charge transfer is from $v_{2}$ to $v_{1}$.)

- If the process is repeated at a rate of $f_{S}\left(=1 / T_{S}\right)$ cycles/sec, then the charge transferred in one second is $f_{S} \Delta Q=f_{S} C\left(v_{1}-v_{2}\right)$. But, charge/second represents average current, $i_{\mathrm{avg}}=f_{S} C\left(v_{1}-v_{2}\right)$, suggesting that the switched-capacitor block acts like an equivalent resistance $R_{e q}=\left(v_{1}-v_{2}\right) / i_{\text {avg }}$, or

$$
\begin{equation*}
R_{e q}=\frac{1}{C f_{S}} \tag{5.83}
\end{equation*}
$$

This equivalence is depicted in Fig. 5.59, where the MOSFET pair of Fig. 5.57a is shown as a break-before-make switch of the single-pole double-throw (SPDT) type. We must prevent the MOSFETs from being on simultaneously as this would short the $v_{1}$ and $v_{2}$ sources together and invalidate Eq. (5.82). Hence, the need for non-overlapping gate drives in the manner of Fig. 5.57b.

A popular application of the simulated resistor of Eq. (5.82) is in the synthesis of filters, of which the integrator to be investigated next is the most basic building block.
image_name:(a)
description:
[
name: r_DS1, type: Resistor, value: r_DS1, ports: {N1: V1, N2: VC}
name: r_DS2, type: Resistor, value: r_DS2, ports: {N1: VC, N2: V2}
name: C, type: Capacitor, value: C, ports: {Np: VC, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: VC, G: VL}
name: M2, type: NMOS, ports: {S: VC, D: GND, G: VL}
name: v1, type: VoltageSource, value: v1, ports: {Np: V1, Nn: GND}
name: v2, type: VoltageSource, value: v2, ports: {Np: V2, Nn: GND}
]
extrainfo:The circuit illustrates a switched-capacitor network with two configurations: (a) when M2 is active, connecting the capacitor to V1; and (b) when M1 is active, connecting the capacitor to V2. The NMOS transistors M1 and M2 act as switches controlled by the gate voltage VL.
image_name:(b)
description:
[
name: v1, type: VoltageSource, value: v1, ports: {Np: V1, Nn: GND}
name: r_DS2, type: Resistor, value: r_DS2, ports: {N1: VC, N2: V2}
name: C, type: Capacitor, value: C, ports: {Np: VC, Nn: GND}
name: M1, type: NMOS, ports: {S: V1, D: VC, G: VL}
name: v2, type: VoltageSource, value: v2, ports: {Np: V2, Nn: GND}
]
extrainfo:The circuit is a switched-capacitor configuration with an NMOS transistor M1, which connects the voltage sources v1 and v2 through a capacitor C when switched. The circuit is designed to prevent simultaneous connection of v1 and v2, ensuring a non-overlapping gate drive.

FIGURE 5.58 Circuit equivalent of the switched capacitor of Fig. $5.57 a$ when (a) $\phi$ is high and (b) $\bar{\phi}$ is high.
image_name:FIGURE 5.58
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: V2, type: VoltageSource, value: V2, ports: {Np: V2, Nn: GND}
name: SW1, type: Switch, ports: {N1: W1, N2: W2}
name: C, type: Capacitor, value: C, ports: {Np: W2, Nn: GND}
name: Req, type: Resistor, value: 1/Cfs, ports: {N1: V1, N2: V2}
]
extrainfo:The circuit is a switched-capacitor configuration with two voltage sources V1 and V2 connected through a switch SW1 and a capacitor C. When SW1 is closed, V1 charges the capacitor C. The equivalent resistance when switched at frequency f_s is represented as Req = 1/(C*f_s), connecting V1 and V2.
image_name:FIGURE 5.59
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: V2, type: VoltageSource, value: V2, ports: {Np: V2, Nn: GND}
name: C, type: Capacitor, value: C, ports: {Np: W1, Nn: GND}
name: SW1, type: Switch, ports: {N1: W1, N2: W2}
name: Req, type: Resistor, value: 1/Cfs, ports: {N1: V1, N2: V2}
]
extrainfo:The circuit diagram represents a switched-capacitor network where a capacitor C is switched at frequency fs between two voltage sources V1 and V2. The equivalent resistance of the switched-capacitor is 1/(Cfs). The switch SW1 controls the connection between nodes W1 and W2, alternating the capacitor connection between the two voltage sources.

FIGURE 5.59 A capacitance $C$ switched at a frequency of $f_{s}$ draws on average the same current as a resistance of value $1 /\left(C f_{s}\right)$.

### Switched-Capacitor Integrator

The classic integrator of Fig. 5.60a is also called RC integrator because we use the external $R$-C network to configure the op amp for integration. Applying KCL we get $\left(V_{i}-0\right) / R_{1}=\left(0-V_{o}\right) /\left[1 /\left(s C_{2}\right)\right]$. Letting $s \rightarrow j 2 \pi f$ and simplifying gives the inverting-type integrator transfer function

$$
\begin{equation*}
H_{R C}(j f)=\frac{V_{o}}{V_{i}}=-\frac{1}{j f / f_{0}} \tag{5.84}
\end{equation*}
$$

where

$$
\begin{equation*}
f_{0}=\frac{1}{2 \pi R_{1} C_{2}} \tag{5.85}
\end{equation*}
$$

is called the unity-gain frequency because $\left|H_{R C}\left(j f_{0}\right)\right|=1$. We now wish to rephrase the circuit of Fig. $5.60 a$ in switched-capacitor (SC) form so we can fabricate it entirely on chip. To achieve this we replace $R_{1}$ with a simulated resistor as in Fig. 5.60b, and we scale $C_{2}$ to a small enough value so we can realistically fabricate it on chip. Using Eq. (5.83) to write $R_{1}=1 /\left(C_{1} f_{S}\right)$ and substituting into Eq. (5.85) we get

$$
\begin{equation*}
f_{0}=\frac{1}{2 \pi} \frac{C_{1}}{C_{2}} f_{S} \tag{5.86}
\end{equation*}
$$

We make the following important observations:

- The SC integrator uses no resistors, a definite advantage because accurate and stable resistors are difficult to fabricate on chip. The SC integrator uses MOSFETs and capacitors instead.
image_name:(a)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vi, N2: 0V}
name: C2, type: Capacitor, value: C2, ports: {Np: 0V, Nn: Vo}
name: OpAmp1, type: OpAmp, value: OpAmp1, ports: {InP: GND, InN: 0V, OutP: Vo}
]
extrainfo:The circuit is an RC integrator. It uses a resistor (R1) and capacitor (C2) to integrate the input voltage (Vi) and produce an output voltage (Vo). The operational amplifier (OpAmp1) is configured as an integrator with the capacitor (C2) providing feedback.
image_name:(b)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: fs, type: Switch, ports: {N1: Vi, N2: C1}
name: C1, type: Capacitor, value: C1, ports: {Np: C1, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: 0V, Nn: Vo}
name: OpAmp, type: OpAmp, value: OpAmp, ports: {InP: 0V, InN: GND, OutP: Vo}
]
extrainfo:The circuit is a switched-capacitor integrator. The input voltage Vi is sampled by the switch fs and capacitor C1. The operational amplifier, along with capacitor C2, integrates the input signal to produce an output voltage Vo.

FIGURE 5.60 (a) The $R C$ integrator, and (b) its switched-capacitor (SC) implementation.

- The unity-gain frequency $f_{0}$ is established by the product $R_{1} C_{2}$ in the $R C$ integrator, but by the ratio $C_{2} / C_{1}$ in the $S C$ integrator. Compared to products, ratios are much easier to control during fabrication and to maintain with temperature and time. Capacitance matching within $0.5 \%$ is easily achievable in MOS technology. ${ }^{2}$ This is another important advantage of $S C$ integrators.
- The unity-gain frequency $f_{0}$ of the $S C$ integrator is directly proportional to the switching frequency $f_{S}$, so, if desired, we can program $f_{0}$ automatically over a wide range of values by suitably varying $f_{S}$.
(a) Specify component values for $f_{0}=10 \mathrm{kHz}$ in the integrator of Fig. 5.60a, and comment.
(b) Repeat, but for the circuit of Fig. $5.60 b$ if $f_{S}=1 \mathrm{MHz}$. Do not exceed a total capacitance of 10 pF .

#### Solution

(a) Arbitrarily choose $C_{2}=1 \mathrm{nF}$. Then Eq. (5.85) gives,

$$
R_{1}=\frac{1}{2 \pi C_{2} f_{0}}=\frac{1}{2 \pi 10^{-9} \times 10^{4}}=15.9 \mathrm{k} \Omega
$$

Both values are easily available off the shelf, but $C_{2}$ could hardly be fabricated on chip. Moreover, because of component tolerances, $f_{0}$ may require tuning (via $R_{1}$ ), and will drift with temperature because so do $R_{1}$ and $C_{2}$.
(b) By Eq. (5.86) we have

$$
\frac{C_{2}}{C_{1}}=\frac{f_{S}}{2 \pi f_{0}}=\frac{10^{6}}{2 \pi 10^{4}}=15.9
$$

Arbitrarily pick $C_{1}=0.5 \mathrm{pF}$, so $C_{2}=7.958 \mathrm{pF}$, for a total capacitance of less than 10 pF , which we can readily fabricate on chip.

### Discrete-Time Considerations

The SC integrator is a discrete-time circuit because the current between the input source and the op amp flows in the form of charge packets. (Conversely, the $R C$ integrator is a continuous-time circuit because so is the current flowing via $R_{1}$.) We now wish to investigate how charge discretization affects the transfer function of the SC integrator compared to its $R C$ counterpart. To this end we use the PSpice circuit of Fig. 5.61 and turn our attention to the waveforms of Fig. 5.62. As shown, $C_{1}$ switches back and forth between $v_{I}$ and the op amp's virtual ground $(0 \mathrm{~V})$ at a frequency of $f_{S}=10 \mathrm{MHz}$, so we divide the time axis into intervals of $T_{S}=1 / f_{S}=1 / 10^{7}=100 \mathrm{~ns}$ each. For $v_{I}>0, C_{1}$ 's charge is dumped into $C_{2}$, causing a negative-going step in $v_{0}$. Conversely, for $v_{I}<0$, charge is pulled out of $C_{2}$, yielding a positive-going step in $v_{O}$. Of particular significance are the falling edges of the $v_{G 1}$ pulse train because these are the instants at which $C_{1}$, after having been fully charged to $v_{l}$, is ready to be discharged into $C_{2}$. Labeling these instants sequentially as $\ldots n-1, n, n+1 \ldots$
image_name:FIGURE 5.61 PSpice circuit
description:
[
name: VC1, type: VoltageSource, value: VC1, ports: {Np: VG1, Nn: GND}
name: VG1, type: VoltageSource, value: VG1, ports: {Np: VG1, Nn: GND}
name: VG2, type: VoltageSource, value: VG2, ports: {Np: VG2, Nn: GND}
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: M1, type: NMOS, ports: {S: VB, D: VC1, G: VG2}
name: M2, type: NMOS, ports: {S: VI, D: VC1, G: VG1}
name: C1, type: Capacitor, value: 10 pF, ports: {Np: VC1, Nn: GND}
name: C2, type: Capacitor, value: 100 pF, ports: {Np: VO, Nn: InN}
name: A1, type: OpAmp, value: A1, ports: {InP: VC1, InN: GND, OutP: VO}
]
extrainfo:The circuit is a switched-capacitor integrator. It uses NMOS transistors M1 and M2 to control the charge transfer between capacitors C1 and C2. The operational amplifier A1 is configured to integrate the input voltage VI, producing the output voltage VO. The gates of M1 and M2 are controlled by voltage sources VG2 and VG1, respectively.

FIGURE 5.61 PSpice circuit to investigate the SC integrator in the time domain.
we can say that the change experienced by $v_{O}$ from the instant $n-1$ to the instant $n$ is set by the charge $C_{1} v_{I}(n-1)$ accumulated in $C_{1}$ at the instant $n-1$ according to

$$
\begin{equation*}
v_{O}(n)-v_{O}(n-1)=\frac{-C_{1} v_{l}(n-1)}{C_{2}} \tag{5.87}
\end{equation*}
$$

image_name:FIGURE 5.62 Waveforms of the PSpice circuit of Fig. 5.61
description:The graph titled "FIGURE 5.62 Waveforms of the PSpice circuit of Fig. 5.61" presents time-domain waveforms for a switched-capacitor (SC) integrator circuit. It consists of three subplots showing different voltage signals over time, measured in nanoseconds (ns).

1. **Top Subplot (VG1 and VG2):**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The vertical axis represents voltage in volts (V), ranging from -2 V to 5 V. The horizontal axis represents time in nanoseconds (ns), spanning from 0 to 1000 ns.
- **Overall Behavior and Trends:** The waveforms are square waves for both VG1 and VG2, indicating periodic switching between high and low states.
- **Key Features:** VG1 and VG2 alternate between approximately 0 V and 5 V, with VG2 lagging VG1 slightly.

2. **Middle Subplot (vC1 and vI):**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The vertical axis represents voltage in volts (V), ranging from 0 V to 1 V. The horizontal axis is the same as the top subplot.
- **Overall Behavior and Trends:** The waveform vC1 shows a series of decaying exponential curves, while vI displays a linear decrease over time.
- **Key Features:** vC1 peaks at approximately 1 V and decreases rapidly, while vI gradually decreases from 1 V to near 0 V over the entire time span.

3. **Bottom Subplot (vO):**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The vertical axis represents voltage in volts (V), ranging from -0.5 V to 0 V. The horizontal axis is consistent with the other subplots.
- **Overall Behavior and Trends:** The waveform vO shows a stepped decrease in voltage, with each step occurring at regular time intervals.
- **Key Features:** Each step decreases the voltage by approximately 0.1 V, resulting in a cumulative decrease over time.

Overall, the graph illustrates the behavior of a switched-capacitor integrator, showing how input voltages VG1 and VG2 control the charging and discharging of capacitors, affecting the output voltage vO in discrete steps.

FIGURE 5.62 Waveforms of the PSpice circuit of Fig. 5.61.

This discrete-time sequence is best investigated via the Fourier transforms $V_{i}(j \omega)$ and $V_{o}(j \omega)$. A well-known property of these transforms states that delaying a signal by one clock period $T_{S}$ is equivalent to multiplying its Fourier transform by $\exp \left(-j \omega T_{S}\right)$. This means that Eq. (5.87) transforms into

$$
V_{o}(j \omega)-V_{o}(j \omega) e^{-j \omega T_{s}}=-\frac{C_{1}}{C_{2}} V_{i}(j \omega) e^{-j \omega T_{s}}
$$

Collecting and simplifying we get

$$
V_{o}(j \omega)=-\frac{C_{1}}{C_{2}} V_{i}(j \omega) \frac{e^{-j \omega T_{s}}}{1-e^{-j \omega T_{s}}}=-\frac{C_{1}}{C_{2}} V_{i}(j \omega) \frac{e^{-j \omega T_{s} / 2}}{e^{j \omega T_{s} / 2}-e^{-j \omega T_{s} / 2}}
$$

Letting $\omega=2 \pi f, T_{S}=1 / f_{S}$, and using the identity $\sin x=\left(e^{x}-e^{-x}\right) / 2 j$ we get, after some algebra,

$$
\begin{equation*}
H_{S C}(j f)=\frac{V_{o}(j f)}{V_{i}(j f)}=-\frac{1}{j f / f_{0}} \times \frac{\pi f / f_{S}}{\sin \left(\pi f / f_{S}\right)} \times e^{-j \pi f / f_{s}} \tag{5.88}
\end{equation*}
$$

where again

$$
\begin{equation*}
f_{0}=\frac{1}{2 \pi} \frac{C_{1}}{C_{2}} f_{S} \tag{5.89}
\end{equation*}
$$

We observe that in the limit $f \ll f_{S}$ we have $H_{S C}(j f) \rightarrow H_{R C}(j f)$, that is, the $S C$ integrator approximates the $R C$ integrator. Physically this makes sense because for $f_{S} \gg f$ charge transfer can be regarded as a continuous process. Otherwise, $H_{S C}(j f)$ will deviate from $H_{R C}(j f)$ by the magnitude and phase errors

$$
\begin{equation*}
\varepsilon_{m}(f)=\frac{\pi f / f_{S}}{\sin \left(\pi f / f_{S}\right)}-1 \quad \varepsilon_{\phi}(f)=-180^{\circ}\left(f / f_{S}\right) \tag{5.90}
\end{equation*}
$$

Figure 5.63 compares the transfer function magnitudes for the case $f_{S}=10 f_{0}$.
image_name:Figure 5.63
description:Figure 5.63 is a plot comparing the transfer function magnitudes of an RC integrator and an SC integrator. The graph is a Bode plot, which is typically used to illustrate the frequency response of a system.

1. **Type of Graph and Function:**
- The graph is a Bode plot showing magnitude responses of two integrators.

2. **Axes Labels and Units:**
- The x-axis represents frequency, labeled from 0 to $f_S$, with a significant point marked at $f_0$.
- The y-axis represents the magnitude of the transfer function, ranging from 0 to 2.
- The plot uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The plot shows two curves: one for the SC integrator $|H_{SC}|$ and one for the RC integrator $|H_{RC}|$.
- Both curves start at a high magnitude near 2 when the frequency is near 0 and decrease as the frequency increases.
- The SC integrator curve ($|H_{SC}|$) decreases more sharply compared to the RC integrator curve ($|H_{RC}|$), indicating a more pronounced drop in magnitude with increasing frequency.
- At higher frequencies, the SC integrator curve increases again, forming a U-shape, while the RC integrator curve continues to decrease.

4. **Key Features and Technical Details:**
- At frequency $f_0$, both curves have decreased significantly from their initial values.
- The SC integrator shows a deviation from the RC integrator, as indicated by the sharper decline and subsequent increase at higher frequencies.
- The deviation is characterized by the magnitude error $\varepsilon_{m}(f)$ and phase error $\varepsilon_{\phi}(f)$ as described in the context.

5. **Annotations and Specific Data Points:**
- The graph is annotated with the labels $|H_{SC}|$ and $|H_{RC}|$ to distinguish between the two curves.
- There are no specific numerical values marked on the graph, but the context provides calculations for these deviations at certain frequencies.

FIGURE 5.63 Comparing the transfer functions of the $R C$ and $S C$ integrators.

EXAMPLE 5.16 (a) Calculate the deviation of $H_{S C}(j f)$ from $H_{R C}(j f)$ in Fig. 5.63 at $f=f_{0}$ and at $f=2 f_{0}$. Compare and comment.
(b) Repeat, but for the circuit of Fig. 5.61. Compare with (a) and comment.

#### Solution

(a) In Fig. 5.63 we have $f_{0} / f_{S}=1 / 10$, so Eq. (5.90) gives $\varepsilon_{m}\left(f_{0}\right)=(\pi / 10) /$ $\sin (\pi / 10)-1=1.0166-1=1.66 \%$ and $\varepsilon_{\phi}\left(f_{0}\right)=-180 / 10=-18^{\circ}$. Similarly, $\varepsilon_{m}\left(2 f_{0}\right)=6.9 \%$ and $\varepsilon_{\phi}\left(2 f_{0}\right)=-36^{\circ}$, indicating a doubling in $\varepsilon_{\phi}$ but a much greater increase in $\varepsilon_{m}$.
(b) By Eq. (5.89) the circuit of Fig. 5.61 has $f_{0} / f_{S}=\left(C_{1} / C_{2}\right) /(2 \pi)=(10 / 100) /$ $(2 \pi)=1 / 62.83$, so we now get $\varepsilon_{m}\left(f_{0}\right)=0.0417 \%$ and $\varepsilon_{\phi}\left(f_{0}\right)=-2.86^{\circ}$. Also, $\varepsilon_{m}\left(2 f_{0}\right)=0.167 \%$ and $\varepsilon_{\phi}\left(2 f_{0}\right)=-5.73^{\circ}$. The deviations are now appreciably smaller because the ratio $f_{0} / f_{S}$ is $2 \pi$ times as small.

### Autozeroing Techniques

Because of component mismatches stemming from fabrication process variations, a differential amplifier such as an op amp or a voltage comparator exhibit some input offset voltage $V_{O S}$. As shown in Fig. 5.64a, we can visualize a real-life amplifier as consisting of an ideal, offsetless amplifier but equipped with an internal voltage source $V_{O S}$ in series with one of its inputs to account for the internal imbalances (it doesn't matter which input, as $V_{O S}$ is unpredictable both in magnitude and polarity). The presence of $V_{O S}$ is likely to be a serious drawback in precision applications, so it is desirable to automatically compensate for its presence, a task referred to as autozeroing. CMOS circuits utilize a capacitor $C$ as in Fig. 5.64b to store a voltage of equal magnitude but opposite polarity as $V_{O S}$. Being in series, the two voltages cancel each other out, giving the appearance of offset-free behavior. The amplifier alternates between two modes of operation known as the autozeroing and the sampling mode:

- During the autozero phase depicted in Fig. 5.65a, switches $S_{1}$ and $S_{2}$ disconnect the amplifier from nodes $v_{P}$ and $v_{N}$ while $S_{4}$ configures it as a unity-gain voltage follower. The circuit now buffers its own internal offset voltage $V_{O S}$ to $C$ via $S_{3}$, so with $S_{5}$ closed $C$ will charge to whatever value of $V_{O S}$ the amplifier exhibits at that moment. (For this scheme to work, the amplifier must be unity-gain stable.
image_name:(a)
description:
[
name: VOS, type: VoltageSource, value: VOS, ports: {Np: vP, Nn: vN}
name: OpAmp, type: OpAmp, ports: {InP: vN, InN: vP, OutP: vO, OutN: '}
name: C, type: Capacitor, value: C, ports: {Np: vP, Nn: vN'}
]
extrainfo:The circuit represents an autozeroing phase for a differential amplifier. The offset voltage VOS is buffered and stored across the capacitor C, allowing the amplifier to operate as an offsetless unity-gain voltage follower.
image_name:(b)
description:
[
name: OpAmp_b, type: OpAmp, ports: {InP: vP, InN: vN, OutP: vO}
name: C, type: Capacitor, value: C, ports: {Np: vP, Nn: VOS}
]
extrainfo:The circuit diagram (b) shows an operational amplifier with an input offset voltage VOS. A capacitor C is used to store a corrective voltage to nullify the effect of the offset voltage. The input nodes are vP and vN, and the output node is vO.

FIGURE 5.64 (a) Modeling the input offset voltage $V_{\text {os }}$ of a differential amplifier, and (b) nulling the effect of $V_{\text {OS }}$ by using a capacitor to store a corrective voltage of equal magnitude but opposite polarity as $V_{O S}$.
image_name:(a)
description:
[
name: VN, type: VoltageSource, value: vN, ports: {Np: VN, Nn: GND}
name: VP, type: VoltageSource, value: vP, ports: {Np: VP, Nn: GND}
name: S1, type: Switch, ports: {N1: VN, N2: VOS}
name: S2, type: Switch, ports: {N1: VP, N2: GND}
name: S3, type: Switch, ports: {N1: VOS, N2: VP}
name: S4, type: Switch, ports: {N1: VOS, N2: vO}
name: S5, type: Switch, ports: {N1: VP, N2: GND}
name: C, type: Capacitor, value: C, ports: {Np: VP, Nn: GND}
name: VOS, type: VoltageSource, value: VOS, ports: {Np: VOS, Nn: VP}
name: OpAmp1, type: OpAmp, ports: {InP: VOS, InN: VP, OutP: vO, OutN: GND}
name: OpAmp2, type: OpAmp, ports: {InP: VOS, InN: VP, OutP: vO, OutN: GND}
]
extrainfo:The circuit diagram (a) shows an operational amplifier with an input offset voltage VOS. A capacitor C is used to store a corrective voltage to nullify the effect of the offset voltage. The input nodes are vP and vN, and the output node is vO. Switches S1 to S5 control the connections during different phases of operation.
image_name:(b)
description:
[
name: VN, type: VoltageSource, value: VN, ports: {Np: vN, Nn: GND}
name: VP, type: VoltageSource, value: VP, ports: {Np: vP, Nn: GND}
name: S1, type: Switch, ports: {N1: VN, N2: VOS}
name: S2, type: Switch, ports: {N1: VP, N2: C}
name: S3, type: Switch, ports: {N1: VOS, N2: C}
name: S4, type: Switch, ports: {N1: VOS, N2: vO}
name: S5, type: Switch, ports: {N1: C, N2: GND}
name: VOS, type: VoltageSource, value: VOS, ports: {Np: VOS, Nn: C}
name: C, type: Capacitor, value: C, ports: {Np: C, Nn: GND}
name: OpAmp, type: OpAmp, ports: {InP: VN, InN: VP, OutP: vO}
]
extrainfo:The circuit diagram (b) shows an operational amplifier with an input offset voltage VOS. A capacitor C is used to store a corrective voltage to nullify the effect of the offset voltage. The input nodes are vP and vN, and the output node is vO. The switches S1 to S5 are used to control the connection of the capacitor and the offset voltage during different phases of operation.

FIGURE 5.65 Switch positions during the (a) autozeroing mode and (b) during the sampling mode.

If necessary, a suitable frequency-compensation network must be switched into the amplifier during this phase.)

- Once we have stored $V_{O S}$ in the capacitor, we open switches $S_{3}$ through $S_{5}$ as in Fig. $5.65 b$ to place the capacitor voltage in series with the internal offset voltage so the two cancel each other out. At the same time, we close $S_{1}$ and $S_{2}$ to reconnect the amplifier to nodes $v_{P}$ and $v_{N}$ for normal operation, such as negativefeedback op amp operation or voltage comparison. The scheme shown is popular especially with voltage comparators, where the circuit is autozeroed before each comparison instance. Should $V_{O S}$ drift with temperature or should $C$ experience leakage between consecutive comparisons, autozeroing is renewed each time.

### Transmission Gates

The $n$ MOSFET switches of Fig. 5.57 will close convincingly only as long as the voltages at the source and drain terminals are sufficiently lower than $V_{H}$. As $v_{1}$ and $v_{2}$ increase, the overdrive voltages are reduced, thus increasing the channel resistances. If $v_{1}$ or $v_{2}$ rise above $V_{H}-V_{t n}$, the FET won't even turn on and the switch will therefore fail to close. If we were to use $p$ MOSFET switches instead, they would work well for $v_{1}$ and $v_{2}$ sufficiently high, but fail to turn on if $v_{1}$ or $v_{2}$ drop below $V_{L}+\left|V_{t p}\right|$, just the opposite of $n$ MOSFETs. The circuit of Fig. 5.66, popularly known as transmission gate, combines the best of both by using a pair of complementary FETs connected in parallel and driven in anti-phase.

When the switch-enable control $E$ is low $\left(E=V_{S S}\right.$ ) and its complement $\bar{E}$ is therefore high $\left(\bar{E}=V_{D D}\right)$, both FETs are off. Driving $E$ high and thus $\bar{E}$ low will tend to turn on both FETs. In fact, so long as $V_{S S}+\left|V_{t p}\right|<v<V_{D D}-V_{t n}$, both FETs are indeed on, ensuring a net transmission-gate resistance $r_{T G}$ that, for the case of matched devices with $k_{n}=k_{p}=k$ and $V_{t n}=-V_{t p}=V_{t}$, is such that

$$
r_{T G}=r_{D S n} / / r_{S D_{p}}=\frac{1}{k v_{O V n}} / / \frac{1}{k v_{O V_{p}}}=\frac{1}{k\left(V_{D D}-v-V_{t}\right)} / / \frac{1}{k\left(v-V_{S S}-V_{t}\right)}
$$

image_name:(a)
description:
[
name: Mn, type: NMOS, ports: {S: VSS, D: VDD, G: E}
name: Mp, type: PMOS, ports: {S: VDD, D: VSS, G: E_bar}
name: v, type: VoltageSource, ports: {Np: v, Nn: GND}
name: CAND, type: Capacitor, value: CAND, ports: {Np: v, Nn: GND}
name: D, type: Inverter, ports: {In: v, Out: E_bar}
]
extrainfo:The circuit diagram shows a transmission gate with NMOS and PMOS transistors controlled by signals E and E_bar. The voltage source v and capacitor CAND are connected to the input of the inverter D, which controls the gate of the PMOS.
image_name:(b)
description:The graph in Figure 5.66(b) is a plot of resistance versus voltage, specifically illustrating the behavior of a transmission gate's resistance (r_{TG}) and the individual channel resistances of the n-channel (r_{DSn}) and p-channel (r_{SDp}) FETs.

1. **Type of Graph and Function:**
- The graph is a resistance versus voltage plot, showing how the resistance of a transmission gate and its components vary with the input voltage, v.

2. **Axes Labels and Units:**
- The horizontal axis represents the voltage, v, with no specific units labeled, but it ranges from V_{SS} to V_{DD}.
- The vertical axis represents resistance in ohms (Ω).

3. **Overall Behavior and Trends:**
- The graph shows three curves: r_{DSn}, r_{SDp}, and r_{TG}.
- r_{DSn} and r_{SDp} are shown as gray curves that intersect, indicating the individual resistances of the n-channel and p-channel FETs, respectively.
- The r_{TG} curve is a flat, black line over the interval from V_{t} to V_{DD} - V_{t}, indicating that the transmission gate resistance remains constant in this range.
- Outside this interval, the r_{TG} curve rises sharply, showing that the transmission gate resistance increases rapidly when the voltage is outside the specified range.

4. **Key Features and Technical Details:**
- The flat region of r_{TG} indicates that the transmission gate's resistance is independent of v within the specified range, consistent with the equation provided in the context.
- The intersections of r_{DSn} and r_{SDp} represent the points where each FET transitions on or off, affecting the overall resistance.

5. **Annotations and Specific Data Points:**
- The graph is annotated with key voltage points: V_{SS}, V_{t}, V_{DD} - V_{t}, and V_{DD}, marking the intervals where the transmission gate's resistance remains constant or changes.
- The flat region of r_{TG} aligns with the theoretical derivation showing its independence from v within the specified range.

FIGURE 5.66 (a) Transmission gate and (b) its zero-current resistance $r_{\text {TG }}$, along with the individual channel resistances $r_{D S n}$ and $r_{\text {SDP }}$.

Expanding and simplifying gives

$$
\begin{equation*}
r_{T G}=\frac{1}{k\left(V_{D D}-V_{S S}-2 V_{t}\right)} \tag{5.91}
\end{equation*}
$$

Under the assumption of matched FETs, $r_{T G}$ is independent of $v$ over the given interval (see Fig. 5.66b). If $v$ is driven outside the above interval, one of the FETs will go off but the other will become even more conductive, thus ensuring a low overall resistance over the entire range $V_{S S}<v<V_{D D}$.

### Stray Capacitances and Charge Injection

Returning to Fig. 5.56, we observe the presence of a number of stray or parasitic capacitances:

- The top and bottom plates of $C$ form themselves stray capacitances with the substrate, here denoted as $C_{t o p}$ and $C_{b t m}$. While $C_{b t m}$ is typically $10 \%-20 \%$ of $C$, $C_{\text {top }}$ is considerably smaller.
- The sides of the gate of the MOSFET switch form the overlap capacitances $C_{O V}$ with the source and drain regions, and these regions form in turn the diffusion capacitances $C_{j}$ with the substrate.
- Additionally, we observe that in order to turn on/off the $n$ MOSFET we need to build up or remove the electron charge $Q_{n}$ in the channel (see Example 3.3). $Q_{n}$ enters/exits the channel through the source and drain regions.

Depending on circuit topology, the stray capacitances may interfere with the intended charge transfer and cause errors. In the switch/capacitor example of Fig. 5.67 the bottom-plate capacitance $C_{b t m}$ plays no role because shorted to ground. Moreover, the overlap and junction capacitances associated with the source region, relabeled as $C_{g s}$ and $C_{s b}$, affect the input source $v_{1}$ but have no impact on the useful capacitance $C$. However, the remaining parasitics do play a role. Specifically, $C_{t o p}$ and $C_{d b}$ are in parallel with $C$, thus yielding a total capacitance $C_{t o t}=C_{d b}+C_{t o p}+C$. Moreover,
image_name:FIGURE 5.67
description:
[
name: M1, type: NMOS, ports: {S: GND, D: VC, G: VG}
name: C, type: Capacitor, value: C, ports: {Np: VC, Nn: GND}
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: VG, Nn: V1}
name: Csb, type: Capacitor, value: Csb, ports: {Np: V1, Nn: GND}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: VG, Nn: VC}
name: Cdb, type: Capacitor, value: Cdb, ports: {Np: VC, Nn: GND}
name: Ctop, type: Capacitor, value: Ctop, ports: {Np: VC, Nn: GND}
name: Cbtm, type: Capacitor, value: Cbtm, ports: {Np: GND, Nn: GND}
name: v1, type: VoltageSource, value: v1, ports: {Np: V1, Nn: GND}
]
extrainfo:The circuit is a simple switched-capacitor network with parasitic capacitances. Cbtm is shorted to ground and does not affect the circuit. Ctop and Cdb are in parallel with the main capacitor C, forming the total capacitance Ctot = C + Ctop + Cdb. Cgd introduces clock feedthrough, and charge injection occurs when M1 is switched.

FIGURE 5.67 Showing the capacitive parasitics of a simple switch-capacitor pair (the capacitances shown in shaded form have no effect in this particular circuit).
$C_{g d}$ couples the clock signal $v_{G}$ to $C_{\text {tot }}$, a phenomenon referred to as clock feedthrough. Additionally, turning the switch off/on causes a fraction $\alpha(0<\alpha<1)$ of the total electron charge $Q_{n}$ in the channel to flow to/from $C_{\text {tot }}$, a phenomenon referred to as charge injection.

We are particularly interested in the trailing edge of $v_{G}$ because at this instant, denoted as $t_{O F F}$, we witness (a) the removal of the charge $Q_{g d}$ from $C_{t o t}$ and (b) the injection of the charge $\alpha Q_{n}$ into $C_{\text {tot }}$ (see Fig. 5.68a). Since the electron charge $Q_{n}$ is negative, the effect is equivalent to removing the positive charge $\alpha\left|Q_{n}\right|$ from $C_{t o t}$, so the two undesired charge transfers reinforce each other. As a result, $v_{O}$ will be affected by an error of $\Delta v_{O} \cong-\left(Q_{g d}+\alpha\left|Q_{n}\right|\right) / C_{\text {tot }}$, where $C_{g d} \ll C_{\text {tot }}$ has been assumed.

One way to reduce the above error is to deliberately introduce an opposing clock feedthrough and charge injection via a dummy transistor $M_{2}$ driven in anti-phase with respect to $M_{1}$ (see Fig. 5.68b). With proper selection of $M_{2}$ 's channel width $W_{2}, M_{2}$ 's feedthrough and injection will approximately cancel out those of $M_{1}$, resulting in a much smaller error in $v_{o}$ (see Problem 5.50). Alternatively, we can implement the switch with a transmission gate and adjust the $W / L$ ratios of the $n$ FET and $p$ FET so as to make their undesirable charge transfers approximately cancel each other out.
image_name:FIGURE 5.68 (a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vo, G: VG}
name: Ggd, type: Capacitor, value: Ggd, ports: {Np: VG, Nn: Vo}
name: Ctot, type: Capacitor, value: Ctot, ports: {Np: Vo, Nn: GND}
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
]
extrainfo:The circuit diagram FIGURE 5.68 (a) shows a charge transfer and charge injection scenario at the instant the NMOS switch M1 is turned off. The capacitor Ggd connects the gate and drain of M1, and Ctot connects the output node Vo to ground. The voltage source VI provides the input voltage.
image_name:FIGURE 5.68 (b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X1, G: VG}
name: M2, type: NMOS, ports: {S: X1, D: VO, G: X2}
name: V1, type: VoltageSource, value: V1, ports: {Np: VI, Nn: GND}
name: D1, type: Diode, ports: {Na: VG, Nc: X2}
name: Ctot, type: Capacitor, value: Ctot, ports: {Np: VO, Nn: GND}
]
extrainfo:The circuit uses two NMOS transistors, M1 and M2, driven in anti-phase to minimize charge injection and feedthrough errors. A diode D1 is used to control the gate of M2. The capacitor Ctot is connected between the output VO and ground.

FIGURE 5.68 (a) Charge transfer $\left(Q_{g d}\right)$ and charge injection $\left(Q_{n}\right)$ at the instant $t_{\text {OFF }}$ in which the $M_{1}$ switch is turned off. (b) Compensation via a second dummy transistor $M_{2}$ driven in anti-phase with respect to $M_{1}$.

### Stray-Insensitive Integrators

With clever design techniques it is often possible to stave off errors due to parasitic capacitances. Figure $5.69 a$ shows a popular modification to the $S C$ integrator of Fig. 5.60 b to render it stray insensitive. Flipping the switches down completely discharges $C_{1}$, while flipping the switches up charges $C_{1}$ to $V_{i}$, so for $V_{i}>0$ charge transfers into the summing junction of the op amp, while for $V_{i}<0$ charge transfers out of the summing node. The situation is similar to that of Fig. 5.60b, so the circuit is an inverting-type SC integrator.

Turning next to Fig. $5.69 b$, we observe that with the switches in the position shown, $C_{1}$ charges to $V_{i}$, and that commutating the switches transfers charge out of the summing junction if $V_{i}>0$, and into the summing junction if $V_{i}<0$, just the opposite of Fig. 5.69a. So, the circuit is a noninverting-type SC integrator, obtained from that of Fig. 5.69a by a mere clock-phase change for the second SPDT switch.
image_name:(a)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: s2, Nn: s1}
name: C2, type: Capacitor, value: C2, ports: {Np: Inv, Nn: Vo}
name: SW1, type: Switch, ports: {N1: w3, N2: s2}
name: SW2, type: Switch, ports: {N1: w1, N2: s1}
name: OpAmp, type: OpAmp, ports: {InP: GND, InN: Inv, Out: Vo}
]
extrainfo:This circuit is an inverting-type switched-capacitor integrator. The switches SW1 and SW2 are controlled by a clock signal fs, allowing C1 to transfer charge to the inverting input of the OpAmp. C2 provides feedback, integrating the input voltage Vi.

image_name:(b)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: fs, Nn: fs}
name: C2, type: Capacitor, value: C2, ports: {Np: Vo, Nn: Inv}
name: OpAmp, type: OpAmp, value: OpAmp, ports: {InP: GND, InN: Inv, Out: Vo}
name: fs, type: Switch, ports: {N1: Vi, N2: fs}
]
extrainfo:This circuit is a non-inverting type switched-capacitor integrator. The switches are controlled by a clock signal fs, allowing C1 to transfer charge to the input of the OpAmp. C2 provides feedback, integrating the input voltage Vi.

(b)

FIGURE 5.69 Stray-insensitive SC integrators: (a) inverting type and (b) noninverting type.

To appreciate the stray insensitivity of the above integrators, consider Fig. 5.70, where the total stray capacitances (top/bottom parasitics plus FET parasitics) associated of the two plates of $C_{1}$ have been denoted as $C_{X}$ and $C_{Y}$. Since $C_{X}$ is switched between ground and the op amp's virtual-ground input, it remains permanently discharged, so the circuit is insensitive to $C_{X} . C_{Y}$ does intervene in the transfer of charge between $V_{i}$ and ground, but without interfering with $C_{1}$, so the circuit is insensitive also to $C_{Y}$. The price for stray insensitivity is a more complex switch system (four FETs instead of two), but this price is certainly worthwhile!
image_name:FIGURE 5.70
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: CY, type: Capacitor, value: CY, ports: {Np: Y, Nn: GND}
name: CX, type: Capacitor, value: CX, ports: {Np: X, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Y, Nn: X}
name: C2, type: Capacitor, value: C2, ports: {Np: Vo, Nn: GND}
name: NMOS1, type: NMOS, ports: {S: GND, D: Vi, G: phi}
name: NMOS2, type: NMOS, ports: {S: GND, D: X, G: phi_bar}
name: OpAmp1, type: OpAmp, value: OpAmp1, ports: {InP: GND, InN: X, OutP: Vo}
]
extrainfo:The circuit is designed to be insensitive to stray capacitance, utilizing a more complex switch system involving four FETs. The op-amp is configured to amplify the input signal, with capacitors CY and CX providing charge transfer without interference.
