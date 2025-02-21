# 5. Output Stages

## 5.1 Introduction

The output stage of an amplifier must satisfy a number of special requirements. One of the most important requirements is to deliver a specified amount of signal power to a load with acceptably low levels of signal distortion. Another common objective of output-stage design is to minimize the output impedance so that the voltage gain is relatively unaffected by the value of load impedance. A well-designed output stage should achieve these performance specifications while consuming low quiescent power and, in addition, should not be a major limitation on the frequency response of the amplifier.

In this chapter, several output-stage configurations will be considered to satisfy the above requirements. The simplest output-stage configurations are the emitter and source followers. More complex output stages employing multiple output devices are also treated, and comparisons are made of power-output capability and efficiency.

Because of their excellent current-handling capability, bipolar transistors are the preferred devices for use in output stages. Although parasitic bipolar transistors can be used in some CMOS output stages, output stages in CMOS technologies are usually constructed without bipolar transistors and are also described in this chapter.

## 5.2 The Emitter Follower as an Output Stage

An emitter-follower output stage is shown in Fig. 5.1. To simplify the analysis, positive and negative bias supplies of equal magnitude $V_{C C}$ are assumed, although these supplies may have different values in practice. When output voltage $V_{o}$ is zero, output current $I_{o}$ is also zero. The emitter-follower output device $Q_{1}$ is biased to a quiescent current $I_{Q}$ by current source $Q_{2}$. The output stage is driven by voltage $V_{i}$, which has a quiescent dc value of $V_{b e 1}$ for $V_{o}=0 \mathrm{~V}$. The bias components $R_{1}, R_{3}$, and $Q_{3}$ can be those used to bias other stages in the circuit. Since the quiescent current $I_{Q}$ in $Q_{2}$ will usually be larger than the reference current $I_{R}$, resistor $R_{2}$ is usually smaller than $R_{1}$ to accommodate this difference.

This circuit topology can also be implemented in CMOS technologies using an MOS current source for bias and the parasitic bipolar-transistor emitter follower available in standard CMOS processes. Because any large current flow to the substrate can initiate the pnpn latch-up phenomenon described in Chapter 2, however, this configuration should be used carefully in CMOS technologies with lightly doped substrates. Extensive substrate taps in the vicinity of the emitter follower are essential to collect the substrate current flow.

### 5.2.1 Transfer Characteristics of the Emitter-Follower

The circuit of Fig. 5.1 must handle large signal amplitudes; that is, the current and voltage swings resulting from the presence of signals may be a large fraction of the bias values. As
image_name:Figure 5.1 Emitter-follower output stage with current-mirror bias
description:
[
name: Q1, type: NPN, ports: {C: VCC, B: Vi, E: e1c2}
name: Q2, type: NPN, ports: {C: e1c2, B: b2a3, E: e2}
name: Q3, type: Diode, ports: {Na: b2a3, Nc:k3}
name: R1, type: Resistor, value: R1, ports: {N1: k3, N2: -VCC}
name: R2, type: Resistor, value: R2, ports: {N1: e2, N2: -VCC}
name: R3, type: Resistor, value: R3, ports: {N1: q2a3, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: e1c2, N2: GND}
]
extrainfo:The circuit is an emitter-follower output stage with current-mirror bias. It uses three NPN transistors (Q1, Q2, Q3) and four resistors (R1, R2, R3, RL). The input voltage Vi is fed into the base of Q1, and the output voltage Vo is taken across RL. The circuit is biased with VCC and -VCC voltages. Q3 is used as a current mirror to provide biasing current for Q2.

Figure 5.1 Emitter-follower output stage with current-mirror bias.
a result, the small-signal analyses that have been used extensively up to this point must be used with care in this situation. For this reason, we first determine the dc transfer characteristic of the emitter follower. This characteristic allows calculation of the gain of the circuit and also gives important information on the linearity and thus on the distortion performance of the stage.

Consider the circuit of Fig. 5.1. The large-signal transfer characteristic can be derived as follows:

$$
\begin{equation*}
V_{i}=V_{b e 1}+V_{o} \tag{5.1}
\end{equation*}
$$

In this case, the base-emitter voltage $V_{b e 1}$ of $Q_{1}$ cannot be assumed constant but must be expressed in terms of the collector current $I_{c 1}$ of $Q_{1}$ and the saturation current $I_{S}$. If the load resistance $R_{L}$ is small compared with the output resistance of the transistors,

$$
\begin{equation*}
V_{b e 1}=\frac{k T}{q} \ln \left(\frac{I_{c 1}}{I_{S}}\right) \tag{5.2}
\end{equation*}
$$

if $Q_{1}$ is in the forward-active region. Also

$$
\begin{equation*}
I_{c 1}=I_{Q}+\frac{V_{o}}{R_{L}} \tag{5.3}
\end{equation*}
$$

if $Q_{2}$ is in the forward-active region and $\beta_{F}$ is assumed large. Substitution of (5.3) and (5.2) in (5.1) gives

$$
\begin{equation*}
V_{i}=\frac{k T}{q} \ln \left(\frac{I_{Q}+\frac{V_{o}}{R_{L}}}{I_{S}}\right)+V_{o} \tag{5.4}
\end{equation*}
$$

Equation 5.4 is a nonlinear equation relating $V_{o}$ and $V_{i}$ if both $Q_{1}$ and $Q_{2}$ are in the forwardactive region.

The transfer characteristic from (5.4) has been plotted in Fig. 5.2. First, consider the case where $R_{L}$ is large, which is labeled $R_{L 1}$. In this case, the first term on the right-hand side of (5.4), which represents the base-emitter voltage $V_{b e 1}$ of $Q_{1}$, is almost constant as $V_{o}$ changes. This result stems from the observation that the current in the load is small for a large $R_{L}$;
image_name:Figure 5.2
description:The graph in Figure 5.2 is a transfer characteristic plot showing the relationship between the output voltage \(V_o\) and the input voltage \(V_i\) for a circuit with transistors \(Q_1\) and \(Q_2\). The graph is plotted with \(V_o\) on the vertical axis and \(V_i\) on the horizontal axis.

Axes Labels and Units:
- **Vertical Axis (\(V_o\))**: Represents the output voltage.
- **Horizontal Axis (\(V_i\))**: Represents the input voltage.

Overall Behavior and Trends:
The graph displays different regions based on the operation of transistors \(Q_1\) and \(Q_2\):
1. **Region where \(Q_2\) is saturated**: At low input voltages, \(Q_2\) is saturated, and the output voltage \(V_o\) is approximately equal to \(-V_{CC} + V_{CE2(sat)}\).
2. **Linear Region**: As \(V_i\) increases, the graph shows a linear region with a slope of unity. This occurs when both transistors are in the forward-active region, and \(Q_1\) is not yet saturated.
3. **Region where \(Q_1\) is saturated**: At higher input voltages, \(Q_1\) becomes saturated, and the output voltage levels off at \(V_{CC} - V_{CE1(sat)}\).

Key Features and Technical Details:
- The linear region is offset on the \(V_i\) axis by \(V_{BE1}\), the base-emitter voltage of \(Q_1\).
- The graph includes specific points such as \([-V_{CC} + V_{CE1(sat)} + V_{be1}]\), \(V_{BE1}\), and \((V_{CC} - V_{CE1(sat)} + V_{be1})\).
- The transition points between the regions are marked by dashed lines, indicating the points where \(Q_1\) cuts off and where \(Q_1\) becomes saturated.

Annotations and Specific Data Points:
- The point \(V_{BE1}\) is marked, indicating the quiescent value of the base-emitter voltage.
- The graph includes annotations such as \(Q_1\) cutoff and \(Q_1\) saturated, highlighting the operational regions of the transistors.
- Load resistances are marked as \(R_{L1}\) and \(R_{L2}\), affecting the slope and offset of the linear region.

This transfer characteristic plot illustrates how varying the input voltage \(V_i\) affects the output voltage \(V_o\) across different operating conditions of the transistors, providing insight into the circuit's behavior under varying load resistances.

Figure 5.2 Transfer characteristic of the circuit of Fig. 5.1 for a low $\left(R_{L 2}\right)$ and a high ( $R_{L 1}$ ) value of load resistance.
therefore, the current in $Q_{1}$ and $V_{b e 1}$ are both almost constant as $V_{o}$ changes in this case. As a result, the center part of the transfer characteristic for $R_{L}=R_{L 1}$ is nearly a straight line with unity slope that is offset on the $V_{i}$ axis by $V_{B E 1}$, the quiescent value of $V_{b e 1}$. This near-linear region depends on both $Q_{1}$ and $Q_{2}$ being in the forward-active region. However, as $V_{i}$ is made large positive or negative, one of these devices saturates and the transfer characteristic abruptly changes slope.

Consider $V_{i}$ made large and positive. Output voltage $V_{o}$ follows $V_{i}$ until $V_{o}=V_{C C}-$ $V_{C E 1 \text { (sat) }}$ at which point $Q_{1}$ saturates. The collector-base junction of $Q_{1}$ is then forward biased and large currents flow from base to collector. In practice, the transistor base resistance (and any source resistance present) limit the current in the forward-biased collector-base junction and prevent the voltage at the internal transistor base from rising appreciably higher. Further increases in $V_{i}$ thus produce little change in $V_{o}$ and the characteristic flattens out, as shown in Fig. 5.2. The value of $V_{i}$ required to cause this behavior is slightly larger than the supply voltage because $V_{b e 1}$ is larger than the saturation voltage $V_{C E(\text { sat })}$. Consequently, the preceding stage often limits the maximum positive output voltage in a practical circuit because a voltage larger than $V_{C C}$ usually cannot be generated at the base of the output stage. (The portion of the curve for $V_{i}$ large positive where $Q_{1}$ is saturated actually has a positive slope if the effect of the collector series resistance $r_{c}$ of $Q_{1}$ is included. In any event, this portion of the transfer characteristic must be avoided, because the saturation of $Q_{1}$ results in large nonlinearity and a major reduction of power gain.)

Now consider $V_{i}$ made large and negative. The output voltage follows the input until $V_{o}=-V_{C C}+V_{C E 2 \text { (sat) }}$, at which point $Q_{2}$ saturates. (The voltage drop across $R_{2}$ is assumed small and is neglected. It could be lumped in with the saturation voltage $V_{C E 2 \text { (sat) }}$ of $Q_{2}$ if necessary.) When $Q_{2}$ saturates, another discontinuity in the transfer curve occurs, and the slope abruptly decreases. For acceptable distortion performance in the circuit, the voltage swing must be limited to the region between these two break points. As mentioned above, the driver stage supplying $V_{i}$ usually cannot produce values of $V_{i}$ that have a magnitude exceeding $V_{C C}$ (if it is connected to the same supply voltages) and the driver itself then sets the upper limit.

Next consider the case where $R_{L}$ in Fig. 5.1 has a relatively small value. Then when $V_{o}$ is made large and negative, the first term in (5.4) can become large. In particular, this term
image_name:(a)
description:The graph labeled "(a)" represents an AC input voltage waveform plotted against time. It is a time-domain waveform.

1. **Axes Labels and Units:**
- The horizontal axis represents time, denoted as 't'.
- The vertical axis represents the AC input voltage, labeled as 'ac input voltage'.

2. **Overall Behavior and Trends:**
- The graph shows two sinusoidal waveforms. The waveforms are periodic and exhibit oscillatory behavior.
- The first waveform, labeled as ①, has a smaller amplitude and is nested within the second waveform, labeled as ②, which has a larger amplitude.
- Both waveforms are symmetrical around the horizontal axis, indicating that they have no DC offset.

3. **Key Features and Technical Details:**
- The waveform ① reaches a peak at voltage level \(V_1\) and a trough at \(-V_1\).
- The waveform ② reaches a peak at voltage level \(V_2\) and a trough at \(-V_2\), showing that it has a greater amplitude than waveform ①.
- There are no annotations for phase shifts or frequency values, but the periodic nature suggests a consistent frequency for both waveforms.

4. **Annotations and Specific Data Points:**
- The graph includes horizontal dashed lines indicating the voltage levels \(V_1\), \(-V_1\), \(V_2\), and \(-V_2\).
- The waveforms are labeled with numbers ① and ② to distinguish between the two.
image_name:(b)
description:The graph labeled (b) is a time-domain waveform graph depicting the AC output voltage as a function of time (t). The horizontal axis represents time, while the vertical axis represents the AC output voltage. The scale appears to be linear, and there are significant markers on the voltage axis at levels $V_1$, $V_2$, $-V_1$, $-V_2$, and $-I_Q R_{L2}$.

1. **Type of Graph and Function:**
- This is a time-domain waveform graph showing the behavior of AC output voltage over time.

2. **Axes Labels and Units:**
- **Horizontal Axis (x-axis):** Represents time (t).
- **Vertical Axis (y-axis):** Represents AC output voltage.
- The voltage scale is marked at specific points: $V_1$, $V_2$, $-V_1$, $-V_2$, and $-I_Q R_{L2}$.

3. **Overall Behavior and Trends:**
- The waveform shows a periodic oscillation, similar to a sine wave, but with noticeable clipping at the negative peaks.
- The positive peaks of the waveform reach up to $V_2$, while the negative peaks are clipped at $-I_Q R_{L2}$, indicating a distortion in the waveform.
- The waveform is symmetric around the time axis, but the clipping causes the negative half to flatten at the bottom.

4. **Key Features and Technical Details:**
- The waveform clipping occurs at the negative peaks, specifically marked with the label "Waveform clipping."
- The clipping level at $-I_Q R_{L2}$ suggests that the circuit is unable to produce output voltages below this threshold, likely due to the current limitations described in the context.
- The waveform maintains its sinusoidal shape on the positive side but is distorted on the negative side due to the clipping.

5. **Annotations and Specific Data Points:**
- The graph is annotated with voltage levels $V_1$ and $V_2$ for reference.
- The clipping level is explicitly marked at $-I_Q R_{L2}$.
- The annotations indicate two different input signal levels (1 and 2) corresponding to different amplitudes in the input waveform shown in graph (a).

Figure 5.3 (a) ac input signals applied to the circuit of Fig. 5.1. (b) ac output waveforms corresponding to the inputs in (a) with $R_{L}=R_{L 2}$.
approaches minus infinity when $V_{o}$ approaches the critical value

$$
\begin{equation*}
V_{o}=-I_{Q} R_{L} \tag{5.5}
\end{equation*}
$$

In this situation, the current drawn from the load $\left(-V_{o} / R_{L}\right)$ is equal to the current $I_{Q}$, and device $Q_{1}$ cuts off, leaving $Q_{2}$ to draw the current $I_{Q}$ from the load. Further decreases in $V_{i}$ produce no change in $V_{o}$, and the transfer characteristic is the one labeled $R_{L 2}$ in Fig. 5.2. The transfer characteristic for positive $V_{i}$ is similar for both cases.

For the case $R_{L}=R_{L 2}$, the stage will produce severe waveform distortion if $V_{i}$ is a sinusoid with amplitude exceeding $I_{Q} R_{L 2}$. Consider the two sinusoidal waveforms in Fig. 5.3a. Waveform (1) has an amplitude $V_{1}<I_{Q} R_{L 2}$ and waveform (2) has an amplitude $V_{2}>I_{Q} R_{L 2}$. If these signals are applied as inputs at $V_{i}$ in Fig. 5.1 (together with a bias voltage), the output waveforms that result are as shown in Fig. $5.3 b$ for $R_{L}=R_{L 2}$. For the smaller input signal, the circuit acts as a near-linear amplifier and the output is near sinusoidal. The output waveform distortion, which is apparent for the larger input, is termed "clipping" and must be avoided in normal operation of the circuit as a linear output stage. For a given $I_{Q}$ and $R_{L}$, the onset of clipping limits the maximum signal that can be handled. Note that if $I_{Q} R_{L}$ is larger than $V_{C C}$, the situation shown for $R_{L}=R_{L 1}$ in Fig. 5.2 holds, and the output voltage can swing almost to the positive and negative supply voltages before excessive distortion occurs.

### 5.2.2 Power Output and Efficiency

Further insight into the operation of the circuit of Fig. 5.1 can be obtained from Fig. 5.4 where three different load lines are drawn on the $I_{c}-V_{c e}$ characteristics of $Q_{1}$. The equation for the
image_name:Figure 5.4
description:Figure 5.4 illustrates the load lines on the $I_{c1}-V_{ce1}$ plane for the emitter follower $Q_{1}$ from Fig. 5.1. This graph is a characteristic plot showing the relationship between the collector current ($I_{c1}$) on the vertical axis and the collector-emitter voltage ($V_{ce1}$) on the horizontal axis.

1. **Type of Graph and Function:**
- The graph is a plot of transistor characteristics, specifically showing load lines for different load resistances ($R_L$) on the $I_{c1}-V_{ce1}$ plane.

2. **Axes Labels and Units:**
- **Vertical Axis:** $I_{c1}$ (Collector Current)
- **Horizontal Axis:** $V_{ce1}$ (Collector-Emitter Voltage)
- No specific units are mentioned, but these typically would be in amperes for current and volts for voltage.

3. **Overall Behavior and Trends:**
- The graph shows several load lines corresponding to different values of load resistance ($R_L = R_{L1}, R_{L2}, R_{L3}$).
- These load lines are linear and intersect at the quiescent point $Q$ where $I_{c1} = I_Q$ and $V_{ce1} = V_{CC}$.
- The curves of constant $V_{be1}$ are also shown, which indicate the boundaries of the transistor's operation.

4. **Key Features and Technical Details:**
- Quiescent Point $Q$: This is where the transistor operates with no input signal, at $I_{c1} = I_Q$ and $V_{ce1} = V_{CC}$.
- Maximum Power Points: The graph marks the maximum power points for each load line ($P_{L\max}$ for $R_{L1}$, $R_{L2}$, and $R_{L3}$).
- Saturation and Maximum Voltage: The leftmost point on the load lines corresponds to $V_{CE1}(sat)$, indicating saturation. The maximum possible value of $V_{ce1}$ is annotated as $[2V_{CC} - V_{CE2}(sat)]$.

5. **Annotations and Specific Data Points:**
- Points A, B, C indicate specific operational points on the load lines.
- The shaded areas represent the region of maximum power dissipation for each load resistance.
- The diagram includes annotations for the values of $V_{CC}$ and $V_{CC} + I_Q R_{L2}$, marking significant voltage levels.

Overall, this graph provides a detailed view of how different load resistances affect the operation of the transistor in terms of current and voltage, highlighting the impact on power output and efficiency.

Figure 5.4 Load lines in the $I_{c 1}-V_{c e 1}$ plane for emitter follower $Q_{1}$ of Fig. 5.1.
load lines can be written from Fig. 5.1 and is

$$
\begin{equation*}
V_{c e 1}=V_{C C}-\left(I_{c 1}-I_{Q}\right) R_{L} \tag{5.6}
\end{equation*}
$$

when both $Q_{1}$ and $Q_{2}$ are in the forward-active region. The values of $V_{c e 1}$ and $I_{c 1}$ are related by (5.6) for any value of $V_{i}$ and the line includes the quiescent point $Q$, where $I_{c 1}=I_{Q}$ and $V_{c e 1}=V_{C C}$. Equation 5.6 is plotted in Fig. 5.4 for load resistances $R_{L 1}, R_{L 2}$, and $R_{L 3}$ and the device operating point moves up and down these lines as $V_{i}$ varies. As $V_{i}$ increases and $V_{c e 1}$ decreases, $Q_{1}$ eventually saturates, as was illustrated in Fig. 5.2. As $V_{i}$ decreases and $V_{c e 1}$ increases, there are two possibilities as described above. If $R_{L}$ is large ( $\left.R_{L 1}\right), V_{o}$ decreases and $V_{c e 1}$ increases until $Q_{2}$ saturates. Thus the maximum possible value that $V_{c e 1}$ can attain is [ $\left.2 V_{C C}-V_{C E 2 \text { (sat) }}\right]$ and this value is marked on Fig. 5.4. However, if $R_{L}$ is small $\left(R_{L 2}\right)$, the maximum negative value of $V_{o}$ as illustrated in Fig. 5.2 is $-I_{Q} R_{L 2}$ and the maximum possible value of $V_{c e 1}$ is $\left(V_{C C}+I_{Q} R_{L 2}\right)$.

Thus far no mention has been made of the maximum voltage limitations of the output stage. As described in Chapter 1, avalanche breakdown of a bipolar transistor occurs for $V_{c e}=B V_{C E O}$ in the common-emitter configuration, which is the worst case for breakdown voltage. In a conservative design, the value of $V_{c e}$ in the circuit of Fig. 5.1 should always be less than $B V_{C E O}$ by an appropriate safety margin. In the preceding analysis, the maximum value that $V_{c e 1}$ can attain in this circuit for any load resistance was calculated as approximately $2 V_{C C}$, and thus $B V_{C E O}$ must be greater than this value.

Consider now the power relationships in the circuit. When sinusoidal signals are present, the power dissipated in various elements varies with time. We are concerned both with the instantaneous power dissipated and with the average power dissipated. Instantaneous power
is important when considering transistor dissipation with low-frequency or dc signals. The junction temperature of the transistor will tend to rise and fall with the instantaneous power dissipated in the device, limiting the maximum allowable instantaneous power dissipation for safe operation of any device.

Average power levels are important because the power delivered to a load is usually specified as an average value. Also note that if an output stage handles only high-frequency signals, the transistor junction temperature will not vary appreciably over a cycle and the average device power dissipation will then be the limiting quantity.

Consider the output signal power that can be delivered to load $R_{L}$ when a sinusoidal input is applied at $V_{i}$. Assuming that $V_{o}$ is approximately sinusoidal, the average output power delivered to $R_{L}$ is

$$
\begin{equation*}
P_{L}=\frac{1}{2} \hat{V}_{o} \hat{I}_{o} \tag{5.7}
\end{equation*}
$$

where $\hat{V}_{o}$ and $\hat{I}_{o}$ are the amplitudes (zero to peak) of the output sinusoidal voltage and current. As described previously, the maximum output signal amplitude that can be attained before clipping occurs depends on the value of $R_{L}$. If $\left.P_{L}\right|_{\max }$ is the maximum value of $P_{L}$ that can be attained before clipping occurs with sinusoidal signals, then

$$
\begin{equation*}
\left.P_{L}\right|_{\max }=\frac{1}{2} \hat{V}_{o m} \hat{I}_{o m} \tag{5.7a}
\end{equation*}
$$

where $\hat{V}_{o m}$ and $\hat{I}_{o m}$ are the maximum values of $\hat{V}_{o}$ and $\hat{I}_{o}$ that can be attained before clipping.
Consider the case of the large load resistance, $R_{L 1}$. Figures 5.2 and 5.4 show that clipping occurs symmetrically in this case, and we have

$$
\begin{equation*}
\hat{V}_{o m}=V_{C C}-V_{C E(\mathrm{sat})} \tag{5.8}
\end{equation*}
$$

assuming equal saturation voltages in $Q_{1}$ and $Q_{2}$. The corresponding sinusoidal output current amplitude is $\hat{I}_{o m}=\hat{V}_{o m} / R_{L 1}$. The maximum average power that can be delivered to $R_{L 1}$ is calculated by substituting these values in (5.7a). This value of power can be interpreted geometrically as the area of the triangle $A$ in Fig. 5.4 since the base of the triangle equals $\hat{V}_{o m}$ and its height is $\hat{I}_{o m}$. As $R_{L 1}$ is increased, the maximum average output power that can be delivered diminishes because the triangle becomes smaller. The maximum output voltage amplitude remains essentially the same but the current amplitude decreases as $R_{L 1}$ increases.

If $R_{L}=R_{L 2}$ in Fig. 5.4, the maximum output voltage swing before clipping occurs is

$$
\begin{equation*}
\hat{V}_{o m}=I_{Q} R_{L 2} \tag{5.9}
\end{equation*}
$$

The corresponding current amplitude is $\hat{I}_{o m}=I_{Q}$. Using (5.7a), the maximum average output power $\left.P_{L}\right|_{\text {max }}$ that can be delivered is given by the area of triangle $B$, shown in Fig. 5.4. As $R_{L 2}$ is decreased, the maximum average power that can be delivered is diminished.

An examination of Fig. 5.4 shows that the power-output capability of the stage is maxi$\operatorname{mized}$ for $R_{L}=R_{L 3}$, which can be calculated from (5.6) and Fig. 5.4 as

$$
\begin{equation*}
R_{L 3}=\frac{V_{C C}-V_{C E(\mathrm{sat})}}{I_{Q}} \tag{5.10}
\end{equation*}
$$

This load line gives the triangle of largest area $(C)$ and thus the largest average output power. In this case, $\hat{V}_{o m}=\left[V_{C C}-V_{C E(\mathrm{sat})}\right]$ and $\hat{I}_{o m}=I_{Q}$. Using (5.7a), we have

$$
\begin{equation*}
\left.P_{L}\right|_{\max }=\frac{1}{2} \hat{V}_{o m} \hat{I}_{o m}=\frac{1}{2}\left[V_{C C}-V_{C E(\mathrm{sat})}\right] I_{Q} \tag{5.11}
\end{equation*}
$$

To calculate the efficiency of the circuit, the power drawn from the supply voltages must now be calculated. The current drawn from the positive supply is the collector current of $Q_{1}$,
which is assumed sinusoidal with an average value $I_{Q}$. The current flowing in the negative supply is constant and equal to $I_{Q}$ (neglecting bias current $I_{R}$ ). Since the supply voltages are constant, the average power drawn from the supplies is constant and independent of the presence of sinusoidal signals in the circuit. The total power drawn from the two supplies is thus

$$
\begin{equation*}
P_{\text {supply }}=2 V_{C C} I_{Q} \tag{5.12}
\end{equation*}
$$

The power conversion efficiency $\left(\eta_{C}\right)$ of the circuit at an arbitrary output power level is defined as the ratio of the average power delivered to the load to the average power drawn from the supplies.

$$
\begin{equation*}
\eta_{C}=\frac{P_{L}}{P_{\text {supply }}} \tag{5.13}
\end{equation*}
$$

Since the power drawn from the supplies is constant in this circuit, the efficiency increases as the output power increases. Also, since the previous analysis shows that the power-output capability of the circuit depends on the value of $R_{L}$, the efficiency also depends on $R_{L}$. The best efficiency occurs for $R_{L}=R_{L 3}$ since this value gives maximum average power output. If $R_{L}=R_{L 3}$ and $\hat{V}_{o}=\hat{V}_{o m}$, then substitution of (5.11) and (5.12) in (5.13) gives for the maximum possible efficiency

$$
\begin{equation*}
\eta_{\max }=\frac{1}{4}\left(1-\frac{V_{C E(\mathrm{sat})}}{V_{C C}}\right) \tag{5.14}
\end{equation*}
$$

Thus if $V_{C E(\text { sat })} \ll V_{C C}$, the maximum efficiency of the stage is $1 / 4$ or 25 percent.
Another important aspect of circuit performance is the power dissipated in the active device. The current and voltage waveforms in $Q_{1}$ at maximum signal swing and with $R_{L}=R_{L 3}$ are shown in Fig. 5.5 (assuming $V_{C E(\text { sat })} \simeq 0$ for simplicity) together with their product, which
image_name:(a)
description:The graph labeled "(a)" is a time-domain waveform depicting the collector-emitter voltage ($V_{ce1}$) of a transistor as a function of time ($t$). The vertical axis represents the voltage in volts, and the horizontal axis represents time. The waveform is sinusoidal, indicating periodic variations in the voltage.

