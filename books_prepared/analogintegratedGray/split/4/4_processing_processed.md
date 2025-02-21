# 4. Current Mirrors, Active Loads, and References

## 4.1 Introduction

Current mirrors made by using active devices have come to be widely used in analog integrated circuits both as biasing elements and as load devices for amplifier stages. The use of current mirrors in biasing can result in superior insensitivity of circuit performance to variations in power supply and temperature. Current mirrors are frequently more economical than resistors in terms of the die area required to provide bias current of a certain value, particularly when the required value of bias current is small. When used as a load element in transistor amplifiers, the high incremental resistance of the current mirror results in high voltage gain at low powersupply voltages.

The first section of this chapter describes the general properties of current mirrors and compares various bipolar and MOS mirrors to each other using these properties. The next section deals with the use of current mirrors as load elements in amplifier stages. The last section shows how current mirrors are used to construct references that are insensitive to variations in supply and temperature. Finally, the appendix analyzes the effects of device mismatch.

## 4.2 Current Mirrors

### 4.2.1 General Properties

A current mirror is an element with at least three terminals, as shown in Fig. 4.1. The common terminal is connected to a power supply, and the input current source is connected to the input terminal. Ideally, the output current is equal to the input current multiplied by a desired current gain. If the gain is unity, the input current is reflected to the output, leading to the name current mirror. Under ideal conditions, the current-mirror gain is independent of input frequency, and the output current is independent of the voltage between the output and common terminals. Furthermore, the voltage between the input and common terminals is ideally zero because this condition allows the entire supply voltage to appear across the input current source, simplifying its transistor-level design. More than one input and/or output terminals are sometimes used.

In practice, real transistor-level current mirrors suffer many deviations from this ideal behavior. For example, the gain of a real current mirror is never independent of the input frequency. The topic of frequency response is covered in Chapter 7, and mainly dc and lowfrequency ac signals are considered in the rest of this chapter. Deviations from ideality that will be considered in this chapter are listed below.

1. One of the most important deviations from ideality is the variation of the current-mirror output current with changes in voltage at the output terminal. This effect is characterized
image_name:(a)
description:The block diagram labeled "(a)" illustrates a current mirror circuit referenced to ground. The main components of this diagram include:

1. **Current Mirror Block**: This is the central component labeled as "Current Mirror" with three connections: IN, OUT, and COMMON. The current mirror is responsible for copying the input current to the output with high precision.

2. **Input Current Source ($I_{IN}$)**: This is shown as a current source connected to the IN terminal of the current mirror. The input voltage ($V_{IN}$) is applied across this current source.

3. **Output Resistance ($R_{o}$)**: This is depicted as a resistor connected in parallel with the output of the current mirror. It models the small-signal output resistance of the current mirror.

4. **Supply Voltage ($V_{SUP}$)**: The current mirror is powered by a supply voltage, $V_{SUP}$, which is connected to the top of the current source.

5. **Output Current ($I_{OUT}$)**: This is the current flowing out of the OUT terminal of the current mirror, through the output resistance, and towards the load, represented by the arrow labeled $I_{OUT}$.

6. **Output Voltage ($V_{OUT}$)**: This is the voltage across the load, shown as $V_{OUT}$.

**Flow of Information or Control**:
- The input current $I_{IN}$ is fed into the IN terminal of the current mirror block. The current mirror replicates this current at the OUT terminal.
- The output current $I_{OUT}$ flows through the output resistance $R_{o}$, which is connected in parallel with the current mirror's output.
- The output voltage $V_{OUT}$ is developed across the load connected at the OUT terminal.

**Labels, Annotations, and Key Indicators**:
- The diagram includes annotations such as $V_{IN}$, $V_{OUT}$, $I_{IN}$, and $I_{OUT}$ to indicate the input and output parameters.
- The ground symbol indicates the reference point for the circuit's voltages.

**Overall System Function**:
The primary function of this current mirror circuit is to replicate the input current at the output with high accuracy. The presence of the output resistance $R_{o}$ models the non-ideal behavior of the current mirror, affecting the output current based on changes in the output voltage. This setup is essential for maintaining consistent current levels in various circuit applications, despite variations in load or supply voltage.
image_name:(b)
description:The diagram labeled (b) illustrates a current mirror circuit referenced to the positive supply. The main components of this system include:

1. **Current Mirror Block**: This is the central component of the diagram, labeled as "Current mirror" with terminals marked as IN, OUT, and COMMON. The current mirror is responsible for copying the input current ($I_{IN}$) to the output current ($I_{OUT}$) with high accuracy.

2. **Input Current Source ($I_{IN}$)**: Positioned at the bottom left, this source provides the input current to the current mirror. It is connected to the IN terminal of the current mirror.

3. **Output Resistance ($R_{o}$)**: This is depicted as a resistor connected in series with the current mirror's output. It represents the small-signal output resistance of the current mirror, which impacts the performance by affecting the output current's dependency on the output voltage.

4. **Voltage Supply ($V_{SUP}$)**: This is connected to the COMMON terminal of the current mirror, providing necessary power for the operation of the current mirror.

5. **Output Voltage ($V_{OUT}$)**: Located on the right side of the diagram, this is the voltage across the output terminals, influenced by the output current and the output resistance.

**Flow of Information:**
- The input current ($I_{IN}$) is fed into the IN terminal of the current mirror.
- The current mirror attempts to replicate this current to its OUT terminal, producing the output current ($I_{OUT}$).
- The output current flows through the output resistance ($R_{o}$) and affects the output voltage ($V_{OUT}$).

**Labels and Annotations:**
- The diagram includes labels for input and output currents ($I_{IN}$ and $I_{OUT}$), input voltage ($V_{IN}$), and output voltage ($V_{OUT}$).
- Reference points $X_1$ and $X_2$ are marked, indicating connection points for the input and output voltages.

**Overall System Function:**
The primary function of this system is to mirror the input current at the output while maintaining a constant output current regardless of variations in the output voltage. The presence of the output resistance ($R_{o}$) highlights the non-ideality of the current mirror, as it introduces a dependency of the output current on the output voltage. This setup is commonly used in analog circuits for current replication and biasing purposes, where maintaining a stable current is essential.

Figure 4.1 Current-mirror block diagrams referenced to (a) ground and (b) the positive supply.
by the small-signal output resistance, $R_{o}$, of the current mirror. A Norton-equivalent model of the output of the current mirror includes $R_{o}$ in parallel with a current source controlled by the input current. The output resistance directly affects the performance of many circuits that use current mirrors. For example, the common-mode rejection ratio of the differential amplifier depends directly on this resistance, as does the gain of the active-load circuits. Increasing the output resistance reduces the dependence of the output current on the output voltage and is therefore desirable. Generally speaking, the output resistance increases in practical circuits when the output current decreases. Unfortunately, decreasing the output current also decreases the maximum operating speed. Therefore, when comparing the output resistance of two current mirrors, they should be compared at identical output currents.
2. Another important error source is the gain error, which is the deviation of the gain of a current mirror from its ideal value. The gain error is separated into two parts: (1) the systematic gain error and (2) the random gain error. The systematic gain error, $\epsilon$, is the gain error that arises even when all matched elements in the mirror are perfectly matched and will be calculated for each of the current mirrors presented in this section. The random gain error is the gain error caused by unintended mismatches between matched elements.
3. When the input current source is connected to the input terminal of a real current mirror, it creates a positive voltage drop, $V_{\text {IN }}$, that reduces the voltage available across the input current source. Minimizing $V_{\text {IN }}$ is important because it simplifies the design of the input current source, especially in low-supply applications. To reduce $V_{\text {IN }}$, current mirrors sometimes have more than one input terminal. In that case, we will calculate an input voltage for each input terminal. An example is the MOS high-swing cascode current mirror considered in Section 4.2.5.
4. A positive output voltage, $V_{\text {OUT }}$, is required in practice to make the output current depend mainly on the input current. This characteristic is summarized by the minimum voltage across the output branch, $V_{\text {OUT }(\mathrm{min})}$, that allows the output device(s) to operate in the active region. Minimizing $V_{\mathrm{OUT}(\min )}$ maximizes the range of output voltages for which the current-mirror output resistance is almost constant, which is important in applications where current mirrors are used as active loads in amplifiers (especially with low power-supply voltages). This topic is covered in Section 4.3. When current mirrors have more than one output terminal, each output must be biased above its $V_{\text {OUT(min) }}$ to make the corresponding output current depend mainly on the input current.
In later sections, the performance of various current mirrors will be compared to each other through these four parameters: $R_{o}, \epsilon, V_{\mathrm{IN}}$, and $V_{\mathrm{OUT}(\mathrm{min})}$.

### 4.2.2 Simple Current Mirror

#### 4.2.2.1 Bipolar

The simplest form of a current mirror consists of two transistors. Fig. 4.2 shows a bipolar version of this mirror. Transistor $Q_{1}$ is diode connected, forcing its collector-base voltage to zero. In this mode, the collector-base junction is off in the sense that no injection takes place there, and $Q_{1}$ operates in the forward-active region. Assume that $Q_{2}$ also operates in the forward-active region and that both transistors have infinite output resistance. Then $I_{\text {OUT }}$ is controlled by $V_{B E 2}$, which is equal to $V_{B E 1}$ by KVL. A KVL equation is at the heart of the operation of all current mirrors. Neglecting junction leakage currents,

$$
\begin{equation*}
V_{B E 2}=V_{T} \ln \frac{I_{C 2}}{I_{S 2}}=V_{B E 1}=V_{T} \ln \frac{I_{C 1}}{I_{S 1}} \tag{4.1}
\end{equation*}
$$

where $V_{T}=k T / q$ is the thermal voltage and $I_{S 1}$ and $I_{S 2}$ are the transistor saturation currents. From (4.1),

$$
\begin{equation*}
I_{C 2}=\frac{I_{S 2}}{I_{S 1}} I_{C 1} \tag{4.2}
\end{equation*}
$$

If the transistors are identical, $I_{S 1}=I_{S 2}$ and (4.2) shows that the current flowing in the collector of $Q_{1}$ is mirrored to the collector of $Q_{2}$. KCL at the collector of $Q_{1}$ yields

$$
\begin{equation*}
I_{\mathrm{IN}}-I_{C 1}-\frac{I_{C 1}}{\beta_{F}}-\frac{I_{C 2}}{\beta_{F}}=0 \tag{4.3}
\end{equation*}
$$

image_name:Figure 4.2 A simple bipolar current mirror
description:
[
name: Q1, type: NPN, ports: {C: VIN, B: VIN, E: GND}
name: Q2, type: NPN, ports: {C: VOUT, B: VIN, E: GND}
name: I_IN, type: CurrentSource, ports: {Np: VCC, Nn: VIN}
]
extrainfo:The circuit is a simple bipolar current mirror with two identical NPN transistors, Q1 and Q2. The input current I_IN is mirrored to the output, I_OUT, with the assumption that I_OUT = I_C2 = I_C1. The gain of the current mirror is approximately unity if the transistors are identical and beta_F is large.

Figure 4.2 A simple bipolar current mirror.

Therefore, with identical transistors,

$$
\begin{equation*}
I_{\mathrm{OUT}}=I_{C 2}=I_{C 1}=\frac{I_{\mathrm{IN}}}{1+\frac{2}{\beta_{F}}} \tag{4.4}
\end{equation*}
$$

If $\beta_{F}$ is large, the base currents are small and

$$
\begin{equation*}
I_{\mathrm{OUT}}=I_{C 1} \simeq I_{\mathrm{IN}} \tag{4.5}
\end{equation*}
$$

Thus for identical devices $Q_{1}$ and $Q_{2}$, the gain of the current mirror is approximately unity. This result holds for both dc and low-frequency ac currents. Above the $3-\mathrm{dB}$ frequency of the mirror, however, the base current increases noticeably because the impedance of the baseemitter capacitance decreases, reducing the gain of the current mirror. Frequency response is studied in Chapter 7. The rest of this section considers dc currents only.

In practice, the devices need not be identical. Then from (4.2) and (4.3),

$$
\begin{equation*}
I_{\mathrm{OUT}}=\frac{I_{S 2}}{I_{S 1}} I_{C 1}=\left(\frac{I_{S 2}}{I_{S 1}} I_{\mathrm{IN}}\right)\left(\frac{1}{1+\frac{1+\left(I_{S 2} / I_{S 1}\right)}{\beta_{F}}}\right) \tag{4.6}
\end{equation*}
$$

When $I_{S 2}=I_{S 1}$, (4.6) is the same as (4.4). Since the saturation current of a bipolar transistor is proportional to its emitter area, the first term in (4.6) shows that the gain of the current mirror can be larger or smaller than unity because the emitter areas can be ratioed. If the desired current-mirror gain is a rational number, $M / N$, the area ratio is usually set by connecting $M$ identical devices called units in parallel to form $Q_{2}$ and $N$ units in parallel to form $Q_{1}$ to minimize mismatch arising from lithographic effects in forming the emitter regions. However, area ratios greater than about five to one consume a large die area dominated by the area of the larger of the two devices. Thus other methods described in later sections are preferred for the generation of large current ratios. The last term in (4.6) accounts for error introduced by finite $\beta_{F}$. Increasing $I_{S 2} / I_{S 1}$ increases the magnitude of this error by increasing the base current of $Q_{2}$ compared to that of $Q_{1}$.

In writing (4.1) and (4.2), we assumed that the collector currents of the transistors are independent of their collector-emitter voltages. If a transistor is biased in the forward-active region, its collector current actually increases slowly with increasing collector-emitter voltage. Fig. 4.3 shows an output characteristic for $Q_{2}$. The output resistance of the current mirror at any given operating point is the reciprocal of the slope of the output characteristic at that point. In the forward-active region,

$$
\begin{equation*}
R_{o}=r_{o 2}=\frac{V_{A}}{I_{C 2}} \tag{4.7}
\end{equation*}
$$

image_name:Figure 4.3 npn output characteristic
description:The graph in Figure 4.3 is an output characteristic curve for an NPN transistor, specifically for $Q_{2}$. This graph is a plot of the collector current ($I_{OUT} = I_{C2}$) on the vertical axis against the collector-emitter voltage ($V_{OUT} = V_{CE2}$) on the horizontal axis.

1. **Axes Labels and Units:**
- The vertical axis represents the output current ($I_{OUT} = I_{C2}$) with no specific units marked, but typically measured in amperes (A).
- The horizontal axis represents the output voltage ($V_{OUT} = V_{CE2}$) with no specific units marked, but typically measured in volts (V).
- The graph uses a linear scale for both axes.

2. **Overall Behavior and Trends:**
- The graph shows a characteristic curve typical of a transistor in the forward-active region.
- Initially, as $V_{OUT}$ increases from negative values, $I_{OUT}$ remains low and constant, indicating the cutoff region.
- As $V_{OUT}$ reaches a certain threshold ($V_{CE1}$), the current begins to increase, marking the transition to the active region.
- In the active region, the curve becomes linear, indicating that $I_{OUT}$ increases with $V_{OUT}$ but at a slower rate, due to the transistor being in the forward-active region.

3. **Key Features and Technical Details:**
- The point where $V_{BE2} = V_{BE1}$ and $V_{CE2} = V_{CE1}$ is marked on the graph. At this point, the collector current $I_{C2}$ is defined as $\left(\frac{I_{S2}}{I_{S1}}\right) I_{C1}$.
- The slope of the characteristic line in the active region is related to the output resistance of the current mirror, which can be calculated as $R_{o}=\frac{V_{A}}{I_{C2}}$.
- The dashed line extending from the origin through the active region represents the linear approximation of $I_{C2}$ for changes in $V_{CE2}$.

4. **Annotations and Specific Data Points:**
- The graph includes a dashed line showing the relationship between $I_{C2}$ and $V_{CE2}$, with a specific reference point where $I_{C2} = \left(\frac{I_{S2}}{I_{S1}}\right) I_{C1}$.
- The negative voltage point $-V_{A}$ on the horizontal axis is marked, indicating the voltage level before the transistor enters the active region.

This graph provides a visual representation of the transistor's behavior in different regions of operation, particularly highlighting the transition from cutoff to active regions and the linear relationship in the forward-active region.

Figure 4.3 npn output characteristic.

The point where $V_{C E 2}=V_{C E 1}$ and $V_{B E 2}=V_{B E 1}$ is labeled on the characteristic. Because the collector current is controlled by the base-emitter and collector-emitter voltages, $I_{C 2}=$ $\left(I_{S 2} / I_{S 1}\right) I_{C 1}$ at this point. If the slope of the characteristic in saturation is constant, the variation in $I_{C 2}$ for changes in $V_{C E 2}$ can be predicted by a straight line that goes through the labeled point. As described in Chapter 1, extrapolation of the output characteristic in the forward-active region back to the $V_{C E 2}$ axis gives an intercept at $-V_{A}$, where $V_{A}$ is the Early voltage. If $V_{A} \gg V_{C E 1}$, the slope of the straight line is about equal to $\left(I_{S 2} / I_{S 1}\right)\left(I_{C 1} / V_{A}\right)$. Therefore,

$$
\begin{equation*}
I_{\mathrm{OUT}}=\frac{I_{S 2}}{I_{S 1}} I_{C 1}\left(1+\frac{V_{C E 2}-V_{C E 1}}{V_{A}}\right)=\frac{\frac{I_{S 2}}{I_{S 1}} I_{\mathrm{IN}}\left(1+\frac{V_{C E 2}-V_{C E 1}}{V_{A}}\right)}{1+\frac{1+\left(I_{S 2} / I_{S 1}\right)}{\beta_{F}}} \tag{4.8}
\end{equation*}
$$

Since the ideal gain of the current mirror is $I_{S 2} / I_{S 1}$, the systematic gain error, $\epsilon$, of the current mirror can be calculated from (4.8).

$$
\begin{equation*}
\epsilon=\left(\frac{1+\frac{V_{C E 2}-V_{C E 1}}{V_{A}}}{1+\frac{1+\left(I_{S 2} / I_{S 1}\right)}{\beta_{F}}}\right)-1 \simeq \frac{V_{C E 2}-V_{C E 1}}{V_{A}}-\frac{1+\left(I_{S 2} / I_{S 1}\right)}{\beta_{F}} \tag{4.9}
\end{equation*}
$$

The first term in (4.9) stems from finite output resistance and the second term from finite $\beta_{F}$. If $V_{C E 2}>V_{C E 1}$, the polarities of the two terms are opposite. Since the two terms are independent, however, cancellation is unlikely in practice. The first term dominates when the difference in the collector-emitter voltages and $\beta_{F}$ are large. For example, with identical transistors and $V_{A}=130 \mathrm{~V}$, if the collector-emitter voltage of $Q_{1}$ is held at $V_{B E(\mathrm{on})}$, and if the collectoremitter voltage of $Q_{2}$ is 30 V , then the systematic gain error $(30-0.6) / 130-2 / 200 \simeq 0.22$. Thus for a circuit operating at a power-supply voltage of 30 V , the current-mirror currents can differ by more than 20 percent from those values calculated by assuming that the transistor output resistance and $\beta_{F}$ are infinite. Although the first term in (4.9) stems from finite output resistance, it does not depend on $r_{o 2}$ directly but instead on the collector-emitter and Early voltages. The Early voltage is independent of the bias current, and

$$
\begin{equation*}
V_{\mathrm{IN}}=V_{C E 1}=V_{B E 1}=V_{B E(\mathrm{on})} \tag{4.10}
\end{equation*}
$$

Since $V_{B E(\text { on })}$ is proportional to the natural logarithm of the collector current, $V_{\text {IN }}$ changes little with changes in bias current. Therefore, changing the bias current in a current mirror changes systematic gain error mainly through changes in $V_{C E 2}$.

Finally, the minimum output voltage required to keep $Q_{2}$ in the forward-active region is

$$
\begin{equation*}
V_{\mathrm{OUT}(\mathrm{~min})}=V_{\text {CE2(sat) }} \tag{4.11}
\end{equation*}
$$

#### 4.2.2.2 MOS

Figure 4.4 shows an MOS version of the simple current mirror. The drain-gate voltage of $M_{1}$ is zero; therefore, the channel does not exist at the drain, and the transistor operates in the saturation or active region if the threshold is positive. Although the principle of operation for MOS transistors does not involve forward biasing any diodes, $M_{1}$ is said to be diode connected in an analogy to the bipolar case. Assume that $M_{2}$ also operates in the active region and that both transistors have infinite output resistance. Then $I_{D 2}$ is controlled by $V_{G S 2}$, which is equal to $V_{G S 1}$ by KVL. A KVL equation is at the heart of the operation of all current mirrors. As described in Section 1.5.3, the gate-source voltage of a given MOS transistor is usually
image_name:Figure 4.4 A simple MOS current mirror
description:
[
name: M1, type: NMOS, ports: {S: GND, D: VIN, G: VIN}
name: M2, type: NMOS, ports: {S: GND, D: VOUT, G: VIN}
name: I_IN, type: CurrentSource, value: I_IN, ports: {Np: VDD, Nn: VIN}
name: V_DD, type: VoltageSource, value: V_DD, ports: {Np: VDD, Nn: GND}
]
extrainfo:This circuit is a simple MOS current mirror. The current I_OUT equals I_D2 and is controlled by the gate-source voltage V_GS2, which is equal to V_GS1. M1 is diode-connected, and both transistors are assumed to have infinite output resistance.

Figure 4.4 A simple MOS current mirror.
separated into two parts: the threshold $V_{t}$ and the overdrive $V_{o v}$. Assuming square-law behavior as in (1.157), the overdrive for $M_{2}$ is

$$
\begin{equation*}
V_{o v 2}=V_{G S 2}-V_{t}=\sqrt{\frac{2 I_{D 2}}{k^{\prime}(W / L)_{2}}} \tag{4.12}
\end{equation*}
$$

Since the transconductance parameter $k^{\prime}$ is proportional to mobility, and since mobility falls with increasing temperature, the overdrive rises with temperature. In contrast, Section 1.5.4 shows that the threshold falls with increasing temperature. From KVL and (1.157),

$$
\begin{equation*}
V_{G S 2}=V_{t}+\sqrt{\frac{2 I_{D 2}}{k^{\prime}(W / L)_{2}}}=V_{G S 1}=V_{t}+\sqrt{\frac{2 I_{D 1}}{k^{\prime}(W / L)_{1}}} \tag{4.13}
\end{equation*}
$$

Equation 4.13 shows that the overdrive of $M_{2}$ is equal to that of $M_{1}$.

$$
\begin{equation*}
V_{o v 2}=V_{o v 1}=V_{o v} \tag{4.14}
\end{equation*}
$$

If the transistors are identical, $(W / L)_{2}=(W / L)_{1}$, and therefore

$$
\begin{equation*}
I_{\mathrm{OUT}}=I_{D 2}=I_{D 1} \tag{4.15}
\end{equation*}
$$

Equation 4.15 shows that the current that flows in the drain of $M_{1}$ is mirrored to the drain of $M_{2}$. Since $\beta_{F} \rightarrow \infty$ for MOS transistors, (4.15) and KCL at the drain of $M_{1}$ yield

$$
\begin{equation*}
I_{\mathrm{OUT}}=I_{D 1}=I_{\mathrm{IN}} \tag{4.16}
\end{equation*}
$$

Thus for identical devices operating in the active region with infinite output resistance, the gain of the current mirror is unity. This result holds when the gate currents are zero; that is, (4.16) is at least approximately correct for dc and low-frequency ac currents. As the input frequency increases, however, the gate currents of $M_{1}$ and $M_{2}$ increase because each transistor has a nonzero gate-source capacitance. The part of the input current that flows into the gate leads does not flow into the drain of $M_{1}$ and is not mirrored to $M_{2}$; therefore, the gain of the current mirror decreases as the frequency of the input current increases. The rest of this section considers dc currents only.

In practice, the devices need not be identical. Then from (4.13) and (4.16),

$$
\begin{equation*}
I_{\mathrm{OUT}}=\frac{(W / L)_{2}}{(W / L)_{1}} I_{D 1}=\frac{(W / L)_{2}}{(W / L)_{1}} I_{\mathrm{IN}} \tag{4.17}
\end{equation*}
$$

Equation 4.17 shows that the gain of the current mirror can be larger or smaller than unity because the transistor sizes can be ratioed. To ratio the transistor sizes, either the widths or the lengths can be made unequal in principle. In practice, however, the lengths of $M_{1}$ and $M_{2}$ are rarely made unequal. The lengths that enter into (4.17) are the effective channel lengths given by (2.35). Equation 2.35 shows that the effective channel length of a given transistor differs from its drawn length by offset terms stemming from the depletion region at the drain and lateral diffusion at the drain and source. Since the offset terms are independent of the drawn length, a ratio of two effective channel lengths is equal to the drawn ratio only if the drawn lengths are identical. As a result, a ratio of unequal channel lengths depends on process parameters that may not be well controlled in practice. Similarly, Section 2.9.1 shows that the effective width of a given transistor differs from the drawn width because of lateral oxidation resulting in a bird's beak. Therefore, a ratio of unequal channel widths will also be process dependent. In many applications, however, the shortest channel length allowed in a given technology is selected for most transistors to maximize speed and minimize area. In contrast, the drawn channel widths are usually many times larger than the minimum dimensions allowed in a given technology. Therefore, to minimize the effect of the offset terms when the current-mirror gain is designed to differ from unity, the widths are ratioed rather than the lengths in most practical cases. If the desired current-mirror gain is a rational number, $M / N$, the ratio is usually set by connecting $M$ identical devices called units in parallel to form $M_{2}$ and $N$ units in parallel to form $M_{1}$ to minimize mismatch arising from lithographic effects in forming the gate regions. As in the bipolar case, ratios greater than about five to one consume a large die area dominated by the area of the larger of the two devices. Thus other methods described in later sections are preferred for the generation of large current ratios.

In writing (4.13) and (4.15), we assumed that the drain currents of the transistors are independent of their drain-source voltages. If a transistor is biased in the active region, its drain current actually increases slowly with increasing drain-source voltage. Figure 4.5 shows an output characteristic for $M_{2}$. The output resistance of the current mirror at any given operating point is the reciprocal of the slope of the output characteristic at that point. In the active region,

$$
\begin{equation*}
R_{o}=r_{o 2}=\frac{V_{A}}{I_{D 2}}=\frac{1}{\lambda I_{D 2}} \tag{4.18}
\end{equation*}
$$

The point where $V_{D S 2}=V_{D S 1}$ and $V_{G S 2}=V_{G S 1}$ is labeled on the characteristic. Because the drain current is controlled by the gate-source and drain-source voltages, $I_{D 2}=$ $\left[(W / L)_{2} /(W / L)_{1}\right] I_{D 1}$ at this point. If the slope of the characteristic in saturation is constant, the variation in $I_{D 2}$ for changes in $V_{D S 2}$ can be predicted by a straight line that goes through the
image_name:Figure 4.5 Output characteristic of simple MOS current mirror
description:The graph depicted is a characteristic curve of a simple MOS current mirror, labeled as Figure 4.5. It is a plot showing the relationship between the output current, \( I_{OUT} = I_{D2} \), and the output voltage, \( V_{OUT} = V_{DS2} \).

1. **Type of Graph and Function**:
- This is an output characteristic graph of a MOS current mirror.

2. **Axes Labels and Units**:
- The vertical axis represents the output current \( I_{OUT} = I_{D2} \).
- The horizontal axis represents the output voltage \( V_{OUT} = V_{DS2} \).
- The units are not specified, but typically they would be in amperes for current and volts for voltage.

3. **Overall Behavior and Trends**:
- The graph starts with a sharp increase in current as the voltage increases from zero, indicating the initial linear region.
- After the initial rise, the curve reaches a saturation region where the current remains relatively constant despite further increases in voltage.
- The curve is generally flat in the saturation region, indicating that the current is stable and controlled by the gate-source voltage.

4. **Key Features and Technical Details**:
- The point where the curve transitions from the linear region to the saturation region is marked, showing the intersection at \( V_{DS1} \).
- The current at this point is given by \( \frac{(W/L)_2}{(W/L)_1} I_{D1} \), illustrating the scaling of current in the mirror.
- The gate-source voltages are equal at this point, denoted as \( V_{GS2} = V_{GS1} \).

5. **Annotations and Specific Data Points**:
- A specific point on the curve is marked to indicate the equal gate-source voltages and the corresponding current scaling.
- The slope of the line in the saturation region is constant, implying a linear relationship in this part of the characteristic.

This graph effectively demonstrates the behavior of a MOS current mirror, highlighting the relationship between the output current and voltage, and the impact of the gate-source voltage on the current stability in the saturation region.

Figure 4.5 Output characteristic of simple MOS current mirror.
labeled point. As described in Chapter 1, extrapolation of the output characteristic in the active region back to the $V_{D S 2}$ axis gives an intercept at $-V_{A}=-1 / \lambda$, where $V_{A}$ is the Early voltage. If $V_{A} \gg V_{D S 1}$, the slope of the straight line is about equal to $\left[(W / L)_{2} /(W / L)_{1}\right]\left[I_{D 1} / V_{A}\right]$. Therefore,

$$
\begin{equation*}
I_{\mathrm{OUT}}=\frac{(W / L)_{2}}{(W / L)_{1}} I_{\mathrm{IN}}\left(1+\frac{V_{D S 2}-V_{D S 1}}{V_{A}}\right) \tag{4.19}
\end{equation*}
$$

Since the ideal gain of the current mirror is $(W / L)_{2} /(W / L)_{1}$, the systematic gain error, $\epsilon$, of the current mirror can be calculated from (4.19).

$$
\begin{equation*}
\epsilon=\frac{V_{D S 2}-V_{D S 1}}{V_{A}} \tag{4.20}
\end{equation*}
$$

For example, if the drain-source voltage of $M_{1}$ is held at 1.2 V , and if the drain-source voltage of $M_{2}$ is 5 V , then the systematic gain error is $(5-1.2) / 10 \simeq 0.38$ with $V_{A}=10 \mathrm{~V}$. Thus for a circuit operating at a power-supply voltage of 5 V , the current-mirror currents can differ by more than 35 percent from those values calculated by assuming that the transistor output resistance is infinite. Although $\epsilon$ stems from finite output resistance, it does not depend on $r_{o 2}$ directly but instead on the drain-source and Early voltages. Since the Early voltage is independent of the bias current, this observation shows that changing the input bias current in a current mirror changes systematic gain error mainly through changes to the drain-source voltages.

For the simple MOS current mirror, the input voltage is

$$
\begin{equation*}
V_{\mathrm{IN}}=V_{G S 1}=V_{t}+V_{o v 1}=V_{t}+V_{o v} \tag{4.21}
\end{equation*}
$$

With square-law behavior, the overdrive in (4.21) is proportional to the square root of the input current. In contrast, (4.10) shows that the entire $V_{\text {IN }}$ in a simple bipolar mirror is proportional to the natural logarithm of the input current. Therefore, for a given change in the input current, the variation in $V_{\mathrm{IN}}$ in a simple MOS current mirror is generally larger than in its bipolar counterpart.

Finally, the minimum output voltage required to keep $M_{2}$ in the active region is

$$
\begin{equation*}
V_{\mathrm{OUT}(\min )}=V_{o v 2}=V_{o v}=\sqrt{\frac{2 I_{\mathrm{OUT}}}{k^{\prime}(W / L)_{2}}} \tag{4.22}
\end{equation*}
$$

Equation 4.22 predicts that $V_{\text {OUT }(\min )}$ depends on the transistor geometry and can be made arbitrarily small in a simple MOS mirror, unlike in the bipolar case. However, if the overdrive predicted by (4.22) is less than $2 n V_{T}$, where $n$ is defined in (1.247) and $V_{T}$ is a thermal voltage, the result is invalid except to indicate that the transistors operate in weak inversion. At room temperature with $n=1.5,2 n V_{T} \simeq 78 \mathrm{mV}$. If the transistors operate in weak inversion,

$$
\begin{equation*}
V_{\text {OUT }(\min )} \simeq 3 V_{T} \tag{4.23}
\end{equation*}
$$

as shown in Fig. 1.43. ${ }^{1}$

### 4.2.3 Simple Current Mirror with Beta Helper

#### 4.2.3.1 Bipolar

In addition to the variation in output current due to finite output resistance, the second term in (4.9) shows that the collector current $I_{C 2}$ differs from the input current because of finite $\beta_{F}$. To reduce this source of error, an additional transistor can be added, as shown in Fig. 4.6. If $Q_{1}$ and $Q_{3}$ are identical, the emitter current of transistor $Q_{2}$ is

$$
\begin{equation*}
I_{E 2}=-\frac{I_{C 1}}{\beta_{F}}-\frac{I_{C 3}}{\beta_{F}}=-\frac{2}{\beta_{F}} I_{C 1} \tag{4.24}
\end{equation*}
$$

image_name:Figure 4.6 Simple current mirror with beta helper
description:
[
name: Q1, type: NPN, ports: {C: VIN, B: VCC, E: GND}
name: Q2, type: NPN, ports: {C: VCC, B: VCC, E: bie2b3}
name: Q3, type: NPN, ports: {C: VOUT, B: bie2b3, E: GND}
name: I_IN, type: CurrentSource, value: I_IN, ports: {Np: VCC, Nn: VIN}
]
extrainfo:This circuit is a simple current mirror with a beta helper. It consists of three NPN transistors and a current source. The circuit is designed to improve the accuracy of the current mirror by reducing the error caused by finite beta (βF) of the transistors.

Figure 4.6 Simple current mirror with beta helper.
where $I_{E}, I_{C}$, and $I_{B}$ are defined as positive when flowing into the transistor, and where we have neglected the effects of finite output resistance. The base current of transistor $Q_{2}$ is equal to

$$
\begin{equation*}
I_{B 2}=-\frac{I_{E 2}}{\beta_{F}+1}=\frac{2}{\beta_{F}\left(\beta_{F}+1\right)} I_{C 1} \tag{4.25}
\end{equation*}
$$

Finally, KCL at the collector of $Q_{1}$ gives

$$
\begin{equation*}
I_{\mathrm{IN}}-I_{C 1}-\frac{2}{\beta_{F}\left(\beta_{F}+1\right)} I_{C 1}=0 \tag{4.26}
\end{equation*}
$$

Since $I_{C 1}$ and $I_{C 3}$ are equal when $Q_{1}$ and $Q_{3}$ are identical,

$$
\begin{equation*}
I_{\mathrm{OUT}}=I_{C 3}=\frac{I_{\mathrm{IN}}}{1+\frac{2}{\beta_{F}\left(\beta_{F}+1\right)}} \simeq I_{\mathrm{IN}}\left(1-\frac{2}{\beta_{F}\left(\beta_{F}+1\right)}\right) \tag{4.27}
\end{equation*}
$$

Equation 4.27 shows that the systematic gain error from finite $\beta_{F}$ has been reduced by a factor of $\left[\beta_{F}+1\right]$, which is the current gain of emitter follower $Q_{2}$. As a result, $Q_{2}$ is often referred to as a beta helper.

Although the beta helper has little effect on the output resistance and the minimum output voltage of the current mirror, it increases the input voltage by the base-emitter voltage of $Q_{2}$ :

$$
\begin{equation*}
V_{\mathrm{IN}}=V_{B E 1(\mathrm{on})}+V_{B E 2(\mathrm{on})} \tag{4.28}
\end{equation*}
$$

If multiple emitter followers are cascaded to further reduce the gain error arising from finite $\beta_{F}, V_{\text {IN }}$ increases by an extra base-emitter voltage for each additional emitter follower, posing one limit to the use of cascaded emitter followers.

Current mirrors often use a beta helper when they are constructed with pnp transistors because the value of $\beta_{F}$ for $p n p$ transistors is usually less than for npn transistors. Another application of the beta-helper configuration is in current mirrors with multiple outputs. An example with two independent outputs is shown in Fig. 4.7. At first, ignore $Q_{2}$ and imagine that $Q_{1}$ is simply diode connected. Also, let $R_{1}=R_{3}=R_{4}=0$ here. (The effects of nonzero resistances will be considered in Section 4.2.4.) Then the gain from the input to each output is primarily determined by the area ratios $I_{S 3} / I_{S 1}$ and $I_{S 4} / I_{S 1}$. Because the bases of three instead of two transistors are connected together, the total base current is increased here, which increases the gain error from the input to either output arising from finite $\beta_{F}$. Furthermore, the
image_name:Figure 4.7 Simple current mirror with beta helper, multiple outputs, and emitter degeneration
description:
[
name: I_IN, type: CurrentSource, value: I_IN, ports: {Np: Vcc, Nn: C1b2}
name: Q1, type: NPN, ports: {C: C1b2, B: E2b1b3b4, E: e1}
name: Q2, type: NPN, ports: {C: Vcc, B: C1b2, E: E2b1b3b4}
name: Q3, type: NPN, ports: {C: LOAD1, B: E2b1b3b4, E: e3}
name: Q4, type: NPN, ports: {C: LOAD2, B: E2b1b3b4, E: e4}
name: R1, type: Resistor, value: R1, ports: {N1: e1, N2: GND}
name: R3, type: Resistor, value: R3, ports: {N1: e3, N2: GND}
name: R4, type: Resistor, value: R4, ports: {N1: e4, N2: GND}
]
extrainfo:This circuit is a simple current mirror with a beta helper (Q2) and multiple outputs (Q3, Q4). The beta helper reduces the gain error due to finite beta (βF) by a factor of [βF + 1]. The resistors R1, R3, and R4 are set to zero in this analysis. The gain from input to each output is determined by the area ratios IS3/IS1 and IS4/IS1. The total base current is increased due to the bases of three transistors being connected, which increases the gain error.

Figure 4.7 Simple current mirror with beta helper, multiple outputs, and emitter degeneration.
gain errors worsen as the number of independent outputs increases. Since the beta helper, $Q_{2}$, reduces the gain error from the input to each output by a factor of $\left[\beta_{F}+1\right]$, it is often used in bipolar current mirrors with multiple outputs.

#### 4.2.3.2 MOS

Since $\beta_{F} \rightarrow \infty$ for an MOS transistor, beta helpers are not used in simple MOS current mirrors to reduce the systematic gain error. However, a beta-helper configuration can increase the bandwidth of MOS and bipolar current mirrors.

### 4.2.4 Simple Current Mirror with Degeneration

#### 4.2.4.1 Bipolar

The performance of the simple bipolar transistor current mirror of Fig. 4.6 can be improved by the addition of emitter degeneration as shown in Fig. 4.7 for a current mirror with two independent outputs. The purpose of the emitter resistors is twofold. First, Appendix A.4.1 shows that the matching between $I_{\mathrm{IN}}$ and outputs $I_{C 3}$ and $I_{C 4}$ can be greatly improved by using emitter degeneration. Second, as shown in Section 3.3.8, the use of emitter degeneration boosts the output resistance of each output of the current mirror. Transistors $Q_{1}$ and $Q_{2}$ combine to present a very low resistance at the bases of $Q_{3}$ and $Q_{4}$. Therefore, from (3.99), the small-signal output resistance seen at the collectors of $Q_{3}$ and $Q_{4}$ is

$$
\begin{equation*}
R_{o} \simeq r_{o}\left(1+g_{m} R_{E}\right) \tag{4.29}
\end{equation*}
$$

if $r_{\pi} \gg R_{E}$. Taking $Q_{3}$ as an example and using $g_{m 3}=I_{C 3} / V_{T}$, we find

$$
\begin{equation*}
R_{o} \simeq r_{o 3}\left(1+\frac{I_{C 3} R_{3}}{V_{T}}\right) \tag{4.30}
\end{equation*}
$$

This increase in the output resistance for a given output current also decreases the component of systematic gain error that stems from finite output resistance by the same factor. From (4.9) and (4.30) with infinite $\beta_{F}$,

$$
\begin{equation*}
\epsilon \simeq \frac{V_{C E 2}-V_{C E 1}}{V_{A}\left(1+\frac{I_{C 3} R_{3}}{V_{T}}\right)} \tag{4.31}
\end{equation*}
$$

The quantity $I_{C 3} R_{3}$ is just the dc voltage drop across $R_{3}$. If this quantity is 260 mV , for example, then $R_{o}$ is about $10 r_{o}$ at room temperature, and $\epsilon$ is reduced by a factor of about eleven. Unfortunately, this improvement in $R_{o}$ is limited by corresponding increases in the input and minimum output voltages of the mirror:

$$
\begin{equation*}
V_{\mathrm{IN}} \simeq V_{B E 1(\mathrm{on})}+V_{B E 2(\mathrm{on})}+I_{\mathrm{IN}} R_{1} \tag{4.32}
\end{equation*}
$$

and

$$
\begin{equation*}
V_{\mathrm{OUT}(\mathrm{~min})}=V_{C E 3(\mathrm{sat})}+I_{C 3} R_{3} \tag{4.33}
\end{equation*}
$$

The emitter areas of $Q_{1}, Q_{3}$, and $Q_{4}$ may be matched or ratioed. For example, if we want $I_{\text {OUT } 1}=I_{\mathrm{IN}}$ and $I_{\text {OUT2 }}=2 I_{\mathrm{IN}}$, we would make $Q_{3}$ identical to $Q_{1}$, and $Q_{4}$ consist of two copies of $Q_{1}$ connected in parallel so that $I_{S 4}=2 I_{S 1}$. In addition, we could make $R_{3}=R_{1}$, and $R_{4}$ consist of two copies of $R_{1}$ connected in parallel so that $R_{4}=R_{1} / 2$. Note that all the dc voltage drops across $R_{1}, R_{3}$, and $R_{4}$ would then be equal. Using KVL around the loop including $Q_{1}$ and $Q_{4}$ and neglecting base currents, we find

$$
\begin{equation*}
I_{C 1} R_{1}+V_{T} \ln \frac{I_{C 1}}{I_{S 1}}=I_{C 4} R_{4}+V_{T} \ln \frac{I_{C 4}}{I_{S 4}} \tag{4.34}
\end{equation*}
$$

from which

$$
\begin{equation*}
I_{\mathrm{OUT} 2}=I_{C 4}=\frac{1}{R_{4}}\left(I_{\mathrm{IN}} R_{1}+V_{T} \ln \frac{I_{\mathrm{IN}}}{I_{C 4}} \frac{I_{S 4}}{I_{S 1}}\right) \tag{4.35}
\end{equation*}
$$

Since $I_{S 4}=2 I_{S 1}$, the solution to (4.35) is

$$
\begin{equation*}
I_{\mathrm{OUT} 2}=\frac{R_{1}}{R_{4}} I_{\mathrm{IN}}=2 I_{\mathrm{IN}} \tag{4.36}
\end{equation*}
$$

because the last term in (4.35) goes to zero. If we make the voltage drops $I_{\text {IN }} R_{1}$ and $I_{C 4} R_{4}$ much greater than $V_{T}$, the current-mirror gain to the $Q_{4}$ output is determined primarily by the resistor ratio $R_{4} / R_{1}$, and only to a secondary extent by the emitter area ratio, because the natural log term in (4.35) varies slowly with its argument.

#### 4.2.4.2 MOS

Source degeneration is rarely used in MOS current mirrors because, in effect, MOS transistors are inherently controlled resistors. Thus, matching in MOS current mirrors is improved simply by increasing the gate areas of the transistors. ${ }^{2,3,4}$ Furthermore, the output resistance can be increased by increasing the channel length. To increase the output resistance while keeping the current and $V_{G S}-V_{t}$ constant, the $W / L$ ratio must be held constant. Therefore, the channel width must be increased as much as the length, and the price paid for the improved output resistance is that increased chip area is consumed by the current mirror.

### 4.2.5 Cascode Current Mirror

#### 4.2.5.1 Bipolar

Section 3.4.2 shows that the cascode connection achieves a very high output resistance. Since this is a desirable characteristic for a current mirror, exploring the use of cascodes for highperformance current mirrors is natural. A bipolar-transistor current mirror based on the cascode connection is shown in Fig. 4.8. Transistors $Q_{3}$ and $Q_{1}$ form a simple current mirror, and emitter resistances can be added to improve the matching. Transistor $Q_{2}$ acts as the common-base part of the cascode and transfers the collector current of $Q_{1}$ to the output while presenting a high
image_name:Figure 4.8
description:
[
name: Q1, type: NPN, ports: {C: VOUT, B: X, E: GND}
name: Q2, type: NPN, ports: {C: VOUT, B: VIN, E: X}
name: Q3, type: NPN, ports: {C: X, B: VIN, E: GND}
name: Q4, type: NPN, ports: {C: VIN, B: VIN, E: X}
name: I_IN, type: CurrentSource, value: I_IN, ports: {Np: VCC, Nn: VIN}
name: C_e2, type: Capacitor, value: C_e2, ports: {Np: X, Nn: GND}
]
extrainfo:The circuit is a cascode current mirror with bipolar transistors. Q3 and Q1 form the basic current mirror, while Q2 and Q4 provide cascode operation for high output resistance. The current source I_IN provides the input current, and C_e2 is used for stability or compensation.

Figure 4.8 Cascode current mirror with bipolar transistors.
output resistance. Transistor $Q_{4}$ acts as a diode level shifter and biases the base of $Q_{2}$ so that $Q_{1}$ operates in the forward-active region with $V_{C E 1} \simeq V_{C E 3}=V_{B E 3(\text { on })}$. If we assume that the small-signal resistances of diodes $Q_{3}$ and $Q_{4}$ are small, a direct application of (3.98) with $R_{E}=r_{o 1}$ concludes that

$$
\begin{equation*}
R_{o}=r_{o 2}\left(1+\frac{g_{m 2} r_{o 1}}{1+\frac{g_{m 2} r_{o 1}}{\beta_{0}}}\right) \simeq \beta_{0} r_{o 2} \tag{4.37}
\end{equation*}
$$

because $g_{m 2} r_{o 1} \simeq g_{m 1} r_{o 1} \gg \beta_{0}$. This calculation assumes that almost all of the small-signal current that flows into the collector of $Q_{2}$ flows out its base because the small-signal resistance connected to the emitter of $Q_{2}$ is much greater than that connected to its base. A key problem with this calculation, however, is that it ignores the effect of the simple current mirror formed by $Q_{3}$ and $Q_{1}$. Let $i_{b 2}$ and $i_{e 2}$ represent increases in the base and emitter currents flowing out of $Q_{2}$ caused by increasing output voltage. Then the simple mirror forces $i_{e 2} \simeq i_{b 2}$. As a result, the variation in the collector current of $Q_{2}$ splits into two equal parts and half flows in $r_{\pi 2}$. A small-signal analysis shows that $R_{o}$ in (4.37) is reduced by half to

$$
\begin{equation*}
R_{o} \simeq \frac{\beta_{0} r_{o 2}}{2} \tag{4.38}
\end{equation*}
$$

Thus, the cascode configuration boosts the output resistance by approximately $\beta_{0} / 2$. For $\beta_{0}=100, V_{A}=130 \mathrm{~V}$, and $I_{C 2}=1 \mathrm{~mA}$,

$$
\begin{equation*}
R_{o}=\frac{\beta_{0} V_{A}}{2 I_{C 2}}=\frac{100(130)}{2 \mathrm{~mA}}=6.5 \mathrm{M} \Omega \tag{4.39}
\end{equation*}
$$

In this calculation of output resistance, we have neglected the effects of $r_{\mu}$. Although this assumption is easy to justify in the case of the simple current mirror, it must be reexamined here because the output resistance is so high. The collector-base resistance $r_{\mu}$ results from modulation of the base-recombination current as a consequence of the Early effect, as described in Chapter 1. For a transistor whose base current is composed entirely of base-recombination current, the percentage change in base current when $V_{C E}$ is changed at a constant $V_{B E}$ would equal that of the collector current, and $r_{\mu}$ would be equal to $\beta_{0} r_{0}$. In this case, the effect of
$r_{\mu}$ would be to reduce the output resistance of the cascode current mirror given in (4.38) by a factor of 1.5 .

In actual integrated-circuit npn transistors, however, only a small percentage of the base current results from recombination in the base. Since only this component is modulated by the Early effect, the observed values of $r_{\mu}$ are a factor of 10 or more larger than $\beta_{0} r_{o}$. Therefore, $r_{\mu}$ has a negligible effect here with npn transistors. On the other hand, for lateral pnp transistors, the feedback resistance $r_{\mu}$ is much smaller than for $n p n$ transistors because most of the base current results from base-region recombination. The actual value of this resistance depends on a number of process and device-geometry variables, but observed values range from 2 to 5 times $\beta_{0} r_{0}$. Therefore, for a cascode current mirror constructed with lateral pnp transistors, the effect of $r_{\mu}$ on the output resistance can be significant. Furthermore, when considering current mirrors that give output resistances higher than $\beta_{0} r_{o}$, the effects of $r_{\mu}$ must be considered.

In the cascode current mirror, the base of $Q_{1}$ is connected to a low-resistance point because $Q_{3}$ is diode connected. As a result, feedback from $r_{\mu 1}$ is greatly attenuated and has negligible effect on the output resistance. On the other hand, if the resistance from the base of $Q_{1}$ to ground is increased while all other parameters are held constant, local feedback from $r_{\mu 1}$ significantly affects the base-emitter voltage of $Q_{1}$ and reduces the output resistance. In the limit where the resistance from the base of $Q_{1}$ to ground becomes infinite, $Q_{1}$ acts as if it were diode connected. Local feedback is considered in Chapter 8.

The input voltage of the cascode current mirror is

$$
\begin{equation*}
V_{\mathrm{IN}}=V_{B E 3}+V_{B E 4}=2 V_{B E(\text { on })} \tag{4.40}
\end{equation*}
$$

Although $V_{\text {IN }}$ is higher here than in (4.10) for a simple current mirror, the increase becomes a limitation only if the power-supply voltage is reduced to nearly two diode drops.

The minimum output voltage for which the output resistance is given by (4.38) must allow both $Q_{1}$ and $Q_{2}$ to be biased in the forward-active region. Since $V_{C E 1} \simeq V_{C E 3}=V_{B E(\text { on })}$,

$$
\begin{equation*}
V_{\mathrm{OUT}(\min )}=V_{C E 1}+V_{C E 2(\mathrm{sat})} \simeq V_{B E(\mathrm{on})}+V_{C E 2(\mathrm{sat})} \tag{4.41}
\end{equation*}
$$

Comparing (4.41) and (4.11) shows that the minimum output voltage for a cascode current mirror is higher than for a simple current mirror by a diode drop. This increase poses an important limitation on the minimum supply voltage when the current mirror is used as an active load for an amplifier.

Since $V_{C E 1} \simeq V_{C E 3}, I_{C 1} \simeq I_{C 3}$, and the systematic gain error arising from finite transistor output resistance is almost zero. A key limitation of the cascode current mirror, however, is that the systematic gain error arising from finite $\beta_{F}$ is worse than for a simple current mirror. From KCL at the collector of $Q_{3}$,

$$
\begin{equation*}
-I_{E 4}=I_{C 3}+\frac{2 I_{C 3}}{\beta_{F}} \tag{4.42}
\end{equation*}
$$

From KCL at the collector of $Q_{4}$,

$$
\begin{equation*}
I_{\mathrm{IN}}=-I_{E 4}+\frac{I_{C 2}}{\beta_{F}} \tag{4.43}
\end{equation*}
$$

The collector current of $Q_{2}$ is

$$
\begin{equation*}
I_{C 2}=\frac{\beta_{F}}{\beta_{F}+1} I_{C 3} \tag{4.44}
\end{equation*}
$$

Substituting (4.42) and (4.44) into (4.43) gives

$$
\begin{equation*}
I_{\mathrm{IN}}=I_{C 3}+\frac{2 I_{C 3}}{\beta_{F}}+\frac{I_{C 3}}{\beta_{F}+1} \tag{4.45}
\end{equation*}
$$

Rearranging (4.45) to find $I_{C 3}$ and substituting back into (4.44) gives

$$
\begin{equation*}
I_{\mathrm{OUT}}=I_{C 2}=\left(\frac{\beta_{F}}{\beta_{F}+1}\right)\left(\frac{I_{\mathrm{IN}}}{1+\frac{2}{\beta_{F}}+\frac{1}{\beta_{F}+1}}\right) \tag{4.46}
\end{equation*}
$$

Equation 4.46 can be rearranged to give

$$
\begin{equation*}
I_{\mathrm{OUT}}=I_{\mathrm{IN}}\left(1-\frac{4 \beta_{F}+2}{\beta_{F}^{2}+4 \beta_{F}+2}\right) \tag{4.47}
\end{equation*}
$$

Equation 4.47 shows that the systematic gain error is

$$
\begin{equation*}
\epsilon=-\frac{4 \beta_{F}+2}{\beta_{F}^{2}+4 \beta_{F}+2} \tag{4.48}
\end{equation*}
$$

When $\beta_{F} \gg 1$, (4.48) simplifies to

$$
\begin{equation*}
\epsilon \simeq-\frac{4}{\beta_{F}+4} \tag{4.49}
\end{equation*}
$$

In contrast, the systematic gain error stemming from finite $\beta_{F}$ in a simple current mirror with identical transistors is about $-2 / \beta_{F}$, which is less in magnitude than (4.49) predicts for a cascode current mirror if $\beta_{F}>4$. This limitation of a cascode current mirror is overcome by the Wilson current mirror described in Section 4.2.6.

### 4.2.5.2 MOS

The cascode current mirror is widely used in MOS technology, where it does not suffer from finite $\beta_{F}$ effects. Figure 4.9 shows the simplest form. From (3.107), the small-signal output resistance is

$$
\begin{equation*}
R_{o}=r_{o 2}\left[1+\left(g_{m 2}+g_{m b 2}\right) r_{o 1}\right]+r_{o 1} \tag{4.50}
\end{equation*}
$$

As shown in the previous section, the bipolar cascode current mirror cannot realize an output resistance larger than $\beta_{0} r_{o} / 2$ because $\beta_{0}$ is finite and nonzero small-signal base current flows in the cascode transistor. In contrast, the MOS cascode is capable of realizing arbitrarily high output resistance by increasing the number of stacked cascode devices because $\beta_{0} \rightarrow \infty$ for MOS transistors. However, the MOS substrate leakage current described in Section 1.9 can create a resistive shunt to ground from the output node, which can dominate the output resistance for $V_{\text {OUT }}>V_{\text {OUT(min) }}{ }^{5}$

#### EXAMPLE

Find the output resistance of the double-cascode current mirror shown in Fig. 4.10. Assume all the transistors operate in the active region with $I_{D}=10 \mu \mathrm{~A}, V_{A}=50 \mathrm{~V}$, and $g_{m} r_{o}=50$. Neglect body effect.

The output resistance of each transistor is

$$
r_{o}=\frac{V_{A}}{I_{D}}=\frac{50 \mathrm{~V}}{10 \mu \mathrm{~A}}=5 \mathrm{M} \Omega
$$

From (4.50), looking into the drain of $M_{2}$ :

$$
\begin{equation*}
R_{o 2}=r_{o 2}\left(1+g_{m 2} r_{o 1}\right)+r_{o 1} \tag{4.51}
\end{equation*}
$$

image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: VOUT, G: X}
name: M2, type: NMOS, ports: {S: X, D: d1s2, G: VIN}
name: M3, type: NMOS, ports: {S: GND, D: X, G: VIN}
name: M4, type: NMOS, ports: {S: VIN, D: VIN, G: VIN}
name: I_IN, type: CurrentSource, ports: {Np: VDD, Nn: VIN}
]
extrainfo:This circuit is a double-cascode current mirror using NMOS transistors. It is designed to provide a high output resistance and improve current matching. The circuit uses a current source I_IN to bias the transistors. The output current I_OUT is provided at the node VOUT.
image_name:(b)
description:The graph labeled (b) is an I-V characteristic plot, which depicts the relationship between the output current \( I_{OUT} \) and the output voltage \( V_{OUT} \) for a cascode current mirror circuit.

1. **Type of Graph and Function:**
- This is an I-V characteristic graph, commonly used to illustrate the behavior of electronic components such as transistors.

2. **Axes Labels and Units:**
- The x-axis represents the output voltage \( V_{OUT} \), although units are not explicitly mentioned, they are typically in volts.
- The y-axis represents the output current \( I_{OUT} \), typically in amperes.

3. **Overall Behavior and Trends:**
- The graph shows a curve that starts at the origin, indicating that as \( V_{OUT} \) increases, \( I_{OUT} \) initially rises steeply.
- After a certain point, the curve flattens, indicating that \( I_{OUT} \) becomes relatively constant with further increases in \( V_{OUT} \).
- This behavior suggests the transition from the triode region to the saturation region for the transistors involved.

4. **Key Features and Technical Details:**
- The curve begins at the origin and rises sharply, indicating the initial active region of the transistor \( M_1 \) while \( M_2 \) is in the triode region.
- As \( V_{OUT} \) increases past a certain threshold, noted as \( V_{OUT(min)} \), the curve levels off, indicating that both \( M_1 \) and \( M_2 \) are in the triode region.
- The point \( V_{ov1} \) marks the onset of the saturation region for \( M_1 \).

5. **Annotations and Specific Data Points:**
- The graph is annotated with regions: \( M_1 \) active, \( M_2 \) in the triode region, and both \( M_1 \) and \( M_2 \) in the triode region.
- The threshold \( V_{OUT(min)} \) is marked as a vertical dashed line, showing the minimum \( V_{OUT} \) required to maintain the desired current mirror operation.

This graph effectively demonstrates the transition of transistor operation regions in a cascode current mirror, highlighting the behavior of \( I_{OUT} \) as \( V_{OUT} \) varies.

Figure 4.9 (a) Cascode current mirror using MOS transistors. (b) I-V characteristic.
image_name:Figure 4.10 Example of a double-cascode current mirror
description:
[
name: M6, type: NMOS, ports: {S: GND, D: g3g6d6, G: g3g6d6}
name: M5, type: NMOS, ports: {S: g3g6d6, D: g2g5d5s5, G: g2g5d5s5}
name: M4, type: NMOS, ports: {S: g2g5d5s5, D: g1g4d4s5, G: g1g4d4s5}
name: M3, type: NMOS, ports: {S: s1d2, D: g3g6d6, G: g3g6d6}
name: M2, type: NMOS, ports: {S: d1s2, D: g2g5d5s5, G: g2g5d5s5}
name: M1, type: NMOS, ports: {S: GND, D: d1s2, G: g1g4d4s5}
name: I_IN, type: CurrentSource, ports: {Np: VDD, Nn: g3g6d6}
]
extrainfo:The circuit is a double-cascode current mirror using NMOS transistors. It has a high output impedance and is designed to provide a stable current output (I_OUT) to the load. The circuit uses a current source I_IN to bias the transistors.

Figure 4.10 Example of a double-cascode current mirror.

Similarly, looking into the drain of $M_{3}$ :

$$
\begin{equation*}
R_{o}=r_{o 3}\left[1+g_{m 3} R_{o 2}\right]+R_{o 2} \tag{4.52}
\end{equation*}
$$

Each cascode stage increases the output resistance by a factor of about $\left(1+g_{m} r_{o}\right)$. Therefore,

$$
\begin{equation*}
R_{o} \simeq r_{o}\left(1+g_{m} r_{o}\right)^{2} \simeq 5(51)^{2} \mathrm{M} \Omega \simeq 13 \mathrm{G} \Omega \tag{4.53}
\end{equation*}
$$

With such a large output resistance, other parasitic leakage paths, such as the substrate leakage path, could be comparable to this resistance in practice.

From KVL in Fig. 4.9,

$$
\begin{equation*}
V_{D S 1}=V_{G S 3}+V_{G S 4}-V_{G S 2} \tag{4.54}
\end{equation*}
$$

Since $V_{D S 3}=V_{G S 3}$, (4.54) shows that $V_{D S 1}=V_{D S 3}$ when $V_{G S 2}=V_{G S 4}$. Under this condition, the systematic gain error of the cascode current mirror is zero because $M_{1}$ and $M_{3}$ are identically biased, and because $\beta_{F} \rightarrow \infty$ for MOS transistors. In practice, $V_{G S 2}$ is not exactly equal to $V_{G S 4}$ even with perfect matching unless $V_{\text {OUT }}=V_{\mathrm{IN}}$ because of channel-length modulation. As a result, $V_{D S 1} \simeq V_{D S 3}$ and

$$
\begin{equation*}
\epsilon \simeq 0 \tag{4.55}
\end{equation*}
$$

The input voltage of the MOS cascode current mirror in Fig. 4.9 is

$$
\begin{align*}
V_{\mathrm{IN}} & =V_{G S 3}+V_{G S 4} \\
& =V_{t 3}+V_{o v 3}+V_{t 4}+V_{o v 4} \tag{4.56}
\end{align*}
$$

The input voltage here includes two gate-source drops, each composed of threshold and overdrive components. Ignoring the body effect and assuming the transistors all have equal overdrives,

$$
\begin{equation*}
V_{\mathrm{IN}}=2 V_{t}+2 V_{o v} \tag{4.57}
\end{equation*}
$$

Also, adding extra cascode levels increases the input voltage by another threshold and another overdrive component for each additional cascode. Furthermore, the body effect increases the threshold of all transistors with $V_{S B}>0$. Together, these facts increase the difficulty of designing the input current source for low power-supply voltages.

When $M_{1}$ and $M_{2}$ both operate in the active region, $V_{D S 1} \simeq V_{D S 3}=V_{G S 3}$. For $M_{2}$ to operate in the active region, $V_{D S 2}>V_{o v 2}$ is required. Therefore, the minimum output voltage for which $M_{1}$ and $M_{2}$ operate in the active region is

$$
\begin{align*}
V_{\mathrm{OUT}(\min )} & =V_{D S 1}+V_{o v 2} \\
& \simeq V_{G S 3}+V_{o v 2}=V_{t}+V_{o v 3}+V_{o v 2} \tag{4.58}
\end{align*}
$$

If the transistors all have equal overdrives,

$$
\begin{equation*}
V_{\mathrm{OUT}(\min )} \simeq V_{t}+2 V_{o v} \tag{4.59}
\end{equation*}
$$

On the other hand, $M_{2}$ operates in the triode region if $V_{\text {OUT }}<V_{\text {OUT }}$ min) , and both $M_{1}$ and $M_{2}$ operate in the triode region if $V_{\mathrm{OUT}}<V_{o v 1}$. These results are shown graphically in Fig. $4.9 b$.

Although the overdrive term in (4.59) can be made small by using large values of $W$ for a given current, the threshold term represents a significant loss of voltage swing when the current mirror is used as an active load in an amplifier. The threshold term in (4.59) stems from the biasing of the drain-source voltage of $M_{1}$ so that

$$
\begin{equation*}
V_{D S 1}=V_{\mathrm{IN}}-V_{G S 2} \tag{4.60}
\end{equation*}
$$

Ignoring the body effect and assuming that $M_{1}-M_{4}$ all operate in the active region with equal overdrives,

$$
\begin{equation*}
V_{D S 1}=V_{t}+V_{o v} \tag{4.61}
\end{equation*}
$$

Therefore, the drain-source voltage of $M_{1}$ is a threshold larger than necessary to operate $M_{1}$ in the active region. To reduce $V_{D S 1}$, the voltage from the gate of $M_{2}$ to ground can be level shifted down by a threshold as shown in Fig. 4.11a. In practice, a source follower is used to implement the level shift, as shown in Fig. 4.11b. ${ }^{6}$ Transistor $M_{5}$ acts as the source follower and is biased by the output of the simple current mirror $M_{3}$ and $M_{6}$. Because the gate-source voltage of $M_{5}$ is greater than its threshold by the overdrive, however, the drain-source voltage of $M_{1}$ would be zero with equal thresholds and overdrives on all transistors. To bias $M_{1}$ at the
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: VOUT, G: Vov}
name: M2, type: NMOS, ports: {S: VOUT, D: Vout, G: (Vt+2Vov)}
name: M3, type: NMOS, ports: {S: GND, D: (Vt+Vov), G: GND}
name: M4, type: NMOS, ports: {S: VDD, D: (Vt+3Vov), G: (2Vt+3Vov)}
name: I_IN, type: CurrentSource, ports: {Np: VDD, Nn: (2Vt+3Vov)}
]
extrainfo:The circuit is a MOS cascode current mirror with improved biasing for maximum voltage swing. It utilizes NMOS transistors and a current source to achieve a specific voltage output. The overdrive voltage is calculated to maintain the transistors in the desired operating region.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: VOUT, G: Vov}
name: M2, type: NMOS, ports: {S: VOUT, D: LOAD, G: Vov}
name: M3, type: NMOS, ports: {S: GND, D: Vov, G: GND}
name: M4, type: NMOS, ports: {S: VDD, D: Vov, G: (Vt+3Vov)}
name: M5, type: NMOS, ports: {S: (Vt+3Vov), D: Vov, G: (Vt+2Vov)}
name: M6, type: NMOS, ports: {S: GND, D: Vov, G: GND}
name: I_IN, type: CurrentSource, ports: {Np: VDD, Nn: (Vt+3Vov)}
]
extrainfo:The circuit is a practical implementation of a MOS cascode current mirror with improved biasing for maximum voltage swing. It uses NMOS transistors to achieve level shifting and biasing. Transistor M5 acts as a source follower biased by the output of the current mirror formed by M3 and M6. The overdrive voltage on M4 is doubled by reducing its W/L ratio by a factor of four to meet the required biasing condition.
image_name:(c)
description:The graph in Figure 4.11(c) is an I-V characteristic curve, which plots the output current (I_OUT) against the output voltage (V_OUT). The x-axis represents V_OUT, indicating the output voltage, while the y-axis represents I_OUT, indicating the output current. Both axes likely use a linear scale.

### Overall Behavior and Trends:
The graph exhibits a characteristic shape typical of a MOSFET operating in different regions. Initially, as V_OUT increases from zero, there is a rapid increase in I_OUT, indicating the device is moving from cutoff to saturation. This rapid rise is followed by a leveling off, where I_OUT becomes relatively constant despite further increases in V_OUT, indicating the device is in saturation.

### Key Features and Technical Details:
- **Initial Region:** At low V_OUT, I_OUT increases sharply, suggesting the transition from the cutoff region to the active region.
- **Saturation Region:** Beyond a certain threshold voltage, I_OUT reaches a plateau, indicating the device is in the saturation region. The graph shows a clear horizontal asymptote at this stage.
- **Critical Points:** The point where the curve begins to level off corresponds to V_OUT = 2V_ov, which marks the transition to the saturation region.

### Annotations and Specific Data Points:
- The graph highlights the threshold voltage at which the saturation region begins, marked by V_OUT = 2V_ov. This is a critical point indicating the minimum voltage required for the device to operate in the saturation region.

The graph effectively demonstrates the behavior of the MOSFET in the circuit, particularly how the output current stabilizes after reaching a certain output voltage, which is crucial for understanding the biasing and operation of the current mirror circuit depicted in the schematic diagrams (a) and (b).

Figure 4.11 (a) MOS cascode current mirror with improved biasing for maximum voltage swing. (b) Practical implementation. (c) I-V characteristic.
boundary between the active and triode regions,

$$
\begin{equation*}
V_{D S 1}=V_{o v} \tag{4.62}
\end{equation*}
$$

is required. Therefore, the overdrive on $M_{4}$ is doubled by reducing its $W / L$ by a factor of four to satisfy (4.62). As a result, the threshold term in (4.59) is eliminated and

$$
\begin{equation*}
V_{\text {OUT }(\min )} \simeq 2 V_{o v} \tag{4.63}
\end{equation*}
$$

Because the minimum output voltage does not contain a threshold component, the range of output voltages for which $M_{1}$ and $M_{2}$ both operate in the active region is significantly improved. Therefore, the current mirror in Fig. 4.11 places much less restriction on the range of output voltages that can be achieved in an amplifier using this current mirror as an active load than the mirror in Fig. 4.9. For this reason, the mirror in Fig. 4.11 is called a high-swing cascode current mirror. This type of level shifting to reduce $V_{\text {OUT(min) }}$ can also be applied to bipolar circuits.

The output resistance of the high-swing cascode current mirror is the same as in (4.50) when both $M_{1}$ and $M_{2}$ operate in the active region. However, the input voltage and the systematic gain error are worsened compared to the cascode current mirror without level shift. The input voltage is still given by (4.56), but the overdrive component of the gate-source voltage of $M_{4}$ has increased by a factor of two because its $W / L$ has been reduced by a factor of four. Therefore,

$$
\begin{equation*}
V_{\mathrm{IN}}=2 V_{t}+3 V_{o v} \tag{4.64}
\end{equation*}
$$

Since $M_{3}$ and $M_{1}$ form a simple current mirror with unequal drain-source voltages, the systematic gain error is

$$
\begin{equation*}
\epsilon=\frac{V_{D S 1}-V_{D S 3}}{V_{A}} \simeq \frac{V_{o v 1}-\left(V_{t}+V_{o v 1}\right)}{V_{A}}=-\frac{V_{t}}{V_{A}} \tag{4.65}
\end{equation*}
$$

The negative sign in (4.65) shows that $I_{\mathrm{OUT}}<I_{\mathrm{IN}}$. For example, if $I_{\mathrm{IN}}=100 \mu \mathrm{~A}, V_{t}=1 \mathrm{~V}$, and $V_{A}=10 \mathrm{~V}, \epsilon \simeq-0.1$, which means that $I_{\text {OUT }} \simeq 90 \mu \mathrm{~A}$.

In practice, $(W / L)_{4}<(1 / 4)(W / L)$ is usually selected for two reasons. First, MOS transistors display an indistinct transition from the triode to active regions. Therefore, increasing the drain-source voltage of $M_{1}$ by a few hundred millivolts above $V_{o v 1}$ is usually required to realize the incremental output resistance predicted by (4.50). Second, although the body effect was not considered in this analysis, it tends to reduce the drain-source voltage on $M_{1}$, which is determined by the following KVL loop

$$
\begin{equation*}
V_{D S 1}=V_{G S 3}+V_{G S 4}-V_{G S 5}-V_{G S 2} \tag{4.66}
\end{equation*}
$$

Each of the gate-source voltage terms in (4.66) contains a threshold component. Since the source-body voltage of $M_{5}$ is higher than that of $M_{4}, V_{t 5}>V_{t 4}$. Also, $V_{t 2}>V_{t 3}$ because the source-body voltage of $M_{2}$ is higher than that of $M_{3}$. Simulations with high-accuracy models are usually required to find the optimum $(W / L)_{4}$.

One drawback of the current mirror in Fig. 4.11 is that the input current is mirrored to a new branch to do the level shift. Combining the input branches eliminates the possibility of mismatch between the two branch currents and may reduce the power dissipation. In a single combined input branch, some element must provide a voltage drop equal to the desired difference between the gate voltages of $M_{1}$ and $M_{2}$. To bias $M_{1}$ at the edge of the active region, the required voltages from the gates $M_{1}$ and $M_{2}$ to ground are $V_{t}+V_{o v}$ and $V_{t}+2 V_{o v}$, respectively. Therefore, the desired difference in the gate voltages is $V_{o v}$. This voltage difference can be developed across the drain to the source of a transistor deliberately operated in the triode region, as shown in Fig. 4.12a. ${ }^{7}$ Since $M_{6}$ is diode connected, it operates
image_name:(a)
description:
[
name: M5, type: NMOS, ports: {S: GND, D: d5s6, G: g5g6d6}
name: M6, type: NMOS, ports: {S: d5s6, D: g5g6d6, G: g5g6d6}
name: IIN, type: CurrentSource, ports: {Np: g5g6d6, Nn: VDD}
]
extrainfo:The circuit forces M5 to operate in the triode region using M6, which is diode-connected. The current source IIN is connected between VDD and the node g5g6d6.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1s2, G: Vt+Vov}
name: M2, type: NMOS, ports: {S: d1s2, D: Vout, G: Vt+2Vov}
name: M3, type: NMOS, ports: {S: GND, D: Vt+Vov, G: Vt+Vov}
name: M4, type: NMOS, ports: {S: Vt+Vov, D: Vt+2Vov, G: Vin}
name: M5, type: NMOS, ports: {S: Vin, D: Vt+Vov, G: Vin}
name: M6, type: NMOS, ports: {S: Vin, D: Vt+2Vov, G: Vin}
name: I_IN, type: CurrentSource, ports: {Np: VDD, Nn: Vin}
]
extrainfo:The circuit in (b) is a cascode current mirror that utilizes NMOS transistors. M5 and M6 are configured to force M4 to operate at specific voltages, ensuring the correct biasing for M1 and M2. The input current I_IN flows from VDD to Vin, setting the bias conditions for the transistors.

Figure 4.12 (a) Circuit that forces $M_{5}$ to operate in the triode region. (b) Sooch cascode current mirror using the circuit in $(a)$.
in the active region as long as the input current and threshold are positive. However, since the gate-source voltage of $M_{6}$ is equal to the gate-drain voltage of $M_{5}$, a channel exists at the drain of $M_{5}$ when it exists at the source of $M_{6}$. In other words, $M_{6}$ forces $M_{5}$ to operate in the triode region.

To use the circuit in Fig. $4.12 a$ in a current mirror, we would like to choose the aspect ratios of the transistors so that the drain-source voltage of $M_{5}$ is $V_{o v}$. Since $M_{6}$ operates in the active region,

$$
\begin{equation*}
I_{\mathrm{IN}}=\frac{k^{\prime}}{2}\left(\frac{W}{L}\right)_{6}\left(V_{G S 6}-V_{t}\right)^{2} \tag{4.67}
\end{equation*}
$$

Since $M_{5}$ operates in the triode region,

$$
\begin{equation*}
I_{\mathrm{IN}}=\frac{k^{\prime}}{2}\left(\frac{W}{L}\right)_{5}\left(2\left(V_{G S 5}-V_{t}\right) V_{D S 5}-\left(V_{D S 5}\right)^{2}\right) \tag{4.68}
\end{equation*}
$$

The goal is to set

$$
\begin{equation*}
V_{D S 5}=V_{o v} \tag{4.69}
\end{equation*}
$$

when

$$
\begin{equation*}
V_{G S 6}=V_{t}+V_{o v} \tag{4.70}
\end{equation*}
$$

From (4.69) and (4.70),

$$
\begin{equation*}
V_{G S 5}=V_{G S 6}+V_{D S 5}=V_{t}+2 V_{o v} \tag{4.71}
\end{equation*}
$$

Substituting (4.68) - (4.71) into (4.67) gives

$$
\begin{equation*}
\frac{k^{\prime}}{2}\left(\frac{W}{L}\right)_{6}\left(V_{o v}\right)^{2}=\frac{k^{\prime}}{2}\left(\frac{W}{L}\right)_{5}\left(2\left(2 V_{o v}\right) V_{o v}-\left(V_{o v}\right)^{2}\right) \tag{4.72}
\end{equation*}
$$

Equation 4.72 can be simplified to

$$
\begin{equation*}
\left(\frac{W}{L}\right)_{5}=\frac{1}{3}\left(\frac{W}{L}\right)_{6} \tag{4.73}
\end{equation*}
$$

The circuit of Fig. 4.12a is used in the current mirror of Fig. 4.12b, ${ }^{7}$ which is called the Sooch cascode current mirror after its inventor. At first, ignore transistor $M_{4}$ and assume that $M_{3}$ is simply diode connected. The difference between the voltages to ground from the gates of $M_{1}$ and $M_{2}$ is set by the drain-source voltage of $M_{5}$. By choosing equal aspect ratios for all devices except $M_{5}$, whose aspect ratio is given by (4.73), the drain-source voltage of $M_{5}$ is $V_{o v}$ and $M_{1}$ is biased at the edge of the active region. The output resistance, minimum output voltage, input voltage, and systematic gain error are the same as in (4.50), (4.63), (4.64), and (4.65) respectively.

Now we will consider the effect of transistor $M_{4}$. The purpose of $M_{4}$ is to set the drainsource voltage of $M_{3}$ equal to that of $M_{1}$. Without $M_{4}$, these drain-source voltages differ by a threshold, causing nonzero systematic gain error. With $M_{4}$,

$$
\begin{equation*}
V_{D S 3}=V_{G 2}-V_{G S 4} \tag{4.74}
\end{equation*}
$$

where

$$
\begin{equation*}
V_{G 2}=V_{G S 3}+V_{D S 5} \tag{4.75}
\end{equation*}
$$

Ignoring channel-length modulation,

$$
\begin{equation*}
V_{G 2}=\left(V_{t}+V_{o v}\right)+V_{o v}=V_{t}+2 V_{o v} \tag{4.76}
\end{equation*}
$$

Ignoring the body effect and assuming that $M_{4}$ operates in the active region,

$$
\begin{equation*}
V_{G S 4}=V_{t}+V_{o v} \tag{4.77}
\end{equation*}
$$

Then substituting (4.76) and (4.77) into (4.74) gives

$$
\begin{equation*}
V_{D S 3}=V_{o v} \tag{4.78}
\end{equation*}
$$

If $M_{2}$ also operates in the active region under these conditions, $V_{D S 3}=V_{D S 1}$. As a result, the systematic gain error is

$$
\begin{equation*}
\epsilon=0 \tag{4.79}
\end{equation*}
$$

Therefore, the purpose of $M_{4}$ is to equalize the drain-source voltages of $M_{3}$ and $M_{1}$ to reduce the systematic gain error.

For $M_{4}$ to operate in the active region, $V_{D S 4}>V_{o v}$ is required. Since

$$
\begin{equation*}
V_{D S 4}=V_{G S 3}-V_{D S 3}=\left(V_{t}+V_{o v}\right)-V_{o v}=V_{t} \tag{4.80}
\end{equation*}
$$

Equation 4.80 shows that $M_{4}$ operates in the active region if $V_{t}>V_{o v}$. Although this condition is usually satisfied, a low threshold and/or high overdrive may cause $M_{4}$ to operate in the triode region. If this happens, the gate-source voltage of $M_{4}$ depends strongly on its drainsource voltage, increasing the systematic gain error. Since increasing temperature causes the threshold to decrease, but the overdrive to increase, checking the region of operation of $M_{4}$ in simulation at the maximum expected operating temperature is important in practice.

The main limitation of the high-swing cascode current mirrors just presented, is that the input voltage is large. In Fig. 4.11, the input voltage is the sum of the gate-source voltages of $M_{3}$ and $M_{4}$ and is given by (4.64) ignoring body effect. In Fig. 4.12, the input voltage is

$$
\begin{align*}
V_{\mathrm{IN}} & =V_{G S 3}+V_{D S 5}+V_{G S 6} \\
& =V_{t}+V_{o v}+V_{o v}+V_{t}+V_{o v} \\
& =2 V_{t}+3 V_{o v} \tag{4.81}
\end{align*}
$$

Equation 4.81 shows that the input voltage of the high-swing cascode current mirror in Fig. 4.12 is the same as in (4.64) for Fig. 4.11. The large input voltages may limit the minimum power-supply voltage because a transistor-level implementation of the input current source requires some nonzero drop for proper operation. With threshold voltages of about 1 V , the cascode current mirrors in Figs. 4.11 and 4.12 can operate properly for power-supply voltages greater than about 3 V . Below about 2 V , however, reduced thresholds or a new configuration is required. Reducing the magnitude of the threshold for all transistors increases the difficulty in turning off transistors that are used as switches. This problem can be overcome by using low-threshold devices in the current mirror and high-threshold devices as switches, but this solution increases process complexity and cost. Therefore, circuit techniques to reduce the input voltage are important to minimize cost.

To reduce the input voltage, the input branch can be split into two branches, as shown in Fig. 4.13. If $M_{1}$ and $M_{2}$ are biased in the active region, the output resistance is still given by (4.50). Also, the minimum output voltage for which (4.50) applies is still given by (4.63). Furthermore, if $M_{4}$ operates in the active region, the drain-source voltage of $M_{3}$ is equal to that of $M_{1}$, and the systematic gain error is still zero as in (4.79).
image_name:Figure 4.13 MOS high-swing current mirror with two input branches
description:
[
name: M6, type: NMOS, ports: {S: VDD, D: d5s6, G: VIN}
name: M5, type: NMOS, ports: {S: d5s6, D: GND, G: VIN1}
name: M4, type: NMOS, ports: {S: VDD, D: d3s4, G: VIN}
name: M3, type: NMOS, ports: {S: d3s4, D: VIN2, G: VIN1}
name: M2, type: NMOS, ports: {S: VDD, D: VOUT, G: VIN2}
name: M1, type: NMOS, ports: {S: d1s2, D: GND, G: VOUT}
name: IIN, type: CurrentSource, value: IIN, ports: {Np: VDD, Nn: VIN}
]
extrainfo:The circuit depicted is a MOS high-swing current mirror with two input branches. It features six NMOS transistors (M1 to M6) and one current source (IIN). The circuit is designed to reduce input voltage by splitting the input branch into two branches, allowing for lower input voltage levels as indicated by VIN1 and VIN2. The transistors are configured to maintain a systematic gain error of zero when M4 operates in the active region.

Figure 4.13 MOS high-swing current mirror with two input branches.

Since the mirror in Fig. 4.13 has two input branches, an input voltage can be calculated for each:

$$
\begin{gather*}
V_{\mathrm{IN} 1}=V_{D S 5}+V_{G S 6}=V_{t}+2 V_{o v}  \tag{4.82}\\
V_{\mathrm{IN} 2}=V_{G S 3}=V_{t}+V_{o v} \tag{4.83}
\end{gather*}
$$

Both $V_{\mathrm{IN} 1}$ and $V_{\mathrm{IN} 2}$ are less than the input voltage given in (4.64) for Fig. $4.12 b$ by more than a threshold, allowing the input current sources to operate properly with power-supply voltages greater than about 2 V , assuming thresholds of about 1 V .

Finally, in Fig. 4.13, the drain-source voltage of $M_{5}$ is only used to bias the source of $M_{6}$. Therefore, $M_{5}$ and $M_{6}$ can be collapsed into one diode-connected transistor whose source is grounded. Call this replacement transistor $M_{7}$. The aspect ratio of $M_{7}$ should be a factor of four smaller than the aspect ratios of $M_{1}-M_{4}$ to maintain the bias conditions as in Fig. 4.13. In practice, the aspect ratio of $M_{7}$ is further reduced to bias $M_{1}$ past the edge of the active region and to overcome a mismatch in the thresholds of $M_{7}$ and $M_{2}$ caused by body effect.

### 4.2.6 Wilson Current Mirror

#### 4.2.6.1 Bipolar

The main limitation of the bipolar cascode current mirror is that the systematic gain error stemming from finite $\beta_{F}$ was large, as given in (4.49). To overcome this limitation, the Wilson current mirror can be used as shown in Fig. 4.14a. ${ }^{8}$ This circuit uses negative feedback through $Q_{1}$, activating $Q_{3}$ to reduce the base-current error and raise the output resistance. (See Chapter 8.)

From a qualitative standpoint, the difference between the input current and $I_{C 3}$ flows into the base of $Q_{2}$. This base current is multiplied by $\left(\beta_{F}+1\right)$ and flows in the diode-connected transistor $Q_{1}$, which causes current of the same magnitude to flow in $Q_{3}$. A feedback path is thus formed that regulates $I_{C 3}$ so that it is nearly equal to the input current, reducing the systematic gain error caused by finite $\beta_{F}$. Similarly, when the output voltage increases, the collector current of $Q_{2}$ also increases, in turn increasing the collector current of $Q_{1}$. As a result, the collector current of $Q_{3}$ increases, which reduces the base current of $Q_{2}$. The decrease in the base current of $Q_{2}$ caused by negative feedback reduces the original change in the collector current of $Q_{2}$ and increases the output resistance.

To find the output resistance of the Wilson current mirror when all transistors operate in the active region, we will analyze the small-signal model shown in Fig. 4.14b, in which a
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: X, B: X, E: GND}
name: Q2, type: NPN, ports: {C: VOUT, B: X, E: X}
name: Q3, type: NPN, ports: {C: X, B: VIN, E: GND}
name: IIN, type: CurrentSource, value: IIN, ports: {Np: VIN, Nn: VCC}
name: rπ2, type: Resistor, value: rπ2, ports: {N1: 3, N2: 2}
name: ro2, type: Resistor, value: ro2, ports: {N1: Vt, N2: 1}
name: ro3, type: Resistor, value: ro3, ports: {N1: 2, N2: GND}
name: 1/gm1, type: Resistor, value: 1/gm1, ports: {N1: 1, N2: GND}
name: gm2vπ2, type: CurrentSource, value: gm2vπ2, ports: {Np: 1, Nn: Vt}
name: it, type: CurrentSource, value: it, ports: {Np: Vt, Nn: GND}
]
extrainfo:The circuit diagram (a) represents a Bipolar Wilson current mirror, which consists of three NPN transistors (Q1, Q2, Q3). It is used to copy current from the input to the output with high output resistance. The small signal model in diagram (b) shows the components used to analyze the output resistance of the Wilson current mirror.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: 1, B: 2, E: GND}
name: Q2, type: NPN, ports: {C: VOUT, B: 1, E: 2}
name: Q3, type: NPN, ports: {C: 2, B: 1, E: GND}
name: IIN, type: CurrentSource, ports: {Np: VIN, Nn: 1}
]
extrainfo:The circuit is a small-signal model of a Wilson current mirror. It uses three NPN transistors (Q1, Q2, Q3) and a current source (IIN). The configuration is designed to increase output resistance using negative feedback.

Figure 4.14 (a) Bipolar Wilson current mirror. (b) Small-signal model.
test current source $i_{t}$ is applied at the output. Transistors $Q_{1}$ and $Q_{3}$ form a simple current mirror. Since $Q_{1}$ is diode connected, the small-signal resistance from the base of $Q_{1}$ to ground is $\left(1 / g_{m 1}\right)\left\|r_{\pi 1}\right\| r_{\pi 3} \| r_{o 1}$. Assume that an unknown current $i_{1}$ flows in this resistance. When $g_{m 1} r_{\pi 1} \gg 1, g_{m 1} r_{\pi 3} \gg 1$, and $g_{m 1} r_{o 1} \gg 1$, this resistance is approximately equal to $1 / g_{m 1}$. Transistor $Q_{3}$ could be modeled as a voltage-controlled current source of value $g_{m 3} v_{\pi 3}$ in parallel with $r_{o 3}$. Since $v_{\pi 3}=v_{\pi 1} \simeq i_{1} / g_{m 1}$, the voltage-controlled current source in the model for $Q_{3}$ can be replaced by a current-controlled current source of value $\left(g_{m 3} / g_{m 1}\right)\left(i_{1}\right)=1\left(i_{1}\right)$, as shown in Fig. 4.14b. This model represents the behavior of the simple current mirror directly: The input current $i_{1}$ is mirrored to the output by the current-controlled current source.

Using this model, the resulting voltage $v_{t}$ is

$$
\begin{equation*}
v_{t}=\frac{i_{1}}{g_{m 1}}+\left(i_{t}-g_{m 2} v_{\pi 2}\right) r_{o 2} \tag{4.84}
\end{equation*}
$$

To find the relationship between $i_{1}$ and $v_{\pi 2}$, note that the voltage across $r_{o 3}$ is $\left(i_{1} / g_{m 1}+v_{\pi 2}\right)$ and use KCL at node (2) in Fig. 4.14b to show that

$$
\begin{equation*}
\frac{v_{\pi 2}}{r_{\pi 2}}+i_{1}+\frac{\frac{i_{1}}{g_{m 1}}+v_{\pi 2}}{r_{o 3}}=0 \tag{4.85}
\end{equation*}
$$

Rearranging (4.85) gives

$$
\begin{equation*}
v_{\pi 2}=-i_{1} r_{\pi 2}\left(\frac{1+\frac{1}{g_{m 1} r_{o 3}}}{1+\frac{r_{\pi 2}}{r_{o 3}}}\right) \tag{4.86}
\end{equation*}
$$

To find the relationship between $i_{1}$ and $i_{t}$, use KCL at node (1) in Fig. $4.14 b$ to show that

$$
\begin{equation*}
i_{t}=i_{1}-\frac{v_{\pi 2}}{r_{\pi 2}} \tag{4.87}
\end{equation*}
$$

Substituting (4.86) into (4.87) and rearranging gives

$$
\begin{equation*}
i_{1}=\frac{i_{t}}{1+\left(\frac{1+\frac{1}{g_{m 1 r_{o 3}}}}{1+\frac{r_{\pi 2}}{r_{o 3}}}\right)} \tag{4.88}
\end{equation*}
$$

Substituting (4.88) into (4.86) and rearranging gives

$$
\begin{equation*}
v_{\pi 2}=-i_{t} r_{\pi 2}\left(\frac{1+\frac{1}{g_{m 1} r_{o 3}}}{2+\frac{r_{\pi 2}}{r_{o 3}}+\frac{1}{g_{m 1} r_{o 3}}}\right) \tag{4.89}
\end{equation*}
$$

Substituting (4.88) and (4.89) into (4.84) and rearranging gives

$$
\begin{equation*}
R_{o}=\frac{v_{t}}{i_{t}}=\frac{1}{g_{m 1}\left[1+\left(\frac{1+\frac{1}{g_{m 1} r_{o 3}}}{1+\frac{r_{22}}{r_{o 3}}}\right)\right]}+r_{o 2}+\frac{g_{m 2} r_{\pi 2} r_{o 2}\left(1+\frac{1}{g_{m 1} r_{o 3}}\right)}{2+\frac{r_{\pi 2}}{r_{o 3}}+\frac{1}{g_{m 1} r_{o 3}}} \tag{4.90}
\end{equation*}
$$

If $r_{o 3} \rightarrow \infty$, the small-signal current that flows in the collector of $Q_{3}$ is equal to $i_{1}$ and (4.90) reduces to

$$
\begin{equation*}
R_{o}=\frac{1}{g_{m 1}(2)}+r_{o 2}+\frac{g_{m 2} r_{\pi 2} r_{o 2}}{2} \simeq \frac{\beta_{0} r_{o 2}}{2} \tag{4.91}
\end{equation*}
$$

This result is the same as (4.38) for the cascode current mirror. In the cascode current mirror, the small-signal current that flows in the base of $Q_{2}$ is mirrored through $Q_{3}$ to $Q_{1}$ so that the small-signal base and emitter currents leaving $Q_{2}$ are approximately equal. On the other hand, in the Wilson current mirror, the small-signal current that flows in the emitter of $Q_{2}$ is mirrored through $Q_{1}$ to $Q_{3}$ and then flows in the base of $Q_{2}$. Although the cause and effect relationship here is opposite of that in a cascode current mirror, the output resistance is unchanged because the small-signal base and emitter currents leaving $Q_{2}$ are still forced to be equal. Therefore, the small-signal collector current of $Q_{2}$ that flows because of changes in the output voltage still splits into two equal parts with half flowing in $r_{\pi 2}$.

For the purpose of dc analysis, we assume that $V_{A} \rightarrow \infty$ and that the transistors are identical. Then the input voltage is

$$
\begin{equation*}
V_{\mathrm{IN}}=V_{C E 3}=V_{B E 1}+V_{B E 2}=2 V_{B E(\mathrm{on})} \tag{4.92}
\end{equation*}
$$

which is the same as in (4.40) for a cascode current mirror. Also, the minimum output voltage for which both transistors in the output branch operate in the forward-active region is

$$
\begin{equation*}
V_{\mathrm{OUT}(\min )}=V_{C E 1}+V_{C E 2(\mathrm{sat})}=V_{B E(\mathrm{on})}+V_{C E 2(\mathrm{sat})} \tag{4.93}
\end{equation*}
$$

The result in (4.93) is the same as in (4.41) for a cascode current mirror.
To find the systematic gain error, start with KCL at the collector of $Q_{1}$ to show that

$$
\begin{equation*}
-I_{E 2}=I_{C 1}+I_{B 1}+I_{B 3}=I_{C 1}\left(1+\frac{1}{\beta_{F}}\right)+\frac{I_{C 3}}{\beta_{F}} \tag{4.94}
\end{equation*}
$$

Since we assumed that the transistors are identical and $V_{A} \rightarrow \infty$,

$$
\begin{equation*}
I_{C 3}=I_{C 1} \tag{4.95}
\end{equation*}
$$

Substituting (4.95) into (4.94) gives

$$
\begin{equation*}
-I_{E 2}=I_{C 1}\left(1+\frac{2}{\beta_{F}}\right) \tag{4.96}
\end{equation*}
$$

Using (4.96), the collector current of $Q_{2}$ is then

$$
\begin{equation*}
I_{C 2}=-I_{E 2}\left(\frac{\beta_{F}}{1+\beta_{F}}\right)=I_{C 1}\left(1+\frac{2}{\beta_{F}}\right)\left(\frac{\beta_{F}}{1+\beta_{F}}\right) \tag{4.97}
\end{equation*}
$$

Rearranging (4.97) we obtain

$$
\begin{equation*}
I_{C 1}=I_{C 2}\left[\frac{1}{\left(1+\frac{2}{\beta_{F}}\right)\left(\frac{\beta_{F}}{1+\beta_{F}}\right)}\right] \tag{4.98}
\end{equation*}
$$

From KCL at the base of $Q_{2}$,

$$
\begin{equation*}
I_{C 3}=I_{\mathrm{IN}}-\frac{I_{C 2}}{\beta_{F}} \tag{4.99}
\end{equation*}
$$

Inserting (4.98) and (4.99) into (4.95), we find that

$$
\begin{equation*}
I_{\mathrm{OUT}}=I_{C 2}=I_{\mathrm{IN}}\left(1-\frac{2}{\beta_{F}^{2}+2 \beta_{F}+2}\right)=\frac{I_{\mathrm{IN}}}{1+\frac{2}{\beta_{F}\left(\beta_{F}+2\right)}} \tag{4.100}
\end{equation*}
$$

In the configuration shown in Fig. 4.14a, the systematic gain error arising from finite output resistance is not zero because $Q_{3}$ and $Q_{1}$ operate with collector-emitter voltages that differ by the base-emitter voltage of $Q_{2}$. With finite $V_{A}$ and finite $\beta_{F}$,

$$
\begin{align*}
I_{\mathrm{OUT}} & \simeq I_{\mathrm{IN}}\left(1-\frac{2}{\beta_{F}^{2}+2 \beta_{F}+2}\right)\left(1+\frac{V_{C E 1}-V_{C E 3}}{V_{A}}\right) \\
& \simeq I_{\mathrm{IN}}\left(1-\frac{2}{\beta_{F}^{2}+2 \beta_{F}+2}\right)\left(1-\frac{V_{B E 2}}{V_{A}}\right) \tag{4.101}
\end{align*}
$$

Therefore, the systematic gain error is

$$
\begin{equation*}
\epsilon \simeq-\left(\frac{2}{\beta_{F}^{2}+2 \beta_{F}+2}+\frac{V_{B E 2}}{V_{A}}\right) \tag{4.102}
\end{equation*}
$$

Comparing (4.102) to (4.49) shows two key points. First, the systematic gain error arising from finite $\beta_{F}$ in a Wilson current mirror is much less than in a cascode current mirror. Second, the systematic gain error arising from finite output resistance is worse in the Wilson current mirror shown in Fig. 4.14a than in the cascode current mirror shown in Fig. 4.9. However, this limitation is not fundamental because it can be overcome by introducing a new diode-connected transistor between the collector of $Q_{3}$ and the base of $Q_{2}$ to equalize the collector-emitter voltages of $Q_{3}$ and $Q_{1}$.

#### 4.2.6.2 MOS

Wilson current mirrors are also used in MOS technology, as shown in Fig. 4.15. Ignoring $M_{4}$, the circuit operation is essentially identical to the bipolar case with $\beta_{F} \rightarrow \infty$. One way to calculate the output resistance is to let $r_{\pi 2} \rightarrow \infty$ in (4.90), which gives

$$
\begin{equation*}
R_{o}=\frac{1}{g_{m 1}}+r_{o 2}+g_{m 2} r_{o 2}\left(1+\frac{1}{g_{m 1} r_{o 3}}\right) r_{o 3} \simeq\left(1+g_{m 2} r_{o 3}\right) r_{o 2} \tag{4.103}
\end{equation*}
$$

image_name:Figure 4.15
description:
[
name: M4, type: NMOS, ports: {S: GND, D: d3s4, G: VIN}
name: M3, type: NMOS, ports: {S: GND, D: X, G: VIN}
name: M2, type: NMOS, ports: {S: VOUT, D: VIN, G: d3s4}
name: M1, type: NMOS, ports: {S: GND, D: X, G: VIN}
name: IIN, type: CurrentSource, value: IIN, ports: {Np: VDD, Nn: VIN}
]
extrainfo:This is an improved MOS Wilson current mirror circuit. It includes an additional device to equalize the drain voltages of M1 and M3. The circuit aims to provide high output resistance and improved current matching.

Figure 4.15 Improved MOS Wilson current mirror with an additional device such that the drain voltages of $M_{1}$ and $M_{3}$ are equal.

Since the calculation in (4.103) is based on the small-signal model for the bipolar Wilson current mirror in Fig. 4.14b, it ignores the body effect in transistor $M_{2}$. Repeating the analysis with a body-effect generator in parallel with $r_{o 2}$ gives

$$
\begin{equation*}
R_{o} \simeq\left(2+g_{m 2} r_{o 3}\right) r_{o 2} \tag{4.104}
\end{equation*}
$$

The body effect on $M_{2}$ has little effect on (4.104) because $M_{1}$ is diode connected and therefore the voltage from the source of $M_{2}$ to ground is almost constant.

Although $\beta_{F} \rightarrow \infty$ for MOS transistors, the systematic gain error is not zero without $M_{4}$ because the drain-source voltage of $M_{3}$ differs from that of $M_{1}$ by the gate-source voltage of $M_{2}$. Therefore, without $M_{4}$,

$$
\begin{equation*}
\epsilon=\frac{V_{D S 1}-V_{D S 3}}{V_{A}}=-\frac{V_{G S 2}}{V_{A}} \tag{4.105}
\end{equation*}
$$

Transistor $M_{4}$ is inserted in series with $M_{3}$ to equalize the drain-source voltages of $M_{3}$ and $M_{1}$ so that

$$
\begin{equation*}
\epsilon \simeq 0 \tag{4.106}
\end{equation*}
$$

With $M_{4}$, the output resistance is still given by (4.104) if all transistors operate in the active region. Also, insertion of $M_{4}$ does not change either the minimum output voltage for which (4.104) applies or the input voltage. Ignoring body effect and assuming equal overdrives on all transistors, the minimum output voltage is

$$
\begin{equation*}
V_{O U T}(\min )=V_{G S 1}+V_{o v 2}=V_{t}+2 V_{o v} \tag{4.107}
\end{equation*}
$$

Under the same conditions, the input voltage is

$$
\begin{equation*}
V_{\mathrm{IN}}=V_{G S 1}+V_{G S 2}=2 V_{t}+2 V_{o v} \tag{4.108}
\end{equation*}
$$

## 4.3 Active Loads

### 4.3.1 Motivation

In differential amplifiers of the type described in Chapter 3, resistors are used as the load elements. For example, consider the differential amplifier shown in Fig. 3.45. For this circuit, the differential-mode (dm) voltage gain is

$$
\begin{equation*}
A_{d m}=-g_{m} R_{C} \tag{4.109}
\end{equation*}
$$

Large gain is often desirable because it allows negative feedback to make the gain with feedback insensitive to variations in the parameters that determine the gain without feedback. This topic is covered in Chapter 8. In Chapter 9, we will show that the required gain should be obtained in as few stages as possible to minimize potential problems with instability. Therefore, maximizing the gain of each stage is important.

Multiplying the numerator and denominator of (4.109) by $I$ gives

$$
\begin{equation*}
A_{d m}=-\frac{I\left(R_{C}\right)}{I / g_{m}} \tag{4.110}
\end{equation*}
$$

With bipolar transistors, let $I$ represent the collector current $I_{C}$ of each transistor in the differential pair. From (1.91), (4.110) can be rewritten as

$$
\begin{equation*}
A_{d m}=-\frac{I_{C} R_{C}}{V_{T}} \tag{4.111}
\end{equation*}
$$

To achieve large voltage gain, (4.111) shows that the $I_{C} R_{C}$ product must be made large, which in turn requires a large power-supply voltage. Furthermore, large values of resistance are required when low current is used to limit the power dissipation. As a result, the required die area for the resistors can be large.

A similar situation occurs in MOS amplifiers with resistive loads. Let $I$ represent the drain current $I_{D}$ of each transistor in the differential pair, and let the resistive loads be $R_{D}$. From (1.157) and (1.180), (4.110) can be rewritten as

$$
\begin{equation*}
A_{d m}=-\frac{I_{D} R_{D}}{\left(V_{G S}-V_{t}\right) / 2}=-\frac{2 I_{D} R_{D}}{V_{o v}} \tag{4.112}
\end{equation*}
$$

Equation 4.112 shows that the $I_{D} R_{D}$ product must be increased to increase the gain with constant overdrive. As a result, a large power supply is usually required for large gain, and large resistance is usually required to limit power dissipation. Also, since the overdrive is usually much larger than the thermal voltage, comparing (4.111) and (4.112) shows that the gain of an MOS differential pair is usually much less than the gain of its bipolar counterpart with equal resistive drops. This result stems from the observation that bipolar transistors provide much more transconductance for a given current than MOS transistors provide.

If the power-supply voltage is only slightly larger than the drop on the resistors, the range of common-mode input voltages for which the input transistors would operate in the active region would be severely restricted in both bipolar and MOS amplifiers. To overcome this problem and provide large gain without large power-supply voltages or resistances, the $r_{o}$ of a transistor can be used as a load element. ${ }^{9}$ Since the load element in such a circuit is a transistor instead of a resistor, the load element is said to be active instead of passive.

### 4.3.2 Common-Emitter-Common-Source Amplifier with Complementary Load

A common-emitter amplifier with pnp current-mirror load is shown in Fig. 4.16a. The commonsource counterpart with a $p$-channel MOS current-mirror load is shown in Fig. 4.16b. In both cases, there are two output variables: the output voltage, $V_{\text {out }}$, and the output current, $I_{\text {out }}$. The relationship between these variables is governed by both the input transistor and the load transistor. From the standpoint of the input transistor $T_{1}$,

$$
\begin{equation*}
I_{\text {out }}=I_{c 1} \quad \text { or } \quad I_{\text {out }}=I_{d 1} \tag{4.113}
\end{equation*}
$$

image_name:(a)
description:
[
name: T1, type: NMOS, ports: {S: GND, D: Vout, G: Vi}
name: T2, type: PMOS, ports: {S: VDD, D: g2g3d2, G: g2g3d2}
name: T3, type: PMOS, ports: {S: VDD, D: g2g3d2, G: g2g3d2}
name: IREF, type: CurrentSource, ports: {Np: g2g3d2, Nn: GND}
]
extrainfo:The circuit is a common-source amplifier with an active load. T1 is the input NMOS transistor, while T2 and T3 are PMOS transistors forming a current mirror. IREF provides the reference current for the current mirror. The output voltage is taken at the drain of T1.
image_name:(b)
description:
[
name: T1, type: NMOS, ports: {S: GND, D: Vout, G: Vi}
name: T2, type: PMOS, ports: {S: VDD, D: g2g3d2, G: Vout}
name: T3, type: PMOS, ports: {S: g2g3d2, D: g3g3d3, G: Vout}
name: IREF, type: CurrentSource, ports: {Np: g3g3d3, Nn: GND}
]
extrainfo:The circuit is a common-source amplifier with an active PMOS load. It uses a current mirror configuration to provide the load.

Figure 4.16 (a) Common-emitter amplifier with active load. (b) Common-source amplifier with active load.
and

$$
\begin{equation*}
V_{\text {out }}=V_{c e 1} \quad \text { or } \quad V_{\text {out }}=V_{d s 1} \tag{4.114}
\end{equation*}
$$

Equations 4.113 and 4.114 show that the output $I-V$ characteristics of $T_{1}$ can be used directly in the analysis of the relationship between the output variables. Since the input voltage is the base-emitter voltage of $T_{1}$ in Fig. $4.16 a$ and the gate-source voltage of $T_{1}$ in Fig. 4.16b, the input voltage is the parameter that determines the particular curve in the family of output characteristics under consideration at any point, as shown in Fig. 4.17a.

In contrast, the base-emitter or gate-source voltage of the load transistor $T_{2}$ is fixed by diode-connected transistor $T_{3}$. Therefore, only one curve in the family of output $I-V$ characteristics needs to be considered for the load transistor, as shown in Fig. 4.17b. From the standpoint of the load transistor,

$$
\begin{equation*}
I_{\mathrm{out}}=-I_{c 2} \quad \text { or } \quad I_{\mathrm{out}}=-I_{d 2} \tag{4.115}
\end{equation*}
$$

and

$$
\begin{equation*}
V_{\text {out }}=V_{C C}+V_{c e 2} \quad \text { or } \quad V_{\text {out }}=V_{D D}+V_{d s 2} \tag{4.116}
\end{equation*}
$$

Equation 4.115 shows that the output characteristic of the load transistor should be mirrored along the horizontal axis to plot in the same quadrant as the output characteristics of the input
image_name:(a)
description:1. **Type of Graph and Function:**
The graph in figure (a) is an I-V characteristic plot for the input transistor, typically used in analog electronics to depict the relationship between current and voltage.

2. **Axes Labels and Units:**
- The x-axis represents the voltage across the collector-emitter (Vce1) or drain-source (Vds1) of the transistor. This axis is likely in volts.
- The y-axis represents the current through the collector (Ic1) or drain (Id1) of the transistor. This axis is likely in amperes.

3. **Overall Behavior and Trends:**
- The graph shows a series of curves, each representing the I-V characteristics at different input voltages (Vi1, Vi2, Vi3, Vi4, Vi5).
- As the voltage on the x-axis increases, the current on the y-axis also increases, showing a typical active region behavior of a transistor.
- Each curve starts at the origin and rises steeply, indicating that as Vce1 or Vds1 increases, the current Ic1 or Id1 also increases.

4. **Key Features and Technical Details:**
- The curves become less steep as the voltage increases, indicating saturation effects.
- The curves are labeled with different input voltages (Vi1 to Vi5), suggesting that higher input voltages lead to higher currents for the same Vce1 or Vds1.
- The graph does not show breakdown or cutoff regions, focusing on the active region.

5. **Annotations and Specific Data Points:**
- The curves are annotated with different input voltages (Vi1, Vi2, Vi3, Vi4, Vi5), showing how the I-V characteristics shift with varying input voltages.
- The steepness of the curves decreases from Vi1 to Vi5, indicating the transistor's response to increasing input voltage.
- There are no specific numerical values given for current or voltage, but the trend is clear from the curve progression.
image_name:(b)
description:The graph labeled (b) is an $I-V$ characteristic curve of the active load transistor. This type of graph is typically used to illustrate the relationship between current and voltage in semiconductor devices.

1. **Axes Labels and Units:**
- The horizontal axis represents the voltage across the collector-emitter or drain-source, labeled as $V_{ce2}$ or $V_{ds2}$. It is likely measured in volts.
- The vertical axis represents the current through the collector or drain, labeled as $I_{c2}$ or $I_{d2}$. This is typically measured in amperes.
- The graph appears to use a linear scale for both axes.

2. **Overall Behavior and Trends:**
- The curve begins at the origin, indicating that initially, both voltage and current are zero.
- As the voltage increases, the current remains nearly constant at a low value, indicating a region where the transistor is not conducting significantly.
- At a certain threshold voltage, the current sharply increases, representing the active region where the transistor begins to conduct more significantly.
- After this sharp increase, the current stabilizes at a constant value, indicating saturation.

3. **Key Features and Technical Details:**
- The graph shows a clear threshold or knee point where the current starts to increase sharply.
- The saturation region is evident where the current plateaus at a constant value, identified as $I_{REF}$.
- The voltage at which the curve bends and the current increases sharply is significant for determining the transistor's operational point.

4. **Annotations and Specific Data Points:**
- The voltage at the threshold is labeled as $V_{BE2}$ or $V_{GS2}$, held constant throughout the measurement.
- The current in the saturation region is marked as $I_{REF}$, indicating a reference current level.

This graph is crucial for understanding the active load's behavior in the circuit, particularly in how it responds to varying voltage levels across the transistor, which influences the overall circuit performance.
image_name:(c)
description:The graph labeled (c) is an I-V characteristic graph with the load characteristic superimposed. It represents the current-voltage relationship for a transistor circuit with an active load.

1. **Type of Graph and Function:**
- This is an I-V (current-voltage) characteristic graph, showing the behavior of a transistor circuit with a superimposed load characteristic.

2. **Axes Labels and Units:**
- The horizontal axis represents the collector-emitter voltage \( V_{ce1} \) or the drain-source voltage \( V_{ds1} \), typically measured in volts (V).
- The vertical axis represents the collector current \( I_{c1} - I_{c2} \) or the drain current \( I_{d1} - I_{d2} \), typically measured in amperes (A).
- The graph is likely on a linear scale.

3. **Overall Behavior and Trends:**
- The graph shows multiple curves, each corresponding to different input voltages \( V_i \), labeled from \( V_{i1} \) to \( V_{i5} \).
- Each curve begins at a low current and increases with increasing \( V_{ce1} \) or \( V_{ds1} \), showing typical transistor behavior.
- The load characteristic is mirrored along the horizontal axis, as suggested by the context, and intersects with the input transistor characteristics.

4. **Key Features and Technical Details:**
- The curves are labeled with numbers 1 through 4, indicating key operating points or transitions.
- At point 1, the curve starts at \( V_{CC} \) or \( V_{DD} \), which is the power-supply voltage.
- The intersection of the input and load characteristics determines the operating point for each input voltage.
- The load characteristic is shifted to the right by the power-supply voltage, aligning with the context provided.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for the input voltages \( V_{i1} \) to \( V_{i5} \), indicating different operating conditions.
- Key points where the curves intersect with the load line are critical for understanding the circuit's operation.
- The graph provides insight into how different input voltages affect the output current and voltage in the presence of an active load.
image_name:(d)
description:The graph labeled (d) is a DC transfer characteristic plot of a common-emitter or common-source amplifier with a current-mirror load.

1. **Type of Graph and Function:**
- This is a DC transfer characteristic graph, which represents the relationship between the input voltage \( V_i \) and the output voltage \( V_{out} \) of the amplifier.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( V_i \), representing the input voltage.
- The vertical axis is labeled \( V_{out} \), representing the output voltage.
- No specific units are mentioned, but they are typically in volts.

3. **Overall Behavior and Trends:**
- The graph shows a sharp transition from a high output voltage to a low output voltage as the input voltage increases.
- Initially, for low values of \( V_i \), the output voltage \( V_{out} \) remains high at approximately \( V_{CC} - V_{CE(sat)} \) or \( V_{DD} \).
- As \( V_i \) increases, the curve drops sharply to a low output voltage near \( V_{CE(sat)} \) or \( 0 \) volts, indicating the transition region.
- The curve has a steep slope in the transition region, showing a rapid change in \( V_{out} \) with respect to \( V_i \).

4. **Key Features and Technical Details:**
- The high output voltage level is approximately \( V_{CC} - V_{CE(sat)} \) or \( V_{DD} \), indicating the saturation region of the amplifier.
- The low output voltage level is near \( V_{CE(sat)} \) or \( 0 \) volts, indicating the cutoff region.
- The transition region is characterized by a steep slope, which is a critical feature for determining the amplifier's switching speed and gain.

5. **Annotations and Specific Data Points:**
- The graph may include markers or annotations at the points \( V_{CC} - V_{CE(sat)} \) or \( V_{DD} \) and \( V_{CE(sat)} \) or \( 0 \) volts to indicate the high and low output levels.
- The exact transition voltage \( V_i \) at which the output switches from high to low can be inferred from the steep slope region, although it is not explicitly marked on the graph.

Figure 4.17 (a) $I-V$ characteristics of the input transistor. (b) $I-V$ characteristic of the active load. (c) $I-V$ characteristics with load characteristic superimposed. (d) dc transfer characteristic of common- emitter or common-source amplifier with current-mirror load.
transistor. Equation 4.116 shows that the load curve should be shifted to the right by an amount equal to the power-supply voltage.

We now consider the dc transfer characteristic of the circuits. Initially, assume that $V_{i}=0$. Then the input transistor is turned off, and the load is saturated in the bipolar case and linear in the MOS case, corresponding to point (1) in Fig. 4.17c. As $V_{i}$ is increased, the input transistor eventually begins to conduct current but the load remains saturated or linear until point (2) is reached. Here the load enters the active region and a small further increase in $V_{i}$ moves the operating point through point (3) to point (4), where the input transistor saturates in the bipolar case or enters the linear region in the MOS case. The change in $V_{i}$ required to move from point (2) to point (4) is small because the slopes of the output $I$ - $V$ characteristics in the active region are small for both transistors. The transfer curve ( $V_{\text {out }}$ as a function of $V_{i}$ ) is sketched in Fig. 4.17d.

A key point of this analysis is that the slope of the output characteristic is not constant, which is important because the slope is the gain of the amplifier. Since the gain of the amplifier depends on the input voltage, the amplifier is nonlinear in general, causing distortion to appear in the amplifier output. For low $V_{i}$, the output is high and the gain is low because the load transistor does not operate in the active region. Similarly, for large $V_{i}$, the output is low and the gain is low because the input transistor does not operate in the active region. To minimize distortion while providing gain, the amplifier should be operated in the intermediate region of $V_{i}$, where all transistors operate in the active region. The range of outputs for which all transistors operate in the active region should be maximized to use the power-supply voltage to the maximum extent. The active loads in Fig. 4.16 maintain high incremental output resistance as long as the drop across the load is more than $V_{\text {OUT }(\min )}$ of the current mirror, which is $\left|V_{C E 2(\text { sat })}\right|$ in the bipolar case and $\left|V_{o v 2}\right|$ in the MOS case here. Therefore, minimizing $V_{\text {OUT(min) }}$ of the mirror maximizes the range of outputs over which the amplifier provides high and nearly constant gain. In contrast, an ideal passive load requires a large voltage drop to give high gain, as shown in (4.111) and (4.112). As a result, the range of outputs for which the gain is high and nearly constant is much less than with an active load.

The gain at any output voltage can be found by finding the slope in Fig. 4.17d. In general, this procedure requires writing equations for the various curves in all of Fig. 4.17. Although this process is required to study the nonlinear behavior of the circuits, it is so complicated analytically that it is difficult to carry out for more than just a couple of transistors at a time. Furthermore, after completing such a large-signal analysis, the results are often so complicated that the effects of the key parameters are difficult to understand, increasing the difficulty of designing with these results. Since we are ultimately interested in being able to analyze and design circuits with a large number of transistors, we will concentrate on the small-signal analysis, which is much simpler to carry out and interpret than the large-signal analysis. Unfortunately, the small-signal analysis provides no information about nonlinearity because it assumes that all transistor parameters are constant.

The primary characteristics of interest in the small-signal analysis here are the voltage gain and output resistance when both devices operate in the active region. The small-signal equivalent circuit is shown in Fig. 4.18. It is drawn for the bipolar case but applies for the MOS case as well when $r_{\pi 1} \rightarrow \infty$ and $r_{\pi 2} \rightarrow \infty$ because $\beta_{0} \rightarrow \infty$. Since $I_{\text {REF }}$ in Fig. 4.16 is assumed constant, the large-signal base-emitter or gate-source voltage of the load transistor is constant. Therefore, the small-signal base-emitter or gate-source voltage of the load transistor, $v_{2}$, is zero. As a result, the small-signal voltage-controlled current $g_{m 2} v_{2}=0$. To find the output resistance of the amplifier, we set the input to zero. Therefore, $v_{1}=0$ and $g_{m 1} v_{1}=0$, and the output resistance is

$$
\begin{equation*}
R_{o}=r_{o 1} \| r_{o 2} \tag{4.117}
\end{equation*}
$$

image_name:Figure 4.18
description:
[
name: r_π1, type: Resistor, value: r_π1, ports: {N1: Vi, N2: GND}
name: r_π2, type: Resistor, value: r_π2, ports: {N1: GND, N2: GND}
name: r_o1, type: Resistor, value: r_o1, ports: {N1: Vo, N2: GND}
name: r_o2, type: Resistor, value: r_o2, ports: {N1: Vo, N2: GND}
name: g_mV1, type: CurrentControlledCurrentSource, ports: {Np: Vo, Nn: GND}
name: g_mV2, type: CurrentControlledCurrentSource, ports: {Np: Vo, Nn: GND}
]
extrainfo:The circuit is a small-signal equivalent of a common-emitter amplifier with active load. It shows the output resistance calculation and voltage gain expression. The input voltage is set to zero for output resistance analysis.

Figure 4.18 Small-signal equivalent circuit for common-emitter amplifier with active load.

Equation 4.117 together with (1.112) and (1.194) show that the output resistance is inversely proportional to the current in both the bipolar and MOS cases.

Since $v_{2}=0, g_{m 1} v_{1}$ flows in $r_{o 1} \| r_{o 2}$ and

$$
\begin{equation*}
A_{v}=-g_{m 1}\left(r_{o 1} \| r_{o 2}\right) \tag{4.118}
\end{equation*}
$$

Substituting (1.91) and (1.112) into (4.118) gives for the bipolar case,

$$
\begin{equation*}
A_{v}=-\frac{1}{\frac{V_{T}}{V_{A 1}}+\frac{V_{T}}{V_{A 2}}} \tag{4.119}
\end{equation*}
$$

Equation 4.119 shows that the gain is independent of the current in the bipolar case because the transconductance is proportional to the current while the output resistance is inversely proportional to the current. Typical values for this voltage gain are in the 1000 to 2000 range. Therefore, the actively loaded bipolar stage provides very high voltage gain.

In contrast, (1.180) shows that the transconductance is proportional to the square root of the current in the MOS case assuming square-law operation. Therefore, the gain in (4.118) is inversely proportional to the square root of the current. With channel lengths less than $1 \mu \mathrm{~m}$, however, the drain current is almost linearly related to the gate-source voltage, as shown in (1.224). Therefore, the transconductance is almost constant, and the gain is inversely proportional to the current with very short channel lengths. Furthermore, typical values for the voltage gain in the MOS case are between 10 and 100, which is much less than with bipolar transistors.

### 4.3.3 Common-Emitter-Common-Source Amplifier with Depletion Load

Actively loaded gain stages using MOS transistors can be realized in processes that include only $n$-channel or only $p$-channel transistors if depletion devices are available. A depletion transistor is useful as a load element because it behaves like a current source when the transistor operates in the active region with the gate shorted to the source.

The $I-V$ characteristic of an $n$-channel MOS depletion-load transistor is illustrated in Fig. 4.19. Neglecting body effect, the device exhibits a very high output resistance (equal to the device $r_{o}$ ) as long as the device operates in the active region. When the body effect is included, the resistance seen across the device drops to approximately $1 / g_{m b}$. A complete gain stage is shown in Fig. 4.20 together with its dc transfer characteristic. The small-signal equivalent model when both transistors operate in the active region is shown in Fig. 4.21. From this circuit, we find that the gain is

$$
\begin{equation*}
\frac{v_{o}}{v_{i}}=-g_{m 1}\left(r_{o 1}\left\|r_{o 2}\right\| \frac{1}{g_{m b 2}}\right) \simeq-\frac{g_{m 1}}{g_{m b 2}} \tag{4.120}
\end{equation*}
$$

For a common-source amplifier with a depletion load, rearranging (4.120) and using (1.180) and (1.200) gives

$$
\begin{equation*}
\frac{v_{o}}{v_{i}} \simeq-\frac{g_{m 1}}{\frac{g_{m b 2}}{g_{m 2}} g_{m 2}}=-\frac{1}{\chi} \sqrt{\frac{(W / L)_{1}}{(W / L)_{2}}} \tag{4.121}
\end{equation*}
$$

image_name:Figure 4.19 (a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vo, G: Vi}
name: M2, type: NMOS, ports: {S: Vo, D: VDD, G: Vo}
]
extrainfo:The circuit is a common-source amplifier with a depletion-mode NMOS load. M1 is the amplifying transistor, and M2 serves as the load. The amplifier is biased with VDD, and the output is taken at Vo. The input voltage is applied at Vi.
image_name:Figure 4.19 (b)
description:Figure 4.19 (b) displays the I-V characteristic of an n-channel depletion-mode load transistor. The graph is a plot with the voltage \( V \) on the x-axis and the current \( I \) on the y-axis. The units are not specified, but it is typical to assume volts for \( V \) and amperes for \( I \). The graph is likely plotted on a linear scale.

The curve shows two distinct regions: the active region and the triode region. The curve begins in the active region, where the current \( I \) remains relatively constant despite increases in \( V \). As \( V \) approaches \( V_{DD} \), the curve transitions into the triode region, where the current decreases sharply.

Two curves are shown: one labeled 'Without body effect' and the other 'With body effect.' The curve with the body effect shows a slightly reduced current compared to the one without the body effect, indicating that the body effect influences the current flow through the transistor.

Significant points are marked on the graph:
- \( (V_{DD} - |V_{ID}|) \): This point indicates the boundary between the active and triode regions.
- \( V_{DD} \): The maximum voltage on the x-axis.

The overall behavior of the graph illustrates how the body effect impacts the I-V characteristics of a depletion-mode transistor, reducing the current in the active region compared to the absence of the body effect.

Figure 4.20 (a) Common-source amplifier with depletion-mode transistor load. (b) dc transfer characteristic.
image_name:Figure 4.21
description:
[
name: ro2, type: Resistor, value: ro2, ports: {N1: Vo, N2: GND}
name: ro1, type: Resistor, value: ro1, ports: {N1: Vo, N2: GND}
name: -gmb2Vo, type: CurrentSource, ports: {Np: Vo, Nn: GND}
name: gm1Vgs1, type: CurrentSource, ports: {Np: GND, Nn: Vo}
name: vi, type: VoltageSource, value: vi, ports: {Np: vi, Nn: GND}
name: vgs1, type: VoltageSource, value: vgs1, ports: {Np: vgs1, Nn: GND}
]
extrainfo:The circuit is a small-signal equivalent of a common-source amplifier with a depletion-mode transistor load. It includes resistors ro1 and ro2, and current sources representing the transconductance and body effect. The input is provided by a voltage source vi, and the output is taken across vo.

Figure 4.21 Small-signal equivalent circuit of the common-source amplifier with depletion load, including the body effect in the load and the channel-length modulation in the load and the common-source device.

From (1.196) and (1.141),

$$
\begin{equation*}
\frac{1}{\chi}=2 \sqrt{2 \phi_{f}} C_{o x} \sqrt{\frac{1+V_{S B} /\left(2 \phi_{f}\right)}{2 q \epsilon N_{A}}} \tag{4.122}
\end{equation*}
$$

Since $\chi$ depends on $V_{o}=V_{S B}$, the incremental voltage gain varies with output voltage, giving the slope variation shown in the active region of Fig. 4.20b.

Equation 4.120 applies for either a common-emitter or common-source driver with a depletion MOS load. If this circuit is implemented in a $p$-well CMOS technology, $M_{2}$ can be built in an isolated well, which can be connected to the source of $M_{2}$. Since this connection sets the source-body voltage in the load transistor to zero, it eliminates the body effect. Setting $g_{m b 2}=0$ in (4.120) gives

$$
\begin{equation*}
\frac{v_{o}}{v_{i}}=-g_{m 1}\left(r_{o 1} \| r_{o 2}\right) \tag{4.123}
\end{equation*}
$$

Although the gain predicted in (4.123) is much higher than in (4.120), this connection reduces the bandwidth of the amplifier because it adds extra capacitance (from the well of $M_{2}$ to the substrate of the integrated circuit) to the amplifier output node.

### 4.3.4 Common-Emitter-Common-Source Amplifier with Diode-Connected Load

In this section, we examine the common-emitter/source amplifier with diode-connected load as shown in MOS form in Fig. 4.22. Since the load is diode connected, the load resistance is no more than the reciprocal of the transconductance of the load. As a result, the gain of this circuit is low, and it is often used in wideband amplifiers that require low gain.

For input voltages that are less than one threshold voltage, transistor $M_{1}$ is off and no current flows in the circuit. When the input voltage exceeds a threshold, transistor $M_{1}$ turns on, and the circuit provides amplification. Assume that both transistors operate in the active region. From (1.157), the drain currents of $M_{1}$ and $M_{2}$ are

$$
\begin{equation*}
I_{1}=\frac{k^{\prime}}{2}\left(\frac{W}{L}\right)_{1}\left(V_{g s 1}-V_{t 1}\right)^{2} \tag{4.124}
\end{equation*}
$$

and

$$
\begin{equation*}
I_{2}=\frac{k^{\prime}}{2}\left(\frac{W}{L}\right)_{2}\left(V_{g s 2}-V_{t 2}\right)^{2} \tag{4.125}
\end{equation*}
$$

image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vo, G: Vi}
name: M2, type: NMOS, ports: {S: Vo, D: VDD, G: VDD}
]
extrainfo:The circuit is a common-source amplifier with an enhancement-mode load, using two NMOS transistors. The input voltage Vi controls the gate of M1, and the output is taken from Vo. M2 is used as a load device with its gate connected to VDD. The circuit provides amplification when the input voltage exceeds a certain threshold, turning on M1.
image_name:(b)
description:The graph labeled (b) is an I-V characteristic curve for a load transistor, likely representing the behavior of transistor $M_2$ in a common-source amplifier circuit.

1. **Type of Graph and Function:**
- This is a current-voltage (I-V) characteristic graph, showing the relationship between the current $I$ through the transistor and the voltage $V$ across it.

2. **Axes Labels and Units:**
- The x-axis represents the voltage $V$, with units typically in volts (V).
- The y-axis represents the current $I$, with units typically in amperes (A).
- The graph does not specify the units explicitly, but these are standard for I-V characteristics.

3. **Overall Behavior and Trends:**
- The graph shows a downward curve starting from a high current at low voltage, decreasing as the voltage increases.
- This behavior indicates that as the voltage across the transistor increases, the current through it decreases, which is typical for a transistor operating in saturation moving towards cutoff.

4. **Key Features and Technical Details:**
- The curve begins at a high current point on the y-axis and approaches zero as it moves rightward along the x-axis.
- The curve is annotated with the expression $\mu_n C_{ox} \left(\frac{W}{L}\right)_2 (V_{DD} - V_{t2})^2$, indicating the maximum current when the transistor is fully on.
- The graph shows a significant point at $V_{DD} - V_{t2}$ on the x-axis, marking a voltage level relevant to the transistor's operation.

5. **Annotations and Specific Data Points:**
- There are annotations indicating the formula for the maximum current, which provides insight into the parameters affecting the transistor's behavior, such as mobility ($\mu_n$), oxide capacitance ($C_{ox}$), and the $W/L$ ratio.
- The curve does not appear to have specific numerical values marked, but the annotated expression suggests that these parameters define the shape and maximum current level of the curve.
image_name:(c)
description:The graph labeled (c) in the image is a transfer characteristic graph of a common-source amplifier with an enhancement-mode load. This graph illustrates the relationship between the input voltage \( V_i \) and the output voltage \( V_o \).

1. **Type of Graph and Function:**
- This is a transfer characteristic graph, which is a plot that shows how the output voltage \( V_o \) changes as the input voltage \( V_i \) is varied.

2. **Axes Labels and Units:**
- The horizontal axis represents the input voltage \( V_i \).
- The vertical axis represents the output voltage \( V_o \).
- Both axes are in volts (V), though specific units are not explicitly marked.

3. **Overall Behavior and Trends:**
- The graph starts at a high output voltage \( V_{DD} \) when both transistors are in cutoff, indicating that no current is flowing through the circuit.
- As \( V_i \) increases past a certain threshold \( V_{t1} \), both transistors become active, and the output voltage \( V_o \) decreases sharply.
- The curve then flattens out as \( V_i \) continues to increase, indicating that transistor \( M_1 \) enters the triode region while \( M_2 \) remains active.

4. **Key Features and Technical Details:**
- The graph shows three distinct regions:
- **Cutoff Region:** At low \( V_i \), where \( V_o = V_{DD} \).
- **Active Region:** As \( V_i \) increases, \( V_o \) drops sharply.
- **Triode Region:** At high \( V_i \), \( V_o \) levels off.
- The critical transition at \( V_{t1} \) is marked, where the behavior shifts from cutoff to active.
- The output voltage \( V_o \) at \( V_{DS(act)} \) is also indicated, showing the point at which \( M_1 \) transitions into the triode region.

5. **Annotations and Specific Data Points:**
- The graph is annotated with labels indicating the regions where both transistors are in cutoff, both are active, and where \( M_1 \) is in the triode region.
- The specific point \( (V_{DD} - V_{t2}) \) is noted on the graph, indicating the voltage level at which both transistors are active.

This graph effectively demonstrates the operational characteristics of the amplifier circuit, highlighting the transitions between different operating regions as the input voltage changes.

Figure 4.22 (a) Common-source amplifier with enhancement-mode load. (b) I-V characteristic of load transistor. (c) Transfer characteristic of the circuit.

From KVL in Fig. 4.22,

$$
\begin{equation*}
V_{o}=V_{D D}-V_{g s 2} \tag{4.126}
\end{equation*}
$$

Solving (4.125) for $V_{g s 2}$ and substituting into (4.126) gives

$$
\begin{equation*}
V_{o}=V_{D D}-V_{t 2}-\sqrt{\frac{2 I_{2}}{k^{\prime}(W / L)_{2}}} \tag{4.127}
\end{equation*}
$$

Since $I_{2}=I_{1}$, (4.127) can be rewritten as

$$
\begin{equation*}
V_{o}=V_{D D}-V_{t 2}-\sqrt{\frac{2 I_{1}}{k^{\prime}(W / L)_{2}}} \tag{4.128}
\end{equation*}
$$

Substituting (4.124) into (4.128) with $V_{g s 1}=V_{i}$ gives

$$
\begin{equation*}
V_{o}=V_{D D}-V_{t 2}-\sqrt{\frac{(W / L)_{1}}{(W / L)_{2}}}\left(V_{i}-V_{t 1}\right) \tag{4.129}
\end{equation*}
$$

Equation 4.129 shows that the slope of the transfer characteristic is the square root of the aspect ratios, assuming that the thresholds are constant. Since the slope of the transfer characteristic is the gain of the amplifier, the gain is constant and the amplifier is linear for a wide range
image_name:Figure 4.23 Small-signal equivalent circuit for the common-source amplifier
description:
[
name: ro1, type: Resistor, value: ro1, ports: {N1: v0, N2: GND}
name: ro2, type: Resistor, value: ro2, ports: {N1: v0, N2: GND}
name: gm1Vgs1, type: VoltageControlledCurrentSource, ports: {Np: v0, Nn: GND}
name: gm2Vs2, type: VoltageControlledCurrentSource, ports: {Np: v0, Nn: GND}
name: gmb2Vs2, type: VoltageControlledCurrentSource, ports: {Np: v0, Nn: GND}
name: Vi, type: VoltageSource, ports: {Np: vi, Nn: GND}
]
extrainfo:This is a small-signal equivalent circuit for a common-source amplifier with an enhancement-mode load. It includes output resistance and body effect in the load. The circuit is used for broadband, low-gain amplifiers with high linearity. The gain is constant and the amplifier is linear for a wide range of inputs if the thresholds are constant.

Figure 4.23 Small-signal equivalent circuit for the common-source amplifier with enhancement-mode load, including output resistance and body effect in the load.
of inputs if the thresholds are constant. This amplifier is useful in implementing broadband, low-gain amplifiers with high linearity.

Equation 4.129 holds when both transistors operate in the active region and when channel-length modulation and body effect are negligible. In practice, the requirement that both transistors operate in the active region leads to an important performance limitation in enhancement-load inverters. The load device remains in the active region only if the drainsource voltage of the load is at least a threshold voltage. For output voltages more positive than $V_{D D}-V_{t 2}$, the load transistor enters the cutoff region and carries no current. Therefore, the amplifier is incapable of producing an output more positive than one threshold voltage below the positive supply. Also, in practice, channel-length modulation and body effect reduce the gain as shown in the following small-signal analysis.

The small-signal voltage gain can be determined by using the small-signal equivalent circuit of Fig. 4.23, in which both the body effect and the output resistance of the two transistors have been included. From KCL at the output node,

$$
\begin{equation*}
g_{m 1} v_{i}+\frac{v_{o}}{r_{o 1}}+\frac{v_{o}}{r_{o 2}}+g_{m 2} v_{o}+g_{m b 2} v_{o}=0 \tag{4.130}
\end{equation*}
$$

Rearranging (4.130) gives

$$
\begin{align*}
\frac{v_{o}}{v_{i}} & =-g_{m 1}\left(\frac{1}{g_{m 2}}\left\|\frac{1}{g_{m b 2}}\right\| r_{o 1} \| r_{o 2}\right) \\
& =-\frac{g_{m 1}}{g_{m 2}}\left(\frac{1}{1+\frac{g_{m b 2}}{g_{m 2}}+\frac{1}{g_{m 2} r_{o 1}}+\frac{1}{g_{m 2} r_{o 2}}}\right) \tag{4.131}
\end{align*}
$$

If $g_{m 2} / g_{m b 2} \gg 1, g_{m 2} r_{o 1} \gg 1$, and $g_{m 2} r_{o 2} \gg 1$,

$$
\begin{equation*}
\frac{v_{o}}{v_{i}} \simeq-\frac{g_{m 1}}{g_{m 2}}=-\sqrt{\frac{(W / L)_{1}}{(W / L)_{2}}} \tag{4.132}
\end{equation*}
$$

as in (4.129). For practical device geometries, this relationship limits the maximum voltage gain to values on the order of 10 to 20.

The bipolar counterpart of the circuit in Fig. 4.22 is a common-emitter amplifier with a diode-connected load. The magnitude of its gain would be approximately equal to the ratio of the transconductances, which would be unity. However, the current that would flow in this circuit would be extremely large for inputs greater than $V_{b e(o n)}$ because the collector current in a bipolar transistor is an exponential function of its base-emitter voltage. To limit the current
but maintain unity gain, equal-value resistors can be placed in series with the emitter of each transistor. Alternatively, the input transistors can be replaced by a differential pair, where the current is limited by the tail current source. In this case, emitter degeneration is used in the differential pair to increase the range of inputs for which all transistors operate in the active region, as in Fig. 3.49. In contrast, source degeneration is rarely used in MOS differential pairs because their transconductance and linear range can be controlled through the device aspect ratios.

### 4.3.5 Differential Pair with Current-Mirror Load

#### 4.3.5.1 Large-Signal Analysis

A straightforward application of the active-load concept to the differential pair would yield the circuit shown in Fig. 4.24a. Assume at first that all $n$-channel transistors are identical
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: X2, D: V01, G: Vi1}
name: M2, type: NMOS, ports: {S: X2, D: V02, G: Vi2}
name: M3, type: PMOS, ports: {S: VDD, D: V01, G: X3}
name: M4, type: PMOS, ports: {S: VDD, D: V02, G: X3}
name: M5, type: PMOS, ports: {S: VDD, D: X3, G: X3}
name: M6, type: NMOS, ports: {S: X1, D: VSS, G: X1}
name: M7, type: NMOS, ports: {S: X1, D: X1, G: X1}
name: M8, type: NMOS, ports: {S: X1, D: X2, G: X1}
name: IREF1, type: CurrentSource, ports: {Np: VDD, Nn: X3}
name: IREF2, type: CurrentSource, ports: {Np: VDD, Nn: X1}
]
extrainfo:The circuit is a differential pair with an active load. It uses NMOS transistors M1 and M2 as the differential pair, with PMOS transistors M3 and M4 as the active load. NMOS transistors M6, M7, and M8 form a current mirror configuration. The circuit is biased using current sources IREF1 and IREF2.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: s1d8, D: d1d3, G: vic}
name: M3, type: PMOS, ports: {S: vdd, D: d1d3, G: g3g5d5}
name: M5, type: PMOS, ports: {S: vdd, D: g3g5d5, G: g3g5d5}
name: M6, type: NMOS, ports: {S: vss, D: g3g9d6, G: g3g9d6}
name: M8, type: NMOS, ports: {S: vss, D: s1d8, G: g3g9d6}
name: IREF1, type: CurrentSource, ports: {Np: vdd, Nn: g3g5d5}
name: IREF2, type: CurrentSource, ports: {Np: g3g9d6, Nn: vss}
]
extrainfo:The circuit is a differential pair with a current-mirror load. It uses PMOS transistors (M3, M5) for the current mirror and NMOS transistors (M1, M6, M8) for the differential pair and tail current source. The current sources IREF1 and IREF2 provide biasing currents.

Figure 4.24 (a) Differential pair with active load. (b) Common-mode half circuit for differential pair with active load.
and that all $p$-channel transistors are identical. Then the differential-mode half circuit for this differential pair is just a common-source amplifier with an active-load, as in Fig. 4.16b. Thus the differential-mode voltage gain is large when all the transistors are biased in the active region. The circuit as it stands, however, has the drawback that the quiescent value of the common-mode output voltage is very sensitive to changes in the drain currents of $M_{3}, M_{4}$, $M_{7}$, and $M_{8}$. As a result, some transistors may operate in or near the triode region, reducing the differential gain or the range of outputs for which the differential gain is high.

This fact is illustrated by the dc common-mode half-circuit shown in Fig. 4.24b. In the common-mode half circuit, the combination of $M_{1}, M_{6}$, and $M_{8}$ form a cascode current mirror, which is connected to the simple current mirror formed by $M_{3}$ and $M_{5}$. If all transistors operate in the active region, $M_{3}$ pushes down a current about equal to $I_{\mathrm{REF} 1}$, and $M_{8}$ pulls down a current about equal to $I_{\mathrm{REF} 2}$. KCL requires that the current in $M_{3}$ must be equal to the current in $M_{8}$. If $I_{\mathrm{REF} 2}=I_{\mathrm{REF} 1}, \mathrm{KCL}$ can be satisfied while all transistors operate in the active region. In practice, however, $I_{\mathrm{REF} 2}$ is not exactly equal to $I_{\mathrm{REF} 1}$, and the current mirrors contain nonzero mismatch, causing changes in the common-mode output to satisfy KCL. Since the output resistance of each current mirror is high, the required change in the common-mode output voltage can be large even for a small mismatch in reference currents or transistors, and one or more transistors can easily move into or near the triode region. For example, suppose that the current pushed down by $M_{3}$ when it operates in the active region is more than the current pulled down by $M_{8}$ when it operates in the active region. Then the common-mode output voltage must rise to reduce the current in $M_{3}$. If the common-mode output voltage rises within $V_{o v 3}$ of $V_{D D}, M_{3}$ operates in the triode region. Furthermore, even if all the transistors continue to be biased in the active region, any change in the common-mode output voltage from its desired value reduces the range of outputs for which the differential gain is high.

Since $M_{1}$ and $M_{2}$ act as cascodes for $M_{7}$ and $M_{8}$, shifts in the common-mode input voltage have little effect on the common-mode output unless the inputs become low enough that $M_{7}$ and $M_{8}$ are forced to operate in the triode region. Therefore, feedback to the inputs of the circuit in Fig. $4.24 a$ is not usually adequate to overcome the common-mode bias problem. Instead, this problem is usually overcome in practice through the use of a separate common-mode feedback circuit, which either adjusts the sum of the currents in $M_{3}$ and $M_{4}$ to be equal to the sum of the currents in $M_{7}$ and $M_{8}$ or vice versa for a given common-mode output voltage. This topic is covered in Chapter 12.

An alternative approach that avoids the need for common-mode feedback is shown in Fig. 4.25. For simplicity in the bipolar circuit shown in Fig. 4.25a, assume that $\beta_{F} \rightarrow \infty$. The circuit in Fig. $4.25 b$ is the MOS counterpart of the bipolar circuit in Fig. $4.25 a$ because each $n p n$ and $p n p$ transistor has been replaced by $n$-channel and $p$-channel MOS transistors, respectively. Then under ideal conditions in both the bipolar and MOS circuits, the active load is a current mirror that forces the current in its output transistor $T_{4}$ to equal the current in its input transistor $T_{3}$. Since the sum of the currents in both transistors of the active load must equal $I_{\text {TAIL }}$ by KCL, $I_{\text {TAIL }} / 2$ flows in each side of the active load. Therefore, these circuits eliminate the common-mode bias problem by allowing the currents in the active load to be set by the tail current source. Furthermore, these circuits each provide a single output with much better rejection of common-mode input signals than a standard resistively loaded differential pair with the output taken off one side only. Although these circuits can be analyzed from a large-signal standpoint, we will concentrate on the small-signal analysis for simplicity.

#### 4.3.5.2 Small-Signal Analysis

We will analyze the low-frequency small-signal behavior of the bipolar circuit shown in Fig. $4.25 a$ because these results cover both the bipolar and MOS cases by letting $\beta_{0} \rightarrow \infty$ and $r_{\pi} \rightarrow \infty$. Key parameters of interest in this circuit include the small-signal
image_name:(a)
description:
[
name: T1, type: NPN, ports: {C: x, B: Vin1, E: p}
name: T2, type: NPN, ports: {C: Vout, B: Vin2, E: p}
name: T3, type: PNP, ports: {C: Vcc, B: x, E: x}
name: T4, type: PNP, ports: {C: Vcc, B: Vout, E: x}
name: V1, type: VoltageSource, ports: {Np: Vin1, Nn: GND}
name: V2, type: VoltageSource, ports: {Np: Vin2, Nn: GND}
name: ITAIL, type: CurrentSource, ports: {Np: p, Nn: Vee}
]
extrainfo:The circuit is an emitter-coupled pair with a current-mirror load. It uses NPN transistors T1 and T2 for differential input and PNP transistors T3 and T4 for the current mirror. The tail current source is ITAIL. The circuit is powered by Vcc and Vee.
image_name:(b)
description:
[
name: T1, type: NMOS, ports: {S: P, D: X, G: Vin1}
name: T2, type: NMOS, ports: {S: P, D: Vout, G: Vin2}
name: T3, type: PMOS, ports: {S: VDD, D: X, G: X}
name: T4, type: PMOS, ports: {S: VDD, D: Vout, G: X}
name: V1, type: VoltageSource, value: V1, ports: {Np: Vin1, Nn: GND}
name: V2, type: VoltageSource, value: V2, ports: {Np: Vin2, Nn: GND}
name: ITAIL, type: CurrentSource, value: ITAIL, ports: {Np: P, Nn: VSS}
]
extrainfo:The circuit is a source-coupled pair with a current-mirror load, using NMOS and PMOS transistors. It operates between VDD and VSS power supplies, with differential inputs Vin1 and Vin2, and a differential output Vout. The current source ITAIL provides biasing current.

Figure 4.25 (a) Emitter-coupled pair with current-mirror load. (b) Source-coupled pair with current-mirror load (MOS counterpart).
transconductance and output resistance. (The product of these two quantities gives the smallsignal voltage gain with no load.) Since only one transistor in the active load is diode connected, the circuit is not symmetrical and a half-circuit approach is not useful. Therefore, we will analyze the small-signal model of this circuit directly. Assume that all transistors operate in the active region with $r_{\mu} \rightarrow \infty$ and $r_{b}=0$. Let $r_{\text {tail }}$ represent the output resistance of the tail current source $I_{\text {TAIL }}$. The resulting small-signal circuit is shown in Fig. 4.26a.

Since $T_{3}$ and $T_{4}$ form a current mirror, we expect the mirror output current to be approximately equal to the mirror input current. Therefore, we will write

$$
\begin{equation*}
g_{m 4} v_{3}=i_{3}\left(1-\epsilon_{m}\right) \tag{4.133}
\end{equation*}
$$

image_name:(a)
description:
[
name: V_i1, type: VoltageSource, value: V_i1, ports: {Np: V_i1, Nn: GND}
name: r_1, type: Resistor, value: r_1, ports: {N1: V_i1, N2: V_a}
name: g_m1, type: CurrentControlledCurrentSource, value: g_m1V_a, ports: {Np: GND, Nn: 1}
name: r_o1, type: Resistor, value: r_o1, ports: {N1: 1, N2: GND}
name: r_tail, type: Resistor, value: r_tail, ports: {N1: 1, N2: GND}
name: V_i2, type: VoltageSource, value: V_i2, ports: {Np: V_i2, Nn: GND}
name: r_2, type: Resistor, value: r_2, ports: {N1: V_i2, N2: V_b}
name: g_m2, type: CurrentControlledCurrentSource, value: g_m2V_b, ports: {Np: 2, Nn: 1}
name: r_o2, type: Resistor, value: r_o2, ports: {N1: 2, N2: 1}
name: r_3, type: Resistor, value: r_3, ports: {N1: 3, N2: V_3}
name: g_m3, type: CurrentControlledCurrentSource, value: g_m3V_3, ports: {Np: 3, Nn: GND}
name: r_4, type: Resistor, value: r_4, ports: {N1: 3, N2: GND}
name: g_m4, type: CurrentControlledCurrentSource, value: g_m4V_3, ports: {Np: 2, Nn: GND}
name: r_o1, type: Resistor, value: r_o1, ports: {N1: GND, N2: GND}
name: i_3, type: CurrentSource, value: i_3, ports: {Np: 3, Nn: 1}
name: i_2, type: CurrentSource, value: i_2, ports: {Np: 2, Nn: GND}
]
extrainfo:The circuit is a small-signal equivalent of a differential pair with a current-mirror load. It includes resistors, controlled current sources, and independent voltage and current sources. The current mirror is formed by g_m3 and g_m4, where g_m4 mirrors the input current i_3 to the output. The resistors r_1, r_2, r_3, and r_4 are connected to various nodes to form the differential pair and current mirror structure.
image_name:(b)
description:
[
name: Vii, type: VoltageSource, value: Vii, ports: {Np: Vi1, Nn: GND}
name: Vi1, type: VoltageSource, value: Vi1, ports: {Np: Va, Nn: GND}
name: rπ(dp), type: Resistor, value: rπ(dp), ports: {N1: Vi2, N2: Vb}
name: ro(dp), type: Resistor, value: ro(dp), ports: {N1: Va, N2: 1}
name: rtail, type: Resistor, value: rtail, ports: {N1: 1, N2: GND}
name: ro(dp), type: Resistor, value: ro(dp), ports: {N1: Vb, N2: 1}
name: g1m(dp)Va, type: CurrentControlledCurrentSource, value: g1m(dp)Va, ports: {Np: Va, Nn: 1}
name: g1m(dp)Vb, type: CurrentControlledCurrentSource, value: g1m(dp)Vb, ports: {Np: Vb, Nn: 1}
name: Vi2, type: VoltageSource, value: Vi2, ports: {Np: Vb, Nn: GND}
name: g1m(mir), type: CurrentControlledCurrentSource, value: g1m(mir), ports: {Np: 3, Nn: 1}
name: (1-εm)i3, type: CurrentControlledCurrentSource, value: (1-εm)i3, ports: {Np: 3, Nn: 2}
name: t_tail, type: CurrentSource, value: t_tail, ports: {Np: 1, Nn: GND}
]
extrainfo:The circuit diagram (b) represents a small-signal model of a differential pair with a current-mirror load. It includes a tail current source 't_tail' and various resistors and controlled current sources depicting the behavior of the transistors in the differential pair. The current mirror is represented by the current-controlled current source '(1-εm)i3', which models the systematic gain error in the mirror. The nodes are labeled to indicate connections between the voltage sources, resistors, and current sources.

Figure 4.26 (a) Small-signal equivalent circuit, differential pair with current-mirror load. (b) Simplified drawing of small-signal model of differential pair with current-mirror load.
where $\epsilon_{m}$ is the systematic gain error of the current mirror calculated from small-signal parameters. Let $r_{3}$ represent the total resistance connected between the base or gate of $T_{3}$ and the power supply. Then $r_{3}$ is the parallel combination of $1 / g_{m 3}, r_{\pi 3}, r_{\pi 4}$, and $r_{o 3}$. Under the simplifying assumptions that $\beta_{0} \gg 1$ and $g_{m} r_{o} \gg 1$, this parallel combination is approximately equal to $1 / g_{m 3}$. Then the drop across $r_{\pi 4}$ is

$$
\begin{equation*}
v_{3}=i_{3} r_{3} \simeq \frac{i_{3}}{g_{m 3}} \tag{4.134}
\end{equation*}
$$

We will also assume that the two transistors in the differential pair match perfectly and operate with equal dc currents, as do the two transistors in the current-mirror load. Then $g_{m(d p)}=g_{m 1}$
$=g_{m 2}, g_{m(m i r)}=g_{m 3}=g_{m 4}, r_{\pi(d p)}=r_{\pi 1}=r_{\pi 2}, r_{\pi(m i r)}=r_{\pi 3}=r_{\pi 4}, r_{o(d p)}=r_{o 1}=r_{o 2}$, and $r_{o(\text { mir })}=r_{o 3}=r_{o 4}$. From (4.134), the resulting voltage-controlled current $g_{m 4} v_{3}$ is

$$
\begin{equation*}
g_{m 4} v_{3}=g_{m(m i r)} v_{3} \simeq g_{m(\operatorname{mir})} \frac{i_{3}}{g_{m(\text { mir })}}=i_{3} \tag{4.135}
\end{equation*}
$$

Equations 4.133 and 4.135 show that $\epsilon_{m} \simeq 0$ and thus the active load acts as a current mirror in a small-signal sense, as expected. Using (4.133), the small-signal circuit is redrawn in Fig. $4.26 b$ with the output grounded to find the transconductance. Note that $r_{o 4}$ is omitted because it is attached to a small-signal ground on both ends.

From KCL at node (1),

$$
\begin{equation*}
\left(v_{i 1}-v_{1}+v_{i 2}-v_{1}\right)\left(\frac{1}{r_{\pi(d p)}}+g_{m(d p)}\right)+\frac{v_{3}-v_{1}}{r_{o(d p)}}-\frac{v_{1}}{r_{o(d p)} \| r_{\text {tail }}}=0 \tag{4.136}
\end{equation*}
$$

where $v_{1}$ and $v_{3}$ are the voltages to ground from nodes (1) and (3). To complete an exact small-signal analysis, KCL equations could also be written at nodes (2) and (3), and these KCL equations plus (4.136) could be solved simultaneously. However, this procedure is complicated algebraically and leads to an equation that is difficult to interpret. To simplify the analysis, we will assume at first that $r_{\text {tail }} \rightarrow \infty$ and $r_{o(d p)} \rightarrow \infty$ since the transistors are primarily controlled by their base-emitter or gate-source voltages. Then from (4.136)

$$
\begin{equation*}
v_{1}=\frac{v_{i 1}+v_{i 2}}{2}=v_{i c} \tag{4.137}
\end{equation*}
$$

where $v_{i c}$ is the common-mode component of the input. Let $v_{i d}=v_{i 1}-v_{i 2}$ represent the differential-mode component of the input. Then $v_{i 1}=v_{i c}+v_{i d} / 2$ and $v_{i 2}=v_{i c}-v_{i d} / 2$, and the small-signal collector or drain currents

$$
\begin{equation*}
i_{1}=g_{m(d p)}\left(v_{i 1}-v_{1}\right)=\frac{g_{m(d p)} v_{i d}}{2} \tag{4.138}
\end{equation*}
$$

and

$$
\begin{equation*}
i_{2}=g_{m(d p)}\left(v_{i 2}-v_{1}\right)=-\frac{g_{m(d p)} v_{i d}}{2} \tag{4.139}
\end{equation*}
$$

With a resistive load and a single-ended output, only $i_{2}$ flows in the output. Therefore, the transconductance for a differential-mode ( dm ) input with a passive load is

$$
\begin{equation*}
G_{m}[d m]=\left.\frac{i_{\text {out }}}{v_{i d}}\right|_{v_{\text {out }}=0}=-\frac{i_{2}}{v_{i d}}=\frac{g_{m(d p)}}{2} \tag{4.140}
\end{equation*}
$$

On the other hand, with the active loads in Fig. 4.25, not only $i_{2}$ but also most of $i_{3}$ flows in the output because of the action of the current mirror, as shown by (4.135). Therefore, the output current in Fig. 4.26b is

$$
\begin{equation*}
i_{\mathrm{out}}=-\left(1-\epsilon_{m}\right) i_{3}-i_{2} \tag{4.141}
\end{equation*}
$$

Assume at first that the current mirror is ideal so that $\epsilon_{m}=0$. Then since $i_{3}=-i_{1}$, substituting (4.138) and (4.139) in (4.141) gives

$$
\begin{equation*}
i_{\mathrm{out}}=g_{m(d p)} v_{i d} \tag{4.142}
\end{equation*}
$$

Therefore, with an active load,

$$
\begin{equation*}
G_{m}[d m]=\left.\frac{i_{\text {out }}}{v_{i d}}\right|_{v_{\text {out }}=0}=g_{m(d p)} \tag{4.143}
\end{equation*}
$$

Equation 4.143 applies for both the bipolar and MOS amplifiers shown in Fig. 4.25. Comparing (4.140) and (4.143) shows that the current-mirror load doubles the differential transconductance
compared to the passive-load case. This result stems from the fact that the current mirror creates a second signal path to the output. (The first path is through the differential pair.) Although frequency response is not analyzed in this chapter, note that the two signal paths usually have different frequency responses, which is often important in high-speed applications.

The key assumptions that led to (4.142) and (4.143) are that the current mirror is ideal so $\epsilon_{m}=0$ and that $r_{\text {tail }} \rightarrow \infty$ and $r_{o(d p)} \rightarrow \infty$. Under these assumptions, the output current is independent of the common-mode input. In practice, none of these assumptions is exactly true, and the output current depends on the common-mode input. However, this dependence is small because the active load greatly enhances the common-mode rejection ratio of this stage, as shown in Section 4.3.5.3.

Another important parameter of the differential pair with active load is the output resistance. The output resistance is calculated using the circuit of Fig. 4.27, in which a test voltage source $v_{t}$ is applied at the output while the inputs are connected to small-signal ground. The resulting current $i_{t}$ has four components. The current in $r_{o 4}$ is

$$
\begin{equation*}
i_{t 1}=\frac{v_{t}}{r_{o 4}} \tag{4.144}
\end{equation*}
$$

The resistance in the emitter or source lead of $T_{2}$ is $r_{\text {tail }}$ in parallel with the resistance seen looking into the emitter or source of $T_{1}$, which is approximately $1 / g_{m 1}$. Thus, using (3.99) for a transistor with degeneration, we find that the effective output resistance looking into the collector or drain of $T_{2}$ is

$$
\begin{equation*}
R_{o 2} \simeq r_{o 2}\left(1+g_{m 2} \frac{1}{g_{m 1}}\right)=2 r_{o 2} \tag{4.145}
\end{equation*}
$$

Hence

$$
\begin{equation*}
i_{t 2}+i_{t 4} \simeq \frac{v_{t}}{2 r_{o 2}} \tag{4.146}
\end{equation*}
$$

If $r_{\text {tail }} \gg 1 / g_{m 1}$, this current flows into the emitter or source of $T_{1}$, and is mirrored to the output with a gain of approximately unity to produce

$$
\begin{equation*}
i_{t 3} \simeq i_{t 2}+i_{t 4} \simeq \frac{v_{t}}{2 r_{o 2}} \tag{4.147}
\end{equation*}
$$

image_name:Figure 4.27
description:
[
name: r_π1, type: Resistor, value: r_π1, ports: {N1: va, N2: GND}
name: r_π2, type: Resistor, value: r_π2, ports: {N1: vb, N2: GND}
name: r_π3, type: Resistor, value: r_π3, ports: {N1: v3, N2: X}
name: r_π4, type: Resistor, value: r_π4, ports: {N1: v3, N2: X}
name: r_o1, type: Resistor, value: r_o1, ports: {N1: X, N2: 1}
name: r_o2, type: Resistor, value: r_o2, ports: {N1: vt, N2: 1}
name: r_o3, type: Resistor, value: r_o3, ports: {N1: v3, N2: X}
name: r_o4, type: Resistor, value: r_o4, ports: {N1: vt, N2: GND}
name: r_tail, type: Resistor, value: r_tail, ports: {N1: 1, N2: GND}
name: g_m1V_a, type: CurrentSource, ports: {Np: X, Nn: 1}
name: g_m2V_b, type: CurrentSource, ports: {Np: 1, Nn: vt}
name: g_m3V_3, type: CurrentSource, ports: {Np: v3, Nn: X}
name: g_m4V_3, type: CurrentSource, ports: {Np: vt, Nn: GND}
name: V_t, type: VoltageSource, value: V_t, ports: {Np: vt, Nn: GND}
]
extrainfo:The circuit is a differential pair with a current-mirror load. It is used to calculate the output resistance. The resistors r_π and r_o are used to model the transistors' small-signal parameters, and the current sources represent the transconductance of the transistors.

Figure 4.27 Circuit for calculation of the output resistance of the differential pair with current-mirror load.

Thus

$$
\begin{equation*}
i_{t}=i_{t 1}+i_{t 2}+i_{t 3}+i_{t 4} \simeq v_{t}\left(\frac{1}{r_{o 4}}+\frac{1}{r_{o 2}}\right) \tag{4.148}
\end{equation*}
$$

Since $r_{o 2}=r_{o(d p)}$ and $r_{o 4}=r_{o(m i r)}$,

$$
\begin{equation*}
R_{o}=\left.\frac{v_{t}}{i_{t}}\right|_{\substack{v_{i 1}=0 \\ v_{i 2}=0}} \simeq \frac{1}{\frac{1}{r_{o(d p)}}+\frac{1}{r_{o(m i r)}}}=r_{o(d p)} \| r_{o(m i r)} \tag{4.149}
\end{equation*}
$$

The result in (4.149) applies for both the bipolar and MOS amplifiers shown in Fig. 4.25. In multistage bipolar amplifiers, the low-frequency gain of the loaded circuit is likely to be reduced by the input resistance of the next stage because the output resistance is high. In contrast, lowfrequency loading is probably not an issue in multistage MOS amplifiers because the next stage has infinite input resistance if the input is the gate of an MOS transistor.

Finally, although the source-coupled pair has infinite input resistance, the emitter-coupled pair has finite input resistance because $\beta_{0}$ is finite. If the effects of the $r_{o}$ of $T_{2}$ and $T_{4}$ are neglected, the differential input resistance of the actively loaded emitter-coupled pair is simply $2 r_{\pi(d p)}$ as in the resistively loaded case. In practice, however, the asymmetry of the circuit together with the high voltage gain cause feedback to occur through the output resistance of $T_{2}$ to node (1). This feedback causes the input resistance to differ slightly from $2 r_{\pi(d p)}$.

In summary, the actively loaded differential pair is capable of providing differential-to-single-ended conversion, that is, the conversion from a differential voltage to a voltage referenced to the ground potential. The high output resistance of the circuit requires that the next stage must have high input resistance if the large gain is to be realized. A small-signal two-port equivalent circuit for the stage is shown in Fig. 4.28.

#### 4.3.5.3 Common-Mode Rejection Ratio

In addition to providing high voltage gain, the circuits in Fig. 4.25 provide conversion from a differential input signal to an output signal that is referenced to ground. Such a conversion is required in all differential-input, single-ended output amplifiers.

The simplest differential-to-single-ended converter is a resistively loaded differential pair in which the output is taken from only one side, as shown in Fig. 4.29a. In this case, $A_{d m}>0$, $A_{c m}<0$, and the output is

$$
\begin{equation*}
v_{o}=-\frac{v_{o d}}{2}+v_{o c}=-\frac{A_{d m} v_{i d}}{2}+A_{c m} v_{i c} \tag{4.150}
\end{equation*}
$$

image_name:Figure 4.28
description:
[
'name': 'Ri', 'type': 'Resistor', 'value': '2π', 'ports': {'N1': 'Vid', 'N2': 'Vid'
'name': 'Gm[dm]', 'type': 'VoltageControlledCurrentSource', 'value': 'gm', 'ports': {'Np': 'Vid', 'Nn': 'GND'
'name': 'Ro', 'type': 'Resistor', 'value': 'ro(dp)||ro(mir)', 'ports': {'N1': 'Vxrt', 'N2': 'Vout'
]
extrainfo:The circuit is a differential-to-single-ended converter with resistive and active loading, using a voltage-controlled current source to convert the differential input voltage to a single-ended output voltage.

Figure 4.28 Two-port representation of small-signal properties of differential pair with current-mirror load. The effects of asymmetrical input resistance have been neglected.
image_name:(a)
description:
[
name: T1, type: NMOS, ports: {S: GND, D: d1, G: vi1}
name: T2, type: NMOS, ports: {S: GND, D: d1, G: vi2}
name: T3, type: PMOS, ports: {S: VDD, D: d1, G: p}
name: T4, type: PMOS, ports: {S: VDD, D: d1, G: p}
name: T5, type: NMOS, ports: {S: GND, D: p, G: vi1}
name: T6, type: NMOS, ports: {S: GND, D: p, G: vi2}
name: RL, type: Resistor, value: RL, ports: {N1: VDD, N2: d1}
name: L1, type: Inductor, value: L1, ports: {N1: d1, N2: Vout}
name: IBIAS, type: CurrentSource, value: IBIAS, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a differential-to-single-ended converter with resistive and active loading. It uses a voltage-controlled current source to convert the differential input voltage to a single-ended output voltage. The diagram represents a differential pair with a current-mirror load, focusing on small-signal properties.
image_name:(b)
description:
[
name: T1, type: NMOS, ports: {S: p, D: d1, G: vi1}
name: T5, type: NMOS, ports: {S: p, D: vo, G: vi2}
name: T6, type: NPN, ports: {C: g5g6d6, B: g5g6d6, E: VSS}
name: T3, type: PMOS, ports: {S: VDD, D: x, G: x}
name: T4, type: PMOS, ports: {S: VDD, D: vo, G: x}
name: RL, type: Resistor, value: RL, ports: {N1: VDD, N2: vo}
name: C1, type: Capacitor, value: C1, ports: {N1: VDD, N2: vo}
name: L1, type: Inductor, value: L1, ports: {N1: VDD, N2: vo}
name: IBIAS, type: CurrentSource, value: IBIAS, ports: {Np: VDD, Nn: g5g6d6}
]
extrainfo:The circuit diagram represents a differential-to-single-ended converter with active loading. It utilizes a current mirror load and voltage-controlled current source to convert differential input to single-ended output. The circuit is designed to minimize the effects of common-mode signals at the input.

Figure 4.29 Differential-to-single-ended conversion using (a) resistively loaded differential pairs and (b) actively loaded differential pairs.

$$
\begin{align*}
v_{o} & =-\frac{A_{d m}}{2}\left(v_{i d}-\frac{2 A_{c m}}{A_{d m}} v_{i c}\right)=-\frac{A_{d m}}{2}\left(v_{i d}+2\left|\frac{A_{c m}}{A_{d m}}\right| v_{i c}\right)  \tag{4.151}\\
& =-\frac{A_{d m}}{2}\left(v_{i d}+\frac{2 v_{i c}}{\mathrm{CMRR}}\right) \tag{4.152}
\end{align*}
$$

Thus, common-mode signals at the input will cause changes in the output voltage. The commonmode rejection ratio (CMRR) is

$$
\begin{equation*}
\mathrm{CMRR}=\left|\frac{A_{d m}}{A_{c m}}\right|=\left|\frac{G_{m}[\mathrm{dm}] R_{o}}{G_{m}[\mathrm{~cm}] R_{o}}\right|=\left|\frac{G_{m}[\mathrm{dm}]}{G_{m}[\mathrm{~cm}]}\right| \tag{4.153}
\end{equation*}
$$

where the common-mode (cm) transconductance is

$$
\begin{equation*}
G_{m}[\mathrm{~cm}]=\left.\frac{i_{\mathrm{out}}}{v_{i c}}\right|_{v_{\mathrm{out}}=0} \tag{4.154}
\end{equation*}
$$

Since the circuits in Fig. 4.29a are symmetrical, a common-mode half circuit can be used to find $G_{m}[\mathrm{~cm}]$. The common-mode half circuit is a common-emitter/source amplifier with degeneration. From (3.93) and (3.104),

$$
\begin{equation*}
G_{m}[\mathrm{~cm}]=-\frac{i_{2}}{v_{i c}} \simeq-\frac{g_{m(d p)}}{1+g_{m(d p)}\left(2 r_{\text {tail }}\right)} \tag{4.155}
\end{equation*}
$$

where $g_{m(d p)}=g_{m 1}=g_{m 2}$ and $r_{\text {tail }}$ represents the output resistance of the tail current source $T_{5}$. The negative sign appears in (4.155) because the output current is defined as positive when it flows from the output terminal into the small-signal ground to be consistent with the differential case, as in Fig. 4.26b. Equation 4.155 applies for both the bipolar and MOS cases if the base current is ignored in the bipolar case, the body effect is ignored in the MOS case, and $r_{o 1}$ and $r_{o 2}$ are ignored in both cases. Substituting (4.140) and (4.155) into (4.153) gives

$$
\begin{equation*}
\mathrm{CMRR}=\frac{1+2 g_{m(d p)} r_{\text {tail }}}{2} \simeq g_{m(d p)} r_{\mathrm{tail}}=g_{m 1} r_{o 5} \tag{4.156}
\end{equation*}
$$

Equation 4.156 shows that the common-mode rejection ratio here is about half that in (3.193) because the outputs in Fig. 4.29 are taken only from one side of each differential pair instead of from both sides, reducing the differential-mode gain by a factor of two. The result in (4.156) applies for both the bipolar and MOS amplifiers shown in Fig. 4.29a. Because $g_{m} r_{o}$ is much higher for bipolar transistors than MOS transistors, the CMRR of a bipolar differential pair with resistive load is much higher than that of its MOS counterpart.

On the other hand, the active-load stages shown in Fig $4.29 b$ have common-mode rejection ratios much superior to those of the corresponding circuits in Fig.4.29a. Assume that the outputs in Fig. $4.29 b$ are connected to small-signal ground to allow calculation of the common-mode transconductance. The small-signal model is the same as shown in Fig. $4.26 b$ with $v_{i 1}=v_{i 2}=$ $v_{i c}$. For simplicity, let $\beta_{0} \rightarrow \infty$ and $r_{\pi} \rightarrow \infty$ at first. As with a resistive load, changes in the common-mode input will cause changes in the tail bias current $i_{\text {tail }}$ because the output resistance of $T_{5}$ is finite. If we assume that the currents in the differential-pair transistors are controlled only by the base-emitter or gate-source voltages, the change in the current in $T_{1}$ and $T_{2}$ is

$$
\begin{equation*}
i_{1}=i_{2}=\frac{i_{\text {tail }}}{2} \tag{4.157}
\end{equation*}
$$

If $\epsilon_{m}=0$, the gain of the current mirror is unity. Then substituting (4.157) into (4.141) with $i_{3}=-i_{1}$ gives

$$
\begin{equation*}
i_{\text {out }}=-i_{3}-i_{2}=i_{1}-i_{2}=0 \tag{4.158}
\end{equation*}
$$

As a result,

$$
\begin{equation*}
G_{m}[\mathrm{~cm}]=\left.\frac{i_{\text {out }}}{v_{i c}}\right|_{v_{\text {out }}=0}=0 \tag{4.159}
\end{equation*}
$$

Therefore,

$$
\begin{equation*}
\mathrm{CMRR} \rightarrow \infty \tag{4.160}
\end{equation*}
$$

The common-mode rejection ratio in (4.160) is infinite because the change in the current in $T_{4}$ cancels that in $T_{2}$ even when $r_{\text {tail }}$ is finite under these assumptions.

The key assumptions that led to (4.160) are that $r_{o(d p)} \rightarrow \infty$ so $i_{1}=i_{2}$ and that the current mirror is ideal so $\epsilon_{m}=0$. In practice, the currents in the differential-pair transistors are not
only controlled by their base-emitter or gate-source voltages, but also to some extent by their collector-emitter or drain-source voltages. As a result, $i_{1}$ is not exactly equal to $i_{2}$ because of finite $r_{o(d p)}$ in $T_{1}$ and $T_{2}$. Furthermore, the gain of the current mirror is not exactly unity, which means that $\epsilon_{m}$ is not exactly zero in practice because of finite $r_{o(m i r)}$ in $T_{3}$ and $T_{4}$. Finite $\beta_{0}$ also affects the systematic gain error of the current mirror when bipolar transistors are used. For these reasons, the common-mode rejection ratio is finite in practice. However, the use of the active load greatly improves the common-mode rejection ratio compared to the resistive load case, as we will show next.

Suppose that

$$
\begin{equation*}
i_{1}=i_{2}\left(1-\epsilon_{d}\right) \tag{4.161}
\end{equation*}
$$

where $\epsilon_{d}$ can be thought of as the gain error in the differential pair. Substituting (4.161) into (4.141) with $i_{3}=-i_{1}$ gives

$$
\begin{equation*}
i_{\text {out }}=i_{1}\left(1-\epsilon_{m}\right)-i_{2}=i_{2}\left(\left(1-\epsilon_{d}\right)\left(1-\epsilon_{m}\right)-1\right) \tag{4.162}
\end{equation*}
$$

Rearranging (4.162) gives

$$
\begin{equation*}
i_{\mathrm{out}}=-i_{2}\left(\epsilon_{d}+\epsilon_{m}-\epsilon_{d} \epsilon_{m}\right) \tag{4.163}
\end{equation*}
$$

If $\epsilon_{d} \ll 1$ and $\epsilon_{m} \ll 1$, the product term $\epsilon_{d} \epsilon_{m}$ is a second-order error and can be neglected. Therefore,

$$
\begin{equation*}
i_{\mathrm{out}} \simeq-i_{2}\left(\epsilon_{d}+\epsilon_{m}\right) \tag{4.164}
\end{equation*}
$$

Substituting (4.164) into (4.154) gives

$$
\begin{equation*}
G_{m}[\mathrm{~cm}] \simeq-\left(\frac{i_{2}}{v_{i c}}\right)\left(\epsilon_{d}+\epsilon_{m}\right) \tag{4.165}
\end{equation*}
$$

Equation 4.165 applies for the active-load circuits shown in Fig. 4.29b; however, the first term has approximately the same value as in the passive-load case. Therefore, we will substitute (4.155) into (4.165), which gives

$$
\begin{equation*}
G_{m}[c m] \simeq-\left(\frac{g_{m(d p)}}{1+g_{m(d p)}\left(2 r_{\text {tail }}\right)}\right)\left(\epsilon_{d}+\epsilon_{m}\right) \tag{4.166}
\end{equation*}
$$

Substituting (4.166) and (4.143) into (4.153) gives

$$
\begin{equation*}
\mathrm{CMRR}=\left|\frac{G_{m}[\mathrm{dm}]}{G_{m}[\mathrm{~cm}]}\right| \simeq \frac{1+2 g_{m(d p)} r_{\mathrm{tail}}}{\left(\epsilon_{d}+\epsilon_{m}\right)} \tag{4.167}
\end{equation*}
$$

Comparing (4.167) and (4.156) shows that the active load improves the common-mode rejection ratio by a factor of $2 /\left(\epsilon_{d}+\epsilon_{m}\right)$. The factor of 2 in the numerator of this expression stems from the increase in the differential transconductance, and the denominator stems from the decrease in the common-mode transconductance.

To find $\epsilon_{d}$, we will refer to Fig. $4.26 b$ with $v_{i 1}=v_{i 2}=v_{i c}$. First, we write

$$
\begin{equation*}
i_{1}=g_{m(d p)}\left(v_{i c}-v_{1}\right)+\frac{v_{3}-v_{1}}{r_{o(d p)}} \tag{4.168}
\end{equation*}
$$

and

$$
\begin{equation*}
i_{2}=g_{m(d p)}\left(v_{i c}-v_{1}\right)-\frac{v_{1}}{r_{o(d p)}} \tag{4.169}
\end{equation*}
$$

Substituting (4.134) and $i_{3}=-i_{1}$ into (4.168) gives

$$
\begin{equation*}
i_{1} \simeq g_{m(d p)}\left(v_{i c}-v_{1}\right)-\frac{v_{1}}{r_{o(d p)}}-\frac{i_{1}}{g_{m(m i r)} r_{o(d p)}} \tag{4.170}
\end{equation*}
$$

Equation 4.170 can be rearranged to give

$$
\begin{equation*}
\left(\frac{1+g_{m(m i r)} r_{o(d p)}}{g_{m(m i r)} r_{o(d p)}}\right) i_{1} \simeq g_{m(d p)}\left(v_{i c}-v_{1}\right)-\frac{v_{1}}{r_{o(d p)}} \tag{4.171}
\end{equation*}
$$

Substituting (4.169) into (4.171) gives

$$
\begin{equation*}
i_{1} \simeq\left(\frac{g_{m(\operatorname{mir})} r_{o(d p)}}{1+g_{m(m i r)} r_{o(d p)}}\right) i_{2} \tag{4.172}
\end{equation*}
$$

Substituting (4.161) into (4.172) gives

$$
\begin{equation*}
\epsilon_{d} \simeq \frac{1}{1+g_{m(\operatorname{mir})} r_{o(d p)}} \tag{4.173}
\end{equation*}
$$

To find $\epsilon_{m}$, we will again refer to Fig. $4.26 b$ with $v_{i 1}=v_{i 2}=v_{i c}$. In writing (4.134), we assumed that $r_{3} \simeq 1 / g_{m 3}$. We will now reconsider this assumption and write

$$
\begin{equation*}
r_{3}=\frac{1}{g_{m 3}}\left\|r_{\pi 3}\right\| r_{\pi 4} \| r_{o 3} \tag{4.174}
\end{equation*}
$$

We will still assume that the two transistors in the differential pair match perfectly and operate with equal dc currents, as do the two transistors in the active load. Then (4.174) can be rewritten as

$$
\begin{equation*}
r_{3}=\frac{r_{\pi(m i r)} r_{o(m i r)}}{r_{\pi(m i r)}+2 r_{o(m i r)}+g_{m(m i r)} r_{\pi(m i r)} r_{o(m i r)}} \tag{4.175}
\end{equation*}
$$

Substituting (4.175) into (4.135) gives

$$
\begin{equation*}
g_{m 4} 4 v_{3}=g_{m 4} i_{3} r_{3}=\frac{g_{m(m i r)} r_{\pi(m i r)} r_{o(m i r)} i_{3}}{r_{\pi(m i r)}+2 r_{o(m i r)}+g_{m(m i r)} r_{\pi(m i r)} r_{o(m i r)}} \tag{4.176}
\end{equation*}
$$

Substituting (4.133) into (4.176) gives

$$
\begin{equation*}
\epsilon_{m}=\frac{r_{\pi(m i r)}+2 r_{o(m i r)}}{r_{\pi(m i r)}+2 r_{o(m i r)}+g_{m(m i r)} r_{\pi(m i r)} r_{o(m i r)}} \tag{4.177}
\end{equation*}
$$

For bipolar transistors, $r_{\pi}$ is usually much less than $r_{o}$; therefore,

$$
\begin{equation*}
\epsilon_{m}[b i p]=\frac{2+\frac{r_{\pi(m i r)}}{r_{o(m i r)}}}{2+\frac{r_{\pi(m i r)}}{r_{o(m i r)}}+g_{m(m i r)} r_{\pi(m i r)}} \simeq \frac{1}{1+\frac{g_{m(m i r)} r_{\pi(m i r)}}{2}}=\frac{1}{1+\frac{\beta_{0}}{2}} \tag{4.178}
\end{equation*}
$$

Since $r_{\pi} \rightarrow \infty$ for MOS transistors,

$$
\begin{equation*}
\epsilon_{m}[M O S]=\frac{1}{1+g_{m(m i r)} r_{o(m i r)}} \tag{4.179}
\end{equation*}
$$

For the bipolar circuit in Fig. 4.29b, substituting (4.173) and (4.178) into (4.167) gives

$$
\begin{equation*}
\mathrm{CMRR} \simeq \frac{1+2 g_{m(d p)} r_{\text {tail }}}{\left(\frac{1}{1+g_{m(m i r)} r_{o(d p)}}+\frac{1}{1+\frac{g_{m(m i r)} r_{\pi(m i r)}}{2}}\right)} \tag{4.180}
\end{equation*}
$$

If $\left(g_{m(m i r)} r_{o(d p)}\right) \gg 1$ and $\left(g_{m(m i r)} r_{\pi(m i r)} / 2\right) \gg 1,(4.180)$ can be simplified to give

$$
\begin{align*}
\mathrm{CMRR} & \simeq\left(1+2 g_{m(d p)} r_{\mathrm{tail}}\right) g_{m(\text { mir })}\left(r_{o(d p)} \| \frac{r_{\pi(\text { mir })}}{2}\right) \\
& \simeq\left(2 g_{m(d p)} r_{\mathrm{tail}}\right) g_{m(\text { mir })}\left(r_{o(d p)} \| \frac{r_{\pi(m i r)}}{2}\right) \tag{4.181}
\end{align*}
$$

Comparing (4.181) and (4.156) shows that the active load increases the common-mode rejection ratio by a factor of about $2 g_{m(\text { mir })}\left(r_{o(d p)} \|\left(r_{\pi(\text { mir })} / 2\right)\right)$ for the bipolar circuit in Fig. $4.29 b$ compared to its passive-load counterpart in Fig. 4.29a.

On the other hand, for the MOS circuit in Fig. 4.29b, substituting (4.173) and (4.179) into (4.167) gives

$$
\begin{equation*}
\mathrm{CMRR} \simeq \frac{1+2 g_{m(d p)} r_{\mathrm{tail}}}{\left(\frac{1}{1+g_{m(\operatorname{mir})} r_{o(d p)}}+\frac{1}{1+g_{m(\operatorname{mir})} r_{o(\mathrm{mir})}}\right)} \tag{4.182}
\end{equation*}
$$

If $\left(g_{m(m i r)} r_{o(d p)}\right) \gg 1$ and $\left(g_{m(m i r)} r_{o(m i r)}\right) \gg 1$, (4.182) can be simplified to give

$$
\begin{align*}
\mathrm{CMRR} & \simeq\left(1+2 g_{m(d p)} r_{\mathrm{tail}}\right) g_{m(m i r)}\left(r_{o(d p)} \| r_{o(\text { mir })}\right) \\
& \simeq\left(2 g_{m(d p)} r_{\mathrm{tail}}\right) g_{m(\text { mir })}\left(r_{o(d p)} \| r_{o(\text { mir })}\right) \tag{4.183}
\end{align*}
$$

Comparing (4.183) and (4.156) shows that the active load increases the common-mode rejection ratio by a factor of about $2 g_{m(m i r)}\left(r_{o(d p)} \| r_{o(m i r)}\right)$ for the MOS circuit in Fig. $4.29 b$ compared to its passive-load counterpart in Fig. 4.29a.

For these calculations, perfect matching was assumed so that $g_{m 1}=g_{m 2}, g_{m 3}=g_{m 4}$, $r_{o 1}=r_{o 2}$, and $r_{o 3}=r_{o 4}$. In practice, however, nonzero mismatch occurs. With mismatch in a MOS differential pair using a current-mirror load, the differential-mode transconductance is

$$
\begin{equation*}
G_{m}[d m] \simeq g_{m 1-2}\left[\frac{1-\left(\frac{\Delta g_{m 1-2}}{2 g_{m 1-2}}\right)^{2}}{1+\left(\frac{\Delta g_{m 3-4}}{2 g_{m 3-4}}\right)}\right] \tag{4.184}
\end{equation*}
$$

where $\Delta g_{m 1-2}=g_{m 1}-g_{m 2}, g_{m 1-2}=\left(g_{m 1}+g_{m 2}\right) / 2, \Delta g_{m 3-4}=g_{m 3}-g_{m 4}$, and $g_{m 3-4}=$ $\left(g_{m 3}+g_{m 4}\right) / 2$. See Problem 4.18. The approximation in (4.184) is valid to the extent that $g_{m} r_{o} \gg 1$ for each transistor and $\left(g_{m 1}+g_{m 2}\right) r_{\text {tail }} \gg 1$ for the tail current source. Equation 4.184 shows that the mismatch between $g_{m 1}$ and $g_{m 2}$ has only a minor effect on $G_{m}[d m]$. This result stems from the fact that the small-signal voltage across the tail current source, $v_{\text {tail }}$, is zero with a purely differential input only when $g_{m 1}=g_{m 2}$, assuming $r_{o 1} \rightarrow \infty$ and $r_{o 2} \rightarrow \infty$. For example, increasing $g_{m 1}$ compared to $g_{m 2}$ tends to increase the small-signal drain current $i_{1}$ if $v_{g s 1}$ is constant. However, this change also increases $v_{\text {tail }}$, which reduces $v_{g s 1}$ for a fixed $v_{i d}$. The combination of these two effects causes $i_{1}$ to be insensitive to $g_{m 1}-g_{m 2}$. On the other hand, mismatch between $g_{m 3}$ and $g_{m 4}$ directly modifies the contribution of $i_{1}$ through the current mirror to the output current. Therefore, (4.184) shows that $G_{m}[d m]$ is most sensitive to the mismatch between $g_{m 3}$ and $g_{m 4}$.

With mismatch in a MOS differential pair using a current-mirror load, the common-mode transconductance is

$$
\begin{equation*}
G_{m}[\mathrm{~cm}] \simeq-\frac{1}{2 r_{\text {tail }}}\left(\epsilon_{d}+\epsilon_{m}\right) \tag{4.185}
\end{equation*}
$$

where $\epsilon_{d}$ is the gain error in the source-coupled pair with a pure common-mode input defined in (4.161) and $\epsilon_{m}$ is the gain error in the current mirror defined in (4.133). From Problem 4.19,

$$
\begin{equation*}
\epsilon_{d} \simeq \frac{1}{g_{m 3} r_{o(d p)}}-\frac{\Delta g_{m 1-2}}{g_{m 1-2}}\left(1+\frac{2 r_{\text {tail }}}{r_{o(d p)}}\right)-\frac{2 r_{\text {tail }}}{r_{o(d p)}} \frac{\Delta r_{o(d p)}}{r_{o(d p)}} \tag{4.186}
\end{equation*}
$$

Each term in (4.186) corresponds to one source of gain error by itself, and interactions between terms are ignored. The first term in (4.186) is consistent with (4.173) when $g_{m 3} r_{o(d p)} \gg 1$ and stems from the observation that the drain of $T_{1}$ is not connected to a small-signal ground during the calculation of $G_{m}[d m]$, unlike the drain of $T_{2}$. The second term in (4.186) stems from mismatch between $g_{m 1}$ and $g_{m 2}$ alone. The third term in (4.186) stems from the mismatch between $r_{o 1}$ and $r_{o 2}$ alone. The contribution of this mismatch to $G_{m}[\mathrm{~cm}]$ is significant because the action of the current mirror nearly cancels the contributions of the input $g_{m}$ generators to $G_{m}[\mathrm{~cm}]$ under ideal conditions, causing $G_{m}[\mathrm{~cm}] \simeq 0$ in (4.166). In contrast, $G_{m}[\mathrm{dm}]$ is insensitive to the mismatch between $r_{o 1}$ and $r_{o 2}$ because the dominant contributions to $G_{m}[\mathrm{dm}]$ arising from the input $g_{m}$ generators do not cancel at the output. From Problem 4.19,

$$
\begin{equation*}
\epsilon_{m}=\frac{1}{1+g_{m 3} r_{o 3}}+\frac{\left(g_{m 3}-g_{m 4}\right) r_{o 3}}{1+g_{m 3} r_{o 3}} \simeq \frac{1}{g_{m 3} r_{o 3}}+\frac{\Delta g_{m 3-4}}{g_{m 3-4}} \tag{4.187}
\end{equation*}
$$

Each term in (4.187) corresponds to one source of gain error by itself, and interactions between terms are ignored. The first term in (4.187), which is consistent with (4.179) when $g_{m 3} r_{o 3} \gg 1$, stems from the observation that the small-signal input resistance of the current mirror is not exactly $1 / g_{m 3}$ but $\left(1 / g_{m 3}\right) \| r_{o 3}$. The second term in (4.187) stems from mismatch between $g_{m 3}$ and $g_{m 4}$ alone. The CMRR with mismatch is the ratio of $G_{m}[\mathrm{dm}]$ in (4.184) to $G_{m}[\mathrm{~cm}]$ in (4.185), using (4.186) and (4.187) for $\epsilon_{d}$ and $\epsilon_{m}$, respectively. Since the common-mode transconductance is very small without mismatch (as a result of the behavior of the currentmirror load), mismatch usually reduces the CMRR by increasing $\left|G_{m}[\mathrm{~cm}]\right|$.

## 4.4 Voltage and Current References

### 4.4.1 Low-Current Biasing

#### 4.4.1.1 Bipolar Widlar Current Source

In ideal operational amplifiers, the current is zero in each of the two input leads. However, the input current is not zero in real op amps with bipolar input transistors because $\beta_{F}$ is finite. Since the op-amp inputs are usually connected to a differential pair, the tail current must usually be very small in such op amps to keep the input current small. Typically, the tail current is on the order of $5 \mu \mathrm{~A}$. Bias currents of this magnitude are also required in a variety of other applications, especially where minimizing power dissipation is important. The simple current mirrors shown in Fig. 4.30 are usually not optimum for such small currents. For example, using a simple bipolar current mirror as in Fig. $4.30 a$ and assuming a maximum practical emitter area ratio between transistors of ten to one, the mirror would need an input current of $50 \mu \mathrm{~A}$ for an output current of $5 \mu \mathrm{~A}$. If the power-supply voltage in Fig. $4.30 a$ is 5 V , and if $V_{B E(\mathrm{on})}=0.7 \mathrm{~V}, R=86 \mathrm{k} \Omega$ would be required. Resistors of this magnitude are costly in terms of die area. Currents of such low magnitude can be obtained with moderate values of resistance, however, by modifying the simple current mirror so that the transistors operate with unequal base-emitter voltages. In the Widlar current source of Fig. 4.31a, resistor $R_{2}$ is inserted in series with the emitter of $Q_{2}$, and transistors $Q_{1}$ and $Q_{2}$ operate with unequal base emitter voltages if $R_{2} \neq 0 .{ }^{10,11}$ This circuit is referred to as a current source rather than a current mirror because the output current in Fig. $4.31 a$ is much less dependent on the input
image_name:Figure 4.30 (a)
description:
[
name: Q1, type: NPN, ports: {C: b1b2c1, B: b1b2c1, E: GND}
name: Q2, type: NPN, ports: {C: LOAD, B: b1b2c1, E: GND}
name: R, type: Resistor, value: R, ports: {N1: VCC, N2: b1b2c1}
]
extrainfo:The circuit is a simple two-transistor current mirror using bipolar transistors. It mirrors the input current IIN to the output IOUT, with the input current set by the supply voltage VCC and a resistor R.
image_name:Figure 4.30 (b)
description:
[
name: R, type: Resistor, value: R, ports: {N1: VDD, N2: g1g2d1}
name: M1, type: NMOS, ports: {S: GND, D: g1g2d1, G: g1g2d1}
name: M2, type: NMOS, ports: {S: GND, D: LOAD, G: g1g2d1}
]
extrainfo:This is a simple two-transistor current mirror using MOS transistors. The input current is set by the supply voltage VDD and a resistor R. The circuit provides an output current IOUT at the LOAD.

Figure 4.30 Simple two-transistor current mirrors where the input current is set by the supply voltage and a resistor using (a) bipolar and (b) MOS transistors.
image_name:Figure 4.30 (a)
description:
[
name: Q1, type: NPN, ports: {C: b1b2c1, B: b1b2c, E: GND}
name: Q2, type: NPN, ports: {C: IOUT, B: b1b2c, E: e2}
name: R1, type: Resistor, value: R1, ports: {N1: VCC, N2: b1b2c1}
name: R2, type: Resistor, value: R2, ports: {N1: e2, N2: GND}
name: R, type: Resistor, value: R, ports: {N1: VCC, N2: b1b2c1}
name: M1, type: NMOS, ports: {S: GND, D: g1g2d1, G: g1g2d1}
name: M2, type: NMOS, ports: {S: GND, D: LOAD, G: g1g2d1}
]
extrainfo:This is a simple two-transistor current mirror using MOS transistors. The input current is set by the supply voltage VDD and a resistor R. The circuit provides an output current IOUT at the LOAD.
image_name:Figure 4.30 (b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: g1g2d1, G: g1g2d1}
name: M2, type: NMOS, ports: {S: GND, D: LOAD, G: g1g2d1}
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: g1g2d1}
name: R2, type: Resistor, value: R2, ports: {N1: LOAD, N2: GND}
]
extrainfo:This is a simple two-transistor current mirror using MOS transistors. The input current is set by the supply voltage VDD and a resistor R1. The circuit provides an output current IOUT at the LOAD. The transistors M1 and M2 are NMOS transistors, with M1 configured to mirror the current through M2.

Figure 4.31 Widlar current sources: (a) bipolar and (b) MOS.
current and the power-supply voltage than in the simple current mirror of Fig. 4.30a, as shown in Section 4.4.2. We will now calculate the output current of the Widlar current source.

If $I_{\text {IN }}>0, Q_{1}$ operates in the forward-active region because it is diode connected. Assume that $Q_{2}$ also operates in the forward active region. KVL around the base-emitter loop gives

$$
\begin{equation*}
V_{B E 1}-V_{B E 2}-\frac{\beta_{F}+1}{\beta_{F}} I_{\mathrm{OUT}} R_{2}=0 \tag{4.188}
\end{equation*}
$$

If we assume that $V_{B E 1}=V_{B E 2}=V_{B E(\text { on })}=0.7 \mathrm{~V}$ in (4.188), we would predict that $I_{\text {OUT }}=0$. Although $I_{\mathrm{OUT}}$ is small in practice, it is greater than zero under the usual bias conditions, which means that the standard assumption about $V_{B E(\text { on })}$ is invalid here. In contrast, the standard assumption is usually valid in calculating $I_{\mathrm{IN}}$ because small variations in $V_{B E 1}$ have little effect on $I_{\mathrm{IN}}$ if $V_{C C} \gg V_{B E 1}$. When one base-emitter voltage is subtracted from another, however, small differences between them are important. If $V_{A} \rightarrow \infty,(4.188)$ can be rewritten
using (1.35) as

$$
\begin{equation*}
V_{T} \ln \frac{I_{C 1}}{I_{S 1}}-V_{T} \ln \frac{I_{\mathrm{OUT}}}{I_{S 2}}-\frac{\beta_{F}+1}{\beta_{F}} I_{\mathrm{OUT}} R_{2}=0 \tag{4.189}
\end{equation*}
$$

If $\beta_{F} \rightarrow \infty$, (4.189) simplifies to

$$
\begin{equation*}
V_{T} \ln \frac{I_{\mathrm{IN}}}{I_{S 1}}-V_{T} \ln \frac{I_{\mathrm{OUT}}}{I_{S 2}}-I_{\mathrm{OUT}} R_{2}=0 \tag{4.190}
\end{equation*}
$$

For identical transistors, $I_{S 1}$ and $I_{S 2}$ are equal, and (4.190) becomes

$$
\begin{equation*}
V_{T} \ln \frac{I_{\mathrm{IN}}}{I_{\mathrm{OUT}}}=I_{\mathrm{OUT}} R_{2} \tag{4.191}
\end{equation*}
$$

This transcendental equation can be solved by trial and error to find $I_{\text {OUT }}$ if $R_{2}$ and $I_{\mathrm{IN}}$ are known, as in typical analysis problems. Because the logarithm function compresses changes in its argument, attention can be focused on the linear term in (4.191), simplifying convergence of the trial-and-error process. In design problems, however, the desired $I_{\text {IN }}$ and $I_{\text {OUT }}$ are usually known, and (4.191) provides the required value of $R_{2}$.

#### EXAMPLE

In the circuit of Fig. 4.31a, determine the proper value of $R_{2}$ to give $I_{\mathrm{OUT}}=5 \mu \mathrm{~A}$. Assume that $V_{C C}=5 \mathrm{~V}, R_{1}=4.3 \mathrm{k} \Omega, V_{B E(\text { on })}=0.7 \mathrm{~V}$, and $\beta_{F} \rightarrow \infty$.

$$
\begin{gathered}
I_{\mathrm{IN}}=\frac{5 \mathrm{~V}-0.7 \mathrm{~V}}{4.3 \mathrm{k} \Omega}=1 \mathrm{~mA} \\
V_{T} \ln \frac{I_{\mathrm{IN}}}{I_{\mathrm{OUT}}}=26 \mathrm{mV} \ln \left(\frac{1 \mathrm{~mA}}{5 \mu \mathrm{~A}}\right)=137 \mathrm{mV}
\end{gathered}
$$

Thus from (4.191)

$$
I_{\text {OUT }} R_{2}=137 \mathrm{mV}
$$

and

$$
R_{2}=\frac{137 \mathrm{mV}}{5 \mu \mathrm{~A}}=27.4 \mathrm{k} \Omega
$$

- The total resistance in the circuit is $31.7 \mathrm{k} \Omega$.

#### EXAMPLE

In the circuit of Fig. $4.31 a$, assume that $I_{\mathrm{IN}}=1 \mathrm{~mA}, R_{2}=5 \mathrm{k} \Omega$, and $\beta_{F} \rightarrow \infty$. Find $I_{\mathrm{OUt}}$. From (4.191),

$$
V_{T} \ln \frac{1 \mathrm{~mA}}{I_{\mathrm{OUT}}}-5 \mathrm{k} \Omega\left(I_{\mathrm{OUT}}\right)=0
$$

Try

$$
\begin{gathered}
I_{\text {OUT }}=15 \mu \mathrm{~A} \\
108 \mathrm{mV}-75 \mathrm{mV} \neq 0
\end{gathered}
$$

The linear term $I_{\text {OUT }} R_{2}$ is too small; therefore, $I_{\text {OUT }}>15 \mu \mathrm{~A}$ should be tried. Try

$$
\begin{gathered}
I_{\text {OUT }}=20 \mu \mathrm{~A} \\
101.7 \mathrm{mV}-100 \mathrm{mV} \simeq 0
\end{gathered}
$$

Therefore, the output current is close to $20 \mu \mathrm{~A}$. Notice that while the linear term increased by 25 mV from the first to the second trial, the logarithm term decreased by only about 6 mV because the logarithm function compresses changes in its argument.

### 4.4.1.2 MOS Widlar Current Source

The Widlar configuration can also be used in MOS technology, as shown in Fig. 4.31b.
If $I_{\mathrm{IN}}>0, M_{1}$ operates in the active region because it is diode connected. Assume that $M_{2}$ also operates in the forward active region. KVL around the gate-source loop gives

$$
\begin{equation*}
V_{G S 1}-V_{G S 2}-I_{\text {OUT }} R_{2}=0 \tag{4.192}
\end{equation*}
$$

If we ignore the body effect, the threshold components of the gate-source voltages cancel and (4.192) simplifies to

$$
\begin{equation*}
I_{\text {OUT }} R_{2}+V_{o v 2}-V_{o v 1}=0 \tag{4.193}
\end{equation*}
$$

If the transistors operate in strong inversion and $V_{A} \rightarrow \infty$,

$$
\begin{equation*}
I_{\mathrm{OUT}} R_{2}+\sqrt{\frac{2 I_{\mathrm{OUT}}}{k^{\prime}(W / L)_{2}}}-V_{o v 1}=0 \tag{4.194}
\end{equation*}
$$

This quadratic equation can be solved for $\sqrt{I_{\text {OUT }}}$.

$$
\begin{equation*}
\sqrt{I_{\mathrm{OUT}}}=\frac{-\sqrt{\frac{2}{k^{\prime}(W / L)_{2}}} \pm \sqrt{\frac{2}{k^{\prime}(W / L)_{2}}+4 R_{2} V_{o v 1}}}{2 R_{2}} \tag{4.195}
\end{equation*}
$$

where $V_{o v 1}=\sqrt{2 I_{\mathrm{IN}} /\left[k^{\prime}(W / L)_{1}\right]}$. From (1.157),

$$
\begin{equation*}
\sqrt{I_{\mathrm{OUT}}}=\sqrt{\frac{k^{\prime}(W / L)_{2}}{2}}\left(V_{G S 2}-V_{t}\right) \tag{4.196}
\end{equation*}
$$

Equation 4.196 applies only when $M_{2}$ operates in the active region, which means that $V_{G S 2}>V_{t}$. As a result, $\sqrt{I_{\text {OUT }}}>0$ and the potential solution where the second term in the numerator of (4.195) is subtracted from the first, cannot occur in practice. Therefore,

$$
\begin{equation*}
\sqrt{I_{\mathrm{OUT}}}=\frac{-\sqrt{\frac{2}{k^{\prime}(W / L)_{2}}}+\sqrt{\frac{2}{k^{\prime}(W / L)_{2}}+4 R_{2} V_{o v 1}}}{2 R_{2}} \tag{4.197}
\end{equation*}
$$

Equation 4.197 shows that a closed-form solution for the output current can be written for a Widlar current source that uses MOS transistors operating in strong inversion, unlike the bipolar case where trial and error is required to find $I_{\text {OUT }}$.

#### EXAMPLE

In Fig. 4.31b, find $I_{\text {OUT }}$ if $I_{\text {IN }}=100 \mu \mathrm{~A}, R_{2}=4 \mathrm{k} \Omega, k^{\prime}=200 \mu \mathrm{~A} / \mathrm{V}^{2}$, and $(W / L)_{1}=$ $(W / L)_{2}=25$. Assume the temperature is $27^{\circ} \mathrm{C}$ and that $n=1.5$ in (1.247).
Then $R_{2}=0.004 \mathrm{M} \Omega, V_{o v 1}=\sqrt{200 /(200 \times 25)} \mathrm{V}=0.2 \mathrm{~V}$,

$$
\sqrt{I_{\text {OUT }}}=\frac{-\sqrt{\frac{2}{200(25)}}+\sqrt{\frac{2}{200(25)}+4(0.004)(0.2)}}{2(0.004)} \sqrt{\mu \mathrm{A}}=5 \sqrt{\mu \mathrm{~A}}
$$

and $I_{\text {OUT }}=25 \mu \mathrm{~A}$. Also,

$$
V_{o v 2}=V_{o v 1}-I_{\text {OUT }} R_{2}=0.2-25 \times 0.004=0.1 \mathrm{~V}>2 n V_{T} \simeq 78 \mathrm{mV}
$$

- Therefore, both transistors operate in strong inversion, as assumed.

#### 4.4.1.3 Bipolar Peaking Current Source

The Widlar source described in Section 4.4.1.1 allows currents in the microamp range to be realized with moderate values of resistance. Biasing integrated-circuit stages with currents on the order of nanoamps is often desirable. To reach such low currents with moderate values of resistance, the circuit shown in Fig. 4.32 can be used. ${ }^{12,13,14}$ Neglecting base currents, we have

$$
\begin{equation*}
V_{B E 1}-I_{\mathrm{IN}} R=V_{B E 2} \tag{4.198}
\end{equation*}
$$

If $V_{A} \rightarrow \infty$, (4.198) can be rewritten using (1.35) as

$$
\begin{equation*}
V_{T} \ln \frac{I_{\mathrm{IN}}}{I_{S 1}}-V_{T} \ln \frac{I_{\mathrm{OUT}}}{I_{S 2}}=I_{\mathrm{IN}} R \tag{4.199}
\end{equation*}
$$

If $Q_{1}$ and $Q_{2}$ are identical, (4.199) can be rewritten as

$$
\begin{equation*}
I_{\mathrm{OUT}}=I_{\mathrm{IN}} \exp \left(-\frac{I_{\mathrm{IN}} R}{V_{T}}\right) \tag{4.200}
\end{equation*}
$$

Equation 4.200 is useful for analysis of a given circuit. For design with identical $Q_{1}$ and $Q_{2}$, (4.199) can be rewritten as

$$
\begin{equation*}
R=\frac{V_{T}}{I_{\mathrm{IN}}} \ln \frac{I_{\mathrm{IN}}}{I_{\mathrm{OUT}}} \tag{4.201}
\end{equation*}
$$

For example, for $I_{\mathrm{IN}}=10 \mu \mathrm{~A}$ and $I_{\mathrm{OUT}}=100 \mathrm{nA},(4.201)$ can be used to show that $R \simeq$ $12 \mathrm{k} \Omega$.

A plot of $I_{\text {OUt }}$ versus $I_{\mathrm{IN}}$ from (4.200) is shown in Fig. 4.33. When the input current is small, the voltage drop on the resistor is small, and $V_{B E 2} \simeq V_{B E 1}$ so $I_{\mathrm{OUT}} \simeq I_{\mathrm{IN}}$. As the input current increases, $V_{B E 1}$ increases in proportion to the logarithm of the input current while the drop on the resistor increases linearly with the input current. As a result, increases in the input current eventually cause the base-emitter voltage of $Q_{2}$ to decrease. The output current
image_name:Figure 4.32 Bipolar peaking current source
description:
[
name: I_IN, type: CurrentSource, value: I_IN, ports: {Np: VCC, Nn: b1}
name: R, type: Resistor, value: R, ports: {N1: b1, N2: Cib2}
name: Q1, type: NPN, ports: {C: b1, B: Cib2, E: GND}
name: Q2, type: NPN, ports: {C: LOAD, B: Cib2, E: GND}
]
extrainfo:The circuit is a bipolar peaking current source. The input current I_IN flows through the resistor R and affects the base-emitter voltage of Q1 and Q2, influencing the output current I_OUT. The output current peaks based on the resistor value R.

Figure 4.32 Bipolar peaking current source.
image_name:Figure 4.33 Transfer characteristics of the bipolar peaking current source
description:The graph titled "Figure 4.33 Transfer characteristics of the bipolar peaking current source" illustrates the relationship between the input current (I_IN) and the output current (I_OUT) of a bipolar peaking current source at a temperature of 27°C.

1. **Type of Graph and Function:**
- The graph is a 2D plot showing the transfer characteristics of the current source.

2. **Axes Labels and Units:**
- The x-axis represents the input current (I_IN) in microamperes (µA), ranging from 0 to 10 µA.
- The y-axis represents the output current (I_OUT) in nanoamperes (nA), ranging from 0 to 1000 nA.
- Both axes use a linear scale.

3. **Overall Behavior and Trends:**
- The graph shows a peaking behavior where the output current (I_OUT) increases with the input current (I_IN) up to a certain point and then decreases. This peak indicates the maximum output current achievable for a given input.

4. **Key Features and Technical Details:**
- Three curves are plotted, each corresponding to different resistor values (R = 10 kΩ, 12 kΩ, and 14 kΩ).
- As the resistor value increases, the peak of the output current decreases and shifts to the right (higher I_IN values).
- The peak output current is highest for R = 10 kΩ and lowest for R = 14 kΩ.

5. **Annotations and Specific Data Points:**
- The peaks of the curves are annotated, showing the dependency of the peak location and magnitude on the resistor value R.
- The graph provides a visual understanding of how changes in resistance affect the peaking behavior of the current source.

Figure 4.33 Transfer characteristics of the bipolar peaking current source with $T=27^{\circ} \mathrm{C}$.
reaches a maximum when $V_{B E 2}$ is maximum. The name peaking current source stems from this behavior, and the location and magnitude of the peak both depend on $R$.

#### 4.4.1.4 MOS Peaking Current Source

The peaking-current configuration can also be used in MOS technology, as shown in Fig. 4.34. If $I_{\mathrm{IN}}$ is small and positive, the voltage drop on $R$ is small and $M_{1}$ operates in the active region. Assume that $M_{2}$ also operates in the active region. KVL around the gate-source loop gives

$$
\begin{equation*}
V_{G S 1}-I_{\mathrm{IN}} R-V_{G S 2}=0 \tag{4.202}
\end{equation*}
$$

Since the sources of $M_{1}$ and $M_{2}$ are connected together, the thresholds cancel and (4.202) simplifies to

$$
\begin{equation*}
V_{o v 2}=V_{o v 1}-I_{\mathrm{IN}} R \tag{4.203}
\end{equation*}
$$

From (1.157),

$$
\begin{equation*}
I_{\text {OUT }}=\frac{k^{\prime}(W / L)_{2}}{2}\left(V_{o v 2}\right)^{2}=\frac{k^{\prime}(W / L)_{2}}{2}\left(V_{o v 1}-I_{\mathrm{IN}} R\right)^{2} \tag{4.204}
\end{equation*}
$$

image_name:Figure 4.34 MOS peaking current source
description:
[
name: IIN, type: CurrentSource, value: IIN, ports: {Np: VDD, Nn: X}
name: R, type: Resistor, value: R, ports: {N1: X, N2: d1g2}
name: M1, type: NMOS, ports: {S: GND, D: d1g2, G: X}
name: M2, type: NMOS, ports: {S: GND, D: LOAD, G: d1g2}
]
extrainfo:The circuit is a MOS peaking current source with two NMOS transistors M1 and M2. The input current IIN flows from VDD to node X, passes through resistor R and NMOS M1, and then controls NMOS M2 to drive the load with output current IOUT.

Figure 4.34 MOS peaking current source.
image_name:Figure 4.35
description:The graph in Figure 4.35 is a plot showing the transfer characteristics of a MOS peaking current source. It specifically illustrates the relationship between input current \( I_{IN} \) and output current \( I_{OUT} \) for the circuit described.

**Type of Graph and Function:**
This is a two-dimensional plot showing the transfer characteristics of a MOS peaking current source. The graph depicts how the output current \( I_{OUT} \) varies with changes in the input current \( I_{IN} \).

**Axes Labels and Units:**
- The x-axis represents the input current \( I_{IN} \) in microamperes (\( \mu A \)), with a scale ranging from 0 to 10 \( \mu A \).
- The y-axis represents the output current \( I_{OUT} \) in nanoamperes (nA), with a scale ranging from 0 to 1500 nA.

**Overall Behavior and Trends:**
- The graph shows two distinct regions labeled as 'Strong inversion' and 'Weak inversion'.
- In the strong inversion region (\( I_{IN} < 1 \mu A \)), the output current \( I_{OUT} \) initially rises sharply, reaching a small peak before decreasing slightly.
- In the weak inversion region (\( I_{IN} > 1 \mu A \)), the output current \( I_{OUT} \) increases more significantly, reaching a maximum peak at around \( I_{IN} = 3 \mu A \) and \( I_{OUT} \approx 1250 \) nA, before gradually decreasing as \( I_{IN} \) continues to increase.

**Key Features and Technical Details:**
- The peak output current occurs at approximately \( I_{IN} = 3 \mu A \), where \( I_{OUT} \) reaches about 1250 nA.
- The graph indicates a transition from strong inversion to weak inversion, highlighting the change in behavior of the MOS transistors as the input current increases.

**Annotations and Specific Data Points:**
- The graph includes annotations with parameters such as \( n = 1.5 \), \( T = 27^\circ C \), \( R = 10 \text{k}\Omega \), \( k' = 200 \mu A/V^2 \), and both transistors having a width-to-length ratio \((W/L)_2 = (W/L)_1 = 25\). These parameters are crucial for understanding the specific conditions under which the graph was plotted.

This detailed description provides a comprehensive understanding of the transfer characteristics of the MOS peaking current source as depicted in Figure 4.35.

Figure 4.35 Transfer characteristics of the MOS peaking current source assuming both transistors operate in weak inversion or in strong inversion.
where $V_{o v 1}=\sqrt{2 I_{\text {IN }} /\left[k^{\prime}(W / L)_{1}\right]}$. Equation 4.204 assumes that the transistors operate in strong inversion. In practice, the input current is usually small enough that the overdrive of $M_{1}$ is less than $2 n V_{T}$, where $n$ is defined in (1.247) and $V_{T}$ is a thermal voltage. Equation 4.203 shows that the overdrive of $M_{2}$ is even smaller than that of $M_{1}$. Therefore, both transistors usually operate in weak inversion, where the drain current is an exponential function of the gatesource voltage as shown in (1.252). If $V_{D S 1}>3 V_{T}$, applying (1.252) to $M_{1}$ and substituting into (4.202) gives

$$
\begin{equation*}
V_{G S 2}-V_{t} \simeq n V_{T} \ln \left(\frac{I_{\mathrm{IN}}}{(W / L)_{1} I_{t}}\right)-I_{\mathrm{IN}} R \tag{4.205}
\end{equation*}
$$

Then if the transistors are identical and $V_{D S 2}>3 V_{T}$, substituting (4.205) into (1.252) gives

$$
\begin{equation*}
I_{\mathrm{OUT}} \simeq \frac{W}{L} I_{t} \exp \left(\frac{V_{G S 2}-V_{t}}{n V_{T}}\right) \simeq I_{\mathrm{IN}} \exp \left(-\frac{I_{\mathrm{IN}} R}{n V_{T}}\right) \tag{4.206}
\end{equation*}
$$

where $I_{t}$ is given by (1.251) and represents the drain current of $M_{2}$ with $V_{G S 2}=V_{t}, W / L=1$, and $V_{D S} \gg V_{T}$. Comparing (4.206) with (4.200) shows that the output current in an MOS peaking current source where both transistors operate in weak inversion is the same as in the bipolar case except that $1.3 \leq n \leq 1.5$ in the MOS case and $n=1$ in the bipolar case.

Plots of (4.206) and (4.204) are shown in Fig. 4.35 for $n=1.5, T=27^{\circ} \mathrm{C}, R=10 \mathrm{k} \Omega$, $k^{\prime}=200 \mu \mathrm{~A} / \mathrm{V}^{2}$, and $(W / L)_{2}=(W / L)_{1}=25$. In both cases, when the input current is small, the voltage drop on the resistor is small, and $I_{\mathrm{OUT}} \simeq I_{\mathrm{IN}}$. As the input current increases, $V_{G S 1}$ increases more slowly than the drop on the resistor. As a result, increases in the input current eventually cause the gate-source voltage of $M_{2}$ to decrease. The output current reaches a maximum when $V_{G S 2}$ is maximum. As in the bipolar case, the name peaking current source stems from this behavior, and the location and magnitude of the peak both depend on $R$. Because the overdrives on both transistors are usually very small, the strong-inversion equation (4.204) usually underestimates the output current.

### 4.4.2 Supply-Insensitive Biasing

Consider the simple current mirror of Fig. 4.30a, where the input current source has been replaced by a resistor. Ignoring the effects of finite $\beta_{F}$ and $V_{A}$, (4.5) shows that the output
current is

$$
\begin{equation*}
I_{\mathrm{OUT}} \simeq I_{\mathrm{IN}}=\frac{V_{C C}-V_{B E(\mathrm{on})}}{R} \tag{4.207}
\end{equation*}
$$

If $V_{C C} \gg V_{B E(\text { on })}$, this circuit has the drawback that the output current is proportional to the power-supply voltage. For example, if $V_{B E(\text { on })}=0.7 \mathrm{~V}$, and if this current mirror is used in an operational amplifier that has to function with power-supply voltages ranging from 3 V to 10 V , the bias current would vary over a four-to-one range, and the power dissipation would vary over a thirteen-to-one range.

One measure of this aspect of bias-circuit performance is the fractional change in the bias current that results from a given fractional change in supply voltage. The most useful parameter for describing the variation of the output current with the power-supply voltage is the sensitivity $S$. The sensitivity of any circuit variable $y$ to a parameter $x$ is defined as follows:

$$
\begin{equation*}
S_{x}^{y}=\lim _{\Delta x \rightarrow 0} \frac{\Delta y / y}{\Delta x / x}=\frac{x}{y} \frac{\partial y}{\partial x} \tag{4.208}
\end{equation*}
$$

Applying (4.208) to find the sensitivity of the output current to small variations in the powersupply voltage gives

$$
\begin{equation*}
S_{V_{\text {SUP }}}^{I_{\text {OUT }}}=\frac{V_{\text {SUP }}}{I_{\mathrm{OUT}}} \frac{\partial I_{\mathrm{OUT}}}{\partial V_{\mathrm{SUP}}} \tag{4.209}
\end{equation*}
$$

The supply voltage $V_{\text {SUP }}$ is usually called $V_{C C}$ in bipolar circuits and $V_{D D}$ in MOS circuits. If $V_{C C} \gg V_{B E(\mathrm{on})}$ in Fig. 4.30a, and if $V_{D D} \gg V_{G S 1}$ in Fig. 4.30b,

$$
\begin{equation*}
S_{V_{\text {SUP }}}^{I_{\text {OUT }}} \simeq 1 \tag{4.210}
\end{equation*}
$$

Equation 4.210 shows that the output currents in the simple current mirrors in Fig. 4.30 depend strongly on the power-supply voltages. Therefore, this configuration should not be used when supply insensitivity is important.

#### 4.4.2.1 Widlar Current Sources

For the case of the bipolar Widlar source in Fig. 4.31a, the output current is given implicitly by (4.191). To determine the sensitivity of $I_{\mathrm{Out}}$ to the power-supply voltage, this equation is differentiated with respect to $V_{C C}$ :

$$
\begin{equation*}
V_{T} \frac{\partial}{\partial V_{C C}} \ln \frac{I_{\mathrm{IN}}}{I_{\mathrm{OUT}}}=R_{2} \frac{\partial I_{\mathrm{OUT}}}{\partial V_{C C}} \tag{4.211}
\end{equation*}
$$

Differentiating yields

$$
\begin{equation*}
V_{T}\left(\frac{I_{\mathrm{OUT}}}{I_{\mathrm{IN}}}\right)\left(\frac{1}{I_{\mathrm{OUT}}} \frac{\partial I_{\mathrm{IN}}}{\partial V_{C C}}-\frac{I_{\mathrm{IN}}}{I_{\mathrm{OUT}}^{2}} \frac{\partial I_{\mathrm{OUT}}}{\partial V_{C C}}\right)=R_{2} \frac{\partial I_{\mathrm{OUT}}}{\partial V_{C C}} \tag{4.212}
\end{equation*}
$$

Solving this equation for $\partial I_{\text {OUT }} / \partial V_{C C}$, we obtain

$$
\begin{equation*}
\frac{\partial I_{\mathrm{OUT}}}{\partial V_{C C}}=\left(\frac{1}{1+\frac{I_{\mathrm{OUT}} R_{2}}{V_{T}}}\right) \frac{I_{\mathrm{OUT}}}{I_{\mathrm{IN}}} \frac{\partial I_{\mathrm{IN}}}{\partial V_{C C}} \tag{4.213}
\end{equation*}
$$

Substituting (4.213) into (4.209) gives

$$
\begin{equation*}
S_{V_{C C}}^{I_{\mathrm{OUT}}}=\left(\frac{1}{1+\frac{I_{\mathrm{OUT}} R_{2}}{V_{T}}}\right) \frac{V_{C C}}{I_{\mathrm{IN}}} \frac{\partial I_{\mathrm{IN}}}{\partial V_{C C}}=\left(\frac{1}{1+\frac{I_{\mathrm{OUT}} R_{2}}{V_{T}}}\right) S_{V_{C C}}^{I_{\mathrm{IN}}} \tag{4.214}
\end{equation*}
$$

If $V_{C C} \gg V_{B E(\text { on }),} I_{\mathrm{IN}} \simeq V_{C C} / R_{1}$ and the sensitivity of $I_{\mathrm{IN}}$ to $V_{C C}$ is approximately unity, as in the simple current mirror of Fig. 4.30a. For the example in Section 4.4.1.1 where $I_{\text {IN }}=$ 1 mA , $I_{\text {OUT }}=5 \mu \mathrm{~A}$, and $R_{2}=27.4 \mathrm{k} \Omega$, (4.214) gives

$$
\begin{equation*}
S_{V_{C C}}^{I_{\text {OUT }}}=\frac{V_{C C}}{I_{\mathrm{OUT}}} \frac{\partial I_{\mathrm{OUT}}}{\partial V_{C C}} \simeq \frac{1}{1+\frac{137 \mathrm{mV}}{26 \mathrm{mV}}} \simeq 0.16 \tag{4.215}
\end{equation*}
$$

Thus for this case, a 10 percent power-supply voltage change results in only 1.6 percent change in Iout.

For the case of the MOS Widlar source in Fig. 4.31b, the output current is given by (4.197). Differentiating with respect to $V_{D D}$ gives

$$
\begin{equation*}
\frac{1}{2 \sqrt{I_{\mathrm{OUT}}}} \frac{\partial I_{\mathrm{OUT}}}{\partial V_{D D}}=\frac{1}{4 R_{2}} \frac{1}{\sqrt{\frac{2}{k^{\prime}(W / L)_{2}}+4 R_{2} V_{o v 1}}} 4 R_{2} \frac{\partial V_{o v 1}}{\partial V_{D D}} \tag{4.216}
\end{equation*}
$$

where

$$
\begin{equation*}
\frac{\partial V_{o v 1}}{\partial V_{D D}}=\sqrt{\frac{2}{k^{\prime}(W / L)_{1}}} \frac{1}{2 \sqrt{I_{\mathrm{IN}}}} \frac{\partial I_{\mathrm{IN}}}{\partial V_{D D}}=\frac{V_{o v 1}}{2 I_{\mathrm{IN}}} \frac{\partial I_{\mathrm{IN}}}{\partial V_{D D}} \tag{4.217}
\end{equation*}
$$

Substituting (4.216) and (4.217) into (4.209) gives

$$
\begin{equation*}
S_{V_{D D}}^{I_{O U T}}=\frac{V_{o v 1}}{\sqrt{V_{o v 2}^{2}+4 I_{\mathrm{OUT}} R_{2} V_{o v 1}}} S_{V_{D D}}^{I_{\mathrm{IN}}} \tag{4.218}
\end{equation*}
$$

Since $I_{\mathrm{OUT}}$ is usually much less than $I_{\mathrm{IN}}, V_{o v 2}$ is usually small and $I_{\mathrm{OUT}} R_{2} \simeq V_{o v 1}$ and (4.218) simplifies to

$$
\begin{equation*}
S_{V_{D D}}^{I_{\mathrm{OUT}}} \simeq \frac{V_{o v 1}}{\sqrt{4 V_{o v 1}^{2}}} S_{V_{D D}}^{I_{\mathrm{IN}}}=0.5 S_{V_{D D}}^{I_{\mathrm{IN}}} \tag{4.219}
\end{equation*}
$$

If $V_{D D} \gg V_{G S 1}, I_{\mathrm{IN}} \simeq V_{D D} / R_{1}$ and the sensitivity of $I_{\mathrm{IN}}$ to $V_{D D}$ is approximately unity, as in the simple current mirror of Fig. 4.30 b . Thus for this case, a 10 percent power-supply voltage change results in a 5 percent change in $I_{\text {OUT }}$.

#### 4.4.2.2 Current Sources Using Other Voltage Standards

The level of power-supply independence provided by the bipolar and MOS Widlar current sources is not adequate for many types of analog circuits. Much lower sensitivity can be obtained by causing bias currents in the circuit to depend on a voltage standard other than the supply voltage. Bias reference circuits can be classified according to the voltage standard by which the bias currents are established. The most convenient standards are the base-emitter or threshold voltage of a transistor, the thermal voltage, or the breakdown voltage of a reversebiased pn junction (a Zener diode). Each of these standards can be used to reduce supply sensitivity, but the drawback of the first three standards is that the reference voltage is quite temperature dependent. Both the base-emitter and threshold voltages have negative temperature coefficients of magnitude 1 to $2 \mathrm{mV} /{ }^{\circ} \mathrm{C}$, and the thermal voltage has a positive temperature coefficient of $k / q \simeq 86 \mu \mathrm{~V} /{ }^{\circ} \mathrm{C}$. The Zener diode has the disadvantage that at least 7 to 10 V of supply voltage are required because standard integrated-circuit processes produce a minimum breakdown voltage of about 6 V across the most highly doped junctions (usually npn transistor emitter-base junctions). Furthermore, $p n$ junctions produce large amounts of voltage
image_name:(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: VCC, N2: cb2}
name: R2, type: Resistor, value: R2, ports: {N1: b1e2, N2: GND}
name: T1, type: NPN, ports: {C: cb2, B: b1e2, E: GND}
name: T2, type: NPN, ports: {C: LOAD, B: cb2, E: b1e2}
]
extrainfo:Figure 4.36 (a) shows a base-emitter referenced current source using NPN transistors. The current source is designed to provide a stable output current IOUT through the load.
image_name:(b)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: d1g2}
name: R2, type: Resistor, value: R2, ports: {N1: b1e2, N2: GND}
name: T1, type: NPN, ports: {C: GND, B: b1e2, E: d1g2}
name: T2, type: NPN, ports: {C: LOAD, B: d1g2, E: b1e2}
]
extrainfo:The circuit is a threshold referenced current source with two NPN transistors T1 and T2. The input current IIN flows through R1, creating a voltage drop that biases T1 and T2. The output current IOUT is taken from the collector of T2.

Figure 4.36 (a) Base-emitter referenced current source. (b) Threshold referenced current source.
noise under the reverse-breakdown conditions encountered in a bias reference circuit. Noise in avalanche breakdown is considered further in Chapter 11.

We now consider bias reference circuits based on the base-emitter or gate-source voltage. The circuit in simplest form in bipolar technology is shown in Fig. 4.36a. This circuit is similar to a Wilson current mirror where the diode-connected transistor is replaced by a resistor. For the input current to flow in $T_{1}$, transistor $T_{2}$ must supply enough current into $R_{2}$ so that the base-emitter voltage of $T_{1}$ is

$$
\begin{equation*}
V_{B E 1}=V_{T} \ln \frac{I_{\mathrm{IN}}}{I_{S 1}} \tag{4.220}
\end{equation*}
$$

If we neglect base currents, $I_{\mathrm{OUT}}$ is equal to the current flowing through $R_{2}$. Since the voltage drop on $R_{2}$ is $V_{B E 1}$, the output current is proportional to this base-emitter voltage. Thus, neglecting base currents, we have

$$
\begin{equation*}
I_{\mathrm{OUT}}=\frac{V_{B E 1}}{R_{2}}=\frac{V_{T}}{R_{2}} \ln \frac{I_{\mathrm{IN}}}{I_{S 1}} \tag{4.221}
\end{equation*}
$$

Differentiating (4.221) and substituting into (4.209) gives

$$
\begin{equation*}
S_{V_{C C}}^{I_{\mathrm{OUT}}}=\frac{V_{T}}{I_{\mathrm{OUT}} R_{2}} S_{V_{C C}}^{I_{\mathrm{IN}}}=\frac{V_{T}}{V_{B E(\mathrm{on})}} S_{V_{C C}}^{I_{\mathrm{IN}}} \tag{4.222}
\end{equation*}
$$

If $V_{C C} \gg 2 V_{B E(\mathrm{on})}, I_{\mathrm{IN}} \simeq V_{C C} / R_{1}$ and the sensitivity of $I_{\mathrm{IN}}$ to $V_{C C}$ is approximately unity. With $V_{B E(\text { on })}=0.7 \mathrm{~V}$,

$$
\begin{equation*}
S_{V_{C C}}^{I_{\mathrm{OUT}}}=\frac{0.026 \mathrm{~V}}{0.7 \mathrm{~V}} \simeq 0.037 \tag{4.223}
\end{equation*}
$$

Thus for this case, a 10 percent power-supply voltage change results in a 0.37 percent change in $I_{\text {OUT }}$. The result is significantly better than for a bipolar Widlar current source.

The MOS counterpart of the base-emitter reference is shown in Fig. 4.36b. Here

$$
\begin{equation*}
I_{\mathrm{OUT}}=\frac{V_{G S 1}}{R_{2}}=\frac{V_{t}+V_{o v 1}}{R_{2}}=\frac{V_{t}+\sqrt{\frac{2 I_{\mathrm{IN}}}{k^{\prime}(W / L)_{1}}}}{R_{2}} \tag{4.224}
\end{equation*}
$$

The case of primary interest is when the overdrive of $T_{1}$ is small compared to the threshold voltage. This case can be achieved in practice by choosing sufficiently low input current and large $(W / L)_{1}$. In this case, the output current is determined mainly by the threshold voltage and $R_{2}$. Therefore, this circuit is known as a threshold-referenced bias circuit. Differentiating (4.224) with respect to $V_{D D}$ and substituting into (4.209) gives

$$
\begin{equation*}
S_{V_{D D}}^{I_{\text {OUT }}}=\frac{V_{o v 1}}{2 I_{\mathrm{OUT}} R_{2}} S_{V_{D D}}^{I_{\mathrm{IN}}}=\frac{V_{o v 1}}{2 V_{G S 1}} S_{V_{D D}}^{I_{\mathrm{IN}}} \tag{4.225}
\end{equation*}
$$

For example, if $V_{t}=1 \mathrm{~V}, V_{o v 1}=0.1 \mathrm{~V}$, and $S_{V_{D D}}^{I_{\mathrm{IN}}} \simeq 1$

$$
\begin{equation*}
S_{V_{D D}}^{\text {IOUT }} \simeq \frac{0.1}{2(1.1)} \simeq 0.045 \tag{4.226}
\end{equation*}
$$

These circuits are not fully supply independent because the base-emitter or gate-source voltages of $T_{1}$ change slightly with power-supply voltage. This change occurs because the collector or drain current of $T_{1}$ is approximately proportional to the supply voltage. The resulting supply sensitivity is often a problem in bias circuits whose input current is derived from a resistor connected to the supply terminal, since this configuration causes the currents in some portion of the circuit to change with the supply voltage.

#### 4.4.2.3 Self-Biasing

Power-supply sensitivity can be greatly reduced by the use of the so-called bootstrap bias technique, also referred to as self-biasing. Instead of developing the input current by connecting a resistor to the supply, the input current is made to depend directly on the output current of the current source itself. The concept is illustrated in block-diagram form in Fig. 4.37a. Assuming that the feedback loop formed by this connection has a stable operating point, the currents flowing in the circuit are much less sensitive to power-supply voltage than in the resistively biased case. The two key variables here are the input current, $I_{\mathrm{IN}}$, and the output current, $I_{\mathrm{OUT}}$. The relationship between these variables is governed by both the current source and the current
image_name:Figure 4.37a
description:The block diagram, labeled as Figure 4.37a, represents a self-biased reference system consisting of two main components: a current mirror and a current source.

1. **Main Components:**
- **Current Mirror:** This block is responsible for replicating the input current ($I_{\mathrm{IN}}$) to generate a corresponding output current ($I_{\mathrm{OUT}}$). It is connected to a power supply voltage ($V_{\mathrm{SUP}}$) and has two labeled ports: OUT and IN.}
- **Current Source:** This block generates a stable output current ($I_{\mathrm{OUT}}$) from the input current ($I_{\mathrm{IN}}$). It is grounded and also has two labeled ports: IN and OUT.}

2. **Flow of Information or Control:**
- The current mirror receives the input current at its IN port and outputs a mirrored current at its OUT port. The output current ($I_{\mathrm{OUT}}$) from the current mirror is directed to the IN port of the current source.
- The current source, in turn, provides a stable output current at its OUT port, which is fed back to the IN port of the current mirror, creating a feedback loop.

3. **Labels, Annotations, and Key Indicators:**
- The diagram includes labels such as $V_{\mathrm{SUP}}$ for the supply voltage, and $I_{\mathrm{IN}}$ and $I_{\mathrm{OUT}}$ for the input and output currents, respectively.
- The term 'COMMON' is used to denote shared connections or reference points between the components, indicating a common ground or reference plane.

4. **Overall System Function:**
- The primary function of this system is to maintain a stable output current that is less sensitive to variations in power supply voltage. The feedback loop formed by the current mirror and the current source ensures that the output current remains stable over a wide range of input currents. This self-biasing mechanism allows for improved stability and performance compared to resistively biased systems.

(a)
image_name:Figure 4.37b
description:The graph depicted in Figure 4.37b is a plot illustrating the relationship between input current \( I_{\text{IN}} \) on the x-axis and output current \( I_{\text{OUT}} \) on the y-axis. The graph is used to determine the operating point of a self-biased reference circuit involving a current mirror and a current source.

1. **Type of Graph and Function:**
- This is a current vs. current graph, showing the behavior of a self-biased reference circuit.

2. **Axes Labels and Units:**
- The x-axis is labeled \( I_{\text{IN}} \), representing the input current.
- The y-axis is labeled \( I_{\text{OUT}} \), representing the output current.
- Both axes are linear and do not specify units, implying a general qualitative analysis.

3. **Overall Behavior and Trends:**
- The graph features two curves: one represents the current mirror (dashed line) where \( I_{\text{IN}} = I_{\text{OUT}} \), indicating a linear relationship with a slope of 1.
- The other curve represents the current source, which initially rises sharply and then levels off, indicating saturation or stabilization of \( I_{\text{OUT}} \) despite increasing \( I_{\text{IN}} \).

4. **Key Features and Technical Details:**
- The intersection of the two curves marks the desired operating point, labeled as Point A. This point represents the stable operating condition where the circuit functions optimally.
- Another point of intersection, labeled Point B, is identified as an undesired operating point, where the circuit may not perform as intended.

5. **Annotations and Specific Data Points:**
- The graph is annotated with arrows and labels indicating the desired and undesired operating points.
- The desired operating point (Point A) is where the current source curve intersects the \( I_{\text{IN}} = I_{\text{OUT}} \) line at a higher \( I_{\text{OUT}} \), suggesting a stable and efficient operation.
- The undesired operating point (Point B) is where the curves intersect at a lower \( I_{\text{OUT}} \), indicating a less efficient or unstable operation.

This graph effectively illustrates how the self-biasing mechanism stabilizes the output current across a range of input currents, highlighting the significance of choosing the correct operating point for optimal circuit performance.

(b)

Figure 4.37 (a) Block diagram of a self-biased reference. (b) Determination of operating point.
mirror. From the standpoint of the current source, the output current is almost independent of the input current for a wide range of input currents as shown in Fig. 4.37b. From the standpoint of the current mirror, $I_{\mathrm{IN}}$ is set equal to $I_{\text {OUT }}$, assuming that the gain of the current mirror is unity. The operating point of the circuit must satisfy both constraints and hence is at the intersection of the two characteristics. In the plot of Fig. $4.37 b$, two intersections or potential operating points are shown. Point $A$ is the desired operating point, and point $B$ is an undesired operating point because $I_{\mathrm{OUT}}=I_{\mathrm{IN}}=0$.

If the output current in Fig. $4.37 a$ increases for any reason, the current mirror increases the input current by the same amount because the gain of the current mirror is assumed to be unity. As a result, the current source increases the output current by an amount that depends on the gain of the current source. Therefore, the loop responds to an initial change in the output current by further changing the output current in a direction that reinforces the initial change. In other words, the connection of a current source and a current mirror as shown in Fig. 4.37a forms a positive feedback loop, and the gain around the loop is the gain of the current source. In Chapter 9, we will show that circuits with positive feedback are stable if the gain around the loop is less than unity. At point $A$, the gain around the loop is quite small because the output current of the current source is insensitive to changes in the input current around point $A$. On the other hand, at point $B$, the gain around the feedback loop is deliberately made greater than unity so that the two characteristics shown in Fig. $4.37 b$ intersect at a point away from the origin. As a result, this simplified analysis shows that point $B$ is an unstable operating point in principle, and the circuit would ideally tend to drive itself out of this state.

In practice, however, point $B$ is frequently a stable operating point because the currents in the transistors at this point are very small, often in the picoampere range. At such low current levels, leakage currents and other effects reduce the current gain of both bipolar and MOS transistors, usually causing the gain around the loop to be less than unity. As a result, actual circuits of this type are usually unable to drive themselves out of the zero-current state. Thus, unless precautions are taken, the circuit may operate in the zero-current condition. For these reasons, self-biased circuits often have a stable state in which zero current flows in the circuit even when the power-supply voltage is nonzero. This situation is analogous to a gasoline engine that is not running even though it has a full tank of fuel. An electrical or mechanical device is required to start the engine. Similarly, a start-up circuit is usually required to prevent the self-biased circuit from remaining in the zero-current state.

The application of this technique to the $V_{B E}$-referenced current source is illustrated in Fig. 4.38a, and the threshold-referenced MOS counterpart is shown in Fig. 4.38b. We assume for simplicity that $V_{A} \rightarrow \infty$. The circuit composed of $T_{1}, T_{2}$, and $R$ dictates that the current $I_{\text {OUT }}$ depends weakly on $I_{\mathrm{IN}}$, as indicated by (4.221) and (4.224). Second, the current mirror composed of matched transistors $T_{4}$ and $T_{5}$ dictates that $I_{\mathrm{IN}}$ is equal to $I_{\text {OUT }}$. The operating point of the circuit must satisfy both constraints and hence is at the intersection of the two characteristics as in Fig. 4.37b. Except for the effects of finite output resistance of the transistors, the bias currents are independent of supply voltage. If required, the output resistance of the current source and mirror could be increased by the use of cascode or Wilson configurations in the circuits. The actual bias currents for other circuits are supplied by $T_{6}$ and/or $T_{3}$, which are matched to $T_{5}$ and $T_{1}$, respectively.

The zero-current state can be avoided by using a start-up circuit to ensure that some current always flows in the transistors in the reference so that the gain around the feedback loop at point $B$ in Fig. $4.37 b$ does not fall below unity. An additional requirement is that the start-up circuit must not interfere with the normal operation of the reference once the desired operating point is reached. The $V_{B E}$-referenced current source with a typical start-up circuit used in bipolar technologies is illustrated in Fig. 4.39a. We first assume that the circuit is in the undesired zero-current state. If this were true, the base-emitter voltage of $T_{1}$ would be
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: X1, B: b1e2b3, E: GND}
name: Q2, type: NPN, ports: {C: X2, B: X1, E: GND}
name: Q3, type: NPN, ports: {C: LOAD, B: X2, E: GND}
name: M4, type: PMOS, ports: {S: VCC, D: X2, G: X1}
name: M5, type: PMOS, ports: {S: VCC, D: X2, G: X2}
name: M6, type: PMOS, ports: {S: VCC, D: X2, G: X2}
name: R, type: Resistor, value: R, ports: {N1: b1e2b3, N2: GND}
]
extrainfo:The circuit is a self-biasing V_BE reference with a start-up circuit. It uses NPN transistors T1, T2, and T3 for biasing and PMOS transistors T4, T5, and T6 for current mirroring and biasing. The resistor R is used to set the bias voltage.
image_name:(b)
description:
[
name: T1, type: NMOS, ports: {S: GND, D: g1s2g3, G: GND}
name: T2, type: NPN, ports: {C: VDD, B: g1s2g3, E: GND}
name: T3, type: NPN, ports: {C: VDD, B: GND, E: GND}
name: T4, type: PMOS, ports: {S: VDD, D: x, G: x}
name: T5, type: PMOS, ports: {S: VDD, D: x, G: x}
name: T6, type: PMOS, ports: {S: VDD, D: VDD, G: x}
name: R, type: Resistor, value: R, ports: {N1: g1s2g3, N2: GND}
]
extrainfo:The circuit in (b) is a self-biasing reference circuit. It uses a combination of NMOS, NPN, and PMOS transistors to establish a stable reference voltage. The resistors and transistors are configured to maintain current flow and biasing conditions. The circuit ensures that the reference voltage is maintained even with variations in supply voltage or temperature.

Figure 4.38 (a) Self-biasing $V_{B E}$ reference. (b) Self-biasing $V_{t}$ reference.
zero. The base-emitter voltage $T_{2}$ would be tens of millivolts above ground, determined by the leakage currents in the circuit. However, the voltage on the left-hand end of $D_{1}$ is four diode drops above ground, so that a voltage of at least three diode drops would appear across $R_{x}$, and a current would flow through $R_{x}$ into the $T_{1}-T_{2}$ combination. This action would cause current to flow in $T_{4}$ and $T_{5}$, avoiding the zero-current state.

The bias reference circuit then drives itself toward the desired stable state, and we require that the start-up circuit not affect the steady-state current values. This can be accomplished by causing $R_{x}$ to be large enough that when the steady-state current is established in $T_{1}$, the voltage drop across $R_{x}$ is large enough to reverse bias $D_{1}$. In the steady state, the collectoremitter voltage of $T_{1}$ is two diode drops above ground, and the left-hand end of $D_{1}$ is four diode drops above ground. Thus if we make $I_{\mathrm{IN}} R_{x}$ equal to two diode drops, $D_{1}$ will have zero voltage across it in the steady state. As a result, the start-up circuit composed of $R_{s}, D_{2}-D_{5}$, and $D_{1}$ is, in effect, disconnected from the circuit for steady-state operation.

Floating diodes are not usually available in MOS technologies. The threshold-referenced current source with a typical start-up circuit used in MOS technologies is illustrated in Fig. 4.39b. If the circuit is in the undesired zero-current state, the gate-source voltage of $T_{1}$ would be less than a threshold voltage. As a result, $T_{7}$ is off and $T_{8}$ operates in the triode region, pulling the gate-source voltage of $T_{9}$ up to $V_{D D}$. Therefore, $T_{9}$ is on and pulls down on the gates of $T_{4}$ and $T_{5}$. This action causes current to flow in $T_{4}$ and $T_{5}$, avoiding the zerocurrent state.

In steady state, the gate-source voltage of $T_{7}$ rises to $I_{\text {OUT }} R$, which turns on $T_{7}$ and reduces the gate-source voltage of $T_{9}$. In other words, $T_{7}$ and $T_{8}$ form a CMOS inverter whose output falls when the reference circuit turns on. Since the start-up circuit should not interfere with normal operation of the reference in steady state, the inverter output should fall low enough to turn $T_{9}$ off in steady state. Therefore, the gate-source voltage of $T_{9}$ must fall below a threshold voltage when the inverter input rises from zero to $I_{\text {OUT }} R$. In practice,
image_name:(a)
description:
[
name: T1, type: NPN, ports: {C: d1g2d4, B: X2, E: GND}
name: T2, type: NPN, ports: {C: X1, B: X2, E: GND}
name: T3, type: NPN, ports: {C: X1, B: X2, E: GND}
name: T4, type: PNP, ports: {C: X2, B: VDD, E: X1}
name: T5, type: PNP, ports: {C: X1, B: VDD, E: VDD}
name: T6, type: PNP, ports: {C: X1, B: VDD, E: VDD}
name: T7, type: NMOS, ports: {S: GND, D: X1, G: X3}
name: T8, type: PMOS, ports: {S: VDD, D: X3, G: X1}
name: T9, type: NMOS, ports: {S: GND, D: X1, G: X1}
name: RS, type: Resistor, value: RS, ports: {N1: VDD, N2: X3}
name: RX, type: Resistor, value: RX, ports: {N1: X2, N2: GND}
name: R, type: Resistor, value: R, ports: {N1: X2, N2: GND}
name: D1, type: Diode, ports: {Na: k1, Nc: a1}
name: D2, type: Diode, ports: {Na: a3, Nc: k1}
name: D3, type: Diode, ports: {Na: a4, Nc: a3}
name: D4, type: Diode, ports: {Na: a5, Nc: a4}
name: D5, type: Diode, ports: {Na: GND, Nc: a5}
]
extrainfo:The circuit is a self-biasing V_BE reference with a start-up circuit. The configuration involves multiple transistors and diodes to establish a stable reference voltage. The start-up circuit ensures the reference circuit turns on properly without interfering with steady-state operation. The aspect ratio of T7 is crucial to ensure T9 turns off in the steady state.
image_name:(b)
description:
[
name: T1, type: NPN, ports: {C: X2, B: d1g2d4, E: GND}
name: T2, type: NPN, ports: {C: X1, B: X2, E: GND}
name: T3, type: NPN, ports: {C: X1, B: X2, E: GND}
name: T4, type: PNP, ports: {C: X2, B: X1, E: VDD}
name: T5, type: PNP, ports: {C: X1, B: X1, E: VDD}
name: T6, type: PNP, ports: {C: X1, B: X1, E: VDD}
name: T7, type: NMOS, ports: {S: GND, D: X1, G: X1}
name: T8, type: PMOS, ports: {S: VDD, D: X2, G: X1}
name: T9, type: NMOS, ports: {S: GND, D: X1, G: X1}
name: RS, type: Resistor, value: RS, ports: {N1: GND, N2: VDD}
name: RX, type: Resistor, value: RX, ports: {N1: X2, N2: GND}
name: R, type: Resistor, value: R, ports: {N1: X2, N2: GND}
name: D1, type: Diode, ports: {Na: d1g2d4, Nc: X2}
name: D2, type: Diode, ports: {Na: d1g2d4, Nc: GND}
name: D3, type: Diode, ports: {Na: d1g2d4, Nc: GND}
name: D4, type: Diode, ports: {Na: d1g2d4, Nc: GND}
name: D5, type: Diode, ports: {Na: d1g2d4, Nc: GND}
]
extrainfo:The circuit diagram (b) represents a self-biasing Vt reference with a start-up circuit. It includes NPN and PNP transistors, NMOS and PMOS transistors, resistors, and diodes. The start-up circuit ensures the reference circuit turns on and stabilizes in steady state. The aspect ratio of T7 is larger than T8 to control the gate-source voltage of T9, turning it off in steady state. The circuit is designed to minimize temperature dependence of the output current.

Figure 4.39 (a) Self-biasing $V_{B E}$ reference with start-up circuit. (b) Self-biasing $V_{t}$ reference with start-up circuit.
this requirement is satisfied by choosing the aspect ratio of $T_{7}$ to be much larger than that of $T_{8}$.

Another important aspect of the performance of biasing circuits is their dependence on temperature. This variation is most conveniently expressed in terms of the fractional change in output current per degree centigrade of temperature variation, which we call the fractional temperature coefficient $T C_{F}$ :

$$
\begin{equation*}
T C_{F}=\frac{1}{I_{\mathrm{OUT}}} \frac{\partial I_{\mathrm{OUT}}}{\partial T} \tag{4.227}
\end{equation*}
$$

For the $V_{B E}$-referenced circuit of Fig. 4.38a,

$$
\begin{align*}
I_{\mathrm{OUT}} & =\frac{V_{B E 1}}{R}  \tag{4.228}\\
\frac{\partial I_{\mathrm{OUT}}}{\partial T} & =\frac{1}{R} \frac{\partial V_{B E 1}}{\partial T}-\frac{V_{B E 1}}{R^{2}} \frac{\partial R}{\partial T}  \tag{4.229}\\
& =I_{\text {OUT }}\left(\frac{1}{V_{B E 1}} \frac{\partial V_{B E 1}}{\partial T}-\frac{1}{R} \frac{\partial R}{\partial T}\right) \tag{4.230}
\end{align*}
$$

Therefore,

$$
\begin{equation*}
T C_{F}=\frac{1}{I_{\mathrm{OUT}}} \frac{\partial I_{\mathrm{OUT}}}{\partial T}=\frac{1}{V_{B E 1}} \frac{\partial V_{B E 1}}{\partial T}-\frac{1}{R} \frac{\partial R}{\partial T} \tag{4.231}
\end{equation*}
$$

Thus the temperature dependence of the output current is related to the difference between the resistor temperature coefficient and that of the base-emitter junction. Since the former has a positive and the latter a negative coefficient, the net $T C_{F}$ is quite large.

#### EXAMPLE

Design a bias reference as shown in Fig. $4.38 a$ to produce $100 \mu \mathrm{~A}$ output current. Find the $T C_{F}$. Assume that for $T_{1}, I_{S}=10^{-14} \mathrm{~A}$. Assume that $\partial V_{B E} / \partial T=-2 \mathrm{mV} /{ }^{\circ} \mathrm{C}$ and that $(1 / R)(\partial R / \partial T)=+1500 \mathrm{ppm} /{ }^{\circ} \mathrm{C}$.

The current in $T_{1}$ will be equal to $I_{\text {OUT }}$, so that

$$
V_{B E 1}=V_{T} \ln \frac{100 \mu \mathrm{~A}}{10^{-14} \mathrm{~A}}=598 \mathrm{mV}
$$

Thus from (4.228),

$$
R=\frac{598 \mathrm{mV}}{0.1 \mathrm{~mA}}=5.98 \mathrm{k} \Omega
$$

From (4.231),

$$
T C_{F} \simeq \frac{-2 \mathrm{mV} /{ }^{\circ} \mathrm{C}}{598 \mathrm{mV}}-1.5 \times 10^{-3} \simeq-3.3 \times 10^{-3}-1.5 \times 10^{-3}
$$

and thus

$$
T C_{F} \simeq-4.8 \times 10^{-3} /{ }^{\circ} \mathrm{C}=-4800 \mathrm{ppm} /{ }^{\circ} \mathrm{C}
$$

- The term ppm is an abbreviation for parts per million and implies a multiplier of $10^{-6}$.

For the threshold-referenced circuit of Fig. 4.38b,

$$
\begin{equation*}
I_{\text {OUT }}=\frac{V_{G S 1}}{R} \simeq \frac{V_{t}}{R} \tag{4.232}
\end{equation*}
$$

Differentiating (4.232) and substituting into (4.227) gives

$$
\begin{equation*}
T C_{F}=\frac{1}{I_{\mathrm{OUT}}} \frac{\partial I_{\mathrm{OUT}}}{\partial T} \simeq \frac{1}{V_{t}} \frac{\partial V_{t}}{\partial T}-\frac{1}{R} \frac{\partial R}{\partial T} \tag{4.233}
\end{equation*}
$$

Since the threshold voltage of an MOS transistor and the base-emitter voltage of a bipolar transistor both change at about $-2 \mathrm{mV} /{ }^{\circ} \mathrm{C}$, (4.233) and (4.231) show that the temperature dependence of the threshold-referenced current source in Fig. $4.38 b$ is about the same as the $V_{B E}$-referenced current source in Fig. 4.38a.
$V_{B E}$-referenced bias circuits are also used in CMOS technology. An example is shown in Fig. 4.40, where the pnp transistor is the parasitic device inherent in $p$-substrate CMOS
image_name:Figure 4.40
description:
[
name: M4, type: PMOS, ports: {S: VDD, D: X, G: X}
name: M5, type: PMOS, ports: {S: VDD, D: X, G: X}
name: M6, type: PMOS, ports: {S: VDD, D: LOAD, G: X}
name: M2, type: NMOS, ports: {S: GND, D: e1s2, G: Y}
name: M3, type: NMOS, ports: {S: Y, D: X, G: X}
name: Q1, type: PNP, ports: {C: GND, B: GND, E: e1s2}
name: S3, type: Resistor, value: R, ports: {N1: X, N2: GND}
]
extrainfo:The circuit is a V_BE-referenced self-biased circuit in CMOS technology. It uses a feedback loop to maintain a stable current through Q1 and resistor R. The PMOS transistors (M4, M5, M6) are used for current mirroring, while the NMOS transistors (M2, M3) and the PNP transistor (Q1) form the feedback loop. The output current I_OUT is determined by the V_BE of Q1 and the resistance R.

Figure 4.40 Example of a
$V_{B E}$-referenced self-biased circuit in CMOS technology.
technologies. A corresponding circuit utilizing $n p n$ transistors can be used in $n$-substrate CMOS technologies. The feedback circuit formed by $M_{2}, M_{3}, M_{4}$, and $M_{5}$ forces the current in transistor $Q_{1}$ to be the same as in resistor $R$. Assuming matched devices, $V_{G S 2}=V_{G S 3}$ and thus

$$
\begin{equation*}
I_{\mathrm{OUT}}=\frac{V_{B E 1}}{R} \tag{4.234}
\end{equation*}
$$

An alternate source for the voltage reference is the thermal voltage $V_{T}$. The difference in junction potential between two junctions operated at different current densities can be shown to be proportional to $V_{T}$. This voltage difference must be converted to a current to provide the bias current. For the Widlar source shown in Fig. 4.31a, (4.190) shows that the voltage across the resistor $R_{2}$ is

$$
\begin{equation*}
I_{\mathrm{OUT}} R_{2}=V_{T} \ln \frac{I_{\mathrm{IN}}}{I_{\mathrm{OUT}}} \frac{I_{S 2}}{I_{S 1}} \tag{4.235}
\end{equation*}
$$

Thus if the ratio of the input to the output current is held constant, the voltage across $R_{2}$ is indeed proportional to $V_{T}$. This fact is utilized in the self-biased circuit of Fig. 4.41. Here $Q_{3}$ and $Q_{4}$ are selected to have equal areas. Therefore, if we assume that $\beta_{F} \rightarrow \infty$ and $V_{A} \rightarrow \infty$, the current mirror formed by $Q_{3}$ and $Q_{4}$ forces the collector current of $Q_{1}$ to equal that of $Q_{2}$. Figure 4.41 also shows that $Q_{2}$ has two emitters and $Q_{1}$ has one emitter, which indicates that the emitter area of $Q_{2}$ is twice that of $Q_{1}$ in this example. This selection is made to force the gain around the positive feedback loop at point $B$ in Fig. $4.37 b$ to be more than unity so that point $B$ is an unstable operating point and a stable nonzero operating point exists at point $A$. As in other self-biased circuits, a start-up circuit is required to make sure that enough current flows to force operation at point $A$ in Fig. $4.37 b$ in practice. Under these conditions, $I_{S 2}=2 I_{S 1}$ and the voltage across $R_{2}$ is

$$
\begin{equation*}
I_{\mathrm{OUT}} R_{2}=V_{T} \ln \frac{I_{\mathrm{IN}}}{I_{\mathrm{OUT}}} \frac{I_{S 2}}{I_{S 1}}=V_{T} \ln 2 \tag{4.236}
\end{equation*}
$$

Therefore, the output current is

$$
\begin{equation*}
I_{\text {OUT }}=\frac{V_{T}}{R_{2}} \ln 2 \tag{4.237}
\end{equation*}
$$

image_name:Figure 4.41 Bias current source using the thermal voltage
description:
[
name: Q1, type: NPN, ports: {C: Y, B: Y, E: GND}
name: Q2, type: NPN, ports: {C: X, B: Y, E: Y}
name: Q3, type: PNP, ports: {C: X, B: X, E: Y}
name: Q4, type: PNP, ports: {C: X, B: X, E: X}
name: R2, type: Resistor, value: R2, ports: {N1: Y, N2: GND}
]
extrainfo:The circuit is a bias current source using thermal voltage. It includes two NPN transistors (Q1, Q2) and two PNP transistors (Q3, Q4). The resistor R2 is connected between node Y and ground. The circuit is designed to provide a stable output current (I_OUT) that is less sensitive to temperature variations, as indicated by the equations provided. The circuit also shows connections to V_CC and load currents I_BIAS1 and I_BIAS2.

Figure 4.41 Bias current source using the thermal voltage.

The temperature variation of the output current can be calculated as follows. From (4.237)

$$
\begin{align*}
\frac{\partial I_{\mathrm{OUT}}}{\partial T} & =(\ln 2) \frac{R_{2} \frac{\partial V_{T}}{\partial T}-V_{T} \frac{\partial R_{2}}{\partial T}}{R_{2}^{2}} \\
& =\frac{V_{T}}{R_{2}}(\ln 2)\left(\frac{1}{V_{T}} \frac{\partial V_{T}}{\partial T}-\frac{1}{R_{2}} \frac{\partial R_{2}}{\partial T}\right) \tag{4.238}
\end{align*}
$$

Substituting (4.237) in (4.238) gives

$$
\begin{equation*}
T C_{F}=\frac{1}{I_{\mathrm{OUT}}} \frac{\partial I_{\mathrm{OUT}}}{\partial T}=\frac{1}{V_{T}} \frac{\partial V_{T}}{\partial T}-\frac{1}{R_{2}} \frac{\partial R_{2}}{\partial T} \tag{4.239}
\end{equation*}
$$

This circuit produces much smaller temperature coefficient of the output current than the $V_{B E}$ reference because the fractional sensitivities of both $V_{T}$ and that of a diffused resistor $R_{2}$ are positive and tend to cancel in (4.239). We have chosen a transistor area ratio of two to one as an example. In practice, this ratio is often chosen to minimize the total area required for the transistors and for resistor $R_{2}$.

#### EXAMPLE

Design a bias reference of the type shown in Fig. 4.41 to produce an output current of $100 \mu \mathrm{~A}$. Find the $T C_{F}$ of $I_{\text {OUT }}$. Assume the resistor temperature coefficient $(1 / R)(\partial R / \partial T)=$ $+1500 \mathrm{ppm} /{ }^{\circ} \mathrm{C}$.

From (4.237)

$$
R_{2}=\frac{V_{T}(\ln 2)}{I_{\text {OUT }}}=\frac{(26 \mathrm{mV})(\ln 2)}{100 \mu \mathrm{~A}} \simeq 180 \Omega
$$

From (4.239)

$$
\begin{aligned}
\frac{1}{I_{\text {OUT }}} \frac{\partial I_{\mathrm{OUT}}}{\partial T} & =\frac{1}{V_{T}} \frac{\partial V_{T}}{\partial T}-1500 \times 10^{-6}=\frac{1}{V_{T}} \frac{V_{T}}{T}-1500 \times 10^{-6} \\
& =\frac{1}{T}-1500 \times 10^{-6}
\end{aligned}
$$

Assuming operation at room temperature, $T=300^{\circ} \mathrm{K}$ and

$$
\frac{1}{I_{\mathrm{OUT}}} \frac{\partial I_{\mathrm{OUT}}}{\partial T} \simeq 3300 \times 10^{-6}-1500 \times 10^{-6}=1800 \mathrm{ppm} /{ }^{\circ} \mathrm{C}
$$

$V_{T}$-referenced bias circuits are also commonly used in CMOS technology. A simple example is shown in Fig. 4.42, where bipolar transistors $Q_{1}$ and $Q_{2}$ are parasitic devices inherent in $p$-substrate CMOS technologies. Here the emitter areas of these transistors differ by a factor $n$, and the feedback loop forces them to operate at the same bias current. As a result, the difference between the two base-emitter voltages must appear across resistor $R$. The resulting current is

$$
\begin{equation*}
I_{\mathrm{OUT}}=\frac{V_{T} \ln (n)}{R} \tag{4.240}
\end{equation*}
$$

In the circuit of Fig. 4.42, small differences in the gate-source voltages of $M_{3}$ and $M_{4}$ result in large variations in the output current because the voltage drop across $R$ is only on the order of 100 mV . Such gate-source voltage differences can result from device mismatches or from channel-length modulation in $M_{3}$ and $M_{4}$ because they have different drain-source voltages. Practical implementations of this circuit typically utilize large geometry devices for $M_{3}$ and $M_{4}$ to minimize offsets and cascode or Wilson current sources to minimize channel-length modulation effects. A typical example of a practical circuit is shown in Fig. 4.43. In general, cascoding is often used to improve the performance of reference circuits in all technologies. The main limitation of the application of cascoding is that it increases the minimum required power-supply voltage to operate all transistors in the active region.
image_name:Figure 4.43
description:
[
name: M5, type: PMOS, ports: {S: VDD, D: X1, G: X1}
name: M6, type: PMOS, ports: {S: VDD, D: X1, G: X1}
name: M7, type: PMOS, ports: {S: VDD, D: LOAD, G: X1}
name: M3, type: NMOS, ports: {S: GND, D: X1, G: e1s3}
name: M4, type: NMOS, ports: {S: X1, D: S4, G: e1s3}
name: Q1, type: PMOS, ports: {C: GND, B: GND, E: e1s3}
name: Q2, type: PMOS, ports: {C: GND, B: GND, E: r1}
name: R, type: Resistor, value: R, ports: {N1: S4, N2: r1}
]
extrainfo:The circuit is a CMOS V_T-referenced self-biased reference circuit with cascoded devices to improve power-supply rejection and initial accuracy. It uses PMOS and NMOS transistors along with resistors to achieve biasing and regulation. The circuit is designed to be temperature-insensitive and improve performance by minimizing channel-length modulation effects.

Figure 4.42 Example of a CMOS $V_{T}$-referenced self-biased circuit.
image_name:Figure 4.42
description:
[
name: M5, type: PMOS, ports: {S: VDD, D: X1, G: X2}
name: M6, type: PMOS, ports: {S: VDD, D: X2, G: X2}
name: M7, type: PMOS, ports: {S: VDD, D: d7s12, G: X2}
name: M10, type: PMOS, ports: {S: VDD, D: d8g9d10, G: X1}
name: M11, type: PMOS, ports: {S: X1, D: d8g9d10, G: X1}
name: M12, type: PMOS, ports: {S: d7s12, D: LOAD, G: X1}
name: M3, type: NMOS, ports: {S: e1s3, D: d3g4s8, G: d8g9d10}
name: M4, type: NMOS, ports: {S: d4s9, D: d3g4s8, G: d8g9d10}
name: M8, type: NMOS, ports: {S: d3g4s8, D: d8g9d10, G: d8g9d10}
name: M9, type: NMOS, ports: {S: d4s9, D: d8g9d10, G: d8g9d10}
name: Q1, type: PNP, ports: {C: e1s3, B: GND, E: GND}
name: Q2, type: PNP, ports: {C: e2, B: GND, E: GND}
name: R, type: Resistor, value: R, ports: {N1: S4, N2: e2}
]
extrainfo:The circuit is a CMOS V_T-referenced self-biased reference circuit with cascoded devices to improve power-supply rejection and initial accuracy. It uses PMOS and NMOS transistors along with resistors to achieve biasing and regulation. The circuit is designed to be temperature-insensitive and improve performance by minimizing channel-length modulation effects.

Figure 4.43 Example of a CMOS
$V_{T}$-referenced self-biased reference circuit with cascoded devices to improve power-supply rejection and initial accuracy.

### 4.4.3 Temperature-Insensitive Biasing

As illustrated by the examples in Section 4.4.2, the base-emitter-voltage- and thermal-voltagereferenced circuits have rather high temperature coefficients of output current. Although the temperature sensitivity is reduced considerably in the thermal-voltage circuit, even its temperature coefficient is not low enough for many applications. Thus we are led to examine other possibilities for the realization of a biasing circuit with low temperature coefficient.

#### 4.4.3.1 Band-Gap-Referenced Bias Circuits in Bipolar Technology

Since the bias sources referenced to $V_{B E(\text { on })}$ and $V_{T}$ have opposite $T C_{F}$, the possibility exists for referencing the output current to a composite voltage that is a weighted sum of $V_{B E(\text { on })}$ and $V_{T}$. By proper weighting, zero temperature coefficient should be attainable.

In the biasing sources described so far, we have concentrated on the problem of obtaining a current with low temperature coefficient. In practice, requirements often arise for low-temperature-coefficient voltage bias or reference voltages. The voltage reference for a voltage regulator is a good example. The design of these two types of circuits is similar except that in the case of the current source, a temperature coefficient must be intentionally introduced into the voltage reference to compensate for the temperature coefficient of the resistor that will define the current. In the following description of the band-gap reference, we assume for simplicity that the objective is a voltage source of low temperature coefficient.

First consider the hypothetical circuit of Fig. 4.44. An output voltage is developed that is equal to $V_{B E(\text { on })}$ plus a constant $M$ times $V_{T}$. To determine the required value for $M$, we must determine the temperature coefficient of $V_{B E(\text { on })}$. Neglecting base current,

$$
\begin{equation*}
V_{B E(\mathrm{on})}=V_{T} \ln \frac{I_{1}}{I_{S}} \tag{4.241}
\end{equation*}
$$

image_name:Figure 4.44 Hypothetical band-gap reference circuit
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: e1b1, E: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: VCC, Nn: e1b1}
name: Sum, type: OpAmp, value: Sum, ports: {InP: e1b1, InN: MVT, Out: Vout}
]
extrainfo:The circuit is a hypothetical band-gap reference circuit aiming to produce a voltage with a low temperature coefficient. The output voltage Vout is the sum of V_BE(on) and a constant M times V_T. The temperature coefficient of V_BE(on) is -2 mV/°C, while the coefficient of V_T is +0.085 mV/°C. The circuit includes a current source I1 and a transistor Q1, with an operational amplifier labeled 'Sum' to combine the voltages.
image_name:V_{BE(on)} vs T
description:### Type of Graph and Function:
The graph is a plot of voltage versus temperature, specifically showing the behavior of \( V_{BE(\text{on})} \) and \( V_T \) as functions of temperature \( T \). This is likely a linear plot, as indicated by the linear trend lines.

Axes Labels and Units:
- **X-axis:** Represents temperature \( T \). The units are typically in degrees Celsius (°C) but are not explicitly labeled in the image.
- **Y-axis:** Represents voltage, specifically \( V_{BE(\text{on})} \) and \( V_T \). The units are in millivolts (mV).

Overall Behavior and Trends:
- **\( V_{BE(\text{on})} \):** This voltage decreases linearly with temperature, following a negative temperature coefficient of \(-2 \text{ mV/°C}\). This suggests a linear decrease in \( V_{BE(\text{on})} \) as temperature increases.
- **\( V_T \):** This voltage increases linearly with temperature, with a positive temperature coefficient of \(+0.085 \text{ mV/°C}\) or \(+3300 \text{ ppm/°C}\). This indicates a linear increase in \( V_T \) as temperature rises.

Key Features and Technical Details:
- The graph highlights the contrasting temperature coefficients of \( V_{BE(\text{on})} \) and \( V_T \).
- \( V_{OUT} = V_{BE(\text{on})} + M \cdot V_T \) is the output voltage, where \( M \) is a constant that adjusts the contribution of \( V_T \) to counterbalance the temperature dependence of \( V_{BE(\text{on})} \).

Annotations and Specific Data Points:
- The graph includes annotations showing the temperature coefficients: \(-2 \text{ mV/°C}\) for \( V_{BE(\text{on})} \) and \(+0.085 \text{ mV/°C}\) for \( V_T \).
- The circuit diagram accompanying the graph shows the relationship between these voltages and the output voltage \( V_{OUT} \), emphasizing the summation of \( V_{BE(\text{on})} \) and \( M \cdot V_T \) to achieve a stable reference voltage.

Figure 4.44 Hypothetical band-gap reference circuit.

As shown in Chapter 1, the saturation current $I_{S}$ can be related to the device structure by

$$
\begin{equation*}
I_{S}=\frac{q A n_{i}^{2} \bar{D}_{n}}{Q_{B}}=B n_{i}^{2} \bar{D}_{n}=B^{\prime} n_{i}^{2} T \bar{\mu}_{n} \tag{4.242}
\end{equation*}
$$

where $n_{i}$ is the intrinsic minority-carrier concentration, $Q_{B}$ is the total base doping per unit area, $\bar{\mu}_{n}$ is the average electron mobility in the base, $A$ is the emitter-base junction area, and $T$ is the temperature. Here, the constants $B$ and $B^{\prime}$ involve only temperature-independent quantities. The Einstein relation $\mu_{n}=(q / k T) D_{n}$ was used to write $I_{S}$ in terms of $\bar{\mu}_{n}$ and $n_{i}^{2}$. The quantities in (4.242) that are temperature dependent are given by ${ }^{15}$

$$
\begin{gather*}
\bar{\mu}_{n}=C T^{-n}  \tag{4.243}\\
n_{i}^{2}=D T^{3} \exp \left(-\frac{V_{G 0}}{V_{T}}\right) \tag{4.244}
\end{gather*}
$$

where $V_{G 0}$ is the band-gap voltage of silicon extrapolated to $0^{\circ} \mathrm{K}$. Here again $C$ and $D$ are temperature-independent quantities whose exact values are unimportant in the analysis. The exponent $n$ in the expression for base-region electron mobility $\bar{\mu}_{n}$ is dependent on the doping level in the base. Combining (4.241), (4.242), (4.243), and (4.244) yields

$$
\begin{equation*}
V_{B E(\mathrm{on})}=V_{T} \ln \left(I_{1} T^{-\gamma} E \exp \frac{V_{G 0}}{V_{T}}\right) \tag{4.245}
\end{equation*}
$$

where $E$ is another temperature-independent constant and

$$
\begin{equation*}
\gamma=4-n \tag{4.246}
\end{equation*}
$$

In actual band-gap circuits, the current $I_{1}$ is not constant but varies with temperature. We assume for the time being that this temperature variation is known and that it can be written
in the form

$$
\begin{equation*}
I_{1}=G T^{\alpha} \tag{4.247}
\end{equation*}
$$

where $G$ is another temperature-independent constant. Combining (4.245) and (4.247) gives

$$
\begin{equation*}
V_{B E(\text { on })}=V_{G 0}-V_{T}[(\gamma-\alpha) \ln T-\ln (E G)] \tag{4.248}
\end{equation*}
$$

From Fig. 4.44, the output voltage is

$$
\begin{equation*}
V_{\text {OUT }}=V_{B E(\mathrm{on})}+M V_{T} \tag{4.249}
\end{equation*}
$$

Substitution of (4.248) into (4.249) gives

$$
\begin{equation*}
V_{\text {OUT }}=V_{G 0}-V_{T}(\gamma-\alpha) \ln T+V_{T}[M+\ln (E G)] \tag{4.250}
\end{equation*}
$$

This expression gives the output voltage as a function of temperature in terms of the circuit parameters $G, \alpha$, and $M$, and the device parameters $E$ and $\gamma$. Our objective is to make $V_{\text {OUT }}$ independent of temperature. To this end, we take the derivative of $V_{\text {OUT }}$ with respect to temperature to find the required values of $G, \gamma$, and $M$ to give zero $T C_{F}$. Differentiating (4.250) gives

$$
\begin{equation*}
0=\left.\frac{d V_{\mathrm{OUT}}}{d T}\right|_{T=T_{0}}=\frac{V_{T 0}}{T_{0}}[M+\ln (E G)]-\frac{V_{T 0}}{T_{0}}(\gamma-\alpha) \ln T_{0}-\frac{V_{T 0}}{T_{0}}(\gamma-\alpha) \tag{4.251}
\end{equation*}
$$

where $T_{0}$ is the temperature at which the $T C_{F}$ of the output is zero and $V_{T 0}$ is the thermal voltage $V_{T}$ evaluated at $T_{0}$. Equation 4.251 can be rearranged to give

$$
\begin{equation*}
[M+\ln (E G)]=(\gamma-\alpha) \ln T_{0}+(\gamma-\alpha) \tag{4.252}
\end{equation*}
$$

This equation gives the required values of circuit parameters $M, \alpha$, and $G$ in terms of the device parameters $E$ and $\gamma$. In principle, these values could be calculated directly from (4.252). However, further insight is gained by back-substituting (4.252) into (4.250). The result is

$$
\begin{equation*}
V_{\text {OUT }}=V_{G 0}+V_{T}(\gamma-\alpha)\left(1+\ln \frac{T_{0}}{T}\right) \tag{4.253}
\end{equation*}
$$

Thus the temperature dependence of the output voltage is entirely described by the single parameter $T_{0}$, which in turn is determined by the constants $M, E$, and $G$.

Using (4.253), the output voltage at the zero $T C_{F}$ temperature ( $T=T_{0}$ ) is given by

$$
\begin{equation*}
\left.V_{\text {OUT }}\right|_{T=T_{0}}=V_{G 0}+V_{T 0}(\gamma-\alpha) \tag{4.254}
\end{equation*}
$$

For example, to achieve zero $T C_{F}$ at $27^{\circ} \mathrm{C}$, assuming that $\gamma=3.2$ and $\alpha=1$,

$$
\begin{equation*}
\left.V_{\text {OUT }}\right|_{T=T_{0}=25^{\circ} \mathrm{C}}=V_{G 0}+2.2 V_{T 0} \tag{4.255}
\end{equation*}
$$

The band-gap voltage of silicon is $V_{G 0}=1.205 \mathrm{~V}$ so that

$$
\begin{equation*}
\left.V_{\text {OUT }}\right|_{T=T_{0}=25^{\circ} \mathrm{C}}=1.205 \mathrm{~V}+(2.2)(0.026 \mathrm{~V})=1.262 \mathrm{~V} \tag{4.256}
\end{equation*}
$$

Therefore, the output voltage for zero temperature coefficient is close to the band-gap voltage of silicon, which explains the name given to these bias circuits.

Differentiating (4.253) with respect to temperature yields

$$
\begin{align*}
\frac{d V_{\mathrm{OUT}}}{d T} & =\frac{1}{T}\left[V_{T}(\gamma-\alpha)\left(1+\ln \frac{T_{0}}{T}\right)\right]-\frac{V_{T}}{T}(\gamma-\alpha) \\
& =(\gamma-\alpha) \frac{V_{T}}{T}\left(\ln \frac{T_{0}}{T}\right) \tag{4.257}
\end{align*}
$$

image_name:Figure 4.45
description:The graph in Figure 4.45 is a plot showing the variation of the band-gap reference output voltage, \( V_{OUT} \), with temperature, \( T \). This is a family of curves for different values of \( T_0 \), where \( T_0 \) is the temperature at which the derivative of the output voltage with respect to temperature, \( \frac{dV_{OUT}}{dT} \), is zero.

**Type of Graph and Function:**
This is a temperature-voltage characteristic graph, typically used to illustrate how the output voltage of a band-gap reference circuit varies with temperature.

**Axes Labels and Units:**
- The x-axis represents temperature \( T \) in degrees Celsius (°C).
- The y-axis represents the output voltage \( V_{OUT} \) in volts (V).

**Overall Behavior and Trends:**
The graph consists of three curves labeled (a), (b), and (c), each corresponding to different values of \( T_0 \):
- Curve (a) corresponds to \( T_0 = 400°K \).
- Curve (b) corresponds to \( T_0 = 300°K \).
- Curve (c) corresponds to \( T_0 = 200°K \).

Each curve exhibits a point where the slope is zero, indicating that the output voltage does not change with temperature at that specific \( T_0 \). For temperatures below \( T_0 \), the curves have a positive slope, meaning the output voltage increases with temperature. For temperatures above \( T_0 \), the curves have a negative slope, indicating the output voltage decreases with temperature.

**Key Features and Technical Details:**
- For curve (a), \( V_{OUT} \) starts around 1.270 V and increases slightly as temperature increases.
- For curve (b), \( V_{OUT} \) starts around 1.260 V, with a peak at \( T_0 = 300°K \) where \( \frac{dV_{OUT}}{dT} = 0 \).
- For curve (c), \( V_{OUT} \) starts around 1.240 V and decreases as temperature increases past \( T_0 = 200°K \).

**Annotations and Specific Data Points:**
- Each curve is annotated at the point where \( \frac{dV_{OUT}}{dT} = 0 \), clearly marking the temperature \( T_0 \) for which the slope is zero.
- The curves show how the output voltage is designed to have minimal temperature dependence at specific \( T_0 \) values, illustrating the concept of zero temperature coefficient in band-gap reference circuits.

Figure 4.45 Variation of band-gap reference output voltage with temperature.

Equation 4.257 gives the slope of the output as a function of temperature. A typical family of output-voltage-variation characteristics is shown in Fig. 4.45 for different values of $T_{0}$ for the special case in which $\alpha=0$ and $I_{1}$ is temperature independent. The slope of each curve is zero at $T=T_{0}$. When $T<T_{0}$, the slope is positive because the argument of the logarithm in (4.257) is more than unity. Similarly, the slope is negative when $T>T_{0}$. For values of $T$ near $T_{0}$,

$$
\begin{equation*}
\ln \frac{T_{0}}{T}=\ln \left(1+\frac{T_{0}-T}{T}\right) \simeq \frac{T_{0}-T}{T} \tag{4.258}
\end{equation*}
$$

and we have

$$
\begin{equation*}
\frac{d V_{\mathrm{OUT}}}{d T} \simeq(\gamma-\alpha) \frac{V_{T}}{T}\left(\frac{T_{0}-T}{T}\right) \tag{4.259}
\end{equation*}
$$

As shown by (4.257) and (4.259), the temperature coefficient of the output is zero only at one temperature $T=T_{0}$. This result stems from the addition of a weighted thermal voltage to a base-emitter voltage as in Fig. 4.44. Since the temperature coefficient of base-emitter voltage is not exactly constant, the gain $M$ can be chosen to set the temperature coefficient of the output to zero only at one temperature. In other words, the thermal voltage generator is used to cancel the linear dependence of the base-emitter voltage with temperature. After this cancellation, the changing outputs in Fig. 4.45 stem from the nonlinear dependence of the base-emitter voltage with temperature. Band-gap references that compensate for this nonlinearity are said to be curvature compensated. ${ }^{16,17,18}$

#### EXAMPLE

A band-gap reference is designed to give a nominal output voltage of 1.262 V , which gives zero $T C_{F}$ at $27^{\circ} \mathrm{C}$. Because of component variations, the actual room temperature output voltage is 1.280 V . Find the temperature of actual zero $T C_{F}$ of $V_{\text {OUT }}$. Also, write an equation for $V_{\text {OUT }}$ as a function of temperature, and calculate the $T C_{F}$ at room temperature. Assume that $\gamma=3.2$ and $\alpha=1$.

From (4.253) at $T=27^{\circ} \mathrm{C}=300^{\circ} \mathrm{K}$,

$$
1.280 \mathrm{~V}=1.205+(0.026 \mathrm{~V})(2.2)\left(1+\ln \frac{T_{0}}{300^{\circ} \mathrm{K}}\right)
$$

and thus

$$
T_{0}=300^{\circ} \mathrm{K}\left(\exp \frac{18 \mathrm{mV}}{57 \mathrm{mV}}\right)=411^{\circ} \mathrm{K}
$$

Therefore, the $T C_{F}$ will be zero at $T_{0}=411^{\circ} \mathrm{K}=138^{\circ} \mathrm{C}$, and we can express $V_{\text {OUT }}$ as

$$
V_{\text {OUT }}=1.205 \mathrm{~V}+57 \mathrm{mV}\left(1+\ln \frac{411^{\circ} \mathrm{K}}{T}\right)
$$

From (4.259) with $T=300^{\circ} \mathrm{K}$ and $T_{0}=411^{\circ} \mathrm{K}$,

$$
\frac{d V_{\mathrm{OUT}}}{d T} \simeq(2.2) \frac{26 \mathrm{mV}}{300^{\circ} \mathrm{K}}\left(\frac{411-300}{300}\right) \simeq 70 \mu \mathrm{~V} /{ }^{\circ} \mathrm{K}=70 \mu \mathrm{~V} /{ }^{\circ} \mathrm{C}
$$

Therefore, the $T C_{F}$ at room temperature is

$$
T C_{F}=\frac{1}{V_{\text {OUT }}} \frac{d V_{\mathrm{OUT}}}{d T} \simeq \frac{70 \mu \mathrm{~V} /{ }^{\circ} \mathrm{C}}{1.280 \mathrm{~V}} \simeq 55 \mathrm{ppm} /{ }^{\circ} \mathrm{C}
$$

To reduce the $T C_{F}$, the constant $M$ in (4.249)-(4.252) is often trimmed at one temperature so that the band-gap output is set to a desired target voltage. ${ }^{19}$ In principle, the target voltage is given by (4.253). In practice, however, significant inaccuracy in (4.253) stems from an approximation in (4.244). ${ }^{20}$ As a result, the target voltage is usually determined experimentally by measuring the $T C_{F}$ directly for several samples of each band-gap reference in a given process. ${ }^{21,22}$ This procedure reduces the $T C_{F}$ at the reference temperature to a level of about $10 \mathrm{ppm} /{ }^{\circ} \mathrm{C}$.

A key parameter of interest in reference sources is the variation of the output that is encountered over the entire temperature range. Since the $T C_{F}$ expresses the temperature sensitivity only at one temperature, a different parameter must be used to characterize the behavior of the circuit over a broad temperature range. An effective temperature coefficient can be defined for a voltage reference as

$$
\begin{equation*}
T C_{F(\mathrm{eff})}=\frac{1}{V_{\mathrm{OUT}}}\left(\frac{V_{\mathrm{MAX}}-V_{\mathrm{MIN}}}{T_{\mathrm{MAX}}-T_{\mathrm{MIN}}}\right) \tag{4.260}
\end{equation*}
$$

where $V_{\mathrm{MAX}}$ and $V_{\mathrm{MIN}}$ are the largest and smallest output voltages observed over the temperature range, and $T_{\mathrm{MAX}}-T_{\mathrm{MIN}}$ is the temperature excursion. $V_{\mathrm{OUT}}$ is the nominal output voltage. By this standard, $T C_{F(\text { eff })}$ over the -55 to $125^{\circ} \mathrm{C}$ range for case (b) of Fig. 4.45 is $44 \mathrm{ppm} /{ }^{\circ} \mathrm{C}$. If the temperature range is restricted to 0 to $70^{\circ} \mathrm{C}, T C_{F(\mathrm{eff})}$ improves to $17 \mathrm{ppm} /{ }^{\circ} \mathrm{C}$. Thus over a restricted temperature range, this reference is comparable with the standard cell in temperature stability once the zero $T C_{F}$ temperature has been set at room temperature. Saturated standard cells (precision batteries) have a $T C_{F}$ of about $\pm 30 \mathrm{ppm} /{ }^{\circ} \mathrm{C}$.

Practical realizations of band-gap references in bipolar technologies take on several forms. ${ }^{15,19,23}$ One such circuit is illustrated in Fig. 4.46a. ${ }^{15}$ This circuit uses a feedback loop to establish an operating point in the circuit such that the output voltage is equal to a $V_{B E(\text { on })}$ plus a voltage proportional to the difference between two base-emitter voltages. The operation of the feedback loop is best understood by reference to Fig. 4.46b, in which a portion of the circuit is shown. We first consider the variation of the output voltage $V_{2}$ as the input voltage $V_{1}$ is varied from zero in the positive direction. Initially, with $V_{1}=0$, devices $Q_{1}$ and $Q_{2}$ do not
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: b1b2c1, B: V1, E: GND}
name: Q2, type: NPN, ports: {C: b1b2c1, B: b1b2c1, E: GND}
name: Q3, type: NPN, ports: {C: VOUT, B: C2b3, E: GND}
name: R1, type: Resistor, value: R1, ports: {N1: V1, N2: VOUT}
name: R2, type: Resistor, value: R2, ports: {N1: VOUT, N2: VOUT}
name: R3, type: Resistor, value: R3, ports: {N1: V2, N2: GND}
name: C2b3, type: Capacitor, value: C2b3, ports: {Np: VCC, Nn: C2b3}
name: C3b4, type: Capacitor, value: C3b4, ports: {Np: VOUT, Nn: GND}
name: A, type: OpAmp, value: A, ports: {InP: VOUT, InN: VOUT, OutP: VOUT, OutN: VOUT}
name: I, type: CurrentSource, value: I, ports: {Np: VCC, Nn: C2b3}
]
extrainfo:This circuit is a Widlar band-gap reference, designed to provide a stable reference voltage that is largely independent of temperature and supply voltage variations. It utilizes transistors Q1, Q2, and Q3, resistors R1, R2, and R3, capacitors C2b3 and C3b4, an op-amp A, and a current source I to achieve this functionality.
image_name:(b)
description:The diagram labeled (b) in Figure 4.46 represents a portion of a band-gap subcircuit. This graph is a voltage transfer characteristic curve, which shows the relationship between the output voltage $V_2$ and the input voltage $V_1$.

1. **Type of Graph and Function:**
- The graph is a voltage transfer characteristic curve.
- It displays the behavior of the output voltage $V_2$ as a function of the input voltage $V_1$.

2. **Axes Labels and Units:**
- The x-axis represents the input voltage $V_1$.
- The y-axis represents the output voltage $V_2$.
- Both axes are likely measured in volts (V), although specific units are not labeled on the graph.

3. **Overall Behavior and Trends:**
- The graph shows a non-linear relationship between $V_1$ and $V_2$.
- Initially, as $V_1$ increases from zero, $V_2$ remains at zero until $V_1$ reaches approximately 0.6 V.
- Beyond this threshold, $V_2$ begins to increase, indicating the conduction of current by the transistors $Q_1$ and $Q_2$.
- There are multiple regions of interest marked as points (1), (2), (3), and (4) on the graph.

4. **Key Features and Technical Details:**
- Point (1) corresponds to the onset of conduction in $Q_1$, where $V_1$ exceeds 0.6 V.
- The curve shows a rise in $V_2$ as $V_1$ continues to increase, suggesting a proportional relationship after the threshold.
- The graph likely represents the behavior of the feedback loop in the circuit, with $V_2$ being a function of the base-emitter voltages of the transistors.

5. **Annotations and Specific Data Points:**
- Key points are annotated on the graph, such as the threshold voltage $V_{BE(on)}$.
- The curve features inflection points that correspond to significant changes in the conduction state of the transistors.
- The annotations provide insight into the operational regions of the circuit, crucial for understanding the feedback mechanism.
image_name:(c)
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: b1c1, E: GND}
name: Q2, type: NPN, ports: {C: b1c1, B: b2c2, E: GND}
name: Q3, type: NPN, ports: {C: Vout, B: b3c4, E: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: b1c1}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: b2c2}
name: R3, type: Resistor, value: R3, ports: {N1: b2c2, N2: GND}
name: A, type: OpAmp, value: A, ports: {InP: b1c1, InN: b2c2, OutP: Vout}
name: I, type: CurrentSource, value: I, ports: {Np: VCC, Nn: b3c4}
]
extrainfo:This is an improved band-gap reference circuit. It utilizes a combination of NPN transistors and an operational amplifier to provide a stable output voltage that is less sensitive to temperature variations. The circuit includes feedback mechanisms to maintain consistent output.

Figure 4.46 (a) Widlar band-gap reference. (b) Band-gap subcircuit. (c) Improved band-gap reference.
conduct and $V_{2}=0$. As $V_{1}$ is increased, $Q_{1}$ and $Q_{2}$ do not conduct significant current until the input voltage reaches about 0.6 V . When $V_{1}<0.6 \mathrm{~V}, V_{2}=V_{1}$ since the voltage drop on $R_{2}$ is zero. When $V_{1}$ exceeds 0.6 V , however, $Q_{1}$ begins to conduct current, corresponding to point (1) in Fig. 4.46b. The magnitude of the current in $Q_{1}$ is roughly equal to $\left(V_{1}-0.6 \mathrm{~V}\right) / R_{1}$. For small values of this current, $Q_{1}$ and $Q_{2}$ carry the same current because the drop across $R_{3}$ is negligible at low currents. Since $R_{2}$ is much larger than $R_{1}$, the voltage drop across $R_{2}$ is much larger than $\left(V_{1}-0.6 \mathrm{~V}\right)$, and transistor $Q_{2}$ saturates, corresponding to point (2) in Fig. 4.46b. Because of the presence of $R_{3}$, the collector current that would flow in $Q_{2}$ if it were in the forward-active region has an approximately logarithmic dependence on $V_{1}$, exactly as in the Widlar source. Thus as $V_{1}$ is further increased, a point is reached at which $Q_{2}$ comes out of saturation because $V_{1}$ increases faster than the voltage drop across $R_{2}$. This point is labeled point (3) in Fig. 4.46b.

Now consider the complete circuit of Fig. 4.46a. If transistor $Q_{3}$ is initially turned off, transistor $Q_{4}$ will drive $V_{1}$ in the positive direction. This process will continue until enough voltage is developed at the base of $Q_{3}$ to produce a collector current in $Q_{3}$ approximately equal to $I$. Thus the circuit stabilizes with voltage $V_{2}$ equal to one diode drop, the base-emitter voltage of $Q_{3}$, which can occur at point (1) or point (4) in Fig. 4.46b. Appropriate start-up circuitry must be included to ensure operation at point (4).

Assuming that the circuit has reached a stable operating point at point (4), the output voltage $V_{\text {OUT }}$ is the sum of the base-emitter voltage of $Q_{3}$ and the voltage drop across $R_{2}$. The drop across $R_{2}$ is equal to the voltage drop across $R_{3}$ multiplied by $R_{2} / R_{3}$ because the collector current of $Q_{2}$ is approximately equal to its emitter current. The voltage drop across $R_{3}$ is equal to the difference in base-emitter voltages of $Q_{1}$ and $Q_{2}$. The ratio of currents in $Q_{1}$ and $Q_{2}$ is set by the ratio of $R_{2}$ to $R_{1}$.

A drawback of this reference is that the current $I$ is set by the power supply and may vary with power-supply variations. A self-biased band-gap reference circuit is shown in Fig. 4.46c. Assume that a stable operating point exists for this circuit and that the op amp is ideal. Then the differential input voltage of the op amp must be zero and the voltage drops across resistors $R_{1}$ and $R_{2}$ are equal. Thus the ratio of $R_{2}$ to $R_{1}$ determines the ratio of $I_{1}$ to $I_{2}$. These two currents are the collector currents of the two diode-connected transistors $Q_{2}$ and $Q_{1}$, assuming base currents are negligible. The voltage across $R_{3}$ is

$$
\begin{equation*}
V_{R 3}=\Delta V_{B E}=V_{B E 1}-V_{B E 2}=V_{T} \ln \frac{I_{1}}{I_{2}} \frac{I_{S 2}}{I_{S 1}}=V_{T} \ln \frac{R_{2}}{R_{1}} \frac{I_{S 2}}{I_{S 1}} \tag{4.261}
\end{equation*}
$$

Since the same current that flows in $R_{3}$ also flows in $R_{2}$, the voltage across $R_{2}$ must be

$$
\begin{equation*}
V_{R 2}=\frac{R_{2}}{R_{3}} V_{R 3}=\frac{R_{2}}{R_{3}} \Delta V_{B E}=\frac{R_{2}}{R_{3}} V_{T} \ln \frac{R_{2}}{R_{1}} \frac{I_{S 2}}{I_{S 1}} \tag{4.262}
\end{equation*}
$$

This equation shows that the voltage across $R_{2}$ is proportional to absolute temperature (PTAT) because of the temperature dependence of the thermal voltage. Since the op amp forces the voltages across $R_{1}$ and $R_{2}$ to be equal, the currents $I_{1}$ and $I_{2}$ are both proportional to temperature if the resistors have zero temperature coefficient. Thus for this reference, $\alpha=1$ in (4.247). The output voltage is the sum of the voltage across $Q_{2}, R_{3}$, and $R_{2}$ :

$$
\begin{align*}
V_{\text {OUT }} & =V_{B E 2}+V_{R 3}+V_{R 2}=V_{B E 2}+\left(1+\frac{R_{2}}{R_{3}}\right) \Delta V_{B E} \\
& =V_{B E 2}+\left(1+\frac{R_{2}}{R_{3}}\right) V_{T} \ln \frac{R_{2}}{R_{1}} \frac{I_{S 2}}{I_{S 1}}=V_{B E 2}+M V_{T} \tag{4.263}
\end{align*}
$$

The circuit thus behaves as a band-gap reference, with the value of $M$ set by the ratios of $R_{2} / R_{3}, R_{2} / R_{1}$, and $I_{S 2} / I_{S 1}$.

#### 4.4.3.2 Band-Gap-Referenced Bias Circuits in CMOS Technology

Band-gap-referenced biasing also can be implemented using the parasitic bipolar devices inherent in CMOS technology. For example, in a $n$-well process, substrate $p n p$ transistors can be used to replace the npn transistors in Fig. 4.46c, as shown in Fig. 4.47. Assume that the CMOS op amp has infinite gain but nonzero input-referred offset voltage $V_{O S}$. (The inputreferred offset voltage of an op amp is defined as the differential input voltage required to drive the output to zero.) Because of the threshold mismatch and the low transconductance per current of CMOS transistors, the offset of op amps in CMOS technologies is usually larger than in bipolar technologies. With the offset voltage, the voltage across $R_{3}$ is

$$
\begin{equation*}
V_{R 3}=V_{E B 1}-V_{E B 2}+V_{O S}=\Delta V_{E B}+V_{O S} \tag{4.264}
\end{equation*}
$$

image_name:Figure 4.47 A band-gap reference in n-well CMOS
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: InN(A)}
name: R2, type: Resistor, value: R2, ports: {N1: Vout, N2: X}
name: R3, type: Resistor, value: R3, ports: {N1: X, N2: e2}
name: Q1, type: PMOS, ports: {S: GND, D: e2, G: GND}
name: Q2, type: PMOS, ports: {S: GND, D: e2, G: GND}
name: Vos, type: VoltageSource, ports: {Np: InN(A), Nn: InP(A)}
name: A, type: OpAmp, value: A, ports: {InP: InP(A), InN: InN(A), Out: Vout}
]
extrainfo:The circuit is a band-gap reference in n-well CMOS technology. It uses PMOS transistors and resistors to stabilize the output voltage against variations in temperature and supply voltage. The op-amp is used to control the voltage across the resistors, and the offset voltage source compensates for mismatches.

Figure 4.47 A band-gap reference in $n$-well CMOS.

The emitter-base voltages are used here because the base-emitter voltages of the $p n p$ transistors operating in the forward-active region are negative. Then the voltage across $R_{2}$ is

$$
\begin{equation*}
V_{R 2}=\frac{R_{2}}{R_{3}} V_{R 3}=\frac{R_{2}}{R_{3}}\left(V_{E B 1}-V_{E B 2}+V_{O S}\right)=\frac{R_{2}}{R_{3}}\left(\Delta V_{E B}+V_{O S}\right) \tag{4.265}
\end{equation*}
$$

and the output voltage is 18

$$
\begin{align*}
V_{\mathrm{OUT}} & =V_{E B 2}+V_{R 3}+V_{R 2} \\
& =V_{E B 2}+\left(1+\frac{R_{2}}{R_{3}}\right)\left(\Delta V_{E B}+V_{O S}\right) \tag{4.266}
\end{align*}
$$

Since the difference in the base-emitter voltages is proportional to the thermal voltage, comparing (4.266) with $V_{O S}=0$ to (4.249) shows that the gain $M$ here is proportional to $\left(1+R_{2} / R_{3}\right)$. Rearranging (4.266) gives

$$
\begin{equation*}
V_{\mathrm{OUT}}=V_{E B 2}+\left(1+\frac{R_{2}}{R_{3}}\right)\left(\Delta V_{E B}\right)+V_{O S(\mathrm{out})} \tag{4.267}
\end{equation*}
$$

where the output-referred offset is

$$
\begin{equation*}
V_{O S(\text { out })}=\left(1+\frac{R_{2}}{R_{3}}\right) V_{O S} \tag{4.268}
\end{equation*}
$$

Equations 4.267 and 4.268 show that the output contains an offset voltage that is a factor of $\left(1+R_{2} / R_{3}\right)$ times bigger than the input-referred offset voltage. Therefore, the same gain that is applied to the difference in the base-emitter voltages is also applied to the input-referred offset voltage.

Assume that the offset voltage is independent of temperature. To set $T C_{F}$ of the output equal to zero, the gain must be changed so that temperature coefficients of the $V_{E B}$ and $\Delta V_{E B}$ terms cancel. Since the offset is assumed to be temperature independent, this cancellation occurs when the output is equal to the target, where zero offset was assumed, plus the outputreferred offset. If the gain is trimmed at $T=T_{0}$ to set the output to a target voltage assuming the offset is zero, (4.267) shows that the gain is too small if the offset voltage is positive and that the gain is too big if the offset voltage is negative. Since the gain is applied to the PTAT term, the resulting slope of the output versus temperature is negative when the offset is positive and the gain is too small. On the other hand, this slope is positive when the offset is negative and the gain is too big.

We will now calculate the magnitude of the slope of the output versus temperature at $T=T_{0}$. With zero offset and a target that assumes zero offset, trimming $R_{2}$ and/or $R_{3}$ to set the output in (4.267) to the target forces the slope of the $\Delta V_{E B}$ term to cancel the slope of the $V_{E B}$ term. With nonzero offset but the same target, the factor $\left(1+R_{2} / R_{3}\right)$ differs from its ideal value after trimming by $-V_{O S(\text { out })} / \Delta V_{E B}$. Since this error is multiplied by $\Delta V_{E B}$ in (4.267), the resulting slope of the output versus temperature is

$$
\begin{equation*}
\left.\frac{d V_{\mathrm{OUT}}}{d T}\right|_{T=T_{0}}=-\left(\frac{V_{O S(\text { out })}}{\Delta V_{E B}}\right) \frac{d \Delta V_{E B}}{d T} \tag{4.269}
\end{equation*}
$$

Since $\Delta V_{E B}$ is proportional to the thermal voltage $V_{T}$,

$$
\begin{equation*}
\Delta V_{E B}=H V_{T} \tag{4.270}
\end{equation*}
$$

where $H$ is a temperature-independent constant. Substituting (4.270) into (4.269) gives

$$
\begin{equation*}
\left.\frac{d V_{\text {OUT }}}{d T}\right|_{T=T_{0}}=-\left.\frac{V_{O S(\text { out })}}{H V_{T}} \frac{H V_{T}}{T}\right|_{T=T_{0}}=-\frac{V_{O S(\text { out })}}{T_{0}} \tag{4.271}
\end{equation*}
$$

Therefore, when the gain is trimmed at one temperature to set the band-gap output to a desired target voltage, variation in the op-amp offset causes variation in the output temperature coefficient. In practice, the op-amp offset is usually the largest source of nonzero temperature coefficient. ${ }^{18}$ Equation 4.271 shows that the temperature coefficient at $T=T_{0}$ is proportional to the output-referred offset under these circumstances. Furthermore, (4.268) shows that the output-referred offset is equal to the gain that is applied to the $\Delta V_{E B}$ term times the inputreferred offset. Therefore, minimizing this gain minimizes the variation in the temperature coefficient at the output. Since the reference output at $T=T_{0}$ for zero $T C_{F}$ is approximately equal to the band-gap voltage, the required gain can be minimized by maximizing the $\Delta V_{E B}$ term.

To maximize the $\Delta V_{E B}$ term, designers generally push a large current into a small transistor and a small current into a large transistor, as shown in Fig. 4.48. Ignoring base currents,

$$
\begin{equation*}
\Delta V_{E B}=V_{E B 1}-V_{E B 2}=V_{T} \ln \left(\frac{I_{1}}{I_{2}} \frac{I_{S 2}}{I_{S 1}}\right) \tag{4.272}
\end{equation*}
$$

Equation 4.272 shows that maximizing the product of the ratios $I_{1} / I_{2}$ and $I_{S 2} / I_{S 1}$ maximizes $\Delta V_{E B}$. In Fig. 4.48, $I_{1}>I_{2}$ is emphasized by drawing the symbol for $I_{1}$ larger than the symbol for $I_{2}$. Similarly, the emitter area of $Q_{2}$ is larger than that of $Q_{1}$ to make $I_{S 2}>I_{S 1}$,
image_name:Figure 4.48
description:
[
name: Q1, type: PNP, ports: {C: VDD, B: e1, E: GND}
name: Q2, type: PNP, ports: {C: VDD, B: e2, E: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: e1}
name: I2, type: CurrentSource, value: I2, ports: {Np: VDD, Nn: e2}
]
extrainfo:The circuit maximizes ΔVEB by increasing the ratios I1/I2 and IS2/IS1. It employs two PNP transistors, Q1 and Q2, with different emitter areas to achieve this.

Figure 4.48 A circuit that increases $\Delta V_{E B}$ by increasing $I_{1} / I_{2}$ and $I_{S 2} / I_{S 1}$.
image_name:Figure 4.49
description:
[
name: Q1, type: PNP, ports: {C: VDD, B: b1e3, E: e1}
name: Q2, type: PNP, ports: {C: VDD, B: b2e4, E: e2}
name: Q3, type: PNP, ports: {C: b1e3, B: b1e3, E: GND}
name: Q4, type: PNP, ports: {C: b2e4, B: b2e4, E: GND}
name: I1, type: CurrentSource, value: I1, ports: {Np: VDD, Nn: e1}
name: I2, type: CurrentSource, value: I2, ports: {Np: VDD, Nn: e2}
name: I3, type: CurrentSource, value: I3, ports: {Np: VDD, Nn: b1e3}
name: I4, type: CurrentSource, value: I4, ports: {Np: VDD, Nn: b2e4}
]
extrainfo:The circuit cascades emitter followers to double ΔVEB if IS3=IS1 and IS4=IS2. It uses two pairs of PNP transistors (Q1, Q3) and (Q2, Q4) with current sources to achieve this effect. The current sources I3 and I4 are equal to I1 and I2, respectively.

Figure 4.49 A circuit that cascades emitter followers to double $\Delta V_{E B}$ if $I_{S 3}=I_{S 1}$ and $I_{S 4}=I_{S 2}$.
and this relationship is shown by drawing the symbol of $Q_{2}$ larger than the symbol of $Q_{1} \cdot{ }^{24}$ In practice, these ratios are often each set to be about equal to ten, and the resulting $\Delta V_{E B} \simeq 120$ mV at room temperature. Because the logarithm function compresses its argument, however, a limitation of this approach arises. For example, if the argument is increased by a factor of ten, $\Delta V_{E B}$ increases by only $V_{T} \ln (10) \simeq 60 \mathrm{mV}$. Therefore, to double $\Delta V_{E B}$ to 240 mV , $\left(I_{1} / I_{2}\right)\left(I_{S 2} / I_{S 1}\right)$ must be increased by a factor of 100 to 10,000 . On the other hand, if $Q_{1}$ and the transistors that form $I_{2}$ are minimum-sized devices when $\left(I_{1} / I_{2}\right)\left(I_{S 2} / I_{S 1}\right)=100$, the required die area would be dominated by the biggest devices ( $Q_{2}$ and/or the transistors that form $\left.I_{1}\right)$. Therefore, increasing $\left(I_{1} / I_{2}\right)\left(I_{S 2} / I_{S 1}\right)$ from 100 to 10,000 would increase the die area by about a factor of 100 but only double $\Delta V_{E B}$.

To overcome this limitation, stages that each contribute to $\Delta V_{E B}$ can be cascaded. ${ }^{25}$ For example, consider Fig. 4.49, where two emitter-follower stages are cascaded. Here

$$
\begin{equation*}
\Delta V_{E B}=V_{E B 3}-V_{E B 4}+V_{E B 1}-V_{E B 2} \tag{4.273}
\end{equation*}
$$

Assume the new devices in Fig. 4.49 are identical to the corresponding original devices in Fig. 4.48 so that $I_{3}=I_{1}, I_{4}=I_{2}, I_{S 3}=I_{S 1}$, and $I_{S 4}=I_{S 2}$. Then ignoring base currents

$$
\begin{equation*}
\Delta V_{E B}=2\left(V_{E B 1}-V_{E B 2}\right)=2 V_{T} \ln \left(\frac{I_{1}}{I_{2}} \frac{I_{S 2}}{I_{S 1}}\right) \tag{4.274}
\end{equation*}
$$

Thus cascading two identical emitter followers doubles $\Delta V_{E B}$ while only doubling the required die area.

The effect of the offset in a band-gap reference can also be reduced by using offset cancellation. An example of offset cancellation in a CMOS band-gap reference with curvature correction in addition to an analysis of other high-order effects arising from finite $\beta_{F}, \beta_{F}$ mismatch, $\beta_{F}$ variation with temperature, nonzero base resistance, and nonzero temperature coefficient in the resistors is presented in Ref. 18.

A high-performance CMOS band-gap reference is shown in Fig. 4.50, where cascoded current mirrors are used to improve supply rejection. A $V_{T}$-dependent current from $M_{11}$ develops a $V_{T}$-dependent voltage across resistor $x R$. A proper choice of the ratio $x$ can give a bandgap voltage at $V_{\text {OUT }}$. If desired, a temperature-independent output current can be realized by choosing $x$ to give an appropriate temperature coefficient to $V_{\text {OUT }}$ to cancel the temperature coefficient of resistor $R_{2}$.
image_name:Figure 4.50
description:
[
name: M12, type: PMOS, ports: {S: VDD, D: s9d12, G: x1}
name: M9, type: PMOS, ports: {S: s9d12, D: s2s8d9, G: x2}
name: M8, type: NMOS, ports: {S: s4g9d8, D: g7g9d9, G: s2s8d9}
name: M4, type: NMOS, ports: {S: e1s4, D: g4g5s8, G: s4g9d8}
name: M13, type: PMOS, ports: {S: VDD, D: x1, G: x1}
name: M10, type: PMOS, ports: {S: x2, D: x2, G: x2}
name: M7, type: NMOS, ports: {S: d7s7, D: d7s7, G: g7g9d9}
name: M5, type: NMOS, ports: {S: s5, D: g4g5s8, G: d7s7}
name: M14, type: PMOS, ports: {S: VDD, D: d11d14, G: d11d14}
name: M11, type: PMOS, ports: {S: VDD, D: d11d14, G: x2}
name: M6, type: NMOS, ports: {S: GND, D: Vout(A0), G: InN(A0)}
name: Q1, type: PNP, ports: {C: GND, B: GND, E: e1s4}
name: Q2, type: PNP, ports: {C: GND, B: n, E: n}
name: Q3, type: PNP, ports: {C: GND, B: GND, E: GND}
name: R, type: Resistor, value: R, ports: {N1: g4g5s8, N2: n}
name: A0, type: OpAmp, value: A0, ports: {InP: InP(A0), InN: InN(A0), OutP: Vout(A0)}
name: R2, type: Resistor, value: R2, ports: {N1: Vout(A0), N2: GND}
]
extrainfo:This circuit is a V_BE-referenced self-biased reference circuit in CMOS technology. It uses cascoded current mirrors to improve supply rejection. The output voltage V_OUT is given by V_BE + xV_T ln(n). The circuit also includes an operational amplifier (A0) to stabilize the output voltage. The temperature-independent output current can be adjusted by choosing the appropriate temperature coefficient for V_OUT to cancel the temperature coefficient of resistor R2.

Figure 4.50 Example of a $V_{B E}$-referenced self-biased reference circuit in CMOS technology.

## APPENDIX

### A.4.1 MATCHING CONSIDERATIONS IN CURRENT MIRRORS

In many types of circuits, an objective of current-mirror design is generation of two or more current sources whose values are identical. This objective is particularly important in the design of digital-to-analog converters, operational amplifiers, and instrumentation amplifiers. We first examine the factors affecting matching in active current mirrors in bipolar technologies and then in MOS technologies.

### A.4.1.1 BIPOLAR

Consider the bipolar current mirror with two outputs in Fig. 4.51. If the resistors and transistors are identical and the collector voltages are the same, the collector currents will match precisely. However, mismatch in the transistor parameters $\alpha_{F}$ and $I_{S}$ and in the emitter resistors will cause the currents to be unequal. For $Q_{3}$,

$$
\begin{equation*}
V_{T} \ln \frac{I_{C 3}}{I_{S 3}}+\frac{I_{C 3}}{\alpha_{F 3}} R_{3}=V_{B} \tag{4.275}
\end{equation*}
$$

For $Q_{4}$,

$$
\begin{equation*}
V_{T} \ln \frac{I_{C 4}}{I_{S 4}}+\frac{I_{C 4}}{\alpha_{F 4}} R_{4}=V_{B} \tag{4.276}
\end{equation*}
$$

Subtraction of these two equations gives

$$
\begin{equation*}
V_{T} \ln \frac{I_{C 3}}{I_{C 4}}-V_{T} \ln \frac{I_{S 3}}{I_{S 4}}+\frac{I_{C 3}}{\alpha_{F 3}} R_{3}-\frac{I_{C 4}}{\alpha_{F 4}} R_{4}=0 \tag{4.277}
\end{equation*}
$$

image_name:Figure 4.51 Matched bipolar current sources
description:
[
name: Q1, type: NPN, ports: {C: e1, B: e2b1b3b4, E: GND}
name: Q2, type: NPN, ports: {C: C1b2, B: e2b1b3b4, E: e1}
name: Q3, type: NPN, ports: {C: LOAD_IC3, B: e2b1b3b4, E: e3}
name: Q4, type: NPN, ports: {C: LOAD_IC4, B: e2b1b3b4, E: e4}
name: C1b2, type: CurrentSource, value: C1b2, ports: {Np: VCC, Nn: e2b1b3b4}
name: R1, type: Resistor, value: R1, ports: {N1: e1, N2: GND}
name: R3, type: Resistor, value: R3, ports: {N1: e3, N2: GND}
name: R4, type: Resistor, value: R4, ports: {N1: e4, N2: GND}
]
extrainfo:The circuit is a matched bipolar current source configuration. It uses NPN transistors Q1 to Q4 to control the current flow. Current source C1b2 provides the input current IIN. The transistors Q3 and Q4 are configured to drive the LOAD with currents IC3 and IC4 respectively. The base voltage VB is common to Q1, Q2, Q3, and Q4.

Figure 4.51 Matched bipolar current sources.

We now define average and mismatch parameters as follows:

$$
\begin{align*}
I_{C} & =\frac{I_{C 3}+I_{C 4}}{2}  \tag{4.278}\\
\Delta I_{C} & =I_{C 3}-I_{C 4}  \tag{4.279}\\
I_{S} & =\frac{I_{S 3}+I_{S 4}}{2}  \tag{4.280}\\
\Delta I_{S} & =I_{S 3}-I_{S 4}  \tag{4.281}\\
R & =\frac{R_{3}+R_{4}}{2}  \tag{4.282}\\
\Delta R & =R_{3}-R_{4}  \tag{4.283}\\
\alpha_{F} & =\frac{\alpha_{F 3}+\alpha_{F 4}}{2}  \tag{4.284}\\
\Delta \alpha_{F} & =\alpha_{F 3}-\alpha_{F 4} \tag{4.285}
\end{align*}
$$

These relations can be inverted to give the original parameters in terms of the average and mismatch parameters. For example,

$$
\begin{align*}
& I_{C 3}=I_{C}+\frac{\Delta I_{C}}{2}  \tag{4.286}\\
& I_{C 4}=I_{C}-\frac{\Delta I_{C}}{2} \tag{4.287}
\end{align*}
$$

This set of equations for the various parameters is now substituted into (4.277). The result is

$$
\begin{align*}
& V_{T} \ln \left(\frac{I_{C}+\frac{\Delta I_{C}}{2}}{I_{C}-\frac{\Delta I_{C}}{2}}\right)-V_{T} \ln \left(\frac{I_{S}+\frac{\Delta I_{S}}{2}}{I_{S}-\frac{\Delta I_{S}}{2}}\right) \\
&+\frac{\left(I_{C}+\frac{\Delta I_{C}}{2}\right)\left(R+\frac{\Delta R}{2}\right)}{\alpha_{F}+\frac{\Delta \alpha_{F}}{2}}-\frac{\left(I_{C}-\frac{\Delta I_{C}}{2}\right)\left(R-\frac{\Delta R}{2}\right)}{\alpha_{F}-\frac{\Delta \alpha_{F}}{2}}=0 \tag{4.288}
\end{align*}
$$

The first term in this equation can be rewritten as

$$
\begin{equation*}
V_{T} \ln \left(\frac{I_{C}+\frac{\Delta I_{C}}{2}}{I_{C}-\frac{\Delta I_{C}}{2}}\right)=V_{T} \ln \left(\frac{1+\frac{\Delta I_{C}}{2 I_{C}}}{1-\frac{\Delta I_{C}}{2 I_{C}}}\right) \tag{4.289}
\end{equation*}
$$

If $\Delta I_{C} / 2 I_{C} \ll 1$, this term can be rewritten as

$$
\begin{align*}
V_{T} \ln \left(\frac{1+\frac{\Delta I_{C}}{2 I_{C}}}{1-\frac{\Delta I_{C}}{2 I_{C}}}\right) & \simeq V_{T} \ln \left[\left(1+\frac{\Delta I_{C}}{2 I_{C}}\right)\left(1+\frac{\Delta I_{C}}{2 I_{C}}\right)\right]  \tag{4.290}\\
& \simeq V_{T} \ln \left[1+\frac{\Delta I_{C}}{I_{C}}+\left(\frac{\Delta I_{C}}{2 I_{C}}\right)^{2}\right]  \tag{4.291}\\
& \simeq V_{T} \ln \left(1+\frac{\Delta I_{C}}{I_{C}}\right) \tag{4.292}
\end{align*}
$$

where the squared term is neglected. The logarithm function has the infinite series

$$
\begin{equation*}
\ln (1+x)=x-\frac{x^{2}}{2}+\cdots \tag{4.293}
\end{equation*}
$$

If $x \ll 1$,

$$
\begin{equation*}
\ln (1+x) \simeq x \tag{4.294}
\end{equation*}
$$

To simplify (4.292) when $\Delta I_{C} / I_{C} \ll 1$, let $x=\Delta I_{C} / I_{C}$. Then

$$
\begin{equation*}
V_{T} \ln \left(\frac{I_{C}+\frac{\Delta I_{C}}{2}}{I_{C}-\frac{\Delta I_{C}}{2}}\right) \simeq V_{T} \frac{\Delta I_{C}}{I_{C}} \tag{4.295}
\end{equation*}
$$

Applying the same approximations to the other terms in (4.288), we obtain

$$
\begin{equation*}
\frac{\Delta I_{C}}{I_{C}} \simeq\left(\frac{1}{1+\frac{g_{m} R}{\alpha_{F}}}\right) \frac{\Delta I_{S}}{I_{S}}+\frac{\frac{g_{m} R}{\alpha_{F}}}{1+\frac{g_{m} R}{\alpha_{F}}}\left(-\frac{\Delta R}{R}+\frac{\Delta \alpha_{F}}{\alpha_{F}}\right) \tag{4.296}
\end{equation*}
$$

We will consider two important limiting cases. First, since $g_{m}=I_{C} / V_{T}$, when $g_{m} R \ll 1$, the voltage drop on an emitter resistor is much smaller than the thermal voltage. In this case, the second term in (4.296) is small and the mismatch is mainly determined by the transistor $I_{S}$ mismatch in the first term. Observed mismatches in $I_{S}$ typically range from $\pm 10$ to $\pm 1$ percent depending on geometry. Second, when $g_{m} R \gg 1$, the voltage drop on an emitter resistor is much larger than the thermal voltage. In this case, the first term in (4.296) is small and the mismatch is mainly determined by the resistor mismatch and transistor $\alpha_{F}$ mismatch in the second term. Resistor mismatch typically ranges from $\pm 2$ to $\pm 0.1$ percent depending on geometry, and $\alpha_{F}$ matching is in the $\pm 0.1$ percent range for npn transistors. Thus for npn current sources, the use of emitter resistors offers significantly improved current matching. On the other hand, for $p n p$ current sources, the $\alpha_{F}$ mismatch is larger due to the lower $\beta_{F}$, typically around $\pm 1$ percent. Therefore, the advantage of emitter degeneration is less significant with $p n p$ than npn current sources.
image_name:Figure 4.52 Matched MOS current sources
description:
[
name: M1, type: NMOS, ports: {S: GND, D: VDD, G: VGS}
name: M2, type: NMOS, ports: {S: GND, D: VDD, G: VGS}
name: VGS, type: VoltageSource, value: VGS, ports: {Np: VGS, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit consists of matched NMOS current sources M1 and M2, both connected to a common gate voltage VGS and powered by a voltage source VDD. The drain current ID1 and ID2 flow from VDD through M1 and M2 respectively to GND. This configuration is used to achieve matched current sources in MOS analog integrated circuits.

Figure 4.52 Matched MOS current sources.

### A.4.1.2 MOS

Matched current sources are often required in MOS analog integrated circuits. The factors affecting this mismatch can be calculated using the circuit of Fig. 4.52. The two transistors $M_{1}$ and $M_{2}$ will have mismatches in their $W / L$ ratios and threshold voltages. The drain currents are given by

$$
\begin{align*}
& I_{D 1}=\frac{1}{2} \mu_{n} C_{o x}\left(\frac{W}{L}\right)_{1}\left(V_{G S}-V_{t 1}\right)^{2}  \tag{4.297}\\
& I_{D 2}=\frac{1}{2} \mu_{n} C_{o x}\left(\frac{W}{L}\right)_{2}\left(V_{G S}-V_{t 2}\right)^{2} \tag{4.298}
\end{align*}
$$

Defining average and mismatch quantities, we have

$$
\begin{align*}
I_{D} & =\frac{I_{D 1}+I_{D 2}}{2}  \tag{4.299}\\
\Delta I_{D} & =I_{D 1}-I_{D 2}  \tag{4.300}\\
\frac{W}{L} & =\frac{1}{2}\left[\left(\frac{W}{L}\right)_{1}+\left(\frac{W}{L}\right)_{2}\right]  \tag{4.301}\\
\Delta \frac{W}{L} & =\left(\frac{W}{L}\right)_{1}-\left(\frac{W}{L}\right)_{2}  \tag{4.302}\\
V_{t} & =\frac{V_{t 1}+V_{t 2}}{2}  \tag{4.303}\\
\Delta V_{t} & =V_{t 1}-V_{t 2} \tag{4.304}
\end{align*}
$$

Substituting these expressions into (4.297) and (4.298) and neglecting high-order terms, we obtain

$$
\begin{equation*}
\frac{\Delta I_{D}}{I_{D}}=\frac{\Delta \frac{W}{L}}{\frac{W}{L}}-\frac{\Delta V_{t}}{\left(V_{G S}-V_{t}\right) / 2} \tag{4.305}
\end{equation*}
$$

The current mismatch consists of two components. The first is geometry dependent and contributes a fractional current mismatch that is independent of bias point. The second is dependent on threshold voltage mismatch and increases as the overdrive $\left(V_{G S}-V_{t}\right)$ is reduced. This change occurs because as the overdrive is reduced, the fixed threshold mismatch progressively becomes a larger fraction of the total gate drive that is applied to the transistors and therefore contributes a progressively larger percentage error to the current mismatch. In practice, these
image_name:Figure 4.53
description:
[
name: IIN, type: CurrentSource, value: IIN, ports: {Np: VDD, Nn: X1}
name: M, type: NMOS, ports: {S: GND, D: X1, G: X1}
name: M2, type: NMOS, ports: {S: S2, D: X1, G: X1}
name: M3, type: NMOS, ports: {S: S3, D: X1, G: X1}
name: RS1, type: Resistor, value: RS1, ports: {N1: GND, N2: S2}
name: RS2, type: Resistor, value: RS2, ports: {N1: S2, N2: S3}
]
extrainfo:The circuit is a current mirror with two outputs (M2 and M3) sharing the same input current (IIN). The resistors RS1 and RS2 are used for voltage routing. The outputs are labeled as IOUT1 and IOUT2.

Figure 4.53 Current mirror with two outputs used to compare voltage- and current-routing techniques.
observations are important because they affect the techniques used to distribute bias signals on integrated circuits.

Consider the current mirror shown in Fig. 4.53, which has one input and two outputs. At first, assume that $R_{S 1}=R_{S 2}=0$. Also, assume that the input current is generated by a circuit with desirable properties. For example, a self-biased band-gap reference might be used to make $I_{\text {IN }}$ insensitive to changes in the power supply and temperature. Finally, assume that each output current is used to provide the required bias in one analog circuit on the integrated circuit (IC). For example, $M_{2}$ and $M_{3}$ could each act as the tail current source of a differential pair.

One way to build the circuit in Fig. 4.53 is to place $M_{1}$ on the IC near the input current source $I_{\text {IN }}$, while $M_{2}$ and $M_{3}$ are placed near the circuits that they bias, respectively. Since the gate-source voltage of $M_{1}$ must be routed to $M_{2}$ and $M_{3}$ here, this case is referred to as an example of the voltage routing of bias signals. An advantage of this approach is that by routing only two nodes (the gate and the source of $M_{1}$ ) around the IC, any number of output currents can be produced. Furthermore the gains from the input to each output of the current mirror are not affected by the number of outputs in MOS technologies because $\beta_{F} \rightarrow \infty$. (In bipolar technologies, $\beta_{F}$ is finite, and the gain error increases as the number of outputs increase, but a beta-helper configuration can be used to reduce such errors as described in Section 4.2.3.)

Unfortunately, voltage routing has two important disadvantages. First, the input and output transistors in the current mirror may be separated by distances that are large compared to the size of the IC, increasing the potential mismatches in (4.305). In particular, the threshold voltage typically displays considerable gradient with distance across a wafer. Therefore, when the devices are physically separated by large distances, large current mismatch can result from biasing current sources sharing the same gate-source bias, especially when the overdrive is small. The second disadvantage of voltage routing is that the output currents are sensitive to variations in the supply resistances $R_{S 1}$ and $R_{S 2}$. Although these resistances were assumed to be zero above, they are nonzero in practice because of imperfect conduction in the interconnect layers and their contacts. Since $I_{\text {OUT2 }}$ flows in $R_{S 2}$ and ( $I_{\text {OUT1 }}+I_{\text {OUT2 }}$ ) flows in $R_{S 1}$, nonzero resistances cause $V_{G S 2}<V_{G S 1}$ and $V_{G S 3}<V_{G S 1}$ when $I_{\text {OUT1 }}>0$ and $I_{\text {OUT2 }}>0$. Therefore, with perfectly matched transistors, the output currents are less than the input current, and the errors in the output currents can be predicted by an analysis similar to that presented in Section 4.4.1 for Widlar current sources. The key point here is that $R_{S 1}$ and $R_{S 2}$ increase as the distances between the input and output transistors increase, increasing the errors in the output currents. As a result of both of these disadvantages, the output currents may have considerable variation from one IC to another with voltage routing, increasing the difficulty of designing the circuits biased by $M_{2}$ and $M_{3}$ to meet the required specifications even if $I_{\text {IN }}$ is precisely controlled.

To overcome these problems, the circuit in Fig. 4.53 can be built so that $M_{1}-M_{3}$ are close together physically, and the current outputs $I_{\mathrm{OUT} 1}$ and $I_{\mathrm{OUT2}}$ are routed as required on the IC. This case is referred to as an example of the current routing of bias signals. Current routing reduces the problems with mismatch and supply resistance by reducing the distances
image_name:Figure 4.54
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X0, G: X0}
name: M2, type: NMOS, ports: {S: GND, D: X0, G: X0}
name: M3, type: NMOS, ports: {S: GND, D: X0, G: X0}
name: M4, type: PMOS, ports: {S: VDD, D: X1, G: X1}
name: M5, type: PMOS, ports: {S: VDD, D: X2, G: X2}
name: M6, type: NMOS, ports: {S: GND, D: X2, G: X2}
name: M7, type: NMOS, ports: {S: GND, D: I_OUT1, G: X2}
name: M8, type: PMOS, ports: {S: VDD, D: X3, G: X3}
name: M9, type: PMOS, ports: {S: VDD, D: X4, G: X4}
name: M10, type: NMOS, ports: {S: GND, D: X4, G: X4}
name: M11, type: NMOS, ports: {S: GND, D: I_OUT2, G: X4}
name: IIN, type: CurrentSource, value: IIN, ports: {Np: VDD, Nn: X0}
]
extrainfo:The circuit is a bias-distribution circuit utilizing both current and voltage routing. It includes a current routing bus for bias signals, addressing mismatch and supply resistance issues by reducing distances between transistors. The circuit outputs two currents, I_OUT1 and I_OUT2, to separate loads.

Figure 4.54 Bias-distribution circuit using both current routing and voltage routing.
between the input and output transistors in the current mirror in Fig. 4.53 compared to voltage routing. One disadvantage of current routing is that it requires one node to be routed for each bias signal. Therefore, when the number of bias outputs is large, the die area required for the interconnect to distribute the bias currents can be much larger than that required with voltage routing. Another disadvantage of current routing is that it can increase the parasitic capacitance on the drains of $M_{2}$ and $M_{3}$. If these nodes are connected to circuits that process high-frequency signals, increased parasitic capacitance can reduce performance in some ways. For example, if $M_{2}$ and $M_{3}$ act as the tail current sources of differential pairs, increased parasitic capacitance will increase the common-mode gain and reduce the common-mode rejection ratio of each differential pair at high frequencies.

In practice, many ICs use a combination of current- and voltage-routing techniques. For example, Fig. 4.54 shows a circuit with five current mirrors, where the input and output currents are still referenced as in Fig. 4.53. If the current routing bus in Fig. 4.54 travels over a large distance, the parasitic capacitances on the drains of $M_{2}$ and $M_{3}$ may be large. However, the parasitic capacitances on the drains of $M_{7}$ and $M_{11}$ are minimized by using voltage routing within each current mirror. Although simple current mirrors are shown in Fig. 4.54, cascoding is often used in practice to reduce gain errors stemming from a finite Early voltage. In ICs using both current and voltage routing, currents are routed globally and voltages locally, where the difference between global and local routing depends on distance. When the distance is large enough to significantly worsen mismatch or supply-resistance effects, the routing is global. Otherwise, it is local. An effective combination of these bias distribution techniques is to divide an IC into blocks, where bias currents are routed between blocks and bias voltages within the blocks.

### A.4.2 INPUT OFFSET VOLTAGE OF DIFFERENTIAL PAIR WITH ACTIVE LOAD

#### A.4.2.1 BIPOLAR

For the resistively loaded emitter-coupled pair, we showed in Chapter 3 that the input offset voltage arises primarily from mismatches in $I_{S}$ in the input transistors and from mismatches in the collector load resistors. In the active-load case, the input offset voltage results from nonzero
base current of the load devices and mismatches in the input transistors and load devices. Refer to Fig. 4.25a. Assume the inputs are grounded. If the matching is perfect and if $\beta_{F} \rightarrow \infty$ in $T_{3}$ and $T_{4}$,

$$
\begin{equation*}
V_{\text {OUT }}=V_{C C}-\left|V_{B E 3}\right| \tag{4.306}
\end{equation*}
$$

Equation 4.306 holds because only this output voltage forces $V_{C E 3}=V_{C E 4}$, where $I_{C 1}=I_{C 2}$ and $V_{B E 1}=V_{B E 2}$, which is required by KVL when $V_{I 1}=V_{I 2}$.

The differential input required to drive the output to the value given by (4.306) is the inputreferred offset voltage. With finite $\beta_{F}$ in the active-load transistors and/or device mismatch, the offset is usually nonzero. In the active-load, KVL shows that

$$
\begin{equation*}
V_{B E 3}=V_{B E 4} \tag{4.307}
\end{equation*}
$$

Solving (1.58) for $V_{B E 3}$ and $V_{B E 4}$ and substituting in (4.307) gives

$$
\begin{equation*}
\frac{I_{C 3}}{I_{S 3}}\left(\frac{1}{1+\frac{V_{C E 3}}{V_{A 3}}}\right)=\frac{I_{C 4}}{I_{S 4}}\left(\frac{1}{1+\frac{V_{C E 4}}{V_{A 4}}}\right) \tag{4.308}
\end{equation*}
$$

Assume that the Early voltages of $T_{3}$ and $T_{4}$ are identical. Since $V_{C E 3}=V_{C E 4}$ when (4.306) is satisfied, (4.308) can be simplified to

$$
\begin{equation*}
I_{C 4}=I_{C 3}\left(\frac{I_{S 4}}{I_{S 3}}\right) \tag{4.309}
\end{equation*}
$$

Since $I_{C 2}=-I_{C 4}$, (4.309) can be written as

$$
\begin{equation*}
I_{C 2}=-I_{C 3}\left(\frac{I_{S 4}}{I_{S 3}}\right) \tag{4.310}
\end{equation*}
$$

From KCL at the collector of $T_{3}$,

$$
\begin{equation*}
I_{C 1}=-I_{C 3}\left[1+\left(\frac{2}{\beta_{F}}\right)\right] \tag{4.311}
\end{equation*}
$$

where $\beta_{F}$ is the ratio of the collector to base current in the active-load devices. From KVL in the input loop,

$$
\begin{equation*}
V_{I D}=V_{I 1}-V_{I 2}=V_{B E 1}-V_{B E 2} \tag{4.312}
\end{equation*}
$$

Then the input offset voltage, $V_{O S}$, is the value of $V_{I D}$ for which the output voltage is given by (4.306). If the Early voltages of $T_{1}$ and $T_{2}$ are identical, solving (1.58) for $V_{B E 1}$ and $V_{B E 2}$ and substituting into (4.312) gives

$$
\begin{equation*}
V_{O S}=V_{I D}=V_{T} \ln \left(\frac{I_{C 1}}{I_{C 2}} \frac{I_{S 2}}{I_{S 1}}\right) \tag{4.313}
\end{equation*}
$$

because $V_{C E 1}=V_{C E 2}$ when (4.306) is satisfied. Substituting (4.310) and (4.311) in (4.313) gives

$$
\begin{equation*}
V_{O S}=V_{T} \ln \left[\frac{I_{S 3}}{I_{S 4}} \frac{I_{S 2}}{I_{S 1}}\left(1+\frac{2}{\beta_{F}}\right)\right] \tag{4.314}
\end{equation*}
$$

If the mismatches are small, this expression can be approximated as

$$
\begin{equation*}
V_{O S} \simeq V_{T}\left(\frac{\Delta I_{S P}}{I_{S P}}-\frac{\Delta I_{S N}}{I_{S N}}+\frac{2}{\beta_{F}}\right) \tag{4.315}
\end{equation*}
$$

using the technique described in Section 3.5.6.3, where

$$
\begin{align*}
\Delta I_{S P} & =I_{S 3}-I_{S 4}  \tag{4.316}\\
I_{S P} & =\frac{I_{S 3}+I_{S 4}}{2}  \tag{4.317}\\
\Delta I_{S N} & =I_{S 1}-I_{S 2}  \tag{4.318}\\
I_{S N} & =\frac{I_{S 1}+I_{S 2}}{2} \tag{4.319}
\end{align*}
$$

In the derivation of (4.315), we assumed that the Early voltages of matched transistors are identical. In practice, mismatch in Early voltages also contributes to the offset, but the effect is usually negligible when the transistors are biased with collector-emitter voltages much less than their Early voltages.

Assuming a worst-case value for $\Delta I_{S} / I_{S}$ of $\pm 5$ percent and a $p n p$ beta of 20 , the worst-case offset voltage is

$$
\begin{equation*}
V_{O S} \simeq V_{T}(0.05+0.05+0.1)=0.2 V_{T} \simeq 5 \mathrm{mV} \tag{4.320}
\end{equation*}
$$

To find the worst-case offset, we have added the mismatch terms for the pnp and $n p n$ transistors in (4.320) instead of subtracting them as shown in in (4.315) because the mismatch terms are random and independent of each other in practice. Therefore, the polarity of the mismatch terms is unknown in general. Comparing (4.320) to (3.219) shows that the actively loaded differential pair has significantly higher offset than the resistively loaded case under similar conditions. The offset arising here from mismatch in the load devices can be reduced by inserting resistors in series with the emitters of $T_{3}$ and $T_{4}$ as shown in Section A.4.1. To reduce the offset arising from finite $\beta_{F}$ in the load devices, the current mirror in the load can use a beta helper transistor as described in Section 4.2.3.

#### A.4.2.2 MOS

The offset in the CMOS differential pair with active load shown in Fig. $4.25 b$ is similar to the bipolar case. If the matching is perfect with the inputs grounded,

$$
\begin{equation*}
V_{\text {OUT }}=V_{D D}-\left|V_{G S 3}\right| \tag{4.321}
\end{equation*}
$$

Equation 4.321 holds because only this output voltage forces $V_{D S 3}=V_{D S 4}$, where $I_{1}=I_{2}$ and $V_{G S 1}=V_{G S 2}$, which is required by KVL when $V_{I 1}=V_{I 2}$.

The differential input required to drive the output to the value given by (4.321) is the input-referred offset voltage. With device mismatch, the offset is usually nonzero.

$$
\begin{equation*}
V_{I D}=V_{G S 1}-V_{G S 2}=V_{t 1}+V_{o v 1}-V_{t 2}-V_{o v 2} \tag{4.322}
\end{equation*}
$$

Assume that the Early voltages of $T_{1}$ and $T_{2}$ are identical. Since $V_{D S 1}=V_{D S 2}=V_{D S N}$ when $V_{I D}=V_{O S}$, applying (1.165) to $V_{o v 1}$ and $V_{o v 2}$ in (4.322) gives

$$
\begin{equation*}
V_{O S}=V_{t 1}-V_{t 2}+\sqrt{\frac{1}{1+\lambda_{N} V_{D S N}}}\left(\sqrt{\frac{2 I_{1}}{k^{\prime}(W / L)_{1}}}-\sqrt{\frac{2 I_{2}}{k^{\prime}(W / L)_{2}}}\right) \tag{4.323}
\end{equation*}
$$

If the mismatches are small, this expression can be approximated as

$$
\begin{equation*}
V_{O S} \simeq V_{t 1}-V_{t 2}+\frac{V_{o v N}}{2}\left(\frac{\Delta I_{N}}{I_{N}}-\frac{\Delta(W / L)_{N}}{(W / L)_{N}}\right) \tag{4.324}
\end{equation*}
$$

using the technique described in Section 3.5.6.7, where

$$
\begin{equation*}
V_{o v N}=\sqrt{\frac{2 I_{N}}{k^{\prime}(W / L)_{N}\left(1+\lambda_{N} V_{D S N}\right)}} \tag{4.325}
\end{equation*}
$$

$$
\begin{gather*}
\Delta I_{N}=I_{1}-I_{2}  \tag{4.326}\\
I_{N}=\frac{I_{1}+I_{2}}{2}  \tag{4.327}\\
\Delta(W / L)_{N}=(W / L)_{1}-(W / L)_{2}  \tag{4.328}\\
(W / L)_{N}=\frac{(W / L)_{1}+(W / L)_{2}}{2} \tag{4.329}
\end{gather*}
$$

Since $I_{1}=-I_{3}$ and $I_{2}=-I_{4}$

$$
\begin{equation*}
\frac{\Delta I_{N}}{I_{N}}=\frac{\Delta I_{P}}{I_{P}} \tag{4.330}
\end{equation*}
$$

where

$$
\begin{gather*}
\Delta I_{P}=I_{3}-I_{4}  \tag{4.331}\\
I_{P}=\frac{I_{3}+I_{4}}{2} \tag{4.332}
\end{gather*}
$$

To find $\Delta I_{P} / I_{P}$, we will use KVL in the gate-source loop in the load as follows

$$
\begin{equation*}
0=V_{G S 3}-V_{G S 4}=V_{t 3}+V_{o v 3}-V_{t 4}-V_{o v 4} \tag{4.333}
\end{equation*}
$$

Since $T_{3}$ and $T_{4}$ are $p$-channel transistors, their overdrives are negative. Assume that the Early voltages of $T_{3}$ and $T_{4}$ are identical. Since $V_{D S 3}=V_{D S 4}=V_{D S P}$ when $V_{I D}=V_{O S}$ (4.333) can be rewritten as

$$
\begin{equation*}
0=V_{t 3}-V_{t 4}-\sqrt{\frac{1}{1+\left|\lambda_{P} V_{D S P}\right|}}\left(\sqrt{\frac{2\left|I_{3}\right|}{k^{\prime}(W / L)_{3}}}-\sqrt{\frac{2\left|I_{4}\right|}{k^{\prime}(W / L)_{4}}}\right) \tag{4.334}
\end{equation*}
$$

In (4.334), absolute value functions have been used so that the arguments of the square-root functions are positive. If the mismatches are small, this expression can be approximated as

$$
\begin{equation*}
\frac{\Delta I_{P}}{I_{P}} \simeq \frac{V_{t 3}-V_{t 4}}{\frac{\left|V_{o v} P\right|}{2}}+\frac{\Delta(W / L)_{P}}{(W / L)_{P}} \tag{4.335}
\end{equation*}
$$

using the technique described in Section 3.5.6.7, where

$$
\begin{gather*}
\left|V_{o v P}\right|=\sqrt{\frac{2\left|I_{P}\right|}{k^{\prime}(W / L)_{P}\left(1+\left|\lambda_{P} V_{D S P}\right|\right)}}  \tag{4.336}\\
\Delta(W / L)_{P}=(W / L)_{3}-(W / L)_{4}  \tag{4.337}\\
(W / L)_{P}=\frac{(W / L)_{3}+(W / L)_{4}}{2} \tag{4.338}
\end{gather*}
$$

Substituting (4.335) and (4.330) into (4.324) gives

$$
\begin{equation*}
V_{O S} \simeq V_{t 1}-V_{t 2}+\frac{V_{o v N}}{2}\left(\frac{V_{t 3}-V_{t 4}}{\frac{\left|V_{o v}\right|}{2}}+\frac{\Delta(W / L)_{P}}{(W / L)_{P}}-\frac{\Delta(W / L)_{N}}{(W / L)_{N}}\right) \tag{4.339}
\end{equation*}
$$

Comparing (4.339) to (4.315) shows that the MOS differential pair with active load includes terms to account for threshold mismatch but excludes a term to account for finite beta in the active load because $\beta_{F} \rightarrow \infty$ in MOS transistors.

#### EXAMPLE

Find the input-referred offset voltage of the circuit in Fig. $4.25 b$ using the transistor parameters in the table below.

| Transistor | $V_{t}(V)$ | $W(\mu \mathrm{~m})$ | $L(\mu \mathrm{~m})$ | $k^{\prime}\left(\mu \mathrm{A} / \mathrm{V}^{2}\right)$ |
| :---: | :---: | :---: | :---: | :---: |
| $T_{1}$ | 0.705 | 49 | 1 | 100 |
| $T_{2}$ | 0.695 | 51 | 1 | 100 |
| $T_{3}$ | -0.698 | 103 | 1 | 50 |
| $T_{4}$ | -0.702 | 97 | 1 | 50 |

Assume that $I_{\text {TAIL }}=200 \mu \mathrm{~A}$ and that $\lambda_{N} V_{D S N} \ll 1$ and $\left|\lambda_{P} V_{D S P}\right| \ll 1$. From (4.327) and KCL,

$$
\begin{equation*}
I_{N}=\frac{I_{1}+I_{2}}{2}=\frac{I_{\mathrm{TAIL}}}{2}=100 \mu \mathrm{~A} \tag{4.340}
\end{equation*}
$$

Substituting (4.340) and (4.329) into (4.325) gives

$$
\begin{equation*}
V_{o v N} \simeq \sqrt{\frac{200}{100(49+51) / 2}} \mathrm{~V}=0.2 \mathrm{~V} \tag{4.341}
\end{equation*}
$$

Similarly, from (4.332) and KCL

$$
\begin{equation*}
I_{P}=\frac{I_{3}+I_{4}}{2}=-\frac{I_{\mathrm{TAIL}}}{2}=-100 \mu \mathrm{~A} \tag{4.342}
\end{equation*}
$$

Substituting (4.342) and (4.338) into (4.336) gives

$$
\begin{equation*}
\left|V_{o v P}\right| \simeq \sqrt{\frac{200}{50(103+97) / 2}} \mathrm{~V}=0.2 \mathrm{~V} \tag{4.343}
\end{equation*}
$$

Substituting (4.337) and (4.328) into (4.339) gives

$$
\begin{align*}
V_{O S} \simeq & 0.705 \mathrm{~V}-0.695 \mathrm{~V} \\
& +0.1\left(\frac{-0.698+0.702}{0.1}+\frac{103-97}{(103+97) / 2}-\frac{49-51}{(49+51) / 2}\right) \mathrm{V} \\
\simeq & 0.01 \mathrm{~V}+0.1(0.04+0.06+0.04) \mathrm{V}=0.024 \mathrm{~V} \tag{4.344}
\end{align*}
$$

In this example, the mismatches have been chosen so that the individual contributions to the offset add constructively to give the worst-case offset.
