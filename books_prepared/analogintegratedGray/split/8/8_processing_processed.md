# 8. Feedback

Negative feedback is widely used in amplifier design because it produces several important benefits. One of the most significant is that negative feedback stabilizes the gain of the amplifier against parameter changes in the active devices due to supply voltage variation, temperature changes, or device aging. A second benefit is that negative feedback allows the designer to modify the input and output impedances of the circuit in any desired fashion. Another significant benefit of negative feedback is the reduction in signal waveform distortion that it produces, and for this reason almost all high-quality audio amplifiers employ negative feedback around the power output stage. Finally, negative feedback can produce an increase in the bandwidth of circuits and is widely used in broadband amplifiers.

However, the benefits of negative feedback listed above are accompanied by two disadvantages. First, the gain of the circuit is reduced in almost direct proportion to the other benefits achieved. Thus, it is often necessary to make up the decrease in gain by adding extra amplifier stages with a consequent increase in hardware cost. The second potential problem associated with the use of feedback is the tendency for oscillation to occur in the circuit, and careful attention by the designer is often required to overcome this problem.

In this chapter, the various benefits of negative feedback are considered, together with a systematic classification of feedback configurations. Two different methods for analyzing feedback circuits are presented. The problem of feedback-induced oscillation and its solution are considered in Chapter 9.

## 8.1 Ideal Feedback Equation

Consider the idealized feedback configuration of Fig. 8.1. In this figure $S_{i}$ and $S_{o}$ are input and output signals that may be voltages or currents. The feedback network (which is usually linear and passive) has a transfer function $f$ and feeds back a signal $S_{f b}$ to the input. At the input, signal $S_{f b}$ is subtracted from input signal $S_{i}$ at the input differencing node. Error signal $S_{\epsilon}$ is the difference between $S_{i}$ and $S_{f b}$, and $S_{\epsilon}$ is fed to the basic amplifier with transfer function a. Note that another common convention is to assume that $S_{i}$ and $S_{f b}$ are added together in an input summing node, and this leads to some sign changes in the analysis. It should be pointed out that negative-feedback amplifiers in practice have an input differencing node and thus the convention assumed here is more convenient for amplifier analysis.

From Fig. 8.1

$$
\begin{equation*}
S_{o}=a S_{\epsilon} \tag{8.1}
\end{equation*}
$$

assuming that the feedback network does not load the basic amplifier. Also

$$
\begin{align*}
S_{f b} & =f S_{o}  \tag{8.2}\\
S_{\epsilon} & =S_{i}-S_{f b} \tag{8.3}
\end{align*}
$$

image_name:Figure 8.1 Ideal feedback configuration
description:The system block diagram in Figure 8.1 represents an ideal feedback configuration for a negative-feedback amplifier system. The main components of this system include:

1. **Input Signal ($S_i$):** This is the initial signal that enters the system.

2. **Differencing Node:** The input signal $S_i$ is applied to a differencing node, which outputs the error signal $S_\epsilon$. This node subtracts the feedback signal $S_{fb}$ from the input signal $S_i$.

3. **Basic Amplifier:** The error signal $S_\epsilon$ is then fed into a basic amplifier with a gain of $a$. The amplifier outputs the signal $S_o$.

4. **Output Signal ($S_o$):** This is the final output of the amplifier system after amplification.

5. **Feedback Network:** The output signal $S_o$ is fed back into the system through a feedback network with a feedback factor of $f$. This network produces the feedback signal $S_{fb}$.

6. **Feedback Loop:** The feedback signal $S_{fb}$ is fed back to the differencing node to complete the loop, creating a negative feedback system.

### Flow of Information:
- The input signal $S_i$ enters the differencing node, where the feedback signal $S_{fb}$ is subtracted, resulting in the error signal $S_\epsilon$.
- The error signal is amplified by the basic amplifier, producing the output signal $S_o$.
- The output signal is then routed through the feedback network, generating the feedback signal $S_{fb}$.
- The feedback signal is looped back to the differencing node, influencing the next cycle of amplification.

Overall System Function:
The primary function of this system is to provide controlled amplification of the input signal while maintaining stability through negative feedback. The feedback reduces the overall gain of the system to $A = \frac{a}{1 + af}$, known as the closed-loop gain, which helps in stabilizing the amplifier and reducing distortion and noise.

Figure 8.1 Ideal feedback configuration.

Substituting (8.2) in (8.3) gives

$$
\begin{equation*}
S_{\epsilon}=S_{i}-f S_{o} \tag{8.4}
\end{equation*}
$$

Substituting (8.4) in (8.1) gives

$$
S_{o}=a S_{i}-a f S_{o}
$$

and thus

$$
\begin{equation*}
\frac{S_{o}}{S_{i}}=A=\frac{a}{1+a f} \tag{8.5}
\end{equation*}
$$

Equation 8.5 is the fundamental equation for negative feedback circuits where $A$ is the overall gain with feedback applied. ( $A$ is often called the closed-loop gain.)

It is useful to define a quantity $T$ called the loop gain such that

$$
\begin{equation*}
T=a f \tag{8.6}
\end{equation*}
$$

and

$$
\begin{equation*}
\frac{S_{o}}{S_{i}}=A=\frac{a}{1+T} \tag{8.7}
\end{equation*}
$$

$T$ is the total gain around the feedback loop. If $T \gg 1$, then, from (8.5), gain $A$ is given by

$$
\begin{equation*}
A \simeq \frac{1}{f} \tag{8.8}
\end{equation*}
$$

That is, for large values of loop gain $T$, the overall amplifier gain is determined by the feedback transfer function $f$. Since the feedback network is usually formed from stable, passive elements, the value of $f$ is well defined and so is the overall amplifier gain.

The feedback loop operates by forcing $S_{f b}$ to be nearly equal to $S_{i}$. This is achieved by amplifying the difference $S_{\epsilon}=S_{i}-S_{f b}$, and the feedback loop then effectively minimizes error signal $S_{\epsilon}$. This can be seen by substituting (8.5) in (8.4) to obtain

$$
S_{\epsilon}=S_{i}-f \frac{a S_{i}}{1+a f}
$$

and this leads to

$$
\begin{equation*}
\frac{S_{\epsilon}}{S_{i}}=\frac{1}{1+a f}=\frac{1}{1+T} \tag{8.9}
\end{equation*}
$$

As $T$ becomes much greater than $1, S_{\epsilon}$ becomes much less than $S_{i}$. In addition, substituting (8.5) in (8.2) gives

$$
S_{f b}=f S_{i} \frac{a}{1+a f}
$$

and thus

$$
\begin{equation*}
\frac{S_{f b}}{S_{i}}=\frac{T}{1+T} \tag{8.10}
\end{equation*}
$$

If $T \gg 1$, then $S_{f b}$ is approximately equal to $S_{i}$. That is, feedback signal $S_{f b}$ is a replica of the input signal. Since $S_{f b}$ and $S_{o}$ are directly related by (8.2), it follows that if $|f|<1$, then $S_{o}$ is an amplified replica of $S_{i}$. This is the aim of a feedback amplifier.

## 8.2 Gain Sensitivity

In most practical situations, gain $a$ of the basic amplifier is not well defined. It is dependent on temperature, active-device operating conditions, and transistor parameters. As mentioned previously, the negative-feedback loop reduces variations in overall amplifier gain due to variations in $a$. This effect may be examined by differentiating (8.5) to obtain

$$
\frac{d A}{d a}=\frac{(1+a f)-a f}{(1+a f)^{2}}
$$

and this reduces to

$$
\begin{equation*}
\frac{d A}{d a}=\frac{1}{(1+a f)^{2}} \tag{8.11}
\end{equation*}
$$

If $a$ changes by $\delta a$, then $A$ changes by $\delta A$ where

$$
\delta A=\frac{\delta a}{(1+a f)^{2}}
$$

The fractional change in $A$ is

$$
\frac{\delta A}{A}=\frac{1+a f}{a} \frac{\delta a}{(1+a f)^{2}}
$$

This can be expressed as

$$
\begin{equation*}
\frac{\delta A}{A}=\frac{\frac{\delta a}{a}}{1+a f}=\frac{\frac{\delta a}{a}}{1+T} \tag{8.12}
\end{equation*}
$$

Equation 8.12 shows that the fractional change in $A$ is reduced by $(1+T)$ compared to the fractional change in $a$. For example, if $T=100$ and $a$ changes by 10 percent due to temperature change, then the overall gain $A$ changes by only 0.1 percent using (8.12).

## 8.3 Effect of Negative Feedback on Distortion

The foregoing results show that even if the basic-amplifier gain $a$ changes, the negative feedback keeps overall gain $A$ approximately constant. This suggests that feedback should be effective in reducing distortion because distortion is caused by changes in the slope of the
image_name:Figure 8.2 Basic-amplifier transfer characteristic
description:The graph in Figure 8.2 is a piecewise linear plot representing the transfer characteristic of a basic amplifier. The x-axis is labeled as $S_\epsilon$, which likely represents the input signal. The y-axis is labeled as $S_0$, representing the output signal.

Axes and Units
- **X-axis ($S_\epsilon$):** This axis represents the input signal. It is marked with a linear scale.
- **Y-axis ($S_0$):** This axis represents the output signal, also on a linear scale.

Overall Behavior and Trends
The graph shows three distinct regions:
1. **Region 1:** For small values of $S_\epsilon$, the output remains constant at $a_3 = 0$, indicating no change in the output despite changes in the input.
2. **Region 2:** As $S_\epsilon$ increases beyond a certain point, the graph shows a linear increase with a slope of $a_1$. This region represents the active amplification zone where the output is directly proportional to the input.
3. **Region 3:** Beyond another threshold, the graph flattens again with $a_3 = 0$, showing saturation where further increases in $S_\epsilon$ do not affect $S_0$.

Key Features and Technical Details
- **Slopes:**
- The slope in the active region is $a_1$, indicating the gain of the amplifier in this linear region.
- The slope changes to $a_2$ at a certain point, suggesting a transition in the amplifier's behavior.
- **Saturation Points:**
- The output saturates at $S_{o1}$ and $S_{o2}$, where changes in input no longer affect the output.
- **Critical Points:**
- Transition points are marked where the slope changes, indicating shifts between linear and saturated behavior.

Annotations and Specific Data Points
- **Reference Lines:**
- Horizontal dashed lines indicate the saturation levels $S_{o1}$ and $S_{o2}$.
- Points are marked where the slope changes from $a_1$ to $a_2$, and where it flattens to $a_3 = 0$.

This graph illustrates the non-linear behavior of the amplifier, with clear regions of linear gain and saturation, which are critical for understanding how feedback can stabilize the overall gain despite changes in the basic amplifier gain.

Figure 8.2 Basic-amplifier transfer characteristic.
basic-amplifier transfer characteristic. The feedback should tend to reduce the effect of these slope changes since $A$ is relatively independent of $a$. This is explained next.

Suppose the basic amplifier has a transfer characteristic with a nonlinearity as shown in Fig. 8.2. It is assumed that two regions exist, each with constant but different slopes $a_{1}$ and $a_{2}$. When feedback is applied, the overall gain will still be given by (8.5) but the appropriate value of $a$ must be used, depending on which region of Fig. 8.2 is being traversed. Thus the overall transfer characteristic with feedback applied will also have two regions of different slope, as shown in Fig. 8.3. However, slopes $A_{1}$ and $A_{2}$ are almost equal because of the effect of the negative feedback. This can be seen by substituting in (8.5) to give

$$
\begin{align*}
& A_{1}=\frac{a_{1}}{1+a_{1} f} \simeq \frac{1}{f}  \tag{8.13}\\
& A_{2}=\frac{a_{2}}{1+a_{2} f} \simeq \frac{1}{f} \tag{8.14}
\end{align*}
$$

Thus the transfer characteristic of the feedback amplifier of Fig. 8.3 shows much less nonlinearity than the original basic-amplifier characteristics of Fig. 8.2.
image_name:Figure 8.3
description:The graph in Figure 8.3 represents the transfer characteristic of a feedback amplifier. It is a plot of the output signal \( S_o \) on the vertical axis against the input signal \( S_i \) on the horizontal axis.

1. **Type of Graph and Function:**
- This is a linear graph showing the relationship between input and output signals in a feedback amplifier system.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( S_i \), representing the input signal.
- The vertical axis is labeled \( S_o \), representing the output signal.
- The scales for both axes are linear.

3. **Overall Behavior and Trends:**
- The graph consists of three distinct linear regions.
- In the central region, the graph has a positive slope labeled \( A_1 \), indicating a proportional relationship between \( S_i \) and \( S_o \).
- The slope \( A_1 \) is approximately equal to \( \frac{1}{f} \) due to negative feedback, as described by equations (8.13) and (8.14).
- On either side of the central region, the graph levels off, with slopes labeled \( A_3 = 0 \), indicating saturation where the output remains constant despite changes in the input.

4. **Key Features and Technical Details:**
- The central linear region has a slope \( A_1 \) and an intersecting point marked as \( S_{o1} \) and \( \frac{S_{o1}}{a_1(1 + a_1f)} \).
- The outer regions, where the slope is zero, are marked by constant values \( S_{o2} \) and \(-S_{o2} \) on the vertical axis, indicating the saturation limits of the amplifier.
- These horizontal sections reflect the reduced gain and nonlinearity due to negative feedback.

5. **Annotations and Specific Data Points:**
- Annotations include the slope \( A_1 \) and the saturation levels \( A_3 = 0 \).
- The graph shows dashed lines indicating the transition points and saturation levels, enhancing the understanding of how feedback affects the amplifier's linearity and gain.

Overall, the graph illustrates how negative feedback flattens the transfer characteristic, reducing gain but enhancing linearity by compressing the scale of the input-output relationship.

Figure 8.3 Feedback-amplifier transfer characteristic corresponding to the basic-amplifier characteristic of Fig. 8.2.

Note that the horizontal scale in Fig. 8.3 has been compressed as compared to Fig. 8.2 in order to allow easy comparison of the two graphs. This scale change is necessary because the negative feedback reduces the gain. The reduction in gain by the factor $(1+T)$, which accompanies the use of negative feedback, presents few serious problems, since the gain can easily be made up by placing a preamplifier in front of the feedback amplifier. Since the preamplifier handles much smaller signals than does the output amplifier, distortion is usually not a problem in that amplifier.

One further point that should be made about Figs. 8.2 and 8.3 is that both show hard saturation of the output amplifier (i.e., the output becomes independent of the input) at an output signal level of $S_{o 2}$. Since the incremental slope $a_{3}=0$ in that region, negative feedback cannot improve the situation as $A_{3}=0$ also, using (8.5).

## 8.4 Feedback Configurations

The treatment in the previous sections was based on the idealized configuration shown in Fig. 8.1. Practical feedback amplifiers are composed of circuits that have current or voltage signals as inputs and produce output currents or voltages. In order to pursue feedback amplifier design at a practical level, it is necessary to specify the details of the feedback sampling process and the circuits used to realize this operation. There are four basic feedback amplifier connections. These are specified according to whether the output signal $S_{o}$ is a current or a voltage and whether the feedback signal $S_{f b}$ is a current or a voltage. It is apparent that four combinations exist and these are now considered.

### 8.4.1 Series-Shunt Feedback

Suppose it is required to design a feedback amplifier that stabilizes a voltage transfer function. That is, a given input voltage should produce a well-defined proportional output voltage. This will require sampling the output voltage and feeding back a proportional voltage for comparison with the incoming voltage. This situation is shown schematically in Fig. 8.4. The basic amplifier has gain $a$, and the feedback network is a two-port with transfer function $f$ that shunts the output of the basic amplifier to sample $v_{0}$. Ideally, the impedance $z_{22 f}=\infty$, and the feedback network does not load the basic amplifier. The feedback voltage $v_{f b}$ is connected in series with the input to allow comparison with $v_{i}$ and, ideally, $z_{11 f}=0$. The signal $v_{\epsilon}$ is the difference between $v_{i}$ and $v_{f b}$ and is fed to the basic amplifier. The basic amplifier and feedback circuits are assumed unilateral in that the basic amplifier transmits only from $v_{\epsilon}$ to $v_{o}$ and the feedback network transmits only from $v_{o}$ to $v_{f b}$. This point will be taken up later.

This feedback is called series-shunt feedback because the feedback network is connected in series with the input and shunts the output.
image_name:Figure 8.4 Series-shunt feedback configuration
description:The diagram titled "Figure 8.4 Series-shunt feedback configuration" illustrates a feedback amplifier system composed of two primary components: a basic amplifier and a feedback network.

1. **Main Components:**
- **Basic Amplifier:** This block is labeled with the gain 'a' and is responsible for amplifying the input signal. The amplifier takes the input voltage difference, \( v_{\epsilon} \), and outputs an amplified signal, \( v_{o} \).
- **Feedback Network:** This block is labeled with the feedback factor 'f'. It receives the output voltage \( v_{o} \) from the basic amplifier and produces a feedback voltage \( v_{fb} \) that is fed back to the input.

2. **Flow of Information or Control:**
- The input voltage \( v_{i} \) is fed into the system where it is compared with the feedback voltage \( v_{fb} \) to produce the error signal \( v_{\epsilon} \) (\( v_{\epsilon} = v_{i} - v_{fb} \)).
- The error signal \( v_{\epsilon} \) is input to the basic amplifier, which outputs the amplified voltage \( v_{o} = a \cdot v_{\epsilon} \).
- The output voltage \( v_{o} \) is then fed into the feedback network, which scales it by the feedback factor 'f' to produce the feedback voltage \( v_{fb} = f \cdot v_{o} \).
- The feedback network is connected in a series-shunt configuration, meaning it is in series with the input and shunts the output.

3. **Labels, Annotations, and Key Indicators:**
- The diagram specifies that \( z_{11f} = 0 \), indicating zero input impedance of the feedback network, and \( z_{22f} = \infty \), indicating infinite output impedance of the feedback network.
- The polarities of the voltages \( v_{i}, v_{\epsilon}, v_{o}, \) and \( v_{fb} \) are clearly marked to show the direction of signal flow and feedback.

4. **Overall System Function:**
- The primary function of this configuration is to stabilize and control the gain of the amplifier by using feedback. The series-shunt feedback configuration improves the input and output impedance characteristics and stabilizes the gain despite variations in the amplifier's characteristics. The feedback loop helps in reducing distortion and increasing bandwidth, making the amplifier more robust and reliable.

Figure 8.4 Series-shunt feedback configuration.
image_name:Figure 8.5 Series-shunt configuration fed from a finite source impedance.
description:The circuit is a series-shunt feedback configuration where the output voltage 'vo' is fed back to the input 'vi' through a feedback network 'f'. The amplifier 'a' stabilizes the gain and improves the impedance characteristics.

Figure 8.5 Series-shunt configuration fed from a finite source impedance.

From Fig. 8.4

$$
\begin{align*}
v_{o} & =a v_{\epsilon}  \tag{8.15}\\
v_{f b} & =f v_{o}  \tag{8.16}\\
v_{\epsilon} & =v_{i}-v_{f b} \tag{8.17}
\end{align*}
$$

From (8.15), (8.16), and (8.17),

$$
\begin{equation*}
\frac{v_{o}}{v_{i}}=\frac{a}{1+a f} \tag{8.18}
\end{equation*}
$$

Thus the ideal feedback equation applies. Equation 8.18 indicates that the transfer function that is stabilized is $v_{o} / v_{i}$, as desired. If the circuit is fed from a high source impedance as shown in Fig. 8.5, the ratio $v_{o} / v_{i}$ is still stabilized [and given by (8.18)], but now $v_{i}$ is given by

$$
\begin{equation*}
v_{i}=\frac{Z_{i}}{Z_{i}+z_{s}} v_{s} \tag{8.19}
\end{equation*}
$$

where $Z_{i}$ is the input impedance seen by $v_{i}$. If $z_{s} \approx Z_{i}$, then $v_{i}$ depends on $Z_{i}$, which is not usually well defined since it often depends on active-device parameters. Thus the overall gain $v_{o} / v_{s}$ will not be stabilized. Consequently, the full benefits of gain stabilization are achieved for a series-shunt feedback amplifier when the source impedance is low compared to the input impedance of the closed-loop amplifier. The ideal driving source is a voltage source.

Consider now the effect of series-shunt feedback on the terminal impedances of the amplifier. Assume the basic amplifier has input and output impedances $z_{i}$ and $z_{o}$ as shown in Fig. 8.6. Again assume the feedback network is ideal and feeds back a voltage $f v_{o}$ as shown. Both networks are unilateral. The applied voltage $v_{i}$ produces input current $i_{i}$ and output voltage $v_{o}$. From Fig. 8.6

$$
\begin{align*}
v_{o} & =a v_{\epsilon}  \tag{8.20}\\
v_{i} & =v_{\epsilon}+f v_{o} \tag{8.21}
\end{align*}
$$

image_name:Figure 8.6
description:This circuit represents a series-shunt feedback amplifier configuration. The basic amplifier has input impedance 'zi' and output impedance 'zo'. The feedback network provides a voltage 'fvo' from the output 'vo' to the input 've'.
Figure 8.6 Series-shunt configuration with finite impedances in the basic amplifier.

Substituting (8.20) in (8.21) gives

$$
\begin{equation*}
v_{i}=v_{\epsilon}+a f v_{\epsilon}=v_{\epsilon}(1+a f) \tag{8.22}
\end{equation*}
$$

Also

$$
\begin{equation*}
i_{i}=\frac{v_{\epsilon}}{z_{i}} \tag{8.23}
\end{equation*}
$$

Substituting (8.22) in (8.23) gives

$$
\begin{equation*}
i_{i}=\frac{v_{i}}{z_{i}} \frac{1}{1+a f} \tag{8.24}
\end{equation*}
$$

Thus, from (8.24), input impedance $Z_{i}$ with feedback applied is

$$
\begin{equation*}
Z_{i}=\frac{v_{i}}{i_{i}}=(1+T) z_{i} \tag{8.25}
\end{equation*}
$$

Series feedback at the input always raises the input impedance by $(1+T)$.
The effect of series-shunt feedback on the output impedance can be calculated using the circuit of Fig. 8.7. The input voltage is removed (the input is shorted) and a voltage $v$ applied at the output. From Fig. 8.7

$$
\begin{align*}
& v_{\epsilon}+f v=0  \tag{8.26}\\
& i=\frac{v-a v_{\epsilon}}{z_{o}} \tag{8.27}
\end{align*}
$$

Substituting (8.26) in (8.27) gives

$$
\begin{equation*}
i=\frac{v+a f v}{z_{o}} \tag{8.28}
\end{equation*}
$$

From (8.28) output impedance $Z_{o}$ with feedback applied is

$$
\begin{equation*}
Z_{o}=\frac{v}{i}=\frac{z_{o}}{1+T} \tag{8.29}
\end{equation*}
$$

Shunt feedback at the output always lowers the output impedance by $(1+T)$. This makes the output a better voltage source so that series-shunt feedback produces a good voltage amplifier. It stabilizes $v_{o} / v_{i}$, raises $Z_{i}$, and lowers $Z_{o}$.

The original series-shunt feedback amplifier of Fig. 8.6 can now be represented as shown in Fig. 8.8a using (8.18), (8.25), and (8.29). As the forward gain $a$ approaches infinity, the equivalent circuit approaches that of Fig. $8.8 b$, which is an ideal voltage amplifier.
image_name:Figure 8.7
description:The circuit is a series-shunt feedback configuration used to calculate output impedance. It includes a feedback voltage source 'fv' and two main voltage sources 'vε' and 'avε' with resistors 'zi' and 'zo'.
Figure 8.7 Circuit for the calculation of the output impedance of the series-shunt feedback configuration.

image_name:(a)
description:
[
name: zi(1+T), type: Resistor, value: zi(1+T), ports: {N1: vi+, N2: vi-}
name: zo/(1+T), type: Resistor, value: zo/(1+T), ports: {N1: vo+, N2: X}
name: a/(1+T)vi, type: VoltageSource, value: a/(1+T)vi, ports: {Np: X+, Nn: vo-}
]
extrainfo:The circuit is a series-shunt feedback configuration used to calculate output impedance. It includes a feedback voltage source 'fv' and two main voltage sources 'vε' and 'avε' with resistors 'zi' and 'zo'.
image_name:(b)
description:
[
name: vi/f, type: VoltageControlledVoltageSource, ports: {Np: vo+, Nn: vo-, InP: vi+, InN: vi-}
]
extrainfo:The circuit represents a series-shunt feedback amplifier configuration. It includes a voltage-controlled voltage source 'vi/f' which connects the input voltage 'vi' to the output voltage 'vo'.

Figure 8.8 (a) Equivalent circuit of a series-shunt feedback amplifier. (b) Equivalent circuit of a series-shunt feedback amplifier for $a \rightarrow \infty$.