1. **Axes Labels and Units:**
- **Vertical Axis:** $V_{ce1}$, with a scale indicating voltage levels. The maximum voltage is marked as $2V_{CC}$, and the quiescent voltage level is labeled as $V_{CC}$.
- **Horizontal Axis:** Time ($t$), with no specific units marked, suggesting a linear time scale.

2. **Overall Behavior and Trends:**
- The waveform is sinusoidal, indicating a periodic oscillation of the collector-emitter voltage.
- The peak voltage reaches $2V_{CC}$, and the minimum voltage drops to zero.
- The waveform oscillates symmetrically around the quiescent voltage level $V_{CC}$.

3. **Key Features and Technical Details:**
- The amplitude of oscillation above the quiescent level is denoted as $\hat{V}_{om}$.
- The waveform completes a full cycle, showing the rise and fall of voltage from $V_{CC}$ to $2V_{CC}$ and back to zero.
- The oscillation frequency appears to be twice the signal frequency, consistent with the context provided about power dissipation.

4. **Annotations and Specific Data Points:**
- The quiescent voltage level is indicated by a horizontal dashed line at $V_{CC}$.
- The peak voltage is marked by another dashed line at $2V_{CC}$.
- Vertical dashed lines indicate points of interest where the waveform crosses the quiescent voltage level and reaches its peaks.

This graph illustrates how the collector-emitter voltage varies over time, showing the dynamic behavior of the transistor in response to changes in input signal and load conditions.
image_name:(b)
description:The graph labeled (b) is a time-domain waveform representing the collector current ($I_{c1}$) of a transistor $Q_{1}$ at full output with $R_{L} = R_{L3}$. The horizontal axis is time ($t$), and the vertical axis is the collector current ($I_{c1}$) with a specific focus on its variation over time.

**Axes Labels and Units:**
- **Horizontal Axis:** Time ($t$), typically in seconds or milliseconds, though units are not explicitly mentioned.
- **Vertical Axis:** Collector current ($I_{c1}$), with annotations for specific current values.

**Overall Behavior and Trends:**
The waveform is sinusoidal, indicating periodic behavior typical of AC signals. It oscillates around a quiescent current level ($I_Q$), with the amplitude of oscillation reaching a peak at $2I_Q$. This suggests that the current varies symmetrically above and below the quiescent level, indicating a full signal swing.

**Key Features and Technical Details:**
- **Quiescent Current ($I_Q$):** The baseline level around which the current oscillates.
- **Peak Current ($2I_Q$):** The maximum amplitude of the current waveform, reached at the peaks of the sinusoidal wave.
- **Amplitude of Oscillation ($\hat{I}_{om}$):** The difference between the peak current and the quiescent level, representing the maximum deviation from the quiescent current.

**Annotations and Specific Data Points:**
- The waveform is annotated with dashed lines indicating the quiescent current level and the peak current ($2I_Q$).
- The peaks and troughs of the waveform are symmetric about the quiescent level, suggesting that the transistor is operating in a balanced mode with equal positive and negative swings.
image_name:(c)
description:The graph labeled "(c)" is a time-domain waveform depicting the instantaneous power dissipation in the transistor $Q_{1}$ as a function of time. The x-axis represents time ($t$) and is linear, while the y-axis represents power dissipation ($P_{c1}$), which is the product of the collector current ($I_{c1}$) and the collector-emitter voltage ($V_{ce1}$).

The waveform is sinusoidal, indicating that the power dissipation varies periodically over time. The frequency of this waveform is twice that of the signal frequency, as suggested by the context. This is characteristic of power dissipation in such circuits, where the power waveform oscillates at twice the frequency of the voltage or current waveforms.

The graph shows peaks and valleys, with the maximum power dissipation occurring at the peaks and the minimum at the valleys. The average power dissipation is indicated as half of the quiescent power, which is marked on the graph as $I_{Q}V_{CC}$, the product of the quiescent current and the supply voltage.

Key features include:
- The waveform is centered around the quiescent power level, showing oscillations above and below this line.
- Peaks and valleys are symmetrical, indicating a consistent power dissipation pattern.
- The maximum amplitude of power dissipation is not explicitly marked, but it can be inferred from the waveform's symmetry and periodicity.

Overall, the graph illustrates how the power dissipation in the transistor fluctuates over time, emphasizing the dynamic nature of power management in electronic circuits.

Figure 5.5 Waveforms for the transistor $Q_{1}$ of Figure 5.1 at full output with $R_{L}=R_{L 3}$. (a) Collector-emitter voltage waveform. (b) Collector current waveform. (c) Collector power dissipation waveform.
is the instantaneous power dissipation in the transistor. The curve of instantaneous power dissipation in $Q_{1}$ as a function of time varies at twice the signal frequency and has an average value of one-half the quiescent value. This result can be shown analytically as follows. The instantaneous power dissipation in $Q_{1}$ is

$$
\begin{equation*}
P_{c 1}=V_{c e 1} I_{c 1} \tag{5.15}
\end{equation*}
$$

At maximum signal swing with a sinusoidal signal, $P_{c 1}$ can be expressed as (from Fig. 5.5)

$$
\begin{equation*}
P_{c 1}=V_{C C}(1+\sin \omega t) I_{Q}(1-\sin \omega t)=\frac{V_{C C} I_{Q}}{2}(1+\cos 2 \omega t) \tag{5.15a}
\end{equation*}
$$

The average value of $P_{c 1}$ from (5.15a) is $V_{C C} I_{Q} / 2$. Thus at maximum output the average power dissipated in $Q_{1}$ is half its quiescent value, and the average device temperature when delivering power with $R_{L}=R_{L 3}$ is less than its quiescent value.

Further information on the power dissipated in $Q_{1}$ can be obtained by plotting curves of constant device dissipation in the $I_{c}-V_{c e}$ plane. Equation 5.15 indicates that such curves are hyperbolas, which are plotted in Fig. 5.6 for constant transistor instantaneous power dissipation values $P_{1}, P_{2}$, and $P_{3}$ (where $P_{1}<P_{2}<P_{3}$ ). The power hyperbola of value $P_{2}$ passes through the quiescent point $Q$, and the equation of this curve can be calculated from (5.15) as

$$
\begin{equation*}
I_{c 1}=\frac{P_{2}}{V_{c e 1}} \tag{5.16}
\end{equation*}
$$

The slope of the curve is

$$
\frac{d I_{c 1}}{d V_{c e 1}}=-\frac{P_{2}}{V_{c e 1}^{2}}
$$

image_name:Figure 5.6
description:The graph in Figure 5.6 is a plot of hyperbolas representing constant instantaneous transistor power dissipation in the \(I_{c1} - V_{ce1}\) plane for an emitter follower transistor \(Q_1\). The axes are labeled \(I_{c1}\) (collector current) on the vertical axis and \(V_{ce1}\) (collector-emitter voltage) on the horizontal axis.

Type of Graph and Function:
This is a hyperbolic plot showing the relationship between collector current \(I_{c1}\) and collector-emitter voltage \(V_{ce1}\) for different levels of power dissipation \(P_1, P_2,\) and \(P_3\).

Axes Labels and Units:
- **Vertical Axis (Y-axis):** \(I_{c1}\) (Collector current)
- **Horizontal Axis (X-axis):** \(V_{ce1}\) (Collector-emitter voltage)

Overall Behavior and Trends:
The graph shows three hyperbolic curves, each representing a constant power dissipation level \(P_1, P_2,\) and \(P_3\) with \(P_1 < P_2 < P_3\). Each hyperbola is asymptotic to both axes, indicating that as one variable increases, the other decreases to maintain constant power.

Key Features and Technical Details:
- The hyperbola for \(P_2\) passes through the quiescent point \(Q\), which is a key operating point for the transistor.
- The slope of the power hyperbolas is negative, indicating an inverse relationship between \(I_{c1}\) and \(V_{ce1}\) for constant power.
- Load lines are shown for \(R_L = 0\), \(R_L = R_{L3}\), and \(R_L \rightarrow \infty\), with the load line intersecting the hyperbolas and indicating different operating conditions.

Annotations and Specific Data Points:
- The graph includes annotations marking regions of low and high transistor power dissipation.
- The quiescent point \(Q\) is marked, which is significant for analyzing the transistor's operating conditions.
- The power levels \(P_1, P_2,\) and \(P_3\) are labeled, and the curve for \(P_3\) is the outermost, representing the highest power dissipation.

This graph is a useful tool for visualizing how changes in voltage and current affect power dissipation in a transistor, and it aids in designing circuits to operate within safe power limits.

Figure 5.6 Hyperbolas of constant instantaneous transistor power dissipation $P_{1}, P_{2}$, and $P_{3}$ in the $I_{c 1}-V_{c e 1}$ plane for emitter follower $Q_{1}$ of Fig. 5.1. Load lines are included for $R_{L}=0, R_{L}=R_{L 3}$, and $R_{L} \rightarrow \infty$. Note that $P_{1}<P_{2}<P_{3}$.
and substitution of (5.16) in this equation gives

$$
\begin{equation*}
\frac{d I_{c 1}}{d V_{c e 1}}=-\frac{I_{c 1}}{V_{c e 1}} \tag{5.17}
\end{equation*}
$$

At the quiescent point $Q$, we have $I_{c 1}=I_{Q}$ and $V_{c e 1}=V_{C C}$. Thus the slope is

$$
\begin{equation*}
\left.\frac{d I_{c 1}}{d V_{c e 1}}\right|_{Q}=-\frac{I_{Q}}{V_{C C}} \tag{5.18}
\end{equation*}
$$

From (5.6), the slope of the load line with $R_{L}=R_{L 3}$ is $-\left(1 / R_{L 3}\right)$. Using (5.10) for $R_{L 3}$ gives

$$
\begin{equation*}
-\frac{1}{R_{L 3}} \simeq-\frac{I_{Q}}{V_{C C}} \tag{5.19}
\end{equation*}
$$

Comparing (5.18) with (5.19) shows that the load line with $R_{L}=R_{L 3}$ is tangent to the power hyperbola passing through the quiescent point, since both curves have the same slope at that point. This result is illustrated in Fig. 5.6. As the operating point leaves the quiescent point and moves on the load line with $R_{L}=R_{L 3}$, the load line then intersects constant-power hyperbolas representing lower power values; therefore, the instantaneous device power dissipation decreases. This point of view is consistent with the power waveform shown in Fig. 5.5.

The load line for $R_{L} \rightarrow \infty$ (open-circuit load) is also shown in Fig. 5.6. In that case, the transistor collector current does not vary over a period but is constant. For values of $V_{c e 1}$ greater than the quiescent value, the instantaneous device power dissipation increases. The maximum possible value of $V_{c e 1}$ is ( $\left.2 V_{C C}-V_{C E 2(\text { sat })}\right)$. At this value, the instantaneous power dissipation in $Q_{1}$ is approximately $2 V_{C C} I_{Q}$ if $V_{C E 2(\text { sat })} \ll V_{C C}$. This dissipation is twice the quiescent value of $V_{C C} I_{Q}$, and this possibility should be taken into account when considering the power-handling requirements of $Q_{1}$. At the other extreme of the swing where $V_{c e 1} \simeq 0$, the power dissipation in $Q_{2}$ is also $2 V_{C C} I_{Q}$.

A situation that is potentially even more damaging can occur if the load is short circuited. In that case, the load line is vertical through the quiescent point, as shown in Fig. 5.6. With large input signals, the collector current (and thus the device power dissipation) of $Q_{1}$ can become quite large. The limit on collector current is set by the ability of the driver to supply the base current to $Q_{1}$, and also by the high-current fall-off in $\beta_{F}$ of $Q_{1}$, described in Chapter 1 . In practice, these limits may be sufficient to prevent burnout of $Q_{1}$, but current-limiting circuitry may be necessary. An example of such protection is given in Section 5.4.6.

A useful general result can be derived from the calculations above involving load lines and constant-power hyperbolas. Figure 5.6 shows that the maximum instantaneous device power dissipation for $R_{L}=R_{L 3}$ occurs at the quiescent point $Q$ (since $P_{1}<P_{2}<P_{3}$ ), which is the midpoint of the load line if $V_{C E 2(\text { sat })} \ll V_{C C}$. (The midpoint of the load line is assumed to be midway between its intersections with the $I_{c}$ and $V_{c e}$ axes.) It can be seen from (5.17) that any load line tangent to a power hyperbola makes contact with the hyperbola at the midpoint of the load line. Consequently, the midpoint is the point of maximum instantaneous device power dissipation with any load line. For example, in Fig. 5.4 with $R_{L}=R_{L 2}$, the maximum instantaneous device power dissipation occurs at the midpoint of the load line where $V_{c e 1}=\frac{1}{2}\left(V_{C C}+I_{Q} R_{L 2}\right)$.

An output stage of the type described in this section, where the output device always conducts appreciable current, is called a Class $A$ output stage. This type of operation can be realized with different transistor configurations but always has a maximum efficiency of 25 percent.

Finally, the emitter follower in this analysis was assumed to have a current source $I_{Q}$ in its emitter as a bias element. In practice, the current source is sometimes replaced by a resistor connected to the negative supply, and such a configuration will give some deviations from the above calculations. In particular, the output power available from the circuit will be reduced.

#### EXAMPLE

An output stage such as shown in Fig. 5.1 has the following parameters: $V_{C C}=10 \mathrm{~V}$, $R_{3}=5 \mathrm{k} \Omega, R_{1}=R_{2}=0, V_{C E(\mathrm{sat})}=0.2 \mathrm{~V}, R_{L}=1 \mathrm{k} \Omega$. Assume that the dc input voltage is adjusted so that the dc output voltage is 0 volts.
(a) Calculate the maximum average output power that can be delivered to $R_{L}$ before clipping occurs, and the corresponding efficiency. What is the maximum possible efficiency with this stage and what value of $R_{L}$ is required to achieve this efficiency? Assume the signals are sinusoidal.
(b) Calculate the maximum possible instantaneous power dissipation in $Q_{1}$. Also calculate the average power dissipation in $Q_{1}$ when $\hat{V}_{o}=1.5 \mathrm{~V}$ and the output voltage is sinusoidal.

The solution proceeds as follows.
(a) The bias current $I_{Q}$ is first calculated.

$$
I_{Q}=I_{R}=\frac{V_{C C}-V_{B E 3}}{R_{3}}=\frac{10-0.7}{5} \mathrm{~mA}=1.86 \mathrm{~mA}
$$

The product, $I_{Q} R_{L}$, is given by

$$
I_{Q} R_{L}=1.86 \times 1=1.86 \mathrm{~V}
$$

Since the dc output voltage is assumed to be 0 volts, and since $I_{Q} R_{L}$ is less than $V_{C C}$, the maximum sinusoidal output voltage swing is limited to 1.86 V by clipping on negative voltage swings and the situation corresponds to $R_{L}=R_{L 2}$ in Fig. 5.4. The maximum output voltage and current swings are thus $\hat{V}_{o m}=1.86 \mathrm{~V}$ and $\hat{I}_{o m}=1.86 \mathrm{~mA}$. The maximum average output power available from the circuit for sinusoidal signals can be calculated from (5.7a) as

$$
\left.P_{L}\right|_{\max }=\frac{1}{2} \hat{V}_{o m} \hat{I}_{o m}=\frac{1}{2} \times 1.86 \times 1.86 \mathrm{~mW}=1.73 \mathrm{~mW}
$$

The power drawn from the supplies is calculated from (5.12) as

$$
P_{\text {supply }}=2 V_{C C} I_{Q}=2 \times 10 \times 1.86 \mathrm{~mW}=37.2 \mathrm{~mW}
$$

The efficiency of the circuit at the output power level calculated above can be determined from (5.13)

$$
\eta_{C}=\frac{\left.P_{L}\right|_{\max }}{P_{\text {supply }}}=\frac{1.73}{37.2}=0.047
$$

The efficiency of 4.7 percent is quite low and is due to the limitation on the negative voltage swing.

The maximum possible efficiency with this stage occurs for $R_{L}=R_{L 3}$ in Fig. 5.4, and $R_{L 3}$ is given by (5.10) as

$$
R_{L 3}=\frac{V_{C C}-V_{C E(\mathrm{sat})}}{I_{Q}}=\frac{10-0.2}{1.86} \mathrm{k} \Omega=5.27 \mathrm{k} \Omega
$$

In this instance, the maximum average power that can be delivered to the load before clipping occurs is found from (5.11) as

$$
\left.P_{L}\right|_{\max }=\frac{1}{2}\left[V_{C C}-V_{C E(\mathrm{sat})}\right] I_{Q}=\frac{1}{2}(10-0.2) 1.86 \mathrm{~mW}=9.11 \mathrm{~mW}
$$

The corresponding efficiency using (5.14) is

$$
\eta_{\max }=\frac{1}{4}\left[1-\frac{V_{C E(\mathrm{sat})}}{V_{C C}}\right]=\frac{1}{4}\left(1-\frac{0.2}{10}\right)=0.245
$$

This result is close to the theoretical maximum of 25 percent.
(b) The maximum possible instantaneous power dissipation in $Q_{1}$ occurs at the midpoint of the load line. Reference to Fig. 5.4 and the load line $R_{L}=R_{L 2}$ shows that this occurs for

$$
V_{c e 1}=\frac{1}{2}\left(V_{C C}+I_{Q} R_{L}\right)=\frac{1}{2}(10+1.86)=5.93 \mathrm{~V}
$$

The corresponding collector current in $Q_{1}$ is $I_{c 1}=5.93 / R_{L}=5.93 \mathrm{~mA}$ since $R_{L}=1 \mathrm{k} \Omega$. Thus the maximum instantaneous power dissipation in $Q_{1}$ is

$$
P_{c 1}=I_{c 1} V_{c e 1}=35.2 \mathrm{~mW}
$$

This power dissipation occurs for $V_{c e 1}=5.93 \mathrm{~V}$, which represents a signal swing beyond the linear limits of the circuit [clipping occurs when the output voltage reaches -1.86 V as calculated in (a)]. However, this condition could easily occur if the circuit is overdriven by a large input signal.

The average power dissipation in $Q_{1}$ can be calculated by noting that for sinusoidal signals, the average power drawn from the two supplies is constant and independent of the presence of signals. Since the power input to the circuit from the supplies is constant, the total average power dissipated in $Q_{1}, Q_{2}$, and $R_{L}$ must be constant and independent of the presence of sinusoidal signals. The average power dissipated in $Q_{2}$ is constant because $I_{Q}$ is constant, and thus the average power dissipated in $Q_{1}$ and $R_{L}$ together is constant. Thus as $\hat{V}_{o}$ is increased, the average power dissipated in $Q_{1}$ decreases by the same amount as the average power in $R_{L}$ increases. With no input signal, the quiescent power dissipated in $Q_{1}$ is

$$
P_{C Q}=V_{C C} I_{Q}=10 \times 1.86 \mathrm{~mW}=18.6 \mathrm{~mW}
$$

For $\hat{V}_{o}=1.5 \mathrm{~V}$, the average power delivered to the load is

$$
P_{L}=\frac{1}{2} \frac{\hat{V}_{o}^{2}}{R_{L}}=\frac{1}{2} \frac{2.25}{1} \mathrm{~mW}=1.13 \mathrm{~mW}
$$

Thus the average power dissipated in $Q_{1}$ when $\hat{V}_{o}=1.5 \mathrm{~V}$ with a sinusoidal signal is

$$
P_{a v}=P_{C Q}-P_{L}=17.5 \mathrm{~mW}
$$

### 5.2.3 Emitter-Follower Drive Requirements

The calculations above have been concerned with the performance of the emitter-follower output stage when driven by a sinusoidal input voltage. The stage preceding the output stage is called the driver stage, and in practice it may introduce additional limitations on the circuit performance. For example, it was shown that to drive the output voltage $V_{o}$ of the emitter follower to its maximum positive value required an input voltage slightly greater than the supply voltage. Since the driver stage is connected to the same supplies as the output stage in most cases, the driver stage generally cannot produce voltages greater than the supply, further reducing the possible output voltage swing.

The above limitations stem from the observation that the emitter follower has a voltage gain of unity and thus the driver stage must handle the same voltage swing as the output. However, the driver can be a much lower power stage than the output stage because the current it must
image_name:Figure 5.7 Low-frequency, smallsignal equivalent circuit for the emitter follower of Fig. 5.1.
description:
[
name: vi, type: VoltageSource, value: vi, ports: {Np: vin, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: vin, N2: x}
name: rπ, type: Resistor, value: rπ, ports: {N1: x, N2: vo}
name: gmV1, type: CurrentControlledCurrentSource, ports: {Np: GND, Nn: vo}
name: RL, type: Resistor, value: RL, ports: {N1: vo+, N2: GND}
]
extrainfo:The circuit is a low-frequency small-signal equivalent circuit for an emitter follower. It includes a voltage source vi, resistors RS, rπ, RO, RL, and a current-controlled current source gmV1. The circuit is grounded at multiple points.

Figure 5.7 Low-frequency, smallsignal equivalent circuit for the emitter follower of Fig. 5.1.
deliver is the base current of the emitter follower, which is about $1 / \beta_{F}$ times the emitter current. Consequently, the driver bias current can be much lower than the output-stage bias current, and a smaller geometry can be used for the driver device. Although it has only unity voltage gain, the emitter follower has substantial power gain, which is a requirement of any output stage.

### 5.2.4 Small-Signal Properties of the Emitter Follower

A simplified low-frequency, small-signal equivalent circuit of the emitter follower of Fig. 5.1 is shown in Fig. 5.7. As described in Chapter 7, the emitter follower is an extremely wideband circuit and rarely is a source of frequency limitation in the small-signal gain of an amplifier. Thus the equivalent circuit of Fig. 5.7 is useful over a wide frequency range and an analysis of this circuit shows that the voltage gain $A_{v}$ and the output resistance $R_{o}$ can be expressed approximately for $\beta_{0} \gg 1$ as

$$
\begin{align*}
A_{v}=\frac{v_{o}}{v_{i}} & \simeq \frac{R_{L}}{R_{L}+\frac{1}{g_{m}}+\frac{R_{S}}{\beta_{0}}}  \tag{5.20}\\
R_{o} & =\frac{1}{g_{m}}+\frac{R_{S}}{\beta_{0}} \tag{5.21}
\end{align*}
$$

These quantities are small-signal quantities, and since $g_{m}=q I_{C} / \mathrm{k} T$ is a function of bias point, both $A_{v}$ and $R_{o}$ are functions of $I_{C}$. Since the emitter follower is being considered here for use as an output stage where the signal swing may be large, (5.20) and (5.21) must be applied with caution. However, for small to moderate signal swings, these equations may be used to estimate the average gain and output resistance of the stage if quiescent bias values are used for transistor parameters in the equations. Equation 5.20 can also be used as a means of estimating the nonlinearity ${ }^{1}$ in the stage by recognizing that it gives the incremental slope of the large-signal characteristic of Fig. 5.2 at any point. If this equation is evaluated at the extremes of the signal swing, an estimate of the curvature of the characteristic is obtained, as illustrated in the following example.

#### EXAMPLE

Calculate the incremental slope of the transfer characteristic of the circuit of Fig. 5.1 as the quiescent point and at the extremes of the signal swing with a peak sinusoidal output of 0.6 V . Use data as in the previous example and assume that $R_{S}=0$.

From (5.20) the small-signal gain with $R_{S}=0$ is

$$
\begin{equation*}
A_{v}=\frac{R_{L}}{R_{L}+\frac{1}{g_{m}}} \tag{5.22}
\end{equation*}
$$

Since $I_{Q}=1.86 \mathrm{~mA}, 1 / g_{m}=14 \Omega$ at the quiescent point and the quiescent gain is

$$
A_{v} Q=\frac{1000}{1000+14}=0.9862
$$

Since the output voltage swing is 0.6 V , the output current swing is

$$
\hat{I}_{o}=\frac{\hat{V}_{o}}{R_{L}}=\frac{0.6}{1000}=0.6 \mathrm{~mA}
$$

Thus at the positive signal peak, the transistor collector current is

$$
I_{Q}+\hat{I}_{o}=1.86+0.6=2.46 \mathrm{~mA}
$$

At this current, $1 / g_{m}=10.6 \Omega$ and use of (5.22) gives the small-signal gain as

$$
A_{v}^{+}=\frac{1000}{1010.6}=0.9895
$$

This gain is 0.3 percent more than the quiescent value. At the negative signal peak, the transistor collector current is

$$
I_{Q}-\hat{I}_{o}=1.86-0.6=1.26 \mathrm{~mA}
$$

At this current, $1 / g_{m}=20.6 \Omega$ and use of (5.22) gives the small-signal gain as

$$
A_{v}^{-}=\frac{1000}{1020.6}=0.9798
$$

This gain is 0.7 percent less than the quiescent value. Although the collector-current signal amplitude is one-third of the bias current in this example, the small-signal gain variation is extremely small. This circuit thus has a high degree of linearity. Since the nonlinearity is small, the resulting distortion can be determined from the three values of the small-signal gain calculated in this example. See Problem 5.8.

## 5.3 The Source Follower as an Output Stage

The small-signal properties of the source follower are calculated in Chapter 3. Since this circuit has low output resistance, it is often used as an output stage. The large signal properties of the source follower are considered next.

### 5.3.1 Transfer Characteristics of the Source Follower

A source-follower output stage is shown in Fig. 5.8 with equal magnitude positive and negative power supplies for simplicity. The large-signal transfer characteristic can be derived as follows:

$$
\begin{equation*}
V_{i}=V_{o}+V_{g s 1}=V_{o}+V_{t 1}+V_{o v 1} \tag{5.23}
\end{equation*}
$$

