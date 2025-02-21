# CHAPTER 2 Basic MOS Device Physics

In studying the design of integrated circuits (ICs), one of two extreme approaches can be taken, (1) begin with quantum mechanics and understand solid-state physics, semiconductor device physics, device modeling, and finally the design of circuits; or (2) treat each semiconductor device as a black box whose behavior is described in terms of its terminal voltages and currents and design circuits with little attention to the internal operation of the device. Experience shows that neither approach is optimum. In the first case, the reader cannot see the relevance of all the physics to designing circuits, and in the second, he or she is constantly mystified by the contents of the black box.

In today's IC industry, a solid understanding of semiconductor devices is essential—more so in analog design than in digital design, because in the former, transistors are not considered to be simple switches, and many of their second-order effects directly impact the performance. Furthermore, as each new generation of IC technologies scales the devices, these effects become more significant. Since the designer must often decide which effects can be neglected in a given circuit, insight into device operation proves invaluable.

In this chapter, we study the physics of MOSFETs at an elementary level, covering the bare minimum that is necessary for basic analog design. The ultimate goal is still to develop a circuit model for each device by formulating its operation, but this is accomplished through a good understanding of the underlying principles. After studying many analog circuits in Chapters 3 through 14 and gaining motivation for a deeper understanding of devices, we return to the subject in Chapter 17 and deal with other aspects of MOS operation.

We begin our study with the structure of MOS transistors and derive their I/V characteristics. Next, we describe second-order effects such as body effect, channel-length modulation, and subthreshold conduction. We then identify the parasitic capacitances of MOSFETs, derive a small-signal model, and present a simple SPICE model. We assume that the reader is familiar with such basic concepts as doping, mobility, and $p n$ junctions.

## 2.1 ■ General Considerations

### 2.1.1 MOSFET as a Switch

Before delving into the actual operation of the MOSFET, we consider a simplistic model of the device so as to gain a feel for what the transistor is expected to be and which aspects of its behavior are important.

Shown in Fig. 2.1 is the symbol for an $n$-type MOSFET, revealing three terminals: gate (G), source (S), and drain (D). The latter two are interchangeable because the device is symmetric. When operating
image_name:Figure 2.1 Simple view of a MOS device
description:
[
name: M1, type: NMOS, ports: {S: Source, D: Drain, G: Gate}
]
extrainfo:The diagram illustrates a simple NMOS transistor with labeled terminals: Source, Drain, and Gate, represented in a basic schematic symbol.

Figure 2.1 Simple view of a MOS device.
as a switch, the transistor "connects" the source and the drain together if the gate voltage, $V_{G}$, is "high" and isolates the source and the drain if $V_{G}$ is "low."

Even with this simplified view, we must answer several questions. For what value of $V_{G}$ does the device turn on? In other words, what is the "threshold" voltage? What is the resistance between S and D when the device is on (or off)? How does this resistance depend on the terminal voltages? Can we always model the path between S and D by a simple linear resistor? What limits the speed of the device?

While all of these questions arise at the circuit level, they can be answered only by analyzing the structure and physics of the transistor.

### 2.1.2 MOSFET Structure

Figure 2.2 shows a simplified structure of an $n$-type MOS (NMOS) device. Fabricated on a $p$-type substrate (also called the "bulk" or the "body"), the device consists of two heavily-doped $n$ regions forming the source and drain terminals, a heavily-doped (conductive) piece of polysilicon ${ }^{1}$ (simply called "poly") operating as the gate, and a thin layer of silicon dioxide $\left(\mathrm{SiO}_{2}\right)$ (simply called "oxide") insulating the gate from the substrate. The useful action of the device occurs in the substrate region under the gate oxide. Note that the structure is symmetric with respect to S and D .
image_name:Figure 2.2 Structure of a MOS device
description:The image depicts the structure of a Metal-Oxide-Semiconductor (MOS) device, specifically illustrating the arrangement of its components and the relationships between them. The key components visible in the diagram are:

1. **Source (S) and Drain (D) Regions:** These are heavily-doped n+ regions, represented on the left and right sides of the diagram, respectively. They form the terminals through which current enters and exits the device.

2. **Gate (G):** This is a piece of heavily-doped polysilicon, labeled as 'Poly' in the diagram. It is positioned above the substrate and controls the conductivity of the channel between the source and drain.

3. **Oxide Layer:** A thin layer of silicon dioxide (SiO2) insulates the gate from the p-substrate below. This layer is labeled as 'Oxide' in the diagram and is crucial for the MOS operation.

4. **p-Substrate:** The main body of the device is labeled as the p-substrate, which forms the foundational layer upon which other components are built.

5. **Dimensions and Labels:**
- The lateral dimension of the gate along the source-drain path is called the length, denoted as 'L'.
- The width 'W' is the dimension perpendicular to the length.
- 'L_drawn' is the total drawn length, while 'L_eff' (effective length) is the actual distance between the source and drain after accounting for side diffusion, calculated as \( L_{drawn} - 2L_D \), where \( L_D \) is the side diffusion length.
- 't_ox' represents the thickness of the oxide layer.

6. **Connections and Interactions:**
- The diagram shows the gate controlling the channel conductivity between the source and drain, which is a fundamental operation of the MOS device.
- The symmetry between the source and drain is indicated, suggesting that the device can operate in either direction depending on the applied voltages.

This schematic provides a conceptual view of a MOS device, highlighting the critical components and their spatial relationships, which are essential for understanding its operation.

Figure 2.2 Structure of a MOS device.
The lateral dimension of the gate along the source-drain path is called the length, $L$, and that perpendicular to the length is called the width, $W$. Since the S/D junctions "side-diffuse" during fabrication, the actual distance between the source and the drain is slightly less than $L$. To avoid confusion, we write, $L_{\text {eff }}=L_{\text {drawn }}-2 L_{D}$, where $L_{\text {eff }}$ is the "effective" length, $L_{\text {drawn }}$ is the total length, ${ }^{2}$ and $L_{D}$ is the amount of side diffusion. As we will see later, $L_{e f f}$ and the gate oxide thickness, $t_{o x}$, play an important role in the performance of MOS circuits. Consequently, the principal thrust in MOS technology development is to reduce both of these dimensions from one generation to the next without degrading other parameters of the device. Typical values at the time of this writing are $L_{e f f} \approx 10 \mathrm{~nm}$ and $t_{o x} \approx 15 \AA$. In the remainder of this book, we denote the effective length by $L$ unless otherwise stated.

[^1]If the MOS structure is symmetric, why do we call one $n$ region the source and the other the drain? This becomes clear if the source is defined as the terminal that provides the charge carriers (electrons in the case of NMOS devices) and the drain as the terminal that collects them. Thus, as the voltages at the three terminals of the device vary, the source and the drain may exchange roles. These concepts are practiced in the problems at the end of the chapter.

We have thus far ignored the substrate on which the device is fabricated. In reality, the substrate potential greatly influences the device characteristics. That is, the MOSFET is a four-terminal device. Since in typical MOS operation, the S/D junction diodes must be reverse-biased, we assume that the substrate of NMOS transistors is connected to the most negative supply in the system. For example, if a circuit operates between zero and 1.2 volts, $V_{\text {sub,NMOS }}=0$. The actual connection is usually provided through an ohmic $p^{+}$region, as depicted in the side view of the device in Fig. 2.3.
image_name:Figure 2.3 Substrate connection
description:The image labeled "Figure 2.3 Substrate connection" depicts a cross-sectional view of an NMOS transistor structure. The diagram illustrates the fundamental components and connections within the device:

1. **Components and Structure:**
- The NMOS transistor is built on a **p-type substrate**. This substrate forms the base layer of the device.
- Three distinct regions are shown: two **n+ regions** and one **p+ region**. The n+ regions are labeled as **S** (Source) and **D** (Drain), while the p+ region is labeled as **B** (Body or Bulk).
- A **gate (G)** is depicted above the substrate, separated by a thin insulating layer, representing the gate oxide.

2. **Connections and Interactions:**
- The Source (S) and Drain (D) regions are heavily doped n-type semiconductor regions that facilitate the flow of electrons when a voltage is applied.
- The Body (B) is a p+ region connected to the most negative supply voltage in the system, ensuring that the source-body junction is reverse-biased.
- The Gate (G) controls the flow of current between the Source (S) and Drain (D) by creating an electric field that modulates the conductivity of the channel beneath it.

3. **Labels, Annotations, and Key Features:**
- The diagram is annotated with labels for each terminal: B (Body), S (Source), G (Gate), and D (Drain).
- The substrate is explicitly labeled as "p-substrate," indicating the type of doping used.
- The n+ and p+ symbols denote the doping concentrations of the respective regions, with n+ indicating a high concentration of donor atoms and p+ indicating a high concentration of acceptor atoms.

This structure is typical for NMOS devices, where the substrate is generally connected to a low potential to ensure proper operation and prevent unwanted current paths.

Figure 2.3 Substrate connection.

In complementary MOS (CMOS) technologies, both NMOS and PMOS transistors are available. From a simplistic viewpoint, the PMOS device is obtained by negating all of the doping types (including the substrate) [Fig. 2.4(a)], but in practice, NMOS and PMOS devices must be fabricated on the same wafer, i.e., the same substrate. For this reason, one device type can be placed in a "local substrate," usually called a "well." In today's CMOS processes, the PMOS device is fabricated in an $n$-well [Fig. 2.4(b)]. Note that the $n$-well must be connected to a potential such that the S/D junction diodes of the PMOS transistor remain reverse-biased under all conditions. In most circuits, the $n$-well is tied to the most positive supply voltage. For the sake of brevity, we sometimes call NMOS and PMOS devices "NFETs" and "PFETs," respectively.

Figure 2.4(b) indicates an interesting difference between NMOS and PMOS transistors: while all NFETs share the same substrate, each PFET can have an independent $n$-well. This flexibility of PFETs is exploited in some analog circuits.

### 2.1.3 MOS Symbols

The circuit symbols used to represent NMOS and PMOS transistors are shown in Fig. 2.5. The symbols in Fig. 2.5(a) contain all four terminals, with the substrate denoted by "B" (bulk) rather than " $S$ " to avoid confusion with the source. The source of the PMOS device is positioned on top as a visual aid because it has a higher potential than its gate. Since in most circuits the bulk terminals of NMOS and PMOS devices are tied to ground and $V_{D D}$, respectively, we usually omit these connections in drawing [Fig. 2.5(b)]. In digital circuits, it is customary to use the "switch" symbols depicted in Fig. 2.5(c) for the two types, but we prefer those in Fig. 2.5(b) because the visual distinction between S and D proves helpful in understanding the operation of circuits.

#### Nanometer Design Notes

Some modern CMOS processes offer a "deep $n$-well," an $n$-well that contains an NMOS device and its $p$-type bulk. As shown below, the NMOS transistor's bulk is now localized and need not be tied to that of other NMOS devices. But the design incurs substantial area overhead because the deep $n$-well must extend beyond the $p$-well by a certain amount and must maintain a certain distance to the regular $n$-well.
image_name:NMOS and PMOS in wells
description:The image illustrates a cross-sectional view of PMOS and NMOS transistors integrated into semiconductor wells. On the left side, a PMOS transistor is shown within an n-well, and on the right side, an NMOS transistor is depicted within a deep n-well structure.

1. **Identification of Components and Structure:**
- **PMOS Transistor (Left):** The PMOS device is embedded in an n-well. The source and drain regions are indicated by p+ regions, and the n-well serves as the bulk.
- **NMOS Transistor (Right):** The NMOS device is placed within a deep n-well that contains a p-well. The source and drain regions are marked by n+ regions, and the p-well serves as the bulk.

2. **Connections and Interactions:**
- The PMOS transistor is isolated within the n-well, allowing its bulk to be connected separately from other PMOS devices. This isolation is achieved by the n-well surrounding the p+ regions.
- The NMOS transistor is similarly isolated by the deep n-well, which encases the p-well. This setup allows the NMOS bulk to be independently connected, preventing interference with other NMOS devices.

3. **Labels, Annotations, and Key Features:**
- The substrate for both transistors is a p-type substrate, as indicated at the bottom of the diagram.
- The n-well and deep n-well are clearly marked, highlighting the structural differences between the PMOS and NMOS configurations.
- The image emphasizes the advantage of using a deep n-well for localizing the NMOS bulk, which reduces unwanted interactions with other devices on the chip.

image_name:Simple PMOS device
description:The image depicts a simple PMOS device structure. It is a cross-sectional diagram showing the layout and components of a PMOS transistor. The main components are labeled as follows:

1. **B (Body):** The body contact is labeled 'B' and is connected to an n+ region, indicating that the body of the PMOS is connected to a positive region.

2. **S (Source):** The source contact is labeled 'S' and is connected to a p+ region, which is typical for PMOS devices as they have p-type source and drain regions.

3. **D (Drain):** The drain contact is labeled 'D' and is also connected to a p+ region, similar to the source.

4. **G (Gate):** The gate is labeled 'G' and is positioned above the channel region, which lies between the source and drain. The gate is insulated from the substrate by a thin layer, typically oxide.

5. **n-substrate:** The entire structure is built on an n-type substrate, which is indicated at the bottom of the diagram. This substrate supports the p-type regions of the PMOS.

**Connections and Interactions:**
- The diagram shows the source and drain regions as p+ regions, indicating heavily doped p-type areas. The gate controls the flow of holes between the source and drain by modulating the channel conductivity beneath it.
- The n+ region connected to the body (B) provides a contact to the n-substrate, which is necessary for biasing the PMOS transistor.

**Labels, Annotations, and Key Features:**
- The labels B, S, G, and D identify the key terminals of the PMOS device.
- The n-substrate label at the bottom highlights the type of substrate used, which is crucial for understanding the device operation and isolation properties.
- The diagram emphasizes the structural elements of a PMOS device, showcasing the typical arrangement and doping types involved.

image_name:Figure 2.4
description:The image labeled "Figure 2.4" illustrates two types of PMOS transistor configurations. The left side of the image shows a simple PMOS device, while the right side displays a PMOS inside an n-well.

1. **Identification of Components and Structure:**
- The left diagram represents a simple PMOS transistor. It includes terminals labeled as B (Body), S (Source), G (Gate), and D (Drain). The device is constructed on a p-substrate, with p+ regions indicating heavily doped p-type material for the Body and Source, and n+ for the Drain.
- The right diagram illustrates a PMOS transistor within an n-well. Similar to the simple PMOS, it has terminals labeled B, S, G, and D. However, this configuration is built on an n-well within a p-substrate, with p+ regions for the Source and Drain, and n+ for the Body.

2. **Connections and Interactions:**
- In both configurations, the Gate (G) is positioned above the channel between the Source (S) and Drain (D), controlling the flow of current between these two terminals. The Source (S) and Drain (D) are connected to p+ regions in the simple PMOS, and the n-well PMOS has p+ regions for Source and Drain embedded in the n-well.
- The Body (B) terminal is connected to the p+ region in the simple PMOS and to the n+ region in the n-well PMOS, which is crucial for biasing and isolating the device.

3. **Labels, Annotations, and Key Features:**
- The labels B, S, G, and D are crucial for identifying the terminals of the PMOS devices.
- The p-substrate and n-well labels highlight the substrate types used, which are essential for understanding the device operation and isolation properties.
- The diagram emphasizes the structural elements of a PMOS device, showcasing the typical arrangement and doping types involved, such as p+ and n+ regions for the respective transistor configurations.

Figure 2.4 (a) Simple PMOS device; (b) PMOS inside an $n$-well.

image_name:NMOS
description:
[
name: M1, type: NMOS, ports: {S: S, D: D, G: G}
]
extrainfo:The diagram shows the symbol for an NMOS transistor with labeled ports: Gate (G), Drain (D), Source (S), and Body (B). The Body terminal is typically connected to the Source in most configurations.}

image_name:NMOS
description:
[
name: M1, type: NMOS, ports: {S: S, D: D, G: G}
]
extrainfo:The diagram shows the symbol for an NMOS transistor with labeled ports: Gate (G), Drain (D), Source (S), and Body (B). The Body terminal is typically connected to the Source in most configurations.}

image_name:NMOS
description:
[
name: M1, type: NMOS, ports: {S: S, D: D, G: G}
]
extrainfo:The diagram shows the symbol for an NMOS transistor with labeled ports: Gate (G), Drain (D), Source (S), and Body (B). The Body terminal is typically connected to the Source in most configurations.}

Figure 2.5 MOS symbols.

## 2.2 ■ MOS I/V Characteristics

In this section, we analyze the generation and transport of charge in MOSFETs as a function of the terminal voltages. Our objective is to derive equations for the I/V characteristics such that we can elevate our abstraction from device physics level to circuit level.

### 2.2.1 Threshold Voltage

Consider an NFET connected to external voltages as shown in Fig. 2.6(a). What happens as the gate voltage, $V_{G}$, increases from zero? Since the gate, the dielectric, and the substrate form a capacitor, as $V_{G}$ becomes more positive, the holes in the $p$-substrate are repelled from the gate area, leaving negative ions behind so as to mirror the charge on the gate. In other words, a depletion region is created [Fig. 2.6(b)]. Under this condition, no current flows because no charge carriers are available.

As $V_{G}$ increases, so do the width of the depletion region and the potential at the oxide-silicon interface. In a sense, the structure resembles a voltage divider consisting of two capacitors in series: the gateoxide capacitor and the depletion-region capacitor [Fig. 2.6(c)]. When the interface potential reaches a sufficiently positive value, electrons flow from the source to the interface and eventually to the drain.
image_name:(a)
description:The image labeled "(a)" depicts a MOSFET (Metal-Oxide-Semiconductor Field-Effect Transistor) structure driven by a gate voltage, $V_G$. The diagram illustrates the basic components and layout of the MOSFET.

1. **Identification of Components and Structure:**
- The MOSFET consists of a gate, source, and drain, with the gate placed on top of a thin oxide layer.
- Below the oxide layer, there is a $p$-type silicon substrate.
- The source and drain are $n^+$ regions, indicating heavily doped n-type areas within the p-substrate.
- The gate is connected to a voltage source labeled $V_G$, which controls the operation of the MOSFET.

2. **Connections and Interactions:**
- The $V_G$ is applied to the gate, which influences the electric field across the oxide layer and the p-substrate.
- The source and drain are connected to external circuits, with a potential difference of +0.1V applied across them.
- There is no channel formed in this initial condition, indicating that the MOSFET is in the "off" state.

3. **Labels, Annotations, and Key Features:**
- The substrate is labeled as "p-substrate," and the heavily doped regions are marked as $n^+$.
- The gate voltage is denoted as $V_G$, showing its role in controlling the MOSFET.
- The absence of a channel under the gate oxide indicates that no current flows between the source and drain at this stage.
image_name:(b)
description:The image labeled as "(b)" depicts a MOSFET structure in the formation of a depletion region. The diagram shows a cross-section of a MOSFET device with a p-type substrate and n+ source and drain regions. The gate is situated above the substrate, separated by a gate oxide layer.

**1. Identification of Components and Structure:**
- **p-substrate:** The main body of the semiconductor, depicted as the lower layer in the diagram.
- **n+ regions:** Located on either side of the gate, these represent heavily doped n-type regions acting as the source and drain.
- **Gate:** Positioned above the substrate and separated by a thin oxide layer, controlling the channel formation.
- **Depletion Region:** Illustrated as a region between the source and drain beneath the gate, where negative ions are accumulated.

**2. Connections and Interactions:**
- The gate voltage \( V_G \) is applied, creating an electric field that influences the charge distribution in the substrate.
- The depletion region forms as the positive gate voltage repels holes in the p-substrate, leaving behind negatively charged ions.
- The diagram indicates the absence of a conductive channel, as no inversion layer is formed yet.

**3. Labels, Annotations, and Key Features:**
- **Negative Ions:** Indicated in the depletion region, showing the charge imbalance due to the applied gate voltage.
- **+0.1 V:** Annotated at the drain, indicating the potential applied across the device.
- **p-substrate, n+ regions, VG:** Clearly labeled to identify the material types and applied voltages.

