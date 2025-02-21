# 2. Bipolar, MOS, and BiCMOS Integrated-Circuit Technology

## 2.1 Introduction

For the designer and user of integrated circuits, a knowledge of the details of the fabrication process is important for two reasons. First, IC technology has become pervasive because it provides the economic advantage of the planar process for fabricating complex circuitry at low cost through batch processing. Thus a knowledge of the factors influencing the cost of fabrication of integrated circuits is essential for both the selection of a circuit approach to solve a given design problem by the designer and the selection of a particular circuit for fabrication as a custom integrated circuit by the user. Second, integrated-circuit technology presents a completely different set of cost constraints to the circuit designer from those encountered with discrete components. The optimum choice of a circuit approach to realize a specified circuit function requires an understanding of the degrees of freedom available with the technology and the nature of the devices that are most easily fabricated on the integratedcircuit chip.

At the present time, analog integrated circuits are designed and fabricated in bipolar technology, in MOS technology, and in technologies that combine both types of devices in one process. The necessity of combining complex digital functions on the same integrated circuit with analog functions has resulted in an increased use of digital MOS technologies for analog functions, particularly those functions such as analog-digital conversion required for interfaces between analog signals and digital systems. However, bipolar technology is now used and will continue to be used in a wide range of applications requiring high-current drive capability and the highest levels of precision analog performance.

In this chapter, we first enumerate the basic processes that are fundamental in the fabrication of bipolar and MOS integrated circuits: solid-state diffusion, lithography, epitaxial growth, ion implantation, selective oxidation, and polysilicon deposition. Next, we describe the sequence of steps that are used in the fabrication of bipolar integrated circuits and describe the properties of the passive and active devices that result from the process sequence. Also, we examine several modifications to the basic process. In the next subsection, we consider the sequence of steps in fabricating MOS integrated circuits and describe the types of devices resulting in that technology. This is followed by descriptions of BiCMOS technology, silicon-germanium heterojunction transistors, and interconnect materials under study to replace aluminum wires and silicon-dioxide dielectric. Next, we examine the factors affecting the manufacturing cost of monolithic circuits and, finally, present packaging considerations for integrated circuits.

## 2.2 Basic Processes in Integrated-Circuit Fabrication

The fabrication of integrated circuits and most modern discrete component transistors is based on a sequence of photomasking, diffusion, ion implantation, oxidation, and epitaxial growth steps applied to a slice of silicon starting material called a wafer. ${ }^{1,2}$ Before beginning a description of the basic process steps, we will first review the effects produced on the electrical properties of silicon by the addition of impurity atoms.

### 2.2.1 Electrical Resistivity of Silicon

The addition of small concentrations of $n$-type or $p$-type impurities to a crystalline silicon sample has the effect of increasing the number of majority carriers (electrons for $n$-type, holes for $p$-type) and decreasing the number of minority carriers. The addition of impurities is called doping the sample. For practical concentrations of impurities, the density of majority carriers is approximately equal to the density of the impurity atoms in the crystal. Thus for $n$-type material,

$$
\begin{equation*}
n_{n} \simeq N_{D} \tag{2.1}
\end{equation*}
$$

where $n_{n}\left(\mathrm{~cm}^{-3}\right)$ is the equilibrium concentration of electrons and $N_{D}\left(\mathrm{~cm}^{-3}\right)$ is the concentration of $n$-type donor impurity atoms. For $p$-type material,

$$
\begin{equation*}
p_{p} \simeq N_{A} \tag{2.2}
\end{equation*}
$$

where $p_{p}\left(\mathrm{~cm}^{-3}\right)$ is the equilibrium concentration of holes and $N_{A}\left(\mathrm{~cm}^{-3}\right)$ is the concentration of $p$-type acceptor impurities. Any increase in the equilibrium concentration of one type of carrier in the crystal must result in a decrease in the equilibrium concentration of the other. This occurs because the holes and electrons recombine with each other at a rate that is proportional to the product of the concentration of holes and the concentration of electrons. Thus the number of recombinations per second, $R$, is given by

$$
\begin{equation*}
R=\gamma n p \tag{2.3}
\end{equation*}
$$

where $\gamma$ is a constant, and $n$ and $p$ are electron and hole concentrations, respectively, in the silicon sample. The generation of the hole-electron pairs is a thermal process that depends only on temperature; the rate of generation, $G$, is not dependent on impurity concentration. In equilibrium, $R$ and $G$ must be equal, so that

$$
\begin{equation*}
G=\text { constant }=R=\gamma n p \tag{2.4}
\end{equation*}
$$

If no impurities are present, then

$$
\begin{equation*}
n=p=n_{i}(T) \tag{2.5}
\end{equation*}
$$

where $n_{i}\left(\mathrm{~cm}^{-3}\right)$ is the intrinsic concentration of carriers in a pure sample of silicon. Equations 2.4 and 2.5 establish that, for any impurity concentration, $\gamma n p=$ constant $=\gamma n_{i}^{2}$, and thus

$$
\begin{equation*}
n p=n_{i}^{2}(T) \tag{2.6}
\end{equation*}
$$

Equation 2.6 shows that as the majority carrier concentration is increased by impurity doping, the minority carrier concentration is decreased by the same factor so that product $n p$ is constant in equilibrium. For impurity concentrations of practical interest, the majority carriers outnumber the minority carriers by many orders of magnitude.

The importance of minority- and majority-carrier concentrations in the operation of the transistor was described in Chapter 1. Another important effect of the addition of impurities is
image_name:Figure 2.1 Hole and electron mobility as a function of doping in silicon
description:The graph is a line plot depicting the relationship between the mobility of charge carriers (holes and electrons) in silicon and the total impurity concentration. The x-axis represents the total impurity concentration in silicon, measured in cm⁻³, and is scaled logarithmically, ranging from 10¹⁴ to 10²¹ cm⁻³. The y-axis represents the mobility (μ) of the charge carriers, measured in cm²/V-s, also on a logarithmic scale, ranging from 10 to 10³ cm²/V-s.

There are two curves shown in the graph: one for electrons and one for holes. Both curves exhibit a downward trend, indicating that as the impurity concentration increases, the mobility of both electrons and holes decreases.

For electrons, the mobility starts at a higher value compared to holes and decreases more sharply as impurity concentration increases. Initially, electron mobility is around 1400 cm²/V-s at lower impurity concentrations (around 10¹⁴ cm⁻³) and drops to about 100 cm²/V-s at higher impurity concentrations (around 10²¹ cm⁻³).

For holes, the mobility starts lower, at about 450 cm²/V-s at the lower impurity concentration end, and decreases to roughly 50 cm²/V-s at the higher impurity concentration.

The graph highlights the significant impact of impurity doping on the mobility of charge carriers in silicon, with electron mobility being generally higher than hole mobility across the range of impurity concentrations. This is an important consideration in semiconductor device design and performance.

Figure 2.1 Hole and electron mobility as a function of doping in silicon. ${ }^{3}$
an increase in the ohmic conductivity of the material itself. This conductivity is given by

$$
\begin{equation*}
\sigma=q\left(\mu_{n} n+\mu_{p} p\right) \tag{2.7}
\end{equation*}
$$

where $\mu_{n}\left(\mathrm{~cm}^{2} / \mathrm{V}-\mathrm{s}\right)$ is the electron mobility, $\mu_{p}\left(\mathrm{~cm}^{2} / \mathrm{V}-\mathrm{s}\right)$ is the hole mobility, and $\sigma$ $(\Omega-\mathrm{cm})^{-1}$ is the electrical conductivity. For an $n$-type sample, substitution of (2.1) and (2.6) in (2.7) gives

$$
\begin{equation*}
\sigma=q\left(\mu_{n} N_{D}+\mu_{p} \frac{n_{i}^{2}}{N_{D}}\right) \simeq q \mu_{n} N_{D} \tag{2.8}
\end{equation*}
$$

For a $p$-type sample, substitution of (2.2) and (2.6) in (2.7) gives

$$
\begin{equation*}
\sigma=q\left(\mu_{n} \frac{n_{i}^{2}}{N_{A}}+\mu_{p} N_{A}\right) \simeq q \mu_{p} N_{A} \tag{2.9}
\end{equation*}
$$

The mobility $\mu$ is different for holes and electrons and is also a function of the impurity concentration in the crystal for high impurity concentrations. Measured values of mobility in silicon as a function of impurity concentration are shown in Fig. 2.1. The resistivity $\rho(\Omega-\mathrm{cm})$ is usually specified in preference to the conductivity, and the resistivity of $n$ - and $p$-type silicon as a function of impurity concentration is shown in Fig. 2.2. The conductivity and resistivity are related by the simple expression $\rho=1 / \sigma$.

### 2.2.2 Solid-State Diffusion

Solid-state diffusion of impurities in silicon is the movement, usually at high temperature, of impurity atoms from the surface of the silicon sample into the bulk material. During this hightemperature process, the impurity atoms replace silicon atoms in the lattice and are termed substitutional impurities. Since the doped silicon behaves electrically as $p$-type or $n$-type material depending on the type of impurity present, regions of $p$-type and $n$-type material can be formed by solid-state diffusion.

The nature of the diffusion process is illustrated by the conceptual example shown in Figs. 2.3 and 2.4. We assume that the silicon sample initially contains a uniform concentration of $n$ type impurity of $10^{15}$ atoms per cubic centimeter. Commonly used $n$-type impurities in silicon are phosphorus, arsenic, and antimony. We further assume that by some means we deposit atoms of $p$-type impurity on the top surface of the silicon sample. The most commonly used
image_name:Figure 2.3
description:The image consists of two parts: a graph and a schematic diagram.

1. **Graph of Resistivity vs. Impurity Concentration:**
- The graph is plotted with impurity concentration on the x-axis, labeled as "Impurity concentration (cm⁻³)", ranging from $10^{14}$ to $10^{20}$.
- The y-axis represents resistivity, labeled as "Resistivity $\rho$ (Ω·cm)", ranging from 0.0001 to 100.
- Two curves are shown, one for $n$-type and one for $p$-type semiconductors, indicating how resistivity changes with impurity concentration.
- Both curves show a general trend of decreasing resistivity with increasing impurity concentration, with the $p$-type curve slightly higher than the $n$-type curve.

2. **Schematic Diagram of Silicon Sample:**
- The lower part of the image shows a schematic of an $n$-type silicon sample.
- The sample is depicted as a rectangular block labeled "n-type sample."
- Boron atoms, represented by dots, are shown deposited on the surface of the silicon sample. This is labeled as "Boron atoms on surface."
- An arrow labeled with "x" indicates the direction, likely representing the direction of diffusion or analysis.

**Key Features and Annotations:**
- The graph clearly distinguishes between $n$-type and $p$-type resistivity changes with impurity concentration.
- The schematic diagram illustrates the initial setup for diffusion, showing boron as the $p$-type impurity deposited on an $n$-type silicon substrate, which is a common process in semiconductor fabrication.

Impurity concentration, atoms $/ \mathrm{cm}^{3}$
image_name:Impurity concentration, atoms $/ \mathrm{cm}^{3}$
description:The graph titled 'Impurity concentration, atoms $/ \mathrm{cm}^{3}$' is a logarithmic plot that displays impurity concentration versus depth in a silicon substrate. The x-axis represents the depth, $x$, in micrometers (μm), and the y-axis shows the impurity concentration in atoms per cubic centimeter (atoms/cm³).

Axes Labels and Units:
- **X-axis:** Depth, $x$ (μm)
- **Y-axis:** Impurity concentration (atoms/cm³)
- The y-axis is logarithmic, ranging from $10^{15}$ to $10^{19}$ atoms/cm³.

Overall Behavior and Trends:
- The graph shows two main impurity concentration profiles labeled as $N_A$ and $N_D$.
- $N_A$ represents the concentration of acceptor atoms, which are typically $p$-type impurities like boron.
- $N_D$ indicates the concentration of donor atoms, which are $n$-type impurities.
- The concentration $N_A$ starts at a high level near the surface and decreases with increasing depth, suggesting a diffusion profile typical for $p$-type impurities pre-deposited on an $n$-type substrate.
- $N_D$ is shown as a constant line, indicating a uniform donor concentration throughout the depth.

Key Features and Technical Details:
- The graph highlights the predeposition step where $p$-type impurities (boron) are introduced on an $n$-type silicon substrate.
- The $N_A$ curve shows a decreasing trend with depth, illustrating the diffusion of boron into the silicon.
- The $N_D$ line is horizontal, implying no change in donor concentration with depth.

Annotations and Specific Data Points:
- The graph includes annotations for $N_A$ and $N_D$, indicating the respective impurity concentrations.
- Specific numerical values are not provided for key data points, but the logarithmic scale gives a clear indication of concentration levels.

Figure 2.3 An $n$-type silicon sample with boron deposited on the surface.
$p$-type impurity in silicon device fabrication is boron. The distribution of impurities prior to the diffusion step is illustrated in Fig. 2.3. The initial placement of the impurity atoms on the surface of the silicon is called the predeposition step and can be accomplished by a number of different techniques.

If the sample is now subjected to a high temperature of about $1100^{\circ} \mathrm{C}$ for a time of about one hour, the impurities diffuse into the sample, as illustrated in Fig. 2.4. Within the silicon, the regions in which the $p$-type impurities outnumber the original $n$-type impurities display $p$-type electrical behavior, whereas the regions in which the $n$-type impurities are more numerous
image_name:Figure 2.4 Distribution of impurities after diffusion
description:The graph titled 'Figure 2.4 Distribution of impurities after diffusion' is a concentration profile of impurities within a silicon sample, illustrating the diffusion process. This is a line graph depicting impurity concentration as a function of depth in the silicon.

1. **Type of Graph and Function:**
- The graph is a concentration profile, showing how impurity concentration varies with depth in the silicon sample.

2. **Axes Labels and Units:**
- The vertical axis represents impurity concentration, labeled as 'Impurity concentration, atoms/cm³', and is scaled logarithmically from 10¹⁵ to 10¹⁹ atoms/cm³.
- The horizontal axis represents depth, labeled as 'Depth, x (µm)', with no specific numerical values marked, indicating a qualitative representation.

3. **Overall Behavior and Trends:**
- The graph shows a steep decrease in the concentration of acceptor impurities (denoted as N_A) from a high value near the surface to a lower value as depth increases.
- The donor impurity concentration (denoted as N_D) is constant, represented by a horizontal dashed line at approximately 10¹⁵ atoms/cm³.
- The graph indicates the formation of a p-n junction where the concentration of acceptor impurities (p-type behavior) exceeds that of donor impurities (n-type behavior).

4. **Key Features and Technical Details:**
- The point where the N_A curve intersects with the N_D line marks the junction depth where the transition from p-type to n-type behavior occurs.
- The graph illustrates the diffusion of boron atoms (p-type) into an n-type silicon sample, resulting in a p-n junction.

5. **Annotations and Specific Data Points:**
- The graph includes annotations indicating the diffusion of boron atoms into the sample and the p-n junction formation.
- The concentration of donor impurities (N_D) is constant at 10¹⁵ atoms/cm³, while the acceptor impurity concentration (N_A) decreases with depth.

This graph effectively demonstrates how impurity diffusion creates a p-n junction in a silicon sample, with a clear depiction of impurity concentration changes with depth.

Figure 2.4 Distribution of impurities after diffusion.
display $n$-type electrical behavior. The diffusion process has allowed the formation of a $p n$ junction within the continuous crystal of silicon material. The depth of this junction from the surface varies from $0.1 \mu \mathrm{~m}$ to $20 \mu \mathrm{~m}$ for silicon integrated-circuit diffusions (where $1 \mu \mathrm{~m}=1$ micrometer $=10^{-6} \mathrm{~m}$ ).

### 2.2.3 Electrical Properties of Diffused Layers

The result of the diffusion process is often a thin layer near the surface of the silicon sample that has been converted from one impurity type to another. Silicon devices and integrated circuits are constructed primarily from these layers. From an electrical standpoint, if the $p n$ junction formed by this diffusion is reverse biased, then the layer is electrically isolated from the underlying material by the reverse-biased junction, and the electrical properties of the layer itself can be measured. The electrical parameter most often used to characterize such layers is the sheet resistance. To define this quantity, consider the resistance of a uniformly doped sample of length $L$, width $W$, thickness $T$, and $n$-type doping concentration $N_{D}$, as shown in Fig. 2.5. The resistance is

$$
R=\frac{\rho L}{W T}=\frac{1}{\sigma} \frac{L}{W T}
$$

image_name:Figure 2.5 Rectangular sample for calculation of sheet resistance
description:The image depicts a rectangular sample used for calculating sheet resistance. It is a three-dimensional block with a rectangular cross-section, represented in a schematic diagram. The block is labeled with three key dimensions: length (L), width (W), and thickness (T).

1. **Identification of Components and Structure:**
- The block is shown in a perspective view, emphasizing its rectangular shape.
- The dimensions are marked with arrows indicating the direction of measurement for length (L), width (W), and thickness (T).
- The cross-section at one end of the block is shaded to denote the thickness (T).

2. **Connections and Interactions:**
- There are no visible electrical connections, wiring, or PCB traces shown in the diagram.
- The image is purely a geometric representation for conceptual understanding, focusing on the physical dimensions relevant to calculating sheet resistance.

3. **Labels, Annotations, and Key Features:**
- The dimensions L, W, and T are clearly labeled, which are critical parameters in the formula for calculating resistance.
- The diagram does not include additional annotations like voltage values or material properties, as it primarily serves to illustrate the geometric relationship needed for the resistance calculation.

The image is a straightforward schematic representation aimed at helping visualize the parameters involved in the calculation of sheet resistance for a uniformly doped sample.

Figure 2.5 Rectangular sample for calculation of sheet resistance.

Substitution of the expression for conductivity $\sigma$ from (2.8) gives

$$
\begin{equation*}
R=\left(\frac{1}{q \mu_{n} N_{D}}\right) \frac{L}{W T}=\frac{L}{W}\left(\frac{1}{q \mu_{n} N_{D} T}\right)=\frac{L}{W} R_{\square} \tag{2.10}
\end{equation*}
$$

Quantity $R_{\square}$ is the sheet resistance of the layer and has units of Ohms. Since the sheet resistance is the resistance of any square sheet of material with thickness $T$, its units are often given as Ohms per square ( $\Omega / \square$ ) rather than simply Ohms. The sheet resistance can be written in terms of the resistivity of the material, using (2.8), as

$$
\begin{equation*}
R_{\square}=\frac{1}{q \mu_{n} N_{D} T}=\frac{\rho}{T} \tag{2.11}
\end{equation*}
$$

The diffused layer illustrated in Fig. 2.6 is similar to this case except that the impurity concentration is not uniform. However, we can consider the layer to be made up of a parallel combination of many thin conducting sheets. The conducting sheet of thickness $d x$ at depth $x$ has a conductance

$$
\begin{equation*}
d G=q\left(\frac{W}{L}\right) \mu_{n} N_{D}(x) d x \tag{2.12}
\end{equation*}
$$

To find the total conductance, we sum all the contributions.

$$
\begin{equation*}
G=\int_{0}^{x_{j}} q \frac{W}{L} \mu_{n} N_{D}(x) d x=\frac{W}{L} \int_{0}^{x_{j}} q \mu_{n} N_{D}(x) d x \tag{2.13}
\end{equation*}
$$

Inverting (2.13), we obtain

$$
\begin{equation*}
R=\frac{L}{W}\left[\frac{1}{\int_{0}^{x_{j}} q \mu_{n} N_{D}(x) d x}\right] \tag{2.14}
\end{equation*}
$$

image_name:Figure 2.6 Calculation of the resistance of a diffused layer
description:The image depicts a rectangular prism representing a diffused layer, used to calculate resistance. The prism is oriented with its length extending horizontally and is labeled with several dimensions and annotations. The key components and features are as follows:

1. **Dimensions and Structure:**
- The prism has a length labeled as \(L\), a width labeled as \(W\), and a thickness labeled as \(T\).
- The cross-section of the prism is rectangular, and the front face is labeled as \(A\), while a small segment within it is labeled \(dx\), indicating an infinitesimal element of the length.

2. **Connections and Interactions:**
- The diagram represents a conceptual model rather than a physical connection of components. It is used to illustrate the calculation of resistance in a diffused layer, with the variable \(x\) indicating a position along the length where measurements or calculations are considered.

3. **Labels and Annotations:**
- The diagram includes arrows indicating the dimensions \(L\), \(W\), and \(T\), providing a clear understanding of the spatial orientation and size.
- The notation \(dx\) is used to denote a differential element along the length \(L\), which is important for integrating over the length to find total resistance.
- The point \(A'\) is marked to indicate the starting point for measuring \(dx\) along \(x\).

This diagram is a high-level representation used in the context of calculating the resistance of a diffused layer by integrating over its length, as described in the surrounding mathematical equations.

Impurity concentration, atoms $/ \mathrm{cm}^{3}$
image_name:Figure 2.6
description:The graph in Figure 2.6 represents the net impurity concentration along a diffused layer. It is a line graph that plots the net donor impurity concentration, denoted as \( N_D(x) \), against the position \( x \) along the layer.

1. **Type of Graph and Function:**
- The graph is a plot of impurity concentration versus position, showing how the concentration of donor atoms changes along the length of the material.

2. **Axes Labels and Units:**
- The horizontal axis represents the position \( x \), with a starting point labeled \( A \) and extending towards \( A' \). The axis is likely in units of length, such as centimeters or micrometers, although specific units are not provided.
- The vertical axis represents the donor impurity concentration \( N_D(x) \), typically measured in atoms per cubic centimeter \( \text{atoms/cm}^3 \).

3. **Overall Behavior and Trends:**
- The graph shows a decreasing trend in impurity concentration from left to right. The curve starts with a high concentration at point \( A \) and decreases as it moves towards \( A' \).
- The curve is smooth and appears to follow an exponential decay pattern, indicating a rapid drop in concentration initially, which then tapers off.

4. **Key Features and Technical Details:**
- The graph includes an annotation for a differential element \( dx \), indicating the infinitesimal length over which the concentration is measured.
- The notation \( T \) suggests a characteristic thickness or diffusion depth where the concentration changes significantly.
- The expression \( N_D(x) - N_A(x) \approx N_D(x) \) indicates that the net impurity concentration is approximately equal to the donor concentration, assuming acceptor concentration \( N_A(x) \) is negligible.

5. **Annotations and Specific Data Points:**
- The graph is annotated with arrows and text explaining the net impurity concentration. The differential element \( dx \) is marked along the \( x \)-axis, emphasizing the integration aspect needed for calculating resistance.
- No specific numerical values are provided for the concentrations or positions, focusing instead on the conceptual representation of impurity distribution.

Figure 2.6 Calculation of the resistance of a diffused layer.

Comparison of (2.10) and (2.14) gives

$$
\begin{equation*}
R_{\square}=\left[\int_{0}^{x_{j}} q \mu_{n} N_{D}(x) d x\right]^{-1} \simeq\left[q \bar{\mu}_{n} \int_{0}^{x_{j}} N_{D}(x) d x\right]^{-1} \tag{2.15}
\end{equation*}
$$

where $\bar{\mu}_{n}$ is the average mobility. Thus (2.10) can be used for diffused layers if the appropriate value of $R_{\square}$ is used. Equation 2.15 shows that the sheet resistance of the diffused layer depends on the total number of impurity atoms in the layer per unit area. The depth $x_{j}$ in (2.13), (2.14), and (2.15) is actually the distance from the surface to the edge of the junction depletion layer, since the donor atoms within the depletion layer do not contribute to conduction. Sheet resistance is a useful parameter for the electrical characterization of diffusion processes and is a key parameter in the design of integrated resistors. The sheet resistance of a diffused layer is easily measured in the laboratory; the actual evaluation of (2.15) is seldom necessary.

#### EXAMPLE

Calculate the resistance of a layer with length $50 \mu \mathrm{~m}$ and width $5 \mu \mathrm{~m}$ in material of sheet resistance $200 \Omega / \square$.

From (2.10)

$$
R=\frac{50}{5} \times 200 \Omega=2 \mathrm{k} \Omega
$$

Note that this region constitutes 10 squares in series, and $R$ is thus 10 times the sheet resistance.

In order to use these diffusion process steps to fabricate useful devices, the diffusion must be restricted to a small region on the surface of the sample rather than the entire planar surface. This restriction is accomplished with photolithography.

### 2.2.4 Photolithography

When a sample of crystalline silicon is placed in an oxidizing environment, a layer of silicon dioxide will form at the surface. This layer acts as a barrier to the diffusion of impurities, so that impurities separated from the surface of the silicon by a layer of oxide do not diffuse into the silicon during high-temperature processing. A pn junction can thus be formed in a selected location on the sample by first covering the sample with a layer of oxide (called an oxidation step), removing the oxide in the selected region, and then performing a predeposition and diffusion step. The selective removal of the oxide in the desired areas is accomplished with photolithography. This process is illustrated by the conceptual example of Fig. 2.7. Again we assume the starting material is a sample of $n$-type silicon. We first perform an oxidation step in which a layer of silicon dioxide $\left(\mathrm{SiO}_{2}\right)$ is thermally grown on the top surface, usually of thickness of $0.2 \mu \mathrm{~m}$ to $1 \mu \mathrm{~m}$. The wafer following this step is shown in Fig. 2.7a. Then the sample is coated with a thin layer of photosensitive material called photoresist. When this material is exposed to a particular wavelength of light, it undergoes a chemical change and, in the case of positive photoresist, becomes soluble in certain chemicals in which the unexposed photoresist is insoluble. The sample at this stage is illustrated in Fig. 2.7b. To define the desired diffusion areas on the silicon sample, a photomask is placed over the surface of the sample; this photomask is opaque except for clear areas where the diffusion is to take place. Light of the appropriate wavelength is directed at the sample, as shown in Fig. 2.7c, and falls on the photoresist only in the clear areas of the mask. These areas of the resist are then chemically
image_name:(a)
description:The image labeled as '(a)' illustrates the initial step in the photolithography process used to form a pn junction diode. In this step, a thin layer of silicon dioxide (SiO2) is grown on the surface of an n-type silicon wafer. This layer acts as a protective barrier for the silicon substrate beneath. The diagram shows a cross-sectional view of the wafer, with the SiO2 layer clearly marked on top of the n-type silicon. This SiO2 layer is crucial as it provides a base for the subsequent application of photoresist and the patterning process that will define the regions for impurity diffusion.
image_name:(b)
description:The image labeled as (b) in Figure 2.7 illustrates the second step in the photolithography process used to form a pn junction diode. In this step, a layer of photoresist is applied to the surface of an n-type silicon wafer, which is already coated with a thin layer of silicon dioxide (SiO2). The diagram shows a cross-sectional view of the wafer, with the SiO2 layer represented as a thin line on top of the n-type silicon substrate. The photoresist layer is depicted as a slightly thicker line above the SiO2 layer.

**1. Identification of Components and Structure:**
- **n-type Wafer:** The main body of the diagram is the n-type silicon wafer, which serves as the substrate for the photolithography process.
- **SiO2 Layer:** A thin layer of silicon dioxide covers the n-type wafer, serving as a protective and insulating layer.
- **Photoresist Layer:** A layer of photoresist is applied on top of the SiO2, ready for exposure to light in the subsequent steps.

**2. Connections and Interactions:**
- At this stage, there are no electrical connections or interactions visible in the diagram. The focus is on the preparation of the wafer surface for patterning through photolithography.

**3. Labels, Annotations, and Key Features:**
- The diagram is labeled with the materials present: 'SiO2', 'n-type wafer', and 'Photoresist'. These labels help in identifying the layers involved in this step of the process.

This step is crucial as it prepares the wafer for the selective exposure to light, which will define the areas where diffusion of impurities will eventually occur, leading to the formation of a pn junction.
image_name:(c)
description:The image labeled as (c) in Figure 2.7 illustrates a step in the photolithography process for forming a pn junction diode. The key components and structure visible in this step include:

1. **n-type Wafer and SiO2 Layer**: The diagram shows a cross-section of an n-type silicon wafer with a thin layer of silicon dioxide (SiO2) on top. This layer acts as a mask during the diffusion process.

2. **Photoresist Layer**: Over the SiO2 layer, a photoresist has been applied. This photoresist is sensitive to light and will be used to define areas where the SiO2 will be etched away.

3. **Photomask**: A mask is placed over the wafer. This mask is opaque with clear areas that allow light to pass through only in specific regions where the photoresist needs to be exposed.

4. **Light Exposure**: Light of the appropriate wavelength is directed at the sample. The arrows in the diagram indicate the direction of the light, showing that it passes through the clear areas of the mask and exposes the photoresist in those regions.

5. **Exposure Process**: The exposed areas of the photoresist will become soluble in the development step that follows. The unexposed areas remain insoluble, protecting the underlying SiO2 from being etched away.

This step is crucial for defining the regions on the wafer where diffusion of impurities will occur, ultimately forming the pn junction in the diode.
image_name:(d)
description:The image shows a step-by-step schematic of the photolithography process used to form a pn junction diode on an n-type silicon wafer. The diagram is divided into six stages labeled (a) through (f):

1. **(a) Grow SiO2:** The first stage shows an n-type silicon wafer with a layer of silicon dioxide (SiO2) grown on its surface. This SiO2 layer acts as a protective mask for the underlying silicon.

2. **(b) Apply Photoresist:** A layer of photoresist is applied over the SiO2 layer. The photoresist is sensitive to light and will be used to define the areas where diffusion will occur.

3. **(c) Expose through Mask:** Light is directed at the wafer through a photomask. The mask has clear areas where light can pass through, exposing the photoresist in those regions. The exposed photoresist undergoes chemical changes.

4. **(d) Develop Photoresist:** The exposed photoresist is chemically dissolved during development, leaving behind a pattern that matches the clear areas of the mask. This creates openings or "windows" in the photoresist layer.

5. **(e) Etch SiO2 and Remove Photoresist:** The SiO2 layer is etched away in the areas where the photoresist was removed, exposing the underlying silicon. After etching, the remaining photoresist is stripped off, leaving a window in the SiO2 layer.

6. **(f) Predeposit and Diffuse Impurities:** P-type impurities are introduced into the exposed silicon areas through the windows in the SiO2 layer. This diffusion process forms p-type regions in the n-type wafer, creating pn junctions necessary for diode function.

Key features include the use of a photomask to selectively expose areas of the photoresist, the development of the photoresist to reveal patterns, and the etching of SiO2 to allow impurity diffusion into the silicon substrate.
image_name:(e)
description:The image labeled as '(e)' is part of a sequence illustrating the photolithography process used to form a pn junction diode. In this step, the diagram shows a cross-section of an n-type silicon wafer. The previously applied photoresist and areas of silicon dioxide (SiO2) have been removed, revealing a 'window' where the SiO2 layer has been etched away.

1. **Identification of Components and Structure:**
- The n-type silicon wafer is the primary substrate visible in the diagram.
- The SiO2 layer has been etched away in a specific area, creating a 'window' on the surface of the wafer.
- The photoresist, which was used to protect certain areas during etching, has been removed.

2. **Connections and Interactions:**
- The diagram does not show electrical connections or interactions, as it focuses on the physical preparation of the silicon surface for subsequent processing steps.
- The 'window' is prepared for the introduction of impurities, which will occur in the next step to form the p-type region.

3. **Labels, Annotations, and Key Features:**
- The term 'Window' is labeled to indicate the etched area where the SiO2 has been removed.
- The n-type region is labeled to show the type of silicon wafer used.
- This step is crucial for defining the areas where diffusion of impurities will occur to create the diode's p-n junction.
image_name:(f)
description:The image illustrates the final step (f) in a series of diagrams depicting the photolithography process used to form a pn junction diode on a silicon wafer. This step shows the predeposition and diffusion of impurities to form the pn junction.

1. **Identification of Components and Structure:**
- The diagram shows an n-type silicon wafer with a window etched into the SiO2 layer, exposing a portion of the silicon surface.
- P-type impurities are being introduced into the exposed n-type silicon through the window.
- The diffusion of these impurities creates a p-type region within the n-type substrate, forming a pn junction.

2. **Connections and Interactions:**
- The arrows labeled as "p-type impurities" indicate the direction of impurity diffusion into the silicon substrate.
- There is no direct electrical connection shown in this diagram, as it is focused on the chemical diffusion process.

3. **Labels, Annotations, and Key Features:**
- The label "p" indicates the newly formed p-type region within the n-type wafer.
- The arrows pointing towards the silicon wafer are labeled "p-type impurities," signifying the introduction of dopants to create the pn junction.
- The term "Window" is used to denote the area where the SiO2 has been removed, allowing for impurity diffusion.

This step is crucial in semiconductor manufacturing as it establishes the fundamental structure of a pn junction, which is essential for diode operation.

Figure 2.7 Conceptual example of the use of photolithography to form a pn junction diode. (a) Grow $\mathrm{SiO}_{2}$. (b) Apply photoresist. (c) Expose through mask. (d) Develop photoresist. (e) Etch $\mathrm{SiO}_{2}$ and remove photoresist. ( $f$ ) Predeposit and diffuse impurities.
dissolved in the development step, as shown in Fig. 2.7d. The unexposed areas of the photoresist are impervious to the developer.

Since the objective is the formation of a region clear of $\mathrm{SiO}_{2}$, the next step is the etching of the oxide. This step can be accomplished by dipping the sample in an etching solution, such as hydrofluoric acid, or by exposing it to an electrically produced plasma in a plasma etcher. In either case, the result is that in the regions where the photoresist has been removed, the oxide is etched away, leaving the bare silicon surface.

The remaining photoresist is next removed by a chemical stripping operation, leaving the sample with holes, or windows, in the oxide at the desired locations, as shown in Fig. 2.7e. The sample now undergoes a predeposition and diffusion step, resulting in the formation of $p$-type regions where the oxide had been removed, as shown in Fig. 2.7f. In some instances, the impurity to be locally added to the silicon surface is deposited by using ion implantation (see Section 2.2.6). This method of insertion can often take place through the silicon dioxide so that the oxide-etch step is unnecessary.

The minimum dimension of the diffused region that can be routinely formed with this technique in device production has decreased with time, and at present is approximately $0.1 \mu \mathrm{~m} \times 0.1 \mu \mathrm{~m}$. The number of such regions that can be fabricated simultaneously can be calculated by noting that the silicon sample used in the production of integrated circuits is a round slice, typically 4 inches to 12 inches in diameter and $250 \mu \mathrm{~m}$ thick. Thus the number of electrically independent $p n$ junctions of dimension $0.1 \mu \mathrm{~m} \times 0.1 \mu \mathrm{~m}$ spaced $0.1 \mu \mathrm{~m}$ apart that can be formed on one such wafer is on the order of $10^{12}$. In actual integrated circuits, a number of masking and diffusion steps are used to form more complex structures such as transistors, but the key points are that photolithography is capable of defining a large number of devices on the surface of the sample and that all of these devices are batch fabricated at the same time. Thus the cost of the photomasking and diffusion steps applied to the wafer during the process is divided among the devices or circuits on the wafer. This ability to fabricate hundreds or thousands of devices at once is the key to the economic advantage of IC technology.
image_name:Figure 2.8 Triple-diffused transistor
description:The image titled "Figure 2.8 Triple-diffused transistor" consists of two main parts: a schematic cross-sectional view of a triple-diffused bipolar transistor and a graph showing the impurity concentration profile.

1. **Identification of Components and Structure:**
- The cross-sectional diagram at the top illustrates a triple-diffused transistor structure. It shows a p-type substrate with three distinct regions labeled as E (Emitter), B (Base), and C (Collector). The emitter and collector regions are n-type, while the base region is p-type.
- The n-type emitter region is diffused into the p-type base, and the n-type collector region is diffused into the p-type substrate.

2. **Connections and Interactions:**
- The diagram indicates the flow of current and signal interactions between the emitter, base, and collector regions. The emitter injects electrons into the base, which are then collected by the collector region. The base serves as a control region for the transistor's operation.
- There are no explicit wiring connections shown, as the focus is on the diffusion profile and semiconductor junctions.

3. **Labels, Annotations, and Key Features:**
- The lower part of the image presents a graph plotting impurity concentration (atoms/cm³) against depth (x in micrometers) into the substrate.
- The graph shows three curves representing emitter diffusion (n-type), base diffusion (p-type), and collector diffusion (n-type). The background p-type concentration is also indicated.
- The impurity concentration for the emitter is the highest, followed by the base and collector, illustrating the diffusion process and depth of each region within the substrate.
- The graph helps visualize how the impurity levels change with depth, critical for understanding the electrical characteristics of the transistor.
image_name:Figure 2.8 Triple-diffused transistor and resulting impurity profile
description:The graph in Figure 2.8 illustrates the impurity concentration profile of a triple-diffused bipolar transistor. It is a plot showing impurity concentration as a function of depth within the semiconductor material.

1. **Type of Graph and Function:**
- This is a semi-logarithmic plot, where the y-axis (impurity concentration) is on a logarithmic scale, and the x-axis (depth) is on a linear scale.

2. **Axes Labels and Units:**
- The y-axis represents impurity concentration in atoms per cubic centimeter (atoms/cm³), ranging from 10¹⁵ to 10²¹.
- The x-axis represents depth in micrometers (µm), ranging from 0 to about 7 µm.

3. **Overall Behavior and Trends:**
- The graph shows three distinct diffusion profiles: emitter, base, and collector.
- The emitter diffusion (n-type) starts with a high concentration of about 10²⁰ atoms/cm³ near the surface (0 µm) and decreases sharply as depth increases.
- The base diffusion (p-type) has a peak concentration around 10¹⁸ atoms/cm³ and forms a hump between the emitter and collector regions.
- The collector diffusion (n-type) begins at a lower concentration than the emitter, gradually decreasing with depth.
- A background concentration is marked as a dashed line at approximately 10¹⁶ atoms/cm³, representing the p-type substrate.

4. **Key Features and Technical Details:**
- The emitter diffusion has the highest concentration at the surface, indicating a heavily doped n-type region.
- The base region is characterized by a distinct peak, indicating a localized increase in p-type doping.
- The collector diffusion shows a more gradual decrease, suggesting a less abrupt transition compared to the emitter.
- The intersection points of the diffusion profiles indicate junction depths and transitions between different regions of the transistor.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for each diffusion type: 'Emitter diffusion (n)', 'Base diffusion (p)', and 'Collector diffusion (n)'.
- The background level is indicated by a horizontal dashed line, marking the base p-type substrate concentration.
- Key depth points are noted, such as the emitter diffusion dropping significantly around 2 µm, and the base diffusion peaking near 3 µm.

Figure 2.8 Triple-diffused transistor and resulting impurity profile.

### 2.2.5 Epitaxial Growth

Early planar transistors and the first integrated circuits used only photomasking and diffusion steps in the fabrication process. However, all-diffused integrated circuits had severe limitations compared with discrete component circuits. In a triple-diffused bipolar transistor, as illustrated in Fig. 2.8, the collector region is formed by an $n$-type diffusion into the $p$-type wafer. The drawbacks of this structure are that the series collector resistance is high and the collector-toemitter breakdown voltage is low. The former occurs because the impurity concentration in the portion of the collector diffusion below the collector-base junction is low, giving the region high resistivity. The latter occurs because the concentration of impurities near the surface of the collector is relatively high, resulting in a low breakdown voltage between the collector and base diffusions at the surface, as described in Chapter 1. To overcome these drawbacks, the impurity concentration should be low at the collector-base junction for high breakdown voltage but high below the junction for low collector resistance. Such a concentration profile cannot be realized with diffusions alone, and the epitaxial growth technique was adopted as a result.

Epitaxial (epi) growth consists of formation of a layer of single-crystal silicon on the surface of the silicon sample so that the crystal structure of the silicon is continuous across the interface. The impurity concentration in the epi layer can be controlled independently and can be greater or smaller than in the substrate material. In addition, the epi layer is often of opposite impurity type from the substrate on which it is grown. The thickness of epi layers used in integrated-circuit fabrication varies from $1 \mu \mathrm{~m}$ to $20 \mu \mathrm{~m}$, and the growth of the layer is accomplished by placing the wafer in an ambient atmosphere containing silicon tetrachloride $\left(\mathrm{SiCl}_{4}\right)$ or silane $\left(\mathrm{SiH}_{4}\right)$ at an elevated temperature. A chemical reaction takes place in which elemental silicon is deposited on the surface of the wafer, and the resulting surface layer of
silicon is crystalline in structure with few defects if the conditions are carefully controlled. Such a layer is suitable as starting material for the fabrication of bipolar transistors. Epitaxy is also utilized in some CMOS and most BiCMOS technologies.

### 2.2.6 Ion Implantation

Ion implantation is a technique for directly inserting impurity atoms into a silicon wafer. ${ }^{5,6}$ The wafer is placed in an evacuated chamber, and ions of the desired impurity species are directed at the sample at high velocity. These ions penetrate the surface of the silicon wafer to an average depth of from less than $0.1 \mu \mathrm{~m}$ to about $0.6 \mu \mathrm{~m}$, depending on the velocity with which they strike the sample. The wafer is then held at a moderate temperature for a period of time (for example, $800^{\circ} \mathrm{C}$ for 10 minutes) in order to allow the ions to become mobile and fit into the crystal lattice. This is called an anneal step and is essential to allow repair of any crystal damage caused by the implantation. The principal advantages of ion implantation over conventional diffusion are (1) that small amounts of impurities can be reproducibly deposited, and (2) that the amount of impurity deposited per unit area can be precisely controlled. In addition, the deposition can be made with a high level of uniformity across the wafer. Another useful property of ion-implanted layers is that the peak of the impurity concentration profile can be made to occur below the surface of the silicon, unlike with diffused layers. This allows the fabrication of implanted bipolar structures with properties that are significantly better than those of diffused devices. This technique is also widely applied in MOS technology where small, well-controlled amounts of impurity are required at the silicon surface for adjustment of device thresholds, as described in Section 1.5.1.

### 2.2.7 Local Oxidation

In both MOS and bipolar technologies, the need often arises to fabricate regions of the silicon surface that are covered with relatively thin silicon dioxide, adjacent to areas covered by relatively thick oxide. Typically, the former regions constitute the active-device areas, whereas the latter constitute the regions that electrically isolate the devices from each other. A second requirement is that the transition from thick to thin regions must be accomplished without introducing a large vertical step in the surface geometry of the silicon, so that the metallization and other patterns that are later deposited can lie on a relatively planar surface. Local oxidation is used to achieve this result. The local oxidation process begins with a sample that already has a thin oxide grown on it, as shown in Fig. 2.9a. First a layer of silicon nitride ( SiN ) is deposited on the sample and subsequently removed with a masking step from all areas where thick oxide is to be grown, as shown in Fig. 2.9b. Silicon nitride acts as a barrier to oxygen
image_name:Fig. 2.9a
description:Fig. 2.9a illustrates the initial stage of a local oxidation process on a silicon wafer. In this diagram, the silicon substrate is shown with a thin layer of silicon dioxide (SiO2) already grown on its surface. This oxide layer serves as the starting point for further processing. The image depicts a cross-sectional view of the silicon wafer, focusing on the interface between the silicon and the thin oxide layer. The thin oxide appears as a uniform, continuous layer on top of the silicon substrate, providing a clear baseline for subsequent steps in the local oxidation process. There are no additional components or structures visible in this stage, as it represents the initial state before any further deposition or patterning occurs. The diagram does not include any labels or annotations, focusing solely on the depiction of the silicon and oxide layers.
image_name:Fig. 2.9b
description:The image labeled "Fig. 2.9b" illustrates a stage in the local oxidation process used in semiconductor fabrication. In this figure, a silicon substrate is shown with a thin layer of silicon dioxide (SiO2) already present on its surface. A layer of silicon nitride (SiN) has been deposited over the entire surface, serving as a mask to control the oxidation process.

1. **Identification of Components and Structure:**
- **Silicon Substrate:** The base material upon which other layers are deposited.
- **Silicon Dioxide (SiO2) Layer:** A thin oxide layer initially grown on the silicon substrate.
- **Silicon Nitride (SiN) Layer:** A deposited layer acting as an oxidation barrier.

2. **Connections and Interactions:**
- The silicon nitride layer covers the silicon dioxide, preventing oxygen from reaching the silicon surface in areas where the nitride is present. This selective masking allows for controlled oxidation only in areas where the nitride has been removed.

3. **Labels, Annotations, and Key Features:**
- The diagram likely includes annotations indicating which areas will undergo oxidation and which will remain protected by the nitride layer. These annotations help in understanding the selective oxidation process and its impact on the substrate's surface topology.

Overall, this figure is part of a sequence demonstrating how local oxidation is used to create a planar surface for subsequent metallization and patterning in semiconductor devices.
image_name:Fig. 2.9c
description:The image labeled "Fig. 2.9c" depicts the result of a local oxidation process on a silicon wafer. The diagram illustrates the cross-sectional view of the silicon substrate after the removal of silicon nitride and the growth of thick oxide in the exposed regions.

1. **Identification of Components and Structure:**
- The base layer is the silicon substrate.
- There are regions with thick silicon dioxide (SiO2) and thin silicon dioxide.
- The thick oxide regions are where the silicon nitride was removed before oxidation.
- The thin oxide regions were covered by silicon nitride during oxidation.

2. **Connections and Interactions:**
- The silicon dioxide forms a smooth transition between thick and thin areas, indicating a gradual change in oxide thickness.
- The oxidation process consumes silicon beneath the thick oxide regions, leading to a reduction in the height of these areas compared to the difference in oxide thickness.

3. **Labels, Annotations, and Key Features:**
- The diagram may include labels indicating the materials (Si, SiO2) and the regions where nitride was present.
- Annotations might highlight the smooth transition and the absence of oxidation under the nitride-covered areas.
- The purpose of the illustration is to show the effectiveness of silicon nitride as an oxidation barrier and the resulting topography of the silicon wafer after the process.
a subsequent long, high-temperature oxidation step is carried out, a thick oxide is grown in the regions where there is no nitride, but no oxidation takes place under the nitride. The resulting geometry after nitride removal is shown in Fig. 2.9c. Note that the top surface of the silicon dioxide has a smooth transition from thick to thin areas and that the height of this transition is less than the oxide thickness difference because the oxidation in the thick oxide regions consumes some of the underlying silicon.

### 2.2.8 Polysilicon Deposition

Many process technologies utilize layers of polycrystalline silicon that are deposited during fabrication. After deposition of the polycrystalline silicon layer on the wafer, the desired features are defined by using a masking step and can serve as gate electrodes for silicon-gate MOS
image_name:(a)
description:The image illustrates the local oxidation process through three stages, labeled (a), (b), and (c).

1. **Stage (a):** This shows a silicon (Si) substrate with a uniform layer of silicon dioxide (SiO2) on top. The SiO2 acts as a protective layer for the silicon beneath.

2. **Stage (b):** In this stage, a layer of silicon nitride (SiN) is deposited on top of the silicon dioxide. The SiN layer is selectively deposited, leaving some areas of the SiO2 exposed. The SiN acts as a mask, preventing oxidation in the areas it covers.

3. **Stage (c):** After the oxidation process, the silicon nitride is removed. The areas that were covered by SiN remain with thin SiO2, while the exposed regions have undergone oxidation, resulting in a thicker SiO2 layer. This differential oxidation creates a step-like profile with thick and thin SiO2 regions.

**Key Features:**
- The SiO2 and SiN layers are clearly labeled, indicating their roles in the oxidation process.
- The thickness variation in SiO2 is a result of the oxidation process, where the underlying silicon is consumed to form the oxide.
- The diagram represents a typical process in semiconductor fabrication for creating isolation regions or defining features on a silicon wafer.
image_name:(b)
description:The diagram illustrates the stages of the local oxidation process in semiconductor fabrication, specifically focusing on the silicon substrate and the deposition of nitride. The image is divided into three parts labeled (a), (b), and (c), representing different stages of the process.

1. **Identification of Components and Structure:**
- **(a) Silicon sample prior to deposition of nitride:** This stage shows a silicon (Si) substrate with an initial layer of silicon dioxide (SiO2) on top. This represents the starting point before any additional layers or processes are applied.
- **(b) After nitride deposition and definition:** In this stage, a silicon nitride (SiN) layer is deposited on top of the silicon dioxide. The SiN is selectively patterned, leaving a strip of SiN on top of the SiO2, which serves as a mask during the subsequent oxidation process.
- **(c) After oxidation and nitride removal:** This final stage shows the result of the oxidation process where the exposed silicon regions (not covered by SiN) have been oxidized to form thicker SiO2 layers. The SiN mask has been removed, leaving a pattern with regions of thick and thin SiO2 on the silicon substrate.

2. **Connections and Interactions:**
- The SiN layer acts as a mask that prevents oxidation in certain areas, allowing for selective thickening of the SiO2 layer. The areas covered by SiN remain with the original SiO2 thickness, while the exposed areas undergo additional oxidation, resulting in a thicker SiO2 layer.

3. **Labels, Annotations, and Key Features:**
- The diagram is clearly labeled with material types such as Si, SiO2, and SiN.
- Annotations include 'Thick SiO2' and 'Thin SiO2,' indicating the outcome of the oxidation process and the selective masking effect of the SiN layer.
- The transitions between the different stages are smooth and clearly depict the progression of the local oxidation process.
image_name:(c)
description:The diagram illustrates the local oxidation process in silicon fabrication, shown in three stages labeled (a), (b), and (c). Each stage represents a different step in the process:

1. **Stage (a) - Initial Setup:**
- The diagram shows a silicon (Si) substrate with a uniform layer of silicon dioxide (SiO₂) on top. This represents the initial state before any further processing.

2. **Stage (b) - Nitride Deposition and Definition:**
- A silicon nitride (SiN) layer is deposited on top of the silicon dioxide layer, covering a specific area while leaving other parts of the SiO₂ exposed. This selective coverage is crucial for the subsequent oxidation step. The silicon substrate remains unchanged beneath these layers.

3. **Stage (c) - Oxidation and Nitride Removal:**
- After the oxidation process, the areas that were not covered by the silicon nitride have undergone further oxidation, resulting in a thicker SiO₂ layer. The diagram shows a distinction between the thick SiO₂ in the exposed areas and the thin SiO₂ where the nitride was present. The silicon nitride layer has been removed at this stage, leaving behind the patterned oxide layers.

**Key Features:**
- The labels "Thick SiO₂" and "Thin SiO₂" indicate the difference in oxide thickness due to the local oxidation process.
- The diagram effectively demonstrates the use of silicon nitride as an oxidation mask to control the growth of silicon dioxide on the silicon substrate.

Figure 2.9 Local oxidation process. (a) Silicon sample prior to deposition of nitride.
(b) After nitride deposition and definition. (c) After oxidation and nitride removal.
transistors, emitters of bipolar transistors, plates of capacitors, resistors, fuses, and interconnect layers. The sheet resistance of such layers can be controlled by the impurity added, much like bulk silicon, in a range from about $20 \Omega / \square$ up to very high values. The process that is used to deposit the layer is much like that used for epitaxy. However, since the deposition is usually over a layer of silicon dioxide, the layer does not form as a single-crystal extension of the underlying silicon but forms as a granular (or polysilicon) film. Some MOS technologies contain as many as three separate polysilicon layers, separated from one another by layers of $\mathrm{SiO}_{2}$.

## 2.3 High-Voltage Bipolar Integrated-Circuit Fabrication

Integrated-circuit fabrication techniques have changed dramatically since the invention of the basic planar process. This change has been driven by developments in photolithography, processing techniques, and also the trend to reduce power-supply voltages in many systems. Developments in photolithography have reduced the minimum feature size attainable from tens of microns to the submicron level. The precise control allowed by ion implantation has resulted in this technique becoming the dominant means of predepositing impurity atoms. Finally, many circuits now operate from 3 V or 5 V power supplies instead of from the $\pm 15 \mathrm{~V}$ supplies used earlier to achieve high dynamic range in stand-alone integrated circuits, such as operational amplifiers. Reducing the operating voltages allows closer spacing between devices in an IC. It also allows shallower structures with higher frequency capability. These effects stem from the fact that the thickness of junction depletion layers is reduced by reducing operating voltages, as described in Chapter 1. Thus the highest-frequency IC processes are designed to operate from $5-\mathrm{V}$ supplies or less and are generally not usable at higher supply voltages. In fact, a fundamental trade-off exists between the frequency capability of a process and its breakdown voltage.

In this section, we examine first the sequence of steps used in the fabrication of highvoltage bipolar integrated circuits using junction isolation. This was the original IC process
image_name:Figure 2.10 Buried-layer diffusion
description:The diagram titled "Figure 2.10 Buried-layer diffusion" illustrates a cross-sectional view of a semiconductor structure used in the fabrication of high-voltage bipolar integrated circuits. The primary components and features in the diagram are as follows:

1. **P-type Substrate:** The base material of the structure is a p-type silicon substrate. This is depicted as a large, dotted region at the bottom of the diagram, indicating the presence of p-type impurities throughout the material.

2. **N+ Buried Layer:** Above the p-type substrate, there is an n+ buried layer. This is shown as a gray, rectangular region embedded within the substrate. The n+ notation indicates a high concentration of n-type dopants, which are used to create a low-resistance path in the semiconductor.

3. **N-type Impurities:** At the surface of the structure, there is a region labeled "n-type impurities." This area is shown as a thin layer at the top of the diagram, suggesting the diffusion of n-type dopants into the substrate. This process is crucial for forming the necessary electrical characteristics of the device.

4. **Diffusion Process:** The diagram visually represents the diffusion process where n-type impurities are introduced into the p-type substrate to form the n+ buried layer. This is a key step in creating junction-isolated bipolar integrated circuits.

Overall, the diagram serves to illustrate the basic structure and process of buried-layer diffusion in semiconductor fabrication, highlighting the interaction between different types of doped regions and their role in forming high-voltage circuits.

Figure 2.10 Buried-layer diffusion.
and is useful as a vehicle to illustrate the basic methods of IC fabrication. It is still used in various forms to fabricate high-voltage circuits.

The fabrication of a junction-isolated bipolar integrated circuit involves a sequence of from six to eight masking and diffusion steps. The starting material is a wafer of $p$-type silicon, usually $250 \mu \mathrm{~m}$ thick and with an impurity concentration of approximately $10^{16}$ atoms $/ \mathrm{cm}^{3}$. We will consider the sequence of diffusion steps required to form an $n p n$ integrated-circuit transistor. The first mask and diffusion step, illustrated in Fig. 2.10, forms a low-resistance n-type layer that will eventually become a low-resistance path for the collector current of the transistor. This step is called the buried-layer diffusion, and the layer itself is called the buried layer. The sheet resistance of the layer is in the range of 20 to $50 \Omega / \square$, and the impurity used is usually arsenic or antimony because these impurities diffuse slowly and thus do not greatly redistribute during subsequent processing.

After the buried-layer step, the wafer is stripped of all oxide and an epi layer is grown, as shown in Fig. 2.11. The thickness of the layer and its $n$-type impurity concentration determine the collector-base breakdown voltage of the transistors in the circuit since this material forms the collector region of the transistor. For example, if the circuit is to operate at a power-supply voltage of 36 V , the devices generally are required to have $B V_{C E O}$ breakdown voltages above this value. As described in Chapter 1, this implies that the plane breakdown voltage in the collector-base junction must be several times this value because of the effects of collector avalanche multiplication. For $B V_{C E O}=36 \mathrm{~V}$, a collector-base plane breakdown voltage of approximately 90 V is required, which implies an impurity concentration in the collector of approximately $10^{15}$ atoms $/ \mathrm{cm}^{3}$ and a resistivity of $5 \Omega-\mathrm{cm}$. The thickness of the epitaxial layer then must be large enough to accommodate the depletion layer associated with the collector-base junction. At 36 V , the results of Chapter 1 can be used to show that the depletionlayer thickness is approximately $6 \mu \mathrm{~m}$. Since the buried layer diffuses outward approximately $8 \mu \mathrm{~m}$ during subsequent processing, and the base diffusion will be approximately $3 \mu \mathrm{~m}$ deep, a total epitaxial layer thickness of $17 \mu \mathrm{~m}$ is required for a $36-\mathrm{V}$ circuit. For circuits with lower operating voltages, thinner and more heavily doped epitaxial layers are used to reduce the transistor collector series resistance, as will be shown later.

Following the epitaxial growth, an oxide layer is grown on the top surface of the epitaxial layer. A mask step and boron ( $p$-type) predeposition and diffusion are performed, resulting in the structure shown in Fig. 2.12. The function of this diffusion is to isolate the collectors of the transistors from each other with reverse-biased pn junctions, and it is termed the isolation
image_name:Figure 2.11 Bipolar integrated-circuit wafer following epitaxial growth.
description:The image shows a cross-sectional view of a semiconductor wafer after the epitaxial growth process, typical in the fabrication of bipolar integrated circuits. The structure consists of three main layers:

1. **n-type Epitaxial Layer:** This is the topmost layer, depicted in a light gray color. It is labeled as an 'n-type epitaxial layer,' indicating that it is a layer of silicon doped with donor impurities to create an excess of electrons, making it conductive.

2. **n+ Region:** Embedded within the n-type epitaxial layer is a darker gray region labeled 'n+.' This region represents a heavily doped n-type area, which is used to reduce the collector series resistance in the transistor. The increased doping level (indicated by the '+' sign) results in higher conductivity compared to the surrounding n-type material.

3. **p-type Substrate:** Below the n-type epitaxial layer and n+ region is the p-type substrate, shown with a dotted pattern. This substrate is doped with acceptor impurities, resulting in a material with an excess of holes. The p-type substrate forms the base upon which the epitaxial layer is grown.

The image does not show any explicit connections or wiring, as it focuses on the material structure at this stage of the wafer processing. There are no additional labels or annotations besides those indicating the types of semiconductor doping (n-type, n+, and p-type). The structure is designed to facilitate further processing steps, such as isolation and base diffusion, which will define the active regions of the transistors in the integrated circuit.

Figure 2.11 Bipolar integrated-circuit wafer following epitaxial growth.
image_name:Figure 2.12 Structure following isolation diffusion
description:The image titled "Figure 2.12 Structure following isolation diffusion" depicts a cross-sectional view of a semiconductor wafer at a specific stage of integrated circuit fabrication. The structure primarily consists of a p-type substrate, which forms the base of the wafer. Above the substrate, there is an n-type epitaxial layer, indicating the presence of a region with added electrons for conductivity.

In the illustration, isolation diffusion has been applied to form p-type regions that extend from the surface of the wafer into the n-type epitaxial layer. These p-type regions are created by introducing p-type impurities, which are likely boron, to form isolation barriers. These barriers electrically separate different sections of the n-type layer, which is crucial for defining individual components within an integrated circuit.

The diagram also shows an n+ region embedded within the n-type layer. This n+ region has a higher concentration of donor impurities, enhancing its conductivity compared to the surrounding n-type material. This region is essential for forming connections or active areas within the semiconductor device.

At the surface, a layer of silicon dioxide (SiO2) is depicted. This layer acts as an insulator and a protective barrier, preventing unwanted diffusion of impurities and providing a surface for further processing steps, such as photolithography.

The labels in the image include 'p-type impurities,' which indicate the regions where p-type doping has occurred, and 'SiO2,' marking the silicon dioxide layer. The structure is indicative of a stage in bipolar integrated circuit fabrication where isolation diffusion is used to define separate transistor regions before further processing steps.

Figure 2.12 Structure following isolation diffusion.
image_name:Figure 2.12 Structure following isolation diffusion
description:The image titled "Figure 2.12 Structure following isolation diffusion" depicts a cross-sectional view of a semiconductor structure at a stage in the fabrication of bipolar integrated circuits. The structure is primarily composed of a p-type substrate, which forms the base layer of the diagram. Above this substrate, there are several regions labeled with different types of doping and materials.

1. **Components and Structure:**
- **P-type Substrate:** The base of the structure is a p-type substrate, depicted with a dotted pattern to indicate its doping type.
- **N-type and N+ Regions:** There is a central n-type region, which is surrounded by a more heavily doped n+ region, indicating a collector or similar structure within the semiconductor.
- **P-type Impurities:** P-type impurities are shown at the surface, indicating areas where p-type doping has been introduced, likely forming the base regions of transistors.
- **Silicon Dioxide (SiO2) Layer:** A silicon dioxide layer is present on the surface, serving as an insulating layer to separate different regions and protect the underlying semiconductor material.
- **Isolation Regions:** The diagram shows isolation regions created by p-type doping, which are used to electrically isolate different components of the circuit.

2. **Connections and Interactions:**
- The n and n+ regions are embedded within the p-type substrate, indicating a typical structure for forming a transistor where the n+ region might serve as a collector, and the p-type regions act as isolation and base areas.
- The SiO2 layer provides electrical insulation and serves as a base for further processing steps, such as photolithography, to pattern additional layers or components.

3. **Labels, Annotations, and Key Features:**
- The labels "p-type impurities" and "SiO2" clearly indicate the areas of doping and material layers.
- The structure is indicative of a stage in the fabrication process where isolation diffusion defines separate transistor regions before further processing.

Overall, this image represents a crucial stage in semiconductor manufacturing, focusing on the isolation and preparation of regions for subsequent steps in the creation of integrated circuits.

Figure 2.13 Structure following base diffusion.
diffusion. Because of the depth to which the diffusion must penetrate, this diffusion requires several hours in a diffusion furnace at temperatures of about $1200^{\circ} \mathrm{C}$. The isolated diffused layer has a sheet resistance from $20 \Omega / \square$ to $40 \Omega / \square$.

The next steps are the base mask, base predeposition, and base diffusion, as shown in Fig. 2.13. The latter is usually a boron diffusion, and the resulting layer has a sheet resistance of from $100 \Omega / \square$ to $300 \Omega / \square$, and a depth of $1 \mu \mathrm{~m}$ to $3 \mu \mathrm{~m}$ at the end of the process. This diffusion forms not only the bases of the transistors, but also many of the resistors in the circuit, so that control of the sheet resistance is important.

Following the base diffusion, the emitters of the transistors are formed by a mask step, $n$-type predeposition, and diffusion, as shown in Fig. 2.14. The sheet resistance is between $2 \Omega / \square$ and $10 \Omega / \square$, and the depth is $0.5 \mu \mathrm{~m}$ to $2.5 \mu \mathrm{~m}$ after the diffusion. This diffusion step is also used to form a low-resistance region, which serves as the contact to the collector region. This is necessary because ohmic contact is difficult to accomplish between aluminum metallization and the high-resistivity epitaxial material directly. The next masking step, the contact mask, is used to open holes in the oxide over the emitter, the base, and the collector of the transistors so that electrical contact can be made to them. Contact windows are also opened
image_name:Figure 2.14 Structure following emitter diffusion
description:The image labeled "Figure 2.14 Structure following emitter diffusion" depicts a cross-sectional view of a semiconductor device, specifically focusing on a transistor structure after the emitter diffusion process.

1. **Identification of Components and Structure:**
- **SiO2 Layer:** At the top of the diagram, there is a thin layer labeled as SiO2, which represents silicon dioxide, commonly used as an insulating layer in semiconductor devices.
- **n-type Impurities:** These are shown as being diffused into a small region, forming the emitter of the transistor. This is a crucial step in establishing the emitter region of an npn transistor.
- **p-type Base:** Below the emitter, there is a layer labeled as the p-type base. This forms the base region of the transistor, which is essential for controlling the electron flow between the emitter and collector.
- **n+ Region:** Below the p-type base, there is an n+ region, indicating a heavily doped n-type area, typically serving as the collector contact to reduce resistance.
- **p-type Substrate:** The bottom-most layer is labeled as the p-type substrate, which forms the foundational layer of the semiconductor device.
- **p Regions:** There are additional p-type regions on either side of the main transistor structure, possibly indicating isolation regions or wells.

2. **Connections and Interactions:**
- The n-type impurities are diffused into the p-type base to form the emitter, allowing for electron injection into the base.
- The base region controls the flow of electrons from the emitter to the n+ collector region.
- The SiO2 layer serves as an insulating layer, preventing unwanted electrical contact and ensuring that connections are made only through designated contact points.

3. **Labels, Annotations, and Key Features:**
- The diagram is annotated with labels indicating the type of semiconductor material (n-type and p-type) and the specific regions (emitter, base, and collector).
- The use of SiO2 is marked, highlighting its role in the structure.
- The diffusion of n-type impurities is visually indicated, showing the process of forming the emitter region.
image_name:Figure 2.15 Final structure following contact mask and metallization
description:The image labeled "Figure 2.15 Final structure following contact mask and metallization" depicts a cross-sectional view of a semiconductor device, specifically an npn transistor structure, after the application of a contact mask and metallization. The diagram illustrates several key components and regions:

1. **Components and Structure:**
- **SiO2 Layer:** The topmost layer is silicon dioxide (SiO2), which acts as an insulating layer, with openings for contacts.
- **n-type Impurities:** There are regions with n-type impurities, indicating the emitter and collector areas of the transistor.
- **p-type Base:** The base of the transistor is shown as a p-type region, sandwiched between the n-type emitter and collector.
- **n+ Region:** A heavily doped n+ region is present, likely serving as the collector contact, providing low resistance.
- **p-type Substrate:** The entire structure is built on a p-type substrate, which forms the foundation of the device.

2. **Connections and Interactions:**
- The n-type emitter, p-type base, and n-type collector are configured in a typical npn transistor arrangement, allowing for the flow of current from the emitter to the collector when the base is properly biased.
- The SiO2 layer has openings that allow for metallization to make electrical contacts to the emitter, base, and collector regions.

3. **Labels, Annotations, and Key Features:**
- The diagram includes labels for the n-type impurities, p-type base, SiO2 layer, and p-type substrate, providing clarity on the material composition and doping characteristics of each region.
- The structure is indicative of a final stage in transistor fabrication, where contacts are made to the essential regions for device operation.

Overall, the image represents a detailed view of the final structural configuration of an npn transistor, highlighting the critical regions and materials involved in its construction and operation.
image_name:Figure 2.16 Scanning electron microscope photograph of npn transistor structure
description:The image labeled "Figure 2.16 Scanning electron microscope photograph of npn transistor structure" depicts a cross-sectional view of an npn transistor. The structure is shown with various layers and regions, each with specific doping characteristics and materials.

1. **Identification of Components and Structure:**
- The transistor is built on a **p-type substrate**, which forms the base of the structure.
- There is a **n+ collector region** embedded within the p-type substrate, indicating a heavily doped n-type region.
- Above the collector, a lightly doped **n-type layer** is present, which serves as the collector contact.
- The **p-type base** region is shown above the n-type collector, creating the second layer of the npn transistor.
- An **n-type emitter** is diffused into the p-type base, completing the npn configuration.
- The entire structure is covered by a layer of **SiO2 (silicon dioxide)**, which acts as an insulating layer.

2. **Connections and Interactions:**
- The n-type emitter, p-type base, and n-type collector form the three regions of the npn transistor, allowing for the flow of electrons from the emitter to the collector when forward biased.
- The SiO2 layer has openings, possibly for the placement of metal contacts to connect the emitter, base, and collector to external circuits.
- The diagram suggests the presence of electrical connections through these openings, although specific wiring or metallization is not visible in this cross-section.

3. **Labels, Annotations, and Key Features:**
- The diagram includes labels indicating the **n-type impurities** for the emitter and collector regions, and the **p-type base**.
- The **SiO2 layer** is labeled, highlighting its role as an insulator.
- The structure is annotated to show the different doping types and regions, which are essential for understanding the functionality of the npn transistor.

Overall, the image provides a detailed view of the internal structure of an npn transistor, illustrating the arrangement and interaction of its key components.

Figure 2.14 Structure following emitter diffusion.
image_name:Figure 2.14 Structure following emitter diffusion
description:The image titled "Figure 2.14 Structure following emitter diffusion" illustrates the cross-sectional view of an npn transistor after the emitter diffusion process. The diagram provides a detailed look at the internal structure and components of the transistor, including the following key elements:

1. **Components and Structure:**
- **Emitter:** Located at the top center, represented by a heavily doped n-type region (n+), indicating that it has undergone emitter diffusion to enhance electron injection into the base.
- **Base:** Situated directly below the emitter, this is a thin p-type region that controls the transistor's operation by modulating the flow of electrons between the emitter and collector.
- **Collector:** Positioned at the sides, forming a wider n-type region beneath the base, designed to collect electrons injected from the emitter.
- **P-type Substrate:** The foundation of the structure, providing the necessary support and isolation for the transistor's active regions.

2. **Connections and Interactions:**
- The emitter, base, and collector are interconnected through the semiconductor material, allowing for the flow of current. The emitter injects electrons into the base, which are then collected by the collector, facilitating the transistor's amplification properties.
- The SiO2 layer acts as an insulator, preventing unwanted current paths and protecting the integrity of the transistor's operation.

3. **Labels, Annotations, and Key Features:**
- **SiO2 Layer:** Clearly labeled, showing its role as an insulating layer above the base and collector regions.
- **Collector Contact, Emitter, and Base:** Each of these components is labeled, providing clarity on their location and function within the transistor.
- **Doping Types:** The diagram indicates the n-type and p-type regions, essential for understanding the operation and characteristics of the npn transistor.

Overall, the image provides a comprehensive view of the npn transistor structure following emitter diffusion, highlighting the arrangement and interaction of its key components and materials.

Figure 2.15 Final structure following contact mask and metallization.
image_name:Figure 2.15 Final structure following contact mask and metallization
description:The image displays a detailed view of an npn transistor structure following contact mask and metallization processes. It is a scanning electron microscope photograph that highlights the various components and their arrangements within the transistor.

1. **Identification of Components and Structure:**
- **Base Metallization:** This is the conductive layer that provides connectivity to the base region of the transistor.
- **Base Contact Window:** A designated area that allows electrical contact to the base region.
- **Emitter Metallization:** Conductive layer facilitating connection to the emitter region.
- **Emitter Contact Window:** An opening for making an electrical connection to the emitter.
- **Collector Metallization:** This layer ensures connectivity to the collector region.
- **Collector Contact Window:** A region that allows for electrical contact to the collector.
- **Edge of Base Diffusion, Emitter Diffusion, and Collector n+ Diffusion:** These are the boundaries of the diffused regions that form the base, emitter, and collector areas respectively.

2. **Connections and Interactions:**
- The metallization layers (base, emitter, and collector) are interconnected through the contact windows, which serve as points for electrical signals to enter and exit the transistor.
- The diffused regions indicate where the semiconductor material has been doped to form the necessary p-n junctions for transistor operation.

3. **Labels, Annotations, and Key Features:**
- The image includes annotations pointing to each of the key components and boundaries, providing clarity on their location and function within the transistor.
- The labels "Edge of base diffusion," "Edge of emitter diffusion," and "Edge of collector n+ diffusion" help in identifying the boundaries between different doped regions, essential for understanding the operation and characteristics of the npn transistor.

Overall, the image provides a comprehensive view of the npn transistor structure following emitter diffusion, highlighting the arrangement and interaction of its key components and materials.

Figure 2.16 Scanning electron microscope photograph of npn transistor structure.
for the passive components on the chip. The entire wafer is then coated with a thin (about $1 \mu \mathrm{~m}$ ) layer of aluminum that will interconnect the circuit elements. The actual interconnect pattern is defined by the last mask step, in which the aluminum is etched away in the areas where the photoresist is removed in the develop step. The final structure is shown in Fig. 2.15. A microscope photograph of an actual structure of the same type is shown in Fig. 2.16. The terraced effect on the surface of the device results from the fact that additional oxide is grown during each diffusion cycle, so that the oxide is thickest over the epitaxial region, where no oxide has been removed, is less thick over the base and isolation regions, which are both opened at the base mask step, and is thinnest over the emitter diffusion. A typical diffusion profile for a high-voltage, deep-diffused analog integrated circuit is shown in Fig. 2.17.

This sequence allows simultaneous fabrication of a large number (often thousands) of complex circuits on a single wafer. The wafer is then placed in an automatic tester, which checks the electrical characteristics of each circuit on the wafer and puts an ink dot on circuits that fail to meet specifications. The wafer is then broken up, by sawing or scribing and breaking, into individual circuits. The resulting silicon chips are called dice, and the singular is die. Each good die is then mounted in a package, ready for final testing.
image_name:cross section A-A'
description:The image shows a cross-sectional diagram of a monolithic npn transistor, labeled as "cross section A-A'." The illustration is divided into two main parts: the structural diagram of the transistor and a graph showing impurity concentration.

1. **Identification of Components and Structure:**
- The structural diagram depicts several layers and regions of an npn transistor. At the top, there are three terminals labeled C (Collector), B (Base), and E (Emitter).
- The transistor is composed of various semiconductor regions:
- **Emitter (n+):** A heavily doped n-type region, indicated by the n+ symbol.
- **Base (p):** A p-type region situated between the emitter and collector.
- **Collector (n):** An n-type region that extends beneath the base.
- **Buried Layer (n+):** A deeper n+ region below the collector, providing a low-resistance path.
- **Substrate (p):** A p-type substrate supporting the entire structure.

2. **Connections and Interactions:**
- The diagram shows the typical connections of an npn transistor with the collector, base, and emitter terminals.
- The flow of current typically goes from the collector to the emitter, controlled by the base.

3. **Labels, Annotations, and Key Features:**
- The graph below the structural diagram depicts impurity concentration (in cm⁻³) versus distance (in micrometers, µm) along the cross-section A-A'.
- The impurity concentration profile includes:
- **Emitter Diffusion (N_D):** A high concentration at the emitter region, rapidly decreasing as it moves into the base.
- **Base Diffusion (N_A):** A lower concentration than the emitter, indicating p-type doping.
- **Buried Layer (N_D):** A peak in concentration indicating the presence of the buried n+ layer.
- **Epitaxial Layer Background Concentration (N_D):** The baseline concentration for the n-type epitaxial layer.
- **Substrate Background Concentration (N_A):** The concentration level for the p-type substrate.
- The diagram provides insight into the doping profiles and structural layout of the npn transistor, which are crucial for its electrical characteristics and performance.
image_name:n p n transistor
description:The diagram shows a cross-section of a monolithic NPN transistor, illustrating impurity concentration across different layers. It highlights the emitter, base, and buried layer diffusions, along with the epitaxial and substrate background concentrations. The graph shows the variation of impurity concentration with depth (x in micrometers).
image_name:Figure 2.17
description:This graph is a plot of impurity concentration versus depth for a monolithic npn transistor in a high-voltage, deep-diffused process. It provides a detailed look at how different dopant concentrations vary across the depth of the transistor structure.

1. **Type of Graph and Function:**
- The graph is a concentration profile plot, showing impurity concentration as a function of depth in micrometers (µm).

2. **Axes Labels and Units:**
- The y-axis represents impurity concentration in units of cm⁻³, ranging from 10¹³ to 10²¹ on a logarithmic scale.
- The x-axis represents depth (x) in micrometers, ranging from 0 to approximately 22 µm.

3. **Overall Behavior and Trends:**
- The impurity concentration shows several distinct regions corresponding to different layers of the transistor.
- Starting from the left, the concentration drops sharply from 10²¹ cm⁻³ at the surface due to emitter diffusion (N_D).
- The base diffusion (N_A) shows a rapid decline to about 10¹⁶ cm⁻³.
- There is a rise in concentration in the buried layer (N_D), peaking at around 10¹⁹ cm⁻³ near 10 µm depth.
- After the buried layer, the concentration decreases gradually, stabilizing at the substrate background concentration (N_A) of about 10¹⁴ cm⁻³.

4. **Key Features and Technical Details:**
- The emitter diffusion shows the highest initial concentration, indicating a heavily doped region.
- The buried layer is distinct with a peak concentration indicating its role in reducing collector resistance.
- The substrate background concentration remains constant beyond 20 µm.

5. **Annotations and Specific Data Points:**
- The graph includes annotations such as 'Emitter diffusion (N_D)', 'Base diffusion (N_A)', 'Buried layer (N_D)', and 'Substrate background concentration (N_A)'.
- Critical transitions occur around 2.5 µm (emitter to base), 5 µm (base to epitaxial layer), and 9 µm (beginning of buried layer).

Figure 2.17 Typical impurity concentration for a monolithic $n p n$ transistor in a high-voltage, deep-diffused process.

## 2.4 Advanced Bipolar Integrated-Circuit Fabrication

A large fraction of bipolar analog integrated circuits currently manufactured uses the basic technology described in the previous section, or variations thereof. The fabrication sequence is relatively simple and low in cost. However, many of the circuit applications of commercial importance have demanded steadily increasing frequency response capability, which translates directly to a need for transistors of higher frequency-response capability in the technology. The higher speed requirement dictates a device structure with thinner base width to reduce base transit time and smaller dimensions overall to reduce parasitic capacitances. The smaller device dimensions require that the width of the junction depletion layers within the structure be reduced in proportion, which in turn requires the use of lower circuit operating voltages and higher impurity concentrations in the device structure. To meet this need, a class of bipolar fabrication technologies has evolved that, compared to the high-voltage process sequence described in the last section, use much thinner and more heavily doped epitaxial layers, selectively oxidized regions for isolation instead of diffused junctions, and a polysilicon layer as the source of dopant for the emitter. Because of the growing importance of this class of bipolar process, the sequence for such a process is described in this section.

The starting point for the process is similar to that for the conventional process, with a mask and implant step resulting in the formation of a heavily-doped $n^{+}$buried layer in a $p$-type
image_name:Figure 2.18 Device cross section
description:The image labeled "Figure 2.18 Device cross section" depicts a cross-sectional view of a semiconductor structure following initial processing steps. The diagram illustrates several key components and layers:

1. **p-type Substrate:** The base of the structure is a p-type substrate, which serves as the foundational layer for the device. This substrate is shown as a dotted region, indicating its material properties and doping type.

2. **n+ Buried Layer:** Above the p-type substrate, there is a heavily doped n+ buried layer. This layer is crucial for device operation, providing a low-resistance path and helping to isolate the active region from the substrate.

3. **n-type Epitaxial Layer:** On top of the n+ buried layer, a thin n-type epitaxial layer is grown. The diagram specifies this layer to be approximately 1 micrometer thick, with a resistivity of about 0.5 Ohm-cm. This layer is essential for forming the active regions of the device.

4. **SiO2 Layer:** The topmost layer in the cross-section is a silicon dioxide (SiO2) layer. This layer is used for isolation and protection of the underlying semiconductor materials.

**Connections and Interactions:**
The structure shown is part of a bipolar process where the n+ buried layer and the n-type epitaxial layer work together to create the necessary conditions for transistor operation. The SiO2 layer provides electrical isolation and helps in defining the active areas of the device.

**Labels and Annotations:**
- The thickness of the n-type epitaxial layer is annotated as 1 micrometer.
- The layers are labeled to indicate their material composition and doping type, such as n-type, n+, and p-type.
- The SiO2 layer is labeled to indicate its role in the structure.

This cross-section is representative of the initial stages in a bipolar transistor fabrication process, highlighting the formation of buried layers and epitaxial growth essential for device functionality.

Figure 2.18 Device cross section following initial buried-layer mask, implant, and epitaxial-layer growth.
substrate. Following this step, a thin $n$-type epitaxial layer is grown, about $1 \mu \mathrm{~m}$ in thickness and about $0.5 \Omega-\mathrm{cm}$ in resistivity. The result after these steps is shown in cross section in Fig. 2.18.

Next, a selective oxidation step is carried out to form the regions that will isolate the transistor from its neighbors and also isolate the collector-contact region from the rest of the transistor. The oxidation step is as described in Section 2.2.7, except that prior to the actual growth of the thick $\mathrm{SiO}_{2}$ layer, an etching step is performed to remove silicon material from the regions where oxide will be grown. If this is not done, the thick oxide growth results in elevated humps in the regions where the oxide is grown. The steps around these humps cause difficulty in coverage by subsequent layers of metal and polysilicon that will be deposited. The removal of some silicon material before oxide growth results in a nearly planar surface after the oxide is grown and removes the step coverage problem in subsequent processing. The resulting structure following this step is shown in Fig. 2.19. Note that the $\mathrm{SiO}_{2}$ regions extend all the way down to the $p$-type substrate, electrically isolating the $n$-type epi regions from one another. These regions are often referred to as moats. Because growth of oxide layers thicker than a micron or so requires impractically long times, this method of isolation is practical only for very thin transistor structures.

Next, two mask and implant steps are performed. A heavy $n^{+}$implant is made in the collector-contact region and diffused down to the buried layer, resulting in a low-resistance path to the collector. A second mask is performed to define the base region, and a thin-base $p$-type implant is performed. The resulting structure is shown in Fig. 2.20.

A major challenge in fabricating this type of device is the formation of very thin base and emitter structures, and then providing low-resistance ohmic contact to these regions. This is most often achieved using polysilicon as a doping source. An $n^{+}$doped layer of polysilicon is deposited and masked to leave polysilicon only in the region directly over the emitter. During subsequent high-temperature processing steps, the dopant (usually arsenic) diffuses out of the polysilicon and into the crystalline silicon, forming a very thin, heavily doped emitter region. Following the poly deposition, a heavy $p$-type implant is performed, which results in a more
image_name:Figure 2.19 Device cross section following selective etch and oxidation to form thick-oxide moats.
description:The image labeled "Figure 2.19 Device cross section following selective etch and oxidation to form thick-oxide moats" depicts a cross-sectional view of a semiconductor device structure.

1. **Identification of Components and Structure:**
- The diagram shows a layered structure with different doping regions. At the bottom, there is a **p-type substrate** represented by a dotted pattern indicating the base material. Above the substrate, there is an **n+ doped region** shown in a darker shade, signifying a heavily doped area.
- Above the n+ region is an **n- doped layer** depicted in a lighter shade, indicating a lightly doped area.
- The topmost layer consists of **SiO2 moats**, which are thick oxide regions formed by selective etching and oxidation.

2. **Connections and Interactions:**
- The diagram does not explicitly show electrical connections or interactions such as wiring or PCB traces. However, the presence of n+ and n- regions suggests potential pathways for electron flow within the device.
- The SiO2 moats serve as isolation structures, preventing electrical interaction between adjacent regions in the semiconductor device.

3. **Labels, Annotations, and Key Features:**
- The key labels include "p-type substrate," "n+," "n-," and "SiO2 moats," each indicating the type of material or structure present in the device.
- The diagram visually distinguishes between different doping levels and materials using shading and labeling, which is crucial for understanding the device's construction and function.

Overall, the image provides a detailed view of the semiconductor device's cross-section, highlighting the formation of thick-oxide moats and the arrangement of doped regions.

Figure 2.19 Device cross section following selective etch and oxidation to form thick-oxide moats.
image_name:Figure 2.19 Device cross section following selective etch and oxidation to form thick-oxide moats
description:The image labeled "Figure 2.19 Device cross section following selective etch and oxidation to form thick-oxide moats" illustrates a cross-sectional view of a semiconductor device. The diagram provides a detailed representation of the device's structure after undergoing selective etching and oxidation processes.

1. **Identification of Components and Structure:**
- **p-type Substrate:** The base of the structure is a p-type substrate, depicted with a dotted pattern to indicate its doping type.
- **n+ and n- Regions:** Above the substrate, there are two distinct n-type regions. The n+ region is heavily doped, shown with a darker shading, while the n- region is lightly doped, indicated with a lighter shading.
- **p- Base Layer:** On top of the n-type regions, there is a p- base layer, labeled clearly in the diagram. This layer is crucial for device operation.
- **Thick-Oxide Moats:** The diagram features thick-oxide moats, formed by selective etching and oxidation, which are shown as raised areas with a distinctive shape.

2. **Connections and Interactions:**
- The cross-section does not depict explicit electrical connections or wiring but focuses on the structural layout and doping profiles. The arrangement of doped regions suggests potential pathways for current flow and isolation provided by the oxide moats.

3. **Labels, Annotations, and Key Features:**
- The diagram includes clear labels for each region, such as "p- base layer," "n+," "n-," and "p-type substrate," which are essential for understanding the doping profile and the function of each layer.
- The shading and labeling effectively distinguish between different materials and doping levels, aiding in the comprehension of the device's construction and function.

Figure 2.20 Device cross section following mask, implant, and diffusion of collector $n^{+}$region, and mask and implant of base $p$-type region.
image_name:Figure 2.21
description:The image, labeled as "Figure 2.21," depicts a cross-sectional view of a semiconductor device following several fabrication steps, including poly deposition, mask application, base p-type implantation, and a thermal diffusion cycle.

Identification of Components and Structure:
- **p+ Base Layer:** This is a heavily doped p-type layer that is present throughout the base region, except directly under the polysilicon.
- **n+ Polysilicon Emitter:** A region where polysilicon is deposited, acting as an emitter. It is positioned above the base layer and influences the doping profile due to its masking properties.
- **n- Epi Layer:** A lightly doped n-type epitaxial layer that covers the n+ region and contributes to the device's electrical characteristics.
- **n+ Region:** A heavily doped n-type region that forms part of the collector structure, providing a low-resistance path for current flow.
- **p-type Substrate:** The foundational layer of the device, providing structural support and influencing the overall electrical behavior.

Connections and Interactions:
- The **p+ implant** arrows indicate the direction and regions where p-type doping is introduced, enhancing the base region's conductivity.
- The **polysilicon emitter** acts as a mask, preventing boron atoms from diffusing into certain areas during the implantation process.

Labels, Annotations, and Key Features:
- The diagram includes clear labels for each region, such as "p+ base layer," "n+ polysilicon emitter," "n- epi layer," and "p-type substrate," which are essential for understanding the doping profile and the function of each layer.
- The shading and labeling effectively distinguish between different materials and doping levels, aiding in the comprehension of the device's construction and function.

This cross-section highlights the complex layering and doping techniques used in semiconductor device fabrication, showcasing the precision required in modern electronic manufacturing.

Figure 2.21 Device cross section following poly deposition and mask, base p-type implant, and thermal diffusion cycle.
heavily doped $p$-type layer at all points in the base region except directly under the polysilicon, where the polysilicon itself acts as a mask to prevent the boron atoms from reaching this part of the base region. The structure that results following this step is shown in Fig. 2.21.

This method of forming low-resistance regions to contact the base is called a self-aligned structure because the alignment of the base region with the emitter happens automatically and does not depend on mask alignment. Similar processing is used in MOS technology, described later in this chapter.

The final device structure after metallization is shown in Fig. 2.22. Since the moats are made of $\mathrm{SiO}_{2}$, the metallization contact windows can overlap into them, a fact that dramatically reduces the minimum achievable dimensions of the base and collector regions. All exposed
image_name:Figure 2.22 Final device cross section
description:The image labeled 'Figure 2.22 Final device cross section' depicts a cross-sectional view of a bipolar transistor device structure. This illustration highlights the arrangement and interaction of various components within the transistor.

1. **Identification of Components and Structure:**
- **Base Contact Metal:** Positioned on the left side of the image, this metal layer makes contact with the base region of the transistor.
- **Polysilicon Emitter:** Located centrally, this is a rectangular block extending above the n+ region, representing the emitter of the transistor. It is made of polysilicon material.
- **Collector Contact Metal:** Found on the right side, this metal layer is in contact with the collector region.
- **n+ Regions:** These are heavily doped n-type regions beneath the base and collector contact metals, providing the necessary electrical characteristics for the transistor operation.
- **p-type Substrate:** The base material of the structure, extending across the entire bottom part of the cross-section.

2. **Connections and Interactions:**
- The base contact metal is connected to the base region, allowing current to flow into the base of the transistor.
- The polysilicon emitter is connected to the n+ region, facilitating the injection of charge carriers into the base.
- The collector contact metal is connected to the collector n+ region, allowing for the collection of charge carriers.
- The alignment of these regions ensures efficient current flow and transistor operation.

3. **Labels, Annotations, and Key Features:**
- The image includes labels for the 'Base contact metal,' 'Polysilicon emitter,' and 'Collector contact metal,' which help in identifying the components.
- The n+ and p-type regions are visually distinguished, indicating the doping types and their roles in the device.
- The overlap of contact windows into the moat regions is a key design feature that reduces the minimum dimensions of the base and collector regions, enhancing the device's performance.

Figure 2.22 Final device cross section. Note that collector and base contact windows can overlap moat regions. Emitter contact for the structure shown here would be made on an extension of the polysilicon emitter out of the device active area, allowing the minimum possible emitter size.
image_name:(a)
description:The image labeled as (a) is a scanning-electron-microscope photograph of a bipolar transistor in an advanced, polysilicon-emitter, oxide-isolated process. This photograph captures the device after the definition of the polysilicon emitter and the first-metal contacts to the base and collector.

1. **Identification of Components and Structure:**
- **Polysilicon Emitter:** The central component in the image, which is 1 µm wide, is prominently visible.
- **Base Contact (First Metal):** Located above the polysilicon emitter, this component establishes the initial connection to the base region.
- **Collector Contact (First Metal):** Positioned below the polysilicon emitter, this component connects to the collector region.
- **Thermal (Grown) Oxide:** The photograph shows a layer of thermal oxide, which plays a role in defining the base region.
- **Oxide Opening Defining Base Region:** This opening is visible around the base contact, indicating the area where the base is accessed.

2. **Connections and Interactions:**
- The polysilicon emitter is centrally located between the base and collector contacts, suggesting a vertical flow of current between these components.
- The oxide layer helps isolate the base region, ensuring that the electrical signals are confined to the desired pathways.

3. **Labels, Annotations, and Key Features:**
- The photograph is annotated with labels identifying the thermal oxide, base contact, collector contact, polysilicon emitter, and the oxide opening for the base region.
- These annotations aid in understanding the structural layout and functional components of the transistor, highlighting the critical areas involved in its operation.
image_name:(b)
description:Figure 2.23(b) is a scanning electron microscope photograph of a section of a bipolar transistor fabricated using an advanced polysilicon-emitter, oxide-isolated process. The image highlights several key components and features of the device:

1. **Deposited (CVD) Oxide:** The surface is covered with a deposited chemical vapor deposition (CVD) oxide layer, providing insulation and protection.

2. **Step Coverage:** The image shows step coverage into a contact through an opening in the deposited oxide, indicating how the metal layers interface with the underlying semiconductor layers.

3. **Second-Metal Interconnects:** There are visible second-metal interconnects leading to the base and emitter. These interconnects are crucial for establishing electrical connections between different parts of the transistor.

4. **Second-Metal Interconnect to Collector:** A separate path connects to the collector, showing the distinct routing for collector signals.

The photograph demonstrates the complexity and precision involved in the fabrication of bipolar transistors, emphasizing the layered structure and interconnectivity necessary for their function. The use of polysilicon for the emitter enhances performance by allowing for smaller emitter sizes and improved current handling capabilities.

Figure 2.23 Scanning-electron-microscope photographs of a bipolar transistor in an advanced, polysilicon-emitter, oxide-isolated process. (a) After polysilicon emitter definition and first-metal contact to the base and collector. The polysilicon emitter is $1 \mu \mathrm{~m}$ wide. (b) After oxide deposition, contact etch, and second-metal interconnect. [QUBic process photograph courtesy of Signetics.]
silicon and polysilicon is covered with a highly conductive silicide (a compound of silicon and a refractory metal such as tungsten) to reduce series and contact resistance. For minimumdimension transistors, the contact to the emitter is made by extending the polysilicon to a region outside the device active area and forming a metal contact to the polysilicon there. A photograph of such a device is shown in Fig. 2.23, and a typical impurity profile is shown in Fig. 2.24. The use of the remote emitter contact with polysilicon connection does add some series emitter resistance, so for larger device geometries or cases in which emitter resistance is critical, a larger emitter is used and the contact is placed directly on top of the polysilicon emitter itself. Production IC processes ${ }^{7,8}$ based on technologies similar to the one just described yield bipolar transistors having $f_{T}$ values well in excess of 10 GHz , compared to a typical value of 500 MHz for deep-diffused, high-voltage processes.

## 2.5 Active Devices in Bipolar Analog Integrated Circuits

The high-voltage IC fabrication process described previously is an outgrowth of the one used to make npn double-diffused discrete bipolar transistors, and as a result the process inherently produces double-diffused npn transistors of relatively high performance. The advanced technology process improves further on all aspects of device performance except for breakdown voltage. In addition to npn transistors, pnp transistors are also required in many analog circuits, and an important development in the evolution of analog IC technologies was the invention of device structures that allowed the standard technology to produce pnp transistors as well. In this section, we will explore the structure and properties of $n p n$, lateral pnp, and substrate pnp transistors. We will draw examples primarily from the high-voltage technology. The available structures in the more advanced technology are similar, except that their frequency response is correspondingly higher. We will include representative device parameters from these newer technologies as well.
image_name:Figure 2.24 Typical impurity profile in a shallow oxide-isolated bipolar transistor
description:The graph in Figure 2.24 is a plot of impurity concentration versus depth in a shallow oxide-isolated bipolar transistor. The x-axis represents the depth in micrometers (µm), ranging from 0 to approximately 2 µm. The y-axis represents the impurity concentration in cm⁻³, with a logarithmic scale ranging from 10¹⁵ to 10²⁰ cm⁻³.

The graph shows several distinct regions corresponding to different parts of the transistor structure:

1. **Emitter (As):** At the surface (0 µm), there is a sharp peak in impurity concentration reaching up to 10²⁰ cm⁻³, indicating a high concentration of arsenic (As) used in the emitter.

2. **Base (B):** Just beneath the emitter, there is a smaller peak around 10¹⁸ cm⁻³, representing the base region doped with boron (B).

3. **Epi Layer (As):** The concentration then decreases sharply and stabilizes around 10¹⁶ cm⁻³ as it transitions into the epitaxial layer, which is also doped with arsenic.

4. **Buried Layer (Sb):** At a depth of approximately 0.5 µm to 1.5 µm, there is a broad peak in the impurity concentration, reaching around 10¹⁹ cm⁻³. This indicates the presence of a buried layer doped with antimony (Sb).

5. **Substrate (B):** Beyond 1.5 µm, the concentration decreases again, representing the transition into the substrate, which is doped with boron.

The graph effectively illustrates the layered structure of the transistor, highlighting the varying levels of doping in different regions, which are critical for the device's electrical properties.

Figure 2.24 Typical impurity profile in a shallow oxide-isolated bipolar transistor.

### 2.5.1 Integrated-Circuit npn Transistors

The structure of a high-voltage, integrated-circuit npn transistor was described in the last section and is shown in plan view and cross section in Fig. 2.25. In the forward-active region of operation, the only electrically active portion of the structure that provides current gain is that portion of the base immediately under the emitter diffusion. The rest of the structure provides a top contact to the three transistor terminals and electrical isolation of the device from the rest of the devices on the same die. From an electrical standpoint, the principal effect of these regions is to contribute parasitic resistances and capacitances that must be included in the small-signal model for the complete device to provide an accurate representation of high-frequency behavior.

An important distinction between integrated-circuit design and discrete-component circuit design is that the IC designer has the capability to utilize a device geometry that is specifically optimized for the particular set of conditions found in the circuit. Thus the circuitdesign problem involves a certain amount of device design as well. For example, the need often exists for a transistor with a high current-carrying capability to be used in the output stage of an amplifier. Such a device can be made by using a larger device geometry than the standard one, and the transistor then effectively consists of many standard devices connected in parallel. The larger geometry, however, will display larger base-emitter, collectorbase, and collector-substrate capacitance than the standard device, and this must be taken into
image_name:The diagram illustrates an integrated-circuit npn transistor with labeled collector (C), base (B), and emitter (E) regions. It shows the layout and cross-sectional view, highlighting the buried layer, isolation, base, emitter, contact opening, and metal layers. The structure includes a p-type substrate with n+ and n- regions for the collector, base, and emitter.
image_name:
description:The image depicts an integrated-circuit npn transistor, illustrated through both a top view layout and a cross-sectional diagram.

Identification of Components and Structure:
1. **Top View Layout:**
- The top view shows a rectangular layout divided into three main sections labeled as C (Collector), B (Base), and E (Emitter).
- Each section is marked with different patterns to indicate various layers:
- **Buried Layer:** Indicated by a line with a triangle.
- **Isolation:** Shown as a dashed line.
- **Base:** Represented by a solid line.
- **Emitter:** Depicted with a double line.
- **Contact Opening:** Illustrated with a shaded pattern.
- **Metal:** Displayed as a line with alternating dashes and dots.

2. **Cross-Sectional Diagram:**
- Shows a vertical cut through the transistor structure.
- **Collector:** Located at the left side, consisting of n+ region beneath the contact opening.
- **Base:** Positioned in the middle, with a p-type region sandwiched between n+ regions.
- **Emitter:** On the right side, featuring an n+ region above the base.
- The entire structure is built on a p-type substrate, with n-type regions forming the active areas of the transistor.

Connections and Interactions:
- The cross-sectional view shows how the emitter, base, and collector are electrically isolated within the p-type substrate.
- The connections between these regions are facilitated by metal contacts, allowing for current flow and signal transmission.
- The buried layer provides a low-resistance path for the collector.

Labels, Annotations, and Key Features:
- The diagram includes a scale on the left indicating distances in micrometers, giving a sense of the dimensions of the transistor.
- Labels for the Collector (C), Base (B), and Emitter (E) are clearly marked, providing clarity on the function and position of each region.
- The diagram includes a key explaining the symbols and patterns used to represent different layers and features within the transistor structure.

This detailed representation allows for an understanding of the physical layout and operational principles of the npn transistor within an integrated circuit.

Figure 2.25 Integrated-circuit $n p n$ transistor. The mask layers are coded as shown.
account in analyzing the frequency response of the circuit. The circuit designer then must be able to determine the effect of changes in device geometry on device characteristics and to estimate the important device parameters when the device structure and doping levels are known. To illustrate this procedure, we will calculate the model parameters of the npn device shown in Fig. 2.25. This structure is typical of the devices used in circuits with a $5-\Omega-\mathrm{cm}$, $17-\mu \mathrm{m}$ epitaxial layer. The emitter diffusion is $20 \mu \mathrm{~m} \times 25 \mu \mathrm{~m}$, the base diffusion is 45 $\mu \mathrm{m} \times 60 \mu \mathrm{~m}$, and the base-isolation spacing is $25 \mu \mathrm{~m}$. The overall device dimensions are $140 \mu \mathrm{~m} \times 95 \mu \mathrm{~m}$. Device geometries intended for lower epi resistivity and thickness can be much smaller; the base-isolation spacing is dictated by the side diffusion of the isolation region plus the depletion layers associated with the base-collector and collector-isolation junctions.

Saturation Current $I_{S}$. In Chapter 1, the saturation current of a graded-base transistor was shown to be

$$
\begin{equation*}
I_{S}=\frac{q A \bar{D}_{n} n_{i}^{2}}{Q_{B}} \tag{2.16}
\end{equation*}
$$

where $A$ is the emitter-base junction area, $Q_{B}$ is the total number of impurity atoms per unit area in the base, $n_{i}$ is the intrinsic carrier concentration, and $\bar{D}_{n}$ is the effective diffusion constant for electrons in the base region of the transistor. From Fig. 2.17, the quantity $Q_{B}$ can be identified as the area under the concentration curve in the base region. This could be determined graphically but is most easily determined experimentally from measurements of the base-emitter voltage at a constant collector current. Substitution of (2.16) in (1.35) gives

$$
\begin{equation*}
\frac{Q_{B}}{\bar{D}_{n}}=A \frac{q n_{i}^{2}}{I_{C}} \exp \frac{V_{B E}}{V_{T}} \tag{2.17}
\end{equation*}
$$

and $Q_{B}$ can be determined from this equation.

#### EXAMPLE

A base-emitter voltage of 550 mV is measured at a collector current of $10 \mu \mathrm{~A}$ on a test transistor with a $100 \mu \mathrm{~m} \times 100 \mu \mathrm{~m}$ emitter area. Estimate $Q_{B}$ if $T=300^{\circ} \mathrm{K}$. From Chapter 1 , we have $n_{i}=1.5 \times 10^{10} \mathrm{~cm}^{-3}$. Substitution in (2.17) gives

$$
\begin{aligned}
\frac{Q_{B}}{\bar{D}_{n}} & =\left(100 \times 10^{-4}\right)^{2} \frac{1.6 \times 10^{-19} \times 2.25 \times 10^{20}}{10^{-5}} \exp (550 / 26) \\
& =5.54 \times 10^{11} \mathrm{~cm}^{-4} \mathrm{~s}
\end{aligned}
$$

At the doping levels encountered in the base, an approximate value of $\bar{D}_{n}$, the electron diffusivity, is

$$
\bar{D}_{n}=13 \mathrm{~cm}^{2} \mathrm{~s}^{-1}
$$

Thus for this example,

$$
Q_{B}=5.54 \times 10^{11} \times 13 \mathrm{~cm}^{-2}=7.2 \times 10^{12} \text { atoms } / \mathrm{cm}^{2}
$$

Note that $Q_{B}$ depends on the diffusion profiles and will be different for different types of processes. Generally speaking, fabrication processes intended for lower voltage operation use thinner base regions and display lower values of $Q_{B}$. Within one nominally fixed process, $Q_{B}$ can vary by a factor of two or three to one because of diffusion process variations. The principal significance of the numerical value for $Q_{B}$ is that it allows the calculation of the saturation current $I_{S}$ for any device structure once the emitter-base junction area is known.

Series Base Resistance $r_{b}$. Because the base contact is physically removed from the active base region, a significant series ohmic resistance is observed between the contact and the active base. This resistance can have a significant effect on the high-frequency gain and on the noise performance of the device. As illustrated in Fig. 2.26a, this resistance consists of two parts. The first is the resistance $r_{b 1}$ of the path between the base contact and the edge of the emitter
image_name:Figure 2.26 (a)
description:The image, labeled as "Figure 2.26 (a)", illustrates the base resistance components for an npn transistor. The diagram is a cross-sectional view showing the internal structure of the transistor's base region.

1. **Identification of Components and Structure:**
- The diagram shows two main regions labeled 'B' for the base contact and 'E' for the emitter contact.
- The base region is depicted as a semi-circular area beneath these contacts, with a dotted pattern representing the semiconductor material.
- The emitter region is shown as a solid, darker area embedded within the base region.
- Two resistive paths are marked within the base region: $r_{b1}$ and $r_{b2}$.

2. **Connections and Interactions:**
- The resistance $r_{b1}$ is shown as a zigzag line, representing the resistive path between the base contact 'B' and the edge of the emitter.
- The resistance $r_{b2}$ is depicted as a straight line with a circle at the end, indicating the resistive path from the edge of the emitter to a point within the base region.
- These resistances illustrate the path of current flow and are critical in determining the overall base resistance, which affects the transistor's performance.

3. **Labels, Annotations, and Key Features:**
- The labels $r_{b1}$ and $r_{b2}$ are clearly annotated next to their respective resistive paths.
- The diagram emphasizes the physical separation and resistance between the base contact and the active base region, which is crucial for understanding the effects on high-frequency gain and noise performance.

Overall, the diagram provides a clear representation of the series base resistance components in an npn transistor, highlighting the structural aspects that contribute to the base resistance.

(a)

Figure 2.26 (a) Base resistance components for the $n p n$ transistor.
image_name:Figure 2.26 (a)
description:The diagram labeled "Figure 2.26 (a)" illustrates the base resistance components for an npn transistor. It provides a detailed view of the structural aspects that contribute to the base resistance.

1. **Identification of Components and Structure:**
- **Base Contact:** This is shown on the left side of the diagram, indicating where the electrical connection to the base region is made.
- **Emitter Diffusion:** A rectangular area labeled as "Emitter diffusion" is depicted, representing the region where the emitter is diffused into the base.
- **Dimensions:** The diagram specifies various dimensions, such as 25 µm for the width of the structure, 10 µm for the length of the emitter diffusion, and 3 µm for the depth of the diffusion region.

2. **Connections and Interactions:**
- The diagram emphasizes the physical separation between the base contact and the emitter diffusion region. This separation is crucial for understanding the resistance path within the base region of the transistor.
- The structure suggests how current flows from the base contact through the base region, encountering resistance due to the geometry and material properties.

3. **Labels, Annotations, and Key Features:**
- The dimensions are clearly marked, providing essential information for calculating resistive components.
- The label "Base contact" indicates the starting point for electrical connection, while "Emitter diffusion" specifies the area affected by the diffusion process.

Overall, the diagram provides a clear representation of the series base resistance components in an npn transistor, highlighting the structural aspects that contribute to the base resistance. It is essential for understanding the effects on high-frequency gain and noise performance.

(b)

Figure 2.26 (b) Calculation of $r_{b 1}$. The $r_{b 1}$ component of base resistance can be estimated by calculating the resistance of the rectangular block above.
diffusion. The second part $r_{b 2}$ is that resistance between the edge of the emitter and the site within the base region at which the current is actually flowing. The former component can be estimated by neglecting fringing and by assuming that this component of the resistance is that of a rectangle of material as shown in Fig. 2.26b. For a base sheet resistance of $100 \Omega / \square$ and typical dimensions as shown in Fig. 2.26b, this would give a resistance of

$$
r_{b 1}=\frac{10 \mu \mathrm{~m}}{25 \mu \mathrm{~m}} 100 \Omega=40 \Omega
$$

The calculation of $r_{b 2}$ is complicated by several factors. First, the current flow in this region is not well modeled by a single resistor because the base resistance is distributed throughout the base region and two-dimensional effects are important. Second, at even moderate current levels, the effect of current crowding ${ }^{9}$ in the base causes most of the carrier injection from the emitter into the base to occur near the periphery of the emitter diffusion. At higher current levels, essentially all of the injection takes place at the periphery and the effective value of $r_{b}$ approaches $r_{b 1}$. In this situation, the portion of the base directly beneath the emitter is not involved in transistor action. A typically observed variation of $r_{b}$ with collector current for the npn geometry of Fig. 2.25 is shown in Fig. 2.27. In transistors designed for low-noise and/or high-frequency applications where low $r_{b}$ is important, an effort is often made to maximize the periphery of the emitter that is adjacent to the base contact. At the same time, the emitter-base
image_name:Figure 2.27
description:The graph in Figure 2.27 is a plot showing the variation of effective small-signal base resistance \( r_b \) with collector current for an integrated-circuit npn transistor. The graph is a two-dimensional line plot.

**Axes Labels and Units:**
- The x-axis represents the collector current, measured in milliamperes (mA), and is plotted on a logarithmic scale. The scale marks are at 0.001, 0.01, 0.1, 1, and 10 mA.
- The y-axis represents the base resistance \( r_b \), measured in ohms (\( \Omega \)), with linear scale marks at intervals of 100 ohms, ranging from 100 to 500 ohms.

**Overall Behavior and Trends:**
- The graph shows a decreasing trend in base resistance as the collector current increases.
- Initially, at low collector currents (around 0.001 mA), the base resistance is high, approximately 500 ohms.
- As the collector current increases, the base resistance decreases sharply, reaching around 200 ohms at higher collector currents (above 1 mA).
- The curve flattens out at higher currents, indicating that the base resistance becomes relatively constant beyond a certain point.

**Key Features and Technical Details:**
- The curve suggests a significant reduction in base resistance with increasing collector current, which is typical for transistors designed for high-frequency or low-noise applications.
- There are no peaks, valleys, or inflection points other than the general downward trend.

**Annotations and Specific Data Points:**
- The graph does not include specific annotations or reference lines, but the key trend is the sharp decrease in resistance from around 500 ohms to 200 ohms as the collector current increases from 0.001 mA to above 1 mA. This behavior highlights the importance of collector current in determining the effective base resistance in npn transistors.

Figure 2.27 Typical variation of effective small-signal base resistance with collector current for integrated-circuit npn transistor.
image_name:(a)
description:
[
name: r_c3, type: Resistor, value: r_c3, ports: {N1: C, N2: B}
name: r_c1, type: Resistor, value: r_c1, ports: {N1: E, N2: B}
name: r_c2, type: Resistor, value: r_c2, ports: {N1: B, N2: C}
]
extrainfo:The diagram represents the components of collector resistance in an integrated-circuit npn transistor. It shows resistors r_c3, r_c1, and r_c2 connected between the collector (C), base (B), and emitter (E).
Figure 2.28 (a) Components of collector resistance $r_{c}$.
junction and collector-base junction areas must be kept small to minimize capacitance. In the case of high-frequency transistors, this usually dictates the use of an emitter geometry that consists of many narrow stripes with base contacts between them. The ease with which the designer can use such device geometries is an example of the flexibility allowed by monolithic IC construction.

Series Collector Resistance $r_{c}$. The series collector resistance is important both in highfrequency circuits and in low-frequency applications where low collector-emitter saturation voltage is required. Because of the complex three-dimensional shape of the collector region itself, only an approximate value for the collector resistance can be obtained by hand analysis. From Fig. 2.28, we see that the resistance consists of three parts: that from the collector-base junction under the emitter down to the buried layer, $r_{c 1}$; that of the buried layer from the region under the emitter over to the region under the collector contact, $r_{c 2}$; and finally, that portion from the buried layer up to the collector contact, $r_{c 3}$. The small-signal series collector resistance in the forward-active region can be estimated by adding the resistance of these three paths.

#### EXAMPLE

Estimate the collector resistance of the transistor of Fig. 2.25, assuming the doping profile of Fig. 2.17. We first calculate the $r_{c 1}$ component. The thickness of the lightly doped epi layer between the collector-base junction and the buried layer is $6 \mu \mathrm{~m}$. Assuming that the collectorbase junction is at zero bias, the results of Chapter 1 can be used to show that the depletion layer is about $1 \mu \mathrm{~m}$ thick. Thus the undepleted epi material under the base is $5 \mu \mathrm{~m}$ thick.

The effective cross-sectional area of the resistance $r_{c 1}$ is larger at the buried layer than at the collector-base junction. The emitter dimensions are $20 \mu \mathrm{~m} \times 25 \mu \mathrm{~m}$, while the buried layer dimensions are $41 \mu \mathrm{~m} \times 85 \mu \mathrm{~m}$ on the mask. Since the buried layer side-diffuses a distance roughly equal to the distance that it out-diffuses, about $8 \mu \mathrm{~m}$ must be added on each edge, giving an effective size of $57 \mu \mathrm{~m} \times 101 \mu \mathrm{~m}$. An exact calculation of the ohmic resistance of this three-dimensional region would require a solution of Laplace's equation in the region, with a rather complex set of boundary conditions. Consequently, we will carry out an approximate analysis by modeling the region as a rectangular parallelepiped, as shown in Fig. 2.28b. Under the assumptions that the top and bottom surfaces of the region are equipotential surfaces, and that the current flow in the region takes place only in the vertical direction, the resistance of the structure can be shown to be

$$
\begin{equation*}
R=\frac{\rho T}{W L} \frac{\ln \left(\frac{a}{b}\right)}{(a-b)} \tag{2.18}
\end{equation*}
$$

image_name:Figure 2.28 (b) Model for calculation of collector resistance
description:The image depicts a three-dimensional geometric model used for calculating collector resistance, specifically a rectangular parallelepiped. The model is shown as a trapezoidal prism, with the top and bottom surfaces being rectangles of different sizes. The top rectangle is smaller, with dimensions labeled as width \( W \) and length \( L \). The bottom rectangle is larger and is shaded to distinguish it from the top.

The height of the model, or the distance between the top and bottom rectangles, is labeled as \( T \), representing the thickness of the region. The model assumes that the top and bottom surfaces are equipotential surfaces, meaning they have the same electric potential, and that the current flows vertically through the prism.

The diagram is annotated with arrows indicating the dimensions \( W \), \( L \), and \( T \). Additionally, the model is used to derive the resistance formula:

\[
R=\frac{\rho T}{W L} \frac{\ln \left(\frac{a}{b}\right)}{(a-b)}
\]

where \( \rho \) is the resistivity of the material, and \( a \) and \( b \) are the ratios of the dimensions of the bottom rectangle to the top rectangle. The model highlights how these geometric parameters affect the resistance calculation, with the assumption of vertical current flow simplifying the analysis.

(b)

Figure 2.28 (b) Model for calculation of collector resistance.
where
$T=$ thickness of the region
$\rho=$ resistivity of the material
$W, L=$ width, length of the top rectangle
$a=$ ratio of the width of the bottom rectangle to the width of the top rectangle
$b=$ ratio of the length of the bottom rectangle to the length of the top rectangle
Direct application of this expression to the case at hand would give an unrealistically low value of resistance, because the assumption of one-dimensional flow is seriously violated when the dimensions of the lower rectangle are much larger than those of the top rectangle. Equation 2.18 gives realistic results when the sides of the region form an angle of about $60^{\circ}$ or less with the vertical. When the angle of the sides is increased beyond this point, the resistance does not decrease very much because of the long path for current flow between the top electrode and the remote regions of the bottom electrode. Thus the limits of the bottom electrode should be determined either by the edges of the buried layer or by the edges of the emitter plus a distance equal to about twice the vertical thickness $T$ of the region, whichever is smaller. For the case of $r_{c 1}$,

$$
\begin{aligned}
T & =5 \mu \mathrm{~m}=5 \times 10^{-4} \mathrm{~cm} \\
\rho & =5 \Omega-\mathrm{cm}
\end{aligned}
$$

We assume that the effective emitter dimensions are those defined by the mask plus approximately $2 \mu \mathrm{~m}$ of side diffusion on each edge. Thus

$$
\begin{aligned}
& W=20 \mu \mathrm{~m}+4 \mu \mathrm{~m}=24 \times 10^{-4} \mathrm{~cm} \\
& L=25 \mu \mathrm{~m}+4 \mu \mathrm{~m}=29 \times 10^{-4} \mathrm{~cm}
\end{aligned}
$$

For this case, the buried-layer edges are further away from the emitter edge than twice the thickness $T$ on all four sides when side diffusion is taken into account. Thus the effective buried-layer dimensions that we use in (2.18) are

$$
\begin{aligned}
W_{B L} & =W+4 T=24 \mu \mathrm{~m}+20 \mu \mathrm{~m}=44 \mu \mathrm{~m} \\
L_{B L} & =L+4 T=29 \mu \mathrm{~m}+20 \mu \mathrm{~m}=49 \mu \mathrm{~m}
\end{aligned}
$$

and

$$
\begin{aligned}
a & =\frac{44 \mu \mathrm{~m}}{24 \mu \mathrm{~m}}=1.83 \\
b & =\frac{49 \mu \mathrm{~m}}{29 \mu \mathrm{~m}}=1.69
\end{aligned}
$$

Thus from (2.18),

$$
r_{c 1}=\frac{(5)\left(5 \times 10^{-4}\right)}{\left(24 \times 10^{-4}\right)\left(29 \times 10^{-4}\right)}(0.57) \Omega=204 \Omega
$$

We will now calculate $r_{c 2}$, assuming a buried-layer sheet resistance of $20 \Omega / \square$. The distance from the center of the emitter to the center of the collector-contact diffusion is $62 \mu \mathrm{~m}$, and the width of the buried layer is $41 \mu \mathrm{~m}$. The $r_{c 2}$ component is thus, approximately,

$$
r_{c 2}=(20 \Omega / \square)\left(\frac{L}{W}\right)=20 \Omega / \square\left(\frac{62 \mu \mathrm{~m}}{41 \mu \mathrm{~m}}\right)=30 \Omega
$$

Here the buried-layer side diffusion was not taken into account because the ohmic resistance of the buried layer is determined entirely by the number of impurity atoms actually diffused [see (2.15)] into the silicon, which is determined by the mask dimensions and the sheet resistance of the buried layer.

For the calculation of $r_{c 3}$, the dimensions of the collector-contact $n^{+}$diffusion are $18 \mu \mathrm{~m} \times 49 \mu \mathrm{~m}$, including side diffusion. The distance from the buried layer to the bottom of the $n^{+}$diffusion is seen in Fig. 2.17 to be $6.5 \mu \mathrm{~m}$, and thus $T=6.5 \mu \mathrm{~m}$ in this case. On the three sides of the collector $n^{+}$diffusion that do not face the base region, the out-diffused buried layer extends only $4 \mu \mathrm{~m}$ outside the $n^{+}$diffusion, and thus the effective dimension of the buried layer is determined by the actual buried-layer edge on these sides. On the side facing the base region, the effective edge of the buried layer is a distance $2 T$, or $13 \mu \mathrm{~m}$, away from the edge of the $n^{+}$diffusion. The effective buried-layer dimensions for the calculation of $r_{c 3}$ are thus $35 \mu \mathrm{~m} \times 57 \mu \mathrm{~m}$. Using (2.18),

$$
r_{c 3}=\frac{(5)\left(6.5 \times 10^{-4}\right)}{\left(18 \times 10^{-4}\right)\left(49 \times 10^{-4}\right)} 0.66=243 \Omega
$$

The total collector resistance is thus

$$
r_{c}=r_{c 1}+r_{c 2}+r_{c 3}=531 \Omega
$$

The value actually observed in such devices is somewhat lower than this for three reasons. First, we have approximated the flow as one-dimensional, and it is actually three-dimensional. Second, for larger collector-base voltages, the collector-base depletion layer extends further into the epi, decreasing $r_{c 1}$. Third, the value of $r_{c}$ that is important is often that for a saturated device. In saturation, holes are injected into the epi region under the emitter by the forwardbiased, collector-base function, and they modulate the conductivity of the region even at moderate current levels. ${ }^{10}$ Thus the collector resistance one measures when the device is in saturation is closer to $\left(r_{c 2}+r_{c 3}\right)$, or about 250 to $300 \Omega$. Thus $r_{c}$ is smaller in saturation than in the forward-active region.

Collector-Base Capacitance. The collector-base capacitance is simply the capacitance of the collector-base junction including both the flat bottom portion of the junction and the sidewalls. This junction is formed by the diffusion of boron into an $n$-type epitaxial material that we will assume has a resistivity of $5 \Omega$-cm, corresponding to an impurity concentration of $10^{15} \mathrm{atoms} / \mathrm{cm}^{3}$. The uniformly doped epi layer is much more lightly doped than the $\rho$-diffused region, and as a result, this junction is well approximated by a step junction in which the depletion layer lies almost entirely in the epitaxial material. Under this assumption, the results of Chapter 1 regarding step junctions can be applied, and for convenience this relationship has been plotted in nomograph form in Fig. 2.29. This nomograph is a graphical representation of the relation

$$
\begin{equation*}
\frac{C_{j}}{A}=\sqrt{\frac{q \epsilon N_{B}}{2\left(\psi_{0}+V_{R}\right)}} \tag{2.19}
\end{equation*}
$$

image_name:Figure 2.29
description:Figure 2.29 is a nomograph depicting the relationship between the capacitance per unit area of an abrupt \( p-n \) junction and the applied reverse voltage \( V_R \), as well as the depletion layer depth \( X_d \). The graph is designed to show how these parameters change with varying impurity concentrations on the lightly doped side of the junction.

### Type of Graph and Function:
This is a nomograph, a type of graphical calculator that represents multiple variables and their interdependencies. It is used to approximate the capacitance and depletion layer width of a \( p-n \) junction.

Axes Labels and Units:
- **X-axis:** Represents Voltage \( V \) in volts (V), ranging from 1 to 100 volts.
- **Left Y-axis:** Represents Capacitance per unit area in picofarads per square micrometer (pF/µm²), with a logarithmic scale ranging from \( 10^{-6} \) to \( 10^{-2} \).
- **Right Y-axis:** Represents Depletion layer depth \( X_d \) in micrometers (µm), also on a logarithmic scale, ranging from 0.01 to 100 µm.

Overall Behavior and Trends:
- The graph shows a series of diagonal lines representing different impurity concentrations, ranging from \( 10^{14} \) to \( 10^{19} \) atoms/cm³. As the voltage increases, the capacitance per unit area decreases.
- The depletion layer depth is inversely related to the capacitance and increases with higher reverse voltages.

Key Features and Technical Details:
- The lines for impurity concentrations are straight and downward sloping, indicating an inverse relationship between capacitance and voltage.
- A dashed line marks the boundary of the breakdown region, indicating a critical point where the junction may fail under high voltage.

Annotations and Specific Data Points:
- The graph includes annotations for impurity concentrations along the lines.
- The breakdown region is clearly indicated, providing a visual warning of the limits of safe operation.

This nomograph is a useful tool for engineers and scientists to quickly estimate the capacitance and depletion layer width for a given set of conditions in semiconductor devices.

Figure 2.29 Capacitance and depletion-layer width of an abrupt $p n$ junction as a function of applied voltage and doping concentration on the lightly doped side of the junction. ${ }^{11}$
where $N_{B}$ is the doping density in the epi material and $V_{R}$ is the reverse bias on the junction. The nomograph of Fig. 2.29 can also be used to determine the junction depletion-region width as a function of applied voltage, since this width is inversely proportional to the capacitance. The width in microns is given on the axis on the right side of the figure.

Note that the horizontal axis in Fig. 2.29 is the total junction potential, which is the applied potential plus the built-in voltage $\psi_{0}$. In order to use the curve, then, the built-in potential must be calculated. While this would be an involved calculation for a diffused junction, the built-in potential is actually only weakly dependent on the details of the diffusion profile and can be assumed to be about 0.55 V for the collector-base junction, 0.52 V for the collector-substrate junction, and about 0.7 V for the emitter-base junction.

#### EXAMPLE

Calculate the collector-base capacitance of the device of Fig. 2.25. The zero-bias capacitance per unit area of the collector-base junction can be found from Fig. 2.29 to be approximately $10^{-4} \mathrm{pF} / \mathrm{mm}^{2}$. The total area of the collector-base junction is the sum of the area of the bottom of the base diffusion plus the base sidewall area. From Fig. 2.25, the bottom area is

$$
A_{\text {bottom }}=60 \mu \mathrm{~m} \times 45 \mu \mathrm{~m}=2700 \mu^{2}
$$

The edges of the base region can be seen from Fig. 2.17 to have the shape similar to one-quarter of a cylinder. We will assume that the region is cylindrical in shape, which yields a sidewall area of

$$
A_{\text {sidewall }}=P \times d \times \frac{\pi}{2}
$$

where
$P=$ base region periphery
$d=$ base diffusion depth
Thus we have

$$
A_{\text {sidewall }}=3 \mu \mathrm{~m} \times(60 \mu \mathrm{~m}+60 \mu \mathrm{~m}+45 \mu \mathrm{~m}+45 \mu \mathrm{~m}) \times \frac{\pi}{2}=989 \mu \mathrm{~m}^{2}
$$

and the total capacitance is

$$
C_{\mu 0}=\left(A_{\text {bottom }}+A_{\text {sidewall }}\right)\left(10^{-4} \mathrm{pF} / \mu \mathrm{m}^{2}\right)=0.36 \mathrm{pF}
$$

Collector-Substrate Capacitance. The collector-substrate capacitance consists of three portions: that of the junction between the buried layer and the substrate, that of the sidewall of the isolation diffusion, and that between the epitaxial material and the substrate. Since the substrate has an impurity concentration of about $10^{16} \mathrm{~cm}^{-3}$, it is more heavily doped than the epi material, and we can analyze both the sidewall and epi-substrate capacitance under the assumption that the junction is a one-sided step junction with the epi material as the lightly doped side. Under this assumption, the capacitance per unit area in these regions is the same as in the collector-base junction.

#### EXAMPLE

Calculate the collector-substrate capacitance of the standard device of Fig. 2.25. The area of the collector-substrate sidewall is

$$
A_{\text {sidewall }}=(17 \mu \mathrm{~m})(140 \mu \mathrm{~m}+140 \mu \mathrm{~m}+95 \mu \mathrm{~m}+95 \mu \mathrm{~m})\left(\frac{\pi}{2}\right)=12,550 \mu \mathrm{~m}^{2}
$$

We will assume that the actual buried layer covers the area defined by the mask, indicated on Fig. 2.25 as an area of $41 \mu \mathrm{~m} \times 85 \mu \mathrm{~m}$, plus $8 \mu \mathrm{~m}$ of side-diffusion on each edge. This gives a total area of $57 \mu \mathrm{~m} \times 101 \mu \mathrm{~m}$. The area of the junction between the epi material and the substrate is the total area of the isolated region, minus that of the buried layer.

$$
\begin{aligned}
A_{\text {epi-substrate }} & =(140 \mu \mathrm{~m} \times 95 \mu \mathrm{~m})-(57 \mu \mathrm{~m} \times 101 \mu \mathrm{~m}) \\
& =7543 \mu \mathrm{~m}^{2}
\end{aligned}
$$

The capacitances of the sidewall and epi-substrate junctions are, using a capacitance per unit area of $10^{-4} \mathrm{pF} / \mu \mathrm{m}^{2}$

$$
\begin{aligned}
C_{c s 0}(\text { sidewall }) & =\left(12,550 \mu^{2}\right)\left(10^{-4} \mathrm{pF} / \mu \mathrm{m}^{2}\right)=1.26 \mathrm{pF} \\
C_{c s 0}(\text { epi-substrate }) & =\left(7543 \mu^{2}\right)\left(10^{-4} \mathrm{pF} / \mu \mathrm{m}^{2}\right)=0.754 \mathrm{pF}
\end{aligned}
$$

For the junction between the buried layer and the substrate, the lightly doped side of the junction is the substrate. Assuming a substrate doping level of $10^{16}$ atoms $/ \mathrm{cm}^{3}$, and a built-in voltage of 0.52 V , we can calculate the zero-bias capacitance per unit area as $3.3 \times$ $10^{-4} \mathrm{pF} / \mathrm{mm}^{2}$. The area of the buried layer is

$$
A_{B L}=57 \mu \mathrm{~m} \times 101 \mu \mathrm{~m}=5757 \mu \mathrm{~m}^{2}
$$

and the zero-bias capacitance from the buried layer to the substrate is thus

$$
C_{c s 0}(B L)=\left(5757 \mu \mathrm{~m}^{2}\right)\left(3.3 \times 10^{-4} \mathrm{pF} / \mu \mathrm{m}^{2}\right)=1.89 \mathrm{pF}
$$

The total zero-bias, collector-substrate capacitance is thus

$$
C_{c s 0}=1.26 \mathrm{pF}+0.754 \mathrm{pF}+1.89 \mathrm{pF}=3.90 \mathrm{pF}
$$

Emitter-Base Capacitance. The emitter-base junction of the transistor has a doping profile that is not well approximated by a step junction because the impurity concentration on both sides of the junction varies with distance in a rather complicated way. Furthermore, the sidewall capacitance per unit area is not constant but varies with distance from the surface because the base impurity concentration varies with distance. A precise evaluation of this capacitance can be carried out numerically, but a first-order estimate of the capacitance can be obtained by calculating the capacitance of an abrupt junction with an impurity concentration on the lightly doped side that is equal to the concentration in the base at the edge of the junction. The sidewall contribution is neglected.

#### EXAMPLE

Calculate the zero-bias, emitter-base junction capacitance of the standard device of Fig. 2.25.
We first estimate the impurity concentration at the emitter edge of the base region. From Fig. 2.17, it can be seen that this concentration is approximately $10^{17}$ atoms $/ \mathrm{cm}^{3}$. From the nomograph of Fig. 2.29, this abrupt junction would have a zero-bias capacitance per unit area of $10^{-3} \mathrm{pF} / \mu \mathrm{m}^{2}$. Since the area of the bottom portion of the emitter-base junction is $25 \mu \mathrm{~m} \times 20$ $\mu \mathrm{m}$, the capacitance of the bottom portion is

$$
C_{\text {bottom }}=\left(500 \mu^{2}\right)\left(10^{-3} \mathrm{pF} / \mu \mathrm{m}^{2}\right)=0.5 \mathrm{pF}
$$

Again assuming a cylindrical cross section, the sidewall area is given by

$$
A_{\text {sidewall }}=2(25 \mu \mathrm{~m}+20 \mu \mathrm{~m})\left(\frac{\pi}{2}\right)(2.5 \mu \mathrm{~m})=353 \mu \mathrm{~m}^{2}
$$

Assuming that the capacitance per unit area of the sidewall is approximately the same as the bottom,

$$
C_{\text {sidewall }}=\left(353 \mu \mathrm{~m}^{2}\right)\left(10^{-3} \mathrm{pF} / \mu \mathrm{m}^{2}\right)=0.35 \mathrm{pF}
$$

The total emitter-base capacitance is

$$
C_{j e 0}=0.85 \mathrm{pF}
$$

Current Gain. As described in Chapter 1, the current gain of the transistor depends on minority-carrier lifetime in the base, which affects the base transport factor, and on the diffusion length in the emitter, which affects the emitter efficiency. In analog IC processing, the base minority-carrier lifetime is sufficiently long that the base transport factor is not a limiting factor in the forward current gain in $n p n$ transistors. Because the emitter region is heavily doped with phosphorus, the minority-carrier lifetime is degraded in this region, and current gain is limited primarily by emitter efficiency. ${ }^{12}$ Because the doping level, and hence lifetime, vary with distance in the emitter, the calculation of emitter efficiency for the npn transistor is difficult, and measured parameters must be used. The room-temperature current gain typically lies between 200 and 1000 for these devices. The current gain falls with decreasing temperature, usually to a value of from 0.5 to 0.75 times the room temperature value at $-55^{\circ} \mathrm{C}$.

Summary of High-Voltage npn Device Parameters. A typical set of device parameters for the device of Fig. 2.25 is shown in Fig. 2.30. This transistor geometry is typical of that used for circuits that must operate at power supply voltages up to 40 V . For lower operating voltages,

|  | Parameter | Typical Value, 5- $\Omega$-cm, $17-\mu \mathrm{m}$ epi 44-V Device | Typical Value, $1-\Omega-\mathrm{cm}, 10-\mu \mathrm{m}$ ері 20-V Device |
| :---: | :---: | :---: | :---: |
|  | $\beta_{F}$ | 200 | 200 |
|  | $B_{R}$ | 2 | 2 |
|  | $V_{A}$ | 130 V | 90 V |
|  | $\eta$ | $2 \times 10^{-4}$ | $2.8 \times 10^{-4}$ |
|  | $I_{S}$ | $5 \times 10^{-15} \mathrm{~A}$ | $1.5 \times 10^{-15} \mathrm{~A}$ |
|  | $I_{C O}$ | $10^{-10} \mathrm{~A}$ | $10^{-10} \mathrm{~A}$ |
|  | $B V_{\text {CEO }}$ | 50 V | 25 V |
|  | $B V_{\text {CBO }}$ | 90 V | 50 V |
|  | $B V_{\text {EBO }}$ | 7 V | 7 V |
|  | $\tau_{F}$ | 0.35 ns | 0.25 ns |
|  | $\tau_{R}$ | 400 ns | 200 ns |
|  | $\beta_{0}$ | 200 | 150 |
|  | $r_{b}$ | $200 \Omega$ | $200 \Omega$ |
|  | $r_{c}$ (saturation) | $200 \Omega$ | $75 \Omega$ |
|  | $r_{e x}$ | $2 \Omega$ | $2 \Omega$ |
| Base-emitter junction | $\left\{\begin{array}{l}C_{j e 0} \\ \psi_{0 e} \\ n_{e}\end{array}\right.$ | $\begin{aligned} & 1 \mathrm{pF} \\ & 0.7 \mathrm{~V} \\ & 0.33 \end{aligned}$ | $\begin{aligned} & 1.3 \mathrm{pF} \\ & 0.7 \mathrm{~V} \\ & 0.33 \end{aligned}$ |
| Base-collector junction | $\left\{\begin{array}{l}C_{\mu 0} \\ \psi_{0 c} \\ n_{c}\end{array}\right.$ | $\begin{aligned} & 0.3 \mathrm{pF} \\ & 0.55 \mathrm{~V} \\ & 0.5 \end{aligned}$ | $\begin{aligned} & 0.6 \mathrm{pF} \\ & 0.6 \mathrm{~V} \\ & 0.5 \end{aligned}$ |
| Collector-substrate junction | $\left\{\begin{array}{l}C_{c s 0} \\ \psi_{0 s} \\ n_{s}\end{array}\right.$ | $\begin{aligned} & 3 \mathrm{pF} \\ & 0.52 \mathrm{~V} \\ & 0.5 \end{aligned}$ | $\begin{aligned} & 3 \mathrm{pF} \\ & 0.58 \mathrm{~V} \\ & 0.5 \end{aligned}$ |

Figure 2.30 Typical parameters for high-voltage integrated npn transistors with $500 \mu^{2}$ emitter area. The thick epi device is typical of those used in circuits operating at up to 44 V power-supply voltage, while the thinner device can operate up to about 20 V . While the geometry of the thin epi device is smaller, the collector-base capacitance is larger because of the heavier epi doping. The emitter-base capacitance is higher because the base is shallower, and the doping level in the base at the emitter-base junction is higher.
thinner epitaxial layers can be used, and smaller device geometries can be used as a result. Also shown in Fig. 2.30 are typical parameters for a device made with 1- $\Omega-\mathrm{cm}$ epi material, which is $10 \mu \mathrm{~m}$ thick. Such a device is physically smaller and has a collector-emitter breakdown voltage of about 25 V .

Advanced-Technology Oxide-Isolated npn Bipolar Transistors. The structure of an advanced oxide-isolated, poly-emitter npn bipolar transistor is shown in plan view and cross section in Fig. 2.31. Typical parameters for such a device are listed in Fig. 2.32. Note the enormous reduction in device size, transit time, and parasitic capacitance compared to the high-voltage, deep-diffused process. These very small devices achieve optimum performance characteristics at relatively low bias currents. The value of $\beta$ for such a device typically peaks at a collector current of about $50 \mu \mathrm{~A}$. For these advanced-technology transistors, the use of ion implantation allows precise control of very shallow emitter $(0.1 \mu \mathrm{~m})$ and base $(0.2 \mu \mathrm{~m})$
image_name:Plan view
description:The image titled "Plan view" illustrates a typical advanced-technology bipolar transistor, focusing on both plan view and cross-sectional details.

1. **Identification of Components and Structure:**
- The diagram consists of two main parts: the plan view (top) and the cross-section (bottom).
- **Plan View:**
- Two rectangular regions represent the layout of the transistor components.
- The rectangles are labeled with dimensions in micrometers, indicating a scale for the layout.
- **Buried Layer:** Indicated by a dashed line, suggesting a layer beneath the surface.
- **Thick Oxide Edge:** Represented by a solid line, surrounding the essential components.
- **n+ Collector:** A region marked with a specific pattern, indicating highly doped n-type material.
- **p+ Base:** Another region with a distinct pattern, indicating highly doped p-type material.
- **Polysilicon:** Identified by diagonal hatching, likely used for gates or interconnects.
- **Contact Regions:** Marked with a cross-hatch pattern, showing where electrical connections are made.
- **Metal:** Represented by solid lines, indicating conductive paths.

2. **Cross-Section:**
- Illustrates the vertical structure of the transistor, showing layers from the surface down to the substrate.
- **Base, Emitter, and Collector:** Labeled clearly, showing their respective positions and materials.
- **SiO2 Layers:** Represented as insulating layers surrounding the active regions.
- **p-type Substrate:** The foundational layer upon which the transistor is built, supporting the n+ and p+ regions.

2. **Connections and Interactions:**
- The plan view shows how the different regions are interconnected, with metal lines indicating paths for electrical signals.
- The cross-section demonstrates the vertical interaction between the emitter, base, and collector, crucial for transistor operation.

3. **Labels, Annotations, and Key Features:**
- The diagram includes a legend explaining the symbols and patterns used to denote different materials and regions.
- Annotations such as 'Distance, µm' provide a scale reference for the plan view.
- Labels like 'Base,' 'Emitter,' and 'Collector' clarify the roles of various regions in the transistor's function.

Overall, the image provides a detailed look at the physical layout and structure of an advanced bipolar transistor, emphasizing the miniaturization and precise fabrication techniques used in modern semiconductor devices.
image_name:cross section
description:The image provides a detailed plan view and cross-section of an advanced-technology bipolar transistor, illustrating its compact design and efficient structure.

**1. Identification of Components and Structure:**
- **Plan View (Top Half):**
- The plan view shows a rectangular layout with clearly marked regions. The components include:
- **Buried Layer:** Indicated by a dashed line with triangles, providing a low-resistance path for collector current.
- **Thick Oxide Edge:** Marked by a solid line, likely serving as isolation.
- **n+ Collector, p+ Base, and Polysilicon:** These are the primary regions of the transistor, with the n+ collector and p+ base regions clearly defined.
- **Contact Regions:** Represented by cross-hatched boxes, indicating where electrical connections are made.
- **Metal:** Shown as solid lines, indicating the metal connections for the device.

- **Cross Section (Bottom Half):**
- The cross-section shows a layered structure:
- **SiO2 Layers:** Used for insulation, covering the base and collector regions.
- **Emitter, Base, and Collector Regions:**
- **Emitter:** Positioned above the base, typically made of polysilicon.
- **Base:** A thin p+ layer underneath the emitter.
- **Collector:** Composed of an n+ layer extending under the base.
- **p-type Substrate:** The foundational layer upon which the other regions are built.

**2. Connections and Interactions:**
- The buried layer and metal connections facilitate current flow and signal transmission between different parts of the transistor. The design minimizes parasitic capacitance and transit time, enhancing performance.

**3. Labels, Annotations, and Key Features:**
- The diagram includes annotations for measurement scales (in micrometers), indicating the compactness of the design.
- Key features such as the buried layer, oxide edges, and contact regions are labeled for clarity.
- The cross-section provides a clear view of the vertical structure and material composition, critical for understanding the device's operation.

Figure 2.31 Plan view and cross section of a typical advanced-technology bipolar transistor. Note the much smaller dimensions compared with the high-voltage device.
regions. The resulting base width is of the order of $0.1 \mu \mathrm{~m}$, and (1.99) predicts a base transit time about 25 times smaller than the deep-diffused device of Fig. 2.17. This is observed in practice, and the ion-implanted transistor has a peak $f_{T}$ of about 13 GHz .

### 2.5.2 Integrated-Circuit pnp Transistors

As mentioned previously, the integrated-circuit bipolar fabrication process is an outgrowth of that used to build double-diffused epitaxial npn transistors, and the technology inherently produces $n p n$ transistors of high performance. However, pnp transistors of comparable performance are not easily produced in the same process, and the earliest analog integrated circuits used no pnp transistors. The lack of a complementary device for use in biasing, level shifting, and as load devices in amplifier stages proved to be a severe limitation on the performance attainable in analog circuits, leading to the development of several pnp transistor structures

| Parameter | Vertical $n p n$ <br> Transistor with $2 \mu \mathrm{~m}^{2}$ <br> Emitter Area | Lateral pnp <br> Transistor with $2 \mu \mathrm{~m}^{2}$ <br> Emitter Area |
| :---: | :---: | :---: |
| $\beta_{F}$ | 120 | 50 |
| $\beta_{R}$ | 2 | 3 |
| $V_{A}$ | 35 V | 30 V |
| $I_{S}$ | $6 \times 10^{-18} \mathrm{~A}$ | $6 \times 10^{-18} \mathrm{~A}$ |
| $I_{C O}$ | 1 pA | 1 pA |
| $B V_{\text {CEO }}$ | 8 V | 14 V |
| $B V_{C B O}$ | 18 V | 18 V |
| $B V_{\text {EBO }}$ | 6 V | 18 V |
| $\tau_{F}$ | 10 ps | 650 ps |
| $\tau_{R}$ | 5 ns | 5 ns |
| $r_{b}$ | $400 \Omega$ | $200 \Omega$ |
| $r_{c}$ | $100 \Omega$ | $20 \Omega$ |
| $r_{e x}$ | $40 \Omega$ | $10 \Omega$ |
| $C_{\text {je0 }}$ | 5 fF | 14 fF |
| $\psi_{0 e}$ | 0.8 V | 0.7 V |
| $n_{e}$ | 0.4 | 0.5 |
| $C{ }^{0}$ | 5 fF | 15 fF |
| $\psi_{0 c}$ | 0.6 V | 0.6 V |
| $n_{c}$ | 0.33 | 0.33 |
| $C_{c s 0}\left(C_{b s 0}\right)$ | 20 fF | 40 fF |
| $\psi_{0 s}$ | 0.6 V | 0.6 V |
| $n_{s}$ | 0.33 | 0.4 |

Figure 2.32 Typical device parameters for bipolar transistors in a low-voltage, oxide-isolated, ion-implanted process.
that are compatible with the standard IC fabrication process. Because these devices utilize the lightly doped $n$-type epitaxial material as the base of the transistor, they are generally inferior to the $n p n$ devices in frequency response and high-current behavior, but are useful nonetheless. In this section, we will describe the lateral pnp and substrate $p n p$ structures.

Lateral pnp Transistors. A typical lateral pnp transistor structure fabricated in a high-voltage process is illustrated in Fig. 2.33a. ${ }^{13}$ The emitter and collector are formed with the same diffusion that forms the base of the npn transistors. The collector is a p-type ring around the emitter, and the base contact is made in the $n$-type epi material outside the collector ring. The flow of minority carriers across the base is illustrated in Fig. 2.33b. Holes are injected from the emitter, flow parallel to the surface across the $n$-type base region, and ideally are collected by the p-type collector before reaching the base contact. Thus the transistor action is lateral rather than vertical as in the case for $n p n$ transistors. The principal drawback of the structure is the fact that the base region is more lightly doped than the collector. As a result, the collectorbase depletion layer extends almost entirely into the base. The base region must then be made wide enough so that the depletion layer does not reach the emitter when the maximum collectoremitter voltage is applied. In a typical analog IC process, the width of this depletion layer is $6 \mu \mathrm{~m}$ to $8 \mu \mathrm{~m}$ when the collector-emitter voltage is in the $40-\mathrm{V}$ range. Thus the minimum base width for such a device is about $8 \mu \mathrm{~m}$, and the minimum base transit time can be estimated from (1.99) as

$$
\begin{equation*}
\tau_{F}=\frac{W_{B}^{2}}{2 D_{p}} \tag{2.20}
\end{equation*}
$$

image_name:Figure 2.33 (a)
description:The image labeled "Figure 2.33 (a)" depicts a lateral pnp transistor structure fabricated in a high-voltage process. The diagram is divided into two main sections: a top view and a cross-sectional view.

Top View:
- **Components:**
- The top view shows a layout with three primary regions labeled as Base (B), Collector (C), and Emitter (E).
- These regions are marked with dashed lines and are arranged in a concentric pattern, indicating the spatial relationship and layout of the transistor elements.
- **Labels and Annotations:**
- The layout includes distance markers along the y-axis, ranging from 0 to 120 micrometers, providing a scale for the dimensions of the components.
- The schematic symbol for a pnp transistor is displayed at the top, showing the conventional current flow from Emitter (E) to Collector (C) through the Base (B).

Cross-Sectional View:
- **Structure and Materials:**
- The cross-sectional view illustrates the vertical structure of the transistor.
- The substrate is identified as a p-type material, with n+ and n- regions indicating doping levels.
- The Base, Collector, and Emitter regions are shown as diffusions within the substrate, with the Base being n+, the Collector and Emitter being p+.
- **Connections and Interactions:**
- Current flows laterally from the Emitter to the Collector through the Base, which is typical for a lateral pnp transistor.
- The diagram shows the interaction between these regions, with the Base region controlling the flow of minority carriers (holes) between the Emitter and Collector.

Key Features:
- **Depletion Regions:**
- The cross-section highlights the depletion regions formed between different doped areas, essential for the transistor's operation at high voltages.
- **Substrate Interaction:**
- The n+ buried layer is shown beneath the main transistor structure, reducing substrate resistance and enhancing device performance.

This detailed layout and cross-section provide a comprehensive understanding of the lateral pnp transistor, highlighting its structural and functional aspects in a high-voltage process.

Figure 2.33 (a) Lateral pnp structure fabricated in a high-voltage process.
image_name:Figure 2.33 (b) Minority-carrier flow in the lateral pnp transistor
description:The diagram labeled "Figure 2.33 (b) Minority-carrier flow in the lateral pnp transistor" illustrates the structure and carrier flow within a lateral pnp transistor fabricated in a high-voltage process.

1. **Identification of Components and Structure:**
- The diagram shows a cross-sectional view of the lateral pnp transistor.
- The main components include the base (B), collector (C), and emitter (E) regions, each marked with their respective symbols.
- The base region is shown as a p-type material, while the collector and emitter are also p-type, indicating the transistor's pnp configuration.
- An n-type substrate is visible beneath these regions, with an n+ buried layer at the bottom.

2. **Connections and Interactions:**
- The diagram highlights the flow of minority carriers, specifically holes, which are injected from the emitter region (E) into the base.
- The arrows depict the movement of these holes through the base and towards the collector regions (C), indicating the direction of minority-carrier flow.
- This flow is essential for the functioning of the transistor, allowing current to pass from the emitter to the collector through the base.

3. **Labels, Annotations, and Key Features:**
- The diagram includes labels such as B, C, and E to denote the base, collector, and emitter, respectively.
- The term "Injected holes" is annotated to indicate the type of minority carriers and their movement within the device.
- The n+ buried layer is shown beneath the main structure, which helps reduce substrate resistance and enhance device performance.

(b)

Figure 2.33 (b) Minority-carrier flow in the lateral pnp transistor.

Use of $W_{B}=8 \mu \mathrm{~m}$ and $D_{p}=10 \mathrm{~cm}^{2} / \mathrm{s}$ (for holes) in (2.20) gives

$$
\tau_{F}=32 \mathrm{~ns}
$$

This corresponds to a peak $f_{T}$ of 5 MHz , which is a factor of 100 lower than a typical $n p n$ transistor in the same process.

The current gain of lateral pnp transistors tends to be low for several reasons. First, minority carriers (holes) in the base are injected downward from the emitter as well as laterally, and some of them are collected by the substrate, which acts as the collector of a parasitic vertical pnp transistor. The buried layer sets up a retarding field that tends to inhibit this process, but it still produces a measurable degradation of $\beta_{F}$. Second, the emitter of the $p n p$ is not as heavily doped as is the case for the npn devices, and thus the emitter injection efficiency given by (1.51b) is not optimized for the pnp devices. Finally, the wide base of the lateral pnp results in both a low emitter injection efficiency and also a low base transport factor as given by (1.51a).

Another drawback resulting from the use of a lightly doped base region is that the current gain of the device falls very rapidly with increasing collector current due to high-level injection. The minority-carrier distribution in the base of a lateral pnp transistor in the forward-active region is shown in Fig. 2.34. The collector current per unit of cross-sectional area can be obtained from (1.32) as

$$
\begin{equation*}
J_{p}=q D_{p} \frac{p_{n}(0)}{W_{B}} \tag{2.21}
\end{equation*}
$$

Inverting this relationship, we can calculate the minority-carrier density at the emitter edge of the base as

$$
\begin{equation*}
p_{n}(0)=\frac{J_{p} W_{B}}{q D_{p}} \tag{2.22}
\end{equation*}
$$

As long as this concentration is much less than the majority-carrier density in the base, low-level injection conditions exist and the base minority-carrier lifetime remains constant. However, when the minority-carrier density becomes comparable with the majority-carrier density, the majority-carrier density must increase to maintain charge neutrality in the base. This causes a decrease in $\beta_{F}$ for two reasons. First, there is a decrease in the effective lifetime of minority carriers in the base since there is an increased number of majority carriers with which recombination can occur. Thus the base transport factor given by (1.51a) decreases. Second, the increase in the majority-carrier density represents an effective increase in base doping density. This causes a decrease in emitter injection efficiency given by (1.51b). Both these mechanisms are also present in $n p n$ transistors, but occur at much higher current levels due to the higher doping density in the base of the npn transistor.
image_name:Figure 2.34 Minority-carrier distribution
description:The graph depicted is a schematic representation of the minority-carrier distribution in the base of a lateral pnp transistor in the forward-active region. This is a spatial distribution graph, where the x-axis represents the position across the base, specifically from the emitter-base depletion layer to the collection-base depletion layer. The y-axis denotes the minority-carrier concentration.

1. **Type of Graph and Function:**
- This is a spatial distribution graph illustrating the concentration of minority carriers across the base of a pnp transistor.

2. **Axes Labels and Units:**
- The x-axis is labeled with positions across the base, indicating the regions from the emitter-base depletion layer to the collection-base depletion layer.
- The y-axis is labeled as "Minority-carrier concentration," though specific units are not provided, it typically represents a normalized or relative concentration.

3. **Overall Behavior and Trends:**
- The graph shows a linear decrease in minority-carrier concentration from the emitter side towards the collector side. This linear trend indicates a diffusion process where minority carriers are injected at the emitter side and recombine or exit at the collector side.

4. **Key Features and Technical Details:**
- **pn(0):** Represents the initial minority-carrier concentration at the emitter-base junction, which is the highest point on the graph.
- **pn(x):** Represents the concentration of minority carriers at any given point x within the base.
- The concentration decreases linearly across the base width \(W_B\), indicating a uniform recombination rate or drift across the base.
- The graph highlights the emitter-base and collection-base depletion layers, showing the boundaries of the region where minority carriers are present.

5. **Annotations and Specific Data Points:**
- The graph is annotated with the labels "Emitter," "Base," and "Collector," marking the different regions of the transistor.
- The depletion layers are marked with hatched lines, indicating the regions where minority carriers are not present or are significantly reduced.

This graph effectively illustrates how the minority-carrier concentration varies linearly across the base of a pnp transistor, which is crucial for understanding the transistor's operation in the forward-active region.

Figure 2.34 Minority-carrier distribution in the base of a lateral pnp transistor in the forward-active region. This distribution is that observed through section $x-x^{\prime}$ in Fig. 2.33b.

The collector current at which these effects become significant can be calculated for a lateral pnp transistor by equating the minority-carrier concentration given by (2.22) to the equilibrium majority-carrier concentration. Thus

$$
\begin{equation*}
\frac{J_{p} W_{B}}{q D_{p}}=n_{n} \simeq N_{D} \tag{2.23}
\end{equation*}
$$

where (2.1) has been substituted for $n_{n}$, and $N_{D}$ is the donor density in the pnp base ( $n p n$ collector). From (2.23), we can calculate the collector current for the onset of high-level injection in a pnp transistor as

$$
\begin{equation*}
I_{C}=\frac{q A N_{D} D_{p}}{W_{B}} \tag{2.24}
\end{equation*}
$$

where $A$ is the effective area of the emitter-base junction. Note that this current depends directly on the base doping density in the transistor, and since this is quite low in a lateral pnp transistor, the current density at which this fall-off begins is quite low.

Lateral pnp transistors are also widely used in shallow oxide-isolated bipolar IC technologies. The device structure used is essentially identical to that of Fig. 2.33, except that the device area is orders of magnitude smaller and the junction isolation is replaced by oxide isolation. Typical parameters for such a device are listed in Fig. 2.32. As in the case of $n p n$ transistors, we see dramatic reductions in device transit time and parasitic capacitance compared to the high-voltage, thick-epi process. The value of $\beta$ for such a device typically peaks at a collector current of about 50 nA .

#### EXAMPLE

Calculate the collector current at which the current gain begins to fall for the pnp structure of Fig. 2.33a. The effective cross-sectional area $A$ of the emitter is the sidewall area of the emitter, which is the $p$-type diffusion depth multiplied by the periphery of the emitter multiplied by $\pi / 2$.

$$
A=(3 \mu \mathrm{~m})(30 \mu \mathrm{~m}+30 \mu \mathrm{~m}+30 \mu \mathrm{~m}+30 \mu \mathrm{~m})\left(\frac{\pi}{2}\right)=565 \mu \mathrm{~m}^{2}=5.6 \times 10^{-6} \mathrm{~cm}^{2}
$$

The majority-carrier density is $10^{15}$ atoms $/ \mathrm{cm}^{3}$ for an epi-layer resistivity of $5 \Omega$ - cm . In addition, we can assume $W_{B}=8 \mu \mathrm{~m}$ and $D_{p}=10 \mathrm{~cm}^{2} / \mathrm{s}$. Substitution of this data in (2.24) gives

$$
I_{C}=5.6 \times 10^{-6} \times 1.6 \times 10^{-19} \times 10^{15} \times 10 \frac{1}{8 \times 10^{-4}} \mathrm{~A}=11.2 \mu \mathrm{~A}
$$

The typical lateral pnp structure of Fig. 2.33a shows a low-current beta of approximately 30 to 50, which begins to decrease at a collector current of a few tens of microamperes, and has fallen to less than 10 at a collector current of 1 mA . A typical set of parameters for a structure of this type is shown in Fig. 2.35. Note that in the lateral pnp transistor, the substrate junction capacitance appears between the base and the substrate.

Substrate pnp Transistors. One reason for the poor high-current performance of the lateral $p n p$ is the relatively small effective cross-sectional area of the emitter, which results from the lateral nature of the injection. A common application for a pnp transistor is in a Class-B output stage where the device is called on to operate at collector currents in the $10-\mathrm{mA}$ range. A lateral pnp designed to do this would require a large amount of die area. In this application, a different structure is usually used in which the substrate itself is used as the collector instead of a diffused $p$-type region. Such a substrate $p n p$ transistor in a high-voltage, thick-epi process is

|  | Parameter | Typical Value, 5- $\Omega-\mathrm{cm}, 17-\mu \mathrm{m}$ epi 44-V Device | Typical Value, $1-\Omega-\mathrm{cm}, 10-\mu \mathrm{m}$ epi 20-V Device |
| :---: | :---: | :---: | :---: |
|  | $\beta_{F}$ | 50 | 20 |
|  | $\beta_{R}$ | 4 | 2 |
|  | $V_{A}$ | 50 V | 50 V |
|  | $\eta$ | $5 \times 10^{-4}$ | $5 \times 10^{-4}$ |
|  | $I_{S}$ | $2 \times 10^{-15} \mathrm{~A}$ | $2 \times 10^{-15} \mathrm{~A}$ |
|  | $I_{C O}$ | $10^{-10} \mathrm{~A}$ | $5 \times 10^{-9} \mathrm{~A}$ |
|  | $B V_{\text {CEO }}$ | 60 V | 30 V |
|  | $B V_{\text {CBO }}$ | 90 V | 50 V |
|  | $B V_{\text {EBO }}$ | 90 V | 50 V |
|  | $\tau_{F}$ | 30 ns | 20 ns |
|  | $\tau_{R}$ | 3000 ns | 2000 ns |
|  | $\beta_{0}$ | 50 | 20 |
|  | $r_{b}$ | $300 \Omega$ | $150 \Omega$ |
|  | $r_{c}$ | $100 \Omega$ | $75 \Omega$ |
|  | $r_{e x}$ | $10 \Omega$ | $10 \Omega$ |
| Base-emitter junction | $\left\{\begin{array}{l} C_{j e 0} \\ \psi_{0 e} \\ n_{e} \end{array}\right.$ | 0.3 pF | 0.6 pF |
|  |  | 0.55 V | 0.6 V |
|  |  | 0.5 | 0.5 |
| Base-collector junction | $\left\{\begin{array}{l} C_{\mu 0} \\ \psi_{0 c} \\ n_{c} \end{array}\right.$ | 1 pF | 2 pF |
|  |  | 0.55 V | 0.6 V |
|  |  | 0.5 | 0.5 |
| Base-substrate junction | $\left\{\begin{array}{l} C_{b s 0} \\ \psi_{0 s} \\ n_{s} \end{array}\right.$ | 3 pF | 3.5 pF |
|  |  | 0.52 V | 0.58 V |
|  |  | 0.5 | 0.5 |

Figure 2.35 Typical parameters for lateral pnp transistors with $900 \mu^{2}$ emitter area in a highvoltage, thick-epi process.
shown in Fig. 2.36a. The $p$-type emitter diffusion for this particular substrate $p n p$ geometry is rectangular with a rectangular hole in the middle. In this hole an $n^{+}$region is formed with the npn emitter diffusion to provide a contact for the $n$-type base. Because of the lightly doped base material, the series base resistance can become quite large if the base contact is far removed from the active base region. In this particular structure, the $n^{+}$base contact diffusion is actually allowed to come in contact with the p-type emitter diffusion, in order to get the low-resistance base contact diffusion as close as possible to the active base. The only drawback of this, in a substrate pnp structure, is that the emitter-base breakdown voltage is reduced to approximately 7 V . If larger emitter-base breakdown is required, then the $p$-emitter diffusion must be separated from the $n^{+}$base contact diffusion by a distance of about $10 \mu \mathrm{~m}$ to $15 \mu \mathrm{~m}$. Many variations exist on the substrate pnp geometry shown in Fig. 2.36a. They can also be realized in thin-epi, oxide-isolated processes.

The minority-carrier flow in the forward-active region is illustrated in Fig. 2.36b. The principal advantage of this device is that the current flow is vertical and the effective crosssectional area of the emitter is much larger than in the case of the lateral pnp for the same overall device size. The device is restricted to use in emitter-follower configurations, however, since the collector is electrically identical with the substrate that must be tied to the most negative circuit potential. Other than the better current-handling capability, the properties of substrate $p n p$ transistors are similar to those for lateral pnp transistors since the base width is similar
image_name:Figure 2.36 (a)
description:The image labeled "Figure 2.36 (a)" depicts the structure of a substrate pnp transistor used in a high-voltage, thick-epi process. The diagram is divided into two main sections: a cross-sectional view and a top view.

1. **Identification of Components and Structure:**
- **Cross-Sectional View:** This part of the diagram illustrates the vertical structure of the substrate pnp transistor. It includes:
- **Emitter Contacts:** These are shown at the top surface, connected to p-type regions that extend into the n-type epitaxial layer.
- **Base Contact:** Located between the emitter contacts, connected to an n+ region within the n-type epitaxial layer.
- **n-type Epitaxial Layer:** This layer is positioned between the p-type emitter regions and the p-type substrate collector.
- **p-type Substrate Collector:** The bottom layer of the structure, serving as the collector for the transistor.

2. **Connections and Interactions:**
- The emitter contacts are connected to the p-type regions, which inject holes into the n-type epitaxial layer.
- The base contact controls the flow of these holes through the n-type layer, influencing the current flow to the p-type substrate collector.
- The collector current flows in the p-type substrate, which is typically tied to the most negative circuit potential.

3. **Labels, Annotations, and Key Features:**
- The top view includes labels for emitter (E) and base (B) regions, with a distance scale on the left indicating dimensions up to 120 micrometers.
- The cross-section is annotated to show the different layers and contacts, highlighting the n-type epi layer and p-type substrate collector.
- A symbolic representation of a pnp transistor is shown above the diagram, indicating the electrical connections between the emitter, base, and substrate.

Overall, the diagram provides a detailed view of the substrate pnp transistor's structure and its key components, illustrating how the device is designed to handle high voltages with its thick epitaxial layer.

Figure 2.36 (a) Substrate pnp structure in a high-voltage, thick-epi process.
image_name:Figure 2.36 (b) Minority-carrier flow in the substrate pnp transistor
description:The diagram labeled "Figure 2.36 (b) Minority-carrier flow in the substrate pnp transistor" illustrates the flow of minority carriers within a pnp transistor structure. The key components and structure of the diagram are as follows:

1. **Components and Structure:**
- **Emitter (E):** Denoted by a terminal at the top of the diagram, connecting to a p-type region. This region is responsible for injecting holes into the base.
- **Base (B):** Shown as a central n+ region between two p-type regions, connected to a terminal labeled 'B'. This region controls the flow of holes from the emitter to the collector.
- **Collector:** The p-type substrate collector is depicted at the bottom, collecting holes injected by the emitter.
- **Injected Holes:** Arrows indicate the flow of holes from the p-type emitter to the n+ base and then towards the p-type collector.

2. **Connections and Interactions:**
- The diagram shows electrical connections to the emitter (E) and base (B) regions, illustrating the path of hole flow (minority carriers) from the emitter through the base to the collector.
- The arrows represent the movement of holes, indicating the direction of current flow within the transistor.
- The interaction between the p-type and n+ regions facilitates the movement of holes, which are the minority carriers in the n+ base region.

3. **Labels, Annotations, and Key Features:**
- The diagram is annotated with labels such as 'E' for emitter, 'B' for base, and 'p-type substrate collector' to identify the components.
- "Injected holes" is clearly labeled, emphasizing the flow of carriers from the emitter to the collector.
- The n+ region is explicitly marked, highlighting its role in the transistor's operation.

Overall, the diagram provides a detailed view of the minority carrier flow in a substrate pnp transistor, focusing on the movement of holes from the emitter, through the base, and into the collector, which is crucial for the transistor's functionality.

(b)

Figure 2.36 (b) Minority-carrier flow in the substrate $p n p$ transistor.
in both cases. An important consideration in the design of substrate pnp structures is that the collector current flows in the $p$-substrate region, which usually has relatively high resistivity. Thus, unless care is taken to provide an adequate low-resistance path for the collector current, a high series collector resistance can result. This resistance can degrade device performance in two ways. First, large collector currents in the pnp can cause enough voltage drop in the substrate region itself that other substrate-epitaxial layer junctions within the circuit can become forward biased. This usually has a catastrophic effect on circuit performance. Second, the effects of the collector-base junction capacitance on the pnp are multiplied by the Miller effect resulting from the large series collector resistance, as described further in Chapter 7. To minimize these effects, the collector contact is usually made by contacting the isolation diffusion immediately adjacent to the substrate pnp itself with metallization. For high-current devices, this isolation diffusion contact is made to surround the device to as great an extent as possible.

The properties of a typical substrate $p n p$ transistor in a high-voltage, thick-epi process are summarized in Fig. 2.37. The dependence of current gain on collector current for a typical $n p n$, lateral $p n p$, and substrate $p n p$ transistor in a high-voltage, thick-epi process are shown in Fig. 2.38. The low-current reduction in $\beta$, which is apparent for all three devices, is due to recombination in the base-emitter depletion region, described in Section 1.3.5.

|  | Parameter | Typical Value, 5- $\Omega$-cm, 17- $\mu \mathrm{m}$ epi 44-V Device $5100 \mu \mathrm{~m}^{2}$ <br> Emitter Area | Typical Value, $1-\Omega-\mathrm{cm}, 10-\mu \mathrm{m}$ epi 20-V Device $5100 \mu \mathrm{~m}^{2}$ <br> Emitter Area |
| :---: | :---: | :---: | :---: |
|  | $\beta_{F}$ | 50 | 30 |
|  | $\beta_{R}$ | 4 | 2 |
|  | $V_{A}$ | 50 V | 30 V |
|  | $\eta$ | $5 \times 10^{-4}$ | $9 \times 10^{-4}$ |
|  | $I_{S}$ | $10^{-14} \mathrm{~A}$ | $10^{-14} \mathrm{~A}$ |
|  | $I_{C O}$ | $2 \times 10^{-10} \mathrm{~A}$ | $2 \times 10^{-10} \mathrm{~A}$ |
|  | $B V_{C E O}$ | 60 V | 30 V |
|  | $B V_{C B O}$ | 90 V | 50 V |
|  | $B V_{\text {EBO }}$ | 7 V or 90 V | 7 V or 50 V |
|  | $\tau_{F}$ | 20 ns | 14 ns |
|  | $\tau_{R}$ | 2000 ns | 1000 ns |
|  | $\beta_{0}$ | 50 | 30 |
|  | $r_{b}$ | $150 \Omega$ | $50 \Omega$ |
|  | $r_{c}$ | $50 \Omega$ | $50 \Omega$ |
|  | $r_{e x}$ | $2 \Omega$ | $2 \Omega$ |
| Base-emitter junction | $\left\{\begin{array}{l}C_{j e 0} \\ \psi_{0 e} \\ n_{e}\end{array}\right.$ | $\begin{aligned} & 0.5 \mathrm{pF} \\ & 0.55 \mathrm{~V} \\ & 0.5 \end{aligned}$ | $\begin{aligned} & 1 \mathrm{pF} \\ & 0.58 \mathrm{~V} \\ & 0.5 \end{aligned}$ |
| Base-collector junction | $\left\{\begin{array}{l}C_{\mu 0} \\ \psi_{0 c} \\ n_{c}\end{array}\right.$ | $\begin{aligned} & 2 \mathrm{pF} \\ & 0.52 \mathrm{~V} \\ & 0.5 \end{aligned}$ | $\begin{aligned} & 3 \mathrm{pF} \\ & 0.58 \mathrm{~V} \\ & 0.5 \end{aligned}$ |

Figure 2.37 Typical device parameters for a substrate pnp with $5100 \mu^{2}$ emitter area in a highvoltage, thick-epi process.
image_name:Figure 2.38
description:The graph in Figure 2.38 is a plot of current gain (β_F) as a function of collector current for different transistor geometries: npn, substrate pnp, and lateral pnp transistors, all in a high-voltage, thick-epi process.

1. **Type of Graph and Function**: This is a logarithmic plot showing the relationship between collector current and current gain for various transistor types.

2. **Axes Labels and Units**:
- The x-axis represents the collector current, labeled in amperes (A), with a logarithmic scale ranging from 0.1 μA to 100 mA.
- The y-axis represents the current gain (β_F), also on a logarithmic scale, ranging from 10 to 1000.

3. **Overall Behavior and Trends**:
- **npn Transistor**: The current gain increases with collector current, reaching a peak and then gradually decreasing.
- **Substrate pnp Transistor**: The current gain follows a similar trend as the npn transistor but starts at a lower gain and peaks at a lower collector current.
- **Lateral pnp Transistor**: This transistor type shows the lowest initial gain, with a peak at a lower collector current than the other two transistors, and a more rapid decline after the peak.

4. **Key Features and Technical Details**:
- The npn transistor with a 500 μm² emitter area shows the highest peak gain.
- The substrate pnp transistor with a 5100 μm² emitter area has a moderate peak gain.
- The lateral pnp transistor with a 900 μm² emitter area exhibits the lowest peak gain.

5. **Annotations and Specific Data Points**:
- The graph is annotated with the transistor types and their respective emitter areas, indicating the differences in performance across these geometries.
- No specific numerical values for peak gains or exact collector current values at peaks are provided, but the trends are clearly visible.

Figure 2.38 Current gain as a function of collector current for typical lateral $p n p$, substrate $p n p$, and $n p n$ transistor geometries in a high-voltage, thick-epi process.

## 2.6 Passive Components in Bipolar Integrated Circuits

In this section, we describe the structures available to the integrated-circuit designer for realization of resistance and capacitance. Resistor structures include base-diffused, emitter-diffused, ion-implanted, pinch, epitaxial, and pinched epitaxial resistors. Other resistor technologies, such as thin-film resistors, are considered in Section 2.7.3. Capacitance structures include MOS and junction capacitors. Inductors with values larger than a few nanohenries have not proven to be feasible in monolithic technology. However, such small inductors are useful in very high frequency integrated circuits. ${ }^{14,15,16}$

### 2.6.1 Diffused Resistors

In an earlier section of this chapter, the sheet resistance of a diffused layer was calculated. Integrated-circuit resistors are generally fabricated using one of the diffused or ion-implanted layers formed during the fabrication process, or in some cases a combination of two layers. The layers available for use as resistors include the base, the emitter, the epitaxial layer, the buried layer, the active-base region layer of a transistor, and the epitaxial layer pinched between the base diffusion and the $p$-type substrate. The choice of layer generally depends on the value, tolerance, and temperature coefficient of the resistor required.
image_name:epi
description:
[
name: D1, type: Diode, ports: {Na: epi, Nc: A}
name: D2, type: Diode, ports: {Na: B, Nc: epi}
name: R, type: Resistor, ports: {N1: A, N2: B}
]
extrainfo:The diagram shows a base-diffused resistor structure used in high-voltage processes. The resistor is formed from the p-type base diffusion for npn transistors and is situated in a separate isolation region. The epitaxial region must be reverse-biased to maintain the pn junction between the resistor and the epi layer.
image_name:Base-diffused resistor structure
description:The image depicts a base-diffused resistor structure used in a high-voltage process, specifically focusing on a resistor formed from the p-type base diffusion for npn transistors. The diagram is divided into two main parts: a schematic top view and a cross-sectional side view.

1. **Identification of Components and Structure:**
- **Top View:**
- The resistor is represented by a rectangular area within an isolation region, marked by dashed lines. It includes two contacts labeled 'R' on either end, connected by a path indicating the resistor's length (L) and width (W).
- There are additional symbols such as triangles indicating connections or vias.
- **Side View:**
- The cross-section shows the layers involved: a p-type diffusion layer where the resistor is formed, an n-type epitaxial layer, and an n+ buried layer situated above a p-type substrate.
- Resistor contacts are shown on the surface, connecting through the p-type diffusion.
- An isolation pocket contact is also depicted, ensuring electrical isolation of the resistor structure.

2. **Connections and Interactions:**
- The resistor is isolated within a specific region to ensure that the pn junction between the resistor and the epitaxial layer remains reverse-biased. This is crucial to prevent unwanted current flow.
- The schematic includes a simple circuit with diodes (D1, D2) and a resistor (R) connected in series, showing potential connections for biasing or integrating the resistor into a larger circuit.

3. **Labels, Annotations, and Key Features:**
- The diagram includes measurements in micrometers along the axes to provide scale.
- Key labels include 'p-type diffusion,' 'resistor contact,' and 'isolation pocket contact,' which help identify the specific elements and their functions.
- Annotations such as 'epi' refer to the epitaxial layer, crucial for understanding the material properties and interactions within the structure.

Overall, the image provides a comprehensive view of a base-diffused resistor's design, highlighting the integration of various semiconductor layers and the importance of isolation and biasing in its operation.

Figure 2.39 Base-diffused resistor structure.

Base and Emitter Diffused Resistors. The structure of a typical base-diffused resistor in a high-voltage process is shown in Fig. 2.39. The resistor is formed from the $p$-type base diffusion for the $n p n$ transistors and is situated in a separate isolation region. The epitaxial region into which the resistor structure is diffused must be biased in such a way that the pn junction between the resistor and the epi layer is always reverse biased. For this reason, a contact is made to the $n$-type epi region as shown in Fig. 2.39, and it is connected either to that end of the resistor that is most positive or to a potential that is more positive than either end of the resistor. The junction between these two regions contributes a parasitic capacitance between the resistor and the epi layer, and this capacitance is distributed along the length of the resistor. For most applications, this parasitic capacitance can be adequately modeled by separating it into two lumped portions and placing one lump at each end of the resistor as illustrated in Fig. 2.40.

The resistance of the structure shown in Fig. 2.39 is given by (2.10) as

$$
R=\frac{L}{W} R_{\square}
$$

where $L$ is the resistor length and $W$ is the width. The base sheet resistance $R_{\square}$ lies in the range 100 to $200 \Omega / \square$, and thus resistances in the range $50 \Omega$ to $50 \mathrm{k} \Omega$ are practical using the base diffusion. The resistance contributed by the clubheads at each end of the resistor can be significant, particularly for small values of $L / W$. The clubheads are required to allow space for ohmic contact to be made at the ends of the resistor.
image_name:Figure 2.40 Lumped model for the base-diffused resistor
description:
[
name: R, type: Resistor, value: R□(L/W), ports: {N1: X1, N2: X2}
name: Cj/2, type: Capacitor, value: Cj/2, ports: {Np: X1, Nn: X3}
name: Cj/2, type: Capacitor, value: Cj/2, ports: {Np: X2, Nn: X3}
]
extrainfo:The circuit represents a lumped model for a base-diffused resistor with two capacitors modeling parasitic capacitance to an isolation region.

Figure 2.40 Lumped model for the base-diffused resistor.

Since minimization of die area is an important objective, the width of the resistor is kept as small as possible, the minimum practical width being limited to about $1 \mu \mathrm{~m}$ by photolithographic considerations. Both the tolerance on the resistor value and the precision with which two identical resistors can be matched can be improved by the use of wider geometries. However, for a given base sheet resistance and a given resistor value, the area occupied by the resistor increases as the square of its width. This can be seen from (2.10) since the ratio $L / W$ is constant.

In shallow ion-implanted processes, the ion-implanted base can be used in the same way to form a resistor.

#### EXAMPLE

Calculate the resistance and parasitic capacitance of the base-diffused resistor structure shown in Fig. 2.39 for a base sheet resistance of $100 \Omega / \square$, and an epi resistivity of $2.5 \Omega-\mathrm{cm}$. Neglect end effects. The resistance is simply

$$
R=100 \Omega / \square\left(\frac{100 \mu \mathrm{~m}}{10 \mu \mathrm{~m}}\right)=1 \mathrm{k} \Omega
$$

The capacitance is the total area of the resistor multiplied by the capacitance per unit area. The area of the resistor body is

$$
A_{1}=(10 \mu \mathrm{~m})(100 \mu \mathrm{~m})=1000 \mu \mathrm{~m}^{2}
$$

The area of the clubheads is

$$
A_{2}=2(30 \mu \mathrm{~m} \times 30 \mu \mathrm{~m})=1800 \mu \mathrm{~m}^{2}
$$

The total zero-bias capacitance is, from Fig. 2.29,

$$
C_{j 0}=\left(10^{-4} \mathrm{pF} / \mu \mathrm{m}^{2}\right)\left(2800 \mathrm{um}^{2}\right)=0.28 \mathrm{pF}
$$

As a first-order approximation, this capacitance can be divided into two parts, one placed at each end. Note that this capacitance will vary depending on the voltage at the clubhead with respect to the epitaxial pocket.

Emitter-diffused resistors are fabricated using geometries similar to the base resistor, but the emitter diffusion is used to form the actual resistor. Since the sheet resistance of this diffusion is in the 2 to $10 \Omega / \square$ range, these resistors can be used to advantage where very low resistance values are required. In fact, they are widely used simply to provide a crossunder beneath an aluminum metallization interconnection. The parasitic capacitance can be
image_name:Figure 2.41 Pinch resistor structure
description:The image labeled "Figure 2.41 Pinch resistor structure" illustrates the structure and components of a pinch resistor used in semiconductor devices. The diagram is divided into two main sections: a top view of the layout and a cross-sectional view of the structure.

1. **Identification of Components and Structure:**
- The top section shows a schematic circuit representation with two diodes (D1 and D2) connected in parallel to a resistor (R) between points A and B. This is labeled as being within an "epi/isolation pocket."
- The lower section provides a cross-sectional view of the physical structure. It includes several layers and regions:
- **p-type substrate:** The base layer of the semiconductor structure.
- **n+ diffusion:** A heavily doped n-type region, which forms part of the pinched region.
- **n diffusion:** A lighter doped n-type region above the n+ diffusion.
- **Pinched region:** The area between the n+ emitter and n-type collector regions, where the resistor is formed.
- **SiO2 layer:** An insulating layer on top.
- **Resistor contact:** Metal contacts that connect the resistor to the circuit.
- **Isolation pocket contact:** Contacts that help isolate the pocket from other regions.

2. **Connections and Interactions:**
- The schematic shows the connection of diodes D1 and D2 in parallel to the resistor R, indicating a possible protection or feedback mechanism.
- The cross-sectional view shows how the resistor is physically isolated and contacted through the SiO2 layer, ensuring it is electrically connected to the desired circuit paths.

3. **Labels, Annotations, and Key Features:**
- The diagram includes labels for various regions and components, such as "p-type diffusion," "n+ diffusion," and "Pinched region."
- Arrows and dashed lines in the top view indicate the flow of current and the boundaries of the epi/isolation pocket.
- The cross-sectional view helps visualize the vertical structure and how different layers interact to form the resistor.

This detailed layout and cross-section provide insight into the construction and functionality of the pinch resistor within an integrated circuit, emphasizing its role in electrical isolation and signal management.

Figure 2.41 Pinch resistor structure.
calculated in a way similar to that for the base diffusion. However, these resistors have different temperature dependence from base-diffused resistors and the two types do not track with temperature.

Base Pinch Resistors. A third layer available for use as a resistor is the layer that forms the active base region in the npn transistor. This layer is pinched between the $n^{+}$emitter and the $n$-type collector regions, giving rise to the term pinch resistor. The layer can be electrically isolated by reverse biasing the emitter-base and collector-base junctions, which is usually accomplished by connecting the $n$-type regions to the most positive end of the resistor. The structure of a typical pinch resistor is shown in Fig. 2.41; the $n^{+}$diffusion overlaps the $p$-diffusion so that the $n^{+}$region is electrically connected to the $n$-type epi region. The sheet resistance is in the $5 \mathrm{k} \Omega / \square$ to $15 \mathrm{k} \Omega / \square$ range. As a result, this resistor allows the fabrication of large values of resistance. Unfortunately, the sheet resistance undergoes the same processrelated variations as does the $Q_{B}$ of the transistor, which is approximately $\pm 50$ percent. Also, because the material making up the resistor itself is relatively lightly doped, the resistance displays a relatively large variation with temperature. Another significant drawback is that the maximum voltage that can be applied across the resistor is limited to around 6 V because of the breakdown voltage between the emitter-diffused top layer and the base diffusion. Nonetheless, this type of resistor has found wide application where the large tolerance and low breakdown voltage are not significant drawbacks.

### 2.6.2 Epitaxial and Epitaxial Pinch Resistors

The limitation of the pinch resistor to low operating voltages disallows its use in circuits where a small bias current is to be derived directly from a power-supply voltage of more than about 7 V using a large-value resistor. The epitaxial layer itself has a sheet resistance much larger than the base diffusion, and the epi layer is often used as a resistor for this application. For example, the sheet resistance of a $17-\mu \mathrm{m}$ thick, $5-\Omega-\mathrm{cm}$ epi layer can be calculated from (2.11) as

$$
\begin{equation*}
R_{\square}=\frac{\rho_{\text {epi }}}{T}=\frac{5 \Omega-\mathrm{cm}}{(17 \mu \mathrm{~m}) \times\left(10^{-4} \mathrm{~cm} / \mu \mathrm{m}\right)}=2.9 \mathrm{k} \Omega / \square \tag{2.25}
\end{equation*}
$$

Large values of resistance can be realized in a small area using structures of the type shown in Fig. 2.42. Again, because of the light doping in the resistor body, these resistors display a rather large temperature coefficient. A still larger sheet resistance can be obtained by putting a $p$-type base diffusion over the top of an epitaxial resistor, as shown in Fig. 2.42. The depth of the $p$-type base and the thickness of the depletion region between the $p$-type base and the
image_name:epi resistor (no top p+ diffusion)
description:
[
name: R, type: Resistor, value: R, ports: {N1: N1, N2: N2}
]
extrainfo:The diagram illustrates an epitaxial resistor structure without top p+ diffusion. It includes a cross-sectional view showing the n+ regions and optional p cap on a p-type substrate. The resistor is designed to achieve large resistance values in a small area.
image_name:epi-FET with top plate (two alternate symbols)
description:
[
name: R, type: Resistor, value: R, ports: {N1: R, N2: R}
]
extrainfo:The diagram illustrates an epitaxial resistor structure with an optional p-cap diffusion forming an epitaxial pinch resistor. It also shows two alternate symbols for an epi-FET with a top plate. The structure is built on a p-type substrate with n+ regions for resistor contacts.
image_name:Figure 2.42 Epitaxial resistor structure
description:The diagram labeled "Figure 2.42 Epitaxial resistor structure" illustrates a cross-sectional view of an epitaxial resistor on a semiconductor substrate. The diagram includes several components and annotations:

1. **Components and Structure:**
- **Epitaxial Resistor:** The main component is the epitaxial resistor, depicted as a rectangular structure on a p-type substrate. The resistor is formed by an n-type region, which is lightly doped, and lies between two n+ regions that serve as contacts.
- **Optional p+ Cap:** An optional p+ diffusion layer is shown above the n-type region, labeled as "Optional p cap." This layer can be used to form an epitaxial pinch resistor, enhancing the resistance by creating a depletion region.
- **Resistor Contacts:** Two resistor contacts are situated at either end of the n-type region, allowing for electrical connection.

2. **Connections and Interactions:**
- The resistor contacts are connected to the n+ regions, facilitating current flow through the n-type region. The presence of the optional p+ cap modifies the electrical characteristics by introducing a controlled depletion region.

3. **Labels, Annotations, and Key Features:**
- The top of the diagram includes symbolic representations of the epitaxial resistor and epi-FET with top plate, indicating possible circuit symbol usage.
- The substrate is identified as p-type, with the n-type and n+ regions clearly marked.
- The diagram highlights the optional nature of the p+ cap diffusion, emphasizing its role in forming a pinch resistor.

Overall, the diagram provides a detailed view of the structure and function of an epitaxial resistor, including optional modifications for increased resistance.

Figure 2.42 Epitaxial resistor structure. The $p$-cap diffusion is optional and forms an epitaxial pinch resistor.

| Resistor Type | Sheet $\rho$ <br> $\Omega / \square$ | Absolute Tolerance (\%) | Matching <br> Tolerance (\%) | Temperature Coefficient |
| :---: | :---: | :---: | :---: | :---: |
| Base diffused | 100 to 200 | $\pm 20$ | $\pm 2(5 \mu \mathrm{~m}$ wide $)$ <br> $\pm 0.2(50 \mu \mathrm{~m}$ wide $)$ | $(+1500$ to +2000$) \mathrm{ppm} /{ }^{\circ} \mathrm{C}$ |
| Emitter diffused | 2 to 10 | $\pm 20$ | $\pm 2$ | $+600 \mathrm{ppm} /{ }^{\circ} \mathrm{C}$ |
| Ion implanted | 100 to 1000 | $\pm 3$ | $\begin{aligned} & \pm 1(5 \mu \mathrm{~m} \text { wide }) \\ & \pm 0.1(50 \mu \mathrm{~m} \text { wide }) \end{aligned}$ | Controllable to $\pm 100 \mathrm{ppm} /{ }^{\circ} \mathrm{C}$ |
| Base pinch | 2k to 10k | $\pm 50$ | $\pm 10$ | $+2500 \mathrm{ppm} /{ }^{\circ} \mathrm{C}$ |
| Epitaxial | 2k to 5k | $\pm 30$ | $\pm 5$ | +3000 ppm/ ${ }^{\circ} \mathrm{C}$ |
| Epitaxial pinch | 4k to 10k | $\pm 50$ | $\pm 7$ | +3000 ppm/ ${ }^{\circ} \mathrm{C}$ |
| Thin film | 0.1 k to 2 k | $\pm 5$ to $\pm 20$ | $\pm 0.2$ to $\pm 2$ | $( \pm 10$ to $\pm 200) \mathrm{ppm} /{ }^{\circ} \mathrm{C}$ |

Figure 2.43 Summary of resistor properties for different types of IC resistors.
n-type epi together reduce the thickness of the resistor, increasing its sheet resistance. Such a structure actually behaves as a junction FET, in which the $p$-type gate is tied to the substrate. ${ }^{17}$

The properties of the various diffused and pinch-resistor structures are summarized in Fig. 2.43.

### 2.6.3 Integrated-Circuit Capacitors

Early analog integrated circuits were designed on the assumption that capacitors of usable value were impractical to integrate on the chip because they would take too much area, and external capacitors were used where required. Monolithic capacitors of value larger than a few tens of picofarads are still expensive in terms of die area. As a result, design approaches have evolved for monolithic circuits that allow small values of capacitance to be used to perform functions that previously required large capacitance values. The compensation of operational amplifiers is perhaps the best example of this result, and monolithic capacitors are now widely used in all types of analog integrated circuits. These capacitors fall into two categories. First, pn junctions under reverse bias inherently display depletion capacitance, and in certain circumstances this capacitance can be effectively utilized. The drawbacks of junction capacitance are that the junction must always be kept reverse biased, that the capacitance varies with reverse voltage, and that the breakdown voltage is only about 7 V for the emitter-base junction. For the collector-base junction, the breakdown voltage is higher, but the capacitance per unit area is quite low.

By far the most commonly used monolithic capacitor in bipolar technology is the MOS capacitor structure shown in Fig. 2.44. In the fabrication sequence, an additional mask step is inserted to define a region over an emitter diffusion on which a thin layer of silicon dioxide is grown. Aluminum metallization is then placed over this thin oxide, producing a capacitor between the aluminum and the emitter diffusion, which has a capacitance of $0.3 \mathrm{fF} / \mu \mathrm{m}^{2}$ to $0.5 \mathrm{fF} / \mathrm{\mu m}^{2}$ and a breakdown voltage of 60 V to 100 V . This capacitor is extremely linear and has a low temperature coefficient. A sizable parasitic capacitance $C_{I S O}$ is present between the n-type bottom plate and the substrate because of the depletion capacitance of the epi-substrate junction, but this parasitic is unimportant in many applications.
image_name:Figure 2.44 MOS capacitor structure
description:
[
name: C, type: Capacitor, value: C, ports: {Np: C1, Nn: C2}
name: CISO, type: Capacitor, value: CISO, ports: {Np: C1, Nn: Substrate}
]
extrainfo:The circuit diagram represents a MOS capacitor structure with three capacitors: C1, C2, and a parasitic capacitor CISO. CISO represents the parasitic capacitance between the n-type bottom plate and the substrate due to the depletion capacitance of the epi-substrate junction. The diagram also shows a thin oxide mask and an aluminum contact over an n-type epitaxial layer on a p-type substrate.
image_name:Figure 2.44 MOS capacitor structure
description:The image depicts a MOS capacitor structure with a schematic representation and a cross-sectional view of the physical construction.

1. **Identification of Components and Structure:**
- **Schematic Diagram:**
- The schematic at the top shows a simple capacitor network with two capacitors, labeled \(C\) and \(C_{ISO}\), connected between nodes \(C_1\), \(C_2\), and the substrate.
- \(C_{ISO}\) represents a parasitic capacitance between the n-type bottom plate and the substrate.
- \(C\) is the main capacitance between the aluminum contact and the emitter diffusion.
- **Cross-Sectional View:**
- The lower part of the image illustrates the cross-sectional view of the MOS capacitor structure.
- The structure includes an aluminum contact on top, layered over a silicon dioxide (SiO2) insulator.
- Below the SiO2, there is an n+ doped region within an n-type epitaxial layer.
- The entire structure is built on a p-type substrate.

2. **Connections and Interactions:**
- The aluminum contact is electrically connected to the n+ region through the SiO2 layer, forming the primary capacitance \(C\).
- The parasitic capacitance \(C_{ISO}\) arises between the n-type epitaxial layer and the p-type substrate due to the depletion region formed at their junction.
- The thin oxide mask is indicated, suggesting a controlled area for the diffusion process.

3. **Labels, Annotations, and Key Features:**
- Labels \(C_1\) and \(C_2\) indicate connection points in the schematic.
- The thin oxide mask is annotated in the diagram, highlighting areas with specific oxide thickness.
- The cross-section clearly marks the layers and materials, providing insight into the physical construction of the MOS capacitor.

Overall, the diagram provides both a conceptual and a physical view of a MOS capacitor, illustrating its electrical connections and material composition.
Figure 2.44 MOS capacitor structure.

### 2.6.4 Zener Diodes

As described in Chapter 1, the emitter-base junction of the npn transistor structure displays a reverse breakdown voltage of between 6 V and 8 V , depending on processing details. When the total supply voltage is more than this value, the reverse-biased, emitter-base junction is useful as a voltage reference for the stabilization of bias reference circuits, and for such functions as level shifting. The reverse bias $I-V$ characteristic of a typical emitter-base junction is illustrated in Fig. 2.45a.

An important aspect of the behavior of this device is the temperature sensitivity of the breakdown voltage. The actual breakdown mechanism is dominated by quantum mechanical tunneling through the depletion layer when the breakdown voltage is below about 6 V ; it is dominated by avalanche multiplication in the depletion layer at the larger breakdown voltages. Because these two mechanisms have opposite temperature coefficients of breakdown voltage, the actually observed breakdown voltage has a temperature coefficient that varies with the value of breakdown voltage itself, as shown in Fig. 2.45b.
image_name:(a)
description:The graph in Figure 2.45 (a) represents the current-voltage (I-V) characteristic of a typical emitter-base Zener diode.

1. **Type of Graph and Function:**
- The graph is a current-voltage (I-V) characteristic curve, which is commonly used to illustrate the behavior of diodes.

2. **Axes Labels and Units:**
- The horizontal axis is labeled 'V' for voltage, measured in volts (V).
- The vertical axis is labeled 'I' for current, measured in amperes (A).
- The scales on both axes appear to be linear.

3. **Overall Behavior and Trends:**
- The graph shows a sharp increase in current after a certain threshold voltage is reached, indicating the Zener breakdown region.
- Initially, as the voltage increases, the current remains nearly zero, showing that the diode is in its non-conducting state.
- At approximately 6.2 V, the current begins to rise steeply, indicating the onset of Zener breakdown where the diode starts to conduct significantly.

4. **Key Features and Technical Details:**
- The breakdown voltage is clearly marked at 6.2 V, which is a critical value for the operation of the Zener diode.
- This point signifies the transition from the non-conducting state to the conducting state due to the Zener effect.
- The steep slope beyond 6.2 V indicates a low dynamic resistance, typical of Zener diodes in breakdown.

5. **Annotations and Specific Data Points:**
- The graph does not have additional annotations or markers beyond the labeled breakdown voltage.
- The curve's sharp transition at 6.2 V is the most significant feature, highlighting the diode's Zener breakdown behavior.
Figure 2.45 (a) Current-voltage characteristic of a typical emitter-base Zener diode.
image_name:Figure 2.45 (b)
description:The graph in Figure 2.45 (b) is a plot depicting the relationship between the junction breakdown voltage and the typical temperature coefficient of a Zener diode.

1. **Type of Graph and Function:**
- This is a two-dimensional plot showing the temperature coefficient of the breakdown voltage as a function of the breakdown voltage itself.

2. **Axes Labels and Units:**
- The x-axis is labeled "Junction breakdown voltage" and is measured in volts (V). The scale is linear, with markers at intervals of 2 volts ranging from 0 to 12 volts.
- The y-axis is labeled "Typical temperature coefficient" and is measured in millivolts per degree Celsius (mV/°C). The scale is linear, with markers at intervals of 1 mV/°C, ranging from -3 to 6 mV/°C.

3. **Overall Behavior and Trends:**
- The graph shows an S-shaped curve starting below the x-axis at lower breakdown voltages and rising above the x-axis at higher breakdown voltages.
- Initially, the temperature coefficient is negative, indicating a decrease in breakdown voltage with increasing temperature.
- As the breakdown voltage increases, the temperature coefficient transitions to positive, indicating an increase in breakdown voltage with temperature.

4. **Key Features and Technical Details:**
- The curve crosses the x-axis around a breakdown voltage of approximately 5 volts, where the temperature coefficient is zero. This point marks a transition from a negative to a positive temperature coefficient.
- The slope of the curve increases steadily beyond 5 volts, indicating a stronger positive temperature coefficient with higher breakdown voltages.

5. **Annotations and Specific Data Points:**
- There are no specific annotations or markers on the graph other than the labeled axes and the plotted curve itself.
- The key transition point at around 5 volts is a critical feature of the graph, highlighting the shift in temperature behavior of the diode.

(b)

Figure 2.45 (b) Temperature coefficient of junction breakdown voltage as a function of breakdown voltage.

### 2.6.5 Junction Diodes

Junction diodes can be formed by various connections of the npn and pnp transistor structures, as illustrated in Fig. 2.46. When the diode is forward biased in the diode connections $a, b$, and $d$ of Fig. 2.46, the collector-base junction becomes forward biased as well. When this occurs, the collector-base junction injects holes into the epi region that can be collected by the reverse-biased, epi-isolation junction or by other devices in the same isolation region. A similar phenomenon occurs when a transistor enters saturation. As a result, substrate currents can flow that can cause voltage drops in the high-resistivity substrate material, and other epiisolation junctions within the circuit can become inadvertently forward biased. Thus the diode connections of Fig. 2.46c are usually preferable since they keep the base-collector junction at zero bias. These connections have the additional advantage of resulting in the smallest amount of minority charge storage within the diode under forward-bias conditions.
image_name:(a)
description:
[
name: D1, type: Diode, ports: {Na: X1, Nc: X2}
name: D2, type: Diode, ports: {Na: X0, Nc: X2}
name: Q1, type: NPN, ports: {C: c1, B: b1, E: e1}
name: Q2, type: PNP, ports: {C: c2, B: b2, E: e2}
]
extrainfo:The circuit diagram (a) includes two diodes D1 and D2, and two transistors Q1 (NPN) and Q2 (PNP). Diode D1 is connected between nodes X1 and X2, while diode D2 is connected between nodes X10 and X2. The NPN transistor Q1 has its collector at C1, base at b1, and emitter at e1. The PNP transistor Q2 has its collector at C2, base at b2, and emitter at e2.
(a)
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: C1, B: b1, E: e1}
name: Q2, type: PNP, ports: {C: C2, B: b2, E: e2}
]
extrainfo:The circuit diagram (a) includes two transistors: Q1 (NPN) with its collector at C1, base at b1, and emitter at e1, and Q2 (PNP) with its collector at C2, base at b2, and emitter at e2. The diagram illustrates the basic configuration of these transistors.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: C1, B: b1, E: e1}
name: Q2, type: PNP, ports: {C: C2, B: b2, E: e2}
]
extrainfo:The circuit diagram (b) includes two transistors: Q1 (NPN) with collector at C1, base at b1, and emitter at e1, and Q2 (PNP) with collector at C2, base at b2, and emitter at e2. The diagram shows the configuration of these transistors without additional components like diodes or resistors.
(b)
image_name:(c)
description:
[
name: Q1, type: NPN, ports: {C: b1c1, B: b1c1, E: e1}
name: Q2, type: PNP, ports: {C: b2c2, B: b2c2, E: e2}
]
extrainfo:The circuit diagram (c) shows two transistors: Q1 (NPN) and Q2 (PNP). Both transistors have their collector and base connected to the same node (b1c1 for Q1 and b2c2 for Q2). The emitters are connected to separate nodes (e1 for Q1 and e2 for Q2).
(c)
image_name:(c)
description:
[
name: Q1, type: NPN, ports: {C: b1c1, B: b1c1, E: e1}
name: Q2, type: PNP, ports: {C: b2c2, B: b2c2, E: e2}
]
extrainfo:The circuit diagram shows two transistors: Q1 (NPN) and Q2 (PNP). Both transistors have their collector and base connected to the same node (b1c1 for Q1 and b2c2 for Q2). The emitters are connected to separate nodes (e1 for Q1 and e2 for Q2).

image_name:(d)
description:
[
name: Q1, type: NPN, ports: {C: b1c1, B: b1c1, E: e1}
name: Q2, type: PNP, ports: {C: b2c2, B: b2c2, E: e2}
]
extrainfo:The circuit diagram shows two transistors: Q1 (NPN) and Q2 (PNP). Both transistors have their collector and base connected to the same node (b1c1 for Q1 and b2c2 for Q2). The emitters are connected to separate nodes (e1 for Q1 and e2 for Q2).

Figure 2.46 Diode connections for $n p n$ and $p n p$ transistors.

## 2.7 Modifications to the Basic Bipolar Process

The basic high-voltage bipolar IC fabrication process described previously can be modified by the addition of extra processing steps to produce special devices or characteristics.

### 2.7.1 Dielectric Isolation

We first consider a special isolation technique-dielectric isolation-that has been used in digital and analog integrated circuits that must operate at very high speed and/or must operate in the presence of large amounts of radiation. The objective of the isolation technique is to electrically isolate the collectors of the devices from each other with a layer of silicon dioxide rather than with a $p n$ junction. This layer has much lower capacitance per unit area than a $p n$ junction, and as a result, the collector-substrate capacitance of the transistors is greatly reduced. Also, the reverse photocurrent that occurs with junction-isolated devices under intense radiation is eliminated.

The fabrication sequence used for dielectric isolation is illustrated in Figs. 2.47a-d. The starting material is a wafer of $n$-type material of resistivity appropriate for the collector region of the transistor. The first step is to etch grooves in the back side of the starting wafer, which will become the isolation regions in the finished circuit. These grooves are about $20 \mu \mathrm{~m}$ deep for typical analog circuit processing. This step, called moat etch, can be accomplished with a variety of techniques, including a preferential etch that allows precise definition of the depth of the moats. Next, an oxide is grown on the surface and a thick layer of polycrystalline silicon is deposited on the surface. This layer will be the mechanical support for the finished wafer and thus must be on the order of $200 \mu \mathrm{~m}$ thick. Next, the starting wafer is etched or ground from the top side until it is entirely removed except for the material left in the isolated islands between the moats, as illustrated in Fig. 2.47c. After the growth of an oxide, the wafer is ready for the rest of the standard process sequence. Note that the isolation of each device is accomplished by means of an oxide layer.
image_name:(a)
description:The image illustrates the fabrication steps in dielectric isolation, specifically focusing on step (a). In this step, a moat etch is performed on the bottom of an n-type wafer. The diagram shows a cross-sectional view of the wafer with etched moats. The top surface of the wafer is covered with a thin layer of silicon dioxide (SiO2), which provides insulation. The etching creates a series of V-shaped grooves or moats in the n-type silicon substrate. These moats are designed to isolate different regions of the wafer for subsequent processing steps. The SiO2 layer is crucial for electrical isolation and serves as a barrier between different sections of the wafer. This step is foundational for creating isolated sections that will later house individual electronic components or circuits. The diagram is labeled to indicate the n-type wafer and the SiO2 layer, with arrows pointing to the moat etch process, emphasizing the structural changes made to the wafer during this step.
image_name:(b)
description:The image labeled "(b)" depicts a stage in the fabrication process of dielectric isolation for semiconductor devices. This stage involves the deposition of a polycrystalline silicon support layer over a previously etched n-type silicon wafer. The image shows a cross-sectional view where the n-type wafer has been etched to create a series of moats or trenches. These trenches are lined with a thin layer of silicon dioxide (SiO₂), which serves as an insulating layer.

Above the etched n-type wafer, a layer of polycrystalline silicon is deposited, filling the trenches and covering the entire surface uniformly. This polycrystalline silicon layer acts as a mechanical support for the structure, providing stability and rigidity for subsequent processing steps.

Key features of the image include:
1. **n-type Wafer:** The base material, shown as a large gray area, which has been etched to form trenches.
2. **SiO₂ Layer:** A thin dark line representing the silicon dioxide insulating layer that lines the trenches and covers the surface of the n-type wafer.
3. **Polycrystalline Silicon Layer:** A dotted area representing the deposited polycrystalline silicon, covering the entire structure and filling the moats.

This stage is crucial for preparing the wafer for further processing, ensuring that the devices are electrically isolated from each other by the oxide layer and supported by the polycrystalline silicon.
image_name:(c)
description:The image labeled "(c)" illustrates a step in the fabrication process of dielectric isolation for semiconductor devices. In this step, the starting wafer has been ground off from the top side, revealing the isolated islands of material left between the moats.

**1. Identification of Components and Structure:**
- The image shows a cross-sectional view where the n-type wafer has been reduced to isolated sections.
- These sections are separated by etched moats which are filled with an insulating material, likely silicon dioxide (SiO₂), as indicated by the labels.
- The remaining n-type regions are supported by a layer of polycrystalline silicon beneath them, which provides mechanical stability.

**2. Connections and Interactions:**
- The polycrystalline silicon acts as a mechanical support layer, ensuring that the isolated n-type regions remain intact after the grinding process.
- The isolation is achieved through the moats filled with SiO₂, which electrically isolates the n-type regions from each other.

**3. Labels, Annotations, and Key Features:**
- The label "Grind off starting wafer" indicates the process being depicted.
- The n-type regions are clearly marked, showing that they are the active material left after the grinding process.
- The presence of SiO₂ as an isolation material is noted, highlighting its role in the dielectric isolation process.
image_name:(d)
description:The image labeled "(d)" is part of a series illustrating the fabrication steps in dielectric isolation for semiconductor devices. This particular stage shows the final configuration after completing the standard process sequence on a wafer.

1. **Identification of Components and Structure:**
- The diagram displays a cross-section of a semiconductor wafer that has undergone several processing steps. The main components visible are the n-type regions, polycrystalline silicon, and oxide isolation.
- There are three key regions labeled as "Emitter," "Base," and "Collector," which are typical components of a bipolar junction transistor (BJT).
- The n-type regions are isolated from each other by oxide layers, which provide dielectric isolation.

2. **Connections and Interactions:**
- The diagram suggests that the emitter, base, and collector are formed in isolated n-type regions, each surrounded by oxide to prevent electrical interaction between adjacent devices.
- This configuration allows for individual operation of each device, as the oxide isolation prevents unwanted electrical connections.

3. **Labels, Annotations, and Key Features:**
- The labels "Emitter," "Base," and "Collector" indicate the typical structure of a BJT, where the emitter injects carriers, the base controls the flow, and the collector gathers the carriers.
- "SiO2" is marked on the oxide layers, indicating silicon dioxide used for isolation.
- "Polycrystalline silicon" is noted at the bottom, providing mechanical support to the structure.
- The "Oxide isolation" label highlights the role of the oxide in electrically isolating different device regions on the wafer.

Overall, this stage of the process illustrates the formation of isolated transistor structures on a semiconductor wafer, ready for integration into electronic circuits.

Figure 2.47 Fabrication steps in dielectric isolation. (a) Moat etch on bottom of starting wafer. (b) Deposit polycrystalline silicon support layer. (c) Grind off starting wafer and polish. (d) Carry out standard process, starting with base mask.

### 2.7.2 Compatible Processing for High-Performance Active Devices

Many specialized circuit applications require a particular type of active device other than the $n p n$ and $p n p$ transistors that result from the standard process schedule. These include high-beta (superbeta) npn transistors for low-input-current amplifiers, MOSFETs for analog switching and low-input-current amplifiers, and high-speed pnp transistors for fast analog circuits. The fabrication of these devices generally requires the addition of one or more mask steps to the basic fabrication process. We now describe these special structures.

Superbeta Transistors. One approach to decreasing the input bias current in amplifiers is to increase the current gain of the input stage transistors. ${ }^{18}$ Since a decrease in the base width
of a transistor improves both the base transport factor and the emitter efficiency (see Section 1.3.1), the current gain increases as the base width is made smaller. Thus the current gain of the devices in the circuit can be increased by simply increasing the emitter diffusion time and narrowing the base width in the resulting devices. However, any increase in the current gain also causes a reduction in the breakdown voltage $B V_{C E O}$ of the transistors. Section 1.3.4 shows that

$$
\begin{equation*}
B V_{C E O}=\frac{B V_{C B O}}{\sqrt[n]{\beta}} \tag{2.26}
\end{equation*}
$$

where $B V_{C B O}$ is the plane breakdown voltage of the collector-base junction. Thus for a given epitaxial layer resistivity and corresponding collector-base breakdown voltage, an increase in beta gives a decrease in $B V_{C E O}$. As a result, using such a process modification to increase the beta of all the transistors in an operational amplifier is not possible because the modified transistors could not withstand the required operating voltage.

The problem of the trade-off between current gain and breakdown voltage can be avoided by fabricating two different types of devices on the same die. The standard device is similar to conventional transistors in structure. By inserting a second diffusion, however, high-beta devices also can be formed. A structure typical of such devices is shown in Fig. 2.48. These devices may be made by utilizing the same base diffusion for both devices and using separate emitter diffusions, or by using two different base diffusions and the same emitter diffusion. Both techniques are used. If the superbeta devices are used only as the input transistors in an operational amplifier, they are not required to have a breakdown voltage of more than about 1 V . Therefore, they can be diffused to extremely narrow base widths, giving current gain on the order of 2000 to 5000 . At these base widths, the actual breakdown mechanism is often no longer collector multiplication at all but is due to the depletion layer of the collector-base junction depleting the whole base region and reaching the emitter-base depletion layer. This breakdown mechanism is called punchthrough. An application of these devices in op-amp design is described in Section 6.9.2.

MOS Transistors. MOS transistors are useful in bipolar integrated-circuit design because they provide high-performance analog switches and low-input-current amplifiers, and particularly because complex digital logic can be realized in a small area using MOS technology. The latter consideration is important since the partitioning of subsystems into analog and digital chips becomes more and more cumbersome as the complexity of the individual chips becomes greater.
image_name:Figure 2.48 Superbeta device structure.
description:The image labeled "Figure 2.48 Superbeta device structure" presents a comparative diagram of two types of transistors: a Super-β transistor and a standard transistor. Both are depicted within a cross-sectional view, highlighting their structural differences and similarities.

1. **Identification of Components and Structure:**
- **Super-β Transistor (Left Side):**
- **Base Width (W_B):** Approximately 0.1 µm to 0.2 µm.
- **Layers:** Includes an emitter (E), base (B), and collector (C) regions.
- **Substrate:** A p-type substrate underlies the device, with n and n+ regions forming the main structure.
- **Doping:** The n+ region is heavily doped, providing enhanced conductivity.
- **Performance Metric:** The transistor has a high beta (β) value ranging from 2000 to 5000, indicating high current gain.

- **Standard Transistor (Right Side):**
- **Base Width (W_B):** Approximately 0.5 µm to 1 µm.
- **Layers:** Similar to the Super-β transistor, it includes emitter (E), base (B), and collector (C) regions.
- **Substrate:** Also built on a p-type substrate with n and n+ regions.
- **Performance Metric:** The beta (β) value ranges from 200 to 500, indicating lower current gain compared to the Super-β transistor.

2. **Connections and Interactions:**
- Both transistors show typical bipolar junction transistor structure with connections for the emitter, base, and collector.
- The reduced base width in the Super-β transistor contributes to its higher current gain, as indicated by the higher beta value.
- The interaction between the n and p-type materials forms the essential junctions for transistor operation.

3. **Labels, Annotations, and Key Features:**
- **Base Width (W_B):** Clearly labeled for both transistors, highlighting the significant difference in dimensions.
- **Beta (β) Values:** Annotated to show the difference in current gain capabilities between the two transistors.
- **Material Types:** Indicated as n, n+, and p, specifying the doping levels and types of semiconductor materials used.
- **Structural Representation:** The diagram uses shading and labeling to distinguish between different regions and doping levels, providing a clear visual distinction between the two types of transistors.

Figure 2.48 Superbeta device structure.
image_name:Figure 2.48 Superbeta device structure
description:The image titled "Figure 2.48 Superbeta device structure" presents a cross-sectional view of a semiconductor device that integrates an **npn transistor** and a **p-channel MOS transistor** on a shared **p-type substrate**.

Identification of Components and Structure:
- **npn Transistor:**
- **Emitter (E):** The emitter region is depicted on the left side, made of heavily doped n-type material (n+).
- **Base (B):** Situated adjacent to the emitter, the base is a lightly doped p-type region.
- **Collector (C):** The collector is shown as a wider n-type region extending downward into the substrate.
- **Aluminum (Al) Contacts:** These are shown above the emitter, base, and collector regions, providing electrical connections.

- **p-channel MOS Transistor:**
- **Source and Drain:** These are formed in the n-type epitaxial layer, with the source on the left and the drain on the right.
- **Gate:** Positioned between the source and drain, above a **thin oxide layer**.
- **Thin Oxide Layer:** This separates the gate from the underlying p-type substrate, critical for MOS operation.
- **Aluminum (Al) Contacts:** Similar to the npn transistor, these contacts are shown above the source, gate, and drain.

Connections and Interactions:
- The **SiO2 layer** acts as an insulating layer, separating the aluminum contacts from the underlying semiconductor materials.
- The npn transistor and p-channel MOS transistor are integrated into a single structure, sharing the p-type substrate, which serves as the common base for both devices.
- There is a clear delineation between the **n-type** regions (used for the npn transistor and the channel of the MOS transistor) and the **p-type substrate**, which supports the structural integration of these components.

Labels, Annotations, and Key Features:
- The diagram uses shading to differentiate between n, n+, and p regions, indicating different doping levels and types of semiconductor materials.
- Labels such as "Emitter," "Base," "Collector," "Source," "Gate," and "Drain" are used to identify the key functional areas of the transistors.
- The **thin oxide** label highlights the insulating layer critical for MOS transistor operation, emphasizing its role in isolating the gate from the underlying channel.
image_name:Figure 2.49 Compatible p-channel MOS transistor
description:The image illustrates the cross-sectional structure of a compatible p-channel MOS transistor integrated within a high-voltage bipolar analog IC process. It shows both an npn transistor and a p-channel MOS transistor side by side on a shared p-type substrate.

1. **Identification of Components and Structure:**
- The left side of the diagram depicts an **npn transistor**, with labeled regions for the **Emitter (E)**, **Base (B)**, and **Collector (C)**. These regions are formed in the n-type material, with a deeper n+ region under the base.
- The right side features the **p-channel MOS transistor**, consisting of a **Source**, **Gate**, and **Drain**. These are formed in the n-type epitaxial layer above the p-type substrate.
- The entire structure is built on a **p-type substrate**, with **SiO2** (silicon dioxide) used as an insulating layer on the surface.
- **Aluminum (Al)** is used for the metal contacts, as indicated by the shading and labeling.

2. **Connections and Interactions:**
- The npn transistor shows typical bipolar junction transistor (BJT) connections, with the emitter, base, and collector regions connected through the n-type material.
- In the MOS transistor, the **Gate** is isolated by a **thin oxide layer**, allowing for capacitive control of the channel between the source and drain.
- The n-type epitaxial layer serves as the channel for the MOS transistor, controlled by the gate voltage to allow or block current flow between the source and drain.

3. **Labels, Annotations, and Key Features:**
- The diagram clearly labels each region of the transistors, including the emitter (E), base (B), collector (C), source, gate, and drain.
- The different materials and doping levels are indicated by shading and labels such as n, n+, and p.
- The p-type substrate is marked, showing the foundational layer upon which the devices are built.
- The use of **thin oxide** for the MOS transistor's gate insulation is highlighted, emphasizing its role in the device's operation.

Figure 2.49 Compatible $p$-channel MOS transistor.
Metal-gate $p$-channel MOS transistors can be formed in a standard high-voltage bipolar analog IC process with one extra mask step. ${ }^{19}$ If a capacitor mask is included in the original sequence, then no extra mask steps are required. As illustrated in Fig. 2.49, the source and drain are formed in the epi material using the base diffusion. The capacitor mask is used to define the oxide region over the channel and the aluminum metallization forms the metal gate.

A major development in IC processing in recent years has been the combination on the same chip of high-performance bipolar devices with CMOS devices in a BiCMOS process. This topic is considered in Section 2.11.

Double-Diffused pnp Transistors. The limited frequency response of the lateral pnp transistor places a limitation on the high-frequency performance attainable with certain types of analog circuits. While this problem can be circumvented by clever circuit design in many cases, the resulting circuit is often quite complex and costly. An alternative approach is to use a more complex process that produces a high-speed, double-diffused pnp transistor with properties comparable to those of the npn transistor. ${ }^{20}$ The process usually utilizes three additional mask steps and diffusions: one to form a lightly doped $p$-type region, which will be the collector of the $p n p$; one $n$-type diffusion to form the base of the $p n p$; and one $p$-type diffusion to form the emitter of the pnp. A typical resulting structure is shown in Fig. 2.50. This process requires
image_name:Figure 2.50 Compatible double-diffused pnp process
description:The image illustrates a cross-sectional view of a compatible double-diffused PNP transistor process. It shows the layered structure and diffusion regions that form the essential components of the PNP transistor.

1. **Identification of Components and Structure:**
- The image depicts a PNP transistor integrated into a semiconductor substrate.
- The substrate is a p-type material, which forms the foundation of the structure.
- A series of epitaxial layers are grown on top of the substrate, with the first and second epitaxial growths being n-type.
- The PNP transistor is formed with a p-type well, which acts as the collector region.
- The base region of the PNP is an n-type diffusion, and the emitter is a p+ diffusion.
- An n+ collector sink is shown for an adjacent NPN transistor, indicating the compatibility of the process for integrating both PNP and NPN transistors.

2. **Connections and Interactions:**
- The diagram shows the diffusion and implantation steps required to form the transistor regions.
- Emitter and base regions are diffused into the epitaxial layers, with specific predeposition steps for phosphorus (n-type) and boron (p-type).
- The diagram indicates the flow of current and connectivity between the collector, base, and emitter regions.

3. **Labels, Annotations, and Key Features:**
- Various annotations describe the process steps, such as predepositions with boron for p-type and phosphorus for n-type regions.
- Labels like 'Base n− region for PNP', 'Emitter p+ diffusion for PNP', and 'p well for PNP' clarify the roles of different regions.
- The image also notes the sequence of processing steps, such as the first isolation diffusion and subsequent epitaxial growths.
- The NPN transistor regions are also labeled, demonstrating the dual compatibility of the process.

Figure 2.50 Compatible double-diffused pnp process.
image_name:Figure 2.51 Typical thin-film resistor structure
description:The image labeled "Figure 2.51 Typical thin-film resistor structure" illustrates the structural layout and components of a thin-film resistor, specifically a tantalum resistor. The diagram includes both a plan view and a sectional view to provide a comprehensive understanding of the resistor's construction.

### Components and Structure:
1. **Tantalum Resistor:** The main component is the tantalum thin-film layer, which acts as the resistive element.
2. **Deposited Oxide Passivation Layer:** This layer is situated above the tantalum film, providing protection and stability to the underlying components.
3. **Aluminum Contacts:** These are positioned at either end of the tantalum resistor, facilitating electrical connections.
4. **Silicon Substrate:** The base layer on which all other components are built, providing mechanical support.
5. **SiO2 Layer:** A silicon dioxide layer is present, likely serving as an insulating layer between the silicon substrate and the tantalum film.

Connections and Interactions:
- The aluminum contacts are connected to the tantalum thin-film layer, allowing current to flow through the resistor. The positioning of these contacts suggests a straightforward path for electrical signals, with the tantalum layer acting as the primary resistive path.

Labels, Annotations, and Key Features:
- The diagram is clearly labeled with annotations such as "Deposited oxide passivation layer," "Aluminum contact," "Tantalum thin-film layer," "Silicon substrate," and "SiO2," which help in identifying the various components and understanding their roles within the structure.
- The plan view provides a top-down perspective, highlighting the layout of the tantalum resistor and its connections, while the sectional view offers a cross-sectional look at the layers and their stacking order, emphasizing the vertical arrangement of materials.

Overall, this diagram serves as a detailed representation of a typical thin-film resistor, showcasing its essential components and their interactions within the device structure.

Figure 2.51 Typical thin-film resistor structure.

|  | Nichrome | Tantalum | Cermet <br> $(\mathrm{Cr}-\mathrm{SiO})$ |
| :--- | :--- | :--- | :--- |
| Range of sheet resistance $(\Omega / \square)$ <br> Temperature coefficient $\left(\mathrm{ppm} /{ }^{\circ} \mathrm{C}\right)$ | 10 to 1000 <br> $\pm 10$ to $\pm 150$ | 10 to 1000 <br> $\pm 5$ to $\pm 200$ | 30 to 2500 <br> $\pm 50$ to $\pm 150$ |

Figure 2.52 Properties of monolithic thin-film resistors.
ten masking steps and two epitaxial growth steps. Oxide isolation and poly-emitter technology have been incorporated into more advanced versions of this process.

### 2.7.3 High-Performance Passive Components

Diffused resistors have three drawbacks: They have high temperature coefficients, they have poor tolerance, and they are junction-isolated. The latter means that a parasitic capacitance is associated with each resistor, and exposure to radiation causes photocurrents to flow across the isolating junction. These drawbacks can be overcome by the use of thin-film resistors deposited on the top surface of the die over an insulating layer of oxide. After the resistor material itself is deposited, the individual resistors are defined in a conventional way using a masking step. They are then interconnected with the rest of the circuit using the standard aluminum interconnect process. The most common materials for the resistors are nichrome and tantalum, and a typical structure is shown in Fig. 2.51. The properties of the resulting resistors using these materials are summarized in Fig. 2.52.

## 2.8 MOS Integrated-Circuit Fabrication

Fabrication technologies for MOS integrated circuits span a considerably wider spectrum of complexity and performance than those for bipolar technology. CMOS technologies provide two basic types of transistors: enhancement-mode $n$-channel transistors (which have positive thresholds) and enhancement-mode $p$-channel transistors (which have negative thresholds). The magnitudes of the threshold voltages of these transistors are typically set to be 0.6 V to 0.8 V so that the drain current resulting from subthreshold conduction with zero gate-source voltage is very small. This property gives standard CMOS digital circuits high noise margins and essentially zero static power dissipation. However, such thresholds do not always minimize the total power dissipation because significant dynamic power is dissipated by
charging and discharging internal nodes during logical transitions, especially for high clock rates and power-supply voltages. ${ }^{21}$ To reduce the minimum required supply voltage and the total power dissipation for some applications, low-threshold, enhancement-mode devices or depletion-mode devices are sometimes used instead of or along with the standard-threshold, enhancement-mode devices. For the sake of illustration, we will consider an example process that contains enhancement-mode $n$ - and $p$-channel devices along with a depletion-mode n-channel device.

CMOS technologies can utilize either a $p$-type or $n$-type substrate, with the complementary device type formed in an implanted well of the opposite impurity type. We will take as an example a process in which the starting material is p-type. The starting material is a silicon wafer with a concentration in the range of $10^{14}$ to $10^{15}$ atoms $/ \mathrm{cm}^{3}$. In CMOS technology, the first step is the formation of a well of opposite impurity-type material where the complementary device will be formed. In this case, the well is $n$-type and is formed by a masking operation and ion implantation of a donor species, typically phosphorus. Subsequent diffusion results in the structure shown in Fig. 2.53. The surface concentration in the well following diffusion is typically between $10^{15}$ and $10^{16}$ atoms $/ \mathrm{cm}^{3}$.

Next, a layer of silicon nitride is deposited and defined with a masking operation so that nitride is left only in the areas that are to become active devices. After this masking operation, additional ion implantations are carried out, which increase the surface concentrations in the areas that are not covered by nitride, called the field regions. This often involves an extra masking operation so that the surface concentration in the well and that in the substrate areas can be independently controlled by means of separate implants. This increase in surface concentration in the field is necessary because the field regions themselves are MOS transistors with very thick gate oxide. To properly isolate the active devices from one another, the field devices must have a threshold voltage high enough that they never turn on. This can be accomplished by increasing the surface concentration in the field regions. Following the field implants, a local oxidation is performed, which results in the structure shown in Fig. 2.54.
image_name:Figure 2.53
description:The image titled "Figure 2.53" is a cross-sectional diagram illustrating the structure of a semiconductor wafer following the implantation and diffusion processes for creating an n-type well. The diagram includes several key components:

1. **p-type Substrate:** The base layer of the structure is a p-type substrate, represented with a dotted pattern. This substrate serves as the foundation for the semiconductor device.

2. **n-type Well:** Embedded within the p-type substrate is an n-type well, depicted as a shaded region. This well is created through the implantation and diffusion of n-type dopants into the substrate, allowing the formation of p-type transistors in this region.

3. **SiO2 Layer:** A thin layer of silicon dioxide (SiO2) is shown on top of the structure. This layer acts as an insulator and is crucial for isolating the components and protecting the substrate.

The diagram is labeled with annotations indicating the different regions, such as "SiO2 (thin)", "p-type substrate", and "n-type well". These labels help in identifying and understanding the materials and their roles in the structure. The image represents a stage in the semiconductor fabrication process where the foundation for both n-channel and p-channel devices is being established, with the n-channel devices forming in the unimplanted p-type portions and the p-channel devices forming within the n-type well region.

Figure 2.53 Cross section of sample following implantation and diffusion of the $n$-type well. Subsequent processing will result in formation of an $n$-channel device in the unimplanted $p$-type portions of the substrate and a $p$-type transistor in the $n$-type well region.
image_name:Figure 2.54
description:The image, labeled as Figure 2.54, depicts a cross-sectional view of a semiconductor device following field implant steps and field oxidation.

1. **Identification of Components and Structure:**
- The diagram shows a p-type substrate as the foundational layer, indicated by a dotted pattern.
- On top of the substrate, there is a thick SiO2 layer, which acts as an insulating layer and is shown as a solid, thick line.
- An implanted p-layer is visible in the substrate, identified by a denser dotted region, pointing to areas where p-type dopants have been introduced.
- Similarly, an implanted n-layer is present, represented by a shaded region, indicating n-type doping.

2. **Connections and Interactions:**
- The thick SiO2 layer covers the surface, providing isolation between different regions. The implanted p-layer and n-layer are embedded within the substrate, suggesting the formation of p-n junctions essential for transistor operation.
- These implanted regions are separated by the SiO2 layer, which helps in defining the active areas of the device and preventing unwanted electrical interactions.

3. **Labels, Annotations, and Key Features:**
- The diagram includes labels such as "Thick SiO2," "Implanted p-layer," and "Implanted n-layer," which help identify the various regions and materials involved.
- The p-type substrate is clearly marked, providing context for the doping and implantation processes described.
- The SiO2 layer is also labeled, indicating its role as an insulator and field oxide, crucial for device isolation and performance.

Overall, the image illustrates the structural setup following critical processing steps in semiconductor fabrication, highlighting the formation and isolation of doped regions necessary for device functionality.

Figure 2.54 Cross section of the sample following field implant steps and field oxidation.
image_name:Figure 2.54 Cross section of the sample following field implant steps and field oxidation.
description:The image, labeled as "Figure 2.54 Cross section of the sample following field implant steps and field oxidation," presents a detailed cross-sectional view of a semiconductor structure post-field implant and oxidation processes.

1. **Identification of Components and Structure:**
- The main components visible in the cross-section include a **p-type substrate** which forms the base layer of the semiconductor device.
- Above the substrate, there is a layer of **SiO2** (silicon dioxide) that acts as an insulator and is crucial for device isolation. This layer is identified as a field oxide.
- An **n-type implanted layer** is present, which is specifically used for depletion devices. This layer is positioned on top of the substrate.
- **Polysilicon regions** are shown, indicating areas where polysilicon material has been deposited. These regions are essential for forming gates in MOS transistors.
- **Buried contacts** are depicted, which facilitate electrical connections within the device architecture.

2. **Connections and Interactions:**
- The image shows how the polysilicon regions are positioned above the n-type implanted layers and are likely used to form gates that control the flow of current in the device.
- The buried contacts suggest pathways for electrical signals to travel, connecting different parts of the semiconductor device.
- The SiO2 layer ensures that the different regions are electrically isolated from each other, preventing unwanted current leakage and ensuring proper device functionality.

3. **Labels, Annotations, and Key Features:**
- The image is annotated with labels such as "n-type implanted layer for depletion device," "Buried contact," "Polysilicon," and "SiO2," providing clarity on the function and composition of each part of the structure.
- The illustration highlights the importance of the SiO2 as a field oxide, emphasizing its role in device isolation and performance.

Overall, this cross-sectional diagram effectively illustrates the complex layering and processing involved in semiconductor fabrication, focusing on the formation of doped regions and their isolation through field oxidation.

Figure 2.55 Cross section of the sample following deposition and definition of the polysilicon gate layer. Ion implantations have been performed in the thin-oxide regions to adjust the thresholds of the devices.

After field-oxide growth, the nitride is removed from the active areas, and implantation steps are carried out, which adjust the surface concentrations in what will become the channel of the MOS transistors. Equation 1.139 , applied to the doping levels usually found in the active-device areas, gives an $n$-channel threshold of within a few hundred millivolts of zero, and $p$-channel threshold of about -2 V . To shift the magnitudes of the device threshold voltages to 0.6 V to 0.8 V , an implantation step that changes the impurity concentration at the surface in the channel regions of the two transistor types is usually included. This shift in threshold can sometimes be accomplished by using a single sheet implant over the entire wafer, which simultaneously shifts the thresholds of both types of devices. More typically, however, two separate masked implants are used, one for each device type. Also, if a depletion-mode $n$-channel device is included in the process, it is defined at this point by a masking operation and subsequent implant to shift the threshold of the selected devices to a negative value so that they are normally on.

Next, a layer of polysilicon is deposited, and the gates of the various devices are defined with a masking operation. The resulting structure is shown in Fig. 2.55. Silicon-gate MOS technology provides three materials that can be used for interconnection: polysilicon, diffusion, and several layers of metal. Unless special provision is made in the process, connections between polysilicon and diffusion layers require a metallization bridge, since the polysilicon layer acts as a mask for the diffused layers. To provide a direct electrical connection between polysilicon and diffusion layers, a buried contact can be included just prior to the polysilicon deposition. This masking operation opens a window in the silicon dioxide under the polysilicon, allowing it to touch the bare silicon surface when it is deposited, forming a direct polysiliconsilicon contact. The depletion device shown in Fig. 2.55 has such a buried contact connecting its source to its gate.

Next, a masking operation is performed such that photoresist covers the $p$-channel devices, and the wafer is etched to remove the oxide from the source and drain areas of the $n$-channel devices. Arsenic or phosphorus is then introduced into these areas, using either diffusion or ion implantation. After a short oxidation, the process is repeated for the $p$-channel source and drain areas, where boron is used. The resulting structure is shown in Fig. 2.56.

At this point in the process, a layer of silicon dioxide is usually deposited on the wafer, using chemical vapor deposition or some other similar technique. This layer is required to reduce the parasitic capacitance of the interconnect metallization and cannot be thermally grown because of the redistribution of the impurities within the device structures that would result during the growth. Following the oxide deposition, the contact windows are formed with a masking operation, and metallization is deposited and defined with a second masking operation. The final structure is shown in Fig. 2.57. A microscope photograph of such a device is shown in Fig. 2.58. Subsequent fabrication steps are as described in Section 2.3 for bipolar technology.
image_name:Figure 2.56 Cross section of the sample following the source drain masking and diffusion operations.
description:The image titled "Figure 2.56 Cross section of the sample following the source drain masking and diffusion operations" depicts a cross-sectional view of a semiconductor device structure. The diagram illustrates several key components and layers involved in the fabrication process:

1. **p-type Substrate**: The base layer in the diagram is a p-type substrate, which serves as the foundational material for the device structure.

2. **n-type Well**: An n-type well is embedded within the p-type substrate. This well is created through doping processes to form a region with excess electrons.

3. **SiO₂ Layer**: A silicon dioxide (SiO₂) layer is shown on the surface of the substrate. This layer acts as an insulating barrier and is crucial for defining the regions of the device.

4. **n⁺ and p⁺ Implants or Diffusions**: The diagram indicates regions with n⁺ and p⁺ implants or diffusions. These areas are heavily doped to create source and drain regions with enhanced conductivity. The n⁺ regions are typically associated with n-channel devices, while the p⁺ regions correspond to p-channel devices.

5. **Masking and Diffusion Operations**: The image suggests that the structure has undergone masking and diffusion operations to precisely define the doped regions. These processes are essential for forming the electrical characteristics of the device.

6. **Arrows Indicating Process Flow**: Arrows are used to indicate the direction of implant or diffusion processes, showing how dopants are introduced into the substrate.

The diagram provides a detailed view of the structural and process elements involved in the formation of semiconductor devices, focusing on the source and drain regions after masking and diffusion operations.

Figure 2.56 Cross section of the sample following the source drain masking and diffusion operations.
image_name:Cross section of the sample following the source drain masking and diffusion operations
description:The image depicts a cross-sectional view of a semiconductor substrate following source and drain masking and diffusion operations. The substrate is identified as a p-type material, which serves as the foundational layer for the transistors.

1. **Identification of Components and Structure:**
- The diagram shows three types of transistors: depletion-mode n-channel, enhancement-mode n-channel, and enhancement-mode p-channel transistors.
- A metallization layer is present on the surface, providing electrical connections to the transistors.
- Each transistor is formed within the p-type substrate, with the n-channel transistors having n-type regions and the p-channel transistor having a p-type region.
- The transistors are separated by SiO2 (silicon dioxide) insulation, which isolates the devices from each other.

2. **Connections and Interactions:**
- The metallization provides pathways for electrical signals to reach the transistors, indicating connections for source, drain, and gate terminals.
- The depletion-mode n-channel transistor includes an implanted channel to adjust its threshold voltage, allowing it to conduct without a gate voltage.
- The enhancement-mode transistors require a gate voltage to create a conductive channel between the source and drain.

3. **Labels, Annotations, and Key Features:**
- The image is annotated to distinguish between the different types of transistors.
- The p-type substrate and SiO2 insulation are labeled, clarifying the structure and material composition.
- Arrows indicating the metallization connections highlight the flow of electrical signals across the device.

Figure 2.57 Cross section of the sample after final process step. The enhancement and depletion $n$-channel devices are distinguished from each other by the fact that the depletion device has received a channel implantation of donor impurities to lower its threshold voltage, usually to the range of -1.5 V to -3 V .
image_name:Figure 2.58
description:The image labeled as "Figure 2.58" is a photomicrograph of a silicon-gate MOS transistor. The photograph showcases several key components of the transistor:

1. **Polysilicon Gate**: This is a crucial part of the MOS transistor, serving as the gate through which voltage is applied to control the flow of current between the source and drain.

2. **Source Metallization and Contact Windows**: The source region is identified with metallization, which is the conductive layer that allows for electrical connectivity. The source contact windows are visible as two smaller rectangular openings, which facilitate electrical contact to the source region.

3. **Drain Metallization and Contact Windows**: Similar to the source, the drain region is also metallized for electrical connectivity. The drain contact windows are also divided into two smaller rectangular openings, aligning with the design choice to use multiple smaller openings instead of a single large one.

4. **Edge of Field Oxide Region**: This marks the boundary of the field oxide, a thick oxide layer used to isolate different components of the transistor and prevent electrical interference.

The layout and design of the contact windows are particularly noteworthy, as they deviate from a single long opening to an array of smaller openings, which is a common practice to enhance reliability and manufacturability in integrated circuits. The image provides a detailed view of the structural and functional elements of the MOS transistor, emphasizing the metallization and contact regions necessary for its operation.

Figure 2.58 Photomicrograph of a silicon-gate MOS transistor. Visible in this picture are the polysilicon gate, field-oxide region boundary, source and drain metallization, and contact windows. In this particular device, the contact windows have been broken into two smaller rectangular openings rather than a single long one as shown in Fig. 2.59. Large contact windows are frequently implemented with an array of small openings so that all individual contact holes in the integrated circuit have the same nominal geometry. This results in better uniformity of the etch rate of the contact windows and better matching.

## 2.9 Active Devices in MOS Integrated Circuits

The process sequence described in the previous section results in a variety of device types having different threshold voltages, channel mobilities, and parasitic capacitances. In addition, the sequence allows the fabrication of a bipolar emitter follower, using the well as a base. In this section, we explore the properties of these different types of devices.

### 2.9.1 n-Channel Transistors

A typical layout of an $n$-channel MOS transistor is shown in Fig. 2.59. The electrically active portion of the device is the region under the gate; the remainder of the device area simply provides electrical contact to the terminals. As in the case of integrated bipolar transistors, these areas contribute additional parasitic capacitance and resistance.

In the case of MOS technology, the circuit designer has even greater flexibility than in the bipolar case to tailor the properties of each device to the role it is to play in the individual circuit application. Both the channel width (analogous to the emitter area in bipolar) and the channel length can be defined by the designer. The latter is analogous to the base width of a bipolar device, which is not under the control of the bipolar circuit designer since it is a process parameter and not a mask parameter. In contrast to a bipolar transistor, the transconductance
image_name:Figure 2.59 Example layout of an n-channel silicon-gate MOS transistor
description:The image illustrates the layout and cross-sectional view of an n-channel silicon-gate MOS transistor. The layout is designed with various mask layers coded for different materials and components. The key components identified in the layout include:

1. **Gate (G):** Represented by a polysilicon layer. The gate is centrally located and controls the channel between the source and drain.

2. **Source (S) and Drain (D):** These are the terminals on either side of the gate, indicated by contact openings. The source and drain regions are where the current enters and exits the transistor.

3. **Substrate:** The p-type substrate is shown in the cross-sectional view, providing the base for the n-channel.

4. **Insulating Layer:** Silicon dioxide (SiO2) acts as the insulating layer between the gate and the substrate.

5. **Metal Connections:** Metal lines are used to make electrical connections to the gate, source, and drain.

The layout shows the gate surrounded by nitride and polysilicon layers, with contact openings for metal connections. The vertical scale is marked in micrometers, indicating the dimensions of the device.

The cross-sectional view at the bottom of the image provides a side view of the transistor, showing the gate oxide layer, the n-channel formed between the source and drain, and the p-type substrate beneath.

Overall, the diagram highlights the structural and material composition of the MOS transistor, illustrating how the gate, source, and drain are interconnected and insulated within the device.

Figure 2.59 Example layout of an $n$-channel silicon-gate MOS transistor. The mask layers are coded as shown.
of an MOS device can be made to vary over a wide range at a fixed drain current by simply changing the device geometry. The same is true of the gate-source voltage. In making these design choices, the designer must be able to relate changes in device geometry to changes in the electrical properties of the device. To illustrate this procedure, we will calculate the model parameters of the device shown in Fig. 2.59. This device has a drawn channel length of $6 \mu \mathrm{~m}$ and channel width of $50 \mu \mathrm{~m}$. We will assume the process has the parameters that are summarized in Table 2.1. This is typical of processes with minimum allowed gate lengths of $3 \mu \mathrm{~m}$. Parameters for more advanced processes are given in Tables 2.2, 2.3, 2.4, 2.5, and 2.6.

Table 2.1 Summary of Process Parameters for a Typical Silicon-Gate $n$-Well CMOS Process with $3 \mu \mathrm{~m}$ Minimum Allowed Gate Length

| Parameter | Symbol | Value <br> $n$-Channel <br> Transistor | Value $p$-Channel <br> Transistor | Units |
| :---: | :---: | :---: | :---: | :---: |
| Substrate doping | $N_{A}, N_{D}$ | $1 \times 10^{15}$ | $1 \times 10^{16}$ | Atoms/cm ${ }^{3}$ |
| Gate oxide thickness | $t_{o x}$ | 400 | 400 | Å |
| Metal-silicon work function | $\phi_{m s}$ | -0.6 | -0.1 | V |
| Channel mobility | $\mu_{n}, \mu_{p}$ | 700 | 350 | $\mathrm{cm}^{2} / \mathrm{V}$-s |
| Minimum drawn channel length | $L_{\text {drwn }}$ | 3 | 3 | $\mu \mathrm{m}$ |
| Source, drain junction depth | $X_{j}$ | 0.6 | 0.6 | $\mu \mathrm{m}$ |
| Source, drain side diffusion | $L_{d}$ | 0.3 | 0.3 | $\mu \mathrm{m}$ |
| Overlap capacitance per unit gate width | $C_{\text {ol }}$ | 0.35 | 0.35 | $\mathrm{fF} / \mu \mathrm{m}$ |
| Threshold adjust implant (box dist) |  |  |  |  |
| impurity type |  | P | P |  |
| effective depth | $X_{i}$ | 0.3 | 0.3 | $\mu \mathrm{m}$ |
| effective surface concentration | $N_{s i}$ | $2 \times 10^{16}$ | $0.9 \times 10^{16}$ | Atoms/cm ${ }^{3}$ |
| Nominal threshold voltage | $V_{t}$ | 0.7 | -0.7 | V |
| Polysilicon gate doping concentration | $N_{\text {dpoly }}$ | $10^{20}$ | $10^{20}$ | Atoms/cm ${ }^{3}$ |
| Poly gate sheet resistance | $R_{s}$ | 20 | 20 | / $/ \square$ |
| Source, drain-bulk junction capacitances (zero bias) | $C_{j 0}$ | 0.08 | 0.20 | $\mathrm{fF} / \mu \mathrm{m}^{2}$ |
| Source, drain-bulk junction capacitance grading coefficient | n | 0.5 | 0.5 |  |
| Source, drain periphery capacitance (zero bias) | $C^{\text {jsw0}}$ | 0.5 | 1.5 | $\mathrm{fF} / \mu \mathrm{m}$ |
| Source, drain periphery capacitance grading coefficient | n | 0.5 | 0.5 |  |
| Source, drain junction built-in potential | $\psi_{0}$ | 0.65 | 0.65 | V |
| Surface-state density | $\frac{Q_{S S}}{q}$ | $10^{11}$ | $10^{11}$ | Atoms/cm ${ }^{2}$ |
| Channel-length modulation parameter | $\left\|\frac{d X_{d}}{d V_{D S}}\right\|$ | 0.2 | 0.1 | $\mu \mathrm{m} / \mathrm{V}$ |

Table 2.2 Summary of Process Parameters for a Typical Silicon-Gate $n$-Well CMOS Process with $1.5 \mu \mathrm{~m}$ Minimum Allowed Gate Length

| Parameter | Symbol | Value $n$-Channel Transistor | Value <br> p-Channel <br> Transistor | Units |
| :---: | :---: | :---: | :---: | :---: |
| Substrate doping | $N_{A}, N_{D}$ | $2 \times 10^{15}$ | $1.5 \times 10^{16}$ | Atoms/cm ${ }^{3}$ |
| Gate oxide thickness | $t_{o x}$ | 250 | 250 | Å |
| Metal-silicon work function | $\phi_{m s}$ | -0.6 | -0.1 | V |
| Channel mobility | $\mu_{n}, \mu_{p}$ | 650 | 300 | $\mathrm{cm}^{2} / \mathrm{V}$-s |
| Minimum drawn channel length | $L_{\text {drwn }}$ | 1.5 | 1.5 | $\mu \mathrm{m}$ |
| Source, drain junction depth | $X_{j}$ | 0.35 | 0.4 | $\mu \mathrm{m}$ |
| Source, drain side diffusion | $L_{d}$ | 0.2 | 0.3 | $\mu \mathrm{m}$ |
| Overlap capacitance per unit gate width | $C_{\text {ol }}$ | 0.18 | 0.26 | $\mathrm{fF} / \mu \mathrm{m}$ |
| Threshold adjust implant (box dist) |  |  |  |  |
| impurity type |  | P | P |  |
| effective depth | $X_{i}$ | 0.3 | 0.3 | $\mu \mathrm{m}$ |
| effective surface concentration | $N_{s i}$ | $2 \times 10^{16}$ | $0.9 \times 10^{16}$ | Atoms/cm ${ }^{3}$ |
| Nominal threshold voltage | $V_{t}$ | 0.7 | -0.7 | V |
| Polysilicon gate doping concentration | $N_{\text {dpoly }}$ | $10^{20}$ | $10^{20}$ | Atoms/cm ${ }^{3}$ |
| Poly gate sheet resistance | $R_{s}$ | 20 | 20 | $\Omega / \square$ |
| Source, drain-bulk junction capacitances (zero bias) | $C_{j 0}$ | 0.14 | 0.25 | $\mathrm{fF} / \mu \mathrm{m}^{2}$ |
| Source, drain-bulk junction capacitance grading coefficient | n | 0.5 | 0.5 |  |
| Source, drain periphery capacitance (zero bias) | $C^{\text {sw0 } 0}$ | 0.8 | 1.8 | $\mathrm{fF} / \mu \mathrm{m}$ |
| Source, drain periphery capacitance grading coefficient | n | 0.5 | 0.5 |  |
| Source, drain junction built-in potential | $\psi_{0}$ | 0.65 | 0.65 | V |
| Surface-state density | $\frac{Q_{S S}}{q}$ | $10^{11}$ | $10^{11}$ | Atoms/cm ${ }^{2}$ |
| Channel-length modulation parameter | $\left\|\frac{d X_{d}}{d V_{D S}}\right\|$ | 0.12 | 0.06 | $\mu \mathrm{m} / \mathrm{V}$ |

Threshold Voltage. In Chapter 1, an MOS transistor was shown to have a threshold voltage of

$$
\begin{equation*}
V_{t}=\phi_{m s}+2 \phi_{f}+\frac{Q_{b}}{C_{o x}}-\frac{Q_{s s}}{C_{o x}} \tag{2.27}
\end{equation*}
$$

where $\phi_{m s}$ is the metal-silicon work function, $\phi_{f}$ is the Fermi level in the bulk silicon, $Q_{b}$ is the bulk depletion layer charge, $C_{o x}$ is the oxide capacitance per unit area, and $Q_{s s}$ is the

Table 2.3 Summary of Process Parameters for a Typical Silicon-Gate $n$-Well CMOS Process with $0.8 \mu \mathrm{~m}$ Minimum Allowed Gate Length

| Parameter | Symbol | Value <br> n-Channel <br> Transistor | Value <br> p-Channel <br> Transistor | Units |
| :---: | :---: | :---: | :---: | :---: |
| Substrate doping | $N_{A}, N_{D}$ | $4 \times 10^{15}$ | $3 \times 10^{16}$ | Atoms/cm ${ }^{3}$ |
| Gate oxide thickness | $t_{o x}$ | 150 | 150 | Å |
| Metal-silicon work function | $\phi_{m s}$ | -0.6 | -0.1 | V |
| Channel mobility | $\mu_{n}, \mu_{p}$ | 550 | 250 | $\mathrm{cm}^{2} / \mathrm{V}$-s |
| Minimum drawn channel length | $L_{\text {drwn }}$ | 0.8 | 0.8 | $\mu \mathrm{m}$ |
| Source, drain junction depth | $X_{j}$ | 0.2 | 0.3 | $\mu \mathrm{m}$ |
| Source, drain side diffusion | $L_{d}$ | 0.12 | 0.18 | $\mu \mathrm{m}$ |
| Overlap capacitance per unit gate width | $C_{\text {ol }}$ | 0.12 | 0.18 | $\mathrm{fF} / \mu \mathrm{m}$ |
| Threshold adjust implant (box dist) |  |  |  |  |
| impurity type |  | P | P |  |
| effective depth | $X_{i}$ | 0.2 | 0.2 | $\mu \mathrm{m}$ |
| effective surface concentration | $N_{s i}$ | $3 \times 10^{16}$ | $2 \times 10^{16}$ | Atoms/cm ${ }^{3}$ |
| Nominal threshold voltage | $V_{t}$ | 0.7 | $-0.7$ | V |
| Polysilicon gate doping concentration | $N_{\text {dpoly }}$ | $10^{20}$ | $10^{20}$ | Atoms/cm ${ }^{3}$ |
| Poly gate sheet resistance | $R_{s}$ | 10 | 10 | / $/ \square$ |
| Source, drain-bulk junction capacitances (zero bias) | $C{ }$ | 0.18 | 0.30 | $\mathrm{fF} / \mu \mathrm{m}^{2}$ |
| Source, drain-bulk junction capacitance grading coefficient | n | 0.5 | 0.5 |  |
| Source, drain periphery capacitance (zero bias) | $C^{\text {sw0 } 0}$ | 1.0 | 2.2 | $\mathrm{fF} / \mu \mathrm{m}$ |
| Source, drain periphery capacitance grading coefficient | n | 0.5 | 0.5 |  |
| Source, drain junction built-in potential | $\psi_{0}$ | 0.65 | 0.65 | V |
| Surface-state density | $\frac{Q_{S S}}{q}$ | $10^{11}$ | $10^{11}$ | Atoms/cm ${ }^{2}$ |
| Channel-length modulation parameter | $\left\|\frac{d X_{d}}{d V_{D S}}\right\|$ | 0.08 | 0.04 | $\mu \mathrm{m} / \mathrm{V}$ |

concentration of surface-state charge. An actual calculation of the threshold is illustrated in the following example.

Often the threshold voltage must be deduced from measurements, and a useful approach to doing this is to plot the square root of the drain current as a function of $V_{G S}$, as shown in Fig. 2.60. The threshold voltage can be determined as the extrapolation of the straight portion

Table 2.4 Summary of Process Parameters for a Typical Silicon-Gate $n$-Well CMOS Process with $0.4 \mu \mathrm{~m}$ Minimum Allowed Gate Length

| Parameter | Symbol | Value $n$-Channel Transistor | Value <br> $p$-Channel <br> Transistor | Units |
| :---: | :---: | :---: | :---: | :---: |
| Substrate doping | $N_{A}, N_{D}$ | $5 \times 10^{15}$ | $4 \times 10^{16}$ | Atoms/cm ${ }^{3}$ |
| Gate oxide thickness | $t_{o x}$ | 80 | 80 | Å |
| Metal-silicon work function | $\phi_{m s}$ | -0.6 | -0.1 | V |
| Channel mobility | $\mu_{n}, \mu_{p}$ | 450 | 150 | $\mathrm{cm}^{2} / \mathrm{V}$-s |
| Minimum drawn channel length | $L_{\text {drwn }}$ | 0.4 | 0.4 | $\mu \mathrm{m}$ |
| Source, drain junction depth | $X_{j}$ | 0.15 | 0.18 | $\mu \mathrm{m}$ |
| Source, drain side diffusion | $L_{d}$ | 0.09 | 0.09 | $\mu \mathrm{m}$ |
| Overlap capacitance per unit gate width | $C_{\text {ol }}$ | 0.35 | 0.35 | $\mathrm{fF} / \mu \mathrm{m}$ |
| Threshold adjust implant (box dist) |  |  |  |  |
| impurity type |  | P | P |  |
| effective depth | $X_{i}$ | 0.16 | 0.16 | $\mu \mathrm{m}$ |
| effective surface concentration | $N_{s i}$ | $4 \times 10^{16}$ | $3 \times 10^{16}$ | Atoms/cm ${ }^{3}$ |
| Nominal threshold voltage | $V_{t}$ | 0.6 | $-0.8$ | V |
| Polysilicon gate doping concentration | $N_{\text {dpoly }}$ | $10^{20}$ | $10^{20}$ | Atoms/cm ${ }^{3}$ |
| Poly gate sheet resistance | $R_{s}$ | 5 | 5 | $\Omega / \square$ |
| Source, drain-bulk junction capacitances (zero bias) | $C_{j 0}$ | 0.2 | 0.4 | $\mathrm{fF} / \mu \mathrm{m}^{2}$ |
| Source, drain-bulk junction capacitance grading coefficient | n | 0.5 | 0.4 |  |
| Source, drain periphery capacitance (zero bias) | $C^{\text {sw0 } 0}$ | 1.2 | 2.4 | fF/ $/$ m |
| Source, drain periphery capacitance grading coefficient | n | 0.4 | 0.3 |  |
| Source, drain junction built-in potential | $\psi_{0}$ | 0.7 | 0.7 | V |
| Surface-state density | $\frac{Q_{S S}}{q}$ | $10^{11}$ | $10^{11}$ | Atoms/cm ${ }^{2}$ |
| Channel-length modulation parameter | $\left\|\frac{d X_{d}}{d V_{D S}}\right\|$ | 0.02 | 0.04 | $\mu \mathrm{m} / \mathrm{V}$ |

of the curve to zero current. The slope of the curve also yields a direct measure of the quantity $\mu_{n} C_{o x} W / L_{\text {eff }}$ for the device at the particular drain-source voltage at which the measurement is made. The measured curve deviates from a straight line at low currents because of subthreshold conduction and at high currents because of mobility degradation in the channel as the carriers approach scattering-limited velocity.

Table 2.5 Summary of Process Parameters for a Typical CMOS Process with $0.2 \mu \mathrm{~m}$ Minimum Allowed Gate Length

| Parameter | Symbol | Value $n$-Channel Transistor | Value p-Channel Transistor | Units |
| :---: | :---: | :---: | :---: | :---: |
| Substrate doping | $N_{A}, N_{D}$ | $8 \times 10^{16}$ | $8 \times 10^{16}$ | Atoms/cm ${ }^{3}$ |
| Gate oxide thickness | $t_{o x}$ | 42 | 42 | Angstroms |
| Metal-silicon work function | $\phi_{m s}$ | -0.6 | -0.1 | V |
| Channel mobility | $\mu_{n}, \mu_{p}$ | 300 | 80 | $\mathrm{cm}^{2} / \mathrm{V}$-s |
| Minimum drawn channel length | $L_{\text {drwn }}$ | 0.2 | 0.2 | $\mu \mathrm{m}$ |
| Source, drain junction depth | $X_{j}$ | 0.16 | 0.16 | $\mu \mathrm{m}$ |
| Source, drain side diffusion | $L_{d}$ | 0.01 | 0.015 | $\mu \mathrm{m}$ |
| Overlap capacitance per unit gate width | $C_{\text {ol }}$ | 0.36 | 0.33 | $\mathrm{fF} / \mu \mathrm{m}$ |
| Threshold adjust implant (box dist.) |  |  |  |  |
| impurity type |  | P | P |  |
| effective depth | $X_{i}$ | 0.12 | 0.12 | $\mu \mathrm{m}$ |
| effective surface concentration | $N_{s i}$ | $2 \times 10^{17}$ | $2 \times 10^{17}$ | Atoms/cm ${ }^{3}$ |
| Nominal threshold voltage | $V_{t}$ | 0.5 | $-0.45$ | V |
| Polysilicon gate doping concentration | $N_{\text {dpoly }}$ | $10^{20}$ | $10^{20}$ | Atoms/cm ${ }^{3}$ |
| Poly gate sheet resistance | $R_{S}$ | 7 | 7 | $\Omega / \square$ |
| Source, drain-bulk junction capacitances (zero bias) | $C_{j 0}$ | 1.0 | 1.1 | $\mathrm{fF} / \mu \mathrm{m}^{2}$ |
| Source, drain-bulk junction capacitance grading coefficient | n | 0.36 | 0.45 |  |
| Source, drain periphery capacitance (zero bias) | $C_{j s w 0}$ | 0.2 | 0.25 | $\mathrm{fF} / \mu \mathrm{m}$ |
| Source, drain periphery capacitance grading coefficient | n | 0.2 | 0.24 |  |
| Source, drain junction built-in potential | $\psi_{0}$ | 0.68 | 0.74 | V |
| Surface-state density | $\frac{Q_{S S}}{q}$ | $10^{11}$ | $10^{11}$ | Atoms/cm ${ }^{2}$ |
| Channel-length modulation parameter | $\left\|\frac{d X_{d}}{d V_{D S}}\right\|$ | 0.028 | 0.023 | $\mu \mathrm{m} / \mathrm{V}$ |

image_name:Figure 2.60 Typical experimental variation of drain current as a function of the square root of gate-source voltage in the active region
description:The graph in Figure 2.60 is a plot of the square root of the drain current (√I_D) versus the gate-source voltage (V_GS) for a transistor in its active region. This is a typical representation used to analyze the behavior of MOSFET devices.

Axes Labels and Units:
- **Y-Axis**: Represents the square root of the drain current (√I_D). The units of I_D are typically in amperes, but the axis is labeled with its square root, which is dimensionless.
- **X-Axis**: Represents the gate-source voltage (V_GS) and is measured in volts (V).

Overall Behavior and Trends:
- The graph starts at the origin, indicating that when V_GS is zero, the drain current is also zero.
- **Subthreshold Conduction**: At low values of V_GS, there is a region of subthreshold conduction where the drain current begins to increase exponentially with V_GS. This is depicted by a steep curve at the beginning of the graph.
- **Extrapolated Threshold**: The point where the curve begins to rise sharply is known as the extrapolated threshold, indicating the onset of significant conduction.
- **Linear Region**: As V_GS increases beyond the threshold, the graph shows a linear relationship between √I_D and V_GS, suggesting that the drain current increases quadratically with V_GS in this region.
- **High-Field Carrier Mobility Falloff**: At higher values of V_GS, the curve begins to flatten, indicating a reduction in the rate of increase of drain current due to high-field effects, such as carrier mobility degradation.

Key Features and Technical Details:
- **Subthreshold Region**: Characterized by an exponential increase in current.
- **Threshold Voltage**: The extrapolated threshold point is critical for determining the threshold voltage of the transistor.
- **Saturation Effects**: The flattening of the curve at higher V_GS values indicates saturation effects where further increases in V_GS do not significantly increase the drain current.

Annotations and Specific Data Points:
- The graph includes annotations such as "Subthreshold conduction," "Extrapolated threshold," and "High-field carrier mobility falloff," which highlight significant regions and behaviors in the graph.
- These annotations help in understanding the different operational regions of the transistor and their implications on device performance.
image_name:
description:
[
name: M1, type: NMOS, ports: {S: GND, D: VDS, G: VGS}
]
extrainfo:The diagram shows the typical experimental variation of drain current as a function of the square root of gate-source voltage in the active region. It illustrates subthreshold conduction and high-field carrier mobility falloff. The circuit includes an NMOS transistor M1 with its source connected to ground, drain connected to VDS, and gate connected to VGS.

Figure 2.60 Typical experimental variation of drain current as a function of the square root of gate-source voltage in the active region.

Table 2.6 Summary of Process Parameters for a Typical CMOS Process with $0.1 \mu \mathrm{~m}$ Minimum Allowed Gate Length

| Parameter | Symbol | Value $n$-Channel Transistor | Value p-Channel Transistor | Units |
| :---: | :---: | :---: | :---: | :---: |
| Substrate doping | $N_{A}, N_{D}$ | $1 \times 10^{17}$ | $1 \times 10^{17}$ | Atoms/cm ${ }^{3}$ |
| Gate oxide thickness | $t_{o x}$ | 25 | 25 | Angstroms |
| Gate leakage current density | $J_{G}$ | 1.2 | 0.4 | $\mathrm{nA} / \mu \mathrm{m}^{2}$ |
| Metal-silicon work function | $\phi_{m s}$ | -0.6 | -0.1 | V |
| Channel mobility | $\mu_{n}, \mu_{p}$ | 390 | 100 | $\mathrm{cm}^{2} / \mathrm{V}$-s |
| Minimum drawn channel length | $L_{\text {drwn }}$ | 0.1 | 0.1 | $\mu \mathrm{m}$ |
| Source, drain junction depth | $X_{j}$ | 0.15 | 0.16 | $\mu \mathrm{m}$ |
| Source, drain side diffusion | $L_{d}$ | 0.005 | 0.005 | $\mu \mathrm{m}$ |
| Overlap capacitance per unit gate width | $C_{\text {ol }}$ | 0.10 | 0.07 | $\mathrm{fF} / \mu \mathrm{m}$ |
| Threshold adjust implant (box dist.) impurity type |  | P | P |  |
| effective depth | $X_{i}$ | 0.1 | 0.1 | $\mu \mathrm{m}$ |
| effective surface concentration | $N_{s i}$ | $5 \times 10^{17}$ | $5 \times 10^{17}$ | Atoms/cm ${ }^{3}$ |
| Nominal threshold voltage | $V_{t}$ | 0.27 | -0.28 | V |
| Polysilicon gate doping concentration | $N_{\text {dpoly }}$ | $10^{20}$ | $10^{20}$ | Atoms/cm ${ }^{3}$ |
| Poly gate sheet resistance | $R_{s}$ | 10 | 10 | $\Omega / \square$ |
| Source, drain-bulk junction capacitances (zero bias) | $C_{j 0}$ | 1.0 | 1.1 | $\mathrm{fF} / \mu \mathrm{m}^{2}$ |
| Source, drain-bulk junction capacitance grading coefficient | n | 0.25 | 0.35 |  |
| Source, drain periphery capacitance (zero bias) | $C^{\text {jsw0}}$ | 0.05 | 0.06 | $\mathrm{fF} / \mu \mathrm{m}$ |
| Source, drain periphery capacitance grading coefficient | n | 0.05 | 0.05 |  |
| Source, drain junction built-in potential | $\psi_{0}$ | 0.6 | 0.65 | V |
| Surface-state density | $\frac{Q_{S S}}{q}$ | $10^{11}$ | $10^{11}$ | Atoms/cm ${ }^{2}$ |
| Channel-length modulation parameter | $\left\|\frac{d X_{d}}{d V_{D S}}\right\|$ | 0.06 | 0.05 | $\mu \mathrm{m} / \mathrm{V}$ |

#### EXAMPLE

Calculate the zero-bias threshold voltage of the unimplanted and implanted NMOS transistors for the process given in Table 2.1.

Each of the four components in the threshold voltage expression (2.27) must be calculated. The first term is the metal-silicon work function. For an $n$-channel transistor with an $n$-type polysilicon gate electrode, this has a value equal to the difference in the Fermi potentials in the two regions, or approximately -0.6 V .

The second term in the threshold voltage equation represents the band bending in the semiconductor that is required to strongly invert the surface. To produce a surface concentration of electrons that is approximately equal to the bulk concentration of holes, the surface potential
must be increased by approximately twice the bulk Fermi potential. The Fermi potential in the bulk is given by

$$
\begin{equation*}
\phi_{f}=\frac{k T}{q} \ln \left(\frac{N_{A}}{n_{i}}\right) \tag{2.28}
\end{equation*}
$$

For the unimplanted transistor with the substrate doping given in Table 2.1, this value is 0.27 V . Thus the second term in (2.27) takes on a value of 0.54 V . The value of this term will be the same for the implanted transistor since we are defining the threshold voltage as the voltage that causes the surface concentration of electrons to be the same as that of holes in the bulk material beneath the channel implant. Thus the potential difference between the surface and the bulk silicon beneath the channel implant region that is required to bring this condition about is still given by (2.30), independent of the details of the channel implant.

The third term in (2.27) is related to the charge in the depletion layer under the channel. We first consider the unimplanted device. Using (1.137), with a value of $N_{A}$ of $10^{15}$ atoms $/ \mathrm{cm}^{3}$,

$$
\begin{align*}
Q_{b 0} & =\sqrt{2 q N_{A} \epsilon 2 \phi_{f}}=\sqrt{2\left(1.6 \times 10^{-19}\right)\left(10^{15}\right)\left(11.6 \times 8.86 \times 10^{-14}\right)(0.54)} \\
& =1.34 \times 10^{-8} \mathrm{C}^{-} \mathrm{cm}^{2} \tag{2.29}
\end{align*}
$$

Also, the capacitance per unit area of the $400-\AA \AA$ gate oxide is

$$
\begin{equation*}
C_{o x}=\frac{\epsilon_{o x}}{t_{o x}}=\frac{3.9 \times 8.86 \times 10^{-14} \mathrm{~F} / \mathrm{cm}}{400 \times 10^{-8} \mathrm{~cm}}=8.6 \times 10^{-8} \frac{\mathrm{~F}}{\mathrm{~cm}^{2}}=0.86 \frac{\mathrm{fF}}{\mu \mathrm{~m}^{2}} \tag{2.30}
\end{equation*}
$$

The resulting magnitude of the third term is 0.16 V .
The fourth term in (2.27) is the threshold shift due to the surface-state charge. This positive charge has a value equal to the charge of one electron multiplied by the density of surface states, $10^{11}$ atoms $/ \mathrm{cm}^{2}$, from Table 2.1. The value of the surface-state charge term is then

$$
\begin{equation*}
\frac{Q_{s s}}{C_{o x}}=\frac{1.6 \times 10^{-19} \times 10^{11}}{8.6 \times 10^{-8}}=0.19 \mathrm{~V} \tag{2.31}
\end{equation*}
$$

Using these calculations, the threshold voltage for the unimplanted transistor is

$$
\begin{equation*}
V_{t}=-0.6 \mathrm{~V}+0.54 \mathrm{~V}+0.16 \mathrm{~V}-0.19 \mathrm{~V}=-0.09 \mathrm{~V} \tag{2.32}
\end{equation*}
$$

For the implanted transistor, the calculation of the threshold voltage is complicated by the fact that the depletion layer under the channel spans a region of nonuniform doping. A precise calculation of device threshold voltage would require consideration of this nonuniform profile. The threshold voltage can be approximated, however, by considering the implanted layer to be approximated by a box distribution of impurities with a depth $X_{i}$ and a specified impurity concentration $N_{i}$. If the impurity profile resulting from the threshold-adjustment implant and subsequent process steps is sufficiently deep so that the channel-substrate depletion layer lies entirely within it, then the effect of the implant is simply to raise the effective substrate doping. For the implant specified in Table 2.1, the average doping in the layer is the sum of the implant doping and the background concentration, or $2.1 \times 10^{16}$ atoms $/ \mathrm{cm}^{3}$. This increases the $Q_{b 0}$ term in the threshold voltage to 0.71 V and gives device threshold voltage of 0.47 V . The validity of the assumption regarding the boundary of the channel-substrate depletion layer can be checked by using Fig. 2.29. For a doping level of $2.1 \times 10^{16}$ atoms $/ \mathrm{cm}^{3}$, a one-sided step junction displays a depletion region width of approximately $0.2 \mu \mathrm{~m}$. Since the depth of the layer is $0.3 \mu \mathrm{~m}$ in this case, the assumption is valid.

Alternatively, if the implantation and subsequent diffusion had resulted in a layer that was very shallow, and was contained entirely within the depletion layer, the effect of the implanted layer would be simply to increase the effective value of $Q_{s s}$ by an amount equal to the effective
implant dose over and above that of the unimplanted transistor. The total active impurity dose for the implant given in Table 2.1 is the product of the depth and the impurity concentration, or $6 \times 10^{11}$ atoms $/ \mathrm{cm}^{2}$. For this case, the increase in threshold voltage would have been 1.11 V , giving a threshold voltage of 1.02 V .

Body-Effect Parameter. For an unimplanted, uniform-channel transistor, the body-effect parameter is given by (1.141).

$$
\begin{equation*}
\gamma=\frac{1}{C_{o x}} \sqrt{2 q \epsilon N_{A}} \tag{2.33}
\end{equation*}
$$

The application of this expression is illustrated in the following example.

#### EXAMPLE

Calculate the body-effect parameter for the unimplanted $n$-channel transistor in Table 2.1.
Utilizing in (2.33) the parameters given in Table 2.1, we obtain

$$
\begin{equation*}
\gamma=\frac{\sqrt{2\left(1.6 \times 10^{-19}\right)\left(11.6 \times 8.86 \times 10^{-14}\right)\left(10^{15}\right)}}{8.6 \times 10^{-8}}=0.21 \mathrm{~V}^{1 / 2} \tag{2.34}
\end{equation*}
$$

The calculation of body effect in an implanted transistor is complicated by the fact that the channel is not uniformly doped and the preceding simple expression does not apply. The threshold voltage as a function of body bias voltage can be approximated again by considering the implanted layer to be approximated by a box distribution of impurity of depth $X_{i}$ and concentration $N_{i}$. For small values of body bias where the channel-substrate depletion layer resides entirely within the implanted layer, the body effect is that corresponding to a transistor with channel doping $\left(N_{i}+N_{A}\right)$. For larger values of body bias for which the depletion layer extends into the substrate beyond the implanted distribution, the incremental body effect corresponds to a transistor with substrate doping $N_{A}$. A typical variation of threshold voltage as a function of substrate bias for this type of device is illustrated in Fig. 2.61.
image_name:Figure 2.61
description:The graph in Figure 2.61 illustrates the variation of threshold voltage \( V_t \) as a function of substrate bias \( \sqrt{2\phi_f + V_{SB}} \) for \( n \)-channel devices. This graph is specifically for devices with uniform channel doping (unimplanted transistors) and with nonuniform channel doping resulting from threshold adjustment channel implant (implanted transistors).

1. **Type of Graph and Function:**
- The graph is a plot showing threshold voltage \( V_t \) on the y-axis against substrate bias \( \sqrt{2\phi_f + V_{SB}} \) on the x-axis.

2. **Axes Labels and Units:**
- The y-axis is labeled \( V_t (V) \), representing the threshold voltage in volts.
- The x-axis is labeled \( \sqrt{2\phi_f + V_{SB}} \), which is a dimensionless parameter related to the substrate bias.
- Both axes have linear scales.

3. **Overall Behavior and Trends:**
- For the unimplanted transistor, the threshold voltage \( V_t \) starts at \( V_{t0} \) and increases linearly as the substrate bias increases.
- For the implanted transistor, the threshold voltage \( V_t \) also starts at \( V_{t0} \) but shows a steeper increase initially, which then gradually levels off as the substrate bias increases.

4. **Key Features and Technical Details:**
- The initial threshold voltage \( V_{t0} \) is the same for both the implanted and unimplanted transistors.
- The implanted transistor's curve shows a rapid increase in \( V_t \) at lower values of substrate bias, indicating a stronger body effect compared to the unimplanted transistor.
- As the substrate bias increases, the rate of increase in \( V_t \) for the implanted transistor diminishes, suggesting a saturation effect.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for both the implanted and unimplanted transistors, clearly distinguishing their respective curves.
- No specific numerical values are marked on the graph, but the general trend and behavior are evident from the curve shapes.

Figure 2.61 Typical variation of threshold voltage as a function of substrate bias for $n$-channel devices with uniform channel doping (no channel implant) and with nonuniform channel doping resulting from threshold adjustment channel implant.

Effective Channel Length. The gate dimension parallel to current flow that is actually drawn on the mask is called the drawn channel length $L_{\text {drwn }}$. This is the length referred to on circuit schematics. Because of exposure variations and other effects, the physical length of the polysilicon strip defining the gate may be somewhat larger or smaller than this value. The actual channel length of the device is the physical length of the polysilicon gate electrode minus the side or lateral diffusions of the source and the drain under the gate. This length will be termed the metallurgical channel length and is the distance between the metallurgical source and drain junctions. Assuming that the lateral diffusion of the source and drain are each equal to $L_{d}$, the metallurgical channel length is $L=\left(L_{\mathrm{drwn}}-2 L_{d}\right)$.

When the transistor is biased in the active or saturation region, a depletion region exists between the drain region and the end of the channel. In Chapter 1, the width of this region was defined as $X_{d}$. Thus for a transistor operating in the active region, the actual effective channel length $L_{\text {eff }}$ is given by

$$
\begin{equation*}
L_{\mathrm{eff}}=L_{\mathrm{drwn}}-2 L_{d}-X_{d} \tag{2.35}
\end{equation*}
$$

A precise determination of $X_{d}$ is complicated by the fact that the field distribution in the drain region is two-dimensional and quite complex. The drain depletion width $X_{d}$ can be approximated by assuming that the electric field in the drain region is one-dimensional and that the depletion width is that of a one-sided step junction with an applied voltage of $V_{D S}-V_{o v}$, where $V_{o v}=V_{G S}-V_{t}$ is the potential at the drain end of the channel with respect to the source. This assumption is used in the following example.

As shown in Chapter 1, the small-signal output resistance of the transistor is inversely proportional to the effective channel length. Because the performance of analog circuits often depends strongly on the transistor small-signal output resistance, analog circuits often use channel lengths that are longer than the minimum channel length for digital circuits. This statement is particularly true for unimplanted transistors.

#### EXAMPLE

Estimate the effective channel length for the unimplanted and implanted transistors for the process shown in Table 2.1 and the device geometry shown in Fig. 2.59. Assume the device is biased at a drain-source voltage of 5 V and a drain current of $10 \mu \mathrm{~A}$. Calculate the transconductance and the output resistance. For the calculation of $X_{d}$, assume that the depletion region between the drain and the end of the channel behaves like a step junction. At the given drain bias voltage, assume that the values of $d X_{d} / d V_{D S}$ have been deduced from other measurements to be $0.1 \mu \mathrm{~m} / \mathrm{V}$ for the unimplanted device and $0.02 \mu \mathrm{~m} / \mathrm{V}$ for the implanted device.

The metallurgical channel length is given by

$$
\begin{equation*}
L=L_{\mathrm{drwn}}-2 L_{d}=6 \mu \mathrm{~m}-(2 \times 0.3 \mu \mathrm{~m})=5.4 \mu \mathrm{~m} \tag{2.36}
\end{equation*}
$$

The effective channel length is this length minus the width of the depletion region at the drain $X_{d}$. In the active region, the voltage at the drain end of the channel is approximately $\left(V_{G S}-V_{t}\right)$. From (1.166),

$$
\begin{equation*}
V_{G S}-V_{t}=\sqrt{\frac{2 I_{D}}{\mu_{n} C_{o x} W / L}}=V_{o v} \tag{2.37}
\end{equation*}
$$

If we ignore $X_{d}$ at first and assume that $L \simeq L_{\text {eff }}$, we obtain a $V_{o v}$ of 0.16 V using the data from Table 2.1. Thus the voltage across the drain depletion region is approximately 4.84 V . To estimate the depletion-region width, assume it is a one-sided step junction that mainly exists in the lightly doped side. Since the channel and the drain are both $n$-type regions,
the built-in potential of the junction is near zero. The width of the depletion layer can be calculated using (1.14) or the nomograph in Fig. 2.29. Using (1.14), and assuming $N_{D} \gg N_{A}$,

$$
\begin{equation*}
X_{d}=\sqrt{\frac{2 \epsilon\left(V_{D S}-V_{o v}\right)}{q N_{A}}} \tag{2.38}
\end{equation*}
$$

For the unimplanted device, this equation gives a depletion width of $2.4 \mu \mathrm{~m}$. For the implanted device, the result is $0.5 \mu \mathrm{~m}$, assuming an effective constant channel doping of $2.1 \times 10^{16}$ atoms $/ \mathrm{cm}^{3}$. Thus the effective channel lengths of the two devices would be approximately $3.0 \mu \mathrm{~m}$ and $4.9 \mu \mathrm{~m}$, respectively.

From (1.180), the device transconductance is given by

$$
\begin{equation*}
g_{m}=\sqrt{2 \mu_{n} C_{o x}(W / L) I_{D}} \tag{2.39}
\end{equation*}
$$

Assuming that $\mu_{n}=700 \mathrm{~cm}^{2} / \mathrm{V}$-s, we find

$$
\begin{equation*}
g_{m}=\sqrt{2(700)\left(8.6 \times 10^{-8}\right)(50 / 3.0)\left(10 \times 10^{-6}\right)}=141 \mu \mathrm{~A} / \mathrm{V} \tag{2.40}
\end{equation*}
$$

for the unimplanted transistor and

$$
\begin{equation*}
g_{m}=\sqrt{2(700)\left(8.6 \times 10^{-8}\right)(50 / 4.9)\left(10 \times 10^{-6}\right)}=111 \mu \mathrm{~A} / \mathrm{V} \tag{2.41}
\end{equation*}
$$

for the implanted transistor.
The output resistance can be calculated by using (1.163) and (1.194). For the unimplanted device,

$$
\begin{equation*}
r_{o}=\frac{L_{\mathrm{eff}}}{I_{D}}\left(\frac{d X_{d}}{d V_{D S}}\right)^{-1}=\left(\frac{3.0 \mu \mathrm{~m}}{10 \mu \mathrm{~A}}\right) \frac{1}{0.1 \mu \mathrm{~m} / \mathrm{V}}=3.0 \mathrm{M} \Omega \tag{2.42}
\end{equation*}
$$

For the implanted device,

$$
\begin{equation*}
r_{o}=\left(\frac{4.9 \mu \mathrm{~m}}{10 \mu \mathrm{~A}}\right) \frac{1}{0.02 \mu \mathrm{~m} / \mathrm{V}}=25 \mathrm{M} \Omega \tag{2.43}
\end{equation*}
$$

Because the depletion region for unimplanted devices is much wider than for implanted devices, the channel length of unimplanted devices must be made longer than for implanted devices to achieve comparable punchthrough voltages and small-signal output resistances under identical bias conditions.

Effective Channel Width. The effective channel width of an MOS transistor is determined by the gate dimension parallel to the surface and perpendicular to the channel length over which the gate oxide is thin. Thick field oxide regions are grown at the edges of each transistor by using the local-oxidation process described in Sections 2.2.7 and 2.8. Before the field oxide is grown, nitride is deposited and patterned so that it remains only in areas that should become transistors. Therefore, the width of a nitride region corresponds to the the drawn width of a transistor. To minimize the width variation, the field oxide should grow only vertically; that is, the oxide thickness should increase only in regions where nitride does not cover the oxide. In practice, however, some lateral growth of oxide also occurs near the edges of the nitride during field-oxide growth. As a result, the edges of the field oxide are not vertical, as shown in Figures 2.9 and 2.54. This lateral growth of the oxide reduces the effective width of MOS transistors compared to their drawn widths. It is commonly referred to as the bird's beak because the gradually decreasing oxide thickness in the cross sections of Figures 2.9 and 2.54 resembles the corresponding portion of the profile of a bird.

As a result, both the effective lengths and the effective widths of transistors differ from the corresponding drawn dimensions. In analog design, the change in the effective length is usually much more important than the change in the effective width because transistors usually have drawn lengths much less than their drawn widths. As a result, the difference between the drawn and effective width is often ignored. However, this difference is sometimes important, especially when the matching between two ratioed transistors limits the accuracy of a given circuit. This topic is considered in Section 4.2.

Intrinsic Gate-Source Capacitance. As described in Chapter 1, the intrinsic gate-source capacitance of the transistor in the active region of operation is given by

$$
\begin{equation*}
C_{g s}=\frac{2}{3} W L_{\mathrm{eff}} C_{o x} \tag{2.44}
\end{equation*}
$$

The calculation of this parameter is illustrated in the next example.
Overlap Capacitance. Assuming that the source and drain regions each diffuse under the gate by $L_{d}$ after implantation, the gate-source and gate-drain overlap capacitances are given by

$$
\begin{equation*}
C_{o l}=W L_{d} C_{o x} \tag{2.45}
\end{equation*}
$$

This parasitic capacitance adds directly to the intrinsic gate-source capacitance. It constitutes the entire drain-gate capacitance in the active region of operation.

Junction Capacitances. Source-substrate and drain-substrate capacitances result from the junction-depletion capacitance between the source and drain diffusions and the substrate. A complicating factor in calculating these capacitances is the fact that the substrate doping around the source and drain regions is not constant. In the region of the periphery of the source and drain diffusions that border on the field regions, a relatively high surface concentration exists on the field side of the junction because of the field threshold adjustment implant. Although approximate calculations can be carried out, the zero-bias value and grading parameter of the periphery capacitance are often characterized experimentally by using test structures. The bulk-junction capacitance can be calculated directly by using (1.21) or can be read from the nomograph in Fig. 2.29.

An additional capacitance that must be accounted for is the depletion capacitance between the channel and the substrate under the gate, which we will term $C_{c s}$. Calculation of this capacitance is complicated by the fact that the channel-substrate voltage is not constant but varies along the channel. Also, the allocation of this capacitance to the source and drain varies with operating conditions in the same way as the allocation of $C_{g s}$. A reasonable approach is to develop an approximate total value for this junction capacitance under the gate and allocate it to source and drain in the same ratio as the gate capacitance is allocated. For example, in the active region, a capacitance of two-thirds of $C_{c s}$ would appear in parallel with the source-substrate capacitance and none would appear in parallel with the drain-substrate capacitance.

#### EXAMPLE

Calculate the capacitances of an implanted device with the geometry shown in Fig. 2.59. Use the process parameters given in Table 2.1 and assume a drain-source voltage of 5 V , drain current of $10 \mu \mathrm{~A}$, and no substrate bias voltage. Neglect the capacitance between the channel and the substrate. Assume that $X_{d}$ is negligibly small.

From (2.44), the intrinsic gate-source capacitance is

$$
\begin{equation*}
C_{g s}=\frac{2}{3} W L_{\mathrm{eff}} C_{o x}=\left(\frac{2}{3}\right) 50 \mu \mathrm{~m} \times 5.4 \mu \mathrm{~m} \times 0.86 \mathrm{fF} / \mu \mathrm{m}^{2}=155 \mathrm{fF} \tag{2.46}
\end{equation*}
$$

From (2.45), the overlap capacitance is given by

$$
\begin{equation*}
C_{o l}=W L_{d} C_{o x}=50 \mu \mathrm{~m} \times 0.3 \mu \mathrm{~m} \times 0.86 \mathrm{fF} / \mu \mathrm{m}^{2}=12.9 \mathrm{fF} \tag{2.47}
\end{equation*}
$$

Thus the total gate-source capacitance is $\left(C_{g s}+C_{o l}\right)$ or 168 fF . The gate-drain capacitance is equal to the overlap capacitance, or 12.9 fF .

The source- and drain-to-substrate capacitances consist of two portions. The periphery or sidewall part $C_{j s w}$ is associated with that portion of the edge of the diffusion area that is adjacent to the field region. The second portion $C_{j}$ is the depletion capacitance between the diffused junction and the bulk silicon under the source and drain. For the bias conditions given, the source-substrate junction operates with zero bias and the drain-substrate junction has a reverse bias of 5 V . Using Table 2.1 , the periphery portion for the source-substrate capacitance is

$$
\begin{equation*}
C_{j s w}(\text { source })=(50 \mu \mathrm{~m}+9 \mu \mathrm{~m}+9 \mu \mathrm{~m})(0.5 \mathrm{fF} / \mu \mathrm{m})=34 \mathrm{fF} \tag{2.48}
\end{equation*}
$$

Here, the perimeter is set equal to $W+2 L$ because that is the distance on the surface of the silicon around the part of the source and drain regions that border on field-oxide regions. Since the substrate doping is high along this perimeter to increase the magnitude of the threshold voltage in the field regions, the sidewall capacitance here is dominant. The bulk capacitance is simply the source-diffusion area multiplied by the capacitance per unit area from Table 2.1.

$$
\begin{equation*}
C_{j}(\text { source })=(50 \mu \mathrm{~m})(9 \mu \mathrm{~m})\left(0.08 \mathrm{fF} / \mu \mathrm{m}^{2}\right)=36 \mathrm{fF} \tag{2.49}
\end{equation*}
$$

The total capacitance from source to bulk is the sum of these two, or

$$
\begin{equation*}
C_{s b}=70 \mathrm{fF} \tag{2.50}
\end{equation*}
$$

For the geometry given for this example, the transistor is symmetrical, and the source and drain areas and peripheries are the same. From Table 2.1, both the bulk and periphery capacitances have a grading coefficient of 0.5 . As a result, the drain-bulk capacitance is the same as the source-bulk capacitance modified to account for the 5 V reverse bias on the junction. Assuming $\psi_{0}=0.65 \mathrm{~V}$,

$$
\begin{equation*}
C_{d b}=\frac{(70 \mathrm{fF})}{\sqrt{1+V_{D B} / \psi_{0}}}=\frac{(70 \mathrm{fF})}{\sqrt{1+5 / 0.65}}=24 \mathrm{fF} \tag{2.51}
\end{equation*}
$$

As the minimum channel length decreases, second-order effects cause the operation of short-channel MOS transistors to deviate significantly from the simple square-law models in Chapters 1 and 2. ${ }^{22}$ Equations that include these second-order effects are complicated and make hand calculations difficult. Therefore, simple models and equations that ignore these effects are often used as a design aid and to develop intuition. SPICE simulations with highly accurate device models are used to verify circuit peformance and to refine a design.

For processes with minimum allowed channel length less than $0.2 \mu \mathrm{~m}$, the gate-oxide thickness can fall below 30 Angstroms (for example, see Table 2.6). With such thin gate oxide, enough carriers in the channel can tunnel through the gate oxide and create nonzero dc gate current that is sometimes important. ${ }^{23}$ This current is referred to as gate-leakage current and is a complicated function of the operating point and oxide thickness. ${ }^{24,25}$ The gate-leakage current $I_{G}$ is the product of the gate-leakage-current density $J_{G}$ and the gate area. SPICE models are available that include gate-leakage current and accurately predict short-channel-device operation. ${ }^{26,27}$

### 2.9.2 p-Channel Transistors

The $p$-channel transistor in most CMOS technologies displays dc and ac properties that are comparable to the $n$-channel transistor. One difference is that the transconductance parameter $k^{\prime}$ of a $p$-channel device is about one-half to one-third that of an $n$-channel device because holes have correspondingly lower mobility than electrons. As shown in (1.209), this difference in mobility also reduces the $f_{T}$ of $p$-channel devices by the same factor. Another difference is that for a CMOS technology with a $p$-type substrate and $n$-type wells, the substrate terminal of the $p$-channel transistors can be electrically isolated since the devices are made in an implanted well. Good use can be made of this fact in analog circuits to alleviate the impact of the high body effect in these devices. For a CMOS process made on an $n$-type substrate with $p$-type wells, the $p$-channel devices are made in the substrate material, which is connected to the highest power-supply voltage, but the $n$-channel devices can have electrically isolated substrate terminals.

The calculation of device parameters for $p$-channel devices proceeds exactly as for $n$ channel devices. An important difference is the fact that for the $p$-channel transistors the threshold voltage that results if no threshold adjustment implant is used is relatively high, usually in the range of 1 to 3 V . This occurs because the polarities of the $Q_{s s}$ term and the work-function term are such that they tend to increase the $p$-channel threshold voltages while decreasing the $n$-channel threshold voltages. Thus the $p$-type threshold adjustment implant is used to reduce the surface concentration by partially compensating the doping of the $n$-type well or substrate. Thus in contrast to the $n$-channel device, the $p$-channel transistor has an effective surface concentration in the channel that is lower than the bulk concentration, and as a result, often displays a smaller incremental body effect for low values of substrate bias and a larger incremental body effect for larger values of substrate bias.

### 2.9.3 Depletion Devices

The properties of depletion devices are similar to those of the enhancement device already considered, except that an implant has been added in the channel to make the threshold negative (for an $n$-channel device). In most respects a depletion device closely resembles an enhancement device with a voltage source in series with the gate lead of value ( $V_{t D}-V_{t E}$ ), where $V_{t D}$ is the threshold voltage of the depletion-mode transistor and $V_{t E}$ is the threshold voltage of the enhancement-mode transistor. Depletion transistors are most frequently used with the gate tied to the source. Because the device is on with $V_{G S}=0$, if it operates in the active region, it operates like a current source with a drain current of

$$
\begin{equation*}
I_{D S S}=\left.I_{D}\right|_{V_{G S}=0}=\frac{\mu_{n} C_{o x}}{2} \frac{W}{L} V_{t D}^{2} \tag{2.52}
\end{equation*}
$$

An important aspect of depletion-device performance is the variation of $I_{D S S}$ with process variations. These variations stem primarily from the fact that the threshold voltage varies substantially from its nominal value due to processing variations. Since the transistor $I_{D S S}$ varies as the square of the threshold voltage, large variations in $I_{D S S}$ due to process variations often occur. Tolerances of $\pm 40$ percent or more from nominal due to process variations are common. Because $I_{D S S}$ determines circuit bias current and power dissipation, the magnitude of this variation is an important factor. Another important aspect of the behavior of depletion devices stems from the body effect. Because the threshold voltage varies with body bias, a depletion device with $V_{G S}=0$ and $v_{s b} \neq 0$ displays a finite conductance in the active region even if the effect of channel-length modulation is ignored. In turn, this finite conductance has a strong effect on the performance of analog circuits that use depletion devices as load elements.

### 2.9.4 Bipolar Transistors

Standard CMOS technologies include process steps that can be used to form a bipolar transistor whose collector is tied to the substrate. The substrate, in turn, is tied to one of the power supplies. Fig. $2.62 a$ shows a cross section of such a device. The well region forms the base of the transistor, and the source/drain diffusion of the device in the well forms the emitter. Since the current flow through the base is perpendicular to the surface of the silicon, the device is a vertical bipolar transistor. It is a pnp transistor in processes that utilize $p$-type substrates as in Fig. 2.62a and an $n p n$ transistor in processes that use an $n$-type substrate. The device is particularly useful in band-gap references, described in Chapter 4, and in output stages, considered in Chapter 5. The performance of the device is a strong function of well depth and doping but is generally similar to the substrate pnp transistor in bipolar technology, described in Section 2.5.2.

The main limitation of such a vertical bipolar transistor is that its collector is the substrate and is connected to a power supply to keep the substrate $p-n$ junctions reverse biased. Standard CMOS processes also provide another bipolar transistor for which the collector need not be connected to a power supply. ${ }^{28}$ Figure $2.62 b$ shows a cross section of such a device. As in the vertical transistor, the well region forms the base and a source/drain diffusion forms the emitter. In this case, however, another source/drain diffusion forms the collector $C_{1}$. Since the
image_name:(a)
description:The image labeled "(a)" shows a cross-sectional diagram of a vertical pnp transistor within an n-well CMOS process. It illustrates the structural components and their interactions within the device.

1. **Identification of Components and Structure:**
- The diagram features three main regions labeled E, B, and C, representing the emitter, base, and collector, respectively.
- The emitter (E) is connected to a p+ region, indicating a heavily doped p-type area.
- The base (B) is connected to an n+ region, indicating a heavily doped n-type area.
- The collector (C) is also connected to a p+ region.
- These regions are situated within an n-type well, which is embedded in a larger p-type substrate.

2. **Connections and Interactions:**
- The emitter (E) and collector (C) are both connected to p+ regions, suggesting that they are of the same doping type, which is typical for a pnp transistor.
- The base (B) is connected to an n+ region, serving as the control region for the transistor.
- The diagram suggests that the emitter injects holes into the base, which are then collected by the collector.
- The n-type well acts as a barrier, isolating the p+ regions from the p-type substrate, ensuring that the transistor operates correctly.

3. **Labels, Annotations, and Key Features:**
- The collector (C) is annotated with a note to connect it to the lowest supply, indicating its role in the transistor's operation.
- The diagram clearly labels the n-type well and p-type substrate, providing context for the device's fabrication process.
- The layout emphasizes the vertical structure of the transistor, with the flow of charge carriers occurring perpendicular to the substrate.

(a)

Gate (connect to highest supply)
image_name:(a)
description:The image labeled "(a)" is a cross-sectional diagram of a vertical pnp transistor in an n-well CMOS process. The diagram illustrates several key components and structures:

1. **Components and Structure:**
- The diagram features a pnp transistor structure, which includes emitter (E), base (B), and collector (C1, C2) regions.
- The emitter is labeled as "E" and positioned on the left side, connected to a p+ region.
- The base, labeled "B," is centrally located and connected to an n+ region.
- Two collectors are indicated as "C1" and "C2," each connected to p+ regions, with C1 positioned near the emitter and C2 on the far right.
- The entire structure is built on an n-type well, which is highlighted in the diagram.
- A gate made of SiO2 is shown above the n-type well, with a note to connect it to the highest supply.

2. **Connections and Interactions:**
- The p+ regions (E, C1, C2) and the n+ region (B) are connected via the n-type well substrate, allowing for charge carrier movement within the transistor.
- The diagram suggests that the gate (SiO2) should be connected to the highest supply, while collector C2 should be connected to the lowest supply, indicating a specific biasing arrangement for the transistor's operation.

3. **Labels, Annotations, and Key Features:**
- The n-type well and p-type substrate are clearly labeled, providing context for the fabrication process of the device.
- The diagram emphasizes the vertical structure of the transistor, with the flow of charge carriers occurring perpendicular to the substrate.
- Annotations indicate the connections for the gate and collector C2, guiding the user on the appropriate supply connections for optimal operation.
$p$-type substrate
(b)

image_name:(c)
description:
[
name: BJT, type: PNP, ports: {C: C1, B: B, E: E}
]
extrainfo:The diagram shows a PNP bipolar junction transistor with capacitors C1 and C2 connected to the collector and emitter, respectively. Currents IC1 and IC2 are flowing through C1 and C2.
(c)

Figure 2.62 (a) Cross section of a vertical pnp transistor in an $n$-well CMOS process. (b) Cross section of lateral and vertical pnp transistors in an $n$-well CMOS process. (c) Schematic of the bipolar transistors in (b).
current flow through the base is parallel to the surface of the silicon, this device is a lateral bipolar transistor. Again, it is a pnp transistor in processes that utilize $n$-type wells and an $n p n$ transistor in processes that use $p$-type wells. The emitter and collector of this lateral device correspond to the source and drain of an MOS transistor. Since the goal here is to build a bipolar transistor, the MOS transistor is deliberately biased to operate in the cutoff region. In Fig. 2.62b, for example, the gate of the $p$-channel transistor must be connected to a voltage sufficient to bias it in the cutoff region. A key point here is that the base width of the lateral bipolar device corresponds to the channel length of the MOS device.

One limitation of this structure is that when a lateral bipolar transistor is intentionally formed, a vertical bipolar transistor is also formed. In Fig. 2.62b, the emitter and base connections of the vertical transistor are the same as for the lateral transistor, but the collector is the substrate, which is connected to the lowest supply voltage. When the emitter injects minority carriers into the base, some flow parallel to the surface and are collected by the collector of the lateral transistor $C_{1}$. However, others flow perpendicular to the surface and are collected by the substrate $C_{2}$. Figure $2.62 c$ models this behavior by showing a transistor symbol with one emitter and one base but two collectors. The current $I_{C 1}$ is the collector current of the lateral transistor, and $I_{C 2}$ is the collector current of the vertical transistor. Although the base current is small because little recombination and reverse injection occur, the undesired current $I_{C 2}$ is comparable to the desired current $I_{C 1}$. To minimize the ratio, the collector of the lateral transistor usually surrounds the emitter, and the emitter area as well as the lateral base width are minimized. Even with these techniques, however, the ratio of $I_{C 2} / I_{C 1}$ is poorly controlled in practice. ${ }^{28,29}$ If the total emitter current is held constant as in many conventional circuits, variation of $I_{C 2} / I_{C 1}$ changes the desired collector current and associated small-signal parameters such as the transconductance. To overcome this problem, the emitter current can be adjusted by negative feedback so that the desired collector current is insensitive to variations in $I_{C 2} / I_{C 1}{ }^{30}$

Some important properties of the lateral bipolar transistor, including its $\beta_{F}$ and $f_{T}$, improve as the base width is reduced. Since the base width corresponds to the channel length of an MOS transistor, the steady reduction in the minimum channel length of scaled MOS technologies is improving the performance and increasing the importance of the available lateral bipolar transistor.

## 2.10 Passive Components in MOS Technology

In this section, we describe the various passive components that are available in CMOS technologies. Resistors include diffused, poly-silicon, and well resistors. Capacitors include poly-poly, metal-poly, metal-silicon, silicon-silicon, and vertical and lateral metal-metal.

### 2.10.1 Resistors

Diffused Resistors. The diffused layer used to form the source and drain of the $n$-channel and $p$-channel devices can be used to form a diffused resistor. The resulting resistor structure and properties are very similar to the resistors described in Section 2.6.1 on diffused resistors in bipolar technology. The sheet resistances, layout geometries, and parasitic capacitances are similar.

Polysilicon Resistors. At least one layer of polysilicon is required in silicon-gate MOS technologies to form the gates of the transistors, and this layer is often used to form resistors. The geometries employed are similar to those used for diffused resistors, and the resistor exhibits a
image_name:(a)
description:The image labeled as Figure 2.63 (a) provides both a plan view and a cross-sectional view of a polysilicon resistor used in silicon-gate MOS technology.

1. **Identification of Components and Structure:**
- **Plan View:** The top part of the image shows a layout of the polysilicon resistor. It features a rectangular shape with metal contacts at both ends, represented by squares. The resistor is depicted as a straight line connecting these contacts. Triangular shapes along the line likely indicate connection points or measurement markings.
- **Cross Section:** The bottom part of the image provides a side view of the resistor. This view shows the polysilicon layer sitting on a field oxide layer, which is on top of a substrate. Metal contacts are connected to the ends of the polysilicon layer, allowing for electrical connectivity.

2. **Connections and Interactions:**
- The metal contacts at each end of the polysilicon layer serve as terminals for the resistor, allowing current to flow through the polysilicon. The field oxide beneath the polysilicon acts as an insulator, preventing unwanted current leakage to the substrate.
- The cross-section illustrates how the polysilicon is isolated from the substrate by the field oxide, and how metal contacts interface with the polysilicon to facilitate electrical connections.

3. **Labels, Annotations, and Key Features:**
- The scale on the left side of the image indicates that the plan view dimensions are given in micrometers (µm), with the resistor length extending to approximately 35 µm.
- Labels such as "Metal," "Polysilicon," "Field oxide," and "Substrate" help identify different materials and layers in the cross-sectional view.
- The image provides a clear representation of how the polysilicon resistor is integrated into the silicon-gate MOS technology, highlighting its structural and material composition.

Figure 2.63 (a) Plan view and cross section of polysilicon resistor.
parasitic capacitance to the underlying layer much like a diffused resistor. In this case, however, the capacitance stems from the oxide layer under the polysilicon instead of from a reversebiased $p n$ junction. The nominal sheet resistance of most polysilicon layers that are utilized in MOS processes is on the order of $20 \Omega / \square$ to $80 \Omega / \square$ and typically displays a relatively large variation around the nominal value due to process variations. The matching properties of polysilicon resistors are similar to those of diffused resistors. A cross section and plan view of a typical polysilicon resistor are shown in Fig. 2.63a.

The sheet resistance of polysilicon can limit the speed of interconnections, especially in submicron technologies. To reduce the sheet resistance, a silicide layer is sometimes deposited on top of the polysilicon. Silicide is a compound of silicon and a metal, such as tungsten, that can withstand subsequent high-temperature processing with little movement. Silicide reduces the sheet resistance by about an order of magnitude. Also, it has little effect on the oxidation rate of polysilicon and is therefore compatible with conventional CMOS process technologies. ${ }^{31}$ Finally, silicide can be used on the source/drain diffusions as well as on the polysilicon.

Well Resistors. In CMOS technologies the well region can be used as the body of a resistor. It is a relatively lightly doped region and when used as a resistor provides a sheet resistance on the order of $10 \mathrm{k} \Omega / \square$. Its properties and geometrical layout are much like the epitaxial resistor described in Section 2.6 .2 and shown in Fig. 2.42. It displays large tolerance, high voltage coefficient, and high temperature coefficient relative to other types of resistors. Higher sheet resistance can be achieved by the addition of the pinching diffusion just as in the bipolar technology case.

MOS Devices as Resistors. The MOS transistor biased in the triode region can be used in many circuits to perform the function of a resistor. The drain-source resistance can be calculated by differentiating the equation for the drain current in the triode region with respect to the drain-source voltage. From (1.152),

$$
\begin{equation*}
R=\left(\frac{\partial I_{D}}{\partial V_{D S}}\right)^{-1}=\frac{L}{W} \frac{1}{k^{\prime}\left(V_{G S}-V_{t}-V_{D S}\right)} \tag{2.53}
\end{equation*}
$$

Since $L / W$ gives the number of squares, the second term on the right side of this equation gives the sheet resistance. This equation shows that the effective sheet resistance is a function of the applied gate bias. In practice, this sheet resistance can be much higher than polysilicon or diffused resistors, allowing large amounts of resistance to be implemented in a small area. Also, the resistance can be made to track the transconductance of an MOS transistor operating in the active region, allowing circuits to be designed with properties insensitive to variations in process, supply, and temperature. An example of such a circuit is considered in Section 9.4.3. The principal drawback of this form of resistor is the high degree of nonlinearity of the resulting resistor element; that is, the drain-source resistance is not constant but depends on the drain-source voltage. Nevertheless, it can be used very effectively in many applications.

### 2.10.2 Capacitors in MOS Technology

As a passive component, capacitors play a much more important role in MOS technology than they do in bipolar technology. Because of the fact that MOS transistors have virtually infinite input resistance, voltages stored on capacitors can be sensed with little leakage using MOS amplifiers. As a result, capacitors can be used to perform many functions that are traditionally performed by resistors in bipolar technology.

Poly-Poly Capacitors. Many MOS technologies that are used to implement analog functions have two layers of polysilicon. The additional layer provides an efficient capacitor structure, an extra layer of interconnect, and can also be used to implement floating-gate memory cells that are electrically programmable and optically erasable with UV light (EPROM). A typical poly-poly capacitor structure is shown in cross section and plan view in Fig. 2.63b. The plate separation is usually comparable to the gate oxide thickness of the MOS transistors.

An important aspect of the capacitor structure is the parasitic capacitance associated with each plate. The largest parasitic capacitance exists from the bottom plate to the underlying layer, which could be either the substrate or a well diffusion whose terminal is electrically isolated. This bottom-plate parasitic capacitance is proportional to the bottom-plate area and typically has a value from 10 to 30 percent of the capacitor itself.
image_name:Plan view
description:The image illustrates a typical poly-poly capacitor, presented in both plan view and cross-section. The plan view shows a square layout with dashed lines indicating the boundaries of the capacitor plates. Small triangular symbols along the edges represent connections or potential points of parasitic capacitance.

In the cross-sectional view, the structure is layered as follows:

1. **First Poly Layer**: This layer forms the bottom plate of the capacitor. It is laid directly above the silicon substrate.

2. **SiO2 Layer**: This insulating layer separates the first and second poly layers, acting as the dielectric material of the capacitor. It is crucial for maintaining the electrical separation between the two plates.

3. **Second Poly Layer**: Positioned above the SiO2 layer, this forms the top plate of the capacitor. It is connected to the rest of the circuit through interconnect metallization or polysilicon.

4. **Si-Substrate**: The base layer, which supports the entire structure. It is typically silicon and may contribute to parasitic capacitance with the bottom plate.

**Connections and Interactions:**
- The triangular symbols on the plan view likely indicate connections or points of interest where parasitic capacitance might occur.
- The cross-section reveals how the layers are stacked, with the SiO2 layer ensuring electrical isolation between the poly layers, which are the active plates of the capacitor.

**Labels, Annotations, and Key Features:**
- The image is labeled with key components such as "First poly layer," "SiO2," "Second poly layer," and "Si-Substrate," providing clear identification of each element.
- The dashed lines and triangular symbols in the plan view suggest the layout and potential parasitic interaction points, which are critical for understanding the electrical characteristics of the capacitor.
image_name:Figure 2.63 (b)
description:The image labeled as "Figure 2.63 (b)" presents a plan view and cross-section of a typical poly-poly capacitor. This capacitor structure is prominently used in integrated circuits for its stable capacitance characteristics.

Identification of Components and Structure:
1. **Plan View:**
- The top view shows a rectangular layout, indicating the footprint of the capacitor.
- The structure is defined by two primary layers: the "First poly layer" and the "Second poly layer," which form the plates of the capacitor.

2. **Cross-Section View:**
- The cross-section illustrates the vertical stack of materials.
- At the bottom is the **Si-Substrate**, a silicon base that supports the entire structure.
- Above the substrate is the **First poly layer**, which acts as the bottom plate of the capacitor.
- The **SiO2** layer, an oxide layer, separates the two polysilicon layers, serving as the dielectric material.
- The **Second poly layer** is placed on top of the SiO2, forming the top plate of the capacitor.

Connections and Interactions:
- The plan view indicates connections to external circuitry, represented by dashed lines leading to the edges of the capacitor.
- These connections are likely for interfacing the capacitor with other components in an integrated circuit.

Labels, Annotations, and Key Features:
- Annotations clearly label the different layers: "First poly layer," "SiO2," and "Second poly layer."
- The Si-Substrate is also labeled, indicating its foundational role.
- The plan view and cross-section together provide a comprehensive understanding of the capacitor's layout and construction.

This detailed depiction helps in understanding the construction and function of poly-poly capacitors, highlighting their role in minimizing parasitic capacitance and optimizing performance in electronic circuits.

Figure 2.63 (b) Plan view and cross section of typical poly-poly capacitor.

The top-plate parasitic is contributed by the interconnect metallization or polysilicon that connects the top plate to the rest of the circuit, plus the parasitic capacitance of the transistor to which it is connected. In the structure shown in Fig. 2.63b, the drain-substrate capacitance of an associated MOS transistor contributes to the top-plate parasitic capacitance. The minimum value of this parasitic is technology dependent but is typically on the order of 5 fF to 50 fF .

Other important parameters of monolithic capacitor structures are the tolerance, voltage coefficient, and temperature coefficient of the capacitance value. The tolerance on the absolute value of the capacitor value is primarily a function of oxide-thickness variations and is usually in the 10 percent to 30 percent range. Within the same die, however, the matching of one capacitor to another identical structure is much more precise and can typically be in the range of 0.05 percent to 1 percent, depending on the geometry. Because the plates of the capacitor are a heavily doped semiconductor rather than an ideal conductor, some variation in surface potential relative to the bulk material of the plate occurs as voltage is applied to the capacitor. ${ }^{32}$ This effect is analogous to the variation in surface potential that occurs in an MOS transistor when a voltage is applied to the gate. However, since the impurity concentration in the plate is usually relatively high, the variations in surface potential are small. The result of these surface potential variations is a slight variation in capacitance with applied voltage. Increasing the doping in the capacitor plates reduces the voltage coefficient. For the impurity concentrations that are typically used in polysilicon layers, the voltage coefficient is usually less than $50 \mathrm{ppm} / \mathrm{V},{ }^{32,33}$ a level small enough to be neglected in most applications.

A variation in the capacitance value also occurs with temperature variations. This variation stems primarily from the temperature variation of the surface potential in the plates previously described. ${ }^{32}$ Also, secondary effects include the temperature variation of the dielectric constant and the expansion and contraction of the dielectric. For heavily doped polysilicon plates, this temperature variation is usually less than $50 \mathrm{ppm} /{ }^{\circ} \mathrm{C} .{ }^{32,33}$

MOS Transistors as Capacitors. The MOS transistor itself can be used as a capacitor when biased in the triode region, the gate forming one plate and the source, drain, and channel forming another. Unfortunately, because the underlying substrate is lightly doped, a large amount of surface potential variation occurs with changes in applied voltage and the capacitor displays a high voltage coefficient. In noncritical applications, however, it can be used effectively under two conditions. The circuit must be designed in such a way that the device is biased in the triode region when a high capacitance value is desired, and the high sheet resistance of the bottom plate formed by the channel must be taken into account.

Other Vertical Capacitor Structures. In processes with only one layer of polysilicon, alternative structures must be used to implement capacitive elements. One approach involves the insertion of an extra mask to reduce the thickness of the oxide on top of the polysilicon layer so that when the interconnect metallization is applied, a thin-oxide layer exists between the metal layer and the polysilicon layer in selected areas. Such a capacitor has properties that are similar to poly-poly capacitors.

Another capacitor implementation in single-layer polysilicon processing involves the insertion of an extra masking and diffusion operation such that a diffused layer with low sheet resistance can be formed underneath the polysilicon layer in a thin-oxide area. This is not possible in conventional silicon-gate processes because the polysilicon layer is deposited before the source-drain implants or diffusions are performed. The properties of such capacitors are similar to the poly-poly structure, except that the bottom-plate parasitic capacitance
is that of a pn junction, which is voltage dependent and is usually larger than in the poly-poly case. Also, the bottom plate has a junction leakage current that is associated with it, which is important in some applications.

To avoid the need for extra processing steps, capacitors can also be constructed using the metal and poly layers with standard oxide thicknesses between layers. For example, in a process with one layer of polysilicon and two layers of metal, the top metal and the poly can be connected together to form one plate of a capacitor, and the bottom metal can be used to form the other plate. A key disadvantage of such structures, however, is that the capacitance per unit area is small because the oxide used to isolate one layer from another is thick. Therefore, such capacitors usually occupy large areas. Furthermore, the thickness of this oxide changes little as CMOS processes evolve with reduced minimum channel length. As a result, the area required by analog circuits using such capacitors undergoes a much smaller reduction than that of digital circuits in new technologies. This characteristic is important because reducing the area of an integrated circuit reduces its cost.

Lateral Capacitor Structures. To reduce the capacitor area, and to avoid the need for extra processing steps, lateral capacitors can be used. ${ }^{34}$ A lateral capacitor can be formed in one layer of metal by separating one plate from another by spacing $s$, as shown in Fig. 2.64a. If $w$ is the width of the metal and $t$ is the metal thickness, the capacitance is $(w t \epsilon / s)$, where $\epsilon$ is the dielectric constant. As technologies evolve to reduced feature sizes, the minimum metal spacing shrinks but the thickness changes little; therefore, the die area required for a given lateral capacitance decreases in scaled technologies. ${ }^{35}$ Note that the lateral capacitance is proportional to the perimeter of each plate that is adjacent to the other in a horizontal plane. Geometries to increase this perimeter in a given die area have been proposed. ${ }^{35}$

Lateral capacitors can be used in conjunction with vertical capacitors, as shown in Fig. $2.64 b .{ }^{34}$ The key point here is that each metal layer is composed of multiple pieces, and each capacitor node is connected in an alternating manner to the pieces in each layer.
image_name:(a)
description:The image labeled as "(a)" depicts a lateral capacitor structure on one level of metal. The diagram shows two parallel rectangular metal plates separated by a gap. The key dimensions are labeled as follows:

1. **Width (w):** The horizontal dimension of each metal plate.
2. **Thickness (t):** The vertical dimension or height of each metal plate.
3. **Spacing (s):** The distance between the two parallel metal plates.

The design suggests that the lateral capacitance is formed between the adjacent sides of the plates, emphasizing the role of the perimeter in enhancing capacitance. This configuration is typically used to maximize capacitance within a given die area by increasing the effective perimeter of the plates. The simple rectangular shape of the plates in a single layer highlights the basic concept of lateral capacitance without additional complexity from multiple layers or vertical components.
image_name:(b)
description:The diagram labeled (b) illustrates a capacitor design using two levels of metal to achieve both lateral and vertical capacitance. The image shows four rectangular metal blocks arranged in two layers. Each block is labeled either 'A' or 'B', indicating alternating connections. The blocks are stacked with a vertical separation labeled as \( t_{ox} \), representing the oxide layer thickness between the layers.

**1. Identification of Components and Structure:**
- **Metal Blocks:** There are four metal blocks, two labeled 'A' and two labeled 'B'. These blocks are arranged such that each layer contains one 'A' and one 'B' block.
- **Dimensions:** The dimensions of the blocks are marked with \( w \) for width, \( t \) for thickness, and \( L \) for length. The separation between adjacent blocks in the same layer is denoted by \( s \).

**2. Connections and Interactions:**
- **Alternating Connections:** The alternating labeling of the blocks (A and B) suggests that each layer is connected in an alternating pattern. This configuration is designed to enhance both lateral and vertical capacitance.
- **Capacitance Contributions:** The total capacitance is a combination of the lateral capacitance between adjacent blocks in the same layer and the vertical capacitance between blocks in different layers.

**3. Labels, Annotations, and Key Features:**
- **\( t_{ox} \):** Indicates the thickness of the oxide layer separating the two metal layers, crucial for vertical capacitance.
- **Capacitor Symbol:** On the right side of the diagram, a capacitor symbol is shown with 'A' and 'B' indicating the nodes, reinforcing the connection pattern and the function of the structure as a capacitor.

This arrangement allows for increased total capacitance by utilizing both lateral and vertical components, effectively using the available die area more efficiently than a purely vertical capacitor structure.

Figure 2.64 (a) Lateral capacitor in one level of metal. (b) Capacitor using two levels of metal in which both lateral and vertical capacitance contribute to the desired capacitance.

As a result, the total capacitance includes vertical and lateral components arising between all adjacent pieces. If the vertical and lateral dielectric constants are equal, the total capacitance is increased compared to the case in which the same die area is used to construct only a vertical capacitor when the minimum spacing $s<\sqrt{2 t\left(t_{o x}\right)}$, where $t$ is the metal thickness and $t_{o x}$ is the oxide thickness between metal layers. This concept can be extended to additional pieces in each layer and additional layers.

### 2.10.3 Latchup in CMOS Technology

The device structures that are present in standard CMOS technology inherently comprise a pnpn sandwich of layers. For example, consider the typical circuit shown in Fig. 2.65a. It uses one $n$-channel and one $p$-channel transistor and operates as an inverter if the two gates are connected together as the inverter input. Figure $2.65 b$ shows the cross section in an $n$-well process. When the two MOS transistors are fabricated, two parasitic bipolar transistors are also formed: a lateral $n p n$ and a vertical $p n p$. In this example, the source of the $n$-channel transistor forms the emitter of the parasitic lateral npn transistor, the substrate forms the base, and the $n$-well forms the collector. The source of the $p$-channel transistor forms the emitter of a parasitic vertical pnp transistor, the $n$-well forms the base, and the $p$-type substrate forms the collector. The electrical connection of these bipolar transistors that results from the layout shown is illustrated in Fig. $2.65 c$. In normal operation, all the $p n$ junctions in the structure are reverse biased. If the two bipolar transistors enter the active region for some reason, however, the circuit can display a large amount of positive feedback, causing both transistors to conduct heavily. This device structure is similar to that of a silicon-controlled rectifier (SCR), a widely used component in
(a)
image_name:(a)
description:
[
name: M1, type: NMOS, ports: {S: GND, D: Output, G: G1}
name: M2, type: PMOS, ports: {S: V+, D: Output, G: G2}
]
extrainfo:The circuit is a CMOS inverter with NMOS (M1) and PMOS (M2) transistors. The input nodes are G1 and G2, and the output is at the 'Output' node. The power supply is connected to V+ and ground (GND).

(b)
image_name:(b)
description:The circuit diagram illustrates the cross-section of parasitic bipolar transistors in a CMOS structure. The resistors R1 and R2 are connected between various nodes, with R1 connecting to ground and R2 connecting across the n and p regions. G1 and G2 are gates connected to ground and V+ respectively. The output is labeled at the top of the diagram.

(c)
image_name:(c)
description:The circuit diagram illustrates a CMOS structure with parasitic bipolar transistors. R1 is connected to ground, and R2 is connected across the n and p regions. The gates G1 and G2 are connected to ground and V+ respectively, creating a positive feedback loop labeled as PFB. This configuration can lead to latchup, a destructive breakdown phenomenon.

Figure 2.65 (a) Schematic of a typical CMOS device pair. (b) Cross section illustrating the parasitic bipolar transistors. (c) Schematic of the parasitic bipolar transistors.
power-control applications. In power-control applications, the property of the pnpn sandwich to remain in the on state with no externally supplied signal is a great advantage. However, the result of this behavior here is usually a destructive breakdown phenomenon called latchup.

The positive feedback loop is labeled in Fig. 2.65c. Feedback is studied in detail in Chapters 8 and 9. To explain why the feedback around this loop is positive, assume that both transistors are active and that the base current of the $n p n$ transistor increases by $i$ for some reason. Then the collector current of the npn transistor increases by $\beta_{n p n} i$. This current is pulled out of the base of the pnp transistor if $R_{2}$ is ignored. As a result, the current flowing out of the collector of the pnp transistor increases by $\beta_{n p n} \beta_{p n p} i$. Finally, this current flows into the base of the $n p n$ transistor if $R_{1}$ is ignored. This analysis shows that the circuit generates a current that flows in the same direction as the initial disturbance; therefore, the feedback is positive. If the gain around the loop is more than unity, the response of the circuit to the initial disturbance continues to grow until one or both of the bipolar transistors saturate. In this case, a large current flows from the positive supply to ground until the power supply is turned off or the circuit burns out. This condition is called latchup. If $R_{1}$ and $R_{2}$ are large enough that base currents are large compared to the currents in these resistors, the gain around the loop is $\beta_{n p n} \beta_{p n p}$. Therefore, latchup can occur if the product of the betas is greater than unity.

For latchup to occur, one of the junctions in the sandwich must become forward biased. In the configuration illustrated in Fig. 2.65, current must flow in one of the resistors between the emitter and the base of one of the two transistors in order for this to occur. This current can come from a variety of causes. Examples are an application of a voltage that is larger than the power-supply voltage to an input or output terminal, improper sequencing of the power supplies, the presence of large dc currents in the substrate or $p$ - or $n$-well, or the flow of displacement current in the substrate or well due to fast-changing internal nodes. Latchup is more likely to occur in circuits as the substrate and well concentration is made lighter, as the well is made thinner, and as the device geometries are made smaller. All these trends in process technology tend to increase $R_{1}$ and $R_{2}$ in Fig. $2.65 b$. Also, they tend to increase the betas of the two bipolar transistors. These changes increase the likelihood of the occurrence of latchup.

The layout of CMOS-integrated circuits must be carried out with careful attention paid to the prevention of latchup. Although the exact rules followed depend on the specifics of the technology, the usual steps are to keep $R_{1}$ and $R_{2}$, as well as the product of the betas, small enough to avoid this problem. The beta of the vertical bipolar transistor is determined by process characteristics, such as the well depth, that are outside the control of circuit designers. However, the beta of the lateral bipolar transistor can be decreased by increasing its base width, which is the distance between the source of the $n$-channel transistor and the $n$-type well. To reduce $R_{1}$ and $R_{2}$, many substrate and well contacts are usually used instead of just one each, as shown in the simple example of Fig. 2.65. In particular, guard rings of substrate and well contacts are often used just outside and inside the well regions. These rings are formed by using the source/drain diffusion and provide low-resistance connections in the substrate and well to reduce series resistance. Also, special protection structures at each input and output pad are usually included so that excessive currents flowing into or out of the chip are safely shunted.

## 2.11 BiCMOS Technology

In Section 2.3, we showed that to achieve a high collector-base breakdown voltage in a bipolar transistor structure, a thick epitaxial layer is used ( $17 \mu \mathrm{~m}$ of $5 \Omega-\mathrm{cm}$ material for $36-\mathrm{V}$ operation). This in turn requires a deep $p$-type diffusion to isolate transistors and other devices.

On the other hand, if a low breakdown voltage (say about 7 V to allow 5-V supply operation) can be tolerated, then a much more heavily doped (on the order of $0.5 \Omega-\mathrm{cm}$ ) collector region can be used that is also much thinner (on the order of $1 \mu \mathrm{~m}$ ). Under these conditions, the bipolar devices can be isolated by using the same local-oxidation technique used for CMOS, as described in Section 2.4. This approach has the advantage of greatly reducing the bipolar transistor collector-substrate parasitic capacitance because the heavily doped high-capacitance regions near the surface are now replaced by low-capacitance oxide isolation. The devices can also be packed much more densely on the chip. In addition, CMOS and bipolar fabrication technologies begin to look rather similar, and the combination of high-speed, shallow, ionimplanted bipolar transistors with CMOS devices in a BiCMOS technology becomes feasible (at the expense of several extra processing steps). ${ }^{36}$ This technology has performance advantages in digital applications because the high current-drive capability of the bipolar transistors greatly facilitates driving large capacitive loads. Such processes are also attractive for analog applications because they allow the designer to take advantage of the unique characteristics of both types of devices.

We now describe the structure of a typical high-frequency, low-voltage, oxide-isolated BiCMOS process. A simplified cross section of a high-performance process ${ }^{37}$ is shown in Fig. 2.66. The process begins with masking steps and the implantation of $n$-type antimony buried layers into a $p$-type substrate wherever an npn bipolar transistor or PMOS device is to be formed. A second implant of $p$-type boron impurities forms a $p$-well wherever an NMOS device is to be formed. This is followed by the growth of about $1 \mu \mathrm{~m}$ of $n^{-}$epi, which forms the collectors of the npn bipolar devices and the channel regions of the PMOS devices. During this and subsequent heat cycles, the more mobile boron atoms out-diffuse and the $p$-well extends to the surface, whereas the antimony buried layers remain essentially fixed.

A masking step defines regions where thick field oxide is to be grown and these regions are etched down into the epi layer. Field-oxide growth is then carried out, followed by a planarization step where the field oxide that has grown above the plane of the surface is etched back level with the other regions. This eliminates the lumpy surface shown in Fig. 2.57 and helps to overcome problems of ensuring reliable metal connections over the oxide steps (so-called step coverage). Finally, a series of masking steps and $p$ - and $n$-type implants are carried out to form bipolar base and emitter regions, low-resistance bipolar collector contact, and source and drain regions for the MOSFETs. In this sequence, gate oxide is grown, polysilicon gates and emitters are formed, and threshold-adjusting implants are made for the MOS devices. Metal contacts are then made to the desired regions, and the chip is coated with a layer of deposited $\mathrm{SiO}_{2}$. A second layer of metal interconnects is formed on top of this oxide with connections where necessary to the first layer of metal below. A further deposited layer of $\mathrm{SiO}_{2}$ is then added with a third layer of metal interconnect and vias to give even more connection flexibility and thus to improve the density of the layout.

## 2.12 Heterojunction Bipolar Transistors

A heterojunction is a pn junction made of two different materials. Until this point, all the junctions we have considered have been homojunctions because the same material (silicon) has been used to form both the $n$-type and the $p$-type regions. In contrast, a junction between an $n$-type region of silicon and a $p$-type region of germanium or a compound of silicon and germanium forms a heterojunction.

In homojunction bipolar transistors, the emitter doping is selected to be much greater than the base doping to give an emitter injection efficiency $\gamma$ of about unity, as shown by
image_name:Figure 2.66 Cross section of a high-performance BiCMOS process
description:The image depicts a cross-section of a high-performance BiCMOS process, showcasing the integration of bipolar and CMOS technologies on a single semiconductor substrate. The diagram is divided into two main sections, each illustrating different components and structures.

1. **Identification of Components and Structure:**
- **Base Contact and Polysilicon Emitter:** On the left side, a metal base contact is visible, connected to a polysilicon emitter. This is part of the bipolar transistor structure. The base is denoted as \( p^- \) and is lightly doped compared to the heavily doped \( p^+ \) base contact region.
- **Collector Contact:** Adjacent to the base, the collector contact is shown, connecting to an \( n^+ \) region. This is part of the bipolar transistor's collector.
- **Polysilicon Gate and Source/Drain Contacts:** On the right side, the CMOS structure is visible with polysilicon gates, source, and drain contacts. The source and drain regions are \( n^+ \) and \( p^+ \) doped, indicating NMOS and PMOS transistors.
- **Substrate and Wells:** The substrate is labeled as \( p^- \), with \( n^- \) and \( p \) wells beneath the CMOS transistors, providing isolation and forming the body of the transistors.

2. **Connections and Interactions:**
- The bipolar and CMOS components are integrated on a single substrate, with field oxide and gate oxide layers providing isolation and supporting the formation of MOS structures.
- The \( n^+ \) buried layer beneath the bipolar section reduces parasitic resistance and enhances performance.
- The polysilicon gates control the channel formation between the source and drain in the CMOS transistors.

3. **Labels, Annotations, and Key Features:**
- **Deposited Oxide:** This label indicates the oxide layers deposited over the structures, providing insulation and support.
- **Field Oxide and Gate Oxide:** These are crucial for isolating different components and forming the gate dielectric in MOS transistors.
- **Annotations:** Various doping levels are indicated (\( p^+ \), \( n^+ \), \( n^- \), \( p^- \)), highlighting the different regions and their roles in the device operation.

This cross-section illustrates the complexity of integrating bipolar and CMOS technologies, highlighting the distinct regions and layers that enable high-performance operation in BiCMOS devices.

Figure 2.66 Cross section of a high-performance BiCMOS process.
(1.51b). As a result, the base is relatively lightly doped while the emitter is heavily doped in practice. Section 1.4.8 shows that the $f_{T}$ of bipolar devices is limited in part by $\tau_{F}$, which is the time required for minority carriers to cross the base. Maximizing $f_{T}$ is important in some applications such as radio-frequency electronics. To increase $f_{T}$, the base width can be reduced. If the base doping is fixed to maintain a constant $\gamma$, however, this approach increases the base resistance $r_{b}$. In turn, this base resistance limits speed because it forms a time constant with capacitance attached to the base node. As a result, a tradeoff exists in standard bipolar technology between high $f_{T}$ on the one hand and low $r_{b}$ on the other, and both extremes limit the speed that can be attained in practice.

One way to overcome this tradeoff is to add some germanium to the base of bipolar transistors to form heterojunction transistors. The key idea is that the different materials on the two sides of the junction have different band gaps. In particular, the band gap of silicon is greater than for germanium, and forming a SiGe compound in the base reduces the band gap there. The relatively large band gap in the emitter can be used to increase the potential barrier to holes that can be injected from the base back to the emitter. Therefore, this structure does not require that the emitter doping be much greater than the base doping to give $\gamma \simeq 1$. As a result, the emitter doping can be decreased and the base doping can be increased in a heterojunction bipolar transistor compared to its homojunction counterpart. Increasing the base doping allows $r_{b}$ to be constant even when the base width is reduced to increase $f_{T}$. Furthermore, this change also reduces the width of the base-collector depletion region in the base when the transistor operates in the forward active region, thus decreasing the effect of base-width modulation and increasing the early voltage $V_{A}$. Not only does increasing the base doping have a beneficial effect on performance, but also decreasing the emitter doping increases the width of the baseemitter, space-charge region in the emitter, reducing the $C_{j e}$ capacitance and further increasing the maximum speed.

The base region of the heterojunction bipolar transistors can be formed by growing a thin epitaxial layer of SiGe using ultra-high vacuum chemical vapor deposition (UHV/CVD). ${ }^{38}$ Since this is an epi layer, it takes on the crystal structure of the silicon in the substrate. Because the lattice constant for germanium is greater than that for silicon, the SiGe layer forms under a compressive strain, limiting the concentration of germanium and the thickness of the layer to avoid defect formation after subsequent high-temperature processing used at the back end of conventional technologies. ${ }^{39}$ In practice, with a base thickness of $0.1 \mu \mathrm{~m}$, the concentration of germanium is limited to about 15 percent so that the layer is unconditionally stable. ${ }^{40}$ With only a small concentration of germanium, the change in the band gap and the resulting shift in the potential barrier that limits reverse injection of holes into the emitter is small. However, the reverse injection is an exponential function of this barrier; therefore, even a small change in the barrier greatly reduces the reverse injection and results in these benefits.

In practice, the concentration of germanium in the base need not be constant. In particular, the UHV/CVD process is capable of increasing the concentration of germanium in the base from the emitter end to the collector end. This grading of the germanium concentration results in an electric field that helps electrons move across the base, further reducing $\tau_{F}$ and increasing $f_{T}$.

The heterojunction bipolar transistors described above can be included as the bipolar transistors in otherwise conventional BiCMOS processes. The key point is that the device processing sequence retains the well-established properties of silicon integrated-circuit processing because the average concentration of germanium in the base is small. ${ }^{39}$ This characteristic is important because it allows the new processing steps to be included as a simple addition to an existing process, reducing the cost of the new technology. For example, a BiCMOS process with a minimum drawn CMOS channel length of $0.3 \mu \mathrm{~m}$ and heterojunction bipolar transistors
with a $f_{T}$ of 50 GHz has been reported. ${ }^{40}$ The use of the heterojunction technology increases the $f_{T}$ by about a factor of two compared to a comparable homojunction technology.

## 2.13 Interconnect Delay

As the minimum feature size allowed in integrated-circuit technologies is reduced, the maximum operating speed and bandwidth have steadily increased. This trend stems partly from the reductions in the minimum base width of bipolar transistors and the minimum channel length of MOS transistors, which in turn increase the $f_{T}$ of these devices. While scaling has increased the speed of the transistors, however, it is also increasing the delay introduced by the interconnections to the point where it could soon limit the maximum speed of integrated circuits. ${ }^{41}$ This delay is increasing as the minimum feature size is reduced because the width of metal lines and spacing between them are both being reduced to increase the allowed density of interconnections. Decreasing the width of the lines increases the number of squares for a fixed length, increasing the resistance. Decreasing the spacing between the lines increases the lateral capacitance between lines. The delay is proportional to the product of the resistance and capacitance. To reduce the delay, alternative materials are being studied for use in integrated circuits.

First, copper is replacing aluminum in metal layers because copper reduces the resistivity of the interconnection by about 40 percent and is less susceptible to electromigration and stress migration than aluminum. Electromigration and stress migration are processes in which the material of a conductor moves slightly while it conducts current and is under tension, respectively. These processes can cause open circuits to appear in metal interconnects and are important failure mechanisms in integrated circuits. Unfortunately, however, copper can not simply be substituted for aluminum with the same fabrication process. Two key problems are that copper diffuses through silicon and silicon dioxide more quickly than aluminum, and copper is difficult to plasma etch. ${ }^{42}$ To overcome the diffusion problem, copper must be surrounded by a thin film of another metal that can endure high-temperature processing with little movement. To overcome the etch problem, a damascene process has been developed. ${ }^{43}$ In this process, a layer of interconnection is formed by first depositing a layer of oxide. Then the interconnect pattern is etched into the oxide, and the wafer is uniformly coated by a thin diffusion-resistant layer and then copper. The wafer is then polished by a chemical-mechanical process until the surface of the oxide is reached, which leaves the copper in the cavities etched into the oxide. A key advantage of this process is that it results in a planar structure after each level of metalization.

Also, low-permittivity dielectrics are being studied to replace silicon dioxide to reduce the interconnect capacitance. The dielectric constant of silicon dioxide is 3.9 times more than for air. For relative dielectric constants between about 2.5 and 3.0, polymers have been studied. For relative dielectric constants below about 2.0, the proposed materials include foams and gels, which include air. ${ }^{42}$ Other important requirements of low-permittivity dielectric materials include low leakage, high breakdown voltage, high thermal conductivity, stability under hightemperature processing, and adhesion to the metal layers. ${ }^{41}$ The search for a replacement for silicon dioxide is difficult because it is an excellent dielectric in all these ways.

## 2.14 Economics of Integrated-Circuit Fabrication

The principal reason for the growing pervasiveness of integrated circuits in systems of all types is the reduction in cost attainable through integrated-circuit fabrication. Proper utilization of the technology to achieve this cost reduction requires an understanding of the factors influencing
the cost of an integrated circuit in completed, packaged form. In this section, we consider these factors.

### 2.14.1 Yield Considerations in Integrated-Circuit Fabrication

As pointed out earlier in this chapter, integrated circuits are batch-fabricated on single wafers, each containing up to several thousand separate but identical circuits. At the end of the processing sequence, the individual circuits on the wafer are probed and tested prior to the breaking up of the wafer into individual dice. The percentage of the circuits that are electrically functional and within specifications at this point is termed the wafer-sort yield $Y_{w s}$ and is usually in the range of 10 percent to 90 percent. The nonfunctional units can result from a number of factors, but one major source of yield loss is point defects of various kinds that occur during the photoresist and diffusion operations. These defects can result from mask defects, pinholes in the photoresist, airborne particles that fall on the surface of the wafer, crystalline defects in the epitaxial layer, and so on. If such a defect occurs in the active region on one of the transistors or resistors making up the circuit, a nonfunctional unit usually results. The frequency of occurrence per unit of wafer area of such defects is usually dependent primarily on the particular fabrication process used and not on the particular circuit being fabricated. Generally speaking, the more mask steps and diffusion operations that the wafer is subjected to, the higher will be the density of defects on the surface of the finished wafer.

The existence of these defects limits the size of the circuit that can be economically fabricated on a single die. Consider the two cases illustrated in Fig. 2.67, where two identical wafers with the same defect locations have been used to fabricate circuits of different area. Although the defect locations in both cases are the same, the wafer-sort yield of the large die would be zero. When the die size is cut to one-fourth of the original size, the wafer sort yield is 62 percent. This conceptual example illustrates the effect of die size on wafer-sort yield. Quantitatively, the expected yield for a given die size is a strong function of the complexity of the process, the nature of the individual steps in the process, and perhaps, most importantly, the maturity and degree of development of the process as a whole and the individual steps within it. Since the inception of the planar process, a steady reduction in defect densities has occurred as a result of improved lithography, increased use of low-temperature processing steps such as ion implantation, improved manufacturing environmental control, and so forth. Three typical curves derived from yield data on bipolar and MOS processes are shown in Fig. 2.68. These are representative of yields for processes ranging from a very complex process with many yield-reducing steps to a very simple process carried out in an advanced VLSI fabrication facility. Also, the yield curves can be raised or lowered by more conservative design rules, and other factors. Uncontrolled factors such as testing problems and design problems in the circuit can cause results for a particular integrated circuit to deviate widely from these curves, but still the overall trend is useful.
image_name:Figure 2.67
description:The image labeled "Figure 2.67" illustrates the conceptual effect of die size on yield through two diagrams.

**Left Diagram:**
- The diagram is a larger rectangle divided into four equal sections.
- There are several black dots scattered across the sections, labeled as "Defects."
- The yield, denoted as \( Y_{ws} \), is calculated to be 0, indicating no successful yield due to the presence of defects in each section.

**Right Diagram:**
- This diagram is a larger rectangle divided into sixteen equal sections.
- Black dots are again scattered across these sections, representing defects.
- The yield, \( Y_{ws} \), is shown as \( \frac{10}{16} = 62\% \), indicating that despite the presence of defects, some sections are defect-free, leading to a higher yield.

The image conceptually demonstrates how increasing the number of sections (or reducing the die size) can lead to a higher yield by reducing the impact of defects on the overall process.
image_name:Figure 2.68
description:The image consists of two diagrams illustrating the effect of defects on yield in semiconductor manufacturing processes.

1. **Left Diagram:**
- This diagram shows a large die divided into four sections, each representing a part of the die.
- There are five black dots labeled as "Defects," indicating the location of defects within the die.
- Due to the placement of defects, each section of the die contains at least one defect, resulting in a yield of zero for this configuration, denoted as \( Y_{ws} = 0 \).

2. **Right Diagram:**
- This diagram shows a smaller die divided into sixteen sections.
- There are five black dots representing defects, similar to the left diagram.
- In this configuration, only six sections are affected by defects, leaving ten sections defect-free.
- The yield is calculated as the ratio of defect-free sections to the total number of sections, resulting in a yield of 62%, expressed as \( Y_{ws} = \frac{10}{16} = 62\% \).

Figure 2.67 Conceptual example of the effect of die size on yield.
image_name:Figure 2.68
description:The graph in Figure 2.68 is a plot showing the relationship between yield and die size for three different processes. This is a two-dimensional graph with a logarithmic scale on both axes. The x-axis represents the die size in units of mil squared (mil² × 10³), ranging from 10 to 100. The y-axis represents the yield percentage \( Y_{ws} \), ranging from 1% to 100%.

Overall Behavior and Trends:
The graph displays three distinct curves, labeled as Process A, Process B, and Process C. Each curve represents a different manufacturing process:
- **Process A**: This curve is the highest and shows the most efficient yield across various die sizes. It starts at 100% yield for the smallest die size and gradually decreases as the die size increases.
- **Process B**: This curve lies below Process A, indicating a less efficient yield. It also starts at a high yield for smaller die sizes but declines more sharply compared to Process A.
- **Process C**: This is the lowest curve, indicating the least efficient yield. It starts with a lower initial yield and declines significantly as die size increases.

Key Features and Technical Details:
- All three curves show a negative correlation between die size and yield; as the die size increases, the yield decreases.
- The decline in yield is more pronounced for processes with lower initial efficiency (Process B and C).
- The graph clearly illustrates the impact of die size on yield, with larger die sizes resulting in lower yields across all processes.

Annotations and Specific Data Points:
- The graph is marked with gridlines to help identify specific data points.
- Key intersections with gridlines indicate approximate yields for given die sizes, helping to compare the efficiency of the processes visually.

This graph effectively demonstrates how different manufacturing processes perform across varying die sizes, highlighting the trade-offs between die size and yield efficiency.

Figure 2.68 Typically observed yield versus die size for the three different processes, ranging from a very simple, well-developed process (curve $A$ ), to a very complex process with many yieldreducing steps (curve $C$ ).

In addition to affecting yield, the die size also affects the total number of dice that can be fabricated on a wafer of a given size. The total number of usable dice on the wafer, called the gross die per wafer $N$, is plotted in Fig. 2.69 as a function of die size for several wafer sizes. The product of the gross die per wafer and the wafer-sort yield gives the net good die per wafer, plotted in Fig. 2.70 for the yield curve of Fig. 2.68, assuming a 4 -inch wafer.
image_name:Figure 2.69 Gross die per wafer for 4-in., 8-in., and 12-in. wafers.
description:The graph in Figure 2.69 is a log-log plot representing the relationship between the gross die per wafer and the die size for wafers of different diameters (4-inch, 8-inch, and 12-inch).

1. **Type of Graph and Function:**
- This is a log-log plot, which is typically used to display data that covers a wide range of values.

2. **Axes Labels and Units:**
- The x-axis is labeled "Die size" and is measured in square mils (mil²), ranging from 10³ to 10⁷.
- The y-axis is labeled "Gross die per wafer" and ranges from 10 to 100,000.

3. **Overall Behavior and Trends:**
- The graph shows a decreasing trend for gross die per wafer as the die size increases.
- Each line on the graph represents a different wafer diameter, with larger wafers supporting more gross die per wafer for a given die size.

4. **Key Features and Technical Details:**
- Three lines are plotted, each corresponding to a different wafer diameter:
- The topmost line represents a 12-inch wafer.
- The middle line represents an 8-inch wafer.
- The bottom line represents a 4-inch wafer.
- All three lines have a similar slope, indicating a consistent rate of decrease in gross die per wafer with increasing die size across different wafer sizes.

5. **Annotations and Specific Data Points:**
- The lines are labeled according to the wafer diameter they represent.
- Gridlines are present, aiding in the estimation of values at specific points on the graph.

Overall, the graph effectively shows how the gross number of dies per wafer decreases as the die size increases, with larger wafers accommodating more dies for any given die size.

Figure 2.69 Gross die per wafer for 4-in., 8-in., and 12-in. wafers.
image_name:Figure 2.70
description:Figure 2.70 illustrates a log-log plot depicting the relationship between die size and the net good die per wafer for three different processes labeled as Process A, Process B, and Process C. The graph is designed to show how the number of good die per wafer changes with varying die sizes, assuming a 4-inch wafer, and can be scaled for other wafer sizes by adjusting the vertical axis proportionally to the wafer area.

1. **Type of Graph and Function:**
- This is a log-log plot, which is useful for displaying data that covers several orders of magnitude on both axes.

2. **Axes Labels and Units:**
- The x-axis represents the "Die size" measured in units of mil² × 10³.
- The y-axis represents the "Net good die/wafer," denoted as \( Y_{WNS} \).
- Both axes use a logarithmic scale, which is appropriate for the wide range of values.

3. **Overall Behavior and Trends:**
- Each curve demonstrates a decreasing trend, indicating that as the die size increases, the number of net good die per wafer decreases.
- The curves are positioned from top to bottom as Process A, Process B, and Process C, showing that Process A yields the highest number of good die per wafer for a given die size, followed by Process B, and then Process C.

4. **Key Features and Technical Details:**
- The graph includes gridlines that help estimate values at specific points, enhancing the readability and usability of the plot.
- The curves appear to follow a power-law distribution, typical for such manufacturing processes, where the number of good die decreases exponentially with increasing die size.

5. **Annotations and Specific Data Points:**
- Each curve is clearly labeled with the process it represents (A, B, or C), allowing for easy comparison between the different processes.
- The graph does not provide specific numerical data points but allows for estimation based on the gridlines and logarithmic scaling.

Overall, Figure 2.70 effectively communicates the impact of die size on the yield of good die per wafer across different manufacturing processes, with Process A being the most efficient and Process C the least efficient for smaller die sizes.

Figure 2.70 Net good die per wafer for the three processes in Fig. 2.66, assuming a 4-in. wafer. The same curve can be obtained approximately for other wafer sizes by simply scaling the vertical axis by a factor equal to the wafer area.

Once the wafer has undergone the wafer-probe test, it is separated into individual dice by sawing or scribing and breaking. The dice are visually inspected, sorted, and readied for assembly into packages. This step is termed die fab, and some loss of good dice occurs in the process. Of the original electrically good dice on the wafer, some will be lost in the die fab process due to breakage and scratching of the surface. The ratio of the electrically good dice following die fab to the number of electrically good dice on the wafer before die fab is called the die fab yield $Y_{d f}$. The good dice are then inserted in a package, and the electrical connections to each die are made with bonding wires to the pins on the package. The packaged circuits then undergo a final test, and some loss of functional units usually occurs because of improper bonding and handling losses. The ratio of the number of good units at final test to the number of good dice into assembly is called the final test yield $Y_{f t}$.

### 2.14.2 Cost Considerations in Integrated-Circuit Fabrication

The principal direct costs to the manufacturer can be divided into two categories: those associated with fabricating and testing the wafer, called the wafer fab cost $C_{w}$, and those associated with packaging and final testing the individual dice, called the packaging cost $C_{p}$. If we consider the costs incurred by the complete fabrication of one wafer of dice, we first have the wafer cost itself $C_{w}$. The number of electrically good dice that are packaged from the wafer is $N Y_{w s} Y_{d f}$. The total cost $C_{t}$ incurred once these units have been packaged and tested is

$$
\begin{equation*}
C_{t}=C_{w}+C_{p} N Y_{w s} Y_{d f} \tag{2.54}
\end{equation*}
$$

The total number of good finished units $N_{g}$ is

$$
\begin{equation*}
N_{g}=N Y_{w s} Y_{d f} Y_{f t} \tag{2.55}
\end{equation*}
$$

Thus the cost per unit is

$$
\begin{equation*}
C=\frac{C_{t}}{N_{g}}=\frac{C_{w}}{N Y_{w s} Y_{d f} Y_{f t}}+\frac{C_{p}}{Y_{f t}} \tag{2.56}
\end{equation*}
$$

The first term in the cost expression is wafer fab cost, while the second is associated with assembly and final testing. This expression can be used to calculate the direct cost of the finished product to the manufacturer as shown in the following example.

#### EXAMPLE

Plot the direct fabrication cost as a function of die size for the following two sets of assumptions.
(a) Wafer-fab cost of $\$ 75.00$, packaging and testing costs per die of $\$ 0.06$, a die-fab yield of 0.9 , and a final-test yield of 0.9. Assume yield curve $B$ in Fig. 2.68. This set of conditions might characterize an operational amplifier manufactured on a medium-complexity bipolar process and packaged in an inexpensive 8 or 14 lead package.

From (2.56),

$$
\begin{equation*}
C=\frac{\$ 75.00}{\left(N Y_{w s}\right)(0.81)}+\frac{0.06}{0.9}=\frac{\$ 92.59}{N Y_{w s}}+0.066 \tag{2.57}
\end{equation*}
$$

This cost is plotted versus die size in Fig. 2.71a.
(b) A wafer-fab cost of $\$ 100.00$, packaging and testing costs of $\$ 1.00$, die-fab yield of 0.9 , and final-test yield of 0.8 . Assume yield curve $A$ in Fig. 2.68. This might characterize a complex analog/digital integrated circuit, utilizing an advanced CMOS process and packaged in a large, multilead package. Again, from (2.56),

$$
\begin{equation*}
C=\frac{\$ 100.00}{\left(N Y_{w s}\right)(0.72)}+\frac{\$ 1.00}{0.8}=\frac{\$ 138.89}{N Y_{w s}}+\$ 1.25 \tag{2.58}
\end{equation*}
$$

This cost is plotted versus die size in Fig. 2.71b.
image_name:Figure 2.71 (b)
description:The graph in Figure 2.71 (b) is a cost curve illustrating the relationship between the cost of a packaged unit and the die size. It is plotted on a two-dimensional Cartesian plane.

1. **Type of Graph and Function:**
- This is a cost versus die size graph.

2. **Axes Labels and Units:**
- The horizontal axis (x-axis) represents the die size in square mils (mil² × 10³).
- The vertical axis (y-axis) represents the cost of the packaged unit in dollars ($).
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The graph shows a curve that starts near the bottom left and rises steeply as it moves to the right.
- Initially, at small die sizes, the cost is low and increases slowly.
- As the die size increases, the cost rises more steeply, indicating an exponential or quadratic trend.

4. **Key Features and Technical Details:**
- The curve is labeled as the "4-inch wafer yield curve B."
- There are two notable horizontal lines: one at approximately $0.50 indicating the "Package cost limited" region and another at $1.00 indicating the "Die cost limited" region.
- The transition from package cost limited to die cost limited occurs as the die size increases, reflecting the shift in cost dominance from packaging to die fabrication.

5. **Annotations and Specific Data Points:**
- The graph is annotated with labels indicating the regions where packaging costs dominate versus where die costs dominate.
- There are no specific numerical values marked on the curve itself, but the annotations provide context for interpreting the cost behavior relative to die size.

(a)

Figure 2.71 (a) Cost curve for example $a$.
image_name:Figure 2.71 (a)
description:The graph in Figure 2.71 (a) is a cost curve for a 4-inch wafer yield, labeled as curve A. It is a line graph that plots the relationship between the finished product cost and the die size.

1. **Type of Graph and Function:**
- This is a line graph representing a cost curve.

2. **Axes Labels and Units:**
- The x-axis represents the die size in units of mil² × 10³, ranging from 0 to 80.
- The y-axis represents the finished product cost in dollars, ranging from $1.00 to $10.00.

3. **Overall Behavior and Trends:**
- The graph shows an upward trend, indicating that the finished product cost increases as the die size increases.
- Initially, the curve is relatively flat, suggesting that the cost is less sensitive to changes in die size for smaller dies.
- As the die size increases beyond a certain point, the curve steepens, indicating a more significant increase in cost with increasing die size.

4. **Key Features and Technical Details:**
- The curve is divided into two annotated regions: "Package cost limited" and "Die cost limited."
- In the "Package cost limited" region, the cost is largely influenced by packaging expenses, which dominate for smaller die sizes.
- In the "Die cost limited" region, the cost is driven by die fabrication expenses, which become more significant for larger die sizes.

5. **Annotations and Specific Data Points:**
- The graph is annotated with labels that indicate the transition from packaging cost dominance to die cost dominance as the die size increases.
- There are no specific numerical values marked on the curve itself, but the annotations provide context for interpreting the cost behavior relative to die size.

(b)

Figure 2.71 (b) Cost curve for example $b$.

This example shows that most of the cost comes from packaging and testing for small die sizes, whereas most of the cost comes from wafer-fab costs for large die sizes. This relationship is made clearer by considering the cost of the integrated circuit in terms of cost per unit area of silicon in the finished product, as illustrated in Fig. 2.72 for the examples previously given. These curves plot the ratio of the finished-product cost to the number of square mils of silicon on the die. The minimum cost per unit area of silicon results midway between the packagecost and die-cost limited regions for each example. Thus the fabrication of excessively large
image_name:Figure 2.72
description:The graph in Figure 2.72 is a plot showing the cost of the finished product in terms of cost per unit area of silicon for two different examples labeled as 'Example a' and 'Example b'. The graph is a two-dimensional plot with the x-axis representing the 'Die area' measured in thousands of square mils (mil² x 10³) and the y-axis representing the 'Cost per 10 k mil² of Si area in finished product', measured in dollars ($).

### Type of Graph and Function:
This is a cost versus area graph, typically used in economic analyses of manufacturing processes.

Axes Labels and Units:
- **X-axis:** Die area in mil² x 10³, ranging from 0 to 60.
- **Y-axis:** Cost per 10 k mil² of Si area, ranging from $0.10 to $0.90.

Overall Behavior and Trends:
- **Example a:** The cost initially decreases as the die area increases, reaching a minimum point, and then starts increasing again. This indicates an optimal die size at which the cost per unit area is minimized before costs rise due to increased die size.
- **Example b:** Shows a similar trend but with a different minimum point, suggesting different economic characteristics or process efficiencies.

Key Features and Technical Details:
- **Example a:** The minimum cost occurs at a smaller die area compared to Example b, indicating that the process or packaging costs are more favorable at smaller die sizes.
- **Example b:** The minimum cost occurs at a larger die area, suggesting a higher yield or efficiency at larger die sizes, possibly due to the process used (referred to as process A).

Annotations and Specific Data Points:
- The graph is annotated with labels indicating regions where costs are limited by packaging or die costs. For Example a, the cost is initially package cost limited and then becomes die cost limited as the die size increases.
- For Example b, similar annotations show transitions from package cost limited to die cost limited regions, but at larger die sizes compared to Example a.

Figure 2.72 Cost of finished product in terms of cost per unit of silicon area for the two examples. Because the package and testing costs are lower in example $a$, the minimum cost point falls at a much smaller die size. The cost per unit of silicon area at large die sizes is smaller for example $b$ because process $A$ gives higher yield at large die sizes.
or small dice is uneconomical in terms of utilizing the silicon die area at minimum cost. The significance of these curves is that, for example, if a complex analog/digital system, characterized by example $b$ in Fig. 2.72 with a total silicon area of 80,000 square mils is to be fabricated in silicon, it probably would be most economical to build the system on two chips rather than on a single chip. This decision would also be strongly affected by other factors such as the increase in the number of total package pins required for the two chips to be interconnected, the effect on performance of the required interconnections, and the additional printed circuit board space required for additional packages. The shape of the cost curves is also a strong function of the package cost, test cost of the individual product, yield curve for the particular process, and so forth.

The preceding analysis concerned only the direct costs to the manufacturer of the fabrication of the finished product; the actual selling price is much higher and reflects additional research and development, engineering, and selling costs. Many of these costs are fixed, however, so that the selling price of a particular integrated circuit tends to vary inversely with the quantity of the circuits sold by the manufacturer.

## APPENDIX

### A.2.1 SPICE MODEL-PARAMETER FILES

In this section, SPICE model-parameter symbols are compared with the symbols employed in the text for commonly used quantities.

|  |  | Bipolar Transistor Parameters |
| :--- | :---: | :--- |
| SPICE |  |  |
| Symbol | Text Symbol | Description |
| IS | $I_{S}$ | Transport saturation current |
| BF | $\beta_{F}$ | Maximum forward current gain |
| BR | $\beta_{R}$ | Maximum reverse current gain |
| VAF | $V_{A}$ | Forward Early voltage |
| RB | $r_{b}$ | Base series resistance |
| RE | $r_{e x}$ | Emitter series resistance |
| RC | $r_{c}$ | Collector series resistance |
| TF | $\tau_{F}$ | Forward transit time |
| TR | $\tau_{R}$ | Reverse transit time |
| CJE | $C_{j e 0}$ | Zero-bias base-emitter depletion capacitance |
| VJE | $\psi_{0 e}$ | Base-emitter junction built-in potential |
| MJE | $n_{e}$ | Base-emitter junction-capacitance exponent |
| CJC | $C_{\mu 0}$ | Zero-bias base-collector depletion capacitance |
| VJC | $\psi_{0 c}$ | Base-collector junction built-in potential |
| MJC | $n_{c}$ | Base-collector junction-capacitance exponent |
| CJS | $C_{C S 0}$ | Zero-bias collector-substrate depletion capacitance |
| VJS | $\psi_{0 s}$ | Collector-substrate junction built-in potential |
| MJS | $n_{s}$ | Collector-substrate junction-capacitance exponent |

Note: Depending on which version of SPICE is used, a separate diode may have to be included to model base-substrate capacitance in a lateral pnp transistor.

### MOSFET Parameters

| SPICE <br> Symbol | Text Symbol | Description |
| :---: | :---: | :---: |
| VTO | $V_{i}$ | Threshold voltage with zero source-substrate voltage |
| KP | $k^{\prime}=\mu C_{o x}$ | Transconductance parameter |
| GAMMA | $\gamma=\frac{\sqrt{2 q \epsilon N_{A}}}{C_{o x}}$ | Threshold voltage parameter |
| PHI | $2 \phi_{f}$ | Surface potential |
| LAMBDA | $\lambda=\frac{1}{L_{\mathrm{eff}}} \frac{d X_{d}}{d V_{D S}}$ | Channel-length modulation parameter |
| CGSO | $C_{\text {ol }}$ | Gate-source overlap capacitance per unit channel width |
| CGDO | $C_{\text {ol }}$ | Gate-drain overlap capacitance per unit channel width |
| CJ | $C 0$ | Zero-bias junction capacitance per unit area from source and drain bottom to bulk (substrate) |
| MJ | n | Source-bulk and drain-bulk junction capacitance exponent (grading coefficient) |
| CJSW | $C_{j s w 0}$ | Zero-bias junction capacitance per unit junction perimeter from source and drain sidewall (periphery) to bulk |
| MJSW | n | Source-bulk and drain-bulk sidewall junction capacitance exponent |
| PB | $\psi_{0}$ | Source-bulk and drain-bulk junction built-in potential |
| TOX | $t_{o x}$ | Oxide thickness |
| NSUB | $N_{A}, N_{D}$ | Substrate doping |
| NSS | $Q_{s s} / q$ | Surface-state density |
| XJ | $X_{j}$ | Source, drain junction depth |
| LD | $L_{d}$ | Source, drain lateral diffusion |