If the threshold and overdrive terms are exactly constant, the output voltage follows the input voltage with a constant difference. In practice, however, the body effect changes the threshold voltage. Also, the overdrive is not constant mainly because the drain current is not constant.
image_name:Figure 5.8 Source-follower output stage with current-mirror bias
description:
[
name: M1, type: NMOS, ports: {S: Vout, D: VDD, G: Vin}
name: M2, type: NMOS, ports: {S: -VDD, D: Vout, G: g2g3d3}
name: M3, type: NMOS, ports: {S: -VDD, D: g2g3d3, G: g2g3d3}
name: IR, type: CurrentSource, value: IR, ports: {Np: VDD, Nn: g2g3d3}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a source-follower output stage with current-mirror biasing. NMOS transistors M1 and M2 form the output stage, while M3 is used for current mirroring. The current source IR provides biasing current, and RL is the load resistor.

Figure 5.8 Source-follower output stage with current-mirror bias.

Substituting (1.140) with $V_{s b}=V_{o}+V_{D D}$ and (1.166) with $I_{d 1}=I_{Q}+V_{o} / R_{L}$ into (5.23) gives

$$
\begin{equation*}
V_{i}=V_{o}+V_{t 0}+\gamma\left(\sqrt{2 \phi_{f}+V_{o}+V_{D D}}-\sqrt{2 \phi_{f}}\right)+\sqrt{\frac{2\left(I_{Q}+\frac{V_{o}}{R_{L}}\right)}{k^{\prime}(W / L)_{1}}} \tag{5.24}
\end{equation*}
$$

This equation is valid provided that $M_{1}$ and $M_{2}$ operate in the active region with output resistances much larger than $R_{L}$.

The transfer characteristic is plotted in Fig. 5.9. It intersects the $x$ axis at the input-referred offset voltage, which is

$$
\begin{equation*}
\left.V_{i}\right|_{V_{o}=0}=V_{t 0}+\gamma\left(\sqrt{2 \phi_{f}+V_{D D}}-\sqrt{2 \phi_{f}}\right)+\sqrt{\frac{2 I_{Q}}{k^{\prime}(W / L)_{1}}} \tag{5.25}
\end{equation*}
$$

The slope at this point is the incremental gain calculated in (3.80). With $r_{o} \rightarrow \infty$, the slope is

$$
\begin{equation*}
\frac{v_{o}}{v_{i}}=\frac{g_{m} R_{L}}{1+\left(g_{m}+g_{m b}\right) R_{L}} \tag{5.26}
\end{equation*}
$$

image_name:Figure 5.9 Transfer characteristic of the circuit of Fig. 5.8
description:The graph in Figure 5.9 is a transfer characteristic plot for a circuit, showing the relationship between the output voltage \( V_o \) on the vertical axis and the input voltage \( V_i \) on the horizontal axis. This plot is used to illustrate how the circuit responds to different input voltages, particularly focusing on two different load resistances, \( R_{L1} \) and \( R_{L2} \).

1. **Type of Graph and Function**:
- This is a transfer characteristic graph, typically used in analog electronics to show how the output of a circuit varies with the input.

2. **Axes Labels and Units**:
- The horizontal axis represents the input voltage \( V_i \), while the vertical axis represents the output voltage \( V_o \). Both axes are likely measured in volts, though specific units are not indicated.

3. **Overall Behavior and Trends**:
- The graph shows a nonlinear relationship between \( V_i \) and \( V_o \). It features a central linear region where the circuit operates linearly, flanked by regions of nonlinearity due to cutoff and triode operation.
- As \( V_i \) increases, \( V_o \) initially rises slowly, then enters a linear region, and finally saturates, indicating the circuit's operating limits.

4. **Key Features and Technical Details**:
- **Cutoff Region**: At lower \( V_i \) values, the curve starts with a gradual slope, indicating the cutoff region for \( M_1 \), where the output is minimal.
- **Triode Region**: As \( V_i \) increases, the curve enters the \( M_2 \) triode region, showing a steeper slope.
- **Linear Region**: The central part of the graph shows a linear behavior where the output voltage increases proportionally with the input voltage.
- **Saturation Region**: At higher \( V_i \) values, the curve flattens, indicating saturation and the \( M_1 \) triode region.
- **Key Points**: Critical voltages such as \( V_{GS1} \), \( V_{DD} - V_{ov1} \), and \( V_{DD} + V_{t1} \) are marked, indicating important thresholds in the circuit's operation.

5. **Annotations and Specific Data Points**:
- The graph is annotated with specific voltage levels like \(-V_{DD} + V_{ov2} + V_{gs1} \), \( -I_QR_{L2} \), and \( V_{DD} \), providing reference points for understanding the circuit's behavior at different operating conditions.
- \( R_{L1} \) and \( R_{L2} \) are marked, showing how different load resistances affect the transfer characteristics.

Overall, the graph effectively illustrates the circuit's behavior across different input voltages and load conditions, highlighting the transition between cutoff, linear, and saturation regions.

Figure 5.9 Transfer characteristic of the circuit of Fig. 5.8 for a low $\left(R_{L 2}\right)$ and a high $\left(R_{L 1}\right)$ value of load resistance.

When $R_{L} \rightarrow \infty$,

$$
\begin{equation*}
\frac{v_{o}}{v_{i}}=\frac{g_{m}}{g_{m}+g_{m b}}=\frac{1}{1+\chi} \tag{5.27}
\end{equation*}
$$

Since $\chi$ is typically in the range of 0.1 to 0.3 , the slope typically ranges from about 0.7 to 0.9 . In contrast, the slope of the emitter-follower transfer characteristic is unity under these conditions. Furthermore, $(1.200)$ shows that $\chi$ depends on the source-body voltage, which is $V_{o}+V_{D D}$ in Fig. 5.8. Therefore, the slope calculated in (5.27) changes as $V_{o}$ changes even when $M_{1}$ operates in the active region, causing distortion. Fig. 5.9 ignores this variation in the slope, but it is considered in Section 5.3.2.

When the output voltage rises within an overdrive of the positive supply, $M_{1}$ enters the triode region, dramatically reducing the slope of the transfer characteristic. The overdrive at this break point is calculated using the total drain current, which exceeds $I_{Q}$ if $R_{L}$ is finite. Therefore, the location of the break point depends on $R_{L}$, but this effect is not shown in Fig. 5.9. Unlike in the emitter follower, the output can pull up asymptotically to the supply voltage with unlimited input voltage. In practice, however, the input must be larger than $V_{D D}$ by at least the threshold voltage to bias $M_{1}$ in the triode region. If the input voltage is limited to $V_{D D}, M_{1}$ never reaches the triode region.

For negative input voltages, the minimum value of the output voltage depends on $R_{L}$, as in the emitter follower. If $I_{Q} R_{L}>V_{D D}$, the slope of the transfer characteristic is approximately constant until $M_{2}$ enters the triode region, which happens when

$$
\begin{equation*}
V_{o}=-V_{D D}+V_{o v 2}=-V_{D D}+\sqrt{\frac{2 I_{Q}}{k^{\prime}(W / L)_{2}}} \tag{5.28}
\end{equation*}
$$

This case is labeled as $R_{L 1}$ in Fig. 5.9. On the other hand, if $I_{Q} R_{L}<V_{D D}$, the slope is almost constant until $M_{1}$ turns off. The corresponding minimum output voltage is

$$
\begin{equation*}
V_{o}=-I_{Q} R_{L} \tag{5.29}
\end{equation*}
$$

This case is labeled as $R_{L 2}$ in Fig. 5.9. From a design standpoint, $I_{Q} R_{L}$ is usually set larger than $V_{D D}$, so that the situation shown for $R_{L}=R_{L 1}$ in Fig. 5.9 holds. Under this condition, the output voltage can swing almost to the positive and negative supply voltages before excessive distortion occurs.

### 5.3.2 Distortion in the Source Follower

The transfer function of the source-follower stage was calculated in (5.23), where $V_{i}$ is expressed as a function of $V_{o}$. The calculation of signal distortion from a nonlinear transfer function will now be illustrated using the source-follower stage as an example.

Using a Taylor series, the input voltage can be written as

$$
\begin{equation*}
V_{i}=V_{I}+v_{i}=\sum_{n=0}^{\infty} \frac{f^{(n)}\left(V_{o}=V_{O}\right)\left(V_{o}-V_{O}\right)^{n}}{n!} \tag{5.30}
\end{equation*}
$$

where $f^{(n)}$ represents the $n^{\text {th }}$ derivative of $f$. Since $v_{o}=V_{o}-V_{O}$, (5.30) can be rewritten as

$$
\begin{equation*}
V_{i}=V_{I}+v_{i}=\sum_{n=0}^{\infty} b_{n}\left(v_{o}\right)^{n} \tag{5.31}
\end{equation*}
$$

where $b_{n}=f^{(n)}\left(V_{o}=V_{O}\right) /(n!)$. For simplicity, assume that $R_{L} \rightarrow \infty$. From (1.140) and (5.23),

$$
\begin{equation*}
V_{i}=f\left(V_{o}\right)=V_{o}+V_{t 0}+\gamma\left(\sqrt{V_{o}+V_{D D}+2 \phi_{f}}-\sqrt{2 \phi_{f}}\right)+V_{o v 1} \tag{5.32}
\end{equation*}
$$

Then

$$
\begin{align*}
f^{\prime}\left(V_{o}\right) & =1+\frac{\gamma}{2}\left(V_{o}+V_{D D}+2 \phi_{f}\right)^{-1 / 2}  \tag{5.33}\\
f^{\prime \prime}\left(V_{o}\right) & =-\frac{\gamma}{4}\left(V_{o}+V_{D D}+2 \phi_{f}\right)^{-3 / 2}  \tag{5.34}\\
f^{\prime \prime \prime}\left(V_{o}\right) & =\frac{3 \gamma}{8}\left(V_{o}+V_{D D}+2 \phi_{f}\right)^{-5 / 2} \tag{5.35}
\end{align*}
$$

Therefore,

$$
\begin{align*}
& b_{0}=f\left(V_{o}=V_{O}\right)=V_{O}+V_{t 0}+\gamma\left(\sqrt{V_{O}+V_{D D}+2 \phi_{f}}-\sqrt{2 \phi_{f}}\right)+V_{o v 1}  \tag{5.36}\\
& b_{1}=f^{\prime}\left(V_{o}=V_{O}\right)=1+\frac{\gamma}{2}\left(V_{O}+V_{D D}+2 \phi_{f}\right)^{-1 / 2}  \tag{5.37}\\
& b_{2}=\frac{f^{\prime \prime}\left(V_{o}=V_{O}\right)}{2}=-\frac{\gamma}{8}\left(V_{O}+V_{D D}+2 \phi_{f}\right)^{-3 / 2}  \tag{5.38}\\
& b_{3}=\frac{f^{\prime \prime \prime}\left(V_{o}=V_{O}\right)}{3!}=\frac{\gamma}{16}\left(V_{O}+V_{D D}+2 \phi_{f}\right)^{-5 / 2} \tag{5.39}
\end{align*}
$$

Since the constant $b_{0}$ is the dc input voltage $V_{I},(5.31)$ can be rewritten as

$$
\begin{equation*}
v_{i}=\sum_{n=1}^{\infty} b_{n}\left(v_{o}\right)^{n}=b_{1} v_{o}+b_{2} v_{o}^{2}+b_{3} v_{o}^{3}+\ldots \tag{5.40}
\end{equation*}
$$

To find the distortion, we would like to rearrange this equation into the following form

$$
\begin{equation*}
v_{o}=\sum_{n=1}^{\infty} a_{n}\left(v_{i}\right)^{n}=a_{1} v_{i}+a_{2} v_{i}^{2}+a_{3} v_{i}^{3}+\ldots \tag{5.41}
\end{equation*}
$$

Substituting (5.41) into (5.40) gives

$$
\begin{align*}
v_{i}= & b_{1}\left(a_{1} v_{i}+a_{2} v_{i}^{2}+a_{3} v_{i}^{3}+\ldots\right)+b_{2}\left(a_{1} v_{i}+a_{2} v_{i}^{2}+a_{3} v_{i}^{3}+\ldots\right)^{2} \\
& +b_{3}\left(a_{1} v_{i}+a_{2} v_{i}^{2}+a_{3} v_{i}^{3}+\ldots\right)^{3}+\ldots \\
= & b_{1} a_{1} v_{i}+\left(b_{1} a_{2}+b_{2} a_{1}^{2}\right) v_{i}^{2}+\left(b_{1} a_{3}+2 b_{2} a_{1} a_{2}+b_{3} a_{1}^{3}\right) v_{i}^{3}+\ldots \tag{5.42}
\end{align*}
$$

Matching coefficients in (5.42) shows that

$$
\begin{align*}
& 1=b_{1} a_{1}  \tag{5.43}\\
& 0=b_{1} a_{2}+b_{2} a_{1}^{2}  \tag{5.44}\\
& 0=b_{1} a_{3}+2 b_{2} a_{1} a_{2}+b_{3} a_{1}^{3} \tag{5.45}
\end{align*}
$$

From (5.43),

$$
\begin{equation*}
a_{1}=\frac{1}{b_{1}} \tag{5.46}
\end{equation*}
$$

Substituting (5.46) into (5.44) and rearranging gives

$$
\begin{equation*}
a_{2}=-\frac{b_{2}}{b_{1}^{3}} \tag{5.47}
\end{equation*}
$$

Substituting (5.46) and (5.47) into (5.45) and rearranging gives

$$
\begin{equation*}
a_{3}=\frac{2 b_{2}^{2}}{b_{1}^{5}}-\frac{b_{3}}{b_{1}^{4}} \tag{5.48}
\end{equation*}
$$

For the source follower, substituting (5.37) into (5.46) gives

$$
\begin{equation*}
a_{1}=\frac{1}{1+\frac{\gamma}{2}\left(V_{O}+V_{D D}+2 \phi_{f}\right)^{-1 / 2}} \tag{5.49}
\end{equation*}
$$

Substituting (5.37) and (5.38) into (5.47) and rearranging gives

$$
\begin{equation*}
a_{2}=\frac{\frac{\gamma}{8}\left(V_{O}+V_{D D}+2 \phi_{f}\right)^{-3 / 2}}{\left(1+\frac{\gamma}{2}\left(V_{O}+V_{D D}+2 \phi_{f}\right)^{-1 / 2}\right)^{3}} \tag{5.50}
\end{equation*}
$$

Substituting (5.37), (5.38), and (5.39) into (5.48) and rearranging gives

$$
\begin{equation*}
a_{3}=-\frac{\frac{\gamma}{16}\left(V_{O}+V_{D D}+2 \phi_{f}\right)^{-5 / 2}}{\left(1+\frac{\gamma}{2}\left(V_{O}+V_{D D}+2 \phi_{f}\right)^{-1 / 2}\right)^{5}} \tag{5.51}
\end{equation*}
$$

Equations $5.41,5.49,5.50$, and 5.51 can be used to calculate the distortion of the sourcefollower stage. For small values of $v_{i}$ such that $a_{2} v_{i}^{2} \ll a_{1} v_{i}$, the first term on the right-hand side of (5.41) dominates and the circuit is essentially linear. However, as $v_{i}$ becomes comparable to $a_{1} / a_{2}$, other terms become significant and distortion products are generated, as is illustrated next. A common method of describing the nonlinearity of an amplifier is the specification of harmonic distortion, which is defined for a single sinusoidal input applied to the amplifier. Thus let

$$
\begin{equation*}
v_{i}=\hat{v}_{i} \sin \omega t \tag{5.52}
\end{equation*}
$$

Substituting (5.52) into (5.41) gives

$$
\begin{align*}
v_{o} & =a_{1} \hat{v}_{i} \sin \omega t+a_{2} \hat{v}_{i}^{2} \sin ^{2} \omega t+a_{3} \hat{v}_{i}^{3} \sin ^{3} \omega t+\ldots \\
& =a_{1} \hat{v}_{i} \sin \omega t+\frac{a_{2} \hat{v}_{i}^{2}}{2}(1-\cos 2 \omega t)+\frac{a_{3} \hat{v}_{i}^{3}}{4}(3 \sin \omega t-\sin 3 \omega t)+\ldots \tag{5.53}
\end{align*}
$$

Equation 5.53 shows that the output voltage contains frequency components at the fundamental frequency, $\omega$ (the input frequency), and also at harmonic frequencies $2 \omega, 3 \omega$, and so on. The latter terms represent distortion products that are not present in the input signal. Secondharmonic distortion $\mathrm{HD}_{2}$ is defined as the ratio of the amplitude of the output-signal component at frequency $2 \omega$ to the amplitude of the first harmonic (or fundamental) at frequency $\omega$. For small distortion, the term (3/4) $a_{3} \hat{v}_{i}^{3} \sin \omega t$ in (5.53) is small compared to $a_{1} \hat{v}_{i} \sin \omega t$, and the amplitude of the fundamental is approximately $a_{1} \hat{v}_{i}$. Again for small distortion, higher-order terms in (5.53) may be neglected and

$$
\begin{equation*}
H D_{2}=\frac{a_{2} \hat{v}_{i}^{2}}{2} \frac{1}{a_{1} \hat{v}_{i}}=\frac{1}{2} \frac{a_{2}}{a_{1}} \hat{v}_{i} \tag{5.54}
\end{equation*}
$$

Under these assumptions, $H D_{2}$ varies linearly with the peak signal level $\hat{v}_{i}$. The value of $H D_{2}$ can be expressed in terms of known parameters by substituting (5.49) and (5.50) in (5.54) to give

$$
\begin{equation*}
H D_{2}=\frac{\gamma}{16} \frac{\left(V_{O}+V_{D D}+2 \phi_{f}\right)^{-3 / 2}\left(\hat{v}_{i}\right)}{\left(1+\frac{\gamma}{2}\left(V_{O}+V_{D D}+2 \phi_{f}\right)^{-1 / 2}\right)^{2}} \tag{5.55}
\end{equation*}
$$

If $\gamma \ll 2 \sqrt{V_{O}+V_{D D}+2 \phi_{f}}$, then

$$
\begin{equation*}
H D_{2} \simeq \frac{\gamma}{16}\left(V_{O}+V_{D D}+2 \phi_{f}\right)^{-3 / 2} \hat{v}_{i} \tag{5.56}
\end{equation*}
$$

This equation shows that the second-harmonic distortion can be reduced by increasing the dc output voltage $V_{O}$. This result is reasonable because this distortion stems from the body effect. Therefore, increasing $V_{O}$ decreases the variation of the source-body voltage compared to its dc value caused by an input with fixed peak amplitude. ${ }^{2}$ Equation 5.56 also shows that the second-harmonic distortion is approximately proportional to $\gamma$, neglecting the effect of $\gamma$ on $V_{O}$.

Similarly, third-harmonic distortion $\mathrm{HD}_{3}$ is defined as the ratio of the output signal component at frequency $3 \omega$ to the first harmonic. From (5.53) and assuming small distortion,

$$
\begin{equation*}
H D_{3}=\frac{a_{3} \hat{v}_{i}^{3}}{4} \frac{1}{a_{1} \hat{v}_{i}}=\frac{1}{4} \frac{a_{3}}{a_{1}} \hat{v}_{i}^{2} \tag{5.57}
\end{equation*}
$$

Under these assumptions, $H D_{3}$ varies as the square of the signal amplitude. The value of $H D_{3}$ can be expressed in terms of known parameters by substituting (5.49) and (5.51) in (5.57) to give

$$
\begin{equation*}
H D_{3}=-\frac{\gamma}{64} \frac{\left(V_{O}+V_{D D}+2 \phi_{f}\right)^{-5 / 2}\left(\hat{v}_{i}^{2}\right)}{\left(1+\frac{\gamma}{2}\left(V_{O}+V_{D D}+2 \phi_{f}\right)^{-1 / 2}\right)^{4}} \tag{5.58}
\end{equation*}
$$

Since the distortion calculated above stems from the body effect, it can be eliminated by placing the source follower in an isolated well and connecting the source to the well. However, this approach specifies the type of source-follower transistor because it must be opposite the type of the doping in the well. Also, this approach adds the well-substrate parasitic capacitance to the output load of the source follower, reducing its bandwidth.

#### EXAMPLE

Calculate second- and third-harmonic distortion in the circuit of Fig. 5.8 for a peak sinusoidal input voltage $\hat{v}_{i}=0.5 \mathrm{~V}$. Assume that $V_{I}=0, V_{D D}=2.5 \mathrm{~V}, I_{Q}=1 \mathrm{~mA}$, and $R_{L} \rightarrow \infty$. Also, assume that $(W / L)_{1}=1000, k^{\prime}=200 \mu \mathrm{~A} / \mathrm{V}^{2}, V_{t 0}=0.7 \mathrm{~V}, \phi_{f}=0.3 \mathrm{~V}$, and $\gamma=0.5 \mathrm{~V}^{1 / 2}$.

First, the dc output voltage $V_{O}$ is

$$
\begin{equation*}
V_{O}=V_{I}-V_{t 0}-\gamma\left(\sqrt{V_{O}+V_{D D}+2 \phi_{f}}-\sqrt{2 \phi_{f}}\right)-V_{o v 1} \tag{5.59}
\end{equation*}
$$

Rearranging (5.59) gives

$$
\begin{align*}
\left(V_{O}+V_{D D}+2 \phi_{f}\right) & +\gamma \sqrt{V_{O}+V_{D D}+2 \phi_{f}} \\
& -V_{I}+V_{o v 1}+V_{t 0}-\gamma \sqrt{2 \phi_{f}}-V_{D D}-2 \phi_{f}=0 \tag{5.60}
\end{align*}
$$

This quadratic equation can be solved for $\sqrt{V_{O}+V_{D D}+2 \phi_{f}}$. Since the result must be positive,

$$
\begin{align*}
\sqrt{V_{O}+V_{D D}+2 \phi_{f}} & = \\
-\frac{\gamma}{2} & +\sqrt{\left(\frac{\gamma}{2}\right)^{2}+V_{I}-V_{o v 1}-V_{t 0}+\gamma \sqrt{2 \phi_{f}}+V_{D D}+2 \phi_{f}} \tag{5.61}
\end{align*}
$$

Squaring both sides and rearranging gives

$$
\begin{align*}
V_{O}= & -V_{D D}-2 \phi_{f} \\
& +\left(-\frac{\gamma}{2}+\sqrt{\left(\frac{\gamma}{2}\right)^{2}+V_{I}-V_{o v 1}-V_{t 0}+\gamma \sqrt{2 \phi_{f}}+V_{D D}+2 \phi_{f}}\right)^{2} \tag{5.62}
\end{align*}
$$

In this example,

$$
\begin{equation*}
V_{o v 1}=\sqrt{\frac{2 I_{Q}}{k^{\prime}(W / L)_{1}}}=\sqrt{\frac{2(1000)}{200(1000)}} \mathrm{V}=0.1 \mathrm{~V} \tag{5.63}
\end{equation*}
$$

Since $V_{D D}+2 \phi_{f}=3.1 \mathrm{~V}$ and $V_{I}-V_{o v 1}-V_{t 0}=-0.8 \mathrm{~V}$,

$$
\begin{aligned}
V_{O} & =-3.1 \mathrm{~V}+\left(-0.25+\sqrt{(0.25)^{2}-0.8+0.5 \sqrt{0.6}+3.1}\right)^{2} \mathrm{~V} \\
& =-1.117 \mathrm{~V}
\end{aligned}
$$

Therefore,

$$
V_{O}+V_{D D}+2 \phi_{f}=(-1.117+2.5+0.6) \mathrm{V}=1.983 \mathrm{~V}
$$

From (5.55),

$$
\begin{equation*}
H D_{2}=\frac{0.5}{16} \frac{(1.983)^{-3 / 2}(0.5)}{\left(1+\frac{0.5}{2}(1.983)^{-1 / 2}\right)^{2}}=0.0040 \tag{5.64}
\end{equation*}
$$

From (5.58),

$$
\begin{equation*}
H D_{3}=-\frac{0.5}{64} \frac{(1.983)^{-5 / 2}(0.5)^{2}}{\left(1+\frac{0.5}{2}(1.983)^{-1 / 2}\right)^{4}}=-1.8 \times 10^{-4} \tag{5.65}
\end{equation*}
$$

Thus the second-harmonic distortion is 0.40 percent and the third-harmonic distortion is 0.018 percent. In practice, the second-harmonic distortion is usually dominant. ${ }^{3}$

## 5.4 Class B Push-Pull Output Stage ${ }^{4,5}$

The major disadvantage of Class A output stages is that large power dissipation occurs even for no ac input. In many applications of power amplifiers, the circuit may spend long periods of time in a standby condition with no input signal, or with intermittent inputs as in the case of voice signals. Power dissipated in these standby periods is wasted, which is important for two reasons. First, in battery-operated equipment, supply power must be conserved to extend the battery life. Second, any power wasted in the circuit is dissipated in the active devices, increasing their operating temperatures and thus the chance of failure. Furthermore, the power dissipated in the devices affects the physical size of device required, and larger devices are more expensive in terms of silicon area.

A Class B output stage alleviates this problem by having essentially zero power dissipation with zero input signal. Two active devices are used to deliver the power instead of one, and each device conducts for alternate half cycles. This behavior is the origin of the name push-pull. Another advantage of Class B output stages is that the efficiency is much higher than for a Class A output stage (ideally 78.6 percent at full output power).
image_name:Figure 5.10 Simple integrated-circuit Class B output stage
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vin, Nn: GND}
name: Q1, type: NPN, ports: {C: VCC, B: Vin, E: Vout}
name: Q2, type: PNP, ports: {C: -VCC, B: Vin, E: Vout}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a Class B output stage using a complementary pair of transistors (NPN and PNP). It operates in a push-pull configuration to improve efficiency, with the load resistor connected to the emitters of the transistors, making them act as emitter followers.

Figure 5.10 Simple integrated-circuit Class B output stage.

A typical integrated-circuit realization of the Class B output stage is shown in Fig. 5.10 in bipolar technology. This circuit uses both $p n p$ and $n p n$ devices and is known as a complementary output stage. The pnp transistor is usually a substrate $p n p$. Note that the load resistance $R_{L}$ is connected to the emitters of the active devices; therefore, the devices act as emitter followers.

### 5.4.1 Transfer Characteristic of the Class B Stage

The transfer characteristic of the circuit of Fig. 5.10 is shown in Fig. 5.11. For $V_{i}$ equal to zero, $V_{o}$ is also zero and both devices are off with $V_{b e}=0$. As $V_{i}$ is made positive, the base-emitter voltage of $Q_{1}$ increases until it reaches the value $V_{B E(\mathrm{on})}$, when appreciable current will start to flow in $Q_{1}$. At this point, $V_{o}$ is still approximately zero, but further increases in $V_{i}$ will cause similar increases in $V_{o}$ because $Q_{1}$ acts as an emitter follower. When $V_{i}>0, Q_{2}$ is off with a reverse bias of $V_{B E(\text { on })}$ across its base-emitter junction. As $V_{i}$ is made even more positive, $Q_{1}$ eventually saturates (for $V_{i}=V_{C C}+V_{b e 1}-V_{C E 1(\text { sat })}$ ), and the characteristic flattens out as for the conventional emitter follower considered earlier.

As $V_{i}$ is taken negative from $V_{i}=0$, a similar characteristic is obtained except that $Q_{2}$ now acts as an emitter follower for $V_{i}$ more negative than $-V_{B E(\mathrm{on})}$. In this region, $Q_{1}$ is held in the off condition with a reverse bias of $V_{B E(\text { on })}$ across its base-emitter junction.
image_name:Figure 5.11 Transfer characteristic of the Class B output stage of Fig. 5.10
description:The graph in Figure 5.11 is a transfer characteristic plot for a Class B output stage. It is a type of voltage transfer curve that maps the input voltage ($V_i$) on the horizontal axis to the output voltage ($V_o$) on the vertical axis.

1. **Axes Labels and Units:**
- The horizontal axis represents the input voltage ($V_i$), and there are no specific units mentioned, but it is typically in volts.
- The vertical axis represents the output voltage ($V_o$), also in volts.

2. **Overall Behavior and Trends:**
- The graph shows a linear region with a slope of approximately 1 between two saturation points. This linear region is centered around $V_i = 0$.
- There is a noticeable deadband or notch around $V_i = 0$, which is common in Class B amplifiers due to the need to overcome the base-emitter voltage ($V_{BE}$) of the transistors.
- The characteristic is symmetrical about the origin, indicating similar behavior for positive and negative inputs.

3. **Key Features and Technical Details:**
- The graph has two distinct saturation regions:
- For positive $V_i$, $Q_1$ saturates, and the output voltage reaches a maximum of $V_{CC} - V_{CE1(sat)}$.
- For negative $V_i$, $Q_2$ saturates, and the output voltage reaches a minimum of $-V_{CC} + V_{BE2} - V_{CE2(sat)}$.
- The linear region has two points of interest:
- When $V_i = V_{BE(on)}$, $Q_1$ turns on, and $Q_2$ turns off.
- When $V_i = -V_{BE(on)}$, $Q_1$ turns off, and $Q_2$ turns on.
- The slopes in the linear regions are approximately 1, indicating unity gain in these regions.

4. **Annotations and Specific Data Points:**
- The graph is annotated with specific conditions for $Q_1$ and $Q_2$ (on/off states) and saturation points.
- Important voltage levels are marked, such as $V_{BE(on)}$, $V_{CC}$, $V_{CE1(sat)}$, and $V_{CE2(sat)}$.

Overall, this graph illustrates the behavior of a Class B output stage, highlighting the deadband around zero input and the linear response outside this region, leading to saturation at extreme input values.