### 8.4.2 Shunt-Shunt Feedback

This configuration is shown in Fig. 8.9. The feedback network again shunts the output of the basic amplifier and samples $v_{o}$ and, ideally, $z_{22 f}=\infty$ as before. However, the feedback network now shunts the input of the main amplifier as well and feeds back a proportional current $f v_{o}$. Ideally, $z_{11 f}=\infty$ so that the feedback network does not produce any shunt loading on the amplifier input. Since the feedback signal is a current, it is more convenient to deal with an error current $i_{\epsilon}$ at the input. The input signal in this case is ideally a current $i_{i}$ and this is assumed. From Fig. 8.9

$$
\begin{equation*}
a=\frac{v_{o}}{i_{\epsilon}} \tag{8.30}
\end{equation*}
$$

where $a$ is a transresistance,

$$
\begin{equation*}
f=\frac{i_{f b}}{v_{o}} \tag{8.31}
\end{equation*}
$$

where $f$ is a transconductance, and

$$
\begin{align*}
v_{o} & =a i_{\epsilon}  \tag{8.32}\\
i_{\epsilon} & =i_{i}-i_{f b} \tag{8.33}
\end{align*}
$$

Substitution of $i_{f b}$ from (8.31) in (8.33) gives

$$
\begin{equation*}
i_{\epsilon}=i_{i}-f v_{o} \tag{8.34}
\end{equation*}
$$

image_name:Figure 8.9
description:The circuit represents a shunt-shunt feedback configuration with a basic amplifier and feedback network. The transresistance and transconductance are represented by equations involving these elements.
Figure 8.9 Shunt-shunt feedback configuration.

Substitution of (8.32) in (8.34) gives

$$
\frac{v_{o}}{a}=i_{i}-f v_{o}
$$

Rearranging terms we find

$$
\begin{equation*}
\frac{v_{o}}{i_{i}}=\frac{a}{1+a f}=A \tag{8.35}
\end{equation*}
$$

Again the ideal feedback equation applies. Note that although $a$ and $f$ have dimensions of resistance and conductance, the loop gain $T=a f$ is dimensionless. This is always true.

In this configuration, if the source impedance $z_{s}$ is finite, a division of input current $i_{i}$ occurs between $z_{s}$ and the amplifier input, and the ratio $v_{o} / i_{i}$ will not be as well defined as (8.35) suggests. The full benefits of negative feedback for a shunt-shunt feedback amplifier are thus obtained for $z_{s} \gg Z_{i}$, which approaches a current-source drive.

The input impedance of the circuit of Fig. 8.9 can be calculated using (8.32) and (8.35) to give

$$
\begin{equation*}
i_{\epsilon}=\frac{i_{i}}{1+a f} \tag{8.36}
\end{equation*}
$$

The input impedance $Z_{i}$ with feedback is

$$
\begin{equation*}
Z_{i}=\frac{v_{i}}{i_{i}} \tag{8.37}
\end{equation*}
$$

Substituting (8.36) in (8.37) gives

$$
\begin{equation*}
Z_{i}=\frac{v_{i}}{i_{\epsilon}} \frac{1}{1+a f}=\frac{z_{i}}{1+T} \tag{8.38}
\end{equation*}
$$

Thus shunt feedback at the input reduces the amplifier input impedance by $(1+T)$. This is always true.

It is easily shown that the output impedance in this case is

$$
\begin{equation*}
Z_{o}=\frac{z_{o}}{1+T} \tag{8.39}
\end{equation*}
$$

as before, for shunt feedback at the output.
Shunt-shunt feedback has made this amplifier a good transresistance amplifier. The transfer function $v_{o} / i_{i}$ has been stabilized and both $Z_{i}$ and $Z_{o}$ are lowered.

The original shunt-shunt feedback amplifier of Fig. 8.9 can now be represented as shown in Fig. 8.10a using (8.35), (8.38), and (8.39). As forward gain $a$ approaches infinity, the equivalent circuit approaches that of Fig. 8.10 b , which is an ideal transresistance amplifier.

### 8.4.3 Shunt-Series Feedback

The shunt-series configuration is shown in Fig. 8.11. The feedback network samples $i_{o}$ and feeds back a proportional current $i_{f b}=f i_{o}$. Since the desired output signal is a current $i_{o}$, it is more convenient to represent the output of the basic amplifier with a Norton equivalent. In this case both $a$ and $f$ are dimensionless current ratios, and the ideal input source is a current
image_name:(a)
description::The circuit diagram (a) represents an equivalent circuit of a shunt-shunt feedback amplifier. It includes resistors and controlled sources to model feedback and input/output interactions. The feedback network samples the output current and provides a proportional feedback current.
image_name:(b)
description:The diagram shows an equivalent circuit of a shunt-shunt feedback amplifier for a → ∞. It includes a current-controlled current source and a resistor in parallel. The input current is ii, and the output voltage is vo.

image_name:Figure 8.11
description:
[
name: z_i/(1+T), type: Resistor, value: z_i/(1+T), ports: {N1: i_i, N2: a/(1+T)}
name: z_o/(1+T), type: Resistor, value: z_o/(1+T), ports: {N1: a/(1+T), N2: v_o}
name: a/(1+T), type: VoltageControlledVoltageSource, value: a/(1+T), ports: {Np: z_i/(1+T), Nn: z_o/(1+T)}
name: i_i/f, type: VoltageControlledVoltageSource, value: i_i/f, ports: {Np: i_i, Nn: v_o}
name: i_i, type: CurrentSource, value: i_i, ports: {Np: input, Nn: z_i/(1+T)}
name: z_i, type: Resistor, value: z_i, ports: {N1: i_i, N2: a_i_e}
name: a_i_e, type: VoltageControlledVoltageSource, value: a_i_e, ports: {Np: z_i, Nn: z_o}
name: z_o, type: Resistor, value: z_o, ports: {N1: a_i_e, N2: output}
name: f_i_o, type: CurrentSource, value: f_i_o, ports: {Np: a_i_e, Nn: z_o}
]
extrainfo:The circuit diagram in Figure 8.11 represents a shunt-series feedback amplifier configuration. It features a combination of basic amplifier and feedback network components. The feedback network samples the output current and feeds back a proportional current to the input, stabilizing the current gain and adjusting input and output impedances.
Figure 8.11 Shunt-series feedback configuration.
source $i_{i}$. It can be shown that

$$
\begin{align*}
\frac{i_{o}}{i_{i}} & =\frac{a}{1+a f}  \tag{8.40}\\
Z_{i} & =\frac{z_{i}}{1+T}  \tag{8.41}\\
Z_{o} & =z_{o}(1+T) \tag{8.42}
\end{align*}
$$

This amplifier is a good current amplifier and has stable current gain $i_{o} / i_{i}$, low $Z_{i}$, and high $Z_{o}$.

### 8.4.4 Series-Series Feedback

The series-series configuration is shown in Fig. 8.12. The feedback network samples $i_{o}$ and feeds back a proportional voltage $v_{f b}$ in series with the input. The forward gain $a$ is a transconductance and $f$ is a transresistance, and the ideal driving source is a voltage source $v_{i}$. It can
image_name:Figure 8.12 Series-series feedback configuration
description:The circuit is a series-series feedback configuration, which samples the output current and feeds back a proportional voltage in series with the input. It is designed as a transconductance amplifier with stabilized gain.

Figure 8.12 Series-series feedback configuration.
be shown that

$$
\begin{align*}
\frac{i_{o}}{v_{i}} & =\frac{a}{1+a f}  \tag{8.43}\\
Z_{i} & =z_{i}(1+T)  \tag{8.44}\\
Z_{o} & =z_{o}(1+T) \tag{8.45}
\end{align*}
$$

This amplifier is a good transconductance amplifier and has a stabilized gain $i_{o} / v_{i}$, as well as high $Z_{i}$ and $Z_{o}$.

## 8.5 Practical Configurations and the Effect of Loading

In practical feedback amplifiers, the feedback network causes loading at the input and output of the basic amplifier, and the division into basic amplifier and feedback network is not as obvious as the above treatment implies. In such cases, the circuit can always be analyzed by writing circuit equations for the whole amplifier and solving for the transfer function and terminal impedances. However, this procedure becomes very tedious and difficult in most practical cases, and the equations so complex that one loses sight of the important aspects of circuit performance. Thus it is profitable to identify a basic amplifier and feedback network in such cases and then to use the ideal feedback equations derived above. In general it will be necessary to include the loading effect of the feedback network on the basic amplifier, and methods of including this loading in the calculations are now considered. The method will be developed through the use of two-port representations of the circuits involved, although this method of representation is not necessary for practical calculations, as we will see.

### 8.5.1 Shunt-Shunt Feedback

Consider the shunt-shunt feedback amplifier of Fig. 8.9. The effect of nonideal networks may be included as shown in Fig. 8.13a, where finite input and output admittances are assumed in both forward and feedback paths, as well as reverse transmission in each. Finite source and load admittances $y_{S}$ and $y_{L}$ are assumed. The most convenient two-port representation in this case is the short-circuit admittance parameters or $y$ parameters, ${ }^{1}$ as used in Fig. 8.13a. The reason for this is that the basic amplifier and the feedback network are connected in parallel at input and output, and thus have identical voltages at their terminals. The $y$ parameters specify the response of a network by expressing the terminal currents in terms of the terminal voltages, and
image_name:(a)
description:The circuit represents a shunt-shunt feedback configuration using y-parameters. It consists of a basic amplifier and a feedback network connected in parallel, sharing identical terminal voltages. The circuit is designed to simplify calculations by expressing terminal currents in terms of terminal voltages.
image_name:(b)
description:The circuit diagram (b) represents a shunt-shunt feedback configuration using y-parameters. It shows a new basic amplifier and feedback network configuration with parallel connections at the input and output terminals.
Figure 8.13 (a) Shunt-shunt feedback configuration using the $y$-parameter representation. (b) Circuit of (a) redrawn with generators $y_{21 f} v_{i}$ and $y_{12 a} v_{o}$ omitted.
this results in very simple calculations when two networks have identical terminal voltages. This will be evident in the circuit calculations to follow. The $y$-parameter representation is illustrated in Fig. 8.14.

From Fig. 8.13a, at the input

$$
\begin{equation*}
i_{s}=\left(y_{S}+y_{11 a}+y_{11 f}\right) v_{i}+\left(y_{12 a}+y_{12 f}\right) v_{o} \tag{8.46}
\end{equation*}
$$

image_name:Figure 8.14
description:The diagram labeled "Figure 8.14" represents a two-port network using the y-parameter (admittance) model. It consists of a rectangular block symbolizing the two-port network with four terminals. The key components and their functions are as follows:

1. **Main Components:**
- The block represents the two-port network characterized by the admittance parameters (y-parameters).
- There are two input terminals on the left side, labeled with voltage \( v_1 \) and current \( i_1 \).
- There are two output terminals on the right side, labeled with voltage \( v_2 \) and current \( i_2 \).

2. **Flow of Information or Control:**
- The input current \( i_1 \) flows into the network at the left side, and the output current \( i_2 \) flows out of the network at the right side.
- The voltages \( v_1 \) and \( v_2 \) are applied across the input and output terminals, respectively.
- The direction of the current flow is indicated by arrows, with \( i_1 \) entering the network and \( i_2 \) exiting.

3. **Labels, Annotations, and Key Indicators:**
- The terminals are clearly labeled with their respective voltages and currents, \( v_1, i_1 \) for the input and \( v_2, i_2 \) for the output.
- The positive and negative signs next to the voltage labels indicate the polarity of the voltages across the terminals.

4. **Overall System Function:**
- The primary function of this two-port network is to relate the input and output voltages and currents through the y-parameters. The y-parameters define how the input current \( i_1 \) and output current \( i_2 \) depend on the input voltage \( v_1 \) and output voltage \( v_2 \). This representation is useful for analyzing and designing circuits involving interconnected networks by simplifying complex interactions into linear equations.

$$
\begin{array}{ll}
i_{1}=y_{11} v_{1}+y_{12} v_{2} & \\
i_{2}=y_{21} v_{1}+y_{22} v_{2} & \\
y_{11}=\left.\frac{i_{1}}{v_{1}}\right|_{v_{2}=0} & y_{12}=\left.\frac{i_{1}}{v_{2}}\right|_{v_{1}=0} \\
y_{21}=\left.\frac{i_{2}}{v_{1}}\right|_{v_{2}=0} & y_{22}=\left.\frac{i_{2}}{v_{2}}\right|_{v_{1}=0}
\end{array}
$$

Figure 8.14 The $y$-parameter representation of a two-port.

Summation of currents at the output gives

$$
\begin{equation*}
0=\left(y_{21 a}+y_{21 f}\right) v_{i}+\left(y_{L}+y_{22 a}+y_{22 f}\right) v_{o} \tag{8.47}
\end{equation*}
$$

It is useful to define

$$
\begin{gather*}
y_{i}=y_{S}+y_{11 a}+y_{11 f}  \tag{8.48}\\
y_{o}=y_{L}+y_{22 a}+y_{22 f} \tag{8.49}
\end{gather*}
$$

Solving (8.46) and (8.47) by using (8.48) and (8.49) gives

$$
\begin{equation*}
\frac{v_{o}}{i_{s}}=\frac{-\left(y_{21 a}+y_{21 f}\right)}{y_{i} y_{o}-\left(y_{21 a}+y_{21 f}\right)\left(y_{12 a}+y_{12 f}\right)} \tag{8.50}
\end{equation*}
$$

The equation can be put in the form of the ideal feedback equation of (8.35) by dividing by $y_{i} y_{o}$ to give

$$
\begin{equation*}
\frac{v_{o}}{i_{s}}=\frac{\frac{-\left(y_{21 a}+y_{21 f}\right)}{y_{i} y_{o}}}{1+\frac{-\left(y_{21 a}+y_{21 f}\right)}{y_{i} y_{o}}\left(y_{12 a}+y_{12 f}\right)} \tag{8.51}
\end{equation*}
$$

Comparing (8.51) with (8.35) gives

$$
\begin{align*}
& a=-\frac{y_{21 a}+y_{21 f}}{y_{i} y_{o}}  \tag{8.52}\\
& f=y_{12 a}+y_{12 f} \tag{8.53}
\end{align*}
$$

At this point, a number of approximations can be made that greatly simplify the calculations. First, we assume that the signal transmitted by the basic amplifier is much greater than the signal fed forward by the feedback network. Since the former has gain (usually large) while the latter has loss, this is almost invariably a valid assumption. This means that

$$
\begin{equation*}
\left|y_{21 a}\right| \gg\left|y_{21 f}\right| \tag{8.54}
\end{equation*}
$$

Second, we assume that the signal fed back by the feedback network is much greater than the signal fed back through the basic amplifier. Since most active devices have very small reverse transmission, the basic amplifier has a similar characteristic, and this assumption is almost invariably quite accurate. This assumption means that

$$
\begin{equation*}
\left|y_{12 a}\right| \ll\left|y_{12 f}\right| \tag{8.55}
\end{equation*}
$$

Using (8.54) and (8.55) in (8.51) gives

$$
\begin{equation*}
\frac{v_{o}}{i_{s}}=A \simeq \frac{\frac{-y_{21 a}}{y_{i} y_{o}}}{1+\left(\frac{-y_{21 a}}{y_{i} y_{o}}\right) y_{12 f}} \tag{8.56}
\end{equation*}
$$

Comparing (8.56) with (8.35) gives

$$
\begin{align*}
a & =-\frac{y_{21 a}}{y_{i} y_{o}}  \tag{8.57}\\
f & =y_{12 f} \tag{8.58}
\end{align*}
$$

A circuit representation of (8.57) and (8.58) can be found as follows. Equations 8.54 and 8.55 mean that in Fig. 8.13a the feedback generator of the basic amplifier and the forwardtransmission generator of the feedback network may be neglected. If this is done the circuit may be redrawn as in Fig. 8.13b, where the terminal admittances $y_{11 f}$ and $y_{22 f}$ of the feedback network have been absorbed into the basic amplifier, together with source and load impedances $y_{S}$ and $y_{L}$. The new basic amplifier thus includes the loading effect of the original feedback network, and the new feedback network is an ideal one as used in Fig. 8.9. If the transfer function of the basic amplifier of Fig. 8.13 b is calculated (by first removing the feedback network), the result given in (8.57) is obtained. Similarly, the transfer function of the feedback network of Fig. 8.13 b is given by (8.58). Thus Fig. 8.13 b is a circuit representation of (8.57) and (8.58).

Since Fig. $8.13 b$ has a direct correspondence with Fig. 8.9, all the results derived in Section 8.4.2 for Fig. 8.9 can now be used. The loading effect of the feedback network on the basic amplifier is now included by simply shunting input and output with $y_{11 f}$ and $y_{22 f}$, respectively. As shown in Fig. 8.14, these terminal admittances of the feedback network are calculated with the other port of the network short-circuited. In practice, loading term $y_{11 f}$ is simply obtained by shorting the output node of the amplifier and calculating the feedback circuit input admittance. Similarly, term $y_{22 f}$ is calculated by shorting the input node in the amplifier and calculating the feedback circuit output admittance. The feedback transfer function $f$ given by (8.58) is the short-circuit reverse transfer admittance of the feedback network and is defined in Fig. 8.14. This is readily calculated in practice and is often obtained by inspection. Note that the use of $y$ parameters in further calculations is not necessary. Once the circuit of Fig. $8.13 b$ is established, any convenient network analysis method may be used to calculate gain $a$ of the basic amplifier. We have simply used the two-port representation as a general means of illustrating how loading effects may be included in the calculations.

For example, consider the common shunt-shunt feedback circuit using an op amp as shown in Fig. 8.15a. The equivalent circuit is shown in Fig. $8.15 b$ and is redrawn in $8.15 c$ to allow for loading of the feedback network on the basic amplifier. The $y$ parameters of the feedback network can be found from Fig. 8.15d.

$$
\begin{align*}
& y_{11 f}=\left.\frac{i_{1}}{v_{1}}\right|_{v_{2}=0}=\frac{1}{R_{F}}  \tag{8.59}\\
& y_{22 f}=\left.\frac{i_{2}}{v_{2}}\right|_{v_{1}=0}=\frac{1}{R_{F}}  \tag{8.60}\\
& y_{12 f}=\left.\frac{i_{1}}{v_{2}}\right|_{v_{1}=0}=-\frac{1}{R_{F}}=f \tag{8.61}
\end{align*}
$$

Using (8.54), we neglect $y_{21 f}$.
The basic-amplifier gain $a$ can be calculated from Fig. 8.15 c by putting $i_{f b}=0$ to give

$$
\begin{align*}
v_{1} & =\frac{z_{i} R_{F}}{z_{i}+R_{F}} i_{i}  \tag{8.62}\\
v_{o} & =-\frac{R}{R+z_{o}} a_{\nu} v_{1} \tag{8.63}
\end{align*}
$$

where

$$
\begin{equation*}
R=R_{F} \| R_{L} \tag{8.64}
\end{equation*}
$$

image_name:(a)
description:
[
name: RF, type: Resistor, value: RF, ports: {N1: In(A0), N2: vo}
name: A0, type: OpAmp, value: A0, ports: {InP: GND, InN: In(A0), OutP: vo, OutN: GND}
name: ii, type: CurrentSource, value: ii, ports: {Np: In(A0), Nn: GND}
]
extrainfo:The circuit diagram (a) represents a shunt-shunt feedback amplifier using an operational amplifier as the gain element. The feedback network is implemented using a resistor RF. The input current source ii is connected to the inverting input of the op-amp, and the output voltage vo is fed back to the input through RF. The circuit is grounded at multiple points, and the output is taken across the load resistor RL.
image_name:(b)
description:
[
name: RF, type: Resistor, value: RF, ports: {N1: v1, N2: v0}
name: RL, type: Resistor, value: RL, ports: {N1: vo, N2: GND}
name: zi, type: Resistor, value: zi, ports: {N1: v1, N2: GND}
name: zo, type: Resistor, value: zo, ports: {N1: v2, N2: vo}
name: ii, type: CurrentSource, value: ii, ports: {Np: v1, Nn: GND}
name: -av_v1, type: VoltageControlledVoltageSource, value: -av_v1, ports: {Np: v2, Nn: GND}
]
extrainfo:The circuit is a shunt-shunt feedback amplifier with an op-amp as the gain element. It includes a feedback network with RF and load resistance RL. The basic amplifier gain is influenced by zi and zo resistances, and the feedback is provided through a voltage-controlled voltage source.
image_name:(c)
description:The circuit is a shunt-shunt feedback amplifier using an op-amp. It consists of a feedback network and a basic amplifier. The feedback network is composed of RF and a current source ijb, and the basic amplifier includes zi, zo, and RL. The input current source ii drives the circuit.
image_name:(d)
description:
[
name: RF, type: Resistor, value: RF, ports: {N1: v1, N2: v2}
name: v1, type: VoltageSource, value: v1, ports: {Np: v1, Nn: GND}
name: v2, type: VoltageSource, value: v2, ports: {Np: v2, Nn: GND}
]
extrainfo:The circuit diagram (d) represents a simple feedback network with two voltage sources, v1 and v2, connected through a resistor RF. The current i1 flows from v1 towards v2, and i2 flows from v2 towards v1, indicating the feedback mechanism.
Figure 8.15 (a) Shunt-shunt feedback circuit using an op amp as the gain element. (b) Equivalent circuit of (a) including load resistance $R_{L}$. (c) Division of the circuit in (b) into forward and feedback paths. (d) Circuit for the calculation of the $y$ parameters of the feedback network of the circuit in (b).

Substituting (8.62) in (8.63) gives

$$
\begin{equation*}
\frac{v_{o}}{i_{i}}=a=-\frac{R}{R+z_{o}} a_{v} \frac{z_{i} R_{F}}{z_{i}+R_{F}} \tag{8.65}
\end{equation*}
$$

Using the formulas derived in Section 8.4.2 we can now calculate all parameters of the feedback circuit. The input and output impedances of the basic amplifier now include the effect of feedback loading, and it is these impedances that are divided by $(1+T)$ as described in Section 8.4.2. Thus the input impedance of the basic amplifier of Fig. 8.15c is

$$
\begin{equation*}
z_{i a}=R_{F} \| z_{i}=\frac{R_{F} z_{i}}{R_{F}+z_{i}} \tag{8.66}
\end{equation*}
$$

When feedback is applied, the input impedance is

$$
\begin{equation*}
Z_{i}=\frac{z_{i a}}{1+T} \tag{8.67}
\end{equation*}
$$

Similarly for the output impedance of the basic amplifier

$$
\begin{equation*}
z_{o a}=z_{o}\left\|R_{F}\right\| R_{L} \tag{8.68}
\end{equation*}
$$

When feedback is applied, this becomes

$$
\begin{equation*}
Z_{o}=\frac{z_{o}\left\|R_{F}\right\| R_{L}}{1+T} \tag{8.69}
\end{equation*}
$$

Note that these calculations can be made using the circuit of Fig. 8.15c without further need of two-port $y$ parameters.

Since the loop gain $T$ is of considerable interest, this is now calculated using (8.61) and (8.65):

$$
\begin{equation*}
T=a f=\frac{R_{F} R_{L}}{R_{F} R_{L}+z_{o} R_{F}+z_{o} R_{L}} a_{v} \frac{z_{i}}{z_{i}+R_{F}} \tag{8.70}
\end{equation*}
$$

#### EXAMPLE

Assuming that the circuit of Fig. $8.15 a$ is realized using a NE5234 op amp with $R_{F}=1 \mathrm{M} \Omega$ and $R_{L}=10 \mathrm{k} \Omega$, calculate the terminal impedances, loop gain, and overall gain of the feedback amplifier at low frequencies. The NE5234 data are $z_{i}=170 \mathrm{k} \Omega, z_{o}=15 \mathrm{k} \Omega$, and $a_{v}=130,000$.

From (8.66) the low-frequency input impedance of the basic amplifier including loading is

$$
\begin{equation*}
z_{i a}=\frac{10^{6} \times 170 \times 10^{3}}{10^{6}+170 \times 10^{3}} \Omega=145 \mathrm{k} \Omega \tag{8.71}
\end{equation*}
$$

From (8.68), the low-frequency output impedance of the basic amplifier is

$$
\begin{equation*}
z_{o a}=15 \mathrm{k} \Omega\|1 \mathrm{M} \Omega\| 10 \mathrm{k} \Omega \simeq 5.96 \mathrm{k} \Omega \tag{8.72}
\end{equation*}
$$

The low-frequency loop gain can be calculated from (8.70) as

$$
\begin{align*}
T & =\frac{10^{6} \times 10^{4}}{10^{6} \times 10^{4}+15 \times 10^{3} \times 10^{6}+15 \times 10^{3} \times 10^{4}} \times 130,000 \times \frac{170 \times 10^{3}}{170 \times 10^{3}+10^{6}} \\
& =7510 \tag{8.73}
\end{align*}
$$

