# 8 Bipolar Devices and Circuits

In the early electronic years, the majority of microcircuits were realized using bipolar-junction transistors (BJTs). However, in the late 1970s, microcircuits that used MOS transistors began to dominate the industry. Presently, the need for digital circuitry in nearly every modern integrated circuit has made CMOS devices and processing domiant, but bipolar devices remain important for many high-performance analog circuits. Modern bipolar-CMOS (BiCMOS) processes permit high performance bipolar devices to be integraed alongside large CMOS digital circuits, a particularly attractive option for mixed analog-digital applications. Thus, it remains important for an analog designer to become familiar with bipolar devices.

## 8.1 BIPOLAR-JUNCTION TRANSISTORS

Bipolar devices offer some inherent advantages over CMOS devices, particularly when a combination of high-frequency operation, high-gain, and/or high breakdown voltage are required. For example, in order to operate at very high speeds, modern CMOS technologies employ very thin gate dielectrics which breakdown under voltages exceeding 1-2 Volts, whereas bipolar devices can be engineered to combine high-speed operation and relatively high breakdown voltages, making them naturally suited to high-voltage

Key Point: Bipolar devices offer advantages over CMOS devices when high-speed operation must be combined with high gain and/ or high breakdown voltages. However, unlike MOSFETs, they draw a nonzero dc base current.
radio-frequency circuits. Moreover, since BJTs can tolerate larger voltage signal swings than short gate-length MOS transistors, they are also capable of higher dynamic range. Very short gate length MOS transistors also suffer from low intrinsic gain, whereas bipolar devices suffer from no such tradeoff. Unfortunately, in bipolar transistors, the base control terminal has a nonzero input current when the transistor is conducting current (from the collector to the emitter for an npn transistor; from the emitter to the collector for a pnp transistor). Fortunately, at low frequencies, the base current is much smaller than the collector-to-emitter cur-rent-it may be only $0.1-1 \%$ of the collector current for an npn transistor. For lateral pnp transistors, the base current may be as large as $1 / 20$ of the emitter-to-collector current.

A typical cross section of an npn bipolar-junction transistor is shown in Fig. 8.1. Although this structure looks quite complicated, it corresponds approximately to the equivalent structure shown in Fig. 8.2. In a good BJT transistor, the width of the base region, W , is small (typically, less than $1 \mu \mathrm{~m}$ ). Also, as we will see, the base must be more lightly doped than the emitter.

The circuit symbols used to represent npn and pnp transistors are shown in Fig. 8.3.

### 8.1.1 Basic Operation

To understand the operation of bipolar transistors, we consider here an npn transistor with the emitter connected to ground, as shown in Fig. 8.4. If the base voltage, $\mathrm{V}_{\mathrm{B}}$, is less than about 0.5 V , the transistor will be cut off, and
image_name:Fig. 8.1 A cross section of an npn bipolar-junction transistor.
description:The image depicts a cross-section of an npn bipolar-junction transistor, illustrating its internal structure and components. The transistor is composed of three main regions: the emitter, base, and collector.

1. **Identification of Components and Structure:**
- **Emitter:** Located on the right, it is labeled as 'n+' indicating a heavily doped n-type region. The emitter is connected to a metal contact.
- **Base:** Situated between the emitter and collector, the base is a 'p' type region, and it is less doped compared to the emitter. It is connected to a metal contact that surrounds the emitter contact to minimize base resistance.
- **Collector:** Found on the left, it is represented as 'n-' and 'n+' regions, indicating varying doping levels. The collector is also connected to a metal contact.
- **SiO2 Insulator (Field Oxide):** A layer of silicon dioxide insulates the collector from other components.
- **Buried Collector Region:** Labeled as 'n+', this region is below the collector and helps in efficient charge collection.
- **Substrate or Bulk:** The bottom layer is labeled 'p-', representing the substrate upon which the transistor is built.

2. **Connections and Interactions:**
- The metal contacts on the emitter, base, and collector facilitate electrical connections to external circuits.
- Arrows within the diagram indicate the direction of current flow, showing that electrons move from the emitter to the collector through the base.
- The base contact surrounds the emitter contact, which helps minimize resistance and improve efficiency.

3. **Labels, Annotations, and Key Features:**
- An annotation explains that the base contact surrounds the emitter to minimize resistance.
- The effective base region is marked, highlighting the area where the base region influences the transistor's operation.
- The diagram uses standard semiconductor labeling conventions ('n+', 'n-', 'p') to indicate doping levels and types.

Fig. 8.1 A cross section of an npn bipolar-junction transistor.
image_name:Fig. 8.2 A simplified structure of an npn transistor
description:The image labeled "Fig. 8.2 A simplified structure of an npn transistor" presents a cross-sectional view of an npn bipolar-junction transistor (BJT). The diagram is a simplified representation, focusing on the essential structural components and doping characteristics.

1. **Identification of Components and Structure:**
- The transistor is composed of three main regions: the emitter, base, and collector.
- The emitter region is labeled as 'n+', indicating that it is heavily doped with donor impurities, providing a high concentration of electrons.
- The base region is labeled as 'p', suggesting it is lightly doped with acceptor impurities, allowing for hole conduction.
- The collector region is divided into two parts: 'n-' and 'n+'. The 'n-' part is lightly doped, while the 'n+' part is heavily doped, facilitating efficient collection of electrons.

2. **Connections and Interactions:**
- Electrical connections are indicated by lines extending from the emitter, base, and collector regions. These lines represent terminals for connecting the transistor to external circuits.
- The arrow labeled 'W' across the base region denotes the width of the base, which is a critical parameter affecting the transistor's operation by influencing the recombination of charge carriers.

3. **Labels, Annotations, and Key Features:**
- The diagram uses standard semiconductor labeling conventions ('n+', 'n-', 'p') to indicate doping levels and types.
- Annotations such as "Emitter," "Base," and "Collector" clearly identify the different regions of the transistor.
- The base contact is shown to be centrally located and is surrounded by the emitter and collector, minimizing resistance and improving efficiency.

Fig. 8.2 A simplified structure of an npn transistor.
image_name:(a) npn
description:The diagram illustrates the structure and current flow of an npn transistor. The collector current I_C is typically 100 times the base current I_B, indicating a high current gain (β).
image_name:(b) pnp
description:The diagram shows the symbol for a PNP bipolar-junction transistor. The current relationships are indicated, with the emitter current (IE) and collector current (IC) shown flowing out of the transistor, and the base current (IB) flowing into the base. The typical current gain for a lateral PNP transistor is given as IC ≈ 20IB.

Fig. 8.3 The symbols representing (a) an npn bipolar-junction transistor and (b) a pnp bipolar-junction transistor.
image_name:Fig. 8.4
description:The diagram labeled "Fig. 8.4" illustrates the internal structure and current flow within an NPN bipolar-junction transistor. This schematic representation includes several key components and annotations:

1. **Components and Structure:**
- The transistor is divided into three regions: the **n+ emitter**, the **p base**, and the **n- collector**. These regions are depicted as horizontal layers, with the n+ and n- regions indicating heavily doped and lightly doped n-type semiconductor materials, respectively.
- The emitter is connected to ground, and the collector is connected to a voltage source, labeled as having a voltage greater than 0.3 V.

2. **Connections and Interactions:**
- **Electron Flow:** There is a large arrow labeled "Electrons" indicating the flow of electrons from the emitter towards the collector through the base. This represents the primary current flow within the transistor.
- **Hole Flow:** A smaller arrow labeled "Holes" indicates the flow of holes from the base towards the emitter.
- The base-emitter junction is forward-biased, as indicated by the voltage V_BE ≈ 0.7 V, allowing current to flow from the base to the emitter.
- The collector-emitter junction is reverse-biased with V_CE > 0.3 V, facilitating the flow of electrons from the collector to the emitter.

3. **Labels, Annotations, and Key Features:**
- **Depletion Regions:** The diagram shows depletion regions at the junctions between the base and the emitter, and the base and the collector. These are marked with brackets and arrows.
- **Voltage Annotations:** The forward bias voltage across the base-emitter junction is annotated as V_BE ≈ 0.7 V, and the collector-emitter voltage is annotated as V_CE > 0.3 V.
- The arrows and annotations clearly indicate the direction of electron and hole flow, which is crucial for understanding the transistor's operation as a current amplifier.

This diagram effectively demonstrates the concept of current amplification in an NPN transistor, with a focus on the flow of charge carriers and the biasing conditions necessary for operation.

Fig. 8.4 Various components of the currents of an npn transistor.
no current will flow. We will see that when the base-emitter pn junction becomes forward biased, current will start to flow from the base to the emitter, but, partly because the base width is small, a much larger proportional current will flow from the collector to the emitter. Thus, the npn transistor can be considered a current amplifier at low frequencies. In other words, if the transistor is not cut off and the collector-base junction is reverse biased, a small base current controls a much larger collector-emitter current.

A simplified overview of how an npn transistor operates follows. When the base-emitter junction becomes forward biased, it starts to conduct, similar to any forward- biased junction. The current consists of majority carriers from the base (in this case, holes) and majority carriers from the emitter (in this case, electrons) diffusing across the junction. Because the emitter is more heavily doped than the base, there are many more electrons injected from the emitter than there are holes injected from the base. Assuming the collector voltage is large enough so that the collector-base junction is reverse biased, no holes from the base will go to the collector. However, the electrons that travel from the emitter to the base, where they are now minority carriers, diffuse away from the base-emitter junction because of the minority-carrier concentration gradient in the base region. Any of these minority electrons that get close to the collector-base junction will immediately be "whisked" across the junction due to the large positive voltage on the collector, which attracts the negatively charged electrons. In a properly designed bipolar transistor, such as that shown in Fig. 8.1, the vertical base width, W, is small, and almost all of the electrons that diffuse from the emitter to the base reach the collector-base junction and are swept across the junction, thus contributing to current flow in the collector. The result is that the collector current very closely equals the electron current flowing from the emitter to the base. The much smaller base current very closely equals the current due to the holes that flow from the base to the emitter. The total emitter current is the sum of the electron collector current and the hole base current, but since the hole current is much smaller than the electron current, the emitter current is approximately equal to the collector current.

Since the collector current is approximately equal to the electron current flowing from the emitter to the base, and the amount of this electron current is determined by the base-emitter voltage, it can be shown (see Appendix at the end of this chapter) that the collector current is exponentially related to the base-emitter voltage by the relationship

$$
\begin{equation*}
\mathrm{I}_{\mathrm{C}} \cong \mathrm{I}_{\mathrm{CS}} \mathrm{e}^{\mathrm{V}_{\mathrm{BE}} / \mathrm{V}_{\mathrm{T}}} \tag{8.1}
\end{equation*}
$$

where $\mathrm{I}_{\mathrm{CS}}$ is the scale current. This scale current is proportional to the area of the base-emitter junction. The base current, determined by the hole current flowing from the base to the emitter, is also exponentially related to the
base-emitter voltage, resulting in the ratio of the collector current to the base current being a constant that, to a first-order approximation, is independent of voltage and current. This ratio, typically denoted $\beta$, is defined to be

$$
\begin{equation*}
\beta \equiv \frac{\mathrm{I}_{\mathrm{C}}}{\mathrm{I}_{\mathrm{B}}} \tag{8.2}
\end{equation*}
$$

where $I_{C}$ and $I_{B}$ are the collector and base currents. Typical values of $\beta$ are between 50 and 200. Lower values arise in lateral bipolar transistors, which are not optimized for high current gain, and higher values arise in heterojunction bipolar transistors.

Key Point: In active mode, with base-emitter junction forwardbiased and base-collector junction reverse-biased, collector current increases exponentially with baseemitter voltage, and the base current is a factor $\beta$ smaller. The variation in collector current with collector voltage is first-order modeled by the Early voltage.

Note that (8.1) implies that the collector current is independent of the collector voltage. This independence ignores second-order effects such as the decrease in effective base width, W , due to the increase in the width of the collector-base depletion region when the collector bias voltage is increased. To illustrate this point, a typical plot of the collector current, $\mathrm{I}_{\mathrm{C}}$, as a function of collector-to-emitter voltage, $\mathrm{V}_{\mathrm{CE}}$, for different values of $\mathrm{I}_{\mathrm{B}}$ is shown in Fig. 8.5 for a practical transistor. The fact that the curves are not flat for $\mathrm{V}_{\mathrm{CE}}>\mathrm{V}_{\mathrm{CE} \text {-sat }}$ indicates the dependence of $\mathrm{I}_{\mathrm{C}}$ on $\mathrm{V}_{\mathrm{CE}}$. Indeed, to a good approximation, the dependence is linear with a slope that intercepts the $V_{C E}$ axis at $V_{C E}=-V_{A}$ for all values of $I_{B}$. The intercept voltage value, $V_{A}$,
is called the Early voltage for bipolar transistors, with a typical value being from 50 V to 100 V . This dependency results in a finite output impedance (as in a MOS transistor) and can be modelled by modifying equation (8.1) [Sze, 1981] to be

$$
\begin{equation*}
\mathrm{I}_{\mathrm{C}} \cong \mathrm{I}_{\mathrm{CS}} \mathrm{e}^{\mathrm{V}_{\mathrm{BE}} \mathrm{~V}_{\mathrm{T}}}\left(1+\frac{\mathrm{V}_{\mathrm{CE}}}{\mathrm{~V}_{\mathrm{A}}}\right) \tag{8.3}
\end{equation*}
$$

#### Large-Signal Modelling

