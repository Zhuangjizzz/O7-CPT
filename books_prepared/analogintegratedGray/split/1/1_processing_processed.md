# 1. Models for Integrated-Circuit Active Devices

## 1.1 Introduction

The analysis and design of integrated circuits depend heavily on the utilization of suitable models for integrated-circuit components. This is true in hand analysis, where fairly simple models are generally used, and in computer analysis, where more complex models are encountered. Since any analysis is only as accurate as the model used, it is essential that the circuit designer have a thorough understanding of the origin of the models commonly utilized and the degree of approximation involved in each.

This chapter deals with the derivation of large-signal and small-signal models for integrated-circuit devices. The treatment begins with a consideration of the properties of $p n$ junctions, which are basic parts of most integrated-circuit elements. Since this book is primarily concerned with circuit analysis and design, no attempt has been made to produce a comprehensive treatment of semiconductor physics. The emphasis is on summarizing the basic aspects of semiconductor-device behavior and indicating how these can be modeled by equivalent circuits.

## 1.2 Depletion Region of a pn Junction

The properties of reverse-biased $p n$ junctions have an important influence on the characteristics of many integrated-circuit components. For example, reverse-biased pn junctions exist between many integrated-circuit elements and the underlying substrate, and these junctions all contribute voltage-dependent parasitic capacitances. In addition, a number of important characteristics of active devices, such as breakdown voltage and output resistance, depend directly on the properties of the depletion region of a reverse-biased pn junction. Finally, the basic operation of the junction field-effect transistor is controlled by the width of the depletion region of a pn junction. Because of its importance and application to many different problems, an analysis of the depletion region of a reverse-biased pn junction is considered below. The properties of forward-biased pn junctions are treated in Section 1.3 when bipolar-transistor operation is described.

Consider a $p n$ junction under reverse bias as shown in Fig. 1.1. Assume constant doping densities of $N_{D}$ atoms $/ \mathrm{cm}^{3}$ in the $n$-type material and $N_{A}$ atoms $/ \mathrm{cm}^{3}$ in the $p$-type material. (The characteristics of junctions with nonconstant doping densities will be described later.) Due to the difference in carrier concentrations in the $p$-type and $n$-type regions, there exists a region at the junction where the mobile holes and electrons have been removed, leaving the fixed acceptor and donor ions. Each acceptor atom carries a negative charge and each donor atom carries a positive charge, so that the region near the junction is one of significant space charge and resulting high electric field. This is called the depletion region or space-charge
image_name:(a)
description:The image depicts an abrupt p-n junction under reverse bias. The diagrams illustrate key concepts related to the junction: (a) a schematic of the junction with applied reverse bias voltage V_R; (b) charge density distribution showing negative charge in the p-region and positive charge in the n-region; (c) the electric field distribution with a peak at the junction; (d) the electrostatic potential across the junction, indicating the built-in potential psi_0 and the effect of the applied reverse bias.
image_name:(b)
description:The graph labeled (b) in Figure 1.1 represents the charge density (\( \rho \)) across a pn-junction under reverse bias \( V_R \). The x-axis denotes the distance across the junction, while the y-axis represents the charge density.

Type of Graph and Function:
This is a charge density distribution graph for a pn-junction diode under reverse bias conditions.

Axes Labels and Units:
- **X-Axis:** Distance (x) across the junction, no specific units are indicated, but typically measured in micrometers or nanometers.
- **Y-Axis:** Charge density (\( \rho \)), with units typically in coulombs per cubic meter (C/m³).

Overall Behavior and Trends:
- The graph shows a step-like behavior in charge density across the depletion region of the pn-junction.
- On the p-side, the charge density is negative, represented by \( -qN_A \), where \( N_A \) is the acceptor concentration.
- On the n-side, the charge density is positive, represented by \( qN_D \), where \( N_D \) is the donor concentration.

Key Features and Technical Details:
- The charge density is constant within each region (p and n) and abruptly changes at the junction interface.
- The negative charge density on the p-side corresponds to the fixed acceptor ions, while the positive charge density on the n-side corresponds to the fixed donor ions.
- The depletion region is characterized by the absence of mobile charge carriers, resulting in a space charge region.

Annotations and Specific Data Points:
- The graph is annotated with \( -qN_A \) and \( qN_D \) to indicate the charge densities in the p and n regions, respectively.
- The depletion region is sharply defined at the junction, as indicated by the vertical lines on the graph.

This graph effectively illustrates the distribution of charge densities within the depletion region of a pn-junction diode under reverse bias, highlighting the presence of fixed ionic charges in the absence of mobile carriers.
image_name:(c)
description:The graph labeled (c) in Figure 1.1 represents the electric field across a $p$-$n$ junction under reverse bias $V_R$. The x-axis is labeled "Distance" and the y-axis is labeled "Electric field $\mathcal{E}$". The graph shows a piecewise linear function that describes the electric field distribution across the depletion region of the junction.

1. **Type of Graph and Function**: This is a piecewise linear plot depicting the electric field distribution across a semiconductor $p$-$n$ junction under reverse bias conditions.

2. **Axes Labels and Units**: The x-axis represents the distance across the junction, moving from the $p$-type region to the $n$-type region. The y-axis represents the electric field $\mathcal{E}$, although units are not explicitly provided, it is typically measured in volts per meter (V/m).

3. **Overall Behavior and Trends**: The graph shows that the electric field is zero outside the depletion region. Within the depletion region, the electric field increases linearly from zero at the edge of the $p$-type region to a maximum at the junction interface, then decreases linearly back to zero at the edge of the $n$-type region. This indicates that the electric field is strongest at the junction and tapers off symmetrically on either side.

4. **Key Features and Technical Details**: The maximum electric field occurs at the junction interface, indicating the point of highest potential barrier. The linear increase and decrease suggest a uniform distribution of charge within the depletion region, consistent with the abrupt junction model.

5. **Annotations and Specific Data Points**: The graph is annotated with vertical dashed lines marking the boundaries of the depletion region. The labels $-W_1$ and $W_2$ denote the edges of the depletion region on the $p$-type and $n$-type sides, respectively. The symmetry of the graph about the junction indicates equal depletion widths on both sides, assuming equal doping levels, although this is not explicitly stated in the graph.
image_name:(d)
description:The diagram labeled "(d)" represents the electrostatic potential across a semiconductor junction under reverse bias. This graph is a plot of potential (V) versus distance (x) across the junction.

1. **Type of Graph and Function:**
- The graph is a potential distribution plot, typically used in semiconductor physics to illustrate the variation of electrostatic potential across a p-n junction.

2. **Axes Labels and Units:**
- The horizontal axis (x-axis) represents the distance across the junction, moving from the p-type region to the n-type region.
- The vertical axis (y-axis) represents the electrostatic potential (V).
- The scale appears to be linear, with distances marked from \(-W_1\) in the p-region to \(W_2\) in the n-region.

3. **Overall Behavior and Trends:**
- The potential graph starts at a lower value \(V_1\) on the p-side and increases as it moves towards the n-side.
- The potential rises sharply at the junction, indicating the presence of a significant electric field within the depletion region.
- Beyond the depletion region, the potential levels off, reaching a constant value \(\psi_0 + V_R\), which includes the built-in potential \(\psi_0\) and the applied reverse bias \(V_R\).

4. **Key Features and Technical Details:**
- The potential increases across the depletion region, indicating the barrier that opposes carrier movement.
- The graph shows two critical points, \(-W_1\) and \(W_2\), which mark the edges of the depletion region.
- The potential difference across the junction is indicated by \(V_2\).

5. **Annotations and Specific Data Points:**
- The graph is annotated with the built-in potential \(\psi_0\) and the applied reverse bias \(V_R\).
- \(V_1\) and \(V_2\) represent specific potential levels that are relevant to the analysis of the junction.
- The potential reaches a maximum value at the n-side, indicating the effect of the applied reverse bias.

Figure 1.1 The abrupt junction under reverse bias $V_{R}$.
(a) Schematic. (b) Charge density. (c) Electric field. (d) Electrostatic potential.
region. It is assumed that the edges of the depletion region are sharply defined as shown in Fig. 1.1, and this is a good approximation in most cases.

For zero applied bias, there exists a voltage $\psi_{0}$ across the junction called the built-in potential. This potential opposes the diffusion of mobile holes and electrons across the junction in equilibrium and has a value ${ }^{1}$

$$
\begin{equation*}
\psi_{0}=V_{T} \ln \frac{N_{A} N_{D}}{n_{i}^{2}} \tag{1.1}
\end{equation*}
$$

where

$$
V_{T}=\frac{k T}{q} \simeq 26 \mathrm{mV} \quad \text { at } \quad 300^{\circ} \mathrm{K}
$$

the quantity $n_{i}$ is the intrinsic carrier concentration in a pure sample of the semiconductor and $n_{i} \simeq 1.5 \times 10^{10} \mathrm{~cm}^{-3}$ at $300^{\circ} \mathrm{K}$ for silicon.

In Fig. 1.1 the built-in potential is augmented by the applied reverse bias, $V_{R}$, and the total voltage across the junction is $\left(\psi_{0}+V_{R}\right)$. If the depletion region penetrates a distance $W_{1}$ into the $p$-type region and $W_{2}$ into the $n$-type region, then we require

$$
\begin{equation*}
W_{1} N_{A}=W_{2} N_{D} \tag{1.2}
\end{equation*}
$$

because the total charge per unit area on either side of the junction must be equal in magnitude but opposite in sign.

Poisson's equation in one dimension requires that

$$
\begin{equation*}
\frac{d^{2} V}{d x^{2}}=-\frac{\rho}{\epsilon}=\frac{q N_{A}}{\epsilon} \quad \text { for } \quad-W_{1}<x<0 \tag{1.3}
\end{equation*}
$$

where $\rho$ is the charge density, $q$ is the electron charge ( $1.6 \times 10^{-19}$ coulomb), and $\epsilon$ is the permittivity of the silicon $\left(1.04 \times 10^{-12} \mathrm{farad} / \mathrm{cm}\right)$. The permittivity is often expressed as

$$
\begin{equation*}
\epsilon=K_{S} \epsilon_{0} \tag{1.4}
\end{equation*}
$$

where $K_{S}$ is the dielectric constant of silicon and $\epsilon_{0}$ is the permittivity of free space $(8.86 \times$ $10^{-14} \mathrm{~F} / \mathrm{cm}$ ). Integration of (1.3) gives

$$
\begin{equation*}
\frac{d V}{d x}=\frac{q N_{A}}{\epsilon} x+C_{1} \tag{1.5}
\end{equation*}
$$

where $C_{1}$ is a constant. However, the electric field $\mathscr{E}$ is given by

$$
\begin{equation*}
\mathscr{E}=-\frac{d V}{d x}=-\left(\frac{q N_{A}}{\epsilon} x+C_{1}\right) \tag{1.6}
\end{equation*}
$$

Since there is zero electric field outside the depletion region, a boundary condition is

$$
\mathscr{E}=0 \quad \text { for } \quad x=-W_{1}
$$

and use of this condition in (1.6) gives

$$
\begin{equation*}
\mathscr{E}=-\frac{q N_{A}}{\epsilon}\left(x+W_{1}\right)=-\frac{d V}{d x} \quad \text { for } \quad-W_{1}<x<0 \tag{1.7}
\end{equation*}
$$

Thus the dipole of charge existing at the junction gives rise to an electric field that varies linearly with distance.

Integration of (1.7) gives

$$
\begin{equation*}
V=\frac{q N_{A}}{\epsilon}\left(\frac{x^{2}}{2}+W_{1} x\right)+C_{2} \tag{1.8}
\end{equation*}
$$

If the zero for potential is arbitrarily taken to be the potential of the neutral $p$-type region, then a second boundary condition is

$$
V=0 \quad \text { for } \quad x=-W_{1}
$$

and use of this in (1.8) gives

$$
\begin{equation*}
V=\frac{q N_{A}}{\epsilon}\left(\frac{x^{2}}{2}+W_{1} x+\frac{W_{1}^{2}}{2}\right) \quad \text { for } \quad-W_{1}<x<0 \tag{1.9}
\end{equation*}
$$

At $x=0$, we define $V=V_{1}$, and then (1.9) gives

$$
\begin{equation*}
V_{1}=\frac{q N_{A}}{\epsilon} \frac{W_{1}^{2}}{2} \tag{1.10}
\end{equation*}
$$

If the potential difference from $x=0$ to $x=W_{2}$ is $V_{2}$, then it follows that

$$
\begin{equation*}
V_{2}=\frac{q N_{D}}{\epsilon} \frac{W_{2}^{2}}{2} \tag{1.11}
\end{equation*}
$$

and thus the total voltage across the junction is

$$
\begin{equation*}
\psi_{0}+V_{R}=V_{1}+V_{2}=\frac{q}{2 \epsilon}\left(N_{A} W_{1}^{2}+N_{D} W_{2}^{2}\right) \tag{1.12}
\end{equation*}
$$

Substitution of (1.2) in (1.12) gives

$$
\begin{equation*}
\psi_{0}+V_{R}=\frac{q W_{1}^{2} N_{A}}{2 \epsilon}\left(1+\frac{N_{A}}{N_{D}}\right) \tag{1.13}
\end{equation*}
$$

From (1.13), the penetration of the depletion layer into the $p$-type region is

$$
\begin{equation*}
W_{1}=\left[\frac{2 \epsilon\left(\psi_{0}+V_{R}\right)}{q N_{A}\left(1+\frac{N_{A}}{N_{D}}\right)}\right]^{1 / 2} \tag{1.14}
\end{equation*}
$$

Similarly,

$$
\begin{equation*}
W_{2}=\left[\frac{2 \epsilon\left(\psi_{0}+V_{R}\right)}{q N_{D}\left(1+\frac{N_{D}}{N_{A}}\right)}\right]^{1 / 2} \tag{1.15}
\end{equation*}
$$

Equations 1.14 and 1.15 show that the depletion regions extend into the $p$-type and $n$-type regions in inverse relation to the impurity concentrations and in proportion to $\sqrt{\psi_{0}+V_{R}}$. If either $N_{D}$ or $N_{A}$ is much larger than the other, the depletion region exists almost entirely in the lightly doped region.

#### EXAMPLE

An abrupt $p n$ junction in silicon has doping densities $N_{A}=10^{15}$ atoms $/ \mathrm{cm}^{3}$ and $N_{D}=10^{16}$ atoms $/ \mathrm{cm}^{3}$. Calculate the junction built-in potential, the depletion-layer depths, and the maximum field with 10 V reverse bias.

From (1.1)

$$
\psi_{0}=26 \ln \frac{10^{15} \times 10^{16}}{2.25 \times 10^{20}} \mathrm{mV}=638 \mathrm{mV} \text { at } 300^{\circ} \mathrm{K}
$$

From (1.14) the depletion-layer depth in the $p$-type region is

$$
\begin{aligned}
W_{1} & =\left(\frac{2 \times 1.04 \times 10^{-12} \times 10.64}{1.6 \times 10^{-19} \times 10^{15} \times 1.1}\right)^{1 / 2}=3.5 \times 10^{-4} \mathrm{~cm} \\
& =3.5 \mu \mathrm{~m}\left(\text { where } 1 \mu \mathrm{~m}=1 \text { micrometer }=10^{-6} \mathrm{~m}\right)
\end{aligned}
$$

The depletion-layer depth in the more heavily doped $n$-type region is

$$
W_{2}=\left(\frac{2 \times 1.04 \times 10^{-12} \times 10.64}{1.6 \times 10^{-19} \times 10^{16} \times 11}\right)^{1 / 2}=0.35 \times 10^{-4} \mathrm{~cm}=0.35 \mu \mathrm{~m}
$$

Finally, from (1.7) the maximum field that occurs for $x=0$ is

$$
\begin{aligned}
\mathscr{E}_{\max } & =-\frac{q N_{A}}{\epsilon} W_{1}=-1.6 \times 10^{-19} \times \frac{10^{15} \times 3.5 \times 10^{-4}}{1.04 \times 10^{-12}} \\
& =-5.4 \times 10^{4} \mathrm{~V} / \mathrm{cm}
\end{aligned}
$$

Note the large magnitude of this electric field.

### 1.2.1 Depletion-Region Capacitance

Since there is a voltage-dependent charge $Q$ associated with the depletion region, we can calculate a small-signal capacitance $C_{j}$ as follows:

$$
\begin{equation*}
C_{j}=\frac{d Q}{d V_{R}}=\frac{d Q}{d W_{1}} \frac{d W_{1}}{d V_{R}} \tag{1.16}
\end{equation*}
$$

Now

$$
\begin{equation*}
d Q=A q N_{A} d W_{1} \tag{1.17}
\end{equation*}
$$

where $A$ is the cross-sectional area of the junction. Differentiation of (1.14) gives

$$
\begin{equation*}
\frac{d W_{1}}{d V_{R}}=\left[\frac{\epsilon}{2 q N_{A}\left(1+\frac{N_{A}}{N_{D}}\right)\left(\psi_{0}+V_{R}\right)}\right]^{1 / 2} \tag{1.18}
\end{equation*}
$$

Use of (1.17) and (1.18) in (1.16) gives

$$
\begin{equation*}
C_{j}=A\left[\frac{q \epsilon N_{A} N_{D}}{2\left(N_{A}+N_{D}\right)}\right]^{1 / 2} \frac{1}{\sqrt{\psi_{0}+V_{R}}} \tag{1.19}
\end{equation*}
$$

The above equation was derived for the case of reverse bias $V_{R}$ applied to the diode. However, it is valid for positive bias voltages as long as the forward current flow is small. Thus, if $V_{D}$ represents the bias on the junction (positive for forward bias, negative for reverse bias), then (1.19) can be written as

$$
\begin{align*}
C_{j} & =A\left[\frac{q \epsilon N_{A} N_{D}}{2\left(N_{A}+N_{D}\right)}\right]^{1 / 2} \frac{1}{\sqrt{\psi_{0}-V_{D}}}  \tag{1.20}\\
& =\frac{C_{j 0}}{\sqrt{1-\frac{V_{D}}{\psi_{0}}}} \tag{1.21}
\end{align*}
$$

where $C_{j 0}$ is the value of $C_{j}$ for $V_{D}=0$.
Equations 1.20 and 1.21 were derived using the assumption of constant doping in the $p$-type and $n$-type regions. However, many practical diffused junctions more closely approach a graded doping profile as shown in Fig. 1.2. In this case, a similar calculation yields

$$
\begin{equation*}
C_{j}=\frac{C_{j 0}}{\sqrt[3]{1-\frac{V_{D}}{\psi_{0}}}} \tag{1.22}
\end{equation*}
$$

image_name:Figure 1.2 Charge density versus distance in a graded junction
description:The graph in Figure 1.2 is a plot representing the charge density (\( \rho \)) versus distance (\( x \)) in a graded junction. The x-axis is labeled as 'Distance' and the y-axis as 'Charge density \( \rho \)'. Both axes appear to use a linear scale, although specific units are not provided.

The graph shows a linear relationship between charge density and distance, with the charge density increasing as the distance increases. The line is divided into two distinct regions: one with a negative slope on the left and one with a positive slope on the right. The transition occurs at the origin, where the distance is zero. The line with a positive slope is annotated with \( \rho = ax \), indicating that the charge density is directly proportional to the distance with a proportionality constant \( a \).

Overall, the graph shows a symmetrical linear increase and decrease in charge density with distance, centered around the origin. The negative slope region represents a decrease in charge density as distance decreases from zero, while the positive slope region represents an increase in charge density as distance increases from zero. This behavior is typical for a graded junction where the doping profile changes gradually across the junction.

Figure 1.2 Charge density versus distance in a graded junction.
image_name:Figure 1.3
description:The graph in Figure 1.3 illustrates the behavior of the $p-n$ junction depletion-layer capacitance, $C_j$, as a function of the bias voltage, $V_D$. The graph is a plot with the capacitance $C_j$ on the vertical axis and the bias voltage $V_D$ on the horizontal axis. The capacitance is measured in arbitrary units, while the bias voltage is divided into reverse and forward bias regions, with a marked point at $\psi_0$ representing a critical voltage level.

Type of Graph and Function
This is a capacitance versus voltage graph, typically used in semiconductor physics to describe the behavior of junction capacitance under varying voltage conditions.

Axes Labels and Units
- **Vertical Axis:** Represents the depletion-layer capacitance, $C_j$.
- **Horizontal Axis:** Represents the bias voltage, $V_D$, with sections labeled as "Reverse bias" and "Forward bias."

Overall Behavior and Trends
The graph shows two curves:
1. **Simple Theory (Equation 1.21):** This curve starts at a baseline capacitance value, $C_{j0}$, under reverse bias and shows a gradual increase as the voltage approaches zero, then a rapid increase in capacitance as the voltage moves into the forward bias region.
2. **More Accurate Calculation:** This curve follows a similar trend but diverges from the simple theory as the forward bias increases, showing a steeper rise in capacitance approaching $\psi_0$.

Key Features and Technical Details
- **Reverse Bias Region:** The capacitance remains relatively constant, reflecting typical behavior where the depletion region is wide, and the capacitance is low.
- **Forward Bias Region:** Both curves show an increase in capacitance, with the more accurate calculation predicting a sharper increase as it approaches $\psi_0$.
- **Critical Points:** The graph highlights a critical voltage level $\psi_0$, where the capacitance theoretically approaches infinity.

Annotations and Specific Data Points
- **$C_{j0}$:** The baseline capacitance value in the reverse bias region.
- **$\psi_0/2$ and $\psi_0$:** Dashed vertical lines indicate significant voltage levels, with $\psi_0$ marking the point where theoretical predictions suggest a divergence in capacitance behavior.

The graph provides a visual comparison between a simplified theoretical model and a more accurate calculation, emphasizing the limitations of simple models in predicting capacitance behavior near critical voltage levels.

Figure 1.3 Behavior of $p n$ junction depletion-layer capacitance $C_{j}$ as a function of bias voltage $V_{D}$.

Note that both (1.21) and (1.22) predict values of $C_{j}$ approaching infinity as $V_{D}$ approaches $\psi_{0}$. However, the current flow in the diode is then appreciable and the equations are no longer valid. A more exact analysis ${ }^{2,3}$ of the behavior of $C_{j}$ as a function of $V_{D}$ gives the result shown in Fig. 1.3. For forward bias voltages up to about $\psi_{0} / 2$, the values of $C_{j}$ predicted by (1.21) are very close to the more accurate value. As an approximation, some computer programs approximate $C_{j}$ for $V_{D}>\psi_{0} / 2$ by a linear extrapolation of (1.21) or (1.22).

#### EXAMPLE

If the zero-bias capacitance of a diffused junction is 3 pF and $\psi_{0}=0.5 \mathrm{~V}$, calculate the capacitance with 10 V reverse bias. Assume the doping profile can be approximated by an abrupt junction.

From (1.21)

$$
C_{j}=\frac{3}{\sqrt{1+\frac{10}{0.5}}} \mathrm{pF}=0.65 \mathrm{pF}
$$

### 1.2.2 Junction Breakdown

From Fig. 1.1c it can be seen that the maximum electric field in the depletion region occurs at the junction, and for an abrupt junction (1.7) yields a value

$$
\begin{equation*}
\mathscr{E}_{\max }=-\frac{q N_{A}}{\epsilon} W_{1} \tag{1.23}
\end{equation*}
$$

Substitution of (1.14) in (1.23) gives

$$
\begin{equation*}
\left|\mathscr{E}_{\max }\right|=\left[\frac{2 q N_{A} N_{D} V_{R}}{\epsilon\left(N_{A}+N_{D}\right)}\right]^{1 / 2} \tag{1.24}
\end{equation*}
$$

where $\psi_{0}$ has been neglected. Equation 1.24 shows that the maximum field increases as the doping density increases and the reverse bias increases. Although useful for indicating the
functional dependence of $\mathscr{E}_{\max }$ on other variables, this equation is strictly valid for an ideal plane junction only. Practical junctions tend to have edge effects that cause somewhat higher values of $\mathscr{E}_{\text {max }}$ due to a concentration of the field at the curved edges of the junction.

Any reverse-biased $p n$ junction has a small reverse current flow due to the presence of minority-carrier holes and electrons in the vicinity of the depletion region. These are swept across the depletion region by the field and contribute to the leakage current of the junction. As the reverse bias on the junction is increased, the maximum field increases and the carriers acquire increasing amounts of energy between lattice collisions in the depletion region. At a critical field $\mathscr{E}_{\text {crit }}$ the carriers traversing the depletion region acquire sufficient energy to create new hole-electron pairs in collisions with silicon atoms. This is called the avalanche process and leads to a sudden increase in the reverse-bias leakage current since the newly created carriers are also capable of producing avalanche. The value of $\mathscr{E}_{\text {crit }}$ is about $3 \times 10^{5} \mathrm{~V} / \mathrm{cm}$ for junction doping densities in the range of $10^{15}$ to $10^{16}$ atoms $/ \mathrm{cm}^{3}$, but it increases slowly as the doping density increases and reaches about $10^{6} \mathrm{~V} / \mathrm{cm}$ for doping densities of $10^{18}$ atoms $/ \mathrm{cm}^{3}$.

A typical $I-V$ characteristic for a junction diode is shown in Fig. 1.4, and the effect of avalanche breakdown is seen by the large increase in reverse current, which occurs as the reverse bias approaches the breakdown voltage $B V$. This corresponds to the maximum field $\mathscr{E}_{\text {max }}$ approaching $\mathscr{E}_{\text {crit }}$. It has been found empirically ${ }^{4}$ that if the normal reverse bias current of the diode is $I_{R}$ with no avalanche effect, then the actual reverse current near the breakdown voltage is

$$
\begin{equation*}
I_{R A}=M I_{R} \tag{1.25}
\end{equation*}
$$

where $M$ is the multiplication factor defined by

$$
\begin{equation*}
M=\frac{1}{1-\left(\frac{V_{R}}{B V}\right)^{n}} \tag{1.26}
\end{equation*}
$$

In this equation, $V_{R}$ is the reverse bias on the diode and $n$ has a value between 3 and 6 .
image_name:Figure 1.4 Typical I-V characteristic of a junction diode showing avalanche breakdown
description:The graph is a typical I-V characteristic curve of a junction diode, illustrating the avalanche breakdown phenomenon. The horizontal axis represents the voltage (V) in volts, while the vertical axis represents the current (I) in milliamperes (mA). The scales on both axes are linear.

Overall Behavior and Trends:
- **Forward Bias Region (V > 0):**
- As the voltage increases from 0 volts, the current remains near zero until a certain threshold, after which it rises sharply, indicating the diode's forward conduction.

- **Reverse Bias Region (V < 0):**
- Initially, the current remains very low as the reverse voltage increases negatively, indicating the diode's reverse blocking state.
- At a specific negative voltage, marked as \(-BV\) (breakdown voltage), the current increases dramatically, illustrating the avalanche breakdown.

Key Features and Technical Details:
- **Breakdown Voltage (\(-BV\)):**
- The breakdown voltage is indicated at approximately \(-25\) volts on the graph. At this point, the reverse current increases significantly, marking the onset of avalanche breakdown.

- **Avalanche Region:**
- Beyond the breakdown voltage, the current rises steeply, showing the diode's inability to block reverse current effectively. This region requires external current limiting to prevent device damage.

Annotations and Specific Data Points:
- A dashed vertical line at \(-BV\) highlights the breakdown voltage threshold.
- The current scales up to 5 mA in the positive direction, showing the diode's conduction capacity in forward bias and the significant increase in reverse current during breakdown.

This graph effectively demonstrates the critical regions of diode operation, particularly emphasizing the avalanche breakdown in the reverse bias region, which is crucial for applications such as voltage regulation in Zener diodes.

Figure 1.4 Typical $I-V$ characteristic of a junction diode showing avalanche breakdown.

The operation of a $p n$ junction in the breakdown region is not inherently destructive. However, the avalanche current flow must be limited by external resistors in order to prevent excessive power dissipation from occurring at the junction and causing damage to the device. Diodes operated in the avalanche region are widely used as voltage references and are called Zener diodes. There is another, related process called Zener breakdown, ${ }^{5}$ which is different from the avalanche breakdown described above. Zener breakdown occurs only in very heavily doped junctions where the electric field becomes large enough (even with small reverse-bias voltages) to strip electrons away from the valence bonds. This process is called tunneling, and there is no multiplication effect as in avalanche breakdown. Although the Zener breakdown mechanism is important only for breakdown voltages below about 6 V , all breakdown diodes are commonly referred to as Zener diodes.

The calculations so far have been concerned with the breakdown characteristic of plane abrupt junctions. Practical diffused junctions differ in some respects from these results and the characteristics of these junctions have been calculated and tabulated for use by designers. ${ }^{5}$ In particular, edge effects in practical diffused junctions can result in breakdown voltages as much as 50 percent below the value calculated for a plane junction.

#### EXAMPLE

An abrupt plane $p n$ junction has doping densities $N_{A}=5 \times 10^{15}$ atoms $/ \mathrm{cm}^{3}$ and $N_{D}=10^{16}$ atoms $/ \mathrm{cm}^{3}$. Calculate the breakdown voltage if $\mathscr{E}_{\text {crit }}=3 \times 10^{5} \mathrm{~V} / \mathrm{cm}$.

The breakdown voltage is calculated using $\mathscr{E}_{\text {max }}=\mathscr{E}_{\text {crit }}$ in (1.24) to give

$$
\begin{aligned}
B V & =\frac{\epsilon\left(N_{A}+N_{D}\right)}{2 q N_{A} N_{D}} \mathscr{E}_{\text {crit }}^{2} \\
& =\frac{1.04 \times 10^{-12} \times 15 \times 10^{15}}{2 \times 1.6 \times 10^{-19} \times 5 \times 10^{15} \times 10^{16}} \times 9 \times 10^{10} \mathrm{~V} \\
& =88 \mathrm{~V}
\end{aligned}
$$

## 1.3 Large-Signal Behavior of Bipolar Transistors

In this section, the large-signal or dc behavior of bipolar transistors is considered. Large-signal models are developed for the calculation of total currents and voltages in transistor circuits, and such effects as breakdown voltage limitations, which are usually not included in models, are also considered. Second-order effects, such as current-gain variation with collector current and Early voltage, can be important in many circuits and are treated in detail.

The sign conventions used for bipolar transistor currents and voltages are shown in Fig. 1.5. All bias currents for both $n p n$ and $p n p$ transistors are assumed positive going into the device.

### 1.3.1 Large-Signal Models in the Forward-Active Region

A typical npn planar bipolar transistor structure is shown in Fig. 1.6a, where collector, base, and emitter are labeled $C, B$, and $E$, respectively. The method of fabricating such transistor structures is described in Chapter 2. It is shown there that the impurity doping density in the base and the emitter of such a transistor is not constant but varies with distance from the top surface. However, many of the characteristics of such a device can be predicted by analyzing the idealized transistor structure shown in Fig. 1.6b. In this structure, the base and emitter
image_name:Figure 1.5 Bipolar transistor sign convention.
description:
[
name: name: Q1, type: NPN, ports: {C: C, B: B, E: E}
name: name: Q1, type: PNP, ports: {C: C, B: B, E: E}
]
extrainfo:The diagram illustrates the sign convention for bipolar transistors, showing both NPN and PNP types with their respective voltage and current directions. For the NPN transistor, the collector current (IC) flows into the collector, the base current (IB) flows into the base, and the emitter current (IE) flows out of the emitter. For the PNP transistor, the current directions are reversed. The voltages VBE, VBC, and VCE are shown with their polarities for both types of transistors.

Figure 1.5 Bipolar transistor sign convention.
image_name:Figure 1.6 (a)
description:The image labeled "Figure 1.6 (a)" depicts a cross-sectional view of a typical NPN planar bipolar transistor structure. The diagram illustrates the layered configuration of semiconductor materials and the electrical connections associated with each region.

1. **Identification of Components and Structure:**
- The structure consists of three primary regions: the **emitter (E)**, the **base (B)**, and the **collector (C)**.
- The **emitter** is labeled with an 'E' and is composed of an n-type semiconductor.
- The **base** is labeled with a 'B' and is a p-type semiconductor region situated between the emitter and collector.
- The **collector** is labeled with a 'C' and is also an n-type semiconductor, forming the main body of the transistor.

2. **Connections and Interactions:**
- The emitter, base, and collector are connected to external circuits through metallic contacts depicted at the top of each region.
- The diagram shows the typical flow of electrons in an NPN transistor, where electrons are injected from the emitter into the base and then collected by the collector.
- The base is thin and lightly doped to allow efficient electron flow from the emitter to the collector.

3. **Labels, Annotations, and Key Features:**
- The diagram includes labels for each region (E, B, C) that denote the emitter, base, and collector, respectively.
- The doping types are indicated by the letters 'n' and 'p' within the respective regions, highlighting the n-type and p-type semiconductor materials used.
- The overall structure is planar, which is typical for integrated circuit applications, allowing for efficient fabrication and operation of the transistor.

This cross-sectional view provides a clear understanding of the internal architecture of an NPN bipolar transistor, showing the arrangement and interaction of its components.


image_name:(b)
description:The image labeled as "(b)" depicts an idealized structure of an NPN planar bipolar transistor. The diagram is a simplified cross-sectional view showing the arrangement of the three main semiconductor regions: two n-type regions and one p-type region sandwiched between them. These regions are labeled as follows:

1. **N-type Region (Emitter):** Located at the bottom, this region is heavily doped and is connected to the terminal labeled "E" for the emitter.

2. **P-type Region (Base):** Positioned in the middle, this region is lightly doped compared to the n-type regions. It is connected to the terminal labeled "B" for the base.

3. **N-type Region (Collector):** Situated at the top, this region is moderately doped and is connected to the terminal labeled "C" for the collector.

The diagram also includes a vertical dashed line labeled "A A'", which represents a cross-section where carrier concentrations are analyzed in other related diagrams (such as part (c) of Figure 1.6). The x-axis is marked with two positions, "x = 0" and "x = W_B", indicating the boundaries of the base region.

This idealized structure is used to illustrate the basic operation and architecture of the NPN transistor, emphasizing the planar design common in integrated circuits. The uniform doping densities assumed in this model are typical for a uniform-base transistor, simplifying the analysis of carrier movement and interactions within the device.