Figure 5.11 Transfer characteristic of the Class B output stage of Fig. 5.10.
image_name:Figure 5.11
description:The graph in Figure 5.11 illustrates the transfer characteristic of a Class B output stage, focusing on how the output voltage \( V_o \) relates to the input voltage \( V_i \). This graph is crucial for understanding the behavior of the Class B amplifier, particularly in relation to crossover distortion.

Type of Graph and Function:
The graph is a transfer characteristic curve, commonly used in electronics to depict the relationship between input and output voltages in an amplifier. It is presented in a linear scale.

Axes Labels and Units:
- **Horizontal Axis (\( V_i \))**: Represents the input voltage. The axis is centered around \( V_i = 0 \) and extends in both positive and negative directions.
- **Vertical Axis (\( V_o \))**: Represents the output voltage. It shows the output levels that correspond to the input voltages.

Overall Behavior and Trends:
- The graph shows a distinct deadband (or notch) around \( V_i = 0 \), characterized by a width of \( 2V_{BE(on)} \). This region indicates where the transistors are off and no output is produced, leading to crossover distortion.
- Outside the deadband, the graph displays a linear relationship between \( V_i \) and \( V_o \) until it reaches saturation points.
- At the extremes, the output voltage saturates at \( V_{CC} - V_{CE(sat)} \) for positive inputs and \( -V_{CC} + V_{CE(sat)} \) for negative inputs.

Key Features and Technical Details:
- **Deadband Width**: The deadband is \( 2V_{BE(on)} \) wide, centered around \( V_i = 0 \).
- **Saturation Levels**: The output voltage saturates at two key points:
- Positive saturation at \( V_{CC} - V_{CE(sat)} \).
- Negative saturation at \( -V_{CC} + V_{CE(sat)} \).
- The linear region outside the deadband is crucial for the amplifier's operation, allowing it to produce an output that is proportional to the input.

Annotations and Specific Data Points:
- The graph is annotated with specific conditions for saturation points and the deadband.
- Important voltage levels such as \( V_{BE(on)} \), \( V_{CC} \), \( V_{CE1(sat)} \), and \( V_{CE2(sat)} \) are marked, providing reference for the behavior of the output stage.

This transfer characteristic is fundamental in analyzing the performance of the Class B amplifier, particularly in understanding the effects of crossover distortion and the linear response of the amplifier outside the deadband region.
image_name:Figure 5.12
description:The graph in Figure 5.12 illustrates the output waveforms for various amplitude input signals applied to a Class B amplifier circuit. It is a time-domain waveform graph, showing how the output voltage \( V_o \) responds to different input voltages \( V_i \) over time.

Axes Labels and Units:
- **Horizontal Axis (bottom):** Represents input voltage \( V_i \).
- **Horizontal Axis (top):** Represents time \( t \).
- **Vertical Axis:** Represents output voltage \( V_o \).
- Units for voltage are likely in volts, and time in arbitrary units, as specific units are not marked.

Overall Behavior and Trends:
- The graph shows three different waveforms labeled as ①, ②, and ③, representing different input signal amplitudes.
- **Waveform ①:** Shows a small input signal, resulting in minimal output response due to the deadband around zero input.
- **Waveform ②:** Displays a medium input signal, leading to some output distortion as it begins to enter the linear region beyond the deadband.
- **Waveform ③:** Represents a large input signal, where the output reaches saturation levels at \( V_{CC} - V_{CE(sat)} \) and \( -V_{CC} + V_{CE(sat)} \).

Key Features and Technical Details:
- The deadband region around zero input voltage is characterized by \( 2V_{BE(on)} \), causing crossover distortion, especially visible in waveforms ① and ②.
- As the input signal increases, the output waveform transitions from a distorted response to a more linear behavior, eventually reaching saturation at higher input levels.
- The saturation levels are marked at \( V_{CC} - V_{CE(sat)} \) for positive saturation and \( -V_{CC} + V_{CE(sat)} \) for negative saturation.

Annotations and Specific Data Points:
- The horizontal lines indicate important voltage levels such as \( V_{CC} - V_{CE(sat)} \) and \( -V_{CC} + V_{CE(sat)} \).
- The notch or deadband is clearly marked and is a significant feature of the Class B output stage, contributing to the crossover distortion observed in the waveforms.

This graph effectively demonstrates the behavior of a Class B amplifier, highlighting the transition from distortion within the deadband to saturation at higher input levels, providing insight into the typical performance characteristics of such circuits.

Figure 5.12 Output waveforms for various amplitude input signals applied to the Class B circuit of Fig. 5.10.

The characteristic of Fig. 5.11 shows a notch (or deadband) of $2 V_{B E(\text { on })}$ in $V_{i}$ centered around $V_{i}=0$. This deadband is common in Class B output stages and gives rise to crossover distortion, which is illustrated in Fig. 5.12, where the output waveforms from the circuit are shown for various amplitude input sinusoidal signals. In this circuit, the distortion is high for small input signals with amplitudes somewhat larger than $V_{B E(\text { on })}$. The effect of this source of distortion diminishes as the input signal becomes larger and the deadband represents a smaller fraction of the signal amplitude. Eventually, for very large signals, saturation of $Q_{1}$ and $Q_{2}$ occurs and distortion rises sharply again due to clipping. This behavior is characteristic of Class B output stages and is why distortion figures are often quoted for both low and high output power operation.

The crossover distortion described above can be reduced by using Class $A B$ operation of the circuit. In this scheme, the active devices are biased so that each conducts a small quiescent current for $V_{i}=0$. Such biasing can be achieved as shown in Fig. 5.13, where the current source $I_{Q}$ forces bias current in diodes $Q_{3}$ and $Q_{4}$. Since the diodes are connected in parallel with the base-emitter junctions of $Q_{1}$ and $Q_{2}$, the output transistors are biased on with a current that is dependent on the area ratios of $Q_{1}, Q_{2}, Q_{3}$, and $Q_{4}$. A typical transfer characteristic for this circuit is shown in Fig. 5.14, and the deadband has been effectively eliminated. The remaining nonlinearities due to crossover in conduction from $Q_{1}$ to $Q_{2}$ can be reduced by using negative feedback, as described in Chapter 8.

The operation of the circuit in Fig. 5.13 is quite similar to that of Fig. 5.11. As $V_{i}$ is taken negative from its quiescent value, emitter follower $Q_{2}$ forces $V_{o}$ to follow. The load current flows through $Q_{2}$, whose base-emitter voltage will increase slightly. Since the diodes maintain a constant total bias voltage across the base-emitter junctions of $Q_{1}$ and $Q_{2}$, the base-emitter voltage of $Q_{1}$ will decrease by the same amount that $Q_{2}$ increased. Thus during the negative output voltage excursion, $Q_{1}$ stays on but conducts little current and plays no part in delivering
image_name:Figure 5.13 Class AB output stage
description:
[
name: IQ, type: CurrentSource, ports: {Np: +VCC, Nn: a3}
name: Q1, type: NPN, ports: {C: +VCC, B: a3, E: Vo}
name: Q2, type: PNP, ports: {C: -Vcc, B: vin, E: Vo}
name: Q3, type: Diode, ports: {Na: a3, Nc: a4}
name: Q4, type: Diode, ports: {Na: a4, Nc: vin}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
name: Vi, type: VoltageSource, ports: {Np: vin, Nn: GND}
]
extrainfo:The circuit is a Class AB output stage designed to reduce crossover distortion using diodes. Q1 and Q2 form a complementary push-pull pair to drive the load RL. The diodes Q3 and Q4 provide biasing to minimize distortion.
image_name:Figure 5.14 Transfer characteristic of the circuit of Fig. 5.13
description:The transfer characteristic graph of the Class AB output stage circuit depicted in Figure 5.13 is a plot that illustrates the relationship between the input voltage \( V_i \) and the output voltage \( V_o \). This graph is typically a piecewise linear plot that shows how the output voltage tracks the input voltage across different regions of operation.

**1. Type of Graph and Function:**
- The graph is a transfer characteristic curve, which is used to show the output response of a circuit to a given input.

**2. Axes Labels and Units:**
- The horizontal axis represents the input voltage \( V_i \), usually in volts.
- The vertical axis represents the output voltage \( V_o \), also in volts.
- Both axes are typically linear, allowing for straightforward interpretation of the circuit's response.

**3. Overall Behavior and Trends:**
- The graph shows a linear relationship between \( V_i \) and \( V_o \) in the mid-region, where the circuit operates in its linear range.
- Near zero input voltage, there is a small region where the output voltage does not change significantly, indicating the presence of crossover distortion.
- As the input voltage becomes significantly positive or negative, the output voltage follows the input more closely, showing the emitter follower action of transistors \( Q_1 \) and \( Q_2 \).

**4. Key Features and Technical Details:**
- The graph typically features two distinct slopes in the positive and negative regions, corresponding to the active regions of \( Q_1 \) and \( Q_2 \).
- The diodes in the circuit help to reduce the crossover distortion, making the transition from negative to positive output smoother.
- The slight non-linearity around the zero crossing is minimized due to the biasing provided by the diodes.

**5. Annotations and Specific Data Points:**
- Key points on the graph would include the zero crossing point, where \( V_i = 0 \), and the output voltage is slightly offset due to diode biasing.
- The slopes of the linear regions can be annotated to show the gain of the circuit in those regions.
- Any annotations would likely include markers for the transition points where the behavior shifts from one transistor conducting to the other.

Overall, this transfer characteristic graph provides a clear visualization of how the Class AB amplifier minimizes crossover distortion and ensures linear amplification across a wide range of input voltages.

Figure 5.13 Class AB output stage. The diodes reduce crossover distortion.
image_name:Figure 5.14 Transfer characteristic of the circuit of Fig. 5.13
description:The graph is a transfer characteristic plot for a Class AB amplifier. It shows the relationship between the input voltage \( V_i \) on the horizontal axis and the output voltage \( V_o \) on the vertical axis. Both axes are linearly scaled and labeled with voltage units.

Overall Behavior and Trends:
- The graph displays a linear region with a slope approximately equal to 1, indicating that the output voltage changes linearly with the input voltage over a certain range.
- There are two distinct regions where the behavior of the circuit changes, corresponding to the conduction shift between transistors.

Key Features and Technical Details:
- The graph has two horizontal asymptotes at the top and bottom, representing saturation limits of the output voltage:
- The upper asymptote is labeled \( V_{CC} - V_{CE1} (\text{sat}) \).
- The lower asymptote is labeled \( -V_{CC} + |V_{CE2} (\text{sat})| \).
- The linear region intersects the vertical axis at the origin, and the slope of this region is approximately 1, indicating linear amplification.
- A marked point on the horizontal axis is labeled \(-V_{BE2}\), indicating the transition point where the behavior shifts from one transistor conducting to the other.

Annotations and Specific Data Points:
- The transition point \(-V_{BE2}\) is annotated, highlighting the shift in conduction between the transistors.
- The saturation points at \( V_{CC} - V_{CE1} (\text{sat}) \) and \(-V_{CC} + |V_{CE2} (\text{sat})| \) indicate the limits of linear operation.

This graph effectively illustrates how the Class AB amplifier minimizes crossover distortion by maintaining linear amplification across a wide range of input voltages, with specific regions dedicated to each transistor's conduction.

Figure 5.14 Transfer characteristic of the circuit of Fig. 5.13.
output power. For $V_{i}$ taken positive, the opposite occurs, and $Q_{1}$ acts as the emitter follower delivering current to $R_{L}$ with $Q_{2}$ conducting only a very small current. In this case, the current source $I_{Q}$ supplies the base-current drive to $Q_{1}$.

In the derivation of the characteristics of Figures 5.11 and 5.14, we assumed that the magnitude of the input voltage $V_{i}$ was unlimited. In the characteristic of Fig. 5.11, the magnitude of $V_{i}$ required to cause saturation of $Q_{1}$ or $Q_{2}$ exceeds the supply voltage $V_{C C}$. However, as in the case of the single emitter follower described earlier, practical driver stages generally cannot produce values of $V_{i}$ exceeding $V_{C C}$ if they are connected to the same supply voltages as the output stage. For example, the current source $I_{Q}$ in Fig. 5.13 is usually realized with a pnp transistor and thus the voltage at the base of $Q_{1}$ cannot exceed $\left(V_{C C}-V_{C E(\mathrm{sat})}\right)$, at which point saturation of the current-source transistor occurs. Consequently, the positive and negative limits of $V_{o}$ where clipping occurs are generally somewhat less than shown in Fig. 5.11 and Fig. 5.14, and the limitation usually occurs in the driver stage. This point will be investigated further when practical output stages are considered in later sections.

### 5.4.2 Power Output and Efficiency of the Class B Stage

The method of operation of a Class B stage can be further appreciated by plotting the collector current waveforms in the two devices, as in Fig. 5.15, where crossover distortion is ignored. Note that each transistor conducts current to $R_{L}$ for half a cycle.
image_name:(a)
description:The graph labeled \((a)\) is a time-domain waveform representing the input voltage \(V_i\) for a Class B output stage. The graph is a sinusoidal waveform plotted against time \(t\), with one complete cycle shown over the period \(T\). The vertical axis represents the input voltage \(V_i\), while the horizontal axis represents time \(t\). No specific units are provided for the axes, but the waveform is periodic with a regular sinusoidal shape.

Type of Graph and Function:
- The graph is a time-domain waveform showing a sinusoidal input voltage.

Axes Labels and Units:
- Vertical Axis: Input Voltage \(V_i\).
- Horizontal Axis: Time \(t\).
- No specific units are indicated, and the scale appears linear.

Overall Behavior and Trends:
- The waveform is sinusoidal, indicating periodic behavior with a consistent amplitude and frequency.
- The graph shows one complete cycle of the sinusoid, starting from zero, peaking at the maximum positive amplitude, returning to zero, reaching the maximum negative amplitude, and then returning to zero again by the end of the period \(T\).

Key Features and Technical Details:
- The waveform has two peaks: one positive and one negative, symmetrically distributed around the zero voltage level.
- The waveform crosses the zero line twice per cycle, indicating zero crossings.

Annotations and Specific Data Points:
- The period \(T\) is marked on the horizontal axis, showing the duration of one complete cycle.
- No specific numerical values or additional annotations are provided in this graph.
image_name:(b)
description:The graph labeled as "(b)" in Figure 5.15 represents the output voltage waveform ($V_o$) of a Class B output stage over time. This is a time-domain waveform illustrating the behavior of the output voltage in response to an input signal.

1. **Axes Labels and Units:**
- The horizontal axis represents time ($t$) and is marked with a period $T$, indicating the time duration of one complete cycle of the waveform.
- The vertical axis represents the output voltage ($V_o$) with unspecified units, but typically in volts.

2. **Overall Behavior and Trends:**
- The waveform is sinusoidal, indicating that the output voltage varies sinusoidally over time.
- The waveform completes one full cycle over the period $T$, showing a positive half-cycle followed by a negative half-cycle.
- There is symmetry in the waveform, with the positive and negative halves being mirror images, typical of sinusoidal signals.

3. **Key Features and Technical Details:**
- The peak value of the output voltage is denoted as $\hat{V}_o$, which is the maximum amplitude reached by the waveform.
- The waveform crosses the time axis (zero voltage) twice within one period, indicating zero crossings at the start and midpoint of the period.

4. **Annotations and Specific Data Points:**
- A dashed line denotes the peak voltage $\hat{V}_o$, highlighting the maximum amplitude of the waveform.
- The waveform is consistent with the typical behavior of a Class B amplifier output, where each transistor conducts for half of the cycle, resulting in a full sinusoidal output when combined.
image_name:(c)
description:The graph labeled (c) represents the collector current waveform for transistor $Q_{1}$ in a Class B output stage. This is a time-domain waveform.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform showing the collector current $I_{c1}$ of transistor $Q_{1}$.

2. **Axes Labels and Units:**
- The horizontal axis represents time ($t$) and is marked with a period $T$ indicating one full cycle.
- The vertical axis represents the collector current $I_{c1}$.

3. **Overall Behavior and Trends:**
- The waveform is a half-sinusoid, indicating that transistor $Q_{1}$ conducts current for half of the cycle.
- The waveform starts at zero, rises to a peak, and returns to zero, completing its conduction over half the period $T$.

4. **Key Features and Technical Details:**
- The peak of the waveform is annotated as $\hat{I}_o = \frac{\hat{V}_o}{R_L}$, which represents the peak output current related to the peak output voltage $\hat{V}_o$ and load resistance $R_L$.
- The waveform is symmetric about the time axis for the conducting half-cycle, indicating no DC offset.

5. **Annotations and Specific Data Points:**
- The peak current value is specifically highlighted, showing the relationship between output voltage and load resistance.
- The graph is periodic with a period $T$, consistent with sinusoidal operation in a Class B amplifier.
image_name:(d)
description:The graph labeled (d) in Figure 5.15 represents the collector current waveform for transistor $Q_2$ in a Class B output stage. This is a time-domain waveform showing how the current $I_{c2}$ varies over one complete cycle of the input signal.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform depicting the collector current $I_{c2}$.

2. **Axes Labels and Units:**
- The horizontal axis represents time $t$, with a period $T$ indicated for one full cycle.
- The vertical axis represents the collector current $I_{c2}$.
- Units for time and current are not explicitly provided but are typically in seconds and amperes, respectively.

3. **Overall Behavior and Trends:**
- The waveform is a half-sinusoidal shape, indicating that $I_{c2}$ conducts for half of the input signal cycle.
- The current is negative over its conducting period, reflecting the operation of the transistor $Q_2$ in the Class B stage.
- The waveform starts at zero, dips to a negative peak, and returns to zero, completing the half-cycle.

4. **Key Features and Technical Details:**
- The peak current value is denoted as $-\hat{I}_o$, which equals $-\frac{\hat{V}_o}{R_L}$, where $\hat{V}_o$ is the peak output voltage and $R_L$ is the load resistance.
- The waveform is symmetric about the time axis, indicating no DC offset in the conducting period.

5. **Annotations and Specific Data Points:**
- The negative peak value is explicitly annotated on the graph as $-\hat{I}_o = -\frac{\hat{V}_o}{R_L}$.
- The graph is marked with vertical dashed lines to indicate the period $T$ of the waveform.

This waveform illustrates the typical behavior of a Class B amplifier where each transistor conducts for half of the cycle, with $Q_2$ conducting during the negative half-cycle of the input signal.

Figure 5.15 Voltage and current waveforms for a Class B output stage. (a) Input voltage. (b) Output voltage. (c) $Q_{1}$ collector current. (d) $Q_{2}$ collector current.

The collector current waveforms of Fig. 5.15 also represent the waveforms of the current drawn from the two supplies. If the waveforms are assumed to be half-sinusoids, then the average current drawn from the $+V_{C C}$ supply is

$$
\begin{equation*}
I_{\text {supply }}=\frac{1}{T} \int_{0}^{T} I_{c 1}(t) d t=\frac{1}{T} \int_{0}^{T / 2} \frac{\hat{V}_{o}}{R_{L}} \sin \left(\frac{2 \pi t}{T}\right) d t=\frac{1}{\pi} \frac{\hat{V}_{o}}{R_{L}}=\frac{1}{\pi} \hat{I}_{o} \tag{5.66}
\end{equation*}
$$

where $T$ is the period of the input signal. Also, $\hat{V}_{o}$ and $\hat{I}_{o}$ are the zero-to-peak amplitudes of the output sinusoidal voltage and current. Since each supply delivers the same current magnitude, the total average power drawn from the two supplies is

$$
\begin{equation*}
P_{\text {supply }}=2 V_{C C} I_{\text {supply }}=\frac{2}{\pi} \frac{V_{C C}}{R_{L}} \hat{V}_{o} \tag{5.67}
\end{equation*}
$$

where (5.66) has been substituted. Unlike in the Class A case, the average power drawn from the supplies does vary with signal level for a Class B stage, and is directly proportional to $\hat{V}_{o}$.

The average power delivered to $R_{L}$ is given by

$$
\begin{equation*}
P_{L}=\frac{1}{2} \frac{\hat{V}_{o}^{2}}{R_{L}} \tag{5.68}
\end{equation*}
$$

From the definition of circuit efficiency in (5.13),

$$
\begin{equation*}
\eta_{C}=\frac{P_{L}}{P_{\text {supply }}}=\frac{\pi}{4} \frac{\hat{V}_{o}}{V_{C C}} \tag{5.69}
\end{equation*}
$$

where (5.67) and (5.68) have been substituted. Equation 5.69 shows that $\eta$ for a Class B stage is independent of $R_{L}$ but increases linearly as the output voltage amplitude $\hat{V}_{o}$ increases.

The maximum value that $\hat{V}_{o}$ can attain before clipping occurs with the characteristic of Fig. 5.14 is $\hat{V}_{o m}=\left(V_{C C}-V_{C E(\text { sat })}\right)$ and thus the maximum average signal power that can be delivered to $R_{L}$ for sinusoidal signals can be calculated from (5.68) as

$$
\begin{equation*}
\left.P_{L}\right|_{\max }=\frac{1}{2} \frac{\left[V_{C C}-V_{C E(\mathrm{sat})}\right]^{2}}{R_{L}} \tag{5.70}
\end{equation*}
$$

From (5.69), the corresponding maximum efficiency is

$$
\begin{equation*}
\eta_{\max }=\frac{\pi}{4}\left(\frac{V_{C C}-V_{C E(\mathrm{sat})}}{V_{C C}}\right) \tag{5.71}
\end{equation*}
$$

If $V_{C E(\text { sat })}$ is small compared with $V_{C C}$, the circuit has a maximum efficiency of 0.786 or 78.6 percent. This maximum efficiency is much higher than the value of 25 percent achieved in Class A circuits. In addition, the standby power dissipation is essentially zero in the Class B circuit. These advantages explain the widespread use of Class B and Class AB output stages.

The load line for one device in a Class B stage is shown in Fig. 5.16. For values of $V_{c e}$ less than the quiescent value (which is $V_{C C}$ ), the load line has a slope of $\left(-1 / R_{L}\right)$. For values of $V_{c e}$ greater than $V_{C C}$, the load line lies along the $V_{c e}$ axis because the device under consideration turns off and the other device conducts. As a result, the $V_{c e}$ of the device under consideration increases while its collector current is zero. The maximum value of $V_{c e}$ is $\left(2 V_{C C}-V_{C E(\mathrm{sat})}\right)$. As in the case of a Class A stage, a geometrical interpretation of the average power $P_{L}$ delivered to $R_{L}$ can be obtained by noting that $P_{L}=\frac{1}{2} \hat{I}_{o} \hat{V}_{o}$, where $\hat{I}_{o}$ and $\hat{V}_{o}$ are the peak sinusoidal current and voltage delivered to $R_{L}$. Thus $P_{L}$ is the area of the triangle in Fig. 5.16 between the $V_{c e}$ axis and the portion of the load line traversed by the operating point.
image_name:Figure 5.16
description:The graph in Figure 5.16 is a load line diagram for a device in a Class B amplifier stage. It is a plot on the Cartesian plane with the horizontal axis labeled as \( V_{ce} \) (collector-emitter voltage) and the vertical axis labeled as \( I_c \) (collector current). Both axes are assumed to be in linear scale, though specific units are not provided.

Axes and Units:
- **Horizontal Axis (\( V_{ce} \))**: Represents the collector-emitter voltage. Important points on this axis include \( V_{CE(sat)} \), \( \frac{V_{CC}}{2} \), \( V_{CC} \), and \( 2V_{CC} - V_{CE(sat)} \).
- **Vertical Axis (\( I_c \))**: Represents the collector current. A critical value noted on this axis is \( \frac{V_{CC}}{R_L} \).

Key Features:
- **Load Line**: The load line is a straight line with a negative slope of \(-\frac{1}{R_L}\), indicating the relationship between \( V_{ce} \) and \( I_c \) for the load resistance \( R_L \).
- **Quiescent Point (Q)**: This point represents the operating point of the amplifier when no input signal is present. It is marked along the load line.
- **Peak Device Dissipation**: The line \( P = I_c V_{ce} = \text{constant} \) marks the maximum power dissipation in the device, shown as a horizontal line.

Behavior and Trends:
- The load line intersects the \( V_{ce} \) axis at \( V_{CC} \) and the \( I_c \) axis at \( \frac{V_{CC}}{R_L} \), indicating the maximum voltage and current conditions, respectively.
- The diagram indicates the region of operation for the device, bounded by the load line and the maximum power dissipation line.

Annotations:
- **\( V_{CE(sat)} \)**: The saturation voltage where the collector-emitter voltage is minimized.
- **\( 2V_{CC} - V_{CE(sat)} \)**: A significant point indicating the maximum swing of \( V_{ce} \) in the positive direction.

This load line analysis helps in understanding the power delivered to the load \( R_L \) and the power dissipated in the device, providing insights into the efficiency and performance of the Class B amplifier stage.

Figure 5.16 Load line for one device in a Class B stage.

Consider the instantaneous power dissipated in one device:

$$
\begin{equation*}
P_{c}=V_{c e} I_{c} \tag{5.72}
\end{equation*}
$$

But

$$
\begin{equation*}
V_{c e}=V_{C C}-I_{c} R_{L} \tag{5.73}
\end{equation*}
$$

Substitution of (5.73) in (5.72) gives

$$
\begin{equation*}
P_{c}=I_{c}\left(V_{C C}-I_{c} R_{L}\right)=I_{c} V_{C C}-I_{c}^{2} R_{L} \tag{5.74}
\end{equation*}
$$

Differentiation of (5.74) shows that $P_{c}$ reaches a peak for

$$
\begin{equation*}
I_{c}=\frac{V_{C C}}{2 R_{L}} \tag{5.75}
\end{equation*}
$$

This peak lies on the load line midway between the $I_{c}$ and $V_{c e}$ axis intercepts and agrees with the result derived earlier for the Class A stage. As in that case, the load line in Fig. 5.16 is tangent to a power hyperbola at the point of peak dissipation. Thus, in a Class B stage, maximum instantaneous device dissipation occurs for an output voltage equal to about half the maximum swing. Since the quiescent device power dissipation is zero, the operating temperature of a Class B device always increases when nonzero signal is applied.

The instantaneous device power dissipation as a function of time is shown in Fig. 5.17, where collector current, collector-emitter voltage, and their product are displayed for one device in a Class B stage at maximum output. (Crossover distortion is ignored, and $V_{C E(\mathrm{sat})}=0$ is assumed.) When the device conducts, the power dissipation varies at twice the signal frequency. The device power dissipation is zero for the half cycle when the device is cut off. For an open-circuited load, the load line in Fig. 5.16 lies along the $V_{c e}$ axis and the device has zero
image_name:(a)
description:The graph labeled "(a)" in the image represents the collector current waveform for one device in a Class B amplifier stage at maximum output. This is a time-domain waveform, displaying how the collector current \(I_{c1}\) varies over time \(t\).

Axes Labels and Units:
- **Vertical Axis:** Represents the collector current \(I_{c1}\) with a maximum value of \(\frac{V_{CC}}{R_L}\).
- **Horizontal Axis:** Represents time \(t\), although specific units are not provided, it is typically in seconds or milliseconds for such waveforms.

Overall Behavior and Trends:
- The waveform is sinusoidal, indicating that the collector current varies periodically over time.
- The waveform has a peak value of \(\frac{V_{CC}}{R_L}\), with the current reaching zero at the midpoints between peaks.
- The waveform is consistent with the operation of a Class B amplifier, where the device conducts for half of the input signal cycle and is cut off for the other half.

Key Features and Technical Details:
- The waveform starts at zero, rises to a peak of \(\frac{V_{CC}}{R_L}\), and returns to zero, completing one half-cycle.
- This is followed by a period where the current remains at zero, corresponding to the cutoff period of the Class B operation.
- The cycle then repeats, showing the periodic nature of the waveform.