A conducting BJT that has a $\mathrm{V}_{\text {CE }}$ greater than $\mathrm{V}_{\mathrm{CE} \text {-sat }}$ (which is approximately 0.3 V ) is said to be operating in the active region. Such a collector-emitter voltage is required to ensure that none of the holes from the base go to the collector. A large-signal model of a BJT operating in the active region is shown in Fig. 8.6.

Since $I_{B}=I_{C} / \beta$, we have

$$
\begin{equation*}
I_{B}=\frac{I_{\mathrm{CS}}}{\beta} e^{v_{B E} / v_{T}}=I_{B S} e^{v_{B E} / V_{T}} \tag{8.4}
\end{equation*}
$$

image_name:Fig. 8.5 Typical plot of I_C versus V_CE for a BJT
description:The graph depicted is a typical plot of the collector current ($I_C$) versus the collector-emitter voltage ($V_{CE}$) for a Bipolar Junction Transistor (BJT). It is a family of curves representing different base currents ($I_B$), although the specific base currents are not labeled on the graph.

1. **Type of Graph and Function:**
- This is a characteristic curve graph for a BJT, illustrating how the collector current varies with the collector-emitter voltage.

2. **Axes Labels and Units:**
- The x-axis represents the collector-emitter voltage ($V_{CE}$) in volts.
- The y-axis represents the collector current ($I_C$) in amperes.
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The curves start from a point near the origin and initially rise steeply as $V_{CE}$ increases from 0 volts.
- After an initial increase, each curve levels off, indicating saturation of the collector current for a given base current.
- As $V_{CE}$ continues to increase, the curves show a slight upward trend, indicating the active region of the BJT.
- A vertical dashed line is present at $V_{CE} \approx 0.3$ V, indicating the saturation voltage ($V_{CE-sat}$).

4. **Key Features and Technical Details:**
- The region to the left of the $V_{CE-sat}$ line is the saturation region, where the BJT is fully on.
- Beyond the initial steep increase, the flat portions of the curves represent the active region, where the BJT operates linearly.
- The rightmost part of the curves approaches the transistor breakdown region, as indicated by the dashed vertical line.

5. **Annotations and Specific Data Points:**
- The graph includes an annotation for the transistor breakdown region, which is beyond a certain $V_{CE}$ value where the curves show an abrupt increase, indicating potential damage to the BJT if operated in this region.
- The $V_{CE-sat}$ point is marked at approximately 0.3 V, a critical value for determining the transition from saturation to the active region.

Fig. 8.5 Typical plot of $I_{C}$ versus $V_{C E}$ for a BJT.
image_name:Fig. 8.6
description:The diagram represents a large-signal model for a BJT in the active region. The diode models the base-emitter junction, and the voltage-controlled current source models the collector current proportional to the base current.

Fig. 8.6 A large-signal model for a BJT in the active region.
which is similar to a diode equation, but with a multiplying constant of $I_{C S} / \beta=I_{B S}$. Since $I_{E}=I_{B}+I_{C}$, we have

$$
\begin{equation*}
I_{E}=I_{C S}\left(\frac{\beta+1}{\beta}\right) e^{V_{B E} / V_{T}}=I_{E S} e^{V_{B E} / V_{T}} \tag{8.5}
\end{equation*}
$$

or equivalently

$$
\begin{equation*}
\mathrm{I}_{\mathrm{C}}=\alpha \mathrm{I}_{\mathrm{E}} \tag{8.6}
\end{equation*}
$$

where $\alpha$ has been defined as

$$
\begin{equation*}
\alpha=\frac{\beta}{\beta+1} \tag{8.7}
\end{equation*}
$$

and for large values of $\beta$, can be approximated as

$$
\begin{equation*}
\alpha \cong 1-\frac{1}{\beta} \cong 1 \tag{8.8}
\end{equation*}
$$

If the effect of $V_{C E}$ on $I_{C}$ is included in the model, the current-controlled source, $\beta I_{B}$, should be replaced by a current source given by

$$
\begin{equation*}
\mathrm{I}_{\mathrm{C}}=\beta \mathrm{I}_{\mathrm{B}}\left(1+\frac{\mathrm{V}_{\mathrm{CE}}}{\mathrm{~V}_{\mathrm{A}}}\right) \tag{8.9}
\end{equation*}
$$

where $\mathrm{V}_{\mathrm{A}}$ is the Early-voltage constant. This additional modeling of the finite output impedance is normally not done in large-signal analysis without the use of a computer due to its complexity.

As the collector-emitter voltage approaches $\mathrm{V}_{\text {CE-sat }}$ (typically around 0.2 to 0.3 V ), the base-collector junction becomes forward biased, and holes from the base will begin to diffuse to the collector. A common model for this case, when the transistor is saturated or in the saturation region, is shown in Fig. 8.7. It should be noted that the value of $\mathrm{V}_{\mathrm{CE} \text {-sat }}$ decreases for smaller values of collector current.

Key Point: As the base-collector junction approaches forward-bias, at collector-emitter voltages of about 0.2 to 0.3 V , a finite basecollector current flows, and the transistor is saturated.

#### Base-Charge Storage in the Active Region

When a transistor is in the active region, many minority carriers are stored in the base region (electrons are stored in an npn transistor). Recall that this minority charge is responsible for $\mathrm{I}_{\mathrm{C}}$, so this charge must be removed (through the base contact) before a transistor can turn off. As in a forward-bias diode, this charge can be modelled as a diffusion capacitance, $C_{d}$, between the base and emitter given by (see Appendix at the end of this chapter)

$$
\begin{equation*}
\mathrm{C}_{\mathrm{d}}=\tau_{\mathrm{b}} \frac{\mathrm{I}_{\mathrm{C}}}{\mathrm{~V}_{\mathrm{T}}} \tag{8.10}
\end{equation*}
$$

where $\tau_{\mathrm{b}}$ is the base-transit-time constant. Thus, we see that the diffusion capacitance is proportional to $\mathrm{I}_{\mathrm{C}}$. The total base-emitter capacitance, $\mathrm{C}_{\mathrm{be}}$, will include the base-emitter depletion capacitance, $\mathrm{C}_{\mathrm{j}}$, in parallel with $\mathrm{C}_{\mathrm{d}}$. Normally, however, $\mathrm{C}_{\mathrm{j}}$ is much less than $\mathrm{C}_{\mathrm{d}}$, unless the transistor current is small, and can often be ignored.

#### Base-Charge Storage of a Saturated Transistor

When a transistor becomes saturated, the minority-charge storage in the base and, even more so, in the lightly doped region of the collector, increases drastically. The major component of this charge storage is due to holes diffusing from the base, through the collector junction, and continuing on through the lightly doped $\mathrm{n}^{-}$epitaxial region of the collector to the $\mathrm{n}^{+}$collector region. The $\mathrm{n}^{-}$epitaxial region is so named because it is epitaxially grown on a p region. Most of the charge storage occurs in this region. Also, additional charge storage occurs because electrons that diffused from the collector are stored in the base, but this charge is normally smaller. The magnitude of the additional charge stored by a transistor that is saturated is given by

$$
\begin{equation*}
Q_{s}=\tau_{s}\left(I_{B}-\frac{I_{C}}{\beta}\right) \tag{8.11}
\end{equation*}
$$

where the base overdrive current, defined to be $I_{B}-I_{C} / \beta$, is approximately equal to the hole current from the base to the collector. Normally, in saturation, $\mathrm{I}_{\mathrm{B}}>>\mathrm{I}_{\mathrm{C}} / \beta$, and (8.11) can be approximated by

$$
\begin{equation*}
\mathrm{Q}_{\mathrm{s}} \cong \tau_{\mathrm{s}} \mathrm{I}_{\mathrm{B}} \tag{8.12}
\end{equation*}
$$

The constant $\tau_{\mathrm{s}}$ is approximately equal to the epitaxial-region transit time, $\tau_{\mathrm{E}}$ (ignoring the storage of electrons in the base that diffused from the collector). Since the epitaxial region is much wider than the base, the constant $\tau_{\mathrm{s}}$ is normally much larger than the base transit time, the constant $\tau_{\mathrm{b}}$, often by up to two orders of magnitude. The specific value of $\tau_{\mathrm{s}}$ is usually found empirically for a given technology.

When a saturated transistor is being turned off, first the base current will reverse. However, before the collector current will change, the saturation char ge, $\mathrm{Q}_{\mathrm{s}}$, must be $r$ emoved. After $\mathrm{Q}_{\mathrm{s}}$ is removed, the base minority charge, $Q_{b}$, will be removed. During this time, the collector current will decrease until the transistor shuts off. Typically, the time to remove $Q_{S}$ greatly dominates the overall charge removal.

If the time required to remove the base saturation charge, $\mathrm{t}_{\mathrm{s}}$, is much shorter than the epitaxial-region transit time, $\tau_{\mathrm{E}}$, then one can derive a simple expression for the time required to remove the saturation charge. If the reverse base current (when the saturation charge is being removed), denoted by $I_{B R}$, remains constant while $Q_{S}$ is being removed, then we have [Hodges, 1988]

$$
\begin{equation*}
\mathrm{t}_{\mathrm{s}} \cong \frac{\mathrm{Q}_{\mathrm{s}}}{\mathrm{I}_{\mathrm{BR}}} \cong \frac{\tau_{\mathrm{s}}\left(\mathrm{I}_{\mathrm{B}}-\frac{\mathrm{I}_{\mathrm{C}}}{\beta}\right)}{\mathrm{I}_{\mathrm{BR}}} \cong \tau_{\mathrm{s}} \frac{\mathrm{I}_{\mathrm{B}}}{\mathrm{I}_{\mathrm{BR}}} \tag{8.13}
\end{equation*}
$$

where $\tau_{\mathrm{s}} \cong \tau_{\mathrm{E}}$.
image_name:Fig. 8.7
description:The circuit diagram represents a large-signal model for a BJT in the saturation region. The diagram shows the base current (IB), collector current (IC), and emitter current (IE) with the relationship IE = IC + IB. It also includes the voltage across the collector-emitter junction in saturation (VCE-sat ≈ 0.3V) and the diode equation for the base current IB = IBSe^(VBE/VT).

Fig. 8.7 A large-signal model for a BJT in the saturation region.

Normally, the forward base current during saturation, $\mathrm{I}_{\mathrm{B}}$, will be much smaller than the reverse base current during saturation-charge removal, $\mathrm{I}_{\mathrm{BR}}$. If this were not the case, then our original assumption that $\mathrm{t}_{\mathrm{S}} \ll \tau_{\mathrm{E}} \cong \tau_{\mathrm{S}}$ would not be true. In this case, the turn-off time of the BJT would be so slow as to make the circuit unusable in most applications. Nevertheless, the turn-off time for this case, when $\mathrm{t}_{\mathrm{S}}$ is not much less than $\tau_{\mathrm{E}}$, is given by [Hodges, 1988]

$$
\begin{equation*}
\mathrm{t}_{\mathrm{s}}=\tau_{\mathrm{s}} \ln \left[\frac{\mathrm{I}_{\mathrm{BR}}+\mathrm{I}_{\mathrm{B}}}{\mathrm{I}_{\mathrm{BR}}+\frac{\mathrm{I}_{\mathrm{C}}}{\beta}}\right] \tag{8.14}
\end{equation*}
$$

The reader should verify that for $I_{B R} \gg I_{B}$ and $I_{B R} \gg I_{C} / \beta$, the expression in (8.14) is approximately equivalent to the much simpler one in (8.13).

In both of the cases just described, the time required to remove the storage charge of a saturated transistor is much larger than the time required to turn off a transistor in the active region. In high-speed microcircuit designs, one never allows bipolar transistors to saturate, to avoid the long turn-off time that would result.

Key Point: The time required to remove the charge stored in a saturated transistor is much larger than the time required to turn off a transistor in the active region. Hence, in high-speed microcircuit designs, one never allows bipolar transistors to saturate.

#### EXAMPLE 8.1

For $\tau_{\mathrm{b}}=0.2 \mathrm{~ns}, \tau_{\mathrm{s}}=100 \mathrm{~ns}$ (a small value for $\tau_{\mathrm{s}}$ ), $\mathrm{I}_{\mathrm{B}}=0.2 \mathrm{~mA}, \mathrm{I}_{\mathrm{C}}=1 \mathrm{~mA}, \beta=100$, and $\mathrm{I}_{\mathrm{BR}}=1 \mathrm{~mA}$, calculate the time required to remove the base saturation charge using (8.13), and compare it to the time obtained using the more accurate expression of (8.14). Compare these results to the time required to remove the base minority charge for the same $I_{B R}$.

#### Solution

Using (8.13), we have

$$
\begin{equation*}
\mathrm{t}_{\mathrm{s}}=\frac{10^{-7}\left(2 \times 10^{-4}\right)}{10^{-3}}=20 \mathrm{~ns} \tag{8.15}
\end{equation*}
$$

Using (8.14), we have

$$
\begin{equation*}
\mathrm{t}_{\mathrm{s}}=10^{-7} \ln \left[\frac{10^{-3}+2 \times 10^{-4}}{10^{-3}+\frac{10^{-3}}{100}}\right]=17.2 \mathrm{~ns} \tag{8.16}
\end{equation*}
$$

which is fairly close to the first result.
The time required for an active transistor to remove the base minority charge, $Q_{b}$, is given by

