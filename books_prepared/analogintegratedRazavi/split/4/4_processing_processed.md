# CHAPTER 4 Differential Amplifiers

The differential amplifier is among the most important circuit inventions, dating back to the vacuum tube era. Offering many useful properties, differential operation has become the de facto choice in todays high-performance analog and mixed-signal circuits.

This chapter deals with the analysis and design of CMOS differential amplifiers. Following a review of single-ended and differential operation, we describe the basic differential pair and analyze both the large-signal and the small-signal behavior. Next, we introduce the concept of common-mode rejection and formulate it for differential amplifiers. We then study differential pairs with diode-connected and current-source loads as well as differential cascode stages. Finally, we describe the Gilbert cell.

## 4.1 ■ Single-Ended and Differential Operation

A "single-ended" signal is defined as one that is measured with respect to a fixed potential, usually the ground [Fig. 4.1(a)]. A differential signal is defined as one that is measured between two nodes that have equal and opposite signal excursions around a fixed potential [Fig. 4.1(b)]. In the strict sense, the two nodes must also exhibit equal impedances to that potential. The "center" potential in differential signaling is called the "common-mode" (CM) level. It is helpful to view the CM level as the bias value of the voltages, i.e., the value in the absence of signals.

The specification of signal swings in a differential system can be confusing. Suppose each singleended output in Fig. 4.1(b) has a peak amplitude of $V_{0}$. Then, the single-ended peak-to-peak swing is $2 V_{0}$ and the differential peak-to-peak swing is $4 V_{0}$. For example, if the voltage at $X$ (with respect to ground) is $V_{0} \cos \omega t+V_{C M}$ and that at $Y$ is $-V_{0} \cos \omega t+V_{C M}$, then the peak-to-peak swing of $V_{X}-V_{Y}$ $\left(=2 V_{0} \cos \omega t\right)$ is $4 V_{0}$. It is therefore not surprising that a circuit with a supply voltage of 1 V can deliver a peak-to-peak differential swing of 1.6 V .

An important advantage of differential operation over single-ended signaling is higher immunity to "environmental" noise. Consider the example depicted in Fig. 4.2, where two adjacent lines in a circuit carry a small, sensitive signal and a large clock waveform. Due to capacitive coupling between the lines, transitions on line $L_{2}$ corrupt the signal on line $L_{1}$. Now suppose, as shown in Fig. 4.2(b), the sensitive signal is distributed as two equal and opposite phases. If the clock line is placed midway between the two, the transitions disturb the differential phases by equal amounts, leaving the difference intact. Since the common-mode level of the two phases is disturbed, but the differential output is not corrupted, we say that this arrangement "rejects" common-mode noise. ${ }^{1}$

image_name:(a)
description:The circuit in Figure 4.1(a) shows a single-ended signal with a resistor Zs connected to a capacitor X2, driven by a voltage source Vin. The NMOS M1 is connected to a load resistor and driven by a signal g1. The circuit is designed to demonstrate signal corruption due to coupling between lines.
image_name:(b)
description:The circuit diagram shows a differential signaling setup with common-mode noise rejection. It uses NMOS transistors M1 and M2 with a clock line placed between two signal lines. Resistors labeled LOAD are connected to a power supply VDD. Capacitors L1, L2, and L3 are used for coupling and decoupling signals. The inverter CK is used to drive the clock line.

Figure 4.2 (a) Corruption of a signal due to coupling; (b) reduction of coupling by differential operation.

Another example of common-mode rejection occurs with noisy supply voltages. In the CS stage of Fig. 4.3(a), if $V_{D D}$ varies by $\Delta V$, then $V_{\text {out }}$ changes by approximately the same amount, i.e., the output is quite susceptible to noise on $V_{D D}$. Now consider the circuit in Fig. 4.3(b). Here, if the circuit is symmetric, noise on $V_{D D}$ affects $V_{X}$ and $V_{Y}$, but not $V_{X}-V_{Y}=V_{\text {out }}$. Thus, the circuit of Fig. 4.3(b) is much more robust in dealing with supply noise.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
]
extrainfo:The circuit is a common-source amplifier with a resistive load, susceptible to noise on the supply voltage VDD. It amplifies the input voltage Vin to produce the output voltage Vout.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vip}
name: M2, type: NMOS, ports: {S: GND, D: Y, G: Vin}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Y}
]
extrainfo:The circuit is a differential amplifier with NMOS transistors M1 and M2. It is designed to reject common-mode noise on VDD. The outputs Vx and Vy are differential, allowing improved noise immunity.
Figure 4.3 Effect of supply noise on (a) a single-ended circuit and (b) a differential circuit.
Thus far, we have seen the importance of employing differential paths for sensitive signals ("victims"). It is also beneficial to employ differential distribution for noisy lines ("aggressors"). For example, suppose the clock signal of Fig. 4.2 is distributed in differential form on two lines (Fig. 4.4). Then, with perfect symmetry, the components coupled from $C K$ and $\overline{C K}$ to the signal line cancel each other.
image_name:Figure 4.4
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vx, G: Vin}
name: LOAD, type: Resistor, value: LOAD, ports: {N1: Vx, N2: CK}
name: L1, type: Inverter, ports: {In: Vx, Out: L1_out}
name: L2, type: Inverter, ports: {In: CK, Out: L2_out}
name: L3, type: Inverter, ports: {In: CK, Out: L3_out}
]
extrainfo:The circuit diagram illustrates a differential clock distribution to reduce coupled noise, utilizing inverters and an NMOS transistor as part of the configuration. The clock signal is distributed in both CK and \overline{CK} lines with inverters L2 and L3.
image_name:Figure 4.4
description:The diagram in Figure 4.4 illustrates a differential circuit configuration involving both differential victims and differential aggressors. The circuit is composed of three main lines labeled as L1, L2, and L3, which are connected to differential clock signals labeled CK and \( \overline{CK} \). These clock signals are fed through inverters before reaching the lines.

1. **Type of Graph and Function:**
- The diagram is a schematic representation of an electronic circuit, specifically focusing on differential signaling.

2. **Axes Labels and Units:**
- As this is a circuit schematic, there are no axes or units typically associated with graphs. Instead, the diagram features components like transistors, capacitors, and inductors, which are standard elements in circuit diagrams.

3. **Overall Behavior and Trends:**
- The circuit is designed to illustrate the concept of differential signaling, where the differential aggressors (clock signals) surround the differential victims (signal path). The idea is to minimize noise coupling by maintaining symmetry in the differential paths.
- The waveform representations on the right side show the expected signal shapes: square waves for the clock signals and a sinusoidal waveform for the victim signal.

4. **Key Features and Technical Details:**
- **Transistor \( M_1 \):** This is a MOSFET transistor connected to the input voltage \( V_{in} \) and ground, controlling the signal path.
- **Load Resistor \( L_{\text{OAP}} \):** This resistor is connected in series with the transistor, affecting the load seen by the transistor.
- **Inductors (L1, L2, L3):** These inductors are part of the differential paths, helping to maintain symmetry and reduce noise coupling.
- **Capacitors:** Placed between the lines, these capacitors are likely used for filtering or coupling purposes.

5. **Annotations and Specific Data Points:**
- The waveforms on the right illustrate the differential nature of the signals. The top and bottom waveforms are square waves, representing the differential clock signals, while the middle waveform is sinusoidal, likely representing the victim signal.
- The differential nature of the signals is intended to demonstrate how noise can be reduced by symmetry in the circuit design, as suggested by the context provided.

#### Example 4.1

If differential victims or differential aggressors improve the overall noise immunity, can we choose differential phases for both victims and aggressors?

#### Solution

Yes, we can. Let us consider the arrangement shown in Fig. 4.5(a), where the differential victims are surrounded by the differential aggressors. Unfortunately, in this case, $V_{\text {out }}^{+}-V_{\text {out }}^{-}$is corrupted because $V_{\text {out }}^{+}$and $V_{\text {out }}^{-}$experience opposite jumps.
image_name:Figure 4.5(a)
description:The circuit in Figure 4.5(a) shows differential victims surrounded by differential aggressors. The outputs Vout+ and Vout- experience opposite voltage jumps, leading to corruption in the differential output.
image_name:Figure 4.5(b)
description:The circuit uses twisted pair routing for noise cancellation, where Vout+ and Vout- are adjacent to CK and CK_bar for half the distance, and then swapped for the other half, effectively canceling out coupling from CK and CK_bar.

Now, suppose we modify the routing as depicted in Fig. 4.5(b), where $V_{\text {out }}^{+}\left(V_{\text {out }}^{-}\right)$is adjacent to $C K(\overline{C K})$ for half of the distance and to $\overline{C K}(C K)$ for the other half. In this case, the couplings from $C K$ and $\overline{C K}$ cancel each other. Interestingly, $V_{\text {out }}^{+}$and $V_{\text {out }}^{-}$are free from the coupling-and so is their difference. This geometry is an example of "twisted pairs."

Another useful property of differential signaling is the increase in maximum achievable voltage swings. In the circuit of Fig. 4.3, for example, the maximum output swing at $X$ or $Y$ is equal to $V_{D D}-\left(V_{G S}-V_{T H}\right)$, whereas for $V_{X}-V_{Y}$, the peak-to-peak swing is equal to $2\left[V_{D D}-\left(V_{G S}-V_{T H}\right)\right]$. Other advantages of differential circuits over their single-ended counterparts include simpler biasing and higher linearity (Chapter 14).

While differential circuits may occupy about twice as much area as single-ended alternatives, in practice this is a minor drawback. The numerous advantages of differential operation by far outweigh the possible increase in the area.

## 4.2 ■ Basic Differential Pair

How do we amplify a differential signal? As suggested by the observations in the previous section, we may incorporate two identical single-ended signal paths to process the two phases [Fig. 4.6(a)]. Here, two differential inputs, $V_{i n 1}$ and $V_{i n 2}$, having a certain CM level, $V_{i n, C M}$, are applied to the gates. The outputs are also differential and swing around the output CM level, $V_{\text {out }, C M}$. Such a circuit indeed offers some of the advantages of differential signaling: high rejection of supply noise, higher output swings, etc. But what happens if $V_{i n 1}$ and $V_{i n 2}$ experience a large common-mode disturbance or simply do not have a well-defined common-mode dc level? As the input CM level, $V_{i n, C M}$, changes, so do the bias currents of $M_{1}$ and $M_{2}$, thus varying both the transconductance of the devices and the output CM level. The variation of the transconductance, in turn, leads to a change in the small-signal gain, while the departure of the output CM level from its ideal value lowers the maximum allowable output swings. For example, as shown in Fig. 4.6(b), if the input CM level is excessively low, the minimum values of $V_{i n 1}$ and $V_{i n 2}$ may in fact turn off $M_{1}$ and $M_{2}$, leading to severe clipping at the output. Thus, it is important that the bias currents of the devices have minimal dependence on the input CM level.
image_name:(a)
description:
[
name: RD1, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RD2, type: Resistor, value: RD, ports: {N1: VDD, N2: Y}
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vin1}
name: M2, type: NMOS, ports: {S: GND, D: Y, G: Vin2}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a differential pair with NMOS transistors M1 and M2. It shows sensitivity to the input common-mode level, which can lead to clipping if the input CM level is too low. The circuit outputs are Vout1 and Vout2, which are affected by the input signals Vin1 and Vin2.
image_name:(b)
description:The diagram labeled "(b)" illustrates the sensitivity of a differential pair circuit to the input common-mode (CM) level. It consists of two main sections: a circuit diagram on the left and a set of waveforms on the right.

Circuit Diagram:
- **Components:**
- Two MOSFETs labeled \(M_1\) and \(M_2\) with their gates connected to inputs \(V_{in1}\) and \(V_{in2}\), respectively.
- Two resistors labeled \(R_D\) connected to the drains of \(M_1\) and \(M_2\), leading to output nodes \(V_{out1}\) and \(V_{out2}\).
- The sources of \(M_1\) and \(M_2\) are grounded.
- The circuit is powered by a supply voltage \(V_{DD}\).

Waveforms:
- **Input Waveforms:**
- \(V_{in1}\) and \(V_{in2}\) are shown as sinusoidal signals around a common-mode level \(V_{in,CM}\). The signals are in anti-phase, meaning when one is at its peak, the other is at its trough.
- **Output Waveforms:**
- \(V_{out1}\) and \(V_{out2}\) are shown as sinusoidal signals around a common-mode level \(V_{out,CM}\).
- \(V_{out1}\) and \(V_{out2}\) maintain their sinusoidal shape but are affected by clipping due to the input CM level.

Behavior and Sensitivity:
- The waveforms illustrate the impact of the input CM level on the operation of the MOSFETs.
- If the input CM level is too low, \(M_1\) and \(M_2\) can turn off, leading to output clipping. This is depicted by the areas where the waveforms flatten at the bottom.
- Clipping occurs when the input signal amplitude is too high relative to the CM level, causing the transistors to turn off during part of the cycle.

Key Features:
- The diagram emphasizes the importance of maintaining an appropriate input CM level to prevent distortion in the output signals.
- Annotations indicate where \(M_1\) and \(M_2\) turn off, highlighting the sensitivity to low CM levels.

Figure 4.6 (a) Simple differential circuit; (b) illustration of sensitivity to the input common-mode level.
image_name:Figure 4.7 Basic differential pair.
description:
[
name: RD1, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RD2, type: Resistor, value: RD, ports: {N1: VDD, N2: Y}
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin1}
name: M2, type: NMOS, ports: {S: P, D: Y, G: Vin2}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit shown is a basic differential pair with a current source ISS. It maintains constant current through the differential pair regardless of the input common-mode voltage. The resistors RD1 and RD2 are equal, ensuring symmetrical operation. The output nodes are Vout1 and Vout2. The circuit aims to stabilize the output common-mode level and is less sensitive to variations in input common-mode level.

A simple modification can resolve the above issue. Shown in Fig. 4.7, the "differential pair" ${ }^{2}$ employs a current source $I_{S S}$ to make $I_{D 1}+I_{D 2}$ independent of $V_{i n, C M}$. Thus, if $V_{i n 1}=V_{i n 2}$, the bias current of

each transistor equals $I_{S S} / 2$ and the output common-mode level is $V_{D D}-R_{D} I_{S S} / 2$. It is instructive to study the large-signal behavior of the circuit for both differential and common-mode input variations. In the large-signal study, we neglect channel-length modulation and body effect.

### 4.2.1 Qualitative Analysis

Let us assume that in Fig. 4.7, $V_{i n 1}-V_{i n 2}$ varies from $-\infty$ to $+\infty$. If $V_{i n 1}$ is much more negative than $V_{\text {in2 }}, M_{1}$ is off, $M_{2}$ is on, and $I_{D 2}=I_{S S}$. Thus, $V_{\text {out } 1}=V_{D D}$ and $V_{\text {out } 2}=V_{D D}-R_{D} I_{S S}$. As $V_{i n 1}$ is brought closer to $V_{i n 2}, M_{1}$ gradually turns on, drawing a fraction of $I_{S S}$ from $R_{D 1}$ and hence lowering $V_{\text {out } 1}$. Since $I_{D 1}+I_{D 2}=I_{S S}$, the drain current of $M_{2}$ falls and $V_{\text {out } 2}$ rises. As shown in Fig. 4.8(a), for $V_{\text {in } 1}=V_{\text {in } 2}$, we have $V_{\text {out } 1}=V_{\text {out } 2}=V_{D D}-R_{D} I_{S S} / 2$, which is the output CM level. As $V_{\text {in } 1}$ becomes more positive than $V_{\text {in2 }}, M_{1}$ carries a greater current than does $M_{2}$ and $V_{\text {out } 1}$ drops below $V_{\text {out } 2}$. For sufficiently large $V_{i n 1}-V_{i n 2}, M_{1}$ "hogs" all of $I_{S S}$, turning $M_{2}$ off. As a result, $V_{\text {out } 1}=V_{D D}-R_{D} I_{S S}$ and $V_{\text {out } 2}=V_{D D}$. Figure 4.8 also plots $V_{\text {out } 1}-V_{\text {out } 2}$ versus $V_{\text {in } 1}-V_{\text {in } 2}$. Note that the circuit contains three differential quantities: $V_{i n 1}-V_{\text {in } 2}, V_{\text {out } 1}-V_{\text {out } 2}$, and $I_{D 1}-I_{D 2}$.
image_name:Figure 4.8 Differential input-output characteristics of a differential pair.(a)
description:The graph labeled "(a)" in Figure 4.8 is a plot representing the differential input-output characteristics of a differential pair. This graph is a type of voltage transfer characteristic graph.

Axes Labels and Units:
- **Horizontal Axis (X-axis):** Represents the differential input voltage \( V_{in1} - V_{in2} \) with no specific units marked, as it is generally understood to be in volts.
- **Vertical Axis (Y-axis):** Represents the output voltages \( V_{out1} \) and \( V_{out2} \), also in volts.

