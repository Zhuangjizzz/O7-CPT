# 1. Integrated-Circuit Devices and Modelling

In this chapter, both the operation and modelling of semiconductor devices are described. Although it is possible to do simple integrated-circuit design with a basic knowledge of semiconductor device modelling, for state-of-theart design, an in-depth understanding of the second-order effects of device operation and their modelling is considered critical.

It is assumed that most readers have been introduced to transistors and their basic modelling in a previous course. Thus, fundamental semiconductor concepts are only briefly reviewed. Section 1.1 describes pn junctions (or diodes). This section is important in understanding the parasitic capacitances in many device models, such as junction capacitances. Section 1.2 covers the basics of MOS transistors and modelling. A summary of device models and important equations is presented in Section 1.3. This summary is particularly useful for a reader who already has a good background in transistor modelling, in which case the summary can be used to follow the notation used throughout the remainder of this book. Advanced MOS modelling is treated in Section 1.4, including behavior not covered by a simple square-law voltage-current relationship. It should be noted that all sections on MOS devices rely to some degree on the material previously presented in Section 1.1, in which depletion capacitance is covered. In addition, a brief description is given of the most important process-related parameters used in SPICE modelling in Section 1.5. Since passive devices are often required for analog design, the most common passives on integrated circuits are described in Section 1.6. Finally, this chapter concludes with an Appendix containing derivations of the more physically-based device equations.

## 1.1 SEMICONDUCTORS AND pn JUNCTIONS

A semiconductor is a crystal lattice structure that can have free electrons (which are negative carriers) and/or free holes (which are an absence of electrons and are equivalent to positive carriers). The type of semiconductor typically used is silicon, an abundant element found, for example, in high concentrations in sand. This material has a valence of four, implying that each atom has four electrons to share with neighboring atoms when forming the covalent bonds of the crystal lattice. Intrinsic silicon (i.e., undoped silicon) is a very pure crystal structure that has equal numbers of free electrons and holes. These free carriers are those electrons that have gained enough energy due to thermal agitation to escape their bonds, and the resulting holes that they leave behind. At room temperature, there are approximately $1.1 \times 10^{10}$ carriers of each type per $\mathrm{cm}^{3}$, or equivalently $\mathrm{n}_{\mathrm{i}}=1.1 \times 10^{16}$ carriers $/ \mathrm{m}^{3}$, defined as the carrier concentration of intrinsic silicon. The number of carriers approximately doubles for every $11^{\circ} \mathrm{C}$ increase in temperature.

If one dopes silicon with a pentavalent impurity (i.e., atoms of an element having a valence of five, or equivalently five electrons in the outer shell, available when bonding with neighboring atoms), there will be almost one extra free electron for every impurity atom. ${ }^{1}$ These free electrons can be used to conduct current. A pentavalent

[^0]impurity is said to donate free electrons to the silicon crystal, and thus the impurity is known as a donor. Examples of donor elements are phosphorus, P , and arsenic, As. These impurities are also called n-type dopants since the free carriers resulting from their use have negative charge. When an n-type impurity is used, the total number of negative carriers or electrons is almost the same as the doping concentration, and is much greater than the number of free electrons in intrinsic silicon. In other words,
\$\$

$$
\begin{equation*}
\mathrm{n}_{\mathrm{n}}=\mathrm{N}_{\mathrm{D}} \tag{1.1}
\end{equation*}
$$

$$
where $n_{n}$ denotes the free-electron concentration in $n$-type material and $N_{D}$ is the doping concentration (with the subscript D denoting donor). On the other hand, the number of free holes in $n$-doped material will be much less than the number of holes in intrinsic silicon and can be shown [Sze, 1981] to be given by
$$

$$
\begin{equation*}
\mathrm{p}_{\mathrm{n}}=\frac{\mathrm{n}_{\mathrm{i}}^{2}}{\mathrm{~N}_{\mathrm{D}}} \tag{1.2}
\end{equation*}
$$

\$\$

Similarly, if one dopes silicon with atoms that have a valence of three, for example, boron (B), the concentration of positive carriers or holes will be approximately equal to the acceptor concentration, $\mathrm{N}_{\mathrm{A}}$,

$$
\begin{equation*}
\mathrm{p}_{\mathrm{p}}=\mathrm{N}_{\mathrm{A}} \tag{1.3}
\end{equation*}
$$

and the number of negative carriers in the p -type silicon, $\mathrm{n}_{\mathrm{p}}$, is given by

$$
\begin{equation*}
\mathrm{n}_{\mathrm{p}}=\frac{\mathrm{n}_{\mathrm{i}}^{2}}{\mathrm{~N}_{\mathrm{A}}} \tag{1.4}
\end{equation*}
$$

### EXAMPLE 1.1

Intrinsic silicon is doped with boron at a concentration of $10^{26}$ atoms $/ \mathrm{m}^{3}$. At room temperature, what are the concentrations of holes and electrons in the resulting doped silicon? Assume that $\mathrm{n}_{\mathrm{i}}=1.1 \times 10^{16}$ carriers $/ \mathrm{m}^{3}$.

### Solution

The hole concentration, $p_{p}$, will approximately equal the doping concentration $\left(p_{p}=N_{A}=10^{26}\right.$ holes $\left./ \mathrm{m}^{3}\right)$. The electron concentration is found from (1.4) to be

$$
\begin{equation*}
\mathrm{n}_{\mathrm{p}}=\frac{\left(1.1 \times 10^{16}\right)^{2}}{10^{26}}=1.2 \times 10^{6} \text { electrons } / \mathrm{m}^{3} \tag{1.5}
\end{equation*}
$$

Such doped silicon is referred to as p-type since it has many more free holes than free electrons.

### 1.1.1 Diodes

To realize a diode, also called a pn junction, one part of a semiconductor is doped $n$-type and an adjacent part is doped p -type, as shown in Fig. 1.1. The diode, or junction, is formed between the $\mathrm{p}^{+}$region and the n region, where superscripts are used to indicate the relative doping levels. For example, the $\mathrm{p}^{-}$bulk region in Fig. 1.1 might have an impurity concentration of $5 \times 10^{21}$ carriers $/ \mathrm{m}^{3}$, whereas the $\mathrm{p}^{+}$and $\mathrm{n}^{+}$regions would be doped more
image_name:Fig. 1.1
description:
[
name: Diode, type: Diode, ports: {Na: Anode, Nc: Cathode}
]
extrainfo:The diagram shows a cross-section of a pn junction diode with p+ and n+ regions heavily doped. The anode is connected to the p+ region and the cathode is connected to the n+ region. Metal contacts are made with aluminum to prevent Schottky diode formation.

Fig. 1.1 A cross section of a pn diode.
heavily to a value around $10^{25}$ to $10^{27}$ carriers $/ \mathrm{m}^{3}{ }^{2}$ Also, note that the metal contacts to the diode (in this case, aluminum) are connected to heavily doped regions, otherwise a Schottky diode would form. (Schottky diodes are discussed on page 13.) Thus, in order not to make a Schottky diode, the connection to the n region is actually made via the $\mathrm{n}^{+}$region.

In the $\mathrm{p}^{+}$side, a large number of free positive carriers are available, whereas in the n side, many free negative carriers are available. The holes in the $\mathrm{p}^{+}$side will tend to disperse or diffuse into the n side, whereas the free electrons in the n side will tend to diffuse to the $\mathrm{p}^{+}$side. This process is very similar to two gases randomly diffusing together. This diffusion lowers the concentration of free carriers in the region between the two sides. As the two types of carriers diffuse together, they recombine. Every electron that diffuses from the n side to the p side leaves behind a bound positive charge close to the transition region. Similarly, every hole that diffuses from the p side leaves behind a bound electron near the transition region. The end result is shown in Fig. 1.2. This diffusion of free carriers creates a depletion region at the junction of the two sides where no free carriers exist, and which has a net negative charge on the $\mathrm{p}^{+}$side and a net positive charge on the n side. The total amount of exposed or bound charge on the two sides of the junction must be equal for charge neutrality. This requirement causes the depletion region to extend farther into the more lightly doped n side than into the $\mathrm{p}^{+}$side.

As these bound charges are exposed, an electric field develops going from the n side to the $\mathrm{p}^{+}$side. This electric field gives rise to a potential difference between the n and $\mathrm{p}^{+}$sides, called the built-in voltage of the junction. It opposes the diffusion of free carriers until there is no net movement of charge under open-circuit and steadystate conditions. The built-in voltage of an open-circuit pn junction is [Sze 1981]

$$
\begin{equation*}
\Phi_{0}=\mathrm{V}_{\mathrm{T}} \ln \left(\frac{\mathrm{~N}_{\mathrm{A}} \mathrm{~N}_{\mathrm{D}}}{\mathrm{n}_{\mathrm{i}}^{2}}\right) \tag{1.6}
\end{equation*}
$$

where

$$
\begin{equation*}
V_{T}=\frac{k T}{q} \tag{1.7}
\end{equation*}
$$

T is the temperature in degrees Kelvin ( $\cong 300^{\circ} \mathrm{K}$ at room temperature), k is Boltzmann's constant $\left(1.38 \times 10^{-23} \mathrm{JK}^{-1}\right)$, and q is the charge of an electron $\left(1.602 \times 10^{-19} \mathrm{C}\right)$. At room temperature, $\mathrm{V}_{\mathrm{T}}$ is approximately 26 mV .

#### EXAMPLE 1.2

A pn junction has $\mathrm{N}_{\mathrm{A}}=10^{25}$ holes $/ \mathrm{m}^{3}$ and $\mathrm{N}_{\mathrm{D}}=10^{22}$ electrons $/ \mathrm{m}^{3}$. What is the built-in junction potential? Assume that $\mathrm{n}_{\mathrm{i}}=1.1 \times 10^{16}$ carriers $/ \mathrm{m}^{3}$.

#### Solution

Using (1.6), we obtain

$$
\begin{equation*}
\Phi_{0}=0.026 \times \ln \left(\frac{10^{25} \times 10^{22}}{\left(1.1 \times 10^{16}\right)^{2}}\right)=0.89 \mathrm{~V} \tag{1.8}
\end{equation*}
$$

This is a typical value for the built-in potential of a junction with one side heavily doped. As an approximation, we will normally use $\Phi_{0} \cong 0.9 \mathrm{~V}$ for the built-in potential of a junction having one side heavily doped.

### 1.1.2 Reverse-Biased Diodes

A silicon diode having an anode-to-cathode (i.e., p side to n side) voltage of 0.4 V or less will not be conducting appreciable current. In this case, it is said to be reverse-biased. If a diode is reverse-biased, current flow is primarily due to thermally generated carriers in the depletion region, and it is extremely small. Although this reverse-biased current is only weakly dependent on the applied voltage, the reverse-biased current is directly proportional to the area of the diode junction. However, an effect that should not be ignored, particularly at high frequencies, is the junction capacitance of a diode. In reverse-biased diodes, this junction capacitance is due to varying charge storage in the depletion regions and is modelled as a depletion capacitance.

To determine the depletion capacitance, we first state the relationship between the depletion widths and the applied reverse voltage, $\mathrm{V}_{\mathrm{R}}$ [Sze, 1981].

$$
\begin{align*}
& x_{n}=\left[\frac{2 \mathrm{~K}_{\mathrm{s}} \varepsilon_{0}\left(\Phi_{0}+\mathrm{V}_{\mathrm{R}}\right)}{\mathrm{q}} \frac{\mathrm{~N}_{\mathrm{A}}}{\mathrm{~N}_{\mathrm{D}}\left(\mathrm{~N}_{\mathrm{A}}+\mathrm{N}_{\mathrm{D}}\right)}\right]^{1 / 2}  \tag{1.9}\\
& \mathrm{x}_{\mathrm{p}}=\left[\frac{2 \mathrm{~K}_{\mathrm{s}} \varepsilon_{0}\left(\Phi_{0}+\mathrm{V}_{\mathrm{R}}\right)}{\mathrm{q}} \frac{\mathrm{~N}_{\mathrm{D}}}{\mathrm{~N}_{\mathrm{A}}\left(\mathrm{~N}_{\mathrm{A}}+\mathrm{N}_{\mathrm{D}}\right)}\right]^{1 / 2} \tag{1.10}
\end{align*}
$$

Here, $\varepsilon_{0}$ is the permittivity of free space (equal to $8.854 \times 10^{-12} \mathrm{~F} / \mathrm{m}$ ), $\mathrm{V}_{\mathrm{R}}$ is the reverse-bias voltage of the diode, and $\mathrm{K}_{\mathrm{s}}$ is the relative permittivity of silicon (equal to 11.8). These equations assume an abrupt junction where the doping changes instantly from the n to the p side. Modifications to these equations for graded junctions are treated in the next section.

From the above equations, we see that if one side of the junction is more heavily doped than the other, the depletion region will extend mostly on the lightly doped side. For example, if $N_{A} \gg N_{D}$ (i.e., if the $p$ region is more heavily doped), we can approximate (1.9) and (1.10) as

$$
\begin{equation*}
\mathrm{x}_{\mathrm{n}} \cong\left[\frac{2 \mathrm{~K}_{\mathrm{s}} \varepsilon_{0}\left(\Phi_{0}+\mathrm{V}_{\mathrm{R}}\right)}{\mathrm{qN}}\right]^{1 / 2} \mathrm{x}_{\mathrm{p}} \cong\left[\frac{2 \mathrm{~K}_{\mathrm{s}} \varepsilon_{0}\left(\Phi_{0}+\mathrm{V}_{\mathrm{R}}\right) \mathrm{N}_{\mathrm{D}}}{q N_{A}^{2}}\right]^{1 / 2} \tag{1.11}
\end{equation*}
$$

Indeed, for this case

$$
\begin{equation*}
\frac{x_{n}}{x_{p}} \cong \frac{N_{A}}{N_{D}} \tag{1.12}
\end{equation*}
$$

This special case is called a single-sided diode.

#### EXAMPLE 1.3

For a pn junction having $\mathrm{N}_{\mathrm{A}}=10^{25}$ holes $/ \mathrm{m}^{3}$ and $\mathrm{N}_{\mathrm{D}}=10^{22}$ electrons $/ \mathrm{m}^{3}$, what are the depletion region depths for a $1-\mathrm{V}$ reverse-bias voltage?

#### Solution

Since $\mathrm{N}_{\mathrm{A}} \gg>\mathrm{N}_{\mathrm{D}}$ and we already have found in Example 1.2 that $\Phi_{0}=0.9 \mathrm{~V}$, we can use (1.11) to find

$$
\begin{gather*}
\mathrm{x}_{\mathrm{n}}=\left[\frac{2 \times 11.8 \times 8.854 \times 10^{-12} \times 1.9}{1.6 \times 10^{-19} \times 10^{22}}\right]^{1 / 2}=0.50 \mu \mathrm{~m}  \tag{1.13}\\
\mathrm{x}_{\mathrm{p}}=\frac{\mathrm{x}_{\mathrm{n}}}{\left(\mathrm{~N}_{\mathrm{A}} / \mathrm{N}_{\mathrm{D}}\right)}=0.50 \mathrm{~nm} \tag{1.14}
\end{gather*}
$$

Note that the depletion region width in the lightly doped n region is 1,000 times greater than that in the more heavily doped $p$ region.

The charge stored in the depletion region, per unit cross-sectional area, is found by multiplying the depletion region width by the concentration of the immobile charge (which is approximately equal to q times the impurity doping density). For example, on the n side, we find the charge in the depletion region to be given by multiplying (1.9) by $\mathrm{qN}_{\mathrm{D}}$, resulting in

$$
\begin{equation*}
\mathrm{Q}^{+}=\left[2 \mathrm{qK}_{\mathrm{s}} \varepsilon_{0}\left(\Phi_{0}+\mathrm{V}_{\mathrm{R}}\right) \frac{\mathrm{N}_{\mathrm{A}} \mathrm{~N}_{\mathrm{D}}}{\mathrm{~N}_{\mathrm{A}}+\mathrm{N}_{\mathrm{D}}}\right]^{1 / 2} \tag{1.15}
\end{equation*}
$$

This amount of charge must also equal $\mathrm{Q}^{-}$on the p side since there is charge equality. In the case of a single-sided diode when $N_{A} \gg N_{D}$, we have

$$
\begin{equation*}
\mathrm{Q}^{-}=\mathrm{Q}^{+} \cong\left[2 \mathrm{qK}_{\mathrm{s}} \varepsilon_{0}\left(\Phi_{0}+\mathrm{V}_{\mathrm{R}}\right) \mathrm{N}_{\mathrm{D}}\right]^{1 / 2} \tag{1.16}
\end{equation*}
$$

Key Point: The chargevoltage relationship of a reverse-biased pn junction is modeled by a nonlinear depletion capacitance.

Note that this result is independent of the impurity concentration on the heavily doped side. Thus, we see from the above relation that the charge stored in the depletion region is nonlinearly dependent on the applied reverse-bias voltage. This charge-voltage relationship is modelled by a nonlinear depletion capacitance.

For small changes in the reverse-biased junction voltage, about a bias voltage, we can find an equivalent small-signal capacitance, $\mathrm{C}_{\mathrm{j}}$, by differentiating (1.15) with respect to $\mathrm{V}_{\mathrm{R}}$. Such a differentiation results in

$$
\begin{equation*}
C_{j}=\frac{\mathrm{dQ}^{+}}{d V_{R}}=\left[\frac{q K_{s} \varepsilon_{0}}{2\left(\Phi_{0}+V_{R}\right)} \frac{N_{A} N_{D}}{N_{A}+N_{D}}\right]^{1 / 2}=\frac{C_{j 0}}{\sqrt{1+\frac{V_{B}}{\Phi_{0}}}} \tag{1.17}
\end{equation*}
$$

where $C_{j 0}$ is the depletion capacitance per unit area at $V_{R}=0$ and is given by

$$
\begin{equation*}
C_{j} 0=\sqrt{\frac{q K_{s} \varepsilon_{0}}{2 \Phi_{0}} \frac{N_{A} N_{D}}{N_{A}+N_{D}}} \tag{1.18}
\end{equation*}
$$

In the case of a one-sided diode with $\mathrm{N}_{\mathrm{A}} \gg \mathrm{N}_{\mathrm{D}}$, we have

$$
\begin{equation*}
\mathrm{C}_{\mathrm{j}}=\left[\frac{\mathrm{qK}_{\mathrm{s}} \varepsilon_{0} \mathrm{~N}_{\mathrm{D}}}{2\left(\Phi_{0}+\mathrm{V}_{\mathrm{R}}\right)}\right]^{1 / 2}=\frac{\mathrm{C}_{\mathrm{j} 0}}{\sqrt{1+\frac{\mathrm{V}_{\mathrm{R}}}{\Phi_{0}}}} \tag{1.19}
\end{equation*}
$$

where now

$$
\begin{equation*}
C_{j 0}=\sqrt{\frac{q K_{s} \varepsilon_{0} N_{D}}{2 \Phi_{0}}} \tag{1.20}
\end{equation*}
$$

It should be noted that many of the junctions encountered in integrated circuits are one-sided junctions with the lightly doped side being the substrate or sometimes what is called the well. The more heavily doped side is often used to form a contact to interconnecting metal. From (1.20), we see that, for these one-sided junctions, the depletion capacitance is approximately independent of the doping concentration on the heavily doped side, and is proportional to the square root of the doping concentration of the more lightly doped side. Thus, smaller depletion capacitances are obtained for more lightly doped substrates - a strong incentive to strive for lightly doped substrates.

Finally, note that by combining (1.15) and (1.18), we can express the equation for the immobile charge on either side of a reverse-biased junction as

$$
\begin{equation*}
\mathrm{Q}=2 \mathrm{C}_{\mathrm{j} 0} \Phi_{0} \sqrt{1+\frac{\mathrm{V}_{\mathrm{R}}}{\Phi_{0}}} \tag{1.21}
\end{equation*}
$$

As seen in Example 1.6, this equation is useful when one is approximating the large-signal charging (or discharging) time for a reverse-biased diode.

#### EXAMPLE 1.4

For a pn junction having $\mathrm{N}_{\mathrm{A}}=10^{25}$ holes $/ \mathrm{m}^{3}$ and $\mathrm{N}_{\mathrm{D}}=10^{22}$ electrons $/ \mathrm{m}^{3}$, what is the total zero-bias depletion capacitance for a diode of area $10 \mu \mathrm{~m} \times 10 \mu \mathrm{~m}$ ? What is its depletion capacitance for a 3-V reverse-bias voltage?

#### Solution

Making use of (1.20), we have

$$
\begin{equation*}
C_{j 0}=\sqrt{\frac{1.6 \times 10^{-19} \times 11.8 \times 8.854 \times 10^{-12} \times 10^{22}}{2 \times 0.9}}=304.7 \mu \mathrm{~F} / \mathrm{m}^{2} \tag{1.22}
\end{equation*}
$$

Since the diode area is $100 \times 10^{-12} \mathrm{~m}^{2}$, the total zero-bias depletion capacitance is

$$
\begin{equation*}
\mathrm{C}_{\mathrm{T}-\mathrm{j} 0}=100 \times 10^{-12} \times 304.7 \times 10^{-6}=30.5 \mathrm{fF} \tag{1.23}
\end{equation*}
$$

At a 3-V reverse-bias voltage, we have from (1.19)

$$
\begin{equation*}
\mathrm{C}_{\mathrm{T}-\mathrm{j}}=\frac{30.5 \mathrm{fF}}{\sqrt{1+\left(\frac{3}{0.9}\right)}}=14.7 \mathrm{fF} \tag{1.24}
\end{equation*}
$$

We see a decrease in junction capacitance as the width of the depletion region is increased.

### 1.1.3 Graded Junctions

All of the above equations assumed an abrupt junction where the doping concentration changes quickly from p to n over a small distance. Although this is a good approximation for many integrated circuits, it is not always so. For example, the collector-to-base junction of a bipolar transistor is most commonly realized as a graded junction. In the case of graded junctions, the exponent $1 / 2$ in (1.15) is inaccurate, and an exponent closer to unity is more accurate, perhaps 0.6 to 0.7 . Thus, for graded junctions, (1.15) is typically written as

$$
\begin{equation*}
Q=\left[2 q K_{s} \varepsilon_{0}\left(\Phi_{0}+V_{R}\right) \frac{N_{A} N_{D}}{N_{A}+N_{D}}\right]^{1-m_{j}} \tag{1.25}
\end{equation*}
$$

where $m_{j}$ is a constant that depends upon the doping profile. For example, a linearly graded junction has $m_{j}=1 / 3$.
Differentiating (1.25) to find the depletion capacitance, we have

$$
\begin{equation*}
C_{j}=\left(1-m_{j}\right)\left[2 q K_{s} \varepsilon_{0} \frac{N_{A} N_{D}}{N_{A}+N_{D}}\right]^{1-m_{j}} \frac{1}{\left(\Phi_{0}+V_{R}\right)^{m_{j}}} \tag{1.26}
\end{equation*}
$$

This depletion capacitance can also be written as

$$
\begin{equation*}
C_{j}=\frac{C_{j 0}}{\left(1+\frac{V_{R}}{\Phi_{0}}\right)^{m_{j}}} \tag{1.27}
\end{equation*}
$$

where

$$
\begin{equation*}
C_{j 0}=\left(1-m_{j}\right)\left[2 q K_{s} \varepsilon_{0} \frac{N_{A} N_{D}}{N_{A}+N_{D}}\right]^{1-m_{j}} \frac{1}{\Phi_{0}^{m_{j}}} \tag{1.28}
\end{equation*}
$$

From (1.27), we see that a graded junction results in a depletion capacitance that is less dependent on $\mathrm{V}_{\mathrm{R}}$ than the equivalent capacitance in an abrupt junction. In other words, since $m$ is less than 0.5 , the depletion capacitance for a graded junction is more linear than that for an abrupt junction. Correspondingly, increasing the reverse-bias voltage for a graded junction is not as effective in reducing the depletion capacitance as it is for an abrupt junction.

Finally, as in the case of an abrupt junction, the depletion charge on either side of the junction can also be written as

$$
\begin{equation*}
\mathrm{Q}=\frac{\mathrm{C}_{\mathrm{j} 0}}{1-\mathrm{m}_{\mathrm{j}}} \Phi_{0}\left(1+\frac{\mathrm{V}_{\mathrm{R}}}{\Phi_{0}}\right)^{1-\mathrm{m}_{\mathrm{j}}} \tag{1.29}
\end{equation*}
$$

#### EXAMPLE 1.5

Repeat Example 1.4 for a graded junction with $\mathrm{m}_{\mathrm{j}}=0.4$.

#### Solution

Noting once again that $N_{A} \gg N_{D}$, we approximate (1.28) as

$$
\begin{equation*}
\mathrm{C}_{\mathrm{j} 0}=\left(1-\mathrm{m}_{\mathrm{j}}\right)\left[2 \mathrm{qK}_{\mathrm{s}} \varepsilon_{0} \mathrm{~N}_{\mathrm{D}}\right]^{1-\mathrm{m}_{\mathrm{j}}} \frac{1}{\Phi_{0}^{m_{\mathrm{j}}}} \tag{1.30}
\end{equation*}
$$

resulting in

$$
\begin{equation*}
\mathrm{C}_{\mathrm{j} 0}=81.5 \mu \mathrm{~F} / \mathrm{m}^{2} \tag{1.31}
\end{equation*}
$$

which, when multiplied by the diode's area of $10 \mu \mathrm{~m} \times 10 \mu \mathrm{~m}$, results in

$$
\begin{equation*}
\mathrm{C}_{\mathrm{T}-\mathrm{j} 0}=8.1 \mathrm{fF} \tag{1.32}
\end{equation*}
$$

For a 3-V reverse-bias voltage, we have

$$
\begin{equation*}
\mathrm{C}_{\mathrm{T}-\mathrm{j}}=\frac{8.1 \mathrm{fF}}{(1+3 / 0.9)^{0.4}}=4.5 \mathrm{fF} \tag{1.33}
\end{equation*}
$$

### 1.1.4 Large-Signal Junction Capacitance

The equations for the junction capacitance given above are only valid for small changes in the reverse-bias voltage. This limitation is due to the fact that $\mathrm{C}_{\mathrm{j}}$ depends on the size of the reverse-bias voltage instead of being a constant. As a result, it is extremely difficult and time consuming to accurately take this nonlinear capacitance into account when calculating the time to charge or discharge a junction over a large voltage change. A commonly used approximation when analyzing the transient response for large voltage changes is to use an average size for the junction capacitance by calculating the junction capacitance at the two extremes of the reverse-bias voltage. Unfortunately, a problem with this approach is that when the diode is forward biased with $\mathrm{V}_{\mathrm{R}} \cong-\Phi_{0}$, equation (1.17) "blows up" (i.e., is equal to infinity). To circumvent this problem, one can instead calculate the charge stored in the junction for the two extreme values of applied voltage (through the use of (1.21)), and then through the use of $\mathrm{Q}=\mathrm{CV}$, calculate the average capacitance according to

$$
\begin{equation*}
C_{j-\mathrm{av}}=\frac{Q\left(V_{2}\right)-Q\left(V_{1}\right)}{V_{2}-V_{1}} \tag{1.34}
\end{equation*}
$$

where $\mathrm{V}_{1}$ and $\mathrm{V}_{2}$ are the two voltage extremes [Hodges, 1988].
From (1.21), for an abrupt junction with reverse-bias voltage $V_{i}$, we have

$$
\begin{equation*}
\mathrm{Q}\left(\mathrm{~V}_{\mathrm{i}}\right)=2 \mathrm{C}_{\mathrm{j} 0} \Phi_{0} \sqrt{1+\frac{\mathrm{V}_{\mathrm{i}}}{\Phi_{0}}} \tag{1.35}
\end{equation*}
$$

Therefore,

$$
\begin{equation*}
\mathrm{C}_{\mathrm{j}-\mathrm{av}}=2 \mathrm{C}_{\mathrm{j} 0} \Phi_{0} \frac{\left(\sqrt{1+\frac{\mathrm{V}_{2}}{\Phi_{0}}}-\sqrt{1+\frac{\mathrm{V}_{1}}{\Phi_{0}}}\right)}{\mathrm{V}_{2}-\mathrm{V}_{1}} \tag{1.36}
\end{equation*}
$$

#### EXAMPLE 1.6

For the circuit shown in Fig. 1.3, where a reverse-biased diode is being charged from 0 V to 1 V , through a $10-\mathrm{k} \Omega$ resistor, calculate the time required to charge the diode from 0 V to 0.7 V . Assume that $\mathrm{C}_{\mathrm{j} 0}=0.2 \mathrm{fF} /(\mu \mathrm{m})^{2}$ and that the diode has an area of $20 \mu \mathrm{~m} \times 5 \mu \mathrm{~m}$. Compare your answer to that obtained using SPICE. Repeat the question for the case of the diode being discharged from 1 V to 0.3 V .

#### Solution

For the special case of $\mathrm{V}_{1}=0 \mathrm{~V}$ and $\mathrm{V}_{2}=1 \mathrm{~V}$, and using $\Phi_{0}=0.9 \mathrm{~V}$ in equation (1.36) we find that

$$
\begin{equation*}
C_{j-a v}=0.815 C_{j 0} \tag{1.37}
\end{equation*}
$$

Thus, as a rough approximation to quickly estimate the charging time of a junction capacitance from 0 V to 1 V (or vice versa), one can use

$$
\begin{equation*}
C_{j-a v} \cong 0.8 C_{j 0} \tag{1.38}
\end{equation*}
$$

The total small-signal capacitance of the junction at $0-\mathrm{V}$ bias voltage is obtained by multiplying $0.2 \mathrm{fF} /(\mu \mathrm{m})^{2}$ by the junction area to obtain

$$
\begin{equation*}
C_{T-j 0}=0.2 \times 10^{-15} \times 20 \times 5=0.02 \mathrm{pF} \tag{1.39}
\end{equation*}
$$

Fig. 1.3 (a) The circuit used in
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: 1 V, ports: {Np: Vin, Nn: GND}
name: R, type: Resistor, value: 10 kΩ, ports: {N1: Vin, N2: Vout}
name: Diode, type: Diode, ports: {Na: Cj0, Nc: Vout}
name: Cj0, type: Capacitor, value: 0.2 fF/(μm)^2, ports: {Np: Cj0, Nn: GND}
]
extrainfo:The circuit consists of a voltage source Vin, a resistor R, a diode, and a capacitor Cj0. The resistor and diode are connected in series with the voltage source, and the capacitor is connected in parallel with the diode. The diode has a junction area of 20 μm × 5 μm.

image_name:(b)
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: GND}
name: R, type: Resistor, value: 10kΩ, ports: {N1: Vin, N2: Vout}
name: C_eq, type: Capacitor, value: 0.016pF, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is a simple RC low-pass filter consisting of a voltage source Vin, a resistor R, and a capacitor C_eq. The resistor and capacitor form an RC network that filters high-frequency signals, allowing low-frequency signals to pass through to the output Vout. The time constant of the circuit is given by τ = R * C_eq = 0.16 ns.

Example 1.6; (b) its RC approximate equivalent.

Using (1.37), we have

$$
\begin{equation*}
\mathrm{C}_{\mathrm{T}-\mathrm{j}-\mathrm{av}}=0.815 \times 0.02=0.016 \mathrm{pF} \tag{1.40}
\end{equation*}
$$

resulting in a time constant of

$$
\begin{equation*}
\tau=R C_{j-a v}=0.16 \mathrm{~ns} \tag{1.41}
\end{equation*}
$$

It is not difficult to show that the time it takes for a first-order circuit to rise (or fall) 70 percent of its final value is equal to $1.2 \tau$. Thus, in this case,

$$
\begin{equation*}
\mathrm{t}_{70 \%}=1.2 \tau=0.20 \mathrm{~ns} \tag{1.42}
\end{equation*}
$$

As a check, the circuit of Fig. 1.3(a) was analyzed using SPICE. The SPICE simulation gave a $0-\mathrm{V}$ to $0.7-\mathrm{V}$ rise time of 0.21 ns and a $1-\mathrm{V}$ to $0.3-\mathrm{V}$ fall time of 0.19 ns , in general agreement with the 0.20 ns predicted. The reason for the different values of the rise and fall times is the nonlinearity of the junction capacitance. For smaller bias voltages it is larger than that predicted by (1.37), whereas for larger bias voltages it is smaller. Normally, the extra accuracy that results from performing a more accurate analysis is not worth the extra complication because one seldom knows the value of $\mathrm{C}_{\mathrm{j} 0}$ to better than 20 percent accuracy.

### 1.1.5 Forward-Biased Junctions

A positive voltage applied from the p side to the n side of a diode reduces the electric field opposing the diffusion of the free carriers across the depletion region. It also reduces the width of the depletion region. If this forward-bias voltage is large enough, the carriers will start to diffuse across the junction, resulting in a current flow from the anode to the cathode. For silicon, appreciable diode current starts to occur for a forward-bias
voltage around 0.5 V . For germanium and gallium arsenide semiconductor materials, current conduction starts to occur around 0.3 V and 0.9 V , respectively.

When the junction potential is sufficiently lowered for conduction to occur, the carriers diffuse across the junction due to the large gradient in the mobile carrier concentrations. Note that there are more carriers diffusing from the heavily doped side to the lightly doped side than from the lightly doped side to the heavily doped side.