$$
\begin{equation*}
\mathrm{t}_{\mathrm{A}}=\frac{\mathrm{Q}_{\mathrm{b}}}{\mathrm{I}_{\mathrm{BR}}}=\frac{\tau_{\mathrm{b}} \mathrm{I}_{\mathrm{C}}}{\mathrm{I}_{\mathrm{BR}}}=0.2 \mathrm{~ns} \tag{8.17}
\end{equation*}
$$

This is approximately 100 times shorter than the time for removing the base saturation charge!

#### Small-Signal Modelling

The most commonly used small-signal model is the hybrid- $\pi$ model. This model is similar to the small-signal model used for MOS transistors, except it includes a finite base-emitter impedance, $\mathrm{r}_{\pi}$, and it has no emitter-tobulk capacitance. The hybrid- $\pi$ model is shown in Fig. 8.8. As in the MOS case, we will first discuss the transconductance, $\mathrm{g}_{\mathrm{m}}$, and the small-signal resistances, and then we will discuss the parasitic capacitances.

The transistor transconductance, $g_{m}$, is perhaps the most important parameter of the small-signal model. The transconductance is the ratio of the small-signal collector current, $i_{c}$, to the small-signal base-emitter voltage, $v_{b e}$. Thus, we have

$$
\begin{equation*}
g_{m}=\frac{i_{c}}{v_{b e}}=\frac{\partial I_{C}}{\partial V_{B E}} \tag{8.18}
\end{equation*}
$$

Recall that in the active region

$$
\begin{equation*}
I_{C}=I_{C S} e^{v_{B E} / v_{T}} \tag{8.19}
\end{equation*}
$$

Then

$$
\begin{equation*}
g_{m}=\frac{\partial I_{C}}{\partial V_{B E}}=\frac{\mathrm{I}_{\mathrm{CS}}}{\mathrm{~V}_{\mathrm{T}}} e^{\mathrm{V}_{\mathrm{BE}} / \mathrm{V}_{\mathrm{T}}} \tag{8.20}
\end{equation*}
$$

Using (8.19) again, we obtain

$$
\begin{equation*}
g_{m}=\frac{I_{C}}{V_{T}} \tag{8.21}
\end{equation*}
$$

where $V_{T}$ is given by

$$
\begin{equation*}
V_{T}=\frac{k T}{q} \tag{8.22}
\end{equation*}
$$

Key Point: BJT smallsignal transconductance is proportional to collector current.
and is approximately 26 mV at a room temperature of $\mathrm{T}=300 \mathrm{~K}$. Thus, the transconductance is proportional to the bias current of a BJT. In integrated-circuit design, it is important that the transconductance (which determines the bandwidth of many circuits) remains temperature independent, so the bias currents are usually made proportional to absolute temperature (since $\mathrm{V}_{\mathrm{T}}$ is proportional to absolute temperature).

The presence of the resistor $r_{\pi}$ reflects the fact that the base current is nonzero. We have

$$
\begin{equation*}
\mathrm{r}_{\pi}=\frac{\partial \mathrm{V}_{\mathrm{BE}}}{\partial \mathrm{I}_{\mathrm{B}}} \tag{8.23}
\end{equation*}
$$

image_name:Fig. 8.8 The small-signal model of an active BJT
description:This circuit is the small-signal model of an active BJT, showing the base, collector, and emitter connections. It includes resistors, capacitors, and a voltage-controlled current source for modeling the transistor's behavior.

Fig. 8.8 The small-signal model of an active BJT.

Because from (8.4) we have

$$
\begin{equation*}
\mathrm{I}_{\mathrm{B}}=\frac{\mathrm{I}_{\mathrm{C}}}{\beta}=\frac{\mathrm{I}_{\mathrm{CS}}}{\beta} e^{\mathrm{V}_{\mathrm{BE}} \mathrm{~V}_{\mathrm{T}}} \tag{8.24}
\end{equation*}
$$

we therefore have

$$
\begin{equation*}
\frac{1}{r_{\pi}}=\frac{\partial \mathrm{I}_{\mathrm{B}}}{\partial \mathrm{~V}_{\mathrm{BE}}}=\frac{\mathrm{I}_{\mathrm{CS}}}{\beta \mathrm{~V}_{\mathrm{T}}} \mathrm{e}^{\mathrm{v}_{\mathrm{BE}} / \mathrm{V}_{\mathrm{T}}} \tag{8.25}
\end{equation*}
$$

Using (8.24) again, we have

$$
\begin{equation*}
\mathrm{r}_{\pi}=\frac{\mathrm{V}_{\mathrm{T}}}{\mathrm{I}_{\mathrm{B}}} \tag{8.26}
\end{equation*}
$$

or equivalently,

$$
\begin{equation*}
r_{\pi}=\beta \frac{V_{T}}{I_{C}}=\frac{\beta}{g_{m}} \tag{8.27}
\end{equation*}
$$

Since

$$
\begin{equation*}
i_{e}=i_{c}+i_{b} \tag{8.28}
\end{equation*}
$$

we also have

$$
\begin{align*}
\frac{\partial \mathrm{I}_{\mathrm{E}}}{\partial \mathrm{~V}_{\mathrm{BE}}} & =\frac{\partial \mathrm{I}_{\mathrm{c}}}{\partial \mathrm{~V}_{\mathrm{BE}}}+\frac{\partial \mathrm{I}_{\mathrm{B}}}{\partial \mathrm{~V}_{\mathrm{BE}}} \\
& =\mathrm{g}_{\mathrm{m}}+\frac{\mathrm{g}_{\mathrm{m}}}{\beta} \\
& =\mathrm{g}_{\mathrm{m}}\left(\frac{1+\beta}{\beta}\right)  \tag{8.29}\\
& =\frac{\mathrm{g}_{\mathrm{m}}}{\alpha}
\end{align*}
$$

Continuing, we have

$$
\begin{equation*}
\frac{1}{r_{0}}=\frac{\partial \mathrm{I}_{\mathrm{C}}}{\partial \mathrm{~V}_{\mathrm{CE}}} \tag{8.30}
\end{equation*}
$$

The small-signal resistance, $r_{0}$, models the dependence of the collector current on the collector-emitter voltage. Repeating (8.3) here for convenience,

$$
\begin{equation*}
I_{C}=I_{C S} e^{v_{B E} V_{T}}\left(1+\frac{V_{C E}}{V_{A}}\right) \tag{8.31}
\end{equation*}
$$

we have

$$
\begin{equation*}
\frac{1}{r_{0}}=\frac{\partial \mathrm{I}_{\mathrm{C}}}{\partial \mathrm{~V}_{\mathrm{CE}}}=\frac{\mathrm{I}_{\mathrm{CS}}}{\mathrm{~V}_{\mathrm{A}}} e^{\mathrm{V}_{\mathrm{BE}} \mathrm{~V}_{\mathrm{T}}} \tag{8.32}
\end{equation*}
$$

Thus,

$$
\begin{equation*}
r_{0}=\frac{V_{A}}{I_{C}} \tag{8.33}
\end{equation*}
$$

which is inversely proportional to the collector current.
The resistor $r_{b}$ models the resistance of the semiconductor material between the base contact and the effective base region due to the moderately lightly doped base p material (see Fig. 8.1). This resistor, although small
image_name:Fig. 8.9
description:This is a high-frequency, small-signal T model for an active BJT, incorporating resistors and capacitors to model the transistor's behavior. The circuit includes a voltage-controlled current source to represent the transconductance of the BJT.

Fig. 8.9 A high-frequency, small-signal T model for an active BJT.
(typically a few hundred ohms or less), can be important in limiting the speed of very-high-frequency low-gain BJT circuits and is a major source of noise.

The hybrid- $\pi$ model is only one of a number of small-signal models that can be used. One common alternative is the $T$ model shown in Fig. 8.9. It incorporates an emitter resistance, $r_{e}$, where

$$
\begin{equation*}
r_{e}=\frac{\partial V_{B E}}{\partial I_{E}}=\frac{\alpha}{g_{m}} \tag{8.34}
\end{equation*}
$$

Use of this T model can result in simplified analysis when the emitter is not at small-signal ground.

#### EXAMPLE 8.2

For $I_{C}=1 \mathrm{~mA}, \beta=100$, and $V_{A}=100 \mathrm{~V}$, calculate $g_{m}, r_{\pi}, r_{e}, r_{0}$, and $g_{m} r_{0}$.

#### Solution

We have

$$
\begin{gather*}
g_{m}=\frac{I_{C}}{V_{T}}=\frac{10 \times 10^{-3} \mathrm{~A}}{0.026 \mathrm{~V}}=38.5 \mathrm{~mA} / \mathrm{V}  \tag{8.35}\\
r_{\pi}=\frac{\beta}{g_{m}}=2.6 \mathrm{k} \Omega  \tag{8.36}\\
r_{e}=\frac{\alpha}{g_{m}}=\left(\frac{100}{101}\right) 26=25.7 \Omega  \tag{8.37}\\
r_{0}=\frac{V_{A}}{I_{C}}=\frac{100}{10^{-3}}=100 \mathrm{k} \Omega \tag{8.38}
\end{gather*}
$$

The high-frequency operation of a BJT is limited by the capacitances of the small-signal model. We have already encountered one of these capacitances in Section 8.1.1: that of the forward-biased base-emitter junction, $\mathrm{C}_{\mathrm{be}}$. Recapping, we have

$$
\begin{equation*}
C_{b e}=C_{j}+C_{d} \tag{8.39}
\end{equation*}
$$

where $C_{j}$ is the depletion capacitance of the base-emitter junction. For a forward-biased junction, a rough approximation for $C_{j}$ is

$$
\begin{equation*}
C_{j} \cong 2 A_{E} C_{j e 0} \tag{8.40}
\end{equation*}
$$

The diffusion capacitance, $\mathrm{C}_{\mathrm{d}}$, is given in (8.10) as

$$
\begin{equation*}
C_{d}=\tau_{b} \frac{I_{C}}{V_{T}}=g_{m} \tau_{b} \tag{8.41}
\end{equation*}
$$

Detailed expressions for $\tau_{b}$ are deried in the Appendix to this chapter. The capacitor, $\mathrm{C}_{\mathrm{cb}}$, models the depletion capacitance of the collector-base junction. Since this is a graded junction, we can approximate $\mathrm{C}_{\mathrm{cb}}$ by

$$
\begin{equation*}
\mathrm{C}_{\mathrm{cb}}=\frac{\mathrm{A}_{\mathrm{C}} \mathrm{C}_{\mathrm{jc} 0}}{\left(1+\frac{\mathrm{V}_{\mathrm{CB}}}{\Phi_{\mathrm{c} 0}}\right)^{1 / 3}} \tag{8.42}
\end{equation*}
$$

where $A_{C}$ is the effective area of the collector-base interface.
Due to the lower doping levels in the base and especially in the collector (perhaps $5 \times 10^{22}$ acceptors $/ \mathrm{m}^{3}$ and $10^{21}$ donors $/ \mathrm{m}^{3}$, respectively), $\Phi_{\mathrm{c} 0}$, the built-in potential for the collector-base junction, will be less than that of the base-emitter junction (perhaps 0.75 V as opposed to 0.9 V ). It should be noted that the cross-sectional area of the collector-base junction, $A_{C}$, is typically much larger than the effective area of the base-emitter junction, $A_{E}$, which is shown in Fig. 8.1. This size differential results in $\mathrm{A}_{C} \mathrm{C}_{\mathrm{j} \mathbf{c} 0}$ being larger than

Key Point: The high-frequency operation of active BJTs is limited by capacitances modeling charge storage in the depletion regions and the storage of diffusing charge-carriers in the base.
$\mathrm{A}_{\mathrm{E}} \mathrm{C}_{\mathrm{je} 0}$, the base-emitter junction capacitance at 0 V bias, despite the lower doping levels.

Finally, another large capacitor is $\mathrm{C}_{\mathrm{cS}}$, the capacitance of the collector-to-substrate junction. Since this area is quite large, $\mathrm{C}_{\mathrm{cS}}$, which is the depletion capacitance that results from this area, will be much larger than either $\mathrm{C}_{\mathrm{cb}}$ or the depletion capacitance component of $\mathrm{C}_{\mathrm{be}}$, that is, $\mathrm{C}_{\mathrm{j}}$. The value of $\mathrm{C}_{\mathrm{cs}}$ can be calculated using

$$
\begin{equation*}
C_{\mathrm{cs}}=\frac{\mathrm{A}_{\mathrm{T}} \mathrm{C}_{\mathrm{js} 0}}{\left(1+\frac{\mathrm{V}_{\mathrm{Cs}}}{\Phi_{\mathrm{s} 0}}\right)^{1 / 2}} \tag{8.43}
\end{equation*}
$$

where $A_{T}$ is the effective transistor area and $C_{j s 0}$ is the collector-to-substrate capacitance per unit area at $0-\mathrm{V}$ bias voltage.

### 8.1.2 Analog Figures of Merit

The intrinsic gain of a bipolar transistor, $A_{i}$, as with MOS transistors, is the maximum possible gain achievable using that single transistor and is given by

$$
\begin{equation*}
A_{i}=g_{m} r_{o}=V_{A} / V_{T} \tag{8.44}
\end{equation*}
$$

Key Point: Active BJTs offer an intrinsic gain that is generally higher than that of MOS transistors and independent of operating point.

Hence, the intrinsic gain of a bipolar transistor is a constant value independent of the transistor operating point. This is fundamentally different than a MOS transistor, whose intrinsic gain was shown in equation (1.115) $\mathrm{A}_{\mathrm{i}} \cong 2 / \lambda \mathrm{V}_{\text {eff }}$ to decrease with increasing bias current. The intrinsic gain of a npn BJT is usually between 2000 and 8000.