Overall Behavior and Trends:
- The graph displays two curves indicating the behavior of \( V_{out1} \) and \( V_{out2} \) as \( V_{in1} - V_{in2} \) changes.
- The curve for \( V_{out1} \) starts at \( V_{DD} - R_D I_{SS} \) for large negative \( V_{in1} - V_{in2} \) and rises to \( V_{DD} \) for large positive \( V_{in1} - V_{in2} \).
- Conversely, the curve for \( V_{out2} \) starts at \( V_{DD} \) for large negative \( V_{in1} - V_{in2} \) and falls to \( V_{DD} - R_D I_{SS} \) for large positive \( V_{in1} - V_{in2} \).
- Both curves are symmetric about the center point \( V_{out,CM} = V_{DD} - \frac{R_D I_{SS}}{2} \), which is the common-mode output voltage.

Key Features and Technical Details:
- The maximum output voltage for \( V_{out1} \) is \( V_{DD} \), and the minimum is \( V_{DD} - R_D I_{SS} \).
- The crossover point, where \( V_{in1} = V_{in2} \), is at \( V_{out,CM} = V_{DD} - \frac{R_D I_{SS}}{2} \).
- The graph demonstrates that the output voltages \( V_{out1} \) and \( V_{out2} \) are inversely related as the input differential voltage varies.

Annotations and Specific Data Points:
- The graph includes annotations for critical values such as \( V_{DD} \), \( V_{out,CM} \), and \( V_{DD} - R_D I_{SS} \), providing reference points for understanding the voltage levels.
- The symmetry of the curves around the common-mode voltage highlights the balanced nature of the differential pairs operation.

This graph effectively illustrates the relationship between differential input voltage and the resulting differential output voltages in a differential pair circuit, highlighting the linear and symmetrical response around the common-mode point.
image_name:Figure 4.8 Differential input-output characteristics of a differential pair.(b)
description:The graph labeled "(b)" in Figure 4.8 is a plot illustrating the differential input-output characteristics of a differential pair. This specific graph is a voltage transfer characteristic curve, showing the relationship between the differential output voltage \( V_{\text{out}1} - V_{\text{out}2} \) and the differential input voltage \( V_{\text{in}1} - V_{\text{in}2} \).

Axes Labels and Units:
- **Horizontal Axis (X-axis):** Represents the differential input voltage \( V_{\text{in}1} - V_{\text{in}2} \).
- **Vertical Axis (Y-axis):** Represents the differential output voltage \( V_{\text{out}1} - V_{\text{out}2} \).
- The units for both axes are typically in volts (V), although specific units arent marked on the diagram.

Overall Behavior and Trends:
- The curve is S-shaped, indicating a nonlinear relationship between the input and output differential voltages.
- As \( V_{\text{in}1} - V_{\text{in}2} \) increases from negative to positive values, the differential output voltage \( V_{\text{out}1} - V_{\text{out}2} \) transitions from \( -R_D I_{SS} \) to \( +R_D I_{SS} \).
- When \( V_{\text{in}1} = V_{\text{in}2} \), the differential output is zero, indicating symmetry around this point.

Key Features and Technical Details:
- The graph shows saturation regions where the output voltage levels off at \( +R_D I_{SS} \) and \( -R_D I_{SS} \).
- The slope of the curve is steepest around the origin, indicating maximum small-signal gain at \( V_{\text{in}1} = V_{\text{in}2} \).

Annotations and Specific Data Points:
- The curve is centered around the origin, with the zero crossing at \( V_{\text{in}1} = V_{\text{in}2} \).
- The saturation points are marked at \( +R_D I_{SS} \) and \( -R_D I_{SS} \), representing the limits of the differential output voltage.

The foregoing analysis reveals two important attributes of the differential pair. First, the maximum and minimum levels at the output are well-defined ( $V_{D D}$ and $V_{D D}-R_{D} I_{S S}$, respectively) and independent of the input CM level. Second, as proved later, the small-signal gain (the slope of $V_{\text {out } 1}-V_{\text {out } 2}$ versus $V_{i n 1}-V_{i n 2}$ ) is maximum for $V_{i n 1}=V_{i n 2}$, gradually falling to zero as $\left|V_{i n 1}-V_{i n 2}\right|$ increases. In other words, the circuit becomes more nonlinear as the input voltage swing increases. For $V_{i n 1}=V_{i n 2}$, we say that the circuit is in "equilibrium."

Now let us consider the common-mode behavior of the circuit. As mentioned earlier, the role of the tail current source is to suppress the effect of input CM level variations on the operation of $M_{1}$ and $M_{2}$ and the output level. Does this mean that $V_{i n, C M}$ can assume arbitrarily low or high values? To answer this question, we set $V_{i n 1}=V_{i n 2}=V_{i n, C M}$ and vary $V_{i n, C M}$ from 0 to $V_{D D}$. Figure 4.9(a) shows the circuit with $I_{S S}$ implemented by an NFET. Note that the symmetry of the pair requires that $V_{\text {out } 1}=V_{\text {out } 2}$.

What happens if $V_{i n, C M}=0$ ? Since the gate potential of $M_{1}$ and $M_{2}$ is not more positive than their source potential, both devices are off, yielding $I_{D 3}=0$. This indicates that $M_{3}$ operates in the deep triode region because $V_{b}$ is high enough to create an inversion layer in the transistor. With $I_{D 1}=I_{D 2}=0$, the circuit is incapable of signal amplification, $V_{\text {out } 1}=V_{\text {out } 2}=V_{D D}$, and $V_{P}=0$.

Now suppose $V_{i n, C M}$ becomes more positive. Modeling $M_{3}$ by a resistor as in Fig. 4.9(b), we note that $M_{1}$ and $M_{2}$ turn on if $V_{i n, C M} \geq V_{T H}$. Beyond this point, $I_{D 1}$ and $I_{D 2}$ continue to increase, and $V_{P}$ also rises [Fig. 4.9(c)]. In a sense, $M_{1}$ and $M_{2}$ constitute a source follower, forcing $V_{P}$ to track $V_{i n, C M}$. For a sufficiently high $V_{i n, C M}$, the drain-source voltage of $M_{3}$ exceeds $V_{G S 3}-V_{T H 3}$, allowing the device to operate in saturation. The total current through $M_{1}$ and $M_{2}$ then remains constant. We conclude that for proper operation, $V_{i n, C M} \geq V_{G S 1}+\left(V_{G S 3}-V_{T H 3}\right)$.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin,CM}
name: M2, type: NMOS, ports: {S: P, D: Y, G: Vin,CM}
name: M3, type: NMOS, ports: {S: GND, D: P, G: Vb}
name: RD1, type: Resistor, value: RD, ports: {N1: X, N2: VDD}
name: RD2, type: Resistor, value: RD, ports: {N1: Y, N2: VDD}
]
extrainfo:The circuit is a differential pair sensing an input common-mode change. M1 and M2 form a source follower configuration. M3 operates in saturation to maintain constant current through M1 and M2 for proper operation. The circuit behavior is influenced by Vin,CM, Vout1, Vout2, and Vb.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin,CM}
name: M2, type: NMOS, ports: {S: P, D: Y, G: Vin,CM}
name: RD1, type: Resistor, value: RD, ports: {N1: X, N2: VDD}
name: RD2, type: Resistor, value: RD, ports: {N1: Y, N2: VDD}
name: Ron3, type: Resistor, value: Ron3, ports: {N1: P, N2: GND}
]
extrainfo:The circuit diagram (b) is a differential pair with NMOS transistors M1 and M2, and a common-mode feedback transistor M3. The resistors RD are connected to VDD, providing load resistance for the drains of M1 and M2. The resistor Ron3 is connected between the common source node of M1 and M2 and ground, modeling the on-resistance of M3 in the triode region.
image_name:(c)
description:The graph in Figure 4.9(c) consists of three separate plots, each depicting different characteristics related to the common-mode input voltage, \( V_{in,CM} \).

1. **First Plot (Left):**
- **Type:** Current vs. Voltage Graph
- **Axes:**
- **X-axis:** \( V_{in,CM} \) (Common-mode input voltage)
- **Y-axis:** \( I_{D1}, I_{D2} \) (Drain currents of transistors \( M_1 \) and \( M_2 \))
- **Behavior:**
- The plot shows an initial increase in the drain currents as \( V_{in,CM} \) rises, starting from zero and increasing sharply after a threshold voltage \( V_{TH1} \).
- The current then plateaus, indicating saturation.
- **Key Features:**
- A vertical dashed line marks the threshold voltage \( V_{GS1} + V_{GS3} - V_{TH3} \), indicating where the device transitions to saturation.

2. **Second Plot (Middle):**
- **Type:** Voltage vs. Voltage Graph
- **Axes:**
- **X-axis:** \( V_{in,CM} \) (Common-mode input voltage)
- **Y-axis:** \( V_{P} \) (Voltage at node P)
- **Behavior:**
- The plot shows a linear relationship, with \( V_{P} \) increasing linearly as \( V_{in,CM} \) increases.
- **Key Features:**
- The line starts from a point just after \( V_{TH1} \), indicating the beginning of the linear tracking of \( V_{P} \) with \( V_{in,CM} \).

3. **Third Plot (Right):**
- **Type:** Voltage vs. Voltage Graph
- **Axes:**
- **X-axis:** \( V_{in,CM} \) (Common-mode input voltage)
- **Y-axis:** \( V_{out1}, V_{out2} \) (Output voltages)
- **Behavior:**
- The plot shows a constant output voltage \( V_{DD} \) initially, which then decreases sharply after \( V_{TH1} \), and stabilizes to a lower constant value \( V_{DD} - \frac{I_{SS}}{2}R_D \).
- **Key Features:**
- Two vertical dashed lines mark the critical voltages \( V_{TH1} \) and \( V_{GS1} + V_{GS3} - V_{TH3} \), indicating transitions in the output behavior.

Overall, these plots illustrate the behavior of the differential pair as it responds to changes in the common-mode input voltage, showing how the currents and voltages adjust with respect to the input.

Figure 4.9 (a) Differential pair sensing an input common-mode change; (b) equivalent circuit if $M_{3}$ operates in the deep triode region; (c) common-mode input-output characteristics.

What happens if $V_{\text {in }, C M}$ rises further? Since $V_{\text {out } 1}$ and $V_{\text {out } 2}$ are relatively constant, we expect that $M_{1}$ and $M_{2}$ enter the triode region if $V_{\text {in,CM }}>V_{\text {out } 1}+V_{T H}=V_{D D}-R_{D} I_{S S} / 2+V_{T H}$. This sets an upper limit on the input CM level. In summary, the allowable value of $V_{i n, C M}$ is bounded as follows:

$$
\begin{equation*}
V_{G S 1}+\left(V_{G S 3}-V_{T H 3}\right) \leq V_{i n, C M} \leq \min \left[V_{D D}-R_{D} \frac{I_{S S}}{2}+V_{T H}, V_{D D}\right] \tag{4.1}
\end{equation*}
$$

Beyond the upper bound, the CM characteristics of Fig. 4.9(c) do not change, but the differential gain drops. ${ }^{3}$

#### Example 4.2

Sketch the small-signal differential gain of a differential pair as a function of the input CM level.
image_name:Figure 4.10
description:The graph in Figure 4.10 is a plot of the small-signal differential gain \( A_V \) of a differential pair as a function of the input common-mode voltage \( V_{in,CM} \). The graph is a typical representation of gain behavior against varying input common-mode levels.

Axes Labels and Units:
- **Horizontal Axis (x-axis):** Represents the input common-mode voltage \( V_{in,CM} \).
- **Vertical Axis (y-axis):** Represents the absolute value of the differential gain \( |A_V| \).

Overall Behavior and Trends:
- **Initial Increase:** The gain \( A_V \) begins to increase as \( V_{in,CM} \) exceeds a threshold voltage \( V_{TH} \).
- **Constant Region:** After reaching a certain level \( V_1 \), where the tail current source enters saturation, the gain remains relatively constant.
- **Decrease:** As \( V_{in,CM} \) continues to increase and reaches \( V_2 \), the gain starts to decrease, indicating the input transistors have entered the triode region.

Key Features and Technical Details:
- **Threshold Voltage \( V_{TH} \):** Marks the point where gain begins to rise.
- **Saturation Point \( V_1 \):** Indicates where the gain stabilizes in a flat plateau.
- **Triode Region Entry \( V_2 \):** Marks the beginning of the gains decline.

Annotations and Specific Data Points:
- **\( V_{TH} \), \( V_1 \), and \( V_2 \):** These points are annotated on the graph with dashed vertical lines, highlighting key transitions in the gain behavior.

This graph effectively illustrates how the differential gain of a pair varies with changes in the common-mode input voltage, showing distinct regions of operation: initial increase, constant gain, and eventual decrease.

#### Solution

As shown in Fig. 4.10, the gain begins to increase as $V_{i n, C M}$ exceeds $V_{T H}$. After the tail current source enters saturation ( $V_{i n, C M}=V_{1}$ ), the gain remains relatively constant. Finally, if $V_{i n, C M}$ is so high that the input transistors enter the triode region $\left(V_{i n, C M}=V_{2}\right)$, the gain begins to fall.

[^17]With our understanding of differential and common-mode behavior of the differential pair, we can now answer another important question: How large can the output voltage swings of a differential pair be? Suppose the circuit is biased with input and output bias levels $V_{i n, C M}$ and $V_{o u t, C M}$, respectively, and $V_{\text {in }, C M}<V_{\text {out }, C M}$. Also, assume that the voltage gain is high, that is, the input swing is much less than the output swing. As illustrated in Fig. 4.11, for $M_{1}$ and $M_{2}$ to be saturated, each output can go as high as $V_{D D}$ but as low as approximately $V_{i n, C M}-V_{T H}$. In other words, the higher the input CM level, the smaller the allowable output swings. For this reason, it is desirable to choose a relatively low $V_{i n, C M}$, but, of course, no less than $V_{G S 1}+\left(V_{G S 3}-V_{T H 3}\right)$. Such a choice affords a single-ended peak-to-peak output swing of $V_{D D}-\left(V_{G S 1}-V_{T H 1}\right)-\left(V_{G S 3}-V_{T H 3}\right)$ (why?). The reader is encouraged to repeat this analysis if the voltage gain is around unity.
image_name:Figure 4.11
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin1}
name: M2, type: NMOS, ports: {S: P, D: Y, G: Vin2}
name: M3, type: NMOS, ports: {S: GND, D: P, G: Vb}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Y}
]
extrainfo:This circuit is a differential pair with NMOS transistors M1, M2, and a current source M3. The resistors RD are used as load resistors. The input signals are Vin1 and Vin2, and the bias voltage is Vb. The circuit is designed to analyze the maximum allowable output swings in a differential pair.
image_name:Vin1 Vin2
description:The graph labeled "Vin1 Vin2" represents a time-domain waveform illustrating the behavior of a differential pair circuit. The graph is divided into two main sections: the schematic of the differential pair on the left and the waveform on the right.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform that shows the input and output voltages of a differential pair circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents time (t), though the specific units are not labeled.
- The vertical axis represents voltage, but specific units are not provided. It shows the common-mode input voltage (Vin,CM), input voltages (Vin1 and Vin2), and output voltages (Vout,CM, Vx, Vy).

3. **Overall Behavior and Trends:**
- The input voltages Vin1 and Vin2 are shown as sinusoidal waveforms that are 180 degrees out of phase with each other, indicating a differential input signal.
- The output voltages Vx and Vy also exhibit sinusoidal behavior, with the waveform of Vx being in phase with Vin1 and Vy being in phase with Vin2.
- The common-mode output voltage (Vout,CM) is depicted as a reference level between Vx and Vy.

4. **Key Features and Technical Details:**
- The graph shows the maximum allowable output swings with reference to the threshold voltage VTH1.
- The output voltages Vx and Vy oscillate around the common-mode output voltage, with the peak-to-peak amplitude limited by the threshold voltage.
- The waveform suggests that the differential pair is operating within its linear region, as the output swings are symmetric around the common-mode level.

5. **Annotations and Specific Data Points:**
- The threshold voltage VTH1 is marked as a vertical distance between the common-mode level and the peak of the output waveform.
- The graph emphasizes the relationship between the input common-mode voltage and the allowable output swings, aligning with the context provided about maximizing output swings while maintaining a low input common-mode voltage.
image_name:Vout,CM
description:The graph titled "Vout,CM" is a time-domain waveform that illustrates the behavior of output voltages in a differential pair circuit. The x-axis represents time \(t\), while the y-axis represents voltage levels, specifically the common-mode output voltage \(V_{out,CM}\) along with individual output voltages \(V_X\) and \(V_Y\).

Axes Labels and Units:
- **X-axis:** Time \(t\) (no specific units are provided, but typically in seconds or milliseconds in circuit analysis).
- **Y-axis:** Voltage levels (units in volts).

Overall Behavior and Trends:
The graph shows two sinusoidal waveforms, \(V_X\) and \(V_Y\), which are 180 degrees out of phase with each other. These waveforms represent the differential output voltages of the circuit. The common-mode voltage \(V_{out,CM}\) is depicted as a horizontal dashed line, indicating a constant voltage level around which the sinusoidal waveforms oscillate.

Key Features and Technical Details:
- **Sinusoidal Waveforms:** The waveforms \(V_X\) and \(V_Y\) oscillate symmetrically around the common-mode voltage \(V_{out,CM}\).
- **Amplitude and Phase:** Both \(V_X\) and \(V_Y\) have the same amplitude but are out of phase, which is typical for a differential pair output.
- **Threshold Voltage:** The graph includes a reference line labeled \(V_{TH1}\), indicating a threshold voltage level. This threshold is crucial for analyzing the maximum allowable output swings.