The loop gain in this case is large. Note that a finite source resistance at the input could reduce this significantly.

The input impedance with feedback applied is found by substituting (8.71) and (8.73) in (8.67) to give

$$
Z_{i}=\frac{145 \times 10^{3}}{7511} \Omega=19.3 \Omega
$$

The output impedance with feedback applied is found by substituting (8.72) and (8.73) in (8.69) to give

$$
Z_{o}=\frac{5.96 \times 10^{3}}{7511} \Omega=0.794 \Omega
$$

In practice, second-order effects in the circuit may result in a larger value of $Z_{o}$.
The overall transfer function with feedback can be found approximately from (8.8) as

$$
\begin{equation*}
\frac{v_{o}}{i_{i}}=A \simeq \frac{1}{f} \tag{8.74}
\end{equation*}
$$

Using (8.61) in (8.74) gives

$$
\frac{v_{o}}{i_{i}}=A \simeq-R_{F}
$$

Substituting for $R_{F}$ we obtain

$$
\begin{equation*}
\frac{v_{o}}{i_{i}}=A \simeq-1 \mathrm{M} \Omega \tag{8.75}
\end{equation*}
$$

A more exact value of $A$ can be calculated from (8.5). Since the loop gain is large in this case, it is useful to transform (8.5) as follows:

$$
\begin{align*}
A & =\frac{1}{f} \frac{1}{1+\frac{1}{a f}}  \tag{8.76}\\
& =\frac{1}{f} \frac{1}{1+\frac{1}{T}} \tag{8.77}
\end{align*}
$$

Since $T$ is high in this example, $A$ differs little from $1 / f$. Substituting $T=7510$ and $1 / f=$ $-1 \mathrm{M} \Omega$ in (8.77), we obtain

$$
\begin{equation*}
A=-999,867 \Omega \tag{8.78}
\end{equation*}
$$

- For most practical purposes, (8.75) is sufficiently accurate.

### 8.5.2 Series-Series Feedback

Consider the series-series feedback connection of Fig. 8.12. The effect of nonideal networks can be calculated using the representation of Fig. 8.16a. In this case the most convenient two-port representation is the use of the open-circuit impedance parameters or $z$ parameters because the basic amplifier and the feedback network are now connected in series at input and output and thus have identical currents at their terminals. As shown in Fig. 8.17, the $z$
image_name:(a)
description:The circuit diagram shows a series-series feedback configuration using z-parameters. It consists of a basic amplifier and a feedback network connected in series at both input and output, sharing identical currents at their terminals. The z-parameters are used to express terminal voltages in terms of terminal currents, simplifying calculations. The basic amplifier and feedback network are represented with resistors and voltage-controlled current sources.
image_name:(b)
description:This is a series-series feedback circuit using z-parameter representation. It consists of a basic amplifier and a feedback network. The basic amplifier is connected in series at both input and output, sharing identical currents with the feedback network.
Figure 8.16 (a) Series-series feedback configuration using the $z$-parameter representation.
(b) Circuit of (a) redrawn with generators $z_{21 f} i_{i}$ and $z_{12 a} i_{o}$ omitted.
parameters specify the network by expressing terminal voltages in terms of terminal currents, and this results in simple calculations when the two networks have common terminal currents. The calculation in this case proceeds as the exact dual of that in Section 8.5.1. From Fig. 8.16, summation of voltages at the input gives

$$
\begin{equation*}
v_{s}=\left(z_{S}+z_{11 a}+z_{11 f}\right) i_{i}+\left(z_{12 a}+z_{12 f}\right) i_{o} \tag{8.79}
\end{equation*}
$$

image_name:Figure 8.17
description:The diagram labeled "Figure 8.17" represents a two-port network using z-parameters (impedance parameters). It is a block diagram with two sets of terminals: one on the left side and one on the right side. The left terminals are labeled with voltage $v_1$ and current $i_1$, while the right terminals are labeled with voltage $v_2$ and current $i_2$. The current $i_1$ flows into the block from the left, and $i_2$ flows out of the block from the right, indicating the direction of current flow.

Main Components:
- **Two-Port Network Block:** This is the main component of the diagram, functioning as a black box that relates input and output voltages and currents through z-parameters.

Flow of Information or Control:
- **Input Side:** Voltage $v_1$ and current $i_1$ enter the block from the left.
- **Output Side:** Voltage $v_2$ and current $i_2$ exit the block on the right.
- The relationships between these voltages and currents are governed by the z-parameters.

Labels, Annotations, and Key Indicators:
- **Z-Parameters Equations:**
- $v_1 = z_{11} i_1 + z_{12} i_2$
- $v_2 = z_{21} i_1 + z_{22} i_2$
- **Definitions of Z-Parameters:**
- $z_{11} = \frac{v_1}{i_1} \bigg|_{i_2=0}$: Input impedance with output open-circuited.
- $z_{21} = \frac{v_2}{i_1} \bigg|_{i_2=0}$: Forward transfer impedance with output open-circuited.
- $z_{12} = \frac{v_1}{i_2} \bigg|_{i_1=0}$: Reverse transfer impedance with input open-circuited.
- $z_{22} = \frac{v_2}{i_2} \bigg|_{i_1=0}$: Output impedance with input open-circuited.

Overall System Function:
The primary function of this two-port network is to describe the relationship between the input and output voltages and currents using the z-parameter model. This model is useful for analyzing networks where impedance is the primary concern, allowing for the calculation of voltages and currents when the network is connected to external circuits. The z-parameters provide a convenient way to express these relationships, particularly for complex networks, by using open-circuit conditions to define the parameters.

Figure 8.17 The z-parameter representation of a two-port.

Summing voltages at the output we obtain

$$
\begin{equation*}
0=\left(z_{21 a}+z_{21 f}\right) i_{i}+\left(z_{L}+z_{22 a}+z_{22 f}\right) i_{o} \tag{8.80}
\end{equation*}
$$

It is useful to define

$$
\begin{align*}
z_{i} & =z_{S}+z_{11 a}+z_{11 f}  \tag{8.81}\\
z_{o} & =z_{L}+z_{22 a}+z_{22 f} \tag{8.82}
\end{align*}
$$

Again neglecting reverse transmission through the basic amplifier, we assume that

$$
\begin{equation*}
\left|z_{12 a}\right| \ll\left|z_{12 f}\right| \tag{8.83}
\end{equation*}
$$

Also neglecting feed-forward through the feedback network, we can write

$$
\begin{equation*}
\left|z_{21 a}\right| \gg\left|z_{21 f}\right| \tag{8.84}
\end{equation*}
$$

With these assumptions it follows that

$$
\begin{equation*}
\frac{i_{o}}{v_{s}}=A \simeq \frac{\frac{-z_{21 a}}{z_{i} z_{o}}}{1+\left(\frac{-z_{21 a}}{z_{i} z_{o}}\right) z_{12 f}}=\frac{a}{1+a f} \tag{8.85}
\end{equation*}
$$

where

$$
\begin{align*}
& a=-\frac{z_{21 a}}{z_{i} z_{o}}  \tag{8.86}\\
& f=z_{12 f} \tag{8.87}
\end{align*}
$$

A circuit representation of $a$ in (8.86) and $f$ in (8.87) can be found by removing generators $z_{21 f} i_{i}$ and $z_{12 a} i_{o}$ from Fig. $8.16 a$ in accord with (8.83) and (8.84). This gives the approximate representation of Fig. 8.16b, where the new basic amplifier includes the loading effect of the original feedback network. The new feedback network is an ideal one as used in Fig. 8.12. The transfer function of the basic amplifier of Fig. 8.16b is the same as in (8.86), and the transfer function of the feedback network of Fig. $8.16 b$ is given by (8.87). Thus Fig. $8.16 b$ is a circuit representation of (8.86) and (8.87).

Since Fig. 8.16b has a direct correspondence with Fig. 8.12, all the results of Section 8.4.4 can now be used. The loading effect of the feedback network on the basic amplifier is included
by connecting the feedback-network terminal impedances $z_{11 f}$ and $z_{22 f}$ in series at input and output of the basic amplifier. Terms $z_{11 f}$ and $z_{22 f}$ are defined in Fig. 8.17 and are obtained by calculating the terminal impedances of the feedback network with the other port open circuited. Feedback function $f$ given by (8.87) is the reverse transfer impedance of the feedback network.

Consider, for example, the series-series feedback triple of Fig. 8.18a, which is useful as a wideband feedback amplifier. $R_{E 2}$ is usually a small resistor that samples the output current $i_{o}$, and the resulting voltage across $R_{E 2}$ is sampled by the divider $R_{F}$ and $R_{E 1}$ to produce a feedback voltage across $R_{E 1}$. Usually $R_{F} \gg R_{E 1}$ and $R_{E 2}$.

The two-port theory derived earlier cannot be applied directly in this case because the basic amplifier cannot be represented by a two-port. However, the techniques developed previously using two-port theory can be used with minor modification by first noting that the feedback network can be represented by a two-port as shown in 8.18 b . One problem with this circuit is that the feedback generator $z_{12} i_{e 3}$ is in the emitter of $Q_{1}$ and not in the input lead where it can be compared directly with $v_{s}$. This problem can be overcome by considering the small-signal equivalent of the input portion of this circuit as shown in Fig. 8.19. For this circuit

$$
\begin{equation*}
v_{s}=i_{i} z_{S}+v_{b e}+i_{e 1} z_{11 f}+z_{12 f} i_{e 3} \tag{8.88}
\end{equation*}
$$

Using

$$
\begin{equation*}
i_{e 3}=\frac{i_{o}}{\alpha_{3}} \tag{8.89}
\end{equation*}
$$

in (8.88) gives

$$
\begin{equation*}
v_{s}-z_{12 f} \frac{i_{o}}{\alpha_{3}}=i_{i} z_{S}+v_{b e}+i_{e 1} z_{11 f} \tag{8.90}
\end{equation*}
$$

where the quantities in these equations are small-signal quantities. Equation 8.90 shows that the feedback voltage generator $z_{12 f}\left(i_{o} / \alpha_{3}\right)$ can be moved back in series with the input lead; if this was done, exactly the same equation would result. (See Fig. 8.18c.) Note that the commonbase current gain $\alpha_{3}$ of $Q_{3}$ appears in this feedback expression because the output current is sampled by $R_{E 2}$ in the emitter of $Q_{3}$ in order to feed back a correcting signal to the input. This problem is common to most circuits employing series feedback at the output, and the $\alpha_{3}$ of $Q_{3}$ is outside the feedback loop. There are many applications where this is not a problem, since $\alpha \simeq 1$. However, if high gain precision is required, variations in $\alpha_{3}$ can cause difficulties.

The $z$ parameters of the feedback network can be determined from Fig. 8.20 as

$$
\begin{align*}
& z_{12 f}=\left.\frac{v_{1}}{i_{2}}\right|_{i_{1}=0}=\frac{R_{E 1} R_{E 2}}{R_{E 1}+R_{E 2}+R_{F}}  \tag{8.91}\\
& z_{22 f}=\left.\frac{v_{2}}{i_{2}}\right|_{i_{1}=0}=R_{E 2} \|\left(R_{E 1}+R_{F}\right)  \tag{8.92}\\
& z_{11 f}=\left.\frac{v_{1}}{i_{1}}\right|_{i_{2}=0}=R_{E 1} \|\left(R_{F}+R_{E 2}\right) \tag{8.93}
\end{align*}
$$

Using (8.84), we neglect $z_{21}$.
From the foregoing results we can redraw the circuit of Fig. $8.18 b$ as shown in Fig. 8.18c. As in previous calculations, the signal fed forward via the feedback network (in this case $\left.z_{21} i_{e 1}\right)$ is neglected. The feedback voltage generator is placed in series with the input lead
image_name:(a)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: Zs, type: Resistor, value: Zs, ports: {N1: Vs, N2: b1}
name: Q1, type: NPN, ports: {C: b1, B: e1, E: GND}
name: RL1, type: Resistor, value: RL1, ports: {N1: c1b2, N2: GND}
name: Q2, type: NPN, ports: {C: c1b2, B: c2b3, E: GND}
name: RL2, type: Resistor, value: RL2, ports: {N1: c2b3, N2: GND}
name: Q3, type: NPN, ports: {C: c2b3, B: e3, E: GND}
name: RF, type: Resistor, value: RF, ports: {N1: e1, N2: e3}
name: RE1, type: Resistor, value: RE1, ports: {N1: e1, N2: GND}
name: RE2, type: Resistor, value: RE2, ports: {N1: e3, N2: GND}
name: ZL, type: Resistor, value: ZL, ports: {N1: c3, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: b1, Nn: c1b2}
name: C2, type: Capacitor, value: C2, ports: {Np: c1b2, Nn: c2b3}
name: C3, type: Capacitor, value: C3, ports: {Np: c2b3, Nn: c3}
]
extrainfo:The circuit is a series-series feedback triple amplifier with three NPN transistors (Q1, Q2, Q3) and a feedback network composed of resistors RF, RE1, and RE2. The input is provided by a voltage source Vs through a resistor Zs. The output is taken across a load resistor ZL. Capacitors C1, C2, and C3 are used for coupling between stages. The feedback network connects the emitter of Q1 to the emitter of Q3.
image_name:(b)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: Zs, type: Resistor, value: Zs, ports: {N1: Vs, N2: b1}
name: Q1, type: NPN, ports: {C: b1, B: e1, E: GND}
name: C1b2, type: Capacitor, value: C1b2, ports: {Np: e1, Nn: GND}
name: Q2, type: NPN, ports: {C: e1, B: e2, E: GND}
name: RL1, type: Resistor, value: RL1, ports: {N1: e1, N2: GND}
name: C2b2, type: Capacitor, value: C2b2, ports: {Np: e2, Nn: GND}
name: Q3, type: NPN, ports: {C: e2, B: e3, E: GND}
name: RL2, type: Resistor, value: RL2, ports: {N1: e2, N2: GND}
name: C3, type: Capacitor, value: C3, ports: {Np: e3, Nn: GND}
name: ZL, type: Resistor, value: ZL, ports: {N1: e3, N2: GND}
name: RF, type: Resistor, value: RF, ports: {N1: e1, N2: e3}
name: RE1, type: Resistor, value: RE1, ports: {N1: e1, N2: GND}
name: RE2, type: Resistor, value: RE2, ports: {N1: e3, N2: GND}
]
extrainfo:The circuit diagram represents a feedback amplifier with three NPN transistors (Q1, Q2, Q3) configured in a series-series feedback topology. The feedback network consists of resistors RE1, RE2, and RF. The input is connected through a voltage source Vs and a series resistor Zs. The output is taken across a load resistor ZL. Capacitors C1b2, C2b2, and C3 are used for coupling and bypassing signals.
image_name:(c)
description:
[
name: VS, type: VoltageSource, value: VS, ports: {Np: Vs, Nn: GND}
name: ZS, type: Resistor, value: ZS, ports: {N1: Vs, N2: b1}
name: Q1, type: NPN, ports: {C: b1, B: e1, E: GND}
name: RE1, type: Resistor, value: RE1, ports: {N1: e1, N2: GND}
name: RF, type: Resistor, value: RF, ports: {N1: e1, N2: e3}
name: RFE2, type: Resistor, value: (RF||RE2), ports: {N1: e1, N2: GND}
name: C1b2, type: Capacitor, value: C1b2, ports: {N1: b1, N2: GND}
name: Q2, type: NPN, ports: {C: b2, B: e3, E: GND}
name: RL1, type: Resistor, value: RL1, ports: {N1: b2, N2: GND}
name: C2b2, type: Capacitor, value: C2b2, ports: {N1: b2, N2: GND}
name: Q3, type: NPN, ports: {C: e3, B: GND, E: GND}
name: RL2, type: Resistor, value: RL2, ports: {N1: e3, N2: GND}
name: C3, type: Capacitor, value: C3, ports: {N1: e3, N2: GND}
name: ZL, type: Resistor, value: ZL, ports: {N1: e3, N2: GND}
]
extrainfo:The circuit diagram represents a feedback amplifier with three NPN transistors (Q1, Q2, Q3) arranged to provide amplification with feedback. The feedback network includes resistors RF and RE1||RE2. Capacitors C1b2, C2b2, and C3 are used for coupling and decoupling. The input is connected through a voltage source VS and a series resistor ZS. The output is taken across the load resistor ZL. The circuit employs series-series feedback to stabilize the gain and bandwidth.

Figure 8.18 (a) Series-series feedback triple. (b) Circuit of (a) redrawn using a two-port z-parameter representation of the feedback network. (c) Approximate representation of the circuit in (b).
image_name:Figure 8.19
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: X1, Nn: GND}
name: zS, type: Resistor, value: zS, ports: {N1: X1, N2: X2}
name: rπ1, type: Resistor, value: rπ1, ports: {N1: X2, N2: X1}
name: z11f, type: Resistor, value: z11f, ports: {N1: X1, N2: GND}
name: z12f, type: Resistor, value: z12f, ports: {N1: X1, N2: GND}
name: gm1Vbe, type: CurrentSource, ports: {Np: X1, Nn: X1}
]
extrainfo:The circuit represents a small-signal equivalent model of an input stage with feedback. The voltage source Vs is connected to the ground. Resistors zS and rπ1 form part of the input network. The feedback network includes resistors z11f and z12f. The current source gm1Vbe models the transconductance of the transistor.

Figure 8.19 Small-signal equivalent circuit of the input stage of the circuit in Fig. 8.18b.
and an ideal differencing node then exists at the input. The effect of feedback loading on the basic amplifier is represented by the impedances in the emitters of $Q_{1}$ and $Q_{3}$. Note that this case does differ somewhat from the example of Fig. $8.16 b$ in that the impedances $z_{11 f}$ and $z_{22 f}$ of the feedback network appear in series with the input and output leads in Fig. 8.16b, whereas in Fig. $8.18 c$ these impedances appear in the emitters of $Q_{1}$ and $Q_{3}$. This is due to the fact that the basic amplifier of the circuit of Fig. 8.18a cannot be represented by two-port $z$ parameters but makes no difference to the method of analysis. Since the feedback voltage generator in Fig. $8.18 c$ is directly in series with the input and is proportional to $i_{o}$, a direct correspondence with Fig. $8.16 b$ can be established and the results of Section 8.4 .4 can be applied. There is no further need of the $z$ parameters, and by inspection we can write

$$
\begin{equation*}
\frac{i_{o}}{v_{s}}=A \simeq \frac{a}{1+a f} \tag{8.94}
\end{equation*}
$$

where

$$
\begin{equation*}
f=\frac{z_{12 f}}{\alpha_{3}}=\frac{1}{\alpha_{3}} \frac{R_{E 1} R_{E 2}}{R_{E 1}+R_{E 2}+R_{F}} \tag{8.95}
\end{equation*}
$$

and $a$ is the transconductance of the circuit of Fig. $8.18 c$ with the feedback generator $\left[\left(z_{12 f} / \alpha_{3}\right) i_{o}\right]$ removed.

The input impedance seen by $v_{s}$ with feedback applied is $(1+a f) \times$ (input impedance of the basic amplifier of Fig. 8.18c including feedback loading).

The output impedance with feedback applied is $(1+a f)$ times the output impedance of the basic amplifier including feedback loading.
image_name:Figure 8.20
description:
[
name: i1, type: CurrentSource, ports: {Np: GND, Nn: V1}
name: RE1, type: Resistor, value: RE1, ports: {N1: V1, N2: GND}
name: RF, type: Resistor, value: RF, ports: {N1: V1, N2: V2}
name: RE2, type: Resistor, value: RE2, ports: {N1: V2, N2: GND}
name: i2, type: CurrentSource, ports: {Np: V2, Nn: GND}
]
extrainfo:The circuit consists of a series of resistors and current sources connected between nodes V1 and V2, with connections to ground. It is used to calculate the z parameters of the feedback network.

Figure 8.20 Circuit for the calculation of the $z$ parameters of the feedback network of the circuit in Fig 8.18a.

If the loop gain $T=a f$ is large, then the gain with feedback applied is

$$
\begin{equation*}
A=\frac{i_{o}}{v_{s}} \simeq \frac{1}{f}=\alpha_{3} \frac{R_{E 1}+R_{E 2}+R_{F}}{R_{E 1} R_{E 2}} \tag{8.96}
\end{equation*}
$$

#### EXAMPLE

A commercial integrated circuit ${ }^{2}$ based on the series-series triple is the MC 1553 shown in Fig. 8.21a. Calculate the terminal impedances, loop gain, and overall gain of this amplifier at low frequencies.

The MC 1553 is a wideband amplifier with a bandwidth of 50 MHz at a voltage gain of 50. The circuit gain is realized by the series-series triple composed of $Q_{1}, Q_{2}$, and $Q_{3}$. The output voltage is developed across the load resistor $R_{C}$ and is then fed to the output via emitter follower $Q_{4}$, which ensures a low output impedance. The rest of the circuit is largely for bias
image_name:Figure 8.21 (a)
description:The circuit is a multi-stage amplifier with a series-series configuration using transistors Q1, Q2, and Q3. The output is buffered by Q4 to ensure low output impedance. Biasing is provided by several resistors and capacitors in the circuit.

image_name:Figure 8.21 (b)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: 88, type: Resistor, value: 88Ω, ports: {N1: e1, N2: GND}
name: Q1, type: NPN, ports: {C: c1b2, B: vs, E: e1}
name: 9k, type: Resistor, value: 9kΩ, ports: {N1: c1b2, N2: GND}
name: Q2, type: NPN, ports: {C: c2b3, B: c1b2, E: GND}
name: 5k, type: Resistor, value: 5kΩ, ports: {N1: c2b3, N2: GND}
name: Q3, type: NPN, ports: {C: Vo, B: c2b3, E: e3}
name: 88, type: Resistor, value: 88Ω, ports: {N1: Vo, N2: GND}
name: Rc, type: Resistor, value: Rc, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a multi-stage amplifier with a series-series configuration using transistors Q1, Q2, and Q3. The output is buffered by Q4 to ensure low output impedance. Biasing is provided by several resistors and capacitors in the circuit.

Figure 8.21 (a) Circuit of the MC 1553 wideband integrated circuit. (b) Basic amplifier of the seriesseries triple in (a).
image_name:Figure 8.21 (c)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: rπ1, type: Resistor, value: rπ1, ports: {N1: Vs, N2: X1}
name: 88 Ω, type: Resistor, value: 88 Ω, ports: {N1: X1, N2: GND}
name: g_m1V1, type: VoltageControlledCurrentSource, value: g_m1V1, ports: {Np: V2, Nn: X1}
name: rπ2, type: Resistor, value: rπ2, ports: {N1: V2, N2: GND}
name: 9 kΩ, type: Resistor, value: 9 kΩ, ports: {N1: V2, N2: GND}
name: g_m2V2, type: VoltageControlledCurrentSource, value: g_m2V2, ports: {Np: V4, Nn: GND}
name: rπ3, type: Resistor, value: rπ3, ports: {N1: V4, N2: X2}
name: 5 kΩ, type: Resistor, value: 5 kΩ, ports: {N1: X2, N2: GND}
name: g_m3V3, type: VoltageControlledCurrentSource, value: g_m3V3, ports: {Np: Vo, Nn: X2}
name: 88 Ω, type: Resistor, value: 88 Ω, ports: {N1: Vo, N2: GND}
name: R_C, type: Resistor, value: R_C, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a small-signal equivalent of a multi-stage amplifier with a series-series configuration. It uses transistors Q1, Q2, and Q3, with Q4 providing output buffering to ensure low output impedance. The diagram shows biasing through resistors and capacitors, and the current sources represent transconductance in the stages.

$$
\begin{aligned}
& I_{C 1}=0.6 \mathrm{~mA} \quad I_{C 2}=1 \mathrm{~mA} \quad I_{C 3}=4 \mathrm{~mA} \\
& r_{\pi 1}=4.33 \mathrm{k} \Omega \quad r_{\pi 2}=2.6 \mathrm{k} \Omega \quad r_{\pi 3}=650 \Omega \\
& g_{m 1}=\frac{1}{43.3} \mho \quad g_{m 2}=\frac{1}{26} \mho \quad g_{m 3}=\frac{4}{26} \mho
\end{aligned}
$$

(c)

Figure 8.21 (c) Small-signal equivalent circuit of the basic amplifier in (b).
purposes except capacitors $C_{P}, C_{F}$, and $C_{B}$. Capacitors $C_{P}$ and $C_{F}$ are small capacitors of several picofarads and are included on the chip. They ensure stability of the feedback loop, and their function will be described in Chapter 9 . Capacitor $C_{B}$ is external to the chip and is a large bypass capacitor used to decouple the bias circuitry at the signal frequencies of interest.