Annotations and Specific Data Points:
- The peak current value is explicitly marked as \(\frac{V_{CC}}{R_L}\), indicating the maximum conduction level.
- The zero crossings and peak points are critical for understanding the conduction and cutoff periods in Class B operation.

This waveform is essential for analyzing the performance and efficiency of the Class B amplifier, particularly in understanding how the current changes during the conduction period and how it affects power dissipation in the device.
image_name:(b)
description:The graph labeled "(b)" is a time-domain waveform illustrating the collector-emitter voltage ($V_{ce1}$) in a Class B amplifier stage. The horizontal axis represents time ($t$), while the vertical axis represents the collector-emitter voltage, labeled as $V_{ce1}$. The voltage is measured in volts, and there are two significant voltage levels marked: $V_{CC}$ and $2V_{CC}$.

**Overall Behavior and Trends:**
- The waveform is sinusoidal and periodic, demonstrating a full cycle of oscillation. This represents the voltage variation across the collector-emitter junction during operation.
- The waveform oscillates between $V_{CC}$ and $2V_{CC}$, indicating that the peak voltage reaches twice the supply voltage ($V_{CC}$).
- The waveform has a consistent amplitude and period, characteristic of sinusoidal signals in amplifier circuits.

**Key Features and Technical Details:**
- The waveform crosses the $V_{CC}$ level at the midpoint of each half-cycle, indicating a transition point where the voltage rises above the supply voltage during the positive half-cycle and falls below during the negative half-cycle.
- There are no zero crossings since the waveform does not dip below $V_{CC}$.
- The peaks of the waveform occur at $2V_{CC}$, which is the maximum voltage level reached during operation.

**Annotations and Specific Data Points:**
- The graph is annotated with $V_{CC}$ and $2V_{CC}$, which are key voltage levels for understanding the operation of the Class B amplifier.
- The periodicity of the waveform suggests it is synchronized with the input signal frequency, doubling the frequency of the power dissipation waveform as described in the context.

This waveform is crucial for understanding how the voltage across the collector-emitter junction varies with time, particularly in a Class B amplifier stage where the device conducts for one half of the input signal cycle.
image_name:(c)
description:The graph in Figure 5.17(c) represents the collector power dissipation waveform for one device in a Class B amplifier stage at maximum output. This is a time-domain waveform illustrating how the power dissipation varies over time.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform depicting power dissipation.

2. **Axes Labels and Units:**
- The horizontal axis represents time \( t \) (units not specified, but typically in seconds or milliseconds).
- The vertical axis represents power dissipation \( P_{c1} = I_{c1} V_{ce1} \) (units not specified, but typically in watts).
- The scale is linear.

3. **Overall Behavior and Trends:**
- The waveform shows a periodic pattern, with power dissipation occurring in bursts.
- The power dissipation is zero during the half-cycle when the device is cut off, and it rises sharply during the conduction phase.
- The waveform has a frequency that is twice the signal frequency, indicating that power dissipation occurs at twice the rate of the input signal frequency.

4. **Key Features and Technical Details:**
- The peaks of the waveform reach a maximum power dissipation value of \( \frac{V_{CC}^2}{4R_L} \), as indicated by the horizontal dashed line.
- The waveform consists of sharp, narrow peaks separated by intervals of zero power dissipation.
- The waveform reflects the behavior of a Class B amplifier, where power is dissipated only during the conduction phase.

5. **Annotations and Specific Data Points:**
- The peak power dissipation value is clearly marked on the vertical axis with a dashed line.
- There are no specific numerical data points annotated, but the maximum power dissipation value is derived from the given expression.

This graph effectively illustrates the power dissipation characteristics in a Class B amplifier, with power being dissipated only when the device is conducting, leading to a waveform with twice the frequency of the input signal.

Figure 5.17 Waveforms at maximum output for one device in a Class B stage.
(c) (a) Collector current waveform.
(b) Collector voltage waveform.
(c) Collector power dissipation waveform.
dissipation. As in the case of Class A stage, the load line in Fig. 5.16 becomes vertical through the quiescent point for a short-circuited load, and the instantaneous device power dissipation can then become excessive. Methods of protection against such a possibility are described in Section 5.4.6.

#### EXAMPLE

A Class B stage of the type shown in Fig. 5.10 drives a load $R_{L}=500 \Omega$. If the positive and negative supplies have magnitudes of 15 V , calculate the maximum average power that is delivered to $R_{L}$ for $\hat{V}_{o}=14.4 \mathrm{~V}$, the corresponding efficiency, and the maximum instantaneous device dissipation. Assume that $V_{o}$ is sinusoidal.

From (5.66), the average of supply current is

$$
I_{\text {supply }}=\frac{1}{\pi} \frac{\hat{V}_{o}}{R_{L}}=\frac{1}{\pi} \frac{14.4}{500}=9.17 \mathrm{~mA}
$$

Use of (5.67) gives the average power drawn from the supplies as

$$
P_{\text {supply }}=I_{\text {supply }} \times 2 V_{C C}=9.17 \times 30 \mathrm{~mW}=275 \mathrm{~mW}
$$

From (5.68), the average power delivered to $R_{L}$ is

$$
P_{L}=\frac{1}{2} \frac{\hat{V}_{o}^{2}}{R_{L}}=\frac{1}{2} \frac{14.4^{2}}{500}=207 \mathrm{~mW}
$$

From (5.13), the corresponding efficiency is

$$
\eta_{C}=\frac{P_{L}}{P_{\text {supply }}}=\frac{207}{275}=75.3 \text { percent }
$$

This result is close to the theoretical maximum of 78.6 percent. From (5.75), the maximum instantaneous device power dissipation occurs when

$$
I_{c}=\frac{V_{C C}}{2 R_{L}}=\frac{15 \mathrm{~V}}{1000 \Omega}=15 \mathrm{~mA}
$$

The corresponding value of $V_{c e}$ is $V_{C C} / 2=7.5 \mathrm{~V}$ and thus the maximum instantaneous device dissipation is

$$
P_{c}=I_{c} V_{c e}=15 \times 7.5 \mathrm{~mW}=112.5 \mathrm{~mW}
$$

By conservation of power, the average power dissipated per device is

$$
P_{\mathrm{av}}=\frac{1}{2}\left(P_{\text {supply }}-P_{L}\right)=\frac{1}{2}(275-207) \mathrm{mW}=34 \mathrm{~mW}
$$

### 5.4.3 Practical Realizations of Class B Complementary Output Stages ${ }^{6}$

The practical aspects of Class B output-stage design will now be illustrated by considering two examples. One of the simplest realizations is the output stage of the 709 op amp , and a simplified schematic of this is shown in Fig. 5.18. Transistor $Q_{3}$ acts as a common-emitter driver stage for output devices $Q_{1}$ and $Q_{2}$.

The transfer characteristic of this stage can be calculated as follows. In the quiescent condition, $V_{o}=0$ and $V_{1}=0$. Since $Q_{1}$ and $Q_{2}$ are then off, there is no base current in these devices. Therefore, for $V_{C C}=10 \mathrm{~V}$, the bias current in $Q_{3}$ is

$$
I_{C 3}=\frac{V_{C C}-V_{1}}{R_{1}}=\frac{V_{C C}}{R_{1}}=\frac{10 \mathrm{~V}}{20 \mathrm{k} \Omega}=0.50 \mathrm{~mA}
$$

image_name:Figure 5.18 Simplified schematic of the output stage of the 709 op amp
description:
[
name: R1, type: Resistor, value: 20kΩ, ports: {N1: VCC, N2: V1}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
name: Q1, type: NPN, ports: {C: VCC, B: V1, E: Vo}
name: Q2, type: PNP, ports: {C: -VCC, B: V1, E: Vo}
name: Q3, type: NPN, ports: {C: V1, B: Vi, E: -VCC}
]
extrainfo:Q3 acts as a common-emitter driver stage for output devices Q1 and Q2. The circuit is part of the output stage of the 709 op amp. It operates with a bias current of 0.50 mA in Q3 when quiescent. The limiting values of Vo are determined by the driver stage.

Figure 5.18 Simplified schematic of the output stage of the 709 op amp.

The limiting values that $V_{o}$ can take are determined by the driver stage. When $V_{i}$ is taken large positive, $V_{1}$ decreases until $Q_{3}$ saturates, at which point the negative voltage limit $V_{o}^{-}$is reached:

$$
\begin{equation*}
V_{o}^{-}=-V_{C C}+V_{C E 3(\mathrm{sat})}-V_{b e 2} \tag{5.76}
\end{equation*}
$$

For values of $V_{1}$ between $\left(-V_{C C}+V_{C E 3(\mathrm{sat})}\right)$ and $\left(-V_{B E(\mathrm{on})}\right)$, both $Q_{3}$ and $Q_{2}$ are in the forward-active region, and $V_{o}$ follows $V_{1}$ with $Q_{2}$ acting as an emitter follower.

As $V_{i}$ is taken negative, the current in $Q_{3}$ decreases and $V_{1}$ rises, turning $Q_{1}$ on. The positive voltage limit $V_{o}^{+}$is reached when $Q_{3}$ cuts off and the base of $Q_{1}$ is simply fed from the positive supply via $R_{1}$. Then

$$
\begin{equation*}
V_{C C}=I_{b 1} R_{1}+V_{b e 1}+V_{o}^{+} \tag{5.77}
\end{equation*}
$$

If $\beta_{F 1}$ is large then

$$
V_{o}^{+}=I_{c 1} R_{L}=\beta_{F 1} I_{b 1} R_{L}
$$

where $\beta_{F 1}$ is the current gain of $Q_{1}$. Thus

$$
\begin{equation*}
I_{b 1}=\frac{V_{o}^{+}}{\beta_{F 1} R_{L}} \tag{5.78}
\end{equation*}
$$

Substituting (5.78) in (5.77) and rearranging gives

$$
\begin{equation*}
V_{o}^{+}=\frac{V_{C C}-V_{b e 1}}{1+\frac{R_{1}}{\beta_{F 1} R_{L}}} \tag{5.79}
\end{equation*}
$$

For $R_{L}=10 \mathrm{k} \Omega$ and $\beta_{F 1}=100$, (5.79) gives

$$
V_{o}^{+}=0.98\left(V_{C C}-V_{b e 1}\right)
$$

In this case, the limit on $V_{o}$ is similar for positive and negative swings. However, if $R_{L}=1 \mathrm{k} \Omega$ and $\beta_{F 1}=100$, (5.79) gives

$$
V_{o}^{+}=0.83\left(V_{C C}-V_{b e 1}\right)
$$

image_name:Figure 5.19
description:The graph depicted in Figure 5.19 is a transfer characteristic curve, showing the relationship between the output voltage \( V_o \) and the input voltage \( V_i \) for a given circuit. The graph features two curves, each corresponding to a different load resistance \( R_L \): one for \( R_L = 1 \text{k}\Omega \) and another for \( R_L = 10 \text{k}\Omega \).

Axes Labels and Units:
- The horizontal axis represents the input voltage \( V_i \) in volts, ranging from 0.60 V to 0.66 V.
- The vertical axis represents the output voltage \( V_o \) in volts, ranging from -9 V to 6 V.

Overall Behavior and Trends:
- Both curves show a non-linear relationship between \( V_i \) and \( V_o \), with the output voltage decreasing as the input voltage increases.
- The curve for \( R_L = 10 \text{k}\Omega \) (dashed line) lies above the curve for \( R_L = 1 \text{k}\Omega \) (solid line), indicating a higher output voltage for the same input voltage when the load resistance is higher.

Key Features and Technical Details:
- The curves exhibit a steep decline, especially pronounced as \( V_i \) approaches 0.64 V, indicating a rapid change in output voltage.
- The maximum output voltage for \( R_L = 10 \text{k}\Omega \) is around 6 V, while for \( R_L = 1 \text{k}\Omega \), it is approximately 3 V.
- Clipping occurs for \( R_L = 1 \text{k}\Omega \) at lower input voltages, illustrating reduced output voltage swing compared to \( R_L = 10 \text{k}\Omega \).

Annotations and Specific Data Points:
- Both curves intersect the \( V_i \) axis near 0.63 V, which seems to be a critical point for the operation of the circuit.
- The graph visually demonstrates the effect of load resistance on the output characteristics, emphasizing how a lower load resistance reduces the maximum achievable output voltage and leads to earlier clipping.

Figure 5.19 SPICE-generated transfer characteristic for the circuit of Fig. 5.18 with $V_{C C}=10 \mathrm{~V}$ and $R_{L}=1 \mathrm{k} \Omega$ and $10 \mathrm{k} \Omega$.

For this lower value of $R_{L}$, the maximum positive value of $V_{o}$ is reduced, and clipping on a sine wave occurs first for $V_{o}$ going positive.

Computer-generated transfer curves using SPICE for this circuit with $V_{C C}=10 \mathrm{~V}$ are shown in Fig. 5.19 for $R_{L}=1 \mathrm{k} \Omega$ and $R_{L}=10 \mathrm{k} \Omega$. ( $\beta_{F}=100$ is assumed for all devices.) The reduced positive voltage capability for $R_{L}=1 \mathrm{k} \Omega$ is apparent, as is the deadband present in the transfer characteristic. The curvature in the characteristic is due to the exponential nonlinearity of the driver $Q_{3}$. In practice, the transfer characteristic may be even more nonlinear than shown in Fig. 5.19 because $\beta_{F}$ for the $n p n$ transistor $Q_{1}$ is generally larger than $\beta_{F}$ for the pnp transistor $Q_{2}$, causing the positive and negative sections of the characteristic to differ significantly. This behavior can be seen by calculating the small-signal gain $\Delta V_{o} / \Delta V_{i}$ for positive and negative $V_{o}$. In the actual 709 integrated circuit, negative feedback is applied around this output stage to reduce these nonlinearities in the transfer characteristic.

A second example of a practical Class B output stage is shown Fig. 5.20, where SPICEcalculated bias currents are included. This circuit is a simplified schematic of the 741 op amp output circuitry. The output devices $Q_{14}$ and $Q_{20}$ are biased to a collector current of about 0.17 mA by the diodes $Q_{18}$ and $Q_{19}$. The value of the bias current in $Q_{14}$ and $Q_{20}$ depends on the effective area ratio between diodes $Q_{18}$ and $Q_{19}$ and the output devices. ( $Q_{18}$ and $Q_{19}$ are implemented with transistors in practice.) The output stage is driven by lateral $p n p$ emitter-follower $Q_{23}$, which is driven by common-emitter stage $Q_{17}$ biased to 0.68 mA by current source $Q_{13 \mathrm{~B}}$.

The diodes in Fig. 5.20 essentially eliminate crossover distortion in the circuit, which can be seen in the SPICE-generated transfer characteristic of Fig. 5.21. The linearity of this stage is further improved by the fact that the output devices are driven from a low resistance provided by the emitter follower $Q_{23}$. Consequently, differences in $\beta_{F}$ between $Q_{14}$ and $Q_{20}$ produce little effect on the transfer characteristic because small-signal gain $\Delta V_{o} / \Delta V_{1} \simeq 1$ for any practical value of $\beta_{F}$ with either $Q_{14}$ or $Q_{20}$ conducting.

The limits on the output voltage swing shown in Fig. 5.21 can be determined as follows. As $V_{i}$ is taken positive, the voltage $V_{1}$ at the base of $Q_{23}$ goes negative, and voltages $V_{2}$ and
image_name:Figure 5.20 (a)
description:The circuit is a simplified schematic of the 741 op amp output stage. It includes a push-pull amplifier configuration with transistors Q14 and Q20. The diagram shows the current paths and biasing setup for the output stage, including the feedback and load connections.
image_name:Figure 5.20 (b)
description:The circuit is the output stage of a 741 operational amplifier. It includes a complementary push-pull output stage with transistors Q14 and Q20. The circuit is designed to drive a load resistor RL connected to ground. The biasing and current mirror configurations help stabilize the output stage.

Figure 5.20 (a) Simplified schematic of the 741 op amp output stage. (b) Schematic of the 741 output stage showing the detail of $Q_{18}$ and $Q_{19}$.
$V_{o}$ follow with $Q_{20}$ drawing current from $R_{L}$. When $Q_{17}$ saturates, the output voltage limit for negative excursions is reached at

$$
\begin{equation*}
V_{o}^{-}=-V_{C C}+V_{C E 17(\mathrm{sat})}-V_{b e 23}-V_{b e 20} \tag{5.80}
\end{equation*}
$$

This limit is about 1.4 V more positive than the negative supply. Thus $V_{o}^{-}$is limited by saturation in $Q_{17}$, which is the stage preceding driver stage $Q_{23}$.

As $V_{i}$ is taken negative from its quiescent value (where $V_{o}=0$ ), voltage $V_{1}$ rises and voltages $V_{2}$ and $V_{o}$ follow with $Q_{14}$ delivering current to the load. The positive output voltage
image_name:Figure 5.21
description:The graph in Figure 5.21 is a transfer curve illustrating the relationship between input voltage \( V_i \) and output voltage \( V_o \). The x-axis represents the input voltage \( V_i \) in volts, ranging from approximately 0.625 V to 0.665 V. The y-axis represents the output voltage \( V_o \) in volts, ranging from -16 V to 16 V.

Overall Behavior and Trends:
- The graph shows a sharp transition between two saturation regions, indicating the behavior of a nonlinear amplifier or a similar device.
- For input voltages \( V_i \) less than approximately 0.64 V, the output voltage \( V_o \) is saturated at a high level of approximately 14.2 V.
- As the input voltage \( V_i \) increases past 0.64 V, the output voltage \( V_o \) decreases sharply.
- The transition occurs over a narrow range of input voltages, centered around 0.645 V.
- For input voltages \( V_i \) greater than approximately 0.65 V, the output voltage \( V_o \) saturates at a low level of approximately -13.6 V.

Key Features:
- **Saturation Levels:** The output voltage \( V_o \) reaches a positive saturation level of 14.2 V and a negative saturation level of -13.6 V.
- **Transition Region:** The steep transition occurs around an input voltage of 0.645 V.

Annotations and Specific Data Points:
- The graph is annotated with the saturation levels 14.2 V and -13.6 V, indicating the limits of the output voltage.
- The transition is characterized by a nearly vertical slope, suggesting a high gain in this region.

This transfer curve is typical of a device like an operational amplifier operating in a nonlinear region, where the output switches between saturation levels as the input crosses a threshold.

Figure 5.21 SPICE-generated transfer curve for the circuit of Fig. $5.20 a$ with $V_{C C}=15 \mathrm{~V}$ and $R_{L}=1 \mathrm{k} \Omega$.
limit $V_{o}^{+}$is reached when current source $Q_{13 \mathrm{~A}}$ saturates and

$$
\begin{equation*}
V_{o}^{+}=V_{C C}+V_{C E 13 \mathrm{~A}(\mathrm{sat})}-V_{b e 14} \tag{5.81}
\end{equation*}
$$

This limit is about 0.8 V below the positive supply because $V_{C E 13 \mathrm{~A}(\mathrm{sat})} \simeq-0.1 \mathrm{~V}$ for the $p n p$ device. Thus $V_{o}^{+}$is also limited by the driver stage.

The power requirements of the driver circuits in a configuration such as shown in Fig. 5.20 require some consideration. The basic requirement of the driver is to supply sufficient drive to the output stage so that it can supply the desired power to $R_{L}$. As $V_{o}$ is taken negative, $Q_{23}$ draws current from the base of $Q_{20}$ with essentially no limit. In fact, the circuit must be protected in case of a short-circuited load. Otherwise in this case, a large input signal could cause $Q_{23}$ and $Q_{20}$ to conduct such heavy currents that they burn out. As explained before, the negative voltage limit is reached when $Q_{17}$ saturates and can no longer drive the base of $Q_{23}$ negative.

As $V_{o}$ is taken positive (by $V_{i}$ going negative and $V_{1}$ going positive), $Q_{23}$ conducts less, and current source $Q_{13 \mathrm{~A}}$ supplies base current to $Q_{14}$. The maximum output current is limited by the current of 0.22 mA available for driving $Q_{14}$. As $V_{1}, V_{2}$, and $V_{o}$ go positive, the current in $Q_{14}$ increases, and the current in $Q_{13 \mathrm{~A}}$ is progressively diverted to the base of $Q_{14}$. The maximum possible output current delivered by $Q_{14}$ is thus

$$
I_{o}=\beta_{F 14} \times 0.22 \mathrm{~mA}
$$

If $\beta_{F 14}=100$, the maximum output current is 22 mA . The driver stage may thus limit the maximum positive current available from the output stage. However, this output current level is only reached if $R_{L}$ is small enough so that $Q_{13 \mathrm{~A}}$ does not saturate on the positive voltage excursion.

The stage preceding the driver in this circuit is $Q_{17}$. As mentioned above, the negative voltage limit of $V_{o}$ is reached when $Q_{17}$ saturates. The bias current of 0.68 mA in $Q_{17}$ is much greater than the base current of $Q_{23}$, and thus $Q_{23}$ produces very little loading on $Q_{17}$. Consequently, voltage $V_{1}$ at the base of $Q_{23}$ can be driven to within $V_{C E(\text { sat })}$ of either supply voltage with only a very small fractional change in the collector current of $Q_{17}$.

Finally, we will now examine the detail of the fabrication of diodes $Q_{18}$ and $Q_{19}$ in the 741. The actual circuit is shown in Fig. $5.20 b$ with the output protection circuitry omitted. Diode $Q_{19}$ conducts only a current equal to the base current of $Q_{18}$ plus the bleed current in pinch resistor $R_{10}$. Transistor $Q_{18}$ thus conducts most of the bias current of current source $Q_{13 \mathrm{~A}}$. This arrangement is used for two reasons. First, the basic aim of achieving a voltage drop equal to two base-emitter voltages is achieved. Since $Q_{18}$ and $Q_{19}$ have common collectors, however, they can be placed in the same isolation region, reducing die area. Second, since $Q_{19}$ conducts only a small current, the bias voltage produced by $Q_{18}$ and $Q_{19}$ across the bases of $Q_{14}$ and $Q_{20}$ is less than would result from a connection as shown in Fig. 5.20a. This observation is important because output transistors $Q_{14}$ and $Q_{20}$ generally have emitter areas larger than the standard device geometry (typically four times larger or more) so that they can maintain high $\beta_{F}$ while conducting large output currents. Thus in the circuit of Fig. 5.20a, the bias current in $Q_{14}$ and $Q_{20}$ would be about four times the current in $Q_{18}$ and $Q_{19}$, which would be excessive in a 741-type circuit. However, the circuit of Fig. 5.20b can be designed to bias $Q_{14}$ and $Q_{20}$ to a current comparable to the current in the diodes, even though the output devices have a large area. The basic reason for this result is that the small bias current in $Q_{19}$ in Fig. 5.20 b gives it a smaller base-emitter voltage than for the same device in Fig. 5.20a, reducing the total bias voltage between the bases of $Q_{14}$ and $Q_{20}$.

The results described above can be illustrated quantitatively by calculating the bias currents in $Q_{14}$ and $Q_{20}$ of Fig. 5.20b. From KVL,

$$
V_{B E 19}+V_{B E 18}=V_{B E 14}+\left|V_{B E 20}\right|
$$

and thus

$$
\begin{equation*}
V_{T} \ln \frac{I_{C 19}}{I_{S 19}}+V_{T} \ln \frac{I_{C 18}}{I_{S 18}}=V_{T} \ln \frac{I_{C 14}}{I_{S 14}}+V_{T} \ln \left|\frac{I_{C 20}}{I_{S 20}}\right| \tag{5.82}
\end{equation*}
$$

If we assume that the circuit is biased for $V_{o}=0 \mathrm{~V}$ and also that $\beta_{F 14} \gg 1$ and $\beta_{F 20} \gg 1$, then $\left|I_{C 14}\right|=\left|I_{C 20}\right|$ and (5.82) becomes

$$
\frac{I_{C 19} I_{C 18}}{I_{S 18} I_{S 19}}=\frac{I_{C 14}^{2}}{I_{S 14} I_{S 20}}
$$

from which

$$
\begin{equation*}
I_{C 14}=-I_{C 20}=\sqrt{I_{C 19} I_{C 18}} \sqrt{\frac{I_{S 14} I_{S 20}}{I_{S 18} I_{S 19}}} \tag{5.83}
\end{equation*}
$$

Equation 5.83 may be used to calculate the output bias current in circuits of the type shown in Fig. 5.20b. The output-stage bias current from (5.83) is proportional to $\sqrt{I_{C 18}}$ and $\sqrt{I_{C 19}}$. For this specific example, the collector current in $Q_{19}$ is approximately equal to the current in $R_{10}$ if $\beta_{F}$ is large and thus

$$
I_{C 19} \simeq \frac{V_{B E 18}}{R_{10}} \simeq \frac{0.6}{40} \mathrm{~mA}=15 \mu \mathrm{~A}
$$

If the base currents of $Q_{14}$ and $Q_{20}$ are neglected, the collector current of $Q_{18}$ is

$$
I_{C 18} \simeq\left|I_{C 13 \mathrm{~A}}\right|-I_{C 19}=(220-15) \mu \mathrm{A}=205 \mu \mathrm{~A}
$$

To calculate the output-stage bias currents from (5.83), values for the various reverse saturation currents are required. These values depend on the particular IC process used, but typical values are $I_{S 18}=I_{S 19}=2 \times 10^{-15} \mathrm{~A}, I_{S 14}=4 I_{S 18}=8 \times 10^{-15} \mathrm{~A}$, and $I_{S 20}=4 \times 10^{-15} \mathrm{~A}$. Substitution of these data in (5.83) gives $I_{C 14}=-I_{C 20}=0.16 \mathrm{~mA}$.

#### EXAMPLE

For the output stage of Fig. 5.20a, calculate bias currents in all devices for $V_{o}=+10 \mathrm{~V}$. Assume that $V_{C C}=15 \mathrm{~V}, R_{L}=2 \mathrm{k} \Omega$, and $\beta_{F}=100$. For simplicity, assume all devices have equal area and for each device

$$
\begin{equation*}
\left|I_{C}\right|=10^{-14} \exp \left|\frac{V_{b e}}{V_{T}}\right| \tag{5.84}
\end{equation*}
$$

Assuming that $Q_{14}$ supplies the load current for positive output voltages, we have

$$
I_{c 14}=\frac{V_{o}}{R_{L}}=\frac{10 \mathrm{~V}}{2 \mathrm{k} \Omega}=5 \mathrm{~mA}
$$

Substitution in (5.84) and rearranging gives

$$
V_{b e 14}=(26 \mathrm{mV}) \ln \left(\frac{5 \times 10^{-3}}{10^{-14}}\right)=700 \mathrm{mV}
$$

Also

$$
I_{b 14}=\frac{I_{c 14}}{\beta_{F 14}}=\frac{5 \mathrm{~mA}}{100}=0.05 \mathrm{~mA}
$$

Thus

$$
I_{c 19} \simeq I_{c 18} \simeq-I_{c 23}=(0.22-0.05) \mathrm{mA}=0.17 \mathrm{~mA}
$$

Substitution in (5.84) and rearranging gives

$$
V_{b e 19}=V_{b e 18}=-V_{b e 23}=(26 \mathrm{mV}) \ln \left(\frac{0.17 \times 10^{-3}}{10^{-14}}\right)=613 \mathrm{mV}
$$

Thus

$$
V_{b e 20}=-\left(V_{b e 19}+V_{b e 18}-V_{b e 14}\right)=-525 \mathrm{mV}
$$

Use of (5.84) gives

$$
I_{c 20}=-5.9 \mu \mathrm{~A}
$$

and the collector current in $Q_{20}$ is quite small as predicted. Finally

