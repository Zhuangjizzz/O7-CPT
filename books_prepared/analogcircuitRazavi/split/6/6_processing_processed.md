# 6  Physics of MOS Transistors

Today's field of microelectronics is dominated by a type of device called the metal-oxide-semiconductor field-effect transistor (MOSFET). Conceived in the 1930s but first realized in the 1960s, MOSFETs (also called MOS devices) offer unique properties that have led to the revolution of the semiconductor industry. This revolution has culminated in microprocessors having 100 million transistors, memory chips containing billions of transistors, and sophisticated communication circuits providing tremendous signal processing capability.

Our treatment of MOS devices and circuits follows the same procedure as that taken in Chapters 2 and 3 for $p n$ junctions. In this chapter, we analyze the structure and operation of MOSFETs, seeking models that prove useful in circuit design. In Chapter 7, we utilize the models to study MOS amplifier topologies. The outline below illustrates the sequence of concepts covered in this chapter.

Operation of MOSFETs

- MOS Structure
- Operation in Triode Region
- Operation in Saturation
- I/V Characteristics

MOS Device Models

- Large-Signal Model
- Small-Signal Model

PMOS Devices

- Structure
- Models

## 6.1 STRUCTURE OF MOSFET

Recall from Chapter 5 that any voltage-controlled current source can provide signal amplification. MOSFETs also behave as such controlled sources but their characteristics are different from those of bipolar transistors.

In order to arrive at the structure of the MOSFET, we begin with a simple geometry consisting of a conductive (e.g., metal) plate, an insulator ("dielectric"), and a doped
image_name:(a)
description:### Description of Figure 6.1 (a)

1. **Identification of Components and Structure:**
- The diagram illustrates a hypothetical semiconductor device structure consisting of three main layers:
- A **conductive plate** at the top, which is typically metal.
- An **insulator** layer beneath the conductive plate, which acts as a dielectric material.
- A **p-type silicon** substrate at the bottom, which is a semiconductor material.

2. **Connections and Interactions:**
- The conductive plate and the p-type silicon together form a basic capacitor structure. The conductive plate acts as one electrode, while the p-type silicon acts as the other electrode.
- The insulator prevents direct electrical conduction between the conductive plate and the silicon, allowing only capacitive effects.

3. **Labels, Annotations, and Key Features:**
- The diagram is labeled to indicate the conductive plate, insulator, and p-type silicon.
- Arrows show the direction of potential charge movement, suggesting that the p-type silicon mirrors the charge on the conductive plate when a voltage is applied.

This setup illustrates the basic concept of a MOSFET (Metal-Oxide-Semiconductor Field-Effect Transistor), where the gate (conductive plate) controls the flow of charge carriers in the semiconductor channel beneath it.
image_name:(b)
description:The image labeled as (b) illustrates a hypothetical semiconductor device operating as a capacitor. It consists of three main components: a conductive plate, an insulator, and a piece of p-type silicon. The conductive plate is positioned at the top, with the insulator beneath it, and the p-type silicon at the bottom. This structure forms a capacitor due to the conductive nature of the p-type silicon, which mirrors any charge on the conductive plate.

In this configuration, a potential difference (V1) is applied across the device. The positive voltage on the conductive plate attracts electrons from the p-type silicon, forming a channel of electrons just below the insulator. This results in a capacitor-like behavior, where the charge on the conductive plate induces an opposite charge in the silicon, creating an electric field across the insulator.

The diagram includes annotations indicating the direction of the electric field and the formation of the electron channel, which is crucial for understanding the device's operation as a voltage-controlled element.
image_name:(c)
description:The image shows a series of diagrams illustrating the operation of a hypothetical semiconductor device, specifically focusing on the MOSFET structure and its operation. The diagrams are labeled as (a), (b), and (c):

1. **Diagram (a): Basic Structure**
- **Components:**
- A conductive plate (metal) is shown on the top.
- An insulator (dielectric) layer is depicted below the conductive plate.
- A layer of p-type silicon is shown at the bottom.
- **Functionality:**
- This configuration operates as a capacitor, with the p-type silicon acting as a conductive substrate that mirrors the charge on the conductive plate.

2. **Diagram (b): Capacitive Operation**
- **Components:**
- Similar to (a), with the addition of a voltage source labeled **V1**.
- **Connections and Interactions:**
- The voltage source **V1** is connected across the conductive plate and the p-type silicon.
- Positive charge on the conductive plate attracts electrons (negative charge) to the surface of the p-type silicon, forming a channel of electrons.
- **Key Features:**
- The diagram indicates the formation of an electron channel beneath the insulator as a result of the applied voltage.

3. **Diagram (c): Current Flow**
- **Components:**
- Similar to (b), with an additional voltage source labeled **V2**.
- **Connections and Interactions:**
- Voltage source **V1** is still applied across the conductive plate and p-type silicon.
- Voltage source **V2** is applied across the ends of the p-type silicon.
- The combined effect of **V1** and **V2** causes a current to flow through the channel of electrons, as indicated by an arrow.
- **Key Features:**
- The diagram illustrates the operation of the MOSFET as a voltage-controlled current source, where the potential difference **V1** controls the conductivity of the channel, and **V2** drives the current through the channel.

Figure 6.1 (a) Hypothetical semiconductor device, (b) operation as a capacitor, (c) current flow as a result of potential difference.
piece of silicon. Illustrated in Fig. 6.1(a), such a structure operates as a capacitor because the p-type silicon is somewhat conductive, "mirroring" any charge deposited on the top plate.

What happens if a potential difference is applied as shown in Fig. 6.1(b)? As positive charge is placed on the top plate, it attracts negative charge, e.g., electrons, from the piece of silicon. (Even though doped with acceptors, the p-type silicon does contain a small number of electrons.) We therefore observe that a "channel" of free electrons may be created at the interface between the insulator and the piece of silicon, potentially serving as a good conductive path if the electron density is sufficiently high. The key point here is that the density of electrons in the channel varies with $V_{1}$, as evident from $Q=C V$, where $C$ denotes the capacitance between the two plates.

The dependence of the electron density upon $V_{1}$ leads to an interesting property: if, as depicted in Fig. 6.1(c), we allow a current to flow from left to right through the silicon material, $V_{1}$ can control the current by adjusting the resistivity of the channel. (Note that the current prefers to take the path of least resistance, thus flowing primarily through the channel rather than through the entire body of silicon.) This will serve our objective of building a voltage-controlled current source.

Equation $Q=C V$ suggests that, to achieve a strong control of $Q$ by $V$, the value of $C$ must be maximized, for example, by reducing the thickness of the dielectric layer separating the two plates. ${ }^{1}$ The ability of silicon fabrication technology to produce extremely thin but uniform dielectric layers (with thicknesses below $20 \AA$ today) has proven essential to the rapid advancement of microelectronic devices.

The foregoing thoughts lead to the MOSFET structure shown in Fig. 6.2(a) as a candidate for an amplifying device. Called the "gate" $(\mathrm{G})$, the top conductive plate resides on a thin dielectric (insulator) layer, which itself is deposited on the underlying $p$-type silicon "substrate." To allow current flow through the silicon material, two contacts are attached to the substrate through two heavily-doped $n$-type regions because direct connection of metal to the substrate would not produce a good "ohmic" contact. ${ }^{2}$ These two terminals are called "source" (S) and "drain" (D) to indicate that the former can provide charge carriers and the latter can absorb them. Figure 6.2(a) reveals that the device is symmetric with respect to S and D ; i.e., depending on the voltages applied to the device, either of

[^8]image_name:(a)
description:The image labeled as Figure 6.2(a) illustrates the structure of an NMOS (n-type Metal-Oxide-Semiconductor) Field-Effect Transistor (MOSFET). The diagram is a three-dimensional representation showing the various components and their arrangement.

1. **Identification of Components and Structure:**
- **Source (S):** Located on the left, connected to a heavily-doped n-type region (n+). This terminal provides charge carriers, specifically electrons.
- **Drain (D):** Positioned on the right, also connected to an n+ region. This terminal absorbs charge carriers.
- **Gate (G):** Situated above the channel, connected to a conductive plate. It controls the flow of electrons between the source and drain by modulating the electric field.
- **p-Substrate:** The base material of the device, typically made of p-type semiconductor material.
- **Insulator:** A layer between the gate and the substrate, preventing direct current flow between them.

2. **Connections and Interactions:**
- The source and drain are connected through n+ regions to the p-substrate, forming a channel for electron flow when the gate voltage is applied.
- The gate, separated by an insulator, controls the channel's conductivity by applying a voltage, which modulates the electric field and allows or prevents electron flow between the source and drain.

3. **Labels, Annotations, and Key Features:**
- The n+ regions are labeled to indicate the heavily-doped n-type areas.
- The conductive plate is shown as part of the gate structure, highlighting its role in controlling the channel.
- The insulator is clearly marked, emphasizing its importance in isolating the gate from the substrate.

Overall, this diagram provides a detailed view of the NMOS transistor, highlighting its symmetric design and the roles of the source, drain, and gate in electron flow control.
image_name:(b)
description:The image labeled as (b) illustrates a side view of an NMOS (n-type Metal-Oxide-Semiconductor) transistor structure. This diagram provides a simplified representation of the physical layout of the device components.

1. **Identification of Components and Structure:**
- The diagram shows a cross-sectional view of a semiconductor device built on a **p-type substrate**.
- Two heavily doped **n+ regions** are embedded into the substrate, labeled as the **Source (S)** and **Drain (D)**. These regions are responsible for providing and collecting charge carriers, respectively.
- Above the substrate and between the source and drain, there is an **insulating layer** (often silicon dioxide in real devices) that separates the conductive channel from the gate.
- A **gate (G)** terminal is positioned over the insulator, which controls the flow of charge carriers between the source and drain by varying the voltage applied to it.

2. **Connections and Interactions:**
- The **source (S)** and **drain (D)** are connected through the channel region that forms when a voltage is applied to the gate. This allows for the flow of electrons from the source to the drain.
- The **gate (G)** modulates this flow by creating an electric field that influences the conductivity of the channel.

3. **Labels, Annotations, and Key Features:**
- The source, gate, and drain terminals are clearly labeled as **S**, **G**, and **D** respectively.
- The **p-substrate** is labeled to indicate the type of substrate used, which is crucial for understanding the device's operation as an NMOS transistor.
- The presence of the **n+ regions** is noted, highlighting the heavily doped areas that facilitate ohmic contacts with the metal terminals.
image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: S, D: D, G: G}
]
extrainfo:The diagram shows the structure and symbol of an NMOS transistor. It indicates the source (S), drain (D), and gate (G) terminals. The device operates with electrons, as it uses n-type source/drain regions and a p-type substrate.

Figure 6.2 (a) Structure of MOSFET, (b) side view, (c) circuit symbol.
these two terminals can drain the charge carriers from the other. As explained in Section 6.2 , with $n$-type source/drain and $p$-type substrate, this transistor operates with electrons rather than holes and is therefore called an $n$-type MOS (NMOS) device. (The $p$-type counterpart is studied in Section 6.4.) We draw the device as shown in Fig. 6.2(b) for simplicity. Figure 6.2(c) depicts the circuit symbol for an NMOS transistor, wherein the arrow signifies the source terminal.

Before delving into the operation of the MOSFET, let us consider the types of materials used in the device. The gate plate must serve as a good conductor and was in fact realized by metal (aluminum) in the early generations of MOS technology. However, it was discovered that noncrystalline silicon ("polysilicon" or simply "poly") with heavy doping (for low resistivity) exhibits better fabrication and physical properties. Thus, today's MOSFETs employ polysilicon gates.

The dielectric layer sandwiched between the gate and the substrate plays a critical role in the performance of transistors and is created by growing silicon dioxide (or simply
image_name:Figure 6.3
description:The diagram labeled "Figure 6.3" illustrates the cross-sectional view of a modern MOSFET (Metal-Oxide-Semiconductor Field-Effect Transistor). It highlights the typical dimensions and structure of the device.

1. **Identification of Components and Structure:**
- **Polysilicon Gate:** The topmost layer is marked as 'Polysilicon,' which acts as the gate material. It is a heavily doped noncrystalline silicon, providing better physical properties for MOSFETs.
- **Oxide Layer:** Beneath the polysilicon gate is the 'Oxide' layer, which is typically silicon dioxide. This layer acts as the dielectric, insulating the gate from the substrate.
- **Source/Drain Diffusion:** Labeled as 'S/D Diffusion,' these are the n+ regions on either side of the gate. They are heavily doped to form the source and drain terminals of the MOSFET.
- **p-Substrate:** The base material is a p-type substrate, which forms the body of the transistor.
- **Oxide-Silicon Interface:** The interface between the oxide layer and the silicon substrate is crucial for the device's operation.

2. **Connections and Interactions:**
- The diagram shows the gate, source, and drain regions. The flow of current in the MOSFET is controlled by the voltage applied to the gate, which modulates the conductivity between the source and drain through the channel formed in the p-substrate.
- The n+ source and drain regions form diodes with the p-substrate, which must remain reverse-biased for proper operation, indicated by the small diode symbols.

3. **Labels, Annotations, and Key Features:**
- **t_ox = 18 Å:** This label indicates the thickness of the oxide layer, which is 18 angstroms, a critical dimension affecting the capacitance and performance of the device.
- **Length = 90 nm:** The horizontal length of the gate region is specified as 90 nanometers, reflecting the scale of modern MOSFETs.

Overall, the diagram provides a detailed view of the structural and dimensional aspects of a MOSFET, essential for understanding its fabrication and operation.

Figure 6.3 Typical dimensions of today's MOSFETs.
"oxide") on top of the silicon area. The $n^{+}$regions are sometimes called source/drain "diffusion," referring to a fabrication method used in early days of microelectronics. We should also remark that these regions in fact form diodes with the $p$-type substrate (Fig. 6.3). As explained later, proper operation of the transistor requires that these junctions remain reverse-biased. Thus, only the depletion region capacitance associated with the two diodes must be taken into account. Figure 6.3 shows some of the device dimensions in today's state-of-the-art MOS technologies. The oxide thickness is denoted by $t_{o x}$.

## 6.2 OPERATION OF MOSFET

This section deals with a multitude of concepts related to MOSFETs. The outline is shown in Fig. 6.4.
image_name:Figure 6.4 Outline of concepts to be studied
description:The diagram titled "Figure 6.4 Outline of concepts to be studied" outlines the key concepts related to the operation of MOSFETs and is organized into four main blocks, each representing a category of study.

1. **Qualitative Analysis**:
- This block includes fundamental concepts such as:
- *Formation of Channel*: Understanding how a conductive path is created between the source and drain.
- *MOSFET as Resistor*: Examining how a MOSFET can function as a resistive element.
- *Channel Pinch-off*: Describing the condition where the channel is constricted, affecting current flow.
- *I/V Characteristics*: Studying the current-voltage relationships of the MOSFET.

2. **I/V Characteristics**:
- This section delves deeper into the electrical properties, focusing on:
- *Channel Charge Density*: The distribution of charge within the channel.
- *Drain Current*: The current flowing from the drain to the source.
- *Triode and Saturation Regions*: Different operational regions of the MOSFET based on voltage levels.

3. **Analog Properties**:
- This block highlights important analog characteristics:
- *Transconductance*: A measure of the MOSFET's ability to control output current via input voltage.
- *Channel-Length Modulation*: How variations in channel length affect the device's behavior.

4. **Other Properties**:
- This section covers additional effects and phenomena:
- *Body Effect*: Influence of the substrate voltage on the threshold voltage.
- *Subthreshold Conduction*: Current flow when the MOSFET is below the threshold voltage.
- *Velocity Saturation*: The limiting of carrier velocity at high electric fields.

**Flow of Information or Control**:
- The diagram suggests a logical progression from understanding basic qualitative aspects to more complex analog properties and other effects.
- Each block is connected with arrows indicating the flow of study or analysis from one concept to the next, showing a structured approach to comprehending MOSFET operations.

**Overall System Function**:
- The primary function of this diagram is to provide a comprehensive framework for studying and understanding the various operational aspects of MOSFETs. By organizing the concepts into these four categories and showing the connections between them, the diagram facilitates a systematic exploration of MOSFET behavior, from basic principles to advanced properties.

Figure 6.4 Outline of concepts to be studied.

### 6.2.1 Qualitative Analysis

Our study of the simple structures shown in Figs. 6.1 and 6.2 suggests that the MOSFET may conduct current between the source and drain if a channel of electrons is created by making the gate voltage sufficiently positive. Moreover, we expect that the magnitude of the current can be controlled by the gate voltage. Our analysis will indeed confirm these conjectures while revealing other subtle effects in the device. Note that the gate terminal draws no (low-frequency) current as it is insulated from the channel by the oxide.

Since the MOSFET contains three terminals, ${ }^{3}$ we may face many combinations of terminal voltages and currents. Fortunately, with the (low-frequency) gate current being zero, the only current of interest is that flowing between the source and the drain. We must study the dependence of this current upon the gate voltage (e.g., for a constant drain voltage) and upon the drain voltage (e.g., for a constant gate voltage). These concepts become clearer below.

Let us first consider the arrangement shown in Fig. 6.5(a), where the source and drain are grounded and the gate voltage is varied. This circuit does not appear partic-

Did you know?