Annotations and Specific Data Points:
- **Common-Mode Voltage \(V_{out,CM}\):** Shown as a horizontal dashed line.
- **Threshold Voltage \(V_{TH1}\):** Displayed as a vertical distance between \(V_X\) and \(V_Y\), indicating the maximum allowable deviation from the common-mode voltage before reaching the threshold.

This graph effectively illustrates how the differential pairs output voltages oscillate around a common-mode level, with the threshold voltage \(V_{TH1}\) being a critical parameter for determining the output swing limits in this context.

Figure 4.11 Maximum allowable output swings in a differential pair.

#### Example 4.3

Compare the maximum output voltage swings provided by a CS stage and a differential pair.

#### Solution

Recall from Chapter 3 that a CS stage (with resistive load) allows an output swing of $V_{D D}$ minus one overdrive $\left(V_{D D}-V_{D, s a t}\right)$. As seen above, with proper choice of the input CM level, a differential pair provides a maximum output swing of $V_{D D}$ minus two overdrives (single-ended) or $2 V_{D D}$ minus four overdrives (differential) $\left(2 V_{D D}-4 V_{D, s a t}\right)$, which is typically quite a lot larger than $V_{D D}-V_{D, s a t}$.

### 4.2.2 Quantitative Analysis

In this section, we quantify both large-signal and small-signal characteristics of MOS differential pairs. We begin with large-signal analysis to arrive at expressions for the plots shown in Fig. 4.8.

Large-Signal Behavior Consider the differential pair shown in Fig. 4.12. Our objective is to determine $V_{\text {out } 1}-V_{\text {out } 2}$ as a function of $V_{\text {in } 1}-V_{\text {in } 2}$. We have $V_{\text {out } 1}=V_{D D}-R_{D 1} I_{D 1}$ and $V_{\text {out } 2}=V_{D D}-R_{D 2} I_{D 2}$, that is, $V_{\text {out } 1}-$ $V_{\text {out } 2}=R_{D 2} I_{D 2}-R_{D 1} I_{D 1}=R_{D}\left(I_{D 2}-I_{D 1}\right)$ if $R_{D 1}=R_{D 2}=R_{D}$. Thus, we simply calculate $I_{D 1}$ and $I_{D 2}$ in terms of $V_{i n 1}$ and $V_{i n 2}$, assuming the circuit is symmetric, $M_{1}$ and $M_{2}$ are saturated, and $\lambda=0$. Since the voltage at node $P$ is equal to $V_{i n 1}-V_{G S 1}$ and $V_{i n 2}-V_{G S 2}$,

$$
\begin{equation*}
V_{i n 1}-V_{i n 2}=V_{G S 1}-V_{G S 2} \tag{4.2}
\end{equation*}
$$

image_name:Figure 4.12 Differential pair
description:
[
name: M1, type: NMOS, ports: {S: P, D: Vout1, G: Vin1}
name: M2, type: NMOS, ports: {S: P, D: Vout2, G: Vin2}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: Vout1}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: Vout2}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: P, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:This is a differential pair circuit with two NMOS transistors M1 and M2. The current source Iss provides the bias current. The resistors RD1 and RD2 are connected to the drains of M1 and M2, respectively, and the power supply VDD is connected to the top of these resistors. The circuit is designed to amplify the difference between Vin1 and Vin2, producing outputs Vout1 and Vout2.

For a square-law device, we have

$$
\begin{equation*}
\left(V_{G S}-V_{T H}\right)^{2}=\frac{I_{D}}{\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}} \tag{4.3}
\end{equation*}
$$

and, therefore,

$$
\begin{equation*}
V_{G S}=\sqrt{\frac{2 I_{D}}{\mu_{n} C_{o x} \frac{W}{L}}}+V_{T H} \tag{4.4}
\end{equation*}
$$

It follows from (4.2) and (4.4) that

$$
\begin{equation*}
V_{i n 1}-V_{i n 2}=\sqrt{\frac{2 I_{D 1}}{\mu_{n} C_{o x} \frac{W}{L}}}-\sqrt{\frac{2 I_{D 2}}{\mu_{n} C_{o x} \frac{W}{L}}} \tag{4.5}
\end{equation*}
$$

We wish to calculate the differential output current, $I_{D 1}-I_{D 2}$. Squaring the two sides of (4.5) and recognizing that $I_{D 1}+I_{D 2}=I_{S S}$, we obtain

$$
\begin{equation*}
\left(V_{i n 1}-V_{i n 2}\right)^{2}=\frac{2}{\mu_{n} C_{o x} \frac{W}{L}}\left(I_{S S}-2 \sqrt{I_{D 1} I_{D 2}}\right) \tag{4.6}
\end{equation*}
$$

That is,

$$
\begin{equation*}
\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{i n 1}-V_{i n 2}\right)^{2}-I_{S S}=-2 \sqrt{I_{D 1} I_{D 2}} \tag{4.7}
\end{equation*}
$$

Squaring the two sides again and noting that $4 I_{D 1} I_{D 2}=\left(I_{D 1}+I_{D 2}\right)^{2}-\left(I_{D 1}-I_{D 2}\right)^{2}=I_{S S}^{2}-\left(I_{D 1}-I_{D 2}\right)^{2}$, we arrive at

$$
\begin{equation*}
\left(I_{D 1}-I_{D 2}\right)^{2}=-\frac{1}{4}\left(\mu_{n} C_{o x} \frac{W}{L}\right)^{2}\left(V_{i n 1}-V_{i n 2}\right)^{4}+I_{S S} \mu_{n} C_{o x} \frac{W}{L}\left(V_{i n 1}-V_{i n 2}\right)^{2} \tag{4.8}
\end{equation*}
$$

Thus,

$$
\begin{align*}
I_{D 1}-I_{D 2} & =\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{i n 1}-V_{i n 2}\right) \sqrt{\frac{4 I_{S S}}{\mu_{n} C_{o x} \frac{W}{L}}-\left(V_{i n 1}-V_{i n 2}\right)^{2}}  \tag{4.9}\\
& =\sqrt{\mu_{n} C_{o x} \frac{W}{L} I_{S S}\left(V_{i n 1}-V_{i n 2}\right) \sqrt{1-\frac{\mu_{n} C_{o x}(W / L)}{4 I_{S S}}\left(V_{i n 1}-V_{i n 2}\right)^{2}}} \tag{4.10}
\end{align*}
$$

We can say that $M_{1}, M_{2}$, and the tail operate as a voltage-dependent current source producing $I_{D 1}-I_{D 2}$ according to the above large-signal characteristics. As expected, $I_{D 1}-I_{D 2}$ is an odd function of $V_{i n 1}-V_{i n 2}$,
falling to zero for $V_{i n 1}=V_{i n 2}$. As $\left|V_{i n 1}-V_{i n 2}\right|$ increases from zero, $\left|I_{D 1}-I_{D 2}\right|$ increases because the factor preceding the square root rises more rapidly than the argument in the square root drops. ${ }^{4}$

Before examining (4.9) further, it is instructive to calculate the slope of the characteristic, i.e., the equivalent $G_{m}$ of $M_{1}$ and $M_{2}$. Denoting the differential quantities $I_{D 1}-I_{D 2}$ and $V_{i n 1}-V_{i n 2}$ by $\Delta I_{D}$ and $\Delta V_{i n}$, respectively, the reader can show that

$$
\begin{equation*}
\frac{\partial \Delta I_{D}}{\partial \Delta V_{i n}}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L} \frac{\frac{4 I_{S S}}{\mu_{n} C_{o x} W / L}-2 \Delta V_{i n}^{2}}{\sqrt{\frac{4 I_{S S}}{\mu_{n} C_{o x} W / L}-\Delta V_{i n}^{2}}} \tag{4.11}
\end{equation*}
$$

For $\Delta V_{i n}=0, G_{m}$ is maximum (why?) and equal to $\sqrt{\mu_{n} C_{o x}(W / L) I_{S S}}$. Moreover, since $V_{\text {out } 1}-V_{\text {out } 2}=$ $R_{D} \Delta I=-R_{D} G_{m} \Delta V_{i n}$, we can write the small-signal differential voltage gain of the circuit in the equilibrium condition as

$$
\begin{equation*}
\left|A_{v}\right|=\sqrt{\mu_{n} C_{o x} \frac{W}{L} I_{S S}} R_{D} \tag{4.12}
\end{equation*}
$$

Since each transistor carries a bias current of $I_{S S} / 2$ in this condition, the factor $\sqrt{\mu_{m} C_{o x}(W / L) I_{S S}}$ is in fact the same as the transconductance of each device, that is, $\left|A_{v}\right|=g_{m} R_{D}$. Equation (4.11) also suggests that $G_{m}$ falls to zero for $\Delta V_{i n}=\sqrt{2 I_{S S} /\left(\mu_{n} C_{o x} W / L\right)}$. As we will see below, this value of $\Delta V_{i n}$ plays an important role in the operation of the circuit.

Let us now examine Eq. (4.9) more closely. If $\left(V_{i n 1}-V_{i n 2}\right)^{2} \ll 4 I_{S S} /\left[\mu_{n} C_{o x}(W / L)\right]$, then

$$
\begin{equation*}
I_{D 1}-I_{D 2}=\sqrt{\mu_{n} C_{o x} \frac{W}{L} I_{S S}}\left(V_{i n 1}-V_{i n 2}\right) \tag{4.13}
\end{equation*}
$$

which yields the same equilibrium $G_{m}$ as that obtained above.
But what happens for larger values of $\left|V_{i n 1}-V_{i n 2}\right|$ ? It appears that the argument in the square root drops to zero for $\Delta V_{i n}=\sqrt{4 I_{S S} /\left(\mu_{n} C_{o x} W / L\right)}$ and $\Delta I_{D}$ crosses zero at two different values of $\Delta V_{i n}$, an effect not predicted by our qualitative analysis in Fig. 4.8. This conclusion, however, is incorrect. To understand why, recall that (4.9) was derived with the assumption that both $M_{1}$ and $M_{2}$ are on. In reality, as $\Delta V_{i n}$ exceeds a limit, one transistor carries the entire $I_{S S}$, turning off the other. ${ }^{5}$ Denoting this value by $\Delta V_{i n 1}$, we have $I_{D 1}=I_{S S}$ and $\Delta V_{i n 1}=V_{G S 1}-V_{T H}$ because $M_{2}$ is nearly off. It follows that

$$
\begin{equation*}
\Delta V_{i n 1}=\sqrt{\frac{2 I_{S S}}{\mu_{n} C_{o x} \frac{W}{L}}} \tag{4.14}
\end{equation*}
$$

For $\Delta V_{i n}>\Delta V_{i n 1}, M_{2}$ is off and (4.9) and (4.10) do not hold. As mentioned above, $G_{m}$ falls to zero for $\Delta V_{i n}=\Delta V_{i n 1}$. Figure 4.13 plots the behavior.

#### Example 4.4

Plot the output currents of a differential pair versus $\Delta V_{i n}$ as the device width and the tail current vary.

#### Solution

Consider the characteristic shown in Fig. 4.14(a). As $W / L$ increases, $\Delta V_{i n 1}$ decreases, narrowing the input range across which both devices are on [Fig. 4.14(b)]. As $I_{S S}$ increases, both the input range and the output current swing increase [Fig. 4.14(c)]. Intuitively, we expect the circuit to become more linear as $I_{S S}$ increases or $W / L$ decreases.

image_name:(a)
description:The graph labeled "(a)" is a plot of drain currents \(I_{D1}\) and \(I_{D2}\) versus the differential input voltage \(\Delta V_{in}\) for a differential pair. The x-axis represents the differential input voltage \(\Delta V_{in}\), marked with key points \(-\Delta V_{in1}\) and \(+\Delta V_{in1}\), while the y-axis represents the drain currents \(I_{D1}\) and \(I_{D2}\).

**Type of Graph and Function:**
- The graph is a characteristic curve showing the relationship between input voltage and output currents in a differential pair circuit.

**Axes Labels and Units:**
- X-axis: \(\Delta V_{in}\) (differential input voltage)
- Y-axis: \(I_{D1}\) and \(I_{D2}\) (drain currents)

**Overall Behavior and Trends:**
- As the input voltage \(\Delta V_{in}\) increases from negative to positive, the current \(I_{D1}\) increases while \(I_{D2}\) decreases symmetrically.
- The graph shows a crossover point at \(\Delta V_{in} = 0\), where both currents are equal.
- The curves are S-shaped, indicating a smooth transition between states.

**Key Features and Technical Details:**
- The currents \(I_{D1}\) and \(I_{D2}\) are equal at \(\Delta V_{in} = 0\), which is the point of symmetry for the differential pair.
- The input voltage range \([-\Delta V_{in1}, +\Delta V_{in1}]\) defines the region where both transistors are active.

**Annotations and Specific Data Points:**
- The graph is annotated with \(-\Delta V_{in1}\) and \(+\Delta V_{in1}\) to indicate the input voltage limits where the differential pair begins to turn one side off completely.

This graph is critical for understanding how the differential pair responds to changes in input voltage, showing the linearity and the range of operation of the circuit.
image_name:(b)
description:The graph labeled "(b)" is a plot of transconductance \( G_m \) versus differential input voltage \( \Delta V_{in} \). It is a typical bell-shaped curve, commonly seen in the analysis of differential pairs.

1. **Type of Graph and Function:**
- This is a plot of transconductance, which is a measure of the gain of a differential pair, as a function of the differential input voltage.

2. **Axes Labels and Units:**
- The horizontal axis represents the differential input voltage \( \Delta V_{in} \), with units likely in volts (V).
- The vertical axis represents the transconductance \( G_m \), which is typically measured in siemens (S).

3. **Overall Behavior and Trends:**
- The graph shows a peak in transconductance at the center, where \( \Delta V_{in} \) is zero, indicating maximum gain at this point.
- As \( \Delta V_{in} \) moves away from zero in either direction (positive or negative), the transconductance decreases, showing a symmetrical drop on both sides of the peak.
- This behavior suggests that the differential pair is most linear and has the highest gain when the input voltage difference is minimal.

4. **Key Features and Technical Details:**
- The peak of the curve corresponds to the maximum transconductance, which occurs at \( \Delta V_{in} = 0 \).
- The curve is symmetrical about the vertical axis, indicating balanced behavior for both positive and negative input differences.
- The width of the curve at the base indicates the range of \( \Delta V_{in} \) over which the transconductance is significant.

5. **Annotations and Specific Data Points:**
- The graph does not show specific numerical annotations or markers, but the peak and symmetry are key qualitative features.
- The points labeled \( -\Delta V_{in1} \) and \( +\Delta V_{in1} \) likely represent the input voltage limits where the transconductance begins to significantly decrease.

Figure 4.13 Variation of drain currents and overall transconductance of a differential pair versus input voltage.
image_name:Figure 4.14(a)
description:The graph labeled "(a)" is a plot that illustrates the variation of the difference in drain currents (denoted as \( I_{D1} - I_{D2} \)) of a differential pair versus the input voltage \( \Delta V_{in} \).

1. **Type of Graph and Function:**
- This is a characteristic curve graph representing the relationship between differential input voltage and differential output current in a differential amplifier.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( \Delta V_{in} \), representing the input voltage difference. It does not specify units, but it is typically in volts.
- The vertical axis is labeled \( I_{D1} - I_{D2} \), representing the difference in drain currents. Units are not specified, but it is typically in amperes.

3. **Overall Behavior and Trends:**
- The graph shows an S-shaped curve centered around the origin. As \( \Delta V_{in} \) increases from negative to positive, \( I_{D1} - I_{D2} \) transitions from \(-I_{SS}\) to \(+I_{SS}\), indicating that the current difference increases with input voltage.
- The curve is symmetrical around the origin, suggesting that the behavior of the differential pair is balanced for positive and negative input voltages.

4. **Key Features and Technical Details:**
- The curve starts at \(-I_{SS}\) when \( \Delta V_{in} \) is negative and transitions smoothly to \(+I_{SS}\) as \( \Delta V_{in} \) becomes positive.
- The transition region is centered around \( \Delta V_{in} = 0 \) and is steep, indicating high transconductance in this region.
- The points \(-\Delta V_{in1}\) and \(+\Delta V_{in1}\) are marked, indicating the input voltage limits where the transconductance begins to significantly decrease.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for \(-\Delta V_{in1}\) and \(+\Delta V_{in1}\), which are critical points where the slope of the curve changes significantly.
- The levels \(-I_{SS}\) and \(+I_{SS}\) are marked on the vertical axis, indicating the saturation levels of the current difference.
image_name:Figure 4.14(b)
description:The graph labeled (b) is a plot depicting the difference in drain currents \( I_{D1} - I_{D2} \) versus the input voltage difference \( \Delta V_{in} \) for a differential pair.

1. **Type of Graph and Function:**
- This is a characteristic curve graph showing the behavior of a differential pair in response to varying input voltage.

2. **Axes Labels and Units:**
- The x-axis represents the input voltage difference \( \Delta V_{in} \), with positive and negative limits marked as \( +\Delta V_{in1} \) and \( -\Delta V_{in1} \) respectively.
- The y-axis represents the difference in drain currents \( I_{D1} - I_{D2} \), with limits at \( +I_{SS} \) and \( -I_{SS} \).
- Both axes appear to be on a linear scale.