(b)
image_name:(c)
description:The graph in Figure 1.6 (c) represents the carrier concentrations along the cross-section \( AA' \) of an idealized NPN transistor structure. The x-axis is labeled with positions "x = 0" and "x = W_B", representing the boundaries of the base region. The y-axis is labeled as "Carrier concentration," indicating the concentration levels of different carriers in the transistor.

Type of Graph and Function:
This is a schematic plot illustrating carrier concentration profiles across the emitter, base, and collector regions of an NPN transistor. It is not a mathematical function plot but a conceptual illustration.

Axes Labels and Units:
- **X-axis:** Represents the position along the cross-section of the transistor, marked with significant points at \( x = 0 \) (beginning of the base) and \( x = W_B \) (end of the base).
- **Y-axis:** Represents carrier concentration, although no specific units are provided, it is implied to be in terms of concentration levels.

Overall Behavior and Trends:
- **Emitter Region (left side):**
- The electron concentration \( n_{nE} \) is high and constant.
- The hole concentration \( p_{nE} \) starts high and decreases sharply into the depletion region.
- **Base Region (middle section):**
- The hole concentration \( p_p(x) \) linearly decreases from \( x = 0 \) to \( x = W_B \).
- The electron concentration \( n_p(x) \) also decreases linearly but starts from a lower concentration compared to holes.
- \( N_A \) indicates the acceptor doping concentration in the base.
- **Collector Region (right side):**
- The electron concentration \( n_{nC} \) is high and constant.
- The hole concentration \( p_{nC} \) starts low and increases sharply into the depletion region.
- \( N_D \) represents the donor doping concentration in the collector.

Key Features and Technical Details:
- **Depletion Regions:** Marked by vertical dashed lines, indicating areas where carrier concentration changes sharply.
- **Carrier Concentrations:**
- \( n_{nE} \), \( p_{nE}(0) \), \( n_{p}(0) \), \( n_{p}(W_B) \), \( n_{nC} \), and \( p_{nC} \) denote specific carrier concentrations at key points.
- **Doping Levels:** \( N_A \) and \( N_D \) are indicated to show the level of doping in the base and collector, respectively.

Annotations and Specific Data Points:
- The graph includes annotations for specific concentrations and doping levels, providing a clear understanding of the carrier distribution in different regions of the transistor.
- The transitions between regions are marked by vertical dashed lines, indicating the boundaries of the depletion regions.

(c)

Figure 1.6 (a) Cross section of a typical npn planar bipolar transistor structure. (b) Idealized transistor structure. (c) Carrier concentrations along the cross section $A A^{\prime}$ of the transistor in (b). Uniform doping densities are assumed. (Not to scale.)
doping densities are assumed constant, and this is sometimes called a uniform-base transistor. Where possible in the following analyses, the equations for the uniform-base analysis are expressed in a form that applies also to nonuniform-base transistors.

A cross section $A A^{\prime}$ is taken through the device of Fig. $1.6 b$ and carrier concentrations along this section are plotted in Fig. 1.6c. Hole concentrations are denoted by $p$ and electron concentrations by $n$ with subscripts $p$ or $n$ representing $p$-type or $n$-type regions. The $n$ type emitter and collector regions are distinguished by subscripts $E$ and $C$, respectively. The carrier concentrations shown in Fig. 1.6c apply to a device in the forward-active region. That is, the base-emitter junction is forward biased and the base-collector junction is reverse biased. The minority-carrier concentrations in the base at the edges of the depletion regions can be calculated from a Boltzmann approximation to the Fermi-Dirac distribution function to give ${ }^{6}$

$$
\begin{align*}
n_{p}(0) & =n_{p o} \exp \frac{V_{B E}}{V_{T}}  \tag{1.27}\\
n_{p}\left(W_{B}\right) & =n_{p o} \exp \frac{V_{B C}}{V_{T}} \simeq 0 \tag{1.28}
\end{align*}
$$

where $W_{B}$ is the width of the base from the base-emitter depletion layer edge to the basecollector depletion layer edge and $n_{p o}$ is the equilibrium concentration of electrons in the base. Note that $V_{B C}$ is negative for an $n p n$ transistor in the forward-active region and thus $n_{p}\left(W_{B}\right)$ is very small. Low-level injection conditions are assumed in the derivation of (1.27) and (1.28). This means that the minority-carrier concentrations are always assumed much smaller than the majority-carrier concentration.

If recombination of holes and electrons in the base is small, it can be shown that ${ }^{7}$ the minority-carrier concentration $n_{p}(x)$ in the base varies linearly with distance. Thus a straight line can be drawn joining the concentrations at $x=0$ and $x=W_{B}$ in Fig. 1.6c.

For charge neutrality in the base, it is necessary that

$$
\begin{equation*}
N_{A}+n_{p}(x)=p_{p}(x) \tag{1.29}
\end{equation*}
$$

and thus

$$
\begin{equation*}
p_{p}(x)-n_{p}(x)=N_{A} \tag{1.30}
\end{equation*}
$$

where $p_{p}(x)$ is the hole concentration in the base and $N_{A}$ is the base doping density that is assumed constant. Equation 1.30 indicates that the hole and electron concentrations are separated by a constant amount and thus $p_{p}(x)$ also varies linearly with distance.

Collector current is produced by minority-carrier electrons in the base diffusing in the direction of the concentration gradient and being swept across the collector-base depletion region by the field existing there. The diffusion current density due to electrons in the base is

$$
\begin{equation*}
J_{n}=q D_{n} \frac{d n_{p}(x)}{d x} \tag{1.31}
\end{equation*}
$$

where $D_{n}$ is the diffusion constant for electrons. From Fig. 1.6c

$$
\begin{equation*}
J_{n}=-q D_{n} \frac{n_{p}(0)}{W_{B}} \tag{1.32}
\end{equation*}
$$

If $I_{C}$ is the collector current and is taken as positive flowing into the collector, it follows from (1.32) that

$$
\begin{equation*}
I_{C}=q A D_{n} \frac{n_{p}(0)}{W_{B}} \tag{1.33}
\end{equation*}
$$

where $A$ is the cross-sectional area of the emitter. Substitution of (1.27) into (1.33) gives

$$
\begin{align*}
I_{C} & =\frac{q A D_{n} n_{p o}}{W_{B}} \exp \frac{V_{B E}}{V_{T}}  \tag{1.34}\\
& =I_{S} \exp \frac{V_{B E}}{V_{T}} \tag{1.35}
\end{align*}
$$

where

$$
\begin{equation*}
I_{S}=\frac{q A D_{n} n_{p o}}{W_{B}} \tag{1.36}
\end{equation*}
$$

and $I_{S}$ is a constant used to describe the transfer characteristic of the transistor in the forwardactive region. Equation 1.36 can be expressed in terms of the base doping density by noting that ${ }^{8}$ (see Chapter 2)

$$
\begin{equation*}
n_{p o}=\frac{n_{i}^{2}}{N_{A}} \tag{1.37}
\end{equation*}
$$

and substitution of (1.37) in (1.36) gives

$$
\begin{equation*}
I_{S}=\frac{q A D_{n} n_{i}^{2}}{W_{B} N_{A}}=\frac{q A \bar{D}_{n} n_{i}^{2}}{Q_{B}} \tag{1.38}
\end{equation*}
$$

where $Q_{B}=W_{B} N_{A}$ is the number of doping atoms in the base per unit area of the emitter and $n_{i}$ is the intrinsic carrier concentration in silicon. In this form (1.38) applies to both uniformand nonuniform-base transistors and $D_{n}$ has been replaced by $\bar{D}_{n}$, which is an average effective value for the electron diffusion constant in the base. This is necessary for nonuniform-base devices because the diffusion constant is a function of impurity concentration. Typical values of $I_{S}$ as given by (1.38) are from $10^{-14}$ to $10^{-16} \mathrm{~A}$.

Equation 1.35 gives the collector current as a function of base-emitter voltage. The base current $I_{B}$ is also an important parameter and, at moderate current levels, consists of two major components. One of these ( $I_{B 1}$ ) represents recombination of holes and electrons in the base and is proportional to the minority-carrier charge $Q_{e}$ in the base. From Fig. 1.6c, the minority-carrier charge in the base is

$$
\begin{equation*}
Q_{e}=\frac{1}{2} n_{p}(0) W_{B} q A \tag{1.39}
\end{equation*}
$$

and we have

$$
\begin{equation*}
I_{B 1}=\frac{Q_{e}}{\tau_{b}}=\frac{1}{2} \frac{n_{p}(0) W_{B} q A}{\tau_{b}} \tag{1.40}
\end{equation*}
$$

where $\tau_{b}$ is the minority-carrier lifetime in the base. $I_{B 1}$ represents a flow of majority holes from the base lead into the base region. Substitution of (1.27) in (1.40) gives

$$
\begin{equation*}
I_{B 1}=\frac{1}{2} \frac{n_{p o} W_{B} q A}{\tau_{b}} \exp \frac{V_{B E}}{V_{T}} \tag{1.41}
\end{equation*}
$$

The second major component of base current (usually the dominant one in integratedcircuit $n p n$ devices) is due to injection of holes from the base into the emitter. This current component depends on the gradient of minority-carrier holes in the emitter and is ${ }^{9}$

$$
\begin{equation*}
I_{B 2}=\frac{q A D_{p}}{L_{p}} p_{n E}(0) \tag{1.42}
\end{equation*}
$$

where $D_{p}$ is the diffusion constant for holes and $L_{p}$ is the diffusion length (assumed small) for holes in the emitter. $p_{n E}(0)$ is the concentration of holes in the emitter at the edge of the
depletion region and is

$$
\begin{equation*}
p_{n E}(0)=p_{n E o} \exp \frac{V_{B E}}{V_{T}} \tag{1.43}
\end{equation*}
$$

If $N_{D}$ is the donor atom concentration in the emitter (assumed constant), then

$$
\begin{equation*}
p_{n E o} \simeq \frac{n_{i}^{2}}{N_{D}} \tag{1.44}
\end{equation*}
$$

The emitter is deliberately doped much more heavily than the base, making $N_{D}$ large and $p_{n E o}$ small, so that the base-current component, $I_{B 2}$, is minimized.

Substitution of (1.43) and (1.44) in (1.42) gives

$$
\begin{equation*}
I_{B 2}=\frac{q A D_{p}}{L_{p}} \frac{n_{i}^{2}}{N_{D}} \exp \frac{V_{B E}}{V_{T}} \tag{1.45}
\end{equation*}
$$

The total base current, $I_{B}$, is the sum of $I_{B 1}$ and $I_{B 2}$ :

$$
\begin{equation*}
I_{B}=I_{B 1}+I_{B 2}=\left(\frac{1}{2} \frac{n_{p o} W_{B} q A}{\tau_{b}}+\frac{q A D_{p}}{L_{p}} \frac{n_{i}^{2}}{N_{D}}\right) \exp \frac{V_{B E}}{V_{T}} \tag{1.46}
\end{equation*}
$$

Although this equation was derived assuming uniform base and emitter doping, it gives the correct functional dependence of $I_{B}$ on device parameters for practical double-diffused nonuniform-base devices. Second-order components of $I_{B}$, which are important at low current levels, are considered later.

Since $I_{C}$ in (1.35) and $I_{B}$ in (1.46) are both proportional to $\exp \left(V_{B E} / V_{T}\right)$ in this analysis, the base current can be expressed in terms of collector current as

$$
\begin{equation*}
I_{B}=\frac{I_{C}}{\beta_{F}} \tag{1.47}
\end{equation*}
$$

where $\beta_{F}$ is the forward current gain. An expression for $\beta_{F}$ can be calculated by substituting (1.34) and (1.46) in (1.47) to give

$$
\begin{equation*}
\beta_{F}=\frac{\frac{q A D_{n} n_{p o}}{W_{B}}}{\frac{1}{2} \frac{n_{p o} W_{B} q A}{\tau_{b}}+\frac{q A D_{p} n_{i}^{2}}{L_{p} N_{D}}}=\frac{1}{\frac{W_{B}^{2}}{2 \tau_{b} D_{n}}+\frac{D_{p}}{D_{n}} \frac{W_{B}}{L_{p}} \frac{N_{A}}{N_{D}}} \tag{1.48}
\end{equation*}
$$

where (1.37) has been substituted for $n_{p o}$. Equation 1.48 shows that $\beta_{F}$ is maximized by minimizing the base width $W_{B}$ and maximizing the ratio of emitter to base doping densities $N_{D} / N_{A}$. Typical values of $\beta_{F}$ for $n p n$ transistors in integrated circuits are 50 to 500 , whereas lateral pnp transistors (to be described in Chapter 2) have values 10 to 100. Finally, the emitter current is

$$
\begin{equation*}
I_{E}=-\left(I_{C}+I_{B}\right)=-\left(I_{C}+\frac{I_{C}}{\beta_{F}}\right)=-\frac{I_{C}}{\alpha_{F}} \tag{1.49}
\end{equation*}
$$

where

$$
\begin{equation*}
\alpha_{F}=\frac{\beta_{F}}{1+\beta_{F}} \tag{1.50}
\end{equation*}
$$

The value of $\alpha_{F}$ can be expressed in terms of device parameters by substituting (1.48) in (1.50) to obtain

$$
\begin{equation*}
\alpha_{F}=\frac{1}{1+\frac{1}{\beta_{F}}}=\frac{1}{1+\frac{W_{B}^{2}}{2 \tau_{b} D_{n}}+\frac{D_{p}}{D_{n}} \frac{W_{B}}{L_{p}} \frac{N_{A}}{N_{D}}} \simeq \alpha_{T} \gamma \tag{1.51}
\end{equation*}
$$

where

$$
\begin{gather*}
\alpha_{T}=\frac{1}{1+\frac{W_{B}^{2}}{2 \tau_{b} D_{n}}}  \tag{1.51a}\\
\gamma=\frac{1}{1+\frac{D_{p}}{D_{n}} \frac{W_{B}}{L_{p}} \frac{N_{A}}{N_{D}}} \tag{1.51b}
\end{gather*}
$$

The validity of $(1.51)$ depends on $W_{B}^{2} / 2 \tau_{b} D_{n} \ll 1$ and $\left(D_{p} / D_{n}\right)\left(W_{B} / L_{p}\right)\left(N_{A} / N_{D}\right) \ll 1$, and this is always true if $\beta_{F}$ is large [see (1.48)]. The term $\gamma$ in (1.51) is called the emitter injection efficiency and is equal to the ratio of the electron current ( $n p n$ transistor) injected into the base from the emitter to the total hole and electron current crossing the base-emitter junction. Ideally $\gamma \rightarrow 1$, and this is achieved by making $N_{D} / N_{A}$ large and $W_{B}$ small. In that case very little reverse injection occurs from base to emitter.

The term $\alpha_{T}$ in (1.51) is called the base transport factor and represents the fraction of carriers injected into the base (from the emitter) that reach the collector. Ideally $\alpha_{T} \rightarrow 1$ and this is achieved by making $W_{B}$ small. It is evident from the above development that fabrication changes that cause $\alpha_{T}$ and $\gamma$ to approach unity also maximize the value of $\beta_{F}$ of the transistor.

The results derived above allow formulation of a large-signal model of the transistor suitable for bias-circuit calculations with devices in the forward-active region. One such circuit is shown in Fig. 1.7 and consists of a base-emitter diode to model (1.46) and a controlled collector-current generator to model (1.47). Note that the collector voltage ideally has no influence on the collector current and the collector node acts as a high-impedance current source. A simpler version of this equivalent circuit, which is often useful, is shown in Fig. $1.7 b$, where the input diode has been replaced by a battery with a value $V_{B E(\text { on })}$, which is usually 0.6 to 0.7 V . This represents the fact that in the forward-active region the base-emitter voltage varies very little because of the steep slope of the exponential characteristic. In some circuits the temperature coefficient of $V_{B E(\text { on })}$ is important, and a typical value for this is $-2 \mathrm{mV} /{ }^{\circ} \mathrm{C}$. The equivalent circuits of Fig. 1.7 apply for $n p n$ transistors. For $p n p$ devices the corresponding equivalent circuits are shown in Fig. 1.8.
image_name:Figure 1.7 (a)
description:
[
name: V_BE, type: VoltageSource, value: V_BE, ports: {Np: B, Nn: E}
name: Diode, type: Diode, ports: {Na: B, Nc: E}
name: β_F I_B, type: CurrentControlledCurrentSource, value: β_F I_B, ports: {Np: C, Nn: E}
]
extrainfo:The circuit is a large-signal model of an NPN transistor for bias calculations, incorporating an input diode.
image_name:Figure 1.7 (b)
description:
[
name: V_BE(on), type: VoltageSource, value: V_BE(on), ports: {Np: B, Nn: E}
name: β_FI_B, type: CurrentControlledCurrentSource, ports: {Np: C, Nn: E}
]
extrainfo:The circuit represents a large-signal model of an npn transistor for bias calculations, incorporating a voltage source V_BE(on) and a current-controlled current source β_FI_B.

$$
I_{B}=\frac{I_{S}}{\beta_{F}} \exp \frac{V_{B E}}{V_{T}}
$$

(a)

Figure 1.7 Large-signal models of npn transistors for use in bias calculations. (a) Circuit incorporating an input diode.
(b) Simplified circuit with an input voltage source.
image_name:(a)
description:
[
name: V_BE, type: VoltageSource, value: V_BE, ports: {Np: B, Nn: E}
name: Diode, type: Diode, ports: {Na: B, Nc: E}
name: β_F I_B, type: CurrentControlledCurrentSource, value: β_F I_B, ports: {Np: C, Nn: E}
]
extrainfo:The circuit (a) represents a large-signal model of an npn transistor for bias calculations, incorporating a voltage source V_BE and a current-controlled current source β_FI_B. The equation I_B = (I_S/β_F) * exp(V_BE/V_T) describes the base current I_B in terms of the saturation current I_S, the forward current gain β_F, the base-emitter voltage V_BE, and the thermal voltage V_T.
image_name:(b)
description:
[
name: V_BE(on), type: VoltageSource, value: V_BE(on), ports: {Np: E, Nn: B}
name: CurrentSource, type: β_F I_B, value: β_F I_B, ports: {Np: C, Nn: E}
]
extrainfo:The circuit represents a large-signal model of an npn transistor for bias calculations, incorporating a voltage source V_BE(on) and a current-controlled current source β_FI_B. This model simplifies the analysis of transistor biasing by replacing the input diode with an input voltage source.

Figure 1.8 Large-signal models of pnp transistors corresponding to the circuits of Fig. 1.7.

### 1.3.2 Effects of Collector Voltage on Large-Signal Characteristics in the Forward-Active Region

In the analysis of the previous section, the collector-base junction was assumed reverse biased and ideally had no effect on the collector currents. This is a useful approximation for firstorder calculations, but is not strictly true in practice. There are occasions when the influence of collector voltage on collector current is important, and this will now be investigated.

The collector voltage has a dramatic effect on the collector current in two regions of device operation. These are the saturation ( $V_{C E}$ approaches zero) and breakdown ( $V_{C E}$ very large) regions that will be considered later. For values of collector-emitter voltage $V_{C E}$ between these extremes, the collector current increases slowly as $V_{C E}$ increases. The reason for this can be seen from Fig. 1.9, which is a sketch of the minority-carrier concentration in the base of the transistor. Consider the effect of changes in $V_{C E}$ on the carrier concentration for constant $V_{B E}$. Since $V_{B E}$ is constant, the change in $V_{C B}$ equals the change in $V_{C E}$ and this causes an increase in the collector-base depletion-layer width as shown. The change in the base width of the transistor, $\Delta W_{B}$, equals the change in the depletion-layer width and causes an increase $\Delta I_{C}$ in the collector current.

From (1.35) and (1.38) we have

$$
\begin{equation*}
I_{C}=\frac{q A \bar{D}_{n} n_{i}^{2}}{Q_{B}} \exp \frac{V_{B E}}{V_{T}} \tag{1.52}
\end{equation*}
$$

image_name:Figure 1.9
description:This graph is a schematic representation of the carrier concentration across a bipolar transistor, specifically illustrating the effects of an increase in the collector-emitter voltage, \( V_{CE} \).

Type of Graph and Function:
- The graph is a conceptual diagram, not a numerical plot, showing the relationship between carrier concentration and position across the transistor structure.

Axes Labels and Units:
- The vertical axis represents "Carrier concentration," but no specific units are provided as this is a qualitative diagram.
- The horizontal axis is labeled with positions across the transistor: "Emitter," "Base," and "Collector."

Overall Behavior and Trends:
- The graph illustrates how an increase in \( V_{CE} \) causes the collector depletion region to widen, which is shown by the shift of the rightmost dashed line further to the right.
- The initial depletion region is marked, and the increase in depletion width is indicated by \( \Delta W_B \).

Key Features and Technical Details:
- The carrier concentration at the base-emitter junction is given by \( n_p(0) = n_{po} \exp\left(\frac{V_{BE}}{V_T}\right) \), indicating an exponential relationship dependent on the base-emitter voltage \( V_{BE} \).
- The diagram shows two current paths: \( I_C \) and \( I_C + \Delta I_C \), illustrating an increase in collector current due to the change in the base width \( \Delta W_B \).
- The slope of the carrier concentration decreases as it moves from the emitter to the collector, reflecting the gradient in carrier concentration.

Annotations and Specific Data Points:
- The diagram includes annotations such as "Collector depletion region widens due to \( \Delta V_{CE} \)" and "Initial depletion region," highlighting the effects of voltage changes on the transistor's physical structure.
- The base width \( W_B \) and its change \( \Delta W_B \) are clearly marked, showing the impact of \( V_{CE} \) on the transistor's operation.

Overall, the diagram effectively conveys how an increase in \( V_{CE} \) affects the depletion region and carrier concentration within a bipolar transistor, leading to changes in collector current.

Figure 1.9 Effect of increases in $V_{C E}$ on the collector depletion region and base width of a bipolar transistor.

Differentiation of (1.52) yields

$$
\begin{equation*}
\frac{\partial I_{C}}{\partial V_{C E}}=-\frac{q A \bar{D}_{n} n_{i}^{2}}{Q_{B}^{2}}\left(\exp \frac{V_{B E}}{V_{T}}\right) \frac{d Q_{B}}{d V_{C E}} \tag{1.53}
\end{equation*}
$$

and substitution of (1.52) in (1.53) gives

$$
\begin{equation*}
\frac{\partial I_{C}}{\partial V_{C E}}=-\frac{I_{C}}{Q_{B}} \frac{d Q_{B}}{d V_{C E}} \tag{1.54}
\end{equation*}
$$

For a uniform-base transistor $Q_{B}=W_{B} N_{A}$, and (1.54) becomes

$$
\begin{equation*}
\frac{\partial I_{C}}{\partial V_{C E}}=-\frac{I_{C}}{W_{B}} \frac{d W_{B}}{d V_{C E}} \tag{1.55}
\end{equation*}
$$

Note that since the base width decreases as $V_{C E}$ increases, $d W_{B} / d V_{C E}$ in (1.55) is negative and thus $\partial I_{C} / \partial V_{C E}$ is positive. The magnitude of $d W_{B} / d V_{C E}$ can be calculated from (1.18) for a uniform-base transistor. This equation predicts that $d W_{B} / d V_{C E}$ is a function of the bias value of $V_{C E}$, but the variation is typically small for a reverse-biased junction and $d W_{B} / d V_{C E}$ is often assumed constant. The resulting predictions agree adequately with experimental results.

Equation 1.55 shows that $\partial I_{C} / \partial V_{C E}$ is proportional to the collector-bias current and inversely proportional to the transistor base width. Thus narrow-base transistors show a greater dependence of $I_{C}$ on $V_{C E}$ in the forward-active region. The dependence of $\partial I_{C} / \partial V_{C E}$ on $I_{C}$ results in typical transistor output characteristics as shown in Fig. 1.10. In accordance with the assumptions made in the foregoing analysis, these characteristics are shown for constant values of $V_{B E}$. However, in most integrated-circuit transistors the base current is dependent only on $V_{B E}$ and not on $V_{C E}$, and thus constant-base-current characteristics can often be used in the following calculation. The reason for this is that the base current is usually dominated by the $I_{B 2}$ component of (1.45), which has no dependence on $V_{C E}$. Extrapolation of the characteristics of Fig. 1.10 back to the $V_{C E}$ axis gives an intercept $V_{A}$ called the Early voltage, where

$$
\begin{equation*}
V_{A}=\frac{I_{C}}{\frac{\partial I_{C}}{\partial V_{C E}}} \tag{1.56}
\end{equation*}
$$

image_name:Figure 1.10
description:The graph in Figure 1.10 is a bipolar transistor output characteristic plot, illustrating the Early effect.

1. **Type of Graph and Function:**
- This is an output characteristic graph for a bipolar junction transistor (BJT).

2. **Axes Labels and Units:**
- The x-axis is labeled $V_{CE}$, representing the collector-emitter voltage.
- The y-axis is labeled $I_C$, representing the collector current.
- Both axes likely use linear scales, though the units are not explicitly marked.

3. **Overall Behavior and Trends:**
- The graph shows several curves representing different base-emitter voltages ($V_{BE1}$, $V_{BE2}$, $V_{BE3}$, $V_{BE4}$).
- Each curve starts at a low $I_C$ value and increases with $V_{CE}$, showing a slight upward curve before becoming nearly linear.
- The curves extrapolate back to intersect at a common point on the $V_{CE}$ axis, indicating the Early voltage ($V_A$).

4. **Key Features and Technical Details:**
- The Early voltage ($V_A$) is marked on the $V_{CE}$ axis, representing the intercept point of the extrapolated linear portions of the curves.
- The curves show that as $V_{BE}$ increases, the $I_C$ for a given $V_{CE}$ also increases.
- The dashed lines represent the extrapolated portions of the curves, illustrating how all characteristics converge to the Early voltage.

5. **Annotations and Specific Data Points:**
- The curves are labeled with different $V_{BE}$ values, indicating different operating conditions for the transistor.
- The Early voltage ($V_A$) is a critical parameter, as it is used to describe the variation of $I_C$ with $V_{CE}$, known as the Early effect.

This graph is crucial for understanding how the collector current behaves with changes in the collector-emitter voltage and base-emitter voltage, and it is used to determine the Early voltage, a key parameter in transistor modeling.

Figure 1.10 Bipolar transistor output characteristics showing the Earlyvoltage, $V_{A}$.

Substitution of (1.55) in (1.56) gives

$$
\begin{equation*}
V_{A}=-W_{B} \frac{d V_{C E}}{d W_{B}} \tag{1.57}
\end{equation*}
$$

which is a constant, independent of $I_{C}$. Thus all the characteristics extrapolate to the same point on the $V_{C E}$ axis. The variation of $I_{C}$ with $V_{C E}$ is called the Early effect, and $V_{A}$ is a common model parameter for circuit-analysis computer programs. Typical values of $V_{A}$ for integrated-circuit transistors are 15 to 100 V . The inclusion of Early effect in dc bias calculations is usually limited to computer analysis because of the complexity introduced into the calculation. However, the influence of the Early effect is often dominant in small-signal calculations for high-gain circuits and this point will be considered later.

Finally, the influence of Early effect on the transistor large-signal characteristics in the forward-active region can be represented approximately by modifying (1.35) to

$$
\begin{equation*}
I_{C}=I_{S}\left(1+\frac{V_{C E}}{V_{A}}\right) \exp \frac{V_{B E}}{V_{T}} \tag{1.58}
\end{equation*}
$$

This is a common means of representing the device output characteristics for computer simulation.

### 1.3.3 Saturation and Inverse-Active Regions

Saturation is a region of device operation that is usually avoided in analog circuits because the transistor gain is very low in this region. Saturation is much more commonly encountered in digital circuits, where it provides a well-specified output voltage that represents a logic state.

In saturation, both emitter-base and collector-base junctions are forward biased. Consequently, the collector-emitter voltage $V_{C E}$ is quite small and is usually in the range 0.05 to 0.3 V . The carrier concentrations in a saturated $n p n$ transistor with uniform base doping are shown in Fig. 1.11. The minority-carrier concentration in the base at the edge of the depletion region is again given by (1.28) as

$$
\begin{equation*}
n_{p}\left(W_{B}\right)=n_{p o} \exp \frac{V_{B C}}{V_{T}} \tag{1.59}
\end{equation*}
$$

image_name:Figure 1.11
description:The graph in Figure 1.11 illustrates the carrier concentration profiles in a saturated npn transistor. It is a spatial distribution graph that shows how the carrier concentration varies across different regions of the transistor: the emitter, base, and collector.

1. **Type of Graph and Function:**
- The graph is a spatial distribution plot, illustrating carrier concentrations.

2. **Axes Labels and Units:**
- The horizontal axis is labeled 'x', representing the position within the transistor, moving from the emitter through the base to the collector.
- The vertical axis represents the carrier concentration, though specific units are not provided.

3. **Overall Behavior and Trends:**
- In the emitter region, the graph shows high concentrations of electrons \(n_{nE}\) and holes \(p_{nE}\), with sharp declines as they approach the base.
- Within the base, the minority-carrier concentration \(n_p(x)\) decreases linearly from \(n_p(0)\) at the emitter-base junction to \(n_p(W_B)\) at the base-collector junction.
- The majority-carrier concentration \(p_p(x)\) is also shown, decreasing linearly across the base.
- Two other profiles, \(n_{p1}(x)\) and \(n_{p2}(x)\), intersect within the base, indicating changes in carrier distribution.
- In the collector region, the concentrations of electrons \(n_{nC}\) and holes \(p_{nC}\) are shown to decrease exponentially.

4. **Key Features and Technical Details:**
- The graph indicates the direction of the collector current \(I_C\) across the base.
- The width of the base \(W_B\) is marked, showing the region where the carrier concentrations are plotted.

5. **Annotations and Specific Data Points:**
- The graph is annotated with specific points such as \(n_p(0)\) and \(n_p(W_B)\), marking the minority-carrier concentration at the edges of the base.
- The intersection of \(n_{p1}(x)\) and \(n_{p2}(x)\) within the base is also highlighted, indicating a shift in carrier concentration dynamics.

Figure 1.11 Carrier concentrations in a saturated npn transistor. (Not to scale.)
image_name:Figure 1.12
description:The graph in Figure 1.12 is a plot of the collector current \(I_C\) in milliamperes (mA) against the collector-emitter voltage \(V_{CE}\) in volts for an npn bipolar transistor. The graph illustrates the typical \(I_C-V_{CE}\) characteristics, showing distinct regions of operation: saturation, forward active, and inverse active.

**Axes Labels and Units:**
- The vertical axis represents the collector current \(I_C\) in milliamperes (mA).
- The horizontal axis represents the collector-emitter voltage \(V_{CE}\) in volts.
- The scales are linear for both axes.

**Overall Behavior and Trends:**
- **Forward Active Region:** As \(V_{CE}\) increases from 0 to about 30 volts, \(I_C\) increases linearly for each base current \(I_B\) level, indicating the forward active region. This region is between the saturation region and the breakdown voltage \(BV_{CEO}\).
- **Saturation Region:** For low \(V_{CE}\) values near zero, the curves flatten, indicating the saturation region where the transistor is fully on.
- **Inverse Active Region:** When \(V_{CE}\) is negative, \(I_C\) becomes negative, showing the inverse active region.

**Key Features and Technical Details:**
- The curves are plotted for different base currents \(I_B\) ranging from 0 to 0.04 mA.
- The forward active region shows a linear increase in \(I_C\) with increasing \(V_{CE}\) for each \(I_B\).
- The breakdown voltage \(BV_{CEO}\) is marked near 40 volts, beyond which the curves rise steeply.
- In the inverse active region, \(I_C\) decreases with increasing negative \(V_{CE}\), showing a similar pattern for different \(I_B\) values.

**Annotations and Specific Data Points:**
- The graph is annotated with the base current values \(I_B = 0, 0.01, 0.02, 0.03, 0.04\) mA.
- The saturation region is labeled around \(V_{CE} = 0\) volts.
- The forward active region is highlighted as the area between saturation and \(BV_{CEO}\).
- The inverse active region is indicated for negative \(V_{CE}\) values.

Figure 1.12 Typical $I_{C}-V_{C E}$ characteristics for an npn bipolar transistor. Note the different scales for positive and negative currents and voltages.
but since $V_{B C}$ is now positive, the value of $n_{p}\left(W_{B}\right)$ is no longer negligible. Consequently, changes in $V_{C E}$ with $V_{B E}$ held constant (which cause equal changes in $V_{B C}$ ) directly affect $n_{p}\left(W_{B}\right)$. Since the collector current is proportional to the slope of the minority-carrier concentration in the base [see (1.31)], it is also proportional to $\left[n_{p}(0)-n_{p}\left(W_{B}\right)\right]$ from Fig. 1.11. Thus changes in $n_{p}\left(W_{B}\right)$ directly affect the collector current, and the collector node of the transistor appears to have a low impedance. As $V_{C E}$ is decreased in saturation with $V_{B E}$ held constant, $V_{B C}$ increases, as does $n_{p}\left(W_{B}\right)$ from (1.59). Thus, from Fig. 1.11, the collector current decreases because the slope of the carrier concentration decreases. This gives rise to the saturation region of the $I_{C}-V_{C E}$ characteristic shown in Fig. 1.12. The slope of the $I_{C}-V_{C E}$ characteristic in this region is largely determined by the resistance in series with the collector lead due to the finite resistivity of the $n$-type collector material. A useful model for the transistor in this region is shown in Fig. 1.13 and consists of a fixed voltage source to represent $V_{B E(\text { on })}$, and a fixed voltage source to represent the collector-emitter voltage $V_{C E(\text { sat })}$. A more accurate but more complex model includes a resistor in series with the collector. This resistor can have a value ranging from 20 to $500 \Omega$, depending on the device structure.

An additional aspect of transistor behavior in the saturation region is apparent from Fig. 1.11. For a given collector current, there is now a much larger amount of stored charge in the base than there is in the forward-active region. Thus the base-current contribution represented by (1.41) will be larger in saturation. In addition, since the collector-base junction is now forward biased, there is a new base-current component due to injection of carriers from the
image_name:(a) npn
description:The diagram shows large-signal models for bipolar transistors in the saturation region. It includes voltage drops V_BE(on) and V_CE(sat) for both NPN and PNP transistors. The NPN transistor is labeled as 'a' and the PNP transistor as 'b', with the nodes B, C, and E indicated for each.
image_name:(b) pnp
description:The circuit diagram shows a large-signal model for a PNP bipolar transistor in the saturation region, with voltages V_BE(on) and V_CE(sat) indicated.

Figure 1.13 Large-signal models for bipolar transistors in the saturation region.
base to the collector. These two effects result in a base current $I_{B}$ in saturation, which is larger than in the forward-active region for a given collector current $I_{C}$. Ratio $I_{C} / I_{B}$ in saturation is often referred to as the forced $\beta$ and is always less than $\beta_{F}$. As the forced $\beta$ is made lower with respect to $\beta_{F}$, the device is said to be more heavily saturated.

The minority-carrier concentration in saturation shown in Fig. 1.11 is a straight line joining the two end points, assuming that recombination is small. This can be represented as a linear superposition of the two dotted distributions as shown. The justification for this is that the terminal currents depend linearly on the concentrations $n_{p}(0)$ and $n_{p}\left(W_{B}\right)$. This picture of device carrier concentrations can be used to derive some general equations describing transistor behavior. Each of the distributions in Fig. 1.11 is considered separately and the two contributions are combined. The emitter current that would result from $n_{p 1}(x)$ above is given by the classical diode equation

$$
\begin{equation*}
I_{E F}=-I_{E S}\left(\exp \frac{V_{B E}}{V_{T}}-1\right) \tag{1.60}
\end{equation*}
$$

where $I_{E S}$ is a constant that is often referred to as the saturation current of the junction (no connection with the transistor saturation previously described). Equation 1.60 predicts that the junction current is given by $I_{E F} \simeq I_{E S}$ with a reverse-bias voltage applied. However, in practice (1.60) is applicable only in the forward-bias region, since second-order effects dominate under reverse-bias conditions and typically result in a junction current several orders of magnitude larger than $I_{E S}$. The junction current that flows under reverse-bias conditions is often called the leakage current of the junction.

Returning to Fig. 1.11, we can describe the collector current resulting from $n_{p 2}(x)$ alone as

$$
\begin{equation*}
I_{C R}=-I_{C S}\left(\exp \frac{V_{B C}}{V_{T}}-1\right) \tag{1.61}
\end{equation*}
$$

where $I_{C S}$ is a constant. The total collector current $I_{C}$ is given by $I_{C R}$ plus the fraction of $I_{E F}$ that reaches the collector (allowing for recombination and reverse emitter injection). Thus

$$
\begin{equation*}
I_{C}=\alpha_{F} I_{E S}\left(\exp \frac{V_{B E}}{V_{T}}-1\right)-I_{C S}\left(\exp \frac{V_{B C}}{V_{T}}-1\right) \tag{1.62}
\end{equation*}
$$

where $\alpha_{F}$ has been defined previously by (1.51). Similarly, the total emitter current is composed of $I_{E F}$ plus the fraction of $I_{C R}$ that reaches the emitter with the transistor acting in an inverted mode. Thus

$$
\begin{equation*}
I_{E}=-I_{E S}\left(\exp \frac{V_{B E}}{V_{T}}-1\right)+\alpha_{R} I_{C S}\left(\exp \frac{V_{B C}}{V_{T}}-1\right) \tag{1.63}
\end{equation*}
$$

where $\alpha_{R}$ is the ratio of emitter to collector current with the transistor operating inverted (i.e., with the collector-base junction forward biased and emitting carriers into the base and the emitter-base junction reverse biased and collecting carriers). Typical values of $\alpha_{R}$ are 0.5 to 0.8 .

An inverse current gain $\beta_{R}$ is also defined

$$
\begin{equation*}
\beta_{R}=\frac{\alpha_{R}}{1-\alpha_{R}} \tag{1.64}
\end{equation*}
$$

and has typical values 1 to 5 . This is the current gain of the transistor when operated inverted and is much lower than $\beta_{F}$ because the device geometry and doping densities are designed to maximize $\beta_{F}$. The inverse-active region of device operation occurs for $V_{C E}$ negative in an $n p n$ transistor and is shown in Fig. 1.12. In order to display these characteristics adequately in the same figure as the forward-active region, the negative voltage and current scales have been expanded. The inverse-active mode of operation is rarely encountered in analog circuits.

Equations 1.62 and 1.63 describe npn transistor operation in the saturation region when $V_{B E}$ and $V_{B C}$ are both positive, and also in the forward-active and inverse-active regions. These equations are the Ebers-Moll equations. In the forward-active region, they degenerate into a form similar to that of (1.35), (1.47), and (1.49) derived earlier. This can be shown by putting $V_{B E}$ positive and $V_{B C}$ negative in (1.62) and (1.63) to obtain

$$
\begin{align*}
I_{C} & =\alpha_{F} I_{E S}\left(\exp \frac{V_{B E}}{V_{T}}-1\right)+I_{C S}  \tag{1.65}\\
I_{E} & =-I_{E S}\left(\exp \frac{V_{B E}}{V_{T}}-1\right)-\alpha_{R} I_{C S} \tag{1.66}
\end{align*}
$$

Equation 1.65 is similar in form to (1.35) except that leakage currents that were previously neglected have now been included. This minor difference is significant only at high temperatures or very low operating currents. Comparison of (1.65) with (1.35) allows us to identify $I_{S}=\alpha_{F} I_{E S}$, and it can be shown ${ }^{10}$ in general that

$$
\begin{equation*}
\alpha_{F} I_{E S}=\alpha_{R} I_{C S}=I_{S} \tag{1.67}
\end{equation*}
$$

where this expression represents a reciprocity condition. Use of (1.67) in (1.62) and (1.63) allows the Ebers-Moll equations to be expressed in the general form

$$
\begin{align*}
I_{C} & =I_{S}\left(\exp \frac{V_{B E}}{V_{T}}-1\right)-\frac{I_{S}}{\alpha_{R}}\left(\exp \frac{V_{B C}}{V_{T}}-1\right)  \tag{1.62a}\\
I_{E} & =-\frac{I_{S}}{\alpha_{F}}\left(\exp \frac{V_{B E}}{V_{T}}-1\right)+I_{S}\left(\exp \frac{V_{B C}}{V_{T}}-1\right) \tag{1.63a}
\end{align*}
$$

This form is often used for computer representation of transistor large-signal behavior.
The effect of leakage currents mentioned above can be further illustrated as follows. In the forward-active region, from (1.66)

$$
\begin{equation*}
I_{E S}\left(\exp \frac{V_{B E}}{V_{T}}-1\right)=-I_{E}-\alpha_{R} I_{C S} \tag{1.68}
\end{equation*}
$$

Substitution of (1.68) in (1.65) gives

$$
\begin{equation*}
I_{C}=-\alpha_{F} I_{E}+I_{C O} \tag{1.69}
\end{equation*}
$$

where

$$
\begin{equation*}
I_{C O}=I_{C S}\left(1-\alpha_{R} \alpha_{F}\right) \tag{1.69a}
\end{equation*}
$$

and $I_{C O}$ is the collector-base leakage current with the emitter open. Although $I_{C O}$ is given theoretically by (1.69a), in practice, surface leakage effects dominate when the collector-base junction is reverse biased and $I_{C O}$ is typically several orders of magnitude larger than the value
given by (1.69a). However, (1.69) is still valid if the appropriate measured value for $I_{C O}$ is used. Typical values of $I_{C O}$ are from $10^{-10}$ to $10^{-12} \mathrm{~A}$ at $25^{\circ} \mathrm{C}$, and the magnitude doubles about every $8^{\circ} \mathrm{C}$. As a consequence, these leakage terms can become very significant at high temperatures. For example, consider the base current $I_{B}$. From Fig. 1.5 this is

$$
\begin{equation*}
I_{B}=-\left(I_{C}+I_{E}\right) \tag{1.70}
\end{equation*}
$$

If $I_{E}$ is calculated from (1.69) and substituted in (1.70), the result is

$$
\begin{equation*}
I_{B}=\frac{1-\alpha_{F}}{\alpha_{F}} I_{C}-\frac{I_{C O}}{\alpha_{F}} \tag{1.71}
\end{equation*}
$$

But from (1.50)

$$
\begin{equation*}
\beta_{F}=\frac{\alpha_{F}}{1-\alpha_{F}} \tag{1.72}
\end{equation*}
$$

and use of (1.72) in (1.71) gives

$$
\begin{equation*}
I_{B}=\frac{I_{C}}{\beta_{F}}-\frac{I_{C O}}{\alpha_{F}} \tag{1.73}
\end{equation*}
$$

Since the two terms in (1.73) have opposite signs, the effect of $I_{C O}$ is to decrease the magnitude of the external base current at a given value of collector current.

#### EXAMPLE

If $I_{C O}$ is $10^{-10} \mathrm{~A}$ at $24^{\circ} \mathrm{C}$, estimate its value at $120^{\circ} \mathrm{C}$.
Assuming that $I_{C O}$ doubles every $8^{\circ} \mathrm{C}$, we have

$$
\begin{aligned}
I_{C O}\left(120^{\circ} \mathrm{C}\right) & =10^{-10} \times 2^{12} \\
& =0.4 \mu \mathrm{~A}
\end{aligned}
$$

### 1.3.4 Transistor Breakdown Voltages

In Section 1.2.2 the mechanism of avalanche breakdown in a pn junction was described. Similar effects occur at the base-emitter and base-collector junctions of a transistor and these effects limit the maximum voltages that can be applied to the device.

First consider a transistor in the common-base configuration shown in Fig. 1.14a and supplied with a constant emitter current. Typical $I_{C}-V_{C B}$ characteristics for an npn transistor in such a connection are shown in Fig. 1.14b. For $I_{E}=0$ the collector-base junction breaks down at a voltage $B V_{C B O}$, which represents collector-base breakdown with the emitter open. For finite values of $I_{E}$, the effects of avalanche multiplication are apparent for values of $V_{C B}$ below $B V_{C B O}$. In the example shown, the effective common-base current gain $\alpha_{F}=I_{C} / I_{E}$ becomes larger than unity for values of $V_{C B}$ above about 60 V . Operation in this region (but below $B V_{C B O}$ ) can, however, be safely undertaken if the device power dissipation is not excessive. The considerations of Section 1.2.2 apply to this situation, and neglecting leakage currents, we can calculate the collector current in Fig. 1.14a as

$$
\begin{equation*}
I_{C}=-\alpha_{F} I_{E} M \tag{1.74}
\end{equation*}
$$

where $M$ is defined by (1.26) and thus

$$
\begin{equation*}
I_{C}=-\alpha_{F} I_{E} \frac{1}{1-\left(\frac{V_{C B}}{B V_{C B O}}\right)^{n}} \tag{1.75}
\end{equation*}
$$

image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: VCB, B: GND, E: e1}
name: IE, type: CurrentSource, value: IE, ports: {Np: e1, Nn: GND}
name: VCB, type: VoltageSource, value: VCB, ports: {Np: VCB, Nn: GND}
]
extrainfo:The circuit diagram represents a common-base configuration of an NPN transistor. The collector current IC is controlled by the emitter current IE and the voltage VCB. The graph shows the IC-V_CB characteristics for different values of IE, illustrating minimal Early effect at low VCB values.
image_name:(b)
description:The graph depicted in Figure 1.14b is a characteristic curve of a common-base transistor configuration, illustrating the relationship between the collector current (I_C) and the collector-base voltage (V_CB). This is a type of I-V characteristic curve commonly used in transistor analysis.

