# 3. MOS Field-Effect Transistors

Chapter Outline
3.1 Physical Structure of the MOSFET ..... 224
3.2 The Threshold Voltage $V_{t}$ ..... 226
3.3 The $n$-Channel Characteristic ..... 237
3.4 The $i-v$ Characteristics of MOSFETs ..... 247
3.5 MOSFETs in Resistive Dc Circuits ..... 259
3.6 The MOSFET as an Amplifier/Switch ..... 273
3.7 Small-Signal Operation of the MOSFET ..... 282
3.8 Basic MOSFET Voltage Amplifiers ..... 290
3.9 MOSFET Voltage and Current Buffers ..... 300
3.10 The CMOS Inverter/Amplifier ..... 306
Appendix 3A: SPICE Models for MOSFETs ..... 314
References ..... 316
Problems ..... 316

The age of semiconductor electronics began when the triode function (a controlled current source-see the introduction to Chapter 2 for a discussion of the vacuum-tube triode) was implemented on a piece of semiconductor material. This occurred in 1947 with the invention of the bipolar junction transistor (BJT), the first working realization of the semiconductor triode concept. However, neither is the BJT the only transistor type possible, nor was it the first transistor to be conceived. In fact, as early as 1925, Julius Lilienfeld patented a device of the type today known as the field-effect transistor (FET). However, because of fabrication difficulties at the time, he could never get it to work. It took another 35 years or so before Dawon Kahng and John Atalla of Bell Laboratories demonstrated, in 1960, the first FET of the so-called metal-oxide-semiconductor (MOS) type, or MOSFET for short.

The closest MOSFET counterpart of the vacuum-tube triode is what is today known as the $n$-channel depletion-type MOSFET ( $n$-channel DMOSFET), which is one of four possible MOSFET types. Briefly stated, a DMOSFET consists of a thin layer of $n$-type material called the channel, which forms a parallel-plate capacitor with an electrode called the gate. One end of the channel, called the source, acts as a copious source of
free electrons, which are designed to flow to the opposite end of the channel, aptly called the drain. The roles of source and drain are similar to those of cathode and plate in the triode (or emitter and collector in the BJT). The role of the gate, similar to that of the grid in the triode (or the base in the BJT), is to modulate the channel's conductivity and thus control the electron flow from source to drain. Specifically, driving the gate voltage negative will induce a positive charge in the channel, at the expense of a reduction in the concentration of free electrons there. For a sufficiently negative gate voltage, the channel will be depleted of free electrons and current flow will cease altogether. By a hydraulic analogy, FET behavior can be likened to that of a garden hose being squeezed for the purpose of controlling water flow, or even being shut off completely.

Following the successful demonstration of the first MOSFET, the new technology was put to use especially in those applications in which the advantages of smaller size and lower power consumption of the MOSFET made it competitive with its BJT counterpart. The first battery-powered electronic calculators and wristwatches made use precisely of this new technology. Also, a new digital integrated circuit (IC) family known as complementary MOS (or CMOS for short) was introduced by RCA as a low-power alternative to the then prevalent bipolar logic family known as TTL. In 1971 Intel used MOS technology to develop the first microprocessor. Since then, IC electronics has advanced exponentially and has penetrated virtually every aspect of modern life. This impressive growth has been governed by Moore's law, roughly stating that thanks to continued advances in IC fabrication, the number of devices that can be integrated on a given chip area doubles every approximately 18 months. Originally formulated in 1965, this law still holds to this day, though it has been pointed out that technology is bound to approach physical limits that will eventually lead to the demise of this law.

Over the years, the MOSFET has overtaken its BJT predecessor especially in high-density IC electronics, owing to its aforementioned advantages of smaller size and lower power consumption. Nonetheless, there are applications such as high-performance analog electronics, in which the BJT continues to be the preferred transistor type. To exploit the advantages of both BJTs and MOSFETs, the two device types are sometimes fabricated simultaneously on the same chip. The resulting technology, aptly called biCMOS technology, provides even greater design opportunities than the all-BJT or all-MOSFET technologies individually. Also, contemporary ICs often combine digital as well as analog functions on the same chip, this being the reason for the name mixed-signal or also mixed-mode ICs.

There is no question that microelectronics is a most exciting, challenging, and rapidly evolving field. The beginner may feel overwhelmed by all this, and rightly so. But, as we embark upon the study of today's dominant processes and devices, we will try to focus on general principles that transcend the particular technological milieu of the moment and that we can apply to understand new processes and devices as they become available and commercially mature. Focus on general principles, combined with continuing education, is a necessity for the young engineer aiming at establishing and maintaining a satisfying career in a seemingly ever-changing field.

CHAPTER HIGHLIGHTS
The chapter begins with a study of the physical structure of the MOSFET, basic underlying semiconductor principles, device characteristics, operating regions and modeling. Much emphasis is placed on practical aspects of relevance to today's industrial environment (rules of thumb). The FETs under scrutiny are of the so-called long-channel type (channel lengths in the range of several micrometers or longer) because their behavior conforms reasonably well to theoretical prediction, so they are easier to model as well as easier to grasp by the beginner. However, the devices available in today's ever shrinking IC processes are of the short-channel type (channel lengths of a fraction of $1 \mu \mathrm{~m}$ ). At such small sizes, a number of higher-order effects arise, particularly carrier velocity saturation, which may cause significant departure from long-channel behavior. Aptly called short-channel effects, they require more complex formalism and more sophisticated models as the price for providing more realistic results. These advanced models, while realizable in computer simulators, are too complicated for hand analysis. We shall nevertheless continue to rely on the formalism and models of long-channel devices to develop an intuitive understanding of MOSFETs, and then turn to computer simulation for more accurate results.

After examining a variety of resistive MOSFET circuits so as to develop a basic feel for MOSFET circuit operation, we investigate the MOSFET in its two most important class of applications, namely, as an amplifier in analog electronics, and as a switch in digital electronics. Next, we develop suitable large-signal models as well as small-signal models for the FETs, so we can turn to the three basic amplifier configurations, namely, the common-source (CS), common-drain (CD), and common-gate (CG) configurations. The CS configuration is presented as the natural realization of voltage amplification, whereas the CD and CG configurations serve most naturally as voltage and current buffers, respectively. Suitable emphasis is placed on the role of the MOSFET as a resistance transformation device, which actually provided the basis for the name transistor. The transformation equations are conveniently tabulated for easy reference in later chapters.

The amplifiers studied in this chapter are of the discrete type because they can be built using individual transistors, resistors, and capacitors. (In this respect, a handy device to experiment with in the lab is the CD4007 CMOS Transistor Array, comprising three $n$ MOSFETs and three $p$ MOSFETs.) Though nowadays MOSFET amplifiers are implemented mostly in IC form, the motivation for studying discrete designs is primarily pedagogical, as discrete circuits are somewhat easier to grasp, and yet they reveal important aspects that apply to IC implementations as well. Once we master the basics of discrete design involving a single-transistor amplifier, we will be in a better position to tackle the complexity of multi-transistor ICs, a subject that will be undertaken in Chapter 4.

For the benefit especially of computer engineering majors, the chapter concludes with a detailed analysis of the CMOS inverter/amplifier as a simple yet important IC building block that demonstrates the flexibility of CMOS technology both in the analog and digital domains. Basic CMOS logic gates are also addressed in some detail.

The chapter makes abundant use of PSpice both as a software oscilloscope to display MOSFET characteristics, transfer curves and waveforms, and as a verification tool for dc as well as ac calculations.

## 3.1 PHYSICAL STRUCTURE OF THE MOSFET

Figure 3.1 shows, in simplified form, the structure of the $n$-channel, metal-oxidesemiconductor (MOS) field-effect transistor (FET), or nMOSFET for short. The device is fabricated through a complex sequence of steps involving pattern definition, oxidation, diffusion, ion implantation, material deposition and material removal, on a wafer of lightly-doped p-type silicon ( $p^{-}$) called the body or also the bulk of the $n$ MOSFET. The wafer is also called the substrate because it provides physical support for the device under consideration as well as all other devices of the same integrated circuit (IC). Starting out with a polished wafer, the fabrication of an $n$ MOSFET consists of the following principal steps:

- First, a thin $\left(t_{o x}\right)$ insulating layer of silicon oxide $\left(\mathrm{SiO}_{2}\right)$ is thermally grown on the surface of the substrate.
- Next, the gate electrode is created by growing over the oxide a layer of heavilydoped $n$-type silicon $\left(n^{+}\right)$. Being extremely rich in free electrons, this electrode acts for all practical purposes like a metal. The resulting metal-oxide-semiconductor (MOS) structure is the reason for the name of the device.
- Next, the oxide is removed from each side of the gate, and ion implantation is used to create two heavily-doped $n$-type regions $\left(n^{+}\right)$extending into the substrate, called the source and the drain regions.
- Finally, two metal depositions form the source and drain electrodes. (The interested student is encouraged to search the Web for videos and articles illustrating the fascinating subject of MOSFET fabrication.)

The region of the body just below the oxide is called the channel region. Its length and width are denoted as $L$ and $W$, respectively. In current VLSI technology, $L$ and $W$ can be as small as fractions of a micrometer $\left(1 \mu \mathrm{~m}=10^{-6} \mathrm{~m}=10^{-4} \mathrm{~cm}\right)$, while the oxide thickness $t_{o x}$ can be as low as ten nanometers ( $1 \mathrm{~nm}=10^{-9} \mathrm{~m}=$ $\left.10^{-7} \mathrm{~cm}=10 \AA ̊\right)$. We identify two basic ingredients in a MOSFET:

- the channel region extending between the source and drain regions, and
- the parallel-plate capacitor formed by the gate and the channel region.
image_name:FIGURE 3.1 Basic physical structure of the n MOSFET
description:The image titled "FIGURE 3.1 Basic physical structure of the n MOSFET" depicts a schematic diagram of an n-type Metal-Oxide-Semiconductor Field-Effect Transistor (MOSFET). The key components and structure of the MOSFET are illustrated as follows:

1. **Components and Structure:**
- **Source and Drain Regions:** These are labeled as 'Source' and 'Drain' on the diagram. They are heavily doped n-type regions (denoted as n+) within the p-type substrate. The source and drain are positioned on opposite sides of the channel.
- **Gate:** The gate is shown as a large, flat conductive region above the oxide layer. It controls the conductivity of the channel by applying a voltage.
- **Oxide Layer:** This is the insulating layer between the gate and the channel, labeled as 'Oxide' in the diagram. It acts as a dielectric in the gate capacitor.
- **Channel:** The channel is the region between the source and drain under the gate. It is where the current flows when the MOSFET is active.
- **Body (or Substrate):** The p-type substrate is labeled as 'p- Substrate.' The body is connected to the lowest potential in the circuit.

2. **Connections and Interactions:**
- The gate controls the channel conductivity through the gate-body capacitance. By applying a voltage to the gate, an electric field is created, modulating the channel's conductivity.
- The source and drain are connected through the channel when the MOSFET is on, allowing current to flow from the source to the drain.

3. **Labels, Annotations, and Key Features:**
- **W:** The width of the channel.
- **L:** The length of the channel, indicating the distance between the source and drain.
- **t_ox:** The thickness of the oxide layer.
- Annotations such as 'n+', 'p- Substrate,' and directional arrows indicating the flow of current and voltage application are present to help understand the MOSFET's operation.

This diagram provides a clear conceptual view of how an n-type MOSFET is structured and operates, emphasizing the role of the gate in controlling the channel conductivity.

FIGURE 3.1 Basic physical structure of the $n$ MOSFET.

Briefly stated, the principle at the basis of the MOSFET is to utilize the gate-body capacitance to control the channel-region conductance. The path extending from the source to the drain regions includes two back-to-back pn junctions (the body-source and the body-drain junctions), so it normally exhibits very high resistance to current flow (typically $\sim 10^{12} \Omega$ ). However, by raising the potential of the gate electrode to a suitable value, we can create favorable conditions for free electrons to exist in the channel region, and thus form a continuous conductive path, or channel, from source to drain, along which electrons can flow and produce current. To investigate device behavior, we will have to address two basic questions:

- What is the threshold voltage $V_{t}$ to which we need to raise the gate potential relative to the bulk to form a channel and thus turn on the device?
- Once the device has been turned on, what are the $i$-v characteristics of its channel?

Both issues will be addressed in the following sections.

### Complementary MOSFETs

The dominant IC technology today utilizes the $n$ MOSFET as well as its dual (or complementary) device, the $p$ MOSFET. Aptly called complementary MOS (or CMOS) technology, it requires that both device types be fabricated on the same substrate. A $p$ MOSFET is obtained by negating the doping types of the body, source, and drain regions of an $n$ MOSFET, so that the body is now $n^{-}$, and the source and drain regions are $p^{+}$. To allow for the coexistence of the two devices on a common substrate, the $p$ MOSFET is placed inside a local lightly doped $n$-type ( $n^{-}$) substrate, also called well or tub, which is formed by a separate diffusion into the existing $p^{-}$wafer prior to the fabrication of the transistors themselves.

The structure is depicted in cross-sectional form in Fig. 3.2, where subscripts $n$ and $p$ identify the terminals of the $n$ MOSFET and the $p$ MOSFET, respectively. The $n$ MOSFET, located left of center, is similar to that of Fig. 3.1, except that the connection to its body $\left(B_{n}\right)$ is not at the bottom, as shown in the simplified rendition of Fig. 3.1, but at the top, left. This is mandated by the planar-IC requirement that all interconnections be made at the top of the wafer. The $p$ MOSFET, located right of center, is placed inside its own well $\left(n^{-}\right)$, and connection to the well $\left(B_{p}\right)$ is at the top, right. To ensure good-quality ohmic contacts, the metal connections to the bulks are implemented through heavily doped regions, as shown.
image_name:FIGURE 3.2 Cross-sectional view of CMOS transistors
description:The image titled "FIGURE 3.2 Cross-sectional view of CMOS transistors" shows a detailed cross-section of complementary metal-oxide-semiconductor (CMOS) transistors, illustrating both n-channel (nMOS) and p-channel (pMOS) transistors in an integrated circuit.

1. **Identification of Components and Structure:**
- The left side of the diagram features an n-channel MOSFET (nMOS) situated on a p-type body. The nMOS transistor comprises several key components:
- **Bn:** Bulk connection for the nMOS, connected to a p+ region.
- **Sn:** Source of the nMOS, connected to an n+ region.
- **Gn:** Gate of the nMOS, located above the n-channel (n-ch).
- **Dn:** Drain of the nMOS, connected to another n+ region.
- The right side of the diagram shows a p-channel MOSFET (pMOS) placed within an n-type well:
- **Dp:** Drain of the pMOS, connected to a p+ region.
- **Gp:** Gate of the pMOS, located above the p-channel (p-ch).
- **Sp:** Source of the pMOS, connected to another p+ region.
- **Bp:** Bulk connection for the pMOS, connected to an n+ region.

2. **Connections and Interactions:**
- The nMOS transistor is built on a p-type substrate, while the pMOS is in an n-type well, ensuring that both transistors are properly isolated.
- **SiO2 Layers:** The diagram shows silicon dioxide (SiO2) insulator layers surrounding the transistors, providing electrical isolation between devices.
- The gate terminals of both transistors are shown as rectangles above their respective channels, indicating the control mechanism for the flow of current between source and drain.
- The pMOS and nMOS are electrically isolated from each other by the SiO2 field oxide.

3. **Labels, Annotations, and Key Features:**
- The pMOS is placed inside an n-well, as indicated by the label "n-Well," and the nMOS is on a "p- Body."
- The heavily doped regions, marked as n+ and p+, are used to ensure good ohmic contacts for the metal connections to the source, drain, and bulk terminals.
- The diagram clearly shows the layout of the CMOS structure, emphasizing the need for electrical isolation and proper component placement within an integrated circuit.

FIGURE 3.2 Cross-sectional view of CMOS transistors.

Figure 3.2 illustrates also another important aspect of ICs, namely, the need for adjacent devices to be electrically isolated from each other. This constraint is met by growing, prior to fabrication of the actual transistors, a ring of $\mathrm{SiO}_{2}$ insulator material, also called field oxide, around each transistor's intended site. Indeed, each transistor must be kept electrically isolated not only from its neighboring devices, but also from its own body! The $p$-type body of the $n$ MOSFET forms $p n$ junctions with the $n$-type source and drain regions, so in this case body isolation is achieved by anchoring $B_{n}$ to the most negative voltage (MNV) in the circuit. This will keep both junctions reverse biased, and therefore in cutoff, under all possible circuit conditions. Likewise, the $n$-type well of the $p$ MOSFET forms $n p$ junctions with the $p$-type source and drain regions, so anchoring $B_{p}$ to the most positive voltage (MPV) in the circuit will keep both junctions in cutoff under all possible circuit conditions. For instance, in the case of a digital CMOS circuit powered between 5 V and ground, $B_{n}$ is connected to ground, and $B_{p}$ is connected to +5 V . The manufacturer makes these connections internally to the IC.

## 3.2 THE THRESHOLD VOLTAGE $V_{t}$

To investigate the mechanism of channel formation in a $n$ MOSFET, we focus on its gate-oxide-bulk structure, which forms a parallel-plate capacitor, albeit one with plates of different materials. Though in earlier MOSFETs the gate electrode was made of metal, such as aluminum, nowadays it is fabricated using $n^{+}$silicon, this being the reason why modern processes are also referred to as silicon-gate processes. Since the $n^{+}$silicon film is grown over amorphous oxide, it consists of sub-micrometersized crystallites, rather than a single crystal, and it is thus referred to a polysilicon. Regardless, $n^{+}$polysilicon is very rich in free electrons, just like a metal, and it is used not only to create the gate electrode, but also to interconnect different devices in an IC. The reason for making the gate electrode of polysilicon is that the subsequent ion implantation to create the source and drain regions will inherently guarantee a high degree of alignment among the different regions. In particular, as the ions diffuse downward into the body, they also diffuse sideways a bit, resulting in a small amount of overlap between the edges of the gate and those of the source/drain regions. As we proceed, we shall appreciate how this slight overlap, clearly shown in both pictures above, is critical for the proper functioning of the MOSFET.

We now wish to investigate the effect of an external bias upon the type of charges as well as their distributions in the bulk region just below the oxide layer. Since no current flows through the insulating oxide layer, the only means for the gate to influence the channel region is via the electric field inside the oxide. Hence, the designation field-effect transistor (FET).

### The Gate-Body Capacitor

Figure 3.3 shows a section of the gate-oxide-body structure of Fig. 3.1, but rotated counterclockwise by $90^{\circ}$. As mentioned in connection with Fig. 3.2, the function of the $p^{+}$ region is to ensure a good-quality ohmic contact between the $p^{-}$bulk and the metal connection, so it will play no role in our analysis. The well-known formula for parallelplate capacitance gives, in the present case, $C=\varepsilon_{o x}(W \times L) / t_{o x}$, where $W$ and $L$ are the
image_name:(a)
description:The image consists of two diagrams labeled (a) and (b), illustrating the gate-body capacitor structure at different bias conditions.

**Diagram (a):**
1. **Components and Structure:**
- The diagram shows a cross-section of a gate-body capacitor.
- It includes an **n⁺ gate**, a **SiO₂ (silicon dioxide) layer**, a **p⁻ body**, and a **p⁺ region**.
- The **n⁺ gate** is on the left side, followed by the SiO₂ layer, which acts as the dielectric between the gate and the body.
- The **p⁻ body** is adjacent to the SiO₂ layer, and the **p⁺ region** ensures good ohmic contact.

2. **Connections and Interactions:**
- The **gate (G)** is connected to the metal contact on the n⁺ gate.
- The **body (B)** is connected to the metal contact on the p⁺ region.
- The diagram illustrates the presence of **space-charge layers**, with donor ions near the n⁺ gate and acceptor ions in the p⁻ body.

3. **Labels, Annotations, and Key Features:**
- "Donor ions" and "Acceptor ions" are labeled to indicate the charge distribution within the space-charge layers.
- The region is marked as containing space-charge layers, indicating the influence of charges in the dielectric.

**Diagram (b):**
1. **Components and Structure:**
- Similar to diagram (a), it includes an **n⁺ gate**, a **SiO₂ layer**, a **p⁻ body**, and a **p⁺ region**.

2. **Connections and Interactions:**
- The **gate (G)** and **body (B)** connections remain the same.
- The diagram shows the capacitor biased at **V_GB = -φ₀**, eliminating the space-charge layers.

3. **Labels, Annotations, and Key Features:**
- "No space-charge layers present" is labeled, indicating that the bias voltage has neutralized the space-charge region.
- The bias voltage **V_GB = -φ₀** is shown with a symbol indicating the applied potential.

These diagrams collectively illustrate how the gate-body capacitor behaves under different bias conditions, with emphasis on the presence or absence of space-charge layers.
image_name:(b)
description:The image shows two diagrams labeled (a) and (b) representing the gate-body capacitor structure at different bias conditions.

**Diagram (a):**
- **Components and Structure:**
- The diagram illustrates a cross-section of a gate-body capacitor with an \(n^+\) gate, a \(SiO_2\) layer, and a \(p^-\) body.
- The \(n^+\) gate is connected to a terminal labeled \(G\).
- The \(SiO_2\) layer, which acts as an insulating layer, is situated between the \(n^+\) gate and the \(p^-\) body.
- The \(p^-\) body has a \(p^+\) region at the end, connected to a terminal labeled \(B\).
- Space-charge layers are present, indicated by the presence of donor ions near the \(n^+\) gate and acceptor ions in the \(p^-\) body.
- **Connections and Interactions:**
- The \(n^+\) gate is connected to the \(G\) terminal, and the \(p^+\) region is connected to the \(B\) terminal.
- The space-charge layers are formed due to the electric field across the \(SiO_2\) layer, showing the presence of donor and acceptor ions.
- **Labels, Annotations, and Key Features:**
- The space-charge layers are labeled, with donor ions near the \(n^+\) gate and acceptor ions in the \(p^-\) body.

**Diagram (b):**
- **Components and Structure:**
- Similar to diagram (a), it shows the \(n^+\) gate, \(SiO_2\) layer, and \(p^-\) body with a \(p^+\) region.
- The connections to terminals \(G\) and \(B\) remain the same.
- **Connections and Interactions:**
- A voltage \(V_{GB} = -\phi_0\) is applied between the gate and body, eliminating the space-charge layers.
- The absence of space-charge layers is indicated by the lack of ion representation.
- **Labels, Annotations, and Key Features:**
- The diagram is labeled to show that no space-charge layers are present under the applied bias \(V_{GB} = -\phi_0\).

FIGURE 3.3 Gate-body capacitor (a) at 0-V bias, and (b) biased at $-\phi_{0}$ to eliminate the space-charge layers.
channel-region's width and length depicted in Fig. 3.1, $\varepsilon_{o x}$ is the permittivity of the oxide layer, and $t_{o x}$ is its thickness. To make analysis independent of the particular device size, it is convenient to work with the capacitance per unit area, defined as $C_{o x}=C /(W \times L)$, or

$$
\begin{equation*}
C_{o x}=\frac{\varepsilon_{o x}}{t_{o x}} \tag{3.1}
\end{equation*}
$$

In today's technology $W$ and $L$ are typically in the sub-micron range $(1 \mu \mathrm{~m}=$ $\left.10^{-9} \mathrm{~m}\right)$, and $t_{o x}$ can be in the range of $10 \mathrm{~nm}\left(1 \mathrm{~nm}=10^{-9} \mathrm{~m}\right)$ or less. Silicon oxide has $\varepsilon_{o x}=345 \mathrm{fF} / \mathrm{cm}$, so a fabrication process with, say, $t_{o x}=10 \mathrm{~nm}$ gives $C_{o x}=$ $3.45 \mathrm{fF} / \mu \mathrm{m}^{2}$. (As a rule, $C_{o x}=34.5 / t_{o x}, C_{o x} \mathrm{in} \mathrm{fF} / \mu \mathrm{m}^{2}$ and $t_{o x}$ in nm.)

The bulk-oxide-gate structure is reminiscent of the familiar $p n$ junction, except that the present $p^{-}$and $n^{+}$materials are separated by an insulator layer, which prevents direct current flow. However, if we connect $G$ and $B$ externally as in Fig. 3.3a, electrons will diffuse from the electron-rich $n^{+}$gate, through the connection, to the electron-starved $p^{-}$bulk, leaving behind a layer of immobile positive donor ions in the gate. Once in the bulk, these excess electrons recombine with holes there in order to satisfy the massaction law, leading in turn to the formation of a layer of immobile negative acceptor ions in the bulk. The two layers concentrate near the gate-oxide and the bulk-oxide interfaces in order to minimize the electrostatic energy of the system. Just as in the case of the $p n$ junction, these space-charge layers yield an electric field $E$ from the gate, through the oxide, to the bulk, and an equilibrium condition is reached whereby this field opposes further diffusion of electrons through the external connection. Associated with this field is a built-in potential $\phi_{0}=\phi_{n}-\phi_{p}$ across the gate-bulk structure, where

$$
\begin{equation*}
\phi_{p}=V_{T} \ln \frac{n_{i}}{N_{A}} \quad \phi_{n}=V_{T} \ln \frac{N_{D}}{n_{i}} \tag{3.2}
\end{equation*}
$$

are, respectively, the equilibrium electrostatic potentials (also called Fermi potentials) of the bulk and of the gate. Here, $V_{T}=k T / q$ is the thermal voltage ( $V_{T} \cong 26 \mathrm{mV}$ at $T=300 \mathrm{~K}), N_{A}$ and $N_{D}$ are the doping densities in the bulk and gate materials, and
$n_{i}$ is the intrinsic electron-hole concentration of silicon $\left(n_{i} \cong 1.4 \times 10^{10} / \mathrm{cm}^{3}\right.$ at $T=$ 300 K ). Since both $N_{A}$ and $N_{D}$ are greater than $n_{i}$, we have $\phi_{p}<0$ and $\phi_{n}>0$. Moreover, since $N_{A}$ and $N_{D}$ appear in the argument of the logarithmic function, $\phi_{p}$ and $\phi_{n}$ are not overly sensitive to variations in the doping doses.

An ordinary capacitance with its plates shorted together will be in the discharged state $(Q=0)$. However, if the plates are made of dissimilar materials, as in the present case, we have $Q \neq 0$ even though $V_{G B}=0$. If we want to drive $Q$ to zero as in Fig. $3.3 b$, we need to apply a voltage $V_{G B}$ of equal magnitude but opposite polarity as $\phi_{0}$, or $V_{G B}=-\phi_{0}=\phi_{p}-\phi_{n}$. This value of $V_{G B}(<0)$ is also called the flatband voltage because of its effect on the energy bands of the bulk material. We shall use this voltage as the reference voltage for the analysis to follow.

EXAMPLE 3.1 Assuming $N_{A}=10^{16} / \mathrm{cm}^{3}$ and $N_{D}=10^{20} / \mathrm{cm}^{3}$, find the electrostatic potentials as well as the value of $V_{G B}$ needed to eliminate the space-charge layers.

#### Solution

From Eq. (3.2),

$$
\begin{aligned}
& \phi_{p}=0.026 \ln \frac{1.4 \times 10^{10}}{10^{16}}=-0.35 \mathrm{~V} \\
& \phi_{n}=0.026 \ln \frac{10^{20}}{1.4 \times 10^{10}}=+0.59 \mathrm{~V}
\end{aligned}
$$

To achieve charge neutrality in the gate and bulk, the gate must be biased more negatively than the body such that $V_{G B}=-\phi_{0}=-0.35-0.59=-0.94 \mathrm{~V}$.

Remark: Were the gate-bulk an ordinary $n p$ junction, with $V_{G B}=-0.94 \mathrm{~V}$ it would be forward biased quite heavily and conduct a large forward current from the $p$-bulk (anode) to the $n$-gate (cathode). In the present case, however, no current flows because of the oxide insulator separating the two.

### Inversion

Let us now gradually increase $V_{G B}$, starting at $V_{G B}=-\phi_{0}$ (or $V_{G B}=-0.94 \mathrm{~V}$ in our example). The effect of this increase is to re-establish space-charge layers on both sides of the oxide, uncovering positive charge in the gate and negative charge in the bulk. We are particularly interested in the situation in the bulk, so we will ignore that in the gate, keeping in mind that the charge in the gate is always of equal magnitude but opposite polarity as the charge in the bulk. The situation in the bulk is depicted in Fig. 3.4, where we have chosen the origin of the $x$-axis to coincide with the oxide-bulk interface, a surface that will play an important role in our analysis. Initially, the negative charge in the bulk consists of the negative acceptor ions there (the holes are simply pushed away from the oxide-bulk interface, leaving behind the bound ions). The resulting space-charge layer is also referred to as a depletion layer because it is devoid of holes. However, as we increase $V_{G B}$ and thus widen the depletion layer of the bulk, the surface potential $\phi(0)$
image_name:Figure 3.4
description:
[

]
extrainfo:The diagram illustrates the formation of an inversion layer in an nMOSFET before the onset of strong inversion. It shows the distribution of donor and acceptor ions, the formation of an inversion layer, and the relationship between charge density (ρ), electric field (E), and potential (φ) across the semiconductor. The graph plots these parameters as a function of position (x) from the oxide interface into the semiconductor. The inversion layer is formed near the surface when the surface potential (φ(0)) changes from negative to positive, indicating a transition from p-type to n-type material near the surface.
image_name:ρ (C/cm³)
description:The graph titled "ρ (C/cm³)" is part of a set of graphs depicting the behavior of charge density, electric field, and potential in an nMOSFET before the onset of strong inversion.

1. **Type of Graph and Function:**
- The graph is a charge density plot, which is part of a series illustrating the spatial distribution of charge, electric field, and potential.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \(x\), representing the position across the semiconductor structure.
- The vertical axis is labeled \(ρ\) with units of \(C/cm³\), indicating charge density.
- The graph is linear, with significant markers at \(0\) and \(x_p\), which denote the boundaries of the depletion region.

3. **Overall Behavior and Trends:**
- The charge density \(ρ\) is constant at \(-qN_A\) from \(0\) to \(x_p\), indicating a uniform distribution of negative acceptor ions in the depletion region.
- Beyond \(x_p\), the charge density drops to zero, indicating no net charge.

4. **Key Features and Technical Details:**
- The graph shows a clear boundary at \(x_p\), where the charge density transitions from a constant negative value to zero.
- This behavior is typical of a depletion region where the mobile charge carriers are absent, leaving behind the fixed ionized acceptors.

5. **Annotations and Specific Data Points:**
- The graph is part of a larger illustration, which includes electric field \(E(V/cm)\) and potential \(φ(V)\) plots. These graphs are aligned vertically to show the relationship between charge density, electric field, and potential.
- The charge density \(ρ\) is shown to be negative, consistent with the presence of acceptor ions in the depletion region of a p-type semiconductor.

This graph helps visualize the distribution of charge in the depletion layer of an nMOSFET, which is crucial for understanding the device's operation before strong inversion occurs.
image_name:E (V/cm)
description:The graph labeled "E (V/cm)" in the context of an nMOSFET before the onset of strong inversion illustrates the electric field distribution across the device. The graph is a plot of electric field strength (E) in volts per centimeter (V/cm) against the position (x) within the semiconductor.

Axes Labels and Units:
- **Vertical Axis (Y-Axis):** Represents the electric field strength, labeled as "E (V/cm)."
- **Horizontal Axis (X-Axis):** Represents the position within the semiconductor, labeled as "x."

Overall Behavior and Trends:
- The electric field starts at a maximum value, denoted as \( E_m \), at the oxide-semiconductor interface (x=0).
- It decreases linearly as the position x increases, reaching zero at the point \( x_p \), which is the boundary of the depletion region.
- This linear decrease indicates that the electric field is strongest at the interface and diminishes as it moves further into the bulk of the semiconductor.

Key Features and Technical Details:
- **Maximum Electric Field (\( E_m \)):** The graph starts at this peak value at the interface.
- **Zero Crossing:** The electric field becomes zero at the position \( x_p \), indicating the end of the space-charge region.

Annotations and Specific Data Points:
- The graph is part of a series illustrating charge density (\( \rho \)), electric field (E), and potential (\( \phi \)) across an nMOSFET.
- The electric field profile is crucial for understanding the behavior of the inversion layer and the onset of inversion in the MOSFET device.

This graph is essential for analyzing how the electric field affects the charge carrier distribution and the potential profile within the semiconductor, particularly in the context of device operation before strong inversion occurs.
image_name:ϕ (V)
description:The graph titled "ϕ (V)" is a plot that represents the potential distribution in an nMOSFET device before the onset of strong inversion. It is part of a series of diagrams illustrating the charge distribution, electric field, and potential in the semiconductor.

1. **Type of Graph and Function:**
- The graph is a potential distribution plot, showing how the potential changes across the semiconductor material.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as 'x', representing the position across the semiconductor material.
- The vertical axis is labeled as 'ϕ (V)', representing the electric potential in volts.
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The potential ϕ starts at a value of ϕ(0) at the oxide-semiconductor interface and decreases as it moves into the bulk of the semiconductor.
- The curve is concave upwards, indicating a quadratic dependence of potential on position.
- The potential decreases from ϕ(0) to ϕ_p, showing the transition from the oxide interface into the bulk.

4. **Key Features and Technical Details:**
- The potential at the surface, ϕ(0), is an important parameter as it determines the onset of inversion.
- The potential reaches a minimum value, ϕ_p, at a distance x_p from the interface, indicating the extent of the depletion region.
- The graph shows the potential becoming more negative as it moves into the bulk, highlighting the formation of the depletion layer.

5. **Annotations and Specific Data Points:**
- The graph includes a reference line at 0 volts to indicate the baseline potential level.
- Annotations such as ϕ(0) and ϕ_p are marked to signify the potential at the surface and the minimum potential in the bulk, respectively.
- The position x_p is marked to show the extent of the depletion region.

FIGURE 3.4 The situation in a nMOSFET before the onset of strong inversion.
also increases because of the quadratic dependence $\phi$ versus $x$ (recall Fig. 1.39). When $\phi(0)$ changes from negative to positive, the bulk near the surface is said to undergo inversion because it turns from $p$-type to $n$-type, at least electrostatically speaking. For this reason, the bulk region near the surface is called inversion layer.

With reference to Fig. 3.4, we observe that the space-charge layers yield in turn an electric field $E(x)$. The field strength as a function of $x$ is readily visualized by counting the field lines, each of which starts on a positive ion in the gate and ends on a negative ion in the bulk. We are interested in the lines in the bulk, whose number is maximum at the oxide-bulk interface ( $x=0$ ), and decreases linearly with $x$ to finally drop to zero at the edge of the depletion layer $\left(x=x_{p}\right)$. We readily find a relationship between the maximum strength $E_{m}$ and the layer's width $x_{p}$ using Gauss's theorem.

In a one-dimensional case such as ours, this theorem is expressed as $d E / d x=\rho / \varepsilon_{s i}$, where $\rho$ is the charge density in the depletion layer ( $\rho=-q N_{A}$ ), and $\varepsilon_{s i}$ is silicon's permittivity $\left(\varepsilon_{s i}=1.04 \mathrm{pF} / \mathrm{cm}\right)$. By inspection, $d E / d x=-E_{m} / x_{p}=-q N_{A} / \varepsilon_{s i}$, so

$$
\begin{equation*}
E_{m}=\frac{q N_{A} x_{p}}{\varepsilon_{s i}} \tag{3.3}
\end{equation*}
$$

Electric field and potential are in turn related as $E=-d \phi / d x$. Rewriting as $d \phi=$ $-E d x$ and integrating both sides from $x=0$ to $x=x_{p}$, we get

$$
\int_{0}^{x_{p}} d \phi=-\int_{0}^{x_{p}} E(x) d x
$$

The term at the left is simply the difference $\phi_{p}-\phi(0)$, while the term at the right is the area of the triangle under the $E$ curve, or $1 / 2\left(x_{p} \times E_{m}\right)$, so

$$
\phi_{p}-\phi(0)=-\frac{E_{m} x_{p}}{2}
$$

Using Eq. (3.3) to eliminate $E_{m}$, we obtain an expression for the depletion-layer width as a function of the surface potential $\phi(0)$,

$$
x_{p}=\sqrt{\frac{2 \varepsilon_{s i}}{q N_{A}}\left[\phi(0)-\phi_{p}\right]}
$$

### Onset of Strong Inversion

We are interested in the situation in which the surface potential attains the value $\phi(0)=-\phi_{p}$ (or +0.35 V in our example), for then the electron concentration $n$ in the inversion layer becomes equal to the hole concentration $p$ in the bulk, or $n=N_{A}$ $\left(=10^{16} / \mathrm{cm}^{3}\right.$ in our example). This situation, depicted in Fig. 3.5, is said to mark the onset of strong inversion. Using subscript 0 to mark this onset, we now wish to find the gate-body bias $V_{G B 0}$ required to bring about this onset itself. To this end, we first substitute $\phi(0)=-\phi_{p}$ to find the depletion-layer width at the onset of strong inversion

$$
\begin{equation*}
x_{p 0}=\sqrt{\frac{2 \varepsilon_{s i}}{q N_{A}} 2\left(-\phi_{p}\right)} \tag{3.4}
\end{equation*}
$$

Next, we observe that the unit-area charge in the bulk depletion-layer is $Q_{b 0}=-q N_{A} x_{p 0}$. Using Eq. (3.4),

$$
\begin{equation*}
Q_{b 0}=-\sqrt{2 q N_{A} \varepsilon_{s i} 2\left(-\phi_{p}\right)} \tag{3.5}
\end{equation*}
$$

This negative charge in the bulk is matched by a positive charge in the gate. By the capacitance law, the voltage required to sustain this charge redistribution is $V_{o x 0}=$ - $Q_{b 0} / C_{o x}$. Finally, the gate-to-body voltage drop required to bring about the onset of strong inversion is, by KVL, $V_{G B 0}=-\phi_{0}+2\left(-\phi_{p}\right)+V_{o x 0}$, or

$$
\begin{equation*}
V_{G B 0}=-\phi_{0}-2 \phi_{p}-\frac{Q_{b 0}}{C_{o x}} \tag{3.6}
\end{equation*}
$$

image_name:FIGURE 3.5 Situation at the onset of strong inversion.
description:The diagram titled "FIGURE 3.5 Situation at the onset of strong inversion" illustrates the conditions and charge distribution in a semiconductor device at the onset of strong inversion. The graph and accompanying schematic depict the relationships between charge, voltage, and position within the device.

1. **Type of Graph and Function:**
- The graph is a combination of a schematic diagram and a plot showing potential distribution within a semiconductor.

2. **Axes Labels and Units:**
- The x-axis is labeled as position \( x \) and does not have specific units marked, but it represents spatial position in the semiconductor.
- The y-axis represents potential \( \phi \) in volts (V) and charge density \( \rho \) in coulombs per cubic centimeter (C/cm³).

3. **Overall Behavior and Trends:**
- The potential \( \phi \) starts at zero at the gate and decreases to \(-\phi_p\) at the semiconductor surface. It then increases back to \( \phi_p \) as it moves into the bulk of the semiconductor.
- The charge density \( \rho \) is shown as negative \(-qN_A\) in the bulk, indicating a p-type substrate.

4. **Key Features and Technical Details:**
- The diagram shows the presence of donor ions, electrons, and acceptor ions, with an inversion layer forming at the interface between the gate oxide (SiO2) and the semiconductor.
- The potential drop across the oxide is labeled as \( V_{ox0} \), and the potential change required to achieve strong inversion is marked as \( 2(-\phi_p) \).
- The position \( x_{p0} \) indicates the boundary of the depletion region.

5. **Annotations and Specific Data Points:**
- The schematic diagram includes annotations for the gate \( G \), the inversion layer, and the various charges (donor ions, electrons, acceptor ions).
- The potential \( \phi \) at the surface is shown transitioning from \(-\phi_p\) to \( \phi_p \), with specific reference lines indicating these potential levels.
- The diagram provides a visual representation of the voltage \( V_{GB0} \) required to initiate strong inversion, highlighting the electrostatic conditions necessary for this state.

FIGURE 3.5 Situation at the onset of strong inversion.

In other words, to bring about the onset of strong inversion, we need to increase $V_{G B}$, starting from the reference level $-\phi_{0}$, (a) by the term $2\left(-\phi_{p}\right)$ to raise the surface potential $\phi(0)$ from $\phi_{p}$, through zero, to $-\phi_{p}$, and (b) by the term $-Q_{b 0} / C_{o x}$ to sustain the unit-area charge $Q_{b 0}$ in the bulk depletion layer.

Assuming the doping densities of Example 3.1, along with $t_{o x}=25 \mathrm{~nm}$, find the values of all relevant physical quantities right at the onset of strong inversion.

#### Solution

The unit-area capacitance is

$$
C_{o x}=\frac{345 \times 10^{-15}}{2.5 \times 10^{-6}}=138 \mathrm{nF} / \mathrm{cm}^{2}
$$

At the onset of strong inversion, the depletion layer width is

$$
x_{p 0}=\sqrt{\frac{2 \times 1.04 \times 10^{-12}}{1.602 \times 10^{-19} \times 10^{16}} 2(0.35)}=301 \mathrm{~nm}
$$

The corresponding electric field intensity is

$$
E_{m 0}=\frac{1.602 \times 10^{-19} \times 10^{16} \times 30.1 \times 10^{-6}}{1.04 \times 10^{-12}}=46.4 \mathrm{kV} / \mathrm{cm}
$$

The unit-area charge in the bulk depletion-layer is

$$
Q_{b 0}=-\sqrt{4 \times 1.602 \times 10^{-19} \times 10^{16} \times 1.04 \times 10^{-12}(0.35)}=-48.3 \mathrm{nC} / \mathrm{cm}^{2}
$$

Finally, the required gate-body voltage drop is, by Eq. (3.6),

$$
V_{G B 0}=-0.94-2(-0.35)-\frac{-48.3}{138}=-0.94+0.70+0.35=+0.11 \mathrm{~V}
$$

Once strong inversion is reached, the surface potential $\phi(0)$ and, hence, the depletion-layer width $x_{p}$, will change very little with the applied voltage $V_{G B}$ because $\phi(0)$ depends on $V_{G B}$ only logarithmically. Any increase $\Delta V_{G B}$ above $V_{G B 0}$ will essentially be accompanied by an increase $\Delta Q_{n} \cong-C_{o x} \Delta V_{G B}$ in the unit-area electron charge of the inversion layer. These electrons are supplied by the $n^{+}$source region (hence the name), where they exist in abundant supply. In fact, in order for these electrons to be enticed into the inversion layer, the gate must slightly overlap the source region to allow for the fringe electric field to attract electrons from the source to the channel. As mentioned, the advantage of the silicon-gate process is that it is a self-aligning process.

EXAMPLE 3.3 Assuming the data of Example 3.2, find the change $\Delta Q_{n}$ brought about by a 1-V increase $\Delta V_{G B}$ in strong inversion. Compare with the depletion-layer charge $Q_{b 0}$.

#### Solution

We have $\Delta Q_{n} \cong-C_{o x} \Delta V_{G B}=-\left(138 \mathrm{nF} / \mathrm{cm}^{2}\right) \times(1 \mathrm{~V})=-138 \mathrm{nC} / \mathrm{cm}^{2}$, indicating that the inversion-layer charge $\left|\Delta Q_{n}\right|$ can be significantly greater than the depletionlayer charge $\left|Q_{b 0}\right|\left(=48.3 \mathrm{nC} / \mathrm{cm}^{2}\right.$ in our example), even though the inversion layer is much thinner than the depletion layer.

### The Threshold Voltage $\mathbf{V}_{t 0}$

We now wish to apply the above findings to the full-fledged MOSFET, starting from the situation at the onset of strong inversion depicted in Fig. 3.6 for both MOSFET types. Note the presence of the inversion layer immediately below the oxide-bulk surface, along with the depletion layer extending not only below the inversion layer, but also around the source and drain regions, as they form $p n$ junctions with the body. The threshold voltage $V_{t}$ is defined as the gate-source voltage $v_{G S}$ needed to bring about the onset of strong inversion in the channel region. When body and source are at the same potential (ground in Fig. 3.6), the threshold is denoted as $V_{t 0}$. For the case of an $n$ MOSFET it takes on the general form

$$
\begin{equation*}
V_{t 0}=-\phi_{0}-2 \phi_{p}-\frac{Q_{b 0}}{C_{o x}}-\frac{Q_{o x}}{C_{o x}}-\frac{Q_{i}}{C_{o x}} \tag{3.7}
\end{equation*}
$$

image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: GND, G: Vtn0}
]
extrainfo:The diagram shows the onset of strong inversion in an nMOSFET with the body grounded. The gate-source voltage is Vtn0 (>0).
image_name:(b)
description:
[
name: (b), type: PMOS, ports: {S: VDD, D: GND, G: G, B: GND}
]
extrainfo:The diagram illustrates the onset of strong inversion in a PMOS transistor. The source is connected to VDD, the drain is connected to ground, the gate is labeled as G, and the body is also connected to ground. The PMOS is in a configuration where the gate-source voltage V_GS is less than the threshold voltage V_tp0, indicating the condition for strong inversion.

FIGURE 3.6 The onset of strong inversion in (a) the $n$ MOSFET and (b) the pMOSFET.

The first three terms are simply those of Eq. (3.6). The next term, involving the unitarea charge $Q_{o x}$, accounts for the presence of dangling bonds in the bulk right at the interface, as well as positive ions that during fabrication get trapped in the oxide right near the oxide-bulk interface. ${ }^{2}$ The first four terms form what is known as the native threshold of the $n$ MOSFET. The last term, involving the unit-area charge $Q_{i}$, accounts for impurities that the manufacturer introduces deliberately in the bulk, right at the oxide-bulk interface, to adjust $V_{t 0}$ to the prescribed value. For $p$-type impurities we have $Q_{i}<0$, and for $n$-type impurities we have $Q_{i}>0$. For obvious reasons, the native threshold is also called the undoped threshold.

Assuming the data of Example 3.2, along with a surface state density $N_{o x}=$ $2 \times 10^{11}$ positive ions/ $\mathrm{cm}^{2}$,
(a) Find the native threshold of the $n$ MOSFET.
(b) Find the implant type and dosage $N_{i}$ needed for $V_{t 0}=+1.0 \mathrm{~V}$.
(c) Find the implant type and dosage $N_{i}$ needed for $V_{t 0}=-1.0 \mathrm{~V}$.

#### Solution

(a) We have $Q_{o x}=q N_{o x}=1.602 \times 10^{-19} \times 2 \times 10^{11}=32 \mathrm{nC} / \mathrm{cm}^{2}$. So, using the result of Example 3.2,

$$
V_{t 0}=0.11-\frac{32}{138}=-0.122 \mathrm{~V}
$$

(b) To raise $V_{t 0}=$ from its native value of -0.122 V to +1.0 V , we need a $p$-type implant, such as boron, which will contribute negative ions ( $Q_{i}<0$ ) in the bulk near the surface. Imposing

$$
+1.0=-0.122-\frac{Q_{i}}{C_{o x}}=-0.122-\frac{-q N_{i}}{C_{o x}}=-0.122+\frac{1.602 \times 10^{-19} N_{i}}{138 \times 10^{-9}}
$$

gives $N_{i}=9.66 \times 10^{11} p$-type ions $/ \mathrm{cm}^{2}$.
(c) To lower $V_{t 0}$ from its native value of -0.122 V to -1.0 V , we need an $n$-type implant, such as phosphorus, which will contribute positive ions ( $Q_{i}>0$ ) in the bulk near the surface. Imposing

$$
-1.0=-0.122-\frac{Q_{i}}{C_{o x}}=-0.122-\frac{q N_{i}}{C_{o x}}=-0.122-\frac{1.602 \times 10^{-19} N_{i}}{138 \times 10^{-9}}
$$

$$
\text { gives } N_{i}=7.56 \times 10^{11} n \text {-type ions } / \mathrm{cm}^{2} \text {. }
$$

#### Exercise 3.1

Show that for a polysilicon-gate technology the first two terms in the threshold voltage of an $n$ MOSFET can be expressed concisely as

$$
-\phi_{0}-2 \phi_{p}=V_{T} \ln \left(N_{A} / N_{D}\right)
$$

### The Four MOSFET Types and Their Circuit Symbols

Depending on the body type ( $p^{-}$or $n^{-}$) and threshold-voltage polarity ( $V_{t}>0$ or $V_{t}<0$ ), we can have four different types of MOSFET. We now make some important observations:

- An $n$ MOSFET with $V_{t 0}>0$ is said to be normally off because with $v_{G S}=0$ there is no channel present. We need to raise $V_{G S}$ above $V_{t 0}(>0)$ in order to create a channel or, equivalently, to enhance the channel-region conductivity. This type of device is aptly referred to as enhancement nMOSFET. The higher the ( $p$-type) implant dosage, the more positive the value of $V_{t 0}$. The circuit symbol for this device, shown in Fig. 3.7a, uses a broken line to signify a normally nonconductive channel.
- An $n$ MOSFET with $V_{t 0}<0$ is said to be normally on because with $v_{G S}=0$ there is already a channel present. In this case we need to lower $v_{G S}$ below $V_{t 0}(<0)$ in order to eliminate the channel or, equivalently, to deplete the channel region of its free electrons. This device type is aptly referred to as depletion $n$ MOSFET. The higher the ( $n$-type) implant dosage, the more negative the value of $V_{t 0}$. The circuit symbol for this device, shown in Fig. 3.7b, uses a continuous line to signify a normally conductive channel.
- A $p$ MOSFET with $V_{t 0}<0$ is said to be normally off because with $v_{G S}=0$ there is no channel present. We need to lower $v_{G S}$ below $V_{t 0}(<0)$ in order to create a
image_name:Enhancement n-ch. (a)
description:
[
name: M1, type: NMOS, ports: {S: S, D: D, G: G, B: B}
]
extrainfo:The diagram shows a PMOS transistor with its source (S), drain (D), gate (G), and body (B) labeled. It is likely part of a larger circuit, but only the PMOS symbol is visible here.

Enhancement $n$-ch.
(a)
image_name:Enhancement n-ch. (a)
description:
[
name: M2, type: NMOS, ports: {S: S, D: D, G: G, B: B}
]
extrainfo:The diagram shows a PMOS transistor with its source (S), drain (D), gate (G), and body (B) labeled. It is likely part of a larger circuit, but only the PMOS symbol is visible here.

Depletion $n$-ch.
(b)

Enhancement $p$-ch.
(c)
image_name:Enhancement $p$-ch. (c)
description:
[
name: M1, type: PMOS, ports: {S: B, D: D, G: G}
]
extrainfo:The diagram shows an NMOS transistor with labeled gate (G), source (S), drain (D), and body (B) connections.

Depletion $n$-ch.
(d)

FIGURE 3.7 Full-fledged circuit symbols for the four MOSFET types.
image_name:FIGURE 3.7 Full-fledged circuit symbols for the four MOSFET types
description:
[
name: GDS, type: NMOS, ports: {S: S, D: D, G: G}
name: GDS, type: PMOS, ports: {S: S, D: D, G: G}
]
extrainfo:The diagram shows the transition from a depletion-mode NMOS transistor symbol to an enhancement-mode PMOS transistor symbol. Both symbols depict the gate (G), source (S), and drain (D) connections.

Depletion $n$-ch.
image_name:FIGURE 3.7 Full-fledged circuit symbols for the four MOSFET types
description:
[
name: Left Device, type: NMOS, ports: {S: S, D: D, G: G}
name: Right Device, type: PMOS, ports: {S: S, D: D, G: G}
]
extrainfo:The diagram shows the transition from a depletion-mode NMOS transistor symbol to an enhancement-mode PMOS transistor symbol, depicting the gate (G), source (S), and drain (D) connections.

Enhancement $p$-ch.
image_name:FIGURE 3.7 Full-fledged circuit symbols for the four MOSFET types
description:
[
name: Left Device, type: NMOS, ports: {S: S, D: D, G: G}
name: Right Device, type: PMOS, ports: {S: S, D: D, G: G}
]
extrainfo:The diagram illustrates the transition from a depletion-mode NMOS transistor symbol to an enhancement-mode PMOS transistor symbol, showing the gate (G), source (S), and drain (D) connections.

Depletion $p$-ch.

Enhancement $n$-ch.

FIGURE 3.8 Simplified circuit symbols for the four MOSFET types.
channel, or, equivalently, to enhance its channel conductivity. Aptly called enhancement $p$ MOSFET, this device is shown in Fig. 3.7c.

- A $p$ MOSFET with $V_{t 0}>0$ is said to be normally on because with $v_{G S}=0$ there is already a channel. If we want to deplete it of its free holes, we need to raise $v_{G S}$ above $V_{t 0}(>0)$. The circuit symbol of this device, aptly called depletion $p$ MOSFET, is shown in Fig. 3.7d.

The preferred mode of operation of a MOSFET is with the body tied to the source, resulting in a three-terminal device. This is the case, for instance, of discrete devices. Figure 3.8 shows the simplified MOSFET symbols most commonly used for this type of connection. To avoid the awkward broken lines, the enhancement types are given solid lines. To signify that the channels of the depletion types are already present, thicker lines are used.

### The Body Effect and the Threshold Voltage $\boldsymbol{V}_{\boldsymbol{t}}$

When multiple devices share the same substrate, the latter must be tied to the most negative voltage (MNV) to avoid inadvertently turning on any of the body-source or body-drain pn junctions. Likewise, the common substrate of $p$ MOSFETs must be tied to the most positive voltage (MPV). It is thus possible for the source of an $n$ MOSFET to find itself at a higher voltage than the body, or $V_{S}>V_{B}$ (likewise, we can have $V_{S}<V_{B}$ for a $p$ MOSFET). We wish to investigate the effect of body bias on the threshold voltage of an $n$ MOSFET.

Denoting the source-body voltage of an $n$ MOSFET as $V_{S B}\left(V_{S B} \geq 0\right)$, we can simply recycle our previous findings by replacing [2( $\left.\left.-\phi_{p}\right)\right]$ with $\left[2\left(-\phi_{p}\right)+V_{S B}\right]$ in Eq. (3.5). The result is

$$
Q_{b}=-\sqrt{2 q N_{A} \varepsilon_{s i}\left(V_{S B}+2\left|\phi_{p}\right|\right)}
$$

where we are using the absolute value of $\phi_{p}\left(\phi_{p}<0\right)$ to reduce the possibility of confusion. Clearly, the increase in the depletion-region charge $Q_{b}\left(Q_{b}>0\right)$ comes at the expense of a simultaneous decrease in the inversion-layer charge $Q_{n}\left(Q_{n}<0\right)$. To return the channel to its former state we need to suitably increase $v_{G S}$. To find out by how much, we rewrite Eq. (3.7) as

$$
\begin{aligned}
V_{t} & =-\phi_{0}-2 \phi_{p}-\frac{Q_{b}}{C_{o x}}-\frac{Q_{o x}}{C_{o x}}-\frac{Q_{i}}{C_{o x}}=-\phi_{0}-2 \phi_{p}-\frac{Q_{b 0}}{C_{o x}}-\frac{Q_{o x}}{C_{o x}}-\frac{Q_{i}}{C_{o x}}-\frac{Q_{b}-Q_{b 0}}{C_{o x}} \\
& =V_{t 0}-\frac{Q_{b}-Q_{b 0}}{C_{o x}}
\end{aligned}
$$

We can concisely express the threshold voltage in the insightful form

$$
\begin{equation*}
V_{t}=V_{t 0}+\gamma\left[\sqrt{V_{S B}+2\left|\phi_{p}\right|}-\sqrt{2\left|\phi_{p}\right|}\right] \tag{3.8}
\end{equation*}
$$

where $V_{t 0}$ is the zero-body-bias value of $V_{t}$ as given in Eq. (3.7), and

$$
\begin{equation*}
\gamma=\frac{\sqrt{2 q N_{A} \varepsilon_{s i}}}{C_{o x}} \tag{3.9}
\end{equation*}
$$

is called the body-effect parameter. Its value, in $\mathrm{V}^{1 / 2}$, is typically on the order of a fraction of $1 \mathrm{~V}^{1 / 2}$.

EXAMPLE 3.5 (a) For the enhancement $n$ MOSFET of Example $3.4 b$, which has $V_{t 0}=1.0 \mathrm{~V}$, find $V_{t}$ at $V_{S B}=1 \mathrm{~V}$, as well as at $V_{S B}=5 \mathrm{~V}$.
(b) For the depletion nMOSFET of Example $3.4 c$, which has $V_{t 0}=-1.0 \mathrm{~V}$, find $V_{t}$ at $V_{S B}=1 \mathrm{~V}$, as well as at $V_{S B}=5 \mathrm{~V}$. For what value of $V_{S B}$ do we get $V_{t}=-0.5 \mathrm{~V}$ ?

#### Solution

$$
\gamma=\frac{\sqrt{2 \times 1.602 \times 10^{-19} \times 10^{16} \times 1.04 \times 10^{-12}}}{138 \times 10^{-9}}=0.418 \mathrm{~V}^{1 / 2}
$$

(a) For the enhancement $n \mathrm{MOSFET}$ we have

$$
\begin{aligned}
& V_{t}\left(V_{S B}=1 \mathrm{~V}\right)=1.0+0.418(\sqrt{1+0.7}-\sqrt{0.7})=1.0+0.195=1.195 \mathrm{~V} \\
& V_{t}\left(V_{S B}=5 \mathrm{~V}\right)=1.0+0.418(\sqrt{5+0.7}-\sqrt{0.7})=1.0+0.648=1.648 \mathrm{~V}
\end{aligned}
$$

(b) For the depletion $n$ MOSFET we have

$$
\begin{aligned}
& V_{t}\left(V_{S B}=1 \mathrm{~V}\right)=-1.0+0.418(\sqrt{1+0.7}-\sqrt{0.7})=-1.0+0.195=-0.805 \mathrm{~V} \\
& V_{t}\left(V_{S B}=5 \mathrm{~V}\right)=-1.0+0.418(\sqrt{5+0.7}-\sqrt{0.7})=-1.0+0.648=-0.352 \mathrm{~V}
\end{aligned}
$$

Imposing

$$
-0.5=-1.0+0.418\left(\sqrt{V_{S B}+0.7}-\sqrt{0.7}\right)
$$

gives $V_{S B}=3.43 \mathrm{~V}$.

The example indicates that the effect of body bias is to shift the threshold voltage of an $n$ MOSFET in the positive direction, regardless of whether it is a depletion or enhancement type. By contrast, for a $p$ MOSFET the shift is in the negative direction. Adapted to the $p$ MOSFET case, Eq. (3.8) becomes

$$
\begin{equation*}
V_{t}=V_{t 0}-\gamma\left[\sqrt{V_{B S}+2 \phi_{n}}-\sqrt{2 \phi_{n}}\right] \tag{3.10}
\end{equation*}
$$

where $\gamma$ is still given by Eq. (3.9), but with $N_{A}$ replaced by $N_{D}$. The dependence of $V_{t}$ upon the body bias is referred to as the body effect, and the body itself is sometimes
referred to as back gate because it influences the inversion layer like the gate, though in the opposite direction and also in square-root fashion.

A certain enhancement $p$ MOSFET has $V_{t 0}=-1.5 \mathrm{~V}$ and $\gamma=0.5 \mathrm{~V}^{1 / 2}$. If EXAMPLE 3.6 $\phi_{n}=+0.3 \mathrm{~V}$, find $V_{t}$ at $V_{B S}=3 \mathrm{~V}$.

#### Solution

$V_{t}\left(V_{B S}=3 \mathrm{~V}\right)=-1.5-0.5(\sqrt{3+2 \times 0.3}-\sqrt{2 \times 0.3})=-1.5-0.56=-2.06 \mathrm{~V}$
As mentioned, body bias causes a negative shift in the threshold voltage of a $p$ MOSFET, regardless of the polarity of $V_{t 0}$.

## 3.3 THE n-CHANNEL CHARACTERISTIC

We are now ready to investigate the $i-v$ characteristics of the $n$-channel, anticipating that our understanding of the $p$-channel will follow easily once we have mastered the $n$-channel. Figure 3.9 shows the sequence of situations an $n$-channel goes through as we gradually increase $v_{D S}$ starting out with $v_{D S} \cong 0$. Once the MOSFET is biased in strong inversion, its channel can be viewed as a resistor of length $L$, width $W$, and thickness proportional to the overdrive voltage, which is defined as the amount by which the gate-source voltage exceeds the threshold voltage $V_{t}$,

$$
\begin{equation*}
V_{O V}=V_{G S}-V_{t} \tag{3.11}
\end{equation*}
$$

For instance, in the device of Example 3.3, every volt of $V_{O V}$ induces an electron charge of $-138 \mathrm{nC} / \mathrm{cm}^{2}$ in the channel, so the greater $V_{O V}$, the more conductive the channel will be. If we now apply a voltage $v_{D S}>0$ to the drain, electrons will drift from the source, through the channel, to the drain, like in an ordinary resistor (hence the designation ohmic for this region of operation), thus producing current. But, electrons are negative, so the current $i_{D}$ at the drain terminal will flow into the device, as shown in Fig. 3.9a. The source and drain designations reflect the fact that mobile charges (electrons in $n$ MOSFETS, holes in $p$ MOSFETs) are sourced to the channel at one end, and drained from the channel at the other.

### The Triode Region

If we now increase $v_{D S}$ further, an interesting effect occurs, namely, the channel becomes tapered, as depicted in Fig. 3.9b. This stems from the fact that while at the source end we have $V_{O V}=V_{G S}-V_{t}$, at the drain end we only have $V_{O V}=\left(V_{G S}-v_{D S}\right)-V_{t}$, indicating a thinner channel there. For instance, let $V_{t}=1 \mathrm{~V}, V_{G S}=5 \mathrm{~V}$, and $v_{D S}=$ 2 V . Then, the overdrive at the source end is $V_{O V(\text { source })}=5-1=4 \mathrm{~V}$, but that at the drain end is only $V_{O V(\text { drain })}=(5-2)-1=2 \mathrm{~V}$. In this example, the channel at the drain end is only half as thick as at the source end.

To investigate quantitatively, refer to Fig. 3.10, where we imagine that we have sliced the channel like a loaf of bread, and we focus on the slice of width $d y$ located
image_name:FIGURE 3.9
description:The diagram illustrates an NMOS transistor with gate-source voltage VGS greater than the threshold voltage Vt, and a small drain-source voltage VDS. The channel is formed between the source and drain terminals, and a depletion layer is shown. The body is connected to ground.

(a)
image_name:(a)
description:The circuit diagram illustrates an NMOS transistor operating in the ohmic region with VGS > Vt and a small VDS. The channel is formed between the source and drain, with a depletion layer visible. The body is connected to ground.

(b)
image_name:Figure 3.9 (c)
description:The circuit diagram illustrates an NMOS transistor operating at the edge of saturation (pinch-off point) with VGS > Vt and VDS = VGS - Vt. The body is connected to ground, and current iD flows from the drain to the source.

(c)
image_name:(d)
description:The diagram illustrates an NMOS transistor in the saturation, or active region, labeled as (d). The key components and structure are as follows:

1. **Components and Structure:**
- **NMOS Transistor:** The main element shown is an NMOS transistor with three primary terminals: Source (S), Gate (G), and Drain (D). The body (B) is also depicted and connected to ground.
- **Voltage Sources:** Two voltage sources are indicated:
- **VGS (Gate-Source Voltage):** This is greater than the threshold voltage (Vt), ensuring the transistor is on.
- **VDS (Drain-Source Voltage):** This is greater than \(V_{GS} - V_t\), indicating the transistor is in the saturation region.
- **Current Flow (iD):** The current flows from the drain to the source.

2. **Connections and Interactions:**
- The source (S) is connected to a voltage source labeled as VGS, which controls the gate voltage.
- The drain (D) is connected to the voltage source VDS, which provides the drain voltage.
- The gate (G) is directly connected to the VGS source, and the body (B) is grounded.
- The interaction between VGS and VDS ensures the transistor operates in the saturation region, allowing for maximum current flow through the channel.

3. **Labels, Annotations, and Key Features:**
- **VGS > Vt:** Indicates the condition where the gate-source voltage is greater than the threshold voltage, turning the transistor on.
- **VDS > (VGS - Vt):** Specifies the condition for saturation, where the drain-source voltage exceeds the gate-source voltage minus the threshold voltage.
- **Channel Length Modulation:** The diagram shows a channel with length L and a modulation effect \(\Delta L\), illustrating the pinch-off effect typical in saturation.
- **n+ Regions:** These are the heavily doped source and drain regions, which are typical in NMOS structures.

This diagram effectively represents the NMOS transistor operating in the saturation region, emphasizing the conditions and structural elements that define this mode of operation.

FIGURE 3.9 Illustrating the different regions of operation of the $n$ MOSFET: (a) ohmic, (b) triode, (c) pinch-off, or edge of saturation (EOS), and (d) saturation, or active region.
image_name:FIGURE 3.10
description:The image depicts a detailed schematic of an n-channel MOSFET (nMOS) operating in the triode region. The structure includes the following components:

1. **Source (S), Gate (G), and Drain (D):** These are the three primary terminals of the MOSFET. The source is connected to a ground symbol, and the gate is connected to a voltage source labeled $V_{GS} > V_{t}$, indicating that the gate-source voltage is greater than the threshold voltage. The drain is connected to a current source and a voltage source labeled $i_D$ and $v_{DS} < (V_{GS} - V_{t})$, respectively.

2. **n+ Regions:** These are the heavily doped source and drain regions, typical in NMOS structures. They are indicated as n+ in the diagram.

3. **Channel Region:** The channel is formed between the source and drain, and a charge packet $dQ_n$ is shown within this region. The channel length is denoted by $L$, and the width by $W$.

4. **Oxide Layer ($t_{ox}$):** This thin layer separates the gate from the channel, providing the gate capacitance that controls the channel conductivity.

5. **Substrate (B):** The bulk or body of the MOSFET is shown grounded, indicating a common configuration where the substrate is connected to the lowest potential.

6. **Distance and Voltage:** The diagram includes a horizontal line from 0 to $y$ to $L$, with $dy$ indicating a small slice of the channel. The voltage at this slice varies from 0 V at the source to $v_{DS}$ at the drain.

**Connections and Interactions:**
- The gate voltage ($V_{GS}$) controls the channel conductivity by inducing charge in the channel. The drain-source voltage ($v_{DS}$) is less than the overdrive voltage ($V_{GS} - V_{t}$), placing the MOSFET in the triode region where it behaves like a variable resistor.
- Current $i_D$ flows from drain to source, influenced by both $V_{GS}$ and $v_{DS}$.

**Labels and Annotations:**
- $V_{GS} > V_{t}$: Gate-source voltage greater than threshold voltage.
- $v_{DS} < (V_{GS} - V_{t})$: Drain-source voltage is less than the gate overdrive voltage.
- $dQ_n$: Charge packet in the channel.
- $t_{ox}$: Thickness of the oxide layer.
- $W$: Width of the channel.
- $L$: Length of the channel.
- $dy$: Small slice of the channel indicating differential analysis.

FIGURE 3.10 The $n$ MOSFET in the triode region.
at some distance $y$ from the source. The voltage at each slice varies from 0 V at the leftmost slice to $v_{D S}$ at the rightmost slice, so the voltage $v(y)$ at our particular slice will lie somewhere in between, or $0 \leq v(y) \leq v_{D S}$. Now, the gate strip immediately above our slice forms a capacitance $d C=C_{o x} \times W \times d y$ with the channel itself, so the charge packet $d Q_{n}$ induced in the channel is, by the capacitance law,

$$
d Q_{n}=-d C\left\{\left[V_{G S}-v(y)\right]-V_{t}\right\}=-C_{o x} W d y\left[V_{G S}-V_{t}-v(y)\right]
$$

(This charge is negative because it consists of electrons.) The voltage drop $v_{D S}$ across the channel produces an electric field $E$ inside the channel, oriented from drain to source. This field, in turn, causes the negative charge packet $d Q_{n}$ to drift toward the drain, thus producing the current $i_{D}$. By definition,

$$
i_{D}=-\frac{d Q_{n}}{d t}=C_{o x} W\left[V_{G S}-V_{t}-v(y)\right] \frac{d y}{d t}
$$

where $d y / d t$ represents the velocity with which $d Q_{n}$ drifts toward the drain. This velocity is proportional to the electric field, or $d y / d t=-\mu_{n} E(y)$, where $\mu_{n}$ is the electron mobility. (The negative sign stems from the fact that electrons drift against the electric field.) But, electric field and potential are related as $E(y)=-d v(y) / d y$, so $d y / d t=\mu_{n} d v(y) / d y$. Substituting in the above equation gives

$$
i_{D}=\mu_{n} C_{o x} W\left[V_{G S}-V_{t}-v(y)\right] \frac{d v(y)}{d y}
$$

Multiplying both sides by $d y$ and integrating from $y=0$, where $v(y)=0$, to $y=L$, where $v(y)=v_{D S}$, we get

$$
\int_{0}^{L} i_{D} d y=\mu_{n} C_{o x} W \int_{0}^{v_{D S}}\left[V_{G S}-V_{t}-v(y)\right] d v(y)
$$

The left side integrates to $i_{D} L$, and the right side integrates to $\left(V_{G S}-V_{t}\right) v_{D S}-1 / 2 v_{D S}^{2}$. This allows us to express $i_{D}$ in the following insightful form

$$
\begin{equation*}
i_{D}=k\left[\left(V_{G S}-V_{t}\right) v_{D S}-\frac{1}{2} v_{D S}^{2}\right] \tag{3.12}
\end{equation*}
$$

where the quantity

$$
\begin{equation*}
k=k^{\prime} \frac{W}{L} \tag{3.13}
\end{equation*}
$$

is called the device transconductance parameter. This is simply a scale factor, in $\mathrm{A} / \mathrm{V}^{2}$, that indicates how much current a device will draw for a given set of $V_{G S}, V_{t}$, and $v_{D S}$ values. The IC designer can tailor the value of $k$ to meet given needs by suitably specifying the device's dimensions $W$ and $L$; hence, the reason for using the qualifier device. The quantity

$$
\begin{equation*}
k^{\prime}=\mu_{n} C_{o x}=\frac{\mu_{n} \varepsilon_{o x}}{t_{o x}} \tag{3.14}
\end{equation*}
$$

is called the process transconductance parameter, in $\mathrm{A} / \mathrm{V}^{2}$. Being common to all devices, it is unique of the particular fabrication process; hence, the reason for the qualifier process. Figure 3.11 shows the plot of $i_{D}$ versus $v_{D S}$ for a given overdrive voltage $V_{O V}$.

We observe that near the origin, where $v_{D S}$ is small enough to render the quadratic term negligible in Eq. (3.12), the $i_{D}-v_{D S}$ characteristic approaches, for a given gatesource drive $V_{G S}$, a straight line, or

$$
\begin{equation*}
i_{D} \cong k\left(V_{G S}-V_{t}\right) v_{D S} \tag{3.15}
\end{equation*}
$$

For this reason, the region corresponding to small values of $v_{D S}$ is called the linear region. Rewriting Eq. (3.15) in the form of Ohm's law as

$$
\begin{equation*}
i_{D}=\frac{1}{r_{D S}} v_{D S} \tag{3.16}
\end{equation*}
$$

image_name:FIGURE 3.11
description:The graph in FIGURE 3.11 is a plot of the drain current ($i_D$) versus the drain-source voltage ($v_{DS}$), which is characteristic of a MOSFET for a given overdrive voltage $V_{OV} = V_{GS} - V_t > 0$.

Axes Labels and Units:
- **X-axis:** Represents the drain-source voltage ($v_{DS}$) in volts. It is marked from 0 onwards, indicating positive voltage values.
- **Y-axis:** Represents the drain current ($i_D$) in amperes, starting from 0 and increasing.

Overall Behavior and Trends:
- The graph starts at the origin (0,0) and initially follows a linear path, indicating the Ohmic region, where the device behaves like a resistor.
- As $v_{DS}$ increases, the curve begins to bend upwards, entering the Triode region, where the linearity starts to diminish.
- The curve eventually reaches a point known as the Pinch-off point (EOS), beyond which the current becomes relatively constant, indicating the Saturation region.

Key Features and Technical Details:
- **Ohmic Region:** At small values of $v_{DS}$, the graph is linear, characterized by a slope of $1/r_{DS}$, indicating the channel acts as a resistor.
- **Triode Region:** The transition from the Ohmic region to the Pinch-off point, where the curve starts to deviate from the linear path.
- **Pinch-off Point (EOS):** This is the point where the curve changes from the Triode to the Saturation region.
- **Saturation Region:** After the Pinch-off point, the curve flattens out, indicating that the current $i_D$ becomes constant, and the slope is $1/r_o$.
- The graph indicates $I_{D(EOS)}$ as the maximum current at the end of the Ohmic region and $V_{DS(EOS)}$ as the corresponding voltage.

Annotations and Specific Data Points:
- The graph is annotated with regions: Ohmic, Triode, and Saturation, along with specific markers such as $I_{D(EOS)}$, $V_{DS(EOS)}$, and the slopes $1/r_{DS}$ and $1/r_o$.

This graph effectively illustrates the transition of a MOSFET from a resistive state to a saturation state as the drain-source voltage increases, highlighting the key operational regions of the device.

FIGURE 3.11 The complete $i_{D}-V_{D S}$ characteristic for a given overdrive voltage $V_{\text {OV }}=V_{G S}-V_{t}>0$. Note that $V_{D S(E O S)}=V_{O V}$.
confirms that the channel acts as a resistor, this being the reason why this region is also referred to as the ohmic region. The channel resistance $r_{D S}$ is controlled by the overdrive $V_{O V}$ as

$$
\begin{equation*}
r_{D S}=\frac{1}{k\left(V_{G S}-V_{t}\right)}=\frac{1}{k^{\prime} \frac{W}{L} V_{O V}} \tag{3.17}
\end{equation*}
$$

This resistance depends also on the $W / L$ ratio, also called the aspect ratio, indicating that by proper choice of this ratio, the IC designer can set this resistance to virtually any value for a given overdrive $V_{O V}$.
(a) Assuming $\mu_{n}=600 \mathrm{~cm}^{2} / \mathrm{Vs}, C_{o x}=83 \mathrm{nF} / \mathrm{cm}^{2}$, and $V_{t}=1.0 \mathrm{~V}$, specify the $W / L$ ratio so that $r_{D S}=1 \mathrm{k} \Omega$ for $V_{G S}=5 \mathrm{~V}$.
(b) Calculate $r_{D S}$ for $V_{G S}=4 \mathrm{~V}, 3 \mathrm{~V}, 2 \mathrm{~V}, 1 \mathrm{~V}, 0 \mathrm{~V}$.

#### Solution

(a) By Eq. (3.14), $k^{\prime}=600 \times 83 \times 10^{-9} \cong 50 \mu \mathrm{~A} / \mathrm{V}^{2}$. Using Eq. (3.17) to impose

$$
10^{3}=\frac{1}{50 \times 10^{-6}(W / L)(5-1)}
$$

we get $W / L=5$. Consequently, $k=\left(50 \mu \mathrm{~A} / \mathrm{V}^{2}\right) 5=250 \mu \mathrm{~A} / \mathrm{V}^{2}$.
(b) By Eq. (3.17), for $V_{G S}=4 \mathrm{~V}$ we have

$$
r_{D S}=\frac{1}{250 \times 10^{-6}(4-1)}=1.333 \mathrm{k} \Omega
$$

Likewise, for $V_{G S}=3 \mathrm{~V}$ we find $r_{D S}=2 \mathrm{k} \Omega$, and for $V_{G S}=2 \mathrm{~V}$ we find $r_{D S}=4 \mathrm{k} \Omega$. For $V_{G S} \leq 1 \mathrm{~V}$ the MOSFET is in cutoff and $r_{D S}=\infty$.

As we increase $v_{D S}$ further, the channel becomes progressively thinner at the drain end, and the quadratic term of Eq. (3.12) becomes more and more pronounced. Consequently, the slope of the curve decreases, indicating a corresponding increase in the dynamic resistance of the channel. This region of operation is called the triode region by analogy with vacuum tubes, which exhibit similar characteristics. We also observe in the sequence depicted in Fig. 3.9 that the depletion layer associated with the body-drain junction widens as we keep increasing $v_{D S}$.

### The Pinchoff Point

Once $v_{D S}$ achieves the critical value $V_{D S(\text { EOS })}=V_{G S}-V_{t}$, or

$$
\begin{equation*}
V_{D S(\mathrm{EOS})}=V_{O V} \tag{3.18}
\end{equation*}
$$

the channel thickness at the drain end reduces to zero, as depicted in Fig. 3.9c, and the corresponding point on the $i_{D}-v_{D S}$ curve is referred to as the pinchoff point. As
we shall see shortly, this point marks the beginning, or edge of saturation (EOS) condition. The current at this point is readily found by substituting $\mathrm{v}_{D S}=V_{G S}-V_{t}$ in Eq. (3.12). The result is

$$
\begin{equation*}
I_{D(\mathrm{EOS})}=\frac{k}{2}\left(V_{G S}-V_{t}\right)^{2} \tag{3.19}
\end{equation*}
$$

with $k$ as given in Eq. (3.13). This is also expressed as $I_{D(\mathrm{EOS})}=(k / 2) V_{D S(\mathrm{EOS})}^{2}$, or better yet as

$$
\begin{equation*}
I_{D(\mathrm{EOS})}=\frac{k}{2} V_{O V}^{2} \tag{3.20}
\end{equation*}
$$

### The Saturation Region

If we raise $v_{D S}$ above the critical value $V_{D S(\mathrm{EOS})}$, the voltage at the pinchoff point continues to remain at $V_{D S(\mathrm{EOS})}$, and the excess difference $v_{D S}-V_{D S(\mathrm{EOS})}$ is dropped across a narrow depletion layer of width $\Delta L$ between the pinchoff point and the edge of the drain. As depicted in Fig. 3.9d, the pinchoff point moves leftwards away from the drain, in effect shortening the channel by the amount $\Delta L$. This situation, aptly referred to as channel-length modulation, results in the actual channel length

$$
L_{\text {actual }}=L-\Delta L=L\left(1-\frac{\Delta L}{L}\right)
$$

To find the $i_{D}-v_{D S}$ characteristic past the pinchoff point we adapt Eq. (3.19) and write

$$
\begin{aligned}
i_{D} & =\frac{1}{2}\left(k^{\prime} \frac{W}{L_{\text {actual }}}\right)\left(V_{G S}-V_{t}\right)^{2}=\frac{1}{2} k^{\prime} \frac{W}{L\left(1-\frac{\Delta L}{L}\right)}\left(V_{G S}-V_{t}\right)^{2} \\
& \cong \frac{1}{2} k^{\prime} \frac{W}{L}\left(1+\frac{\Delta L}{L}\right)\left(V_{G S}-V_{t}\right)^{2}
\end{aligned}
$$

where we have exploited the fact that usually $\Delta L / L \ll 1$. It is an established practice in the literature to assume that the fractional change $\Delta L / L$ be linearly proportional to $v_{D S}$, or $\Delta L / L=\lambda v_{D S}$. Consequently, the $i_{D}-v_{D S}$ characteristic past the pinchoff point is expressed as

$$
\begin{equation*}
i_{D}=\frac{k}{2}\left(V_{G S}-V_{t}\right)^{2}\left(1+\lambda v_{D S}\right) \tag{3.21}
\end{equation*}
$$

with $k$ as given in Eq. (3.13). The proportionality constant $\lambda$ (in $\mathrm{V}^{-1}$ ) is called the channel-length modulation parameter. Typically, $\lambda$ is on the order of 0.01 to $0.1 \mathrm{~V}^{-1}$, and for simplicity it is usually ignored $(\lambda \rightarrow 0)$ in the course of hand dc calculations. The region past the pinchoff point is aptly referred to as the saturation region because $i_{D}$ increases with $v_{D S}$ only slightly there, in effect saturating.

The slope of the saturation-region characteristic is the reciprocal of a resistance $r_{o}$ called the output resistance of the MOSFET in saturation. Differentiating Eq. (3.21) and calculating at the EOS gives

$$
\frac{1}{r_{o}}=\frac{\partial i_{D}}{\partial v_{D S}}=\lambda I_{D(\mathrm{EOS})}
$$

The output resistance is usually expressed in the form

$$
\begin{equation*}
r_{o}=\frac{1}{\lambda I_{D}} \tag{3.22}
\end{equation*}
$$

where $I_{D}$ is the current at the actual saturation-region operating point $\left(I_{D} \cong I_{D(\mathrm{EOS})}\right)$. In general, $r_{o}$ is fairly large relative to other resistances in a MOSFET circuit. Indeed, the smaller the value of $\lambda$, the higher the value of $r_{o}$. In the limit $\lambda \rightarrow 0$, a saturated MOSFET would approach ideal current-source behavior, or, more precisely, it would act as an ideal voltage-controlled current-source (VCCS), with $V_{G S}$ as the control voltage. As such, the MOSFET finds application as an amplifier.
Remark: To ensure continuity between Eqs. (3.12) and (3.21) at the EOS, the righthand side of Eq. (3.12) should also be multiplied by the term $\left(1+\lambda v_{D S}\right)$. In practice, to simplify the triode-region calculations, the term $\lambda v_{D S}$ is usually ignored as $v_{D S}$ is small in that region.

A certain $n$ MOSFET has $V_{t 0}=1.0 \mathrm{~V}, k=0.5 \mathrm{~mA} / \mathrm{V}^{2}, \lambda=0.02 \mathrm{~V}^{-1}, \gamma=0.6 \mathrm{~V}^{1 / 2}$, and $\phi_{p}=-0.3 \mathrm{~V}$.
(a) If $V_{G S}=3 \mathrm{~V}$ and $V_{S B}=0$, find $V_{D S(E O S)}, I_{D(\mathrm{EOS})}$, and $r_{r}$.
(b) What is the value of $I_{D}$ at $V_{D S}=0.5 V_{D S(\mathrm{EOS})}$ ? At $V_{D S}=2 V_{D S(\mathrm{EOS})}$ ? At $V_{D S}=$ $4 V_{D S(\mathrm{EOS})}$ ?
(c) Repeat parts (a) and (b), but with $V_{S B}=2 \mathrm{~V}$. Comment on your findings.
(d) Find $V_{S B}$ so that $V_{D S(\mathrm{EOS})}=1 \mathrm{~V}$ with $V_{G S}=3 \mathrm{~V}$. What is the corresponding value of $I_{D(\mathrm{EOS})}$ ?

#### Solution

(a) We have $V_{D S(\mathrm{EOS})}=V_{O V}=V_{G S}-V_{t 0}=3-1=2 \mathrm{~V}$, so

$$
I_{D(\mathrm{EOS})}=\frac{k}{2} V_{O V}^{2}\left(1+\lambda V_{D S(\mathrm{EOS})}\right)=\frac{0.5}{2} 2^{2}(1+0.02 \times 2)=1.04 \mathrm{~mA}
$$

Moreover, $r_{o}=1 /(0.02 \times 1.04)=48 \mathrm{k} \Omega$.
(b) With reference to Fig. 3.11, we observe that for $V_{D S}=0.5 V_{D S(\mathrm{EOS})}=1 \mathrm{~V}\left(<V_{O V}\right)$ the FET is operating in the triode region, while for $V_{D S}=2 V_{D S(\mathrm{EOS})}=4 \mathrm{~V}$ ( $>V_{O V}$ ) the FET is operating in saturation. Consequently, we use Eqs. (3.12) and (3.21) to find

$$
\begin{aligned}
& I_{D}\left(V_{D S}=1 \mathrm{~V}\right)=0.5\left(2 \times 1-1^{2} / 2\right)=0.75 \mathrm{~mA} \\
& I_{D}\left(V_{D S}=4 V\right)=(0.25) 2^{2}(1+0.02 \times 4)=1.08 \mathrm{~mA} \\
& \text { Similarly, } I_{D}\left(V_{D S}=8 \mathrm{~V}\right)=1.16 \mathrm{~mA}
\end{aligned}
$$

(c) By Eq. (3.8), we now have

$$
V_{t}\left(V_{S B}=2 \mathrm{~V}\right)=1.0+0.6(\sqrt{2+2 \times 0.3}-\sqrt{2 \times 0.3})=1.5 \mathrm{~V}
$$

Consequently, $V_{D S(\mathrm{EOS})}=V_{O V}=3-1.5=1.5 \mathrm{~V}$. By analogous calculations, we now get

$$
I_{D(\mathrm{EOS})}=0.25 \times 1.5^{2}(1+0.02 \times 1.5)=0.58 \mathrm{~mA}
$$

and $r_{o}=1 /(0.02 \times 0.58)=86 \mathrm{k} \Omega$. Moreover,

$$
\begin{aligned}
& I_{D}\left(V_{D S}=0.75 \mathrm{~V}\right)=0.5\left(1.5 \times 0.75-0.75^{2} / 2\right)=0.42 \mathrm{~mA} \\
& I_{D}\left(V_{D S}=3 \mathrm{~V}\right)=0.25 \times 1.5^{2}(1+0.02 \times 3)=0.60 \mathrm{~mA}
\end{aligned}
$$

Likewise, $I_{D}\left(V_{D S}=6 \mathrm{~V}\right)=0.63 \mathrm{~mA}$. The increase in $V_{t}$ due to the body affect has resulted in a less conductive channel, thus causing a decrease in the drain current values as well as an increase in $r_{o}$.
(d) We now have $V_{t}=V_{G S}-V_{D S(\mathrm{EOS})}=3-1=2 \mathrm{~V}$. Using Eq. (3.8) to impose

$$
\begin{aligned}
& \quad 2=1.0+0.6\left(\sqrt{V_{S B}+0.6}-\sqrt{0.6}\right) \\
& \text { yields } V_{S B}=5.36 \mathrm{~V} \text {. Finally, } I_{D(\mathrm{EOS})}=0.25 \times 1^{2}(1+0.02 \times 1)=0.255 \mathrm{~mA}
\end{aligned}
$$

### Determining the Operating Region of a nMOSFET

As we progress, we will often face the need to identify the operating region of a FET from a set of incomplete data. For the case of an $n$ MOSFET, we will proceed as follows:

- If $V_{G S} \leq V_{t}$, the FET is operating in the cut-off (CO) region, where $i_{D}=0$.
- If $V_{G S}>V_{t}$, the FET is on, but is it operating in the triode or in the saturation region? This depends on whether $V_{D S}<V_{O V}$ or $V_{D S}>V_{O V}$, respectively. To find out, proceed as follows:
- Assume the FET is saturated, and use Eq. (3.21) to find the missing data until you have both $V_{O V}$ and $V_{D S}$ in hand. If it turns out that $V_{D S}>V_{O V}$, the assumption was correct, and no further steps are needed.
- Otherwise you get a contradiction, indicating that the FET is in the triode region, and you must recalculate the missing data via Eq. (3.12) instead. As a final check, verify that indeed $V_{D S}<V_{O V}$.
- Alternatively, we could start out with the assumption that the FET be in the triode region, and then check that indeed $V_{D S}<V_{O V}$ to confirm our assumption. Otherwise, we get a contradiction signifying that the FET is instead saturated. An example will better illustrate the above procedure.

EXAMPLE 3.9 A certain $n$ MOSFET has $V_{t}=1.5 \mathrm{~V}, k=1.0 \mathrm{~mA} / \mathrm{V}^{2}$, and $\lambda=0.02 \mathrm{~V}^{-1}$, and is operated at $V_{S B}=0$.
(a) Find $V_{G S}$ so that the FET gives $I_{D}=2.2 \mathrm{~mA}$ at $V_{D S}=5 \mathrm{~V}$.
(b) Find $V_{G S}$ for $I_{D}=2 \mathrm{~mA}$ at $V_{D S}=1 \mathrm{~V}$.
(c) Find $V_{D S}$ so that the FET gives $I_{D}=4 \mathrm{~mA}$ with $V_{G S}=4.5 \mathrm{~V}$.
(d) Find $V_{D S}$ for $I_{D}=0.52 \mathrm{~mA}$ with $V_{G S}=2.5 \mathrm{~V}$.

#### Solution

(a) Assume the FET is saturated, and then check. By Eq. (3.21), the overdrive $V_{O V}$ needed to sustain 2.2 mA in saturation is such that

$$
2.2=\frac{1}{2} V_{o V}^{2}(1+0.02 \times 5)
$$

This gives $V_{O V}=2 \mathrm{~V}$. Since $V_{D S}>V_{O V}(5>2)$, the FET is indeed in saturation, confirming that our assumption was correct. Clearly, $V_{G S}=V_{t}+V_{O V}=$ $1.5+2=3.5 \mathrm{~V}$.
(b) Assume again saturation. Imposing

$$
2=0.5 V_{O V}^{2}(1+0.02 \times 1)
$$

gives $V_{O V}=1.98 \mathrm{~V}$, that is, $V_{D S}<V_{O V}(1<1.98)$. This contradicts our assumption of a saturated FET, so the device must be operating in the triode region, where Eq. (3.12) holds. The overdrive $V_{O V}$ needed to sustain 2 mA in the triode region is such that

$$
2=1\left(V_{O V} \times 1-\frac{1^{2}}{2}\right)
$$

This gives $V_{O V}=2.5 \mathrm{~V}$. The fact that $V_{D S}<V_{O V}(1<2.5)$ confirms that the FET is indeed in the triode region. Moreover, $V_{G S}=1.5+2.5=4 \mathrm{~V}$.
(c) As an alternative, assume this time the FET to be in the triode region, and then check as usual. Now, $V_{O V}=V_{G S}-V_{t}=4.5-1.5=3 \mathrm{~V}$. By Eq. (3.12) we must have

$$
4=1\left(3 \times V_{D S}-\frac{V_{D S}^{2}}{2}\right)
$$

or $0.5 V_{D S}^{2}-3 V_{D S}+4=0$. This quadratic equation admits two solutions, $V_{D S}=2 \mathrm{~V}$ and $V_{D S}=4 \mathrm{~V}$. The second one is unacceptable as it would imply a saturated FET ( $V_{D S}>V_{O V}$ ), for which Eq. ( 3.21 ) would predict $I_{D}=4.86 \mathrm{~mA}$, in blatant contradiction with the desired value of $I_{D}$. Consequently, our FET is indeed in the triode region, and $V_{D S}=2 \mathrm{~V}$.
(d) Assume again the triode region. We have $V_{O V}=2.5-1.5=1 \mathrm{~V}$, and

$$
0.52=1\left(1 \times V_{D S}-\frac{V_{D S}^{2}}{2}\right)
$$

or $0.5 V_{D S}^{2}-V_{D S}+0.52=0$. This quadratic equation admits the solutions $V_{D S}=$ $1 \pm 0.2 j$, which are complex numbers and thus physically unacceptable. Evidently, our triode-region assumption was wrong. We must thus use Eq. (3.21) and impose

$$
0.52=\frac{1}{2} 1^{2}\left(1+0.02 V_{D S}\right)
$$

which yields $V_{D S}=2 \mathrm{~V}$. The fact that $V_{D S}>V_{O V}(2>1)$ confirms that the FET is indeed saturated.

### Series/Parallel MOSFET Combinations

As we proceed we shall often encounter FETs connected in series or parallel. The channels combine just like resistors do, namely, in series combinations the channel resistances add up, while in parallel combinations the channel conductances add up.
image_name:FIGURE 3.12
description:
[
name: (W/L)_1, type: NMOS, ports: {S: S, D: D, G: G}
name: (W/L)_2, type: NMOS, ports: {S: S, D: D, G: G}
name: (W/L)_m, type: NMOS, ports: {S: S, D: D, G: G}
]
extrainfo:The diagram shows multiple NMOS transistors connected in parallel. The equivalent width-to-length ratio (W/L)_eq is the sum of the individual (W/L) ratios of each NMOS transistor. This configuration allows the transistors to act as a single equivalent transistor with an enhanced drive capability.

FIGURE 3.12 When $m$ FETs are connected in parallel, they act like a single equivalent FET whose $W / L$ ratio is the sum of the individual $W / L$ ratios.

Consider $m$ MOSFETs having the same $V_{t}$ and $k^{\prime}$ but individual ratios $(W / L)_{1}$, $(W / L)_{2}, \ldots(W / L)_{m}$, and suppose they are connected in parallel, as in Fig. 3.12. The current drawn by each FET is linearly proportional to its $W / L$ ratio, and since all FETs are subjected to the same input drive, the proportionality constant is the same for all FETs. But, the total current drawn from the drain terminal is the sum of the individual currents, so the parallel combination of $m$ FETs acts like a a single equivalent FET having

$$
\begin{equation*}
\left(\frac{W}{L}\right)_{e q}=\left(\frac{W}{L}\right)_{1}+\left(\frac{W}{L}\right)_{2}+\cdots+\left(\frac{W}{L}\right)_{m} \tag{3.23}
\end{equation*}
$$

A common occurrence is when two identical FETs are in parallel, which can intuitively be regarded as a single FET but with $W$ twice as long.

Figure 3.13 shows the case of $m$ FETs connected in series. Assuming for simplicity $\gamma=0$ and $\lambda=0$ throughout, one can prove that if all FETs have the same $V_{t}$ and $k^{\prime}$ but individual ratios $(W / L)_{1},(W / L)_{2}, \ldots(W / L)_{m}$, they act like single equivalent MOSFET such that

$$
\begin{equation*}
\left(\frac{W}{L}\right)_{e q}^{-1}=\left(\frac{W}{L}\right)_{1}^{-1}+\left(\frac{W}{L}\right)_{2}^{-1}+\cdots+\left(\frac{W}{L}\right)_{m}^{-1} \tag{3.24}
\end{equation*}
$$

image_name:FIGURE 3.13
description:
[
name: M1, type: NMOS, ports: {S: X1, D: X1D, G: G}
name: M2, type: NMOS, ports: {S: Xm-1, D: X1, G: G}
name: Mm-1, type: NMOS, ports: {S: S, D: Xm-1, G: G}
]
extrainfo:The circuit consists of m NMOS transistors connected in series, each with a different (W/L) ratio. The equivalent (W/L) ratio of the series connection is given by the reciprocal of the sum of the reciprocals of the individual (W/L) ratios. The diagram illustrates the transformation of the series connection into an equivalent single NMOS with a combined (W/L) ratio.

FIGURE 3.13 When $m$ FETs are connected in series, they act like a single equivalent FET whose $L / W$ ratio is the sum of the individual $L / W$ ratios.

A common occurrence is one of two identical FETs in series, which can intuitively be regarded as a single FET but with $L$ twice as large.

Suppose two FETs are fabricated in a $0.5-\mu \mathrm{m}$ process with $(W / L)_{1}=(1.0 \mu \mathrm{~m}) /$
EXAMPLE 3.10 $(0.5 \mu \mathrm{~m})$ and $(W / L)_{2}=(0.5 \mu \mathrm{~m}) /(0.5 \mu \mathrm{~m})$. Find $(W / L)_{e q}$ if the FETs are connected (a) in parallel, and (b) in series. In either case, express $(W / L)_{e q}$ in such a way that the smaller of $W$ and $L$ is $0.5 \mu \mathrm{~m}$.

#### Solution

(a) By Eq. (3.23), $(W / L)_{e q}=(1.0 / 0.5)+(0.5 / 0.5)=(1.5 \mu \mathrm{~m}) /(0.5 \mu \mathrm{~m})$.
(b) By Eq. (3.24), $(L / W)_{e q}=(0.5 / 1.0)+(0.5 / 0.5)=1.5$, so $(W / L)_{e q}=1 / 1.5=$ $(0.5 \mu \mathrm{~m}) /(0.75 \mu \mathrm{~m})$.

## 3.4 THE i-v CHARACTERISTICS OF MOSFETS

The two most important MOSFET characteristics are the plot of $i_{D}$ versus $v_{G S}$ in saturation, and the plot of $i_{D}$ versus $v_{D S}$ for different values of $V_{G S}$. These curves can be displayed either in the lab, via an oscilloscope equipped with a suitable curve-tracer module, or on a computer monitor via PSpice (see Appendix 3A for PSpice models for MOSFETs).

### Diode-Mode Operation

In the PSpice circuit of Fig. 3.14 (see Appendix 3A) the gate and drain terminals are tied together, turning the $n$ MOSFET into a two-terminal device with $v_{D S}=v_{G S}$. For $v_{G S}<V_{t}$ the device is in cutoff. For $v_{G S}>V_{t}$ the device is on and in saturation because $v_{D S}=v_{G S}$ implies $v_{D S}>V_{G S}-V_{t}$, the condition for a saturated $n$ MOSFET. Consequently, when on, the device is governed by Eq. (3.21), but with $v_{D S}=v_{G S}$. The result is the curve of Fig. 3.15, which reveals a tendency by a diode-connected MOSFET to favor current flow in one direction (drain-to-source for an $n$ MOSFET, source-todrain for a $p$ MOSFET) while inhibiting it in the opposite direction. Hence the name diode for this mode of operation.
image_name:FIGURE 3.14 Diode-connected enhancement n MOSFET
description:
[
name: VGS, type: VoltageSource, value: VGS, ports: {Np: VGS, Nn: GND}
name: Mn, type: NMOS, ports: {S: GND, D: VGS, G: VGS}
]
extrainfo:The circuit diagram features a diode-connected NMOS transistor Mn connected to a voltage source VGS. The source of Mn is connected to ground, while the gate and drain are connected together to VGS, forming a diode connection. This configuration allows current to flow in one direction, similar to a diode.

$$
\begin{gathered}
\mathrm{Mn}: W=2 \mu \mathrm{~m}, L=1 \mu \mathrm{~m}, k^{\prime}=50 \mu \mathrm{~A} / \mathrm{V}^{2}, \\
V_{t}=1.0 \mathrm{~V}, \lambda=0.05 \mathrm{~V}^{-1}
\end{gathered}
$$

FIGURE 3.14 Diode-connected enhancement $n$ MOSFET.
image_name:FIGURE 3.15
description:The graph in FIGURE 3.15 is an \( i-v \) characteristic curve for a diode-connected enhancement \( n \) MOSFET. It plots the drain current \( i_D \) on the vertical axis against the gate-source voltage \( v_{GS} \) on the horizontal axis.

1. **Type of Graph and Function:**
- This is a current-voltage (\( i-v \)) characteristic graph.

2. **Axes Labels and Units:**
- The vertical axis is labeled "Drain current \( i_D \)" with units in milliamperes (mA).
- The horizontal axis is labeled "Gate-source voltage \( v_{GS} \)" with units in volts (V).

3. **Overall Behavior and Trends:**
- The curve starts near the origin and exhibits an increasing trend as \( v_{GS} \) increases, showing that the drain current \( i_D \) increases with the gate-source voltage.
- The curve's shape indicates an exponential rise at lower voltages, transitioning to a more quadratic-like increase as \( v_{GS} \) exceeds the threshold voltage \( V_t \).

4. **Key Features and Technical Details:**
- The threshold voltage \( V_t \) is marked on the graph, indicating the point where the MOSFET begins to conduct significantly.
- The point \( Q \) is marked on the curve, representing a specific operating point with corresponding \( i_D \) and \( v_{GS} \) values.
- The transconductance \( g_m \) is indicated as a slope at the point \( Q \), showing the rate of change of \( i_D \) with respect to \( v_{GS} \).
- \( V_{OV} \) is labeled as the overdrive voltage, which is the difference between \( v_{GS} \) and \( V_t \).

5. **Annotations and Specific Data Points:**
- The graph includes gridlines for better readability of specific current and voltage values.
- \( I_D \) is marked on the vertical axis at approximately 0.5 mA, indicating a reference current level.
- The curve shows a smooth transition from subthreshold to above-threshold operation, reflecting the gradual nature of MOSFET conduction onset.

FIGURE 3.15 The $i-v$ characteristic of the diode-connected enhancement $n$ MOSFET of Fig. 3.14.

At this juncture it must be pointed out that the MOSFET's transition from off to on in the vicinity of $V_{t}$ is not abrupt, but rather a gradual process. In fact, the channel already starts to conduct for a range of $v_{G S}$ values less than, if close to, $V_{t}$. Over this range, aptly called the subthreshold region, $i_{D}$ increases exponentially-rather than quadratically-with $v_{G S}$. The choice of $V_{t}$ as the value of $v_{G S}$ responsible for the onset of strong inversion is primarily a matter of mathematical convenience and mental bookkeeping.

The slope of the curve at a given point $V_{G S}$ is denoted as $g_{m}$ and is called the transconductance

$$
\begin{equation*}
g_{m}=\left.\frac{\partial i_{D}}{\partial v_{G S}}\right|_{V_{G S}} \tag{3.25}
\end{equation*}
$$

Its units are $\mathrm{A} / \mathrm{V}$, or more likely $\mu \mathrm{A} / \mathrm{V}$ for micropower devices. Differentiating Eq. (3.21) but with $\lambda=0$ for simplicity, and suitably manipulating, we find three different expressions for the transconductance,

$$
\begin{gather*}
g_{m}=\sqrt{2 k I_{D}}  \tag{3.26a}\\
g_{m}=k V_{O V}  \tag{3.26b}\\
g_{m}=\frac{I_{D}}{0.5 V_{O V}} \tag{3.26c}
\end{gather*}
$$

Though the three forms are equivalent, each provides different insight. The first form indicates that $g_{m}$ increases with the square root of $I_{D}$. By contrast, in a bipolar junction transistor (BJT), $g_{m}$ is linearly proportional to the collector current $I_{C}$, or $g_{m}=$ $I_{C} / V_{T}$, where $V_{T}=26 \mathrm{mV}$ is the thermal voltage. The second form indicates that $g_{m}$ is proportional to the overdrive voltage $V_{O V}=V_{G S}-V_{t}$. Moreover, comparison of Eq. (3.26b) with Eq. (3.17) reveals the additional interesting relation $g_{m}=1 / r_{D S}$.
(a) Assuming the $n$ MOSFET data of Fig. 3.14, but with $\lambda=0$ to simplify the calculations, find $V_{G S}$ for $I_{D}=1 \mathrm{~mA}$. Compare with Fig. 3.15, and comment.
(b) Find $g_{m}$ at that point, and compare with the $g_{m}$ of a bipolar junction transistor (BJT) operating at the same current level.
(c) Find $W / L$ to raise the $g_{m}$ of the FET to the same value as that of the BJT.

#### Solution

(a) By Eq. (3.13), $k=50 \times 10^{-6}(2 / 1)=100 \mu \mathrm{~A} / \mathrm{V}^{2}$. Using Eq. (3.21) but with $\lambda=0$ we get $1 \times 10^{-3}=1 / 2\left(100 \times 10^{-6}\right) \times\left(V_{G S}-1.0\right)^{2}$, or $V_{G S}=5.472 \mathrm{~V}$. This is a bit higher than the value ( 5 V ) predicted by Fig. 3.15 because we have assumed $\lambda=0$. This gives an idea of the error incurred by ignoring $\lambda$.
(b) By Eq. (3.26a), $g_{m}=\sqrt{2 k I_{D}}=\sqrt{2 \times 100 \times 10^{-6} \times 10^{-3}}=0.447 \mathrm{~mA} / \mathrm{V}$. By contrast, at 1 mA a BJT gives $g_{m}=1 / 26=38.5 \mathrm{~mA} / \mathrm{V}$, almost two orders of magnitude higher.
(c) Since $g_{m}$ is linearly proportional to $\sqrt{k}$, and thus to $\sqrt{\mathrm{W} / \mathrm{L}}$, we impose a simple proportion,

$$
\frac{\sqrt{(W / L)_{\mathrm{new}}}}{\sqrt{(W / L)_{\mathrm{old}}}}=\frac{38.5}{0.447}
$$

which gives $(W / L)_{\text {new }} \cong 14,800$, an outlandish number. This example illustrates a notorious drawback of FETs compared to BJTs, namely, their generally much lower $g_{m} s$. Indeed, Eq. (3.26c) gives $g_{m}=I_{D} /[0.5(5.472-1.0) \mathrm{V}]=I_{D} /(2,236 \mathrm{mV})$, which compares quite unfavorably with the BJT relation $g_{m}=I_{C} /(26 \mathrm{mV})$.

### The $i_{D}-V_{D S}$ Characteristics

In Fig. 3.11 we have illustrated the behavior of the channel as we walk it through the different situations of Fig. 3.9, but for only a single fixed value of $V_{G S}\left(V_{G S}>V_{t}\right)$. To get the complete picture, we need to display the characteristics for different values of $V_{G S}$. The PSpice circuit of Fig. 3.16 displays the $i_{D}-v_{D S}$ characteristics of the FET of Fig. 3.14, but with $V_{G S}$ stepped in $0.5-\mathrm{V}$ increments. The result is the family of curves of Fig. 3.17, with respect to which we make the following observations:
image_name:FIGURE 3.16
description:
[
name: Mn, type: NMOS, ports: {S: GND, D: VDS, G: VGS}
name: VGS, type: VoltageSource, value: VGS, ports: {Np: VGS, Nn: GND}
name: VDS, type: VoltageSource, value: VDS, ports: {Np: VDS, Nn: GND}
]
extrainfo:The circuit displays the iD-vDS characteristics of an NMOS transistor with parameters: W = 2 μm, L = 1 μm, k' = 50 μA/V², Vt = 1.0 V, λ = 0.05 V⁻¹. The NMOS is connected with its source to GND, drain to VDS, and gate to VGS. VGS is stepped to show different characteristics.

FIGURE 3.16 PSpice circuit to display the complete $i_{D}-V_{D S}$ characteristics of the nMOSFET of Fig. 3.14.
image_name:Figure 3.17
description:The graph in Figure 3.17 is an i_D-v_DS characteristic plot of an NMOS transistor, showing the drain current (i_D) versus the drain-source voltage (v_DS) for different gate-source voltages (V_GS). The x-axis represents the drain-source voltage, v_DS, in volts (V), ranging from 0 to 5 V. The y-axis represents the drain current, i_D, in milliamperes (mA), ranging from 0 to 0.6 mA.

The graph is divided into three main regions: cutoff, triode, and saturation.

1. **Cutoff Region:**
- When V_GS ≤ 1.0 V, the NMOS is in the cutoff region, and the drain current i_D is zero. This is indicated at the bottom of the graph where no curves are present until V_GS exceeds 1.0 V.

2. **Triode Region:**
- For each V_GS value above the threshold voltage (V_t = 1.0 V), the NMOS enters the triode region initially as v_DS increases. This region is marked on the graph extending from the origin to the point where v_DS equals (V_GS - V_t).
- The curves in the triode region show a quadratic increase in i_D with increasing v_DS.

3. **Saturation Region:**
- Beyond the point where v_DS = V_GS - V_t, the NMOS enters the saturation region. In this region, i_D becomes relatively constant for further increases in v_DS.
- The curves flatten out, showing that the drain current is largely independent of v_DS in this region.

The graph contains several curves, each corresponding to a different V_GS value: 1.5 V, 2.0 V, 2.5 V, 3.0 V, 3.5 V, and 4.0 V. As V_GS increases, both the triode and saturation regions show higher i_D values, indicating that the transistor can conduct more current with higher gate-source voltages.

The transition between the triode and saturation regions is marked by the line v_DS = V_GS - V_t, which is shown on the graph, helping to identify the boundary between these two operating regions. The saturation region is shaded to distinguish it from the triode region.

FIGURE 3.17 Complete $i_{D}-v_{D S}$ characteristics of the enhancement $n$ MOSFET of Fig. 3.16, and its regions of operation.

- For $V_{G S}<V_{t}$ (or $V_{G S}<1.0 \mathrm{~V}$ in our example), the device gives $i_{D}=0$ and is thus in cutoff (CO). Its terminals draw only leakage currents, which are negligible in most practical situations.
- For $V_{G S}>V_{t}$, the device is on, either in the triode region if $v_{D S}<\left(V_{G S}-V_{t}\right)$, or in the saturation region if $v_{D S}>\left(V_{G S}-V_{t}\right)$. Either region requires a separate equation for finding $i_{D}$, namely,

$$
\begin{aligned}
& v_{D S}<\left(V_{G S}-V_{t}\right) \Rightarrow \text { Triode region } \Rightarrow i_{D}=k\left[\left(V_{G S}-V_{t}\right) v_{D S}-\frac{1}{2} v_{D S}^{2}\right] \\
& v_{D S}>\left(V_{G S}-V_{t}\right) \Rightarrow \text { Satur.n region } \Rightarrow i_{D}=\frac{k}{2}\left(V_{G S}-V_{t}\right)^{2}\left(1+\lambda v_{D S}\right)
\end{aligned}
$$

- The locus of points for which $v_{D S}=V_{G S}-V_{t}=V_{O V}$ provides the borderline between the two regions (the borderline is aptly referred to as edge of saturation, or EOS for short). Since the abscissas are spaced evenly while the ordinates are spaced quadratically, this locus is a parabola. In fact, one can readily see that this locus is simply the $i-v$ curve of Fig. 3.15, but shifted to the left by $V_{i}$.
- The saturation-region curves, when extrapolated toward the left, converge to a common point located at $-1 / \lambda$ on the $v_{D S}$ axis. This is shown in the compressed rendition of Fig. 3.18. Also called the Early voltage $V_{A}$ by analogy with its counterpart in the case of BJTs, this voltage is simply

$$
\begin{equation*}
V_{A}=\frac{1}{\lambda} \tag{3.27}
\end{equation*}
$$

Typically, $V_{A}$ is on the order of 10 to 100 V . In our example, $V_{A}=1 / 0.05=20 \mathrm{~V}$, so the intercept is located at $v_{D S}=-V_{A}=-20 \mathrm{~V}$. As a rule, the shorter the channel, the lower the value of $V_{A}$, indicating that $V_{A}$ scales with $L$. For longchannel devices, this is sometimes expressed via the empirical form $V_{A} \cong$ $L /(0.1 \mu \mathrm{~m}) \mathrm{V}$, or, equivalently, as $\lambda \cong(0.1 \mu \mathrm{~m}) / L \mathrm{~V}^{-1}$.
image_name:FIGURE 3.18 Effect of channel-length modulation on the i-v characteristics
description:The graph titled "FIGURE 3.18 Effect of channel-length modulation on the i-v characteristics" is a plot illustrating the effect of channel-length modulation on the current-voltage characteristics of a MOSFET device.

1. **Type of Graph and Function**: The graph is an I-V (current-voltage) characteristic plot, typically used to show the behavior of a semiconductor device like a MOSFET.

2. **Axes Labels and Units**:
- The x-axis represents the drain-source voltage, denoted as $v_{DS}$, and is measured in volts (V). The scale ranges from 0 to 10 V.
- The y-axis represents the drain current, denoted as $i_D$, and is measured in milliamperes (mA). The scale ranges from 0 to 0.6 mA.

3. **Overall Behavior and Trends**:
- The graph shows multiple curves, each representing a different gate voltage. The curves start at the origin and initially rise steeply before leveling off, indicating saturation.
- As $v_{DS}$ increases, the curves bend upwards, showing the effect of channel-length modulation, which causes an increase in drain current even in the saturation region.

4. **Key Features and Technical Details**:
- The intercept on the negative x-axis, labeled as $-1/\lambda$, indicates the inverse of the channel-length modulation parameter $\lambda$. This point shows the theoretical extension of the linear region of the curves.
- The saturation region is evident where the curves flatten out, but due to channel-length modulation, they exhibit a slight upward slope.

5. **Annotations and Specific Data Points**:
- The graph does not have specific numerical annotations for each curve, but the effect of channel-length modulation is clearly demonstrated by the upward shift in the saturation region.
- The gridlines help in estimating the values of $i_D$ for given $v_{DS}$ values, particularly showing how $i_D$ increases with $v_{DS}$ even in the saturation region due to channel-length modulation.

FIGURE 3.18 Effect of channel-length modulation on the $i-v$ characteristics.

### The pMOSFET and Comparison with the nMOSFET

The voltage-current relationships developed for the $n$ MOSFET apply also to the $p$ MOSFET, provided we (a) reverse all current directions and (b) reverse all voltage polarities. The two devices are compared in Fig. 3.19, where voltage is likened to height, so higher voltages are at the top and lower voltages at the bottom. Moreover,
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: S, D: D, G: G}
name: M2, type: PMOS, ports: {S: S, D: D, G: G}
]
extrainfo:This circuit diagram compares the enhancement nMOSFET and pMOSFET configurations, showing voltage and current directions, as well as operating regions such as saturation and triode. The nMOSFET has current flowing into the drain, while the pMOSFET has current flowing out of the drain. Both devices share the same gate and source nodes in this configuration.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: S, D: D, G: G}
name: M2, type: PMOS, ports: {S: S, D: D, G: G}
]
extrainfo:The diagram compares the voltage polarities, current directions, voltage ranges, and operating regions for enhancement nMOSFETs and pMOSFETs. The nMOSFET has current flowing into the drain, while the pMOSFET has current flowing out of the drain. Both devices have their source connected to the same reference node labeled 'S'.

FIGURE 3.19 Comparing voltage polarities, current directions, voltage ranges, and operating regions for the enhancement nMOSFETS and pMOSFETs. All voltages are positive at the top.
current through each device flows downwards. Following is a summary of similarities and differences between the two devices.

- The current $i_{D}$ flows into the drain of the $n$ MOSFET, but out of the drain of the $p$ MOSFET.
- In a $p$-channel, $i_{D}$ consists of holes flowing from the higher potential of the source to the lower potential of the drain.
- In an $n$-channel, $i_{D}$ consists of electrons flowing from the lower potential of the source to the higher potential of the drain. However, electrons are negative, so $i_{D}$ is taken to flow from drain to source.
- In both devices, the source and drain regions are interchangeable. The source will always be the region at lower potential in an $n$ MOSFET, and that at higher potential in a $p$ MOSFET.
- An enhancement nMOSFET is normally off. To turn it on we need to create favorable conditions for electrons to exist in its channel region. Electrons are negative, so we need to induce an opposing positive charge on the gate. This requires that we raise the gate voltage $v_{G}$ above the source voltage $v_{S}$ by at least $V_{t n}$, the threshold voltage. The amount $V_{O V n}=V_{G S}-V_{t n}, V_{O V n}>0$ is called the overdrive.
- An enhancement pMOSFET is normally off. To turn it on we need to create favorable conditions for holes to exist in its channel region. Holes are positive, so we need to induce an opposing negative charge on the gate. This requires that we lower the gate voltage $v_{G}$ below the source voltage $v_{S}$ by at least $V_{t}$, the threshold voltage (for enhancement $p$ MOSFETs the threshold $V_{t p}$ is negative, so the turn-on condition is less confusingly expressed as $v_{S G}>\left|V_{t p}\right|$. The overdrive is now $V_{O V_{p}}=V_{S G}-\left|V_{t p}\right|$.
- If $v_{D S}$ is large enough to satisfy the condition $v_{D S}>V_{O V n}$, the $n$ channel is operating in saturation, and

$$
\begin{equation*}
i_{D}=\frac{k_{n}}{2}\left(V_{G S}-V_{t n}\right)^{2}\left(1+\lambda_{n} v_{D S}\right) \quad \text { for } v_{D S}>V_{O V n} \tag{3.28a}
\end{equation*}
$$

- If $v_{S D}$ is large enough to satisfy the condition $v_{S D}>V_{O V p}$, the $p$ channel is operating in saturation, and

$$
\begin{equation*}
i_{D}=\frac{k_{p}}{2}\left(V_{S G}-\left|V_{t p}\right|\right)^{2}\left(1+\lambda_{p} v_{S D}\right) \quad \text { for } v_{S D}>V_{O V_{p}} \tag{3.28b}
\end{equation*}
$$

- If $v_{D S}$ is small enough to satisfy $v_{D S}<V_{O V n}$, then the $n$ channel is operating in the triode region, and

$$
\begin{equation*}
i_{D}=k_{n}\left[\left(V_{G S}-V_{t n}\right) v_{D S}-\frac{1}{2} v_{D S}^{2}\right] \quad \text { for } v_{D S}<V_{O V n} \tag{3.29a}
\end{equation*}
$$

- If $v_{S D}$ is small enough to satisfy $v_{S D}<V_{O V}$, then the $p$ channel is operating in the triode region, and

$$
\begin{equation*}
i_{D}=k_{p}\left[\left(V_{S G}-\left|V_{t p}\right|\right) v_{S D}-\frac{1}{2} v_{S D}^{2}\right] \quad \text { for } v_{S D}<V_{O V_{p}} \tag{3.29b}
\end{equation*}
$$

- The device transconducance parameters for the $n$ MOSFET and the $p$ MOSFET are, respectively,

$$
\begin{equation*}
k_{n}=k_{n}^{\prime} \frac{W_{n}}{L_{n}} \quad k_{p}=k_{p}^{\prime} \frac{W_{p}}{L_{p}} \tag{3.30}
\end{equation*}
$$

- The process transconducance parameters for the $n$ MOSFET and the $p$ MOSFET are, respectively,

$$
\begin{equation*}
k_{n}^{\prime}=\frac{\mu_{n} \varepsilon_{o x}}{t_{o x}} \quad k_{p}^{\prime}=\frac{\mu_{p} \varepsilon_{o x}}{t_{o x}} \tag{3.31}
\end{equation*}
$$

- To avoid the inadvertent turn-on of the internal $p n$ junctions, the bodies must be biased so that $V_{S B} \geq 0$ for the $n \mathrm{MOSFET}$, and $V_{S B} \leq 0$ (that is, $V_{B S} \geq 0$ ) for the $p$ MOSFET.
- Body bias in the $n$ MOSFET shifts $V_{t n}$ in the positive direction as

$$
\begin{equation*}
V_{t n}=V_{t n 0}+\gamma_{n}\left[\sqrt{V_{S B}+2\left|\phi_{p}\right|}-\sqrt{2\left|\phi_{p}\right|}\right] \tag{3.32a}
\end{equation*}
$$

- Body bias in the $p$ MOSFET shifts $V_{t p}$ in the negative direction as

$$
\begin{equation*}
V_{t p}=V_{t p 0}-\gamma_{p}\left[\sqrt{V_{B S}+2 \phi_{n}}-\sqrt{2 \phi_{n}}\right] \tag{3.32b}
\end{equation*}
$$

In general, $V_{t 00}, V_{t p 0}, \lambda_{n}, \lambda_{p}, \gamma_{n}$, and $\gamma_{p}$ are found experimentally via suitable measurements.

As we know, the transconductance parameters of Eq. (3.31) are proportional to the mobilities ( $\mu_{n}$ or $\mu_{p}$ ) of the charges intervening in the main current in the device. This is not surprising, as MOSFET current is of the drift type. When studying BJTs, in the previous chapter, we have encountered a similar parameter, namely, the saturation current $I_{s}$, which instead is proportional to the diffusivity $\left(D_{n}\right.$ or $\left.D_{p}\right)$ of the charges responsible for the main current in the device; this is so because BJT current is of the diffusion type. For a given doping density, electron mobility and diffusivity are two to three times higher than hole mobility and diffusivity, respectively. For these reasons, $n$-channel FETs are generally preferred over $p$-channel types, just like $n p n$ BJTs are generally preferred over pnp types.

A certain $p$ MOSFET has $V_{t 0}=-1.0 \mathrm{~V}, k=0.4 \mathrm{~mA} / \mathrm{V}^{2}, \lambda=0.05 \mathrm{~V}^{-1}, \gamma=0.73 \mathrm{~V}^{1 / 2}$, and $\phi_{n}=0.3 \mathrm{~V}$. Unless otherwise specified, the device is operated at $V_{B S}=0$.
(a) If $V_{S G}=3 \mathrm{~V}$, find $I_{D}$ at $V_{S D}=1.5 \mathrm{~V}$.
(b) Repeat part (a) if $V_{S D}=3 \mathrm{~V}$.
(c) Find $V_{S D}$ so that the FET gives $I_{D}=1.6 \mathrm{~mA}$ with $V_{S G}=4 \mathrm{~V}$.
(d) Find $V_{S G}$ so that the FET gives $I_{D}=0.24 \mathrm{~mA}$ with $V_{S D}=4 \mathrm{~V}$.
(e) Repeat part (a), but for $V_{B S}=4 \mathrm{~V}$.
(f) Find $V_{B S}$ so that the FET, with $V_{S G}=3.5 \mathrm{~V}$, gives $I_{D}=1 \mathrm{~mA}$ at $V_{S D}=5 \mathrm{~V}$.

#### Solution

(a) We have $V_{O V}=V_{S G}-\left|V_{t 0}\right|=3-1=2 \mathrm{~V}$. Since $V_{S D}<V_{O V}(1.5<2)$, the FET is operating in the triode region. By Eq. (3.29b),

$$
I_{D}=0.4\left(2 \times 1.5-\frac{1.5^{2}}{2}\right)=0.75 \mathrm{~mA}
$$

(b) The FET is now saturated because $V_{S D}>V_{O V}(3>2)$. By Eq. (3.28b), we have

$$
I_{D}=\frac{0.4}{2} 2^{2}(1+0.05 \times 3)=0.92 \mathrm{~mA}
$$

(c) We now have $V_{O V}=4-1=3 \mathrm{~V}$, but we don't know whether the FET is in the triode region or in saturation. Assume saturation, and check. Using Eq. (3.28b), impose

$$
1.6=0.2 \times 3^{2}\left(1+0.05 V_{S D}\right)
$$

whose solution is $V_{S D}=-2.2 \mathrm{~V}$. This is physically unacceptable, indicating that our assumption was wrong. Evidently the FET is in the triode region, so we use Eq. (3.29b) to impose

$$
1.6=0.4\left(3 V_{S D}-\frac{V_{S D}^{2}}{2}\right)
$$

or $0.5 V_{S D}^{2}-3 V_{S D}+4=0$. The solutions to this quadratic equation are $V_{S D}=4 \mathrm{~V}$ and $V_{S D}=2 \mathrm{~V}$. The first solution would imply a saturated FET $\left(V_{S D}>V_{O V}\right.$ because $4>3$ ) which we have just proved not to be the case. So, the physically acceptable solution is $V_{S D}=2 \mathrm{~V}$, which corroborates trioderegion operation because $V_{S D}<V_{O V}(2<3)$.
(d) Assume triode-region operation and use Eq. (3.29b) to impose

$$
0.24=0.4\left(V_{O V} \times 4-\frac{4^{2}}{2}\right)
$$

This yields $V_{O V}=2.15 \mathrm{~V}$, or $V_{S D}>V_{O V}(4>2.15)$, contradicting our assumption. Evidently the FET is saturated, so impose

$$
0.24=0.2 \times V_{O V}^{2}(1+0.05 \times 4)
$$

This gives $V_{O V}=1 \mathrm{~V}$. The fact that $V_{S D}>V_{O V}(4>1)$ corroborates saturation operation.
(e) By Eq. (3.32b), the threshold voltage is now

$$
V_{t}=-1.0-0.73[\sqrt{4+2 \times 0.3}-\sqrt{2 \times 0.3}]=-2 \mathrm{~V}
$$

so the overdrive is $V_{O V}=3-|-2|=1 \mathrm{~V}$. Since $V_{S D}>V_{O V}(1.5>1)$, the FET is now saturated, and

$$
I_{D}=0.2 \times 1^{2}(1+0.05 \times 1.5)=0.215 \mathrm{~mA}
$$

(f) Assume operation in saturation, and then check. The required overdrive is such that

$$
1=0.2 \times V_{O V}^{2}(1+0.05 \times 5)
$$

or $V_{O V}=2 \mathrm{~V}$. Since $V_{S D}>V_{O V}(5>2)$, the FET is indeed saturated. The required threshold voltage $V_{t}$ must be such that $V_{O V}=V_{S G}-\left|V_{t}\right|$, or $2=3.5-\left|V_{t}\right|$, or $\left|V_{t}\right|=1.5 \mathrm{~V}$. As we know, $V_{t}$ is negative, so we use Eq. (3.32b) to impose

$$
-1.5=-1.0-0.73\left[\sqrt{V_{B S}+2 \times 0.3}-\sqrt{2 \times 0.3}\right]
$$

This finally gives $V_{B S}=1.53 \mathrm{~V}$.

### Large-Signal Models for Saturated FETs

Figures 3.20 and 3.21 show the circuit models of the $n$ MOSFET and the $p$ MOSFET operating in saturation.

Also called large-signal models (to distinguish them from the small-signal models to be introduced later), they are used primarily in dc calculations. Since the gate is the plate of a capacitor, the G-S (or input) port appears as an open circuit, at least at
image_name:Figure 3.20 Large-signal model for the saturated n MOSFET
description:
[
name: M1, type: NMOS, ports: {S: S, D: D, G: G}
name: G, type: VoltageSource, value: VGS, ports: {Np: G, Nn: S}
name: D, type: VoltageSource, value: VDS, ports: {Np: D, Nn: S}
name: kn/2(VGS-Vtn)^2, type: VoltageControlledCurrentSource, ports: {Np: D, Nn: S}
name: 1/λnID, type: Resistor, value: 1/λnID, ports: {N1: D, N2: S}
]
extrainfo:The diagram shows the large-signal model for a saturated n-MOSFET. The gate-source voltage (VGS) controls the current source, and the drain-source voltage (VDS) is across the resistor modeling the output resistance.

FIGURE 3.20 Large-signal model for the saturated $n$ MOSFET.
image_name:FIGURE 3.21 Large-signal model for the saturated p MOSFET.
description:
[
name: M1, type: PMOS, ports: {S: S, D: D, G: G}
name: kp/2(VSG+Vtp)^2, type: VoltageControlledCurrentSource, ports: {Np: S, Nn: S}
name: 1/lpID, type: Resistor, value: 1/lpID, ports: {N1: S, N2: D}
]
extrainfo:The diagram shows the large-signal model for a saturated p-MOSFET. The gate-source voltage (VSG) controls the current source, and the source-drain voltage (VSD) is across the resistor modeling the output resistance. The gate current (iG) is zero, and the drain current (iD) flows from the source to the drain.

FIGURE 3.21 Large-signal model for the saturated $p$ MOSFET.
dc , so $i_{G}=0$, and $i_{S}=i_{D}$. The D-S (or output) port is modeled with its Norton equivalent consisting of a dependent current source calculated at the edge of saturation, and an output resistance to model the slight increase of $i_{D}$ with $v_{D S}$ in $n$ MOSFETs and $v_{S D}$ in $p$ MOSFETs.

To simplify dc calculations it is customary to ignore the output resistance, which is equivalent to assuming $\lambda=0$. Also, for the enhancement $p$ MOSFET, we shall express the dependent-source value in the form $\left(k_{p} / 2\right)\left(V_{S G}-\left|V_{t p}\right|\right)^{2}$, more closely resembling that of the $n$ MOSFET.

### Depletion MOSFETs

As we know, enhancement-type FETs are normally off devices. To turn them on, we need to apply a suitable gate-source voltage exceeding the device's threshold voltage $V_{t}$. By contrast, depletion-type MOSFETs (or DFETs) are deliberately fabricated with a channel already present. As depicted in Fig. 3.22, an $n$ DFET is created via a suitable $n$-type channel implant, and a $p$ FET via a suitable $p$-type channel implant. For obvious reasons, DFETs are said to be normally on devices. In this case we ask ourselves what needs to be done to turn a DFET off. Keeping in mind that the gate-channel structure forms a parallel-plate capacitor, we make the following statements:

- To turn off the $n$ DFET of Fig. 3.22a we need to induce positive charges in its channel region so as to neutralize the free electrons already present there. This requires inducing negative charge on the gate electrode. Consequently, we need to lower the gate voltage $v_{G}$ below the source voltage $v_{S}$ by a suitable amount, a condition expressed as $v_{G S} \leq V_{t n}$, where the threshold voltage $V_{t n}$ is now negative. Thus, for $v_{G S} \leq V_{t n}, V_{t n}<0$, the $n \mathrm{DFET}$ is off, while for $v_{G S}>V_{t n}$ it is on, and its conductivity is controlled by the overdrive voltage $V_{O V n}=V_{G S}-V_{t n}$, as usual.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: S, D: D, G: G}
name: M2, type: PMOS, ports: {S: S, D: D, G: G}
]
extrainfo:This diagram illustrates the structure and symbol of depletion-mode MOSFETs. The nMOSFET is shown on the left, and the pMOSFET is on the right. Both devices have their gate (G), source (S), and drain (D) terminals labeled. The body (B) terminal is connected to the source in both cases, which is a common configuration for discrete MOSFETs to prevent body effect.
image_name:(b)
description:
[
name: M1, type: PMOS, ports: {S: S, D: D, G: G}
]
extrainfo:The diagram shows a depletion-type pMOSFET with source connected to node S, drain to node D, and gate to node G.

FIGURE 3.22 Depletion MOSFETs.

To reduce the possibility of confusion stemming from the negative threshold, the overdrive for an $n$ DMOSFET is often expressed as $V_{O V_{n}}=V_{G S}+\left|V_{t n}\right|$. Note, in particular, that with $V_{G S}=0$ the device is conductive with $V_{O V n}=\left|V_{t n}\right|$.

- To turn off the $p$ DFET of Fig. $3.22 b$ we need to induce negative charges in its channel region so as to neutralize the free holes already present there. This requires inducing positive charge on the gate electrode. Consequently, we need to raise the gate voltage $v_{G}$ above the source voltage $v_{S}$ by a suitable amount, a condition expressed as $v_{G S} \geq V_{t p}$, where the threshold voltage $V_{t p}$ is now positive. Thus, for $v_{G S} \geq V_{t p}, V_{t p}>0$, the $p$ DFET is off, while for $v_{G S}<V_{t p}$ it is on, and its conductivity is controlled by the overdrive voltage, which now is $V_{O V_{p}}=$ $V_{S G}+V_{t p}$. Note, in particular, that with $V_{S G}=0$, the device is conductive with $V_{O V_{p}}=V_{t p}$.
The beginner may feel confused by the different FET types and corresponding threshold-voltage polarites, and trying to memorize them may provide even more confusion. The best approach is to refer to the physical structures of Figs. 3.19 and 3.22 , and ask oneself what kind of gate-to-source voltage is needed to turn the device on if it is a normally off type, or to turn it off if it is a normally on type.

The $i-v$ characteristics of the depletion FET are similar to those of its enhancement counterpart, except for a shift along the $v_{G S}$ axis. This is depicted in Fig. 3.23 for the case of an $n$ DFET with $V_{t}=-1.5 \mathrm{~V}, k=1 \mathrm{~mA} / \mathrm{V}^{2}$, and $\lambda=0.05 \mathrm{~V}^{1 / 2}$. Note that the curve of Fig. 3.23a is similar to that of Fig. 3.15, except that it is shifted to the left because now $V_{t}<0$. Starting at $v_{G S}=0 \mathrm{~V}$, we can either make the device more conductive by raising $v_{G S}$ above 0 V , or make it less conductive by lowering $v_{G S}$ below 0 V , until it shuts off completely once $v_{G S}$ reaches $V_{t}(=-1.5 \mathrm{~V}$ in our example). The effect of sweeping $v_{G S}$ can be appreciated also from Fig. 3.23b, where we note that the curve corresponding to $v_{G S}=0 \mathrm{~V}$ is now somewhere in the middle. However, the locus of the pinchoff points is still $v_{D S}=V_{G S}-V_{t}\left(=V_{G S}+1.5 \mathrm{~V}\right.$ in our example.)
image_name:(a)
description:The graph labeled '(a)' is a plot depicting the relationship between the gate-source voltage \( v_{GS} \) and the drain current \( i_D \) for a depletion \( n \) MOSFET. It is a typical \( i-v \) curve used to illustrate the MOSFET's behavior under different gate-source voltages.

1. **Type of Graph and Function:**
- This is a current-voltage (\( i-v \)) characteristic graph for a depletion \( n \) MOSFET.

2. **Axes Labels and Units:**
- The x-axis represents the gate-source voltage \( v_{GS} \) in volts (V), ranging from -2 V to 0.5 V.
- The y-axis represents the drain current \( i_D \) in milliamperes (mA), ranging from 0 mA to 2.5 mA.
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The graph shows a nonlinear relationship between \( v_{GS} \) and \( i_D \).
- As \( v_{GS} \) increases from -2 V towards 0.5 V, the drain current \( i_D \) increases exponentially.
- There is a threshold voltage \( V_t \) marked at \( -1.5 \) V, below which the device is less conductive.

4. **Key Features and Technical Details:**
- The curve starts at \( v_{GS} = -2 \) V with a drain current of 0 mA, indicating the device is off.
- As \( v_{GS} \) approaches 0 V, the device becomes more conductive, and \( i_D \) increases significantly.
- The threshold voltage \( V_t = -1.5 \) V is a critical point where the MOSFET begins to conduct more noticeably.

5. **Annotations and Specific Data Points:**
- The threshold voltage \( V_t \) is explicitly marked on the graph at \( -1.5 \) V.
- The curve passes through important regions, transitioning from a non-conductive to a conductive state as \( v_{GS} \) increases.
image_name:(b)
description:The graph labeled as (b) is an $i-v$ characteristic plot of a depletion-mode $n$-channel MOSFET. It illustrates the relationship between the drain-source voltage ($v_{DS}$) on the x-axis and the drain current ($i_D$) on the y-axis. Both axes are measured in volts (V) for $v_{DS}$ and milliamperes (mA) for $i_D$. The graph uses a linear scale.

The plot shows several curves representing different gate-source voltages ($v_{GS}$), specifically $v_{GS} = 0.5 \, \text{V}$, $0 \, \text{V}$, $-0.5 \, \text{V}$, $-1.0 \, \text{V}$, and $v_{GS} \leq -1.5 \, \text{V}$. Each curve depicts how the drain current varies with the drain-source voltage at these fixed gate-source voltages.

Key features of the graph include two distinct regions labeled as 'Triode' and 'Saturation'. In the Triode region, the curves start from the origin and initially increase linearly with $v_{DS}$. As $v_{DS}$ increases further, the curves enter the Saturation region, where the drain current reaches a relatively constant value, indicating that the MOSFET is fully on.

The curve for $v_{GS} = 0.5 \, \text{V}$ shows the highest drain current, while the curve for $v_{GS} \leq -1.5 \, \text{V}$ shows the lowest, demonstrating that increasing $v_{GS}$ increases the conductivity of the MOSFET. The pinchoff points, where the curves transition from the Triode to the Saturation region, shift rightward as $v_{GS}$ increases.

The graph is annotated with points marking the transition between the Triode and Saturation regions for each curve. These points are critical for understanding the operational limits of the MOSFET in different modes. The overall behavior indicates that the MOSFET is normally on, and its conductivity can be modulated by adjusting $v_{GS}$. The trends depicted are consistent with the behavior of a depletion-mode MOSFET, where a negative threshold voltage ($V_{t} = -1.5 \, \text{V}$) is given.

FIGURE 3.23 The $i-v$ curves of a depletion $n$ MOSFET with $V_{t}=-1.5 \mathrm{~V}, k=1 \mathrm{~mA} / \mathrm{V}^{2}$, and $\lambda=0.05 \mathrm{~V}^{1 / 2}$.

A common DMOSFET application is illustrated in Fig. 3.24a, where the gate and source are tied together $\left(V_{G S}=0\right)$ to form a two-terminal, normally on device. Its $i-v$ characteristic, shown in Fig. 3.24b, indicates that the device can be used either as a resistor, if operated near the origin, or as a current source or sink, if operated to the right of the edge of saturation (EOS). When operated as a current source or sink, the DFET finds application in the biasing of other FETs, such as amplifiers.
image_name:(a)
description:
[
name: V, type: VoltageSource, value: V, ports: {Np: V, Nn: GND}
name: NMOS, type: NMOS, ports: {S: GND, D: V, G: GND}
]
extrainfo:The circuit diagram shows a depletion nMOSFET connected as a two-terminal device with the gate and source tied together, forming a normally-on device. This configuration can function as a resistor or a current source/sink, depending on the operating region.
image_name:(b)
description:The graph in Fig. 3.24b represents the current-voltage ($i-v$) characteristics of a depletion-mode n-channel MOSFET (DFET). This is a plot typically used to illustrate the behavior of a MOSFET when used as a current source.

1. **Type of Graph and Function:**
- This is a plot of current ($i$) versus voltage ($v$), showing the characteristic curve of a DFET.

2. **Axes Labels and Units:**
- The horizontal axis is labeled as $v$, representing voltage. The vertical axis is labeled as $i$, representing current. The units are not explicitly mentioned but are typically volts for $v$ and amperes for $i$.

3. **Overall Behavior and Trends:**
- The graph shows a curve that begins at the origin, rising sharply and then leveling off as it approaches saturation.
- Beyond a certain voltage, labeled as $V_{(\mathrm{EOS})}$, the current $i$ reaches a relatively constant value, indicating the saturation region where the MOSFET behaves as a current source.
- The slope beyond the edge of saturation is labeled as $1/r_o$, indicating the output resistance in the saturation region.

4. **Key Features and Technical Details:**
- The point where the curve transitions from the linear region to the saturation region is marked by $V_{(\mathrm{EOS})}$ on the voltage axis and $I_{(\mathrm{EOS})}$ on the current axis.
- In the saturation region, the current $i$ remains almost constant, which is a desired characteristic for a current source.
- The slope of the line in the saturation region provides information about the output resistance, $r_o$. A smaller slope (larger $r_o$) indicates a better current source.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for $V_{(\mathrm{EOS})}$ and $I_{(\mathrm{EOS})}$, which are critical points defining the transition to the saturation region.
- The line representing $1/r_o$ is also annotated, providing insight into the output resistance of the device when it is operating as a current source.

FIGURE 3.24 The depletion $n$ MOSFET as a current source.
(a) Assuming the data of Fig. 3.23 for the DFET of Fig. 3.24, find the channel resistance $r_{D S}$ in the ohmic region.
(b) What are the edge-of-saturation values $V_{(\mathrm{EOS})}$ and $I_{(\mathrm{EOS})}$ ?
(c) What is the output resistance $r_{o}$ in the saturation region?

#### Solution

(a) With $V_{G S}=0$ we have $V_{O V}=0-V_{t}=0-(-1.5)=1.5 \mathrm{~V}$. So, $r_{D S}=1 /\left(k V_{O V}\right)=$ $1 /(1 \times 1.5)=667 \Omega$.
(b) $V_{(\mathrm{EOS})}=V_{O V}=1.5 \mathrm{~V} . I_{(\mathrm{EOS})}=(k / 2) V_{\text {(EOS) }}^{2}\left(1+\lambda V_{(\mathrm{EOS})}\right)=(1 / 2)(1.5)^{2}(1+$ $0.05 \times 1.5)=1.21 \mathrm{~mA}$.
(c) $r_{o}=1 /\left(\lambda I_{(\mathrm{EOS})}\right)=1 /\left(0.05 \times 1.21 \times 10^{-3}\right)=16.5 \mathrm{k} \Omega$.

### Temperature Dependence

Both the transconductance parameter $k$ and the threshold voltage $V_{t}$ are temperature dependent. ${ }^{3,4}$ The parameter $k$ is proportional to the mobility $\mu$, which decreases with temperature. At room temperature, this dependence exhibits a temperature coefficient (TC) of about $-0.005 \%$ for every degree centigrade, so

$$
\begin{equation*}
\mathrm{TC}(k) \cong-0.005 \% /{ }^{\circ} \mathrm{C} \tag{3.33}
\end{equation*}
$$

The threshold $V_{t}$ depends on temperature via the Fermi potential ( $\phi_{p}<0$ for $n$ MOSFETs and $\phi_{n}>0$ for $p$ MOSFETs). This dependence, in turn, is influenced by doping levels and oxide thickness. For the case of an $n$ MOSFET, engineers remember this dependence via a rule of thumb similar to that for a forward-biased $p n$ junction,

$$
\begin{equation*}
\mathrm{TC}\left(V_{t n}\right) \cong-2 \mathrm{mV} /{ }^{\circ} \mathrm{C} \tag{3.34}
\end{equation*}
$$

For a $p \operatorname{MOSFET}, \mathrm{TC}\left(V_{t p}\right) \cong+2 \mathrm{mV} /{ }^{\circ} \mathrm{C}$.
The two TCs have opposing effects, as a temperature decrease in $k$ tends to reduce $I_{D}$, while a temperature decrease in $V_{t}$ increases $V_{O V}$ and thus tends to increase $I_{D}$. These opposing tendencies can be exploited on purpose to bias a FET at a point where they cancel each other out, resulting in a temperature-independent current $I_{D}$ (see Problem 3.33)

### Sub-Threshold Operation

If we take the square root of both sides of the equation $i_{D}=(k / 2)\left(v_{G S}-V_{t}\right)^{2}$ and plot $\sqrt{i_{D}}$ versus $v_{G S}$, we obtain a straight line with a slope of $\sqrt{k / 2}$ and an intercept at $v_{G S}=V_{t}$, as shown in Fig. 3.25a. In fact, this is often a quick procedure for determining the values of $k$ and $V_{t}$ experimentally.

However, in the vicinity of and below $V_{t}$, the $i_{D}-v_{G S}$ characteristic of an actual MOSFET ceases to be quadratic and becomes exponential, very much like that of a bipolar junction transistor. ${ }^{5}$ When driven with $v_{G S}$ well above $V_{t}$, the MOSFET is said
image_name:(a)
description:The graph in Figure 3.25 (a) is a plot illustrating the relationship between the square root of the drain current, \( \sqrt{i_D} \), and the gate-source voltage, \( v_{GS} \), for a MOSFET device.

Axes Labels and Units:
- **Horizontal Axis (x-axis):** Represents the gate-source voltage, \( v_{GS} \), with no specific units marked, but typically measured in volts.
- **Vertical Axis (y-axis):** Represents the square root of the drain current, \( \sqrt{i_D} \), again with no specific units marked, but typically the current would be in amperes.

Overall Behavior and Trends:
- The graph shows two distinct regions of operation for the MOSFET:
- **Weak Inversion:** This region occurs when \( v_{GS} \) is near or below the threshold voltage, \( V_t \). In this region, the graph starts at the origin and shows a very gradual increase, indicating an exponential relationship typical of sub-threshold conduction.
- **Strong Inversion:** Beyond \( V_t \), the graph transitions to a linear region with a positive slope, indicating a linear increase in \( \sqrt{i_D} \) with \( v_{GS} \). This linear region is characterized by a slope of \( \sqrt{k/2} \).

Key Features and Technical Details:
- **Threshold Voltage, \( V_t \):** Marked on the x-axis, it is the point where the transition from weak to strong inversion occurs.
- **Slope in Strong Inversion:** The slope of the line in the strong inversion region is \( \sqrt{k/2} \), which is a key parameter for determining the transconductance parameter \( k \) of the MOSFET.

Annotations and Specific Data Points:
- The graph is annotated to indicate the regions of weak and strong inversion.
- \( V_t \) is explicitly marked to show the transition point.

This graph is crucial for understanding how a MOSFET transitions from weak to strong inversion as \( v_{GS} \) increases, and it provides a method to determine the threshold voltage and the transconductance parameter experimentally.
image_name:(b)
description:The graph labeled (b) is a plot of the drain current ($i_D$) versus the drain-source voltage ($v_{DS}$) for a MOSFET operating in the sub-threshold region. This is a characteristic curve often used to analyze the behavior of MOSFETs in weak inversion.

1. **Type of Graph and Function:**
- The graph is a plot showing the relationship between drain current and drain-source voltage for different gate-source voltage levels below the threshold voltage.

2. **Axes Labels and Units:**
- The x-axis represents the drain-source voltage ($v_{DS}$) in millivolts (mV), ranging from 0 to 400 mV.
- The y-axis represents the drain current ($i_D$) in picoamperes (pA), ranging from 0 to 100 pA.

3. **Overall Behavior and Trends:**
- The curves show an exponential increase in drain current as the drain-source voltage increases, characteristic of the weak inversion region.
- Each curve is distinct for different values of $V_{GS} - V_t$, showing that as the gate-source voltage gets closer to the threshold voltage from below, the drain current increases.
- The curves start from the origin and rise steeply, eventually reaching a saturation point where further increases in $v_{DS}$ result in minimal increases in $i_D$.

4. **Key Features and Technical Details:**
- The graph includes multiple curves corresponding to different values of $V_{GS} - V_t$: 0 mV, -20 mV, -40 mV, -60 mV, and -80 mV.
- As $V_{GS} - V_t$ decreases (becomes more negative), the curves shift downward, indicating lower drain currents for the same $v_{DS}$.
- The saturation region is more pronounced at higher values of $V_{GS} - V_t$ (closer to 0 mV).

5. **Annotations and Specific Data Points:**
- Each curve is labeled with its respective $V_{GS} - V_t$ value, providing a clear comparison of how the drain current changes with different gate-source voltages.
- The gridlines help in estimating the values of $i_D$ for given $v_{DS}$ values.

FIGURE 3.25 (a) Weak inversion, and (b) the $i_{D}-V_{D S}$ characteristics in the sub-threshold region.
to be operating in strong inversion, but when confined to $v_{G S}$ near or below $V_{t}$ it is said to be operating in weak inversion, or also in the sub-threshold region. In weak inversion, the characteristic is expressed as ${ }^{4,5}$

$$
\begin{equation*}
i_{D}=\frac{W}{L} I_{0} \exp \left(\frac{v_{G S}-V_{t}}{n V_{T}}\right)\left[1-\exp \left(-\frac{v_{D S}}{V_{T}}\right)\right] \tag{3.35}
\end{equation*}
$$

where $W$ and $L$ are the channel width and length; $I_{0}$ is a suitable scaling factor, typically on the order of $1 \mu \mathrm{~A}$ or less; $V_{T}$ is the familiar thermal voltage; and $n$ is a suitable factor, typically $1<n<3$. Figure $3.25 b$ shows the $i_{D}-v_{D S}$ characteristics for different values of $v_{G S}-V_{t}$. Sub-threshold operation finds application in very low power circuits with limited frequency bandwidths. As we proceed, we shall assume operation in strong inversion.

## 3.5 MOSFETS IN RESISTIVE Dc CIRCUITS

We now wish to familiarize ourselves with the behavior of a MOSFET when embedded in a resistive circuit. We find it convenient to start out with simple dc circuits, and to assume $\lambda=0$ both to speed up our calculations and to focus on the essentials of MOSFET behavior.

As we know, to sustain a conductive channel, a FET requires a suitable overdrive voltage $V_{O V}$. For an $n$ MOSFET we have $V_{O V n}=V_{G S}-V_{t n}$, where $V_{t n}>0$ for an enhancement type and $V_{t n}<0$ for a depletion type. For a $p$ MOSFET we have $V_{O V_{p}}=$ $V_{S G}+V_{t p}$, where $V_{t p}<0$ for an enhancement type and $V_{t p}>0$ for a depletion type. Once a channel is conductive, the question arises as to whether operation is in saturation or in the triode region. In certain cases, such as the diode mode, the operating region is evident by inspection. When it isn't, we need to determine (and verify!) it via suitable calculations. As already outlined in Section 3 for the $n$ MOSFET case, one way to proceed is as follows:

- Assume the FET is saturated, and utilize the expression $I_{D}=(k / 2) V_{O V}^{2}$ to carry out the necessary calculations until the values of both $V_{O V}$ and $V_{D S}$ (or $V_{S D}$ for the pMOSFET case) are known.
- If it turns out that $V_{D S}>V_{O V}$ (or $V_{S D}>V_{O V}$ for the $p$ MOSFET case), then the FET is indeed saturated.
- Otherwise you get some kind of contradiction, such as a physically unacceptable result, indicating that our assumption was wrong, and that the FET is in the triode region.

### Diode-Connected MOSFETs

Figure $3.26 a$ shows the resistive biasing of a diode-connected $n$ MOSFET. As we know, for $v \leq V_{t n}$ the FET is in cutoff, giving $i=0$. For $v>V_{t n}$, the FET is saturated, giving the quadratic $i-v$ characteristic

$$
\begin{equation*}
i=\frac{k_{n}}{2}\left(v-V_{t n}\right)^{2} \tag{3.36a}
\end{equation*}
$$

image_name:(a)
description:
[
name: R, type: Resistor, value: R, ports: {N1: VDD, N2: D}
name: NMOS, type: NMOS, ports: {S: GND, D: D, G: D}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit contains a diode-connected NMOS transistor with its gate and drain shorted. It is biased using a resistor R connected to VDD, and a voltage source V is applied across the NMOS and ground. The operating point Q is determined by the intersection of the load line and the NMOS characteristic curve.
image_name:(b)
description:The graph in Figure 3.26(b) is a plot of current versus voltage, specifically illustrating the $i-v$ characteristics of a diode-connected nMOSFET. The graph consists of two curves: a quadratic curve representing the MOSFET's behavior and a linear curve representing the external circuit.

1. **Type of Graph and Function:**
- This is an $i-v$ characteristic plot, where the current $i$ is plotted against the voltage $v$.

2. **Axes Labels and Units:**
- The horizontal axis is labeled "Voltage $v$" and represents the voltage across the MOSFET.
- The vertical axis is labeled "Current $i$" and represents the current through the MOSFET.
- Both axes are likely in linear scale, although specific units are not provided in the image.

3. **Overall Behavior and Trends:**
- The quadratic curve starts at the origin (0,0) and rises steeply after the threshold voltage $V_{tn}$, indicating the MOSFET is in saturation.
- The linear curve starts at the point $(0, \frac{V_{DD}}{R})$ and decreases linearly to $(V_{DD}, 0)$, representing the resistive load line of the external circuit.

4. **Key Features and Technical Details:**
- The intersection point of the two curves is labeled as the operating point, or quiescent point $Q$. This is the point where the current through the MOSFET equals the current through the resistor, satisfying both the MOSFET and circuit equations.
- The threshold voltage $V_{tn}$ is marked on the horizontal axis, showing where the MOSFET transitions from cutoff to saturation.
- The graph highlights the relationship between the MOSFET's quadratic $i-v$ behavior and the linear behavior of the external circuit.

5. **Annotations and Specific Data Points:**
- The point $Q$ is annotated on the graph, indicating the operating conditions of the MOSFET in the circuit.
- The voltage $V$ at the operating point is shown as an intersection with the vertical line drawn from the $Q$ point to the voltage axis.
- The current $I$ at the operating point is shown as an intersection with the horizontal line drawn from the $Q$ point to the current axis.

This graph effectively demonstrates the interaction between the diode-connected MOSFET and its external resistive load, highlighting the operating point where both components satisfy their respective characteristics.

FIGURE 3.26 Investigating the dc operation of a diode-connected nMOSFET.
The $i-v$ characteristic of the circuit external to the FET is the straight line

$$
\begin{equation*}
i=\frac{V_{D D}-v}{R} \tag{3.36b}
\end{equation*}
$$

The two curves intercept at a common point called the operating point, or also the quiescent point $Q$. To find its abscissa $V$, we simply equate the two currents,

$$
\begin{equation*}
\frac{V_{D D}-V}{R}=\frac{k_{n}}{2}\left(V-V_{t n}\right)^{2} \tag{3.37}
\end{equation*}
$$

The resulting quadratic equation is readily solved for $V$. Of the two solutions, only one makes physical sense, so the other must be discarded. We then substitute the physically correct value of $V$ into either of Eq. (3.36) to find $I$. This is a common situation arising when we deal with dc circuits incorporating FETs.

EXAMPLE 3.14 In the circuit of Fig. 3.26a let $V_{D D}=7 \mathrm{~V}$ and $R=10 \mathrm{k} \Omega$, and let the FET have $V_{t n}=1.0 \mathrm{~V}$ and $k_{n}=0.2 \mathrm{~mA} / \mathrm{V}^{2}$. Assuming $\lambda_{n}=0$, find $V$ and $I$.

#### Solution

With resistance in $\mathrm{k} \Omega$ and current in mA , Eq. (3.37) gives

$$
\frac{7-V}{10}=\frac{0.2}{2}(V-1)^{2}
$$

which results in the following quadratic equation

$$
V^{2}-V-6=0
$$

Its solutions are

$$
V=\frac{1 \pm \sqrt{1+24}}{2}
$$

or $V=+3 \mathrm{~V}$ and $V=-2 \mathrm{~V}$. The second value makes no physical sense, as it would imply $V_{G S}<V_{t n}$, and thus a FET in cutoff, when in fact we know that the FET is on. The first value implies the overdrive voltage $V_{O V}=3-1=2 \mathrm{~V}$. The resulting current is $(7-3) / 10=0.4 \mathrm{~mA}$.
(a) In the circuit of Example 3.14, find the value of $R$ needed to give $I=0.9 \mathrm{~mA}$.
(b) What happens if $R$ is shorted out $(R \rightarrow 0)$ ?

#### Solution

(a) We use Eq. (3.36a) to impose

$$
0.9=\frac{0.2}{2}(V-1)^{2}
$$

The solutions are $V=+4 \mathrm{~V}$ and -2 V , but only $V=4 \mathrm{~V}$ is acceptable, so $R=(7-4) / 0.9=3.33 \mathrm{k} \Omega$.
(b) With $R=0$, we have $V=7 \mathrm{~V}$, and $I=(0.2 / 2) \times(7-1)^{2}=3.6 \mathrm{~mA}$.

Figure 3.27 shows the dual situation of Fig. 3.26, involving a $p$ MOSFET but with the source referenced to $V_{D D}$ instead of ground. Considering that $v_{S G}=V_{D D}-v$, the $i-v$ characteristic of the combination consisting of the FET and the $V_{D D}$ source is $i=0$ for $v \geq V_{D D}-\left|V_{t p}\right|$, and the quadratic curve

$$
\begin{equation*}
i=\frac{k_{p}}{2}\left(V_{D D}-v-\left|V_{t p}\right|\right)^{2} \tag{3.38a}
\end{equation*}
$$

for $v<V_{D D}-\left|V_{t p}\right|$. Compared to Fig. 3.26b, the quadratic curve is now folded about the vertical axis, and shifted along the $v$-axis so that conduction starts at $v=V_{D D}-\left|V_{t p}\right|$. The $i-v$ characteristic of the resistor is the straight line

$$
\begin{equation*}
i=\frac{v}{R} \tag{3.38b}
\end{equation*}
$$

The abscissa of the operating point $Q$ is readily found by solving the quadratic equation in $V$

$$
\begin{equation*}
\frac{V}{R}=\frac{k_{p}}{2}\left(V_{D D}-V-\left|V_{t p}\right|\right)^{2} \tag{3.39}
\end{equation*}
$$

and retaining only the physically acceptable solution, as illustrated in the following example.
image_name:(a)
description:
[
name: V_DD, type: VoltageSource, value: V_DD, ports: {Np: VDD, Nn: GND}
name: M1, type: PMOS, ports: {S: VDD, D: V, G: V}
name: R, type: Resistor, value: R, ports: {N1: V, N2: GND}
]
extrainfo:This circuit is a simple diode-connected PMOS transistor with a resistor connected to ground. The PMOS gate and drain are tied together to form a diode connection. The voltage V is across the resistor R, and the current I flows from VDD through the PMOS to the resistor and then to ground.

(a)
image_name:FIGURE 3.27
description:The graph in FIGURE 3.27 is a plot illustrating the DC operation of a diode-connected PMOS transistor circuit. It features two curves intersecting at a point labeled \( Q \). The horizontal axis is labeled "Voltage \( v \)" and spans from 0 to \( V_{DD} \), with a specific point marked at \( V \). The vertical axis is labeled "Current \( i \)" and ranges from 0 to \( \frac{V_{DD}}{R} \), with a specific current \( I \) indicated.

Type of Graph and Function:
This is a current-voltage (I-V) characteristic graph for a diode-connected PMOS transistor with a resistor.

Axes Labels and Units:
- **Horizontal Axis (X-axis):** Voltage \( v \) in volts.
- **Vertical Axis (Y-axis):** Current \( i \) in milliamperes (mA).

Overall Behavior and Trends:
- **First Curve:** Starts at the top left, decreasing non-linearly towards the right, representing the I-V characteristic of the PMOS in saturation.
- **Second Curve:** Starts from the bottom left, increasing linearly towards the top right, representing the load line of the resistor.

Key Features and Technical Details:
- **Intersection Point \( Q \):** Represents the operating point where the PMOS current equals the resistor current. This is where the circuit reaches equilibrium.
- **Voltage \( V \):** The voltage across the resistor at the operating point.
- **Current \( I \):** The current through the PMOS and the resistor at equilibrium.
- **Voltage Threshold \( |V_{tp}| \):** Marked on the horizontal axis, indicating the threshold voltage of the PMOS.

Annotations and Specific Data Points:
- The graph includes a specific annotation for \( |V_{tp}| \), showing the threshold voltage of the PMOS.
- The load line extends from 0 to \( \frac{V_{DD}}{R} \) on the current axis, indicating the maximum possible current through the resistor when \( v = 0 \).
- The curves intersect at point \( Q \), which is crucial for determining the operating conditions of the circuit.

(b)

FIGURE 3.27 Investigating the dc operation of a diode-connected pMOSFET.

EXAMPLE 3.16 (a) In the circuit of Fig. $3.27 a$ let $V_{D D}=5 \mathrm{~V}, V_{t p}=-1.0 \mathrm{~V}$, and $k_{p}=0.5 \mathrm{~mA} / \mathrm{V}^{2}$. Assuming $\lambda_{p}=0$, find $V$ and $I$ if $R=2.0 \mathrm{k} \Omega$.
(b) Repeat, but with $R=0$ (short).

#### Solution

(a) With resistance in $\mathrm{k} \Omega$ and current in mA , Eq. (3.39) gives

$$
\frac{V}{2.0}=\frac{0.5}{2}(5-V-1)^{2}
$$

whose solutions are $V=2 \mathrm{~V}$, and $V=8 \mathrm{~V}$ (physically impossible). Then, $I=2 / 2.0=1.0 \mathrm{~mA}$.
(b) With $R=0$ we get $V=0$, so $I=(0.5 / 2)(5-1)^{2}=4 \mathrm{~mA}$.

### Current Mirrors

A common application of a diode-connected FET, especially in integrated-circuit (IC) design, is the generation of a suitable gate-source voltage drop to bias another similar FET (or FETs). Owing to the fact that when fabricated in IC form, different FETs of the same type enjoy a high degree of matching in the values of $V_{t}, k^{\prime}$, and $\lambda$, both analysis and design are simplified considerably.

Figure 3.28a shows an example involving matched $n$ MOSFETs. Denoting their common gate-source drive as $V_{G S}$, the current drawn by $M_{1}$ is

$$
I_{1}=\frac{1}{2} k^{\prime} \frac{W_{1}}{L_{1}}\left(V_{G S}-V_{t}\right)^{2}\left(1+\lambda V_{G S}\right)
$$

For $v=V_{G S}, M_{2}$ operates under the same voltage conditions as $M_{1}$, giving

$$
I_{2}=\frac{1}{2} k^{\prime} \frac{W_{2}}{L_{2}}\left(V_{G S}-V_{t}\right)^{2}\left(1+\lambda V_{G S}\right)
$$

Combining the two equations, we easily obtain, for $v=V_{G S}$,

$$
\begin{equation*}
I_{2}=\frac{W_{2} / L_{2}}{W_{1} / L_{1}} I_{1} \tag{3.40}
\end{equation*}
$$

image_name:(a)
description:
[
name: R, type: Resistor, value: R, ports: {N1: VDD, N2: VGs}
name: M1, type: NMOS, ports: {S: GND, D: VGs, G: VGs}
name: M2, type: NMOS, ports: {S: GND, D: V, G: Vas}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a current mirror using NMOS transistors M1 and M2. The current I1 through M1 is mirrored to M2, providing output current i to the load. The load is connected to the drain of M2 and is grounded.
image_name:(b)
description:The function graph (b) represents the $i-v$ characteristic of an nMOSFET current mirror circuit. This type of graph is typically a plot showing the relationship between the current ($i$) through the load and the voltage ($v$) across it.

1. **Type of Graph and Function:**
- The graph is an $i-v$ characteristic curve, which is a common representation in electronics to show how current varies with voltage in a particular circuit configuration.

2. **Axes Labels and Units:**
- The x-axis represents the voltage $v$ across the load, likely in volts (V).
- The y-axis represents the current $i$ through the load, likely in amperes (A).
- The scales for both axes could be linear, although this is not specified in the provided context.

3. **Overall Behavior and Trends:**
- The general behavior of the graph would typically show a linear region where the current $i$ is proportional to the voltage $v$, reflecting the operation of the current mirror circuit where $I_2 = I_1$ when $W/L$ ratios are identical.
- There may be saturation regions where the current levels off, indicating the limits of the MOSFET's operation.

4. **Key Features and Technical Details:**
- The linear region is significant in demonstrating the mirror effect, where $M_2$ mirrors the current of $M_1$.
- There might be a threshold voltage below which the current is negligible, indicating the cut-off region of the MOSFET.
- The saturation region might be marked by a flat line where the current no longer increases with voltage.

5. **Annotations and Specific Data Points:**
- The graph might include reference lines or annotations marking significant points such as the threshold voltage or the saturation current.
- Any specific data points, such as the maximum current or voltage values, would be critical for understanding the limits of the circuit's operation.

This $i-v$ characteristic graph helps in understanding the behavior of the current mirror circuit, particularly how the output current $i$ relates to the input voltage $v$, and how well $M_2$ can replicate the current of $M_1$ under given conditions.

(a)
image_name:(a)
description:The graph shown is an $i-v$ characteristic curve for an nMOSFET current mirror, specifically illustrating the relationship between the output current $i$ and the input voltage $v$.

1. **Type of Graph and Function:**
- This is a characteristic curve graph for a current mirror circuit using MOSFETs.

2. **Axes Labels and Units:**
- The horizontal axis represents the input voltage $v$.
- The vertical axis represents the output current $i$.
- There are no specific units mentioned, but typically $v$ would be in volts and $i$ in amperes.

3. **Overall Behavior and Trends:**
- The graph shows an initial rapid increase in current as the voltage increases from zero.
- After reaching a certain point, the curve flattens, indicating saturation where the current remains relatively constant despite further increases in voltage.
- The curve has a slight upward slope in the saturation region, representing the finite output resistance $1/r_o$.

4. **Key Features and Technical Details:**
- The curve starts from the origin (0,0) and initially rises steeply.
- It levels off at a point marked by the ratio $(W_2/L_2)/(W_1/L_1) I_1$, indicating the mirrored current when devices have identical $W/L$ ratios.
- The graph includes important voltage markers: $V_{OV}$ (overdrive voltage) and $V_{GS}$ (gate-source voltage), which are critical for transistor operation.
- The slope in the saturation region is denoted by $1/r_o$, indicating the output conductance.

5. **Annotations and Specific Data Points:**
- The graph is annotated with $V_{OV}$ and $V_{GS}$ on the voltage axis, marking significant operational points.
- The current level $(W_2/L_2)/(W_1/L_1) I_1$ is a key reference point for understanding the mirroring behavior of the current mirror.

This graph is essential for understanding how well the MOSFET $M_2$ can replicate the current of $M_1$ in a current mirror circuit, particularly when the transistors have identical $W/L$ ratios. It highlights the saturation behavior and the finite output resistance of the circuit.

(b)

FIGURE 3.28nMOSFET current mirror, and its $i-v$ characteristic.

Of particular interest is the case of devices with identical $W / L$ ratios, for then Eq. (3.40) gives, for $v=V_{G S}, I_{2}=I_{1}$, indicating that the current of $M_{2}$ will mirror that of $M_{1}$, this being the reason for the circuit's name.

In the example shown, $I_{1}$ is established by $R$ in a manner similar to that of Example 3.14. However, there are also other techniques for forcing current through $M_{1}$, but $M_{2}$ will just mirror the behavior of $M_{1}$ regardless of the technique. In IC design we have the flexibility of establishing virtually any ratio between the two currents by suitably specifying the $W / L$ ratios of the two devices. For instance, if $W_{1} / L_{1}=$ $(1 \mu \mathrm{~m}) /(1 \mu \mathrm{~m})$, then, specifying $W_{2} / L_{2}=(2 \mu \mathrm{~m}) /(1 \mu \mathrm{~m})$ we get, for $v=V_{G S}, I_{2}=2 I_{1}$. Likewise, with $W_{2} / L_{2}=(1 \mu \mathrm{~m}) /(2 \mu \mathrm{~m})$ we get $I_{2}=0.5 I_{1}$, whereas with $W_{2} / L_{2}=$ $(1 \mu \mathrm{~m}) /(1 \mu \mathrm{~m})$ we get $I_{2}=I_{1}$.

The $i-v$ characteristic of the current mirror is shown in Fig. 3.28b. As we know, the saturation portion of the curve exhibits a slope of $1 / r_{o}$. Moreover, the saturation region extends all the way down to $v=V_{O V}=V_{G S}-V_{t}$.

Assume $V_{D D}=5 \mathrm{~V}$ and identical devices with $V_{t}=1.0 \mathrm{~V}, k=0.8 \mathrm{~mA} / \mathrm{V}^{2}$, and $\lambda=0.02 \mathrm{~V}^{-1}$ in Fig. 3.28a.
(a) Find $R$ so that the circuit gives $i=100 \mu \mathrm{~A}$ for $v=V_{G S}$. Here, assume $\lambda=0$ for simplicity.
(b) Find the lower voltage limit for operation in saturation, as well as $r_{o}$ and the per-volt change of $i$ in the saturation region.

#### Solution

(a) The overdrive voltage required to sustain the given current is

$$
V_{O V}=\sqrt{\frac{2 I_{1}}{k}}=\sqrt{\frac{2 \times 100 \times 10^{-6}}{0.8 \times 10^{-3}}}=0.5 \mathrm{~V}
$$

Consequently, $V_{G S}=V_{t}+V_{O V}=1+0.5=1.5 \mathrm{~V}$, and $R=\left(V_{D D}-V_{G S}\right) / I_{1}=$ $(5-1.5) / 0.1=35 \mathrm{k} \Omega$.
(b) The saturation region extends over the range $v \geq 0.5 \mathrm{~V}$, where $r_{o} \cong 1 /(\lambda I)=$ $1 /\left(0.02 \times 100 \times 10^{-6}\right)=500 \mathrm{k} \Omega$, and where $i$ increases with $v$ at the rate of $1 /(500 \mathrm{k} \Omega)=2 \mu \mathrm{~A} / \mathrm{V}$.

The current mirror of Fig. 3.28a is also referred to as a current $\operatorname{sink}$ because $M_{2}$ sinks current from the load. By contrast, its $p$ MOSFET counterpart of Fig. $3.29 a$ is referred to as a current source, as $M_{2}$ in this case sources current to the load. Using similar reasoning we conclude that for $v=V_{S S}-V_{S G}$ the two transistors operate under identical voltage conditions, so $M_{2}$ gives $I_{2}=\left[\left(W_{2} / L_{2}\right) /\left(W_{1} / L_{1}\right)\right] I_{1}$. As depicted in Fig. 3.29b, the saturation region extends all the way up to $V_{D D}-V_{O V}$, and the slope of the saturation-region curve is now $-1 / r_{o}$.
image_name:(a)
description:
[
name: M1, type: PMOS, ports: {S: VSS, D: g1g2d1, G: g1g2d1}
name: M2, type: PMOS, ports: {S: VSS, D: V, G: g1g2d1}
name: R, type: Resistor, value: R, ports: {N1: g1g2d1, N2: GND}
name: VSS, type: VoltageSource, value: VSS, ports: {Np: VSS, Nn: GND}
name: Load, type: Other, ports: {N1: V, N2: GND}
]
extrainfo:This is a PMOS current mirror circuit. M1 is used to mirror the current to M2, which drives the load. The voltage VSS is the supply voltage for the circuit. The resistor R sets the reference current I1. The graph (b) shows the i-v characteristic of the current mirror, indicating the saturation region and the effect of channel-length modulation.
image_name:(b)
description:The graph depicted in Fig. 3.29(b) is an I-V characteristic curve for a MOSFET current mirror circuit. The graph is plotted with the voltage \( v \) on the horizontal axis and the current \( i \) on the vertical axis. Both axes are likely using linear scales.

Axes Labels and Units:
- **Horizontal Axis (\( v \))**: Represents the voltage across the device.
- **Vertical Axis (\( i \))**: Represents the current through the device.

Overall Behavior and Trends:
- The graph shows the behavior of the current mirror as the voltage \( v \) changes.
- Initially, as \( v \) increases from zero, the current \( i \) remains constant, indicating operation in the saturation region.
- The constant current is given by \( \left(\frac{W_2/L_2}{W_1/L_1}\right) I_1 \), showing the proportionality between the transistors in the current mirror.
- As \( v \) approaches \( V_{SS} - V_{SG} \), the current begins to decrease slightly, indicating the onset of the transition out of saturation.
- The slope in this region is \(-1/r_o\), where \( r_o \) is the output resistance.
- The current continues to decrease more sharply as \( v \) approaches \( V_{SS} - V_{OV} \), marking the boundary to the cutoff region.

Key Features and Technical Details:
- **Saturation Region**: The flat portion of the curve where the current is constant.
- **Transition Region**: The region where the slope \(-1/r_o\) is observed, indicating decreasing current.
- **Cutoff Region**: The steep decline in current past \( V_{SS} - V_{OV} \).

Annotations and Specific Data Points:
- The graph is annotated with critical voltage points: \( V_{SS} - V_{SG} \) and \( V_{SS} - V_{OV} \), marking transitions between different operating regions.
- The slope \(-1/r_o\) is explicitly marked on the graph, indicating the characteristic behavior in the transition region.

FIGURE $3.29 p$ MOSFET current mirror, and its $i-v$ characteristic. $-1.5 \mathrm{~V}, k_{2}=2 k_{1}=0.5 \mathrm{~A} / \mathrm{V}^{2}$, and $\lambda_{2}=\lambda_{1}=0.04 \mathrm{~V}^{-1}$. Find $R$ for $V_{O V}=2 \mathrm{~V}$. What is the corresponding value of $I_{1}$ ?
(b) Find $i$ at $v=V_{S S}-V_{S G}, v=0$, and $v=V_{S S}-V_{O V}$.

#### Solution

(a) With $V_{O V}=2 \mathrm{~V}$ we have $V_{S D 1}=V_{S G}=V_{O V}+\left|V_{t}\right|=2+1.5=3.5 \mathrm{~V}$. Since $k_{1}=0.25 \mathrm{~mA} / \mathrm{V}^{2}$,

$$
I_{1}=\frac{0.25}{2} 2^{2}(1+0.04 \times 3.5)=0.57 \mathrm{~mA}
$$

Moreover, $R=\left(V_{S S}-V_{S G}\right) / I_{1}=(6-3.5) / 0.57=4.39 \mathrm{k} \Omega$.
(b) For $v=6-3.5=2.5 \mathrm{~V}$ we get $i=\left(k_{2} / k_{1}\right) I_{1}=2 \times 0.57=1.14 \mathrm{~mA}$. For $v=0$ we have $V_{S D 2}=6 \mathrm{~V}$, so

$$
i=\frac{0.5}{2} 2^{2}(1+0.04 \times 6)=1.24 \mathrm{~mA}
$$

Likewise, for $v=6-2=4 \mathrm{~V}$ we have $V_{S D 2}=2 \mathrm{~V}$, so $i=1(1+0.04 \times 2)=$ 1.08 mA .

### Resistive Biasing of MOSFETs—Dual-Supply Schemes

When studying FET amplifiers, we shall find it necessary to bias a FET at a specific dc operating point $Q=Q\left(I_{D}, V_{D S}\right)$ in the saturation region, a region also called the active region. FET biasing can be dealt with from either a design or an analysis viewpoint. The objective of design is to devise a suitable external circuit to bias the FET at the specified operating point $Q$. Conversely, the objective of analysis is to find the operating point $Q$, given the circuit in which the FET is embedded. The diode-connected FETs examined above have already provided examples of dc biasing in saturation.
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: s1, D: d1, G: GND}
name: RD, type: Resistor, value: RD, ports: {N1: d1, N2: VDD}
name: RS, type: Resistor, value: RS, ports: {N1: s1, N2: GND}
]
extrainfo:The circuit is a dual-supply biasing setup for an NMOS transistor operating in the active region. It uses resistors RD and RS to establish the drain current ID and the drain-source voltage VDS. The gate of the NMOS is grounded, resulting in zero gate current (IG=0).
image_name:(b)
description:The circuit diagram (b) represents the DC equivalent of an NMOS transistor biased in the active region using dual power supplies. The drain current ID is 0.5 mA, and the voltages at key nodes are marked as +10V, +1V, -4V, and -10V.
image_name:(c)
description:
[
name: M1, type: NMOS, ports: {S: -4V, D: 5V, G: GND}
name: RD, type: Resistor, value: 18kΩ, ports: {N1: +10V, N2: 5V}
name: RS, type: Resistor, value: 12kΩ, ports: {N1: -4V, N2: -10V}
]
extrainfo:The circuit is a dual-supply biasing scheme for an NMOS transistor. The NMOS transistor M1 is biased with a gate voltage of 0V (ground), a drain voltage of 5V, and a source voltage of -4V. The resistors RD and RS are used to set the drain and source voltages, respectively. A current source of 0.5mA is connected from +10V to ground. Additional voltages of +1V and -4V are applied across specific nodes.

FIGURE 3.30 Dual-supply biasing of an nMOSFET in the active region. (a) General circuit, (b) its dc equivalent, and (c) an actual example, showing all voltages and currents.

The biasing scheme of Fig. 3.30a, based on a dual power-supply system, utilizes the resistance $R_{S}$ to establish the value of $I_{D}$, and the resistance $R_{D}$ to establish the value of $V_{D S}$. To better understand circuit operation, replace the $n \mathrm{FET}$ with its dc equivalent as in Fig. 3.30b, where for simplicity we are assuming $\lambda_{n}=0$ and, hence, $r_{o}=\infty$. As we know, to draw a given current $I_{D}$, the $n$ FET requires the overdrive voltage $V_{O V}=\sqrt{2 I_{D} / k_{n}}$, indicating that in the present biasing scheme the source must be held at $V_{S}=-\left(V_{t n}+V_{O V}\right)$. This task is performed by $R_{S}$, which is chosen on the basis of dropping the voltage difference $\left(V_{S}-V_{S S}\right)$ at the given current $I_{D}$. An example will better illustrate.

In the circuit of Fig. 3.30a let $V_{D D}=10 \mathrm{~V}$ and $V_{S S}=-10 \mathrm{~V}$, and let the FET have $V_{t n}=1.5 \mathrm{~V}$ and $k_{n}=0.16 \mathrm{~mA} / \mathrm{V}^{2}$. Assuming $\lambda_{n}=0$, specify values for $R_{S}$ and $R_{D}$ to bias the FET at $I_{D}=0.5 \mathrm{~mA}$ and $V_{D S}=5 \mathrm{~V}$.

#### Solution

The required overdrive voltage is $V_{O V}=\sqrt{2 I_{D} / k_{n}}=\sqrt{2 \times 0.5 / 16}=2.5 \mathrm{~V}$, indicating that the source must be held at $V_{S}=-\left(V_{t n}+V_{O V}\right)=-(1.5+2.5)=-4 \mathrm{~V}$. This requires

$$
R_{S}=\frac{V_{S}-V_{S S}}{I_{D}}=\frac{-4-(-10)}{0.5}=12 \mathrm{k} \Omega
$$

To ensure $V_{D S}=5 \mathrm{~V}$, the drain voltage must be held at $V_{D}=V_{S}+V_{D S}=-4+5=$ +1 V. Consequently,

$$
R_{D}=\frac{V_{D D}-V_{D}}{I_{D}}=\frac{10-1}{0.5}=18 \mathrm{k} \Omega
$$

The circuit is shown in Fig. 3.30c, and since $V_{D S}>V_{O V}(5>2.5)$, the FET is indeed saturated.

Remark: We wonder what makes the FET maintain $I_{D}$ precisely at 0.5 mA . We justify as follows:

- Suppose that for some reason the FET attempted to draw less than 0.5 mA . Then, the voltage drop across $R_{S}$ would decrease, causing a decrease also in $V_{S}$. But this, in turn, would increase $V_{G S}$, and hence $V_{O V}$, in effect forcing the FET to draw more current.
- Conversely, any attempt by the FET to draw more than 0.5 mA would be met by a decrease in $V_{O V}$, and thus by a directive to draw less current.
- In either case, any attempt by $I_{D}$ to deviate from 0.5 mA is met by a counteraction that tends to neutralize the attempted deviation and restore $I_{D}$ to the prescribed value of 0.5 mA . This state of affairs is summarized by saying that $R_{S}$ provides a negative feedback action around the FET, and that this action stabilizes the biasing condition of the device. Negative feedback is also referred to as degenerative feedback, to distinguish it from positive feedback, which may become regenerative. Consequently, $R_{S}$ is also referred to as degeneration resistance (more on this in Chapter 7).
(a) In the circuit of Fig. 3.31a let the FET have $V_{t n}=1.0 \mathrm{~V}, k_{n}=0.5 \mathrm{~mA} / \mathrm{V}^{2}$. Assuming $\lambda_{n}=0$, find the FET's operating point $Q$.
(b) To what value must we increase $R_{D}$ to bring the FET to operate at the edge of saturation (EOS)?
(c) What happens if $R_{D}$ is raised to twice the value found in part (b)?
image_name:(a)
description:
[
name: RD, type: Resistor, value: 4kΩ, ports: {N1: +5V, N2: d1}
name: RS, type: Resistor, value: 2kΩ, ports: {N1: s1, N2: GND}
name: M1, type: NMOS, ports: {S: s1, D: d1, G: GND}
]
extrainfo:The circuit is a common-source NMOS amplifier with degeneration resistance Rs. The NMOS transistor M1 is operating with a drain current ID and has a gate connected to ground. The circuit is powered by a +5V supply, and the source is connected to a -5V supply through Rs. The resistor RD is connected between the drain and the +5V supply.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: s1, D: d1, G: GND}
name: RD, type: Resistor, value: 4 kΩ, ports: {N1: d1, N2: +5V}
name: RS, type: Resistor, value: 2 kΩ, ports: {N1: s1, N2: -5V}
]
extrainfo:The circuit is a common-source NMOS amplifier with degeneration resistance. The NMOS transistor M1 is connected with its drain at node d1 and source at node s1. The gate is grounded. RD is connected to +5V and RS is connected to -5V. The circuit is operating with a drain current ID.
image_name:(c)
description:
[
name: RD, type: Resistor, value: 6kΩ, ports: {N1: VDD, N2: d1}
name: RS, type: Resistor, value: 2kΩ, ports: {N1: s1, N2: GND}
name: M1, type: NMOS, ports: {S: s1, D: d1, G: GND}
]
extrainfo:The circuit is operating at the edge of saturation with a 6kΩ drain resistor. The NMOS transistor M1 has its source connected to ground through a 2kΩ resistor, and its drain connected to a 6kΩ resistor leading to +5V. The gate is grounded. The voltage across the NMOS is 2V.
image_name:(d)
description:
[
name: RD, type: Resistor, value: 12 kΩ, ports: {N1: 5V, N2: d1}
name: RS, type: Resistor, value: 2 kΩ, ports: {N1: s1, N2: -5V}
name: M1, type: NMOS, ports: {S: s1, D: d1, G: GND}
]
extrainfo:The circuit is a simple NMOS amplifier with a degeneration resistor RS and a load resistor RD. The NMOS transistor M1 is operating at the edge of saturation with V_DS = 0.57 V and a drain current of 0.674 mA. The circuit is powered by a +5V supply.

FIGURE 3.31 (a) Circuit of Example 3.20, and operation (b) in saturation, (c) at the EOS, and (d) in the triode region.

#### Solution

(a) Following the directive at the beginning of this section, we start out by assuming a saturated FET, and we check afterwards whether the assumption was correct. If the assumption proves wrong, it simply means that the FET is in the triode region, and that we must redo our calculations using the trioderegion expression for $I_{D}$. In saturation we have

$$
\begin{aligned}
I_{D} & =\frac{k_{n}}{2}\left(V_{G S}-V_{t n}\right)^{2}=\frac{k_{n}}{2}\left(V_{G}-V_{S}-V_{t n}\right)^{2}=\frac{k_{n}}{2}\left(0-V_{S}-V_{t n}\right)^{2} \\
& =\frac{0.5}{2}\left[-\left(-5+2 \times I_{D}\right)-1\right]^{2}=\frac{1}{4}\left(4-2 I_{D}\right)^{2}
\end{aligned}
$$

After expanding, collecting, and simplifying, we end up with the quadratic equation

$$
I_{D}^{2}-5 I_{D}+4=0
$$

whose solutions are $I_{D}=1 \mathrm{~mA}$ and $I_{D}=4 \mathrm{~mA}$ (physically impossible). We finally get $V_{D}=5-4 \times 1=1 \mathrm{~V}$ and $V_{S}=-5+2 \times 1=-3 \mathrm{~V}$. Consequently, $V_{D S}=1-(-3)=4 \mathrm{~V}$, and $V_{O V}=-(-3)-1=2 \mathrm{~V}$. Since $V_{D S}>V_{O V}(4>2)$, the FET is indeed in saturation. Summarizing, the operating point is $Q=Q(1 \mathrm{~mA}, 4 \mathrm{~V})$. The situation is shown in Fig. 3.31b.
(b) Raising $R_{D}$ lowers $V_{D}$, in turn reducing $V_{D S}$. The EOS is reached when $V_{D S}=V_{O V}=2 \mathrm{~V}$, or $V_{D}=V_{S}+V_{O V}=-3+2=-1 \mathrm{~V}$. The corresponding resistance value is $R_{D}=[5-(-1)] / 1=6 \mathrm{k} \Omega$. The situation is shown in Fig. 3.31c, where the operating point is now $Q=Q(1 \mathrm{~mA}, 2 \mathrm{~V})$.
(c) With $R_{D}=2 \times 6=12 \mathrm{k} \Omega$ the FET will definitely be in the triode region. We can convince ourselves by noting that if it were still in saturation, we would have $V_{D}=5-12 \times 1=-7 \mathrm{~V}$, thus implying $V_{D S}=V_{D}-V_{S}=-7-(-3)=$ -4 V , an absurdity! Clearly, we must re-compute $I_{D}$, but using the triode expression. In part (a) we have found that

$$
V_{G S}-V_{t n}=4-2 I_{D}
$$

Moreover, we have $V_{D S}=V_{D}-V_{S}=\left(5-12 \times I_{D}\right)-\left(-5+2 \times I_{D}\right)$ or

$$
V_{D S}=10-14 I_{D}
$$

Consequently,

$$
I_{D}=k_{n}\left[\left(V_{G S}-V_{t n}\right) V_{D S}-\frac{V_{D S}^{2}}{2}\right]=0.5\left[\left(4-2 I_{D}\right)\left(10-14 I_{D}\right)-\frac{\left(10-14 I_{D}\right)^{2}}{2}\right]
$$

Collecting terms and solving the ensuing quadratic equation we get

$$
I_{D}=\frac{31 \pm \sqrt{261}}{70}
$$

or $I_{D}=0.674 \mathrm{~mA}$, and $I_{D}=0.212 \mathrm{~mA}$ (physically impossible-can you tell why?). The various voltages are easily found as $V_{D}=-3.08 \mathrm{~V}, V_{S}=-3.65 \mathrm{~V}$, and $V_{D S}=0.57 \mathrm{~V}$. The situation is summarized in Fig. 3.31d, where the operating point is now $Q=Q(0.674 \mathrm{~mA}, 0.57 \mathrm{~V})$. Finally, we find $V_{O V}=$ 2.65 V . The fact that $V_{D S}<V_{O V}(0.57<2.65)$ confirms that the FET is indeed operating in the triode region.

Figure 3.32 shows the $p$ MOSFET counterpart of the $n$ MOSFET circuit of Fig. 3.31. Again, this circuit can be investigated from either a design or an analysis standpoint. The procedure is similar to that of the $n$ MOSFET, as long as we handle voltages and currents in dual fashion.

EXAMPLE 3.21
(a) In the circuit of Fig. $3.32 a$ let $V_{S S}=6 \mathrm{~V}$ and $V_{D D}=-6 \mathrm{~V}$, and let the FET have $V_{t p}=-1.5 \mathrm{~V}$ and $k_{p}=0.5 \mathrm{~mA} / \mathrm{V}^{2}$. Assuming $\lambda_{p}=0$, specify suitable values for $R_{S}$ and $R_{D}$ to bias the FET at $I_{D}=0.25 \mathrm{~mA}$ and $V_{S D}=4 \mathrm{~V}$. What region is the FET operating in?
(b) Find the FET's operating point and region if $R_{S}=6 \mathrm{k} \Omega$ and $R_{D}=16 \mathrm{k} \Omega$.
image_name:(a)
description:
[
name: M1, type: PMOS, ports: {S: S1, D: d1, G: GND}
name: RS, type: Resistor, value: RS, ports: {N1: VSS, N2: S1}
name: RD, type: Resistor, value: RD, ports: {N1: d1, N2: VDD}
]
extrainfo:The circuit is a dual-supply biasing configuration for a pMOSFET. It includes a PMOS transistor biased with resistors RS and RD. The source is connected to VSS through RS, the drain is connected to VDD through RD, and the gate is grounded. The circuit is designed to operate the FET in the saturation region.
image_name:(b)
description:The circuit is a dual-supply biasing configuration for a PMOS transistor. It is designed to operate in the saturation region with specified values for source and drain resistors to achieve desired biasing conditions.

FIGURE 3.32 Dual-supply biasing of a pMOSFET in the saturation (or active) region.

#### Solution

(a) Assuming saturation, and retracing dual steps of those of Example 3.19, we find

$$
\begin{aligned}
& V_{O V}=\sqrt{2 I_{D} / k_{p}}=\sqrt{2 \times 0.25 / 0.5}=1 \mathrm{~V} \\
& V_{S}=V_{O V}+\left|V_{t p}\right|=1+1.5=2.5 \mathrm{~V} \\
& R_{S}=\left(V_{S S}-V_{S}\right) / I_{D}=(6-2.5) / 0.25=14 \mathrm{k} \Omega \\
& V_{D}=V_{S}-V_{S D}=2.5-4=-1.5 \mathrm{~V} \\
& R_{D}=\left(V_{D}-V_{D D}\right) / I_{D}=[-1.5-(-6)] / 0.25=18 \mathrm{k} \Omega
\end{aligned}
$$

The circuit is shown in Fig. 3.33a. The fact that $V_{S D}>V_{O V}(4>1)$ confirms saturation-region operation.
image_name:(a)
description:
[
name: M1, type: PMOS, ports: {S: s1, D: d1, G: GND}
name: Resistor1, type: Resistor, value: 14kΩ, ports: {N1: 6V, N2: s1}
name: Resistor2, type: Resistor, value: 18kΩ, ports: {N1: d1, N2: -6V}
name: VoltageSource1, type: VoltageSource, value: 6V, ports: {Np: 6V, Nn: GND}
name: VoltageSource3, type: VoltageSource, value: -6V, ports: {Np: GND, Nn: -6V}
]
extrainfo:The circuit is a PMOS transistor circuit operating in saturation, with a current source and voltage sources providing biasing. The resistors set the voltage levels at the nodes.
image_name:(b)
description:
[
name: M1, type: PMOS, ports: {S: GND, D: d1, G: GND}
name: R1, type: Resistor, value: 6kΩ, ports: {N1: VDD, N2: d1}
name: R2, type: Resistor, value: 16kΩ, ports: {N1: d1, N2: GND}
]
extrainfo:The circuit is a PMOS configuration with a voltage source of 1V and a current source of 0.5mA. The resistors are connected to form a voltage divider across the PMOS transistor.

FIGURE 3.33 Circuits of Example 3.21.
(b) Assume saturation again, and check. We have

$$
V_{S G}-\left|V_{t p}\right|=V_{S S}-R_{S} I_{D}-\left|V_{t p}\right|=6-6 I_{D}-1.5=4.5-6 I_{D}
$$

Consequently, in saturation we would have

$$
I_{D}=\frac{0.5}{2}\left(4.5-6 I_{D}\right)^{2}
$$

This quadratic equation admits the solutions $I_{D}=1.1 \mathrm{~mA}$ and $I_{D}=0.51 \mathrm{~mA}$, both of which are untenable because the first would imply $V_{S G}<0$ (cutoff), while the second would imply $V_{S D}<V_{O V}$ (triode), both of which contradict the saturation assumption. Evidently the FET is in the triode region. Considering that

$$
V_{S D}=\left(V_{S S}-V_{D D}\right)-\left(R_{D} I_{D}-R_{S} I_{D}\right)=12-22 I_{D}
$$

we have, in the triode region,

$$
I_{D}=0.5\left[\left(4.5-6 I_{D}\right) \times\left(12-22 I_{D}\right)-\left(12-22 I_{D}\right)^{2} / 2\right]
$$

This quadratic equation admits two solutions, with the physically acceptable one being $I_{D}=0.5 \mathrm{~mA}$. Consequently, $V_{S D}=12-22 \times 0.5=1 \mathrm{~V}$, indicating the operating point $Q=Q(0.5 \mathrm{~mA}, 1 \mathrm{~V})$. The circuit is shown in Fig. 3.33b. As a check, we calculate $V_{O V}=4.5-6 \times 0.5=1.5 \mathrm{~V}$, and confirm that $V_{S D}<V_{O V}(1<1.5)$, that is, triode-region operation.

### Resistive Biasing of MOSFETs-Single-Supply Schemes

Figure 3.34 shows single-supply MOSFET biasing alternatives. The function of the voltage divider $R_{1}-R_{2}$ is to establish an intermediate bias voltage for the gate. Since the gate draws zero dc current, these resistances can be chosen to be fairly large if desired, say, in the $\mathrm{M} \Omega$-range.

EXAMPLE 3.22
In the circuit of Fig. 3.34a let $V_{D D}=15 \mathrm{~V}$, and let the FET have $V_{t n}=2.0 \mathrm{~V}$ and $k_{n}=0.5 \mathrm{~mA} / \mathrm{V}^{2}$. Assuming $\lambda_{n}=0$, specify suitable resistance values to ensure $I_{D}=1 \mathrm{~mA}$, to bias the source at $(1 / 3) V_{D D}$, and to bias the drain halfway between the drain voltage corresponding to the edge of conduction (EOC) and that corresponding to the edge of saturation (EOS). Impose a current of $5 \mu \mathrm{~A}$ through $R_{1}$ and $R_{2}$.
image_name:(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: q1}
name: R2, type: Resistor, value: R2, ports: {N1: q1, N2: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: d1}
name: RS, type: Resistor, value: RS, ports: {N1: s1, N2: GND}
name: M1, type: NMOS, ports: {S: s1, D: d1, G: q1}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a single-supply biasing configuration for an NMOS transistor. It includes resistors R1 and R2 forming a voltage divider for the gate bias, and RD and RS for drain and source resistances. The NMOS transistor M1 is used for amplification or switching applications.

(a)
image_name:(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: VSS, N2: q1}
name: R2, type: Resistor, value: R2, ports: {N1: q1, N2: GND}
name: RS, type: Resistor, value: RS, ports: {N1: VSS, N2: s1}
name: RD, type: Resistor, value: RD, ports: {N1: d1, N2: GND}
name: M1, type: PMOS, ports: {S: s1, D: d1, G: q1}
name: VSS, type: VoltageSource, value: VSS, ports: {Np: VSS, Nn: GND}
]
extrainfo:The circuit is a single-supply biasing configuration for a PMOS transistor. It includes resistors R1 and R2 forming a voltage divider for the gate bias, and RD and RS for drain and source resistances. The PMOS transistor M1 is used for amplification or switching applications.

(b)

FIGURE 3.34 Single-supply biasing for (a) the $n M O S F E T$ and (b) the $p$ MOSFET.

#### Solution

The required overdrive is $V_{O V}=\sqrt{2 I_{D} / k_{n}}=\sqrt{2 \times 1 / 0.5}=2.0 \mathrm{~V}$, so $V_{G S}=V_{t n}+$ $V_{O V}=2+2=4 \mathrm{~V}$. We thus have

$$
\begin{aligned}
& V_{S}=(1 / 3) V_{D D}=(1 / 3) 15=5 \mathrm{~V} \\
& V_{G}=V_{S}+V_{G S}=5+4=9 \mathrm{~V}
\end{aligned}
$$

Consequently, $R_{1}=(15-9) / 5=1.2 \mathrm{M} \Omega, R_{2}=9 / 5=1.8 \mathrm{M} \Omega$, and $R_{S}=$ $5 / 1=5 \mathrm{k} \Omega$. Now, the value of $V_{D}$ corresponding to the EOC is $V_{D(\mathrm{EOC})}=V_{D D}=$ 15 V , and that corresponding to the EOS is $V_{D(\mathrm{EOS})}=V_{S}+V_{O V}=5+2=7 \mathrm{~V}$. The halfway value is thus

$$
V_{D}=(15+7) / 2=11 \mathrm{~V}
$$

Finally, $R_{D}=(15-11) / 1=4 \mathrm{k} \Omega$.

EXAMPLE 3.23 In the circuit of Fig. 3.34a let $V_{D D}=12 \mathrm{~V}, R_{1}=1 \mathrm{M} \Omega, R_{2}=1.4 \mathrm{M} \Omega, R_{D}=8 \mathrm{k} \Omega$, and $R_{S}=10 \mathrm{k} \Omega$, and let the FET have $V_{t n}=1.0 \mathrm{~V}$ and $k_{n}=0.4 \mathrm{~mA} / \mathrm{V}^{2}$. Assuming $\lambda_{n}=0$, find the operating point $Q$.

#### Solution

Start out by assuming the FET is in saturation, and check later that the assumption was correct. We have

$$
V_{G S}=V_{G}-V_{S}=\frac{R_{2}}{R_{1}+R_{2}} V_{D D}-R_{S} I_{S}=\frac{1.4}{1+1.4} 12-10 I_{S}=7-10 I_{D}
$$

and

$$
I_{D}=\frac{k_{n}}{2}\left(V_{G S}-V_{t n}\right)^{2}=\frac{0.4}{2}\left(7-10 I_{D}-1\right)^{2}
$$

This quadratic equation admits the solutions $I_{D}=0.45 \mathrm{~mA}$ and $I_{D}=0.8 \mathrm{~mA}$ (physically impossible-can you tell why?). Consequently,

$$
\begin{aligned}
& V_{S}=R_{S} I_{S}=R_{S} I_{D}=10 \times 0.45=4.5 \mathrm{~V} \\
& V_{D}=V_{D D}-R_{D} I_{D}=12-8 \times 0.45=8.4 \mathrm{~V} \\
& V_{D S}=V_{D}-V_{S}=8.4-4.5=3.9 \mathrm{~V}
\end{aligned}
$$

Considering that the overdrive voltage is $V_{O V}=V_{G S}-V_{t}=7-4.5-1=1.5 \mathrm{~V}$, it follows that $V_{D S}>V_{O V}(3.9>1.5)$, confirming that our initial assumption of a saturated FET was indeed correct.

In the circuit of Fig. $3.34 b$ let $V_{S S}=10 \mathrm{~V}, R_{1}=1.8 \mathrm{M} \Omega, R_{2}=2.2 \mathrm{M} \Omega, R_{D}=$ $10 \mathrm{k} \Omega$, and $R_{S}=7.5 \mathrm{k} \Omega$, and let the FET have $V_{t p}=-0.5 \mathrm{~V}$ and $k_{p}=0.8 \mathrm{~mA} / \mathrm{V}^{2}$. Assuming $\lambda_{p}=0$, find the operating point $Q$.

#### Solution

Assume a saturated FET, and then check whether the assumption is correct. We have

$$
\begin{aligned}
V_{S G} & =V_{S}-V_{G}=\left(V_{D D}-R_{S} I_{S}\right)-\frac{R_{2}}{R_{1}+R_{2}} V_{D D}=\left(10-7.5 I_{S}\right)-5.5 \\
& =4.5-7.5 I_{D}
\end{aligned}
$$

and

$$
I_{D}=\frac{k_{p}}{2}\left(V_{S G}-\left|V_{t p}\right|\right)^{2}=\frac{0.8}{2}\left(4.5-7.5 I_{D}-0.5\right)^{2}
$$

This quadratic equation admits the solutions $I_{D}=0.4 \mathrm{~mA}$ and $I_{D}=0.711 \mathrm{~mA}$ (physically impossible). Consequently, $V_{S}=V_{D D}-R_{S} I_{S}=10-7.5 \times 0.4=$ $7 \mathrm{~V}, V_{D}=R_{D} I_{D}=10 \times 0.4=4 \mathrm{~V}$, and $V_{S D}=V_{S}-V_{D}=7-4=3 \mathrm{~V}$. Considering that the overdrive voltage is $V_{O V}=V_{S G}-\left|V_{t p}\right|=1 \mathrm{~V}$, it follows that $V_{S D}>$ $V_{O V}(3>1)$, thus confirming a saturated FET. The operating point is $Q\left(I_{D}, V_{S D}\right)=$ $Q(0.4 \mathrm{~mA}, 3 \mathrm{~V})$.

EXAMPLE 3.25 In the circuit of Fig. 3.35 specify $R_{1}$ and $R_{2}$ so that $V_{D S n}=4 \mathrm{~V}$ under the constraint that the smaller of $R_{1}$ and $R_{2}$ be $1 \mathrm{M} \Omega$. Show all voltages and currents in your circuit.
image_name:Figure 3.35
description:
[
name: Mp, type: PMOS, ports: {S: VDD, D: dpgn, G: gp}
name: Mn, type: NMOS, ports: {S: sn, D: dn, G: dpgn}
name: R1, type: Resistor, value: R1, ports: {N1: VDD, N2: gp}
name: R2, type: Resistor, value: R2, ports: {N1: gp, N2: GND}
name: R3, type: Resistor, value: 10kΩ, ports: {N1: VDD, N2: dpgn}
name: R4, type: Resistor, value: 7.5kΩ, ports: {N1: dpgn, N2: GND}
name: R5, type: Resistor, value: 10kΩ, ports: {N1: VDD, N2: dn}
name: R6, type: Resistor, value: 2.0kΩ, ports: {N1: GND, N2: sn}
name: VDD, type: VoltageSource, value: 10V, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit consists of a PMOS (Mp) and an NMOS (Mn) transistor. The PMOS is connected between VDD and the node dpgn, with its gate connected to gp. The NMOS is connected between nodes dn and sn, with its gate connected to dpgn. Resistors R1 and R2 form a voltage divider connected to the gate of the PMOS. Resistors R3 and R4 are connected between VDD and GND through the node dpgn. Resistors R5 and R6 are connected in series between VDD and sn through the node dn. The circuit is powered by a 10V source (VDD).

FIGURE 3.35 Circuit of Example 3.25.

#### Solution

Start out at $V_{D S n}$ and work your way back to $R_{1}$ and $R_{2}$, one step at a time. The numerical result of each step is identified by the corresponding step number in Fig. 3.36.

1. By KVL and Ohm's law, $M_{n}$ 's current $I_{D n}$ is such that $V_{D D}=R_{5} I_{D n}+V_{D S n}+$ $R_{6} I_{D n}$, or $10=10 I_{D n}+4+2 I_{D n}$. This gives $I_{D n}=0.5 \mathrm{~mA}$.
2. By Ohm's law, $M_{n}$ 's source voltage is $V_{S n}=R_{6} I_{D n}=2 \times 0.5=1 \mathrm{~V}$.
3. Assume $M_{n}$ is saturated. Then, the overdrive needed to sustain 0.5 mA is $V_{O V n}=\sqrt{2 \times 0.5 / 1}=1 \mathrm{~V}$. This is less than $V_{D S n}(=4 \mathrm{~V})$, so the FET is saturated. We have $V_{G S n}=V_{t n}+V_{O V n}=1+1=2 \mathrm{~V}$.
4. By KVL, $M_{n}$ 's gate voltage is $V_{G n}=V_{S n}+V_{G S n}=1+2=3 \mathrm{~V}$. This is also $M_{p}$ 's drain voltage $V_{D p}$.
5. $M_{p}$ 's drain current is $I_{D p}=V_{D p} / R_{4}=3 / 7.5=0.4 \mathrm{~mA}$.
6. By KVL and Ohm's law, $M_{p}$ 's source voltage is $V_{S p}=V_{D D}-R_{3} I_{D p}=$ $10-10 \times 0.4=6 \mathrm{~V}$.
7. By KVL, $M_{p}$ 's source-drain voltage drop is $V_{S D p}=V_{S p}-V_{D p}=6-3=3 \mathrm{~V}$.
8. Assume $M_{p}$ is saturated. Then, the overdrive needed to sustain 0.4 mA is $V_{O V_{p}}=\sqrt{2 \times 0.4 / 0.2}=2 \mathrm{~V}$. This is less than $V_{S D p}(=3 \mathrm{~V})$, so the FET is saturated. We have $V_{S G p}=\left|V_{t p}\right|+V_{O V_{p}}=1.5+2=3.5 \mathrm{~V}$.
9. By KVL, $M_{p}$ 's gate voltage is $V_{G p}=V_{S p}-V_{S G_{p}}=6-3.5=2.5 \mathrm{~V}$.
10. We note that $R_{2}$ drops 2.5 V and $R_{1}$ drops 7.5 V , so $R_{1}=3 R_{2}$. Use $R_{2}=1 \mathrm{M} \Omega$ and $R_{1}=3 \mathrm{M} \Omega$.
image_name:FIGURE 3.36
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: 9, N2: 10 V}
name: R2, type: Resistor, value: R2, ports: {N1: 9, N2: GND}
name: R3, type: Resistor, value: R3, ports: {N1: 10V, N2: 6}
name: R4, type: Resistor, value: R4, ports: {N1: 4, N2: GND}
name: R5, type: Resistor, value: R5, ports: {N1: 10V, N2: 1}
name: R6, type: Resistor, value: R6, ports: {N1: 2, N2: GND}
name: Mp, type: PMOS, ports: {S: 6, D: 4, G: 9}
name: Mn, type: NMOS, ports: {S: 2, D: 1, G: 3}
]
extrainfo:The circuit is a MOSFET amplifier/switch configuration with PMOS Mp and NMOS Mn transistors. The PMOS is connected with its source to a 6V node, and the NMOS is connected with its source to ground. The gate of the PMOS is controlled by a 2.5V node, while the gate of the NMOS is controlled by a 3V node. Resistors R1 and R2 form a voltage divider that sets the gate voltage for the PMOS. The circuit operates with a supply voltage of 10V.

FIGURE 3.36 Circuit of Fig. 3.35 with each voltage and current identified by the corresponding computational step number in the text.

## 3.6 THE MOSFET AS AN AMPLIFIER/SWITCH

Let us now investigate the two fundamental MOSFET applications, amplification and switching. To this end, refer to the basic circuit of Fig. 3.37, where $R_{D}$ and $M$ can be viewed as forming a voltage divider of sorts: $R_{D}$ tends to pull $v_{O} u p$ toward $V_{D D}$, and $M$ tends to pull $v_{O}$ down toward ground. Depending on which pull action prevails, $v_{O}$ will assume a value somewhere in between. The plot of $v_{O}$ versus $v_{l}$, called the voltage transfer curve (VTC), provides much insight into the capabilities of this
image_name:Fig. 3.37
description:
[
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: RD, type: Resistor, value: 10kΩ, ports: {N1: VDD, N2: VO}
name: Mn, type: NMOS, ports: {S: GND, D: VO, G: VI}
]
extrainfo:The circuit is a basic NMOS amplifier/switch configuration. The voltage source VI controls the gate of the NMOS transistor Mn, allowing it to act as a switch or amplifier. The resistor RD forms a voltage divider with Mn, affecting the output voltage VO. The circuit operates with a supply voltage VDD of +5V.

$$
\mathrm{Mn}: W=10 \mu \mathrm{~m}, L=1 \mu \mathrm{~m}, k^{\prime}=100 \mu \mathrm{~A} / \mathrm{V}^{2}, V_{t}=1.0 \mathrm{~V}, \lambda=0
$$

FIGURE 3.37 PSpice circuit to investigate the MOSFET as an amplifier/switch.
image_name:FIGURE 3.38
description:The graph consists of two plots that illustrate the behavior of a MOSFET circuit as the input voltage \( v_I \) is varied from 0 V to 5 V.

1. **Type of Graph and Function:**
- The top plot is a characteristic curve showing the drain current \( i_D \) in microamperes (\( \mu A \)) as a function of the input voltage \( v_I \) in volts (V).
- The bottom plot is a voltage transfer characteristic (VTC) curve showing the output voltage \( v_O \) in volts (V) as a function of the input voltage \( v_I \).

2. **Axes Labels and Units:**
- **Top Plot:**
- Y-axis: Drain current \( i_D \) (\( \mu A \))
- X-axis: Input voltage \( v_I \) (V)
- **Bottom Plot:**
- Y-axis: Output voltage \( v_O \) (V)
- X-axis: Input voltage \( v_I \) (V)
- Both plots use a linear scale.

3. **Overall Behavior and Trends:**
- **Top Plot:** The drain current \( i_D \) is zero for \( v_I \leq 1.0 \) V, indicating the cutoff region. As \( v_I \) increases past 1.0 V, \( i_D \) rises sharply, indicating the transition to the active region. The current continues to increase but starts to saturate as \( v_I \) approaches 5.0 V.
- **Bottom Plot:** The output voltage \( v_O \) starts at 5.0 V for \( v_I = 0 \) V, indicating the high output voltage \( V_{OH} \). As \( v_I \) increases, \( v_O \) decreases sharply, entering the forward-active (FA) region, and continues to decrease towards the low output voltage \( V_{OL} \) as \( v_I \) approaches 5.0 V.

4. **Key Features and Technical Details:**
- **Top Plot:**
- Cutoff region at \( v_I \leq 1.0 \) V with \( i_D = 0 \).
- Edge of conduction (EOC) marked near \( v_I = 1.0 \) V.
- Drain current saturates around 500 \( \mu A \) as \( v_I \) approaches 5.0 V.
- **Bottom Plot:**
- High output voltage \( V_{OH} \) at \( v_I = 0 \) V.
- Forward-active (FA) region where \( v_O \) decreases sharply.
- Edge of saturation (EOS) marked around \( v_I = 2.0 \) V.
- Triode region as \( v_O \) stabilizes towards \( V_{OL} \).

5. **Annotations and Specific Data Points:**
- **Top Plot:** Annotated points for cutoff and edge of conduction (EOC).
- **Bottom Plot:** Annotated points for \( V_{OH} \), forward-active (FA) region, edge of saturation (EOS), and triode region.
- Critical values include \( V_t = 1.0 \) V for cutoff, \( V_{OH} = 5.0 \) V, and \( V_{OL} \) as \( v_I \) approaches 5.0 V.

FIGURE 3.38 Sweeping the MOSFET of Fig. 3.37 from cutoff (CO), to the edge of conduction (EOC), through the forward-active (FA) region, to the edge of saturation (EOS), into the triode region.
circuit. Figure 3.38 shows the drain current as well as the VTC for the case in which $v_{I}$ is swept from 0 V to 5 V and the FET possesses the characteristics tabulated in Fig. 3.37. We make the following observations:

- For $v_{I} \leq V_{t}\left(V_{t}=1.0 \mathrm{~V}\right)$ the FET is in cutoff (CO). With no current being drawn by the drain, the voltage across $R_{D}$ is 0 V , indicating that $R_{D}$ is pulling $v_{O}$ all the way up to $V_{D D}$. We express this by writing $v_{O}=V_{O H}$, where

$$
\begin{equation*}
V_{O H}=V_{D D}=5 \mathrm{~V} \tag{3.41}
\end{equation*}
$$

- As we raise $v_{I}$ to the value

$$
\begin{equation*}
V_{I(\mathrm{EOC})}=V_{t}=1.0 \mathrm{~V} \tag{3.42}
\end{equation*}
$$

the FET reaches the edge of conduction (EOC) and begins to pull $v_{O}$ down from $V_{D D}$.

- Raising $v_{I}$ further brings the FET into full conduction. As long as $v_{O} \geq V_{O V}$, the FET will be operating in the saturation region, where we can write, for the given device parameter and component values,

$$
\begin{equation*}
v_{O}=V_{D D}-R_{D} I_{D}=5-10 \frac{1}{2}\left(v_{I}-1\right)^{2}=10 v_{I}-5 v_{I}^{2} \tag{3.43}
\end{equation*}
$$

- As $v_{O}$ drops to the value $v_{O}=V_{O V}$, the FET reaches the edge of saturation (EOS), where we have $v_{I}=V_{t}+V_{O V}=1+V_{O V}$. Letting $v_{O}=V_{O V}$ and $v_{I}=1+V_{O V}$ in Eq. (3.43), solving the ensuing quadratic equation, and keeping only the physically acceptable solution, we get $V_{O V}=0.905 \mathrm{~V}$. Denoting the corresponding value of $v_{I}$ as $V_{l(\mathrm{EOS})}$, we have, for the given device and components,

$$
\begin{equation*}
V_{I(\mathrm{EOS})} \cong 1.9 \mathrm{~V} \tag{3.44}
\end{equation*}
$$

- For $v_{I} \geq V_{I(\mathrm{EOS})}, v_{O}$ drops below $V_{O V}$, so the FET enters the triode region, where we now have, for the given device and components,

$$
\begin{align*}
v_{O} & =V_{D D}-R_{D} I_{D}=5-10 \times 1\left[\left(v_{I}-1\right) v_{O}-\frac{1}{2} v_{O}^{2}\right] \\
& =5-10\left(v_{I}-1\right) v_{O}+5 v_{O}^{2} \tag{3.45}
\end{align*}
$$

- For $v_{I}=V_{D D}=5$ V, Eq. (3.45) gives, for the given device and component values, $v_{O}=V_{O L}$, where

$$
\begin{equation*}
V_{O L}=0.124 \mathrm{~V} \tag{3.46}
\end{equation*}
$$

We wish to point out that in order to simplify our calculations and thus facilitate the comparison with simulated data, we have assumed $\lambda=0$ in Fig. 3.37. In practice, a nonzero $\lambda$ will alter the curves a little, but our general observations still stand. The interested reader can easily visualize the differences by running the above PSpice circuit with, say, $\lambda=0.05 \mathrm{~V}^{-1}$.

### The MOSFET as an Amplifier

The slope of the VTC represents voltage gain. Denoted as $a$, it is readily found by differentiating Eq. (3.43). The result is, for the given device and component values,

$$
\begin{equation*}
a=\frac{d v_{O}}{d v_{I}}=10\left(1-v_{I}\right) \tag{3.47}
\end{equation*}
$$

Figure 3.39 shows the VTC as well as the slope $a$. In cutoff and in the triode region $a$ is small or even zero. However, there are two points, denoted as $V_{I L}$ and $V_{I H}$, such that for $V_{I L} \leq v_{I} \leq V_{I H}$ we have $|a|>1 \mathrm{~V} / \mathrm{V}$, indicating that the circuit can be used as an amplifier (if of the inverting type). As seen, the voltage gain peaks at about $-9 \mathrm{~V} / \mathrm{V}$ just before the EOS.

A circuit whose gain is not constant but varies with the value of the signal itself is nonlinear. Moreover, the VTC does not go through the origin, but is offset both along the $v_{I}$ and the $v_{O}$ axes. How can we make such a circuit work as a voltage amplifier? The answer relies on two premises, which are illustrated in Fig. 3.40:

- First, we bias the FET at a suitable operating point $Q_{0}=Q_{0}\left(V_{l}, V_{o}\right)$ in the FA region by applying the appropriate dc voltage $V_{I}$. Aptly called the quiescent operating point, $Q_{0}$ in effect establishes a new system of axes for signal variations about this point. $Q_{0}$ should be located sufficiently away from either extreme (EOC and EOS) to allow for an adequate output signal swing in both directions.
image_name:FIGURE 3.39 The voltage transfer curve (VTC) and its slope, representing the voltage gain a.
description:The provided graph is a voltage transfer curve (VTC) for a field-effect transistor (FET), illustrating the relationship between the input voltage \( v_I \) and the output voltage \( v_o \). It also includes a graph of the voltage gain \( a \) as a function of the input voltage \( v_I \).

Top Graph: Voltage Transfer Curve (VTC)
1. **Type of Graph:**
- The top graph is a voltage transfer curve, showing how the output voltage \( v_o \) varies with the input voltage \( v_I \).

2. **Axes Labels and Units:**
- The horizontal axis represents the input voltage \( v_I \) in volts, ranging from 0 to 5 volts.
- The vertical axis represents the output voltage \( v_o \) in volts, ranging from 0 to 5 volts.

3. **Overall Behavior and Trends:**
- The curve starts at a high output voltage of approximately 5 volts when the input voltage is low, indicating a region called "Cutoff."
- As the input voltage increases, the output voltage sharply decreases, indicating a transition region.
- After this transition, the curve flattens out, representing the "Triode" region where the output voltage remains relatively constant despite changes in input voltage.

4. **Key Features and Technical Details:**
- The transition between the "Cutoff" and "Triode" regions occurs between the input voltages \( V_{IL} \) and \( V_{IH} \), which are critical points for defining the operating regions.
- The slope \( a \) of the VTC in the transition region represents the voltage gain.

5. **Annotations and Specific Data Points:**
- The graph is annotated with the terms "Cutoff" and "Triode" to indicate different operating regions of the FET.
- The critical input voltages \( V_{IL} \) and \( V_{IH} \) are marked on the horizontal axis.

Bottom Graph: Voltage Gain \( a \)
1. **Type of Graph:**
- The bottom graph shows the voltage gain \( a \) as a function of the input voltage \( v_I \).

2. **Axes Labels and Units:**
- The horizontal axis represents the input voltage \( v_I \) in volts, ranging from 0 to 5 volts.
- The vertical axis represents the voltage gain \( a \) in volts per volt (V/V), ranging from -10 to 1.

3. **Overall Behavior and Trends:**
- The gain is initially close to zero when the input voltage is low.
- There is a sharp dip in gain to approximately -9 V/V as the input voltage approaches \( V_{IL} \), indicating a high sensitivity to changes in input voltage in this region.
- The gain then recovers and approaches zero again as the input voltage increases beyond \( V_{IH} \).

4. **Key Features and Technical Details:**
- The minimum gain occurs between \( V_{IL} \) and \( V_{IH} \), corresponding to the steepest part of the VTC.

5. **Annotations and Specific Data Points:**
- The points \( V_{IL} \) and \( V_{IH} \) are marked, corresponding to critical points where significant changes in gain occur.

FIGURE 3.39 The voltage transfer curve (VTC) and its slope, representing the voltage gain a.

- Then, we apply an ac input $v_{i}$, which will cause the instantaneous operating point to move up and down the VTC (between $Q_{1}$ and $Q_{2}$ ), to yield a magnified ac voltage $v_{o}$ at the output.

In our discussion we are relying on the same notation that proved so convenient in the study of diodes, namely, we express the input and output voltages as

$$
\begin{align*}
& v_{I}=V_{I}+v_{i}  \tag{3.48a}\\
& v_{O}=V_{O}+v_{o} \tag{3.48b}
\end{align*}
$$

where:

- $v_{I}$ and $v_{O}$ are referred to as the total signals (lower-case symbols with upper-case subscripts)
- $V_{I}$ and $V_{o}$ are their dc components (upper-case symbols with upper-case subscripts)
- $v_{i}$ and $v_{o}$ are their ac components (lower-case symbols with lower-case subscripts)

As depicted in Fig. 3.40b for the circuit of Fig. 3.37, the bias point $Q_{0}$ has been chosen half-way between the value of $v_{O}$ corresponding to the EOC and that corresponding to the EOS, or $V_{o}=(5+0.905) / 2 \cong 3 \mathrm{~V}$. The voltage gain there is denoted as $a\left(Q_{0}\right)$.
image_name:(a)
description:
[
name: M, type: NMOS, ports: {S: GND, D: Vo, G: Vi}
name: RD, type: Resistor, value: RD, ports: {N1: Vo, N2: VDD}
name: V1, type: VoltageSource, value: V1, ports: {Np: Vi, Nn: GND}
]
extrainfo:The circuit is a MOSFET voltage amplifier with an NMOS transistor. The drain of the NMOS is connected to a resistor RD and VDD, while the source is connected to ground. The gate is driven by a voltage source V1. The output is taken from the drain node Vo.
image_name:(b)
description:The graph depicted in Figure 3.40(b) is a plot representing the relationship between the input voltage $v_I$ and the output voltage $v_O$ for a MOSFET used as a voltage amplifier. The graph is a voltage transfer characteristic curve.

1. **Type of Graph and Function:**
- This is a voltage transfer characteristic graph showing the output voltage $v_O$ as a function of the input voltage $v_I$.

2. **Axes Labels and Units:**
- The horizontal axis represents the input voltage $v_I$ in volts (V), ranging from 0 to 3 volts.
- The vertical axis represents the output voltage $v_O$ in volts (V), ranging from 0 to 5 volts.

3. **Overall Behavior and Trends:**
- The graph shows a nonlinear relationship between $v_I$ and $v_O$, with a distinct region of linearity around the operating point $Q_0$.
- As the input voltage $v_I$ increases from 0 V, the output voltage $v_O$ initially remains high and constant at around 5 V, indicating the saturation region.
- As $v_I$ approaches the threshold, the output $v_O$ begins to decrease sharply, indicating the transition from saturation to the active region.
- Beyond the linear region, as $v_I$ continues to increase, the output voltage $v_O$ decreases further and eventually levels off, approaching 0 V, indicating the cutoff region.

4. **Key Features and Technical Details:**
- The bias point $Q_0$ is marked on the graph at $v_I = 1.632$ V and $v_O = 3$ V, which is the midpoint of the linear region.
- The slope at $Q_0$ represents the voltage gain $a(Q_0)$ which is approximately -6.324 V/V.
- Points $Q_1$ and $Q_2$ are also marked, indicating the endpoints of the linear region.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for the bias point $Q_0$ and the corresponding voltage gain $a$.
- Reference lines are drawn to show the operating point and the linear region, emphasizing the steep slope that indicates high gain.

This graph is crucial for understanding the amplification characteristics of the MOSFET in the given circuit, particularly how it operates around the bias point $Q_0$ with a significant voltage gain.

FIGURE 3.40 (a) The MOSFET of Fig. 3.37 as a voltage amplifier, and (b) variations about the operating point $Q_{0}$.

#### Exercise 3.2

Find the value of $V_{I}$ needed to bias the drain at $V_{O}=3.0 \mathrm{~V}$ in the circuit of Fig. 3.37.
What is the corresponding voltage gain $a$ there?
Ans. $V_{I}=1.632 \mathrm{~V}, a\left(Q_{0}\right)=-6.324 \mathrm{~V} / \mathrm{V}$.

PSpice simulations with a triangular input $v_{i}$ of progressively increasing magnitude give the waveforms of Fig. 3.41, where we make the following observations:

- In Fig. $3.41 a$ the ac input $v_{i}$ has peak values of $\pm 100 \mathrm{mV}$ and the ac output $v_{o}$ is an inverted and magnified version of $v_{i}$. The slight distortion exhibited by $v_{o}$ is due to the quadratic (rather than linear) active-region VTC.
image_name:(a)
description:The graph in Fig. 3.41(a) is a time-domain waveform depicting the response of a circuit to a triangular input voltage. The horizontal axis represents time in milliseconds (ms), ranging from 0 to 2 ms. The vertical axis represents voltage in volts (V), with a scale from 0 to 5 V.

**Type of Graph and Function:**
- The graph shows two waveforms: the input voltage \(v_i\) and the output voltage \(v_o\).
- The input \(v_i\) is a triangular waveform with peak values of \(\pm 100 \text{ mV}\).

**Axes Labels and Units:**
- The x-axis is labeled 'Time \(t\)' with units in milliseconds (ms).
- The y-axis is labeled 'Waveforms (V)' with units in volts (V).
- The graph uses a linear scale for both axes.

**Overall Behavior and Trends:**
- The input waveform \(v_i\) is a small amplitude triangular wave centered around 0 V.
- The output waveform \(v_o\) is an inverted and magnified version of \(v_i\), indicating amplification and phase inversion.
- The output waveform shows slight distortion, deviating from a perfect triangular shape due to the quadratic characteristics of the active-region voltage transfer characteristic (VTC).

**Key Features and Technical Details:**
- The output waveform \(v_o\) has a larger amplitude than the input, indicating a gain in the circuit.
- There is a noticeable inversion of the waveform as the peaks of \(v_o\) correspond to the troughs of \(v_i\) and vice versa.
- The distortion in \(v_o\) suggests the non-linear behavior of the circuit, especially at higher amplitudes.

**Annotations and Specific Data Points:**
- The graph includes annotations indicating \(v_o\) and \(v_i\) for clarity.
- The peak values of \(v_i\) are \(\pm 100 \text{ mV}\), while \(v_o\) reaches up to approximately 5 V, showing significant amplification.
image_name:(b)
description:The graph labeled as (b) in Figure 3.41 illustrates the time-domain waveforms of an input and output signal for a given circuit. The x-axis represents time in milliseconds (ms), ranging from 0 to 2 ms. The y-axis represents voltage in volts (V), ranging from 0 to 5 V.

In this graph, the input voltage $v_I$ is a triangular waveform with peak values of ±250 mV. This waveform is shown as a thin line oscillating around a baseline, indicating a small amplitude relative to the output.

The output voltage $v_O$ is also a waveform, but it is significantly more distorted compared to the input. It is an inverted and magnified version of the input waveform, with its peaks reaching close to 5 V and valleys approaching 0 V. This distortion is due to the nonlinear voltage transfer characteristics (VTC) of the circuit, which becomes more pronounced as the input amplitude increases.

The output waveform exhibits a clear inversion, meaning that where the input waveform has a peak, the output has a valley, and vice versa. The distortion is evident as the waveform does not maintain the perfect triangular shape of the input, instead showing rounded peaks and valleys.

Overall, the graph demonstrates how the circuit responds to a triangular input waveform with moderate amplitude, highlighting the nonlinear distortion effects present in the output waveform due to the circuit's characteristics.
image_name:(c)
description:The graph in Fig. 3.41(c) is a time-domain waveform plot depicting the response of a circuit to a triangular input voltage, denoted as \( v_{i} \), with peak values of \( \pm 750 \mathrm{mV} \). The graph displays two waveforms: the input voltage \( v_{i} \) and the output voltage \( v_{o} \).

1. **Axes Labels and Units:**
- The horizontal axis represents time, \( t \), measured in milliseconds (ms), ranging from 0 to 2 ms.
- The vertical axis represents voltage, \( V \), measured in volts (V), with a range from 0 to 5 V.

2. **Overall Behavior and Trends:**
- The input waveform \( v_{i} \) is a triangular wave with smaller amplitude compared to the output. It maintains a consistent triangular shape throughout the observed period.
- The output waveform \( v_{o} \) is significantly distorted compared to the input, exhibiting a nonlinear response. The waveform is inverted and magnified, indicating a phase inversion and gain in the circuit.
- The distortion in \( v_{o} \) becomes more pronounced due to the larger peak values of the input, causing the operating point to traverse a wider portion of the nonlinear voltage transfer characteristic (VTC).

3. **Key Features and Technical Details:**
- The output waveform \( v_{o} \) shows clear peaks and valleys, with the peaks reaching close to the maximum voltage of 5 V and valleys approaching 0 V.
- The waveform is periodic, with a period matching that of the input waveform, indicating that the frequency of the output is consistent with the input.

4. **Annotations and Specific Data Points:**
- The graph includes annotations for \( v_{i} \) and \( v_{o} \), clearly marking the respective waveforms.
- The peak distortion in \( v_{o} \) is a critical observation, highlighting the nonlinear behavior of the circuit under large input conditions.

FIGURE 3.41 The responses of the circuit of Fig. 3.37 to a triangular wave $v_{i}$ with peak values of: (a) $\pm 100 \mathrm{mV}$, (b) $\pm 250 \mathrm{mV}$, and (c) $\pm 750 \mathrm{mV}$. The FET is biased at $V_{l}=1.63 \mathrm{~V}$.

- Raising $v_{i}$ 's peak values to $\pm 250 \mathrm{mV}$ as in Fig. $3.41 b$ yields a far more distorted waveform for $v_{o}$, as the operating point is now moving up and down a wider portion of the nonlinear VTC.
- With $v_{i}$ 's peak values as large as $\pm 750 \mathrm{mV}$ as in Fig. $3.41 c$, the operating point not only sweeps the entire active-region VTC, but it also spills over into the cutoff and the triode regions. Consequently, beside higher distortion, $v_{o}$ now exhibits also clipping at the top due to cutoff, and compression at the bottom due to nonlinear triode behavior.

We now better appreciate the reason for biasing the FET somewhere in the middle of its active region, sufficiently away from both cutoff and triode behavior, as well as the reason for keeping the magnitude of $v_{i}$ and, hence, of $v_{o}$, sufficiently small. In fact, the smaller the signals the lesser the amount of output distortion. Indeed, if we keep the ac signal magnitudes sufficiently small to allow for the substitutions $d v_{I} \rightarrow v_{i}$ and $d v_{o} \rightarrow v_{o}$ in Eq. (3.47), then we can approximate $a=v_{o} / v_{i}$, or

$$
\begin{equation*}
v_{o}=a\left(Q_{0}\right) \times v_{i} \tag{3.49}
\end{equation*}
$$

where $a\left(Q_{0}\right)$ is the gain at the operating point $Q_{0}$. Viewed in this light, $v_{i}$ and $v_{o}$ are also referred to as small signals. A more rigorous treatment of this subject will be undertaken in the next section.

#### ExAMPLE 3.26

With reference to Fig. 3.41a, investigate the ac output $v_{o}$ using both exact analysis via Eq. (3.43), and approximate analysis via Eq. (3.49), and compare the two cases.

#### Solution

For $v_{I}=V_{I}+v_{i}=1.632+0$ V, Eq. (3.43) yields $v_{O}=V_{O}+v_{o}=3.003+0=$ 3.003 V , and the circuit is operating at $Q_{0}$ (see Fig. $3.40 b$ ), where the gain is $a=-6.324 \mathrm{~V} / \mathrm{V}$.

For $v_{I}=V_{I}+v_{i}=1.632 \mathrm{~V}+100 \mathrm{mV}=1.732 \mathrm{~V}$, Eq. (3.43) yields $v_{O}=$ 2.321 V , and the circuit is now operating at $Q_{1}$ (see again Fig. 3.40b). Expressing as $v_{O}=V_{O}+v_{o}$, or $2.321=3.003+v_{o}$, gives $v_{o}=2.321-3.003=-682 \mathrm{mV}$. This represents the actual negative peak value of $v_{o}$. By Eq. (3.49), the approximate peak value is $-6.324 \times 100=-632 \mathrm{mV}$, indicating a $7.3 \%$ underestimate. This stems from the fact that the actual gain magnitude between $Q_{0}$ and $Q_{1}$ is more than $6.324 \mathrm{~V} / \mathrm{V}$.

For $v_{I}=V_{I}-v_{i}=1.632 \mathrm{~V}-100 \mathrm{mV}=1.532 \mathrm{~V}$, Eq. (3.43) yields $v_{O}=3.585 \mathrm{~V}$, and the circuit is now operating at $Q_{2}$ (see again Fig. 3.40b). Expressing again as $v_{O}=V_{O}+v_{o}$ gives $v_{o}=3.585-3.003=+582 \mathrm{mV}$. This represents the actual positive peak value of $v_{o}$. By Eq. (3.49), the approximate peak value is $-6.324 \times(-100)=+632 \mathrm{mV}$, indicating an $8.6 \%$ overestimate. This stems from the fact that the actual gain magnitude between $Q_{0}$ and $Q_{2}$ is less than $6.324 \mathrm{~V} / \mathrm{V}$.
image_name:(a)
description:
[
name: VI, type: VoltageSource, ports: {Np: VI, Nn: GND}
name: VDD, type: VoltageSource, ports: {Np: VDD, Nn: GND}
name: M1, type: NMOS, ports: {S: s1, D: d1, G: VI}
name: RL, type: Resistor, ports: {N1: VDD, N2: d1}
]
extrainfo:The circuit operates the NMOS transistor M1 as a switch. When VI is low, M1 is in cutoff and acts as an open switch. When VI is high, M1 conducts, closing the switch and allowing current to flow from VDD through RL to ground.
image_name:(b)
description:
[
name: R_L, type: Resistor, value: R_L, ports: {N1: V_DD, N2: s1}
name: V_DD, type: VoltageSource, value: V_DD, ports: {Np: V_DD, Nn: GND}
name: S1, type: Switch, ports: {N1: s1, N2: GND}
]
extrainfo:The circuit diagram (b) shows an NMOS transistor M1 acting as a switch. When the input voltage V_I is low, the switch S1 is open, and when V_I is high, the switch closes, connecting R_L to GND through r_DS.
image_name:(c)
description:
[
name: RL, type: Resistor, value: RL, ports: {N1: VDD, N2: d1}
name: VDD, type: VoltageSource, value: VDD, ports: {Np: VDD, Nn: GND}
name: SW, type: Switch, ports: {N1: s1, N2: d1}
name: r_DS, type: Resistor, value: r_DS, ports: {N1: s1, N2: GND}
]
extrainfo:The circuit diagram (c) shows an NMOS transistor M1 acting as a switch. When the input voltage VI is high, the switch is closed (represented by r_DS), connecting VDD to GND through RL. When VI is low, the switch is open.

FIGURE 3.42 Operating the MOSFET as an electronic switch.

### The MOSFET as an Electronic Switch

When FET operation alternates between the cutoff and the ohmic regions, the device acts as an electronically controlled switch $S W$. This function is illustrated in Fig. 3.42, where we observe the following:

- When the input voltage level in the circuit of Fig. $3.42 a$ is low, such as near 0 V , the FET is in cutoff, and since it draws no current, it can be regarded as an open switch, as pictured in Fig. 3.42b.
- When the input voltage level is high, such as near $V_{D D}$, or 5 V , the FET is in the ohmic region, and acts like a closed switch with a resistance $r_{D S}$ as pictured in Fig. 3.42c. In a well designed circuit $r_{D S} \ll R_{L}$. With $v_{I}=V_{D D}=5 \mathrm{~V}$ the circuit of Fig. 3.37 gives, by Eq. (3.17), $r_{D S}=1 /(5-1)=250 \Omega$.

### The MOSFET as a Logic Inverter

One of the most important applications of the FET switch is logic inversion in computer circuitry. As depicted in Fig. 3.43a, a logic inverter outputs a high level $V_{O H}$ in response to a low input level ( $v_{I} \cong 0 \mathrm{~V}$ ), and a low level $V_{O L}$ in response to a high input level $\left(v_{I} \cong 5 \mathrm{~V}\right)$. As already mentioned, with the component values of Fig. 3.37,
image_name:(a)
description:
[
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: VO}
name: M, type: NMOS, ports: {S: GND, D: VO, G: VI}
]
extrainfo:The circuit is a MOSFET logic inverter. It outputs a high level (VOH = 5 V) when the input is low (VI ≈ 0 V) and a low level (VOL = 0.12 V) when the input is high (VI ≈ 5 V). The voltage transfer characteristic (VTC) shows the transition region where the inverter switches states.
image_name:(b)
description:The graph in Figure 3.43(b) is a Voltage Transfer Characteristic (VTC) plot for a MOSFET logic inverter. It is a curve that represents the relationship between the input voltage \( v_I \) and the output voltage \( v_O \) of the inverter.

1. **Type of Graph and Function:**
- This is a VTC graph, which is used to analyze the behavior of digital logic inverters.

2. **Axes Labels and Units:**
- The x-axis is labeled as 'Input \( v_I \) (V)' and ranges from 0 to 5 volts.
- The y-axis is labeled as 'Output \( v_O \) (V)' and also ranges from 0 to 5 volts.
- Both axes use a linear scale.

3. **Overall Behavior and Trends:**
- The graph shows a steep transition region where the output voltage drops sharply as the input voltage increases.
- For low input voltages (close to 0 V), the output voltage is high at approximately 5 V (\( V_{OH} \)).
- As the input voltage increases to around 2.5 V, the output voltage rapidly decreases.
- For high input voltages (close to 5 V), the output voltage stabilizes at a low value of approximately 0.12 V (\( V_{OL} \)).

4. **Key Features and Technical Details:**
- The transition region is marked where the slope of the curve \(|a| > 1 \text{ V/V}\), indicating a high gain region where the inverter is switching states.
- The curve is steepest between the input voltages \( V_{IL} \) and \( V_{IH} \), which are the input low and high thresholds, respectively.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for \( V_{OH} \) and \( V_{OL} \), representing the high and low output voltage levels.
- The transition region is clearly marked, emphasizing the rapid change in output voltage with respect to input voltage.

This VTC plot effectively illustrates the behavior of the MOSFET as a logic inverter, showing how it inverts the input signal from high to low and vice versa, with a sharp transition between these states.

FIGURE 3.43 (a) The MOSFET of Fig. 3.37 as a logic inverter, and (b) the relevant portions of its VTC.
we have $V_{O H}=5 \mathrm{~V}$ and $V_{O L}=0.12 \mathrm{~V}$. Figure $3.43 b$ shows the two portions of the VTC intended for logic-inverter operation. Of course, as the inverter switches from one state to the other, its operating point will momentarily travel through the intermediate portion of the VTC, but in high-speed logic circuits such as those in use nowadays, an inverter will dwell within this region only briefly, typically for few nanoseconds or less ( $1 \mathrm{~ns}=10^{-9} \mathrm{~s}$ ).

A logic inverter must function reliably even in the presence of disturbances, collectively referred to as noise. Should a disturbance appear at its input, the inverter must suppress it, or at least attenuate it, to avoid passing it on to subsequent circuits in magnified and thus in potentially even more detrimental form. Consequently, the transition region, where gain magnitude is greater than unity, represents a forbidden region of operation of an inverter. Its extremes, where gain is $-1 \mathrm{~V} / \mathrm{V}$, are readily visualized with the help of Fig. 3.38, bottom. The values of $v_{I}$ at these extremes are denoted as $V_{I L}$ and $V_{I H}$.

To find $V_{I L}$, impose $-1=10\left(1-V_{I L}\right)$ in Eq. (3.47). This gives

$$
\begin{equation*}
V_{I L}=1.1 \mathrm{~V} \tag{3.50a}
\end{equation*}
$$

To find $V_{I H}$, we differentiate both sides of Eq. (3.45) with respect to $v_{I}$

$$
\frac{d v_{O}}{d v_{I}}=-10\left[v_{O}+\left(v_{I}-1\right) \frac{d v_{O}}{d v_{I}}-v_{O} \frac{d v_{O}}{d v_{I}}\right]
$$

Imposing $d v_{O} / d v_{I}=-1$ yields a relationship between $v_{O}$ and $v_{I}$ right at the point of negative unity slope,

$$
v_{O}=0.5 v_{I}-0.45
$$

Substituting back into Eq. (3.45), solving the resulting quadratic equation in $v_{l}$, and retaining only the physically acceptable solution, which is obviously $V_{I H}$, we finally get

$$
\begin{equation*}
V_{I H}=2.055 \mathrm{~V} \tag{3.50b}
\end{equation*}
$$

To better appreciate the inverter's ability to reject noise, we run a PSpice simulation of the circuit of Fig. 3.37 for the case in which the input levels are contaminated by noise spikes, as exemplified in the plot of $v_{I}$ of Fig. 3.44, top. In practice such spikes may arise from ground and power-supply interference, unwanted electric/ magnetic coupling between adjacent circuits, and other causes that are beyond our scope here. When the inverter's input is low we need to worry about positivegoing spikes, whereas when the input is high we need to worry about negative-going spikes, as both spike types tend to drive the operating point toward the forbidden region of the VTC, where they are magnified. Looking at the plot of $v_{O}$ of Fig. 3.44, bottom, we state the following:

- The input spikes $v_{i 1}$ and $v_{i 2}$ have no or little effect upon the output, as their peak values are below $V_{I L}$. Likewise, $v_{i 4}$ and $v_{i 5}$ have little effect upon the output because their peak values are above $V_{I H}$.
- The peak value of $v_{i 3}$ is above $V_{I L}$, indicating that its upper portion will be amplified to produce the output spike $v_{o 3}$. This is undesirable, as we want the inverter to either suppress or attenuate its input spikes, not to amplify them!
image_name:FIGURE 3.44
description:The graph labeled "FIGURE 3.44" consists of two plots showing the behavior of a logic inverter in the presence of noise. The horizontal axis on both plots represents time in microseconds (μs), ranging from 0 to 6 μs. The vertical axis of the top plot represents the input voltage $v_i$ in volts (V), ranging from 0 to 5 V, while the vertical axis of the bottom plot represents the output voltage $v_o$, also in volts (V), ranging from 0 to 5 V.

Top Plot: Input Voltage ($v_i$)
- **Axes and Labels**: The vertical axis is labeled "Input $v_i$ (V)" and the horizontal axis "Time (μs)".
- **Noise Margins**: There are two significant horizontal lines at $V_{IL}$ and $V_{IH}$, marking the lower and upper noise margins, respectively. The area between these lines is shaded, indicating a transition region or forbidden region where noise can be magnified.
- **Behavior and Trends**: The input voltage exhibits several spikes labeled $v_{i1}$ to $v_{i6}$.
- $v_{i1}$ and $v_{i2}$ have peak values below $V_{IL}$, indicating minimal effect on the output.
- $v_{i3}$ peaks above $V_{IL}$ but below $V_{IH}$, suggesting it will be amplified, which is undesirable.
- $v_{i4}$, $v_{i5}$, and $v_{i6}$ have peak values above $V_{IH}$, indicating little effect on the output.

Bottom Plot: Output Voltage ($v_o$)
- **Axes and Labels**: The vertical axis is labeled "Output $v_o$ (V)" and the horizontal axis "Time (μs)".
- **Noise Margins**: Similar to the input plot, the noise margins $V_{OL}$ and $V_{OH}$ are marked, with the shaded transition region between $V_{IL}$ and $V_{IH}$.
- **Behavior and Trends**: The output voltage shows corresponding spikes labeled $v_{o1}$ to $v_{o6}$.
- $v_{o1}$ and $v_{o2}$ remain stable with minimal disturbance.
- $v_{o3}$ corresponds to $v_{i3}$ and shows amplification, peaking significantly, which is undesirable.
- $v_{o4}$ and $v_{o5}$ show minimal output spikes.
- $v_{o6}$ corresponds to $v_{i6}$ and shows some amplification.

Key Observations:
- The shaded region in both plots represents the forbidden region where the inverter's behavior is undesirable due to noise amplification.
- The noise margins $NM_L$ and $NM_H$ are crucial for determining the inverter's robustness against noise.
- The graph illustrates the inverter's inability to suppress certain input spikes, leading to amplified output spikes, which is not ideal for logic operations.

FIGURE 3.44 Logic-inverter behavior in the presence of noise, showing the noise margins $N M_{L}$ and $N M_{H}$ (the shaded area represents the transition or forbidden region, where noise gets magnified).

- The peak value of $v_{i 6}$ is below $V_{I H}$, indicating that its lower portion will be amplified to produce the output spike $v_{o 6}$. Again, this is undesirable.
An inverter's ability to function properly in spite of input disturbances is quantified in terms of its noise margins, defined as

$$
\begin{align*}
& N M_{L}=V_{I L}-V_{O L}  \tag{3.51a}\\
& N M_{H}=V_{O H}-V_{I H} \tag{3.51b}
\end{align*}
$$

As visualized in the plot of $v_{I}$ of Fig. 3.44, $N M_{L}$ represents the maximum tolerable noise at the input in the low state. In our example, $N M_{L}=1.1-0.124=0.98 \mathrm{~V}$, indicating that positive-going input spikes of magnitudes not exceeding 0.98 V will be either suppressed or attenuated. Likewise, $N M_{H}$ represents the maximum tolerable noise at the input in the high state. In our example, $N M_{H}=5-2.055=2.95 \mathrm{~V}$, indicating our circuit's ability to attenuate negative-going input spikes of magnitudes not exceeding 2.95 V . The circuit of our particular example tolerates noise more easily in the high than in the low input state. Using a FET with a higher value of $V_{t}$, such as $V_{t}=2 \mathrm{~V}$, will shift the VTC toward the right, thus increasing $N M_{L}$, if at the expense of a decrease in $N M_{H}$, and resulting in more balanced noise margins.

## 3.7 SMALL-SIGNAL OPERATION OF THE MOSFET

We now wish to pursue a more systematic investigation of the small-signal operation introduced in the previous section. Let us start with the circuit of Fig. 3.45a, where we are using the dc source $V_{G S}$ to bias the FET at some quiescent point $Q_{0}=$ $Q_{0}\left(I_{D}, V_{G S}\right)$ up the quadratic curve (see Fig. $3.46 a$ ), and the source $V_{D D}$, along with the resistance $R_{D}$, to bias the BJT at the corresponding operating point $Q_{0}=Q_{0}\left(I_{D}, V_{D S}\right)$ in the active region (see Fig. 3.46b). Applying Eq. (3.21) at $Q_{0}$ gives

$$
\begin{equation*}
I_{D}=\frac{k}{2}\left(V_{G S}-V_{t}\right)^{2}\left(1+\lambda V_{D S}\right) \tag{3.52}
\end{equation*}
$$

Along with the $i_{D}-v_{G S}$ curves of the FET, Fig. $3.46 b$ shows also the curve of the external circuit seen by the drain, a curve known as the load line,

$$
i_{D}=\frac{V_{D D}-v_{D S}}{R_{D}}
$$

The quiescent point $Q_{0}=Q_{0}\left(I_{D}, V_{D S}\right)$ lies right where the FET curve corresponding to the given value of $V_{G S}$ intersects the load line.

If we now turn on the ac source $v_{g s}$ as in Fig. 3.45b, the operating point will move up and down the quadratic curve of Fig. 3.46a, as well as up and down the load line of Fig. 3.46b . In Fig. 3.46 we have captured a positive alternation of $v_{g s}$, during which the instantaneous operating point in Fig. 3.46a is $Q_{1}=Q_{1}\left(I_{D}+i_{d}, V_{G S}+v_{g s}\right)$, and in Fig. $3.46 b$ is $Q_{1}=Q_{1}\left(I_{D}+i_{d}, V_{D S}+v_{d s}\right)$. We wish to find a relationship between the ac current $i_{d}$ and the ac voltages $v_{g s}$ and $v_{d s}$. Applying Eq. (3.21) at $Q_{1}$ gives

$$
I_{D}+i_{d}=\frac{k}{2}\left[V_{G S}+v_{g s}-V_{t}\right]^{2}\left[1+\lambda\left(V_{D S}+v_{d s}\right)\right]
$$

Regrouping and multiplying out gives

$$
\begin{equation*}
I_{D}+i_{d}=\frac{k}{2}\left[\left(V_{G S}-V_{t}\right)^{2}+2\left(V_{G S}-V_{t}\right) v_{g s}+v_{g s}^{2}\right]\left[\left(1+\lambda V_{D S}\right)+\lambda v_{d s}\right] \tag{3.53}
\end{equation*}
$$

image_name:(a)
description:
[
name: M, type: NMOS, ports: {S: GND, D: VDS, G: VGS}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: VDS}
name: VGS, type: VoltageSource, value: VGS, ports: {Np: VGS, Nn: GND}
]
extrainfo:The circuit is a large-signal or DC version of a MOSFET amplifier. It uses an NMOS transistor with a resistor RD connected to VDD, forming a common-source amplifier configuration with VGS as the input voltage.
image_name:(b)
description:
[
name: M, type: NMOS, ports: {S: GND, D: VDS, G: VGS}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: VDS}
name: VGS, type: VoltageSource, ports: {Np: X1, Nn: GND}
name: VDD, type: VoltageSource, ports: {Np: VDD, Nn: GND}
name: vgs, type: VoltageSource, ports: {Np: VGS, Nn: X1}
]
extrainfo:The circuit is a small-signal model of an NMOS amplifier with the drain connected to VDD through a resistor RD. The gate is driven by a combination of DC and AC sources, VGS and vgs, with the source connected to ground. The current source X1 represents the AC component of the gate voltage.
image_name:(c)
description:
[
name: M, type: NMOS, ports: {S: GND, D: Vds, G: Vgs}
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: Vds}
name: VGS, type: VoltageSource, value: VGS, ports: {Np: Vgs, Nn: GND}
]
extrainfo:The circuit is a small-signal amplifier using an NMOS transistor. It includes a resistor RD connected between VDD and the drain of the NMOS. The gate is driven by a combination of DC and AC voltage sources (VGS and vgs). The output is taken from the drain, labeled as Vds.

FIGURE 3.45 Systematic analysis of the MOSFET as a small-signal amplifier. The actual circuit is shown in (b), while (a) shows its large-signal or dc version, and (c) shows its small-signal or ac version.
image_name:(a)
description:The graph labeled (a) is a plot of the drain current \(i_D\) versus the gate-source voltage \(v_{GS}\) for an NMOS transistor operating as a small-signal amplifier. This is a characteristic curve that illustrates the relationship between these two parameters.

1. **Type of Graph and Function:**
- The graph is a characteristic curve showing the relationship between gate-source voltage and drain current for an NMOS transistor.

2. **Axes Labels and Units:**
- The x-axis is labeled "Gate-source voltage \(v_{GS}\)" and represents the voltage applied between the gate and source terminals of the transistor.
- The y-axis is labeled "Drain current \(i_D\)" and represents the current flowing through the drain of the transistor.
- Both axes likely use linear scales, although specific units are not provided in the graph.

3. **Overall Behavior and Trends:**
- The graph shows a non-linear relationship where the drain current \(i_D\) initially increases slowly with increasing \(v_{GS}\), followed by a more rapid increase. This indicates the transistor's threshold behavior and its transition into the saturation region.
- The curve is smooth and upward-sloping, indicating increasing current with increasing voltage.

4. **Key Features and Technical Details:**
- The graph highlights two key operating points, \(Q_0\) and \(Q_1\), which represent the quiescent point and a point with an additional small signal, respectively.
- The slope at \(Q_0\) is marked as \(g_m\), the transconductance, which is the derivative of \(i_D\) with respect to \(v_{GS}\) at the quiescent point.
- The operating points \(V_{GS}\) and \(V_{GS} + v_{gs}\) are marked on the x-axis, indicating the DC and small-signal components of the gate-source voltage.
- The corresponding drain currents \(I_D\) and \(I_D + i_d\) are marked on the y-axis.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for \(Q_0\) and \(Q_1\), showing the transition from the quiescent operating point to a point with a small-signal variation.
- The quiescent point \(Q_0\) is where \(V_{GS}\) results in a steady-state drain current \(I_D\), while \(Q_1\) includes the small-signal variation \(v_{gs}\), resulting in \(I_D + i_d\).
image_name:(b)
description:The graph labeled (b) is a characteristic curve of an NMOS transistor used as a small-signal amplifier, depicting the relationship between the drain current \( i_D \) and the drain-source voltage \( v_{DS} \). This is a typical output characteristic graph for a MOSFET.

Axes Labels and Units:
- **X-axis:** Drain-source voltage \( v_{DS} \), with units typically in volts (V).
- **Y-axis:** Drain current \( i_D \), with units typically in amperes (A).

Overall Behavior and Trends:
- The graph shows several curves representing different gate-source voltages \( V_{GS} \). These curves illustrate how \( i_D \) varies with \( v_{DS} \) for different \( V_{GS} \) values.
- The curves are generally increasing, indicating that as the drain-source voltage \( v_{DS} \) increases, the drain current \( i_D \) also increases.
- There is a load line drawn across the graph, which intersects the transistor curves. This line represents the constraints imposed by the external circuit, specifically the resistor \( R_D \) connected between \( V_{DD} \) and the drain.

Key Features and Technical Details:
- **Load Line:** The load line is a straight line with a negative slope, defined by the equation \( V_{DD}/R_D \). It represents the maximum possible drain current for a given \( v_{DS} \).
- **Operating Points (Q-points):** Two key points, \( Q_0 \) and \( Q_1 \), are marked on the graph. \( Q_0 \) is the quiescent point, indicating the DC operating condition, and \( Q_1 \) represents the AC operating condition when a small signal is applied.
- **Transconductance (\( g_m \)):** The slope of the curve at the operating point \( Q_0 \) is related to the transconductance, \( g_m \), which is a measure of the transistor's ability to convert gate voltage changes into drain current changes.
- **Output Conductance (\( 1/r_o \)):** The slope of the curve at \( Q_1 \) indicates the output conductance, \( 1/r_o \), which is the inverse of the output resistance.

Annotations and Specific Data Points:
- The graph is annotated with the points \( Q_0 \) and \( Q_1 \), which are crucial for understanding the amplifier's operation.
- The load line intersects the \( V_{GS} \) curves at these points, showing the conditions under which the transistor operates in the circuit.

This graph is essential for analyzing and designing the NMOS transistor as a small-signal amplifier, providing insights into how the transistor responds to different gate and drain-source voltages.

FIGURE 3.46 Graphical illustrations of the FET amplifier of Fig. 3.45.

For $\lambda V_{D S} \ll 1$ we can approximate $(k / 2)\left(V_{G S}-V_{t}\right)^{2} \cong I_{D}$ and rewrite as

$$
\lambda_{D}+i_{d}=\lambda_{D}+k V_{O V} v_{g s}+\lambda I_{D} v_{d s}+\cdots
$$

where $V_{O V}=V_{G S}-V_{t}$, as usual. So long as we can ignore higher-order terms involving ac products and powers, the above expression allows us to write

$$
\begin{equation*}
i_{d}=g_{m} v_{g s}+\frac{v_{d s}}{r_{o}} \tag{3.54}
\end{equation*}
$$

where $g_{m}$ is the already familiar transconductance of the FET introduced in Eq. (3.25) and repeated here in its three equivalent forms

$$
\begin{equation*}
g_{m}=k V_{O V}=\sqrt{2 k I_{D}}=2 \frac{I_{D}}{V_{O V}} \tag{3.55}
\end{equation*}
$$

and

$$
\begin{equation*}
r_{o}=\frac{1}{\lambda I_{D}} \tag{3.56}
\end{equation*}
$$

is the familiar drain's output resistance. As shown in Fig. 3.46, $g_{m}$ and $1 / r_{o}$ represent, respectively, the slope of the $i_{D}-v_{G S}$ and the slope of the $i_{D}-v_{D S}$ curve at $Q_{0}$. Both parameters depend on the operating current $I_{D}$. Moreover, the fact that $1 / r_{o} \ll g_{m}$ indicates a much weaker dependence of $i_{d}$ on $v_{d s}$ than on $v_{g s}$.

We wish to assess under what conditions we can ignore higher-order terms in Eq. (3.53). By inspection, the quadratic term can be ignored as long as we keep $v_{g s}$ small enough to satisfy the condition $v_{g s}^{2} \ll 2\left(V_{G S}-V_{t}\right) \mid v_{g s}$, , that is,

$$
\begin{equation*}
\left|v_{g s}\right| \ll 2 V_{O V} \tag{3.57}
\end{equation*}
$$

For obvious reasons Eq. (3.54) is referred to as the small signal approximation, and Eq. (3.57) quantifies the validity of such an approximation.

#### ExAMPLE 3.27

(a) Suppose $v_{g s}$ in Fig. $3.46 a$ is an ac signal with peak values of $\pm V_{m}$. If $I_{D}=1 \mathrm{~mA}$ and $V_{O V}=1 \mathrm{~V}$, find the maximum value of $V_{m}$ for a small-signal approximation error of not more than $10 \%$.
(b) Use the small-signal approximation to estimate the peak values of $i_{d}$.
(c) Find the exact peak values of $i_{d}$, compare with the approximated values, and comment.

#### Solution

(a) With reference to Eq. (3.57), impose $V_{m} \leq 0.1 \times\left(2 V_{O V}\right)=0.1 \times(2 \times 1)=0.2 \mathrm{~V}$.
(b) By Eq. (3.55), $g_{m}=2 I_{D} / V_{O V}=2 \times 1 / 1=2 \mathrm{~mA} / \mathrm{V}$. The small-signal approximation of Eq. (3.54) predicts, for $i_{d}$, peak values of $\pm I_{m}=g_{m}\left( \pm V_{m}\right)=$ $2( \pm 0.2)= \pm 0.4 \mathrm{~mA}$.
(c) With the given data, $k=2 I_{D} / V_{O V}^{2}=2 \times 1 / 1^{2}=2 \mathrm{~mA} / \mathrm{V}^{2}$. By Eq. (3.53), the exact peak values of $i_{d}$ are, respectively, $\pm g_{m} V_{m}+(k / 2) V_{m}^{2}=\left[ \pm 0.4+(2 / 2) 0.2^{2}\right] \mathrm{mA}$, or 0.44 mA and -0.36 mA , respectively. Because of the curvature of the $i_{D}-v_{D S}$ characteristic, the small-signal approximation underestimates the positive current peak by $10 \%$, and overestimates the negative current peak by $10 \%$.

Just like we use the $d c$ equivalent of Fig. 3.45a to investigate the biasing conditions of our FET, we shall use the $a c$ equivalent of Fig. $3.45 c$ to investigate its operation as an amplifier. Indeed, the latter gives, by KVL, Ohm's law, and Eq. (3.54),

$$
v_{d s}=0-R_{D} i_{d}=-R_{D}\left(g_{m} v_{g s}+\frac{v_{d s}}{r_{o}}\right)
$$

Collecting, and solving for $v_{d s}$, we can write

$$
v_{d s}=-g_{m}\left(R_{D} / / r_{o}\right) v_{g s}
$$

indicating that our circuit magnifies $v_{g s}$ by the $\operatorname{gain}-g_{m}\left(R_{D} / / r_{o}\right)$. To give an idea, let $g_{m}=1 \mathrm{~mA} / \mathrm{V}, R_{D}=10 \mathrm{k} \Omega$, and $r_{o}=100 \mathrm{k} \Omega$. Then, $v_{d s}=-9.1 v_{g s}$.

The need to perform dc and ac analysis separately will be illustrated further as we proceed. Figures 3.20 and 3.21 presented large-signal MOSFET models for the purpose of facilitating dc analysis, as exemplified in Figs. 3.30 and 3.32. We now need to develop a small-signal MOSFET model to facilitate ac analysis.

### The Small-Signal Model

Figure 3.47 shows the small-signal model of the MOSFET. The function of this model, also called the incremental model or simply the ac equivalent, is to provide a circuit representation of the dependence of $i_{d}$ upon $v_{g s}$ and $v_{d s}$ as expressed by Eq. (3.54). As we know, the dependence on $v_{d s}$ is much weaker than that on $v_{g s}$, this being the reason why the second term in Eq. (3.54) is sometimes ignored in order to speed up calculations. In this chapter we are limiting our study to MOSFET applications in which body and source are tied together, and the model of Fig. 3.47 is adequate for this kind of investigation. If the source is allowed to float independently of the body, the ensuing body effect requires further refinements in the small-signal model presented here (this will be the subject of the next chapter). The small-signal parameter definitions (for the case of the $n$ MOSFET) and their calculations are summarized in Table 3.1.
image_name:FIGURE 3.47 Small-signal MOSFET model
description:
[
name: NMOS, type: NMOS, ports: {S: S, D: D, G: G}
name: PMOS, type: PMOS, ports: {S: S, D: D, G: G}
name: g_m v_gs, type: VoltageControlledCurrentSource, value: g_m v_gs, ports: {Np: S, Nn: D}
name: r_o, type: Resistor, value: r_o, ports: {N1: D, N2: S}
]
extrainfo:The diagram illustrates the small-signal model for both NMOS and PMOS transistors, where the source and body are tied together. The voltage-controlled current source represents the transconductance, and the resistor represents the output resistance. The direction of current id is shown for both types of transistors.

FIGURE 3.47 Small-signal MOSFET model. This model applies both to the $n$ MOSFET and the pMOSFET.

We wish to point out that the model of Fig. 3.47 applies both to the $n$ MOSFET and the $p$ MOSFET, with no change in voltage polarities or current directions. To see why, consider the effect of increasing $v_{G S}$ by $v_{g s}$ in both devices. In the $n$ MOSFET $i_{D}$ will also increase, but in the $p$ MOSFET $i_{D}$ will decrease. Consequently, $i_{d}$ will have the same direction as $i_{D}$ in the $n \operatorname{MOSFET}$ ( $i_{d}$ into the drain terminal), but the opposite direction as $i_{D}$ in the $p$ MOSFET: since $i_{D}$ flows out of the drain terminal, $i_{d}$ will be into the drain terminal, just as in the $n$ MOSFET case. We must stress that the smallsignal model should not be confused with the large signal models. The latter are used in dc analysis, examples of which we have already seen. The former is used in ac analysis, to be demonstrated next.

TABLE 3.1 Small-signal parameter summary.

| Definition | Calculation |
| :---: | :---: |
| $g_{m}=\left.\frac{\partial i_{D}}{\partial v_{G S}}\right\|_{V_{D S}}$ | $g_{m}=\sqrt{2 k I_{D}}=2 \frac{I_{D}}{V_{O V}}=k V_{O V}$ |
| $\frac{1}{r_{o}}=\left.\frac{\partial i_{D}}{\partial v_{D S}}\right\|_{V_{G S}}$ | $r_{o}=\frac{1}{\lambda I_{D}}$ |

### A Generalized MOSFET Circuit

As our first application of the small-signal model we investigate the generalized MOSFET circuit of Fig. 3.48a, similar to that of Fig. 3.45b, except for the inclusion of the additional resistance $R_{S}$. Our analysis will reveal a number of interesting relationships stemming from the interaction between the FET and the surrounding circuit elements. Moreover, it will provide some general expressions that will help us expedite the ac analysis of future MOSFET amplifiers.

The function of the dc sources $V_{G}$ and $V_{D D}$ is to bias the FET at some dc current $I_{D}$ in the saturation region. Turning on the input ac source $v_{g}$ will result in the drain ac current $i_{d}$ as well as the output ac voltages $v_{d}$ and $v_{s}$. We wish to investigate how the small signals $i_{d}, v_{d}$, and $v_{s}$ are related to $v_{g}$. We also wish to find the small-signal resistances seen looking into the gate, source, and drain terminals, which we shall denote as $R_{g}, R_{s}$, and $R_{d}$. (Note the use of lower-case subscripts to distinguish them from the resistances external to the FET, identified by upper-case subscripts.)
image_name:(a)
description:
[
name: VG, type: VoltageSource, value: VG, ports: {Np: VG, Nn: GND}
name: M1, type: NMOS, ports: {S: s1, D: d1, G: VG}
name: RD, type: Resistor, value: RD, ports: {N1: d1, N2: VDD}
name: RS, type: Resistor, value: RS, ports: {N1: s1, N2: GND}
]
extrainfo:The circuit is a common-source NMOS amplifier with a drain resistor RD and a source resistor RS. The gate voltage is provided by VG, and the output is taken from the drain of the NMOS transistor.

image_name:(b)
description:
[
name: Vg, type: VoltageSource, value: Vg, ports: {Np: Vg, Nn: GND}
name: RS, type: Resistor, value: RS, ports: {N1: Vs, N2: GND}
name: RD, type: Resistor, value: RD, ports: {N1: Vd, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: Vd, N2: Vs}
name: gmVgs, type: VoltageControlledCurrentSource, ports: {N1: Vd, N2: Vs}
]
extrainfo:The circuit is a small-signal model of a MOSFET amplifier. It includes a voltage source Vg, resistors RD, RS, and ro, and a voltage-controlled current source gmVgs. The small-signal output voltages vd and vs are measured across the drain and source, respectively.

(b)

FIGURE 3.48 (a) A generalized MOSFET circuit, and (b) its small-signal equivalent.
As a rule, in order to perform the small-signal analysis of a MOS circuit,

- We replace the FET with its small-signal model
- We show only the ac signals, as depicted in the equivalent circuit of Fig. 3.48b. The bias voltages $\left(V_{G}\right.$ and $\left.V_{D D}\right)$ as well as all other dc components $\left(V_{S}, V_{D}\right.$, and $I_{D}$ ) do not appear in this equivalent because they are constant and thus possess no ac components. Consequently, as we go from the actual circuit to its small-signal equivalent, we set all dc voltages and all dc currents to zero.

Let us now proceed to find the aforementioned small-signal relationships and resistances.

- The Circuit's Small-Signal Transconductance $\boldsymbol{G}_{m}=\boldsymbol{i}_{d} / \boldsymbol{v}_{g}$. With reference to Fig. 3.48b, KCL gives,

$$
i_{d}=g_{m} v_{g s}+\frac{v_{d}-v_{s}}{r_{o}}
$$

Now, by Ohm's law, $0-v_{d}=R_{D} i_{d}$, or

$$
\begin{equation*}
v_{d}=-R_{D} i_{d} \tag{3.58}
\end{equation*}
$$

By Ohm's law again,

$$
\begin{equation*}
v_{s}=R_{S} i_{d} \tag{3.59}
\end{equation*}
$$

Also, by definition, $v_{g s}=v_{g}-v_{s}$, or

$$
\begin{equation*}
v_{g s}=v_{g}-R_{S} i_{d} \tag{3.60}
\end{equation*}
$$

Substituting $v_{g s}, v_{d}$, and $v_{s}$ into the expression for $i_{d}$ and collecting, we get

$$
\begin{equation*}
i_{d}=G_{m} v_{g} \tag{3.61}
\end{equation*}
$$

where $G_{m}$, referred to as the circuit's transconductance (not to be confused with the individual FET's transconductance $g_{m}$ ) is given by

$$
\begin{equation*}
G_{m}=\frac{g_{m}}{1+g_{m} R_{S}+\left(R_{D}+R_{S}\right) / r_{o}} \tag{3.62a}
\end{equation*}
$$

As we proceed, we will find that in discrete MOSFET amplifiers we usually have $\left(R_{D}+R_{S}\right) / r_{o} \ll 1$, so Eq. (3.62a) simplifies to

$$
\begin{equation*}
G_{m} \cong \frac{g_{m}}{1+g_{m} R_{S}} \tag{3.62b}
\end{equation*}
$$

Note that for $R_{S}=0$ we have $G_{m}=g_{m}$, but for $R_{S} \neq 0$ we have $G_{m}<g_{m}$. This transconductance reduction, referred to as degeneration, stems from the fact that the voltage drop $R_{S} i_{d}$ subtracts from the input $v_{g}$ to yield a reduced control signal $v_{g s}$ for the dependent source, as per Eq. (3.60). Hence, $i_{d}\left(=g_{m} v_{g s}\right)$ will also get reduced. A more systematic investigation of degeneration reveals that $R_{S}$ provides a negative feedback function, as mentioned in connection with Example 3.19. Though this subject will be investigated systematically in Chapter 7, suffice it to say here that the presence of $R_{S}$, aptly called source-degeneration resistance, not only reduces the transconductance, but also affects the small-signal resistance $R_{d}$ seen looking into the drain, as we are about to find out.

- The Small-Signal Voltage Gain $\boldsymbol{v}_{\boldsymbol{d}} / \boldsymbol{v}_{g}$ from Gate to Drain. By Eqs. (3.58), (3.61), and (3.62a), this gain is

$$
\begin{equation*}
\frac{v_{d}}{v_{g}}=\frac{-g_{m} R_{D}}{1+g_{m} R_{S}+\left(R_{D}+R_{S}\right) / r_{o}} \tag{3.63a}
\end{equation*}
$$

The negative sign indicates inverting amplification from gate to drain: positive (negative) alternations in $v_{g}$ result in negative (positive) alternations in $v_{d}$. If the condition $\left(R_{D}+R_{S}\right) \ll r_{o}$ holds, Eq. (3.63a) simplifies to

$$
\begin{equation*}
\frac{v_{d}}{v_{g}} \cong-\frac{g_{m} R_{D}}{1+g_{m} R_{S}} \tag{3.63b}
\end{equation*}
$$

- The Small-Signal Voltage Gain $\boldsymbol{v}_{\boldsymbol{s}} / \boldsymbol{v}_{\boldsymbol{g}}$ from Gate to Source. By Eqs. (3.59), (3.61), and (3.62), this gain is

$$
\begin{equation*}
\frac{v_{s}}{v_{g}}=\frac{g_{m} R_{S}}{1+g_{m} R_{S}+\left(R_{D}+R_{S}\right) / r_{o}} \tag{3.64a}
\end{equation*}
$$

indicating that $v_{s}$ is in phase with $v_{g}$. If the condition $\left(R_{D}+R_{S}\right) \ll r_{o}$ holds, Eq. (3.64a) simplifies to

$$
\begin{equation*}
\frac{v_{s}}{v_{g}} \cong \frac{1}{1+1 /\left(g_{m} R_{S}\right)} \tag{3.64b}
\end{equation*}
$$

The gain from gate to source is a bit less than unity, depending on how large the product $g_{m} R_{S}$ is compared to unity. We summarize this by saying that the source follows the gate.

- The Small-Signal Resistance $\boldsymbol{R}_{g}$ Seen Looking into the Gate. As we know, the gate electrode is the plate of a tiny capacitor, which draws negligible current, at

EXAMPLE 3.28 A certain FET with $k=0.5 \mathrm{~mA} / \mathrm{V}^{2}$ and $\lambda=0.01 \mathrm{~V}^{-1}$ is biased at $I_{D}=1 \mathrm{~mA}$. If $R_{D}=10 \mathrm{k} \Omega$ and $R_{S}=2.0 \mathrm{k} \Omega$, estimate the gains $v_{d} / v_{g}$ and $v_{s} / v_{g}$.

#### Solution

By Eqs. (3.55) and (3.56) we have $g_{m}=1 /(1 \mathrm{k} \Omega)$ and $r_{o}=100 \mathrm{k} \Omega$. Exploiting the fact that $\left(R_{D}+R_{S}\right) \ll r_{o}(12 \ll 100)$, we use the approximate expressions of Eqs. (3.63b) and (3.64b) to find

$$
\frac{v_{d}}{v_{g}} \cong-\frac{1 \times 10}{1+1 \times 2}=-3.33 \mathrm{~V} / \mathrm{V} \quad \frac{v_{s}}{v_{g}} \cong \frac{1}{1+1 /(1 \times 2)}=0.67 \mathrm{~V} / \mathrm{V}
$$

least up to moderate frequencies. For practical purposes we can thus say that the resistance seen looking into the gate of a MOSFET is

$$
\begin{equation*}
R_{g}=\infty \tag{3.65}
\end{equation*}
$$

- The Small-Signal Resistance $\boldsymbol{R}_{s}$ Seen Looking into the Source. To find this resistance, set $v_{g} \rightarrow 0$ in the ac equivalent of Fig. $3.48 b$, apply a test voltage $v_{s}$ right to the source terminal as in Fig. 3.49a (note that the external resistance $R_{S}$ does not intervene in this test), find the resulting current $i_{s}$, and finally let $R_{s}=v_{s} / i_{s}$. Thus, summing currents into the source node we get

$$
i_{s}+g_{m} v_{g s}+\frac{v_{d}-v_{s}}{r_{o}}=0
$$

But, $v_{g s}=v_{g}-v_{s}=0-v_{s}=-v_{s}$, and $v_{d}=R_{D} i_{s}$. Substituting, collecting, and solving for the ratio $v_{s} / i_{s}$ we get, after suitable algebraic manipulation,

$$
\begin{equation*}
R_{s}=\left(\frac{1}{g_{m}} / / r_{o}\right)+\frac{R_{D}}{1+g_{m} r_{o}} \tag{3.66a}
\end{equation*}
$$

Because of the coupling action by $r_{o}, R_{s}$ depends also on the external drain resistance $R_{D}$, and we say that reflected to the source, $R_{D}$ gets divided by $\left(1+g_{m} r_{o}\right)$. MOSFETs usually have $g_{m} r_{o} \gg 1$. Moreover, discrete MOSFET amplifiers usually have $R_{D} \ll r_{o}$. Under these conditions, Eq. (3.66a) simplifies to

$$
\begin{equation*}
R_{s} \cong \frac{1}{g_{m}} / / r_{o} \cong \frac{1}{g_{m}} \tag{3.66b}
\end{equation*}
$$

Note the similarity with BJTs.
image_name:(a)
description:
[
name: R_D, type: Resistor, value: R_D, ports: {N1: Vd, N2: GND}
name: r_o, type: Resistor, value: r_o, ports: {N1: Vd, N2: Vs}
name: g_m*v_gs, type: VoltageControlledCurrentSource, ports: {Np: Vd, Nn: Vs}
name: v_s, type: VoltageSource, value: v_s, ports: {Np: Vs, Nn: GND}
]
extrainfo:The circuit is used to find the small-signal resistance Rs seen looking into the source. It consists of a voltage-controlled current source, resistors, and a voltage source.
image_name:(b)
description:
[
name: RS, type: Resistor, value: RS, ports: {N1: Vs, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: Vd, N2: Vs}
name: gmvgs, type: VoltageControlledCurrentSource, ports: {Np: Vs, Nn: Vd}
name: RS, type: Resistor, value: RS, ports: {N1: Vs, N2: GND}
name: Vd, type: VoltageSource, value: Vd, ports: {Np: Vd, Nn: GND}
]
extrainfo:The circuit diagram (b) shows a test circuit to find the small-signal resistance Rs seen looking into the source. It includes a voltage-controlled current source gmvgs, and resistors RD, ro, and RS. The voltage source vd is connected across the drain and ground.

FIGURE 3.49 Test circuits to find (a) the small-signal resistance $R_{s}$ seen looking into the source, and (b) the small-signal resistance $R_{d}$ seen looking into the drain.

- The Small-Signal Resistance $\boldsymbol{R}_{d}$ Seen Looking into the Drain. To find this resistance, let $v_{g} \rightarrow 0$ in the ac equivalent of Fig. 3.48b, apply a test voltage $v_{d}$ right to the drain terminal as in Fig. $3.49 b$ (note that $R_{D}$ does not intervene in this test), find the resulting current $i_{d}$, and finally let $R_{d}=v_{d} / i_{d}$. Thus, KCL at the source node gives

$$
\begin{aligned}
i_{d} & =g_{m} v_{g s}+\frac{v_{d}-v_{s}}{r_{o}}=g_{m}\left(0-v_{s}\right)+\frac{v_{d}}{r_{o}}-\frac{v_{s}}{r_{o}}=\frac{v_{d}}{r_{o}}-\left(g_{m}+\frac{1}{r_{o}}\right) v_{s} \\
& =\frac{v_{d}}{r_{o}}-\left(\frac{g_{m}+1}{r_{o}}\right) R_{s} i_{d}
\end{aligned}
$$

Collecting and solving for the ratio $v_{d} / i_{d}$ gives

$$
\begin{equation*}
R_{d}=r_{o}+\left(1+g_{m} r_{o}\right) R_{S} \tag{3.67a}
\end{equation*}
$$

Because of the coupling action by $r_{o}, R_{d}$ depends also on the external source resistance $R_{S}$, and we say that reflected to the drain, $R_{S}$ gets multiplied by $\left(1+g_{m} r_{o}\right)$. Again exploiting the fact that $g_{m} r_{o} \gg 1$ and that discrete MOSFET amplifiers usually have $R_{S} \ll r_{o}$, we simplify Eq. (3.67a) as

$$
\begin{equation*}
R_{d} \cong r_{o}\left(1+g_{m} R_{S}\right) \tag{3.67b}
\end{equation*}
$$

We observe that with $R_{S}=0$ we get $R_{d}=r_{o}$, but with $R_{S} \neq 0$ we get $R_{d}>r_{o}$. This increase in $R_{d}$ is the result of the aforementioned negative-feedback action by the source-degeneration resistance $R_{S}$. (Note also the similarity with BJTs.)

It is interesting to contrast the effects that the FET has upon its external resistances: while $R_{D}$ reflected to the source gets divided by $\left(1+g_{m} r_{o}\right), R_{S}$ reflected to the drain gets multiplied by $\left(1+g_{m} r_{o}\right)$. For convenience the small-signal characteristics are tabulated in Fig. 3.50 for the ac equivalent shown.
image_name:ac equivalent
description:
[
name: M1, type: NMOS, ports: {S: Vs, D: Vd, G: Vg}
name: R_D, type: Resistor, value: R_D, ports: {N1: Vd, N2: GND}
name: R_S, type: Resistor, value: R_S, ports: {N1: Vs, N2: GND}
name: v_g, type: VoltageSource, value: v_g, ports: {Np: vg, Nn: GND}
]
extrainfo:The circuit is an AC equivalent model of an NMOS transistor with source degeneration. It includes resistors R_D and R_S for drain and source, respectively, and a gate resistor R_g. The table summarizes small-signal gains and terminal resistances.
image_name:Summary of small-signal gains and terminal resistances
description:The image consists of a diagram and a table summarizing the small-signal gains and terminal resistances for a field-effect transistor (FET) circuit.

**Diagram Description:**
- The circuit diagram on the left shows a common-source FET configuration.
- The FET is labeled as M1, with the gate voltage (Vg), drain voltage (Vd), and source voltage (Vs) indicated.
- The circuit includes resistors Rs and RD connected to the source and drain, respectively.
- The input voltage vg is applied at the gate, and the output is taken across the drain.

**Table Description:**
- The table on the right is divided into two columns: "Exact" and "Approximate," listing the expressions for small-signal parameters.

**Exact Column:**
1. Transconductance gain (Gm):
\[ G_m = \frac{i_d}{v_g} = \frac{g_m}{1 + g_m R_S + (R_D + R_S)/r_o} \]
2. Voltage gain from gate to drain (vd/vg):
\[ \frac{v_d}{v_g} = \frac{-g_m R_D}{1 + g_m R_S + (R_D + R_S)/r_o} \]
3. Voltage gain from gate to source (vs/vg):
\[ \frac{v_s}{v_g} = \frac{g_m R_S}{1 + g_m R_S + (R_D + R_S)/r_o} \]
4. Gate resistance (Rg):
\[ R_g = \infty \]
5. Source resistance (Rs):
\[ R_s = \left(\frac{1}{g_m} || r_o\right) + \frac{R_D}{1 + g_m r_o} \]
6. Drain resistance (Rd):
\[ R_d = r_o (1 + g_m R_S) + R_S \]

**Approximate Column:**
1. Transconductance gain (Gm):
\[ G_m \approx \frac{g_m}{1 + g_m R_S} \]
2. Voltage gain from gate to drain (vd/vg):
\[ \frac{v_d}{v_g} \approx \frac{-g_m R_D}{1 + g_m R_S} \]
3. Voltage gain from gate to source (vs/vg):
\[ \frac{v_s}{v_g} \approx \frac{1}{1 + 1/(g_m R_S)} \]
4. Gate resistance (Rg):
\[ R_g = \infty \]
5. Source resistance (Rs):
\[ R_s \approx \frac{1}{g_m} \]
6. Drain resistance (Rd):
\[ R_d \approx r_o (1 + g_m R_S) \]

The table provides both exact and simplified expressions for analyzing the small-signal behavior of the FET circuit, highlighting the impact of various resistances and parameters such as transconductance (gm) and output resistance (ro).

FIGURE 3.50 Summary of small-signal gains and terminal resistances, and approximations for discrete designs.

EXAMPLE 3.29 (a) Using the small-signal FET parameters of Example 3.28, estimate $R_{s}$ if $R_{D}=0$.
(b) Estimate $R_{d}$ if $R_{S}=5 \mathrm{k} \Omega$.

#### Solution

(a) Exploiting the fact that $1 / g_{m} \ll r_{o}$, we use Eq. (3.66b) to find

$$
R_{s} \cong 1 / g_{m}=1 \mathrm{k} \Omega
$$

(b) Since $R_{S} \ll r_{o}$, we use Eq. (3.67b) to find

$$
R_{d} \cong 100(1+1 \times 5)=600 \mathrm{k} \Omega
$$

## 3.8 BASIC MOSFET VOLTAGE AMPLIFIERS

Depending on which terminal we apply the input to and which terminal we obtain the output from, a MOSFET can be used in any one of three amplifier configurations: the common-source, common-drain, and common-gate configurations. In the following we shall assume that body and source are tied together so that the MOSFET is operated as a three-terminal device. Viewing an amplifier as a two-port block, it is apparent that one of the terminals of the three-terminal FET will have to be common to both ports; hence, the reason for the above designations.

Nowadays the majority of MOSFET circuits are implemented in integratedcircuit form using MOSFETs to provide both active functions (such as amplification) and passive functions (such as dc biasing and active loading). However, before turning to multiple-transistor circuitry, we need to master single-transistor stages, and this is best done if we focus on a single MOSFET surrounded by already familiar components such as resistors and capacitors. The resulting circuits, referred to as discrete circuits because we can build them in the lab using off-the-shelf components, provide not only an historical prospective, but are also somewhat easier to grasp, and yet reveal important aspects that apply to integrated-circuit implementations as well.

Figure 3.51 shows the block diagram of a voltage amplifier. The amplifier receives its input $v_{i}$ from a signal source $v_{s i g}$ with internal resistance $R_{s i g}$, and supplies its output $v_{o}$ to a resistive load $R_{L}$. The amplifier is uniquely characterized in terms of its input resistance $R_{i}$, output resistance $R_{o}$, and the open-circuit voltage gain $a_{o c}$. At the amplifier's input we have a voltage divider, resulting in input loading

$$
\begin{equation*}
v_{i}=\frac{R_{i}}{R_{s i g}+R_{i}} v_{s i g} \tag{3.68}
\end{equation*}
$$

image_name:FIGURE 3.51 Block diagram of a voltage amplifier
description:The block diagram of a voltage amplifier, labeled as FIGURE 3.51, illustrates the flow of signals from a signal source to a load through an amplifier. Here is a detailed description of the system:

1. **Main Components:**
- **Signal Source ($v_{sig}$):** This is the initial source of the input signal, represented by a voltage source in series with an internal resistance $R_{sig}$.
- **Input Resistance ($R_{i}$):** This is the resistance at the input of the amplifier, forming a voltage divider with $R_{sig}$.
- **Amplifier Block:** Characterized by its open-circuit voltage gain $a_{oc}$. It amplifies the input voltage $v_{i}$ to produce an intermediate voltage $a_{oc} \times v_{i}$.
- **Output Resistance ($R_{o}$):** The resistance at the output of the amplifier, forming a voltage divider with the load resistance $R_{L}$.
- **Load Resistance ($R_{L}$):** The resistive load connected to the amplifier's output.

2. **Flow of Information or Control:**
- The input signal $v_{sig}$ flows through the internal resistance $R_{sig}$, reaching the amplifier's input where it encounters the input resistance $R_{i}$.
- The voltage at the amplifier input, $v_{i}$, is determined by the voltage divider formed by $R_{sig}$ and $R_{i}$, calculated as $v_{i} = \frac{R_{i}}{R_{sig} + R_{i}} v_{sig}$.
- Inside the amplifier, this input voltage $v_{i}$ is multiplied by the open-circuit gain $a_{oc}$, resulting in the amplified voltage $a_{oc} \times v_{i}$.
- This amplified voltage is then subject to another voltage divider formed by the output resistance $R_{o}$ and the load resistance $R_{L}$, producing the final output voltage $v_{o} = \frac{R_{L}}{R_{o} + R_{L}} a_{oc} \times v_{i}$.

3. **Labels, Annotations, and Key Indicators:**
- The diagram clearly labels all components and signals, including $v_{sig}$, $R_{sig}$, $v_{i}$, $R_{i}$, $a_{oc}$, $R_{o}$, $R_{L}$, and $v_{o}$.
- Ground (GND) symbols are used to indicate common reference points for the voltages.

4. **Overall System Function:**
- The primary function of this system is to amplify the input signal $v_{sig}$ and deliver an amplified output voltage $v_{o}$ to the load $R_{L}$. The system uses voltage dividers at both the input and output to manage signal levels, with the amplifier providing the necessary gain through its open-circuit voltage gain $a_{oc}$. The configuration ensures that the input and output impedances are matched to optimize signal transfer and minimize losses.

FIGURE 3.51 Block diagram of a voltage amplifier.

Likewise, at the amplifier's output we have another voltage divider, resulting in output loading

$$
\begin{equation*}
v_{o}=\frac{R_{L}}{R_{o}+R_{L}} a_{o c} \times v_{i} \tag{3.69}
\end{equation*}
$$

We observe that

$$
\begin{equation*}
a_{o c}=\left.\frac{v_{o}}{v_{i}}\right|_{R_{L} \rightarrow \infty} \tag{3.70}
\end{equation*}
$$

that is, $a_{o c}$ represents the gain with which the amplifier would amplify its input $v_{i}$ in the absence of any output load. Consequently, $a_{o c}$ is called the open-circuit voltage gain, or also the unloaded voltage gain. Eliminating $v_{i}$ from the above equations, we obtain the signal-to-load voltage gain

$$
\begin{equation*}
\frac{v_{o}}{v_{s i g}}=\frac{R_{i}}{R_{s i g}+R_{i}} \times a_{o c} \times \frac{R_{L}}{R_{o}+R_{L}} \tag{3.71}
\end{equation*}
$$

As the signal progresses from the source to the load, first it undergoes some attenuation at the amplifier's input, then it gets magnified by $a_{o c}$, and finally it undergoes some additional attenuation at the output.

### The Common-Source (CS) Configuration

In the circuit of Fig. 3.52 the amplifier proper is made up of the FET and surrounding components. To prevent the source and the load from disturbing the dc conditions of the FET we use the ac-coupling capacitors $C_{1}$ and $C_{2}$. Moreover, to establish an ac ground at the source terminal, we use the bypass capacitor $C_{3}$.

At dc the capacitors draw zero current and thus act as open circuits. In fact, in the dc equivalent of Fig. 3.53a, the capacitors have been omitted altogether. Also, to simplify dc analysis, we assume $\lambda=0$ and we use a dc current $\operatorname{sink} I_{D}$ to bias the
image_name:FIGURE 3.52 The common-source (CS) amplifier.
description:
[
name: Vsig, type: VoltageSource, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: vi}
name: C1, type: Capacitor, value: C1, ports: {Np: vi, Nn: g1}
name: RG, type: Resistor, value: RG, ports: {N1: g1, N2: GND}
name: RD, type: Resistor, value: RD, ports: {N1: d1, N2: VDD}
name: C2, type: Capacitor, value: C2, ports: {Np: d1, Nn: vo}
name: Ro, type: Resistor, value: Ro, ports: {N1: vo, N2: RL}
name: RL, type: Resistor, value: RL, ports: {N1: vo, N2: GND}
name: M1, type: NMOS, ports: {S: s1, D: d1, G: g1}
name: ID, type: CurrentSource, value: ID, ports: {Np: s1, Nn: VSS}
name: C3, type: Capacitor, value: C3, ports: {Np: s1, Nn: GND}
]
extrainfo:The circuit is a common-source (CS) amplifier using an NMOS transistor with ac-coupling and bypass capacitors to isolate dc conditions. The input signal is ac-coupled through C1, and the output is taken across C2. The current source ID provides biasing for the NMOS transistor.

FIGURE 3.52 The common-source (CS) amplifier.
image_name:Figure 3.52 (a)
description:
[
name: RD, type: Resistor, value: RD, ports: {N1: VDD, N2: VD}
name: RG, type: Resistor, value: RG, ports: {N1: VG, N2: GND}
name: k/2(VGS-Vt)^2, type: VoltageControlledCurrentSource, ports: {N1: VD, N2: VS, N3: VG, N4: VS}
]
extrainfo:The circuit is a common-source (CS) amplifier using an NMOS transistor with ac-coupling and bypass capacitors to isolate dc conditions. The input signal is ac-coupled through C1, and the output is taken across C2. The current source ID provides biasing for the NMOS transistor.

(a)
image_name:(b)
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: vi}
name: RG, type: Resistor, value: RG, ports: {N1: vi, N2: GND}
name: gmVgs, type: VoltageControlledCurrentSource, value: gmVgs, ports: {Np: vo, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: vo, N2: GND}
name: RD, type: Resistor, value: RD, ports: {N1: vo, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: vo, N2: GND}
]
extrainfo:The circuit is an AC equivalent model of a common-source amplifier with an NMOS transistor. It includes a voltage source (Vsig) for the input signal, resistors for biasing and load (Rsig, Ri, RG, RD, Ro, RL), and a voltage-controlled current source (gmVgs) to model the transistor's transconductance. The output is taken across the load resistor RL.

(b)

FIGURE 3.53 (a) $D c$ and (b) ac equivalents of the CS amplifier of Fig. 3.52.
FET. Such a sink could be implemented with another FET, such as a current mirror (let us not worry about these details here). The dc voltages are then

$$
\begin{equation*}
V_{G}=0 \quad V_{D}=V_{D D}-R_{D} I_{D} \quad V_{S}=-\left(V_{t}+V_{O V}\right) \tag{3.72}
\end{equation*}
$$

where $V_{O V}=\sqrt{2 I_{D} / k}$. When power is applied to the circuit, each capacitor will charge up until its plates attain the dc voltages of their corresponding nodes. For instance, while the bottom plate of $C_{3}$ remains at ground potential, the top plate will charge to $V_{S}$, which in this circuit is negative. Likewise, the left plate of $C_{2}$ will charge to $V_{D}$, while the right plate is pulled to 0 V by $R_{L}$.

When analyzing a voltage amplifier we are interested in its signal-to-load voltage gain $v_{o} / v_{s i g}$. By Eq. (3.71) this requires finding the input resistance $R_{i}$ seen by the signal source, the output resistance $R_{o}$ seen by the load, and the unloaded voltage gain $a_{o c}$. We find these parameters by working with the ac equivalent of Fig. 3.53b. However, since the small-signal parameters $g_{m}$ and $r_{o}$ depend on the dc bias of the FET, we need to analyze also the dc equivalent of Fig. 3.53a. Before proceeding, we wish to call the reader's attention to the difference between dc and ac analysis as well as the need to keep them separate!

In going from the original circuit of Fig. 3.52 to its dc equivalent of Fig. 3.53a we apply the following

Dc Analysis Procedure:

- Set all ac sources to zero
- Replace the MOSFET with its large-signal model (assume $\lambda=0$ for simplicity)
- Replace all capacitors with open circuits

Conversely, in going from the original circuit of Fig. 3.52 to its ac equivalent of Fig. $3.53 b$ we apply the following

Ac Analysis Procedure:

- Set all $d c$ sources to zero
- Replace the MOSFET with its small-signal model, inclusive of $r_{o}$
- Replace all capacitors with short circuits

With reference to Fig. 3.53b, we note by inspection that

$$
\begin{equation*}
R_{i}=R_{G} \quad R_{o}=R_{D} / / r_{o} \tag{3.73}
\end{equation*}
$$

Moreover, by Ohm's law, we have

$$
0-v_{o}=\left(r_{o} / / R_{D} / / / R_{L}\right) g_{m} v_{g s}=\left(r_{o} / / R_{D} / / R_{L}\right) g_{m} v_{i}
$$

Letting $R_{L} \rightarrow \infty$ gives $v_{o}=-\left(r_{o} / / R_{D}\right) g_{m} v_{i}$. But, according to Eq. (3.70), the ratio $v_{o} / v_{i}$ in the limit $R_{L} \rightarrow \infty$ is the unloaded voltage gain. Consequently,

$$
\begin{equation*}
a_{o c}=-g_{m}\left(R_{D} / / r_{o}\right) \tag{3.74}
\end{equation*}
$$

Having obtained expressions for $R_{i}, R_{o}$, and $a_{o c}$, we now apply Eq. (3.71) to find the signal-to-load gain.

In the circuit of Fig. 3.52 let $V_{D D}=-V_{S S}=12 \mathrm{~V}, I_{D}=1 \mathrm{~mA}, R_{G}=1 \mathrm{M} \Omega$, and $R_{D}=10 \mathrm{k} \Omega$, and let the FET have $V_{t}=1.0 \mathrm{~V}, k=0.5 \mathrm{~mA} / \mathrm{V}^{2}$, and $\lambda=0.01 \mathrm{~V}^{-1}$. Assuming $R_{\text {sig }}=0.1 \mathrm{M} \Omega, R_{L}=30 \mathrm{k} \Omega$, and

$$
v_{s i g}=(100 \mathrm{mV}) \cos \omega t
$$

find all node voltages in the circuit, express each of them as the sum of the dc and ac component, in the manner of Eq. (3.48), and show them explicitly in the circuit.

#### Solution

We have $V_{O V}=\sqrt{2 I_{D} / k}=\sqrt{2 \times 1 / 0.5}=2 \mathrm{~V}$, so Eq. (3.72) gives

$$
V_{G}=0 \quad V_{D}=12-10 \times 1=2 \mathrm{~V} \quad V_{S}=-(1+2)=-3 \mathrm{~V}
$$

Moreover, $g_{m}=\sqrt{2 k I_{D}}=\sqrt{2 \times 0.5 \times 1}=1 \mathrm{~mA} / \mathrm{V}$ and $r_{o}=1 / \lambda I_{D}=1 /(0.01 \times 1)=$ $100 \mathrm{k} \Omega$. Consequently, Eqs. (3.73) and (3.74) give

$$
R_{i}=1 \mathrm{M} \Omega \quad R_{o}=10 / / 100=9.09 \mathrm{k} \Omega \quad a_{o c}=-1 \times 9.09=-9.09 \mathrm{~V} / \mathrm{V}
$$

Also, Eq. (3.68) gives $v_{i}=[1 /(0.1+1)] v_{s i g}=(90.9 \mathrm{mV}) \cos \omega t$. Finally, using Eq. (3.71) we find

$$
\begin{aligned}
v_{o} & =\left[\frac{1}{0.1+1}(-9.09) \frac{30}{9.09+30}\right] v_{s i g}=-6.34 \times(100 \mathrm{mV}) \cos \omega t \\
& =(634 \mathrm{mV}) \cos \left(\omega t-180^{\circ}\right)
\end{aligned}
$$

The node voltages are shown in Fig. 3.54. The reader is encouraged to verify each of them in detail.
image_name:Figure 3.54
description:
[
name: V1, type: VoltageSource, value: 100 mVcosωt, ports: {Np: V1, Nn: GND}
name: R1, type: Resistor, value: 0.1 MΩ, ports: {N1: V1, N2: NC1}
name: R2, type: Resistor, value: 1 MΩ, ports: {N1: g1, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: NC1, Nn: g1}
name: R3, type: Resistor, value: 10 kΩ, ports: {N1: VDD, N2: D1}
name: R4, type: Resistor, value: 30 kΩ, ports: {N1: NC2, N2: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: D1, Nn: NC2}
name: M1, type: NMOS, ports: {S: S1, D: D1, G: g1}
name: I1, type: CurrentSource, value: 1 mA, ports: {Np: S1, Nn: GND}
name: C3, type: Capacitor, value: C3, ports: {Np: S1, Nn: GND}
]
extrainfo:The circuit is an amplifier with a voltage source input and an NMOS transistor. The circuit shows both DC and AC voltage components at each node, with an emphasis on the AC analysis. The NMOS transistor operates with a gate connected to the input signal, and the output is taken across a resistor-capacitor network. The DC biasing is provided by a current source and a voltage source.

FIGURE 3.54 Circuit of Example 3.30, showing the dc and ac voltage component at each node.

The systematic procedure of redrawing an amplifier both in dc and ac form, as exemplified in Fig. 3.53, though highly recommended for the beginner, may soon prove an overkill as one seeks to speed up the analysis process. With experience, some of the intermediate steps can be carried out mentally without having to draw detailed circuit equivalents. Moreover, one can use inspection to recycle a good deal of the results developed in connection with the generalized circuit of Fig. 3.48, and summarized in Fig. 3.50. We shall illustrate with a variety of examples as we proceed.

EXAMPLE 3.31 Shown in Fig. $3.55 a$ is a popular single-supply realization of the CS amplifier. The function of $R_{1}$ and $R_{2}$ is to bias the gate at some intermediate voltage between the $10-\mathrm{V}$ supply and ground, and that of $R_{S}$ is to set the value of the bias current $I_{D}$.
(a) Assuming $V_{t}=1.5 \mathrm{~V}, k=0.8 \mathrm{~mA} / \mathrm{V}^{2}$, and $\lambda=0.02 \mathrm{~V}^{-1}$, find the small-signal parameters $R_{i}, R_{o}$, and $a_{o c}=v_{o} / v_{i}$.
(b) Find the signal-to-load gain if the circuit is driven by a source with $R_{s i g}=$ $100 \mathrm{k} \Omega$, and it drives a load $R_{L}=75 \mathrm{k} \Omega$.

#### Solution

(a) First we need to find the bias current $I_{D}$. Considering that at dc all capacitors act as open circuits, it is apparent that the dc version of our amplifier is of the type of Fig. 3.34a. Proceeding as in Example 3.23 with $\lambda=0$ to simplify dc analysis, we readily find $I_{D}=0.4 \mathrm{~mA}$. We thus have

$$
\begin{aligned}
g_{m} & =\sqrt{2 k I_{D}}=\sqrt{2 \times 0.8 \times 0.4}=0.8 \mathrm{~mA} / \mathrm{V} \\
r_{o} & =1 / \lambda I_{D}=1 /(0.02 \times 0.4)=125 \mathrm{k} \Omega
\end{aligned}
$$

image_name:(a)
description:
[
name: R1, type: Resistor, value: 2.2 MΩ, ports: {N1: g1, N2: 10V}
name: R2, type: Resistor, value: 1.8 MΩ, ports: {N1: g1, N2: GND}
name: RS, type: Resistor, value: 5 kΩ, ports: {N1: s1, N2: GND}
name: RD, type: Resistor, value: 10 kΩ, ports: {N1: d1, N2: 10V}
name: M1, type: NMOS, ports: {S: s1, D: d1, G: g1}
name: C1, type: Capacitor, value: C1, ports: {Np: vi, Nn: g1}
name: C2, type: Capacitor, value: C2, ports: {Np: d1, Nn: vo}
name: C3, type: Capacitor, value: C3, ports: {Np: s1, Nn: GND}
]
extrainfo:The circuit is a single-supply common-source (CS) amplifier. The NMOS transistor M1 is used for amplification with a biasing network formed by R1 and R2. Capacitors C1, C2, and C3 are used for coupling and bypassing. The amplifier is powered by a 10V supply.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Vo, G: Vi}
name: R1, type: Resistor, value: 2.2 MΩ, ports: {N1: Vi, N2: GND}
name: R2, type: Resistor, value: 1.8 MΩ, ports: {N1: Vi, N2: GND}
name: RD, type: Resistor, value: 10 kΩ, ports: {N1: Vd, N2: GND}
]
extrainfo:The circuit is an AC equivalent of a common-source amplifier with bypassed source resistor, simplifying the gain calculation. The source is at AC ground due to the bypass capacitor C3.

FIGURE 3.55 (a) Single-supply CS amplifier of Example 3.31, and (b) its ac equivalent.
Next, refer to the ac equivalent of Fig. $3.55 b$, where we note that the bypass action by $C_{3}$ puts the source at ac ground. Consequently, we recycle the results tabulated in Fig. 3.50, but with $R_{S}=0$. By inspection,

$$
\begin{aligned}
& R_{i}=R_{1} / / R_{2} / / R_{g}=2.2 / / 1.8 / / 00=990 \mathrm{k} \Omega \\
& R_{o}=R_{D} / / R_{d}=R_{D} / / r_{o}=10 / / 125=9.26 \mathrm{k} \Omega \\
& a_{o c}=-g_{m} R_{o}=-0.8 \times 9.26=-7.4 \mathrm{~V} / \mathrm{V}
\end{aligned}
$$

(b) Owing to input and output loading, the gain drops to

$$
\frac{v_{o}}{v_{s i g}}=\frac{990}{100+990}(-7.4) \frac{75}{9.26+75}=-5.98 \mathrm{~V} / \mathrm{V}
$$

The single-supply CS amplifier of Fig. $3.56 a$ utilizes a popular dc biasing alternative known as feedback bias. The name stems from the presence of resistance $R_{F}$, which feeds the dc voltage of the drain back to the gate. Since $I_{G}=0$, the voltage drop across $R_{F}$ is 0 V , indicating that the FET operates with $V_{G}=V_{D}$, that is, in the diode mode, and therefore in saturation.
(a) Assuming $V_{t}=2.0 \mathrm{~V}, k=1.0 \mathrm{~mA} / \mathrm{V}^{2}$, and $\lambda=0.033 \mathrm{~V}^{-1}$, find the dc operating point of the FET, as well as $a_{o c}=v_{o} / v_{i}, R_{i}$ (the input resistance with the output port open-circuited), and $R_{o}$ (the output resistance with the input port short-circuited).
(b) Assuming $v_{i}$ is an ac signal with amplitude $V_{i m}$, what is the maximum value of $V_{i m}$ if we wish to contain the small-signal approximation error within $10 \%$ ? What is the corresponding amplitude $V_{o m}$ of the output? Is the FET operating at all times in the active region?
image_name:(a)
description:
[
name: Vi, type: VoltageSource, ports: {Np: vi, Nn: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: vi, Nn: g1}
name: RF, type: Resistor, value: 10MΩ, ports: {N1: g1, N2: d1}
name: RD, type: Resistor, value: 12kΩ, ports: {N1: 9V, N2: d1}
name: C2, type: Capacitor, value: C2, ports: {Np: d1, Nn: vo}
name: M1, type: NMOS, ports: {S: GND, D: d1, G: g1}
]
extrainfo:This is a common-source (CS) amplifier with feedback bias. The input signal vi is capacitively coupled through C1 to the gate of the NMOS M1. The feedback resistor RF provides DC biasing. The drain of M1 is connected to RD and the output is taken across C2. The circuit is powered by a 9V supply.
image_name:(b)
description:
[
name: Vi, type: VoltageSource, ports: {Np: vi, Nn: GND}
name: RD, type: Resistor, value: 12 kΩ, ports: {N1: vo, N2: GND}
name: RF, type: Resistor, value: 10 MΩ, ports: {N1: vi, N2: vo}
name: ro, type: Resistor, value: 12 kΩ, ports: {N1: vo, N2: GND}
name: gmvi, type: VoltageControlledCurrentSource,value: gmvi, ports: {NP: vo, Nn: GND}
]
extrainfo:The circuit is a common-source amplifier with feedback biasing. It uses an NMOS transistor (M1) with a feedback resistor (RF) and coupling capacitors (C1 and C2). The input signal is applied at vi and the output is taken from vo. The drain resistor RD is connected to a 9V supply. The circuit is designed to amplify small AC signals.

FIGURE 3.56 (a) CS amplifier with feedback bias, and (b) its ac equivalent.

#### Solution

(a) We have $V_{G S}=V_{D S}=V_{D D}-R_{D} I_{D}=9-12 I_{D}$, so $V_{O V}=V_{G S}-V_{t}=7-12 I_{D}$. Letting

$$
I_{D}=\frac{1}{2}\left(7-12 I_{D}\right)^{2}
$$

and solving as usual, we get $I_{D}=0.5 \mathrm{~mA}$ and $V_{D S}=3.0 \mathrm{~V}$. Moreover, $g_{m}=$ $1.0 \mathrm{~mA} / \mathrm{V}$ and $r_{o}=60.6 \mathrm{k} \Omega$.

To find the small-signal parameters we need to work explicitly with the small-signal equivalent of Fig. 3.56b. (Note that the presence of the feedback resistance $R_{F}$ precludes us from recycling the results of Fig. 3.50!) Given that $R_{o}$ is the output-node resistance in the limit $v_{i} \rightarrow 0$, we find, by inspection,

$$
R_{o}=R_{F} / / r_{o} / / R_{D}=10,000 / / 60.6 / / 12=10 \mathrm{k} \Omega
$$

To find $a_{o c}$ we apply KCL at the output node, and get

$$
\frac{v_{i}-v_{o}}{R_{F}}=g_{m} v_{i}+\frac{v_{o}}{r_{o}}+\frac{v_{o}}{R_{D}}
$$

Collecting terms and solving for the ratio $v_{o} / v_{i}$ gives

$$
a_{o c}=\frac{v_{o}}{v_{i}}=-\left(g_{m}-\frac{1}{R_{F}}\right) R_{o} \cong-g_{m} R_{o}=-1 \times 10=-10 \mathrm{~V} / \mathrm{V}
$$

where we have exploited the fact that $1 / R_{F} \ll g_{m}$. The input resistance is found as $R_{i}=v_{i} / i_{i}$, where $i_{i}=\left(v_{i}-v_{o}\right) / R_{F}$. Substituting $v_{o}=a_{o c} \times v_{i}$ and collecting gives $i_{i}=v_{i}\left(1-a_{o c}\right) / R_{F}$. Consequently,

$$
R_{i}=\frac{v_{i}}{i_{i}}=\frac{R_{F}}{1-a_{o c}}=\frac{10 \times 10^{6}}{1-(-10)}=\frac{10 \times 10^{6}}{11}=0.91 \mathrm{M} \Omega
$$

Interestingly enough, when reflected to the input, the feedback resistance $R_{F}$ gets divided by the factor $\left(1-a_{o c}\right)$, a phenomenon known as the Miller effect (more on this in Chapters 6 and 7).
(b) For an error of not more than $10 \%$, Eq. (3.57) requires that we keep $V_{i m} \leq\left(2 V_{O V}\right) / 10=(2 \times 1) / 10=0.2 \mathrm{~V}$. The corresponding output amplitude is $V_{o m} \cong\left|a_{o c}\right| \times V_{i m}=10 \times 0.2=2 \mathrm{~V}$. The dc voltage at the drain is $V_{D}=3 \mathrm{~V}$, and operation in the active region, or saturation, is maintained all the way down to $V_{D}=V_{O V}=1 \mathrm{~V}$. The maximum allowed downswing for the drain is thus 2 V , indicating that our amplifier will just barely accommodate an input with $0.2-\mathrm{V}$ of peak amplitude.

### Quick Estimate for the Gain of the CS Configuration

In daily practice an engineer often needs to come up with a quick if rough estimate for the gain of a MOSFET amplifier. The above examples reveal that the CS configuration tends to give $a_{o c}=-g_{m} R_{o}$. In discrete designs $R_{o}$ is usually dominated by $R_{D}$, indicating that we can approximate $a_{o c} \cong-g_{m} R_{D}$. Letting $g_{m}=2 I_{D} / V_{O V}$, we can estimate the unloaded gain of a discrete-type CS amplifier as

$$
\begin{equation*}
a_{o c} \cong-g_{m} R_{D}=-\frac{R_{D} I_{D}}{0.5 V_{O V}} \tag{3.75a}
\end{equation*}
$$

In words, the magnitude of the unloaded gain of a CS amplifier is the ratio of the voltage-drop across $R_{D}$ to half the overdrive $V_{O V}$. For the circuit of Example 3.30, Eq. (3.75a) gives the estimate $a_{o c} \cong-2(10 \times 1) / 2=-10 \mathrm{~V} / \mathrm{V}$, in fair agreement with the calculated value of $-9.09 \mathrm{~V} / \mathrm{V}$. Likewise, the estimates for Examples 3.31 and 3.32 are $a_{o c} \cong-2(10 \times 0.4) / 1=-8 \mathrm{~V} / \mathrm{V}$, and $a_{o c} \cong-2(12 \times 0.5) / 1=-12 \mathrm{~V} / \mathrm{V}$. Both compare reasonably well with the calculated values of $-7.4 \mathrm{~V} / \mathrm{V}$ and $-10 \mathrm{~V} / \mathrm{V}$.

The student already familiar with bipolar junction transistors (BJTs) will note that the expression $a_{o c} \cong-R_{D} I_{D} /\left(0.5 V_{O V}\right)$ for the CS amplifier is similar to the expression $a_{o c} \cong-R_{C} I_{C} / V_{T}$ for the common-emitter (CE) amplifier. However, considering that $V_{T}=26 \mathrm{mV}$, while $0.5 V_{O V}$ is typically on the order of a volt or so, it is apparent that under similar biasing conditions the gain available from a FET tends to be much lower than that available from a BJT. This stems from the notoriously lower transconductance of FETs. In IC design the gain of the CS configuration is boosted by using a current source in place of $R_{D}$. As we shall see in Chapter 4 , such a source is implemented with a $p$ MOSFET.

#### Exercise 3.3

Show that if we take also $r_{o}$ into account, then Eq. (3.75a) becomes

$$
\begin{equation*}
a_{o c}=-\frac{R_{D} I_{D}}{0.5 V_{O V}} \times \frac{1}{1+\lambda R_{D} I_{D}} \tag{3.75b}
\end{equation*}
$$

### The Common-Source with Source-Degeneration (CS-SD) Configuration

The circuit of Fig. 3.57 is similar to the CS amplifier of Fig. 3.52, except for the presence of the unbypassed resistance $R_{S}$ in series with the FET's source. Turning to its ac equivalent of Fig. 3.58 we note that, aside from the presence of the input voltage
image_name:Figure 3.57
description:
[
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: vi}
name: RG, type: Resistor, value: RG, ports: {N1: g1, N2: GND}
name: RD, type: Resistor, value: RD, ports: {N1: d1, N2: VDD}
name: RL, type: Resistor, value: RL, ports: {N1: vo, N2: GND}
name: RS, type: Resistor, value: RS, ports: {N1: s1, N2: P}
name: C1, type: Capacitor, value: C1, ports: {Np: vi, Nn: g1}
name: C2, type: Capacitor, value: C2, ports: {Np: d1, Nn: vo}
name: C3, type: Capacitor, value: C3, ports: {Np: P, Nn: GND}
name: M1, type: NMOS, ports: {S: s1, D: d1, G: g1}
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: ID, type: CurrentSource, value: ID, ports: {Np: P, Nn: VSS}
]
extrainfo:The circuit is a common-source amplifier with source degeneration. It uses an NMOS transistor M1 with a source resistor RS for degeneration, improving linearity and stability. The input signal Vsig is AC-coupled through C1, and the output is AC-coupled through C2. The load is connected at the output node vo.

FIGURE 3.57 The common-source with source-degeneration (CS-SD) amplifier.
divider and output load, the circuit is identical to that of Fig. 3.50. We can again reuse the relationships developed there, provided we let $v_{s} / v_{g} \rightarrow v_{o} / v_{i}$. By inspection,

$$
\begin{equation*}
R_{i}=R_{G} \tag{3.76a}
\end{equation*}
$$

As we know, one of the effects of the source-degeneration resistance $R_{S}$ is to raise the resistance seen looking into the drain from $r_{o}$ to $R_{d} \cong r_{o}\left(1+g_{m} R_{S}\right)$. Consequently, we now have

$$
\begin{equation*}
R_{o}=R_{D} / / R_{d} \cong R_{D} / /\left[r_{o}\left(1+g_{m} R_{S}\right)\right] \cong R_{D} \tag{3.76b}
\end{equation*}
$$

The unloaded voltage gain, defined as the ratio $v_{o} / v_{i}$ in the limit $R_{L} \rightarrow \infty$, is now

$$
\begin{equation*}
a_{o c}=-\frac{g_{m} R_{D}}{1+g_{m} R_{S}+\left(R_{D}+R_{S}\right) / r_{o}} \cong-\frac{g_{m} R_{D}}{1+g_{m} R_{S}} \tag{3.77}
\end{equation*}
$$

image_name:FIGURE 3.58
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: vi}
name: RG, type: Resistor, value: RG, ports: {N1: G1, N2: GND}
name: M1, type: NMOS, ports: {S: S1, D: Vo, G: G1}
name: RD, type: Resistor, value: RD, ports: {N1: Vo, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: vo, N2: GND}
name: RS, type: Resistor, value: RS, ports: {N1: S1, N2: GND}
]
extrainfo:The circuit is an AC equivalent of a common-source (CS) amplifier with source degeneration (SD). It includes a voltage source Vsig and several resistors (Rsig, Ri, RG, RD, Ro, RL, RS) connected to an NMOS transistor (M1). The presence of RS provides negative feedback, reducing the gain.

FIGURE 3.58 Ac equivalent of the CS-SD amplifier of Fig. 3.57.
where we have exploited the fact that in discrete designs we have $\left(R_{D}+R_{S}\right) \ll r_{o}$. Comparing Eq. (3.77) with Eq. (3.74) we observe that the presence of $R_{S}$ causes $a_{o c}$ to drop from approximately $-g_{m} R_{D}$ to approximately $-g_{m} R_{D} /\left(1+g_{m} R_{S}\right)$. This magnitude reduction stems from the negative-feedback action, or degenerative action, provided by $R_{S}$. Rewriting in the alternative form

$$
\begin{equation*}
a_{o c} \cong-\frac{R_{D}}{1 / g_{m}+R_{S}} \tag{3.78}
\end{equation*}
$$

provides us with a useful rule of thumb for a quick estimation of the gain of the CS-SD configuration:

The unloaded voltage gain from gate to drain is the (negative of the) ratio of the drain resistance to the total source resistance

Having obtained expressions for $R_{i}, R_{o}$, and $a_{o c}$, we can apply Eq. (3.71) to find the signal-to-load gain.
(a) Investigate the effect of inserting a source-degeneration resistance $R_{S}=2 \mathrm{k} \Omega$

EXAMPLE 3.33 in the CS circuit of Example 3.30, and thus turning it into a CS-SD circuit of the type of Fig. 3.57.
(b) Estimate $R_{S}$ for an unloaded gain of $-2 \mathrm{~V} / \mathrm{V}$.

#### Solution

(a) All dc voltages and dc current remain the same, and so do $g_{m}(=1 \mathrm{~mA} / \mathrm{V})$ and $r_{o}(=100 \mathrm{k} \Omega)$. The insertion of $R_{S}=2 \mathrm{k} \Omega$ in the circuit has the following effects:

- $R_{d}$ increases from $100 \mathrm{k} \Omega$ to $100(1+1 \times 2)=300 \mathrm{k} \Omega$.
- $R_{o}$ increases from $9.09 \mathrm{k} \Omega$ to $10 / / 300=9.68 \mathrm{k} \Omega$.
- $a_{o c}$ drops (or degenerates) from $-9.09 \mathrm{~V} / \mathrm{V}$ to $-(1 \times 9.68) /(1 / 1+1 \times 2)=$ -3.23 V/V.
Using Eq. (3.71), we find that $v_{o}$ changes to

$$
\begin{aligned}
v_{o} & =\left[\frac{1}{0.1+1}(-3.23) \frac{30}{9.68+30}\right] v_{s i g}=-2.22 \times(100 \mathrm{mV}) \cos \omega t \\
& =(222 \mathrm{mV}) \cos \left(\omega t-180^{\circ}\right)
\end{aligned}
$$

(b) Use Eq. (3.78) to impose $-2 \cong-10 /\left(1 / 1+R_{S}\right)$. This yields $R_{S}=4 \mathrm{k} \Omega$.

### Capacitor Selection

Before leaving the subject of discrete MOSFET amplifiers, we wish to address the issue of how to go about selecting the various capacitances in the circuits discussed above. As the signal source is turned on, we want each capacitance $C$ to act as an ac short at the source's frequency $f_{s i g}$. Physically, this requires that we select $C$ large enough to prevent it from charging/discharging appreciably in response to the ac signal alternations.

As we know, the impedance presented by a capacitance $C$ at the signal frequency $f_{s i g}$ is $Z_{C}\left(j f_{s i g}\right)=1 /\left(j 2 \pi f_{s i g}\right)$. For this capacitance to act effectively as an ac short at $f_{s i g}$, its impedance must be such that

$$
\left|Z_{C}\left(j f_{s i g}\right)\right| \ll R_{e q}
$$

where $R_{e q}$ is the equivalent resistance seen by $C$ itself. This condition is rephrased in terms of $C$ as

$$
\begin{equation*}
C \gg \frac{1}{2 \pi R_{e q} f_{s i g}} \tag{3.79}
\end{equation*}
$$

If the circuit is designed to operate over a range of frequencies, then we must use the lowest frequency $f_{\text {sig(min) }}$ in the above condition. It is good practice to use $C \cong 10 /\left(2 \pi R_{e q} f_{\text {sig(min) }}\right)$.

EXAMPLE 3.34 Specify suitable capacitances in the CS amplifier of Fig. 3.54 for operation over the audio range.

#### Solution

The audio range extends from 20 Hz to 20 kHz , so $f_{\text {sig(min) }}=20 \mathrm{~Hz}$.

- For $C_{1}$ we have $R_{e q 1}=R_{s i g}+R_{i}=0.1+1=1.1 \mathrm{M} \Omega$, so $C_{1} \gg 1 /[2 \pi \times 1.1 \times$ $\left.10^{6} \times 20\right) \cong 7 \mathrm{nF}$ (use 100 nF ).
- For $C_{2}$ we have $R_{e q 2}=R_{o}+R_{L}=10.7+30=40.7 \mathrm{k} \Omega$, so $C_{2} \gg 1 /[2 \pi \times$ $\left.40.7 \times 10^{3} \times 20\right) \cong 0.2 \mu \mathrm{~F}(2 \mu \mathrm{~F})$.
- For $C_{3}$ we have $R_{e q 3}=R_{s} \cong 1 / g_{m}=1 \mathrm{k} \Omega$, so $C_{3} \gg 1 /\left[2 \pi \times 10^{3} \times 20\right) \cong 8 \mu \mathrm{~F}$ ( $100 \mu \mathrm{~F}$ ).

## 3.9 MOSFET VOLTAGE AND CURRENT BUFFERS

In this section we examine the two remaining single-FET amplifier configurations of interest, namely, the common-drain and the common-gate configurations. We shall see that these configurations find application as voltage buffers and current buffers, respectively.

### The Common-Drain (CD) Configuration

The common-drain (CD) amplifier receives the input at the gate and delivers the output at the source. The circuit realization of Fig. 3.59a utilizes the same biasing scheme as the CS amplifier of Fig. 3.52. Turning to its ac equivalent of Fig. 3.59b, we observe that it is similar to that of Fig. 3.50, but with $R_{D}=0$. Instead of repeating the small-signal analysis routine all over again, we simply reuse the results tabulated there, but after letting $R_{D} \rightarrow 0$ and re-labeling resistors and signals as $R_{S} \rightarrow R_{L}$, $R_{s} \rightarrow R_{o}$, and $v_{s} / v_{g} \rightarrow v_{o} / v_{i}$. This yields the following results:

$$
R_{i}=R_{G} \quad R_{o}=\frac{r_{o}}{1+g_{m} r_{o}}=\frac{1}{g_{m}} / / r_{o}
$$

image_name:(a)
description:
[
name: Vsig, type: VoltageSource, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: vi}
name: C1, type: Capacitor, value: C1, ports: {Np: vi, Nn: g1}
name: RG, type: Resistor, value: RG, ports: {N1: g1, N2: GND}
name: M1, type: NMOS, ports: {S: s1, D: VDD, G: g1}
name:    ID, type: CurrentSource, value: ID, ports: {Np: s1, Nn: VSS}
name: C2, type: Capacitor, value: C2, ports: {Np: s1, Nn: vo}
name: RL, type: Resistor, value: RL, ports: {N1: vo, N2: GND}
]
extrainfo:The circuit diagram (a) is a common-drain (CD) configuration. The NMOS transistor M1 is connected with its source at node s1, drain at node g1, and gate at node g1. The input voltage is applied at node vi, and the output voltage is taken from node vo. This configuration is used for impedance matching and voltage buffering.
image_name:(b)
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: vi}
name: RG, type: Resistor, value: RG, ports: {N1: vi, N2: GND}
name: M1, type: NMOS, ports: {S: GND, D: vo, G: vi}
name: ID, type: CurrentSource, value: ID, ports: {Np: s1, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: vo, Nn: GND}
name: RL, type: Resistor, value: RL, ports: {N1: vo, N2: GND}
name: Rg, type: Resistor, value: Rg, ports: {N1: vi, N2: GND}
]
extrainfo:This is a common-drain (CD) configuration circuit. The NMOS transistor is used for amplification with the output taken from the source. The circuit includes a voltage source, resistors, and capacitors for signal processing. The unloaded voltage gain is given by a_oc = 1/(1 + 1/(gm * ro)) in the limit RL -> infinity.

FIGURE 3.59 (a) The common-drain (CD) configuration, and (b) its ac equivalent.

$$
v_{o}=\frac{g_{m} R_{L}}{1+g_{m} R_{L}+R_{L} / r_{o}} v_{i}
$$

In the limit $R_{L} \rightarrow \infty$ we get

$$
v_{o}=\frac{g_{m}}{g_{m}+1 / r_{o}} v_{i}=\frac{1}{1+1 /\left(g_{m} r_{o}\right)} v_{i}
$$

But, according to Eq. (3.70), the ratio $v_{o} / v_{i}$ in the limit $R_{L} \rightarrow \infty$ is the unloaded voltage gain, so

$$
\begin{equation*}
a_{o c}=\frac{1}{1+1 /\left(g_{m} r_{o}\right)} \tag{3.81}
\end{equation*}
$$

Since in general $g_{m} r_{o} \gg 1$, the unloaded gain from gate to source is fairly close to unity. Physically, the source voltage $v_{s}$ follows the gate voltage $v_{g}$ closely, this being the reason why the CD amplifier is also called source follower. Even though not much of a winner as a voltage amplifier, the CD configuration offers the advantages of potentially high input resistance and low output resistance, which makes it suited to applications as a voltage buffer, either to reduce inter-stage loading, or to equip a CS amplifier with low output resistance. Having obtained expressions for $R_{i}, R_{o}$, and $a_{o c}$, we can now apply Eq. (3.71) to find the signal-to-load gain.
(a) In the circuit of Fig. 3.59, let $V_{D D}=-V_{S S}=10 \mathrm{~V}, I_{D}=1 \mathrm{~mA}$, and $R_{G}=$

#### ExAMPLE 3.35

$5 \mathrm{M} \Omega$, and let the FET have $V_{t}=1.0 \mathrm{~V}, k=0.5 \mathrm{~mA} / \mathrm{V}^{2}$, and $\lambda=0.01 \mathrm{~V}^{-1}$. Assuming $R_{s i g}=0.1 \mathrm{M} \Omega, R_{L}=10 \mathrm{k} \Omega$, and

$$
v_{s i g}=5.0 \mathrm{~V}+(1.0 \mathrm{~V}) \cos \omega t
$$

find all node voltages in the circuit, express each of them as the sum of its dc and ac component, in the manner of Eq. (3.48), and show them explicitly in the circuit.
(b) Check that the FET satisfies the small-signal approximation condition of Eq. (3.57).

#### Solution

(a) We have $g_{m}=1 \mathrm{~mA} / \mathrm{V}, r_{o}=100 \mathrm{k} \Omega, 1 / g_{m}=1 \mathrm{k} \Omega$, and $g_{m} r_{o}=100$. Consequently,

$$
\begin{aligned}
& R_{i}=R_{G}=5 \mathrm{M} \Omega \quad R_{o}=\frac{1}{g_{m}} / / r_{o} \cong \frac{1}{g_{m}}=1 \mathrm{k} \Omega \\
& a_{o c}=\frac{1}{1+1 /\left(g_{m} r_{o}\right)}=\frac{1}{1+1 / 100}=0.99 \mathrm{~V} / \mathrm{V}
\end{aligned}
$$

(As expected, $R_{i}$ is high, $R_{o}$ is low, and $a_{o c}$ is close to unity.) Moreover, by the voltage divider rule, we have $v_{i}=[5 /(0.1+5)] v_{s i g}=(0.980 \mathrm{~V}) \cos \omega t$. Finally,

$$
\begin{aligned}
v_{o} & =\left[\frac{5}{0.1+5}(0.99) \frac{10}{1+10}\right] v_{s i g}=0.882 \times(1.0 \mathrm{~V}) \cos \omega t \\
& =(0.882 \mathrm{~V}) \cos \omega t
\end{aligned}
$$

The node voltages are shown in Fig. 3.60. The reader is encouraged to verify each of them in detail.
image_name:FIGURE 3.60
description:
[
name: V, type: VoltageSource, value: 5.0 V + (1.0 V)cos ωt, ports: {Np: V, Nn: GND}
name: R1, type: Resistor, value: 0.1 MΩ, ports: {N1: V, N2: X1}
name: C1, type: Capacitor, value: C1, ports: {Np: X1, Nn: X2}
name: NMOS1, type: NMOS, ports: {S: X3, D: 10V, G: X2}
name: I1, type: CurrentSource, value: 1 mA, ports: {Np: X4, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: X3, Nn: X5}
name: R4, type: Resistor, value: 10 kΩ, ports: {N1: X5, N2: GND}
]
extrainfo:The circuit is a common-drain (source follower) amplifier using an NMOS transistor. It is biased with a DC voltage source and a current source, and AC coupled with capacitors C1 and C2. The input voltage is applied at the gate, and the output is taken from the source of the NMOS.

FIGURE 3.60 Circuit of Example 3.35, showing the $d c$ and ac component of each node voltage.
(b) For the FET we have $v_{g s}=v_{i}-v_{o} \cong(98 \mathrm{mV}) \cos \omega t$. Considering that $V_{O V}=$ 2 V , so that $2 V_{O V}=4 \mathrm{~V}$, we have $0.098 \ll 4$, thus confirming the validity of the small-signal approximation.
Remark: Even though neither $v_{i}$ nor $v_{o}$ can be regarded as small signals in this circuit, $v_{g s}$ nevertheless is! The reason for the CD amplifier's ability to handle linearly even signals that are not strictly of the small-signal type stems from the negative feedback action (more in Chapter 7) provided by the source resistance (in this case $R_{L}$ ). Indeed, $R_{L}$ develops a voltage $v_{o}$ close to $v_{i}$ to yield the small-signal difference $v_{g s}=v_{i}-v_{o}$.

#### ExAMPLE 3.36
Figure 3.61 shows a single-supply source follower. To prevent the follower from loading the signal source appreciably, $R_{1}$ and $R_{2}$ have been chosen so that $R_{1} / / R_{2} \gg R_{\text {sig }}$. As usual, the function of $R_{S}$ is to establish the bias current $I_{D}$. Assuming $V_{t}=1.0 \mathrm{~V}$, $k=0.625 \mathrm{~mA} / \mathrm{V}^{2}$, and $\lambda=0.025 \mathrm{~V}^{-1}$, find the small-signal resistances $R_{i}$ and $R_{o}$, and estimate the signal-to-load gain.
image_name:Figure 3.61
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: 0.2 MΩ, ports: {N1: Vsig, N2: vi}
name: R1, type: Resistor, value: 10 MΩ, ports: {N1: 12V, N2: G1}
name: R2, type: Resistor, value: 20 MΩ, ports: {N1: G1, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: vi, Nn: G1}
name: M1, type: NMOS, ports: {S: s1, D: 12V, G: G1}
name: Rs, type: Resistor, value: 4 kΩ, ports: {N1: s1, N2: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: s1, Nn: vo}
name: RL, type: Resistor, value: 5 kΩ, ports: {N1: vo, N2: GND}
]
extrainfo:The circuit is a single-supply source follower (common drain amplifier) with an NMOS transistor. It is designed to prevent loading the signal source by choosing R1 and R2 such that R1||R2 >> Rsig. The voltage source Vsig provides the input signal. The resistors Rs and RL set the bias current and load, respectively. Capacitors C1 and C2 are coupling capacitors for the input and output.

FIGURE 3.61 Single-supply CD amplifier of Example 3.36.

#### Solution

Proceeding as usual, but with $\lambda=0$ to facilitate our dc calculations, we find $I_{D}=1.25 \mathrm{~mA}, 1 / g_{m}=0.8 \mathrm{k} \Omega, r_{o}=32 \mathrm{k} \Omega$, and $g_{m} r_{o}=40$. Referring to the ac equivalent of Fig. 3.62 we find, by inspection,
image_name:FIGURE 3.62
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: vi}
name: R1, type: Resistor, value: R1, ports: {N1: g1, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: g1, N2: GND}
name: Rg, type: Resistor, value: Rg, ports: {N1: g1, N2: GND}
name: M1, type: NMOS, ports: {S: vo, D: GND, G: g1}
name: Rs, type: Resistor, value: Rs, ports: {N1: Vo, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: vo, N2: GND}
]
extrainfo:This is an AC equivalent circuit of a single-supply common-drain (CD) amplifier. The input is provided through Vsig and Rsig, with coupling through Ri. The transistor M1 is configured as a source follower, providing output at Vo. The resistors R1, R2, and Rg are part of the biasing network. Rs and Ro set the output impedance, and RL is the load resistor.

FIGURE 3.62 Ac equivalent of the circuit of Fig. 3.61.
We also have $R_{s}=\left(1 / g_{m}\right) / / r_{o}=0.8 / / 32=0.78 \mathrm{k} \Omega$, so we can write, by inspection,

$$
R_{o}=R_{s} / / R_{S}=0.78 / / 4=0.65 \mathrm{k} \Omega
$$

Finally, the source-to-load gain is

$$
\frac{v_{o}}{v_{s}}=\frac{6.7}{0.2+6.7} \times \frac{1}{1+1 / 40} \times \frac{5}{0.65+5}=0.838 \mathrm{~V} / \mathrm{V}
$$

### The Common-Gate (CG) Configuration

The common-gate (CG) amplifier receives the input at the source and delivers the output from the drain. Since the resistance seen looking into the source is generally small ( $R_{s} \cong 1 / g_{m}$ ), the natural input signal for this configuration is a current, $i_{s i g}$. Also, since the resistance seen looking into the drain is generally large ( $R_{d}=r_{o}$, or even $R_{d} \gg r_{o}$ if there is sufficient source degeneration), the natural output signal is also a current, $i_{o}$. Just like the CD configuration approximates a voltage buffer, which ideally has $R_{i} \rightarrow \infty, R_{o} \rightarrow 0$, and $v_{o} / v_{s i g} \rightarrow 1 \mathrm{~V} / \mathrm{V}$, the CG configuration approximates a current buffer, which ideally has

$$
R_{i} \rightarrow 0 \quad R_{o} \rightarrow \infty \quad \frac{i_{o}}{i_{s i g}} \rightarrow 1 \mathrm{~A} / \mathrm{A}
$$

The CG amplifier is shown in Fig. 3.63a, where the signal source is now modeled with a Norton equivalent. As we turn to the ac equivalent of Fig. $3.63 b$ we note its similarity to the generalized circuit of Fig. 3.50. We can again reuse the relationships developed there, provided we let $R_{S} \rightarrow R_{s i g}, R_{D} \rightarrow R_{L}, R_{s} \rightarrow R_{i}$, and $R_{d} \rightarrow R_{o}$. The results are

$$
\begin{equation*}
R_{i}=\left(\frac{1}{g_{m}} / / r_{o}\right)+\frac{R_{L}}{1+g_{m} r_{o}} \tag{3.82}
\end{equation*}
$$

and

$$
\begin{equation*}
R_{o}=r_{o}\left(1+g_{m} R_{s i g}\right)+R_{s i g} \tag{3.83}
\end{equation*}
$$

The input resistance $R_{i}$ forms a current divider with the signal resistance $R_{s i g}$, so

$$
i_{i}=\frac{R_{s i g}}{R_{s i g}+R_{i}} i_{s i g}
$$

image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: p1, D: d1, G: GND}
name: R_L, type: Resistor, value: R_L, ports: {N1: VDD, N2: d1}
name: R_sig, type: Resistor, value: R_sig, ports: {N1: p2, N2: GND}
name: C_1, type: Capacitor, value: C_1, ports: {Np: p2, Nn: p1}
name: i_sig, type: CurrentSource, value: i_sig, ports: {Np: GND, Nn: p2}
name: I_D, type: CurrentSource, value: I_D, ports: {Np: p1, Nn: VSS}
]
extrainfo:The circuit represents a common-gate (CG) amplifier configuration. It includes an NMOS transistor (M1) with its gate connected to ground, a load resistor (R_L) connected to VDD, and a signal resistor (R_sig) at the input. The input current source (i_sig) is connected to ground, and the output is taken across R_o. The circuit is designed for analyzing current gain in the CG amplifier.
image_name:(b)
description:
[
name: M1, type: NMOS, ports: {S: s1, D: d1, G: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: S1, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: VDD, N2: d1}
name: isig, type: CurrentSource, value: isig, ports: {Np: S1, Nn: GND}
]
extrainfo:This circuit is a common-gate amplifier configuration. It uses an NMOS transistor (M1) with a load resistor (RL) and a source resistor (Rsig). The input current source (isig) drives the circuit, and the output is taken across the load resistor (Ro). The circuit also includes a capacitor (C1) for coupling and a resistor (Ri) for input resistance.

FIGURE 3.63 (a) The common-gate (CG) amplifier, and (b) its ac equivalent.

Since the gate current is zero, KCL gives $i_{o}=i_{i}$. Combining with Eq. (3.82) we obtain, after suitable algebraic manipulation, the signal-to-load current gain

$$
\begin{equation*}
\frac{i_{o}}{i_{s i g}}=\frac{1}{1+\frac{r_{o}+R_{L}}{\left(1+g_{m} r_{o}\right) R_{s i g}}} \tag{3.84}
\end{equation*}
$$

It is apparent that this gain is less than (though close to) unity. The CG configuration is particularly useful when its signal input is supplied by the drain of another FET. The resulting two-transistor configuration, known as the cascode configuration, enjoys advantages of speed and flexibility that make it particularly suited to integratedcircuit realizations, as we shall see in Chapters 4 and 6.
(a) In the circuit of Fig. $3.63 a$ let $V_{D D}=-V_{S S}=12 \mathrm{~V}, I_{D}=1 \mathrm{~mA}$, and $R_{s i g}=50 \mathrm{k} \Omega$, and let the FET have the same parameters as in Example 3.35 $\left(V_{t}=1.0 \mathrm{~V}, k=0.5 \mathrm{~mA} / \mathrm{V}^{2}\right.$, and $\left.\lambda=0.01 \mathrm{~V}^{-1}\right)$. Estimate $R_{i}, R_{o}$, and $i_{o} / i_{s i g}$ if $R_{L}=0$. Comment on your findings.
(b) Repeat if $R_{L}=10 \mathrm{k} \Omega$, and comment.

#### Solution

(a) By Eq. (3.82) through (3.84) we have

$$
\begin{aligned}
& R_{i} \cong 1 / / 100=0.99 \mathrm{k} \Omega \text { (low) } \\
& R_{o}=100(1+1 \times 50)+50=5.15 \mathrm{M} \Omega \text { (high) } \\
& \frac{i_{o}}{i_{s i g}}=\frac{1}{1+\frac{100}{(1+100) 50}}=0.980 \mathrm{~A} / \mathrm{A} \text { (close to unity) }
\end{aligned}
$$

(b) Recalculating with $R_{L}=10 \mathrm{k} \Omega$ we get

$$
\begin{aligned}
& R_{i} \cong(1 / / 100)+10 / 101=1.09 \mathrm{k} \Omega \quad R_{o}=5.15 \mathrm{M} \Omega \\
& \frac{i_{o}}{i_{s i g}}=\frac{1}{1+\frac{100+10}{101 \times 50}}=0.979 \mathrm{~A} / \mathrm{A}
\end{aligned}
$$

The presence of $R_{L}=10 \mathrm{k} \Omega$ has no effect on $R_{o}$. However, it causes a slight increase in $R_{i}$ and a slight drop in gain.

### The CG Configuration as a Voltage Amplifier

Even though the most common application of the CG configuration is as a current buffer, there are situations in which it is used as a voltage amplifier with gain $v_{d} / v_{s}$. Considering that $v_{d}=-g_{m}\left(R_{L} / / r_{o}\right) v_{g s}=-g_{m}\left(R_{L} / / r_{o}\right)\left(v_{g}-v_{s}\right)$, and that the CG configuration has $v_{g}=0$, we get

$$
\begin{equation*}
\frac{v_{d}}{v_{s}}=+g_{m}\left(R_{L} / / / r_{o}\right) \tag{3.85}
\end{equation*}
$$

In words, the voltage gain of the CG configuration has the same magnitude but opposite polarity as that of the CS configuration. The other major difference is in the input resistance, which is $\infty$ in the CS case, but generally low in the CG case. For the circuit of Example $3.37 b$ this voltage gain is $v_{d} / v_{s}=1 \times(10 / / 100) \cong+9.1 \mathrm{~V} / \mathrm{V}$. In the limit $R_{L} \rightarrow \infty$ this gain tends to $g_{m} r_{o}=1 \times 100=100 \mathrm{~V} / \mathrm{V}$ (more on this in Chapter 4).

## 3.10 THE CMOS INVERTER/AMPLIFIER

A simple yet most elegant and useful circuit configuration, the CMOS inverter/ amplifier is at the basis of a wide variety of contemporary circuitry, both digital and analog. As shown in Fig. 3.64, it consists of an $n$ MOSFET and a $p$ MOSFET with their gates tied together to form the input node, and their drains tied together to form the output node. For each device, body and source are tied together, so there are no body effects. Moreover, the source of the $n$ channel is connected to the lowest potential, and that of the $p$ channel to the highest potential. In our example, these potentials are ground and $V_{D D}$, but other arrangements are possible, such as split power supplies. The circuit is usually implemented with matched FETs, whose parameters we shall concisely express as

$$
\begin{equation*}
k_{p}=k_{n}=k \quad V_{t n}=-V_{t p}=V_{t} \quad \lambda_{n}=\lambda_{p}=\lambda \tag{3.86}
\end{equation*}
$$

Considering that the process transconductance parameter $k_{p}^{\prime}$ is typically 2 to 3 times smaller than its counterpart $k_{n}^{\prime}$, the manufacturer compensates for this imbalance by fabricating the $p$ MOSFET with a $W / L$ ratio 2 to 3 times greater than that of the $n$ MOSFET, thus ensuring matched device transconductance parameters, or $k_{p}=k_{n}$. Moreover, the manufacturer effects suitable doping implants to ensure $\left|V_{t p}\right|=V_{t n}$. Typically, the implant dosages are chosen so that $V_{t} \cong 0.2 V_{D D}$, or $V_{t}=1 \mathrm{~V}$ for $V_{D D}=5 \mathrm{~V}$. Also shown in Fig. 3.64 is the logic symbol used for the inverter, with the power-supply details omitted to reduce cluttering the circuit schematics.
image_name:FIGURE 3.64 Circuit schematic and logic symbol of the CMOS inverter/amplifier
description:The diagram illustrates a CMOS inverter/amplifier circuit schematic alongside its logic symbol representation.

Main Components:
1. **MOSFETs:**
- **Mp (P-channel MOSFET):** Connected to the positive supply voltage $V_{DD}$ with its source terminal at $V_{DD}$ and drain connected to the output $v_O$. The gate terminal is connected to the input $v_I$.
- **Mn (N-channel MOSFET):** Connected to ground with its source terminal at ground and drain connected to the output $v_O$. The gate terminal is also connected to the input $v_I$.

2. **Power Supply:**
- **$V_{DD}$:** The positive supply voltage connected to the source of the P-channel MOSFET.
- **Ground (GND):** Connected to the source of the N-channel MOSFET.

3. **Input and Output:**
- **Input Voltage ($v_I$):** The input signal applied to the gates of both MOSFETs.
- **Output Voltage ($v_O$):** The output signal is taken from the common drain connection of the two MOSFETs.

Flow of Information or Control:
- **Signal Flow:**
- The input voltage $v_I$ controls the state of both MOSFETs.
- As $v_I$ increases from 0 to $V_{DD}$, the N-channel MOSFET (Mn) transitions from cutoff to a conducting state, while the P-channel MOSFET (Mp) transitions from a conducting state to cutoff. This results in a logic inversion at the output $v_O$.

Labels, Annotations, and Key Indicators:
- **$i_D$:** The drain current flowing through the P-channel MOSFET.
- **Logic Symbol:** Depicts the inverter function where the input $v_I$ is inverted to produce the output $v_O$.

Overall System Function:
- The primary function of this CMOS inverter is to invert the input signal. When the input $v_I$ is low, the output $v_O$ is high, and vice versa. This is achieved through complementary switching of the P-channel and N-channel MOSFETs, ensuring efficient logic level inversion with minimal power consumption when the input is static.

FIGURE 3.64 Circuit schematic and logic symbol of the CMOS inverter/amplifier.

### The Voltage Transfer Curve (VTC)

To investigate circuit operation we sweep $v_{I}$ from 0 to $V_{D D}$ and examine the ensuing response $v_{o}$. Keeping in mind that $V_{G S n}=v_{I}$ and $V_{S G p}=V_{D D}-v_{I}$, we make two general observations:

- As $v_{I}$ is swept from 0 to $V_{D D}, M_{n}$ goes from the cutoff state to a highly conductive state, while $M_{p}$ goes from a highly conductive state to the cutoff state, indicating complementary behavior by the FETs.
- With respect to the output $v_{o}, M_{p}$ exerts a pull-up action toward $V_{D D}$, while $M_{n}$ exerts a pull-down action toward ground. As a consequence, $v_{O}$ will assume a value somewhere in between, depending on which pull action prevails.

The plot of $v_{O}$ versus $v_{I}$, called the voltage transfer curve (VTC), is readily visualized via PSpice. Figure 3.65 shows one such example, and Fig. 3.66, top, displays the VTC for the component and device parameter values shown. We make the following considerations:

- For $v_{I} \leq V_{t n}$, or $V_{G S n} \leq 1.0 \mathrm{~V}, M_{n}$ is in cutoff and acts as an open switch. On the other hand, $M_{p}$ is highly conductive because $V_{S G_{p}} \geq 4 \mathrm{~V}$. But, owing to the cutoff state of $M_{n}$, no current can flow through $M_{p}$, forcing it to operate right at the origin of its $i_{D}-v_{S D}$ characteristics, that is, in the ohmic region. The situation is illustrated further in Fig. 3.67a, top, which shows the curves corresponding to $V_{G S n}=0$ and $V_{S G p}=5 \mathrm{~V}$. The operating point $Q_{H}$ lies right at the intersection of the two curves, that is, at $v_{O}=V_{O H}=V_{D D}=5 \mathrm{~V}$ and $i_{D}=0$. The FETs thus act as in Fig. 3.67a, bottom. The $p$-channel resistance pulling $v_{O}$ to $V_{D D}$ is $r_{S D p}=1 /\left[k_{p}\left(V_{S G p}-\left|V_{t p}\right|\right)\right]=1 /[1(5-1)]=0.25 \mathrm{k} \Omega$.
- For $v_{I} \geq V_{D D}-\left|V_{t p}\right|$, or $v_{I} \geq 5-1=4 \mathrm{~V}$, we have the opposite situation to the one just described, namely, $M_{n}$ is highly conductive while $M_{p}$ is in cutoff. As depicted in Fig. 3.67c, top, the operating point $Q_{L}$ lies right at the intersection of the curves corresponding to $V_{G S n}=5 \mathrm{~V}$ and $V_{S G p}=0 \mathrm{~V}$, that is, at $v_{O}=V_{O L}=0 \mathrm{~V}$ and $i_{D}=0$. The FETs now act as in Fig. 3.67c, bottom. The $n$-channel resistance pulling $v_{O}$ to ground is $r_{D S n}=1 /\left[k_{n}\left(V_{G S n}-V_{t n}\right)\right]=0.25 \mathrm{k} \Omega$.
image_name:Figure 3.65
description:
[
name: Mp, type: PMOS, ports: {S: VDD, D: vO, G: vI}
name: Mn, type: NMOS, ports: {S: GND, D: vO, G: vI}
name: VI, type: VoltageSource, value: VI, ports: {Np: vI, Nn: GND}
]
extrainfo:The circuit is a CMOS inverter with a PMOS and NMOS transistor. The PMOS is connected to VDD and the NMOS is connected to GND. The output node is labeled vO, and the input is controlled by a voltage source VI.

$$
\begin{aligned}
& \mathrm{Mn}: k_{n}=1.0 \mathrm{~mA} / \mathrm{V}^{2}, V_{t n}=1.0 \mathrm{~V}, \lambda_{n}=0.05 \mathrm{~V}^{-1} \\
& \mathrm{Mp}: k_{p}=1.0 \mathrm{~mA} / \mathrm{V}^{2}, V_{t p}=-1.0 \mathrm{~V}, \lambda_{p}=0.05 \mathrm{~V}^{-1}
\end{aligned}
$$

FIGURE 3.65 PSpice circuit for the simulation of the CMOS inverter/amplifier.
image_name:FIGURE 3.66
description:The graph in FIGURE 3.66 consists of three plots related to a CMOS inverter/amplifier circuit, each illustrating different parameters as a function of input voltage $v_I$ (in volts).

Top Plot: Output Voltage $v_O$ vs. Input Voltage $v_I$
- **Type of Graph:** Voltage transfer characteristic curve.
- **Axes Labels:**
- **X-axis:** Input voltage $v_I$ (V), ranging from 0 to 5 volts.
- **Y-axis:** Output voltage $v_O$ (V), ranging from 0 to 5 volts.
- **Overall Behavior and Trends:**
- The curve starts at $V_{OH}$ (5 V) when $v_I$ is low, indicating that the PMOS is in the ohmic region and NMOS is in cutoff.
- As $v_I$ increases past $V_{tn}$ (1 V), $v_O$ begins to decrease sharply, indicating the NMOS enters saturation and PMOS enters the triode region.
- In the middle region, both transistors are in saturation, and the output voltage transitions through an intermediate range.
- As $v_I$ approaches $V_{DD} - |V_{tp}|$, the PMOS enters cutoff and NMOS enters the ohmic region, bringing $v_O$ to $V_{OL}$ (0 V).
- **Key Features:**
- $V_{IL}$ and $V_{IH}$ are marked, indicating the input low and high threshold voltages.
- The transition region shows a steep slope, representing high gain.

Middle Plot: Voltage Gain $a$ vs. Input Voltage $v_I$
- **Type of Graph:** Gain characteristic curve.
- **Axes Labels:**
- **X-axis:** Input voltage $v_I$ (V), ranging from 0 to 5 volts.
- **Y-axis:** Voltage gain $a$ (V/V), ranging from -30 to 0.
- **Overall Behavior and Trends:**
- The gain is zero when $v_I$ is at very low or very high values.
- There is a sharp negative peak in gain around the transition region, indicating maximum amplification.
- **Key Features:**
- $V_{IL}$ and $V_{IH}$ are marked, showing the boundaries of significant gain.

Bottom Plot: Current $i_D$ vs. Input Voltage $v_I$
- **Type of Graph:** Current characteristic curve.
- **Axes Labels:**
- **X-axis:** Input voltage $v_I$ (V), ranging from 0 to 5 volts.
- **Y-axis:** Drain current $i_D$ (mA), ranging from 0 to 1.5 mA.
- **Overall Behavior and Trends:**
- The current starts at zero when $v_I$ is low, increases to a peak at $V_m$, and then decreases back to zero as $v_I$ approaches 5 V.
- The peak current $I_m$ is marked, indicating the maximum current flow during the transition.
- **Key Features:**
- The peak current occurs when both transistors are in saturation, maximizing the current flow through the circuit.

FIGURE 3.66 Plots of $v_{0}, a$, and $i_{D}$ versus $v_{l}$ for the CMOS inverter/amplifier of Fig. 3.65.

- As we raise $v_{I}$ just $a$ bit above $V_{t n}\left(=1.0 \mathrm{~V}\right.$ in our example), $M_{n}$ goes into conduction and starts pulling down $v_{O}$. However, as long as $v_{O}$ is still sufficiently high, $M_{n}$ operates in saturation because $v_{D S n}\left(=v_{o}\right)$ is large, and $M_{p}$ operates in the triode region because $v_{S D p}\left(=V_{D D}-v_{o}\right)$ is small.
- By dual reasoning, if we lower $v_{I}$ just a bit below $V_{D D}-\left|V_{t p}\right|(=4 \mathrm{~V}$ in our example), $M_{p}$ goes into conduction and starts pulling up $v_{O}$. However, as long as $v_{O}$ is still sufficiently low, $M_{p}$ operates in saturation and $M_{n}$ operates in the triode region.
- There is a range of $v_{I}$ values over which both FETs operate in saturation. With matched devices, this region is centered at the midpoint voltage $V_{m}=1 / 2 V_{D D}$ ( $=2.5 \mathrm{~V}$ in our example). As depicted in Fig. 3.67b, top, the operating point $Q_{m}$ lies right at the intersection of the curves corresponding to $V_{G S n}=V_{m}(=2.5 \mathrm{~V})$ and
image_name:Q_H
description:The graph labeled 'Q_H' is a current-voltage characteristic plot for a CMOS inverter/amplifier circuit. It shows the relationship between the output voltage \( v_O \) on the x-axis and the drain current \( i_D \) on the y-axis. The x-axis is labeled as 'Output \( v_O \)' and spans from 0 to \( V_{DD} \) (the supply voltage), while the y-axis is labeled 'Current \( i_D \)'.

1. **Type of Graph and Function:**
- This is a characteristic curve graph illustrating the behavior of a CMOS inverter.

2. **Axes Labels and Units:**
- **X-axis:** 'Output \( v_O \)', ranging from 0 to \( V_{DD} \).
- **Y-axis:** 'Current \( i_D \)', representing the drain current.

3. **Overall Behavior and Trends:**
- The graph shows multiple curves representing different gate-source voltage \( V_{GS} \) conditions. These curves illustrate the behavior of the drain current as the output voltage changes.
- The curves are concave and show how the current increases with increasing output voltage until it reaches a peak and then decreases.

4. **Key Features and Technical Details:**
- The point labeled \( Q_H \) represents the operating point when \( V_{GS_n} = V_{OL} \) and \( V_{SG_p} = V_{DD} - V_{OL} \). This is where the NMOS is in saturation, and the PMOS is in the triode region.
- The curves converge at the top and bottom, indicating limits of operation for the MOSFETs.

5. **Annotations and Specific Data Points:**
- The point \( Q_H \) is specifically marked on the graph, indicating a significant operating condition.
- No specific numerical values are provided for the current, but the graph visually indicates the relationship between \( v_O \) and \( i_D \) under different conditions.
image_name:Q_m
description:The graph labeled 'Q_m' is a plot of the current $i_D$ versus the output voltage $v_O$ for a CMOS inverter/amplifier. This is a type of operating point graph, often used to illustrate the behavior of MOSFETs in different regions of operation.

**Axes Labels and Units:**
- The x-axis represents the output voltage $v_O$ and is marked from 0 to $V_{DD}$.
- The y-axis represents the current $i_D$.
- No specific units are provided, but typically in such contexts, $v_O$ is in volts and $i_D$ is in amperes.

**Overall Behavior and Trends:**
- The graph shows multiple curves representing different operating conditions of the MOSFETs.
- The curves are parabolic, indicating the relationship between $i_D$ and $v_O$.
- The central region around $V_m = 2.5 V$ is highlighted, where both MOSFETs operate in saturation.

**Key Features and Technical Details:**
- The operating point $Q_m$ is marked at the intersection of the curves where $V_{GS_n} = V_m$ and $V_{SG_p} = V_{DD} - V_m$.
- At $Q_m$, the coordinates are $v_O = V_m$ and $i_D = I_m$, indicating the midpoint of operation.
- The graph also shows the transition between different regions of operation, such as saturation and triode regions.

**Annotations and Specific Data Points:**
- The midpoint voltage $V_m = 2.5 V$ is annotated.
- The graph includes reference points $Q_H$ and $Q_L$ on either side of $Q_m$, corresponding to high and low output states.
- The curves indicate the current-voltage characteristics for different gate-source voltages.

This graph is crucial for understanding the behavior of the CMOS inverter at various input conditions, particularly at the midpoint voltage where both transistors are in saturation, providing insights into the switching characteristics and amplification behavior of the device.
image_name:Q_L
description:The graph labeled "Q_L" is part of a set of diagrams illustrating the operating points and large-signal models of a CMOS inverter/amplifier. This specific graph is focused on the case where the input voltage $v_{l}$ is equal to the high output voltage $V_{OH}$.

1. **Type of Graph and Function:**
- This is a plot showing the relationship between the drain current $i_D$ and the output voltage $v_O$ for a CMOS inverter.
- The graph is a characteristic curve for the MOSFET devices in the circuit.

2. **Axes Labels and Units:**
- The horizontal axis represents the output voltage $v_O$, ranging from 0 to $V_{DD}$.
- The vertical axis represents the drain current $i_D$.

3. **Overall Behavior and Trends:**
- The graph shows multiple curves representing different gate-source voltages for the PMOS and NMOS transistors.
- The curves are symmetrical and show saturation and triode regions for the transistors.
- At the point $Q_L$, the output voltage $v_O$ is at its minimum value when the input $v_l$ is at $V_{OH}$.

4. **Key Features and Technical Details:**
- The point $Q_L$ is marked on the graph, indicating the specific operating point where $v_O$ is at its lowest.
- The curves indicate the transition between the triode and saturation regions for the MOSFETs.
- The graph illustrates the behavior of the inverter when the PMOS is fully on and the NMOS is off.

5. **Annotations and Specific Data Points:**
- The graph is annotated with $V_{SGP} = V_{DD} - V_{OH}$ and $V_{GSN} = V_{OH}$, indicating the gate-source voltages at this operating point.
- The operating point $Q_L$ corresponds to the conditions when the PMOS is in saturation and the NMOS is off, leading to a high output voltage $v_O$ close to $V_{DD}$.
image_name:(a)
description:
[
name: rSDP, type: Resistor, value: rSDP, ports: {N1: VDD, N2: VOH}
name: SW1, type: Switch, ports: {N1: VOH, N2: GND}
name: V1, type: VoltageSource, ports: {Np: VI, Nn: GND}
]
extrainfo:The circuit diagram (a) shows a simple switch configuration connected to a resistor rSDP between VDD and ground. The switch SW1 is connected in parallel with the resistor. The input voltage VI is applied across the switch. The diagram illustrates a basic CMOS inverter/amplifier configuration used for analyzing different operating points (QH, Qm, QL) of the circuit.
image_name:(b)
description:
[
name: V1, type: VoltageSource, value: V1, ports: {Np: vI, Nn: GND}
name: kP/2(VDD-vI-|Vtp|)^2, type: VoltageControlledCurrentSource, ports: {Np: VDD, Nn: vO}
name: kN/2(vI-Vtn)^2, type: VoltageControlledCurrentSource, ports: {Np: vO, Nn: GND}
name: rop, type: Resistor, value: rop, ports: {N1: VDD, N2: vO}
name: ron, type: Resistor, value: ron, ports: {N1: vO, N2: GND}
]
extrainfo:The circuit diagram (b) represents a CMOS inverter/amplifier configuration with a PMOS and NMOS transistor. The PMOS is controlled by a voltage-controlled current source with a gain factor kP, and the NMOS is controlled by a voltage-controlled current source with a gain factor kN. The resistors rop and ron are connected to the output node vO, which serves as the output of the circuit. The input voltage is applied at node vI, and the circuit is powered by VDD.
image_name:(c)
description:
[
name: rDSn, type: Resistor, value: rDSn, ports: {N1: VOL, N2: GND}
name: SW1, type: Switch, ports: {N1: VOL, N2: GND}
name: VI, type: VoltageSource, ports: {Np: VDD, Nn: VOL}
]
extrainfo:The circuit diagram (c) represents a configuration where a resistor rDSn is connected between VDD and VOL. A switch SW1 connects VOL to GND. The voltage source VI is connected to GND with input voltage VI = VOH.

FIGURE 3.67 Operating points and large-signal models of the CMOS inverter/amplifier for the cases (a) $v_{l}=V_{O L}$, (b) $v_{l}$ near $V_{m}$, and (c) $v_{l}=V_{O H}$.
$V_{S G p}=V_{D D}-V_{m}(=2.5 \mathrm{~V})$. The coordinates of $Q_{m}$ are thus $v_{O}=V_{m}$ and $i_{D}=I_{m}$, where $I_{m}$ is readily found via the $n$ MOSFET expression

$$
\begin{equation*}
I_{m}=\frac{k}{2}\left(V_{m}-V_{t}\right)^{2}\left(1+\lambda V_{m}\right) \tag{3.87}
\end{equation*}
$$

In our example,

$$
I_{m}=\frac{1}{2}(2.5-1)^{2}(1+0.05 \times 2.5)=1.27 \mathrm{~mA}
$$

The FETs now act as in Fig. 3.67b, bottom.
As we know, the slope of the VTC represents voltage gain. Figure 3.66, top, indicates that slope is steepest in the region where both FETs are saturated. Figure 3.66, center, shows the gain $a$ as a function of $v_{I}$. Also shown in Fig. 3.66, bottom, is the current $i_{D}$ drawn from the power supply.

### The CMOS Inverter as a Logic Element

When used as a logic element, the CMOS inverter of Fig. 3.64 offers a number of unique advantages:

- The output swings from rail to rail, or

$$
\begin{equation*}
V_{O L}=0 \mathrm{~V} \quad V_{O H}=V_{D D} \tag{3.88}
\end{equation*}
$$

thus providing maximum signal swing and, hence, the widest noise margins.

- As demonstrated by Fig. 3.66, bottom, the circuit draws zero current in either of its logic states, indicating zero static power dissipation. This is confirmed by the equivalent circuits of Figs. 3.67a and $c$. However, in the course of a transition from one state to the other, the circuit will draw a charge packet from its supply, as per Fig. 3.66, bottom. The more frequent the transitions, the higher the amount of charge drawn per second, indicating that the dynamic power dissipation will tend to increase in proportion to the digital clock frequency.
- As demonstrated by the equivalent circuits of Figs. $3.67 a$ and $c$, the inverter offers fairly low output resistance in either logic state ( $0.25 \mathrm{k} \Omega$ in our example), indicating a relative immunity from output loading as well as output disturbances.
- Since the input node consists of two gate electrodes, each forming the plate of a tiny capacitor, the input resistance is virtually infinite, at least at dc, indicating the absence of static loading when different circuits of the CMOS-inverter type are interconnected together.

The above advantages, along with the small chip area taken up by MOSFETs, explain why nowadays CMOS technology is predominant in digital as well as mixedmode (digital/analog) integrated circuits, especially in battery-powered systems such as notebooks, smart phones, digital cameras, pacemakers, and a wide variety of others.

### The Noise Margins

As we know, the ability of a digital gate to function reliably in the presence of input noise is expressed in terms of its noise margins $N M_{L}=V_{I L}-V_{O L}$ and $N M_{H}=$ $V_{O H}-V_{I H}$, where $V_{I L}$ and $V_{I H}$ are the values of $v_{I}$ at which $a=-1 \mathrm{~V} / \mathrm{V}$, and $V_{O L}$ and $V_{O H}$ are given by Eq. (3.88). Considering the symmetry of the CMOS inverter, we only need to find one of the two, say, $V_{I H}$. Then, we obtain the other as $V_{I L}=V_{D D}-V_{I H}$.

Turning again to Fig. 3.66, top, we observe that $V_{I H}$ is located in the region where $M_{p}$ operates in saturation and $M_{n}$ in the triode region. Imposing $i_{D p(\text { sat })}=i_{D n(\text { triode })}$ yields an equation relating $v_{I}$ and $v_{O}$. For the case of matched FETs this is expressed as

$$
\begin{equation*}
\frac{k}{2}\left(V_{D D}-v_{I}-V_{t}\right)^{2}=k\left[\left(v_{I}-V_{t}\right) v_{O}-\frac{1}{2} v_{o}^{2}\right] \tag{3.89}
\end{equation*}
$$

Differentiating both sides with respect to $v_{I}$ and simplifying gives

$$
-\left(V_{D D}-v_{I}-V_{t}\right)=\left(v_{I}-V_{t}\right) \frac{d v_{O}}{d v_{I}}+v_{O}-v_{O} \frac{d v_{O}}{d v_{I}}
$$

Imposing $d v_{O} / d v_{I}=-1$ yields a relationship between $v_{O}$ and $v_{I}$ right at the point of negative unity slope,

$$
v_{O}=v_{I}-\frac{V_{D D}}{2}
$$

Substituting back into Eq. (3.89), letting $v_{I}=V_{I H}$, and solving for $V_{I H}$, we finally obtain

$$
\begin{equation*}
V_{I H}=\frac{5 V_{D D}-2 V_{t}}{8} \tag{3.90a}
\end{equation*}
$$

image_name:Figure 3.68
description:The graph in Figure 3.68 is a voltage transfer characteristic curve of a CMOS inverter. It is a plot showing the relationship between the input voltage \( v_I \) on the horizontal axis and the output voltage \( v_O \) on the vertical axis. Both axes are labeled in volts, and the graph uses a linear scale.

Overall Behavior and Trends:
The curve begins at the top left, indicating that when the input voltage \( v_I \) is low, the output voltage \( v_O \) is high, at \( V_{OH} \). As \( v_I \) increases, the curve sharply transitions downward, indicating the inverter's switching action, until it reaches a low output voltage \( V_{OL} \) when \( v_I \) is high. This characteristic is typical for digital inverters, which output a logic high when the input is low and vice versa.

Key Features and Technical Details:
- **Critical Points:** The curve shows two critical points where the slope is \(-1 \text{ V/V}\), marked on the graph. These points represent the input voltages \( V_{IL} \) and \( V_{IH} \), where the inverter has maximum sensitivity.
- **Noise Margins:** The graph illustrates the noise margins \( NM_L \) and \( NM_H \) as horizontal distances between \( V_{OL} \) and \( V_{IL} \), and \( V_{IH} \) and \( V_{OH} \), respectively. These margins are critical for determining the inverter's tolerance to noise and ensure reliable switching between logic levels.
- **Annotations:** The graph includes annotations for \( V_{OL}, V_{IL}, V_{IH}, \) and \( V_{OH} \), and marks the regions of noise margins \( NM_L \) and \( NM_H \).

Annotations and Specific Data Points:
- **\( V_{OH} \):** Represents the high output voltage.
- **\( V_{OL} \):** Represents the low output voltage.
- **\( V_{IL} \):** The input voltage at which the output starts to fall.
- **\( V_{IH} \):** The input voltage at which the output is almost low.
- **\( NM_L \):** Noise margin low, calculated as \( V_{IL} - V_{OL} \).
- **\( NM_H \):** Noise margin high, calculated as \( V_{OH} - V_{IH} \).

This graph effectively visualizes the switching behavior and noise margin characteristics of a CMOS inverter, with emphasis on the critical transition region where the slope is \(-1 \text{ V/V}\).

By symmetric reasoning, $V_{I L}=V_{D D}-V_{I H}$, or

$$
V_{I L}=\frac{3 V_{D D}+2 V_{t}}{8}
$$

FIGURE 3.68 Visualizing the noise margins of the CMOS inverter.

Combining with Eq. (3.88), we readily find the noise margins for the case of matched FETs as

$$
\begin{equation*}
N M_{L}=N M_{H}=\frac{3 V_{D D}+2 V_{t}}{8} \tag{3.91}
\end{equation*}
$$

The noise margins are illustrated further in Fig. 3.68.

Find $V_{I L}$ and $V_{I H}$ as well as the noise margins of the inverter of Fig. 3.65.

#### Solution

Using Eqs. (3.90) and (3.91), we find $V_{I L}=(3 \times 5+2 \times 1) / 8=2.1 \mathrm{~V}, V_{I H}=2.9 \mathrm{~V}$, and $N M_{L}=N M_{H}=2.1 \mathrm{~V}$.

### Basic NOR and NAND Gates

Figures $3.69 a$ and $3.70 a$ show how the CMOS inverter topology can serve as basis for the implementation of the basic logic functions known as NOR and NAND. Here, $A$ and $B$ are the inputs, $Y$ is the output, and their logic levels are $L$ for 0 V and $H$ for $V_{D D}$ (such as 5 V ). In either case, circuit behavior is best understood by tracing through the different table entries, one row at a time.

- With reference to the 1 st row in the table of Fig. $3.69 b$ we observe that with $A B=L L$ both $M_{A n}$ and $M_{B n}$ are cut off $(\mathrm{CO})$ while both $M_{A p}$ and $M_{B p}$ are in the ohmic region $(\Omega)$,
image_name:(a)
description:
[
name: MAp, type: PMOS, ports: {S: VDD, D: Y, G: A}
name: MBp, type: PMOS, ports: {S: VDD, D: Y, G: B}
name: MAn, type: NMOS, ports: {S: GND, D: Y, G: X1}
name: MBn, type: NMOS, ports: {S: X1, D: Y, G: B}
]
extrainfo:This is a CMOS implementation of a NOR gate. The PMOS transistors (MAp and MBp) are connected to VDD, while the NMOS transistors (MAn and MBn) are connected to GND. The output Y is connected to the drains of all transistors.

(a)

| $A$ | $B$ | $M_{A n}$ | $M_{B n}$ | $M_{A p}$ | $M_{B p}$ | $Y$ | $R_{o}$ |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| $L$ | $L$ | CO | CO | $\Omega$ | $\Omega$ | $H$ | $2 r_{S D p}$ |
| $L$ | $H$ | CO | $\Omega$ | $\Omega$ | CO | $L$ | $r_{D S n}$ |
| $H$ | $L$ | $\Omega$ | CO | CO | CO | $L$ | $r_{D S n}$ |
| $H$ | $H$ | $\Omega$ | $\Omega$ | CO | CO | $L$ | $r_{D S n} / 2$ |

(b)

FIGURE 3.69 (a) CMOS implementation of the NOR gate, and (b) table illustrating the various circuit conditions for each of the four possible input combinations.
thus pulling $Y$ high. The resistance $R_{o}$ seen looking into the $Y$ node is simply the series combination of the two $p$-channel resistances, $2 r_{S D p}$, pulling $Y$ to $V_{D D}$.

- Proceeding to the 2nd row of Fig. 3.69b, where $A B=L H$, we observe that now $M_{B n}$ becomes conductive ( $\Omega$ ) and $M_{B p}$ goes in cutoff (CO), while the states of $M_{A n}$ and $M_{A p}$ remain unchanged relative to the first row. Consequently, $M_{B n}$ will now pull $Y$ low, and $R_{o}$ is $M_{B n}$ 's resistance $r_{D S n}$ pulling $Y$ to ground.
- The 3rd row of Fig. 3.69b is similar to the second row, but with the roles of $A$ and $B$ interchanged, so the output conditions are similar to those of the second row.
- Finally, in the 4th row of Fig. 3.69b, where $A B=H H$, both $n$-channels are in the ohmic region $(\Omega)$, while both $p$-channels are in cutoff (CO). Consequently, $Y$ is
image_name:FIGURE 3.70 (a)
description:
[
name: M_Ap, type: PMOS, ports: {S: VDD, D: D1, G: A}
name: M_Bp, type: PMOS, ports: {S: D1, D: Y, G: B}
name: M_Bn, type: NMOS, ports: {S: GND, D: Y, G: B}
name: M_An, type: NMOS, ports: {S: GND, D: X, G: A}
]
extrainfo:This circuit is a CMOS NAND gate. The PMOS transistors (M_Ap and M_Bp) are connected in parallel, while the NMOS transistors (M_Bn and M_An) are connected in series. The output Y is high when either input A or B is low, and low when both inputs are high, implementing the NAND logic function.

(a)

| $A$ | $B$ | $M_{A n}$ | $M_{B n}$ | $M_{A p}$ | $M_{B p}$ | $Y$ | $R_{o}$ |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| $L$ | $L$ | CO | CO | $\Omega$ | $\Omega$ | $H$ | $r_{S D p} / 2$ |
| $L$ | $H$ | CO | $\Omega$ | $\Omega$ | CO | $H$ | $r_{S D p}$ |
| $H$ | $L$ | $\Omega$ | CO | CO | CO | $H$ | $r_{S D p}$ |
| $H$ | $H$ | $\Omega$ | $\Omega$ | CO | CO | $L$ | $2 r_{D S n}$ |

(b)

FIGURE 3.70 (a) CMOS implementation of the NAND gate, and (b) table illustrating the various circuit conditions for each of the four possible input combinations.
image_name:FIGURE 3.71
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: Vi, Nn: GND}
name: gmp, type: VoltageControlledCurrentSource, value: gmp*v_gsp, ports: {Np: VO, Nn: GND}
name: gmn, type: VoltageControlledCurrentSource, value: gmn*v_gsn, ports: {Np: Vo, Nn: GND}
name: rop, type: Resistor, value: rop, ports: {N1: Vo, N2: GND}
name: ron, type: Resistor, value: ron, ports: {N1: Vo, N2: GND}
]
extrainfo:The circuit is a small-signal model of a CMOS inverter in the active region. The output voltage Vo is influenced by the parallel combination of resistors rop and ron, and the current sources controlled by the gate-source voltages v_gsp and v_gsn.

FIGURE 3.71 Small-signal model of the CMOS inverter in the active region.
pulled low by the action of two channel resistances in parallel, and such that $R_{o}$ is now $r_{D S n} / 2$. It is apparent that the NOR gate differentiates the state $A B=L L$ from all others.

The reader is encouraged to repeat a similar analysis for the circuit of Fig. 3.70a, and to trace through each row in detail. It is apparent that the NAND gate differentiates the state $A B=H H$ from all others.

### The CMOS Inverter as an Amplifier

As mentioned, in the vicinity of the midpoint $V_{m}=1 / 2 V_{D D}(=2.5$ in our example) both FETs are saturated and thus provide linear amplification. The corresponding output voltage range is

$$
\begin{equation*}
\left(V_{m}-V_{t n}\right) \leq v_{O} \leq\left(V_{m}+\left|V_{t p}\right|\right) \tag{3.92}
\end{equation*}
$$

We wish to find the small-signal gain a over this range. To this end we replace the FETs with their respective small-signal models, and obtain the ac equivalent of Fig. 3.71. By Ohm's law,

$$
v_{o}=-\left(g_{m n} v_{g s n}+g_{m p} v_{g s p}\right) \times\left(r_{o n} / / r_{o p}\right)
$$

Considering that $v_{g s n}=v_{g s p}=v_{i}$, we get

$$
\begin{equation*}
a=\frac{v_{o}}{v_{i}}=-\left(g_{m n}+g_{m p}\right) \times\left(r_{o n} / / r_{o p}\right) \tag{3.93}
\end{equation*}
$$

With matched devices $\left(g_{m n}=g_{m p}=g_{m}, r_{o n}=r_{o p}=r_{o}\right)$, this simplifies as $a=-\left(2 g_{m}\right) \times$ ( $r_{o} / 2$ ), or

$$
\begin{equation*}
a=-g_{m} r_{o} \tag{3.94}
\end{equation*}
$$

Note that the two FETs reinforce each other in pulling ac current out of the output node. Moreover, each FET can be viewed as a CS amplifier with the output resistance $r_{o}$ of the other FET as its load resistance. There's no doubt that the CMOS inverter/ amplifier, despite its simplicity, is a clever circuit!

EXAMPLE 3.39 For the inverter of Fig. 3.65, find the output voltage range of linear operation as well as the gain there.

#### Solution

Since $V_{m}=2.5 \mathrm{~V}$ and $V_{t}=1.0 \mathrm{~V}$, Eq. (3.92) gives $1.5 \mathrm{~V} \leq v_{o} \leq 3.5 \mathrm{~V}$. We also have $g_{m}=\sqrt{2 k I_{D}}=\sqrt{2 \times 1 \times 1.27}=1.6 \mathrm{~mA} / \mathrm{V}$ and $r_{o}=1 / \lambda I_{D}=1 /(0.05 \times 1.27)=$ $15.7 \mathrm{k} \Omega$, so $a=-1.6 \times 15.7 \cong-25 \mathrm{~V} / \mathrm{V}$.

#### Exercise 3.4

(a) Show that the voltage gain of a CMOS inverter/amplifier with matched FETs can be estimated as

$$
\begin{equation*}
a=-\frac{2 V_{A}}{0.5 V_{D D}-V_{t}} \tag{3.95}
\end{equation*}
$$

where $V_{A}=1 / \lambda$.
(b) Use Eq. (3.95) to verify the result of Example 3.39.
(c) What happens if $V_{D D}$ is increased from 5 V to 10 V ? Comment.

Ans. (b) $a=-26.7 \mathrm{~V} / \mathrm{V}$. (c) $a=-10 \mathrm{~V} / \mathrm{V}$; raising $V_{D D}$ lowers $a$.

## APPENDIX 3A

SPICE Models for MOSFETs

As in the case of the BJT, the characteristics of a MOSFET are expressed in terms of a list of parameters that PSpice then uses to create an internal model of the device. Over the last several decades CMOS technology has evolved dramatically along the lines of Moore's law, as mentioned at the beginning of this chapter. As channel lengths keep shrinking to the nanometer range, various higher-order effects come into play, which make the task of modeling a MOSFET for computer simulation an increasingly complex and challenging task. Presently, three different model levels are available. Level 1, also known as the Shichman-Hodges model, works well for devices with channel lengths in the micrometer range, where the $i-v$ characteristics are governed by the square law espoused in this chapter. Level $\mathbf{2}$ is a more advanced model utilizing analytical techniques to calculate the higher-order effects that arise at the submicron level. Level 3 calculates higher-order effects utilizing a combination of analytical and empirical tools.

For our scope here we shall limit ourselves to Level 1, whose parameter list is shown in Table 3A.1. Going down the list, we easily recognize a number of already familiar parameters in the first half or so. The second half contains parameters intervening in the calculation of the various internal capacitances of the MOSFET, a

TABLE 3A. 1 Partial parameter list of the PSpice model for Level-1 MOSFETs.

| Symbol | Name | Parameter description | Units | Default | Example |
| :---: | :---: | :---: | :---: | :---: | :---: |
|  | Level | Model level number |  | 1 | 3 |
| $V_{t 0}$ | Vto | Zero-bias threshold voltage | V | 0 | 1.0 |
| $k^{\prime}$ | Kp | Process transconductance parameter | A/V ${ }^{2}$ | $20 \mu$ | $50 \mu$ |
| $\gamma$ | Gamma | Body-effect parameter | $\mathrm{V}^{1 / 2}$ | 0 | 0.5 |
| $2 \phi_{f}$ | Phi | Surface potential | V | 0.6 V | 0.65 |
| $\lambda$ | Lambda | Channel-length modulation parameter | $\mathrm{V}^{-1}$ | 0 | 0.05 |
| $r_{d}$ | Rd | Bulk resistance of the drain | $\Omega$ | 0 | 1 |
| $r_{s}$ | Rs | Bulk resistance of the source | $\Omega$ | 0 | 1 |
| $\mu$ | Uo | Surface mobility | $\mathrm{cm}^{2} / \mathrm{Vs}$ | 600 | 500 |
| $t_{o x}$ | Tox | Oxide thickness | m | 100 n | 10 n |
| $N_{A}$ or $N_{D}$ | Nsub | Substrate doping | $\mathrm{cm}^{-3}$ | 0 | $10^{15}$ |
| $C_{d b 0}$ | Cbd | Zero-bias B-D junction capacitance | F | 0 | 10 fF |
| $C_{s b 0}$ | Cbs | Zero-bias B-S junction capacitance | F | 0 | 10 fF |
| $\phi_{0}$ | Pb | B-D and B-S junction built-in potential | V | 0.8 | 0.75 |
| image_name:Cov/W
description:The image displays the notation 'C_{ov}/W', which represents the overlap capacitance per unit width. This parameter is used in semiconductor device physics to describe the capacitance associated with the overlap of the gate electrode over the source/drain regions, normalized by the width of the device. It is a crucial factor in determining the parasitic capacitances in MOSFET devices, affecting their switching speed and overall performance. The unit for this parameter is typically Farads per meter (F/m).
| Cgso | G-S overlap capacitance per unit $W$ | F/m | 0 | 100 p |
| image_name:C_{ov}/W
description:The image depicts a mathematical expression used in semiconductor device physics, specifically representing overlap capacitance per unit width. The expression shown is **C_{ov}/W**, where **C_{ov}** stands for the overlap capacitance, and **W** denotes the width. This parameter is crucial in determining parasitic capacitances in MOSFET devices, influencing their switching speed and overall performance. The unit for this parameter is typically Farads per meter (F/m).
| Cgdo | G-D overlap capacitance per unit $W$ | F/m | 0 | 100 p |
| $C_{g b} / L$ | Cgbo | G-B overlap capacitance per unit $L$ | F/m | 0 | 250 p |
| $C_{j 0 \text { (bm) }}$ | Cj | Unit-area zero-bias bulk junction bottom capacitance | F/m ${ }^{2}$ | 0 | $250 \mu$ |
| $m_{\text {btm }}$ | Mj | Bulk junction bottom grading coefficient |  | 0.5 | 0.5 |
| $C_{j 0(\mathrm{sw})}$ | Cjsw | Unit-perimeter zero-bias bulk junction sidewall capacitance | F/m | 0 | 0.5 n |
| $m_{\text {sw }}$ | Mjsw | Bulk junction sidewall grading coefficient |  | 0.33 | 0.33 |
| $X_{i}$ | xj | Metallurgical S-B and D-B junction depth | m | 0 | $0.5 \mu$ |
| $L_{o v}$ | LD | Lateral diffusion | m | 0 | 100 n |

subject that will be taken up in great detail in Chapter 6, when we will investigate the frequency and transient responses of integrated circuits.

The library of the PSpice version used in this book comes with the Level 3 models of two power MOSFETs, the $n$-channel IRF150 and the $p$-channel IRF9140. The user can create additional models by editing either of these models. As an example, consider the PSpice circuits of Figs. 3.14 and 3.16 that were created to plot the $i-v$ curves of a homebrew MOSFET having $k^{\prime}=50 \mu \mathrm{~A} / \mathrm{V}^{2}, V_{t 0}=1.0 \mathrm{~V}, \lambda=0.05 \mathrm{~V}^{-1}$, $W=2 \mu \mathrm{~m}$, and $L=1 \mu \mathrm{~m}$. As usual, we create a PSpice circuit schematic via the Place $\rightarrow$ Part commands to lay out the various components, and the Place $\rightarrow$ Wire commands to interconnect them. When it comes to placing the FET, we import it from PSpice's library by going down the list of entries and selecting the IRF150 part by left-clicking on it. Once the FET has been placed in the circuit schematic, we can visualize its model by left-clicking on the FET itself to select it, and then
right-clicking to activate a pull-down menu of possible actions. If we left-click on Edit PSpice Model, the following list will appear:

```
.model IRF150 NMOS(Level=3 Gamma=0 Delta=0 Eta=0 Theta=0
+ Kappa=0 Vmax=0 Xj=0 Tox=100n Uo=600 Phi=.6 Rs=1.624m
+ Kp=20.53u W=.3 L=2u Vto=2.831 Rd=1.031m Rds=444.4K
+ Cbd=3.229n Pb=.8 Mj=.5 Fc=.5 Cgso=9.027n Cgdo=1.679n
+ Rg=13.89 Is=194E-18 N=1 Tt=288n)
```

To create our own homebrew $n$ MOSFET model we simply edit (overwrite) the above list, making sure to give our new model a different name before saving it, such as Mn, in order to avoid destroying the existing one. The result is

```
.model Mn NMOS(W=2u L=1u Kp=50u VtO=1.0V Lambda=0.05)
```

Likewise, a homebrew $p$ MOSFET model called Mp and having $k^{\prime}=20 \mu \mathrm{~A} / \mathrm{V}^{2}$, $V_{t 0}=-0.75 \mathrm{~V}, \lambda=0.1 \mathrm{~V}^{-1}, W=5$, and $L=1 \mu \mathrm{~m}$ would be .model Mp PMOS(W=5u L=1u Kp=20u Vto=-0.75V lambda=0.1)

All omitted parameters are automatically assigned default values according to Table 3A.1.