$$
I_{c 17}=0.68 \mathrm{~mA}-\frac{I_{c 23}}{\beta_{F 23}}=\left(0.68-\frac{0.17}{100}\right) \mathrm{mA}=0.68 \mathrm{~mA}
$$

and also

$$
V_{2}=V_{o}-\left|V_{b e 20}\right|=(10-0.525) \mathrm{V}=9.475 \mathrm{~V}
$$

and

$$
V_{1}=V_{2}-\left|V_{b e 23}\right|=(9.475-0.613) \mathrm{V}=8.862 \mathrm{~V}
$$

### 5.4.4 All-npn Class B Output Stage ${ }^{7,8,9}$

The Class B circuits described above are adequate for many integrated-circuit applications where the output power to be delivered to the load is of the order of several hundred milliwatts or less. However, if output-power levels of several watts or more are required, these circuits are inadequate because the substrate $p n p$ transistors used in the output stage have a limited current-carrying capability. This limit stems from the fact that the doping levels in the emitter, base, and collector of these devices are not optimized for pnp structures because the $n p n$ devices in the circuit have conflicting requirements.

A circuit design that uses high-power npn transistors in both halves of a Class B configuration is shown in Fig. 5.22. In this circuit, common-emitter transistor $Q_{1}$ delivers power to the load during the negative half-cycle, and emitter follower $Q_{2}$ delivers power during the positive half-cycle.

To examine the operation of this circuit, consider $V_{i}$ taken negative from its quiescent value so that $Q_{1}$ is off and $I_{c 1}=0$. Then diodes $D_{1}$ and $D_{2}$ must both be off and all of the collector current of $Q_{3}$ is delivered to the base of $Q_{2}$. The output voltage then has its maximum positive value $V_{o}^{+}$. If $R_{L}$ is big enough, $Q_{3}$ saturates and

$$
\begin{equation*}
V_{o}^{+}=V_{C C}-\left|V_{C E 3(\mathrm{sat})}\right|-V_{b e 2} \tag{5.85}
\end{equation*}
$$

To attain this maximum positive value, transistor $Q_{3}$ must saturate in this extreme condition. In contrast, $Q_{2}$ in this circuit cannot saturate because the collector of $Q_{2}$ is connected to the positive supply and the base voltage of $Q_{2}$ cannot exceed the positive supply voltage. The condition for $Q_{3}$ to be saturated is that the nominal collector bias current $I_{Q 3}$ in $Q_{3}$ (when $Q_{3}$ is not saturated) should be larger than the required base current of $Q_{2}$ when $V_{o}=V_{o}^{+}$. Thus we require

$$
\begin{equation*}
I_{Q 3}>I_{b 2} \tag{5.86}
\end{equation*}
$$

Since $Q_{2}$ supplies the current to $R_{L}$ for $V_{o}>0$, we have

$$
\begin{equation*}
V_{o}^{+}=-I_{e 2} R_{L}=\left(\beta_{2}+1\right) I_{b 2} R_{L} \tag{5.87}
\end{equation*}
$$

image_name:Figure 5.22 All-npn Class B output stage
description:
[
name: Q1, type: NPN, ports: {C: V1, B: Vin, E: -VCC}
name: Q2, type: NPN, ports: {C: VCC, B: V2, E: V0}
name: Q3, type: PNP, ports: {C: V2, B: v3, E: VCC}
name: D1, type: Diode, ports: {Na: V2, Nc: V1}
name: D2, type: Diode, ports: {Na: Vo, Nc: V1}
name: RL, type: Resistor, value: RL, ports: {N1: V0, N2: GND}
name: b3, type: Resistor, value: b3, ports: {N1: b3, N2: GND}
]
extrainfo:The circuit is an all-NPN Class B output stage with a PNP transistor Q3 providing biasing. The diodes D1 and D2 are used for thermal stability and biasing. The output voltage Vo is taken across the load resistor RL. The circuit operates with positive and negative supply voltages VCC and -VCC.

Figure 5.22 All-npn Class B output stage.

Substitution of (5.87) and (5.85) in (5.86) gives the requirement on the bias current of $Q_{3}$ as

$$
\begin{equation*}
I_{Q 3}>\frac{V_{C C}-V_{C E 3(\mathrm{sat})}-V_{b e 2}}{\left(\beta_{2}+1\right) R_{L}} \tag{5.88}
\end{equation*}
$$

Equation 5.88 also applies to the circuit of Fig. 5.20a. It gives limits on $I_{C 3}, \beta_{2}$, and $R_{L}$ for $V_{o}$ to be able to swing close to the positive supply. If $I_{Q 3}$ is less than the value given by (5.88), $V_{o}$ will begin clipping at a positive value less than that given by (5.85) and $Q_{3}$ will never saturate.

Now consider $V_{i}$ made positive to turn $Q_{1}$ on and produce nonzero $I_{c 1}$. Since the base of $Q_{2}$ is more positive than its emitter, diode $D_{1}$ will turn on in preference to $D_{2}$, which will be off with zero volts across its junction. The current $I_{c 1}$ will flow through $D_{1}$ and will be drawn from $Q_{3}$, which is assumed saturated at first. As $I_{c 1}$ increases, $Q_{3}$ will eventually come out of saturation, and voltage $V_{2}$ at the base of $Q_{2}$ will then be pulled down. Since $Q_{2}$ acts as an emitter follower, $V_{o}$ will follow $V_{2}$ down. This behavior occurs during the positive half of the cycle, and $Q_{1}$ acts as a driver with $Q_{2}$ as the output device.

When $V_{o}$ is reduced to 0 V , the load current is zero and $I_{c 2}=0$. This point corresponds to $I_{c 1}=\left|I_{C 3}\right|$, and all of the bias current in $Q_{3}$ passes through $D_{1}$ to $Q_{1}$. If $I_{c 1}$ is increased further, $V_{o}$ stays constant at 0 V while $V_{2}$ is reduced to 0 V also. Therefore, $V_{1}$ is negative by an amount equal to the diode voltage drop of $D_{1}$, and thus power diode $D_{2}$ turns on. Since the current in $D_{1}$ is essentially fixed by $Q_{3}$, further increases in $I_{c 1}$ cause increasing current to flow through $D_{2}$. The negative half of the cycle consists of $Q_{1}$ acting as the output device and feeding $R_{L}$ through $D_{2}$. The maximum negative voltage occurs when $Q_{1}$ saturates and is

$$
\begin{equation*}
V_{o}^{-}=-V_{C C}+V_{C E 1(\mathrm{sat})}+V_{d 2} \tag{5.89}
\end{equation*}
$$

where $V_{d 2}$ is the forward voltage drop across $D_{2}$.
The sequence just described gives rise to a highly nonlinear transfer characteristic, as shown in Fig. 5.23, where $V_{o}$ is plotted as a function of $I_{c 1}$ for convenience. When $V_{o}$ is positive, the current $I_{c 1}$ feeds into the base of $Q_{2}$ and the small-signal gain is

$$
\frac{\Delta V_{o}}{\Delta I_{c 1}} \simeq \frac{\Delta V_{2}}{\Delta I_{c 1}}=r_{o 1}\left\|r_{o 3}\right\|\left[r_{\pi 2}+\left(\beta_{2}+1\right) R_{L}\right]
$$

image_name:Figure 5.23
description:The graph in Figure 5.23 is a transfer characteristic plot, illustrating the relationship between the output voltage \( V_o \) and the input current \( I_{c1} \). The graph is presented on a Cartesian coordinate system with \( V_o \) on the vertical axis and \( I_{c1} \) on the horizontal axis. Both axes are likely on a linear scale, though specific units are not provided.

Overall Behavior and Trends:
- **Positive Region:**
- When \( V_o \) is positive, the graph shows a steep slope indicating a high gain. This region is defined by the formula:
\[ \text{Slope} = r_{o1} \parallel r_{o3} \parallel \left[ r_{\pi2} + (\beta_2 + 1) R_L \right] \]
- The output voltage \( V_o^+ \) is given by:
\[ V_o^+ = [V_{CC} - V_{be2} - |V_{CE3(sat)}|] \]
- This region ends where transistor \( Q_3 \) becomes saturated.

- **Negative Region:**
- When \( V_o \) is negative, the slope is less steep, indicating a lower gain. The slope in this region is:
\[ \text{Slope} = R_L \parallel r_{o1} \]
- The output voltage \( V_o^- \) is given by:
\[ V_o^- = [-V_{CC} + V_{d2} + V_{CE1(sat)}] \]
- This region ends where transistor \( Q_1 \) becomes saturated.

Key Features and Technical Details:
- The graph has distinct linear regions for positive and negative values of \( V_o \), with different slopes indicating different circuit configurations and gains.
- The transition points are marked where the transistors \( Q_1 \) and \( Q_3 \) become saturated, which are critical points for the operation of the circuit.
- \( I_{c3} \) and \( I_{c2}/\beta_2 \) are marked on the \( I_{c1} \) axis, indicating specific current values relevant to the circuit's operation.

Annotations and Specific Data Points:
- The graph includes annotations for the slopes in both the positive and negative regions, which are important for understanding the gain characteristics of the circuit.
- The saturation points for \( Q_1 \) and \( Q_3 \) are annotated, providing insights into the limiting behavior of the circuit under different conditions.

Figure 5.23 Transfer characteristic of the circuit of Fig. 5.22 from $I_{c 1}$ to $V_{o}$.
where the impedance of $D_{1}$ is assumed negligible. That is, the impedance at the base of $Q_{2}$ is equal to the parallel combination of the output resistances of $Q_{1}$ and $Q_{3}$ and the input resistance of emitter follower $Q_{2}$.

When $V_{o}$ in Fig. 5.22 is negative, $I_{c 1}$ feeds $R_{L}$ directly and the small-signal gain is

$$
\frac{\Delta V_{o}}{\Delta I_{c 1}} \simeq r_{o 1} \| R_{L}
$$

where the impedance of $D_{2}$ is assumed negligible.
Note the small deadband in Fig. 5.23 where diode $D_{2}$ turns on. This deadband can be eliminated by adding a second diode in series with $D_{1}$. In practice, negative feedback must be used around this circuit to linearize the transfer characteristic, and such feedback will reduce any crossover effects. The transfer characteristic of the circuit from $V_{i}$ to $V_{o}$ is even more nonlinear than shown in Fig. 5.23 because it includes the exponential nonlinearity of $Q_{1}$.

In integrated-circuit fabrication of the circuit of Fig. 5.22, devices $Q_{1}$ and $Q_{2}$ are identical large-power transistors. In high-power circuits (delivering several watts or more), they may occupy 50 percent of the whole die. Diode $D_{2}$ is a large-power diode that also occupies considerable area. These features are illustrated in Fig. 5.24, which is a die photo of the 791 high-power op amp. This circuit can dissipate 10 W of power and can deliver 15 W of output power into an $8-\Omega$ load. The large power transistors in the output stage can be seen on the right-hand side of the die.

Finally, the power and efficiency results derived previously for the complementary Class B stage apply equally to the all- $\boldsymbol{n p n}$ Class B stage if allowance is made for the voltage drop in $D_{2}$. Thus the ideal maximum efficiency is 79 percent.
image_name:Figure 5.24 Die photo of the 791 high-power op amp
description:The image shows the die of a 791 high-power operational amplifier (op amp). This die is a detailed view of the internal structure of the op amp, showcasing various components and connections. On the right-hand side of the die, large power transistors are visible, which are crucial for the output stage of the op amp. These transistors are responsible for handling high power levels, allowing the circuit to dissipate 10 watts of power and deliver 15 watts into an 8-ohm load.

The layout includes a complex network of interconnections, likely representing the metal traces that connect different components on the chip. These traces enable the flow of signals and power throughout the op amp, ensuring proper operation. The die is divided into distinct regions, each housing different functional parts of the amplifier circuit.

There are no specific labels or annotations visible on the die itself, but the layout and structure suggest a highly integrated design typical of power amplifiers. The efficiency of this op amp, as mentioned, can reach up to 79% under ideal conditions, which aligns with the characteristics of a complementary Class B stage or an all-npn Class B stage, considering the voltage drop in diode D2.

Figure 5.24 Die photo of the 791 high-power op amp.

### 5.4.5 Quasi-Complementary Output Stages ${ }^{10}$

The all-npn stage described above is one solution to the problem of the limited power-handling capability of the substrate pnp. Another solution is shown in Fig. 5.25, where a composite pnp has been made from a lateral pnp $Q_{3}$ and a high-power $n p n$ transistor $Q_{4}$. This circuit is called a quasi-complementary output stage.

The operation of the circuit of Fig. 5.25 is almost identical to that of Fig. 5.20. The pair $Q_{3}-Q_{4}$ is equivalent to a $p n p$ transistor as shown in Fig. 5.26, and the collector current of $Q_{3}$ is

$$
\begin{equation*}
I_{C 3}=-I_{S} \exp \left(-\frac{V_{B E}}{V_{T}}\right) \tag{5.90}
\end{equation*}
$$

The composite collector current $I_{C}$ is the emitter current of $Q_{4}$, which is

$$
\begin{equation*}
I_{C}=\left(\beta_{F 4}+1\right) I_{C 3}=-\left(\beta_{F 4}+1\right) I_{S} \exp \left(-\frac{V_{B E}}{V_{T}}\right) \tag{5.91}
\end{equation*}
$$

The composite device thus shows the standard relationship between $I_{C}$ and $V_{B E}$ for a pnp transistor. However, most of the current is carried by the high-power npn transistor. Note that the magnitude of the saturation voltage of the composite device is $\left(\left|V_{C E 3 \text { (sat) }}\right|+V_{B E 4}\right)$. This
image_name:Figure 5.25 Quasi-complementary Class B output stage.
description:
[
name: Q8, type: Diode, ports: {Na: VCC, Nc: b7a8}
name: Q7, type: PNP, ports: {C: b2c7, B: b7a8, E: VCC}
name: Q2, type: NPN, ports: {C: VCC, B: b2c7, E: Vo}
name: Q6, type: Diode, ports: {Na: b2c7, Nc: a5}
name: Q5, type: Diode, ports: {Na: a5, Nc: c1b3}
name: Q3, type: PNP, ports: {C: c3b4, B: c1b3, E: Vo}
name: Q1, type: NPN, ports: {C: c1b3, B: Vi, E: -VCC}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a quasi-complementary Class B output stage, which uses a combination of NPN and PNP transistors to amplify the input signal. This configuration is designed to improve efficiency and reduce distortion in the output stage.

Figure 5.25
Quasi-complementary Class B output stage.
image_name:Figure 5.26 Equivalence of the composite connection and a pnp transistor
description:
[
name: Q3, type: PNP, ports: {C: c3b4, B: B, E: E}
name: Q4, type: NPN, ports: {C: E, B: c3b4, E: C}
]
extrainfo:The circuit diagram shows the equivalence of a composite connection using a PNP (Q3) and NPN (Q4) transistor to form a configuration similar to a single PNP transistor. This arrangement is used to achieve a specific current amplification behavior, with the composite configuration providing an equivalent current flow as a single PNP transistor.
Figure 5.26 Equivalence of the composite connection and a p $n p$ transistor.
image_name:Figure 5.26
description:
[
name: Q, type: PNP, ports: {C: C, B: B, E: E}
]
extrainfo:The circuit diagram shows the equivalence of a composite connection using a PMOS (M3) and NPN (Q4) transistor to form a configuration similar to a single PMOS transistor. The composite configuration provides an equivalent current flow, denoted as ID, from the source S to the drain D.

image_name:Figure 5.27
description:
[
name: M3, type: PMOS, ports: {S: S, D: d3g4, G: G}
name: Q4, type: NPN, ports: {C: S, B: d3g4, E: D}
]
extrainfo:The compound high-current PMOS connection shows a PMOS transistor (M3) and an NPN transistor (Q4) in a configuration that mimics a single PMOS transistor. This setup enhances current handling capability, with the current ID flowing from the source S to the drain D. The voltage VGS is applied between the gate G and source S.

Figure 5.27 Compound high-current PMOS connection.
magnitude is higher than normal because saturation occurs when $Q_{3}$ saturates, and $V_{B E 4}$ must be added to this voltage.

The major problem with the configuration of Fig. 5.25 is potential instability of the local feedback loop formed by $Q_{3}$ and $Q_{4}$, particularly with capacitive loads on the amplifier. The stability of feedback loops is considered in Chapter 9 .

The quasi-complementary Class B stage can also be effectively implemented in BiCMOS technology. In the circuit of Fig. 5.25, the compound bipolar device $Q_{3}-Q_{4}$ can be replaced by the MOS-bipolar combination ${ }^{11}$ of Fig. 5.27, where $Q_{4}$ is a large-area high-current bipolar device. The overall transfer characteristic is

$$
\begin{equation*}
I_{D}=\left(\beta_{F 4}+1\right) I_{D 3}=-\left(\beta_{F 4}+1\right) \frac{\mu_{n} C_{o x}}{2}\left(\frac{W}{L}\right)_{3}\left(V_{G S}-V_{t}\right)^{2} \tag{5.92}
\end{equation*}
$$

Equation 5.92 shows that the composite PMOS device appears to have a $W / L$ ratio $\left(\beta_{F 4}+1\right)$ times larger than the physical PMOS device $M_{3}$. With this circuit, one of the diodes $Q_{5}$ or $Q_{6}$ in Fig. 5.25 would now be replaced by a diode-connected PMOS transistor to set up a temperature-stable standby current in the output stage. A bias bleed resistor can be connected from the base to the emitter of $Q_{4}$ to optimize the bias current in $M_{3}$ and to speed up the turnoff of $Q_{4}$ in high-frequency applications by allowing reverse base current to remove the base charge. Such a resistor can also be connected from the base to the emitter of $Q_{4}$ in Fig. 5.25.

### 5.4.6 Overload Protection

The most common type of overload protection in integrated-circuit output stages is short-circuit current protection. As an example, consider the 741 output stage shown in Fig. 5.28 with partial short-circuit protection included. Initially assume that $R_{6}=0$ and ignore $Q_{15}$. The maximum positive drive delivered to the output stage occurs for $V_{i}$ large positive. If $R_{L}=0$ then $V_{o}$ is held at zero volts and $V_{a}$ in Fig. 5.28 is equal to $V_{b e 14}$. Thus, as $V_{i}$ is taken positive, $Q_{23}, Q_{18}$, and $Q_{19}$ will cut off and all of the current of $Q_{13 \mathrm{~A}}$ is fed to $Q_{14}$. If this is a high- $\beta_{F}$ device, then the output current can become destructively large:

$$
\begin{equation*}
I_{c 14}=\beta_{F 14}\left|I_{C 13 \mathrm{~A}}\right| \tag{5.93}
\end{equation*}
$$

If

$$
\beta_{F 14}=500
$$

then

$$
I_{c 14}=500 \times 0.22=110 \mathrm{~mA}
$$

image_name:Figure 5.28
description:The circuit is a part of the 741 operational amplifier with partial short-circuit protection. It uses Q15 and R6 to limit the current under short-circuit conditions. The current through Q14 can become destructively large if not controlled.

Figure 5.28 Schematic of the 741 op amp showing partial short-circuit protection.

If $V_{C C}=15 \mathrm{~V}$, this current level gives a power dissipation in $Q_{14}$ of

$$
P_{c 14}=V_{c e} I_{c}=15 \times 110 \mathrm{~mW}=1.65 \mathrm{~W}
$$

which is sufficient to destroy the device. Thus the current under short-circuit conditions must be limited, and this objective is achieved using $R_{6}$ and $Q_{15}$ for positive $V_{o}$.

The short-circuit protection operates by sensing the output current with resistor $R_{6}$ of about $25 \Omega$. The voltage developed across $R_{6}$ is the base-emitter voltage of $Q_{15}$, which is normally off. When the current through $R_{6}$ reaches about 20 mA (the maximum safe level), $Q_{15}$ begins to conduct appreciably and diverts any further drive away from the base of $Q_{14}$. The drive current is thus harmlessly passed to the output instead of being multiplied by the $\beta_{F}$ of $Q_{14}$.

The operation of this circuit can be seen by calculating the transfer characteristic of $Q_{14}$ when driving a short-circuit load. This can be done using Fig. 5.29.

$$
\begin{align*}
I_{i} & =I_{b 14}+I_{c 15}  \tag{5.94}\\
I_{c 15} & =I_{S 15} \exp \frac{V_{b e 15}}{V_{T}} \tag{5.95}
\end{align*}
$$

Also

$$
\begin{equation*}
V_{b e 15} \simeq I_{c 14} R \tag{5.96}
\end{equation*}
$$

From (5.94)

$$
I_{b 14}=I_{i}-I_{c 15}
$$

But

$$
\begin{equation*}
I_{c 14}=\beta_{F 14} I_{b 14}=\beta_{F 14}\left(I_{i}-I_{c 15}\right) \tag{5.97}
\end{equation*}
$$

image_name:Figure 5.29
description:
[
name: Q14, type: NPN, ports: {C: VCC, B: Vin, E: e14b15}
name: Q15, type: NPN, ports: {C: Vin, B: e14b15, E: GND}
name: R, type: Resistor, value: R, ports: {N1: e14b15, N2: GND}
name: Ii, type: CurrentSource, ports: {Np: GND, Nn: Vi}
]
extrainfo:This circuit shows the interaction between transistors Q14 and Q15, where Q15 affects the transfer characteristic of Q14. The current source Ii provides input current, and resistor R is connected between the emitter of Q14 and ground. The circuit operates with a supply voltage VCC.

Figure 5.29 Equivalent circuit for the calculation of the effect of $Q_{15}$ on the transfer characteristic of $Q_{14}$ in Fig. 5.28 when $R_{L}=0$ 。
image_name:Figure 5.30
description:The graph in Figure 5.30 is a transfer characteristic plot depicting the relationship between the collector current \( I_{c14} \) and the input current \( I_i \) for the circuit shown in Figure 5.29. The graph is plotted with two different scenarios: with and without the protection transistor \( Q_{15} \).

1. **Type of Graph:**
- This is a transfer characteristic graph showing the current relationship in a transistor circuit.

2. **Axes Labels and Units:**
- The x-axis represents the input current \( I_i \) in milliamperes (mA), with a range from 0 to 0.25 mA.
- The y-axis represents the collector current \( I_{c14} \) in milliamperes (mA), ranging from 0 to 40 mA.
- Both axes use a linear scale.

3. **Overall Behavior and Trends:**
- The graph shows a linear increase in \( I_{c14} \) with \( I_i \) in the absence of protection, following the equation \( I_{c14} = \beta_{F14} I_i \), represented by a dashed line.
- With protection, the \( I_{c14} \) curve initially follows a similar path but quickly saturates, leveling off around 20 mA as \( I_i \) increases.

4. **Key Features and Technical Details:**
- The dashed line indicates the expected linear relationship without the protection transistor, suggesting a direct proportionality between \( I_{c14} \) and \( I_i \).
- The solid curve shows the effect of the protection transistor \( Q_{15} \), which limits \( I_{c14} \) to around 20 mA, demonstrating a saturation behavior.

5. **Annotations and Specific Data Points:**
- Annotations on the graph highlight the two scenarios: "No protection" and "With protection."
- The intersection point where the curve diverges from the linear path indicates the onset of saturation due to the protection mechanism.

Figure 5.30 Transfer characteristic of the circuit of Fig. 5.29 with and without protection transistor $Q_{15}\left(\beta_{F 14}=500\right)$.

Substitution of (5.95) and (5.96) in (5.97) gives

$$
\begin{equation*}
I_{c 14}+\beta_{F 14} I_{S 15} \exp \frac{I_{c 14} R}{V_{T}}=\beta_{F 14} I_{i} \tag{5.98}
\end{equation*}
$$

The second term on the left side of (5.98) stems from $Q_{15}$. If this term is negligible, then $I_{c 14}=\beta_{F 14} I_{i}$ as expected. The transfer characteristic of the stage is plotted from (5.98) in Fig. 5.30, using $\beta_{F 14}=500, I_{S 15}=10^{-14} \mathrm{~A}$, and $R=25 \Omega$. For a maximum drive of $I_{i}=0.22 \mathrm{~mA}$, the value of $I_{c 14}$ is effectively limited to 24 mA . For values of $I_{c 14}$ below $20 \mathrm{~mA}, Q_{15}$ has little effect on circuit operation.

Similar protection for negative output voltages in Fig. 5.29 is achieved by sensing the voltage across $R_{7}$ and diverting the base drive away from one of the preceding stages.

## 5.5 CMOS Class AB Output Stages

The classical Class AB topology of Fig. 5.13 can also be implemented in standard CMOS technology. However, the output swing of the resulting circuit is usually much worse than in the bipolar case. Although the swing can be improved using a common-source configuration, this circuit suffers from poor control of the quiescent current in the output devices. These issues are described below.

### 5.5.1 Common-Drain Configuration

Figure 5.31 shows the common-drain Class AB output configuration. From KVL,

$$
\begin{equation*}
V_{S G 5}+V_{G S 4}=V_{g s 1}+V_{s g 2} \tag{5.99}
\end{equation*}
$$

Ignoring the body effect, $V_{S G 5}+V_{G S 4}$ is constant if the bias current from $M_{3}$ is constant. Under these conditions, increasing $V_{g s 1}$ decreases $V_{s g 2}$ and vice versa.

For simplicity, assume at first that a short circuit is connected from the drain of $M_{4}$ to the drain of $M_{5}$. Then $V_{S G 5}+V_{G S 4}=0$ and $V_{g s 1}=V_{g s 2}$ from (5.99). For $M_{1}$ to conduct nonzero drain current, $V_{g s 1}>V_{t 1}$ is required. Similarly, $V_{g s 2}<V_{t 2}$ is required for $M_{2}$ to conduct nonzero drain current. With standard enhancement-mode devices, $V_{t 1}>0$ and $V_{t 2}<0$. Therefore, $M_{1}$ and $M_{2}$ do not both conduct simultaneously under these conditions, which is a characteristic of a Class B output stage. When $V_{o}>0, M_{1}$ operates as a source follower and $M_{2}$ is off. Similarly, $M_{2}$ operates as a source follower and $M_{1}$ is off when $V_{o}<0$.

In Fig. 5.31, however, $V_{S G 5}+V_{G S 4}>0$ and both $M_{1}$ and $M_{2}$ are biased to conduct nonzero drain current when $V_{o}=0$, which is a characteristic of a Class AB output stage. If $V_{t 1}=V_{t 4}$ and $V_{t 2}=V_{t 5}$, using (1.157) in (5.99) with $I_{D 5}=-I_{D 4}$ gives

$$
\begin{equation*}
\sqrt{\frac{2 I_{D 4}}{k_{p}^{\prime}(W / L)_{5}}}+\sqrt{\frac{2 I_{D 4}}{k_{n}^{\prime}(W / L)_{4}}}=\sqrt{\frac{2 I_{d 1}}{k_{n}^{\prime}(W / L)_{1}}}+\sqrt{\frac{2\left|I_{d 2}\right|}{k_{p}^{\prime}(W / L)_{2}}} \tag{5.100}
\end{equation*}
$$

If $V_{o}=0$, then $I_{d 2}=-I_{d 1}$ and (5.100) can be rearranged to give

$$
\begin{equation*}
I_{D 1}=I_{D 4} \frac{\left(\sqrt{\frac{1}{k_{n}^{\prime}(W / L)_{4}}}+\sqrt{\frac{1}{k_{p}^{\prime}(W / L)_{5}}}\right)^{2}}{\left(\sqrt{\frac{1}{k_{n}^{\prime}(W / L)_{1}}}+\sqrt{\frac{1}{k_{p}^{\prime}(W / L)_{2}}}\right)^{2}} \tag{5.101}
\end{equation*}
$$

where $I_{D 1}=I_{d 1}$ with $V_{o}=0$. The key point of this equation is that the quiescent current in the output transistors is well controlled with respect to the bias current that flows in the diode-connected transistors, as in the bipolar case.
image_name:Figure 5.31
description:
[
name: M1, type: NMOS, ports: {S: Vo, D: VDD, G: g1d3g4}
name: M2, type: NMOS, ports: {S: Vo, D: -Vss, G: g2g5d6}
name: M3, type: PMOS, ports: {S: VDD, D: g1d3g4, G: VBIAS}
name: M4, type: NMOS, ports: {S: s4s5, D: g1d3g4, G: g1d3g4}
name: M5, type: PMOS, ports: {S: s4s5, D: g2g5d6, G: g2g5d6}
name: M6, type: NMOS, ports: {S: -VSS, D: g2g5d6, G: Vi}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:This circuit is a complementary source follower CMOS output stage. The output swing is limited due to the use of CMOS instead of bipolar transistors. M1 and M2 form the output stage, with M1 acting as a source follower when Vo > 0.

Figure 5.31 Complementary sourcefollower CMOS output stage based on traditional bipolar implementation.

An important problem with this circuit is that its output swing can be much less than the corresponding bipolar circuit with equal supply voltages. For $V_{o}>0, V_{g s 1}>V_{t 1}$ and $M_{1}$ acts as a source follower. Therefore,

$$
\begin{equation*}
V_{o}=V_{D D}-V_{s d 3}-V_{g s 1} \tag{5.102}
\end{equation*}
$$

The minimum $V_{s d 3}$ required to operate $M_{3}$ as a current source is $\left|V_{o v 3}\right|=\left|V_{G S 3}-V_{t 3}\right|$. From (5.102), the maximum output voltage $V_{o}^{+}$is

$$
\begin{equation*}
V_{o}^{+}=V_{D D}-\left|V_{o v 3}\right|-V_{g s 1} \tag{5.103}
\end{equation*}
$$

The minimum output voltage can be found by similar reasoning. (See Problem 5.21.) Although (5.103) appears to be quite similar to (5.81) if $V_{C C}$ in Fig. 5.20 is equal to $V_{D D}$ in Fig. 5.31, the limit in (5.103) is usually much less than in (5.81) for three reasons. First, the gate-source voltage includes a threshold component that is absent in the base-emitter voltage. Second, the body effect increases the threshold voltage $V_{t 1}$ as $V_{o}$ increases. Finally, the overdrive part of the gate-source voltage rises more steeply with increasing current than the entire base-emitter voltage because the overdrive is proportional to the square root of the current and the baseemitter voltage is proportional to the logarithm of the current. In practice, the output voltage swing can be increased by increasing the $W / L$ ratios of the output devices to reduce their overdrives. However, the required transistor sizes are sometimes so large that the parasitic capacitances associated with the output devices can dominate the overall performance at high frequencies. Thus the circuit of Fig. 5.31 is generally limited to much smaller currents than its bipolar equivalent.

#### EXAMPLE

An output stage such as shown in Fig. 5.31 is required to produce a maximum output voltage of 0.7 V with $R_{L}=35 \Omega$ and $V_{D D}=V_{S S}=1.5 \mathrm{~V}$. Using the transistor parameters in Table 2.4, find the required $W / L$ of $M_{1}$. Assume $\left|V_{o v 3}\right|=100 \mathrm{mV}$, and ignore the body effect.

From (5.103),

$$
V_{g s 1}=V_{D D}-\left|V_{o v 3}\right|-V_{o}^{+}=(1.5-0.1-0.7) \mathrm{V}=0.7 \mathrm{~V}
$$

Since Table 2.4 gives $V_{t 1}=0.6 \mathrm{~V}$,

$$
V_{o v 1}=V_{g s 1}-V_{t 1}=(0.7-0.6) \mathrm{V}=0.1 \mathrm{~V}
$$

With $V_{o}=0.7 \mathrm{~V}$, the current in the load is $(0.7 \mathrm{~V}) /(35 \Omega)=20 \mathrm{~mA}$. If $I_{d 2}=0$ under these conditions, $I_{d 1}=20 \mathrm{~mA}$. Rearranging (1.157) gives

$$
\begin{equation*}
\left(\frac{W}{L}\right)_{1}=\frac{2 I}{k_{n}^{\prime} V_{o v 1}{ }^{2}}=\frac{2(20000)}{194(0.1)^{2}} \simeq 20,000 \tag{5.104}
\end{equation*}
$$

which is a very large transistor.

### 5.5.2 Common-Source Configuration with Error Amplifiers

Another alternative is the use of quasi-complementary configurations. In this case, a common-source transistor together with an error amplifier replaces an output source-follower device. A circuit with this substitution for both output transistors is shown conceptually in Fig. 5.32. ${ }^{12,13,14}$ The combination of the error amplifier and the common-source device mimics the behavior of a source follower with high dc transconductance. The function of the amplifiers is to sense the voltage difference between the input and the output of the stage and drive the gates of the output transistors so as to make the difference as small as possible. This
image_name:Figure 5.32
description:
[
name: A0, type: OpAmp, value: A0, ports: {InP: Vout, InN: Vi, OutP: Vout(A0),  Vdd: VDD, -Vdd: GND}
name: A1, type: OpAmp, value: A1, ports: {InP: Vout, InN: Vi, OutP: Vout(A1),Vdd: VDD, -Vdd: GND}
name: M1, type: PMOS, ports: {S: VDD, D: Vout, G: Vout(A0)}
name: M2, type: NMOS, ports: {S: -VSS, D: Vout, G: Vout(A1)}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit is a complementary Class AB output stage using embedded common-source output devices. It uses error amplifiers to minimize the voltage difference between input and output, employing negative feedback to reduce output resistance.
image_name:Figure 5.33
description:
[
name: A0, type: OpAmp, value: A0, ports: {InP: Vt, InN: GND, Out: Vgs2}
name: A1, type: OpAmp, value: A1, ports: {InP: Vt, InN: GND, Out: Vgs1}
name: M1, type: PMOS, ports: {S: VDD, D: Vout, G: Vgs1}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: Vgs2}
name: RL, type: Resistor, value: RL, ports: {N1: Vout, N2: GND}
name: g_m1v_gs1, type: CurrentSource, value: g_m1v_gs1, ports: {Np: GND, Nn: Vgs1}
name: g_m2v_gs2, type: CurrentSource, value: g_m2v_gs2, ports: {Np: GND, Nn: Vgs2}
name: r1, type: Resistor, value: r1, ports: {N1: Vgs1, N2: GND}
name: r2, type: Resistor, value: r2, ports: {N1: Vgs2, N2: GND}
name: Ro, type: Resistor, value: Ro, ports: {N1: Vt, N2: Vout}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: Vt, Nn: GND}
]
extrainfo:The circuit is a small-signal model of a complementary Class AB output stage. It uses error amplifiers to sense and minimize the voltage difference between the input and output. The PMOS and NMOS transistors are configured in a push-pull arrangement to drive the output, with feedback reducing the output resistance.

Figure 5.32 A complementary Class AB output stage using embedded common-source output devices.

Figure 5.33 Small-signal model of the output stage in Fig. 5.32 used to find $R_{0}$.
operation can be viewed as negative feedback. A key advantage of the use of negative feedback here is that it reduces the output resistance. Since negative feedback is covered in Chapter 8 , we will analyze this structure with straightforward circuit analysis.

To find the output resistance, consider the small-signal model of this output stage shown in Fig. 5.33. The current $i_{t}$ is

$$
\begin{equation*}
i_{t}=\frac{v_{t}}{r_{o 1}}+\frac{v_{t}}{r_{o 2}}+g_{m 1} A v_{t}+g_{m 2} A v_{t} \tag{5.105}
\end{equation*}
$$

Rearranging this equation to solve for $v_{t} / i_{t}$ gives

$$
\begin{equation*}
R_{o}=\left.\frac{v_{t}}{i_{t}}\right|_{v_{i}=0}=\frac{1}{\left(g_{m 1}+g_{m 2}\right) A}\left\|r_{o 1}\right\| r_{o 2} \tag{5.106}
\end{equation*}
$$

This equation shows that increasing the gain $A$ of the error amplifiers reduces $R_{o}$ and that $R_{o}$ is much less than the drain-source resistance of $M_{1}$ or $M_{2}$ because of the negative feedback.

To find the transfer characteristic, consider the dc model of the output stage shown in Fig. 5.34. The model includes the input-referred offset voltages of the error amplifiers as voltage sources. Assume $k_{p}^{\prime}(W / L)_{1}=k_{n}^{\prime}(W / L)_{2}=k^{\prime}(W / L)$ and $-V_{t 1}=V_{t 2}=V_{t}$. Also assume that the error amplifiers are designed so that $-I_{D 1}=I_{D 2}=I_{Q}$ when $V_{i}=0, V_{O S P}=0$, and $V_{O S N}=0$. Under these conditions, $V_{o}=0$ and

$$
\begin{align*}
& V_{g s 1}=-V_{t}-V_{o v}  \tag{5.107}\\
& V_{g s 2}=V_{t}+V_{o v} \tag{5.108}
\end{align*}
$$

image_name:Figure 5.34
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
name: M1, type: PMOS, ports: {S: VDD, D: Vo, G: Vout(A0)}
name: M2, type: NMOS, ports: {S: -VSS, D: Vo, G: Vout(A1)}
name: A0, type: OpAmp, value: A0, ports: {InP: Vo, InN: InN(A0), OutP: Vout(A0)}
name: A1, type: OpAmp, value: A1, ports: {InP: Vo, InN: Vo, OutP: Vout(A1)}
name: VOSP, type: VoltageSource, value: VOSP, ports: {Np: Vi, Nn: InN(A0)}
name: VOSN, type: VoltageSource, value: VOSN, ports: {Np: Vi, Nn: InN(A1)}
]
extrainfo:The circuit is a differential amplifier with PMOS and NMOS transistors forming a push-pull output stage. The op-amps A0 and A1 are used to control the gates of M1 and M2, respectively, based on the input voltage Vi and offset voltages VOSP and VOSN. The output voltage Vo is taken across the load resistor RL.