1. **Type of Graph and Function:**
- The graph is an I-V characteristic curve for a transistor in a common-base configuration.

2. **Axes Labels and Units:**
- The horizontal axis represents the collector-base voltage (V_CB) in volts.
- The vertical axis represents the collector current (I_C) in milliamperes (mA).
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The curves show the collector current I_C for different emitter currents (I_E = 0.5 mA, 1.0 mA, and 1.5 mA) as a function of V_CB.
- For low values of V_CB, the collector current remains relatively constant, indicating a flat region.
- As V_CB increases, there is a slight upward curvature in the I_C, which becomes more pronounced as V_CB approaches the breakdown voltage (BV_CBO).

4. **Key Features and Technical Details:**
- The graph shows three distinct curves corresponding to different emitter currents (I_E = 0.5 mA, 1.0 mA, and 1.5 mA).
- Each curve starts at a point on the vertical axis corresponding to its respective I_E value.
- The breakdown voltage (BV_CBO) is marked on the V_CB axis at approximately 100 volts, beyond which the avalanche effect becomes significant.
- The Early effect is minimal in this configuration for low V_CB values.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for I_E values on each curve.
- A dashed vertical line marks the breakdown voltage (BV_CBO) at 100 volts, indicating the limit where the transistor may enter an avalanche breakdown region.
- The curves are labeled with the corresponding I_E values, providing a clear reference for the different operating conditions.

Figure 1.14 Common-base transistor connection. (a) Test circuit. (b) $I_{C}-V_{C B}$ characteristics.

One further point to note about the common-base characteristics of Fig. 1.14b is that for low values of $V_{C B}$ where avalanche effects are negligible, the curves show very little of the Early effect seen in the common-emitter characteristics. Base widening still occurs in this configuration as $V_{C B}$ is increased, but unlike the common-emitter connection, it produces little change in $I_{C}$. This is because $I_{E}$ is now fixed instead of $V_{B E}$ or $I_{B}$, and in Fig. 1.9, this means the slope of the minority-carrier concentration at the emitter edge of the base is fixed. Thus the collector current remains almost unchanged.

Now consider the effect of avalanche breakdown on the common-emitter characteristics of the device. Typical characteristics are shown in Fig. 1.12, and breakdown occurs at a value $B V_{C E O}$, which is sometimes called the sustaining voltage $L V_{C E O}$. As in previous cases, operation near the breakdown voltage is destructive to the device only if the current (and thus the power dissipation) becomes excessive.

The effects of avalanche breakdown on the common-emitter characteristics are more complex than in the common-base configuration. This is because hole-electron pairs are produced by the avalanche process and the holes are swept into the base, where they effectively contribute to the base current. In a sense, the avalanche current is then amplified by the transistor. The base current is still given by

$$
\begin{equation*}
I_{B}=-\left(I_{C}+I_{E}\right) \tag{1.76}
\end{equation*}
$$

Equation 1.74 still holds, and substitution of this in (1.76) gives

$$
\begin{equation*}
I_{C}=\frac{M \alpha_{F}}{1-M \alpha_{F}} I_{B} \tag{1.77}
\end{equation*}
$$

where

$$
\begin{equation*}
M=\frac{1}{1-\left(\frac{V_{C B}}{B V_{C B O}}\right)^{n}} \tag{1.78}
\end{equation*}
$$

Equation 1.77 shows that $I_{C}$ approaches infinity as $M \alpha_{F}$ approaches unity. That is, the effective $\beta$ approaches infinity because of the additional base-current contribution from the avalanche process itself. The value of $B V_{C E O}$ can be determined by solving

$$
\begin{equation*}
M \alpha_{F}=1 \tag{1.79}
\end{equation*}
$$

If we assume that $V_{C B} \simeq V_{C E}$, this gives

$$
\begin{equation*}
\frac{\alpha_{F}}{1-\left(\frac{B V_{C E O}}{B V_{C B O}}\right)^{n}}=1 \tag{1.80}
\end{equation*}
$$

and this results in

$$
\frac{B V_{C E O}}{B V_{C B O}}=\sqrt[n]{1-\alpha_{F}}
$$

and thus

$$
\begin{equation*}
B V_{C E O} \simeq \frac{B V_{C B O}}{\sqrt[n]{\beta_{F}}} \tag{1.81}
\end{equation*}
$$

Equation 1.81 shows that $B V_{C E O}$ is less than $B V_{C B O}$ by a substantial factor. However, the value of $B V_{C B O}$, which must be used in (1.81), is the plane junction breakdown of the collector-base junction, neglecting any edge effects. This is because it is only collector-base avalanche current actually under the emitter that is amplified as described in the previous calculation. However, as explained in Section 1.2.2, the measured value of $B V_{C B O}$ is usually determined by avalanche in the curved region of the collector, which is remote from the active base. Consequently, for typical values of $\beta_{F}=100$ and $n=4$, the value of $B V_{C E O}$ is about one-half of the measured $B V_{C B O}$ and not 30 percent as (1.81) would indicate.

Equation 1.81 explains the shape of the breakdown characteristics of Fig. 1.12 if the dependence of $\beta_{F}$ on collector current is included. As $V_{C E}$ is increased from zero with $I_{B}=0$, the initial collector current is approximately $\beta_{F} I_{C O}$ from (1.73); since $I_{C O}$ is typically several picoamperes, the collector current is very small. As explained in the next section, $\beta_{F}$ is small at low currents, and thus from (1.81) the breakdown voltage is high. However, as avalanche breakdown begins in the device, the value of $I_{C}$ increases and thus $\beta_{F}$ increases. From (1.81) this causes a decrease in the breakdown voltage and the characteristic bends back as shown in Fig. 1.12 and exhibits a negative slope. At higher collector currents, $\beta_{F}$ approaches a constant value and the breakdown curve with $I_{B}=0$ becomes perpendicular to the $V_{C E}$ axis. The value of $V_{C E}$ in this region of the curve is usually defined to be $B V_{C E O}$, since this is the maximum voltage the device can sustain. The value of $\beta_{F}$ to be used to calculate $B V_{C E O}$ in (1.81) is thus the peak value of $\beta_{F}$. Note from (1.81) that high- $\beta$ transistors will thus have low values of $B V_{C E O}$.

The base-emitter junction of a transistor is also subject to avalanche breakdown. However, the doping density in the emitter is made very large to ensure a high value of $\beta_{F}\left[N_{D}\right.$ is made large in $(1.45)$ to reduce $\left.I_{B 2}\right]$. Thus the base is the more lightly doped side of the junction and determines the breakdown characteristic. This can be contrasted with the collector-base junction, where the collector is the more lightly doped side and results in typical values of $B V_{C B O}$ of 20 to 80 V or more. The base is typically an order of magnitude more heavily doped than the collector, and thus the base-emitter breakdown voltage is much less than $B V_{C B O}$ and is typically about 6 to 8 V . This is designated $B V_{E B O}$. The breakdown voltage for inverse-active operation shown in Fig. 1.12 is approximately equal to this value because the base-emitter junction is reverse biased in this mode of operation.

The base-emitter breakdown voltage of 6 to 8 V provides a convenient reference voltage in integrated-circuit design, and this is often utilized in the form of a Zener diode. However,
care must be taken to ensure that all other transistors in a circuit are protected against reverse base-emitter voltages sufficient to cause breakdown. This is because, unlike collector-base breakdown, base-emitter breakdown is damaging to the device. It can cause a large degradation in $\beta_{F}$, depending on the duration of the breakdown-current flow and its magnitude. ${ }^{11}$ If the device is used purely as a Zener diode, this is of no consequence, but if the device is an amplifying transistor, the $\beta_{F}$ degradation may be serious.

#### EXAMPLE

If the collector doping density in a transistor is $2 \times 10^{15} \mathrm{atoms} / \mathrm{cm}^{3}$ and is much less than the base doping, calculate $B V_{C E O}$ for $\beta=100$ and $n=4$. Assume $\mathscr{E}_{\text {crit }}=3 \times 10^{5} \mathrm{~V} / \mathrm{cm}$.

The plane breakdown voltage in the collector can be calculated from (1.24) using $\mathscr{E}_{\max }=\mathscr{E}_{\text {crit }}:$

$$
B V_{C B O}=\frac{\epsilon\left(N_{A}+N_{D}\right)}{2 q N_{A} N_{D}} \mathscr{E}_{\text {crit }}^{2}
$$

Since $N_{D} \ll N_{A}$, we have

$$
\left.B V_{C B O}\right|_{\text {plane }}=\frac{\epsilon}{2 q N_{D}} \mathscr{E}_{\text {crit }}^{2}=\frac{1.04 \times 10^{-12}}{2 \times 1.6 \times 10^{-19} \times 2 \times 10^{15}} \times 9 \times 10^{10} \mathrm{~V}=146 \mathrm{~V}
$$

From (1.81)

$$
B V_{C E O}=\frac{146}{\sqrt[4]{100}} \mathrm{~V}=46 \mathrm{~V}
$$

### 1.3.5 Dependence of Transistor Current Gain $\beta_{F}$ on Operating Conditions

Although most first-order analyses of integrated circuits make the assumption that $\beta_{F}$ is constant, this parameter does in fact depend on the operating conditions of the transistor. It was shown in Section 1.3.2, for example, that increasing the value of $V_{C E}$ increases $I_{C}$ while producing little change in $I_{B}$, and thus the effective $\beta_{F}$ of the transistor increases. In Section 1.3.4 it was shown that as $V_{C E}$ approaches the breakdown voltage, $B V_{C E O}$, the collector current increases due to avalanche multiplication in the collector. Equation 1.77 shows that the effective current gain approaches infinity as $V_{C E}$ approaches $B V_{C E O}$.

In addition to the effects just described, $\beta_{F}$ also varies with both temperature and transistor collector current. This is illustrated in Fig. 1.15, which shows typical curves of $\beta_{F}$ versus $I_{C}$ at three different temperatures for an npn integrated circuit transistor. It is evident that $\beta_{F}$ increases as temperature increases, and a typical temperature coefficient for $\beta_{F}$ is $+7000 \mathrm{ppm} /{ }^{\circ} \mathrm{C}$ (where ppm signifies parts per million). This temperature dependence of $\beta_{F}$ is due to the effect of the extremely high doping density in the emitter, ${ }^{12}$ which causes the emitter injection efficiency $\gamma$ to increase with temperature.

The variation of $\beta_{F}$ with collector current, which is apparent in Fig. 1.15, can be divided into three regions. Region I is the low-current region, where $\beta_{F}$ decreases as $I_{C}$ decreases. Region II is the midcurrent region, where $\beta_{F}$ is approximately constant. Region III is the highcurrent region, where $\beta_{F}$ decreases as $I_{C}$ increases. The reasons for this behavior of $\beta_{F}$ with $I_{C}$ can be better appreciated by plotting base current $I_{B}$ and collector current $I_{C}$ on a $\log$ scale
image_name:Figure 1.15
description:Figure 1.15 is a graph depicting the relationship between the forward current gain (β_F) and the collector current (I_C) for an npn integrated-circuit transistor with a 6 μm² emitter area. The graph is plotted on a logarithmic scale for the x-axis, representing the collector current (I_C) in microamperes (μA) and milliamperes (mA), ranging from 0.1 μA to 10 mA. The y-axis represents the forward current gain (β_F), ranging from 0 to 400, on a linear scale.

The graph is divided into three distinct regions:

1. **Region I (Low-Current Region):** In this region, β_F decreases as I_C decreases. This is observed at the lower end of the I_C scale.
2. **Region II (Mid-Current Region):** Here, β_F remains approximately constant over a range of I_C values. This region represents the ideal behavior of the transistor.
3. **Region III (High-Current Region):** In this region, β_F decreases as I_C increases, which is apparent at the higher end of the I_C scale.

Three curves are plotted on the graph, each representing a different temperature: **T = 125°C, T = 25°C, and T = -55°C.**

- At **T = 125°C**, the curve starts at a higher β_F value and shows a peak slightly above 400 in Region II before decreasing in Region III.
- At **T = 25°C**, the curve follows a similar trend, peaking around 300 in Region II.
- At **T = -55°C**, the curve starts at a lower β_F value, peaking around 200 in Region II before decreasing in Region III.

The graph highlights how temperature affects the forward current gain, with higher temperatures resulting in higher peak β_F values. The behavior of β_F with respect to I_C across different temperature levels is clearly illustrated in this graph.

Figure 1.15 Typical curves of $\beta_{F}$ versus $I_{C}$ for an $n p n$ integrated-circuit transistor with $6 \mu \mathrm{~m}^{2}$ emitter area.
as a function of $V_{B E}$. This is shown in Fig. 1.16, and because of the log scale on the vertical axis, the value of $\ln \beta_{F}$ can be obtained directly as the distance between the two curves.

At moderate current levels represented by region II in Figs. 1.15 and 1.16, both $I_{C}$ and $I_{B}$ follow the ideal behavior, and

$$
\begin{align*}
I_{C} & =I_{S} \exp \frac{V_{B E}}{V_{T}}  \tag{1.82}\\
I_{B} & \simeq \frac{I_{S}}{\beta_{F M}} \exp \frac{V_{B E}}{V_{T}} \tag{1.83}
\end{align*}
$$

where $\beta_{F M}$ is the maximum value of $\beta_{F}$ and is given by (1.48).
At low current levels, $I_{C}$ still follows the ideal relationship of (1.82), and the decrease in $\beta_{F}$ is due to an additional component in $I_{B}$, which is mainly due to recombination of carriers in the base-emitter depletion region and is present at any current level. However, at higher current levels the base current given by (1.83) dominates, and this additional component has
image_name:Figure 1.16
description:Figure 1.16 is a graph depicting the base and collector currents of a bipolar transistor plotted against the base-emitter voltage \( V_{BE} \). The graph is a semi-logarithmic plot where the vertical axis represents the natural logarithm of the current \( \ln I \) while the horizontal axis represents \( V_{BE} \) on a linear scale.

Axes Labels and Units:
- **Vertical Axis:** \( \ln I \) (Logarithmic scale)
- **Horizontal Axis:** \( V_{BE} \) (Linear scale)

Overall Behavior and Trends:
The graph shows two main curves:
1. **Collector Current \( I_C \):** This curve starts from the origin and rises steeply in Region I, continuing to increase through Regions II and III. The slope of this curve indicates an exponential relationship with \( V_{BE} \), consistent with the ideal diode equation at low current levels.
2. **Base Current \( I_B \):** This curve also rises but starts at a lower value than \( I_C \). The distance between \( I_C \) and \( I_B \) curves represents \( \ln \beta_F \), where \( \beta_F \) is the current gain of the transistor.

Key Features and Technical Details:
- **Regions:** The graph is divided into three regions marked as I, II, and III. These regions indicate different operational behaviors of the transistor.
- **\( \ln \beta_F \) Distances:**
- \( \ln \beta_{FL} \) in Region I
- \( \ln \beta_{FM} \) in Region II
- \( \ln \beta_{FH} \) in Region III
- **Intersection Point:** The dashed line intersects the \( I_C \) and \( I_B \) curves in Region I, indicating a point where recombination effects are significant.

Annotations and Specific Data Points:
- The graph includes annotations for \( \ln \beta_{FL} \), \( \ln \beta_{FM} \), and \( \ln \beta_{FH} \), which highlight the changes in current gain across different regions.
- The dashed lines serve as reference markers for these regions, showing where transitions occur.

This graph effectively illustrates how the base and collector currents change with the base-emitter voltage and highlights the impact of recombination and current gain across different operational regions of the transistor.

Figure 1.16 Base and collector currents of a bipolar transistor plotted on a log scale versus $V_{B E}$ on a linear scale. The distance between the curves is a direct measure of $\ln \beta_{F}$.
little effect. The base current resulting from recombination in the depletion region is ${ }^{5}$

$$
\begin{equation*}
I_{B X} \simeq I_{S X} \exp \frac{V_{B E}}{m V_{T}} \tag{1.84}
\end{equation*}
$$

where

$$
m \simeq 2
$$

At very low collector currents, where (1.84) dominates the base current, the current gain can be calculated from (1.82) and (1.84) as

$$
\begin{equation*}
\beta_{F L} \simeq \frac{I_{C}}{I_{B X}}=\frac{I_{S}}{I_{S X}} \exp \frac{V_{B E}}{V_{T}}\left(1-\frac{1}{m}\right) \tag{1.85}
\end{equation*}
$$

Substitution of (1.82) in (1.85) gives

$$
\begin{equation*}
\beta_{F L} \simeq \frac{I_{S}}{I_{S X}}\left(\frac{I_{C}}{I_{S}}\right)^{[1-(1 / m)]} \tag{1.86}
\end{equation*}
$$

If $m \simeq 2$, then (1.86) indicates that $\beta_{F}$ is proportional to $\sqrt{I_{C}}$ at very low collector currents.
At high current levels, the base current $I_{B}$ tends to follow the relationship of (1.83), and the decrease in $\beta_{F}$ in region III is due mainly to a decrease in $I_{C}$ below the value given by (1.82). (In practice the measured curve of $I_{B}$ versus $V_{B E}$ in Fig. 1.16 may also deviate from a straight line at high currents due to the influence of voltage drop across the base resistance.) The decrease in $I_{C}$ is due partly to the effect of high-level injection, and at high current levels the collector current approaches ${ }^{7}$

$$
\begin{equation*}
I_{C} \simeq I_{S H} \exp \frac{V_{B E}}{2 V_{T}} \tag{1.87}
\end{equation*}
$$

The current gain in this region can be calculated from (1.87) and (1.83) as

$$
\begin{equation*}
\beta_{F H} \simeq \frac{I_{S H}}{I_{S}} \beta_{F M} \exp \left(-\frac{V_{B E}}{2 V_{T}}\right) \tag{1.88}
\end{equation*}
$$

Substitution of (1.87) in (1.88) gives

$$
\beta_{F H} \simeq \frac{I_{S H}^{2}}{I_{S}} \beta_{F M} \frac{1}{I_{C}}
$$

Thus $\beta_{F}$ decreases rapidly at high collector currents.
In addition to the effect of high-level injection, the value of $\beta_{F}$ at high currents is also decreased by the onset of the Kirk effect ${ }^{13}$ which occurs when the minority-carrier concentration in the collector becomes comparable to the donor-atom doping density. The base region of the transistor then stretches out into the collector and becomes greatly enlarged.

## 1.4 Small-Signal Models of Bipolar Transistors

Analog circuits often operate with signal levels that are small compared to the bias currents and voltages in the circuit. In these circumstances, incremental or small-signal models can be derived that allow calculation of circuit gain and terminal impedances without the necessity of including the bias quantities. A hierarchy of models with increasing complexity can be derived, and the more complex ones are generally reserved for computer analysis. Part of the designer's skill is knowing which elements of the model can be omitted when performing hand calculations on a particular circuit, and this point is taken up again later.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: Vcc, B: b1, E: GND}
name: b1, type: VoltageSource, value: V_BE, ports: {Np: V_BE, Nn: GND}
name: V_CC, type: VoltageSource, value: V_CC, ports: {Np: Vcc, Nn: GND}
"name:v_i,type:VoltageSource,value:vi,ports:{Np:b1,Nn:VBE}
]
extrainfo:The circuit is a small-signal model of a bipolar transistor in the forward-active region, showing the effect of a small-signal input voltage.
image_name:(b)
description:The graph in Figure 1.17(b) illustrates the effect of a small-signal input voltage on the carrier concentration in the base region of a bipolar transistor when it is in the forward-active region. This is a carrier concentration versus position graph.

1. **Type of Graph and Function:**
- The graph is a spatial distribution plot showing carrier concentration across the emitter, base, and collector regions of a bipolar transistor.

2. **Axes Labels and Units:**
- The horizontal axis represents the position (x) across the transistor from the emitter to the collector.
- The vertical axis represents carrier concentration, though specific units are not provided in the diagram.

3. **Overall Behavior and Trends:**
- The carrier concentration decreases linearly from the emitter through the base to the collector.
- The effect of a small-signal input voltage is represented by a shift in the carrier concentration levels, depicted by the shaded areas (ΔQh and ΔQe).
- The graph shows a higher concentration of carriers at the emitter side, decreasing towards the collector, consistent with typical operation in the forward-active region.

4. **Key Features and Technical Details:**
- The emitter depletion region is marked at the beginning of the graph, followed by the base and collector regions.
- The base region shows a linear decrease in carrier concentration, with annotations indicating the quiescent and small-signal components of the collector current (I_C and i_c, respectively).
- The shaded areas (ΔQh and ΔQe) indicate changes in hole and electron charges due to the small-signal input.
- The exponential expressions for carrier concentration at the emitter (n_p(0)) are given, highlighting the effect of bias voltage (V_BE) and small-signal input (v_i).

5. **Annotations and Specific Data Points:**
- Annotations indicate the exponential dependence of carrier concentration on the base-emitter voltage (V_BE) and thermal voltage (V_T).
- The graph highlights the quiescent charge (Q_e) and the changes in charge (ΔQe and ΔQh) due to the input signal, which affect the collector current (I_C + i_c).

Figure 1.17 Effect of a small-signal input voltage applied to a bipolar transistor. (a) Circuit schematic. (b) Corresponding changes in carrier concentrations in the base when the device is in the forward-active region.

Consider the bipolar transistor in Fig. $1.17 a$ with bias voltages $V_{B E}$ and $V_{C C}$ applied as shown. These produce a quiescent collector current, $I_{C}$, and a quiescent base current, $I_{B}$, and the device is in the forward-active region. A small-signal input voltage $v_{i}$ is applied in series with $V_{B E}$ and produces a small variation in base current $i_{b}$ and a small variation in collector current $i_{c}$. Total values of base and collector currents are $I_{b}$ and $I_{c}$, respectively, and thus $I_{b}=\left(I_{B}+i_{b}\right)$ and $I_{c}=\left(I_{C}+i_{c}\right)$. The carrier concentrations in the base of the transistor corresponding to the situation in Fig. 1.17a are shown in Fig. 1.17b. With only bias voltages applied, the carrier concentrations are given by the solid lines. Application of the small-signal voltage $v_{i}$ causes $n_{p}(0)$ at the emitter edge of the base to increase, and produces the concentrations shown by the dotted lines. These pictures can now be used to derive the various elements in the small-signal equivalent circuit of the bipolar transistor.

### 1.4.1 Transconductance

The transconductance is defined as

$$
\begin{equation*}
g_{m}=\frac{d I_{C}}{d V_{B E}} \tag{1.89}
\end{equation*}
$$

Since

$$
\Delta I_{C}=\frac{d I_{C}}{d V_{B E}} \Delta V_{B E}
$$

we can write

$$
\Delta I_{C}=g_{m} \Delta V_{B E}
$$

and thus

$$
\begin{equation*}
i_{c}=g_{m} v_{i} \tag{1.90}
\end{equation*}
$$

The value of $g_{m}$ can be found by substituting (1.35) in (1.89) to give

$$
\begin{equation*}
g_{m}=\frac{d}{d V_{B E}} I_{S} \exp \frac{V_{B E}}{V_{T}}=\frac{I_{S}}{V_{T}} \exp \frac{V_{B E}}{V_{T}}=\frac{I_{C}}{V_{T}}=\frac{q I_{C}}{k T} \tag{1.91}
\end{equation*}
$$

The transconductance thus depends linearly on the bias current $I_{C}$ and is $38 \mathrm{~mA} / \mathrm{V}$ for $I_{C}=$ 1 mA at $25^{\circ} \mathrm{C}$ for any bipolar transistor of either polarity ( $n p n$ or pnp), of any size, and made of any material ( $\mathrm{Si}, \mathrm{Ge}, \mathrm{GaAs}$ ).

To illustrate the limitations on the use of small-signal analysis, the foregoing relation will be derived in an alternative way. The total collector current in Fig. 1.17a can be calculated using (1.35) as

$$
\begin{equation*}
I_{c}=I_{S} \exp \frac{V_{B E}+v_{i}}{V_{T}}=I_{S} \exp \frac{V_{B E}}{V_{T}} \exp \frac{v_{i}}{V_{T}} \tag{1.92}
\end{equation*}
$$

But the collector bias current is

$$
\begin{equation*}
I_{C}=I_{S} \exp \frac{V_{B E}}{V_{T}} \tag{1.93}
\end{equation*}
$$

and use of (1.93) in (1.92) gives

$$
\begin{equation*}
I_{c}=I_{C} \exp \frac{v_{i}}{V_{T}} \tag{1.94}
\end{equation*}
$$

If $v_{i}<V_{T}$, the exponential in (1.94) can be expanded in a power series,

$$
\begin{equation*}
I_{c}=I_{C}\left[1+\frac{v_{i}}{V_{T}}+\frac{1}{2}\left(\frac{v_{i}}{V_{T}}\right)^{2}+\frac{1}{6}\left(\frac{v_{i}}{V_{T}}\right)^{3}+\cdots\right] \tag{1.95}
\end{equation*}
$$

Now the incremental collector current is

$$
\begin{equation*}
i_{c}=I_{c}-I_{C} \tag{1.96}
\end{equation*}
$$

and substitution of (1.96) in (1.95) gives

$$
\begin{equation*}
i_{c}=\frac{I_{C}}{V_{T}} v_{i}+\frac{1}{2} \frac{I_{C}}{V_{T}^{2}} v_{i}^{2}+\frac{1}{6} \frac{I_{C}}{V_{T}^{3}} v_{i}^{3}+\cdots \tag{1.97}
\end{equation*}
$$

If $v_{i} \ll V_{T}$, (1.97) reduces to (1.90), and the small-signal analysis is valid. The criterion for use of small-signal analysis is thus $v_{i}=\Delta V_{B E} \ll 26 \mathrm{mV}$ at $25^{\circ} \mathrm{C}$. In practice, if $\Delta V_{B E}$ is less than 10 mV , the small-signal analysis is accurate within about 10 percent.

### 1.4.2 Base-Charging Capacitance

Figure $1.17 b$ shows that the change in base-emitter voltage $\Delta V_{B E}=v_{i}$ has caused a change $\Delta Q_{e}=q_{e}$ in the minority-carrier charge in the base. By charge-neutrality requirements, there is an equal change $\Delta Q_{h}=q_{h}$ in the majority-carrier charge in the base. Since majority carriers
are supplied by the base lead, the application of voltage $v_{i}$ requires the supply of charge $q_{h}$ to the base, and the device has an apparent input capacitance

$$
\begin{equation*}
C_{b}=\frac{q_{h}}{v_{i}} \tag{1.98}
\end{equation*}
$$

The value of $C_{b}$ can be related to fundamental device parameters as follows. If (1.39) is divided by (1.33), we obtain

$$
\begin{equation*}
\frac{Q_{e}}{I_{C}}=\frac{W_{B}^{2}}{2 D_{n}}=\tau_{F} \tag{1.99}
\end{equation*}
$$

The quantity $\tau_{F}$ has the dimension of time and is called the base transit time in the forward direction. Since it is the ratio of the charge in transit $\left(Q_{e}\right)$ to the current flow $\left(I_{C}\right)$, it can be identified as the average time per carrier spent in crossing the base. To a first order it is independent of operating conditions and has typical values 10 to 500 ps for integrated npn transistors and 1 to 40 ns for lateral pnp transistors. Practical values of $\tau_{F}$ tend to be somewhat lower than predicted by (1.99) for diffused transistors that have nonuniform base doping. ${ }^{14}$ However, the functional dependence on base width $W_{B}$ and diffusion constant $D_{n}$ is as predicted by (1.99).

From (1.99)

$$
\begin{equation*}
\Delta Q_{e}=\tau_{F} \Delta I_{C} \tag{1.100}
\end{equation*}
$$

But since $\Delta Q_{e}=\Delta Q_{h}$, we have

$$
\begin{equation*}
\Delta Q_{h}=\tau_{F} \Delta I_{C} \tag{1.101}
\end{equation*}
$$

and this can be written

$$
\begin{equation*}
q_{h}=\tau_{F} i_{c} \tag{1.102}
\end{equation*}
$$

Use of (1.102) in (1.98) gives

$$
\begin{equation*}
C_{b}=\tau_{F} \frac{i_{c}}{v_{i}} \tag{1.103}
\end{equation*}
$$

and substitution of (1.90) in (1.103) gives