This diagram illustrates the initial stage of MOSFET operation where the depletion region is formed, but no conductive channel is present yet, as the gate voltage has not reached the threshold level necessary for inversion.
image_name:(c)
description:Figure 2.6(c) illustrates the onset of inversion in a MOSFET structure. The diagram shows a cross-section of the MOSFET, highlighting the formation of capacitive elements at the oxide-silicon interface. The key components in this diagram include:

1. **Gate (G):** The gate is connected to a voltage source labeled \( V_G \), which controls the operation of the MOSFET.

2. **Oxide Layer:** This is the insulating layer between the gate and the silicon substrate, represented by a horizontal line separating the gate from the substrate.

3. **Depletion Region:** Below the oxide layer, a depletion region forms, indicated by a dashed line. This region is devoid of free charge carriers.

4. **Capacitors:** Two capacitors are depicted in series:
- \( C_{ox} \): The gate oxide capacitor, representing the capacitance of the oxide layer.
- \( C_{dep} \): The depletion region capacitor, representing the capacitance of the depletion region.

5. **Substrate:** The \( p \)-type substrate is shown at the bottom of the diagram, with \( n^+ \) regions on either side, indicating source and drain regions.

6. **Voltage Levels:** The diagram indicates a voltage of \(+0.1 \text{ V}\) applied to the drain.

The diagram effectively illustrates the concept of the MOSFET acting as a voltage divider, with the gate voltage \( V_G \) influencing the potential at the oxide-silicon interface. As \( V_G \) increases, the depletion region widens, and the system approaches the threshold voltage where inversion occurs, allowing current to flow from source to drain.
image_name:(d)
description:The image labeled as Figure 2.6(d) depicts the formation of an inversion layer in a MOSFET structure, indicating the transistor is turned on. The diagram shows a cross-sectional view of a MOSFET device with key components and annotations:

1. **Components and Structure:**
- The diagram includes a p-type substrate with two n+ regions representing the source and drain.
- Above the substrate, there is a gate oxide layer, and above this layer is the gate electrode connected to a gate voltage, V_G.
- The source and drain are labeled with a voltage of +0.1 V.

2. **Connections and Interactions:**
- The gate is connected to a voltage source labeled V_G, which is positive, indicating it is applying a positive gate voltage.
- As V_G increases, an inversion layer forms at the oxide-silicon interface, depicted by a series of negative symbols (electrons) beneath the gate oxide, creating a conductive channel between the source and drain.
- This channel allows electrons to flow from the source to the drain, indicating that the MOSFET is in the 'on' state.

3. **Labels, Annotations, and Key Features:**
- The diagram is annotated with the label 'Electrons (Channel)' to indicate the formation of the inversion layer.
- The substrate is labeled as 'p-substrate,' and the n+ regions are clearly marked.
- The diagram visually represents the concept of inversion, where the positive gate voltage induces a conductive channel of electrons in the p-type substrate, allowing current to flow between the source and drain.

Figure 2.6 (a) A MOSFET driven by a gate voltage; (b) formation of depletion region; (c) onset of inversion; (d) formation of inversion layer.

Thus, a "channel" of charge carriers is formed under the gate oxide between S and D , and the transistor is "turned on." We say the interface is "inverted." For this reason, the channel is also called the "inversion layer." The value of $V_{G}$ for which this occurs is called the "threshold voltage," $V_{T H}$. If $V_{G}$ rises further, the charge in the depletion region remains relatively constant while the channel charge density continues to increase, providing a greater current from S to D .

In reality, the turn-on phenomenon is a gradual function of the gate voltage, making it difficult to define $V_{T H}$ unambiguously. In semiconductor physics, the $V_{T H}$ of an NFET is usually defined as the gate voltage for which the interface is "as much $n$-type as the substrate is $p$-type." It can be proved [1] that $^{3}$

$$
\begin{equation*}
V_{T H}=\Phi_{M S}+2 \Phi_{F}+\frac{Q_{d e p}}{C_{o x}} \tag{2.1}
\end{equation*}
$$

where $\Phi_{M S}$ is the difference between the work functions of the polysilicon gate and the silicon substrate, $\Phi_{F}=(k T / q) \ln \left(N_{\text {sub }} / n_{i}\right), k$ is Boltzmann's constant, $q$ is the electron charge, $N_{\text {sub }}$ is the doping density of the substrate, $n_{i}$ is the density of electrons in undoped silicon, $Q_{d e p}$ is the charge in the depletion region, and $C_{o x}$ is the gate-oxide capacitance per unit area. From $p n$ junction theory, $Q_{d e p}=\sqrt{4 q \epsilon_{s i}\left|\Phi_{F}\right| N_{s u b}}$, where $\epsilon_{s i}$ denotes the dielectric constant of silicon. Since $C_{o x}$ appears very frequently in device and circuit calculations, it is helpful to remember that for $t_{o x} \approx 20 \AA, C_{o x} \approx 17.25 \mathrm{fF} / \mu \mathrm{m}^{2}$. The value of $C_{o x}$ can then be scaled proportionally for other oxide thicknesses.

In practice, the "native" threshold value obtained from the above equation may not be suited to circuit design, e.g., $V_{T H}=0$ and the device does not turn off for $V_{G} \geq 0 .{ }^{4}$ For this reason, the threshold voltage is typically adjusted by implantation of dopants into the channel area during device fabrication, in essence altering the doping level of the substrate near the oxide interface. For example, as shown in Fig. 2.7, if a thin sheet of $p^{+}$is created, the gate voltage required to deplete this region increases.

[^2]image_name:Figure 2.7
description:The image labeled "Figure 2.7" illustrates a cross-sectional view of a semiconductor device structure, focusing on the implantation of $p^+$ dopants to alter the threshold voltage.

1. **Identification of Components and Structure:**
- The diagram shows a semiconductor substrate labeled as "p-substrate," indicating that the base material is p-type.
- There are two n+ regions on either side of the structure, which likely represent heavily doped n-type source and drain regions.
- A thin sheet of $p^+$ is depicted beneath the gate oxide, indicating the presence of a highly doped p-type region. This is crucial for modifying the threshold voltage of the device.
- Above the $p^+$ region, there is a layer that represents the gate oxide and gate electrode.

2. **Connections and Interactions:**
- The $p^+$ region is strategically placed under the gate oxide layer, affecting the electric field distribution when a voltage is applied to the gate. This setup is designed to increase the gate voltage required to deplete the channel, thereby adjusting the threshold voltage.
- The n+ regions are separated by the $p^+$ channel, which is modulated by the gate voltage to control the current flow between the source and drain.

3. **Labels, Annotations, and Key Features:**
- The diagram is annotated with labels such as "p-substrate," "n+," and "p+" to clearly identify the different regions and doping types.
- An arrow points to the $p^+$ region, emphasizing its role in the device structure.
- The layout suggests a typical MOSFET configuration, where the manipulation of the channel doping is used to adjust the device's electrical characteristics, specifically the threshold voltage.

Figure 2.7 Implantation of $p+$ dopants to alter the threshold.

The above definition is not directly applicable to the measurement of $V_{T H}$. In Fig. 2.6(a), only the drain current can indicate whether the device is "on" or "off," failing to reveal at what $V_{G S}$ the interface is as much $n$-type as the bulk is $p$-type. As a result, the calculation of $V_{T H}$ from I/V measurements is somewhat ambiguous. We will return to this point later, but assume for now that the device turns on abruptly for $V_{G S} \geq V_{T H}$.

The turn-on phenomenon in a PMOS device is similar to that of NFETs, but with all the polarities reversed. As shown in Fig. 2.8, if the gate-source voltage becomes sufficiently negative, an inversion layer consisting of holes is formed at the oxide-silicon interface, providing a conduction path between the source and the drain. That is, the threshold voltage of a PMOS device is typically negative.
image_name:Figure 2.8 Formation of inversion layer in a PFET
description:
[
name: M1, type: PMOS, ports: {S: GND, D: d1, G: g1}
name: VG, type: VoltageSource, value: VG, ports: {Np: GND, Nn: g1}
]
extrainfo:The circuit illustrates the formation of an inversion layer in a PMOS device when the gate-source voltage is sufficiently negative. The PMOS transistor M1 is connected with its source to node 'p', its drain to node 'd1', and its gate to node 'g1'. The voltage source VG supplies a voltage between 'p' and 'g1' to control the gate voltage.

Figure 2.8 Formation of inversion layer in a PFET.

### 2.2.2 Derivation of I/V Characteristics

In order to obtain the relationship between the drain current of a MOSFET and its terminal voltages, we make two observations.

First, consider a semiconductor bar carrying a current $I$ [Fig. 2.9(a)]. If the mobile charge density along the direction of current is $Q_{d}$ coulombs per meter and the velocity of the charge is $v$ meters per second, then

$$
\begin{equation*}
I=Q_{d} \cdot v \tag{2.2}
\end{equation*}
$$

To understand why, we measure the total charge that passes through a cross section of the bar in unit time. With a velocity $v$, all of the charge enclosed in $v$ meters of the bar must flow through the cross section in
image_name:Figure 2.9 (a)
description:The image consists of two parts labeled (a) and (b), each depicting a semiconductor bar to illustrate the flow of current and charge.

1. **Figure 2.9 (a):**
- **Components and Structure:** This part of the image shows a rectangular block representing a semiconductor bar. An arrow labeled 'I' is drawn across the bar, indicating the direction of current flow through the semiconductor.
- **Connections and Interactions:** The arrow suggests a unidirectional flow of electric current along the length of the bar.
- **Labels, Annotations, and Key Features:** The label 'I' signifies the current flowing through the bar.

2. **Figure 2.9 (b):**
- **Components and Structure:** This section is divided into two snapshots of the same semiconductor bar, shown one second apart. The bar is divided into segments to illustrate the movement of charge carriers.
- **Connections and Interactions:** The first snapshot shows a section of the bar shaded to represent a certain volume of charge carriers moving at a velocity 'v'. In the second snapshot, taken one second later, this shaded section has moved further along the bar by 'v' meters, illustrating the displacement of charge carriers over time.
- **Labels, Annotations, and Key Features:** The label 'v meters' indicates the distance the charge carriers have moved in one second. An arrow labeled 'One second later' connects the two snapshots to show the passage of time and movement of charge.
image_name:Figure 2.9 (b)
description:The image consists of two parts labeled as Figure 2.9 (a) and Figure 2.9 (b).

1. **Figure 2.9 (a)**: This part of the image shows a schematic representation of a semiconductor bar. The bar is depicted as a rectangular block with an arrow inside it pointing to the right, indicating the direction of current flow, labeled as 'I'. This suggests that the semiconductor bar is conducting an electric current.

2. **Figure 2.9 (b)**: This part illustrates the movement of charge carriers within the semiconductor bar over time. It consists of two snapshots of the bar, one taken initially and the other one second later. The bar is divided into sections:
- The left section is shaded in light gray, representing the initial position of the charge carriers.
- The middle section is shaded in dark gray, indicating the position of the charge carriers after moving a distance of 'v' meters in one second.
- The right section is unshaded initially but becomes shaded one second later, illustrating the movement of the charge carriers from the left to the right over time.
- An arrow labeled "One second later" connects the two snapshots, emphasizing the time lapse and the movement of carriers.

**Key Features and Annotations**:
- The distance 'v meters' is marked with arrows showing the direction of the movement of charge carriers.
- The annotation "One second later" highlights the time interval between the two snapshots.

This diagram helps in visualizing how the charge carriers move through the semiconductor bar over time, contributing to the flow of current as described by the equation \( I = Q_{d} \cdot v \), where \( Q_{d} \) is the charge density and \( v \) is the velocity of the charge carriers.

Figure 2.9 (a) A semiconductor bar carrying a current $I$; (b) snapshots of the carriers one second apart.
one second [Fig. 2.9(b)]. Since the charge density is $Q_{d}$, the total charge in $v$ meters equals $Q_{d} \cdot v$. This lemma proves useful in analyzing semiconductor devices.

Second, to utilize the above lemma, we must determine the mobile charge density in a MOSFET. To this end, consider an NFET whose source and drain are connected to ground [Fig. 2.10(a)]. What is the charge density in the inversion layer? Since we assume that the onset of inversion occurs at $V_{G S}=V_{T H}$, the inversion charge density produced by the gate-oxide capacitance is proportional to $V_{G S}-V_{T H}$. For $V_{G S} \geq V_{T H}$, any charge placed on the gate must be mirrored by the charge in the channel, yielding a uniform channel charge density (charge per unit length along the source-drain path) equal to

$$
\begin{equation*}
Q_{d}=W C_{o x}\left(V_{G S}-V_{T H}\right) \tag{2.3}
\end{equation*}
$$

where $C_{o x}$ is multiplied by $W$ to represent the total capacitance per unit length.
Now suppose, as depicted in Fig. 2.10(b), that the drain voltage is greater than zero. Since the channel potential varies from zero at the source to $V_{D}$ at the drain, the local voltage difference between the gate and the channel varies from $V_{G}$ (near the source) to $V_{G}-V_{D}$ (near the drain). Thus, the charge density at a point $x$ along the channel can be written as

$$
\begin{equation*}
Q_{d}(x)=W C_{o x}\left[V_{G S}-V(x)-V_{T H}\right] \tag{2.4}
\end{equation*}
$$

where $V(x)$ is the channel potential at $x$. From (2.2), the current is given by

$$
\begin{equation*}
I_{D}=-W C_{o x}\left[V_{G S}-V(x)-V_{T H}\right] v \tag{2.5}
\end{equation*}
$$

image_name:Channel charge with equal source and drain voltages
description:The image depicts a cross-sectional view of a MOSFET (Metal-Oxide-Semiconductor Field-Effect Transistor) structure, highlighting the channel charge when the source and drain voltages are equal. The diagram consists of several key components and annotations:

1. **Components and Structure:**
- **Source (S) and Drain (D):** These are the terminals of the MOSFET where current enters and exits the device. They are labeled with 'S' and 'D' respectively.
- **Gate (G):** Positioned above the channel, it is labeled with 'V_G', indicating the gate voltage.
- **Channel Width (W):** The width of the channel through which the charge carriers move.
- **p-substrate and n+ regions:** The substrate is p-type, while the source and drain regions are heavily doped n-type (n+).
- **Gate-Substrate Voltage Difference:** This is marked as a vertical distance between the gate and the substrate, indicating the potential difference that controls the channel conductivity.

2. **Connections and Interactions:**
- The channel lies between the source and drain, allowing for the flow of electrons when a voltage is applied to the gate.
- The gate voltage (V_G) controls the electron flow by creating an electric field that modulates the conductivity of the channel.
- The diagram shows a current flow from source to drain, as indicated by arrows.

3. **Labels, Annotations, and Key Features:**
- The gate voltage is labeled as 'V_G', crucial for controlling the channel.
- The width of the channel is indicated by 'W'.
- A small schematic on the right shows a simplified representation of the MOSFET with the gate voltage 'V_G' and a transistor symbol 'M_1' indicating the MOSFET.
- The diagram emphasizes the equal voltage condition at the source and drain, which is a critical aspect of the charge distribution in the channel.

Overall, the image provides a clear visualization of the MOSFET structure and its operation under equal source and drain voltage conditions, focusing on the charge distribution in the channel and the impact of gate voltage.
image_name:Channel charge with unequal source and drain voltages
description:
[
name: M1, type: NMOS, ports: {S: GND, D: GND, G: VG}
]
extrainfo:The diagram shows an NMOS transistor M1 with the gate connected to VG and both the source and drain connected to ground. The illustration also depicts the channel charge distribution with unequal source and drain voltages.

image_name:(b)
description:The image illustrates an NMOS transistor labeled as M1. The diagram focuses on the channel charge distribution with unequal source and drain voltages. The NMOS transistor is structured with the source (S) and drain (D) terminals both connected to ground, while the gate (G) is connected to a voltage source labeled VG.

In the diagram, the NMOS transistor is built on a p-type substrate, with n+ regions indicating the source and drain areas. A channel is formed between these n+ regions, and the charge distribution within this channel is depicted. The diagram shows a gradient illustrating how the charge density varies along the channel length, denoted by 'x', from the source to the drain.

The channel width is labeled as 'W', and the length of the channel is marked as 'L'. The charge carriers, which are electrons in this NMOS device, move from the source to the drain, driven by the voltage difference between these terminals.

Additionally, the image includes a schematic representation of the NMOS transistor on the right side, showing the connections of the gate to VG, the source to ground, and the drain to a voltage source VD, which is not equal to the source voltage. This setup creates the condition of unequal source and drain voltages, affecting the charge distribution in the channel as indicated by the curve labeled 'Gate-Sub. Voltage Difference'.

Overall, the diagram effectively illustrates the effect of unequal voltages at the source and drain on the charge distribution within the NMOS transistor's channel.
image_name:Channel charge with unequal source and drain voltages
description:
[
name: M1, type: NMOS, ports: {S: GND, D: GND, G: VG}
]
extrainfo:The NMOS transistor M1 has its gate connected to VG, the source connected to node s1 (ground), and the drain connected to node d1, which is also connected to the positive terminal of the voltage source VD. The voltage source VD has its negative terminal connected to ground. The diagram illustrates the channel charge distribution with unequal source and drain voltages.

Figure 2.10 Channel charge with (a) equal source and drain voltages and (b) unequal source and drain voltages.
where the negative sign is inserted because the charge carriers are negative. Note that $v$ denotes the velocity of the electrons in the channel. For semiconductors, $v=\mu E$, where $\mu$ is the mobility of charge carriers and $E$ is the electric field. Noting that $E(x)=-d V / d x$ and representing the mobility of electrons by $\mu_{n}$, we have

$$
\begin{equation*}
I_{D}=W C_{o x}\left[V_{G S}-V(x)-V_{T H}\right] \mu_{n} \frac{d V(x)}{d x} \tag{2.6}
\end{equation*}
$$

subject to boundary conditions $V(0)=0$ and $V(L)=V_{D S}$. While $V(x)$ can be easily found from this equation, the quantity of interest is in fact $I_{D}$. Multiplying both sides by $d x$ and performing integration, we obtain

$$
\begin{equation*}
\int_{x=0}^{L} I_{D} d x=\int_{V=0}^{V_{D S}} W C_{o x} \mu_{n}\left[V_{G S}-V(x)-V_{T H}\right] d V \tag{2.7}
\end{equation*}
$$

Since $I_{D}$ is constant along the channel,

$$
\begin{equation*}
I_{D}=\mu_{n} C_{o x} \frac{W}{L}\left[\left(V_{G S}-V_{T H}\right) V_{D S}-\frac{1}{2} V_{D S}^{2}\right] \tag{2.8}
\end{equation*}
$$

Note that $L$ is the effective channel length.
Figure 2.11 plots the parabolas given by (2.8) for different values of $V_{G S}$, indicating that the "current capability" of the device increases with $V_{G S}$. Calculating $\partial I_{D} / \partial V_{D S}$, the reader can show that the peak of each parabola occurs at $V_{D S}=V_{G S}-V_{T H}$ and the peak current is

$$
\begin{equation*}
I_{D, \max }=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2} \tag{2.9}
\end{equation*}
$$

We call $V_{G S}-V_{T H}$ the "overdrive voltage" and $W / L$ the "aspect ratio." If $V_{D S} \leq V_{G S}-V_{T H}$, we say the device operates in the "triode region." 5
image_name:Figure 2.11 Drain current versus drain-source voltage in the triode region.
description:The graph in Figure 2.11 is a plot illustrating the relationship between the drain current ($I_D$) and the drain-source voltage ($V_{DS}$) for a MOSFET operating in the triode region. The graph is a typical representation used in CMOS circuit design to understand how the drain current varies with changes in the drain-source voltage under different gate-source voltages ($V_{GS}$).

1. **Type of Graph and Function:**
- The graph is a plot of drain current ($I_D$) versus drain-source voltage ($V_{DS}$) for different gate-source voltages ($V_{GS}$).

2. **Axes Labels and Units:**
- The vertical axis is labeled $I_D$, representing the drain current. The units are typically in amperes (A).
- The horizontal axis is labeled $V_{DS}$, representing the drain-source voltage, typically measured in volts (V).
- The graph is plotted on a linear scale.

