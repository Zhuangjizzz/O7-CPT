# CHAPTER <br> 11 Nanometer Design Studies

The previous chapters of this book have taken us on a "scenic" route through the world of analog circuits, presenting important concepts and useful topologies. We have occasionally made design efforts, but only on a small scale. In this chapter, we embark upon two comprehensive designs so as to appreciate the mindset that an analog designer must uphold and the multitude of tasks that he or she must complete for a given circuit. The designs are carried out in $40-\mathrm{nm}$ CMOS technology with a 1-V supply. The reader is encouraged to review the op amp design examples in Chapter 9 before starting this chapter.

We begin with a brief look at the imperfections of nanometer devices and the design procedures to achieve certain transistor parameters. We then delve into the design of an op amp and, through simulations, optimize its performance. Finally, we deal with the design of a high-speed, high-precision amplifier and pursue various techniques to achieve a low power dissipation.

## 11.1 - Transistor Design Considerations

In Chapter 2, we studied the basic operation of MOSFETs and included a few second-order effects. Our investigation has produced a large-signal model (consisting of the triode-region quadratic equation and the saturation-region square-law relation), which becomes necessary in two cases: (1) when the transistor experiences large voltage (or current) changes due to the input or output signals, disobeying the small-signal model, or (2) when the transistor must be biased, requiring certain terminal voltages so as to carry a specified current. In analog design, the former case occurs occasionally, while the latter almost always.

The large-signal behavior of nanometer MOSFETs significantly departs from the "long-channel" model that we have developed. As a result of technology scaling, i.e., the shrinkage of MOS dimensions, several effects besides those studied in Chapter 2 manifest themselves, thereby altering the I/V characteristics. As an example, Fig. 11.1 plots the actual $I_{D}-V_{D S}$ characteristics of an NFET with $W / L=5 \mu \mathrm{~m} / 40$ nm and $V_{T H} \approx 300 \mathrm{mV}$ (using a BSIM4 model) against a "best-fit" long-channel square-law approximation. We observe that the two diverge considerably. Thus, even if we are not interested in the large-signal analysis of a circuit, we still face the problem of bias calculations using the square-law model.

In this section, we briefly consider a few "short-channel" effects that make the long-channel model inaccurate. A detailed treatment of short-channel effects is deferred to Chapter 17. It is important to note that the MOS small-signal model developed in Chapter 2 still holds for short-channel devices and, as seen throughout this book, suffices for the initial analysis of many analog circuit blocks. However, the expressions relating $g_{m}$ and $r_{O}$ to the bias conditions must be revised.
image_name:Figure 11.1
description:The graph in Figure 11.1 is an I-V characteristic plot for a 5-μm/40-nm MOS device. The plot compares the actual device characteristics (depicted with black curves) to a best-fit square-law model (depicted with gray curves). The x-axis represents the drain-source voltage, $V_{DS}$, measured in volts (V), ranging from 0 to 1 V. The y-axis represents the drain current, $I_{D}$, measured in milliamperes (mA), ranging from 0 to 3.5 mA.

The graph consists of several curves, each corresponding to different gate-source voltages, $V_{GS}$, which are incremented from 300 mV to 800 mV in 100-mV steps. These values are annotated on the right side of the graph for clarity.

The general behavior of the curves shows an initial rapid increase in $I_{D}$ as $V_{DS}$ increases from 0 V, which then begins to level off, indicating channel-length modulation effects. The actual device curves (black) exhibit more pronounced leveling compared to the square-law model (gray), highlighting the deviation from ideal behavior due to short-channel effects.

Key features include the 'knee' points on each curve, which serve as rough boundaries between the triode and saturation regions. These knee points are less distinct in the actual device curves, complicating the distinction between operating regions. The overall trend shows that higher $V_{GS}$ values result in higher $I_{D}$ for a given $V_{DS}$, consistent with MOSFET behavior.

Figure 11.1 I-V characteristics of an actual 5- $\mu \mathrm{m} / 40-\mathrm{nm}$ device (black curves) and a best-fit square-law device (gray curves). ( $V_{G S}$ is incremented from 300 mV to 800 mV in $100-\mathrm{mV}$ steps.)

The characteristics shown in Fig. 11.1 exhibit severe channel-length modulation for the actual 40nm devices, making it difficult to distinguish between the triode and saturation regions. But we can associate a "knee" point with each curve as a rough boundary. Figure 11.2 plots the actual $40-\mathrm{nm}$ device characteristics for a narrower $V_{G S}$ range, namely, $V_{G S}-V_{T H}=50 \mathrm{mV}, 100 \mathrm{mV}, \cdots, 350 \mathrm{mV}$. We observe knee points below $V_{D S}=0.2 \mathrm{~V}$. (Here, $W=5 \mu \mathrm{~m}$ and $V_{T H} \approx 200 \mathrm{mV}$.)
image_name:Figure 11.2
description:The graph in Figure 11.2 is an I-V characteristic plot for a 5-micrometer by 40-nanometer device, showing the relationship between the drain current ($I_D$) and the drain-source voltage ($V_{DS}$) for different gate-source voltage ($V_{GS}$) levels. The x-axis represents $V_{DS}$ in volts, ranging from 0 to 1 V, while the y-axis represents $I_D$ in milliamperes (mA), ranging from 0 to 1.2 mA. Both axes use a linear scale.

The plot consists of several curves, each corresponding to a different $V_{GS} - V_{TH}$ value, ranging from 50 mV to 350 mV in increments of 50 mV. The curves exhibit a typical MOSFET behavior, with each curve starting at the origin and initially increasing sharply, indicating the triode region. As $V_{DS}$ increases, the curves gradually flatten, showing the transition into the saturation region.

The knee point, which marks the transition from the triode to the saturation region, is observed below $V_{DS} = 0.2$ V for all curves. As $V_{GS}$ increases, the curves shift upwards, indicating higher drain currents for higher gate-source voltages.

Overall, the graph illustrates the expected behavior of MOSFET devices, highlighting the impact of varying $V_{GS}$ on the drain current and the clear demarcation between the triode and saturation regions at lower $V_{DS}$ values.

Figure 11.2 I-V characteristics of a $5-\mu \mathrm{m} / 40-\mathrm{nm}$ device for $V_{G S}-V_{T H}=50, \cdots, 350 \mathrm{mV}$.

## 11.2 - Deep-Submicron Effects

Among various short-channel effects, two are particularly important at this stage of our studies; both relate to the mobility of the carriers in the channel. Recall that we have assumed that the carrier velocity is given by $v=\mu E$, where $E$ denotes the electric field. We revisit this assumption here.

Velocity Saturation In a MOSFET, as $V_{D S}$ and hence the electric field along the source-drain path increase, $v$ does not rise proportionally (Fig. 11.3).
image_name:Figure 11.3 Velocity saturation at high electric fields.
description:The graph depicted in Figure 11.3 is a plot of carrier velocity versus electric field, illustrating the phenomenon of velocity saturation in a MOSFET. The graph is a two-dimensional plot with the horizontal axis labeled as 'E', representing the electric field, and the vertical axis labeled as 'Carrier Velocity', with units in cm/s.

The graph shows a curve starting from the origin, initially rising linearly, which indicates that at low electric fields, the carrier velocity increases proportionally with the electric field. However, as the electric field continues to increase, the curve begins to flatten, indicating a decrease in the rate of increase of the carrier velocity. This flattening of the curve signifies the onset of velocity saturation, where the carrier velocity approaches a maximum value and does not increase significantly despite further increases in the electric field.

The critical electric field, denoted as 'E_crit', is marked on the horizontal axis. This is the point where the linear increase transitions into saturation. At this point, the carrier velocity approaches a value of approximately 10^7 cm/s, as indicated by a horizontal dashed line extending from the vertical axis. This horizontal line represents the maximum carrier velocity achievable under the given conditions, highlighting the effect of velocity saturation.

Overall, the graph effectively demonstrates how carrier velocity becomes limited at high electric fields due to velocity saturation, a significant factor in the behavior of short-channel MOSFETs.

We say that the carriers experience "velocity saturation" or, equivalently, that the mobility (the slope of $v$ versus $E$ ) falls. This effect has arisen because the length of MOSFETs has shrunk from, say, $1 \mu \mathrm{~m}$ to 40 nm (a factor of 25) while the allowable drain-source voltage has decreased from 5 V to about 1 V . The lateral electric field has thus exceeded $E_{\text {crit }}(\approx 1 \mathrm{~V} / \mu \mathrm{m})$ in Fig. 11.3.

We deal with the modeling of velocity saturation in Chapter 17, but let us consider an extreme case here: suppose the charge carriers reach the saturated velocity, $v_{\text {sat }}$, as soon as they depart from the source. Since $I=Q_{d} \cdot v$, where $Q_{d}$ is the charge density (per unit length) and given by $W C_{o x}\left(V_{G S}-V_{T H}\right)$, we have

$$
\begin{equation*}
I_{D}=W C_{o x}\left(V_{G S}-V_{T H}\right) v_{s a t} \tag{11.1}
\end{equation*}
$$

Extreme velocity saturation therefore creates three departures from the square-law behavior. First, the device carries a current that is linearly proportional to the overdrive and independent of the channel length. ${ }^{1}$ Second, $I_{D}$ reaches saturation even for $V_{D S}<V_{G S}-V_{T H}$ (Fig. 11.4). As evident in Fig. 11.2, the knee points occur at relatively small $V_{D S}$ 's even as the overdrive reaches 350 mV . Third, the transconductance of a fully velocity-saturated MOSFET emerges as

$$
\begin{align*}
g_{m} & =\left.\frac{\partial I_{D}}{\partial V_{G S}}\right|_{V_{D S \text { const }}}  \tag{11.2}\\
& =W C_{o x} v_{\text {sat }} \tag{11.3}
\end{align*}
$$

a relatively constant value versus $I_{D}$ or $V_{G S}$. For example, in the plots of Fig. 11.2, the change in $I_{D}$ is fairly constant as the overdrive increments from 250 mV to 300 mV and from 300 mV to 350 mV .
image_name:Figure 11.4 Premature saturation of drain current due to velocity saturation.
description:The graph in Figure 11.4 illustrates the behavior of drain current \( I_D \) as a function of the drain-source voltage \( V_{DS} \) in a MOSFET, highlighting the effect of velocity saturation.

1. **Type of Graph and Function:**
- This is a plot graph showing the relationship between two variables: drain current \( I_D \) and drain-source voltage \( V_{DS} \).

2. **Axes Labels and Units:**
- The vertical axis represents the drain current \( I_D \), although specific units are not provided, it is typically measured in amperes (A).
- The horizontal axis represents the drain-source voltage \( V_{DS} \), which is typically measured in volts (V).
- Key points on the horizontal axis include \( V_{D0} \) and \( V_{GS} - V_{TH} \), indicating the threshold voltage level and the onset of saturation.

3. **Overall Behavior and Trends:**
- The graph shows two curves: one representing the behavior without velocity saturation (dashed line) and one with velocity saturation (solid line).
- Without velocity saturation, \( I_D \) increases sharply with \( V_{DS} \) and reaches a higher saturation level.
- With velocity saturation, \( I_D \) increases initially but levels off much sooner, indicating a lower saturation current.

4. **Key Features and Technical Details:**
- The dashed line indicates a scenario where the current continues to increase with \( V_{DS} \) beyond the threshold, reaching a higher saturation level.
- The solid line shows that with velocity saturation, the current reaches a plateau at a lower value of \( V_{DS} \), indicating premature saturation.
- The point \( V_{GS} - V_{TH} \) marks the transition to the saturation region.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for both conditions: "Without Velocity Saturation" and "With Velocity Saturation," clearly differentiating the two scenarios.
- Vertical dashed lines indicate critical voltage points such as \( V_{D0} \) and \( V_{GS} - V_{TH} \), highlighting the onset of the saturation region.

Mobility Degradation with Vertical Field The mobility of the charge carriers in the channel also declines as the gate-source voltage and the vertical field increase (Fig. 11.5).

image_name:Figure 11.5 Reduction of mobility due to vertical electric field.
description:Figure 11.5 is a graph illustrating the reduction of mobility (\( \mu \)) due to the vertical electric field as a function of the overdrive voltage \( V_{GS} - V_{TH} \). The graph is a two-dimensional plot with the x-axis labeled \( V_{GS} - V_{TH} \) and the y-axis labeled \( \mu \), representing mobility.

1. **Type of Graph and Function:**
- The graph is a plot showing the relationship between mobility and overdrive voltage, specifically focusing on how mobility decreases as the vertical electric field increases.

2. **Axes Labels and Units:**
- **X-axis:** \( V_{GS} - V_{TH} \) (Overdrive Voltage)
- **Y-axis:** \( \mu \) (Mobility)
- The units for the axes are not explicitly mentioned, but \( V_{GS} - V_{TH} \) is typically in volts, and mobility is a dimensionless ratio or could be in cm²/V·s.

3. **Overall Behavior and Trends:**
- The graph starts with a horizontal line at \( \mu_0 \), indicating initial constant mobility.
- As \( V_{GS} - V_{TH} \) increases, the mobility \( \mu \) begins to decrease in a nonlinear fashion, showing a downward slope.
- This behavior suggests a degradation in mobility due to increased vertical electric field.

4. **Key Features and Technical Details:**
- The graph exhibits a clear transition from a flat region to a declining slope.
- There are no specific peaks, valleys, or inflection points marked, but the overall trend is a smooth decline.

5. **Annotations and Specific Data Points:**
- The graph does not have specific annotations or numerical values marked on it, but it visually represents the concept of mobility degradation with increasing \( V_{GS} - V_{TH} \).

What is the impact of this mobility degradation on the device transconductance? We intuitively expect that $g_{m}$ no longer follows the linear relationship, $g_{m}=\mu C_{o x}(W / L)\left(V_{G S}-V_{T H}\right)$, with the overdrive voltage. Figure 11.6 displays this behavior for the $5-\mu \mathrm{m} / 40-\mathrm{nm}$ NFET mentioned above.
image_name:Figure 11.6 Transconductance as a function of overdrive voltage
description:The graph in Figure 11.6 is a plot of transconductance \( g_m \) as a function of the overdrive voltage \( V_{GS} - V_{TH} \). It is a line graph with the x-axis representing the overdrive voltage \( V_{GS} - V_{TH} \) in volts (V), ranging from 0 to 0.6 V. The y-axis represents the transconductance \( g_m \) in millisiemens (mS), ranging from 0 to 5 mS.

Overall Behavior and Trends:
The graph shows a nonlinear relationship between \( g_m \) and \( V_{GS} - V_{TH} \). Initially, as \( V_{GS} - V_{TH} \) increases from 0, \( g_m \) increases sharply, indicating a strong dependence of transconductance on the overdrive voltage in this region. However, as \( V_{GS} - V_{TH} \) approaches 0.5 V, the rate of increase in \( g_m \) starts to diminish, showing a saturation trend.

Key Features and Technical Details:
- The graph indicates that \( g_m \) does not increase linearly with \( V_{GS} - V_{TH} \) due to mobility degradation, which is consistent with the context provided.
- There is a noticeable inflection point around 0.3 V where the rate of increase in \( g_m \) begins to slow down.
- \( g_m \) reaches a maximum value slightly above 5 mS as \( V_{GS} - V_{TH} \) approaches 0.6 V, suggesting a saturation effect.

Annotations and Specific Data Points:
- The graph is marked with gridlines to aid in visualizing the changes in \( g_m \) as \( V_{GS} - V_{TH} \) changes.
- No specific data points are annotated, but the trend is clear and consistent with the theoretical expectation that mobility degradation affects the transconductance behavior, deviating from linearity as \( V_{GS} - V_{TH} \) increases.

#### Example 11.1

We approximate the mobility plot of Fig. 11.5 by

$$
\begin{equation*}
\mu=\frac{\mu_{0}}{1+\theta\left(V_{G S}-V_{T H}\right)} \tag{11.4}
\end{equation*}
$$

where $\theta$ is a proportionality factor with a dimension of (voltage) ${ }^{-1}$. Determine the transconductance of a MOSFET that suffers from this type of mobility degradation.

#### Solution

We write

$$
\begin{equation*}
I_{D}=\frac{1}{2} \frac{\mu_{0} C_{o x}}{1+\theta\left(V_{G S}-V_{T H}\right)} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2} \tag{11.5}
\end{equation*}
$$

and hence

$$
\begin{equation*}
g_{m}=\mu_{0} C_{o x} \frac{W}{L} \frac{(\theta / 2)\left(V_{G S}-V_{T H}\right)^{2}+V_{G S}-V_{T H}}{\left[1+\theta\left(V_{G S}-V_{T H}\right)\right]^{2}} \tag{11.6}
\end{equation*}
$$

As expected, for $\theta\left(V_{G S}-V_{T H}\right) \ll 1$, we have $g_{m} \approx \mu_{0} C_{o x}(W / L)\left(V_{G S}-V_{T H}\right)$. At the other extreme, if $\left(V_{G S}-V_{T H}\right) \gg 2 / \theta$, then $g_{m}$ approaches a constant value: $g_{m} \approx(1 / 2) \mu_{0} C_{o x}(W / L) / \theta$.

In the general case, the degradation of the mobility due to both lateral and vertical fields ( $V_{D S}$ and $V_{G S}$, respectively) must be considered. Nonetheless, the simple results derived above suffice for most of our studies in analog design.

## 11.3 ■ Transconductance Scaling

Device transconductances manifest themselves in almost every analog circuit. Suppose a transistor operates in the saturation region but does not provide the required transconductance. The $g_{m}$ equations in Chapter 2,

$$
\begin{align*}
g_{m} & =\mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)  \tag{11.7}\\
& =\sqrt{2 \mu_{n} C_{o x} \frac{W}{L} I_{D}}  \tag{11.8}\\
& =\frac{2 I_{D}}{V_{G S}-V_{T H}} \tag{11.9}
\end{align*}
$$

suggest that adjustments in three parameters, namely, $W / L, V_{G S}-V_{T H}$, or $I_{D}$, can scale $g_{m}$. We study these scenarios, assuming for now a long-channel device and hence $I_{D} \approx(1 / 2) \mu_{n} C_{o x}(W / L)\left(V_{G S}-V_{T H}\right)^{2}$. That is, $V_{G S}-V_{T H} \approx \sqrt{2 I_{D} /\left(\mu_{n} C_{o x} W / L\right)}$. In each case, we keep one of the parameters constant and vary the other two.

From (11.7), we can increase $W / L$ while keeping $V_{G S}-V_{T H}$ constant. In this case, both $g_{m}$ and $I_{D}$ linearly scale with $W / L$ (why?) [Fig. 11.7(a)], and so does the power consumption. Alternatively, we
image_name:(a)
description:The graph labeled (a) is a linear plot illustrating the relationship between the transconductance (g_m) and the drain current (I_D) with respect to the width-to-length ratio (W/L) of a MOSFET device. The x-axis represents the width-to-length ratio (W/L), and the y-axis represents both the transconductance (g_m) and the drain current (I_D). The parameter V_GS - V_TH is held constant in this graph.

1. **Type of Graph and Function:**
- This is a linear plot showing the dependence of g_m and I_D on W/L.

2. **Axes Labels and Units:**
- **X-axis:** Width-to-length ratio (W/L) (unitless).
- **Y-axis:** Transconductance (g_m) and Drain Current (I_D) (units not specified, assumed to be consistent with typical electrical units like Siemens for g_m and Amperes for I_D).

3. **Overall Behavior and Trends:**
- Both g_m and I_D increase linearly with increasing W/L. This indicates a direct proportionality between these parameters and the width-to-length ratio when V_GS - V_TH is constant.

4. **Key Features and Technical Details:**
- The graph shows two straight lines originating from the origin, reflecting the linear scaling of both g_m and I_D with W/L.
- The linearity suggests that doubling the W/L will double both g_m and I_D, maintaining the proportionality.

5. **Annotations and Specific Data Points:**
- The graph does not have specific numerical values or markers, but the linear trend is clear and consistent across the range of W/L values shown.
image_name:(b)
description:The graph labeled (b) in Figure 11.7 is a plot illustrating the relationship between the transconductance, \( g_m \), the drain current, \( I_D \), and the gate-source voltage minus the threshold voltage, \( V_{GS} - V_{TH} \), while keeping the width-to-length ratio, \( W/L \), constant.

1. Type of Graph and Function:
This is a linear graph showing the dependencies of two parameters, \( g_m \) and \( I_D \), on \( V_{GS} - V_{TH} \).

2. Axes Labels and Units:
- **Horizontal Axis:** Represents \( V_{GS} - V_{TH} \).
- **Vertical Axis:** Represents both \( g_m \) and \( I_D \).
- The graph uses a linear scale for both axes.

3. Overall Behavior and Trends:
- The plot shows that as \( V_{GS} - V_{TH} \) increases, \( g_m \) increases linearly, while \( I_D \) also increases but at a decreasing rate, indicating a sub-linear relationship.
- The graph starts from the origin, suggesting that both \( g_m \) and \( I_D \) are zero when \( V_{GS} - V_{TH} \) is zero.

4. Key Features and Technical Details:
- \( g_m \) exhibits a positive linear trend with \( V_{GS} - V_{TH} \), suggesting a direct proportionality.
- \( I_D \) increases with \( V_{GS} - V_{TH} \) but the curve bends downwards, indicating diminishing returns in \( I_D \) increase as \( V_{GS} - V_{TH} \) grows.

5. Annotations and Specific Data Points:
- The graph does not have specific numerical values annotated, but the linear and sub-linear trends are clearly marked.
- There are no specific markers or reference lines other than the axes themselves.
image_name:(c)
description:The graph labeled (c) in Figure 11.7 illustrates the relationship between the transconductance (g_m) and the ratio of the width to length (W/L) of a MOSFET, with the gate-source voltage minus the threshold voltage (V_GS - V_TH) held constant. The axes are as follows:

1. **Y-axis**: Represents the transconductance (g_m), which is a measure of the gain of the MOSFET. It is depicted in arbitrary units.
2. **X-axis**: Represents the ratio of the width to length (W/L) of the MOSFET, also in arbitrary units.

**Overall Behavior and Trends:**
- As W/L increases, the transconductance (g_m) also increases, showing a positive correlation between these two parameters.
- The graph shows a nonlinear upward trend, suggesting that the increase in g_m is not directly proportional to W/L but rather follows a curve that rises more slowly as W/L becomes larger.

**Key Features and Technical Details:**
- The graph starts from the origin, indicating that at zero W/L, the transconductance is also zero.
- There is a noticeable curve in the plot, which suggests diminishing returns in transconductance increase as W/L grows larger.
- There are no specific annotations or markers on the graph, but the curve implies an asymptotic behavior as it approaches a certain value.

**Annotations and Specific Data Points:**
- The graph is free of specific numerical values or markers, focusing on the qualitative relationship between g_m and W/L when V_GS - V_TH is constant.

This graph is useful for understanding how changing the physical dimensions of a MOSFET affects its transconductance when the voltage condition is kept constant, emphasizing the importance of device geometry in electrical performance.
image_name:(d)
description:The graph labeled (d) in Figure 11.7 is a plot showing the relationship between the transconductance ($g_m$) and the gate-source voltage minus the threshold voltage ($V_{GS} - V_{TH}$) as dependent on the drain current ($I_D$), with the width-to-length ratio ($W/L$) held constant.

1. **Type of Graph and Function**: This is a linear plot showing how $g_m$ and $V_{GS} - V_{TH}$ vary with respect to $I_D$.

2. **Axes Labels and Units**:
- The horizontal axis represents the drain current ($I_D$).
- The left vertical axis represents the transconductance ($g_m$).
- The right vertical axis represents the gate-source voltage minus the threshold voltage ($V_{GS} - V_{TH}$).
- The scales are linear for all axes.

3. **Overall Behavior and Trends**:
- As $I_D$ increases, $g_m$ shows an upward curve, indicating that transconductance increases with increasing drain current.
- Simultaneously, $V_{GS} - V_{TH}$ also increases, showing a similar upward trend.

4. **Key Features and Technical Details**:
- Both $g_m$ and $V_{GS} - V_{TH}$ increase non-linearly with $I_D$, suggesting a quadratic relationship typical of MOSFET behavior in saturation.
- The graph implies that with a constant $W/L$, increasing $I_D$ leads to higher $g_m$ and $V_{GS} - V_{TH}$, reflecting the dependency of these parameters on the drain current.

5. **Annotations and Specific Data Points**:
- There are no specific annotations or numerical data points marked on the graph. The curves are smooth and continuous, indicating a theoretical representation rather than empirical data.
image_name:(e)
description:The graph labeled (e) in Figure 11.7 illustrates the relationship between the transconductance (g_m) and the width-to-length ratio (W/L) as functions of the drain current (I_D), with the gate-source voltage minus threshold voltage (V_GS - V_TH) held constant.

1. **Type of Graph and Function:**
- The graph is a linear plot showing the dependence of two variables, g_m and W/L, on I_D.

2. **Axes Labels and Units:**
- The horizontal axis represents the drain current (I_D), which is typically measured in amperes (A).
- The vertical axis on the left represents the transconductance (g_m), usually measured in siemens (S).
- The vertical axis on the right represents the width-to-length ratio (W/L), a dimensionless quantity.

3. **Overall Behavior and Trends:**
- Both g_m and W/L exhibit a linear increase as the drain current (I_D) increases. This indicates a direct proportionality between these parameters and I_D when V_GS - V_TH is constant.

4. **Key Features and Technical Details:**
- The graph shows linear behavior with no visible saturation or non-linear effects, suggesting that the device operates in a region where g_m and W/L are directly proportional to I_D.
- There are no peaks, valleys, or inflection points, indicating a straightforward linear relationship.

5. **Annotations and Specific Data Points:**
- The graph does not show specific numerical values or annotations, focusing instead on the qualitative linear trend of the relationships.

This graph is useful for understanding how changes in drain current affect the transconductance and width-to-length ratio when the gate overdrive voltage is constant. It highlights the linear scaling of these parameters with I_D, which is critical for designing and optimizing MOSFET operation in analog circuits.
image_name:(f)
description:The graph labeled (f) in Figure 11.7 illustrates the relationship between the transconductance \( g_m \) and the width-to-length ratio \( W/L \) with respect to \( V_{GS} - V_{TH} \) when the drain current \( I_D \) is kept constant.

Type of Graph and Function
This is a parametric plot showing the dependence of two variables, \( g_m \) and \( W/L \), on the voltage difference \( V_{GS} - V_{TH} \), with a constant drain current \( I_D \).

Axes Labels and Units
- The horizontal axis represents \( V_{GS} - V_{TH} \), which is the gate-source voltage minus the threshold voltage.
- The left vertical axis represents the transconductance \( g_m \).
- The right vertical axis represents the width-to-length ratio \( W/L \).

Overall Behavior and Trends
- The plot shows two curves:
- The \( g_m \) curve starts at a higher value and decreases as \( V_{GS} - V_{TH} \) increases. It exhibits a downward slope, indicating that \( g_m \) decreases with increasing \( V_{GS} - V_{TH} \) when \( I_D \) is constant.
- The \( W/L \) curve starts at a lower value and increases as \( V_{GS} - V_{TH} \) increases. It shows an upward trend, suggesting that \( W/L \) increases with \( V_{GS} - V_{TH} \).

Key Features and Technical Details
- The \( g_m \) curve has a noticeable curvature, starting at a high point and gradually decreasing, indicating a nonlinear relationship.
- The \( W/L \) curve, on the other hand, starts low and increases, suggesting an inverse relationship with \( g_m \).
- There is a dotted line indicating a threshold or reference level for \( I_D/\xi V_T \), which provides a reference for the transconductance.

Annotations and Specific Data Points
- The graph is annotated with a dotted horizontal line representing \( I_D/\xi V_T \), serving as a reference for comparing the behavior of \( g_m \).
- No specific numerical values are provided, but the trends are clear and indicative of the relationships between the variables.

Figure 11.7 Dependence of (a) $g_{m}$ and $I_{D}$ upon $W / L$, (b) $g_{m}$ and $I_{D}$ upon $V_{G S}-V_{T H}$, (c) $g_{m}$ and $V_{G S}-V_{T H}$ upon $W / L$, (d) $g_{m}$ and $V_{G S}-V_{T H}$ upon $I_{D}$, (e) $g_{m}$ and $W / L$ upon $I_{D}$, and (f) $g_{m}$ and $W / L$ upon $V_{G S}-V_{T H}$.
can increase $V_{G S}-V_{T H}$ but keep $W / L$ constant [Fig. 11.7(b)], thus requiring a higher drain current. In the former case, the device capacitances rise whereas in the latter, $V_{D S, \text { min }}$ increases. In this chapter, we use the notations $V_{D S, \text { min }}, V_{D, s a t}$, and $V_{G S}-V_{T H}$ interchangeably.

From (11.8), we can raise $W / L$ while $I_{D}$ is constant [Fig. 11.7(c)], as a result of which $V_{G S}-V_{T H}$ is lowered (why?). Due to subthreshold conduction, however, $g_{m}$ does not climb indefinitely in this case. If we keep $W / L$ constant and increase $I_{D}$ [Fig. 11.7(d)], then $V_{G S}-V_{T H}$ and hence $V_{D S, \min }$ must rise.

From (11.9), we can increase $I_{D}$ while $V_{G S}-V_{T H}$ is constant [Fig. 11.7(e)]. This requires that $W / L$ increase. Alternatively, we can lower $V_{G S}-V_{T H}$ and keep $I_{D}$ constant [Fig. 11.7(f)], which means that $W / L$ must increase. For $V_{G S}-V_{T H} \approx 0$, the device enters the subthreshold region and $g_{m} \approx I_{D} /\left(\xi V_{T}\right)$. In both cases, the device capacitances climb.

Let us now reconsider the foregoing six scenarios for nanometer devices. We note that the plots in Fig. 11.7 still hold qualitatively, but the $g_{m}$ and overdrive equations are more complex. The case of Fig. 11.7(a) is particularly interesting and useful and is studied further in the following example.

#### Example 11.2

The linear scaling of $g_{m}$ and $I_{D}$ with $W / L$, shown in Fig. 11.7(a), holds regardless of the transistor characteristics. Explain why.

#### Solution

Consider, as an example, two identical transistors connected in parallel (Fig. 11.8), each having a transconductance of $g_{m}$. If $V_{G S}$ changes by $\Delta V$, then the drain current of each device changes by $g_{m} \Delta V$, and hence the current of the composite device changes by $2 g_{m} \Delta V$. That is, the parallel combination exhibits a transconductance of $2 g_{m}$. We conclude that increasing both the width and the drain current of the transistor by a factor of $K(>1)$ is equivalent to placing $K$ transistors in parallel and raising the $g_{m}$ by a factor of $K$. We say that the scaling preserves the device "current density" $\left(I_{D} / W\right)$ in this case. Note that the bias overdrive voltage remains constant in this scenario, and so does the $g_{m} / I_{D}$ ratio. The latter property proves useful in our studies.
image_name:Figure 11.8
description:
[
name: M1, type: NMOS, ports: {S: GND, D: LOAD, G: VGS}
name: M2, type: NMOS, ports: {S: GND, D: LOAD, G: VGS}
name: VGS, type: VoltageSource, value: VGS, ports: {Np: VGS, Nn: GND}
]
extrainfo:The circuit consists of two NMOS transistors, M1 and M2, in a push-pull configuration with a load connected at the common drain node. The gate voltage is provided by a voltage source VGS.

Of the six scenarios depicted in Fig. 11.7, which ones are more common in practice? Since modern analog circuits must operate with low supplies (around 1 V ), we often limit $V_{G S}-V_{T H}$ to a few hundred millivolts. Thus, to obtain a certain transconductance, we first keep increasing the width [Fig. 11.7(c)] to the extent that it raises the $g_{m}$ significantly. As $g_{m}$ approaches a constant value (in the subthreshold region), the width is no longer a determining factor, leaving the drain current as the only parameter that can increase the $g_{m}$ [Fig. 11.7(d)]. However, as we increase $I_{D}$ in this case, $V_{G S}-V_{T H}$ may exceed the allotted value, forcing us to resort to the scenario in Fig. 11.7(e) [which is equivalent to that in Fig. 11.7(a)]. These trials and errors seem rather haphazard, but do not despair! The remainder of this section is dedicated to developing a methodical approach to transistor design. We begin with an important example.

#### Example 11.3

A transistor having an aspect ratio of $(W / L)_{R E F}$ exhibits the $g_{m}-I_{D}$ characteristic shown in Fig. 11.9(a).
image_name:(a)
description:The graph in Fig. 11.9(a) is a plot of transconductance (g_m) versus drain current (I_D) for a transistor with a specific aspect ratio \((W/L)_{REF}\). This is a characteristic curve used in transistor analysis.

1. **Type of Graph and Function:**
- This is a characteristic curve graph depicting the relationship between transconductance and drain current for a transistor.