$$
\begin{align*}
C_{b} & =\tau_{F} g_{m}  \tag{1.104}\\
& =\tau_{F} \frac{q I_{C}}{k T} \tag{1.105}
\end{align*}
$$

Thus the small-signal, base-charging capacitance is proportional to the collector bias current.
In the inverse-active mode of operation, an equation similar to (1.99) relates stored charge and current via a time constant $\tau_{R}$. This is typically orders of magnitude larger than $\tau_{F}$ because the device structure and doping are optimized for operation in the forward-active region. Since the saturation region is a combination of forward-active and inverse-active operation, inclusion of the parameter $\tau_{R}$ in a SPICE listing will model the large charge storage that occurs in saturation.

### 1.4.3 Input Resistance

In the forward-active region, the base current is related to the collector current by

$$
\begin{equation*}
I_{B}=\frac{I_{C}}{\beta_{F}} \tag{1.47}
\end{equation*}
$$

Small changes in $I_{B}$ and $I_{C}$ can be related using (1.47):

$$
\begin{equation*}
\Delta I_{B}=\frac{d}{d I_{C}}\left(\frac{I_{C}}{\beta_{F}}\right) \Delta I_{C} \tag{1.106}
\end{equation*}
$$

and thus

$$
\begin{equation*}
\beta_{0}=\frac{\Delta I_{C}}{\Delta I_{B}}=\frac{i_{c}}{i_{b}}=\left[\frac{d}{d I_{C}}\left(\frac{I_{C}}{\beta_{F}}\right)\right]^{-1} \tag{1.107}
\end{equation*}
$$

where $\beta_{0}$ is the small-signal current gain of the transistor. Note that if $\beta_{F}$ is constant, then $\beta_{F}=\beta_{0}$. Typical values of $\beta_{0}$ are close to those of $\beta_{F}$, and in subsequent chapters little differentiation is made between these quantities. A single value of $\beta$ is often assumed for a transistor and then used for both ac and dc calculations.

Equation 1.107 relates the change in base current $i_{b}$ to the corresponding change in collector current $i_{c}$, and the device has a small-signal input resistance given by

$$
\begin{equation*}
r_{\pi}=\frac{v_{i}}{i_{b}} \tag{1.108}
\end{equation*}
$$

Substitution of (1.107) in (1.108) gives

$$
\begin{equation*}
r_{\pi}=\frac{v_{i}}{i_{c}} \beta_{0} \tag{1.109}
\end{equation*}
$$

and use of (1.90) in (1.109) gives

$$
\begin{equation*}
r_{\pi}=\frac{\beta_{0}}{g_{m}} \tag{1.110}
\end{equation*}
$$

Thus the small-signal input shunt resistance of a bipolar transistor depends on the current gain and is inversely proportional to $I_{C}$.

### 1.4.4 Output Resistance

In Section 1.3.2 the effect of changes in collector-emitter voltage $V_{C E}$ on the large-signal characteristics of the transistor was described. It follows from that treatment that small changes $\Delta V_{C E}$ in $V_{C E}$ produce corresponding changes $\Delta I_{C}$ in $I_{C}$, where

$$
\begin{equation*}
\Delta I_{C}=\frac{\partial I_{C}}{\partial V_{C E}} \Delta V_{C E} \tag{1.111}
\end{equation*}
$$

Substitution of (1.55) and (1.57) in (1.111) gives

$$
\begin{equation*}
\frac{\Delta V_{C E}}{\Delta I_{C}}=\frac{V_{A}}{I_{C}}=r_{o} \tag{1.112}
\end{equation*}
$$

where $V_{A}$ is the Early voltage and $r_{o}$ is the small-signal output resistance of the transistor. Since typical values of $V_{A}$ are 50 to 100 V , corresponding values of $r_{o}$ are 50 to $100 \mathrm{k} \Omega$ for $I_{C}=1 \mathrm{~mA}$. Note that $r_{o}$ is inversely proportional to $I_{C}$, and thus $r_{o}$ can be related to $g_{m}$, as are many of the other small-signal parameters.

$$
\begin{equation*}
r_{o}=\frac{1}{\eta g_{m}} \tag{1.113}
\end{equation*}
$$

where

$$
\begin{equation*}
\eta=\frac{k T}{q V_{A}} \tag{1.114}
\end{equation*}
$$

image_name:Figure 1.18 Basic bipolar transistor small-signal equivalent circuit
description:
[
name: rπ, type: Resistor, value: rπ, ports: {N1: B, N2: E}
name: Cb, type: Capacitor, value: Cb, ports: {Np: B, Nn: E}
name: gmv1, type: VoltageControlledCurrentSource, ports: {Np: C, Nn: E}
name: ro, type: Resistor, value: ro, ports: {N1: C, N2: E}
]
extrainfo:The circuit represents a basic bipolar transistor small-signal equivalent circuit with parameters defined for rπ, ro, gm, and Cb. It includes a voltage-controlled current source (gmv1) and is configured for small-signal analysis.

Figure 1.18 Basic bipolar transistor small-signal equivalent circuit.

If $V_{A}=100 \mathrm{~V}$, then $\eta=2.6 \times 10^{-4}$ at $25^{\circ} \mathrm{C}$. Note that $1 / r_{o}$ is the slope of the output characteristics of Fig. 1.10.

### 1.4.5 Basic Small-Signal Model of the Bipolar Transistor

Combination of the above small-signal circuit elements yields the small-signal model of the bipolar transistor shown in Fig. 1.18. This is valid for both $n p n$ and $p n p$ devices in the forwardactive region and is called the hybrid- $\pi$ model. Collector, base, and emitter nodes are labeled $C, B$ and $E$, respectively. The elements in this circuit are present in the equivalent circuit of any bipolar transistor and are specified by relatively few parameters ( $\left.\beta, \tau_{F}, \eta, I_{C}\right)$. Note that in the evaluation of the small-signal parameters for pnp transistors, the magnitude only of $I_{C}$ is used. In the following sections, further elements are added to this model to account for parasitics and second-order effects.

### 1.4.6 Collector-Base Resistance

Consider the effect of variations in $V_{C E}$ on the minority charge in the base as illustrated in Fig. 1.9. An increase in $V_{C E}$ causes an increase in the collector depletion-layer width and consequent reduction of base width. This causes a reduction in the total minority-carrier charge stored in the base and thus a reduction in base current $I_{B}$ due to a reduction in $I_{B 1}$ given by (1.40). Since an increase $\Delta V_{C E}$ in $V_{C E}$ causes a decrease $\Delta I_{B}$ in $I_{B}$, this effect can be modeled by inclusion of a resistor $r_{\mu}$ from collector to base of the model of Fig. 1.18. If $V_{B E}$ is assumed held constant, the value of this resistor can be determined as follows.

$$
\begin{equation*}
r_{\mu}=\frac{\Delta V_{C E}}{\Delta I_{B 1}}=\frac{\Delta V_{C E}}{\Delta I_{C}} \frac{\Delta I_{C}}{\Delta I_{B 1}} \tag{1.115}
\end{equation*}
$$

Substitution of (1.112) in (1.115) gives

$$
\begin{equation*}
r_{\mu}=r_{o} \frac{\Delta I_{C}}{\Delta I_{B 1}} \tag{1.116}
\end{equation*}
$$

If the base current $I_{B}$ is composed entirely of component $I_{B 1}$, then (1.107) can be used in (1.116) to give

$$
\begin{equation*}
r_{\mu}=\beta_{0} r_{o} \tag{1.117}
\end{equation*}
$$

This is a lower limit for $r_{\mu}$. In practice, $I_{B 1}$ is typically less than 10 percent of $I_{B}$ [component $I_{B 2}$ from (1.42) dominates] in integrated $n p n$ transistors, and since $I_{B 1}$ is very small, the change $\Delta I_{B 1}$ in $I_{B 1}$ for a given $\Delta V_{C E}$ and $\Delta I_{C}$ is also very small. Thus a typical value for $r_{\mu}$ is greater than $10 \beta_{0} r_{o}$. For lateral $p n p$ transistors, recombination in the base is more significant, and $r_{\mu}$ is in the range $2 \beta_{0} r_{o}$ to $5 \beta_{0} r_{o}$.

### 1.4.7 Parasitic Elements in the Small-Signal Model

The elements of the bipolar transistor small-signal equivalent circuit considered so far may be considered basic in the sense that they arise directly from essential processes in the device. However, technological limitations in the fabrication of transistors give rise to a number of parasitic elements that must be added to the equivalent circuit for most integrated-circuit transistors. A cross section of a typical $n p n$ transistor in a junction-isolated process is shown in Fig. 1.19. The means of fabricating such devices is described in Chapter 2.

As described in Section 1.2, all pn junctions have a voltage-dependent capacitance associated with the depletion region. In the cross section of Fig. 1.19, three depletion-region capacitances can be identified. The base-emitter junction has a depletion-region capacitance $C_{j e}$ and the base-collector and collector-substrate junctions have capacitances $C_{\mu}$ and $C_{c s}$, respectively. The base-emitter junction closely approximates an abrupt junction due to the steep rise of the doping density caused by the heavy doping in the emitter. Thus the variation of $C_{j e}$ with bias voltage is well approximated by (1.21). The collector-base junction behaves like a graded junction for small bias voltages since the doping density is a function of distance near the junction. However, for larger reverse-bias values (more than about a volt), the junction depletion region spreads into the collector, which is uniformly doped, and thus for devices with thick collectors the junction tends to behave like an abrupt junction with uniform doping. Many modern high-speed processes, however, have very thin collector regions (of the order of one micron), and the collector depletion region can extend all the way to the buried layer for quite small reverse-bias voltages. When this occurs, both the depletion region and the associated capacitance vary quite slowly with bias voltage. The collector-base capacitance $C_{\mu}$ thus tends to follow (1.22) for very small bias voltages and (1.21) for large bias voltages in thick-collector devices. In practice, measurements show that the variation of $C_{\mu}$ with bias voltage for most devices can be approximated by

$$
\begin{equation*}
C_{\mu}=\frac{C_{\mu 0}}{\left(1-\frac{V}{\psi_{o}}\right)^{n}} \tag{1.117a}
\end{equation*}
$$

where $V$ is the forward bias on the junction and $n$ is an exponent between about 0.2 and 0.5 . The third parasitic capacitance in a monolithic $n p n$ transistor is the collector-substrate capacitance
image_name:Figure 1.19 Integrated-circuit npn bipolar transistor structure showing parasitic elements
description:The image illustrates the structure of an integrated-circuit npn bipolar transistor, highlighting its parasitic elements. The diagram is not to scale and is a cross-sectional view of the transistor.

Identification of Components and Structure:
1. **Collector, Base, and Emitter:**
- The transistor has three main terminals labeled as Collector, Base, and Emitter, each connected to specific regions within the structure.
- The collector region consists of an n+ type material, indicating a heavily doped n-type semiconductor.
- The base region is made of p-type material, situated between the collector and emitter.
- The emitter is also composed of n+ type material.

2. **Buried Layer and Substrate:**
- A buried layer labeled as n+ is shown below the main transistor structure, providing a low-resistance path for current.
- The substrate is made of p-type material, supporting the entire structure.

3. **Parasitic Elements:**
- **Capacitances:**
- **C_je:** Represents the junction capacitance between the base and emitter.
- **C_μ:** Represents the parasitic capacitance between the base and collector.
- **C_cs:** Denotes the collector-substrate capacitance.
- **Resistances:**
- **r_b:** Base resistance.
- **r_ex:** Emitter resistance.
- **r_c1, r_c2, r_c3:** Collector resistances, indicating different paths and interactions within the structure.

Connections and Interactions:
- **Injected Electron Motion:**
- Arrows indicate the motion of injected electrons from the emitter to the collector through the base, illustrating the flow of current in the active region of the transistor.
- **Feedback and Control Loops:**
- The parasitic capacitances and resistances form loops that can affect the transistor's operation, particularly in high-frequency applications.

Labels, Annotations, and Key Features:
- The diagram includes labels for different regions and components, such as n+, p, and n, indicating doping types and material properties.
- Annotations like "Injected electron motion" help in understanding the electron flow within the transistor.
- The presence of various resistances and capacitances highlights the complexity and parasitic nature of the integrated circuit transistor, which can impact performance and needs to be considered in design and analysis.

Overall, the diagram provides a detailed view of the internal structure and parasitic elements of an npn bipolar transistor, essential for understanding its electrical behavior in integrated circuits.

Figure 1.19 Integrated-circuit npn bipolar transistor structure showing parasitic elements. (Not to scale.)
$C_{c s}$, and for large reverse bias voltages this varies according to the abrupt junction equation (1.21) for junction-isolated devices. In the case of oxide-isolated devices, however, the deep $p$ diffusions used to isolate the devices are replaced by oxide. The sidewall component of $C_{c s}$ then consists of a fixed oxide capacitance. Equation 1.117a may then be used to model $C_{c s}$, but a value of $n$ less than 0.5 gives the best approximation. In general, (1.117a) will be used to model all three parasitic capacitances with subscripts $e, c$, and $s$ on $n$ and $\psi_{0}$ used to differentiate emitter-base, collector-base, and collector-substrate capacitances, respectively. Typical zero-bias values of these parasitic capacitances for a minimum-size npn transistor in a modern oxide-isolated process are $C_{j e 0} \simeq 10 \mathrm{fF}, C_{\mu 0} \simeq 10 \mathrm{fF}$, and $C_{c s 0} \simeq 20 \mathrm{fF}$. Values for other devices are summarized in Chapter 2.

As described in Chapter 2, lateral $p n p$ transistors have a parasitic capacitance $C_{b s}$ from base to substrate in place of $C_{c s}$. Note that the substrate is always connected to the most negative voltage supply in the circuit in order to ensure that all isolation regions are separated by reverse-biased junctions. Thus the substrate is an ac ground, and all parasitic capacitance to the substrate is connected to ground in an equivalent circuit.

The final elements to be added to the small-signal model of the transistor are resistive parasitics. These are produced by the finite resistance of the silicon between the top contacts on the transistor and the active base region beneath the emitter. As shown in Fig. 1.19, there are significant resistances $r_{b}$ and $r_{c}$ in series with the base and collector contacts, respectively. There is also a resistance $r_{e x}$ of several ohms in series with the emitter lead that can become important at high bias currents. (Note that the collector resistance $r_{c}$ is actually composed of three parts labeled $r_{c 1}, r_{c 2}$, and $r_{c 3}$.) Typical values of these parameters are $r_{b}=50$ to $500 \Omega$, $r_{e x}=1$ to $3 \Omega$, and $r_{c}=20$ to $500 \Omega$. The value of $r_{b}$ varies significantly with collector current because of current crowding. ${ }^{15}$ This occurs at high collector currents where the dc base current produces a lateral voltage drop in the base that tends to forward bias the base-emitter junction preferentially around the edges of the emitter. Thus the transistor action tends to occur along the emitter periphery rather than under the emitter itself, and the distance from the base contact to the active base region is reduced. Consequently, the value of $r_{b}$ is reduced, and in a typical $n p n$ transistor, $r_{b}$ may decrease 50 percent as $I_{C}$ increases from 0.1 mA to 10 mA .

The value of these parasitic resistances can be reduced by changes in the device structure. For example, a large-area transistor with multiple base and emitter stripes will have a smaller value of $r_{b}$. The value of $r_{c}$ is reduced by inclusion of the low-resistance buried $n^{+}$layer beneath the collector.

The addition of the resistive and capacitive parasitics to the basic small-signal circuit of Fig. 1.18 gives the complete small-signal equivalent circuit of Fig. 1.20. The internal base node
image_name:Figure 1.20
description:
[
name: rb, type: Resistor, value: rb, ports: {N1: B, N2: "B"}
name: rπ, type: Resistor, value: rπ, ports: {N1: "B", N2: "E"}
name: rμ, type: Resistor, value: rμ, ports: {N1: "B", N2: "C"}
name: ro, type: Resistor, value: ro, ports: {N1: "C", N2: "E"}
name: rc, type: Resistor, value: rc, ports: {N1: "C", N2: C}
name: rex, type: Resistor, value: rex, ports: {N1: "E", N2: E}
name: Cπ, type: Capacitor, value: Cπ, ports: {Np: "B", Nn: "E"}
name: Cμ, type: Capacitor, value: Cμ, ports: {Np: "B", Nn: "C"}
name: Ccs, type: Capacitor, value: Ccs, ports: {Np: "C", Nn: GND}
name: gmV1, type: VoltageControlledCurrentSource, ports: {Np: "E", Nn: "C"}
]
extrainfo:The circuit represents a complete small-signal equivalent model of a bipolar transistor, incorporating parasitic resistances and capacitances. Node B' is the internal base node, distinct from the external base contact B. Capacitance Cπ includes the base-charging capacitance Cb and the emitter-base depletion layer capacitance Cje.

Figure 1.20 Complete bipolar transistor small-signal equivalent circuit.
is labeled $B^{\prime}$ to distinguish it from the external base contact $B$. The capacitance $C_{\pi}$ contains the base-charging capacitance $C_{b}$ and the emitter-base depletion layer capacitance $C_{j e}$.

$$
\begin{equation*}
C_{\pi}=C_{b}+C_{j e} \tag{1.118}
\end{equation*}
$$

Note that the representation of parasitics in Fig. 1.20 is an approximation in that lumped elements have been used. In practice, as suggested by Fig. 1.19, $C_{\mu}$ is distributed across $r_{b}$ and $C_{c s}$ is distributed across $r_{c}$. This lumped representation is adequate for most purposes but can introduce errors at very high frequencies. It should also be noted that while the parasitic resistances of Fig. 1.20 can be very important at high bias currents or for high-frequency operation, they are usually omitted from the equivalent circuit for low-frequency calculations, particularly for collector bias currents less than 1 mA .

#### EXAMPLE

Derive the complete small-signal equivalent circuit for a bipolar transistor at $I_{C}=1 \mathrm{~mA}$, $V_{C B}=3 \mathrm{~V}$, and $V_{C S}=5 \mathrm{~V}$. Device parameters are $C_{j e 0}=10 \mathrm{fF}, n_{e}=0.5, \psi_{0 e}=0.9 \mathrm{~V}, C_{\mu 0}=$ $10 \mathrm{fF}, n_{c}=0.3, \psi_{0 c}=0.5 \mathrm{~V}, C_{c s 0}=20 \mathrm{fF}, n_{s}=0.3, \psi_{0 s}=0.65 \mathrm{~V}, \beta_{0}=100, \tau_{F}=10 \mathrm{ps}$, $V_{A}=20 \mathrm{~V}, r_{b}=300 \Omega, r_{c}=50 \Omega, r_{e x}=5 \Omega, r_{\mu}=10 \beta_{0} r_{o}$.

Since the base-emitter junction is forward biased, the value of $C_{j e}$ is difficult to determine for reasons described in Section 1.2.1. Either a value can be determined by computer or a reasonable estimation is to double $C_{j e 0}$. Using the latter approach, we estimate

$$
C_{j e}=20 \mathrm{fF}
$$

Using (1.117a) gives, for the collector-base capacitance,

$$
C_{\mu}=\frac{C_{\mu 0}}{\left(1+\frac{V_{C B}}{\psi_{0 c}}\right)^{n_{c}}}=\frac{10}{\left(1+\frac{3}{0.5}\right)^{0.3}}=5.6 \mathrm{fF}
$$

The collector-substrate capacitance can also be calculated using (1.117a)

$$
C_{c s}=\frac{C_{c s 0}}{\left(1+\frac{V_{C S}}{\psi_{0 s}}\right)^{n_{s}}}=\frac{20}{\left(1+\frac{5}{0.65}\right)^{0.3}}=10.5 \mathrm{fF}
$$

From (1.91) the transconductance is

$$
g_{m}=\frac{q I_{C}}{k T}=\frac{10^{-3}}{26 \times 10^{-3}} \mathrm{~A} / \mathrm{V}=38 \mathrm{~mA} / \mathrm{V}
$$

From (1.104) the base-charging capacitance is

$$
C_{b}=\tau_{F} g_{m}=10 \times 10^{-12} \times 38 \times 10^{-3} \mathrm{~F}=0.38 \mathrm{pF}
$$

The value of $C_{\pi}$ from (1.118) is

$$
C_{\pi}=0.38+0.02 \mathrm{pF}=0.4 \mathrm{pF}
$$

image_name:Figure 1.21 Complete small-signal equivalent circuit for a bipolar transistor
description:
[
name: 300 Ω, type: Resistor, value: 300 Ω, ports: {N1: B, N2: "B"}
name: 2.6 kΩ, type: Resistor, value: 2.6 kΩ, ports: {N1: "B", N2: E}
name: 20 MΩ, type: Resistor, value: 20 MΩ, ports: {N1: "B", N2: "C"}
name: 20 kΩ, type: Resistor, value: 20 kΩ, ports: {N1: "C", N2: "E"}
name: 5 Ω, type: Resistor, value: 5 Ω, ports: {N1: "E", N2: E}
name: 50 Ω, type: Resistor, value: 50 Ω, ports: {N1: "C", N2: C}
name: 5.6 fF, type: Capacitor, value: 5.6 fF, ports: {Np: "B", Nn: "C"}
name: 0.4 pF, type: Capacitor, value: 0.4 pF, ports: {Np: "B", Nn: "E"}
name: 10.5 fF, type: Capacitor, value: 10.5 fF, ports: {Np: "C", Nn: GND}
name: v1, type: VoltageSource, value: v1, ports: {Np: "B", Nn: "E"}
name: 38 x 10^-3 v1, type: VoltageControlledCurrentSource, value: 38 x 10^-3 v1, ports: {Np: "C", Nn: "E'"}
]
extrainfo:The circuit is a small-signal equivalent model for a bipolar transistor with various resistors and capacitors representing different parasitic elements. It includes a voltage-controlled current source, indicating transconductance behavior, and several capacitors modeling junction capacitances.

Figure 1.21 Complete small-signal equivalent circuit for a bipolar transistor at $I_{C}=1 \mathrm{~mA}, V_{C B}=3 \mathrm{~V}$, and $V_{C S}=5 \mathrm{~V}$. Device parameters are $C_{j e 0}=10 \mathrm{fF}, n_{e}=0.5, \psi_{0 e}=0.9 \mathrm{~V}, C_{\mu 0}=10 \mathrm{fF}, n_{c}=0.3$, $\psi_{0 c}=0.5 \mathrm{~V}, C_{c s 0}=20 \mathrm{fF}, n_{s}=0.3, \psi_{0 s}=0.65 \mathrm{~V}, \beta_{0}=100, \tau_{F}=10 \mathrm{ps}, V_{A}=20 \mathrm{~V}, r_{b}=300 \Omega$, $r_{c}=50 \Omega, r_{e x}=5 \Omega, r_{\mu}=10 \beta_{0} r_{0}$.

The input resistance from (1.110) is

$$
r_{\pi}=\frac{\beta_{0}}{g_{m}}=100 \times 26 \Omega=2.6 \mathrm{k} \Omega
$$

The output resistance from (1.112) is

$$
r_{o}=\frac{20}{10^{-3}} \Omega=20 \mathrm{k} \Omega
$$

and thus the collector-base resistance is

$$
r_{\mu}=10 \beta_{0} r_{o}=10 \times 100 \times 20 \mathrm{k} \Omega=20 \mathrm{M} \Omega
$$

The equivalent circuit with these parameter values is shown in Fig. 1.21.

### 1.4.8 Specification of Transistor Frequency Response

The high-frequency gain of the transistor is controlled by the capacitive elements in the equivalent circuit of Fig. 1.20. The frequency capability of the transistor is most often specified in practice by determining the frequency where the magnitude of the short-circuit, commonemitter current gain falls to unity. This is called the transition frequency, $f_{T}$, and is a measure of the maximum useful frequency of the transistor when it is used as an amplifier. The value of $f_{T}$ can be measured as well as calculated, using the ac circuit of Fig. 1.22. A small-signal current $i_{i}$ is applied to the base, and the output current $i_{o}$ is measured with the collector short-circuited for ac signals. A small-signal equivalent circuit can be formed for this situation by using the equivalent circuit of Fig. 1.20 as shown in Fig. 1.23, where $r_{e x}$ and $r_{\mu}$ have been neglected. If $r_{c}$ is assumed small, then $r_{o}$ and $C_{c s}$ have no influence, and we have

$$
\begin{equation*}
v_{1} \simeq \frac{r_{\pi}}{1+r_{\pi}\left(C_{\pi}+C_{\mu}\right) s} i_{i} \tag{1.119}
\end{equation*}
$$

If the current fed forward through $C_{\mu}$ is neglected,

$$
\begin{equation*}
i_{o} \simeq g_{m} v_{1} \tag{1.120}
\end{equation*}
$$

image_name:Figure 1.22 Schematic of ac circuit for measurement of $f_{T}$
description:
[
name: Q1, type: NPN, ports: {C: GND, B: b1, E: GND}
name: i_i, type: CurrentSource, ports: {Np: GND, Nn: b1}
]
extrainfo:The circuit is a simple NPN transistor amplifier with a current source input. The output current i_o is taken from the collector of the transistor, which is connected to the ground.

Figure 1.22 Schematic of ac circuit for measurement of $f_{T}$.
image_name:Figure 1.22 Schematic of ac circuit for measurement of $f_{T}$
description:
[
name: i_i, type: CurrentSource, value: i_i, ports: {Np: X, Nn: GND}
name: r_b, type: Resistor, value: r_b, ports: {N1: X, N2: b1}
name: C_π, type: Capacitor, value: C_π, ports: {Np: b1, Nn: GND}
name: r_π, type: Resistor, value: r_π, ports: {N1: b1, N2: GND}
name: C_μ, type: Capacitor, value: C_μ, ports: {Np: b1, Nn: C1}
name: g_mv_1, type: VoltageControlledCurrentSource, value: g_mv_1, ports: {Np: C1, Nn: GND}
name: r_o, type: Resistor, value: r_o, ports: {N1: C1, N2: GND}
name: C_cs, type: Capacitor, value: C_cs, ports: {Np: C1, Nn: GND}
name: r_c, type: Resistor, value: r_c, ports: {N1: C1, N2: GND}
name: i_o, type: CurrentSource, value: i_o, ports: {Np: C1, Nn: GND}
]
extrainfo:The circuit is a small-signal model used to measure the transition frequency (f_T) of an NPN transistor. It includes a current source input (i_i), various resistors (r_b, r_π, r_o, r_c), capacitors (C_π, C_μ, C_cs), and a voltage-controlled current source (g_mv_1). The output current (i_o) is measured at the collector node (C1), which is grounded.

Figure 1.23 Small-signal equivalent circuit for the calculation of $f_{T}$.

Substitution of (1.119) in (1.120) gives

$$
i_{o} \simeq i_{i} \frac{g_{m} r_{\pi}}{1+r_{\pi}\left(C_{\pi}+C_{\mu}\right) s}
$$

and thus

$$
\begin{equation*}
\frac{i_{o}}{i_{i}}(j \omega)=\frac{\beta_{0}}{1+\beta_{0} \frac{C_{\pi}+C_{\mu}}{g_{m}} j \omega} \tag{1.121}
\end{equation*}
$$

using (1.110).
Now if $i_{o} / i_{i}(j \omega)$ is written as $\beta(j \omega)$ (the high-frequency, small-signal current gain), then

$$
\begin{equation*}
\beta(j \omega)=\frac{\beta_{0}}{1+\beta_{0} \frac{C_{\pi}+C_{\mu}}{g_{m}} j \omega} \tag{1.122}
\end{equation*}
$$

At high frequencies the imaginary part of the denominator of (1.122) is dominant, and we can write

$$
\begin{equation*}
\beta(j \omega) \simeq \frac{g_{m}}{j \omega\left(C_{\pi}+C_{\mu}\right)} \tag{1.123}
\end{equation*}
$$

From (1.123), $|\beta(j \omega)|=1$ when

$$
\begin{equation*}
\omega=\omega_{T}=\frac{g_{m}}{C_{\pi}+C_{\mu}} \tag{1.124}
\end{equation*}
$$

and thus

$$
\begin{equation*}
f_{T}=\frac{1}{2 \pi} \frac{g_{m}}{C_{\pi}+C_{\mu}} \tag{1.125}
\end{equation*}
$$

The transistor behavior can be illustrated by plotting $|\beta(j \omega)|$ using (1.122) as shown in Fig. 1.24. The frequency $\omega_{\beta}$ is defined as the frequency where $|\beta(j \omega)|$ is equal to $\beta_{0} / \sqrt{2}$
image_name:Figure 1.24
description:Figure 1.24 is a Bode plot illustrating the magnitude of the small-signal AC current gain, \(|\beta(j \omega)|\), versus frequency for a typical bipolar transistor. The plot is characterized by the following features:

1. **Axes Labels and Units:**
- The vertical axis represents the magnitude of the current gain, \(|\beta(j \omega)|\), on a logarithmic scale, ranging from 1 to 1000.
- The horizontal axis represents frequency, \(\omega\), also on a logarithmic scale. Specific frequency markers such as \(\omega_{\beta}\), \(0.1\omega_{T}\), and \(\omega_{T}\) are indicated.

2. **Overall Behavior and Trends:**
- At low frequencies, the magnitude \(|\beta(j \omega)|\) remains constant at a value denoted as \(\beta_0\), which is the low-frequency gain.
- As the frequency increases, the gain begins to decrease at a rate of \(-6 \text{ dB/octave}\).
- The decrease continues until it reaches a point where the gain is significantly lower.

3. **Key Features and Technical Details:**
- \(\omega_{\beta}\) is marked as the frequency where the gain drops to \(\beta_0/\sqrt{2}\), indicating the -3 dB point.
- \(\omega_{T}\) is the unity-gain frequency where the magnitude of the gain becomes 1.
- The slope of the decrease is consistent with a \(-6 \text{ dB/octave}\) roll-off, indicating a single-pole response.

4. **Annotations and Specific Data Points:**
- The plot is annotated with a dashed line indicating the low-frequency gain \(\beta_0\).
- The horizontal dashed lines at \(|\beta(j \omega)| = 100\) and \(|\beta(j \omega)| = 10\) help illustrate the logarithmic scale and the rate of decrease.

This plot provides insight into the frequency response of a bipolar transistor, highlighting its gain characteristics over a range of frequencies and identifying critical points such as \(\omega_{\beta}\) and \(\omega_{T}\).

Figure 1.24 Magnitude of small-signal ac current gain $|\beta(j \omega)|$ versus frequency for a typical bipolar transistor.
( 3 dB down from the low-frequency value). From (1.122) we have

$$
\begin{equation*}
\omega_{\beta}=\frac{1}{\beta_{0}} \frac{g_{m}}{C_{\pi}+C_{\mu}}=\frac{\omega_{T}}{\beta_{0}} \tag{1.126}
\end{equation*}
$$

From Fig. 1.24 it can be seen that $\omega_{T}$ can be determined by measuring $|\beta(j \omega)|$ at some frequency $\omega_{x}$ where $|\beta(j \omega)|$ is falling at $6 \mathrm{~dB} /$ octave and using

$$
\begin{equation*}
\omega_{T}=\omega_{x}\left|\beta\left(j \omega_{x}\right)\right| \tag{1.127}
\end{equation*}
$$

This is the method used in practice, since deviations from ideal behavior tend to occur as $|\beta(j \omega)|$ approaches unity. Thus $|\beta(j \omega)|$ is typically measured at some frequency where its magnitude is about 5 or 10 , and (1.127) is used to determine $\omega_{T}$.

It is interesting to examine the time constant, $\tau_{T}$, associated with $\omega_{T}$. This is defined as

$$
\begin{equation*}
\tau_{T}=\frac{1}{\omega_{T}} \tag{1.128}
\end{equation*}
$$

and use of (1.124) in (1.128) gives

$$
\begin{equation*}
\tau_{T}=\frac{C_{\pi}}{g_{m}}+\frac{C_{\mu}}{g_{m}} \tag{1.129}
\end{equation*}
$$

Substitution of (1.118) and (1.104) in (1.129) gives

$$
\begin{equation*}
\tau_{T}=\frac{C_{b}}{g_{m}}+\frac{C_{j e}}{g_{m}}+\frac{C_{\mu}}{g_{m}}=\tau_{F}+\frac{C_{j e}}{g_{m}}+\frac{C_{\mu}}{g_{m}} \tag{1.130}
\end{equation*}
$$

Equation 1.130 indicates that $\tau_{T}$ is dependent on $I_{C}$ (through $g_{m}$ ) and approaches a constant value of $\tau_{F}$ at high collector bias currents. At low values of $I_{C}$, the terms involving $C_{j e}$ and $C_{\mu}$ dominate, and they cause $\tau_{T}$ to rise and $f_{T}$ to fall as $I_{C}$ is decreased. This behavior is illustrated in Fig. 1.25, which is a typical plot of $f_{T}$ versus $I_{C}$ for an integrated-circuit $n p n$ transistor. The decline in $f_{T}$ at high collector currents is not predicted by this simple theory and is due to an increase in $\tau_{F}$ caused by high-level injection and Kirk effect at high currents. These are the same mechanisms that cause a decrease in $\beta_{F}$ at high currents as described in Section 1.3.5.
image_name:Figure 1.25
description:Figure 1.25 is a plot of the transition frequency ($f_{T}$) versus the collector current ($I_{C}$) for an $n p n$ integrated-circuit transistor. The graph is plotted on a logarithmic scale for the x-axis, which represents the collector current ($I_{C}$) in amperes, ranging from 10 microamperes ($10 \mu A$) to 10 milliamperes ($10 mA$). The y-axis is linear and represents the transition frequency ($f_{T}$) in gigahertz (GHz), ranging from 1 GHz to 10 GHz.

The graph shows that as the collector current ($I_{C}$) increases from 10 microamperes, the transition frequency ($f_{T}$) initially rises, reaching a peak around 1 mA. After this peak, the transition frequency begins to decline as the collector current continues to increase.

This behavior indicates that $f_{T}$ increases with $I_{C}$ up to a certain point, after which it decreases, likely due to high-level injection and the Kirk effect at high currents, as mentioned in the context. This trend reflects a typical characteristic of $n p n$ transistors where the transition frequency is optimized at moderate current levels but degrades at higher currents due to physical limitations.

Figure 1.25 Typical curve of $f_{T}$ versus $I_{C}$ for an $n p n$ integrated-circuit transistor with $6 \mu \mathrm{~m}^{2}$ emitter area in a high-speed process.

#### EXAMPLE

A bipolar transistor has a short-circuit, common-emitter current gain at 1 GHz of 8 with $I_{C}=0.25 \mathrm{~mA}$ and 9 with $I_{C}=1 \mathrm{~mA}$. Assuming that high-level injection effects are negligible, calculate $C_{j e}$ and $\tau_{F}$, assuming both are constant. The measured value of $C_{\mu}$ is 10 fF .

From the data, values of $f_{T}$ are

$$
\begin{array}{lll}
f_{T 1}=8 \times 1=8 \mathrm{GHz} & \text { at } \quad I_{C}=0.25 \mathrm{~mA} \\
f_{T 2}=9 \times 1=9 \mathrm{GHz} & \text { at } \quad I_{C}=1 \mathrm{~mA}
\end{array}
$$

Corresponding values of $\tau_{T}$ are

$$
\begin{aligned}
& \tau_{T 1}=\frac{1}{2 \pi f_{T 1}}=19.9 \mathrm{ps} \\
& \tau_{T 2}=\frac{1}{2 \pi f_{T 2}}=17.7 \mathrm{ps}
\end{aligned}
$$

Using these data in (1.130), we have

$$
\begin{equation*}
19.9 \times 10^{-12}=\tau_{F}+104\left(C_{\mu}+C_{j e}\right) \tag{1.131}
\end{equation*}
$$

at $I_{C}=0.25 \mathrm{~mA}$. At $I_{C}=1 \mathrm{~mA}$ we have

$$
\begin{equation*}
17.7 \times 10^{-12}=\tau_{F}+26\left(C_{\mu}+C_{j e}\right) \tag{1.132}
\end{equation*}
$$

Subtraction of (1.132) from (1.131) yields