Figure 5.34 A dc model of the output stage in Fig. 5.32 used to find the transfer characteristic.
where

$$
\begin{equation*}
V_{o v}=\sqrt{\frac{2 I_{Q}}{k^{\prime}(W / L)}} \tag{5.109}
\end{equation*}
$$

With nonzero input and offsets, the output may not be zero. As a result, the differential input to the top error amplifier changes from zero to $V_{o}-\left(V_{i}-V_{O S P}\right)$. Similarly, the differential input to the bottom error amplifier changes from zero to $V_{o}-\left(V_{i}-V_{O S N}\right)$. Assuming that the output of each error amplifier changes by its gain $A$ times the change in its input,

$$
\begin{align*}
& V_{g s 1}=-V_{t}-V_{o v}+A\left[V_{o}-\left(V_{i}-V_{O S P}\right)\right]  \tag{5.110}\\
& V_{g s 2}=V_{t}+V_{o v}+A\left[V_{o}-\left(V_{i}-V_{O S N}\right)\right] \tag{5.111}
\end{align*}
$$

If $M_{1}$ and $M_{2}$ operate in the active region,

$$
\begin{gather*}
I_{d 1}=-\frac{k_{p}^{\prime}}{2}\left(\frac{W}{L}\right)_{1}\left(V_{g s 1}-V_{t 1}\right)^{2}=-\frac{k^{\prime}}{2} \frac{W}{L}\left(V_{g s 1}+V_{t}\right)^{2}  \tag{5.112}\\
I_{d 2}=\frac{k_{n}^{\prime}}{2}\left(\frac{W}{L}\right)_{2}\left(V_{g s 2}-V_{t 2}\right)^{2}=\frac{k^{\prime}}{2} \frac{W}{L}\left(V_{g s 2}-V_{t}\right)^{2} \tag{5.113}
\end{gather*}
$$

Also,

$$
\begin{equation*}
I_{o}=\frac{V_{o}}{R_{L}} \tag{5.114}
\end{equation*}
$$

From KCL at the output,

$$
\begin{equation*}
I_{o}+I_{d 1}+I_{d 2}=0 \tag{5.115}
\end{equation*}
$$

Substituting (5.110)-(5.114) into (5.115) and rearranging gives

$$
\begin{equation*}
V_{o}=\frac{V_{i}-\frac{V_{O S P}+V_{O S N}}{2}}{1+\frac{1}{k^{\prime} \frac{W}{L} A\left[2 V_{o v}-A\left(V_{O S P}-V_{O S N}\right)\right] R_{L}}} \tag{5.116}
\end{equation*}
$$

If $V_{O S P}=V_{O S N}=0$,

$$
\begin{equation*}
V_{o}=\frac{V_{i}}{1+\frac{1}{k^{\prime} \frac{W}{L} A 2 V_{o v} R_{L}}}=\frac{V_{i}}{1+\frac{1}{2 A g_{m} R_{L}}} \simeq V_{i}\left(1-\frac{1}{2 A g_{m} R_{L}}\right) \tag{5.117}
\end{equation*}
$$

where $g_{m}=k^{\prime}(W / L) V_{o v}$ as shown in (1.180). The term $\left(2 A g_{m} R_{L}\right)$ is the gain around the feedback loop or the loop gain and is usually chosen to be high enough to make the slope of the transfer characteristic to be unity within an allowable gain error. (The concept of loop gain is described in Chapter 8.) The gain error here is approximately $1 /\left(2 A g_{m} R_{L}\right)$. The key point is that the error is reduced if $A, g_{m}$, or $R_{L}$ are increased.

With nonzero offsets, (5.116) shows that the circuit also displays an offset error. If $A\left(V_{O S P}-V_{O S N}\right) \ll 2 V_{o v}$ and $2 A g_{m} R_{L} \gg 1$,

$$
\begin{equation*}
V_{o} \simeq \frac{V_{i}-\frac{V_{O S P}+V_{O S N}}{2}}{1+\frac{1}{k^{\prime} \frac{W}{L} A 2 V_{O V} R_{L}}}=\frac{V_{i}-\frac{V_{O S P}+V_{O S N}}{2}}{1+\frac{1}{2 A g_{m} R_{L}}} \simeq V_{i}-\frac{V_{O S P}+V_{O S N}}{2} \tag{5.118}
\end{equation*}
$$

Therefore, the input offset voltage of the buffer is about $-\left(V_{O S P}+V_{O S N}\right) / 2$.
Equation 5.116 is valid as long as both $M_{1}$ and $M_{2}$ operate in the active region. If the magnitude of the output voltage is large enough, however, one of the two output transistors turns off. For example, when $V_{i}$ increases, $V_{o}$ also increases but the gain is slightly less than unity. As a result, the differential inputs to the error amplifiers both decrease, decreasing $V_{g s 1}$ and $V_{g s 2}$. In turn, these changes increase $\left|I_{d 1}\right|$ but reduce $I_{d 2}$, and $M_{2}$ turns off for large enough $V_{i}$. To find the portion of the transfer characteristic with $M_{1}$ in the active region but $M_{2}$ off, the above analysis can be repeated with $I_{d 2}=0$. See Problem 5.23.

The primary motivation for using the quasi-complementary configuration is to increase the output swing. If the output transistors are not allowed to operate in the triode region, the output voltage can pull within an overdrive of either supply. This result is an improvement compared to the limit given in (5.103) for the common-drain output stage mostly because the threshold voltages of the output transistors do not limit the output swing in the common-source configuration.

Although quasi-complementary circuits improve the output swing, they suffer from two main problems. First, the error amplifiers must have large bandwidth to prevent crossover distortion problems for high input frequencies. Unfortunately, increasing the bandwidth of the error amplifiers worsens the stability margins, especially in the presence of large capacitive loads. As a result, these circuits present difficult design problems in compensation. The topics of stability and compensation are covered in Chapter 9. Second, nonzero offset voltages in the error amplifiers change the quiescent current flowing in the output transistors. From a design standpoint, the quiescent current is chosen to be barely high enough to limit crossover distortion to an acceptable level. Although further increases in the quiescent current reduce the crossover distortion, such increases also increase the power dissipation and reduce the output swing. Therefore, proper control of the quiescent current with nonzero offsets is also a key design constraint.

One way to control the quiescent current is to sense and feedback a copy of the current. ${ }^{12}$ This method is not considered further here. Another way to limit the variation in the quiescent current is to design the error amplifiers to have low gain. ${ }^{13,14}$ The concept is that the quiescent current is controlled by the gate-source voltages on the output transistors, which in turn are controlled by the outputs of the error amplifiers. Therefore, reducing the error-amplifier gain reduces the variation of gate-source voltages and the quiescent current for a given variation in the offset voltages.

To study this situation quantitatively, define the quiescent current in the output devices as the common-mode component of the current flowing from $V_{D D}$ to $-V_{S S}$ with $V_{i}=0$. Then

$$
\begin{equation*}
I_{Q}=\frac{I_{D 2}-I_{D 1}}{2} \tag{5.119}
\end{equation*}
$$

Subtraction is used in the above equation because the drain current of each transistor is defined as positive when it flows into the transistor. Substituting (5.110)-(5.113) into (5.119) gives

$$
\begin{equation*}
I_{Q}=\frac{k^{\prime}}{4} \frac{W}{L}\left(\left(V_{o v}+A\left[V_{o}+V_{O S N}\right]\right)^{2}+\left(-V_{o v}+A\left[V_{o}+V_{O S P}\right]\right)^{2}\right) \tag{5.120}
\end{equation*}
$$

Since $V_{o}=0$ if $V_{O S P}=V_{O S N}=0,(5.120)$ shows that

$$
\begin{equation*}
\left.I_{Q}\right|_{\substack{V_{O S P}=0 \\ V_{O S N}=0}}=\frac{k^{\prime}}{4} \frac{W}{L}\left(\left(V_{o v}\right)^{2}+\left(-V_{o v}\right)^{2}\right)=\frac{k^{\prime}}{2} \frac{W}{L}\left(V_{o v}\right)^{2} \tag{5.121}
\end{equation*}
$$

From (5.118) with $V_{i}=0$,

$$
\begin{align*}
& V_{o}+V_{O S P} \simeq \frac{V_{O S P}-V_{O S N}}{2}  \tag{5.122}\\
& V_{o}+V_{O S N} \simeq-\frac{V_{O S P}-V_{O S N}}{2} \tag{5.123}
\end{align*}
$$

Substituting (5.122) and (5.123) into (5.120) gives

$$
\begin{equation*}
I_{Q}=\frac{k^{\prime}}{2} \frac{W}{L}\left(V_{o v}-A\left[\frac{V_{O S P}-V_{O S N}}{2}\right]\right)^{2} \tag{5.124}
\end{equation*}
$$

Define $\Delta I_{Q}$ as the change in $I_{Q}$ caused by nonzero offsets; that is,

$$
\begin{equation*}
\Delta I_{Q}=\left.I_{Q}\right|_{\substack{V_{O S P}=0 \\ V_{O S N}=0}}-I_{Q} \tag{5.125}
\end{equation*}
$$

Substituting (5.124) and (5.121) into (5.125) gives

$$
\begin{equation*}
\Delta I_{Q}=\frac{k^{\prime}}{2} \frac{W}{L} A\left(V_{O S P}-V_{O S N}\right)\left[V_{o v}-A\left(\frac{V_{O S P}-V_{O S N}}{4}\right)\right] \tag{5.126}
\end{equation*}
$$

To evaluate the magnitude of $\Delta I_{Q}$, we will compare it to the quiescent current with zero offsets by dividing ( 5.126 ) by (5.121). The result is

$$
\begin{equation*}
\frac{\Delta I_{Q}}{\left.I_{Q}\right|_{\substack{V O S P=0 \\ V_{O S N}=0}}}=A\left(\frac{V_{O S P}-V_{O S N}}{V_{o v}}\right)\left[1-A\left(\frac{V_{O S P}-V_{O S N}}{4 V_{o v}}\right)\right] \tag{5.127}
\end{equation*}
$$

If $A\left(V_{O S P}-V_{O S N}\right) \ll 4 V_{o v}$,

Therefore, to keep the fractional change in the quiescent current less than a given amount, the maximum error-amplifier gain is

$$
\begin{equation*}
A<\left(\frac{V_{o v}}{V_{O S P}-V_{O S N}}\right)\left(\frac{\Delta I_{Q}}{\left.I_{Q}\right|_{\substack{V_{O S P}=0 \\ V_{O S N}=0}}}\right) \tag{5.129}
\end{equation*}
$$

For example, if $V_{o v}=200 \mathrm{mV}, V_{O S P}-V_{O S N}=5 \mathrm{mV}$, and up to 20 percent variation in the quiescent current is allowed, (5.129) shows that the error amplifier gain should be less than about $8 .{ }^{13,14}$

Figure 5.35 shows a schematic of the top error amplifier and $M_{1}$ from Fig. 5.32. ${ }^{14} \mathrm{~A}$ complementary structure used to drive $M_{2}$ is not shown. The difference between $V_{i}$ and $V_{o}$ is sensed by the differential pair $M_{11}$ and $M_{12}$, which is biased by the tail current source $I_{\text {TAIL }}$. The load of the differential pair consists of two parts: current mirror $M_{13}$ and $M_{14}$ and commondrain transistors $M_{15}$ and $M_{16}$. The purpose of the common-drain transistors is to reduce the
image_name:Figure 5.35
description:The circuit is an error amplifier with a differential pair (M11, M12) biased by a tail current source (ITAIL). The load consists of a current mirror (M13, M14) and common-drain transistors (M15, M16) to reduce output resistance. Negative feedback is used to adjust the voltage at the gate of M15, ensuring M17 operates in the active region.

Figure 5.35 Schematic of the top error amplifier and output transistor $M_{1}$.
output resistance of the error amplifier to set its gain to a well-defined low value. The gates of the common-drain transistors are biased by a negative feedback loop including $M_{13}, M_{17}, I_{\mathrm{BIAS}}$, and $M_{15}$. This circuit adjusts the voltage at the gate of $M_{15}$ so that $M_{17}$ operates in the active region and conducts $I_{\text {BIAS }}$. Although negative feedback is studied in Chapter 8 , the basic idea can be understood here as follows. If $\left|I_{D 17}\right|$ is less than $I_{\mathrm{BIAS}}$, current source $I_{\mathrm{BIAS}}$ pulls the gate voltage of $M_{15}$ down. Since $M_{15}$ operates as a source follower, the source of $M_{15}$ is pulled down, increasing $\left|I_{D 13}\right|$. Because $M_{13}$ and $M_{17}$ together form a current mirror, $\left|I_{D 17}\right|$ also increases until $\left|I_{D 17}\right|=I_{\text {BIAS }}$. Similar reasoning shows that this equality is established when $\left|I_{D 17}\right|$ is initially greater than $I_{\text {BIAS }}$. If $M_{15}$ and $M_{17}$ are enhancement-mode devices, $M_{17}$ operates in the active region because $V_{G D 17}=V_{S G 15}=\left|V_{t 15}\right|+\left|V_{o v 15}\right|>0>V_{t 17}$; therefore, the channel does not exist at the drain of $M_{17}$.

Since $M_{13}$ and $M_{17}$ form a current mirror,

$$
\begin{equation*}
I_{D 13}=I_{D 17} \frac{(W / L)_{13}}{(W / L)_{17}}=-I_{\mathrm{BIAS}} \frac{(W / L)_{13}}{(W / L)_{17}} \tag{5.130}
\end{equation*}
$$

Since $M_{13}$ and $M_{14}$ also form a current mirror, and since $(W / L)_{14}=(W / L)_{13}$,

$$
\begin{equation*}
I_{D 14}=I_{D 13}=-I_{\mathrm{BIAS}} \frac{(W / L)_{13}}{(W / L)_{17}} \tag{5.131}
\end{equation*}
$$

With $V_{i}=V_{o}$,

$$
\begin{equation*}
I_{D 11}=I_{D 12}=\frac{I_{\mathrm{TAIL}}}{2} \tag{5.132}
\end{equation*}
$$

From KCL,

$$
\begin{equation*}
I_{D 16}=I_{D 14}+I_{D 11} \tag{5.133}
\end{equation*}
$$

Substituting (5.131) and (5.132) into (5.133) gives

$$
\begin{equation*}
I_{D 16}=-I_{\mathrm{BIAS}} \frac{(W / L)_{13}}{(W / L)_{17}}+\frac{I_{\mathrm{TAIL}}}{2} \tag{5.134}
\end{equation*}
$$

Since $I_{D 15}=I_{D 16}$ when $I_{D 11}=I_{D 12}$,

$$
\begin{equation*}
V_{S D 14}=V_{S D 13}=V_{S G 13}=V_{S G 1} \tag{5.135}
\end{equation*}
$$

Therefore, ignoring channel-length modulation,

$$
\begin{equation*}
I_{D 1}=I_{D 13} \frac{(W / L)_{1}}{(W / L)_{13}} \tag{5.136}
\end{equation*}
$$

Substituting (5.130) into (5.136) and rearranging gives

$$
\begin{equation*}
I_{D 1}=-I_{\mathrm{BIAS}} \frac{(W / L)_{1}}{(W / L)_{17}} \tag{5.137}
\end{equation*}
$$

This equation shows that the drain current in $M_{1}$ is controlled by $I_{\text {BIAS }}$ and a ratio of transistor sizes if the offset voltage of the error amplifier is zero so that $V_{o}=0$ when $V_{i}=0$. In practice, $(W / L)_{1} \gg(W / L)_{17}$ so that little power is dissipated in the bias circuits.

Another design consideration comes out of these equations. To keep the gain of the error amplifier low under all conditions, $M_{16}$ must never cut off. Therefore, from (5.133), $\left|I_{D 14}\right|$ should be greater than the maximum value of $I_{D 11}$. Since the maximum value of $I_{D 11}$ is $I_{\text {TAIL }}$, (5.131) and (5.133) show that

$$
\begin{equation*}
\left|I_{D 14}\right|=I_{\mathrm{BIAS}} \frac{(W / L)_{13}}{(W / L)_{17}}>I_{\mathrm{TAIL}} \tag{5.138}
\end{equation*}
$$

To find the gain of the error amplifier, the key observation is that the small-signal resistance looking into the source of of $M_{15}$ is zero, ignoring channel-length modulation. This result stems from the operation of the same negative feedback loop that biases the gate of $M_{15}$. If the small-signal voltage at the source of $M_{15}$ changes, the negative feedback loop works to undo the change. For example, suppose that the source voltage of $M_{15}$ increases. This change reduces the gate voltage of $M_{15}$ because $M_{17}$ operates as a common-source amplifier. Then the source voltage of $M_{15}$ falls because $M_{15}$ operates as a source follower. Ignoring channel-length modulation, the source voltage of $M_{15}$ must be held exactly constant because $i_{d 17}=0$ if $I_{\text {BIAS }}$ is constant. Therefore, the small-signal resistance looking into the source of $M_{15}$ is zero. As a result, none of the small-signal drain current from $M_{12}$ flows in $M_{13}$. Instead, it all flows in the source of $M_{15}$. To calculate the transconductance of the error amplifier, the output at the drain of $M_{16}$ is connected to a small-signal ground. Since $M_{15}$ and $M_{16}$ share the same gate connection, and since their sources each operate at small-signal grounds, the small-signal current in $M_{15}$ is copied to $M_{16}$. Therefore, the entire small-signal current from the differential pair flows at the error-amplifier output and the transconductance is

$$
\begin{equation*}
G_{m}=g_{m 11}=g_{m 12} \tag{5.139}
\end{equation*}
$$