3. **Overall Behavior and Trends:**
- The graph shows several parabolic curves, each corresponding to a different $V_{GS}$ value.
- As $V_{DS}$ increases, the drain current initially increases, reaching a peak, and then decreases.
- The peak of each parabola occurs at $V_{DS} = V_{GS} - V_{TH}$, where $V_{TH}$ is the threshold voltage.
- The curves shift to the right as $V_{GS}$ increases, indicating higher peak drain currents for higher gate-source voltages.

4. **Key Features and Technical Details:**
- The shaded region on the left of the graph indicates the triode region of operation, where $V_{DS} \leq V_{GS} - V_{TH}$.
- The peaks of the parabolas represent the maximum drain current ($I_{D,\max}$) for each $V_{GS}$.
- The aspect ratio ($W/L$) and the overdrive voltage ($V_{GS} - V_{TH}$) are key parameters influencing the peak current.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for different $V_{GS}$ values, labeled as $V_{GS1}$, $V_{GS2}$, and $V_{GS3}$.
- Vertical dashed lines are drawn at $V_{GS} - V_{TH}$ for each $V_{GS}$, marking the points of maximum drain current.
- The graph effectively demonstrates the dependency of the drain current on the gate-source voltage and the drain-source voltage in the triode region.

Figure 2.11 Drain current versus drain-source voltage in the triode region.

Equations (2.8) and (2.9) serve as our first step toward CMOS circuit design, describing the dependence of $I_{D}$ upon the constant of the technology, $\mu_{n} C_{o x}$, the device dimensions, $W$ and $L$, and the gate and drain potentials with respect to the source. Note that the integration in (2.7) assumes that $\mu_{n}$ and $V_{T H}$ are independent of $x$ and the gate and drain voltages, an approximation that we will revisit in Chapter 17.

[^3]If in (2.8), $V_{D S} \ll 2\left(V_{G S}-V_{T H}\right)$, we have

$$
\begin{equation*}
I_{D} \approx \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right) V_{D S} \tag{2.10}
\end{equation*}
$$

that is, the drain current is a linear function of $V_{D S}$. This is also evident from the characteristics of Fig. 2.11 for small $V_{D S}$ : as shown in Fig. 2.12, each parabola can be approximated by a straight line. The linear relationship implies that the path from the source to the drain can be represented by a linear resistor equal to

$$
\begin{equation*}
R_{o n}=\frac{1}{\mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)} \tag{2.11}
\end{equation*}
$$

image_name:Figure 2.12
description:Figure 2.12 illustrates the drain current ($I_D$) versus the drain-source voltage ($V_{DS}$) characteristics of a MOSFET, highlighting its operation in the deep triode region. The graph is a family of curves plotted on a Cartesian coordinate system, with $I_D$ on the vertical axis and $V_{DS}$ on the horizontal axis. Both axes are likely in linear scale.

**Axes Labels and Units:**
- **Vertical Axis ($I_D$):** Represents the drain current, typically measured in amperes (A).
- **Horizontal Axis ($V_{DS}$):** Represents the drain-source voltage, typically measured in volts (V).

**Overall Behavior and Trends:**
- The graph shows three distinct curves, each corresponding to a different gate-source voltage ($V_{GS1}$, $V_{GS2}$, $V_{GS3}$) with $V_{GS3} > V_{GS2} > V_{GS1}$.
- Each curve starts at the origin and initially rises linearly, indicating a linear relationship between $I_D$ and $V_{DS}$ for small values of $V_{DS}$, which is characteristic of the deep triode region.
- As $V_{DS}$ increases, each curve begins to bend, indicating a transition from the linear region to a more saturated behavior.

**Key Features and Technical Details:**
- The linear region is emphasized by an inset zooming in on the initial part of the curves, where the curves appear as straight lines.
- This linear region corresponds to the condition $V_{DS} \ll 2(V_{GS} - V_{TH})$, where the MOSFET behaves like a linear resistor.
- The slope of these lines in the linear region is steeper for higher $V_{GS}$ values, indicating higher drain currents for the same $V_{DS}$.

**Annotations and Specific Data Points:**
- The inset highlights the linear approximation of the curves, providing a clear visual of the linear operation.
- The curves are labeled with their respective $V_{GS}$ values, showing the dependency of the drain current on the gate-source voltage.

Figure 2.12 Linear operation in deep triode region.
A MOSFET can therefore operate as a resistor whose value is controlled by the overdrive voltage [so long as $\left.V_{D S} \ll 2\left(V_{G S}-V_{T H}\right)\right]$. This is conceptually illustrated in Fig. 2.13. Note that in contrast to bipolar transistors, a MOS device may be on even if it carries no current. With the condition $V_{D S} \ll 2\left(V_{G S}-V_{T H}\right)$, we say the device operates in the deep triode region.
image_name:Figure 2.13 MOSFET as a controlled linear resistor
description:
[
name: M1, type: NMOS, ports: {S: S, D: D, G: G}
]
extrainfo:The diagram shows a MOSFET operating as a controlled linear resistor, where the gate-source voltage (VGS) controls the resistance between the source (S) and drain (D).

Figure 2.13 MOSFET as a controlled linear resistor.

#### Example 2.1

For the arrangement in Fig. 2.14(a), plot the on-resistance of $M_{1}$ as a function of $V_{G}$. Assume that $\mu_{n} C_{o x}=$ $50 \mu \mathrm{~A} / \mathrm{V}^{2}, W / L=10$, and $V_{T H}=0.3 \mathrm{~V}$. Note that the drain terminal is open.

#### Solution

Since the drain terminal is open, $I_{D}=0$ and $V_{D S}=0$. Thus, if the device is on, it operates in the deep triode region. For $V_{G}<1 \mathrm{~V}+V_{T H}, M_{1}$ is off and $R_{o n}=\infty$. For $V_{G}>1 \mathrm{~V}+V_{T H}$, we have

$$
\begin{equation*}
R_{o n}=\frac{1}{50 \mu \mathrm{~A} / \mathrm{V}^{2} \times 10\left(V_{G}-1 \mathrm{~V}-0.3 \mathrm{~V}\right)} \tag{2.12}
\end{equation*}
$$

The result is plotted in Fig. 2.14(b).
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: S1, D: d1, G: VG}
name: S1, type: VoltageSource, value: 1V, ports: {Np: S1, Nn: GND}
]
extrainfo:The NMOS transistor M1 is used as a controllable resistor with its source connected to the voltage source S1, drain open at node d1, and gate voltage VG controlling the resistance. The graph (b) shows how the on-resistance Ron of M1 varies with the gate voltage VG, indicating that Ron decreases as VG increases beyond 1.3 V.
image_name:(b)
description:The graph in Figure 2.14(b) is a plot depicting the relationship between the gate voltage \( V_G \) and the on-resistance \( R_{on} \) of a MOSFET device. This is a typical curve used to illustrate how the resistance changes with varying gate voltage in a MOS transistor operating as a voltage-controlled resistor.

Axes Labels and Units:
- **X-axis (Horizontal):** Represents the gate voltage \( V_G \) in volts (V). The scale appears to be linear, with a significant marker at 1.3 V.
- **Y-axis (Vertical):** Represents the on-resistance \( R_{on} \), likely in ohms (Ω), although specific units are not annotated on the graph.

Overall Behavior and Trends:
- The graph shows a decreasing trend, indicating that as the gate voltage \( V_G \) increases, the on-resistance \( R_{on} \) decreases.
- The curve starts at a high resistance value when \( V_G \) is just above 1.3 V and decreases sharply.
- This behavior is consistent with the MOSFET entering the triode region, where an increase in \( V_G \) reduces the channel resistance.

Key Features and Technical Details:
- **Threshold Voltage:** The graph indicates a threshold around 1.3 V, beyond which the on-resistance starts decreasing significantly. This corresponds to the condition \( V_G > 1 \text{ V} + V_{TH} \), where \( V_{TH} \) is the threshold voltage of the MOSFET.
- **Sharp Decrease:** The curve shows a sharp decrease in \( R_{on} \) immediately after 1.3 V, which is typical for MOSFETs as they transition from the cutoff to the triode region.

Annotations and Specific Data Points:
- There is a vertical dashed line at 1.3 V, highlighting the threshold voltage where the change in behavior occurs.
- No other specific numerical values or annotations are provided on the graph, but the general trend is clear from the shape of the curve.

Figure 2.14

MOSFETs operating as controllable resistors play a crucial role in many analog circuits. For example, a voltage-controlled resistor can be used to adjust the frequency of the clock generator in a laptop computer if the system must go into a power saving mode. As studied in Chapter 13, MOSFETs also serve as switches.

What happens if the drain-source voltage in Fig. 2.11 exceeds $V_{G S}-V_{T H}$ ? In reality, the drain current does not follow the parabolic behavior for $V_{D S}>V_{G S}-V_{T H}$. In fact, as shown in Fig. 2.15, $I_{D}$ becomes relatively constant, and we say the device operates in the "saturation" region. ${ }^{6}$ To understand this phenomenon, recall from (2.4) that the local density of the inversion-layer charge is proportional to $V_{G S}-V(x)-V_{T H}$. Thus, if $V(x)$ approaches $V_{G S}-V_{T H}$, then $Q_{d}(x)$ drops to zero. In other words, as depicted in Fig. 2.16, if $V_{D S}$ is slightly greater than $V_{G S}-V_{T H}$, then the inversion layer stops at $x \leq L$, and we say the channel is "pinched off." As $V_{D S}$ increases further, the point at which $Q_{d}$ equals zero gradually moves toward the source. Thus, at some point along the channel, the local potential difference between the gate and the oxide-silicon interface is not sufficient to support an inversion layer.
image_name:Figure 2.15 Saturation of drain current
description:The graph in Figure 2.15 is a plot depicting the saturation of drain current (I_D) in a MOSFET device as a function of the drain-source voltage (V_DS). The graph is a family of curves, each representing a different gate-source voltage (V_GS) level: V_GS1, V_GS2, and V_GS3, with V_GS3 being the highest.

**Axes Labels and Units:**
- The vertical axis is labeled I_D, representing the drain current. The units are not specified, but it is typically measured in amperes (A).
- The horizontal axis is labeled V_DS, representing the drain-source voltage, typically measured in volts (V).

**Overall Behavior and Trends:**
- The curves show that as V_DS increases, the drain current I_D initially increases. However, after a certain point, the current levels off, indicating the onset of the saturation region.
- The saturation region is highlighted in the graph, showing where the drain current remains relatively constant despite further increases in V_DS.
- The curves for higher V_GS (such as V_GS3) reach higher levels of I_D, indicating that increasing the gate-source voltage allows more current to flow.

**Key Features and Technical Details:**
- The point where each curve enters the saturation region is marked by V_GS - V_TH for each respective curve, indicating the threshold voltage V_TH.
- The graph illustrates that the saturation region begins when V_DS exceeds V_GS - V_TH.

**Annotations and Specific Data Points:**
- There are vertical dashed lines marking the points V_GS1 - V_TH, V_GS2 - V_TH, and V_GS3 - V_TH on the V_DS axis, indicating the transition into the saturation region for each corresponding V_GS level.
- The shaded area emphasizes the saturation region, where the drain current remains constant for each curve.

Overall, the graph effectively illustrates the behavior of the drain current in response to varying gate-source and drain-source voltages, highlighting the saturation phenomenon in MOSFET operation.

Figure 2.15 Saturation of drain current.

How does the device conduct current in the presence of pinch-off? As the electrons approach the pinch-off point (where $Q_{d} \rightarrow 0$ ), their velocity rises tremendously ( $v=I / Q_{d}$ ). Upon passing the pinchoff point, the electrons simply shoot through the depletion region near the drain junction and arrive at the drain terminal.

[^4]image_name:Figure 2.16 Pinch-off behavior
description:The diagram labeled "Figure 2.16 Pinch-off behavior" illustrates the pinch-off phenomenon in a MOSFET device. It consists of two sections, each depicting a different state of the device under varying drain-source voltage conditions.

1. **Identification of Components and Structure:**
- The diagram shows two n+ regions (source and drain) separated by a channel region under a gate. The gate is depicted as a metal layer above a dielectric, illustrating the MOSFET structure.
- The gate voltage ($V_G$) is applied to the gate terminal, and the drain-source voltages ($V_{DS1}$ and $V_{DS2}$) are applied to the drain terminal.
- The channel is shown under the gate, and it is represented with a shaded area which narrows towards the drain, indicating the pinch-off region.

2. **Connections and Interactions:**
- The source is grounded, and the gate has a voltage $V_G$ applied. The drain has a variable voltage, either $V_{DS1}$ or $V_{DS2}$.
- The pinch-off point is indicated where the channel narrows, showing the transition from a conductive channel to a depletion region near the drain.
- The diagram illustrates how the channel length reduces as the drain-source voltage increases, demonstrating the effect of pinch-off on current flow.

3. **Labels, Annotations, and Key Features:**
- Important labels include $V_{G}$ for gate voltage and $V_{DS1}$, $V_{DS2}$ for drain-source voltages, with $V_{DS2} > V_{DS1}$.
- The pinch-off point is marked with arrows and labeled, indicating the location where the channel becomes depleted of carriers.
- Voltage differences and threshold voltage ($V_{TH}$) are annotated, showing the relationship between gate-substrate voltage difference and the pinch-off phenomenon.
- The depletion region is highlighted in the second diagram, illustrating the effect of increased drain-source voltage.

Overall, the diagram provides a clear visual representation of how varying the drain-source voltage affects the channel and the onset of pinch-off in a MOSFET, leading to saturation of the drain current.

Figure 2.16 Pinch-off behavior.

With the above observations, we reexamine (2.7) for a saturated device. Since $Q_{d}$ is the density of mobile charge, the integral on the left-hand side of (2.7) must be taken from $x=0$ to $x=L^{\prime}$, where $L^{\prime}$ is the point at which $Q_{d}$ drops to zero (e.g., $x_{2}$ in Fig. 2.16), and that on the right from $V(x)=0$ to $V(x)=V_{G S}-V_{T H}$. As a result,

$$
\begin{equation*}
I_{D}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L^{\prime}}\left(V_{G S}-V_{T H}\right)^{2} \tag{2.13}
\end{equation*}
$$

indicating that $I_{D}$ is relatively independent of $V_{D S}$ if $L^{\prime}$ remains close to $L$. We say the device exhibits a "square-law" behavior. If $I_{D}$ is known, then $V_{G S}$ is obtained as

$$
\begin{equation*}
V_{G S}=\sqrt{\frac{2 I_{D}}{\mu_{n} C_{o x} \frac{W}{L^{\prime}}}}+V_{T H} \tag{2.14}
\end{equation*}
$$

We must emphasize that for the transistor to remain in saturation (as is the case in many analog circuits), the drain-source voltage must be equal to or greater than the overdrive voltage. For this reason, some books write $V_{D, s a t}=V_{G S}-V_{T H}$, where $V_{D, s a t}$ denotes the minimum $V_{D S}$ necessary for operation in saturation. As seen later in this book, if the signal swings at the drain or the gate cause $V_{D S}$ to fall below $V_{G S}-V_{T H}$, then a number of undesirable effects occur. For this reason, the choice of the overdrive and hence $V_{D, s a t}$ translates to a certain voltage "headroom" for the signal swings in the circuit: the larger the $V_{D, s a t}$, the less headroom is available for the signals.

Equations (2.8) and (2.13) represent the "large-signal" behavior of NMOS devices; i.e., they can predict the drain current for arbitrary voltages applied to the gate, source, and drain (but only if the device is on). Since the nonlinear nature of these equations makes the analysis difficult, we often resort to linear approximations ("small-signal" models) so as to develop some understanding of a given circuit. This point becomes clear in Sec. 2.4.3.

For PMOS devices, Eqs. (2.8) and (2.13) are respectively written as

$$
\begin{equation*}
I_{D}=-\mu_{p} C_{o x} \frac{W}{L}\left[\left(V_{G S}-V_{T H}\right) V_{D S}-\frac{1}{2} V_{D S}^{2}\right] \tag{2.15}
\end{equation*}
$$

and

$$
\begin{equation*}
I_{D}=-\frac{1}{2} \mu_{p} C_{o x} \frac{W}{L^{\prime}}\left(V_{G S}-V_{T H}\right)^{2} \tag{2.16}
\end{equation*}
$$

The negative sign appears here because we assume that $I_{D}$ flows from the drain to the source, whereas holes flow in the reverse direction. Note that $V_{G S}, V_{D S}, V_{T H}$, and $V_{G S}-V_{T H}$ are negative for a PMOS transistor that is turned on. Since the mobility of holes is about one-half the mobility of electrons, PMOS devices suffer from lower "current drive" capability.
image_name:Figure 2.17
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1, G: Vb}
name: M2, type: PMOS, ports: {S: VDD, D: S2, G: Vb}
]
extrainfo:The diagram shows two saturated MOSFETs operating as current sources. NMOS M1 is configured to inject current I1 into the ground, while PMOS M2 draws current I2 from VDD. Both transistors are controlled by the bias voltage Vb.

Figure 2.17 Saturated MOSFETs operating as current sources.

With $L$ assumed constant, a saturated MOSFET can be used as a current source connected between the drain and the source (Fig. 2.17), an important component in analog design. Note that the NMOS current source injects current into ground and the PMOS current source draws current from $V_{D D}$. In other words, only one terminal of each current source is "floating." (It is difficult to design a current source that flows between two arbitrary nodes of a circuit.)

#### Example 2.2

On a $V_{D S}-V_{G S}$ plane, show the regions of operation of an NMOS transistor.
image_name:Figure 2.18
description:The graph in Figure 2.18 is a plot on the $V_{DS}-V_{GS}$ plane, which is used to illustrate the regions of operation for an NMOS transistor.

1. **Type of Graph and Function:**
- This is a two-dimensional plot showing the relationship between the drain-source voltage ($V_{DS}$) and the gate-source voltage ($V_{GS}$) for an NMOS transistor.

2. **Axes Labels and Units:**
- The horizontal axis represents the gate-source voltage ($V_{GS}$).
- The vertical axis represents the drain-source voltage ($V_{DS}$).
- Both axes are typically measured in volts.

3. **Overall Behavior and Trends:**
- The graph is divided into three regions based on the lines drawn: Off, Saturation, and Triode.
- The line $V_{DS} = V_{GS} - V_{TH}$ separates the saturation region from the triode region. Above this line, the NMOS transistor operates in the saturation region, whereas below it, the transistor is in the triode region.
- The vertical line at $V_{GS} = V_{TH}$ indicates the threshold voltage. To the left of this line, the transistor is in the 'Off' state.

4. **Key Features and Technical Details:**
- The threshold voltage ($V_{TH}$) is marked on the $V_{GS}$ axis, and it is a critical point where the transistor begins to conduct.
- The line $V_{DS} = V_{GS} - V_{TH}$ is a diagonal line starting from the point $(V_{TH}, 0)$ on the $V_{GS}$ axis and extending upwards.
- The regions are clearly labeled as 'Off', 'Saturation', and 'Triode'.

5. **Annotations and Specific Data Points:**
- The graph is annotated with the regions of operation for clarity.
- The threshold voltage ($V_{TH}$) is a pivotal point on the graph, indicating the onset of conduction.
- The line $V_{DS} = V_{GS} - V_{TH}$ serves as a boundary between the saturation and triode regions.

Figure 2.18 $V_{D S}-V_{G S}$ plane showing regions of operation.

#### Solution

Since the value of $V_{D S}$ with respect to $V_{G S}-V_{T H}$ determines the region of operation, we draw the line $V_{D S}=$ $V_{G S}-V_{T H}$ in the plane, as shown in Fig. 2.18. If $V_{G S}>V_{T H}$, then the region above the line corresponds to saturation, and that below the line corresponds to the triode region. Note that for a given $V_{D S}$, the device eventually leaves saturation as $V_{G S}$ increases. The minimum allowable $V_{D S}$ for operation in saturation is also called $V_{D, s a t}$. It is important to bear in mind that $V_{D, s a t}=V_{G S}-V_{T H}$.