2. **Axes Labels and Units:**
- The x-axis represents the drain current \(I_D\), which is typically measured in amperes.
- The y-axis represents the transconductance \(g_m\), typically measured in siemens (S).
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The curve shows a positive, increasing relationship between transconductance \(g_m\) and drain current \(I_D\).
- As the drain current \(I_D\) increases, the transconductance \(g_m\) also increases, indicating that higher currents enhance the transistor's ability to control the output current.

4. **Key Features and Technical Details:**
- The graph begins at a lower value of \(g_m\) and rises as \(I_D\) increases.
- There is a marked point on the curve at \(I_{D1}\) where \(g_m\) is equal to \(g_{m1}\).
- The curve does not display any saturation or maximum point within the visible range, suggesting a continuous increase in \(g_m\) with \(I_D\).

5. **Annotations and Specific Data Points:**
- A specific reference point \((W/L)_{REF}\) is indicated, highlighting the aspect ratio used for this characteristic curve.
- The point \((I_{D1}, g_{m1})\) is specifically marked, providing a reference for initial biasing conditions.

This graph provides a visual understanding of how changes in drain current affect the transconductance of a transistor, which is crucial for designing and optimizing transistor performance in circuits.
image_name:(b)
description:The graph in Fig. 11.9(b) is a plot of transconductance \( g_m \) versus drain current \( I_D \). The x-axis represents the drain current \( I_D \), and the y-axis represents the transconductance \( g_m \). The graph is plotted on a linear scale for both axes.

Overall Behavior and Trends
The graph shows a nonlinear relationship between \( g_m \) and \( I_D \), with \( g_m \) increasing as \( I_D \) increases. It starts at a lower value \( g_{m1} \) at \( I_{D1} \) and rises to \( 2g_{m1} \) when the drain current doubles to \( 2I_{D1} \). The curve is concave down, indicating diminishing returns in \( g_m \) increase as \( I_D \) continues to rise.

Key Features and Technical Details
- **Initial Point:** The curve starts at \( I_{D1} \) with a corresponding transconductance \( g_{m1} \).
- **Doubling Width Effect:** The dashed line indicates the effect of doubling the transistor width \( W \), which results in doubling the transconductance for the same \( I_D \). This is shown by the point \( 2g_{m1} \) at \( I_{D1} \).
- **Concave Shape:** The curve's concave shape illustrates that as \( I_D \) increases, the rate of increase in \( g_m \) decreases.

Annotations and Specific Data Points
- **Reference Line:** A dashed line from \( g_{m1} \) to \( 2g_{m1} \) highlights the relationship between the initial and doubled transconductance values.
- **Markers:** Specific points are marked to show \( g_{m1} \) at \( I_{D1} \) and \( 2g_{m1} \) at \( 2I_{D1} \).
image_name:(c)
description:The graph labeled (c) is a plot illustrating the relationship between the transconductance (g_m) and the drain current (I_D) with respect to the overdrive voltage (V_GS - V_TH). This is a characteristic curve for a transistor with variable width (W) and constant length (L). The x-axis represents the drain current (I_D) and the overdrive voltage (V_GS - V_TH), while the y-axis represents the transconductance (g_m).

1. **Axes Labels and Units:**
- **X-axis:** The left side of the x-axis is labeled as V_GS - V_TH, representing the overdrive voltage, while the right side is labeled as I_D, representing the drain current. The scale is linear.
- **Y-axis:** Labeled as g_m, representing the transconductance, with a linear scale.

2. **Overall Behavior and Trends:**
- The graph shows a non-linear, upward-sloping curve, indicating that as the overdrive voltage and drain current increase, the transconductance also increases.
- The curve represents a scenario where the width of the transistor is varied, affecting the transconductance at different points.

3. **Key Features and Technical Details:**
- Two overdrive voltages are marked: (V_GS - V_TH)_1 and (V_GS - V_TH)_2, with corresponding transconductance values of g_m1 and g_m2.
- As the width (W) of the transistor doubles, the transconductance increases from g_m1 to 2g_m2, showing a proportional relationship.
- The graph illustrates two points on the I_D axis: I_D1 and I_D2, with I_D2 being twice I_D1, indicating the effect of doubling the width.

4. **Annotations and Specific Data Points:**
- The curve is annotated with dashed lines showing how changes in overdrive voltage and width affect the transconductance and drain current.
- The specific points (I_D1, g_m1) and (I_D2, g_m2) are highlighted to show the initial and doubled conditions.

This graph effectively demonstrates the impact of changing the width of the transistor on its transconductance and drain current, under constant overdrive voltage conditions.
image_name:(d)
description:The graph labeled (d) in Figure 11.9 is a plot illustrating the relationship between transconductance (g_m) and the drain current (I_D) for a transistor. The graph is a two-dimensional plot with the vertical axis labeled as g_m and the horizontal axis labeled as I_D. Both axes are on a linear scale.

Type of Graph and Function:
This is a characteristic curve graph showing how transconductance varies with changes in the drain current under specific conditions of gate-source voltage minus threshold voltage (V_GS - V_TH).

Axes Labels and Units:
- **Vertical Axis (g_m):** Represents the transconductance of the transistor. No specific units are provided, but transconductance is typically measured in siemens (S).
- **Horizontal Axis (I_D):** Represents the drain current, typically measured in amperes (A).

Overall Behavior and Trends:
The graph shows a nonlinear curve that starts at a certain transconductance value (g_m0) when the drain current is I_D0. As the drain current increases towards I_DX, the transconductance also increases, reaching a higher value of 2g_mx. The curve exhibits a smooth, upward trend indicating that transconductance increases with increasing drain current.

Key Features and Technical Details:
- **Starting Point:** The curve begins at a point (I_D0, g_m0) where the initial transconductance is g_m0.
- **Ending Point:** The curve ends at a point (I_DX, 2g_mx) where the transconductance doubles to 2g_mx.
- **Slope:** The curve has a positive slope, indicating that as the drain current increases, the transconductance increases.
- **Reference Lines:** The graph includes dashed reference lines showing the initial and final transconductance values and corresponding drain currents.

Annotations and Specific Data Points:
- The graph is annotated with arrows indicating the direction of change in transconductance as the drain current increases.
- The dashed lines and arrows serve as guides to show the relationship between changes in the drain current and the corresponding changes in transconductance.

(I) Suppose the device is first biased at $I_{D}=I_{D 1}$. What happens to the transconductance and the drain current if the width is doubled while $V_{G S}-V_{T H}$ remains constant? (II) Repeat (I) if we begin with a greater overdrive. (III) We wish to obtain a transconductance of $g_{m x}$ at a drain current of $I_{D x}$. How should the transistor be scaled?

#### Solution

(I) With a constant $V_{G S}-V_{T H}$, doubling the width also doubles the transconductance and the drain current (Example 11.2). Since $g_{m} / I_{D}$ is constant, to obtain this point on the $g_{m}-I_{D}$ plane, we pass a straight line through the origin and $\left(I_{D 1}, g_{m 1}\right)$, continuing to reach $\left(2 I_{D 1}, 2 g_{m 1}\right)$ [Fig. 11.9(b)]. Thus, all ( $\left.I_{D}, g_{m}\right)$ combinations resulting from the scaling of $W$ fall on this line if the overdrive is fixed.
(II) If we begin with a greater overdrive, $\left(V_{G S}-V_{T H}\right)_{2}$, the $\left(I_{D}, g_{m}\right)$ point is located elsewhere, at $\left(I_{D 2}, g_{m 2}\right)$, on the characteristic [Fig. 11.9(c)]. We again draw a straight line through the origin and ( $I_{D 2}, g_{m 2}$ ) and continue to $\left(2 I_{D 2}, 2 g_{m 2}\right)$. Thus, each such line in the $g_{m}-I_{D}$ plane represents the possible $\left(I_{D}, g_{m}\right)$ combinations that can be obtained by scaling $W$ for a given overdrive.
(III) We draw a line through the origin and the point $\left(I_{D x}, g_{m x}\right)$ [Fig. 11.9(d)]. The intersection of the line and the $g_{m}$ plot yields a "reference" point specifying the proper overdrive voltage, $\left(V_{G S}-V_{T H}\right)_{0}$, and an acceptable ( $I_{D}, g_{m}$ ) combination, $\left(I_{D 0}, g_{m 0}\right)$. If the width is scaled up by a factor of $g_{m x} / g_{m 0}\left(=I_{D x} / I_{D 0}\right)$, and the overdrive remains equal to $\left(V_{G S}-V_{T H}\right)_{0}$, then the desired transconductance and current are obtained.

## 11.4 - Transistor Design

The reader may have noticed by now that a given transistor in a circuit is characterized by a multitude of parameters. In this section, we assume that transistors operate in saturation and focus on two bias quantities, $I_{D}$ and $V_{G S}-V_{T H}\left(=V_{D S, \min }\right)$, one small-signal parameter, $g_{m}$, and one physical parameter, $W / L$. A typical transistor design problem specifies two of the first three and seeks the other two (Table 11.1). We wish to develop methodical approaches to computing these two parameters for nanometer devices. While not listed here explicitly, the output resistance, $r_{O}$, also proves important in many circuits and is eventually included in our studies in Sec. 11.4.5.

Table 11.1 Three scenarios encountered in transistor design.

|  | Case I | Case II | Case III |
| :--- | :---: | :---: | :---: |
| Given | $I_{D}, V_{D S, \min }$ | $g_{m}, I_{D}$ | $g_{m}, V_{D S, \min }$ |
| To Be Determined | $\frac{W}{L}, g_{m}$ | $\frac{W}{L}, V_{D S, \min }$ | $\frac{W}{L}, I_{D}$ |
| Design Revision | $g_{m}$ insufficient; | $V_{D S, \min \text { too large; }}$ | $I_{D}$ too large; |
|  | Raise $I_{D}$ and $\frac{W}{L}$ | Raise $\frac{W}{L}$ | Raise $\frac{W}{L} ;$ Lower $V_{G S}-V_{T H}$ |

The reader may recognize that the design problems shown in Table 11.1 are "overconstrained," i.e., the two given parameters inevitably lead to certain values for the other two-even though the results may not always be desirable. For example, a known $I_{D}$ and $V_{D S, \min }$ directly give a value for $g_{m}$ that may not be sufficient for a particular circuit. In such a case, we must modify the design as prescribed in the last row of the table. We will elaborate on this row in the design studies to be followed, but let us make some preliminary remarks here. In Case I, an insufficient $g_{m}$ would require a higher $I_{D}$ (possibly exceeding a power budget) and a greater $W / L$ (to satisfy the specified $V_{D S, \min }$ ). In Case II, the given $I_{D}$ and $g_{m}$ may yield an unacceptably large $V_{D S, \text { min }}$, thereby dictating a greater $W / L$. In Case III, the necessary $I_{D}$ may be excessive, demanding a greater $W / L$ and a smaller overdrive. ${ }^{2}$

### 11.4.1 Design for Given $I_{D}$ and $V_{D S, \min }$

A common situation that arises in analog design is as follows. For a particular transistor in the circuit, we have chosen a bias current (perhaps according to a power budget) and a minimum $V_{D S}$ (perhaps according to the voltage headroom, i.e., the restrictions imposed by the supply voltage and the required swings). ${ }^{3}$ We now wish to determine the dimensions and the transconductance of the device, recognizing that the square-law equations are inaccurate. Of course, with the transistor models available, we can simulate the device and obtain these values, but we seek a more methodical and less laborious procedure. Our approach proceeds in three steps. We consider $I_{D}=0.5 \mathrm{~mA}$ and $V_{D S, \min }=200 \mathrm{mV}$ as an example.

Step 1 Select a "reference" transistor, with a width $W_{R E F}$ and a length equal to the minimum allowable value, $L_{\min }$ (e.g., $L_{\min }=40 \mathrm{~nm}$ ). Let us choose $W_{R E F}=5 \mu \mathrm{~m}$ as an example.

Step 2 Using the actual device models and a circuit simulator, plot the $I_{D}-V_{D S}$ characteristics of the reference transistor for different values of $V_{G S}-V_{T H}$. In typical analog circuits, $V_{G S}-V_{T H}$ ranges from about 50 mV to about 600 mV . We can therefore construct the characteristics with the overdrive

image_name:Figure 11.10
description:Figure 11.10 is a plot of the drain current ($I_D$) versus the drain-source voltage ($V_{DS}$) for a reference transistor. The graph is a set of $I_D$-$V_{DS}$ characteristics for different values of the overdrive voltage, $V_{GS} - V_{TH}$, incremented in steps of 50 mV, ranging from 50 mV to 350 mV.

1. **Type of Graph and Function:**
- This is an $I_D$-$V_{DS}$ characteristics plot, commonly used in transistor analysis to show how the drain current varies with the drain-source voltage for different gate-source overdrive voltages.

2. **Axes Labels and Units:**
- The x-axis represents $V_{DS}$ (drain-source voltage) in volts (V), ranging from 0 to 1 V.
- The y-axis represents $I_D$ (drain current) in milliamperes (mA), ranging from 0 to 1.2 mA.
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The curves exhibit typical transistor behavior, where the drain current increases with an increase in $V_{DS}$ and also with an increase in $V_{GS} - V_{TH}$.
- For lower values of $V_{DS}$, the curves show a linear increase in current, indicating operation in the ohmic region.
- As $V_{DS}$ increases further, the curves flatten, indicating the saturation region where the current becomes relatively constant.

4. **Key Features and Technical Details:**
- Each curve corresponds to a specific $V_{GS} - V_{TH}$ value, starting from 50 mV and increasing in 50 mV steps up to 350 mV.
- The saturation current increases with higher $V_{GS} - V_{TH}$ values.
- A vertical line is drawn at $V_{DS} = 0.2$ V, which intersects the curves, indicating a reference point, possibly related to a specific operating condition.

5. **Annotations and Specific Data Points:**
- The vertical line at $V_{DS} = 0.2$ V intersects the curves around $I_D = 0.5$ mA, highlighting a specific operating point or condition of interest.

Figure 11.10 Drain current for $V_{G S}-V_{T H}=50 \mathrm{mV} \cdots 350 \mathrm{mV}$ in steps of 50 mV for a reference device.
incrementing in steps of $50 \mathrm{mV} .^{4}$ Figure 11.10 shows the results for $W_{R E F} / L_{\text {min }}=5 \mu \mathrm{~m} / 40 \mathrm{~nm}$. (Here, $V_{G S}-V_{T H}$ increments from 50 mV to 350 mV for clarity.)

Step 3 Bearing in mind that our example specifies $I_{D}=0.5 \mathrm{~mA}$ and $V_{D S, \min }=200 \mathrm{mV}$, we draw a vertical line at $V_{D S}=200 \mathrm{mV}$ (Fig. 11.10) and find its intersection with the plots. Which plot should we select? If the device obeyed the square law, we would choose the plot for $V_{G S}-V_{T H}=V_{D S, \text { min }}=200 \mathrm{mV}$. However, the short-channel device remains in saturation even for $V_{G S}-V_{T H}=350 \mathrm{mV}$ at $V_{D S}=200 \mathrm{mV}$. The situation is therefore more complex, but let us proceed with $V_{G S}-V_{T H}=200 \mathrm{mV}$ for now.

Step 4 The foregoing procedure has yielded, for the reference transistor, one operating point that satisfies the $V_{D S}$ requirement. The drain current, $I_{D, R E F}$, however, may not be close to the necessary value, 0.5 mA in our example. What shall we do here? We must now scale the width of the transistor and hence its drain current. Since in Fig. 11.10, $I_{D, R E F} \approx 100 \mu \mathrm{~A}$, we choose a transistor width of $(500 \mu \mathrm{~A} / 100 \mu \mathrm{~A}) \times W_{R E F}=5 W_{R E F}=25 \mu \mathrm{~m}$.

How much is the transconductance of the earlier reference transistor? We recognize from the plots of Fig. 11.10 that, as $V_{G S}-V_{T H}$ is incremented from 200 mV to $250 \mathrm{mV}, I_{D}$ changes by about $100 \mu \mathrm{~A}$. Thus, $g_{m} \approx 100 \mu \mathrm{~A} / 50 \mathrm{mV}=2 \mathrm{mS}$. Since the change in the overdrive is not much less than the initial value of 200 mV , we may seek a more accurate value for $g_{m}$. To this end, let us return to the reference transistor and, using simulations, plot its transconductance as a function of $V_{G S}-V_{T H}$ with $V_{D S}=200 \mathrm{mV}$. For a square-law device, this plot would be a straight line, $g_{m}=\mu_{n} C_{o x}\left(W_{R E F} / L_{\text {min }}\right)\left(V_{G S}-V_{T H}\right)$, but with short-channel effects, $g_{m}$ eventually saturates. Shown in Fig. 11.11, the result predicts $g_{m}=1.5 \mathrm{mS}$ for $V_{G S}-V_{T H}=200 \mathrm{mV}$. Now, if both the width and the drain current are scaled up by a factor of 5 , then $g_{m}$ also rises by the same factor (Example 11.2), reaching a value of 7.5 mS . As indicated in Table 11.1, if this transconductance is insufficient, $W / L$ must be increased further.

With the $I_{D}$ and $g_{m}$ plots obtained for the reference device, we can readily perform scaling to determine the width and transconductance of other transistors in a circuit. The key point here is that the $I_{D}$ and $g_{m}$ simulations are performed only once (for a given channel length) but serve most of our design work.

image_name:Figure 11.11
description:The graph in Figure 11.11 is a plot of transconductance ($g_{m}$) versus overdrive voltage ($V_{GS} - V_{TH}$) for a specific transistor configuration. The x-axis represents the overdrive voltage, $V_{GS} - V_{TH}$, measured in volts (V), ranging from 0 to 0.6 V. The y-axis represents the transconductance, $g_{m}$, measured in millisiemens (mS), ranging from 0 to 6 mS.

The graph shows a curve that begins near the origin and rises steeply, indicating that as the overdrive voltage increases, the transconductance also increases. The curve starts with a steep slope, showing a rapid increase in transconductance for small increases in overdrive voltage. This behavior continues up to around 0.4 V, where the curve begins to level off, indicating a saturation region where further increases in overdrive voltage result in smaller increases in transconductance.

Key features of the graph include:
- A steep initial increase in $g_{m}$ as $V_{GS} - V_{TH}$ increases from 0 to about 0.3 V.
- A transition region from about 0.3 V to 0.4 V where the rate of increase in $g_{m}$ begins to slow.
- A saturation region beyond 0.4 V where $g_{m}$ approaches a maximum value of just over 5 mS.

The graph is significant for understanding how changes in overdrive voltage affect the transconductance of a transistor, which is crucial for designing circuits that require specific transconductance values.

Figure 11.11 Dependence of $g_{m}$ on overdrive for $W / L=5 \mu \mathrm{~m} / 40 \mathrm{~nm}$ and $V_{D S}=200 \mathrm{mV}$.
Can we choose a higher overdrive voltage in Fig. 11.10? Suppose we select $V_{G S}-V_{T H}=250 \mathrm{mV}$, obtaining $I_{D}=200 \mu \mathrm{~A}$ for the reference transistor and a transconductance of about 2.3 mS from Fig. 11.11. If scaled up to $12.5 \mu \mathrm{~m}$ so as to carry $500 \mu \mathrm{~A}$, the transistor exhibits a transconductance of $2.5 \times 2.3 \mathrm{mS}=5.75 \mathrm{mS}$, a value less than that observed in the previous case $(7.5 \mathrm{mS})$. This occurs because $g_{m}=2 I_{D} /\left(V_{G S}-V_{T H}\right)$ in saturation. To obtain a high transconductance, therefore, we typically choose $V_{G S}-V_{T H} \approx V_{D S, \text { min }}$ even though it translates to a wider transistor.

#### Example 11.4

The circuit shown in Fig. 11.12 must be designed for a power budget of 1 mW and a peak-to-peak output voltage swing of 0.8 V . Assuming $L=40 \mathrm{~nm}$ for $M_{1}$, compute its required width. Can the transistor provide a transconductance of $1 /(50 \Omega)$ ?
image_name:Figure 11.12
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vout}
name: VDD, type: VoltageSource, value: 1V, ports: {Np: VDD, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
]
extrainfo:The circuit is a common-source NMOS amplifier with a drain resistor RD. The NMOS transistor M1 is used for amplification, and the circuit is powered by a 1V supply. The output voltage swing is between 0.2V and 1V.
image_name:Figure 11.12
description:The graph depicted is a time-domain waveform illustrating the output voltage, \( V_{out} \), of a transistor circuit over time. The waveform is a sinusoidal signal with a peak-to-peak voltage swing of 0.8 V, oscillating between 1 V and 0.2 V. The horizontal axis represents time, typically in seconds or a submultiple thereof, while the vertical axis represents the output voltage in volts.

Type of Graph and Function
- **Graph Type:** Time-domain waveform
- **Function Type:** Sinusoidal signal

Axes Labels and Units
- **Horizontal Axis:** Time (units not specified, but generally in seconds)
- **Vertical Axis:** Voltage (in volts)
- **Voltage Range:** 0.2 V to 1 V

Overall Behavior and Trends
- The waveform displays a sinusoidal behavior, indicating periodic oscillations in the output voltage.
- The amplitude of the waveform is consistent, suggesting stable operation within the specified voltage range.

Key Features and Technical Details
- **Peak Voltage:** 1 V
- **Minimum Voltage:** 0.2 V
- **Peak-to-Peak Voltage Swing:** 0.8 V
- The waveform remains within the saturation region of the transistor, as indicated by the context, ensuring \( M_1 \) remains in saturation.

Annotations and Specific Data Points
- The waveform is annotated with horizontal dashed lines at 1 V and 0.2 V, marking the peak and minimum voltage levels, respectively.

This graph is crucial for analyzing the performance of the transistor \( M_1 \) in maintaining the required output voltage swing while staying within the power budget and saturation region.

#### Solution

The power budget along with $V_{D D}=1 \mathrm{~V}$ translates to a drain bias current of 1 mA . For the circuit to accommodate an output swing of $0.8 \mathrm{~V}, M_{1}$ must remain in saturation as $V_{D S}$ falls to 0.2 V . We return to the $I_{D}-V_{D S}$ characteristics of Fig. 11.10 and recall that $I_{D, R E F} \approx 100 \mu \mathrm{~A}$ for $V_{D S}=V_{G S}-V_{T H}=200 \mathrm{mV}$. We must therefore scale $W_{R E F}$ up by a factor of $1 \mathrm{~mA} / 0.1 \mathrm{~mA}$, obtaining $W / L=50 \mu \mathrm{~m} / 40 \mathrm{~nm}$. The transconductance is also multiplied by this factor, reaching $15 \mathrm{mS}=1 /(67 \Omega)$. Note that these results are independent of the value of $R_{D}$.

We conclude that, if the transistor is designed simply to satisfy this example's $I_{D}$ and $V_{D S}$ specifications, then it does not necessarily achieve a transconductance of $1 /(50 \Omega)$.

In addition to $I_{D}, V_{G S}-V_{T H}$, and $g_{m}$, the output impedance of the transistors also becomes important in many analog circuits. As explained in Chapter 17, $r_{O}$ cannot be expressed as $1 /\left(\lambda I_{D}\right)$ for short-channel devices. The value of $r_{O}$ can be estimated from the slope of the $I_{D}$ characteristics in Fig. 11.2, but for convenience and accuracy, we use simulations to plot $r_{O}$ for the reference transistor as a function of $I_{D}$ (Fig. 11.13).
image_name:Figure 11.13
description:Figure 11.13 is a graph illustrating the output resistance \( r_O \) of a 5-\( \mu \)m / 40-nm NMOS device as a function of the drain current \( I_D \). The graph is a two-dimensional plot with the x-axis labeled \( I_D \) (mA) representing the drain current in milliamperes, ranging from 0 to 0.5 mA. The y-axis is labeled \( r_O \) (k\( \Omega \)), indicating the output resistance in kilo-ohms, ranging from 0 to 14 k\( \Omega \).

The graph shows a downward-sloping curve, indicating that as the drain current \( I_D \) increases, the output resistance \( r_O \) decreases. The curve starts at an output resistance of approximately 12 k\( \Omega \) when the drain current is near 0 mA and decreases to about 3 k\( \Omega \) as the drain current approaches 0.5 mA.

The graph has a smooth, continuous curve with no sharp transitions or discontinuities, suggesting a consistent relationship between the drain current and output resistance over the range of values plotted. The trend is characterized by a steep decrease in resistance at lower drain currents, gradually leveling off as the current increases.

Figure 11.13 Output resistance of a $5-\mu \mathrm{m} / 40-\mathrm{nm}$ NMOS device as a function of drain current.

#### Example 11.5

Determine the output resistance of $M_{1}$ in Example 11.4.

#### Solution

The reference transistor in Example 11.4 carries a current of $100 \mu \mathrm{~A}$, exhibiting an output resistance of $8 \mathrm{k} \Omega$. Since both the width and the drain current are scaled up by a factor of 10 , the output resistance drops by the same factor, falling to $800 \Omega$.

### 11.4.2 Design for Given $g_{m}$ and $I_{D}$

In many analog circuits, a given transistor must provide sufficient transconductance while consuming minimal power. We thus begin with a specified transconductance, $g_{m 1}$, and an upper limit for the drain bias current, $I_{D 1}$, seek the corresponding values of $W / L$ and $V_{G S}-V_{T H}$. In this section, we assume that $g_{m 1}=10 \mathrm{mS}$ and $I_{D 1}=1 \mathrm{~mA}$. Of course, our first task is to determine whether $g_{m 1}$ can be obtained at all with $I_{D} \leq I_{D 1}$. The maximum $g_{m}$ occurs in the subthreshold region (if $W / L$ is large) and is given by $I_{D} /\left(\xi V_{T}\right)$, where $\xi \approx 1.5$ (Chapter 2). For example, if $I_{D}=1 \mathrm{~mA}$, then $g_{m}$ cannot exceed 26 mS at the room temperature.

Since in our example, $g_{m 1}<I_{D 1} /\left(\xi V_{T}\right)$, we can proceed to design the transistor. The reader is encouraged to first read Example 11.3 carefully.

Step 1 Using simulations, we plot $g_{m}$ as a function of $I_{D}$ for a reference transistor, e.g., with $W_{R E F} / L_{\text {min }}=5 \mu \mathrm{~m} / 40 \mathrm{~nm}$ (Fig. 11.14).
Step 2 We identify the point $\left(I_{D 1}, g_{m 1}\right)$ on the $g_{m}-I_{D}$ plane and draw a line through the origin and this point, obtaining the intersection at $\left(I_{D, R E F}, g_{m, R E F}\right)=(240 \mu \mathrm{~A}, 2.4 \mathrm{mS})$ and a corresponding overdrive.

Step 3 We multiply $W_{R E F}$ by $g_{m 1} / g_{m, R E F}=4.2$ so as to travel on the straight line to point $\left(I_{D 1}, g_{m 1}\right)$ while maintaining the same overdrive (Example 11.3). This completes the design of the transistor.

The above procedure elicits two questions. First, does the straight line passing through the origin and $\left(I_{D 1}, g_{m 1}\right)$ always intersect the $g_{m}-I_{D}$ plot? If we consider a square-law device in strong inversion, then $g_{m}=\sqrt{2 \mu_{n} C_{o x}(W / L) I_{D}}$ has a slope of infinity at the origin, guaranteeing an intersection point. In the
image_name:Figure 11.14 Transconductance as a function of $I_{D}$ for $W / L=5 \mu \mathrm{~m} / 40 \mathrm{~nm}$.
description:The graph titled 'Figure 11.14 Transconductance as a function of I_D' is a plot showing the relationship between the transconductance \( g_m \) and the drain current \( I_D \) for a MOSFET device.

**Type of Graph and Function:**
This is a linear plot depicting a characteristic curve of a MOSFET device.

**Axes Labels and Units:**
- The horizontal axis represents the drain current \( I_D \), measured in milliamperes (mA), ranging from 0 to 0.5 mA.
- The vertical axis represents the transconductance \( g_m \), measured in millisiemens (mS), ranging from 0 to 4 mS.

**Overall Behavior and Trends:**
The graph shows a curve that starts at the origin (0,0) and rises as \( I_D \) increases. Initially, the curve increases steeply, indicating a sharp rise in \( g_m \) with small increases in \( I_D \). As \( I_D \) continues to increase, the slope of the curve decreases, showing a trend towards saturation.

**Key Features and Technical Details:**
- At low values of \( I_D \), the curve is steep, indicating high sensitivity of \( g_m \) to changes in \( I_D \).
- As \( I_D \) approaches 0.3 mA, the curve begins to flatten, suggesting the onset of saturation.
- The graph includes a straight line that intersects the curve, representing a specific design point or operating condition.

**Annotations and Specific Data Points:**
- A notable point on the curve is around \( I_D = 0.3 \) mA and \( g_m = 2.5 \) mS, where the straight line intersects the curve. This point may represent a typical operating condition for the device.
- The graph is marked with dashed grid lines for ease of reading specific values on the axes.

image_name:Figure 11.15 Unachievable g_m region
description:The graph in Figure 11.15 is a plot of transconductance \( g_m \) as a function of drain current \( I_D \). The axes are labeled with \( g_m \) on the vertical axis and \( I_D \) on the horizontal axis. The plot is divided into two main regions: weak inversion and strong inversion, which are typical operating conditions for transistors.

**Axes Labels and Units:**
- The vertical axis represents transconductance \( g_m \) and is likely in units of millisiemens (mS), although the specific unit is not labeled.
- The horizontal axis represents drain current \( I_D \) and is likely in units of milliamperes (mA), although the specific unit is not labeled.

**Overall Behavior and Trends:**
- The graph shows a curve that starts at the origin and increases as \( I_D \) increases.
- In the weak inversion region, the curve starts with a steep slope, indicating a proportional relationship between \( g_m \) and \( I_D \).
- As the curve progresses into the strong inversion region, the slope decreases, suggesting a less direct relationship between \( g_m \) and \( I_D \).

**Key Features and Technical Details:**
- There is a dashed line that extends from the origin upwards, representing the boundary between weak and strong inversion regions.
- The curve intersects this dashed line at a point labeled \( I_{D1} \), which marks the transition from weak to strong inversion.
- A shaded gray region is present above the curve in the weak inversion area, indicating an unachievable \( g_m \) region.

**Annotations and Specific Data Points:**
- The graph is annotated with labels for weak and strong inversion regions.
- The point of intersection at \( I_{D1} \) is marked, highlighting the transition between the two regions.
- A horizontal dashed line labeled \( g_{m1} \) represents a specific transconductance value, which intersects the curve in the strong inversion region.

This graph effectively illustrates the relationship between \( g_m \) and \( I_D \) across different operating regions of a transistor, with specific emphasis on the transition from weak to strong inversion and the unachievable \( g_m \) values in the gray region.

subthreshold region, on the other hand, $g_{m} \propto I_{D}$ (Fig. 11.15), which means that the $\left(I_{D}, g_{m}\right)$ combinations in the gray region are not achievable.

The second question is, what if $\left(V_{G S}-V_{T H}\right)_{R E F}$ is excessively large? As stipulated in Table 11.1, we must then increase $W$ further, but by what factor? Suppose, as shown in Fig. 11.16, an overdrive of $\left(V_{G S}-V_{T H}\right)_{2}<\left(V_{G S}-V_{T H}\right)_{R E F}$ is desired. We then find the corresponding current, $I_{D 2}$, and transconductance, $g_{m 2}$, on the $g_{m}-I_{D}$ plane. Next, we draw a line through the origin and the point ( $I_{D 2}$, $g_{m 2}$ ) and continue to $I_{D}=I_{D 1}$, i.e., we multiply $W_{R E F}$ by $I_{D 1} / I_{D 2}$. The resulting width guarantees an overdrive of $\left(V_{G S}-V_{T H}\right)_{2}$ at a drain current of $I_{D 1}$ and provides a transconductance of at least $g_{m 1}$. The new transconductance, $g_{m 1}^{\prime}$, is inevitably greater because the width has been increased beyond $g_{m 1} / g_{m, R E F}\left(=I_{D 1} / I_{D, R E F}\right)$.

### 11.4.3 Design for Given $g_{m}$ and $V_{D S, m i n}$

In some designs, the transconductance is dictated by some performance requirements (voltage gain, noise, etc.) and the minimum $V_{D S}$ by the voltage headroom—with no explicit specification of $I_{D}$. Of course, each circuit eventually faces a power budget and hence an upper bound on its bias current(s).