$$
C_{\mu}+C_{j e}=28.2 \mathrm{fF}
$$

Since $C_{\mu}$ was measured as 10 fF , the value of $C_{j e}$ is given by

$$
C_{j e} \simeq 18.2 \mathrm{fF}
$$

Substitution in (1.131) gives

$$
\tau_{F}=17 \mathrm{ps}
$$

This is an example of how basic device parameters can be determined from high-frequency current-gain measurements. Note that the assumption that $C_{j e}$ is constant is a useful approximation in practice because $V_{B E}$ changes by only 36 mV as $I_{C}$ increases from 0.25 mA to 1 mA .

## 1.5 Large-Signal Behavior of Metal-Oxide-Semiconductor Field-Effect Transistors

Metal-oxide-semiconductor field-effect transistors (MOSFETs) have become dominant in the area of digital integrated circuits because they allow high density and low power dissipation. In contrast, bipolar transistors still provide many advantages in stand-alone analog integrated circuits. For example, the transconductance per unit bias current in bipolar transistors is usually much higher than in MOS transistors. So in systems where analog techniques are used on some integrated circuits and digital techniques on others, bipolar technologies are often preferred for the analog integrated circuits and MOS technologies for the digital. To reduce system cost and increase portability, both increased levels of integration and reduced power dissipation are required, forcing the associated analog circuits to use MOS-compatible technologies. One way to achieve these goals is to use a processing technology that provides both bipolar and MOS transistors, allowing great design flexibility. However, all-MOS processes are less expensive than combined bipolar and MOS processes. Therefore, economic considerations drive integrated-circuit manufacturers to use all-MOS processes in many practical cases. As a result, the study of the characteristics of MOS transistors that affect analog integrated-circuit design is important.

### 1.5.1 Transfer Characteristics of MOS Devices

A cross section of a typical enhancement-mode $n$-channel MOS (NMOS) transistor is shown in Fig. 1.26. Heavily doped $n$-type source and drain regions are fabricated in a $p$-type substrate (often called the body). A thin layer of silicon dioxide is grown over the substrate material and
image_name:Figure 1.26 Typical enhancement-mode NMOS structure
description:The diagram illustrates a typical enhancement-mode n-channel MOS (NMOS) transistor structure. It depicts a cross-sectional view of the transistor, highlighting its key components and their arrangement.

1. **Identification of Components and Structure:**
- **Source (S) and Drain (D):** These are heavily doped n-type regions, labeled as n+, embedded in a p-type substrate (the body of the transistor). The source and drain are the terminals between which current flows.
- **Gate (G):** Positioned above the channel region, the gate is made of metal or polycrystalline silicon. It is separated from the substrate by a thin layer of silicon dioxide (SiO2), which acts as an insulator.
- **p-type Substrate (Body):** The main body of the transistor is a p-type semiconductor material. This substrate supports the formation of the channel region when a voltage is applied.
- **Silicon Dioxide (SiO2) Layer:** This insulating layer is located between the gate and the substrate, preventing direct electrical contact.

2. **Connections and Interactions:**
- The gate-source voltage (Vgs) controls the conductance of the channel region, which forms between the source and drain under the gate when a sufficient voltage is applied. This allows the gate voltage to modulate the current flow from source to drain.
- The channel region is the path through which electrons flow when the transistor is in the 'on' state, controlled by the gate voltage.

3. **Labels, Annotations, and Key Features:**
- The diagram includes labels for the source (S), gate (G), drain (D), and body (B) terminals.
- Annotations indicate the n+ doping of the source and drain, the metal or poly silicon gate contact, and the presence of the SiO2 layer.
- The channel region is marked, showing the area influenced by the gate voltage to control current flow.

Figure 1.26 Typical enhancement-mode NMOS structure.
a conductive gate material (metal or polycrystalline silicon) covers the oxide between source and drain. Note that the gate is horizontal in Fig. 1.26, and we will use this orientation in all descriptions of the physical operation of MOS devices. In operation, the gate-source voltage modifies the conductance of the region under the gate, allowing the gate voltage to control the current flowing between source and drain. This control can be used to provide gain in analog circuits and switching characteristics in digital circuits.

The enhancement-mode NMOS device of Fig. 1.26 shows significant conduction between source and drain only when an $n$-type channel exists under the gate. This observation is the origin of the $n$-channel designation. The term enhancement mode refers to the fact that no conduction occurs for $V_{G S}=0$. Thus, the channel must be enhanced to cause conduction. MOS devices can also be made by using an $n$-type substrate with a $p$-type conducting channel. Such devices are called enhancement-mode $p$-channel MOS (PMOS) transistors. In complementary MOS (CMOS) technology, both device types are present.

The derivation of the transfer characteristics of the enhancement-mode NMOS device of Fig. 1.26 begins by noting that with $V_{G S}=0$, the source and drain regions are separated by back-to-back $p n$ junctions. These junctions are formed between the $n$-type source and drain regions and the $p$-type substrate, resulting in an extremely high resistance (about $10^{12} \Omega$ ) between drain and source when the device is off.

Now consider the substrate, source, and drain grounded with a positive voltage $V_{G S}$ applied to the gate as shown in Fig. 1.27. The gate and substrate then form the plates of a capacitor with the $\mathrm{SiO}_{2}$ as a dielectric. Positive charge accumulates on the gate and negative charge in the substrate. Initially, the negative charge in the $p$-type substrate is manifested by the creation of a depletion region and the exclusion of holes under the gate as described in Section 1.2 for a $p n$-junction. The depletion region is shown in Fig. 1.27. The results of Section 1.2 can now be applied. Using (1.10), the depletion-layer width $X$ under the oxide is

$$
\begin{equation*}
X=\left(\frac{2 \epsilon \phi}{q N_{A}}\right)^{1 / 2} \tag{1.133}
\end{equation*}
$$

where $\phi$ is the potential in the depletion layer at the oxide-silicon interface, $N_{A}$ is the doping density (assumed constant) of the $p$-type substrate in atoms $/ \mathrm{cm}^{3}$, and $\epsilon$ is the permittivity of the silicon. The charge per area in this depletion region is

$$
\begin{equation*}
Q=q N_{A} X=\sqrt{2 q N_{A} \epsilon \phi} \tag{1.134}
\end{equation*}
$$

image_name:Figure 1.27 Idealized NMOS device cross section
description:The image depicts an idealized cross-section of an NMOS (n-channel metal-oxide-semiconductor) device with a positive gate-source voltage \(V_{GS}\) applied. The structure consists of several key components:

1. **Substrate and Regions:**
- The main body of the device is a \(p\)-type substrate, which is the base material.
- Two \(n^+\) regions are embedded in the \(p\)-type substrate, labeled as the source \(S\) and the drain \(D\). These regions are highly doped with n-type material to form the source and drain terminals.
- A depletion region is shown around the \(n^+\) regions, indicating areas where mobile carriers are depleted.

2. **Gate Structure:**
- Above the substrate and between the source and drain is a thin layer of silicon dioxide \(SiO_2\), acting as the gate oxide.
- On top of the \(SiO_2\) layer is the gate \(G\), which is a conductive layer that controls the flow of carriers in the channel.
- A positive voltage \(V_{GS}\) is applied to the gate relative to the source, inducing an \(n\)-type channel in the \(p\)-type substrate just beneath the oxide layer.

3. **Channel:**
- The induced \(n\)-type channel runs between the source and drain, allowing current to flow when a voltage is applied between the drain and source.
- The channel length \(L\) is indicated, representing the distance between the source and drain terminals.

4. **Connections and Annotations:**
- The source \(S\) and drain \(D\) are connected to ground, indicating they are at the same potential.
- The gate \(G\) has a positive voltage \(V_{GS}\) applied, which is crucial for the operation of the NMOS device.
- The diagram is labeled with annotations such as "Induced \(n\)-type channel" and "Depletion region," providing clarity on the function and structure of the device.

This cross-section illustrates the basic operation of an NMOS transistor, highlighting the formation of a conductive channel when a positive voltage is applied to the gate, allowing current to flow between the source and drain through the induced channel.

Figure 1.27 Idealized NMOS device cross section with positive $V_{G S}$ applied, showing depletion regions and the induced channel.

When the surface potential in the silicon reaches a critical value equal to twice the Fermi level $\phi_{f}$, a phenomenon known as inversion occurs. ${ }^{16}$ The Fermi level $\phi_{f}$ is defined as

$$
\begin{equation*}
\phi_{f}=\frac{k T}{q} \ln \left[\frac{N_{A}}{n_{i}}\right] \tag{1.135}
\end{equation*}
$$

where $k$ is Boltzmann's constant. Also, $n_{i}$ is the intrinsic carrier concentration, which is

$$
\begin{equation*}
n_{i}=\sqrt{N_{c} N_{v}} \exp \left(-\frac{E_{g}}{2 k T}\right) \tag{1.136}
\end{equation*}
$$

where $E_{g}$ is the band gap of silicon at $T=0^{\circ} \mathrm{K}, N_{c}$ is the density of allowed states near the edge of the conduction band, and $N_{v}$ is the density of allowed states near the edge of the valence band, respectively. The Fermi level $\phi_{f}$ is usually about 0.3 V . After the potential in the silicon reaches $2 \phi_{f}$, further increases in gate voltage produce no further changes in the depletion-layer width but instead induce a thin layer of electrons in the depletion layer at the surface of the silicon directly under the oxide. Inversion produces a continuous $n$-type region with the source and drain regions and forms the conducting channel between source and drain. The conductivity of this channel can be modulated by increases or decreases in the gate-source voltage. In the presence of an inversion layer, and without substrate bias, the depletion region contains a fixed charge density

$$
\begin{equation*}
Q_{b 0}=\sqrt{2 q N_{A} \epsilon 2 \phi_{f}} \tag{1.137}
\end{equation*}
$$

If a substrate bias voltage $V_{S B}$ (positive for $n$-channel devices) is applied between the source and substrate, the potential required to produce inversion becomes ( $\left.2 \phi_{f}+V_{S B}\right)$, and the charge density stored in the depletion region in general is

$$
\begin{equation*}
Q_{b}=\sqrt{2 q N_{A} \epsilon\left(2 \phi_{f}+V_{S B}\right)} \tag{1.138}
\end{equation*}
$$

The gate-source voltage $V_{G S}$ required to produce an inversion layer is called the threshold voltage $V_{t}$ and can now be calculated. This voltage consists of several components. First, a voltage $\left[2 \phi_{f}+\left(Q_{b} / C_{o x}\right)\right]$ is required to sustain the depletion-layer charge $Q_{b}$, where $C_{o x}$ is the gate oxide capacitance per unit area. Second, a work-function difference $\phi_{m s}$ exists between the gate metal and the silicon. Third, positive charge density $Q_{s s}$ always exists in the
image_name:
description:The image contains a continuation of the text discussing the electrical properties at the silicon interface. It mentions that the positive charge density $Q_{ss}$ exists at the oxide at the silicon interface. This charge is attributed to crystal discontinuities at the Si-SiO2 interface. This context is important for understanding the components contributing to the threshold voltage $V_t$ in semiconductor devices, as previously described in the equations provided in the context.
interface and must be compensated by a gate-source voltage contribution of $-Q_{s s} / C_{o x}$. Thus we have a threshold voltage

$$
\begin{align*}
V_{t} & =\phi_{m s}+2 \phi_{f}+\frac{Q_{b}}{C_{o x}}-\frac{Q_{s s}}{C_{o x}}  \tag{1.139}\\
& =\phi_{m s}+2 \phi_{f}+\frac{Q_{b 0}}{C_{o x}}-\frac{Q_{s s}}{C_{o x}}+\frac{Q_{b}-Q_{b 0}}{C_{o x}} \\
& =V_{t 0}+\gamma\left(\sqrt{2 \phi_{f}+V_{S B}}-\sqrt{2 \phi_{f}}\right) \tag{1.140}
\end{align*}
$$

where (1.137) and (1.138) have been used, and $V_{t 0}$ is the threshold voltage with $V_{S B}=0$. The parameter $\gamma$ is defined as

$$
\begin{equation*}
\gamma=\frac{1}{C_{o x}} \sqrt{2 q \epsilon N_{A}} \tag{1.141}
\end{equation*}
$$

and

$$
\begin{equation*}
C_{o x}=\frac{\epsilon_{o x}}{t_{o x}} \tag{1.142}
\end{equation*}
$$

where $\epsilon_{o x}$ and $t_{o x}$ are the permittivity and the thickness of the oxide, respectively. A typical value of $\gamma$ is $0.5 \mathrm{~V}^{1 / 2}$, and $C_{o x}=3.45 \mathrm{fF} / \mu \mathrm{m}^{2}$ for $t_{o x}=100$ angstroms.
image_name:Figure 1.28 NMOS device with bias voltages applied
description:The image illustrates an NMOS device with bias voltages applied, providing a cross-sectional view of the transistor structure. Key components and features include:

1. **Structure and Components:**
- **Source (S):** The source terminal is connected to the left n+ region, which is linked to ground.
- **Drain (D):** The drain terminal is connected to the right n+ region, with a voltage $V_{DS}$ applied between the drain and the source.
- **Gate (G):** The gate is positioned above the channel, with a voltage $V_{GS}$ applied, controlling the channel conductivity.
- **Channel:** The channel is formed between the source and drain under the gate, within the p-type substrate.
- **Depletion Region:** The depletion regions are shown around the n+ regions, indicating areas where charge carriers are depleted.
- **p-type Substrate:** The substrate is p-type, which is common for NMOS devices.

2. **Connections and Interactions:**
- **Voltage Application:**
- $V_{GS}$ is applied between the gate and source.
- $V_{DS}$ is applied between the drain and source to drive the current $I_D$ through the channel.
- $V_{SB}$ is applied between the substrate and source, influencing the threshold voltage.
- **Current Flow:**
- The current $I_D$ flows from drain to source, controlled by the gate voltage.
- **Voltage Distribution:**
- The voltage $V(y)$ is indicated along the channel from source to drain, showing potential variation.

3. **Labels and Annotations:**
- **Voltage Labels:** $V_{GS}$, $V_{DS}$, and $V_{SB}$ are labeled to indicate the applied voltages.
- **Current Direction:** The direction of $I_D$ is marked, showing electron flow direction.
- **Depletion Region:** Labeled to highlight the areas of reduced carrier concentration.

This diagram serves as a detailed representation of an NMOS transistor, illustrating the physical layout and electrical connections necessary for its operation.

Figure 1.28 NMOS device with bias voltages applied.

In practice, the value of $V_{t 0}$ is usually adjusted in processing by implanting additional impurities into the channel region. Extra $p$-type impurities are implanted in the channel to set $V_{t 0}$ between 0.3 V and 1.5 V for $n$-channel enhancement devices. By implanting $n$-type impurities in the channel region, a conducting channel can be formed even for $V_{G S}=0$, forming a depletion device with typical values of $V_{t 0}$ in the range -1 V to -4 V . If $Q_{i}$ is the charge density due to the implant, then the threshold voltage given by (1.139) is shifted by approximately $Q_{i} / C_{o x}$.

The preceding equations can now be used to calculate the large-signal characteristics of an $n$-channel MOSFET. In this analysis, the source is assumed grounded and bias voltages $V_{G S}, V_{D S}$, and $V_{S B}$ are applied as shown in Fig. 1.28. If $V_{G S}>V_{t}$, inversion occurs and a conducting channel exists. The channel conductivity is determined by the vertical electric field, which is controlled by the value of $\left(V_{G S}-V_{t}\right)$. If $V_{D S}=0$, the current $I_{D}$ that flows from drain to source is zero because the horizontal electric field is zero. Nonzero $V_{D S}$ produces a horizontal electric field and causes current $I_{D}$ to flow. The value of the current depends on both the horizontal and the vertical electric fields, explaining the term field-effect transistor. Positive voltage $V_{D S}$ causes the reverse bias from the drain to the substrate to be larger than from the source to substrate, and thus the widest depletion region exists at the drain. For simplicity, however, we assume that the voltage drop along the channel itself is small so that the depletion-layer width is constant along the channel.

The drain current $I_{D}$ is

$$
\begin{equation*}
I_{D}=\frac{d Q}{d t} \tag{1.143}
\end{equation*}
$$

where $d Q$ is the incremental channel charge at a distance $y$ from the source in an incremental length $d y$ of the channel, and $d t$ is the time required for this charge to cross length $d y$. The charge $d Q$ is

$$
\begin{equation*}
d Q=Q_{I} W d y \tag{1.144}
\end{equation*}
$$

where $W$ is the width of the device perpendicular to the plane of Fig. 1.28 and $Q_{I}$ is the induced electron charge per unit area of the channel. At a distance $y$ along the channel, the voltage with respect to the source is $V(y)$ and the gate-to-channel voltage at that point is $V_{G S}-V(y)$. We assume this voltage exceeds the threshold voltage $V_{t}$. Thus the induced electron charge per unit area in the channel is

$$
\begin{equation*}
Q_{I}(y)=C_{o x}\left[V_{G S}-V(y)-V_{t}\right] \tag{1.145}
\end{equation*}
$$

Also,

$$
\begin{equation*}
d t=\frac{d y}{v_{d}(y)} \tag{1.146}
\end{equation*}
$$

where $v_{d}$ is the electron drift velocity at a distance $y$ from the source. Combining (1.144) and (1.146) gives

$$
\begin{equation*}
I_{D}=W Q_{I}(y) v_{d}(y) \tag{1.147}
\end{equation*}
$$

The drift velocity is determined by the horizontal electric field. When the horizontal electric field $\mathscr{E}(y)$ is small, the drift velocity is proportional to the field and

$$
\begin{equation*}
v_{d}(y)=\mu_{n} \mathscr{E}(y) \tag{1.148}
\end{equation*}
$$

where the constant of proportionality $\mu_{n}$ is the average electron mobility in the channel. In practice, the mobility depends on both the temperature and the doping level but is almost constant for a wide range of normally used doping levels. Also, $\mu_{n}$ is sometimes called the surface mobility for electrons because the channel forms at the surface of the silicon. Typical values range from about $500 \mathrm{~cm}^{2} /(\mathrm{V}-\mathrm{s})$ to about $700 \mathrm{~cm}^{2} /(\mathrm{V}-\mathrm{s})$, which are much less than the mobility of electrons in the bulk of the silicon (about $1400 \mathrm{~cm}^{2} / \mathrm{V}-\mathrm{s}$ ) because surface defects not present in the bulk impede the flow of electrons in MOS transistors. ${ }^{17}$ The electric field $\mathscr{E}(y)$ is

$$
\begin{equation*}
\mathscr{E}(y)=\frac{d V}{d y} \tag{1.149}
\end{equation*}
$$

where $d V$ is the incremental voltage drop along the length of channel $d y$ at a distance $y$ from the source. Substituting (1.145), (1.148), and (1.149) into (1.147) gives

$$
\begin{equation*}
I_{D}=W C_{o x}\left[V_{G S}-V-V_{t}\right] \mu_{n} \frac{d V}{d y} \tag{1.150}
\end{equation*}
$$

Separating variables and integrating gives

$$
\begin{equation*}
\int_{0}^{L} I_{D} d y=\int_{0}^{V_{D S}} W \mu_{n} C_{o x}\left(V_{G S}-V-V_{t}\right) d V \tag{1.151}
\end{equation*}
$$

Carrying out this integration gives

$$
\begin{equation*}
I_{D}=\frac{k^{\prime}}{2} \frac{W}{L}\left[2\left(V_{G S}-V_{t}\right) V_{D S}-V_{D S}^{2}\right] \tag{1.152}
\end{equation*}
$$

where

$$
\begin{equation*}
k^{\prime}=\mu_{n} C_{o x}=\frac{\mu_{n} \epsilon_{o x}}{t_{o x}} \tag{1.153}
\end{equation*}
$$

When $V_{D S} \ll 2\left(V_{G S}-V_{t}\right)$, (1.152) predicts that $I_{D}$ is approximately proportional to $V_{D S}$. This result is reasonable because the average horizontal electric field in this case is $V_{D S} / L$, and the average drift velocity of electrons is proportional to the average field when the field is small. Equation 1.152 is important and describes the $I-V$ characteristics of an MOS transistor, assuming a continuous induced channel. A typical value of $k^{\prime}$ for $t_{o x}=100$ angstroms is about $200 \mu \mathrm{~A} / \mathrm{V}^{2}$ for an $n$-channel device.

As the value of $V_{D S}$ is increased, the induced conducting channel narrows at the drain end and (1.145) indicates that $Q_{I}$ at the drain end approaches zero as $V_{D S}$ approaches $\left(V_{G S}-V_{t}\right)$. That is, the channel is no longer connected to the drain when $V_{D S}>V_{G S}-V_{t}$. This phenomenon is called pinch-off and can be understood by writing a KVL equation around the transistor:

$$
\begin{equation*}
V_{D S}=V_{D G}+V_{G S} \tag{1.154}
\end{equation*}
$$

Therefore, when $V_{D S}>V_{G S}-V_{t}$,

$$
\begin{equation*}
V_{D G}+V_{G S}>V_{G S}-V_{t} \tag{1.155}
\end{equation*}
$$

Rearranging (1.155) gives

$$
\begin{equation*}
V_{G D}<V_{t} \tag{1.156}
\end{equation*}
$$

Equation 1.156 shows that when drain-source voltage is greater than $\left(V_{G S}-V_{t}\right)$, the gatedrain voltage is less than a threshold, which means that the channel no longer exists at the drain. This result is reasonable because we know that the gate-to-channel voltage at the point where the channel disappears is equal to $V_{t}$ by the definition of the threshold voltage. Therefore, at the point where the channel pinches off, the channel voltage is $\left(V_{G S}-V_{t}\right)$. As a result, the average horizontal electric field across the channel in pinch-off does not depend on the the drainsource voltage but instead on the voltage across the channel, which is $\left(V_{G S}-V_{t}\right)$. Therefore, (1.152) is no longer valid if $V_{D S}>V_{G S}-V_{t}$. The value of $I_{D}$ in this region is obtained by substituting $V_{D S}=V_{G S}-V_{t}$ in (1.152), giving

$$
\begin{equation*}
I_{D}=\frac{k^{\prime}}{2} \frac{W}{L}\left(V_{G S}-V_{t}\right)^{2} \tag{1.157}
\end{equation*}
$$

Equation 1.157 predicts that the drain current is independent of $V_{D S}$ in the pinch-off region. In practice, however, the drain current in the pinch-off region varies slightly as the drain voltage is varied. This effect is due to the presence of a depletion region between the physical pinch-off point in the channel at the drain end and the drain region itself. If this depletion-layer width is $X_{d}$, then the effective channel length is given by

$$
\begin{equation*}
L_{\mathrm{eff}}=L-X_{d} \tag{1.158}
\end{equation*}
$$

If $L_{\text {eff }}$ is used in place of $L$ in (1.157), we obtain a more accurate formula for current in the pinch-off region

$$
\begin{equation*}
I_{D}=\frac{k^{\prime}}{2} \frac{W}{L_{\mathrm{eff}}}\left(V_{G S}-V_{t}\right)^{2} \tag{1.159}
\end{equation*}
$$

Because $X_{d}$ (and thus $L_{\text {eff }}$ ) are functions of the drain-source voltage in the pinch-off region, $I_{D}$ varies with $V_{D S}$. This effect is called channel-length modulation. Using (1.158) and (1.159), we obtain

$$
\begin{equation*}
\frac{\partial I_{D}}{\partial V_{D S}}=-\frac{k^{\prime}}{2} \frac{W}{L_{\mathrm{eff}}^{2}}\left(V_{G S}-V_{t}\right)^{2} \frac{d L_{\mathrm{eff}}}{d V_{D S}} \tag{1.160}
\end{equation*}
$$

and thus

$$
\begin{equation*}
\frac{\partial I_{D}}{\partial V_{D S}}=\frac{I_{D}}{L_{\mathrm{eff}}} \frac{d X_{d}}{d V_{D S}} \tag{1.161}
\end{equation*}
$$

This equation is analogous to (1.55) for bipolar transistors. Following a similar procedure, the Early voltage can be defined as

$$
\begin{equation*}
V_{A}=\frac{I_{D}}{\partial I_{D} / \partial V_{D S}} \tag{1.162}
\end{equation*}
$$

and thus

$$
\begin{equation*}
V_{A}=L_{\mathrm{eff}}\left(\frac{d X_{d}}{d V_{D S}}\right)^{-1} \tag{1.163}
\end{equation*}
$$

For MOS transistors, a commonly used parameter for the characterization of channellength modulation is the reciprocal of the Early voltage,

$$
\begin{equation*}
\lambda=\frac{1}{V_{A}} \tag{1.164}
\end{equation*}
$$

As in the bipolar case, the large-signal properties of the transistor can be approximated by assuming that $\lambda$ and $V_{A}$ are constants, independent of the bias conditions. Thus we can include the effect of channel-length modulation in the $I-V$ characteristics by modifying (1.157) to

$$
\begin{equation*}
I_{D}=\frac{k^{\prime}}{2} \frac{W}{L}\left(V_{G S}-V_{t}\right)^{2}\left(1+\frac{V_{D S}}{V_{A}}\right)=\frac{k^{\prime}}{2} \frac{W}{L}\left(V_{G S}-V_{t}\right)^{2}\left(1+\lambda V_{D S}\right) \tag{1.165}
\end{equation*}
$$

In practical MOS transistors, variation of $X_{d}$ with voltage is complicated by the fact that the field distribution in the drain depletion region is not one-dimensional. As a result, the calculation of $\lambda$ from the device structure is quite difficult, ${ }^{18}$ and developing effective values of $\lambda$ from experimental data is usually necessary. The parameter $\lambda$ is inversely proportional to the effective channel length and a decreasing function of the doping level in the channel. Typical values of $\lambda$ are in the range $0.05 \mathrm{~V}^{-1}$ to $0.005 \mathrm{~V}^{-1}$.

Plots of $I_{D}$ versus $V_{D S}$ with $V_{G S}$ as a parameter are shown in Fig. 1.29 for an NMOS transistor. The device operates in the pinch-off region when $V_{D S}>\left(V_{G S}-V_{t}\right)$. The pinchoff region for MOS devices is often called the saturation region. In saturation, the output characteristics are almost flat, which shows that the current depends mostly on the gate-source voltage and only to a small extent on the drain-source voltage. On the other hand, when $V_{D S}<\left(V_{G S}-V_{t}\right)$, the device operates in the Ohmic or triode region, where the device can be modeled as a nonlinear voltage-controlled resistor connected between the drain and source. The resistance of this resistor is nonlinear because the $V_{D S}^{2}$ term in (1.152) causes the resistance to depend on $V_{D S}$. Since this term is small when $V_{D S}$ is small, however, the nonlinearity is also small when $V_{D S}$ is small, and the triode region is also sometimes called the linear region. The boundary between the triode and saturation regions occurs when $V_{D S}=\left(V_{G S}-V_{t}\right)$. On this boundary, both (1.152) and (1.157) correctly predict $I_{D}$. Since $V_{D S}=\left(V_{G S}-V_{t}\right)$ along the boundary between triode and saturation, (1.157) shows that the boundary is $I_{D}=$ $\left(k^{\prime} / 2\right)(W / L) V_{D S}^{2}$. This parabolic function of $V_{D S}$ is shown in Fig. 1.29. For depletion $n$-channel MOS devices, $V_{t}$ is negative, and $I_{D}$ is nonzero even for $V_{G S}=0$. For PMOS devices, all polarities of voltages and currents are reversed.
image_name:Figure 1.29 NMOS device characteristics
description:The graph in Figure 1.29 illustrates the NMOS device characteristics by plotting the drain current ($I_D$) against the drain-source voltage ($V_{DS}$). The graph is a characteristic curve typical for an NMOS transistor, showcasing two distinct regions: the "Ohmic or triode region" and the "Active or pinch-off region."

Axes:
- **Y-axis**: Represents the drain current ($I_D$).
- **X-axis**: Represents the drain-source voltage ($V_{DS}$).

### Behavior and Trends:
- **Ohmic or Triode Region**: In this region, the curves exhibit a linear increase in $I_D$ with $V_{DS}$ for lower values of $V_{DS}$. This linear behavior is indicative of the transistor operating in the ohmic region where the device behaves like a resistor.
- **Active or Pinch-off Region**: As $V_{DS}$ increases, the curves enter the active region where $I_D$ becomes relatively constant, indicating that the NMOS transistor is in saturation. In this region, the current is less dependent on $V_{DS}$ and more on the gate-source voltage ($V_{GS}$).

Key Features:
- **$V_{DS} = V_{GS} - V_t$ Line**: The boundary between the ohmic and active regions is marked by a dashed line representing $V_{DS} = V_{GS} - V_t$, where $V_t$ is the threshold voltage.
- **Actual vs. Ideal Curves**: The graph shows both actual and ideal curves for the NMOS device, with the actual curve deviating slightly from the ideal as $V_{DS}$ increases.
- **$V_{GS}$ Influence**: The curves are shown for different values of $V_{GS}$, with an arrow indicating the direction of increasing $V_{GS}$. As $V_{GS}$ increases, the saturation current $I_D$ also increases, shifting the curves upward.

Annotations:
- The graph includes annotations for the regions and the $V_{DS} = V_{GS} - V_t$ line, providing clarity on the transition between operating modes.
- The position of the ideal and actual curves is noted, highlighting the difference in expected vs. real-world performance.
Figure 1.29 NMOS device characteristics.

image_name:Figure 1.30 Large-signal model for the NMOS transistor
description:
[
name: ID, type: CurrentSource, ports: {Np: D, Nn: S}
]
extrainfo:The circuit diagram represents a large-signal model for an NMOS transistor in saturation. The current source ID represents the drain current flowing from the drain (D) to the source (S) with gate (G) controlling the transistor operation through VGS.
Figure 1.30 Large-signal model for the NMOS transistor.

The results derived above can be used to form a large-signal model of the NMOS transistor in saturation. The model topology is shown in Fig. 1.30, where $I_{D}$ is given by (1.152) in the triode region and (1.157) in saturation, ignoring the effect of channel-length modulation. To include the effect of channel-length modulation, (1.159) or (1.165) should be used instead of (1.157) to find the drain current in saturation.

### 1.5.2 Comparison of Operating Regions of Bipolar and MOS Transistors

Notice that the meaning of the word saturation for MOS transistors is quite different than for bipolar transistors. Saturation in bipolar transistors refers to the region of operation where both junctions are forward biased and the collector-emitter voltage is approximately constant or saturated. On the other hand, saturation in MOS transistors refers to the region of operation where the channel is attached only to the source but not to the drain and the current is approximately constant or saturated. To avoid confusion, the term active region will be used in this book to describe the flat region of the MOS transistor characteristics, as shown in Fig. 1.29. This wording is selected to form a link between the operation of MOS and bipolar transistors. This link is summarized in the table of Fig. 1.31, which reviews the operating regions of npn bipolar and $n$-channel MOS transistors.

When the emitter junction is forward biased and the collector junction is reverse biased, bipolar transistors operate in the forward-active region. They operate in the reverse-active region when the collector junction is forward biased and the emitter junction is reverse biased. This distinction is important because integrated-circuit bipolar transistors are typically not symmetrical in practice; that is, the collector operates more efficiently as a collector of minority carriers than as an emitter. Similarly, the emitter operates more efficiently as an emitter of minority carriers than as a collector. One reason for this asymmetry is that the collector region surrounds the emitter region in integrated-circuit bipolar transistors, as shown in Fig. 1.19. A consequence of this asymmetry is that the current gain in the forward-active region $\beta_{F}$ is usually much greater than the current gain in the reverse-active region $\beta_{R}$.

In contrast, the source and drain of MOS transistors are completely interchangeable based on the preceding description. (In practice, the symmetry is good but not perfect.) Therefore, distinguishing between the forward-active and reverse-active regions of operation of an MOS transistor is not necessary.

| npn Bipolar Transistor |  | n-channel MOS Transistor |  |  |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Region | $V_{B E}$ | $V_{B C}$ | Region | $V_{G S}$ | $V_{G D}$ |
| Cutoff | $<V_{B E(\text { on })}$ | $<V_{B C(\text { on })}$ | Cutoff | $<V_{t}$ | $<V_{t}$ |
| Forward Active | $\geq V_{B E(\mathrm{on})}$ | $<V_{B C(\text { on })}$ | Saturation(Active) | $\geq V_{t}$ | $<V_{t}$ |
| Reverse Active | $<V_{B E(\mathrm{on})}$ | $\geq V_{B C(\text { on })}$ | Saturation(Active) | $<V_{t}$ | $\geq V_{t}$ |
| Saturation | $\geq V_{B E(\mathrm{on})}$ | $\geq V_{B C(\text { on })}$ | Triode | $\geq V_{t}$ | $\geq V_{t}$ |

Figure 1.31 Operating regions of $n p n$ bipolar and $n$-channel MOS transistors.

Figure 1.31 also shows that $n p n$ bipolar transistors operate in cutoff when both junctions are reversed biased. Similarly, MOS transistors operate in cutoff when the gate is biased so that inversion occurs at neither the source nor the drain. Furthermore, npn transistors operate in saturation when both junctions are forward biased, and MOS transistors operate in the triode region when the gate is biased so that the channel is connected to both the source and the drain. Therefore, this comparison leads us to view the voltage required to invert the surface of an MOS transistor as analogous to the voltage required to forward bias a pn junction in a bipolar transistor. To display this analogy, we will use the circuit symbols in Fig. 1.32a to represent MOS transistors. These symbols are intentionally chosen to appear similar to the symbols of the corresponding bipolar transistors. In bipolar-transistor symbols, the arrow at the emitter junction represents the direction of current flow when the emitter junction is forward biased. In MOS transistors, the pn junctions between the source and body and the drain and body are reverse biased for normal operation. Therefore, the arrows in Fig. 1.32a do not indicate pn junctions. Instead, they indicate the direction of current flow when the terminals are biased so that the terminal labeled as the drain operates as the drain and the terminal labeled as the source operates as the source. In NMOS transistors, the source is the source of electrons; therefore, the source operates at a lower voltage than the drain, and the current flows in a direction opposite that of the electrons in the channel. In PMOS transistors, the source is the source of holes; therefore, the source operates at a higher voltage than the drain, and the current flows in the same direction as the holes in the channel.

In CMOS technology, one device type is fabricated in the substrate, which is common to all devices, invariably connected to a dc power-supply voltage, and usually not shown on the circuit diagram. The other device type, however, is fabricated in separate isolation regions called wells, which may or may not be connected together and which may or may not be connected to a power-supply voltage. If these isolation regions are connected to the appropriate power supply, the symbols of Fig. $1.32 a$ will be used, and the substrate connection will not
image_name:Figure 1.32 (a)
description:
[
name: M0, type: NMOS, ports: {S: S, D: D, G: G}
name: M1, type: PMOS, ports: {S: S, D: D, G: G}
]
extrainfo:The diagram shows NMOS and PMOS symbols used in CMOS circuits with standard substrate connections. The NMOS (M0) and PMOS (M1) devices have their gates, drains, and sources labeled, but no body connections are shown, indicating standard substrate connections.
image_name:Figure 1.32 (b)
description:
[
name: M0, type: NMOS, ports: {S: S, D: D, G: G, B: B}
name: M1, type: PMOS, ports: {S: S, D: D, G: G, B: B}
]
extrainfo:The diagram shows NMOS and PMOS symbols used when the substrate connection is nonstandard, with the body terminal labeled as B.
image_name:Figure 1.32 (c)
description:
[
name: M2, type: NMOS, ports: {S: S, D: D, G: G}
name: M3, type: PMOS, ports: {S: S, D: D, G: G}
]
extrainfo:Figure 1.32 (c) shows the symbols for depletion-mode NMOS and PMOS devices, where a channel forms for V_GS=0. These symbols are used to represent the devices in CMOS circuits where the substrate connection is non-standard.