Bias Calculation. The analysis of the circuit begins with the bias conditions. The bias current levels are set by the reference current $I_{R K}$ in the resistor $R_{K}$, and assuming $V_{B E(\text { on })}=0.6 \mathrm{~V}$ and $V_{C C}=6 \mathrm{~V}$, we obtain

$$
\begin{equation*}
I_{R K}=\frac{V_{C C}-2 V_{B E(\mathrm{on})}}{R_{K}} \tag{8.97}
\end{equation*}
$$

Substituting data in (8.97) gives

$$
I_{R K}=\frac{6-1.2}{6000} \mathrm{~A}=0.80 \mathrm{~mA}
$$

The current in the output emitter follower $Q_{4}$ is determined by the currents in $Q_{6}$ and $Q_{8}$. Transistor $Q_{8}$ has an area three times that of $Q_{7}$ and $Q_{6}$ and thus

$$
\begin{aligned}
& I_{C 8}=3 \times 0.8 \mathrm{~mA}=2.4 \mathrm{~mA} \\
& I_{C 6}=0.8 \mathrm{~mA}
\end{aligned}
$$

where $\beta_{F}$ is assumed large in these bias calculations. If the base current of $Q_{1}$ is small, all of $I_{C 6}$ and $I_{C 8}$ flow through $Q_{4}$ and

$$
\begin{equation*}
I_{C 4} \simeq I_{C 6}+I_{C 8} \tag{8.98}
\end{equation*}
$$

Thus

$$
I_{C 4} \simeq 3.2 \mathrm{~mA}
$$

Transistor $Q_{8}$ supplies most of the bias current to $Q_{4}$, and this device functions as a Class A emitter-follower output stage of the type described in Section 5.2. The function of $Q_{6}$ is to allow formation of a negative-feedback bias loop for stabilization of the dc operating point, and resistor $R_{G}$ is chosen to cause sufficient dc voltage drop to allow connection of $R_{D}$ back to the base of $Q_{1}$. Transistors $Q_{1}, Q_{2}, Q_{3}$, and $Q_{4}$ are then connected in a negative-feedback bias loop and the dc conditions can be ascertained approximately as follows.

If we assume that $Q_{2}$ is on, the voltage at the collector of $Q_{1}$ is about 0.6 V and the voltage $\operatorname{across} R_{A}$ is 5.4 V . Thus the current through $R_{A}$ is

$$
\begin{align*}
I_{R A} & =\frac{5.4}{R_{A}} \\
& =\frac{5.4}{9000}=0.6 \mathrm{~mA} \tag{8.99}
\end{align*}
$$

If $\beta_{F}$ is assumed high, it follows that

$$
\begin{equation*}
I_{C 1} \simeq I_{R A}=0.6 \mathrm{~mA} \tag{8.100}
\end{equation*}
$$

Since the voltage across $R_{E 1}$ is small, the voltage at the base of $Q_{1}$ is approximately 0.6 V , and if the base current of $Q_{1}$ is small, this is also the voltage at the collector of $Q_{6}$ since any voltage across $R_{D}$ will be small. The dc output voltage can be written

$$
\begin{equation*}
V_{O}=V_{C 6}+I_{C 6} R_{G} \tag{8.101}
\end{equation*}
$$

Substitution of data gives

$$
V_{O}=(0.6+0.8 \times 3) \mathrm{V}=3 \mathrm{~V}
$$

The voltage at the base of $Q_{4}$ (collector of $Q_{3}$ ) is $V_{B E}$ above $V_{O}$ and is thus 3.6 V . The collector current of $Q_{3}$ is

$$
\begin{equation*}
I_{C 3} \simeq \frac{V_{C C}-V_{C 3}}{R_{C}} \tag{8.102}
\end{equation*}
$$

Substitution of parameter values gives

$$
I_{C 3} \simeq \frac{6-3.6}{600} \mathrm{~A}=4 \mathrm{~mA}
$$

The voltage at the base of $Q_{3}$ (collector of $Q_{2}$ ) is

$$
\begin{equation*}
V_{B 3} \simeq-I_{E 3} R_{E 2}+V_{B E(\mathrm{on})} \tag{8.103}
\end{equation*}
$$

Thus

$$
V_{B 3}=V_{C 2} \simeq(4 \times 0.1+0.6) \mathrm{V}=1 \mathrm{~V}
$$

$I_{C 2}$ may be calculated from

$$
\begin{equation*}
I_{C 2} \simeq \frac{V_{C C}-V_{C 2}}{R_{B}} \tag{8.104}
\end{equation*}
$$

and substitution of parameter values gives

$$
I_{C 2} \simeq \frac{6-1}{5000} \mathrm{~A}=1 \mathrm{~mA}
$$

The ac Calculation. The ac analysis can now proceed using the methods previously developed in this chapter. For purposes of ac analysis, the feedback triple composed of $Q_{1}, Q_{2}$, and $Q_{3}$ in Fig. 8.21 $a$ is identical to the circuit in Fig. 8.18a, and the results derived previously for the latter circuit are directly applicable to the triple in Fig. 8.21a. To obtain the voltage gain of the circuit of Fig. 8.21a, we simply multiply the transconductance of the triple by the load resistor $R_{C}$, since the gain of the emitter follower $Q_{4}$ is almost exactly unity. Note that resistor $R_{D}$ is
assumed grounded for ac signals by the large capacitor $C_{B}$, and thus has no influence on the ac circuit operation, except for a shunting effect at the input that will be discussed later. From (8.95) the feedback factor $f$ of the series-series triple of Fig. 8.21a is

$$
\begin{equation*}
f=\frac{1}{0.99} \frac{100 \times 100}{100+100+640} \Omega=12.0 \Omega \tag{8.105}
\end{equation*}
$$

where $\beta_{0}=100$ has been assumed.
If the loop gain is large, the transconductance of the triple of Fig. $8.21 a$ can be calculated from (8.96) as

$$
\begin{equation*}
\frac{i_{o 3}}{v_{s}} \simeq \frac{1}{f}=\frac{1}{12} \mathrm{~A} / \mathrm{V} \tag{8.106}
\end{equation*}
$$

where $i_{03}$ is the small-signal collector current in $Q_{3}$ in Fig. 8.21a. If the input impedance of the emitter follower $Q_{4}$ is large, the load resistance seen by $Q_{3}$ is $R_{C}=600 \Omega$ and the voltage gain of the circuit is

$$
\begin{equation*}
\frac{v_{o}}{v_{s}}=-\frac{i_{o 3}}{v_{s}} \times R_{C} \tag{8.107}
\end{equation*}
$$

Substituting (8.106) in (8.107) gives

$$
\begin{equation*}
\frac{v_{o}}{v_{s}}=-50.0 \tag{8.108}
\end{equation*}
$$

Consider now the loop gain of the circuit of Fig. 8.21a. This can be calculated by using the basic-amplifier representation of Fig. $8.18 c$ to calculate the forward gain $a$. Fig. $8.18 c$ is redrawn in Fig. $8.21 b$ using data from this example, assuming that $z_{s}=0$ and omitting the feedback generator. The small-signal, low-frequency equivalent circuit is shown in Fig. 8.21c assuming $\beta_{0}=100$, and it is a straightforward calculation to show that the gain of the basic amplifier is

$$
\begin{equation*}
a=\frac{i_{3}}{v_{s}}=20.3 \mathrm{~A} / \mathrm{V} \tag{8.109}
\end{equation*}
$$

Combination of (8.105) and (8.109) gives

$$
\begin{equation*}
T=a f=12 \times 20.3=243.6 \tag{8.110}
\end{equation*}
$$

The transconductance of the triple can now be calculated more accurately from (8.94) as

$$
\begin{equation*}
\frac{i_{o 3}}{v_{s}}=\frac{a}{1+T}=\frac{20.3}{244.6} \mathrm{~A} / \mathrm{V}=0.083 \mathrm{~A} / \mathrm{V} \tag{8.111}
\end{equation*}
$$

Substitution of (8.111) in (8.107) gives for the overall voltage gain

$$
\begin{equation*}
\frac{v_{o}}{v_{s}}=-\frac{i_{o 3}}{v_{s}} R_{C}=-0.083 \times 600=-49.8 \tag{8.112}
\end{equation*}
$$

This is close to the approximate value given by (8.108).
The input resistance of the basic amplifier is readily determined from Fig. $8.21 c$ to be

$$
\begin{equation*}
r_{i a}=13.2 \mathrm{k} \Omega \tag{8.113}
\end{equation*}
$$

The input resistance when feedback is applied is

$$
\begin{equation*}
R_{i}=r_{i a}(1+T) \tag{8.114}
\end{equation*}
$$

Substituting (8.113) and (8.110) in (8.114) gives

$$
\begin{equation*}
R_{i}=13.2 \times 244.6 \mathrm{k} \Omega=3.23 \mathrm{M} \Omega \tag{8.115}
\end{equation*}
$$

As expected, series feedback at the input results in a high input resistance. In this example, however, the bias resistor $R_{D}$ directly shunts the input for ac signals and is outside the feedback loop. Since $R_{D}=12 \mathrm{k} \Omega$ and is much less than $R_{i}$, the resistor $R_{D}$ determines the input resistance for this circuit.

Finally, the output resistance of the circuit is of some interest. The output resistance of the triple can be calculated from Fig. 8.21 c by including output resistance $r_{o}$ in the model for $Q_{3}$. The resistance obtained is then multiplied by $(1+T)$ and the resulting value is much greater than the collector load resistor of $Q_{3}$, which is $R_{C}=600 \Omega$. The output resistance of the full circuit is thus essentially the output resistance of emitter follower $Q_{4}$ fed from a $600-\Omega$ source resistance, and this is

$$
\begin{equation*}
R_{o}=\frac{1}{g_{m 4}}+\frac{R_{C}}{\beta_{4}}=\left(\frac{26}{3.2}+\frac{600}{100}\right) \Omega=14 \Omega \tag{8.116}
\end{equation*}
$$

### 8.5.3 Series-Shunt Feedback

Series-shunt feedback is shown schematically in Fig. 8.4. The basic amplifier and the feedback network have the same input current and the same output voltage. A two-port representation that uses input current and output voltage as the independent variables is the hybrid $h$-parameter representation shown in Fig. 8.22. The $h$ parameters can be used to represent nonideal circuits in a series-shunt feedback as shown in Fig. 8.23a. Summation of voltages at the input of this figure gives

$$
\begin{equation*}
v_{s}=\left(z s+h_{11 a}+h_{11 f}\right) i_{i}+\left(h_{12 a}+h_{12 f}\right) v_{o} \tag{8.117}
\end{equation*}
$$

Summing currents at the output yields

$$
\begin{equation*}
0=\left(h_{21 a}+h_{21 f}\right) i_{i}+\left(y_{L}+h_{22 a}+h_{22 f}\right) v_{o} \tag{8.118}
\end{equation*}
$$

We now define

$$
\begin{align*}
z_{i} & =z_{S}+h_{11 a}+h_{11 f}  \tag{8.119}\\
y_{o} & =y_{L}+h_{22 a}+h_{22 f} \tag{8.120}
\end{align*}
$$

image_name:Figure 8.22
description:The diagram represents the h-parameter model of a two-port network. It includes equations for the voltages and currents at the input and output ports, expressed in terms of h-parameters. The parameters are defined as ratios of voltages and currents under specific conditions (v2=0 or i1=0). This model is useful for analyzing linear electrical networks.

Figure 8.22 The $h$-parameter representation of a two-port.
image_name:(a)
description:The circuit diagram represents a series-shunt feedback configuration using h-parameters. It consists of a basic amplifier and a feedback network. The amplifier is characterized by h-parameters: h11a, h12a, h21a, and h22a. The feedback network is characterized by h11f, h12f, h21f, and h22f. The circuit is used to analyze linear electrical networks with feedback.
image_name:(b)
description:This circuit diagram represents a series-shunt feedback configuration using the h-parameter model. The new basic amplifier and feedback network are shown, with key components like resistors and sources labeled with h-parameters. The feedback network is simplified by omitting certain generators.

Figure 8.23 (a) Series-shunt feedback configuration using the $h$-parameter representation. (b) Circuit of (a) redrawn with generators $h_{21 f} i_{i}$ and $h_{12 a} v_{o}$ omitted.
and make the same assumptions as in previous examples:

$$
\begin{align*}
& \left|h_{12 a}\right| \ll\left|h_{12 f}\right|  \tag{8.121}\\
& \left|h_{21 a}\right| \gg\left|h_{21 f}\right| \tag{8.122}
\end{align*}
$$

image_name:Figure 8.24
description:
[
name: RE, type: Resistor, value: RE, ports: {N1: V2, N2: GND}
name: RF, type: Resistor, value: RF, ports: {N1: V2, N2: Vo}
name: ZL, type: Resistor, value: ZL, ports: {N1: Vo, N2: GND}
name: Zi, type: Resistor, value: Zi, ports: {N1: V2, N2: Vs}
name: Zo, type: Resistor, value: Zo, ports: {N1: V3, N2: Vo}
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: Av, type: VoltageControlledVoltageSource, value: -av*v1, ports: {Np: V3, Nn: GND}
]
extrainfo:The circuit is a series-shunt feedback configuration using an op amp as the gain element. It includes a feedback network with resistors RE and RF, and a load resistor ZL. The op amp is represented by a voltage-controlled voltage source with gain -av.

Figure 8.24 Series-shunt feedback circuit using an op amp as the gain element.
It can then be shown that

$$
\begin{equation*}
\frac{v_{o}}{v_{s}}=A \simeq \frac{-\frac{h_{21 a}}{z_{i} y_{o}}}{1+\left(-\frac{h_{21 a}}{z_{i} y_{o}}\right) h_{12 f}}=\frac{a}{1+a f} \tag{8.123}
\end{equation*}
$$

where

$$
\begin{align*}
& a=-\frac{h_{21 a}}{z_{i} y_{o}}  \tag{8.124}\\
& f=h_{12 f} \tag{8.125}
\end{align*}
$$

A circuit representation of $a$ in (8.124) and $f$ in (8.125) can be found by removing the generators $h_{12 a} v_{o}$ and $h_{21} i_{i}$ from Fig. $8.23 a$ as suggested by the approximations of (8.121) and (8.122). This gives the approximate representation of Fig. $8.23 b$, where the new basic amplifier includes the loading effect of the original feedback network. As in previous examples, the circuit of Fig. $8.23 b$ is a circuit representation of (8.123), (8.124), and (8.125) and has the form of an ideal feedback loop. Thus all the equations of Section 8.4 .1 can be applied to the circuit.

For example, consider the common series-shunt op amp circuit of Fig. 8.24, which fits exactly the model described above. We first determine the $h$ parameters of the feedback network from Fig. 8.25:

$$
\begin{align*}
& h_{22 f}=\left.\frac{i_{2}}{v_{2}}\right|_{i_{1}=0}=\frac{1}{R_{F}+R_{E}}  \tag{8.126}\\
& h_{12 f}=\left.\frac{v_{1}}{v_{2}}\right|_{i_{1}=0}=\frac{R_{E}}{R_{E}+R_{F}} \tag{8.127}
\end{align*}
$$