The distinction between saturation and triode regions can be confusing, especially for PMOS devices. Intuitively, we note that the channel is pinched off if the difference between the gate and drain voltages is not sufficient to create an inversion layer. As depicted conceptually in Fig. 2.19, as $V_{G}-V_{D}$ of an NFET drops below $V_{T H}$, pinch-off occurs. Similarly, if $V_{D}-V_{G}$ of a PFET is not large enough ( $<\left|V_{T H P}\right|$ ), the device is saturated. Note that this view does not require knowledge of the source voltage. This means that we must know a priori which terminal operates as the drain. The drain is defined as the terminal with a higher (lower) voltage than the source for an NFET (PFET).
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: s1, D: d1, G: g1}
name: M2, type: PMOS, ports: {S: s1, D: d1, G: g1}
]
extrainfo:The diagram illustrates the transition between saturation and the edge of the triode region for both NMOS and PMOS transistors. It shows the voltage threshold conditions for NMOS (V_THN) and PMOS (|V_THP|) transistors.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: s1, D: d1, G: g1}
name: M2, type: PMOS, ports: {S: s1, D: d1, G: g1}
]
extrainfo:The diagram shows the transition between saturation and the edge of the triode region for both NMOS and PMOS transistors. It illustrates how the gate-source voltage affects the operation of the transistors.

Figure 2.19 Conceptual visualization of saturation and triode regions.

### 2.2.3 MOS Transconductance

Since a MOSFET operating in saturation produces a current in response to its gate-source overdrive voltage, we may define a figure of merit that indicates how well a device converts a voltage to a current. More specifically, since in processing signals, we deal with the changes in voltages and currents, we define the figure of merit as the change in the drain current divided by the change in the gate-source voltage. Called the "transconductance" (and usually defined in the saturation region) and denoted by $g_{m}$, this quantity is expressed as

$$
\begin{align*}
g_{m} & =\left.\frac{\partial I_{D}}{\partial V_{G S}}\right|_{V D S \text { const. }}  \tag{2.17}\\
& =\mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right) \tag{2.18}
\end{align*}
$$

In a sense, $g_{m}$ represents the sensitivity of the device: for a high $g_{m}$, a small change in $V_{G S}$ results in a large change in $I_{D}$. We express $g_{m}$ in $1 / \Omega$ or in siemens (S); e.g., $g_{m}=1 /(100 \Omega)=0.01 \mathrm{~S}$. In analog design, we sometimes say a MOSFET operates as a "transconductor" or a " $V / I$ converter" to indicate that it converts a voltage change to a current change. Interestingly, $g_{m}$ in the saturation region is equal to the inverse of $R_{o n}$ in the deep triode region.

The reader can prove that $g_{m}$ can also be expressed as

$$
\begin{align*}
g_{m} & =\sqrt{2 \mu_{n} C_{o x} \frac{W}{L} I_{D}}  \tag{2.19}\\
& =\frac{2 I_{D}}{V_{G S}-V_{T H}} \tag{2.20}
\end{align*}
$$

Plotted in Fig. 2.20, each of the above expressions proves useful in studying the behavior of $g_{m}$ as a function of one parameter while other parameters remain constant. For example, (2.18) suggests that
image_name:Figure 2.20 Approximate MOS transconductance as a function of overdrive and drain current
description:Figure 2.20 consists of three separate graphs illustrating the behavior of MOS transconductance ($g_{m}$) as a function of overdrive voltage ($V_{GS} - V_{TH}$) and drain current ($I_{D}$) under different conditions.

1. **First Graph (Left):**
- **Type:** Linear plot.
- **Axes:**
- **X-axis:** Overdrive voltage ($V_{GS} - V_{TH}$) with the condition that $W/L$ (width-to-length ratio) is constant.
- **Y-axis:** Transconductance ($g_{m}$).
- **Behavior:** The graph shows a linear increase in $g_{m}$ as the overdrive voltage increases, indicating a direct proportionality when $W/L$ is constant.

2. **Second Graph (Middle):**
- **Type:** Non-linear curve.
- **Axes:**
- **X-axis:** Drain current ($I_{D}$) with the condition that $W/L$ is constant.
- **Y-axis:** Transconductance ($g_{m}$).
- **Behavior:** The graph depicts a curve that starts steep and gradually flattens, suggesting that $g_{m}$ increases with $I_{D}$ but at a decreasing rate as $I_{D}$ becomes larger.

3. **Third Graph (Right):**
- **Type:** Non-linear curve.
- **Axes:**
- **X-axis:** Overdrive voltage ($V_{GS} - V_{TH}$) with the condition that $I_{D}$ is constant.
- **Y-axis:** Transconductance ($g_{m}$).
- **Behavior:** This graph shows a decreasing trend where $g_{m}$ diminishes as the overdrive voltage increases, indicating an inverse relationship under constant $I_{D}$ conditions.

These graphs collectively demonstrate how $g_{m}$ varies with different parameters, highlighting the complex dependencies of transconductance on overdrive voltage and drain current in MOS transistors.

Figure 2.20 Approximate MOS transconductance as a function of overdrive and drain current.
$g_{m}$ increases with the overdrive if $W / L$ is constant, whereas (2.20) implies that $g_{m}$ decreases with the overdrive if $I_{D}$ is constant.

The $I_{D}$ and $V_{G S}-V_{T H}$ terms in the above $g_{m}$ equations are bias values. For example, a transistor with $W / L=5 \mu \mathrm{~m} / 0.1 \mu \mathrm{~m}$ and biased at $I_{D}=0.5 \mathrm{~mA}$ may exhibit a transconductance of $(1 / 200 \Omega)$. If a signal is applied to the device, then $I_{D}$ and $V_{G S}-V_{T H}$ and hence $g_{m}$ vary, but in small-signal analysis, we assume that the signal amplitude is small enough that this variation is negligible.

Equation (2.19) implies that the transconductance can be raised arbitrarily if we increase $W / L$ and keep $I_{D}$ constant. This result is incorrect and will be revised in Sec. 2.3.

The concept of transconductance can also be applied to a device operating in the triode region, as illustrated in the following example.

#### Example 2.3

For the arrangement shown in Fig. 2.21, plot the transconductance as a function of $V_{D S}$.
image_name:Figure 2.21
description:The graph in Figure 2.21 is a plot of transconductance \( g_m \) as a function of the drain-source voltage \( V_{DS} \). This is a typical characteristic curve for a MOSFET device.

1. **Type of Graph and Function**:
- The graph is a characteristic curve showing the relationship between transconductance \( g_m \) and \( V_{DS} \).

2. **Axes Labels and Units**:
- The horizontal axis represents \( V_{DS} \), the drain-source voltage. The units are typically in volts (V).
- The vertical axis represents \( g_m \), the transconductance. The units are typically in siemens (S) or mhos.

3. **Overall Behavior and Trends**:
- The graph shows a piecewise linear behavior.
- For values of \( V_{DS} \) greater than \( V_b - V_{TH} \), the transconductance \( g_m \) remains constant, indicating that the device is in the saturation region.
- As \( V_{DS} \) decreases below \( V_b - V_{TH} \), \( g_m \) decreases linearly, indicating the transition into the triode region.

4. **Key Features and Technical Details**:
- The transition point at \( V_{DS} = V_b - V_{TH} \) is marked by a vertical dashed line, which is a critical point where the behavior of the device changes from saturation to triode region.
- In the saturation region, \( g_m \) is constant, which implies that the current \( I_D \) is relatively constant as well.

5. **Annotations and Specific Data Points**:
- The graph includes a dashed line indicating the threshold voltage \( V_b - V_{TH} \), which is a significant point where the behavior changes.
- No specific numerical values are provided, but the graph qualitatively describes the behavior of \( g_m \) as \( V_{DS} \) varies.

Figure 2.21

#### Solution

It is simpler to study $g_{m}$ as $V_{D S}$ decreases from infinity. So long as $V_{D S} \geq V_{b}-V_{T H}, M_{1}$ is in saturation, $I_{D}$ is relatively constant, and, from (2.19), so is $g_{m}$. If the drain voltage falls below the gate voltage by more than one threshold, $M_{1}$ enters the triode region, and

$$
\begin{align*}
g_{m} & =\frac{\partial}{\partial V_{G S}}\left\{\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left[2\left(V_{G S}-V_{T H}\right) V_{D S}-V_{D S}^{2}\right]\right\}  \tag{2.21}\\
& =\mu_{n} C_{o x} \frac{W}{L} V_{D S} \tag{2.22}
\end{align*}
$$

Thus, as plotted in Fig. 2.21, the transconductance drops in the triode region. For amplification, therefore, we usually employ MOSFETs in saturation.

For a PFET, the transconductance in the saturation region is expressed as $g_{m}=-\mu_{p} C_{o x}(W / L)$ $\left(V_{G S}-V_{T H}\right)=-2 I_{D} /\left(V_{G S}-V_{T H}\right)=\sqrt{2 \mu_{p} C_{o x}(W / L) I_{D}}$.

## 2.3 - Second-Order Effects

Our analysis of the MOS structure has thus far entailed various simplifying assumptions, some of which are not valid in many analog circuits. In this section, we describe three second-order effects that are essential in our subsequent circuit analyses. Other phenomena that appear in nanometer devices are studied in Chapter 17.

Body Effect In the analysis of Fig. 2.10, we tacitly assumed that the bulk and the source of the transistor were tied to ground. What happens if the bulk voltage of an NFET drops below the source voltage (Fig. 2.22)? Since the S and D junctions remain reverse-biased, we surmise that the device continues to operate properly, but some of its characteristics may change. To understand the effect, suppose
image_name:Figure 2.22 NMOS device with negative bulk voltage
description:
[
name: M1, type: NMOS, ports: {S: GND, D: VD, G: VG, B: VB}
]
extrainfo:The diagram shows an NMOS transistor with a negative bulk voltage (VB < 0). The source is connected to ground, the drain is connected to VD, the gate is connected to VG, and the body is connected to a negative voltage VB.

Figure 2.22 NMOS device with negative bulk voltage.
image_name:Figure 2.22 NMOS device with negative bulk voltage
description:The image depicts two cross-sectional diagrams of an NMOS transistor, illustrating the effects of different bulk voltages on the device.

**Identification of Components and Structure:**
- The diagrams show an NMOS transistor structure with key regions labeled:
- **p-substrate:** The base layer of the transistor.
- **n+ regions:** Source and drain regions, heavily doped with n-type material.
- **p+ region:** A heavily doped p-type region, possibly indicating a body or bulk connection.
- **Gate (VG):** Positioned above the channel, separated by an insulating layer.

**Connections and Interactions:**
- The source is connected to ground (GND).
- The drain is connected to a voltage source labeled VD.
- The gate is connected to a voltage source labeled VG.
- The body or bulk connection is shown with two scenarios:
- In the left diagram, the bulk voltage (VB) is zero.
- In the right diagram, the bulk voltage (VB) is negative.

**Labels, Annotations, and Key Features:**
- **Qd:** Represents the depletion charge region under the gate.
- The left diagram shows a smaller depletion region with VB = 0, while the right diagram shows a wider depletion region when VB is negative.
- The diagrams illustrate how a negative bulk voltage increases the depletion region by attracting more holes to the substrate, thereby increasing the negative charge left behind.
- The presence of the gate voltage (VG) is indicated by a voltage source symbol with positive and negative terminals.

Overall, the diagrams provide a visual explanation of how varying the bulk voltage affects the depletion region in an NMOS transistor, which is crucial for understanding its electrical characteristics and behavior.
image_name:Figure 2.23 Variation of depletion region charge with bulk voltage
description:The image depicts two cross-sectional diagrams of an NMOS transistor, illustrating the variation of the depletion region charge with changes in bulk voltage (VB). The diagrams are labeled with key voltages and components to aid understanding.

**Left Diagram (VB = 0):**
1. **Components and Structure:**
- The NMOS transistor is built on a p-type substrate.
- It includes p+ and n+ regions representing the source and drain, respectively.
- A gate is placed above the channel, separated by an insulating layer.

2. **Connections and Interactions:**
- The gate voltage (VG) is applied, but no inversion layer is formed as VG is less than the threshold voltage (VTH).
- The depletion region (Qd) is visible under the gate, indicated by a few negative charges.
- The bulk voltage (VB) is set to 0, indicating no additional charge is attracted to the substrate.

3. **Labels, Annotations, and Key Features:**
- The p-substrate and the n+ source/drain regions are clearly labeled.
- The depletion region is marked as Qd.

**Right Diagram (VB < 0):**
1. **Components and Structure:**
- Similar structure as the left diagram with the same components.

2. **Connections and Interactions:**
- The bulk voltage (VB) is negative, attracting more holes to the substrate connection.
- This results in a wider depletion region (Qd), as indicated by an increased number of negative charges under the gate.
- The gate voltage (VG) remains applied, but still no inversion layer forms since VG is less than VTH.

3. **Labels, Annotations, and Key Features:**
- The diagram clearly shows the effect of a negative bulk voltage on the depletion region width.
- The p-substrate and n+ regions are labeled similarly to the left diagram.

Overall, these diagrams illustrate how the depletion region widens as the bulk voltage becomes more negative, highlighting the impact on the NMOS transistor's electrical characteristics.

Figure 2.23 Variation of depletion region charge with bulk voltage.
$V_{S}=V_{D}=0$, and $V_{G}$ is somewhat less than $V_{T H}$, so that a depletion region is formed under the gate but no inversion layer exists. As $V_{B}$ becomes more negative, more holes are attracted to the substrate connection, leaving a larger negative charge behind; i.e., as depicted in Fig. 2.23, the depletion region becomes wider. Now recall from Eq. (2.1) that the threshold voltage is a function of the total charge in the depletion region because the gate charge must mirror $Q_{d}$ before an inversion layer is formed. Thus, as $V_{B}$ drops and $Q_{d}$ increases, $V_{T H}$ also increases. This phenomenon is called the "body effect" or the "back-gate effect."

It can be proved that with body effect,

$$
\begin{equation*}
V_{T H}=V_{T H 0}+\gamma\left(\sqrt{2 \Phi_{F}+V_{S B}}-\sqrt{\left|2 \Phi_{F}\right|}\right) \tag{2.23}
\end{equation*}
$$

where $V_{T H 0}$ is given by $(2.1), \gamma=\sqrt{2 q \epsilon_{s i} N_{s u b}} / C_{o x}$ denotes the body-effect coefficient, and $V_{S B}$ is the source-bulk potential difference [1]. The value of $\gamma$ typically lies in the range of 0.3 to $0.4 \mathrm{~V}^{1 / 2}$.

#### Example 2.4

In Fig. 2.24(a), plot the drain current if $V_{X}$ varies from $-\infty$ to 0 . Assume $V_{T H 0}=0.3 \mathrm{~V}, \gamma=0.4 \mathrm{~V}^{1 / 2}$, and $2 \Phi_{F}=0.7 \mathrm{~V}$.
image_name:Figure 2.24 (a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: d1, G: g1(1.2V)}
name: d1, type: VoltageSource, value: 2V, ports: {Np: d1, Nn: GND}
]
extrainfo:The circuit consists of an NMOS transistor M1 with the gate connected to a node labeled g1, the drain connected to a node labeled d1, and the source connected to ground. There is a voltage source of 2V connected between node d1 and ground. The voltage Vx is applied to the source-bulk potential of M1.

image_name:(b)
description:The graph is a plot of the drain current \( I_D \) versus the source-bulk potential \( V_X \) for an NMOS transistor. The horizontal axis represents \( V_X \), with values increasing from left to right, and the vertical axis represents \( I_D \), with values increasing upwards.

Axes Labels and Units:
- **Horizontal Axis (\( V_X \))**: This axis is labeled with \( V_X \) and includes a marked point at \( V_{X1} \), which is a negative value, and 0, indicating the threshold for operation.
- **Vertical Axis (\( I_D \))**: This axis is labeled with \( I_D \), representing the drain current.

Overall Behavior and Trends:
- The graph shows an exponential increase in \( I_D \) as \( V_X \) approaches 0 from a negative value.
- For \( V_X < V_{X1} \), the current \( I_D \) is negligible, indicating that the NMOS transistor is off.
- As \( V_X \) increases from \( V_{X1} \) towards 0, \( I_D \) begins to increase sharply, reflecting the transistor turning on.

Key Features and Technical Details:
- The graph starts at a point where \( V_X = V_{X1} \), and \( I_D \) is approximately zero, indicating the cutoff region of the transistor.
- The transition from zero current to a significant increase in \( I_D \) occurs as \( V_X \) approaches 0, which is consistent with the threshold voltage effect described in the provided context.

Annotations and Specific Data Points:
- The graph is annotated with \( V_{X1} \) on the \( V_X \) axis, which is a critical value where the threshold voltage exceeds 1.2 V, turning the device off.
- The point where \( V_X = 0 \) marks the beginning of the region where \( I_D \) increases significantly, indicating the transistor is turning on and conducting current.

Figure 2.24

#### Solution

If $V_{X}$ is sufficiently negative, the threshold voltage of $M_{1}$ exceeds 1.2 V and the device is off. That is,

$$
\begin{equation*}
1.2 \mathrm{~V}=0.3+0.4\left(\sqrt{0.7-V_{X 1}}-\sqrt{0.7}\right) \tag{2.24}
\end{equation*}
$$

and hence $V_{X 1}=-8.83 \mathrm{~V}$. For $V_{X 1}<V_{X}<0, I_{D}$ increases according to

$$
\begin{equation*}
I_{D}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left[V_{G S}-V_{T H 0}-\gamma\left(\sqrt{2 \Phi_{F}-V_{X}}-\sqrt{2 \Phi_{F}}\right)\right]^{2} \tag{2.25}
\end{equation*}
$$

Fig. 2.24(b) shows the resulting behavior.

For body effect to manifest itself, the bulk potential, $V_{\text {sub }}$, need not change: if the source voltage varies with respect to $V_{\text {sub }}$, the same phenomenon occurs. For example, consider the circuit in Fig. 2.25(a), first ignoring body effect. We note that as $V_{\text {in }}$ varies, $V_{\text {out }}$ closely follows the input because the drain current remains equal to $I_{1}$. In fact, we can write

$$
\begin{equation*}
I_{1}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{\text {in }}-V_{\text {out }}-V_{T H}\right)^{2} \tag{2.26}
\end{equation*}
$$

concluding that $V_{\text {in }}-V_{\text {out }}$ is constant if $I_{1}$ is constant [Fig. 2.25(b)].
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: Vout, D: VDD, G: Vin}
name: I1, type: CurrentSource, value: I1, ports: {Np: Vout, Nn: GND}
]
extrainfo:The circuit consists of an NMOS transistor and a current source. The NMOS transistor M1 has its source connected to Vout, drain to VDD, and gate to Vin. The current source I1 flows into Vout and out to ground.

image_name:(b)
description:The graph in Figure 2.25(b) is a time-domain waveform plot depicting the relationship between the input voltage ($V_{in}$) and the output voltage ($V_{out}$) over time. The x-axis represents time ($t$), though no specific units or scales are provided, indicating a qualitative analysis rather than a quantitative one. The y-axis represents voltage, with two distinct lines labeled as $V_{in}$ and $V_{out}$.

Both $V_{in}$ and $V_{out}$ are shown as straight, parallel lines, suggesting a linear relationship between the input and output voltages. The lines are inclined upwards from left to right, indicating that both voltages are increasing over time. The fact that the lines are parallel suggests that the difference between $V_{in}$ and $V_{out}$ remains constant over the observed time period, implying no phase shift or delay between them.

This graph likely illustrates a scenario where the body effect is not present, as indicated by the context, allowing $V_{out}$ to follow $V_{in}$ closely without additional voltage drops or shifts. The absence of any markers, gridlines, or specific numerical values suggests the graph is intended to convey the general behavior of the circuit rather than precise measurements.

image_name:(b)
description:The graph labeled (b) is a time-domain waveform illustrating the behavior of input and output voltages, specifically $V_{in}$ and $V_{out}$, over time. The horizontal axis represents time, denoted as \( t \), while the vertical axis represents voltage levels.

In this graph, $V_{in}$ is depicted as a straight, upward-sloping line, indicating a linear increase in input voltage over time. In contrast, $V_{out}$ follows a similar upward trend but with a noticeable curvature, suggesting that the output voltage increases at a decreasing rate compared to the input voltage. This curvature implies that there is a deviation between $V_{in}$ and $V_{out}$, likely due to some inherent characteristics of the circuit, such as capacitance or resistance, which might cause a lag or attenuation in the output.