The concept of MOSFET was proposed by Julins Edgar Lilienfeld in 1925, decades before the invention of the bipolar transistor. But why did it take until the 1960s for the MOS transistor to be successfully fabricated? The critical issue was the oxide-silicon interface. In initial attempts, this interface contained many "surface states," trapping the charge carriers and leading to poor conduction. As semiconductor technology advanced and "clean rooms" were invented for fabrication, the oxide could be grown on silicon with almost no surface states, yielding a high transconductance.
ularly useful but it gives us a great deal of insight. Recall from Fig. 6.1(b) that, as $V_{G}$ rises, the positive charge on the gate must be mirrored by negative charge in the substrate. While we stated in Section 6.1 that electrons are attracted to the interface, in reality, another phenomenon precedes the formation of the channel. As $V_{G}$ increases from zero, the positive charge on the gate repels the holes in the substrate, thereby exposing negative ions and creating a depletion region [Fig. 6.5(b)]. ${ }^{4}$

[^9]image_name:(a)
description:
[
name: VG, type: VoltageSource, ports: {Np: VG, Nn: GND}
name: NMOS, type: NMOS, ports: {S: GND, D: GND, G: VG}
]
extrainfo:The diagram shows a MOSFET with a gate voltage VG applied. The MOSFET is in the off state as the positive charge on the gate repels holes in the substrate, creating a depletion region without forming a conductive channel. The circuit acts as a capacitor with no current flowing from source to drain.
image_name:(b)
description:
[
name: VG, type: VoltageSource, ports: {Np: VG, Nn: GND}
]
extrainfo:The diagram illustrates the formation of a depletion region in a MOSFET structure when a gate voltage (VG) is applied. The depletion region forms as the positive charge on the gate repels holes in the p-substrate, exposing negative ions. The MOSFET is in the 'off' state, preventing current flow from source to drain.
image_name:(c)
description:
[
name: VG, type: VoltageSource, value: VG, ports: {Np: VG, Nn: GND}
name: NMOS, type: NMOS, ports: {S: GND, D: GND, G: VG}
]
extrainfo:The diagram shows the formation of a channel in an NMOS transistor as the gate voltage VG increases, allowing free electrons to form a conductive path between the source and drain. The NMOS is initially off until VG is sufficient to invert the channel.

Figure 6.5 (a) MOSFET with gate voltage, (b) formation of depletion region, (c) formation of channel.

Note that the device still acts as a capacitor-positive charge on the gate is mirrored by negative charge in the substrate-but no channel of mobile charge is created yet. Thus, no current can flow from the source to the drain. We say the MOSFET is off.

Can the source-substrate and drain-substrate junctions carry current in this mode? To avoid this effect, the substrate itself is also tied to zero, ensuring that these diodes are not forward-biased. For simplicity, we do not show this connection in the diagrams.

What happens as $V_{G}$ increases? To mirror the charge on the gate, more negative ions are exposed and the depletion region under the oxide becomes deeper. Does this mean the transistor never turns on?! Fortunately, if $V_{G}$ becomes sufficiently positive, free electrons are attracted to the oxide-silicon interface, forming a conductive channel [Fig. 6.5(c)]. We say the MOSFET is on. The gate potential at which the channel begins to appear is called the "threshold voltage," $V_{T H}$, and falls in the range of 300 mV to 500 mV . Note that the electrons are readily provided by the $n^{+}$source and drain regions, and need not be supplied by the substrate.

It is interesting to recognize that the gate terminal of the MOSFET draws no (lowfrequency) current. Resting on top of the oxide, the gate remains insulated from other terminals and simply operates as a plate of a capacitor.

MOSFET as a Variable Resistor The conductive channel between S and D can be viewed as a resistor. Furthermore, since the density of electrons in the channel must increase as $V_{G}$ becomes more positive (why?), the value of this resistor changes with the gate voltage. Conceptually illustrated in Fig. 6.6, such a voltage-dependent resistor proves extremely useful in analog and digital circuits.
image_name:Figure 6.6 MOSFET viewed as a voltage-dependent resistor
description:
[
name: G, type: NMOS, ports: {S: S, D: D, G: G}
name: X1, type: Resistor, ports: {N1: S, N2: X1}
name: X2, type: Resistor, ports: {N1: X1, N2: X2}
name: X3, type: Resistor, ports: {N1: X2, N2: X3}
name: X4, type: Resistor, ports: {N1: X3, N2: D}
]
extrainfo:The circuit diagram shows a MOSFET configured as a voltage-dependent resistor, with a series of resistors (X1, X2, X3, X4) connected between the source (S) and drain (D) terminals.

Figure 6.6 MOSFET viewed as a voltage-dependent resistor.

Example
6.1

In the vicinity of a wireless base station, the signal received by a cellphone may become very strong, possibly "saturating" the circuits and prohibiting proper operation. Devise a variable-gain circuit that lowers the signal level as the cellphone approaches the base station.

Solution A MOSFET can form a voltage-controlled attenuator along with a resistor as shown in Fig. 6.7.

Since

$$
\begin{equation*}
\frac{v_{\text {out }}}{v_{\text {in }}}=\frac{R_{1}}{R_{M}+R_{1}} \tag{6.1}
\end{equation*}
$$

the output signal becomes smaller as $V_{\text {cont }}$ falls because the density of electrons in the channel decreases and $R_{M}$ rises. MOSFETs are commonly utilized as voltage-dependent resistors in "variable-gain amplifiers."
image_name:Figure 6.7
description:
[
name: Vin, type: VoltageSource, ports: {Np: Vin, Nn: X1}
name: RM, type: Resistor, value: RM, ports: {N1: X1, N2: X4}
name: R1, type: Resistor, value: R1, ports: {N1: Vout, N2: GND}
]
extrainfo:The circuit diagram features a MOSFET used as a voltage-controlled attenuator. The MOSFET's resistance, RM, varies with the control voltage Vcont, affecting the output voltage Vout. The resistor R1 is connected between Vout and ground.

Figure 6.7 Use of MOSFET to adjust signal levels.
Exercise What happens to $R_{M}$ if the channel length is doubled?

In the arrangement of Fig. 6.5(c), no current flows between S and D because the two terminals are at the same potential. We now raise the drain voltage as shown in Fig. 6.8(a) and examine the drain current ( $=$ source current). If $V_{G}<V_{T H}$, no channel exists, the device is off, and $I_{D}=0$ regardless of the value of $V_{D}$. On the other hand, if $V_{G}>V_{T H}$, then $I_{D}>0$ [Fig. 6.8(b)]. In fact, the source-drain path may act as a simple resistor, yielding the $I_{D}-V_{D}$ characteristic shown in Fig. 6.8(c). The slope of the characteristic is equal to $1 / R_{\text {on }}$, where $R_{\text {on }}$ denotes the "on-resistance" of the transistor. ${ }^{5}$

Our brief treatment of the MOS I-V characteristics thus far points to two different views of the operation: in Fig. 6.8(b), $V_{G}$ is varied while $V_{D}$ remains constant whereas in Fig. 6.8(c), $V_{D}$ is varied while $V_{G}$ remains constant. Each view provides valuable insight into the operation of the transistor.

How does the characteristic of Fig. 6.8(b) change if $V_{G}$ increases? The higher density of electrons in the channel lowers the on-resistance, yielding a greater slope. Depicted in Fig. 6.8(d), the resulting characteristics strengthen the notion of voltage-dependent resistance.

[^10]image_name:(a)
description:
[
name: M, type: NMOS, ports: {S: GND, D: VD, G: VG}
name: VG, type: VoltageSource, value: VG, ports: {Np: VG, Nn: GND}
name: VD, type: VoltageSource, value: VD, ports: {Np: VD, Nn: GND}
]
extrainfo:The circuit diagram shows an NMOS transistor with gate voltage VG and drain voltage VD. The source and body are connected to ground. The diagram illustrates the basic operation of the NMOS with varying gate and drain voltages, emphasizing the voltage-dependent resistance of the channel.
image_name:(b)
description:The graph in Fig. 6.8(b) is an **I-V characteristic curve** for a MOSFET, specifically showing the relationship between the drain current ($I_D$) and the gate voltage ($V_G$), while the drain voltage ($V_D$) is held constant.

1. **Type of Graph and Function:**
- The graph is an I-V characteristic curve for a MOSFET.

2. **Axes Labels and Units:**
- The x-axis represents the gate voltage ($V_G$) and is likely measured in volts.
- The y-axis represents the drain current ($I_D$) and is likely measured in amperes.
- Both axes are on a linear scale.

3. **Overall Behavior and Trends:**
- The graph shows a threshold behavior. Initially, as $V_G$ increases from zero, the drain current $I_D$ remains very low until a certain threshold voltage ($V_{TH}$) is reached.
- Beyond this threshold voltage, the drain current $I_D$ increases sharply, indicating the MOSFET is turning on and conducting more current as the gate voltage increases.
- The curve has a positive slope beyond the threshold, indicating the increase in current with gate voltage.

4. **Key Features and Technical Details:**
- The threshold voltage ($V_{TH}$) is a critical point where the MOSFET begins to conduct significantly.
- The sharp increase in $I_D$ beyond $V_{TH}$ reflects the MOSFET entering the saturation region.

5. **Annotations and Specific Data Points:**
- The graph may have annotations indicating the threshold voltage $V_{TH}$, which is a key point on the curve.
- The curve is smooth and continuous, with no abrupt changes other than the threshold transition.
image_name:(c)
description:The graph labeled as Fig. 6.8(c) is an $I_D - V_D$ characteristic graph for a MOSFET, where the gate voltage $V_G$ is held constant. This type of graph is typically used to illustrate how the drain current $I_D$ varies with changes in the drain voltage $V_D$.

**Axes Labels and Units:**
- The x-axis represents the drain voltage $V_D$. The scale and units are not specified, but it is typically measured in volts.
- The y-axis represents the drain current $I_D$, usually measured in amperes (or milliamperes).

**Overall Behavior and Trends:**
- The graph shows a linear increase in the drain current $I_D$ as the drain voltage $V_D$ increases. This linear relationship suggests that the MOSFET is operating in the ohmic or linear region where the device behaves like a variable resistor.

**Key Features and Technical Details:**
- The slope of the line is indicative of the on-resistance $R_{on}^{-1}$ of the MOSFET when $V_G$ is constant. A steeper slope would imply a lower on-resistance.
- The graph does not show saturation, suggesting that the voltage range depicted is within the linear region of operation.

**Annotations and Specific Data Points:**
- The graph includes a reference to $R_{on}^{-1}$, indicating the inverse of the on-resistance. This is a critical parameter in assessing the efficiency and performance of the MOSFET in the linear region.
- There are no specific numerical values or markers on the graph, but the linear trend is clearly depicted with a solid line and a dashed extension, indicating the continuation of the linear trend beyond the visible range.
image_name:(d)
description:The graph in Figure 6.8(d) is an \(I_D-V_D\) characteristic plot for a MOSFET, showing the relationship between the drain current \(I_D\) and the drain voltage \(V_D\) for various gate voltages \(V_G\).

1. **Type of Graph and Function:**
- This is a characteristic curve plot, often used in semiconductor device analysis, specifically for MOSFETs. It illustrates how the drain current changes with variations in the drain voltage for different gate voltages.

2. **Axes Labels and Units:**
- The x-axis represents the drain voltage \(V_D\), typically measured in volts (V).
- The y-axis represents the drain current \(I_D\), usually measured in amperes (A).
- The plot is linear in both axes.

3. **Overall Behavior and Trends:**
- The graph displays a set of linear curves, each corresponding to a different gate voltage \(V_G\). These curves indicate that as \(V_D\) increases, \(I_D\) also increases linearly.
- The slope of each line increases with higher \(V_G\) values, indicating that the on-resistance decreases with increasing gate voltage, allowing more current to flow for the same \(V_D\).

4. **Key Features and Technical Details:**
- The plot shows multiple lines, each labeled with a different gate voltage \(V_{G1}, V_{G2}, V_{G3}\), with \(V_{G3} > V_{G2} > V_{G1}\).
- The lines do not intersect, and each successive line is steeper than the previous one, demonstrating the effect of increased gate voltage on channel conductivity.

5. **Annotations and Specific Data Points:**
- The plot may include specific annotations such as \(R_{on}^{-1}\) to indicate the inverse of the on-resistance, though this is typically more relevant in the context of Figure 6.8(c).
- The graph visually supports the concept that increasing \(V_G\) enhances the channel's electron density, thus reducing resistance and increasing current flow for a given \(V_D\).

This graph helps illustrate the voltage-dependent behavior of the MOSFET, highlighting how changes in gate voltage can significantly affect the device's electrical characteristics.

Figure 6.8 (a) MOSFET with gate and drain voltages, (b) $I_{D}-V_{G}$ characteristic, (c) $I_{D}-V_{D}$ characteristic, (d) $I_{D}-V_{D}$ characteristics for various gate voltages

Recall from Chapter 2 that charge flow in semiconductors occurs by diffusion or drift. How about the transport mechanism in a MOSFET? Since the voltage source tied to the drain creates an electric field along the channel, the current results from the drift of charge.

The $I_{D}-V_{G}$ and $I_{D^{-}}-V_{D}$ characteristics shown in Figs. 6.8 (b) and (c), respectively, play a central role in our understanding of MOS devices. The following example reinforces the concepts studied thus far.

Sketch the $I_{D}-V_{G}$ and $I_{D}-V_{D}$ characteristics for (a) different channel lengths, and (b) different oxide thicknesses.

Solution As the channel length increases, so does the on-resistance. ${ }^{6}$ Thus, for $V_{G}>V_{T H}$, the drain current begins with lesser values as the channel length increases [Fig. 6.9(a)]. Similarly, $I_{D}$ exhibits a smaller slope as a function of $V_{D}$ [Fig. 6.9(b)]. It is therefore desirable to minimize the channel length so as to achieve large drain currents-an important trend in the MOS technology development.

How does the oxide thickness, $t_{\text {os }}$, affect the 1-V characteristics? As $t_{\text {our }}$ increases, the capacitance between the gate and the silicon substrate decreases. Thus, from $Q=C V$, we note that a given voltage results in less charge on the gate and hence a lower electron density in the channel. Consequently, the device suffers from a higher on-resistance, producing less drain current for a given gate voltage [Fig. 6.9(c)] or drain voltage [Fig. 6.9(d)]. For this reason, the semiconductor industry has continued to reduce the gate oxide thickness.
${ }^{\text {s }}$ Recall that the resistance of a conductor is proportional to the length.
image_name:(a)
description:The graph labeled (a) in Figure 6.9 illustrates the $I_D-V_G$ characteristics for different channel lengths in a semiconductor device. The x-axis represents the gate voltage ($V_G$), with a threshold voltage ($V_{TH}$) marked on the axis, indicating the point where the device begins to conduct. The y-axis represents the drain current ($I_D$), showing how the current varies with changes in the gate voltage.

This graph is a family of curves, each corresponding to a different channel length. As the gate voltage increases beyond the threshold voltage, the drain current initially rises sharply, indicating the device is turning on. However, the rate of increase of the drain current diminishes as the gate voltage continues to rise, showing a sub-linear region typical for MOSFET devices.

The curves demonstrate that as the channel length decreases, for a given gate voltage, the drain current increases. This is due to the reduced resistance in shorter channels, allowing more current to flow. The graph highlights the importance of channel length in determining the electrical characteristics of the device, with shorter channels providing higher current levels for the same gate voltage.
image_name:(b)
description:The graph labeled (b) is an \(I_D-V_D\) characteristics plot, which depicts the relationship between the drain current \(I_D\) and the drain voltage \(V_D\) for different channel lengths in a semiconductor device.

1. **Type of Graph and Function:**
- This is a characteristic curve graph, typically used in semiconductor physics to illustrate how the drain current \(I_D\) varies with the drain voltage \(V_D\).

2. **Axes Labels and Units:**
- The x-axis represents the drain voltage \(V_D\).
- The y-axis represents the drain current \(I_D\).
- Units are likely in volts (V) for \(V_D\) and amperes (A) for \(I_D\), although specific units are not labeled in the diagram.

3. **Overall Behavior and Trends:**
- The graph shows multiple curves, each representing a different channel length.
- As the channel length decreases, the curves shift upwards, indicating that a shorter channel length results in a higher drain current for the same drain voltage.
- The curves exhibit an initial linear increase in \(I_D\) with \(V_D\), followed by a saturation region where \(I_D\) levels off as \(V_D\) continues to increase.

4. **Key Features and Technical Details:**
- The initial linear region represents the ohmic or linear region, where the device behaves like a resistor.
- The saturation region occurs when the drain current reaches a maximum and remains relatively constant despite further increases in \(V_D\).
- The transition from the linear to the saturation region occurs at different \(V_D\) values depending on the channel length.

5. **Annotations and Specific Data Points:**
- The graph includes schematic representations of the device structure, indicating the changes in channel length.
- There are no numerical annotations or specific data points provided on the graph, but the trends are clearly indicated by the direction of the arrows, showing the effect of reducing channel length.
image_name:(c)
description:The graph in Figure 6.9(c) is an \( I_D-V_G \) characteristics plot for different oxide thicknesses. This graph is a type of semiconductor device characteristic curve, specifically illustrating the relationship between the drain current \( I_D \) and the gate voltage \( V_G \) for a MOSFET device.