#### EXAMPLE 8.3

Find the maximum possible gain of a single-transistor amplifier using the transistor in Example 8.2.

#### Solution

The maximum gain is given by $\mathrm{g}_{\mathrm{m}} \mathrm{r}_{\mathrm{o}}$,

$$
\begin{equation*}
g_{m} r_{o}=\frac{V_{A}}{V_{T}}=3,846 \tag{8.45}
\end{equation*}
$$

Note that this gain is much higher than the 32.9 that was found for a single MOS transistor in Example 1.15. Also note that this BJT maximum gain is independent of the bias current. For MOS transistors, equation (1.115) shows that the maximum gain is inversely proportional to $\mathrm{V}_{\text {eff }}$ and, hence, inversely proportional to the square-root of its bias current. This is one of the reasons why it is possible to realize a single-transistor BJT amplifier with a much larger gain than would result if a MOS transistor were used, especially at high current levels (and therefore at high frequencies).

A common indicator for the speed of a BJT is the frequency at which the transistor's current gain drops to unity, when its collector is connected to a small-signal ground. This frequency is denoted $\mathrm{f}_{\mathrm{t}}$ and is called the transistor unity-gain frequency or cutoff frequency. We can see how this frequency is related to the transistor model parameters by analyzing the small-signal circuit of Fig. 8.10. In the simplified model in Fig. 8.10(b), the resistor
image_name:(a)
description:The circuit diagram (a) represents a small-signal model used to find the unity-gain frequency f_t of a BJT. It includes a current source Iin driving the base, with resistors rb and rπ, capacitors Cbe, Ccb, and Ccs, and a voltage-controlled current source gmvbe representing the transconductance.
image_name:(b)
description:The circuit is a simplified small-signal model to analyze the cutoff frequency (f_t) of a BJT. It includes a current source, capacitors, a resistor, and a voltage-controlled current source.

Fig. 8.10 (a) A small-signal model used to find $\mathrm{f}_{\mathrm{t}}$; (b) an equivalent simplified model.
$r_{b}$ is ignored because it has no effect on $i_{b}$ since the circuit is being driven by a perfect current source. We have

$$
\begin{equation*}
\mathrm{V}_{\mathrm{be}}=\mathrm{i}_{\mathrm{b}}\left(\mathrm{r}_{\pi}\left\|\frac{1}{s \mathrm{C}_{\mathrm{be}}}\right\| \frac{1}{\mathrm{sC}}\right) \tag{8.46}
\end{equation*}
$$

and

$$
\begin{equation*}
\mathrm{i}_{\mathrm{c}}=\mathrm{g}_{\mathrm{m}} \mathrm{~V}_{\mathrm{be}} \tag{8.47}
\end{equation*}
$$

Solving for $i_{c} / i_{b}$ gives

$$
\begin{equation*}
\frac{i_{c}}{i_{b}}=\frac{g_{m} r_{\pi}}{1+s\left(C_{b e}+C_{c b}\right) r_{\pi}} \tag{8.48}
\end{equation*}
$$

At low frequencies, the current gain is $g_{m} r_{\pi}$, which equals the expected value of $\beta$ using (8.27). At high frequencies, $i_{c} / i_{b}$ is approximately given by

$$
\begin{equation*}
\left|\frac{i_{c}}{i_{b}}(\omega)\right| \cong \frac{g_{m} r_{\pi}}{\omega\left(C_{b e}+C_{c b}\right) r_{\pi}}=\frac{g_{m}}{\omega\left(C_{b e}+C_{c b}\right)} \tag{8.49}
\end{equation*}
$$

To find the unity-gain frequency, we set $\left|\left(\mathrm{i}_{\mathrm{c}} / \mathrm{i}_{\mathrm{b}}\right)\left(\omega_{\mathrm{t}}\right)\right|=1$ and solve for $\omega_{\mathrm{t}}$, which results in

$$
\begin{equation*}
\omega_{\mathrm{t}}=\frac{g_{\mathrm{m}}}{\mathrm{C}_{\mathrm{be}}+\mathrm{C}_{\mathrm{cb}}} \tag{8.50}
\end{equation*}
$$

or

$$
\begin{equation*}
f_{t}=\frac{g_{m}}{2 \pi\left(C_{b e}+C_{c b}\right)} \tag{8.51}
\end{equation*}
$$

Substituting (8.21) and (8.39) into (8.51) yields

$$
\begin{equation*}
f_{t}=\left[2 \pi\left(\frac{\left(C_{b e}+C_{c b}\right) V_{T}}{I_{C}}+\tau_{b}\right)\right]^{-1} \tag{8.52}
\end{equation*}
$$

Finally, using the expression (8.102) for the transit time of the base from the Appendix gives

$$
\begin{equation*}
f_{t}=\left[2 \pi\left(\frac{\left(C_{b e}+C_{c b}\right) V_{T}}{I_{C}}+\frac{W^{2}}{2 D_{n}}\right)\right]^{-1} \tag{8.53}
\end{equation*}
$$

This expression neglects some other charge storage effects, but captures the most important terms. At low collector currents, the unity-gain frequency is dominated by the terms inversely proportional to $\mathrm{I}_{\mathrm{C}}$. As collector current increases, those terms diminish and $f_{t}$ increases up to a limit imposed by the base transit time constant, $\tau_{b}$

$$
\begin{equation*}
\mathrm{f}_{\mathrm{t}, \max } \approx \frac{1}{2 \pi} \cdot \frac{2 \mathrm{D}_{\mathrm{n}}}{\mathrm{~W}^{2}} \tag{8.54}
\end{equation*}
$$

where $D_{n}$ is the diffusion constant of minority carriers in the base, $\left(\mu_{\mathrm{n}} \mathrm{kT}\right) / \mathrm{q}$, and W is the width of the base region. Clearly, the width of the base region is a critical dimension influencing the high-speed performance of a bipolar transistor, analogous to the length of a MOSFET gate. Often, either $\mathrm{f}_{\mathrm{t}}, \omega_{\mathrm{t}}$, or $\tau_{\mathrm{t}}=1 / \omega_{\mathrm{t}}$ will be specified for a transistor at a particular bias current. These values are representative of an upper limit on the maximum frequency at which the transistor can be effectively used at that bias current.

Not captured by (8.53) are speed-limiting effects that arise at high cur-

Key Point: BJT unity-gain frequency increases in proportion to bias current up to a limit imposed by the transit time of carriers through the base. Hence, the base thickness is a critical parameter limiting the maximum operating speed of a BJT.
rent densities. For example, at high current densities the concentration of charge carriers passing through the base becomes so high that it moves the effective edge of the base region further towards and even into the collector. Doing so increases the effective width of the base, W, resulting in an

Fig. 8.11 A sketch of transistor $f_{t}$ versus collector current, $I_{C}$.
image_name:Fig. 8.11
description:The graph in Fig. 8.11 is a plot of the transition frequency, denoted as $f_t$, versus the collector current, $I_C$, for a bipolar junction transistor (BJT). This is a typical curve used to illustrate the relationship between these two parameters in semiconductor devices.

1. **Type of Graph and Function:**
- The graph is a plot of $f_t$ (transition frequency) against $I_C$ (collector current).

2. **Axes Labels and Units:**
- The vertical axis represents the transition frequency ($f_t$) and is typically measured in hertz (Hz).
- The horizontal axis represents the collector current ($I_C$), usually measured in amperes (A).
- The scales of the axes are not explicitly marked, but the graph typically uses linear scales for both axes.

3. **Overall Behavior and Trends:**
- The graph starts at the origin, indicating that at zero collector current, the transition frequency is zero.
- As the collector current increases, the transition frequency $f_t$ also increases, reaching a peak value.
- Beyond this peak, $f_t$ begins to decrease with further increases in $I_C$. This decrease at high current levels is indicative of the Kirk effect, where the effective base width increases, leading to a reduction in $f_t$.

4. **Key Features and Technical Details:**
- The peak of the graph represents the maximum transition frequency, labeled as $f_{t,max}$. This is the highest frequency at which the transistor can operate effectively.
- The initial increase and subsequent decrease in $f_t$ with respect to $I_C$ is a critical feature of the graph, highlighting the optimal operating range for the transistor before the onset of the Kirk effect.

5. **Annotations and Specific Data Points:**
- A dashed horizontal line is drawn at the level of $f_{t,max}$, emphasizing the maximum transition frequency achieved.
- There are no specific numerical values or data points labeled on the graph, but the general shape and annotations provide a qualitative understanding of the behavior of $f_t$ as a function of $I_C$.

This graph is essential for understanding how a BJT's performance is affected by changes in collector current, particularly in high-speed applications where the transition frequency is a critical parameter.

increase in the transit time of the base and a decrease in $f_{t}$. This is known as the Kirk effect [Kirk, 1962] and causes $f_{t}$ to drop at high collector currents as illustrated in Fig. 8.11.

## 8.2 BIPOLAR DEVICE MODEL SUMMARY

### Active Transistor

| $\mathrm{I}_{\mathrm{C}}=\mathrm{I}_{\mathrm{CS}} \mathrm{e}^{\mathrm{V}_{\mathrm{BE}} / \mathrm{V}_{\mathrm{T}}}$ | $\mathrm{V}_{\mathrm{T}}=\frac{\mathrm{kT}}{\mathrm{q}} \cong 26 \mathrm{mV} \text { at } 300^{\circ} \mathrm{K}$ |
| :---: | :---: |
| For more accuracy, $\mathrm{I}_{\mathrm{C}}=\mathrm{I}_{\mathrm{CS}} \mathrm{e}^{\mathrm{V}_{\mathrm{BE}} / \mathrm{V}_{\mathrm{T}}}\left(1+\frac{\mathrm{V}_{\mathrm{CE}}}{\mathrm{V}_{\mathrm{A}}}\right)$ |  |
| $I_{C S}=\frac{A_{E} q D_{n} n_{i}^{2}}{W N_{A}}$ | $I_{B}=\frac{I_{C}}{\beta}$ |
| $\mathrm{I}_{\mathrm{E}}=\left(1+\frac{1}{\beta}\right) \mathrm{I}_{\mathrm{C}}=\frac{1}{\alpha} \mathrm{I}_{\mathrm{C}}=(\beta+1) \mathrm{I}_{\mathrm{B}}$ | $\beta=\frac{I_{C}}{I_{B}}=\frac{D_{n} N_{D} L_{p}}{D_{p} N_{A} W} \cong 2.5 \frac{N_{D}}{N_{A}} \frac{L_{p}}{W}$ |
| $\alpha=\frac{\beta}{1+\beta}$ |  |

### Small-Signal Model of an Active BJT

image_name:Small-Signal Model of an Active BJT
description:This circuit represents the small-signal model of an active BJT. It includes resistors, capacitors, and a voltage-controlled current source to model the behavior of the transistor in response to small input signals. The nodes are labeled to represent the base (v_b), collector (v_c), and emitter (v_e) terminals.

| $g_{m}=\frac{I_{C}}{V_{T}}$ | $r_{\pi}=\frac{V_{T}}{I_{B}}=\frac{\beta}{g_{m}}$ |
| :---: | :---: |
| $r_{e}=\frac{\alpha}{g_{m}}$ | $r_{o}=\frac{V_{A}}{I_{C}}$ |
| $g_{m} r_{o}=\frac{V_{A}}{V_{T}}$ | $C_{b e}=C_{j}+C_{d}$ |
| $C_{j} \cong 2 A_{E} C_{j e 0}$ | $C_{d}=\tau_{b} \frac{I_{C}}{V_{T}}=g_{m} \tau_{b}$ |
| $C_{c b}=\frac{A_{c} C_{j c 0}}{\left(1+\frac{V_{C B}}{\Phi_{c 0}}\right)^{1 / 3}}$ | $C_{c s}=\frac{A_{T} C_{j s 0}}{\left(1+\frac{V_{C s}}{\Phi_{s 0}}\right)^{1 / 2}}$ |

## 8.3 SPICE MODELING

For historical reasons, most parameters for modelling bipolar transistors are specified absolutely. Also, rather than specifying the emitter area of a BJT in $(\mu \mathrm{m})^{2}$ on the line where the individual transistor connections are specified, most SPICE versions have multiplication factors. These multiplication factors can be used to automatically multiply parameters when a transistor is composed of several transistors connected in parallel. This multiplying parameter is normally called M .

The most important dc parameters are the transistor current gain, $\beta$, specified by the SPICE parameter BF; the transistor-transport saturation current, $\mathrm{I}_{\mathrm{CS}}$, specified using the parameter IS; and the Early-voltage constant, specified by the parameter VAF. Typical values for these might be $100,10^{-17} \mathrm{~A}$, and 50 V , respectively. If one wants to model the transistor in reverse mode (where the emitter voltage is higher than the collector voltage for an npn), then one might specify BR, ISS, and VAR, as well; these are the parameters that correspond to BF, IS, and VAF in the reverse direction. Typically, this reverse-mode modelling is not important for most circuits. Some other important dc parameters for accurate simulations are the base, emitter, and collector resistances, which are specified by $R B, R E$, and RC, respectively. It is especially important to specify RB (which might be $200 \Omega$ to $500 \Omega$ ).