There are no specific numerical values or units provided for the axes, emphasizing that the graph is intended to convey the general relationship and behavior between the input and output voltages rather than precise measurements. The absence of gridlines or markers further supports this qualitative analysis.

Overall, the graph shows that while $V_{out}$ attempts to follow $V_{in}$, it does so with some lag or attenuation, possibly due to the absence of the body effect, as described in the context. The output does not exactly mirror the input, indicating some level of distortion or phase shift, albeit without significant body effect interference.

(c)

Figure 2.25 (a) A circuit in which the source-bulk voltage varies with input level; (b) input and output voltages with no body effect; (c) input and output voltages with body effect.

Now suppose that the substrate is tied to ground and body effect is significant. Then, as $V_{i n}$ and hence $V_{\text {out }}$ become more positive, the potential difference between the source and the bulk increases, raising the value of $V_{T H}$. Equation (2.26) implies that $V_{i n}-V_{\text {out }}$ must increase so as to maintain $I_{D}$ constant [Fig. 2.25(c)].

Body effect is usually undesirable. The change in the threshold voltage, e.g., as in Fig. 2.25(a), often complicates the design of analog (and even digital) circuits. Device technologists balance $N_{s u b}$ and $C_{o x}$ to obtain a reasonable value for $\gamma$.

#### Example 2.5

Equation (2.23) suggests that if $V_{S B}$ becomes negative, then $V_{T H}$ decreases. Is this correct?

#### Solution

Yes, it is. If the bulk voltage of an NMOS device rises above its source voltage, $V_{T H}$ falls below $V_{T H 0}$. This observation proves useful in low-voltage design, where the performance of a circuit may suffer due to a high threshold voltage; one can bias the bulk to reduce $V_{T H}$. Unfortunately, this is not straightforward for NFETs because they typically share one substrate, but it can readily be applied to individual PFETs.

Channel-Length Modulation In the analysis of channel pinch-off in Sec. 2.2, we noted that the actual length of the channel gradually decreases as the potential difference between the gate and the drain decreases. In other words, in (2.13), $L^{\prime}$ is in fact a function of $V_{D S}$. This effect is called "channel-length modulation." Writing $L^{\prime}=L-\Delta L$, i.e., $1 / L^{\prime} \approx(1+\Delta L / L) / L$, and assuming a first-order relationship between $\Delta L / L$ and $V_{D S}$, such as $\Delta L / L=\lambda V_{D S}$, we have, in saturation,

$$
\begin{equation*}
I_{D} \approx \frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2}\left(1+\lambda V_{D S}\right) \tag{2.27}
\end{equation*}
$$

where $\lambda$ is the "channel-length modulation coefficient." Illustrated in Fig. 2.26, this phenomenon results in a nonzero slope in the $I_{D} / V_{D S}$ characteristic and hence a nonideal current source between D and S in saturation. The parameter $\lambda$ represents the relative variation in length for a given increment in $V_{D S}$. Thus, for longer channels, $\lambda$ is smaller.
image_name:Figure 2.26
description:The graph in Figure 2.26 is a plot representing the drain current ($I_D$) versus the drain-source voltage ($V_{DS}$) for a MOSFET transistor, illustrating the effect of channel-length modulation in the saturation region.

1. **Type of Graph and Function:**
- This is a characteristic curve graph, commonly used in electronics to show the behavior of transistors.

2. **Axes Labels and Units:**
- The vertical axis represents the drain current ($I_D$), typically measured in amperes (A), though specific units are not provided in the graph.
- The horizontal axis represents the drain-source voltage ($V_{DS}$), typically measured in volts (V).
- Both axes appear to use a linear scale.

3. **Overall Behavior and Trends:**
- The graph shows two curves, each corresponding to a different gate-source voltage ($V_{GS}$). The curve for $V_{GS2}$ is above the curve for $V_{GS1}$, indicating a higher drain current for the higher gate-source voltage.
- Initially, as $V_{DS}$ increases, $I_D$ increases rapidly, indicating the device is in the triode region.
- As $V_{DS}$ continues to increase, the curves begin to flatten, indicating the onset of saturation.
- In the saturation region, the curves exhibit a slight upward slope due to channel-length modulation, deviating from the ideal flat line.

4. **Key Features and Technical Details:**
- The transition from the triode to the saturation region is characterized by a noticeable change in the slope of the $I_D$ versus $V_{DS}$ curves.
- The upward slope in the saturation region is a result of channel-length modulation, where the channel length effectively decreases with increasing $V_{DS}$, leading to an increase in $I_D$.
- The higher $V_{GS}$ value ($V_{GS2}$) results in a higher drain current at any given $V_{DS}$ compared to the lower $V_{GS}$ ($V_{GS1}$).

5. **Annotations and Specific Data Points:**
- The graph includes annotations for two different gate-source voltages, $V_{GS1}$ and $V_{GS2}$, represented by dotted lines extending from the saturation region of each curve.
- No specific numerical values or data points are provided in the graph.

Figure 2.26 Finite saturation region slope resulting from channel-length modulation.

#### Example 2.6

Is there channel-length modulation in the triode region?

#### Solution

No, there is not. In the triode region, the channel continuously stretches from the source to the drain, experiencing no pinch-off. Thus, the drain voltage does not modulate the length of the channel.

The reader may then observe a discontinuity in the equations as the device goes from the triode region to saturation:

$$
\begin{align*}
I_{D, t r i} & =\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left[2\left(V_{G S}-V_{T H}\right) V_{D S}-V_{D S}^{2}\right]  \tag{2.28}\\
I_{D, s a t} & =\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2}\left(1+\lambda V_{D S}\right) \tag{2.29}
\end{align*}
$$

The former yields $(1 / 2) \mu_{n} C_{o x} W / L\left(V_{G S}-V_{T H}\right)^{2}$ at the edge of the triode region, whereas the latter exhibits an additional factor of $1+\lambda V_{D S}$. This discrepancy is removed in more complex models of MOSFETs (Chapter 17).

With channel-length modulation, some of the expressions derived for $g_{m}$ must be modified. Equations (2.18) and (2.19) are respectively rewritten as

$$
\begin{align*}
g_{m} & =\mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)\left(1+\lambda V_{D S}\right)  \tag{2.30}\\
& =\sqrt{2 \mu_{n} C_{o x}(W / L) I_{D}\left(1+\lambda V_{D S}\right)} \tag{2.31}
\end{align*}
$$

while Eq. (2.20) remains unchanged.

#### Nanometer Design Notes

Nanometer transistors suffer from various imperfections and markedly depart from square-law behavior. Shown below are the actual I-V characteristics of an NFET with $W / L=5 \mu \mathrm{~m} / 40 \mathrm{~nm}$ for $V_{G S}=0.3 \mathrm{~V} \cdots 0.8 \mathrm{~V}$. Also plotted are the characteristics of a square-law device of the same dimensions. Despite our best efforts to match the latter device to the former, we still observe significant differences.
image_name:I-V characteristics
description:The graph titled "I-V characteristics" illustrates the drain current ($I_D$) versus the drain-source voltage ($V_{DS}$) for an NFET with dimensions $W / L = 5 \mu m / 40 nm$. The $I_D$ is measured in milliamperes (mA) and is plotted on the vertical axis, while $V_{DS}$ is measured in volts (V) and is plotted on the horizontal axis. The graph uses a linear scale for both axes, with $I_D$ ranging from 0 to 3.5 mA and $V_{DS}$ ranging from 0 to 1 V.

The graph features multiple curves, each representing different gate-source voltages ($V_{GS}$) ranging from 0.3 V to 0.8 V. The curves show the behavior of the NFET under different $V_{GS}$ values. The general trend observed is that as $V_{GS}$ increases, the drain current $I_D$ also increases for a given $V_{DS}$. This is indicative of the transistor entering the saturation region at higher $V_{DS}$ values.

The curves start at the origin (0,0) and rise sharply initially, indicating a rapid increase in current with increasing voltage, which then tapers off, showing a slower rate of increase in current as the device approaches saturation. This behavior deviates from the ideal square-law characteristics, as noted in the context, due to the imperfections in nanometer-scale transistors.

Key features include the initial steep slope of each curve, which becomes more pronounced with higher $V_{GS}$ values, and the eventual flattening of the curves as they approach saturation. These characteristics highlight the non-linear behavior of the device under varying gate-source voltages. The graph is marked with gridlines at regular intervals to aid in reading specific values, though no specific data points are annotated.

#### Example 2.7
Keeping all other parameters constant, plot the $I_{D} / V_{D S}$ characteristic of a MOSFET for $L=L_{1}$ and $L=2 L_{1}$.

#### Solution

Writing

$$
\begin{equation*}
I_{D}=\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2}\left(1+\lambda V_{D S}\right) \tag{2.32}
\end{equation*}
$$

and $\lambda \propto 1 / L$, we note that if the length is doubled, the slope of $I_{D}$ vs. $V_{D S}$ is divided by four because $\partial I_{D} / \partial V_{D S} \propto$ $\lambda / L \propto 1 / L^{2}$ (Fig. 2.27). (This is true only if $V_{G S}-V_{T H}$ is constant.) For a given gate-source overdrive, a larger $L$ gives a more ideal current source while degrading the current capability of the device. Thus, $W$ may need to be increased proportionally. In fact, if we double $W$ to restore $I_{D}$ to its original value, the slope also doubles. In other words, for a required drain current and a given overdrive, doubling the length reduces the slope by a factor of 2 .
image_name:Figure 2.27 Effect of doubling channel length
description:The graph in Figure 2.27 illustrates the effect of doubling the channel length on the drain current ($I_{D}$) versus drain-source voltage ($V_{DS}$) characteristics of a MOSFET. This is a plot with $I_{D}$ on the vertical axis and $V_{DS}$ on the horizontal axis. The axes are not labeled with specific units, but $I_{D}$ is typically measured in amperes (A) and $V_{DS}$ in volts (V).

The graph presents two curves: one for a channel length $L = L_1$ and another for a doubled channel length $L = 2L_1$. Both curves start from the origin, indicating that the drain current is zero when the drain-source voltage is zero.

As $V_{DS}$ increases, both curves initially rise sharply, indicating a rapid increase in drain current. However, the curve for $L = L_1$ rises more steeply than the curve for $L = 2L_1$. This suggests that a shorter channel length allows for a higher rate of increase in current as $V_{DS}$ increases.

As the curves continue, they both begin to flatten, indicating that the current approaches a saturation point where increases in $V_{DS}$ result in smaller increases in $I_{D}$. The $L = L_1$ curve reaches a higher saturation current than the $L = 2L_1$ curve, demonstrating that a longer channel length reduces the drain current for a given $V_{DS}$.

Dotted lines are used to indicate the differences in current levels between the two curves at a given $V_{DS}$, emphasizing the reduction in current capability with increased channel length. This behavior aligns with the discussion in the context provided, which states that doubling the channel length reduces the slope of the $I_{D}$ vs. $V_{DS}$ characteristics, thereby degrading the current capability of the device.

Figure 2.27 Effect of doubling channel length.

The linear approximation $\Delta L / L \propto V_{D S}$ becomes less accurate in short-channel transistors, resulting in a variable slope in the saturated $I_{D} / V_{D S}$ characteristics. We return to this issue in Chapter 17.

The dependence of $I_{D}$ upon $V_{D S}$ in saturation may suggest that the bias current of a MOSFET can be defined by the proper choice of the drain-source voltage, allowing freedom in the choice of $V_{G S}-V_{T H}$. However, since the dependence on $V_{D S}$ is much weaker, the drain-source voltage is not used to set the current. That is, we always consider $V_{G S}-V_{T H}$ as the current-defining parameter. The effect of $V_{D S}$ on $I_{D}$ is usually considered an error, and it is studied in Chapter 5.

Subthreshold Conduction In our analysis of the MOSFET, we have assumed that the device turns off abruptly as $V_{G S}$ drops below $V_{T H}$. In reality, for $V_{G S} \approx V_{T H}$, a "weak" inversion layer still exists and some current flows from D to S . Even for $V_{G S}<V_{T H}, I_{D}$ is finite, but it exhibits an exponential dependence on $V_{G S}[2,3]$. Called "subthreshold conduction," this effect can be formulated for $V_{D S}$ greater than roughly 100 mV as

$$
\begin{equation*}
I_{D}=I_{0} \exp \frac{V_{G S}}{\xi V_{T}} \tag{2.33}
\end{equation*}
$$

where $I_{0}$ is proportional to $W / L, \xi>1$ is a nonideality factor, and $V_{T}=k T / q$. We also say the device operates in "weak inversion." (Similarly, for $V_{G S}>V_{T H}$, we say the device operates in "strong inversion.") Except for $\xi,(2.33)$ is similar to the exponential $I_{C} / V_{B E}$ relationship of a bipolar transistor. The key point here is that as $V_{G S}$ falls below $V_{T H}$, the drain current drops at a finite rate. With typical values of $\xi$, at room temperature $V_{G S}$ must decrease by approximately 80 mV for $I_{D}$ to decrease by one decade (Fig. 2.28). For example, if a threshold of 0.3 V is chosen in a process to allow low-voltage operation, then when $V_{G S}$ is reduced to zero, the drain current decreases by only a factor of $10^{0.3 \mathrm{~V} / 80 \mathrm{mV}}=10^{3.75} \approx 5.62 \times 10^{3}$. For example, if the transistor carries about $1 \mu \mathrm{~A}$ for $V_{G S}=V_{T H}$ and we have 100 million such devices, then
image_name:Figure 2.28 MOS subthreshold characteristics
description:The graph in Figure 2.28 illustrates the subthreshold characteristics of a MOS (Metal-Oxide-Semiconductor) transistor. It is a plot of the logarithm of the drain current (log I_D) versus the gate-source voltage (V_GS).

**Type of Graph and Function:**
- The graph is a semi-logarithmic plot, where the vertical axis is logarithmic and the horizontal axis is linear.

**Axes Labels and Units:**
- The vertical axis represents the logarithm of the drain current (log I_D), measured in decades, indicating exponential changes in current.
- The horizontal axis represents the gate-source voltage (V_GS), measured in volts (V).

**Overall Behavior and Trends:**
- The graph shows two distinct regions of operation for the MOS transistor: the exponential region and the square law region.
- In the subthreshold region (left side of V_TH), the graph exhibits an exponential increase in drain current with increasing V_GS.
- Beyond the threshold voltage (V_TH), the graph transitions into a region where the current follows a square law behavior, indicating a different mode of operation.

**Key Features and Technical Details:**
- The threshold voltage (V_TH) is marked on the horizontal axis, indicating the transition point between the exponential and square law regions.
- The exponential region is characterized by a slope that indicates the current increases by one decade for every 80 mV increase in V_GS.
- The square law region shows a more gradual increase in current, typical of MOS operation above the threshold voltage.

**Annotations and Specific Data Points:**
- The graph is annotated with labels for the exponential and square law regions.
- A dashed line extrapolates the linear behavior in the subthreshold region to emphasize the exponential nature of the current increase below V_TH.
- A vertical dashed line marks the threshold voltage (V_TH), serving as a reference point for the transition between the two regions of operation.

Figure 2.28 MOS subthreshold characteristics.
they draw 18 mA when they are nominally off. Especially problematic in large circuits such as memories, subthreshold conduction can result in significant power dissipation (or loss of analog information).

If a MOS device conducts for $V_{G S}<V_{T H}$, then how do we define the threshold voltage? Indeed, numerous definitions have been proposed. One possibility is to extrapolate, on a logarithmic vertical scale, the weak inversion and strong inversion characteristics and consider their intercept voltage as the threshold (Fig. 2.28).

We now reexamine Eq. (2.19) for the transconductance of a MOS device operating in the subthreshold region. Is it possible to achieve an arbitrarily high transconductance by increasing $W$ while maintaining $I_{D}$ constant? Is it possible to obtain a higher transconductance than that of a bipolar transistor $\left(I_{C} / V_{T}\right)$ biased at the same current? Equation (2.19) was derived from the square-law characteristic $I_{D}=$ $(1 / 2) \mu_{n} C_{o x}(W / L)\left(V_{G S}-V_{T H}\right)^{2}$. However, if $W$ increases while $I_{D}$ remains constant, then $V_{G S} \rightarrow V_{T H}$ and the device enters the subthreshold region. As a result, the transconductance is calculated from (2.33) to be $g_{m}=I_{D} /\left(\xi V_{T}\right)$, revealing that MOSFETs are still inferior to bipolar transistors in this respect.

At what overdrive voltage can we say the transistor goes from strong inversion to weak inversion? While somewhat arbitrary, this transition point can be defined as the overdrive voltage, $\left(V_{G S}-V_{T H}\right)_{1}$, at which the corresponding transconductances would become equal for the same drain current:

$$
\begin{equation*}
\frac{I_{D}}{\xi V_{T}}=\frac{2 I_{D}}{\left(V_{G S}-V_{T H}\right)_{1}} \tag{2.34}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\left(V_{G S}-V_{T H}\right)_{1}=2 \xi V_{T} \tag{2.35}
\end{equation*}
$$

For $\xi \approx 1.5$, this amounts to about 80 mV .
The exponential dependence of $I_{D}$ upon $V_{G S}$ in subthreshold operation may suggest the use of MOS devices in this regime so as to achieve a higher gain. However, since such conditions are met only by a large device width or low drain current, the speed of subthreshold circuits is severely limited.

#### Example 2.8

Examine the behavior of a MOSFET as the drain "current density," $I_{D} / W$, varies.

#### Solution

For a given drain current and device width, how do we determine the region of operation? We must consider the equations for both strong and weak inversion:

$$
\begin{align*}
I_{D} & =\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2}  \tag{2.36}\\
I_{D} & =\alpha \frac{W}{L} \exp \frac{V_{G S}}{\xi V_{T}} \tag{2.37}
\end{align*}
$$

where channel-length modulation is neglected and $I_{0}$ in Eq. (2.33) has been expressed as a proportionality factor, $\alpha$, multiplied by $W / L$. What happens if the device is in strong inversion and we continue to reduce $I_{D}$ while $W / L$ is constant? Can $V_{G S}$ simply approach $V_{T H}$ to yield an arbitrarily small value for $\left(V_{G S}-V_{T H}\right)^{2}$ ? Why does the square-law equation not hold as $V_{G S}$ approaches $V_{T H}$ ?

To answer these questions, we return to the plot of Fig. 2.28 and observe that only currents beyond a certain level can be supported in strong inversion. In other words, for a given current and $W / L$, we must obtain $V_{G S}$ from both the square-law and exponential equations and select the lower value:

$$
\begin{align*}
V_{G S} & =\sqrt{\frac{2 I_{D}}{\mu_{n} C_{o x} W / L}}+V_{T H}  \tag{2.38}\\
V_{G S} & =\xi V_{T} \ln \frac{I_{D}}{\alpha W / L} \tag{2.39}
\end{align*}
$$

If $I_{D}$ remains constant and $W$ increases, $V_{G S}$ falls and the device goes from strong inversion to weak inversion.

Voltage Limitations A MOSFET experiences various undesirable effects if its terminal voltage differences exceed certain limits (if the device is "stressed"). At high gate-source voltages, the gate oxide breaks down irreversibly, damaging the transistor. In short-channel devices, an excessively large drain-source voltage widens the depletion region around the drain so much that it touches that around the source, creating a very large drain current. (This effect is called "punchthrough.") Even without breakdown, MOSFETs' characteristics can change permanently if the terminal voltage differences exceed a specified value. Such effects are described in Chapter 17.

## 2.4 ■ MOS Device Models

### 2.4.1 MOS Device Layout

For the developments in subsequent sections, it is beneficial to have some understanding of the layout of a MOSFET. We describe only a simple view here, deferring the fabrication details and structural subtleties to Chapters 18 and 19.

The layout of a MOSFET is determined by both the electrical properties required of the device in the circuit and the "design rules" imposed by the technology. For example, $W / L$ is chosen to set the transconductance or other circuit parameters while the minimum $L$ is dictated by the process. In addition to the gate, the source and drain areas must be defined properly as well.

