# 2. Bipolar Junction Transistors
Chapter Outline
2.1 Physical Structure of the BJT 112
2.2 Basic BJT Operation 117
2.3 The $i-v$ Characteristics of BJTs 130
2.4 Operating Regions and BJT Models 137
2.5 The BJT as an Amplifier/Switch 150
2.6 Small-Signal Operation of the BJT 157
2.7 BJT Biasing for Amplifier Design 169
2.8 Basic Bipolar Voltage Amplifiers 177
2.9 Bipolar Voltage and Current Buffers 189
Appendix 2A: SPICE Models for BJTs 201
References 203
Problems 203
There is no doubt that the invention of the vacuum-tube diode paved the way for a number of useful applications that would have been impossible using only the linear devices that we study in introductory circuits courses. However, the horizons of electronics were expanded much further with the invention of a three-element vacuum tube called the triode. In 1906 Lee DeForest modified Fleming's diode valve, discussed at the beginning of Chapter 1, by inserting a third element between the cathode and the anode, called the grid, which he used to modulate the electron flow from cathode to anode. In fact, by driving the grid with an audio signal from a microphone, he could get a much stronger signal at the anode (which he renamed plate), and he then used this signal to drive a pair of earphones. Aptly called audion, this new valve was in effect an amplifier, which subsequently he applied to the design of radio signal detectors and oscillators. In fact, the electronics of the next half-century was dominated by vacuum tubes, which in the course of the years were further refined by incorporating additional grids to create first the tetrode and finally the pentode. During this period, a number of milestone innovations took place, such as the development of radio communications (AM and FM), television, radar, and finally, right after World War II, the first digital computers.
Central to the operation of the triode was the idea of using one of its elements (the grid) to control the current flow between the other two (cathode and plate). By a hydraulic analogy, the triode could be viewed as a valve. From a circuit viewpoint, it simply implemented the concept of controlled (or dependent) source that we study in introductory circuit courses. The next electronics-era milestone occurred when the triode function was realized on a piece of semiconductor material. Such a device, called the transistor, was invented in 1947 by John Bardeen, Walter Brattain, and William Shockley at Bell Labs. The closest counterpart of the triode is what today we refer to as the npn bipolar junction transistor (npn BJT). It consists of a slab of $n$-type semiconductor material with: (a) one side doped very heavily ( $n^{+}$-type) to act as a copious source of free electrons, and thus called the emitter; (b) the opposite side, designed to act like the plate of a triode and thus called the collector; and (c) an extremely thin layer of $p$-type material sandwiched in between and called the base, designed to entice electrons from the emitter and direct them in controlled fashion to the collector-just like the grid in the triode. What made triodes and then transistors so useful is that the power being controlled can be much higher than that expended in effecting the control itself. For this reason, triodes and transistors are said to be active devices, and are also referred to as amplifiers. Of course, power cannot be created or magnified out of nothing-by active device we simply mean a device that uses little power to control the transfer of a much greater amount of power from an external energy source such as a power supply. A classic example is the car radio, where a low-power radio receiver controls, via an audio power amplifier, the transfer of a much higher amount of power from the car battery to the loudspeakers. In fact, the very name transistor was coined as a contraction of the words transfer and resistor. In summary, a transistor in itself is a passive device; however, when used in conjunction with an external source of energy, it can be made to act as an active device.
The newly invented transistor was soon put to use as a replacement for the much bulkier, power-hungry, and only moderately reliable vacuum tube. In fact, the first transistor circuits were virtual replicas of vacuum-tube circuit prototypes, if with suitable scaling of the power supplies and surrounding components. The 1950s saw the appearance of the first electronic consumer product using this new device, namely, the hand-held all-transistor radio. Toward the end of the decade it was also realized that the dramatic miniaturization and power savings brought about by the transistor could be exploited further by fabricating entire circuits (transistors, diodes, resistors, and small capacitors, along with their interconnections) monolithically, that is, on the same piece of semiconductor material, or chip. Called the integrated circuit (IC), it was first implemented in 1958 by Jack Kilby at Texas Instruments, and, independently, in 1959 by Robert Noyce at Fairchild Semiconductor. The 1960s saw a feverish activity that resulted in the development, among others, of the first IC operational amplifier (IC op amp) by Fairchild Semiconductor ( $\mu \mathrm{A}$ Series), as well as the digital IC families known as transistor-transistor logic (TTL) by Texas Instruments ( 7400 Series), and emitter-coupled logic (ECL) by Motorola (10K Series).
Meanwhile, in the very early 1970s, another type of transistor known as the metal-oxide-semiconductor (MOS) field-effect transistor (FET), or MOSFET for short, become a commercial reality. Compared to its BJT predecessor, the MOSFET
could be fabricated in an even smaller size, and digital MOSFET circuits could be designed to consume practically zero standby power. The first battery-powered electronic calculators and wristwatches made precise use of this new technology. Also, a new digital IC family known as complementary MOS (or CMOS for short) was introduced by RCA ( 4000 Series) as a low-power alternative to the bipolar families of the TTL and ECL types. Finally, Intel used MOS technology to develop the first microprocessor, in 1971. Since then, IC electronics has advanced exponentially and has penetrated virtually every aspect of modern life. This impressive growth has been governed by Moore's law, roughly stating that thanks to continued advances in IC fabrication, the number of devices that can be integrated on a given chip area doubles approximately every 18 months. Originally formulated in 1965, the law still holds to this day, though it has been pointed out that technology is bound to approach physical limits that will eventually lead to the demise of this law.
The BJT, after having been the dominant semiconductor device for nearly three decades, has been overtaken by the MOSFET especially in digital electronics, thanks to the latter's aforementioned advantages of smaller size and lower power consumption. Nonetheless, the BJT continues to be the device of choice in a number of specialized areas, such as high-performance analog electronics and radiofrequency electronics. It is also preferred in discrete designs, thanks to the availability of a wide selection of devices. BJTs and MOSFETs can also be fabricated simultaneously on the same chip, if at an increase in fabrication steps and thus production cost. The resulting technology, aptly called biCMOS technology, exploits the advantages of both transistor types to provide even more innovative design opportunities. Contemporary ICs often combine digital as well as analog functions on the same chip, this being the reason for the name mixed-signal or also mixed-mode ICs.
There is no question that microelectronics is one of the most exciting, challenging, and rapidly evolving fields of human endeavor. The beginner may feel overwhelmed by all this, and rightly so. But, as we embark upon the study of today's dominant processes and devices, we will try to focus on general principles that transcend the particular technological milieu of the moment and that we can apply in the future to understand new processes and devices as they become available and commercially mature. Focus on general principles, combined with continuing education, is a necessity for the young engineer determined to establish and maintain a satisfying career in a seemingly ever-changing field.
CHAPTER HIGHLIGHTS
This chapter begins with the physical structure of the BJT, basic underlying semiconductor principles, device characteristics, operating regions and modeling. As in Chapter 1's treatment of the pn junction, emphasis is placed on practical aspects of relevance to today's industrial environment (rules of thumb).
Next, the BJT is investigated in its two most important class of applications, namely, as an amplifier for analog electronics, and as a switch for digital electronics. The large-signal and small-signal models developed for the pn junction are now expanded to accommodate the more complex BJT.
After a discussion of BJT biasing techniques, the remainder of the chapter investigates the three basic amplifier configurations, namely, the common-emitter (CE), common-collector (CC), and common-base (CB) configurations. The CE configuration is presented as the natural realization of voltage amplification, whereas the CC and CB configurations serve most naturally as voltage and current buffers, respectively. Also, proper emphasis is placed on the role of the BJT as a resistance transformation device (which actually provided the basis for its very name.) The transformation equations are conveniently tabulated for easy reference in later chapters.
The amplifiers investigated in this chapter are of the so-called discrete type because they can be built using off-the-shelf components (transistors, resistors, and capacitors), and as such they can easily be tried out by the student in the lab. Though nowadays electronic circuits comprise large numbers of transistors fabricated monolithically on the same semiconductor chip, we need to understand the workings of a single-transistor amplifier before tackling the complexity of multi-transistor ICs, a subject that will be undertaken in Chapter 4. In this respect, a discrete amplifier offers the pedagogical advantage that the transistor is surrounded by the circuit elements most familiar to the student (resistors, and when necessary, capacitors). Also, the separation between dc and ac components is usually more obvious than in more complex monolithic realizations. Lastly, it must be said that when an engineer tests or applies an IC, the need often arises to surround it with ancillary circuitry made up of discrete components (a buffer, a driver, a power booster, etc.). In summary, the objective of this chapter is to introduce the student to the basics of single-transistor amplifiers, and in so doing, to lay a solid foundation for the study of multi-transistor monolithic realizations in later chapters.
The chapter makes abundant use of PSpice both as a software oscilloscope to display BJT characteristics, transfer curves and waveforms, and as a verification tool for dc as well as ac calculations.
## 2.1 PHYSICAL STRUCTURE OF THE BJT
Figure 2.1 shows, in simplified form, the structure of an npn bipolar junction transistor (npn BJT) of the type encountered in more traditional integrated-circuit (IC) technology. The device is fabricated through a complex sequence of steps including pattern definition, crystal growth, diffusion, material deposition and material removal, on a wafer of lightly-doped $p$-type silicon ( $p^{-}$) called the substrate. The wafer provides physical support for the device under consideration as well as all other devices of the same IC.
A BJT is equipped with three terminals, called respectively, the emitter $(E)$, base (B), and collector (C). A fourth terminal $(S)$ provides access to the substrate, but serves no active function except for ensuring electric isolation between adjacent devices. Starting out with a polished $p^{-}$wafer shown at the bottom, the fabrication of a npn BJT proceeds according to the following steps:
- First, some heavily doped $n$-type silicon $\left(n^{+}\right)$is deposited in the area to be occupied by the BJT, and then is diffused into the wafer to form a low-resistance path known as buried layer.
image_name:FIGURE 2.1 Basic physical structure of an IC npn BJT
description:The diagram illustrates the basic physical structure of an integrated circuit (IC) npn bipolar junction transistor (BJT). The components and layers are arranged in a cross-sectional view, highlighting the different regions and materials involved in the device's construction.
1. **Components and Structure:**
- **Emitter, Base, and Collector:** These are the three main regions of the npn BJT. The emitter and collector are made of heavily doped n-type silicon (n+), while the base is a p-type region.
- **n+ Buried Layer:** This is a heavily doped n-type silicon layer that provides a low-resistance path for the collector current.
- **n- Epitaxial Layer:** A lightly doped n-type silicon layer grown on top of the n+ buried layer, forming the collector region.
- **p- Substrate:** The bottom layer of the structure, made of lightly doped p-type silicon.
- **p- Isolation (p- Iso):** These regions surround the BJT structure, providing electrical isolation from adjacent devices.
2. **Connections and Interactions:**
- The emitter, base, and collector are vertically aligned, facilitating the flow of charge carriers (electrons) from the emitter to the collector through the base.
- The n+ buried layer ensures a low-resistance path for the collector current, enhancing the transistor's performance.
- The p- isolation regions electrically isolate the BJT from other components on the same chip, preventing unwanted interactions.
3. **Labels and Annotations:**
- "Emitter," "Base," and "Collector" labels identify the respective regions of the BJT.
- "n+ Buried layer," "n- Epitaxy," "p- Iso," and "p- Substrate" labels indicate the material properties and doping levels of the different regions.
- "Junction isolation" label highlights the isolation technique used to separate the BJT from other devices.
- "Base width" annotation indicates the physical width of the base region, which is a critical parameter affecting the transistor's performance.
FIGURE 2.1 Basic physical structure of an IC npn BJT.
- Next, a crystal layer of lightly doped $n$-type silicon $\left(n^{-}\right)$is grown on top of the $n^{+}$buried layer and the surrounding $p^{-}$wafer area. This layer, known as epitaxial (or epi) layer, is designed to form the collector region.
- A $p$-type diffusion is made into the epi layer along the perimeter of the region destined to be occupied by the BJT, until it joins the $p$-type substrate underneath. As we shall see, this diffusion, referred to as $p^{-}$iso, is designed to provide junction isolation between adjacent BJTs.
- Another but less deep $p$-type diffusion is made into the epi layer to create the base region of the BJT.
- Two heavily doped $n$-type diffusions are made simultaneously, one into the $p$ type base region to form the $n^{+}$emitter region, and the other into the $n^{-}$epi layer to provide what is referred to as an ohmic contact between the $n^{-}$epi region and the collector electrode. (Nowadays the $n^{+}$collector diffusion is made to extend all the way to the buried layer below.)
- Finally, three metal depositions form the $E, B$, and $C$ electrodes. An additional connection is made to the substrate ( $S$ ), which, in the case of the npn BJT shown, is always kept at the most negative voltage (MNV) in the circuit. (The interested student is encouraged to search the Web for videos and articles illustrating the fascinating subject of transistor fabrication.)
Viewing the collector regions as $n$-type material surrounded by $p$-type regions, we identify a distributed $p n$ junction of sorts. Biasing the $p^{-}$substrate (and thus the outer $p^{-}$iso regions) at the MNV ensures that this distributed junction is at all times reverse biased. Aside for usually negligible leakage currents, the collectors of adjacent BJTs are thus kept isolated from each other, allowing for different BJTs to operate in electrically independent fashion.
We identify two basic ingredients in a BJT: (a) the $p n$ junction formed by the base-emitter (B-E) regions, and (b) the pn junction formed by the base-collector (B-C)
image_name:FIGURE 2.2 Currents in a monolithic npn BJT operating in the forward active mode.
description:The image is a cross-sectional diagram of a monolithic npn bipolar junction transistor (BJT) operating in the forward active mode. It illustrates the flow of currents and the structure of the BJT.
1. **Identification of Components and Structure:**
- The BJT is composed of three main regions: the emitter (E), base (B), and collector (C).
- The emitter and collector are denoted as \( n^+ \) regions, indicating heavily doped n-type semiconductor material.
- The base is a \( p \) region, indicating p-type semiconductor material.
- The diagram also features \( n^- \) epitaxy, which is a lightly doped n-type layer between the base and collector.
- Surrounding the main structure are \( p^- \) iso regions, which provide electrical isolation.
- The substrate is labeled as \( p^- \) and is connected to the ground.
2. **Connections and Interactions:**
- The emitter (E) is connected to ground, and the current \( i_E \) flows from it.
- The base (B) is connected to a voltage source \( v_{BE} \) of approximately 0.7 V, indicating that the base-emitter junction is forward biased.
- The collector (C) is connected to a voltage source \( v_{CB} \) of at least 0.2 V, indicating that the base-collector junction is reverse biased.
- The flow of electrons is shown moving from the emitter through the base and into the collector, which is characteristic of forward active mode operation.
- Holes are shown in the base region, indicating recombination processes.
- The currents \( i_E \), \( i_B \), and \( i_C \) are depicted, with \( i_B \) being the base current and \( i_C \) being the collector current.
3. **Labels, Annotations, and Key Features:**
- The diagram includes arrows to indicate the direction of electron flow and hole movement.
- The \( v_{BE} \) and \( v_{CB} \) voltages are labeled with their respective values, emphasizing the biasing conditions.
- The diagram is annotated with labels for electrons and holes to clarify the charge carriers involved in the operation of the BJT.
- The \( p^- \) substrate is connected to a terminal labeled \( S \), which is grounded, ensuring the isolation of the device from other components.
FIGURE 2.2 Currents in a monolithic npn BJT operating in the forward active mode.
regions. The most common mode of operation of a BJT is with the B-E junction forward biased and the B-C junction reverse biased. This mode, which is at the basis of BJT applications as an amplifier, is called the forward active (FA) mode. Briefly stated, the main event taking place in an $n p n$ BJT operating in the FA mode is
A current of electrons flowing from the emitter, through the base, to the collector, under control by the base-emitter voltage drop $v_{B E}$.
The situation is illustrated in Fig. 2.2, where we note that since electrons are negative, the directions of the terminal currents $i_{E}$ and $i_{C}$ are opposite to the direction of electron flow. Additionally, we make the two following observations:
- Not all of the electrons emitted from the emitter are collected by the collector. As they transit through the $p$-type base region, a small fraction recombines with the many holes present there, indicating the existence of a base current component of holes to sustain this recombination process. By fabricating the base region very thin (fractions of $1 \mu \mathrm{~m}$ ) the manufacturer ensures that the recombination component is suitably small.
- As is the case with all pn junctions, the diffusion of electrons from $E$ to $B$ is accompanied by a diffusion of holes from $B$ to $E$. By doping the emitter much more heavily than the base (typically by two or more orders of magnitude), the manufacturer ensures that the inrush of electrons from the emitter literally dwarfs the diffusion of holes from the base, thus keeping this second basecurrent component also suitably small.
The reasons for desiring a small base current $i_{B}$ for a given collector current $i_{C}$ is that the ratio
$$
\begin{equation*}
\beta_{F}=\frac{i_{C}}{i_{B}} \tag{2.1}
\end{equation*}
$$
which is aptly called the forward current gain, represents a figure of merit of the BJT. It also provides us with additional flexibility in that we can operate the BJT either as a voltage-controlled current source ( $i_{C}$ controlled by $v_{B E}$ ) or as a currentcontrolled current source ( $i_{C}$ controlled by $i_{B}$ ). Integrated-circuit BJTs have typically $\beta_{F} \cong 250$, though it is possible to fabricate special BJTs, known as superbeta BJTs, with $\beta_{F}$ as high as 10,000 . As we proceed, we shall re-examine BJT behavior in much greater detail.
### pnp BJTs
A pnp BJT is obtained by negating the doping type of each region of an npn BJT so that the emitter region is now $p^{+}$, the base is $n$, and the collector is $p^{-}$. This indeed is the case of discrete pnp BJTs, that is, devices that are fabricated and packaged individually. However, in conventional bipolar IC technology pnp BJTs must be fabricated using the same processing steps as npn BJTs. In this technology two pnp BJT structures are in common use: (a) the lateral pnp BJT and (b) the substrate or vertical pnp BJT (see Fig. 2.3). We make the following observations:
- In both pnp types the $n^{-}$epi layer, which served as the collector region of the $n p n$ BJT, is now put to use as the base region (the function of the $n^{+}$diffusion is only to ensure an ohmic contact to the external terminal $B$ ).
- In both pnp types the $p$-type diffusion, which served as the base region of the $n p n$ BJT, is now put to use as the emitter region, whose function is to act as a source of holes.
- In the lateral pnp BJT the role of the collector is played by another $p$-type diffusion, fabricated in the guise of a ring surrounding the emitter (as viewed from above). As shown, holes flow laterally out of the centralized $p$-type emitter region and into the surrounding $p$-type collector ring.
- In the substrate pnp BJT the role of the collector is played by the $p^{-}$substrate, so holes now flow vertically from the emitter (fabricated in the guise of a ring surrounding the $n^{+}$contact region), through the $n^{-}$epi layer, to the $p^{-}$substrate.
- Unlike lateral BJTs, vertical BJTs are constrained to have their collector (formed by the substrate) connected to the MNV in the circuit.
- In either pnp structure the base region is not as thin as that of the npn structure, indicating a higher base-current component of electrons recombining with the holes in transit through this wider base.
- Since the $p$-type emitters are not as heavily doped as the $n^{+}$emitter of the $n p n$ structure, the injection of holes from emitter to base will not dwarf that of electrons from base to emitter as dramatically.
image_name:FIGURE 2.3
description:The image labeled as "FIGURE 2.3" illustrates the physical structures and currents of planar-process pnp Bipolar Junction Transistors (BJTs), specifically showing the lateral pnp (left) and the substrate or vertical pnp (right).
1. **Identification of Components and Structure:**
- **Lateral pnp (Left):**
- The structure includes a p-type base region surrounded by n+ regions, with n- epitaxy and a p- substrate.
- The device is isolated by p- isolation regions.
- **Vertical pnp (Right):**
- This structure also features a p-type base but is more vertically oriented, with the p-type regions extending downwards.
- It is supported by an n- epitaxy and n+ buried layer, with isolation provided by p- regions.
2. **Connections and Interactions:**
- **Lateral pnp:**
- Current flows from the emitter (E) to the collector (C) via the base (B), with the current directions indicated by arrows.
- Voltage across the emitter-base (V_EB) is approximately 0.7 V, and the base-collector voltage (V_BC) is around 0.2 V.
- Currents i_E (emitter current), i_B (base current), and i_C (collector current) are labeled, showing typical flow directions.
- **Vertical pnp:**
- Similar current flow as the lateral pnp, with emitter, base, and collector connections marked.
- Voltage and current directions are similarly annotated, with V_EB and V_BC values indicated.
3. **Labels, Annotations, and Key Features:**
- Both structures have detailed annotations for voltages (V_EB, V_BC) and currents (i_E, i_B, i_C).
- The p-type and n-type regions are clearly marked, with n+ and n- indicating different doping levels.
- The diagram highlights the movement of charge carriers (holes) within the p-type regions, depicted with plus signs and arrows.
- Isolation regions and substrate are labeled, providing context for the device's placement and electrical isolation.
FIGURE 2.3 Physical structures and currents of planar-process pnp BJTs: the lateral pnp (left) and the substrate or vertical pnp (right).
- For these and other reasons, lateral pnp BJTs offer lower current gains than their npn counterparts (typically $\beta_{F} \approx 50$ ). The fabrication process has been optimized for the fabrication of $n p n$ devices, so pnp BJTs come out as second-rate devices. But, if no such constraints are imposed, pnp BJTs can indeed be fabricated with comparable performance characteristics as their npn counterparts, if at the price of additional processing steps and therefore higher cost.
The fabrication process just discussed, aptly referred to as junction-isolated, double-diffusion bipolar planar process, is just one of various processes in use today. In high-speed applications, processes using dielectric isolation are preferable as they are exempt from the parasitic capacitance provided by the isolating junction. Also, in BiCMOS technology, BJTs are fabricated via processes compatible with the fabrication of MOSFETs. Finally, it is possible to fabricate both npn and pnp BJTs with comparable high-quality performance, if at the price of increased processing complexity and cost.
### Circuit Symbols for the BJTs
Figure 2.4 shows the circuit symbols used for the two BJT types, along with the current directions and voltage polarities. In either case, the terminal with the arrow is by definition the emitter, and the arrow itself indicates emitter-current direction. In the pnp BJT, where the main current is due to holes, the arrow coincides with the direction of hole flow. However, in the npn BJT, where the main current is due to
image_name:Figure 2.4
description:
[
name: Q1, type: NPN, ports: {C: C, B: B, E: E}
name: Q2, type: PNP, ports: {C: C, B: B, E: E}
]
extrainfo:The diagram shows the symbols for NPN and PNP BJTs with current directions and voltage polarities indicated. The NPN transistor Q1 has current iC flowing into the collector and iE flowing out of the emitter. The PNP transistor Q2 has current iC flowing out of the collector and iE flowing into the emitter. Voltage polarities are marked for VCB, VBE, VCE, VEB, VBC, and VEC across the BJTs.
FIGURE 2.4 BJT symbols, showing the correct current directions and voltage polarities. Note that the two devices have opposite current directions as well as opposite voltage polarities. To signify opposite current directions, we simply reverse the current arrows (for instance, $i_{c}$ flows into the npn BJT, but out of the pnp BJT). To signify opposite voltage polarities, we simply interchange the order of the subscripts in voltage drops. In so doing, we avoid having to work with negative voltage drops. For instance, we use $v_{B E}>0$ to turn on the npn BJT, and $v_{E B}>0$ (rather than $v_{B E}<0$ ) to turn on the pnp BJT.
electrons, which are negative, the emitter arrow is opposite to the direction of internal electron flow.
Regardless of the device type and operating mode, a BJT must at all times satisfy KCL,
$$
\begin{equation*}
i_{E}=i_{C}+i_{B} \tag{2.2}
\end{equation*}
$$
When analyzing a BJT circuit, it pays to draw a circle around the device and regard it as a supernode.
## 2.2 BASIC BJT OPERATION
Figure 2.5, top, shows a vertical slice of the emitter-base-collector structure of Fig. 2.1, but rotated counterclockwise by $90^{\circ}$ to facilitate analysis. To develop a feel for the various physical quantities involved, we shall assume the following doping densities:
$$
\begin{align*}
\text { Emitter }\left(n^{+}\right): & N_{D E}=10^{20} \text { donor atoms } / \mathrm{cm}^{3}  \tag{2.3a}\\
\text { Base }(p): & N_{A B}=10^{18} \text { acceptor atoms } / \mathrm{cm}^{3}  \tag{2.3b}\\
\text { Collector }\left(n^{-}\right): & N_{D C}=10^{16} \text { donor atoms } / \mathrm{cm}^{3} \tag{2.3c}
\end{align*}
$$
At room temperature, virtually all dopant atoms are ionized, so the electron concentrations in the emitter and collector regions are, respectively, $n_{E 0} \cong N_{D E}$ and $n_{C 0} \cong$ $N_{D C}$, and the hole concentration in the base region is $p_{B 0} \cong N_{A B}$. Also referred to as majority-carrier concentrations, they are thus
$$
\begin{equation*}
n_{E 0} \cong 10^{20} \text { electrons } / \mathrm{cm}^{3} \quad p_{B 0} \cong 10^{18} \text { holes } / \mathrm{cm}^{3} \quad n_{C 0} \cong 10^{16} \text { electrons } / \mathrm{cm}^{-3} \tag{2.4}
\end{equation*}
$$
image_name:FIGURE 2.5 Equilibrium electron and hole concentrations inside an npn BJT.
description:The image labeled "FIGURE 2.5 Equilibrium electron and hole concentrations inside an npn BJT" is a schematic representation of an npn bipolar junction transistor (BJT) showing the distribution of electrons and holes across its different regions.
1. **Identification of Components and Structure:**
- The diagram is divided into three main regions: the emitter (labeled as \(n^+\)), the base (labeled as \(p\)), and the collector (labeled as \(n^-\)).
- Each region is depicted with a concentration of charge carriers: electrons in the \(n^+\) emitter and \(n^-\) collector, and holes in the \(p\) base.
- The emitter and collector regions are heavily doped with donor ions (indicated by circles with plus signs), while the base is doped with acceptor ions (indicated by circles with minus signs).
2. **Connections and Interactions:**
- The diagram shows the emitter \(E\), base \(B\), and collector \(C\) terminals, indicating where external connections would be made.
- Two space-charge layers (SCL) are highlighted: the base-emitter space-charge layer (B-E SCL) and the base-collector space-charge layer (B-C SCL). These regions are shown with a gradient of charge carriers, illustrating the formation of depletion regions.
- The electric fields across these layers are indicated by \(E_{EB}\) and \(E_{CB}\), showing the direction of potential barriers that affect carrier movement.
3. **Labels, Annotations, and Key Features:**
- The concentrations of electrons \(n\) and holes \(p\) are plotted along the \(x\)-axis, showing how they vary across the device. The majority carrier concentrations are labeled as \(n_{E0} \approx 10^{20} \text{ electrons/cm}^3\) for the emitter, \(p_{B0} \approx 10^{18} \text{ holes/cm}^3\) for the base, and \(n_{C0} \approx 10^{16} \text{ electrons/cm}^3\) for the collector.
- The graph beneath the schematic illustrates the exponential decrease in majority carrier concentrations as they move away from their respective regions, complying with the mass-action law \(n \times p = n_i^2\).
- The intrinsic concentration \(n_i\) is not explicitly labeled in the diagram but is implied through the mass-action law and temperature dependence discussed in the context.
Overall, this diagram provides a detailed view of the charge carrier distribution and potential barriers within an npn BJT at equilibrium, crucial for understanding its operation.
FIGURE 2.5 Equilibrium electron and hole concentrations inside an npn BJT.
In each region, the electron and hole concentrations $n$ and $p$ satisfy the mass-action law,
$$
n \times p=n_{i}^{2}
$$
where $n_{i}$ is the intrinsic concentration of holes and electrons in silicon. This concentration is a strong function of temperature, and for silicon it takes on the form
$$
\begin{equation*}
n_{i}^{2}(T)=1.5 \times 10^{33} T^{3} e^{-14028 / T} \mathrm{~cm}^{-6} \tag{2.5}
\end{equation*}
$$
At room temperature ( $T=300 \mathrm{~K}$ ), Eq. (2.5) gives $n_{i}^{2}=2 \times 10^{20} \mathrm{~cm}^{-6}$. The minoritycarrier concentrations are thus found as $p_{E 0}=n_{i}^{2} / n_{E 0}, n_{B 0}=n_{i}^{2} / p_{B 0}$, and $p_{C 0}=n_{i}^{2} / n_{C 0}$. For the above doping densities, they are
$p_{E 0} \cong 2 \times 10^{0}$ holes $/ \mathrm{cm}^{3} \quad n_{B 0} \cong 2 \times 10^{2}$ electrons/cm ${ }^{-3} \quad p_{C 0} \cong 2 \times 10^{4}$ holes $/ \mathrm{cm}^{-3}$
Both the majority and minority concentrations are diagrammed (not to scale) in Fig. 2.5, bottom.
During fabrication itself, electrons from the electron-rich emitter region will spontaneously diffuse into the adjacent electron-starved base region, leaving behind positively charged donor ions. Likewise, holes from the base region will diffuse to the adjacent emitter region, leaving behind negatively charged acceptor ions. Both ion types are bound to fixed positions of the crystal lattice, and end up forming a space-charge layer (SCL) at each side of the B-E metallurgical junction. Inside the SCL there is an electric field $E_{E B}$ directed from the positive ions to the negative ions. A similar situation occurs at the B-C junction, where the electric field is denoted as $E_{C B}$. In equilibrium, the strengths of both fields are such as to exactly counterbalance the tendency by electrons to diffuse from the emitter and collector regions to the base region, and by holes to diffuse from the base to the emitter and collector regions.
### Operation in the Forward Active (FA) Mode
The BJT reveals its unique abilities when we perturb the above equilibrium by applying suitable voltages across its junctions. As mentioned, the most useful mode of operation is the forward active (FA) mode, which occurs when we forward-bias the B-E junction and reverse bias the B-C junction. Forward-biasing the B-E junction with a voltage $v_{B E}$ will reduce the potential barrier that keeps electrons and holes from diffusing across the junction. We are particularly interested in the situation right at the base edge of the B-E SCL, which has been taken as the origin of the $x$-axis in Fig. 2.5. By the law of the junction discussed in connection with Eq. (1.51), the effect of applying $v_{B E}$ is to cause the electron concentration $n_{B}(0)$ at the SCL's edge to shoot up from its equilibrium value $n_{B 0}\left(\cong 2 \times 10^{2} \mathrm{~cm}^{-3}\right)$ to the new value
$$
\begin{equation*}
n_{B}(0)=n_{B 0} e^{v_{B E} / V_{T}} \tag{2.7}
\end{equation*}
$$
where $V_{T}=k T / q$ is the thermal voltage ( $V_{T}=25.9 \mathrm{mV} \cong 26 \mathrm{mV}$ at $T=300 \mathrm{~K}$ ). To get an idea, with the typical value $v_{B E}=700 \mathrm{mV}, n_{B}(0)$ shoots up from $n_{B 0} \cong$ $2 \times 10^{2} \mathrm{~cm}^{-3}$ to
$$
n_{B}(0) \cong\left(2 \times 10^{2}\right) e^{700 / 26} \cong\left(2 \times 10^{2}\right) \times 5 \times 10^{11}=10^{14} \mathrm{~cm}^{-3}
$$
This is quite an increase! However, since we still have $n_{B}(0) \ll p_{B 0}\left(\right.$ as $\left.10^{14} \ll 10^{18}\right)$, the majority of mobile charges there continue to be holes. We refer to this situation as low-level injection (in this case, injection of electrons from the emitter).
Reverse-biasing the B-C junction with a voltage $v_{B C} \leq 0.2 \mathrm{~V}$ or, equivalently, with a voltage $v_{C B} \geq 0.2 \mathrm{~V}$, will, once again by the law of the junction, change the existing electron concentration at the base-edge of the B-C SCL to the new value
$$
\begin{equation*}
n_{B}\left(W_{B}\right)=n_{B 0} e^{v_{B d} / V_{T}}=n_{B 0} e^{-v_{c c} / V_{T}} \tag{2.8}
\end{equation*}
$$
where $W_{B}$ denotes the effective base width, defined as the distance between the base edges of the two SCLs. With a reverse bias of as little as 0.2 V , Eq. (2.8) gives $n_{B}\left(W_{B}\right) \cong\left(2 \times 10^{2}\right) e^{-200 / 26} \cong\left(2 \times 10^{2}\right) / 2191 \cong 0.1 \mathrm{~cm}^{-3}$, which for practical purposes can be regarded as 0 compared to other concentrations. Given that the base is fabricated deliberately very thin, the electron distribution in the base takes on a straight-line profile, as shown. Were the base made wide, the distribution profile would be an exponential decay, indicating that most electrons would recombine in
the base and thus fail to make it successfully to the collector. We can see why it is critical that the base be fabricated very thin (typically a fraction of a $\mu \mathrm{m}$ ).
### The Collector Current
It is apparent that operating the BJT in the forward-active mode, as depicted in Fig. 2.6, establishes an excess of minority carriers (electrons, in the present case) in its base region. This excess electron distribution, defined as
$$
n_{B}^{\prime}(x)=n_{B}(x)-n_{B 0}
$$
is shown in Fig. 2.7, along with its values at $x=0$ and $x=W_{B}$. Once injected into the base, the excess electrons diffuse towards the SCL of the B-C junction, where the electric field $E_{C B}$ sweeps them away from the base, through the SCL, and into the collector region, from where they proceed toward the collector electrode (see Fig. 2.6). Electron diffusion within the base region is governed by the diffusion equation
$$
\begin{equation*}
J_{n}=q D_{n} \frac{d n_{B}^{\prime}(x)}{d x} \tag{2.9}
\end{equation*}
$$
where $J_{n}$ is the electron current density (in $\mathrm{A} / \mathrm{cm}^{2}$ ), $q$ is the electron charge, and $D_{n}$ is the electron diffusion constant, also called electron diffusivity (in $\mathrm{cm}^{2} / \mathrm{s}$ ). Calculating the slope of the triangle, we get
$$
J_{n}=q D_{n}\left[-\frac{n_{B 0}\left(e^{v_{B E} / V_{T}}-1\right)-\left(-n_{B 0}\right)}{W_{B}}\right]=-\frac{q D_{n} n_{B 0}}{W_{B}} e^{v_{B E} / V_{T}}
$$
where the negative sign indicates that the direction of $J_{n}$ is opposite to $x$, that is, from right to left. This is not surprising, as $J_{n}$ is due to the flow of electrons, which are negative.
The collector current $i_{C}$ (in A) is obtained by multiplying the current density $J_{n}$ by the emitter area $A_{E}$ (in $\mathrm{cm}^{2}$ ) shared by the solid-state emitter diffusion with the base region in Fig. 2.1. Choosing the direction of $i_{C}$ from right to left as in Fig. 2.6 allows us to write $i_{C}=-A_{E} J_{n}$, and thus avoid the negative sign of $J_{n}$. Using also $n_{B 0}=n_{i}^{2} / p_{B 0} \cong n_{i}^{2} / N_{A B}$, we put $i_{C}$ in the insightful form
$$
\begin{equation*}
i_{C}=I_{S} e^{v_{B E} / V_{T}} \tag{2.10}
\end{equation*}
$$
where
$$
\begin{equation*}
I_{s}=A_{E} \times \frac{1}{W_{B}} \times n_{i}^{2}(T) \times \frac{q D_{n}}{N_{A B}} \tag{2.11}
\end{equation*}
$$
Called the collector saturation current, $I_{s}$ is just a scale factor giving a measure of how much collector current $i_{C}$ a BJT will provide for a given voltage drive $v_{B E}$. For
image_name:FIGURE 2.6
description:The diagram in FIGURE 2.6 illustrates the operation of an npn Bipolar Junction Transistor (BJT) in the forward active mode. It is divided into two main sections: the top part shows the relevant currents, and the bottom part displays the minority-carrier distributions.
Top Section: Relevant Currents
- **Currents and Voltages:**
- The emitter current \(i_E\) flows from the emitter \(E\) to the base \(B\).
- The base current \(i_B\) flows into the base \(B\).
- The collector current \(i_C\) flows out of the collector \(C\).
- The voltage \(v_{BE}\) across the base-emitter junction is approximately 0.7 V, indicating forward bias.
- The voltage \(v_{CB}\) across the collector-base junction is greater than 0.2 V, indicating reverse bias.
- **Electron Flow:**
- Arrows indicate the flow of electrons, showing that electrons move from the emitter to the collector via the base.
- The electron flow is opposite to the conventional current direction.
### Bottom Section: Minority-Carrier Distributions
- **Carrier Concentrations:**
- The diagram shows the distribution of minority carriers (electrons in the p-region and holes in the n-regions) across the transistor.
- The x-axis represents the position \(x\) across the transistor, divided into regions: \(n^+\) emitter, \(p\) base, and \(n^-\) collector.
- The y-axis represents the concentration of carriers \(n, p\) in \(\text{cm}^{-3}\).
- **Emitter Region \(n^+\):**
- Carrier concentration \(p_{E0}\) is approximately \(2 \times 10^0\) at the emitter edge.
- The concentration linearly decreases towards the base.
- **Base Region \(p\):**
- The electron concentration \(n_B\) starts at \(n_B(0) \approx 10^{14}\) and decreases linearly to \(n_B(W_B) \approx 0\).
- **Collector Region \(n^-\):**
- Carrier concentration \(p_{C0}\) is approximately \(2 \times 10^4\) at the collector edge.
- The concentration linearly decreases towards the base.
Key Features and Technical Details
- **Base Width \(W_B\):**
- The base width \(W_B\) is indicated, showing the region where minority carrier recombination occurs.
- **Emitter and Collector Widths \(W_E, W_C\):**
- The widths of the emitter \(W_E\) and collector \(W_C\) are shown, indicating the regions where the majority carriers dominate.
Annotations
- The diagram is annotated with relevant voltages and currents, helping to visualize the operation of the BJT in the forward active mode.
- The minority-carrier distribution graph provides insight into how carrier concentrations change across the different regions of the transistor, crucial for understanding the transistor's operation.
FIGURE 2.6 The npn BJT operating in the forward active mode: top: relevant currents; bottom: minority-carrier distributions.
low-power BJTs, $I_{s}$ is typically in the range of femto-amperes ( $1 \mathrm{fA}=10^{-15} \mathrm{~A}$.) We make the following important observations:
- $I_{s}$ is directly proportional to the emitter area. The larger the emitter, the more current the collector will draw for a given drive $v_{B E}$. Indeed, power BJTs have suitably large emitters.
- $I_{s}$ is inversely proportional to the base width $W_{B}$. The narrower the base, the steeper the distribution of Fig. 2.7 for a given drive $v_{B E}$. Also, this dependence upon $W_{B}$ is at the basis of the Early effect, to be discussed in Section 2.3.
- $I_{s}$ is a strong function of temperature, especially because of $n_{i}^{2}(T)$. Engineers quantify temperature dependence via the following useful rule of thumb:
The collector saturation current $I_{s}$ doubles for about every $5^{\circ} \mathrm{C}$ of temperature increase
image_name:Figure 2.7
description:The graph in Figure 2.7 is a plot representing the excess minority carrier distribution in the base of a bipolar junction transistor (BJT). The graph is a triangular distribution with the following characteristics:
1. **Type of Graph and Function:**
- This is a linear distribution graph showing the excess minority carrier concentration as a function of position within the base of a BJT.
2. **Axes Labels and Units:**
- The horizontal axis (x-axis) is labeled as \( x \), representing the position within the base, with units not specified but typically in micrometers or similar for semiconductor devices.
- The vertical axis (y-axis) is labeled as \( n'_{B}(x) \), representing the excess minority carrier concentration.
- The graph spans from \( x = 0 \) to \( x = W_{B} \), where \( W_{B} \) is the base width.
3. **Overall Behavior and Trends:**
- The graph shows a linear decrease in excess minority carrier concentration from a maximum at \( x = 0 \) to zero at \( x = W_{B} \).
- This linear trend indicates a steady depletion of excess carriers as they move through the base.
4. **Key Features and Technical Details:**
- The slope of the line is proportional to the current \( J_{n} \), indicating that the current is driven by the gradient of the carrier concentration.
- The area under the curve, shaded in grey, represents the excess charge \( Q_{n} \) in the base.
- The maximum excess carrier concentration at \( x = 0 \) is given by \( n'_{B0}(e^{v_{BE}/V_{T}} - 1) \), where \( v_{BE} \) is the base-emitter voltage and \( V_{T} \) is the thermal voltage.
- The concentration at \( x = W_{B} \) is \( -n'_{B0} \), indicating the boundary condition at the collector side of the base.
5. **Annotations and Specific Data Points:**
- The graph includes annotations for \( J_{n} \) and \( Q_{n} \), highlighting the proportionality of the current to the slope and the representation of excess charge by the area, respectively.
- The endpoints of the graph are clearly marked at \( x = 0 \) and \( x = W_{B} \), with the respective values of the carrier concentration noted.
FIGURE 2.7 Excess minority carrier distribution in the base. The current $J_{n}$ is proportional to the slope, and the excess charge $Q_{n}$ is proportional to the area.
Taking the logarithm of both sides of Eq. (2.10), and solving for $v_{B E}$, we get
$$
\begin{equation*}
v_{B E}=V_{T} \ln \frac{i_{C}}{I_{s}} \tag{2.12}
\end{equation*}
$$
This allows us to find the voltage $v_{B E}$ necessary to sustain a given current $i_{C}$.
EXAMPLE 2.1 Consider a BJT with emitter area $A_{E}=(100 \mu \mathrm{~m}) \times(100 \mu \mathrm{~m})$ and base width $W_{B}=0.5 \mu \mathrm{~m}$, along with $D_{n}=10 \mathrm{~cm}^{2} / \mathrm{s}$ and the doping doses of Eq. (2.1).
(a) Find $I_{s}$.
(b) Find $i_{C}$ if $v_{B E}=700 \mathrm{mV}$.
(c) Find $v_{B E}$ for $i_{C}=1.0 \mathrm{~mA}$.
(d) Find the square area $A_{E}$ needed to achieve $i_{C}=1 \mathrm{~mA}$ with $v_{B E}=700 \mathrm{mV}$.
#### Solution
(a) By Eq. (2.11),
$$
\begin{aligned}
I_{s} & =\frac{100 \times 10^{-4} \times 100 \times 10^{-4} \times 2 \times 10^{20} \times 1.602 \times 10^{-19} \times 10}{0.5 \times 10^{-4} \times 10^{18}} \\
& =0.64 \mathrm{fA}
\end{aligned}
$$
(b) By Eq. (2.10),
$$
i_{C}=0.64 \times 10^{-15} e^{700 / 26}=0.316 \mathrm{~mA}
$$
(c) By Eq. (2.12),
$$
v_{B E}=0.026 \ln \frac{1 \times 10^{-3}}{0.64 \times 10^{-15}}=730 \mathrm{mV}
$$
(d) From part (b) we find that $A_{E}$ needs to be scaled in proportion as
$$
A_{E}=\frac{1.0 \mathrm{~mA}}{0.316 \mathrm{~mA}}(100 \mu \mathrm{~m}) \times(100 \mu \mathrm{~m})=(178 \mu \mathrm{~m}) \times(178 \mu \mathrm{~m})
$$
### The Three Base-Current Components
With reference to Fig. 2.6, top, we observe that the base current consists of three components, denoted as $i_{B E}, i_{B B}$, and $i_{B C}$. Let us examine each one in detail.
- The component $i_{B E}$ consists of holes injected into the emitter. This component is the counterpart of the electrons injected into the base, so we can adapt Eqs. (2.10) and (2.11) to the case of holes injected into the emitter and write
$$
\begin{equation*}
i_{B E}=\frac{A_{E} n_{i}^{2}(T) q D_{p}}{W_{E} N_{D E}} e^{v_{B E} / V_{T}} \tag{2.13}
\end{equation*}
$$
where $D_{p}$ is the hole diffusivity and $W_{E}$ the emitter width, also referred to as the emitter length.
- The component $i_{B B}$ consists of holes recombining with the electrons transiting from emitter to collector. To develop an expression for this component, we observe that in the forward active mode the BJT sustains a cloud of excess electrons in its base region. Call its total charge $Q_{n}$. If a transiting electron takes on average $\tau_{n}$ seconds to recombine with a hole in the base region, then the excess charge lost to recombination in one second is $Q_{n} / \tau_{n}$, and its negative is precisely the hole current $i_{B B}$ needed to replenish the holes lost to recombination.
To obtain an expression for $Q_{n}$, refer to Fig. 2.8 and consider a vertical slice of thickness $d x$. The volume of this slice is $A_{E} d x$. To find the excess charge $d Q_{n}(x)$ inside this slice, first multiply its volume by $n_{B}^{\prime}(x)$ to find the number of excess electrons, and then multiply by $-q$ to find the charge itself, or $d Q_{n}(x)=$ $-n_{B}^{\prime}(x) q A_{E} d x$. The total excess charge within the base region is then found by integrating over the length of this region,
$Q_{n}=-q A_{E} \int_{0}^{W_{B}} n_{B}^{\prime}(x) d x=-q A_{E} \frac{W_{B}\left[n_{B 0}\left(e^{v_{B E} / V_{T}}-1\right)-\left(-n_{B 0}\right)\right]}{2}=-\frac{q A_{E} n_{i}^{2}(T) W_{B}}{2 N_{A E}} e^{v_{B E} / V_{T}}$
where we have used simple geometry to find the area of the triangle, and have also substituted $n_{B 0}=n_{i}^{2} / N_{A E}$. Letting $i_{B B}=-Q_{n} / \tau_{n}$, we finally get
$$
\begin{equation*}
i_{B B}=\frac{q A_{E} n_{i}^{2}(T) W_{B}}{2 \tau_{n} N_{A E}} e^{v_{B E} / V_{T}} \tag{2.14}
\end{equation*}
$$
where $\tau_{n}$ is called the mean electron lifetime in the base.
image_name:FIGURE 2.8 Calculating the excess charge Q_n in the base region.
description:The graph in "FIGURE 2.8 Calculating the excess charge Q_n in the base region" is a three-dimensional plot illustrating the distribution of charge carriers in the base region of a bipolar junction transistor (BJT).
1. **Type of Graph and Function:**
- This is a 3D geometric representation showing the variation of excess electron concentration across the base region of a BJT.
2. **Axes Labels and Units:**
- The vertical axis represents the electron concentration, labeled as \( n'_B(x) \), and is a function of position \( x \) across the base.
- The horizontal axis represents the position \( x \) within the base, ranging from \( 0 \) to \( W_B \), where \( W_B \) is the width of the base.
- The third dimension, perpendicular to the \( x \)-axis, is implicit and represents the variation in concentration due to the applied base-emitter voltage \( V_{BE} \).
3. **Overall Behavior and Trends:**
- The graph depicts a linearly increasing electron concentration from \( -n_{B0} \) at \( x = 0 \) to a higher concentration at \( x = W_B \). This increase is due to the term \( n_{B0} (e^{v_{BE}/V_T} - 1) \), which represents the exponential increase in carrier concentration with applied voltage.
4. **Key Features and Technical Details:**
- The shaded region represents the excess charge \( Q_n \) in the base, which is the integration of the concentration over the base width.
- The line \( n'_B(x) \) shows how the concentration changes linearly across the base.
- The differential element \( dQ_n \) is illustrated, indicating the infinitesimal change in charge across an infinitesimal width \( dx \).
5. **Annotations and Specific Data Points:**
- The graph includes annotations such as \( dQ_n \) and \( dx \) to highlight the differential element of charge and width.
- The base width \( W_B \) is marked on the x-axis, and the concentration at \( x = 0 \) is shown as \( -n_{B0} \).
Overall, the graph provides a visual understanding of how the excess charge in the base of a BJT is distributed and calculated, emphasizing the dependence on both the position within the base and the applied base-emitter voltage.
FIGURE 2.8 Calculating the excess charge $Q_{n}$ in the base region.
- The component $i_{B C}$ accounts for the thermal generation of electron-hole pairs within the SCL of the reverse-biased B-C junction. Once generated, holes and electrons are swept into opposite directions by the strong electric field $E_{C B}$ present there. Depending on the quality of fabrication, surface leakage may also be present. BJT data sheets usually report $I_{C B 0}$, the C-B leakage current with the emitter open. At room temperature, $I_{C B 0}$ is typically in the range of 1 nA to 1 pA , and since it is so small, it is usually ignored in the course of hand calculations. However, this current is a strong function of temperature, something that engineers quantify via the following rule of thumb:
The leakage current $I_{C B 0}$ doubles for about every $10^{\circ} \mathrm{C}$ of temperature increase
Consequently, if sufficiently high operating temperatures are anticipated, it may prove necessary to take the leakage current into account even in the course of our hand analysis.
Looking back at Fig. 2.6 we observe that all base-current components consist of holes. Yet, the base electrode, usually made of metal, conducts only by electron flow. It follows that in order to ensure the continuity between the two current types, free electron-hole pairs must be generated automatically right at the metal-base interface. Once generated, holes progress into the base region to sustain $i_{B E}+i_{B B}$, while electrons drift up the base wire to sustain $i_{B}$.
A fraction of the holes needed to sustain $i_{B E}+i_{B B}$ comes also from the collector, in the form of $i_{B C}$. As mentioned, $i_{B C}$ increases with temperature. It is worth mentioning that we can increase $i_{B C}$ also by shining light upon the B-C SCL. As the quanta of light impinge upon the crystal, they impact enough energy to create free hole-electron pairs, which are then swept into opposite directions by the electric field present there. With sufficient light, the current of holes from collector to base can be raised to the point of turning the BJT convincingly on, with no need for any externally supplied current $i_{B}$ ! When used as a light-controlled device, the BJT is called a phototransistor and finds application as part of an optocoupler. An optocoupler consists of a lightemitting diode (LED) and a phototransistor mounted in the same package. Forcing current through the LED causes it to emit light, which then turns on the BJT. Since the LED and the BJT are coupled only via light, they can be part of separate circuits and thus provide galvanic isolation between the two. We can also couple a LED and a BJT via a fiber optic, thus allowing for the transmission of information over long distances and with minimal signal loss and interference.
### The Forward Current Gain $\boldsymbol{\beta}_{\boldsymbol{F}}$
The base current in the forward active mode of operation is $i_{B}=i_{B E}+i_{B B}-i_{B C}$. As mentioned, we usually ignore $i_{B C}$ and write $i_{B} \cong i_{B E}+i_{B B}$. Using Eqs. (2.13) and (2.14), along with Eqs. (2.10) and (2.11), we put $i_{B}$ in the insightful form
$$
i_{B}=\left(\frac{D_{p}}{D_{n}} \frac{N_{A B}}{N_{D E}} \frac{W_{B}}{W_{E}}+\frac{W_{B}^{2}}{2 \tau_{n} D_{n}}\right) I_{s} e^{v_{B E} / V_{T}}
$$
Comparing with Eq. (2.10), we observe that $i_{B}$ is linearly proportional to $i_{C}$, a relationship expressed as
$$
i_{B}=\frac{i_{C}}{\beta_{F}}
$$
where $\beta_{F}$ is the forward current gain mentioned earlier,
$$
\begin{equation*}
\beta_{F}=\frac{1}{\frac{D_{p}}{D_{n}} \frac{N_{A B}}{N_{D E}} \frac{W_{B}}{W_{E}}+\frac{W_{B}^{2}}{2 \tau_{n} D_{n}}} \tag{2.15}
\end{equation*}
$$
This expression confirms the already familiar criteria for the fabrication of high-beta BJTs:
- Make $W_{B}$ small by fabricating the base very thin
- Make the ratio $N_{D E} / N_{A B}$ large by doping the emitter much more heavily than the base.
Equation (2.15) reveals two additional features that the manufacturer can exploit to $\operatorname{maximize} \beta_{F}$ : (a) fabricate the emitter long $\left(W_{E} \gg W_{B}\right)$ to further reduce $i_{B E}$; (b) create favorable conditions for a long minority-carrier lifetime in the base (long $\tau_{n}$ for $n p n$ BJTs, and long $\tau_{p}$ for pnp BJTs) to lower $i_{B B}$ further.
Assuming $\beta_{F}=100$ in the BJT of Fig. 2.9a, find all terminal currents (a) first for the case in which the collector terminal is left disconnected, and (b) then with the collector connected to the $+5-\mathrm{V}$ supply, as shown. Discuss the various current components as well as the main differences between the two cases.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: +5V, B: GND, E: E}
name: E, type: Resistor, value: 4.3kΩ, ports: {N1: E, N2: -5V}
]
extrainfo:In this circuit, the collector of the NPN transistor Q1 is left disconnected, resulting in no collector current (IC = 0). The base-emitter junction acts as a diode, with the emitter current (IE) calculated as 1.0 mA. The base current (IB) equals the emitter current in this configuration.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: +5 V, B: GND, E: E}
name: R1, type: Resistor, value: 4.3 kΩ, ports: {N1: E, N2: -5 V}
name: V1, type: VoltageSource, value: +5 V, ports: {Np: +5 V, Nn: GND}
name: V2, type: VoltageSource, value: -5 V, ports: {Np: GND, Nn: -5 V}
]
extrainfo:The circuit in diagram (b) includes an NPN transistor Q1 with its collector connected to +5V, base to GND, and emitter through a 4.3 kΩ resistor to -5V. The collector current is 0.99 mA, base current is 9.9 μA, and emitter current is 1.0 mA.
image_name:(c)
description:
[
name: Q1, type: NPN, ports: {C: +5V, B: GND, E: E}
name: E, type: Resistor, value: 4.3kΩ, ports: {N1: E, N2: -5V}
]
extrainfo:The circuit contains an NPN transistor Q1 with its collector connected to +5V, base connected to GND, and emitter connected to a resistor E of 4.3kΩ, which is then connected to -5V. The current through the emitter is 1.0 mA, and the base current is 9.9 µA. The collector current is 0.99 mA.
FIGURE 2.9 Circuit of Example 2.2.
#### Solution
(a) Leaving the collector disconnected results in $I_{C}=0$. The only functioning part of the BJT is now its B-E junction, which acts as a plain diode with the base as the anode and the emitter as the cathode. Assuming a typical junction voltage-drop of 0.7 V , the emitter is at -0.7 V , so the emitter current is
$$
I_{E}=\frac{-0.7-(-5)}{4.3}=1.0 \mathrm{~mA}
$$
Since $I_{C}=0$ (collector disconnected), we must have $I_{B}=I_{E}=1.0 \mathrm{~mA}$. The situation is depicted in Fig. 2.9b, where we observe that both $I_{E}$ and $I_{B}$ consist primarily of electrons injected from the emitter into the base region and thence progressing to the base terminal. Additionally, there is a current of holes injected from the base into the emitter, as it is the case with all pn junctions, but this component is much smaller because of the much heavier emitter doping. In this situation the BJT works as an ordinary pn diode.
(b) Connecting the collector to the $+5-\mathrm{V}$ supply reverse biases the $\mathrm{B}-\mathrm{C}$ junction, making it now possible for the electrons injected into the thin base to proceed to the positively biased collector. A few will recombine with the many holes in the base, but the majority will now make it to the collector. We now have
$$
I_{B}=\frac{I_{C}}{\beta_{F}}=\frac{I_{E}-I_{B}}{\beta_{F}}
$$
or
$$
I_{B}=\frac{I_{E}}{\beta_{F}+1}
$$
Presently, $I_{B}=1.0 / 101=9.9 \mu \mathrm{~A}$ and $I_{C}=100 \times 9.9=0.99 \mathrm{~mA}$. The situation is shown in Fig. 2.9c, where the main event now is electron flow from E to C.
#### Exercise 2.1
Three students are debating whether one can synthesize a BJT simply by connecting two discrete $p n$ junctions back to back. The first student proposes creating a homebrew npn BJT by connecting together the anodes of the two discrete diodes to obtain the $p$-type base, and then using one of the cathodes as the $n$-type emitter, and the other as the $n$-type collector. The second student claims that the resulting device won't provide any base-current amplification. Why? List two main reasons. After hearing the arguments of the second student, the third student comes up with a better alternative, namely, using the B-E junction of one npn BJT and the $\mathrm{B}-\mathrm{C}$ junction of a different $n p n$ BJT to guarantee the relative doping constraints needed of a BJT, and then connecting their base terminals together to form the base of the composite device (the collector terminal of the first BJT and the emitter terminal of the second BJT are left disconnected). The second student claims that the device still won't work as a current amplifier. Why?
(a) Assuming Eq. (2.15) gives $\beta_{F}=1 /(1 / 150+1 / 300)=100$ for the BJT of
#### ExAMPLE 2.3
Fig. 2.9c, find $I_{B}$ as well as the base current components $I_{B E}$ and $I_{B B}$.
(b) What happens if the manufacturer reduces $W_{B}$ in half? What if the manufacturer doubles $W_{B}$ ?
#### Solution
(a) We easily find
$$
I_{B}=I_{B E}+I_{B B}=\frac{I_{C}}{\beta_{F}}=\left(\frac{1}{150}+\frac{1}{300}\right) 0.99 \mathrm{~mA}=6.6 \mu \mathrm{~A}+3.3 \mu \mathrm{~A}=9.9 \mu \mathrm{~A}
$$
(b) Considering that the denominator terms in Eq. (2.15) involve both $W_{B}$ and $W_{B}^{2}$, it is apparent that halving $W_{B}$ gives
$$
\beta_{F}=\frac{1}{\frac{1}{150}(0.5)+\frac{1}{300}(0.5)^{2}}=\frac{1}{\frac{1}{300}+\frac{1}{1200}}=240
$$
Retracing similar calculations, we still get $I_{E}=1.0 \mathrm{~mA}$. However, we now have $I_{B}=1.0 / 241=4.15 \mu \mathrm{~A}, I_{C}=0.996 \mathrm{~mA}, I_{B E}=3.32 \mu \mathrm{~A}$, and $I_{B B}=$ $0.83 \mu \mathrm{~A}$. Doubling $W_{B}$ gives $\beta_{F}=1 /(1 / 75+1 / 75)=37.5, I_{B}=1.0 / 38.5=$ $26 \mu \mathrm{~A}, I_{C}=0.974 \mathrm{~mA}, I_{B E}=I_{B B}=13 \mu \mathrm{~A}$.
### A Practical Application: The BJT as a Current Booster
To start appreciating the usefulness of the BJT, let us examine what could easily be a hobbyist's project: the design of a $5-\mathrm{V}, 200-\mathrm{mA}$ regulated power supply starting from an unregulated voltage source such as a $12-\mathrm{V}$ car battery. Based on the knowledge acquired so far, we could start out with the design of Fig. 2.10a. Here, the LM336-5.0 diode provides a high-quality $5-\mathrm{V}$ voltage reference, which we then buffer to the load
image_name:(a)
description:
[
name: VDD, type: VoltageSource, value: 12V, ports: {Np: VDD, Nn: GND}
name: R1, type: Resistor, value: 3.0kΩ, ports: {N1: VDD, N2: Vz}
name: LM336-5.0, type: Diode, ports: {Na: GND, Nc: Vz}
name: OpAmp1, type: OpAmp, value: 741, ports: {InP: Vz, InN: Vo, Out: Vo, Vdd: VDD, -Vdd: GND}
]
extrainfo:The circuit is a 5V regulated power supply using a 741 op-amp and LM336-5.0 diode with a 3.0kΩ resistor. It is powered by a 12V source and is capable of driving loads up to approximately 25mA.
image_name:(b)
description:
[
name: 12 V, type: VoltageSource, value: 12 V, ports: {Np: VDD, Nn: GND}
name: 3.0 kΩ, type: Resistor, value: 3.0 kΩ, ports: {N1: VDD, N2: Vo}
name: LM336-5.0, type: Diode, ports: {Na: Vo, Nc: GND}
name: 741, type: OpAmp, ports: {InP: Vo, InN: GND, OutP: B, OutN: GND}
name: NPN, type: NPN, ports: {C: VDD, B: B, E: Vo}
name: LD, type: Other, ports: {N1: Vo, N2: GND}
]
extrainfo:This circuit is a regulated power supply using a BJT as a current booster. The BJT increases the output current drive capability of the op-amp. The LM336-5.0 provides a 5V reference voltage, and the 741 op-amp is configured as a voltage follower. The circuit is powered by a 12V source, and the load can draw up to 200mA.
FIGURE 2.10 Showing the use of a BJT to increase the output current drive capability of an op amp.
via a 741 op amp connected as a voltage follower. This circuit will work properly but only for load currents of up to about 25 mA , which the data-sheets report as the maximum output-current capability of the 741 op amp . If the circuitry that we intend to power, here denoted as a load LD, attempts to draw a current $I_{L}$ exceeding this value, the output voltage will simply drop, and regulation will be lost.
But this is precisely where the BJT comes to our rescue! If we interpose a BJT between the op amp and the load as in Fig. 2.10b, the op amp's output current will get boosted by $\beta_{F}+1$, as seen in Example 2.2, thus causing a much heftier current to flow from the unregulated 12-V source, through the BJT, to the load. Circuit behavior is governed by the familiar op amp rule, stating that the op amp will provide whatever output voltage and current it takes to make its inverting input voltage ( $V_{o}$ ) in this case) track its non-inverting input voltage $\left(V_{Z}\right)$. In our case the op amp must source to the BJT the current
$$
I_{B}=\frac{I_{E}}{\beta_{F}+1}=\frac{200 \mathrm{~mA}}{100+1}=1.98 \mathrm{~mA}
$$
which is well within the $25-\mathrm{mA}$ capability of the 741 op amp. Assuming a typical B-E junction voltage drop of about 0.7 V , we observe that the op amp must also supply the base voltage
$$
V_{B}=V_{B E}+V_{E} \cong 0.7+5.0=5.7 \mathrm{~V}
$$
But this too is well within the 741's output voltage capability.
In the application just illustrated the BJT is put to use to boost the output current drive capability of a low-power device such as an op amp. In this function, the BJT finds application in a wide variety of power-related circuits, of which regulated power supplies and audio power amplifiers are two common examples. Even though voltage regulators are available in IC form, it is instructive for the beginner to assemble the circuits of Fig. 2.10 and try them out in the lab.
### The pnp BJT Operating in the Forward-Active Mode
Figure 2.11 shows the relevant currents inside the pnp BJT. Comparing it with its npn counterpart of Fig. 2.6, we note a strong similarity, except for the interchange of holes and electrons, as well as a reversal in voltage polarities and current directions. As we know, the main event now is a hole flow from the emitter, through the thin base, and onto the collector. Without repeating the derivations, we can simply recycle the results developed for the npn BJT and write
$$
\begin{equation*}
i_{C}=I_{s} e^{v_{E B} / V_{T}} \tag{2.16}
\end{equation*}
$$
where
$$
\begin{equation*}
I_{s}=A_{E} \times \frac{1}{W_{B}} \times n_{i}^{2}(T) \times \frac{q D_{p}}{N_{D B}} \tag{2.17}
\end{equation*}
$$
image_name:FIGURE 2.11 Relevant currents in a pnp BJT operating in the forward active mode.
description:The diagram illustrates the operation of a pnp BJT in forward active mode, showing the flow of various currents: i_E, i_B, i_C, i_EB, i_BB, and i_BC. The emitter-base voltage (VEB) is approximately 0.7V, and the base-collector voltage (VBC) is at least 0.2V.
FIGURE 2.11 Relevant currents in a pnp BJT operating in the forward active mode.
Here, $D_{p}$ is the hole diffusivity and $N_{D B}$ the donor concentration in the base. Moreover, we have
$$
\begin{equation*}
\beta_{F}=\frac{1}{\frac{D_{n}}{D_{p}} \frac{N_{D B}}{N_{A E}} \frac{W_{B}}{W_{E}}+\frac{W_{B}^{2}}{2 \tau_{p} D_{p}}} \tag{2.18}
\end{equation*}
$$
where $D_{n}$ is the electron diffusivity, $N_{D B}$ is the donor concentration in the base, $N_{A E}$ is the acceptor concentration in the emitter, and $\tau_{p}$ is the mean hole lifetime in the base.
Equations (2.11) and (2.17) reveal an additional interesting feature, namely, that the scale factor $I_{s}$ is proportional to the diffusivity $\left(D_{n}\right.$ or $\left.D_{p}\right)$ of the charges producing the main current in the BJT. This is not surprising, as the collector current is of the diffusion type. When studying MOSFETs, in the next chapter, we will encounter a similar scale factor, called the transconductance parameter $k$, which instead is proportional to the mobility ( $\mu_{n}$ or $\mu_{p}$ ) of the charges responsible for the main current in the device. This is so because MOSFET current is of the drift type. Figure 1.37 shows that for a given doping density, electron mobility and diffusivity are two to three times higher than hole mobility and diffusivity, respectively. For these reasons, $n p n$ BJTs are generally preferred over $p n p$ types, and $n$-channel FETs are preferred over $p$-channel types.
### Dependence of $\boldsymbol{\beta}_{\boldsymbol{F}}$ Upon $\boldsymbol{I}_{\boldsymbol{c}}$ and $\boldsymbol{T}$
The current gain $\beta_{F}$ is not constant but varies both with the operating current $I_{C}$ and the temperature $T$. This is illustrated in Fig. 2.12 for the case of the popular 2N2222 BJT. For a fixed value of $T$, say $T=25{ }^{\circ} \mathrm{C}, \beta_{F}$ is approximately constant only in the neighborhood of $I_{C}=100 \mu \mathrm{~A}$ for this particular device. At higher current levels $\beta_{F}$ decreases due to current crowding as well as high-level injection effects. ${ }^{1} \mathrm{At}$ lower current levels it decreases due to carrier recombination inside the B-E SCL. ${ }^{1}$
image_name:(a)
description:
[
name: Q, type: NPN, ports: {C: V_CE, B: Vb, E: GND}
name: V_CE, type: VoltageSource, value: 1V, ports: {Np: V_CE, Nn: GND}
]
extrainfo:The circuit demonstrates the dependence of the current gain (βF) of a 2N2222 BJT on the collector current (IC) and temperature (T). The plot shows βF at different temperatures (125°C, 25°C, -55°C) over a range of IC values.
image_name:(b)
description:The graph in part (b) of Figure 2.12 is a plot showing the relationship between the current gain, denoted as $\beta_F$, and the collector current, $I_C$, for a 2N2222 BJT transistor. This relationship is illustrated at three different temperatures: $T = 125^{\circ}C$, $T = 25^{\circ}C$, and $T = -55^{\circ}C$.
1. **Type of Graph and Function:**
- The graph is a logarithmic plot of current gain ($\beta_F$) versus collector current ($I_C$).
2. **Axes Labels and Units:**
- The x-axis represents the collector current, $I_C$, in microamperes (µA) and is plotted on a logarithmic scale.
- The y-axis represents the current gain, $\beta_F$, which is dimensionless.
3. **Overall Behavior and Trends:**
- For each temperature, the graph shows a rise in $\beta_F$ with increasing $I_C$, reaching a peak, and then decreasing as $I_C$ continues to increase.
- The peak values of $\beta_F$ occur at different $I_C$ levels depending on the temperature.
4. **Key Features and Technical Details:**
- At $T = 25^{\circ}C$, $\beta_F$ is approximately constant near $I_C = 100 \mu A$, which is a notable point where $\beta_F$ is stable.
- As temperature increases to $T = 125^{\circ}C$, the peak $\beta_F$ is higher and occurs at a higher $I_C$ compared to lower temperatures.
- Conversely, at $T = -55^{\circ}C$, the peak $\beta_F$ is lower and occurs at a lower $I_C$.
5. **Annotations and Specific Data Points:**
- The graph shows three distinct curves for the three temperatures, each labeled accordingly.
- The curves demonstrate how $\beta_F$ varies with both $I_C$ and temperature, highlighting the temperature dependence of the transistor's performance.
This graph effectively illustrates the impact of temperature on the current gain of a 2N2222 BJT, showing that $\beta_F$ is not constant across different $I_C$ levels and temperatures, which is critical for understanding the device's behavior in different conditions.
FIGURE 2.12 (a) PSpice circuit to display (b) the dependence of $\beta_{F}$ on $I_{C}$ and $T$ for the 2N2222 BJT.
This results in an additional base-current component that, though always present, becomes relevant only at low current levels. Unless stated to the contrary, we shall assume constant $\beta_{F}$ throughout for simplicity.
## 2.3 THE i-v CHARACTERISTICS OF BJTS
The most important characteristics of an npn BJT are the forward active plot of $i_{C}$ versus $v_{B E}$, and the plot of $i_{C}$ versus $v_{C E}$ for different $\mathrm{B}-\mathrm{E}$ driving conditions. Since the B-E junction can be either voltage driven or current driven, we have two families of curves, one obtained by plotting $i_{C}$ versus $v_{C E}$ for different values of $V_{B E}$, and the other by plotting $i_{C}$ versus $v_{C E}$ for or different values of $I_{B}$. Each family offers valuable insight into BJT operation. It is understood that the body of knowledge that we shall acquire for the npn BJT can readily be extended to its pnp counterpart by interchanging holes and electrons as well as reversing voltage polarities and current directions. The various $i-v$ curves can be displayed either in the lab, via an oscilloscope equipped with a suitable curve-tracer module, or on a computer monitor via PSpice. In the following we shall use the popular 2N2222 npn BJT as a working example. The reader is encouraged to perform a web search for the data sheets of popular BJTs such as the 2N2222 type, and consult them frequently to develop a feel for the practical side of the theory we are going to study.
### The Exponential Characteristic
Figure 2.13a shows a PSpice circuit to display the $i_{C}-v_{B E}$ characteristic of the 2N2222 npn BJT using the model available in PSpice's library (See Appendix 2A). The result, shown in Fig. 2.13b, is the familiar exponential curve predicted by Eq. (2.10), albeit with a minor modification to be discussed below, in connection with Eq. (2.21). The PSpice model uses $I_{s}=14.34 \mathrm{fA}$. Recall that the B-E junction acts like an ordinary $p n$ diode, except that almost all electrons injected into the base go to the collector
image_name:(a)
description:
[
name: Q, type: NPN, ports: {C: V_CE, B: V_BE, E: GND}
name: V_BE, type: VoltageSource, value: V_BE, ports: {Np: V_BE, Nn: GND}
name: V_CE, type: VoltageSource, value: 1V, ports: {Np: V_CE, Nn: GND}
]
extrainfo:The circuit displays the i_C-v_BE characteristic of the 2N2222 NPN BJT. The BJT is biased with V_BE and V_CE to observe the exponential i-v curve. V_BE is the input voltage controlling the base-emitter junction, while V_CE is set to 1V to provide the collector-emitter voltage.
image_name:(b)
description:The graph in Fig. 2.13b illustrates the $i_C-v_{BE}$ characteristic curve of the 2N2222 NPN BJT. This graph is an exponential $i-v$ curve characteristic of a bipolar junction transistor (BJT), specifically focusing on the collector current ($i_C$) versus the base-emitter voltage ($v_{BE}$).
1. **Type of Graph and Function:**
- This is an exponential $i-v$ curve, typical for BJTs, showing the relationship between the collector current and the base-emitter voltage.
2. **Axes Labels and Units:**
- The x-axis is labeled $v_{BE}$ (mV), representing the base-emitter voltage in millivolts.
- The y-axis is labeled $i_C$ (mA), representing the collector current in milliamperes.
- Both axes use a linear scale.
3. **Overall Behavior and Trends:**
- The graph shows an exponential increase in collector current ($i_C$) as the base-emitter voltage ($v_{BE}$) increases. This is typical of the diode-like behavior of the BJT's base-emitter junction.
- The curve starts at a low current level and rises steeply as $v_{BE}$ approaches 700 mV.
4. **Key Features and Technical Details:**
- The point labeled $Q$ on the curve represents a quiescent operating point, indicating a specific $v_{BE}$ and corresponding $i_C$.
- The graph depicts the exponential nature of the BJT's operation, where small increases in $v_{BE}$ result in significant increases in $i_C$.
- The 18 mV and 60 mV rules apply here, indicating that small changes in $v_{BE}$ can lead to octave and decade changes in $i_C$, respectively.
5. **Annotations and Specific Data Points:**
- The graph includes a horizontal line marking a specific collector current level ($I_C$) and a vertical line marking a specific base-emitter voltage ($V_{BE}$).
- The slope at the point $Q$ is labeled as $g_m$, which represents the transconductance at that operating point.
- The curve is annotated with gridlines to help identify specific values of $v_{BE}$ and $i_C$.
- The exponential curve suggests that the BJT is in the active region, where it functions effectively as an amplifier.
FIGURE 2.13 Using PSpice to display the exponential $i-v$ curve of the 2N2222 BJT.
rather than to the base terminal. Consequently, all properties exhibited by the $p n$ junction's $i-v$ characteristic hold also for the BJT's $i_{C}-v_{B E}$ characteristic. In particular, the following rules of thumb hold also for BJTs:
- To effect an octave change in $i_{C}$ we need to change $v_{B E}$ by 18 mV (18-mV Rule)
- To effect a decade change in $i_{C}$ we need to change $v_{B E}$ by 60 mV ( $\mathbf{6 0} \mathbf{- m V}$ Rule)
- The voltage drop $V_{B E}$ exhibits a temperature coefficient of about $-2 \mathrm{mV} /{ }^{\circ} \mathrm{C}$ (-2-mV Rule)
The slope of the $i_{C}-V_{B E}$ curve at a particular operating point $Q=Q\left(I_{C}, V_{B E}\right)$ is denoted as $g_{m}$ and is called the transconductance (in A/V),
$$
\begin{equation*}
g_{m}=\left.\frac{\partial i_{C}}{\partial v_{B E}}\right|_{Q} \tag{2.19}
\end{equation*}
$$
Differentiating Eq. (2.10), we readily find
$$
\begin{equation*}
g_{m}=\frac{I_{C}}{V_{T}} \tag{2.20}
\end{equation*}
$$
which allows us to calculate the BJT's transconductance at any bias current $I_{C}$. To get a feel, at $I_{C}=1 \mathrm{~mA}$ we get $g_{m}=38 \mathrm{~mA} / \mathrm{V}$, which is often expressed in the alternative form $g_{m}=1 /(26 \Omega)$.
(The reader who has already been exposed to MOSFETs may have noted a similarity with the MOSFET's transconductance expressed in the form $g_{m}=I_{D} /\left(0.5 V_{O V}\right)$, where $V_{O V}$ is the overdrive voltage needed to sustain a given drain current $I_{D}$. Typically $0.5 V_{O V} \gg V_{T}$, so for the same bias current a FET will generally exhibit much lower transconductance than a BJT. This is a notorious drawback of FETs compared to BJTs, especially in the design of high-gain amplifiers.)
### The $\boldsymbol{i}_{\boldsymbol{c}}-\boldsymbol{V}_{\boldsymbol{C E}}$ Characteristics for Different $\boldsymbol{V}_{B E}$ Drives
Figure 2.14a shows a PSpice circuit to display the 2N2222's $i_{C}-v_{C E}$ curves for different voltage drives $V_{B E}$. In the example shown, $V_{B E}$ is stepped from 650 mV to 710 mV in $10-\mathrm{mV}$ increments. From Fig. $2.14 b$, we note that for sufficiently positive values of $v_{C E}$, the $i-v$ curves are fairly flat and thus indicative of voltage-controlled currentsource behavior by the BJT. This is the forward active (FA) region of operation. In this region, curve spacing increases exponentially with the $V_{B E}$ steps, in accordance with Eq. (2.10). (The reader who has already been exposed to MOSFETs will recall that curve spacing for FETs increases only quadratically with each $V_{G S}$ step.)
For low values of $v_{C E}$ the curves bend downwards, indicating a progressive decrease in $i_{C}$. This is due to the fact that once the value of $v_{C E}$ drops below that of $V_{B E}$, the B-C junction becomes forward biased, raising the current component $i_{B C}$ from the base region to the collector region. By KCL, the current into the collector terminal is now $i_{C}=I_{s} \exp \left(V_{B E} / V_{T}\right)-i_{B C}$. As the B-C junction becomes more and more forward biased, $i_{C}$ decreases till its drops to zero when the two terms cancel each other out. This occurs for $v_{C E}$ near to 0 V , though not necessarily exactly 0 V , as the saturation currents of the two junctions are generally not identical in value. When both its junctions are forward biased, the BJT is said to be operating in the saturation (Sat) mode. The reason for this name will become apparent as we proceed.
### The Early Effect
If we display the $i_{C}-v_{C E}$ curves on a more compressed horizontal scale as in Fig. 2.15, we note that the slope of the curves in the active region increases progressively with $v_{B E}$. Moreover, the extrapolations of all curves meet at a common point ${ }^{4}$ located at $v_{C E}=-V_{A}$. Called the Early voltage for James M. Early, who first investigated this phenomenon, $V_{A}$ is typically in the range of 10 V to 100 V . The value used in the PSpice model of the 2N2222 BJT is $V_{A}>75 \mathrm{~V}$.
image_name:(a)
description:
[
name: Q2N2222, type: NPN, ports: {C: V_CE, B: V_BE, E: GND}
name: V_BE, type: VoltageSource, value: V_BE, ports: {Np: V_BE, Nn: GND}
name: V_CE, type: VoltageSource, value: V_CE, ports: {Np: V_CE, Nn: GND}
]
extrainfo:The diagram illustrates the i_C-V_CE curves of the 2N2222 NPN transistor for various V_BE values, showcasing the Early effect. The curves demonstrate the relationship between collector current (i_C) and collector-emitter voltage (v_CE) for different base-emitter voltages (V_BE) ranging from 650 mV to 710 mV.
image_name:(b)
description:The graph in figure (b) is an $i_C - v_{CE}$ curve for a 2N2222 BJT, displaying the collector current ($i_C$) versus the collector-emitter voltage ($v_{CE}$) for various base-emitter voltages ($V_{BE}$). The x-axis represents $v_{CE}$ in volts, ranging from 0 to 1 V, while the y-axis represents $i_C$ in milliamperes, ranging from 0 to 12 mA.
1. **Type of Graph and Function**: This is a family of characteristic curves for a bipolar junction transistor (BJT), specifically showing the relationship between the collector current and collector-emitter voltage for different base-emitter voltages.
2. **Axes Labels and Units**: The x-axis is labeled $v_{CE}$ (V) and the y-axis is labeled $i_C$ (mA). The graph uses a linear scale for both axes, with gridlines to aid in reading values.
3. **Overall Behavior and Trends**: Each curve represents a different $V_{BE}$ value, ranging from 650 mV to 710 mV. As $v_{CE}$ increases, the collector current $i_C$ initially rises sharply and then levels off, indicating the transistor is in the active region. The curves show that for higher $V_{BE}$ values, the collector current is higher, reflecting increased transistor activity.
4. **Key Features and Technical Details**: The curves exhibit a slight upward slope as $v_{CE}$ increases, demonstrating the Early effect, where the effective base width decreases with increasing $v_{CE}$. This results in a slight increase in $i_C$ even in the active region. The curves do not reach saturation within the given $v_{CE}$ range.
5. **Annotations and Specific Data Points**: Each curve is annotated with its corresponding $V_{BE}$ value, clearly indicating the effect of base-emitter voltage on collector current. The curves converge toward a common point at higher $v_{CE}$ values, illustrating the Early voltage concept, although this is not explicitly shown due to the limited $v_{CE}$ range in the graph.
FIGURE 2.14 Using PSpice to display the 2N2222's $i_{C}-V_{C E}$ curves for different $V_{B E}$ values and $0 \leq v_{C E} \leq 1 \mathrm{~V}$.
image_name:Figure 2.15
description:Figure 2.15 is a plot illustrating the Early effect and the Early voltage ($V_A$) in a bipolar junction transistor (BJT). The graph is an $i_C$ vs. $v_{CE}$ plot, where the x-axis represents the collector-emitter voltage ($v_{CE}$) in volts, and the y-axis represents the collector current ($i_C$) in milliamperes (mA). The x-axis spans from 0 to 20 volts, and the y-axis ranges from 0 to 15 mA.
The graph consists of multiple linear curves, each representing a different base-emitter voltage ($V_{BE}$). These curves are positively sloped, indicating that as $v_{CE}$ increases, $i_C$ also increases. The curves begin at different points on the y-axis, reflecting the impact of different $V_{BE}$ values on the collector current.
A notable feature of the graph is that all the curves appear to converge at a single point on the negative x-axis, labeled as $-V_A$. This convergence point represents the Early voltage, a conceptual value indicating the extrapolated intersection of the curves. The Early effect is demonstrated here by the non-zero slope of the curves, which signifies the modulation of the effective base width with changes in $v_{CE}$.
The overall behavior of the graph shows a linear increase in $i_C$ with increasing $v_{CE}$, and the convergence of the curves suggests the Early effect, where the collector current is influenced by the base-width modulation as $v_{CE}$ increases. The graph effectively visualizes the relationship between the collector current and collector-emitter voltage under the influence of varying base-emitter voltages, highlighting the Early effect's impact on BJT operation.
FIGURE 2.15 Illustrating the Early effect and the Early voltage $V_{A}$.
The slant of the $i_{C}-v_{C E}$ curves is due to the fact that the effective base width $W_{B}$ shrinks with increasing $v_{C E}$, a phenomenon aptly referred to as base-width modulation or also as the Early effect. To appreciate it, suppose the BJT is initially biased at some voltage $v_{C E}=V_{C E 1}$ in the active region (see Fig. 2.16a). Let the corresponding base width be $W_{B 1}$, the electron current density be $J_{n 1}$ (see Fig. 2.16b), and the collector current be $I_{C 1}\left(=J_{n 1} A_{E}\right)$. If we now increase $v_{C E}$ to the new value $V_{C E 2}$, the amount of reverse bias across the B-C junction will also increase, indicating a corresponding increase in the electric field $E_{C B}$ inside its space-charge layer (SCL). Referring back to Fig. 2.5, we can state that the increase in the number of field lines can only come at the price of a widening of the SCL, so as to uncover more ions. Consequently, the base width will shrink to a new value $W_{B 2}\left(<W_{B 1}\right)$, as depicted in Fig. 2.16b. But, with a narrower base width, the slope of $n_{B}^{\prime}(x)$ increases, ultimately raising the current density to the new value $J_{n 2}\left(>J_{n 1}\right)$, and, hence, the collector current to $I_{C 2}\left(>I_{C 1}\right)$. The chain of cause-effect relationships is summarized as follows:
$$
\begin{aligned}
\left(\text { increasing } v_{C E}\right) & \Rightarrow(\text { widens the B-C SCL }) \Rightarrow\left(\text { shrinks } W_{B}\right) \\
& \Rightarrow\left(\text { increases the slope of } n_{B}^{\prime}\right) \Rightarrow\left(\text { increases } J_{n}\right)
\end{aligned}
$$
image_name:(a)
description:The graph labeled "(a)" is a plot illustrating the relationship between the collector current \(i_C\) and the collector-emitter voltage \(v_{CE}\) in a bipolar junction transistor (BJT), demonstrating the Early effect.
1. **Type of Graph and Function:**
- This is a linear plot showing the dependency of the collector current \(i_C\) on the collector-emitter voltage \(v_{CE}\) at a constant base-emitter voltage \(v_{BE}\).
2. **Axes Labels and Units:**
- The vertical axis represents the collector current \(i_C\), typically measured in amperes (A).
- The horizontal axis represents the collector-emitter voltage \(v_{CE}\), typically measured in volts (V).
3. **Overall Behavior and Trends:**
- The graph shows a set of parallel lines with a positive slope, indicating that as \(v_{CE}\) increases, \(i_C\) also increases, but at a decreasing rate due to the Early effect.
- The main line of interest is a bold line indicating a specific \(v_{BE}\) value where the collector current \(i_C\) is observed.
- The plot demonstrates a slight increase in \(i_C\) as \(v_{CE}\) increases, which is characteristic of the Early effect, showing how \(i_C\) is weakly dependent on \(v_{CE}\).
4. **Key Features and Technical Details:**
- Two points, \(Q_1\) and \(Q_2\), are marked on the bold line, corresponding to two different \(v_{CE}\) values, \(V_{CE1}\) and \(V_{CE2}\), with corresponding collector currents \(I_{C1}\) and \(I_{C2}\).
- The increase in \(i_C\) from \(I_{C1}\) to \(I_{C2}\) as \(v_{CE}\) goes from \(V_{CE1}\) to \(V_{CE2}\) illustrates the Early effect.
- The graph also shows several other lines with different \(v_{BE}\) values, demonstrating how \(i_C\) varies with \(v_{BE}\) and \(v_{CE}\).
5. **Annotations and Specific Data Points:**
- The graph is annotated with \(V_{BE}\) to indicate the constant base-emitter voltage at which the observations are made.
- The points \(Q_1\) and \(Q_2\) are specifically marked to show the change in \(i_C\) with changing \(v_{CE}\), highlighting the Early effect in BJTs.
image_name:(b)
description:The graph labeled "(b)" illustrates the concept of base-width modulation in a Bipolar Junction Transistor (BJT) by showing the change in the electron concentration gradient across the base region.
1. **Type of Graph and Function:**
- This is a schematic representation of electron concentration as a function of position within the base of a BJT.
2. **Axes Labels and Units:**
- The horizontal axis is labeled as \(x\), representing the position across the base.
- The vertical axis is labeled as \(n'_B(x)\), indicating the electron concentration gradient, with units of \(\text{cm}^{-3}\).
- The scale appears linear, with no specific units or markers indicated.
3. **Overall Behavior and Trends:**
- The graph shows a triangular region where the electron concentration decreases linearly from a maximum at \(x = 0\) to zero at the base width. This indicates a linear gradient of electron concentration.
- The slope of the line decreases as the base width narrows, illustrating the Early effect, where a narrower base increases the current density.
4. **Key Features and Technical Details:**
- Two key lines are shown: one representing the initial condition with a base width \(W_{B1}\) and another showing a reduced base width \(W_{B2}\).
- The initial gradient \(J_{n1}\) is steeper than the gradient \(J_{n2}\) after the base width is reduced, indicating an increase in current density as \(W_B\) decreases.
- The shaded area represents the increase in current density \(J_n\) as the base width narrows.
5. **Annotations and Specific Data Points:**
- The graph highlights the initial electron concentration \(n_{B0}\) and its exponential dependence on \(v_{BE}\) as \(n_{B0}(e^{v_{BE}/V_T} - 1)\).
- The critical points \(W_{B1}\) and \(W_{B2}\) are marked to show the change in base width, with \(W_{B2} < W_{B1}\).
- The difference between \(J_{n1}\) and \(J_{n2}\) is highlighted to emphasize the increase in current density due to base-width modulation.
FIGURE 2.16 Illustrating the effects of base-width modulation.
It is apparent that even though $i_{C}$ is primarily controlled by $v_{B E}$, it also depends, if weakly, on $v_{C E}$. To reflect this dependence, Eq. (2.10) is modified as
$$
\begin{equation*}
i_{C}=I_{s}{ }^{v_{B E} / V_{z}}\left(1+\frac{v_{C E}}{V_{A}}\right) \tag{2.21}
\end{equation*}
$$
We observe that the narrower the base with which the BJT has been fabricated initially, the more pronounced the Early effect, and thus the lower the value of $V_{A}$. We are now able to perform a spot check on the PSpice simulation of Fig. 2.13, a task an engineer should always perform as a matter of good working habit. Thus, picking for instance $V_{B E}=700 \mathrm{mV}$, we use Eq. (2.21) with $V_{C E}=1.0 \mathrm{~V}$ to find
$$
I_{C}=14.34 \times 10^{-15} e^{700 / 25.9}\left(1+\frac{1}{75}\right) \cong 7.9 \mathrm{~mA}
$$
which agrees with the plotted value of Fig. 2.13b.
### The $\boldsymbol{i}_{C}-\mathbf{V}_{C E}$ Characteristics for Different $I_{B}$ Drives
Given that the BJT lends itself to both voltage and current control, an alternative way of characterizing it is by displaying its $i_{C}-v_{C E}$ curves for different current drives $I_{B}$. In the example of Fig. 2.17, $I_{B}$ is stepped from 0 to $60 \mu \mathrm{~A}$ in $10-\mu \mathrm{A}$ increments. For $I_{B}=0$ we have $I_{C}=0$, and the BJT is said to be cut off $(\mathrm{CO})$. We note that curve spacing in the forward active region is now much more uniform. Also, as in the voltagedriven case, the curves are a bit slanted because of the Early effect. An advantage of this type of characteristics is that they allow us to find $\beta_{F}$ at a given active-region operating point $Q_{F}$ by mere inspection. For instance, consider the point $Q_{F}$ lying right on the $I_{B}=60 \mu \mathrm{~A}$ curve at $V_{C E}=0.8 \mathrm{~V}$. A visual readout of the collector current
image_name:(a)
description:
[
name: Q2N2222, type: NPN, ports: {C: VCE, B: Vb, E: GND}
name: V_CE, type: VoltageSource, value: V_CE, ports: {Np: VCE, Nn: GND}
name: I_B, type: CurrentSource, value: I_B, ports: {Np: Vb, Nn: GND}
]
extrainfo:The circuit diagram shows a common-emitter configuration of an NPN transistor (2N2222) with a variable base current (I_B) and a collector-emitter voltage (V_CE). The graph on the right displays the output characteristics, showing the collector current (i_C) versus collector-emitter voltage (v_CE) for different base current values, illustrating the Early effect and the transistor's current gain (β_F) at a specific point.
image_name:(b)
description:The graph depicted is a set of characteristic curves for a 2N2222 transistor, illustrating the relationship between the collector current \(i_C\) and the collector-emitter voltage \(v_{CE}\) for various base currents \(I_B\). This type of graph is commonly referred to as an \(i_C-v_{CE}\) plot.
**Axes Labels and Units:**
- The horizontal axis represents the collector-emitter voltage \(v_{CE}\), measured in volts (V), ranging from 0 to 1 V.
- The vertical axis represents the collector current \(i_C\), measured in milliamperes (mA), ranging from 0 to 12 mA.
**Overall Behavior and Trends:**
- The graph shows several curves, each corresponding to a different base current \(I_B\) value, ranging from 0 to 60 µA in increments of 10 µA.
- Each curve starts at the origin and initially rises steeply, indicating that \(i_C\) increases rapidly with \(v_{CE}\) at low voltages.
- As \(v_{CE}\) increases, the curves tend to flatten out, showing that \(i_C\) becomes relatively constant, indicating the transistor is in the forward active region.
- The spacing between the curves is more uniform in the forward active region, reflecting the linear relationship between \(i_C\) and \(I_B\).
**Key Features and Technical Details:**
- The curves are slightly slanted due to the Early effect, which causes a slight increase in \(i_C\) with increasing \(v_{CE}\) even in the active region.
- At low \(v_{CE}\) values, the curves bend downward, indicating the onset of saturation.
**Annotations and Specific Data Points:**
- Specific base current values \(I_B\) are annotated beside each curve, allowing for easy identification of the operating conditions.
- A notable data point is at \(v_{CE} = 0.8\) V on the \(I_B = 60\) µA curve, where the collector current \(i_C\) is approximately 10.5 mA, leading to a current gain \(\beta_F = 174\).
FIGURE 2.17 Using PSpice to display the 2N2222's $i_{C}-v_{C E}$ curves for different $I_{B}$ values and $0 \leq v_{C E} \leq 1 \mathrm{~V}$.
gives approximately $I_{C}=10.5 \mathrm{~mA}$. Consequently, the current gain at the given operating point $Q_{F}\left(I_{C}, V_{C E}\right)=Q_{F}(10.5 \mathrm{~mA}, 0.8 \mathrm{~V})$ is simply $\beta_{F}=10.5 / 0.060=174$.
As in the voltage-driven case, the curves bend downward at low values of $v_{C E}$. This bending is again due to the fact that once $v_{C E}$ drops below $V_{B E}$, the B-C junction becomes forward biased, thus drawing the current $i_{B C}$ from the base to the collector. This new current component subtracts from the existing currents both at the base and collector, so the net current into the collector terminal is now $i_{C}=\beta_{F}\left(I_{B}-i_{B C}\right)-$ $i_{B C}=\beta_{F} I_{B}-\left(\beta_{F}+1\right) i_{B C}$. As the B-C junction becomes more and more forward biased, $i_{C}$ decreases till it drops to zero when the two terms cancel each other out. Since the effect of $i_{B C}$ is now magnified by $\beta_{F}+1$, it takes a smaller amount of forward bias to bring about the onset of saturation. Compared to Fig. 2.14b, the curves now start to bend "earlier", that is, slightly more to the right.
### The Reverse Active (RA) Mode
If we allow $v_{C E}$ to take on negative values in the circuit of Fig. 2.17a, then the roles of the emitter and collector will be interchanged (B-C junction forward biased, B-E junction reverse biased.) When operating in this mode, referred to as the reverseactive (RA) mode, the BJT exhibits a notoriously low current gain, now defined as
$$
\beta_{R}=\frac{-I_{E}}{I_{B}}
$$
This is depicted in the lower-left area of Fig. 2.18a for the popular 2N2222 BJT. The lower gain stems from the fact that electrons are now injected into the base from the lightly doped collector region, and holes are injected into the collector region from the more heavily doped base region. Clearly, the conditions that were critical to ensure a high current gain in the FA region turn out to be detrimental for RA operation. Actual transistors exhibit $\beta_{R}$ values ranging from as high as 10 to as low as 0.1 or lower (see the end-of-chapter problems for examples of how to measure $\beta_{R}$ ).
image_name:(a)
description:The graph labeled (a) illustrates the four regions of operation for a 2N2222 npn BJT transistor, plotting the collector current (i_C) in milliamperes (mA) against the collector-emitter voltage (v_CE) in volts (V). The graph is divided into four distinct regions: Reverse Active, Cutoff, Forward Active, and Saturation, each corresponding to different operational modes of the BJT.
1. **Axes Labels and Units:**
- The x-axis represents the collector-emitter voltage (v_CE) ranging from -1.0 V to 1.0 V.
- The y-axis represents the collector current (i_C) ranging from 0 mA to 4.0 mA.
2. **Overall Behavior and Trends:**
- In the Reverse Active region (v_CE < 0), the collector current remains constant and very low, indicating minimal current flow.
- As v_CE approaches 0 V, the BJT transitions into the Cutoff region where the collector current is near zero, indicating the transistor is off.
- The Forward Active region begins around v_CE = 0.5 V, where the collector current increases sharply with increasing v_CE, indicating the transistor is on and amplifying.
- The Saturation region occurs at higher collector currents and lower v_CE, where the increase in i_C begins to level off, indicating the transistor is fully on.
3. **Key Features and Technical Details:**
- The transition from Cutoff to Forward Active is marked by a sharp increase in i_C, demonstrating the transistor's ability to amplify current.
- The graph shows multiple curves representing different base currents (I_B), each increasing in the upward direction in the Forward Active region, illustrating how i_C varies with I_B.
4. **Annotations and Specific Data Points:**
- The graph is annotated with labels for each region, providing clarity on the operational state of the BJT.
- The transition points between regions are visually marked, though not numerically specified.
image_name:(b)
description:The image consists of two parts: a graph (a) and a table (b).
**Graph (a):**
- The graph plots the collector current (i_C) in milliamps (mA) on the y-axis against the collector-emitter voltage (v_CE) in volts (V) on the x-axis.
- The x-axis ranges from -1.0 V to 1.0 V, while the y-axis ranges from 0 mA to 4.0 mA.
- The graph is divided into three regions, labeled as "Reverse active," "Cutoff," "Forward active," and "Saturation."
- The "Reverse active" region is on the left, where v_CE is negative.
- The "Cutoff" region is around v_CE = 0.5 V, where the collector current is minimal.
- The "Forward active" region is to the right, where v_CE is positive, and i_C increases with increasing base current (I_B).
- The "Saturation" region is marked as overlapping the "Forward active" region when i_C is at its maximum.
- Arrows labeled "Incr I_B" indicate increasing base current in both the reverse and forward active regions.
**Table (b):**
- The table lists the four modes of BJT operation.
- It has three columns labeled "B-E," "B-C," and "Mode."
- "B-E" and "B-C" represent the biasing of the base-emitter and base-collector junctions, respectively, with "R" indicating reverse bias and "F" indicating forward bias.
- The "Mode" column lists the corresponding operational mode of the BJT:
- CO (Cutoff): Both B-E and B-C are reverse biased.
- FA (Forward Active): B-E is forward biased, B-C is reverse biased.
- RA (Reverse Active): B-E is reverse biased, B-C is forward biased.
- Sat (Saturation): Both B-E and B-C are forward biased.
FIGURE 2.18 (a) The four regions of operation of the popular 2N2222 npn BJT. (b) The four modes of BJT operation (F stands for forward biased, and R for reverse biased.)
Except for a few specialized cases, operation of the BJT in the RA region hardly offers any practical advantages. We will take up this mode again in Chapter 6, when studying the storage time of the BJT in switching applications. For convenience, the four operating modes of a BJT are tabulated in Fig. 2.18b. This table applies both to npn and pnp BJTs.
### Transistor Breakdown Voltages
With sufficient reverse bias, each junction of a BJT can be driven in the breakdown region. Since the emitter side is heavily doped, the B-E junction (with the collector terminal) open breaks down by the Zener mechanism, typically at a breakdown voltage $B V_{E B O} \cong 6 \mathrm{~V}$. This mode, while not necessarily destructive so long as we limit power dissipation, is to be avoided as it tends to degrade in the value of $\beta_{F}$ significantly. ${ }^{1}$
On the other hand, to permit operation over an adequately wide range of $v_{C E}$ values, the collector side is doped much more lightly, so in this case breakdown occurs by the avalanche mechanism. The breakdown process of the $i_{C}{ }^{-v_{C E}}$ characteristics, pictured in Fig. 2.19, is far more complex ${ }^{4}$ than that of a basic pn junction because of the current amplification provided by the BJT itself. Any current entering the base, whether generated thermally in the B-C SCL or triggered by the onset of the avalanche process, gets magnified by $\beta_{F}$. Moreover, $\beta_{F}$ starts out low but grows with the current itself, as per Fig. 2.12. Suffice it to say here that because of current amplification, the value of $B V_{C E O}$ is appreciably lower than the breakdown voltage of the $\mathrm{B}-\mathrm{C}$ junction alone, that is, with the emitter open. It is apparent that BJT operation must be restricted over a range of $v_{C E}$ values lower than $B V_{C E O}$ by an adequately safe margin. If a given BJT fails to meet the requirements of the application at hand, a different type with a higher $B V_{C E O}$ rating must be selected. BJTs are available with a wide range of $B V_{C E O}$ ratings, from a half a dozen volts for BJTs intended for digital applications to many hundreds of volts for BJTs intended for power-handling applications.
FIGURE 2.19 The collectoremitter breakdown characteristics.
image_name:FIGURE 2.19
description:The graph in FIGURE 2.19 is a plot of the collector-emitter current-voltage characteristics of a Bipolar Junction Transistor (BJT). The graph is specifically a set of collector current \(i_C\) versus collector-emitter voltage \(v_{CE}\) curves, illustrating the breakdown characteristics of the BJT.
**1. Type of Graph and Function:**
This is a family of characteristic curves typically used to describe the behavior of BJTs under different base current \(i_B\) conditions.
**2. Axes Labels and Units:**
- The horizontal axis represents the collector-emitter voltage \(v_{CE}\) in volts.
- The vertical axis represents the collector current \(i_C\) in amperes.
- The graph is marked with a critical voltage point labeled \(BV_{CEO}\), indicating the breakdown voltage.
**3. Overall Behavior and Trends:**
- The curves show the relationship between \(i_C\) and \(v_{CE}\) for different base currents \(i_B\), which are not numerically specified but are implied to increase from the bottom curve upwards.
- Each curve starts at the origin, indicating no collector current at zero collector-emitter voltage.
- As \(v_{CE}\) increases, \(i_C\) initially rises steeply and then levels off, indicating the active region of the BJT.
- Beyond a certain point (at \(BV_{CEO}\)), the curves rise sharply, indicating the onset of breakdown.
**4. Key Features and Technical Details:**
- The curves are nearly horizontal in the active region, showing that \(i_C\) is relatively constant for a range of \(v_{CE}\).
- The breakdown region is marked by a sharp increase in \(i_C\) at \(BV_{CEO}\), indicating the voltage at which the transistor cannot sustain further increases in \(v_{CE}\) without significant increases in \(i_C\).
**5. Annotations and Specific Data Points:**
- The graph is annotated with \(i_B = 0\) at the bottom curve, suggesting that the base current is zero and increases for the higher curves.
- The breakdown voltage \(BV_{CEO}\) is a critical point on the \(v_{CE}\) axis, beyond which the BJT enters the breakdown region.
## 2.4 OPERATING REGIONS AND BJT MODELS
We now re-examine the various BJT operating modes in greater detail, and develop suitable BJT models to expedite hand calculations in dc analysis. By analogy with pn diodes, we shall stipulate that to make a BJT fully conductive it takes a B-E voltage drop of approximately 0.7 V . We express this by writing
$$
\begin{equation*}
V_{B E(\mathrm{n})}=0.7 \mathrm{~V} \tag{2.22a}
\end{equation*}
$$
for an $n p n$ BJT, and $V_{E B(\text { on })}=0.7 \mathrm{~V}$ for a pnp BJT. For bookkeeping purposes, we shall stipulate that to bring a BJT to the edge of conduction (EOC) it takes a B-E drop of approximately 0.6 V , or
$$
\begin{equation*}
V_{B E(\mathrm{EOC})}=0.6 \mathrm{~V} \tag{2.22b}
\end{equation*}
$$
for an $n p n \mathrm{BJT}$, and $V_{E B(\mathrm{EOC})}=0.6 \mathrm{~V}$ for a pnp BJT. As we move along we will find that when a BJT is meant to be in saturation, its base current is made on purpose considerably higher than in the forward active mode, to be on the safe side. Consequently, the B-E drop also tends to be slightly higher. We shall stipulate
$$
\begin{equation*}
V_{B E(\mathrm{sat})}=0.8 \mathrm{~V} \tag{2.22c}
\end{equation*}
$$
for an $n p n$ BJT, and $V_{E B(\text { sat })}=0.8 \mathrm{~V}$ for a pnp BJT. The above differences are minor, and many authors use the same value of 0.7 V throughout. But, as mentioned, we shall keep these distinctions primarily for bookkeeping purposes.
### The Cutoff (CO) Region
The cutoff $(\mathrm{CO})$ region is defined as
$$
i_{C}=0
$$
in the $i_{C^{-}} v_{C E}$ characteristics (see Fig. 2.20a). A BJT operates in cutoff (CO) when neither junction is sufficiently forward-biased to conduct significant current. We can thus ignore all currents and say that for practical purposes the B-E and C-B ports act as open circuits, as modeled in Fig. 2.20b. But, as we know, a junction's reverse current doubles for about every $10^{\circ} \mathrm{C}$ of temperature increase, so if high operating
image_name:Fig. 2.20a
description:The graph in Fig. 2.20a is a characteristic curve of a Bipolar Junction Transistor (BJT) in the cutoff region. It is a plot of collector current \(i_C\) against collector-emitter voltage \(v_{CE}\). The horizontal axis represents \(v_{CE}\) with units likely in volts, while the vertical axis represents \(i_C\) with units in amperes. The scales on both axes are linear.
The graph displays several curves that begin at the origin and quickly rise to a flat, nearly horizontal line, indicating that the collector current \(i_C\) remains approximately constant as \(v_{CE}\) increases beyond a certain point. This behavior is typical for a BJT in the active region, but the focus here is on the cutoff region where \(i_C\) is essentially zero.
The "Cutoff region" is marked on the graph, highlighting the area near the origin where the transistor is not conducting. In this region, neither the base-emitter nor the base-collector junctions are forward-biased, resulting in negligible collector current. Thus, the curves in this area are very close to the horizontal axis, indicating \(i_C = 0\).
This graph is crucial in understanding the BJT's behavior in different regions of operation, particularly in identifying the cutoff state where the transistor acts as an open circuit, allowing no current to flow through the collector-emitter path.
image_name:Fig. 2.20b
description:
[

]
extrainfo:The diagram shows the i_C vs. v_CE characteristics of a BJT, highlighting the cutoff region where the collector current i_C is zero. This is a graphical representation of the BJT's behavior in the cutoff region, indicating that both the base-emitter and collector-base junctions are not forward-biased enough to conduct significant current.
image_name:Fig. 2.21
description:
[

]
extrainfo:The image shows the cutoff region in the iC-vCE characteristics of a BJT. In this region, the collector current iC is approximately zero, indicating that the transistor is off and neither junction is forward-biased enough to conduct significant current. This is a graphical representation of the cutoff region for a BJT, not a circuit diagram, so no netlist can be generated.
(a)
image_name:FIGURE 2.20
description:
[
name: Q, type: NPN, ports: {C: C, B: B, E: E}
]
extrainfo:The diagram shows the cutoff region of a BJT where the transistor is off, and no significant current flows between the collector, base, and emitter.
(b)
FIGURE 2.20 The cutoff region, and the corresponding largesignal model for the npn BJT.
image_name:(a)
description:The graph in Figure 2.20(a) is a plot representing the cutoff region for a Bipolar Junction Transistor (BJT), specifically an NPN transistor. It is not a circuit diagram but rather a graphical representation of the transistor's behavior in the cutoff region.
Type of Graph and Function:
This is a characteristic curve graph of a BJT, illustrating the relationship between the collector current (i_C) and the collector-emitter voltage (v_CE) for various base currents (I_B).
Axes Labels and Units:
- The horizontal axis represents the collector-emitter voltage (v_CE) in volts.
- The vertical axis represents the collector current (i_C) in amperes.
- The graph uses a linear scale for both axes.
Overall Behavior and Trends:
- The graph shows a series of curves, each representing a different base current (I_B) level. These curves are concave and start from the origin, rising sharply initially and then leveling off as v_CE increases.
- As the base current (I_B) increases, the curves shift upwards, indicating higher collector currents for the same collector-emitter voltage.
Key Features and Technical Details:
- The cutoff region is indicated by the area where i_C is essentially zero, regardless of v_CE. This occurs when the base current (I_B) is also zero or very low.
- The graph highlights the edge of saturation, V_CE(EOS), marked at approximately 0.2 V. Beyond this point, the BJT transitions from saturation to the active region.
- The point Q_FA represents a specific operating point in the forward active region, where i_C is greater than zero and v_CE is greater than V_CE(EOS).
Annotations and Specific Data Points:
- The curves are annotated with increasing I_B, showing the relationship between base current and the resulting collector current.
- V_CE(EOS) is specifically marked on the graph, providing a reference for the transition point between saturation and active regions.
This graph effectively illustrates the cutoff region of a BJT, showing how the collector current behaves with varying collector-emitter voltages and base currents, emphasizing the conditions under which the transistor remains off (i.e., in the cutoff region).
image_name:(b)
description:
[
name: Q, type: NPN, ports: {C: C, B: B, E: E}
name: V_BE(on), type: VoltageSource, value: 0.7V, ports: {Np: B, Nn: E}
name: β_FI_B, type: CurrentControlledCurrentSource, ports: {Np: C, Nn: E}
]
extrainfo:The diagram represents the forward active region of an NPN BJT. In this region, the collector current (IC) is greater than zero, and the voltage across the collector-emitter junction (VCE) is greater than the edge of saturation voltage (VCE(EOS) ≈ 0.2 V). The base-emitter voltage is 0.7 V, and the collector current is controlled by the base current (IB) multiplied by the current gain (βF).
FIGURE 2.21 The forward active region, and the corresponding large-signal model of the npn BJT.
temperatures are anticipated, the designer must check whether the actual leakage currents affect circuit performance at the high end of the temperature range.
### The Forward Active (FA) Region
The forward active (FA) region, highlighted in Fig. 2.21a, is defined as
$$
i_{C}>0 \quad v_{C E}>V_{C E(\mathrm{EOS})}(\cong 0.2 \mathrm{~V})
$$
where the subscript EOS designates the edge of saturation. (For a pnp BJT, these conditions are $i_{C}>0$ and $v_{E C}>V_{E C(\mathrm{EOS})} \cong 0.2 \mathrm{~V}$.) In order for an $n p n$ BJT to operate in the FA region, its B-E junction must be forward biased at $v_{B E}=V_{B E(o n)} \cong 0.7 \mathrm{~V}$, and its B-C junction must be reverse biased, or at most it can be slightly forward biased, but not enough to conduct any significant forward current $i_{B C}$. Judging by the 2N2222's characteristics of Fig. 2.17b, which are fairly typical of low-power to me-dium-power BJTs, we see that this BJT tolerates a slight amount of B-C forward bias and still gives flat curves all the way down to $v_{C E} \cong 0.2 \mathrm{~V}$, where $v_{B C}=v_{B E}-v_{C E} \cong$ $0.7-0.2=0.5 \mathrm{~V}$.
The curves in the FA region are approximately horizontal, indicating currentsource behavior there. So, we model the C-E port with a current controlled current source (CCCS) as in Fig. 2.21b,
$$
\begin{equation*}
I_{C}=\beta_{F} I_{B} \tag{2.23}
\end{equation*}
$$
Some authors include also a suitably large resistance $r_{o}$ in parallel with the CCCS to model the slant of the curves, but in the course of dc calculations this resistance is usually ignored for simplicity, so we omit it altogether. As shown in the figure, the B-E port is modeled as an ordinary $p n$ diode, that is, with a voltage source $V_{B E(\text { on })} \cong 0.7 \mathrm{~V}$. As mentioned, the value of $\beta_{F}$ at any operating point $Q_{\mathrm{FA}}$ within the active region is found as
$$
\begin{equation*}
\beta_{F}=\left.\frac{I_{C}}{I_{B}}\right|_{Q_{\mathrm{FA}}} \tag{2.24}
\end{equation*}
$$
By KCL, we have $I_{E}=I_{B}+I_{C}=I_{B}+\beta_{F} I_{B}$ or
$$
\begin{equation*}
I_{E}=\left(\beta_{F}+1\right) I_{B} \tag{2.25}
\end{equation*}
$$
We also have $I_{C}=\beta_{F} I_{B}=\beta_{F} I_{E} /\left(\beta_{F}+1\right)$, or
$$
\begin{equation*}
I_{C}=\alpha_{F} I_{E} \tag{2.26}
\end{equation*}
$$
where $\alpha_{F}$, referred to as the common-base forward current gain, is
$$
\begin{equation*}
\alpha_{F}=\frac{\beta_{F}}{\beta_{F}+1} \tag{2.27}
\end{equation*}
$$
By contrast, $\beta_{F}$ is called the common-emitter forward current gain. If $\alpha_{F}$ is known, then $\beta_{F}$ is found as
$$
\begin{equation*}
\beta_{F}=\frac{\alpha_{F}}{1-\alpha_{F}} \tag{2.28}
\end{equation*}
$$
As mentioned, a BJT may typically have $\beta_{F}=100$, and thus $\alpha_{F}=100 / 101=0.99$. Likewise, if $\beta_{F}=250$, then $\alpha_{F}=0.996$. We observe that $\alpha_{F}$ is less than unity, though quite close to it. A small variation in $\alpha_{F}$ generally results in a much greater variation in $\beta_{F}$, so care must be exercised in applying Eq. (2.28). Because of $\alpha_{F}$ 's closeness to unity, Eq. (2.26) is often approximated as $I_{C} \cong I_{E}$, but only in the FA region!
### The Saturation (Sat) Region
The saturation region, highlighted in Fig. 2.22a, is defined as
$$
i_{C}>0 \quad 0<v_{C E}<V_{C E(\mathrm{EOS})} \cong 0.2 \mathrm{~V}
$$
(For a pnp BJT, these conditions are $i_{C}>0$ and $v_{E C}<V_{E C(\mathrm{EOS})} \cong 0.2 \mathrm{~V}$.) As we know, in saturation the B-C junction becomes forward biased, drawing current away from the base region and thus allowing only a fraction of $I_{B}$ to undergo amplification by $\beta_{F}$. Consequently, for a given base drive $I_{B}$, the collector current at any operating point $Q_{\text {sat }}$ in the saturation region will always be less than the collector current at an operating point $Q_{\mathrm{FA}}$ in the forward active region. In other words, we always have $I_{C(\text { sat })}<\beta_{F} I_{B}$. The ratio $I_{C(\text { sat })} / I_{B}$, aptly denoted as $\beta_{\text {sat }}$, is such that
$$
\begin{equation*}
\beta_{s a t}=\left.\frac{I_{C(\mathrm{sat})}}{I_{B}}\right|_{Q_{\mathrm{sat}}}<\beta_{F} \tag{2.29}
\end{equation*}
$$
This inequality provides an alternative test of determining whether a BJT is operating in saturation.
image_name:(a)
description:The graph labeled (a) is a plot depicting the collector current \( i_C \) as a function of the collector-emitter voltage \( V_{CE} \) for a bipolar junction transistor (BJT) in the saturation region. This is a characteristic curve used to analyze the behavior of the BJT in this region.
1. **Type of Graph and Function**:
- This is a characteristic curve graph, specifically for an npn BJT in the saturation region.
2. **Axes Labels and Units**:
- The horizontal axis represents the collector-emitter voltage \( V_{CE} \), measured in volts (V).
- The vertical axis represents the collector current \( i_C \), measured in amperes (A).
- The graph uses a linear scale for both axes.
3. **Overall Behavior and Trends**:
- The curves are steep, indicating a voltage-source behavior typical of the saturation region.
- The curves are bundled together, showing minimal change in \( i_C \) with increasing \( V_{CE} \) up to a certain point.
- As \( V_{CE} \) increases from 0 V to about 0.2 V, \( i_C \) remains relatively constant, indicating the saturation behavior.
4. **Key Features and Technical Details**:
- The saturation current \( I_{C(sat)} \) is marked on the graph, indicating the level of collector current in saturation.
- The operating point \( Q_{sat} \) is shown, marking the transition into the saturation region.
- The graph indicates that \( V_{CE(sat)} \approx 0.1 \) V, which is typical for a BJT in saturation.
- The end of saturation (EOS) point is marked at \( V_{CE(EOS)} = 0.2 \) V.
- The curves are labeled with increasing base current \( I_B \), indicating how the saturation current changes with different base currents.
5. **Annotations and Specific Data Points**:
- There is a shaded region indicating the saturation area on the graph.
- The graph is annotated with key points such as \( I_{C(sat)} \) and \( Q_{sat} \), which are critical for understanding the BJT's operation in saturation.
- The graph is part of a larger figure that includes a schematic representation of the BJT's large-signal model in saturation, shown in figure (b), with specific voltage values annotated.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: C, B: B, E: E}
name: VBE, type: VoltageSource, value: 0.8V, ports: {Np: B, Nn: E}
name: VCE, type: VoltageSource, value: 0.1V, ports: {Np: C, Nn: E}
]
extrainfo:The circuit diagram (b) represents a large-signal model of an NPN BJT in the saturation region. It includes a voltage source VBE with a value of 0.8V between the base and emitter, and another voltage source VCE with a value of 0.1V between the collector and emitter. The diagram highlights the saturation conditions with currents IB and IC(sat) flowing through the base and collector, respectively.
FIGURE 2.22 The saturation region, and the corresponding large-signal model of the npn BJT.
The curves in the saturation region are relatively steep, indicating voltage-source behavior there. Moreover, they are bundled together somewhere in the middle of the saturation region. Consequently, as depicted in Fig. 2.22b, we model the C-E port with a voltage source
$$
\begin{equation*}
V_{C E(\mathrm{sat})} \cong 0.1 \mathrm{~V} \tag{2.30}
\end{equation*}
$$
Some authors include also a suitably small resistance $R_{C E(\text { sat })}$ in series with this source to model the slant of the curves, but in the course of dc calculations this resistance is usually ignored for simplicity, so we omit it altogether. As shown in the figure, the B-E port is modeled like an ordinary pn diode, but with a slightly higher voltage drop $V_{B E(\text { sat })} \cong 0.8 \mathrm{~V}$ to account for the fact that in actual applications a BJT is driven in saturation with higher than usual base currents. It is important to realize that because of the inequality of Eq. (2.29), Eqs. (2.23) through (2.28) no longer hold once the BJT enters saturation. The region of their validity is only the FA region! However, we still have, by KCL, $I_{E}=I_{B}+I_{C}$.
EXAMPLE 2.4 Suppose a BJT is biased in the active region with $V_{B E}=700 \mathrm{mV}$ and $V_{C E}=1 \mathrm{~V}$, and it is found to have $\beta_{F}=100$. If $V_{C E}$ is gradually decreased until a $10 \%$ drop in $\beta_{F}$ is observed, what is the value of $V_{C E}$ ? For simplicity assume the B-E and B-C junctions have identical values of $I_{s}$.
Note: when this drop occurs, the BJT is said to be in soft saturation, a condition also referred to as the edge of saturation (EOS).
#### Solution
In soft saturation the B-C junction becomes weakly forward biased and carries a current $I_{B C} \neq 0$. To cause a $10 \%$ drop in $\beta_{F}\left(=I_{C} / I_{B}\right), I_{B}$ must increase by about $10 \%$, and this increase is precisely $I_{B C}$. Imposing $I_{B C} \cong 0.1 I_{B}=0.1\left(I_{C} / 100\right)=$ $I_{C} / 10^{3}$ indicates that $I_{B C}$ is 3 decades lower than $I_{C}$. By the $60-\mathrm{mV}$ Rule, $V_{B C}=$ $V_{B E}-3 \times 60 \mathrm{mV}=700-180=520 \mathrm{mV}$. By KVL, $V_{C E}=V_{B E}-V_{C E}=0.18 \mathrm{~V}$ ( $\cong 0.2 \mathrm{~V}$ typically assumed).
image_name:(a)
description:
[
name: Q1, type: PNP, ports: {C: C, B: B, E: E}
name: VEB(on), type: VoltageSource, value: 0.7V, ports: {Np: E, Nn: B}
name: βFIB, type: CurrentControlledCurrentSource, ports: {Np: C, Nn: E}
name: VEB(sat), type: VoltageSource, value: 0.8V, ports: {Np: E, Nn: B}
name: VEC(sat), type: VoltageSource, value: 0.1V, ports: {Np: E, Nn: C}
]
extrainfo:The diagram shows large-signal models of a PNP BJT in forward active and saturation regions. In the forward active mode, the base-emitter voltage is 0.7V, and the collector current is controlled by βF times the base current. In saturation, the base-emitter voltage is 0.8V, and the collector-emitter voltage is 0.1V.
image_name:(b)
description:
[
name: Q2, type: PNP, ports: {C: C, B: B, E: E}
name: VEB(sat), type: VoltageSource, value: 0.8V, ports: {Np: E, Nn: B}
name: VEC(sat), type: VoltageSource, value: 0.1V, ports: {Np: E, Nn: C}
]
extrainfo:The diagram shows a large-signal model of a PNP BJT in the saturation region. The base-emitter voltage is 0.8V, and the emitter-collector voltage is 0.1V.
FIGURE 2.23 Large-signal models of the pnp BJT in the (a) forward active and (b) saturation region.
### Large-Signal Models for the pnp BJT
As mentioned, the body of knowledge pertaining to the npn BJT can readily be extended to its pnp counterpart provided we reverse all current directions and voltage polarities. The pnp models are shown in Fig. 2.23. To point out similarities and differences between the $n p n$ and $p n p$ devices, and also to initiate the reader to basic BJT circuit methodologies, let us consider a practical circuit example.
In the circuit of Fig. 2.24 find $V_{1}$ so that $V_{2}=5 \mathrm{~V}$. Show all voltages and currents in your final circuit.
#### Solution
Start out at $V_{2}$ and work your way back to $V_{1}$, one step at a time. The numerical result of each step is identified by the corresponding step number in Fig. 2.25.
1. By Ohm's law, $Q_{2}$ 's collector current is $I_{C 2}=V_{2} / R_{5}=5 / 1=5.0 \mathrm{~mA}$, flowing out of the device.
2. Assume $Q_{2}$ is in the FA region. Then, its emitter current is $I_{E 2}=I_{C 2} / \alpha_{F 2}=$ $5 /(100 / 101)=5.05 \mathrm{~mA}$, flowing into $Q_{2}$.
image_name:FIGURE 2.24 Circuit of Example 2.5
description:
[
name: Q1, type: NPN, ports: {C: Vc1, B: Vb, E: E}
name: Q2, type: PNP, ports: {C: V2, B: VC1, E: Ve2}
name: R1, type: Resistor, value: 110kΩ, ports: {N1: V1, N2: Vb}
name: R2, type: Resistor, value: 30kΩ, ports: {N1: Vcc, N2: Vc1}
name: R3, type: Resistor, value: 18kΩ, ports: {N1: E, N2: GND}
name: R4, type: Resistor, value: 1.2kΩ, ports: {N1: Vcc, N2: Ve2}
name: R5, type: Resistor, value: 1.0kΩ, ports: {N1: V2, N2: GND}
name: V1, type: VoltageSource, value: V1, ports: {Np: V1, Nn: GND}
]
extrainfo:The circuit is a two-stage amplifier with transistors Q1 and Q2. Q1 is an NPN transistor and Q2 is a PNP transistor. The circuit is powered by a 15V supply (Vcc). The resistors R1, R2, R3, R4, and R5 set the biasing conditions for the transistors. The circuit includes parameters for transistor beta, V_BE(on), and V_CE(EOS).
FIGURE 2.24 Circuit of Example 2.5.
image_name:FIGURE 2.25 Circuit of Fig. 2.24
description:
[
name: Q1, type: NPN, ports: {C: Vc1, B: Vb1, E: Ve1}
name: Q2, type: PNP, ports: {C: Vc2, B: Vc1, E: Ve2}
name: R1, type: Resistor, value: R1, ports: {N1: Vin, N2: Vb1}
name: R2, type: Resistor, value: 5.05 mA, ports: {N1: VDD, N2: Vc1}
name: R3, type: Resistor, value: 5.0 mA, ports: {N1: Ve1, N2: GND}
name: V1, type: VoltageSource, value: 6V, ports: {Np: VIN, Nn: GND}
name: VDD, type: VoltageSource, value: 15V, ports: {Np: VDCC, Nn: GND}
]
extrainfo:The circuit is a two-stage amplifier powered by a 15V supply. It includes an NPN transistor (Q1) and a PNP transistor (Q2). Resistors R1, R2, and R3 set the biasing conditions. The circuit shows voltage and current values at various nodes, indicating the operational conditions of the transistors.
FIGURE 2.25 Circuit of Fig. 2.24 with each voltage and current identified by the corresponding computational step number in the text.
3. By Ohm's law and KVL, $Q_{2}$ 's emitter voltage is $V_{E 2}=V_{C C}-R_{4} I_{E 2}=15-1.2 \times$ $5.05=8.94 \mathrm{~V}$.
4. Check: $V_{E C 2}=V_{E 2}-V_{C 2}=8.94-5=3.94 \mathrm{~V}>0.2 \mathrm{~V}$, thus confirming that $Q_{2}$ is in the FA region.
5. Since $Q_{2}$ is in the FA region, its base current is $I_{B 2}=I_{C 2} / \beta_{F 2}=5 / 100=0.05 \mathrm{~mA}$, flowing out of $Q_{2}$.
6. By KVL, $Q_{2}$ 's base voltage is $V_{B 2}=V_{E 2}-V_{E B 2(\text { on })}=8.94-0.7=8.24 \mathrm{~V}$. This is also $Q_{1}$ 's collector voltage $V_{C 1}$.
7. By Ohm's law, the current through $R_{2}$ is $I_{R_{2}}=\left(V_{C C}-V_{C 1}\right) / R_{2}=(15-8.24) / 30=$ 0.225 mA .
8. By KCL, $Q_{1}$ 's collector current is $I_{C 1}=I_{R_{2}}+I_{B 2}=0.225+0.05=0.275 \mathrm{~mA}$, flowing into $Q_{1}$.
9. Assume $Q_{1}$ is in the FA region. Then, its emitter current is $I_{E 1}=I_{C 1} / \alpha_{F 1}=$ $0.275 /(100 / 101)=0.278 \mathrm{~mA}$, flowing out of $Q_{1}$.
10. By Ohm's law, $Q_{1}$ 's emitter voltage is $V_{E 1}=R_{3} I_{E 1}=18 \times 0.278=5.0 \mathrm{~V}$.
11. Check: $V_{C E 1}=V_{C 1}-V_{E 1}=8.24-5=3.24>0.2 \mathrm{~V}$, thus confirming that $Q_{1}$ is in the FA region.
12. By KVL, $Q_{1}$ 's base voltage is $V_{B 1}=V_{E 1}+V_{B E 1(\text { on })}=5.0+0.7=5.7 \mathrm{~V}$.
13. Since $Q_{1}$ is in the FA region, its base current is $I_{B 1}=I_{C 1} / \beta_{F 1}=0.275 / 100=$ $2.75 \mu \mathrm{~A}$, into $Q_{1}$.
14. By Ohm's law and KVL, the required voltage is $V_{1}=R_{1} I_{B 1}+V_{B 1}=0.110 \times$ $2.75+5.7=6.0 \mathrm{~V}$.
The student is urged to trace through each step in detail, referring also to the FA models of Figs. $2.21 b$ and 2.23a.
### Finding the Operating Mode of a BJT
A frequent task in the dc analysis of BJT circuits is to find a BJT's operating mode in a given circuit. Barring the seldom-used reverse-active mode, a BJT can be either in the cutoff (CO), or forward active (FA), or saturation (Sat) regions. Following is one possible way to proceed for the case of an npn BJT:
- Find the open-circuit voltage $V_{B E(\text { oc })}$ produced by the external circuit across the B-E junction, that is, the voltage between the $B$ and $E$ nodes with the BJT removed from the circuit. If $V_{B E(\mathrm{oc})}<V_{B E(\mathrm{EOC})} \cong 0.6 \mathrm{~V}$, then the BJT is in CO, and we are finished. Otherwise, it is on, and it is either in FA or in Sat.
- Assume FA operation. Using the FA large-signal BJT model, find the operating point $Q=Q\left(I_{C}, V_{C E}\right)$, and check whether the assumption was correct by examining $V_{C E}$. If $V_{C E}>V_{C E(\mathrm{EOS})} \cong 0.2 \mathrm{~V}$, then the BJT is indeed in FA, and we are finished.
- Conversely, if our calculation yields $V_{C E}<V_{C E(\mathrm{EOS})} \cong 0.2 \mathrm{~V}$, the BJT must be saturated, and we need to recalculate $I_{C}$, but via the saturation model, which uses $V_{C E}=V_{C E(\text { sat })} \cong 0.1 \mathrm{~V}$. As a final check, take the ratio $\beta_{\text {sat }}=I_{C} / I_{B}$, and verify that indeed you get $\beta_{\text {sat }}<\beta_{F}$.
This procedure applies to the pnp BJT as well, provided we reverse all current directions and voltage polarities. Specifically, if $V_{E B(\mathrm{oc})}<V_{E B(\mathrm{EOC})} \cong 0.6 \mathrm{~V}$, the pnp device is in CO. Otherwise it is on, and we need to examine $V_{E C}$ to tell its operating mode. If our calculation yields $V_{E C}>V_{E C(\mathrm{EOS})} \cong 0.2 \mathrm{~V}$, then the BJT is in FA. Otherwise, it is saturated, and we recalculate $I_{C}$ via the saturation model, which uses $V_{E C}=$ $V_{E C \text { (sat) }} \cong 0.1 \mathrm{~V}$.
Let the BJT of Fig. 2.26a have $\beta_{F}=125$, as well as the voltages of Eqs. (2.22) and (2.30).
(a) Find all BJT voltages and currents.
(b) To what value must we increase $R_{C}$ to bring the BJT to the edge of saturation (EOS)?
(c) What happens if $R_{C}$ is raised to twice the value found in part (b)?
#### Solution
(a) Since the base is at 0 V and $R_{E}$ is pulling the emitter toward -5 V , it is clear that the BJT is on. Assume it is in the forward active region, so that $V_{E}=$ -0.7 V . Then, $I_{E}=[-0.7-(-5)] / 4.3=1.0 \mathrm{~mA}, I_{C}=(125 / 126) \times 1.0=$ $0.992 \mathrm{~mA}, V_{C}=5-2 \times 0.992 \cong 3.0 \mathrm{~V}$, and $V_{C E}=V_{C}-V_{E}=3-(-0.7)=$ 3.7 V .
Check: Since $V_{C E}>V_{C E(\mathrm{EOS})}(3.7 \mathrm{~V}>0.2 \mathrm{~V})$, the BJT is indeed in the FA region, as assumed. The situation is summarized in Fig. 2.26b, which also shows that $I_{B}=1.0 / 126=8 \mu \mathrm{~A}$.
Remark: For the purpose of finding $V_{C}$, we could have approximated $I_{C} \cong I_{E}=$ 1.0 mA to speed up our calculations, obtaining results that are still fairly accurate.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: VC1, B: GND, E: VEI}
name: RC, type: Resistor, value: 2 kΩ, ports: {N1: VDD, N2: VC1}
name: RE, type: Resistor, value: 4.3 kΩ, ports: {N1: VEI, N2: -5 V}
name: VDD (a), type: VoltageSource, value: +5 V, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit is a basic NPN transistor amplifier configuration. It includes a voltage divider biasing network and operates in the forward active region. The collector-emitter voltage VCE is 3.7 V, indicating the transistor is in active mode. Resistors RC and RE are used for biasing and stabilization.
image_name:(b)
description:
[
name: Q2, type: NPN, ports: {C: VC1, B: GND, E: VE1}
name: RC, type: Resistor, value: 2 kΩ, ports: {N1: VDD, N2: VC1}
name: RE, type: Resistor, value: 4.3 kΩ, ports: {N1: VE1, N2: GND}
name: VDD, type: VoltageSource, value: 5 V, ports: {Np: VDD, Nn: GND}
]
extrainfo:This circuit is operating in the forward active region with Q2 having V_CE = 3.7 V, I_C = 0.992 mA, and I_B = 8 μA. The voltage across the collector and emitter is greater than the saturation voltage, confirming the active region operation.
image_name:(c)
description:
[
name: Q3, type: NPN, ports: {C: VC1(-0.5V), B: GND, E: VE1(-0.7V)}
name: RC, type: Resistor, value: 5.5kΩ, ports: {N1: VDD(5V), N2: VC1(-0.5V)}
name: RE, type: Resistor, value: 4.3kΩ, ports: {N1: VE1(-0.7V), N2: -5V}
name: VDD, type: VoltageSource, value: 5V, ports: {Np: VDD(5V), Nn: GND}
]
extrainfo:The circuit is in the edge of saturation (EOS) state with Q3 having VCE = 0.2V. The base current is 8 µA, and the collector current is approximately 0.992 mA.
image_name:(d)
description:
[
name: Q4, type: NPN, ports: {C: VC1(-0.7V), B: GND, E: VE1(-0.8V)}
name: RC, type: Resistor, value: 11kΩ, ports: {N1: VDD(5V), N2: VC1(-0.7V)}
name: RE, type: Resistor, value: 4.3kΩ, ports: {N1: VE1(-0.8V), N2: VEE(-5V)}
name: VDD, type: VoltageSource, value: 5V, ports: {Np: VDD(5V), Nn: GND}
name: VEE, type: VoltageSource, value: -5V, ports: {Np: GND, Nn: VEE(-5V)}
]
extrainfo:The circuit diagram (d) operates with Q4 in saturation, with a V_CE of 0.1V. The circuit uses a VDD of 5V and a VEE of -5V, with a collector current of 0.518 mA and an emitter current of 0.977 mA. The base current is 0.459 mA. The resistors RC and RE have values of 11kΩ and 4.3kΩ, respectively.
FIGURE 2.26 (a) Circuit of Example 2.6, and operation (b) in the active region, (c) at the EOS, and (d) in saturation.
(b) At the EOS all currents are still as in the FA case, the only difference being that now $V_{C E}=V_{C E(\mathrm{EOS})}=0.2 \mathrm{~V}$. As depicted in Fig. 2.26c, we now have $V_{C}=V_{E}+V_{C E E O S)}=-0.7+0.2=-0.5 \mathrm{~V}$. Thus, the value of $R_{C}$ that brings the BJT to the EOS is $R_{C}=[5-(-0.5)] / 0.992 \cong 5.5 \mathrm{k} \Omega$, as shown.
(c) We claim that with $R_{C}=2 \times 5.5=11 \mathrm{k} \Omega$ the BJT is saturated. To convince ourselves, let us pretend it is still in FA. Then, we'd have $V_{C}=5-11 \times 0.992=$ -5.9 V , and $V_{C E}=-5.9-(-0.7)=-5.2 \mathrm{~V}$, an impossible proposition! So, the BJT must be saturated at $V_{C E}=V_{C E(\text { sat) }}=0.1 \mathrm{~V}$ and $V_{B E(\text { sat })}=-0.8 \mathrm{~V}$
This is depicted in Fig. 2.26d. We now have $I_{E}=(5-0.8) / 4.3=0.977 \mathrm{~mA}, V_{C}=$ $-0.8+0.1=-0.7 \mathrm{~V}$, and $I_{C}=5.7 / 11=0.518 \mathrm{~mA}$. By KCL, the base current is now
$$
I_{B}=I_{E}-I_{C}=0.977-0.518=0.459 \mathrm{~mA}
$$
quite an increase from the FA value of 0.008 mA !
Check: Just to make sure, calculate $\beta_{\text {sat }}=0.518 / 0.459 \cong 1.1$. Since $\beta_{s a t}<\beta_{F}$ ( $1.1<125$ ), the BJT is indeed in deep saturation!
In the popular circuit of Fig. 2.27a, the voltage divider made up of $R_{1}$ and $R_{2}$ establishes a bias voltage for the base, while $R_{E}$ and $R_{C}$ set the BJT's operating point. To simplify analysis, it is convenient to replace the voltage divider with its Thévenin equivalent, consisting of the open-circuit voltage source
$$
\begin{equation*}
V_{B B}=\frac{R_{2}}{R_{1}+R_{2}} V_{C C} \tag{2.31a}
\end{equation*}
$$
and series resistance
$$
\begin{equation*}
R_{B}=R_{1} / / R_{2} \tag{2.31b}
\end{equation*}
$$
image_name:(a)
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: VCC, N2: Vb1}
name: R2, type: Resistor, value: R2, ports: {N1: Vb1, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Vc1}
name: RE, type: Resistor, value: RE, ports: {N1: Ve1, N2: GND}
name: Q1, type: NPN, ports: {C: Vc1, B: Vb1, E: Ve1}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
]
extrainfo:The circuit is a single-supply BJT amplifier with a voltage divider biasing network formed by R1 and R2. The BJT operating point is set by RC and RE. VCC is the supply voltage.
(a)
image_name:Figure 2.27 (b)
description:
[
name: RB, type: Resistor, value: RB, ports: {N1: VBB, N2: X2}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: X1}
name: RE, type: Resistor, value: RE, ports: {N1: P, N2: GND}
name: VBB, type: VoltageSource, value: VBB, ports: {Np: VBB, Nn: GND}
name: VBE, type: VoltageSource, value: VBE, ports: {Np: X2, Nn: P}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: CurrentSource, type: CurrentControlledCurrentSource, ports: {Np: X1, Nn: P}
]
extrainfo:The circuit is a single-supply BJT amplifier with a voltage divider biasing network. The BJT is represented by a current-controlled current source in the forward active region. The circuit includes biasing through VBB and stabilization through RE.
(b)
image_name:(c)
description:
[
'name': 'RB', 'type': 'Resistor', 'value': 'RB', 'ports': {'N1': 'VBB', 'N2': 'X2'
'name': 'RC', 'type': 'Resistor', 'value': 'RC', 'ports': {'N1': 'VCC', 'N2': 'X1'
'name': 'RE', 'type': 'Resistor', 'value': 'RE', 'ports': {'N1': 'VE', 'N2': 'GND'
'name': 'VBB', 'type': 'VoltageSource', 'value': 'VBB', 'ports': {'Np': 'VBB', 'Nn': 'GND'
'name': 'VCC', 'type': 'VoltageSource', 'value': 'VCC', 'ports': {'Np': 'VCC', 'Nn': 'GND'
'name': 'VCE', 'type': 'VoltageSource', 'value': 'VCE', 'ports': {'Np': 'X1', 'Nn': 'VE'
'name': 'VBE', 'type': 'VoltageSource', 'value': 'VBE', 'ports': {'Np': 'X2', 'Nn': 'GND'
]
extrainfo:The circuit is a single-supply BJT amplifier with a voltage divider biasing network. The BJT is represented by a current-controlled current source in the forward active region. The circuit includes biasing through VBB and stabilization through RE.
FIGURE 2.27 (a) A popular single-supply BJT circuit, and its equivalents for the case of the BJT operating in the (b) forward active and (c) saturation region.
Then, the circuit reduces to either equivalent of Fig. $2.27 b$ or $2.27 c$, depending on whether the BJT is operating in the forward active or saturation mode. In this regard, we make the following observations:
- In the forward active equivalent of Fig. $2.27 b$ we apply KVL and write
$$
V_{B B}=R_{B} I_{B}+V_{B E(\mathrm{on})}+R_{E}\left(\beta_{F}+1\right) I_{B}
$$
Solving for $I_{B}$, and then multiplying by $\beta_{F}$, we get
$$
\begin{equation*}
I_{C}=\beta_{F} \frac{V_{B B}-V_{B E(\mathrm{on})}}{R_{B}+\left(\beta_{F}+1\right) R_{E}} \tag{2.32}
\end{equation*}
$$
- In the saturation equivalent of Fig. 2.27c we apply KCL and write
$$
\begin{equation*}
\frac{V_{B B}-\left(V_{E}+V_{B E(\text { sat })}\right)}{R_{B}}+\frac{V_{C C}-\left(V_{E}+V_{C E(\text { sat })}\right)}{R_{C}}=\frac{V_{E}}{R_{E}} \tag{2.33}
\end{equation*}
$$
This equation is readily solved for $V_{E}$, after which we can find all other voltages and all currents in the circuit via repeated usage of KVL and Ohm's law.
In the circuit of Fig. $2.27 a$, let $V_{C C}=9 \mathrm{~V}, R_{1}=30 \mathrm{k} \Omega, R_{2}=15 \mathrm{k} \Omega, R_{C}=3.0 \mathrm{k} \Omega$,
EXAMPLE 2.7 and $R_{E}=2.2 \mathrm{k} \Omega$, and let the BJT have $\beta_{F}=100$ as well as the voltages of Eqs. (2.22) and (2.30).
(a) Find all BJT voltages and currents, and show them in the circuit.
(b) Repeat part (a) if $R_{E}$ is lowered to $0.75 \mathrm{k} \Omega$.
(c) Repeat (a) if $R_{2}$ is lowered to $1.0 \mathrm{k} \Omega$.
image_name:(a)
description:
[
name: V1, type: VoltageSource, value: 9V, ports: {Np: VDD, Nn: GND}
name: R1, type: Resistor, value: 30kΩ, ports: {N1: VDD, N2: VB}
name: R2, type: Resistor, value: 15kΩ, ports: {N1: VB, N2: GND}
name: R3, type: Resistor, value: 3.0kΩ, ports: {N1: VDD, N2: VC}
name: R4, type: Resistor, value: 2.2kΩ, ports: {N1: VE, N2: GND}
name: Q1, type: NPN, ports: {C: VC, B: VB, E: VE}
]
extrainfo:The circuit is a BJT amplifier with a voltage divider biasing network. It operates in the forward active region with a base voltage of 2.9V, collector voltage of 6.0V, and emitter voltage of 2.2V in part (a). The current through the collector is 0.99 mA, and the base current is 0.01 mA.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: 1.9V, B: 2.6V, E: 1.8V}
name: 3.0kΩ, type: Resistor, value: 3.0kΩ, ports: {N1: 9V, N2: 1.9V}
name: R1, type: Resistor, value: 30kΩ, ports: {N1: 9V, N2: 2.6V}
name: R2, type: Resistor, value: 15kΩ, ports: {N1: 2.6V, N2: GND}
name: R3, type: Resistor, value: 0.75kΩ, ports: {N1: 1.8V, N2: GND}
name: 9V, type: VoltageSource, value: 9V, ports: {Np: 9V, Nn: GND}
]
extrainfo:The circuit is a BJT amplifier with resistive biasing. The BJT Q1 operates in forward active mode with a collector current of 2.36 mA and a base current of 0.04 mA. The emitter resistor has been lowered to 0.75kΩ, increasing the emitter current to 2.40 mA.
FIGURE 2.28 Circuits of Example 2.6, showing (a) forward active operation with $\beta_{F}=100$, and (b) saturation operation with $\beta_{\text {sat }}=59$.
#### Solution
(a) Assume the BJT is in the FA region. Applying Eq. (2.31), we get
$$
V_{B B}=\frac{15}{30+15} 9=3 \mathrm{~V} \quad R_{B}=\frac{30 \times 15}{30+15}=10 \mathrm{k} \Omega
$$
Using Eq. (2.32), we obtain
$$
I_{C}=100 \frac{3-0.7}{10+101 \times 2.2}=0.99 \mathrm{~mA}
$$
Consequently, we have $I_{B}=I_{C} / \beta_{F}=0.99 / 100 \cong 0.01 \mathrm{~mA}, I_{E}=I_{C} / \alpha_{F}=$ 0.99/(100/101) = 1.0 mA . Also,
$$
\begin{aligned}
& V_{B}=V_{B B}-R_{B} I_{B}=3-10 \times 0.01=2.9 \mathrm{~V} \\
& V_{C}=V_{C C}-R_{C} I_{C}=9-3.0 \times 0.99 \cong 6.0 \mathrm{~V} \\
& V_{E}=V_{B}-V_{B E(\mathrm{on})}=2.9-0.7=2.2 \mathrm{~V}
\end{aligned}
$$
All voltages and currents are shown in Fig. 2.28a.
Check: We have $V_{C E}=V_{C}-V_{E}=6.0-2.2=3.8 \mathrm{~V}$. Since $V_{C E}>V_{C E(\mathrm{EOS})}(3.8 \mathrm{~V}>$ 0.2 V ), the BJT is indeed in the FA region, as assumed.
Remark: The actual base voltage $\left(V_{B}=2.9 \mathrm{~V}\right)$ is a bit less than the open-circuit voltage $\left(V_{B B}=3 \mathrm{~V}\right.$ ) because of the tiny base current, which causes the BJT to load down the base-biasing network.
(b) We can start out again assuming forward active operation. Repeating the above calculations but with $R_{E}=0.75 \mathrm{k} \Omega$ we get $I_{C} \cong 2.7 \mathrm{~mA}$, so $V_{C E} \cong 9-$ $3 \times 2.7-0.75 \times 2.7=-1 \mathrm{~V}$. Since this would imply $V_{C E}<V_{C E(\mathrm{EOS})}(-1 \mathrm{~V}<$ 0.2 V ), we conclude that the BJT is now saturated, and we can no longer use
the active-region relationships, such as $I_{C}=\beta_{F} I_{B}$ and the like. We must apply Eq. (2.33) instead, and write
$$
\frac{3-\left(V_{E}+0.8\right)}{10}+\frac{9-\left(V_{E}+0.1\right)}{3}=\frac{V_{E}}{0.75}
$$
Solving for $V_{E}$, we get
$$
\begin{aligned}
& V_{E}=95.6 / 53=1.8 \mathrm{~V} \\
& V_{B}=1.8+0.8=2.6 \mathrm{~V} \\
& V_{C}=1.8+0.1=1.9 \mathrm{~V}
\end{aligned}
$$
Moreover,
$$
I_{B}=\frac{3-2.6}{10}=0.04 \mathrm{~mA} \quad I_{C}=\frac{9-1.9}{3}=2.36 \mathrm{~mA} \quad I_{E}=\frac{1.8}{0.75}=2.40 \mathrm{~mA}
$$
(Note, as a check, that the currents satisfy KCL.) All voltages and currents are shown in Fig. 2.28b.
Check: Just to make sure, calculate $\beta_{\text {sat }}=2.36 / 0.04=59$. Since $\beta_{\text {sat }}<$ $\beta_{F}(59<100)$, the BJT is indeed in saturation!
Remark: In the present example we have driven the BJT in saturation by lowering $R_{E}$ and thus increasing $I_{C}$. In Example 2.5 we drove it in saturation by raising $R_{C}$. Both changes lowered $V_{C}$ to the point of trying to make $V_{C E}<V_{C E(\mathrm{EOS})}$. Any other change in the circuit that will decrease the value of $V_{C E}$ will tend to drive the BJT in saturation. Possible examples are increasing $V_{B B}$, or replacing the BJT with another unit with higher $\beta_{F}$, or a combination of both.
(c) We now have $V_{B B}=[1 /(30+1)] 9=0.29 \mathrm{~V}$. This is insufficient to turn on the B-E junction convincingly. The BJT is now cut off, and all currents are for practical purposes zero. Moreover, $V_{B} \cong 0.29 \mathrm{~V}, V_{E} \cong 0$, and $V_{C} \cong 9 \mathrm{~V}$.
Assuming the BJTs in the circuit of Fig. $2.29 a$ have $\beta_{F 1}=\beta_{F 2}=100$ and baseemitter voltage drops of 0.7 V , find all BJT terminal voltages and currents, and show them explicitly.
#### Solution
Consider the two BJT circuits separately, one at a time. Turning first to $Q_{1}$ and its related resistors, and performing the usual Thévenin reduction of its base-biasing network, we end up with the equivalent of Fig. 2.30a. By KVL we have
$$
V_{C C}=R_{3}\left(\beta_{F 1}+1\right) I_{B 1}+V_{E B 1(\mathrm{on})}+R_{B 1} I_{B 1}+V_{B B 1}
$$
or
$$
12=18(100+1) I_{B 1}+0.7+75 I_{B 1}+7.5
$$
image_name:FIGURE 2.29 (a)
description:
[
name: R1, type: Resistor, value: 120kΩ, ports: {N1: b1, N2: VCC}
name: R2, type: Resistor, value: 200kΩ, ports: {N1: b1, N2: GND}
name: R3, type: Resistor, value: 18kΩ, ports: {N1: VCC, N2: e1}
name: R4, type: Resistor, value: 20kΩ, ports: {N1: clb2, N2: GND}
name: R5, type: Resistor, value: 1.6kΩ, ports: {N1: VCC, N2: c1}
name: R6, type: Resistor, value: 1.1kΩ, ports: {N1: e2, N2: GND}
name: Q1, type: PNP, ports: {C: clb2, B: b1, E: e1}
name: Q2, type: NPN, ports: {C: c1, B: clb2, E: e2}
name: VCC, type: VoltageSource, value: 12V, ports: {Np: VCC, Nn: GND}
]
extrainfo:This circuit involves two BJTs, Q1 (PNP) and Q2 (NPN), configured with resistors R1 to R6, a capacitor C1, and a voltage source VCC. The circuit is designed for biasing and amplification purposes, utilizing a combination of voltage divider biasing and coupling capacitors.
(a)
image_name:Figure 2.29 (b)
description:
[
name: Q1, type: PNP, ports: {C: c1b2, B: b1, E: e1}
name: Q2, type: NPN, ports: {C: c2, B: c1b2, E: e2}
name: VCC, type: VoltageSource, value: 12V, ports: {Np: VCC, Nn: GND}
name: R1, type: Resistor, value: 120kΩ, ports: {N1: VCC, N2: b1}
name: R2, type: Resistor, value: 18kΩ, ports: {N1: VCC, N2: e1}
name: R3, type: Resistor, value: 200kΩ, ports: {N1: b1, N2: GND}
name: R4, type: Resistor, value: 20kΩ, ports: {N1: c1b2, N2: GND}
name: R5, type: Resistor, value: 1.6kΩ, ports: {N1: VCC, N2: c2}
name: R6, type: Resistor, value: 1.1kΩ, ports: {N1: e2, N2: GND}
]
extrainfo:The circuit is designed for biasing and amplification using two BJTs, Q1 (PNP) and Q2 (NPN). The voltage and current values at various nodes are explicitly shown, indicating the biasing conditions and operating points of the transistors. The circuit uses a combination of voltage divider biasing and coupling capacitors to achieve stability and amplification.
(b)
FIGURE 2.29 (a) Circuit of Example 2.7. (b) Showing all BJT voltages and currents explicitly.
image_name:Figure 2.30 (a)
description:
[
name: Q1, type: PNP, ports: {C: Vc1, B: b1, E: e1}
name: RB1, type: Resistor, value: 75kΩ, ports: {N1: VBB1, N2: b1}
name: R3, type: Resistor, value: 18kΩ, ports: {N1: VCC, N2: e1}
name: R4, type: Resistor, value: 20kΩ, ports: {N1: Vc1, N2: GND}
name: VCC, type: VoltageSource, value: 12V, ports: {Np: VCC, Nn: GND}
name: VBB1, type: VoltageSource, value: 7.5V, ports: {Np: VBB1, Nn: GND}
]
extrainfo:The circuit is designed for biasing and amplification using a PNP BJT, Q1. It shows the biasing conditions with explicit voltage and current values at various nodes. The circuit uses voltage divider biasing and coupling capacitors to achieve stability and amplification.
(a)
image_name:(b)
description:
[
name: VCC, type: VoltageSource, value: 12V, ports: {Np: VCC, Nn: GND}
name: VBB2, type: VoltageSource, value: 4.00V, ports: {Np: VBB2, Nn: GND}
name: R5, type: Resistor, value: 1.6kΩ, ports: {N1: VCC, N2: c2}
name: R6, type: Resistor, value: 1.1kΩ, ports: {N1: e2, N2: GND}
name: RB2, type: Resistor, value: 20kΩ, ports: {N1: VBB2, N2: b2}
name: Q2, type: NPN, ports: {C: c2, B: b2, E: e2}
]
extrainfo:The circuit is designed for biasing and amplification using an NPN BJT, Q2. It uses a voltage divider biasing method with resistors R5 and R6 to stabilize the transistor's operation. The voltage source VBB2 provides a bias voltage for the base of the transistor.
(b)
FIGURE 2.30 Intermediate steps in the analysis of the circuit of Fig. 2.29a.
This gives
$$
I_{B 1}=2 \mu \mathrm{~A} \quad I_{C 1}=100 \times 2=200 \mu \mathrm{~A} \quad I_{E 1}=101 \times 2=202 \mu \mathrm{~A}
$$
Moreover, we have
$$
\begin{aligned}
& V_{B 1}=7.5+75 \times 0.002=7.65 \mathrm{~V} \\
& V_{E 1}=7.65+0.7=8.35 \mathrm{~V} \\
& V_{C 1(\mathrm{oc})}=20 \times 0.200=4.00 \mathrm{~V}
\end{aligned}
$$
where $V_{C 1(\text { oc })}$ is the open-circuit voltage at $Q_{1}$ 's collector. Once we bring $Q_{2}$ 's back into the picture, this voltage will act as $V_{B B 2}$ to $Q_{2}$, and $R_{4}$ will act as $R_{B 2}$. For the
purpose of our calculations we can thus replace the entire circuit based on $Q_{1}$ with its Thévenin equivalent and work with the much simpler equivalent of Fig. 2.30b. This circuit is similar to that of Fig. 2.27b, so we can proceed in the manner of Example 2.7, and come up with the voltages and currents shown in Fig. 2.29b.
Remark: Because of $I_{B 1}, V_{B 1}$ is a bit higher than $V_{B B 1}$, and because of $I_{B 2}, V_{B 2}$ is a bit lower than $V_{B B 2}$. As we know, these effects are commonly referred to as loading.
### The Diode Mode of Operation
Tying the base and collector together turns a BJT into a two-terminal device. To find its $i-v$ characteristic we subject it to a test voltage $v$ and examine its current response $i$, as shown in Fig. 2.31a. By KCL,
$$
\begin{equation*}
i=i_{B}+i_{C}=\left(\frac{1}{\beta_{F}}+1\right) i_{C}=\frac{I_{s}}{\alpha_{F}} e^{v / V_{T}} \tag{2.34}
\end{equation*}
$$
indicating that the two-terminal device acts as a diode having the $B-C$ terminal as the anode $(A)$, the emitter terminal as the cathode $(C)$, and $I_{s} / \alpha_{F}\left(\cong I_{s}\right)$ as the saturation current. In fact, in integrated circuits this is how a diode is often created, namely, using a BJT with its $B$ and $C$ terminals tied together. The analysis of circuits incorporating a diode-connected BJT proceeds as in the case of ordinary diodes.
In the circuit of Fig. $2.31 b$ let the BJT have $I_{s}=10 \mathrm{fA}, \beta_{F}=100$, and $V_{B E(\mathrm{~m})}=0.7 \mathrm{~V}$.
(a) Find $I$ if $V_{C C}=5 \mathrm{~V}$ and $R=10 \mathrm{k} \Omega$.
(b) Repeat, but for $V_{C C}=0.75 \mathrm{~V}$ and $R=1 \mathrm{k} \Omega$.
#### Solution
(a) Since $V_{C C} \gg V$, we don't need to know $V$ that accurately, so we approximate $V \cong V_{B E(\mathrm{on})}=0.7 \mathrm{~V}$, and write
$$
I=\frac{V_{C C}-V}{R} \cong \frac{5-0.7}{10}=0.43 \mathrm{~mA}
$$
image_name:(a)
description:
[
name: V, type: VoltageSource, ports: {Np: A, Nn: C}
name: Q, type: NPN, ports: {C: A, B: A, E: C}
]
extrainfo:The circuit is a diode-connected BJT configuration where the base and collector are shorted together. The voltage source V is connected between nodes A and C.
image_name:(b)
description:
[
name: v, type: VoltageSource, ports: {Np: VCC, Nn: GND}
name: Q, type: NPN, ports: {C: cb, B: cb, E: GND}
name: R, type: Resistor, value: R, ports: {N1: VCC, N2: cb}
]
extrainfo:The circuit is a diode-connected BJT configuration with a voltage source VCC, a resistor R, and an NPN transistor Q. The collector of Q is connected to VCC, the base is connected to node V (between R and Q), and the emitter is connected to GND. The resistor R is connected between VCC and node V.
FIGURE 2.31 Diode-connected BJT. (a) Test circuit to find its $i-v$
(b) characteristic. (b) Circuit example.
(b) In this case $V_{C C}$ is too close to $V_{B E(0 n)}$ for us to proceed as in part (a). Rather, we need to apply the familiar iterative technique for diodes, and find $V$ first,
$$
V=V_{T} \ln \frac{I}{I_{s} / \alpha_{F}} \cong V_{T} \ln \frac{\left(V_{C C}-V\right) / R}{I_{s}}=0.026 \ln \frac{0.75-V}{10^{-11}}
$$
Starting out with the initial estimate $V=0.65 \mathrm{~V}$, we find, after a few iterations, $V=0.6078 \mathrm{~V}$. Consequently, $I=(0.75-0.608) / 1=0.142 \mathrm{~mA}$.
## 2.5 THE BJT AS AN AMPLIFIER/SWITCH
We shall now investigate the two most important BJT applications: amplification and switching. To this end, refer to the basic circuit of Fig. 2.32, where $R_{B}$ serves the function of converting $v_{I}$ to the base drive $i_{B}$, and $R_{C}$ and $Q$ can be viewed as forming a voltage divider of sorts: $R_{C}$ tends to pull $v_{O}$ up toward $V_{C C}$, and $Q$ tends to pull $v_{O}$ down toward ground. Depending on which pull action prevails, $v_{O}$ will assume a value somewhere in between. The plot of $v_{O}$ versus $v_{I}$, called the voltage transfer curve (VTC), provides much insight into the capabilities of this circuit. Figure 2.33 shows the VTC as well as other pertinent curves for the case in which $v_{I}$ is swept from 0 V to 2 V and the BJT possesses the characteristics tabulated in Fig. 2.32. We make the following observations:
- For $v_{I}<V_{B E(\mathrm{EOC})} \cong 0.6 \mathrm{~V}$, the B-E junction is insufficiently biased and the BJT is therefore in cutoff. With no current being drawn by the collector, the voltage across $R_{C}$ is 0 V , indicating that $R_{C}$ is pulling $v_{O}$ all the way up to $V_{C C}$. We express this by writing $v_{O}=V_{O H}$, where
$$
\begin{equation*}
V_{O H}=V_{C C}=5 \mathrm{~V} \tag{2.35}
\end{equation*}
$$
image_name:Figure 2.32
description:
[
name: RC, type: Resistor, value: 1kΩ, ports: {N1: VCC, N2: Vo}
name: RB, type: Resistor, value: 10kΩ, ports: {N1: U1, N2: b}
name: Qn, type: NPN, ports: {C: Vo, B: b, E: GND}
name: VI, type: VoltageSource, ports: {Np: U1, Nn: GND}
]
extrainfo:The circuit is a BJT amplifier/switch with a voltage source VI providing input to the base of the NPN transistor Qn. RC is connected between VCC and the collector of Qn, while RB is connected between the input voltage source VI and the base of Qn. The emitter of Qn is connected to ground. The parameters for the transistor Qn are Is = 2 fA, βF = 100, and VA = ∞.
FIGURE 2.32 PSpice circuit to investigate the BJT as an amplifier/ switch.
image_name:Base current iB
description:The graph titled "Base current iB" is a plot showing the behavior of the base current \( i_B \) in microamperes (\( \mu A \)) as a function of the input voltage \( v_I \) in volts (V). The x-axis represents the input voltage \( v_I \) ranging from 0 to 2 volts, while the y-axis represents the base current \( i_B \) ranging from 0 to 150 microamperes. The scale for both axes is linear.
Overall Behavior and Trends:
- **Cutoff Region:** At the beginning, when \( v_I \) is near 0 volts, the base current \( i_B \) is at 0 microamperes, indicating the transistor is in the cutoff region.
- **Edge of Conduction (EOC):** As \( v_I \) increases to approximately 0.6 volts, the base current begins to increase from 0, marking the edge of conduction.
- **Forward Active Region:** As \( v_I \) continues to increase, \( i_B \) rises steadily, indicating the transistor is in the forward active region.
- **Saturation Region:** Beyond a certain point (around 1.5 volts), \( i_B \) continues to increase, reaching higher values as the transistor approaches saturation.
Key Features:
- **Annotations:** The graph is annotated with key regions such as Cutoff, EOC (Edge of Conduction), and Saturation.
- **Critical Points:**
- At \( V_{I(EOC)} \approx 0.6 \) V, the base current starts to rise.
- The transition to saturation occurs as \( v_I \) approaches 1.5 volts and beyond.
This graph is part of a series of plots analyzing the behavior of a BJT amplifier/switch circuit as the input voltage is varied, illustrating the transition of the transistor through different operational regions.
image_name:Collector current iC
description:Type of Graph and Function:
The graph is a plot of the collector current \(i_C\) of a BJT transistor as a function of the input voltage \(v_I\). It is a linear graph showing how the collector current changes with varying input voltage.
Axes Labels and Units:
- **X-axis:** Represents the input voltage \(v_I\) in volts (V), ranging from 0 to 2 volts.
- **Y-axis:** Represents the collector current \(i_C\) in milliamperes (mA), ranging from 0 to 5 mA.
- The scale used is linear for both axes.
Overall Behavior and Trends:
- The graph begins at the origin with \(i_C = 0\) mA when \(v_I = 0\) V, indicating the cutoff region.
- As \(v_I\) increases past approximately 0.6 V (the edge of conduction, EOC), \(i_C\) begins to rise sharply, entering the forward active (FA) region.
- The collector current reaches its peak near \(v_I = 1.2\) V, marking the edge of saturation (EOS).
- Beyond this point, \(i_C\) levels off, indicating the transistor is in full saturation.
Key Features and Technical Details:
- **EOC (Edge of Conduction):** At \(v_I \approx 0.6\) V, \(i_C\) starts to increase significantly.
- **FA (Forward Active Region):** Between approximately 0.6 V and 1.2 V, \(i_C\) increases linearly.
- **EOS (Edge of Saturation):** Around \(v_I = 1.2\) V, \(i_C\) reaches a maximum value.
- **Saturation:** Beyond 1.2 V, \(i_C\) remains constant, indicating full saturation.
Annotations and Specific Data Points:
- The graph is annotated with regions such as "Cutoff," "EOC," "FA," "EOS," and "Saturation" to indicate different operating states of the BJT.
- The peak collector current is labeled as \(I_{C(\text{sat})}\), which occurs at the saturation region.
image_name:Output vO
description:The graph titled "Output vO" is part of a series of plots analyzing the behavior of a BJT amplifier/switch circuit. This specific graph is a voltage output plot, showing the relationship between the output voltage \( v_O \) and the input voltage \( v_I \).
1. **Type of Graph and Function:**
- This is a voltage transfer characteristic graph, depicting how the output voltage \( v_O \) changes as the input voltage \( v_I \) is varied.
2. **Axes Labels and Units:**
- The x-axis represents the input voltage \( v_I \) in volts (V), ranging from 0 to 2 V.
- The y-axis represents the output voltage \( v_O \) in volts (V), also ranging from 0 to 5 V.
3. **Overall Behavior and Trends:**
- The graph starts with a high output voltage near 5 V when the input voltage \( v_I \) is low, indicating the cutoff region.
- As \( v_I \) increases towards approximately 0.6 V, the output voltage remains relatively constant, representing the transition from cutoff to the forward active (FA) region.
- In the forward active region, as \( v_I \) continues to increase, \( v_O \) begins to decrease linearly.
- As \( v_I \) approaches 1.5 V, the output voltage drops sharply, indicating the transition from the forward active region to the edge of saturation (EOS).
- Beyond this point, \( v_O \) reaches a low saturation level, close to 0 V, as \( v_I \) continues to increase.
4. **Key Features and Technical Details:**
- The graph highlights key regions such as Cutoff, Forward Active (FA), and Saturation.
- Critical points include the high output voltage \( V_{OH} \) in the cutoff region and low output voltage \( V_{OL} \) in saturation.
- The edge of conduction (EOC) is marked around \( v_I = 0.6 \) V, and the edge of saturation (EOS) is indicated around \( v_I = 1.5 \) V.
5. **Annotations and Specific Data Points:**
- The graph is annotated with labels for regions (Cutoff, FA, Saturation) and specific points such as \( V_{OH} \) and \( V_{OL} \).
- Reference lines or markers are not explicitly shown, but the transitions between regions are clearly marked.
image_name:Current ratio iC/iB
description:The graph titled "Current ratio iC/iB" illustrates the behavior of the current gain (β) of a BJT as a function of the input voltage (vI) in volts (V). The x-axis represents the input voltage vI ranging from 0 to 2 volts. The y-axis represents the current ratio iC/iB, which is dimensionless.
Type of Graph and Function:
This is a linear plot showing how the current gain (β) varies with the input voltage in a BJT circuit.
Axes Labels and Units:
- **X-axis:** Input voltage vI (V), ranging from 0 to 2 V.
- **Y-axis:** Current ratio iC/iB (dimensionless), with values from 0 to 150.
Overall Behavior and Trends:
- The graph shows a nearly constant value of β around 100 when the BJT is in the forward active (FA) region.
- As the input voltage increases beyond the edge of saturation (EOS), the current gain decreases.
Key Features and Technical Details:
- **βF (forward active):** At vI = V_{I(EOC)}, the current ratio is approximately 100, indicating the BJT is in the forward active region.
- **EOS (Edge of Saturation):** As vI approaches V_{I(EOS)}, the current ratio begins to decrease, indicating the transition towards saturation.
- **βsat (Saturation):** In the saturation region, the current ratio decreases further, reflecting the reduced efficiency of current amplification in this region.
Annotations and Specific Data Points:
- **V_{I(EOC)}:** Marked at approximately 0.6 V, indicating the edge of conduction.
- **V_{I(EOS)}:** Another critical point beyond which the current ratio starts to decline.
- **βF:** The flat region where the current ratio is stable around 100.
- **βsat:** The decline in current ratio as the BJT enters saturation.
This graph helps visualize the operational regions of the BJT, highlighting how the current gain varies across different input voltages, and is crucial for understanding the transistor's behavior as an amplifier or switch.
FIGURE 2.33 Plots for the circuit of Fig. 2.32, showing the variations of $i_{B}, i_{C}, v_{O}$, and beta $\left(=i_{C} / i_{B}\right)$ as the BJT is swept from cutoff (CO), to the edge of conduction (EOC), through the forward active (FA) region, to the edge of saturation (EOS), to full saturation (sat).
- As we raise $v_{I}$ to the value
$$
\begin{equation*}
V_{I(\mathrm{EOC})} \cong 0.6 \mathrm{~V} \tag{2.36}
\end{equation*}
$$
the BJT reaches the edge of conduction (EOC) and begins to pull $v_{O}$ down from $V_{C C}$.
- Raising $v_{I}$ further brings the BJT into full conduction. As long as $v_{O} \geq V_{C E(\mathrm{EOS})} \cong$ 0.2 V , the BJT is operating in the forward active (FA) region, where it gives
$$
\begin{equation*}
i_{C}=\beta_{F} i_{B}=100 i_{B} \tag{2.37}
\end{equation*}
$$
Moreover, using KVL, along with Ohm's law and the $v_{B E}-i_{C}$ characteristic of the BJT, we write
$$
v_{I}=R_{B} i_{B}+v_{B E}=R_{B} \frac{i_{C}}{\beta_{F}}+V_{T} \ln \frac{i_{C}}{I_{s}}=R_{B} \frac{V_{C C}-v_{O}}{\beta_{F} R_{C}}+V_{T} \ln \frac{V_{C C}-v_{O}}{R_{C} I_{s}}
$$
With the resistance values and BJT parameters of Fig. 2.32, this expression becomes
$$
\begin{equation*}
v_{I}=\frac{5-v_{O}}{10}+0.026 \ln \frac{5-v_{O}}{2 \times 10^{-12}} \tag{2.38}
\end{equation*}
$$
which can be used to find the input $v_{I}$ needed to sustain a given output $v_{O}$ in the FA region.
- Once the collector voltage drops to $v_{o}=V_{C E(\mathrm{EOS})} \cong 0.2 \mathrm{~V}$, the BJT reaches the edge of saturation (EOS). This designation stems from the fact that the collector current $i_{C}$ starts to saturate, as shown.
Substituting $v_{O}=0.2 \mathrm{~V}$ into Eq. (2.38), we find that the corresponding value of $v_{I}$ is
$$
\begin{equation*}
V_{I(\mathrm{EOS})} \cong 1.22 \mathrm{~V} \tag{2.39}
\end{equation*}
$$
Raising $v_{I}$ above $V_{I(\mathrm{EOS})}$ drives the BJT in full saturation, where $i_{C}$ eventually settles to the value
$$
\begin{equation*}
I_{C(\mathrm{sat})}=\frac{V_{C C}-V_{C E(\mathrm{sat})}}{R_{C}} \cong \frac{5-0.1}{1}=4.9 \mathrm{~mA} \tag{2.40}
\end{equation*}
$$
Accordingly, $v_{O}$ settles to the value
$$
\begin{equation*}
V_{O L}=V_{C E(\mathrm{sat})} \cong 0.1 \mathrm{~V} \tag{2.41}
\end{equation*}
$$
- Past the EOS, $i_{B}$ continues to rise with $v_{I}$ whereas $i_{C}$ remains constant at $i_{C} \cong I_{C(\mathrm{sat})}$. It is apparent that the ratio $i_{C} / i_{B}$ decreases as we drive the BJT further in saturation, so we denote this ratio as $\beta_{s a t}\left(<\beta_{F}\right.$ !). The deeper we drive the BJT in saturation, the lower the value of $\beta_{\text {sat }}$. For instance, for $v_{I}=5 \mathrm{~V}$ we get $i_{B}=\left(V_{C C}-V_{B E(\text { sat) }}\right) / R_{B} \cong$ $(5-0.8) / 10=0.42 \mathrm{~mA}$, and thus $\beta_{\text {sat }}=I_{C(\text { sat })} / i_{B}=4.9 / 0.42 \cong 12$. It is important to realize that while $\beta_{F}$ is an intrinsic parameter of the BJT, the value of $\beta_{\text {sat }}$ is established by the user, depending on how deeply we drive the BJT in saturation.
We wish to point out that in order to simplify our calculations and thus facilitate the comparison of calculated with simulated data, we have assumed $V_{A}=\infty$.
In practice, the effect of non-infinite $V_{A}$ will alter the curves a little, but our general observations still stand.
### The BJT as an Amplifier
The slope of the VTC represents voltage gain, denoted as $a$. Differentiating both sides of Eq. (2.38) with respect to $v_{I}$ we get
$$
\frac{d v_{I}}{d v_{I}}=-\frac{1}{10} \frac{d v_{O}}{d v_{I}}+0.026 \frac{2 \times 10^{-12}}{5-v_{O}}\left(-\frac{1}{2 \times 10^{-12}} \frac{d v_{O}}{d v_{I}}\right)
$$
After simplifying, we obtain, for the parameter values of Fig. 2.32,
$$
\begin{equation*}
a=\frac{d v_{O}}{d v_{I}}=-10 \frac{5-v_{O}}{5.26-v_{O}} \tag{2.42}
\end{equation*}
$$
Figure 2.34 shows the VTC as well as the slope $a$. In cutoff and in saturation we have $a=0$. However, there are two points, denoted as $V_{I L}$ and $V_{I H}$, such that for $V_{I L} \leq$ $v_{I} \leq V_{I H}$ we have $|a|>1 \mathrm{~V} / \mathrm{V}$, indicating that the circuit can be used as an amplifier. As seen, the voltage gain peaks at about $-9 \mathrm{~V} / \mathrm{V}$ just before the EOS.
image_name:Figure 2.34
description:Figure 2.34 consists of two graphs: the Voltage Transfer Curve (VTC) and the slope representing the voltage gain (a).
**Top Graph (Voltage Transfer Curve):**
- **Type of Graph:** Voltage Transfer Curve (VTC).
- **Axes Labels and Units:**
- **X-axis:** Input voltage \(v_I\) in volts (V), ranging from 0 to 2 V.
- **Y-axis:** Output voltage \(v_O\) in volts (V), ranging from 0 to 5 V.
- **Overall Behavior and Trends:**
- The graph shows a nonlinear relationship between input and output voltages.
- The curve starts at 5 V for low input voltages, indicating a cutoff region.
- As \(v_I\) increases, \(v_O\) sharply drops towards 0 V, transitioning through a linear region around 1 V, then flattens at 0 V, indicating a saturation region.
- **Key Features and Technical Details:**
- The transition from cutoff to saturation occurs around \(v_I = 1 V\).
- The steepest part of the curve represents the active region where amplification occurs.
**Bottom Graph (Slope/Voltage Gain):**
- **Type of Graph:** Slope of VTC, representing voltage gain \(a\).
- **Axes Labels and Units:**
- **X-axis:** Input voltage \(v_I\) in volts (V), ranging from 0 to 2 V.
- **Y-axis:** Voltage gain \(a\) in volts per volt (V/V), ranging from 0 to -10 V/V.
- **Overall Behavior and Trends:**
- The gain \(a\) is 0 in both cutoff and saturation regions.
- Between these regions, the gain becomes negative, reaching a minimum value of approximately -9 V/V.
- **Key Features and Technical Details:**
- The gain is significant (|a| > 1 V/V) between two points \(V_{IL}\) and \(V_{IH}\), marking the range where the circuit behaves as an amplifier.
- The gain peaks just before the end of the active region, indicating the maximum amplification capability of the circuit.
- **Annotations and Specific Data Points:**
- \(V_{IL}\) and \(V_{IH}\) are marked on the graph, showing the boundaries of the amplification region.
FIGURE 2.34 The voltage transfer curve (VTC) and its slope, representing the voltage gain a.
image_name:(a)
description:
[
name: VI, type: VoltageSource, value: VI, ports: {Np: vI, Nn: GND}
name: RB, type: Resistor, value: RB, ports: {N1: vI, N2: b}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: vO}
name: Q, type: NPN, ports: {C: vO, B: b, E: GND}
]
extrainfo:The circuit is a BJT voltage amplifier biased at a quiescent point Q0. The voltage transfer curve (VTC) shows a nonlinear behavior with a significant gain between VIL and VIH. The gain peaks near the end of the active region, indicating maximum amplification capability.
image_name:(b)
description:The graph in Figure 2.35(b) is a voltage transfer characteristic (VTC) curve, illustrating the relationship between the input voltage \( v_I \) and the output voltage \( v_O \) of a BJT (bipolar junction transistor) configured as a voltage amplifier.
1. **Type of Graph and Function:**
- This is a VTC graph, which represents the nonlinear relationship between the input and output voltages of the BJT amplifier.
2. **Axes Labels and Units:**
- The horizontal axis represents the input voltage \( v_I \) in volts (V), ranging from 0 to 2.0 V.
- The vertical axis represents the output voltage \( v_O \) in volts (V), ranging from 0 to 5.0 V.
3. **Overall Behavior and Trends:**
- The graph shows a nonlinear curve with distinct regions: cutoff, active, and saturation.
- At low input voltages, the output voltage is high, indicating the cutoff region.
- As the input voltage increases, the output voltage sharply decreases, marking the transition into the active region where amplification occurs.
- Beyond a certain input voltage, the output voltage levels off, indicating the saturation region.
4. **Key Features and Technical Details:**
- **Cutoff Region:** The output voltage \( v_O \) remains high when the input voltage \( v_I \) is low.
- **Active Region:** The slope of the curve is steep in this region, indicating high gain. This is where the transistor acts as an amplifier. The gain is represented by the slope \( a \) at the operating point \( Q_0 \).
- **Saturation Region:** The output voltage \( v_O \) becomes low and constant as the input voltage \( v_I \) increases further.
- The operating point \( Q_0 \) is marked on the graph, representing the quiescent point where the transistor is biased for optimal amplification.
- Points \( Q_1 \) and \( Q_2 \) indicate the boundaries of the active region.
5. **Annotations and Specific Data Points:**
- The graph includes annotations for the cutoff and saturation regions.
- The active region is emphasized with a bold line, highlighting the range where the transistor provides significant amplification.
- Critical points such as \( Q_0 \), \( Q_1 \), and \( Q_2 \) are marked to indicate key operating conditions.
FIGURE 2.35 (a) The BJT of Fig. 2.32 as a voltage amplifier, and (b) variations about the operating point $Q_{0}$.
A circuit whose gain is not constant but varies with the value of the signal itself is nonlinear. Moreover, the VTC does not go through the origin, but is offset both along the $v_{I}$ and the $v_{O}$ axes. How can we make such a circuit work as a voltage amplifier? The answer relies on two premises, which are illustrated in Fig. 2.35:
- First, we bias the BJT at a suitable quiescent point $Q_{0}=Q_{0}\left(V_{l}, V_{o}\right)$ in the FA region by applying the appropriate $d c$ voltage $V_{I}$. Aptly called the quiescent operating point, $Q_{0}$ in effect establishes a new system of axes for signal variations about this point. $Q_{0}$ should be located sufficiently away from either extreme (EOC and EOS) to allow for an adequate output signal swing in both directions.
- Then, we apply an ac input $v_{i}$, which will cause the instantaneous operating point to move up and down the VTC (between $Q_{1}$ and $Q_{2}$ ), to yield a magnified ac voltage $v_{o}$ at the output.
In our discussion we are relying on the same notation that proved so convenient in the study of diodes, namely, we express the input and output voltages as
$$
\begin{gather*}
v_{I}=V_{I}+v_{i}  \tag{2.43a}\\
v_{O}=V_{O}+v_{o} \tag{2.43b}
\end{gather*}
$$
where:
- $v_{I}$ and $v_{O}$ are referred to as the total signals (lower-case symbols with upper-case subscripts)
- $V_{I}$ and $V_{O}$ are their dc components (upper-case symbols with upper-case subscripts)
- $v_{i}$ and $v_{o}$ are their ac components (lower-case symbols with lower-case subscripts)
As depicted in Fig. $2.35 b$ for the circuit with the parameters of Fig. 2.32, the bias point $Q_{0}$ has been chosen in the middle of the active portion of the VTC so that $V_{o}=2.5 \mathrm{~V}$. The voltage gain there is $a\left(Q_{0}\right)$.
Find the voltage $V_{I}$ needed to bias the BJT of Fig. 2.32 at $V_{O}=2.5 \mathrm{~V}$. What is the voltage gain $a$ there?
#### Solution
By Eq. (2.38),
$$
V_{I}=\frac{5-2.5}{10}+0.026 \ln \frac{5-2.5}{2 \times 10^{-12}}=0.25+0.724=0.974 \mathrm{~V}
$$
indicating that we need 0.724 V to bias the $\mathrm{B}-\mathrm{E}$ junction, and 0.25 V to supply the required base current via $R_{B}$. By Eq. (2.42),
$$
a\left(Q_{0}\right)=-10 \frac{5-2.5}{5.26-2.5} \cong-9 \mathrm{~V} / \mathrm{V}
$$
PSpice simulations with a triangular input $v_{i}$ of progressively increasing magnitude yield the waveforms of Fig. 2.36. We make the following observations:
- In Fig. $2.36 a$ the ac input $v_{i}$ has peak values of $\pm 0.1 \mathrm{~V}$, and the ac output $v_{o}$ is an inverted and magnified version of $v_{i}$, or $v_{o} \cong-9 v_{i}$. The amount of output distortion is imperceptible.
- Doubling $v_{i}$ 's peak values to $\pm 0.2 \mathrm{~V}$ still yields a fairly undistorted output, as seen in Fig. 2.36b. The operating point moves up and down a wider portion of the VTC, which however is still approximately straight.
image_name:(a)
description:The graph in Fig. 2.36(a) is a time-domain waveform plot showing the input and output voltages of a circuit. The x-axis represents time in milliseconds (ms), ranging from 0 to 2 ms, while the y-axis represents voltage in volts (V), ranging from 0 to 5 V.
1. **Type of Graph and Function:**
- The graph is a time-domain waveform plot, illustrating the behavior of voltages over time.
2. **Axes Labels and Units:**
- **X-axis:** Time (t) in milliseconds (ms).
- **Y-axis:** Voltage (V) in volts.
- The graph uses a linear scale for both axes.
3. **Overall Behavior and Trends:**
- The input voltage, denoted as \( v_i \), is a triangular waveform with peak values of approximately \( \pm 0.1 \) V, centered around a bias voltage \( V_I = 0.94 \) V.
- The output voltage, denoted as \( v_o \), is an inverted and amplified version of the input, with a peak amplitude of about 0.9 V (since \( v_o \approx -9v_i \)).
- The output waveform maintains the triangular shape of the input, indicating minimal distortion.
4. **Key Features and Technical Details:**
- The input waveform crosses zero volts twice per cycle, at approximately 0.5 ms and 1.5 ms.
- The output waveform is inverted, with its peaks occurring where the input waveform has valleys and vice versa.
- The output voltage remains within the linear region of the circuit's transfer characteristic, ensuring minimal distortion.
5. **Annotations and Specific Data Points:**
- The graph includes annotations for the input \( v_i \) and output \( v_o \) waveforms.
- The bias voltages \( V_I = 0.94 \) V and \( V_O = 2.5 \) V are indicated on the graph, showing the DC levels around which the AC signals oscillate.
Overall, the graph demonstrates the circuit's ability to invert and amplify the input signal with minimal distortion when the input peak values are \( \pm 0.1 \) V.
image_name:(b)
description:The graph labeled (b) is a time-domain waveform plot displaying the input and output voltages of a circuit over a time interval from 0 to 2 milliseconds (ms).
**Axes Labels and Units:**
- The x-axis represents time in milliseconds (ms), ranging from 0 to 2 ms.
- The y-axis represents voltage in volts (V), ranging from 0 to 5 V.
**Overall Behavior and Trends:**
- The input voltage, \(v_i\), is shown as a triangular waveform with peak values of \(\pm 0.2\) V. This waveform is relatively small and consistent, oscillating symmetrically around the baseline with a period that matches the time axis.
- The output voltage, \(v_o\), is an inverted and magnified version of the input waveform. It exhibits a larger amplitude, indicating a gain factor of approximately -9, as discussed in the context. The waveform is also triangular, maintaining the shape of the input but with inversion.
**Key Features and Technical Details:**
- The output waveform \(v_o\) reaches peaks near the maximum and minimum y-axis values, approximately -1.8 V and 1.8 V, respectively. This indicates a consistent gain and inversion across the waveform.
- The waveform remains undistorted, suggesting the circuit operates within its linear region, effectively amplifying the input signal without distortion.
**Annotations and Specific Data Points:**
- The graph includes annotations for \(v_i\) and \(v_o\), clearly identifying the input and output waveforms.
- The baseline voltages \(V_I\) and \(V_O\) are marked, corresponding to the biasing conditions at 0.94 V and 2.5 V, respectively.
This graph effectively demonstrates the circuit's ability to amplify and invert an input signal with minimal distortion, maintaining linear operation even as the input amplitude is increased to \(\pm 0.2\) V.
image_name:(c)
description:The graph labeled (c) in the provided image is a time-domain waveform plot showing the input and output voltages of a circuit. The x-axis represents time in milliseconds (ms), ranging from 0 to 2 ms. The y-axis represents voltage in volts (V), ranging from 0 to 5 V.
1. **Type of Graph and Function**:
- This is a time-domain waveform graph depicting the behavior of input and output voltages over time.
2. **Axes Labels and Units**:
- The x-axis is labeled "Time t (ms)" and measures time in milliseconds.
- The y-axis is labeled "Waveforms (V)" and measures voltage in volts.
3. **Overall Behavior and Trends**:
- The input voltage $v_{i}$ is a triangular waveform with peak values of approximately ±0.4 V. This waveform is shown as a thin line.
- The output voltage $v_{o}$ is also a waveform but is highly distorted compared to the input. It is represented as a thick line and shows significant deviation from a simple triangular shape, with sections that flatten out, indicating clipping or saturation.
4. **Key Features and Technical Details**:
- The input waveform $v_{i}$ maintains a consistent triangular shape throughout the time period.
- The output waveform $v_{o}$ shows distortion with peaks reaching close to the 5 V mark, indicating that the circuit is operating beyond its linear range, causing the waveform to clip.
- The distortion is due to the operating point spilling over into the cutoff and saturation regions, where the gain drops significantly.
5. **Annotations and Specific Data Points**:
- The graph includes horizontal reference lines at $V_{I} = 0.94 \, V$ and $V_{O} = 2.5 \, V$.
- The input and output waveforms are marked with arrows labeled $v_{i}$ and $v_{o}$ respectively.
Overall, the graph illustrates how increasing the input peak values to ±0.4 V leads to a highly distorted output due to the limitations of the circuit's linear operating range. The output is no longer a simple inverted and magnified version of the input, as seen with lower input levels, but instead exhibits significant distortion due to clipping.
FIGURE 2.36 The responses of the circuit of Fig. 2.39 to a triangular wave $v_{i}$ with peak values of: (a) $\pm 0.1 \mathrm{~V}$, (b) $\pm 0.2 \mathrm{~V}$, and (c) $\pm 0.4 \mathrm{~V}$. The BJT is biased at $V_{I}=0.94 \mathrm{~V}$ and $V_{0}=2.5 \mathrm{~V}$.
- Raising $v_{i}$ 's peak values to $\pm 0.4 \mathrm{~V}$ forces the operating point to spill over into the cutoff and the saturation regions, where gain drops dramatically. The result is the highly distorted output waveform of Fig. 2.36c. Distortion at the top is due to BJT cutoff, and distortion at the bottom to BJT saturation.
We can now better appreciate the reason for biasing the BJT somewhere in the middle of the FA region, sufficiently away from both cutoff and saturation, as well as the reason for keeping the magnitude of $v_{i}$ and, hence, of $v_{o}$, sufficiently small. In fact, the smaller the signals the lesser the amount of output distortion. Viewed in this light, $v_{i}$ and $v_{o}$ are also referred to as small signals. A more rigorous treatment of this subject will be undertaken in the next section.
### The BJT as a Switch/Logic Inverter
When BJT operation alternates between the cutoff and the saturation modes, the device acts as an electronic switch SW. In this capacity, illustrated in Fig. 2.37, the BJT can be used to turn on/off power to some arbitrary load $R_{L}$, such as a light-emitting device, a dc motor, or a heating element. With reference to Fig. 2.37, we make the following observations:
- When $v_{I}$ is low, near 0 V , the BJT is in cutoff, and since it draws no current, it can be regarded as an open switch. This is pictured in Fig. 2.37b.
- When $v_{I}$ is high, say near $V_{C C}$, the BJT is designed to saturate. Consequently, it can be regarded as a closed switch, but in series with a tiny battery $V_{C E(\text { sat })} \cong$ 0.1 V , as pictured in Fig. 2.37c. Consequently, the load $R_{L}$ now receives the full power supplied by $V_{C C}$. To guarantee a reliably closed switch under all possible conditions, especially in view of fluctuations in the value of $\beta_{F}$, we must force the BJT in sufficiently deep saturation. We must thus ensure that $\beta_{\text {sat }}<\beta_{F(\min )}$ with a certain margin of safety.
image_name:(a)
description:
[
name: RB, type: Resistor, value: RB, ports: {N1: VI, N2: b}
name: RL, type: Resistor, value: RL, ports: {N1: VCC, N2: C}
name: Q, type: NPN, ports: {C: C, B: b, E: GND}
name: VI, type: VoltageSource, value: VI, ports: {Np: VI, Nn: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
]
extrainfo:The circuit operates as a BJT logic inverter. When the input voltage VI is low, the switch SW is open, and when VI is high, the switch closes, simulating a closed switch with a small voltage drop (VCE(sat) ≈ 0.1 V). The circuit is designed to drive a load RL with a BJT operating in saturation to ensure reliable switching.
image_name:(b)
description:
[
name: RL, type: Resistor, value: RL, ports: {N1: VCC, N2: C}
name: SW, type: Switch, ports: {N1: C, N2: GND}
]
extrainfo:The circuit diagram (b) shows a BJT used as a switch. When the input voltage VI is low, the switch SW is open, and when VI is high, the switch is closed, allowing current to flow through RL from VCC to GND.
image_name:(c)
description:
[
name: RL, type: Resistor, value: RL, ports: {N1: VCC, N2: c}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: VCE, type: VoltageSource, value: VCE, ports: {Np: VCE, Nn: GND}
name: SW, type: Switch, ports: {N1: c, N2: VCE}
]
extrainfo:The circuit diagram (c) shows a BJT operating as an electronic switch with a voltage source V_CE(sat) of 0.1 V in series with the switch. When v_I is high, the switch is closed, and the load resistor R_L receives the full power from V_CC.
FIGURE 2.37 Operating the BJT as an electronic switch.
image_name:Figure 2.38 (a)
description:
[
name: RB, type: Resistor, value: RB, ports: {N1: A, N2: b}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: Y}
name: Q, type: NPN, ports: {C: Y, B: b, E: GND}
]
extrainfo:The circuit diagram (a) shows a BJT used as a logic inverter. When input A is high, the transistor Q is saturated, pulling the output Y low. When input A is low, the transistor is off, and the output Y is high. The truth table in (b) confirms this behavior, showing the inverter functionality of the circuit.
image_name:Figure 2.38 (b)
description:The image consists of two parts labeled (a) and (b), illustrating the BJT as a logic inverter.
**Part (a): Circuit Diagram**
- The circuit shows a BJT transistor labeled as \( Q \), configured as a switch.
- The input signal \( A \) is connected to the base of the transistor through a resistor \( R_B \).
- The collector of the transistor is connected to a resistor \( R_C \) and then to a positive voltage source \( V_{CC} \).
- The emitter is connected to the ground (GND).
- The output \( Y \) is taken from the collector of the transistor.
- The input \( A \) can be either 'High' or 'Low'.
- The output \( Y \) can be either \( V_{OH} \) (high) or \( V_{OL} \) (low).
**Part (b): Logic Symbol and Truth Table**
- The logic symbol represents an inverter (INV) with input \( A \) and output \( Y \).
- The truth table is presented with three columns:
- Column 1 labeled \( A \) with values 'L' (Low) and 'H' (High).
- Column 2 labeled \( Q \) with values 'CO' (cut-off) and 'Sat' (saturation).
- Column 3 labeled \( Y \) with values 'H' (High) and 'L' (Low).
- When \( A \) is 'L', \( Q \) is in cut-off (CO), and \( Y \) is 'H'.
- When \( A \) is 'H', \( Q \) is in saturation (Sat), and \( Y \) is 'L'.
This illustrates how the BJT operates as an inverter, switching the output between high and low states based on the input signal's level.
FIGURE 2.38 The BJT as a logic inverter. (a) circuit, (b) logic symbol and truth table.
A BJT with $\beta_{F}$ specified to be anywhere within the range $50 \leq \beta_{F} \leq 200$ is to be used as a switch for a $100-\mathrm{mA}$ load. If $v_{I}$ is a logic signal with logic levels of 0 V and 5 V , find a suitable value for $R_{B}$.
#### Solution
To guarantee a saturated BJT under all possible conditions, including the worstcase scenario of $\beta_{F}=50$, we need $I_{B}>100 / 50=2 \mathrm{~mA}$. Impose $I_{B}=3 \mathrm{~mA}$ to be on the safe side. Then, $R_{B}=(5-0.8) / 3=1.4 \mathrm{k} \Omega$.
A popular application of the BJT switch is to provide logic inversion in computer circuitry. As implied by its name, a logic inverter outputs a high voltage level (H) in response to a low input level (L), and outputs a low level in response to a high input level. For the BJT inverter of Fig. 2.38a, these levels are, respectively,
$$
\begin{gather*}
V_{O H}=V_{C C}  \tag{2.44a}\\
V_{O L}=V_{C E(\mathrm{sat})} \tag{2.44b}
\end{gather*}
$$
Typically $V_{O H}=5 \mathrm{~V}$, and $V_{O L}=0.1 \mathrm{~V}$. Figure $2.38 b$ shows the logic symbol for the inverter, along with the truth table listing the BJT's operating mode as well as the logic output for the two possible logic input combinations.
## 2.6 SMALL-SIGNAL OPERATION OF THE BJT
We now wish to pursue a more systematic investigation of the small-signal operation introduced in the previous section. Let us start with the circuit of Fig. 2.39a, where we are using the dc source $V_{B E}$ to bias the BJT at some quiescent point $Q_{0}=Q_{0}\left(I_{C}, V_{B E}\right)$ up the exponential curve (see Fig. 2.40a), and the source $V_{C C}$, along
image_name:(a)
description:
[
name: Q, type: NPN, ports: {C: VCE, B: VBE, E: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: VCE}
name: VBE, type: VoltageSource, value: VBE, ports: {Np: VBE, Nn: GND}
]
extrainfo:The circuit in diagram (a) is a large-signal or DC version of a BJT amplifier. It biases the BJT using VBE and VCC to establish a quiescent point Q0 in the active region. RC is used as a load resistor.
image_name:(b)
description:
[
name: Q, type: NPN, ports: {C: VCE, B: VBE, E: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: VCE}
name: VBE, type: VoltageSource, value: VBE, ports: {Np: VBE1, Nn: GND}
name: vbe, type: VoltageSource, value: vbe, ports: {Np: VBE, Nn: VBE1}
]
extrainfo:The circuit diagram (b) represents a BJT biased with a DC voltage source VBE and a collector resistor RC. The transistor Q is in the active region, and VCC provides the collector voltage.
image_name:(c)
description:
[
name: Q, type: NPN, ports: {C: VCE, B: vbe, E: GND}
name: RC, type: Resistor, value: RC, ports: {N1: GND, N2: VCE}
name: VBE, type: VoltageSource, value: vbe, ports: {Np: vbe, Nn: GND}
]
extrainfo:The circuit diagram (c) represents a small-signal model of a BJT amplifier. It includes an NPN transistor biased with a small-signal voltage source vbe. The collector is connected to a resistor RC and a DC supply voltage VCC. The emitter is grounded.
FIGURE 2.39 Systematic analysis of the BJT as a small-signal amplifier. The actual circuit is shown in (b), while (a) shows its large-signal or dc version, and (c) shows its small-signal or ac version.
with the resistance $R_{C}$, to bias the BJT at the corresponding operating point $Q_{0}=$ $Q_{0}\left(I_{C}, V_{C E}\right)$ in the active region (see Fig. 2.40b). Applying Eq. (2.21) at $Q_{0}$ gives
$$
\begin{equation*}
I_{C}=I_{s} e^{V_{B E} / V_{T}}\left(1+\frac{V_{C E}}{V_{A}}\right) \tag{2.45}
\end{equation*}
$$
Along with the $i_{C}-v_{C E}$ curves of the BJT, Fig. $2.40 b$ also shows the curve of the circuit external to the collector, a curve known as the load line,
$$
\begin{equation*}
i_{C}=\frac{V_{C C}-v_{C E}}{R_{C}} \tag{2.46}
\end{equation*}
$$
image_name:(a)
description:The graph labeled (a) is a plot of the collector current \(i_C\) against the base-emitter voltage \(v_{BE}\) for a BJT (Bipolar Junction Transistor). This is an exponential graph representing the relationship between the collector current and the base-emitter voltage, reflecting the exponential increase in current with voltage characteristic of a BJT in the active region.
Axes Labels and Units:
- **Horizontal Axis:** Base-emitter voltage \(v_{BE}\). The axis is marked from 0 to \(V_{BE} + v_{be}\), indicating the variation in base-emitter voltage including an AC component.
- **Vertical Axis:** Collector current \(i_C\). The axis is marked from 0 to \(I_C + i_c\), indicating the variation in collector current including an AC component.
Overall Behavior and Trends:
- The graph shows an exponential curve starting from the origin (0,0) and rising steeply as \(v_{BE}\) increases. This reflects the exponential relationship between \(i_C\) and \(v_{BE}\) as per the diode equation for BJTs.
- The curve passes through two key points: \(Q_0\) and \(Q_1\). \(Q_0\) is the quiescent point indicating the DC operating condition, while \(Q_1\) represents a point on the curve when an AC signal is superimposed.
Key Features and Technical Details:
- **Quiescent Point \(Q_0\):** This is where the BJT operates under DC conditions without any AC signal. It is marked on the graph at a specific \(v_{BE}\) and corresponding \(i_C\).
- **Point \(Q_1\):** Indicates the operating point when an AC signal is applied, showing the increase in both \(v_{BE}\) and \(i_C\).
- **Transconductance \(g_m\):** The graph shows a vertical line from \(Q_0\) to \(Q_1\), labeled \(g_m\), representing the change in collector current per unit change in base-emitter voltage.
Annotations and Specific Data Points:
- The graph is annotated with horizontal lines indicating the levels \(I_C\) and \(I_C + i_c\), showing the DC and AC components of the collector current.
- Vertical markers indicate \(V_{BE}\) and \(V_{BE} + v_{be}\), showing the DC and AC components of the base-emitter voltage.
This graph effectively illustrates the exponential increase in collector current with increasing base-emitter voltage, a fundamental characteristic of BJT operation in the active region.
image_name:(b)
description:The graph labeled (b) is a plot illustrating the behavior of a Bipolar Junction Transistor (BJT) in the active region, specifically showing the relationship between the collector current \(i_C\) and the collector-emitter voltage \(v_{CE}\). This is a graphical representation of the BJT's output characteristics.
1. **Type of Graph and Function:**
- The graph is an output characteristic curve of a BJT, featuring both the transistor's characteristic curves and the load line.
2. **Axes Labels and Units:**
- The x-axis represents the collector-emitter voltage \(v_{CE}\) and is measured in volts.
- The y-axis represents the collector current \(i_C\) and is measured in amperes.
- Both axes use a linear scale.
3. **Overall Behavior and Trends:**
- The graph shows multiple curves representing different base-emitter voltages \(V_{BE}\). Each curve has a distinct slope, indicating the transistor's operation at different levels of base current.
- The load line is a straight line with a negative slope, representing the external circuit constraints on the transistor.
- The intersection of the load line with the BJT curves determines the operating point or quiescent point \(Q_0\).
4. **Key Features and Technical Details:**
- The load line is defined by the equation \(i_C = \frac{V_{CC} - v_{CE}}{R_C}\), where \(V_{CC}\) is the supply voltage and \(R_C\) is the collector resistor.
- The quiescent point \(Q_0\) is shown where the load line intersects the BJT curve for a specific \(V_{BE}\).
- Another point \(Q_1\) is shown, indicating a different operating condition possibly due to an AC signal superimposed on the DC bias.
- The slope of the load line is related to the resistance \(R_C\), and the point \(1/r_o\) indicates the output conductance of the transistor.
5. **Annotations and Specific Data Points:**
- \(Q_0\) is marked as the quiescent point, and \(Q_1\) as another operating point.
- The load line intersects multiple BJT curves, showing potential operating points for different base currents.
- The graph provides a visual representation of how changes in \(v_{CE}\) and \(V_{BE}\) affect the collector current \(i_C\).
FIGURE 2.40 Graphical illustrations of the BJT amplifier of Fig. 2.39.
The quiescent point $Q_{0}=Q_{0}\left(I_{C}, V_{C E}\right)$ lies right where the BJT curve corresponding to the given value of $V_{B E}$ intersects the load line.
If we now turn on the ac source $v_{b e}$ as in Fig. 2.39b, the operating point will move up and down the exponential curve of Fig. 2.40a as well as up and down the load line of Fig. 2.40b. In Fig. 2.40 we have captured a positive alternation of $v_{b e}$, during which the instantaneous operating point in Fig. 2.40a is $Q_{1}=Q_{1}\left(I_{C}+i_{c}, V_{B E}+v_{b e}\right)$, and in Fig. 2.40b is $Q_{1}=Q_{1}\left(I_{C}+i_{c}, V_{C E}+v_{c e}\right)$. We wish to find a relationship between the ac current $i_{c}$ and the ac voltages $v_{b e}$ and $v_{c e}$. Applying Eq. (2.21) at the new operating point $Q_{1}$,
$$
I_{C}+i_{c}=I_{s} e^{\left(V_{B E}+v_{b E}\right) / V_{T}}\left(1+\frac{V_{C E}+v_{c e}}{V_{A}}\right)=I_{s} e^{V_{B E} / V_{T}}\left(1+\frac{V_{C E}}{V_{A}}+\frac{v_{c e}}{V_{A}}\right) e^{v_{s e} / V_{T}}
$$
For $V_{C E} / V_{A} \ll 1$ we approximate $I_{s} \exp \left(V_{B E} / V_{T}\right) \cong I_{C}$ and rewrite as
$$
I_{C}+i_{c} \cong I_{C}\left(1+\frac{v_{c e}}{V_{A} / I_{C}}\right) e^{v_{b c} / V_{T}}
$$
Performing the series expansion of the exponential term gives
$$
\begin{align*}
I_{C}+i_{c} & \cong I_{C}\left(1+\frac{v_{c e}}{V_{A} / I_{C}}\right)\left[1+\frac{v_{b e}}{V_{T}}+\frac{1}{2!}\left(\frac{v_{b e}}{V_{T}}\right)^{2}+\frac{1}{3!}\left(\frac{v_{b e}}{V_{T}}\right)^{3}+\cdots\right] \\
& \cong I_{C}+\frac{I_{C}}{V_{T}} v_{b e}+\frac{v_{c e}}{V_{A} / I_{C}}+\cdots \tag{2.47}
\end{align*}
$$
As long as we can ignore higher-order terms involving ac products and powers, Eq. (2.47) allows us to write
$$
\begin{equation*}
i_{c}=g_{m} v_{b e}+\frac{v_{c e}}{r_{o}} \tag{2.48}
\end{equation*}
$$
where
$$
\begin{equation*}
g_{m}=\frac{I_{C}}{V_{T}} \tag{2.49}
\end{equation*}
$$
is the transconductance of the BJT, and
$$
\begin{equation*}
r_{o}=\frac{V_{A}}{I_{C}} \tag{2.50}
\end{equation*}
$$
is the collector's output resistance. As shown in Fig. 2.40, $g_{m}$ and $1 / r_{o}$ represent, respectively, the slopes of the $i_{C}-v_{B E}$ and the slope of the $i_{C}-v_{C E}$ curve at $Q_{0}$. Both $g_{m}$ and $r_{o}$ depend on the operating current $I_{C}$. Moreover, the fact that $V_{A} \gg V_{T}$ indicates a much weaker dependence of $i_{c}$ on $v_{c e}$ than on $v_{b e}$.
We wish to assess under what conditions we can ignore higher-order powers and products in Eq. (2.47). By inspection, we can stop at the second term within
brackets in Eq. (2.47) provided we keep $v_{b e}$ small enough to satisfy the condition $1 / 2\left(v_{b e} / V_{T}\right)^{2} \ll\left|v_{b e}\right| / V_{T}$, that is,
$$
\begin{equation*}
\left|v_{b e}\right| \ll 2 V_{T}(\cong 52 \mathrm{mV}) \tag{2.51}
\end{equation*}
$$
For obvious reasons, Eq. (2.48) is referred to as the small signal approximation, and Eq. (2.51) quantifies the validity of such an approximation. The error $\varepsilon$ incurred in the small-signal approximation is
$$
\begin{equation*}
\varepsilon \cong \frac{v_{b e}}{2 V_{T}} \cong \frac{v_{b e}}{52 \mathrm{mV}} \tag{2.52}
\end{equation*}
$$
or about $2 \%$ for every mV of $v_{b e}$. Thus, if we wish to keep $\varepsilon$ below $10 \%$ (an acceptable error in most practical situations), then we need to ensure that
$$
\begin{equation*}
\left|v_{b e}\right| \leq 5 \mathrm{mV} \tag{2.53}
\end{equation*}
$$
This shall be our working condition as we move along.
EXAMPLE 2.12 (a) With reference to Fig. $2.40 a$, suppose $v_{b e}$ is an ac signal with peak values of $\pm 5 \mathrm{mV}$. Assuming $V_{A}=\infty$ for simplicity, use the small-signal approximation to estimate the peak values of $i_{c}$ at $I_{C}=1 \mathrm{~mA}$.
(b) Find the exact peak values of $i_{c}$, compare with the approximated values of part (a) and comment.
#### Solution
(a) By Eq. (2.49), $g_{m}=1 / 26 \mathrm{~A} / \mathrm{V}$. The small-signal approximation of Eq. (2.48) predicts, for $i_{c}$, peak values of $(1 / 26)\left( \pm 5 \times 10^{-3}\right) \cong \pm 192 \mu \mathrm{~A}$.
(b) The exact peak values of $i_{c}$ are
$$
i_{c}=I_{C}\left(1-e^{v_{b c} / V_{T}}\right)=(1.0 \mathrm{~mA}) \times\left(e^{ \pm 5 / 26}-1\right)
$$
or $+212 \mu \mathrm{~A}$ and $-175 \mu \mathrm{~A}$, respectively. Because of the curvature of the $i_{C^{-}} v_{B E}$ characteristic, the small-signal approximation underestimates the positive current peak by $(212-192) / 212 \cong 9.4 \%$, and overestimates the negative peak by $(192-175) / 175 \cong 9.7 \%$. These errors are consistent with Eq. (2.52).
Just like we use the $d c$ equivalent of Fig. $2.39 a$ to investigate the biasing conditions of our BJT, we use the $a c$ equivalent of Fig. $2.39 c$ to investigate its operation as an amplifier. Indeed, the latter gives, by KVL, Ohm's law, and Eq. (2.48),
$$
v_{c e}=0-R_{C} i_{c}=-R_{C}\left(g_{m} v_{b e}+\frac{v_{c e}}{r_{o}}\right)
$$
Collecting, and solving for $v_{c e}$, we can write
$$
v_{c e}=-g_{m}\left(R_{C} / / r_{o}\right) v_{b e}
$$
indicating that our circuit magnifies $v_{b e}$ by the gain $-g_{m}\left(R_{C} / / r_{o}\right)$.
Assuming $R_{C}=10 \mathrm{k} \Omega$ and $V_{A}=100 \mathrm{~V}$ in Fig. 2.39b, find the small-signal gain at $I_{C}=1 \mathrm{~mA}$.
#### Solution
We have $g_{m}=1 / 26 \mathrm{~A} / \mathrm{V}, r_{o}=100 / 1=100 \mathrm{k} \Omega$, and $-g m\left(R_{C} / / r_{o}\right)=-(1 / 26) \times$ $(10 / / 100) 10^{3} \cong-350 \mathrm{~V} / \mathrm{V}$.
### The Small-Signal BJT Model
Figure 2.41 shows the small-signal model for the BJT. The function of this model, also referred to as incremental model or simply as ac model, is to provide a circuit representation of the dependence of $i_{c}$ upon $v_{b e}$ and $v_{c e}$ as expressed by Eq. (2.48). As we know, the dependence on $v_{c e}$ is much weaker than that on $v_{b e}$, so the term $v_{c e} / r_{o}$ is sometimes ignored to speed up calculations. This is tantamount to assuming $r_{o}=\infty$ in the ac model. The model includes also the resistance
$$
\begin{equation*}
r_{\pi}=\frac{v_{b e}}{i_{b}} \tag{2.54}
\end{equation*}
$$
to account for the fact that the BJT responds to $v_{b e}$ not only with the collector current $i_{c}$ but also with the base current $i_{b}$. The ratio of the two is called the common-emitter ac current gain
$$
\begin{equation*}
\beta_{0}=\frac{i_{c}}{i_{b}} \tag{2.55}
\end{equation*}
$$
and it is customary to assume $\beta_{0} \cong \beta_{F}$, even though there are subtle differences between the two betas. ${ }^{4}$ By the above equations we have $r_{\pi}=v_{b e} / i_{b}=\left(i_{c} / g_{m}\right) / i_{b}=$ $\left(i_{c} / i_{b}\right) / g_{m}$, or
$$
\begin{equation*}
r_{\pi}=\frac{\beta_{0}}{g_{m}}=\beta_{0} \frac{V_{T}}{I_{C}} \tag{2.56}
\end{equation*}
$$
image_name:FIGURE 2.41 Small-signal BJT model
description:
[
name: Q, type: NPN, ports: {C: C, B: B, E: E}
name: rπ, type: Resistor, value: rπ, ports: {N1: B, N2: E}
name: βib, type: VoltageControlledCurrentSource, value: βib, ports: {Np: C, Nn: E}
name: ro, type: Resistor, value: ro, ports: {N1: C, N2: E}
]
extrainfo:The diagram represents a small-signal model of a BJT (Bipolar Junction Transistor) in common-emitter configuration. It includes the base-emitter resistance (rπ), the output resistance (ro), and a current-controlled current source modeling the transistor's current gain (βib).
FIGURE 2.41 Small-signal BJT model. This model applies both to the npn and the pnp BJT.
### TABLE 2.1 Small-signal parameter summary.
| Definition | Calculation |
| :---: | :--- |
| $g_{m}=\left.\frac{\partial i_{C}}{\partial v_{B E}}\right\|_{V_{C E}}$ | $g_{m}=\frac{I_{C}}{V_{T}}$ |
| $\frac{1}{r_{\pi}}=\left.\frac{\partial i_{B}}{\partial v_{B E}}\right\|_{V_{C E}}$ | $r_{\pi}=\frac{\beta_{0}}{g_{m}}=\beta_{0} \frac{V_{T}}{I_{C}}$ |
| $\frac{1}{r_{o}}=\left.\frac{\partial i_{C}}{\partial v_{C E}}\right\|_{V_{B E}}$ | $r_{o}=\frac{V_{A}}{I_{C}}$ |
indicating that $r_{\pi}$ itself depends on the bias current $I_{C}$, just like $g_{m}$ and $r_{o}$ do. To develop a feel for the various parameters, consider a BJT with $\beta_{0}=100$ and $V_{A}=100 \mathrm{~V}$ that is operating at $I_{C}=1 \mathrm{~mA}$. Then,
$$
1 / g_{m}=26 \Omega \text { (small) } \quad r_{\pi}=2.6 \mathrm{k} \Omega \text { (medium) } \quad r_{o}=100 \mathrm{k} \Omega \text { (large) }
$$
It pays to have an idea of the orders of magnitude of these parameters when dealing with a BJT amplifier. Their definitions (for the case of the npn BJT) as well as their calculations are summarized in Table 2.1.
As we know, in forward-active operation a BJT can be regarded either as a voltage-controlled (VC) or as a current-controlled (CC) device. This versatility carries over also to the small-signal domain, where we can express the value of the dependent source either as $g_{m} v_{b e}$ (VCCS) or as $\beta_{0} i_{b}$ (CCCS). This is shown explicitly in the ac model of Fig. 2.41. When we use this second alternative, Eq. (2.48) becomes
$$
\begin{equation*}
i_{c}=\beta_{0} i_{b}+\frac{v_{c e}}{r_{o}} \tag{2.57}
\end{equation*}
$$
As we proceed, we have the option of using whichever of the two expressions makes our analysis simpler.
We wish to point out that the model of Fig. 2.41 applies both to the npn BJT and the pnp BJT, with no change in voltage polarities or current directions. Indeed, consider the effect of increasing $v_{B E}$ by $v_{b e}$ in both devices. In the npn BJT $i_{C}$ will also increase, but in the pnp BJT $i_{C}$ will decrease. Consequently, $i_{c}$ will have the same direction as $i_{C}$ in the $n p n$ case ( $i_{c}$ into the collector terminal), but the opposite direction as $i_{C}$ in the pnp case. Since in the pnp case $i_{C}$ flows out of the collector terminal, $i_{c}$ will be into the collector terminal, just as in the npn case. We must stress that the small-signal model should not be confused with the large signal models. Large-signal models are used for $d c$ analysis, examples of which we have already seen. The small-signal model is used for ac analysis, to be demonstrated next.
### The BJT as a Resistance-Transformation Device
Before embarking on a systematic investigation of the amplifying capabilities of the BJT, we wish to explore some intriguing resistance-transformation properties that will prove quite useful as we proceed. Specifically, we wish to find the small-signal
image_name:Figure 2.42
description:
[
name: RB, type: Resistor, value: RB, ports: {N1: GND, N2: B}
name: Re, type: Resistor, value: Re, ports: {N1: E, N2: GND}
name: RE, type: Resistor, value: RE, ports: {N1: E, N2: GND}
name: Q, type: NPN, ports: {C: GND, B: B, E: E}
]
extrainfo:The circuit is a small-signal model of a BJT with resistors connected to the base, collector, and emitter. The resistances seen looking into the BJT's terminals are analyzed for exact and approximate values.
image_name:Exact and Approximate
description:The image contains a schematic of a BJT (Bipolar Junction Transistor) circuit with terminals labeled B (base), E (emitter), and C (collector). The circuit includes resistances labeled \( R_B \), \( R_E \), \( R_b \), \( R_e \), and \( R_c \). The BJT is represented with a symbol for a transistor, and the connections are grounded at certain points.
To the right of the schematic, there are two tables labeled 'Exact' and 'Approximate,' which provide formulas for calculating the small-signal resistances \( R_b \), \( R_e \), and \( R_c \) at the BJT terminals.
**Exact Formulas:**
- \( R_b = r_\pi + (\beta_0 + 1)(R_E || r_o) \)
- \( R_e = \left( \frac{R_B + r_\pi}{\beta_0 + 1} \right) // r_o \)
- \( R_c = r_o \left[ 1 + \frac{g_m r_\pi R_E}{R_B + r_\pi + R_E} \right] + (R_B + r_\pi) // R_E \)
**Approximate Formulas:**
- \( R_b \approx r_\pi + (\beta_0 + 1)R_E \)
- \( R_e \approx \frac{R_B}{\beta_0 + 1} + r_e \)
- \( R_c \approx r_o [1 + g_m (r_\pi // R_E)] \)
These formulas help in analyzing the small-signal resistances seen at the BJT's terminals when looking into the base, emitter, and collector.
FIGURE 2.42 The small-signal resistances seen looking into the BJT's terminals.
resistances seen looking into the base, the emitter, and the collector terminals of the circuit of Fig. 2.42. We denote these resistances as $R_{b}, R_{e}$, and $R_{c}$ (lower-case subscripts). Conversely, we denote the resistances external to the BJT as $R_{B}$ and $R_{E}$ (upper-case subscripts.) To find the small-signal resistance $R_{x}$ seen looking into terminal $X(X=B, E, C)$, proceed as follows:
- Replace the BJT with its small-signal model
- Apply a test voltage $v_{x}$ to the terminal $X$ under consideration
- Determine the resulting current $i_{x}$ into $X$
- Find the resistance seen looking into that terminal as $R_{x}=v_{x} / i_{x}$
This procedure will give us an opportunity to put the small-signal BJT model to use. At times we shall find it more convenient to express the dependent source as $g_{m} v_{b e}$, at others as $\beta_{0} i_{b}$.
- The Small-Signal Resistance $\boldsymbol{R}_{b}$ Seen Looking into the Base. The circuit to find this resistance is shown in Fig. 2.43a (note that since we are looking right
image_name:(a)
description:
[
name: vb, type: VoltageSource, value: vb, ports: {Np: B, Nn: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: B, N2: ve}
name: β0ib, type: VoltageControlledCurrentSource, value: β0ib, ports: {Np: ve, Nn: ve}
name: ro, type: Resistor, value: ro, ports: {N1: GND, N2: ve}
name: RE, type: Resistor, value: RE, ports: {N1: ve, N2: GND}
]
extrainfo:The circuit diagram (a) is used to find the small-signal resistance Rb seen looking into the base of the BJT. The dependent current source is expressed as β0ib, and the small-signal model ignores ro for simplification.
image_name:(b)
description:
[
name: RB, type: Resistor, value: RB, ports: {N1: GND, N2: "B"}
name: rπ, type: Resistor, value: rπ, ports: {N1: "B", N2: E}
name: β0ib, type: VoltageControlledCurrentSource, ports: {Np: GND, Nn: E}
name: ro, type: Resistor, value: ro, ports: {N1: E, N2: GND}
name: ve, type: VoltageSource, value: ve, ports: {Np: E, Nn: GND}
]
extrainfo:The circuit is used to find the small-signal resistance seen looking into the emitter (R_e). It includes a voltage source ve, a resistor ro, and a voltage-controlled current source β0ib connected to nodes E and ve.
FIGURE 2.43 Test circuits to find the small-signal resistance (a) $R_{b}$ seen looking into the base, and (b) $R_{e}$ seen looking into the emitter. In both cases we ignore $r_{0}$ to simplify our initial analysis.
into the base terminal, $R_{B}$ does not intervene in this test.) To simplify our analysis, let us momentarily ignore $r_{o}$. By Ohm's law and KCL,
$$
i_{b}=\frac{v_{b}-v_{e}}{r_{\pi}}=\frac{v_{b}-R_{E}\left(\beta_{0}+1\right) i_{b}}{r_{\pi}}
$$
Collecting and solving for the ratio $R_{b}=v_{b} / i_{b}$ gives
$$
\begin{equation*}
R_{b}=r_{\pi}+\left(\beta_{0}+1\right) R_{E} \tag{2.58a}
\end{equation*}
$$
Interestingly, when seen looking through the base terminal, $R_{E}$ appears $\left(\beta_{0}+1\right)$ times as large. We also say that the emitter resistance, when reflected to the base, gets multiplied by $\left(\beta_{0}+1\right)$. This is not surprising as the base current is $\left(\beta_{0}+1\right)$ times as small as that flowing through $R_{E}$. It pays to think of the combination made up of $R_{E}$ and the dependent source $\beta_{0} i_{b}$ as a single resistance of value $\left(\beta_{0}+1\right) R_{E}$.
In the above analysis we have deliberately ignored $r_{o}$, but we can readily take it into account by noting that it is in parallel with $R_{E}$ ( $r_{o}$ shares the same node pair as $R_{E}$, namely, $v_{e}$ and ac ground). We thus modify Eq. (2.58a) by replacing $R_{E}$ with $R_{E} / / r_{o}$ and write
$$
\begin{equation*}
R_{b}=r_{\pi}+\left(\beta_{0}+1\right)\left(R_{E} / / r_{\mathrm{o}}\right) \tag{2.58b}
\end{equation*}
$$
(The reader should be observant of simple tricks, such as the present one, to simplify hand analysis.)
- The Small-Signal Resistance $\boldsymbol{R}_{e}$ Seen Looking into the Emitter. The circuit to find this resistance is shown in Fig. $2.43 b$ (note that since we are looking right into the emitter terminal, $R_{E}$ does not intervene in this test.) Again, to simplify our analysis, we momentarily ignore $r_{o}$. Summing currents into the emitter node, we get
$$
i_{b}+\beta_{0} i_{b}+i_{e}=0
$$
Also, by Ohm's law,
$$
i_{b}=\frac{0-v_{e}}{R_{B}+r_{\pi}}
$$
Eliminating $i_{b}$, collecting and solving for the ratio $R_{e}=v_{e} / i_{e}$ gives
$$
\begin{equation*}
R_{e}=\frac{R_{B}+r_{\pi}}{\beta_{0}+1}=\frac{R_{B}}{\beta_{0}+1}+r_{e} \tag{2.59a}
\end{equation*}
$$
where $r_{e}$ is the small-signal resistance seen looking into the emitter in the limit $R_{B} \rightarrow 0$. This resistance is $r_{e}=r_{\pi} /\left(\beta_{0}+1\right)=\left(\beta_{0} / g_{m}\right) /\left(\beta_{0}+1\right)$. Defining the common-base ac current gain as
$$
\begin{equation*}
\alpha_{0}=\frac{\beta_{0}}{\beta_{0}+1} \tag{2.60}
\end{equation*}
$$
we get
$$
\begin{equation*}
r_{e}=\frac{\alpha_{0}}{g_{m}} \cong \frac{1}{g_{m}} \tag{2.61}
\end{equation*}
$$
In general, $r_{e}$ is very small compared to $r_{\pi}$ and $r_{o}$ : for instance at $I_{C}=1 \mathrm{~mA}$ we have $r_{e} \cong 1 / g_{m}=(26 \mathrm{mV}) /(1 \mathrm{~mA})=26 \Omega$. Equation (2.59a) indicates that the presence of the BJT makes $R_{B}$ appear $\left(\beta_{0}+1\right)$ times as small when seen looking through the emitter terminal. We also say that the base resistance $R_{B}$, reflected to the emitter, gets divided by $\left(\beta_{0}+1\right)$. This stems from the fact that the emitter current is $\left(\beta_{0}+1\right)$ times as large as that through $R_{B}$. Clearly, the effect of the BJT upon $R_{B}$ is inverse of that upon $R_{E}$.
In the above analysis we have deliberately ignored $r_{o}$, but we can readily take it into account by noting that it is in parallel with the test source. We thus modify Eq. (2.59a) as
$$
\begin{equation*}
R_{e}=\left(\frac{r_{\pi}+R_{B}}{\beta_{0}+1}\right) / / r_{o} \tag{2.59b}
\end{equation*}
$$
Let the BJT of Fig. 2.42 have $\beta_{0}=100, g_{m}=1 / 26 \mathrm{~A} / \mathrm{V}, r_{\pi}=2.6 \mathrm{k} \Omega$, and $r_{o}=$ $100 \mathrm{k} \Omega$. If $R_{B}=10 \mathrm{k} \Omega$ and $R_{E}=1.0 \mathrm{k} \Omega$, estimate $R_{b}$ and $R_{e}$.
#### Solution
Applying the approximate expressions of Eqs. (2.58a) and (2.59a) we get
$$
\begin{aligned}
& R_{b} \cong 2.6+101 \times 1.0=103.6 \mathrm{k} \Omega(\text { large }) \\
& R_{e} \cong \frac{10,000}{101}+26=125 \Omega(\mathrm{small})
\end{aligned}
$$
Using instead the exact Eqs. (2.58b) and (2.59b) we get $R_{b}=102.6 \mathrm{k} \Omega$ and $R_{e}=124.6 \Omega$. The difference is so small that ignoring $r_{o}$ is quite acceptable, at least in this example.
- The Small-Signal Resistance $\boldsymbol{R}_{c}$ Seen Looking into the Collector. The circuit to find this resistance is shown in Fig. 2.44, with $r_{o}$ now deliberately included. This time we are using the alternative form $g_{m} v_{b e}$ for the dependent source. By KCL and Ohm's law,
$$
i_{c}=g_{m} v_{b e}+\frac{v_{c}-v_{e}}{r_{o}}
$$
By the voltage divider formula,
$$
v_{b e}=-\frac{r_{\pi}}{R_{B}+r_{\pi}} v_{e}
$$
FIGURE 2.44 Test circuit to find the small-signal resistance $R_{c}$ seen looking into the collector.
image_name:Figure 2.44
description:
[
name: RB, type: Resistor, value: RB, ports: {N1: "b", N2: GND}
name: rπ, type: Resistor, value: rπ, ports: {N1: "b", N2: ve}
name: RE, type: Resistor, value: RE, ports: {N1: ve, N2: GND}
name: ro, type: Resistor, value: ro, ports: {N1: c, N2: ve}
name: gmVbe, type: VoltageControlledCurrentSource, ports: {Np: c, Nn: ve}
name: vc, type: VoltageSource, value: vc, ports: {Np: c, Nn: GND}
]
extrainfo:The circuit is used to determine the small-signal resistance Rc seen looking into the collector. It includes resistors RB, rπ, RE, ro, a voltage-controlled current source gmVbe, and a voltage source vc. The circuit uses Kirchhoff's Current Law (KCL) and Ohm's Law to derive Rc.
The test current $i_{c}$ splits between $r_{o}$ and the dependent source and then re-converges at node $v_{e}$, so we apply Ohm's law to write
$$
v_{e}=\left[\left(R_{B}+r_{\pi}\right) / / R_{E}\right] \times i_{c}
$$
Eliminating $v_{b e}$ and $v_{e}$, collecting, and solving for the ratio $R_{c}=v_{c} / i_{c}$ gives, after some algebra,
$$
\begin{equation*}
R_{c}=r_{o}\left[1+\frac{g_{m}\left(r_{\pi} / / R_{E}\right)}{1+R_{B} /\left(r_{\pi}+R_{E}\right)}\right]+\left[\left(R_{B}+r_{\pi}\right) / / R_{E}\right] \tag{2.62a}
\end{equation*}
$$
In most cases of practical interest the last term is negligible compared to the rest, so it will be ignored. Of particular interest is the limiting case $R_{B} \ll R_{E}+r_{\pi}$, for then Eq. (2.62a) simplifies to
$$
\begin{equation*}
R_{c} \cong r_{o}\left[1+g_{m}\left(r_{\pi} / / R_{E}\right)\right] \tag{2.62b}
\end{equation*}
$$
Two additional sub-cases are of great interest. One is $R_{E} \ll r_{\pi}$, for then Eq. (2.62b) reduces to
$$
\begin{equation*}
R_{c} \cong r_{o}\left(1+g_{m} R_{E}\right) \tag{2.62c}
\end{equation*}
$$
The other case is $R_{E} \gg r_{\pi}$, for then Eq. (2.61a) reduces to $R_{c} \cong\left(1+g_{m} r_{\pi}\right)$, or
$$
\begin{equation*}
R_{c} \cong r_{o}\left(1+\beta_{0}\right) \tag{2.62d}
\end{equation*}
$$
Regardless, we note that the presence of $R_{E}$ raises the resistance seen looking into the collector. To justify this physically, consider first the case $R_{E}=0$, which results in $v_{e}=0$ in Fig. 2.44. In this case we have $v_{b e}=0$, indicating that the dependent source in Fig. 2.44 is off, thus giving $i_{c}=v_{c} / r_{o}$, or $R_{c}=v_{c} / i_{c}=r_{o}$. Now consider the case $R_{E} \neq 0$, which results in $v_{e}>0$ because of the current coming from the test source via $r_{o}$. We now have $v_{b e}<0$, indicating that the dependent source is on and its direction is reversed, so that it pumps current into node $C$. But, this reduces the current $i_{c}$ required of the test source, thus raising the ratio $v_{c} / i_{c}$. The fact that the test-source current is met by a counter-action that tends to reduce it indicates that $R_{E}$ provides a negative-feedback action. In Chapter 7 we shall encounter alternative forms of negative feedback for the purpose of raising $R_{c}$.
(a) Find $R_{c}$ for the BJT of Example 2.14.
EXAMPLE 2.15
(b) Repeat if $R_{E}$ is raised from $1.0 \mathrm{k} \Omega$ to $100 \mathrm{k} \Omega$. Comment on your findings.
#### Solution
(a) Applying Eq. (2.62a) we get
$$
\begin{aligned}
R_{c} & =100\left[1+\frac{(2.6 / / 1.0) / 0.026}{1+10 /(2.6+1)}\right]+(10+2.6) / / 1=835+0.93 \\
& =836 \mathrm{k} \Omega \text { (quite large) }
\end{aligned}
$$
(b) By similar calculation we now find $R_{c} \cong 9 \mathrm{M} \Omega$ (huge). Clearly, the larger $R_{E}$, the higher $R_{c}$. In the limit $R_{E} \rightarrow \infty$, Eq. $(2.62 d)$ predicts $R_{c} \cong 101 r_{o} \cong 10 \mathrm{M} \Omega$, a truly huge value.
Equations (2.58) through (2.62) reveal an intriguing BJT feature, namely, the ability to alter the values of resistances seen looking into one of its terminals. This is not surprising, as the dependent source across the C -E port, in turn controlled by the B-E port, establishes interdependence among the three BJT terminals. The expressions for the three resistances are tabulated in Fig. 2.42. Also shown separately in Fig. 2.45 are simpler, if approximate, expressions for the student to keep handy as we embark upon the study of discrete BJT amplifiers in the rest of this chapter. We note that the last two examples reveal a tendency that holds in general, namely, a crescendo in resistance levels as we go from $R_{e}$ (small), to $R_{b}$ (medium), to $R_{c}$ (large).
### A Practical Application: The BJT as a Current Source
The BJT's ability to achieve truly high $R_{c}$ values makes it suited to the implementation of current sources/sinks. Figure 2.46 offers an example of how a pnp BJT can be configured to source current to a load (LD). If we need to sink
image_name:(a)
description:
[
name: Q, type: NPN, ports: {C: GND, B: b, E: e}
name: RE, type: Resistor, value: RE, ports: {N1: e, N2: GND}
]
extrainfo:Figure (a) shows a simple NPN BJT circuit with the base connected to node 'b', the emitter connected to node 'e', and the collector connected to ground. The resistor RE is connected between the emitter and ground.
image_name:(b)
description:
[
name: Q, type: NPN, ports: {C: GND, B: "b", E: e}
name: RB, type: Resistor, value: RB, ports: {N1: GND, N2: "b"}
]
extrainfo:This is a BJT configuration showing small-signal resistances with an NPN transistor and a resistor RB. The transistor's collector is connected to GND, the base is connected through RB to GND, and the emitter is labeled as 'e'.
image_name:(c)
description:
[
name: Q, type: NPN, ports: {C: c, B: GND, E: e}
name: RE, type: Resistor, value: RE, ports: {N1: e, N2: GND}
]
extrainfo:The circuit diagram (c) features an NPN transistor (Q) with its collector connected to node 'c', base to ground, and emitter to node 'e'. The resistor RE is connected between node 'e' and ground. This configuration is a simplified representation of a common-emitter amplifier stage with emitter degeneration.
FIGURE 2.45 Visualizing the small-signal resistances seen looking into the base, emitter, and collector. The effect of $r_{o}$ is negligible in (a) and (b), so it has been ignored.
current from the load, then we use an npn BJT with all voltages and currents reversed. As we shall see, a common application of current sources/sinks is to bias other circuits.
EXAMPLE 2.16 Let the BJT of Fig. 2.46 have $\beta_{0}=\beta_{F}=100, V_{A}=100 \mathrm{~V}, V_{E B(\text { on })}=0.7 \mathrm{~V}$, and $V_{E C(\mathrm{EOS})}=0.2 \mathrm{~V}$.
(a) Find $I_{O}$ and $R_{o}$.
(b) What is the maximum load voltage for which the circuit will still operate properly?
(c) By how much does $I_{O}$ change for each 1-V change in the voltage across the load? Express this change in percentage form.
image_name:FIGURE 2.46
description:
[
name: R1, type: Resistor, value: 100kΩ, ports: {N1: VCC, N2: b}
name: R2, type: Resistor, value: 100kΩ, ports: {N1: b, N2: GND}
name: RE, type: Resistor, value: 10kΩ, ports: {N1: e, N2: VDD}
name: Q, type: PNP, ports: {C: VL, B: b, E: e}
]
extrainfo:The circuit uses a PNP BJT to implement a current source with an output current of 0.5mA. The Norton equivalent circuit includes a 3.3MΩ resistor in parallel with the current source. The BJT is biased with a voltage VCC of 12V, and the resistors R1 and R2 form a voltage divider to provide the base voltage. The emitter resistor RE is connected to ground.
image_name:Norton equivalent
description:The circuit uses a PNP BJT to implement a current source with a Norton equivalent. The BJT is biased with resistors R1 and R2, and the emitter is connected to RE. The Norton equivalent circuit consists of a 0.5mA current source and a 3.3MΩ resistor. The load voltage VL can be measured across the load LD, and the output current IO flows through it.
FIGURE 2.46 Using a pnp BJT to implement a current source, and its Norton equivalent.
#### Solution
(a) We have $V_{B B}=6 \mathrm{~V}$ and $R_{B}=50 \mathrm{k} \Omega$. Proceeding as in the first part of Example 2.8 , we get $I_{O}=0.5 \mathrm{~mA}$. So, $g_{m}=0.5 / 26=1 /(52 \Omega), r_{\pi}=100 \times 52=$ $5.2 \mathrm{k} \Omega$, and $r_{o}=100 / 0.5=200 \mathrm{k} \Omega$. By Eq. $(2.62 a)$,
$$
R_{o} \cong 200\left[1+\frac{(5.2 / / 10) / 0.052}{1+50 /(5.2+10)}\right]=3.3 \mathrm{M} \Omega
$$
(b) To ensure proper circuit operation we must prevent the BJT from ever saturating. Considering that $V_{E} \cong 12-10 \times 0.5=7 \mathrm{~V}$, we need to ensure that the collector voltage never rises above $7-0.2=6.8 \mathrm{~V}$. Consequently, the maximum permissible load voltage is 6.8 V .
(c) For each $1-\mathrm{V}$ change in the load voltage within the permissible range $I_{O}$ changes by $(1 \mathrm{~V}) /(3.3 \mathrm{M} \Omega)=0.3 \mu \mathrm{~A}$. This represents $0.06 \%$ of the nominal $500-\mu \mathrm{A}$ output current, a truly small value if you think. We now know how to apply a BJT to implement a good-quality current source/sink!
## 2.7 BJT BIASING FOR AMPLIFIER DESIGN
As we know, to operate a BJT as an amplifier we must bias it in the forward active (FA) region. Since the amplifier's characteristics are determined by the smallsignal parameters $g_{m}, r_{\pi}$, and $r_{o}$, which in turn depend on the bias current $I_{C}$, it is apparent that to achieve predictable and stable amplifier characteristics we need to establish a predictable and stable bias current $I_{C}$. Among the factors conspiring against us is the spread in the parameter values of the BJTs that we use, particularly $V_{B E(\text { on })}$ and $\beta_{F}$. When designing a BJT circuit, it is customary to assume the typical values
$$
\begin{gather*}
V_{B E(\mathrm{on})}=0.7 \mathrm{~V}  \tag{2.63a}\\
\beta_{F}=100 \tag{2.63b}
\end{gather*}
$$
which we shall also refer to as nominal values. However, because of fabrication process variations, the actual values will vary from one BJT sample to another, even for samples of the same device type, such as the popular 2N2222 considered previously. For example, Eqs. (2.11) and (2.15) indicate that both $I_{s}$ and $\beta_{F}$ are inversely proportional to the base width $W_{B}$, which is fabricated very thin (a fraction of a micro-meter) to ensure high betas. With reference to Fig. 2.1, it is not difficult to imagine the impact of even a tiny variation in the depth of the $n^{+}$emitter diffusion during fabrication. Moreover, both $I_{s}$ and $\beta_{F}$ drift with temperature as well as with time, so their actual values can lie anywhere within a range that can be quite wide. For the sake of discussion we shall assume the following parameter-value spreads:
$$
\begin{gather*}
0.4 \mathrm{~V} \leq V_{B E(\text { on })} \leq 0.8 \mathrm{~V}  \tag{2.64a}\\
50 \leq \beta_{F} \leq 200 \tag{2.64b}
\end{gather*}
$$
As a rule, the performance of a transistor circuit should be independent of the particular transistor sample being used, so a good BJT amplifier requires a quiescent point $Q=Q\left(I_{C}, V_{C E}\right)$ that is relatively independent of $V_{B E(\text { on })}$ and $\beta_{F}$. As an added bonus, should a BJT fail, we can simply replace it with one of the same family and still expect the same overall performance level, even though the actual parameter values of the new unit may be quite different from those of the old unit.
Based on our studies so far, a given bias current $I_{C}$ can be established in three different ways,
$$
I_{C}=\beta_{F} I_{B}=\alpha_{F} I_{E}=I_{s} e_{B E}^{V_{B E} / V_{T}}
$$
that is, via $I_{B}$, via $I_{E}$, or via $V_{B E}$. In the following we shall investigate merits and drawbacks of each.
image_name:FIGURE 2.47 BJT biasing via I_B
description:
[
name: RB, type: Resistor, value: RB, ports: {N1: VCC, N2: b}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: c}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: Q, type: NPN, ports: {C: c, B: b, E: GND}
]
extrainfo:The circuit is a BJT biasing scheme using resistor RB to set the base current IB, establishing collector current IC with the relation IC = βF IB. Resistor RC is used to set the voltage VCE across the transistor. The circuit is powered by VCC.
FIGURE 2.47 BJT biasing via $I_{B}$.
### BJT Biasing via $I_{B}$
The biasing scheme of Fig. 2.47 uses $R_{B}$ to establish the base drive $I_{B}$ necessary to sustain the desired bias current as $I_{C}=\beta_{F} I_{B}$. Moreover, it uses $R_{C}$ to achieve the desired voltage $V_{C E}$. We have
$$
\begin{gather*}
I_{C}=\beta_{F} \frac{V_{C C}-V_{B E(\mathrm{n})}}{R_{B}}  \tag{2.65a}\\
V_{C E}=V_{C C}-R_{C} I_{C} \tag{2.65b}
\end{gather*}
$$
We immediately note a serious drawback of this biasing scheme, namely, $I_{C}$ being directly proportional to $\beta_{F}$, which is notoriously an ill-defined parameter. Consequently, the spread of Eq. (2.64b) will affect $I_{C}$ as well. An actual example will better illustrate.
EXAMPLE 2.17 (a) Assuming $V_{C C}=12 \mathrm{~V}$ in the circuit of Fig. 2.47, along with the nominal specifications of Eq. (2.63), specify standard 5\% values for $R_{B}$ and $R_{C}$ to bias the BJT at $I_{C}=1 \mathrm{~mA}$ and $V_{C E}=5 \mathrm{~V}$.
(b) Find the range of variability of $I_{C}$ and $V_{C E}$ as a consequence of the parameter spread of Eq. (2.64). Comment on your results.
#### Solution
(a) By Eq. $(2.65 a)$,
$$
R_{B}=100 \frac{12-0.7}{1}=1.13 \mathrm{M} \Omega
$$
The closest standard value is $1.1 \mathrm{M} \Omega$. Reinserting it into Eq. (2.65a) gives $I_{C \text { (nom) }} \cong 1.03 \mathrm{~mA}$. By Eq. (2.65b),
$$
R_{C}=\frac{12-5}{1.03}=6.8 \mathrm{k} \Omega
$$
which is a standard value. In summary, using $R_{B}=1.1 \mathrm{M} \Omega$ and $R_{C}=6.8 \mathrm{k} \Omega$ yields $I_{C(\text { nom })} \cong 1.03 \mathrm{~mA}$ and $V_{C E(\text { nom })}=5 \mathrm{~V}$.
(b) Equation (2.65) indicates that $I_{C}$ is minimized when $\beta_{F}$ is minimum and $V_{B E \text { (on) }}$ is maximum. Moreover, when $I_{C}$ is minimized, $V_{C E}$ is maximized, and vice versa. We thus have
$$
I_{C(\min )}=50 \frac{12-0.8}{1100}=0.51 \mathrm{~mA} \quad \mathrm{~V}_{C E(\max )}=12-6.8 \times 0.51=8.5 \mathrm{~V}
$$
Likewise, using the maximum value of $\beta_{F}$ and the minimum value of $V_{B E(\text { on })}$ we would get
$$
I_{C}=200 \frac{12-0.4}{1100}=2.1 \mathrm{~mA} \quad V_{C E}=12-6.8 \times 2.1=-2.3 \mathrm{~V}
$$
The last result is impossible, indicating a saturated BJT! Consequently, under the given conditions, we have
$$
V_{C E(\min )}=V_{C E(\mathrm{sat})}=0.1 \mathrm{~V} \quad I_{C(\max )}=\frac{12-0.1}{6.8}=1.75 \mathrm{~mA}
$$
It is apparent that under the given conditions, this biasing scheme is unacceptable, for not only does it result in a wide spread of operating points, but it may even drive the BJT in saturation.
However tempting because of its simplicity, the biasing scheme of Fig. 2.47 is seldom used in actual BJT amplifier design. It is used, however, to bias the BJT in saturation in switching applications. As we have already seen in Example 2.11, the BJT is biased in deep saturation precisely to cope with the wide spread in the values of $\beta_{F}$. The reason for covering this scheme is to pave the way for the alternative scheme to be discussed next.
### BJT Biasing via $I_{E}$
A much better alternative is to bias the BJT via its emitter current $I_{E}$ to get $I_{C}=\alpha_{F} I_{E}$. The reason is that the spread in the values of $\alpha_{F}$ is far more limited than that of $\beta_{F}$. Indeed, since $\alpha_{F}=\beta_{F} /\left(\beta_{F}+1\right)$, the spread of Eq. (2.64b) translates into the following spread for $\alpha_{F}$,
$$
0.980 \leq \alpha_{F} \leq 0.995
$$
that is, a spread of less than $1.5 \%$ ! To establish $I_{E}$ we need to bias the emitter at some voltage $V_{E}>0$, and then use an emitter resistance $R_{E}$ to set $I_{E}=V_{E} / R_{E}$. This is achieved by biasing the base via the voltage divider $R_{1}-R_{2}$, as depicted in Fig. 2.48. This circuit is identical to that of Fig. 2.27a, so we simply recycle the results developed there and write
$$
\begin{gather*}
I_{C}=\beta_{F} \frac{V_{B B}-V_{B E(\mathrm{n})}}{R_{B}+\left(\beta_{F}+1\right) R_{E}}  \tag{2.66a}\\
V_{C E} \cong V_{C C}-\left(R_{C}+R_{E}\right) I_{C} \tag{2.66b}
\end{gather*}
$$
FIGURE 2.48 BJT biasing via $I_{E}$.
image_name:FIGURE 2.48 BJT biasing via I_E
description:
[
name: R1, type: Resistor, value: R1, ports: {N1: VCC, N2: b}
name: R2, type: Resistor, value: R2, ports: {N1: b, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: c}
name: RE, type: Resistor, value: RE, ports: {N1: e, N2: GND}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: Q1, type: NPN, ports: {C: c, B: b, E: e}
]
extrainfo:This is a BJT biasing circuit using a voltage divider for biasing the base of the NPN transistor. The voltage source VCC provides power to the circuit, and the resistors R1 and R2 form a voltage divider to set the base voltage. RC and RE are used to set the collector and emitter currents, respectively.
where
$$
\begin{equation*}
V_{B B}=\frac{R_{2}}{R_{1}+R_{2}} V_{C C} \quad R_{B}=R_{1} / / R_{2} \tag{2.67}
\end{equation*}
$$
(Note that in Eq. (2.66b) we have approximated $I_{E} \cong I_{C}$.) Dividing numerator and denominator by $\beta_{F}$ in the right-hand side of Eq. (2.66a), and letting $\left(\beta_{F}+1\right) / \beta_{F} \cong 1$, yields the more insightful expression
$$
I_{C} \cong \frac{V_{B B}-V_{B E(\mathrm{on})}}{R_{B} / \beta_{F}+R_{E}}
$$
This instructs us on how to go to ensure a fairly stable and predictable bias current $I_{C}$ :
- To render $I_{C}$ relatively insensitive to variations in $V_{B E(\text { n })}$ impose
$$
V_{B B} \gg \Delta V_{B E(\mathrm{n})}
$$
where $\Delta V_{B E(\text { on })}$ is the expected spread in $V_{B E(\text { on })}$ (In our running example we have $\Delta V_{B E(\mathrm{~m})}=0.8-0.4=0.4 \mathrm{~V}$.) Indirectly this condition implies that the emitter voltage $V_{E}$ be made large enough to swamp any variations in $V_{B E(\text { on })}$. Clearly, the larger $V_{E}$ the better. However, this erodes the signal swing of the collector. A reasonable compromise is to impose $V_{E} \cong 10 \Delta V_{B E(\text { on })}$ and then to bias the collector halfway between $V_{C C}$ and $V_{E}$ for a symmetric collector signal swing. Some authors simply propose the so-called $1 / 3-1 / 3-1 / 3$ Rule: Let $V_{E}=\frac{1}{3} V_{C C}$ and $V_{C E}=\frac{1}{3} V_{C C}$, so $R_{C} I_{C}=\frac{1}{3} V_{C C}$.
- To render $I_{C}$ relatively insensitive to variations in $\beta_{F}$ impose
$$
R_{B} / \beta_{F} \ll R_{E}
$$
Indirectly, this condition implies that $R_{1}$ and $R_{2}$ be chosen small enough so that their standby current is sufficiently large to swamp the effect of any variations in the base current $I_{B}$ stemming from the spread in $\beta_{F}$. Clearly, the smaller $R_{1}$ and $R_{2}$ the better. However, this increases the current drain from $V_{C C}$ and, even more undesirable, it lowers the input resistance when the base is used as the amplifier's input. A reasonable compromise is to impose a standby current of about $10 I_{B(\text { nom })}$.
(a) Assuming $V_{C C}=12 \mathrm{~V}$ in the circuit of Fig. 2.48, along with the nominal
#### ExAMPLE 2.18
specifications of Eq. (2.63), specify standard $5 \%$ resistances to bias the BJT at $I_{C}=1 \mathrm{~mA}$ and the collector halfway between $V_{C C}$ and $V_{E}$. Show your final circuit and calculate the nominal values of $I_{C}$ and $V_{C E}$.
(b) Find the range of variability of $I_{C}$ and $V_{C E}$ as a consequence of the parameter spread of Eq. (2.64). Comment on your results.
#### Solution
(a) Let $V_{E}=10 \Delta V_{B E(\mathrm{on})}=10 \times 0.4=4 \mathrm{~V}$. To bias the collector halfway we need $V_{C}=\left(V_{C C}+V_{E}\right) / 2=(12+4) / 2=8 \mathrm{~V}$. Then, approximating $I_{E} \cong I_{C}$, we find
$$
R_{E}=\frac{V_{E}}{I_{E}} \cong \frac{4}{1}=4 \mathrm{k} \Omega \quad R_{C}=\frac{V_{C C}-V_{C}}{I_{C}}=\frac{12-8}{1}=4 \mathrm{k} \Omega
$$
The closest standard values are $R_{E}=R_{C}=3.9 \mathrm{k} \Omega$.
We have $I_{B(\text { nom })}=1 / 100=10 \mu \mathrm{~A}$. Impose a current through $R_{2}$ of $10 I_{B(\text { nom })}$, or $10 \times 10=100 \mu \mathrm{~A}$. Considering that we have, by KVL, $V_{B}=V_{E}+V_{B E(\text { on })}=$ $4+0.7=4.7 \mathrm{~V}$, then
$$
R_{2}=\frac{V_{B}}{I_{R_{2}}}=\frac{4.7}{0.1}=47 \mathrm{k} \Omega
$$
which is a standard value. The current through $R_{1}$ is, by KCL, $10+100=$ $110 \mu \mathrm{~A}$, so
$$
R_{1}=\frac{V_{C C}-V_{B}}{I_{R_{1}}}=\frac{12-4.7}{0.11}=66 \mathrm{k} \Omega
$$
The closest standard value is $68 \mathrm{k} \Omega$. The circuit is shown in Fig. 2.49.
image_name:Figure 2.49 Circuit of Example 2.18
description:
[
name: R1, type: Resistor, value: 68kΩ, ports: {N1: VCC, N2: b}
name: R2, type: Resistor, value: 47kΩ, ports: {N1: b, N2: GND}
name: RC, type: Resistor, value: 3.9kΩ, ports: {N1: VCC, N2: c}
name: RE, type: Resistor, value: 3.9kΩ, ports: {N1: e, N2: GND}
name: VCC, type: VoltageSource, value: 12V, ports: {Np: VCC, Nn: GND}
name: Q, type: NPN, ports: {C: c, B: b, E: e}
]
extrainfo:The circuit is a common-emitter amplifier with an NPN transistor. It includes biasing resistors R1 and R2 for base biasing and resistors RC and RE for collector and emitter stabilization, respectively. The table provides the minimum, nominal, and maximum values for collector current IC and collector-emitter voltage VCE.
image_name:Table of I_C and V_CE values
description:The image consists of a circuit diagram and a table.
**Circuit Diagram:**
- The circuit is powered by a voltage source labeled \( V_{CC} = 12 \text{ V} \).
- There are two resistors connected in a voltage divider configuration: \( R_1 = 68 \text{ k}\Omega \) and \( R_2 = 47 \text{ k}\Omega \).
- A transistor labeled \( Q \) is included in the circuit with the collector \( C \), base \( B \), and emitter \( E \) terminals marked.
- The collector is connected to a resistor \( R_C = 3.9 \text{ k}\Omega \) and the emitter is connected to a resistor \( R_E = 3.9 \text{ k}\Omega \).
- The voltage \( V_{CE} \) is indicated across the collector-emitter junction of the transistor.
**Table:**
- The table lists values for collector current \( I_C \) and collector-emitter voltage \( V_{CE} \) under different conditions:
- **Min:** \( I_C = 0.904 \text{ mA} \), \( V_{CE} = 3.4 \text{ V} \)
- **Nom:** \( I_C = 0.996 \text{ mA} \), \( V_{CE} = 4.2 \text{ V} \)
- **Max:** \( I_C = 1.109 \text{ mA} \), \( V_{CE} = 4.9 \text{ V} \)
FIGURE 2.49 Circuit of Example 2.18.
To find the nominal values of $I_{C}$ and $V_{C E}$, insert $R_{1}=68 \mathrm{k} \Omega$ and $R_{2}=47 \mathrm{k} \Omega$ into Eq. (2.67) and find $V_{B B}=4.9 \mathrm{~V}$ and $R_{B}=27.8 \mathrm{k} \Omega$. Then, use Eq. (2.66) to find
$$
\begin{aligned}
& I_{C(\mathrm{nom})}=100 \frac{4.9-0.7}{27.8+(100+1) 3.9}=0.996 \mathrm{~mA} \\
& V_{C E(\mathrm{nom})}=12-(3.9+3.9) 0.996=4.2 \mathrm{~V}
\end{aligned}
$$
(b) Equation (2.66) indicates that $I_{C}$ is minimized when $\beta_{F}$ is minimum and $V_{B E(\text { on })}$ is maximum. Moreover, when $I_{C}$ is minimized, $V_{C E}$ is maximized, and vice versa. We thus have
$$
\begin{aligned}
& I_{C(\min )}=50 \frac{4.9-0.8}{27.8+(50+1) 3.9}=0.904 \mathrm{~mA} \\
& V_{C E(\max )}=12-(3.9+3.9) 0.904=4.9 \mathrm{~V}
\end{aligned}
$$
Likewise, using the maximum value of $\beta_{F}$ and the minimum value of $V_{B E(\text { n })}$ we get
$$
\begin{aligned}
& I_{C(\max )}=200 \frac{4.9-0.4}{27.8+(200+1) 3.9}=1.109 \mathrm{~mA} \\
& V_{C E(\min )}=12-(3.9+3.9) 1.109=3.4 \mathrm{~V}
\end{aligned}
$$
The data are tabulated in Fig. 2.49, where we observe a spread in $I_{C}$ on the order of $\pm 10 \%$. Not at all bad, considering the much wider spreads of Eq. (2.64)!
You may be wondering what makes the BJT maintain $I_{C}$ at its prescribed value of 1 mA . Suppose the BJT attempted to draw less than 1 mA . Then, the voltage drop across $R_{E}$ would decrease, causing a decrease also in $V_{E}$. But this, in turn, would increase $V_{B E}$, thus directing the BJT to draw more current. Conversely, any attempt to draw more than 1 mA would be met by a decrease in $V_{B E}$, and thus an invitation to draw less current. In either case, any attempt by $I_{C}$ to deviate from its prescribed value of about 1 mA is met by a counteraction that tends to restore $I_{C}$ to its prescribed value. This state of affairs is summarized by saying that $R_{E}$ provides a negative feedback action around the BJT, and that this action tends to stabilize the biasing condition of the device (more on this in Chapter 7).
### Feedback Bias
Figure 2.50 shows an alternative biasing scheme in which the stabilizing feedback action is now provided by $R_{C}$ and $R_{F}$. To see how, note that the current coming from $R_{C}$ splits between the base and the collector, and then re-converges at the emitter, so it must equal $I_{E}$, as shown. By KVL and Ohm's law,
$$
V_{C C}=R_{C} I_{E}+R_{F} I_{B}+V_{B E(\mathrm{on})}
$$
Substituting $I_{E}=\left[\left(\beta_{F}+1\right) / \beta_{F}\right] I_{C}$ and $I_{B}=I_{C} / \beta_{F}$, collecting, and solving for $I_{C}$ gives
$$
\begin{equation*}
I_{C}=\beta_{F} \frac{V_{C C}-V_{B E(\mathrm{on})}}{R_{F}+\left(\beta_{F}+1\right) R_{C}} \tag{2.68a}
\end{equation*}
$$
image_name:FIGURE 2.50 Feedback bias.
description:
[
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: C(VCE)}
name: RF, type: Resistor, value: RF, ports: {N1: b, N2: C(VCE)}
name: Q1, type: NPN, ports: {C: C(VCE), B: b, E: GND}
]
extrainfo:The circuit represents a feedback bias configuration using an NPN transistor. The voltage V_CC is applied across the resistor RC and the transistor, while RF provides feedback to the base of the transistor. The emitter is connected to ground.
FIGURE 2.50 Feedback bias.
This expression is similar to that of Eq. (2.66a), but with $R_{C}$ in place of $R_{E}, R_{F}$ in place of $R_{B}$, and $V_{C C}$ in place of $V_{B B}$. Consequently, the stabilizing advantages discussed above hold also in the present case. We also have, by KVL, $V_{C E}=V_{B E(\text { on })}+R_{F} I_{B}$, or
$$
\begin{equation*}
V_{C E}=V_{B E(\mathrm{on})}+\frac{R_{F}}{\beta_{F}} I_{C} \tag{2.68b}
\end{equation*}
$$
indicating that this scheme does not offer much flexibility for the specification of $V_{C E}$. Typically, $V_{C E}$ is just a bit higher than $V_{B E(\text { on })}$, so the collector's downswing capability is much more limited than with the scheme of Fig. 2.48. The circuit of Fig. 2.50 finds application in preamplifier situations, where the signals are small enough to fit within the modest signal swing.
(a) Assuming $V_{C C}=12 \mathrm{~V}$ in the circuit of Fig. 2.50, along with the nominal specifications of Eq. (2.63), specify standard 5\% resistances to bias the BJT at $I_{C}=1 \mathrm{~mA}$.
(b) What are the nominal collector swing capabilities of your circuit?
#### Solution
(a) Impose $R_{F} \ll\left(\beta_{F}+1\right) R_{C}=101 R_{C}$. Pick $R_{F}=10 R_{C}$. Then, substitution into Eq. (2.68a) gives
$$
1=100 \frac{12-0.7}{10 R_{C}+(100+1) R_{C}}
$$
or $R_{C}=10.2 \mathrm{k} \Omega$. Pick the standard value $R_{C}=10 \mathrm{k} \Omega$. Then, $R_{F}=100 \mathrm{k} \Omega$.
(b) Plugging the above resistance values into Eq. (2.68) gives $I_{C}=1.02 \mathrm{~mA}$ and $V_{C E}=1.7 \mathrm{~V}$. The nominal downswing is $V_{C E}-V_{C E(\mathrm{EOS})}=1.7-0.2=1.5 \mathrm{~V}$. The nominal upswing is $V_{C C}-V_{C E}=12-1.7=10.3 \mathrm{~V}$, indicating a highly asymmetric situation.
### BJT Biasing via $\mathbf{V}_{B E}$ (Current Mirror)
The third way of biasing a BJT is via a suitable voltage drive $V_{B E}$ in the manner illustrated previously in Fig. 2.39a. Because of the exponential dependence of $I_{C}$ upon $V_{B E}$, the $V_{B E}$ drive needs to be accurate down to the milli-volt if we want to ensure a prescribed $I_{C}$ with a good degree of reproducibility. Considering the spread of Eq. (2.64a), along with the fact that $V_{B E}$ is temperature sensitive, this is a most arduous task, unless we have a means for anticipating the required $V_{B E}$ as well as the ability to continuously adjust it to follow the whims of temperature.
In integrated circuits (ICs) this task is accomplished rather easily by exploiting the superior matching characteristics of devices fabricated simultaneously on the same substrate. Simply put, to bias a certain BJT $Q_{2}$ at a prescribed current $I_{C 2}$, we use a twin BJT $Q_{1}$ connected as a diode, and we drive it with a current $I_{C 1}$ of the same magnitude as the desired current $I_{C 2} . Q_{1}$ then develops a voltage $V_{B E}$ that is fed also to $Q_{2}$. Since the two devices are matched and experience the same $V_{B E}$ drop, $I_{C 2}$ will simply mimic $I_{C 1}$, this being the reason why the two BJTs are said to form a current mirror. Moreover, if the BJTs lie next to each other on the chip, they will experience the same temperature variations, so their characteristics will drift identically, a feature known as temperature tracking. This ingenious technique is illustrated in Fig. 2.51. Ignoring the tiny base currents, and also ignoring the Early effect as is customary in dc analysis, we express the bias conditions of $Q_{2}$, the device being biased, as $I_{C 2}=I_{C 1}$, or
$$
\begin{align*}
I_{C 2} & =\frac{V_{C C}-V_{B E}}{R_{1}}  \tag{2.69a}\\
V_{C E 2} & =V_{C C}-R_{2} I_{C 2} \tag{2.69b}
\end{align*}
$$
Current mirrors find wide application in IC design, both as current-signal processing blocks also known as current reversers, and as dc biasing blocks for other circuits. For instance, $Q_{2}$ of this circuit could be used to provide the emitter current bias for yet another BJT for its use as an amplifier.
FIGURE 2.51 Current-mirror arrangement to bias $Q_{2}$. Note: $Q_{1}$ and $Q_{2}$ are matched BJTs.
image_name:Figure 2.51
description:
[
name: Q1, type: NPN, ports: {C: b1Cb2(VBE), B: b1Cb2(VBE), E: GND}
name: Q2, type: NPN, ports: {C: C2, B: b1Cb2(VBE), E: GND}
name: R1, type: Resistor, value: R1, ports: {N1: Vcc, N2: b1Cb2(VBE)}
name: R2, type: Resistor, value: R2, ports: {N1: Vcc, N2: C2}
]
extrainfo:The circuit is a current mirror with matched BJTs Q1 and Q2. It biases Q2 with IC2. The resistors R1 and R2 set the biasing currents for Q1 and Q2, respectively. The capacitor C2 is connected across the collector of Q2 to ground.
Assuming $V_{C C}=5 \mathrm{~V}$ in the circuit of Fig. 2.51, along with the nominal specifications of Eq. (2.63), specify standard 5\% resistances to bias $Q_{2}$ at $I_{C}=1 \mathrm{~mA}$ and its collector right in the middle of the active region.
#### Solution
By Ohm's law, $R_{1}=(5-0.7) / 1=4.3 \mathrm{k} \Omega$, and $R_{2}=(5-2.5) / 1=2.5 \mathrm{k} \Omega$ (use $2.4 \mathrm{k} \Omega$ ).
It goes without saying that the biasing scheme of Fig. 2.51 works well only in IC situations. If we were to use discrete BJT samples, they would most likely be mismatched, and certainly would not track each other in temperature as closely as in the case of monolithic devices. If you use PSpice to simulate a circuit, be aware that all BJTs with the same device model are treated as identical, giving the beginner the false impression of matched devices throughout. If needed, one can use Monte Carlo techniques to simulate the parameter spreads of real-life discrete devices. ${ }^{6}$
## 2.8 BASIC BIPOLAR VOLTAGE AMPLIFIERS
Depending on which terminal we apply the input to, and which terminal we obtain the output from, a BJT can be used in any one of three amplifier configurations: the common-emitter, common-collector, and common-base configurations. Viewing an amplifier as a two-port block, it is apparent that one of the three terminals of the BJT will have to be common to both ports (hence the reason for the above designations). The circuit implementations to be discussed herewith are referred to as discrete because we can build them using discrete transistors, resistors, and capacitors. Though nowadays a great deal of BJT amplifiers are implemented in integrated-circuit (IC) form, the motivation for studying discrete BJT implementations is not only historical, but also pedagogical as discrete designs are somewhat easier to grasp, and yet reveal important aspects that apply to IC implementations as well. Moreover, students who have access to an electronics lab can try them out experimentally to reinforce their understanding while simultaneously developing experimental skills as part of a wellrounded academic formation. Lacking a lab, the student can simulate the circuits via PSpice (see Appendix 2A).
### Unilateral Voltage Amplifiers
Figure 2.52 shows the block diagram of a voltage amplifier of the unilateral type, so called because the signal progresses only in the forward direction, from source to load, with no return signal paths. (In the next section we will encounter an example of a non-unilateral amplifier in the common-collector configuration. More examples will be found in the study of IC amplifiers.) The amplifier receives its input $v_{i}$ from a signal source $v_{s i g}$ with internal resistance $R_{s i g}$, and supplies its output $v_{o}$ to a resistive load $R_{L}$. The amplifier is uniquely characterized in terms of its input resistance $R_{i}$,
image_name:FIGURE 2.52
description:The block diagram in FIGURE 2.52 represents a unilateral voltage amplifier system. This system consists of several key components arranged to amplify an input signal and deliver it to a load.
1. **Main Components:**
- **Signal Source ($v_{sig}$):** This is the initial input voltage source with an internal resistance $R_{sig}$. It provides the input signal to the amplifier.
- **Input Resistance ($R_{i}$):** This is the resistance at the amplifier's input. It forms a voltage divider with the source resistance $R_{sig}$.
- **Amplifier Block:** The central component of the diagram, characterized by an open-circuit voltage gain $a_{oc}$. The amplifier takes the input voltage $v_{i}$ and produces an amplified output $a_{oc} \times v_{i}$.
- **Output Resistance ($R_{o}$):** This is the resistance at the amplifier's output, which forms a voltage divider with the load resistance $R_{L}$.
- **Load Resistance ($R_{L}$):** The resistive load connected at the output of the amplifier, receiving the amplified signal.
2. **Flow of Information or Control:**
- The input signal $v_{sig}$ flows through the internal resistance $R_{sig}$ and is divided across $R_{sig}$ and $R_{i}$, resulting in $v_{i}$ at the amplifier input. This is expressed by the equation $v_{i} = \frac{R_{i}}{R_{sig} + R_{i}} v_{sig}$.
- The amplifier then processes $v_{i}$, amplifying it by the factor $a_{oc}$, creating an intermediate signal $a_{oc} \times v_{i}$.
- The amplified signal passes through the output resistance $R_{o}$, which with $R_{L}$ forms another voltage divider, resulting in the final output voltage $v_{o} = \frac{R_{L}}{R_{o} + R_{L}} a_{oc} \times v_{i}$.
3. **Labels, Annotations, and Key Indicators:**
- The diagram is annotated with the variables $v_{sig}$, $v_{i}$, and $v_{o}$ to indicate the input, intermediate, and output voltages, respectively.
- Resistances $R_{sig}$, $R_{i}$, $R_{o}$, and $R_{L}$ are labeled to show their roles in the voltage division process.
- The gain $a_{oc}$ is highlighted as the key parameter of the amplifier's performance.
4. **Overall System Function:**
- The primary function of this system is to amplify an input voltage signal $v_{sig}$ and deliver it to a load with a desired gain. The system is designed to minimize loading effects at both the input and output, ensuring that the amplifier's performance is primarily determined by its internal characteristics and the external resistive load, rather than the source or load resistances themselves. The unilateral nature of the amplifier indicates that there is no feedback path from output to input, simplifying the analysis and design of the system.
FIGURE 2.52 Block diagram of a voltage amplifier of the unilateral type.
output resistance $R_{o}$, and the open-circuit voltage gain $a_{o c}$. At the amplifier's input we have a voltage divider, resulting in input loading
$$
\begin{equation*}
v_{i}=\frac{R_{i}}{R_{s i g}+R_{i}} v_{s i g} \tag{2.70}
\end{equation*}
$$
Likewise, at the amplifier's output we have another voltage divider, resulting in output loading
$$
\begin{equation*}
v_{o}=\frac{R_{L}}{R_{o}+R_{L}} a_{o c} \times v_{i} \tag{2.71}
\end{equation*}
$$
We observe that
$$
\begin{equation*}
a_{o c}=\lim _{R_{L} \rightarrow \infty} \frac{v_{o}}{v_{i}} \tag{2.72a}
\end{equation*}
$$
that is, $a_{o c}$ represents the gain with which the amplifier would amplify its input $v_{i}$ in the absence of any output load. Consequently, $a_{o c}$ is called the open-circuit voltage gain, or also the unloaded gain. Eliminating $v_{i}$ from the above equations we obtain the signal-to-load voltage gain
$$
\begin{equation*}
\frac{v_{o}}{v_{s i g}}=\frac{R_{i}}{R_{s i g}+R_{i}} \times a_{o c} \times \frac{R_{L}}{R_{o}+R_{L}} \tag{2.73}
\end{equation*}
$$
As the signal progresses from the source to the load, first it undergoes some attenuation at the amplifier's input, then it gets magnified by $a_{o c}$, and finally it undergoes some additional attenuation at the output. In light of Eq. (2.73) we can also write
$$
\begin{equation*}
a_{o c}=\left.\frac{v_{o}}{v_{s i g}}\right|_{R_{s i b} \rightarrow 0, R_{L} \rightarrow \infty} \tag{2.72b}
\end{equation*}
$$
which provides an alternative way of finding the unloaded gain.
### The Common-Emitter (CE) Configuration
In the circuit of Fig. 2.53 the amplifier proper is made up of the BJT and its surrounding components. To prevent the source and the load from disturbing the dc conditions of the amplifier, we use the ac-coupling capacitors $C_{1}$ and $C_{2}$. Moreover, to establish an ac ground at the emitter terminal, we use the bypass capacitor $C_{3}$.
image_name:Figure 2.53
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: vsig, N2: vi}
name: C1, type: Capacitor, value: C1, ports: {Np: vi, Nn: b}
name: RB, type: Resistor, value: RB, ports: {N1: b, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: c}
name: C2, type: Capacitor, value: C2, ports: {Np: c, Nn: vo}
name: RL, type: Resistor, value: RL, ports: {N1: vo, N2: GND}
name: C3, type: Capacitor, value: C3, ports: {Np: e, Nn: GND}
name: IE, type: CurrentSource, value: IE, ports: {Np: e, Nn: VEE}
name: Q, type: NPN, ports: {C: c, B: b, E: e}
name: VCC, type: VoltageSource, value: VCC, ports: {Np: VCC, Nn: GND}
name: VEE, type: VoltageSource, value: VEE, ports: {Np: VEE, Nn: GND}
]
extrainfo:The circuit is a common-emitter amplifier with ac-coupling capacitors C1 and C2, and a bypass capacitor C3 at the emitter. The BJT is biased with a current source IE. The input signal is Vs and the output is taken across RL. The circuit uses a dual power supply with VCC and VEE.
FIGURE 2.53 The common-emitter (CE) amplifier.
At dc, the capacitors draw zero current and thus act as open circuits. In fact, in the dc equivalent of Fig. 2.54a, the capacitors have been omitted altogether. Also, to simplify dc analysis, we assume $V_{A}=\infty$, and we use a dc current $\operatorname{sink} I_{E}$ to bias the BJT. Such a sink could be implemented with a current mirror of the type of Fig. 2.51 (let us not worry about these details here). The dc voltages are then
$$
\begin{equation*}
V_{B}=-R_{B} \frac{I_{E}}{\beta_{F}+1} \quad V_{C}=V_{C C}-\alpha_{F} R_{C} I_{E} \quad V_{E}=V_{B}-V_{B E(\mathrm{nn})} \tag{2.74}
\end{equation*}
$$
Moreover, we have $I_{C}=\alpha_{F} I_{E} \cong I_{E}$. When power is applied to the circuit, each capacitor will charge up until its plates attain the dc voltages of their corresponding nodes. For instance, while the bottom plate of $C_{3}$ remains at ground potential, the top plate will charge to $V_{E}$, which in this circuit is negative. Likewise, the left plate of $C_{2}$ will charge to $V_{C}$, while the right plate is pulled to 0 V by $R_{L}$.
image_name:(a)
description:
[
name: RB, type: Resistor, value: RB, ports: {N1: VB, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: VC}
name: IE, type: CurrentSource, value: IE, ports: {Np: VE, Nn: VEE}
name: VBE, type: VoltageSource, value: VBE, ports: {Np: VBE, Nn: VE}
name: αFIE, type: CurrentControlledVoltageSource, ports: {N1: VC, N2: VE}
]
extrainfo:This circuit is a common-emitter (CE) amplifier. It includes a current-controlled voltage source and a voltage-controlled current source, which are used to model the transistor behavior. The circuit is designed to amplify the input signal 'vsig' and provide an output 'vo'. The resistors and current source 'IE' are used for biasing and setting the operating point of the transistor.
image_name:(b)
description:
[
name: Rsig, type: Resistor, value: Rsig, ports: {N1: vsig, N2: vi}
name: RB, type: Resistor, value: RB, ports: {N1: vi, N2: vbe}
name: Rπ, type: Resistor, value: Rπ, ports: {N1: vi, N2: GND}
name: gmvbe, type: VoltageControlledCurrentSource, ports: {Np: vo, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: vo, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: vo, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: vo, N2: GND}
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: vsig, Nn: GND}
]
extrainfo:The circuit diagram is an AC equivalent of a common-emitter amplifier. It includes resistors, a voltage-controlled current source, and a voltage source. The circuit is used to determine the signal-to-load voltage gain.
FIGURE 2.54 (a) Dc and (b) ac equivalents of the CE amplifier of Fig. 2.53.
When analyzing a voltage amplifier we are interested in its signal-to-load voltage gain $v_{o} / v_{s i g}$. By Eq. (2.73), this requires finding the input resistance $R_{i}$ seen by the signal source, the output resistance $R_{o}$ seen by the load, and the unloaded voltage gain $a_{o c}$. We find these parameters by working on the ac equivalent of Fig. 2.54b. However, since the small-signal parameters $g_{m}, r_{\pi}$, and $r_{o}$ depend on the dc bias of the BJT, we need to analyze also the dc equivalent of Fig. 2.54a. Before proceeding, we wish to call the reader's attention to the difference between dc and ac analysis as well as the need to keep them separate!
In going from the original circuit of Fig. 2.53 to its dc equivalent of Fig. 2.54a we apply the following
### - Dc Analysis Procedure:
- Set all ac sources to zero
- Replace the BJT with its large-signal model (assume $V_{A}=\infty$ for simplicity)
- Replace all capacitors with open circuits
Conversely, in going from the original circuit of Fig. 2.53 to its ac equivalent of Fig. $2.54 b$ we apply by applying the following
- Ac Analysis Procedure:
- Set all $d c$ sources to zero
- Replace the BJT with its small-signal model, inclusive of $r_{o}$
- Replace all capacitors with short circuits
With reference to Fig. 2.54b, we note by inspection that
$$
\begin{equation*}
R_{i}=R_{B} / / r_{\pi} \quad R_{o}=R_{C} / / r_{o} \tag{2.75}
\end{equation*}
$$
Moreover, by Ohm's law, we have
$$
0-v_{o}=\left(r_{o} / / R_{C} / / R_{L}\right) g_{m} v_{b e}=\left(r_{o} / / R_{C} / / R_{L}\right) g_{m} v_{i}
$$
Letting $R_{L} \rightarrow \infty$ gives $v_{o}=-\left(r_{o} / / R_{C}\right) g_{m} v_{i}$. But, according to Eq. (2.72a), the ratio $v_{o} / v_{i}$ in the limit $R_{L} \rightarrow \infty$ is the unloaded voltage gain, so
$$
\begin{equation*}
a_{o c}=-g_{m}\left(R_{C} / / r_{o}\right) \tag{2.76}
\end{equation*}
$$
Having obtained expressions for $R_{i}, R_{o}$, and $a_{o c}$, we finally apply Eq. (2.73) to find the signal-to-load gain.
EXAMPLE 2.21 In the circuit of Fig. 2.53 let $V_{C C}=-V_{E E}=12 \mathrm{~V}, I_{E}=1 \mathrm{~mA}, R_{B}=75 \mathrm{k} \Omega$, and $R_{C}=6.2 \mathrm{k} \Omega$. Moreover, let the BJT have $\beta_{F}=150, V_{B E(\mathrm{on})}=0.7 \mathrm{~V}$, and $V_{A}=80 \mathrm{~V}$. Assuming $R_{s i g}=0.5 \mathrm{k} \Omega, R_{L}=30 \mathrm{k} \Omega$, and
$$
v_{s i g}=(5 \mathrm{mV}) \cos \omega t
$$
find all node voltages in the circuit, and express each of them as the sum of its dc and ac component, in the manner of Eq. (2.43).
image_name:FIGURE 2.55
description:
[
name: V1, type: VoltageSource, value: (5mV)cosωt, ports: {Np: Vin, Nn: GND}
name: R1, type: Resistor, value: 0.5kΩ, ports: {N1: Vin, N2: N1}
name: C1, type: Capacitor, value: C1, ports: {Np: N1, Nn: N2}
name: R2, type: Resistor, value: 75kΩ, ports: {N1: N2, N2: GND}
name: Q, type: NPN, ports: {C: N3, B: N2, E: N4}
name: R3, type: Resistor, value: 6.2kΩ, ports: {N1: N3, N2: VCC}
name: V2, type: VoltageSource, value: 12V, ports: {Np: VCC, Nn: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: N3, Nn: N5}
name: R6, type: Resistor, value: 30kΩ, ports: {N1: N5, N2: GND}
name: I1, type: CurrentSource, value: 1mA, ports: {Np: N4, Nn: VEE}
name: V3, type: VoltageSource, value: -12V, ports: {Np: GND, Nn: VEE}
name: C3, type: Capacitor, value: C3, ports: {Np: N4, Nn: GND}
]
extrainfo:The circuit is a common-emitter amplifier with a voltage gain. The NPN transistor Q is biased with a 1 mA current source. The input voltage is a small AC signal superimposed on a DC level. The circuit uses resistors and capacitors for biasing and coupling.
FIGURE 2.55 Circuit of Example 2.21, with each node voltage expressed as the sum of its $d c$ and ac component.
#### Solution
We have $I_{C} \cong I_{E}=1 \mathrm{~mA}$. By Eq. (2.74) we have
$$
\begin{aligned}
& V_{B}=-75 \frac{1}{151}=-0.5 \mathrm{~V} \\
& V_{C} \cong 12-6.2 \times 1=5.8 \mathrm{~V} \\
& V_{E}=-0.5-0.7=-1.2 \mathrm{~V}
\end{aligned}
$$
Moreover, $g_{m}=1 / 26 \mathrm{~A} / \mathrm{V}, r_{\pi}=150 \times 26=3.9 \mathrm{k} \Omega$, and $r_{o}=80 / 1=80 \mathrm{k} \Omega$. Consequently, Eqs. (2.75) and (2.76) give
$$
\begin{aligned}
R_{i} & =75 / / 3.9=3.7 \mathrm{k} \Omega \\
R_{o} & =6.2 / / 80=5.8 \mathrm{k} \Omega \\
a_{o c} & =-5,800 / 26=-223 \mathrm{~V} / \mathrm{V}
\end{aligned}
$$
Also, Eq. (2.70) gives $v_{i}=[3.7 /(0.5+3.7)] v_{s i g}=0.88 v_{s i g}=(4.4 \mathrm{mV}) \cos \omega t$. Finally, Eq. (2.73) gives
$$
\begin{aligned}
v_{o} & =\left[\frac{3.7}{0.5+3.7}(-223) \frac{30}{5.8+30}\right] v_{s i g}=-165 v_{s i g}=-165(5 \mathrm{mV}) \cos \omega t \\
& =(825 \mathrm{mV}) \cos \left(\omega t-180^{\circ}\right)
\end{aligned}
$$
The node voltages are shown in Fig. 2.55. The reader is encouraged to verify each of them in detail.
The systematic procedure of redrawing an amplifier both in dc and ac form, as exemplified in Fig. 2.54, though highly recommended for the beginner, may soon prove an overkill as one seeks to speed up the analysis process. With experience, some of the intermediate steps can be carried out mentally without having to draw
detailed circuit equivalents. Moreover, one can use inspection to recycle a good deal of the results summarized in Fig. 2.42. We shall illustrate with a variety of examples as we proceed.
EXAMPLE 2.22 (a) In Fig. $2.56 a$ the circuit designed in Example 2.18 is put to use as a CE amplifier. Recalling that $\beta_{F}=100$ and $I_{C}=0.99 \mathrm{~mA}$, find the small-signal parameters $R_{i}, R_{o}$, and $a_{o c}$. Assume $V_{A}=100 \mathrm{~V}$.
(b) Find the signal-to-load gain if the circuit is driven by a source with $R_{s i g}=$ $1 \mathrm{k} \Omega$ and drives a load $R_{L}=18 \mathrm{k} \Omega$.
image_name:(a)
description:
[
name: VCC, type: VoltageSource, value: 12V, ports: {Np: VCC, Nn: GND}
name: R1, type: Resistor, value: 68kΩ, ports: {N1: VCC, N2: b}
name: R2, type: Resistor, value: 47kΩ, ports: {N1: b, N2: GND}
name: RC, type: Resistor, value: 3.9kΩ, ports: {N1: VCC, N2: c}
name: RE, type: Resistor, value: 3.9kΩ, ports: {N1: e, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: vi, Nn: b}
name: C2, type: Capacitor, value: C2, ports: {Np: c, Nn: vo}
name: C3, type: Capacitor, value: C3, ports: {Np: e, Nn: GND}
name: Q, type: NPN, ports: {C: c, B: b, E: e}
]
extrainfo:The circuit is a common emitter (CE) amplifier. It uses an NPN transistor with a voltage source of 12V. The resistors R1 and R2 form a voltage divider biasing network. Capacitors C1, C2, and C3 are coupling and bypass capacitors. The output is taken from the collector of the transistor.
(a)
image_name:(b)
description:
[
name: Vi, type: VoltageSource, value: Vi, ports: {Np: vi, Nn: GND}
name: R1, type: Resistor, value: R1, ports: {N1: "vi", N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: "vi", N2: GND}
name: Rc, type: Resistor, value: Rc, ports: {N1: vo, N2: GND}
name: Q, type: NPN, ports: {C: vo, B: ', E: GND'}
]
extrainfo:The circuit is a single-supply common emitter amplifier. It uses an NPN transistor with a voltage source of 12V. Resistors R1 and R2 form a voltage divider biasing network. Capacitors are used for coupling and bypassing, and the output is taken from the collector of the transistor.
(b)
FIGURE 2.56 (a) Single-supply CE amplifier of Example 2.22 and (b) it ac equivalent.
#### Solution
(a) We have $g_{m}=0.99 / 26=38 \mathrm{~mA} / \mathrm{V}, r_{\pi}=100 \times 26 / 0.99=2.6 \mathrm{k} \Omega$, and $r_{o}=$ $100 / 0.99=101 \mathrm{k} \Omega$. Next, refer to the ac equivalent of Fig. $2.56 b$, where we observe that because of the bypass action by $C_{3}$, the emitter is at ac ground. By inspection, $R_{b}=r_{\pi}$ and $R_{c}=r_{o}$. Consequently,
$$
\begin{aligned}
R_{i} & =R_{1} / / R_{2} / / R_{b}=68 / / 47 / / 2.6=2.4 \mathrm{k} \Omega \\
R_{o} & =R_{C} / / R_{c}=3.9 / / 101=3.8 \mathrm{k} \Omega \\
a_{o c} & =-g_{m} R_{o}=-38 \times 3.8=-144 \mathrm{~V} / \mathrm{V}
\end{aligned}
$$
(b) Due to input and output loading, the gain drops to
$$
\frac{v_{o}}{v_{s i g}}=\frac{2.4}{1+2.4}(-144) \frac{18}{3.8+18}=-84 \mathrm{~V} / \mathrm{V}
$$
### Quick Estimates for the CE Configuration
In everyday practice the circuit designer often needs to come up with quick if rough estimates for the relevant parameters of a BJT amplifier. In light of the above derivations and examples, we draw the following conclusions for the CE configuration:
- $R_{i}$ is dominated by $r_{\pi}$
- $R_{o}$ is dominated by $R_{C}$
- $a_{o c}$ is approximately $-g_{m} R_{C}$
Using $g_{m}=I_{C} / V_{T}$ we can also write
$$
\begin{equation*}
a_{o c} \cong-\frac{R_{C} I_{C}}{V_{T}} \tag{2.77a}
\end{equation*}
$$
indicating that the unloaded gain magnitude of a CE amplifier is approximately the ratio of the voltage drop across $R_{C}$ to the thermal voltage $V_{T}$. For instance, in the splitsupply amplifier of Example 2.21, $R_{C}$ dropped approximately $V_{C C} / 2$, so Eq. (2.77a) gives the estimate $a_{o c} \cong-\left(V_{C C} / 2\right) / V_{T}=-(12 / 2) / 0.026=-230 \mathrm{~V} / \mathrm{V}$. Similarly, in the single-supply design of Example 2.22, where the BJT was biased according to the $1 / 3-1 / 3-1 / 3$ Rule, Eq. (2.77a) gives $a_{o c} \cong-\left(V_{C C} / 3\right) / V_{T}=-(12 / 3) / 0.026=$ $-160 \mathrm{~V} / \mathrm{V}$. Both estimates are in reasonable agreement with the respective examples, so keep Eq. $(2.77 a)$ in mind!
#### Exercise 2.2
Show that if we take also $r_{o}$ into account, then Eq. (2.77a) becomes
$$
\begin{equation*}
a_{o c}=-\frac{R_{C} I_{C}}{V_{T}\left(1+R_{C} I_{C} / V_{A}\right)} \tag{2.77b}
\end{equation*}
$$
### The Common-Emitter with Emitter-Degeneration (CE-ED) Configuration
The circuit of Fig. 2.57 is similar to that of Fig. 2.53, except for the presence of the unbypassed resistance $R_{E}$ in series with the emitter. To find the small-signal parameters, we turn to the ac equivalent of Fig. 2.58. Equation (2.62b) indicates that the presence of $R_{E}$ can raise $R_{c}$ considerably to the point of making $R_{c} \gg R_{C}$. In discrete designs this is usually the case, so we approximate $R_{o}=R_{C} / R_{c} \cong R_{C}$. In fact, to simplify the analysis and also help the beginner develop a quick feel for the circuit, it is customary to ignore $r_{o}$ altogether in discrete CE-ED circuits (though this is not necessarily the case with their IC counterparts, as we shall see in Chapter 4.) This allows us to make the approximations
$$
\begin{equation*}
R_{i}=R_{B} / / R_{b} \cong R_{B} / /\left[r_{\pi}+\left(\beta_{0}+1\right) R_{E}\right] \quad R_{o} \cong R_{C} \tag{2.78}
\end{equation*}
$$
Next we wish to derive an expression for $i_{c}$. With $r_{o}$ out of the way, Eq. (2.52) simplifies as $i_{c}=g_{m} v_{b e}$. With reference to the ac equivalent of Fig. 2.58, we have
$$
i_{c}=g_{m} v_{b e}=g_{m}\left(v_{b}-v_{e}\right)=g_{m}\left(v_{i}-R_{E} i_{e}\right) \cong g_{m}\left(v_{i}-R_{E} i_{c}\right)
$$
image_name:FIGURE 2.57 The common-emitter with emitter-degeneration (CE-ED) amplifier.
description:
[
name: Vsig, type: VoltageSource, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: vi}
name: C1, type: Capacitor, value: C1, ports: {Np: vi, Nn: b}
name: RB, type: Resistor, value: RB, ports: {N1: b, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VCC, N2: c}
name: C2, type: Capacitor, value: C2, ports: {Np: c, Nn: vo}
name: RL, type: Resistor, value: RL, ports: {N1: vo, N2: GND}
name: RE, type: Resistor, value: RE, ports: {N1: e1, N2: e}
name: C3, type: Capacitor, value: C3, ports: {Np: e, Nn: GND}
name: IE, type: CurrentSource, ports: {Np: e, Nn: VEE}
name: Q, type: NPN, ports: {C: c, B: b, E: e1}
]
extrainfo:The circuit is a common-emitter amplifier with emitter degeneration, which helps to stabilize the gain and increase linearity. The transistor Q is biased using resistor RB, and the emitter resistor RE provides negative feedback. Capacitors C1, C2, and C3 are used for coupling and bypassing.
FIGURE 2.57 The common-emitter with emitter-degeneration (CE-ED) amplifier.
having used the fact that $i_{e}=i_{c} / \alpha_{0} \cong i_{c}$. Collecting and solving for $i_{c}$ gives
$$
\begin{equation*}
i_{c}=G_{m} v_{i} \tag{2.79a}
\end{equation*}
$$
where
$$
\begin{equation*}
G_{m} \cong \frac{g_{m}}{1+g_{m} R_{E}} \tag{2.79b}
\end{equation*}
$$
We observe that with $R_{E}=0$ the entire signal $v_{i}$ appears across the B-E port, giving $G_{m}=g_{m}$. However, with $R_{E} \neq 0$, only a portion of $v_{i}$ appears across the B-E port,
image_name:FIGURE 2.58
description:
[
name: Rsig, type: Resistor, value: Rsig, ports: {N1: v_sig, N2: v_i}
name: RB, type: Resistor, value: RB, ports: {N1: v_i, N2: GND}
name: RC, type: Resistor, value: RC, ports: {N1: VDD, N2: v_o}
name: RE, type: Resistor, value: RE, ports: {N1: v_e, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: v_o, N2: GND}
name: v_sig, type: VoltageSource, value: v_sig, ports: {Np: v_sig, Nn: GND}
name: NPN, type: NPN, ports: {C: v_o, B: v_i, E: v_e}
]
extrainfo:The circuit is a CE-ED amplifier with emitter degeneration. The presence of RE provides negative feedback, reducing transconductance and stabilizing the amplifier.
FIGURE 2.58 Ac equivalent of the CE-ED amplifier of Fig. 2.57.
the rest being dropped across $R_{E}$. Consequently we have $G_{m}<g_{m}$, indicating a smaller response $i_{c}$ for the same $v_{i}$. This transconductance reduction is referred to as degeneration because $R_{E}$ provides a negative feedback function, as mentioned previously. Though this subject will be investigated systematically in Chapter 7, suffice it to say here that the presence of $R_{E}$, aptly called emitter-degeneration resistance, not only reduces the transconductance, but also raises the value of $R_{b}$, and hence the value of $R_{i}$, by Eq. (2.78).
To find the voltage gain, refer again to the ac equivalent of Fig. 2.58 and write Ohm's law,
$$
0-v_{o}=\left(R_{o} / / R_{L}\right) i_{c} \cong\left(R_{C} / / R_{L}\right) i_{c}=\left(R_{C} / / R_{L}\right) G_{m} v_{i}
$$
Letting $R_{L} \rightarrow \infty$ gives $v_{o} \cong-R_{C} G_{m} v_{i}$. But, according to Eq. (2.72a), the ratio $v_{o} / v_{i}$ in the limit $R_{L} \rightarrow \infty$ is the unloaded voltage gain, so
$$
\begin{equation*}
a_{o c} \cong-G_{m} R_{C} \cong-\frac{g_{m} R_{C}}{1+g_{m} R_{E}} \tag{2.80}
\end{equation*}
$$
Comparing with Eq. (2.76) we note that the presence of the degeneration resistance $R_{E}$ causes $a_{o c}$ to drop by about $\left(1+g_{m} R_{E}\right.$ ). Rewriting Eq. (2.80) in the alternative form
$$
\begin{equation*}
a_{o c} \cong-\frac{R_{C}}{1 / g_{m}+R_{E}} \cong-\frac{R_{C}}{r_{e}+R_{E}} \tag{2.81a}
\end{equation*}
$$
provides us with a useful rule of thumb for a quick estimation of the gain of the CE-ED configuration:
The unloaded voltage gain from base to collector is the (negative of the) ratio of the total collector resistance to the total emitter resistance
We observe that if $g_{m} R_{E} \gg 1$ (or, equivalently, if $R_{E} \gg 1 / g_{m}$ ), then
$$
\begin{equation*}
a_{o c} \cong-\frac{R_{C}}{R_{E}} \tag{2.81b}
\end{equation*}
$$
indicating that the gain becomes independent of $g_{m}$ and thus of the biasing conditions of the BJT-an important advantage of emitter degeneration! Having obtained expressions for $R_{i}, R_{o}$, and $a_{o c}$, we finally apply Eq. (2.73) to find the signal-to-load gain.
(a) Investigate the effect of inserting an emitter-degeneration resistance $R_{E}=$ circuit of Fig. 2.57a.
(b) Find $R_{E}$ for an unloaded gain of $-10 \mathrm{~V} / \mathrm{V}$.
#### Solution
(a) All dc voltages and dc current remain the same, and so do $g_{m}(=38 \mathrm{~mA} / \mathrm{V})$ and $r_{\pi}$ $(=3.9 \mathrm{k} \Omega)$. The insertion of $R_{E}=220 \Omega$ in the circuit has the following effects:
- $R_{b}$ increases from $3.9 \mathrm{k} \Omega$ to $[3.9+(150+1) 0.22]=37 \mathrm{k} \Omega$ (almost a tenfold increase!)
- $R_{i}$ increases from $3.7 \mathrm{k} \Omega$ to $75 / / 37=25 \mathrm{k} \Omega$ (a desirable affect)
- $a_{o c}$ drops (or degenerates) from $-223 \mathrm{~V} / \mathrm{V}$ to $-[6,200 /(26+220)]=$ $-25 \mathrm{~V} / \mathrm{V}$
Using Eq. (2.73) we find that $v_{o}$ drops to
$$
\begin{aligned}
v_{o} & =\left[\frac{25}{0.5+25}(-25) \frac{30}{6.2+30}\right] v_{\text {sig }}=-20 v_{\text {sig }}=-20(5 \mathrm{mV}) \cos \omega t \\
& =(100 \mathrm{mV}) \cos \left(\omega t-180^{\circ}\right)
\end{aligned}
$$
(b) Use Eq. (2.80) to impose $-6,200 /\left(26+R_{E}\right)=-10$. This yields $R_{E}=594 \Omega$.
### Summary for the CE-ED Configuration
We summarize the effects of the emitter-degeneration resistance $R_{E}$ as follows:
- The transconductance $g_{m}$ as well as the unloaded gain $a_{o c}$ are reduced by the amount $\left(1+g_{m} R_{E}\right)$.
- $R_{b}$ is raised from $r_{\pi}$ to $r_{\pi}+\left(\beta_{0}+1\right) R_{E} \cong r_{\pi}\left(1+g_{m} R_{E}\right)$, that is, it is increased by the amount $\left(1+g_{m} R_{E}\right)$.
- The input signal range is raised to $v_{i}=v_{b e}+v_{e}=v_{b e}+R_{E} i_{e} \cong v_{b e}+R_{E} i_{c}=$ $v_{b e}\left(1+g_{m} R_{E}\right)$, that is, it is increased by the amount $\left(1+g_{m} R_{E}\right)$, thus widening the range of applicability of the small-signal approximation.
- The signal-to-load gain is less dependent on $\beta_{0}$ and $I_{C}$, and is established by external resistance ratios.
Though gain reduction may be undesirable in certain situations, all other effects are generally welcome, and as such they are often exploited on purpose by the designer to optimize the circuit at hand (in Chapter 6 we will see another important effect of degeneration, namely, faster frequency/time responses).
### Capacitance Selection
To complete our understanding of discrete BJT amplifiers we need to address the issue on how to go about selecting the various capacitances involved in discrete design. As the signal source is turned on, we want each capacitance $C$ to act as an ac short at the source's frequency $f_{\text {sig. }}$. Physically, this requires that we select $C$ large enough so as to prevent it from charging/discharging appreciably in response to the ac alternations of $v_{s i g}$.
As we know, the impedance presented by a capacitance $C$ at the signal frequency $f_{s i g}$ is $Z_{C}\left(j f_{s i g}\right)=1 /\left(j 2 \pi f_{s i g}\right)$. For this capacitance to act effectively as an ac short at $f_{s i g}$, its impedance must be such that
$$
\left|Z_{C}\left(j f_{s i g}\right)\right| \ll R_{e q}
$$
where $R_{e q}$ is the equivalent resistance seen by $C$. This condition is readily rephrased in terms of $C$ as
$$
\begin{equation*}
C \gg \frac{1}{2 \pi R_{e q} f_{s i g}} \tag{2.82}
\end{equation*}
$$
If the circuit is designed to operate over a range of signal frequencies, then we must use the lowest frequency in the above condition, that is, $f_{\text {sig(min) }}$.
Specify suitable capacitances in the CE amplifier of Example 2.21 for operation over the audio range.
#### Solution
The audio range extends from 20 Hz to 20 kHz , so $f_{\text {sig(min) }}=20 \mathrm{~Hz}$.
- For $C_{1}$ we have $R_{e q 1}=R_{s i g}+R_{i}=0.5+3.7=4.2 \mathrm{k} \Omega$, so we need $C_{1} \gg$ $1 /\left[2 \pi \times 4.2 \times 10^{3} \times 20\right) \cong 2.0 \mu \mathrm{~F}$.
- For $C_{2}$ we have $R_{e q 2}=R_{\mathrm{o}}+R_{L}=5.8+30=35.8 \mathrm{k} \Omega$, so impose $C_{2} \gg$ $1 /\left[2 \pi \times 35.8 \times 10^{3} \times 20\right) \cong 0.22 \mu \mathrm{~F}$.
- For $C_{3}$ we adapt Eq. (2.59a) to the present case and write
$$
\begin{aligned}
& \quad R_{e q 3} \cong \frac{\left(R_{s i g} / / R_{B}\right)+r_{\pi}}{\beta_{0}+1}=\frac{(0.5 / / 75)+3.9}{150+1}=29 \Omega \\
& \text { so impose } C_{3} \gg 1 /[2 \pi \times 29 \times 20) \cong 275 \mu \mathrm{~F}
\end{aligned}
$$
A reasonable way to go is to use standard capacitance values that exceed the calculated lower limits by an order of magnitude or more. Thus, use $C_{1}=22 \mu \mathrm{~F}$, $C_{2}=2.2 \mu \mathrm{~F}$, and $C_{3}=2.7 \mathrm{mF}$. Since it sees a very small equivalent resistance, $C_{3}$ comes out quite large. To save on size, it is common to compromise and use a smaller value, such as $330 \mu \mathrm{~F}$ in the present case.
### PSpice Simulation
The circuits discussed herein can readily be verified via PSpice (see Appendix 2A). The student can either make up ad-hoc BJT models, or use the device models available in the library that comes with the Student Version of PSpice, such as the popular 2N2222 npn BJT. Figure 2.59 shows a PSpice circuit to simulate the CE amplifier of Example 2.22, but using a 2N2222 BJT. All relevant waveforms are displayed in Fig. 2.60.
As seen, the input signal $v_{s i g}$ is a $1-\mathrm{kHz}$ sine wave with $\pm 5-\mathrm{mV}$ peak values. The waveform $v_{B}$ at the base is still a sine wave with peak values of almost $\pm 5-\mathrm{mV}$, but with a dc component $V_{B}=4.717 \mathrm{~V}$ as established by the dc biassing resistances $R_{1}$ and $R_{2}$. The waveform $v_{E}$ at the emitter has a dc component $V_{E}=4.072 \mathrm{~V}$, about $0.7-\mathrm{V}$ lower than $V_{B}$. We note also a small ac component $v_{e}$. Ideally, $v_{e}$ should be zero (perfect ac ground at the emitter), but this would require $C_{2} \rightarrow \infty$. In practice we specify $C_{2}$ to be large enough to ensure $\left|v_{e}\right| \ll\left|v_{b}\right|$. Finally, we note that the waveform $v_{C}$ at the collector has a dc component $V_{C}=7.968$ and an ac component $v_{c}$ which is a
image_name:FIGURE 2.59
description:
[
name: Vsig, type: VoltageSource, value: VAMPL = 5mV, FREQ = 1kHz, ports: {Np: Vsig, Nn: GND}
name: R1, type: Resistor, value: 68kΩ, ports: {N1: VCC, N2: B}
name: R2, type: Resistor, value: 47kΩ, ports: {N1: B, N2: GND}
name: RC, type: Resistor, value: 3.9kΩ, ports: {N1: VCC, N2: VC}
name: RE, type: Resistor, value: 3.9kΩ, ports: {N1: E, N2: GND}
name: C1, type: Capacitor, value: 10µF, ports: {Np: Vsig, Nn: B}
name: C2, type: Capacitor, value: 220µF, ports: {Np: E, Nn: GND}
name: Q, type: NPN, ports: {C: VC, B: B, E: E}
name: VCC, type: VoltageSource, value: 12V, ports: {Np: VCC, Nn: GND}
]
extrainfo:The circuit is a common-emitter (CE) amplifier using an NPN transistor (Q2N2222). The input signal is amplified with a gain of approximately -147.2 V/V, with the output inverted and slightly distorted. The DC biasing ensures the transistor operates in the active region.
FIGURE 2.59 PSpice circuit to display the waveforms of a
CE amplifier.
magnified version of the input $v_{s i g}$, but shifted by $180^{\circ}$. Its peak-to-peak amplitude is $(8.659-7187)=1.472 \mathrm{~V}$. Since the peak-to-peak amplitude of the input is 10 mV , the gain is $-1.472 / 0.010=-147.2 \mathrm{~V} / \mathrm{V}$, which is in reasonable agreement with the value of $-144 \mathrm{~V} / \mathrm{V}$ predicted in Example 2.22. In practice the output waveform is slightly distorted, though imperceptibly so in the present case, because of the nonlinear (exponential) BJT characteristic. In fact, one can verify that its average value is not exactly halfway between its peaks. Consequently, the calculations of Example 2.22, based on the small-signal approximation, are bound to be in slight disagreement with the more dependable results provided by computer simulation or actual lab measurements.
image_name:v_sig
description:The graph titled 'v_sig' is a time-domain waveform plot displaying the signal voltage over time. The x-axis represents time in milliseconds (ms), ranging from 0 to 2 ms, while the y-axis represents voltage in millivolts (mV), ranging from -5 mV to 5 mV.
1. **Type of Graph and Function:**
- The graph is a time-domain waveform plot showing the signal voltage, labeled as 'v_sig'.
2. **Axes Labels and Units:**
- **X-axis:** Time (ms)
- **Y-axis:** Voltage (mV)
- The scale is linear, and the graph includes gridlines at regular intervals to aid in reading values.
3. **Overall Behavior and Trends:**
- The waveform is sinusoidal, showing periodic oscillations with a consistent frequency over the plotted time period.
- The signal completes two full cycles within the 2 ms timeframe, indicating a frequency of approximately 1 kHz.
4. **Key Features and Technical Details:**
- The waveform peaks at approximately 5 mV and troughs at -5 mV, indicating an amplitude of 5 mV.
- There are zero crossings at approximately 0.25 ms, 0.75 ms, 1.25 ms, and 1.75 ms.
- The waveform is symmetric about the time axis, suggesting no DC offset.
5. **Annotations and Specific Data Points:**
- The graph is annotated with the label 'v_sig' to identify the waveform.
- No specific numerical values or reference lines are provided beyond the general gridlines and axis labels.
image_name:v_B
description:The graph labeled "v_B" is a time-domain waveform plot illustrating the voltage at the base of a transistor in a common-emitter amplifier configuration. The x-axis represents time in milliseconds (ms), ranging from 0 to 2 ms, while the y-axis represents voltage in volts (V), specifically ranging from approximately 4.712 V to 4.722 V.
Overall Behavior and Trends:
The waveform is sinusoidal, indicating an AC signal superimposed on a DC bias. The waveform has a periodic nature, repeating every 1 ms, which suggests a frequency of 1 kHz. The amplitude of the waveform is relatively small, with peak-to-peak variations around 0.01 V.
Key Features and Technical Details:
- **Peaks and Valleys:** The waveform reaches its maximum value slightly above 4.722 V and its minimum value slightly below 4.712 V.
- **Zero Crossings:** There are no true zero crossings in this waveform, as it is offset by a DC bias.
- **Periodic Behavior:** The waveform completes a full cycle every 1 ms, confirming its periodic nature.
Annotations and Specific Data Points:
The graph is annotated with the label "v_B" indicating it measures the base voltage of the transistor. There are no additional markers or reference lines in this specific plot. The waveform’s periodicity and amplitude are consistent with typical small-signal analysis for a transistor amplifier, where the AC component is superimposed on a DC level.
image_name:v_E
description:The graph labeled "v_E" is a time-domain waveform plot, representing the voltage across the emitter in a common-emitter amplifier configuration.
1. **Axes Labels and Units:**
- The horizontal axis represents time, measured in milliseconds (ms), spanning from 0 to 2 ms.
- The vertical axis represents voltage, measured in volts (V), with a range from approximately 4.065 V to 4.079 V.
2. **Overall Behavior and Trends:**
- The waveform is a sinusoidal signal with a very small amplitude, indicating slight oscillations around a DC offset.
- The waveform appears relatively flat, indicating minimal variation in the emitter voltage, which is characteristic of a common-collector configuration where the output closely follows the input signal.
3. **Key Features and Technical Details:**
- The waveform's peaks and valleys are not prominently distinct due to the small amplitude of oscillation.
- The average value of the waveform is not centered between its peaks, reflecting a slight distortion due to the nonlinear characteristics of the BJT.
4. **Annotations and Specific Data Points:**
- The plot includes an annotation labeled "v_E," indicating the specific voltage being measured.
- There are no additional markers or reference lines on this specific plot.
This graph is part of a set of waveforms that likely depict different points in the amplifier circuit, providing insight into the operation and performance of the common-emitter amplifier.
image_name:v_C
description:The graph labeled **v_C** is a time-domain waveform plot, depicting the voltage across the collector of a transistor in a common emitter amplifier configuration.
1. **Axes Labels and Units:**
- The horizontal axis represents time in milliseconds (ms), ranging from 0 to 2 ms.
- The vertical axis represents the voltage v_C in volts (V), with values ranging approximately from 7.187 V to 8.659 V.
2. **Overall Behavior and Trends:**
- The waveform exhibits a periodic sinusoidal shape, indicating an AC signal superimposed on a DC offset.
- The waveform oscillates between a minimum of around 7.187 V and a maximum of approximately 8.659 V.
- There is a noticeable DC offset, centering the waveform around a mean value, which is not exactly halfway between the peaks, suggesting slight distortion due to non-linearities in the transistor's characteristics.
3. **Key Features and Technical Details:**
- The waveform shows clear periodicity with a regular sinusoidal pattern, consistent with the expected output of an amplifier responding to an AC input.
- The peaks and troughs occur symmetrically, indicating the waveform maintains a consistent frequency throughout the observed period.
4. **Annotations and Specific Data Points:**
- The waveform is annotated with the label v_C, identifying it as the collector voltage.
- The time intervals are marked with gridlines at 0.5 ms intervals, aiding in the visualization of the waveform's periodicity.
Overall, the graph provides a clear visualization of the collector voltage in a CE amplifier, highlighting the sinusoidal nature of the signal and the impact of the transistor's characteristics on the waveform's symmetry and offset.
FIGURE 2.60 Probe plots of the waveforms of the CE amplifier of Fig. 2.59.
## 2.9 BIPOLAR VOLTAGE AND CURRENT BUFFERS
In this section we examine the two remaining single-transistor amplifier configurations of interest, namely, the common collector and the common base configurations. As we shall see, these configurations find application as voltage buffers and current buffers, respectively.
### The Common Collector (CC) Configuration
The common-collector (CC) amplifier receives the input at the base and delivers the output from the emitter. In the circuit realization of Fig. 2.61 $a$ we have chosen to drive the base directly from the signal source so that we can focus on the bare essentials of the circuit. Turning to its ac equivalent of Fig. $2.61 b$ we note that it is identical to that of Fig. 2.42, so we just recycle the results developed there, provided we suitably re-label the resistances.
The input resistance in Fig. $2.61 b$ is simply $R_{b}$ as given in Eq. (2.58b), but with $R_{E} \rightarrow R_{L}$,
$$
\begin{equation*}
R_{i}=r_{\pi}+\left(\beta_{0}+1\right)\left(R_{L} / / r_{o}\right) \tag{2.83}
\end{equation*}
$$
This resistance is usually large, thanks to the magnifying effect by $\beta_{0}$. The output resistance in Fig. $2.61 b$ is simply $R_{e}$ as given in Eq. (2.59b), but with $R_{B} \rightarrow R_{s i g}$,
$$
\begin{equation*}
R_{o}=\left(\frac{R_{s i g}+r_{\pi}}{\beta_{0}+1}\right) / / r_{o} \tag{2.84}
\end{equation*}
$$
This resistance is usually small, thanks to the presence of $\beta_{0}$ in the denominator. Just like Eq. (2.83) reveals that $R_{i}$ is a function of $R_{L}$, Eq. (2.84) reveals that $R_{o}$ is a function of $R_{s i g}$. As mentioned, an amplifier exhibiting this interdependence is said to be a non-unilateral amplifier.
To find the voltage gain, we observe that if we replace the BJT with its small-signal model and look into its base, we see $r_{\pi}$ followed by the trio $\beta_{0} i_{b}, R_{L}$, and $r_{o}$. In light of
image_name:(a)
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: vi}
name: Q, type: NPN, ports: {C: VCC, B: vi, E: E}
name: C2, type: Capacitor, value: C2, ports: {Np: E, Nn: vo}
name: IE, type: CurrentSource, value: IE, ports: {Np: E, Nn: VEE}
name: RL, type: Resistor, value: RL, ports: {N1: vo, N2: GND}
]
extrainfo:The circuit is a common-collector (CC) amplifier configuration. It uses an NPN transistor with a voltage source Vsig providing the input signal through Rsig. The output is taken across the load resistor RL. Capacitor C2 is used for coupling the output signal, and the current source IE provides biasing for the transistor.
image_name:(b)
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: vi}
name: Q, type: NPN, ports: {C: GND, B: vi, E: vo}
name: RL, type: Resistor, value: RL, ports: {N1: vo, N2: GND}
]
extrainfo:The circuit is a common-collector (CC) amplifier configuration using an NPN transistor. The input signal is applied through Rsig and Ri to the base of the transistor. The output is taken from the emitter, which is connected to the load RL. The circuit is designed for impedance matching, providing a high input impedance and low output impedance.
FIGURE 2.61 The common-collector (CC) amplifier, and it ac equivalent.
image_name:(a)
description:
[
name: Rsig, type: Resistor, value: Rsig, ports: {N1: v_sig, N2: B}
name: rπ, type: Resistor, value: rπ, ports: {N1: B, N2: E}
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: v_sig, Nn: GND}
name: ro, type: Resistor, value: ro, ports: {N1: E, N2: vo}
]
extrainfo:The circuit is a common-collector (CC) amplifier configuration using an NPN transistor. The input signal is applied through Rsig and Ri to the base of the transistor. The output is taken from the emitter, which is connected to the load RL. The circuit is designed for impedance matching, providing a high input impedance and low output impedance.
image_name:(b)
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: vo}
name: ro, type: Resistor, value: ro, ports: {N1: vo, N2: E(vo)}
name: RL, type: Resistor, value: RL, ports: {N1: vo, N2: GND}
]
extrainfo:The circuit in diagram (b) represents the small-signal equivalent of a common-collector amplifier as seen by the load. It includes a voltage source Vsig, a series resistance Rsig, and resistors ro, Ro, and RL. The output is taken across RL, and the configuration is designed for impedance matching, providing a high input impedance and low output impedance.
FIGURE 2.62 Small-signal equivalents of the CC amplifier of Fig. 2.61 as seen (a) by the source and (b) as seen by the load.
Eq. (2.83), it is comforting to realize that we can lump these three elements together and treat them as a single equivalent resistance of value $\left(\beta_{0}+1\right) \times\left(R_{L} / / r_{o}\right)$. This is precisely what has been done in Fig. 2.62a, which shows the equivalent ac circuit as seen by the signal source. Using the voltage divider rule, we find the signal-to-load gain to be
$$
\begin{equation*}
\frac{v_{o}}{v_{s i g}}=\frac{\left(\beta_{0}+1\right)\left(R_{L} / / r_{o}\right)}{R_{s i g}+r_{\pi}+\left(\beta_{0}+1\right)\left(R_{L} / / r_{o}\right)} \tag{2.85a}
\end{equation*}
$$
Dividing numerator and denominator by $\left(\beta_{0}+1\right)$ yields an insightful alternative expression for the signal-to-load gain,
$$
\begin{equation*}
\frac{v_{o}}{v_{s i g}}=\frac{R_{L} / / r_{o}}{\frac{R_{s i g}+r_{\pi}}{\beta_{0}+1}+\left(R_{L} / / r_{o}\right)} \tag{2.85b}
\end{equation*}
$$
Viewing this expression as a voltage divider rule, we can readily draw the circuit originating it. Shown in Fig. 2.62b, this is the equivalent ac circuit as seen by the load. These alternative equivalents ought to help the reader develop a better feel for this intriguing circuit. As mentioned, a CC amplifier provides high input resistance and low output resistance.
To investigate the gain more closely, we divide numerator and denominator by the numerator itself in the right-hand side of Eq. (2.85) and obtain yet another insightful alternative
$$
\begin{equation*}
\frac{v_{o}}{v_{s i g}}=\frac{1}{1+\frac{R_{s i g}+r_{\pi}}{\left(\beta_{0}+1\right)\left(R_{L} / / r_{o}\right)}} \tag{2.86}
\end{equation*}
$$
Voltage gain is less than unity, though generally quite close to unity because $\beta_{0}$ is large. For this reason the CC amplifier is also called a voltage follower. (The ac voltage at the emitter simply follows the ac voltage at the base, though the total emitter voltage is offset by about -0.7 V relative to that at the base.) In accordance with
Eq. (2.72b), we readily find the unloaded gain $a_{o c}$ by letting $R_{s i g} \rightarrow 0$ and $R_{L} \rightarrow \infty$ in Eq (2.86). The result is
$$
\begin{equation*}
a_{o c} \cong \frac{1}{1+1 /\left(g_{m} r_{o}\right)}=\frac{1}{1+V_{T} / V_{A}} \tag{2.87}
\end{equation*}
$$
a value extremely close to unity. We conclude with the following observations:
- Even though not much of a winner as a voltage amplifier, the CC configuration offers the advantages of potentially high input resistance and low output resistance, which make it a good voltage buffer. Ideally, a voltage buffer has,
$$
\begin{equation*}
R_{i} \rightarrow \infty \quad R_{o} \rightarrow 0 \quad \frac{v_{o}}{v_{s i g}} \rightarrow 1 \mathrm{~V} / \mathrm{V} \tag{2.88}
\end{equation*}
$$
Even though the CC configuration is only an approximation of the ideal voltage buffer, it is widely used to reduce inter-stage loading. For instance, preceding a CE amplifier by a voltage buffer can provide a much higher input resistance at the price of a negligible reduction in the overall gain, just like following it by a buffer can result in a much lower output resistance.
- The CC amplifier can also be viewed as a current amplifier that accepts the ac current $i_{b}$ at the base and delivers the ac current $i_{e}$ at the emitter with the gain
$$
\begin{equation*}
\frac{i_{e}}{i_{b}}=\beta_{0}+1 \tag{2.89}
\end{equation*}
$$
When used in this capacity, the CC configuration provides power amplification and finds application as the output stage of power-handling circuits such as dc power supplies and audio power amplifiers.
(a) In the circuit of Fig. 2.61a, let $V_{C C}=-V_{E E}=12 \mathrm{~V}$ and $I_{E}=1 \mathrm{~mA}$, and let the BJT have $\beta_{0}=\beta_{F}=150, V_{B E(\mathrm{~m})}=0.7 \mathrm{~V}$, and $V_{A}=80 \mathrm{~V}$. If $R_{s i g}=47 \mathrm{k} \Omega$, $R_{L}=10 \mathrm{k} \Omega$, and
$$
v_{s i g}=0 \mathrm{~V}+(2.0 \mathrm{~V}) \cos \omega t
$$
find all node voltages in the circuit, and express each of them as the sum of the dc and ac components, in the manner of Eq. (2.43). Show them explicitly in the circuit.
(b) Check that the BJT satisfies the small-signal approximation condition of Eq. (2.51).
#### Solution
(a) The dc conditions of the circuit are
$$
V_{B}=0-47 \frac{1}{151} \cong-0.3 \mathrm{~V} \quad V_{E} \cong-0.3-0.7=-1.0 \mathrm{~V}
$$
image_name:FIGURE 2.63
description:
[
name: Q, type: NPN, ports: {C: 12 V, B: b, E: e}
name: 47 kΩ, type: Resistor, value: 47 kΩ, ports: {N1: Vi, N2: b}
name: 10 kΩ, type: Resistor, value: 10 kΩ, ports: {N1: vo, N2: GND}
name: C2, type: Capacitor, value: C2, ports: {Np: e, Nn: vo}
name: (2V)cosωt, type: VoltageSource, value: (2V)cosωt, ports: {Np: vi, Nn: GND}
name: 1 mA, type: CurrentSource, value: 1 mA, ports: {Np: -1.0 V + (1.927 V)cos ωt, Nn: -12 V}
]
extrainfo:The circuit involves a BJT transistor with a small-signal model, including resistors, capacitors, and sources. Node voltages are expressed as sums of DC and AC components.
FIGURE 2.63 Circuit of Example 2.25, with each node voltage expressed as the sum of its $d c$ and ac components.
Moreover, $I_{C} \cong I_{E}=1 \mathrm{~mA}, r_{\pi} \cong 150 \times 26 / 1=3.9 \mathrm{k} \Omega$ and $r_{o} \cong 80 / 1=$ $80 \mathrm{k} \Omega$. So, Eqs. (2.83) and (2.84) give
$$
\begin{aligned}
& R_{i}=3.9+(150+1)(10 / / 80) \cong 1.35 \mathrm{M} \Omega(\text { high }) \\
& R_{o}=\frac{47+3.9}{150+1} / / 80=0.336 \mathrm{k} \Omega(\text { low })
\end{aligned}
$$
By Eq. (2.86),
$$
v_{o}=\frac{1}{1+\frac{47+3.9}{(150+1)(10 / / 80)}} v_{\text {sig }}=0.963 v_{s i g}=(1.927 \mathrm{~V}) \cos \omega t
$$
Also,
$$
v_{i}=\frac{R_{i}}{R_{s i g}+R_{i}} v_{s i g}=\frac{1.35}{0.047+1.35} v_{s i g}=(1.933 \mathrm{~V}) \cos \omega t
$$
The node voltages are shown in Fig. 2.63. The reader is encouraged to verify each of them in detail.
(b) For the BJT we have $v_{b e}=v_{i}-v_{o} \cong(6 \mathrm{mV}) \cos \omega t$, indicating a peak value close to the $5-\mathrm{mV}$ limit agreed upon in Eq. (2.51). The CC amplifier's ability to handle in fairly linear fashion external signals that are not strictly of the small-signal type stems from the negative feedback action provided by the emitter resistance, in this case $R_{L}$. As previously noted in the CE-ED case, the presence of $R_{L}$ increases the input signal range by the factor $\left(1+g_{m} R_{L}\right)=$ $(1+10,000 / 26)=386$ !
EXAMPLE 2.26 Figure 2.64 shows a single-supply emitter follower. As we know, $R_{1}$ and $R_{2}$ bias the base, and $R_{E}$ sets the emitter current bias. Assuming $\beta_{0}=\beta_{F}=100, V_{B E(\text { on })}=$ 0.7 V , and $V_{A}=75 \mathrm{~V}$, find the small-signal resistances $R_{i}$ and $R_{o}$, as well as the signal-to-load gain.
image_name:FIGURE 2.64
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: 1 kΩ, ports: {N1: Vsig, N2: vi}
name: R1, type: Resistor, value: 18 kΩ, ports: {N1: VDD, N2: b}
name: R2, type: Resistor, value: 47 kΩ, ports: {N1: b, N2: GND}
name: RE, type: Resistor, value: 2.0 kΩ, ports: {N1: e, N2: GND}
name: RL, type: Resistor, value: 1 kΩ, ports: {N1: vo, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: vi, Nn: b}
name: C2, type: Capacitor, value: C2, ports: {Np: e, Nn: vo}
name: Q, type: NPN, ports: {C: VDD, B: b, E: e}
]
extrainfo:The circuit is a single-supply emitter follower with resistors R1 and R2 biasing the base of the transistor Q, and RE setting the emitter current bias. The circuit is powered by a 10V supply.
FIGURE 2.64 Single-supply emitter follower of Example 2.26.
#### Solution
Proceeding in the now familiar manner we find $I_{C}=3 \mathrm{~mA}$. Consequently, $r_{\pi}=$ $100(26 / 3)=0.87 \mathrm{k} \Omega$ and $r_{o}=75 / 3=25 \mathrm{k} \Omega$. With reference to the ac equivalent of Fig. 2.65a, we adapt Eq. (2.58) to write
$$
R_{b}=r_{\pi}+\left(\beta_{0}+1\right)\left(R_{E} / / r_{o} / / R_{L}\right)=0.87+101(2 / / 25 / / 1)=66 \mathrm{k} \Omega
$$
and
$$
R_{i}=R_{1} / / R_{2} / / R_{b}=18 / / 47 / / 66=11 \mathrm{k} \Omega
$$
image_name:(a)
description:
[
name: Vsig, type: VoltageSource, value: Vsig, ports: {Np: Vsig, Nn: GND}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vsig, N2: vi}
name: Ri, type: Resistor, value: Ri, ports: {N1: vi, N2: GND}
name: R1, type: Resistor, value: R1, ports: {N1: vi, N2: GND}
name: R2, type: Resistor, value: R2, ports: {N1: vi, N2: GND}
name: Q, type: NPN, ports: {C: GND, B: vi, E: vo}
name: Re, type: Resistor, value: Re, ports: {N1: vo, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: vo, N2: GND}
]
extrainfo:This circuit is an AC equivalent model of a transistor amplifier. It includes a voltage source, several resistors, and an NPN transistor in a common emitter configuration. The resistors Rsig, Ri, R1, R2, Rb, Re, Ro, and RL form the biasing and load network. The transistor Q amplifies the input signal applied to its base.
image_name:(b)
description:
[
name: Vsig, type: VoltageSource, ports: {Np: Vsig, Nn: GND}
name: RB, type: Resistor, value: RB, ports: {N1: X, N2: b1}
name: Re, type: Resistor, value: Re, ports: {N1: vo, N2: GND}
name: Q1, type: NPN, ports: {C: GND, B: b1, E: vo}
]
extrainfo:The circuit is a reduced AC equivalent of a transistor amplifier. It includes a voltage source, resistors for input and biasing, and an NPN transistor for amplification.
FIGURE 2.65 (a) Ac equivalent of the circuit of Fig. 2.64, and (b) the same after further reduction.
The equivalent resistance seen looking towards the left of the base is
$$
R_{B}=R_{s i g} / / R_{1} / / R_{2}=1 / / 18 / / 47=0.93 \mathrm{k} \Omega
$$
so, we adapt Eq. (2.59b) to write
$$
R_{e}=\frac{R_{B}+r_{\pi}}{\beta_{0}+1} / / r_{o}=\frac{0.93+0.87}{101} / / 25 \cong 0.018 \mathrm{k} \Omega=18 \Omega
$$
and
$$
R_{o}=R_{E} / / R_{e}=2000 / / 18 \cong 18 \Omega \text { (very low) }
$$
To find the signal-to-load gain, we apply Thévenin's theorem to the input network to obtain the equivalent of Fig. 2.65b. Finally, we apply Eq. (2.86) to write
$$
v_{o}=\frac{1}{1+\frac{R_{B}+r_{\pi}}{\left(\beta_{0}+1\right)\left(R_{E} / / R_{L} / / r_{o}\right)}} \times \frac{R_{\mathrm{l}} / / R_{2}}{R_{s i g}+\left(R_{1} / / R_{2}\right)} v_{s i g}=0.90 v_{s i g}
$$
indicating that the signal-to-load gain is $0.90 \mathrm{~V} / \mathrm{V}$.
EXAMPLE 2.27 Figure 2.66 shows how we can utilize a CC stage to lower the output resistance presented by the CE amplifier of Fig. 2.56. Assuming $Q_{2}$ is similar to $Q_{1}\left(\beta_{0}=\right.$ $\beta_{F}=100, V_{B E(\text { on })}=0.7 \mathrm{~V}$, and $V_{A}=100 \mathrm{~V}$ ), find the small-signal parameters $R_{i}$, $R_{o}$, and $a_{o c}=v_{o} / v_{i}$ for the overall circuit. Comment on your results.
image_name:Figure 2.66
description:
[
name: R1, type: Resistor, value: 68kΩ, ports: {N1: VCC, N2: b1}
name: R2, type: Resistor, value: 47kΩ, ports: {N1: b1, N2: e1}
name: R3, type: Resistor, value: 3.9kΩ, ports: {N1: VCC, N2: c1b2}
name: R4, type: Resistor, value: 3.9kΩ, ports: {N1: e1, N2: GND}
name: R5, type: Resistor, value: 4.3kΩ, ports: {N1: e2, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: vi, Nn: b1}
name: C2, type: Capacitor, value: C2, ports: {Np: e2, Nn: vo}
name: C3, type: Capacitor, value: C3, ports: {Np: e1, Nn: GND}
name: Q1, type: NPN, ports: {C: c1b2, B: b1, E: e1}
name: Q2, type: NPN, ports: {C: VCC, B: c1b2, E: e2}
]
extrainfo:The circuit is a CE-CC amplifier configuration with Q1 as the common emitter and Q2 as the common collector. It is designed to lower the output resistance presented by the CE amplifier.
FIGURE 2.66 CE-CC circuit of Example 2.27.
#### Solution
Proceed along the lines of Example 2.8, analyzing one stage at a time. For dc analysis, replace the CE stage with its $d c$ Thévenin equivalent as in Fig. 2.67a. Recall from previous analysis that $I_{C 1}=0.99 \mathrm{~mA}$, so the CE stage provides the open-circuit dc voltage $V_{C 1}=V_{C C}-R_{3} I_{C 1}=12-3.9 \times 0.99=8.1 \mathrm{~V}$ with the equivalent series resistance $R_{e q}=R_{3}=3.9 \mathrm{k} \Omega$. Adapting Eq. (2.32) with $V_{B B}=$ $V_{C 1}=8.1 \mathrm{~V}$ we get
$$
I_{C 2}=100 \frac{8.1-0.7}{3.9+101 \times 4.3}=1.7 \mathrm{~mA}
$$
image_name:(a)
description:
[
name: R3, type: Resistor, value: 3.9kΩ, ports: {N1: b2, N2: VC1}
name: R5, type: Resistor, value: 4.3kΩ, ports: {N1: GND, N2: e2}
name: Q2, type: NPN, ports: {C: VDC(12V), B: b2, E: e2}
name: VC1, type: VoltageSource, value: 8.1V, ports: {Np: VC1, Nn: GND}
name: VDD, type: VoltageSource, value: 12V, ports: {Np: VDD(12V), Nn: GND}
]
extrainfo:The circuit is a DC equivalent of a CE stage with an NPN transistor Q2. The transistor is biased with a 12V supply and an 8.1V source, with resistors R3 and R5 setting the biasing and load conditions. The collector current IC2 is calculated to be 1.7 mA.
image_name:(b)
description:
[
name: R5, type: Resistor, value: 4.3 kΩ, ports: {N1: e2, N2: GND}
name: Q2, type: NPN, ports: {C: GND, B: b2, E: e2}
name: Ro1, type: Resistor, value: 3.8 kΩ, ports: {N1: Va, N2: b2}
name: Vo1, type: VoltageSource, value: -144vi, ports: {Np: Va, Nn: GND}
]
extrainfo:This circuit is a CE-CC amplifier stage used for AC signal amplification. The NPN transistor Q2 is configured with a collector resistor Ro1 and an emitter resistor R5. The input voltage is amplified by the voltage source Vo1 with a gain of -144.
FIGURE 2.67 (a) Dc and (b) ac equivalents of the CE-CC circuit of Fig. 2.66.
Consequently, $r_{\pi 2}=100(26 / 1.7)=1.5 \mathrm{k} \Omega$ and $r_{o 2}=100 / 1.7=59 \mathrm{k} \Omega$.
For ac analysis, replace the CE stage with its Thévenin ac equivalent as in Fig. 2.67b. Recall from Example 2.22 that the CE stage provides the open-circuit ac voltage $v_{o 1}=-144 v_{i}$ with the equivalent output resistance $R_{o 1}=3.8 \mathrm{k} \Omega$. We can thus adapt Eq. (2.86) and write
$$
\frac{v_{o}}{v_{o 1}}=\frac{v_{o}}{-144 v_{i}}=\frac{1}{1+\frac{3.8+1.5}{(100+1)(4.3 / / 59)}}=0.987
$$
so the overall voltage gain is $a_{o c}=v_{o} / v_{i}=-144 \times 0.987=-142$ V/V. Finally, we adapt Eq. (2.59a) (the experience gained with Example 2.25 indicates that we can ignore $r_{o}$ ) and obtain
$$
R_{e 2}=\frac{R_{o 1}+r_{\pi 2}}{\beta_{02}+1}=\frac{3.8+1.5}{101}=0.052 \mathrm{k} \Omega=52 \Omega
$$
Consequently,
$$
R_{o}=R_{5} / / R_{e 2}=4,300 / / 52 \cong 52 \Omega \text { (very low) }
$$
Since $a_{o c}$ is reduced from $-144 \mathrm{~V} / \mathrm{V}$ to $-142 \mathrm{~V} / \mathrm{V}$, loading of the CE stage by the CC stage is minimal. However, the reduction in $R_{o}$ is truly dramatic, from 3,800 $\Omega$ to $52 \Omega$ !
### The Common-Base (CB) Configuration
The common-base (CB) amplifier receives the input at the emitter and delivers the output from the collector. Since the resistance seen looking into the emitter is generally low $\left(R_{e} \cong 1 / g_{m}\right)$, the natural input signal for this configuration is a current, $i_{s i g}$. Also, since the resistance seen looking into the collector is generally high ( $R_{c} \cong r_{o}$, or even higher if there is emitter degeneration), the natural output signal is also a current, $i_{0}$. Just like the CC configuration approximates a voltage buffer, which ideally has $R_{i} \rightarrow \infty, R_{o} \rightarrow 0$, and $v_{o} / v_{s i g} \rightarrow 1 \mathrm{~V} / \mathrm{V}$, the CB configuration approximates a current buffer, which ideally has
$$
\begin{equation*}
R_{i} \rightarrow 0 \quad R_{o} \rightarrow \infty \quad \frac{i_{o}}{i_{s i g}} \rightarrow 1 \mathrm{~A} / \mathrm{A} \tag{2.90}
\end{equation*}
$$
image_name:(a)
description:
[
name: Q, type: NPN, ports: {C: c, B: GND, E: e}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: e}
name: Rsig, type: Resistor, value: Rsig, ports: {N1: Vin, N2: GND}
name: RL, type: Resistor, value: RL, ports: {N1: VCC, N2: c}
name: isig, type: CurrentSource, value: isig, ports: {Np: Vin, Nn: GND}
name: IE, type: CurrentSource, value: IE, ports: {Np: e, Nn: GND}
]
extrainfo:The circuit is a common-base amplifier configuration. The signal source is modeled with a Norton equivalent. The output is taken across Ro and RL, with the transistor Q providing the amplification.
image_name:(b)
description:
[
name: Q, type: NPN, ports: {C: c, B: GND, E: e}
name: R_L, type: Resistor, value: R_L, ports: {N1: GND, N2: c}
name: R_sig, type: Resistor, value: R_sig, ports: {N1: e, N2: GND}
name: i_sig, type: CurrentSource, value: i_sig, ports: {Np: e, Nn: GND}
]
extrainfo:The circuit is a common-base amplifier configuration with an NPN transistor. The input current source i_sig is connected to the emitter, and the output is taken from the collector node c. Resistors R_i and R_sig are connected to the emitter node e.
FIGURE 2.68 The common-base (CB) amplifier and its ac equivalent.
The CB configuration is shown in Fig. 2.68a, where we observe that the signal source is now modeled with a Norton equivalent. To find the small-signal parameters, refer to the ac equivalent of Fig. $2.68 b$. The output resistance $R_{o}$ is readily found by recycling Eq. (2.62a), but with $R_{B} \rightarrow 0$ and $R_{E} \rightarrow R_{s i g}$,
$$
\begin{equation*}
R_{o} \cong r_{o}\left[1+g_{m}\left(r_{\pi} / / R_{s i g}\right)\right] \tag{2.91}
\end{equation*}
$$
If $R_{s i g} \gg r_{\pi}$, then $R_{o} \cong r_{o}\left(1+g_{m} r_{\pi}\right)=r_{o}\left(1+\beta_{0}\right)$, a truly large value. In the calculation of the (low) input resistance $R_{i}$ it is customary to ignore the presence of the (high) resistance $r_{o}$, at least in discrete designs, where the coupling from emitter to collector via $r_{o}$ is generally negligible (this, however, may not necessarily be the case in IC designs, as we shall see in Chapter 4.) We thus adapt Eq. (2.59) and write
$$
\begin{equation*}
R_{i} \cong r_{e} \tag{2.92}
\end{equation*}
$$
To find the signal-to-load current gain, we note that the source resistance $R_{s i g}$ forms a current divider with the input resistance $R_{i}$, giving
$$
i_{i}=\frac{R_{s i g}}{R_{s i g}+R_{i}} i_{s i g}
$$
But, $i_{o}=\alpha_{0} i_{i}$, so, combining with Eq. (2.92) we get
$$
\begin{equation*}
\frac{i_{o}}{i_{s i g}}=\frac{\alpha_{0}}{1+r_{e} / R_{s i g}} \tag{2.93}
\end{equation*}
$$
It is apparent that this gain is less than unity, but it can be very close to unity for $R_{s i g} \gg r_{e}$. The CB configuration is particularly useful when its signal input is supplied
by the collector of another BJT. The resulting two-transistor configuration, known as the cascode configuration, enjoys advantages of speed and flexibility that make it particularly suited to IC implementations, as we shall see in Chapters 4 and 6.
In the circuit of Fig. $2.68 a$ let $V_{C C}=-V_{E E}=5 \mathrm{~V}$ and $I_{E}=1 \mathrm{~mA}$, and let the BJT have $\beta_{0}=\beta_{F}=100$ and $V_{A}=100 \mathrm{~V}$. Find $R_{i}, R_{o}$, and $i_{o} / i_{s i g}$ if $R_{s i g}=10 \mathrm{k} \Omega$, and comment on your findings.
#### Solution
We have $\alpha_{0}=0.99, g_{m}=38.5 \mathrm{~mA} / \mathrm{V}, r_{e}=26 \Omega, r_{\pi}=2.6 \mathrm{k} \Omega$, and $r_{o}=100 \mathrm{k} \Omega$. By Eqs. (2.91) through (2.93),
$$
\begin{aligned}
R_{i} & \cong 26 \Omega \\
R_{o} & =100[1+38.5(2.6 / / 10)] \cong 8 \mathrm{M} \Omega \\
\frac{i_{o}}{i_{s i g}} & =\frac{0.99}{1+0.026 / 10}=0.987 \mathrm{~A} / \mathrm{A}
\end{aligned}
$$
As expected of a current buffer, $R_{i}$ is truly low, $R_{o}$ truly high, and the gain is fairly close to unity.
### The CB Configuration as a Voltage Amplifier
Even though the most appropriate application of the CB configuration is as a current buffer, there are situations in which it is used as a voltage amplifier with gain $v_{c} / v_{e}$. Considering that $v_{c}=-g_{m}\left(R_{L} / / r_{o}\right) v_{b e}=-g_{m}\left(R_{L} / / r_{o}\right)\left(v_{b}-v_{e}\right)=-g_{m}\left(R_{L} / / r_{o}\right)\left(0-v_{e}\right)$, it follows that
$$
\begin{equation*}
\frac{v_{c}}{v_{e}}=+g_{m}\left(R_{L} / / r_{o}\right) \tag{2.94}
\end{equation*}
$$
In words, the voltage gain of the CB configuration has the same magnitude but opposite polarity as that of the CE configuration. The other major difference is in the input resistance, which is $r_{\pi}$ in the CE case, but $r_{e}$ (which is $\beta_{0}+1$ times as small) in the CB case. For instance, with $R_{L}=10 \mathrm{k} \Omega$ the circuit of Example 2.28 gives the voltage gain $v_{c} / v_{e}=38 \times(10 / / 100) \cong+350 \mathrm{~V} / \mathrm{V}$, a fairly large value.
### The $T$ Model of the BJT
Even though the small-signal model of Fig. 2.41 is adequate for the ac analysis of all three BJT configurations, an alternative model is available, which offers additional insight especially into the CB configuration. To illustrate, consider the ac model of Fig. 2.41, repeated in Fig. $2.69 a$ but with $r_{o}$ omitted for simplicity. Since it is reminiscent of the Greek letter $\pi$, it is also referred to as the $\pi$ model.
If we now replace the dependent source with two identical sources connected in series as in Fig. 2.69b, circuit behavior won't change. Indeed, since the node common
image_name:(a)
description:
[
name: rπ, type: Resistor, value: rπ, ports: {N1: B, N2: E}
name: gmvbe, type: VoltageControlledCurrentSource, ports: {Np: C, Nn: E}
]
extrainfo:The diagram represents the transformation of the π model into the T model of a BJT for AC analysis. The dependent current source 'gmvbe' is connected between nodes C and E, with the control voltage 'vbe' across the resistor 'rπ'.
image_name:(b)
description:
[
name: rπ, type: Resistor, value: rπ, ports: {N1: B, N2: E}
name: g_mvbe_1, type: VoltageControlledCurrentSource, value: g_mvbe, ports: {Np: X, Nn: E}
name: g_mvbe_2, type: CurrentControlledVoltageSource, value: g_mvbe, ports: {Np: C, Nn: X}
]
extrainfo:The circuit diagram (b) is a transformation of the π model into a T model for a BJT. It includes a resistor rπ between nodes B and E, a voltage-controlled current source between nodes X and E, and a current-controlled voltage source between nodes C and X.
image_name:(c)
description:
[
name: rπ, type: Resistor, value: rπ, ports: {N1: B, N2: E}
name: gmvbe, type: VoltageControlledCurrentSource, ports: {Np: B, Nn: E}
name: gmvbe, type: VoltageControlledVoltageSource, ports: {Np: B, Nn: C}
]
extrainfo:The circuit diagram (c) is a transformation of the π model to the T model for a BJT. It includes a resistor rπ connected between nodes B and E, a voltage-controlled current source between nodes B and E, and a voltage-controlled voltage source between nodes B and C.
FIGURE 2.69 Steps for transforming the $\pi$ model into the $T$ model of the BJT.
to the two sources is such that the current entering it equals that exiting it, we can tie it to the base terminal $B$ as in Fig. 2.69c, and circuit behavior still won't change. However, by this artifice we avoid having a dependent source directly between the collector and emitter, a definite advantage in the ac analysis of the CB configuration, as we shall see. Now, we can simplify the model further because the bottom dependent source is controlled by the voltage $v_{b e}$ across its own terminals and thus acts as a resistance of value $v_{b e} /\left(g_{m} v_{b e}\right)=1 / g_{m}$. Its parallel combination with $r_{\pi}$ is
$$
r_{\pi} / / \frac{1}{g_{m}}=\frac{\beta_{0}}{g_{m}} / / \frac{1}{g_{m}}=\frac{\beta_{0}}{\beta_{0}+1} \frac{1}{g_{m}}=\frac{\alpha_{0}}{g_{m}}=r_{e}
$$
that is, it is simply the dynamic resistance of the B-E junction as encountered in Eq. (2.61). (We should have anticipated this intuitively!) As for the top dependent source, we can regard it either as controlled by $v_{b e}$, as shown, or as controlled by the current $i_{e}=v_{b e} / r_{e}$, in which case we express it as
$$
g_{m} v_{b e}=g_{m} r_{e} i_{e}=\alpha_{0} i_{e}
$$
We can finally draw the alternative small-signal BJT model as in Fig. 2.70, where we have included also the small-signal resistance $r_{o}$ to account for the Early effect.
image_name:Figure 2.70
description:
[
name: Q, type: NPN, ports: {C: C, B: B, E: E}
name: gm*vbe/alpha0*ie, type: VoltageControlledCurrentSource, ports: {Np: C, Nn: B}
name: ro, type: Resistor, value: ro, ports: {N1: C, N2: B}
name: re, type: Resistor, value: re, ports: {N1: B, N2: E}
]
extrainfo:The circuit is a small-signal BJT model known as the T model, which includes the small-signal resistance ro to account for the Early effect.
image_name:Figure 2.70(c)
description:
[
name: Q1, type: NPN, ports: {C: C, B: B, E: E}
]
extrainfo:The diagram shows the small-signal model of a BJT using the T model, illustrating the relationship between the base-emitter voltage (vbe), the emitter current (ie), and the transconductance (gm) with the Early effect modeled by ro.
FIGURE 2.70 The small-signal BJT model known as the T model. Note that it applies both to the npn and the pnp BJT.
image_name:(a)
description:
[
name: vb, type: VoltageSource, value: vb, ports: {Np: B, Nn: E(GND)}
name: rπ, type: Resistor, value: rπ, ports: {N1: B, N2: E(GND)}
name: gmvb, type: VoltageControlledCurrentSource, ports: {Np: C, Nn: E(GND)}
name: RC, type: Resistor, value: RC, ports: {N1: C, N2: E(GND)}
]
extrainfo:The circuit diagram illustrates the small-signal models of a BJT in both CE and CB configurations using the T model. The diagram shows the relationship between base-emitter voltage (vbe), emitter current (ie), and transconductance (gm). The models omit the Early effect for simplicity.
image_name:(b)
description:
[
name: v_e, type: VoltageSource, value: v_e, ports: {Np: E, Nn: GND}
name: r_e, type: Resistor, value: r_e, ports: {N1: E, N2: B}
name: g_m v_e, type: VoltageControlledCurrentSource, value: g_m v_e, ports: {Np: C, Nn: B}
name: RC, type: Resistor, value: RC, ports: {N1: C, N2: B(GND)}
]
extrainfo:The diagram shows the small-signal model of a BJT using the T model. It illustrates the relationship between the base-emitter voltage (vbe), the emitter current (ie), and the transconductance (gm) with the Early effect modeled by ro. The model applies to both npn and pnp BJTs.
FIGURE 2.71 The CE and CB configurations are compared most effectively if we use, respectively, (a) the $\pi$ model, and (b) and $T$ model for the BJT.
Since this model, with $r_{o}$ omitted, looks like a rotated letter $T$, it is aptly called the $T$ model.
Figure 2.71 utilizes both BJT models ( $r_{o}$ is again omitted for simplicity) for a quick comparison of the CE and CB configurations. By inspection, the CE amplifier of Fig. $2.71 a$ presents an input resistance of $r_{\pi}$, and yields $v_{c}=-R_{C} g_{m} v_{b}$, indicating a gain of $v_{c} / v_{b}=-g_{m} R_{c}$. Turning to Fig. $2.71 b$, we note that the direction of the dependent source has been reversed compared to Fig. 2.70, owing to the fact that $g_{m} v_{b e}=$ $g_{m}\left(v_{b}-v_{e}\right)=g_{m}\left(0-v_{e}\right)=-g_{m} v_{e}$. By inspection, the CB amplifier presents an input resistance of $r_{e}$ and yields $v_{c}=+R_{C} g_{m} v_{e}$, indicating a gain of $v_{c} / v_{e}=+g_{m} R_{C}$. These quick analyses confirm that the input resistances differ by a factor of $\left(\beta_{0}+1\right)$, and the gains have equal magnitudes but opposite polarities. Also, in both cases, applying a voltage across the input resistance ( $r_{\pi}$ or $r_{e}$ ) results in the transfer of current to another resistance ( $R_{C}$ at the output.) Not surprisingly, the name transistor was coined as a contraction of the words transfer and resistor.
### PSpice Simulation
As we study BJT circuits, it is always good practice to corroborate the predictions of hand calculations with computer simulation or laboratory measurements. Figure $2.72 a$ shows a PSpice circuit to simulate the CE-CC amplifier of Example 2.27, but using 2N2222 BJTs.
Shown in Fig. $2.72 b$ is the Bode plot of the gain magnitude $\left|V_{o} / V_{i}\right|$. At 1 kHz , PSpice predicts a gain of 43.3 dB , or a gain magnitude of $10^{43.3 / 20}=146 \mathrm{~V} / \mathrm{V}$. In Example 2.27 we predicted a gain magnitude of 142 V/V. Considering that the present simulation uses 2N2222 BJTs, whose characteristics differ a bit from those of the BJTs used in the example, some discrepancy is expected. We also note that gain drops at the low end of the frequency range. This too is expected, as the capacitances cease to act as ac shorts at low frequencies. In the present case, the gain decrease is dominated by $C_{2}$.
For a complete picture, we need to plot also the input and output impedances $\left|Z_{i}\right|$ and $\left|Z_{o}\right|$. Recall from basic circuits courses that the impedance $Z$ seen looking into a
image_name:(a)
description:
[
name: Vi, type: VoltageSource, value: 1 mVac, ports: {Np: Vi, Nn: GND}
name: C1, type: Capacitor, value: 22 uF, ports: {Np: Vi, Nn: B}
name: C2, type: Capacitor, value: 330 uF, ports: {Np: E, Nn: GND}
name: R1, type: Resistor, value: 68 kOhm, ports: {N1: VCC, N2: B}
name: R2, type: Resistor, value: 47 kOhm, ports: {N1: B, N2: GND}
name: R3, type: Resistor, value: 4.3 kOhm, ports: {N1: Vo, N2: GND}
name: Rc, type: Resistor, value: 3.9 kOhm, ports: {N1: VCC, N2: C}
name: Re, type: Resistor, value: 3.9 kOhm, ports: {N1: E, N2: GND}
name: Q1, type: NPN, ports: {C: C, B: B, E: E}
name: Q2, type: NPN, ports: {C: VCC, B: C, E: E}
]
extrainfo:This is a CE-EC amplifier circuit using 2N2222 BJTs, designed to display the Bode plot of gain. The circuit includes two stages of amplification with capacitive coupling and biasing resistors. The input is provided by a small AC voltage source, and the output is taken across a load resistor R3. The circuit operates with a supply voltage VCC of 12V.
image_name:(b)
description:The graph labeled "(b)" is a Bode plot displaying the gain of a CE-EC amplifier using 2N2222 BJTs. The horizontal axis represents frequency in Hertz (Hz) on a logarithmic scale, ranging from 20 Hz to 10,000 Hz (or 10^4 Hz). The vertical axis represents gain in decibels (dB), ranging from 0 dB to 60 dB.
**Overall Behavior and Trends:**
The plot shows a relatively flat gain response across the frequency range, indicating that the amplifier maintains a consistent gain over a wide band of frequencies. There is a slight increase in gain as the frequency increases from 20 Hz, reaching a stable level that remains mostly constant up to 10,000 Hz.
**Key Features and Technical Details:**
- At the low-frequency end (around 20 Hz), there is a noticeable drop in gain, which is attributed to the capacitive elements in the circuit, particularly $C_{2}$, as mentioned in the context. This is a common characteristic in amplifiers due to the impedance of capacitors increasing at lower frequencies.
- The gain stabilizes quickly as the frequency increases, maintaining a nearly constant level throughout the mid to high-frequency range.
**Annotations and Specific Data Points:**
- The plot does not show explicit numerical values for the gain level, but it appears to stabilize just below 60 dB.
- There are no additional annotations or markers such as -3 dB points or other reference lines visible on the graph.
This Bode plot effectively demonstrates the frequency response of the amplifier, highlighting its ability to maintain a steady gain across a wide range of frequencies, with a slight drop-off at the low end due to capacitive effects.
FIGURE 2.72 PSpice circuit to display the Bode plot of gain for the CE-EC amplifier of Example 2.27, but using 2N2222 BJTs.
given terminal is obtained by applying an ac test voltage $V$ (or an ac test current $I$ ), obtaining the resulting ac current $I$ (or ac voltage $V$ ), and then taking the ratio $Z=$ $V / I$. Here, $V$ and $I$ represent the phasors associated with the given ac test signals.
To find $Z_{i}$, we still use the PSpice circuit of Fig. 2.72a but with the input source $V_{i}$ now acting as the test voltage. Then, $Z_{i}=V_{i} / I_{i}$, where $I_{i}$ is the ac current out of the source $V_{i}$. The result, plotted in Fig. 2.73 b , top, yields $\left|Z_{i}\right|=3.7 \mathrm{k} \Omega$ at 1 kHz . Note that $\left|Z_{i}\right|$ increases at low frequencies, again because of the fact that the capacitors cease to act as ac shorts as frequency is lowered.
To find $Z_{o}$, use the PSpice circuit of Fig. 2.73a, where the input signal has been set to zero and the output terminal is subjected to a test current $I_{o}$. Then, $Z_{o}=V_{o} / I_{o}$,
image_name:Figure 2.73a
description:
[
name: Q1, type: NPN, ports: {C: C, B: B, E: E}
name: Q2, type: NPN, ports: {C: VCC, B: C, E: Vo}
name: R1, type: Resistor, value: 68kΩ, ports: {N1: VCC, N2: B}
name: R2, type: Resistor, value: 47kΩ, ports: {N1: B, N2: GND}
name: R3, type: Resistor, value: 4.3kΩ, ports: {N1: Vo, N2: GND}
name: RC, type: Resistor, value: 3.9kΩ, ports: {N1: VCC, N2: C}
name: RE, type: Resistor, value: 3.9kΩ, ports: {N1: E, N2: GND}
name: C1, type: Capacitor, value: 22μF, ports: {Np: GND, Nn: B}
name: C2, type: Capacitor, value: 330μF, ports: {Np: E, Nn: GND}
name: Io, type: CurrentSource, value: 1μAac, ports: {Np: Vo, Nn: GND}
]
extrainfo:The circuit is a two-stage amplifier with NPN transistors Q1 and Q2. It uses resistors R1, R2, RC, RE, and R3 for biasing and stabilization, and capacitors C1 and C2 for coupling and bypassing. The circuit is designed to measure the output impedance Z_o using a test current source Io.
(a)
image_name:Figure 2.73b
description:The graph in Figure 2.73b is a frequency plot depicting the magnitudes of the input and output impedances, |Z_i| and |Z_o|, of a two-stage amplifier circuit. The x-axis represents frequency in hertz (Hz) on a logarithmic scale, ranging from 20 Hz to 10,000 Hz (10^4 Hz). The y-axis represents impedance in ohms (Ω), also on a logarithmic scale, ranging from 10 Ω to 10,000 Ω (10^4 Ω).
Overall Behavior and Trends:
- **Input Impedance (|Z_i|):** The plot shows that the input impedance starts at a high value close to 10,000 Ω at lower frequencies and remains relatively flat across the frequency range, indicating minimal variation with frequency.
- **Output Impedance (|Z_o|):** The output impedance is shown to be relatively flat and constant at around 36 Ω across the frequency spectrum.
Key Features and Technical Details:
- At 1 kHz, the output impedance |Z_o| is specifically noted as 36 Ω, which is a critical value for this analysis.
- The input impedance |Z_i| remains significantly higher than the output impedance, which is typical for amplifier circuits to ensure proper signal transfer.
Annotations and Specific Data Points:
- The graph does not show any peaks, valleys, or inflection points, indicating stable impedance characteristics over the frequency range.
- The constant nature of both impedances across the frequency range suggests effective design for frequency-independent performance.
This graph effectively illustrates the impedance characteristics of the amplifier circuit, highlighting the low output impedance and higher input impedance, which are consistent with desired amplifier properties.
(b)
FIGURE 2.73 (a) PSpice circuit to find the output impedance $Z_{0}$. (b) Frequency plots of the input and output impedances.
where $V_{o}$ is the ac voltage appearing at the output. The result, plotted in Fig. 2.73b, bottom, yields $\left|Z_{o}\right|=36 \Omega$ at 1 kHz . Again, these results are fairly consistent with those predicted in Examples 2.22 and 2.27. The main cause for the discrepancies are the differences in the betas of the transistors used in the examples and those used in the simulation. The motivated student may wish to create ad hoc PSpice models for the BJTs of the examples, and verify a much closer agreement between predictions and simulations.
### APPENDIX 2A
#### SPICE Models for BJTs
As in the case of the $p n$ diode, the characteristics of a BJT are expressed in terms of a list of parameters that SPICE then uses to create an internal model of the device. Such a list is shown in Table 2A.1. PSpice's library comes with the models of several popular BJTs, such as the npn 2N2222 and the pnp 2N2907. The user can create additional models by editing any one of the models already provided.
As an example, consider the PSpice circuit of Fig. 2.59, utilizing the popular 2N2222 npn BJT. By PSpice convention, BJT names must start with the letter Q, so the part number has been designated as Q2N2222. To create a PSpice circuit schematic we use the Place $\rightarrow$ Part commands to lay out the various components, and the Place $\rightarrow$ Wire commands to interconnect them. When it comes to placing the BJT, we import it from the library by going down the list of entries and selecting the Q2N2222 part by left-clicking on it. Once the BJT has been placed in the circuit schematic, we can visualize its model by left-clicking on the BJT itself to select it, and then right-clicking to activate a pull-down menu of possible actions. If we left-click on Edit PSpice Model, the following list will appear:
```
.model Q2N2222 NPN(Is=14.34f Xti=3 Eg=1.11 Vaf=74.03 Bf=255.9
+ Ne=1.307 Ise=14.34f Ikf=.2847 Xtb=1.5 Br=6.092 Nc=2
+ Isc=0 Ikr=0 Rc=1 Cjc=7.306p Mjc=.3416 Vjc=.75 Fc=.5
+ Cje=22.01p Mje=.377 Vje=.75 Tr=46.91n Tf=411.1p Itf=.6
+ Vtf=1.7 Xtf=3 Rb=10)
```
The parameter values shown are designed to match as closely as possible those given in the manufacturer's data sheets. Scanning the list we easily see that this particular BJT type has $I_{s}=14.34 \mathrm{fA}, V_{A}=74.03 \mathrm{~V}, \beta_{F}=255.9, \beta_{R}=6.092, r_{c}=1 \Omega$, $C_{i c 0}=7.306 \mathrm{pF}, m_{c}=0.3416, \phi_{c}=0.75 \mathrm{~V}, C_{j e 0}=22.01 \mathrm{pF}, m_{e}=0.377, \phi_{e}=0.75 \mathrm{~V}$, $\tau_{R}=46.91 \mathrm{~ns}, \tau_{F}=411.1 \mathrm{ps}$, and $r_{b}=10 \Omega$. The list contains additional parameters representing higher-order effects that are beyond our present scope. One such effect is the dependence of $\beta_{F}$ upon $I_{C}$, as illustrated in Fig. 2.12b. For more details, see Ref. [12]. Also shown in the list are the parameters intervening in the calculation of the junction capacitances associated with the base-emitter $\left(C_{j e}\right)$, base-collector $\left(C_{j c}\right)$, and collector-substrate junctions $\left(C_{s}\right)$. This subject will be taken up in great detail in Chapter 6, when we will investigate the frequency response of integrated circuits.
TABLE 2A.1 Partial parameter list of the PSpice model for BJTs.
| Symbol | Name | Parameter description | Units | Default | Example |
| :---: | :---: | :---: | :---: | :---: | :---: |
| $I_{s}$ | Is | Saturation current | A | 0.1 fA | 2 fA |
| $\beta_{F}$ | Bf | Forward current gain |  | 100 | 250 |
| $\mathrm{V}_{\text {A }}$ | Vaf | Forward Early voltage | V | $\infty$ | 75 V |
| $\beta_{R}$ | Br | Reverse current gain |  | 1 | 2.5 |
| $r_{b}$ | Rb | Bulk resistance of the base | $\Omega$ | 0 | $200 \Omega$ |
| $r_{c}$ | Rc | Bulk resistance of the collector | $\Omega$ | 0 | $50 \Omega$ |
| $r_{e x}$ | Re | Bulk resistance of the emitter | $\Omega$ | 0 | $1 \Omega$ |
| $\mathrm{C}_{j e 0}$ | Cje | Zero-bias B-E junction capacitance | F | 0 | 1.0 pF |
| $\phi_{e}$ | Vje | B-E built-in potential | V | 0.75 V | 0.8 V |
| $m_{e}$ | Mje | $\mathrm{B}-\mathrm{E}$ grading coefficient |  | 0.33 | 0.5 |
| $C_{j c 0}$ | Cjc | Zero-bias B-C junction capacitance | F | 0 | 0.5 pF |
| $\phi_{c}$ | Vjc | B-C built-in potential | V | 0.75 V | 0.7 V |
| $m_{c}$ | Mjc | B-C grading coefficient |  | 0.33 | 0.5 |
| $C_{s 0}$ | Cjs | Zero-bias collector-substrate junction capacitance | F | 0 | 1.0 pF |
| $\phi_{s}$ | Vjs | Collector-substrate built-in potential | V | 0.75 V | 0.6 V |
| $m_{s}$ | Mjs | Collector-substrate grading coefficient |  | 0 | 0.5 |
| $\tau_{F}$ | Tf | Forward transit time | s | 0 | 0.2 ns |
| $\tau_{R}$ | Tr | Reverse transit times | S | 0 | 15 ns |
As another example, consider the 2N2907A pnp BJT, whose model is also available in PSpice's library. Its parameter list is as follows:
```
.model Q2N2907A PNP(Is=650.6E-18 Xti=3 Eg=1.11 Vaf=115.7
+ Bf=231.7 Ne=1.829 Ise=54.81f Ikf=1.079 Xtb=1.5
+ Br=3.563 Nc=2 Isc=0 Ikr=0 Rc=.715 Cjc=14.76p
+ Mjc=.5383 Vjc=.75 Fc=.5 Cje=19.82p Mje=.3357
+ Vje=.75 Tr=111.3n Tf=603.7p Itf=.65 Vtf=5
+ Xtf=1.7 Rb=10)
```
As in the 2N2222 case, the name has been changed to Q2N2907A, and the (parenthesized) list is now preceded by the designation PNP specifying the device type. The parameter list is very similar to that of the Q2N2222 model, except for the different parameter values reflecting differences in the data-sheet characteristics.
If you wish to create your own BJT model, you can do so simply by overwriting (editing) the parameter values of an existing BJT model, such as the Q2N2222 or the Q2N2907A models seen above. However, to avoid losing the original parameter list, a new name must be given to the newly formed model before saving it. This is what was done to create the model for the simplified npn BJT of Fig. 2.32. The BJT model was renamed as Qn, and the parameter list was edited as follows:
```
.model Qn NPN(Is=2fA Bf=100)
```
Likewise, the model of a homebrew pnp BJT with, say, $I_{s}=0.5 \mathrm{fA}, \beta_{F}=75$, and $V_{A}=50 \mathrm{~V}$ would be
.model Qp PNP(Is=0.5fA Bf=75 Vaf=50V)
All omitted parameters are automatically assigned default values according to Table 2A.1.