After the carriers cross the depletion region, they greatly increase the minority charge at the edge of the depletion region. These minority carriers will diffuse away from the junction toward the bulk. As they diffuse, they recombine with the majority carriers, thereby decreasing their concentration. This concentration gradient of the minority charge (which decreases the farther one gets from the junction) is responsible for the current flow near the junction.

The majority carriers that recombine with the diffusing minority carriers come from the metal contacts at the junctions because of the forward-bias voltage. These majority carriers flow across the bulk, from the contacts to the junction, due to an electric field applied across the bulk. This current flow is called drift. It results in small potential drops across the bulk, especially in the lightly doped side. Typical values of this voltage drop might be 50 mV to 0.1 V , depending primarily on the doping concentration of the lightly doped side, the distance from the contacts to the junction, and the cross-sectional area of the junction.

In the forward-bias region, the current-voltage relationship is exponential and can be shown (see Appendix) to be

$$
\begin{equation*}
I_{D}=I_{S} e^{V_{D} V_{T}} \tag{1.43}
\end{equation*}
$$

where $\mathrm{V}_{\mathrm{D}}$ is the voltage applied across the diode and

$$
\begin{equation*}
I_{S} \propto A_{D}\left(\frac{1}{N_{A}}+\frac{1}{N_{D}}\right) \tag{1.44}
\end{equation*}
$$

$I_{S}$ is known as the scale current and is seen to be proportional to the area of the diode junction, $A_{D}$, and inversely proportional to the doping concentrations.

### 1.1.6 Junction Capacitance of Forward-Biased Diode

When a junction changes from reverse biased (with little current through it) to forward biased (with significant current flow across it), the charge being stored near and across the junction changes. Part of the change in charge is due to the change in the width of the depletion region and therefore the amount of immobile charge stored in it. This change in charge is modelled by the depletion capacitance, $C_{j}$, similar to when the junction is reverse biased. An additional change in charge storage is necessary to account for the change of the minority carrier concentration close to the junction required for the diffusion current to exist. For example, if a forward-biased diode current is to double, then the slopes of the minority charge storage at the diode junction edges must double, and this, in turn, implies that the minority charge storage must double. This component is modelled by another capacitance, called the diffusion capacitance, and denoted $\mathrm{C}_{\mathrm{d}}$.

The diffusion capacitance can be shown (see Appendix) to be

$$
\begin{equation*}
\mathrm{C}_{\mathrm{d}}=\tau_{\mathrm{T}} \frac{\mathrm{I}_{\mathrm{D}}}{\mathrm{~V}_{\mathrm{T}}} \tag{1.45}
\end{equation*}
$$

where $\tau_{\top}$ is the transit time of the diode. Normally $\tau_{\top}$ is specified for a given technology, so that one can calculate the diffusion capacitance. Note that the diffusion capac itance of a forward-biased junction is proportional to the diode current.

The total capacitance of the forward-biased junction is the sum of the diffusion capacitance, $\mathrm{C}_{\mathrm{d}}$, and the depletion capacitance, $\mathrm{C}_{\mathrm{j}}$. Thus, the total junction capacitance is given by

$$
\begin{equation*}
C_{T}=C_{d}+C_{j} \tag{1.46}
\end{equation*}
$$

For a forward-biased junction, the depletion capacitance, $C_{j}$, can be roughly approximated by $2 C_{j 0}$. The accuracy of this approximation is not critical since the diffusion capacitance is typically much larger than the depletion capacitance.

Finally, it should be mentioned that as a diode is turned off for a short period of time a current will flow in the negative direction until the minority charge is removed. This behavior does not occur in Schottky diodes since they do not have minority charge storage.

### 1.1.7 Small-Signal Model of a Forward-Biased Diode

image_name:Fig. 1.4
description:
[
name: rd, type: Resistor, value: rd, ports: {N1: X, N2: Y}
name: Cj, type: Capacitor, value: Cj, ports: {Np: Y, Nn: Z}
name: Cd, type: Capacitor, value: Cd, ports: {Np: Y, Nn: Z}
]
extrainfo:This is a small-signal model of a forward-biased diode, showing the resistive and capacitive components connected in parallel.

Fig. 1.4 The small-signal model for a forward-biased junction.

A small-signal equivalent model for a forward-biased diode is shown in Fig. 1.4. A resistor, $r_{d}$, models the change in the diode voltage, $\mathrm{V}_{\mathrm{D}}$, that occurs when $I_{D}$ changes. Using (1.43), we have

$$
\begin{equation*}
\frac{1}{r_{d}}=\frac{d I_{D}}{d V_{D}}=I_{S} \frac{e^{V_{D} / V_{T}}}{V_{T}}=\frac{I_{D}}{V_{T}} \tag{1.47}
\end{equation*}
$$

This resistance is called the incremental resistance of the diode. For very accurate modelling, it is sometimes necessary to add the series resistance due to the bulk and also the resistance associated with the contacts. Typical values for the contact resistance (caused by the workfunction ${ }^{3}$ difference between metal and silicon) might be $20 \Omega$ to $40 \Omega$.

By combining (1.45) and (1.47), we see that an alternative equation for the diffusion capacitance, $\mathrm{C}_{\mathrm{d}}$, is

$$
\begin{equation*}
\mathrm{C}_{\mathrm{d}}=\frac{\tau_{\mathrm{T}}}{\mathrm{r}_{\mathrm{d}}} \tag{1.48}
\end{equation*}
$$

Since for moderate forward-bias currents, $C_{d} \gg C_{j}$, the total small-signal capacitance is $C_{T} \cong C_{d}$, and

$$
\begin{equation*}
r_{d} C_{T} \cong \tau_{T} \tag{1.49}
\end{equation*}
$$

Thus, for charging or discharging a forward-biased junction with a current source having an impedance much larger than $r_{d}$, the time constant of the charging is approximately equal to the transit time of the diode and is independent of the diode current. For smaller diode currents, where $\mathrm{C}_{\mathrm{j}}$ becomes important, the charging or discharging time constant of the circuit becomes larger than $\tau_{\mathrm{T}}$.

#### EXAMPLE 1.7

A given diode has a transit time of 100 ps and is biased at 1 mA . What are the values of its small-signal resistance and diffusion capacitance? Assume room temperature, so that $V_{T}=k T / q=26 \mathrm{mV}$.
3. The work-function of a material is defined as the minimum energy required to remove an electron at the Fermi level to the outside vacuum region.

#### Solution

We have

$$
\mathrm{r}_{\mathrm{d}}=\frac{\mathrm{V}_{\mathrm{T}}}{\mathrm{I}_{\mathrm{D}}}=\frac{26 \mathrm{mV}}{1 \mathrm{~mA}}=26 \Omega
$$

and

$$
\mathrm{C}_{\mathrm{d}}=\frac{\tau_{\mathrm{T}}}{\mathrm{r}_{\mathrm{d}}}=\frac{100 \mathrm{ps}}{26 \Omega}=3.8 \mathrm{pF}
$$

Note that this diffusion capacitance is over 100 times larger than the total depletion capacitance found in Examples 1.4 and 1.5 .

### 1.1.8 Schottky Diodes

A different type of diode, one sometimes used in microcircuit design, is realized by contacting metal to a lightly doped semiconductor region (rather than a heavily doped region) as shown in Fig. 1.5. Notice that the aluminum anode is in direct contact with a relatively lightly doped $\mathrm{n}^{-}$region. Because the $\mathrm{n}^{-}$region is relatively lightly doped, the work-function difference between the aluminum contact and the $\mathrm{n}^{-}$silicon is larger than would be the case for aluminum contacting to an $\mathrm{n}^{+}$region, as occurs at the cathode. This causes a depletion region and, correspondingly, a diode to occur at the interface between the aluminum anode and the $\mathrm{n}^{-}$silicon region. This diode has different characteristics than a normal pn junction diode. First, its voltage drop when forward biased is smaller. This voltage drop is dependent on the metal used; for aluminum it might be around 0.5 V . More importantly, when the diode is forward biased, there is no minority-charge storage in the lightly doped $\mathrm{n}^{-}$region. Thus, the small-signal model of a forward-biased Schottky diode has $\mathrm{C}_{\mathrm{d}}=0$ (with reference to Fig. 1.4). The absence of this diffusion capacitance makes the diode much faster. It is particularly faster when turning off, because it is not necessary to remove the minority charge first. Rather, it is only necessary to discharge the depletion capacitance through about 0.2 V .

Schottky diodes have been used extensively in bipolar logic circuits. They are also used in a number of highspeed analog circuits, particularly those realized in gallium arsenide (GaAs) technologies, rather than silicon technologies.
image_name:Fig. 1.5 A cross section of a Schottky diode.
description:The image is a cross-sectional diagram of a Schottky diode, illustrating its structure and components.

1. **Identification of Components and Structure:**
- The diagram shows a layered structure with an anode and a cathode labeled at the top.
- The anode is connected to a metal layer, identified as aluminum (Al), which forms a junction with the semiconductor material.
- Below the metal layer, there is a region labeled as the 'Schottky diode depletion region,' which is part of the semiconductor substrate.
- The substrate is divided into different regions, marked as n⁻ and p⁻, with a bulk region labeled below.
- The cathode is connected to another metal layer on the opposite side of the structure.

2. **Connections and Interactions:**
- The Schottky diode is formed by the junction between the metal (Al) and the n-type semiconductor region.
- The depletion region is where the Schottky barrier is formed, allowing the diode to conduct current in one direction.
- The diagram indicates the flow of current from the anode to the cathode through the depletion region.

3. **Labels, Annotations, and Key Features:**
- The diagram includes labels such as SiO₂, indicating the presence of an insulating layer, and Al for the metal contact.
- An equivalent circuit symbol for the Schottky diode is shown to the right, with the anode and cathode labeled, and a diode symbol indicating the direction of conventional current flow.
- Arrows indicate the direction of current flow and the boundaries of the depletion region.

Overall, the diagram provides a detailed view of the physical structure and function of a Schottky diode, highlighting the key components and their interactions.
image_name:Schottky diode symbol
description:
[
name: D1, type: Diode, ports: {Na: Anode, Nc: Cathode}
]
extrainfo:The diagram shows a cross-section and symbol of a Schottky diode. The Schottky diode is made using a metal-semiconductor junction, typically involving materials like aluminum and silicon. It features a depletion region and is known for its fast switching speed due to the absence of minority charge carriers.

Fig. 1.5 A cross section of a Schottky diode.

## 1.2 MOS TRANSISTORS

Presently, the most popular technology for realizing microcircuits makes use of MOS transistors. Unlike most bipolar junction transistor (BJT) technologies, which make dominant use of only one type of transistor (npn transistors in the case of BJT processes ${ }^{4}$ ), MOS circuits normally use two complementary types of transistors-n-channel and p -channel. While n -channel devices conduct with a positive gate voltage, p -channel devices conduct with a negative gate voltage. Moreover, electrons are used to conduct current in n -channel transistors, while holes are used in p-channel transistors. Microcircuits containing both n-channel and p-channel transistors are called CMOS circuits, for complementary MOS. The acronym MOS stands for metal-oxide semiconductor, which historically denoted the gate, insulator, and channel region materials, respectively. However, most present CMOS technologies utilize polysilicon gates rather than metal gates.

Before CMOS technology became widely available, most MOS processes made use of only n-channel transistors (NMOS). However, often two different types of $n$-channel transistors could be realized. One type, enhancement n-channel transistors, is similar to the n-channel transistors realized in CMOS technologies. Enhancement transistors require a positive gate-to-source voltage to conduct current. The other type, depletion transistors, conduct current with a gate-source voltage of 0 V . Depletion transistors were used to create highimpedance loads in NMOS logic gates.

Key Point: The source terminal of an $n$-channel transistor is defined as whichever of the two terminals has a lower voltage. For a p-channel transistor, the source would be the terminal with the higher voltage.

A typical cross section of an n-channel enhancement-type MOS transistor is shown in Fig. 1.6. With no voltage applied to the gate, the $\mathrm{n}^{+}$source and drain regions are separated by the $\mathrm{p}^{-}$substrate. The distance between the drain and the source is called the channel length, L . In present MOS technologies, the minimum channel length may be as small as 28 nm . It should be noted that there is no physical difference between the drain and the source. ${ }^{5}$ The source terminal of an n-channel transistor is defined as whichever of the two terminals has a lower voltage. For a p-channel transistor, the source would be the terminal with the higher voltage. When a transistor is turned on, current flows from the drain to the source in an n-channel transistor and from the source to the drain in a p-channel transistor. In both cases, the true carriers travel from the source to drain, but the current directions are different because n -channel carriers (electrons) are negative, whereas p -channel carriers (holes) are positive.
image_name:Fig. 1.6 A cross section of a typical n-channel transistor.
description:The image is a cross-sectional diagram of a typical n-channel MOSFET (Metal-Oxide-Semiconductor Field-Effect Transistor). This transistor is structured with several key components and layers:

1. **Source and Drain:**
- The diagram shows two heavily doped n+ regions labeled as the source and drain. These are positioned on either side of the transistor and are responsible for the flow of electrons when the transistor is in operation.

2. **Gate:**
- A polysilicon gate is situated above the channel region, separated by a thin insulating layer of silicon dioxide (SiO2). The gate controls the flow of electrons between the source and drain by creating an electric field when a voltage is applied.

3. **Substrate:**
- The bulk or substrate is labeled as p-type, indicating that it is doped with positive carriers (holes). This forms the body of the transistor and provides a contrast to the n+ source and drain regions.

4. **Insulating Layer:**
- The SiO2 layer acts as an insulator between the gate and the channel. This is crucial for the MOSFET's operation as it allows the gate to control the channel without direct electrical contact.

5. **Metal Contacts:**
- Metal (Aluminum, Al) contacts are shown connecting to the source, gate, and drain, facilitating external electrical connections.

6. **Current Flow:**
- The diagram includes arrows indicating the direction of electron flow from the source to the drain when the transistor is activated.

This structure allows the n-channel MOSFET to function as a switch or amplifier in electronic circuits, with the gate voltage controlling the conductivity of the channel between the source and drain.

Fig. 1.6 A cross section of a typical n-channel transistor.
4. Most BJT technologies can also realize low-speed lateral pnp transistors. Normally these would only be used to realize current sources as they have low gains and poor frequency responses. Recently, bipolar technologies utilizing high-speed vertical pnp transistors, as well as high-speed npn transistors, have become available and are growing in popularity. These technologies are called complementary bipolar technologies.
5. Large MOS transistors used for power applications are an exception as they might not be realized with symmetric drain and source junctions.

The gate is normally realized using polysilicon, which is heavily doped noncrystalline (or amorphous) silicon. Polysilicon gates are used (instead of metal) because polysilicon has allowed the dimensions of the transistor to be realized much more accurately during the patterning of the transistor. This higher geometric accuracy has resulted in smaller, faster transistors. However, due to the relatively higher resistance of polysilicon, there are continuous efforts to realize metal gates in CMOS fabrication technologies.

The gate is physically separated from the surface of the silicon by a thin insulator made of silicon dioxide $\left(\mathrm{SiO}_{2}\right)$. Thus, the gate is electrically isolated from the channel and affects the channel (and hence, the transistor current) only through electrostatic (capacitive) coupling. The typical thickness of the $\mathrm{SiO}_{2}$ insulator between the gate and the channel is presently between 1 to 30 nm . Since the gate is electrically isolated from the channel, it does not conduct appreciable dc current. However, because of the inherent capacitances in MOS transistors, transient gate currents do exist when gate voltage is quickly changing.

Normally the $\mathrm{p}^{-}$substrate (or bulk) is connected to the most negative voltage in a microcircuit. In analog circuits, this might be the negative power supply, and in digital circuits it is normally ground or 0 V . This connection results in all transistors placed in the substrate being surrounded by reverse-biased junctions, which electrically isolate the transistors and thereby prevent conduction between the transistor terminals and the substrate (unless, of course, they are connected together through some other means).

### 1.2.1 Symbols for MOS Transistors

Many symbols have been used to represent MOS transistors. Figure 1.7 shows some of the symbols that have been used to represent n-channel MOS transistors. The symbol in Fig. 1.7(a) is often used; note that there is nothing in the symbol to specify whether the transistor is n -channel or p -channel. A common rule is to assume, when in doubt, that the transistor is an n -channel transistor. The symbol in Fig. 1.7(a) will be used occasionally in this text when there is no need to distinguish between the drain and source terminals. Figure $1.7(b)$ is the most commonly used symbol for an n -channel transistor in analog design and is used most often throughout this text. An arrow points outward on the source terminal to indicate that the transistor is n -channel and indicates the direction of current.

MOS transistors are actually four-terminal devices, with the substrate being the fourth terminal. In n -channel devices, the $\mathrm{p}^{-}$substrate is normally connected to the most negative voltage in the microcircuit, whereas for p -channel devices, the $\mathrm{n}^{-}$substrate is normally connected to the most positive voltage. In these cases the substrate connection is normally not shown in the symbol. However, for CMOS technologies, at least one of the two types of transistors will be formed in a well substrate that need not be connected to one of the power supply nodes. For example, an $n$-well process would form $n$-channel transistors in a $\mathrm{p}^{-}$substrate encompassing the entire microcircuit, while the p -channel transistors would be formed in many separate $n$-well substrates. In this case, most of the n-well substrates would be connected to the most positive power supply, while some might be connected to other nodes in the circuit (often the well is connected to the source of a transistor that is not connected to the power supply). In these cases, the symbol shown in Fig. 1.7(c) can be used to show the substrate connection explicitly. Note that the arrow points from the p substrate region to the n -channel region, just like the arrow in the diode symbol which points from the p anode to the n cathode region. It should be noted that this case is not encountered often in digital circuits and is more common in analog circuits. Sometimes, in the interest of simplicity, the isolation of the gate is not explicitly shown, as is the case of the symbol of Fig. 1.7(d). This simple notation is more common for
image_name:(a)
description:
[
name: (a), type: NMOS, ports: {S: s, D: d, G: g}
]
extrainfo:The diagram shows a simple NMOS transistor with three ports: source (s), drain (d), and gate (g). The body connection is not shown explicitly.}
image_name:(b)
description:
[
name: (b), type: PMOS, ports: {S: s, D: d, G: g}
]
extrainfo:The diagram shows commonly used symbols for n-channel and p-channel transistors. The device (b) is a PMOS transistor with source (s), drain (d), and gate (g) terminals.
image_name:(c)
description:
[
name: M1, type: PMOS, ports: {S: s, D: d, G: g, B: b}
]
extrainfo:The diagram shows a PMOS transistor with labeled ports: source (s), drain (d), gate (g), and body (b). This is a common symbol used to represent PMOS transistors.}
image_name:(d)
description:
[
name: M1, type: NMOS, ports: {S: s, D: d, G: g}
]
extrainfo:The diagram represents a commonly used symbol for an NMOS transistor, showing the gate (g), source (s), and drain (d) connections.
image_name:(e)
description:
[
name: (e), type: NMOS, ports: {S: s, D: d, G: g}
]
extrainfo:The diagram shows commonly used symbols for n-channel transistors. Diagram (e) represents an NMOS transistor with its source (s), drain (d), and gate (g) labeled.

Fig. 1.7 Commonly used symbols for n-channel transistors.

### 1.2.2 Basic Operation

The basic operation of MOS transistors will be described with respect to an n -channel transistor. First, consider the simplified cross sections shown in Fig. 1.9, where the source, drain, and substrate are all connected to ground. In this case, the MOS transistor operation is similar to a capacitor. The gate acts as one plate of the capacitor, and the surface of the silicon, just under the thin insulating $\mathrm{SiO}_{2}$, acts as the other plate.

If the gate voltage is very negative, as shown in Fig. 1.9(a), positive charge will be attracted to the channel region. Since the substrate was originally doped $\mathrm{p}^{-}$, this negative gate voltage has the effect of simply increasing the channel doping to $\mathrm{p}^{+}$, resulting in what is called an accumulated channel. The $\mathrm{n}^{+}$source and drain regions are separated from the $\mathrm{p}^{+}$-channel region by depletion regions, resulting in the equivalent circuit of two back-to-back diodes. Thus, only leakage current will flow even if one of the source or drain voltages becomes large (unless the drain voltage becomes so large as to cause the transistor to break down).

In the case of a positive voltage being applied to the gate, the opposite situation occurs, as shown in Fig. $1.9(b)$. For small positive gate voltages, the positive carriers in the channel under the gate are initially repulsed and the channel changes from a $\mathrm{p}^{-}$doping level to a depletion region. As a more positive gate voltage is applied, the gate attracts negative charge from the source and drain regions, and the channel becomes an n region with mobile electrons connecting the drain and source regions. ${ }^{6}$ In short, a sufficiently large positive gate-source voltage changes the channel beneath the gate to an n region, and the channel is said to be inverted.

The gate-source voltage, for which the concentration of electrons under the gate is equal to the concentration of holes in the $\mathrm{p}^{-}$substrate far from the gate, is commonly referred to as the transistor threshold voltage and denoted $\mathrm{V}_{\mathrm{tn}}$ (for n -channel transistors). For gate-source voltages larger than $\mathrm{V}_{\mathrm{tn}}$, there is an n -type channel present, and conduction between the drain and the source can occur. For gate-source voltages less than $\mathrm{V}_{\mathrm{tn}}$, it is normally assumed that the transistor is off and no current flows between the drain and the source. However, it should be noted that this assumption of zero drain-source current for a transistor that is

[^1]is not synonymous with our previous use, in which it designated a pn interface of a diode.
image_name:(a)
description:The image consists of two diagrams labeled (a) and (b), depicting the operation of an n-channel MOS transistor under different gate voltage conditions.

**Diagram (a):**
- **Components and Structure:** The diagram shows a cross-section of an n-channel MOS transistor. It includes a source and a drain, both labeled as n+ regions, indicating heavily doped n-type semiconductor material. These regions are connected to ground. The area between the source and drain is a p- substrate, indicating a lightly doped p-type semiconductor. Above the substrate, there is a layer of SiO2, which acts as an insulating layer.
- **Connections and Interactions:** The gate voltage (V_G) is shown as being much less than zero (V_G << 0). This negative gate voltage causes an accumulation of holes at the SiO2 interface, forming an accumulation region. This setup prevents the formation of an n-type channel, thus no current flows between the drain and the source.
- **Labels, Annotations, and Key Features:** The diagram labels the depletion region formed around the n+ source and drain areas, and the accumulation region where holes gather due to the negative gate voltage. The substrate is labeled as p-.

**Diagram (b):**
- **Components and Structure:** Similar to diagram (a), this cross-section also includes the source and drain as n+ regions, a p- substrate, and a SiO2 layer.
- **Connections and Interactions:** Here, the gate voltage (V_G) is shown as being much greater than zero (V_G >> 0). This positive gate voltage attracts electrons to the interface between the SiO2 and the p- substrate, forming an n-type channel. This channel allows current to flow from the drain to the source.
- **Labels, Annotations, and Key Features:** The diagram highlights the depletion region around the n+ source and drain, and the newly formed channel that enables conduction due to the positive gate voltage. The substrate remains labeled as p-.
image_name:(b)
description:The image consists of two diagrams labeled (a) and (b), depicting the cross-section of an n-channel MOS transistor under different gate voltage conditions.

**Diagram (b):**
1. **Identification of Components and Structure:**
- The diagram shows an n-channel MOS transistor.
- It includes a source and a drain, both connected to n+ regions.
- A p-type substrate is present, labeled as "p- substrate."
- A layer of silicon dioxide (SiO2) is depicted above the substrate, acting as an insulator.
- The gate is positioned above the SiO2 layer.

2. **Connections and Interactions:**
- The source and drain are connected to n+ regions, which are heavily doped to facilitate electron flow.
- The diagram indicates that the gate voltage (V_G) is much greater than 0 (V_G >> 0).
- Under this condition, an n-type channel is formed between the source and drain, allowing current to flow.
- The channel is depicted as a continuous path, indicating conduction is possible.

3. **Labels, Annotations, and Key Features:**
- The diagram is labeled with V_G >> 0, indicating a positive gate voltage.
- The depletion region is shown around the n+ source and drain regions.
- The formation of the channel is marked, showing the presence of mobile electrons enabling conduction.
- The presence of positive charges on the gate and negative charges in the channel is indicated, showing the electrostatic interaction that facilitates channel formation.

Fig. 1.9 An n-channel MOS transistor. (a) $\mathrm{V}_{\mathrm{G}} \ll 0$, resulting in an accumulated channel (no current flow); (b) $\mathrm{V}_{\mathrm{G}}>>0$, and the channel is present (current flow possible from drain to source).
off is only an approximation. In fact, for gate voltages around $\mathrm{V}_{\mathrm{tn}}$, there is no abrupt current change, and for gate-source voltages slightly less than $\mathrm{V}_{\mathrm{tn}}$, small amounts of subthreshold current can flow, as discussed in Section 1.4.1.

When the gate-source voltage, $\mathrm{V}_{\mathrm{GS}}$, is larger than $\mathrm{V}_{\mathrm{tn}}$, the channel is present. As $\mathrm{V}_{\mathrm{Gs}}$ is increased, the density of electrons in the channel increases. Indeed, the carrier density, and therefore the charge density, is proportional to $\mathrm{V}_{\mathrm{Gs}}-\mathrm{V}_{\mathrm{t} \mathrm{n}}$, which is often called the effective gate-source voltage and denoted $\mathrm{V}_{\text {eff }}$. Specifically, define

$$
\begin{equation*}
\mathrm{V}_{\mathrm{eff}} \equiv \mathrm{~V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{tn}} \tag{1.50}
\end{equation*}
$$

The charge density of electrons is then given by

$$
\begin{equation*}
Q_{n}=C_{o x}\left(V_{G S}-V_{\mathrm{tn}}\right)=C_{o x} V_{\text {eff }} \tag{1.51}
\end{equation*}
$$

Here, $C_{0 x}$ is the gate capacitance per unit area and is given by

$$
\begin{equation*}
\mathrm{C}_{\mathrm{ox}}=\frac{\mathrm{K}_{\mathrm{ox}} \varepsilon_{0}}{\mathrm{t}_{\mathrm{ox}}} \tag{1.52}
\end{equation*}
$$

where $\mathrm{K}_{\mathrm{ox}}$ is the relative permittivity of $\mathrm{SiO}_{2}$ (approximately 3.9) and $\mathrm{t}_{\mathrm{ox}}$ is the thickness of the thin oxide under the gate. A point to note here is that (1.51) is only accurate when both the drain and the source voltages are zero.

To obtain the total gate capacitance, (1.52) should be multiplied by the effective gate area, WL, where W is the gate width and L is the effective gate length. These dimensions are shown in Fig. 1.10. Thus the total gate capacitance, $\mathrm{C}_{\mathrm{g}}$, is given by

$$
\begin{equation*}
C_{g}=W L C_{o x} \tag{1.53}
\end{equation*}
$$

and the total charge of the channel, $Q_{T-n}$, is given by

$$
\begin{equation*}
Q_{T-n}=W L C_{o x}\left(V_{G S}-V_{t n}\right)=W L C_{o x} V_{\text {eff }} \tag{1.54}
\end{equation*}
$$

The gate capacitance is one of the major load capacitances that circuits must be capable of driving. Gate capacitances are also important when one is calculating charge injection, which occurs when a MOS transistor is being turned off because the channel charge, $Q_{T-n}$, must flow from under the gate out through the terminals to other places in the circuit.

Next, if the drain voltage is increased above 0 V , a drain-source potential difference exists. This difference results in current flowing from the drain to the source. ${ }^{7}$ The relationship between $\mathrm{V}_{\mathrm{DS}}$ and the drain-source current, $I_{D}$, is the same as for a resistor, assuming $V_{D S}$ is small. This relationship is given [Sze, 1981] by

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D}}=\mu_{\mathrm{n}} \mathrm{Q}_{\mathrm{n}} \frac{\mathrm{~W}}{\mathrm{~L}} \mathrm{~V}_{\mathrm{DS}} \tag{1.55}
\end{equation*}
$$

where $\mu_{n}$ is the mobility of electrons near the silicon surface, and $Q_{n}$ is the charge concentration of the channel per unit area (looking from the top down). Electron mobility is $0.14 \mathrm{~m}^{2} / \mathrm{Vs}$ in pure intrinsic silicon, decreasing with increasing dopant concentrations to $\mu_{n} \cong 0.01-0.06 \mathrm{~m}^{2} / \mathrm{Vs}$ in modern NMOS devices. Note that as the channel length increases, the drain-source current decreases, whereas this current increases as either the charge density or the transistor width increases. Using (1.54) and (1.55) results in

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D}}=\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}} \frac{\mathrm{~W}}{\mathrm{~L}}\left(\mathrm{~V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{tn}}\right) \mathrm{V}_{\mathrm{DS}}=\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}} \frac{\mathrm{~W}}{\mathrm{~L}} \mathrm{~V}_{\mathrm{eff}} \mathrm{~V}_{\mathrm{DS}} \tag{1.56}
\end{equation*}
$$

where it should be emphasized that this relationship is only valid for drain-source voltages near zero (i.e., $\mathrm{V}_{\mathrm{DS}}$ much smaller than $\mathrm{V}_{\text {eff }}$ ).
image_name:Fig. 1.10
description:The diagram in Fig. 1.10 illustrates a cross-sectional view of a MOS (Metal-Oxide-Semiconductor) transistor, highlighting its important dimensions and components. The primary elements visible in the diagram include:

1. **Gate**: Positioned at the top, the gate is depicted as a rectangular block. It controls the flow of current between the source and drain by modulating the electric field.

2. **SiO2 Layer**: Beneath the gate, a thin layer of silicon dioxide (SiO2) acts as an insulating layer, preventing direct electrical contact between the gate and the underlying semiconductor.

3. **n+ Regions**: On either side of the gate, there are heavily doped n+ regions. These represent the source and drain of the transistor, where the current enters and exits.

4. **n Channel**: The channel is formed between the n+ regions when a voltage is applied to the gate. It is the path through which electrons flow from source to drain.

5. **Dimensions L and W**: The diagram indicates the length (L) and width (W) of the channel. These dimensions are crucial for determining the electrical characteristics of the MOS transistor.

6. **t_ox**: This refers to the thickness of the oxide layer (SiO2) beneath the gate.

7. **Current Flow**: The diagram suggests the direction of current flow from the source to the drain, facilitated by the gate's control of the channel.

Overall, this diagram serves as a schematic representation of a MOS transistor, emphasizing the spatial arrangement and interaction of its key components.

Fig. 1.10 The important dimensions of a MOS transistor.

[^2]from source to drain results in a positive current from drain to source, $\mathrm{I}_{\mathrm{DS}}$.
image_name:Fig. 1.10
description:The diagram represents a schematic of a MOS transistor, focusing on the channel charge density as the drain-source voltage (V_D) increases. It illustrates the depletion region, the gate voltage (V_G), and the source voltage (V_S), emphasizing the charge density Q_n(x) at various points along the channel. The diagram shows the relationship between the gate-source voltage (V_GS), channel voltage (V_ch), and threshold voltage (V_tn).

Fig. 1.11 The channel charge density for $\mathrm{V}_{\mathrm{DS}}>0$.

As the drain-source voltage increases, the channel charge concentration decreases at the drain end. This decrease is due to the smaller gate-to-channel voltage difference across the thin gate oxide as one moves closer to the drain. In other words, since the drain voltage is assumed to be at a higher voltage than the source, there is an increasing voltage gradient from the source to the drain, resulting in a smaller gate-to-channel voltage near the drain. Since the charge density at a distance $x$ from the source end of the channel is proportional to $\mathrm{V}_{\mathrm{G}}-\mathrm{V}_{\mathrm{ch}}(\mathrm{x})-\mathrm{V}_{\mathrm{tn}}$, as $\mathrm{V}_{\mathrm{G}}-\mathrm{V}_{\mathrm{ch}}(\mathrm{x})$ decreases, the charge density also decreases. ${ }^{8}$ This

Key Point: The relationship between drainsource voltage and drain current of a MOS device is approximately linear when $\mathrm{V}_{\mathrm{DS}} \ll \mathrm{V}_{\text {eff }}$.
effect is illustrated in Fig. 1.11.

Note that at the drain end of the channel, we have

$$
\begin{equation*}
V_{G}-V_{c h}(L)=V_{G D} \tag{1.57}
\end{equation*}
$$

For small $V_{D S}$, we saw from (1.56) that $I_{D}$ was linearly related to $\mathrm{V}_{\mathrm{DS}}$. However, as $\mathrm{V}_{\mathrm{DS}}$ increases, and the charge density decreases near the drain, the relationship becomes nonlinear. In fact, the linear relationship for $I_{D}$ versus $V_{D S}$ flattens for larger $\mathrm{V}_{\mathrm{DS}}$, as shown in Fig. 1.12.

As the drain voltage is increased, at some point the gate-tochannel voltage at the drain end will decrease to the threshold value $\mathrm{V}_{\mathrm{tn}}$ - the minimum gate-to-channel voltage needed for n carriers in the channel to exist. Thus, at the drain end, the channel becomes pinched off, as shown in Fig. 1.13. This pinch-off occurs at $\mathrm{V}_{\mathrm{GD}}=\mathrm{V}_{\mathrm{tn}}$, since the channel voltage at the drain end is simply equal to $V_{D}$. Thus, pinch-off occurs for