Shown in Fig. 2.29 are the "bird's-eye view" and the top view of a MOSFET. The gate polysilicon and the source and drain terminals must be tied to metal (aluminum) wires that serve as interconnects with low resistance and capacitance. To accomplish this, one or more "contact windows" must be opened in each region, filled with metal, and connected to the upper metal wires. Note that the gate poly extends beyond the channel area by some amount to ensure reliable definition of the "edge" of the transistor.

The source and drain junctions play an important role in the performance. To minimize the capacitance of $S$ and $D$, the total area of each junction must be minimized. We see from Fig. 2.29 that one dimension of the junctions is equal to $W$. The other dimension must be large enough to accommodate the contact windows and is specified by the technology design rules. ${ }^{7}$

[^5]image_name:(a)
description:The image consists of two views of a MOS device: a bird's-eye view and a vertical view.

1. **Identification of Components and Structure:**
- **Bird's-eye View (a):** This perspective shows a three-dimensional representation of a MOS transistor. Key components include the gate, which is a raised structure extending over the channel area. The source and drain regions are labeled as 'n+' indicating heavily doped n-type semiconductor material. These regions are positioned on either side of the gate.
- **Vertical View (b):** This is a top-down, two-dimensional schematic of the same structure. The channel area is highlighted, indicating where the gate controls the flow of current between the source and drain. Contact windows are shown as dark squares on the source and drain regions, allowing for electrical connections.

2. **Connections and Interactions:**
- The gate is positioned over the channel area, controlling the current flow between the source and drain regions. The source and drain are connected to external circuits through the contact windows, which are openings in the insulating layer that allow for electrical connections.
- The width of the device is marked as 'W,' which is a critical dimension for determining the current-carrying capability of the transistor.

3. **Labels, Annotations, and Key Features:**
- The labels include 'Gate,' 'n+,' 'Channel Area,' 'Contact Windows,' 'W,' and 'L_drawn.'
- The dimension 'W' is crucial for understanding the size and scale of the device, while 'L_drawn' represents the drawn length of the channel.
- The contact windows are essential features for making electrical connections to the source and drain.

Overall, the image provides a clear visualization of a MOS transistor, highlighting its structural components and the critical dimensions necessary for its operation.
image_name:(b)
description:The image labeled "(b)" provides a top-down view of a MOS (Metal-Oxide-Semiconductor) device layout, specifically focusing on the channel area and contact windows. The layout is a schematic representation that includes several key components:

1. **Channel Area**: The central vertical strip represents the channel area where the transistor action occurs. This is the region between the source and drain where current flows when the transistor is active.

2. **Contact Windows**: These are depicted as small, dark squares on either side of the channel. They represent the areas where electrical contacts are made to the source and drain regions, allowing for electrical connection to the rest of the circuit.

3. **W (Width)**: The width of the device is indicated by the label "W," which is a crucial dimension for determining the current-carrying capability of the transistor.

4. **L_drawn (Drawn Length)**: This is the horizontal dimension of the channel, labeled as "L_drawn," which is the length over which the gate controls the channel.

The layout emphasizes the spatial arrangement of the channel and contact windows, which are critical for minimizing capacitance and ensuring efficient operation of the device. The schematic nature of the diagram suggests it is used for design and analysis purposes in integrated circuit fabrication.

Figure 2.29 Bird's-eye and vertical views of a MOS device.

#### Example 2.9

Draw the layout of the circuit shown in Fig. 2.30(a).
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: C, D: E, G: A}
name: M2, type: NMOS, ports: {S: N, D: C, G: B}
name: M3, type: NMOS, ports: {S: N, D: F, G: C}
]
extrainfo:The circuit consists of three NMOS transistors. M1 and M2 share the drain-source junction at node C, while M2 and M3 share the source-drain junction at node N. The gates of M1, M2, and M3 are connected to nodes A, B, and C respectively. The layout in Fig. 2.30(b) and (c) shows the spatial arrangement and interconnections using aluminum wires.
image_name:(b)
description:The image labeled as Figure 2.30(b) illustrates a simplified layout of three MOS transistors, labeled as $M_1$, $M_2$, and $M_3$. The diagram is a vertical representation showing the alignment of these transistors. Each transistor is represented by a horizontal bar, indicating the gate polysilicon, and is annotated with node labels $E$, $C$, $N$, and $F$ corresponding to their electrical connections.

1. **Identification of Components and Structure:**
- **Transistors:** The layout includes three MOS transistors ($M_1$, $M_2$, and $M_3$) arranged vertically.
- **Nodes:** The nodes $E$, $C$, $N$, and $F$ are marked, representing the shared source/drain connections between the transistors.

2. **Connections and Interactions:**
- The diagram highlights the shared source/drain junctions at nodes $C$ and $N$. Specifically, $M_1$ and $M_2$ share the junction at node $C$, while $M_2$ and $M_3$ share the junction at node $N$.
- There are no visible interconnects or metal layers shown in this layout, focusing primarily on the spatial arrangement of the transistors.

3. **Labels, Annotations, and Key Features:**
- The layout is annotated with the transistor labels ($M_1$, $M_2$, $M_3$) and node labels ($E$, $C$, $N$, $F$).
- The layout is schematic and does not specify material properties or voltage values, focusing on the arrangement of components for design purposes.
image_name:(c)
description:The image labeled "(c)" depicts a detailed layout of a circuit involving three MOS transistors, labeled as M1, M2, and M3. This layout is a physical representation of the schematic shown in the adjacent figures. The layout is designed to illustrate the spatial arrangement of the transistors and their connections.

1. **Identification of Components and Structure:**
- **Transistors:** The layout includes three transistors, M1, M2, and M3, arranged vertically. Each transistor is represented by a rectangular region.
- **Nodes and Connections:** The nodes are labeled as A, B, C, N, E, and F. These nodes correspond to the source, drain, and gate connections of the transistors.
- **Aluminum Wires:** The layout includes aluminum wires used to interconnect the various components. These wires are depicted as lines connecting different nodes.

2. **Connections and Interactions:**
- **Shared Junctions:** M1 and M2 share a source/drain junction at node C, and M2 and M3 share a junction at node N. This is indicated by the physical overlap of the regions corresponding to these nodes.
- **Interconnects:** The gate of M3 is connected via a metal interconnect to the source of M1, which is necessary due to the physical layout constraints.
- **Signal Flow:** The layout shows the path of electrical signals through the transistors, with connections between nodes A, B, C, N, E, and F.

3. **Labels, Annotations, and Key Features:**
- **Labels:** Each node is clearly labeled, and the aluminum wires are annotated to indicate their material.
- **Key Features:** The layout emphasizes the efficient use of space and the minimization of capacitance by sharing junctions between transistors. The use of aluminum wires is highlighted as a key feature for connecting the components.

This layout is crucial for understanding the physical implementation of the circuit, ensuring that the design is optimized for performance and space efficiency in integrated circuit fabrication.

Figure 2.30

#### Solution

Observing that $M_{1}$ and $M_{2}$ share the same $\mathrm{S} / \mathrm{D}$ junctions at node $C$ and $M_{2}$ and $M_{3}$ also do so at node $N$, we surmise that the three transistors can be laid out as shown in Fig. 2.30(b). Connecting the remaining terminals, we obtain the layout in Fig. 2.30(c). Note that the gate polysilicon of $M_{3}$ cannot be directly tied to the source material of $M_{1}$, thus requiring a metal interconnect.

### 2.4.2 MOS Device Capacitances

The basic quadratic I/V relationships derived in the previous section, along with corrections for body effect and channel-length modulation, provide some understanding of the low-frequency behavior of CMOS circuits. In many analog circuits, however, the capacitances associated with the devices must also be taken into account so as to predict the high-frequency behavior as well.

We expect that a capacitance exists between every two of the four terminals of a MOSFET (Fig. 2.31). ${ }^{8}$ Moreover, the value of each of these capacitances may depend on the bias conditions of the transistor.

image_name:Figure 2.31 MOS capacitances
description:
[
name: M1, type: NMOS, ports: {S: S, D: D, G: G}
name: C_GD, type: Capacitor, value: C_GD, ports: {Np: G, Nn: D}
name: C_DB, type: Capacitor, value: C_DB, ports: {Np: D, Nn: B}
name: C_GS, type: Capacitor, value: C_GS, ports: {Np: G, Nn: S}
name: C_SB, type: Capacitor, value: C_SB, ports: {Np: S, Nn: B}
name: C_GB, type: Capacitor, value: C_GB, ports: {Np: G, Nn: B}
]
extrainfo:The diagram illustrates the various capacitances associated with a MOSFET, highlighting the capacitances between each pair of the four terminals: gate, drain, source, and body.
image_name:(a)
description:The image labeled "(a)" provides a detailed schematic representation of MOS device capacitances. It illustrates the cross-sectional view of a MOSFET, focusing on the capacitances between various terminals.

1. **Identification of Components and Structure:**
- The diagram shows a MOSFET with its source (S), drain (D), gate (G), and bulk (B) terminals.
- Several capacitances are labeled, indicating their positions between these terminals: \(C_{GS}\) (gate-source capacitance), \(C_{GD}\) (gate-drain capacitance), \(C_{DB}\) (drain-bulk capacitance), \(C_{SB}\) (source-bulk capacitance), and \(C_{GB}\) (gate-bulk capacitance).
- The cross-sectional view highlights the structure of the MOSFET, including the inversion layer, depletion layer, and the \(n^+\) regions.

2. **Connections and Interactions:**
- The capacitive elements are depicted as parallel lines between the terminals, indicating the potential for charge storage and the influence of these capacitances on the device's behavior.
- The inversion layer and depletion layer are shown to interact with the \(p\)-substrate and \(n^+\) regions, affecting the capacitance values.

3. **Labels, Annotations, and Key Features:**
- The diagram includes annotations for each capacitance \(C_1\) to \(C_6\), which represent different components of the total capacitance seen by the gate.
- The \(L_D\) notation indicates the lateral diffusion length of the \(n^+\) regions.
- The lower part of the diagram provides a simplified representation of the MOSFET structure, with the \(p\)-substrate and \(n^+\) regions clearly marked.

Overall, this diagram serves to explain the distribution and impact of capacitances within a MOSFET, which are crucial for understanding its high-frequency behavior.
image_name:(b)
description:The image labeled as Figure 2.32 (b) illustrates the decomposition of source/drain (S/D) junction capacitance into its components within a MOSFET structure. This diagram is a simplified representation focusing on the capacitance aspects of the junction.

Identification of Components and Structure:
- **n+ Region**: The diagram shows an n+ doped region, which is part of the source or drain of a MOSFET.
- **Capacitance Elements**: The capacitance is divided into two main components:
- **Cj**: This represents the bottom-plate junction capacitance. It is the capacitance between the n+ region and the substrate directly beneath it.
- **Cjsw**: This stands for the sidewall junction capacitance, which is the capacitance along the vertical edges of the n+ region.

Connections and Interactions:
- The diagram does not explicitly show connections or signal flow, as it is focused on illustrating the capacitance components rather than the entire circuit.
- The capacitances (Cj and Cjsw) are crucial for understanding the parasitic effects in the MOSFET, particularly at higher frequencies where these capacitances can affect the performance of the device.

Labels, Annotations, and Key Features:
- **n+**: Indicates the doping type of the region, which is heavily doped with electrons.
- **Cj and Cjsw**: These labels identify the specific capacitance components, crucial for analyzing the electrical characteristics of the MOSFET junction.

This decomposition is important for accurate modeling of the MOSFET's behavior, especially in high-frequency applications, as it helps engineers understand and mitigate parasitic effects that can degrade circuit performance.

Figure 2.32 (a) MOS device capacitances; (b) decomposition of S/D junction capacitance into bottom-plate and sidewall components.

#### Nanometer Design Notes

New generations of CMOS technology incorporate the "FinFET" structure. Unlike the conventional "planar" device, the FinFET extends in the third dimension. As shown below, it consists of an $n^{+}$ wall (resembling a shark's fin) and a gate that wraps around the wall. The transistor carries current from the source to the drain on the surfaces of the fin. Owing to the tight confinement of the electric field between the two vertical walls of the gate, the FinFET exhibits less channel-length modulation and subthreshold leakage. But where do the S/D contacts land? What other issues do we face in FinFETs? We return to these questions later in this book.
image_name:Fig. 2.32(a)
description:The image labeled as Fig. 2.32(a) depicts the structural diagram of a FinFET (Fin Field-Effect Transistor). It features several key components and characteristics:

1. **Components and Structure:**
- **n+ Fin:** The central element of the diagram is the n+ doped fin, which resembles a shark's fin. This fin acts as the channel through which current flows from the source (S) to the drain (D).
- **Gate (G):** The gate is shown wrapping around the fin, providing a three-dimensional control over the channel. This wrap-around gate is a defining feature of the FinFET architecture, allowing for better electrostatic control compared to planar transistors.
- **Oxide Layer:** An oxide layer is present between the gate and the fin, serving as the gate dielectric. This layer is crucial for the gate's ability to control the channel.
- **Source (S) and Drain (D):** These are the regions where current enters and exits the fin, respectively. They are marked on the diagram as n+ regions on either side of the fin.
- **Substrate:** The entire structure is built on a substrate, which is indicated at the base of the diagram.

2. **Connections and Interactions:**
- The current flows vertically along the surfaces of the fin from the source to the drain. The gate's electric field controls this flow, modulating the channel conductivity.
- The tight confinement of the electric field between the vertical walls of the gate reduces channel-length modulation and subthreshold leakage, enhancing the performance of the FinFET.

3. **Labels, Annotations, and Key Features:**
- The diagram includes labels such as 'S/D Fin', 'Oxide', 'n+', 'G', 'S', 'D', and 'Substrate', which help in identifying the components and understanding their roles.
- The S/D Fin label indicates the combined source/drain fin structure, while the annotations n+ denote heavily doped regions essential for the creation of source and drain contacts.

Overall, the diagram effectively illustrates the unique three-dimensional structure of the FinFET, highlighting its components and operational principles.

Considering the physical structure in Fig. 2.32(a), we identify the following: (1) the oxide capacitance between the gate and the channel, $C_{1}=W L C_{o x}$; (2) the depletion capacitance between the channel and the substrate, $C_{2}=$ $W L \sqrt{q \epsilon_{s i} N_{s u b} /\left(4 \Phi_{F}\right)}$; and (3) the capacitance due to the overlap of the gate poly with the source and drain areas, $C_{3}$ and $C_{4}$. Owing to fringing electric field lines, $C_{3}$ and $C_{4}$ cannot be simply written as $W L_{D} C_{o x}$, and are usually obtained by more elaborate calculations. The overlap capacitance per unit width is denoted by $C_{o v}$ and expressed in $\mathrm{F} / \mathrm{m}$ (or $\mathrm{fF} / \mu \mathrm{m}$ ). We simply multiply $C_{o v}$ by $W$ to find the gate-source and gate-drain overlap capacitances. (4) The junction capacitance between the source/drain areas and the substrate. As shown in Fig. 2.32(b), this last capacitance is decomposed into two components: the bottom-plate capacitance associated with the bottom of the junction, $C_{j}$, and the sidewall capacitance due to the perimeter of the junction, $C_{j s w}$. The distinction is necessary because different transistor geometries yield different area and perimeter values for the S/D junctions. We specify $C_{j}$ and $C_{j s w}$ as capacitance per unit area (in $\mathrm{F} / \mathrm{m}^{2}$ ) and unit length (in $\mathrm{F} / \mathrm{m}$ ), respectively. Thus, $C_{j}$ is multiplied by the S/D area, and $C_{j s w}$ by the S/D perimeter. Note that each junction capacitance can be expressed as $C_{j}=C_{j 0} /\left[1+V_{R} /\left(\Phi_{B}\right)\right]^{m}$, where $V_{R}$ is the reverse voltage across the junction, $\Phi_{B}$ is the junction built-in potential, and $m$ is a power typically in the range of 0.3 and 0.4 .

#### Example 2.10

Calculate the source and drain junction capacitances of the two structures shown in Fig. 2.33.
image_name:Fig. 2.33(a)
description:The image labeled "Fig. 2.33(a)" depicts a schematic diagram of a transistor layout. This layout shows a top-down view of the transistor structure with the following components and features:

1. **Components and Structure:**
- The diagram illustrates a rectangular layout with a central vertical strip representing the gate region.
- To the left and right of this central strip are shaded areas indicating the source and drain regions.
- The width of the transistor is labeled as 'W', and the extension of the gate over the source or drain is labeled as 'E'.

2. **Connections and Interactions:**
- The source and drain terminals are positioned on opposite ends of the structure. The source terminal is at the bottom, while the drain terminal is at the top.
- The diagram suggests a direct path for current flow between the source and drain through the gate-controlled channel.

3. **Labels, Annotations, and Key Features:**
- The layout includes annotations for the dimensions 'W' and 'E', indicating the width of the transistor and the overlap of the gate, respectively.
- The schematic representation at the bottom left corner shows a simplified symbol of the transistor with three terminals, representing the source, drain, and gate.

This layout is typical for a planar MOSFET, where the gate length is determined by the vertical dimension in the diagram, and the gate width is the horizontal dimension. The overlap 'E' is crucial for calculating the junction capacitances as specified in the context.
image_name:Fig. 2.33(b)
description:
[
name: M1, type: NMOS, ports: {S: s1s2, D: d1d2, G: g1g2}
name: M2, type: NMOS, ports: {S: s1s2, D: d1d2, G: g1g2}
]
extrainfo:The circuit shown in Fig. 2.33(b) is a folded NMOS structure with shared source and gate nodes between two transistors M1 and M2. The source terminals are connected to node s1s2, the drain terminals are connected to node d1d2, and the gate terminals are connected to node g1g2.

#### Solution

For the transistor in Fig. 2.33(a), we have

$$
\begin{equation*}
C_{D B}=C_{S B}=W E C_{j}+2(W+E) C_{j s w} \tag{2.40}
\end{equation*}
$$

whereas for that in Fig. 2.33(b),

$$
\begin{align*}
C_{D B} & =\frac{W}{2} E C_{j}+2\left(\frac{W}{2}+E\right) C_{j s w}  \tag{2.41}\\
C_{S B} & =2\left[\frac{W}{2} E C_{j}+2\left(\frac{W}{2}+E\right) C_{j s w}\right]  \tag{2.42}\\
& =W E C_{j}+2(W+2 E) C_{j s w} \tag{2.43}
\end{align*}
$$

Called a "folded" structure, the geometry in Fig. 2.33(b) exhibits substantially less drain junction capacitance than that in Fig. 2.33(a) while providing the same $W / L$.

In the above calculations, we have assumed that the total source or drain perimeter, $2(W+E)$, is multiplied by $C_{j s w}$. In reality, the capacitance of the inner sidewall (under the gate) may be different from that of the other sidewalls. ${ }^{9}$ Nonetheless, we typically assume that all four sides have the same $C_{j s w}$. The error resulting from this assumption is negligible because each node in a circuit is connected to a number of other device capacitances as well.

We now derive the capacitances between terminals of a MOSFET in different regions of operation. If the device is off, $C_{G D}=C_{G S}=C_{o v} W$, and the gate-bulk capacitance consists of the series combination of the gate-oxide capacitance and the depletion-region capacitance [Fig. 2.32(a)], i.e., $C_{G B}=\left(W L C_{o x}\right) C_{d} /\left(W L C_{o x}+C_{d}\right)$, where $L$ is the effective length, $C_{d}=W L \sqrt{q \epsilon_{s i} N_{s u b} /\left(4 \Phi_{F}\right)}$, and

[^7]$\epsilon_{s i}=\epsilon_{r, s i} \times \epsilon_{0}=11.8 \times\left(8.85 \times 10^{-14}\right) \mathrm{F} / \mathrm{cm}$. The value of $C_{S B}$ and $C_{D B}$ is a function of the source and drain voltages with respect to the substrate.

If the device is in the deep triode region, i.e., if $S$ and $D$ have approximately equal voltages, then the gate-channel capacitance, $W L C_{o x}$, is divided equally between the gate and source terminals and the gate and drain terminals (Fig. 2.34). This is because a change of $\Delta V$ in the gate voltage draws equal amounts of charge from S and D . Thus, $C_{G D}=C_{G S}=W L C_{o x} / 2+W C_{o v}$.
image_name:Figure 2.34 Variation of gate-source and gate-drain capacitances versus V_GS
description:
[
name: M1, type: NMOS, ports: {S: GND, D: VD, G: VG}
name: VG, type: VoltageSource, value: VG, ports: {Np: VG, Nn: GND}
]
extrainfo:The circuit includes an NMOS transistor M1 and a voltage source VG. The graph shows the variation of gate-source (C_GS) and gate-drain (C_GD) capacitances with respect to V_GS, indicating different regions: off, saturation, and triode.
image_name:Figure 2.34 Variation of gate-source and gate-drain capacitances versus V_GS
description:The graph in Figure 2.34 illustrates the variation of gate-source capacitance ($C_{GS}$) and gate-drain capacitance ($C_{GD}$) as functions of the gate-source voltage ($V_{GS}$).

**Type of Graph and Function:**
- This is a plot showing capacitance versus gate-source voltage, a common type of graph used in semiconductor device analysis to depict how capacitance values change with varying $V_{GS}$.

**Axes Labels and Units:**
- The x-axis represents the gate-source voltage, $V_{GS}$, with no specific units marked but typically measured in volts.
- The y-axis represents the capacitance values, with no specific units marked, but typically measured in farads.
- The graph uses a linear scale for both axes.

**Overall Behavior and Trends:**
- As $V_{GS}$ increases from 0, the graph shows an initial constant level of capacitance at $W C_{ov}$ when the device is in the "Off" state.
- Upon reaching the threshold voltage $V_{TH}$, $C_{GS}$ begins to increase sharply, indicating the onset of conduction.
- As $V_{GS}$ continues to increase, the capacitance reaches a saturation level at $\frac{2}{3} W L C_{ox} + W C_{ov}$.
- Beyond this point, as $V_{GS}$ approaches $V_D + V_{TH}$, the capacitance transitions to the triode region, stabilizing at $\frac{W L C_{ox}}{2} + W C_{ov}$.

**Key Features and Technical Details:**
- The graph identifies three distinct regions: "Off," "Saturation," and "Triode."
- The transition between these regions is marked by significant changes in capacitance.
- The saturation region shows a plateau, indicating a stable capacitance value over a range of $V_{GS}$ values.

**Annotations and Specific Data Points:**
- The graph is annotated with key capacitance values at different operating regions:
- Off region: $W C_{ov}$
- Saturation region: $\frac{2}{3} W L C_{ox} + W C_{ov}$
- Triode region: $\frac{W L C_{ox}}{2} + W C_{ov}$
- Vertical dashed lines indicate the transition points at $V_{TH}$ and $V_D + V_{TH}$.

This graph effectively shows how the capacitance between the gate-source and gate-drain changes with the gate-source voltage, highlighting the behavior of the device in different operational regions.

Figure 2.34 Variation of gate-source and gate-drain capacitances versus $V_{G S}$.

Let us now consider $C_{G D}$ and $C_{G S}$. If in saturation, a MOSFET exhibits a gate-drain capacitance roughly equal to $W C_{o v}$. As for $C_{G S}$, we note that the potential difference between the gate and the channel varies from $V_{G S}$ at the source to $V_{T H}$ at the pinch-off point, resulting in a nonuniform vertical electric field in the gate oxide as we travel from the source to the drain. It can be proved that the equivalent capacitance of this structure, excluding the gate-source overlap capacitance, equals (2/3)WLC $C_{o x}$ [1]. Thus, $C_{G S}=2 W L_{e f f} C_{o x} / 3+W C_{o v}$. The behavior of $C_{G D}$ and $C_{G S}$ in different regions of operation is plotted in Fig. 2.34. Note that the above equations do not provide a smooth transition from one region of operation to another, creating convergence difficulties in simulation programs. This issue is revisited in Chapter 17.

The gate-bulk capacitance is usually neglected in the triode and saturation regions because the inversion layer acts as a "shield" between the gate and the bulk. In other words, if the gate voltage varies, the charge is supplied by the source and the drain rather than the bulk.

Example 2.11
Sketch the capacitances of $M_{1}$ in Fig. 2.35 as $V_{X}$ varies from zero to 3 V . Assume that $V_{T H}=0.3 \mathrm{~V}$ and $\lambda=\gamma=0$.
image_name:Figure 2.35
description:
[
name: M1, type: NMOS, ports: {S: F, D: N, G: E}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: F, Nn: GND}
]
extrainfo:The circuit consists of an NMOS transistor M1 with its source connected to node F, drain to node N, and gate to node E. A voltage source Vx is connected between node F and ground.