image_name:Figure 8.25
description:
[
'name': 'I1', 'type': 'CurrentSource', 'value': 'I1', 'ports': {'Np': 'V1', 'Nn': 'GND'
'name': 'RE', 'type': 'Resistor', 'value': 'RE', 'ports': {'N1': 'V1', 'N2': 'GND'
'name': 'RF', 'type': 'Resistor', 'value': 'RF', 'ports': {'N1': 'V1', 'N2': 'V2'
'name': 'V2', 'type': 'VoltageSource', 'value': 'V2', 'ports': {'Np': 'V2', 'Nn': 'GND'
]
extrainfo:The circuit is a feedback network with a current source I1 and resistors RE and RF. The voltage sources V1 and V2 are connected to ground. The current i1 flows from V1 to ground, and the current i2 flows from V2 through RF towards V1.

image_name:Figure 8.26
description:
[
name: RE||RF, type: Resistor, value: RE||RF, ports: {N1: X1, N2: V+}
name: zi, type: Resistor, value: zi, ports: {N1: X1, N2: Vs}
name: zO, type: Resistor, value: zO, ports: {N1: V2, N2: Vo}
name: RE+RF, type: Resistor, value: RE+RF, ports: {N1: Vo, N2: GND}
name: zL, type: Resistor, value: zL, ports: {N1: Vo, N2: GND}
name: RE/(RE+RF)*v0, type: VoltageSource, value: RE/(RE+RF)*v0, ports: {Np: V+, Nn: GND}
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: -av1, type: VoltageSource, value: -av1, ports: {Np: V2, Nn: GND}
]
extrainfo:The circuit represents a feedback amplifier network. The left side shows a voltage divider with RE||RF and a feedback voltage source V4. The right side shows the amplifier output with a load resistor zL connected to ground. The gain of the amplifier is represented by the voltage source -av1.

Figure 8.26 Equivalent circuit for Fig. 8.24.

$$
\begin{equation*}
h_{11 f}=\left.\frac{v_{1}}{i_{1}}\right|_{v_{2}=0}=R_{E} \| R_{F} \tag{8.128}
\end{equation*}
$$

Using (8.122), we neglect $h_{21 f}$. The complete feedback amplifier including loading effects is shown in Fig. 8.26 and has a direct correspondence with Fig. 8.23b. (The only difference is that the op amp output is represented by a Thévenin rather than a Norton equivalent.)

The gain $a$ of the basic amplifier can be calculated from Fig. 8.26 by initially disregarding the feedback generator to give

$$
\begin{equation*}
a=\frac{z_{i}}{z_{i}+R} a_{v} \frac{z_{L X}}{z_{L X}+z_{o}} \tag{8.129}
\end{equation*}
$$

where

$$
\begin{align*}
R & =R_{E} \| R_{F}  \tag{8.130}\\
z_{L X} & =z_{L} \|\left(R_{E}+R_{F}\right) \tag{8.131}
\end{align*}
$$

Also

$$
\begin{equation*}
f=\frac{R_{E}}{R_{E}+R_{F}} \tag{8.132}
\end{equation*}
$$

Thus the overall gain of the feedback circuit is

$$
\begin{equation*}
A=\frac{v_{o}}{v_{s}}=\frac{a}{1+a f} \tag{8.133}
\end{equation*}
$$

and $A$ can be evaluated using (8.129) and (8.132).

#### EXAMPLE

Assume that the circuit of Fig. 8.24 is realized, using a differential amplifier with low-frequency parameters $z_{i}=100 \mathrm{k} \Omega, z_{o}=10 \mathrm{k} \Omega$, and $a_{v}=3000$. Calculate the input impedance of the feedback amplifier at low frequencies if $R_{E}=5 \mathrm{k} \Omega, R_{F}=20 \mathrm{k} \Omega$, and $z_{L}=10 \mathrm{k} \Omega$. Note that $z_{o}$ in this case is not small as is usually the case for an op amp, and this situation can arise in some applications.

This problem is best approached by first calculating the input impedance of the basic amplifier and then multiplying by $(1+T)$ as indicated by (8.25) to calculate the input impedance of the feedback amplifier. By inspection from Fig. 8.26 the input impedance of the basic amplifier is

$$
z_{i a}=z_{i}+R_{E} \| R_{F}=(100+5 \| 20) \mathrm{k} \Omega=104 \mathrm{k} \Omega
$$

image_name:Figure 8.27 Series-shunt feedback circuit
description:
[
name: Q1, type: NPN, ports: {C: C1b2, B: b1, E: e1}
name: Q2, type: NPN, ports: {C: C2b3, B: C1b2, E: GND}
name: Q3, type: NPN, ports: {C: GND, B: C2b3, E: Vo}
name: D1, type: Diode, ports: {Na: vS, Nc: Q1}
name: zS, type: Resistor, value: zS, ports: {N1: vS, N2: D1}
name: RL1, type: Resistor, value: RL1, ports: {N1: Cb2, N2: GND}
name: RL2, type: Resistor, value: RL2, ports: {N1: C2b3, N2: GND}
name: RE, type: Resistor, value: RE, ports: {N1: e1, N2: GND}
name: RF, type: Resistor, value: RF, ports: {N1: e1, N2: Vo}
name: zL, type: Resistor, value: zL, ports: {N1: Vo, N2: GND}
name: vS, type: VoltageSource, value: vS, ports: {Np: vS, Nn: GND}
]
extrainfo:The circuit is a series-shunt feedback amplifier with three NPN transistors Q1, Q2, and Q3. The feedback network is connected between the emitter of Q1 and the output node Vo. The input is applied at vS, and the output is taken from Vo. The circuit is designed to provide amplification with feedback to stabilize the gain.

Figure 8.27 Series-shunt feedback circuit.

The parallel combination of $z_{L}$ and $\left(R_{F}+R_{E}\right)$ in Fig. 8.27 is

$$
z_{L X}=\frac{10 \times 25}{35}=7.14 \mathrm{k} \Omega
$$

Substitution in (8.129) gives, for the gain of the basic amplifier of Fig. 8.26,

$$
a=\frac{100}{100+4} \times 3000 \times \frac{7.14}{7.14+10}=1202
$$

From (8.127) the feedback factor $f$ for this circuit is

$$
f=\frac{5}{5+20}=0.2
$$

and thus the loop gain is

$$
T=a f=1202 \times 0.2=240
$$

The input impedance of the feedback amplifier is thus

$$
Z_{i}=z_{i a}(1+T)=104 \times 241 \mathrm{k} \Omega=25 \mathrm{M} \Omega
$$

In this example the loading effect produced by $\left(R_{F}+R_{E}\right)$ on the output has a significant effect on the gain $a$ of the basic amplifier and thus on the input impedance of the feedback amplifier.

As another example of a series-shunt feedback circuit, consider the series-series triple of Fig. 8.18a but assume that the output signal is taken as the voltage at the emitter of $Q_{3}$, as shown in Fig. 8.27. This is an example of how the same circuit can realize two different feedback functions if the output is taken from different nodes. As in the case of Fig. 8.18a, the basic amplifier of Fig. 8.27 cannot be represented as a two-port. However, the feedback network can be represented as a two-port and the appropriate parameters are the $h$ parameters as shown in Fig. 8.28. The $h$ parameters for this feedback network are given by (8.126), (8.127), and (8.128) and $h_{21 f}$ is neglected. The analysis of Fig. 8.28 then proceeds in the usual manner.

### 8.5.4 Shunt-Series Feedback

Shunt-series feedback is shown schematically in Fig. 8.11. In this case the basic amplifier and the feedback network have common input voltages and output currents, and hybrid $g$ parameters as defined in Fig. 8.29 are best suited for use in this case. The feedback circuit is
image_name:Figure 8.28
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: Zs, type: Resistor, value: Zs, ports: {N1: Vs, N2: b1}
name: Q1, type: NPN, ports: {C: c1b2, B: b1, E: e1}
name: RL1, type: Resistor, value: RL1, ports: {N1: c1b2, N2: GND}
name: Q2, type: NPN, ports: {C: c2b3, B: c1b2, E: GND}
name: RL2, type: Resistor, value: RL2, ports: {N1: c2b3, N2: GND}
name: Q3, type: NPN, ports: {C: Vo, B: c2b3, E: GND}
name: (RF+RE), type: Resistor, value: (RF+RE), ports: {N1: Vo, N2: GND}
name: ZL, type: Resistor, value: ZL, ports: {N1: Vo, N2: Vo}
]
extrainfo:The circuit is a multi-stage amplifier with shunt-series feedback, consisting of three NPN transistors Q1, Q2, and Q3. The feedback network is connected to the output through a combination of resistors (RF+RE) and ZL, providing a feedback voltage to stabilize the amplifier's gain. The circuit is powered by a voltage source Vs and includes additional resistors Zs, RL1, and RL2 for biasing and load management.

Figure 8.28 Circuit equivalent to that of Fig. 8.27 using a two-port representation of the feedback network.
image_name:Figure 8.29
description:The system block diagram depicted in Figure 8.29 represents a two-port network using the $g$-parameter representation. This network is a fundamental building block in electrical engineering used to describe the behavior of linear electrical circuits.

Main Components:
1. **Two-Port Network Block:**
- The central component is a rectangular block representing the two-port network.
- It has two pairs of terminals: an input port and an output port.
- The input port is characterized by voltage $v_1$ and current $i_1$.
- The output port is characterized by voltage $v_2$ and current $i_2$.

2. **$g$-Parameters:**
- The block is defined by four $g$-parameters: $g_{11}$, $g_{12}$, $g_{21}$, and $g_{22}$.
- These parameters are used to express the relationships between the voltages and currents at the input and output ports.

Flow of Information or Control:
- **Input to Output Relations:**
- The current at the input, $i_1$, is given by the equation $i_1 = g_{11}v_1 + g_{12}i_2$.
- The voltage at the output, $v_2$, is given by the equation $v_2 = g_{21}v_1 + g_{22}i_2$.
- **Direction of Signal Flow:**
- The signals flow from the input port to the output port, with interactions between the input and output characterized by the $g$-parameters.

### Labels, Annotations, and Key Indicators:
- The diagram includes annotations indicating the relationships between the $g$-parameters and the voltages and currents.
- Each $g$-parameter is defined with specific boundary conditions, such as $g_{11} = \frac{i_1}{v_1}|_{i_2=0}$, which defines it as the input conductance with the output open-circuited.

Overall System Function:
- The primary function of this two-port network is to model the linear relationships between the input and output voltages and currents using the $g$-parameter set. This representation is particularly useful for analyzing and designing amplifiers and other linear circuits where feedback and interaction between stages are significant.

Figure 8.29 The $g$-parameter representation of a two-port.
shown in Fig. 8.30a, and, at the input, we find that

$$
\begin{equation*}
i_{s}=\left(y_{S}+g_{11 a}+g_{11 f}\right) v_{i}+\left(g_{12 a}+g_{12 f}\right) i_{o} \tag{8.134}
\end{equation*}
$$

At the output

$$
\begin{equation*}
0=\left(g_{21 a}+g_{21 f}\right) v_{i}+\left(z_{L}+g_{22 a}+g_{22 f}\right) i_{o} \tag{8.135}
\end{equation*}
$$

Defining

$$
\begin{align*}
& y_{i}=y_{S}+g_{11 a}+g_{11 f}  \tag{8.136}\\
& z_{o}=z_{L}+g_{22 a}+g_{22 f} \tag{8.137}
\end{align*}
$$

and making the assumptions

$$
\begin{align*}
& \left|g_{12 a}\right| \ll\left|g_{12 f}\right|  \tag{8.138}\\
& \left|g_{21 a}\right| \gg\left|g_{21 f}\right| \tag{8.139}
\end{align*}
$$

we find

$$
\begin{equation*}
\frac{i_{o}}{i_{s}}=A \simeq \frac{-\frac{g_{21 a}}{y_{i} z_{o}}}{1+\left(-\frac{g_{21 a}}{y_{i} z_{o}}\right) g_{12 f}}=\frac{a}{1+a f} \tag{8.140}
\end{equation*}
$$

image_name:(a)
description:The circuit diagram represents a shunt-series feedback configuration using g-parameter representation. It includes a basic amplifier section and a feedback network section. The basic amplifier consists of a current source, resistors, and voltage-controlled sources. The feedback network includes additional resistors and controlled sources to provide feedback to the amplifier.
image_name:(b)
description:The circuit diagram (b) represents a shunt-series feedback amplifier configuration. It includes a current source 'i_s', resistors 'y_s', 'g11a', 'g11f', 'g22a', 'z_L', and 'g22f'. The circuit also features a current-controlled current source 'g12a' and 'g12f', and a voltage-controlled voltage source 'g21a' and 'g21f'. The feedback network is integrated to improve the stability and bandwidth of the amplifier.

Figure 8.30 (a) Shunt-series feedback configuration using the $g$-parameter representation. (b) Circuit of (a) redrawn with generators $g_{21 f} v_{i}$ and $g_{12 a} i_{o}$ omitted.
where

$$
\begin{gather*}
a=-\frac{g_{21 a}}{y_{i} z_{o}}  \tag{8.141}\\
f=g_{12 f} \tag{8.142}
\end{gather*}
$$

Following the procedure for the previous examples, we can find a circuit representation for this case by eliminating the generators $g_{21 f} v_{i}$ and $g_{12 a} i_{o}$ to obtain the approximate
image_name:Figure 8.31
description:
[
name: is, type: CurrentSource, value: is, ports: {Np: b1, Nn: GND}
name: yS, type: Resistor, value: yS, ports: {N1: b1, N2: GND}
name: Q1, type: NPN, ports: {C: c1d2, B: b1, E: GND}
name: RL1, type: Resistor, value: RL1, ports: {N1: c1d2, N2: GND}
name: Q2, type: NPN, ports: {C: c2, B: c1d2, E: e2}
name: zL, type: Resistor, value: zL, ports: {N1: c2, N2: GND}
name: RF, type: Resistor, value: RF, ports: {N1: b1, N2: e2}
name: RE, type: Resistor, value: RE, ports: {N1: e2, N2: GND}
]
extrainfo:The circuit is a current feedback pair with a feedback network consisting of RF and RE. The feedback network connects the base of Q1 to the emitter of Q2.

Figure 8.31 Current feedback pair.
image_name:Figure 8.32
description:
[
name: v1, type: VoltageSource, value: v1, ports: {Np: V1, Nn: GND}
name: RF, type: Resistor, value: RF, ports: {N1: V1, N2: V2}
name: RE, type: Resistor, value: RE, ports: {N1: V2, N2: GND}
name: v2, type: CurrentSource, value: v2, ports: {Np: V2, Nn: GND}
]
extrainfo:The circuit is a simple series feedback network with two resistors and a voltage and current source. RF connects the voltage source v1 to node V2, and RE connects node V2 to ground. The current source v2 is connected at node V2 to ground.

Figure 8.32 Circuit for the calculation of the $g$ parameters of the feedback network in Fig. 8.31.
representation of Fig. 8.30b. Since this has the form of an ideal feedback circuit, all the results of Section 8.4.3 may now be used.

A common shunt-series feedback amplifier is the current-feedback pair of Fig. 8.31. Since the basic amplifier of Fig. 8.31 cannot be represented by a two-port, the representation of Fig. 8.30 b cannot be used directly. However, as in previous examples, the feedback network can be represented by a two-port, and the $g$ parameters can be calculated using Fig. 8.32 to give

$$
\begin{align*}
g_{11 f} & =\left.\frac{i_{1}}{v_{1}}\right|_{i_{2}=0}=\frac{1}{R_{F}+R_{E}}  \tag{8.143}\\
g_{12 f} & =\left.\frac{i_{1}}{i_{2}}\right|_{v_{1}=0}=-\frac{R_{E}}{R_{E}+R_{F}}  \tag{8.144}\\
g_{22 f} & =\left.\frac{v_{2}}{i_{2}}\right|_{v_{1}=0}=R_{E} \| R_{F} \tag{8.145}
\end{align*}
$$

Using (8.139), we neglect $g_{21 f}$. Assuming that $g_{21 f} v_{i}$ is negligible, we can redraw the circuit of Fig. 8.31 as shown in Fig. 8.33. This circuit has an ideal input differencing node, and the
image_name:Figure 8.33
description:
[
name: is, type: CurrentSource, value: is, ports: {Np: b1, Nn: GND}
name: yS, type: Resistor, value: yS, ports: {N1: b1, N2: GND}
name: (RE + RF), type: Resistor, value: (RE + RF), ports: {N1: b1, N2: GND}
name: -RE/(RE + RF), type: VoltageSource, value: -RE/(RE + RF), ports: {Np: b1, Nn: GND}
name: Q1, type: NPN, ports: {C: c1b2, B: b1, E: GND}
name: RL1, type: Resistor, value: RL1, ports: {N1: c1d2, N2: GND}
name: Q2, type: NPN, ports: {C: c2, B: c1b2, E: e2}
name: RE||RF, type: Resistor, value: RE||RF, ports: {N1: e2, N2: GND}
name: zL, type: Resistor, value: zL, ports: {N1: c2, N2: GND}
]
extrainfo:The circuit consists of two NPN transistors, Q1 and Q2, with a feedback network involving resistors and a current source. The feedback function is given by f = -RE/(RE + RF) * 1/α2, and the circuit is designed to calculate the overall current gain with feedback applied.

Figure 8.33 Circuit equivalent to that of Fig. 8.31 using a two-port representation of the feedback network.
feedback function can be identified as

$$
\begin{equation*}
f=-\frac{R_{E}}{R_{E}+R_{F}} \frac{1}{\alpha_{2}} \tag{8.146}
\end{equation*}
$$

The gain $a$ of the basic amplifier is determined by calculating the current gain of the circuit of Fig. 8.33 with the feedback generator removed. The overall current gain with feedback applied can then be calculated from (8.40).

### 8.5.5 Summary

The results derived above regarding practical feedback circuits and the effect of feedback loading can be summarized as follows.

First, input and output variables must be identified and the feedback identified as shunt or series at input and output.

The feedback function $f$ is found by the following procedure. If the feedback is shunt at the input, short the input feedback node to ground and calculate the feedback current. If the feedback is series at the input, open circuit the input feedback node and calculate the feedback voltage. In both these cases, if the feedback is shunt at the output, drive the feedback network with a voltage source. If the feedback is series at the output, drive with a current source.

The effect of feedback loading on the basic amplifier is found as follows. If the feedback is shunt at the input, short the input feedback node to ground to find the feedback loading on the output. If the feedback is series at the input, open circuit the input feedback node to calculate output feedback loading. Similarly, if the feedback is shunt or series at the output, then short or open the output feedback node to calculate feedback loading on the input.

These results along with other information are summarized in Table 8.1.

## 8.6 Single-Stage Feedback

The considerations of feedback circuits in this chapter have been mainly directed toward the general case of circuits with multiple stages in the basic amplifier. However, in dealing with some of these circuits (such as the series-series triple of Fig. 8.18a), equivalent circuits were derived in which one or more stages contained an emitter resistor. (See Fig. 8.18c.) Such a stage represents in itself a feedback circuit as will be shown. Thus the circuit of Fig. 8.18c contains feedback loops within a feedback loop, and this has a direct effect on the amplifier performance. For example, the emitter of $Q_{3}$ in Fig. $8.18 c$ has a linearizing effect on $Q_{3}$, and so does the overall feedback when the loop is closed. It is thus important to calculate the effects of both local and overall feedback loops. The term local feedback is often used instead of single-stage feedback. Local feedback is often used in isolated stages as well as being found inside overall feedback loops. In this section, the low-frequency characteristics of two basic single-stage feedback circuits will be analyzed.

### 8.6.1 Local Series-Series Feedback

A local series-series feedback stage in bipolar technology (emitter degeneration) is shown in Fig. 8.34a. The characteristics of this circuit were considered previously in Section 3.3.8,

Table 8.1 Summary of Feedback Configurations

| Feedback <br> Configuration | Two-PortParameterRepresentation | Output <br> Variable | Input <br> Variable | Transfer <br> Function <br> Stabilized | $Z_{i}$ | $Z_{o}$ | To Calculate Feedback Loading |  | To Calculate Feedback Function $f$ |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
|  |  |  |  |  |  |  | At Input | At Output |  |
| Shunt-shunt | y | $v_{o}$ | $i_{s}$ | $\frac{v_{o}}{i_{s}}$ <br> Transresistance | Low | Low | Short circuit <br> output <br> feedback <br> node | Short circuit input feedback node | Drive the feedback network with a voltage at its output and calculate the current flowing into a short at its input |
| Shunt-series | g | $i_{o}$ | $i_{s}$ | $\begin{aligned} & \frac{i_{o}}{i_{s}} \\ & \text { Current gain } \end{aligned}$ | Low | High | Open circuit output feedback node | Short circuit input feedback node | Drive the feedback network with a current and calculate the current flowing into a short |
| Series-shunt | h | $v_{o}$ | $v_{s}$ | $\begin{aligned} & \frac{v_{o}}{v_{s}} \\ & \text { Voltage gain } \end{aligned}$ | High | Low | Short circuit <br> output <br> feedback <br> node | Open circuit input feedback node | Drive the feedback network with a voltage and calculate the voltage produced into an open circuit |
| Series-series | z | $i_{o}$ | $v_{s}$ | $\frac{i_{o}}{v_{s}}$ <br> Transconductance | High | High | Open circuit <br> output <br> feedback <br> node | Open circuit input feedback node | Drive the feedback network with a current and calculate the voltage produced into an open circuit |

image_name:(a)
description:
[
name: vs, type: VoltageSource, value: vs, ports: {Np: Vs, Nn: GND}
name: B0, type: NPN, ports: {C: Vo, B: Vs, E: e0}
name: RE, type: Resistor, value: RE, ports: {N1: e0, N2: GND}
name: ZL, type: Resistor, value: ZL, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a single-stage series-series feedback amplifier with an NPN transistor. It uses a voltage source vs and feedback is provided through resistors rb, rπ, and rb||rN. The output is taken across a load resistor ZL.
image_name:(b)
description:
[
name: vs, type: VoltageSource, value: vs, ports: {Np: Vs, Nn: GND}
name: rb, type: Resistor, value: rb, ports: {N1: Vs, N2: rbrπ}
name: rπ, type: Resistor, value: rπ, ports: {N1: rbrπ, N2: X1}
name: RE, type: Resistor, value: RE, ports: {N1: X1, N2: GND}
name: gmV1, type: VoltageControlledCurrentSource, value: gmV1, ports: {Np: Vo, Nn: X1}
name: zL, type: Resistor, value: zL, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a low-frequency equivalent of a single-stage series-series feedback amplifier. It uses a voltage source vs, resistors rb, rπ, rb||rN, RE, and zL, and a voltage-controlled current source gmV1. The circuit forms a feedback loop with the output voltage Vo and input voltage Vs.

image_name:(c)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: rb, type: Resistor, value: rb, ports: {N1: Vs, N2: rbrπ}
name: rπ, type: Resistor, value: rπ, ports: {N1: rbrπ, N2: RErπ}
name: RE, type: Resistor, value: RE, ports: {RErπ: vπ, N2: GND}
name: vfb, type: VoltageSource, value: ioRE, ports: {Np: Vfb, Nn: GND}
]
extrainfo:The circuit is a low-frequency equivalent of a single-stage series-series feedback amplifier. It forms a feedback loop with the output voltage Vo and input voltage Vs. The feedback is observed through the voltage-controlled current source gmV1 and resistors rb, rπ, and RE.

(c)

Figure 8.34 (a) Single-stage series-series feedback circuit. (b) Low-frequency equivalent circuit of $(a)$. (c) Circuit equivalent to (b) using a Thévenin equivalent across the plane AA.
and it will be considered again here from the feedback viewpoint. Similar results are found for MOS transistors with source degeneration.

The circuit of Fig. 8.34a can be recognized as a degenerate series-series feedback configuration as described in Sections 8.4.4 and 8.5.2. Instead of attempting to use the generalized forms of those sections, we can perform a more straightforward calculation in this simple case by working directly from the low-frequency, small-signal equivalent circuit shown in Fig. 8.34b. For simplicity, source impedance is assumed zero but can be lumped in with $r_{b}$ if desired. If a Thévenin equivalent across the plane $A A$ is calculated, Fig. $8.34 b$ can be redrawn as in Fig. 8.34c. The existence of an input differencing node is apparent, and quantity $i_{o} R_{E}$ is identified as the feedback voltage $v_{f b}$. Writing equations for Fig. $8.34 c$ we find

$$
\begin{gather*}
v_{1}=\frac{r_{\pi}}{r_{\pi}+r_{b}+R_{E}}\left(v_{s}-v_{f b}\right)  \tag{8.147}\\
i_{o}=g_{m} v_{1}  \tag{8.148}\\
v_{f b}=i_{o} R_{E} \tag{8.149}
\end{gather*}
$$

These equations are of the form of the ideal feedback equations where $v_{1}$ is the error voltage, $i_{o}$ is the output signal, and $\nu_{f b}$ is the feedback signal. From (8.147) and (8.148) we know that

$$
\begin{equation*}
i_{o}=\frac{g_{m} r_{\pi}}{r_{\pi}+r_{b}+R_{E}}\left(v_{s}-v_{f b}\right) \tag{8.150}
\end{equation*}
$$

and thus we can identify

$$
\begin{equation*}
a=\frac{g_{m} r_{\pi}}{r_{\pi}+r_{b}+R_{E}}=\frac{g_{m}}{1+\frac{r_{b}+R_{E}}{r_{\pi}}} \tag{8.151}
\end{equation*}
$$

From (8.149)

$$
\begin{equation*}
f=R_{E} \tag{8.152}
\end{equation*}
$$

Thus for the complete circuit

$$
\begin{equation*}
\frac{i_{o}}{v_{s}}=A=\frac{a}{1+a f}=\frac{1}{R_{E}} \frac{1}{1+\frac{1}{R_{E}}\left(\frac{1}{g_{m}}+\frac{r_{b}+R_{E}}{\beta_{0}}\right)} \tag{8.153}
\end{equation*}
$$

and $A \simeq 1 / R_{E}$ for large loop gain.
The loop gain is given by $T=a f$ and thus

$$
\begin{equation*}
T=\frac{g_{m} R_{E}}{1+\frac{r_{b}+R_{E}}{r_{\pi}}} \tag{8.154}
\end{equation*}
$$

If $\left(r_{b}+R_{E}\right) \ll r_{\pi}$ we find

$$
\begin{equation*}
T \simeq g_{m} R_{E} \tag{8.155}
\end{equation*}
$$

The input resistance of the circuit is given by

$$
\begin{align*}
\text { Input resistance } & =(1+T) \times\left(\text { input resistance with } v_{f b}=0\right) \\
& =(1+T)\left(r_{b}+r_{\pi}+R_{E}\right) \tag{8.156}
\end{align*}
$$

Using (8.154) in (8.156) gives

$$
\begin{align*}
\text { Input resistance } & =r_{b}+R_{E}+r_{\pi}\left(1+g_{m} R_{E}\right)  \tag{8.157}\\
& =r_{b}+r_{\pi}+\left(\beta_{0}+1\right) R_{E} \tag{8.158}
\end{align*}
$$

We can also show that if the output resistance $r_{o}$ of the transistor is included, the output resistance of the circuit is given by

$$
\begin{equation*}
\text { Output resistance } \simeq r_{o}\left(1+\frac{g_{m} R_{E}}{1+\frac{r_{b}+R_{E}}{r_{\pi}}}\right) \tag{8.159}
\end{equation*}
$$

Both input and output resistance are increased by the application of emitter feedback, as expected.

#### EXAMPLE

Calculate the low-frequency parameters of the series-series feedback stage represented by $Q_{3}$ in Fig. 8.21b. The relevant parameters are as follows:

$$
R_{E}=88 \Omega \quad r_{\pi}=650 \Omega \quad g_{m}=\frac{4}{26} \mathrm{~A} / \mathrm{V} \quad \beta_{0}=100 \quad r_{b}=0
$$

The loading produced by $Q_{3}$ at the collector of $Q_{2}$ is given by the input resistance expression of (8.158) and is

$$
\begin{equation*}
R_{i 3}=(650+101 \times 88) \Omega=9.54 \mathrm{k} \Omega \tag{8.160}
\end{equation*}
$$

The output resistance seen at the collector of $Q_{3}$ can be calculated from (8.159) using $r_{b}=$ $5 \mathrm{k} \Omega$ to allow for the finite source resistance in Fig. $8.21 b$. If we assume that $r_{o}=25 \mathrm{k} \Omega$ at $I_{C}=4 \mathrm{~mA}$ for $Q_{3}$, then from (8.159) we find that

$$
\begin{equation*}
R_{o 3}=25\left(1+\frac{\frac{4}{26} 88}{1+\frac{5088}{650}}\right) \mathrm{k} \Omega=63 \mathrm{k} \Omega \tag{8.161}
\end{equation*}
$$

In the example of Fig. 8.21b, the above output resistance would be multiplied by the loop gain of the series-series triple.

Finally, when ac voltage $v_{4}$ at the collector of $Q_{2}$ in Fig. $8.21 c$ is determined, output current $i_{3}$ in $Q_{3}$ can be calculated using (8.153):

$$
\begin{equation*}
\frac{i_{3}}{v_{4}}=\frac{1}{88} \frac{1}{1+\frac{1}{88}\left(\frac{26}{4}+\frac{88}{100}\right)} \mathrm{A} / \mathrm{V}=\frac{1}{95.4} \mathrm{~A} / \mathrm{V} \tag{8.162}
\end{equation*}
$$

Note that since the voltage $v_{4}$ exists at the base of $Q_{3}$, the effective source resistance in the above calculation is zero.

### 8.6.2 Local Series-Shunt Feedback

Another example of a local feedback stage is the common-drain stage shown in Fig. 8.35a. This circuit is a series-shunt feedback configuration. The small-signal model is shown in Fig. 8.35b. The current through the $g_{m b}$ controlled source is controlled by the voltage across it; therefore, it can be replaced by a resistor of value $1 / g_{m b}$. Using this transformation, the small-signal model in Fig. $8.35 b$ is redrawn in Fig. $8.35 c$, where

$$
\begin{equation*}
R_{L}^{\prime}=R_{L}\left\|r_{o}\right\| \frac{1}{g_{m b}} \tag{8.163}
\end{equation*}
$$

The feedback network is taken to be $R_{L}^{\prime}$. Using Fig. 8.35d, the $h$ two-port parameters for the feedback network are

$$
\begin{gather*}
h_{11 f}=\left.\frac{v_{1}}{i_{1}}\right|_{v_{2}=0}=0  \tag{8.164}\\
h_{22 f}=\left.\frac{i_{2}}{v_{2}}\right|_{i_{1}=0}=\frac{1}{R_{L}^{\prime}} \tag{8.165}
\end{gather*}
$$

image_name:(a)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vs, N2: g0}
name: NMOS, type: NMOS, ports: {S: V0, D: VDD, G: go}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a source follower driving a resistive load with a feedback network. The NMOS transistor is connected in a common-drain configuration, with the source grounded and the drain connected to the output node Vo. The input voltage Vs is applied through resistor RS.
image_name:(b)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vs, N2: V1(V0+vx)}
name: g_m*v_x, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Vo}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: GND}
name: g_mb*v_o, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: Vo}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit in diagram (b) is a small-signal model of a source follower driving a resistive load. It includes a voltage source Vs, a resistor RS, an NMOS transistor, and two voltage-controlled current sources modeling the transconductance g_m and body effect g_mb. The output is taken across RL, the load resistor, and ro, the output resistance of the transistor.
image_name:(c)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vs, N2: V1}
name: "g_mv_x", type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: V0}
name: "RL", type: Resistor, value: "RL", ports: {N1: Vo, N2: GND'}
]
extrainfo:The circuit diagram (c) represents a simplified small-signal model with a feedback network. The feedback network is represented by R'L and a voltage-controlled current source g_m'v_x. The source voltage Vs is connected through a resistor RS to the input node V1. The output voltage Vo is connected across the feedback network to ground.
image_name:(d)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: v1, Nn: GND}
name: V2, type: VoltageSource, value: V2, ports: {Np: v1, Nn: GND}
name: "RL", type: Resistor, value: "RL", ports: {N1: v1, N2: GND}
]
extrainfo:The circuit represents a two-port network model with a voltage source V1 and V2 connected across a resistor R'L. The network is used to find two-port parameters for the feedback network.

image_name:(e)
description:The circuit is a feedback network with a voltage source Vs, a resistor Rs, a current source Is that depends on Vx, and a load resistor R'L. The feedback factor is given by v_fb = 1 * v_o, and the feedback network is used to find the two-port parameters.

Figure 8.35 (a) A source follower driving a resistive load. (b) A small-signal model for the circuit in (a). (c) A simplified small-signal model. (d) Circuit for finding the two-port parameters for the feedback network. (e) The circuit in (c) with the feedback network replaced by a two-port model.
and the feedback factor is

$$
\begin{equation*}
f=h_{12 f}=\left.\frac{v_{1}}{v_{2}}\right|_{i_{1}=0}=1 \tag{8.166}
\end{equation*}
$$

Here we neglect the forward transmission through the feedback network, $h_{21 f}$, as was done in Section 8.5.3.

Figure $8.35 b$ is redrawn in Fig. $8.35 e$ with the feedback network replaced by a two-port model. The gain of the basic amplifier $a$ is found by setting the feedback to zero in Fig. $8.35 e$

$$
\begin{equation*}
a=\left.\frac{v_{o}}{v_{s}}\right|_{v_{f b}=0}=g_{m} R_{L}^{\prime} \tag{8.167}
\end{equation*}
$$

Using (8.166) and (8.167), the closed-loop gain is

$$
\begin{equation*}
A=\frac{a}{1+a f}=\frac{g_{m} R_{L}^{\prime}}{1+g_{m} R_{L}^{\prime}} \tag{8.168}
\end{equation*}
$$

This closed-loop gain is always less than one and approaches unity as $g_{m} R_{L}^{\prime} \rightarrow \infty$.
From Fig. 8.35e, the output resistance without feedback is $R_{L}^{\prime}$, and the closed-loop output resistance is

$$
\begin{equation*}
R_{o}=\frac{R_{L}^{\prime}}{1+a f}=\frac{R_{L}^{\prime}}{1+g_{m} R_{L}^{\prime}}=\frac{1}{\frac{1}{R_{L}^{\prime}}+g_{m}}=\frac{1}{\frac{1}{R_{L}}+\frac{1}{r_{o}}+g_{m b}+g_{m}} \tag{8.169}
\end{equation*}
$$