3. **Overall Behavior and Trends:**
- The graph shows a sigmoid or "S"-shaped curve.
- As \( \Delta V_{in} \) increases from negative to positive, \( I_{D1} - I_{D2} \) transitions from \( -I_{SS} \) to \( +I_{SS} \).
- The curve is symmetric around the origin, indicating balanced behavior for positive and negative inputs.

4. **Key Features and Technical Details:**
- The curve starts at \( -I_{SS} \) when \( \Delta V_{in} \) is at its negative limit and rises steeply through the origin.
- It reaches \( +I_{SS} \) as \( \Delta V_{in} \) approaches its positive limit.
- The steepest part of the curve is around the origin, indicating high sensitivity or transconductance in this region.

5. **Annotations and Specific Data Points:**
- The points \( -\Delta V_{in1} \) and \( +\Delta V_{in1} \) are marked, likely indicating the input voltage limits where the transconductance begins to significantly decrease.
- The symmetry and steepness of the curve around the origin are notable qualitative features.
image_name:Figure 4.14(c)
description:The graph labeled "(c)" is a plot illustrating the variation of the difference in drain currents \( I_{D1} - I_{D2} \) of a differential pair versus the input voltage difference \( \Delta V_{in} \). This type of graph is typically used to analyze the behavior of differential pairs in electronic circuits, particularly in the context of analog design.

1. **Type of Graph and Function:**
- This is a voltage-current characteristic curve, commonly used in analog electronics to depict the behavior of differential pairs.

2. **Axes Labels and Units:**
- The x-axis represents the input voltage difference \( \Delta V_{in} \).
- The y-axis represents the difference in drain currents \( I_{D1} - I_{D2} \).
- The graph does not specify units for the axes, but typically, the x-axis would be in volts and the y-axis in milliamperes or another current unit.

3. **Overall Behavior and Trends:**
- The graph exhibits an S-shaped curve, indicating a nonlinear relationship between the input voltage difference and the drain current difference.
- At the center of the graph, around \( \Delta V_{in} = 0 \), the curve is steep, showing a high sensitivity of current difference to small changes in input voltage.
- As \( \Delta V_{in} \) increases positively or negatively beyond certain thresholds (\( +\Delta V_{in1} \) and \( -\Delta V_{in1} \)), the curve flattens, indicating saturation where further increases in input voltage result in minimal changes in current difference.

4. **Key Features and Technical Details:**
- The graph is symmetric about the origin, which is a characteristic feature of differential pairs.
- The saturation levels on the y-axis are marked as \( +I_{SS2} \) and \( -I_{SS2} \), indicating the maximum and minimum current differences achievable.
- The points \( +\Delta V_{in1} \) and \( -\Delta V_{in1} \) mark the boundaries where the current difference begins to saturate.

5. **Annotations and Specific Data Points:**
- The graph includes dashed lines indicating the saturation levels and the input voltage limits \( +\Delta V_{in1} \) and \( -\Delta V_{in1} \).
- No specific numerical values are provided for these points, but they are crucial for understanding the operational limits of the differential pair in this context.

The value of $\Delta V_{i n 1}$ given by (4.14) in essence represents the maximum differential input that the circuit can "handle." It is possible to relate $\Delta V_{i n 1}$ to the overdrive voltage of $M_{1}$ and $M_{2}$ in equilibrium. For a zero differential input, $I_{D 1}=I_{D 2}=I_{S S} / 2$, yielding

$$
\begin{equation*}
\left(V_{G S}-V_{T H}\right)_{1,2}=\sqrt{\frac{I_{S S}}{\mu_{n} C_{o x} \frac{W}{L}}} \tag{4.15}
\end{equation*}
$$

Thus, $\Delta V_{i n 1}$ is equal to $\sqrt{2}$ times the equilibrium overdrive. The point is that increasing $\Delta V_{i n 1}$ to make the circuit more linear inevitably increases the overdrive voltage of $M_{1}$ and $M_{2}$. For a given $I_{S S}$, this is accomplished only by reducing $W / L$ and hence the transconductance of the transistors, trading small-signal gain for linearity. Alternatively, we can increase $I_{S S}$, but at the cost of power. (What happens to the gain if $I_{S S}$ is increased but $I_{S S} R_{D}$ is kept constant due to headroom constraints?)

#### Example 4.5

Due to a manufacturing defect, the differential signals applied to a differential pair have unequal dc levels (Fig. 4.15). If the peak swing, $V_{0}$, is small and the imbalance, $V_{O S}$, happens to be equal to $\Delta V_{i n 1} / 2=(1 / 2) \sqrt{2 I_{S S} /\left(\mu_{n} C_{o x} W / L\right)}$, sketch the output voltage waveforms and determine the small-signal voltage gain.
image_name:Figure 4.15(a)
description:The diagram labeled "(a)" illustrates a differential pair circuit with its input and output voltage waveforms.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform representation of input and output voltages in a differential pair circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents time (t), though no specific units are provided.
- The vertical axis represents voltage, with specific voltages labeled as \( V_{in1} \), \( V_{in2} \), \( V_{X} \), and \( V_{Y} \).

3. **Overall Behavior and Trends:**
- The input voltages \( V_{in1} \) and \( V_{in2} \) are sinusoidal waveforms with a small peak swing \( V_{0} \) and a dc level imbalance \( V_{OS} \).
- The output voltages \( V_{X} \) and \( V_{Y} \) also display sinusoidal behavior, shifted due to the imbalance in the input.

4. **Key Features and Technical Details:**
- The differential input voltages \( V_{in1} \) and \( V_{in2} \) have a peak-to-peak amplitude of \( V_{0} \) and are offset by \( V_{OS} \), indicating an imbalance.
- The output voltage difference \( V_{Y} - V_{X} \) is given by \( -\frac{\sqrt{7}}{4} I_{SS} R_{D} \), reflecting the effect of the input imbalance on the differential pair.
- The gain is affected by the transconductance \( G_{m1} \) and the load resistance \( R_{D} \), contributing to the amplitude of the output waveforms.

5. **Annotations and Specific Data Points:**
- The diagram includes annotations such as \( V_{0} \) and \( V_{OS} \) for the input voltages and \( G_{m1} R_{D} V_{0} \) and \( \frac{\sqrt{7}}{4} I_{SS} R_{D} \) for the output voltage difference.
- These annotations help in understanding the relationship between the input imbalance and the resulting output voltage differences in the circuit.
image_name:Figure 4.15(b)
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin1}
name: M2, type: NMOS, ports: {S: P, D: Y, G: Vin2}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Y}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
]
extrainfo:This circuit is a differential pair with NMOS transistors M1 and M2. The current source ISS provides biasing. Resistors RD are connected to the drains of M1 and M2, and VDD is the supply voltage. The circuit is designed to analyze the effect of differential input imbalance VOS on the output voltage waveforms.
image_name:Figure 4.15(c)
description:The function graph labeled "(c)" in the provided image is a time-domain waveform graph depicting the output voltages \(V_X\) and \(V_Y\) over time \(t\). This graph is part of a differential pair circuit analysis where the differential signals have unequal DC levels due to a manufacturing defect.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform plot showing the behavior of two output voltages, \(V_X\) and \(V_Y\), over time.

2. **Axes Labels and Units:**
- The horizontal axis represents time \(t\), although specific units are not provided, it is typically in seconds or milliseconds for such circuits.
- The vertical axis represents voltage, but specific units are not labeled. It is assumed to be in volts.

3. **Overall Behavior and Trends:**
- Both \(V_X\) and \(V_Y\) waveforms are sinusoidal, indicating periodic voltage changes over time.
- The waveforms show a phase shift relative to each other, which is typical in differential pairs with DC level imbalances.
- The amplitude of the waveforms is annotated, showing different peak levels for \(V_X\) and \(V_Y\).

4. **Key Features and Technical Details:**
- The peak-to-peak swing of \(V_Y\) is marked as \(G_{m1} R_D V_0\), where \(G_{m1}\) is the transconductance, \(R_D\) is the drain resistance, and \(V_0\) is the peak swing.
- The difference between the DC levels of \(V_X\) and \(V_Y\) is annotated as \(\frac{\sqrt{7}}{4} I_{SS} R_D\), indicating the impact of the imbalance \(V_{OS}\) on the differential pair.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for the peak swing and DC level difference, providing insight into the circuits performance under the described conditions.
- These annotations help in understanding the effect of the imbalance and how it influences the output voltages of the differential pair.

This waveform graph effectively illustrates the impact of the DC imbalance \(V_{OS}\) on the differential pairs output voltages, highlighting the resulting phase shift and amplitude differences.

#### Solution

Let us first study the circuit with only dc inputs that differ by $V_{O S}$. The differential pair senses an imbalance of $V_{i n 1}-V_{i n 2}=V_{O S}$ and, from Eq. (4.10), generates

$$
\begin{equation*}
I_{D 1}-I_{D 2}=\frac{\sqrt{7}}{4} I_{S S} \tag{4.16}
\end{equation*}
$$

That is, $I_{D 1} \approx 0.83 I_{S S}, I_{D 2} \approx 0.17 I_{S S}$ and $V_{X}-V_{Y}=-(\sqrt{7} / 4) I_{S S} R_{D}$.
Now, we recognize from Fig. 4.15(b) that the input dc imbalance biases the transistors away from the highest transconductance, yielding from Eq. (4.11)

$$
\begin{equation*}
G_{m 1}=\frac{3}{\sqrt{14}} \sqrt{\mu_{n} C_{o x} \frac{W}{L} I_{S S}} \tag{4.17}
\end{equation*}
$$

This value is about 20\% less than that at equilibrium. The output waveforms are shown in Fig. 4.15(c).

Small-Signal Analysis We now study the small-signal behavior of differential pairs. As depicted in Fig. 4.16, we apply small signals $V_{i n 1}$ and $V_{i n 2}$ and assume that $M_{1}$ and $M_{2}$ are saturated. What is the differential voltage gain, $\left(V_{\text {out } 1}-V_{\text {out } 2}\right) /\left(V_{\text {in1 }}-V_{\text {in2 }}\right)$ ? Recall from Eq. (4.12) that this quantity equals $\sqrt{\mu_{n} C_{o x} I_{S S} W / L} R_{D}$. Since in the vicinity of equilibrium, each transistor carries approximately $I_{S S} / 2$, this expression reduces to $g_{m} R_{D}$, where $g_{m}$ denotes the transconductance of $M_{1}$ and $M_{2}$. To arrive at the same result by small-signal analysis, we employ two different methods, each providing insight into the circuits operation. We assume that $R_{D 1}=R_{D 2}=R_{D}$.
image_name:Figure 4.16 Differential pair with small-signal inputs
description:
[
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: X}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: Y}
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin1}
name: M2, type: NMOS, ports: {S: P, D: Y, G: Vin2}
name: Vin1, type: VoltageSource, value: Vin1, ports: {Np: Vin1, Nn: GND}
name: Vin2, type: VoltageSource, value: Vin2, ports: {Np: Vin2, Nn: GND}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential pair with NMOS transistors M1 and M2, driven by small-signal inputs Vin1 and Vin2. The transistors share a common source node P, connected to a current source ISS. The outputs are taken across resistors RD1 and RD2, leading to nodes Vout1 and Vout2.

Method I The circuit of Fig. 4.16 is driven by two independent signals. Thus, the output can be computed by superposition. (The voltages in this section are small-signal quantities.)
image_name:(a)
description:
[
name: Vin1, type: VoltageSource, value: Vin1, ports: {Np: Vin1, Nn: GND}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: X}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: Y}
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin1}
name: M2, type: NMOS, ports: {S: P, D: Y, G: GND}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential pair with NMOS transistors M1 and M2. It is driven by a small-signal input Vin1, with the outputs taken across resistors RD1 and RD2 at nodes Vout1 and Vout2. The common source node P is connected to a current source ISS.
image_name:(b)
description:
[
name: Vin1, type: VoltageSource, value: Vin1, ports: {Np: Vin1, Nn: GND}
name: M1, type: NMOS, ports: {S: s1s2, D: X, G: Vin1}
name: M2, type: NMOS, ports: {S: s1s2, D: Y, G: GND}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: X}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: Y}
name: Vin1, type: VoltageSource, value: Vin1, ports: {Np: Vin1, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: S1, N2: GND}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: X}
name: M1, type: NMOS, ports: {S: S1, D: X, G: Vin1}
]
extrainfo:The circuit diagram (c) represents a differential pair with NMOS transistor M1, driven by a small-signal input Vin1. The output is taken across resistor RD1, leading to node VX. The source of M1 is connected to ground through resistor RS.

Figure 4.17 (a) Differential pair sensing one input signal; (b) circuit of (a) viewed as a CS stage degenerated by $M_{2}$; (c) equivalent circuit of (b).

Let us set $V_{i n 2}$ to zero and find the effect of $V_{i n 1}$ at $X$ and $Y$ [Fig. 4.17(a)]. To obtain $V_{X}$, we note that $M_{1}$ forms a common-source stage with a degeneration resistance equal to the impedance seen looking into the source of $M_{2}$ [Fig. 4.17(b)]. Neglecting channel-length modulation and body effect, we have $R_{S}=1 / g_{m 2}[$ Fig. 4.17(c) $]$ and

$$
\begin{equation*}
\frac{V_{X}}{V_{i n 1}}=\frac{-R_{D}}{\frac{1}{g_{m 1}}+\frac{1}{g_{m 2}}} \tag{4.18}
\end{equation*}
$$

To calculate $V_{Y}$, we note that $M_{1}$ drives $M_{2}$ as a source follower and replace $V_{i n 1}$ and $M_{1}$ by a Thevenin equivalent (Fig. 4.18): the Thevenin voltage $V_{T}=V_{i n 1}$ and the resistance $R_{T}=1 / g_{m 1}$. Here, $M_{2}$ operates as a common-gate stage, exhibiting a gain equal to

$$
\begin{equation*}
\frac{V_{Y}}{V_{i n 1}}=\frac{R_{D}}{\frac{1}{g_{m 2}}+\frac{1}{g_{m 1}}} \tag{4.19}
\end{equation*}
$$

It follows from (4.18) and (4.19) that the overall voltage gain for $V_{i n 1}$ is

$$
\begin{equation*}
\left.\left(V_{X}-V_{Y}\right)\right|_{\text {Due to } \operatorname{Vin} 1}=\frac{-2 R_{D}}{\frac{1}{g_{m 1}}+\frac{1}{g_{m 2}}} V_{i n 1} \tag{4.20}
\end{equation*}
$$

image_name:(a)
description:
[
name: Vin1, type: VoltageSource, value: Vin1, ports: {Np: Vin1, Nn: GND}
name: M1, type: NMOS, ports: {S: s1s2, D: d1, G: Vin1}
name: M2, type: NMOS, ports: {S: s1s2, D: Y, G: GND}
name: RD1, type: Resistor, value: RD1, ports: {N1: d1, N2: VDD}
name: RD2, type: Resistor, value: RD2, ports: {N1: Y, N2: VDD}
]
extrainfo:The circuit (a) is a differential amplifier with NMOS transistors M1 and M2. Vin1 is the input voltage source, and RD1 and RD2 are the load resistors. M1 operates in a common-source configuration, and M2 in a common-gate configuration. The output is taken at node Y.
image_name:(b)
description:
[
name: Vin1, type: VoltageSource, value: Vin1, ports: {Np: Vin1, Nn: GND}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: Y}
name: M2, type: NMOS, ports: {S: s2, D: Y, G: GND}
name: VT, type: VoltageSource, value: VT, ports: {Np: Vin1, Nn: GND}
name: RT, type: Resistor, value: RT, ports: {N1: Vin1, N2: S2}
]
extrainfo:The circuit diagram (b) shows a simplified common-gate amplifier configuration using an NMOS transistor M2. The input voltage is applied through a Thevenin equivalent circuit consisting of a voltage source VT and resistor RT. The output is taken across RD2 with node Y as the output node Vout2.

Figure 4.18 Replacing $M_{1}$ by a Thevenin equivalent.

which, for $g_{m 1}=g_{m 2}=g_{m}$, reduces to

$$
\begin{equation*}
\left.\left(V_{X}-V_{Y}\right)\right|_{\text {Due to } V i n 1}=-g_{m} R_{D} V_{i n 1} \tag{4.21}
\end{equation*}
$$

By virtue of symmetry, the effect of $V_{i n 2}$ at $X$ and $Y$ is identical to that of $V_{i n 1}$ except for a change in the polarities:

$$
\begin{equation*}
\left.\left(V_{X}-V_{Y}\right)\right|_{\text {Due to } \operatorname{Vin2}}=g_{m} R_{D} V_{i n 2} \tag{4.22}
\end{equation*}
$$

Adding the two sides of (4.21) and (4.22) to perform superposition, we have

$$
\begin{equation*}
\frac{\left(V_{X}-V_{Y}\right)_{t o t}}{V_{i n 1}-V_{i n 2}}=-g_{m} R_{D} \tag{4.23}
\end{equation*}
$$

Comparison of (4.21), (4.22), and (4.23) indicates that the magnitude of the differential gain is equal to $g_{m} R_{D}$ regardless of how the inputs are applied: in Figs. 4.17 and 4.18 , the input is applied to only one side, whereas in Fig. 4.16 the input is the difference between two sources. It is also important to recognize that if the output is single-ended, i.e., it is sensed between $X$ or $Y$ and ground, the gain is halved.