Figure 2.35

#### Solution

To avoid confusion, we label the three terminals as shown in Fig. 2.35 and denote the bulk by $B$. For $V_{X} \approx 0, M_{1}$ is in the triode region, $C_{E N} \approx C_{E F}=(1 / 2) W L C_{o x}+W C_{o v}$, and $C_{F B}$ is maximum. The value of $C_{N B}$ is independent of $V_{X}$. As $V_{X}$ exceeds 1 V , the role of the source and drain is exchanged [Fig. 2.36(a)], eventually bringing $M_{1}$ out of the triode region for $V_{X} \geq 2 \mathrm{~V}-0.3 \mathrm{~V}$. The variation of the capacitances is plotted in Figs. 2.36(b) and (c).
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: N, D: F, G: E}
name: Vx, type: VoltageSource, value: Vx, ports: {Np: F, Nn: GND}
]
extrainfo:The circuit involves an NMOS transistor M1 with the source connected to node N, the drain to node F, and the gate to node E. A voltage source Vx is connected between node F and ground.
image_name:(b)
description:The graph labeled "(b)" is a plot of capacitance values versus voltage, specifically the voltage $V_X$ in volts (V). The y-axis represents capacitance, with specific capacitance values labeled as $C_{EN}$ and $C_{EF}$. The x-axis represents the voltage $V_X$ in volts (V).

1. **Type of Graph and Function:**
- The graph is a plot showing the relationship between voltage and capacitance in a MOSFET circuit.

2. **Axes Labels and Units:**
- The x-axis is labeled as $V_X$ (V), representing the voltage across the MOSFET.
- The y-axis represents capacitance, with specific values shown for $C_{EN}$ and $C_{EF}$.

3. **Overall Behavior and Trends:**
- As $V_X$ increases, the capacitance values change significantly around $V_X = 1.7$ V.
- The graph shows two distinct capacitance values: $C_{EN}$ and $C_{EF}$, which diverge as $V_X$ approaches 1.7 V.
- For values of $V_X$ less than 1.7 V, $C_{EN}$ and $C_{EF}$ are close, but as $V_X$ exceeds 1.7 V, they separate, with $C_{EN}$ increasing and $C_{EF}$ decreasing.

4. **Key Features and Technical Details:**
- The graph indicates a critical voltage point at $V_X = 1.7$ V where the capacitance values diverge.
- At low $V_X$, $C_{EN}$ and $C_{EF}$ are approximately equal, but as $V_X$ increases, $C_{EN}$ approaches $\frac{2}{3} WLC_{ox} + WC_{ov}$ and $C_{EF}$ approaches $\frac{1}{2} WLC_{ox} + WC_{ov}$.

5. **Annotations and Specific Data Points:**
- The graph includes horizontal lines indicating the asymptotic capacitance values for $C_{EN}$ and $C_{EF}$ as $V_X$ increases beyond 1.7 V.
image_name:(c)
description:The graph labeled (c) in Figure 2.36 is a plot of capacitance versus voltage, specifically illustrating the behavior of the capacitances \( C_{FB} \) and \( C_{NB} \) as a function of \( V_X \), the voltage on the x-axis.

1. **Type of Graph and Function:**
- The graph is a capacitance-voltage plot, showing how different capacitances vary with the applied voltage \( V_X \).

2. **Axes Labels and Units:**
- The x-axis represents \( V_X \), the voltage, in volts (V).
- The y-axis represents capacitance, although the units are not explicitly labeled, it's implied to be in farads (F) or a subunit thereof.
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The graph shows two capacitance curves: \( C_{FB} \) and \( C_{NB} \).
- \( C_{FB} \) starts at a higher value when \( V_X \) is approximately 0 V and decreases as \( V_X \) increases.
- \( C_{NB} \) remains constant as \( V_X \) increases, indicating its independence from \( V_X \).

4. **Key Features and Technical Details:**
- \( C_{FB} \) has a negative slope, indicating a decrease with increasing \( V_X \).
- \( C_{NB} \) is plotted as a constant line, showing no variation with \( V_X \).
- A specific point is marked at \( V_X = 1.0 \) V for \( C_{NB} \), highlighting its value.

5. **Annotations and Specific Data Points:**
- The graph has a vertical dashed line at \( V_X = 1.0 \) V, emphasizing the point where \( C_{NB} \) is marked.
- No specific numerical values are provided for the capacitances, but the general trend and behavior are clearly depicted.

Figure 2.36

### 2.4.3 MOS Small-Signal Model

The quadratic characteristics described by (2.8) and (2.9) along with the voltage-dependent capacitances derived above form the large-signal model of MOSFETs. Such a model proves essential in analyzing circuits in which the signal significantly disturbs the bias points, particularly if nonlinear effects are of concern. By contrast, if the perturbation in bias conditions is small, a "small-signal" model, i.e., an approximation of the large-signal model around the operating point, can be employed to simplify the calculations. Since in many analog circuits, MOSFETs are biased in the saturation region, we derive the corresponding small-signal model here. For transistors operating as switches, a linear resistor given by (2.11) together with device capacitances serves as a rough small-signal equivalent.

We derive the small-signal model by producing a small increment in one bias parameter and calculating the resulting increment in other bias parameters. Specifically, we (1) apply certain bias voltages to the terminals of the device, (2) increment the potential difference between two of the terminals while other terminal voltages remain constant, and (3) measure the resulting change in all terminal currents. If we change the voltage between two terminals by $\Delta V$ and measure a current change of $\Delta I$ in some branch, we can model the effect by a voltage-dependent current source. Let us apply a change to the gate-source voltage, $\Delta V=V_{G S}$, where $V_{G S}$ is a small-signal quantity. ${ }^{10}$ The drain current therefore changes by $g_{m} V_{G S}$ and is modeled by a voltage-dependent current source tied between the drain and source terminals [Fig. 2.37(a)]. The gate current is very small and its change is negligible, thus requiring no representation here. The result is the small-signal model of an ideal MOSFET-the model that an analog designer applies to most devices in a circuit at first glance.

Owing to channel-length modulation, the drain current also varies with the drain-source voltage. This effect can be modeled by a voltage-dependent current source [Fig. 2.37(b)], but a current source whose value linearly depends on the voltage across it is equivalent to a linear resistor [Fig. 2.37(c)] (why?). Tied between D and S , the resistor is given by

$$
\begin{align*}
r_{O} & =\frac{\partial V_{D S}}{\partial I_{D}}  \tag{2.44}\\
& =\frac{1}{\partial I_{D} / \partial V_{D S}}  \tag{2.45}\\
& =\frac{1}{\frac{1}{2} \mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)^{2} \cdot \lambda} \tag{2.46}
\end{align*}
$$

image_name:(a)
description:
[
name: gmVGS, type: VoltageControlledCurrentSource, value: gmVGS, ports: {Np: D, Nn: S}
]
extrainfo:This circuit diagram (a) represents a basic MOS small-signal model with a voltage-controlled current source 'gmVGS' connected between nodes D and S. The gate node is labeled as G, and the source node is labeled as S.
image_name:(b)
description:
[
name: gmVGS, type: VoltageControlledCurrentSource, ports: {Np: D, Nn: S}
name: αVDS, type: VoltageControlledCurrentSource, ports: {Np: D, Nn: S}
]
extrainfo:The circuit diagram (b) represents a MOS small-signal model with channel-length modulation depicted by a dependent current source. It includes two voltage-controlled current sources, gmVGS and αVDS, both connected between nodes D and S.
image_name:(c)
description:
[
name: gmVGS, type: VoltageControlledCurrentSource, ports: {Np: D, Nn: S}
name: ro, type: Resistor, value: ro, ports: {N1: D, N2: S}
]
extrainfo:The circuit diagram (c) represents a MOS small-signal model with channel-length modulation depicted as a resistor ro in parallel with the current source gmVGS.
image_name:(d)
description:
[
name: gmVgs, type: VoltageControlledCurrentSource, value: gmVgs, ports: {Np: D, Nn: S}
name: ro, type: Resistor, value: ro, ports: {N1: D, N2: S}
name: gmbVbs, type: VoltageControlledCurrentSource, value: gmbVbs, ports: {Np: D, Nn: S}
]
extrainfo:The circuit diagram (d) represents a small-signal model for a MOS transistor with body effect, including a voltage-controlled current source gmVgs between nodes D and S, a resistor ro also between nodes D and S, and another voltage-controlled current source gmbVbs between nodes D and S, affected by VBS.

Figure 2.37 (a) Basic MOS small-signal model; (b) channel-length modulation represented by a dependent current source; (c) channel-length modulation represented by a resistor; (d) body effect represented by a dependent current source.

$$
\begin{align*}
& \approx \frac{1+\lambda V_{D S}}{\lambda I_{D}}  \tag{2.47}\\
& \approx \frac{1}{\lambda I_{D}} \tag{2.48}
\end{align*}
$$

where it is assumed that $\lambda V_{D S} \ll 1$. As seen throughout this book, the output resistance, $r_{O}$, affects the performance of many analog circuits. For example, $r_{O}$ limits the maximum voltage gain of most amplifiers.

Now recall that the bulk potential influences the threshold voltage and hence the gate-source overdrive. As demonstrated in Example 2.3, with all other terminals held at a constant voltage, the drain current is a function of the bulk voltage. That is, the bulk behaves as a second gate. Modeling this dependence by a current source connected between D and S [Fig. 2.37(d)], we write the value as $g_{m b} V_{b s}$, where $g_{m b}=\partial I_{D} / \partial V_{B S}$. In the saturation region, $g_{m b}$ can be expressed as

$$
\begin{align*}
g_{m b} & =\frac{\partial I_{D}}{\partial V_{B S}}  \tag{2.49}\\
& =\mu_{n} C_{o x} \frac{W}{L}\left(V_{G S}-V_{T H}\right)\left(-\frac{\partial V_{T H}}{\partial V_{B S}}\right) \tag{2.50}
\end{align*}
$$

We also have

$$
\begin{align*}
\frac{\partial V_{T H}}{\partial V_{B S}} & =-\frac{\partial V_{T H}}{\partial V_{S B}}  \tag{2.51}\\
& =-\frac{\gamma}{2}\left(2 \Phi_{F}+V_{S B}\right)^{-1 / 2} \tag{2.52}
\end{align*}
$$

Thus,

$$
\begin{align*}
g_{m b} & =g_{m} \frac{\gamma}{2 \sqrt{2 \Phi_{F}+V_{S B}}}  \tag{2.53}\\
& =\eta g_{m} \tag{2.54}
\end{align*}
$$

where $\eta=g_{m b} / g_{m}$ and is typically around 0.25 . As expected, $g_{m b}$ is proportional to $\gamma$. Equation (2.53) also suggests that the incremental body effect becomes less pronounced as $V_{S B}$ increases. Note that $g_{m} V_{G S}$ and $g_{m b} V_{B S}$ have the same polarity, i.e., raising the gate voltage has the same effect as raising the bulk potential.

The model in Fig. 2.37(d) is adequate for most low-frequency small-signal analyses. In reality, each terminal of a MOSFET exhibits a finite ohmic resistance resulting from the resistivity of the material (and the contacts), but proper layout can minimize such resistances. For example, consider the two structures of Fig. 2.33, repeated in Fig. 2.38 along with the gate distributed resistance. We note that folding reduces the gate resistance by a factor of four.
image_name:(a)
description:The image labeled '(a)' shows a schematic representation of a MOSFET structure and its equivalent circuit model. On the left side of the image, there is a physical layout diagram of a MOSFET, which includes a gate represented by a vertical line with a series of resistors symbolizing the distributed gate resistance. The gate width is indicated as 'W'. Adjacent to the gate, there are shaded regions representing the source and drain contacts.

Below this layout, there is an equivalent circuit diagram. The circuit includes a MOSFET labeled 'M1', with its gate connected to a node labeled 'X1'. The gate resistance is denoted as 'RG', and it is connected in series with the gate terminal of the transistor. The source terminal is labeled 's1', and the drain terminal is labeled 'd1'. The transconductance of the MOSFET is indicated by 'g1'.

The right side of the image shows a folded MOSFET structure, which effectively reduces the gate resistance by splitting it into two parallel paths. The width of each path is labeled as 'W/2'. The equivalent circuit for this folded structure shows two MOSFETs labeled 'M1' and 'M2', each with its gate resistance labeled as 'RG/2'. The gates of 'M1' and 'M2' are connected to the same node 'X1', and their sources and drains are labeled 's1/s2' and 'd1/d2', respectively. The transconductance for each MOSFET is labeled as 'g1' and 'g2'. This configuration demonstrates how folding the MOSFET reduces the overall gate resistance by distributing it across multiple paths, thus improving the performance of the device.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: s1s2, D: d1d2, G: g1}
name: M2, type: NMOS, ports: {S: s1s2, D: d1d2, G: g2}
name: RG, type: Resistor, value: RG/2, ports: {N1: g1, N2: X1}
name: RG/2, type: Resistor, value: RG/2, ports: {N1: g2, N2: X1}
]
extrainfo:The circuit diagram (b) shows two NMOS transistors, M1 and M2, with shared source and drain nodes (s1s2 and d1d2). The gate of M1 is connected to node g1, and the gate of M2 is connected to node g2. There are two resistors, each with a value of RG/2, connecting g1 and g2 to node X1.

Figure 2.38 Reduction of gate resistance by folding.

Shown in Fig. 2.39, the complete small-signal model includes the device capacitances as well. The value of each capacitance is calculated according to the equations derived in Sec. 2.4.2. The reader may wonder how a complex circuit is analyzed intuitively if each transistor must be replaced by the model of Fig. 2.39. The first step is to determine the simplest device model that can represent the role of each transistor with reasonable accuracy. We provide some guidelines for this task at the end of Chapter 3.
image_name:Figure 2.39
description:
[
name: C_GS, type: Capacitor, value: C_GS, ports: {Np: G, Nn: S}
name: C_GB, type: Capacitor, value: C_GB, ports: {Np: G, Nn: B}
name: C_GD, type: Capacitor, value: C_GD, ports: {Np: G, Nn: D}
name: g_mV_GS, type: VoltageControlledCurrentSource, ports: {Np: D, Nn: S}
name: r_o, type: Resistor, value: r_o, ports: {N1: D, N2: S}
name: g_mbV_BS, type: VoltageControlledCurrentSource, ports: {Np: D, Nn: S}
name: C_SB, type: Capacitor, value: C_SB, ports: {Np: S, Nn: B}
name: C_DB, type: Capacitor, value: C_DB, ports: {Np: D, Nn: B}
]
extrainfo:This is a complete small-signal model of a MOS transistor, including device capacitances and controlled sources. The model represents the transistor's behavior in terms of its gate, source, drain, and body terminals.

Example 2.12
Sketch $g_{m}$ and $g_{m b}$ of $M_{1}$ in Fig. 2.40 as a function of the bias current $I_{1}$.

#### Solution

Since $g_{m}=\sqrt{2 \mu_{n} C_{o x}(W / L) I_{D}}$, we have $g_{m} \propto \sqrt{I_{1}}$. The dependence of $g_{m b}$ upon $I_{1}$ is less straightforward. As $I_{1}$ increases, $V_{X}$ decreases, and so does $V_{S B}$.
image_name:Figure 2.40
description:
[
name: M1, type: NMOS, ports: {S: X, D: VDD, G: VDD}
name: I1, type: CurrentSource, value: I1, ports: {Np: X, Nn: GND}
]
extrainfo:The circuit contains an NMOS transistor M1 connected with its source at node X, drain at VDD, and gate at VDD. A capacitor b1 is connected between VDD and node X. A current source I1 flows into node X and out to ground.