$$
\begin{equation*}
V_{D G}>-V_{t n} \tag{1.58}
\end{equation*}
$$

Denoting $\mathrm{V}_{\mathrm{DS} \text {-sat }}$ as the drain-source voltage when the channel becomes pinched off, we can substitute $V_{D G}=V_{D S}-V_{G S}$ into
image_name:Fig. 1.12
description:The graph in Fig. 1.12 is a plot of the drain current \( I_D \) versus the drain-source voltage \( V_{DS} \) for a MOSFET. The graph is a typical characteristic curve used to analyze the behavior of MOSFETs in electronics.

1. **Type of Graph and Function:**
- This is a characteristic curve for a MOSFET, showing the relationship between the drain current \( I_D \) and the drain-source voltage \( V_{DS} \).

2. **Axes Labels and Units:**
- The vertical axis represents the drain current \( I_D \), typically measured in amperes (A).
- The horizontal axis represents the drain-source voltage \( V_{DS} \), typically measured in volts (V).
- The axes are linear without specified units in the image, but standard practice assumes amperes and volts respectively.

3. **Overall Behavior and Trends:**
- The graph shows an initial linear increase in \( I_D \) as \( V_{DS} \) increases, indicating ohmic or linear region behavior.
- As \( V_{DS} \) continues to increase, the curve bends upwards, indicating the onset of saturation where the current becomes less dependent on \( V_{DS} \).

4. **Key Features and Technical Details:**
- The linear region is defined by the equation \( I_D = \mu_n C_{ox} \frac{W}{L} (V_{GS} - V_{tn}) V_{DS} \), where \( \mu_n \) is the mobility of electrons, \( C_{ox} \) is the oxide capacitance per unit area, \( W \) is the width of the channel, \( L \) is the length of the channel, \( V_{GS} \) is the gate-source voltage, and \( V_{tn} \) is the threshold voltage.
- The curve transitions from the linear region to the saturation region, where \( I_D < \mu_n C_{ox} \frac{W}{L} (V_{GS} - V_{tn}) V_{DS} \).
- The transition point marks the beginning of the saturation region where the channel is pinched off.

5. **Annotations and Specific Data Points:**
- The graph includes annotations of the equations governing the linear and saturation regions.
- There are no specific numerical values or markers provided, but the equations are key to understanding the behavior of the MOSFET in different regions.

Fig. 1.12 For $V_{D S}$ not close to zero, the $I_{D}$ versus $V_{D S}$ relationship is no longer linear.
(1.58) and find an equivalent pinch-off expression

$$
\begin{equation*}
V_{D S}>V_{D S-s a t} \tag{1.59}
\end{equation*}
$$

[^3]since the gate material is highly conductive.
image_name:Fig. 1.13
description:The image depicts a cross-sectional view of a MOSFET (Metal-Oxide-Semiconductor Field-Effect Transistor) in the saturation region. It illustrates the behavior of the transistor when the drain-source voltage ($V_{DS}$) is increased such that the gate-drain voltage ($V_{GD}$) becomes less than the threshold voltage ($V_{tn}$), leading to pinch-off at the drain end.

#### Identification of Components and Structure:
- **Gate (G):** The gate is shown as a horizontal bar above the channel. It is connected to a voltage source, indicating $V_G >> V_{tn}$, suggesting that the gate voltage is significantly greater than the threshold voltage, which allows for channel formation.
- **Source (S):** The source is labeled with $V_S = 0$, indicating it is grounded.
- **Drain (D):** The drain is on the opposite side of the channel from the source. The voltage at the drain is represented as $V_{DG}$, which is greater than $-V_{tn}$.
- **Channel Region:** The channel is formed between the source and drain beneath the gate. It is indicated by a dashed line, showing the path of current flow.
- **Depletion Regions:** These are shaded areas on either side of the channel, indicating regions where mobile charge carriers are depleted.

#### Connections and Interactions:
- **Pinch-off Region:** The diagram shows a pinch-off point near the drain end where the channel narrows, illustrating the condition $V_{GD} < V_{tn}$. This indicates that the channel is pinched off at the drain, limiting the current.
- **Current Flow:** The current flows from the source to the drain through the channel when the gate voltage is applied.

#### Labels, Annotations, and Key Features:
- **Depletion Region:** Labeled on the source side, indicating the extent of the depletion region due to the applied gate voltage.
- **Pinch-off Condition:** Annotated with an arrow pointing to the pinch-off region, explaining the condition $V_{GD} < V_{tn}$.
- **Electrical Annotations:** Voltage levels are indicated ($V_S = 0$, $V_G >> V_{tn}$, $V_{DG} > -V_{tn}$), which are crucial for understanding the operational state of the MOSFET in this diagram.

Fig. 1.13 When $\mathrm{V}_{\mathrm{DS}}$ is increased so that $\mathrm{V}_{\mathrm{GD}}<\mathrm{V}_{\mathrm{tn}}$, the channel becomes pinched off at the drain end.
where $\mathrm{V}_{\mathrm{DS} \text {-sat }}$ is given ${ }^{9}$ by

$$
\begin{equation*}
V_{D S-s a t}=V_{G S}-V_{t n}=V_{\text {eff }} \tag{1.60}
\end{equation*}
$$

The current travelling through the pinched-off channel region is saturated, similar to a gas under pressure travelling through a very small tube. If the drain-gate voltage rises above this critical pinch-off voltage of $-\mathrm{V}_{\mathrm{tn}}$, the charge concentration in the channel remains constant (to a first-order approximation) and the drain current no longer increases with increasing $\mathrm{V}_{\mathrm{DS}}$. The result is the current-voltage relationship shown in Fig. 1.14 for a given gate-source voltage. In the region of operation where $\mathrm{V}_{\mathrm{DS}}>\mathrm{V}_{\mathrm{DS} \text {-sat }}$, the drain current is independent of $\mathrm{V}_{\mathrm{DS}}$ and is called the active region. ${ }^{10}$ The region where $\mathrm{I}_{\mathrm{D}}$ changes linearly with $\mathrm{V}_{\mathrm{DS}}$ is called the triode region. When MOS transistors are used in analog amplifiers, they almost always are biased in the active region. When they are used in digital logic gates, they often operate in both regions.

It is sometimes necessary to distinguish between transistors in weak, moderate, and strong inversion. As just discussed, a gate-source voltage greater than $\mathrm{V}_{\mathrm{tn}}$ results in an inverted channel, and drain-source current can flow. However, as the gate-source voltage is increased, the channel does not become inverted (i.e., n-region) suddenly,

$$
\mathrm{I}_{\mathrm{D}}=\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}} \frac{\mathrm{~W}}{\mathrm{~L}}\left[\left(\mathrm{~V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{tn}}\right) \mathrm{V}_{\mathrm{DS}}-\frac{\mathrm{V}_{\mathrm{DS}}^{2}}{2}\right] \text { : }
$$

[^4]but rather gradually. Thus, it is useful to define three regions of channel inversion with respect to the gate-source voltage. In most circuit applications, noncutoff MOSFET transistors are operated in strong inversion, with $\mathrm{V}_{\text {eff }}>100 \mathrm{mV}$ (many prudent circuit designers use a minimum value of 200 mV ). As the name suggests, strong inversion occurs when the channel is strongly inverted. It should be noted that all the equation models in this section assume strong inversion operation. Weak inversion occurs when $\mathrm{V}_{\mathrm{GS}}$ is approximately 100 mV or more below $\mathrm{V}_{\mathrm{tn}}$ and is discussed as subthreshold operation in Section 1.4.1. Finally, moderate inversion is the region between weak and strong inversion.

### 1.2.3 Large-Signal Modelling

The triode region equation for a MOS transistor relates the drain current to the gate-source and drain-source voltages. It can be shown (see Appendix) that this relationship is given by

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D}}=\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)\left[\left(\mathrm{V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{tn}}\right) \mathrm{V}_{\mathrm{DS}}-\frac{\mathrm{V}_{\mathrm{DS}}^{2}}{2}\right] \tag{1.61}
\end{equation*}
$$

As $V_{D S}$ increases, $I_{D}$ increases until the drain end of the channel becomes pinched off, and then $I_{D}$ no longer increases. This pinch-off occurs for $\mathrm{V}_{\mathrm{DG}}=-\mathrm{V}_{\mathrm{tn}}$, or approximately,

$$
\begin{equation*}
V_{D S}=V_{G S}-V_{t n}=V_{\text {eff }} \tag{1.62}
\end{equation*}
$$

Right at the edge of pinch-off, the drain current resulting from (1.61) and the drain current in the active region (which, to a first-order approximation, is constant with respect to $\mathrm{V}_{\mathrm{DS}}$ ) must have the same value. Therefore, the active region equation can be found by substituting (1.62) into (1.61), resulting in

$$
\begin{equation*}
I_{D}=\frac{\mu_{\mathrm{n}} C_{o x}}{2}\left(\frac{W}{L}\right)\left(V_{G S}-V_{t n}\right)^{2} \tag{1.63}
\end{equation*}
$$

For $\mathrm{V}_{\mathrm{DS}}>\mathrm{V}_{\text {eff }}$, the current stays constant at the value given by (1.63), ignoring second-order effects such as channel-length modulation. This equation is perhaps the most important one that describes the large-signal operation of a MOS transistor. It should be noted here that (1.63) represents a square-law current-voltage relationship for a MOS transistor in the active region. In the case of a BJT transistor, an exponential current-voltage relationship exists in the active region.

Key Point: For $\mathrm{V}_{\mathrm{DS}}>\mathrm{V}_{\mathrm{eff}}$, MOS device exhibits a square-law current-voltage relationship.

As just mentioned, (1.63) implies that the drain current, $I_{D}$, is independent of the drain-source voltage. This independence is only true to a first-order approximation. The major source of error is due to the channel length shrinking as $\mathrm{V}_{\mathrm{DS}}$ increases. To see this effect, consider Fig. 1.15, which shows a cross section of a transistor in the
image_name:Fig. 1.15
description:The diagram in Fig. 1.15 illustrates a cross-section of a MOSFET transistor in the active region, highlighting the phenomenon of channel length shortening for \( V_{\mathrm{DS}} > V_{\mathrm{eff}} \). The main components visible in the diagram include:

1. **Transistor Structure:**
- **Source (S):** Located on the left side, marked with \( V_{S} = 0 \), indicating it is grounded.
- **Drain (D):** Located on the right side, with a higher voltage \( V_{\mathrm{DS}} > V_{\mathrm{GS}} - V_{\mathrm{tn}} \).
- **Gate (G):** Positioned above the channel, with the condition \( V_{\mathrm{GS}} > V_{\mathrm{tn}} \) indicated.
- **Channel Region:** The area between the source and drain, where current \( I_{D} \) flows.

2. **Depletion and Pinch-off Regions:**
- **Depletion Region:** Shown on both sides, indicating areas with very low charge density.
- **Pinch-off Region:** Located near the drain, where the channel narrows significantly due to high \( V_{\mathrm{DS}} \).

3. **Current Flow and Channel Length:**
- The drain current \( I_{D} \) is depicted as flowing from the drain to the source, with an arrow indicating direction.
- The channel length \( L \) is marked, showing the effective length of the channel that changes due to the pinch-off effect.
- The change in channel length \( \Delta L \) is noted with a proportionality expression: \( \Delta L \propto \sqrt{V_{\mathrm{DS}} - V_{\mathrm{eff}} + \Phi_{0}} \), indicating the dependence of channel shortening on the drain-source voltage.

4. **Annotations and Labels:**
- Various voltages and conditions are labeled, such as \( V_{S} = 0 \), \( V_{\mathrm{GS}} > V_{\mathrm{tn}} \), and \( V_{\mathrm{DS}} > V_{\mathrm{GS}} - V_{\mathrm{tn}} \).
- The diagram emphasizes the physical changes in the transistor structure as \( V_{\mathrm{DS}} \) increases beyond \( V_{\mathrm{eff}} \), leading to the formation of the pinch-off region and the associated impact on channel length and current flow.

Fig. 1.15 Channel length shortening for $\mathrm{V}_{\mathrm{DS}}>\mathrm{V}_{\text {eff }}$.
active region. A pinched-off region with very little charge exists between the drain and the channel. The voltage at the end of the channel closest to the drain is fixed at $\mathrm{V}_{\mathrm{Gs}}-\mathrm{V}_{\mathrm{tn}}=\mathrm{V}_{\text {eff }}$. The voltage difference between the drain and the near end of the channel lies across a short depletion region often called the pinch-off region. As $\mathrm{V}_{\mathrm{DS}}$ becomes larger than $\mathrm{V}_{\text {eff }}$, this depletion region surrounding the drain junction increases its width in a square-root relationship with respect to $\mathrm{V}_{\mathrm{DS}}$. This increase in the width of the depletion region surrounding the drain junction decreases the effective channel length. In turn, this decrease in effective channel length increases the drain current, resulting in what is commonly referred to as channel-length modulation.

To derive an equation to account for channel-length modulation, we first make use of (1.11) and denote the width of the depletion region by $\mathrm{x}_{\mathrm{d}}$, resulting in

$$
\begin{align*}
\mathrm{x}_{\mathrm{d}} & \cong \mathrm{k}_{\mathrm{ds}} \sqrt{V_{\mathrm{D}-\mathrm{ch}}+\Phi_{0}}  \tag{1.64}\\
& =\mathrm{k}_{\mathrm{ds}} \sqrt{V_{\mathrm{DG}}+\mathrm{V}_{\mathrm{tn}}+\Phi_{0}}
\end{align*}
$$

where

$$
\begin{equation*}
\mathrm{k}_{\mathrm{ds}}=\sqrt{\frac{2 \mathrm{~K}_{\mathrm{s}} \varepsilon_{0}}{\mathrm{qN}}} \tag{1.65}
\end{equation*}
$$

and has units of $m / \sqrt{V}$. Note that $N_{A}$ is used here since the $n$-type drain region is more heavily doped than the p-type channel (i.e., $N_{D} \gg N_{A}$ ). By writing a Taylor approximation for $I_{D}$ around its operating value of $V_{D S}=V_{G S}-V_{t n}=V_{\text {eff }}$, we find $I_{D}$ to be given by

$$
\begin{equation*}
I_{D}=I_{D-s a t}+\left(\frac{\partial I_{D}}{\partial L}\right)\left(\frac{\partial L}{\partial V_{D S}}\right) \Delta V_{D S} \cong I_{D-s a t}\left(1+\frac{k_{d s}\left(V_{D S}-V_{\text {eff }}\right)}{2 L \sqrt{V_{D G}+V_{t n}+\Phi_{0}}}\right) \tag{1.66}
\end{equation*}
$$

where $I_{D \text {-sat }}$ is the drain current when $V_{D S}=V_{\text {eff }}$, or equivalently, the drain current when the channel-length modulation is ignored. Note that in deriving the final equation of (1.66), we have used the relationship $\partial \mathrm{L} / \partial \mathrm{V}_{\mathrm{DS}}=-\partial \mathrm{x}_{\mathrm{d}} / \partial \mathrm{V}_{\mathrm{DS}}$. Usually, (1.66) is written as

$$
\begin{equation*}
I_{D}=\frac{\mu_{n} C_{o x}}{2}\left(\frac{W}{L}\right)\left(V_{G S}-V_{t n}\right)^{2}\left[1+\lambda\left(V_{D S}-V_{\text {eff }}\right)\right] \tag{1.67}
\end{equation*}
$$

where $\lambda$ is the output impedance constant (in units of $\mathrm{V}^{-1}$ ) given by

$$
\begin{equation*}
\lambda=\frac{k_{\mathrm{ds}}}{2 L \sqrt{V_{D G}+V_{t n}+\Phi_{0}}}=\frac{k_{d s}}{2 L \sqrt{V_{D S}-V_{\text {eff }}+\Phi_{0}}} \tag{1.68}
\end{equation*}
$$

Equation (1.67) is accurate until $\mathrm{V}_{\mathrm{DS}}$ is large enough to cause second-order effects, often called short-channel effects. For example, (1.67) assumes that current flow down the channel is not velocity-saturated, in which case increasing the electric field no longer increases the carrier speed. Short-channel effects cause $I_{D}$ to deviate from the result predicted by (1.67) and are discussed in Section 1.4. Of course, for quite large values of $\mathrm{V}_{\mathrm{DS}}$, the transistor will eventually break down.

A plot of $I_{D}$ versus $V_{D S}$ for different values of $V_{G S}$ is shown in Fig. 1.16. Note that in the active region, the small (but nonzero) slope indicates the small dependence of $I_{D}$ on $V_{D S}$.
image_name:Fig. 1.16
description:The graph in Fig. 1.16 is a plot of drain current ($I_{D}$) versus drain-source voltage ($V_{DS}$) for different gate-source voltages ($V_{GS}$) in an n-channel MOSFET.

1. **Type of Graph and Function:**
- This is a characteristic curve graph for a MOSFET transistor, illustrating the relationship between $I_{D}$ and $V_{DS}$ for various values of $V_{GS}$.

2. **Axes Labels and Units:**
- The x-axis represents the drain-source voltage ($V_{DS}$), typically measured in volts (V).
- The y-axis represents the drain current ($I_{D}$), typically measured in amperes (A).
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The graph shows a series of curves, each corresponding to a different value of $V_{GS}$.
- For low $V_{DS}$ values, the curves rise steeply, indicating the triode region where the MOSFET operates as a variable resistor.
- As $V_{DS}$ increases, the curves flatten out, entering the active (or saturation) region where $I_{D}$ becomes relatively constant.
- The slope of the curves in the active region is small, indicating a weak dependence of $I_{D}$ on $V_{DS}$.
- Short-channel effects are noted at higher $V_{DS}$ values, where the curves begin to deviate from the ideal behavior.

4. **Key Features and Technical Details:**
- The transition from the triode to the active region is marked by the condition $V_{DS} = (V_{GS} - V_{tn})$, shown by a dashed line.
- The curves shift upwards with increasing $V_{GS}$, indicating higher $I_{D}$ for higher gate-source voltages.
- The region labeled "Short-channel effects" indicates where the actual device behavior deviates due to physical limitations.

5. **Annotations and Specific Data Points:**
- The graph is annotated with regions labeled "Triode region," "Active region," and "Short-channel effects."
- An arrow indicates increasing $V_{GS}$, showing the trend of the curves.
- The condition $V_{GS} > V_{tn}$ is noted, indicating operation above the threshold voltage.

Fig. 1.16 $\quad I_{D}$ versus $V_{D S}$ for different values of $V_{G S}$.

#### EXAMPLE 1.8

Find $I_{D}$ for an $n$-channel transistor that has doping concentrations of $N_{D}=10^{25}$ electrons $/ \mathrm{m}^{3}$, $\mathrm{N}_{\mathrm{A}}=5 \times 10^{22}$ holes $/ \mathrm{m}^{3}, \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}=270 \mu \mathrm{~A} / \mathrm{V}^{2}, \mathrm{~W} / \mathrm{L}=5 \mu \mathrm{~m} / 0.5 \mu \mathrm{~m}, \mathrm{~V}_{\mathrm{GS}}=0.8 \mathrm{~V}, \mathrm{~V}_{\mathrm{tn}}=0.45 \mathrm{~V}$, and $V_{D S}=V_{\text {eff }}$. Assuming $\lambda$ remains constant, estimate the new value of $I_{D}$ if $V_{D S}$ is increased by 0.5 V .

#### Solution

From (1.65), we have

$$
\mathrm{k}_{\mathrm{ds}}=\sqrt{\frac{2 \times 11.8 \times 8.854 \times 10^{-12}}{1.6 \times 10^{-19} \times 5 \times 10^{22}}}=162 \times 10^{-9} \mathrm{~m} / \sqrt{\mathrm{V}}
$$

which is used in (1.68) to find $\lambda$ as

$$
\lambda=\frac{162 \times 10^{-9}}{2 \times 0.5 \times 10^{-6} \times \sqrt{0.9}}=0.171 \mathrm{~V}^{-1}
$$

Using (1.67), we find for $\mathrm{V}_{\mathrm{DS}}=\mathrm{V}_{\text {eff }}=0.4 \mathrm{~V}$,

$$
I_{D 1}=\left(\frac{270 \times 10^{-6}}{2}\right)\left(\frac{5}{0.5}\right)(0.35)^{2}(1)=165 \mu \mathrm{~A}
$$

In the case where $\mathrm{V}_{\mathrm{Ds}}=\mathrm{V}_{\text {eff }}+0.5 \mathrm{~V}=0.9 \mathrm{~V}$, we have

$$
\mathrm{I}_{\mathrm{D} 2}=165 \mu \mathrm{~A} \times(1+\lambda \times 0.5)=180 \mu \mathrm{~A}
$$

Note that this example shows almost a 10 percent increase in drain current for a 0.5 V increase in drain-source voltage.

### 1.2.4 Body Effect

Key Point: The body effect is the influence of the body potential on the channel, modelled as an increase in the threshold voltage, $V_{t n}$, with increasing source-tobody reverse-bias.

The large-signal equations in the preceding section were based on the assumption that the source voltage was the same as the body voltage (i.e., the substrate or bulk voltage or an NMOS device). However, often the source and body can be at different voltages. Looking at Fig. 1.11, it is evident that the body is capacitively coupled to the channel region just as the gate is, albeit through the junction capacitance between them instead of the gate-oxide capacitance. ${ }^{11}$ Hence, the amount of charge in the channel and conduction through it is influenced by the potential difference between body and source.

Typically called the body effect, the influence of the body potential on the channel is modelled as an increase in the threshold voltage, $\mathrm{V}_{\mathrm{tn}}$, with increasing source-to-body reverse-bias voltage. The body effect is more important for transistors in a well of a CMOS process where the body terminal's doping concentration is higher and the resulting junction capacitance between body and channel is larger. The body effect is often important in analog circuit designs and should not be ignored.

To account for the body effect, it can be shown (see Appendix at the end of this chapter) that the threshold voltage of an n -channel transistor is now given by

$$
\begin{equation*}
\mathrm{V}_{\mathrm{tn}}=\mathrm{V}_{\mathrm{tn} 0}+\gamma\left(\sqrt{\mathrm{V}_{\mathrm{SB}}+\left|2 \phi_{\mathrm{F}}\right|}-\sqrt{\left|2 \phi_{\mathrm{F}}\right|}\right) \tag{1.69}
\end{equation*}
$$

where $V_{t n 0}$ is the threshold voltage with zero $V_{S B}$ (source-to-body voltage), $\phi_{F}=(k T / q) \ln \left(N_{A} / n_{i}\right)$ is the Fermi potential of the body, and

$$
\begin{equation*}
\gamma=\frac{\sqrt{2 \mathrm{qN}_{\mathrm{A}} \mathrm{~K}_{\mathrm{s}} \varepsilon_{0}}}{\mathrm{C}_{\mathrm{ox}}} \tag{1.70}
\end{equation*}
$$

The factor $\gamma$ is often called the body-effect constant and has units of $\sqrt{\mathrm{V}}$. Notice that $\gamma$ is proportional to $\sqrt{\mathrm{N}_{\mathrm{A}}},{ }^{12}$ so the body effect is larger for transistors in a well where typically the doping is higher than the substrate of the microcircuit.

### 1.2.5 p-Channel Transistors

All of the preceding equations have been presented for n -channel enhancement transistors. In the case of p-channel transistors, these equations can also be used if a neg ative sign is placed in front of eve ry voltage variable. Thus, $\mathrm{V}_{\mathrm{GS}}$ becomes $\mathrm{V}_{\mathrm{SG}}, \mathrm{V}_{\mathrm{Ds}}$ becomes $\mathrm{V}_{\mathrm{SD}}, \mathrm{V}_{\mathrm{tn}}$ becomes $-\mathrm{V}_{\mathrm{tp}}$, and so on. The condition required for conduction is now $V_{S G}>V_{t p}$, where $V_{t p}$ is now a negative quantity for an enhancement $p$-channel transistor. ${ }^{13}$ The requirement on the source-drain voltage for a $p$-channel transistor to be in the active region is $\mathrm{V}_{\mathrm{SD}}>\mathrm{V}_{\mathrm{SG}}+\mathrm{V}_{\mathrm{tp}}$. The equations for $\mathrm{I}_{\mathrm{D}}$, in both regions, remain unchanged, because all voltage variables are squared, resulting in positive hole current flow from the source to the drain in p-channel transistors.

[^5]
### 1.2.6 Low-Frequency Small-Signal Modelling in the Active Region

The most commonly used low-frequency small-signal model for a MOS transistor operating in the active region shown in Fig. 1.17. The voltage-controlled current source, $\mathrm{g}_{\mathrm{m}} \mathrm{v}_{\mathrm{gs}}$, is the most important component of the model, with the transistor transconductance $\mathrm{g}_{\mathrm{m}}$ defined as

$$
\begin{equation*}
\mathrm{g}_{\mathrm{m}}=\frac{\partial \mathrm{I}_{\mathrm{D}}}{\partial \mathrm{~V}_{\mathrm{GS}}} \tag{1.71}
\end{equation*}
$$

In the active region, we use (1.63), which is repeated here for convenience,

$$
\begin{equation*}
I_{D}=\frac{1}{2} \mu_{n} C_{o x}\left(\frac{W}{L}\right)\left(V_{G S}-V_{t n}\right)^{2}=\frac{1}{2} \mu_{n} C_{o x}\left(\frac{W}{L}\right) V_{\text {eff }}^{2} \tag{1.72}
\end{equation*}
$$

and we apply the derivative shown in (1.71) to obtain

$$
\begin{equation*}
g_{m}=\frac{\partial I_{D}}{\partial V_{G S}}=\mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{t n}\right)=\mu_{n} C_{o x} \frac{W}{L} V_{\text {eff }} \tag{1.73}
\end{equation*}
$$

or equivalently,

$$
\begin{equation*}
g_{m}=\mu_{n} C_{o x} \frac{W}{L} V_{\text {eff }} \tag{1.74}
\end{equation*}
$$

where the effective gate-source voltage, $\mathrm{V}_{\text {eff }}$, is defined as $\mathrm{V}_{\text {eff }} \equiv \mathrm{V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{tn}}$. Thus, we see that the transconductance of a MOS transistor is directly proportional to $\mathrm{V}_{\text {eff }}$.

Sometimes it is desirable to express $g_{m}$ in terms of $I_{D}$ rather than $V_{G s}$. From (1.72), we have

$$
\begin{equation*}
\mathrm{V}_{\mathrm{Gs}}=\mathrm{V}_{\mathrm{tn}}+\sqrt{\frac{2 \mathrm{I}_{\mathrm{D}}}{\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{~W} / \mathrm{L})}} \tag{1.75}
\end{equation*}
$$

The second term in (1.75) is the effective gate-source voltage, $\mathrm{V}_{\text {eff }}$, where

$$
\begin{equation*}
V_{\text {eff }}=V_{G S}-V_{t n}=\sqrt{\frac{2 I_{D}}{\mu_{n} C_{o x}(W / L)}} \tag{1.76}
\end{equation*}
$$

Substituting (1.76) in (1.74) results in an alternative expression for $\mathrm{g}_{\mathrm{m}}$.
image_name:Fig. 1.17
description:
[
name: vgs, type: VoltageSource, value: vgs, ports: {Np: vg, Nn: vs}
name: gmvgs, type: VoltageControlledCurrentSource, ports: {Np: vd, Nn: vs}
name: gsvsb, type: VoltageControlledCurrentSource, ports: {Np: vs, Nn: vd}
name: rds, type: Resistor, ports: {N1: vd, N2: vs}
]
extrainfo:The circuit is a low-frequency, small-signal model for an active MOS transistor. It includes a voltage source, two voltage-controlled current sources, and a resistor. The current id flows from the node vd through the resistor rds.

Fig. 1.17 The low-frequency, small-signal model for an active MOS transistor.

$$
\begin{equation*}
g_{m}=\sqrt{2 \mu_{n} C_{o x} \frac{W}{L} I_{D}} \tag{1.77}
\end{equation*}
$$

Thus, the transistor transconductance is proportional to $\sqrt{\mathrm{I}_{\mathrm{D}}}$ for a MOS transistor. ${ }^{14}$
A third expression for $\mathrm{g}_{\mathrm{m}}$ is found by rearranging (1.77) and then using (1.76) to obtain

$$
\begin{equation*}
g_{m}=\frac{2 I_{D}}{V_{\text {eff }}} \tag{1.78}
\end{equation*}
$$

Key Point: The square-root relationship for transconductance $g_{m}=\sqrt{2 \mu_{\mathrm{n}} C_{0 x}(W / L) I_{D}}$ is useful for circuit analysis when device sizes are fixed. However, the simpler expression $\mathrm{g}_{\mathrm{m}}=2 \mathrm{I}_{\mathrm{D}} / \mathrm{V}_{\text {eff }}$ is useful during initial circuit design when transistor sizes are yet to be determined.

Note that this expression is independent of $\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}$ and $\mathrm{W} / \mathrm{L}$, and it relates the transconductance to the ratio of drain current to effective gate-source voltage. However, it can cause some confusion for new analog designers as it appears to indicate that transconductance is proportional to drain current, whereas (1.77) indicates a square-root relationship. This discrepancy is resolved by recognizing that increasing $\mathrm{I}_{\mathrm{D}}$ while keeping $\mathrm{V}_{\text {eff }}$ constant implies a proportional increase in (W/L). Hence, (1.77) is useful for analysis where the transistor sizes are given whereas the simple expression in (1.78) can be quite useful during an initial circuit design when the transistor sizes are yet to be determined.

Design often begins with a set of transistor voltage-current measurements, obtained either by experiment or simulation, from which the designer may estimate the device constants $\mu_{n} C_{o x}, V_{t n}$, etc. based on the relationships presented above.

#### EXAMPLE 1.9

The drain current for a particular NMOS device with an aspect ratio $\mathrm{W} / \mathrm{L}=10$ is plotted in Fig. 1.18(a) versus $V_{G S}$ for constant drain, source, and body voltages. From this data, estimate $\mu_{n} C_{o x}$ and $V_{t n}$.

#### Solution

Taking the derivative of Fig. 1.18(a) gives the plot of $\mathrm{g}_{\mathrm{m}}=\delta \mathrm{I}_{\mathrm{D}} / \delta \mathrm{V}_{\mathrm{Gs}}$ in Fig. 1.18(b). Based on the square-law equation (1.74), this plot should be linear in the active region intersecting the line $g_{m}=0$ at $V_{\text {eff }}=0$. Hence, extrapolating the linear portion of the curve in Fig. 1.18(b) provides an intersection at $\mathrm{V}_{\mathrm{Gs}}=\mathrm{V}_{\mathrm{tn}}$. In this case, $\mathrm{V}_{\mathrm{tn}} \cong 450 \mathrm{mV}$. Furthermore, (1.73) shows that the slope of the $\mathrm{g}_{\mathrm{m}}$ versus $\mathrm{V}_{\mathrm{GS}}$ curve should be $\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{W} / \mathrm{L})$ in active operation. In Fig. 1.18(b) this slope is approximately $2.7 \mathrm{~mA} / \mathrm{V}^{2}$ which translates to a value of $\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}=270 \mu \mathrm{~A} / \mathrm{V}^{2}$. These are approximate values, particularly since (1.74) is derived without considering channel-length modulation. However, these values are very useful during design for quickly and roughly estimating the device sizes, currents and voltages required to obtain a desired $\mathrm{g}_{\mathrm{m}}$.

The second voltage-controlled current-source in Fig. 1.17, shown as $\mathrm{g}_{\mathrm{s}} \mathrm{v}_{\mathrm{s}}$, models the body effect on the small-signal drain current, $i_{d}$. When the source is connected to small-signal ground, or when its voltage does not change appreciably, then this current source can be ignored. When the body effect cannot be ignored, we have

$$
\begin{equation*}
\mathrm{g}_{\mathrm{s}}=\frac{\partial \mathrm{I}_{\mathrm{D}}}{\partial \mathrm{~V}_{\mathrm{SB}}}=\frac{\partial \mathrm{I}_{\mathrm{D}}}{\partial \mathrm{~V}_{\mathrm{tn}}} \frac{\partial \mathrm{~V}_{\mathrm{tn}}}{\partial \mathrm{~V}_{\mathrm{SB}}} \tag{1.79}
\end{equation*}
$$

[^6]image_name:(a)
description:The graph labeled (a) is a plot of the drain current (I_D) versus the gate-to-source voltage (V_GS) for a transistor.

1. **Type of Graph and Function:**
- This is an I-V characteristic curve, specifically showing the relationship between the drain current (I_D) and the gate-to-source voltage (V_GS) for a MOSFET.

2. **Axes Labels and Units:**
- The x-axis is labeled as V_GS (V), representing the gate-to-source voltage in volts.
- The y-axis is labeled as I_D (mA), representing the drain current in milliamperes.
- Both axes are on a linear scale.

3. **Overall Behavior and Trends:**
- The graph shows that the drain current (I_D) remains near zero for V_GS values up to approximately 0.4 volts, indicating a threshold behavior.
- Beyond this point, the current increases sharply, showing a nonlinear rise with increasing V_GS.
- This behavior is typical of a MOSFET entering the saturation region.