Ignoring channel-length modulation, the output resistance is set by common-drain transistor $M_{16}$. From (3.84),

$$
\begin{equation*}
R_{o}=\frac{1}{g_{m 16}+g_{m b 16}} \tag{5.140}
\end{equation*}
$$

Therefore, the gain of the error amplifier is

$$
\begin{equation*}
A=G_{m} R_{o}=\frac{g_{m 11}}{g_{m 16}+g_{m b 16}} \tag{5.141}
\end{equation*}
$$

### 5.5.3 Alternative Configurations

The main potential advantage of the common-source output stage described in the last section is that it can increase the output swing compared to the common-drain case. However, the common-source configuration suffers from an increase in harmonic distortion, especially at high frequencies, for two main reasons. First, the bandwidth of the error amplifiers is usually limited, to avoid stability problems. Second, the gain of these amplifiers is limited to establish adequate control on the quiescent output current.

#### 5.5.3.1 Combined Common-Drain Common-Source Configuration

One way to overcome this problem is to use a combination of the common-drain and commonsource configurations shown in Fig. 5.31 and Fig. 5.32. ${ }^{15}$ The combined schematic is shown in Fig. 5.36. The key aspect of this circuit is that it uses two buffers connected to the output: a Class AB common-drain buffer ( $M_{1}-M_{2}$ ) and a Class B quasi-complementary common-source buffer ( $M_{11}-M_{12}$ and the error amplifiers $A$ ). The common-source buffer is dominant when the output swing is maximum, but off with zero output. On the other hand, the commondrain buffer controls the quiescent output current and improves the frequency response, as described next.

From KVL,

$$
\begin{equation*}
V_{o}=V_{1}+V_{g s 4}-V_{g s 1} \tag{5.142}
\end{equation*}
$$

If $V_{t 1}=V_{t 4}$, this equation can be rewritten as

$$
\begin{equation*}
V_{o}=V_{1}+V_{o v 4}-V_{o v 1} \tag{5.143}
\end{equation*}
$$

Therefore, when $V_{i}$ is adjusted so that $V_{1}=0, M_{1}-M_{5}$ force $V_{o}=0$ if $V_{o v 1}=V_{o v 4}$. From (1.166), $V_{o v 1}=V_{o v 4}$ if

$$
\begin{equation*}
\frac{I_{D 1}}{(W / L)_{1}}=\frac{I_{D 4}}{(W / L)_{4}} \tag{5.144}
\end{equation*}
$$

Substituting (5.101) into (5.144) and rearranging shows that $V_{o v 1}=V_{o v 4}$ if

$$
\begin{equation*}
\frac{(W / L)_{1}}{(W / L)_{2}}=\frac{(W / L)_{4}}{(W / L)_{5}} \tag{5.145}
\end{equation*}
$$

image_name:Figure 5.36 Combined common-drain, common-source output stage
description:The circuit is a combined common-drain, common-source output stage with two error amplifiers (A0 and A1) providing feedback to control the output voltage Vo. The circuit includes a biasing network and is designed to maintain Vo at 0 when V1 is 0. The PMOS and NMOS transistors are configured to manage the current flow and maintain stability in the output stage.

Figure 5.36 Combined common-drain, common-source output stage.

We will assume that this condition holds so that $V_{o}=0$ when $V_{1}=0$. In this case, $M_{11}$ and $M_{12}$ are designed to be cut off. This characteristic stems from small offsets designed into the error amplifiers. These offsets are shown as voltage sources $V_{O S}$ in Fig. 5.36 and can be introduced by intentionally mismatching the input differential pair in each error amplifier. With $V_{1}=V_{o}=0$ and $V_{O S}>0$, the error amplifiers are designed to give $V_{g s 11}>V_{t 11}$ and $V_{g s 12}<V_{t 12}$ so that $M_{11}$ and $M_{12}$ are off. As a result, the quiescent output current is controlled by the common-drain stage and its biasing circuit $M_{1}-M_{5}$, as shown in (5.101).

As $V_{i}$ decreases from the value that forces $V_{1}=0, V_{1}$ increases and $V_{o}$ follows but with less than unity gain if $R_{L}$ is finite. Therefore $V_{1}-V_{o}$ increases, and both $V_{g s 11}$ and $V_{g s 12}$ decrease, eventually turning on $M_{11}$ but keeping $M_{12}$ off. After $M_{11}$ turns on, both $I_{d 1}$ and $\left|I_{d 11}\right|$ increase as $V_{o}$ rises until $V_{g s 1}-V_{t 1}$ reaches its maximum value. Such a maximum occurs when the output swing from the common-source stage is greater than that of the common-drain stage. As $V_{o}$ rises beyond this point, $\left|I_{d 11}\right|$ increases but $I_{d 1}$ decreases, and the common-source stage becomes dominant.

From (5.103), the output swing allowed by the common-drain stage in Fig. 5.31 is limited in part by $V_{g s 1}$, which includes a threshold component. On the other hand, the output swing limitation of common-source stage in Fig. 5.32 does not include a threshold term, and this circuit can swing within an overdrive of the positive supply. So with proper design, we expect the common-source stage to have a larger output swing than the common-drain stage. When the two circuits are combined as in Fig. 5.36, however, the output swing is limited by the driver stage that produces $V_{1}$. Define $V_{1}^{+}$as the maximum value of $V_{1}$ for which $M_{3}$ operates in the active region. Then

$$
\begin{equation*}
V_{1}^{+}=V_{D D}-\left|V_{o v 3}\right|-V_{g s 4} \tag{5.146}
\end{equation*}
$$

Since $V_{1}$ is the input to the common-source stage, the maximum output $V_{o}^{+}$can be designed to be

$$
\begin{equation*}
V_{o}^{+} \simeq V_{1}^{+}=V_{D D}-\left|V_{o v 3}\right|-V_{g s 4} \tag{5.147}
\end{equation*}
$$

Comparing (5.147) with (5.103) shows that the positive swing of the combined output stage in Fig. 5.36 exceeds that of the common-drain output stage in Fig. 5.31 provided that $V_{g s 4}<V_{g s 1}$ when $V_{o}=V_{o}^{+}$. This condition is usually satisfied because $I_{d 4} \ll I_{d 1}$ when the output is maximum with finite $R_{L}$. Therefore, the circuit in Fig. 5.36 can be designed to increase the output swing.

Since the common-source stage in Fig. 5.36 is not responsible for establishing the quiescent output current, the gain of the error amplifiers in Fig. 5.36 is not limited as in (5.129). In practice, the error amplifiers are often designed as one-stage amplifiers with a gain related to the product of $g_{m}$ and $r_{o}$ that can be achieved in a given technology. This increase in gain reduces the harmonic distortion because it reduces the error between the input and the output of the common-source stage.

Finally, we will consider the frequency response of the circuit in Fig. 5.36 qualitatively. The circuit has two paths from $V_{1}$ to the output. The path through the common-source transistors $M_{11}$ and $M_{12}$ may be slow because of the need to limit the bandwidth of the error amplifiers to guarantee that the circuit is stable. (Stability is studied in Chapter 9.) On the other hand, the path through the common-drain transistors $M_{1}$ and $M_{2}$ is fast because source followers are high-bandwidth circuits, as shown in Chapter 7. Since the circuit sums the current from the common-drain and common-source stages in the load to produce the output voltage, the fast path will dominate for high-frequency signals. This technique is called feedforward, and other instances are described in Chapter 9. It causes the circuit to take on the characteristics of the source followers for high frequencies, reducing the phase shift that would otherwise be introduced by the slow error amplifiers. As a result, the design required
image_name:Figure 5.37 Combined common-drain, common-source output stage with improved swing.
description:The circuit combines common-drain and common-source stages to improve output swing. It uses a feedforward technique to enhance high-frequency performance and reduce phase shift. The design includes an operational amplifier for error correction and improved stability.

Figure 5.37 Combined common-drain, common-source output stage with improved swing.
to guarantee stability is simplified, ${ }^{15}$ and the harmonic distortion for high-frequency signals is reduced.

#### 5.5.3.2 Combined Common-Drain Common-Source Configuration with High Swing

Although the swing of the circuit in Fig. 5.36 is improved compared to the circuit in Fig. 5.31, it can be improved even further. As shown in (5.147), the main limitation to the positive swing in Fig. 5.36 stems from $V_{g s 4}$. This voltage includes a threshold component, which increases with increasing $V_{1}$ and $V_{o}$ because of the body effect. Similarly, the negative swing is limited by $V_{g s 5}$, whose threshold component increases in magnitude as $V_{1}$ and $V_{o}$ decrease. In practice, these terms alone reduce the available output swing by about 1.5 V to 2 V .

Figure 5.37 shows a circuit that overcomes this limitation. ${ }^{16}$ The circuit is the same as in Fig. 5.36 except that one extra branch is included. The new branch consists of transistors $M_{7}$ and $M_{8}$ and operates in parallel with the branch containing $M_{3}-M_{6}$ to produce voltage $V_{1}$. The swing of $V_{1}$ in Fig. 5.36 is limited by the threshold voltages of $M_{4}$ and $M_{5}$ as described above. In contrast, the new branch in Fig. 5.37 can drive $V_{1}$ within an overdrive of either supply while $M_{7}$ and $M_{8}$ operate in the active region. Since the output swing in Fig. 5.36 is limited by the swing of $V_{1}$, improving the swing of $V_{1}$ as in Fig. 5.37 also improves the output swing.

#### 5.5.3.3 Parallel Common-Source Configuration

Another circuit that overcomes the problem described in the introduction of Section 5.5.3 is shown in Fig. 5.38. ${ }^{17}$ Like the circuit in Fig. 5.37, this circuit combines two buffers in parallel at the output. The error amplifiers with gain $A_{1}$ along with $M_{1}$ and $M_{2}$ form one buffer, which controls the operation of the output stage with $V_{i}=0$. The error amplifiers with gain $A_{2}$ together with $M_{11}$ and $M_{12}$ form the other buffer, which dominates the operation of the output stage for large-magnitude output voltages.

This behavior stems from small offset voltages intentionally built into the $A_{1}$ amplifiers. These offsets are shown as voltage sources $V_{O S}$ in Fig. 5.38 and are introduced in practice by intentionally mismatching the input differential pairs in the $A_{1}$ amplifiers. At first, assume that these offsets have little effect on the drain currents of $M_{1}$ and $M_{2}$ because $A_{1}$ is intentionally chosen to be small. Therefore, $M_{1}$ and $M_{2}$ operate in the active region when $V_{i}=0$, and the buffer that includes these transistors operates in a Class AB mode. On the other hand, the offsets force $M_{11}$ and $M_{12}$ to operate in cutoff when $V_{i}=0$ because the gates of these transistors
image_name:Figure 5.39
description:The circuit is a differential amplifier with Class AB and Class B output stages. It uses NMOS transistors and operational amplifiers to drive the output load, RL. The input signal Vi is amplified by the A1 op-amp, and the amplified signals control the gates of M1 and M2. The A2 op-amps drive the gates of M11 and M12, forming the output stage. The circuit operates with a positive supply voltage VDD and a negative supply voltage VSS.

Figure 5.38 Output stage with a Class AB common-source buffer and a Class B common-source buffer.
image_name:Figure 5.39 Schematic of the top A1 amplifier and output transistor M1
description:The circuit is a differential amplifier with PMOS load and NMOS input pair. It is powered by VDD and VSS, with IBIAS and ITAIL providing biasing currents. The output is taken from node Vo.

Figure 5.39 Schematic of the top $A_{1}$ amplifier and output transistor $M_{1}$.
are driven by the outputs of the $A_{2}$ amplifiers, which in turn are driven by the differential outputs of the $A_{1}$ amplifiers. In particular, the product $V_{O S} A_{1} A_{2}$ is chosen by design to be big enough to force $V_{g s 11}>V_{t 11}$ and $V_{g s 12}<V_{t 12}$ so that $M_{11}$ and $M_{12}$ are off when $V_{i}=0$. As a result, the quiescent output current of this output stage is controlled by $M_{1}, M_{2}$, and the $A_{1}$ amplifiers.

Figure 5.39 shows a schematic of the top $A_{1}$ amplifier and $M_{1}$ from Fig. 5.38. ${ }^{17}$ A complementary configuration is used for the bottom $A_{1}$ amplifier but is not shown for simplicity. The difference between $V_{i}$ and $V_{o}$ is sensed by the differential pair $M_{3}$ and $M_{4}$. The load of the differential pair consists of two parts: diode-connected transistors $M_{5}$ and $M_{6}$ and current sources $I_{\text {BIAS }}$, which are implemented by the outputs of $p$-channel current mirrors in practice. The purpose of the diode-connected transistors is to limit the gain of the error amplifier to a small value so that the output quiescent current is well controlled. Ignoring channel-length modulation, the gain of this error amplifier is

$$
\begin{equation*}
A_{1}=\frac{g_{m 3}}{g_{m 5}} \tag{5.148}
\end{equation*}
$$

where $A_{1}$ is the gain from the differential input to the differential output of the error amplifier. This equation shows that the gain is determined by the ratios of the transconductance of a differential-pair transistor to that of a load transistor. Substituting (1.180) into (5.148) for each transistor, and rearranging gives

$$
\begin{equation*}
A_{1}=\sqrt{\frac{k_{n}^{\prime}}{k_{p}^{\prime}} \frac{(W / L)_{3}}{(W / L)_{5}} \frac{I_{D 3}}{\left|I_{D 5}\right|}} \tag{5.149}
\end{equation*}
$$

This equation shows that the gain is determined by the product of the ratios of the transconductance parameters, the transistor sizes, and the bias currents. From KCL at the drain of $M_{5}$,

$$
\begin{equation*}
-I_{D 5}=I_{D 3}-I_{\mathrm{BIAS}} \tag{5.150}
\end{equation*}
$$

where $I_{D 3}>I_{\text {BIAS }}$. Substituting (5.150) into (5.149) gives

$$
\begin{equation*}
A_{1}=\sqrt{\frac{k_{n}^{\prime}}{k_{p}^{\prime}} \frac{(W / L)_{3}}{(W / L)_{5}}\left(\frac{I_{D 3}}{I_{D 3}-I_{\mathrm{BIAS}}}\right)} \tag{5.151}
\end{equation*}
$$

This equation shows that the purpose of the $I_{\text {BIAS }}$ current sources is to allow the bias current in a transistor in the differential pair to exceed that in a diode-connected load. As a result, the term in parentheses in (5.151) is greater than unity and contributes to the required gain.

Now consider the effect of the offset $V_{O S}$ in Fig. 5.38. In practice, the offset is implemented in Fig. 5.39 by choosing the width of $M_{3}$ to be less than the width of $M_{4}$ by about 20 percent. ${ }^{17}$ Assume that $V_{o}=0$ when $V_{i}=0$. Increasing $V_{O S}$ reduces $I_{D 3}$, making $\left|I_{D 5}\right|$ less than the value given in (5.150). Since $M_{5}$ and $M_{1}$ form a current mirror, a positive offset reduces $\left|I_{D 1}\right|$. Under the assumption that $V_{o}=0$ when $V_{i}=0$, the differential pair in the error amplifier operates with $V_{g s 3}=V_{g s 4}$. Therefore, if $V_{t 3}=V_{t 4}, V_{o v 3}=V_{o v 4}$. From (1.166),

$$
\begin{equation*}
\frac{I_{D 3}}{(W / L)_{3}}=\frac{I_{D 4}}{(W / L)_{4}} \tag{5.152}
\end{equation*}
$$

Substituting $I_{D 3}+I_{D 4}=I_{\text {TAIL }}$ into (5.152) and rearranging gives

$$
\begin{equation*}
I_{D 3}=\frac{(W / L)_{3}}{(W / L)_{3}+(W / L)_{4}} I_{\mathrm{TAIL}} \tag{5.153}
\end{equation*}
$$

when $V_{o}=V_{i}=0$. Similarly, a positive offset in the bottom $A_{1}$ amplifier as labeled in Fig. 5.38 reduces $I_{D 2}$. If the tail and bias current in the top $A_{1}$ amplifier are identical to the corresponding values in the bottom $A_{1}$ amplifier, and if the fractional mismatches in the differential pairs are identical, the reductions in $\left|I_{D 1}\right|$ and $I_{D 2}$ caused by the mismatches intentionally introduced into the differential pairs are equal and $V_{o}=0$ when $V_{i}=0$ is assumed. In other words, the offset of the entire output stage shown in Fig. 5.38 is zero even with nonzero $V_{O S}$ in the error amplifiers.

Because a design goal is to bias $M_{1}$ in the active region when $V_{i}=0$, the offset must be chosen to be small enough that $I_{D 3}>0$ when $V_{o}=V_{i}=0$. Also, the error amplifiers contain some unintentional mismatches stemming from random effects in practice. Because another design goal is to bias $M_{11}$ in cutoff, the random component must not be allowed to be larger than the systematic offset in magnitude and opposite in polarity. Therefore, $V_{O S}$ is chosen to be bigger than the expected random offset.

Since the quiescent output current is controlled by the $A_{1}$ error amplifiers along with $M_{1}$ and $M_{2}$, the gain of the $A_{2}$ error amplifiers driving $M_{11}$ and $M_{12}$ need not be small. With large $A_{2}, M_{11}$ or $M_{12}$ becomes the dominant output device for large output magnitudes if the aspect ratios of $M_{11}$ and $M_{12}$ are at least as big as $M_{1}$ and $M_{2}$, respectively. Furthermore, increasing $A_{2}$ has the advantage of increasing the loop gain when $M_{11}$ or $M_{12}$ turns on. This loop gain
image_name:Figure 5.40 Schematic of the top A2 amplifier
description:
[
name: M21, type: PMOS, ports: {S: VDD, D: X1, G: V2t}
name: M22, type: PMOS, ports: {S: VDD, D: Vg11, G: V2t}
name: M23, type: NMOS, ports: {S: X2, D: X1, G: BIAS}
name: M24, type: NMOS, ports: {S: X3, D: Vg11, G: BIAS}
name: M25, type: NMOS, ports: {S: -VSS, D: X2, G: X1}
name: M26, type: NMOS, ports: {S: -VSS, D: X3, G: X1}
]
extrainfo:This circuit is a part of a differential amplifier configuration. It uses PMOS transistors M21 and M22 as loads for the differential pair formed by NMOS transistors M23 and M24. NMOS transistors M25 and M26 form current sources for the differential pair. The circuit is biased with a BIAS voltage to control the NMOS transistors.

Figure 5.40 Schematic of the top $A_{2}$ amplifier.
is related to the product of $A_{2}, g_{m 11}$ or $g_{m 12}$, and $R_{L}$. Increasing the loop gain reduces the error between the input and output, as shown in Chapter 8. If $M_{11}$ conducts, increasing $A_{2}$ allows the output stage to drive reduced loads with constant $g_{m 11}$ and error. If the load is fixed, increasing $A_{2}$ allows the transconductance to be reduced, which in turn allows $(W / L)_{11}$ to be reduced. One potential concern here is that reducing the transistor sizes also reduces the range of outputs for which the devices operate in the active region. If $M_{11}$ operates in the triode region, its drain-source resistance $r_{o 11}$ is finite, and the loop gain is proportional to the product $A_{2} g_{m 11}\left(r_{o 11} \| R_{L}\right)$. Thus, operation of $M_{11}$ in the triode region increases the error by reducing $g_{m 11}$ and $r_{o 11}$. However, increasing $A_{2}$ compensates for this effect. Therefore, a key advantage of the output-stage configuration shown in Fig. 5.38 is that it allows the output swing with a given level of nonlinearity to be increased by allowing the dominant transistor to operate in the triode region.

The $A_{1}$ and $A_{2}$ amplifiers together form the two-stage error amplifiers that drive $M_{11}$ and $M_{12}$. The $A_{2}$ amplifiers operate on the differential outputs of the $A_{1}$ amplifiers. Since the common-mode components of the outputs of the $A_{1}$ amplifiers are well controlled by diode-connected loads, differential pairs are not required at the inputs of the $A_{2}$ amplifiers. Figure 5.40 shows a schematic of the top $A_{2}$ amplifier. ${ }^{17}$ A complementary configuration used for the bottom $A_{2}$ amplifier is not shown for simplicity. The inputs are applied to the gates of common-source transistors $M_{21}$ and $M_{22}$. The cascode current mirror $M_{23}-M_{26}$ then converts the differential signal into a single-ended output. Because the output resistance of the cascode-current mirror is large compared to the output resistance of the common-source transistor $M_{22}$,

$$
\begin{equation*}
A_{2} \simeq g_{m 22} r_{o 22} \tag{5.154}
\end{equation*}
$$

and $A_{2} \simeq 70$ in Ref. 17 .
To determine the range of input voltages for which $M_{11}$ and $M_{12}$ are both off, let $V_{g 11}$ represent the voltage from the gate of $M_{11}$ to ground. Assuming that the gains $A_{1}$ and $A_{2}$ are constant,

$$
\begin{equation*}
V_{g 11}=\left[V_{o}-\left(V_{i}-V_{O S}\right)\right] A_{1} A_{2}+K \tag{5.155}
\end{equation*}
$$

where $K$ is a constant. If the differential input voltage to the top $A_{2}$ amplifier shown in Fig. 5.40 is zero, $V_{g 11}=-V_{S S}+V_{t 25}+V_{o v 25}$ so that $I_{d 21}=I_{d 22}$. Substituting this boundary condition
image_name:Figure 5.41
description:1. **Type of Graph and Function:**
The graph in Figure 5.41 is a linear plot showing the relationship between the output voltage \( V_o \) and the input voltage \( V_i \). This is likely a part of a transfer characteristic curve for a transistor or amplifier circuit.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( V_i \), representing the input voltage. Units are likely in volts, although not explicitly stated.
- The vertical axis is labeled \( V_o \), representing the output voltage, also presumably in volts.
- The scale appears linear for both axes.

3. **Overall Behavior and Trends:**
- The graph shows two linear segments with different slopes, indicating different gain regions or operating conditions of the circuit.
- The line labeled "From (5.157)" has a shallower slope compared to the line "From (5.159)", suggesting a change in gain.

4. **Key Features and Technical Details:**
- The graph intersects the vertical axis at \(-V_{OS}\), indicating an offset voltage.
- The point \( V_{i(\min)} \) is marked on the \( V_i \) axis, representing the minimum input voltage needed to turn on \( M_{11} \) in the circuit described in the context.
- The intersection of the two lines suggests a change in operating mode or regime of the circuit.

5. **Annotations and Specific Data Points:**
- The graph includes two annotations "From (5.159)" and "From (5.157)", indicating specific equations or conditions related to different segments of the graph.
- A vertical dashed line is drawn at \( V_{i(\min)} \), highlighting its significance as a threshold or critical point.

Figure 5.41 Graphical interpretation of $V_{i(\min )}$, which is the minimum $V_{i}$ needed to turn on $M_{11}$ in Fig. 5.38.
into (5.155) gives $K=-V_{S S}+V_{t 25}+V_{o v 25}$; therefore,

$$
\begin{equation*}
V_{g 11}=\left[V_{o}-\left(V_{i}-V_{O S}\right)\right] A_{1} A_{2}-V_{S S}+V_{t 25}+V_{o v 25} \tag{5.156}
\end{equation*}
$$

Also, (5.117) with $g_{m}=g_{m 1}=g_{m 2}$ gives $V_{o}$ in terms of $V_{i}$ for the output stage in Fig. 5.38 as long as the random offset is negligible, both $M_{1}$ and $M_{2}$ operate in the active region, and $M_{11}$ and $M_{12}$ are off. Since the gates of $M_{1}$ and $M_{2}$ are each driven by only one output of the corresponding $A_{1}$ amplifiers, $A=A_{1} / 2$. With these substitutions, (5.117) gives

$$
\begin{equation*}
V_{o}=\frac{V_{i}}{1+\frac{1}{A_{1} g_{m 1} R_{L}}} \tag{5.157}
\end{equation*}
$$

To turn $M_{11}$ on, $V_{g 11}<V_{D D}-\left|V_{t 11}\right|$. Substituting this condition and (5.157) into (5.156) gives

$$
\begin{equation*}
V_{i(\mathrm{~min})}=V_{O S}\left(1+A_{1} g_{m 1} R_{L}\right)-\frac{\left(V_{D D}+V_{S S}-\left|V_{t 11}\right|-V_{t 25}-V_{o v 25}\right)\left(1+A_{1} g_{m 1} R_{L}\right)}{A_{1} A_{2}} \tag{5.158}
\end{equation*}
$$

where $V_{i(\min )}$ is the minimum value of $V_{i}$ for which $M_{11}$ conducts nonzero drain current. To interpret this result, let $A_{2} \rightarrow \infty$. Then to turn $M_{11}$ on, the required differential input voltage of the top $A_{2}$ amplifier $V_{2 t}=0$. Therefore, the required differential input of the top $A_{1}$ amplifier is zero; that is,

$$
\begin{equation*}
V_{o}=V_{i}-V_{O S} \tag{5.159}
\end{equation*}
$$

This equation and (5.157) are both plotted in Fig. 5.41. As the input voltage increases, the output voltage follows with a slope less than unity if $R_{L}$ is finite, as shown by the solid plot. Therefore, as $V_{i}$ increases, $V_{i}-V_{o}$ also increases. To turn $M_{11}$ barely on, this difference must be equal to $V_{O S}$ so that the circuit operates at the intersection of the two lines in Fig. 5.41. Substituting (5.157) into (5.159) gives

$$
\begin{equation*}
V_{i(\min )}=V_{O S}\left(1+A_{1} g_{m 1} R_{L}\right) \tag{5.160}
\end{equation*}
$$

This equation agrees with the result that would be obtained by allowing $A_{2} \rightarrow \infty$ in (5.158). The term in parentheses in (5.160) is equal to the reciprocal of the difference in the slopes of the two lines in Fig. 5.41.

#### EXAMPLE

Find the minimum input voltage in Fig. 5.38 for which $M_{11}$ turns on, assuming at first that $A_{2} \rightarrow \infty$ and then that $A_{2}=70$. Let $V_{O S}=10 \mathrm{mV}, A_{1}=8, g_{m 1}=5 \mathrm{~mA} / \mathrm{V}, R_{L}=60 \Omega$, $V_{D D}=V_{S S}=2.5 \mathrm{~V}, V_{t 11}=-0.7 \mathrm{~V}, V_{t 25}=0.7 \mathrm{~V}$, and $V_{o v 25}=0.1 \mathrm{~V}$.

From (5.160),

$$
V_{i(\min )}=10 \mathrm{mV}[1+8(0.005)(60)]=34 \mathrm{mV}
$$

when $A_{2} \rightarrow \infty$. On the other hand, when $A_{2}=70,(5.158)$ shows that

$$
V_{i(\min )}=10 \mathrm{mV}[1+8(0.005)(60)]-\frac{3.5[1+8(0.005)(60)]}{8(70)} \simeq 0.13 \mathrm{mV}
$$

This example shows that the minimum input voltage required to turn on $M_{11}$ is reduced from the value given in (5.160) when $A_{2}$ is finite, because the fractional term in (5.158) is - positive.

The key point of this analysis is that $M_{11}$ and $M_{12}$ in Fig. 5.38 remain off for only a small range of input voltages. Therefore, the nonlinearity introduced by turning on $M_{11}$ or $M_{12}$ occurs when $\left|V_{i}\right|$ is small. As a result, this circuit is well suited for the ISDN (Integrated Service Digital Network) line-driving application for which it was designed because the required four-level output code does not include zero, avoiding distortion that would be introduced by turning $M_{11}$ and $M_{12}$ on or off ${ }^{17}$ if a zero-level output pulse were required.