Figure 1.32 (a) NMOS and PMOS symbols used in CMOS circuits. (b) NMOS and PMOS symbols used when the substrate connection is nonstandard. (c) Depletion MOS device symbols.
be shown. On the other hand, if the individual isolation regions are connected elsewhere, the devices will be represented by the symbols of Fig. 1.32b, where the substrate is labeled $B$. Finally, symbols for depletion-mode devices, for which a channel forms for $V_{G S}=0$, are shown in Fig. 1.32c.

### 1.5.3 Decomposition of Gate-Source Voltage

The gate-source voltage of a given MOS transistor is usually separated into two parts: the threshold, $V_{t}$, and the voltage over the threshold, $V_{G S}-V_{t}$. We will refer to this latter part of the gate-source voltage as the overdrive. This decomposition is used because these two components of the gate-source voltage have different properties. Assuming square-law behavior as in (1.157), the overdrive is

$$
\begin{equation*}
V_{o v}=V_{G S}-V_{t}=\sqrt{\frac{2 I_{D}}{k^{\prime}(W / L)}} \tag{1.166}
\end{equation*}
$$

Since the transconductance parameter $k^{\prime}$ is proportional to mobility, and since mobility falls with increasing temperature, the overdrive rises with temperature. In contrast, the next section shows that the threshold falls with increasing temperature. Furthermore, (1.140) shows that the threshold depends on the source-body voltage, but not on the current; (1.166) shows that the overdrive depends directly on the current, but not on the source-body voltage.

### 1.5.4 Threshold Temperature Dependence

Assume that the source-body voltage is zero. Substituting (1.138) into (1.139) gives

$$
\begin{equation*}
V_{t}=\frac{\sqrt{2 q N_{A} \epsilon\left(2 \phi_{f}\right)}}{C_{o x}}+2 \phi_{f}+\phi_{m s}-\frac{Q_{s s}}{C_{o x}} \tag{1.167}
\end{equation*}
$$

Assume that $\phi_{m s}, Q_{s s}$, and $C_{o x}$ are independent of temperature. ${ }^{19}$ Then differentiating (1.167) gives

$$
\begin{equation*}
\frac{d V_{t}}{d T}=\frac{\sqrt{2 q N_{A} \epsilon(2)}}{2 C_{o x} \sqrt{\phi_{f}}} \frac{d \phi_{f}}{d T}+2 \frac{d \phi_{f}}{d T}=\frac{d \phi_{f}}{d T}\left[2+\frac{1}{C_{o x}} \sqrt{\frac{q N_{A} \epsilon}{\phi_{f}}}\right] \tag{1.168}
\end{equation*}
$$

Substituting (1.136) into (1.135) gives

$$
\begin{equation*}
\phi_{f}=\frac{k T}{q} \ln \left[\frac{N_{A} \exp \left(\frac{E_{g}}{2 k T}\right)}{\sqrt{N_{c} N_{v}}}\right] \tag{1.169}
\end{equation*}
$$

Assume both $N_{c}$ and $N_{v}$ are independent of temperature. ${ }^{20}$ Then differentiating (1.169) gives

$$
\begin{equation*}
\frac{d \phi_{f}}{d T}=\frac{k T}{q}\left[-\frac{E_{g}}{2 k T^{2}}\right]+\frac{k}{q} \ln \left[\frac{N_{A} \exp \left(\frac{E_{g}}{2 k T}\right)}{\sqrt{N_{c} N_{v}}}\right] \tag{1.170}
\end{equation*}
$$

Substituting (1.169) into (1.170) and simplifying gives

$$
\begin{equation*}
\frac{d \phi_{f}}{d T}=-\frac{E_{g}}{2 q T}+\frac{\phi_{f}}{T}=-\frac{1}{T}\left[\frac{E_{g}}{2 q}-\phi_{f}\right] \tag{1.171}
\end{equation*}
$$

Substituting (1.141) and (1.171) into (1.168) gives

$$
\begin{equation*}
\frac{d V_{t}}{d T}=-\frac{1}{T}\left[\frac{E_{g}}{2 q}-\phi_{f}\right]\left[2+\frac{\gamma}{\sqrt{2 \phi_{f}}}\right] \tag{1.172}
\end{equation*}
$$

Equation 1.172 shows that the threshold voltage falls with increasing temperature if $\phi_{f}<$ $E_{g} /(2 q)$. The slope is usually in the range of $-0.5 \mathrm{mV} /{ }^{\circ} \mathrm{C}$ to $-4 \mathrm{mV} /{ }^{\circ} \mathrm{C} .{ }^{21}$

#### EXAMPLE

Assume $T=300^{\circ} \mathrm{K}, N_{A}=10^{15} \mathrm{~cm}^{-3}$, and $t_{o x}=100 \AA$. Find $d V_{t} / d T$.
From (1.135),

$$
\begin{equation*}
\phi_{f}=(25.8 \mathrm{mV}) \ln \left(\frac{10^{15} \mathrm{~cm}^{-3}}{1.45 \times 10^{10} \mathrm{~cm}^{-3}}\right)=287 \mathrm{mV} \tag{1.173}
\end{equation*}
$$

Also

$$
\begin{equation*}
\frac{E_{g}}{2 q}=\frac{1.12 \mathrm{eV}}{2 q}=0.56 \mathrm{~V} \tag{1.174}
\end{equation*}
$$

Substituting (1.173) and (1.174) into (1.171) gives

$$
\begin{equation*}
\frac{d \phi_{f}}{d T}=-\frac{1}{300}(560-287) \frac{\mathrm{mV}}{{ }^{\circ} \mathrm{K}}=-0.91 \frac{\mathrm{mV}}{{ }^{\circ} \mathrm{K}} \tag{1.175}
\end{equation*}
$$

From (1.142),

$$
\begin{equation*}
C_{o x}=\frac{3.9\left(8.854 \times 10^{-14} \mathrm{~F} / \mathrm{cm}\right)}{100 \times 10^{-8} \mathrm{~cm}}=3.45 \frac{\mathrm{fF}}{\mu \mathrm{~m}^{2}} \tag{1.176}
\end{equation*}
$$

Also,

$$
\begin{align*}
\frac{\gamma}{\sqrt{2 \phi_{f}}} & =\frac{1}{C_{o x}} \sqrt{\frac{(2)\left(1.6 \times 10^{-19} \mathrm{C}\right)(11.7)\left(8.854 \times 10^{-14} \mathrm{~F} / \mathrm{cm}\right)\left(10^{15} \mathrm{~cm}^{-3}\right)}{(2)(0.287 \mathrm{~V})}} \\
& =\frac{2.4 \times 10^{-8} \mathrm{~F} / \mathrm{cm}^{2}}{3.45 \times 10^{-15} \mathrm{~F} / \mathrm{mm}^{2}}=\frac{2.4 \times 10^{-16} \mathrm{~F} / \mu \mathrm{m}^{2}}{3.45 \times 10^{-15} \mathrm{~F} / \mu \mathrm{m}^{2}}=0.07 \tag{1.177}
\end{align*}
$$

Substituting (1.173) - (1.177) into (1.172) gives

$$
\begin{equation*}
\frac{d V_{t}}{d T}=\left(-0.91 \frac{\mathrm{mV}}{{ }^{\circ} \mathrm{K}}\right)(2+0.07) \simeq-1.9 \frac{\mathrm{mV}}{{ }^{\circ} \mathrm{K}}=-1.9 \frac{\mathrm{mV}}{{ }^{\circ} \mathrm{C}} \tag{1.178}
\end{equation*}
$$

### 1.5.5 MOS Device Voltage Limitations

The main voltage limitations in MOS transistors are described next. ${ }^{22,23}$ Some of these limitations have a strong dependence on the gate length $L$; others have little dependence on $L$. Also, some of the voltage limitations are inherently destructive; others cause no damage as long as overheating is avoided.

Junction Breakdown. For long channel lengths, the drain-depletion region has little effect on the channel, and the $I_{D}$-versus- $V_{D S}$ curves closely follow the ideal curves of Fig. 1.29. For increasing $V_{D S}$, however, eventually the drain-substrate $p n$-junction breakdown voltage is exceeded, and the drain current increases abruptly by avalanche breakdown as described in Section 1.2 .2. This phenomenon is not inherently destructive.

Punchthrough. If the depletion region around the drain in an MOS transistor touches the depletion region around the source before junction breakdown occurs, increasing the drainsource voltage increases the drain current by reducing the barrier to electron flow between the source and drain. This phenomenon is called punchthrough. Since it depends on the two depletion regions touching, it also depends on the gate length. Punchthrough is not inherently destructive and causes a more gradual increase in the drain current than is caused by avalanche breakdown. Punchthrough normally occurs below the surface of the silicon and is often prevented by an extra ion implantation below the surface to reduce the size of the depletion regions.

Hot Carriers. With sufficient horizontal or vertical electric fields, electrons or holes may reach sufficient velocities to be injected into the oxide, where most of them increase the gate current and some of them become trapped. Such carriers are called hot because the required velocity for injection into the oxide is usually greater than the random thermal velocity. Carriers trapped in the oxide shift the threshold voltage and may cause a transistor to remain on when it should turn off or vice versa. In this sense, injection of hot carriers into the oxide is a destructive process. This process is most likely to be problematic in short-channel technologies, where horizontal electric fields are likely to be high.

Oxide Breakdown. In addition to $V_{D S}$ limitations, MOS devices must also be protected against excessive gate voltages. Typical gate oxides break down with an electric field of about $6 \times 10^{6} \mathrm{~V} / \mathrm{cm}$ to $7 \times 10^{6} \mathrm{~V} / \mathrm{cm},{ }^{24,25}$ which corresponds to 6 to 7 V applied from gate to channel with an oxide thickness of 100 angstroms. Since this process depends on the vertical electrical field, it is independent of channel length. However, this process is destructive to the transistor, resulting in resistive connections between the gate and the channel. Oxide breakdown can be caused by static electricity and can be avoided by using pn diodes and resistors to limit the voltage range at sensitive nodes internal to the integrated circuit that connect to bonding pads.

## 1.6 Small-Signal Models of MOS Transistors

As mentioned in Section 1.5, MOS transistors are often used in analog circuits. To simplify the calculation of circuit gain and terminal impedances, small-signal models can be used. As in the case for bipolar transistors, a hierarchy of models with increasing complexity can be derived, and choosing the simplest model required to do a given analysis is important in practice.

Consider the MOS transistor in Fig. 1.33 with bias voltages $V_{G S}$ and $V_{D D}$ applied as shown. These bias voltages produce quiescent drain current $I_{D}$. If $V_{G S}>V_{t}$ and $V_{D D}>\left(V_{G S}-V_{t}\right)$, the device operates in the saturation or active region. A small-signal input voltage $v_{i}$ is applied in series with $V_{G S}$ and produces a small variation in drain current $i_{d}$. The total value of the drain current is $I_{d}=\left(I_{D}+i_{d}\right)$.
image_name:Figure 1.33
description:
[
name: M1, type: NMOS, ports: {S: GND, D: VDD, G: g1}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: vi, type: VoltageSource, value: vi, ports: {Np: g1, Nn: VGS}
name: VGS, type: VoltageSource, value: VGS, ports: {Np: VGS, Nn: GND}
]
extrainfo:The circuit is a common-source NMOS amplifier with a biasing network. The input voltage vi is applied to the gate of the NMOS transistor M1, and the drain is connected to VDD. The source is grounded. The total drain current is given by Id = ID + id.

Figure 1.33 Schematic of an MOS transistor with biasing.

### 1.6.1 Transconductance

Assuming square-law operation, the transconductance from the gate can be determined from (1.165) by differentiating

$$
\begin{equation*}
g_{m}=\frac{\partial I_{D}}{\partial V_{G S}}=k^{\prime} \frac{W}{L}\left(V_{G S}-V_{t}\right)\left(1+\lambda V_{D S}\right) \tag{1.179}
\end{equation*}
$$

If $\lambda V_{D S} \ll 1,(1.179)$ simplifies to

$$
\begin{equation*}
g_{m}=k^{\prime} \frac{W}{L}\left(V_{G S}-V_{t}\right)=\sqrt{2 k^{\prime} \frac{W}{L} I_{D}} \tag{1.180}
\end{equation*}
$$

Unlike the bipolar transistor, the transconductance of the MOS transistor is proportional to the square root of the bias current and depends on device geometry (oxide thickness via $k^{\prime}$ and $W / L)$. Another key difference between bipolar and MOS transistors can be seen by calculating the ratio of the transconductance to the current. Using (1.157) and (1.180) for MOS transistors shows that

$$
\begin{equation*}
\frac{g_{m}}{I_{D}}=\frac{2}{V_{G S}-V_{t}}=\frac{2}{V_{o v}} \tag{1.181}
\end{equation*}
$$

Also, for bipolar transistors, (1.91) shows that

$$
\begin{equation*}
\frac{g_{m}}{I_{C}}=\frac{q}{k T}=\frac{1}{V_{T}} \tag{1.182}
\end{equation*}
$$

At room temperature, the thermal voltage $V_{T}$ is about equal to 26 mV . In contrast, the overdrive $V_{o v}$ for MOS transistors in many applications is chosen to be approximately several hundred mV so that MOS transistors are fast enough for the given application. (Section 1.6.8 shows that the transition frequency $f_{T}$ of an MOS transistor is proportional to the overdrive.) Under these conditions, the transconductance per given current is much higher for bipolar transistors than for MOS transistors. One of the key challenges in MOS analog circuit design is designing high-quality analog circuits with a low transconductance-to-current ratio.

The transconductance calculated in (1.180) is valid for small-signal analysis. To determine the limitation on the use of small-signal analysis, the change in the drain current resulting from a change in the gate-source voltage will be derived from a large-signal standpoint. The total drain current in Fig. 1.33 can be calculated using (1.157) as

$$
\begin{equation*}
I_{d}=\frac{k^{\prime}}{2} \frac{W}{L}\left(V_{G S}+v_{i}-V_{t}\right)^{2}=\frac{k^{\prime}}{2} \frac{W}{L}\left[\left(V_{G S}-V_{t}\right)^{2}+2\left(V_{G S}-V_{t}\right) v_{i}+v_{i}^{2}\right] \tag{1.183}
\end{equation*}
$$

Substituting (1.157) in (1.183) gives

$$
\begin{equation*}
I_{d}=I_{D}+\frac{k^{\prime}}{2} \frac{W}{L}\left[2\left(V_{G S}-V_{t}\right) v_{i}+v_{i}^{2}\right] \tag{1.184}
\end{equation*}
$$

Rearranging (1.184) gives

$$
\begin{equation*}
i_{d}=I_{d}-I_{D}=k^{\prime} \frac{W}{L}\left(V_{G S}-V_{t}\right) v_{i}\left[1+\frac{v_{i}}{2\left(V_{G S}-V_{t}\right)}\right] \tag{1.185}
\end{equation*}
$$

If the magnitude of the small-signal input $\left|v_{i}\right|$ is much less than twice the overdrive defined in (1.166), substituting (1.180) into (1.185) gives

$$
\begin{equation*}
i_{d} \simeq g_{m} v_{i} \tag{1.186}
\end{equation*}
$$

In particular, if $\left|v_{i}\right|=\left|\Delta V_{G S}\right|$ is less than 20 percent of the overdrive, the small-signal analysis is accurate within about 10 percent.

### 1.6.2 Intrinsic Gate-Source and Gate-Drain Capacitance

If $C_{o x}$ is the oxide capacitance per unit area from gate to channel, then the total capacitance under the gate is $C_{o x} W L$. This capacitance is intrinsic to the device operation and models the gate control of the channel conductance. In the triode region of device operation, the channel exists continuously from source to drain, and the gate-channel capacitance is usually lumped into two equal parts at the drain and source with

$$
\begin{equation*}
C_{g s}=C_{g d}=\frac{C_{o x} W L}{2} \tag{1.187}
\end{equation*}
$$

In the saturation or active region, however, the channel pinches off before reaching the drain, and the drain voltage exerts little influence on either the channel or the gate charge. As a consequence, the intrinsic portion of $C_{g d}$ is essentially zero in the saturation region. To calculate the value of the intrinsic part of $C_{g s}$ in the saturation or active region, we must calculate the total charge $Q_{T}$ stored in the channel. This calculation can be carried out by substituting (1.145) into (1.144) and integrating to obtain

$$
\begin{equation*}
Q_{T}=W C_{o x} \int_{0}^{L}\left[V_{G S}-V(y)-V_{t}\right] d y \tag{1.188}
\end{equation*}
$$

Solving (1.150) for $d y$ and substituting into (1.188) gives

$$
\begin{equation*}
Q_{T}=\frac{W^{2} C_{o x}^{2} \mu_{n}}{I_{D}} \int_{0}^{V_{G S}-V_{t}}\left(V_{G S}-V-V_{t}\right)^{2} d V \tag{1.189}
\end{equation*}
$$

where the limit $y=L$ corresponds to $V=\left(V_{G S}-V_{t}\right)$ in the saturation or active region. Solution of (1.189) and use of (1.153) and (1.157) gives

$$
\begin{equation*}
Q_{T}=\frac{2}{3} W L C_{o x}\left(V_{G S}-V_{t}\right) \tag{1.190}
\end{equation*}
$$

Therefore, in the saturation or active region,

$$
\begin{equation*}
C_{g s}=\frac{\partial Q_{T}}{\partial V_{G S}}=\frac{2}{3} W L C_{o x} \tag{1.191}
\end{equation*}
$$

and

$$
\begin{equation*}
C_{g d}=0 \tag{1.192}
\end{equation*}
$$

### 1.6.3 Input Resistance

The gate of an MOS transistor is insulated from the channel by the $\mathrm{SiO}_{2}$ dielectric. As a result, the low-frequency gate current is essentially zero and the input resistance is essentially infinite. This characteristic is important in some circuits such as sample-and-hold amplifiers, where the gate of an MOS transistor can be connected to a capacitor to sense the voltage on the capacitor without leaking away the charge that causes that voltage. In contrast, bipolar transistors have small but nonzero base current and finite input resistance looking into the base, complicating the design of bipolar sample-and-hold amplifiers.

### 1.6.4 Output Resistance

In Section 1.5.1, the effect of changes in drain-source voltage on the large-signal characteristics of the MOS transistor was described. Increasing drain-source voltage in an $n$-channel MOS transistor increases the width of the depletion region around the drain and reduces the effective channel length of the device in the saturation or active region. This effect is called channellength modulation and causes the drain current to increase when the drain-source voltage is increased. From that treatment, we can calculate the change in the drain current $\Delta I_{D}$ arising from changes in the drain-source voltage $\Delta V_{D S}$ as

$$
\begin{equation*}
\Delta I_{D}=\frac{\partial I_{D}}{\partial V_{D S}} \Delta V_{D S} \tag{1.193}
\end{equation*}
$$

Substitution of (1.161), (1.163), and (1.164) in (1.193) gives

$$
\begin{equation*}
\frac{\Delta V_{D S}}{\Delta I_{D}}=\frac{V_{A}}{I_{D}}=\frac{1}{\lambda I_{D}}=r_{o} \tag{1.194}
\end{equation*}
$$

where $V_{A}$ is the Early voltage, $\lambda$ is the channel-length modulation parameter, $I_{D}$ is the drain current without channel-length modulation given by (1.157), and $r_{o}$ is the small-signal output resistance of the transistor.

### 1.6.5 Basic Small-Signal Model of the MOS Transistor

Combination of the preceding small-signal circuit elements yields the small-signal model of the MOS transistor shown in Fig. 1.34. This model was derived for $n$-channel transistors in the saturation or active region and is called the hybrid- $\pi$ model. Drain, gate, and source nodes are labeled $D, G$, and $S$, respectively. When the gate-source voltage is increased, the model predicts that the incremental current $i_{d}$ flowing from drain to source increases. Since the dc drain current $I_{D}$ also flows from drain to source in an $n$-channel transistor, increasing the gatesource voltage also increases the total drain current $I_{d}$. This result is reasonable physically because increasing the gate-source voltage in an $n$-channel transistor increases the channel conductivity and drain current.
image_name:Figure 1.34
description:
[
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: G, Nn: S}
name: gm*vgs, type: VoltageControledCurrentSource, value: gm*vgs, ports: {Np: D, Nn: S}
name: ro, type: Resistor, value: ro, ports: {N1: D, N2: S}
]
extrainfo:The circuit diagram represents a small-signal model of an MOS transistor in saturation or active region, showing the relationship between gate-source voltage and drain current.

Figure 1.34 Basic small-signal model of an MOS transistor in the saturation or active region.

The model shown in Fig. 1.34 is also valid for $p$-channel devices. Therefore, the model again shows that increasing the gate-source voltage increases the incremental current $i_{d}$ flowing from drain to source. Unlike in the $n$-channel case, however, the dc current $I_{D}$ in a $p$-channel transistor flows from source to drain because the source acts as the source of holes. Therefore, the incremental drain current flows in a direction opposite to the dc drain current when the gate-source voltage increases, reducing the total drain current $I_{d}$. This result is reasonable physically because increasing the gate-source voltage in a $p$-channel transistor reduces the channel conductivity and drain current.

### 1.6.6 Body Transconductance

The drain current is a function of both the gate-source and body-source voltages. On the one hand, the gate-source voltage controls the vertical electric field, which controls the channel conductivity and therefore the drain current. On the other hand, the body-source voltage changes the threshold, which changes the drain current when the gate-source voltage is fixed. This effect stems from the influence of the substrate acting as a second gate and is called the body effect. Note that the body of an MOS transistor is usually connected to a constant power-supply voltage, which is a small-signal or ac ground. However, the source connection can have a significant ac voltage impressed on it, which changes the body-source voltage when the body voltage is fixed. Therefore, when the body-source voltage is not constant, two transconductance terms are required to model MOS transistors: one associated with the main gate and the other associated with the body or second gate.

Using (1.165), the transconductance from the body or second gate is

$$
\begin{equation*}
g_{m b}=\frac{\partial I_{D}}{\partial V_{B S}}=-k^{\prime} \frac{W}{L}\left(V_{G S}-V_{t}\right)\left(1+\lambda V_{D S}\right) \frac{\partial V_{t}}{\partial V_{B S}} \tag{1.195}
\end{equation*}
$$

From (1.140)

$$
\begin{equation*}
\frac{\partial V_{t}}{\partial V_{B S}}=-\frac{\gamma}{2 \sqrt{2 \phi_{f}+V_{S B}}}=-\chi \tag{1.196}
\end{equation*}
$$

This equation defines a factor $\chi$, which is the rate of change of threshold voltage with body bias voltage. Substitution of (1.141) in (1.196) and use of (1.20) gives

$$
\begin{equation*}
\chi=\frac{C_{j s}}{C_{o x}} \tag{1.197}
\end{equation*}
$$

where $C_{j s}$ is the capacitance per unit area of the depletion region under the channel, assuming a one-sided step junction with a built-in potential $\psi_{0}=2 \phi_{f}$. Substitution of (1.196) in (1.195) gives

$$
\begin{equation*}
g_{m b}=\frac{\gamma k^{\prime}(W / L)\left(V_{G S}-V_{t}\right)\left(1+\lambda V_{D S}\right)}{2 \sqrt{2 \phi_{f}+V_{S B}}} \tag{1.198}
\end{equation*}
$$

If $\lambda V_{D S} \ll 1$, we have

$$
\begin{equation*}
g_{m b}=\frac{\gamma k^{\prime}(W / L)\left(V_{G S}-V_{t}\right)}{2 \sqrt{2 \phi_{f}+V_{S B}}}=\gamma \sqrt{\frac{k^{\prime}(W / L) I_{D}}{2\left(2 \phi_{f}+V_{S B}\right)}} \tag{1.199}
\end{equation*}
$$

The ratio $g_{m b} / g_{m}$ is an important quantity in practice. From (1.179) and (1.198), we find

$$
\begin{equation*}
\frac{g_{m b}}{g_{m}}=\frac{\gamma}{2 \sqrt{2 \phi_{f}+V_{S B}}}=\chi \tag{1.200}
\end{equation*}
$$

The factor $\chi$ is typically in the range 0.1 to 0.3 ; therefore, the transconductance from the main gate is typically a factor of about 3 to 10 times larger than the transconductance from the body or second gate.

### 1.6.7 Parasitic Elements in the Small-Signal Model

The elements of the small-signal model for MOS transistors described above may be considered basic in the sense that they arise directly from essential processes in the device. As in the case of bipolar transistors, however, technological limitations in the fabrication of the devices give rise to a number of parasitic elements that must be added to the equivalent circuit for most integrated-circuit transistors. A cross section and top view of a typical $n$-channel MOS transistor are shown in Fig. 1.35. The means of fabricating such devices is described in Chapter 2.

All pn junctions in the MOS transistor should be reverse biased during normal operation, and each junction exhibits a voltage-dependent parasitic capacitance associated with its depletion region. The source-body and drain-body junction capacitances shown in Fig. 1.35a are $C_{s b}$ and $C_{d b}$, respectively. If the doping levels in the source, drain, and body regions are assumed to be constant, (1.21) can be used to express these capacitances as follows:

$$
\begin{align*}
C_{s b} & =\frac{C_{s b 0}}{\left(1+\frac{V_{S B}}{\psi_{0}}\right)^{1 / 2}}  \tag{1.201}\\
C_{d b} & =\frac{C_{d b 0}}{\left(1+\frac{V_{D B}}{\psi_{0}}\right)^{1 / 2}} \tag{1.202}
\end{align*}
$$

These capacitances are proportional to the source and drain region areas (including sidewalls). Since the channel is attached to the source in the saturation or active region, $C_{s b}$ also includes
image_name:Figure 1.35 (a)
description:The image consists of two parts labeled as Figure 1.35 (a) and (b), representing different views of an n-channel MOS transistor.

1. **Identification of Components and Structure:**
- **Figure 1.35 (a):** This is a cross-sectional view of an n-channel MOS transistor. It shows the following components:
- **Source (S):** Labeled on the left, connected to an n+ doped region.
- **Gate (G):** Positioned above the channel, connected to a metal or polysilicon layer.
- **Drain (D):** Labeled on the right, connected to another n+ doped region.
- **Body (B):** The p-type substrate, with a p+ doped region for body contact.
- **Capacitances (C_ol, C_sb, C_db):** Indicated between the gate and channel (C_ol), source and body (C_sb), and drain and body (C_db).
- **p-type Substrate (p):** The central region where the channel forms.

2. **Connections and Interactions:**
- The source and drain are connected through n+ regions, forming the channel under the gate.
- The gate controls the channel conductivity by applying a voltage, influencing the flow of current between the source and drain.
- Capacitances such as C_ol, C_sb, and C_db represent the capacitance between the gate and channel, source and body, and drain and body, respectively.

3. **Labels, Annotations, and Key Features:**
- **Figure 1.35 (b):** This is the top view of the n-channel MOS transistor.
- **Source (S), Gate (G), Drain (D):** Clearly marked.
- **Channel Width (W) and Length (L):** Indicated by arrows, showing the dimensions of the channel.
- **Capacitance (C_gb):** Shown between the gate and body.
- **Body (B):** Labeled on the right, indicating the connection to the body.

Overall, this diagram provides a detailed representation of the structure and electrical connections within an n-channel MOS transistor, highlighting the key components and capacitances involved in its operation.
image_name:Figure 1.35 (b)
description:Figure 1.35 (b) presents a top view of an n-channel MOS transistor. This diagram illustrates the layout of the transistor, highlighting key components and their spatial relationships.

1. **Identification of Components and Structure:**
- **Source (S):** Represented on the left side of the diagram, it connects to the channel region. The source is typically where carriers (electrons for n-channel) enter the channel.
- **Gate (G):** Positioned centrally, the gate controls the flow of carriers in the channel by applying a voltage. It is shown as a rectangular area covering the channel.
- **Drain (D):** Located on the right side, opposite the source, the drain is where carriers exit the channel.
- **Body (B):** The body is connected to the substrate and is shown connected to the gate via a capacitance labeled as \( C_{gb} \).

2. **Connections and Interactions:**
- The diagram shows the gate overlapping the channel between the source and drain, indicating its role in modulating the channel conductivity.
- The length \( L \) and width \( W \) of the channel are marked, which are critical dimensions affecting the transistor's electrical characteristics.
- The gate forms a capacitor with the body, represented by \( C_{gb} \), which influences the threshold voltage and overall device behavior.

3. **Labels, Annotations, and Key Features:**
- \( C_{gb} \): Capacitance between the gate and body, crucial for understanding the device's electrical properties.
- \( L \): Channel length, a key parameter in determining the transistor's speed and current-carrying capacity.
- \( W \): Channel width, affecting the current drive capability of the transistor.

This top view complements the cross-section view (Figure 1.35 (a)) by providing a spatial perspective on how the source, gate, and drain are arranged, and how the gate overlaps the channel to control current flow.
Figure 1.35 (a) Cross section and (b) top view of an $n$-channel MOS transistor.

image_name:Figure 1.36 Small-signal MOS transistor equivalent circuit
description:
[
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: G, Nn: S}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: G, Nn: D}
name: Cgb, type: Capacitor, value: Cgb, ports: {Np: G, Nn: B}
name: Csb, type: Capacitor, value: Csb, ports: {Np: B, Nn: S}
name: Cdb, type: Capacitor, value: Cdb, ports: {Np: D, Nn: B}
name: 8mVgs, type: VoltageControlledCurrentSource, ports: {Np: D, Nn: S}
name: gmbVbs, type: VoltageControlledCurrentSource, ports: {Np: D, Nn: S}
name: ro, type: Resistor, value: ro, ports: {N1: D, N2: S}
]
extrainfo:This is a small-signal model of an NMOS transistor showing various capacitances and controlled current sources representing the transistor's behavior. The circuit illustrates the interaction between gate, source, drain, and body terminals.
Figure 1.36 Small-signal MOS transistor equivalent circuit.
depletion-region capacitance from the induced channel to the body. A detailed analysis of the channel-body capacitance is given by Tsividis. ${ }^{26}$

In practice, $C_{g s}$ and $C_{g d}$, given in (1.187) for the triode region of operation and in (1.191) and (1.192) for the saturation or active region, are increased due to parasitic oxide capacitances arising from gate overlap of the source and drain regions. These overlap capacitances $C_{o l}$ are shown in Fig. 1.35a, and their values are calculated in Chapter 2.

Capacitance $C_{g b}$ between gate and body or substrate models parasitic oxide capacitance between the gate-contact material and the substrate outside the active-device area. This capacitance is independent of the gate-body voltage and models coupling from polysilicon and metal interconnects to the underlying substrate, as shown by the shaded regions in the top view of Fig. 1.35b. Parasitic capacitance of this type underlies all polysilicon and metal traces on integrated circuits. Such parasitic capacitance should be taken into account when simulating and calculating high-frequency circuit and device performance. Typical values depend on oxide thicknesses. With a silicon dioxide thickness of $100 \AA$, the capacitance is about 3.45 fF per square micron. Fringing capacitance becomes important for lines narrower in width than several microns.

Parasitic resistance in series with the source and drain can be used to model the nonzero resistivity of the contacts and diffusion regions. In practice, these resistances are often ignored in hand calculations for simplicity but included in computer simulations. These parasitic resistances have an inverse dependence on channel width $W$. Typical values of these resistances are $50 \Omega$ to $100 \Omega$ for devices with $W$ of about $1 \mu \mathrm{~m}$. Similar parasitic resistances in series with the gate and body terminals are sometimes included but often ignored because very little current flows in these terminals, especially at low frequencies. The small-signal model including capacitive parasitics but ignoring resistive parasitics is shown in Fig. 1.36.

### 1.6.8 MOS Transistor Frequency Response

As for a bipolar transistor, the frequency capability of an MOS transistor is usually specified by finding the transition frequency $f_{T}$. For an MOS transistor, $f_{T}$ is defined as the frequency where the magnitude of the short-circuit, common-source current gain falls to unity. Although the dc gate current of an MOS transistor is essentially zero, the high-frequency behavior of the transistor is controlled by the capacitive elements in the small-signal model, which cause the gate current to increase as frequency increases. To calculate $f_{T}$, consider the ac circuit of Fig. 1.37a and the small-signal equivalent of Fig. 1.37b. Since $v_{s b}=v_{d s}=0, g_{m b}$,
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: GND, G: vgs}
name: vgs, type: VoltageSource, value: vgs, ports: {Np: vgs, Nn: GND}
]
extrainfo:The circuit represents a small-signal model of an MOS transistor for calculating the cutoff frequency f_T. It includes capacitive elements that affect the high-frequency behavior.
image_name:(b)
description:
[
name: vgs, type: VoltageSource, value: vgs, ports: {Np: vgs, Nn: GND}
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: vgs, Nn: GND}
name: Cgb, type: Capacitor, value: Cgb, ports: {Np: vgs, Nn: GND}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: vgs, Nn: GND}
name: gmvgs, type: CurrentSource, value: gmvgs, ports: {Np: GND, Nn: GND}
]
extrainfo:The circuit represents the small-signal model for calculating the transition frequency fT of an MOS transistor. It includes the gate-source voltage source, capacitive elements, and the transconductance current source.
Figure 1.37 Circuits for calculating the $f_{T}$ of an MOS transistor: (a) ac schematic and (b) smallsignal equivalent.

$r_{o}, C_{s b}$, and $C_{d b}$ have no effect on the calculation and are ignored. The small-signal input current $i_{i}$ is

$$
\begin{equation*}
i_{i}=s\left(C_{g s}+C_{g b}+C_{g d}\right) v_{g s} \tag{1.203}
\end{equation*}
$$

If the current fed forward through $C_{g d}$ is neglected,

$$
\begin{equation*}
i_{o} \simeq g_{m} v_{g s} \tag{1.204}
\end{equation*}
$$

Solving (1.203) for $v_{g s}$ and substituting into (1.204) gives

$$
\begin{equation*}
\frac{i_{o}}{i_{i}} \simeq \frac{g_{m}}{s\left(C_{g s}+C_{g b}+C_{g d}\right)} \tag{1.205}
\end{equation*}
$$

To find the frequency response, we set $s=j \omega$. Then

$$
\begin{equation*}
\frac{i_{o}}{i_{i}} \simeq \frac{g_{m}}{j \omega\left(C_{g s}+C_{g b}+C_{g d}\right)} \tag{1.206}
\end{equation*}
$$

The magnitude of the small-signal current gain is unity when

$$
\begin{equation*}
\omega=\omega_{T}=\frac{g_{m}}{C_{g s}+C_{g b}+C_{g d}} \tag{1.207}
\end{equation*}
$$

Therefore,

$$
\begin{equation*}
f_{T}=\frac{1}{2 \pi} \omega_{T}=\frac{1}{2 \pi} \frac{g_{m}}{C_{g s}+C_{g b}+C_{g d}} \tag{1.208}
\end{equation*}
$$

Assume the intrinsic device capacitance $C_{g s}$ is much greater than $\left(C_{g b}+C_{g d}\right)$. Then substituting (1.180) and (1.191) into (1.208) gives

$$
\begin{equation*}
f_{T}=1.5 \frac{\mu_{n}}{2 \pi L^{2}}\left(V_{G S}-V_{t}\right) \tag{1.209}
\end{equation*}
$$

Comparison of this equation with the intrinsic $f_{T}$ of a bipolar transistor when parasitic depletion-layer capacitance is neglected leads to an interesting result. From (1.128) and (1.130) with $\tau_{F} \gg\left(C_{j e}+C_{\mu}\right) / g_{m}$,

$$
\begin{equation*}
f_{T}=\frac{1}{2 \pi \tau_{F}} \tag{1.210}
\end{equation*}
$$

Substituting from (1.99) for $\tau_{F}$ and using the Einstein relationship $D_{n} / \mu_{n}=k T / q=V_{T}$, we find for a bipolar transistor

$$
\begin{equation*}
f_{T}=2 \frac{\mu_{n}}{2 \pi W_{B}^{2}} V_{T} \tag{1.211}
\end{equation*}
$$