**Axes Labels and Units:**
- The x-axis represents the gate voltage \( V_G \), starting from a threshold voltage \( V_{TH} \) and increasing to the right. The units are typically in volts (V).
- The y-axis represents the drain current \( I_D \), increasing upwards. The units are typically in amperes (A).

**Overall Behavior and Trends:**
- The graph shows a family of curves, each corresponding to a different oxide thickness.
- As the gate voltage \( V_G \) increases beyond the threshold voltage \( V_{TH} \), the drain current \( I_D \) increases.
- The curves exhibit a steep rise after \( V_{TH} \), indicating the onset of strong inversion in the MOSFET channel.
- Thicker oxide layers result in lower drain current for the same gate voltage, as indicated by the downward shift of the curves.

**Key Features and Technical Details:**
- The threshold voltage \( V_{TH} \) is a critical point where the curves begin to rise sharply.
- The separation between the curves illustrates the effect of oxide thickness on device performance, with thinner oxides allowing for higher \( I_D \) at the same \( V_G \).

**Annotations and Specific Data Points:**
- The graph is annotated with arrows showing the trend of decreasing oxide thickness leading to increased \( I_D \).
- No specific numerical values are provided for \( V_G \) or \( I_D \), but the qualitative trend is clear: reducing oxide thickness enhances current conduction for a given gate voltage.
image_name:(d)
description:The graph labeled (d) is an $I_D-V_D$ characteristic curve for different oxide thicknesses in a semiconductor device. The x-axis represents the drain voltage ($V_D$), while the y-axis represents the drain current ($I_D$). The graph is plotted in a linear scale.

Overall, the graph illustrates how the drain current varies with the drain voltage for different oxide thicknesses. There are multiple curves shown, each representing a different oxide thickness. The curves start from the origin and rise with increasing $V_D$, indicating a positive correlation between $I_D$ and $V_D$.

Key features include:
1. **Trend:** As the oxide thickness decreases, the curves show a higher $I_D$ for the same $V_D$, indicating that thinner oxides result in higher current flow.
2. **Behavior:** The curves exhibit a linear region initially, which then transitions into a saturation region as $V_D$ increases further.
3. **Annotations:** The graph includes arrows indicating the direction of decreasing oxide thickness, emphasizing the trend that thinner oxides enhance current conduction.

The graph effectively demonstrates the impact of oxide thickness on the device's electrical characteristics, showing that reducing oxide thickness can improve the device's performance by allowing more current to flow at lower drain voltages.

Figure 6.9 (a) $I_{D}-V_{G}$ characteristics for different channel lengths, (b) $I_{D}-V_{D}$ characteristics for different channel lengths, (c) $I_{D}-V_{G}$ characteristics for different oxide thicknesses, (d) $I_{D}-V_{D}$ characteristics for different oxide thicknesses.

Exercise The current conduction in the channel is in the form of drift. If the mobility falls at high temperatures, what can we say about the on-resistance as the temperature goes up?

While both the length and the oxide thickness affect the performance of MOSFETs, only the former is under the circuit designer's control, i.e., it can be specified in the "layout" of the transistor. The latter, on the other hand, is defined during fabrication and remains constant for all transistors in a given generation of the technology.

Another MOS parameter controlled by circuit designers is the width of the transistor, the dimension perpendicular to the length [Fig. 6.10(a)]. We therefore observe that
image_name:(a)
description:The image depicts a cross-sectional view of a Metal-Oxide-Semiconductor Field-Effect Transistor (MOSFET). The diagram highlights the key dimensions and structural components of the MOSFET, which are critical for its operation.

1. **Identification of Components and Structure:**
- The diagram shows a layered structure with a channel region between two source/drain regions, labeled as \( n^+ \). These regions are heavily doped with n-type impurities.
- Above the channel, there is a gate structure consisting of a conductive material, typically polysilicon or metal, separated from the channel by a thin insulating oxide layer.

2. **Connections and Interactions:**
- The channel length \( L \) is the distance between the two \( n^+ \) regions, which influences the current flow when the MOSFET is active.
- The width \( W \) of the transistor is perpendicular to the length and also under the designer's control, affecting the current-carrying capability of the device.
- The oxide thickness \( t_{ox} \) is shown as the distance between the gate and the channel, crucial for the gate's ability to control the channel conductivity.

3. **Labels, Annotations, and Key Features:**
- **\( W \):** Represents the width of the MOSFET, a parameter adjustable by circuit designers.
- **\( L \):** Indicates the channel length, another designer-controlled dimension.
- **\( t_{ox} \):** Represents the thickness of the oxide layer, which is fixed during fabrication and affects the gate capacitance.

This diagram is fundamental for understanding how the physical dimensions of a MOSFET influence its electrical characteristics and performance in circuits.

(a)
image_name:(b)
description:The graph labeled as (b) consists of two separate plots, both illustrating the impact of gate width (W) on the drain current (I_D) characteristics of a MOSFET.

1. **Type of Graph and Function:**
- The graph depicts the I_D characteristics, specifically focusing on how the drain current varies with changes in gate voltage (V_G) and drain voltage (V_D) for different gate widths.

2. **Axes Labels and Units:**
- The left plot has the x-axis labeled as V_G (gate voltage) and the y-axis as I_D (drain current).
- The right plot has the x-axis labeled as V_D (drain voltage) and the y-axis as I_D (drain current).
- No specific units are provided on the axes, but they typically represent volts for V_G and V_D, and amperes for I_D.

3. **Overall Behavior and Trends:**
- **Left Plot:**
- The curves show a threshold behavior starting at V_TH (threshold voltage), beyond which the drain current increases with gate voltage.
- As the width (W) increases, the slope of the I_D-V_G curve becomes steeper, indicating higher current for the same gate voltage.
- **Right Plot:**
- The curves demonstrate a linear increase in drain current with increasing drain voltage.
- Similarly, as the width (W) increases, the slope of the I_D-V_D curve also becomes steeper, indicating that a wider MOSFET can conduct more current.

4. **Key Features and Technical Details:**
- The threshold voltage (V_TH) is marked on the left plot, which is the point where the drain current begins to increase significantly.
- In both plots, arrows indicate the direction of increasing width (W), showing that larger widths result in higher drain currents.

5. **Annotations and Specific Data Points:**
- The plots use arrows to indicate the effect of increasing width, emphasizing the parallel shift in the I_D characteristics.
- No specific numerical values are provided, but the trend is clearly depicted with multiple curves for different widths.

(b)
image_name:(c)
description:The image labeled as "(c)" represents a conceptual diagram illustrating the equivalence of multiple MOSFET devices connected in parallel. The diagram is a three-dimensional representation showing two MOSFET structures side by side, indicating how they can be combined to function as a single device with increased width (W).

1. **Identification of Components and Structure:**
- The diagram features two MOSFET devices, each with a source (S), gate (G), and drain (D) terminal. These terminals are marked with labels 'S', 'G', and 'D' respectively.
- Each MOSFET is depicted with a channel region between the source and drain, over which the gate is placed.
- The structure highlights the lateral dimensions, particularly the width (W), which can be adjusted by circuit designers.

2. **Connections and Interactions:**
- The source terminals of both MOSFETs are connected together, as are the gate and drain terminals. This parallel connection effectively increases the total width of the channel, allowing for greater current flow.
- The diagram implies that by increasing the width through parallel connections, the overall resistance between the source and drain is reduced, enhancing the current carrying capability.

3. **Labels, Annotations, and Key Features:**
- The image includes labels for each terminal (S, G, D), which are crucial for understanding the flow of current and the control mechanism of the device.
- The illustration emphasizes the concept of combining devices to achieve desired electrical characteristics by manipulating the physical dimensions (width in this case).
- The visual representation helps to convey the idea that lateral dimensions such as width (W) are under the control of the circuit designer, contrasting with vertical dimensions that are fixed.

(c)

Figure 6.10 (a) Dimensions of a MOSFET ( $W$ and $L$ are under circuit designer's control), (b) $I_{D}$ characteristics for different values of $W$, (c) equivalence to devices in parallel.
"lateral" dimensions such as $L$ and $W$ can be chosen by circuit designers whereas "vertical" dimensions such as $t_{o x}$ cannot.

How does the gate width impact the I-V characteristics? As $W$ increases, so does the width of the channel, thus lowering the resistance between the source and the drain ${ }^{7}$ and yielding the trends depicted in Fig. 6.10(b). From another perspective, a wider device can be viewed as two narrower transistors in parallel, producing a high drain current [Fig. 6.10(c)]. We may then surmise that $W$ must be maximized, but we must also note that the total gate capacitance increases with $W$, possibly limiting the speed of the circuit. Thus, the width of each device in the circuit must be chosen carefully.

Channel Pinch-Off Our qualitative study of the MOSFET thus far implies that the device acts as a voltage-dependent resistor if the gate voltage exceeds $V_{T H}$. In reality, however, the transistor operates as a current source if the drain voltage is sufficiently positive. To understand this effect, we make two observations: (1) to form a channel, the potential difference between the gate and the oxide-silicon interface must exceed $V_{T H}$; (2) if the drain voltage remains higher than the source voltage, then the voltage at each point along the channel with respect to ground increases as we go from the source towards the drain. Illustrated in Fig. 6.11(a), this effect arises from the gradual voltage drop along the channel resistance. Since the gate voltage is constant (because the gate is conductive but carries no current in any direction), and since the potential at the oxide-silicon interface rises from the source to the drain, the potential difference between the gate and the oxide-silicon interface decreases along the $x$-axis [Fig. 6.11(b)]. The density of electrons in the channel follows the same trend, falling to a minimum at $x=L$ 。
image_name:Figure 6.11 (a)
description:
[
name: V_G, type: VoltageSource, value: V_G, ports: {Np: VG, Nn: GND}
name: V_D, type: VoltageSource, value: V_D, ports: {Np: VD, Nn: GND}
]
extrainfo:The diagram illustrates the potential difference along the channel in an NMOS transistor. The voltage drops from VG at the source to VG-VD at the drain, indicating a decrease in electron density along the channel. The current ID flows from the drain to the source.
image_name:Figure 6.11 (b)
description:The graph in Figure 6.11(b) is a plot representing the gate-substrate voltage difference along the channel of a MOSFET device. This is a line graph with the x-axis labeled as \( x \), representing the position along the channel from the source to the drain, up to a length \( L \). The y-axis is labeled as \( V(x) \), indicating the potential difference between the gate and the oxide-silicon interface.

**Type of Graph and Function:**
- The graph is a line graph showing the variation of potential difference along the channel length.

**Axes Labels and Units:**
- **x-axis:** \( x \), representing the position along the channel.
- **y-axis:** \( V(x) \), representing the potential difference between the gate and the oxide-silicon interface.

**Overall Behavior and Trends:**
- The graph shows an increasing trend of the potential difference \( V(x) \) as \( x \) increases from the source towards the drain.
- The potential difference starts at a minimum value at the source and increases gradually towards the drain, reaching a maximum at \( x = L \).

**Key Features and Technical Details:**
- The potential difference is maximum at \( x = L \), where it equals \( V_G - V_D \), indicating the drain voltage's influence.
- The shape of the graph suggests a nonlinear increase, likely due to the gradual voltage drop along the channel resistance.

**Annotations and Specific Data Points:**
- The graph is annotated with potential difference values: \( = V_G \), \( < V_G \), and \( = V_G - V_D \), indicating changes along the channel.

(a)
image_name:Gate-Substrate Potential Difference
description:The graph titled "Gate-Substrate Potential Difference" depicts the variation of potential difference between the gate and substrate along the channel, represented on the x-axis. The x-axis is labeled with the variable \( x \) and extends to \( L \), likely indicating the length of the channel. The y-axis represents the potential difference and is marked with two key values: \( V_G \) at the top and \( V_D - V_G \) at the bottom.

The graph illustrates a nonlinear decrease in potential difference from \( V_G \) to \( V_D - V_G \) as \( x \) increases from 0 to \( L \). This suggests that the potential difference decreases gradually along the channel, likely due to the resistance encountered.

Key features include:
- A starting point at \( x = 0 \) where the potential difference is \( V_G \).
- A smooth, nonlinear downward curve indicating a gradual reduction in potential difference.
- At \( x = L \), the potential difference reaches its minimum value of \( V_D - V_G \), showing the influence of the drain voltage.

The graph is annotated with these potential difference values, highlighting the change from \( V_G \) to \( V_D - V_G \) along the channel. This reflects the voltage drop along the channel due to the resistance, which is consistent with the behavior of potential difference in such systems.

(b)

Figure 6.11 (a) Channel potential variation, (b) gate-substrate voltage difference along the channel.

[^11]image_name:Figure 6.12 (a)
description:
[
name: Device1, type: NMOS, ports: {S: GND, D: VD, G: VG}
name: Device2, type: NMOS, ports: {S: GND, D: VD, G: VG}
]
extrainfo:The diagram illustrates the pinchoff condition in NMOS transistors when the drain voltage VD is high enough to satisfy the condition VG - VD ≤ VTH. The channel ceases to exist near the drain, causing a significant reduction in current flow.
image_name:Figure 6.12 (b)
description:
[
name: VG, type: VoltageSource, value: VG, ports: {Np: VG, Nn: GND}
name: VD, type: VoltageSource, value: VD, ports: {Np: VD, Nn: GND}
name: NMOS, type: NMOS, ports: {S: GND, D: VD, G: VG}
]
extrainfo:The diagram illustrates the effect of drain voltage on channel length modulation in an NMOS transistor. The voltage sources VG and VD control the gate and drain voltages, respectively. The channel is shown to be pinched off near the drain when VD is sufficiently high.
image_name:Figure 6.12 (c)
description:
[
name: VG, type: VoltageSource, value: VG, ports: {Np: VG, Nn: GND}
name: VD, type: VoltageSource, value: VD, ports: {Np: VD, Nn: GND}
name: NMOS, type: NMOS, ports: {S: GND, D: VD, G: VG}
]
extrainfo:The circuit illustrates the operation of an NMOS transistor with gate voltage VG and drain voltage VD. The diagram shows the electron flow and the impact of the drain voltage on the channel length, particularly near the drain, where the channel is pinched off if VD exceeds VG-VTH.

Figure 6.12 (a) Pinchoff, (b) variation of length with drain voltage, (c) detailed operation near the drain.

From these observations, we conclude that, if the drain voltage is high enough to produce $V_{G}-V_{D} \leq V_{T H}$, then the channel ceases to exist near the drain. We say the gatesubstrate potential difference is not sufficient at $x=L$ to attract electrons and the channel is "pinched off" [Fig. 6.12(a)].

What happens if $V_{D}$ rises even higher than $V_{G}-V_{T H}$ ? Since $V(x)$ now goes from 0 at $x=0$ to $V_{D}>V_{G}-V_{T H}$ at $x=L$, the voltage difference between the gate and the substrate falls to $V_{T H}$ at some point $L_{1}<L$ [Fig. 6.12(b)]. The device therefore contains no channel between $L_{1}$ and $L$. Does this mean the transistor cannot conduct current? No, the device still conducts: as illustrated in Fig. 6.12(c), once the electrons reach the end of the channel, they experience the high electric field in the depletion region surrounding the drain junction and are rapidly swept to the drain terminal. Nonetheless, as shown in the next section, the drain voltage no longer affects the current significantly, and the MOSFET acts as a constant current source-similar to a bipolar transistor in the forward active region. Note that the source-substrate and drain-substrate junctions carry no current.

### 6.2.2 Derivation of I-V Characteristics

With the foregoing qualitative study, we can now formulate the behavior of MOSFETs in terms of their terminal voltages.

Channel Charge Density Our derivations require an expression for the channel charge (i.e., free electrons) per unit length, also called the "charge density." From $Q=C V$, we note
image_name:Figure 6.13 Illustration of capacitance per unit length
description:The image depicts a cross-sectional view of a MOSFET structure, focusing on the concept of capacitance per unit length. It illustrates the gate oxide layer sandwiched between the gate electrode and the channel region, which is formed between two n+ doped regions. These n+ regions represent the source and drain of the MOSFET.

1. **Identification of Components and Structure:**
- **n+ Regions:** These are heavily doped semiconductor regions labeled as 'n+', indicating the source and drain terminals of the MOSFET.
- **Gate Oxide Layer:** A thin insulating layer is visible between the gate electrode and the channel. This layer is crucial for the operation of the MOSFET as it influences the capacitance per unit length.
- **Gate Electrode:** Positioned above the oxide layer, it controls the channel formation by applying a voltage.
- **Channel Width (W):** The width of the channel is indicated by an arrow labeled 'W', which is a critical parameter in determining the device's current-carrying capability.

2. **Connections and Interactions:**
- The gate electrode is isolated from the channel by the oxide layer, forming a capacitor. The capacitance per unit length is determined by the properties of this oxide layer and the width of the channel.
- The n+ regions are connected to form the source and drain, with the channel between them allowing current to flow when a voltage is applied to the gate.

3. **Labels, Annotations, and Key Features:**
- **n+ Labels:** Indicate the heavily doped regions on either side of the channel.
- **Arrow labeled 'W':** Denotes the width of the channel, a key factor in calculating the gate capacitance per unit length.

This diagram is a simplified representation focusing on the capacitance aspect of a MOSFET, highlighting the critical structural components and their roles in device operation.

Figure 6.13 Illustration of capacitance per unit length.
that if $C$ is the gate capacitance per unit length and $V$ the voltage difference between the gate and the channel, then $Q$ is the desired charge density. Denoting the gate capacitance per unit area by $C_{o x}$ (expressed in $\mathrm{F} / \mathrm{m}^{2}$ or $\mathrm{fF} / \mu \mathrm{m}^{2}$ ), we write $C=W C_{o x}$ to account for the width of the transistor (Fig. 6.13). Moreover, we have $V=V_{G S}-V_{T H}$ because no mobile charge exists for $V_{G S}<V_{T H}$. (Hereafter, we denote both the gate and drain voltages with respect to the source.) It follows that

$$
\begin{equation*}
Q=W C_{o x}\left(V_{G S}-V_{T H}\right) . \tag{6.2}
\end{equation*}
$$

Note that $Q$ is expressed in coulomb/meter. Now recall from Fig. 6.11(a) that the channel voltage varies along the length of the transistor, and the charge density falls as we go from the source to the drain. Thus, Eq. (6.2) is valid only near the source terminal, where the channel potential remains close to zero. As shown in Fig. 6.14, we denote the channel potential at $x$ by $V(x)$ and write

$$
\begin{equation*}
Q(x)=W C_{o x}\left[V_{G S}-V(x)-V_{T H}\right], \tag{6.3}
\end{equation*}
$$

noting that $V(x)$ goes from zero to $V_{D}$ if the channel is not pinched off.

Drain Current What is the relationship between the mobile charge density and the current? Consider a bar of semiconductor having a uniform charge density (per unit length) equal to $Q$ and carrying a current $I$ (Fig. 6.15). Note from Chapter 2 that (1) $I$ is given by the total charge that passes through the cross section of the bar in one second, and (2) if the carriers move with a velocity of $v \mathrm{~m} / \mathrm{s}$, then the charge enclosed in $v$ meters along the bar passes through the cross section in one second. Since the charge enclosed in $v$ meters is equal to $Q \cdot v$, we have

$$
\begin{equation*}
I=Q \cdot v . \tag{6.4}
\end{equation*}
$$

image_name:Figure 6.14 Device illustration for calculation of drain current
description:The diagram illustrates a semiconductor device used for calculating drain current, likely a MOSFET or similar transistor. It includes the following components and features:

1. **Semiconductor Regions:**
- Two n+ (heavily doped n-type) regions are depicted, likely representing the source and drain of the device.

2. **Gate Structure:**
- A gate is shown above the channel with a voltage labeled as $V_G$. This gate controls the current flow through the channel.

3. **Channel Region:**
- The region between the two n+ areas is the channel, where the voltage varies as a function of position $x$ along the channel. This is represented by $V(x)$.

4. **Voltage and Current Labels:**
- The source is grounded.
- The drain is connected to a voltage source labeled $V_D$, with the current flowing through the drain labeled as $I_D$.
- The gate voltage is denoted as $V_G$.

5. **Connections and Interactions:**
- The diagram shows the gate voltage $V_G$ influencing the channel's conductivity, thereby controlling the current $I_D$ flowing from the drain to the source.
- The drain-source voltage $V_D$ is applied across the channel, influencing the current flow.

6. **Annotations and Key Features:**
- The length of the channel is denoted as $L$, with a differential element $dx$ marked along the channel.
- The ground connections (GND) are clearly marked for both the source and the drain voltage source.

This diagram is a typical representation of a field-effect transistor, showing the essential components and electrical connections necessary for analyzing the drain current as a function of gate and drain voltages.

Figure 6.14 Device illustration for calculation of drain current.
image_name:Figure 6.14 Device illustration for calculation of drain current
description:The image illustrates a device model used for calculating drain current in a field-effect transistor (FET). It consists of two diagrams, both depicting a rectangular channel on a substrate. The channel is shown at two different time points, \( t = t_1 \) and \( t = t_1 + 1 \text{s} \).

1. **Identification of Components and Structure:**
- The channel is a shaded rectangular region on a larger rectangular substrate.
- The channel has a defined width \( W \), length \( L \), and height \( h \).
- The position \( x_1 \) is marked along the length of the channel.
- The substrate appears to be a flat plane on which the channel sits.

2. **Connections and Interactions:**
- A voltage source \( V_1 \) is connected at \( x_1 \), suggesting an electrical connection influencing the charge movement in the channel.
- The diagram implies movement of charge or current along the length \( x \) of the channel, as indicated by the arrows.
- The velocity \( v \) of the charge is marked, showing the direction of charge flow.

3. **Labels, Annotations, and Key Features:**
- The diagram is labeled with time points \( t = t_1 \) and \( t = t_1 + 1 \text{s} \) to indicate the progression of charge or current flow over time.
- The dimensions \( W \), \( L \), and \( h \) are marked to provide a spatial understanding of the channel.
- The position \( x_1 \) and the voltage \( V_1 \) are annotated to highlight key points of interest in the analysis of the drain current.

Figure 6.15 Relationship between charge velocity and current.

As explained in Chapter 2,

$$
\begin{align*}
v & =-\mu_{n} E  \tag{6.5}\\
& =+\mu_{n} \frac{d V}{d x} \tag{6.6}
\end{align*}
$$

where $d V / d x$ denotes the derivative of the voltage at a given point. Combining Eqs. (6.3), (6.4), and (6.6), we obtain

$$
\begin{equation*}
I_{D}=W C_{o x}\left[V_{G S}-V(x)-V_{T H}\right] \mu_{n} \frac{d V(x)}{d x} . \tag{6.7}
\end{equation*}
$$

Interestingly, since $I_{D}$ must remain constant along the channel (why?), $V(x)$ and $d V / d x$ must vary such that the product of $V_{G S}-V(x)-V_{T H}$ and $d V / d x$ is independent of $x$.

While it is possible to solve the above differential equation to obtain $V(x)$ in terms of $I_{D}$ (and the reader is encouraged to do that), our immediate need is to find an expression for $I_{D}$ in terms of the terminal voltages. To this end, we write

$$
\begin{equation*}
\int_{x=0}^{x=L} I_{D} d x=\int_{V(x)=0}^{V(x)=V_{D S}} \mu_{n} C_{o x} W\left[V_{G S}-V(x)-V_{T H}\right] d V . \tag{6.8}
\end{equation*}
$$

That is,

$$
\begin{equation*}
I_{D}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left[2\left(V_{G S}-V_{T H}\right) V_{D S}-V_{D S}^{2}\right] . \tag{6.9}
\end{equation*}
$$

We now examine this important equation from different perspectives to gain more insight. First, the linear dependence of $I_{D}$ upon $\mu_{n}, C_{o x}$, and $W / L$ is to be expected: a higher mobility yields a greater current for a given drain-source voltage; a higher gate oxide capacitance leads to a larger electron density in the channel for a given gate-source voltage; and a larger $W / L$ (called the device "aspect ratio") is equivalent to placing more transistors in parallel [Fig. 6.10(c)]. Second, for a constant $V_{G S}, I_{D}$ varies parabolically with $V_{D S}$ (Fig. 6.16), reaching a maximum of

$$
\begin{equation*}
I_{D, \max }=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2} \tag{6.10}
\end{equation*}
$$