The design procedure for obtaining a transconductance of $g_{m 1}$ at $V_{D S, \min }$ in this case is as follows.
Step 1 We use simulations to plot the $g_{m}$ as a function of $V_{G S}-V_{T H}$ for the reference transistor (Fig. 11.17). Now, we select $\left(V_{G S}-V_{T H}\right)_{1}=V_{D S, \min }$ and obtain the corresponding transconductance, $g_{m, R E F}$. In this case, it is helpful to plot $I_{D}$ on the same plane and find $I_{D, R E F}$ at $\left(V_{G S}-V_{T H}\right)_{1}$.
image_name:Figure 11.16 Modification of transistor design for a lower overdrive.
description:The graph in Figure 11.16 is a plot showing the relationship between the transconductance \( g_m \) and the overdrive voltage \( V_{GS} - V_{TH} \) for a reference transistor. It is a two-dimensional plot with the following characteristics:

1. **Axes Labels and Units:**
- The horizontal axis represents the overdrive voltage \( V_{GS} - V_{TH} \).
- The vertical axis represents the transconductance \( g_m \).
- Both axes are marked with reference points and values, but no specific units are provided.

2. **Overall Behavior and Trends:**
- The graph shows a curve that initially rises as \( V_{GS} - V_{TH} \) increases, indicating an increase in transconductance \( g_m \).
- The curve appears to have a gentle slope, suggesting a non-linear relationship between \( V_{GS} - V_{TH} \) and \( g_m \).
- There is a peak or maximum point on the curve, beyond which the transconductance decreases with further increase in \( V_{GS} - V_{TH} \).