4. **Key Features and Technical Details:**
- The threshold voltage (V_th) can be inferred to be around 0.4 volts, where the current starts to increase significantly.
- There are no explicit peaks or valleys, as the graph shows a monotonic increase after the threshold.

5. **Annotations and Specific Data Points:**
- The graph does not have specific annotations or markers indicating particular data points, but the trend is clear from the shape of the curve.
image_name:(b)
description:The graph labeled (b) is a plot of transconductance (g_m) versus gate-source voltage (V_GS) for a MOSFET. The x-axis represents V_GS in volts (V), ranging from 0 to 0.8 V. The y-axis represents g_m in milliamperes per volt (mA/V), ranging from 0 to 0.8 mA/V.

Overall Behavior and Trends:
The graph shows a region of linear increase in g_m as V_GS increases. Initially, for V_GS values from 0 to about 0.4 V, g_m remains close to zero, indicating the MOSFET is in cutoff or subthreshold region. Beyond 0.4 V, g_m starts to increase linearly, showing the MOSFET entering the saturation region.

Key Features and Technical Details:
- **Linear Region:** The linear slope of the g_m curve is indicated as \( \mu_n C_{ox}(W/L) = 2.7 \text{ mA/V}^2 \).
- **Threshold Voltage (V_tn):** The graph is annotated with an intersection point at V_GS = 0.45 V, which is identified as the threshold voltage (V_tn). This is the point where the MOSFET starts to conduct significantly.

Annotations and Specific Data Points:
- **Linear Slope Annotation:** A dashed line is shown on the graph to highlight the linear relationship, with an annotation pointing to the slope value.
- **Intersection at V_tn:** An arrow points to the intersection at V_GS = 0.45 V, marking the threshold voltage where the curve begins to rise sharply.

This graph is useful for estimating the threshold voltage and the transconductance parameter \( \mu_n C_{ox}(W/L) \) from the MOSFET's I-V characteristics.

Fig. 1.18 Estimation of $\mathrm{V}_{\mathrm{tn}}$ and $\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}$ from transistor voltage-current data.
From (1.72) we have

$$
\begin{equation*}
\frac{\partial \mathrm{I}_{\mathrm{D}}}{\partial \mathrm{~V}_{\mathrm{tn}}}=-\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)\left(\mathrm{V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{tn}}\right)=-\mathrm{g}_{\mathrm{m}} \tag{1.80}
\end{equation*}
$$

Using (1.69), which gives $\mathrm{V}_{\mathrm{tn}}$ as

$$
\begin{equation*}
\mathrm{V}_{\mathrm{tn}}=\mathrm{V}_{\mathrm{tn} 0}+\gamma\left(\sqrt{\mathrm{V}_{\mathrm{SB}}+\left|2 \phi_{\mathrm{F}}\right|}-\sqrt{\left|2 \phi_{\mathrm{F}}\right|}\right) \tag{1.81}
\end{equation*}
$$

we have

$$
\begin{equation*}
\frac{\partial V_{\mathrm{tn}}}{\partial \mathrm{~V}_{\mathrm{SB}}}=\frac{\gamma}{2 \sqrt{\mathrm{~V}_{\mathrm{SB}}+\left|2 \phi_{\mathrm{F}}\right|}} \tag{1.82}
\end{equation*}
$$

The negative sign of (1.80) is eliminated by subtracting the current $\mathrm{g}_{\mathrm{s}} \mathrm{v}_{\mathrm{s}}$ from the major component of the drain current, $\mathrm{g}_{\mathrm{m}} \mathrm{V}_{\mathrm{gs}}$, as shown in Fig. 1.17. Thus, using (1.80) and (1.82), we have

$$
\begin{equation*}
g_{s}=\frac{\gamma g_{m}}{2 \sqrt{V_{S B}+\left|2 \phi_{F}\right|}} \tag{1.83}
\end{equation*}
$$

Note that although $g_{s}$ is nonzero for $V_{S B}=0$, if the source is connected to the bulk $v_{s b}$ is zero and $g_{s}$ may be excluded from the model. However, if the source happens to be biased at the same potential as the bulk but is not directly connected to $i t$, then the effect of $g_{s}$ should be taken into account since there may be nonzero small signals, $\mathrm{V}_{\mathrm{sb}}$.

The resistor, $r_{d s}$, shown in Fig. 1.17, accounts for the finite output impedance (i.e., it models the channellength modulation and its effect on the drain current due to changes in $\mathrm{V}_{\mathrm{DS}}$ ). Using (1.67), repeated here for convenience,

$$
\begin{equation*}
I_{D}=\frac{\mu_{n} C_{o x}}{2}\left(\frac{W}{L}\right)\left(V_{G S}-V_{t n}\right)^{2}\left[1+\lambda\left(V_{D S}-V_{\text {eff }}\right)\right] \tag{1.84}
\end{equation*}
$$

we have

$$
\begin{equation*}
\frac{1}{r_{d s}}=g_{d s}=\frac{\partial I_{D}}{\partial V_{D S}}=\lambda\left(\frac{\mu_{n} C_{o x}}{2}\right)\left(\frac{W}{L}\right)\left(V_{G S}-V_{t n}\right)^{2}=\lambda I_{D-s a t} \cong \lambda I_{D} \tag{1.85}
\end{equation*}
$$

where the approximation assumes $\lambda$ is small, such that we can approximate the drain bias current as being the same as $I_{D-\text { sat }}$. Thus,

$$
\begin{equation*}
r_{\mathrm{ds}} \cong \frac{1}{\lambda \mathrm{I}_{\mathrm{D}}} \tag{1.86}
\end{equation*}
$$

where

$$
\begin{equation*}
\lambda=\frac{\mathrm{k}_{\mathrm{ds}}}{2 \mathrm{~L} \sqrt{\mathrm{~V}_{\mathrm{Ds}}-\mathrm{V}_{\mathrm{eff}}+\Phi_{0}}} \tag{1.87}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{k}_{\mathrm{ds}}=\sqrt{\frac{2 \mathrm{~K}_{\mathrm{s}} \varepsilon_{0}}{\mathrm{qN}}} \tag{1.88}
\end{equation*}
$$

Key Point: Small signalr ds is proportional to $\mathrm{L} / \mathrm{I}_{\mathrm{D}}$.

Substituting (1.87) into (1.86) reveals that $r_{\mathrm{ds}}$ is proportional to $\mathrm{L} / \mathrm{I}_{\mathrm{D}}$. It should be noted here that (1.86) is often empirically adjusted to take into account secondorder effects.

#### EXAMPLE 1.10

Derive the low-frequency model parameters for an n -channel transistor that has doping concentrations of $\mathrm{N}_{\mathrm{D}}=10^{25}$ electrons $/ \mathrm{m}^{3}, \mathrm{~N}_{\mathrm{A}}=5 \times 10^{22}$ holes $/ \mathrm{m}^{3}, \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}=270 \mu \mathrm{~A} / \mathrm{V}^{2}, \mathrm{~W} / \mathrm{L}=5 \mu \mathrm{~m} / 0.5 \mu \mathrm{~m}, \mathrm{~V}_{\mathrm{GS}}=0.8 \mathrm{~V}$, $\mathrm{V}_{\mathrm{tn}}=0.45 \mathrm{~V}$, and $\mathrm{V}_{\mathrm{DS}}=\mathrm{V}_{\text {eff }}$. Assume $\gamma=0.25 \sqrt{\mathrm{~V}}$ and $\mathrm{V}_{\mathrm{SB}}=0.5 \mathrm{~V}$. What is the new value of $\mathrm{r}_{\mathrm{ds}}$ if the drain-source voltage is increased by 0.5 V ?

#### Solution

Since these parameters are the same as in Example 1.8, we have

$$
\mathrm{g}_{\mathrm{m}}=\frac{2 \mathrm{I}_{\mathrm{D}}}{\mathrm{~V}_{\mathrm{eff}}}=\frac{2 \times 165 \mu \mathrm{~A}}{0.35 \mathrm{~V}}=0.94 \mathrm{~mA} / \mathrm{V}
$$

The Fermi potential of the body at room temperature with $\mathrm{N}_{\mathrm{A}}=5 \times 10^{22}$ holes $/ \mathrm{m}^{3}$ is $\phi_{F}=(\mathrm{kT} / \mathrm{q})$ $\ln \left(N_{A} / n_{i}\right) \cong 0.38 \mathrm{~V}$, and from (1.83) we have

$$
\mathrm{g}_{\mathrm{s}}=\frac{0.25 \times 0.94 \times 10^{-3}}{2 \sqrt{0.5+0.766}}=0.104 \mathrm{~mA} / \mathrm{V}
$$

Note that this source-bulk transconductance value is about 1/9th that of the gate-source transconductance. For $r_{d s}$, we use (1.86) to find

$$
\mathrm{r}_{\mathrm{ds}}=\frac{1}{0.171 \times 165 \times 10^{-6}}=35 \mathrm{k} \Omega
$$

Recalling that $\mathrm{V}_{\text {eff }}=0.35 \mathrm{~V}$, if $\mathrm{V}_{\mathrm{Ds}}$ is increased to 0.85 V , the new value for $\lambda$ is

$$
\lambda=\frac{162 \times 10^{-9}}{2\left(0.5 \times 10^{-6}\right) \sqrt{1.4}}=0.137 \mathrm{~V}^{-1}
$$

resulting in a new value of $r_{d s}$ given by

$$
r_{\mathrm{ds}}=\frac{1}{\lambda \mathrm{I}_{\mathrm{D} 2}}=\frac{1}{0.137 \times 180 \times 10^{-6}} \cong 41 \mathrm{k} \Omega
$$

#### EXAMPLE 1.11

Plotted in Fig. 1.19(a) is the drain current of a particular NMOS device versus its $\mathrm{V}_{\mathrm{DS}}$ with constant gate, source, and body voltages. From this data, estimate the device parameter $\lambda$.

#### Solution

First, rearrange (1.85) into

$$
\lambda=\frac{g_{\mathrm{ds}}}{I_{D-\text { sat }}}=\left(\frac{\partial I_{D}}{\partial V_{D S}}\right) \frac{1}{I_{D-\text { sat }}}
$$

Hence, a plot of $\mathrm{g}_{\mathrm{ds}} / \mathrm{I}_{\mathrm{D}}=\left(\partial \mathrm{I}_{\mathrm{D}} / \partial \mathrm{V}_{\mathrm{DS}}\right) / \mathrm{I}_{\mathrm{D}}$ versus $\mathrm{V}_{\mathrm{DS}}$ for a constant value of $\mathrm{V}_{\mathrm{GS}}$ will be roughly flat in strong inversion providing a rough estimate of $\lambda$. This is done for the present example in Fig. 1.19(b) yielding a value of $\lambda=0.45 \mathrm{~V}^{-1}$. Estimates obtained in this way are only approximate since $r_{d s}$ is subject to many higher-order effects, especially at short channel lengths where $\lambda$ may change by $50 \%$ or even more.
image_name:(a)
description:The graph labeled (a) is a plot of the drain current ($I_D$) in milliamperes (mA) versus the drain-source voltage ($V_{DS}$) in volts (V) for a MOS transistor. The x-axis represents $V_{DS}$ ranging from 0 to 1 V, while the y-axis represents $I_D$ ranging from 0 to 0.04 mA. The graph uses a linear scale for both axes.

**Overall Behavior and Trends:**
The plot shows an initial steep increase in $I_D$ as $V_{DS}$ increases from 0 to about 0.1 V, indicating the transistor is transitioning from the cutoff to the active region. Beyond this point, the curve flattens significantly, suggesting the transistor is in saturation where $I_D$ becomes relatively constant despite increases in $V_{DS}$. This behavior is typical in the saturation region of a MOSFET, where the current is primarily controlled by the gate-source voltage ($V_{GS}$) rather than the drain-source voltage.

**Key Features and Technical Details:**
- The curve starts at the origin (0,0) and rises sharply, reaching a current of approximately 0.02 mA at around 0.1 V of $V_{DS}$.
- Beyond 0.1 V, the curve becomes nearly horizontal, indicating a saturation region with a current of approximately 0.03 to 0.04 mA.
- This flat region is used to estimate the channel-length modulation parameter ($\lambda$), although the graph itself does not explicitly show $\lambda$.

**Annotations and Specific Data Points:**
- The graph does not include specific annotations or markers for key data points other than the general shape and behavior of the curve. However, the context suggests that the flat region is crucial for estimating $
\lambda$, as mentioned in the text.

This graph is useful for analyzing the behavior of a MOS transistor in different regions of operation, specifically highlighting the transition from the linear to the saturation region.
image_name:(b)
description:The graph labeled (b) is a plot of the transconductance efficiency, \( g_{ds}/I_D \) (in \( V^{-1} \)), versus the drain-source voltage, \( V_{DS} \) (in volts). This is a typical graph used to analyze the behavior of a MOS transistor in its active region.

**Type of Graph and Function:**
The graph is a 2D Cartesian plot representing the relationship between the transconductance efficiency and the drain-source voltage of a MOS transistor.

**Axes Labels and Units:**
- The x-axis represents the drain-source voltage, \( V_{DS} \), measured in volts (V), with a linear scale ranging from 0 to 1 V.
- The y-axis represents the transconductance efficiency ratio, \( g_{ds}/I_D \), measured in inverse volts (\( V^{-1} \)), with a linear scale ranging from 0 to 1 \( V^{-1} \).

**Overall Behavior and Trends:**
The graph shows a decreasing trend of the transconductance efficiency \( g_{ds}/I_D \) as the \( V_{DS} \) increases. Initially, the curve starts at a high value and rapidly decreases, stabilizing as it approaches the right side of the graph, indicating the active region of the MOS transistor.

**Key Features and Technical Details:**
- The curve starts at a high transconductance efficiency value near 1 \( V^{-1} \) at low \( V_{DS} \) and decreases sharply.
- A horizontal dashed line is marked at \( \lambda = 0.45 \; V^{-1} \), indicating the approximate value of the channel-length modulation parameter \( \lambda \).
- The active region is labeled on the graph, indicating where the MOS transistor operates effectively.

**Annotations and Specific Data Points:**
- The dashed line at \( \lambda = 0.45 \; V^{-1} \) serves as a reference for estimating the channel-length modulation parameter, which is crucial for understanding the behavior of the transistor in the active region.

Fig. 1.19 Estimation of $\lambda$ from transistor voltage-current data.
image_name:Fig. 1.20
description:
[
name: rds, type: Resistor, value: rds, ports: {N1: Vd, N2: Vs}
name: rs, type: Resistor, value: 1/gm, ports: {N1: Vg, N2: Vs}
name: is, type: CurrentSource, value: is, ports: {Np: Vd, Nn: Vg}
]
extrainfo:The circuit represents a small-signal, low-frequency T model for an active MOS transistor. The model uses a voltage source, current source, and resistors to simulate the behavior of the transistor without modeling the body effect.

Fig. 1.20 The small-signal, low-frequency T model for an active MOS transistor (the body effect is not modelled).

An alternate low-frequency model, known as a T model, is shown in Fig. 1.20. This T model can often result in simpler equations and is most often used by experienced designers for a quick analysis. At first glance, it might appear that this model allows for nonzero gate current, but a quick check confirms that the drain current must always equal the source current, and, therefore, the gate current must always be zero. For this reason, when using the T model, one assumes from the beginning that the gate current is zero.

#### EXAMPLE 1.12

Find the T model parameter, $r_{\mathrm{s}}$, for the transistor in Example 1.10.

#### Solution

The value of $r_{s}$ is simply the inverse of $g_{m}$, resulting in

$$
r_{s}=\frac{1}{g_{m}}=\frac{1}{0.94 \times 10^{-3}}=1.06 \mathrm{k} \Omega
$$

The value of $r_{\mathrm{ds}}$ remains the same, either $35 \mathrm{k} \Omega$ or $41 \mathrm{k} \Omega$ depending on the drain-source voltage.

### 1.2.7 High-Frequency Small-Signal Modelling in the Active Region

A high-frequency model of a MOSFET in the active region is shown in Fig. 1.21. Most of the capacitors in the small-signal model are related to the physical transistor. Shown in Fig. 1.22 is a cross section of a MOS transistor, where the parasitic capacitances are shown at the appropriate locations. The largest capacitor in Fig. 1.22 is $\mathrm{C}_{\mathrm{gs}}$. This capacitance is primarily due to the change in channel charge as a result of a change in $\mathrm{V}_{\mathrm{GS}}$. It can be shown [Tsividis, 1987] that $\mathrm{C}_{\mathrm{gs}}$ is approximately given by

$$
\begin{equation*}
\mathrm{C}_{\mathrm{gs}} \cong \frac{2}{3} \mathrm{WLC}_{\mathrm{ox}} \tag{1.89}
\end{equation*}
$$

image_name:Fig. 1.21 The small-signal model for a MOS transistor in the active region.
description:
[
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: Vg, Nn: Vs}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: Vg, Nn: Vd}
name: Csb, type: Capacitor, value: Csb, ports: {Np: Vs, Nn: GND}
name: Cdb, type: Capacitor, value: Cdb, ports: {Np: Vd, Nn: GND}
name: g_m*v_gs, type: VoltageControlledCurrentSource, ports: {Np: Vd, Nn: Vs}
name: g_s*v_s, type: VoltageControlledCurrentSource, ports: {Np: Vs, Nn: Vd}
name: r_ds, type: Resistor, value: r_ds, ports: {N1: Vd, N2: Vd}
]
extrainfo:The circuit is a small-signal model for a MOS transistor in the active region, showing parasitic capacitances and controlled sources.

Fig. 1.21 The small-signal model for a MOS transistor in the active region.

When accuracy is important, an additional term should be added to (1.89) to take into account the overlap between the gate and source junction, which should include the fringing capacitance (fringing capacitance is due to boundary effects). This additional component is given by

$$
\begin{equation*}
C_{o v}=W L_{o v} C_{o x} \tag{1.90}
\end{equation*}
$$

where $L_{\mathrm{ov}}$ is the effective overlap distance and is usually empirically derived ${ }^{15}$. Thus,

$$
\begin{equation*}
\mathrm{C}_{\mathrm{gs}}=\frac{2}{3} \mathrm{WLC}_{\mathrm{ox}}+\mathrm{C}_{\mathrm{ov}} \tag{1.91}
\end{equation*}
$$

Key Point: In a MOSFET, the largest parasitic capacitance is $\mathrm{C}_{\mathrm{gs} \text { s }}$, proportional to gate area WL and via $\mathrm{C}_{\mathrm{ox}}$ inversely proportional to oxide thickness.
when higher accuracy is needed.
image_name:Fig. 1.22
description:The image is a cross-sectional diagram of an n-channel MOS transistor, illustrating the small-signal capacitances involved. Key components and their interactions are highlighted as follows:

1. **Components and Structure:**
- **Polysilicon Gate:** This is the control gate of the MOSFET, shown in the center, with arrows indicating the application of gate-source voltage \( V_{GS} > V_{tn} \).
- **Source and Drain Regions:** These are labeled as \( n^+ \) regions on either side of the gate, indicating heavily doped n-type semiconductor areas.
- **p+ Field Implant:** Located on the left, this is used to control the electric field and reduce leakage.
- **p- Substrate:** The bulk of the transistor, indicated as the base layer.
- **Aluminum (Al) Contacts:** These are metal contacts for the source and drain, providing electrical connection.
- **SiO2 Layer:** This is the oxide layer separating the gate from the channel.

2. **Connections and Interactions:**
- **Gate-Source Capacitance \( C_{gs} \):** This is a key parasitic capacitance between the gate and source, affecting the transistor’s switching speed.
- **Gate-Drain Capacitance \( C_{gd} \):** This capacitance affects the Miller effect and switching characteristics.
- **Source-Bulk Capacitance \( C_{sb} \):** This is the capacitance between the source and substrate.
- **Drain-Bulk Capacitance \( C_{db} \):** This capacitance is between the drain and substrate.
- **Overlap Capacitance \( L_{ov} \):** Shown by a dashed line, it indicates the overlap region contributing to parasitic capacitance.
- **Source-Substrate Capacitance \( C_{s-sw} \):** Associated with the source-well junction.
- **Drain-Substrate Capacitance \( C_{d-sw} \):** Associated with the drain-well junction.

3. **Labels, Annotations, and Key Features:**
- Voltage conditions such as \( V_{SB} = 0 \) and \( V_{DG} > -V_{tn} \) are noted, indicating biasing conditions for the MOSFET.
- The diagram includes directional arrows showing the direction of current flow and electric field lines.
- The effective overlap distance \( L_{ov} \) is marked to signify its contribution to the overlap capacitance.

Fig. 1.22 A cross section of an n-channel MOS transistor showing the small-signal capacitances.
15. Part of the overlap capacitance is due to fringe electric fields, and therefore $\mathrm{L}_{\mathrm{ov}}$ is usually taken larger than its actual physical overlap to more accurately give an effective value for overlap capacitances.

The next largest capacitor in Fig. 1.22 is $\mathrm{C}_{\text {sb }}$, the capacitor between the source and the substrate. This capacitor is due to the depletion capacitance of the reverse-biased source junction, and it includes the channel-to-bulk capacitance (assuming the transistor is on). Its size is given by

$$
\begin{equation*}
C_{s b}^{\prime}=\left(A_{s}+A_{c h}\right) C_{j s} \tag{1.92}
\end{equation*}
$$

where $A_{s}$ is the area of the source junction, $A_{c h}$ is the area of the channel (i.e., $W L$ ) and $C_{j s}$ is the depletion capacitance of the source junction, given by

$$
\begin{equation*}
\mathrm{C}_{\mathrm{is}}=\frac{\mathrm{C}_{\mathrm{j} 0}}{\sqrt{1+\frac{\mathrm{V}_{\mathrm{SB}}}{\Phi_{0}}}} \tag{1.93}
\end{equation*}
$$

Note that the total area of the effective source includes the original area of the junction (when no channel is present) plus the effective area of the channel.

The depletion capacitance of the drain is smaller because it does not include the channel area. Here, we have

$$
\begin{equation*}
\mathrm{C}_{\mathrm{db}}^{\prime}=\mathrm{A}_{\mathrm{d}} \mathrm{C}_{\mathrm{jd}} \tag{1.94}
\end{equation*}
$$

where

$$
\begin{equation*}
\mathrm{C}_{\mathrm{jd}}=\frac{\mathrm{C}_{\mathrm{j} 0}}{\sqrt{1+\frac{\mathrm{V}_{\mathrm{DB}}}{\Phi_{0}}}} \tag{1.95}
\end{equation*}
$$

and $A_{d}$ is the area of the drain junction.
The capacitance $\mathrm{C}_{\mathrm{gd}}$, sometimes called the Miller capacitance, is important when there is a large voltage gain between gate and drain. It is primarily due to the overlap between the gate and the drain and fringing capacitance. Its value is given by

$$
\begin{equation*}
C_{g d}=C_{o x} W L_{o v} \tag{1.96}
\end{equation*}
$$

Key Point: The gate-drain capacitance $\mathrm{C}_{\mathrm{gd}}$ also known as the Miller capacitance, is due to physical overlap of the gate and drain regions as well as fringing fields. It is especially important when there is a large voltage gain between gate and drain.
where, once again, $\mathrm{L}_{\mathrm{ov}}$ is usually empirically derived.
Two other capacitors are often important in integrated circuits. These are the source and drain sidewall capacitances, $\mathrm{C}_{\mathrm{s} \text {-sw }}$ and $\mathrm{C}_{\mathrm{d} \text {-sw }}$. These capacitances can be large because of some highly doped $\mathrm{p}^{+}$regions under the thick field oxide called field implants. The major reason these regions exist is to ensure there is no leakage current between transistors. Because they are highly doped and they lie beside the highly doped source and drain junctions, the sidewall capacitances can result in large additional capacitances that must be taken into account in determining $C_{s b}$ and $C_{d b}$. The sidewall capacitances are especially important in modern technologies as dimensions shrink. For the source, the sidewall capacitance is given by

$$
\begin{equation*}
C_{s-s w}=P_{s} C_{j-s w} \tag{1.97}
\end{equation*}
$$

where $P_{s}$ is the length of the perimeter of the source junction, excluding the side adjacent to the channel, and

$$
\begin{equation*}
C_{j-s w}=\frac{C_{j-s w 0}}{\sqrt{1+\frac{V_{S B}}{\Phi_{0}}}} \tag{1.98}
\end{equation*}
$$

It should be noted that $\mathrm{C}_{\mathrm{j} \text {-sw } 0}$, the sidewall capacitance per unit length at $0-\mathrm{V}$ bias voltage, can be quite large because the field implants are heavily doped.

The situation is similar for the drain sidewall capacitance, $\mathrm{C}_{\mathrm{d} \text {-sw }}$,

$$
\begin{equation*}
C_{d-s w}=P_{d} C_{j-s w} \tag{1.99}
\end{equation*}
$$

where $P_{d}$ is the drain perimeter excluding the portion adjacent to the gate.
Finally, the source-bulk capacitance, $\mathrm{C}_{\mathrm{sb}}$, is given by

$$
\begin{equation*}
C_{s b}=C_{s b}^{\prime}+C_{s-\mathrm{sw}} \tag{1.100}
\end{equation*}
$$

with the drain-bulk capacitance, $\mathrm{C}_{\mathrm{db}}$, given by

$$
\begin{equation*}
C_{d b}=C_{d b}^{\prime}+C_{d-s w} \tag{1.101}
\end{equation*}
$$

#### EXAMPLE 1.13

An n -channel transistor is modelled as having the following capacitance parameters: $\mathrm{C}_{\mathrm{j}}=2.4 \times 10^{-4} \mathrm{pF} /(\mu \mathrm{m})^{2}$, $\mathrm{C}_{\mathrm{j} \text {-sw }}=2.0 \times 10^{-4} \mathrm{pF} / \mu \mathrm{m}, \mathrm{C}_{\mathrm{ox}}=1.9 \times 10^{-3} \mathrm{pF} /(\mu \mathrm{m})^{2}, \mathrm{C}_{\mathrm{ov}}=2.0 \times 10^{-4} \mathrm{pF} / \mu \mathrm{m}$. Find the capacitances $\mathrm{C}_{\mathrm{gs}}$, $\mathrm{C}_{\mathrm{gd},} \mathrm{C}_{\mathrm{db} \text {, and }} \mathrm{C}_{\mathrm{sb}}$ for a transistor having $\mathrm{W}=100 \mu \mathrm{~m}$ and $\mathrm{L}=2 \mu \mathrm{~m}$. Assume the source and drain junctions extend $4 \mu \mathrm{~m}$ beyond the gate, so that the source and drain areas are $A_{s}=A_{d}=400(\mu \mathrm{~m})^{2}$ and the perimeter of each is $P_{s}=P_{d}=108 \mu \mathrm{~m}$.

#### Solution

We calculate the various capacitances as follows:

$$
\begin{gathered}
C_{g s}=\left(\frac{2}{3}\right) W L C_{o x}+C_{o v} \times W=0.27 \mathrm{pF} \\
C_{g d}=C_{o v} \times W=0.02 \mathrm{pF} \\
C_{s b}=C_{j}\left(A_{s}+W L\right)+\left(C_{j-s w} \times P_{s}\right)=0.17 \mathrm{pF} \\
C_{d b}=\left(C_{j} \times A_{d}\right)+\left(C_{j-s w} \times P_{d}\right)=0.12 \mathrm{pF}
\end{gathered}
$$

Note that the source-bulk and drain-bulk capacitances are significant compared to the gate-source capacitance, in this case $1-2 \mathrm{fF} / \mu \mathrm{m}$ width compared with $2.7 \mathrm{fF} / \mu \mathrm{m}$ for $\mathrm{C}_{\mathrm{gs}}$. Thus, for high-speed circuits, it is important to keep the areas and perimeters of drain and source junctions as small as possible (possibly by sharing junctions between transistors, as seen in the next chapter).

### 1.2.8 Small-Signal Modelling in the Triode and Cutoff Regions

The low-frequency, small-signal model of a MOS transistor in the triode region (which is sometimes referred to as the linear region) is a voltage-controlled resistor with $\mathrm{V}_{\mathrm{GS}}$, or equivalently $\mathrm{V}_{\text {eff }}$, used as the control terminal. Using (1.61), the large-signal equation for $I_{D}$ in the triode region,

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D}}=\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)\left[\left(\mathrm{V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{tn}}\right) \mathrm{V}_{\mathrm{DS}}-\frac{\mathrm{V}_{\mathrm{DS}}^{2}}{2}\right] \tag{1.102}
\end{equation*}
$$

results in

$$
\begin{equation*}
\frac{1}{r_{d s}}=g_{d s}=\frac{\partial I_{D}}{\partial V_{D S}}=\mu_{n} C_{o x}\left(\frac{W}{L}\right)\left(V_{G S}-V_{t n}-V_{D S}\right) \tag{1.103}
\end{equation*}
$$

where $r_{d s}$ is the small-signal drain-source resistance (and $g_{d s}$ is the conductance). For the common case of $V_{D S}$ near zero, we have

$$
\begin{equation*}
g_{\mathrm{ds}}=\frac{1}{\mathrm{r}_{\mathrm{ds}}}=\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)\left(\mathrm{V}_{\mathrm{Gs}}-\mathrm{V}_{\mathrm{tn}}\right)=\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right) \mathrm{V}_{\mathrm{eff}} \tag{1.104}
\end{equation*}
$$

which is similar to the $I_{D}$-versus- $V_{D S}$ relationship given earlier in (1.56).

#### EXAMPLE 1.14

For the transistor of Example 1.10, find the triode model parameters when $\mathrm{V}_{\mathrm{DS}}$ is near zero.

#### Solution

From (1.104), we have

$$
g_{\mathrm{ds}}=270 \times 10^{-6} \times\left(\frac{5}{0.5}\right) \times 0.35=0.94 \mathrm{~mA} / \mathrm{V}
$$

Note that this conductance value is the same as the transconductance of the transistor, $\mathrm{g}_{\mathrm{m}}$, in the active region. The resistance, $\mathrm{r}_{\mathrm{ds}}$, is simply $1 / \mathrm{g}_{\mathrm{ds}}$, resulting in $\mathrm{r}_{\mathrm{ds}}=1.06 \mathrm{k} \Omega$.

The accurate small-signal modelling of the high-frequency operation of a transistor in the triode region is nontrivial (even with the use of a computer simulation). A moderately accurate model is shown in Fig. 1.23, where the gate-to-channel capacitance and the channel-to-substrate capacitance are modelled as distributed elements. However, the I-V relationships of the distributed RC elements are highly nonlinear because the junction capacitances of the source and drain are nonlinear depletion capacitances, as is the channel-to-substrate capacitance. Also, if $\mathrm{V}_{\mathrm{DS}}$ is not small, then the channel resistance per unit length should increase as one moves closer to the drain. This model is much too complicated for use in hand analysis.
image_name:Fig. 1.23 A distributed RC model for a transistor in the triode region.
description:
[
name: Csb, type: Capacitor, value: Csb, ports: {Np: Vs, Nn: GND}
name: Cdb, type: Capacitor, value: Cdb, ports: {Np: Vd, Nn: GND}
]
extrainfo:The circuit diagram represents a distributed RC model for a transistor in the triode region. It includes channel-to-substrate capacitance and gate-to-channel capacitance. The resistive element models the channel resistance.

Fig. 1.23 A distributed RC model for a transistor in the triode region.

A simplified model often used for small $\mathrm{V}_{\mathrm{DS}}$ is shown in Fig. 1.24, where the resistance, $r_{d s}$, is given by (1.104). Here, the gate-to-channel capacitance has been evenly divided between the source and drain nodes,

$$
\begin{equation*}
C_{g s}=C_{g d}=\frac{A_{c h} C_{0 x}}{2}=\frac{W_{L C} C_{0 x}}{2} \tag{1.105}
\end{equation*}
$$

Note that this equation ignores the gate-to-junction overlap capacitances, as given by (1.90), which should be taken into account when accuracy is very important. The channel-tosubstrate capacitance has also been divided in half and shared between the source and drain junctions. Each of these capacitors should be added to the junction-to-substrate capacitance and the junction-sidewall capacitance at the appropriate node.
image_name:Fig. 1.24
description:
[
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: Vg, Nn: Vs}
name: Csb, type: Capacitor, value: Csb, ports: {Np: Vs, Nn: GND}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: Vg, Nn: Vd}
name: Cdb, type: Capacitor, value: Cdb, ports: {Np: Vd, Nn: GND}
name: rds, type: Resistor, value: rds, ports: {N1: Vs, N2: Vd}
]
extrainfo:The circuit represents a simplified triode-region model for small V_DS, including capacitive effects between the gate, source, drain, and body.

Fig. 1.24 A simplified triode-region model valid for small $V_{D S}$.

Thus, we have

$$
\begin{equation*}
C_{s b-0}=C_{j 0}\left(A_{s}+\frac{A_{c h}}{2}\right)+C_{j-s w 0} P_{s} \tag{1.106}
\end{equation*}
$$

and

$$
\begin{equation*}
C_{d b-0}=C_{j 0}\left(A_{d}+\frac{A_{c h}}{2}\right)+C_{j-s w 0} P_{d} \tag{1.107}
\end{equation*}
$$