at $V_{D S}=V_{G S}-V_{T H}$. It is common to write $W / L$ as the ratio of two values e.g., $5 \mu \mathrm{~m} / 0.18 \mu \mathrm{~m}$ (rather than 27.8) to emphasize the choice of $W$ and $L$. While only the
image_name:Figure 6.16
description:The graph in Figure 6.16 is a parabolic plot representing the relationship between the drain current \( I_D \) and the drain-source voltage \( V_{DS} \) for a MOSFET, given a constant gate-source voltage \( V_{GS} \).

1. **Type of Graph and Function:**
- The graph is a plot of \( I_D \) versus \( V_{DS} \), showing a parabolic characteristic.

2. **Axes Labels and Units:**
- The vertical axis represents the drain current \( I_D \), typically measured in amperes (A).
- The horizontal axis represents the drain-source voltage \( V_{DS} \), typically measured in volts (V).

3. **Overall Behavior and Trends:**
- The graph exhibits a parabolic shape, starting at the origin and increasing to a maximum value before decreasing again.
- The maximum point of the parabola occurs at \( V_{DS} = V_{GS} - V_{TH} \), where \( V_{TH} \) is the threshold voltage.

4. **Key Features and Technical Details:**
- The maximum drain current \( I_{D, \text{max}} \) is given by the formula:
\[
I_{D, \text{max}} = \frac{1}{2} \mu_n C_{ox} \frac{W}{L} (V_{GS} - V_{TH})^2
\]
- This maximum occurs at the point \( V_{DS} = V_{GS} - V_{TH} \).

5. **Annotations and Specific Data Points:**
- The graph includes a dotted line marking the maximum current level and the corresponding \( V_{DS} \) value.
- The parabolic curve is emphasized with a solid line up to the maximum point, while the rest of the parabola is indicated with a dashed line beyond the maximum point.

Figure 6.16 Parabolic $I_{D}-V_{D S}$ characteristic.
ratio appears in many MOS equations, the individual values of $W$ and $L$ also become critical in most cases. For example, if both $W$ and $L$ are doubled, the ratio remains unchanged but the gate capacitance increases.

Example Plot the $I_{D}-V_{D S}$ characteristics for different values of $V_{G S}$.
6.3

Solution As $V_{G S}$ increases, so do $I_{D, \max }$ and $V_{G S}-V_{T H}$. Illustrated in Fig. 6.17, the characteristics exhibit maxima that follow a parabolic shape themselves because $I_{D, \max } \propto\left(V_{G S}-V_{T H}\right)^{2}$.
image_name:Figure 6.17 MOS characteristics for different gate-source voltages
description:The graph is a plot of the drain current ($I_D$) versus the drain-source voltage ($V_{DS}$) for a MOS transistor, illustrating the $I_{D}-V_{DS}$ characteristics for different gate-source voltages ($V_{GS}$). The x-axis represents the drain-source voltage ($V_{DS}$), while the y-axis represents the drain current ($I_D$).

Type of Graph and Function:
This is a characteristic curve graph for a MOSFET, showing how the drain current varies with the drain-source voltage for different gate-source voltages.

Axes Labels and Units:
- **X-axis:** $V_{DS}$ (Drain-Source Voltage)
- **Y-axis:** $I_D$ (Drain Current)

Overall Behavior and Trends:
The graph shows three curves for different values of $V_{GS}$, labeled as $V_{GS1}$, $V_{GS2}$, and $V_{GS3}$, where $V_{GS3} > V_{GS2} > V_{GS1}$. Each curve starts at the origin and initially increases linearly, indicating that the transistor is in the ohmic or linear region. As $V_{DS}$ increases, the curves start to saturate, showing a plateau where the current becomes relatively constant, indicating the saturation region.

Key Features and Technical Details:
- **Parabolic Shape:** The maxima of the curves follow a parabolic trajectory as indicated, with $I_{D, \text{max}} \propto (V_{GS} - V_{TH})^2$, where $V_{TH}$ is the threshold voltage.
- **Saturation Points:** The saturation current levels are marked as $I_{D, \text{max2}}$, $I_{D, \text{max3}}$, and $I_{D, \text{max4}}$ for $V_{GS1}$, $V_{GS2}$, and $V_{GS3}$ respectively, showing increasing maximum current levels with increasing $V_{GS}$.

Annotations and Specific Data Points:
- **Threshold Voltage ($V_{TH}$):** Marked on the x-axis, indicating the point where each curve transitions from the linear to the saturation region.
- **Gate-Source Voltages:** Dashed lines from the x-axis to the curves indicate the specific $V_{GS}$ values at which each curve is plotted.

This graph effectively demonstrates how increasing the gate-source voltage $V_{GS}$ results in higher maximum drain current $I_{D, \text{max}}$, highlighting the transistor's operation from the linear to saturation regions.

Figure 6.17 MOS characteristics for different gate-source voltages.
Exercise What happens to the above plots if $t_{o x}$ is halved?

The nonlinear relationship between $I_{D}$ and $V_{D S}$ reveals that the transistor cannot generally be modeled as a simple linear resistor. However, if $V_{D S} \ll 2\left(V_{G S}-V_{T H}\right)$, Eq. (6.9) reduces to:

$$
\begin{equation*}
I_{D} \approx \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right) V_{D S} \tag{6.11}
\end{equation*}
$$

image_name:Figure 6.17 MOS characteristics for different gate-source voltages
description:The graph in Figure 6.17 illustrates the MOSFET characteristics depicting the relationship between the drain current (I_D) and the drain-source voltage (V_DS) for different gate-source voltages (V_GS). It consists of two main parts: the main plot on the left and an inset on the right.

1. **Type of Graph and Function:**
- The graph is a set of I-V characteristic curves for a MOSFET, showing how the drain current (I_D) varies with the drain-source voltage (V_DS) at different gate-source voltages (V_GS).

2. **Axes Labels and Units:**
- The vertical axis represents the drain current (I_D), typically measured in amperes.
- The horizontal axis represents the drain-source voltage (V_DS), typically measured in volts.
- Both axes are linear scales.

3. **Overall Behavior and Trends:**
- The curves demonstrate a nonlinear relationship between I_D and V_DS, indicating that the MOSFET does not behave as a simple linear resistor.
- For small values of V_DS (near the origin), the curves can be approximated by straight lines, suggesting a linear region where the MOSFET behaves like a resistor.
- As V_DS increases, the curves bend upwards, showing the saturation region where the current levels off.
- Each curve corresponds to a different gate-source voltage (V_GS1, V_GS2, V_GS3), with higher V_GS values leading to higher I_D for the same V_DS.

4. **Key Features and Technical Details:**
- The inset on the right highlights the linear region at small V_DS, where the curves appear as straight lines with different slopes.
- The slope of each line in the linear region represents the on-resistance (R_on) of the MOSFET, which decreases with increasing V_GS.

5. **Annotations and Specific Data Points:**
- The graph is annotated with different V_GS levels (V_GS1, V_GS2, V_GS3), indicating the shift in the curves as the gate-source voltage increases.
- The inset provides a magnified view of the linear region, emphasizing the initial linear behavior of the MOSFET at small V_DS values.
image_name:Figure 6.18 Detailed characteristics for small V_DS
description:The graph in Figure 6.18 is a set of MOSFET characteristics illustrating the relationship between the drain current ($I_D$) and the drain-source voltage ($V_{DS}$) for different gate-source voltages ($V_{GS}$). It consists of two parts: a main graph and an inset zoomed-in view.

1. **Type of Graph and Function:**
- The graph is a set of $I_D$ versus $V_{DS}$ characteristic curves for a MOSFET transistor.

2. **Axes Labels and Units:**
- The x-axis represents the drain-source voltage ($V_{DS}$).
- The y-axis represents the drain current ($I_D$).
- Both axes are likely in standard units of volts and amperes, respectively, though specific units are not labeled.

3. **Overall Behavior and Trends:**
- The main graph shows three curves for different gate-source voltages ($V_{GS1}$, $V_{GS2}$, and $V_{GS3}$), each representing a different level of gate bias.
- Each curve starts at the origin and initially exhibits a linear region where $I_D$ increases proportionally with $V_{DS}$, indicating ohmic behavior.
- As $V_{DS}$ increases further, the curves bend, showing a nonlinear region where the MOSFET enters saturation.

4. **Key Features and Technical Details:**
- The inset focuses on the linear region near the origin, showing a zoomed view of the initial linear behavior for small $V_{DS}$.
- In this region, the curves appear as straight lines with different slopes, corresponding to different $V_{GS}$ values. Higher $V_{GS}$ values result in steeper slopes, indicating lower on-resistance ($R_{on}$).

5. **Annotations and Specific Data Points:**
- The curves are annotated with $V_{GS1}$, $V_{GS2}$, and $V_{GS3}$, showing the progression of the gate-source voltage from lowest to highest.
- The inset highlights the linearity of the $I_D$-$V_{DS}$ relationship at small $V_{DS}$ values, which can be approximated by straight lines.

This graph effectively demonstrates how the MOSFET's drain current response varies with changes in gate-source voltage, particularly emphasizing the linear behavior at low $V_{DS}$ values and the transition to saturation at higher $V_{DS}$ values.

Figure 6.18 Detailed characteristics for small $V_{D S}$.
exhibiting a linear $I_{D}-V_{D S}$ behavior for a given $V_{G S}$. In fact, the equivalent on-resistance is given by $V_{D S} / I_{D}$ :

$$
\begin{equation*}
R_{o n}=\frac{1}{\mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)} . \tag{6.12}
\end{equation*}
$$

From another perspective, at small $V_{D S}$ (near the origin), the parabolas in Fig. 6.17 can be approximated by straight lines having different slopes (Fig. 6.18).

As predicted in Section 6.2.1, Eq. (6.12) suggests that the on-resistance can be controlled by the gate-source voltage. In particular, for $V_{G S}=V_{T H}, R_{o n}=\infty$, i.e., the device can operate as an electronic switch.

A cordless telephone incorporates a single antenna for reception and transmission. Explain how the system must be configured.

Solution The system is designed so that the phone receives for half of the time and transmits for the other half. Thus, the antenna is alternately connected to the receiver and the transmitter in regular intervals, e.g., every 20 ms (Fig. 6.19). An electronic antenna switch is therefore necessary here. ${ }^{8}$
image_name:Figure 6.19
description:The system block diagram illustrates the role of an electronic antenna switch in a cordless phone. The diagram is divided into two main sections, each depicting a different state of operation for the antenna.