image_name:(b)
description:The graph in question is a plot with two curves labeled \( g_m \) and \( g_{mb} \). It represents the relationship between the transconductance parameters and the current \( I_1 \). The x-axis is labeled \( I_1 \), indicating the current, while the y-axis is unlabeled but represents the transconductance values \( g_m \) and \( g_{mb} \).

1. **Type of Graph and Function:**
- This is a plot showing the variation of transconductance parameters with respect to the current \( I_1 \).

2. **Axes Labels and Units:**
- The x-axis is labeled \( I_1 \), likely representing the current in amperes.
- The y-axis is not labeled with specific units but is understood to represent transconductance values.

3. **Overall Behavior and Trends:**
- Both \( g_m \) and \( g_{mb} \) curves start from the origin and increase as \( I_1 \) increases.
- The curve for \( g_m \) is above the curve for \( g_{mb} \), indicating that \( g_m \) is generally higher than \( g_{mb} \) for the same \( I_1 \) value.
- The curves exhibit a non-linear increase, suggesting that the relationship between \( I_1 \) and these transconductance values is not linear.

4. **Key Features and Technical Details:**
- There are no specific numerical values or markers provided on the graph.
- The graph suggests that as \( I_1 \) increases, both \( g_m \) and \( g_{mb} \) continue to rise, with \( g_m \) consistently higher.

5. **Annotations and Specific Data Points:**
- The graph is annotated with the labels \( g_m \) and \( g_{mb} \) to distinguish the two curves.
- No specific data points, numerical values, or additional annotations are present.

(b)

Figure 2.40

PMOS Small-Signal Model The derivation of the small-signal model seeks changes in the terminal currents due to changes in the terminal voltage differences. As such, this derivation yields exactly the same model for PMOS devices as for NMOS devices. For example, consider the arrangement shown in Fig. 2.41(a), where the voltage source $V_{1}$ is changed by a small amount and the change in $I_{D}$ is measured (while $M_{1}$ remains in saturation). Suppose $V_{1}$ becomes more positive, making $V_{G S}$ more negative. Since the transistor now has a greater overdrive, it carries a higher current, and hence $I_{D}$ becomes more negative. (Recall that $I_{D}$, in the direction shown here, is negative because the actual current of holes flows from the source to the drain.) Thus, a negative $\Delta V_{G S}$ leads to a negative $\Delta I_{D}$. Conversely, a positive $\Delta V_{G S}$ produces a positive $\Delta I_{D}$, as is the case for an NMOS device.
image_name:(a)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: VDD, Nn: g1}
name: M1, type: PMOS, ports: {S: VDD, D: d1, G: g1}
name: VD, type: Capacitor, value: VD, ports: {Np: d1, Nn: GND}
]
extrainfo:The circuit diagram (a) shows a PMOS transistor M1 with its source connected to VDD, gate to g1, and drain to node d1. A voltage source V1 is connected between V1 and g1. A capacitor C1 is connected between node d1 and ground. The current ID flows from the drain of the PMOS to ground.
image_name:(b)
description:The circuit is a small-signal model of a PMOS device. It shows the voltage-dependent current source (ID) between the source and drain, controlled by the gate voltage V1. The PMOS transistor M1 has its source connected to a positive supply and the drain connected to ground through a capacitor C1.

Figure 2.41 (a) Small-signal test of a PMOS device, and (b) small-signal model.

In our circuit diagrams, we usually draw the PMOS devices with their source terminals on top and their drain terminals on the bottom because the former are at a more positive voltage. This practice may cause confusion in drawing small-signal models. Let us draw the small-signal equivalent of the above circuit, assuming no channel-length modulation. Depicted in Fig. 2.41(b), the model shows the voltagedependent current source pointing upward, giving the (wrong) impression that the direction of the current in the PMOS model is the opposite of that in the NMOS model. The reader is cautioned to avoid this confusion and bear in mind that the small-signal models of NMOS and PMOS transistors are identical.

Unless otherwise stated, in this book we assume that the bulk of all NFETs is tied to the most negative supply (usually the ground) and that of PFETs to the most positive supply (usually $V_{D D}$ ).

### 2.4.4 MOS SPICE models

In order to represent the behavior of transistors in circuit simulations, simulators such as SPICE and Cadence require an accurate model for each device. Over the last three decades, MOS modeling has made tremendous progress, reaching sophisticated levels so as to represent high-order effects in shortchannel devices.

In this section, we describe the simplest MOS SPICE model, known as "Level 1," and provide typical values for each parameter in the model corresponding to a $0.5-\mu \mathrm{m}$ technology. Chapter 17 describes
more accurate SPICE models. Table 2.1 shows the model parameters for NMOS and PMOS devices. The parameters are defined as follows:

Table 2.1 Level 1 SPICE models for NMOS and PMOS devices.

| NMOS Model |  |  |  |
| :--- | :--- | :--- | :--- |
| LEVEL $=1$ | VTO $=0.7$ | GAMMA $=0.45$ | PHI $=0.9$ |
| NSUB $=9 \mathrm{e}+14$ | $\mathrm{LD}=0.08 \mathrm{e}-6$ | $\mathrm{UO}=350$ | LAMBDA $=0.1$ |
| TOX $=9 \mathrm{e}-9$ | $\mathrm{~PB}=0.9$ | $\mathrm{CJ}=0.56 \mathrm{e}-3$ | $\mathrm{CJSW}=0.35 \mathrm{e}-11$ |
| MJ $=0.45$ | $\mathrm{MJSW}=0.2$ | $\mathrm{CGDO}=0.4 \mathrm{e}-9$ | $\mathrm{JS}=1.0 \mathrm{e}-8$ |
| PMOS Model |  |  |  |
| LEVEL $=1$ | $\mathrm{VTO}=-0.8$ | $\mathrm{GAMMA}=0.4$ | $\mathrm{PHI}=0.8$ |
| NSUB $=5 \mathrm{e}+14$ | $\mathrm{LD}=0.09 \mathrm{e}-6$ | $\mathrm{UO}=100$ | LAMBDA $=0.2$ |
| TOX $=9 \mathrm{e}-9$ | $\mathrm{~PB}=0.9$ | $\mathrm{CJ}=0.94 \mathrm{e}-3$ | $\mathrm{CJSW}=0.32 \mathrm{e}-11$ |
| $\mathrm{MJ}=0.5$ | $\mathrm{MJSW}=0.3$ | $\mathrm{CGDO}=0.3 \mathrm{e}-9$ | $\mathrm{JS}=0.5 \mathrm{e}-8$ |

VTO: threshold voltage with zero $V_{S B}$ (unit: V)
GAMMA: body-effect coefficient (unit: $\mathrm{V}^{1 / 2}$ )
PHI: $2 \Phi_{F}$ (unit: V)
TOX: gate-oxide thickness (unit: m)
NSUB: substrate doping (unit: $\mathrm{cm}^{-3}$ )
LD: source/drain side diffusion (unit: m)
UO: channel mobility (unit: $\mathrm{cm}^{2} / \mathrm{V} / \mathrm{s}$ )
LAMBDA: channel-length modulation coefficient (unit: $\mathrm{V}^{-1}$ )
CJ: source/drain bottom-plate junction capacitance per unit area (unit: F/m²)
CJSW: source/drain sidewall junction capacitance per unit length (unit: F/m)
PB: source/drain junction built-in potential (unit: V)
MJ: exponent in CJ equation (unitless)
MJSW: exponent in CJSW equation (unitless)
CGDO: gate-drain overlap capacitance per unit width (unit: F/m)
CGSO: gate-source overlap capacitance per unit width (unit: F/m)
JS: source/drain leakage current per unit area (unit: $\mathrm{A} / \mathrm{m}^{2}$ )

### 2.4.5 NMOS Versus PMOS Devices

In most CMOS technologies, PMOS devices are quite inferior to NMOS transistors. For example, due to the lower mobility of holes, $\mu_{p} C_{o x} \approx 0.5 \mu_{n} C_{o x}$, yielding low current drive and transconductance. Moreover, for given dimensions and bias currents, NMOS transistors exhibit a higher output resistance, providing more ideal current sources and higher gain in amplifiers. For these reasons, incorporating NFETs rather than PFETs wherever possible is preferred. ${ }^{11}$

### 2.4.6 Long-Channel Versus Short-Channel Devices

In this chapter, we have employed a very simple view of MOSFETs so as to understand the basic principles of their operation. Most of our treatment is valid for "long-channel" devices, e.g., transistors having a minimum length of a few microns. Many of the relationships derived here must be reexamined and revised for short-channel MOSFETs. Furthermore, the SPICE models necessary for simulation of today's devices

[^9]are much more sophisticated than the Level 1 model. For example, the intrinsic gain, $g_{m} r_{O}$, calculated from the device parameters in Table 2.1 is much higher than actual values. These issues are studied in Chapter 17.

The reader may wonder why we begin with a simplistic view of devices if such a view does not lead to high accuracy in predicting the performance of circuits. The key point is that the simple model provides a great deal of intuition that is necessary in analog design. As we will see throughout this book, we often encounter a trade-off between intuition and rigor, and our approach is to establish the intuition first and gradually complete our understanding so as to achieve rigor as well.

## 2.5 - Appendix A: FinFETs

New CMOS technology generations ("nodes") have migrated from the two-dimensional transistor structure to a three-dimensional geometry called the "FinFET." This device exhibits superior performance as channel lengths fall below approximately 20 nm . In fact, FinFET I/V characteristics are closer to square-law behavior, making our simple large-signal mode relevant again.

Shown in Fig. 2.42(a), the FinFET consists of a vertical silicon "fin," a dielectric (e.g., oxide) layer deposited over the fin, and a polysilicon or metal gate created over the dielectric layer. Controlled by the gate voltage, the current flows from one end of the fin to the other. The top view looks similar to that of a planar MOSFET [Fig. 2.42(b)].
image_name:(a) FinFET structure
description:The image consists of two parts, labeled (a) and (b), depicting different views of a FinFET structure.

**(a) FinFET Structure:**
- **Components and Structure:** The diagram illustrates a vertical silicon fin, which is the primary structure of the FinFET. The fin is surrounded by a dielectric layer, labeled as 'Oxide,' over which a gate material, either polysilicon or metal, is placed. The fin extends vertically from the substrate, and the current flows from the source at one end of the fin to the drain at the other end.
- **Connections and Interactions:** The gate controls the current flow through the fin by applying a voltage, which modulates the conductivity between the source and drain. The current flows on three sides of the fin, which is a key feature of FinFETs, allowing for better control over the channel.
- **Labels, Annotations, and Key Features:** The diagram includes labels for 'Source,' 'Drain,' 'Gate,' 'Oxide,' and 'Substrate.' The dimensions of the fin are indicated with 'H_F' representing the height of the fin and 'W_F' representing the width. The 'Gate Length' is also marked, showing the length of the gate covering the fin.

**(b) Top View:**
- **Components and Structure:** This view shows a simplified, planar representation of the FinFET from above. It highlights the alignment of the source, gate, and drain.
- **Connections and Interactions:** The source and drain are positioned on opposite sides of the gate, illustrating the linear flow of current when viewed from above.
- **Labels, Annotations, and Key Features:** The top view is labeled with 'Source,' 'Drain,' and 'Gate,' providing a straightforward representation of their arrangement in the device.
image_name:(b) top view
description:The image consists of two parts labeled (a) and (b). Part (a) depicts a three-dimensional structure of a FinFET, while part (b) shows the top view of the FinFET.

1. **Identification of Components and Structure:**
- **Part (a):** This section illustrates the FinFET structure, which includes a vertical silicon fin. The fin is covered by a dielectric layer, typically an oxide, and a gate, which can be made of polysilicon or metal, wraps around the fin. The image highlights the source and drain regions at either end of the fin. The substrate is shown at the bottom, supporting the entire structure.
- **Part (b):** This section shows the top view of the FinFET. It displays the gate as a rectangular block with the source and drain regions extending from either side.

2. **Connections and Interactions:**
- **Part (a):** The current flow is controlled by the gate voltage, which modulates the current between the source and drain through the silicon fin. The diagram visually represents the current path using arrows, indicating that the current flows along three facets of the fin, enhancing control and efficiency.
- **Part (b):** The top view simplifies the structure, showing the gate's position relative to the source and drain, emphasizing the planar alignment typical of MOSFETs.

3. **Labels, Annotations, and Key Features:**
- **Part (a):** The diagram labels key dimensions such as the fin height ($H_{F}$) and fin width ($W_{F}$). It also notes the gate length, which is a crucial parameter for device performance. Annotations indicate the material layers (oxide, gate) and the direction of current flow.
- **Part (b):** This view is labeled to identify the source, gate, and drain, providing a simplified representation of the FinFET’s layout from above, which resembles a planar MOSFET configuration.

Figure 2.42 (a) FinFET structure, and (b) top view.
As depicted in Fig. 2.42(a), the gate length can be readily identified, but how about the gate width? We note that the current flows on three facets of the fin. The equivalent channel width is therefore equal to the sum of the fin's width, $W_{F}$, and twice its height, $H_{F}: W=W_{F}+2 H_{F}$. Typically, $W_{F} \approx 6 \mathrm{~nm}$ and $H_{F} \approx 50 \mathrm{~nm}$.

Since $H_{F}$ is not under the circuit designer's control, it appears that $W_{F}$ can be chosen so that $W_{F}+2 H_{F}$ yields the desired transistor width. However, $W_{F}$ affects device imperfections such as source and drain series resistance, channel-length modulation, subthreshold conduction, etc. For this reason, the fin width is also fixed, dictating discrete values for the transistor width. For example, if $W_{F}+2 H_{F}=100 \mathrm{~nm}$, then wider transistors can be obtained only by increasing the number of fins and only in 100-nm increments (Fig. 2.43). The spacing between the fins, $S_{F}$, also plays a significant role in the performance and is typically fixed.

Due to the small dimensions of the intrinsic FinFET, the gate and S/D contacts must be placed away from the core of the device. Figure 2.44 shows the details for a single- and a double-fin structure.
image_name:Figure 2.43 FinFET with multiple fins
description:The image labeled "Figure 2.43 FinFET with multiple fins" illustrates a schematic representation of a Fin Field-Effect Transistor (FinFET) with multiple fins. The diagram is a simplified model showing the essential components and structure of the device.

1. **Identification of Components and Structure:**
- The central component is the **Gate**, depicted as a large rectangular block horizontally oriented across the image.
- There are multiple vertical lines intersecting the Gate, representing the **fins** of the FinFET. These fins extend above and below the Gate.
- The **Source** and **Drain** are labeled on opposite sides of the Gate, with the Source on the left and the Drain on the right.

2. **Connections and Interactions:**
- The fins act as channels through which current flows between the Source and Drain, controlled by the Gate.
- The spacing between the fins, labeled as **S_F**, is critical for device performance and is shown as a bidirectional arrow indicating the distance between adjacent fins.

3. **Labels, Annotations, and Key Features:**
- The diagram is annotated with labels for Source, Drain, Gate, and the fin spacing (S_F).
- The fins are uniformly spaced, indicating a regular pattern essential for scaling and performance optimization in FinFET technology.

Overall, the image provides a clear and simplified view of a FinFET device, highlighting its multi-fin structure and the spatial relationships between its components.

Figure 2.43 FinFET with multiple fins.
image_name:Figure 2.44 Layout of single- and double-fin transistors
description:The image labeled "Figure 2.44 Layout of single- and double-fin transistors" shows two schematic representations of transistor layouts, specifically focusing on single-fin and double-fin configurations.

1. **Identification of Components and Structure:**
- The diagram on the left represents a single-fin transistor layout. It consists of a central rectangular region, likely representing the gate, connected vertically to two smaller square regions, which could represent the source and drain terminals.
- The diagram on the right depicts a double-fin transistor layout. This configuration includes a similar central rectangular gate region but with two parallel connections to each of the square regions, indicating the presence of two fins.

2. **Connections and Interactions:**
- In both layouts, the central rectangular region (gate) is connected to the square regions (source and drain) via vertical lines. These lines likely represent the fins, which are critical for the operation of FinFETs by controlling the current flow between source and drain.
- The double-fin layout shows two parallel connections, indicating enhanced performance capabilities due to increased surface area for current conduction.

3. **Labels, Annotations, and Key Features:**
- The diagrams are simplified and do not contain specific labels or annotations for voltage values or material properties. However, the structural difference between single and double fins is clearly illustrated, emphasizing the scalability and performance differences between them.
- The uniformity in the spacing and alignment of components suggests a focus on precision and optimization in the design of FinFET technology.

Figure 2.44 Layout of single- and double-fin transistors.

## 2.6 ■ Appendix B: Behavior of a MOS Device as a Capacitor

In this chapter, we have limited our treatment of MOS devices to a basic level. However, the behavior of a MOSFET as a capacitor merits some attention. Recall that if the source, drain, and bulk of an NFET are grounded and the gate voltage rises, an inversion layer begins to form for $V_{G S} \approx V_{T H}$. We also noted that for $0<V_{G S}<V_{T H}$, the device operates in the subthreshold region.

Now consider the NFET of Fig. 2.45. The transistor can be considered a two-terminal device, and hence its capacitance can be examined for different gate voltages. Let us begin with a very negative gate-source voltage. The negative potential on the gate attracts the holes in the substrate to the oxide interface. We say that the MOSFET operates in the "accumulation" region. The two-terminal device can be viewed as a capacitor having a unit-area capacitance of $C_{o x}$ because the two "plates" of the capacitor are separated by $t_{o x}$.
image_name:Figure 2.45 NMOS operating in accumulation mode
description:
[
name: VG, type: VoltageSource, ports: {Np: Gate, Nn: GND}
]
extrainfo:The diagram shows an NMOS transistor operating in accumulation mode with a negative gate voltage (VG < 0). The negative potential attracts holes to the oxide interface, indicating the presence of a p-type substrate. The NMOS transistor is connected with its gate to the voltage source VG, and the source and drain are connected to ground.

Figure 2.45 NMOS operating in accumulation mode.

As $V_{G S}$ rises, the density of holes at the interface falls, a depletion region begins to form under the oxide, and the device enters weak inversion. In this mode, the capacitance consists of the series combination of $C_{o x}$ and $C_{d e p}$. Finally, as $V_{G S}$ exceeds $V_{T H}$, the oxide-silicon interface sustains a channel and the unit-area capacitance returns to $C_{o x}$. Figure 2.46 plots the behavior.
image_name:Figure 2.46 Capacitance-voltage characteristic of an NMOS device
description:The graph is a capacitance-voltage (C-V) characteristic plot of an NMOS device, specifically labeled as Figure 2.46.

1. **Type of Graph and Function:**
- This is a capacitance-voltage graph, which is used to show how the capacitance between the gate and the source of an NMOS transistor changes with the gate-source voltage (V_GS).

2. **Axes Labels and Units:**
- The x-axis represents the gate-source voltage (V_GS), which is typically measured in volts.
- The y-axis represents the gate-source capacitance (C_GS), which is measured in farads.
- The graph is linear in scale.

3. **Overall Behavior and Trends:**
- The graph shows a distinct U-shape, indicating how capacitance varies with voltage.
- As V_GS increases from negative to positive, the capacitance initially decreases, reaches a minimum, and then increases again.
- The capacitance is high in the accumulation region (negative V_GS) and the strong inversion region (positive V_GS beyond the threshold voltage V_TH).

4. **Key Features and Technical Details:**
- The graph has a minimum point at which the capacitance is lowest, occurring at the transition from accumulation to inversion.
- The threshold voltage (V_TH) is marked on the x-axis, signifying the transition to strong inversion where the capacitance begins to rise again.
- In accumulation (left side of the graph), the capacitance is primarily determined by the oxide capacitance (C_ox).
- In strong inversion (right side), the capacitance is also dominated by C_ox as a channel forms.

5. **Annotations and Specific Data Points:**
- The graph is annotated with the terms "Accumulation" on the left side and "Strong Inversion" on the right side, indicating the different operating regions of the NMOS device.
- The threshold voltage (V_TH) is indicated with a vertical dashed line, showing the point where the device transitions from weak to strong inversion.

Figure 2.46 Capacitance-voltage characteristic of an NMOS device.