#### Example 4.6

Due to a manufacturing error, in the circuit of Fig. 4.19, $M_{2}$ is twice as wide as $M_{1}$. Calculate the small-signal gain if the dc levels of $V_{i n 1}$ and $V_{i n 2}$ are equal.
image_name:Figure 4.19
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout2, G: Vin1}
name: M2, type: NMOS, ports: {S: GND, D: Vout1, G: Vin2}
name: RD, type: Resistor, value: RD, ports: {N1: Vout2, N2: VDD}
name: RD, type: Resistor, value: RD, ports: {N1: Vout1, N2: VDD}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential pair with NMOS transistors M1 and M2. M2 is twice as wide as M1. The current source ISS provides biasing current to the differential pair. The outputs are taken as Vout1 and Vout2, and each output is connected to VDD through a resistor RD.

#### Solution

If the gates of $M_{1}$ and $M_{2}$ are at the same dc potential, then $V_{G S 1}=V_{G S 2}$ and $I_{D 2}=2 I_{D 1}=2 I_{S S} / 3$. Thus, $g_{m 1}=\sqrt{2 \mu_{n} C_{o x}(W / L) I_{S S} / 3}$ and $g_{m 2}=\sqrt{2 \mu_{n} C_{o x}(2 W / L)\left(2 I_{S S}\right) / 3}=2 g_{m 1}$. Following the same procedure as above, the reader can show that

$$
\begin{align*}
\left|A_{v}\right| & =\frac{2 R_{D}}{\frac{1}{g_{m 1}}+\frac{1}{2 g_{m 1}}}  \tag{4.24}\\
& =\frac{4}{3} g_{m 1} R_{D} \tag{4.25}
\end{align*}
$$

Note that, for a given $I_{S S}$, this value is lower than the gain of a symmetric differential pair [Eq. (4.23)] because $g_{m 1}$ is smaller. The reader can show that the characteristics of Fig. 4.13 are shifted horizontally, and hence the circuit exhibits an "offset." We utilize this idea in Chapter 14 to linearize differential pairs.

How does the transconductance of a differential pair compare with that of a common-source stage? For a given total bias current, the value of $g_{m}$ in (4.23) is $1 / \sqrt{2}$ times that of a single transistor biased at $I_{S S}$ with the same dimensions. Thus, the total $G_{m}$ is proportionally less.

Method II If a fully-symmetric differential pair senses differential inputs (i.e., the two inputs change by equal and opposite amounts from the equilibrium condition), then the concept of "half circuit" can be applied. We first prove a lemma.

Lemma Consider the symmetric circuit shown in Fig. 4.20(a), where $D_{1}$ and $D_{2}$ represent any threeterminal active device. Suppose $V_{i n 1}$ and $V_{i n 2}$ change differentially, the former from $V_{0}$ to $V_{0}+\Delta V_{i n}$ and the latter from $V_{0}$ to $V_{0}-\Delta V_{\text {in }}$ [Fig. 4.20(b)]. Then, if the circuit remains linear, $V_{P}$ does not change. Assume $\lambda=0$.
image_name:(a)
description:The circuit is symmetric with two diodes and two differential input voltage sources. Node P acts as a virtual ground due to symmetry.
image_name:(b)
description:The diagram labeled as (b) is a time-domain waveform graph illustrating differential voltage changes in a symmetric circuit. The horizontal axis represents time \(t\), while the vertical axis represents voltage \(V\). The graph shows two separate curves for \(V_{in1}\) and \(V_{in2}\), both initially starting at a common reference voltage \(V_0\).

As time progresses, \(V_{in1}\) increases from \(V_0\) to \(V_0 + \Delta V_{in}\), while \(V_{in2}\) decreases from \(V_0\) to \(V_0 - \Delta V_{in}\). This change is symmetric around the initial voltage \(V_0\), depicted by the dotted horizontal line.

The overall behavior of the graph indicates a differential input change, where the increase in \(V_{in1}\) is matched by an equal decrease in \(V_{in2}\). This symmetry is crucial for maintaining the virtual ground condition at node \(P\) in the circuit, as stated in the lemma. The graph emphasizes the linear and symmetric nature of the voltage changes, which are essential for the circuits operation as a differential amplifier.
image_name:(c)
description:The graph labeled as (c) in the provided image is a time-domain waveform diagram, illustrating the behavior of voltages $V_1$ and $V_2$ over time, as they respond to differential input changes.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform, showing how voltages $V_1$ and $V_2$ change with respect to time $t$.

2. **Axes Labels and Units:**
- The horizontal axis represents time ($t$), although no specific units are provided.
- The vertical axis represents voltage, with changes denoted as $\Delta V_1$ and $\Delta V_2$.

3. **Overall Behavior and Trends:**
- The waveform shows symmetric changes in $V_1$ and $V_2$ around a central voltage $V_a$.
- As time progresses, $V_1$ increases by an amount $\Delta V_1$ from $V_a$, while $V_2$ decreases by $\Delta V_2$ from $V_a$, indicating a differential change.
- The curves for both $V_1$ and $V_2$ appear smooth, suggesting a gradual change rather than abrupt transitions.

4. **Key Features and Technical Details:**
- The diagram emphasizes the symmetry in the changes of $V_1$ and $V_2$, consistent with the concept of differential input changes as discussed in the context.
- The central voltage $V_a$ acts as a reference point, similar to the virtual ground concept at node $P$.

5. **Annotations and Specific Data Points:**
- The changes $\Delta V_1$ and $\Delta V_2$ are marked with arrows, indicating the magnitude of change from the reference voltage $V_a$.
- No specific numerical values are provided, but the symmetrical nature of the voltages is highlighted.

Figure 4.20 Illustration of why node $P$ is a virtual ground.

Proof. The lemma can be proved by invoking symmetry. As long as the operation remains linear, so that the difference between the bias currents of $D_{1}$ and $D_{2}$ is negligible, the circuit is symmetric. Thus, $V_{P}$ cannot "favor" the change at one input and "ignore" the other.

From another point of view, the effect of $D_{1}$ and $D_{2}$ at node $P$ can be represented by Thevenin equivalents (Fig. 4.21). If $V_{T 1}$ and $V_{T 2}$ change by equal and opposite amounts and $R_{T 1}$ and $R_{T 2}$ are equal, then $V_{P}$ remains constant. We emphasize that this is valid if the changes are small enough that we can assume $R_{T 1}=R_{T 2}$ (e.g., $\left.1 / g_{m 1}=1 / g_{m 2}\right) .{ }^{6}$ This perspective suggests the lemmas validity even if the tail current source is not ideal.
image_name:Figure 4.21
description:
[
name: VT1, type: VoltageSource, value: VT1, ports: {Np: VT1+, Nn: GND}
name: RT1, type: Resistor, value: RT1, ports: {N1: VT1+, N2: P}
name: VT2, type: VoltageSource, value: VT2, ports: {Np: VT2+, Nn: GND}
name: RT2, type: Resistor, value: RT2, ports: {N1: VT2+, N2: P}
]
extrainfo:The circuit consists of two voltage sources VT1 and VT2, each connected to resistors RT1 and RT2 respectively, forming a node P where the resistors meet. Thevenin equivalents are used to analyze the effect on node P.

Figure 4.21 Replacing each half of a differential pair by a Thevenin equivalent.

We now offer a more formal proof. Let us assume that $V_{1}$ and $V_{2}$ have an equilibrium value of $V_{a}$ and change by $\Delta V_{1}$ and $\Delta V_{2}$, respectively [Fig. 4.20 (c)]. The output currents therefore change by $g_{m} \Delta V_{1}$ and $g_{m} \Delta V_{2}$. Since $I_{1}+I_{2}=I_{T}$, we have $g_{m} \Delta V_{1}+g_{m} \Delta V_{2}=0$, i.e., $\Delta V_{1}=-\Delta V_{2}$. We also know that $V_{i n 1}-V_{1}=V_{i n 2}-V_{2}$, and hence $V_{0}+\Delta V_{i n}-\left(V_{a}+\Delta V_{1}\right)=V_{0}-\Delta V_{i n}-\left(V_{a}+\Delta V_{2}\right)$. Consequently, $2 \Delta V_{\text {in }}=\Delta V_{1}-\Delta V_{2}=2 \Delta V_{1}$. In other words, if $V_{i n 1}$ and $V_{i n 2}$ change by $+\Delta V_{i n}$ and $-\Delta V_{i n}$, respectively, then $V_{1}$ and $V_{2}$ change by the same values, i.e., a differential change in the inputs is simply "absorbed" by $V_{1}$ and $V_{2}$. In fact, since $V_{P}=V_{i n 1}-V_{1}$, and since $V_{1}$ exhibits the same change as $V_{i n 1}, V_{P}$ does not change.

The above lemma greatly simplifies the small-signal analysis of differential amplifiers. As shown in Fig. 4.22, since $V_{P}$ experiences no change, node $P$ can be considered "ac ground" (or a "virtual ground"), and the circuit can be decomposed into two separate halves. We say that we have applied the "half-circuit concept" [1]. We can write $V_{X} / V_{i n 1}=-g_{m} R_{D}$ and $V_{Y} /\left(-V_{i n 1}\right)=-g_{m} R_{D}$, where $V_{i n 1}$ and $-V_{i n 1}$ denote the voltage change on each side. Thus, $\left(V_{X}-V_{Y}\right) /\left(2 V_{i n 1}\right)=-g_{m} R_{D}$.
image_name:Fig. 4.22(a)
description:
[
name: Vin1, type: VoltageSource, value: Vin1, ports: {Np: Vin1, Nn: GND}
name: RD1, type: Resistor, value: RD1, ports: {N1: VDD, N2: X}
name: RD2, type: Resistor, value: RD2, ports: {N1: VDD, N2: Y}
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin1}
name: M2, type: NMOS, ports: {S: P, D: Y, G: -Vin1}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
]
extrainfo:This circuit is a differential amplifier using NMOS transistors M1 and M2, with resistive loads RD1 and RD2, and a current source ISS. The circuit is split into two halves using the half-circuit concept for analysis.
image_name:Fig. 4.22(b)
description:
[
name: Vin1, type: VoltageSource, value: Vin1, ports: {Np: Vin1, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vin1}
name: M2, type: NMOS, ports: {S: GND, D: Y, G: Vin1}
name: RD1, type: Resistor, value: RD1, ports: {N1: X, N2: VDD}
name: RD2, type: Resistor, value: RD2, ports: {N1: Y, N2: VDD}
]
extrainfo:The circuit uses a differential pair with NMOS transistors M1 and M2. The resistors RD1 and RD2 are connected to VDD and provide load for the NMOS transistors. The current source ISS provides biasing for the differential pair. The input voltage source Vin1 is connected to both gates of the NMOS transistors, with the source terminals connected to a common node P, which is also connected to the current source ISS.

Figure 4.22 Application of the half-circuit concept.

#### Example 4.7

Calculate the differential gain of the circuit of Fig. 4.22(a) if $\lambda \neq 0$.

#### Solution

Applying the half-circuit concept as illustrated in Fig. 4.23, we have $V_{X} / V_{i n 1}=-g_{m}\left(R_{D} \| r_{O 1}\right)$ and $V_{Y} /\left(-V_{i n 1}\right)=$ $-g_{m}\left(R_{D} \| r_{O 2}\right)$, thus arriving at $\left(V_{X}-V_{Y}\right) /\left(2 V_{i n 1}\right)=-g_{m}\left(R_{D} \| r_{O}\right)$, where $r_{O}=r_{O 1}=r_{O 2}$. Note that Method I would require lengthy calculations here.
image_name:Figure 4.23
description:
[
name: Vin1, type: VoltageSource, value: Vin1, ports: {Np: Vin1, Nn: GND}
name: -Vin1, type: VoltageSource, value: -Vin1, ports: {Np: -Vin1, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: RD1, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RD2, type: Resistor, value: RD, ports: {N1: VDD, N2: Y}
name: ro1, type: Resistor, value: ro1, ports: {N1: X, N2: GND}
name: ro2, type: Resistor, value: ro2, ports: {N1: Y, N2: GND}
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vin1}
name: M2, type: NMOS, ports: {S: GND, D: Y, G: -Vin1}
]
extrainfo:This circuit is a differential amplifier using NMOS transistors M1 and M2. The resistors RD1 and RD2 are connected to VDD and serve as load resistors for the transistors. Resistors ro1 and ro2 represent the output resistances of the transistors. The circuit amplifies the difference between the input voltages Vin1 and -Vin1.

The half-circuit concept provides a powerful technique for analyzing symmetric differential pairs with fully differential inputs. But what happens if the two inputs are not fully differential [Fig. 4.24(a)]? As depicted in Figs. 4.24(b) and (c), the two inputs $V_{i n 1}$ and $V_{i n 2}$ can be viewed as

$$
\begin{align*}
& V_{i n 1}=\frac{V_{i n 1}-V_{i n 2}}{2}+\frac{V_{i n 1}+V_{i n 2}}{2}  \tag{4.26}\\
& V_{i n 2}=\frac{V_{i n 2}-V_{i n 1}}{2}+\frac{V_{i n 1}+V_{i n 2}}{2} \tag{4.27}
\end{align*}
$$

Since the second term is common to both inputs, we obtain the equivalent circuit in Fig. 4.24(d), recognizing that the circuit senses a combination of a differential input and a common-mode variation. Therefore, as illustrated in Fig. 4.25, the effect of each type of input can be computed by superposition, with the half-circuit concept applied to the differential-mode operation. We deal with CM analysis in Sec. 4.3.
image_name:(a)
description:The circuit diagram (a) is a differential amplifier with two NMOS transistors M1 and M2. The transistors are configured to amplify the difference between the input voltages Vin1 and Vin2. A current source Iss is connected between the common node P and ground to provide biasing current. The differential input is applied to the gates of the NMOS transistors, and the common node P is the output node where the amplified signal is obtained.
image_name:(b)
description:The circuit diagram (b) shows a differential pair with NMOS transistors M1 and M2. The transistors are connected to a current source Iss at their common source node P. M1 and M2 have their gates connected to input nodes Vin1 and Vin2, respectively. The drains of M1 and M2 are connected to LOAD1 and LOAD2. This configuration senses differential input signals.
image_name:(c)
description:The circuit in diagram (c) consists of two NMOS transistors M1 and M2, and a current source Iss. M1 is connected with its source to ground, drain to LOAD1, and gate to Vin1. M2 is connected with its source to ground, drain to LOAD2, and gate to Vin2. The current source Iss is connected between node P and ground. This configuration is used to analyze differential and common-mode signals.
image_name:(d)
description:The circuit in (d) is a differential amplifier with NMOS transistors M1 and M2. It uses a current source Iss to provide biasing. The inputs are Vin1 and Vin2, and the outputs are at LOAD1 and LOAD2. The configuration allows for differential and common-mode signal analysis.

Figure 4.24 Conversion of arbitrary inputs to differential and common-mode components.

image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: LOAD1, G: (Vin1-Vin2)/2}
name: M2, type: NMOS, ports: {S: P, D: LOAD2, G: (Vin2-Vin1)/2}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with NMOS transistors M1 and M2. It uses a current source Iss to provide biasing. The inputs are Vin1 and Vin2, and the outputs are at LOAD1 and LOAD2. The configuration allows for differential and common-mode signal analysis.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: P, D: LOAD1, G: g1g2}
name: M2, type: NMOS, ports: {S: P, D: LOAD2, G: g1g2}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit in (b) is a differential amplifier with NMOS transistors M1 and M2. It uses a current source Iss to provide biasing. The inputs are Vin1 and Vin2, and the outputs are at LOAD1 and LOAD2. The configuration allows for differential and common-mode signal analysis.

Figure 4.25 Superposition for (a) differential and (b) common-mode signals.

#### Example 4.8

In the circuit of Fig. 4.22(a), calculate $V_{X}$ and $V_{Y}$ if $V_{i n 1} \neq-V_{i n 2}$ and $\lambda \neq 0$.

#### Solution

For differential-mode operation, we have from Fig. 4.26(a)

$$
\begin{align*}
& V_{X}=-g_{m}\left(R_{D} \| r_{O 1}\right) \frac{V_{i n 1}-V_{i n 2}}{2}  \tag{4.28}\\
& V_{Y}=-g_{m}\left(R_{D} \| r_{O 2}\right) \frac{V_{i n 2}-V_{i n 1}}{2} \tag{4.29}
\end{align*}
$$

That is,

$$
\begin{equation*}
V_{X}-V_{Y}=-g_{m}\left(R_{D} \| r_{O}\right)\left(V_{i n 1}-V_{i n 2}\right) \tag{4.30}
\end{equation*}
$$