1. **Main Components:**
- **Antenna:** A single antenna is used for both receiving and transmitting signals.
- **Receiver Block:** This block is responsible for processing incoming signals from the antenna.
- **Transmitter Block:** This block is responsible for sending signals out through the antenna.
- **Electronic Switch:** The switch alternates the connection of the antenna between the receiver and the transmitter.

2. **Flow of Information or Control:**
- **Receiving Mode (Left Diagram):** In this state, the antenna is connected to the receiver. Incoming signals are captured by the antenna and directed to the receiver block for processing. The switch is positioned to allow signal flow from the antenna to the receiver.
- **Transmitting Mode (Right Diagram):** Here, the antenna is connected to the transmitter. Signals from the transmitter block are sent out through the antenna. The switch is positioned to allow signal flow from the transmitter to the antenna.

3. **Labels, Annotations, and Key Indicators:**
- Arrows indicate the direction of signal flow, showing how the antenna alternates between sending and receiving modes.
- The switch positions are marked to show the connection paths in each mode.

4. **Overall System Function:**
- The primary function of this system is to enable a single antenna to handle both the reception and transmission of signals. This is achieved by using an electronic switch that alternates the connection of the antenna between the receiver and transmitter at regular intervals. This configuration allows the cordless phone to operate efficiently without the need for multiple antennas, simplifying the design and reducing hardware complexity.

Figure 6.19 Role of antenna switch in a cordless phone.

Exercise
Some systems employ two antennas, each of which receives and transmits signals. How many switches are needed?

[^12]In most applications, it is desirable to achieve a low on-resistance for MOS switches. The circuit designer must therefore maximize $W / L$ and $V_{G S}$. The following example illustrates this point.

Example In the cordless phone of Example 6.4, the switch connecting the transmitter to the 6.5 antenna must negligibly attenuate the signal, e.g., by no more than $10 \%$. If $V_{D D}=1.8 \mathrm{~V}$, $\mu_{n} C_{o x}=100 \mu \mathrm{~A} / \mathrm{V}^{2}$, and $V_{T H}=0.4 \mathrm{~V}$, determine the minimum required aspect ratio of the switch. Assume the antenna can be modeled as a $50-\Omega$ resistor.

Solution As depicted in Fig. 6.20, we wish to ensure

$$
\begin{equation*}
\frac{V_{\text {out }}}{V_{\text {in }}} \geq 0.9 \tag{6.13}
\end{equation*}
$$

image_name:Figure 6.20
description:
[
name: R_ant, type: Resistor, value: 50Ω, ports: {N1: Vout, N2: GND}
name: R_on, type: Resistor, ports: {N1: Vout, N2: Vin}
name: Transmitter, type: Other, ports: {N1: Vin, N2: Antenna}
]
extrainfo:The circuit diagram represents a transmitter connected to an antenna through a switch modeled by an on-resistance (R_on). The antenna is modeled as a 50Ω resistor (R_ant). The goal is to minimize signal attenuation, ensuring Vout/Vin ≥ 0.9, which requires R_on ≤ 5.6Ω. The minimum required aspect ratio (W/L) for the switch is 1276, given the parameters VDD=1.8V, μnCox=100μA/V², and VTH=0.4V.

Figure 6.20 Signal degradation due to on-resistance of antenna switch.
and hence

$$
\begin{equation*}
R_{o n} \leq 5.6 \Omega \tag{6.14}
\end{equation*}
$$

Setting $V_{G S}$ to the maximum value, $V_{D D}$, we obtain from Eq. (6.12),

$$
\begin{equation*}
\frac{W}{L} \geq 1276 \tag{6.15}
\end{equation*}
$$

(Since wide transistors introduce substantial capacitance in the signal path, this choice of $W / L$ may still attenuate high-frequency signals.)

Exercise What $W / L$ is necessary if $V_{D D}$ drops to 1.2 V ?

Triode and Saturation Regions Equation (6.9) expresses the drain current in terms of the device terminal voltages, implying that the current begins to fall for $V_{D S}>V_{G S}-V_{T H}$. We say the device operates in the "triode region" (also called the "linear region") if $V_{D S}<V_{G S}-V_{T H}$ (the rising section of the parabola). We also use the term "deep triode region" for $V_{D S} \ll 2\left(V_{G S}-V_{T H}\right)$, where the transistor operates as a resistor.
image_name:Figure 6.21 Overall MOS characteristic
description:The graph is a plot of the drain current (I_D) versus the drain-source voltage (V_DS) for a MOSFET, illustrating the transition between the triode and saturation regions. The x-axis represents V_DS, the drain-source voltage, while the y-axis represents I_D, the drain current. The graph is plotted on a linear scale for both axes.

In the triode region, which is labeled on the left side of the graph, the drain current increases with an increase in V_DS. This region is characterized by a parabolic rise in the current as V_DS is less than V_GS - V_TH (gate-source voltage minus threshold voltage). The equation governing this region is shown as \( \frac{1}{2} \mu_n C_{ox} \frac{W}{L} (V_{GS} - V_{TH})^2 \), indicating the dependence of I_D on these parameters.

Once V_DS exceeds V_GS - V_TH, the device enters the saturation region, marked on the right side of the graph. Here, the drain current becomes constant, illustrating the saturation behavior of the MOSFET. This is because the channel experiences pinch-off, and further increases in V_DS do not significantly affect the current.

The graph is divided by a vertical dashed line at V_DS = V_GS - V_TH, clearly separating the triode region from the saturation region. The saturation region shows a flat line indicating that the current remains constant despite increases in V_DS.

Figure 6.21 Overall MOS characteristic.

In reality, the drain current reaches "saturation," that is, becomes constant for $V_{D S}>V_{G S}-V_{T H}$ (Fig. 6.21). To understand why, recall from Fig. 6.12 that the channel experiences pinch-off if $V_{D S}=V_{G S}-V_{T H}$. Thus, further increase in $V_{D S}$ simply shifts the pinch-off point slightly toward the drain. Also, recall that Eqs. (6.7) and (6.8) are valid only where channel charge exists. It follows that the integration in Eq. (6.8) must encompass only the channel, i.e., from $x=0$ to $x=L_{1}$ in Fig. 6.12(b), and be modified to

$$
\begin{align*}
\int_{x=0}^{x=L_{1}} I_{D} d x= & \int_{V(x)=0}^{V(x)=V_{G S}-V_{T H}} \mu_{n} C_{o x} W\left[V_{G S}\right. \\
& \left.-V(x)-V_{T H}\right] d V . \tag{6.16}
\end{align*}
$$

Note that the upper limits correspond to the channel pinch-off point. In particular, the integral on the right-hand side is evaluated up to $V_{G S}-V_{T H}$ rather than $V_{D S}$. Consequently,

$$
\begin{equation*}
I_{D}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L_{1}}\left(V_{G S}-V_{T H}\right)^{2}, \tag{6.17}
\end{equation*}
$$

a result independent of $V_{D S}$ and identical to $I_{D, \max }$ in Eq. (6.10) if we assume $L_{1} \approx L$. Called the "overdrive voltage," the quantity $V_{G S}-V_{T H}$ plays a key role in MOS circuits. MOSFETs are sometimes called "squarelaw" devices to emphasize the relationship between $I_{D}$ and the overdrive. For the sake of brevity, we hereafter denote $L_{1}$ with $L$.

The I-V characteristic of Fig. 6.21 resembles that of bipolar devices, with the triode and saturation regions in MOSFETs appearing similar to saturation and forward active regions in bipolar transistors, respectively. It is unfortunate that the term "saturation" refers to completely different regions in MOS and bipolar I-V characteristics.

We employ the conceptual illustration in Fig. 6.22 to determine the region of operation. Note that the gate-drain potential difference suits this purpose and we need not compute the gate-source and gate-drain voltages separately.

Did you know?

The explosive growth of MOS technology is attributed to two factors: the ability to shrink the dimensions of the MOS device ( $W, L$, tox, etc.) and the ability to integrate a greater number of MOS devices on a chip each year. The latter trend was predicted by one of Intel's founders, Gordon Moore, in 1965. He observed that the number of transistors per chip doubled every two years. Indeed, starting with 50 devices per chip in 1965, we now have reached tens of billions on memory chips and several billion on microprocessor chips. Can you think of any other product in human history that has grown so much so fast (except for Bill Gates' wealth)?
image_name:Moore's Law: transistor count per chip throughout the years.
description:The graph is a logarithmic plot illustrating Moore's Law, depicting the increase in microprocessor transistor count over the years. The x-axis represents the year, ranging from 1965 to 2015, marked in increments of 5 years. The y-axis represents the microprocessor transistor count, displayed on a logarithmic scale ranging from 10^1 to 10^10.

The graph shows an exponential growth trend, consistent with Moore's Law, which predicts the doubling of transistor count approximately every two years. Data points are plotted as circles, and a solid line connects them, highlighting the trend. The line continues as a dashed line beyond 2015, suggesting projected growth.

Key features include a steady upward trajectory, indicating rapid technological advancement. The graph starts with a transistor count of around 10 in 1965 and reaches nearly 10^9 by 2015, showcasing the significant increase in transistor density over time.

Overall, the graph effectively visualizes the exponential increase in transistor count per chip, affirming Moore's observation and prediction of technological growth in microprocessors.

Moore's Law: transistor count per chip throughout the years.
image_name:Figure 6.22 Illustration of triode and saturation regions
description:The graph in Figure 6.22 illustrates the behavior of a MOSFET in both the triode and saturation regions based on the gate-source voltage \( V_{GS} \) and the drain-source voltage \( V_{DS} \). This plot is a typical representation used to describe the current-voltage characteristics of a MOSFET.

Type of Graph and Function:
The graph is a current-voltage characteristic curve for a MOSFET, showing the relationship between the drain current \( I_D \) and the gate-source voltage \( V_{GS} \) minus the threshold voltage \( V_{TH} \), as well as the drain-source voltage \( V_{DS} \).

Axes Labels and Units:
- **Y-Axis:** Represents the drain current \( I_D \), typically measured in amperes (A).
- **X-Axis:** Represents \( V_{GS} - V_{TH} \) and \( V_{DS} \), typically measured in volts (V).
- The graph uses a linear scale for both axes.

Overall Behavior and Trends:
- **Triode Region:** At lower values of \( V_{DS} \), the MOSFET operates in the triode region. In this region, \( I_D \) increases linearly with \( V_{DS} \) for a given \( V_{GS} \) above \( V_{TH} \).
- **Saturation Region:** As \( V_{DS} \) increases, the MOSFET enters the saturation region, where \( I_D \) becomes relatively constant ("flat") despite further increases in \( V_{DS} \).

Key Features and Technical Details:
- The transition between the triode and saturation regions is marked by a dotted vertical line, indicating the boundary where the MOSFET switches from linear to saturation behavior.
- The equation \( \frac{1}{2} \mu_n C_{ox} \frac{W}{L} (V_{GS} - V_{TH})^2 \) is provided, representing the saturation current equation for a MOSFET, where \( \mu_n \) is the mobility of electrons, \( C_{ox} \) is the oxide capacitance per unit area, \( W \) is the width, and \( L \) is the length of the MOSFET.

Annotations and Specific Data Points:
- The graph includes annotations of MOSFET symbols with load connections, indicating different configurations and biasing conditions for the device.
- The regions are labeled explicitly as "Triode Region" and "Saturation Region," providing clear demarcation of operating modes.

This graph is essential for understanding how a MOSFET can function as a voltage-controlled current source, with its behavior in the saturation region being particularly important for analog circuit design.
image_name:MOSFET Circuit
description:
[
name: M1, type: NMOS, ports: {S: LOAD, D: d1, G: g1+}
name: M1, type: NMOS, ports: {S: LOAD, D: d1, G: g1>VTH}
name: M1, type: NMOS, ports: {S: LOAD, D: d1, G: g1-}
name: M1, type: NMOS, ports: {S: LOAD, D: d1, G: g1+}
]
extrainfo:The diagram illustrates the operation of NMOS transistors in different regions based on gate voltage. The transistors are shown in a configuration where the gate voltage varies around the threshold voltage, VTH, affecting the current flow through the device. The graph depicts the triode and saturation regions of MOSFET operation.

(a)
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1, G: g}
]
extrainfo:The circuit diagram illustrates an NMOS transistor (M1) operating in the saturation region. The gate is connected to node 'g', the drain to node 'd1', and the source to ground (GND). This configuration shows the NMOS acting as a current source.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1, G: g}
]
extrainfo:The diagram illustrates an NMOS transistor M1 operating in the saturation region. The gate is connected to node g, the drain is connected to node d1, and the source is grounded. This configuration is equivalent to a current source connected to node X and ground.

(b)

Figure 6.22 Illustration of triode and saturation regions based on the gate and drain voltages.

Exhibiting a "flat" current in the saturation region, a MOSFET can operate as a current source having a value given by Eq. (6.17). Furthermore, the square-law dependence of $I_{D}$ upon $V_{G S}-V_{T H}$ suggests that the device can act as a voltage-controlled current source.

Example Calculate the bias current of $M_{1}$ in Fig. 6.23. Assume $\mu_{n} C_{o x}=100 \mu \mathrm{~A} / \mathrm{V}^{2}$ and $V_{T H}=$ 6.6 0.4 V . If the gate voltage increases by 10 mV , what is the change in the drain voltage?
image_name:Figure 6.23 Simple MOS circuit
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: g1}
name: RD, type: Resistor, value: 5k, ports: {N1: VDD, N2: X}
name: VDD, type: VoltageSource, value: 1.8V, ports: {Np: VDD, Nn: GND}
name: V1, type: VoltageSource, value: 1V, ports: {Np: g1, Nn: GND}
]
extrainfo:The circuit is a simple NMOS biasing circuit with a resistor RD connected to VDD. The NMOS transistor M1 is connected to ground, with its gate connected to a 1V voltage source. The drain of M1 is connected to node X, which is also connected to RD. The circuit is used to demonstrate the operation of an NMOS in saturation with given parameters.

Figure 6.23 Simple MOS circuit.

Solution It is unclear a priori in which region $M_{1}$ operates. Let us assume $M_{1}$ is saturated and proceed. Since $V_{G S}=1 \mathrm{~V}$,

$$
\begin{align*}
I_{D} & =\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2}  \tag{6.18}\\
& =200 \mu \mathrm{~A} . \tag{6.19}
\end{align*}
$$

We must check our assumption by calculating the drain potential:

$$
\begin{align*}
V_{X} & =V_{D D}-R_{D} I_{D}  \tag{6.20}\\
& =0.8 \mathrm{~V} \tag{6.21}
\end{align*}
$$

The drain voltage is lower than the gate voltage, but by less than $V_{T H}$. The illustration in Fig. 6.22 therefore indicates that $M_{1}$ indeed operates in saturation.

If the gate voltage increases to 1.01 V , then

$$
\begin{equation*}
I_{D}=206.7 \mu \mathrm{~A} \tag{6.22}
\end{equation*}
$$

lowering $V_{X}$ to

$$
\begin{equation*}
V_{X}=0.766 \mathrm{~V} \tag{6.23}
\end{equation*}
$$

Fortunately, $M_{1}$ is still saturated. The $34-\mathrm{mV}$ change in $V_{X}$ reveals that the circuit can amplify the input.

Exercise What choice of $R_{D}$ places the transistor at the edge of the triode region?

It is instructive to identify several points of contrast between bipolar and MOS devices. (1) A bipolar transistor with $V_{B E}=V_{C E}$ resides at the edge of the active region whereas a MOSFET approaches the edge of saturation if its drain voltage falls below its gate voltage by $V_{T H}$. (2) Bipolar devices exhibit an exponential $I_{C}-V_{B E}$ characteristic while MOSFETs display a square-law dependence. That is, the former provide a greater transconductance than the latter (for a given bias current). (3) In bipolar circuits, most transistors have the same dimensions and hence the same $I_{S}$, whereas in MOS circuits, the aspect ratio of each device may be chosen differently to satisfy the design requirements. (4) The gate of MOSFETs draws no bias current. ${ }^{9}$

Example Determine the value of $W / L$ in Fig. 6.23 that places $M_{1}$ at the edge of saturation and calculate the drain voltage change for a 1-mV change at the gate. Assume $V_{T H}=0.4 \mathrm{~V}$.

Solution With $V_{G S}=+1 \mathrm{~V}$, the drain voltage must fall to $V_{G S}-V_{T H}=0.6 \mathrm{~V}$ for $M_{1}$ to enter the triode region. That is,

$$
\begin{align*}
I_{D} & =\frac{V_{D D}-V_{D S}}{R_{D}}  \tag{6.24}\\
& =240 \mu \mathrm{~A} . \tag{6.25}
\end{align*}
$$

Since $I_{D}$ scales linearly with $W / L$,

$$
\begin{align*}
\left.\frac{W}{L}\right|_{\max } & =\frac{240 \mu \mathrm{~A}}{200 \mu \mathrm{~A}} \cdot \frac{2}{0.18}  \tag{6.26}\\
& =\frac{2.4}{0.18} \tag{6.27}
\end{align*}
$$

If $V_{G S}$ increases by 1 mV ,