Also,

$$
\begin{equation*}
\mathrm{C}_{\mathrm{sb}}=\frac{\mathrm{C}_{\mathrm{sb}-0}}{\sqrt{1+\frac{\mathrm{V}_{\mathrm{sb}}}{\Phi_{0}}}} \tag{1.108}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{C}_{\mathrm{db}}=\frac{\mathrm{C}_{\mathrm{db}-0}}{\sqrt{1+\frac{\mathrm{V}_{\mathrm{db}}}{\Phi_{0}}}} \tag{1.109}
\end{equation*}
$$

It might be noted that $\mathrm{C}_{\mathrm{sb}}$ is often comparable in size to $\mathrm{C}_{\mathrm{gs}}$ due to its larger area and the sidewall capacitance.
When the transistor turns off, the small-signal model changes considerably. A reasonable model is shown in Fig. 1.25. Perhaps the biggest difference is that $r_{d s}$ is now infinite. Another major difference is that $C_{g s}$ and $C_{g d}$ are now much smaller. Since the channel has disappeared, these capacitors are now due to only overlap and fringing capacitance. Thus, we have

$$
\begin{equation*}
C_{g s}=C_{g d}=W L_{o v} C_{o x} \tag{1.110}
\end{equation*}
$$

However, the reduction of $\mathrm{C}_{g \mathrm{~s}}$ and $\mathrm{C}_{\mathrm{gd}}$ does not mean that the total gate capacitance is necessarily smaller. We now have a "new" capacitor, $\mathrm{C}_{\mathrm{gb}}$, which is the gate-to-substrate capacitance. This capacitor is highly nonlinear and dependent on the gate voltage. If the gate voltage has been very negative for some time and the gate is accumulated, then we have

$$
\begin{equation*}
C_{g b}=A_{c h} C_{o x}=W L C_{o x} \tag{1.111}
\end{equation*}
$$

image_name:Fig. 1.25
description:
[
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: Vs, Nn: Vg}
name: Csb, type: Capacitor, value: Csb, ports: {Np: Vs, Nn: GND}
name: Cgb, type: Capacitor, value: Cgb, ports: {Np: Vg, Nn: GND}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: Vg, Nn: Vd}
name: Cdb, type: Capacitor, value: Cdb, ports: {Np: Vd, Nn: GND}
]
extrainfo:The diagram represents a small-signal model for a MOSFET that is turned off, highlighting various capacitances between the gate, source, drain, and substrate.

Fig. 1.25 A small-signal model for a MOSFET that is turned off.

If the gate-to-source voltage is around 0 V , then $\mathrm{C}_{\mathrm{gb}}$ is equal to $\mathrm{C}_{\mathrm{ox}}$ in series with the channel-to-bulk depletion capacitance and is considerably smaller, especially when the substrate is lightly doped. Another case where $\mathrm{C}_{\mathrm{gb}}$ is small is just after a transistor has been turned off, before the channel has had time to accumulate. Because of the complicated nature of correctly modelling $\mathrm{C}_{\mathrm{gb}}$ when the transistor is turned off, equation (1.111) is usually used for hand analysis as a worst-case estimate.

The capacitors $\mathrm{C}_{\mathrm{sb}}$ and $\mathrm{C}_{\mathrm{db}}$ are also smaller when the channel is not present. We now have

$$
\begin{equation*}
\mathrm{C}_{\mathrm{sb}-0}=\mathrm{A}_{\mathrm{s}} \mathrm{C}_{\mathrm{j} 0} \tag{1.112}
\end{equation*}
$$

and

$$
\begin{equation*}
C_{d b-0}=A_{d} C_{j 0} \tag{1.113}
\end{equation*}
$$

### 1.2.9 Analog Figures of Merit and Trade-offs

With so many device constants and small-signal model parameters, it is sometimes useful to have a single number that captures some key aspect of transistor performance. Two such figures of merit are considered in this section: intrinsic gain, which relates to the transistor's low-frequency small-signal performance; and intrinsic speed, related to the transistor's high-frequency small-signal performance.

The intrinsic gain of a transistor is a measure of the maximum possible low-frequency small-signal voltage gain it can provide. The voltage gain of a transistor is generally maximized by operating it in the active mode with the source terminal (small-signal) grounded, the input applied to the gate, and the output observed at the drain terminal, as shown in Fig. 1.26(a). In order to maximize gain, an ideal current source is used to provide the drain current so that the only load the drain terminal sees is the transistor itself. Measured in this way, the intrinsic gain is closely related to the gain provided by several important singlestage amplifier stages discussed in later sections, such as common-source amplifiers and differential pairs with active loads.
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vgs, Nn: g1}
name: Vgs, type: VoltageSource, value: Vgs, ports: {Np: Vgs, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: g1}
name: LOAD, type: CurrentSource, ports: {Np: VDD, Nn: Vout}
]
extrainfo:The circuit is designed to measure the intrinsic gain of a transistor using an NMOS configuration with a current source as the load. The intrinsic gain is calculated as the product of transconductance (gm) and output resistance (rds). The input is applied at the gate of the NMOS, and the output is taken from the drain terminal.
image_name:(b)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Vgs, type: VoltageSource, value: Vgs, ports: {Np: Vin, Nn: GND}
name: gmVgs, type: VoltageControlledCurrentSource, value: gmVgs, ports: {Np: GND, Nn: Vout}
name: rds, type: Resistor, value: rds, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit diagram (b) represents a small-signal equivalent model at DC for characterizing the intrinsic gain of a transistor. It includes a voltage source Vin driving the input, a voltage-controlled current source gmVgs representing the transistor's transconductance, and a resistor rds modeling the drain-source resistance. The output is measured across Vout.

(b)

Fig. 1.26 The circuit used to characterize transistor intrinsic gain: a) complete circuit; b) dc smallsignal equivalent.

The small-signal equivalent circuit at dc simplifies to that shown in Fig. 1.26(b). The transistor's intrinsic gain is therefore,

$$
\begin{equation*}
A_{i}=\left|\frac{v_{\text {out }}}{v_{\text {in }}}\right|=g_{m} r_{\text {ds }} \tag{1.114}
\end{equation*}
$$

Substituting the expressions for $g_{m}$ from equation (1.78) and $r_{d s}$ from (1.86) gives a simple expression for transistor intrinsic gain dependent on only a few device parameters.

$$
\begin{equation*}
A_{i} \cong \frac{2 I_{D}}{V_{\text {eff }}} \cdot \frac{1}{\lambda I_{D}}=\frac{2}{\lambda V_{\text {eff }}} \tag{1.115}
\end{equation*}
$$

The intrinsic gain in the active mode will be somewhat larger than this because (1.115) assumes $r_{d s} \cong 1 / \lambda I_{D}$ whereas in fact $r_{d s} \cong 1 / \lambda I_{D, \text { sat }}$ which is somewhat larger.

This reveals two important general conclusions about analog design: first, that to maximize dc gain, transistors should be operated with small values of $\mathrm{V}_{\text {eff }}$; second, since $\lambda$ is inversely proportional to gate length L , as shown in equation (1.87), intrinsic gain is maximized by taking long gate lengths.

#### EXAMPLE 1.15

Calculate the intrinsic gain of the transistor in Example 1.10 when in active mode.

#### Solution

The intrinsic gain is obtained by substituting the values for $g_{m}$ and $r_{d s}$ calculated in Example 1.10 into (1.114).

$$
A_{i}=g_{m} r_{d s}=32.9
$$

This is the largest voltage gain this single transistor can achieve under these operating bias conditions.

The unity-gain frequency of a transistor, $\mathrm{f}_{\mathrm{t}}$, is intended to provide some measure of the maximum operating frequency at which a transistor might prove useful. It is the most common (though not the only) measure of transistor intrinsic speed. As with intrinsic gain, $f_{t}$ is measured in the common-source configuration because of its broad relevance to both analog and digital design. An idealized measurement setup is shown in Fig. 1.27(a). Bias
image_name:(a)
description:
[
name: Vin, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: M1, type: NMOS, ports: {S: GND, D: Vout, G: Vin}
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: Vin, Nn: GND}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: Vin, Nn: Vout}
name: X, type: VoltageControlledCurrentSource, value: gmVgs, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit is used to characterize the intrinsic speed of a transistor by measuring the unity-gain frequency. It includes an NMOS transistor, gate-source and gate-drain capacitances, and a voltage-controlled current source representing the transconductance.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vgs, G: Vin}
name: g1, type: VoltageSource, value: Vin, ports: {Np: Vin, Nn: GND}
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: Vgs, Nn: GND}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: Vgs, Nn: X}
name: X, type: VoltageControlledCurrentSource, value: gmvgs, ports: {Np: X, Nn: GND}
]
extrainfo:The circuit represents a high-frequency small-signal equivalent of a transistor, focusing on its intrinsic speed characteristics. It includes gate-source and gate-drain capacitances (Cgs and Cgd) and a transconductance element (gmvgs).

Fig. 1.27 The circuit used to characterize transistor intrinsic speed: (a) complete circuit; (b) high-frequency small-signal equivalent.
voltages $\mathrm{V}_{\mathrm{GS}}$ and $\mathrm{V}_{\mathrm{DS}}$ are applied to the gate and drain, respectively. A sinusoidal signal, $\mathrm{v}_{\mathrm{in}}$, with very small amplitude is superimposed on the gate voltage. This gives rise to small sinusoidal currents: $\mathrm{i}_{\mathrm{in}}$ which charges and discharges the gate capacitances in response to $v_{i n}$; and $i_{\text {out }}$ which is a small signal current superimposed on the dc drain current, $\mathrm{I}_{\mathrm{D}}$. The unity-gain frequency is defined as the maximum frequency at which the amplitude of the output small-signal current, $\left|\mathrm{i}_{\text {out }}\right|$, exceeds that of the input current, $\left|\mathrm{i}_{\mathrm{in}}\right|$. Although conceptually simple, this measurement is notoriously difficult to perform in the lab since the frequencies involved are high and any parasitic capacitances in the measurement setup will influence the result.

A first-order analytical solution for the transistor $f_{t}$ follows straightforwardly from an analysis of the smallsignal equivalent circuit in Fig. 1.27(b), which is left as an exercise for the reader.

$$
\begin{equation*}
\mathrm{f}_{\mathrm{t}} \approx \frac{\mathrm{~g}_{\mathrm{m}}}{2 \pi\left(\mathrm{C}_{\mathrm{gs}}+\mathrm{C}_{\mathrm{gd}}\right)} \tag{1.116}
\end{equation*}
$$

Although the accuracy of (1.116) is limited, we will adopt this expression as our definition of $f_{t}$ because it is compact and closely related to the bandwidth of many important circuits we shall study.

Clearly, transistor intrinsic speed is dependent on biasing. Substituting (1.74) and (1.89) into (1.116) and assuming $\mathrm{C}_{g s}$ » $\mathrm{C}_{\mathrm{gd}}$ gives the following approximate result for the unity-gain frequency of a transistor:

$$
\begin{equation*}
f_{t} \approx \frac{\mu_{n} C_{o x}(W / L) V_{\text {eff }}}{2 \pi C_{o x} W(2 / 3) L}=\frac{3 \mu_{n} V_{\text {eff }}}{4 \pi L^{2}} \tag{1.117}
\end{equation*}
$$

Key Point: For operation with high gain, transistors should have long gate lengths and be biased with low $\mathrm{V}_{\text {eff }}$ For high speed, the opposite is desirable: small L and high $\mathrm{V}_{\text {eff }}$

As with intrinsic gain, some important fundamental conclusions about analog design are revealed by (1.117). First, for operation at high-speed, device parasitic capacitances should be minimized, which implies minimizing the device gate length, L . Second, speed is maximized by biasing with high values of $\mathrm{V}_{\text {eff }}$. These requirements are in direct conflict with those outlined for maximizing transistor intrinsic gain.

## 1.3 DEVICE MODEL SUMMARY

As a useful aid, all of the equations for the large-signal and small-signal modelling of diodes and MOS transistors, along with values for the various constants, are listed in the next few pages.

### 1.3.1 Constants

| $\mathrm{q}=1.602 \times 10^{-19} \mathrm{C}$ | $\mathrm{k}=1.38 \times 10^{-23} \mathrm{JK}^{-1}$ |
| :--- | :--- |
| $\mathrm{n}_{\mathrm{i}}=1.1 \times 10^{16} \mathrm{carriers} / \mathrm{m}^{3}$ at $\mathrm{T}=300{ }^{\circ} \mathrm{K}$ | $\varepsilon_{0}=8.854 \times 10^{-12} \mathrm{~F} / \mathrm{m}$ |
| $\mathrm{K}_{\mathrm{ox}} \cong 3.9$ | $\mathrm{~K}_{\mathrm{s}} \cong 11.8$ |

### 1.3.2 Diode Equations

#### Reverse-Biased Diode (Abrupt Junction)

| $C_{j}=\frac{C_{j 0}}{\sqrt{1+\frac{V_{B}}{\Phi_{0}}}}$ | $\mathrm{Q}=2 \mathrm{C}_{\mathrm{j} 0} \Phi_{0} \sqrt{1+\frac{\mathrm{V}_{\mathrm{B}}}{\Phi_{0}}}$ |
| :---: | :---: |
| $\mathrm{C}_{\mathrm{j} 0}=\sqrt{\frac{\mathrm{q} \mathrm{K}_{\mathrm{s}} \varepsilon_{0}}{2 \Phi_{0}} \frac{\mathrm{~N}_{\mathrm{D}} \mathrm{N}_{\mathrm{A}}}{\mathrm{N}_{\mathrm{A}}+\mathrm{N}_{\mathrm{D}}}}$ | $\mathrm{C}_{\mathrm{j} 0}=\sqrt{\frac{\mathrm{q} \mathrm{K}_{\mathrm{s}} \varepsilon_{0} \mathrm{~N}_{\mathrm{D}}}{2 \Phi_{0}}}$ if $\mathrm{N}_{\mathrm{A}}>>\mathrm{N}_{\mathrm{D}}$ |
| $\Phi_{0}=\frac{\mathrm{kT}}{\mathrm{q}} \ln \left(\frac{\mathrm{N}_{\mathrm{A}} \mathrm{N}_{\mathrm{D}}}{\mathrm{n}_{\mathrm{i}}^{2}}\right)$ |  |

#### Forward-Biased Diode

$$
\begin{gathered}
\hline I_{D}=I_{S} e^{v_{D} / v_{T}} \quad I_{S}=A_{D} q n_{i}^{2}\left(\frac{D_{n}}{L_{n} N_{A}}+\frac{D_{p}}{L_{p} N_{D}}\right) \\
\hline V_{T}=\frac{k T}{q} \cong 26 \mathrm{mV} \text { at } 300^{\circ} \mathrm{K}
\end{gathered}
$$

Small-Signal Model of Forward-Biased Diode

| $\left\{\begin{array}{l} \text { LOAD } 1 \\ x \end{array}\right.$ |  |
| :---: | :---: |
| $\left.r_{d}\right\} \quad c_{j}$ | $=C_{d}=$ <br> LOAD 2 |
| $r_{d}=\frac{V_{T}}{I_{D}}$ | $\mathrm{C}_{\mathrm{T}}=\mathrm{C}_{\mathrm{d}}+\mathrm{C}_{\mathrm{j}}$ |
| $\mathrm{C}_{\mathrm{d}}=\tau_{\mathrm{T}} \frac{\mathrm{I}_{\mathrm{D}}}{\mathrm{V}_{\mathrm{T}}}$ | $C_{j} \cong 2 C_{j 0}$ |
| $\tau_{T}=\frac{\mathrm{L}_{n}^{2}}{\mathrm{D}_{\mathrm{n}}}$ |  |

### 1.3.3 MOS Transistor Equations

The following equations are for $n$-channel devices-for p -channel devices, put negative signs in front of all voltages. These equations do not account for short-channel effects (i.e., $\mathrm{L}<2 \mathrm{~L}_{\text {min }}$ ).

#### Triode Region ( $V_{G s}>V_{t n}, V_{o s} \leq V_{\text {eff }}$ )

| $\mathrm{I}_{\mathrm{D}}=\mu_{\mathrm{n}} \mathrm{C}_{\text {ox }}\left(\frac{\mathrm{W}}{\mathrm{L}}\right)\left[\left(\mathrm{V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{tn}}\right) \mathrm{V}_{\mathrm{DS}}-\frac{\mathrm{V}_{\mathrm{DS}}^{2}}{2}\right]$ |  |
| :---: | :---: |
| $V_{\text {eff }}=V_{G S}-V_{\text {tn }}$ | $\mathrm{V}_{\mathrm{tn}}=\mathrm{V}_{\mathrm{tn}-0}+\gamma\left(\sqrt{\mathrm{V}_{\mathrm{SB}}+2 \phi_{\mathrm{F}}}-\sqrt{2 \phi_{\mathrm{F}}}\right)$ |
| $\phi_{\mathrm{F}}=\frac{\mathrm{kT}}{\mathrm{q}} \ln \left(\frac{\mathrm{N}_{\mathrm{A}}}{\mathrm{n}_{\mathrm{i}}}\right)$ | image_name:γ = √(2qK_siε_0N_A) / C_ox
description:The image shows a mathematical expression for gamma (γ), which is given by the formula:

\[ \gamma = \frac{\sqrt{2qK_{si}\varepsilon_0N_A}}{C_{ox}} \]

This formula represents the body effect coefficient in semiconductor physics, where:
- \( q \) is the elementary charge,
- \( K_{si} \) is the relative permittivity of silicon,
- \( \varepsilon_0 \) is the permittivity of free space,
- \( N_A \) is the acceptor concentration,
- \( C_{ox} \) is the oxide capacitance per unit area.
|
|  | $\mathrm{C}_{\text {ox }}=\frac{\mathrm{K}_{\mathrm{ox}} \varepsilon_{0}}{\mathrm{t}_{\mathrm{ox}}}$ |

Small-Signal Model in Triode Region (for $V_{D s} \ll V_{\text {eff }}$ )
image_name:Small-Signal Model in Triode Region
description:
[
name: Cgs, type: Capacitor, value: Cgs, ports: {Np: Vg, Nn: Vs}
name: Csb, type: Capacitor, value: Csb, ports: {Np: Vs, Nn: GND}
name: Cgd, type: Capacitor, value: Cgd, ports: {Np: Vg, Nn: Vd}
name: Cdb, type: Capacitor, value: Cdb, ports: {Np: Vd, Nn: GND}
name: rds, type: Resistor, value: rds, ports: {N1: Vs, N2: Vd}
]
extrainfo:This is a small-signal model of a MOSFET in the triode region. The circuit includes capacitors modeling gate-source, gate-drain, source-bulk, and drain-bulk capacitances, along with a resistor modeling the drain-source resistance.

| $r_{d s}=\frac{1}{\mu_{n} C_{o x}\left(\frac{W}{L}\right) V_{\text {eff }}}$ |  |
| :---: | :---: |
|  |  |
| $\mathrm{C}_{\mathrm{gd}}=\mathrm{C}_{\mathrm{gs}} \cong \frac{1}{2} \mathrm{WLC}_{\mathrm{ox}}+\mathrm{WL}_{\mathrm{ov}} \mathrm{C}_{\mathrm{ox}}$ | $C_{s b}=C_{d b}=\frac{C_{j 0}\left(A_{s}+W L / 2\right)}{\sqrt{1+\frac{V_{s b}}{\Phi_{0}}}}$ |

Active (or Pinch-Off) Region ( $V_{G s}>V_{t n}, V_{D s} \geq V_{\text {eff }}$ )

| $\mathrm{I}_{\mathrm{D}}=\frac{1}{2} \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}} \frac{\mathrm{W}}{\mathrm{L}}\left(\mathrm{V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{tn}}\right)^{2}\left[1+\lambda\left(\mathrm{V}_{\mathrm{DS}}-\mathrm{V}_{\mathrm{eff}}\right)\right]$ |
| :---: |
| $\lambda \propto \frac{1}{\mathrm{~L} \sqrt{\mathrm{~V}_{\mathrm{DS}}-\mathrm{V}_{\text {eff }}+\Phi_{0}}} \quad \mathrm{~V}_{\mathrm{tn}}=\mathrm{V}_{\mathrm{tn}-0}+\gamma\left(\sqrt{V_{\mathrm{SB}}+2 \phi_{\mathrm{F}}}-\sqrt{2 \phi_{\mathrm{F}}}\right)$ |
| $\mathrm{V}_{\text {eff }}=\mathrm{V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{tn}}=\sqrt{\frac{2 \mathrm{I}_{\mathrm{D}}}{\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}} \mathrm{W} / \mathrm{L}}}$ |

Small-Signal Model (Active Region)
image_name:Small-Signal Model (Active Region)
description:The circuit is a small-signal model in the active region, featuring capacitors and voltage-controlled current sources. It represents the behavior of a MOSFET with parameters like transconductance (gm) and source conductance (gs). The capacitors model the gate-source, gate-drain, source-bulk, and drain-bulk capacitances.

| $g_{m}=\mu_{n} C_{o x}\left(\frac{W}{L}\right) V_{\text {eff }}$ | $g_{m}=\sqrt{2 \mu_{n} C_{o x}(W / L) I_{D}}$ |
| :---: | :---: |
| $g_{m}=\frac{2 I_{D}}{V_{\text {eff }}}$ | $g_{s}=\frac{\gamma g_{m}}{2 \sqrt{V_{S B}+\left\|2 \phi_{F}\right\|}}$ |
| $r_{d s}=\frac{1}{\lambda I_{D-\text { sat }}} \cong \frac{1}{\lambda I_{D}}$ | $g_{s} \cong 0.2 g_{m}$ |
| $\lambda=\frac{k_{r d s}}{2 L \sqrt{V_{D S}-V_{\text {eff }}+\Phi_{0}}}$ | $\mathrm{k}_{\mathrm{rds}}=\sqrt{\frac{2 \mathrm{~K}_{\mathrm{s}} \varepsilon_{0}}{q N_{A}}}$ |
| $C_{\mathrm{gs}}=\frac{2}{3} \mathrm{WLC}_{\mathrm{ox}}+\mathrm{WL}_{\mathrm{ov}} \mathrm{C}_{\mathrm{ox}}$ | $\mathrm{C}_{\mathrm{gd}}=\mathrm{WL}_{\mathrm{ov}} \mathrm{C}_{\mathrm{ox}}$ |

| $C_{s b}=\left(A_{s}+W L\right) C_{i s}+P_{s} C_{i \cdot s w}$ | $C_{i s}=\frac{C_{j 0}}{\sqrt{1+V_{s B} / \Phi_{0}}}$ |
| :--- | :--- |
| $C_{d b}=A_{d} C_{i d}+P_{d} C_{j-s w}$ | $C_{i d}=\frac{C_{j 0}}{\sqrt{1+V_{D B} / \Phi_{0}}}$ |

## 1.4 ADVANCED MOS MODELLING

The square-law relationship between effective gate-source voltage and drain current expressed in equation (1.67) is only valid for active operation in strong inversion. For very small (and negative) values of $\mathrm{V}_{\text {eff }}$, MOS devices operate in weak inversion, also called subthreshold operation, where an exponential voltage-current relationship holds. For large values of $\mathrm{V}_{\text {eff }}$, a combination of effects give rise to a sub-square-law voltage-current relationship. Both are considered in this section. Other advanced modelling concepts that an analog microcircuit designer is likely to encounter are also covered, including parasitic resistances, short channel effects, and leakage currents.

### 1.4.1 Subthreshold Operation

Key Point: In subthreshold operation, also called weak inversion, transistors obey an exponential voltagecurrent relationship instead of a square-law. Hence, a small but finite current flows even when $\mathrm{V}_{\mathrm{GS}}=0$.

The device equations presented for active or triode region MOS transistors in the preceding sections are all based on the assumption that $\mathrm{V}_{\text {eff }}$ is greater than about 100 mV and the device is in strong inversion. When this is not the case, the accuracy of the square-law equations is poor. For negative values of $\mathrm{V}_{\text {eff }}$, the transistor is in weak inversion and is said to be operating in the subthreshold region. In this regime, the dominant physical mechanism for conduction between drain and source is diffusion, not drift as in strong inversion, and the transistor is more accurately modelled by an exponential relationship between its control voltage (at the gate) and current, somewhat similar to a bipolar transistor. In the subthreshold region, the drain current is approximately given by an exponential relationship.

$$
\begin{equation*}
I_{D(\text { sub -th })} \cong I_{D 0}\left(\frac{W}{L}\right) e^{\left(q V_{e f f} / n k T\right)} \tag{1.118}
\end{equation*}
$$

where

$$
\begin{align*}
\mathrm{n} & =\frac{\mathrm{C}_{\mathrm{ox}}+\mathrm{C}_{\mathrm{j} 0}}{\mathrm{C}_{\mathrm{ox}}} \approx 1.5  \tag{1.119}\\
\mathrm{I}_{\mathrm{D} 0} & =(\mathrm{n}-1) \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{kT}}{\mathrm{q}}\right)^{2} \tag{1.120}
\end{align*}
$$

and it has been assumed that $\mathrm{V}_{\mathrm{S}}=0$ and $\mathrm{V}_{\mathrm{DS}}>75 \mathrm{mV}$. Not captured here is drain-induced barrier lowering, a short-channel effect that causes subthreshold current to also depend on drain-source voltage.

Plotting drain current on a logarithmic axis versus $\mathrm{V}_{\mathrm{GS}}$ in the subthreshold regime gives a straight line. The inverse of this slope, called the subthreshold slope and equal to $\ln (10) \cdot \mathrm{nkT} / \mathrm{q}=2.3 \mathrm{nkT} / \mathrm{q}$, is a measure of the voltage change in $\mathrm{V}_{\mathrm{GS}}$ required to effect an order-of-magnitude change in subthreshold drain current.

Also note that the current does not drop to zero even when $\mathrm{V}_{\mathrm{GS}}=0 \mathrm{~V}$. This residual drain current is called subthreshold leakage and considering equation (1.118) is given by

$$
\begin{equation*}
I_{\text {off }}=I_{D o}\left(\frac{W}{L}\right) e^{\left(-q V_{t} / n k T\right)}=(n-1) \mu_{n} C_{o x}\left(\frac{W}{L}\right)\left(\frac{k T}{q}\right)^{2} e^{\left(-q V_{t} / n k T\right)} \tag{1.121}
\end{equation*}
$$

Equation (1.121) reveals a complex temperature dependence due to the explicit inclusion of absolute temperature ( $T$ ), and due to the temperature dependence of carrier mobility $\left(\mu_{n}\right)$ and threshold voltage $\left(\mathrm{V}_{\mathrm{t}}\right)$. In general, subthreshold leakage increases significantly with temperature and is often a dominant source of power consumption in analog circuits that are temporarily powered down or in standby.

#### EXAMPLE 1.16

A transistor has a subthreshold leakage current of $\mathrm{I}_{\text {off }}=10 \mathrm{nA}$ at 300 K . How much must $\mathrm{V}_{\text {eff }}$ decrease to reduce $\mathrm{I}_{\text {off }}$ to 1 nA ?

#### Solution

From (1.118), it is evident that to decrease subthreshold drain current by a factor of 10 requires that $\mathrm{V}_{\text {eff }}$ decrease by $\ln (10) \cdot \mathrm{nkT} / \mathrm{q} \cong 90 \mathrm{mV}$ at room temperature. This can be achieved either by decreasing $\mathrm{V}_{\mathrm{GS}}$, or increasing $\mathrm{V}_{\mathrm{tn}}$.

The transconductance of a transistor in the subthreshold region is determined by taking the derivative of (1.118) with respect to $\mathrm{V}_{\mathrm{GS}}$ resulting in

$$
\begin{equation*}
g_{m(\text { sub -th })}=\left(\frac{q}{n k T}\right) I{ }_{D 0}\left(\frac{W}{L}\right) e^{\left(q V_{\text {eff }} / n k T\right)}=\frac{q l_{D}}{n k T} \tag{1.122}
\end{equation*}
$$

Note that for fixed drain current, $\mathrm{I}_{\mathrm{D}}$, the transconductance in subthreshold is independent of $\mathrm{V}_{\text {eff }}$. Normalizing the transconductance with respect to the drain current yields a constant value in subthreshold,

$$
\begin{equation*}
\frac{g_{m(\text { sub-th })}}{I_{D(\text { sub-th })}}=\frac{q}{n k T} \tag{1.123}
\end{equation*}
$$

As $\mathrm{V}_{\mathrm{Gs}}$ is increased well beyond $\mathrm{V}_{\mathrm{t}}$, the MOS device enters strong inversion and the transconductance then decreases in inverse proportion to $\mathrm{V}_{\text {eff }}$, as indicated by (1.78). Hence, for a fixed drain current, transconductance of a MOS device is maximized in the subthreshold region with the value given in (1.122). In other words, a targeted value of transconductance can be achieved with less drain current in the subthreshold region than in strong inversion. However, to achieve prac-

Key Point: For a fixed drain current, the smallsignal transconductance of a MOSdevice is maximized in subthreshold operation at a value of $\mathrm{g}_{\mathrm{m}}=\mathrm{qI}_{\mathrm{D}} / \mathrm{nkT}$.
tically useful values of transconductance in the subthreshold region requires a transistor with a very large aspect ratio, $\mathrm{W} / \mathrm{L}$. Such large aspect ratios generally imply large parasitic capacitances making very high-speed operation difficult. Therefore, subthreshold operation is useful primarily when speed can be sacrificed for lower drain currents and, hence, generally lower power consumption.

The transition between subthreshold and strong inversion is not abrupt. For a broad range of gate-source voltages, both diffusion and drift currents with comparable magnitudes exist making accurate device modeling in this region notoriously difficult. This is generally referred to as moderate inversion. To get a feel for what gate-source voltages imply moderate inversion, equate the expressions for $g_{m}$ in active mode (1.78) and $g_{m(\text { sub - th })}$ (1.122) and solve for $\mathrm{V}_{\text {eff }}$ resulting in

$$
\begin{equation*}
V_{\text {eff }}=\frac{2 n k T}{q} \tag{1.124}
\end{equation*}
$$

At room temperature and assuming $n \approx 1.5$, moderate inversion occurs around $V_{\text {eff }} \approx 75 \mathrm{mV}$, increasing to approximately 90 mV at 350 K . Hence, to ensure operation in strong inversion, prudent designers generally take $V_{\text {eff }}>100 \mathrm{mV}$.

#### EXAMPLE 1.17

Estimate the value of n from the data for the NMOS device in Example 1.9 at $\mathrm{T}=300 \mathrm{~K}$.

#### Solution

The logarithmic plot of $\mathrm{I}_{\mathrm{D}}$ versus $\mathrm{V}_{\mathrm{GS}}$ in Fig. 1.28(a) has a slope equal to ( 2.3 nkT )/q which in this case can be used to estimate n . The dashed line shows a reasonable fit with $\mathrm{n}=1.6$. This estimate can be confirmed by looking at the plot of $\mathrm{g}_{\mathrm{m}} / \mathrm{I}_{\mathrm{D}}$ also on Fig. $1.28(\mathrm{~b})$, which should reach a maximum of $\mathrm{q} / \mathrm{nkT}$ in subthreshold. Again, the dashed line with $\mathrm{n}=1.6$ is a reasonable approximation. Also shown on that plot is the result for the squarelaw model based on (1.78) based on the threshold voltage of $\mathrm{V}_{\mathrm{tn}} \cong 0.45 \mathrm{~V}$ obtained in Example 1.9. Note that the two regions intersect at $\mathrm{V}_{\mathrm{GS}}=\mathrm{V}_{\mathrm{tn}}+2 \mathrm{nkT} / \mathrm{q}$.

### 1.4.2 Mobility Degradation

Transistors subjected to large electric fields experience a degradation in the effective mobility of their carriers. Large lateral electric fields, as shown in Fig. 1.29 for an NMOS device, accelerate carriers in the channel up to a
image_name:(a)
description:The graph labeled (a) is a plot of the drain current, \( I_D \), versus the gate-to-source voltage, \( V_{GS} \), for a MOS device in the subthreshold region.

1. **Type of Graph and Function:**
- This is a semilogarithmic plot, where the y-axis (\( I_D \)) is on a logarithmic scale, and the x-axis (\( V_{GS} \)) is on a linear scale.

2. **Axes Labels and Units:**
- The x-axis is labeled \( V_{GS} \) in volts (V), ranging from 0 to 0.6 V.
- The y-axis is labeled \( I_D \) in amperes (A), ranging from \( 10^{-8} \) A to \( 10^{-2} \) A.

3. **Overall Behavior and Trends:**
- The graph shows an exponential increase in the drain current \( I_D \) with increasing \( V_{GS} \). This behavior is typical in the subthreshold region of a MOSFET, where the current increases exponentially with the gate voltage.

4. **Key Features and Technical Details:**
- The plot includes a line with a slope corresponding to \( \frac{q}{2.3n kT} \), indicating the subthreshold slope, a critical parameter in MOSFET operation.
- The linear fit (dashed line) closely follows the data points (marked by diamonds), highlighting the exponential relationship between \( I_D \) and \( V_{GS} \) in this region.