which is to be expected.
For common-mode operation, the circuit reduces to that in Fig. 4.26(b). How much do $V_{X}$ and $V_{Y}$ change as $V_{i n, C M}$ changes? If the circuit is fully symmetric and $I_{S S}$ an ideal current source, the currents drawn by $M_{1}$ and $M_{2}$ from $R_{D 1}$ and $R_{D 2}$ are exactly equal to $I_{S S} / 2$ and independent of $V_{i n, C M}$. Thus, $V_{X}$ and $V_{Y}$ remain equal to $V_{D D}-R_{D}\left(I_{S S} / 2\right)$ and experience no change as $V_{i n, C M}$ varies. Interestingly, the circuit simply amplifies the difference between $V_{i n 1}$ and $V_{i n 2}$ while eliminating the effect of $V_{i n, C M}$.
image_name:Figure 4.26(a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: g1}
name: M2, type: NMOS, ports: {S: P, D: Y, G: g2}
name: RD, type: Resistor, value: RD, ports: {N1: X, N2: VDD}
name: RD, type: Resistor, value: RD, ports: {N1: Y, N2: VDD}
name: ro1, type: Resistor, value: ro1, ports: {N1: X, N2: P}
name: ro2, type: Resistor, value: ro2, ports: {N1: Y, N2: P}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
name: Vip, type: VoltageSource, value: (Vin1-Vin2)/2, ports: {Np: g1, Nn: GND}
name: Vin, type: VoltageSource, value: (Vin2-Vin1)/2, ports: {Np: g2, Nn: GND}
]
extrainfo:The circuit is a degenerated differential pair with resistive degeneration using resistors ro1 and ro2. It amplifies the difference between Vin1 and Vin2 while eliminating the effect of the common-mode input voltage Vin,CM.
image_name:Fig. 4.27(b)
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: g1g2}
name: M2, type: NMOS, ports: {S: P, D: Y, G: g1g2}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Y}
name: ro1, type: Resistor, value: ro1, ports: {N1: X, N2: P}
name: ro2, type: Resistor, value: ro2, ports: {N1: Y, N2: P}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
]
extrainfo:This circuit is a degenerated differential pair with resistive degeneration to improve linearity. It amplifies the difference between Vin1 and Vin2 while eliminating the effect of Vin,CM. The currents through M1 and M2 are equal to ISS / 2.

### 4.2.3 Degenerated fferential Pair

As with a simple common-source stage, a differential pair can incorporate resistive degeneration to improve its linearity. Shown in Fig. 4.27(a), such a topology softens the nonlinear behavior of $M_{1}$ and $M_{2}$ by $R_{S 1}$ and $R_{S 2}$. This can be seen from the input-output characteristics of Fig. 4.27(b), where, due to degeneration, the differential voltage necessary to turn off one side increases in magnitude. We can
image_name:(a)
description:
[
name: Vin1, type: VoltageSource, ports: {Np: Vin1, Nn: GND}
name: Vin2, type: VoltageSource, ports: {Np: Vin2, Nn: GND}
name: M1, type: NMOS, ports: {S: S1, D: X, G: Vin1}
name: M2, type: NMOS, ports: {S: S2, D: Y, G: Vin2}
name: RD1, type: Resistor, value: RD, ports: {N1: X, N2: VDD}
name: RD2, type: Resistor, value: RD, ports: {N1: Y, N2: VDD}
name: RS1, type: Resistor, value: RS, ports: {N1: S1, N2: P}
name: RS2, type: Resistor, value: RS, ports: {N1: S2, N2: P}
name: Iss, type: CurrentSource, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a degenerated differential pair with resistive degeneration to improve linearity. It consists of two NMOS transistors M1 and M2, each with a source degeneration resistor RS1 and RS2, and load resistors RD1 and RD2. The input voltages are Vin1 and Vin2, and the current source Iss biases the pair.
image_name:(b)
description:The graph in Figure 4.27(b) is a plot depicting the input-output characteristics of a degenerated differential pair circuit, specifically showing the effect of resistive degeneration on the behavior of the circuit.

1. **Type of Graph and Function**:
- The graph is a characteristic curve plot, showing the relationship between differential input voltage (ΔV_in) and output voltages (V_X and V_Y) for a differential pair circuit.

2. **Axes Labels and Units**:
- The horizontal axis represents the differential input voltage (ΔV_in), with key points marked as -ΔV_in1, -ΔV_in2, +ΔV_in1, and +ΔV_in2.
- The vertical axis represents the output voltages V_X and V_Y.
- No specific units are given, but they are typically in volts.

3. **Overall Behavior and Trends**:
- The graph shows two sets of curves: one for R_S = 0 (no degeneration) and one for R_S > 0 (with degeneration).
- Without degeneration (R_S = 0), the curves are steeper, indicating a sharper transition in the input-output relationship.
- With degeneration (R_S > 0), the curves are smoother and less steep, indicating improved linearity and a more gradual transition.

4. **Key Features and Technical Details**:
- The central point of the graph corresponds to a balanced input condition (ΔV_in = 0), where the output voltages are equal.
- The degeneration causes the differential voltage necessary to turn off one side of the pair to increase, as indicated by the wider spread of the curves with R_S > 0.
- The output voltages V_X and V_Y are marked at specific levels: V_DD, V_DD - RD I_SS, and V_DD - RD I_SS/2, corresponding to the operating points of the circuit.

5. **Annotations and Specific Data Points**:
- The graph includes annotations for the cases of R_S = 0 and R_S > 0, highlighting the difference in slope and linearity.
- The graph is symmetric around the vertical axis, indicating balanced operation of the differential pair.

This plot effectively demonstrates how resistive degeneration affects the linearity and input-output characteristics of a differential pair circuit, making it an essential tool for understanding the trade-offs in amplifier design.

Figure 4.27 (a) Degenerated differential pair, and (b) characteristics with and without degeneration.
readily prove this point. Suppose that at $V_{i n 1}-V_{i n 2}=\Delta V_{i n 2}, M_{2}$ turns off and $I_{D 1}=I_{S S}$. We then have $V_{G S 2}=V_{T H}$, and hence

$$
\begin{equation*}
V_{i n 1}-V_{G S 1}-R_{S} I_{S S}=V_{i n 2}-V_{T H} \tag{4.31}
\end{equation*}
$$

which yields

$$
\begin{align*}
V_{i n 1}-V_{i n 2} & =V_{G S 1}-V_{T H}+R_{S} I_{S S}  \tag{4.32}\\
& =\sqrt{\frac{2 I_{S S}}{\mu_{n} C_{o x} \frac{W}{L}}}+R_{S} I_{S S} \tag{4.33}
\end{align*}
$$

We recognize the first term on the right-hand side as $\Delta V_{i n 1}$ (the input difference necessary for turning off $M_{2}$ if $R_{S}=0$ ). It follows that

$$
\begin{equation*}
\Delta V_{i n 2}-\Delta V_{i n 1}=R_{S} I_{S S} \tag{4.34}
\end{equation*}
$$

suggesting that the linear input range is widened by approximately $\pm R_{S} I_{S S}$.
The small-signal voltage gain of the degenerated differential pair can be obtained by applying the half-circuit concept. The half circuit is simply a degenerated CS stage, exhibiting a gain of

$$
\begin{equation*}
\left|A_{v}\right|=\frac{R_{D}}{\frac{1}{g_{m}}+R_{S}} \tag{4.35}
\end{equation*}
$$

if $\lambda=\gamma=0$. The circuit thus trades gain for linearity-as is also observed from the slopes of the characteristics in Fig. 4.27(b). Note that $A_{v}$ is less sensitive to $g_{m}$ variations in this case.

In addition to reducing the gain, the degeneration resistors in Fig. 4.27(a) also consume voltage headroom. In the equilibrium condition, each resistor sustains a voltage drop of $R_{S} I_{S S} / 2$, as if the tail current source itself required this much more headroom. The input common-mode level must therefore be higher by this amount, and so must be the minimum voltage at $X$ or $Y$. In other words, the maximum allowable differential output swing is reduced by $R_{S} I_{S S}$. This issue can be resolved as shown in Fig. 4.28, where the tail current source is split in half, with each half directly tied to a source. In equilibrium, no current flows through the degeneration resistance, and hence no headroom is sacrificed. ${ }^{7}$ Other methods of linearizing differential pairs are described in Chapter 14.
image_name:Figure 4.28 Degenerated differential pair with split tail current source
description:
[
name: RD1, type: Resistor, value: RD1, ports: {N1: X, N2: VDD}
name: RD2, type: Resistor, value: RD2, ports: {N1: Y, N2: VDD}
name: M1, type: NMOS, ports: {S: S1, D: X, G: g1}
name: M2, type: NMOS, ports: {S: S2, D: Y, G: g2}
name: 2Rs, type: Resistor, value: 2Rs, ports: {N1: S1, N2: S2}
name: Iss/2_1, type: CurrentSource, value: Iss/2, ports: {Np: S1, Nn: GND}
name: Iss/2_2, type: CurrentSource, value: Iss/2, ports: {Np: S2, Nn: GND}
]
extrainfo:The circuit is a degenerated differential pair with a split tail current source. It features two NMOS transistors, M1 and M2, each connected to a resistor (RD1 and RD2) at the drain. The sources of M1 and M2 are connected through a resistor 2Rs, and each source is also connected to a current source Iss/2, which is tied to ground. The gates of M1 and M2 are connected to inputs g1 and g2, respectively.

## 4.3 ■ Common-Mode Response

An important attribute of differential amplifiers is their ability to suppress the effect of common-mode perturbations. Example 4.8 portrays an idealized case of common-mode response. In reality, neither is the circuit fully symmetric nor does the current source exhibit an infinite output impedance. As a result, a fraction of the input CM variation appears at the output.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin,CM}
name: M2, type: NMOS, ports: {S: P, D: Y, G: Vin,CM}
name: RD, type: Resistor, value: RD, ports: {N1: X, N2: VDD}
name: RD, type: Resistor, value: RD, ports: {N1: Y, N2: VDD}
name: RSS, type: Resistor, value: RSS, ports: {N1: P, N2: GND}
]
extrainfo:The circuit is a degenerated differential pair with a split tail current source. It senses common-mode input and is designed to suppress common-mode perturbations. The resistors RD are connected to the power supply VDD, and RSS is the tail resistor connected to ground.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin,CM}
name: RD, type: Resistor, value: RD, ports: {N1: X, N2: VDD}
name: RSS, type: Resistor, value: RSS, ports: {N1: P, N2: GND}
]
extrainfo:This circuit is a simplified differential pair sensing common-mode input with a finite output impedance current source RSS. It demonstrates the common-mode response with nodes X and P connected to the NMOS M1.
image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: s12, D: Vout, G: Vin,CM}
name: M2, type: NMOS, ports: {S: s12 D: Vout, G: Vin,CM}
name: RD, type: Resistor, value: RD/2, ports: {N1: VDD, N2: Vout}
name: RSS, type: Resistor, value: RSS, ports: {N1: s12, N2: GND}
]
extrainfo:The circuit is a simplified differential amplifier with a split tail current source, showing common-mode input suppression. M1 and M2 are NMOS transistors sharing the same gate and source nodes, with a combined drain node. RD is split into two equal halves, each connected to VDD and Vout.

Figure 4.29 (a) Differential pair sensing CM input; (b) simplified version of (a); (c) equivalent circuit of (b).

We first assume that the circuit is symmetric, but the current source has a finite output impedance, $R_{S S}$ [Fig. 4.29(a)]. As $V_{i n, C M}$ changes, so does $V_{P}$, thereby increasing the drain currents of $M_{1}$ and $M_{2}$ and lowering both $V_{X}$ and $V_{Y}$. Owing to symmetry, $V_{X}$ remains equal to $V_{Y}$ and, as depicted in Fig. 4.29(b), the two nodes can be shorted together. Since $M_{1}$ and $M_{2}$ are now "in parallel," i.e., they share all of their respective terminals, the circuit can be reduced to that in Fig. 4.29(c). Note that the composite device, $M_{1}+M_{2}$, has twice the width and the bias current of each of $M_{1}$ and $M_{2}$ and, therefore, twice their transconductance. The "common-mode gain" of the circuit is thus equal to

$$
\begin{align*}
A_{v, C M} & =\frac{V_{\text {out }}}{V_{\text {in, }, C M}}  \tag{4.36}\\
& =-\frac{R_{D} / 2}{1 /\left(2 g_{m}\right)+R_{S S}} \tag{4.37}
\end{align*}
$$

where $g_{m}$ denotes the transconductance of each of $M_{1}$ and $M_{2}$ and $\lambda=\gamma=0$.
What is the significance of this calculation? In a symmetric circuit, input CM variations disturb the bias points, altering the small-signal gain and possibly limiting the output voltage swings. This can be illustrated by an example.

#### Example 4.9

The circuit of Fig. 4.30 uses a resistor rather than a current source to define a tail current of 1 mA . Assume that $(W / L)_{1,2}=25 / 0.5, \mu_{n} C_{o x}=50 \mu \mathrm{~A} / \mathrm{V}^{2}, V_{T H}=0.6 \mathrm{~V}, \lambda=\gamma=0$, and $V_{D D}=3 \mathrm{~V}$.
(a) What is the required input CM voltage for which $R_{S S}$ sustains 0.5 V ?
(b) Calculate $R_{D}$ for a differential gain of 5 .
(c) What happens at the output if the input CM level is 50 mV higher than the value calculated in (a)?
image_name:Figure 4.30
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin1}
name: M2, type: NMOS, ports: {S: P, D: Y, G: Vin2}
name: RD1, type: Resistor, value: RD, ports: {N1: X, N2: VDD}
name: RD2, type: Resistor, value: RD, ports: {N1: Y, N2: VDD}
name: RSS, type: Resistor, value: RSS, ports: {N1: P, N2: GND}
]
extrainfo:The circuit is a differential amplifier with NMOS transistors M1 and M2. It uses resistors RD for load and RSS for tail current stabilization. A current source of 1 mA is connected at the tail.

#### Solution

(a) Since $I_{D 1}=I_{D 2}=0.5 \mathrm{~mA}$, we have

$$
\begin{align*}
V_{G S 1}=V_{G S 2} & =\sqrt{\frac{2 I_{D 1}}{\mu_{n} C_{o x} \frac{W}{L}}}+V_{T H}  \tag{4.38}\\
& =1.23 \mathrm{~V} \tag{4.39}
\end{align*}
$$

Thus, $V_{\text {in }, C M}=V_{G S 1}+0.5 \mathrm{~V}=1.73 \mathrm{~V}$. Note that $R_{S S}=500 \Omega$.
(b) The transconductance of each device is $g_{m}=\sqrt{2 \mu_{n} C_{o x}(W / L) I_{D 1}}=1 /(632 \Omega)$, requiring $R_{D}=3.16 \mathrm{k} \Omega$ for a gain of 5 .

Note that the output bias level is equal to $V_{D D}-I_{D 1} R_{D}=1.42 \mathrm{~V}$. Since $V_{i n, C M}=1.73 \mathrm{~V}$ and $V_{T H}=0.6 \mathrm{~V}$, the transistors are 290 mV away from the triode region.
(c) If $V_{i n, C M}$ increases by 50 mV , the equivalent circuit of Fig. 4.29 (c) suggests that $V_{X}$ and $V_{Y}$ drop by

$$
\begin{align*}
\left|\Delta V_{X, Y}\right| & =\Delta V_{i n, C M} \frac{R_{D} / 2}{R_{S S}+1 /\left(2 g_{m}\right)}  \tag{4.40}\\
& =50 \mathrm{mV} \times 1.94  \tag{4.41}\\
& =96.8 \mathrm{mV} \tag{4.42}
\end{align*}
$$

Now, $M_{1}$ and $M_{2}$ are only 143 mV away from the triode region because the input CM level has increased by 50 mV and the output CM level has decreased by 96.8 mV .

The foregoing discussion indicates that the finite output impedance of the tail current source results in some common-mode gain in a symmetric differential pair. Nonetheless, this is usually a minor concern. More troublesome is the variation of the differential output as a result of a change in $V_{i n, C M}$, an effect that occurs because in reality the circuit is not fully symmetric, i.e., the two sides suffer from slight mismatches during manufacturing. For example, in Fig. 4.29(a), $R_{D 1}$ may not be exactly equal to $R_{D 2}$.

We now study the effect of input common-mode variations if the circuit is asymmetric and the tail current source suffers from a finite output impedance. Suppose, as shown in Fig. 4.31, $R_{D 1}=R_{D}$ and $R_{D 2}=R_{D}+\Delta R_{D}$, where $\Delta R_{D}$ denotes a small mismatch and the circuit is otherwise symmetric. Assume that $\lambda=\gamma=0$ for $M_{1}$ and $M_{2}$. What happens to $V_{X}$ and $V_{Y}$ as $V_{i n, C M}$ increases? We recognize that $M_{1}$ and $M_{2}$ operate as one source follower,

image_name:Figure 4.31 Common-mode response in the presence of resistor mismatch
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin,CM}
name: M2, type: NMOS, ports: {S: P, D: Y, G: Vin,CM}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RD + ΔRD, type: Resistor, value: RD + ΔRD, ports: {N1: VDD, N2: Y}
name: RSS, type: Resistor, value: RSS, ports: {N1: P, N2: GND}
]
extrainfo:The circuit demonstrates the common-mode response in the presence of resistor mismatch, showing how Vout1 and Vout2 are affected by changes in Vin,CM. The mismatch in resistors RD and RD + ΔRD causes differential behavior in the output voltages.

raising $V_{P}$ by

$$
\begin{equation*}
\Delta V_{P}=\frac{R_{S S}}{R_{S S}+\frac{1}{2 g_{m}}} \Delta V_{i n, C M} \tag{4.43}
\end{equation*}
$$