3. **Key Features and Technical Details:**
- Several important points are marked on the graph: \((V_{GS} - V_{TH})_{REF}\) and \((V_{GS} - V_{TH})_2\), which correspond to specific overdrive voltages.
- Corresponding transconductance values \( g_{m,REF} \), \( g_{m1} \), \( g_{m2} \), and \( g'_{m1} \) are indicated by horizontal dashed lines.
- Current values \( I_{D,REF} \), \( I_{D1} \), and \( I_{D2} \) are marked on the horizontal axis, corresponding to the respective transconductance values.

4. **Annotations and Specific Data Points:**
- The point \((I_{D1}, g_{m1})\) is highlighted, indicating a specific operating condition on the curve.
- Dotted lines connect these critical points to the axes, providing a visual guide to the relationships between \( V_{GS} - V_{TH} \), \( g_m \), and \( I_D \).
- The graph serves as a tool for determining the necessary transistor width scaling to achieve a desired transconductance \( g_{m1} \) from a reference \( g_{m,REF} \).

image_name:Figure 11.17 Calculation of $g_{m, R E F}$ for a given overdrive.
description:The graph in Figure 11.16 is a plot used to illustrate the modification of transistor design for achieving a lower overdrive voltage. This is a two-dimensional graph with the x-axis representing \( V_{GS} - V_{TH} \), which is the gate-source voltage minus the threshold voltage, and the y-axis representing both transconductance \( g_m \) and drain current \( I_D \).

Axes and Units:
- **X-axis**: Labeled as \( V_{GS} - V_{TH} \), representing the overdrive voltage. This axis is linear and extends to the right.
- **Y-axis**: Represents two parameters:
- **Upper part**: \( g_m \), the transconductance, with a reference level \( g_{m,REF} \) marked by a dotted horizontal line.
- **Lower part**: \( I_D \), the drain current, with a reference level \( I_{D,REF} \) also marked by a dotted horizontal line.

Overall Behavior and Trends:
- The graph shows two distinct curves:
- **Transconductance Curve (Upper)**: This curve starts from the origin and rises linearly, indicating that the transconductance \( g_m \) increases with increasing \( V_{GS} - V_{TH} \).
- **Drain Current Curve (Lower)**: This curve starts from the origin and decreases, suggesting that the drain current \( I_D \) reduces as \( V_{GS} - V_{TH} \) increases.

Key Features and Technical Details:
- **Dotted Lines**: There are horizontal dotted lines indicating the reference values \( g_{m,REF} \) and \( I_{D,REF} \), which are essential for understanding the scaling required for achieving the desired transconductance \( g_{m1} \).
- **Intersection Points**: The dotted lines intersect the y-axis, marking the reference values for \( g_m \) and \( I_D \).
- **Critical Point**: The graph highlights a specific point \((V_{GS} - V_{TH})_1\) on the x-axis, which is connected by vertical dotted lines to the curves, indicating the specific operating condition for the desired transconductance \( g_{m1} \).

Annotations and Specific Data Points:
- The graph serves as a visual guide for scaling the transistor width to achieve a desired transconductance \( g_{m1} \) from a reference \( g_{m,REF} \), with the understanding that \( I_D \) will scale by the same factor. This is crucial for designing transistors with specific electrical characteristics.

Step 2 To reach the required transconductance, $g_{m 1}$, we scale the transistor width up by a factor of $g_{m 1} / g_{m, R E F}$. Note that $I_{D}$ scales by the same factor.

These two steps complete the design, but what if the resulting $I_{D}$ is excessively large? We can return to Case II in Sec. 11.4.2 and redesign for a given $g_{m}$ and $I_{D}$. The device is now wider and has a smaller transconductance.

As can be seen from our procedures in this section, we have portrayed the overdrive voltage (or $V_{D, s a t}$ ) as an indispensable dimension in our device design. This is because today's low supply voltages have made the problem of headroom more severe than ever.

### 11.4.4 Design for a Given $g_{m}$

Our approach has assumed that the drain current and the overdrive voltage are specified and the other device parameters must be determined. Since power consumption and voltage headroom prove critical in today's analog design, this assumption holds in most cases. However, suppose a design problem specifies only the transconductance, and we wish to compute the remaining parameters. How do we select the transistor's drain current, overdrive voltage, and dimensions?

Two scenarios must be envisaged. (1) We select a certain $W / L$ and raise $I_{D}$ until we obtain the desired transconductance, $g_{m 1}$. In this case, the required $I_{D}$, and hence the power consumption, may be excessive. More important, the overdrive voltage may be unacceptably large, leaving little headroom for voltage swings. (2) We select a reasonable value for $I_{D}$ (perhaps according to a power budget) and
increase $W / L$ to obtain $g_{m 1}$. In this case, however, we may not be able to reach $g_{m 1}$; increasing $W / L$ (and hence decreasing $V_{G S}$ ) eventually drives the device into the subthreshold region, where $g_{m}$ cannot exceed $I_{D} /\left(\xi V_{T}\right)$. This means that the selected current is insufficient, i.e., we should always briefly check to see if the upper limit given by $I_{D} /\left(\xi V_{T}\right)$ can be met with the current budget.

The above scenarios indicate the need for a systematic approach to the selection of device parameters when only $g_{m 1}$ is known. To this end, we return to the concept of the reference device and, using simulations, construct two plots for it. Shown in Fig. 11.18, the two represent $g_{m}$ and $V_{G S}-V_{T H}$ as a function of $I_{D} .{ }^{5}$ We begin by selecting a reasonable value for $V_{G S}-V_{T H}$, e.g., 200 mV , which points to $I_{D, R E F}$ and $g_{m, R E F}$. Now, we scale the width and the drain current by a factor of $g_{m 1} / g_{m, R E F}$.
image_name:Figure 11.18 Translation of overdrive to $g_{m, R E F}$.
description:The graph in Figure 11.18 is a dual plot that represents the relationship between transconductance ($g_m$) and the overdrive voltage ($V_{GS} - V_{TH}$) as a function of the drain current ($I_D$). It is a parametric plot where the $g_m$ and $V_{GS} - V_{TH}$ are plotted against $I_D$ on a common axis.

1. **Type of Graph and Function:**
- The graph is a parametric plot showing $g_m$ and $V_{GS} - V_{TH}$ versus $I_D$.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as $I_D$, representing the drain current.
- The vertical axis has two parameters:
- $g_m$, the transconductance.
- $V_{GS} - V_{TH}$, the overdrive voltage, marked at 200 mV.

3. **Overall Behavior and Trends:**
- The plot shows two curves diverging from a common point on the $I_D$ axis.
- The curve for $g_m$ increases as $I_D$ increases, indicating a direct relationship between the two.
- The curve for $V_{GS} - V_{TH}$ decreases as $I_D$ increases, showing an inverse relationship.

4. **Key Features and Technical Details:**
- The reference point $(I_{D, REF}, g_{m, REF})$ is marked, representing a specific operating condition.
- The width of the device is indicated as $W = W_{REF}$, suggesting that the width remains constant for this reference condition.

5. **Annotations and Specific Data Points:**
- A specific overdrive voltage of 200 mV is annotated on the $V_{GS} - V_{TH}$ curve.
- The reference transconductance $g_{m, REF}$ is marked on the $g_m$ curve.
- The intersection of these parameters at $I_{D, REF}$ is highlighted, indicating a balanced operating point for the reference device.

What if the foregoing method yields an unacceptably high $I_{D}$ ? We can choose a smaller overdrive, e.g., 150 mV , and repeat the earlier steps.

### 11.4.5 Choice of Channel Length

If the selection of $I_{D}, V_{G S}-V_{T H}$, and $g_{m}$ does not yield a sufficiently high $r_{O}$, we must increase the length of the transistor. Of course, to maintain the same drain current, overdrive voltage, and $g_{m}$, the width must also be increased proportionally. However, such scaling of the length and the width is not straightforward because, as the drawn length is increased from $L_{\text {min }}$ to, say, $2 L_{\text {min }}$, the effective length rises from $L_{\text {min }}-2 L_{D}$ to $2 L_{\text {min }}-2 L_{D}$, i.e., by a factor of less than 2 . For this reason, we must use simulations to construct the $I_{D}-V_{D S}, g_{m}$ and $r_{O}$ characteristics for several channel lengths, e.g., 60 nm , 80 nm , and 100 nm (drawn values).

## 11.5 ■ Op Amp Design Examples

In this section, we wish to repeat the op amp design examples studied in Chapter 9 in 40-nm technology. We target the following typical specifications:

- Differential Output Voltage Swing $=1 \mathrm{~V}_{p p}$
- Power Consumption $=2 \mathrm{~mW}$
- Voltage Gain $=500$
- Supply Voltage $=1 \mathrm{~V}$

[^81]The single-ended output swing of $0.5 \mathrm{~V}_{\mathrm{pp}}$ is small enough to make telescopic or folded-cascode op amps a plausible choice. We therefore explore these topologies before deciding whether a two-stage op amp is necessary.

A few notes about our transistor sizing methodology are warranted. We wish to begin with the minimum allowable width and length unless otherwise dictated by current, transconductance, $V_{D, s a t}$, output resistance, or other requirements. Interestingly, in the designs pursued in this chapter, all transistor widths are greater than the minimum value. Also, for simplicity, we may scale the drawn $W$ and $L$ by the same factor even though the effective $W / L$ does not remain exactly constant.

### 11.5.1 Telescopic Op Amp

Can a telescopic-cascode op amp topology meet the above specifications? In this section, we explore this possibility. It may not, but we will learn a great deal. Consider the circuit shown in Fig. 11.19. Of the total supply current of 2 mA , we allow $50 \mu \mathrm{~A}$ for $I_{R E F 1}, 50 \mu \mathrm{~A}$ for $I_{R E F 2}$, and 0.95 mA for each branch of the differential pair. We must now allocate the transistor drain-source voltages so as to accommodate a single-ended peak-to-peak output swing of 0.5 V ; i.e., we must distribute the remaining 0.5 V over $M_{9}$, $M_{1,2}, M_{3,4}, M_{5,6}$, and $M_{7,8}$. Let us allow a $V_{D S}$ of 100 mV for each—even though the PMOS devices have a lower mobility. With the bias currents and overdrives known, we can determine the $W / L$ 's by examining the transistor I/V characteristics.
image_name:Figure 11.19 Telescopic-cascode op amp
description:
[
name: Mb2, type: PMOS, ports: {S: VDD, D: Y, G: Y}
name: M7, type: PMOS, ports: {S: VDD, D: ssd7, G: X}
name: M8, type: PMOS, ports: {S: VDD, D: sbd8, G: X}
name: M5, type: PMOS, ports: {S: ssd7, D: Voutp, G: Vb2}
name: M6, type: PMOS, ports: {S: sbd8, D: Voutn, G: Vb2}
name: M1, type: NMOS, ports: {S: GND, D: diss3, G: Vinp}
name: M2, type: NMOS, ports: {S: GND, D: d2s4, G: Vinn}
name: M3, type: NMOS, ports: {S: diss3, D: Voutp, G: Vb1}
name: M4, type: NMOS, ports: {S: d2s4, D: Voutn, G: Vb1}
name: M9, type: NMOS, ports: {S: GND, D: P, G: X}
name: Mb1, type: NMOS, ports: {S: GND, D: X, G: X}
]
extrainfo:The circuit is a telescopic-cascode operational amplifier. It includes differential input pair M1 and M2, cascode transistors M3 and M4, and current mirror loads M5 and M6. The PMOS transistors M7 and M8 act as cascode current sources. Biasing is provided by Mb1 and Mb2. The amplifier is designed to achieve high gain with a single-ended output swing of 0.5 V.

Before delving into details, however, we should pause and think about the feasibility of the design, specifically in terms of the required voltage gain. We make three observations: (1) for $L=40 \mathrm{~nm}$, the intrinsic gain, $g_{m} r_{O}$, of NMOS devices is around 7 to 10 and that of PMOS devices around 5 to 7, (2) for reasonable device dimensions, it is difficult to raise $g_{m} r_{O}$ beyond 10 for PFETs (unless we allow longer lengths and hence lower speeds), and (3) if we approximate $g_{m}$ as $2 I_{D} /\left(V_{G S}-V_{T H}\right)=$ $2 \times 0.95 \mathrm{~mA} / 100 \mathrm{mV}=19 \mathrm{mS}$, we estimate $r_{O} \approx 530 \Omega$ from $g_{m} r_{O} \approx 10$.

Let us now apply the foregoing values to the telescopic topology in Fig. 11.19. If $g_{m 1,2} \approx 19 \mathrm{mS}$, then for the gain, $G_{m} R_{\text {out }}$, to reach 500 , the op amp output impedance must exceed $26 \mathrm{k} \Omega$. equal to $\left(g_{m 5,6} r_{O 5,6}\right) r_{O 7,8}$, pointing to a serious limitation. However, with $g_{m 3,4} r_{O 3,4} \approx 10$ and $r_{O 7,8} \approx 530 \Omega$ (from the third observation above), we have $\left(g_{m 3,4} r_{O 3,4}\right) r_{O 1,2} \approx 5.3 \mathrm{k} \Omega$, obtaining a voltage gain of only about 100 even if the PMOS devices have $\lambda=0$ ! This fivefold deficit makes the telescopic arrangement impractical for a gain of 500 .

Out of curiosity, we still continue with the design and see what performance we can achieve. To this end, we use simulations to construct the I/V characteristics of NMOS and PMOS devices with $L=40 \mathrm{~nm}$ and 80 nm , predicting that the minimum length exhibits an unacceptably low $r_{O}$ and $g_{m} r_{O}$. The simulation parameters must also ensure that the devices remain in saturation for $\left|V_{D S}\right| \geq 100 \mathrm{mV}$. Given that the
threshold and the overdrive elude a clear definition in nanometer technologies, we must adjust $V_{G S}$ in simulations to ensure saturation.

The results are plotted in Fig. 11.20(a) for $(W / L)_{N}=5 \mu \mathrm{~m} / 40 \mathrm{~nm}$ and $10 \mu \mathrm{~m} / 80 \mathrm{~nm}$ with $V_{G S}=$ 300 mV , and in Fig. 11.20(b) for $(W / L)_{P}=5 \mu \mathrm{~m} / 40 \mathrm{~nm}$ and $5 \mu \mathrm{~m} / 80 \mathrm{~nm}$ with $V_{G S}=-400 \mathrm{mV}{ }^{6}$ We should make some remarks. First, it is difficult to distinguish between triode and saturation regions, especially for PFETs. In fact, the $40-\mathrm{nm}$ PMOS device behaves almost as a resistor and displays a
image_name:(a)
description:The graph labeled (a) is an \(I_D-V_{DS}\) characteristic plot for an NMOS device. The x-axis represents the drain-source voltage \(V_{DS}\) in volts, ranging from 0 to 0.4 V. The y-axis represents the drain current \(I_D\) in microamperes (\(\mu A\)), ranging from 0 to 40 \(\mu A\). The graph is plotted with two different \(W/L\) ratios: 5 \(\mu m/40\) nm (black plot) and 10 \(\mu m/80\) nm (gray plot).

**Overall Behavior and Trends:**
- For both \(W/L\) ratios, the drain current \(I_D\) increases with increasing \(V_{DS}\), showing a positive trend.
- The black plot (5 \(\mu m/40\) nm) shows a steeper increase compared to the gray plot (10 \(\mu m/80\) nm), indicating a higher current for the same \(V_{DS}\) values.

**Key Features and Technical Details:**
- The black plot starts at the origin and rises sharply, indicating a rapid increase in \(I_D\) as \(V_{DS}\) increases.
- The gray plot also starts at the origin but rises more gradually compared to the black plot.
- Both plots exhibit a linear region as \(V_{DS}\) approaches 0.4 V, suggesting a transition towards saturation.

**Annotations and Specific Data Points:**
- There are no specific annotations or marked data points, but the gridlines provide a clear reference for estimating values at particular \(V_{DS}\) and \(I_D\) points.

This graph helps illustrate the effect of different \(W/L\) ratios on the \(I_D-V_{DS}\) characteristics of an NMOS device, with higher \(W/L\) ratios resulting in lower current for the same voltage.
image_name:(b)
description:The graph in Figure 11.20(b) is an $I_D$-$V_{DS}$ characteristic plot for a PMOS device. The x-axis represents the drain-source voltage, $V_{DS}$, measured in volts (V), ranging from -0.4 V to 0 V. The y-axis represents the drain current, $I_D$, measured in microamperes (µA), ranging from -60 µA to 0 µA.

This plot includes two curves, corresponding to different $W/L$ ratios for the PMOS device. The black curve represents a $W/L$ ratio of $5 \mu \text{m} / 40 \text{nm}$, while the gray curve represents a $W/L$ ratio of $5 \mu \text{m} / 80 \text{nm}$. Both curves are plotted with a gate-source voltage, $V_{GS}$, of -400 mV.

**Overall Behavior and Trends:**
- Both curves show a generally decreasing trend in $I_D$ as $|V_{DS}|$ increases from 0 V to -0.4 V, indicating typical PMOS behavior where the current magnitude increases as the drain-source voltage becomes more negative.
- The black curve ($5 \mu \text{m} / 40 \text{nm}$) shows a more pronounced increase in current magnitude compared to the gray curve ($5 \mu \text{m} / 80 \text{nm}$).

**Key Features and Technical Details:**
- The curves start at $I_D = 0$ µA when $V_{DS} = 0$ V and decrease to approximately -50 µA for the black curve and -30 µA for the gray curve as $V_{DS}$ approaches -0.4 V.
- The slope of the black curve is steeper compared to the gray curve, indicating a lower output impedance for the device with a $W/L$ ratio of $5 \mu \text{m} / 40 \text{nm}$.

**Annotations and Specific Data Points:**
- The graph is marked with dashed gridlines to aid in reading specific data points.
- No additional annotations or markers are present, but the general shape of the curves suggests typical PMOS characteristics with different $W/L$ ratios affecting the slope and current magnitude.

Figure 11.20 $I_{D}-V_{D S}$ characteristics for (a) an NMOS device with $V_{G S}=300 \mathrm{mV}$ and $W / L=5 \mu \mathrm{~m} / 40 \mathrm{~nm}$ (black plot) or $10 \mu \mathrm{~m} / 80 \mathrm{~nm}$ (gray plot), and (b) a PMOS device with $V_{G S}=-400 \mathrm{mV}$ and $W / L=5 \mu \mathrm{~m} / 40 \mathrm{~nm}$ (black plot) or $5 \mu \mathrm{~m} / 80 \mathrm{~nm}$ (gray plot).

decreasing output impedance as $\left|V_{D S}\right|$ approaches $400 \mathrm{mV} .^{7}$ For the other three characteristics, we can roughly identify a "knee" point beyond which the slope falls considerably. The gate-source voltages have been chosen to place this point below $\left|V_{D S}\right|=100 \mathrm{mV}$.

Second, at $V_{D S}=100 \mathrm{mV}$, the $10-\mu \mathrm{m} / 80-\mathrm{nm}$ NMOS transistor provides an output resistance of $22.8 \mathrm{k} \Omega$ and a drain current of $16 \mu \mathrm{~A}$. If scaled up to carry $950 \mu \mathrm{~A}$ with the same terminal voltages, the device exhibits an $r_{O}$ of $385 \Omega$ ! Similarly, the $5-\mu \mathrm{m} / 80-\mathrm{nm}$ PMOS transistor has an $r_{O}$ of $18.45 \mathrm{k} \Omega$ at $V_{D S}=-100 \mathrm{mV}$ with $I_{D}=15 \mu \mathrm{~A}$, thus offering $r_{O}=290 \Omega$ if scaled up to carry $950 \mu \mathrm{~A}$. These very low $r_{O}$ values are quite discouraging, but we will continue to explore.

We now scale the NMOS and PMOS device widths to accommodate a drain current of $950 \mu \mathrm{~A}$ with $V_{G S, N}=300 \mathrm{mV}, V_{G S, P}=-400 \mathrm{mV}$, and $\left|V_{D S}\right|=100 \mathrm{mV}$. The resulting design is shown in Fig. 11.21. ${ }^{8}$ As a general principle, we prefer to use minimum-length devices in the signal path so as to maximize their speed (or at least minimize their capacitances for a given $g_{m}$ ). It is surprising to see such large widths in 40-nm technology for a drain current of $950 \mu \mathrm{~A}$, an inevitable outcome of confining $\left|V_{D S}\right|$ to 100 mV .
image_name:Figure 11.21
description:
[
name: M1, type: NMOS, ports: {S: P, D: A, G: Vip}
name: M2, type: NMOS, ports: {S: P, D: B, G: Vin}
name: M3, type: NMOS, ports: {S: A, D: X, G: Vb1}
name: M4, type: NMOS, ports: {S: B, D: Y, G: Vb1}
name: M5, type: PMOS, ports: {S: VDD, D: X, G: Vb2}
name: M6, type: PMOS, ports: {S: VDD, D: Y, G: Vb2}
name: M7, type: PMOS, ports: {S: VDD, D: C, G: Vb3}
name: M8, type: PMOS, ports: {S: VDD, D: D, G: Vb3}
name: Iss, type: CurrentSource, value: 1.9 mA, ports: {Np: VDD, Nn: P}
]
extrainfo:This is a telescopic cascode operational amplifier design. The circuit uses minimum-length devices to maximize speed and minimize capacitance for a given transconductance (gm). The bias voltages are chosen to optimize the performance of the amplifier. The NMOS transistors M1 and M2 form the input differential pair, while the PMOS transistors M7 and M8 act as the load. The current source Iss provides a tail current of 1.9 mA.

Figure 11.21 First design of telescopiccascode op amp.

The bias voltages are tentatively chosen as follows: (a) the input common-mode level, $V_{C M, i n}$, is equal to 100 mV for the tail current source plus $V_{G S 1,2}\left(=300 \mathrm{mV}\right.$ ), (b) $V_{b 1}$ is equal to $V_{D 1,2}$ $(=200 \mathrm{mV})$ plus $V_{G S 3,4}(=300 \mathrm{mV})$, (c) $V_{b 2}$ is equal to $V_{D D}-\left|V_{D S 7,8}\right|-\left|V_{G S 5,6}\right|$, and (d) $V_{b 3}$ is equal to $V_{D D}-\left|V_{G S 7,8}\right|$. Upon simulating the circuit with these values, the reader may encounter a very low or high output common-mode level. This effect arises from the absence of common-mode feedback and hence the departure of $\left|I_{D 7,8}\right|$ from $1.9 \mathrm{~mA} / 2$. We avoid this issue by a slight adjustment of $V_{b 3}$ for now.

We perform a dc sweep simulation of the differential input voltage, $V_{i n}$, and examine the voltages at various nodes in Fig. 11.21 to ensure that the transistors are "healthy." Plotted in Fig. 11.22, the drain voltages of $M_{1}$ and $M_{2}$ are around 220 mV in the middle of the range. Similarly, the drain voltages of $M_{7}$ and $M_{8}$ are close to the targeted value.

### 11.5.2 Output Behavior
Next, we study the output behavior, depicted in Fig. 11.22 by $V_{X}$ and $V_{Y}$. The slope of each singleended output is approximately equal to 15 in the vicinity of $V_{i n}=0$, yielding a differential gain of 30 , far below our target. Can this design deliver a single-ended peak-to-peak swing of 0.5 V ? We note that the characterisitic becomes very nonlinear as each output rises toward 0.7 V . In fact, around this output level, the slope gives a differential gain of about 6.4 .

image_name:V_A, V_B
description:The graph consists of three subplots, each representing the behavior of voltages at different nodes (V_A, V_B), (V_X, V_Y), and (V_C, V_D) with respect to the input voltage V_in.

Type of Graph and Function:
- The graphs are linear plots showing the relationship between input voltage (V_in) and various output voltages.

Axes Labels and Units:
- **X-Axis:** Represents the input voltage (V_in) in millivolts (mV), ranging from -20 mV to 20 mV.
- **Y-Axis:** Represents the voltages at different nodes:
- Top subplot: V_A and V_B in millivolts (mV), ranging from 160 mV to 240 mV.
- Middle subplot: V_X and V_Y in millivolts (mV), ranging from 200 mV to 800 mV.
- Bottom subplot: V_C and V_D in millivolts (mV), ranging from 885 mV to 910 mV.

Overall Behavior and Trends:
- **Top Subplot (V_A, V_B):**
- V_A decreases as V_in increases, while V_B increases symmetrically.
- The intersection point occurs at V_in = 0 mV, where both V_A and V_B are approximately 210 mV.

- **Middle Subplot (V_X, V_Y):**
- V_X decreases and V_Y increases with increasing V_in.
- The intersection occurs at V_in = 0 mV, where both V_X and V_Y are approximately 500 mV.

- **Bottom Subplot (V_C, V_D):**
- V_C decreases and V_D increases as V_in increases.
- The intersection at V_in = 0 mV shows both V_C and V_D at approximately 900 mV.

Key Features and Technical Details:
- Each subplot shows a linear relationship between the input voltage and the respective output voltages, with a clear crossing point at V_in = 0 mV.
- The slopes of the lines indicate the differential gain at these nodes, which is a critical factor in analyzing the circuit's performance.

Annotations and Specific Data Points:
- The graphs are marked with gridlines and dashed lines to indicate significant intervals, aiding in precise reading of voltage values.
- The symmetry around V_in = 0 mV is a notable feature, indicating balanced behavior in the circuit's response to the input voltage.
image_name:V_X, V_Y
description:The graph in question is a set of three plots illustrating the behavior of voltages at different nodes with respect to the input voltage $V_{in}$. Each plot is a voltage transfer characteristic, showing how the output voltages $V_{A}, V_{B}$, $V_{X}, V_{Y}$, and $V_{C}, V_{D}$ change as a function of $V_{in}$.

1. **Type of Graph and Function:**
- The graphs are voltage transfer characteristics, typically used to show the relationship between input and output voltages in electronic circuits.

2. **Axes Labels and Units:**
- The x-axis for all plots is labeled $V_{in}$ (mV), representing the input voltage, with a range from -20 mV to 20 mV.
- The y-axis of the first plot is labeled $V_{A}, V_{B}$ (mV), ranging from 160 mV to 240 mV.
- The y-axis of the second plot is labeled $V_{X}, V_{Y}$ (mV), ranging from 200 mV to 800 mV.
- The y-axis of the third plot is labeled $V_{C}, V_{D}$ (mV), ranging from 885 mV to 910 mV.

3. **Overall Behavior and Trends:**
- In each plot, two curves are shown, one increasing and the other decreasing, indicating complementary changes in the voltages as $V_{in}$ varies.
- In the first plot, as $V_{in}$ increases from -20 mV to 20 mV, $V_{A}$ decreases while $V_{B}$ increases.
- In the second plot, $V_{X}$ decreases and $V_{Y}$ increases as $V_{in}$ increases.
- In the third plot, $V_{C}$ decreases and $V_{D}$ increases with increasing $V_{in}$.

4. **Key Features and Technical Details:**
- All plots exhibit a smooth transition with no abrupt changes, suggesting linear or near-linear behavior within the given range.
- The slopes of these curves are indicative of the differential gain at each stage of the circuit.
- The middle plot, representing $V_{X}$ and $V_{Y}$, is particularly important as it shows the output nodes with a more significant voltage swing compared to the other plots.

5. **Annotations and Specific Data Points:**
- No specific annotations or markers are present in the plots. However, the symmetry around $V_{in} = 0$ is notable, indicating balanced operation.
- The crossover points, where the increasing and decreasing curves meet, occur at $V_{in} = 0$ for each plot, highlighting the point of symmetry.
image_name:V_C, V_D
description:The graph labeled "V_C, V_D" is a voltage versus input voltage plot, showing the behavior of the voltages at the drains of PMOS current sources (V_C and V_D) as a function of input voltage (V_in). The x-axis represents the input voltage (V_in) in millivolts (mV), ranging from -20 mV to 20 mV. The y-axis represents the voltages V_C and V_D, also in millivolts (mV), ranging from 885 mV to 910 mV.

Overall Behavior and Trends:
- **Symmetrical Behavior:** The graph shows symmetrical behavior around V_in = 0 mV.
- **Crossing Point:** Both V_C and V_D cross at approximately V_in = 0 mV, with V_C decreasing and V_D increasing as V_in increases from negative to positive values.
- **Nonlinear Characteristics:** The curves are nonlinear, with a noticeable curvature indicating a change in slope as V_in moves away from zero.

Key Features and Technical Details:
- **Initial Decrease/Increase:** As V_in moves from -20 mV towards 0 mV, V_C decreases from about 910 mV to around 895 mV, while V_D increases from about 885 mV to around 900 mV.
- **Post-Crossing Behavior:** Beyond the crossing point at V_in = 0 mV, V_C continues to decrease, reaching around 885 mV at V_in = 20 mV, while V_D increases to about 910 mV.

Annotations and Specific Data Points:
- **Crossing Point:** The crossing of V_C and V_D at V_in = 0 mV is a significant feature, indicating a balanced point where the behavior of the PMOS current sources is symmetrical with respect to the input voltage.
- **Endpoints:** The endpoints show the maximum deviation from the crossing point, highlighting the range of voltage swing for both V_C and V_D as the input voltage varies.

This graph illustrates the voltage behavior at the drains of PMOS current sources in response to varying input voltages, showcasing the symmetry and nonlinear characteristics of the system.

Figure 11.22 Behavior of the voltages at the drains of input transistors $\left(V_{A}, V_{B}\right)$, the output nodes $\left(V_{X}, V_{Y}\right)$, and the drains of PMOS current sources $\left(V_{C}, V_{D}\right)$.

#### Example 11.6

The slope of the characteristics in Fig. 11.22 predicts a differential gain of 3 from the input to nodes $A$ and $B$. Explain the reason for such a high gain at the cascode nodes.

#### Solution

Recall from Chapter 3 that the impedance seen at the source of a cascode device is roughly equal to the impedance seen at its drain divided by its $g_{m} r_{O}$. Due to the low $g_{m} r_{O}$, the impedance seen at $A$ and $B$ is quite a lot higher than $1 / g_{m 3,4}$, leading to a large gain.

Let us raise the gain by increasing $(W / L)_{3,4}$ to $600 \mu \mathrm{~m} / 80 \mathrm{~nm}$. Plotted in Fig. 11.23, the characteristics exhibit a gain of about 54 but still a limited output swing.
Bias Circuit The op amp of Fig. 11.21 relies on the proper choice of $I_{S S}, V_{b 1}, V_{b 2}$, and $V_{b 3}$. We must therefore design a circuit to generate these bias quantities. We recognize that $I_{S S}$ and $V_{b 3}$ must be established by current mirror action (why?) and $V_{b 2}$ by low-voltage cascode biasing. The bias voltage $V_{b 1}$ requires a different approach.

We begin with $I_{S S}=1.9 \mathrm{~mA}$, choosing a channel length of 40 nm and, scaling from Fig. 11.20, a width of $600 \mu \mathrm{~m}$ for $V_{D S}=100 \mathrm{mV}$. Utilizing a reference budget current of $25 \mu \mathrm{~A}$, we arrive at the arrangement shown in Fig. 11.24(a), where $W_{12}$ is scaled down from $W_{11}$ by a factor of $1.9 \mathrm{~mA} / 25 \mu \mathrm{~A}$. Since $M_{11}$ operates with a $V_{D S}$ of 100 mV , we insert $R_{1}$ in series with the drain of $M_{12}$ and select its value such that $V_{D S 12}=V_{G S 12}-V_{R 1}=100 \mathrm{mV}$.

The above bias design is still sensitive to the CM level sensed by $M_{1}$ and $M_{2}$ because $V_{D S 11}=$ $V_{C M, \text { in }}-V_{G S 1,2}$, whereas $V_{D S 12}=V_{G S 1,2}-V_{R 1}$. In other words, we must ensure that the drain voltage of $M_{12}$ tracks $V_{C M, i n}$. This can be accomplished as shown in Fig. 11.24(b), where $R_{1}$ is replaced by a differential pair driven by $V_{i n 1}$ and $V_{i n 2}$. With proper scaling of the widths, we now have $V_{G S 13,14}=V_{G S 1,2}$, and hence $V_{D S 12}=V_{D S 11}$.

Next, we deal with the generation of $V_{b 1}$ in Fig. 11.21. This voltage must be equal to $V_{G S 3,4}+$ $V_{D S 1,2}+V_{P}$, where $V_{D S 1,2}=100 \mathrm{mV}$. Since $V_{b 1}$ is higher than $V_{P}$ by $V_{G S 3,4}+V_{D S 1,2}$, we surmise that a diode-connected device in series with a drain-source voltage added to $V_{P}$ can produce $V_{b 1}$. Illustrated in Fig. 11.25, the idea is to match $V_{G S 15}$ to $V_{G S 3,4}$ and $V_{D S 16}$ to $V_{D S 1,2}$. The bias current $I_{b}$ must be much less than $I_{S S}$ so as to negligibly affect the power budget. We select $I_{b}=15 \mu \mathrm{~A}$, and hence $(W / L)_{15,16}=10 \mu \mathrm{~m} / 80 \mathrm{~nm} .{ }^{9}$ It is important to observe how $V_{b 1}$ tracks $V_{C M, \text { in }}:$ if $V_{C M, \text { in }}$ goes up, so do $V_{P}$ and, consequently, $V_{b 1}$, thus keeping $V_{D S 1,2}$ constant. That is, $M_{15}$ and $M_{16}$ operate as level shifters. If $V_{b 1}$ were constant, a rise in $V_{C M, i n}$ would inevitably reduce $V_{D S 1,2}$ and the gain.

In order to generate $V_{b 3}$ and $V_{b 2}$, we construct a low-voltage cascode bias network as shown in Fig. 11.26. Here, transistors $M_{17}$ and $M_{18}$ are scaled down from $M_{7,8}$ and $M_{5,6}$, respectively, ensuring that $V_{D S 17}=V_{D S 7,8}$. To create $V_{b 2}=V_{D D}-\left|V_{D S 7,8}\right|-\left|V_{G S 5,6}\right|$, we again employ a diode-connected device, $M_{20}$, in series with a $V_{D S}$ (produced by $M_{19}$ ).

We should emphasize that the very narrow voltage margins dictated by the low supply make this design sensitive to mismatches between the bias branches and the core of the circuit. For example, a mismatch between $V_{G S 18}$ and $V_{G S 5,6}$ can leave less $\left|V_{D S}\right|$ for $M_{7,8}$, pushing these two current sources below the knee point. Also, note that we still have a few ideal current sources, which would be copied from a bandgap reference (Chapter 12).

Common-Mode Feedback With various mismatches present in the above op amp design, the PMOS currents in Fig. 11.21 are not exactly equal to $I_{S S} / 2$, forcing the output CM level toward $V_{D D}$ or ground

image_name:Figure 11.23
description:Figure 11.23 consists of three separate graphs, each depicting the behavior of voltages in a circuit as a function of input voltage \( V_{in} \) ranging from -20 mV to 20 mV.

1. **Top Graph:**
- **Type:** Voltage vs. Input Voltage Graph
- **Axes Labels:**
- X-axis: \( V_{in} \) in millivolts (mV)
- Y-axis: \( V_{A}, V_{B} \) in millivolts (mV)
- **Behavior:**
- The graph shows two curves representing \( V_{A} \) and \( V_{B} \).
- \( V_{A} \) starts at 150 mV when \( V_{in} = -20 \) mV and increases linearly to 210 mV as \( V_{in} \) reaches 20 mV.
- \( V_{B} \) starts at 210 mV when \( V_{in} = -20 \) mV and decreases linearly to 150 mV as \( V_{in} \) reaches 20 mV.
- The intersection occurs at \( V_{in} = 0 \) mV, where both \( V_{A} \) and \( V_{B} \) are approximately 200 mV.

2. **Middle Graph:**
- **Type:** Voltage vs. Input Voltage Graph
- **Axes Labels:**
- X-axis: \( V_{in} \) in millivolts (mV)
- Y-axis: \( V_{X}, V_{Y} \) in millivolts (mV)
- **Behavior:**
- The graph shows two curves representing \( V_{X} \) and \( V_{Y} \).
- \( V_{X} \) starts at 700 mV for \( V_{in} = -20 \) mV and decreases to 100 mV as \( V_{in} \) reaches 20 mV.
- \( V_{Y} \) starts at 100 mV for \( V_{in} = -20 \) mV and increases to 700 mV as \( V_{in} \) reaches 20 mV.
- The intersection occurs at \( V_{in} = 0 \) mV, where both \( V_{X} \) and \( V_{Y} \) are approximately 500 mV.

3. **Bottom Graph:**
- **Type:** Voltage vs. Input Voltage Graph
- **Axes Labels:**
- X-axis: \( V_{in} \) in millivolts (mV)
- Y-axis: \( V_{C}, V_{D} \) in millivolts (mV)
- **Behavior:**
- The graph shows two curves representing \( V_{C} \) and \( V_{D} \).
- \( V_{C} \) starts at 910 mV for \( V_{in} = -20 \) mV and decreases to 885 mV as \( V_{in} \) reaches 20 mV.
- \( V_{D} \) starts at 885 mV for \( V_{in} = -20 \) mV and increases to 910 mV as \( V_{in} \) reaches 20 mV.
- The intersection occurs at \( V_{in} = 0 \) mV, where both \( V_{C} \) and \( V_{D} \) are approximately 900 mV.

**Overall Trends:**
- Each pair of curves in the graphs exhibits a symmetrical behavior around \( V_{in} = 0 \) mV, with one curve increasing and the other decreasing linearly as \( V_{in} \) changes from negative to positive values.
- The three graphs demonstrate how different nodes in the circuit respond to changes in input voltage, with clear linear relationships and intersections at \( V_{in} = 0 \) mV.

Figure 11.23 Behavior of the voltages at the drains of input transistors $\left(V_{A}, V_{B}\right)$, the output nodes $\left(V_{X}, V_{Y}\right)$, and the drains of PMOS current sources $\left(V_{C}, V_{D}\right)$.
image_name:(a)
description:
[
name: R1, type: Resistor, value: 8kΩ, ports: {N1: VDD, N2: X}
name: M12, type: NMOS, ports: {S: GND, D: X, G: GND}
name: M1, type: NMOS, ports: {S: X, D: LOAD, G: Vb}
name: M2, type: NMOS, ports: {S: GND, D: Y, G: Vin}
name: M11, type: NMOS, ports: {S: GND, D: Y, G: GND}
name: VoltageSource, type: VoltageSource, value: 25μA, ports: {Np: VDD, Nn: X}
]
extrainfo:This circuit is a differential amplifier with NMOS transistors M1 and M2 forming the input stage. The tail current source is implemented with a voltage source and resistor R1. The NMOS transistors M11 and M12 are used for current sinking.
image_name:(b)
description:
[
name: R1, type: Resistor, value: 8kΩ, ports: {N1: VDD, N2: X}
name: M1, type: NMOS, ports: {S: X, D: LOAD1, G: Vip2}
name: M2, type: NMOS, ports: {S: LOAD1, D: P, G: Vin2}
name: M11, type: NMOS, ports: {S: P, D: GND, G: X}
name: M12, type: NMOS, ports: {S: X, D: GND, G: X}
name: M13, type: NMOS, ports: {S: X, D: d2s13s14, G: Vbp1}
name: M14, type: NMOS, ports: {S: d2s13s14, D: Vin2, G: Vin}
name: VDD, type: CurrentSource, value: 25μA, ports: {Np: VDD, Nn: X}
name: VDD, type: CurrentSource, value: 25μA, ports: {Np: VDD, Nn: X}
]
extrainfo:The circuit diagram (b) is a more accurate biasing for a tail current source. It includes several NMOS transistors and a resistor, with two current sources providing 25μA each. M13 and M14 form a cascode structure with gate bias voltages Vip2 and Vbp1. The circuit operates with a total current of 1.9 mA flowing through M11 to ground.

Figure 11.24 (a) Simple and (b) more accurate biasing for tail current source.
image_name:Figure 11.24 (b)
description:
[
name: M1, type: NMOS, ports: {S: P, D: d1s3, G: Vip}
name: M2, type: NMOS, ports: {S: P, D: d2s4, G: Vin}
name: M3, type: NMOS, ports: {S: d1s3, D: X, G: Vb1}
name: M4, type: NMOS, ports: {S: d2s4, D: Y, G: Vb1}
name: M15, type: NMOS, ports: {S: sisdb, D: Vb1, G: Vb1}
name: M16, type: NMOS, ports: {S: sisdb, D: P, G: Vb1}
name: Ib, type: CurrentSource, value: Ib, ports: {Np: VDD, Nn: Vb1}
name: Iss, type: CurrentSource, value: Iss, ports: {Np: P, Nn: GND}
]
extrainfo:The circuit diagram is a more accurate biasing for a tail current source. It includes NMOS transistors M1 to M4 and M15, M16, forming a cascode structure. The circuit uses two current sources, Ib and Iss, providing biasing currents. M13 and M14 form a cascode structure with gate bias voltages Vip2 and Vbp1. The circuit operates with a total current of 1.9 mA flowing through M11 to ground.

Figure 11.25 Generation of cascode gate bias voltage.
image_name:Figure 11.25 Generation of cascode gate bias voltage
description:
[
name: M19, type: PMOS, ports: {S: VDD, D: d19s20, G: Vb3}
name: M20, type: PMOS, ports: {S: VDD, D: d19s20, G: Vb2}
name: M17, type: PMOS, ports: {S: VDD, D: d17s18, G: Vb3}
name: M18, type: PMOS, ports: {S: VDD, D: d17s18, G: Vb2}
name: M7, type: PMOS, ports: {S: VDD, D: ssd7, G: Vb3}
name: M8, type: PMOS, ports: {S: VDD, D: s8d8, G: Vb2}
name: M5, type: PMOS, ports: {S: VDD, D: ssd7, G: Vb3}
name: M6, type: PMOS, ports: {S: VDD, D: s8d8, G: Vb2}
name: 15 μA, type: CurrentSource, value: 15 μA, ports: {Np: d19s20, Nn: GND}
name: 15 μA, type: CurrentSource, value: 15 μA, ports: {Np: d17s18, Nn: GND}
]
extrainfo:The circuit diagram shows a cascode gate bias voltage generation circuit using PMOS transistors. It includes a set of PMOS transistors M19, M20, M17, M18, M7, M8, M5, and M6, which are used to generate bias voltages Vb2 and Vb3. These transistors are connected to two 15 μA current sources that provide the necessary biasing currents. The n-wells of the PMOS transistors are tied to their sources, and the transistors have a width-to-length ratio of 5 μm/80 nm. The circuit is designed to generate stable bias voltages for other parts of the system.

Figure 11.26 Generation of bias for PMOS cascode current sources.
and hence requiring CMFB. We must sense the output CM level, $V_{C M}$, and feed the result back to the NMOS or PMOS current sources.

Recall from Chapter 9 that the CM level can be sensed by resistors, triode transistors, or source followers. The high output impedance of the op amp dictates very large resistors, ${ }^{10}$ and the tight voltage margins demand precise CM control and preclude triode devices. The only solution, source followers, however, cannot measure the CM level across a wide output swing. As shown in Fig. 11.27(a), if $V_{X}$ (or $V_{Y}$ ) falls (in response to differential signals), $I_{1}$ (or $I_{2}$ ) eventually collapses, disabling the source follower. But, is it possible to complement the NMOS followers by PMOS counterparts? Consider the arrangement depicted in Fig. 11.27(b), where PMOS followers $M_{23}$ and $M_{24}$ also sense the output CM

image_name:(a)
description:
[
name: M3, type: NMOS, ports: {S: GND, D: X, G: GND}
name: M4, type: NMOS, ports: {S: GND, D: X, G: GND}
name: M5, type: NMOS, ports: {S: Y, D: VDD, G: X}
name: M6, type: NMOS, ports: {S: Y, D: VDD, G: X}
name: M21, type: NMOS, ports: {S: GND, D: Y, G: GND}
name: M22, type: NMOS, ports: {S: GND, D: Y, G: GND}
name: I1, type: CurrentSource, ports: {Np: GND, Nn: GND}
name: I2, type: CurrentSource, ports: {Np: GND, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: V1, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: V1, N2: GND}
]
extrainfo:The circuit in Fig. 11.27(a) is designed for CM level reconstruction using NMOS source followers. It uses NMOS transistors M3, M4, M5, M6, M21, and M22, along with current sources I1 and I2, and resistors R1 and R2. The NMOS transistors are configured to sense differential signals and reconstruct the common-mode level.
image_name:(b)
description:
[
name: M3, type: NMOS, ports: {S: GND, D: X, G: Vin}
name: M4, type: NMOS, ports: {S: GND, D: X, G: Vin}
name: M5, type: NMOS, ports: {S: VDD, D: Y, G: X}
name: M6, type: NMOS, ports: {S: VDD, D: Y, G: X}
name: M21, type: NMOS, ports: {S: GND, D: V1, G: Y}
name: M22, type: NMOS, ports: {S: VDD, D: V1, G: Y}
name: M23, type: NMOS, ports: {S: GND, D: V2, G: Y}
name: M24, type: NMOS, ports: {S: VDD, D: V2, G: Y}
name: I1, type: CurrentSource, ports: {Np: GND, Nn: M21}
name: I2, type: CurrentSource, ports: {Np: GND, Nn: M22}
name: I3, type: CurrentSource, ports: {Np: GND, Nn: M23}
name: I4, type: CurrentSource, ports: {Np: GND, Nn: M24}
name: R1, type: Resistor, value: R1, ports: {N1: V1, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: V1, N2: VDD}
name: R3, type: Resistor, value: R3, ports: {N1: V2, N2: GND}
name: R4, type: Resistor, value: R4, ports: {N1: V2, N2: VDD}
]
extrainfo:The circuit diagram (b) is a CM level reconstruction circuit using complementary source followers. It uses NMOS and PMOS transistors to sense the output CM level and drive the resistors R3 and R4. The equations governing the voltages V1 and V2 are given by V1 = VCM - VGS21,22 and V2 = VCM + |VGS23,24|.
image_name:(c)
description:
[
name: M3, type: NMOS, ports: {S: X, D: GND, G: X}
name: M4, type: NMOS, ports: {S: X, D: GND, G: X}
name: M5, type: NMOS, ports: {S: VDD, D: Y, G: Y}
name: M6, type: NMOS, ports: {S: VDD, D: Y, G: Y}
name: M21, type: NMOS, ports: {S: GND, D: X, G: X}
name: M22, type: NMOS, ports: {S: Y, D: V1, G: V1}
name: M23, type: NMOS, ports: {S: GND, D: Vtot, G: Vtot}
name: M24, type: NMOS, ports: {S: VDD, D: V2, G: V2}
name: I1, type: CurrentSource, value: I1, ports: {Np: GND, Nn: X}
name: I2, type: CurrentSource, value: I2, ports: {Np: GND, Nn: V1}
name: I3, type: CurrentSource, value: I3, ports: {Np: GND, Nn: Vtot}
name: I4, type: CurrentSource, value: I4, ports: {Np: VDD, Nn: V2}
name: R1, type: Resistor, value: R1, ports: {N1: V1, N2: Vtot}
name: R2, type: Resistor, value: R2, ports: {N1: V1, N2: Vtot}
name: R3, type: Resistor, value: R3, ports: {N1: Vtot, N2: V2}
name: R4, type: Resistor, value: R4, ports: {N1: Vtot, N2: V2}
]
extrainfo:The circuit diagram (c) illustrates a combining network using NMOS transistors and resistors to achieve CM level reconstruction. This network combines differential signals, maintaining balance across the resistors, and ensures that the output CM level is reconstructed effectively. The arrangement of current sources and NMOS transistors allows for the manipulation of the CM level across a wide output swing.

Figure 11.27 (a) CM level reconstruction using NMOS source followers, (b) CM level reconstruction using complementary source followers, and (c) combining network.
level and drive $R_{3}$ and $R_{4}$, respectively. We recognize that $V_{1}$ is lower than $V_{C M}$ by $V_{G S 21,22}$ and $V_{2}$ is higher than $V_{C M}$ by $\left|V_{G S 23,24}\right|$ :

$$
\begin{align*}
& V_{1}=V_{C M}-V_{G S 21,22}  \tag{11.10}\\
& V_{2}=V_{C M}+\left|V_{G S 23,24}\right| \tag{11.11}
\end{align*}
$$

We therefore surmise that a linear combination of $V_{1}$ and $V_{2}$ can remove the $V_{G S}$ terms, yielding a value in proportion to $V_{C M}$. That is, if

$$
\begin{equation*}
\alpha V_{1}+\beta V_{2}=(\alpha+\beta) V_{C M}-\alpha V_{G S 21,22}+\beta\left|V_{G S 23,24}\right| \tag{11.12}
\end{equation*}
$$

then we must choose $\alpha V_{G S 21,22}=\beta\left|V_{G S 23,24}\right|$, obtaining $\alpha V_{1}+\beta V_{2}=(\alpha+\beta) V_{C M}$. We also choose $\alpha+\beta=1$ so that the reconstructed value is equal to the op amp output CM level.

The weighting factors, $\alpha$ and $\beta$, can readily be implemented by $R_{1}-R_{4}$ in Fig. 11.27(b). In fact, if $V_{1}$ and $V_{2}$ are shorted, the weighted sum of $V_{1}$ and $V_{2}$ is produced. With the aid of the equivalent circuit in Fig. 11.27(c), the reader can show that

$$
\begin{equation*}
V_{\text {tot }}=V_{C M}+\frac{R_{N}\left|V_{G S 23,24}\right|-R_{P} V_{G S 21,22}}{R_{N}+R_{P}} \tag{11.13}
\end{equation*}
$$

where $R_{N}=R_{1}=R_{2}$ and $R_{P}=R_{3}=R_{4}$. We therefore choose $R_{N} / R_{P}=V_{G S 21,22} /\left|V_{G S 23,24}\right|$.
In order to evaluate the feasibility of the above idea, we first run a dc sweep in simulations and examine the behavior of $V_{\text {tot }}$. We select a bias current of $10 \mu \mathrm{~A}$ (slightly exceeding the power budget), $W / L=10 \mu \mathrm{~m} / 40 \mathrm{~nm}$ for all of the source followers, and $R_{N}=R_{P}=20 \mathrm{k} \Omega$. The $10-\mu \mathrm{A}$ bias current sources are also implemented as transistors (with $W / L=10 \mu \mathrm{~m} / 40 \mathrm{~nm}$ ) to ensure a realistic behavior as $V_{X}$ and $V_{Y}$ approach $V_{D D}$ or ground. ${ }^{11}$ Figure 11.28 plots the outputs, their actual common-mode level, defined as $\left(V_{X}+V_{Y}\right) / 2$, and the reconstructed counterpart, $V_{t o t}$. We note that $V_{t o t}$ closely follows the CM level of $V_{X}$ and $V_{Y}$.

[^86]image_name:Figure 11.28
description:The graph in Figure 11.28 is a voltage versus input differential voltage plot, specifically displaying the behavior of a cascode operational amplifier. The x-axis represents the input differential voltage, $V_{in}$, in millivolts (mV), ranging from -20 mV to 20 mV. The y-axis represents the voltage in millivolts (mV), ranging from 0 mV to 800 mV.

Three curves are depicted in the graph:

1. **$V_X$ and $V_Y$ Curves:** These are shown with lighter lines, representing the output voltages $V_X$ and $V_Y$. As $V_{in}$ increases from -20 mV to 20 mV, $V_X$ decreases from approximately 700 mV to 300 mV, while $V_Y$ increases from approximately 300 mV to 700 mV. This indicates an inverse relationship between $V_X$ and $V_Y$ as $V_{in}$ changes.

2. **Actual CM Level Curve:** Labeled as $(V_X + V_Y)/2$, this curve represents the actual common-mode level of the outputs. It is shown with a dashed line, starting at around 500 mV at $V_{in} = 0$ mV and remaining relatively constant across the range of $V_{in}$.

3. **Reconstructed CM Level Curve ($V_{tot}$):** This curve is shown with a solid line, closely following the actual CM level. It starts at around 500 mV when $V_{in} = 0$ mV and maintains a similar level across the input range, indicating that $V_{tot}$ effectively reconstructs the common-mode level.

**Overall Behavior and Trends:**
- The graph illustrates the differential behavior of the cascode op amp, with $V_X$ and $V_Y$ diverging as $V_{in}$ moves from negative to positive values.
- The common-mode levels, both actual and reconstructed, remain stable, demonstrating the effectiveness of the common-mode feedback mechanism in maintaining a constant CM level despite changes in $V_{in}$.

Figure 11.28 Actual CM level, $\left(V_{X}+V_{Y}\right) / 2$, and reconstructed CM level, $V_{t o t}$, of cascode op amp as a function of input differential voltage.

### 11.5.3 CM Feedback Around a Telescopic Op Amp
In the next test, let us close the CM feedback loop: we compare $V_{t o t}$ to a reference, amplify the error, and return the result to control $I_{S S}$. To this end, we design the error amplifier as a five-transistor OTA with $W / L=5 \mu \mathrm{~m} / 80 \mathrm{~nm}$ for all transistors, a tail current of $20 \mu \mathrm{~A}$, and a voltage gain of 10 . The output of this amplifier controls a fraction of the main tail current, $I_{1}$ (Fig. 11.29). For example, if we expect $20 \%$ mismatch between the PMOS current sources in the op amp and the tail current source, we choose $I_{1} \approx 0.2 I_{S S}$. Figure 11.29 depicts the result, where the OTA's input and output connections are chosen so as to establish negative feedback around the loop.
image_name:Figure 11.29
description:
[
name: Vb1, type: VoltageSource, ports: {Np: Vb1, Nn: GND}
name: 20 kΩ 1, type: Resistor, value: 20 kΩ, ports: {N1: Vb1, N2: Node1}
name: 20 kΩ 2, type: Resistor, value: 20 kΩ, ports: {N1: Node1, N2: Vtot}
name: 20 kΩ 3, type: Resistor, value: 20 kΩ, ports: {N1: Node2, N2: GND}
name: 20 kΩ 4, type: Resistor, value: 20 kΩ, ports: {N1: Node2, N2: Vtot}
name: 20 μA, type: CurrentSource, value: 20 μA, ports: {Np: Vref, Nn: GND}
name: M1, type: NMOS, ports: {S: Node3, D: C, G: Vref}
name: M2, type: NMOS, ports: {S: Node4, D: C, G: Vref}
name: M3, type: PMOS, ports: {S: VDD, D: Node3, G: H}
name: M4, type: PMOS, ports: {S: VDD, D: Node4, G: H}
name: MT, type: NMOS, ports: {S: GND, D: H, G: I1}
name: MG, type: NMOS, ports: {S: G, D: Node2, G: Vref}
name: Iss - I1, type: CurrentSource, ports: {Np: H, Nn: GND}
]
extrainfo:The circuit depicts a CMFB loop around a telescopic op-amp. It uses PMOS transistors in the input stage to sense the common-mode level and maintain sufficient V_DS for the tail current source. The op-amp core is designed to establish negative feedback around the loop.

Figure 11.29 CMFB loop around telescopic op amp.

#### Example 11.7

Explain why the OTA in Fig. 11.29 employs PMOS (rather than NMOS) input devices.

#### Solution

The choice is dictated by two considerations. First, these transistors must sense the CM level while leaving sufficient $V_{D S}$ for their tail current source. With $V_{t o t} \approx V_{D D} / 2$ in this case, there is no particular preference for NMOS or PMOS devices. Second, the output of the OTA should have a nominal dc value compatible with that required by $M_{T}$.

Since $V_{H}=V_{G}$ (in the absence of mismatches), and since $V_{G}$ is equal to the gate-source voltage of a diode-connected NMOS transistor, we expect that $M_{T}$ nominally copies the bias current of $M_{G}$ (with a multiplication factor).

Figure 11.30 shows the closed-loop dc sweep results with $V_{\text {ref }}=0.5 \mathrm{~V}$.
image_name:Figure 11.30
description:The graph in Figure 11.30 is a plot depicting the closed-loop behavior of two variables related to a cascode operational amplifier as a function of input differential voltage ($V_{in}$). The graph is plotted on a Cartesian plane with the horizontal axis representing the input differential voltage ($V_{in}$) in millivolts, ranging from -20 mV to 20 mV, and the vertical axis representing voltage levels in millivolts, ranging from 500 mV to 508 mV.

There are two curves plotted on this graph:

1. **Reconstructed Common-Mode Level ($V_{tot}$):**
- This curve is shown in black and exhibits a clear, symmetric bell-shaped profile, peaking at approximately 507 mV when $V_{in}$ is around 0 mV. The curve starts at about 503 mV at $V_{in} = -20$ mV, increases to a peak value, and then symmetrically decreases back to about 503 mV at $V_{in} = 20$ mV. This indicates that the reconstructed common-mode level is sensitive to the input differential voltage, showing a peak at zero input.

2. **Actual Common-Mode Level (($V_{X} + V_{Y})/2$):**
- This curve is depicted in gray and demonstrates a much flatter profile compared to $V_{tot}$. It starts at slightly above 501 mV at $V_{in} = -20$ mV, rises gently to just below 503 mV near $V_{in} = 0$ mV, and then descends slightly back towards 501 mV at $V_{in} = 20$ mV. This suggests that the actual common-mode level remains relatively stable despite changes in the input differential voltage.

**Overall Behavior and Trends:**
- The graph illustrates how feedback in the cascode op amp design helps stabilize the actual common-mode level, while the reconstructed common-mode level varies more significantly with changes in input voltage. The feedback mechanism appears to minimize variations in the actual common-mode level, maintaining it within a narrow range.

**Key Features:**
- The peak of $V_{tot}$ at $V_{in} = 0$ mV highlights the maximum deviation due to the input differential voltage.
- The relatively constant behavior of (($V_{X} + V_{Y})/2$) across the input range suggests effective common-mode feedback control.

Figure 11.30 Closed-loop behavior of actual CM level, $\left(V_{X}+V_{Y}\right) / 2$, and reconstructed CM level, $V_{\text {tot }}$, of cascode op amp as a function of input differential voltage.

By virtue of feedback, the CM variation is greatly reduced as $V_{X}$ and $V_{Y}$ reach high or low values. Next, we create a $10 \%$ mismatch between the PMOS current sources ( $M_{7}$ and $M_{8}$ in Fig. 11.21) and $I_{S S} / 2=950 \mu \mathrm{~A}$ and repeat the dc sweep. Figure 11.31 depicts the variations, indicating that CMFB suppresses the mismatch by adjusting $I_{1}$.
image_name:Figure 11.31
description:The graph in Figure 11.31 is a plot depicting the behavior of a cascode op amp's common-mode (CM) levels as a function of the input differential voltage, \( V_{in} \). The x-axis represents the input differential voltage \( V_{in} \) in millivolts (mV), ranging from -20 mV to 20 mV. The y-axis shows the voltage level in millivolts (mV), ranging from 475 mV to 495 mV.

There are two curves on the graph:

1. **\((V_X + V_Y)/2\) Curve (Gray Line):** This curve represents the actual common-mode level, \((V_X + V_Y)/2\). It displays a broad, gentle peak around the center of the \( V_{in} \) range. The curve starts at approximately 490 mV at \( V_{in} = -20 \) mV, rises slightly to around 492 mV near \( V_{in} = 0 \) mV, and then descends back to around 490 mV at \( V_{in} = 20 \) mV.

2. **\(V_{tot}\) Curve (Black Line):** This curve represents the reconstructed common-mode level, \( V_{tot} \). It exhibits a more pronounced peak compared to the gray line, with a maximum value slightly above 485 mV. The curve starts at 475 mV at \( V_{in} = -20 \) mV, peaks between \( V_{in} = -10 \) mV and \( V_{in} = 10 \) mV, and then decreases to around 475 mV at \( V_{in} = 20 \) mV.

**Overall Behavior and Trends:**
- The gray line shows a relatively stable CM level with minor variations, indicating effective suppression of mismatch effects.
- The black line demonstrates a more dynamic response, reflecting the CMFB's action in adjusting \( I_1 \) to compensate for mismatch.

**Key Features:**
- The peak of the \( V_{tot} \) curve suggests the point of maximum feedback adjustment.
- Both curves illustrate the feedback system's ability to manage CM levels despite input variations, with the \( V_{tot} \) curve showing more significant adjustments.

Figure 11.31 Closed-loop behavior of actual CM level, $\left(V_{X}+V_{Y}\right) / 2$, and reconstructed CM level, $V_{\text {tot }}$, of cascode op amp in the presence of mismatch between tail and PMOS current sources.

CMFB Stability We must investigate the stability of the CM loop. This is accomplished by placing the overall op amp in its intended feedback system, applying differential pulses at the input, and examining
the differential and common-mode behavior of the output. Figure 11.32(a) shows a feedback topology for a nominal closed-loop gain of 2, and Fig. 11.32(b) depicts a more detailed diagram highlighting the CM feedback loop. ${ }^{12}$
image_name:(a)
description:
[
name: R1, type: Resistor, value: 50kΩ, ports: {N1: Vin, N2: X}
name: R2, type: Resistor, value: 100kΩ, ports: {N1: X, N2: Vout}
name: M1, type: NMOS, ports: {S: g1, D: dis3, G: Vb2}
name: M2, type: NMOS, ports: {S: g2, D: d2s4, G: Vb1}
name: M3, type: NMOS, ports: {S: dis3, D: X, G: Vb3}
name: M4, type: NMOS, ports: {S: d2s4, D: X, G: Y}
name: M5, type: PMOS, ports: {S: VDD, D: ssd1, G: Vbx}
name: M6, type: PMOS, ports: {S: VDD, D: Y, G: sbd8}
name: M7, type: PMOS, ports: {S: VDD, D: ssd1, G: Vbx}
name: M8, type: PMOS, ports: {S: VDD, D: Y, G: sbd8}
name: MT, type: NMOS, ports: {S: GND, D: H, G: Vb1}
name: Mg, type: NMOS, ports: {S: GND, D: H, G: Vb1}
]
extrainfo:The circuit is a closed-loop amplifier with a CMFB loop. It includes NMOS and PMOS transistors forming a differential pair and current mirrors. The CMFB loop is used for common-mode stability, and compensation is required due to poles at various nodes. The circuit is designed to analyze transient response with a nominal closed-loop gain of 2.
image_name:(b)
description:
[
name: R1, type: Resistor, value: 50kΩ, ports: {N1: Vin, N2: X}
name: R2, type: Resistor, value: 100kΩ, ports: {N1: X, N2: GND}
name: M1, type: NMOS, ports: {S: g1, D: d1s3, G: Vb2}
name: M2, type: NMOS, ports: {S: g2, D: d2s4, G: Vb1}
name: M3, type: NMOS, ports: {S: d1s3, D: X, G: Vb3}
name: M4, type: NMOS, ports: {S: d2s4, D: P, G: X}
name: M5, type: PMOS, ports: {S: VDD, D: ssd1, G: Vb4}
name: M6, type: PMOS, ports: {S: sbd8, D: Y, G: X}
name: M7, type: PMOS, ports: {S: VDD, D: ssd1, G: Vb4}
name: M8, type: PMOS, ports: {S: sbd8, D: Y, G: X}
name: MT, type: NMOS, ports: {S: GND, D: H, G: Vb1}
name: Mg, type: NMOS, ports: {S: GND, D: H, G: Vb1}
name: OpAmp, type: OpAmp, ports: {InP: H, InN: Vref, OutP: Vtot, OutN: CM Extraction}
name: Vref, type: VoltageSource, ports: {Np: Vref, Nn: GND}
name: CM Extraction, type: Other, ports: {N1: CM Extraction, N2: Y}
]
extrainfo:The circuit is a common-mode feedback (CMFB) loop with compensation needed due to poles at various nodes. It includes NMOS and PMOS transistors, resistors for setting gains, and an op-amp for feedback control.

Figure 11.32 (a) Closed-loop amplifier for transient analysis, and (b) detailed view showing the CMFB loop.
Plotted in Fig. 11.33 are the output waveforms in response to an input step, revealing common-mode instability. As evident from Fig. 11.32(b), the CM loop contains a pole at the input of the error amplifier, one at node $H$, one at node $P$, one at the sources of the NMOS cascode devices, and one at the main outputs. The loop therefore demands compensation.
image_name:Figure 11.33
description:The graph in Figure 11.33 is a time-domain waveform depicting the transient response of an op-amp circuit, specifically illustrating common-mode instability. The x-axis represents time in nanoseconds (ns), ranging from 0 to 40 ns. The y-axis represents voltage in millivolts (mV), with values ranging from 300 mV to 700 mV. The graph features two waveforms, likely representing different nodes or outputs, depicted in different shades for distinction.

The overall behavior of the waveforms shows an initial response to a step input, followed by oscillations indicative of instability. Starting at around 500 mV, both waveforms initially exhibit a rapid increase and decrease, with one waveform peaking slightly above 600 mV and the other dipping below 400 mV. Subsequently, both waveforms enter a phase of damped oscillations, with decreasing amplitude until around 15 ns. After this period, the oscillations grow in amplitude, indicating a lack of stability in the system.

Key features include the initial peak and trough within the first 10 ns, followed by a series of oscillations. The waveforms show a clear increase in oscillation amplitude after 20 ns, suggesting a positive feedback or resonance effect that exacerbates the instability. The presence of multiple oscillation cycles and their increasing amplitude highlight the need for compensation in the common-mode feedback loop to stabilize the system. The graph does not feature any annotations or specific markers, but the oscillatory behavior is a critical point of analysis for identifying the instability issues in the circuit.

Figure 11.33 Transient response revealing CM loop instability.

#### Example 11.8

We wish to study the CM loop frequency response and obtain the phase margin. Should the differential feedback be present when the CM loop is broken? In other words, which of the two topologies in Fig. 11.34(a) should be used to determine the CM loop transmission?

[^87]image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vin, G: Vip}
name: M2, type: NMOS, ports: {S: Vin, D: GND, G: Vin}
name: MT, type: NMOS, ports: {S: GND, D: Vref, G: H}
name: R1, type: Resistor, value: R1, ports: {N1: GND, N2: Vip}
name: R2, type: Resistor, value: R2, ports: {N1: Vip, N2: Vin}
name: C1, type: Capacitor, value: C1, ports: {Np: VDD, Nn: Vin}
name: H, type: OpAmp, value: H, ports: {InP: Vin, InN: Vref, OutP: H, OutN: GND}
name: Vtot, type: VoltageSource, value: Vtot, ports: {Np: Vtot, Nn: GND}
name: Vref, type: VoltageSource, value: Vref, ports: {Np: Vref, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: d1, type: CurrentSource, value: d1, ports: {Np: VDD, Nn: Vip}
name: d2, type: CurrentSource, value: d2, ports: {Np: VDD, Nn: Vin}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: Vt, Nn: GND}
name: VF, type: VoltageSource, value: VF, ports: {Np: VF, Nn: GND}
]
extrainfo:The diagram represents a common-mode feedback (CMFB) system with NMOS transistors and operational amplifiers. The CM Extraction block processes the common-mode signal, and the system is powered by a VDD source. The op-amp labeled 'H' is used for differential feedback.
image_name:(b)
description:
[
name: MT, type: NMOS, ports: {S: GND, D: Vref, G: Vtot}
name: H, type: OpAmp, ports: {InP: Vtot, InN: GND, Out: Vref}
name: R1, type: Resistor, value: R1, ports: {N1: GND, N2: Vin}
name: R2, type: Resistor, value: R2, ports: {N1: Vin, N2: CM Extraction}
name: M1, type: NMOS, ports: {S: d1, D: d1s1, G: Vip}
name: M2, type: NMOS, ports: {S: d2, D: d2s1, G: Vin}
name: d1, type: CurrentSource, ports: {Np: VDD, Nn: d1}
name: d2, type: CurrentSource, ports: {Np: VDD, Nn: d2}
name: C1, type: Capacitor, value: C1, ports: {Np: VDD, Nn: CM Extraction}
name: Vt, type: VoltageSource, ports: {Np: Vt, Nn: GND}
name: VF, type: VoltageSource, ports: {Np: VF, Nn: GND}
]
extrainfo:The circuit in (b) is a common-mode feedback configuration with differential inputs. It includes NMOS transistors M1 and M2, current sources d1 and d2, and a CM extraction block. The op-amp H stabilizes the common-mode voltage.
image_name:(c)
description:
[
name: MT, type: NMOS, ports: {S: GND, D: Vref, G: Vtot}
name: H, type: OpAmp, value: H, ports: {InP: Vref, InN: Vtot, OutP: Vtot, OutN: Vref}
name: R1, type: Resistor, value: R1, ports: {N1: GND, N2: Vtot}
name: R2, type: Resistor, value: R2, ports: {N1: Vtot, N2: VDD}
name: M1, type: NMOS, ports: {S: GND, D: P, G: Vtot}
name: M2, type: NMOS, ports: {S: GND, D: P, G: Vtot}
name: C1, type: Capacitor, value: C1, ports: {Np: P, Nn: VDD}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: Vref, Nn: GND}
name: VF, type: VoltageSource, value: VF, ports: {Np: Vref, Nn: GND}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: d1, type: CurrentSource, value: d1, ports: {Np: VDD, Nn: P}
name: d2, type: CurrentSource, value: d2, ports: {Np: VDD, Nn: P}
]
extrainfo:The circuit diagram (c) is designed for common-mode feedback (CMFB) analysis with differential feedback present. It includes NMOS transistors M1 and M2, a capacitor C1, and a common-mode extraction block. The CMFB loop is analyzed with the presence of differential feedback to ensure stability. The circuit also includes voltage sources Vt and VF for reference and feedback purposes.