5. **Annotations and Specific Data Points:**
- The graph includes an annotation indicating the slope \( \frac{q}{2.3n kT} \), which is a measure of the subthreshold slope. This is a key parameter for determining the efficiency and switching speed of the transistor.
- No specific numerical values for key data points are provided, but the graph visually demonstrates the exponential trend in the subthreshold region.
image_name:(b)
description:The graph labeled (b) in the image is a plot showing the relationship between the gate-source voltage (V_GS) and the transconductance-to-drain current ratio (g_m/I_D) for a MOS device. The graph is used to illustrate mobility degradation effects in the subthreshold region.

1. **Type of Graph and Function:**
- The graph is a plot of transconductance efficiency (g_m/I_D) versus gate-source voltage (V_GS).

2. **Axes Labels and Units:**
- The x-axis represents the gate-source voltage (V_GS) in volts (V), ranging from 0 to 1 V.
- The y-axis represents the transconductance-to-drain current ratio (g_m/I_D) in inverse volts (V^{-1}), ranging from 0 to 30 V^{-1}.

3. **Overall Behavior and Trends:**
- The plot shows two distinct regions: a horizontal dashed line representing the theoretical value q/nkT and a decreasing curve labeled "Square law g_m/I_D = 2/V_eff".
- The g_m/I_D ratio initially follows the horizontal line, indicating a constant value, and then transitions to a decreasing trend following the square-law behavior.

4. **Key Features and Technical Details:**
- The intersection point between the horizontal line and the decreasing curve is marked and annotated as "Intersection at V_eff = 2nkT/q".
- The transition from the constant region to the square-law region occurs around V_GS = 0.45 V, which corresponds to the threshold voltage plus an additional term (2nkT/q).

5. **Annotations and Specific Data Points:**
- The graph includes a dashed line representing the theoretical value (q/nkT) and a curved line representing the square-law behavior (2/V_eff).
- The intersection point is highlighted as a critical value where the behavior of the device changes from subthreshold to above-threshold operation.

Fig. 1.28 Drain current and transconductance of a MOS device in subthreshold.
maximum velocity, approximately $10^{7} \mathrm{~cm} / \mathrm{s}$ in silicon. This is referred to as velocity saturation. Vertical electric fields greater than approximately $5 \cdot 10^{6} \mathrm{~V} / \mathrm{m}$ cause the effective channel depth to decrease and also cause more charge-carrier collisions.

For the purposes of design, these effects may be modeled together by an effective carrier mobility that decreases at high $\mathrm{V}_{\text {eff }}$,

$$
\begin{equation*}
\mu_{\mathrm{n}, \mathrm{eff}} \cong \frac{\mu_{\mathrm{n}}}{\left(\left[1+\left(\theta \mathrm{V}_{\mathrm{eff}}\right)^{\mathrm{m}}\right]\right)^{1 / \mathrm{m}}} \tag{1.125}
\end{equation*}
$$

where $\theta$ and $m$ are device parameters. Substituting the effective carrier mobility, $\mu_{n, \text { eff }}$, from (1.125) in place of $\mu_{\mathrm{n}}$ in equation (1.72) gives a new expression for the drain current incorporating mobility degradation.

$$
\begin{equation*}
I_{D}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L} V_{\text {eff }}^{2}\left(\frac{1}{\left[1+\left(\theta V_{\text {eff }}\right)^{m}\right]^{1 / m}}\right) \tag{1.126}
\end{equation*}
$$

For small values of $\mathrm{V}_{\text {eft }}$, the final term in equation (1.126) approaches unity and the entire expression simplifies to the square-law relationship in (1.72). For values of $\mathrm{V}_{\text {eff }} \gg 1 / \theta$, the final term in (1.126) approaches $\left(1 / \theta \mathrm{V}_{\text {eff }}\right)$ resulting in a linear relationship between effective gate-source voltage and current. Taking the derivative of (1.126) with respect to gate-source voltage assuming large $\mathrm{V}_{\text {eff }}$ gives a small-signal transconductance that is independent of drain current,

$$
\begin{equation*}
g_{m(\text { mob-deg })}=\frac{1}{2} \mu_{\mathrm{n}} C_{o x} \frac{\mathrm{~W}}{\mathrm{~L}} \frac{1}{\theta} \tag{1.127}
\end{equation*}
$$

Equation (1.127) establishes the maximum transconductance achievable with a given transistor. A square-law model for transconductance (1.73) predicts a transconductance equal to (1.127) when $\mathrm{V}_{\text {eff }}=1 / 2 \theta$. Due to mobility degradation, increases in $\mathrm{V}_{\text {eff }}$ beyond 1/20:

- fail to provide significant increases in small-signal transconductance,
- reduce the available signal swing limited by the fixed supply voltages, and
- reduce transistor intrinsic gain $A_{i}$ dramatically
image_name:Fig. 1.29
description:The diagram in Fig. 1.29 illustrates an NMOS transistor in active mode, also known as saturation mode. It highlights the lateral and vertical electric field components within the device.

1. **Identification of Components and Structure:**
- The NMOS device is shown with its typical structure, including the source (S), gate (G), and drain (D) terminals, which are labeled as $V_S$, $V_G$, and $V_D$, respectively.
- The source and drain regions are depicted as highly doped n+ regions, indicating that they are heavily doped with donor impurities to form the n-type regions essential for NMOS operation.
- The gate is positioned above the channel region and is separated by a thin insulating layer, typically made of silicon dioxide.

2. **Connections and Interactions:**
- The diagram shows the flow of electrons from the source to the drain, controlled by the gate voltage $V_G$.
- The vertical electric field is indicated with downward arrows, showing the influence of the gate voltage in attracting electrons towards the channel.
- The lateral electric field is depicted with a horizontal arrow pointing from the source to the drain, representing the electric field that drives the electron flow across the channel.

3. **Labels, Annotations, and Key Features:**
- "Vertical Electric Field" is labeled with arrows pointing downwards, indicating the field due to the gate voltage that affects the channel charge.
- "Lateral Electric Field" is labeled with an arrow pointing from left to right, illustrating the field responsible for carrier transport from source to drain.
- The n+ regions are labeled, emphasizing their role as the source and drain contacts.

This diagram effectively illustrates the electric fields in an NMOS transistor, crucial for understanding its operation in saturation mode, where the drain current is primarily controlled by the gate voltage.

Lateral Electric Field
image_name:Fig. 1.29 An NMOS device in active mode
description:The image contains a depiction of a ground symbol labeled 'GND'. This is a common reference point in circuits, typically used as a return path for current and a stable reference voltage.

Fig. 1.29 An NMOS device in active mode (saturation) identifying the lateral and vertical electric field components.

For these reasons, operation under mobility degradation is generally avoided in analog design, although this is becoming increasingly difficult in modern CMOS processes. Transistors are, however, sometimes biased with $\mathrm{V}_{\text {eff }}>1 / 2 \theta$ when their size must be limited. For example, when very-high frequency operation is sought, parasitic capacitances must be minimized by keeping all transistor dimensions as small as possible.

Key Point: For large values of $\mathrm{V}_{\text {eff }}$, transistors have a sub-square-law voltage current relationship, tending towards a linear relationship for very large values of $\mathrm{V}_{\mathrm{eff}}$

For operating conditions around $\mathrm{V}_{\text {eff }} \approx 1 / 2 \theta$, more sophisticated modeling is required to obtain high accuracy [Sodini, 1984]. However, a piecewise-linear assumption whereby (1.73) is applied when $\mathrm{V}_{\text {eff }}<1 / 2 \theta$ and (1.127) when $\mathrm{V}_{\text {eff }}>1 / 2 \theta$ is often sufficient for first pass design.

In the past, mobility degradation appeared only at extremely large values of $\mathrm{V}_{\text {eff }}$, but this is no longer always the case. Shrinking MOS device dimensions have meant that lower voltages are required to generate the critical electric fields. The value of $\theta$ increases from around $0.06 \mathrm{~V}^{-1}$ for a $0.8-\mu \mathrm{m}$-long transistor in a $0.8-\mu \mathrm{m}$ CMOS process, to greater than $2 \mathrm{~V}^{-1}$ for minimum-sized devices in modern CMOS processes. Hence, mobility degradation can appear at $\mathrm{V}_{\text {eff }}$ values of only a few hundred mV . Since (1.124) places a fundamental lower limit of $\mathrm{V}_{\text {eff }}>100 \mathrm{mV}$ to ensure operation in strong inversion there remains only a narrow range of effective gate-source voltages for which the square-law voltage-current relationship expressed in (1.72) remains valid in nanoscale CMOS devices. In many voltage-to-current conversion circuits that rely on the square-law characteristic, this inaccuracy can be a major source of error. Taking channel lengths larger than the minimum allowed helps to minimize this degradation.

#### EXAMPLE 1.18

Estimate the value of $\theta$ based on the data in Fig. 1.30.

#### Solution

Mobility degradation is evident at high values of $\mathrm{V}_{\text {eff }}$ where the drain current in Fig. 1.30(a) is clearly subquadratic. An estimate of $\theta$ is more easily obtained from the plot of $g_{m}$ versus $V_{G s}$ in Fig. 1.30(b). The value of $\mathrm{V}_{\text {eff }}$ at which the transconductance ceases to follow a linear relationship is approximately $1 / 2 \theta$. In this case, this
image_name:Fig. 1.30(a)
description:The graph in Fig. 1.30(a) is a plot of drain current ($I_D$) versus gate-source voltage ($V_{GS}$) for a MOS device. The x-axis represents $V_{GS}$ in volts (V), ranging from 0 to 1.2 V, while the y-axis represents the drain current $I_D$ in amperes (A), ranging from 0 to 0.8 A. The graph uses a linear scale on both axes.

The graph shows the behavior of the drain current as a function of the gate-source voltage. Initially, for $V_{GS}$ less than approximately 0.6 V, the drain current remains close to zero, indicating the device is off or in a subthreshold region. As $V_{GS}$ increases beyond 0.6 V, the drain current begins to rise, following a subquadratic trend at higher values of $V_{GS}$, deviating from the ideal square law model indicated by the dashed line. This deviation is due to mobility degradation at high effective voltages ($V_{eff}$).

Key features include the point where the actual curve diverges from the square law model, highlighting the onset of mobility degradation. The graph emphasizes that the drain current becomes subquadratic at high $V_{GS}$ values, indicating non-ideal behavior in the MOS device.
image_name:Fig. 1.30(b)
description:The graph in Fig. 1.30(b) is a plot of transconductance (g_m) versus gate-source voltage (V_GS) for a MOS device. The horizontal axis represents V_GS in volts (V), ranging from 0 to 1.2 V. The vertical axis represents the transconductance g_m in milliamps per volt (mA/V), ranging from 0 to 1 mA/V.

The graph shows a clear trend where the transconductance initially increases linearly with V_GS and then begins to deviate from this linearity as V_GS increases further. This deviation indicates mobility degradation at higher V_GS values. The transition point where g_m ceases to follow a linear relationship is marked on the graph at approximately V_GS = 0.75 V, corresponding to V_eff = 0.3 V.

A horizontal dashed line is drawn at g_m = μ_nC_ox(W/L)(1/2θ), illustrating the expected transconductance level based on the given formula. The intersection of the g_m curve with this line occurs at V_eff = 1/2θ, which is used to estimate the parameter θ. This intersection is annotated on the graph, and the estimated value of θ is approximately 1.7 V^-1.

Overall, the graph effectively demonstrates the behavior of transconductance in relation to gate-source voltage, highlighting the impact of mobility degradation at higher voltages.

Fig. 1.30 Drain current and transconductance of a MOS device in at large values of $\mathrm{V}_{\text {eff }}$.
occurs at approximately $\mathrm{V}_{\mathrm{GS}}=0.75 \mathrm{~V}$ or $\mathrm{V}_{\text {eff }}=0.3 \mathrm{~V}$, corresponding to $\theta \cong 1.7 \mathrm{~V}^{-1}$. At $\mathrm{V}_{\text {eff }}>0.3 \mathrm{~V}$, the constant $\mu_{n} C_{o x}(W / L)(1 / 2 \theta) \quad$ can be used as a rough estimate of $g_{m}$. More accuracy is provided using the model of (1.126) with, in this case, a value $\mathrm{m}=1.6$ resulting in the dotted line on Fig. 1.30(b).

### 1.4.3 Summary of Subthreshold and Mobility Degradation Equations

The key expressions for operation in subthreshold, stronginversion, and mobility degradation are summarized in Table 1.1 and the progression of transistor drain current and smallsignal transconductance as its gate-source voltage is swept is sketched in Fig. 1.31. Transition regions appear at the borders between these operating modes where the voltage-current relationship and small-signal transconductance are compromises between the expressions in the table. Generally, operation in or near subthreshold is considered only for analog circuits where low-power but low-speed operation is required. Operation under mobility degradation is necessary only when very highspeed is required, thus demanding minimal parasitic capacitances and, hence, low device aspect ratios.

### 1.4.4 Parasitic Resistances

Parasitic resistance appears in series with all four MOSFET terminals. The resistance of the polysilicon gate carries no dc current, but may be significant in small-signal analysis since it is in series with the gate-source capacitance, $\mathrm{C}_{\mathrm{gs}}$. Contacts to the drain and source region are resistive and may have significant voltage drops across them when carrying large currents. Additionally, in modern CMOS processes, the drain
image_name:Fig. 1.31
description:The graph in Fig. 1.31 illustrates the progression of transistor drain current (I_D) and small-signal transconductance (g_m) as a function of the gate-source voltage (V_GS). The graph is divided into three distinct regions: subthreshold, square law, and mobility degradation.

1. **Type of Graph and Function:**
- The graph is a plot showing the relationship of drain current (I_D) and transconductance (g_m) with respect to gate-source voltage (V_GS).

2. **Axes Labels and Units:**
- The x-axis represents the gate-source voltage (V_GS), while the y-axes represent the drain current (I_D) in the upper graph and the transconductance (g_m = dI_D/dV_GS) in the lower graph.
- There are no specific units provided, but these typically would be volts for V_GS and amperes for I_D.

3. **Overall Behavior and Trends:**
- **Drain Current (I_D):**
- In the subthreshold region, the drain current is very low and increases exponentially with V_GS.
- In the square law region, the current increases more steeply, following a parabolic curve.
- In the mobility degradation region, the rate of increase in current diminishes, showing a saturation trend.
- **Transconductance (g_m):**
- In the subthreshold region, g_m increases gradually.
- In the square law region, it shows a rapid increase and then begins to level off.
- In the mobility degradation region, g_m reaches a maximum and then starts to decrease.

4. **Key Features and Technical Details:**
- The transition point between subthreshold and square law regions is marked by the threshold voltage (V_t).
- The graph shows a clear distinction between the three operational regions of a MOSFET.
- The trends illustrate the impact of V_GS on both I_D and g_m, highlighting the operational characteristics of MOSFETs.

5. **Annotations and Specific Data Points:**
- The graph is annotated with dashed vertical lines to demarcate the boundaries between subthreshold, square law, and mobility degradation regions.
- The threshold voltage (V_t) is indicated on the V_GS axis, marking the transition from subthreshold to square law behavior.

Fig. 1.31 The progression of transistor drain current and small-signal transconductance from subthreshold to square law to mobility degradation.

Table 1.1 A summary of MOS device operation in the subthreshold, strong inversion, and mobility degradation regions.

|  | Subthreshold (exponential) | Strong Inversion (square-law) | Mobility Degradation (linear) |
| :---: | :---: | :---: | :---: |
| Region of validity | $V_{\text {eff }} \lesssim 0$ | $\frac{2 n k T}{q}<V_{\text {eff }}<\frac{1}{2 \theta}$ | $V_{\text {eff }}>\frac{1}{2 \theta}$ |
| Drain current, $\mathrm{I}_{\mathrm{D}}$ | $I_{D 0}\left(\frac{W}{L}\right) e^{\left(q V_{\text {eff }} / n \mathrm{TT}\right)}$ | $\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L} V_{\text {eff }}^{2}$ | $\frac{0.5 \mu_{n} C_{o x}(W / L) V_{\text {eff }}^{2}}{\left[1+\left(\theta V_{\text {eff }}\right)^{m}\right]^{1 / m}}$ |
| Small-signal transconductance, $\mathrm{g}_{\mathrm{m}}$ | $\frac{q l_{D}}{n k T}$ | $\frac{2 I_{D}}{V_{\text {eff }}}=\mu_{n} C_{o x} \frac{W}{L} V_{\text {eff }}$ | $\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L} \frac{1}{\theta}$ |
| Most useful | Very low-power operation | Most analog design | Very high-speed operation |

and source regions themselves are engineered to have a very shallow depth near the channel region. These shallow source and drain extensions present a narrow cross-sectional area through which all channel current must flow resulting in significant series resistance. Finally, the body terminal is relatively lightly doped semiconductor and, hence, may impose a significant series resistance. All of these parasitics are generally on the order of a few Ohms, and hence are only considered when they are conducting very large currents, or at very high frequencies where the resistances combine with transistor parasitic capacitances to form small-signal poles of significance. Furthermore, they can often be minimized by proper design (for example, by providing additional contacts). They are considered negligible throughout the remainder of the text.

### 1.4.5 Short-Channel Effects

A number of short-channel effects degrade the operation of MOS transistors as device dimensions are scaled down. These effects include reduced output impedance and hot-carrier effects (such as oxide trapping and substrate currents). These short-channel effects will be briefly described here. For more detailed modelling of shortchannel effects, see [Wolf, 1995].

Transistors with short channel lengths experience a reduced output impedance because depletion region variations at the drain end (which affect the effective channel length) have an increased proportional effect on the drain current. In addition, a phenomenon known as drain-induced barrier lowering (DIBL) effectively lowers $\mathrm{V}_{\mathrm{t}}$ as $\mathrm{V}_{\mathrm{DS}}$ is increased, thereby further lowering the output impedance of a short-channel device.

Another important short-channel effect is due to hot carriers. These high-velocity carriers can cause harmful effects, such as the generation of electron-hole pairs by impact ionization and avalanching. These extra electronhole pairs can cause currents to flow from the drain to the substrate, as shown in Fig. 1.32. This effect can be modelled by a finite drain-to-ground impedance. As a result, this effect is one of the major limitations on achieving very high output impedances of cascode current sources. In addition, this current flow can cause voltage drops across the substrate and possibly cause latch-up, as the next chapter describes.

Another hot-carrier effect occurs when electrons gain energies high enough to tunnel into and possibly through the thin gate oxide. Thus, this effect can cause dc gate currents. However, often more harmful is the fact that any charge trapped in the oxide will cause a shift in transistor threshold voltage. As a result, hot carriers are one of the major factors limiting the long-term reliability of MOS transistors.
image_name:Fig. 1.32
description:The diagram, labeled as Fig. 1.32, illustrates the hot carrier effects in an n-channel MOS (Metal-Oxide-Semiconductor) transistor. The main components visible in the diagram include the source and drain regions, both marked as n+ to indicate heavily doped n-type semiconductor material. The gate is shown above the channel, separated by an oxide layer, and is connected to a voltage source labeled \( V_G >> V_{tn} \), where \( V_{tn} \) is the threshold voltage.

The diagram highlights several currents and effects:

1. **Gate Current:** There is a depiction of a gate current flowing through the thin gate oxide, indicated by an arrow pointing downward into the gate. This is caused by electrons gaining enough energy to tunnel through the oxide.

2. **Punch-through Current:** An arrow labeled as punch-through current shows electrons with sufficient energy moving directly from the source to the drain, bypassing the normal channel conduction.

3. **Drain-to-Substrate Current:** Another arrow indicates a drain-to-substrate current, which is caused by electron-hole pairs generated by impact ionization at the drain end of the channel. This current flows from the drain into the substrate, depicted by arrows pointing downward.

The substrate is connected to ground (GND), and there are annotations indicating that the drain voltage \( V_D >> 0 \) is significantly positive compared to the source, which is grounded. These annotations and arrows effectively illustrate the flow of high-energy electrons and the resultant currents due to hot carrier effects in the transistor.

Fig. 1.32 An illustration of hot carrier effects in an n-channel MOS transistor. Drain-to-substrate current is caused by electron-hole pairs generated by impact ionization at the drain end of the channel.

A third hot-carrier effect occurs when electrons with enough energy punch through from the source to the drain. As a result, these high-energy electrons are no longer limited by the drift equations governing normal conduction along the channel. This mechanism is somewhat similar to punch-through in a bipolar transistor, where the collector depletion region extends right through the base region to the emitter. In a MOS transistor, the channel length becomes effectively zero, resulting in unlimited current flow (except for the series source and drain impedances, as well as external circuitry). This effect is an additional cause of lower output impedance and possibly transistor breakdown.

All of the hot-carrier effects just described are more pronounced for n -channel transistors than for their p -channel counterparts because electrons have larger velocities than holes.

### 1.4.6 Leakage Currents

Leakage currents impose limitations on how long a dynamically charged signal can be maintained in a high impedance state, and on the minimum power consumption achievable when an analog circuit is in an idle (powerdown) state. Three leakage currents are important in MOS transistors: subthreshold leakage, gate leakage, and junction leakage. Of these, subthreshold leakage is often the largest. It results in a finite drain current even when the transistor is off, and was described in detail in section 1.4.1. Gate leakage results from quantum-mechanical tunneling of electrons through very thin gate oxides, and can be significant in digital circuits and when large gate areas are used, for example to implement a capacitor. Finally, the reverse-biased source-body and drain-body pn junctions conduct a finite leakage current. This leakage can be important, for example, in estimating the maximum time a sample-and-hold circuit or a dynamic memory cell can be left in hold mode. The leakage current of a reverse-biased junction (not close to breakdown) is approximately given by
where $A_{j}$ is the junction area, $n_{i}$ is the intrinsic concentration of carriers in undoped silicon, $\tau_{0}$ is the effective minority carrier lifetime, $\mathbf{X}_{\mathrm{d}}$ is the thickness of the depletion region, and $\tau_{0}$ is given by

$$
\begin{equation*}
\tau_{0} \cong \frac{1}{2}\left(\tau_{n}+\tau_{p}\right) \tag{1.129}
\end{equation*}
$$

where $\tau_{n}$ and $\tau_{p}$ are the electron and hole lifetimes. Also, $\mathbf{x}_{\mathrm{d}}$ is given by

$$
\begin{equation*}
\mathrm{x}_{\mathrm{d}}=\sqrt{\frac{2 \mathrm{~K}_{\mathrm{s}} \varepsilon_{0}}{\mathrm{qN}}\left(\Phi_{\mathrm{A}}+\mathrm{V}_{\mathrm{r}}\right)} \tag{1.130}
\end{equation*}
$$

and $\mathrm{n}_{\mathrm{i}}$ is given by

$$
\begin{equation*}
\mathrm{n}_{\mathrm{i}} \cong \sqrt{\mathrm{~N}_{\mathrm{C}} \mathrm{~N}_{\mathrm{V}}} \mathrm{e}^{\left(-\mathrm{E}_{\mathrm{g}}\right) /(\mathrm{KT})} \tag{1.131}
\end{equation*}
$$

where $N_{C}$ and $N_{V}$ are the densities of states in the conduction and valence bands and $E_{g}$ is the difference in energy between the two bands.

Since the intrinsic concentration, $\mathrm{n}_{\mathrm{i}}$, is a strong function of temperature (it approximately doubles for every temperature increase of $11^{\circ} \mathrm{C}$ for silicon), the leakage current is also a strong function of temperature. The leakage current roughly doubles for every $11^{\circ} \mathrm{C}$ rise in temperature; thus, at higher temperatures it is much larger than at room temperature.

## 1.5 SPICE MODELLING PARAMETERS

This section briefly describes some of the important model parameters for diodes and MOS transistors used during a SPICE simulation. It should be noted here that not all SPICE model parameters are described. However, enough are described to enable the reader to understand the relationship between the relative parameters and the corresponding constants used when doing hand analysis.

### 1.5.1 Diode Model

There are a number of important dc parameters. The constant $\mathrm{I}_{\mathrm{S}}$ is specified using either the parameter IS or JS in SPICE. These two parameters are synonyms, and only one should be specified. A typical value specified for $\mathrm{I}_{\mathrm{S}}$ might be between $10^{-18} \mathrm{~A}$ and $10^{-15} \mathrm{~A}$ for small diodes in a microcircuit. Another important parameter is called the emission coefficient, $\mathrm{n}_{\mathrm{j}}$. This constant multiplies $\mathrm{V}_{\mathrm{T}}$ in the exponential diode I-V relationship given by

$$
\begin{equation*}
I_{D}=I_{S} e^{V_{B E} /\left(n_{i} V_{T}\right)} \tag{1.132}
\end{equation*}
$$

The SPICE parameter for $\mathrm{n}_{\mathrm{j}}$ is N and is defaulted to 1 when not specified ( 1 is a reasonable value for junctions in an integrated circuit). A third important dc characteristic is the series resistance, which is specified in SPICE using RS. It should be noted here that some SPICE programs allow the user to specify the area of the diode, whereas others expect absolute parameters that already take into account the effective area. The manual for the program being used should be consulted.

The diode transit time is specified using the SPICE parameter TT. The most important capacitance parameter specified is CJ. CJO and CJ are synonyms - one should never specify both. This parameter specifies the capacitance at $0-\mathrm{V}$ bias. Once again, it may be specified as absolute or as relative to the area (i.e., $\mathrm{F} / \mathrm{m}^{2}$ ), depending on the version of SPICE used. Also, the area junction grading coefficient, MJ, might be specified to determine the exponent used in the capacitance equation. Typical values are 0.5 for abrupt junctions and 0.33 for graded junctions. In some SPICE versions, it might also be possible to specify the sidewall capacitance at 0 -V bias as well as its grading junction coefficient. Finally, the built-in potential of the junction, which is also used in calculating the capacitance, can be specified using PB. PHI, VJ, and PHA are all synonyms of PB.

Reasonably accurate diode simulations can usually be obtained by specifying only IS, CJ, MJ, and PB. However, most modern versions of SPICE have many more parameters that can be specified if one wants accurate temperature and noise simulations. Users should consult their manuals for more information.

Table 1.2 summarizes some of the more important diode parameters. This set of parameters constitutes a minimal set for reasonable simulation accuracy under ordinary conditions.

Table 1.2 Important SPICE parameters for modelling diodes.

| SPICE <br> Parameter | Model <br> Constant | Brief Description | Typical Value |
| :--- | :--- | :--- | :--- |
| IS | $\mathrm{I}_{\mathrm{S}}$ | Transport saturation current | $10^{-17} \mathrm{~A}$ |
| RS | $\mathrm{R}_{\mathrm{d}}$ | Series resistance | $30 \Omega$ |
| TT | $\tau_{\mathrm{T}}$ | Diode transit time | 12 ps |
| CJ | $\mathrm{C}_{\mathrm{j} 0}$ | Capacitance at 0-V bias | 0.01 pF |
| MJ | $\mathrm{m}_{\mathrm{j}}$ | Diode grading coefficient exponent | 0.5 |
| PB | $\Phi_{0}$ | Built-in diode contact potential | 0.9 V |

### 1.5.2 MOS Transistors

Modern MOS models are quite complicated, so only some of the more important MOS parameters used in SPICE simulations are described here. These parameters are used in what are called the Level 2 or Level 3 models. The model level can be chosen by setting the SPICE parameter LEVEL to either 2 or 3 . The oxide thickness, $\mathrm{t}_{\mathrm{ox}}$, is specified using the SPICE parameter TOX. If it is specified, then it is not necessary to specify the thin gate-oxide capacitance ( $\mathrm{C}_{\mathrm{ox}}$, specified by parameter COX). The mobility, $\mu_{n}$, can be specified using UO. If UO is specified, the intrinsic transistor conductance ( $\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}$ ) will be calculated automatically, unless this automatic calculation is overridden by specifying either KP (or its synonym, BETA). The transistor threshold voltage at $\mathrm{V}_{\mathrm{S}}=0 \mathrm{~V}, \mathrm{~V}_{\mathrm{tn}}$, is specified by VTO. The body-effect parameter, $\gamma$, can be specified using GAMMA, or it will be automatically calculated if the substrate doping, $\mathrm{N}_{\mathrm{A}}$, is specified using NSUB. Normally, one would not want SPICE to calculate $\gamma$ because the effective substrate doping under the channel can differ significantly from the substrate doping in the bulk due to threshold-voltage adjust implants. The output impedance constant, $\lambda$, can be specified using LAMBDA. Normally, LAMBDA should not be specified since it takes precedence over internal calculations and does not change the output impedance as a function of different transistor lengths or bias voltages (which should be the case). Indeed, modelling the transistor output impedance is one of weakest points in SPICE. If LAMBDA is not specified, it is calculated automatically. The surface inversion potential, $\left|2 \phi_{F}\right|$, can be specified using PHI, or it will be calculated automatically. Another parameter usually specified is the lateral diffusion of the junctions under the gate, $L_{D}$, which is specified by LD. For accurate simulations, one might also specify the resistances in series with the source and drain by specifying RS and RD (typically only the source resistance is important). Many other parameters exist to model such things as short-channel effects, subthreshold effects, and channel-width effects, but these parameters are outside the scope of this book.

The modelling of parasitic capacitances in SPICE is quite involved. The capacitances under the junctions per unit area at $0-\mathrm{V}$ bias, (i.e., $\mathrm{C}_{\mathrm{j} 0}$ ) can be specified using CJ or can be calculated automatically from the specified substrate doping. The sidewall capacitances at $0 \mathrm{~V}, \mathrm{C}_{\mathrm{j} \text {-sw0 }}$, should normally be specified using CJSW because this parameter is used to calculate significant parasitic capacitances. The bulk grading coefficient specified by MJ can usually be defaulted to 0.5 . Similarly, the sidewall grading coefficient specified by MJSW can usually be defaulted to 0.33 (SPICE assumes a graded junction). The built-in bulk-to-junction contact potential, $\Phi_{0}$, can be specified using PB or defaulted to 0.8 V (note that 0.9 V would typically be more accurate, but the resulting simulation differences are small). Sometimes the gate-to-source or drain-overlap capacitances can be specified using CGSO or CGDO, but normally these would be left to be calculated automatically using COX and LD.

Some of the more important parameters that should result in reasonable simulations (except for modelling short-channel effects) are summarized in Table 1.3 for both n - and p -channel transistors. Table 1.3 lists reasonable parameters for a typical $0.8-\mu \mathrm{m}$ technology.

### 1.5.3 Advanced SPICE Models of MOS Transistors

Although the SPICE model parameters presented in the last section provide reasonable accuracy for long-channel devices, for channel lengths $L \ll 1 \mu \mathrm{~m}$ their accuracy becomes very poor. Many SPICE MOS models have therefore been developed to try to capture higher-order effects. A summary of the capabilities of the more common modern SPICE model formats is provided in Table 1.4.

Unfortunately, these SPICE models require over 100 parameters to accurately capture transistor operation in all of its modes over a wide range of temperatures. Many parameters are required because, for very small device sizes, fundamental constants such as threshold voltage and effective carrier mobility become dependent on the transistor's exact width and length. Hence, it is strongly recommended that analog designers use only a small set of "unit-sized" transistors, forming all transistors from parallel combinations of these elementary devices.

Table 1.3 A reasonable set of Level 2 or 3 MOS parameters for a typical 0.8- $\mu \mathrm{m}$ technology.

| SPICE <br> Parameter | Model <br> Constant | Brief Description | Typical Value |
| :---: | :---: | :---: | :---: |
| VTO | $\mathrm{V}_{\mathrm{t} \mathrm{n}}: \mathrm{V}_{\mathrm{tp}}$ | Transistor threshold voltage (in V) | 0.8:-0.9 |
| UO | $\mu_{\mathrm{n}}: \mu_{\mathrm{p}}$ | Carrier mobility in bulk (in $\mathrm{cm}^{2} / \mathrm{V} \cdot \mathrm{s}$ ) | 500:175 |
| TOX | $t_{\text {ox }}$ | Thickness of gate oxide (in m) | $1.8 \times 10^{-8}$ |
| LD | $\mathrm{L}_{\mathrm{D}}$ | Lateral diffusion of junction under gate (in m) | $6 \times 10^{-8}$ |
| GAMMA | $\gamma$ | Body-effect parameter | 0.5: 0.8 |
| NSUB | $\mathrm{N}_{\mathrm{A}}: \mathrm{N}_{\mathrm{D}}$ | The substrate doping (in $\mathrm{cm}^{-3}$ ) | $3 \times 10^{16}: 7.5 \times 10^{16}$ |
| PHI | \|2 $\phi_{\mathrm{F}} \mid$ | Surface inversion potential (in V) | 0.7 |
| PB | $\Phi_{0}$ | Built-in contact potential of junction to bulk (in V) | 0.9 |
| CJ | $\mathrm{C}_{\mathrm{j} 0}$ | Junction-depletion capacitance at $0-\mathrm{V}$ bias (in $\mathrm{F} / \mathrm{m}^{2}$ ) | $2.5 \times 10^{-4}: 4.0 \times 10^{-4}$ |
| CJSW | $\mathrm{C}_{\mathrm{j} \text {-sw0 }}$ | Sidewall capacitance at $0-\mathrm{V}$ bias (in $\mathrm{F} / \mathrm{m}$ ) | $2.0 \times 10^{-10}: 2.8 \times 10^{-10}$ |
| MJ | $\mathrm{m}_{\mathrm{j}}$ | Bulk-to-junction exponent (grading coefficient) | 0.5 |
| MJSW | $\mathrm{m}_{\mathrm{j} \text { sw }}$ | Sidewall-to-junction exponent (grading coefficient) | 0.3 |