The similarity in form between (1.211) and (1.209) is striking. In both cases, the intrinsic device $f_{T}$ increases as the inverse square of the critical device dimension across which carriers are in transit. The voltage $V_{T}=26 \mathrm{mV}$ is fixed for a bipolar transistor, but the $f_{T}$ of an MOS transistor can be increased by operating at high values of $\left(V_{G S}-V_{t}\right)$. Note that the base width $W_{B}$ in a bipolar transistor is a vertical dimension determined by diffusions or implants and can typically be made much smaller than the channel length $L$ of an MOS transistor, which depends on surface geometry and photolithographic processes. Thus bipolar transistors generally have higher $f_{T}$ than MOS transistors made with comparable processing. Finally, (1.209) was derived assuming that the MOS transistor exhibits square-law behavior as in (1.157). However, as described in Section 1.7, submicron MOS transistors depart significantly from square-law characteristics, and we find that for such devices $f_{T}$ is proportional to $L^{-1}$ rather than $L^{-2}$.

#### EXAMPLE

Derive the complete small-signal model for an NMOS transistor with $I_{D}=100 \mu \mathrm{~A}, V_{S B}=$ $1 \mathrm{~V}, V_{D S}=2 \mathrm{~V}$. Device parameters are $\phi_{f}=0.3 \mathrm{~V}, W=10 \mu \mathrm{~m}, L=1 \mu \mathrm{~m}, \gamma=0.5 \mathrm{~V}^{1 / 2}$, $k^{\prime}=200 \mu \mathrm{~A} / \mathrm{V}^{2}, \lambda=0.02 \mathrm{~V}^{-1}, t_{o x}=100$ angstroms, $\psi_{0}=0.6 \mathrm{~V}, C_{s b 0}=C_{d b 0}=10 \mathrm{fF}$. Overlap capacitance from gate to source and gate to drain is 1 fF . Assume $C_{g b}=5 \mathrm{fF}$.

From (1.166),

$$
V_{o v}=V_{G S}-V_{t}=\sqrt{\frac{2 I_{D}}{k^{\prime}(W / L)}}=\sqrt{\frac{2 \times 100}{200 \times 10}} \simeq 0.316 \mathrm{~V}
$$

Since $V_{D S}>V_{o v}$, the transistor operates in the saturation or active region. From (1.180),

$$
g_{m}=\sqrt{2 k^{\prime} \frac{W}{L} I_{D}}=\sqrt{2 \times 200 \times 10 \times 100} \mu \mathrm{~A} / \mathrm{V} \simeq 632 \mu \mathrm{~A} / \mathrm{V}
$$

From (1.199),

$$
g_{m b}=\gamma \sqrt{\frac{k^{\prime}(W / L) I_{D}}{2\left(2 \phi_{f}+V_{S B}\right)}}=0.5 \sqrt{\frac{200 \times 10 \times 100}{2 \times 1.6}} \simeq 125 \mu \mathrm{~A} / \mathrm{V}
$$

From (1.194),

$$
r_{o}=\frac{1}{\lambda I_{D}}=\frac{1000}{0.02 \times 100} \mathrm{k} \Omega=500 \mathrm{k} \Omega
$$

Using (1.201) with $V_{S B}=1 V$, we find

$$
C_{s b}=\frac{10}{\left(1+\frac{1}{0.6}\right)^{1 / 2}} \mathrm{fF} \simeq 6 \mathrm{fF}
$$

The voltage from drain to body is

$$
V_{D B}=V_{D S}+V_{S B}=3 \mathrm{~V}
$$

and substitution in (1.202) gives

$$
C_{d b}=\frac{10}{\left(1+\frac{3}{0.6}\right)^{1 / 2}} \mathrm{fF} \simeq 4 \mathrm{fF}
$$

From (1.142), the oxide capacitance per unit area is

$$
C_{o x}=\frac{3.9 \times 8.854 \times 10^{-14} \frac{\mathrm{~F}}{\mathrm{~cm}} \times \frac{100 \mathrm{~cm}}{10^{6} \mu \mathrm{~m}}}{100 \AA \times \frac{10^{6} \mu \mathrm{~m}}{10^{10} \AA}} \simeq 3.45 \frac{\mathrm{fF}}{\mu \mathrm{~m}^{2}}
$$

The intrinsic portion of the gate-source capacitance can be calculated from (1.191), giving

$$
C_{g s} \simeq \frac{2}{3} \times 10 \times 1 \times 3.45 \mathrm{fF} \simeq 23 \mathrm{fF}
$$

The addition of overlap capacitance gives

$$
C_{g s} \simeq 24 \mathrm{fF}
$$

Finally, since the transistor operates in the saturation or active region, the gate-drain capacitance consists of only overlap capacitance and is

$$
C_{g d}=1 \mathrm{fF}
$$

The complete small-signal equivalent circuit is shown in Fig. 1.38. The $f_{T}$ of the device can be calculated from (1.208) as

$$
f_{T}=\frac{1}{2 \pi} \frac{g_{m}}{C_{g s}+C_{g b}+C_{g d}}=\frac{1}{2 \pi} \times 632 \times 10^{-6} \times \frac{10^{15}}{24+5+1} \mathrm{~Hz}=3.4 \mathrm{GHz}
$$

image_name:Figure 1.38
description:
[
name: C1, type: Capacitor, value: 24 fF, ports: {Np: G, Nn: S}
name: C2, type: Capacitor, value: 1 fF, ports: {Np: G, Nn: D}
name: C3, type: Capacitor, value: 5 fF, ports: {Np: G, Nn: B}
name: C4, type: Capacitor, value: 6 fF, ports: {Np: B, Nn: S}
name: C5, type: Capacitor, value: 4 fF, ports: {Np: D, Nn: GND}
name: I1, type: CurrentSource, value: 632 x 10^-6 x vgs, ports: {Np: D, Nn: S}
name: I2, type: CurrentSource, value: 125 x 10^-6 x vbs, ports: {Np: D, Nn: B}
name: R1, type: Resistor, value: 500 kΩ, ports: {N1: D, N2: GND}
]
extrainfo:This is a small-signal equivalent circuit for an NMOS transistor with specified capacitances and current sources modeling the transconductance and body effect. The circuit is used to analyze the frequency response and other characteristics of the transistor in a specific operating region.

Figure 1.38 Complete small-signal equivalent circuit for an NMOS transistor with $I_{D}=100 \mu \mathrm{~A}$,
$V_{S B}=1 \mathrm{~V}, V_{D S}=2 \mathrm{~V}$. Device parameters are $W=10 \mu \mathrm{~m}, L=1 \mu \mathrm{~m}, \gamma=0.5 \mathrm{~V}^{1 / 2}, k^{\prime}=200 \mu \mathrm{~A} / \mathrm{V}^{2}$, $\lambda=0.02 \mathrm{~V}^{-1}, t_{o x}=100 \AA, \psi_{0}=0.6 \mathrm{~V}, C_{s b 0}=C_{d b 0}=10 \mathrm{fF}, C_{g d}=1 \mathrm{fF}$, and $C_{g b}=5 \mathrm{fF}$.

## 1.7 Short-Channel Effects in MOS Transistors

The evolution of integrated-circuit processing techniques has led to continuing reductions in both the horizontal and vertical dimensions of the active devices. (The minimum allowed dimensions of passive devices have also decreased.) This trend is driven primarily by economics in that reducing dimensions increases the number of devices and circuits that can be processed at one time on a given wafer. A second benefit has been that the frequency capability of the active devices continues to increase, as intrinsic $f_{T}$ values increase with smaller dimensions while parasitic capacitances decrease.

Vertical dimensions such as the base width of a bipolar transistor in production processes may now be on the order of $0.05 \mu \mathrm{~m}$ or less, whereas horizontal dimensions such as bipolar emitter width or MOS transistor gate length may be significantly less than $1 \mu \mathrm{~m}$. Even with these small dimensions, the large-signal and small-signal models of bipolar transistors given in previous sections remain valid. However, significant short-channel effects become important in MOS transistors at channel lengths of about $1 \mu \mathrm{~m}$ or less and require modifications to the MOS models given previously. The primary effect is to modify the classical MOS square-law transfer characteristic in the saturation or active region to make the device voltage-to-current transfer characteristic more linear. However, even in processes with submicron capability, many of the MOS transistors in a given analog circuit may be deliberately designed to have channel lengths larger than the minimum and may be well approximated by the square-law model.

### 1.7.1 Velocity Saturation from the Horizontal Field

The most important short-channel effect in MOS transistors stems from velocity saturation of carriers in the channel. ${ }^{27}$ When an MOS transistor operates in the triode region, the average horizontal electric field along the channel is $V_{D S} / L$. When $V_{D S}$ is small and/or $L$ is large, the horizontal field is low, and the linear relation between carrier velocity and field assumed in (1.148) is valid. At high fields, however, the carrier velocities approach the thermal velocities, and subsequently the slope of the carrier velocity decreases with increasing field. This effect is illustrated in Fig. 1.39, which shows typical measured electron drift velocity $v_{d}$ versus horizontal electric field strength magnitude $\mathscr{E}_{8}$ in an NMOS surface channel. While the velocity at low field values is proportional to the field, the velocity at high field values approaches a constant called the scattering-limited velocity $v_{\text {scl }}$. A first-order analytical approximation to this curve is

$$
\begin{equation*}
v_{d}=\frac{\mu_{n} \mathscr{E}}{1+\mathscr{E} / \mathscr{E}_{c}} \tag{1.212}
\end{equation*}
$$

where $\mathscr{E}_{c} \simeq 1.5 \times 10^{6} \mathrm{~V} / \mathrm{m}$ and $\mu_{n} \simeq 0.07 \mathrm{~m}^{2} / \mathrm{V}$-s is the low-field mobility close to the gate. Equation 1.212 is also plotted in Fig. 1.39. From (1.212), as $\mathscr{E} \rightarrow \infty, v_{d} \rightarrow v_{s c l}=\mu_{n} \mathscr{E}_{c}$. At the critical field value $\mathscr{E}_{C}$, the carrier velocity is a factor of 2 less than the low-field formula would predict. In a device with a channel length $L=0.5 \mu \mathrm{~m}$, we need a voltage drop of only 0.75 V along the channel to produce an average field equal to $\mathscr{E}_{c}$, and this condition is readily achieved in short-channel MOS transistors. Similar results are found for PMOS devices.

Substituting (1.212) and (1.149) into (1.147) and rearranging gives

$$
\begin{equation*}
I_{D}\left(1+\frac{1}{\mathscr{E}_{c}} \frac{d V}{d y}\right)=W Q_{I}(y) \mu_{n} \frac{d V}{d y} \tag{1.213}
\end{equation*}
$$

image_name:Figure 1.39
description:The graph in "Figure 1.39" is a plot of electron drift velocity ($v_d$) versus the horizontal electric field ($\mathscr{E}$) in an MOS surface channel.

1. **Type of Graph and Function:**
- This is a line graph showing the relationship between two variables: drift velocity and electric field.

2. **Axes Labels and Units:**
- The x-axis represents the electric field $\mathscr{E}$, measured in volts per meter (V/m), with a logarithmic scale ranging from $5 \times 10^5$ to $10^7$ V/m.
- The y-axis represents the drift velocity $v_d$, measured in meters per second (m/s), with a logarithmic scale ranging from $10^4$ to $10^5$ m/s.

3. **Overall Behavior and Trends:**
- The solid line shows the typical measured electron drift velocity, which initially increases with the electric field. However, as the electric field continues to increase, the drift velocity begins to saturate, showing a slower rate of increase.
- The dashed line represents an analytical approximation of the drift velocity, which closely follows the measured values but shows a slightly different curvature, indicating the theoretical model.

4. **Key Features and Technical Details:**
- The graph shows a clear saturation behavior where the increase in drift velocity diminishes as the electric field becomes very large.
- The saturation occurs around an electric field of approximately $1.5 \times 10^6$ V/m, as indicated by the context.
- The solid line and dashed line converge at lower electric fields but diverge slightly at higher fields, reflecting the limitations of the analytical approximation.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for the saturation velocity $v_{scl}$, which is the maximum drift velocity approached as the electric field increases.
- There are no specific numeric data points marked on the graph, but the general trend and saturation level are clearly illustrated.

Figure 1.39 Typical measured electron drift velocity $v_{d}$ versus horizontal electric field $\mathscr{E}$ in an MOS surface channel (solid plot). Also shown (dashed plot) is the analytical approximation of Eq. 1.212 with $\mathscr{E}_{c}=1.5 \times 10^{6} \mathrm{~V} / \mathrm{m}$ and $\mu_{n}=0.07 \mathrm{~m}^{2} / \mathrm{V}$-s.

Note that as $\mathscr{E}_{c} \rightarrow \infty$ and velocity saturation becomes negligible, (1.213) approaches the original equation (1.147). Integrating (1.213) along the channel, we obtain

$$
\begin{equation*}
\int_{0}^{L} I_{D}\left(1+\frac{1}{\mathscr{E}_{c}} \frac{d V}{d y}\right) d y=\int_{0}^{V_{D S}} W Q_{I}(y) \mu_{n} d V \tag{1.214}
\end{equation*}
$$

and thus

$$
\begin{equation*}
I_{D}=\frac{\mu_{n} C_{o x}}{2\left(1+\frac{V_{D S}}{\mathscr{E}_{c} L}\right)} \frac{W}{L}\left[2\left(V_{G S}-V_{t}\right) V_{D S}-V_{D S}^{2}\right] \tag{1.215}
\end{equation*}
$$

In the limit as $\mathscr{E}_{c} \rightarrow \infty,(1.215)$ is the same as (1.152), which gives the drain current in the triode region without velocity saturation. The quantity $V_{D S} / L$ in (1.215) can be interpreted as the average horizontal electric field in the channel. If this field is comparable to $\mathscr{E}_{c}$, the drain current for a given $V_{D S}$ is less than the simple expression (1.152) would predict.

Equation 1.215 is valid in the triode region. Let $V_{D S(\text { act })}$ represent the maximum value of $V_{D S}$ for which the transistor operates in the triode region, which is equivalent to the minimum value of $V_{D S}$ for which the transistor operates in the active region. In the active region, the current should be independent of $V_{D S}$ because channel-length modulation is not included here. Therefore, $V_{D S(\text { act })}$ is the value of $V_{D S}$ that sets $\partial I_{D} / \partial V_{D S}=0$. From (1.215),

$$
\begin{equation*}
\frac{\partial I_{D}}{\partial V_{D S}}=\frac{k^{\prime}}{2} \frac{W}{L}\left[\frac{\left(1+\frac{V_{D S}}{\mathscr{E}_{C} L}\right)\left[2\left(V_{G S}-V_{t}\right)-2 V_{D S}\right]-\frac{\left[2\left(V_{G S}-V_{t}\right) V_{D S}-V_{D S}^{2}\right]}{\mathscr{E}_{C} L}}{\left(1+\frac{V_{D S}}{\mathscr{E}_{C} L}\right)^{2}}\right] \tag{1.216}
\end{equation*}
$$

where $k^{\prime}=\mu_{n} C_{o x}$ as given by (1.153). To set $\partial I_{D} / \partial V_{D S}=0$,

$$
\begin{equation*}
\left(1+\frac{V_{D S}}{\mathscr{E}_{C} L}\right)\left[2\left(V_{G S}-V_{t}\right)-2 V_{D S}\right]-\frac{\left[2\left(V_{G S}-V_{t}\right) V_{D S}-V_{D S}^{2}\right]}{\mathscr{E}_{c} L}=0 \tag{1.217}
\end{equation*}
$$

Rearranging (1.217) gives

$$
\begin{equation*}
\frac{V_{D S}^{2}}{\mathscr{E}_{c} L}+2 V_{D S}-2\left(V_{G S}-V_{t}\right)=0 \tag{1.218}
\end{equation*}
$$

Solving the quadratic equation gives

$$
\begin{equation*}
V_{D S(\mathrm{act})}=V_{D S}=-\mathscr{E}_{c} L \pm \mathscr{E}_{c} L \sqrt{1+\frac{2\left(V_{G S}-V_{t}\right)}{\mathscr{E}_{c} L}} \tag{1.219}
\end{equation*}
$$

Since the drain-source voltage must be greater than zero,

$$
\begin{equation*}
V_{D S(\mathrm{act})}=V_{D S}=\mathscr{E}_{c} L\left(\sqrt{1+\frac{2\left(V_{G S}-V_{t}\right)}{\mathscr{E}_{c} L}}-1\right) \tag{1.220}
\end{equation*}
$$

To determine $V_{D S(\text { act })}$ without velocity-saturation effects, let $\mathscr{E}_{c} \rightarrow \infty$ so that the drift velocity is proportional to the electric field, and let $x=\left(V_{G S}-V_{t}\right) /\left(\mathscr{E}_{c} L\right)$. Then $x \rightarrow 0$, and a Taylor series can be used to show that

$$
\begin{equation*}
\sqrt{1+2 x}=1+x-\frac{x^{2}}{2}+\cdots \tag{1.221}
\end{equation*}
$$

Using (1.221) in (1.220) gives

$$
\begin{equation*}
V_{D S(\mathrm{act})}=\left(V_{G S}-V_{t}\right)\left(1-\frac{V_{G S}-V_{t}}{2 \mathscr{E}_{c} L}+\cdots\right) \tag{1.222}
\end{equation*}
$$

When $\mathscr{E}_{c} \rightarrow \infty,(1.222)$ shows that $V_{D S(\text { act })} \rightarrow\left(V_{G S}-V_{t}\right)$, as expected. ${ }^{28}$ This observation is confirmed by plotting the ratio of $V_{D S(\text { act })}$ to the overdrive $V_{o v}$ versus $\mathscr{E}_{c} L$ in Fig. 1.40. When $\mathscr{E}_{c} \rightarrow \infty, V_{D S(\text { act })} \rightarrow V_{o v}=V_{G S}-V_{t}$, as predicted by (1.222). On the other hand, when $\mathscr{E}_{c}$ is small enough that velocity saturation is significant, Fig. 1.40 shows that $V_{D S(\text { act })}<V_{o v}$.

To find the drain current in the active region with velocity saturation, substitute $V_{D S(a c t)}$ in (1.220) for $V_{D S}$ in (1.215). After rearranging, the result is

$$
\begin{equation*}
I_{D}=\frac{\mu_{n} C_{o x}}{2} \frac{W}{L}\left[V_{D S(\mathrm{act})}\right]^{2} \tag{1.223}
\end{equation*}
$$

Equation 1.223 is in the same form as (1.157), where velocity saturation is neglected, except that $V_{D S \text { (act) }}$ is less than $\left(V_{G S}-V_{t}\right)$ when velocity saturation is significant, as shown in Fig. 1.40. Therefore, the current predicted by (1.157) overestimates the current that really flows when the carrier velocity saturates. To examine the limiting case when the velocity is completely
image_name:Figure 1.40
description:**Figure 1.40** is a plot illustrating the relationship between the ratio of the minimum drain-source voltage required for operation in the active region to the overdrive voltage, \( \frac{V_{DS(\text{act})}}{V_{ov}} \), and the product of the critical field and the channel length, \( \mathscr{E}_{c}L \), measured in volts.

1. **Type of Graph and Function:**
- This is a two-dimensional line graph showing the behavior of a semiconductor device under varying conditions of critical field and channel length.

2. **Axes Labels and Units:**
- The x-axis represents \( \mathscr{E}_{c}L \) in volts, ranging from 0 to 10 V.
- The y-axis represents the ratio \( \frac{V_{DS(\text{act})}}{V_{ov}} \), ranging from 0.5 to 1.

3. **Overall Behavior and Trends:**
- The graph shows two curves representing different overdrive voltages, \( V_{ov} = 0.1 \) V and \( V_{ov} = 0.5 \) V.
- Both curves start at a lower value on the y-axis and rise steeply initially, then gradually level off as \( \mathscr{E}_{c}L \) increases.
- The curve for \( V_{ov} = 0.1 \) V starts at a higher initial value compared to the \( V_{ov} = 0.5 \) V curve, indicating a smaller minimum drain-source voltage ratio for lower overdrive voltages.

4. **Key Features and Technical Details:**
- As \( \mathscr{E}_{c} \rightarrow \infty \), the curves approach a y-value of 1, suggesting that velocity saturation is not a factor and \( V_{DS(\text{act})} \rightarrow V_{ov} \).
- For smaller values of \( \mathscr{E}_{c}L \), the curves are significantly below 1, indicating the effect of velocity saturation.
- The steep rise at lower \( \mathscr{E}_{c}L \) values highlights the transition from significant velocity saturation to negligible saturation.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for \( V_{ov} = 0.1 \) V and \( V_{ov} = 0.5 \) V, clearly marking the two curves.
- No specific numerical data points are labeled, but the trend and behavior are clearly depicted.

Figure 1.40 Ratio of the minimum drain-source voltage required for operation in the active region to the overdrive versus the product of the critical field and the channel length. When $\mathscr{E}_{c} \rightarrow \infty$, velocity saturation is not a factor, and $V_{D S \text { (act) }} \rightarrow$ $V_{o v}=V_{G S}-V_{t}$, as expected. When velocity saturation is significant, $V_{D S(\text { act })}<V_{o v}$.
saturated, let $\mathscr{E}_{c} \rightarrow 0$. Then (1.212) shows that the drift velocity approaches the scatteringlimited velocity $v_{d} \rightarrow v_{s c l}=\mu_{n} \mathscr{E}_{c}$. Substituting (1.220) into (1.223) gives

$$
\begin{equation*}
\lim _{\mathscr{E}_{c} \rightarrow 0} I_{D}=\mu_{n} C_{o x} W\left(V_{G S}-V_{t}\right) \mathscr{E}_{c}=W C_{o x}\left(V_{G S}-V_{t}\right) v_{s c l} \tag{1.224}
\end{equation*}
$$

In contrast to the square-law behavior predicted by (1.157), (1.224) shows that the drain current is a linear function of the overdrive $\left(V_{G S}-V_{t}\right)$ when the carrier velocity saturates. Also, (1.224) shows that the drain current is independent of the channel length when the carrier velocity saturates. In this case, both the charge in the channel and the time required for the charge to cross the channel are proportional to $L$. Since the current is the ratio of the charge in the channel to the time required to cross the channel, the current does not depend on $L$ as long as the channel length is short enough to produce an electric field that is high enough for velocity saturation to occur. ${ }^{29}$ In contrast, when the carrier velocity is proportional to the electric field instead of being saturated, the time required for channel charge to cross the channel is proportional to $L^{2}$ because increasing $L$ both reduces the carrier velocity and increases the distance between the source and the drain. Therefore, when velocity saturation is not significant, the drain current is inversely proportional to $L$, as we have come to expect through (1.157). Finally, (1.224) shows that the drain current in the active region is proportional to the scattering-limited velocity $v_{s c l}=\mu_{n} \mathscr{E}_{c}$ when the velocity is saturated.

Substituting (1.222) into (1.223) gives

$$
\begin{align*}
I_{D} & =\frac{\mu_{n} C_{o x}}{2} \frac{W}{L}\left(V_{G S}-V_{t}\right)^{2}\left(1-\frac{V_{G S}-V_{t}}{2 \mathscr{E}_{c} L}+\cdots\right)^{2} \\
& =\frac{\mu_{n} C_{o x}}{2} \frac{W}{L}\left(V_{G S}-V_{t}\right)^{2}\left(1-\frac{x}{2}+\cdots\right)^{2}  \tag{1.225}\\
& =\frac{\mu_{n} C_{o x}}{2} \frac{W}{L}\left(V_{G S}-V_{t}\right)^{2}(1-x+\cdots) \\
& =\frac{\mu_{n} C_{o x}}{2} \frac{W}{L}\left(V_{G S}-V_{t}\right)^{2}\left(1-\frac{V_{G S}-V_{t}}{\mathscr{E}_{c} L}+\cdots\right)
\end{align*}
$$

where $x=\left(V_{G S}-V_{t}\right) /\left(\mathscr{E}_{c} L\right)$ as defined for $(1.221)$. If $x \ll 1,(1-x) \simeq 1 /(1+x)$, and

$$
\begin{equation*}
I_{D} \simeq \frac{\mu_{n} C_{o x}}{2\left(1+\frac{V_{G S}-V_{t}}{\mathscr{E}_{c} L}\right)} \frac{W}{L}\left(V_{G S}-V_{t}\right)^{2} \tag{1.226}
\end{equation*}
$$

Equation 1.226 is valid without velocity saturation and at its onset, where $\left(V_{G S}-V_{t}\right) \ll \mathscr{E}_{c} L$. The effect of velocity saturation on the current in the active region predicted by (1.226) can be modeled with the addition of a resistance in series with the source of an ideal square-law device, as shown in Fig. 1.41. Let $V_{G S}^{\prime}$ be the gate-source voltage of the ideal square-law
image_name:Figure 1.41
description:
[
name: M1, type: NMOS, ports: {S: S1, D: D, G: G}
name: RSX, type: Resistor, value: RSX, ports: {N1: S1, N2: S}
]
extrainfo:The circuit models velocity saturation in an NMOS transistor by adding a series source resistance RSX to the ideal square-law device M1. The gate-source voltage V_GS is the sum of V'_GS and the voltage drop across RSX.

Figure 1.41 Model of velocity saturation in an MOSFET by addition of series source resistance to an ideal square-law device.
transistor. From (1.157),

$$
\begin{equation*}
I_{D}=\frac{\mu_{n} C_{o x}}{2} \frac{W}{L}\left(V_{G S}^{\prime}-V_{t}\right)^{2} \tag{1.227}
\end{equation*}
$$

Let $V_{G S}$ be the sum of $V_{G S}^{\prime}$ and the voltage drop on $R_{S X}$. Then

$$
\begin{equation*}
V_{G S}=V_{G S}^{\prime}+I_{D} R_{S X} \tag{1.228}
\end{equation*}
$$

This sum models the gate-source voltage of a real MOS transistor with velocity saturation. Substituting (1.228) into (1.227) gives

$$
\begin{gather*}
I_{D}=\frac{\mu_{n} C_{o x}}{2} \frac{W}{L}\left(V_{G S}-I_{D} R_{S X}-V_{t}\right)^{2} \\
I_{D}=\frac{\mu_{n} C_{o x}}{2} \frac{W}{L}\left(\left(V_{G S}-V_{t}\right)^{2}-2\left(V_{G S}-V_{t}\right) I_{D} R_{S X}+\left(I_{D} R_{S X}\right)^{2}\right) \tag{1.229}
\end{gather*}
$$

Rearranging (1.229) while ignoring the $\left(I_{D} R_{S X}\right)^{2}$ term gives

$$
\begin{equation*}
I_{D} \simeq \frac{\mu_{n} C_{o x}}{2\left(1+\mu_{n} C_{o x} \frac{W}{L} R_{S X}\left(V_{G S}-V_{t}\right)\right)} \frac{W}{L}\left(V_{G S}-V_{t}\right)^{2} \tag{1.230}
\end{equation*}
$$

Equation 1.230 has the same form as (1.226) if we identify

$$
\begin{equation*}
\mu_{n} C_{o x} \frac{W}{L} R_{S X}=\frac{1}{\mathscr{E}_{C} L} \tag{1.231}
\end{equation*}
$$

Rearranging (1.231) gives

$$
\begin{equation*}
R_{S X}=\frac{1}{\mathscr{E}_{c} \mu_{n} C_{o x} W} \tag{1.232}
\end{equation*}
$$

Thus the influence of velocity saturation on the large-signal characteristics of an MOS transistor can be modeled to first order by a resistor $R_{S X}$ in series with the source of an ideal square-law device. Note that $R_{S X}$ varies inversely with $W$, as does the intrinsic physical series resistance due to the source and drain contact regions. Typically, $R_{S X}$ is larger than the physical series resistance. For $W=2 \mu \mathrm{~m}, k^{\prime}=\mu_{n} C_{o x}=200 \mu \mathrm{~A} / \mathrm{V}^{2}$, and $\mathscr{E}_{c}=1.5 \times 10^{6} \mathrm{~V} / \mathrm{m}$, we find $R_{S X} \simeq 1700 \Omega$.

### 1.7.2 Transconductance and Transition Frequency

The values of all small-signal parameters can change significantly in the presence of shortchannel effects. ${ }^{30}$ One of the most important changes is to the transconductance. Substituting (1.220) into (1.223) and calculating $\partial I_{D} / \partial V_{G S}$ gives

$$
\begin{equation*}
g_{m}=\frac{\partial I_{D}}{\partial V_{G S}}=W C_{o x} v_{s c l} \frac{\sqrt{1+\frac{2\left(V_{G S}-V_{t}\right)}{\mathscr{E}_{c} L}}-1}{\sqrt{1+\frac{2\left(V_{G S}-V_{t}\right)}{\mathscr{E}_{c} L}}} \tag{1.233}
\end{equation*}
$$

where $v_{s c l}=\mu_{n} \mathscr{E}_{c}$ as in Fig. 1.39. To determine $g_{m}$ without velocity saturation, let $E_{c} \rightarrow \infty$ and $x=\left(V_{G S}-V_{t}\right) /\left(\mathscr{E}_{c} L\right)$. Then substituting (1.221) into (1.233) and rearranging gives

$$
\begin{equation*}
\lim _{\mathscr{C}_{c} \rightarrow \infty} g_{m}=k^{\prime} \frac{W}{L}\left(V_{G S}-V_{t}\right) \tag{1.234}
\end{equation*}
$$

as predicted by (1.180). In this case, the transconductance increases when the overdrive increases or the channel length decreases. On the other hand, letting $\mathscr{E}_{c} \rightarrow 0$ to determine $g_{m}$ when the velocity is saturated gives

$$
\begin{equation*}
\lim _{\mathscr{E}_{c} \rightarrow 0} g_{m}=W C_{o x} v_{s c l} \tag{1.235}
\end{equation*}
$$

Equation 1.235 shows that further decreases in $L$ or increases in $\left(V_{G S}-V_{t}\right)$ do not change the transconductance when the velocity is saturated.

From (1.223) and (1.233), the ratio of the transconductance to the current can be calculated as

$$
\begin{equation*}
\frac{g_{m}}{I}=\frac{2}{\left(\mathscr{E}_{c} L\right) \sqrt{1+\frac{2\left(V_{G S}-V_{t}\right)}{\mathscr{E}_{c} L}}\left(\sqrt{\left.1+\frac{2\left(V_{G S}-V_{t}\right)}{\mathscr{E}_{C} L}-1\right)}\right.} \tag{1.236}
\end{equation*}
$$

As $\mathscr{E}_{c} \rightarrow 0$, the velocity saturates and

$$
\begin{equation*}
\lim _{\mathscr{E}_{c} \rightarrow 0} \frac{g_{m}}{I}=\frac{1}{V_{G S}-V_{t}} \tag{1.237}
\end{equation*}
$$

Comparing (1.237) to (1.181) shows that velocity saturation reduces the transconductance-tocurrent ratio for a given overdrive.

On the other hand, when $x=\left(V_{G S}-V_{t}\right) /\left(\mathscr{E}_{c} L\right) \ll 1$, substituting (1.221) into (1.236) gives

$$
\begin{equation*}
\frac{g_{m}}{I} \simeq \frac{2}{\left(V_{G S}-V_{t}\right)(1+x)} \tag{1.238}
\end{equation*}
$$

Therefore, as $\mathscr{E}_{c} \rightarrow \infty, x \rightarrow 0$, and (1.238) collapses to

$$
\begin{equation*}
\lim _{\mathscr{E}_{c} \rightarrow \infty} \frac{g_{m}}{I}=\frac{2}{V_{G S}-V_{t}} \tag{1.239}
\end{equation*}
$$

as predicted by (1.181). Equation 1.238 shows that if $x<0.1$, the error in using (1.181) to calculate the transconductance-to-current ratio is less than about 10 percent. Therefore, we will conclude that velocity-saturation effects are insignificant in hand calculations if

$$
\begin{equation*}
\left(V_{G S}-V_{t}\right)<0.1\left(\mathscr{C}_{c} L\right) \tag{1.240}
\end{equation*}
$$

Figure 1.42 plots the transconductance-to-current ratio versus the overdrive for three cases. The highest and lowest ratios come from (1.239) and (1.237), which correspond to asymptotes where velocity saturation is insignificant and dominant, respectively. In practice, the transition between these extreme cases is gradual and described by (1.236), which is plotted in Fig. 1.42 for an example where $\mathscr{E}_{c}=1.5 \times 10^{6} \mathrm{~V} / \mathrm{m}$ and $L=0.5 \mu \mathrm{~m}$.

One reason the change in transconductance caused by velocity saturation is important is because it affects the transition frequency $f_{T}$. Assuming that $C_{g s} \gg C_{g b}+C_{g d}$, substituting (1.235) into (1.208) shows that

$$
\begin{equation*}
f_{T}=\frac{1}{2 \pi} \frac{g_{m}}{C_{g s}} \propto \frac{W C_{o x} v_{s c l}}{W L C_{o x}} \propto \frac{v_{s c l}}{L} \tag{1.241}
\end{equation*}
$$

One key point here is that the transition frequency is independent of the overdrive once velocity saturation is reached. In contrast, (1.209) shows that increasing $\left(V_{G S}-V_{t}\right)$ increases $f_{T}$ before the velocity saturates. Also, (1.241) shows that the transition frequency is inversely proportional to the channel length when the velocity is saturated. In contrast, (1.209) predicts that $f_{T}$ is
image_name:Figure 1.42
description:The graph in Figure 1.42 is a plot of the transconductance-to-current ratio \( \frac{g_m}{I} \) versus the overdrive voltage \( V_{GS} - V_t \). The x-axis represents the overdrive voltage \( V_{GS} - V_t \) in volts, ranging from 0 to 3 V. The y-axis represents the transconductance-to-current ratio \( \frac{g_m}{I} \) in units of \( \text{V}^{-1} \), ranging from 0 to 5 \( \text{V}^{-1} \).

The graph shows three curves corresponding to different conditions of velocity saturation characterized by the parameter \( \mathscr{E}_c L \):

1. **\( \mathscr{E}_c L \rightarrow \infty \)**: This curve is labeled as "Eq. 1.239" and represents the scenario where velocity saturation is insignificant. It is the uppermost curve on the graph, starting at a higher transconductance-to-current ratio and decreasing as \( V_{GS} - V_t \) increases.

2. **\( \mathscr{E}_c L = 0.75 \text{ V} \)**: This curve is labeled as "Eq. 1.236" and represents a condition where velocity saturation is of gradually increasing importance. It lies between the other two curves, showing a moderate decrease in the transconductance-to-current ratio with increasing \( V_{GS} - V_t \).

3. **\( \mathscr{E}_c L \rightarrow 0 \)**: This curve is labeled as "Eq. 1.237" and represents the condition where velocity saturation is dominant. It is the lowermost curve, starting at a lower transconductance-to-current ratio and decreasing more gently as \( V_{GS} - V_t \) increases.

Overall, the graph illustrates how the transconductance-to-current ratio decreases with increasing overdrive voltage and how this behavior is influenced by the degree of velocity saturation. The curves show that as velocity saturation becomes more significant, the transconductance-to-current ratio decreases more slowly with increasing \( V_{GS} - V_t \).

Figure 1.42
Transconductance-to-current ratio versus overdrive $\left(V_{G S}-V_{t}\right)$ where velocity saturation is insignificant ( $\left.\mathscr{E}_{c} L \rightarrow \infty\right)$, dominant ( $\mathscr{E}_{c} L=0$ ), and of gradually increasing importance ( $\mathscr{E}_{c} L=0.75 \mathrm{~V}$ ).
inversely proportional to the square of the channel length before the velocity saturates. As a result, velocity saturation reduces the speed improvement that can be achieved through reductions in the minimum channel length.

### 1.7.3 Mobility Degradation from the Vertical Field

Thus far, we have considered only the effects of the horizontal field due to the $V_{D S}$ along the channel when considering velocity saturation. However, a vertical field originating from the gate voltage also exists and influences carrier velocity. A physical reason for this effect is that increasing the vertical electric field forces the carriers in the channel closer to the surface of the silicon, where surface imperfections impede their movement from the source to the drain, reducing mobility. ${ }^{31}$ The vertical field at any point in the channel depends on the gate-channel voltage. Since the gate-channel voltage is not constant from the source to the drain, the effect of the vertical field on mobility should be included within the integration in (1.214) in principle. ${ }^{32}$ For simplicity, however, this effect is often modeled after integration by changing the mobility in the previous equations to an effective mobility given by