Figure 11.34

#### Solution

Common-mode feedback must ultimately behave well with differential feedback present. This is because the actual environment in which CMFB must be stable incorporates differential feedback. As an example, consider the simple op amp shown in Fig. 11.34(b). For CM analysis, the two sides can be merged into one, yielding the two possible scenarios depicted in Fig. 11.34(c) if the differential feedback is absent or present. Obtained as $-V_{F} / V_{t}$, the CM loop transmissions derived for these two cases are not necessarily the same. For example, if the capacitance at the drain, $C_{1}$, is considered, the pole associated with this node assumes different values in the two topologies. Thus, we must maintain differential feedback while studying CM stability.

Let us break the CM loop in Fig. 11.32(b) at node $H$ as shown in Fig. 11.35. Here, the error amplifier drives a dummy device, $M_{d}$, identical to $M_{T}$ so as to see the loading effect of the latter. Plotted in
image_name:Figure 11.35
description:
[
name: M1, type: NMOS, ports: {S: P, D: X, G: Vin}
name: M2, type: NMOS, ports: {S: P, D: Y, G: Vin}
name: M3, type: PMOS, ports: {S: X, D: P, G: VDD}
name: M4, type: PMOS, ports: {S: Y, D: P, G: VDD}
name: M5, type: PMOS, ports: {S: VDD, D: X, G: X}
name: M6, type: PMOS, ports: {S: VDD, D: Y, G: Y}
name: M7, type: PMOS, ports: {S: VDD, D: X, G: X}
name: M8, type: PMOS, ports: {S: VDD, D: Y, G: Y}
name: M9, type: NMOS, ports: {S: GND, D: P, G: Vin}
name: MT, type: NMOS, ports: {S: GND, D: H, G: P}
name: Md, type: NMOS, ports: {S: GND, D: H, G: VDD}
name: OpAmp, type: OpAmp, ports: {InP: Vref, InN: Vtot, OutP: H, OutN: GND}
name: Vt, type: VoltageSource, ports: {Np: Vt, Nn: GND}
name: VF, type: VoltageSource, ports: {Np: VF, Nn: GND}
name: VDD, type: VoltageSource, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a common-mode feedback loop with an error amplifier and dummy device Md to replicate the loading effect of MT. It includes multiple PMOS and NMOS transistors for differential feedback and stability. The error amplifier receives inputs from Vtot and Vref, with the output driving node H.

Figure 11.35 Measurement of CMFB loop transmission.

Fig. 11.36(a) are the magnitude and phase of $-V_{F} / V_{t}$ as a function of frequency, revealing a phase of $-190^{\circ}$ at the unity-gain frequency. We seek a convenient node for compensation. Unfortunately, the error amplifier in Fig. 11.29 does not provide signal inversion from $V_{t o t}$ to $H$ and hence cannot employ Miller compensation.
image_name:Figure 11.36(a)
description:Figure 11.36(a) is a Bode plot illustrating the magnitude and phase response of the common-mode feedback (CMFB) loop transmission before compensation. The graph consists of two subplots:

1. **Magnitude Plot**:
- **X-Axis**: Frequency, ranging from 10^6 Hz (1 MHz) to 10^9 Hz (1 GHz) on a logarithmic scale.
- **Y-Axis**: Magnitude in decibels (dB), ranging from -20 dB to 40 dB.
- **Behavior**: The magnitude starts at around 40 dB and decreases steadily as frequency increases, crossing 0 dB slightly above 10^8 Hz.

2. **Phase Plot**:
- **X-Axis**: Frequency, identical to the magnitude plot.
- **Y-Axis**: Phase in degrees, ranging from -300° to 0°.
- **Behavior**: The phase starts near 0° and decreases to about -190° at the unity-gain frequency (where the magnitude crosses 0 dB), continuing to drop towards -300° as the frequency increases further.

**Key Features**:
- The unity-gain frequency is a critical point where the magnitude crosses 0 dB, and the phase is approximately -190°, indicating a stability concern.
- The plot reveals a decreasing trend in both magnitude and phase as frequency increases, typical of a feedback loop before compensation.
- The phase margin at the unity-gain frequency is negative, suggesting potential instability without compensation.
image_name:Figure 11.36(b)
description:Figure 11.36(b) presents a Bode plot, which consists of two graphs showing the frequency response of a system after compensation. The top graph depicts the magnitude response, and the bottom graph shows the phase response.

1. **Magnitude Plot**:
- **Axes**: The x-axis represents frequency in hertz (Hz) on a logarithmic scale ranging from \(10^6\) to \(10^9\) Hz. The y-axis represents magnitude in decibels (dB), ranging from -100 dB to 50 dB.
- **Behavior**: The magnitude starts at around 40 dB and gradually decreases as frequency increases, showing a steady decline throughout the frequency range.
- **Key Features**: The plot does not indicate any peaks or resonances, suggesting a smooth roll-off in gain.

2. **Phase Plot**:
- **Axes**: The x-axis again represents frequency in hertz (Hz) on a logarithmic scale from \(10^6\) to \(10^9\) Hz. The y-axis represents phase in degrees, ranging from -300° to 0°.
- **Behavior**: The phase starts near 0° and decreases with increasing frequency. It crosses -100° and continues to decline, reaching approximately -300° at the highest frequencies.
- **Key Features**: The phase response indicates a phase margin improvement compared to the uncompensated system, with a smoother transition and no abrupt changes.

Overall, the compensated system in Figure 11.36(b) shows a stable frequency response with a gradual decrease in magnitude and phase, suggesting effective compensation with a phase margin of about 50°.

Figure 11.36 CMFB loop transmission (a) before and (b) after compensation.
Can we compensate the CM loop by adding capacitance from high-impedance nodes $X$ and $Y$ to ground? Yes, but this also affects the differential response. Instead, we tie a 3-pF capacitor from the error amplifier output to ground, obtaining the response shown in Fig. 11.36(b) and a phase margin of about $50^{\circ}$. The closed-loop pulse response depicted in Fig. 11.37(a) implies that the common-mode feedback loop is now properly compensated and the CM level incurs little ringing.

Differential Compensation Why do $V_{X}$ and $V_{Y}$ in Fig. 11.37(a) exhibit differential ringing? This is because the pole formed by the large resistors in the feedback network of Fig. 11.32(a) and the input
image_name:(a)
description:The graph in Figure 11.37(a) is a time-domain waveform illustrating the transient response of voltages $V_X$ and $V_Y$ over time with common-mode feedback (CMFB) loop compensation. The x-axis represents time in nanoseconds (ns), ranging from 0 to 40 ns, while the y-axis represents voltage in millivolts (mV), ranging from 350 mV to 650 mV.

**Overall Behavior and Trends:**
The graph shows two distinct waveforms, likely representing the differential outputs $V_X$ (in black) and $V_Y$ (in gray). Initially, both waveforms start at approximately 500 mV. The waveform for $V_X$ exhibits a peak reaching just above 600 mV around 5 ns, followed by a dip below 550 mV at approximately 10 ns, indicating ringing behavior. Similarly, $V_Y$ dips below 400 mV before rising sharply, also showing ringing. Both waveforms stabilize around 500 mV after 20 ns, indicating that the system eventually settles.

**Key Features and Technical Details:**
- **Ringing:** Both waveforms exhibit differential ringing, with $V_X$ peaking above 600 mV and $V_Y$ dipping below 400 mV.
- **Settling:** After the initial oscillations, both waveforms stabilize at around 500 mV, indicating the effectiveness of the CMFB loop compensation in reducing ringing over time.
- **Annotations:** There are no specific annotations or markers, but the gridlines suggest a focus on the transient behavior between 0 and 20 ns.

The graph effectively demonstrates the behavior of the system with CMFB loop compensation, highlighting the initial differential ringing and eventual stabilization of the voltages.
image_name:(b)
description:The graph in Fig. 11.37(b) is a time-domain waveform illustrating the transient response of a system with additional differential compensation. The x-axis is labeled "Time (ns)" and spans from 0 to 40 nanoseconds, while the y-axis is labeled "V_X, V_Y (mV)" and ranges from 350 to 650 millivolts.

The graph displays two curves, one in black and one in gray, representing the voltages V_X and V_Y, respectively. Initially, both voltages start at approximately 500 mV. The black curve (V_X) shows a rapid increase, peaking at around 600 mV within the first few nanoseconds, indicating a quick response to an input change. Following the peak, the voltage drops sharply to below 500 mV and then gradually stabilizes back to approximately 500 mV without significant overshoot or ringing.

The gray curve (V_Y) initially decreases to around 400 mV, also within the first few nanoseconds, before rising sharply back to approximately 500 mV, where it stabilizes. This behavior suggests a well-compensated differential response with minimal oscillation compared to the initial transient behavior.

Overall, the graph demonstrates effective differential compensation, as indicated by the smooth stabilization of both voltages with minimal ringing, contrasting with the more oscillatory response seen in Fig. 11.37(a).

Figure 11.37 Transient response with (a) CMFB loop compensation and (b) additional differential compensation.
capacitance of the op amp is located at a low frequency, degrading the phase margin (of differential feedback). To compensate the differential signal path, we connect two 7-fF capacitors from the outputs of the op amp to its inputs (in parallel with the feedback resistors) so as to create Miller multiplication. Shown in Fig. 11.37(b), the resulting response is now well behaved. This pole-zero cancellation technique is studied in Problem 11.14.

#### Example 11.9

Explain what design modifications are necessary if the op amp drives a significant load capacitance, $C_{L}$.

#### Solution

The load capacitance lowers the magnitude of the pole at $X$ (and $Y$ ), increasing the differential signal path phase margin (Chapter 10) while decreasing the CM loop phase margin. For this reason, the capacitance tied to the error
amplifier output must be increased, or the pole at $X$ and $Y$ must become the dominant pole for the CM loop as well.

Design Summary In this section, we have attempted to design a telescopic-cascode op amp for a voltage gain of 500 and a differential output swing of $1 \mathrm{~V}_{\mathrm{pp}}$. Neither specification could be met with a 1-V supply, but we have established the steps that one must complete in order to arrive at the final design. Specifically, we have dealt with the following general principles:

1. Allocation of $V_{D S}$ and $I_{D}$ to transistors according to required swings and power dissipation, respectively
2. Characterization and scaling of MOSFETs for allowable $V_{D S}$ and desired current level
3. Quick estimate of the achievable voltage gain
4. Use of dc sweep to study bias conditions and nonlinearity
5. Design of bias circuitry using current mirrors and low-voltage cascodes
6. Common-mode feedback design and compensation
7. Use of closed-loop transient analysis to study CM and differential stability

As seen in subsequent sections, these principles provide a systematic approach to the design of op amps.
The next natural candidate for our op amp design is the folded cascade. However, our gain calculations for the telescopic cascode roughly apply here as well, predicting that it is extremely difficult to achieve a gain of 500 . For this reason, we do not pursue the folded-cascode topology for these specifications.

### 11.5.2 Two-Stage Op Amp

Both the relatively high voltage gain and the $1-\mathrm{V}_{\mathrm{pp}}$ swing point to a two-stage configuration as a feasible candidate. We note that a gain of 500 dictates the use of cascoding in the first stage, encouraging us to utilize the telescopic design from the previous section (Fig. 11.21). However, two points must be borne in mind. First, the previous design exhausts the power budget, leaving none for the second stage. Second, with a gain of about 50 in the first stage, the gain of the second stage can be around 10 . Thus, the single-ended peak-to-peak swing at the outputs of the first stage can be as small as 50 mV , allowing us to redesign the cascode for greater $V_{D S}$ 's and hence more robust operation.

We must first partition the power budget between the two stages, a task requiring speed and/or noise specifications. We split the power equally here; further optimization could be pursued after one round of complete design. With about $100 \mu \mathrm{~A}$ reserved for the bias network, we allocate $1.9 \mathrm{~mA} / 4=475 \mu \mathrm{~A}$ to each branch of transistors in the first and second stages.
First-Stage Design The telescopic-cascode configuration must accommodate a single-ended swing of $50 \mathrm{mV}_{\mathrm{pp}}$, allowing 0.95 V for the sum of five $V_{D S}$ 's. With some margin, we choose $V_{D S, N}=150 \mathrm{mV}$ and $V_{D S, P}=200 \mathrm{mV}$ and simulate our reference transistors ( $W / L=5 \mu \mathrm{~m} / 40 \mathrm{~nm}$ and $10 \mu \mathrm{~m} / 80 \mathrm{~nm}$ ), seeking acceptable knee voltages. Shown in Fig. 11.38 for $V_{G S, N}=350 \mathrm{mV}$ and $V_{G S, P}=-450 \mathrm{mV}$, the characteristics exhibit substantially higher drain currents than those in Sec. 11.5.1. It is interesting to note that, as a result of velocity saturation, the knee voltage has not increased by 50 mV . The width of the NMOS transistors in the signal path must be scaled by a factor of $450 \mu \mathrm{~A} / 50 \mu \mathrm{~A}$ for either $L=40$ nm or $L=80 \mathrm{~nm}$. Similarly, the width of the PMOS device must be scaled by a factor of $450 \mu \mathrm{~A} / 90$ $\mu \mathrm{A}$ for $L=80 \mathrm{~nm}$. We also choose for the tail current device $W=(900 \mu \mathrm{~A} / 50 \mu \mathrm{~A}) \times 10 \mu \mathrm{~m}$ and $L=80 \mathrm{~nm}$. The cascode-stage devices are thus much narrower than those used in the previous section. The first-stage design is shown in Fig. 11.39(a) and its simulated behavior in Fig. 11.39(b), revealing a gain of about 50. The biasing of this stage is similar to that described in Sec. 11.5.1.
image_name:(a)
description:The graph in part (a) is an $I_D-V_{DS}$ characteristic curve for an NMOS device. The x-axis represents the drain-source voltage, $V_{DS}$, in volts (V), ranging from 0 to 0.4 V. The y-axis represents the drain current, $I_D$, in microamperes (µA), ranging from 0 to 100 µA. The graph displays two curves: a gray plot for a device with $W/L = 5 \mu \mathrm{m} / 40 \mathrm{~nm}$ and a black plot for a device with $W/L = 10 \mu \mathrm{m} / 80 \mathrm{~nm}$.\n\nThe curves show the relationship between the drain current and the drain-source voltage for different device dimensions. Both curves start at the origin (0,0) and exhibit a rising trend as $V_{DS}$ increases, indicating that the drain current increases with an increase in drain-source voltage. The black plot, representing the larger $W/L$ ratio, shows a higher slope and reaches a higher $I_D$ value at the same $V_{DS}$ compared to the gray plot, indicating a higher current capacity for the larger device dimensions.\n\nThe behavior suggests that the NMOS device with larger $W/L$ has better current driving capability due to increased channel width, which reduces the resistance and allows more current to flow for the same applied voltage. This is typical for MOSFET devices, where increasing the width of the channel allows for more carriers to contribute to the current flow."}
image_name:(b)
description:The graph in figure (b) illustrates the $I_D-V_{DS}$ characteristics for a PMOS device. This is a plot showing the relationship between the drain current ($I_D$) and the drain-source voltage ($V_{DS}$). The x-axis represents $V_{DS}$ in volts, ranging from -0.4 V to 0 V, while the y-axis represents the drain current $I_D$ in microamperes (µA), ranging from -120 µA to 0 µA.

Two curves are displayed: one in gray and one in black. The gray curve corresponds to a device with a width-to-length ratio ($W/L$) of $5 \mu m / 40 \ nm$, while the black curve corresponds to a $W/L$ ratio of $10 \mu m / 80 \ nm$.

Overall, the graph shows that as the magnitude of $V_{DS}$ increases (more negative), the magnitude of the drain current $I_D$ also increases (more negative), indicating typical PMOS behavior. The black curve is steeper than the gray curve, suggesting that the device with the larger $W/L$ ratio allows more current to flow for a given $V_{DS}$, indicating higher transconductance and drive capability.

Key features include the nonlinear increase in current as $V_{DS}$ approaches zero, with the black curve showing a more pronounced increase than the gray curve. This suggests that the device with a larger $W/L$ ratio is more efficient in conducting at lower $V_{DS}$ values.

Figure 11.38 $I_{D}-V_{D S}$ characteristics for (a) an NMOS device with $V_{G S}=350 \mathrm{mV}$ and $W / L=5 \mu \mathrm{~m} / 40 \mathrm{~nm}$ (gray plot) or $10 \mu \mathrm{~m} / 80 \mathrm{~nm}$ (black plot), and (b) a PMOS device with $V_{G S}=-450 \mathrm{mV}$ and $W / L=5 \mu \mathrm{~m} / 40 \mathrm{~nm}$ (gray plot) or $10 \mu \mathrm{~m} / 80 \mathrm{~nm}$ (black plot).

#### Example 11.10

In order to determine, with the aid of simulation, the small-signal resistance seen at node $X$ in Fig. 11.39(a), a student sets the input signal to zero, ties a unit ac current source from this node to ground, and measures the resulting voltage. Explain why this test overestimates the resistance.

#### Solution

The voltage developed at $X$ causes a current to flow through $r_{O 3}$ to the drain of $M_{1}$ and through $r_{O 1}$ to the source of $M_{2}$. In other words, since $M_{1}$ is degenerated by $M_{2}$, the resistance at $X$ is overestimated. To avoid this error, a large
image_name:Figure 11.39 (a)
description:
[
name: M1, type: NMOS, ports: {S: P, D: d1s3, G: Vin}
name: M2, type: NMOS, ports: {S: Vin-, D: d2s4, G: P}
name: M3, type: NMOS, ports: {S: d1s3, D: X, G: Vb1}
name: M4, type: NMOS, ports: {S: d2s4, D: Y, G: X}
name: M5, type: PMOS, ports: {S: X, D: Vb2, G: Vb3}
name: M6, type: PMOS, ports: {S: Y, D: s5d6, G: Vb2}
name: M7, type: PMOS, ports: {S: VDD, D: s5d7, G: Vb3}
name: M8, type: PMOS, ports: {S: s5d7, D: s5d8, G: Vb3}
]
extrainfo:The circuit in Figure 11.39(a) is a multi-stage amplifier design. It includes NMOS and PMOS transistors configured to achieve specific voltage gains. The second stage is designed to provide a voltage gain of about 10. The transistors are labeled with specific channel lengths, indicating their design parameters for achieving the desired electrical characteristics.
image_name:Figure 11.39 (b)
description:The graph in Figure 11.39(b) is a plot showing the input-output characteristics of a circuit. It is a Cartesian plot with the x-axis labeled as $V_{in}$, representing the input voltage in millivolts (mV), and the y-axis labeled as $V_X, V_Y$, representing the output voltages at nodes X and Y, also in millivolts (mV).

**Axes and Units:**
- **X-axis:** Input voltage $V_{in}$, ranging from -20 mV to 20 mV.
- **Y-axis:** Output voltages $V_X$ and $V_Y$, ranging from 200 mV to 800 mV.
- The scale on both axes is linear, with gridlines marking significant intervals.

**Overall Behavior and Trends:**
- The graph displays two curves: one representing $V_X$ and the other representing $V_Y$.
- As $V_{in}$ increases from -20 mV to 20 mV, $V_X$ shows a decreasing trend, starting from around 700 mV and dropping to approximately 300 mV.
- Conversely, $V_Y$ shows an increasing trend, starting from around 300 mV and rising to approximately 700 mV.
- The curves intersect at approximately $V_{in} = 0$ mV, where both $V_X$ and $V_Y$ are around 500 mV.

**Key Features and Technical Details:**
- The intersection point at $V_{in} = 0$ mV suggests a symmetry in the circuit's response to positive and negative input voltages.
- The curves are smooth and continuous, indicating a linear or near-linear relationship within this input range.
- The symmetry and crossing point at 500 mV for $V_X$ and $V_Y$ suggest balanced characteristics for the circuit.

**Annotations and Specific Data Points:**
- No specific numerical annotations are present on the graph, but the gridlines provide reference points for estimating values.
- The crossing point at $V_{in} = 0$ mV and $V_X = V_Y = 500$ mV is a critical feature of this plot, indicating the point of equal output voltages for the given input.

Figure 11.39 (a) First stage design, and (b) its input-output characteristics.
capacitance must be tied from the source of $M_{1}$ to ground to create a short circuit at the test frequency. Alternatively, we can attach the ac current source between $X$ and $Y$, measure the resistance, and divide the result by two.

### 11.5.3 Second-Stage Design
Second-Stage Design The second stage must provide a voltage gain of about 10, dictating channel lengths greater than 40 nm for both NMOS and PMOS devices. Do we use an NFET or a PFET for the input of the second stage? The need for gain may point to an NFET due to its higher $g_{m} r_{O}$, but we must examine the situation more closely. Bearing in mind that the output CM level of the first stage is around 0.55 V , let us consider a transistor having $W / L=10 \mu \mathrm{~m} / 80 \mathrm{~nm}$ and determine its $g_{m} r_{O}$ if it is an NFET with $V_{G S} \approx 0.55 \mathrm{~V}$ or a PFET with $\left|V_{G S}\right| \approx 0.45 \mathrm{~V}$. Using simulations, we obtain $\left(g_{m} r_{O}\right)_{N}=12.8$ and $r_{O N}=1.86 \mathrm{k} \Omega$ at $V_{D S}=0.5 \mathrm{~V}$ and $I_{D}=900 \mu \mathrm{~A}$, and $\left(g_{m} r_{O}\right)_{P}=17.5$ and $r_{O P}=9.75 \mathrm{k} \Omega$ at $\left|V_{D S}\right|=0.5 \mathrm{~V}$ and $\left|I_{D}\right|=110 \mu \mathrm{~A}$. We therefore select the PFET and scale its width to $(450 \mu \mathrm{~A} / 110 \mu \mathrm{~A}) \times 10 \mu \mathrm{~m} \approx 41 \mu \mathrm{~m}$ to accommodate the nominal bias current. With $W / L=41 \mu \mathrm{~m} / 80 \mathrm{~nm}$, such a device exhibits an output resistance of $2.38 \mathrm{k} \Omega$. The drain of the PFET is tied to an NMOS current source.

The NMOS current source output resistance must not lower the gain of the second stage, $\left|A_{v 2}\right|$, below 10. Writing $\left|A_{v 2}\right|=g_{m P}\left(r_{O P}| | r_{O N}\right) \geq 10$, we have $r_{O N} \geq 1.33 r_{O P}=3.0 \mathrm{k} \Omega$ at $I_{D}=475 \mu \mathrm{~A}$. If the $10-\mu \mathrm{m} / 80-\mathrm{nm}$ NFET considered above with $r_{O}=1.86 \mathrm{k} \Omega$ and $I_{D}=900 \mu \mathrm{~A}$ is scaled down by a factor of 2 , it yields $r_{O N}=3.72 \mathrm{k} \Omega$, which is close to the desired value.

Figure 11.40(a) shows the op amp developed thus far, and Fig. 11.40(b) plots the input-output characteristics. In order to determine the maximum output swing that the op amp can handle, we plot the slope of the differential characteristic in Fig. 11.40(c), noting that the differential output cannot exceed 450 mV if the gain must not drop below 500. To resolve this issue, we double the width and length of the output NFETs, raising the gain and arriving at the results depicted in Fig. 11.41. Now, the single-ended swing reaches 530 mV for a minimum gain of 500. Of course, the gain variation (nonlinearity) is unabated, posing difficulties in some applications.

Common-Mode Feedback As explained in Chapter 9, two-stage op amps generally require CMFB for both stages. For the first stage, we can utilize the CMFB scheme illustrated in Fig. 11.29. We therefore focus on CMFB for the second stage.

The second stage can also incorporate the method of Fig. 11.29 and control the NMOS current sources. However, the lower output impedance here allows the use of resistors for direct sensing of the CM level,
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1s3, G: Vin+, B: GND}
name: M2, type: NMOS, ports: {S: GND, D: d2s4, G: Vin-, B: GND}
name: M3, type: NMOS, ports: {S: d1s3, D: X, G: Vb1, B: GND}
name: M4, type: NMOS, ports: {S: d2s4, D: Y, G: Vb1, B: GND}
name: M5, type: NMOS, ports: {S: X, D: ssd7, G: Vb5, B: GND}
name: M6, type: PMOS, ports: {S: VDD, D: ssd8, G: Vb2, B: VDD}
name: M7, type: PMOS, ports: {S: VDD, D: ssd7, G: Vb2, B: VDD}
name: M8, type: PMOS, ports: {S: VDD, D: ssd8, G: Vb2, B: VDD}
name: M9, type: PMOS, ports: {S: VDD, D: X, G: Vb3, B: VDD}
name: M10, type: PMOS, ports: {S: VDD, D: Y, G: Vb3, B: VDD}
name: M11, type: NMOS, ports: {S: GND, D: Vout1, G: Vb4, B: GND}
name: M12, type: NMOS, ports: {S: GND, D: Vout2, G: Vb5, B: GND}
]
extrainfo:The circuit is a two-stage operational amplifier with common-mode feedback. It includes NMOS and PMOS transistors and utilizes bias voltages Vb1, Vb2, Vb3, Vb4, and Vb5. The PMOS transistors are connected to the power supply VDD, and the NMOS transistors are connected to ground. The circuit has differential inputs Vin+ and Vin- and differential outputs Vout1 and Vout2.
image_name:(b)
description:The graph labeled "(b)" is a plot depicting the input-output characteristics of a two-stage operational amplifier. It is a Cartesian graph with the x-axis labeled as $V_{in}$ (mV), representing the input voltage in millivolts, ranging from -2 mV to 2 mV. The y-axis has two scales: on the left, it is labeled $V_{out1}, V_{out2}$ (mV), representing the output voltages in millivolts, ranging from 0 mV to 1000 mV.

The graph shows two curves, each representing the output voltage of one of the two outputs, $V_{out1}$ and $V_{out2}$. The curve for $V_{out1}$ starts at approximately 1000 mV when $V_{in}$ is -2 mV and decreases linearly to around 200 mV as $V_{in}$ increases to 2 mV. Conversely, the curve for $V_{out2}$ starts at approximately 200 mV when $V_{in}$ is -2 mV and increases linearly to around 1000 mV as $V_{in}$ increases to 2 mV.

This behavior indicates that the output voltages are inversely related to each other across the input voltage range, exhibiting a complementary relationship typical of differential output stages in operational amplifiers. The linearity of the curves suggests a proportional relationship between input and output voltages within the given range. The graph is marked with grid lines at intervals of 200 mV on the y-axis and 1 mV on the x-axis, aiding in the visualization of the input-output relationship.
image_name:(c)
description:The graph labeled (c) is a plot of gain versus input voltage (Vin) for a two-stage operational amplifier.

1. **Type of Graph and Function:**
- This is a gain plot, showing how the gain of the amplifier varies with different input voltages.

2. **Axes Labels and Units:**
- The x-axis represents the input voltage (Vin) in millivolts (mV), ranging from -2 mV to 2 mV.
- The y-axis represents the gain, without specific units, ranging from 100 to 700.
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The graph shows a peak in gain around an input voltage of 0 mV, indicating the maximum gain occurs at this point.
- The gain decreases symmetrically as the input voltage moves away from 0 mV in either direction.
- This behavior suggests a bell-shaped curve, which is typical for gain versus input voltage plots in amplifiers.

4. **Key Features and Technical Details:**
- The maximum gain is approximately 700, occurring at 0 mV input voltage.
- The gain drops to about 100 at the extremes of -2 mV and 2 mV input voltage.
- This indicates a sharp peak, suggesting high sensitivity around the zero input voltage point.