where (8.163) is used in the right-most expression. The output resistance is reduced because of the feedback. The input resistance is infinite because the resistance from the gate to the source in the model in Fig. 8.35 is infinite.

## 8.7 The Voltage Regulator as a Feedback Circuit

As an example of a practical feedback circuit, the operation of a voltage regulator will be examined. This section is introduced for the dual purpose of illustrating the use of feedback in practice and for describing the elements of voltage regulator design.

Voltage regulators are widely used components that accept a poorly specified (possibly fluctuating) dc input voltage and produce from it a constant, well-specified output voltage that can then be used as a supply voltage for other circuits. ${ }^{3}$ In this way, fluctuations in the supply voltage are essentially eliminated, and this usually results in improved performance for circuits powered from such a supply.

A common type of voltage regulator is the series regulator shown schematically in Fig. 8.36. The name series comes from the fact that the output voltage is controlled by a power transistor in series with the output. This is the last stage of a high-gain voltage amplifier, as shown in Fig. 8.36.

Many of the techniques discussed in previous chapters are utilized in the design of circuits of this kind. A stable reference voltage $V_{R}$ can be generated using a Zener diode or a bandgap reference, as described in Chapter 4. This is then fed to the noninverting input of the high-gain amplifier, where it is compared with a sample of the output taken by resistors $R_{1}$ and $R_{2}$. This is recognizable as a series-shunt feedback arrangement, and using (8.132) we find that for large loop gain

$$
\begin{equation*}
V_{O}=V_{R} \frac{R_{1}+R_{2}}{R_{2}} \tag{8.170}
\end{equation*}
$$

The output voltage can be varied by changing ratio $R_{1} / R_{2}$.
image_name:Figure 8.36
description:This is a series voltage regulator circuit. The OpAmp compares the reference voltage V_R with a portion of the output voltage V_O, adjusted by resistors R1 and R2. The output voltage V_O can be adjusted by changing the ratio of R1 to R2.

Figure 8.36 Schematic of a series voltage regulator.

The characteristics required in the amplifier of Fig. 8.36 are those of a good op amp, as described in Chapter 6. In particular, low drift and offset are essential so that the output voltage $V_{O}$ is as stable as possible. Note that the series-shunt feedback circuit will present a high input impedance to the reference generator, which is desirable to minimize loading effects. In addition, a very low output impedance will be produced at $V_{O}$, which is exactly the requirement for a good voltage source. If the effects of feedback loading are neglected (usually a good assumption in such circuits), the low-frequency output resistance of the regulator is given by (8.29) as

$$
\begin{equation*}
R_{o}=\frac{r_{o a}}{1+T} \tag{8.171}
\end{equation*}
$$

where

$$
\begin{align*}
T & =a \frac{R_{2}}{R_{1}+R_{2}}  \tag{8.172}\\
r_{o a} & =\text { output resistance of the amplifier without feedback } \\
a & =\text { magnitude of the forward gain of the regulator amplifier }
\end{align*}
$$

If the output voltage of the regulator is varied by changing ratio $R_{1} / R_{2}$, then (8.171) and (8.172) indicate that $T$ and thus $R_{o}$ also change. Assuming that $V_{R}$ is constant and $T \gg 1$, we can describe this behavior by substituting (8.170) and (8.172) in (8.171) to give

$$
\begin{equation*}
R_{o}=\frac{r_{o a}}{a V_{R}} V_{O} \tag{8.173}
\end{equation*}
$$

which shows $R_{o}$ to be a function of $V_{O}$ if $a, V_{R}$, and $r_{o a}$ are fixed. If the output current drawn from the regulator changes by $\Delta I_{O}$, then $V_{O}$ changes by $\Delta V_{O}$, where

$$
\begin{equation*}
\Delta V_{O}=R_{o} \Delta I_{O} \tag{8.174}
\end{equation*}
$$

Substitution of (8.173) in (8.174) gives

$$
\begin{equation*}
\frac{\Delta V_{O}}{V_{O}}=\frac{r_{o a}}{a V_{R}} \Delta I_{O} \tag{8.175}
\end{equation*}
$$

This equation allows calculation of the load regulation of the regulator. This is a widely used specification, which gives the percentage change in $V_{O}$ for a specified change in $I_{O}$ and should be as small as possible.

Another common regulator specification is the line regulation, which is the percentage change in output voltage for a specified change in input voltage. Since $V_{O}$ is directly proportional to $V_{R}$, the line regulation is determined by the change in reference voltage $V_{R}$ with changes in input voltage and depends on the particular reference circuit used.

As an example of a practical regulator, consider the circuit diagram of the 723 monolithic voltage regulator shown in Fig. 8.37. The correspondence to Fig. 8.36 can be recognized, with the portion of Fig. 8.37 to the right of the dashed line being the voltage amplifier with feedback. The divider resistors $R_{1}$ and $R_{2}$ in Fig. 8.36 are labeled $R_{A}$ and $R_{B}$ in Fig. 8.37 and are external to the chip. The output power transistor $Q_{15}$ is on the chip and is Darlington connected with $Q_{14}$ for high gain. Differential pair $Q_{11}$ and $Q_{12}$, together with active load $Q_{8}$, contribute most of the gain of the amplifier. Resistor $R_{C}$ couples the reference voltage to the amplifier and $C_{2}$ is an external capacitor, which is needed to prevent oscillation in the high-gain feedback loop. Its function is discussed in Chapter 9.

#### - EXAMPLE

Calculate the bias conditions and load regulation of the 723. Assume the total supply voltage is 15 V .

The bias calculation begins at the left-hand side of Fig. 8.37. Current source $I_{1}$ models a transistor current source that uses a junction field-effect transistor $(\mathrm{JFET})^{4}$ that behaves like an $n$-channel MOS transistor with a negative threshold voltage. Diodes $D_{1}$ and $D_{2}$ are Zener diodes. ${ }^{4}$ When operating in reverse breakdown, the voltage across a Zener diode is nearly constant as described in Chapter 2.

The Zener diode $D_{1}$ produces a voltage drop of about 6.2 V , which sets up a reference current in $Q_{2}$ :

$$
\begin{align*}
I_{C 2} & =-\frac{6.2-\left|V_{B E 2}\right|}{R_{1}+R_{2}} \\
& =-\frac{6.2-0.6}{16,000} \mathrm{~A} \\
& =-348 \mu \mathrm{~A} \tag{8.176}
\end{align*}
$$

Note that $I_{C 2}$ is almost independent of supply voltage because it is dependent only on the Zener diode voltage.

The voltage across $R_{1}$ and $Q_{2}$ establishes the currents in current sources $Q_{3}, Q_{7}$, and $Q_{8}$.

$$
\begin{align*}
& I_{C 7}=I_{C 8}=-174 \mu \mathrm{~A}  \tag{8.177}\\
& I_{C 3}=-10.5 \mu \mathrm{~A} \tag{8.178}
\end{align*}
$$

Current source $Q_{3}$ establishes the operating current in the voltage reference circuit composed of transistors $Q_{4}, Q_{5}, Q_{6}$, resistors $R_{6}, R_{7}, R_{8}$, and Zener diode $D_{2}$. This circuit can be recognized as a variation of the Wilson current source described in Chapter 4, and
image_name:Figure 8.37 Circuit diagram of the 723 monolithic voltage regulator
description:The circuit is a 723 monolithic voltage regulator. It includes a voltage reference circuit with a Zener diode (D2) and transistors Q4, Q5, Q6, and resistors R6, R7, R8. The reference voltage V_R is approximately 6.8 V. The current sources Q3, Q7, and Q8 establish specific currents in the circuit. The circuit utilizes a Wilson current source configuration.

Figure 8.37 Circuit diagram of the 723 monolithic voltage regulator.
the negative feedback loop forces the current in $Q_{6}$ to equal $I_{C 3}$ so that

$$
\begin{equation*}
I_{C 6}=10.5 \mu \mathrm{~A} \tag{8.179}
\end{equation*}
$$

where the base current of $Q_{4}$ has been neglected.
The output reference voltage $V_{R}$ is composed of the sum of the Zener diode voltage $D_{2}$ plus the base-emitter voltage of $Q_{6}$, giving a reference voltage of about 6.8 V . The current in the Zener is established by $V_{B E 6}$ and $R_{8}$ giving

$$
\begin{equation*}
I_{D 2}=\frac{V_{B E 6}}{R_{8}}=\frac{600}{5} \mu \mathrm{~A}=120 \mu \mathrm{~A} \tag{8.180}
\end{equation*}
$$

The Darlington pair $Q_{4}, Q_{5}$ helps give a large loop gain that results in a very low output impedance at the voltage reference node. Resistor $R_{6}$ limits the current and protects $Q_{5}$ in case of an accidental grounding of the voltage reference node. Resistor $R_{7}$ and capacitor $C_{1}$ form the high-frequency compensation required to prevent oscillation in the feedback loop. Note that the feedback is shunt at the output node. Any changes in reference-node voltage (due to loading for example) are detected at the base of $Q_{6}$, amplified, and fed to the base of $Q_{4}$ and thus back to the output where the original change is opposed.

The biasing of the amplifier is achieved via current sources $Q_{7}$ and $Q_{8}$. The current in $Q_{7}$ also appears in $Q_{10}$ (neglecting the base current of $Q_{9}$ ). Transistor $Q_{13}$ has an area twice that of $Q_{10}$ and one half the emitter resistance. Thus

$$
\begin{equation*}
I_{C 13}=2 I_{C 10}=2 I_{C 7}=348 \mu \mathrm{~A} \tag{8.181}
\end{equation*}
$$

Transistor $Q_{9}$ provides current gain to minimize the effect of base current in $Q_{10}$ and $Q_{13}$. This beta-helper current mirror was described in Chapter 4.

The bias current in each half of the differential pair $Q_{11}, Q_{12}$ is thus

$$
\begin{equation*}
I_{C 11}=I_{C 12}=\frac{1}{2} I_{C 13}=174 \mu \mathrm{~A} \tag{8.182}
\end{equation*}
$$

Since $Q_{8}$ and $R_{5}$ are identical to $Q_{7}$ and $R_{4}$, the current in $Q_{8}$ is given by

$$
\begin{equation*}
I_{C 8}=-174 \mu \mathrm{~A} \tag{8.183}
\end{equation*}
$$

Transistor $Q_{8}$ functions as an active load for $Q_{12}$, and, since the collector currents in these two devices are nominally equal, the input offset voltage for the differential pair is nominally zero.

The current in output power transistor $Q_{15}$ depends on the load resistance but can go as high as 150 mA before a current-limit circuit (not shown) prevents further increase. Resistor $R_{12}$ provides bleed current so that $Q_{14}$ always has at least 0.04 mA of bias current, even when the current in $Q_{15}$ is low and/or its current gain is large.

In order to calculate the load regulation of the $723,(8.175)$ indicates that it is necessary to calculate the open-loop gain and output resistance of the regulator amplifier. For this purpose, a differential ac equivalent circuit of this amplifier is shown in Fig. 8.38. Load resistance $R_{L 12}$ is the output resistance presented by $Q_{8}$, which is

$$
\begin{equation*}
R_{L 12} \simeq r_{o 8}\left(1+g_{m 8} R_{5}\right) \tag{8.184}
\end{equation*}
$$

Assuming that the magnitude of the Early voltage of $Q_{8}$ is 100 V and $I_{C 8}=-174 \mu \mathrm{~A}$, we can calculate the value of $R_{L 12}$ as

$$
\begin{equation*}
R_{L 12}=\frac{100}{0.174}\left(1+\frac{0.174}{26} 1000\right) \mathrm{k} \Omega=4.42 \mathrm{M} \Omega \tag{8.185}
\end{equation*}
$$

image_name:Figure 8.38
description:
[
name: Q12, type: NPN, ports: {C: V1, B: Vi, E: GND}
name: Q14, type: NPN, ports: {C: GND, B: V1, E: e14b15}
name: Q15, type: NPN, ports: {C: GND, B: e14b15, E: Vo}
name: 1/gm11, type: Resistor, value: 1/gm11, ports: {N1: e12, N2: GND}
name: R12, type: Resistor, value: R12, ports: {N1: e14b15, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:This circuit is an AC equivalent of a regulator amplifier in a 723 voltage regulator. It includes transistors Q12, Q14, and Q15, which are NPN transistors, and resistors R12, RL12, and RL. The circuit regulates voltage by controlling the output through these components.

Figure 8.38 An ac equivalent circuit of the regulator amplifier of the 723 voltage regulator.

Since $g_{m 11}=g_{m 12}$, the impedance in the emitter of $Q_{12}$ halves the transconductance and gives an effective output resistance of

$$
\begin{equation*}
R_{o 12}=\left(1+g_{m 12} \frac{1}{g_{m 11}}\right) r_{o 12} \tag{8.186}
\end{equation*}
$$

where $r_{o 12}$ is the output resistance of $Q_{12}$ alone and is $575 \mathrm{k} \Omega$ if the Early voltage is 100 V .
Thus

$$
\begin{equation*}
R_{o 12}=1.15 \mathrm{M} \Omega \tag{8.187}
\end{equation*}
$$

The external load resistance $R_{L}$ determines the load current and thus the bias currents in $Q_{14}$ and $Q_{15}$. However, $R_{L}$ is not included in the small-signal calculation of output resistance because this quantity is the resistance seen by $R_{L}$ looking back into the circuit. Thus, for purposes of calculating the ac output resistance, $R_{L}$ may be assumed infinite and the output Darlington pair then produces no loading at the collector of $Q_{12}$. The voltage gain of the circuit may then be calculated as

$$
\begin{align*}
a=\left|\frac{v_{o}}{v_{i}}\right|=\left|\frac{v_{1}}{v_{i}}\right| & =\frac{g_{m 12}}{2}\left(R_{o 12} \| R_{L 12}\right) \\
& =\frac{0.174}{26} \frac{1}{2}(1.15 \| 4.42) \times 10^{6} \\
& =3054 \tag{8.188}
\end{align*}
$$

The output resistance $r_{o a}$ of the circuit of Fig. 8.38 is the output resistance of a Darlington emitter follower. If $R_{12}$ is assumed large compared with $r_{\pi 15}$ then

$$
\begin{equation*}
r_{o a}=\frac{1}{g_{m 15}}+\frac{1}{\beta_{0(15)}}\left(\frac{1}{g_{m 14}}+\frac{R_{S}}{\beta_{0(14)}}\right) \tag{8.189}
\end{equation*}
$$

where

$$
\begin{equation*}
R_{S}=R_{o 12} \| R_{L 12}=913 \mathrm{k} \Omega \tag{8.190}
\end{equation*}
$$

If we assume collector bias currents of 20 mA in $Q_{15}$ and 0.5 mA in $Q_{14}$ together with $\beta_{0(15)}=\beta_{0(14)}=100$, then substitution in (8.189) gives

$$
\begin{align*}
r_{o a} & =\left[1.3+\frac{1}{100}\left(52+\frac{913,000}{100}\right)\right] \Omega \\
& =(1.3+92) \Omega \\
& =93 \Omega \tag{8.191}
\end{align*}
$$

Substituting for $r_{o a}$ and $a$ in (8.175) and using $V_{R}=6.8 \mathrm{~V}$, we obtain, for the load regulation,

$$
\begin{align*}
\frac{\Delta V_{O}}{V_{O}} & =\frac{93}{3054 \times 6.8} \Delta I_{O} \\
& =4.5 \times 10^{-3} \Delta I_{O} \tag{8.192}
\end{align*}
$$

where $\Delta I_{O}$ is in Amps.
If $\Delta I_{O}$ is 50 mA , then (8.192) gives

$$
\begin{equation*}
\frac{\Delta V_{O}}{V_{O}}=2 \times 10^{-4}=0.02 \text { percent } \tag{8.193}
\end{equation*}
$$

This answer is close to the value of 0.03 percent given on the specification sheet. Note the extremely small percentage change in output voltage for a $50-\mathrm{mA}$ change in load current.

## 8.8 Feedback Circuit Analysis Using Return Ratio

The feedback analysis presented so far has used two-ports to manipulate a feedback circuit into unilateral forward amplifier and feedback networks. Since real feedback circuits have bilateral feedback networks and possibly bilateral amplifiers, some work is required to find the amplifier $a$ and feedback $f$ networks. The correct input and output variables and the type of feedback must be identified, and the correct two-port representation $(y, z, h$, or $g$ ) must be used. After this work, the correspondence between the original circuit and modified two-ports is small, which can make these techniques difficult to use.

Alternatively, a feedback circuit can be analyzed in a way that does not use two-ports. This alternative analysis, which is often easier than two-port analysis, is called return-ratio analysis. ${ }^{5,6,7}$ Here, the closed-loop properties of a feedback circuit are described in terms of the return ratio for a dependent source in the small-signal model of an active device. The return ratio for a dependent source in a feedback loop is found by the following procedure:

1. Set all independent sources to zero.
2. Disconnect the dependent source from the rest of the circuit, which introduces a break in the feedback loop.
3. On the side of the break that is not connected to the dependent source, connect an independent test source $s_{t}$ of the same sign and type as the dependent source.
4. Find the return signal $s_{r}$ generated by the dependent source.

Then the return ratio ( $\mathscr{R}$ ) for the dependent source is $\mathscr{R}=-s_{r} / s_{t}$, where the variable $s$ represents either a current or a voltage.

Figure 8.39a shows a negative feedback amplifier that includes a dependent voltage source. Figure $8.39 b$ shows how the circuit is modified to find the return ratio. The dependent source is disconnected from the rest of the circuit by breaking the connections at the two X's marked in Fig. 8.39a. A test signal $v_{t}$ is connected on the side of the break that is not connected to the controlled source. The return signal $v_{r}$ is measured at the open circuit across the controlled source to find the return ratio $\mathscr{R}=-v_{r} / v_{t}$.
image_name:Figure 8.39a
description:
[
name: VS, type: VoltageSource, value: VS, ports: {Np: VS, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: VS, N2: VX}
name: RI, type: Resistor, value: RI, ports: {N1: VX, N2: GND}
name: RF, type: Resistor, value: RF, ports: {N1: VX, N2: VOP}
name: RO, type: Resistor, value: RO, ports: {N1: VOP, N2: x}
name: Av, type: VoltageControlledVoltageSource, value: -avVx, ports: {Np: x, Nn: x}
name: OpAmp, type: OpAmp, ports: {InP: VX, InN: GND, OutP: VOP, OutN: VON}
]
extrainfo:The circuit is a feedback amplifier with an inverting voltage gain. The dependent voltage source is controlled by the voltage across RI. The return ratio is determined by breaking the loop at the dependent source and injecting a test signal.
image_name:Figure 8.39b
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vs, N2: Vx}
name: RF, type: Resistor, value: RF, ports: {N1: Vx, N2: Vo}
name: ri, type: Resistor, value: ri, ports: {N1: Vx, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: Vt}
name: -av*vx, type: VoltageControlledVoltageSource, value: -av*vx, ports: {Np: Vr, Nn: GND}
]
extrainfo:The circuit is used to find the return ratio by breaking the loop at the dependent voltage source and inserting a test signal Vt. The return signal Vr is measured to calculate the return ratio R = -Vr/Vt. The resistors form a voltage divider network.

Figure 8.39 (a) A feedback circuit that gives an inverting voltage gain. The " $X$ " marks indicate where the loop will be broken. (b) The circuit in $(a)$ modified to find the return ratio for the dependent voltage source.

#### EXAMPLE

Find the return ratio for the circuit in Fig. 8.39b.
The return ratio can be found with little computation because the resistors form a voltage divider

$$
\begin{equation*}
v_{x}=\frac{R_{S} \| r_{i}}{R_{S} \| r_{i}+R_{F}+r_{o}} v_{t} \tag{8.194}
\end{equation*}
$$

The return voltage $v_{r}$ is

$$
\begin{equation*}
v_{r}=-a_{v} v_{x} \tag{8.195}
\end{equation*}
$$

Combining these equations gives

$$
\begin{equation*}
\mathscr{R}=-\frac{v_{r}}{v_{t}}=\frac{R_{S} \| r_{i}}{R_{S} \| r_{i}+R_{F}+r_{o}} a_{v} \tag{8.196}
\end{equation*}
$$

Figure $8.40 a$ is a single-stage feedback circuit. Its small-signal model shown in Fig. 8.40b includes a dependent current source. Figure 8.40 c illustrates how the return ratio is found in this case. Here, the dependent source is disconnected from the rest of the circuit, and a test current source $i_{t}$ is connected on the side of the break that is not connected to the dependent source. A short circuit is applied across the dependent current source to provide a path for the return current $i_{r}$ to flow. The return ratio is computed as $\mathscr{R}=-i_{r} / i_{t}$.