$$
\begin{equation*}
I_{D}=248.04 \mu \mathrm{~A} \tag{6.28}
\end{equation*}
$$

changing $V_{X}$ by

$$
\begin{align*}
\Delta V_{X} & =\Delta I_{D} \cdot R_{D}  \tag{6.29}\\
& =4.02 \mathrm{mV} \tag{6.30}
\end{align*}
$$

The voltage gain is thus equal to 4.02 in this case.

Exercise Repeat the above example if $R_{D}$ is doubled.

[^13]Example
6.8

Calculate the maximum allowable gate voltage in Fig. 6.24 if $M_{1}$ must remain saturated.
image_name:Figure 6.24 Simple MOS circuit
description:
[
name: M1, type: NMOS, ports: {S: GND, D: X, G: VGS}
name: RD, type: Resistor, value: 5k, ports: {N1: VDD, N2: X}
name: VDD, type: VoltageSource, value: 1.8V, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a simple NMOS amplifier with a resistor RD connected between VDD and the drain of the NMOS. The source of the NMOS is connected to GND, and the gate is controlled by VGS. The voltage across RD is used to determine the drain current ID.

Figure 6.24 Simple MOS circuit.

Solution At the edge of saturation, $V_{G S}-V_{T H}=V_{D S}=V_{D D}-R_{D} I_{D}$. Substituting for $I_{D}$ from Eq. (6.17) gives

$$
\begin{equation*}
V_{G S}-V_{T H}=V_{D D}-\frac{R_{D}}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2}, \tag{6.31}
\end{equation*}
$$

and hence

$$
\begin{equation*}
V_{G S}-V_{T H}=\frac{-1+\sqrt{1+2 R_{D} V_{D D} \mu_{n} C_{o x} \frac{W}{L}}}{R_{D} \mu_{n} C_{o x} \frac{W}{L}} \tag{6.32}
\end{equation*}
$$

Thus,

$$
\begin{equation*}
V_{G S}=\frac{-1+\sqrt{1+2 R_{D} V_{D D} \mu_{n} C_{o x} \frac{W}{L}}}{R_{D} \mu_{n} C_{o x} \frac{W}{L}}+V_{T H} \tag{6.33}
\end{equation*}
$$

Exercise Calculate the value of $V_{G S}$ if $\mu_{n} C_{o x}=100 \mu \mathrm{~A} / \mathrm{V}^{2}$ and $V_{T H}=0.4$.

### 6.2.3 Channel-Length Modulation

In our study of the pinch-off effect, we observed that the point at which the channel vanishes in fact moves toward the source as the drain voltage increases. In other words, the value of $L_{1}$ in Fig. 6.12(b) varies with $V_{D S}$ to some extent. Called "channel-length modulation" and illustrated in Fig. 6.25, this phenomenon yields a larger drain current as $V_{D S}$ increases because $I_{D} \propto 1 / L_{1}$ in Eq. (6.17). Similar to the Early effect in bipolar devices,
image_name:Figure 6.25
description:Figure 6.25 illustrates the behavior of the drain current, \(I_D\), in the saturation region of a MOSFET, with respect to the drain-source voltage, \(V_{DS}\). The graph is a plot of \(I_D\) on the vertical axis versus \(V_{DS}\) on the horizontal axis. The graph is a linear plot, where the vertical axis represents the drain current \(I_D\), and the horizontal axis represents the drain-source voltage \(V_{DS}\).

The graph shows an initially steep rise in \(I_D\) as \(V_{DS}\) increases, indicating the onset of saturation. After reaching a certain threshold, the curve flattens slightly, showing that \(I_D\) continues to increase but at a slower rate. This behavior is due to channel-length modulation, which is analogous to the Early effect in bipolar junction transistors. The equation provided, \(I_{D}=\frac{1}{2} \mu_{n} C_{ox} \frac{W}{L}(V_{GS}-V_{TH})^{2}(1+\lambda V_{DS})\), suggests that \(I_D\) is proportional to \(1/L_1\), where \(L_1\) is the effective channel length, and \(\lambda\) is the channel-length modulation parameter.

The graph includes a dotted horizontal reference line representing a constant value of \(I_D\) without channel-length modulation. The solid curve above this line represents the actual \(I_D\) with channel-length modulation, illustrating the increase in \(I_D\) due to the modulation effect. The point where the curve begins to deviate from the horizontal reference line marks the influence of \(\lambda V_{DS}\) on \(I_D\).

Key features include the threshold voltage \(V_{GS} - V_{TH}\), where the curve begins, and the gradual increase of \(I_D\) as \(V_{DS}\) increases, indicating the finite output impedance due to channel-length modulation.

Figure 6.25 Variation of $I_{D}$ in saturation region.
channel-length modulation results in a finite output impedance given by the inverse of the $I_{D}-V_{D S}$ slope in Fig. 6.25.

To account for channel-length modulation, we assume $L$ is constant, but multiply the right-hand side of Eq. (6.17) by a corrective term:

$$
\begin{equation*}
I_{D}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2}\left(1+\lambda V_{D S}\right), \tag{6.34}
\end{equation*}
$$

where $\lambda$ is called the "channel-length modulation coefficient." While only an approximation, this linear dependence of $I_{D}$ upon $V_{D S}$ still provides a great deal of insight into the circuit design implications of channel-length modulation.

Unlike the Early effect in bipolar devices (Chapter 4), the amount of channel-length modulation is under the circuit designer's control. This is because $\lambda$ is inversely proportional to $L$ : for a longer channel, the relative change in $L$ (and hence in $I_{D}$ ) for a given change in $V_{D S}$ is smaller (Fig. 6.26). ${ }^{10}$ (By contrast, the base width of bipolar devices cannot be adjusted by the circuit designer, yielding a constant Early voltage for all transistors in a given technology.)
image_name:L1
description:The image depicts two diagrams illustrating the concept of channel-length modulation in MOSFETs, labeled as "L1" and "L2." Each diagram consists of two main parts: a cross-sectional view of a MOSFET and a corresponding graph of drain current (I_D) versus drain-source voltage (V_DS).

1. **Identification of Components and Structure:**
- **Cross-sectional Views:**
- Both diagrams show a simplified cross-sectional view of a MOSFET. The MOSFET is represented with a source and drain region, separated by a channel of length L (L1 or L2). A gate is positioned above the channel.
- The channel length is indicated by arrows labeled L1 and L2, showing the distance between the source and drain regions.

2. **Connections and Interactions:**
- **Channel-Length Modulation:**
- The diagrams illustrate how the effective channel length changes with different conditions, affecting the drain current (I_D).
- The change in channel length is represented by the angled lines in the cross-sections, suggesting the modulation effect.

3. **Labels, Annotations, and Key Features:**
- **Graphs of I_D vs. V_DS:**
- Below each cross-sectional view is a graph plotting I_D (on the vertical axis) against V_DS (on the horizontal axis).
- The solid lines in the graphs represent the actual I_D versus V_DS characteristics, while the dashed lines indicate the ideal characteristic without channel-length modulation.
- The left diagram with L1 shows a more pronounced modulation effect compared to the right diagram with L2, demonstrating how a longer channel reduces the modulation effect.

Overall, the diagrams illustrate the impact of channel-length modulation on the performance of MOSFETs, highlighting how longer channel lengths (L2) lead to reduced modulation effects, resulting in more stable I_D characteristics.
image_name:L2
description:The graph in Figure 6.26 illustrates the concept of channel-length modulation in MOSFETs, showing two different scenarios with channel lengths \( L_1 \) and \( L_2 \). The graph plots the drain current \( I_D \) on the vertical axis against the drain-source voltage \( V_{DS} \) on the horizontal axis.

1. **Type of Graph and Function:**
- This is a characteristic curve graph typically used in electronics to show the relationship between current and voltage in a transistor.

2. **Axes Labels and Units:**
- The vertical axis is labeled \( I_D \) representing the drain current, typically measured in amperes.
- The horizontal axis is labeled \( V_{DS} \) representing the drain-source voltage, typically measured in volts.
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- For both channel lengths \( L_1 \) and \( L_2 \), the drain current \( I_D \) initially increases sharply with \( V_{DS} \) and then starts to level off, indicating saturation.
- The solid line represents the actual behavior, while the dashed line indicates the ideal behavior without channel-length modulation.
- The graph for \( L_1 \) shows a more pronounced increase in \( I_D \) with \( V_{DS} \) in the saturation region compared to \( L_2 \), reflecting greater channel-length modulation.

4. **Key Features and Technical Details:**
- The difference in slope in the saturation region between \( L_1 \) and \( L_2 \) highlights the impact of channel-length modulation, which is more significant for shorter channel lengths (\( L_1 \)).
- The dashed line represents the ideal case where channel-length modulation does not occur, showing a flat saturation region.

5. **Annotations and Specific Data Points:**
- The diagrams above the graphs illustrate the physical representation of the channel lengths \( L_1 \) and \( L_2 \), with \( L_1 \) being shorter than \( L_2 \).
- No specific numerical values are provided, but the general trend indicates that the longer channel \( L_2 \) has less channel-length modulation effect, maintaining a more constant \( I_D \) in the saturation region.

Figure 6.26 Channel-length modulation.

Example
6.9

Solution We write

$$
\begin{align*}
& I_{D 1}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2}\left(1+\lambda V_{D S 1}\right)  \tag{6.35}\\
& I_{D 2}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2}\left(1+\lambda V_{D S 2}\right) \tag{6.36}
\end{align*}
$$

and hence

$$
\begin{equation*}
I_{D 2}=I_{D 1} \frac{1+\lambda V_{D S 2}}{1+\lambda V_{D S 1}} \tag{6.37}
\end{equation*}
$$

With $I_{D 1}=1 \mathrm{~mA}, V_{D S 1}=0.5 \mathrm{~V}, V_{D S 2}=1 \mathrm{~V}$, and $\lambda=0.1 \mathrm{~V}^{-1}$,

$$
\begin{equation*}
I_{D 2}=1.048 \mathrm{~mA} \tag{6.38}
\end{equation*}
$$

[^14]The change in $I_{D}$ is therefore equal to $48 \mu \mathrm{~A}$, yielding an output impedance of

$$
\begin{align*}
r_{O} & =\frac{\Delta V_{D S}}{\Delta I_{D}}  \tag{6.39}\\
& =10.42 \mathrm{k} \Omega \tag{6.40}
\end{align*}
$$

Exercise Does $W$ affect the above results?

The above example reveals that channel-length modulation limits the output impedance of MOS current sources. The same effect was observed for bipolar current sources in Chapters 4 and 5.

Assuming $\lambda \propto 1 / L$, calculate $\Delta I_{D}$ and $r_{O}$ in Example 6.9 if both $W$ and $L$ are doubled.

Solution In Eqs. (6.35) and (6.36), $W / L$ remains unchanged but $\lambda$ drops to $0.05 \mathrm{~V}^{-1}$. Thus,

$$
\begin{align*}
I_{D 2} & =I_{D 1} \frac{1+\lambda V_{D S 2}}{1+\lambda V_{D S 1}}  \tag{6.41}\\
& =1.024 \mathrm{~mA} . \tag{6.42}
\end{align*}
$$

That is, $\Delta I_{D}=24 \mu \mathrm{~A}$ and

$$
\begin{equation*}
r_{O}=20.84 \mathrm{k} \Omega . \tag{6.43}
\end{equation*}
$$

Exercise What output impedance is achieved if $W$ and $L$ are quadrupled and $I_{D}$ is halved?

### 6.2.4 MOS Transconductance

As a voltage-controlled current source, a MOS transistor can be characterized by its transconductance:

$$
\begin{equation*}
g_{m}=\frac{\partial I_{D}}{\partial V_{G S}} . \tag{6.44}
\end{equation*}
$$

This quantity serves as a measure of the "strength" of the device: a higher value corresponds to a greater change in the drain current for a given change in $V_{G S}$. Using Eq. (6.17) for the saturation region, we have

$$
\begin{equation*}
g_{m}=\mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right), \tag{6.45}
\end{equation*}
$$

concluding that (1) $g_{m}$ is linearly proportional to $W / L$ for a given $V_{G S}-V_{T H}$, and (2) $g_{m}$ is linearly proportional to $V_{G S}-V_{T H}$ for a given $W / L$. Also, substituting for $V_{G S}-V_{T H}$ from Eq. (6.17), we obtain

$$
\begin{equation*}
g_{m}=\sqrt{2 \mu_{n} C_{o x} \frac{W}{L} I_{D}} \tag{6.46}
\end{equation*}
$$

[^0]:    ${ }^{8} \mathrm{~A}$ common mistake here is to make the impedance of $C_{1}$ much less than $R_{E}$.

[^1]:    ${ }^{9}$ Note that the topologies of Figs. 5.60 and 5.61(a) are identical even though $Q_{1}$ is drawn differently.

[^2]:    ${ }^{10}$ This example serves only as an illustration of the CB stage. A CE stage may prove more suited to sensing a thermometer voltage.

[^3]:    ${ }^{11}$ If the input impedance of each stage is not matched to the characteristic impedance of the preceding transmission line, then "reflections" occur, corrupting the signal or at least creating dependence on the length of the lines.

[^4]:    ${ }^{12}$ The dots denote the need for biasing circuitry, as described later in this section.

[^5]:    ${ }^{13}$ Alternatively, the current through $r_{\pi}+R_{B}$ is equal to $v_{X} /\left(r_{\pi}+R_{B}\right)$, yielding a voltage of $-r_{\pi} v_{X} /\left(r_{\pi}+R_{B}\right)$ across $r_{\pi}$.

[^6]:    ${ }^{14}$ In the extreme case, $R_{E}=0$ (Example 5.41) and $i_{2}=0$.

[^7]:    ${ }^{15}$ In an extreme case described in Example 5.43, the gain becomes equal to unity.

[^8]:    ${ }^{1}$ The capacitance between two plates is given by $\epsilon A / t$, where $\epsilon$ is the "dielectric constant" (also called the "permitivity"), $A$ is the area of each plate, and $t$ is the dielectric thickness.
${ }^{2}$ Used to distinguish it from other types of contacts such as diodes, the term "ohmic" contact emphasizes bi-directional current flow-as in a resistor.

[^9]:    ${ }^{3}$ The substrate acts as a fourth terminal, but we ignore that for now.
${ }^{4}$ Note that this depletion region contains only one immobile charge polarity, whereas the depletion region in a pn junction consists of two areas of negative and positive ions on the two sides of the junction.

[^10]:    ${ }^{5}$ The term "on-resistance" always refers to that between the source and drain, as no resistance exists between the gate and other terminals.

[^11]:    ${ }^{7}$ Recall that the resistance of a conductor is inversely proportional to the cross section area, which itself is equal to the product of the width and thickness of the conductor.

[^12]:    ${ }^{8}$ Some cellphones operate in the same manner.

[^13]:    ${ }^{9}$ New generations of MOSFETs suffer from gate "leakage" current, but we neglect this effect here.

[^14]:    ${ }^{10}$ Since different MOSFETs in a circuit may be sized for different $\lambda$ 's, we do not define a quantity similar to the Early voltage here.

TABLE 6.1 Various dependencies of $g_{m}$.

| $\begin{gathered} \frac{W}{L} \text { Constant } \\ V_{G S}-V_{T H} \text { Variable } \end{gathered}$ | $\begin{gathered} \frac{W}{L} \text { Variable } \\ V_{G S}-V_{T H} \text { Constant } \end{gathered}$ | $\begin{gathered} \frac{W}{L} \text { Variable } \\ V_{G S}-V_{T H} \text { Constant } \end{gathered}$ |
| :---: | :---: | :---: |
| $g_{\mathrm{m}} \propto \sqrt{I_{D}}$ | $g_{\mathrm{m}} \propto I_{D}$ | $g_{\mathrm{m}} \propto \sqrt{\frac{W}{L}}$ |
| $g_{\mathrm{m}} \propto V_{G S}-V_{T H}$ | $g_{\mathrm{m}} \propto \frac{W}{L}$ | $g_{\mathrm{m}} \propto \frac{1}{V_{G S}-V_{T H}}$ |

That is, (1) $g_{m}$ is proportional to $\sqrt{W / L}$ for a given $I_{D}$, and (2) $g_{m}$ is proportional to $\sqrt{I_{D}}$ for a given $W / L$. Moreover, dividing Eq. (6.45) by (6.17) gives

$$
\begin{equation*}
g_{m}=\frac{2 I_{D}}{V_{G S}-V_{T H}} \tag{6.47}
\end{equation*}
$$

revealing that (1) $g_{m}$ is linearly proportional to $I_{D}$ for a given $V_{G S}-V_{T H}$, and (2) $g_{m}$ is inversely proportional to $V_{G S}-V_{T H}$ for a given $I_{D}$. Summarized in Table 6.1, these dependencies prove critical in understanding performance trends of MOS devices and have no counterpart in bipolar transistors. ${ }^{11}$ Among these three expressions for $g_{m}$, Eq. (6.46) is more frequently used because $I_{D}$ may be predetermined by power dissipation requirements.

Example
6.11

For a MOSFET operating in saturation, how do $g_{m}$ and $V_{G S}-V_{T H}$ change if both $W / L$ and $I_{D}$ are doubled?