Since $M_{1}$ and $M_{2}$ are identical, $I_{D 1}$ and $I_{D 2}$ increase by $\left[g_{m} /\left(1+2 g_{m} R_{S S}\right)\right] \Delta V_{i n, C M}$, but $V_{X}$ and $V_{Y}$ change by different amounts:

$$
\begin{align*}
\Delta V_{X} & =-\Delta V_{i n, C M} \frac{g_{m}}{1+2 g_{m} R_{S S}} R_{D}  \tag{4.44}\\
\Delta V_{Y} & =-\Delta V_{i n, C M} \frac{g_{m}}{1+2 g_{m} R_{S S}}\left(R_{D}+\Delta R_{D}\right) \tag{4.45}
\end{align*}
$$

Thus, a common-mode change at the input introduces a differential component at the output. We say that the circuit exhibits common-mode to differential conversion. This is a critical problem because if the input of a differential pair includes both a differential signal and common-mode noise, the circuit corrupts the amplified differential signal by the input CM change. The effect is illustrated in Fig. 4.32.
image_name:Figure 4.32 Effect of CM noise in the presence of resistor mismatch.
description:
[
name: M1, type: NMOS, ports: {S: s1s2, D: Voutn, G: Vin,DM}
name: M2, type: NMOS, ports: {S: s1s2, D: Voutp, G: Vin,CM}
name: RD, type: Resistor, value: RD, ports: {N1: Voutn, N2: VDD}
name: RD + ΔRD, type: Resistor, value: RD + ΔRD, ports: {N1: Voutp, N2: VDD}
name: RSS, type: Resistor, value: RSS, ports: {N1: s1s2, N2: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a differential pair with common-mode and differential-mode inputs. It shows the effect of common-mode noise in the presence of resistor mismatch, leading to common-mode to differential conversion.

In summary, the common-mode response of differential pairs depends on the output impedance of the tail current source and asymmetries in the circuit, manifesting itself through two effects: variation of the output CM level (in the absence of mismatches) and conversion of input common-mode variations to differential components at the output. In analog circuits, the latter effect is much more severe than the
former. For this reason, the common-mode response should usually be studied with mismatches taken into account.

How significant is common-mode to differential conversion? We make two observations. First, as the frequency of the CM disturbance increases, the total capacitance shunting the tail current source introduces larger tail current variations. Thus, even if the output resistance of the current source is high, common-mode to differential conversion becomes significant at high frequencies. Shown in Fig. 4.33, this capacitance arises from the parasitics of the current source itself as well as the source-bulk junctions of $M_{1}$ and $M_{2}$. Second, the asymmetry in the circuit stems from both the load resistors and the input transistors, the latter contributing a typically much greater mismatch.
image_name:Figure 4.33 CM response with finite tail capacitance.
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin,CM}
name: M2, type: NMOS, ports: {S: P, D: Y, G: Vin,CM}
name: RD1, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RD2, type: Resistor, value: RD, ports: {N1: VDD, N2: Y}
name: C1, type: Capacitor, value: C1, ports: {Np: P, Nn: GND}
name: ISS, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
]
extrainfo:This circuit is a differential pair with NMOS transistors M1 and M2, sharing a common source node P. The load resistors RD1 and RD2 are connected to VDD. The current source ISS provides biasing, and the capacitor C1 is connected between the common source node and ground.

Let us study the asymmetry resulting from mismatches between $M_{1}$ and $M_{2}$ in Fig. 4.34(a). Owing to dimension and threshold voltage mismatches, the two transistors carry slightly different currents and exhibit unequal transconductances. We assume that $\lambda=\gamma=0$. To calculate the small-signal gain from $V_{i n, C M}$ to $X$ and $Y$, we use the equivalent circuit in Fig. 4.34(b), writing $I_{D 1}=g_{m 1}\left(V_{i n, C M}-V_{P}\right)$ and $I_{D 2}=g_{m 2}\left(V_{i n, C M}-V_{P}\right)$. Since $\left(I_{D 1}+I_{D 2}\right) R_{S S}=V_{P}$,

$$
\begin{equation*}
\left(g_{m 1}+g_{m 2}\right)\left(V_{i n, C M}-V_{P}\right) R_{S S}=V_{P} \tag{4.46}
\end{equation*}
$$

and

$$
\begin{equation*}
V_{P}=\frac{\left(g_{m 1}+g_{m 2}\right) R_{S S}}{\left(g_{m 1}+g_{m 2}\right) R_{S S}+1} V_{i n, C M} \tag{4.47}
\end{equation*}
$$

image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin,CM}
name: M2, type: NMOS, ports: {S: P, D: Y, G: Vin,CM}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Y}
name: RSS, type: Resistor, value: RSS, ports: {N1: P, N2: GND}
]
extrainfo:The circuit is a differential pair with NMOS transistors M1 and M2, sensing a common-mode input voltage Vin,CM. The resistors RD are connected to VDD and nodes X and Y, which are the outputs Vout1 and Vout2, respectively. RSS provides a common-source connection to ground.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin,CM}
name: M2, type: NMOS, ports: {S: P, D: Y, G: Vin,CM}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Y}
name: RSS, type: Resistor, value: RSS, ports: {N1: P, N2: GND}
]
extrainfo:The circuit is a differential pair with NMOS transistors M1 and M2, sensing a common-mode input Vin,CM. The resistors RD are used as load resistors connected to VDD. RSS is a source degeneration resistor connected to ground.

Figure 4.34 (a) Differential pair sensing CM input; (b) equivalent circuit of (a).

We now obtain the output voltages as

$$
\begin{align*}
V_{X} & =-g_{m 1}\left(V_{i n, C M}-V_{P}\right) R_{D}  \tag{4.48}\\
& =\frac{-g_{m 1}}{\left(g_{m 1}+g_{m 2}\right) R_{S S}+1} R_{D} V_{i n, C M} \tag{4.49}
\end{align*}
$$

and

$$
\begin{align*}
V_{Y} & =-g_{m 2}\left(V_{i n, C M}-V_{P}\right) R_{D}  \tag{4.50}\\
& =\frac{-g_{m 2}}{\left(g_{m 1}+g_{m 2}\right) R_{S S}+1} R_{D} V_{i n, C M} \tag{4.51}
\end{align*}
$$

The differential component at the output is therefore given by

$$
\begin{equation*}
V_{X}-V_{Y}=-\frac{g_{m 1}-g_{m 2}}{\left(g_{m 1}+g_{m 2}\right) R_{S S}+1} R_{D} V_{i n, C M} \tag{4.52}
\end{equation*}
$$

In other words, the circuit converts input CM variations to a differential error by a factor equal to

$$
\begin{equation*}
A_{C M-D M}=-\frac{\Delta g_{m} R_{D}}{\left(g_{m 1}+g_{m 2}\right) R_{S S}+1} \tag{4.53}
\end{equation*}
$$

where $A_{C M-D M}$ denotes common-mode to differential-mode conversion and $\Delta g_{m}=g_{m 1}-g_{m 2}$.

#### Example 4.10

Two differential pairs are cascaded as shown in Fig. 4.35. Transistors $M_{3}$ and $M_{4}$ suffer from a $g_{m}$ mismatch of $\Delta g_{m}$, the total parasitic capacitance at node $P$ is represented by $C_{P}$, and the circuit is otherwise symmetric. What fraction of the supply noise appears as a differential component at the output? Assume that $\lambda=\gamma=0$.
image_name:Figure 4.35
description:
[
name: M1, type: NMOS, ports: {S: P2, D: A, G: Vip}
name: M2, type: NMOS, ports: {S: P2, D: B, G: Vin}
name: M3, type: NMOS, ports: {S: P, D: X, G: B}
name: M4, type: NMOS, ports: {S: P, D: Y, G: A}
name: RD1, type: Resistor, value: RD, ports: {N1: VDD, N2: A}
name: RD2, type: Resistor, value: RD, ports: {N1: VDD, N2: B}
name: RD3, type: Resistor, value: RD, ports: {N1: VDD, N2: X}
name: RD4, type: Resistor, value: RD, ports: {N1: VDD, N2: Y}
name: ISS1, type: CurrentSource, value: ISS, ports: {Np: P2, Nn: GND}
name: ISS2, type: CurrentSource, value: ISS, ports: {Np: P, Nn: GND}
name: CP, type: Capacitor, value: CP, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a cascaded differential pair with NMOS transistors. It is symmetric, with two differential pairs M1-M2 and M3-M4. The parasitic capacitance CP is connected at node P, and the circuit is powered by VDD. The output is taken from node Y as Vout.

#### Solution

Neglecting the capacitance at nodes $A$ and $B$, we note that the supply noise appears at these nodes with no attenuation. Substituting $1 /\left(C_{P} s\right)$ for $R_{S S}$ in (4.53) and taking the magnitude, we have

$$
\begin{equation*}
\left|A_{C M-D M}\right|=\frac{\Delta g_{m} R_{D}}{\sqrt{1+\left(g_{m 3}+g_{m 4}\right)^{2}\left|\frac{1}{C_{P} \omega}\right|^{2}}} \tag{4.54}
\end{equation*}
$$

The key point is that the effect becomes more noticeable as the supply noise frequency, $\omega$, increases.

For a meaningful comparison of differential circuits, the undesirable differential component produced by CM variations must be normalized to the wanted differential output resulting from amplification. We define the "common-mode rejection ratio" (CMRR) as the desired gain divided by the undesired gain:

$$
\begin{equation*}
\mathrm{CMRR}=\left|\frac{A_{D M}}{A_{C M-D M}}\right| \tag{4.55}
\end{equation*}
$$

If only $g_{m}$ mismatch is considered, the reader can show from the analysis of Fig. 4.17 that

$$
\begin{equation*}
\left|A_{D M}\right|=\frac{R_{D}}{2} \frac{g_{m 1}+g_{m 2}+4 g_{m 1} g_{m 2} R_{S S}}{1+\left(g_{m 1}+g_{m 2}\right) R_{S S}} \tag{4.56}
\end{equation*}
$$

and hence

$$
\begin{align*}
\mathrm{CMRR} & =\frac{g_{m 1}+g_{m 2}+4 g_{m 1} g_{m 2} R_{S S}}{2 \Delta g_{m}}  \tag{4.57}\\
& \approx \frac{g_{m}}{\Delta g_{m}}\left(1+2 g_{m} R_{S S}\right) \tag{4.58}
\end{align*}
$$

where $g_{m}$ denotes the mean value, that is, $g_{m}=\left(g_{m 1}+g_{m 2}\right) / 2$. In practice, all mismatches must be taken into account. Note that $2 g_{m} R_{S S} \gg 1$, and hence $\mathrm{CMRR} \approx 2 g_{m}^{2} R_{S S} / \Delta g_{m}$.

#### Example 4.11

Our studies suggest that an ideal tail current source guarantees infinite CM rejection. Is this always true?

#### Solution

Interestingly, it is not. If the two transistors exhibit body-effect mismatch, then the circuit still converts an input CM change to a differential output component even if the tail impedance is infinite. As illustrated in Fig. 4.36, a change in $V_{i n, C M}$ produces a change in $V_{P}$, and hence in $V_{B S}$ of both transistors. If $g_{m b 1} \neq g_{m b 2}$, the change in $I_{D 1}\left(=g_{m b 1} V_{B S 1}\right)$ is not equal to that in $I_{D 2}$, yielding a differential change at the output.
image_name:Figure 4.36
description:
[
name: Vin,CM, type: VoltageSource, value: Vin,CM, ports: {Np: Vin,CM, Nn: GND}
name: M1, type: NMOS, ports: {S: p, D: d1, G: Vin,CM}
name: M2, type: NMOS, ports: {S: p, D: d2, G: Vin,CM}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: p, Nn: GND}
]
extrainfo: A current source Iss provides bias current. The circuit converts common-mode input voltage Vin,CM to differential output currents through body-effect mismatch.

## 4.4 - Differential Pair with MOS Loads

The load of a differential pair need not be implemented by linear resistors. As with the commonsource stages studied in Chapter 3, differential pairs can employ diode-connected or current-source loads (Fig. 4.37). The small-signal differential gain can be derived using the half-circuit concept. For Fig. 4.37(a),

$$
\begin{align*}
A_{v} & =-g_{m N}\left(g_{m P}^{-1}\left\|r_{O N}\right\| r_{O P}\right)  \tag{4.59}\\
& \approx-\frac{g_{m N}}{g_{m P}} \tag{4.60}
\end{align*}
$$

image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: p, D: X, G: Vip}
name: M2, type: NMOS, ports: {S: p, D: Y, G: Vin}
name: M3, type: PMOS, ports: {S: VDD, D: X, G: X}
name: M4, type: PMOS, ports: {S: VDD, D: Y, G: Y}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: p, Nn: GND}
]
extrainfo:The circuit is a differential pair with diode-connected PMOS loads. The NMOS transistors M1 and M2 form the differential pair, while PMOS transistors M3 and M4 provide the diode-connected loads. The current source Iss provides biasing for the differential pair.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: p, D: Voutp, G: Vip}
name: M2, type: NMOS, ports: {S: p, D: Voutn, G: Vin}
name: M3, type: PMOS, ports: {S: VDD, D: Voutp, G: Vb}
name: M4, type: PMOS, ports: {S: VDD, D: Voutn, G: Vb}
name: I_SS, type: CurrentSource, value: I_SS, ports: {Np: p, Nn: GND}
]
extrainfo:This circuit is a differential pair with current-source loads. It consists of two NMOS transistors (M1 and M2) with their sources connected to a current source I_SS, and two PMOS transistors (M3 and M4) acting as loads. The PMOS transistors are biased with a voltage Vb.
Figure 4.37 Differential pair with (a) diode-connected and (b) current-source loads.

where the subscripts $N$ and $P$ denote NMOS and PMOS, respectively. Expressing $g_{m N}$ and $g_{m P}$ in terms of device dimensions, we have

$$
\begin{equation*}
A_{v} \approx-\sqrt{\frac{\mu_{n}(W / L)_{N}}{\mu_{p}(W / L)_{P}}} \tag{4.61}
\end{equation*}
$$

For Fig. 4.37(b), we have

$$
\begin{equation*}
A_{v}=-g_{m N}\left(r_{O N} \| r_{O P}\right) \tag{4.62}
\end{equation*}
$$

#### Example 4.12

It is possible to obviate the need for $V_{b}$ in the circuit of Fig. 4.37(b) as shown in Fig. 4.38(a), where $R_{1}$ and $R_{2}\left(=R_{1}\right)$ are relatively large. In the absence of signals, $V_{X}=V_{Y}=V_{N}=V_{D D}-\left|V_{G S 3,4}\right|$. That is, $M_{3}$ and $M_{4}$ are "self-biased." Determine the differential voltage gain of this topology.
image_name:Fig. 4.38(a)
description:
[
name: M1, type: NMOS, ports: {S: p, D: X, G: Vip}
name: M2, type: NMOS, ports: {S: p, D: Y, G: Vin}
name: M3, type: PMOS, ports: {S: VDD, D: X, G: N}
name: M4, type: PMOS, ports: {S: VDD, D: Y, G: N}
name: R1, type: Resistor, value: R1, ports: {N1: X, N2: N}
name: R2, type: Resistor, value: R2, ports: {N1: Y, N2: N}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: p, Nn: GND}
]
extrainfo:The circuit is a differential amplifier with self-biased PMOS loads. The resistors R1 and R2 are used for biasing, and the current source Iss provides a constant current. The PMOS transistors M3 and M4 are self-biased, maintaining constant voltage at node N.
image_name:Fig. 4.38(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: M3, type: PMOS, ports: {S: GND, D: Vout, G: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: Vout}
]
extrainfo:The circuit is a differential amplifier with a simplified half-circuit representation. M1 is an NMOS transistor with its source connected to ground, drain to the output node Vout, and gate to the input node Vin. M3 is a PMOS transistor with its source connected to VDD, drain to Vout, and gate also to Vout. R1 is connected across Vout, providing feedback or load resistance.

#### Solution

For differential outputs, $V_{N}$ does not change (why?) and can be considered ac ground. Shown in Fig. 4.38(b), the half-circuit yields

$$
\begin{equation*}
\left|A_{v}\right|=g_{m 1}\left(r_{O 1}\left\|R_{1}\right\| r_{O 3}\right) \tag{4.63}
\end{equation*}
$$

If the resistors are much greater than $r_{O 1} \| r_{O 3}$, then they negligibly reduce the gain.

In the circuit of Fig. 4.37(a), the diode-connected loads consume voltage headroom, thus creating a trade-off between the output voltage swings, the voltage gain, and the input CM range. Recall from Eq. (3.37) that, for given bias current and input device dimensions, the circuits gain and the PMOS overdrive voltage scale together. To achieve a higher gain, $(W / L)_{P}$ must decrease, thereby increasing $\left|V_{G S P}-V_{T H P}\right|$ and lowering the CM level at nodes $X$ and $Y$.