The important capacitance parameters and their corresponding SPICE parameters include the depletion capacitances at $0-\mathrm{V}$ bias voltage, CJE, CJC, CJS; their grading coefficients, MJE, MJC, MJS; and their built-in voltages, VJE, VJC, VJS, for base-emitter, base-collector, and collector-substrate junctions. Again, the 0-V depletion capacitances should be specified in absolute values for a unit-sized transistor. Normally the base-emitter and base-collector junctions are graded (i.e., MJE, MJC $=0.33$ ), whereas the collector-substrate junction may be either abrupt (MJS $=0.5$ ) or graded (MJS $=0.33$ ), depending on processing details. Typical built-in voltages might be 0.75 V to 0.8 V . In addition, for accurate simulations, one should specify the forward-base transit time, $\tau_{\mathrm{F}}$, specified by TF , and, if the transistor is to be operated in reverse mode or under saturated conditions, the reverse-base transit time, $\tau_{\mathrm{R}}$, specified by TR.

The most important of the model parameters just described are summarized in Table 8.1. These form the basis of the Gummel-Poon SPICE model, and its variants. Many other parameters can be specified if accurate simulation is desired. Other parameters might include those to model $\beta$ degradation under very high or low current applications and parameters for accurate noise and temperature analysis.

Table 8.1 The most important SPICE parameters for modelling BJTs.

| SPICE <br> Parameter | Model <br> Constant | Brief Description | Typical Value |
| :--- | :--- | :--- | :--- |
| BF | b | Transistor current gain in forward direction | 100 |
| BR | $\beta_{\mathrm{R}}$ | Transistor current gain in the reverse direction | 1 |
| IS | $\mathrm{I}_{\mathrm{CS}}$ | Transport saturation current in forward direction | $2 \times 10^{-18} \mathrm{~A}$ |
| VAF | $\mathrm{V}_{\mathrm{A}}$ | Early voltage in forward direction | 50 V |
| RB | $\mathrm{r}_{\mathrm{b}}$ | Series base resistance | $500 \Omega$ |
| RE | $\mathrm{R}_{\mathrm{E}}$ | Series emitter resistance | $30 \Omega$ |
| RC | $\mathrm{R}_{\mathrm{C}}$ | Series collector resistance | $90 \Omega$ |
| CJE | $\mathrm{C}_{\mathrm{j} 0}$ | Base-emitter depletion capacitance at 0 V | 0.015 pF |
| CJC | $\mathrm{C}_{\mathrm{j} 0}$ | Base-collector depletion capacitance at 0 V | 0.018 pF |
| CJS | $\mathrm{C}_{\mathrm{j} 0}$ | Collector-substrate depletion capacitance at 0 V | 0.040 pF |
| MJE | $\mathrm{m}_{\mathrm{e}}$ | Base-emitter junction exponent (grading factor) | 0.30 |
| MJC | $\mathrm{m}_{\mathrm{c}}$ | Base-collector junction exponent (grading factor) | 0.35 |
| MJS | $\mathrm{m}_{\mathrm{s}}$ | Collector-substrate junction exponent (grading factor) | 0.29 |
| VJE | $\Phi_{\mathrm{e}}$ | Base-emitter built-in potential | 0.9 V |
| VJC | $\Phi_{\mathrm{c}}$ | Base-collector built-in potential | 0.7 V |
| VJS | $\Phi_{\mathrm{s}}$ | Collector-substrate built-in potential | 0.64 V |
| TF | $\tau_{\mathrm{F}}$ | Forward-base transit time | 12 ps |
| TR | $\tau_{\mathrm{R}}$ | Reverse-base transit time | 4 ns |

Another popular SPICE model for modern bipolar transistors is the High Current Model (HiCuM). As the name suggests, it is particularly effective for modeling transistor behavior at high current densities, and is therefore well suited to the design of circuits operating at very high frequencies. Since high-frequency design is an area where bipolar devices continue to offer some advantages over MOSFETs, the HiCuM model has become very popular.

Readers should refer to their SPICE manuals for complete descriptions of the Gummel-Poon and HighCurrent models and their parameters.

## 8.4 BIPOLAR AND BICMOS PROCESSING

The processing steps required for realizing bipolar transistors are similar to those used for realizing MOS transistors, although naturally the precise recipe is different. Thus, rather than presenting the complete realization of modern bipolar transistors, we briefly discuss some of the modifications needed for realizing them.

### 8.4.1 Bipolar Processing

A bipolar process normally starts with a $\mathrm{p}^{-}$substrate. The first masking step involves the diffusion (or ion implantation) of $\mathrm{n}^{+}$regions into the substrate wherever transistors are desired. These $\mathrm{n}^{+}$regions are used to lower the series collector resistance. Next, an $\mathrm{n}^{-}$single-crystal epitaxial layer is deposited.

In the next step, isolation structures are patterned, using either field-oxide growth and/or by etching trenches and filling them with $\mathrm{SiO}_{2}$. Next, the $\mathrm{n}^{+}$-collector contact region is implanted. This region extends from the surface down to the $\mathrm{n}^{+}$-buried region under the transistor.

Polysilicon is generally used to contact the emitter, the base, and possibly the collector, as Fig. 8.12 shows for a typical npn BJT structure. One approach is to begin by depositing the base $\mathrm{p}^{+}$polysilicon. This polysilicon is heavily doped $\mathrm{p}^{+}$so that later, during a high-temperature step, the boron dopant from the polysilicon contact diffuses into the silicon underneath the base polysilicon to make the underlying region $\mathrm{p}^{+}$. The base polysilicon is removed in the active area of the transistor. Next, using one of a variety of possible methods, the base polysilicon is covered with a thin layer of $\mathrm{SiO}_{2}$, perhaps $0.5 \mu \mathrm{~m}$ in thickness, leaving an opening over the active area of the transistor. This $\mathrm{SiO}_{2}$ spacer, which separates the base polysilicon from the emitter polysilicon, as shown in Fig. 8.12, allows the base polysilicon (or contact) to be very close to the emitter polysilicon (or contact), thereby minimizing the base resistance. Next, the base is ion-implanted to p -type silicon, and then $\mathrm{n}^{+}$polysilicon is deposited for the emitter. At this point, the true emitter has not yet been formed-only the emitter $\mathrm{n}^{+}$polysilicon has been laid down. However, when the wafer is annealed, the $\mathrm{n}^{+}$from the emitter polysilicon diffuses into the base p silicon to form the true emitter region. During annealing, the $\mathrm{p}^{+}$dopants from the base polysilicon also diffuse into the extrinsic base region. As a result, this procedure results in a self-aligned process since the use of the $\mathrm{SiO}_{2}$ spacer allows the base polysilicon to determine where the emitter is finally located. The importance of this process is that, through the use of self-aligned contacts and field-oxide isolation, very small, high-frequency bipolar transistors can be realized using methods similar to those used in realizing modern MOS transistors.

### 8.4.2 Modern SiGe BiCMOS HBT Processing

A major limitation of the processing described above is that the p -type base region is formed by ion implantation. As illustrated in Fig. 2.4, this results in a dopant profile with an approximately Gaussian distribution. Moreover, any subsequent high-temperature processing of the wafer may cause annealing and, hence, a spreading of the base
image_name:Fig. 8.12
description:The image, labeled as Fig. 8.12, depicts a cross-section of a modern, self-aligned bipolar transistor with oxide isolation. The structure is built upon a p-type substrate, denoted as \( p^- \) substrate, which forms the foundational layer of the device.

### Components and Structure:
1. **Collector:**
- Located on the left side of the diagram, the collector region is indicated as being formed by an \( n^+ \) type layer, which is heavily doped to facilitate efficient electron collection.
- The collector is encapsulated by a polysilicon (poly) layer.

2. **Base:**
- The base region is centrally located and consists of a \( p^+ \) polysilicon layer. This base is thin, allowing for high-frequency performance, as noted in the context description.
- The base extends laterally and connects with the emitter and collector regions.

3. **Emitter:**
- Positioned to the right of the base, the emitter is formed by an \( n^+ \) polysilicon layer, allowing for efficient electron emission into the base.
- It is labeled with an aluminum (Al) contact for electrical connectivity.

4. **Isolation:**
- The device uses SiO2 spacers for isolation, which are visible as horizontal lines separating different doped regions.

5. **Epitaxial Layer (n- epi):**
- Beneath the base and emitter, an \( n^- \) epitaxial layer is present, providing a controlled environment for carrier movement.

### Connections and Interactions:
- The diagram indicates the flow of charge carriers, primarily electrons, from the emitter through the base to the collector.
- The polysilicon layers serve as conductive paths for electrical signals, ensuring efficient operation of the bipolar transistor.

### Labels, Annotations, and Key Features:
- The key regions are clearly labeled: Collector, Base, and Emitter.
- The doping concentrations are indicated with symbols such as \( n^+ \), \( p^+ \), and \( n^- \), denoting the type and level of doping.
- The use of polysilicon (poly) is highlighted, showing its role in forming the structural and conductive parts of the device.

This cross-section effectively illustrates the complex layering and integration of materials used in modern bipolar transistor fabrication, emphasizing the use of oxide isolation and polysilicon for enhanced performance.

Fig. 8.12 Cross section of a modern, self-aligned bipolar transistor with oxide isolation. The term "poly" refers to polysilicon.
region. As a result, it is difficult to realize a very thin base region using this method, which as shown in equation (8.54) limits the device's high-frequency performance.

Key Point: High-performance modern bipolar transistors are manufactured by epitaxially growing a very thin base region. The use of a different material for the base, such as sil-icon-germanium, results in a heterojunction bipolar transistor (HBT) whose bandgap structure can be tailored to provide high current gain, high unity-gain frequency, and/ or high Early voltage.

The solution is to epitaxially grow the base region on top of the collector. This allows very thin base regions to be deposited with very abrupt doping profiles at the junctions. It also affords the opportunity to grow a compound semiconductor for the base region instead of pure silicon. Specifically, the use of silicon-germanium (SiGe) in the base offers several advantages [Harame, 1995]. Because the base region is SiGe while the collector and emitter are Si, this device structure is a heterojunction bipolar transistor (HBT). Introducing germanium in the base lowers its bandgap, which in turn lowers the energy required for electrons to cross the emitterbase junction (in a npn transistor). Hence, at a fixed $\mathrm{V}_{\mathrm{BE}}$, the electron current is higher with a SiGe base layer than a silicon base layer, resulting in increased current gain $\beta$. The increase in $\beta$ provided by the use of a SiGe base offsets the need to have a lower dopant concentration there; hence, the dopant concentration of the base can be higher in a SiGe HBT than in a silicon BJT, lowering the base resistance $r_{b}$. Moreover, by varying the environment in during epitaxial growth of the base, it is possible to vary the silicon-germanium ratio across the base region. Doing so gives rise to an electric field which accelerates electrons from emitter to collector, reducing the base transit time $\tau_{b}$ and increasing the unity-gain frequency $f_{t}$ compared with silicon transistors. Grading the germanium content also makes it possible to increase the Early voltage, $\mathrm{V}_{\mathrm{A}}$. In summary, the use of an epitaxially grown base region is a significant advance that has offered the flexibility to engineer a bipolar transistor with improved analog performance in virtually every way.

All of the bipolar processing described above can be performed on wafers alongside CMOS circuitry. A series of masks defines the regions where $\mathrm{n}^{+}$subcollectors are deposited, base epitaxy is performed, emitter contacts are made, etc. without interfering with neighbouring CMOS circuits. The primary challenges are ensuring that the surface preparation required for epitaxial growth of the base does not deteriorate the CMOS regions, and that high-temperature annealing of the CMOS devices does not deteriorate bipolar transistor performance. The result is a bipolar-CMOS (BiCMOS) manufacturing processes that can realize highperformance bipolar devices alongside CMOS devices.

### 8.4.3 Mismatch in Bipolar Devices

Like all integrated circuit components, side-by-side bipolar transistors on the same die that are specified to have the exact same dimensions will still exhibit slight parametric differences due to finite tolerances during fabrication. Although bipolar circuits are generally less affected by mismatch than their MOS counterparts, mismatch in the collector currents of bipolar transistor is of significant interest as it leads to offset in differential pairs and current mirrors. Collector current mismatch is determined by mismatch between the transistors' scale currents.

$$
\begin{equation*}
I_{C S}=\frac{A_{E} q D_{n} n_{i}^{2}}{W N_{A}} \tag{8.55}
\end{equation*}
$$

Uncertainty in the emitter area $A_{E}$, base width $W$, and base dopant concentration $N_{A}$, during manufacture are all causes of mismatch in bipolar transistor scale currents, and hence collector currents. As a result, collector currents vary statistically as described in Section 2.3 .3 so that the percentage mismatch between the collector current of two identically sized bipolar transistors is inversely related to the device area. Specifically, the mean squared deviation in the collector current of a particular bipolar device away from its nominal value is modeled as follows:

$$
\begin{equation*}
\sigma^{2}\left(\frac{\Delta \mathrm{I}_{\mathrm{C}}}{\mathrm{I}_{\mathrm{C}}}\right)=\sigma^{2}\left(\frac{\Delta \mathrm{I}_{\mathrm{CS}}}{\mathrm{I}_{\mathrm{CS}}}\right)=\frac{\mathrm{A}_{\mathrm{IC}}^{2}}{\mathrm{~A}_{\mathrm{E}}} \tag{8.56}
\end{equation*}
$$

The constant $A_{I c}$ parameterizes the matching accuracy of a particular bipolar fabrication process, and is in the range of $0.01-0.04 ~ \mathrm{~m}^{-1}$ for typical modern bipolar processes [Tuinhout, 2003].