$$
\begin{equation*}
\mu_{\mathrm{eff}}=\frac{\mu_{n}}{1+\theta\left(V_{G S}-V_{t}\right)} \tag{1.242}
\end{equation*}
$$

where $\mu_{n}$ is the mobility with zero vertical field, and $\theta$ is inversely proportional to the oxide thickness. For $t_{o x}=100 \AA, \theta$ is typically in the range from $0.1 \mathrm{~V}^{-1}$ to $0.4 \mathrm{~V}^{-1} .33$ In practice, $\theta$ is determined by a best fit to measured device characteristics.

## 1.8 Weak Inversion in MOS Transistors

The MOSFET analysis of Section 1.5 considered the normal region of operation for which a well-defined conducting channel exists under the gate. In this region of strong inversion, changes in the gate-source voltage are assumed to cause only changes in the channel charge and not in the depletion-region charge. In contrast, for gate-source voltages less than the extrapolated threshold voltage $V_{t}$ but high enough to create a depletion region at the surface of the silicon, the device operates in weak inversion. In the weak-inversion region, the channel charge is much less than the charge in the depletion region, and the drain current arising from the drift of majority carriers is negligible. However, the total drain current in weak inversion
is larger than that caused by drift because a gradient in minority-carrier concentration causes a diffusion current to flow. In weak inversion, an $n$-channel MOS transistor operates as an $n p n$ bipolar transistor, where the source acts as the emitter, the substrate as the base, and the drain as the collector. ${ }^{34}$

### 1.8.1 Drain Current in Weak Inversion

To analyze this situation, assume that the source and the body are both grounded. Also assume that $V_{D S}>0$. (If $V_{D S}<0$, the drain acts as the emitter and the source as the collector.) ${ }^{35}$ Then increasing the gate-source voltage increases the surface potential $\psi_{s}$, which tends to reduce the reverse bias across the source-substrate (emitter-base) junction and to exponentially increase the concentration of electrons in the $p$-type substrate at the source $n_{p}(0)$. From (1.27),

$$
\begin{equation*}
n_{p}(0)=n_{p o} \exp \frac{\psi_{s}}{V_{T}} \tag{1.243}
\end{equation*}
$$

where $n_{p o}$ is the equilibrium concentration of electrons in the substrate (base). Similarly, the concentration of electrons in the substrate at the drain $n_{p}(L)$ is

$$
\begin{equation*}
n_{p}(L)=n_{p o} \exp \frac{\psi_{s}-V_{D S}}{V_{T}} \tag{1.244}
\end{equation*}
$$

From (1.31), the drain current due to the diffusion of electrons in the substrate is

$$
\begin{equation*}
I_{D}=q A D_{n} \frac{n_{p}(L)-n_{p}(0)}{L} \tag{1.245}
\end{equation*}
$$

where $D_{n}$ is the diffusion constant for electrons, and $A$ is the cross-sectional area in which the diffusion current flows. The area $A$ is the product of the transistor width $W$ and the thickness $X$ of the region in which $I_{D}$ flows. Substituting (1.243) and (1.244) into (1.245) and rearranging gives

$$
\begin{equation*}
I_{D}=\frac{W}{L} q X D_{n} n_{p o} \exp \left(\frac{\psi_{s}}{V_{T}}\right)\left[1-\exp \left(-\frac{V_{D S}}{V_{T}}\right)\right] \tag{1.246}
\end{equation*}
$$

In weak inversion, the surface potential is approximately a linear function of the gatesource voltage. ${ }^{36}$ Assume that the charge stored at the oxide-silicon interface is independent of the surface potential. Then, in weak inversion, changes in the surface potential $\Delta \psi_{s}$ are controlled by changes in the gate-source voltage $\Delta V_{G S}$ through a voltage divider between the oxide capacitance $C_{o x}$ and the depletion-region capacitance $C_{j s}$. Therefore,

$$
\begin{equation*}
\frac{d \psi_{s}}{d V_{G S}}=\frac{C_{o x}}{C_{j s}+C_{o x}}=\frac{1}{n}=\frac{1}{1+\chi} \tag{1.247}
\end{equation*}
$$

in which $n=\left(1+C_{j s} / C_{o x}\right)$ and $\chi=C_{j s} / C_{o x}$, as defined in (1.197). Separating variables in (1.247) and integrating gives

$$
\begin{equation*}
\psi_{s}=\frac{V_{G S}}{n}+k_{1} \tag{1.248}
\end{equation*}
$$

where $k_{1}$ is a constant. Equation 1.248 is valid only when the transistor operates in weak inversion. When $V_{G S}=V_{t}$ with $V_{S B}=0, \psi_{s}=2 \phi_{f}$ by definition of the threshold voltage. For $V_{G S}>V_{t}$, the inversion layer holds the surface potential nearly constant and (1.248) is not valid. Since (1.248) is valid only when $V_{G S} \leq V_{t}$, (1.248) is rewritten as follows:

$$
\begin{equation*}
\psi_{s}=\frac{V_{G S}-V_{t}}{n}+k_{2} \tag{1.249}
\end{equation*}
$$

where $k_{2}=k_{1}+V_{t} / n$. Substituting (1.249) into (1.246) gives

$$
\begin{equation*}
I_{D}=\frac{W}{L} q X D_{n} n_{p o} \exp \left(\frac{k_{2}}{V_{T}}\right) \exp \left(\frac{V_{G S}-V_{t}}{n V_{T}}\right)\left[1-\exp \left(-\frac{V_{D S}}{V_{T}}\right)\right] \tag{1.250}
\end{equation*}
$$

Let

$$
\begin{equation*}
I_{t}=q X D_{n} n_{p o} \exp \left(\frac{k_{2}}{V_{T}}\right) \tag{1.251}
\end{equation*}
$$

represent the drain current with $V_{G S}=V_{t}, W / L=1$, and $V_{D S} \gg V_{T}$. Then

$$
\begin{equation*}
I_{D}=\frac{W}{L} I_{t} \exp \left(\frac{V_{G S}-V_{t}}{n V_{T}}\right)\left[1-\exp \left(-\frac{V_{D S}}{V_{T}}\right)\right] \tag{1.252}
\end{equation*}
$$

Figure 1.43 plots the drain current versus the drain-source voltage for three values of the overdrive, with $W=20 \mu \mathrm{~m}, L=20 \mu \mathrm{~m}, n=1.5$, and $I_{t}=0.1 \mu \mathrm{~A}$. Notice that the drain current is almost constant when $V_{D S}>3 V_{T}$ because the last term in (1.252) approaches unity in this case. Therefore, unlike in strong inversion, the minimum drain-source voltage required to force the transistor to operate as a current source in weak inversion is independent of the overdrive. ${ }^{37}$ Figure 1.43 and Equation 1.252 also show that the drain current is not zero when $V_{G S} \leq V_{t}$. To further illustrate this point, we show measured NMOS characteristics plotted on two different scales in Fig. 1.44. In Fig. 1.44a, we show $\sqrt{I_{D}}$ versus $V_{G S}$ in the active region plotted on linear scales. For this device, $W=20 \mu \mathrm{~m}, L=20 \mu \mathrm{~m}$, and short-channel effects are negligible. (See Problem 1.21 for an example of a case in which short-channel effects are important.) The resulting straight line shows that the device characteristic is close to an ideal square law. Plots like the one in Fig. 1.44a are commonly used to obtain $V_{t}$ by extrapolation ( 0.7 V in this case) and also $k^{\prime}$ from the slope of the curve ( $54 \mu \mathrm{~A} / \mathrm{V}^{2}$ in this case). Near the threshold voltage, the curve deviates from the straight line representing the square law. This region is weak inversion. The data are plotted a second time in Fig. $1.44 b$ on log-linear scales. The straight line obtained for $V_{G S}<V_{t}$ fits (1.252) with $n=$ 1.5. For $I_{D}<10^{-12} \mathrm{~A}$, the slope decreases because leakage currents are significant and do not follow (1.252).
image_name:Figure 1.43
description:Figure 1.43 is a graph depicting the relationship between the drain current (I_D) and the drain-source voltage (V_DS) in weak inversion for an NMOS transistor. The graph is plotted on linear scales with the x-axis representing the drain-source voltage (V_DS) in volts (V) and the y-axis representing the drain current (I_D) in microamperes (µA).

**Axes Labels and Units:**
- X-axis: V_DS (V), ranging from 0 to 0.5 volts.
- Y-axis: I_D (µA), ranging from 0 to 0.12 microamperes.

**Overall Behavior and Trends:**
The graph shows three curves, each representing different gate-source voltage conditions:
1. **V_GS - V_t = 0:** The curve starts at the origin and rises steeply, reaching a saturation point around 0.1 µA as V_DS approaches 0.1 V, after which it flattens out.
2. **V_GS - V_t = -10 mV:** This curve follows a similar trend but starts at a lower initial current and reaches saturation at a lower current level, around 0.06 µA.
3. **V_GS - V_t = -20 mV:** This curve again follows the pattern but with an even lower initial current, saturating around 0.03 µA.

**Key Features and Technical Details:**
- The curves exhibit a sharp increase in drain current initially, indicating the transition from the subthreshold region to the weak inversion region.
- A vertical dashed line is drawn at V_DS = 3V_T ≈ 78 mV, indicating a significant point where the curves begin to saturate.
- The saturation current level decreases as the gate-source voltage decreases, demonstrating the effect of V_GS on the drain current in weak inversion.

**Annotations and Specific Data Points:**
- The annotations indicate the gate-source voltage offset (V_GS - V_t) for each curve, providing context for the behavior of the transistor in different biasing conditions.
- The critical point at V_DS = 78 mV is highlighted, showing where the saturation begins for each curve.

Figure 1.43 Drain current versus drain-source voltage in weak inversion.
image_name:Figure 1.44 (a)
description:The graph in Figure 1.44 (a) is a plot of the square root of the drain current (I_D) measured in microamperes (µA) raised to the power of 1/2, versus the gate-source voltage (V_GS) in volts (V). This graph represents the NMOS transfer characteristic in the active region, plotted on linear scales, highlighting the square-law behavior typical of MOSFETs in saturation.

**Axes Labels and Units:**
- The x-axis represents the gate-source voltage (V_GS) in volts (V), ranging from 0 to 5 volts.
- The y-axis represents the square root of the drain current (√I_D) in microamperes (µA) raised to the power of 1/2, with values ranging from 0 to 25 µA^(1/2).

**Overall Behavior and Trends:**
- The graph shows a linear relationship between √I_D and V_GS, indicating the square-law characteristic of the NMOS transistor in the active region.
- The curve starts at a low value of V_GS and increases linearly as V_GS increases.

**Key Features and Technical Details:**
- The threshold voltage (V_t) is extrapolated to be approximately 0.7 V, as indicated by the dashed line extending to the x-axis.
- The parameters provided in the graph include a drain-source voltage (V_DS) of 5 V, a channel width (W) of 20 µm, and a channel length (L) of 20 µm.

**Annotations and Specific Data Points:**
- The graph includes an annotation for the extrapolated threshold voltage (V_t = 0.7 V), marking the point where the linear relationship begins, which is critical for understanding the onset of strong inversion in the MOSFET.

This graph effectively demonstrates the square-law behavior of the NMOS transistor in the active region, with a clear linear relationship between √I_D and V_GS, starting at the threshold voltage.

(a)

Figure 1.44 (a) Measured NMOS transfer characteristic in the active region plotted on linear scales as $\sqrt{I_{D}}$ versus $V_{G S}$, showing the square-law characteristic.
image_name:(b)
description:The graph in Figure 1.44 (b) is a log-linear plot showing the NMOS transistor's transfer characteristics in the active region. The x-axis represents the gate-source voltage, \( V_{GS} \), measured in volts (V), while the y-axis represents the drain current, \( I_{D} \), measured in amperes (A). The y-axis is plotted on a logarithmic scale, ranging from \( 10^{-13} \) A to \( 10^{-3} \) A, and the x-axis is on a linear scale, ranging from 0 V to 2 V.

The graph illustrates two distinct regions of transistor operation:

1. **Subthreshold Exponential Region:**
- This region is observed for \( V_{GS} \) values less than approximately 0.5 V.
- In this region, \( I_{D} \) increases exponentially with \( V_{GS} \), indicating the weak inversion or subthreshold operation of the NMOS transistor.
- This behavior is typical for very low power applications where the transistor operates below the threshold voltage.

2. **Square-law Region:**
- For \( V_{GS} \) values greater than approximately 0.5 V, the graph transitions into a region where \( I_{D} \) follows a square-law relationship with \( V_{GS} \).
- This behavior is indicative of the strong inversion region where the transistor operates in the active mode.
- The linear relationship between \( \sqrt{I_{D}} \) and \( V_{GS} \) in this region highlights the square-law characteristic of the NMOS transistor.

The graph is annotated to indicate the transition between these regions, with the subthreshold and square-law regions clearly labeled. The specific conditions for the graph are given as \( V_{DS} = 5 \) V, \( W = 20 \) µm, and \( L = 20 \) µm, which are typical parameters for analyzing transistor behavior in these regions.

Figure 1.44 (b) Data from Fig. $1.44 a$ plotted on log-linear scales showing the exponential characteristic in the subthreshold region.

The major use of transistors operating in weak inversion is in very low power applications at relatively low signal frequencies. The limitation to low signal frequencies occurs because the MOSFET $f_{T}$ becomes very small. This result stems from the fact that the small-signal $g_{m}$ calculated from (1.252) becomes proportional to $I_{D}$ and therefore very small in weak inversion, as shown next.

### 1.8.2 Transconductance and Transition Frequency in Weak Inversion

Calculating $\partial I_{D} / \partial V_{G S}$ from (1.252) and using (1.247) gives

$$
\begin{equation*}
g_{m}=\frac{W}{L} \frac{I_{t}}{n V_{T}} \exp \left(\frac{V_{G S}-V_{t}}{n V_{T}}\right)\left[1-\exp \left(-\frac{V_{D S}}{V_{T}}\right)\right]=\frac{I_{D}}{n V_{T}}=\frac{I_{D}}{V_{T}} \frac{C_{o x}}{C_{j s}+C_{o x}} \tag{1.253}
\end{equation*}
$$

The transconductance of an MOS transistor operating in weak inversion is identical to that of a corresponding bipolar transistor, as shown in (1.182), except for the factor of $1 / n=C_{o x} /$ $\left(C_{j s}+C_{o x}\right)$. This factor stems from a voltage divider between the oxide and depletion capacitors in the MOS transistor, which models the indirect control of the gate on the surface potential.

From (1.253), the ratio of the transconductance to the current of an MOS transistor in weak inversion is

$$
\begin{equation*}
\frac{g_{m}}{I}=\frac{1}{n V_{T}}=\frac{1}{V_{T}} \frac{C_{o x}}{C_{j s}+C_{o x}} \tag{1.254}
\end{equation*}
$$

Equation 1.254 predicts that this ratio is independent of the overdrive. In contrast, (1.181) predicts that the ratio of transconductance to current is inversely proportional to the overdrive. Therefore, as the overdrive approaches zero, (1.181) predicts that this ratio becomes infinite. However, (1.181) is valid only when the transistor operates in strong inversion. To estimate the overdrive required to operate the transistor in strong inversion, we will equate the $g_{m} / I$ ratios calculated in (1.254) and (1.181). The result is

$$
\begin{equation*}
V_{o v}=V_{G S}-V_{t}=2 n V_{T} \tag{1.255}
\end{equation*}
$$

which is about 78 mV at room temperature with $n=1.5$. Although this analysis implies that the transition from weak to strong inversion occurs abruptly, a nonzero transition width occurs in practice. Between weak and strong inversion, the transistor operates in a region of moderate inversion, where both diffusion and drift currents are significant. ${ }^{38}$

Figure 1.45 plots the transconductance-to-current ratio versus overdrive for an example case with $n=1.5$. When the overdrive is negative but high enough to cause depletion at the surface, the transistor operates in weak inversion and the transconductance-to-current ratio is constant, as predicted by (1.254). When $V_{G S}-V_{t}=0$, the surface potential is $2 \psi_{f}$, which means that the surface concentration of electrons is equal to the bulk concentration of holes. This point is usually defined as the upper bound on the region of weak inversion. When
image_name:Figure 1.45 Transconductance-to-current ratio versus overdrive
description:The graph in Figure 1.45 is a plot of the transconductance-to-current ratio \( \frac{g_m}{I} \) versus the overdrive voltage \( V_{GS} - V_t \). The graph is a line plot with the x-axis labeled as \( V_{GS} - V_t \) in volts (V), ranging from -0.5 V to 0.5 V, and the y-axis labeled as \( \frac{g_m}{I} \) in inverse volts (V\(^{-1}\)), ranging from 0 to 30 V\(^{-1}\).

Overall Behavior and Trends:
- **Weak Inversion Region:** For negative overdrive values, the transconductance-to-current ratio is constant at around 25 V\(^{-1}\). This behavior is predicted by equation (1.254) with \( n = 1.5 \), indicating operation in weak inversion.
- **Moderate Inversion Region:** As the overdrive increases towards zero, the graph indicates a transition to moderate inversion, where the ratio begins to decrease.
- **Strong Inversion Region:** For positive overdrive values greater than \( 2nV_T \), the ratio decreases significantly, following the prediction of equation (1.181), suggesting strong inversion.

Key Features and Technical Details:
- The transition from weak to moderate inversion occurs at \( V_{GS} - V_t = 0 \), where the surface potential is \( 2 \psi_f \).
- The boundary between moderate and strong inversion is marked at \( V_{GS} - V_t = 2nV_T \).
- The graph shows a clear demarcation between the regions, with annotations indicating the equations relevant to each region.

Annotations and Specific Data Points:
- The graph is annotated with labels indicating the regions of weak, moderate, and strong inversion.
- The constant value in the weak inversion region is clearly marked at 25 V\(^{-1}\).

This graph effectively illustrates the relationship between the transconductance-to-current ratio and the overdrive voltage in different operational regions of a transistor, highlighting the transitions between weak, moderate, and strong inversion.

Figure 1.45 Transconductance-to-current ratio versus overdrive.
$V_{G S}-V_{t}>2 n V_{T}$, the transconductance-to-current ratio is given by (1.181), assuming that velocity saturation is negligible. If velocity saturation is significant, (1.236) should be used instead of (1.181) both to predict the transconductance-to-current ratio and to predict the overdrive required to operate in strong inversion. For $0 \leq V_{G S}-V_{t} \leq 2 n V_{T}$, the transistor operates in moderate inversion. Because simple models for moderate inversion are not known in practice, we will ignore this region in the remainder of this book and assume that MOS transistors operate in weak inversion for overdrives less than the bound given in (1.255).

Equation 1.208 can be used to find the transition frequency. In weak inversion, $C_{g s} \simeq$ $C_{g d} \simeq 0$ because the inversion layer contains little charge. ${ }^{39}$ However, $C_{g b}$ can be thought of as the series combination of the oxide and depletion capacitors. Therefore,

$$
\begin{equation*}
C_{g s}+C_{g b}+C_{g d} \simeq C_{g b}=W L\left(\frac{C_{o x} C_{j s}}{C_{o x}+C_{j s}}\right) \tag{1.256}
\end{equation*}
$$

Substituting (1.253) and (1.256) into (1.208) gives

$$
\begin{equation*}
f_{T}=\frac{1}{2 \pi} \omega_{T}=\frac{1}{2 \pi} \frac{\frac{I_{D}}{V_{T}} \frac{C_{o x}}{C_{j s}+C_{o x}}}{W L \frac{C_{o x} C_{j s}}{C_{o x}+C_{j s}}}=\frac{1}{2 \pi} \frac{I_{D}}{V_{T}} \frac{1}{W L C_{j s}} \tag{1.257}
\end{equation*}
$$

Let $I_{M}$ represent the maximum drain current that flows in the transistor in weak inversion. Then

$$
\begin{equation*}
I_{M}=\frac{W}{L} I_{t} \tag{1.258}
\end{equation*}
$$

where $I_{t}$ is given in (1.251). Multiplying numerator and denominator in (1.257) by $I_{M}$ and using (1.258) gives

$$
\begin{equation*}
f_{T}=\frac{1}{2 \pi} \frac{\frac{W}{L} I_{t}}{V_{T}} \frac{1}{W L C_{j s}} \frac{I_{D}}{I_{M}}=\frac{1}{2 \pi} \frac{I_{t}}{V_{T}} \frac{1}{C_{j s}} \frac{1}{L^{2}} \frac{I_{D}}{I_{M}} \tag{1.259}
\end{equation*}
$$

From (1.251), $I_{t} \propto D_{n}$. Using the Einstein relationship $D_{n}=\mu_{n} V_{T}$ gives

$$
\begin{equation*}
f_{T} \propto \frac{D_{n}}{L^{2}} \frac{I_{D}}{I_{M}} \propto \frac{\mu_{n} V_{T}}{L^{2}} \frac{I_{D}}{I_{M}} \tag{1.260}
\end{equation*}
$$

Equation 1.260 shows that the transition frequency for an MOS transistor operating in weak inversion is inversely proportional to the square of the channel length. This result is consistent with (1.209) for strong inversion without velocity saturation. In contrast, when velocity saturation is significant, the transition frequency is inversely proportional to the channel length, as predicted by (1.241). Equation 1.260 also shows that the transition frequency in weak inversion is independent of the overdrive, unlike the case in strong inversion without velocity saturation, but like the case with velocity saturation. Finally, a more detailed analysis shows that the constant of proportionality in (1.260) is approximately unity. ${ }^{39}$

#### EXAMPLE

Calculate the overdrive and the transition frequency for an NMOS transistor with $I_{D}=1 \mu \mathrm{~A}$, $I_{t}=0.1 \mu \mathrm{~A}$, and $V_{D S} \gg V_{T}$. Device parameters are $W=10 \mu \mathrm{~m}, L=1 \mu \mathrm{~m}, n=1.5, k^{\prime}=$ $200 \mu \mathrm{~A} / \mathrm{V}^{2}$, and $t_{o x}=100 \AA$. Assume that the temperature is $27^{\circ} \mathrm{C}$.

From (1.166), if the transistor operates in strong inversion,

$$
V_{o v}=V_{G S}-V_{t}=\sqrt{\frac{2 I_{D}}{k^{\prime}(W / L)}}=\sqrt{\frac{2 \times 1}{200 \times 10}} \simeq 32 \mathrm{mV}
$$

Since the value of the overdrive calculated by (1.166) is less than $2 n V_{T} \simeq 78 \mathrm{mV}$, the overdrive calculated previously is not valid except to indicate that the transistor does not operate in strong inversion. From (1.252), the overdrive in weak inversion with $V_{D S} \gg V_{T}$ is

$$
V_{o v}=n V_{T} \ln \left(\frac{I_{D}}{I_{t}} \frac{L}{W}\right)=(1.5)(26 \mathrm{mV}) \ln \left(\frac{1}{0.1} \frac{1}{10}\right)=0
$$

From (1.253),

$$
g_{m}=\frac{1 \mu \mathrm{~A}}{1.5(26 \mathrm{mV})} \simeq 26 \frac{\mu \mathrm{~A}}{\mathrm{~V}}
$$

From (1.247),

$$
C_{j s}=(n-1) C_{o x}=(0.5) C_{o x}
$$

From (1.256),

$$
\begin{aligned}
C_{g s}+C_{g b}+C_{g d} \simeq C_{g b} & =W L \frac{C_{o x}\left(0.5 C_{o x}\right)}{C_{o x}+0.5 C_{o x}}=W L \frac{C_{o x}}{3} \\
& =\frac{10 \mu^{2}}{3} \frac{3.9 \times 8.854 \times 10^{-14} \frac{\mathrm{~F}}{\mathrm{~cm}} \times \frac{100 \mathrm{~cm}}{10^{6} \mu \mathrm{~m}}}{100 \AA \times \frac{10^{6} \mu \mathrm{~m}}{10^{10} \AA}} \\
& \simeq 11.5 \mathrm{fF}
\end{aligned}
$$

From (1.208),

$$
f_{T}=\frac{1}{2 \pi} \omega_{T}=\frac{1}{2 \pi} \frac{26 \mu \mathrm{~A} / \mathrm{V}}{11.5 \mathrm{fF}} \simeq 360 \mathrm{MHz}
$$

Although 360 MHz may seem to be a high transition frequency at first glance, this result should be compared with the result of the example at the end of Section 1.6, where the same transistor operating in strong inversion with an overdrive of 316 mV had a transition frequency of 3.4 GHz .

## 1.9 Substrate Current Flow in MOS Transistors

In Section 1.3.4, the effects of avalanche breakdown on bipolar transistor characteristics were described. As the reverse-bias voltages on the device are increased, carriers traversing the depletion regions gain sufficient energy to create new electron-hole pairs in lattice collisions by a process known as impact ionization. Eventually, at sufficient bias voltages, the process results in large avalanche currents. For collector-base bias voltages well below the breakdown value, a small enhanced current flow may occur across the collector-base junction due to this process, with little apparent effect on the device characteristics.

Impact ionization also occurs in MOS transistors but has a significantly different effect on the device characteristics. This difference is because the channel electrons (for the NMOS case) create electron-hole pairs in lattice collisions in the drain depletion region, and some of the resulting holes then flow to the substrate, creating a substrate current. (The electrons created in the process flow out the drain terminal.) The carriers created by impact ionization are therefore not confined within the device as in a bipolar transistor. The effect of this phenomenon can be modeled by inclusion of a controlled current generator $I_{D B}$ from drain to substrate, as shown
image_name:Figure 1.46
description:
[
name: M1, type: NMOS, ports: {S: S, D: D, G: G,B:B}
name: IDB, type: CurrentSource, value: IDB, ports: {Np: D, Nn: B}
]
extrainfo:The circuit represents an NMOS transistor with a controlled current source modeling impact ionization, flowing from the drain to the substrate.

Figure 1.46 Representation of impact ionization in an MOSFET by a drain-substrate current generator.
in Fig. 1.46 for an NMOS device. The magnitude of this substrate current depends on the voltage across the drain depletion region (which determines the energy of the ionizing channel electrons) and also on the drain current (which is the rate at which the channel electrons enter the depletion region). Empirical investigation has shown that the current $I_{D B}$ can be expressed as

$$
\begin{equation*}
I_{D B}=K_{1}\left(V_{D S}-V_{D S(\mathrm{act})}\right) I_{D} \exp \left(-\frac{K_{2}}{V_{D S}-V_{D S(\mathrm{act})}}\right) \tag{1.261}
\end{equation*}
$$

where $K_{1}$ and $K_{2}$ are process-dependent parameters and $V_{D S(\text { act })}$ is the minimum value of $V_{D S}$ for which the transistor operates in the active region. ${ }^{40}$ Typical values for NMOS devices are $K_{1}=5 \mathrm{~V}^{-1}$ and $K_{2}=30 \mathrm{~V}$. The effect is generally much less significant in PMOS devices because the holes carrying the charge in the channel are much less efficient in creating electronhole pairs than energetic electrons.

The major impact of this phenomenon on circuit performance is that it creates a parasitic resistance from drain to substrate. Because the common substrate terminal must always be connected to the most negative supply voltage in the circuit, the substrate of an NMOS device in a $p$-substrate process is an ac ground. Therefore, the parasitic resistance shunts the drain to ac ground and can be a limiting factor in many circuit designs. Differentiating (1.261), we find that the drain-substrate small-signal conductance is

$$
\begin{equation*}
g_{d b}=\frac{\partial I_{D B}}{\partial V_{D}}=\frac{I_{D B}}{V_{D S}-V_{D S(\mathrm{act})}}\left(\frac{K_{2}}{V_{D S}-V_{D S(\mathrm{act})}}+1\right) \simeq \frac{K_{2} I_{D B}}{\left(V_{D S}-V_{D S(\mathrm{act})}\right)^{2}} \tag{1.262}
\end{equation*}
$$

where the gate and the source are assumed to be held at fixed potentials.

#### EXAMPLE

Calculate $r_{d b}=1 / g_{d b}$ for $V_{D S}=2 \mathrm{~V}$ and 4 V , and compare with the device $r_{o}$. Assume $I_{D}=100 \mu \mathrm{~A}, \lambda=0.05 \mathrm{~V}^{-1}, V_{D S(\mathrm{act})}=0.3 \mathrm{~V}, K_{1}=5 \mathrm{~V}^{-1}$, and $K_{2}=30 \mathrm{~V}$.

For $V_{D S}=2 \mathrm{~V}$, we have from (1.261)

$$
I_{D B}=5 \times 1.7 \times 100 \times 10^{-6} \times \exp \left(-\frac{30}{1.7}\right) \simeq 1.8 \times 10^{-11} \mathrm{~A}
$$

From (1.262),

$$
g_{d b} \simeq \frac{30 \times 1.8 \times 10^{-11}}{1.7^{2}} \simeq 1.9 \times 10^{-10} \frac{\mathrm{~A}}{\mathrm{~V}}
$$

and thus

$$
r_{d b}=\frac{1}{g_{d b}} \simeq 5.3 \times 10^{9} \Omega=5.3 \mathrm{G} \Omega
$$

This result is negligibly large compared with

$$
r_{o}=\frac{1}{\lambda I_{D}}=\frac{1}{0.05 \times 100 \times 10^{-6}}=200 \mathrm{k} \Omega
$$

However, for $V_{D S}=4 \mathrm{~V}$,

$$
I_{D B}=5 \times 3.7 \times 100 \times 10^{-6} \times \exp \left(-\frac{30}{3.7}\right) \simeq 5.6 \times 10^{-7} \mathrm{~A}
$$

The substrate leakage current is now about 0.5 percent of the drain current. More important, we find from (1.262)

$$
g_{d b} \simeq \frac{30 \times 5.6 \times 10^{-7}}{3.7^{2}} \simeq 1.2 \times 10^{-6} \frac{\mathrm{~A}}{\mathrm{~V}}
$$

and thus

$$
r_{d b}=\frac{1}{g_{d b}} \simeq 8.15 \times 10^{5} \Omega=815 \mathrm{k} \Omega
$$

This parasitic resistor is now comparable to $r_{o}$ and can have a dominant effect on high-outputimpedance MOS current mirrors, as described in Chapter 4.

## APPENDIX

### A.1.1 SUMMARY OF ACTIVE-DEVICE PARAMETERS

### (a) npn Bipolar Transistor Parameters

| Quantity | Formula |
| :--- | :--- |
| Large-Signal Forward-Active | Operation |
| Small-Signal Forward-Active | $I_{c}=I_{S} \exp \frac{V_{b e}}{V_{T}}$ |
| Transcoration |  |
| Transconductance-to-current ratio | $g_{m}=\frac{q I_{C}}{k T}=\frac{I_{C}}{V_{T}}$ |
| Input resistance | $\frac{g_{m}}{I_{C}}=\frac{1}{V_{T}}$ |
| Output resistance | $r_{\pi}=\frac{\beta_{0}}{g_{m}}$ |
| Collector-base resistance | $r_{o}=\frac{V_{A}}{I_{C}}=\frac{1}{\eta g_{m}}$ |
| Base-charging capacitance | $r_{\mu}=\beta_{0} r_{o}$ to $5 \beta_{0} \mathrm{r}_{0}$ |
| Base-emitter capacitance | $C_{b}=\tau_{F} g_{m}$ |
| Emitter-base junction depletion capacitance | $C_{\pi}=C_{b}+C_{j e}$ |

(continued)

| Quantity | Formula |
| :--- | :--- |
| Collector-base junction <br> capacitance | $C_{\mu}=\frac{C_{\mu 0}}{\left(1-\frac{V_{B C}}{\psi_{0 c}}\right)^{n_{c}}}$ |
| Collector-substrate junction <br> capacitance | $C_{c s}=\frac{C_{c s 0}}{\left(1-\frac{V_{S C}}{\psi_{0 s}}\right)^{n_{s}}}$ |
| Transition frequency | $f_{T}=\frac{1}{2 \pi} \frac{g_{m}}{C_{\pi}+C_{\mu}}$ |
| Effective transit time | $\tau_{T}=\frac{1}{2 \pi f_{T}}=\tau_{F}+\frac{C_{j e}}{g_{m}}+\frac{C_{\mu}}{g_{m}}$ |
| Maximum gain | $=\frac{V_{A}}{V_{T}}=\frac{1}{\eta}$ |

### (b) NMOS Transistor Parameters

| Quantity | Formula |
| :--- | :--- |
|  | Large-Signal Operation |
| Drain current (active <br> region) | $I_{d}=\frac{\mu C_{o x}}{2} \frac{W}{L}\left(V_{g s}-V_{t}\right)^{2}$ |
| Drain current (triode <br> region) | $I_{d}=\frac{\mu C_{o x}}{2} \frac{W}{L}\left[2\left(V_{g s}-V_{t}\right) V_{d s}-V_{d s}{ }^{2}\right]$ |
| Threshold voltage | $V_{t}=V_{t 0}+\gamma\left[\sqrt{2 \phi_{f}+V_{s b}}-\sqrt{2 \phi_{f}}\right]$ |
| Threshold voltage <br> parameter | $\gamma=\frac{1}{C_{o x}} \sqrt{2 q \epsilon N_{A}}$ |
| Oxide capacitance |  |

### Small-Signal Operation (Active Region)

Top-gate transconductance $\quad g_{m}=\mu C_{o x} \frac{W}{L}\left(V_{G S}-V_{t}\right)=\sqrt{2 I_{D} \mu C_{o x} \frac{W}{L}}$
$\begin{gathered}\text { Transconductance-to- } \\ \text { current ratio }\end{gathered} \quad \frac{g_{m}}{I_{D}}=\frac{2}{V_{G S}-V_{t}}$
Body-effect
transconductance

$$
g_{m b}=\frac{\gamma}{2 \sqrt{2 \phi_{f}+V_{S B}}} g_{m}=\chi g_{m}
$$

image_name:Channel-length modulation parameter
description:The image contains a formula related to the channel-length modulation parameter in MOSFETs. It shows that the parameter \( \lambda \) is defined as:

\[ \lambda = \frac{1}{V_A} = \frac{1}{L_{\text{eff}}} \frac{dX_d}{dV_{DS}} \]

Where:
- \( \lambda \) is the channel-length modulation parameter.
- \( V_A \) is the Early voltage.
- \( L_{\text{eff}} \) is the effective channel length.
- \( X_d \) is the depletion layer width.
- \( V_{DS} \) is the drain-source voltage.

This formula indicates that the channel-length modulation parameter is inversely proportional to the Early voltage and is also related to the change in the depletion layer width with respect to the drain-source voltage, normalized by the effective channel length.

(continued)

| Quantity | Formula |
| :---: | :---: |
| Small-Signal Operation (Active Region) |  |
| Output resistance | $r_{o}=\frac{1}{\lambda I_{D}}=\frac{L_{\text {eff }}}{I_{D}}\left(\frac{d X_{d}}{d V_{D S}}\right)^{-1}$ |
| Effective channel length Maximum gain | $\begin{aligned} & L_{\mathrm{eff}}=L_{\mathrm{drwn}}-2 L_{d}-X_{d} \\ & g_{m} r_{o}=\frac{1}{\lambda} \frac{2}{V_{G S}-V_{t}}=\frac{2 V_{A}}{V_{G S}-V_{t}} \end{aligned}$ |
| Source-body depletion capacitance | $C_{s b}=\frac{C_{s b 0}}{\left(1+\frac{V_{S B}}{\psi_{0}}\right)^{0.5}}$ |
| Drain-body depletion capacitance | $C_{d b}=\frac{C_{d b 0}}{\left(1+\frac{V_{D B}}{\psi_{0}}\right)^{0.5}}$ |
| Gate-source capacitance Transition frequency | $\begin{aligned} C_{g s} & =\frac{2}{3} W L C_{o x} \\ f_{T} & =\frac{g_{m}}{2 \pi\left(C_{g s}+C_{g d}+C_{g b}\right)} \end{aligned}$ |