In order to alleviate the above difficulty, part of the bias currents of the input transistors can be provided by PMOS current sources. Illustrated in Fig. 4.39(a), the idea is to lower the $g_{m}$ of the load devices by reducing their current rather than their aspect ratio. For example, if the "auxiliary" current sources, $M_{5}$ and $M_{6}$, carry $80 \%$ of the drain current of $M_{1}$ and $M_{2}$, the current through $M_{3}$ and $M_{4}$ is reduced by a factor of five. For a given $\left|V_{G S P}-V_{T H P}\right|$, this translates to a fivefold reduction in the transconductance of $M_{3}$ and $M_{4}$ because the aspect ratio of the devices can be lowered by the same factor. Thus, the differential gain is now five times that of the case with no PMOS current sources (if $\lambda=0$ ).
image_name:Figure 4.39 Addition of current sources to increase the voltage gain with (a) diode-connected loads
description:The circuit diagram shows a differential amplifier with diode-connected PMOS loads (M3 and M4) and additional PMOS current sources (M5 and M6) to increase the voltage gain. The current sources M5 and M6 carry 80% of the drain current of M1 and M2. The current through M3 and M4 is reduced by a factor of five, increasing the differential gain by five times.

image_name:(b)
description:The circuit is a differential amplifier with resistive loads (RD1 and RD2) and diode-connected PMOS transistors (M3 and M4) for increased voltage gain. The current sources M5 and M6 carry 80% of the drain current of M1 and M2. The current through M3 and M4 is reduced by a factor of five, increasing the differential gain by five times.

Figure 4.39 Addition of current sources to increase the voltage gain with (a) diode-connected loads and (b) resistive loads.

Since the voltage headroom consumed by diode-connected devices cannot be less than $V_{T H}$ (if subthreshold conduction is neglected), the topology of Fig. 4.39(a) allows limited output voltage swings. We therefore prefer the alternative shown in Fig. 4.39(b), where the loads are realized by resistors-and the maximum voltage at each output node is equal to $V_{D D}-\left|V_{G S 3,4}-V_{T H 3,4}\right|$ rather than $V_{D D}-\left|V_{T H 3,4}\right|$. For a given output CM level and $80 \%$ auxiliary currents, $R_{D}$ can be five times as large, yielding a voltage gain of

$$
\begin{equation*}
\left|A_{v}\right|=g_{m N}\left(R_{D}\left\|r_{O N}\right\| r_{O P}\right) \tag{4.64}
\end{equation*}
$$

If the PMOS devices are long (and, necessarily, wide), then $r_{O P} \gg r_{O N}$ and the gain is limited by $R_{D} \| r_{O N}$. The circuit of Fig. 4.39(b) approaches that in Fig. 4.37(b) if $R_{D} \rightarrow \infty$, with the PMOS current sources providing all of the bias currents of $M_{1}$ and $M_{2}$.

The small-signal gain of the differential pair with current-source loads is relatively low-in the range of 5 to 10 in nanometer technologies. How do we increase the voltage gain? Borrowing ideas from the amplifiers in Chapter 3, we increase the output impedance of both the PMOS and the NMOS devices by cascoding, in essence creating a differential version of the cascode stage introduced in Chapter 3. The result is depicted in Fig. 4.40(a). To calculate the gain, we construct the half circuit of Fig. 4.40(b), which is similar to the cascode stage of Fig. 3.70. It follows that

$$
\begin{equation*}
\left|A_{v}\right| \approx g_{m 1}\left[\left(g_{m 3} r_{O 3} r_{O 1}\right) \|\left(g_{m 5} r_{O 5} r_{O 7}\right)\right] \tag{4.65}
\end{equation*}
$$

Cascoding therefore increases the differential gain substantially, but at the cost of consuming more voltage headroom. We return to this circuit in Chapter 9.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: d1s3, G: Vip}
name: M2, type: NMOS, ports: {S: P, D: d2s4, G: "Vin"}
name: M3, type: NMOS, ports: {S: d1s3, D: Voutp, G: Vb1}
name: M4, type: NMOS, ports: {S: d2s4, D: Voutn, G: Vb1}
name: M5, type: PMOS, ports: {S: s5d7, D: Voutp, G: Vb2}
name: M6, type: PMOS, ports: {S: s6d8, D: Voutn, G: Vb2}
name: M7, type: PMOS, ports: {S: VDD, D: s5d7, G: Vb3}
name: M8, type: PMOS, ports: {S: VDD, D: s6d8, G: Vb3}
name: Iss, type: CurrentSource, ports: {Np: p, Nn: GND}
]
extrainfo:The circuit is a cascode differential pair with NMOS input transistors (M1, M2) and PMOS load transistors (M5, M6). It includes additional PMOS transistors (M7, M8) for cascoding to increase gain. The circuit is biased with a current source Iss. The output nodes are Voutp and Voutn, and the inputs are Vin and Vin.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1s3, G: Vin}
name: M3, type: NMOS, ports: {S: d1s3, D: Vout, G: Vb1}
name: M5, type: PMOS, ports: {S: VDD, D: Vout, G: Vb2}
name: M7, type: PMOS, ports: {S: VDD, D: s5d7, G: Vb3}
name: Iss, type: CurrentSource, ports: {Np: p, Nn: GND}
]
extrainfo:The circuit is a half circuit of a cascode differential pair, which is used to analyze the gain. It consists of NMOS and PMOS transistors and a current source. The NMOS transistors are M1 and M3, and the PMOS transistors are M5 and M7. The circuit aims to increase the differential gain by employing a cascode configuration.
Figure 4.40 (a) Cascode differential pair; (b) half circuit of (a).

As a final note, we should mention that high-gain fully differential amplifiers require a means of defining the output common-mode level. For example, in Fig. 4.37(b), the output common-mode level is not well-defined, whereas in Fig. 4.37(a), diode-connected transistors define the output CM level as $V_{D D}-V_{G S P}$. We revisit this issue in Chapter 9.

## 4.5 ■ Gilbert Cell

Our study of differential pairs reveals two important aspects of their operation: (1) the small-signal gain of the circuit is a function of the tail current, and (2) the two transistors in a differential pair provide a simple means of steering the tail current to one of two destinations. By combining these two properties, we can develop a versatile building block.

Suppose we wish to construct a differential pair whose gain is varied by a control voltage. This can be accomplished as depicted in Fig. 4.41(a), where the control voltage defines the tail current and hence the gain. In this topology, $A_{v}=V_{\text {out }} / V_{\text {in }}$ varies from zero (if $I_{D 3}=0$ ) to a maximum value given by voltage headroom limitations and device dimensions. This circuit is a simple example of a "variable-gain amplifier" (VGA). VGAs find application in systems where the signal amplitude may experience large variations and hence requires inverse changes in the gain.

Now suppose we seek an amplifier whose gain can be continuously varied from a negative value to a positive value. Consider two differential pairs that amplify the input by opposite gains [Fig. 4.41(b)]. We now have $V_{\text {out } 1} / V_{\text {in }}=-g_{m} R_{D}$ and $V_{\text {out } 2} / V_{\text {in }}=+g_{m} R_{D}$, where $g_{m}$ denotes the transconductance of each transistor in equilibrium. If $I_{1}$ and $I_{2}$ vary in opposite directions, so do $\left|V_{\text {out } 1} / V_{\text {in }}\right|$ and $\left|V_{\text {out } 2} / V_{\text {in }}\right|$.

But how should $V_{\text {out } 1}$ and $V_{\text {out } 2}$ be combined into a single output? As illustrated in Fig. 4.42(a), the two voltages can be summed, producing $V_{\text {out }}=V_{\text {out } 1}+V_{\text {out } 2}=A_{1} V_{\text {in }}+A_{2} V_{\text {in }}$, where $A_{1}$ and $A_{2}$ are controlled by $V_{\text {cont } 1}$ and $V_{\text {cont } 2}$, respectively. The actual implementation is in fact quite simple: since $V_{\text {out } 1}=$ $R_{D} I_{D 1}-R_{D} I_{D 2}$ and $V_{\text {out } 2}=R_{D} I_{D 4}-R_{D} I_{D 3}$, we have $V_{\text {out } 1}+V_{\text {out } 2}=R_{D}\left(I_{D 1}+I_{D 4}\right)-R_{D}\left(I_{D 2}+I_{D 3}\right)$. Thus, rather than add $V_{\text {out } 1}$ and $V_{\text {out } 2}$, we simply short the corresponding drain terminals to sum the currents and subsequently generate the output voltage [Fig. 4.42(b)]. Note that if $I_{1}=0$, then $V_{\text {out }}=+g_{m} R_{D}$, and if $I_{2}=0$, then $V_{\text {out }}=-g_{m} R_{D}$. For $I_{1}=I_{2}$, the gain drops to zero.
image_name:Figure 4.41 (a)
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Voutp}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Voutn}
name: M1, type: NMOS, ports: {S: s1s2d3, D: Voutp, G: Vip}
name: M2, type: NMOS, ports: {S: s1s2d3, D: Voutn, G: Vin}
name: M3, type: NMOS, ports: {S: GND, D: s1s2d3, G: Vcont}
]
extrainfo:This circuit is a simple variable gain amplifier (VGA) with two NMOS transistors (M1 and M2) configured to amplify the differential input signals Vip and Vin. The gain is controlled by the NMOS transistor M3, which is modulated by the control voltage Vcont. The resistors RD are used to convert the current to voltage at the output nodes Voutp and Voutn. The current source I1 provides a bias current to M3.
image_name:Figure 4.41 (b)
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout1P}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout1N}
name: M1, type: NMOS, ports: {S: p, D: Vout1P, G: Vin}
name: M2, type: NMOS, ports: {S: p, D: Vout1N, G: Vin}
name: I1, type: CurrentSource, value: I1, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit is a two-stage amplifier providing variable gain. The NMOS transistors M1 and M2 are used for amplification, controlled by the input voltage Vin. The resistors RD are connected to VDD, providing load resistance. M3 and M4 are additional NMOS transistors used for gain control, influenced by control voltages Vcont1 and Vcont2. The current sources I1 and I2 adjust the biasing of the circuit.

Figure 4.41 (a) Simple VGA; (b) two stages providing variable gain.
image_name:Figure 4.42(a)
description:The diagram labeled (a) illustrates a simple variable gain amplifier (VGA) circuit. This circuit is designed to provide variable amplification of an input signal, controlled by external voltages. Here’s a detailed breakdown:

1. **Main Components:**
- **Amplifiers (A1 and A2):** Two operational amplifiers are used to amplify the input signals. Each amplifier receives a differential input and produces an output voltage (Vout1 and Vout2).
- **Summation Block:** The outputs from the two amplifiers are summed to produce the final output voltage (Vout).
- **Control Voltages (Vcont1 and Vcont2):** These voltages are used to control the gain of the amplifiers A1 and A2, respectively.
- **Input Signals (Vin, Vinp, Vinn):** The circuit receives a differential input signal, where Vinp is the positive input and Vinn is the negative input.

2. **Flow of Information or Control:**
- The input signals Vinp and Vinn are fed into the amplifiers A1 and A2.
- The amplifiers process these signals, adjusting their gain based on the control voltages Vcont1 and Vcont2.
- The outputs of A1 (Vout1) and A2 (Vout2) are then summed in the summation block to produce the final output voltage Vout.

3. **Labels, Annotations, and Key Indicators:**
- The diagram includes labels for the input signals (Vinp, Vinn), the control voltages (Vcont1, Vcont2), and the output signals (Vout1, Vout2, Vout).
- The summation block is indicated by a circle with a summation symbol inside, showing the combination of Vout1 and Vout2.

4. **Overall System Function:**
- The primary function of this system is to provide a variable gain to the input signal. By adjusting the control voltages Vcont1 and Vcont2, the gain of each amplifier can be varied, allowing for precise control over the amplification of the input signal. This is useful in applications where signal levels need to be dynamically adjusted, such as in audio processing or communication systems.
image_name:Figure 4.42(b)
description:The circuit in diagram (b) is a two-stage amplifier providing variable gain. NMOS transistors M1 and M2 are used for amplification, controlled by input voltages Vip and Vin. Resistors RD are connected to VDD, providing load resistance. M3 and M4 are additional NMOS transistors used for gain control, influenced by control voltages Vcont1 and Vcont2. Current sources I1 and I2 adjust the biasing of the circuit.
image_name:Figure 4.42(c)
description:The circuit is a differential amplifier circuit with variable gain control using NMOS transistors. It uses two pairs of NMOS transistors (M1, M2 and M3, M4) for amplification. The gain is controlled by transistors M5 and M6, which are influenced by control voltages Vcont1 and Vcont2. The resistors RD provide load resistance, and the current source ISS sets the bias current.
image_name:Figure 4.42(d)
description:The circuit is a Gilbert cell, which is used for gain control in analog circuits. The NMOS transistors M1 to M6 form a differential pair configuration to control the gain, influenced by control voltages Vcontp and Vcontn. The resistors RD provide load resistance, and the current source ISS provides biasing.

Figure 4.42 (a) Summation of the output voltages of two amplifiers; (b) summation in the current domain; (c) use of $M_{5}-M_{6}$ to control the gain; (d) Gilbert cell.

In the circuit of Fig. 4.42(b), $V_{\text {cont } 1}$ and $V_{\text {cont } 2}$ must change $I_{1}$ and $I_{2}$ in opposite directions such that the gain of the amplifier changes monotonically. What circuit can vary two currents in opposite directions? A differential pair provides such a characteristic, leading to the topology of Fig. 4.42(c). Note that for a large $\left|V_{\text {cont } 1}-V_{\text {cont } 2}\right|$, all of the tail current is steered to one of the top differential pairs and the gain from $V_{\text {in }}$ to $V_{\text {out }}$ is at its most positive or most negative value. If $V_{\text {cont } 1}=V_{\text {cont } 2}$, the gain is zero. For simplicity, we redraw the circuit as shown in Fig. 4.42(d). Called the "Gilbert cell" [2], this topology is widely used in many analog and communication systems. In a typical design, $M_{1}-M_{4}$ are identical, and so are $M_{5}$ and $M_{6}$.

#### Example 4.13

Explain why the Gilbert cell can operate as an analog voltage multiplier.

#### Solution

Since the gain of the circuit is a function of $V_{\text {cont }}=V_{\text {cont } 1}-V_{\text {cont } 2}$, we have $V_{\text {out }}=V_{\text {in }} \cdot f\left(V_{\text {cont }}\right)$. Expanding $f\left(V_{\text {cont }}\right)$ in a Taylor series and retaining only the first-order term, $\alpha V_{\text {cont }}$, we have $V_{\text {out }}=\alpha V_{\text {in }} V_{\text {cont }}$. Thus, the circuit can multiply voltages. This property accompanies any voltage-controlled variable-gain amplifier.

As with a cascode structure, the Gilbert cell consumes a greater voltage headroom than a simple differential pair does. This is because the two differential pairs $M_{1}-M_{2}$ and $M_{3}-M_{4}$ are "stacked" on top of the control differential pair. To understand this point, suppose the differential input, $V_{i n}$, in Fig. 4.42(d) has a common-mode level $V_{C M, i n}$. Then, $V_{A}=V_{B}=V_{C M, i n}-V_{G S 1}$, where $M_{1}-M_{4}$ are assumed identical. For $M_{5}$ and $M_{6}$ to operate in saturation, the CM level of $V_{c o n t}, V_{C M, c o n t}$, must be such that $V_{C M, \text { cont }} \leq V_{C M, \text { in }}-V_{G S 1}+V_{T H 5,6}$. Since $V_{G S 1}-V_{T H 5,6}$ is roughly equal to one overdrive voltage, we conclude that the control CM level must be lower than the input CM level by at least this value.

In arriving at the Gilbert cell topology, we opted to vary the gain of each differential pair through its tail current, thereby applying the control voltage to the bottom pair and the input signal to the top pairs. Interestingly, the order can be exchanged while still obtaining a VGA. Illustrated in Fig. 4.43(a), the idea is to convert the input voltage to current by means of $M_{5}$ and $M_{6}$ and route the current through $M_{1}-M_{4}$ to the output nodes. If, as shown in Fig. 4.43(b), $V_{\text {cont }}$ is very positive, then only $M_{1}$ and $M_{3}$ are on and $V_{\text {out }}=g_{m 5,6} R_{D} V_{\text {in }}$. Similarly, if $V_{\text {cont }}$ is very negative [Fig. 4.43(c)], then only $M_{2}$ and $M_{4}$ are on and $V_{\text {out }}=-g_{m 5,6} R_{D} V_{\text {in }}$. For a zero differential control voltage, $V_{\text {out }}=0$. The input differential pair may incorporate degeneration to provide a linear voltage-to-current conversion.
image_name:(a)
description:The circuit is a Gilbert cell mixer. It uses an NMOS differential pair (M5, M6) to convert input voltage to current, which is then steered by another differential pair (M1, M2) controlled by the control voltage Vcont. The output is taken across the resistors RD at Voutp and Voutn.
image_name:(b)
description:The circuit is a Gilbert cell mixer configuration with a focus on the signal path for a very positive Vcont. M1 and M3 are active, forming the main signal path. The differential pair M5 and M6 are degenerated to linearize the voltage-to-current conversion.
image_name:(c)
description:The circuit is a Gilbert cell mixer configuration with M2, M4, M5, and M6 active. It is designed to produce an output signal at Vout based on the differential input Vip and Vin, with control voltage Vcont influencing the operation of M2 and M4.
Figure 4.43 (a) Gilbert cell sensing the input voltage by the bottom differential pair; (b) signal path for very positive $V_{\text {cont }}$; (c) signal path for very negative $V_{\text {cont }}$.