5. **Annotations and Specific Data Points:**
- There are no specific annotations or markers on the graph, but the symmetry and peak are clearly visible.
- The plot effectively illustrates the operational range and sensitivity of the amplifier to input voltage changes.

Figure 11.40 (a) Two-stage op amp design, (b) its input-output characteristics, and (c) its gain variation.
simplifying the design. Consider the topology depicted in Fig. 11.42(a), where $R_{1}$ and $R_{2}$ ( $\approx 30 \mathrm{k} \Omega$ ) reconstruct the CM level at node $G$, applying the result to the gates of $M_{11}$ and $M_{12}$. Under equilibrium, the resistors draw no current, establishing an output CM voltage equal to $V_{G S 11,12}$. This voltage varies by about 50 mV with PVT, a value that can be tolerated in this design. Note that this CMFB loop is stable.

What if $V_{G S 11,12}$ is not close to the desired output CM level? As shown in Fig. 11.42(b), if we inject a current $I_{B}$ into node $G$, the output CM level is shifted by $I_{B} R_{1} / 2\left(=I_{B} R_{2} / 2\right)$. For example, a shift of 100 mV requires a current of $(100 \mathrm{mV} / 30 \mathrm{k} \Omega) \times 2=6.7 \mu \mathrm{~A}$. A positive $I_{B}$ shifts the CM level down and vice versa.

Frequency Compensation The two-stage op amp designed above contains several poles and most likely demands compensation. Recall from Chapter 10 that the first nondominant pole of two-stage op amps typically arises from the output node and hence depends on the load capacitance, $C_{L}$. The stability
image_name:(a)
description:The graph labeled "(a)" is a plot of the input-output characteristics of a modified two-stage operational amplifier. It features two curves representing output voltages \( V_{out1} \) and \( V_{out2} \) as functions of the input voltage \( V_{in} \), measured in millivolts (mV). The x-axis represents \( V_{in} \) ranging from -2 mV to 2 mV, while the y-axis represents the output voltages \( V_{out1} \) and \( V_{out2} \) in millivolts, ranging from 0 to 1000 mV.

**Overall Behavior and Trends:**
- **\( V_{out1} \):** The curve for \( V_{out1} \) starts at a high value when \( V_{in} \) is -2 mV and decreases as \( V_{in} \) increases, reaching a lower value at 2 mV. This indicates a negative correlation between \( V_{in} \) and \( V_{out1} \).
- **\( V_{out2} \):** Conversely, the curve for \( V_{out2} \) starts at a low value when \( V_{in} \) is -2 mV and increases as \( V_{in} \) increases, reaching a higher value at 2 mV. This indicates a positive correlation between \( V_{in} \) and \( V_{out2} \).

**Key Features and Technical Details:**
- The curves intersect at \( V_{in} = 0 \) mV, where both \( V_{out1} \) and \( V_{out2} \) have equal values, approximately 500 mV.
- The graph demonstrates the complementary nature of the output voltages, with one increasing as the other decreases across the range of \( V_{in} \).

**Annotations and Specific Data Points:**
- The gridlines provide clear reference points at every 200 mV increment on both axes, aiding in the visualization of the trends and intersections of the curves.
image_name:(b)
description:The graph labeled (b) is a plot showing the gain variation of a modified two-stage operational amplifier as a function of the input voltage, \( V_{in} \), measured in millivolts (mV). The horizontal axis represents the input voltage \( V_{in} \) ranging from -2 mV to 2 mV, while the vertical axis represents the gain, which is dimensionless and ranges from 0 to 800.

Overall Behavior and Trends
The graph exhibits a bell-shaped curve, indicating that the gain of the amplifier increases with \( V_{in} \), reaches a peak, and then decreases as \( V_{in} \) continues to rise. This behavior suggests a resonant or optimal operating point where the gain is maximized.

Key Features and Technical Details
- The gain starts at approximately 100 when \( V_{in} \) is -2 mV.
- The gain increases sharply as \( V_{in} \) approaches 0 mV.
- A peak gain of approximately 700 is observed around \( V_{in} = 0 \) mV, indicating the maximum amplification point.
- Beyond this peak, the gain decreases symmetrically as \( V_{in} \) approaches 2 mV, returning to around 100.

Annotations and Specific Data Points
- The peak gain is a critical value indicating the optimal input voltage for maximum amplification, which is around 0 mV in this case.
- The symmetry of the curve suggests that the system behaves similarly for positive and negative deviations from the optimal \( V_{in} \).

Figure 11.41 (a) Input-output characteristics and (b) gain variation of modified two-stage op amp with $(W / L)_{11,12}=10 \mu \mathrm{~m} / 0.16 \mu \mathrm{~m}$.
image_name:Figure 11.41 (a)
description:
[
name: M1, type: NMOS, ports: {S: G, D: P, G: Vin1}
name: M2, type: NMOS, ports: {S: G, D: d2s4, G: Vin2}
name: M3, type: NMOS, ports: {S: d1s3, D: Y, G: Vb1}
name: M4, type: NMOS, ports: {S: d2s4, D: Y, G: Vb1}
name: M5, type: PMOS, ports: {S: VDD, D: X, G: Y}
name: M6, type: PMOS, ports: {S: VDD, D: Y, G: Vb2}
name: M7, type: PMOS, ports: {S: VDD, D: X, G: Vb2}
name: M8, type: PMOS, ports: {S: VDD, D: Y, G: Vb2}
name: M9, type: PMOS, ports: {S: VDD, D: Vout1, G: X}
name: M10, type: PMOS, ports: {S: VDD, D: Vout2, G: Y}
name: M11, type: NMOS, ports: {S: GND, D: G, G: Vout1}
name: M12, type: NMOS, ports: {S: GND, D: G, G: Vout2}
name: R1, type: Resistor, value: R1, ports: {N1: Vin1, N2: G}
name: R2, type: Resistor, value: R2, ports: {N1: Vin2, N2: G}
name: IB, type: CurrentSource, value: IB, ports: {Np: VDD, Nn: G}
]
extrainfo:This is a modified two-stage operational amplifier circuit with common-mode feedback around the second stage. The circuit is designed to manage input-output characteristics and gain variation. It features a combination of NMOS and PMOS transistors, with a focus on maintaining symmetry and optimal gain.
image_name:Figure 11.41 (b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: P, G: Vin1}
name: M2, type: NMOS, ports: {S: Vin2, D: d2s4, G: Y}
name: M3, type: NMOS, ports: {S: d1s3, D: X, G: Vb1}
name: M4, type: NMOS, ports: {S: d2s4, D: Y, G: Vb1}
name: M5, type: PMOS, ports: {S: VDD, D: X, G: Vb2}
name: M6, type: PMOS, ports: {S: VDD, D: Y, G: Vb2}
name: M7, type: PMOS, ports: {S: VDD, D: Vb2, G: Vb3}
name: M8, type: PMOS, ports: {S: VDD, D: Vb2, G: Vb3}
name: M9, type: PMOS, ports: {S: VDD, D: X, G: Vout1}
name: M10, type: PMOS, ports: {S: VDD, D: Y, G: Vout2}
name: M11, type: NMOS, ports: {S: GND, D: G, G: Vin1}
name: M12, type: NMOS, ports: {S: GND, D: G, G: Vin2}
name: R1, type: Resistor, value: R1, ports: {N1: Vin1, N2: G}
name: R2, type: Resistor, value: R2, ports: {N1: G, N2: Vin2}
name: IB, type: CurrentSource, value: IB, ports: {Np: VDD, Nn: G}
]
extrainfo:This circuit is a modified two-stage operational amplifier with common-mode feedback. It includes NMOS and PMOS transistors forming differential pairs and current mirrors, and uses resistors and a current source for biasing. The circuit is designed to manage input-output characteristics and gain variation, with specific attention to common-mode feedback and load capacitance effects.

Figure 11.42 (a) Simple common-mode feedback around the second stage; (b) injection of current to shift CM level.
analysis must therefore assume a value of $C_{L}$, which itself is given by the environment in which the op amp is used. Let us choose a single-ended load capacitance of 1 pF in this example, obtaining an output pole frequency of around 90 MHz . We begin the study with the open-loop op amp, bearing in mind that the feedback network may add its own effects and eventually require further modifications.

Plotted in Fig. 11.43 are the open-loop (differential) magnitude and phase response of the circuit, revealing a low-frequency gain of $57 \mathrm{~dB}(\approx 700)$, a unity-gain frequency of 3.2 GHz , and a phase margin of about $-8^{\circ}$. This bandwidth appears very impressive, but we also note that the phase reaches $-120^{\circ}$ at 240 MHz . In other words, after compensation for $60^{\circ}$ phase margin, the unity-gain bandwidth can drop by a factor of 13 !
image_name:Figure 11.43 Frequency response of open-loop op amp
description:The graph in Figure 11.43 is a Bode plot, which is commonly used to represent the frequency response of an open-loop operational amplifier (op amp). It consists of two plots: a magnitude plot (in decibels) and a phase plot (in degrees), both plotted against frequency (in hertz) on a logarithmic scale.

Magnitude Plot:
- **Y-Axis (Magnitude in dB):** The vertical axis represents the gain magnitude in decibels (dB).
- **X-Axis (Frequency in Hz):** The horizontal axis represents the frequency ranging from $10^5$ Hz to $10^{10}$ Hz.
- **Behavior:** The magnitude starts at approximately 57 dB at low frequencies and remains relatively flat until around $10^7$ Hz. Beyond this frequency, the magnitude begins to decrease, indicating a roll-off typical of a low-pass filter response.
- **Key Features:** The unity-gain frequency, where the magnitude crosses 0 dB, is indicated at 3.2 GHz (or $3.2 \times 10^9$ Hz).

Phase Plot:
- **Y-Axis (Phase in Degrees):** The vertical axis represents the phase shift in degrees.
- **X-Axis (Frequency in Hz):** The horizontal axis is the same as the magnitude plot, with a logarithmic frequency scale from $10^5$ Hz to $10^{10}$ Hz.
- **Behavior:** The phase starts near 0 degrees at low frequencies and decreases as frequency increases. At around 240 MHz, the phase reaches approximately -120 degrees, continuing to decrease as frequency increases.
- **Key Features:** The phase margin, which is the difference between the phase at the unity-gain frequency and -180 degrees, is about -8 degrees, indicating potential stability issues. The phase does not reach -135 degrees at 90 MHz, contrary to expectations from a simple pole model, due to closely spaced poles.

Annotations and Specific Data Points:
- The graph highlights the low-frequency gain of 57 dB, unity-gain frequency of 3.2 GHz, and a phase margin of about -8 degrees. The phase at 240 MHz is noted as -120 degrees, which is relevant for compensation considerations.

Figure 11.43 Frequency response of open-loop op amp.

#### Example 11.11

The above results are rather curious: the output pole is located around 90 MHz , suggesting a phase of about $-135^{\circ}$ at this frequency, but the actual phase is around $-85^{\circ}$ at this frequency. Explain the reason for this behavior.

#### Solution

In the above design, we cannot say that the phase reaches $-135^{\circ}$ at the second pole because the poles are not widely spaced. In fact, the pole at $X$ in Fig. 11.42 is around 95 MHz . The pole at $X$ and the output pole produce at 90 MHz a phase shift of $-\tan ^{-1}(90 / 95)-\tan ^{-1}(90 / 90) \approx-88^{\circ}$.

We express the phase shift at 240 MHz due to these two poles as $-\tan ^{-1}(240 \mathrm{MHz} / 95 \mathrm{MHz})-\tan ^{-1}(240 \mathrm{MHz} /$ $90 \mathrm{MHz})=-138^{\circ}$. Why does this result disagree with the simulated value of $-120^{\circ}$ ? This is because the gate-drain capacitance of the output PMOS transistor creates some pole splitting, raising the output pole beyond 90 MHz and lowering the pole at $X$ below 95 MHz .

In order to compensate the op amp, we begin at 240 MHz and 0 dB on the magnitude plot in Fig. 11.43 and draw a straight line toward the $y$-axis with a slope of $-20 \mathrm{~dB} / \mathrm{dec}$. The frequency at which this line intersects the magnitude plot is roughly equal to $240 \mathrm{MHz} / 700=344 \mathrm{kHz}$ (why?), yielding the desired value for the dominant pole.

Which node should produce the dominant pole: $X$ or the output node? We prefer the former for two reasons, namely, a smaller compensation capacitance due to Miller multiplication and pole splitting; neither of these benefits accrues if the dominant pole is established at the output.

With the output resistance of $8 \mathrm{k} \Omega$ seen at node $X$ and a voltage gain of about 12 provided by the output stage, we choose a Miller compensation capacitor, $C_{C}$, equal to 4.5 pF so as to create a $344-\mathrm{kHz}$ pole at this node. Figure 11.44 shows the resulting open-loop frequency response, confirming that the dominant pole is now located around 340 kHz . Unfortunately, the gain crossover occurs at 350 MHz and the phase margin is only $18^{\circ}$ because the zero introduced by $C_{C}, \omega_{z}=g_{m 10} / C_{C}$, is as low as 250 MHz . As explained in Chapter 10, we can insert a resistor, $R_{z}$, in series with $C_{C}$ so as to move the zero to the second pole, $\omega_{p 2}$. The second pole can be roughly estimated from Fig. 11.44 as the frequency at
image_name:C_C=4.5 pF
description:
[
name: M10, type: PMOS, ports: {S: VDD, D: N1, G: N1}
name: Cc, type: Capacitor, value: 4.5 pF, ports: {Np: N1, Nn: N2}
name: M12, type: NMOS, ports: {S: GND, D: N2, G: N1}
]
extrainfo:The circuit is a part of an open-loop operational amplifier frequency response analysis. The capacitor Cc introduces a zero in the frequency response.
image_name:Figure 11.44
description:The graph in Figure 11.44 is a Bode plot representing the frequency response of a compensated open-loop operational amplifier with a compensation capacitor \(C_C\) of 4.5 pF. It is divided into two parts: the magnitude plot and the phase plot.

Magnitude Plot:
- **Type:** Logarithmic scale Bode plot.
- **X-axis:** Frequency in hertz (Hz), ranging from \(10^5\) to \(10^9\) Hz.
- **Y-axis:** Magnitude in decibels (dB), ranging from -20 dB to 60 dB.
- **Behavior:** The magnitude starts around 60 dB at low frequencies and decreases steadily, crossing 0 dB around the gain crossover frequency of 350 MHz.
- **Trend:** The graph shows a typical roll-off behavior as frequency increases, indicating a decrease in gain.

Phase Plot:
- **Type:** Logarithmic scale Bode plot.
- **X-axis:** Frequency in hertz (Hz), same range as the magnitude plot.
- **Y-axis:** Phase in degrees, ranging from -300° to 0°.
- **Behavior:** The phase starts near 0° at low frequencies and decreases, crossing -135° at approximately 185 MHz, which corresponds to the second pole frequency.
- **Trend:** The phase continues to decrease, indicating a lag as frequency increases.

Key Features:
- **Dominant Pole:** Located around 340 kHz, influencing the initial phase and magnitude behavior.
- **Zero Introduced by \(C_C\):** Located at 250 MHz, affecting the phase margin and gain crossover.
- **Second Pole:** Estimated at 185 MHz, where the phase reaches -135°.
- **Gain Crossover Frequency:** Occurs at approximately 350 MHz with a phase margin of 18°, indicating potential instability.

Annotations:
- The plot includes gridlines and markers at significant frequencies, aiding in the identification of key points such as the gain crossover and second pole frequency. This visual representation is crucial for analyzing the stability and performance of the op amp circuit.

Figure 11.44 Frequency response of compensated open-loop op amp with $C_{C}=4.5 \mathrm{pF}$.
which $\angle H$ reaches $-135^{\circ}$ and is equal to 185 MHz . Selecting $R_{z}$ according to $\left(\omega_{p 2} C_{C}\right)^{-1}=190 \Omega$, we observe the response depicted in Fig. 11.45(a). The phase margin rises to $96^{\circ}$ because of the pole-zero cancellation.

The phase margin revealed by Fig. 11.45(a) suggests that the compensation capacitor can be smaller and the unity-gain bandwidth larger. By some iteration, we choose $C_{C}=0.8 \mathrm{pF}$ and $R_{z}=450 \Omega$, arriving at the response shown in Fig. 11.45(b). Remarkably, the op amp now exhibits a unity-gain bandwidth of 1.9 GHz with a phase margin of $65^{\circ}$.

Closed-Loop Behavior We now configure the op amp as a closed-loop amplifier having a nominal gain of 2 and a load capacitance of 1 pF [Fig. 11.46(a)]. The small-signal transient response appears as shown in Fig. 11.46(b), exhibiting significant ringing. Why does this happen despite the $65^{\circ}$ phase margin obtained above? This is due to the large resistance values used in the feedback network. We draw the single-ended equivalent as in Fig. 11.47(a) for the loop transmission calculation, observing that an open-loop pole around $\left[2 \pi(100 \mathrm{k} \Omega \| 50 \mathrm{k} \Omega) C_{i n}\right]^{-1} \approx 95 \mathrm{MHz}$ is formed at the input of the op amp.

In order to improve the closed-loop stability, we can reduce $R_{1}$ and $R_{2}$ in Fig. 11.47(a) to, say, $25 \mathrm{k} \Omega$ and $50 \mathrm{k} \Omega$, respectively, before the open-loop gain falls appreciably, but this remedy only doubles the input pole frequency. Alternatively, we can increase the resistance in series with the compensation capacitors from $450 \Omega$ to $1500 \Omega$, arriving at the response shown in Fig. 11.47(b). The circuit now settles much faster.

We conclude this section with two remarks. First, the op amp has been compensated for unity-gain feedback, whereas the topology of Fig. 11.46 operates with a feedback factor of $50 \mathrm{k} \Omega / 150 \mathrm{k} \Omega=1 / 3$. Thus, the compensation capacitance can be reduced to lower the phase margin to around $60^{\circ}$. Second, the design has assumed the "typical-NMOS, typical-PMOS" (TT) corner of the process, a temperature of $27^{\circ} \mathrm{C}$, and a constant supply of 1 V . In practice, we must account for other corners (e.g., SS or FF), the required temperature range (e.g., $0^{\circ} \mathrm{C}$ to $75^{\circ} \mathrm{C}$ ), and supply variations (e.g., by $\pm 5 \%$ ). To meet the specifications under all of these conditions, the design must often be more conservative in terms of gain, swings, and power consumption than that presented here.
image_name:(a)
description:
[
name: Cc, type: Capacitor, value: 4.5 pF, ports: {Np: g12, Nn: rc}
name: Rz, type: Resistor, value: 190 Ω, ports: {N1: rc, N2: diode12}
name: M10, type: PMOS, ports: {S: VDD, D: diode12, G: g10}
name: M12, type: NMOS, ports: {S: GND, D: diode12, G: Vb}
]
extrainfo:The circuit is an open-loop amplifier with PMOS and NMOS transistors. It includes a compensation capacitor and a zero resistor for frequency response tuning.
image_name:Figure 11.45
description:The graph in Figure 11.45 is a Bode plot representing the frequency response of an open-loop amplifier with specific component values: \(C_{C}=4.5\,\text{pF}\) and \(R_{Z}=190\,\Omega\). It consists of two main plots: the magnitude plot and the phase plot.

1. **Magnitude Plot:**
- **Axes:**
- The x-axis represents frequency in hertz (Hz), ranging from \(10^5\) to \(10^{10}\) Hz on a logarithmic scale.
- The y-axis represents magnitude in decibels (dB), ranging from -50 dB to 100 dB.
- **Behavior:**
- The magnitude starts at approximately 60 dB at lower frequencies and gradually decreases as the frequency increases.
- There is a noticeable slope indicating a roll-off, suggesting a decrease in gain with increasing frequency.

2. **Phase Plot:**
- **Axes:**
- The x-axis, similar to the magnitude plot, represents frequency in hertz (Hz) on a logarithmic scale.
- The y-axis represents phase in degrees, ranging from -200° to 0°.
- **Behavior:**
- The phase starts near 0° at low frequencies and decreases as frequency increases.
- There is a significant phase drop between \(10^6\) Hz and \(10^9\) Hz, indicating a phase lag typically associated with capacitive effects in the circuit.

3. **Key Features:**
- The magnitude plot shows a steady decline typical of a first-order low-pass filter response, with no specific resonance peaks.
- The phase plot indicates a lagging phase shift, suggesting a dominant pole contributing to the frequency response.
- The -3 dB point (cut-off frequency) is not explicitly marked but can be inferred from the magnitude plot's downward trend.

This Bode plot provides insights into the amplifier's bandwidth, gain, and phase margin, essential for assessing stability and performance in various applications.

(a)
image_name:(a)
description:
[
name: Cc, type: Capacitor, value: 0.8 pF, ports: {Np: g10, Nn: rc}
name: Rz, type: Resistor, value: 450 Ω, ports: {N1: rc, N2: diod12}
name: M10, type: PMOS, ports: {S: VDD, D: diod12, G: g10}
name: M12, type: NMOS, ports: {S: GND, D: diod12, G: Vc}
]
extrainfo:The circuit is an open-loop amplifier with a frequency response characterized by a first-order low-pass filter. The Bode plot shows a magnitude plot with a downward trend and a phase plot indicating a lagging phase shift, suggesting a dominant pole. The cut-off frequency can be inferred from the plot.
image_name:Figure 11.45 (b)
description:The graph shown is a Bode plot, which consists of two parts: a magnitude plot and a phase plot, both of which are used to analyze the frequency response of an open-loop amplifier. The specific configuration for this plot is with a compensation capacitor \(C_C\) of 0.8 pF and a zero-resistance \(R_Z\) of 450 \(\Omega\).

Magnitude Plot:
- **Y-Axis (Magnitude in dB):** The vertical axis represents the magnitude of the frequency response in decibels (dB).
- **X-Axis (Frequency in Hz):** The horizontal axis is logarithmically scaled and represents frequency in hertz (Hz), ranging from \(10^5\) to \(10^{10}\) Hz.
- **Overall Behavior:** The magnitude plot starts at a high level and shows a gradual decrease as frequency increases. This indicates a typical low-pass filter behavior where higher frequencies are attenuated.
- **Key Features:** There is no specific resonance peak, and the -3 dB point, which indicates the cutoff frequency, is implied by the downward trend but not explicitly marked.

Phase Plot:
- **Y-Axis (Phase in Degrees):** The vertical axis shows the phase angle in degrees.
- **X-Axis (Frequency in Hz):** The same logarithmic frequency scale is used as in the magnitude plot.
- **Overall Behavior:** The phase plot shows a lagging phase shift, starting near 0 degrees at low frequencies and decreasing to about -180 degrees as frequency increases.
- **Key Features:** The phase shift indicates the presence of a dominant pole affecting the frequency response, typical for a first-order low-pass filter.

General Insights:
This Bode plot provides insights into the amplifier's bandwidth and phase margin, which are crucial for understanding its stability and performance in various applications. The absence of resonance peaks and the gradual phase shift suggest a stable and predictable frequency response.

Figure 11.45 Frequency response of open-loop amp with (a) $C_{C}=4.5 \mathrm{pF}$ and $R_{Z}=190 \Omega$, and (b) $C_{C}=0.8 \mathrm{pF}$ and $R_{Z}=450 \Omega$.
image_name:(a)
description:
[
name: R1, type: Resistor, value: 50kΩ, ports: {N1: Vip, N2: InP(A1)}
name: R1, type: Resistor, value: 50kΩ, ports: {N1: Vin, N2: InN(A1)}
name: R2, type: Resistor, value: 100kΩ, ports: {N1: OutP(Av), N2: OutN(Av)}
name: R2, type: Resistor, value: 100kΩ, ports: {N1: OutN(Av), N2: InN(A1)}
name: C1, type: Capacitor, value: 1pF, ports: {Np: OutN(Av), Nn: GND}
name: C1, type: Capacitor, value: 1pF, ports: {Np: OutP(Av), Nn: GND}
name: Av, type: OpAmp, value: Av, ports: {InP: InP(A1), InN: InN(A1), OutP: OutP(Av), OutN: OutN(Av)}
]
extrainfo:This circuit is a differential amplifier configuration using an operational amplifier with feedback resistors R1 and R2. The capacitors C1 are used for stability and frequency compensation. The input signals are Vip and Vin, and the output is taken between OutP(Av) and OutN(Av).
image_name:(b)
description:The graph in part (b) is a time-domain waveform illustrating the step response of a closed-loop amplifier. The x-axis represents time in nanoseconds (ns), ranging from 0 to 40 ns. The y-axis shows the output voltage, \( V_{out1}, V_{out2} \), in millivolts (mV), ranging from 470 mV to 530 mV.

The graph displays two waveforms, one in black and the other in gray, representing the output responses \( V_{out1} \) and \( V_{out2} \) of the amplifier to a step input. Initially, both waveforms start at approximately 500 mV.

- **Black waveform (\( V_{out1} \)):** This waveform shows an initial overshoot, reaching about 525 mV at around 5 ns. It then slightly undershoots below 500 mV before settling back to a steady-state value slightly above 500 mV after approximately 30 ns.

- **Gray waveform (\( V_{out2} \)):** This waveform also exhibits overshoot and undershoot. It rises to about 520 mV initially, then dips below 490 mV before stabilizing slightly below 500 mV after around 30 ns.

The waveforms indicate typical step response characteristics, such as overshoot, undershoot, and settling time, which are important for assessing the stability and performance of the amplifier. The graph suggests that the amplifier has a relatively fast response with some transient oscillations before reaching steady state.

Figure 11.46 (a) Closed-loop amplifier and (b) its step response.
image_name:Equivalent circuit of closed-loop amplifier
description:
[
name: R1, type: Resistor, value: 100k, ports: {N1: Vin, N2: InN}
name: R2, type: Resistor, value: 50k, ports: {N1: InN, N2: GND}
name: Cin, type: Capacitor, value: 50fF, ports: {Np: InN, Nn: GND}
name: CL, type: Capacitor, value: 1pF, ports: {Np: Vout, Nn: GND}
name: A1, type: OpAmp, value: Av, ports: {InP: GND, InN: InN, OutP: Vout}
]
extrainfo:The circuit is an equivalent circuit of a closed-loop amplifier. It includes a feedback network with resistors and capacitors for stability and performance enhancement. The op-amp is configured with negative feedback to stabilize the output voltage.

(a)
image_name:(b)
description:The graph in Figure 11.47 (b) is a time-domain waveform showing the step response of a closed-loop amplifier with a zero-resistance (Rz) of 1500 Ω. The x-axis represents time in nanoseconds (ns), ranging from 0 to 40 ns. The y-axis represents the output voltages, Vout1 and Vout2, in millivolts (mV), covering a range from 470 mV to 530 mV.

The graph displays two curves, one in black and the other in gray, indicating the voltages Vout1 and Vout2, respectively. The response begins at approximately 500 mV for both outputs. At the start of the graph (around 0 ns), there is a rapid rise in Vout1 to about 520 mV, while Vout2 drops to around 480 mV. This indicates a quick response to an input step.

Both outputs then stabilize, with Vout1 maintaining a level close to 520 mV and Vout2 around 480 mV until approximately 20 ns. At this point, there is a noticeable transition where Vout1 drops to slightly above 500 mV and Vout2 rises to just below 500 mV, indicating a settling phase in the amplifier's response.

The waveform stabilizes again after the transition, with Vout1 and Vout2 reaching approximately equal levels near 500 mV, maintaining this until the end of the observed time frame at 40 ns. The graph illustrates the amplifier's ability to quickly respond to changes and settle to a steady-state output with minimal overshoot and ringing, demonstrating its high-speed performance characteristics.

(b)

Figure 11.47 (a) Equivalent circuit of closed-loop amplifier and (b) step response with $R_{z}=1500 \Omega$.

## 11.6 ■ High-Speed Amplifier

Some applications require an amplifier with fast settling and accurate gain. For example, "pipelined" ADC architectures can tolerate but a small gain error in their constituent amplifiers. In this section, we design a differential amplifier according to the following specifications:

- Voltage gain $=4$
- Gain error $\leq 1 \%$
- Differential output swing $=1 \mathrm{~V}_{p p}$
- Load capacitance $=1 \mathrm{pF}$
- Step response settling time to $0.5 \%$ accuracy $=5 \mathrm{nS}$
- $V_{D D}=1 \mathrm{~V}$

As illustrated in Fig. 11.48, the settling time, $t_{s}$, is defined as the time necessary for the output to reach within $0.5 \%$ of its final value. Our objective is to minimize the power consumption of the circuit.
image_name:Amplifier
description:
[
name: Amplifier, type: OpAmp, value: Amplifier, ports: {InP: Vin1, InN: Vin2, OutP: Vout1, OutN: Vout2}
name: C1, type: Capacitor, value: 1 pF, ports: {Np: Vout1, Nn: GND}
name: C2, type: Capacitor, value: 1 pF, ports: {Np: Vout2, Nn: GND}
]
extrainfo:The amplifier is configured with a differential input (Vin1, Vin2) and differential output (Vout1, Vout2). The output is connected to capacitive loads of 1 pF each, grounded on one side. The diagram also illustrates the definition of settling time (ts) as the time required for the output to reach within 0.5% of its final value.
image_name:Vin1-Vin2 vs t
description:The graph labeled "Vin1-Vin2 vs t" is a time-domain waveform illustrating the differential input voltage \(V_{in1} - V_{in2}\) against time \(t\). The graph is divided into two sections:

1. **Input Voltage (Vin1-Vin2) vs Time:**
- **Axes:**
- The vertical axis represents the differential input voltage \(V_{in1} - V_{in2}\) in volts (V).
- The horizontal axis represents time \(t\) in seconds (s).
- **Behavior:**
- The input voltage is shown as a constant value over time, indicating a step input.
- The waveform is a horizontal line, suggesting that the input voltage remains constant.

2. **Output Voltage (Vout1-Vout2) vs Time:**
- **Axes:**
- The vertical axis represents the differential output voltage \(V_{out1} - V_{out2}\) in volts (V).
- The horizontal axis represents time \(t\) in seconds (s).
- **Overall Behavior and Trends:**
- The graph shows the output response to the step input.
- Initially, there is an overshoot beyond the final value \(V_F\), followed by oscillations that gradually settle.
- The waveform exhibits damped oscillations.
- **Key Features and Technical Details:**
- The overshoot exceeds the final value \(V_F\) by a certain percentage.
- The settling time \(t_s\) is marked, representing the time it takes for the output to remain within \(0.5\%\) of the final value \(V_F\).
- The output eventually stabilizes at \(V_F\) after the oscillations diminish.
- **Annotations:**
- The graph includes horizontal dashed lines indicating \(0.5\%\) above and below the final value \(V_F\), illustrating the settling accuracy requirement.
- The settling time \(t_s\) is explicitly marked on the time axis, showing the point where the output remains within the specified accuracy of the final value.
image_name:Vout1-Vout2 vs t
description:### Graph Description: Vout1-Vout2 vs t

1. **Type of Graph and Function:**
- The graph is a time-domain waveform depicting the differential output voltage (Vout1 - Vout2) of an amplifier over time.

2. **Axes Labels and Units:**
- **X-axis (Horizontal):** Represents time, labeled as 't'. The units are not explicitly mentioned but can be assumed to be in nanoseconds (nS) based on the context of the settling time.
- **Y-axis (Vertical):** Represents the differential output voltage (Vout1 - Vout2), labeled with the final voltage value as VF. The units are not explicitly mentioned but can be assumed to be in volts.

3. **Overall Behavior and Trends:**
- The waveform begins at zero and initially rises sharply, overshooting the final value (VF). It then oscillates, decreasing in amplitude over time.
- The waveform eventually settles within a band of ±0.5% of the final value (VF), indicating the settling time (t_s).

4. **Key Features and Technical Details:**
- **Initial Overshoot:** The waveform overshoots above the final value VF before oscillating.
- **Settling Time (t_s):** Marked on the graph, it is the time taken for the output to remain within 0.5% of the final value VF.
- **Oscillations:** The waveform shows damped oscillations, indicating a transient response typical in amplifier circuits.
- **Final Value (VF):** The target differential output voltage that the waveform approaches as it stabilizes.

5. **Annotations and Specific Data Points:**
- The graph includes annotations showing the ±0.5% VF range, indicating the precision requirement for settling time.
- The settling time (t_s) is explicitly marked, illustrating the time at which the waveform first stays within the desired precision range.
- The graph does not provide specific numerical values for the overshoot or the exact amplitude of oscillations, focusing instead on the settling behavior.

Figure 11.48 Definition of settling time.

### 11.6.1 General Considerations