Solution Equation (6.46) indicates that $g_{m}$ is also doubled. Moreover, Eq. (6.17) suggests that the overdrive remains constant. These results can be understood intuitively if we view the doubling of $W / L$ and $I_{D}$ as shown in Fig. 6.27. Indeed, if $V_{G S}$ remains constant and the width of the device is doubled, it is as if two transistors carrying equal currents are placed in parallel, thereby doubling the transconductance. The reader can show that this trend applies to any type of transistor.
image_name:Figure 6.27 Equivalence of a wide MOSFET to two in parallel
description:The image illustrates the concept of equating a wide MOSFET to two transistors in parallel. On the left side, a single wide MOSFET is depicted. It is shown with a gate-source voltage ($V_{GS}$) applied across the gate and source terminals, and a drain-source voltage ($V_{DS}$) applied across the drain and source terminals. The MOSFET is represented with its gate, source, and drain terminals, and the flow of current is indicated by arrows.

On the right side, this wide MOSFET is conceptually split into two narrower MOSFETs placed in parallel. Each of these transistors has the same $V_{GS}$ and $V_{DS}$ applied as the original single wide MOSFET. The parallel arrangement effectively doubles the width of the channel, which in turn doubles the current-carrying capability and transconductance ($g_{m}$) of the device, as described in the context. The diagram visually demonstrates how doubling the width ($W$) of a MOSFET is equivalent to having two identical MOSFETs in parallel, thus maintaining the same overdrive voltage while increasing the transconductance.

Figure 6.27 Equivalence of a wide MOSFET to two in parallel.

Exercise
How do $g_{m}$ and $V_{G S}-V_{T H}$ change if only $W$ and $I_{D}$ are doubled?

[^0]
### 6.2.5 Velocity Saturation*

Recall from Section 2.1.3 that at high electric fields, carrier mobility degrades, eventually leading to a constant velocity. Owing to their very short channels (e.g., $0.1 \mu \mathrm{~m}$ ), modern MOS devices experience velocity saturation even with drain-source voltages as low as 1 V . As a result, the I/V characteristics no longer follow the square-law behavior.

Let us examine the derivations in Section 6.2.2 under velocity saturation conditions. Denoting the saturated velocity by $v_{s a t}$, we have

$$
\begin{align*}
I_{D} & =v_{s a t} \cdot Q  \tag{6.48}\\
& =v_{s a t} \cdot W C_{o x}\left(V_{G S}-V_{T H}\right) \tag{6.49}
\end{align*}
$$

Interestingly, $I_{D}$ now exhibits a linear dependence on $V_{G S}-V_{T H}$ and no dependence on L. ${ }^{12} \mathrm{We}$ also recognize that

$$
\begin{align*}
g_{m} & =\frac{\partial I_{D}}{\partial V_{G S}}  \tag{6.50}\\
& =v_{s a t} W C_{o x}, \tag{6.51}
\end{align*}
$$

a quantity independent of $L$ and $I_{D}$.

### 6.2.6 Other Second-Order Effects

Body Effect In our study of MOSFETs, we have assumed that both the source and the substrate (also called the "bulk" or the "body") are tied to ground. However, this condition need not hold in all circuits. For example, if the source terminal rises to a positive voltage while the substrate is at zero, then the source-substrate junction remains reverse-biased and the device still operates properly.

Figure 6.28 illustrates this case. The source terminal is tied to a potential $V_{S}$ with respect to ground while the substrate is grounded through a $p^{+}$contact. ${ }^{13}$ The dashed line added to the transistor symbol indicates the substrate terminal. We denote the voltage difference between the source and the substrate (the bulk) by $V_{S B}$.
image_name:Figure 6.28 Body effect
description:
[
name: V_S, type: VoltageSource, value: V_S, ports: {Np: V_S, Nn: GND}
name: V_G, type: VoltageSource, value: V_G, ports: {Np: V_G, Nn: GND}
name: V_D, type: VoltageSource, value: V_D, ports: {Np: V_D, Nn: GND}
name: NMOS, type: NMOS, ports: {S: V_S, D: V_D, G: V_G}
]
extrainfo:The circuit illustrates the body effect in an NMOS transistor, where the source is connected to a positive voltage V_S, the gate to V_G, and the drain to V_D. The substrate is grounded, creating a reverse-bias condition for the source-substrate junction.

Figure 6.28 Body effect.

[^1]An interesting phenomenon occurs as the source-substrate potential difference departs from zero: the threshold voltage of the device changes. In particular, as the source becomes more positive with respect to the substrate, $V_{T H}$ increases. Called "body effect," this phenomenon is formulated as

$$
\begin{equation*}
V_{T H}=V_{T H 0}+\gamma\left(\sqrt{\left|2 \phi_{F}+V_{S B}\right|}-\sqrt{\left|2 \phi_{F}\right|}\right), \tag{6.52}
\end{equation*}
$$

where $V_{T H 0}$ denotes the threshold voltage with $V_{S B}=0$ (as studied earlier), and $\gamma$ and $\phi_{F}$ are technology-dependent parameters having typical values of $0.4 \sqrt{\mathrm{~V}}$ and 0.4 V , respectively.
image_name:Fig. 6.28
description:The image appears to be an excerpt from Example 6.12, which describes a circuit as shown in Fig. 6.28. The given parameters for the circuit are as follows: \( V_S = 0.5 \, V \), \( V_G = V_D = 1.4 \, V \), \( \mu_n C_{ox} = 100 \, \mu A/V^2 \), \( W/L = 50 \), and \( V_{TH0} = 0.6 \, V \). The task is to determine the drain current \( I_D \) when the channel length modulation parameter \( \lambda = 0 \). This setup is used to calculate the drain current using the provided equations and parameters, likely in the context of a MOSFET operating in saturation.

6.12 $W / L=50$, and $V_{T H 0}=0.6 \mathrm{~V}$. Determine the drain current if $\lambda=0$.

Solution Since the source-body voltage, $V_{S B}=0.5 \mathrm{~V}$, Eq. (6.52) and the typical values for $\gamma$ and $\phi_{F}$ yield

$$
\begin{equation*}
V_{T H}=0.698 \mathrm{~V} \tag{6.53}
\end{equation*}
$$

Also, with $V_{G}=V_{D}$, the device operates in saturation (why?) and hence

$$
\begin{align*}
I_{D} & =\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G}-V_{S}-V_{T H}\right)^{2}  \tag{6.54}\\
& =102 \mu \mathrm{~A} . \tag{6.55}
\end{align*}
$$

Exercise Sketch the drain current as a function of $V_{S}$ as $V_{S}$ goes from zero to 1 V .

Body effect manifests itself in some analog and digital circuits and is studied in more advanced texts. We neglect body effect in this book.

Subthreshold Conduction The derivation of the MOS I-V characteristic has assumed that the transistor abruptly turns on as $V_{G S}$ reaches $V_{T H}$. In reality, formation of the channel is a gradual effect, and the device conducts a small current even for $V_{G S}<V_{T H}$. Called "subthreshold conduction," this effect has become a critical issue in modern MOS devices and is studied in more advanced texts.

## 6.3 MOS DEVICE MODELS

With our study of MOS I-V characteristics in the previous section, we now develop models that can be used in circuit analysis and design.

### 6.3.1 Large-Signal Model

For arbitrary voltage and current levels, we must resort to Eqs. (6.9) and (6.34) to express the device behavior:

$$
\begin{align*}
I_{D} & =\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left[2\left(V_{G S}-V_{T H}\right) V_{D S}-V_{D S}^{2}\right] \text { Triode Region }  \tag{6.56}\\
I_{D} & =\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2}\left(1+\lambda V_{D S}\right) \text { Saturation Region } \tag{6.57}
\end{align*}
$$

image_name:(a)
description:
[
name: ID, type: CurrentSource, ports: {Np: S, Nn: D}
]
extrainfo:The circuit diagram (a) represents the large-signal model of an NMOS transistor in the saturation region. The current source ID is controlled by the gate-source voltage VGS and the drain-source voltage VDS, as described by the equation: ID = 0.5 * μn * Cox * (W/L) * (VGS - VTH)^2 * (1 + λ * VDS).
image_name:(b)
description:
[
name: ID, type: CurrentSource, ports: {Np: D, Nn: S}
name: Ron, type: Resistor, ports: {N1: D, N2: S}
]
extrainfo:The diagram shows a MOSFET in the triode region with a voltage-controlled current source and a resistor representing on-resistance. It models the behavior when V_GS > V_TH and V_DS < V_GS - V_TH.
image_name:(c)
description:
[
name: ID, type: CurrentSource, ports: {Np: D, Nn: S}
name: Ron, type: Resistor, ports: {N1: D, N2: S}
]
extrainfo:The circuit diagram represents a MOSFET in the deep triode region, where the device behaves as a resistor Ron between the drain (D) and source (S) terminals. The gate (G) controls the channel, but the main conduction is between D and S with a resistance Ron.

Figure 6.29 MOS models for (a) saturation region, (b) triode region, (c) deep triode region.

In the saturation region, the transistor acts as a voltage-controlled current source, lending itself to the model shown in Fig. 6.29(a). Note that $I_{D}$ does depend on $V_{D S}$ and is therefore not an ideal current source. For $V_{D S}<V_{G S}-V_{T H}$, the model must reflect the triode region, but it can still incorporate a voltage-controlled current source, as depicted in Fig. 6.29(b). Finally, if $V_{D S} \ll 2\left(V_{G S}-V_{T H}\right)$, the transistor can be viewed as a voltage-controlled resistor [Fig. 6.29(c)]. In all three cases, the gate remains an open circuit to represent the zero gate current.

Example Sketch the drain current of $M_{1}$ in Fig. 6.30(a) versus $V_{1}$ as $V_{1}$ varies from zero to $V_{D D}$. Assume $\lambda=0$.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vi, G: VDD}
name: V1, type: VoltageSource, value: V1, ports: {Np: Vi, Nn: GND}
]
extrainfo:The circuit consists of an NMOS transistor M1 and a voltage source V1. The drain of M1 is connected to the node Vi, which is also the positive terminal of the voltage source V1. The source of M1 is connected to ground, and the gate is connected to VDD. The circuit likely operates in the saturation region.

(a)
image_name:(b)
description:The graph is a plot showing the variation of the drain current, $I_D$, with respect to the voltage $V_1$. This is a typical characteristic curve for an NMOS transistor operating in the saturation region.

1. **Type of Graph and Function**: This is a current-voltage characteristic graph for an NMOS transistor.

2. **Axes Labels and Units**: The vertical axis represents the drain current $I_D$, and the horizontal axis represents the voltage $V_1$. The scales appear to be linear, though specific units are not provided.

3. **Overall Behavior and Trends**: The graph shows a decreasing trend of $I_D$ as $V_1$ increases. Initially, when $V_1$ is zero, $I_D$ is at its maximum value. As $V_1$ increases towards $V_{DD} - V_{TH}$, $I_D$ decreases, indicating that the NMOS transistor is operating in the saturation region. Beyond the point where $V_1 = V_{DD} - V_{TH}$, the drain current $I_D$ approaches zero.

4. **Key Features and Technical Details**: The curve starts at a maximum value of $I_D$ when $V_1 = 0$. As $V_1$ increases, the curve slopes downward, reflecting the decrease in $I_D$. The point $V_{DD} - V_{TH}$ is marked on the horizontal axis, indicating the threshold voltage level where $I_D$ becomes very small.

5. **Annotations and Specific Data Points**: The graph does not have additional annotations or specific numerical data points, but the critical point $V_{DD} - V_{TH}$ is highlighted, showing where the current effectively diminishes.

(b)

Figure 6.30 (a) Simple MOS circuit, (b) variation of $I_{D}$ with $V_{1}$.

Solution Noting that the device operates in saturation (why?), we write

$$
\begin{align*}
I_{D} & =\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2}  \tag{6.58}\\
& =\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{D D}-V_{1}-V_{T H}\right)^{2} . \tag{6.59}
\end{align*}
$$

At $V_{1}=0, V_{G S}=V_{D D}$ and the device carries maximum current. As $V_{1}$ rises, $V_{G S}$ falls and so does $I_{D}$. If $V_{1}$ reaches $V_{D D}-V_{T H}, V_{G S}$ drops to $V_{T H}$, turning the transistor off. The drain current thus varies as illustrated in Fig. 6.30(b). Note that, owing to body effect, $V_{T H}$ varies with $V_{1}$ if the substrate is tied to ground.

Exercise Repeat the above example if the gate of $M_{1}$ is tied to a voltage equal to 1.5 V and $V_{D D}=2 \mathrm{~V}$.

### 6.3.2 Small-Signal Model

If the bias currents and voltages of a MOSFET are only slightly disturbed by signals, the nonlinear, large-signal models can be reduced to linear, small-signal representations. The development of the model proceeds in a manner similar to that in Chapter 4 for bipolar devices. Of particular interest to us in this book is the small-signal model for the saturation region.

Viewing the transistor as a voltagecontrolled current source, we draw the basic model as in Fig. 6.31(a), where $i_{D}=g_{m} v_{G S}$ and the gate remains open. To represent channel-length modulation, i.e., variation of $i_{D}$ with $v_{D S}$, we add a resistor as in Fig. 6.31(b):

$$
\begin{align*}
r_{O} & =\left(\frac{\partial I_{D}}{\partial V_{D S}}\right)^{-1}  \tag{6.60}\\
& =\frac{1}{\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2} \cdot \lambda} \tag{6.61}
\end{align*}
$$

Since channel-length modulation is relatively small, the denominator of Eq. (6.61) can be approximated as $I_{D} \cdot \lambda$, yielding

Did you know?

In addition to integrating a larger number of transistors per chip, MOS technology has also benefited tremendously from "scaling," i.e., the reduction of the transistors' dimensions. The minimum channel length has fallen from about $10 \mu \mathrm{~m}$ to about 25 nm today and the speed of MOSFETs has improved by more than 4 orders of magnitude. For example, the clock frequency of Intel's microprocessors has risen from 100 kHz to 4 GHz . But have analog circuits taken advantage of the scaling as well? Yes, indeed. Plotted below is the frequency of MOS oscillators as a function of time over the past three decades.
image_name:MOS oscillator frequency as a function of time
description:The graph is a semi-logarithmic plot depicting the oscillation frequency of MOS oscillators as a function of time over the past three decades. The x-axis represents the year, ranging from 1988 to 2010, marked at intervals of two years. The y-axis represents the oscillation frequency in gigahertz (GHz) on a logarithmic scale, ranging from 1 GHz to 1000 GHz.

The graph shows a clear upward trend, indicating that the oscillation frequency of MOS oscillators has increased significantly over time. This trend is approximately linear on the logarithmic scale, suggesting an exponential growth in frequency as time progresses.

Key data points are represented by circles, showing the frequency at specific years. These points align closely with a straight line, which has been drawn to represent the general trend. The graph indicates a smooth and consistent increase in frequency, with no apparent peaks or valleys.

The significant increase in frequency over the decades highlights the advancements in MOS technology, particularly in terms of scaling and performance improvements.

MOS oscillator frequency as a function of time.

$$
\begin{equation*}
r_{O} \approx \frac{1}{\lambda I_{D}} \tag{6.62}
\end{equation*}
$$

image_name:(a)
description:
[
name: gmVgs, type: VoltageControlledCurrentSource, ports: {Np: S, Nn: D}
]
extrainfo:The diagram shows a small-signal model of a MOSFET with a voltage-controlled current source (gmVgs) representing the transconductance. The gate (G), source (S), and drain (D) nodes are labeled, and the current source is controlled by the voltage Vgs across the gate and source.

(a)
image_name:(a)
description:
[
name: v_GS, type: VoltageSource, value: v_GS, ports: {Np: G, Nn: S}
name: g_m v_GS, type: CurrentSource, value: g_m v_GS, ports: {Np: S, Nn: D}
name: r_O, type: Resistor, value: r_O, ports: {N1: D, N2: S}
]
extrainfo:The circuit represents a small-signal model of a MOSFET with transconductance represented by a voltage-controlled current source. The voltage source v_GS is connected between the gate (G) and source (S). The current source g_m v_GS is controlled by the voltage v_GS and flows from source (S) to drain (D). The resistor r_O is connected between drain (D) and source (S), representing the output resistance due to channel-length modulation.

(b)

Figure 6.31 (a) Small-signal model of MOSFET, (b) inclusion of channel-length modulation.

| Example $6.14$ | A MOSFET is biased at a drain current of 0.5 mA . If $\mu_{n} C_{o x}=100 \mu \mathrm{~A} / \mathrm{V}^{2}, W / L=10$, and $\lambda=0.1 \mathrm{~V}^{-1}$, calculate its small-signal parameters. |
| :---: | :---: |
| Solution | We have |
|  | $\begin{equation*} g_{m}=\sqrt{2 \mu_{n} C_{o x} \frac{W}{L} I_{D}} \tag{6.63} \end{equation*}$ |
|  | $\begin{equation*} =\frac{1}{1 \mathrm{k} \Omega} . \tag{6.64} \end{equation*}$ |
|  | Also, |
|  | $\begin{equation*} r_{O}=\frac{1}{\lambda I_{D}} \tag{6.65} \end{equation*}$ |
|  | $=20 \mathrm{k} \Omega$. (6.66) |
|  | This means that the intrinsic gain, $g_{m} r_{O}$ (Chapter 4), is equal to 20 for this choice of device dimensions and bias current. |
| Exercise | Repeat the above example if $W / L$ is doubled. |