image_name:Figure 8.40 (a)
description:
[
name: Q1, type: NPN, ports: {C: Vout, B: b1, E: GND}
name: RF, type: Resistor, value: 20 kΩ, ports: {N1: b1, N2: Vout}
name: RC, type: Resistor, value: 10 kΩ, ports: {N1: VDD, N2: Vout}
name: iin, type: CurrentSource, ports: {Np: b1, Nn: GND}
]
extrainfo:The circuit is a transresistance feedback amplifier with a feedback resistor RF and a collector resistor RC. The transistor Q1 is used to amplify the input current iin, and the output voltage is taken across the resistor RC. The dependent current source gmvbe is controlled by the voltage across the base-emitter junction of Q1.
image_name:Figure 8.40 (b)
description:
[
'name': 'RF', 'type': 'Resistor', 'value': '20 kΩ', 'ports': {'N1': 'Vbe', 'N2': 'Vo'
'name': 'RC', 'type': 'Resistor', 'value': 'Rc', 'ports': {'N1': 'V0', 'N2': 'Vo'
'name': 'rπ', 'type': 'Resistor', 'value': '5 kΩ', 'ports': {'N1': 'Vbe', 'N2': 'GND'
'name': 'ro', 'type': 'Resistor', 'value': '1 MΩ', 'ports': {'N1': 'Vo', 'N2': 'GND'
'name': 'gmvbe', 'type': 'CurrentControlledCurrentSource', 'value': '40 mA/V', 'ports': {'Np': 'Vout', 'Nn': GND
'name': 'iin', 'type': 'CurrentSource', 'ports': {'Np': 'Vbe', 'Nn': 'GND'
]
extrainfo:The circuit in Figure 8.40 (b) is a small-signal model of a transresistance feedback amplifier. It includes a dependent current source represented by gm*vbe and several resistors to model the transistor's internal resistances. The circuit is used to analyze the feedback and gain characteristics of the amplifier.
image_name:Figure 8.40 (c)
description:
[
name: RF, type: Resistor, value: 20kΩ, ports: {N1: Vbe, N2: Vo}
name: RC, type: Resistor, value: 10kΩ, ports: {N1: Vo, N2: GND}
name: rπ, type: Resistor, value: 5kΩ, ports: {N1: Vbe, N2: GND}
name: ro, type: Resistor, value: 1MΩ, ports: {N1: Vo, N2: GND}
name: gm, type: VoltageControlledCurrentSource, value: 40mA/V, ports: {Np: 0, Nn: 0}
name: it, type: CurrentSource, ports: {Np: Vo, Nn: GND}
]
extrainfo:The circuit is a transresistance feedback amplifier with a dependent current source. The return ratio is calculated by disconnecting the dependent source and inserting a test current source. The circuit includes resistors, a dependent voltage-controlled current source, and current sources for analysis.

Figure 8.40 (a) A transresistance feedback circuit. (b) The small-signal model for the circuit in (a). The " $X$ " marks indicate where the loop will be broken. (c) The circuit in (b) modified to find the return ratio for the dependent current source.

### 8.8.1 Closed-Loop Gain Using Return Ratio

A formula for the closed-loop gain of a feedback amplifier in terms of the return ratio will now be derived. Consider a feedback amplifier as shown in Fig. 8.41. The feedback amplifier consists of linear elements: passive components, controlled sources, and transistor small-signal models. A controlled source with value $k$ that is part of the small-signal model of an active device is shown explicitly. The output of the controlled source is $s_{o c}$, and the controlling signal is $s_{i c}$. The equation that describes the controlled source is

$$
\begin{equation*}
s_{o c}=k s_{i c} \tag{8.197}
\end{equation*}
$$

image_name:Figure 8.41
description:The circuit is a linear feedback amplifier with controlled sources. The input signal is 's_in', and the output signal is 's_out'. The controlled source has an output 's_oc' and is controlled by 's_ic' with a gain factor 'k'. The feedback loop is part of the 'Rest of feedback amplifier' block.

Figure 8.41 Linear feedback amplifier used to derive the closed-loop gain formula.
(For example, the output of the controlled source in Fig. 8.40b is $s_{o c}=g_{m} v_{b e}$; the controlling signal is $s_{i c}=v_{b e}$, and the value of the controlled source is $k=g_{m}$.) Each signal $s$ in the figure is labeled as if it is a voltage, but each signal could be either a current or a voltage. Because the feedback amplifier is linear, signals $s_{i c}$ and $s_{\text {out }}$ can be expressed as linear functions of the outputs of the two sources, $s_{o c}$ and $s_{\text {in }}$,

$$
\begin{align*}
& s_{i c}=B_{1} s_{\mathrm{in}}-H s_{o c}  \tag{8.198}\\
& s_{\text {out }}=d s_{\mathrm{in}}+B_{2} s_{o c} \tag{8.199}
\end{align*}
$$

The terms $B_{1}, B_{2}$, and $H$ in (8.198) and (8.199) are defined by

$$
\begin{align*}
& B_{1}=\left.\frac{s_{i c}}{s_{\text {in }}}\right|_{s_{o c}=0}=\left.\frac{s_{i c}}{s_{\text {in }}}\right|_{k=0}  \tag{8.200a}\\
& B_{2}=\left.\frac{s_{\text {out }}}{s_{o c}}\right|_{s_{\text {in }}=0}  \tag{8.200b}\\
& H=-\left.\frac{s_{i c}}{s_{o c}}\right|_{s_{\text {in }}=0} \tag{8.200c}
\end{align*}
$$

So $B_{1}$ is the transfer function from the input to the controlling signal evaluated with $k=0$, $B_{2}$ is the transfer function from the dependent source to the output evaluated with the input source set to zero, and $H$ is the transfer function from the output of the dependent source to the controlling signal evaluated with the input source set to zero, times -1 .

Also, the direct feedthrough $d$ is given by

$$
\begin{equation*}
d=\left.\frac{s_{\mathrm{out}}}{s_{\mathrm{in}}}\right|_{s_{o c}=0}=\left.\frac{s_{\mathrm{out}}}{s_{\mathrm{in}}}\right|_{k=0} \tag{8.200d}
\end{equation*}
$$

which is the transfer function from the input to the output evaluated with $k=0$. The calculation of $d$ usually involves signal transfer through passive components that provide a signal path directly from the input to output, a path that goes around rather than through the controlled source $k$.

Equations 8.197 , 8.198, and 8.199 can be solved for the closed-loop gain. Substituting (8.197) in (8.198) and rearranging gives

$$
\begin{equation*}
s_{i c}=\frac{B_{1}}{1+k H} s_{i n} \tag{8.201}
\end{equation*}
$$

Substituting (8.197) in (8.199), then substituting (8.201) in the resulting equation and rearranging terms gives the closed-loop gain $A$

$$
\begin{equation*}
A=\frac{s_{\text {out }}}{s_{\text {in }}}=\frac{B_{1} k B_{2}}{1+k H}+d \tag{8.202}
\end{equation*}
$$

The term $k H$ in the denominator is equal to the return ratio, as will be shown next. The return ratio is found by setting $s_{\mathrm{in}}=0$, disconnecting the dependent source from the circuit, and connecting a test source $s_{t}$ where the dependent source was connected. After these changes, $s_{o c}=s_{t}$ and (8.198) becomes

$$
\begin{equation*}
s_{i c}=-H s_{t} \tag{8.203}
\end{equation*}
$$

Then the output of the dependent source is the return signal $s_{r}=k s_{i c}=-k H s_{t}$. Therefore

$$
\begin{equation*}
\mathscr{R}=-\frac{s_{r}}{s_{t}}=k H \tag{8.204}
\end{equation*}
$$

So the closed-loop gain in (8.202) can be rewritten as

$$
\begin{equation*}
A=\frac{s_{\text {out }}}{s_{\text {in }}}=\frac{B_{1} k B_{2}}{1+\mathscr{R}}+d \tag{8.205a}
\end{equation*}
$$

or

$$
\begin{equation*}
A=\frac{s_{\text {out }}}{s_{\text {in }}}=\frac{g}{1+\mathscr{R}}+d \tag{8.205b}
\end{equation*}
$$

where

$$
\begin{equation*}
g=B_{1} k B_{2} \tag{8.206}
\end{equation*}
$$

Here $g$ is the gain from $s_{\text {in }}$ to $s_{\text {out }}$ if $H=0$ and $d=0$, and $d$ is the direct signal feedthrough, which is the value of $A$ when the controlled source is set to zero $(k=0)$.

The closed-loop gain formula in (8.205a) requires calculations of four terms: $B_{1}, B_{2}, d$, and $\mathscr{R}$. That equation can be manipulated into a more convenient form with only three terms. Combining terms in (8.205b) using a common denominator $1+\mathscr{R}$ gives

$$
\begin{equation*}
A=\frac{g+d(1+\mathscr{R})}{1+\mathscr{R}}=\frac{g+d \mathscr{R}}{1+\mathscr{R}}+\frac{d}{1+\mathscr{R}}=\frac{\left(\frac{g}{\mathscr{R}}+d\right) \mathscr{R}}{1+\mathscr{R}}+\frac{d}{1+\mathscr{R}} \tag{8.207}
\end{equation*}
$$

Defining

$$
\begin{equation*}
A_{\infty}=\frac{g}{\mathscr{R}}+d \tag{8.208}
\end{equation*}
$$

allows (8.207) to be rewritten as

$$
\begin{equation*}
A=A_{\infty} \frac{\mathscr{R}}{1+\mathscr{R}}+\frac{d}{1+\mathscr{R}} \tag{8.209}
\end{equation*}
$$

This is a useful expression for the closed-loop gain. Here, if $\mathscr{R} \rightarrow \infty$, then $A=A_{\infty}$ because $\mathscr{R} /(1+\mathscr{R}) \rightarrow 1$ and $d /(1+\mathscr{R}) \rightarrow 0$. So $A_{\infty}$ is the closed-loop gain when the feedback circuit is ideal (that is, when $\mathscr{R} \rightarrow \infty$ ).

A block-diagram representation of (8.209) is shown in Fig. 8.42. The gain around the feedback loop is $\mathscr{R}$, and the effective forward gain in the loop is $\mathscr{R} A_{\infty}$. A key difference between the two-port and return-ratio analyses can be seen by comparing Figs. 8.1 and 8.42. In the two-port analysis, all forward signal transfer through the amplifier and the feedback network is lumped into $a$. In the return-ratio analysis, there are two forward signal paths: one
image_name:Figure 8.42
description:Figure 8.42 illustrates a block diagram representing the closed-loop gain formula described in equation (8.209). The main components of the diagram include:

1. **Input (s_in):** This is the starting point where the input signal enters the system.

2. **Summation Junction (Σ):** The input signal (s_in) is combined with a feedback signal at this point. The feedback signal is subtracted from the input, indicating a negative feedback loop.

3. **Feedforward Path (d):** The signal from the summation junction is split into two paths. One path goes through a block labeled 'd', representing a direct feedforward path through the feedback network.

4. **Amplifier Block (b = ℜA_∞):** The other path from the summation junction enters an amplifier block with the gain represented as 'b = ℜA_∞'. This block signifies the effective forward gain in the loop.

5. **Second Summation Junction (Σ):** The outputs from the feedforward path (d) and the amplifier block (b = ℜA_∞) are combined at this junction. The summation here involves adding the two signals.

6. **Output (s_out):** The combined signal from the second summation junction is directed to the output of the system.

7. **Feedback Path (1/A_∞):** A portion of the output signal is fed back into the system through a block labeled '1/A_∞'. This block represents the passive feedback network, which is typically determined by a factor 'f' in two-port analysis.

**Flow of Information:**
- The input signal (s_in) is initially combined with the feedback signal at the first summation junction.
- The resultant signal is split into two paths: one through the feedforward block 'd' and the other through the amplifier block 'b = ℜA_∞'.
- The outputs from these paths are summed at the second summation junction to form the system's output (s_out).
- Part of the output is fed back through the feedback path (1/A_∞) to the first summation junction, completing the feedback loop.

**Overall System Function:**
- The system is designed to achieve closed-loop gain as specified by the formula in equation (8.209). The combination of feedforward and feedback paths, along with the effective forward gain, ensures the desired signal processing and stability within the loop. The feedback mechanism helps control the gain and maintain system stability.

Figure 8.42 A block diagram for the closed-loop gain formula in (8.209).
path $(d)$ for the feedforward through the feedback network and another path $\left(\mathscr{R} A_{\infty}\right)$ for the effective forward gain.

Typically, $A_{\infty}$ is determined by a passive feedback network and is equal to $1 / f$ from twoport analysis. The value of $A_{\infty}$ can be found readily since $A_{\infty}=A$ when $k \rightarrow \infty$. Letting $k \rightarrow \infty$ causes $\mathscr{R}=k H \rightarrow \infty$. (Here we assumed $k>0$. If $k<0$ in a negative feedback circuit, then $\mathscr{R} \rightarrow \infty$ when $k \rightarrow-\infty$.) When $k \rightarrow \infty$, the controlling signal $s_{i c}$ for the dependent source must be zero if the output of the dependent source is finite. The controlled source output will be finite if the feedback is negative. These facts can be used to find $A_{\infty}$ with little computation in many circuits, as is demonstrated in the next example.

#### EXAMPLE

Compute the closed-loop gain for the circuit of Fig. 8.40 using (8.209). Use the component values given in the figure.

To use (8.209), $A_{\infty}, \mathscr{R}$, and $d$ are needed. Here, the only controlled source is the $g_{m}$ source, so $k=g_{m}$. Also, $s_{\text {in }}=i_{\text {in }}, s_{\text {out }}=v_{o}$, and $s_{i c}=v_{b e}$. To find $A_{\infty}$, let $g_{m} \rightarrow \infty$, which forces the controlling voltage $v_{b e}$ to equal zero, assuming that the output current from the $g_{m}$ generator is finite. With $v_{b e}=0$, no current flows through $r_{\pi}$, and therefore the input current $i_{\text {in }}$ flows through $R_{F}$ to produce $v_{o}$. Thus

$$
\begin{equation*}
A_{\infty}=\left.\frac{v_{o}}{i_{\mathrm{in}}}\right|_{g_{m}=\infty}=-R_{F}=-20 \mathrm{k} \Omega \tag{8.210}
\end{equation*}
$$

Next, $d$ is found by setting $k=g_{m}=0$ and computing the transfer function from input to output

$$
\begin{align*}
d=\left.\frac{v_{o}}{i_{\mathrm{in}}}\right|_{g_{m}=0} & =\left(r_{o} \| R_{C}\right) \cdot \frac{r_{\pi}}{r_{\pi}+R_{F}+r_{o} \| R_{C}} \\
& =(1 \mathrm{M} \Omega \| 10 \mathrm{k} \Omega) \cdot \frac{5 \mathrm{k} \Omega}{5 \mathrm{k} \Omega+10 \mathrm{k} \Omega+1 \mathrm{M} \Omega \| 100 \mathrm{k} \Omega}  \tag{8.211}\\
& =1.4 \mathrm{k} \Omega
\end{align*}
$$

Finally, the return ratio for the $g_{m}$ generator can be calculated using Fig. 8.40c. Applying a current-divider formula gives the current $i_{\pi}$ through $r_{\pi}$ as

$$
\begin{equation*}
i_{\pi}=-\frac{r_{o} \| R_{C}}{r_{o} \| R_{C}+R_{F}+r_{\pi}} i_{t} \tag{8.212}
\end{equation*}
$$

The return current is

$$
\begin{equation*}
i_{r}=g_{m} v_{b e}=g_{m} r_{\pi} i_{\pi} \tag{8.213}
\end{equation*}
$$

Combining these equations gives

$$
\begin{align*}
\mathscr{R} & =-\frac{i_{r}}{i_{t}}=g_{m} r_{\pi} \cdot \frac{r_{o} \| R_{C}}{r_{o} \| R_{C}+R_{F}+r_{\pi}}  \tag{8.214}\\
& =(40 \mathrm{~mA} / \mathrm{V}) \cdot 5 \mathrm{k} \Omega \cdot \frac{1 \mathrm{M} \Omega \| 10 \mathrm{k} \Omega}{1 \mathrm{M} \Omega \| 10 \mathrm{k} \Omega+20 \mathrm{k} \Omega+5 \mathrm{k} \Omega}=56.7 \tag{8.215}
\end{align*}
$$

Then, using (8.209),

$$
\begin{equation*}
A=A_{\infty} \frac{\mathscr{R}}{1+\mathscr{R}}+\frac{d}{1+\mathscr{R}}=-20 \mathrm{k} \Omega \frac{56.7}{1+56.7}+\frac{1.4 \mathrm{k} \Omega}{1+56.7}=-19.6 \mathrm{k} \Omega \tag{8.216}
\end{equation*}
$$

In (8.209), the second term that includes $d$ can be neglected whenever $|d| \ll\left|A_{\infty} \mathscr{R}\right|$. This condition usually holds at low frequencies because $d$ is the forward signal transfer through a passive network, while $\left|A_{\infty} \mathscr{R}\right|$ is large because it includes the gain through the active device(s). For example, ignoring the $d /(1+\mathscr{R})$ term in (8.216) gives $A \approx-19.7 \mathrm{k} \Omega$, which is close to the exact value. As the frequency increases, however, the gain provided by the transistors falls. As a result, $d$ may become significant at high frequencies.

The effective forward gain $A_{\infty} \mathscr{R}$ can be computed after $A_{\infty}$ and $\mathscr{R}$ have been found. Alternatively, this effective forward gain can be found directly from the feedback circuit. ${ }^{8}$ Call this forward gain $b$, so

$$
\begin{equation*}
b=A_{\infty} \cdot \mathscr{R} \tag{8.217}
\end{equation*}
$$

Then the closed-loop gain in (8.209) can be written as

$$
\begin{equation*}
A=\frac{b}{1+\mathscr{R}}+\frac{d}{1+\mathscr{R}} \tag{8.218}
\end{equation*}
$$

Using (8.206), (8.208), and $\mathscr{R}=k H, b$ can be expressed as

$$
\begin{align*}
b=A_{\infty} \cdot \mathscr{R} & =\left(\frac{g}{\mathscr{R}}+d\right) \cdot \mathscr{R}=\left(B_{1} k B_{2}+d \mathscr{R}\right) \\
& =\left(B_{1} k B_{2}+d k H\right)=\left[B_{1}+\frac{d H}{B_{2}}\right] k B_{2} \tag{8.219}
\end{align*}
$$

This final expression breaks $b$ into parts that can be found by analyzing the feedback circuit. In (8.200b), $B_{2}$ is defined as the transfer function from the output of the controlled source $s_{o c}$ to $s_{\text {out }}$ evaluated with $s_{\text {in }}=0$. The term in brackets in (8.219) is equal to the transfer function from $s_{\text {in }}$ to $s_{i c}$ when $s_{\text {out }}=0$, as will be shown next.

If $s_{\text {out }}=0$, then (8.199) simplifies to

$$
\begin{equation*}
B_{2} s_{o c}=-d s_{\mathrm{in}} \tag{8.220}
\end{equation*}
$$

Substituting (8.220) into (8.198) gives

$$
\begin{equation*}
s_{i c}=B_{1} s_{\mathrm{in}}+\frac{d H}{B_{2}} s_{\mathrm{in}} \tag{8.221}
\end{equation*}
$$

Therefore

$$
\begin{equation*}
\left.\frac{s_{i c}}{s_{\text {in }}}\right|_{s_{\text {out }}=0}=B_{1}+\frac{d H}{B_{2}} \tag{8.222}
\end{equation*}
$$

image_name:(a)
description:
[
name: i_in, type: CurrentSource, value: i_in, ports: {Np: GND, Nn: X1}
name: R_F, type: Resistor, value: R_F, ports: {N1: X1, N2: GND}
name: r_π, type: Resistor, value: r_π, ports: {N1: X1, N2: GND}
]
extrainfo:The circuit includes a current source i_in connected to node X1 and ground. A resistor R_F is connected between node X1 and ground. Another resistor r_π is also connected between node X1 and ground. The output voltage Vo is 0, indicating a grounded output.

image_name:(b)
description:
[
name: RF, type: Resistor, value: RF, ports: {N1: Vbe, N2: Vo}
name: rπ, type: Resistor, value: rπ, ports: {N1: Vbe, N2: GND}
name: ioc, type: CurrentSource, ports: {Np: Vo, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: Vo, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit includes a voltage input vbe connected across rπ and ground. The current source ioc is connected between Vo and ground. Resistors ro and RC are also connected between Vo and ground. RF connects Vbe and Vo.
Figure 8.43 Circuits for finding the effective forward gain $b$. (a) The circuit for the input side. (b) The circuit for the output side.
which is the expression in brackets in (8.219). Substituting (8.222) and (8.200b) into (8.219) gives

$$
\begin{equation*}
b=\left.\left.\frac{s_{i c}}{s_{\text {in }}}\right|_{s_{\text {out }}=0} \cdot k \cdot \frac{s_{\text {out }}}{s_{o c}}\right|_{s_{\text {in }}=0} \tag{8.223}
\end{equation*}
$$

The effective forward gain $b$ can be found using this formula.

#### EXAMPLE

Compute the effective forward gain $b=A_{\infty} \mathscr{R}$ for the circuit in Fig. 8.40.
As in the previous example, $k=g_{m}, s_{\text {in }}=i_{\text {in }}, s_{\text {out }}=v_{o}, s_{i c}=v_{b e}$, and $s_{o c}=i_{o c}=g_{m} v_{b e}$. To compute the first term in (8.223), the output $v_{o}$ must be set to zero by shorting the output to ground. The resulting circuit is shown in Fig. 8.43a. The calculation gives

$$
\begin{equation*}
\left.\frac{s_{i c}}{s_{\mathrm{in}}}\right|_{s_{\mathrm{out}}=0}=\left.\frac{v_{b e}}{i_{\mathrm{in}}}\right|_{v_{o}=0}=r_{\pi}\left\|R_{F}=5 \mathrm{k} \Omega\right\| 20 \mathrm{k} \Omega=4.0 \mathrm{k} \Omega \tag{8.224}
\end{equation*}
$$

The last term in (8.223) is found by setting the input $i_{\text {in }}$ to zero. This input current can be set to zero by replacing the source $i_{\text {in }}$ with an open circuit, as shown in Fig. 8.43b. Treating the $g_{m}$ generator as an independent source with value $i_{o c}$ for this calculation, the result is

$$
\begin{align*}
\left.\frac{s_{\text {out }}}{s_{o c}}\right|_{s_{\text {in }}=0} & =\left.\frac{v_{o}}{i_{o c}}\right|_{i_{\text {in }}=0}=-\left[r_{o}\left\|R_{c}\right\|\left(R_{F}+r_{\pi}\right)\right] \\
& =-[1 \mathrm{M} \Omega\|10 \mathrm{k} \Omega\|(20 \mathrm{k} \Omega+5 \mathrm{k} \Omega)]=-7.09 \mathrm{k} \Omega \tag{8.225}
\end{align*}
$$

Substituting (8.224) and (8.225) into (8.223) gives

$$
b=4.0 \mathrm{k} \Omega\left(g_{m}\right)(-7.09 \mathrm{k} \Omega)=4.0 \mathrm{k} \Omega(40 \mathrm{~mA} / \mathrm{V})(-7.09 \mathrm{k} \Omega)=-1134 \mathrm{k} \Omega
$$

For comparison, we can find $b$ using (8.217) and the values of $A_{\infty}$ and $\mathscr{R}$ computed in the previous example:

$$
b=A_{\infty} \mathscr{R}=-20 \mathrm{k} \Omega(56.7)=-1134 \mathrm{k} \Omega
$$

Both calculations give the same value for the effective forward gain $b$.

### 8.8.2 Closed-Loop Impedance Formula Using Return Ratio

Feedback affects the input and output impedance of a circuit. In this section, a useful expression for the impedance at any port in a feedback circuit in terms of return ratio ${ }^{9}$ is derived. Consider the feedback circuit shown in Fig. 8.44. This feedback amplifier consists of linear elements: passive components, controlled sources, and transistor small-signal models. A controlled source $k$ that is part of the small-signal model of an active device is shown explicitly. The derivation is carried out for the impedance $Z_{\text {port }}$ looking into an arbitrary port that is labeled as port $X$ in Fig. 8.44a. The port impedance can be found by driving the port by an independent current source as shown in Fig. $8.44 b$ and computing $Z_{\text {port }}=v_{x} / i_{x}$. Since the circuit in Fig. 8.44b is linear, the signals $s_{i c}$ and $v_{x}$ are linear functions of the signals $i_{x}$ and $s_{y}$ applied to the ports labeled X and Y . Therefore, we can write

$$
\begin{align*}
& v_{x}=a_{1} i_{x}+a_{2} s_{y}  \tag{8.226}\\
& s_{i c}=a_{3} i_{x}+a_{4} s_{y} \tag{8.227}
\end{align*}
$$

From (8.226), the impedance looking into the port when $k=0$ is

$$
\begin{equation*}
Z_{\text {port }}(k=0)=\left.\frac{v_{x}}{i_{x}}\right|_{k=0}=\left.\frac{v_{x}}{i_{x}}\right|_{s_{y}=0}=a_{1} \tag{8.228}
\end{equation*}
$$

Next we compute two return ratios for the controlled source $k$ under different conditions. Both are used in the final formula for the closed-loop impedance. The first return ratio is found
image_name:(a)
description:The circuit diagram (a) shows a linear feedback amplifier with a voltage-controlled voltage source ksic connected across Port Y. Port X is connected to a resistor Zport and a current source i. The circuit is used to derive Blackman's impedance formula.
image_name:(b)
description:The circuit diagram (b) shows a feedback amplifier with a current source i connected at Port X, and a voltage-controlled voltage source kSic connected at Port Y. Port X is driven by the current source i, and Port Y is part of the feedback loop.

Figure 8.44 (a) The linear feedback circuit used to derive Blackman's impedance formula with respect to port X . (b) The circuit with port X driven by an independent current source.
with the port open. With port X open, $i_{x}=0$. The return ratio is found by disconnecting the controlled source from the circuit and connecting a test source $s_{t}$ where the dependent source was connected. With these changes to the circuit, $s_{y}=s_{t}$ and (8.227) becomes

$$
\begin{equation*}
s_{i c}=a_{4} s_{t} \tag{8.229}
\end{equation*}
$$

The output of the controlled source is the return signal

$$
\begin{equation*}
s_{r}=k s_{i c} \tag{8.230}
\end{equation*}
$$

From the last two equations, we find

$$
\begin{equation*}
\mathscr{R}(\text { port open })=-\frac{s_{r}}{s_{t}}=-k a_{4} \tag{8.231}
\end{equation*}
$$

The other return ratio is found with the port shorted. With port X shorted, the voltage $v_{x}$ is zero. To find the return ratio, we disconnect the controlled source and connect test source $s_{t}$ where the dependent source was connected. With these changes, (8.226) gives

$$
\begin{equation*}
i_{x}=-\frac{a_{2}}{a_{1}} s_{t} \tag{8.232}
\end{equation*}
$$

Substituting (8.232) into (8.227), using $s_{y}=s_{t}$, and rearranging terms gives

$$
\begin{equation*}
s_{i c}=\left(a_{4}-\frac{a_{2} a_{3}}{a_{1}}\right) s_{t} \tag{8.233}
\end{equation*}
$$

The return signal is

$$
\begin{equation*}
s_{r}=k s_{i c} \tag{8.234}
\end{equation*}
$$

Combining these last two equations gives the return ratio with the port shorted

$$
\begin{equation*}
\mathscr{R}(\text { port shorted })=-\frac{s_{r}}{s_{t}}=-k\left(a_{4}-\frac{a_{2} a_{3}}{a_{1}}\right) \tag{8.235}
\end{equation*}
$$

Shortly, we will see that (8.228), (8.231), and (8.235) can be combined to give a useful formula for the port impedance.

To complete the derivation, we find the impedance looking into the port in Fig. 8.44b using

$$
\begin{equation*}
Z_{\mathrm{port}}=\frac{v_{x}}{i_{x}} \tag{8.236}
\end{equation*}
$$

Using (8.226), (8.227), and $s_{y}=k s_{i c}$, we get (after some manipulation)

$$
\begin{equation*}
Z_{\text {port }}=\frac{v_{x}}{i_{x}}=a_{1}\left(\frac{1-k\left(a_{4}-\frac{a_{2} a_{3}}{a_{1}}\right)}{1-k a_{4}}\right) \tag{8.237}
\end{equation*}
$$

Substituting (8.228), (8.231), and (8.235) into (8.237) yields

$$
\begin{equation*}
Z_{\text {port }}=Z_{\text {port }}(k=0)\left[\frac{1+\mathscr{R}(\text { port shorted })}{1+\mathscr{R}(\text { port open })}\right] \tag{8.238}
\end{equation*}
$$

This expression is called Blackman's impedance formula. ${ }^{9}$ The two return ratios, with the port open and shorted, are computed with respect to the same controlled source $k$. Equation 8.238
can be used to compute the impedance at any port, including the input and output ports. A key advantage of this formula is that it applies to any feedback circuit, regardless of the type of feedback. Usually, one of the two return ratios in (8.238) is zero, and in those cases Blackman's formula shows that feedback either increases or decreases the impedance by a factor $(1+\mathscr{R})$.

#### EXAMPLE

Use Blackman's formula to find the output resistance for the feedback circuit in Fig. 8.40.
From Blackman's formula, the output resistance is given by

$$
\begin{equation*}
R_{\text {out }}=R_{\text {out }}\left(g_{m}=0\right)\left[\frac{1+\mathscr{R}(\text { output port shorted })}{1+\mathscr{R}(\text { output port open })}\right] \tag{8.239}
\end{equation*}
$$

Shorting the output port in Fig. $8.40 c$ causes $v_{b e}=0$ so $i_{r}=g_{m} v_{b e}=0$; therefore, $\mathscr{R}($ output port shorted $)=0$. The $\mathscr{R}$ (output port open) is the same return ratio that was computed in $(8.215)$, so $\mathscr{R}$ (output port open $)=56.7$. The only remaining value to be computed is the resistance at the output port when $g_{m}=0$ :

$$
\begin{align*}
R_{\mathrm{out}}\left(g_{m}=0\right) & =r_{0}\left\|R_{C}\right\|\left(R_{F}+r_{\pi}\right)=1 \mathrm{M} \Omega\|10 \mathrm{k} \Omega\|(20 \mathrm{k} \Omega+5 \mathrm{k} \Omega) \\
& =7.1 \mathrm{k} \Omega \tag{8.240}
\end{align*}
$$

Substituting into (8.239) yields

$$
\begin{equation*}
R_{\mathrm{out}}=7.1 \mathrm{k} \Omega\left[\frac{1+0}{1+56.7}\right]=120 \Omega \tag{8.241}
\end{equation*}
$$

The negative feedback reduces the output resistance, which is desirable because the output is a voltage, and a low output resistance is desired in series with a voltage source.

#### EXAMPLE

Find the output resistance for the MOS super-source follower shown in Fig. 8.45a. Ignore body effect here to simplify the analysis.

The super-source follower uses feedback to reduce the output impedance. Ideal current sources $I_{1}$ and $I_{2}$ bias the transistors and are shown rather than transistor current sources to simplify the circuit. With current source $I_{1}$ forcing the current in $M_{1}$ to be constant, $M_{2}$ provides the output current when driving a load. There is feedback from $v_{\text {out }}$ to $v_{g s 2}$ through $M_{1}$. The small-signal model for this circuit is shown in Fig. 8.45b. In this circuit, either $g_{m 1}$ or $g_{m 2}$ could be chosen as $k$. Here, we will use $k=g_{m 2}$. In all the following calculations, the input source $v_{\text {in }}$ is set to zero. First, the output resistance when $g_{m 2}=0$ is

$$
\begin{equation*}
R_{\text {out }}\left(g_{m 2}=0\right)=r_{o 2} \tag{8.242}
\end{equation*}
$$

This result may seem surprising at first, since the output is connected to the source of $M_{1}$, which is usually a low-impedance point. However, an ideal current source, which is a small-signal open circuit, is connected to the drain of $M_{1}$. Therefore the current in the $g_{m 1}$ generator flows only in $r_{o 1}$, so $M_{1}$ has no effect on the output resistance when $g_{m 2}=0$.

The return ratio for the $g_{m 2}$ source with the output port open is found to be

$$
\begin{equation*}
\mathscr{R}(\text { output open })=g_{m 2} r_{o 2}\left(1+g_{m 1} r_{o 1}\right) \tag{8.243}
\end{equation*}
$$

The return ratio with the output port shorted is

$$
\begin{equation*}
\mathscr{R}(\text { output shorted })=0 \tag{8.244}
\end{equation*}
$$

image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: Vout, D: d1g2, G: Vin}
name: M2, type: NMOS, ports: {S: GND, D: Vout, G: d1g2}
name: I1, type: CurrentSource, value: I1, ports: {Np: d1g2, Nn: GND}
name: I2, type: CurrentSource, value: I2, ports: {Np: VDD, Nn: Vout}
]
extrainfo:The circuit is a super-source-follower configuration with two NMOS transistors. M1 and M2 are connected in a configuration where M1's source is grounded, and its gate is driven by the input voltage Vin. M2's gate and drain are connected to the output node Vout, providing feedback. The circuit includes current sources I1 and I2, and resistors ro1 and ro2, with voltage-controlled current sources gm1V1 and gm2V2 representing the transconductance of the transistors.
image_name:(b)
description:
[
name: gm1V1, type: VoltageControlledCurrentSource, value: gm1V1, ports: {Np: V2, Nn: Vout}
name: ro1, type: Resistor, value: ro1, ports: {N1: Vout, N2: V2}
name: gm2V2, type: VoltageControlledCurrentSource, value: gm2V2, ports: {Np: Vout, Nn: GND}
name: ro2, type: Resistor, value: ro2, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit diagram (b) represents a small-signal model of a super-source-follower circuit. It consists of two NMOS transistors, M1 and M2, and two current sources, I1 and I2. The circuit also includes voltage-controlled current sources gm1V1 and gm2V2, and resistors ro1 and ro2. The output is labeled as Vout. The circuit is designed to analyze the return ratio and output resistance in different configurations.
Figure 8.45 (a) The super-source-follower circuit. (b) The circuit with each transistor replaced by its small-signal model.
because shorting the output port forces $v_{\text {out }}=0$ and $v_{1}=-v_{\text {out }}=0$. Hence no current flows in $M_{1}$, so $v_{2}=0$ and therefore the return ratio is zero. Substituting the last three equations into (8.238) gives the closed-loop output resistance

$$
\begin{equation*}
R_{\text {out }}=r_{o 2}\left[\frac{1+0}{1+g_{m 2} r_{o 2}\left(1+g_{m 1} r_{o 1}\right)}\right] \tag{8.245}
\end{equation*}
$$

Assuming $g_{m} r_{o} \gg 1$, then

$$
\begin{equation*}
R_{\mathrm{out}} \approx \frac{r_{o 2}}{g_{m 2} r_{o 2} g_{m 1} r_{o 1}}=\frac{1}{g_{m 2} g_{m 1} r_{o 1}} \tag{8.246}
\end{equation*}
$$

which is much lower than the output resistance of a conventional source follower, which is about $1 / g_{m}$. This result agrees with (3.137), which was derived without the use of feedback principles. Although $g_{m b 1}$ appears in (3.137), it does not appear in (8.246) because the body effect is ignored here.

The next example demonstrates an unusual case where neither return ratio vanishes in Blackman's impedance formula.

#### EXAMPLE

In the Wilson current source in Fig. 8.46a, assume that the three bipolar transistors are identical with $\beta_{0} \gg 1$ and are biased in the forward-active region. Find the output resistance.

Blackman's impedance formula can be used here because there is a feedback loop formed by the current mirror $Q_{1}-Q_{3}$ with $Q_{2}$. With all transistors forward active and $\beta_{F} \gg 1$,
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: X1, B: X1, E: GND}
name: Q2, type: NPN, ports: {C: LOAD, B: c3b2, E: X1}
name: Q3, type: NPN, ports: {C: c3b2, B: X1, E: GND}
name: I_REF, type: CurrentSource, value: I_REF, ports: {Np: VCC, Nn: C3b2}
]
extrainfo:The circuit is a Wilson current mirror, consisting of three NPN transistors Q1, Q2, and Q3. The transistors are biased in the forward-active region, and the circuit is designed to provide a high output resistance. The current mirror uses feedback through Q1 and Q3 to stabilize the output current, and the output is connected to a load at the collector of Q2. The capacitor C3b2 is connected between the reference current source I_REF and the node X1.
image_name:(b)
description:The circuit is a Wilson current mirror with three NPN transistors. It uses feedback to improve output resistance. The transistors are biased in the forward-active region with high beta. The output resistance is calculated using Blackman's impedance formula.
image_name:(c)
description:The circuit in (c) represents the small-signal model for calculating the output resistance of a Wilson current mirror. Transistors Q1, Q2, and Q3 form the current mirror, with feedback from Q2 to Q1 and Q3. The model includes resistors and controlled current sources to represent the transistors' small-signal behavior. The output resistance is analyzed at the output port Vo.
Figure 8.46 (a) The Wilson current mirror. (b) The circuit with each transistor replaced by its small-signal model. (c) The small-signal model modified for calculation of $\mathscr{R}$ for $g_{m 1}$.
$I_{C 1}=I_{C 2}=I_{C 3}=I_{R E F}$. (The output is connected to other circuitry that is not shown, so $I_{C 2}$ is nonzero.) The small-signal model is shown in Fig. 8.46b, where diode-connected $Q_{1}$ is modeled by a resistor of value $1 / g_{m 1}$. Resistor $r_{\pi 3}$, which is in parallel with $1 / g_{m 1}$, is ignored (since $r_{\pi 3}=\beta_{0} / g_{m 3}=\beta_{0} / g_{m 1} \gg 1 / g_{m 1}$ ). Also $r_{o 3}$ is ignored, assuming that it is much larger than the resistance looking into the base of $Q_{2}$. Selecting $k=g_{m 3}$ and calculating the first term in (8.238) gives

$$
\begin{equation*}
R_{\mathrm{out}}\left(g_{m 3}=0\right)=r_{o 2}+\frac{1}{g_{m 1}} \approx r_{o 2} \tag{8.247}
\end{equation*}
$$

since setting $g_{m 3}=0$ forces the current through $r_{\pi 2}$ to be zero. Therefore, the voltage across $r_{\pi 2}$ is zero, which causes the current through the $g_{m 2}$ source to be zero.

The return ratios in Blackman's formula can be found using the circuit shown in Fig. 8.46c. First, let us find $\mathscr{R}$ (output port open). When the output port is open, the current in the $g_{m 2}$ generator can only flow through the parallel resistor $r_{o 2}$, so the currents through $r_{\pi 2}$ and $1 / g_{m 1}$ are equal and are supplied by the test source $i_{t}$. Therefore,

$$
\begin{equation*}
v_{x}=-i_{t} \frac{1}{g_{m 1}} \tag{8.248}
\end{equation*}
$$

Also

$$
\begin{equation*}
i_{r}=g_{m 3} v_{x} \tag{8.249}
\end{equation*}
$$

Combining these two equations gives

$$
\begin{equation*}
\mathscr{R}(\text { output open })=-\frac{i_{r}}{i_{t}}=\frac{g_{m 3}}{g_{m 1}}=1 \tag{8.250}
\end{equation*}
$$

where $g_{m 1}=g_{m 3}$ because $I_{C 1}=I_{C 3}$.
When the output port is shorted, the current through the $g_{m 2}$ generator is not restricted to flow only through $r_{o 2}$. First, notice that with the output port shorted, $r_{o 2}$ is in parallel with $1 / g_{m 1}$, so $r_{o 2}$ can be ignored. With this simplification, the current through the resistance $1 / g_{m 1}$ is from the test and $g_{m 2}$ sources, so

$$
\begin{equation*}
v_{x}=\frac{1}{g_{m 1}}\left(-i_{t}+g_{m 2} v_{y}\right) \tag{8.251}
\end{equation*}
$$

Now

$$
\begin{equation*}
v_{y}=-i_{t} r_{\pi 2} \tag{8.252}
\end{equation*}
$$

Combining these two equations gives

$$
\begin{equation*}
v_{x}=\frac{1}{g_{m 1}}\left(-i_{t}-i_{t} g_{m 2} r_{\pi 2}\right)=-\frac{i_{t}}{g_{m 1}}\left(1+\beta_{0}\right) \tag{8.253}
\end{equation*}
$$

where the relation $\beta_{0}=g_{m 2} r_{\pi 2}$ has been used. The return current is

$$
\begin{equation*}
i_{r}=g_{m 3} v_{x} \tag{8.254}
\end{equation*}
$$

Therefore

$$
\begin{equation*}
\mathscr{R}(\text { output shorted })=-\frac{i_{r}}{i_{t}}=\frac{g_{m 3}}{g_{m 1}}\left(1+\beta_{0}\right)=1+\beta_{0} \tag{8.255}
\end{equation*}
$$

Substituting in Blackman's formula gives

$$
\begin{equation*}
R_{\text {out }}(\text { closed loop })=r_{o 2} \cdot \frac{1+\left(\beta_{0}+1\right)}{1+1}=\frac{r_{o 2}\left(\beta_{0}+2\right)}{2} \approx \frac{\beta_{0} r_{o 2}}{2} \tag{8.256}
\end{equation*}
$$

This approximate result agrees with (4.91), which was derived without the use of Blackman's formula.

### 8.8.3 Summary—Return-Ratio Analysis

Return-ratio analysis is an alternative approach to feedback circuit analysis that does not use two-ports. The loop transmission is measured by the return ratio $\mathscr{R}$. The return ratio is a different measure of loop transmission than af from two-port analysis. (The return ratio $\mathscr{R}$ is referred to as loop gain in some textbooks. That name is not associated with $\mathscr{R}$ here to avoid confusion with $T=a f$, which is called loop gain in this chapter.) For negative feedback circuits, $\mathscr{R}>0$. In an ideal feedback circuit, $\mathscr{R} \rightarrow \infty$ and the closed-loop gain is $A_{\infty}$, which typically depends only on passive components. The actual gain of a feedback circuit is close to $A_{\infty}$ if $\mathscr{R} \gg 1$. Blackman's impedance formula (8.238) gives the closed-loop impedance in terms of two return ratios.

Return-ratio analysis is often simpler than two-port analysis of feedback circuits. For example, return-ratio analysis uses equations that are independent of the type of feedback, and
simple manipulations of the circuit allow computation of the various terms in the equations. In contrast, two-port analysis uses different two-port representations for each of the four feedback configurations (series-series, series-shunt, shunt-series, and shunt-shunt). Therefore, the type of feedback must be correctly identified before undertaking two-port analysis. The resulting two-ports for the amplifier and feedback networks must be manipulated to find the openloop forward gain $a$ and the open-loop input and output impedances. With two-port analysis, the open-loop impedance is either multiplied or divided by $(1+T)$ to give the closed-loop impedance, depending upon the type of feedback. In contrast, Blackman's formula gives an equation for finding the closed-loop impedance, and this one equation applies to any port in any feedback circuit.

### 8.9 Modeling Input and Output Ports in Feedback Circuits

Throughout this chapter, the source and load impedances have been included when analyzing a feedback circuit. For instance, the inverting voltage-gain circuit in Fig. 8.47a, with source resistance $R_{S}$ and load resistance $R_{L}$, can be analyzed using the two-port or return-ratio methods described in this chapter. The resulting model is shown in Fig. 8.47b. The source and load resistances do not appear explicitly in the model, but the gain $A$, input resistance $R_{i}$, and output resistance $R_{o}$ are functions of the source and load resistances. Therefore, use of this model requires that both the source and load resistances are known. However, both the source and load are not always known or fixed in value. For example, a feedback amplifier might have to drive a range of load resistances. In that case, it would be desirable to have a simple model of the amplifier with the following properties: the elements in the model do not depend on the load, and the effect of a load on the gain can be easily calculated.

If only one of the resistances $R_{S}$ and $R_{L}$ is known, a useful model can be generated. First, consider Fig. 8.47a when the source resistance is unknown but the load is known. Then, the model in Fig. 8.47c can be used. Here, the key differences from the model in Fig. 8.47b are that $R_{i}^{\prime}$ and $A^{\prime}$ are used rather than $R_{i}$ and $A, R_{S}$ is shown explicitly, and the controlling voltage for $A^{\prime}$ is the voltage $v_{i}$ across $R_{i}^{\prime}$ rather than the source voltage $v_{s}$. (The single-prime mark here denotes that the quantity is computed with $R_{S}$ unknown.) The input resistance $R_{i}^{\prime}$ and gain $A^{\prime}$ are computed with the load connected and with an ideal input driving network. Here, the Thevenin driving network is ideal if the source resistance $R_{S}$ is zero. (If the input is a Norton equivalent consisting of a current source and parallel source resistance, $R_{i}^{\prime}$ and $A^{\prime}$ are found with $R_{S} \rightarrow \infty$.) The resulting $A^{\prime}$ and $R_{i}^{\prime}$ are not functions of $R_{S}$. The source resistance $R_{S}$ in Fig. 8.47 c forms a voltage divider with $R_{i}^{\prime}$; therefore, the overall voltage gain can be found by

$$
\begin{equation*}
\frac{v_{o}}{v_{s}}=\frac{v_{o}}{v_{i}} \cdot \frac{v_{i}}{v_{s}}=A^{\prime} \frac{R_{i}^{\prime}}{R_{i}^{\prime}+R_{S}} \tag{8.257}
\end{equation*}
$$

Next, consider Fig. 8.47a when the load is unknown but the source resistance is known. Fig. 8.47d shows the appropriate model. Here, the key differences from the model in Fig. 8.47b are that $R_{o}^{\prime \prime}$ and $A^{\prime \prime}$ are used rather than $R_{o}$ and $A$, and $R_{L}$ is shown explicitly. (The doubleprime mark denotes that the quantity is computed with $R_{L}$ unknown.) The output resistance $R_{O}^{\prime \prime}$ and gain $A^{\prime \prime}$ for this Thévenin model are computed assuming an ideal load, which is an open circuit here $\left(R_{L} \rightarrow \infty\right)$. The load resistance $R_{L}$ in Fig. $8.47 d$ forms a voltage divider with $R_{o}^{\prime \prime}$, so the loaded voltage gain is

$$
\begin{equation*}
\frac{v_{o}}{v_{s}}=A^{\prime \prime} \frac{R_{L}}{R_{o}^{\prime \prime}+R_{L}} \tag{8.258}
\end{equation*}
$$

image_name:(a)
description:
[
name: vs, type: VoltageSource, value: vs, ports: {Np: Vs, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vs, N2: Vi}
name: ri, type: Resistor, value: ri, ports: {N1: Vi, N2: GND}
name: -avVi, type: VoltageSource, value: -avVi, ports: {Np: -avvi, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: -avvi, N2: Vo}
name: RF, type: Resistor, value: RF, ports: {N1: Vi, N2: Vo}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is an inverting-gain feedback amplifier with a Thévenin equivalent model. The voltage gain is affected by the load resistance RL, forming a voltage divider with Ro''. The amplifier consists of a voltage source Vs, resistors RS, RF, ri, ro, and RL, and a dependent voltage source -avVi.

image_name:(b)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: Ri, type: Resistor, value: Ri, ports: {N1: Vs, N2: GND}
name: Avs, type: VoltageSource, value: Avs, ports: {Np: Avs, Nn: GND}
name: Ro, type: Resistor, value: Ro, ports: {N1: Avs, N2: Vo}
]
extrainfo:The circuit is a part of an inverting-gain feedback amplifier model. It consists of a voltage source Vs, a resistor Ri, a dependent voltage source Avs, and a resistor Ro. The output voltage Vo is taken across Ro.

image_name:(c)
description:
[
name: VS, type: VoltageSource, value: VS, ports: {Np: Vs, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vs, N2: Vi}
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: "Ri", type: Resistor, value: "Ri", ports: {N1: Vi, N2: GND}
name: "AVi", type: VoltageSource, value: "AVi", ports: {Np: "AVi", Nn: GND}
name: Ro, type: Resistor, value: Ro, ports: {N1: "AVi", N2: Vo}
]
extrainfo:The circuit is a model for an inverting-gain feedback amplifier with a known load resistance and unknown source resistance. It includes a voltage source VS, a resistor RS, a voltage source Vi, a resistor R'i, a dependent voltage source A'Vi, and a resistor Ro. The output voltage Vo is taken across Ro.

image_name:(d)
description:
[
name: Vs, type: VoltageSource, value: Vs, ports: {Np: Vs, Nn: GND}
name: Ri, type: Resistor, value: Ri, ports: {N1: Vs, N2: GND}
name: "AVs", type: VoltageSource, value: "AVs", ports: {Np: "AVs", Nn: GND}
name: Ro, type: Resistor, value: Ro, ports: {N1: "AVs", N2: Vo}
name: RL, type: Resistor, value: RL, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a feedback amplifier model with a voltage source Vs, a resistor Ri, a dependent voltage source A''Vs, and resistors Ro and RL. The output voltage Vo is taken across RL.

Figure 8.47 (a) An inverting-gain feedback amplifier. (b) A model for (a) based on feedback analysis with known load and source resistances. (c) Another model for (a) based on known load resistance and unknown source resistance. (d) A different model for (a) based on known source resistance and unknown load.

#### EXAMPLE

Model Fig. 8.47a with the circuit in Fig. 8.47d, assuming the load resistance is unknown.
The model in Fig. 8.47d can be used when $R_{L}$ is unknown. Using return-ratio analysis, the calculations of $R_{o}^{\prime \prime}$ and $A^{\prime \prime}$ are as follows. With $R_{L} \rightarrow \infty$, the circuit in Fig. 8.47a is identical to Fig. 8.39a, and therefore the return ratio is given by (8.196):

$$
\begin{equation*}
\mathscr{R}^{\prime \prime}=\mathscr{R}\left(R_{L} \rightarrow \infty\right)=\frac{R_{S} \| r_{i}}{R_{S} \| r_{i}+R_{F}+r_{o}} a_{v} \tag{8.259}
\end{equation*}
$$

The output resistance with $R_{L} \rightarrow \infty, R_{o}^{\prime \prime}$, can be found using Blackman's formula. First, the output resistance with the controlled source set to zero is

$$
\begin{equation*}
R_{o}^{\prime \prime}\left(a_{v}=0\right)=r_{o} \|\left(R_{F}+r_{i} \| R_{S}\right) \tag{8.260}
\end{equation*}
$$

The return ratio with the output port open is given in (8.259). The return ratio with the output port shorted is zero because shorting the output eliminates the feedback. Therefore, for the closed-loop output resistance, (8.238) gives

$$
\begin{equation*}
R_{o}^{\prime \prime}=r_{o} \|\left(R_{F}+r_{i} \| R_{S}\right) \frac{1+0}{1+\frac{R_{S} \| r_{i}}{R_{S} \| r_{i}+R_{F}+r_{o}} a_{v}} \tag{8.261}
\end{equation*}
$$

Calculation of $A^{\prime \prime}$ requires that $A_{\infty}^{\prime \prime}$ and $d^{\prime \prime}$ be found with $R_{L} \rightarrow \infty$.

$$
\begin{equation*}
A_{\infty}^{\prime \prime}=\left.\frac{v_{o}}{v_{s}}\right|_{a_{v}=\infty \& R_{L}=\infty}=-\frac{R_{F}}{R_{S}} \tag{8.262}
\end{equation*}
$$

and

$$
\begin{equation*}
d^{\prime \prime}=\left.\frac{v_{o}}{v_{s}}\right|_{a_{v}=0 \& R_{L}=\infty}=\frac{\left(R_{F}+r_{o}\right) \| r_{i}}{R_{S}+\left(R_{F}+r_{o}\right) \| r_{i}} \cdot \frac{r_{o}}{R_{F}+r_{o}} \tag{8.263}
\end{equation*}
$$

Using the results for $A_{\infty}^{\prime \prime}, \mathscr{R}^{\prime \prime}$, and $d^{\prime \prime}$, we can compute

$$
\begin{equation*}
A^{\prime \prime}=A_{\infty}^{\prime \prime} \frac{\mathscr{R}^{\prime \prime}}{1+\mathscr{R}^{\prime \prime}}+\frac{d^{\prime \prime}}{1+\mathscr{R}^{\prime \prime}} \tag{8.264}
\end{equation*}
$$

[Typically, the $d^{\prime \prime} /\left(1+\mathscr{R}^{\prime \prime}\right)$ term is small and can be ignored.] The voltage gain when a resistive load is connected can be found using (8.258). The only element of the model that was not computed is the input resistance $R_{i}$. It is a function of $R_{L}$, so it can only be computed once $R_{L}$ is known.

The output-port model in Fig. 8.47d could be drawn as a Thévenin or Norton equivalent. With the Thevenin equivalent shown (a controlled voltage source in series with an output resistance), $R_{o}^{\prime \prime}$ and $A^{\prime \prime}$ are computed with $R_{L} \rightarrow \infty$. When the output port is modeled by a Norton equivalent with a controlled current source and parallel output resistance, their values are found with $R_{L}=0$.