Precision Issues With a myriad of amplifier topologies, where do we begin? In this case, the specifications readily narrow down our choices. The maximum tolerable gain error of $1 \%$ indicates a closed-loop configuration so that the gain can be defined as the ratio of two passive component values and remain relatively independent of PVT. We must therefore design an amplifier whose open-loop gain is high enough to yield a closed-loop gain error of less than $1 \%$. This observation along with the required output swing of $1 \mathrm{~V}_{p p}$ calls for a two-stage op amp.

We have now arrived at the feedback arrangement shown in Fig. 11.49, where the closed-loop gain is given by

$$
\begin{align*}
\frac{V_{\text {out }}}{V_{\text {in }}} & =-\frac{R_{2}}{R_{1}} \frac{1}{1+\left(1+\frac{R_{2}}{R_{1}}\right) \frac{1}{A_{0}}}  \tag{11.14}\\
& \approx-\frac{R_{2}}{R_{1}}\left[1-\left(1+\frac{R_{2}}{R_{1}}\right) \frac{1}{A_{0}}\right] \tag{11.15}
\end{align*}
$$

We choose $R_{2} / R_{1}=4$ and ensure that the gain error falls below $1 \%$ :

$$
\begin{equation*}
\left(1+\frac{R_{2}}{R_{1}}\right) \frac{1}{A_{0}} \leq 0.01 \tag{11.16}
\end{equation*}
$$

thereby obtaining $A_{0} \geq 500$. This calculation neglects the loading of the feedback network on the op amp.
image_name:Figure 11.49 Closed-loop amplifier with resistive feedback
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: Vip, N2: InP(Av)}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: InN(Av)}
name: R2, type: Resistor, value: R2, ports: {N1: InP(Av), N2: VoutN}
name: R2, type: Resistor, value: R2, ports: {N1: InN(Av), N2: VoutP}
name: CL, type: Capacitor, value: CL, ports: {Np: VoutN, Nn: GND}
name: CL, type: Capacitor, value: CL, ports: {Np: VoutP, Nn: GND}
name: Av, type: OpAmp, value: Av, ports: {InP: InP(Av), InN: InN(Av), OutP: VoutP, OutN: VoutN}
]
extrainfo:The circuit is a closed-loop amplifier with resistive feedback, utilizing an operational amplifier with feedback resistors R1 and R2. Capacitors CL are connected at the output for stabilization.

Figure 11.49 Closed-loop amplifier with resistive feedback.

#### Example 11.12

Determine the closed-loop output impedance and bandwidth of the above topology in terms of the open-loop op amp characteristics.

#### Solution

Drawing the half-circuit equivalent for loop gain calculation as shown in Fig. 11.50 and applying a test signal, $V_{t}$, we observe that the feedback network senses $V_{\text {out }}$ and returns a fraction equal to $\beta=\left[R_{1} /\left(R_{1}+R_{2}\right)\right] V_{\text {out }}$ to the input. The loop gain is therefore equal to $\beta A_{0}=A_{0} R_{1} /\left(R_{1}+R_{2}\right) \approx A_{0} / 5 \approx 100$, indicating that the output resistance falls by a factor of 100 as a result of feedback. The bandwidth rises by the same factor.
image_name:Figure 11.50
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: GND, N2: VF}
name: R2, type: Resistor, value: R2, ports: {N1: VF, N2: Vout}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: Vt, Nn: GND}
name: A0, type: OpAmp, value: A0, ports: {InP: Vt, InN: VF, Out: Vout}
]
extrainfo:This circuit is a feedback amplifier with resistive feedback network. The loop gain is given by βA0 = A0 R1 / (R1 + R2).

Figure 11.50

The use of a resistive feedback network poses a difficulty: as explained in Sec. 11.5.2, if $R_{1}$ and $R_{2}$ are large enough not to reduce the open-loop gain of the op amp, then they form a significant pole with the input capacitance, degrading the phase margin. We therefore consider capacitive feedback instead, configuring the circuit as shown in Fig. 11.51(a). The closed-loop gain is now approximately equal to $C_{1} / C_{2}$, or more accurately (Chapter 13):

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}} \approx-\frac{C_{1}}{C_{2}}\left(1-\frac{C_{1}+C_{2}+C_{\text {in }}}{C_{2}} \frac{1}{A_{0}}\right) \tag{11.17}
\end{equation*}
$$

where $C_{i n}$ denotes the (single-ended) input capacitance of the op amp. Drawing the single-ended counterpart for the loop transmission calculation [Fig. 11.51(b)], we observe that $C_{1}$ and $C_{2}$ do not contribute additional poles because $\left(C_{1}+C_{i n}\right) C_{2} /\left(C_{1}+C_{i n}+C_{2}\right.$ ) simply appears in parallel with $C_{L}$. (As explained in Chapter 13, the capacitors also allow sampling and discrete-time operation.)
image_name:(a)
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vip, Nn: X}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: Y}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Voutn}
name: C2, type: Capacitor, value: C2, ports: {Np: Y, Nn: Voutp}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
name: A0, type: OpAmp, value: A0, ports: {InP: X, InN: Y, OutP: Voutp, OutN: Voutn}
]
extrainfo:The circuit is a closed-loop amplifier using capacitive feedback. Capacitors C1 and C2 are used for feedback, and CL is the load capacitor. The op-amp A0 amplifies the differential input. The circuit does not exhibit a high-pass response due to the lack of a resistive path to nodes X and Y.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Cin, type: Capacitor, value: Cin, ports: {Np: X, Nn: GND}
name: VF, type: VoltageSource, value: VF, ports: {Np: X, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: X}
name: Vt, type: VoltageSource, value: Vt, ports: {Np: Vt, Nn: GND}
name: A0, type: OpAmp, value: A0, ports: {InP: X, InN: Vt, OutP: Vout}
name: C2, type: Capacitor, value: C2, ports: {Np: Vout, Nn: X}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit in Figure 11.51(b) is a simplified equivalent for loop gain calculation of a closed-loop amplifier using capacitive feedback. It includes an op-amp A0 with a feedback loop formed by capacitors C1 and C2. The input is provided by voltage sources Vin and Vt, and the output is taken across CL. The capacitors Cin and VF are used for additional filtering and feedback purposes.

Figure 11.51 (a) Closed-loop amplifier using capacitive feedback, and (b) its simplified equivalent for loop gain calculation.

Circuits incorporating capacitive "coupling" typically exhibit a high-pass response. Is that the case for the amplifier of Fig. 11.51(a)?

#### Solution

No, it is not. Since there is no resistive path to $X$ and $Y$, the time constant at these nodes is infinite (if leakage currents are neglected), yielding a frequency response that extends to nearly $f=0$. The reader can consider the frequency response of a simple capacitive divider as an example to appreciate this property.

The circuit of Fig. 11.51(a) provides no bias for the op amp inputs, i.e., the dc levels at $X$ and $Y$ are not defined and can assume any value. (In the presence of gate leakage at the inputs, these nodes charge to $V_{D D}$ or discharge to ground.) Illustrated in Fig. 11.52, a simple remedy is to add two feedback resistors so that the input and output dc levels become equal. However, the finite time constant at $X$ and $Y$ leads to a high-pass response; if $A_{0}=\infty$, then

$$
\begin{align*}
\frac{V_{\text {out }}}{V_{\text {in }}}(s) & =-\frac{R_{F} \| \frac{1}{C_{2} s}}{\frac{1}{C_{1} s}}  \tag{11.18}\\
& =-\frac{R_{F} C_{1} s}{R_{F} C_{2} s+1} \tag{11.19}
\end{align*}
$$

image_name:Figure 11.52 (a)
description:
[
name: RF, type: Resistor, value: RF, ports: {N1: X, N2: Voutn}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Voutn}
name: C1, type: Capacitor, value: C1, ports: {Np: Vip, Nn: X}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: Y}
name: C2, type: Capacitor, value: C2, ports: {Np: Y, Nn: Voutp}
name: RF, type: Resistor, value: RF, ports: {N1: Y, N2: Voutp}
name: A0, type: OpAmp, value: A0, ports: {InP: X, InN: Y, OutP: Voutp, OutN: Voutn}
]
extrainfo:The circuit is a differential amplifier with feedback resistors RF and capacitors C1 and C2. The op-amp A0 has differential inputs X and Y, and differential outputs Voutp and Voutn. The feedback network sets the input and output DC levels equal, resulting in a high-pass filter response.

(a)
image_name:(b)
description:The graph is a Bode plot illustrating the magnitude response of a high-pass filter created by a differential amplifier circuit with feedback resistors and capacitors. The horizontal axis represents angular frequency \( \omega \), and the vertical axis represents the gain \( \frac{V_{out}}{V_{in}} \). The units for the axes are not explicitly labeled but are typically in radians per second for frequency and a dimensionless ratio for gain.

Overall Behavior and Trends:
- The graph shows a low-pass to high-pass transition characteristic of a high-pass filter.
- At low frequencies, the gain is close to zero, indicating that low-frequency signals are attenuated.
- As the frequency increases, the gain rises sharply, indicating the passband of the filter.
- Beyond a certain frequency, the gain stabilizes and becomes constant, indicating the filter's passband.

Key Features and Technical Details:
- The corner frequency, marked on the graph, is \( \frac{1}{R_F C_2} \). This is the frequency at which the gain begins to rise sharply from the low-frequency attenuation level.
- The graph indicates that the corner frequency is crucial for determining the filter's response, and it must be chosen appropriately relative to the minimum input frequency of interest.
- The slope of the rising portion of the graph represents the rate at which the gain increases with frequency, typically 20 dB/decade for a first-order high-pass filter.

Annotations and Specific Data Points:
- A dashed vertical line marks the corner frequency \( \frac{1}{R_F C_2} \), highlighting its significance in the circuit's frequency response.
- There are no additional annotations or specific numerical values provided on the graph, but the corner frequency is the primary point of interest.

This graph effectively demonstrates how the differential amplifier with feedback components acts as a high-pass filter, allowing signals above a certain frequency to pass while attenuating lower frequencies.

(b)

Figure 11.52 Addition of feedback resistors to define input dc levels and the resulting transfer function.
The corner frequency, $1 /\left(2 \pi R_{F} C_{2}\right)$, must therefore be chosen less than the minimum input frequency of interest, a condition that is not practical in all applications. As explained in Chapter $13, R_{F}$ can be replaced with a switch, but we proceed here assuming that $R_{F} C_{2}$ is sufficiently large. In other words, we assume that the circuit reduces to that in Fig. 11.51(a) for the frequencies of interest.

Equation (11.17) indicates that the capacitive-feedback amplifier's gain error also depends on $C_{i n}$. For example, if $C_{i n} \approx\left(C_{1}+C_{2}\right) / 5$, then $A_{0}$ must be $20 \%$ higher than the value dictated by Eq. (11.16). We can choose $C_{1}+C_{2} \gg C_{i n}$, but at the cost of settling speed.

Speed Issues The amplifier must settle to $0.5 \%$ accuracy in 5 ns . Let us first assume a linear, first-order circuit and write the step response as

$$
\begin{equation*}
V_{\text {out }}(t)=V_{0}\left(1-\exp \frac{-t}{\tau}\right) u(t) \tag{11.20}
\end{equation*}
$$

The time necessary for $V_{\text {out }}$ to reach $0.995 V_{0}$ is $t_{s}=-\tau \ln 0.005=5.3 \tau$; i.e., $\tau$ must be no more than 0.94 ns . Thus, the closed-loop amplifier must achieve a $-3-\mathrm{dB}$ bandwidth of at least $1 /(2 \pi \times 0.94 \mathrm{~ns}) \approx$ 170 MHz .

If the op amp in Fig. 11.51(a) is modeled simply by a dependent current source, $G_{m} V_{i n}$, and an output resistance, $R_{\text {out }}$, then the closed-loop time constant is given by (Chapter 13)

$$
\begin{equation*}
\tau=\frac{C_{L}\left(C_{1}+C_{i n}\right)+C_{L} C_{2}+C_{2}\left(C_{1}+C_{i n}\right)}{G_{m} C_{2}} \tag{11.21}
\end{equation*}
$$

where $G_{m} R_{\text {out }}$ is assumed much greater than unity. This expression can be rewritten as

$$
\begin{equation*}
\tau=\left(\frac{C_{1}+C_{2}+C_{i n}}{C_{2}}\right) \frac{C_{L}+\frac{C_{2}\left(C_{i n}+C_{1}\right)}{C_{2}+C_{i n}+C_{1}}}{G_{m}} \tag{11.22}
\end{equation*}
$$

suggesting that the op amp sees the series combination of $C_{2}$ and $C_{1}+C_{i n}$ in parallel with $C_{L}$, and its $G_{m}$ is reduced by the feedback factor, $C_{2} /\left(C_{1}+C_{2}+C_{i n}\right)$ (Fig. 11.53) (Chapter 13).
image_name:Figure 11.53
description:
[
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: X}
name: Cin, type: Capacitor, value: Cin, ports: {Np: X, Nn: GND}
name: Gm, type: OpAmp, value: Gm, ports: {InP: GND, InN: X, Out: Vout}
name: C2, type: Capacitor, value: C2, ports: {Np: X, Nn: Vout}
name: CL, type: Capacitor, value: CL, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit represents a closed-loop time constant model with an equivalent network for a frequency-compensated two-stage op amp. It shows the series combination of C2 and C1+Cin in parallel with CL. The feedback factor is given by C2/(C1+C2+Cin), affecting the transconductance Gm.

Figure 11.53 Representation of closed-loop time constant by an equivalent network.
The foregoing model is not accurate for a two-stage op amp because the internal pole (at the output of the first stage) inevitably affects the response. Let us improve our approximation by considering a frequency-compensated two-stage op amp. Recall that if the loop gain falls to 1 at the second pole, $\omega_{p 2}$, the phase margin is about $45^{\circ}$ for unity-gain feedback.

How do we compensate the op amp for a closed-loop gain of 4 (rather than 1)? In this case, $|\beta H|$ (rather than $|H|$ ) must fall to 0 dB at $\omega_{p 2}$ (i.e., the circuit is not compensated for unity-gain feedback). As illustrated in Fig. 11.54(a), we begin at $\omega=\omega_{p 2}$ and draw a line with a slope of $-20 \mathrm{~dB} /$ decade toward the $y$-axis, seeking its intercept with the plot of $|\beta H|$. We calculate the location of the compensated dominant pole, $\omega_{p 1}^{\prime}$, as follows. Between $\omega_{p 1}^{\prime}$ and $\omega_{p 2}$, we can approximate the compensated $\beta H(s)$ as $\beta A_{0} /\left(1+s / \omega_{p 1}^{\prime}\right)$; we set its magnitude to 1 at $\omega_{p 2}:\left|\beta A_{0} /\left(1+j \omega_{p 2} / \omega_{p 1}^{\prime}\right)\right|=1$. It follows that

$$
\begin{equation*}
\omega_{p 1}^{\prime} \approx \sqrt{\frac{\omega_{p 2}^{2}}{\beta^{2} A_{0}^{2}-1}} \tag{11.23}
\end{equation*}
$$

image_name:Figure 11.54 (a)
description:**Figure 11.54 (a): Frequency Compensation for Loop Gain of \( \beta A_0 \)**

1. **Type of Graph and Function:**
- The graph is a Bode plot representing the magnitude of the loop gain \( |\beta H(\omega)| \) on a logarithmic scale.

2. **Axes Labels and Units:**
- The vertical axis represents \( |\beta H(\omega)| \) on a logarithmic scale.
- The horizontal axis represents frequency \( \omega \) also on a logarithmic scale.
- Significant markers include \( \omega_{p1} \) and \( \omega_{p2} \).

3. **Overall Behavior and Trends:**
- The plot shows two curves: one for \( \beta = 1 \) and another for \( \beta < 1 \).
- For \( \beta = 1 \), the magnitude remains constant at \( A_0 \) until \( \omega_{p1} \), then decreases.
- For \( \beta < 1 \), the curve starts at \( \beta A_0 \), decreases at \( \omega_{p1} \), and continues to decrease past \( \omega_{p2} \).

4. **Key Features and Technical Details:**
- The graph highlights the effect of feedback strength on the loop gain.
- For \( \beta = 1 \), the transition occurs at \( \omega_{p1} \).
- For \( \beta < 1 \), the transition is smoother and spans from \( \omega_{p1} \) to \( \omega_{p2} \).

5. **Annotations and Specific Data Points:**
- The graph includes annotations for \( \beta = 1 \) and \( \beta < 1 \), showing the different behaviors in loop gain.
- The points \( \omega_{p1} \) and \( \omega_{p2} \) are marked to indicate where significant changes occur in the loop gain behavior.
image_name:Figure 11.54 (b)
description:The graph in Figure 11.54 (b) is a Bode plot representing the frequency response of a closed-loop system after compensation. It is plotted on a logarithmic scale for both the magnitude |H(ω)| and the frequency ω.

**Axes Labels and Units:**
- The vertical axis represents the magnitude of the transfer function |H(ω)| in decibels (dB) on a logarithmic scale.
- The horizontal axis represents the frequency ω on a logarithmic scale.

**Overall Behavior and Trends:**
- The plot shows a typical frequency response of a compensated system.
- Initially, the magnitude is constant at A₀ until the first pole frequency ωₚ₁ is reached.
- After ωₚ₁, the magnitude begins to decrease linearly on the logarithmic scale, indicating a reduction in gain.
- The closed-loop response is shown as a horizontal line at a lower magnitude level, A₀/(1 + βA₀), until it reaches the second pole frequency ωₚ₂.
- Beyond ωₚ₂, the magnitude decreases further, following the compensated response.

**Key Features and Technical Details:**
- The plot features two critical frequencies: ωₚ₁ and ωₚ₂, marked with vertical dashed lines.
- The uncompensated magnitude starts at A₀ and decreases after ωₚ₁.
- The closed-loop response is flat between 0 dB and ωₚ₂, showing effective compensation.
- The gain crossover frequency, where the magnitude reaches 0 dB, is not explicitly marked but implied by the trend.

**Annotations and Specific Data Points:**
- The graph includes annotations indicating the 'After Compensation' and 'Closed-Loop Response' regions.
- The initial magnitude level is A₀, and the compensated level is A₀/(1 + βA₀), clearly marked on the graph.
- The transition points at ωₚ₁ and ωₚ₂ are highlighted with circles on the frequency axis.

Figure 11.54 (a) Frequency compensation for loop gain of $\beta A_{0}$, and (b) the resulting closed-loop response.
and

$$
\begin{equation*}
\omega_{p 1}^{\prime} \approx \frac{\omega_{p 2}}{\beta A_{0}} \tag{11.24}
\end{equation*}
$$

As expected, $\omega_{p 1}^{\prime}$ must be chosen lower in magnitude if $\beta$ increases, i.e., if the feedback becomes stronger.

#### Example 11.14

We compensate an op amp for $\beta=1 / 5$ and $\mathrm{PM}=45^{\circ}$. Plot the open-loop frequency response of the op amp, $H$.

#### Solution

On a logarithmic scale, the plot of $H$ is obtained if we shift the plot of $|\beta H|$ up by $-20 \log \beta$. As shown in Fig. 11.55, $H$ begins to fall at $\omega_{p 1}^{\prime}$ and reaches a value of approximately $1 / \beta$ at $\omega_{p 2}$.
image_name:Figure 11.55
description:The graph in Figure 11.55 is a Bode plot, which is used to represent the frequency response of a system. It specifically shows the open-loop gain of an operational amplifier (op amp). The plot is on a logarithmic scale, with the x-axis representing the logarithm of frequency (log ω) and the y-axis representing gain in decibels (dB).

**Axes Labels and Units:**
- **X-axis:** Logarithm of frequency (log ω)
- **Y-axis:** Gain in decibels (dB)

**Overall Behavior and Trends:**
- The graph begins at a high gain level labeled as \( A_0 \) at low frequencies.
- As frequency increases, the gain starts to decrease linearly on the log-log scale.
- The slope of the gain decreases initially at point \( \omega_{p1} \) and continues to drop until it reaches another critical point \( \omega_{p2} \).

**Key Features and Technical Details:**
- The plot shows two critical frequencies, \( \omega_{p1} \) and \( \omega_{p2} \).
- At \( \omega_{p1} \), the gain begins to roll off from the initial level \( A_0 \) and intersects with the line representing \( \beta A_0 \).
- The gain continues to decrease and reaches a level of \( 1/\beta \) at \( \omega_{p2} \).
- The dashed line represents the compensated loop transmission \( |\beta H| \), which is lower in magnitude compared to the open-loop gain \( |H(ω)| \).

**Annotations and Specific Data Points:**
- The graph is annotated with the gain levels \( A_0 \), \( \beta A_0 \), and \( 1/\beta \).
- \( \omega_{p1} \) and \( \omega_{p2} \) are marked as critical frequencies where significant changes in the slope occur.
- The plot shows the typical behavior of an op amp's frequency response with feedback compensation, highlighting how the gain decreases with increasing frequency.

Figure 11.55

Let us now construct the closed-loop frequency response with this choice of $\omega_{p 1}^{\prime}$. To this end, we first plot the magnitude of the loop transmission, $|\beta H|$, for $\beta=1$ and after compensation [Fig. 11.54(b)]. The closed-loop response begins at $A_{0} /\left(1+\beta A_{0}\right)$ at low frequencies and begins to roll off at $\omega \approx \omega_{p 2}$. From another perspective, since the ratio of the open-loop and closed-loop gains at $\omega_{p 1}^{\prime}$ is approximately equal to $\beta A_{0}$ and since the open-loop gain falls at $20 \mathrm{~dB} / \mathrm{dec}$ (i.e., in proportion to $\omega$ ), the two responses intersect at $\omega \approx \beta A_{0} \omega_{p 1}^{\prime} \approx \omega_{p 2}$. We therefore choose this bandwidth equal to $2 \pi(170 \mathrm{MHz}) / 125=2 \pi(1.36 \mathrm{MHz})$.

In summary, the closed-loop gain and settling speed requirements have translated to a dominant pole at 1.36 MHz and a second pole at 170 MHz . The open-loop gain must fall from 500 at low frequencies to 4 at the second pole. These values assume a phase margin of $45^{\circ}$ and must be eventually revisited.

### 11.6.2 Op Amp Design

Based on the foregoing calculations, we seek a two-stage op amp with an open-loop gain of 500, a dominant pole at 1.36 MHz , a second pole at 170 MHz , and a differential output swing of $1 \mathrm{~V}_{p p}$. We thus return to the prototype designed in Sec. 11.5.2 and see whether it can serve our purpose. Most of the specifications of that op amp are the same as those needed here. But, since the compensation can be relaxed to suit a feedback factor of $1 / 5$, the dominant pole of the op amp need not be as low as 344 kHz . Equation (11.24) suggests that, if the feedback factor is reduced from 1 to $\beta$, then the dominant pole can increase by roughly a factor of $1 / \beta$. We therefore expect that the compensation capacitor leading to the response in Fig. 11.45(a) can be lowered from 4.5 pF to 0.9 pF , raising the dominant pole frequency from 340 kHz to 1.7 MHz . For the feedforward zero to cancel the second pole, $R_{2}$ must rise by the same factor, reaching $950 \Omega$.

As observed in Sec. 11.5.2, the zero-pole cancellation creates a greater phase margin, allowing us to reduce $C_{C}$ from 4.5 pF to 0.8 pF . However, in the present design, the feedback network capacitors also
load the output stage, lowering the nondominant pole, $\omega_{p 2}$. Since this effect has not been included in our calculations, we resist the temptation to reduce $C_{C}$ for now and proceed to study the closed-loop behavior.

### 11.6.3 Closed-Loop Small-Signal Performance

Figure 11.56 shows the overall op amp and its closed-loop environment. For a nominal gain of 4 , we choose $C_{1}=1 \mathrm{pF}$ and $C_{2}=0.25 \mathrm{pF}$. With $C_{i n} \approx 50 \mathrm{fF}$, Eq. (11.17) predicts a gain error of less than $1 \%$ if $A_{0}>520$. This gain is slightly greater than that achieved by the op amp at its peak output swings (Fig. 11.41), but we deal with this issue later. For transient studies, $R_{F}$ must be large enough not to cause significant "droop" during time scales of interest. Specifically, for a settling time of 5 ns , we select $R_{F} C_{2}>10 \mu \mathrm{~s}$ so as to confine the discharge of the capacitors to well below $1 \%$; i.e., $R_{F}=40 \mathrm{M} \Omega$. (This extremely large value implies that a switched-capacitor solution is more practical.)
image_name:Figure 11.56
description:
[
name: M1, type: NMOS, ports: {S: GND, D: n, G: Vb1}
name: M2, type: NMOS, ports: {S: n, D: Y, G: Vb2}
name: M3, type: NMOS, ports: {S: Y, D: X, G: Vb1}
name: M4, type: NMOS, ports: {S: X, D: Vout1, G: Vb2}
name: M5, type: PMOS, ports: {S: VDD, D: X, G: Vb3}
name: M6, type: PMOS, ports: {S: VDD, D: Y, G: Vb2}
name: M7, type: PMOS, ports: {S: VDD, D: X, G: Vb3}
name: M8, type: PMOS, ports: {S: VDD, D: Y, G: Vb2}
name: M9, type: PMOS, ports: {S: VDD, D: Vout1, G: Vb3}
name: M10, type: PMOS, ports: {S: VDD, D: Vout2, G: Vb3}
name: M11, type: NMOS, ports: {S: GND, D: Vout1, G: Vout1}
name: M12, type: NMOS, ports: {S: GND, D: Vout2, G: Vout2}
name: Rz, type: Resistor, ports: {N1: Vout1, N2: X}
name: Cc, type: Capacitor, ports: {Np: X, Nn: Vout1}
name: Vb1, type: VoltageSource, ports: {Np: Vb1, Nn: GND}
name: Vb2, type: VoltageSource, ports: {Np: Vb2, Nn: GND}
name: Vb3, type: VoltageSource, ports: {Np: Vb3, Nn: GND}
name: VDD, type: VoltageSource, ports: {Np: VDD, Nn: GND}
name: 20 µA, type: CurrentSource, ports: {Np: n, Nn: GND}
name: 950 Ω, type: Resistor, ports: {N1: Y, N2: Vout2}
name: 0.9 pF, type: Capacitor, ports: {Np: Y, Nn: Vout2}
name: 20 kΩ, type: Resistor, ports: {N1: Vout2, N2: GND}
name: 10 Ω, type: Resistor, ports: {N1: GND, N2: GND}
name: 0.16 µm, type: Resistor, ports: {N1: GND, N2: GND}
name: A0, type: OpAmp, ports: {InP: Vin, InN: Voutn, OutP: Voutp, OutN: Voutn}
name: RF, type: Resistor, ports: {N1: Voutp, N2: Vout}
name: C1, type: Capacitor, value: 1 pF, ports: {Np: Vin, Nn: InP(A0)}
name: C2, type: Capacitor, ports: {Np: Voutp, Nn: Voutn}
]
extrainfo:The circuit is a two-stage op-amp with compensation capacitors and resistors for stability. It includes biasing voltages and a feedback network. The op-amp is configured for differential input and output.
image_name:Figure 11.57
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vb1}
name: M2, type: NMOS, ports: {S: GND, D: Y, G: X}
name: M3, type: NMOS, ports: {S: X, D: VDD, G: Vb1}
name: M4, type: NMOS, ports: {S: Y, D: VDD, G: Vb2}
name: M5, type: NMOS, ports: {S: VDD, D: X, G: Vb3}
name: M6, type: NMOS, ports: {S: VDD, D: Y, G: Vb2}
name: M7, type: PMOS, ports: {S: VDD, D: X, G: Vb3}
name: M8, type: PMOS, ports: {S: VDD, D: Y, G: Vb2}
name: M9, type: PMOS, ports: {S: VDD, D: Vout1, G: Vb3}
name: M10, type: PMOS, ports: {S: VDD, D: Vout2, G: Vb2}
name: M11, type: NMOS, ports: {S: GND, D: Vout1, G: X}
name: M12, type: NMOS, ports: {S: GND, D: Vout2, G: Y}
name: Rz, type: Resistor, ports: {N1: Vout1, N2: X}
name: Cc, type: Capacitor, ports: {Np: X, Nn: Vout1}
name: 20, type: Resistor, value: 20 kΩ, ports: {N1: Y, N2: Vout2}
name: 950, type: Resistor, value: 950 Ω, ports: {N1: Y, N2: Vout2}
name: 0.9, type: Capacitor, value: 0.9 pF, ports: {Np: Y, Nn: Vout2}
name: 10, type: Resistor, value: 10 Ω, ports: {N1: Y, N2: Vout2}
name: 0.16, type: Capacitor, value: 0.16 μm, ports: {Np: Y, Nn: Vout2}
name: 20, type: CurrentSource, value: 20 μA, ports: {Np: VDD, Nn: GND}
name: RF, type: Resistor, ports: {N1: Vout, N2: Vout2}
name: C1, type: Capacitor, value: 1 pF, ports: {Np: Vin, Nn: InP(A0)}
name: C2, type: Capacitor, ports: {Np: Vout, Nn: Vout2}
name: A0, type: OpAmp, ports: {InP: InP(A0), InN: InN(A0), OutP: Vout, OutN: Vout2}
]
extrainfo:The circuit is a two-stage op-amp with compensation and feedback, designed for high gain and stability. It includes multiple NMOS and PMOS transistors, resistors, capacitors, and an operational amplifier. The design aims to achieve a specific output with minimal gain error, as indicated by the precise component values and feedback configuration.

Figure 11.56 Overall compensated two-stage op amp and the closed-loop environment.
Let us apply a small step to the above circuit and examine the output behavior. With a differential input step of 25 mV , we expect an output around 99 mV (for $1 \%$ gain error). Depicted in Fig. 11.57(a) is the differential output waveform and in Fig. 11.57(b) a close-up showing the fine settling. We observe a final value equal to 98.82 mV , a result of insufficient open-loop gain.

How do we increase the gain? If we raise the length (and hence the width) of the first-stage input transistors in Fig. 11.56, $C_{\text {in }}$ also increases, counteracting $A_{0}$ in Eq. (11.17). Instead, we double the (drawn) width and length of the NMOS cascode transistors, obtaining the output shown in Fig. 11.58. Now, the gain error is less than $1 \%$.

#### Example 11.15

Is it possible to increase the length of the PMOS devices in the first stage to raise the gain?

#### Solution

Designed to provide a much higher impedance than its NMOS counterpart, the PMOS cascode structures have a weak effect on the gain of the first stage. The NMOS cascode devices, on the other hand, directly determine the voltage gain (why?).

Let us turn our attention to the settling behavior of the amplifier. If the output reaches 99.1 mV at $t=\infty$, how do we define the settling time to $1 \%$ precision? We must find the time at which
image_name:(a)
description:The graph labeled "(a)" is a time-domain waveform depicting the closed-loop step response of an amplifier circuit. The x-axis represents time in nanoseconds (ns), ranging from 0 to 40 ns. The y-axis represents the voltage difference between two output nodes, \( V_{\text{out1}} - V_{\text{out2}} \), in millivolts (mV), ranging from -20 to 120 mV.

Overall Behavior and Trends:
- The waveform exhibits a rapid rise from approximately 0 mV to a peak just above 100 mV within the first 10 ns. This indicates the initial response of the amplifier to a step input.
- Following the peak, the waveform stabilizes around 100 mV, indicating the steady-state response of the amplifier.
- At around 20 ns, there is a sharp decline in voltage, dropping back to near 0 mV, which may indicate a reset or a different phase of the input signal.

Key Features and Technical Details:
- The initial rise is indicative of the amplifier's fast response time, crucial for high-speed applications.
- The stabilization around 100 mV suggests a stable steady-state output after the initial transient response.
- The sharp decline at 20 ns suggests a significant event or input change, possibly a step-down or a reset signal.

Annotations and Specific Data Points:
- The waveform reaches approximately 100 mV, which is an important reference for the amplifier's output level.
- The quick settling time to the steady-state value demonstrates the efficiency of the amplifier in reaching the desired output level quickly.
image_name:(b)
description:The graph labeled (b) is a time-domain waveform showing the closed-loop step response of an amplifier, focusing on the settling behavior to 1% accuracy. The x-axis represents time in nanoseconds (ns), ranging from 0 to 20 ns. The y-axis represents the output voltage difference (V_out1 - V_out2) in millivolts (mV), ranging from 97 mV to 99 mV.

The waveform exhibits an exponential rise from approximately 97 mV, rapidly approaching a steady-state value near 99.1 mV. The curve starts at about 97 mV at 0 ns and rises sharply, indicating a fast response, and begins to level off around 10 ns. The graph is focused on the region where the voltage settles to within 1% of the final value, approximately 99.1 mV.

Key features of the graph include the rapid initial rise and the subsequent leveling off as the output voltage approaches its final value. The settling time is defined as the time taken for the output to remain within 1% of the final value, which is approximately 99.1 mV ± 1 mV. The curve does not show any overshoot or oscillations, indicating a smooth settling behavior without ringing.