## 8.5 BIPOLAR CURRENT MIRRORS AND GAIN STAGES

In this section, we look at bipolar current mirrors and two bipolar gain circuits: the emitter follower and the differential pair. Although much of the small-signal analyses follow those of their MOS counterparts very closely, one difference is the finite base impedance of bipolar transistors. Here we shall see some simple rules for dealing with this finite base impedance during small-signal analysis. Because of its importance in translinear circuits, we also look at the large-signal behavior of the differential pair.

### 8.5.1 Current Mirrors

The most popular bipolar current mirrors are very similar to the MOS current mirrors. A simple bipolar current mirror is shown in Fig. 8.13. This current mirror has an output current almost equal to its input current. In fact, its output current is slightly smaller than the input current, due to the finite base currents of $Q_{1}$ and $Q_{2}$. Taking these two base currents into account results in

$$
\begin{equation*}
I_{\text {out }}=\frac{1}{(1+2 / \beta)} I_{\text {in }} \tag{8.57}
\end{equation*}
$$

where $\beta$ is the transistor current gain. For large $\beta$, this relation is approximately given by $\mathrm{I}_{\text {out }} \cong(1-2 / \beta) \mathrm{I}_{\mathrm{in}}$.
In one commonly used modification of the simple bipolar current mirror, an emitter-follower buffer, $Q_{3}$, is added to supply the base currents, as shown in Fig. 8.14. This additional transistor minimizes the errors due to finite base currents, resulting in $I_{\text {out }} \cong I_{\text {in }}\left(1-2 / \beta^{2}\right)$. Such an arrangement is almost always used for current mirrors when lateral transistors ${ }^{1}$ are used because of their low current gains (i.e., $\beta$ 's on the order of only $10-20$ ). The output impedance of both of the previous current sources is equal to the output impedance of $Q_{2}$, which is $r_{02}$.

Key Point: Bipolar current mirrors are similar to CMOS mirrors, except that finite base current is a source of mismatch between the input and output currents.

In another often-used variation of the simple current mirror, emitter degeneration is added. This approach results in larger output impedances and also minimizes errors caused by mismatches between $Q_{1}$ and $Q_{2}$. An example of this current mirror is shown in Fig. 8.15. In an analysis similar to that given for the MOS current mirror with source degeneration, the output impedance is now found to be given by

$$
\begin{equation*}
r_{\text {out }} \cong r_{\mathrm{o} 2}\left(1+g_{\mathrm{m} 2} R_{e}\right) \tag{8.58}
\end{equation*}
$$

image_name:Fig. 8.13 A simple bipolar current mirror.
description:The circuit is a simple bipolar current mirror with transistors Q1 and Q2. The input current Iin is mirrored to the output as Iout.

Fig. 8.13 A simple bipolar current mirror.

[^4]Fig. 8.14 A current mirror with fewer inaccuracies caused by finite base currents.
image_name:Fig. 8.14
description:The circuit is a current mirror with an additional transistor Q3 to improve accuracy by compensating for base current errors. The input current Iin is mirrored to the output as Iout.
image_name:Fig. 8.15
description:The circuit shown in Fig. 8.15 is a current mirror with emitter degeneration using resistors Re. It is designed to improve accuracy by reducing the effect of finite base currents. The bias voltage across Re is about 0.25 V.

Fig. 8.15 A current mirror with emitter degeneration.
for $R_{e}<<r_{\pi}$. Normally, this current mirror is designed so that the bias voltage across $R_{e}$, defined to be $V_{R e}$, is about 0.25 V . This implies that $\mathrm{R}_{\mathrm{e}}$ is given by

$$
\begin{equation*}
\mathrm{R}_{\mathrm{e}}=\frac{\mathrm{V}_{\mathrm{Re}}}{\mathrm{I}_{\mathrm{e} 2}} \cong \frac{\mathrm{~V}_{\mathrm{Re}}}{\mathrm{I}_{\mathrm{c} 2}} \tag{8.59}
\end{equation*}
$$

Using the relationship $\mathrm{g}_{\mathrm{m} 2}=\mathrm{I}_{\mathrm{c} 2} / \mathrm{V}_{\mathrm{T}}$, where $\mathrm{V}_{\mathrm{T}}=\mathrm{kT} / \mathrm{q} \cong 26 \mathrm{mV}$ at $300{ }^{\circ} \mathrm{K}$, gives

$$
\begin{equation*}
r_{\text {out }} \cong r_{02}\left(1+g_{\mathrm{m} 2} R_{e}\right)=r_{\mathrm{o} 2}\left(1+\frac{V_{\mathrm{Be}}}{V_{T}}\right) \cong 11 r_{\mathrm{o} 2} \tag{8.60}
\end{equation*}
$$

assuming $\mathrm{V}_{\mathrm{Re}}=0.25 \mathrm{~V}$. It should be mentioned here that the addition of these $\mathrm{R}_{\mathrm{e}}$ resistors also minimizes the noise output current of this current mirror, generated by the base resistance thermal noise, which is often the major source of noise in bipolar wideband circuits.

To achieve still higher output impedances, one can use either a cascode or a Wilson current mirror, as shown in Fig. 8.16. The Wilson current mirror is preferred in bipolar realizations because the cascode mirror exhibits large errors, due to the fact that the base currents of all of the transistors are supplied by $\mathrm{I}_{\text {in }}$ only. As a result, the output current is smaller than the input current by a factor roughly equal to $1-4 / \beta$. For the Wilson current mirror, the base currents of $Q_{3}$ and $Q_{4}$ are supplied by $I_{i n}$, whereas the base currents of $Q_{1}$ and $Q_{2}$ come from $I_{\text {out }}$. It can be shown that the errors due to finite base currents are on the order of $2 / \beta^{2}$ [Gray, 2009]. It can also be shown that both of these current mirrors have an output impedance on the order of [Gray, 2009]

$$
\begin{equation*}
r_{\text {out }} \cong \frac{\beta r_{0}}{2} \tag{8.61}
\end{equation*}
$$

### 8.5.2 Emitter Follower

A bipolar emitter-follower is very similar to a MOS source follower, except that its input resistance is not infinite and its gain is normally much closer to unity. The analysis of its low-frequency response provides a good
image_name:(a)
description:This is a cascode current mirror circuit, which is designed to provide high output impedance and better current matching between input and output.
image_name:(b)
description:This is a Wilson current mirror circuit configuration, providing high output impedance.

Fig. 8.16 High-output impedance (a) cascode and (b) Wilson current mirrors.
illustration of the use of the bipolar T model, and also of some relatively general principles for coming up with quick estimates of input and output impedances of bipolar circuits.

A bipolar emitter follower with a resistive load is shown in Fig. 8.17. Its small-signal model at low frequencies, where the bipolar T model has been used, is shown in Fig. 8.18(a). In this small-signal model, the device base resistance $r_{b}$ has been ignored, since it can be easily taken into account after the fact by simply making $R_{S}$ slightly larger (i.e., equal to $R_{S}+r_{b}$ ). Notice that $R_{E}$ and $r_{0}$ are in parallel. This allows a slightly simplified small-signal model to be analyzed, as shown in Fig. 8.18(b), where $R_{E}^{\prime}=R_{E} \| r_{0}$. The analysis of the gain of this circuit is done in two steps. First, the input impedance looking into the base of the transistor, $\mathrm{R}_{\mathrm{b}}$, is found, allowing us to calculate the gain from the input to the base. Second, the gain from the base to the output is found, which allows us to derive the overall gain. The current in the emitter, $\mathrm{i}_{\mathrm{e}}$, is given by

$$
\begin{equation*}
i_{e}=i_{b}(\beta+1) \tag{8.62}
\end{equation*}
$$

Therefore,

$$
\begin{equation*}
v_{b}=i_{e}\left(r_{e}+R_{E}^{\prime}\right)=i_{b}(\beta+1)\left(r_{e}+R_{E}^{\prime}\right) \tag{8.63}
\end{equation*}
$$

This gives

$$
\begin{equation*}
R_{b}=\frac{v_{b}}{i_{b}}=(\beta+1)\left(r_{e}+R_{E}^{\prime}\right) \tag{8.64}
\end{equation*}
$$

Alternatively, noting that

$$
\begin{equation*}
(\beta+1) r_{e}=(\beta+1) \frac{\alpha}{g_{m}}=(\beta+1) \frac{\beta /(\beta+1)}{g_{m}}=\frac{\beta}{g_{m}}=r_{\pi} \tag{8.65}
\end{equation*}
$$

gives

$$
\begin{equation*}
\mathbf{R}_{\mathrm{b}}=\mathrm{r}_{\pi}+(\beta+1) \mathrm{R}_{\mathrm{E}}^{\prime} \tag{8.66}
\end{equation*}
$$

image_name:Fig. 8.17 A bipolar emitter follower
description:The circuit is a bipolar emitter follower configuration. It uses an NPN transistor with a resistor RS connected to the base and a resistor RE connected to the emitter. The input voltage is applied to the base through RS, and the output is taken from the emitter.

Fig. 8.17 A bipolar emitter follower.
image_name:(a)
description:The circuit is a small-signal model of a bipolar emitter follower. It includes a current-controlled current source representing the transistor's current gain (βib). The input voltage is applied at Vin, and the output is taken from Vout.

image_name:(b)
description:The circuit is a small-signal model of a bipolar emitter follower. It includes a current-controlled current source representing the transistor's current gain (βib). The input voltage is applied at Vin, and the output is taken from Vout. The equivalent emitter resistance R'E is given by the parallel combination of RE and ro.

Fig. 8.18 (a) The small-signal model for the bipolar emitter follower and (b) a simplified model.
Equations (8.64) and (8.66) illustrate a principle that is generally applicable for bipolar circuits: At low frequencies, resistances in series with the emitter appear $\beta+1$ times larger when seen looking into the base or, equivalently, when they are reflected into the base. Continuing, using the resistor-divider formula, we now have

Key Point: At low frequencies, resistances in series with the emitter appear $(\beta+1)$ times larger when seen looking into the base.

$$
\begin{equation*}
\frac{v_{b}}{v_{i n}}=\frac{R_{b}}{R_{b}+R_{S}}=\frac{(\beta+1)\left(r_{e}+R_{E}^{\prime}\right)}{(\beta+1)\left(r_{e}+R_{E}^{\prime}\right)+R_{S}} \tag{8.67}
\end{equation*}
$$

The gain from the base to the emitter, which is the output, is easily found from Fig. 8.17(b), again using the resistor-divider formula, to be given by

$$
\begin{equation*}
\frac{v_{\text {out }}}{v_{b}}=\frac{R_{E}^{\prime}}{R_{E}^{\prime}+r_{e}} \cong \frac{R_{E}^{\prime}}{R_{E}^{\prime}+1 / g_{m}} \tag{8.68}
\end{equation*}
$$

Using (8.67) and (8.68), the overall gain is now given by

$$
\begin{equation*}
\frac{v_{\text {out }}}{v_{\text {in }}}=\frac{v_{\text {b }}}{v_{\text {in }}} \frac{v_{\text {out }}}{v_{b}}=\left(\frac{(\beta+1)\left(r_{e}+R_{E}^{\prime}\right)}{(\beta+1)\left(r_{e}+R_{E}^{\prime}\right)+R_{S}}\right)\left(\frac{R_{E}^{\prime}}{R_{E}^{\prime}+1 / g_{m}}\right) \tag{8.69}
\end{equation*}
$$

With a little practice, transfer functions such as that given by (8.69) can be written by simply inspecting the actual circuit, without actually analyzing the small-signal model.

It is also interesting to find the output impedance of the emitter follower at low frequencies excluding $\mathrm{R}^{\prime}{ }_{\mathrm{E}}$, which is equal to the impedance seen looking into the emitter. The small-signal model for this analysis is shown in Fig. 8.19 , where the input source has been set to 0 and the impedance $R_{e}=v_{x} / i_{x}$ is to be found. First note that

$$
\begin{equation*}
i_{b}=\frac{i_{e}}{\beta+1}=\frac{-i_{x}}{\beta+1} \tag{8.70}
\end{equation*}
$$

Fig. 8.19 The small-signal model for finding the output impedance of an emitter follower.
image_name:Fig. 8.19
description:The circuit is a small-signal model for finding the output impedance of an emitter follower. The current source 'bib' is connected between ground and node 'vb', with resistors 'RS' and 're' forming a path from ground to node 'vx'. The resistor 'Re' is connected between 'vx' and ground.

since $i_{x}=-i_{e}$. Therefore, we have

$$
\begin{align*}
v_{x} & =v_{b}+i_{x} r_{e} \\
& =-i_{b} R_{S}+i_{x} r_{e} \\
& =i_{x} \frac{R_{S}}{\beta+1}+i_{x} r_{e} \tag{8.71}
\end{align*}
$$

This gives the impedance seen looking into the emitter as

$$
\begin{equation*}
R_{e}=\frac{v_{x}}{i_{x}}=\frac{R_{S}}{\beta+1}+r_{e}=\frac{R_{S}}{\beta+1}+\frac{r_{\pi}}{\beta+1} \tag{8.72}
\end{equation*}
$$

This is an example of a general principle for bipolar circuits: Resistances in series with the base are divided by $\beta+1$ when they are seen looking into the emitter, or, equivalently, are reflected to the emitter. The total output impedance of the emitter-follower is now simply $R_{e}$ in parallel with $R_{E}^{\prime}$.

The high-frequency analysis of the emitter follower is very similar to that of

Key Point: Resistances in series with the base are divided by $(\beta+1)$ when they are seen looking into the emitter.
the source follower presented in Section 4.4. As with source followers, some care is required to avoid overshoot and ringing in emitter followers. In fact, ringing is somewhat more likely with emitter followers than with source followers due in part to the absence of any body effect.

### 8.5.3 Bipolar Differential Pair

#### Large-Signal

A bipolar differential pair is shown in Fig. 8.20. This circuit's large-signal behavior can be analyzed by first recalling the exponential relationship for a bipolar transistor,

$$
\begin{equation*}
I_{C}=I_{S} e^{\left(V_{B E} / V_{T}\right)} \tag{8.73}
\end{equation*}
$$

which can be used to find the base-emitter voltages

$$
\begin{align*}
& \mathrm{V}_{\mathrm{BE} 1}=\mathrm{V}_{\mathrm{T}} \ln \left(\frac{\mathrm{I}_{\mathrm{C} 1}}{\mathrm{I}_{\mathrm{S} 1}}\right)  \tag{8.74}\\
& \mathrm{V}_{\mathrm{BE} 2}=\mathrm{V}_{\mathrm{T}} \ln \left(\frac{\mathrm{I}_{\mathrm{C} 2}}{\mathrm{I}_{\mathrm{S} 2}}\right) \tag{8.75}
\end{align*}
$$

Now, writing an equation for the sum of voltages around the loop of input and base-emitter voltages, we have

$$
\begin{equation*}
\mathrm{V}^{+}-\mathrm{V}_{\mathrm{BE} 1}+\mathrm{V}_{\mathrm{BE} 2}-\mathrm{V}^{-}=0 \tag{8.76}
\end{equation*}
$$

image_name:Fig. 8.20 A bipolar differential pair.
description:The circuit is a bipolar differential pair with two NPN transistors Q1 and Q2. The emitters of both transistors are connected to a current source IEE, which is grounded. The bases of Q1 and Q2 are connected to input voltages V+ and V- respectively.

Fig. 8.20 A bipolar differential pair.

Combining (8.74), (8.75), and (8.76), and assuming $\mathrm{I}_{\mathrm{S} 1}=\mathrm{I}_{\mathrm{S} 2}$, we can write

$$
\begin{equation*}
\frac{I_{C 1}}{I_{C 2}}=e^{\left(v^{+}-V^{-}\right) V_{T}}=e^{v_{i d} V_{T}} \tag{8.77}
\end{equation*}
$$

where $\mathrm{V}_{\mathrm{id}}$ is defined as the difference between $\mathrm{V}^{+}$and $\mathrm{V}^{-}$. In addition, we can write

$$
\begin{equation*}
\alpha \mathrm{I}_{\mathrm{EE}}=\mathrm{I}_{\mathrm{C} 1}+\mathrm{I}_{\mathrm{C} 2} \tag{8.78}
\end{equation*}
$$

where $\alpha$ is defined to be $\beta /(\beta+1)$ and is due to some currents flowing through the base terminals. Finally, combining (8.77) and (8.78), we have

$$
\begin{align*}
& I_{C 1}=\frac{\alpha I_{E E}}{1+e^{-\mathrm{V}_{\mathrm{id}} V_{T}}}  \tag{8.79}\\
& I_{\mathrm{C} 2}=\frac{\alpha \mathrm{I}_{\mathrm{EE}}}{1+\mathrm{e}^{\mathrm{v}_{\mathrm{id}} V_{\mathrm{T}}}} \tag{8.80}
\end{align*}
$$

A plot of these two currents with respect to $\mathrm{V}_{\mathrm{id}}$ is shown in Fig. 8.21, where we note that the currents are split equally at $\mathrm{V}_{\mathrm{id}}=0$ and saturate near $\mathrm{I}_{\mathrm{EE}}$ or 0 for differential input voltages approaching $4 \mathrm{~V}_{\mathrm{T}}$ (around 100 mV ). Note that the relations shown in (8.79) and (8.80) results in a hyperbolic tangent function when their difference is taken.

$$
\begin{equation*}
\mathrm{I}_{\mathrm{C} 2}-\mathrm{I}_{\mathrm{C} 1}=\alpha \mathrm{I}_{\mathrm{EE}} \tanh \left(\mathrm{~V}_{\mathrm{id}} / 2 \mathrm{~V}_{\mathrm{T}}\right) \tag{8.81}
\end{equation*}
$$

Thus this current-voltage relationship for a bipolar differential is commonly referred to as the tanh relationship.

#### Small-Signal

The small-signal model for the bipolar differential pair of Fig. 8.20 is shown in Fig. 8.22. Once again, defining $\mathrm{v}_{\mathrm{id}}=\mathrm{v}^{+}-\mathrm{v}^{-}$, we have

$$
\begin{equation*}
i_{\mathrm{c} 1}=\alpha i_{\mathrm{e} 1}=\frac{\alpha v_{\mathrm{id}}}{r_{\mathrm{e} 1}+r_{\mathrm{e} 2}}=\frac{\alpha v_{\mathrm{id}}}{\left(\alpha / \mathrm{g}_{\mathrm{m} 1}\right)+\left(\alpha / \mathrm{g}_{\mathrm{m} 2}\right)} \tag{8.82}
\end{equation*}
$$

In the case where both transistors have the same bias currents through them (i.e., the nominal differential voltage is 0 , resulting in $g_{m 1}=g_{m}$ ), we find the same result as for a MOS differential pair,

$$
\begin{equation*}
\mathrm{i}_{\mathrm{c} 1}=\frac{\mathrm{g}_{\mathrm{m} 1}}{2} \mathrm{v}_{\mathrm{id}} \tag{8.83}
\end{equation*}
$$

A similar result holds for $\mathrm{i}_{\mathrm{c} 2}$.
image_name:Fig. 8.21 Collector currents for a bipolar differential pair.
description:The graph in Fig. 8.21 illustrates the collector currents \( I_{C1} \) and \( I_{C2} \) for a bipolar differential pair as a function of the normalized differential input voltage \( V_{id}/V_T \).

1. **Type of Graph and Function:**
- This is a plot of collector currents versus normalized differential input voltage for a bipolar differential pair.

2. **Axes Labels and Units:**
- The horizontal axis represents the normalized differential input voltage \( V_{id}/V_T \), where \( V_T \) is the thermal voltage.
- The vertical axis represents the collector currents \( I_{C1} \) and \( I_{C2} \), scaled by \( \alpha I_{EE} \), where \( \alpha \) is the common-base current gain and \( I_{EE} \) is the emitter current.

3. **Overall Behavior and Trends:**
- The graph shows two curves representing \( I_{C1} \) and \( I_{C2} \).
- At \( V_{id}/V_T = 0 \), both currents are equal to \( 0.5 \alpha I_{EE} \), indicating a balanced state.
- As \( V_{id}/V_T \) increases positively, \( I_{C1} \) increases towards \( \alpha I_{EE} \) while \( I_{C2} \) decreases towards zero.
- Conversely, as \( V_{id}/V_T \) becomes more negative, \( I_{C1} \) decreases towards zero and \( I_{C2} \) increases towards \( \alpha I_{EE} \).

4. **Key Features and Technical Details:**
- The curves are symmetrical around the vertical line at \( V_{id}/V_T = 0 \).
- The transition between \( I_{C1} \) and \( I_{C2} \) is smooth, indicating a typical exponential response characteristic of differential pairs.
- The currents saturate at \( \alpha I_{EE} \) as \( V_{id}/V_T \) moves towards positive or negative extremes.

5. **Annotations and Specific Data Points:**
- The graph is annotated with key current values \( 0.5 \alpha I_{EE} \) at the center and \( \alpha I_{EE} \) at the extremes.
- The symmetry and smooth transition of the curves highlight the balanced nature of the differential pair operation.

Fig. 8.21 Collector currents for a bipolar differential pair.
image_name:Fig. 8.22 The small-signal model of a bipolar differential pair
description:The circuit diagram represents a small-signal model of a bipolar differential pair. It includes resistors re1 and re2, and current-controlled current sources ic1 and ic2. The differential input is applied across nodes v+ and v-. The currents ic1 and ic2 are controlled by ie1 and ie2, respectively, with a gain factor alpha. The model illustrates the balanced nature of the differential pair operation.

Fig. 8.22 The small-signal model of a bipolar differential pair.

Finally, the input impedance of this differential pair can be found using the impedance-scaling rule just discussed. Specifically, consider the small-signal model shown in Fig. 8.23, where $\mathrm{v}^{-}$is grounded and we wish to find the impedance $r_{i d}$ looking into the base of $Q_{1}$. The impedance, $r_{2}$, seen looking into the emitter of $Q_{2}$ is simply $r_{e 2}$, since the base is grounded. Thus, the total emitter resistance to the ground of $Q_{1}$ is $r_{e 1}+r_{e 2}$, and using the impedance reflection rule, the impedance, $r_{i d}$, seen looking into the base of $Q_{1}$ is equal to $\beta+1$ times the emitter resistance, or, equivalently,

$$
\begin{equation*}
\mathrm{r}_{\mathrm{id}}=(\beta+1)\left(\mathrm{r}_{\mathrm{e} 1}+\mathrm{r}_{\mathrm{e} 2}\right) \tag{8.84}
\end{equation*}
$$

#### High-Frequency

A symetric bipolar differential amplifier with resistive loads is shown in Fig. 8.24. A small-signal model of this amplifier using the T-model is shown in Fig. 8.25. Here we have ignored both the base resistances and the transistor output resistances in order to simplify the circuit. Neither of these simplifications is a significant limitation of the analysis which follows since the former could be accounted for by taking $R_{s 1}$ and $R_{s 2}$ larger, and the latter could be accounted for by taking $R_{c 1}$ and $R_{c 2}$ smaller.

Assuming $R_{c 1}=R_{c 2}, R_{s 1}=R_{s 2}$, and that the transistors are matched, then the circuit is perfectly symetric. If one also assumes that $v_{i n}^{-}=-v_{i n}^{+}$, then based on the symetry, the node voltage $v_{e}$ will never change similar to if it was connected to a small-signal ground. Indeed, if the node $\mathrm{v}_{\mathrm{e}}$ was connected to a small-signal ground, then circuit will operate identically. This allows one to simplify the analysis to that of the half-circuit; with the half-circuit being identical to that of a common-emitter amplifier whose analysis is very similar to that of the common-source MOS amplifier studied previously. Given this equivalence, and assuming the input pole is dominant, the amplifier bandwidth, $\omega_{-3 \mathrm{~dB}}$, is given by

$$
\begin{equation*}
\omega_{-3 \mathrm{~dB}}=\frac{1}{\left(R_{\mathrm{s} 1} \| r_{\pi 1}\right)\left[C_{b e 1}+C_{c b 1}\left(1+g_{m 1} R_{c 1}\right)\right]} \tag{8.85}
\end{equation*}
$$

image_name:Fig. 8.23 Finding the input impedance of a bipolar differential pair.
description:This circuit represents a bipolar differential pair with resistive loads. The input impedance is being analyzed. The circuit includes resistors and current-controlled current sources.

Fig. 8.23 Finding the input impedance of a bipolar differential pair.

Fig. 8.24 Resistively-loaded symetric BJT differential amplifier.
image_name:Fig. 8.24
description:This circuit is a bipolar differential pair with resistive loads. It uses two NPN transistors (Q1 and Q2) with equal collector resistors RC1 and RC2. The input is differential, with Vin+ and Vin- nodes, and the output is also differential, with Vout+ and Vout- nodes. The circuit is biased with a current source Ibias.

Fig. 8.25 The small-signal model of the resistivelyloaded BJT differential amplifier in Fig. 8.24.
image_name:Fig. 8.25
description:This circuit is a small-signal model of a resistively loaded BJT differential amplifier. It includes components such as collector-base capacitances (C_cb1, C_cb2), collector resistors (R_c1, R_c2), and emitter resistors (r_e1, r_e2). The circuit demonstrates the Miller effect with C_cb1 and a second pole at the output.

Note the important role of the Miller effect which applies a multiplicative gain of ( $\left.1+g_{m 1} R_{c 1}\right)$ to the collectorbase capacitance $C_{c b 1}$. A second pole arises at the output, $\omega_{\mathrm{p} 2} \cong 1 / R_{c 1} C_{c s 1}$.

## 8.6 APPENDIX

### 8.6.1 Bipolar Transistor Exponential Relationship

The various components of the base, collector, and emitter currents were shown in Fig. 8.4, on page 333. Figure 8.26 shows plots of the minority-carrier concentrations in the emitter, base, and collector regions. The current flow of these minority carriers is due to diffusion. By calculating the gradient of the minority-carrier concentrations near the base-emitter junction in a manner similar to that used for diodes, it is possible to derive a relationship between the electron current and the hole current of Fig. 8.4.
image_name:Fig. 8.26
description:The graph in Fig. 8.26 illustrates the minority-carrier concentrations in the emitter, base, and collector regions of a bipolar junction transistor (BJT). This is a spatial distribution graph, showing how these concentrations vary across different regions of the transistor.

1. **Type of Graph and Function:**
- The graph is a spatial distribution plot of minority-carrier concentrations across the emitter, base, and collector regions of a BJT.

2. **Axes Labels and Units:**
- The x-axis represents the position across the transistor, denoted as 'x', with specific points labeled as '0' and 'W'.
- The y-axis represents the minority-carrier concentration, though specific units are not provided.

3. **Overall Behavior and Trends:**
- In the **n+ emitter region**, the concentration of holes (minority carriers) decreases exponentially from a point labeled \( p_{e0} \) far from the junction to \( p_e(0) \) at the edge of the base-emitter depletion region. This indicates a diffusion process typical in semiconductors.
- In the **p- base region**, the electron concentration \( n_b(0) \) is shown at the base-emitter junction, and it linearly decreases to zero across the width 'W' of the base. This linear decrease suggests a constant gradient, typical of diffusion under steady-state conditions.
- In the **n- collector region**, the concentration of holes increases slightly near the junction and then stabilizes, indicating minimal recombination.

4. **Key Features and Technical Details:**
- The graph highlights the diffusion of minority carriers: holes in the emitter and electrons in the base.
- The arrows indicate the direction of current flow: hole current in the emitter and electron current in the base.
- The concentration \( p_e(0) \) and \( n_b(0) \) are critical points for understanding the carrier injection and recombination processes.

5. **Annotations and Specific Data Points:**
- The graph includes annotations such as \( p_e(0) \), \( p_{e0} \), and \( n_b(0) \), which are key to understanding the carrier concentration profiles.
- The transition points between regions are marked, and the width 'W' of the base is indicated, emphasizing the spatial change in concentrations.

This graph effectively visualizes the diffusion and distribution of minority carriers in a BJT, crucial for understanding its operation and the associated current flows.

Fig. 8.26 The concentrations of minority carriers in the emitter, base, and collector.

The concentration of holes in the emitter at the edge of the base-emitter depletion region is denoted $\mathrm{p}_{\mathrm{e}}(0)$. This concentration decreases exponentially the farther one gets from the junction, in a manner similar to that described for diodes. The concentration far from the junction, $\mathrm{p}_{\mathrm{e} 0}$, is given by

$$
\begin{equation*}
\mathrm{p}_{\mathrm{e} 0}=\frac{\mathrm{n}_{\mathrm{i}}^{2}}{\mathrm{~N}_{\mathrm{D}}} \tag{8.86}
\end{equation*}
$$

where $\mathrm{N}_{\mathrm{D}}$ is the doping density of the $\mathrm{n}^{+}$emitter. At a distance x from the edge of the emitter-base depletion region, we have

$$
\begin{equation*}
\mathrm{p}_{\mathrm{e}}(\mathrm{x}) \cong \mathrm{p}_{\mathrm{e}}(0) \mathrm{e}^{-\mathrm{x} / \mathrm{L}_{\mathrm{p}}} \tag{8.87}
\end{equation*}
$$

where

$$
\begin{align*}
\mathrm{p}_{\mathrm{e}}(0) & =\mathrm{p}_{\mathrm{e} 0} \mathrm{e}^{\mathrm{v}_{\mathrm{BE}} / \mathrm{V}_{\mathrm{T}}} \\
& =\frac{\mathrm{n}_{\mathrm{i}}^{2}}{\mathrm{~N}_{\mathrm{D}}} \mathrm{e}^{\mathrm{V}_{\mathrm{BE}} / \mathrm{V}_{\mathrm{T}}} \tag{8.88}
\end{align*}
$$

and where $\mathrm{V}_{\mathrm{BE}}$ is the forward-bias voltage of the base-emitter junction.
At the edge of the base-emitter depletion region, the gradient of the hole concentration in the emitter is found, using (8.87), to be

$$
\begin{equation*}
\left.\frac{\mathrm{dp}_{\mathrm{e}}(\mathrm{x})}{\mathrm{dx}}\right|_{\mathrm{x}=0}=\frac{\mathrm{p}_{\mathrm{e}}(0)}{\mathrm{L}_{\mathrm{p}}} \tag{8.89}
\end{equation*}
$$

Using (8.88), we can rewrite this as

$$
\begin{equation*}
\left.\frac{\mathrm{dp}_{\mathrm{e}}(0)}{\mathrm{dx}}\right|_{\mathrm{x}=0}=\frac{\mathrm{n}_{\mathrm{i}}^{2}}{\mathrm{~L}_{\mathrm{p}} \mathrm{~N}_{\mathrm{D}}} \mathrm{e}^{\mathrm{v}_{\mathrm{BE}} / \mathrm{V}_{\mathrm{T}}} \tag{8.90}
\end{equation*}
$$

The hole current is now found using the diffusion equation

$$
\begin{equation*}
I_{p e}=\left.A_{E} q D_{p} \frac{\mathrm{dp}_{e}(x)}{d x}\right|_{x=0} \tag{8.91}
\end{equation*}
$$

where $A_{E}$ is the effective area of the emitter. Recall that the minority-hole current in the emitter, $I_{p e}$, is closely equal to the base current, $\mathrm{I}_{\mathrm{B}}$. After combining (8.90) and (8.91), we obtain

$$
\begin{equation*}
I_{B}=\frac{A_{E} q D_{p} n_{i}^{2}}{L_{p} N_{D}} e^{v_{B E} v_{T}} \tag{8.92}
\end{equation*}
$$

The situation on the base side of the base-emitter junction is somewhat different. The concentration of the minority carriers, in this case electrons that diffused from the emitter, is given by a similar equation,

$$
\begin{equation*}
n_{b}(0)=\frac{n_{i}^{2}}{N_{A}} e^{v_{B E} / V_{T}} \tag{8.93}
\end{equation*}
$$

However, the gradient of this concentration at the edge of the base-emitter depletion region is calculated differently. This difference in gradient concentration is due to the close proximity of the collector-base junction, where the minority carrier (electron) concentration, $\mathrm{n}_{\mathrm{b}}(\mathrm{W})$, must be zero. This zero concentration at the collector-base junction occurs because any electrons diffusing to the edge of the collector-base depletion region immediately drift across the junction to the collector, as stated previously. If the base "width" is much shorter than the diffusion length of electrons in the base, $L_{n}$, then almost no electrons will recombine with base majority carriers (holes) before they diffuse to the collector-base junction. Given this fact, the decrease in electron or minority concentration from the base-emitter junction to the collector-base junction is a linear relationship decreasing from $n_{b}(0)$ at the emitter junction to zero at the collector junction in distance W . This assumption ignores any recombination of electrons in the base as they travel to the collector, which is a reasonable assumption for modern transistors that have very narrow bases. Thus, throughout the base region, the gradient of the minority-carrier concentration is closely given by

$$
\begin{align*}
\frac{d n_{b}(x)}{d x} & =-\frac{n_{b}(0)}{W} \\
& =-\frac{n_{i}^{2}}{W N_{A}} e^{v_{B E} / v_{T}} \tag{8.94}
\end{align*}
$$

Combining (8.94) with the diffusion equation, we obtain

$$
\begin{align*}
I_{n b} & =-A_{E} q D_{n} \frac{d n_{b}(0)}{d x} \\
& =\frac{A_{E} q D_{n} n_{i}^{2}}{W N_{A}} e^{v_{B E} / V_{T}} \tag{8.95}
\end{align*}
$$

Remembering that $I_{n b}$ is closely equal to the collector current $I_{C}$, we have

$$
\begin{equation*}
\mathrm{I}_{\mathrm{C}} \cong \mathrm{I}_{\mathrm{Cs}} \mathrm{e}^{\mathrm{v}_{\mathrm{BE}} / \mathrm{v}_{\mathrm{T}}} \tag{8.96}
\end{equation*}
$$

where

$$
\begin{equation*}
I_{C S}=\frac{A_{E} q D_{n} n_{i}^{2}}{W N_{A}} \tag{8.97}
\end{equation*}
$$

The ratio of the collector current to the base current, commonly called the transistor common-emitter current gain and denoted $\beta$, is found using (8.96), (8.97), and (8.92). We have

$$
\begin{equation*}
\beta=\frac{I_{C}}{I_{B}}=\frac{D_{n} N_{D} L_{p}}{D_{p} N_{A} W} \cong 2.5 \frac{N_{D}}{N_{A}} \frac{L_{p}}{W} \tag{8.98}
\end{equation*}
$$

which is a constant independent of voltage and current. Noting that $N_{D} \gg N_{A}, L_{p}>W$, and $D_{n} \cong 2.5 D_{p}$, we have $\beta \gg 1$. A typical value might be between 50 and 200 . The derivation of $\beta$ just presented ignores many
second-order effects that make $\beta$ somewhat current and voltage dependent and are beyond the scope of this book. Interested readers should see [Roulston, 1990] for more details. Regardless of second-order effects, equation (8.98) does reflect the approximate relationships among $\beta$, doping levels, and base width. For example, (8.98) explains why heavily doped emitters are important to achieve large current gain.

### 8.6.2 Base Charge Storage of an Active BJT

Figure 8.26 shows a minority-carrier storage in the base region, $Q_{b}$, given by

$$
\begin{equation*}
Q_{b}=A_{E} q \frac{n_{b}(0) W}{2} \tag{8.99}
\end{equation*}
$$

Using (8.93) for nb(0), we have

$$
\begin{equation*}
Q_{b}=\frac{A_{E} q n_{i}^{2} W}{2 N_{A}} e^{v_{B E} V_{T}} \tag{8.100}
\end{equation*}
$$

This equation can be rewritten using (8.96) and (8.97) to obtain

$$
\begin{equation*}
\mathrm{Q}_{\mathrm{b}}=\frac{\mathrm{W}^{2}}{2 \mathrm{D}_{\mathrm{n}}} \mathrm{I}_{\mathrm{C}}=\tau_{\mathrm{b}} \mathrm{I}_{\mathrm{c}} \tag{8.101}
\end{equation*}
$$

where $\tau_{\mathrm{b}}$, called the base-transit time constant, is given approximately by

$$
\begin{equation*}
\tau_{\mathrm{b}}=\frac{\mathrm{W}^{2}}{2 \mathrm{D}_{\mathrm{n}}} \tag{8.102}
\end{equation*}
$$

ignoring second-order effects. Normally, the base-transit time constant is specified for a given technology and takes into account other charge-storage effects not considered here, and is therefore often denoted $\tau_{\mathrm{T}}$. However, since the base storage of electrons dominates the other effects, we have $\tau_{\tau} \cong \tau_{\mathrm{b}}$.

If the current in a BJT changes, the base charge storage must also change. This change can be modelled by a diffusion capacitance, $\boldsymbol{C}_{\mathrm{d}}$, between the base and the emitter terminals. Using (8.101), we have

$$
\begin{equation*}
\mathrm{C}_{\mathrm{d}} \cong \frac{\mathrm{dQ}_{\mathrm{b}}}{\mathrm{dV}_{\mathrm{BE}}}=\frac{\mathrm{d}\left(\tau_{\mathrm{b}} \mathrm{I}_{\mathrm{C}}\right)}{\mathrm{dV}_{\mathrm{BE}}} \tag{8.103}
\end{equation*}
$$

Using (8.103) and $I_{C}=I_{C S} e^{V_{B E} / V_{T}}$ results in

$$
\begin{equation*}
\mathrm{C}_{\mathrm{d}}=\tau_{\mathrm{b}} \frac{\mathrm{I}_{\mathrm{C}}}{\mathrm{~V}_{\mathrm{T}}} \tag{8.104}
\end{equation*}
$$

This equation is similar to that for a diode.

## 8.7 SUMMARY OF KEY POINTS

- Bipolar devices offer advantages over CMOS devices when high-speed operation must be combined with high gain and/or high breakdown voltages. However, unlike MOSFETs, they draw a nonzero dc base current. [p. 331]
- In active mode, with base-emitter junction forward-biased and base-collector junction reverse-biased, collector current increases exponentially with base-emitter voltage, and the base current is a factor smaller. The variation in collector current with collector voltage is first-order modeled by the Early voltage. [p. 334]
- As the base-collector junction approaches forward-bias, at collector-emitter voltages of about 0.2 to 0.3 V , a finite base-collector current flows, and the transistor is saturated. [p. 335]
- The time required to remove the charge stored in a saturated transistor is much larger than the time required to turn off a transistor in the active region. Hence, in high-speed microcircuit designs, one never allows bipolar transistors to saturate. [p. 337]
- BJT small-signal transconductance is proportional to collector current. [p. 338]
- The high-frequency operation of active BJTs is limited by capacitances modeling charge storage in the depletion regions and the storage of diffusing charge-carriers in the base. [p. 341]
- Active BJTs offer an intrinsic gain that is generally higher than that of MOS transistors and independent of operating point. [p. 342]
- BJT unity-gain frequency increases in proportion to bias current up to a limit imposed by the transit time of carriers through the base. Hence, the base thickness is a critical parameter limiting the maximum operating speed of a BJT. [p. 343]
- High-performance modern bipolar transistors are manufactured by epitaxially growing a very thin base region. The use of a different material for the base, such as silicon-germanium, results in a heterojunction bipolar transistor (HBT) whose bandgap structure can be tailored to provide high current gain, high unity-gain frequency, and/or high Early voltage. [p. 348]
- Bipolar current mirrors are similar to CMOS mirrors, except that finite base current is a source of mismatch between the input and output currents. [p. 349]
- At low frequencies, resistances in series with the emitter appear $(\beta+1)$ times larger when seen looking into the base. [p. 352]
- Resistances in series with the base are divided by $(\beta+1)$ when they are seen looking into the emitter. [p. 353]

## 8.9 PROBLEMS

Unless otherwise stated, assume npn bipolar transistors with parameters as listed in Table 8.1.