Table 1.4 A summary of modern SPICE model formats.

| SPICE <br> Model | Main strengths compared with previous device models |
| :--- | :--- |
| BSIM3 | Improved modeling of moderate inversion, and the geometry-dependence of device <br> parameters. This also marked a return to a more physics-based model as opposed to the <br> preceding highly empirical models. |
| EKV | Relates terminal currents and voltages with unified equations that cover all modes of transistor <br> operation, hence avoiding discontinuities at transitions between, for example, weak and strong <br> inversion. Also handles geometry-dependent device parameters. |
| BSIM4 $\quad$Improved modeling of leakage currents and short-channel effects, noise, and parasitic resistance <br> in the MOSFET terminals, as well as continued improvements in capturing the geometry- <br> dependence of device parameters. |  |
| PSP $\quad$Improved modeling of noise and the many short-channel and layout-dependent effects now <br> dominant in nanoscale CMOS devices. Particular effort was made to accurately model <br> nonlinearities, which requires accuracy in the high-order derivatives of the transistor's <br> voltage-current relationships. |  |

For example, for a minimum gate-length of $L_{\text {min }}$, device sizes with $(W / L)=\left(8 L_{\text {min }} / L_{\text {min }}\right),\left(12 L_{\text {min }} / 1.5 L_{\text {min }}\right)$, $\left(16 \mathrm{~L}_{\min } / 2 \mathrm{~L}_{\text {min }}\right)$, and $\left(32 \mathrm{~L}_{\min } / 4 \mathrm{~L}_{\text {min }}\right)$ in both NMOS and PMOS varieties might be chosen. Then, if a transistor of size $(W / L)=\left(240 \mathrm{~L}_{\text {min }} / 2 \mathrm{~L}_{\text {min }}\right)$ is desired, simply combine 15 of the $\left(16 \mathrm{~L}_{\text {min }} / 2 \mathrm{~L}_{\text {min }}\right)$-devices in parallel as shown in Fig. 1.33. Of course this practice restricts the device sizes available for design, but the benefits of having device parameters that are consistent and well-understood far outweigh this minor drawback.

For each device in the set, rough estimates of a few basic model parameters such as $\mu_{n} \mathrm{C}_{\mathrm{ox}}, \mathrm{V}_{\mathrm{tn}}$, etc. may be obtained from simulation data, or better yet measurements, of the unit-sized devices following the procedures in Examples $1.9,1.11,1.17$, and 1.18 . These rough model parameters may be used for the many quick handcalculations performed in the course of first-pass design. Similarly, the unit-transistor's parasitic capacitances may
image_name:Fig. 1.33
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: Vin}
name: M2, type: NMOS, ports: {S: GND, D: X, G: Vin}
name: M3, type: NMOS, ports: {S: GND, D: X, G: Vin}
name: M15, type: NMOS, ports: {S: GND, D: X, G: Vin}
]
extrainfo:The circuit consists of 15 parallel NMOS transistors, each with a gate connected to Vin, source connected to GND, and drain connected to node X. This configuration is used to realize a larger transistor by combining smaller unit-sized transistor elements.

Fig. 1.33 Realization of a transistor by parallel combination of small unit-sized transistor elements.
be observed under a typical biasing condition; these capacitance values can then be used to obtain rough estimates of circuit parasitics. Several sets of such parameters that are representative of various CMOS technologies are presented in Table 1.5. When refinement and detailed verification of a design are required, these are of course performed with the aid of SPICE and the complete device models.

Some designers prefer to forgo the extraction of device parameters from data and simply refer to plots of device data throughout the design process, looking up small-signal parameters at different operating points. In any case, performing basic device simulations at the outset of any analog design is useful, not only for extracting approximate device parameters from complex MOS models, but also because it may expose shortcomings in the device models themselves or even the simulation environment. For example, discontinuities observed in plots of drain current or its
able on the book web site for simulation exercises.
derivatives are an indication that the model may be unreliable in that region.

Table 1.5 MOSFET parameters repre sentative of v arious CMOS technologies and used for rough hand calculations in this text.

|  | $\mathbf{0 . 8} \mu \mathbf{m}$ |  | $\mathbf{0 . 3 5} \boldsymbol{\mu m}$ |  | $\mathbf{0 . 1 8} \boldsymbol{\mu m}$ |  | $\mathbf{4 5} \mathbf{~ n m}$ |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Technology | NMOS | PMOS | NMOS | PMOS | NMOS | PMOS | NMOS | PMOS |
| $\mu \mathrm{C}_{\mathrm{ox}}\left(\mu \mathrm{A} / \mathrm{V}^{2}\right)$ | 92 | 30 | 190 | 55 | 270 | 70 | 280 | 70 |
| $\mathrm{~V}_{\mathrm{t} 0}(\mathrm{~V})$ | 0.80 | -0.90 | 0.57 | -0.71 | 0.45 | -0.45 | 0.45 | -0.45 |
| $\lambda \cdot \mathrm{~L}(\mu \mathrm{~m} / \mathrm{V})$ | 0.12 | 0.08 | 0.16 | 0.16 | 0.08 | 0.08 | 0.10 | 0.15 |
| $\mathrm{C}_{\mathrm{ox}}\left(\mathrm{fF} / \mu \mathrm{m}^{2}\right)$ | 1.8 | 1.8 | 4.5 | 4.5 | 8.5 | 8.5 | 25 | 25 |
| $\mathrm{t}_{\mathrm{ox}}(\mathrm{nm})$ | 18 | 18 | 8 | 8 | 5 | 5 | 1.2 | 1.2 |
| n | 1.5 | 1.5 | 1.8 | 1.7 | 1.6 | 1.7 | 1.85 | 1.85 |
| $\theta(1 / \mathrm{V})$ | 0.06 | 0.135 | 1.5 | 1.0 | 1.7 | 1.0 | 2.3 | 2.0 |
| m | 1.0 | 1.0 | 1.8 | 1.8 | 1.6 | 2.4 | 3.0 | 3.0 |
| $\mathrm{C}_{\mathrm{ov}} / \mathrm{W}=\mathrm{L}_{\mathrm{ov}} \mathrm{C}_{\mathrm{ox}}$ | 0.20 | 0.20 | 0.20 | 0.20 | 0.35 | 0.35 | 0.50 | 0.50 |
| $\quad(\mathrm{fF} / \mu \mathrm{m})$ |  |  |  |  |  |  |  |  |
| $\mathrm{C}_{\mathrm{do}} / \mathrm{W} \approx \mathrm{C}_{\mathrm{sb}} / \mathrm{W}$ | 0.50 | 0.80 | 0.75 | 1.10 | 0.50 | 0.55 | 0.45 | 0.50 |
| $(\mathrm{fF} / \mu \mathrm{m})$ |  |  |  |  |  |  |  |  |

## 1.6 PASSIVE DEVICES

Passive components are often required for analog design. However, since transistor performance is the primary consideration in the development of most integrated-circuit fabrication technologies, integrated-circuit passive components exhibit significant nonidealities that must be understood by the analog designer. The most common passive components in analog integrated-circuit design are resistors and capacitors.

### 1.6.1 Resistors

#### Strip Resistors

The simplest realization of an integrated-circuit resistor is nothing more than a strip of conductive material above the silicon substrate, as shown in Fig. 1.34. The conductivity of the material from which the strip is made is generally characterized by its sheet resistance, $\mathrm{R}_{\square}$, which is derived in terms of basic material properties in Section 1.7.4 and has units of $\Omega$. This, along with the dimensions of the strip, determine the value of the resistor.

$$
\begin{equation*}
R=R_{\square}\left(\frac{L}{W}\right) \tag{1.133}
\end{equation*}
$$

This equation is also useful for calculating the resistance of interconnects used in integrated circuits. Multiple strips may be combined in series or in parallel to realize the desired total resistance without requiring impractically large or small values of $L$ or $W$.

Strip resistors inevitably have parasitic capacitances to the silicon substrate which is generally held at a constant reference potential. A simple small-signal model is shown in Fig. 1.34. Although strictly speaking the capacitance is distributed evenly along the resistor, this first-order model simply splits the total capacitance into two lumped capacitors at either end of the resistor.

#### EXAMPLE 1.19

In many CMOS manufacturing processes, polysilicon strips are used to provide a controllable sheet resistance for analog design. A typical value is $\mathrm{R}_{\square}=500 \Omega$. If each strip is $1 \mu \mathrm{~m}$ wide and $5 \mu \mathrm{~m}$ long, how many must be connected in series to make a resistor of value $50 \mathrm{k} \Omega$ ?

#### Solution

Each strip has a resistance of

$$
\mathrm{R}=\mathrm{R}_{\square}\left(\frac{\mathrm{L}}{\mathrm{~W}}\right)=500 \Omega\left(\frac{5 \mu \mathrm{~m}}{1 \mu \mathrm{~m}}\right)=2.5 \mathrm{k} \Omega
$$

Hence, 20 must be connected in series to realize the desired total resistance,

$$
\mathrm{R}_{\mathrm{tot}}=20 \mathrm{R}=20(2.5 \mathrm{k} \Omega)=50 \mathrm{k} \Omega
$$

#### Semiconductor Resistors

Integrated-circuit manufacturing processes that are developed primarily for digital design may not include any materials with sufficient sheet resistance to realize practically useful resistor values. In these processes, a lightlydoped section of the silicon substrate with contacts at either end may be used as a resistor. The common case of a
image_name:Fig. 1.34
description:
[
name: CR1, type: Capacitor, value: CR1, ports: {Np: X, Nn: GND}
name: CR2, type: Capacitor, value: CR2, ports: {Np: Y, Nn: GND}
name: L, type: Resistor, value: L, ports: {N1: X, N2: Y}
]
extrainfo:The circuit represents a strip-resistor model with parasitic capacitances CR1 and CR2 connected to the grounded p-substrate. The resistor L is connected between nodes X and Y.

Fig. 1.34 A strip-resistor and its model including parasitic capacitances to the grounded substrate.
image_name:Fig. 1.35
description:The image labeled as Fig. 1.35 depicts a resistor structure made from a lightly doped semiconductor region, specifically an n-type region within a p-substrate. This resistor is isolated from the grounded substrate by a reverse-biased pn-junction, which is indicated by the depletion region surrounding the n region.

**Components and Structure:**
- **n+ Regions:** These are heavily doped n-type semiconductor regions at both ends of the resistor. These regions are connected to aluminum (Al) contacts, which facilitate electrical connections.
- **n- Region:** The central part of the resistor is a lightly doped n-type region, labeled as the n- region. It represents the resistive path between the two n+ regions.
- **p- Substrate:** The entire structure is built on a p-type substrate, which is grounded as indicated by the ground symbol.

**Connections and Interactions:**
- **Capacitances (CR1 and CR2):** Two parasitic capacitances, CR1 and CR2, are shown connected to the n- region and the ground. These represent the capacitance between the n-region and the p-substrate due to the depletion region.
- **Depletion Region:** This is illustrated as a curved boundary around the n- region, indicating the space charge region where no free carriers exist, providing isolation from the substrate.
- **Cd-sw:** This is another capacitance shown at the right side, representing the capacitance due to the sidewall of the depletion region.

**Labels, Annotations, and Key Features:**
- **L:** The length of the n- region is labeled as L, indicating the distance over which the resistive path extends.
- **H:** The height of the depletion region is labeled as H.
- **Ground Connection:** The p-substrate is clearly marked with a ground symbol, indicating that it is at zero potential.

The diagram effectively illustrates the physical layout and electrical characteristics of a strip-resistor model, highlighting the parasitic effects due to the semiconductor structure and substrate interactions.

Fig. 1.35 A resistor made from a lightly doped semiconductor region with depletion region capacitances shown.
type-n resistor in a p-substrate is shown in Fig. 1.35. The resistor is isolated from the grounded substrate by a reverse-biased pn-junction. Depending on the dopant concentration, the effective sheet resistance may be in the range of 10 's of Ohms with a complex temperature dependence. A detailed derivation is presented in section 1.7.4 resulting the in the following sheet resistance, assuming a uniform height (depth) resistor, H :

$$
\begin{equation*}
\mathrm{R}_{\square}=\frac{1}{\mathrm{q} \mu_{\mathrm{n}} \mathrm{Hn} \mathrm{n}_{\mathrm{n}}} \tag{1.134}
\end{equation*}
$$

The small-signal model in Fig. 1.34 is also applicable to semiconductor resistors. However, unlike strip resistors, the parasitic capacitors are junction capacitances so their values depend on the voltages at either end of the resistor. Furthermore, the extent to which the depletion region extends into the resistor also depends upon the resistor's terminal voltages, so its effective cross-section and resistance will change with voltage. This can be problematic for analog design since capacitors and resistors whose values depend on their terminal voltages are nonlinear circuit elements and will introduce harmonic distortion when subjected
to time-varying signals. Finally, the parasitic capacitances $C_{R 1}$ and $C_{R 2}$ for semiconductor resistors are typically larger than for strip resistors because they can be located further from the grounded substrate, and because the relative permittivity of silicon $\left(\mathrm{K}_{\mathrm{s}} \cong 11.8\right)$ is higher than that of the silicon dioxide insulation above the substrate ( $\mathrm{K}_{\mathrm{ox}} \cong 3.9$ ).

#### EXAMPLE 1.20

A $4 \mathrm{k} \Omega$ resistor is to be formed from a single 3- $\mu \mathrm{m}$-wide strip of type-n silicon with a dopant concentration of $\mathrm{N}_{\mathrm{D}}=10^{23}$ atoms $/ \mathrm{m}^{3}$ that extends to a depth of $\mathrm{H}=2 \mu \mathrm{~m}$ into a type-p substrate that has a dopant concentration of $N_{A}=10^{22}$ atoms $/ \mathrm{m}^{3}$. Find the length of the resistor and estimate the parasitic capacitances. Assume that the resistor-substrate junction has a 3-V reverse bias, and $\mu_{\mathrm{n}}=8 \cdot 10^{-2} \mathrm{~m}^{2} / \mathrm{V} \cdot \mathrm{s}$ inside the resistor.

#### Solution

Substitution into (1.134) yields a sheet resistance of

$$
\mathrm{R}_{\square}=\frac{1}{\left(1.6 \cdot 10^{-19}\right)\left(8 \cdot 10^{-2}\right)\left(2 \cdot 10^{-6}\right)\left(10^{23}\right)}=390 \Omega / \mathrm{sq}
$$

Rearranging (1.133),

$$
\mathrm{L}=\left(\frac{\mathrm{R}}{\mathrm{R}_{\square}}\right) \mathrm{W}=\left(\frac{4 \mathrm{k} \Omega}{0.39 \mathrm{k} \Omega}\right) 3 \mu \mathrm{~m}=31 \mu \mathrm{~m}
$$

This lightly-doped junction has a built-in voltage lower than was calculated in Example 1.2.

$$
\Phi_{0}=0.026 \times \ln \left(\frac{10^{23} \times 10^{22}}{\left(1.1 \times 10^{16}\right)^{2}}\right)=0.77 \mathrm{~V}
$$

The junction capacitance per unit area, assuming an abrupt one-sided junction $\left(N_{A}\right.$ « $\left.N_{D}\right)$ and using the reverse bias voltage $\mathrm{V}_{\mathrm{R}}=3 \mathrm{~V}$, may be calculated as follows:

$$
\begin{gathered}
\mathrm{C}_{\mathrm{j} 0}=\sqrt{\frac{\mathrm{qK}_{\mathrm{s}} \varepsilon_{0} \mathrm{~N}_{\mathrm{A}}}{2 \Phi_{0}}}=\sqrt{\frac{1.6 \times 10^{-19} \times 11.8 \times 8.854 \times 10^{-12} \times 10^{22}}{2 \times 0.77}}=0.33 \mathrm{fF} / \mu \mathrm{m}^{2} \\
\mathrm{C}_{\mathrm{j}}=\frac{\mathrm{C}_{\mathrm{j} 0}}{\sqrt{1+\frac{\mathrm{V}_{\mathrm{B}}}{\Phi_{0}}}}=\frac{0.33}{\sqrt{1+\frac{3}{0.77}}} \mathrm{fF} / \mu \mathrm{m}^{2}=0.15 \mathrm{fF} / \mu \mathrm{m}^{2}
\end{gathered}
$$

The resistor forms a pn-junction with an area of $\mathrm{WL}=(3 \mu \mathrm{~m} \cdot 31 \mu \mathrm{~m})=93 \mu \mathrm{~m}^{2}$ and sidewalls having an area approximately equal to the resistor perimeter times its height,

$$
A_{s w}=(3 \mu \mathrm{~m}+31 \mu \mathrm{~m}+3 \mu \mathrm{~m}+31 \mu \mathrm{~m}) \cdot 2 \mu \mathrm{~m}=136 \mu \mathrm{~m}^{2}
$$

Adopting the simple model of Fig. 1.35 and assuming negligible voltage drop across the resistor, the total capacitance may be divided equally between the two resistor terminals.

$$
C_{R 1}=C_{R 2}=\frac{\left(W L+A_{s w}\right) C_{i}}{2}=\frac{(93+136) 0.15}{2} \mathrm{fF}=17 \mathrm{fF}
$$

#### Triode MOS Resistors

There is a third method to realize resistors on an integrated circuit with which the reader is already familiar: a MOS device in triode. Pictured in Fig. 1.11, this is effectively a semiconductor resistor where the channel depth, and hence resistance, are modulated by a gate voltage. Therefore, like semiconductor resistors, triode MOS devices exhibit nonlinear resistance and parasitic capacitances. But, because the conducting channel region is much shallower than in semiconductor resistors, the resistance is even more nonlinear than a semiconductor resistor. Typically, MOS triode resistors are only used when the voltage across the resistor terminals (i.e. the drain and source of the MOS device) will remain significantly less than $\mathrm{V}_{\text {eff }}$.

In spite of these shortcomings, MOS devices in triode have two unique properties that make them very useful as resistors in analog integrated-circuit design. First, the value of resistance may be tuned via a third terminal: the gate voltage. Second, relatively large values of resistance can be realized in a very compact area.

#### EXAMPLE 1.21

As in Example 1.19, you require a resistor of value $50 \mathrm{k} \Omega$. However, since the voltage across the resistor is never expected to exceed 200 mV , you decide it is feasible to use a n-channel MOS devices in triode to implement it. You elect to use multiple devices sized $\mathrm{W} / \mathrm{L}=2 \mu \mathrm{~m} / 1 \mu \mathrm{~m}$ to avoid short-channel effects. If $\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}=300 \mu \mathrm{~A} / \mathrm{V}^{2}$, $\mathrm{V}_{\mathrm{tn}}=0.3 \mathrm{~V}$, and you elect to use $\mathrm{V}_{\mathrm{GS}}=1 \mathrm{~V}$, find the number of series devices required to implement the resistor. Compare the resulting device area to that calculated in Example 1.19 for a strip resistor.

#### Solution

The resistance of a device in triode is given in equation (1.104).

$$
\begin{aligned}
r_{\mathrm{ds}} & =\left(\mu_{\mathrm{n}} C_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)\left(\mathrm{V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{tn}}\right)\right)^{-1} \\
& =\left(300 \mu \mathrm{~A} / \mathrm{V}^{2}\left(\frac{2 \mu \mathrm{~m}}{1 \mu \mathrm{~m}}\right)(1 \mathrm{~V}-0.3 \mathrm{~V})\right)^{-1} \\
& =2.38 \mathrm{k} \Omega
\end{aligned}
$$

With 21 such devices in series, the desired resistance $21 \cdot 2.38 \mathrm{k} \Omega=50 \mathrm{k} \Omega$ is realized. This is considerably smaller than combining 20 strip resistors in series, each $5 \mu \mathrm{~m} \times 1 \mu \mathrm{~m}$, as in Example 1.19.

Regardless of how they are implemented, resistor values vary greatly from one integrated circuit to another and with changes in temperature. Fortunately, with some care it is possible to ensure that such variations effect all
resistors on a given integrated circuit approximately equally. Analog integrated circuits must often be designed to function properly even when the resistor values change by $10-40 \%$.

### 1.6.2 Capacitors

#### pn Junction Capacitors

The capacitance provided by reverse-biased pn-junctions has already been discussed in Section 1.1. Junction capacitances may be introduced intentionally into an analog design to serve as a capacitor. They provide a relatively high value of capacitance per unit area since the depletion region can be quite thin and the relative permittivity of silicon is quite high ( $\mathrm{K}_{\mathrm{s}} \cong 11.8$ ). Their capacitance can be tuned by adjusting the voltage across them. When used to realize a variable capacitor in this way, they are called varactors.

Unfortunately, several features of junction capacitances pose problems for analog design. First, although the tunability of their capacitance is useful in some applications, it also makes them nonlinear elements that distort time-varying signals. Second, the value of capacitance realized by a given size junction varies considerably with dopant concentration which is difficult to control during integrated circuit manufacturing. Finally, junction capacitors have more leakage current than other types of integrated circuit capacitors. The most common application for pn junction capacitors is as a varactor in tunable radio-frequency circuits, notably oscillators, although even there MOS capacitors are now often favoured.

#### MOS Capacitors

Since the gate oxide is the thinnest dielectric available in an integrated circuit, it is imminently sensible to build capacitors around it. There are many ways to do so. All comprise gate and silicon conducting "plates" separated by the gate oxide as a dielectric. All are nonlinear capacitors, whose value depends on the voltage across it. The detailed modeling of all of these is beyond the scope of this section, so we will focus on just one common structure: the PMOS transistor.

When using a PMOS transistor, one terminal is the gate and the other is the source, drain, and body all shorted together underneath, shown schematically in Fig. 1.36(a). In this configuration, $\mathrm{V}_{\mathrm{DS}}=0$ and $\mathrm{V}_{\mathrm{SG}}=-\mathrm{V}_{\mathrm{GS}}$ is the voltage on the capacitor. Small-signal models for a NMOS transistor in this mode were covered in Section 1.2.8, but the salient points are repeated here for a PMOS device.

If $\mathrm{V}_{\mathrm{SG}}>\left|\mathrm{V}_{\mathrm{tp}}\right|$, the device enters triode and the small-signal capacitance is given by the sum of $\mathrm{C}_{\mathrm{gs}}$ and $\mathrm{C}_{\mathrm{gd}}$ from equation (1.105) and two overlap capacitances, $\mathrm{C}_{\mathrm{ov}}$, from equation (1.90).

$$
\begin{equation*}
\mathrm{C}_{\text {Mos(on) }}=\mathrm{WLC}_{\mathrm{ox}}+2 \mathrm{WL}_{\mathrm{ov}} \mathrm{C}_{\mathrm{ox}} \tag{1.135}
\end{equation*}
$$

image_name:(a)
description:The diagram shows a PMOS capacitor with a nonlinear capacitance characteristic and its small-signal model. The PMOS is connected with its source at node 'b', drain at 'b1d1s1', and gate at 'g'. The capacitance is dependent on the gate-source voltage VSG. The small-signal model includes two capacitors, CMOS and Cb, connected to nodes X, Y, and GND.
image_name:(b)
description:The graph labeled "(b)" is a nonlinear capacitance plot for a PMOS device, depicting the relationship between the capacitance \( C_{\text{MOS}} \) and the gate-source voltage \( V_{\text{SG}} \).

1. **Type of Graph and Function:**
- This is a nonlinear capacitance versus voltage graph, commonly used in semiconductor device analysis to show how capacitance changes with voltage.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( V_{\text{SG}} \), representing the gate-source voltage. The voltage is typically measured in volts.
- The vertical axis is labeled \( C_{\text{MOS}} \), representing the MOS capacitance. The capacitance is typically measured in farads or a subunit like picofarads.
- The graph appears to use a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The graph shows a U-shaped curve. As \( V_{\text{SG}} \) increases from zero, \( C_{\text{MOS}} \) initially decreases, reaching a minimum at \( |V_{\text{tp}}| \), and then increases again.
- The curve suggests that the capacitance is at its lowest when \( V_{\text{SG}} \) is equal to the threshold voltage magnitude \( |V_{\text{tp}}| \).

4. **Key Features and Technical Details:**
- The graph has two key horizontal lines marked as \( C_{\text{MOS(on)}} \) and \( C_{\text{MOS(off)}} \), indicating the capacitance values when the device is on and off, respectively.
- \( C_{\text{MOS(on)}} \) is higher than \( C_{\text{MOS(off)}} \), reflecting the increased capacitance when the device is in the on state.
- The intersection of the curve with the \( V_{\text{SG}} \) axis at \( |V_{\text{tp}}| \) is a critical point where the transition between on and off states occurs.

5. **Annotations and Specific Data Points:**
- The graph highlights the threshold voltage \( |V_{\text{tp}}| \) as a significant marker on the \( V_{\text{SG}} \) axis.
- The dashed lines representing \( C_{\text{MOS(on)}} \) and \( C_{\text{MOS(off)}} \) serve as reference levels for capacitance in the on and off states.
image_name:(c)
description:he circuit diagram (c) includes a PMOS device named 'bidisl' with source connected to node 'b', drain and gate connected to node 'g'. It also includes two capacitors: 'CMOS' between nodes 'X' and 'Y', and 'Cb' between node 'X' and ground. The diagram represents a small-signal model with a voltage source V_SG.

Fig. 1.36 A PMOS capacitor: (a) schematic symbol; (b) nonlinear capacitance; (c) small-signal model.

If $\mathrm{V}_{\mathrm{SG}}<\left|\mathrm{V}_{\mathrm{tp}}\right|$, the channel under the device turns off and the small-signal capacitance is mainly provided by only the overlap capacitances $\mathrm{C}_{\mathrm{gs}}$ and $\mathrm{C}_{\mathrm{gd}}$ in equation (1.110).

$$
\begin{equation*}
\mathrm{C}_{\text {MOS(off) }} \cong 2 \mathrm{WL}_{\mathrm{ov}} \mathrm{C}_{\mathrm{ox}} \tag{1.136}
\end{equation*}
$$

Here, we have neglected $\mathrm{C}_{g b}$ which is assumed to be much smaller. Finally, if $\mathrm{V}_{\mathrm{SG}}$ becomes significantly less than zero, the silicon immediately under the gate will eventually accumulate n-type carriers and become conducting again, thus increasing the small-signal capacitance back to a value close to (1.135). Hence, the structure's smallssignal capacitance varies with voltage as shown in Fig. 1.36(b).

The PMOS body terminal is typically a $n$-type well in the p -type substrate, isolated from ground by a reversebiased pn-junction. This of course introduces a junction capacitance between the body and ground, $\mathrm{C}_{\mathrm{b}}$, which can be quite large and whose value varies with changes in the body voltage. A simple small-signal model is shown in Fig. 1.36(c). For more accurate modeling, a series resistance may be included in series with $\mathrm{C}_{\text {mos }}$ due to the resistance of the inverted channel or body region.

Clearly this is a highly nonlinear capacitor and should be used with care in analog design. Nevertheless, it is popular for three reasons. First, because it is relatively well-modeled by standard circuit simulators. It is, after all, a transistor. Second, the very thin gate oxide ensures a high capacitance-per-unit-area. Third, it requires no special modifications to CMOS integrated-circuit fabrication processes.

#### Metal-metal

To realize a purely linear capacitance on an integrated circuit, it is necessary to avoid the use of semiconductors for either plate. Instead, the many electrically-isolated layers of conductors above the silicon substrate are used.

Two different geometries used to implement metal-metal capacitors are shown in Fig. 1.37. The capacitance of the parallel-plate structure is approximately

$$
\begin{equation*}
\mathrm{C} \cong \frac{\varepsilon_{\mathrm{ox}} \mathrm{~A}}{\mathrm{t}_{\mathrm{ox}}} \tag{1.137}
\end{equation*}
$$

where $t_{\mathrm{ox}}$ is the spacing between plates (on the order of $0.1-10 \mu \mathrm{~m}$ ), $\varepsilon_{\mathrm{ox}}$ is the permittivity of the insulator between plates (often silicon dioxide, for which $\varepsilon_{0 x} \cong 3.9 \varepsilon_{0}$ ), and A is the area of the plate. Equation (1.137) neglects the fringe fields around the edges of the capacitor, but these are relatively small if the capacitor area is large. Some integrated circuits are specially engineered to provide parallel-plate capacitors with very small $t_{0 x}$ and/or large $\varepsilon_{0 x}$, thus permitting small area A for a given value of capacitance. For example, two polysilicon (gate) layers are sometimes stacked on top of each other very closely to realize a "double-poly capacitor". ${ }^{16}$ If no such provision is made, the normal metal layers intended for wiring may be used.

The parallel-plate structure is asymmetric since the bottom plate is in closer proximity to the silicon substrate and electrically shields the top plate from ground. Hence, the bottom plate has a larger parasitic capacitance, $\mathrm{C}_{p 1}$ » $\mathrm{C}_{p 2}$. This can often be exploited in analog designs by connecting the bottom plate to a node with a constant potential with respect to ground, thus minimizing parasitics on the plate with time-varying potential. In light of this, a slightly different symbol is used in this book, as shown in Fig. 1.37(a), when the distinction between top and bottom plate is crucial.

The side-wall capacitive structure shown in Fig. 1.37(b) is becoming increasingly popular in modern integrated circuits where metal wires may actually be made thinner (when viewed from above) than their height. Hence, routing many of them immediately next to each other can provide a large total capacitance. In fact, the capacitance-per-unit-area of such a structure is often greater than parallel-plate metal-metal structures (unless special high-density parallel-plate capacitors are available). The structure is symmetric, with equal parasitics on either side of the capacitor, $\mathrm{C}_{\mathrm{p} 1}=\mathrm{C}_{\mathrm{p} 2}$. However, the capacitance is more difficult to estimate since it is largely provided by fringing electrical fields so appropriate computer tools are required to properly design them.
image_name:(a)
description:The image consists of three diagrams labeled (a), (b), and (c), illustrating different metal-metal capacitor geometries and their small-signal model.

1. **Diagram (a) - Parallel Plate Capacitor:**
- This diagram shows a parallel plate capacitor structure. The capacitor is depicted with two metal plates separated by a dielectric material.
- The top plate is labeled as 'C' indicating the main capacitance of the structure.
- There are parasitic capacitances, labeled as \(C_{p1}\) and \(C_{p2}\), connected to each plate and grounded. \(C_{p1}\) is notably larger than \(C_{p2}\), as indicated by the notation \(C_{p1} \gg C_{p2}\).
- The entire structure is situated above a silicon (Si) substrate, which is connected to the ground.

2. **Diagram (b) - Side-Wall Capacitors:**
- This part illustrates a side-wall capacitor configuration with multiple vertical plates.
- Each plate contributes to the total capacitance, denoted as \(C = \Sigma C_i\), where \(C_i\) represents individual capacitances.
- Similar to the parallel plate structure, parasitic capacitances \(C_{p1}\) and \(C_{p2}\) are shown grounded, with the silicon substrate also connected to ground.

3. **Diagram (c) - Small-Signal Model:**
- This is a simplified representation of the capacitor's small-signal model.
- It shows two nodes, labeled X and Y, connected by the main capacitance \(C\).
- Parasitic capacitances \(C_{p1}\) and \(C_{p2}\) are connected to each node and grounded, reflecting their influence on the signal path.

Overall, the diagrams illustrate different capacitor geometries and their equivalent small-signal models, highlighting the role of parasitic capacitances and their grounding to minimize interference.
image_name:(b)
description:The image depicts different metal-metal capacitor geometries, focusing on a side-wall capacitor in part (b). This structure consists of multiple vertical metal plates arranged parallel to each other, forming a comb-like configuration. Each pair of adjacent plates forms a capacitor, contributing to the total capacitance, denoted as \( C = \sum C_i \). These capacitors are connected in parallel, which enhances the overall capacitance of the structure.

Identification of Components and Structure:
- **Metal Plates:** Several vertical metal plates are shown, each contributing to the capacitance.
- **Capacitance \( C \):** The total capacitance is the sum of individual capacitances \( C_1, C_2, \ldots \).
- **Parasitic Capacitances \( C_{p1} \) and \( C_{p2} \):** These are shown on either side of the structure, connected to ground (GND).

Connections and Interactions:
- The metal plates are connected to form multiple capacitors in parallel, enhancing the total capacitance.
- Parasitic capacitances \( C_{p1} \) and \( C_{p2} \) are connected to ground, indicating the potential effects of the silicon substrate below.

Labels, Annotations, and Key Features:
- **"GND" Labels:** Indicate grounding of the parasitic capacitances.
- **"Si substrate" Annotation:** Shows that the structure is built above a silicon substrate, affecting parasitic capacitance.
- **Capacitance Sum Notation:** \( C = \sum C_i \) represents the total capacitance as the sum of individual capacitances across the plates.
image_name:(c)
description::The circuit diagram (c) represents a small-signal model of a capacitor with parasitic capacitors Cp1 and Cp2 connected to ground. The main capacitor C is connected between nodes X and Y. Cp1 and Cp2 represent the parasitic capacitance to ground on either side of the main capacitor.