Figure 11.57 (a) Closed-loop step response and (b) close-up showing settling to $1 \%$ accuracy.
image_name:Figure 11.57 (a)
description:The graph in Figure 11.57 (a) is a time-domain waveform representing the closed-loop step response of a system. The x-axis is labeled 'Time (ns)' and measures time in nanoseconds, while the y-axis is labeled 'V_{out1} - V_{out2} (mV)' and measures the voltage difference in millivolts.

Overall Behavior and Trends:
The graph shows a rapid initial rise in voltage, starting from 0 mV at time 0 ns and quickly approaching a plateau around 99 mV. This indicates a swift response to a step input without any overshoot or oscillations, suggesting an overdamped system. The curve levels off smoothly, maintaining a steady state close to 99.1 mV.

Key Features and Technical Details:
- **Initial Rise:** The voltage rises steeply from 0 mV, reaching approximately 99 mV in a short time span.
- **Settling Time:** The system reaches a steady state within 1% of the final value (99.1 mV ± 1 mV) without any noticeable overshoot.
- **Steady State:** The voltage stabilizes at around 99 mV, indicating the final steady-state value.
- **Absence of Oscillations:** The graph does not exhibit any overshoot or ringing, confirming a smooth settling behavior.

Annotations and Specific Data Points:
- The graph does not have specific markers or annotations, but it clearly illustrates the system's settling behavior within the specified accuracy of 1%.
- The settling time is approximately 5.8 ns, as deduced from the context, though not directly marked on this graph.

In summary, the graph depicts a smooth and rapid response to a step input, with the system quickly reaching and maintaining a steady-state voltage level around 99 mV without overshoot or oscillations, indicative of an overdamped response.
image_name:Figure 11.57 (b)
description:The graph in Figure 11.57 (b) is a time-domain waveform illustrating the closed-loop step response of a system. The x-axis represents time in nanoseconds (ns), ranging from 0 to 20 ns, while the y-axis indicates the output voltage difference \( V_{\text{out1}} - V_{\text{out2}} \) in millivolts (mV), spanning from 97.5 mV to 99.5 mV.

**Overall Behavior and Trends:**
The graph shows a smooth, rising curve that approaches a final steady-state value. Initially, the voltage rises rapidly from approximately 97.5 mV, then gradually levels off as it nears the final value of about 99.1 mV. This behavior is indicative of a system that is settling to its final value without overshoot or oscillations, displaying a critically damped response.

**Key Features and Technical Details:**
- **Settling Time:** The time taken for the output to stay within 1% of the final value (99.1 mV ± 1 mV) is approximately 5.8 ns.
- **No Overshoot:** The curve does not exceed the final value, indicating no overshoot.
- **Smooth Transition:** The absence of oscillations or ringing suggests a well-damped system response.

**Annotations and Specific Data Points:**
There are no specific annotations or markers on the graph, but the smooth curve and the clear settling to within 1% accuracy are key observations. The final steady-state value is approximately 99.1 mV, as noted in the context.

Figure 11.58 (a) Closed-loop step response and (b) close-up showing settling to $1 \%$ accuracy for $(W / L)_{3,4}=180 \mu \mathrm{~m} / 0.16 \mu \mathrm{~m}$.
$V_{\text {out }}=99.1 \mathrm{mV} \pm 0.01 \times 99.1 \mathrm{mV} \approx 99.1 \mathrm{mV} \pm 1 \mathrm{mV}$. From the waveform in Fig. 11.58(b), we obtain $t_{s} \approx 5.8$ ns.

In order to improve the amplifier's speed, we recognize from Fig. 11.58(a) that the circuit is "overcompensated," i.e., the output appears overdamped. We can therefore return to our choice of $C_{C}$ and $R_{z}$ and adjust them more aggressively. We adjust these two values, patiently explore the design space, and examine the trends in the output behavior. With $C_{C}=0.3 \mathrm{pF}$ and $R_{z}=700 \Omega$, we observe the settling shown in Fig. 11.59. The settling time drops to 800 ps , a remarkable improvement. Note that $R_{z}$ is reduced in this case, thus moving the zero to higher frequencies.

### 11.6.4 Op Amp Scaling

If the settling time is so much shorter than the required value, can we trade speed for power dissipation? As explained in Chapter 9, a straightforward approach is to perform "linear scaling." We begin with the
image_name:(a)
description:The graph in Figure 11.59(a) is a time-domain waveform showing the closed-loop step response of an operational amplifier circuit. The x-axis represents time in nanoseconds (ns), ranging from 0 to 40 ns. The y-axis represents the voltage difference between two output nodes, \( V_{\text{out1}} - V_{\text{out2}} \), measured in millivolts (mV), ranging from -20 mV to 120 mV.

**Overall Behavior and Trends:**
- The waveform starts at approximately 100 mV and remains steady for a short duration.
- At around 20 ns, there is a sharp drop in voltage, indicating a step change.
- Following the step change, the waveform stabilizes near 0 mV, indicating the settling of the output.

**Key Features and Technical Details:**
- The initial voltage level is around 100 mV.
- The waveform exhibits a sharp transition at 20 ns, which is characteristic of a step response.
- The settling time is notably quick, aligning with the context description of an 800 ps settling time.

**Annotations and Specific Data Points:**
- The graph is not explicitly annotated with specific markers or reference lines, but the transition and settling regions are clearly visible.
- The waveform stabilizes to within 1% accuracy of 0 mV after the step change, as shown in the close-up view in Figure 11.59(b).
image_name:(b)
description:The graph labeled "(b)" is a time-domain waveform illustrating the settling behavior of an operational amplifier circuit. The x-axis represents time in nanoseconds (ns), ranging from 0 to 20 ns, while the y-axis shows the voltage difference between two outputs, V_out1 and V_out2, measured in millivolts (mV), ranging from 97.5 mV to 99.5 mV.

The waveform begins at approximately 97.5 mV and quickly rises, showing a small overshoot slightly above 99 mV within the first few nanoseconds. Following this overshoot, the waveform settles down to around 99 mV. The settling is characterized by a slight oscillation before stabilizing, indicating a rapid settling time with minor ringing. The graph zooms in on this settling behavior to demonstrate the accuracy to within 1% of the final value.

Overall, the graph highlights the fast settling response of the circuit, with a focus on the precision of the final voltage level achieved after an initial transient response.

Figure 11.59 (a) Closed-loop step response and (b) close-up showing settling to $1 \%$ accuracy.
response shown in Fig. 11.60(a) and scale down all transistor widths and bias currents by a factor of $\alpha$, thereby reducing the power by the same factor while retaining the voltage gain and the headroom. But how about $C_{C}$ and $R_{z}$ ? We make four observations. (1) With the load capacitance fixed, the output pole (before compensation) is scaled down by a factor of $\alpha$ [Fig. 11.60(b)] because the output resistance of the second stage is scaled up by this factor (why?). (2) To maintain the same phase margin, the dominant
image_name:(a)
description:The graph in Figure 11.60 (a) is a Bode plot, which is commonly used to analyze the frequency response of a system, in this case, an operational amplifier (op-amp). The plot is presented on a logarithmic scale for frequency (x-axis) and magnitude (y-axis). The y-axis represents the magnitude of the transfer function |βH(ω)| in decibels (dB), while the x-axis represents the frequency (ω) on a logarithmic scale.

Axes Labels and Units:
- **Y-Axis:** |βH(ω)| (log scale), measured in decibels (dB).
- **X-Axis:** Frequency (ω), presented on a logarithmic scale.

Overall Behavior and Trends:
The graph shows the response of the original op-amp design and the compensation applied for a feedback factor β less than 1. The original design is represented by a dashed line, starting at a high gain level A0 and decreasing at certain frequencies. The compensated response is shown with a solid line, indicating the adjustments made to maintain stability and performance under feedback conditions.

Key Features and Technical Details:
- **Initial Gain:** The original design starts at a gain level of A0, while the compensated design starts at βA0.
- **Poles:** The graph indicates two poles at frequencies ωp1 and ωp2 for the original design. These are critical frequencies where the gain begins to decrease.
- **Compensation:** The compensation for β < 1 is shown by the change in slope and position of the curves. The compensation aims to adjust the pole positions and maintain a stable phase margin.
- **Frequency Points:**
- **ωp1:** The first pole frequency where the gain begins to drop.
- **ωp2:** The second pole frequency, further reducing the gain.

Annotations and Specific Data Points:
- The plot includes annotations for the original design and compensation, indicating how the response changes with feedback.
- Reference lines are drawn to show the gain levels A0 and βA0, and the critical frequencies ωp1 and ωp2 are marked with open circles on the frequency axis.

This Bode plot provides a clear visualization of how frequency compensation affects the op-amp's response, ensuring stability and desired performance even when feedback is applied.
image_name:(b)
description:The graph labeled (b) is a Bode plot that represents the frequency response of an operational amplifier (op-amp) circuit, specifically focusing on the magnitude response. The graph is plotted on a logarithmic scale for frequency (x-axis) and a logarithmic scale for gain magnitude (y-axis), denoted as |βH(ω)|.

Axes Labels and Units:
- **X-axis:** Labeled as 'log ω', representing the logarithm of angular frequency.
- **Y-axis:** Labeled as '|βH(ω)| (log scale)', representing the magnitude of the transfer function in decibels (dB).

Overall Behavior and Trends:
- The original design is shown as a dashed line, while the scaled design is depicted as a solid line.
- The original design starts with a flat gain at A₀, which then decreases after the first pole ωₚ₁, and continues to decrease after the second pole ωₚ₂.
- In the scaled design, the frequency response is adjusted such that the second pole is shifted to ωₚ₂/α, indicating a reduction in frequency by a factor of α.

Key Features and Technical Details:
- **Poles:**
- **ωₚ₁:** The first pole remains unchanged in both designs.
- **ωₚ₂:** In the original design, the second pole is at ωₚ₂. In the scaled design, it is shifted to ωₚ₂/α.
- **Gain Levels:**
- The maximum gain level is A₀ in both designs.
- The scaled design maintains the same initial gain level but compensates for the shift in poles.

Annotations and Specific Data Points:
- The plot includes annotations for the original and scaled designs, clearly indicating the shift in the second pole frequency.
- The dashed line represents the original frequency response, while the solid line shows the modified response after scaling the design by α.

This graph illustrates how the frequency response of an op-amp can be adjusted by scaling the design parameters, specifically showing the impact on pole frequencies and gain behavior.
image_name:(c)
description:The graph in Figure 11.60(c) is a Bode plot, which represents the magnitude of the frequency response of a scaled operational amplifier (op-amp) design after compensation. The plot is shown on a logarithmic scale for the frequency axis, denoted as \( \log \omega \), and the magnitude axis is labeled as \( |\beta H(\omega)| \) in decibels (dB).

**Axes Labels and Units:**
- **Horizontal Axis:** Represents frequency \( \omega \) on a logarithmic scale.
- **Vertical Axis:** Represents the magnitude \( |\beta H(\omega)| \) in dB.

**Overall Behavior and Trends:**
- The plot begins at a high gain level \( A_0 \) and remains flat until it reaches the first pole \( \omega'_{p1}/\alpha \), where the gain starts to drop.
- After the first pole, the magnitude continues to decrease, indicating a reduction in gain.
- Another pole occurs at \( \omega_{p1} \), followed by a further decrease in gain.
- The plot shows a compensation for \( \beta < 1 \), which is illustrated by a dashed line representing the compensated response.

**Key Features and Technical Details:**
- The initial gain is \( A_0 \), and there is a reduced gain level \( \beta A_0 \) shown as a reference.
- The frequency \( \omega'_{p1}/\alpha \) indicates the first adjusted pole due to scaling.
- The second pole \( \omega_{p1} \) is marked, followed by the second adjusted pole \( \omega_{p2}/\alpha \).
- The compensation curve is designed to maintain stability and phase margin, indicated by the dashed line.

**Annotations and Specific Data Points:**
- The plot includes annotations for the poles \( \omega'_{p1}/\alpha \), \( \omega_{p1} \), and \( \omega_{p2}/\alpha \), which are critical for understanding the frequency response after scaling and compensation.
- The compensation for \( \beta < 1 \) is explicitly marked, showing the intended design adjustments to maintain performance.

Figure 11.60 (a) Original op amp reponse and frequency compensation, (b) scaled op amp response, and (c) compensation of scaled op amp.
pole after compensation must also be scaled down by this factor [Fig. 11.60(c)]. (3) Since the output impedance of the first stage is multiplied by $\alpha, C_{C}$ should remain at its original value. (4) To place the zero introduced by $R_{z}$ atop $\omega_{p 2} / \alpha$, we multiply $R_{z}$ by $\alpha$ (why?).

Let us try $\alpha=2$ and examine the results. Figure 11.61(a) plots the output waveform, revealing the same final values as before and an overdamped response with $t_{s} \approx 2.5 \mathrm{~ns}$. We can then try scaling by another factor of 4 (i.e., $\alpha=8$ with respect to the original design), observing the heavily overdamped transient shown in Fig. 11.61(b). Now, we adjust $C_{C}$ and $R_{z}$ manually to optimize the speed. With $C_{C}=0.15 \mathrm{pF}$ and $R_{z}=9 \mathrm{k} \Omega$, the step response appears as in Fig. 11.61(c), exhibiting $t_{s} \approx 4.5 \mathrm{~ns}$.
image_name:(a)
description:The graph labeled "(a)" is a time-domain waveform representing the step response of an operational amplifier. The x-axis is labeled "Time (ns)" and is measured in nanoseconds, ranging from 2 ns to 9 ns. The y-axis is labeled "V_{out1} - V_{out2} (mV)" and is measured in millivolts, ranging from 96 mV to 99 mV.

Overall Behavior and Trends:
The graph shows a rapid rise in voltage difference between the outputs (V_{out1} and V_{out2}) starting from approximately 96 mV. The response quickly approaches a steady-state value just below 99 mV, indicating an overdamped response. The curve is smooth and lacks oscillations, suggesting a stable system with no overshoot.

Key Features and Technical Details:
- **Initial Value:** The step response begins at approximately 96 mV.
- **Steady-State Value:** The voltage difference stabilizes just below 99 mV.
- **Settling Time (t_s):** The graph does not provide explicit markers, but the context suggests a settling time of approximately 2.5 ns, where the system reaches and remains within a certain percentage of the final value.

Annotations and Specific Data Points:
There are no specific annotations or markers on the graph. The response is smooth and exhibits a classic overdamped behavior with no visible oscillations or peaks. The trend is a quick rise followed by a leveling off, characteristic of a well-damped system.
image_name:(b)
description:The graph labeled (b) is a time-domain waveform representing the step response of an operational amplifier with a scaling factor of 8. It is plotted on a Cartesian coordinate system where the x-axis represents time in nanoseconds (ns), ranging from 5 ns to 20 ns, and the y-axis represents the voltage difference \( V_{\text{out1}} - V_{\text{out2}} \) in millivolts (mV), ranging from 91 mV to 99 mV.

Overall Behavior and Trends:
The graph shows a heavily overdamped response, characterized by a smooth and gradual rise in voltage over time. The waveform starts at approximately 91 mV and asymptotically approaches a final steady-state value close to 99 mV. There are no oscillations or overshoots, indicating a stable and controlled response.

Key Features and Technical Details:
- **Initial Value:** The response begins at around 91 mV.
- **Final Value:** The voltage difference approaches approximately 99 mV.
- **Settling Time:** The system reaches near steady-state around 15 ns, indicating a heavily overdamped behavior.
- **No Overshoot:** The absence of overshoot suggests a lack of oscillatory behavior, typical of an overdamped system.

Annotations and Specific Data Points:
The graph does not explicitly mark specific data points or annotations, but the smooth curve illustrates the transition from the initial to the final state without any abrupt changes.

This graph effectively demonstrates the effects of scaling on the step response of the operational amplifier, highlighting the impact of increased damping on system performance.
image_name:(c)
description:The graph labeled (c) is a time-domain waveform depicting the step response of an operational amplifier. The x-axis represents time in nanoseconds (ns), ranging from 0 to 20 ns, while the y-axis represents the output voltage difference, \( V_{\text{out1}} - V_{\text{out2}} \), measured in millivolts (mV), ranging from 96.5 mV to 99.5 mV.

Overall Behavior and Trends:
The graph shows a rapid initial increase in the output voltage difference starting from approximately 97 mV at around 0 ns. The waveform reaches a peak slightly above 99 mV at approximately 5 ns, indicating a slight overshoot. After reaching this peak, the voltage difference decreases slightly and stabilizes around 99 mV, indicating a settling behavior with a small overshoot and no oscillations, characteristic of an overdamped response.

Key Features and Technical Details:
- **Initial Rise:** The waveform quickly rises from around 97 mV, indicating a fast response to the step input.
- **Peak Voltage:** The peak occurs slightly above 99 mV at approximately 5 ns, showing a small overshoot.
- **Settling Time (\( t_s \)):** The system stabilizes around 99 mV by approximately 15 ns, with a settling time of about 4.5 ns as indicated in the context.

Annotations and Specific Data Points:
- The graph is marked with gridlines for precision, showing the waveform's progression and stabilization.
- The waveform's behavior is consistent with an optimized design using \( C_C = 0.15 \text{ pF} \) and \( R_z = 9 \text{ k}\Omega \), resulting in the observed response characteristics.

(c)

Figure 11.61 (a) Step response of op amp with scaling factor of 2, (b) step response of op amp with scaling factor of 8 , and (c) modified design with $C_{C}=0.15 \mathrm{pF}$ and $R_{z}=9 \mathrm{k} \Omega$.

It is remarkable that linear scaling along with some adjustment of $C_{C}$ and $R_{z}$ affords an eightfold reduction in power (and area of the transistors). This scaling method entails minimal redesign effort because it does not alter the circuit's gain and swing values. Of course, the scaling gives rise to longer settling and higher noise (and offset). Figure 11.62 shows the scaled op amp design. ${ }^{13}$

[^88]image_name:Figure 11.62 Scaled op amp design
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vb1}
name: M2, type: NMOS, ports: {S: GND, D: Y, G: Vb1}
name: M3, type: NMOS, ports: {S: X, D: Vout1, G: Y}
name: M4, type: NMOS, ports: {S: Y, D: Vout2, G: X}
name: M5, type: PMOS, ports: {S: VDD, D: X, G: Vb2}
name: M6, type: PMOS, ports: {S: VDD, D: Y, G: Vb2}
name: M7, type: PMOS, ports: {S: VDD, D: X, G: Vb3}
name: M8, type: PMOS, ports: {S: VDD, D: Y, G: Vb3}
name: M9, type: PMOS, ports: {S: VDD, D: Vout1, G: Vout1}
name: M10, type: PMOS, ports: {S: VDD, D: Vout2, G: Vout2}
name: M11, type: NMOS, ports: {S: GND, D: Vout1, G: Vout1}
name: M12, type: NMOS, ports: {S: GND, D: Vout2, G: Vout2}
name: Resistor1, type: Resistor, value: 9 kΩ, ports: {N1: Vout2, N2: Y}
name: Resistor2, type: Resistor, value: 160 kΩ, ports: {N1: Vout2, N2: GND}
name: Capacitor1, type: Capacitor, value: 0.15 pF, ports: {Np: Y, Nn: Vout2}
name: CurrentSource1, type: CurrentSource, value: 113 μA, ports: {Np: GND, Nn: X}
name: CurrentSource2, type: CurrentSource, value: 2.5 μA, ports: {Np: GND, Nn: Vout1}
name: CurrentSource3, type: CurrentSource, value: 120 μA, ports: {Np: Vout2, Nn: GND}
]
extrainfo:The circuit is a scaled operational amplifier design with a focus on reducing power and area while maintaining gain and swing values. It includes a differential pair (M1, M2) with active loads (M5, M6), a current mirror (M7, M8), and output stages (M9, M10, M11, M12). The compensation capacitor (0.15 pF) and zero resistor (9 kΩ) are used for stability and performance tuning. Bias voltages are provided at nodes Vb1, Vb2, and Vb3.

Figure 11.62 Scaled op amp design.

### 11.6.5 Large-Signal Behavior

The amplifier's ultimate test is with large output swings ( $1 \mathrm{~V}_{p p \text {, diff }}$ ). Under this condition, the open-loop gain may drop as some transistors sustain less $V_{D S}$, and the speed may suffer as slewing may occur. In the previous simulations, the differential output begins from zero, jumps to some value, and returns to zero. For large-signal tests, however, $V_{\text {out }}$ must swing from -0.5 V to +0.5 V , which can be accomplished by setting the initial differential conditions at the op amp inputs such that $V_{\text {out }}=-0.5 \mathrm{~V}$ at $t=0$. The result is shown in Fig. 11.63.
image_name:(a)
description:The graph labeled (a) is a time-domain waveform representing the large-signal response of a closed-loop amplifier. The x-axis is labeled 'Time (ns)' and spans from 0 to 40 nanoseconds. The y-axis is labeled 'V_{out1} - V_{out2} (mV)' and ranges from -600 millivolts to 600 millivolts. The graph is plotted on a linear scale with gridlines marking significant intervals.

**Overall Behavior and Trends:**
The waveform begins at approximately -500 mV at time t = 0 ns and quickly rises in a steep, almost linear fashion to reach a peak of about 500 mV at around t = 10 ns. This rapid rise indicates a quick response of the amplifier to the input signal. After reaching the peak, the waveform maintains a stable level close to 500 mV, indicating a steady-state operation.

From t = 20 ns to t = 40 ns, the waveform experiences a sharp drop back to approximately -500 mV. This drop is almost symmetrical to the initial rise, suggesting a return to the initial state or a full cycle of the signal response.

**Key Features and Technical Details:**
- The total change in the output voltage (V_{out}) from t = 20 ns to t = 40 ns is approximately 987.4 mV, slightly less than the allowed value for a 1% gain error.
- The waveform exhibits a settling behavior, reaching within 1% of the final value in approximately 6 ns, indicating the speed at which the amplifier stabilizes its output.

**Annotations and Specific Data Points:**
- The waveform does not show significant oscillations or overshoot beyond the initial rise and fall, suggesting good stability in the amplifier's response.
- The transition regions (rise and fall) are critical for understanding the slewing and settling characteristics of the amplifier.
image_name:(b)
description:The graph labeled (b) is a time-domain waveform depicting the settling behavior of the output voltage difference \( V_{\text{out1}} - V_{\text{out2}} \) of a closed-loop amplifier. The x-axis represents time in nanoseconds (ns), ranging from 0 to 20 ns, while the y-axis represents the voltage difference in millivolts (mV), ranging from 482 mV to 498 mV.

Overall Behavior and Trends:
The waveform shows an initial rapid increase in voltage difference, peaking slightly above 498 mV at around 5 ns. Following the peak, the voltage difference decreases gradually, settling towards a final value close to 496 mV. This behavior indicates the system's response to a step input, with the peak representing an overshoot before settling.

Key Features and Technical Details:
- **Overshoot:** The voltage difference peaks at slightly over 498 mV, indicating an overshoot in response to the input change.
- **Settling Time:** The waveform settles to within 1% of the final value (approximately 496 mV) by about 6 ns after the initial overshoot.
- **Settling Accuracy:** The close-up view highlights the settling behavior with high precision, showing the amplifier's ability to stabilize quickly.

Annotations and Specific Data Points:
- The graph is annotated with gridlines that help in assessing the time and voltage difference precisely, aiding in the analysis of the settling time and overshoot magnitude.

This graph provides a detailed view of the amplifier's dynamic response, emphasizing its speed and accuracy in reaching steady state after a perturbation.

Figure 11.63 (a) Large-signal response of closed-loop amplifier, and (b) close-up of (a) showing settling to $1 \%$ accuracy.

We make two observations, First, the total change in $V_{\text {out }}$ from $t \approx 20 \mathrm{~ns}$ to $t \approx 40 \mathrm{~ns}$ is equal to 987.4 mV , about 2.6 mV less than the allowed value for $1 \%$ gain error. Second, the settling to $1 \%$ from the final value is about 6 ns .

Let us first deal with the insufficient gain. We can measure the voltage gain of each stage under these conditions by dividing its differential output swing by its differential input swing (after the voltages have settled). We obtain $A_{v}=39.5$ for the first stage and 10.2 for the second. (In small-signal operation, these values are equal to 46.3 and 11.2 , respectively.) The open-loop gain has thus dropped from 518 to 403. To raise the gain, we double $W$ and $L$ of the NMOS cascode transistors ( $W / L=45 \mu \mathrm{~m} / 0.32 \mu \mathrm{~m}$ ) in the first stage and the NMOS current sources in the second, arriving at the output shown in Fig. 11.64. The gain error is now less than $1 \%$, but the settling has become longer because the pole associated with the source of the NMOS cascode transistors significantly degrades the phase margin.
image_name:(a)
description:The graph labeled as (a) in Figure 11.64 is a time-domain waveform illustrating the large-signal response of a closed-loop amplifier.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform showing the voltage difference between two outputs, \( V_{out1} - V_{out2} \), over time.

2. **Axes Labels and Units:**
- The x-axis represents time in nanoseconds (ns), ranging from 0 to 40 ns.
- The y-axis represents the voltage difference \( V_{out1} - V_{out2} \) in millivolts (mV), ranging from -600 mV to 600 mV.

3. **Overall Behavior and Trends:**
- Initially, the voltage difference rises sharply from approximately -600 mV to around 500 mV within the first few nanoseconds, indicating a rapid response to an input change.
- The waveform then stabilizes around 500 mV, maintaining this level for a significant portion of the time.
- Near the 20 ns mark, the voltage difference begins to decrease sharply, dropping back towards 0 mV.
- The waveform finally settles close to 0 mV, indicating the system's return to a stable state.

4. **Key Features and Technical Details:**
- The waveform exhibits a sharp rise and fall, suggesting a fast response and recovery time.
- The settling time is noticeable as the waveform requires some time to stabilize after the initial rise and subsequent fall.

5. **Annotations and Specific Data Points:**
- No specific annotations or numerical markers are present on the graph, but the overall trend shows a clear initial overshoot followed by stabilization and eventual settling.
image_name:(b)
description:The graph labeled as (b) is a time-domain waveform showing the close-up view of the settling behavior of a closed-loop amplifier's output.

1. **Type of Graph and Function:**
- This is a time-domain response graph.

2. **Axes Labels and Units:**
- The x-axis is labeled "Time" and is measured in nanoseconds (ns).
- The y-axis is labeled "V_out1 - V_out2" and is measured in millivolts (mV).

3. **Overall Behavior and Trends:**
- The waveform begins at approximately 470 mV and quickly rises to a peak just above 510 mV within the first few nanoseconds.
- Following the peak, the waveform exhibits a damped oscillation as it settles back toward a steady-state value.
- The settling process is indicative of a system adjusting to reach a stable output, with minor overshoot observed initially.

4. **Key Features and Technical Details:**
- The peak occurs at around 5 ns, where the voltage difference reaches slightly above 510 mV.
- The waveform then declines and oscillates slightly before stabilizing around 490 mV.
- The behavior suggests the presence of a pole in the system that affects the phase margin, leading to the observed overshoot and oscillations.

5. **Annotations and Specific Data Points:**
- The graph is focused on the settling behavior to 1% accuracy, as indicated in the context.
- The critical points of interest are the initial peak and the subsequent stabilization near 490 mV, reflecting the system's settling characteristics.

Figure 11.64 (a) Large-signal response of closed-loop amplifier, and (b) close-up of (a) showing settling to $1 \%$ accuracy.

#### Example 11.16

Estimate the above pole frequency.

#### Solution

With $C_{o x} \approx 15 \mathrm{fF} / \mu \mathrm{m}^{2}$, the gate-source capacitance of the cascode NMOS transistors amounts to (2/3)(45 $\mu \mathrm{m} \times$ $0.32 \mu \mathrm{~m}) \times 15 \mathrm{fF} / \mu \mathrm{m}^{2} \approx 144 \mathrm{fF}$. (Our calculation is sloppy because the effective length is less than $0.32 \mu \mathrm{~m}$ and the overlap capacitance is neglected.) To this value we must add the S/D junction capacitances and the gate-drain capacitance of the input transistors, obtaining roughly 200 fF . To estimate the transconductance of the cascode devices, we assume that they operate in weak inversion and write $g_{m} \approx I_{D} /\left(\xi V_{T}\right) \approx 56.5 \mu \mathrm{~A} /(1.5 \times 26 \mathrm{mV})=$ $1 /(690 \Omega)$. The pole frequency is thus around 1.15 GHz , contributing substantial phase shift at the open-loop unity-gain frequency.

To address the settling issue, we consider cascode compensation (Chapter 10). In fact, we can combine both methods and, with some iteration, reach the design shown in Fig. 11.65(a). Depicted in Fig. 11.65(b), takes less than $5 \mathrm{~ns} .{ }^{14}$ This performance is achieved with a power consumption of $370 \mu \mathrm{~W}$.

[^89]image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vb1}
name: M2, type: NMOS, ports: {S: GND, D: Y, G: Vb1}
name: M3, type: NMOS, ports: {S: X, D: Y, G: Vout1}
name: M4, type: NMOS, ports: {S: Y, D: Vout2, G: Vout1}
name: M5, type: NMOS, ports: {S: Vb2, D: X, G: Vb3}
name: M6, type: NMOS, ports: {S: Vb2, D: Y, G: Vb3}
name: M7, type: PMOS, ports: {S: VDD, D: Vb2, G: Vb3}
name: M8, type: PMOS, ports: {S: VDD, D: Vb2, G: Vb3}
name: M9, type: PMOS, ports: {S: VDD, D: Vout1, G: Vout1}
name: M10, type: PMOS, ports: {S: VDD, D: Vout2, G: Vout2}
name: M11, type: NMOS, ports: {S: GND, D: Vout1, G: Vout1}
name: M12, type: NMOS, ports: {S: GND, D: Vout2, G: Vout2}
name: 113 µA, type: CurrentSource, value: 113 µA, ports: {Np: X, Nn: GND}
name: 2.5 µA, type: CurrentSource, value: 2.5 µA, ports: {Np: Y, Nn: GND}
name: 30 kΩ, type: Resistor, value: 30 kΩ, ports: {N1: Vout2, N2: Y}
name: 8 kΩ, type: Resistor, value: 8 kΩ, ports: {N1: Vout1, N2: X}
name: 160 kΩ, type: Resistor, value: 160 kΩ, ports: {N1: Vout2, N2: GND}
name: 50 fF, type: Capacitor, value: 50 fF, ports: {Np: Vout1, Nn: Y}
name: 50 fF, type: Capacitor, value: 50 fF, ports: {Np: Vout2, Nn: Y}
]
extrainfo:This circuit is a differential amplifier with cascode compensation, designed for high-speed operation with a power consumption of 370 µW. It achieves a large-signal step response settling time of less than 5 ns. The circuit utilizes both NMOS and PMOS transistors in a complementary configuration to achieve the desired performance. The presence of capacitors and resistors in the feedback path suggests frequency compensation techniques to improve stability and transient response.
image_name:(b)
description:The graph in Figure 11.65(b) is a time-domain waveform representing the closed-loop large-signal step response of an operational amplifier design. The x-axis is labeled 'Time (ns)' and spans from 0 to 20 nanoseconds, with gridlines marking every 5 nanoseconds. The y-axis is labeled 'V_{out1} - V_{out2} (mV)' and ranges from 475 to 500 millivolts, with gridlines marking every 5 millivolts.

The waveform exhibits an initial overshoot, peaking slightly above 500 mV around 2 ns. This is followed by a damped oscillation that settles towards a steady-state value slightly below 490 mV. The waveform indicates a rapid initial response with a settling time of less than 5 ns, as noted in the context. The behavior suggests a well-compensated system with minimal overshoot and quick settling, characteristic of effective cascode compensation techniques. No specific numerical annotations or reference lines are present on the graph.

Figure 11.65 (a) Final op amp design, and (b) its closed-loop large-signal step response.

## 11.7 ■ Summary

This chapter has portrayed to the reader how the analog designer's mind works. We have seen that the design proceeds methodically, assuming an almost arbitrary power budget, and first strives to meet the voltage swing and gain requirements (the toughest issues today). With a reasonable design in hand, we then aggressively reduce the power by linear scaling, paying attention to parameters that cannot be scaled (e.g., the load capacitance) and bearing in mind that speed, noise, and offset degrade. Our efforts exemplify three steps in good analog design. (1) We closely examine the circuit's behavior and understand the root cause of the undesired phenomena. (2) We adjust only the circuit parameters that relate to the root cause-we do not blindly play with any random device. (3) We continue to explore various circuit techniques and new ideas, sometimes reaching a dead end but many a time improving the performance. The reader can see that we optimize the circuits "by hand" rather than automate the task using tools found in simulators. High-performance analog design requires human intelligence.