## 6.4 PMOS TRANSISTOR

Having seen both $n p n$ and $p n p$ bipolar transistors, the reader may wonder if a $p$ type counterpart exists for MOSFETs. Indeed, as illustrated in Fig. 6.32(a), changing the doping polarities of the substrate and the S/D areas results in a "PMOS" device. The channel now consists of holes and is formed if the gate voltage is below the source potential by one threshold voltage. That is, to turn the device on, $V_{G S}<V_{T H}$, where $V_{T H}$ itself is negative. Following the conventions used for bipolar devices, we draw the PMOS device as in Fig. 6.32(b), with the source terminal identified by the arrow and placed
image_name:(a)
description:The image labeled as "(a)" illustrates the structure of a PMOS device. It depicts a cross-sectional view of the device, highlighting its key components and structure. The device is built on an n-type substrate, which serves as the foundational layer. Two heavily doped p-type regions, labeled as \( p^+ \), are embedded in the substrate, representing the source (S) and drain (D) areas. These regions are where the charge carriers (holes) originate and terminate, respectively.

The gate (G) is positioned above the substrate between the source and drain regions. It is separated from the substrate by a thin insulating layer, typically made of silicon dioxide, which is depicted as a hatched region in the diagram. This insulating layer is crucial as it allows the gate to control the flow of holes in the channel beneath it without direct electrical contact.

The diagram includes connections for each terminal: the source (S), gate (G), and drain (D) are shown with vertical lines leading to the surface, indicating their accessibility for external circuit connections. The source terminal is typically marked with an arrow in PMOS symbols, but here it is simply labeled.

Overall, the diagram effectively demonstrates the typical structure of a PMOS transistor, highlighting its n-substrate base, p-type source and drain regions, and the insulated gate that controls the channel's conductivity.
image_name:(b)
description:
[
name: Device, type: PMOS, ports: {S: S, D: D, G: G}
]
extrainfo:The diagram illustrates the structure of a PMOS transistor with labeled source (S), drain (D), and gate (G) terminals. It shows the device on an n-substrate with p+ doped source and drain regions.
image_name:(c)
description:The image labeled as (c) depicts the structure of a PMOS device. It shows a cross-sectional view with the following components:

1. **Source (S) and Drain (D):** These are marked as p+ regions, indicating that they are heavily doped with positive-type (hole) carriers.

2. **Gate (G):** Positioned above the channel, the gate is separated from the substrate by a thin insulating layer, typically oxide.

3. **n-substrate:** The main body of the device is an n-type substrate, indicating that it is doped with electrons as the majority carriers.

The illustration shows how the PMOS device is structured, with the source and drain embedded in the n-substrate and the gate controlling the channel between them. The device operates by forming a channel of holes when the gate voltage is below the source potential by one threshold voltage.
image_name:Figure 6.32
description:The image shows the structure of a PMOS (P-channel Metal-Oxide-Semiconductor) device. It consists of an n-type substrate with two p+ (heavily doped p-type) regions forming the source (S) and drain (D) terminals. These p+ regions are embedded in the n-substrate. Above the substrate, there is a gate (G) terminal, which is insulated from the substrate by a thin oxide layer, depicted as a striped region. The source (S) and drain (D) terminals are connected to the p+ regions, while the gate (G) is centrally located above the channel area, which is the region between the source and drain under the gate. This configuration allows holes to form the channel when the gate voltage is below the source potential by one threshold voltage, turning the device on.

(a)
image_name:Triode Region
description:
[
name: M1, type: PMOS, ports: {S: S, D: D, G: G}
]
extrainfo:The diagram illustrates the operation of a PMOS transistor (M1) in the triode and saturation regions, with different gate and drain voltage conditions.
image_name:Edge of Saturation
description:
[
name: M1, type: PMOS, ports: {S: S, D: D, G: G}
]
extrainfo:The diagram illustrates the PMOS transistor M1 at the edge of saturation, with the gate voltage equal to the threshold voltage (|VTHP|).

(c)
image_name:(b)
description:
[
name: M, type: PMOS, ports: {S: S, D: D, G: G}
]
extrainfo:The diagram illustrates the PMOS transistor M at the edge of saturation, with the gate voltage equal to the threshold voltage (|VTHP|).

(b)
image_name:(b)
description:
[
name: M1, type: PMOS, ports: {S: S, D: D, G: G}
]
extrainfo:The PMOS transistor M1 is at the edge of saturation, with the gate voltage equal to the threshold voltage (|VTHP|).

Figure 6.32 (a) Structure of PMOS device, (b) PMOS circuit symbol, (c) illustration of triode and saturation regions based on gate and drain voltages.
on top to emphasize its higher potential. The transistor operates in the triode region if the drain voltage is near the source potential, approaching saturation as $V_{D}$ falls to $V_{G}-V_{T H}=V_{G}+\left|V_{T H}\right|$. Figure 6.32(c) conceptually illustrates the gate-drain voltages required for each region of operation. We say that if $V_{D S}$ of a PMOS (NMOS) device is sufficiently negative (positive), then it is in saturation.

Example In the circuit of Fig. 6.33, determine the region of operation of $M_{1}$ as $V_{1}$ goes from $V_{D D}$ 6.15 to zero. Assume $V_{D D}=2.5 \mathrm{~V}$ and $\left|V_{T H}\right|=0.5 \mathrm{~V}$.
image_name:Figure 6.33 Simple PMOS circuit
description:
[
name: M1, type: PMOS, ports: {S: VDD, D: d, G: V1}
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
name: d, type: VoltageSource, value: 1V, ports: {Np: d, Nn: GND}
]
extrainfo:The circuit contains a PMOS transistor M1 with its source connected to VDD, its drain connected to node d, and its gate connected to node V1. The voltage source V1 is connected between node V1 and ground, and the voltage source d is connected between node d and ground. The circuit is used to analyze the operation region of M1 as V1 varies from VDD to 0V.

Figure 6.33 Simple PMOS circuit.

Solution For $V_{1}=V_{D D}, V_{G S}=0$ and $M_{1}$ is off. As $V_{1}$ falls and approaches $V_{D D}-\left|V_{T H}\right|$, the gatesource potential is negative enough to form a channel of holes, turning the device on. At this point, $V_{G}=V_{D D}-\left|V_{T H}\right|=+2 \mathrm{~V}$ while $V_{D}=+1 \mathrm{~V}$; i.e., $M_{1}$ is saturated [Fig. 6.32(c)]. As $V_{1}$ falls further, $V_{G S}$ becomes more negative and the transistor current rises. For $V_{1}=+1 \mathrm{~V}-\left|V_{T H}\right|=0.5 \mathrm{~V}, M_{1}$ is at the edge of the triode region. As $V_{1}$ goes below 0.5 V , the transistor enters the triode region further.

The voltage and current polarities in PMOS devices can prove confusing. Using the current direction shown in Fig. 6.32(b), we express $I_{D}$ in the saturation region as

$$
\begin{equation*}
I_{D, s a t}=-\frac{1}{2} \mu_{p} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2}\left(1-\lambda V_{D S}\right) \tag{6.67}
\end{equation*}
$$

where $\lambda$ is multiplied by a negative sign. ${ }^{14}$ In the triode region,

$$
\begin{equation*}
I_{D, t r i}=-\frac{1}{2} \mu_{p} C_{o x} \frac{W}{L}\left[2\left(V_{G S}-V_{T H}\right) V_{D S}-V_{D S}^{2}\right] \tag{6.68}
\end{equation*}
$$

Alternatively, both equations can be expressed in terms of absolute values:

$$
\begin{align*}
& \left|I_{D, s a t}\right|=\frac{1}{2} \mu_{p} C_{o x} \frac{W}{L}\left(\left|V_{G S}\right|-\left|V_{T H}\right|\right)^{2}\left(1+\lambda\left|V_{D S}\right|\right)  \tag{6.69}\\
& \left|I_{D, t r i}\right|=\frac{1}{2} \mu_{p} C_{o x} \frac{W}{L}\left[2\left(\left|V_{G S}\right|-\left|V_{T H}\right|\right)\left|V_{D S}\right|-V_{D S}^{2}\right] . \tag{6.70}
\end{align*}
$$

The small-signal model of PMOS transistor is identical to that of NMOS devices (Fig. 6.31). The following example illustrates this point.

[^2]Example
6.16

For the configurations shown in Fig. 6.34(a), determine the small-signal resistances $R_{X}$ and $R_{Y}$. Assume $\lambda \neq 0$.
image_name:Figure 6.34 (b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: g1d1, G: g1d1}
name: M2, type: PMOS, ports: {S: VDD, D: g2d2, G: g2d2}
name: Rx, type: Resistor, value: Rx, ports: {N1: g1d1, N2: GND}
name: Ry, type: Resistor, value: Ry, ports: {N1: g2d2, N2: GND}
]
extrainfo:The circuit consists of diode-connected NMOS and PMOS transistors with resistors Rx and Ry connected to the nodes g1d1 and g2d2 respectively. The NMOS source is grounded, and the PMOS source is connected to VDD.

(a)
image_name:Figure 6.34 (b)
description:
[
name: Vx, type: VoltageSource, value: Vx, ports: {Np: vx, Nn: GND}
name: gm1, type: VoltageControlledCurrentSource, value: gm1, ports: {Np: Vx, Nn: GND}
name: r01, type: Resistor, value: r01, ports: {N1: Vx, N2: GND}
]
extrainfo:The circuit represents a small-signal model with a voltage source Vx, a voltage-controlled current source gm1, and a resistor r01 all connected to node Vx. The ground node is labeled as GND. The current ix flows through the voltage source Vx into the node Vx.

(b)
image_name:(b)
description:
[
name: vY, type: VoltageSource, value: vY, ports: {Np: vY+, Nn: GND}
name: iY, type: CurrentControlledCurrentSource, ports: {Np: vY+, Nn: GND}
name: rO2, type: Resistor, value: rO2, ports: {N1: vY+, N2: GND}
]
extrainfo:The circuit is a small-signal model with a voltage source vY connected to a node labeled vY+. A current-controlled current source iY and a resistor rO2 are also connected to the node vY+. The ground node is labeled as GND. The current iY flows through the voltage source vY into the node vY+.

(c)

Figure 6.34 (a) Diode-connected NMOS and PMOS devices, (b) small-signal model of (a), (c) small-signal model of (b).

Solution For the NMOS version, the small-signal equivalent appears as depicted in Fig. 6.34(b), yielding

$$
\begin{align*}
R_{X} & =\frac{v_{X}}{i_{X}}  \tag{6.71}\\
& =\left(g_{m 1} v_{X}+\frac{v_{X}}{r_{O 1}}\right) \frac{1}{i_{X}}  \tag{6.72}\\
& =\frac{1}{g_{m 1}} \| r_{O 1} \tag{6.73}
\end{align*}
$$

For the PMOS version, we draw the equivalent as shown in Fig. 6.34(c) and write

$$
\begin{align*}
R_{Y} & =\frac{v_{Y}}{i_{Y}}  \tag{6.74}\\
& =\left(g_{m 2} v_{Y}+\frac{v_{Y}}{r_{O 1}}\right) \frac{1}{i_{Y}}  \tag{6.75}\\
& =\frac{1}{g_{m 2}} \| r_{O 2} \tag{6.76}
\end{align*}
$$

In both cases, the small-signal resistance is equal to $1 / g_{m}$ if $\lambda \rightarrow 0$.
In analogy with their bipolar counterparts [Fig. 4.44(a)], the structures shown in Fig. 6.34(a) are called "diode-connected" devices and act as two-terminal components: we will encounter many applications of diode-connected devices in Chapters 9 and 10.

Owing to the lower mobility of holes (Chapter 2), PMOS devices exhibit a poorer performance than NMOS transistors. For example, Eq. (6.46) indicates that the transconductance of a PMOS device is lower for a given drain current. We therefore prefer to use NMOS transistors wherever possible.

## 6.5 CMOS TECHNOLOGY

Is it possible to build both NMOS and PMOS devices on the same wafer? Figures 6.2(a) and 6.32(a) reveal that the two require different types of substrate. Fortunately, a local n-type substrate can be created in a $p$-type substrate, thereby accommodating PMOS transistors.
image_name:Figure 6.35 CMOS technology
description:The diagram illustrates CMOS technology, highlighting the integration of NMOS and PMOS transistors on a single substrate. The structure is divided into two main sections, each representing a different type of transistor.

1. **NMOS Device:**
- **Substrate:** The NMOS device is built on a p-type substrate.
- **Components:** It includes a source (S), gate (G), and drain (D). The source and drain are n+ doped regions.
- **Connection:** The gate is positioned above the channel, which is between the source and drain. The body (B) contact is connected to the p-type substrate.

2. **PMOS Device:**
- **Substrate:** The PMOS device is located within an n-well, which is embedded in the p-type substrate.
- **Components:** It consists of a source (S), gate (G), and drain (D). The source and drain are p+ doped regions.
- **Connection:** The gate is similarly positioned above the channel between the source and drain. The body (B) contact is connected to the n-well.

3. **Key Features and Annotations:**
- **Labels:** The diagram clearly labels the NMOS and PMOS devices, their respective components (S, G, D, B), and the substrate types (p-substrate, n-well).
- **Structure:** The n-well is shaded to distinguish it from the p-substrate, indicating the separate regions for NMOS and PMOS transistors.

This structure allows for the complementary operation of both NMOS and PMOS devices on the same chip, enabling the advantages of CMOS technology, such as lower power consumption and increased performance.

Figure 6.35 CMOS technology.
As illustrated in Fig. 6.35, an " $n$-well" encloses a PMOS device while the NMOS transistor resides in the $p$-substrate.

Called "complementary MOS" (CMOS) technology, the above structure requires more complex processing than simple NMOS or PMOS devices. In fact, the first few generations of MOS technology contained only NMOS transistors, ${ }^{15}$ and the higher cost of CMOS processes seemed prohibitive. However, many significant advantages of complementary devices eventually made CMOS technology dominant and NMOS technology obsolete.

## 6.6 COMPARISON OF BIPOLAR AND MOS DEVICES

Having studied the physics and operation of bipolar and MOS transistors, we can now compare their properties. Table 6.2 shows some of the important aspects of each device. Note that the exponential $I_{C}-V_{B E}$ dependence of bipolar devices accords them a higher transconductance for a given bias current.

TABLE 6.2 Comparison of bipolar and MOS transistors.

| Bipolar Transistor | MOSFET |
| :--- | :--- |
| Exponential Characteristic | Quadratic Characteristic |
| Active: $V_{C B}>0$ | Saturation: $V_{D S}>V_{G S}-V_{T H}$ (NMOS) |
| Saturation: $V_{C B}<0$ | Triode: $V_{D S}<V_{G S}-V_{T H}$ (NMOS) |
| Finite Base Current | Zero Gate Current |
| Early Effect | Channel-Length Modulation |
| Diffusion Current | Drift Current |
| - | Voltage-Dependent Resistor |

6.7 CHAPTER SUMMARY

- A voltage-dependent current source can form an amplifier along with a load resistor. MOSFETs are electronic devices that can operate as voltage-dependent current sources.
- A MOSFET consists of a conductive plate (the "gate") atop a semiconductor substrate and two junctions ("source" and "drain") in the substrate. The gate controls the current flow from the source to the drain. The gate draws nearly zero current because an insulating layer separates it from the substrate.

[^3]- As the gate voltage rises, a depletion region is formed in the substrate under the gate area. Beyond a certain gate-source voltage (the "threshold voltage"), mobile carriers are attracted to the oxide-silicon interface and a channel is formed.
- If the drain-source voltage is small, the device operates a voltage-dependent resistor.
- As the drain voltage rises, the charge density near the drain falls. If the drain voltage reaches one threshold below the gate voltage, the channel ceases to exist near the drain, leading to "pinch-off."
- MOSFETs operate in the "triode" region if the drain voltage is more than one threshold below the gate voltage. In this region, the drain current is a function of $V_{G S}$ and $V_{D S}$. The current is also proportional to the device aspect ratio, $W / L$.
- MOSFETs enter the "saturation region" if channel pinch-off occurs, i.e., the drain voltage is less than one threshold below the gate volatge. In this region, the drain current is proportional to $\left(V_{G S}-V_{T H}\right)^{2}$.
- MOSFETs operating in the saturation region behave as current sources and find wide application in microelectronic circuits.
- As the drain voltage exceeds $V_{G S}-V_{T H}$ and pinch-off occurs, the drain end of the channel begins to move toward the source, reducing the effective length of the device. Called "channel-length modulation," this effect leads to variation of drain current in the saturation region. That is, the device is not an ideal current source.
- A measure of the small-signal performance of voltage-dependent current sources is the "transconductance," defined as the change in the output current divided by the change in the input voltage. The transconductance of MOSFETs can be expressed by one of three equations in terms of the bias voltages and currents.
- Operation across different regions and/or with large swings exemplifies "large-signal behavior." If the signal swings are sufficiently small, the MOSFET can be represented by a small-signal model consisting of a linear voltage-dependent current source and an output resistance.
- The small-signal model is derived by making a small change in the voltage difference between two terminals while the the other voltages remain constant.
- The small-signal models of NMOS and PMOS devices are identical.
- NMOS and PMOS transistors are fabricated on the same substrate to create CMOS technology.