Fig. 1.37 Metal-metal capacitor geometries: (a) parallel plate capacitor; (b) side-wall capacitors; (c) small-signal model.

When using either of these geometries, parasitics are minimized by locating them as high above the silicon substrate as possible. Of course, this may not be possible - for example, when a double-poly capacitor is being used. Furthermore, either of these geometries, or combinations of them, may be stacked on top of each other. For example, several parallel-plates may be stacked on top of each other with alternating layers shorted to provide a metal "sandwich" capacitor. Such complex structures generally provide even higher capacitance per unit area, and require the use of computer tools to accurately estimate their value.

## 1.7 APPENDIX

The purpose of this appendix is to present derivations for device equations that rely heavily on device physics knowledge. Specifically, equations are derived for the exponential relationship and diffusion capacitance of diodes, and for the threshold voltage and triode relationship for MOS transistors.

### 1.7.1 Diode Exponential Relationship

The concentration of minority carriers in the bulk, far from the junction, is given by (1.2) and (1.4). Close to the junction, the minority-carrier concentrations are much larger. Indeed, the concentration next to the junction increases exponentially with the external voltage, $\mathrm{V}_{\mathrm{D}}$, that is applied in the forward direction. The concentration of holes in the n side next to the junction, $\mathrm{p}_{\mathrm{n}}$, is given by [Sze, 1981]

$$
\begin{equation*}
p_{n}=p_{n 0} e^{v_{D} v_{T}}=\frac{n_{i}^{2}}{N_{D}} e^{v_{D} / v_{T}} \tag{1.138}
\end{equation*}
$$

Similarly, the concentration of electrons in the p side next to the junction is given by

$$
\begin{equation*}
n_{p}=n_{p 0} e^{v_{D} / v_{T}}=\frac{n_{i}^{2}}{N_{A}} e^{v_{D} V_{T}} \tag{1.139}
\end{equation*}
$$

As the carriers diffuse away from the junction, their concentration exponentially decreases. The relationship for holes in the n side is

$$
\begin{equation*}
p_{n}(x)=p_{n}(0) e^{-x / L_{p}} \tag{1.140}
\end{equation*}
$$

where x is the distance from the junction and $\mathrm{L}_{\mathrm{p}}$ is a constant known as the diffusion length for holes in the n side. Similarly, for electrons in the $p$ side we have

$$
\begin{equation*}
n_{p}(x)=n_{p}(0) e^{-x / L_{n}} \tag{1.141}
\end{equation*}
$$

where $L_{n}$ is a constant known as the diffusion length of electrons in the $p$ side. Note that $p_{n}(0)$ and $n_{p}(0)$ are given by (1.138) and (1.139), respectively. Note also that the constants $L_{n}$ and $L_{p}$ are dependent on the doping concentrations $\mathrm{N}_{\mathrm{A}}$ and $\mathrm{N}_{\mathrm{D}}$, respectively.

The current density of diffusing carriers moving away from the junction is given by the well-known diffusion equations [Sze, 1981]. For example, the current density of diffusing electrons is given by

$$
\begin{equation*}
J_{D-n}=-q D_{n} \frac{d n_{p}(x)}{d x} \tag{1.142}
\end{equation*}
$$

where $D_{n}$ is the diffusion constant of electrons in the $p$ side of the junction. The negative sign is present because electrons have negative charge. Note that $D_{n}(k T / q) \mu_{n}$, where $\mu_{n}$ is the mobility of electrons. Using (1.141), we have

$$
\begin{equation*}
\frac{d n_{p}(x)}{d x}=\frac{n_{p}(0)}{L_{n}} e^{-x / L_{n}}=-\frac{n_{p}(x)}{L_{n}} \tag{1.143}
\end{equation*}
$$

Therefore

$$
\begin{equation*}
J_{D-n}=\frac{q D_{n}}{L_{n}} n_{p}(x) \tag{1.144}
\end{equation*}
$$

Thus, the current density due to diffusion is proportional to the minority-carrier concentration. Next to the junction, all the current flow results from the diffusion of minority carriers. Further away from the junction, some of the current flow is due to diffusion and some is due to majority carriers drifting by to replace carriers that recombined with minority carriers or diffused across the junction.

Continuing, we use (1.139) and (1.144) to determine the current density next to the junction of electrons in the p side:

$$
\begin{align*}
J_{D-n} & =\frac{q D_{n}}{L_{n}} n_{p}(0) \\
& =\frac{q D_{n}}{L_{n}} \frac{n_{i}^{2}}{N_{A}} e^{v_{D} / v_{T}} \tag{1.145}
\end{align*}
$$

For the total current of electrons in the p side, we multiply (1.145) by the effective junction area, $\mathrm{A}_{\mathrm{D}}$. The total current remains constant as we move away from the junction since, in the steady state, the minority carrier concentration at any particular location remains constant with time. In other words, if the current changed as we moved away from the junction, the charge concentrations would change with time.

Using a similar derivation, we obtain the total current of holes in the n side, $\mathrm{I}_{\mathrm{D}-\mathrm{p}}$, as

$$
\begin{equation*}
I_{D-p}=\frac{A_{D} q D_{n} n_{i}^{2}}{L_{p} N_{D}} e^{v_{D} v_{T}} \tag{1.146}
\end{equation*}
$$

where $D_{n}$ is the diffusion constant of electrons in the $p$ side of the junction, $L_{p}$ is the diffusion length of holes in the n side, and $\mathrm{N}_{\mathrm{D}}$ is the impurity concentration of donors in the n side. This current, consisting of positive carriers, flows in the direction opposite to that of the flow of minority electrons in the p side. However, since electron carriers are negatively charged, the direction of the current flow is the same. Note also that if the p side is more heavily doped than the n side, most of the carriers will be holes, whereas if the n side is more heavily doped than the p side, most of the carriers will be electrons.

The total current is the sum of the minority currents at the junction edges:

$$
\begin{equation*}
I_{D}=A_{D} q n_{i}^{2}\left(\frac{D_{n}}{L_{n} N_{A}}+\frac{D_{p}}{L_{p} N_{D}}\right) e^{v_{D} / v_{T}} \tag{1.147}
\end{equation*}
$$

Equation (1.147) is often expressed as

$$
\begin{equation*}
I_{D}=I_{S} e^{V_{D} V_{T}} \tag{1.148}
\end{equation*}
$$

where

$$
\begin{equation*}
I_{S}=A_{D} q n_{i}^{2}\left(\frac{D_{n}}{L_{n} N_{A}}+\frac{D_{p}}{L_{p} N_{D}}\right) \tag{1.149}
\end{equation*}
$$

Equation (1.148) is the well-known exponential current-voltage relationship of forward-biased diodes.
The concentrations of minority carriers near the junction and the direction of current flow are shown in Fig. 1.38.

### 1.7.2 Diode-Diffusion Capacitance

To find the diffusion capacitance, $\mathrm{C}_{\mathrm{d}}$, we first find the minority charge close to the junction, $\mathrm{Q}_{\mathrm{d}}$, and then differentiate it with respect to $\mathrm{V}_{\mathrm{D}}$. The minority charge close to the junction, $\mathrm{Q}_{\mathrm{d}}$, can be found by integrating either (1.140) or (1.141) over a few diffusion lengths. For example, if we assume $\mathrm{n}_{\mathrm{p} 0}$, the minority electron concentration in the $p$ side far from the junction is much less than $n_{p}(0)$, the minority electron concentration at the junction edge, we can use (1.141) to obtain

$$
\begin{align*}
Q_{n} & =q A_{D} \int_{0}^{\infty} n_{p}(x) d x \\
& =q A_{D} \int_{0}^{\infty} n_{p}(0) e^{-x / L_{n}} d x  \tag{1.150}\\
& =q A_{D} L_{n} n_{p}(0)
\end{align*}
$$

image_name:Fig. 1.38
description:**Type of Graph and Function:**
The graph is a spatial distribution diagram illustrating the concentration of minority carriers in a semiconductor material near a forward-biased p-n junction. It shows the exponential decay of carrier concentration on both sides of the junction.

**Axes Labels and Units:**
- The horizontal axis represents the spatial position relative to the junction, with the p-side on the left and the n-side on the right. The positions are labeled as \( x_p \) on the p-side and \( x_n \) on the n-side.
- The vertical axis represents the concentration of minority carriers, but specific units are not provided in the diagram.

**Overall Behavior and Trends:**
- On the p-side, the minority electron concentration \( n_p(x) \) decreases exponentially as it moves away from the junction, following the equation \( n_p(0)e^{-x_n/L_n} \).
- On the n-side, the minority hole concentration \( p_n(x) \) decreases exponentially as it moves away from the junction, following the equation \( p_n(0)e^{-x_p/L_p} \).
- The graph highlights the depletion region at the junction, where immobile charges reside.

**Key Features and Technical Details:**
- The depletion region is marked in the center of the graph, indicating the area devoid of mobile charge carriers.
- The exponential decay functions \( n_p(0)e^{-x_n/L_n} \) and \( p_n(0)e^{-x_p/L_p} \) describe how the minority carrier concentrations diminish with distance from the junction.
- The direction of diffusion is indicated, with electron diffusion moving to the right on the n-side and hole diffusion moving to the left on the p-side.

**Annotations and Specific Data Points:**
- The diagram includes annotations for the concentrations at the junction edge \( n_p(0) \) and \( p_n(0) \).
- Arrows indicate the direction of positive current flow and the diffusion of carriers (holes and electrons) across the junction.
- The presence of immobile charges in the depletion region is denoted by a series of positive and negative signs, representing the fixed charges that establish the electric field across the junction.

Fig. 1.38 The concentration of minority carriers and the direction of diffusing carriers near a forward-biased junction.

Using for $\mathrm{n}_{\mathrm{p}}(0)$ results in

$$
\begin{equation*}
Q_{n}=\frac{q A_{D} L_{n} n_{i}^{2}}{N_{A}} e^{v_{D} / v_{T}} \tag{1.151}
\end{equation*}
$$

In a similar manner, we also have

$$
\begin{equation*}
Q_{p}=\frac{q A_{D} L_{n} n_{i}^{2}}{N_{D}} e^{v_{D} / v_{T}} \tag{1.152}
\end{equation*}
$$

For a typical junction, one side will be much more heavily doped than the other side, and therefore the minority charge storage in the heavily doped side can be ignored since it will be much less than that in the lightly doped side. Assuming the n side is heavily doped, we find the total charge, $\mathrm{Q}_{\mathrm{d}}$, to be approximately given by $\mathrm{Q}_{\mathrm{n}}$, the minority charge in the $p$ side. Thus, the small-signal diffusion capacitance, $C_{d}$, is given by

$$
\begin{equation*}
C_{d}=\frac{d Q_{d}}{d V_{D}} \cong \frac{d Q_{n}}{d V_{D}}=\frac{q A_{D} L_{n} n_{i}^{2}}{N_{A} V_{T}} e^{v_{D} / V_{T}} \tag{1.153}
\end{equation*}
$$

Using (1.147) and again noting that $\mathrm{N}_{\mathrm{D}} \gg \mathrm{N}_{\mathrm{A}}$, we have

$$
\begin{equation*}
C_{d}=\frac{L_{n}^{2}}{D_{n}} \frac{I_{D}}{V_{T}} \tag{1.154}
\end{equation*}
$$

Equation (1.154) is often expressed as

$$
\begin{equation*}
C_{d}=\tau_{T} \frac{I_{D}}{V_{T}} \tag{1.155}
\end{equation*}
$$

where $\tau_{T}$ is the transit time of the diode given by

$$
\begin{equation*}
\tau_{T}=\frac{L_{n}^{2}}{D_{n}} \tag{1.156}
\end{equation*}
$$

for a single-sided diode in which the n side is more heavily doped.

### 1.7.3 MOS Threshold Voltage and the Body Effect

Many factors affect the gate-source voltage at which the channel becomes conductive. These factors are as follows:

1. The work-function difference between the gate material and the substrate material
2. The voltage drop between the channel and the substrate required for the channel to exist
3. The voltage drop across the thin oxide required for the depletion region, with its immobile charge, to exist
4. The voltage drop across the thin oxide due to unavoidable charge trapped in the thin oxide
5. The voltage drop across the thin oxide due to implanted charge at the surface of the silicon. The amount of implanted charge is adjusted in order to realize the desired threshold voltage.

The first factor affecting the transistor threshold voltage, $\mathrm{V}_{\mathrm{t}}$, is the built-in Fermi potential due to the different materials and doping concentrations used for the gate material and the substrate material. If one refers these potentials to that of intrinsic silicon [Tsividis, 1987], we have

$$
\begin{equation*}
\phi_{\mathrm{F}-\text { Gate }}=\frac{\mathrm{kT}}{\mathrm{q}} \ln \left(\frac{\mathrm{~N}_{\mathrm{D}}}{\mathrm{n}_{\mathrm{i}}}\right) \tag{1.157}
\end{equation*}
$$

for a polysilicon gate with doping concentration $N_{D}$, and

$$
\begin{equation*}
\phi_{\mathrm{F} \text {-sub }}=\frac{\mathrm{kT}}{\mathrm{q}} \ln \left(\frac{\mathrm{n}_{\mathrm{i}}}{\mathrm{~N}_{\mathrm{A}}}\right) \tag{1.158}
\end{equation*}
$$

for a p substrate with doping concentration $\mathrm{N}_{\mathrm{A}}$. The work-function difference is then given by

$$
\begin{align*}
\phi_{\mathrm{MS}} & =\phi_{\mathrm{F} \text {-Sub }}-\phi_{\mathrm{F}-\mathrm{Gate}} \\
& =\frac{\mathrm{kT}}{\mathrm{q}} \ln \left(\frac{\mathrm{~N}_{\mathrm{D}} \mathrm{~N}_{\mathrm{A}}}{\mathrm{n}_{\mathrm{i}}^{2}}\right) \tag{1.159}
\end{align*}
$$

The next factor that determines the transistor threshold voltage is the voltage drop from the channel to the substrate, which is required for the channel to exist. The question of exactly when the channel exists does not have a precise answer. Rather, the channel is said to exist when the concentration of electron carriers in the channel is equal to the concentration of holes in the substrate. At this gate voltage, the channel is said to be inverted. As the gate voltage changes from a low value to the value at which the channel becomes inverted, the voltage drop in the silicon also changes, as does the voltage drop in the depletion region between the channel and the bulk. After the channel becomes inverted, any additional increase in gate voltage is closely equal to the increase in voltage drop across the thin oxide. In other words, after channel inversion, gate voltage variations have little effect on the voltage drop in the silicon or the depletion region between the channel and the substrate.

The electron concentration in the channel is equal to the hole concentration in the substrate when the voltage drop from the channel to the substrate is equal to two times the difference between the Fermi potential of the substrate and intrinsic silicon, $\phi_{\mathrm{F}}$, where

$$
\begin{equation*}
\phi_{F}=-\frac{\mathrm{kT}}{\mathrm{q}} \ln \left(\frac{\mathrm{~N}_{\mathrm{A}}}{\mathrm{n}_{\mathrm{i}}}\right) \tag{1.160}
\end{equation*}
$$

Equation (1.200) is a factor in several equations used in modelling MOS transistors. For typical processes, $\phi_{F}$ can usually be approximated as 0.35 V for typical doping levels at room temperature.

The third factor that affects the threshold voltage is due to the immobile negative charge in the depletion region left behind after the p mobile carriers are repelled. This effect gives rise to a voltage drop across the thin oxide of $-Q_{B} / C_{o x}$, where

$$
\begin{equation*}
Q_{B}=-q N_{A} x_{d} \tag{1.161}
\end{equation*}
$$

and $x_{d}$ is the width of the depletion region. Since

$$
\begin{equation*}
\mathrm{x}_{\mathrm{d}}=\sqrt{\frac{2 \mathrm{~K}_{\mathrm{s}} \varepsilon_{0} \mid 2 \phi_{\mathrm{F}}}{\mathrm{qN}_{\mathrm{A}}}} \tag{1.162}
\end{equation*}
$$

we have

$$
\begin{equation*}
\mathrm{Q}_{\mathrm{B}}=-\sqrt{2 \mathrm{qN}_{\mathrm{A}} \mathrm{~K}_{\mathrm{s}} \varepsilon_{0}\left|2 \phi_{\mathrm{F}}\right|} \tag{1.163}
\end{equation*}
$$

The fourth factor that determines $\mathrm{V}_{\mathrm{tn}}$ is due to the unavoidable charge trapped in the thin oxide. Typical values for the effective ion density of this charge, $\mathrm{N}_{\mathrm{OX}}$, might be $2 \times 10^{14}$ to $10^{15} \mathrm{ions} / \mathrm{m}^{3}$. These ions are almost always positive. This effect gives rise to a voltage drop across the thin oxide, $\mathrm{V}_{\mathrm{ox}}$, given by

$$
\begin{equation*}
V_{o x}=\frac{-Q_{o x}}{C_{o x}}=\frac{-q N_{o x}}{C_{o x}} \tag{1.164}
\end{equation*}
$$

The native transistor threshold voltage is the threshold voltage that would occur naturally if one did not include a special ion implant used to adjust the threshold voltage. This value is given by

$$
\begin{equation*}
V_{\text {t-native }}=\phi_{\mathrm{MS}}-2 \phi_{\mathrm{F}}-\frac{\mathrm{Q}_{\mathrm{B}}}{\mathrm{C}_{\mathrm{ox}}}-\frac{\mathrm{Q}_{\mathrm{ox}}}{\mathrm{C}_{\mathrm{ox}}} \tag{1.165}
\end{equation*}
$$

A typical native threshold value might be around -0.1 V . It should be noted that transistors that have native transistor threshold voltages are becoming more important in analog circuit design where they are used in transmission gates or in source-follower buffers.

The fifth factor that affects threshold voltage is a charge implanted in the silicon under the gate to change the threshold voltage from that given by (1.165) to the desired value, which might be between 0.2 to 0.7 V for an n-channel transistor.

For the case in which the source-to-substrate voltage is increased, the effective threshold voltage is increased. This is known as the body effect. The body effect occurs because, as the source-bulk voltage, $\mathrm{V}_{\mathrm{SB}}$, becomes larger, the depletion region between the channel and the substrate becomes wider, and therefore more immobile negative charge becomes uncovered. This increase in charge changes the third factor in determining the transistor threshold voltage. Specifically, instead of using (1.163) to determine $Q_{B}$, one should now use

$$
\begin{equation*}
\left.Q_{B}=-\sqrt{2 q N_{A} K_{s} \varepsilon_{0}\left(V_{S B}+\left|2 \phi_{F}\right|\right.}\right) \tag{1.166}
\end{equation*}
$$

If the threshold voltage when $\mathrm{V}_{\mathrm{SB}}=0$ is denoted $\mathrm{V}_{\mathrm{tn} 0}$, then, using (1.165) and (1.166), one can show that

$$
\begin{align*}
\mathrm{V}_{\mathrm{tn}}= & \mathrm{V}_{\mathrm{tn} 0}+\Delta \mathrm{V}_{\mathrm{tn}} \\
& =\mathrm{V}_{\mathrm{tn} 0}+\frac{\sqrt{2 \mathrm{q} \mathrm{~N}_{\mathrm{A}} \mathrm{~K}_{\mathrm{s}} \varepsilon_{0}}}{\mathrm{C}_{\mathrm{ox}}}\left[\sqrt{\mathrm{~V}_{\mathrm{SB}}+\left|2 \phi_{\mathrm{F}}\right|}-\sqrt{\left|2 \phi_{\mathrm{F}}\right|}\right]  \tag{1.167}\\
& =\mathrm{V}_{\mathrm{tn} 0}+\gamma\left(\sqrt{\mathrm{V}_{\mathrm{SB}}+\left|2 \phi_{\mathrm{F}}\right|}-\sqrt{\left|2 \phi_{\mathrm{F}}\right|}\right)
\end{align*}
$$

where

$$
\begin{equation*}
\gamma=\frac{\sqrt{2 q \mathrm{~N}_{\mathrm{A}} \mathrm{~K}_{\mathrm{s}} \varepsilon_{0}}}{\mathrm{C}_{\mathrm{ox}}} \tag{1.168}
\end{equation*}
$$

The factor $\gamma$ is often called the body-effect constant.

### 1.7.4 MOS Triode Relationship

The current flow in a MOS transistor is due to drift current rather than diffusion current. This type of current flow is the same mechanism that determines the current in a resistor. The current density, J , is proportional to the electrical field, E, where the constant of proportionality, $\sigma$, is called the electrical permittivity. Thus,

$$
\begin{equation*}
J=\sigma E \tag{1.169}
\end{equation*}
$$

This constant for an $n$-type material is given by

$$
\begin{equation*}
\sigma=q n_{n} \mu_{n} \tag{1.170}
\end{equation*}
$$

where n is the concentration per unit volume of negative carriers and $\mu_{\mathrm{n}}$ is the mobility of electrons. Thus, the current density is given by

$$
\begin{equation*}
\mathrm{J}=\mathrm{qn}_{\mathrm{n}} \mu_{\mathrm{n}} \mathrm{E} \tag{1.171}
\end{equation*}
$$

image_name:Fig. 1.39 Current flowing through a unit volume
description:The diagram labeled "Fig. 1.39 Current flowing through a unit volume" illustrates a three-dimensional rectangular prism representing a unit volume. The dimensions of this prism are marked as height (H), width (W), and length (L). The diagram visually represents the flow of current through this volume.

1. **Identification of Components and Structure:**
- The main component is a rectangular prism divided into smaller cubic sections, indicating discrete unit volumes within the larger volume.
- The prism is oriented such that its length (L) is horizontal, width (W) is perpendicular to the length, and height (H) is vertical.

2. **Connections and Interactions:**
- An arrow labeled "J" is shown entering the prism, representing the current density vector. This arrow indicates the direction of current flow through the unit volume, moving perpendicular to the plane formed by the height and width.
- The current flows along the length (L) of the prism, as indicated by the arrow direction.

3. **Labels, Annotations, and Key Features:**
- The prism is labeled "Unit volume" to emphasize the consideration of current flow through a specific volume.
- The direction of current flow is explicitly marked with an arrow, and the label "Current flow through unit volume" is annotated alongside it.
- Dimensions are marked with double-headed arrows and labeled as H, W, and L, which are crucial for understanding the volume through which the current flows.

This diagram is used to conceptualize how current density (J) translates into actual current (I) flowing through a specified volume, as described in the equations provided in the context.

Fig. 1.39 Current flowing through a unit volume.

Next, consider the current flow through the volume shown in Fig. 1.39, where the volume has height H and width W . The current is flowing perpendicular to the plane $\mathrm{H} \times \mathrm{W}$ down the length of the volume, L . The current, I, everywhere along the length of the volume is given by

$$
\begin{equation*}
\mathrm{I}=\mathrm{JWH} \tag{1.172}
\end{equation*}
$$

The voltage drop along the length of the volume in the direction of $L$ for a distance $d x$ is denoted $d V$ and is given by

$$
\begin{equation*}
d V=E(x) d x \tag{1.173}
\end{equation*}
$$

Combining (1.171), (1.172), and (1.173), we obtain

$$
\begin{equation*}
\mathrm{q} \mu_{\mathrm{n}} \mathrm{WHn}_{\mathrm{n}}(\mathrm{x}) \mathrm{dV}=\mathrm{I} d \mathbf{x} \tag{1.174}
\end{equation*}
$$

where the carrier density $n_{n}(x)$ is now assumed to change along the length $L$ and is therefore a function of $x$.
As an aside, we examine the case of a resistor where $n_{n}(x)$ is usually constant. A resistor of length $L$ would therefore have a current given by

$$
\begin{equation*}
\mathrm{I}=\frac{\mathrm{q} \mu_{\mathrm{n}} \mathrm{WHn}}{\mathrm{~L}} \Delta \mathrm{~V} \tag{1.175}
\end{equation*}
$$

Thus, the resistance is given by

$$
\begin{equation*}
\mathrm{R}=\frac{\mathrm{L}}{\mathrm{q} \mu_{\mathrm{n}} \mathrm{WHn}_{\mathrm{n}}} \tag{1.176}
\end{equation*}
$$

Often this resistance is presented in a relative manner, in which the length and width are removed (since they can be design parameters) but the height remains included. In this case, the resulting expression is commonly referred to as the resistance per square and designated as $\mathrm{R}_{\square}$ where

$$
\begin{equation*}
R_{\square}=\frac{1}{q \mu_{n} H n_{n}} \tag{1.177}
\end{equation*}
$$

The total resistance is then given by equation (1.133), repeated here for convenience.

$$
\begin{equation*}
R_{\text {total }}=R_{\square} \frac{L}{W} \tag{1.178}
\end{equation*}
$$

In the case of a MOS transistor, the charge density is not constant down the channel. If, instead of the carrier density per unit volume, one expresses $\mathrm{n}_{\mathrm{n}}(\mathrm{x})$ as a function of charge density per square area from the top looking down, we have

$$
\begin{equation*}
\mathrm{Q}_{\mathrm{n}}(\mathrm{x})=\mathrm{qHn} \mathrm{n}_{\mathrm{n}}(\mathrm{x}) \tag{1.179}
\end{equation*}
$$

Substituting (1.179) into (1.174) results in

$$
\begin{equation*}
\mu_{n} W Q_{n}(x) d V=I d x \tag{1.180}
\end{equation*}
$$

Equation (1.180) applies to drift current through any structure that has varying charge density in the direction of the current flow. It can also be applied to a MOS transistor in the triode region to derive its I-V relationship. It should be noted here that in this derivation, it is assumed the source voltage is the same as the substrate voltage.

Since the transistor is in the triode region, we have $\mathrm{V}_{\mathrm{DG}}<-\mathrm{V}_{\mathrm{tn}}$. This requirement is equivalent to $\mathrm{V}_{\mathrm{DS}}<\mathrm{V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{tn}}=\mathrm{V}_{\text {eff }}$. It is assumed that the effective channel length is L . Assuming the voltage in the channel at distance x from the source is given by $\mathrm{V}_{\mathrm{ch}}(\mathrm{x})$, from Fig. 1.40, we have

$$
\begin{equation*}
Q_{n}(x)=C_{o x}\left[V_{G S}-V_{c h}(x)-V_{t n}\right] \tag{1.181}
\end{equation*}
$$

Substituting (1.181) into (1.180) results in

$$
\begin{equation*}
\mu_{\mathrm{n}} \mathrm{WC}_{\mathrm{ox}}\left[\mathrm{~V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{ch}}(\mathrm{x})-\mathrm{V}_{\mathrm{tn}}\right] \mathrm{d} \mathrm{~V}_{\mathrm{ch}}=\mathrm{I}_{\mathrm{D}} \mathrm{dx} \tag{1.182}
\end{equation*}
$$

Integrating both sides of (1.182), and noting that the total voltage along the channel of length $L$ is $V_{D S}$, we obtain

$$
\begin{equation*}
\int_{0}^{V_{D S}} \mu_{\mathrm{n}} \mathrm{WC}_{\mathrm{ox}}\left[\mathrm{~V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{ch}}(\mathrm{x})-\mathrm{V}_{\mathrm{tn}}\right] \mathrm{d} \mathrm{~V}_{\mathrm{ch}}=\int_{0}^{\mathrm{L}} \mathrm{I}_{\mathrm{D}} \mathrm{dx} \tag{1.183}
\end{equation*}
$$

image_name:Fig. 1.40
description:The image labeled "Fig. 1.40" is a cross-sectional schematic diagram of an n-channel MOSFET (Metal-Oxide-Semiconductor Field-Effect Transistor). It illustrates the transistor's structure and the flow of current through it.

Identification of Components and Structure:
1. **n+ Regions:** These are heavily doped n-type semiconductor regions that form the source and drain of the MOSFET.
2. **Gate (G):** Located above the channel, with a metal or polysilicon gate electrode separated from the substrate by a thin insulating layer (oxide).
3. **Channel:** The area between the source and drain where current flows when the MOSFET is active. It is controlled by the voltage applied to the gate.
4. **Depletion Region:** Shown as a shaded area, indicating regions where mobile charge carriers are depleted.
5. **Substrate:** The body of the transistor, typically connected to ground (GND).

Connections and Interactions:
- **Source (S) Voltage (V_S):** Set to 0V, indicating it is grounded.
- **Gate Voltage (V_G):** Greater than the threshold voltage (V_tn), allowing a channel to form and current to flow.
- **Drain Voltage (V_D):** Positive, indicating the direction of current flow from drain to source.
- **Current Flow (I_D):** Shown by an arrow indicating the flow of electrons (conventional current flows in the opposite direction).
- **Charge Distribution (Q_n(x)):** Represents the charge in the channel, which varies along the length of the channel.

Labels, Annotations, and Key Features:
- **"V_S = 0":** Indicates the source is grounded.
- **"V_G > V_tn":** Indicates the gate voltage is above the threshold, enabling the channel.
- **"V_D > 0":** Indicates a positive voltage at the drain, facilitating current flow.
- **"Increasing x":** Indicates the direction along the channel from source to drain.

This diagram is typically used to explain the operation of a MOSFET in the triode or linear region, where the gate voltage is sufficient to invert the channel and allow current to flow from the drain to the source.

Fig. 1.40 The transistor definitions used in developing the transistor's I-V relationship.
which results in

$$
\begin{equation*}
\mu_{\mathrm{n}} \mathrm{WC}_{\mathrm{ox}}\left[\left(\mathrm{~V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{tn}}\right) \mathrm{V}_{\mathrm{DS}}-\frac{\mathrm{V}_{\mathrm{DS}}^{2}}{2}\right]=\mathrm{I}_{\mathrm{D}} \mathrm{~L} \tag{1.184}
\end{equation*}
$$

Thus, solving for $I_{D}$ results in the well-known triode relationship for a MOS transistor:

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D}}=\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)\left[\left(\mathrm{V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{tn}}\right) \mathrm{V}_{\mathrm{DS}}-\frac{\mathrm{V}_{\mathrm{DS}}^{2}}{2}\right] \tag{1.185}
\end{equation*}
$$

It should be noted that taking into account the body effect along the channel, the triode model of (1.225) is modified to

$$
\begin{equation*}
\mathrm{I}_{\mathrm{D}}=\mu \mathrm{C}_{\mathrm{ox}}\left(\frac{\mathrm{~W}}{\mathrm{~L}}\right)\left[\left(\mathrm{V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{tn}}\right) \mathrm{V}_{\mathrm{DS}}-\alpha \frac{\mathrm{V}_{\mathrm{DS}}^{2}}{2}\right] \tag{1.186}
\end{equation*}
$$

where $\alpha \cong 1.7$ [Tsividis, 1987].

## 1.8 KEY POINTS

- The charge-voltage relationship of a reverse-biased pn junction is modeled by a nonlinear depletion capacitance. [p. 6]
- The source terminal of an n-channel transistor is defined as whichever of the two terminals has a lower voltage. For a p-channel transistor, the source would be the terminal with the higher voltage. [p. 14]
- The relationship between drain-source voltage and drain current of a MOS device is approximately linear when $V_{D S}<<V_{\text {eff: }}$ [p. 19]
- For $\mathrm{V}_{\mathrm{DS}}>\mathrm{V}_{\text {eff }}$, a MOS device exhibits a square-law current-voltage relationship. [p. 21]
- The body effect is the influence of the body potential on the channel, modelled as an increase in the threshold voltage, $\mathrm{V}_{\mathrm{tn}}$, with increasing source-to-body reverse-bias. [p. 24]
- The square-root relationship for transconductance is useful for circuit analysis when device sizes are fixed. However, the simpler expression $\mathrm{g}_{\mathrm{m}}=2 \mathrm{I}_{\mathrm{D}} / \mathrm{V}_{\text {eff }}$ is useful during initial circuit design when transistor sizes are yet to be determined. [p. 26]
- Small signal $r_{d s}$ is proportional to $L / I_{D}$. [p. 28]
- In a MOSFET, the largest parasitic capacitance is $\mathrm{C}_{\mathrm{gs}}$, proportional to gate area WL and via $\mathrm{C}_{\mathrm{ox}}$ inversely proportional to oxide thickness. [p. 31]
- The gate-drain capacitance $\mathrm{C}_{\mathrm{gd}}$, also known as the Miller capacitance, is due to physical overlap of the gate and drain regions as well as fringing fields. It is especially important when there is a large voltage gain between gate and drain. [p. 32]
- For operation with high gain, transistors should have long gate lengths and be biased with low $\mathrm{V}_{\text {eff }}$. For high speed, the opposite is desirable: small L and high $\mathrm{V}_{\mathrm{eff}}$ [p.38]
- In subthreshold operation, also called weak inversion, transistors obey an exponential voltage-current relationship instead of a square-law. Hence, a small but finite current flows even when $\mathrm{V}_{\mathrm{GS}}=0$. [p. 42]
- For a fixed drain current, the small-signal transconductance of a MOS device is maximized in subthreshold operation at a value of $\mathrm{g}_{\mathrm{m}}=\mathrm{qI}_{\mathrm{D}} / \mathrm{nkT}$. [p. 43]
- For large values of $\mathrm{V}_{\text {eff }}$, transistors have a sub-square-law voltage current relationship, tending towards a linear relationship for very large values of $\mathrm{V}_{\text {eff: }}$ [p.46]
