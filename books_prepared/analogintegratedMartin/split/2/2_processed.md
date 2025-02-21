# 2. Processing and Layout

This chapter describes the steps and processes used in realizing modern integrated circuits with emphasis on CMOS processing. After processing is presented, circuit layout is covered. Layout is the design portion of integrated-circuit manufacturing, in which the geometry of circuit elements and wiring connections is defined. This process leads to the development of photographic masks used in manufacturing an integrated circuit. The concepts of design rules and their relationship to integrated circuits are emphasized. Next, circuit layout is related to the transistor models. Here, it is shown that once the layout is completed, the values of certain elements in the transistor models can be determined. This knowledge is necessary for accurate computer simulation of integrated circuits. It is also shown that, by using typical design rules, one can make reasonable assumptions to approximate transistor parasitic components before the layout has been done. Variability in device parameters is unavoidable and particularly problematic for analog circuits. These variations are modeled and their impact on analog circuits analyzed. Finally, analog layout issues are then discussed, including matching and noise considerations.

## 2.1 CMOS PROCESSING

In this section, the basic steps involved in processing a CMOS integrated circuit are presented. For illustrative purposes, we describe here an example n -well process with a p substrate and two layers of metal. Many of the possible variations during processing are also described, but we focus primarily on the basics which any analog designer should know. The processing of nanometer feature sizes can require many additional steps.

### 2.1.1 The Silicon Wafer

The first step in realizing an integrated circuit is to fabricate a defect-free, single-crystalline, lightly doped silicon wafer. To realize such a wafer, one starts by creating metallurgical-grade silicon through the use of a high-temperature chemical process in an electrode-arc furnace. Although metallurgical-grade silicon is about 98 percent pure, it has far too many impurities for use in realizing integrated circuits. Next, a silicon-containing gas is formed and then reduced. Pure silicon is precipitated onto thin rods of single-crystalline silicon. This deposited electronic-grade silicon is very pure but, unfortunately, it is also polycrystalline. To obtain single-crystalline silicon, the silicon is melted once again and allowed to cool. As it cools, a single-crystalline ingot is slowly pulled and turned from the molten silicon using the Czochralski method. The Czochralski method starts with a seed of single crystal silicon, and the pull rate and speed of rotation determine the diameter of the crystalline rod or ingot. Typical diameters are 10 to 30 cm (i.e., 4 to 12 inches) with lengths usually longer than 1 meter. Producing a silicon ingot can take several days.

Key Point: The first step in realizing an integrated circuit is to produce a single-crystalline silicon wafer from 10 to 30 cm in diameter and roughly 1 mm thick. The silicon is either lightly doped, or heavily doped with a thin lightly-doped epitaxial layer on top in which the transistors are made.

Normally, heavily doped silicon is added to the melt before the singlecrystalline ingot is pulled. After the doped silicon diffuses through the molten silicon, a more lightly doped silicon ingot results. In our example process, boron impurities would be added to produce a p -type ingot. The ingot is cut into wafers using a large diamond saw. A typical wafer might have a thickness of about 1 mm . After the ingot is sawed into wafers, each wafer is polished with $\mathrm{Al}_{2} \mathrm{O}_{3}$, chemically etched to remove mechanically damaged material, and then fine-polished again with $\mathrm{SiO}_{2}$ particles in an aqueous solution of NaOH . Very often, the company that produces the silicon wafers is not the same company that eventually patterns them into monolithic circuits.

There are two methods for establishing the background doping level of the surface silicon in which all of the transistors will be made. One is to simply control the boron impurity levels in the ingot to provide a $\mathrm{p}^{-}$wafer concentration of around $\mathrm{N}_{\mathrm{A}} \cong 2 \times 10^{21}$ donor $/ \mathrm{m}^{3}$. Such a doping level would give a resistivity of 10 to $20 \Omega \cdot \mathrm{~cm}$. The other method is to begin with a very heavily doped $\mathrm{p}^{++}$wafer with a low resistivity of around $0.01 \Omega \cdot \mathrm{~cm}$. Then, upon the surface of the $\mathrm{p}^{++}$wafer, a layer of $\mathrm{p}^{-}$silicon is grown with a higher resistivity of 5 to $20 \Omega \cdot \mathrm{~cm}$. All of the devices are fabricated within this top epitaxial layer, which may be from 2 to $20 \mu \mathrm{~m}$ thick. The use of an epitaxial layer provides more precise control over dopant concentrations while the $\mathrm{p}^{++}$substrate underneath provides a low-resistivity ground plane under the circuit helping to prevent latchup, described in Section 2.2.4. In either case, transistors are fabricated in $\mathrm{p}^{-}$silicon near the surface of the wafer.

### 2.1.2 Photolithography and Well Definition

Photolithography is a technique in which selected portions of a silicon wafer can be masked so that some type of processing step can be applied to the remaining areas. Although photolithography is used throughout the manufacture of an integrated circuit, here we describe this photographic process in the context of preparing the wafer for defining the well regions. ${ }^{1}$

Selective coverage for well definition is performed as follows. First, a glass mask, $\mathrm{M}_{1}$, is created, which defines where the well regions will be located. The glass mask is created by covering the mask in photographic materials and exposing it to an electron beam, or e beam, in the regions corresponding to the well locations. Such exposure results in the well regions on the glass mask turning opaque, or dark. As a result, the glass mask can be thought of as a negative of one layer of the microcircuit. In a typical microcircuit process, ten to twenty different masks might be required. The cost for these masks varies considerably depending upon the minimum feature sizes to be patterned on the microcircuit. For example, currently a set of masks for a $0.35-\mu \mathrm{m}$ CMOS process might cost roughly $\$ 30,000$, whereas the cost of a mask set for the most advanced modern processes approaches $\$ 1,000,000$. Because a high degree of precision is required in manufacturing these masks, often (but not always) a company other than the integrated circuit processing company makes the masks. The creation of the opaque regions of the mask by the electron beam is controlled by a computer dependent on the contents of a database. The database required for the e beam is derived from the layout database produced by the designer, using a computer-aided design (CAD) software program.

The first step in masking the surface of the wafer is to thermally grow a thin layer of silicon-dioxide $\left(\mathrm{SiO}_{2}\right)$ to protect the surface of the microcircuit. Details of this step are discussed later. On top of the $\mathrm{SiO}_{2}$, a negative photoresist, $\mathrm{PR}_{1}$, is evenly applied to a thickness of around $1 \mu \mathrm{~m}$ while spinning the microcircuit. Photoresist is a lightsensitive polymer (similar to latex). In the next step, the mask, $\mathrm{M}_{1}$, is placed in close proximity to the wafer, and ultraviolet light is projected through the mask onto the photoresist. Wherever the light strikes, the polymers crosslink, or polymerize. This change makes these regions insoluble to an organic solvent. This step is shown in Fig. 2.1

[^7]Ultraviolet light
image_name:Fig. 2.1
description:The image labeled "Fig. 2.1" illustrates the process of selectively hardening a region of photoresist using a glass mask in microcircuit fabrication. The diagram shows a cross-sectional view of the components involved in this process.

1. **Identification of Components and Structure:**
- **Glass Mask:** The top layer is labeled as a glass mask, which contains both opaque and translucent regions. The opaque regions block ultraviolet (UV) light, while the translucent regions allow it to pass through.
- **Photoresist Layer (PR1):** Beneath the glass mask is a layer of photoresist, which is sensitive to UV light. This layer is where the selective hardening occurs.
- **Silicon Dioxide (SiO2) Layer:** Below the photoresist is a layer of silicon dioxide, which is part of the substrate structure.
- **Substrate (p-):** The bottom layer is labeled as p-, indicating a type of semiconductor substrate.

2. **Connections and Interactions:**
- **UV Light Exposure:** Arrows represent the path of UV light, which passes through the translucent regions of the glass mask and strikes the photoresist layer. The areas of the photoresist exposed to UV light become hardened due to polymerization.
- **Opaque Regions:** The opaque regions of the mask prevent UV light from reaching certain parts of the photoresist, keeping them soluble to the organic solvent used later.

3. **Labels, Annotations, and Key Features:**
- The diagram includes labels such as "Opaque region," "Translucent region," "Glass mask," "Hardened photoresist, PR1," and "SiO2," which help in identifying and understanding the different parts of the process.
- The arrows depicting UV light direction and interaction with the photoresist are key to understanding how selective hardening is achieved.

Overall, this diagram effectively conveys the concept of using a glass mask to selectively harden specific regions of photoresist on a microcircuit wafer by controlling UV light exposure.

Fig. 2.1 Se-lectively hardening a region of photoresist using a glass mask.
The regions where the mask was opaque (i.e., the well regions) are not exposed. The photoresist is removed in these areas using an organic solvent. Next, the remaining photoresist is baked to harden it. After the photoresist in the well regions is removed, the uncovered $\mathrm{SiO}_{2}$ may also be removed using an acid etch. (However, in some processes where this layer is very thin, it may not be removed.) In the next step, the dopants needed to form the well are introduced into the silicon using either diffusion or ion implantation (directly through the thin oxide, in cases where it has not been removed).

The procedure just described involves a negative photor esist, where the exposed photoresist remains after the masking. There are also positive photoresists, in which the exposed photoresist is dissolved by the organic solvents. In this case, the photoresist remains where the mask was opaque. By using both positive and negative resists, a single mask can sometimes be used for two steps-first, to protect one region and implant the complementary region and second, to protect the complementary region and implant the original region.

The feature sizes that may be patterned using photolithography are influenced by the wavelength of light used. When the integrated circuit features are smaller than the wavelength of light (currently 193-nm ultraviolet light is used),

Key Point: Most features on integrated circuits are patterned using photolithography whereby light is passed through a mask to cast patterns onto the underlying silicon wafer, ultimately defining the circuit's physical features such as transistor sizes and wiring.
the wave nature of light results in patterns on the photoresist that do not precisely match those of the mask. Fortunately, these effects can be partially compensated for by modifying the mask pattern so that the resulting geometries more closely match those intended by the designer. This technique is referred to as "optical proximity correction" and is a common practice to realize feature sizes below 100 nm . Further improvements have been made by immersing the photolithography in a liquid bath. Doing so changes the path of light resulting in improved resolution and improved tolerance to unevenness of the substrate surface. Efforts are ongoing to reduce the minimum feature sizes that may be patterned by using shorter wavelengths for photolithography (extreme ultraviolet light or even X-rays).

### 2.1.3 Diffusion and Ion Implantation

After the photoresist over the well region has been removed, the next step is to introduce dopants through the opening where the well region will be located. There are two approaches for introducing these dopants: diffusion and ion implantation.

In both implantation methods, usually the $\mathrm{SiO}_{2}$ in the well region will first be removed using an acid etch. Next, the remaining hardened photoresist is stripped using acetone. This leaves $\mathrm{SiO}_{2}$ that was protected by the hardened photoresist to mask all of the nonwell (i.e., substrate) regions.

In diffusion implantation, the wafers are placed in a quartz tube inside a heated furnace. A gas containing the dopant is introduced into the tube. In the case of forming an n well, the dopant in the gas would probably be phosphorus. Arsenic could also be used, but it takes a much longer time to diffuse. The high temperature of the diffusion furnace, typically 900 to $1100^{\circ} \mathrm{C}$, causes the dopants to diffuse into the silicon both vertically and horizontally. The dopant concentration will be greatest at the surface and will decrease following a Gaussian profile further into the silicon. If a $p$ well had been desired, then boron would have been used as the dopant. The resulting cross section, after diffusing the n well, is shown in Fig. 2.2.

An alternative technique for introducing dopants into the silicon wafer is ion implantation. This technique has now largely replaced diffusion because it allows more independent control over the dopant concentration and the thickness of the doped region. In ion implantation, dopants are introduced as ions into the wafer, as shown in the functional representation of an ion implanter in Fig. 2.3 The ions are generated by bombarding a gas with electrons from an arc-discharge or cold-cathode source. The ions are then focused and sent through a mass separator. This mass separator bends the ion beam and sends it through a narrow slit. Since only ions of a specific mass pass through the slit, the beam is purified. Next, the beam is again focused and accelerated to between 10 keV and 1 MeV . The ion current might range from $10 \mu \mathrm{~A}$ to 2 mA . The deflection plates sweep the beam across the wafer (which is often rotated at the same time) and the acceleration potential controls how deeply the ions are implanted. The beam current and time of implantation determine the amount of dosage. Thus, depth and dosage are controlled independently. Two problems that occur with ion implantation are lattice damage and a narrow doping profile. The lattice damage is due to nuclear collisions that result in the displacement of substrate atoms. The narrow profile results in a heavy concentration over a narrow distance, as is shown in Fig. 2.4. For example, arsenic ions with an acceleration voltage of 100 keV might penetrate approximately $0.06 \mu \mathrm{~m}$ into the silicon, with the majority of ions being at $0.06 \mu \mathrm{~m} \pm 0.02 \mu \mathrm{~m}$. Both of these problems are largely solved by annealing.
image_name:Fig. 2.2
description:The image labeled "Fig. 2.2" illustrates the process of forming an n-well in a silicon substrate using phosphorus diffusion. The diagram is a cross-sectional view showing several key components and materials involved in the process.

1. **Components and Structure:**
- The image shows a silicon substrate with a p-type base, labeled as "p⁻".
- An n-well is depicted within the silicon substrate, indicating an area where phosphorus atoms have been diffused to create an n-type region.
- Above the silicon substrate, there is a layer of silicon dioxide (SiO₂), shown as a hatched area. This layer acts as a mask, with openings allowing diffusion in specific areas.

2. **Connections and Interactions:**
- A gas containing phosphorus, specifically a mixture of phosphine (2PH₃) and oxygen (4O₂), is introduced from above. The gas diffuses through the opening in the SiO₂ layer into the silicon substrate.
- The diffusion of phosphorus atoms into the silicon forms the n-well, altering the electrical properties of that region by introducing excess electrons (n-type doping).

3. **Labels, Annotations, and Key Features:**
- The gas mixture is labeled "Gas containing phosphorus" with the chemical formula "2PH₃ + 4O₂".
- The SiO₂ layer is clearly marked, indicating its role as a diffusion mask.
- The n-well region is labeled, highlighting the area of n-type doping within the p-type substrate.

This diagram is a simplified representation of the diffusion process used in semiconductor fabrication to create doped regions within a silicon wafer.

Fig. 2.2 Forming an $n$ well by diffusing phosphorus from a gas into the silicon, through the opening in the $\mathrm{SiO}_{2}$.

Vertical and horizontal deflection plates
image_name:Fig. 2.3 An ion-implantation system
description:The ion-implantation system diagram, labeled as Fig. 2.3, illustrates a sequential process used in semiconductor fabrication for introducing ions into a silicon wafer. This process involves several key components and steps:

1. **Ion Source**: The process begins with the ion source, where ions are generated. This component is crucial for producing the charged particles needed for implantation.

2. **Focusing Lens**: The ions from the source are directed through a focusing lens. This lens is responsible for converging the ion beam to ensure it is directed accurately through the subsequent stages.

3. **Separating Slit**: After focusing, the ion beam passes through a separating slit. This component serves to filter and direct the ions, ensuring that only the desired ions continue through the system.

4. **Second Focusing Lens**: Another focusing lens further refines the ion beam, enhancing its precision and ensuring it remains tightly focused as it moves forward.

5. **Acceleration Plates**: The focused ion beam then encounters acceleration plates. These plates apply an electric field that accelerates the ions, increasing their energy and velocity as they proceed through the system.

6. **Deflection Plates**: After acceleration, the ion beam passes between deflection plates. These plates can adjust the path of the ion beam, allowing for precise control over its trajectory toward the target.

7. **Target**: The final component is the target, typically a silicon wafer, where the ions are implanted. The ion beam impacts the target, embedding the ions into the wafer's surface to alter its electrical properties.

Overall, the ion-implantation system is designed to accurately and precisely introduce dopants into a semiconductor substrate, which is a critical step in the fabrication of integrated circuits. The arrangement and function of each component ensure that the ion beam is properly generated, focused, accelerated, and directed to achieve the desired implantation profile.

Fig. 2.3 An ion-implantation system.

Annealing is a step in which the wafer is heated to about $1000^{\circ} \mathrm{C}$, perhaps for 15 to 30 minutes, and then allowed to cool slowly. This heating stage thermally vibrates the atoms, which allows the bonds to reform. Annealing also broadens the dopant concentration profile, making the doping levels more uniform, as shown in Fig. 2.4. It should be noted that annealing is performed only once during processing, after all the implantation steps have been performed but before any metal layers have been created. ${ }^{2}$

For n-type dopants, arsenic is used for shallow implantations, such as the source or drain junctions. Phosphorus might be used for the well. Boron is always used to form the p regions.

Although more expensive, ion implantation has been largely replacing diffusion for forming n and p regions because of its greater control over doping levels. Another important advantage of ion implantation is the much smaller sideways diffusion, which allows devices to be more closely spaced and, more importantly for MOS transistors, minimizes the overlap between the gate-source or gate-drain regions.
image_name:Fig. 2.4 Dopant profiles after ion implantation both before and after annealing
description:The graph in Fig. 2.4 is a plot showing dopant profiles after ion implantation both before and after annealing. It is a line graph with the x-axis labeled "Depth into silicon wafer" and the y-axis labeled "Ion dopant concentration." The graph does not specify units for either axis, indicating a qualitative rather than quantitative analysis.

The graph features two curves: a solid line representing the dopant concentration before annealing and a dashed line representing the concentration after annealing.

Before annealing, the dopant concentration curve rises steeply from the surface of the silicon wafer, reaching a peak at a certain depth, and then gradually decreases. This suggests a high concentration of dopants near the surface that diminishes deeper into the wafer.

After annealing, the dashed curve shows a more spread out profile. The peak concentration is lower and occurs at a slightly greater depth compared to the pre-annealing curve. The overall shape is broader, indicating that annealing causes the dopants to diffuse further into the silicon, reducing the peak concentration but increasing the penetration depth.

This behavior is typical in semiconductor processing, where annealing helps to activate dopants and repair damage caused by ion implantation, resulting in a more uniform dopant distribution.

Fig. 2.4 Dopant profiles after ion implantation both before and after annealing.

[^8]In some modern processes, both p and n wells are created in which NMOS and PMOS devices will be fabricated, respectively. This is referred to as a twin-well process.

### 2.1.4 Chemical Vapor Deposition and Defining the Active Regions

The next few steps use the mask $\mathrm{M}_{2}$ to define where the transistors will be located and to make isolation structures between them. A thin layer of thermal $\mathrm{SiO}_{2}$ is first grown everywhere to protect the surface of the silicon lattice. Next, $\mathrm{Si}_{3} \mathrm{~N}_{4}$ is deposited everywhere during a gas-phase reaction in which energy is supplied by heat (at about $850^{\circ} \mathrm{C}$ ). This process is called chemical vapor deposition, or CVD. After this step, the photoresist $\mathrm{PR}_{2}$ is deposited, exposed through the mask, $\mathrm{M}_{2}$, dissolved, and hardened. Often, this step will be done using positive photoresist such that, wherever the mask $\mathrm{M}_{2}$ is not opaque, the photoresist will be softened. In other words, the photoresist is left intact after the organic dissolution step, under the opaque regions of the mask. These become the active device regions where the transistors will eventually be located, also sometimes referred to as the "oxide definition" (OD) regions because over these regions only a very thin gate-oxide will be made. The hardened photoresist is left on top of the $\mathrm{Si}_{3} \mathrm{~N}_{4}$ to protect it over the OD regions. Next, the $\mathrm{Si}_{3} \mathrm{~N}_{4}$, wherever it is not protected by the photoresist, is removed by etching it away with a hot phosphoric acid. $\mathrm{The}^{-1 \mathrm{SiO}_{2}}$ is then removed with a hydrofluoric acid etch. Finally, the remaining photoresist is chemically removed with a process that leaves the remaining $\mathrm{Si}_{3} \mathrm{~N}_{4}$ intact. The remaining $\mathrm{Si}_{3} \mathrm{~N}_{4}$ will act as a mask to protect the active regions while the isolation structures are being made.

These steps result in a thin layer of thermal $\mathrm{SiO}_{2}$, as well as a layer of silicon nitride $\left(\mathrm{Si}_{3} \mathrm{~N}_{4}\right)$, covering all active (OD) regions as shown in Fig. 2.5.

### 2.1.5 Transistor Isolation

Parasitic transistors are formed everywhere on a silicon die wherever a conductor appears above and between the junction regions of different transistors. If the electrical potential on a conductor should approach the threshold voltage of a parasitic transistor underneath it, undesired leakage currents may flow between transistors that are intended to be unconnected. In order to prevent this, extra processing is performed to ensure that these parasitic transistors can not conduct appreciable current. Two popular methods to isolate transistors are local oxidation of the silicon (LOCOS) and shallow-trench isolation (STI).
image_name:Fig. 2.5
description:The image labeled "Fig. 2.5" depicts a cross-sectional view of a silicon wafer after the oxide definition (OD) regions have been patterned, illustrating the Local Oxidation of Silicon (LOCOS) process.

1. **Identification of Components and Structure:**
- The diagram shows a silicon substrate with an "n well" region, which is a doped area intended to host transistors or other semiconductor devices.
- Above the n well, there are layers of silicon dioxide (SiO₂) and silicon nitride (Si₃N₄). The SiO₂ layer is shown as a thick, shaded region that acts as a field oxide, providing electrical isolation between different areas of the wafer.
- The Si₃N₄ layer is depicted as a thin, solid line on top of the SiO₂, serving as a mask during the oxidation process.

2. **Connections and Interactions:**
- The Si₃N₄ layer is used to define areas where oxidation should not occur, thereby controlling the growth of the SiO₂ layer.
- The interaction between the Si₃N₄ and SiO₂ layers is crucial for the LOCOS process, as the nitride layer prevents oxidation in specific regions, allowing for precise patterning of the oxide.

3. **Labels, Annotations, and Key Features:**
- The diagram includes labels for the Si₃N₄ and SiO₂ layers, as well as the n well region, providing clarity on the material composition and structure.
- The cross-section highlights the importance of the field oxide in isolating different components on the silicon wafer, which is essential for preventing leakage currents between transistors.

Overall, the image illustrates the LOCOS process, emphasizing the role of Si₃N₄ and SiO₂ in defining and isolating regions on a silicon wafer to prevent undesired electrical interactions.

$\mathrm{p}^{-}$

Fig. 2.5 The cross section of the wafer after the oxide definition (OD) regions are patterned.

#### Local Oxidation of Silicon (LOCOS)

LOCOS processing involves the implantation of additional dopants (filed-implants) between transistors to ensure any parasitic transistors have a very large threshold voltage, followed by the creation of very thick layers of $\mathrm{SiO}_{2}$ (field-oxide) above the field-implants.

First, the field-implants are introduced under where the field-oxide will be grown. For example, boron is implanted under the field-oxide everywhere except in the n well regions. This implant guarantees that the silicon under the field-oxide will never invert (or become n ) when a conductor over the field-oxide has a large voltage. For the field-oxide in the well regions, where p -channel transistors will eventually reside, an $n$-type implant such as arsenic (As) could be used. Often, it is not necessary to include field-implants under the field-oxide of the well regions because the heavier doping of the well (compared to that of the substrate) normally guarantees that the silicon will never invert under the field-oxide in these regions.

When implanting the field-implants in the substrate regions, it is necessary to first cover the wells with a protective photoresist, $\mathrm{PR}_{3}$, so the n -well regions do not receive the p implant. This can be done using the same mask, $\mathrm{M}_{1}$, that was originally used for implanting the n wells, but now a positive photoresist is used. This positive photoresist remains where the mask is opaque (i.e., dark), which corresponds to the well regions.

After the exposed photoresist has been dissolved, we now have the cross section shown in Fig. 2.6. Notice that at this step, all the active regions, where eventually the transistors will reside, are protected from the field implants by the $\mathrm{Si}_{3} \mathrm{~N}_{4}$ and $\mathrm{SiO}_{2}$. Additionally, the complete well regions are also protected by $\mathrm{PR}_{3}$. The fieldimplant will be a high-energy implant with a fairly high doping level. Before the field-oxide is grown, $\mathrm{PR}_{3}$ is removed, but the silicon-nitride-silicon-dioxide sandwich is left.

The next step is to grow the field-oxide, $\mathrm{SiO}_{2}$. There are two different ways that $\mathrm{SiO}_{2}$ can be grown. In a wet process, water vapor is introduced over the surface at a moderately high temperature. The water vapor diffuses into the silicon and, after some intermediate steps, reacts according to the formula

$$
\begin{equation*}
\mathrm{Si}+2 \mathrm{H}_{2} \mathrm{O} \rightarrow \mathrm{SiO}_{2}+2 \mathrm{H}_{2} \tag{2.1}
\end{equation*}
$$

In a dry process, oxygen is introduced over the wafer, normally at a slightly higher temperature than that used in the wet process, and reacts according to the formula

$$
\begin{equation*}
\mathrm{Si}+\mathrm{O}_{2} \rightarrow \mathrm{SiO}_{2} \tag{2.2}
\end{equation*}
$$

image_name:Fig. 2.6 The cross section when the field-implants are being formed in a LOCOS process.
description:The image labeled "Fig. 2.6 The cross section when the field-implants are being formed in a LOCOS process" depicts a cross-sectional view of a semiconductor wafer during the Local Oxidation of Silicon (LOCOS) process, specifically when field implants are being formed.

1. **Identification of Components and Structure:**
- **Si$_3$N$_4$ (Silicon Nitride) Layer:** A layer of silicon nitride is shown on top of the wafer, which helps in defining the areas where oxidation should occur. It acts as a mask to prevent oxidation in specific regions.
- **PR$_3$ (Photoresist):** A layer of photoresist is applied over the silicon nitride. This is used to pattern the nitride layer during photolithography.
- **n well:** The diagram shows an n-type well in the silicon substrate, indicating regions doped with n-type impurities.
- **SiO$_2$ (Silicon Dioxide):** This is the field oxide layer that is being formed in the LOCOS process.
- **Field-implants:** These are represented by shaded regions in the substrate where dopants (such as boron) are implanted to adjust the electrical properties of the silicon.

2. **Connections and Interactions:**
- The boron ions are shown being implanted into the substrate. The arrows indicate the direction of ion implantation, which is vertical into the silicon.
- The field-implants are located at specific regions to create isolation between different device areas on the silicon wafer.

3. **Labels, Annotations, and Key Features:**
- **Boron ions:** The diagram includes labels indicating the presence of boron ions, which are used as p-type dopants.
- **Field-implants:** Areas where the field-implants are located are marked, showing where the boron ions are being introduced.
- The diagram uses symbols such as plus signs to indicate the positive charge associated with the boron ions.

Overall, this cross-section illustrates the early stages of the LOCOS process, focusing on the formation of field-implants to provide electrical isolation in integrated circuits.

$\mathrm{p}^{-}$

Fig. 2.6 The cross section when the field-implants are being formed in a LOCOS process.
image_name:Fig. 2.6 The cross section when the field-implants are being formed in a LOCOS process.
description:The image depicts a cross-sectional view of a semiconductor structure during the formation of field-implants in a LOCOS (Local Oxidation of Silicon) process. This is a crucial step in integrated circuit fabrication aimed at providing electrical isolation.

1. **Identification of Components and Structure:**
- The diagram shows a substrate with an 'n well' region indicated. This is a doped area within the silicon substrate.
- The structure includes layers of silicon nitride (Si₃N₄) and silicon dioxide (SiO₂), which are essential in the LOCOS process.
- Field-oxide regions are shown as thicker, protruding sections above the substrate, illustrating where oxidation has occurred.
- The p⁺ field-implants are marked, indicating regions where boron ions have been introduced to create p-type regions for electrical isolation.

2. **Connections and Interactions:**
- The Si₃N₄ layer acts as a mask to prevent oxidation in certain areas, allowing for selective growth of the field-oxide.
- The SiO₂ layer is a thin oxide layer that exists beneath the nitride to aid in the oxidation process and protect the underlying silicon.
- The p⁺ field-implants are strategically placed to enhance the isolation properties by introducing positive charges into the substrate.

3. **Labels, Annotations, and Key Features:**
- The diagram is annotated with labels for Si₃N₄, SiO₂, field-oxide, and p⁺ field-implants, clearly marking each component.
- The n well is also labeled, showing the boundary of the doped region.
- Arrows are used to indicate the direction of the boron ion implantation and the areas affected by the oxidation process.

Overall, the diagram effectively illustrates the early stages of the LOCOS process, emphasizing the formation of field-implants and the role of various materials used to achieve electrical isolation.

$\mathrm{p}^{-}$

Fig. 2.7 The cross section after the field-oxide has been grown in a LOCOS process.

Since both of these processes occur at high temperatures, around 800 to $1200^{\circ} \mathrm{C}$, the oxide that results is sometimes called a thermal oxide.

The field oxide does not grow wherever CVD-deposited $\mathrm{Si}_{3} \mathrm{~N}_{4}$ remains, because the $\mathrm{Si}_{3} \mathrm{~N}_{4}$ is relatively inert to both water and oxygen. Wherever the process does occur, the volume increases because oxygen atoms have been added. Specifically, $\mathrm{SiO}_{2}$ takes up approximately 2.2 times the volume of the original silicon. This increase will cause the $\mathrm{SiO}_{2}$ to extend approximately 45 percent into, and 55 percent above, what previously was the surface of the silicon. The resulting cross section is shown in Fig. 2.7. Note that in our example process, the field-oxide in the substrate region has field-implants under it, whereas the field-oxide in the wells does not.

When growing thermal $\mathrm{SiO}_{2}$, the wet process is faster because $\mathrm{H}_{2} \mathrm{O}$ diffuses faster in silicon than $\mathrm{O}_{2}$ does, but the dry process results in denser, higher-quality $\mathrm{SiO}_{2}$ that is less porous. Sometimes, growing the field-oxide starts with a dry process, changes to a wet process, and finishes with a dry process. When thin layers of $\mathrm{SiO}_{2}$ are grown, as the next section describes, usually only a dry process is used.

LOCOS is the preferred method for transistor isolation when minimum feature sizes exceed $0.25 \mu \mathrm{~m}$. At smaller feature sizes the rounded corners of the field-oxide take up too much space and improved isolation processing is required.

#### Shallow-Trench Isolation (STI)

image_name:Fig. 2.8
description:The image labeled as Fig. 2.8 illustrates a cross-sectional view of a silicon wafer using shallow-trench isolation (STI) for transistor isolation. The diagram shows several key components and structures:

1. **Silicon Substrate:** The base layer is a p-type silicon substrate, indicated by the label 'p−'. This forms the foundation upon which other structures are built.

2. **N Well:** Within the p-type substrate, an n-type well is depicted. This n well is crucial for forming the active regions of the transistors.

3. **Trenches:** The image prominently features trenches etched into the silicon substrate. These trenches are the defining feature of STI and are used to isolate different transistor regions.

4. **SiO₂ Layer:** The trenches are filled with silicon dioxide (SiO₂), as indicated by the label. This oxide layer provides electrical isolation between the active regions on the wafer.

5. **Si₃N₄ Layer:** A silicon nitride (Si₃N₄) layer is shown on the surface of the wafer. This layer is used to define the locations of the trenches during the etching process.

6. **Connections and Interactions:** The diagram does not show explicit electrical connections or signal flow, as it focuses on the physical isolation structures. However, the isolation provided by the SiO₂-filled trenches is essential for preventing electrical interference between adjacent transistors.

7. **Labels and Annotations:** The image includes labels for the Si₃N₄ and SiO₂ layers, as well as the n well and p-type substrate. These annotations help clarify the materials and regions involved in the STI process.

Overall, this cross-section illustrates how STI is implemented to achieve effective isolation between transistors in an integrated circuit by using oxide-filled trenches.

Fig. 2.8 The resulting wafer cross section when shallow-trench isolation (STI) is used between transistors.

A STI process involves etching trenches into the silicon substrate between the active regions and filling the trenches with oxide. As with the field-oxide in a LOCOS process, the trench locations are defined by a $\mathrm{Si}_{3} \mathrm{~N}_{4}$ layer. Filling the trenches is a two-step process: first, the trenches are lined with a thin $\mathrm{SiO}_{2}$ layer that is thermally grown; then additional oxide is deposited over the entire wafer, filling the trenches and leaving behind a very uneven surface. Finally, the top surface is polished to planarize it for further processing. These steps are performed at the start of the process flow, prior to well definition. An example wafer cross-section when STI is used in place of LOCOS is illustrated in Fig. 2.8. STI provides good isolation between transistors even when very closely spaced and is currently in wide use. However, it requires more
steps than LOCOS and is therefore more expensive. Moreover, the creation and filling of the trenches places a strain on the silicon wafer's lattice structure, which impacts the electrical characteristics of nearby transistors.

### 2.1.6 Gate-Oxide and Threshold-Voltage Adjustments

In the next step, the $\mathrm{Si}_{3} \mathrm{~N}_{4}$ is removed using hot phosphoric acid. If a thin layer of $\mathrm{SiO}_{2}$ is under the $\mathrm{Si}_{3} \mathrm{~N}_{4}$, protecting the surface, as shown in Fig. 2.7, this $\mathrm{SiO}_{2}$ is also removed, usually with hydrofluoric acid. The high-quality, thin gate-oxide is then grown using a dry process. It is grown everywhere over the wafer to a thickness of between about 1 and 30 nm .

After the gate-oxide has been grown, donors are implanted so that the final threshold voltages of the transistors are correct. Note that this implantation is performed directly through the thin gate-oxide since it now covers the entire surface. Processes differ in how they realize the threshold-adjust step.

In a simple process, the threshold voltages of both the p - and n -channel transistors are adjusted at the same time. We saw in the Appendix of Chapter 1 that the n -channel transistors require a boron implant to increase $\mathrm{V}_{\mathrm{tn}}$ from its native value to its desired value. If the n wells are doped a little heavier than ideal, the native threshold voltage of the p -channel transistors in the well will also be lower than desired. As a result, the same single boron threshold-adjust implant can bring the NMOS and PMOS threshold voltages to their desired value.

By using a single threshold-voltage-adjust implant for both n-channel and p -channel transistors, two photoresist masking steps are eliminated. If

Key Point: Transistors are fabricated inside the "active" or "oxide definition" $(O D)$ regions of the microcircuit. Over OD regions, only a very thin oxide separates the polysilicon gates from the transistor channel regions underneath, and additional dopants are introduced to control the threshold voltages. Surrounding the OD regions are isolation structures to prevent parasitic transistors from conducting leakage currents.
the different transistors are individually implanted, then the second of two types of transistors has to be protected by, say, a negative photoresist while the first type is being implanted. Next, a positive photoresist can be used with the same mask to protect the first type of transistor while the second type is being implanted. The mask used is normally the same mask used in forming the n wells, in other words, $\mathrm{M}_{1}$. Thus, no additional mask is required, but a number of additional processing steps are needed. The major problem with using a single threshold-adjust implant is that the doping level of the n well is higher than optimum. This higher doping level increases the junction capacitances and the body effect of the transistors in the well. Separate p - and n -type threshold adjust implants allow optimum well doping and are currently more popular. The cross section at this stage is shown in Fig. 2.9.
image_name:Fig. 2.9
description:The image, labeled as Fig. 2.9, is a cross-sectional diagram depicting a stage in semiconductor fabrication after the thin gate-oxide growth and threshold-adjust implant. The diagram illustrates several key components and structures:

1. **n Well**: A region in the semiconductor substrate where n-type doping has been applied. This area is indicated in the diagram and is essential for forming the well where transistors will be built.

2. **Thin Gate SiO₂**: A layer of silicon dioxide (SiO₂) that serves as a thin gate oxide. It is shown as a thin line above the n well, indicating its role as an insulating layer crucial for the gate of a transistor.

3. **Field-Oxide**: Thicker regions of oxide shown in the diagram, these provide electrical isolation between different devices on the chip. They are depicted as elevated areas in the cross-section.

4. **p⁺ Field-Implants**: These are regions with p-type doping, indicated by annotations in the diagram. They are typically used to adjust the threshold voltage and to help with isolation.

5. **Gate Threshold-Voltage-Adjust Implant**: This is an area where implantation has been done to adjust the threshold voltage of the device. It is marked with a series of plus signs, indicating the presence of additional dopants.

The diagram shows how these components are laid out in relation to each other, providing insight into the fabrication process at this stage. The interactions between these elements are crucial for the functioning of the semiconductor device, as they determine the electrical characteristics of the transistors formed in this structure.

$\mathrm{p}^{-}$

Fig. 2.9 Cross section after the thin gate-oxide growth and threshold-adjust implant.

### 2.1.7 Polysilicon Gate Formation

The next step in the process is chemical deposition of the polysilicon gate material. One method to create polysilicon is to heat a wafer with silane gas flowing over it so the following reaction occurs

$$
\begin{equation*}
\mathrm{SiH}_{4} \rightarrow \mathrm{Si}+2 \mathrm{H}_{2} \tag{2.3}
\end{equation*}
$$

If this reaction occurs at high temperatures, say, around 1000 to $1250^{\circ} \mathrm{C}$, and the original surface of the wafer was single crystal, the deposited silicon will also be single crystal. This approach is used both when epitaxial layers are grown in bipolar processes and in some modern CMOS processes. However, when depositing the polysilicon gates the original surface is $\mathrm{SiO}_{2}$ and the wafer is heated only to about $650{ }^{\circ} \mathrm{C}$. As a result, the silicon that is deposited is noncrystalline, or amorphous. Thus, this silicon is often referred to as polysilicon.

It is desirable that the polysilicon gates have low resistivity. Any series resistance in the gate will reduce the speed of the resulting transistors, and be an additional source of noise in the circuits. Hence, after the polysilicon is deposited, it is ion implanted with arsenic to increase its conductivity. A typical final resistivity for polysilicon might be 10 to $30 \Omega / \square$, and its thickness might be around $0.25 \mu \mathrm{~m}$. An additional step may be used to create a layer of low-resistivity salicide on top of the polysilicon gate, further reducing its resistance. For analog circuits, polysilicon strips may also be used as integrated circuit resistors rather than transistor gates. To accommodate this, an additional mask may be used to change the ion implantation and block the salicide resulting in a higher resistivity of typically $500 \Omega$ to $3 \mathrm{k} \Omega / \square$ depending upon the processing details, making the material useful for realizing resistor values of $100 \mathrm{~s} \Omega \mathrm{~s}$ to $10 \mathrm{~s} \mathrm{k} \Omega$.

After the deposition just described, the polysilicon gate material covers the entire wafer. This polysilicon is then patterned using a new mask, $\mathrm{M}_{3}$, and a positive photoresist, $\mathrm{PR}_{4}$. The mask is opaque where hardened polysilicon should remain. After the nonhardened photoresist is removed, the polysilicon is etched away using a reactive plasma etch. This etch removes all of the polysilicon not protected by photoresist but removes very little of the underlying $\mathrm{SiO}_{2}$. This thin gate-oxide layer is used to protect the surface during the next step of junction implantation. The cross section at this phase is shown in Fig. 2.10.

### 2.1.8 Implanting the Junctions, Depositing $\mathrm{SiO}_{2}$, and Opening Contact Holes

The next step involves the ion implantation of the junctions. In our example process, the $\mathrm{p}^{+}$junctions are formed first by placing positive photoresist, $\mathrm{PR}_{5}$, everywhere except where the $\mathrm{p}^{+}$regions are desired. A new mask, $\mathrm{M}_{4}$, is
image_name:Fig. 2.10 Cross section after depositing and patterning the polysilicon gates
description:The image labeled "Fig. 2.10 Cross section after depositing and patterning the polysilicon gates" illustrates a semiconductor cross-section during a manufacturing process. Key components and structures in the diagram include:

1. **Polysilicon Gate**: The diagram shows a polysilicon gate structure, which is a critical component in MOSFET (Metal-Oxide-Semiconductor Field-Effect Transistor) fabrication. The gate is depicted as a layered rectangle on the surface of the structure, indicating its position above the silicon substrate.

2. **SiO₂ Layer**: There is a layer of silicon dioxide (SiO₂) beneath the polysilicon gate. This oxide layer acts as an insulator, separating the gate from the underlying silicon substrate.

3. **Photoresist (PR₄)**: The image includes a label for PR₄, a photoresist layer used during the patterning process. This layer is typically applied to protect certain areas during etching or ion implantation.

4. **n Well**: The cross-section shows an n-type well, which is a region doped with donor atoms to create an excess of electrons. This is indicated by a labeled area within the silicon substrate.

5. **p⁺ and p⁻ Regions**: The diagram includes areas labeled as p⁺ and p⁻, indicating regions with different levels of p-type doping. The p⁺ regions are heavily doped compared to the p⁻ regions, which are lightly doped.

6. **Arrows Indicating Doping**: Arrows point towards the p⁺ regions, suggesting the direction of ion implantation or diffusion for creating these doped areas.

7. **Cross-Sectional View**: The overall view is a cross-section, showing the layers and regions within the semiconductor device as they would appear in a slice through the material.

This cross-section is indicative of a stage in semiconductor device fabrication where polysilicon gates have been deposited and patterned, and the structure is prepared for subsequent ion implantation steps.

Fig. 2.10 Cross section after depositing and patterning the polysilicon gates.
image_name:Fig. 2.11
description:The image labeled "Fig. 2.11" is a cross-sectional diagram of a semiconductor device after the ion implantation of \( p^+ \) junctions. This stage follows the deposition and patterning of polysilicon gates, which are visible in the diagram.

1. **Identification of Components and Structure:**
- The diagram shows a series of layers and regions within the semiconductor structure. The most prominent features are the polysilicon gates, which are highlighted as rectangular blocks on the surface of the structure.
- Below the gates, there are \( p^+ \) regions which have been ion-implanted. These regions are marked and shaded differently to indicate their doping levels.
- An \( n \) well is depicted, which provides a substrate for the \( p^+ \) regions.
- The diagram also shows field oxide layers that separate different active areas.

2. **Connections and Interactions:**
- The \( p^+ \) junctions are positioned such that one edge is defined by the field oxide, and the other is aligned with the edge of the polysilicon gate. This alignment is crucial for defining the channel region of the transistor.
- The substrate connection is indicated, showing how the \( p^+ \) regions connect to the rest of the semiconductor device.

3. **Labels, Annotations, and Key Features:**
- Labels such as \( \text{PR}_4 \) and \( \text{PR}_5 \) are used to denote specific process steps or regions in the fabrication process.
- The "polysilicon" label indicates the gate material, which is a key component in the transistor structure.
- The \( p^+ \) and \( n \) well regions are clearly marked to show the different doping types and levels.
- Annotations such as "substrate connection" help clarify the purpose and function of certain regions within the device.

Overall, this cross-section provides a detailed view of the semiconductor device's structure at a particular fabrication stage, focusing on the arrangement and interaction of the polysilicon gates and \( p^+ \) junctions.

$\mathrm{p}^{-}$

Fig. 2.11 Cross section after ion-implanting the $\mathrm{p}^{+}$junctions.
used in this step. The $\mathrm{p}^{+}$regions are then ion implanted, possibly through a thin oxide in some processes. The cross section at this stage is shown in Fig. 2.11.

Notice that the $\mathrm{p}^{+}$junctions of the p -channel transistors are defined on one edge by the field-oxide and, more importantly, next to the active gate area by the edge of the polysilicon gate. During the implantation of the boron, it was the gate polysilicon and the photoresist over it that protected the channel region from the $\mathrm{p}^{+}$implant. Thus, the $\mathrm{p}^{+}$junctions are self-aligned to the polysilicon gates, resulting in very little overlap (i.e., a small $L_{o v}$, as defined in Chapter 1). Also, note that the effective channel areas of the transistors are defined by the intersection of the gate-defining mask, $M_{3}$, and the mask used

Key Point: The edge of transistor source and drain junctions are defined by the edge of the polysilicon gate above. This "self-alignment" of the gate and junctions was key in the development of small high-speed transistors.
in defining the active regions, $\mathrm{M}_{2}$ (i.e., the mask used in defining where $\mathrm{Si}_{3} \mathrm{~N}_{4}$ remains). Thus, these are the two most important masks in any MOS process. The development of this selfaligned process has proven to be an important milestone in realizing small high-speed transistors.

Also notice that a $\mathrm{p}^{+}$junction has been implanted in the substrate region. This junction, called a substrate tie, is used to connect the substrate to ground in microcircuits. These substrate ties are liberally placed throughout the microcircuit to help prevent latch-up, a problem discussed at the end of this chapter. In addition, the underside of the wafer would normally be connected to ground as well, through a package connection.

Next, the photoresists are all removed using acetone. The $\mathrm{p}^{+}$active regions are then protected using the same mask, $\mathrm{M}_{4}$, that was used for the previous step, but now a negative photoresist, $\mathrm{PR}_{6}$, is used. The $\mathrm{n}^{+}$junctions are then implanted using arsenic. The cross section at the end of this stage is shown in Fig. 2.12.
image_name:Fig. 2.12
description:The image, labeled as Fig. 2.12, is a cross-sectional diagram of a semiconductor wafer after the ion-implantation of n+ junctions. The diagram illustrates several key components and structures involved in the semiconductor fabrication process:

1. **Components and Structure:**
- The cross-section shows a layered semiconductor structure with alternating n+ and p+ regions, which represent n-channel and p-channel junctions, respectively. These regions are crucial for forming the active areas of semiconductor devices.
- Polysilicon gates are depicted above the junctions, indicating the presence of MOSFET structures. These gates control the flow of charge carriers in the underlying channels.
- The substrate is labeled as p-, indicating that the base material is a lightly doped p-type semiconductor.
- PR6 (negative photoresist) is shown covering certain areas, protecting specific regions during the ion implantation process.

2. **Connections and Interactions:**
- The diagram includes well ties and substrate ties, which are connections used to ensure proper electrical contact and grounding within the semiconductor structure. These ties help manage the potential differences across the wafer and maintain stability in the device operation.
- The n+ and p+ junctions are strategically placed to create p-channel and n-channel regions, essential for the operation of complementary MOS (CMOS) circuits.

3. **Labels, Annotations, and Key Features:**
- Labels clearly identify the n+ and p+ junctions, polysilicon gates, and the PR6 photoresist. These annotations are crucial for understanding the fabrication steps and the function of each part of the structure.
- The presence of arrows indicates the implantation direction and the regions protected during the process.

Overall, the diagram provides a detailed view of the semiconductor wafer after the n+ junction implantation stage, highlighting the complex layering and precise engineering required in semiconductor device fabrication.

Fig. 2.12 Cross section after ion-implanting the $\mathrm{n}^{+}$junctions.

After the junctions have been implanted and $\mathrm{PR}_{6}$ has been removed, the complete wafer is covered in CVD $\mathrm{SiO}_{2}$. This protective glass layer can be deposited at moderately low temperatures of $500^{\circ} \mathrm{C}$ or lower. The deposited $\mathrm{SiO}_{2}$ might be 0.25 to $0.5 \mu \mathrm{~m}$ thick.

The next step is to open contact holes through the deposited $\mathrm{SiO}_{2}$. The contact holes are defined using mask $\mathrm{M}_{5}$ and positive resist $\mathrm{PR}_{7}$.

### 2.1.9 Annealing, Depositing and Patterning Metal, and Overglass Deposition

After the first layer of $\mathrm{CVD} \mathrm{SiO}_{2}$ has been deposited, the wafer is annealed. As mentioned earlier in this section, annealing entails heating the wafer in an inert gas (such as nitrogen) for some period of time (say, 15 to 30 minutes) at temperatures up to $1000^{\circ} \mathrm{C}$. The resulting thermal vibrations heal the lattice damage sustained during all the ion implantations, broaden the concentration profiles of the implanted dopants, and increase the density of the deposited $\mathrm{SiO}_{2}$.

Next, interconnect metal is deposited everywhere. Historically, aluminum (AI) has been used for the interconnect. However, other metals have been used that have less of a tendency to diffuse into the silicon during electrical operation of the microcircuit. Copper is increasingly being used to take advantage of its lower resistivity, an important consideration for very thin wires and for wires conducting large currents. The metal is deposited using evaporation techniques in a vacuum. The heat required for evaporation is normally produced by using electronbeam bombarding, or possibly ion bombarding in a sputtering system. After the metal is deposited on the entire wafer, it is patterned using mask $\mathrm{M}_{6}$ and positive photoresist $\mathrm{PR}_{8}$, and then it is etched.

At this time, a low-temperature annealing might take place to give better bonds between the metal and the silicon. The temperature of this annealing must be less than $550^{\circ} \mathrm{C}$ so the aluminum doesn't melt.

Key Point: Up to 10 or even

more layers of metal are patterned above the silicon surface, separated by insulating oxide, to provide interconnect between all the devices in a circuit.

Next, an additional layer of $\mathrm{CVD} \mathrm{SiO}_{2}$ is deposited, additional contact holes are formed using mask $\mathrm{M}_{7}$ and photoresist $\mathrm{PR}_{9}$, and then a second layer of metal is deposited and etched using mask $\mathrm{M}_{8}$ and photoresist $\mathrm{PR}_{10}$. Often the primary use of top layers of metal might be to distribute the power supply voltages. Lower layers would be used more often for local interconnects in gates. In modern fabrication, this process may be repeated ten or more times to provide a much denser interconnect.
After the last level of metal is deposited, a final passivation, or overglass, is deposited for protection. This layer would be $\mathrm{CVD} \mathrm{SiO}_{2}$, although often an additional layer of $\mathrm{Si}_{3} \mathrm{~N}_{4}$ might be deposited because it is more impervious to moisture.

The final microcircuit processing step is to etch openings in the passivation to metal pads located in the top metal layer to permit electrical contacts to be formed to the circuit. This final step would use mask $\mathrm{M}_{9}$ and photoresist $\mathrm{PR}_{11}$. A cross section of the final microcircuit for our example process is shown in Fig. 2.13.

### 2.1.10 Additional Processing Steps

This chapter has focused primarily on an example process representative of a technology with minimum feature sizes of approximately $0.5 \mu \mathrm{~m}$. However, many variations, often involving additional masks, are possible. Additional steps are certainly required to realize smaller feature sizes. Some of the possible variations are as follows:

1. Two wells may exist: one for p -channel transistors and one for n -channel transistors. This twin-well process allows both wells to be optimally doped.
2. An additional polysilicon layer may be deposited over the first layer and separated by a thin thermal oxide layer. This extra poly layer can be used to realize highly linear poly-to-poly capacitors.
3. An additional polysilicon layer might be formed that has an extremely high resistivity (say, $1 \mathrm{G} \Omega / \square$ ). This high resistivity is used to realize resistor loads in four-transistor, static random-access memory (SRAM) cells.
image_name:Fig. 2.13 Final cross section of an example CMOS microcircuit.
description:The image labeled "Fig. 2.13 Final cross section of an example CMOS microcircuit" shows a detailed cross-sectional view of a CMOS microcircuit. The diagram is annotated with various layers and components of the circuit.

1. **Components and Structure:**
- The topmost layer is labeled as "Overglass," which likely serves as a protective layer for the circuit.
- Beneath the overglass are two metal layers, "Metal 1" and "Metal 2," which are used for interconnections within the circuit.
- The "Polysilicon gate" is visible, indicating the gate structure for the transistors.
- "CVD SiO2" is shown as a dielectric layer, likely used for insulation between components.
- "Via" connections are indicated, which provide electrical connections between the metal layers.
- The structure includes both "p-channel transistor" and "n-channel transistor," essential components of CMOS technology.
- "Field-oxide" regions are present, which help isolate different components of the circuit.

2. **Connections and Interactions:**
- The metal layers are connected via vias, allowing for signal and power routing between different parts of the circuit.
- The diagram shows the arrangement of n+ and p+ regions, which are the doped areas forming the source and drain of the transistors.
- "Well tie" and "Substrate tie" are noted, providing electrical connections to the well and substrate, ensuring proper biasing.

3. **Labels, Annotations, and Key Features:**
- The diagram includes various annotations such as "n+" and "p+" to indicate doped regions.
- "p+ field-implant" is shown under the field-oxide, which is used for adjusting the threshold voltage and preventing parasitic effects.
- The "p−" and "n" regions are labeled, indicating the substrate and well areas, respectively.

This cross-sectional view provides a comprehensive look at the layered structure and interconnections within a CMOS microcircuit, showcasing how different materials and processes are used to create functional electronic components.

Fig. 2.13 Final cross section of an example CMOS microcircuit.
4. Field-implants may exist under the field-oxide in the well regions as well as under the field-oxide in the substrate regions.
5. Often, the n -channel and the p -channel transistors will have separate threshold-voltage-adjust implants.
6. The microcircuit might have up to ten or more layers of metal.
7. It is usually necessary to add several additional steps so that the surface is made smoother, or planarized, after each metal-patterning step. This is normally done by a reactive etching process in which the metal is covered with $\mathrm{SiO}_{2}$ and the hills are etched faster than the valleys.
8. Different metals might be used for the silicon contacts than for the interconnect, to obtain better fill in and less diffusion into the silicon surface.
9. Thin-film nichrome resistors may exist under the top layer of metal.
10. Additional ion implantation and salicide blocking steps may be used to produce polysilicon strips with high sheet resistance for use as resistors.
11. The transistors may be realized in an epitaxial layer. For example, the substrate may be $\mathrm{p}^{++}$, and a $\mathrm{p}^{-}$epitaxial layer would be grown on top. The advantages of this type of wafer are that it is more immune to a destructive phenomenon called latch-up (described at the end of this chapter), and it is also more immune to gamma radiation in space. Finally, it greatly minimizes substrate noise in microcircuits that have both analog and digital circuits, (i.e., mixed-mode microcircuits).
12. "Shallow-trench isolation" involves etching trenches into the silicon substrate between transistors to reduce the coupling between them, which is increasingly problematic at small feature sizes.
13. In order to mitigate hot carrier effect, the narrow portion of the source/drain regions immediately adjacent to the channel may be ion implanted to reduce their doping levels. Unfortunately, these "lightlydoped drain" regions also introduce a significant resistance in series with the channel.
14. Impurities may be introduced into the crystalline silicon lattice in order to stretch or compress the MOSFET channel regions. For example, silicon germanium has a larger lattice spacing than pure silicon, so by using some silicon germanium to stretch the regular silicon crystal lattice, an increase in electron mobility is effected.
15. Ion implantation with very high acceleration may be used to implant dopants at a depth greater than any of the transistor features; for example, approximately $2 \mu \mathrm{~m}$ below the substrate surface. This is sometimes used to create a buried deep n well region below the silicon substrate and contacted by a regular n well. A critical circuit may be isolated from noise in neighboring circuits by enclosing it in such a buried n well making it useful for mixed analog-digital integrated circuits.
16. Additional processing steps may be used to ensure that bipolar transistors can be included in the same microcircuit as MOS transistors. This type of process is called a BiCMOS process and is particularly popular for analog high-speed microcircuits.

## 2.2 CMOS LAYOUT AND DESIGN RULES

It is the designer's responsibility to determine the geometry of the various masks required during processing. The process of defining the geometry of these masks is known as layout and is done using a CAD program. Here, we describe some typical layout design rules and the reasons for these rules.

### 2.2.1 Spacing Rules

When designing the layout, typically the designer does not need to produce the geometry for all of the masks because some of the masks are automatically produced by the layout program. For example, the $\mathrm{p}^{+}$and $\mathrm{n}^{+}$masks used for the source and drain regions are usually generated automatically. Also, the program might allow the designer to work in the final desired dimensions. The layout program then automatically sizes the masks to account for any lateral diffusion or etching loss; this sizing produces larger- or smaller-dimension masks. For example, a designer might draw a polysilicon line so that a transistor would have a $0.1-\mu \mathrm{m}$ length. The program might then produce a mask that had a $0.12-\mu \mathrm{m}$ line width. This increased mask sizing would account for the junction overlap due to lateral diffusion and the polysilicon loss due to etching.

In a modern layout program, the layout of some circuit cells might already be performed and stored in a library. During overall layout, these cells are then parametrically adapted to a required size, and the corresponding geometries for every layer are automatically generated. Often, when the cells are being connected, they might be automatically placed an $d$ routed, or connected, by the program. The designer might then interactively modify this automatically generated layout. Thus, as time goes on, the layout becomes more automated as more cells become available. However, the designer must still take direct control of the layout of critical cells, especially when the layout must be small or the resulting circuits must be fast. For example, one would rarely allow a computer to automatically generate the layout of a memory cell where space and capacitive loading of the connecting buses are critical. Thus, a digital microcircuit designer must be knowledgeable about the design rules that govern the layout required for the process used.

The two most important masks are those for the active (OD) region and for the gate polysilicon. The intersection of these two masks becomes the channel region of MOS transistors. For example, consider Fig. 2.14(a), which shows a simplified view of a MOS transistor, and Fig. 2.14(b), which shows the corresponding layout of the active mask and the polysilicon, or poly, mask. In Fig. $2.14(b)$, the poly mask runs vertically. The length of the poly that intersects the active-region mask is the transistor width, W , and the width of the poly line is the transistor length, L, as Fig. 2.14 shows.

The design rules for laying out transistors are often expressed in terms of a quantity, $\lambda$, where $\lambda$ is $1 / 2$ the minimum permitted gate length. This generalization allows many of the design rules to be simply expressed, independent of the true value for the minimum channel length (i.e., $2 \lambda$ ). Figure 2.14(b) shows the smallest possible transistor that can be realized in a given process when a contact must be made to each junction. Also shown are many of the minimum dimensions in terms of $\lambda$.

When we express design rules in terms of $\lambda$, we assume that each mask has a worst-case alignment of under $0.75 \lambda$. Thus, we can guarantee that the relative misalignment between any two masks is under $1.5 \lambda$. If an overlap between any two regions of a microcircuit would cause a destructive short circuit, then a separation between the corresponding regions in a layout of $2 \lambda$ guarantees this will never happen. For example, consider the poly mask and the contact mask in Fig. 2.14(b). If these two regions overlap in the microcircuit, then the
image_name:(a)
description:The image consists of two parts, labeled (a) and (b), illustrating components and layout of a transistor and its masks.

**(a) Simplified View of a Partially Finished Transistor:**
- **Components and Structure:**
- The diagram shows a cross-sectional view of a partially finished transistor. There is an active region marked along the bottom, which serves as the substrate for the transistor.
- On top of the active region, a polysilicon structure is visible, represented by a shaded area. This is likely the gate of the transistor.
- Surrounding the active region, there are field oxide regions, which provide isolation between different transistors on a chip.
- **Connections and Interactions:**
- The active region is connected to other parts of the circuit via contacts, indicated by openings in the field oxide.
- The polysilicon gate is positioned over the active region, controlling the current flow through the transistor.
- **Labels, Annotations, and Key Features:**
- The width (W) and length (L) of the active region are marked, showing the dimensions critical for the transistor's operation.

**(b) Corresponding Layout of the Active, Polysilicon, and Contact Masks:**
- **Components and Structure:**
- This part provides a top-down view of the layout masks used during the fabrication of the transistor.
- The polysilicon mask, active-region mask, and contact mask are clearly labeled.
- The field-oxide region is shaded differently to distinguish it from the active region.
- **Connections and Interactions:**
- The effective gate region is indicated between the polysilicon mask and the active-region mask.
- The contact mask is positioned to ensure that openings are correctly aligned with the active region and do not overlap with the polysilicon gate, preventing short circuits.
- **Labels, Annotations, and Key Features:**
- Dimensions are annotated in terms of lambda (λ), a unit used to define design rules in microfabrication. For instance, the field-oxide region is marked as 5λ by 4λ, and the contact mask is positioned 2λ away from critical areas to avoid shorts.
- The layout shows a clear separation between different regions, ensuring that the design rules are adhered to for reliable transistor operation.
image_name:(b)
description:
[

]
extrainfo:The diagram (b) illustrates the layout of a microcircuit with active, polysilicon, and contact masks. It emphasizes the importance of maintaining a separation of at least 2λ between contact openings and other regions to prevent destructive short circuits. The layout shows dimensions and spacing of various regions, including the active region, field-oxide region, and effective gate region, with specific measurements in terms of λ. The field-oxide region ensures isolation, while the polysilicon mask defines the gate area. The active-region mask encompasses the source and drain areas, and the contact mask indicates where connections are made.

Fig. 2.14 (a) A simplified view of a partially finished transistor and (b) the corresponding layout of the active, polysilicon, and contact masks.
metal used to contact the source junction is also short-circuited to the gate poly, causing the transistor to be always turned off, as shown in Fig. 2.15. If the source happens to be connected to ground, this error also shortcircuits the gate-to-ground. To prevent this type of short, the contact openings must be kept at least $2 \lambda$ away from the polysilicon gates.

Another example of a catastrophic failure due to misalignment is a gate that does not fully cross the active region (also shown in Fig. 2.15). Since the junctions are implanted everywhere in the active region except under the gate, this misalignment causes a short circuit between the source and the drain-thus the design rule that polysilicon must always extend at least $2 \lambda$ past the active region.

Another design rule is that active regions should surround contacts by at least $1 \lambda$. If, in reality, an overlap exists between the edge of the active-region mask and the contact mask, no disastrous shorts occur. The circuit still works correctly as long as sufficient overlap exists between the contact and the active masks so that a good connection is made between the aluminum interconnect and the junction. Since the maximum relative misalignment is $1.5 \lambda$, having the source (or drain) region surround the contact by $1 \lambda$ and a minimum contact width of $2 \lambda$ guarantees an overlap of at least $1.5 \lambda$.

The few design rules just described are sufficient to allow one to estimate the minimum dimensions of a junction area and perimeter before a transistor has been laid out. For example, assume that in Fig. 2.14 a contact is to
image_name:Fig. 2.15
description:
[

]
extrainfo:The diagram illustrates potential misalignments in a MOSFET layout, showing a source-to-gate short circuit, a source-to-drain short circuit, and a noncatastrophic misalignment.

Fig. 2.15 Mask misalignment that results in catastrophic short circuits and an example of a noncatastrophic misalignment.
be made to a junction; then the active region must extend past the polysilicon region by at least $5 \lambda$. Thus, the minimum area of a small junction with a contact to it is

$$
\begin{equation*}
A_{s}=A_{d}=5 \lambda \mathrm{~W} \tag{2.4}
\end{equation*}
$$

where W is the transistor width. Similarly, in Fig. 2.14, the perimeter of a junction ${ }^{3}$ with a contact is given by

$$
\begin{equation*}
P_{s}=P_{d}=10 \lambda+W \tag{2.5}
\end{equation*}
$$

These estimates may be used when estimating the parasitic capacitances in the transistor models. They may also be used in SPICE to simulate circuits so the parasitic capacitances are determined more accurately. However, note that they are only estimates; the true layout will differ somewhat from these rough estimates.

Key Point: Finite tolerances during integrated circuit manufacturing impose constraints on the minimum sizes and spacing of transistor and interconnect features. These constraints may be expressed as multiples of $\lambda$, equal to one-half the minimum gate length. They influence parasitic capacitances, and ultimately the circuit bandwidth which an analog designer may expect.

Sometimes, when it is important to minimize the capacitance of a junction, a single junction can be shared between two transistors. For example, consider the series connection of two transistors shown in Fig. 2.16(a). The active, poly, and contact masks might be laid out as shown in Fig. 2.16(b). Notice that a single junction is shared between transistors $Q_{1}$ and $Q_{2}$. The area, and especially the perimeter of this junction, are much smaller than those given by equations (2.4) and (2.5). Also, in a SPICE simulation, the area and perimeter should be divided by 2 when they are specified in each transistor description, since the junction is shared. Alternatively, all of the area and perimeter could be specified in one transistor description, and the area and perimeter of the other junction could be specified as zero.

Since the junction sidewall capacitance is directly proportional to the junction perimeter, and since this capacitance can be a major part of the total junction capacitance (because of the
3. Note that the perimeter does not include the edge between the junction and the active channel separating the junction and the gate because there is no field-implant along this edge, and the sidewall capacitance is therefore smaller along that edge.
image_name:(a)
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: J3, G: g1}
name: Q2, type: NMOS, ports: {S: J3, D: J2, G: g2}
]
extrainfo:The circuit diagram shows a series connection of two NMOS transistors, Q1 and Q2. Q1's source is connected to ground, its drain is connected to node J3, and its gate is connected to g1. Q2's source is connected to node J3, its drain is connected to node J2, and its gate is connected to g2. The layout diagram illustrates the physical dimensions and spacing related to the junctions J1, J2, and J3, with dimensions given in terms of λ.
image_name:(b)
description:The image consists of two parts labeled (a) and (b). Part (a) shows a series connection of two transistors, Q1 and Q2, with their gates labeled g1 and g2 respectively. These transistors are connected between junctions J1 and J2, with J3 being the intermediate junction. The circuit is grounded at J1.

Part (b) is a layout diagram corresponding to the circuit in (a). It shows the physical arrangement of the transistors and junctions on a substrate. The layout includes:

1. **Components:**
- Two long vertical rectangles labeled Q1 and Q2, representing the transistors.
- Three square regions labeled J1, J2, and J3, representing the junctions.

2. **Connections and Interactions:**
- Q1 and Q2 are placed side by side, with Q1 on the left and Q2 on the right.
- The junction J3 is located between Q1 and Q2, representing the connection between the two transistors.
- The layout shows the spacing between the components, with annotations indicating dimensions in terms of λ (lambda).

3. **Labels, Annotations, and Key Features:**
- The dimensions are marked in multiples of λ, such as 2λ, 3λ, and 10λ, indicating the relative sizes and spacing.
- J1 and J2 are positioned at the top and bottom of the layout, respectively, with J3 centrally located between Q1 and Q2.
- The layout emphasizes minimizing the perimeter of the junctions to reduce sidewall capacitance, as mentioned in the context.

Fig. 2.16 (a) A series connection of two transistors and (b) a possible layout.
heavily doped field-implants), minimizing the perimeter is important. Note that it is impossible to share junctions between n -channel and p -channel devices as they must be located in separate substrate regions doped p - and n type respectively.

#### EXAMPLE 2.1

Assuming $\lambda=0.2 \mu \mathrm{~m}$, find the area and perimeters of junctions $J_{1}, J_{2}$, and $J_{3}$ for the circuit in Fig. 2.16.

#### Solution

Since the width and length are shown as $10 \lambda$ and $2 \lambda$, respectively, and $\lambda=0.2 \mu \mathrm{~m}$, the physical sizes are $\mathrm{W}=2 \mu \mathrm{~m}$ and $\mathrm{L}=0.4 \mu \mathrm{~m}$.

Thus, for junction $J_{1}$, using the formulas of (2.4) and (2.5), we have

$$
\begin{equation*}
\mathrm{A}_{\mathrm{J}_{1}}=5 \lambda \mathrm{~W}=5(0.2) 2 \mu \mathrm{~m}^{2}=2 \mu \mathrm{~m}^{2} \tag{2.6}
\end{equation*}
$$

and

$$
\begin{equation*}
P_{\mathrm{J} 1}=10 \lambda+W=[10(0.2)+2] \mu \mathrm{m}=4 \mu \mathrm{~m} \tag{2.7}
\end{equation*}
$$

Since this junction is connected to ground, its parasitic capacitance is unimportant and little has been done to minimize its area. Contrast this case with junction $J_{2}$, where we have

$$
\begin{equation*}
\mathrm{A}_{\mathrm{J} 2}=2 \lambda \mathrm{~W}+12 \lambda^{2}=1.28 \mu \mathrm{~m}^{2} \tag{2.8}
\end{equation*}
$$

The perimeter is unchanged, resulting in $P_{\mathrm{J} 2}=4 \mu \mathrm{~m}$. Thus, we have decreased the junction area by using the fact that the transistor is much wider than the single contact used. However, sometimes wide transistors require
additional contacts to minimize the contact impedance. For example, the two contacts used for junction $J_{1}$ result in roughly half the contact impedance of junction $J_{2}$.

Next, consider the shared junction. Here we have a junction area given by

$$
\begin{equation*}
\mathrm{A}_{\mathrm{J} 3}=2 \lambda \mathrm{~W}=0.8 \mu \mathrm{~m}^{2} \tag{2.9}
\end{equation*}
$$

Since this is a shared junction, in a SPICE simulation we would use

$$
\begin{equation*}
A_{s}=A_{d}=\lambda W=0.4 \mu \mathrm{~m}^{2} \tag{2.10}
\end{equation*}
$$

for each of the two transistors, which is much less than $2 \mu \mathrm{~m}^{2}$. The reduction in the perimeter is even more substantial. Here we have

$$
\begin{equation*}
P_{\mathrm{J} 3}=4 \lambda=0.8 \mu \mathrm{~m} \tag{2.11}
\end{equation*}
$$

for the shared junction; so sharing this perimeter value over the two transistors would result in

$$
\begin{equation*}
P_{S}=P_{d}=2 \lambda=0.4 \mu \mathrm{~m} \tag{2.12}
\end{equation*}
$$

for the appropriate junction of each transistor when simulating it in SPICE. This result is much less than the $4-\mu \mathrm{m}$ perimeter for node $J_{1}$.

Because minimizing the junction capacitance is so important, one of the first steps an experienced designer takes before laying out important high-speed cells is first to identify the most critical nodes and then to investigate possible layouts that minimize the junction capacitance of these nodes.

An additional design rule has been implicitly introduced in the previous example. Notice that for junction $\mathrm{J}_{2}$ in Fig. 2.16, part of the active region boundary is only $2 \lambda$ away from the gate. This minimum junction area is the typical design rule for this case.

Several design rules are required in addition to those just mentioned. Some of these are described next, with reference to the layout of a digital inverter, shown in Fig. 2.17. Notice that the n well surrounds the p -channel active region, and therefore the $\mathrm{p}^{+}$junctions of the p -channel transistors, by at least $3 \lambda$. Notice also that the minimum spacing between the n well and the junctions of n -channel transistors, in the substrate, is $5 \lambda$. This large spacing is required because of the large lateral diffusion of the $n$ well and the fact that if the $n$-channel junction became short-circuited to the n well, which is connected to $\mathrm{V}_{\mathrm{DD}}$, the circuit would not work. Conversely, a $\mathrm{p}^{+}$-substrate tie can be much closer to a well because it is always connected to ground and is separated from the well by a reversebiased junction. A typical dimension here might be $2 \lambda$. Since a $p$-channel junction must be inside the well by at least $3 \lambda$ and an $n$-channel junction must be outside the well by $5 \lambda$, the closest an $n$-channel transistor can be placed to a $p$-channel transistor is $8 \lambda$.

Notice in Fig. 2.17 that metal is used to connect the junctions of the p -channel and n -channel transistors. Normally, the metal must overlap any underlying contacts by at least $\lambda$. A typical minimum width for first-level metal might be $2 \lambda$, the same as the minimum width for polysilicon. However, it can be wider as in Fig. 2.17, where it is $4 \lambda$ wide.

Notice also in Fig. 2.17 that a single contact opening, known as a butting contact, is used to contact both the p-channel transistor source and an $\mathrm{n}^{+}$-well tie, because both will be connected to $\mathrm{V}_{\mathrm{DD}}$. Although the outlines of the $\mathrm{p}^{+}$and $\mathrm{n}^{+}$ masks are not shown in Fig. 2.17, under the contact, one half will be doped $p^{+}$(the $p$-channel junction) and one half will be doped $\mathrm{n}^{+}$(the well tie). Also, for the n -channel transistor, a butting contact was used to connect the n -channel source to a $\mathrm{p}^{+}$-substrate tie, and both will be connected to ground. In a typical set of design rules, a maximum distance between transistors and well (or substrate) ties is specified, and a maximum distance between substrate ties is also specified. For example, the rules might specify that no transistor can be more than $100 \lambda$ from a substrate tie. These rules are necessary to prevent latch-up, a phenomenon described at the end of this chapter.
image_name:(a)
description:
[
name: Q1, type: NMOS, ports: {S: Gnd, D: Vout, G: Vin}
name: Q2, type: PMOS, ports: {S: VDD, D: Vout, G: Vin}
]
extrainfo:The circuit is a CMOS digital inverter with Q1 as the NMOS and Q2 as the PMOS transistor. The input is Vin, and the output is Vout. The NMOS is connected to ground, and the PMOS is connected to VDD.
image_name:(b)
description:The image titled "(b)" illustrates a possible layout of a CMOS digital inverter, highlighting several design rules. This layout includes both p-channel and n-channel transistors, denoted as Q2 and Q1, respectively.

1. **Identification of Components and Structure:**
- **P-Channel Transistor (Q2):** Positioned at the top, embedded within an n-well. It is connected to the supply voltage (V_DD).
- **N-Channel Transistor (Q1):** Located at the bottom, connected to the ground (Gnd) through a p+ substrate tie.
- **Poly Interconnect:** Connects the gates of the transistors, marked as Vin, which serves as the input to the inverter.
- **Metal Interconnect:** Used for connecting various components, including the output (Vout) and other active regions.

2. **Connections and Interactions:**
- The layout shows the p-channel transistor (Q2) connected to the V_DD through an n+ well tie, while the n-channel transistor (Q1) is connected to the ground (Gnd) via an n+ junction and p+ substrate tie.
- The poly interconnect runs horizontally, connecting the gates of both transistors, indicating the input path (Vin).
- The metal interconnects are used to route the output (Vout) from the junction between the two transistors.

3. **Labels, Annotations, and Key Features:**
- **Active Region:** Highlighted areas where the transistors are active.
- **Design Rules:** Distances such as 3λ, 5λ, and λ are annotated to indicate spacing and alignment rules crucial for the layout.
- **N+ and P+ Junctions:** Marked areas indicating the doping regions necessary for forming the transistors and ensuring proper electrical characteristics.
- **N-Well and P+ Substrate Tie:** These are essential for isolating the p-channel transistor and connecting the n-channel transistor to the ground, respectively.

This layout exemplifies the complexity and precision required in designing CMOS circuits, ensuring all components are properly connected and spaced to prevent issues like latch-up.

Fig. 2.17 (a) A CMOS digital inverter and (b) a possible layout with several design rules illustrated.
As a final example, we describe the layout of a large transistor. Normally, a wide transistor is composed of smaller transistors connected in parallel. This approach results in shorter individual polysilicon gate strips and, hence, a lower series gate resistance. It also reduces the junction capacitances, as we shall see in Example 2.2. A simplified layout of this approach is shown in Fig. 2.18(a), where four transistors that have a common gate are connected in parallel. Figure 2.18(b) shows the circuit corresponding to the layout in Fig. 2.18(a), where the transistors have been drawn in the same relative positions. Figure 2.18(c) shows the same circuit redrawn differently, where it is clear that the circuit consists of four transistors connected in parallel. Notice that the second and fourth junction regions are connected by metal to node 1, whereas the first, third, and fifth junction regions are connected by metal to realize node 2 . Because it has a larger total junction area and especially a larger perimeter, node 2 will have a much greater junction capacitance than node 1 . Thus, when the equivalent transistor is connected to a circuit, node 1 should be connected to the more critical node. Also notice the large number of contacts used to minimize the contact impedance. The use of many contacts in wide junction regions greatly minimizes voltage drops that would otherwise occur due to the relatively high resistivity of silicon junctions compared to the resistivity of the metal that overlays the junctions and connects them. ${ }^{4}$
image_name:(a)
description:The image consists of three parts labeled (a), (b), and (c), illustrating the layout and schematic of connecting four transistors in parallel to form a single larger transistor.

1. **Identification of Components and Structure:**
- **(a) Layout:**
- The layout shows four transistors labeled Q1, Q2, Q3, and Q4. Each transistor is depicted with a rectangular active region and multiple contacts, represented by black squares, which minimize contact impedance.
- Metal interconnects are shown as thick lines connecting the transistors to Node 1 and Node 2. The interconnects overlay the active regions and connect them electrically.
- Gates are indicated with arrows pointing to the active regions, showing where the gate voltage (VG) is applied.
- The entire layout is structured to ensure efficient current flow and minimize voltage drops.

2. **Connections and Interactions:**
- **(b) Schematic Diagram:**
- The schematic is drawn in the same relative positions as the layout, showing transistors Q1 to Q4 connected in parallel.
- Node 1 is connected to the top of each transistor, while Node 2 connects to the bottom. The gate voltage (VG) is applied to all transistors simultaneously.
- Junctions J1 to J5 are depicted, indicating connections between the transistors and the nodes.

- **(c) Circuit Redrawn:**
- The circuit is redrawn to highlight the parallel connection of the transistors.
- Transistors Q1 to Q4 are shown in a linear arrangement, with VG applied uniformly across them.
- Node 1 and Node 2 are at opposite ends of the circuit, illustrating the flow of current through the parallel transistors.

3. **Labels, Annotations, and Key Features:**
- The layout (a) highlights the importance of using multiple contacts to reduce impedance.
- The schematic (b) and circuit redrawn (c) diagrams emphasize the parallel configuration of the transistors, ensuring that the equivalent large transistor can handle higher currents.
- Labels such as Node 1, Node 2, VG, and the transistor identifiers (Q1 to Q4) are crucial for understanding the connections and operation of the circuit.

Overall, the image effectively demonstrates how multiple transistors can be combined in parallel to function as a single larger transistor, with careful consideration of layout and interconnections to optimize performance.
image_name:(b)
description:The circuit diagram shows four NMOS transistors (Q1, Q2, Q3, Q4) connected in parallel between Node 1 and Node 2, with a common gate voltage VG. Additionally, there are five other devices (J1, J2, J3, J4, J5) connected between Node 1 and VG.
image_name:(c)
description::The circuit diagram shows four NMOS transistors (Q1, Q2, Q3, Q4) connected in parallel between Node 1 and Node 2, with the gate voltage VG controlling all transistors. Additional components (J1 to J5) are connected between Node 1 and VG.

Fig. 2.18 Connecting four transistors in parallel to realize a single large transistor: (a) the layout, (b) the schematic drawn in the same relative positions as the layout, and (c) the circuit redrawn to make the parallel transistors more obvious.

Design rules also specify the minimum pitch between polysilicon interconnects, metal 1 interconnects, and metal 2 interconnects. These might be $2 \lambda, 2 \lambda$, and $3 \lambda$, respectively. Metal 2 requires a larger minimum pitch because it resides further from the silicon surface where the topography is less even. The minimum widths of poly, metal 1 , and metal 2 might also be $2 \lambda, 2 \lambda$, and $3 \lambda$, respectively.

This concludes our brief introduction to layout and design rules. In a modern process, many more design rules are used than those just described. However, the reasons for using and the methods of applying these rules is similar to that which has been described. Finally, note that when one does modern integrated circuit layout, the design rules are usually available to the layout CAD program and are automatically checked as layout progresses.

#### EXAMPLE 2.2

Consider the transistor shown in Fig. 2.18, where the total width of the four parallel transistors is $80 \lambda$, its length is $2 \lambda$, and $\lambda=0.2 \mu \mathrm{~m}$. Assuming node 2 is the source, node 1 is the drain, and the device is in the active region, find the source-bulk and drain-bulk capacitances given the parameters $C_{j}=0.24 \mathrm{fF} / \mu \mathrm{m}^{2}$ and $\mathrm{C}_{\mathrm{j} \text {-sw }}=0.2 \mathrm{fF} / \mu \mathrm{m}$. Also find the equivalent capacitances if the transistor were realized as a single device with source and drain contacts still evenly placed.

#### Solution

Starting with node 1 , the drain, we find that the areas of the junctions are equal to

$$
\mathrm{A}_{\mathrm{J} 2}=\mathrm{A}_{\mathrm{J} 4}=6 \lambda \times 20 \lambda=120 \lambda^{2}=4.8 \mu \mathrm{~m}^{2}
$$

Ignoring the gate side, the perimeters are given by

$$
P_{\mathrm{J} 2}=P_{\mathrm{J} 4}=6 \lambda+6 \lambda=12 \lambda=2.4 \mu \mathrm{~m}
$$

As a result, $\mathrm{C}_{\mathrm{db}}$ can be estimated to be

$$
\mathrm{C}_{\mathrm{db}}=2\left(\mathrm{~A}_{\mathrm{J} 2} \mathrm{C}_{\mathrm{j}}+\mathrm{P}_{\mathrm{J} 2} \mathrm{C}_{\mathrm{j}-\mathrm{sw}}\right)=3.3 \mathrm{fF}
$$

For node 2, the source, we have

$$
A_{J 1}=A_{J 5}=5 \lambda \times 20 \lambda=100 \lambda^{2}=4 \mu \mathrm{~m}^{2}
$$

and

$$
\mathrm{A}_{\mathrm{J} 3}=\mathrm{A}_{\mathrm{J} 2}=4.8 \mu \mathrm{~m}^{2}
$$

The perimeters are found to be

$$
P_{\mathrm{J} 1}=P_{\mathrm{J} 5}=5 \lambda+5 \lambda+20 \lambda=30 \lambda=6 \mu \mathrm{~m}
$$

and

$$
P_{\mathrm{J} 3}=P_{\mathrm{J} 2}=2.4 \mu \mathrm{~m}
$$

resulting in an estimate for $\mathrm{C}_{\mathrm{sb}}$ of

$$
\begin{aligned}
\mathrm{C}_{\mathrm{sb}} & =\left(\mathrm{A}_{\mathrm{J} 1}+\mathrm{A}_{\mathrm{J} 3}+\mathrm{A}_{\mathrm{J} 5}+\mathrm{WL}\right) \mathrm{C}_{\mathrm{j}}+\left(\mathrm{P}_{\mathrm{J} 1}+\mathrm{P}_{\mathrm{J} 3}+\mathrm{P}_{\mathrm{J} 5}\right) \mathrm{C}_{\mathrm{j}-\mathrm{sw}} \\
& =\left(19.2 \mu \mathrm{~m}^{2}\right) 0.24 \mathrm{fF} / \mu \mathrm{m}^{2}+(14.4 \mu \mathrm{~m}) 0.2 \mathrm{fF} / \mu \mathrm{m} \\
& =7.5 \mathrm{fF}
\end{aligned}
$$

It should be noted that, even without the additional capacitance due to the WL gate area, node 1 has less capacitance than node 2 since it has less area and perimeter.

In the case where the transistor is a single wide device, rather than four transistors in parallel, we find

$$
A_{J}=5 \lambda \times 80 \lambda=400 \lambda^{2}=16 \mu \mathrm{~m}^{2}
$$

and

$$
P_{J}=5 \lambda+5 \lambda+80 \lambda=90 \lambda=18 \mu \mathrm{~m}
$$

resulting in $\mathrm{C}_{\mathrm{db}}=7.4 \mathrm{fF}$ and $\mathrm{C}_{\mathrm{sb}}=9.0 \mathrm{fF}$. Note that in this case, $\mathrm{C}_{\mathrm{db}}$ is nearly twice what it is when four parallel transistors are used.

### 2.2.2 Planarity and Fill Requirements

Many aspects of the fabrication process require the circuit surface to be very planar. Generally, the optics used to achieve fine lithographic resolution in modern CMOS circuits, also ensure a very narrow depth of field for the lithography. Hence, any surface roughness will blur the resulting patterns. As illustrated in Fig. 2.13, depending upon the density of metal, contacts, and polysilicon, the thickness of a microcircuit can vary considerably. Hence, it is typically required that the fraction of an overall microcircuit covered by particular layers be constrained within some range. For example, it might be required that on the first layer of metal, between $10 \%$ and $35 \%$ of the entire area of a layout be filled. Since more advanced CMOS processes require more precise planarity of the circuit, these fill requirements become more stringent. Modern processes place requirements not only on the overall circuit, but also on any particular region (or "tile") of a circuit.

In analog circuits, following the minimum fill design rules can be difficult. Analog layouts are often dominated by relatively large passive components such as resistors and capacitors, which leave many metal layers unused. A typical solution is to add superfluous "dummy" metal, polysilicon, etc. to the layout. This process is automated by many CAD tools, but analog designers may wish to tightly control or at least monitor the process to ensure the resulting dummy fill does not introduce any undesirable parasitic effects.

### 2.2.3 Antenna Rules

Antennal rules are intended to prevent a microcircuit from being permanently damaged during manufacture by static charges that develop on conductors in the circuit. An example is illustrated in Fig. 2.19. During the manufacturing process, before the creation of Metal 2, the circuit shown in Fig. 2.19(a) will look like Fig. 2.19(b). As it
image_name:(a)
description:The diagram illustrates the risk of oxide breakdown due to static charge accumulation on the polysilicon gate during manufacturing. Antenna rules are used to prevent damage by providing a discharge path through a diode, as shown in part (c). The diagram shows the progression from (a) to (c) with the introduction of Metal 2 and the potential for charge accumulation.
image_name:(b)
description:The diagram illustrates the risk of oxide breakdown due to static charge accumulation during the manufacturing process, specifically before the creation of Metal 2. Antenna rules are applied to prevent damage by providing a discharge path through diodes.
image_name:(c)
description:The diagram illustrates the evolution of a microcircuit during the manufacturing process. In part (c), a diode is connected to provide a discharge path for static charges that may accumulate on the polysilicon gate, preventing oxide breakdown and potential damage. This is an example of an antenna rule implementation to protect the circuit.

Fig. 2.19 During the manufacturing process, before the creation of Metal 2, the circuit cross-sedion shown in (a) will look like (b). If a large static charge develops on the polysilicon gate at this time, the gate oxide can be damaged. Antenna rules ensure that nodes at risk of sustaining this type of damage are connected to a diode to provide a discharge path, as shown in (c).
passes through the various fabrication steps, a significant static electric charge may develop on the node connected to the polysilicon gate. Since this node is completely isolated, the charge gives rise to static electric fields, which can have high intensity across the very thin gate oxide. If sufficient charge builds up, the oxide can break down. Antenna rules ensure that nodes at risk of sustaining this type of damage are connected to a diode from the very start of the manufacturing process. The diode is reverse biased during circuit operation, and therefore has no effect other than introducing some junction capacitance, but it provides a discharge path for any charge that may accumulate during manufacture, as shown in Fig. 2.19(c).

### 2.2.4 Latch-Up

Latch-up is a destructive phenomenon in CMOS integrated circuits that can occur when there are relatively large substrate or well currents or, equivalently, large substrate or well voltage drops, that might be caused by capacitive coupling. These triggering voltage drops often occur when power is first applied to a CMOS integrated circuit.

A latched-up circuit is equivalent to a turned-on silicon-controlled rectifier (SCR) between the power supply and ground. This SCR effectively short-circuits the power supplies on the microcircuit and, unless the supply-current is limited, irreparable damage will probably occur (such as a fused open bonding wire or interconnect line).

To understand latch-up, consider the cross section of the CMOS inverter shown in Fig. 2.20 with the parasitic bipolar transistors $Q_{1}$ and $Q_{2}$. Transistor $Q_{1}$ is a lateral npn, with the base being formed by the $\mathrm{p}^{-}$substrate, whereas $Q_{2}$ is a vertical pnp, with the base being formed by the $n$-well region. The parasitic bipolar circuit has been redrawn in Fig. 2.21 along with some of the parasitic resistances due to the lightly doped substrate and well regions. The circuit realizes two cross-coupled common-emitter amplifiers in a positive feedback loop. This is the equivalent circuit of an SCR, which is sometimes referred to as a crowbar switch.

Normally, the parasitic bipolar transistors are off, and the voltages are as shown in Fig. 2.21(a). However, if latch-up is somehow triggered, they turn on when the loop gain is larger than unity, and as a result, the voltages are approximately those shown in Fig. $2.21(b)$. This turned-on SCR effectively places a short-circuit across the power-supply voltage and pulls $\mathrm{V}_{\mathrm{DD}}$ down to approximately 0.9 V . If the power supply does not have a current limit, then excessive current will flow and some portion of the microcircuit may be destroyed.

To prevent latch-up, the loop gain of the cross-coupled bipolar inverters is kept less than unity primarily by having low-impedance paths from the power supplies to the substrate and well resulting in low $R_{n}$ and $R_{p}$. Hence, with an n -well technology, the design rules normally specify a maximum distance between any place in the n -channel region of the microcircuit and the closest $\mathrm{p}^{+}$junction, which connects the substrate to ground.
image_name:Fig. 2.20 Cross section of a CMOS inverter with superimposed schematic of the parasitic transistors responsible for the latch-up mechanism
description:The image depicts a cross-sectional view of a CMOS inverter with superimposed schematic representations of the parasitic transistors responsible for the latch-up mechanism. The diagram illustrates the following components and structures:

1. **Components and Structure:**
- **n-well and p-substrate:** The diagram shows an n-well region embedded in a p-type substrate. This is typical in CMOS technology where p-channel MOSFETs are placed in n-wells.
- **Parasitic Transistors (Q1 and Q2):** Two parasitic bipolar transistors are shown, labeled as Q1 and Q2. Q1 is an npn transistor, and Q2 is a pnp transistor. These transistors are intrinsic to the CMOS structure and can lead to latch-up if not properly managed.
- **p+ and n+ regions:** These are heavily doped regions that form the source and drain of the MOSFETs and are also part of the parasitic transistor structure.

2. **Connections and Interactions:**
- **Ground and VDD Connections:** The diagram highlights the connections to ground (GND) and the supply voltage (VDD). These are crucial for the operation of the CMOS inverter.
- **Resistances (Rp and Rn):** Rp and Rn are shown as resistors in the diagram, representing the resistive paths in the substrate and n-well, respectively. These resistances are critical in determining the susceptibility of the circuit to latch-up.
- **Signal Flow:** The input signal (Vin) is applied at the gate, affecting the operation of the MOSFETs and the parasitic transistors.

3. **Labels, Annotations, and Key Features:**
- **GND and VDD:** Labeled to show the power and ground connections.
- **Vin:** The input voltage applied to the gate of the MOSFETs.
- **p+ and n+ junctions:** Labeled to indicate the heavily doped regions that form the source/drain of the transistors.
- **n-well and p- substrate labels:** These labels help identify the regions within the silicon structure.
- **Arrows indicating current flow:** Arrows are used to show the direction of current flow, which is essential for understanding the latch-up mechanism.

This cross-sectional diagram is a critical tool for understanding how latch-up can occur in CMOS inverters and the importance of design considerations to prevent it, such as minimizing the resistances Rp and Rn.

Fig. 2.20 Cross section of a CMOS inverter with superimposed schematic of the parasitic transistors responsible for the latch-up mechanism.
image_name:(a)
description:
[
name: Q1, type: NPN, ports: {C: b2, B: b1, E: GND}
name: Q2, type: PNP, ports: {C: VDD, B: b2, E: b1}
name: Rn, type: Resistor, value: Rn, ports: {N1: LOAD, N2: b2}
name: Rp, type: Resistor, value: Rp, ports: {N1: b1, N2: GND}
name: C1, type: Capacitor, value: C1, ports: {Np: Vin, Nn: b1}
]
extrainfo:The circuit diagram represents a latch-up scenario in a CMOS inverter, illustrating the parasitic bipolar transistors Q1 and Q2. The NPN transistor Q1 and the PNP transistor Q2 form a feedback loop that can lead to latch-up if not properly managed. The resistors Rn and Rp are part of the parasitic structure influencing the latch-up conditions. The capacitor C1 connects the input voltage Vin to the node b1, which is also connected to the base of Q1 and the emitter of Q2. The diagram highlights the importance of controlling the voltages and resistances in the circuit to prevent latch-up.
image_name:(b)
description:
[
name: Q1, type: NPN, ports: {C: b2, B: b1, E: GND}
name: Q2, type: PNP, ports: {C: b1, B: b2, E: VDD}
name: Rn, type: Resistor, value: Rn, ports: {N1: b2, N2: LOAD}
name: Rp, type: Resistor, value: Rp, ports: {N1: b1, N2: GND}
name: VDD, type: VoltageSource, value: 0.9V, ports: {Np: VDD, Nn: GND}
]
extrainfo:The circuit diagram illustrates the latch-up mechanism in a CMOS inverter. It includes parasitic bipolar transistors Q1 and Q2, and resistors Rp and Rn. The voltage source VDD is set to 0.9V.

Fig. 2.21 (a) The equivalent circuit of the parasitic bipolar transistors, and (b) the voltages after latch-up has occurred.

Similarly, in the p-channel regions, the maximum distance to the nearest $\mathrm{n}^{+}$junction, which connects the n wells to $\mathrm{V}_{\mathrm{DD}}$, is specified. In addition, any transistors that conduct large currents are usually surrounded by guard rings, as illustrated in Fig. 2.29. These guard rings are connections to the substrate for n -channel transistors, or to the n well for p -channel transistors, that completely surround the high-current transistors. Also, ensuring that the back of the die is connected to ground through a eutectic gold bond to the package header is helpful.

One of the best ways of preventing latch-up is to use an epitaxial process, especially one with highly doped buried layers. For example, if there is a $\mathrm{p}^{++}$substrate underneath the $\mathrm{p}^{-}$epitaxial layer in which the transistors are placed, device performance is only marginally affected but the highly conductive $\mathrm{p}^{++}$substrate has very little impedance to ground contacts and to the package header.

## 2.3 VARIABILITY AND MISMATCH

When integrated circuits are manufactured, a variety of effects cause the effective sizes and electrical properties of the components to differ from those intended by the designer. We may categorize these effects as being either systematic variations, process variations, or random variations.

### 2.3.1 Systematic Variations Including Proximity Effects

When lithographic techniques are used, a variety of two-dimensional effects can cause the effective sizes of the components to differ from the sizes of the glass layout masks. Some examples of these effects are illustrated in Fig. 2.22.

For example, Fig. 2.22(a) shows how an effective well area will typically be larger than its mask due to the lateral diffusion that occurs not just during ion implantation but also during later high-temperature steps, such as annealing. Another effect, known as overetching, occurs when layers such as polysilicon or metal are being etched. Figure 2.22(b), for example, shows overetching that occurs under the

Key Point: Systematic variations are those observed repeatedly and consistently, even when a circuit is being mass-produced. Generally, these may be avoided by proper layout techniques, although doing so may impose some penalty in terms of layout size or performance. Process variations are observed because the conditions of manufacture (temperature, concentration levels, etc.) can never be maintained precisely constant. These manifest as device parameters that differ from one sample of a circuit to the next. Random variations are statistical in nature and are present in every individual device. Hence, they may be observed as mismatch between two identically specified transistors fabricated under the same nominal conditions.
image_name:(a)
description:The image consists of three diagrams labeled (a), (b), and (c), each illustrating different two-dimensional effects in microcircuit fabrication that cause the realized components to differ from their intended layout sizes.

1. **Diagram (a):** This diagram depicts the effect of lateral diffusion under an SiO2 mask. It shows a cross-section of a semiconductor substrate with a well region. The SiO2 protection layer is indicated on top, and arrows show the direction of lateral diffusion occurring under the SiO2 mask. This diffusion causes the well to extend beyond the mask boundaries, affecting the size and performance of the component.

2. **Diagram (b):** This section illustrates the overetching effect on a polysilicon gate. The SiO2 protection layer is again visible, with a polysilicon gate beneath it. The overetching process results in the reduction of the polysilicon gate size compared to the mask layout. Arrows indicate the regions affected by overetching, showing how the gate becomes narrower than intended.

3. **Diagram (c):** This part shows a cross-section of an n-channel transistor viewed along the channel from the drain to the source. The diagram highlights the narrowing of the transistor channel width due to the presence of p+ field implants. The polysilicon gate is shown over the channel, and arrows indicate the narrowing effect on the channel width. This narrowing is a critical factor as it influences the electrical characteristics of the transistor.

Overall, these diagrams illustrate common fabrication issues in microelectronics, such as lateral diffusion, overetching, and channel narrowing, which contribute to variations between the designed and actual sizes of microcircuit components.
image_name:(b)
description:The image labeled "(b)" is a diagram illustrating the effect of overetching on a microcircuit component, specifically focusing on the polysilicon gate structure. The diagram is a cross-sectional view showing several key components:

1. **Components and Structure:**
- **SiO₂ Protection Layer:** This layer is depicted at the top, providing a protective barrier during the etching process.
- **Polysilicon Gate:** Beneath the SiO₂ layer, the polysilicon gate is shown. This is a critical component in transistor fabrication, acting as the gate electrode.
- **Overetching:** The diagram highlights the overetching effect, where the material is etched away beyond the intended dimensions, leading to a reduction in size of the polysilicon gate.

2. **Connections and Interactions:**
- The overetching is a process-related interaction that affects the size and shape of the polysilicon gate. This effect can lead to variations in the electrical characteristics of the transistor, as the gate's dimensions are crucial for controlling current flow.

3. **Labels, Annotations, and Key Features:**
- The diagram is labeled with arrows indicating the SiO₂ protection and the polysilicon gate.
- Annotations highlight the overetching effect, emphasizing how this process can alter the intended design dimensions.

Overall, the diagram serves to illustrate the impact of manufacturing variations on the physical dimensions of microcircuit components, specifically showing how overetching can affect the polysilicon gate size, potentially leading to performance variations in the final device.
image_name:(c)
description:The image labeled as Fig. 2.22(c) illustrates a cross-sectional view of an n-channel transistor, focusing on the effects of process variations on the transistor's physical dimensions. This diagram is part of a series that explains how different two-dimensional effects can cause the realized sizes of microcircuit components to differ from their intended layout sizes.

1. **Identification of Components and Structure:**
- The diagram shows a polysilicon gate, which is a critical component in the transistor structure. It is positioned over the channel region, which connects the drain and source of the transistor.
- The transistor channel is marked, indicating the path along which current flows when the transistor is active.
- The diagram also shows p+ field implants on either side of the channel, which are used to control the electrical characteristics of the transistor.

2. **Connections and Interactions:**
- The polysilicon gate is shown interacting with the channel, controlling the flow of current between the source and drain when a voltage is applied.
- The narrowing of the channel width is highlighted, which is a result of process variations and affects the electrical performance of the transistor.

3. **Labels, Annotations, and Key Features:**
- The polysilicon gate is clearly labeled, showing its position relative to the channel.
- "Transistor channel" is labeled to indicate the main conductive path.
- "Channel width narrowing" is annotated to highlight the reduction in channel width due to fabrication effects.
- The presence of p+ field implants is noted, which are used to enhance the transistor's performance by modifying the electric field distribution.

This diagram effectively illustrates the impact of fabrication processes on the physical dimensions of a transistor, emphasizing the deviations from the intended design due to various manufacturing effects.

Fig. 2.22 Various two-dimensional effects causing sizes of realized microcircuit components to differ from sizes of layout masks.
$\mathrm{SiO}_{2}$ protective layer at the polysilicon edges and causes the polysilicon layer to be smaller than the corresponding mask layout. A third effect is shown in Fig. 2.22(c), where an n -channel transistor is shown as we look along the channel from the drain to the source. The width of the transistor is defined by the width of the active region (as opposed to the width of the polysilicon line), and this width is determined by the separation of the isolation oxide between transistors (i.e. the field-oxide in a LOCOS process). The $\mathrm{p}^{+}$field implant under the field-oxide causes the effective substrate doping to be greater at the sides of the transistors than elsewhere. This increased doping raises the effective transistor threshold voltage near the sides of the transistors and therefore decreases the channel-charge density at the edges. The result is that the effective width of the transistor is less than the width drawn on the layout mask.

The features surrounding a device can also impact its electrical performance. For example, neighboring conductors give rise to parasitic capacitances in a circuit. However, there are some more subtle proximity effects. For example, when ion implantation is used for well formation, some incident atoms will scatter when striking near the edge of the photoresist, as shown in Fig. 2.23. As a result, the dopant concentration at the surface of the n -well is elevated near the well edge, gradually decreasing over a distance of $1 \mu \mathrm{~m}$ or more [Drennan, 2006]. Hence, transistors will have threshold voltages that vary considerably depending upon their location and orientation relative to

Ion implantation beam
image_name:Fig. 2.23
description:The diagram, labeled as Fig. 2.23, illustrates the well edge proximity effect caused by ion implantation. The main components depicted include a photoresist layer (labeled PR1), an n-well, and a p-type substrate (labeled p-). Below the photoresist is a silicon dioxide (SiO2) layer.

Vertical arrows represent the ion implantation beam directed towards the surface. These ions penetrate the photoresist and enter the n-well. Near the edge of the photoresist, some ions scatter, leading to a higher dopant concentration at the surface of the n-well near its edge. This scattering effect is shown by arrows deflecting off the edge of the photoresist and entering the n-well at an angle.

The diagram highlights the region where the dopant concentration is elevated, indicated by a circled area and labeled as 'Higher dopant concentration near well edge.' This effect is a result of the scattering of ions during the implantation process, causing a gradient in dopant concentration that decreases with distance from the well edge. This phenomenon affects the threshold voltages of transistors depending on their proximity to the well edge, which is a critical consideration in analog circuit design.

Fig. 2.23 The well edge proximity effect is caused by scattering during ion implantation.
a well edge. The conservative analog designer may layout all transistors some minimum distance from any well edge, perhaps as much as $3 \mu \mathrm{~m}$, to avoid this effect - a huge distance in manufacturing technologies capable of feature sizes smaller than 100 nm .
image_name:Fig. 2.24
description:The image labeled "Fig. 2.24" illustrates the effects of shallow-trench isolation (STI) on surrounding silicon and nearby transistor parameters. The diagram is a cross-sectional view of a semiconductor substrate with several components and annotations.

1. **Identification of Components and Structure:**
- **Polysilicon Gate:** The diagram shows multiple polysilicon gates positioned above the silicon substrate. These are represented as gray blocks on top of the silicon surface.
- **SiO2 (Silicon Dioxide):** The STI regions are filled with SiO2, depicted as hatched vertical sections that extend into the silicon substrate to isolate different regions.
- **n+ Regions:** Beneath the polysilicon gates, there are n+ doped regions, indicating where the source and drain of the transistors are located.

2. **Connections and Interactions:**
- The STI regions create a compressive stress on the surrounding silicon, which is indicated by arrows labeled "STI Stress" pointing towards the n+ regions. This stress affects the electrical properties of the silicon, influencing electron and hole mobility.
- The diagram does not show explicit electrical connections (such as wiring or PCB traces) but focuses on the physical and stress interactions within the silicon substrate.

3. **Labels, Annotations, and Key Features:**
- The labels "Polysilicon gate" and "SiO2" identify the key materials in the structure.
- "STI Stress" is annotated with arrows to indicate the direction and effect of the stress on the silicon lattice.
- The n+ regions are marked to show the areas of higher dopant concentration, essential for transistor operation.

Overall, the image highlights how the STI process impacts the mechanical and electrical characteristics of the silicon substrate, which is crucial for understanding how these factors influence transistor performance in analog circuit design.

$\mathrm{p}^{-}$

Fig. 2.24 Shallow-trench isolation (STI) places stress on the surrounding silicon effecting nearby transistor parameters.

Shallow-trench isolation can also impact the electrical properties of the surrounding silicon. The trench formation and filling places a compressive stress on the silicon lattice, as shown in Fig. 2.24. This compressive stress reduces electron mobility and increases hole mobility. It can also impact the rate of dopant diffusion, thereby influencing threshold voltage as well. Since the stress effects only those devices near the edge of the active OD regions, it can lead to mismatch between transistors that are not laid out identically. For example, if multiple transistors share the same active region they must be oriented so that they are both equidistant from the edge of the active region, and so that they both have the same orientation with respect to the edge (e.g., they should both have their source closer to the edge of the active region). A conservative approach is to always include dummy transistor structures close to the edge every active region, so that no active analog transistors are located close to an STI trench. In the most modern processes, two dummies may be required on each edge of the active regions [Drennan, 2006].

Key Point: The absolute sizes and electrical parameters of integrated circuit components can seldom be accurately determined. For best accuracy, larger objects are made out of several unit-sized components connected together, and the boundary conditions around all objects should be matched, even when this means adding extra unused components.

These examples illustrate typical systematic effects, but many other second-order effects influence the realized components. These other effects include those caused by boundary conditions of an object, the size of the opening in a protective layout through which etching occurs, and the unevenness of the surface of the microcircuit [Maloberti, 1994]. For these reasons, the absolute sizes and electrical parameters of integrated circuit components can seldom be accurately determined. For best accuracy, larger objects are made out of several unit-sized components connected together, and the boundary conditions around all objects should be matched, even when this means adding extra unused components. Inaccuracies also affect the ratios of sizes when the ratio is not unity, although to a lesser degree.

### 2.3.2 Process Variations

Variations in the manufacturing process also influence device performance. For example, the temperatures under which various fabrication steps are performed and the concentration of elements introduced will influence transistor parameters. In spite of intense effort to minimize these variations, they persist and are significant. For example, the oxide thickness may vary by $5 \%$ and dopant concentrations by $10 \%$ [Tsividis, 2002]. These translate into device parameter variations equivalent to, for example, 100 mV changes in $\mathrm{V}_{\mathrm{t}}$, $15 \%$ for $\mathrm{K}^{\prime}$, and $5 \%$ for junction capacitances. All designs will be subject to these process variations regardless of how much care is taken to eliminate the systematic variations described above.

To see the effect of process variations during design, several different device models are used for the analysis and simulation of any analog circuit. Each model represents a different combination of device parameter variations that may be expected to occur during mass production of the design. For example, since PMOS and NMOS devices often are subjected to different channel implantation steps, process variations may cause the PMOS and NMOS threshold voltages to vary either up or down independently of one another. Taking into account variations in all process parameters quickly leads to a huge number of permutations. In addition, a practical design will be
expected to operate effectively over a range of temperatures (which in turn influences carrier mobility and other device parameters), and over a range of different supply voltages. Collectively, these are referred to as PVT (pro-cess-voltage-temperature) variations, and are often a bane to analog designers.

#### EXAMPLE 2.3

Consider a NMOS transistor biased with $\mathrm{V}_{\mathrm{GS}}=0.65 \mathrm{~V}$ and with the device parameters listed for the $0.18-\mu \mathrm{m}$ CMOS process in Table 1.5. How much does the drain current change with a 100 mV increase in $\mathrm{V}_{\mathrm{tn}}, 5 \%$ decrease in $\mathrm{C}_{\mathrm{ox}}$, and $10 \%$ decrease in $\mu_{n}$ ?
image_name:SPICE!
description:The image contains a small graphic with a drawing of a pepper on the left side. Next to the pepper, there is text that reads: 'SPICE! This may be simulated using the corner models on the text website.' The image suggests that the simulation of the described scenario can be conducted using SPICE (Simulation Program with Integrated Circuit Emphasis) software, and that corner models available on a specific website can be used for this purpose."

#### Solution

Note that since Table 1.5 indicates a threshold voltage of $\mathrm{V}_{\mathrm{tn}}=0.45 \mathrm{~V}$, a $\mathrm{V}_{\mathrm{t}}$ increase of 100 mV represents a $50 \%$ decrease in $\mathrm{V}_{\text {eff }}$, from 200 mV to 100 mV . Adopting a simple square law device model, a great simplification considering the large process variations present on $\lambda$, the nominal device drain current is given by

$$
\mathrm{I}_{\mathrm{D}}=\frac{1}{2} \mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}} \frac{\mathrm{~W}}{\mathrm{~L}} \mathrm{~V}_{\mathrm{eff}}^{2}
$$

Accounting for all of the process variations, the new drain current will be

$$
\mathrm{I}_{\mathrm{D}, \mathrm{new}}=\frac{1}{2}\left(0.9 \mu_{\mathrm{n}}\right)\left(0.95 \mathrm{C}_{\mathrm{ox}}\right) \frac{\mathrm{W}}{\mathrm{~L}}\left(0.5 \mathrm{~V}_{\mathrm{eff}}\right)^{2}=\left(0.9 \cdot 0.95 \cdot 0.5^{2}\right) \mathrm{I}_{\mathrm{D}}=0.214 \cdot \mathrm{I}_{\mathrm{D}}
$$

representing a $79 \%$ decrease in drain current. Much of this is a result of the $V_{t}$ variation.

The combination of parameter variations considered in Example 2.3 is colloquially referred to as a "slow process corner" because those variations, combined with larger-than-expected junction capacitances, result in digital circuits that are slower than what may be nominally expected from a particular manufacturing process. Designers also consider a "fast" process corner exhibiting reduced values of $\mathrm{V}_{\mathrm{t}}$ and junction capacitances and increased $\mathrm{C}_{\mathrm{ox}}$ and $\mu$. These slow and fast corners, when combined with high and low operating tem-

Key Point: Practical variations in transistor parameters, supply voltage, and temperature (PVT variations) can be a bane to analog designers trying to reliably meet specific performance criteria.
peratures, and low and high supply voltages respectively, are often considered the extreme cases under which a digital circuit must operate. Unfortunately, analog performance metrics may actually be worst under some different, but equally likely, combination of process parameter variations.

### 2.3.3 Random Variations and Mismatch

Even in the absence of any process variations, there are limits on the accuracy with which devices can be fabricated. For example, the number of dopants present in the channel region of modern minimum-size transistors may be as few as 100. It is impossible to ensure that two transistors will have the exact same number and location of dopants, even when they have identical layouts and are fabricated under identical conditions. As the number of dopants or their relative location varies randomly, so do transistor parameters such as threshold voltage. Channel dopants are just one source of uncertainty-there are several such factors that contribute to random variations in device parameters.

A fundamental analysis of the statistical variation of device parameters on a wafer [Pelgrom, 1989] predicts a Gaussian distribution with variance

$$
\begin{equation*}
\sigma^{2}(\Delta P)=\frac{A_{P}^{2}}{W L}+S_{P}^{2} D^{2} \tag{2.13}
\end{equation*}
$$

where $\Delta P$ is the difference in some device parameter $P$ between two devices spaced a distance $D$ apart, $W$ and $L$ are the dimensions of the device, and $A_{p}$ and $S_{p}$ are proportionality constants usually obtained from experimental measurements. Equation (2.13) captures only random variations in device parameters, not the systematic or process variations already described. The expression is general and can be applied to transistors, capacitors, resistors, etc. although it manifests itself slightly differently in different model parameters. For example, sometimes the variation is in absolute terms, and sometimes in relative terms.

The most important random variations in a MOSFET may be modelled by variations in $\mathrm{V}_{\mathrm{t}}$ (threshold voltage) and $\mathrm{K}^{\prime}=\mu_{\mathrm{n}} \mathrm{C}_{\mathrm{ox}}(\mathrm{W} / \mathrm{L})$.

$$
\begin{align*}
\sigma^{2}\left(\mathrm{~V}_{\mathrm{t} 0}\right) & =\frac{\mathrm{A}_{\mathrm{vt} 0}^{2}}{\mathrm{WL}}+\mathrm{S}_{\mathrm{Vt} 0}^{2} \mathrm{D}^{2}  \tag{2.14}\\
\frac{\sigma^{2}\left(\mathrm{~K}^{\prime}\right)}{\mathrm{K}^{\prime 2}} & =\frac{\mathrm{A}_{\mathrm{K}^{\prime}}^{2}}{\mathrm{WL}}+\mathrm{S}_{\mathrm{K}^{\prime}}^{2} \mathrm{D}^{2} \tag{2.15}
\end{align*}
$$

Although there is some debate in this regard, it is generally conservatively assumed that statistical variations in $\mathrm{V}_{\mathrm{t}}$ and $\mathrm{K}^{\prime}$ are uncorrelated. These expressions clearly illustrate the need to closely space devices whose mismatch is of concern to us. Prime examples are differentially paired transistors and current mirroring transistors. Assuming this is done, the area dependent term will dominate and is therefore our focus.

#### Mismatch in Transistors with the Same $V_{G S}$

Transistors biased with the same gate-source voltage will have currents that vary as follows [Kinget, 2005]:

$$
\begin{equation*}
\left(\frac{\sigma\left(\Delta \mathrm{I}_{\mathrm{D}}\right)}{\mathrm{I}_{\mathrm{D}}}\right)^{2}=\left(\frac{\mathrm{g}_{\mathrm{m}}}{\mathrm{I}_{\mathrm{D}}}\right)^{2} \sigma^{2}\left(\Delta \mathrm{~V}_{\mathrm{t}}\right)+\frac{\sigma^{2}\left(\Delta \mathrm{~K}^{\prime}\right)}{\mathrm{K}^{\prime 2}} \tag{2.16}
\end{equation*}
$$

Key Point: The parameters of devices that are closely spaced with identical layout exhibit a random variance inversely proportional to device area. In practice, the most important random variations in most analog circuits are $\mathrm{V}_{\mathrm{t}}$ mismatch.

This does not presume a square law and is therefore valid over all operating regions. Since both $\Delta V_{T}$ and $\Delta K^{\prime}$ are inversely proportional to the square root of device area, the overall relative current mismatch is also inversely proportional to the square root of the device area. Substituting (2.14) and (2.15) into (2.16) and assuming closely-spaced devices so we may neglect the terms with $\mathrm{D} \approx 0$,

$$
\begin{equation*}
\left(\frac{\sigma\left(\Delta I_{D}\right)}{I_{D}}\right)^{2}=\frac{1}{W L}\left[A_{V t o}^{2}\left(\frac{g_{m}}{I_{D}}\right)^{2}+A_{K^{\prime}}^{2}\right] \tag{2.17}
\end{equation*}
$$

Hence if we want to improve the current matching by a factor of 2 , we must quadruple the device area. This can be achieved, for example, by doubling both W and L .

[^0]:    1. In fact, there will be slightly fewer mobile carriers than the number of impurity atoms since some of the free electrons from the dopants have recombined with holes. However, since the number of holes of intrinsic silicon is much less than typical doping concentrations, this inaccuracy is small.
[^1]:    6. The drain and source regions are sometimes called diffusion regions or junctions for historical reasons. This use of the word junction
[^2]:    7. The current is actually conducted by negative carriers (electrons) flowing from the source to the drain. Negative carriers flowing
[^3]:    8. $\mathrm{V}_{\mathrm{G}}-\mathrm{V}_{\mathrm{CH}}(\mathrm{x})$ is the gate-to-channel voltage drop at distance x from the source end, with $\mathrm{V}_{\mathrm{G}}$ being the same everywhere in the gate,
[^4]:    9. Because of the body effect, the threshold voltage at the drain end of the transistor is increased, resulting in the true value of $\mathrm{V}_{\mathrm{DS} \text {-sat }}$ being slightly lower than $\mathrm{V}_{\text {eff }}$.
10. The active region may also be called the saturation region, but this can lead to confusion because in the case of bipolar transistors, the saturation region occurs for small $\mathrm{V}_{\mathrm{CE}}$, whereas for MOS transistors it occurs for large $\mathrm{V}_{\mathrm{DS}}$. Moreover, we shall see that the drain current does not truly saturate, but continues to increase slightly with increasing drain-source voltage.
[^5]:    11. In fact, JFETs intentionally modulate the conducting channel via a junction capacitance, hence their name: Junction Field-Effect Transistors.
12. For an $n$-channel transistor. For a $p$-channel transistor, $\gamma$ is proportional to the square root of $N_{D}$.
13. It is possible to realize depletion p-channel transistors, but these are of little value and seldom worth the extra processing involved. Depletion n -channel transistors are also seldom encountered in CMOS microcircuits, although they might be worth the extra processing involved in some applications, especially if they were in a well.
[^6]:    14. Whereas it is proportional to $\mathrm{I}_{\mathrm{C}}$ for a BJT.
[^7]:    1. Wells are doped regions that will contain one of the two types of transistors realized in a CMOS process. For example, wells that are n type contain p -channel transistors.
[^8]:    2. If annealing were done after deposition of a metal layer, the metal would melt.

Fig. 2.25 depicts a simple current mirror circuit where $\mathrm{V}_{\mathrm{GS}, 1}=\mathrm{V}_{\mathrm{GS}, 2}$. The currents will therefore vary with a standard deviation given by (2.17). Under a square law, $g_{m} / I_{D}=1 /\left(2 \mathrm{~V}_{\text {eff }}\right)$, so the first terms in (2.16) and (2.17) decrease with increasing $\mathrm{V}_{\text {eff }}$. In subthreshold, the first term approaches a constant maximum value of $g_{m} / I_{D}=q / n k T$. A plot of current mismatch representative of closely spaced $2 \mu \mathrm{~m} / 0.2 \mu \mathrm{~m}$ devices with the same $V_{G S}$ in a $0.18-\mu \mathrm{m}$ CMOS process is presented in Fig. 2.26. Clearly, $\mathrm{V}_{\mathrm{t}}{ }^{-}$ mismatch is the dominant source of error except at impractically large values of $\mathrm{V}_{\text {eff }}=\mathrm{V}_{\mathrm{GS}}-\mathrm{V}_{\mathrm{t}}$. This remains true even for large-area devices since both contributions are inversely proportional to device area, WL.
image_name:Fig. 2.25
description:
[
name: Q1, type: NMOS, ports: {S: GND, D: VI, G: VI}
name: Q2, type: NMOS, ports: {S: GND, D: LOAD2, G: VI}
name: Iin, type: CurrentSource, ports: {Np: LOAD1, Nn: VI}
]
extrainfo:The circuit is a simple current mirror with two NMOS transistors Q1 and Q2. The input current Iin flows through Q1, and the mirrored current Iout flows through Q2. Both transistors share the same gate voltage VI, which is provided by the voltage source.

Fig. 2.25 A simple current mirror with mismatch.

#### EXAMPLE 2.4

Assuming a current mirror is to be biased with $\mathrm{V}_{\text {eff }}=0.4 \mathrm{~V}$, how large must the devices be in order to ensure the current mismatch has a standard deviation better than $1 \%$ ? Assume that $A_{\mathrm{vt} 0}=4 \mathrm{mV} \cdot \mu \mathrm{m}$ and $\mathrm{A}_{\mathrm{K}^{\prime}}=0.01 \mu \mathrm{~m}$.

#### Solution

From Fig. 2.26, the $2 \mu \mathrm{~m} / 0.2 \mu \mathrm{~m}$ device has a standard deviation of $3.2 \%$ at $\mathrm{V}_{\text {eff }}=0.4 \mathrm{~V}$. This will decrease with $\sqrt{\mathrm{WL}}$. Hence the device must be made $3.2^{2}=10.2$ times larger in area. For example, each device could be sized $6.5 \mu \mathrm{~m} / 0.65 \mu \mathrm{~m}$.

Fig. 2.26 considers two transistors of fixed size with the same value of $\mathrm{V}_{\mathrm{GS}}$ and a drain current $\mathrm{I}_{\mathrm{D}}$ that varies with $\mathrm{V}_{\text {eff }}$, in which case the best matching is obtained by selecting a large value of $\mathrm{V}_{\text {eff }}$ where the impact of $\mathrm{V}_{\mathrm{t}}$
image_name:Fig. 2.26
description:The graph in Fig. 2.26 is a plot of current mismatch, represented as \( \sigma(\Delta I/I) \) in percentage, versus the effective gate-source voltage \( V_{gs} - V_t \) in volts. The graph is representative of a situation in a \( 0.18 \mu \mathrm{mCMOS} \) process, focusing on a simple current mirror setup.

**Type of Graph and Function:**
This is a line graph showing the relationship between the effective gate-source voltage and the percentage of current mismatch.

**Axes Labels and Units:**
- The x-axis represents the effective gate-source voltage \( V_{gs} - V_t \) in volts, ranging from approximately -400V to 800V.
- The y-axis represents the current mismatch \( \sigma(\Delta I/I) \) in percentage, ranging from 0% to 20%.

**Overall Behavior and Trends:**
- The graph shows a decreasing trend in the percentage of current mismatch as the effective gate-source voltage increases.
- Initially, at lower values of \( V_{gs} - V_t \), the mismatch is higher, around 18%, and it decreases steadily.
- As \( V_{gs} - V_t \) increases, the mismatch approaches a lower limit around 2%.

**Key Features and Technical Details:**
- The graph includes two contributions to the mismatch: \( V_t \) contribution and \( K' \) contribution.
- The \( V_t \) contribution is significant at lower \( V_{gs} - V_t \) values and decreases with increasing \( V_{gs} - V_t \).
- The \( K' \) contribution remains relatively constant and low across the range.
- The total mismatch is the combination of these contributions, shown as a solid line.

**Annotations and Specific Data Points:**
- The graph is annotated to show where the \( V_t \) contribution diminishes and the total mismatch stabilizes.
- There is a dashed line representing the \( K' \) contribution, which remains around 2% throughout.
- Key points are marked where \( V_t \) contribution and total mismatch are highlighted, indicating the transition from high to low mismatch values.

Fig. 2.26 A plot of current mismatch versus effective gate-source voltage for a simple current mirror. The values are representative of what one might see in a $0.18 \mu \mathrm{mCMOS}$ process with $\mathrm{A}_{\mathrm{vt} 0}=4 \mathrm{mV} \cdot \mu \mathrm{m}$ and $A_{K^{\prime}}=0.01 \mu \mathrm{~m}$ for devices sized $\mathrm{W} / \mathrm{L}=2 \mu \mathrm{~m} / 0.2 \mu \mathrm{~m}$.
variations is reduced. However, if instead the drain current $I_{D}$ is fixed and $V_{\text {eff }}$ varies with device aspect ratio $(W / L)$, then the best matching is obtained at low values of $\mathrm{V}_{\text {eff }}$ since that implies the largest devices.

#### Mismatch in Differential Pairs

image_name:Fig. 2.27 A simple NMOS differential pair
description:
[
name: Q1, type: NMOS, ports: {S: S1S2, D: LOAD1, G: V+, Body: GND}
name: Q2, type: NMOS, ports: {S: S1S2, D: LOAD2, G: V-, Body: GND}
name: I_bias, type: CurrentSource, ports: {Np: S1S2, Nn: GND}
]
extrainfo:The circuit is a simple NMOS differential pair with two NMOS transistors (Q1 and Q2) and a bias current source (I_bias). The sources of Q1 and Q2 are connected together and to the current source, forming a common-source configuration. The gates are driven by differential inputs (V+ and V-). The drains are connected to LOAD1 and LOAD2, respectively.

Fig. 2.27 A simple NMOS differential pair.

Consider the differential pair in Fig. 2.27 where transistors $Q_{1}$ and $Q_{2}$ are subject to random variations. When the differential pair input is zero, $\mathrm{V}^{+}=\mathrm{V}^{-}$and $\mathrm{V}_{\mathrm{GS}, 1}=\mathrm{V}_{\mathrm{GS}, 2}$, the currents will vary with a standard deviation given by (2.17). Hence the input offset voltage is given by

$$
\begin{equation*}
\sigma^{2}\left(\mathrm{~V}_{\mathrm{Os}}\right)=\frac{\sigma^{2}\left(\Delta \mathrm{I}_{\mathrm{D}}\right)}{\mathrm{g}_{\mathrm{m}}^{2}}=\frac{1}{\mathrm{WL}}\left[\mathrm{~A}_{\mathrm{Vt} 0}^{2}+\left(\frac{\mathrm{I}_{\mathrm{D}}}{\mathrm{~g}_{\mathrm{m}}}\right)^{2} \mathrm{~A}_{\mathrm{K}^{\prime}}^{2}\right] \tag{2.18}
\end{equation*}
$$

The first term will practically always dominate, particularly at the input of an opamp where the differential pair devices are sized to have high transconductance per unit of current, $g_{m} / I_{D}$.

#### EXAMPLE 2.5

If a differential pair is to be biased with $\mathrm{I}_{\text {bias }}=200 \mu \mathrm{~A}$, how large must the devices be sized to ensure the input offset is less than $1 \mathrm{mV} 99.8 \%$ of the time? Assume that $\mathrm{A}_{\mathrm{Vt}^{0}}=4 \mathrm{mV} \cdot \mu \mathrm{m}$ and $\mathrm{A}_{\mathrm{K}^{\prime}}=0.01 \mu \mathrm{~m}$.

#### Solution

The specs require the input offset to have a standard deviation better than $1 \mathrm{mV} / 3=0.333 \mathrm{mV}$. Each device has a nominal drain current of $\mathrm{I}_{\mathrm{D}}=100 \mu \mathrm{~A}$. Assuming that the first term is dominant, equation (2.18) gives

$$
(0.333 \mathrm{mV})^{2} \cong \frac{(4 \mathrm{mV} \cdot \mu \mathrm{~m})^{2}}{\mathrm{WL}} \Rightarrow \mathrm{WL}=144 \mu \mathrm{~m}^{2}
$$

For example, if the gate length is $L=0.5 \mu \mathrm{~m}$, the device widths must be $\mathrm{W}=288 \mu \mathrm{~m}$.

#### Mismatch in Transistors with Same Currents

image_name:Fig. 2.28
description:
[
name: V_BIAS, type: VoltageSource, value: V_BIAS, ports: {Np: V_BIAS, Nn: GND}
name: Q1, type: NMOS, ports: {S: P1, D: d1d2, G: V_BIAS}
name: Q2, type: NMOS, ports: {S: P2, D: d1d2, G: V_BIAS}
]
extrainfo:The circuit includes two NMOS transistors biased with the same current I_D. The gate-source voltage differences are labeled as V_GS,1 and V_GS,2. The voltage source V_BIAS is connected to the gate of both transistors and serves as a bias voltage. The drain of Q2 is connected to node d1d2.

Shown in Fig. 2.28, transistors biased with the same currents will have gate-source voltages that vary as follows:

$$
\begin{align*}
\sigma^{2}\left(\Delta \mathrm{~V}_{\mathrm{GS}}\right) & =\sigma^{2}\left(\Delta \mathrm{~V}_{\mathrm{T}}\right)+\left(\frac{\sigma\left(\Delta \mathrm{K}^{\prime}\right)}{\mathrm{K}^{\prime}}\right)^{2}\left(\frac{\mathrm{I}_{\mathrm{D}}}{\mathrm{~g}_{\mathrm{m}}}\right)^{2} \\
& =\frac{1}{\mathrm{WL}}\left[\mathrm{~A}_{\mathrm{Vtt}^{2}}\left(\frac{\mathrm{~g}_{\mathrm{m}}}{\mathrm{I}_{\mathrm{D}}}\right)^{2}+\mathrm{A}_{\mathrm{K}^{\prime}}^{2}\right] \tag{2.19}
\end{align*}
$$

Fig. 2.28 Transistors biased with identical currents.
where it is assumed in the second line that the devices are closely spaced. Again, $\mathrm{V}_{\mathrm{t}}$-variations are likely to dominate in practice. This may be of interest in knowing how much headroom is available at a particular point in a circuit.

## 2.4 ANALOG LAYOUT CONSIDERATIONS

When one designs analog circuits, several important layout issues should be considered to realize high-quality circuits. Firstly, the layout should avoid sources of systematic variation which will cause device parameters to deviate from their expected values. Second, good layout practices will minimize noise and outside interference in the circuit.

### 2.4.1 Transistor Layouts

Transistors in analog circuits are typically much wider than transistors in digital circuits. For this reason, they are commonly laid out using multi-ple-gate fingers similar to the layout shown in Fig. 2.18. When precision matching between transistors is required, then not only should the individual transistors be realized by combining copies of a single-sized unit transistor, but the fingers for one transistor should be interdigitated with the fingers of the second transistor. Specifically, a common-centroid layout is one where the fingers are ordered so that a linear gradient across

Key Point: In a common centroid layout, any linear gradient in electrical properties across the chip effects two or more devices equally. This is achieved by dividing each device into smaller equal-sized units, and arranging the units so that all devices have the same mean position ("centroid").
the integrated circuit in any device parameter, such as the temperature or the gate-oxide thickness, has zero net effect on device performance. This is achieved by ensuring the mean position of the devices are the same. An example of a common-centroid layout for the two identically matched transistors in Fig. 2.27 whose sources are connected is shown in Fig. 2.29 in simplified form [O'Leary, 1991; Maloberti, 1994]. Each of the two transistors
image_name:Fig. 2.29
description:The diagram shows a common-centroid layout for a differential source-coupled pair. It is symmetrical in both x and y axes, designed to minimize nonidealities like opamp input-offset voltage errors. The transistors are composed of four separate fingers connected in parallel, ensuring that any gradients across the microcircuit affect both transistors equally. The layout includes dummy structures to maintain symmetry.

Fig. 2.29 A common-centroid layout for the differential source-coupled pair in Fig. 2.27.
is composed of four separate transistor fingers connected in parallel. The layout is symmetric in both the x and y axes, and any gradients across the microcircuit would affect both $M_{1}$ and $M_{2}$ in the same way. This layout technique greatly minimizes nonidealities such as opamp input-offset voltage errors when using a differential pair in the input stage of an opamp. Also note that inside the structure, the fingers occur in doubles-two for $\mathrm{M}_{2}$, two for $M_{1}$, two for $\mathrm{M}_{2}$, and so on. This permits the use of only 2 drain junctions for 4 fingers, reducing the capacitance on that node. The drain connections for each transistor are routed towards the side of the transistor opposite the gate routing. This minimizes parasitic gate-drain (Miller) capacitance, which has an important influence in circuit bandwidth. For the greatest accuracy, only the inside fingers are active. Outside, or dummy, fingers are included only for better matching accuracy and have no other function. The gates of these dummy fingers are normally connected to the most negative power-supply voltage to ensure they are always turned off (or they are connected to the positive power supply in the case of p -channel transistors). A ring of contacts, called a guard ring, encircles the transistor OD region providing a low resistance connection to the body terminal under the transistors.

When current mirrors with ratios other than unity are required, again, each of the individual transistors should be realized from a single unit-sized transistor. For example, if a current ratio of 1:2 were desired, then the input transistor might be made from four fingers, whereas the output transistor might be realized using eight identical fingers.

### 2.4.2 Capacitor Matching

Very often, analog circuits require precise ratios of capacitors. Ideally, capacitor size is given by

$$
\begin{equation*}
\mathrm{C}_{1}=\frac{\varepsilon_{\mathrm{ox}}}{\mathrm{t}_{\mathrm{ox}}} \mathrm{~A}_{1}=\mathrm{C}_{\mathrm{ox}} \mathrm{x}_{1} \mathrm{y}_{1} \tag{2.20}
\end{equation*}
$$

The major sources of errors in realizing capacitors are due to overetching (which causes the area to be smaller than the area of the layout masks) and an oxide-thickness gradient across the surface of the microcircuit. The former effect is usually dominant and can be minimized by realizing larger capacitors from a parallel combination of smaller, unit-sized capacitors, similar to what is usually done for transistors. For example, to realize two capacitors that have a ratio of $4: 6$, the first capacitor might be realized from four unit-sized capacitors, whereas the second capacitor might be realized by six unit-sized capacitors. Errors due to the gradient of the oxide thickness can then be minimized by interspersing the unit-sized capacitors in a common-centroid layout so the gradient changes affect both capacitors in the same way. Since oxide-thickness variations are not usually large in a reasonably small area, this common-centroid layout is reserved for situations where very accurate capacitors are required.

If only unit-sized capacitors are used, then any overetching will leave the capacitor ratio unaffected. Thus, good designers strive to realize circuits in which only unit-sized capacitors are needed. Unfortunately, this situation is not always possible. When it is not, overetching error can still be minimized by realizing a nonunit-sized capacitor with a specific perimeter-to-area ratio. To determine the correct ratio, first note that the error due to overetching is roughly proportional to the perimeter of the capacitor. Specifically, if we assume that a capacitor has an absolute overetching given by $\Delta e$ and that its ideal dimensions are given by $x_{1}$ and $y_{1}$, then its true dimensions are given by $x_{1 a}=x_{1}-2 \Delta e$ and $y_{1 a}=y_{1}-2 \Delta e$, and the true capacitor size is given by

$$
\begin{equation*}
C_{a}=C_{0 x} x_{1 a} y_{1 a}=C_{o x}\left(x_{1}-2 \Delta e\right)\left(y_{1}-2 \Delta e\right) \tag{2.21}
\end{equation*}
$$

This situation is illustrated in Fig. 2.30. Thus, the error in the true capacitance is given by

$$
\begin{equation*}
\Delta C_{t}=C_{o x} x_{1 a} y_{1 a}-C_{o x} x_{1} y_{1}=C_{o x}\left[-2 \Delta e\left(x_{1}+y_{1}\right)+4 \Delta e^{2}\right] \tag{2.22}
\end{equation*}
$$

When this error is small, then the second-order error term can be ignored and (2.22) can be approximated by

$$
\begin{equation*}
\Delta C_{t} \cong-2 \Delta e\left(x_{1}+y_{1}\right) C_{o x} \tag{2.23}
\end{equation*}
$$

The relative error in the capacitor is therefore given by

$$
\begin{equation*}
\varepsilon_{\mathrm{r}}=\frac{\Delta \mathrm{C}_{\mathrm{t}}}{\mathrm{C}_{\text {ideal }}} \cong \frac{-2 \Delta \mathrm{e}\left(\mathrm{x}_{1}+\mathrm{y}_{1}\right)}{\mathrm{x}_{1} \mathrm{y}_{1}} \tag{2.24}
\end{equation*}
$$

Thus, the relative capacitor error is approximately proportional to the negative of the ratio of the ideal perimeter to the ideal area (assuming only small errors exist, which is reasonable since, if the errors were not small, then that capacitor sizing would probably not be used). When we realize two capacitors that have different sizes, usually the ratio of one capacitor to the other is important, rather than their absolute sizes. This ratio is given by

$$
\begin{equation*}
\frac{\mathrm{C}_{1 \mathrm{a}}}{\mathrm{C}_{2 \mathrm{a}}}=\frac{\mathrm{C}_{1}\left(1+\varepsilon_{\mathrm{r} 1}\right)}{\mathrm{C}_{2}\left(1+\varepsilon_{\mathrm{r} 2}\right)} \tag{2.25}
\end{equation*}
$$

image_name:Fig. 2.30 Capacitor errors due to overetching
description:The image labeled "Fig. 2.30 Capacitor errors due to overetching" illustrates the effect of overetching on the size of a capacitor. The diagram is a schematic representation showing both the ideal and actual dimensions of a capacitor affected by overetching.

1. **Identification of Components and Structure:**
- The diagram shows a rectangular capacitor with two sets of dimensions. The outer rectangle represents the ideal capacitor size, while the inner rectangle represents the true capacitor size after overetching.
- The dimensions of the ideal capacitor are labeled as \(x_1\) and \(y_1\) for width and height, respectively.
- The dimensions of the true capacitor (after overetching) are \(x_1 - 2\Delta e\) and \(y_1 - 2\Delta e\).

2. **Connections and Interactions:**
- The diagram does not depict any electrical connections or interactions, as it focuses on the geometric aspect of capacitor fabrication.
- The focus is on how the physical dimensions change due to the manufacturing process, specifically overetching, which reduces the effective size of the capacitor.

3. **Labels, Annotations, and Key Features:**
- \(\Delta e\) is used to denote the amount of material removed during the overetching process from each side of the capacitor.
- Arrows indicate the direction of measurement for both the ideal and true sizes, providing a visual comparison.
- The diagram clearly labels the ideal capacitor size and the true capacitor size, highlighting the discrepancy caused by overetching.

Overall, the diagram serves as a visual explanation of how overetching affects capacitor dimensions, emphasizing the importance of considering such errors in the design and manufacturing process.

Fig. 2.30 Capacitor errors due to overetching.

If the two capacitors have the same relative errors (i.e., $\varepsilon_{\mathrm{r} 1}=\varepsilon_{\mathrm{r} 2}$ ), then their true ratio is equal to their ideal ratio even when they are not the same sizes. Using (2.24), we see that the relative errors are the same if they both have the same perimeter-to-area ratio. This leads to the following result: To minimize errors in capacitor ratios due to overetching, their perimeter-to-area ratios should be kept the same, even when the capacitors are different sizes.

Normally, the unit-sized capacitor will be taken square. When a non-unit-sized capacitor is required, it is usually set to between one and two times the unit-sized capacitor and is rectangular in shape, so that it has the same number of corners as the unit-sized capacitor. Defining K to be a desired non-unit-sized capacitor ratio, we have

$$
\begin{equation*}
\mathrm{K} \equiv \frac{\mathrm{C}_{2}}{\mathrm{C}_{1}}=\frac{\mathrm{A}_{2}}{\mathrm{~A}_{1}}=\frac{\mathrm{x}_{2} \mathrm{y}_{2}}{\mathrm{x}_{1}^{2}} \tag{2.26}
\end{equation*}
$$

where $C_{1}, A_{1}$, and $x_{1}$ represent the capacitance, area, and side-length of a unit-sized capacitor, respectively. Variables $C_{2}, A_{2}, x_{2}$, and $y_{2}$ are similarly defined, except this non-unit-sized capacitor is now rectangular. Equating the ratios of the perimeters-to-areas implies that

$$
\begin{equation*}
\frac{P_{2}}{A_{2}}=\frac{P_{1}}{A_{1}} \tag{2.27}
\end{equation*}
$$

where $P_{1}$ and $P_{2}$ represent the perimeters of the two capacitors. Rearranging (2.27), we have

$$
\begin{equation*}
\frac{P_{2}}{P_{1}}=\frac{A_{2}}{A_{1}}=K \tag{2.28}
\end{equation*}
$$

which implies that K can also be written as the ratio of perimeters,

$$
\begin{equation*}
\mathrm{K}=\frac{\mathrm{x}_{2}+\mathrm{y}_{2}}{2 \mathrm{x}_{1}} \tag{2.29}
\end{equation*}
$$

This can be rearranged to become

$$
\begin{equation*}
\mathrm{x}_{2}+\mathrm{y}_{2}=2 \mathrm{Kx} \mathrm{x}_{1} \tag{2.30}
\end{equation*}
$$

Also rearranging (2.26), we have

$$
\begin{equation*}
\mathrm{x}_{2}=\frac{\mathrm{Kx}}{\mathrm{y}_{2}^{2}} \tag{2.31}
\end{equation*}
$$

image_name:Fig. 2.31 A capacitor layout
description:The image titled "Fig. 2.31 A capacitor layout" shows a schematic representation of a capacitor layout with two sets of capacitors. The layout is designed to match two capacitors of different sizes, specifically 4 units and 2.314 units, where each unit-sized capacitor measures 10 micrometers by 10 micrometers.

1. **Identification of Components and Structure:**
- The layout consists of four square capacitors arranged in a 2x2 grid. Each square represents a capacitor with dimensions of 10 micrometers by 10 micrometers.
- The capacitors are depicted as grey squares with black borders, indicating their physical boundaries.

2. **Connections and Interactions:**
- There are no visible connections such as wiring or PCB traces in the image. The focus is on the physical arrangement of the capacitors rather than their electrical connections.
- The layout suggests that these capacitors are placed in close proximity to achieve a specific perimeter-to-area ratio.

3. **Labels, Annotations, and Key Features:**
- The image includes annotations indicating the dimensions of the capacitors (10 micrometers) and the relative position (0 micrometers) from a reference point.
- There is no explicit indication of signal flow or current directions, as the emphasis is on the geometric configuration.

The layout is a visual representation of how capacitors can be arranged to achieve matching perimeter-to-area ratios, which is crucial for certain electrical characteristics in integrated circuits.

4 units
image_name:Fig. 2.31
description:The image depicts a capacitor layout intended to achieve matching perimeter-to-area ratios for two different capacitors. The layout is part of Fig. 2.31, which illustrates how capacitors can be arranged to meet specific electrical characteristics in integrated circuits.

1. **Identification of Components and Structure:**
- The image shows two capacitors, each represented as rectangular blocks.
- The first capacitor is a square with each side measuring 10 micrometers, indicating a unit-sized capacitor.
- The second capacitor is a rectangle with dimensions of 10 micrometers by 19.6 micrometers.

2. **Connections and Interactions:**
- There are no visible connections such as wiring or PCB traces in the image. The focus is purely on the geometric arrangement of the capacitors.
- The capacitors are placed adjacent to each other, likely to facilitate a parallel configuration, although this is not explicitly shown in the diagram.

3. **Labels, Annotations, and Key Features:**
- The dimensions of each capacitor are clearly labeled next to the respective rectangles: "10 μm" for the square capacitor and "10 μm" by "19.6 μm" for the rectangular capacitor.
- The layout is part of an example (Example 2.6) that demonstrates how to match two capacitors of sizes 4 units and 2.314 units, where a unit-sized capacitor measures 10 micrometers by 10 micrometers.
- The perimeter-to-area ratio matching is a key feature of this layout, although the specific calculations are not detailed in the image itself.

$6.72 \mu \mathrm{~m}$
2.314 units

Fig. 2.31 A capacitor layout with equal perimeter-to-area ratios of 4 units and 2.314 units.

#### EXAMPLE 2.6

Show a layout that might be used to match two capacitors of size 4 and 2.314 units, where a unit-sized capacitor is $10 \mu \mathrm{~m} \times 10 \mu \mathrm{~m}$.

#### Solution

Four units are simply laid out as four unit-sized capacitors in parallel. We break the 2.314-unit capacitor up into one unit-sized capacitor in parallel with another rectangular capacitor of size 1.314 units. The lengths of the sides for this rectangular capacitor are found from (2.33), resulting in

$$
\mathrm{y}_{2}=10 \mu \mathrm{~m}\left(1.314 \pm \sqrt{1.314^{2}-1.314}\right)=19.56 \mu \mathrm{~m} \text { or } 6.717 \mu \mathrm{~m}
$$

Either of these results can be chosen for $\mathrm{y}_{2}$, and the other result becomes $\mathrm{x}_{2}$; in other words, the choice of sign affects only the rectangle orientation. Thus, we have the capacitor layout as shown in Fig. 2.31 Note that the ratio of the area of the rectangular capacitor to its perimeter equals 2.5 , which is the same as the ratio for the unit-sized capacitor.

Several other considerations should be observed when realizing accurate capacitor ratios. Usually the bottom plate of capacitors is shared by many unit-size capacitors. ${ }^{5}$ The interconnection of the top plates can often be done in metal with contacts to the capacitor plates. The parasitic capacitances of any tabs required to contact the plates should be matched as much as possible. This matching often entails adding extra tabs that are not connected anywhere. Another common matching technique is to ensure that the boundary conditions around the unit-sized capacitors match. This boundary-condition matching is accomplished by adding top-plate material around the outside boundaries of unit-sized capacitors at the edge of an array. Many of these principles are illustrated in the simplified layout of two capacitors shown in Fig. 2.32. Each capacitor in the figure consists of two unit-sized capacitors. An additional technique sometimes used (not shown in Fig. 2.32) is to cover the top plates

[^0]image_name:Fig. 2.32 A simplified layout of a capacitor array.
description:The image, identified as Fig. 2.32, depicts a simplified layout of a capacitor array. It consists of two capacitors labeled as C1 and C2, each composed of two unit-sized capacitors. The layout is designed to ensure boundary condition matching by incorporating polysilicon edge matching around the capacitors.

1. **Identification of Components and Structure:**
- **Capacitors (C1 and C2):** These are the main components, each consisting of two unit-sized capacitors arranged within the array.
- **Top Plates:** These are shown covering the capacitors, responsible for forming the top part of the capacitive structure.
- **Bottom Plate:** This is the underlying layer that forms the bottom part of the capacitive structure, providing a base for the top plates.
- **Polysilicon Edge Matching:** This feature is used around the periphery of the capacitors to ensure uniform boundary conditions and minimize edge effects.
- **Well Contacts:** These are distributed around the edge of the capacitor array, facilitating electrical connections and ensuring proper grounding.
- **Well Region:** This is the area surrounding the capacitors, providing isolation and structural support.

2. **Connections and Interactions:**
- The top plates are connected to specific nodes, potentially critical points such as amplifier inputs, to optimize performance and minimize interference.
- Well contacts are strategically placed to maintain electrical integrity and support grounding.

3. **Labels, Annotations, and Key Features:**
- Each capacitor is labeled as C1 or C2, indicating their specific roles or positions within the array.
- Key features such as top plates, bottom plate, and polysilicon edge matching are annotated, providing clarity on the structural components and their functions.

The design emphasizes shielding and minimal interference, with potential for additional capacitance through a sandwich-like structure, though this specific feature is not depicted in the diagram. The layout also suggests the possibility of using interdigitated metal for further capacitance optimization, as mentioned in the context.

Fig. 2.32 A simplified layout of a capacitor array.
with a layer of metal, which is then connected to the bottom plate. This sandwich-like structure not only gives additional capacitance per area but more importantly, shields the "top" plate from electromagnetic interference. The capacitor plate inside the sandwich is then connected to critical nodes, such as the inputs of amplifiers. Another possibility is to employ interdigitated metal as capacitors, as shown in Fig. 1.37(b).

An important consideration when using capacitors in switched-capacitor circuits is that one plate usually has more noise coupled into it than the other because of differing parasitic capacitances to a noisy substrate and/or supply voltage line. Therefore the quieter "top" plate should be connected to critical nodes such as the virtual inputs of opamps, whereas the more noisy "bottom" plate can be connected to less critical nodes such as opamp outputs.

For more details concerning the realization of integrated capacitors, the interested reader can see [Allstot, 1983; O'Leary, 1991; Maloberti, 1994].

### 2.4.3 Resistor Layout

Integrated resistors can be realized using a wide variety of different conductors. A popular choice is polysilicon, which is a deposited and etched material. Other choices include diffused or ion-implanted regions such as junctions, wells, or base regions. Another possibility is deposited and etched thin-film resistors such as nichrome (consisting of 80 percent nickel and 20 percent chromium) or tantalum. The temperature coefficient of ionimplanted or diffused resistors tends to be positive and large (especially for larger resistivities) with values as large as 1000 to $3000 \mathrm{ppm} /{ }^{\circ} \mathrm{C}$. On the other hand, the temperature coefficient for thin-film resistors can be as small as $100 \mathrm{ppm} /{ }^{\circ} \mathrm{C}$. Polysilicon resistors usually have large positive temperature coefficients (say, $1000 \mathrm{ppm} /{ }^{\circ} \mathrm{C}$ ) for low-resistivity polysilicon, and moderately large negative temperature coefficients for specially doped highresistivity polysilicon. The positive temperature coefficients are primarily due to mobility degradation that results from temperature increases. In implanted and diffused resistors, nonlinear resistance varies greatly with voltage because the depletion-region width is dependent on voltage in the more heavily doped conductive region. This depletion-region width variation is substantially smaller in a polysilicon resistor, which is one of the major
reasons polysilicon resistors are preferred over implanted resistors even though they often require more area due to the low resistivity. When thin-film resistors are available in a particular technology, they are almost always the preferred type-unfortunately, they are seldom available.

Regardless of the type of resistor used, the equations governing the resistance (see the Appendix of Chapter 1) are given by

$$
\begin{equation*}
R_{\square}=\frac{\varrho}{t} \tag{2.34}
\end{equation*}
$$

where $R_{\square}$ is the resistance per square, $\rho=1 /\left(q \mu_{n} N_{D}\right)$ is the resistivity, ${ }^{6} t$ is the thickness of the conductor, and $N_{D}$ is the concentration of carriers, which we assume are electrons. The total resistance is then given by

$$
\begin{equation*}
\mathrm{R}=\frac{\mathrm{L}}{\mathrm{~W}} \mathrm{R}_{\square} \tag{2.35}
\end{equation*}
$$

where $L$ is the length of the resistor and $W$ is the width of the resistor.
The typical resistivity encountered in integrated circuits depends upon the material employed. For example, in a modern process the gates are formed from a sandwich of a refractory metal over polysilicon (a salicide) with a resistivity of perhaps $1-5 \Omega / \square$, making the gate layer useless for realizing moderate-sized resistors. However, a common way to form resistors inside microcircuits is to use a polysilicon layer without the salicide. This type of polysilicon resistor can have a sheet resistance on the order of $100-1500 \Omega / \square$ depending upon process parameters. This value may vary by $10-25 \%$ with process and temperature. However, with accurate common centroid layout techniques, very good matching may be obtained between resistors on the same microcircuit.

To obtain large-valued resistors, one must usually use a serpentine layout similar to that shown in Fig. 2.33. Individual resistor fingers are connected in series by metal. The width of each metal is generally
image_name:Fig. 2.33 A layout for two matched resistors.
description:The image depicts a layout for two matched resistors, identified as **R1** and **R2**, arranged in a serpentine pattern to achieve large resistance values. The layout consists of multiple parallel strips connected in series by metal interconnections. Each strip represents a segment of the resistor, and the metal connections are used to link these segments together, forming a continuous resistive path.

**1. Identification of Components and Structure:**
- The resistors **R1** and **R2** are made from polysilicon and are laid out in an interdigitated fashion to ensure good matching.
- The layout includes "dummy resistors" on the outer edges, which are used to improve the uniformity and matching by compensating for edge effects.
- The metal interconnections are wider than the minimum width allowed by design rules to minimize variations due to edge roughness.

**2. Connections and Interactions:**
- The resistor strips are connected in a series configuration, with metal contacts at the ends of each strip.
- The serpentine layout ensures that the resistors occupy a compact area while achieving the desired resistance value.
- There is a note indicating "No salicide" on certain parts of the layout, which suggests that salicidation is not applied to those areas to control resistance.

**3. Labels, Annotations, and Key Features:**
- The resistors are labeled as **R1** and **R2**, with alternating segments indicating the interdigitated pattern.
- Annotations such as "No salicide" and "Dummy resistor" provide additional context for the design choices and layout strategy.
- The dashed lines indicate the boundary of the active resistor area, with dummy resistors extending beyond these boundaries for improved matching.

Fig. 2.33 A layout for two matched resistors.

[^1]far greater than the minimum permitted by the design rules to minimize variations due to edge roughness. Hence, the layout of medium or large-valued resistors can easily be much greater than that of the surrounding transistors. Assuming polysilicon resistors, the metal contacts require a salicide to be deposited on the ends of each strip. In addition to the strips' sheet resistance, additional series resistances appear at the interfaces between salicided to non-salicided polysilicon and due to the contacts. For example, roughly $20 \Omega$ per contact may be added, but this value is very poorly controlled and may exhibit process variations of over $50 \%$. Hence, the layout should ensure that the contact and interface resistances are a small fraction of the overall resistance. Specifically, very short fingers should be avoided and multiple contacts should always be used in parallel.

The layout in Fig. 2.33 shows two resistors, intended to be well-matched. Two dummy fingers have been included at either side of the layout to match boundary conditions. This structure might result in about 0.1 percent matching accuracy of identical resistors if the finger widths are taken much wider than the fabrication process's minimum feature size. As with integrated capacitors, it is also a good idea to place a shield under a resistor that is connected to a clean power supply. An appropriate shield might be a well region. This shielding helps keep substrate noise from being injected into the conductive layer. (Noise is due to capacitive coupling between the substrate and a large resistor structure.) Also, the parasitic capacitance between the resistor and the shield should be modelled during simulation. Its second-order effects on circuits such as RC filters can often be eliminated using optimization, which is available in many SPICE-like simulators. For low-noise designs, a metal shield over the top of a resistor may also be necessary, although it will result in a corresponding increase in capacitance.

For more information on realizing accurate resistor ratios, the reader is referred to [O'Leary, 1991; Maloberti, 1994].

#### EXAMPLE 2.7

Estimate the resistance of the layout in Fig. 2.33 assuming a sheet resistance of $800 \Omega / \square$ for the non-salicided polysilicon and $20 \Omega$ per contact.

#### Solution

Each finger in the layout comprises a strip of non-salicided polysilicon $10 \square$ long, hence having a resistance of $10 \square \times 800 \Omega / \square=8 \mathrm{k} \Omega$. Each finger also includes two parallel contacts at either end accounting for an additional $2 \times(20 \Omega / 2)=20 \Omega$ series resistance. Each resistor comprises 4 fingers in series, and therefore has a total resistance of approximately

$$
4 \times(8 \mathrm{k} \Omega+20 \Omega) \cong 32 \mathrm{k} \Omega
$$

### 2.4.4 Noise Considerations

Some additional layout issues help minimize noise in analog circuits. Most of these issues either attempt to minimize noise from digital circuits coupling into the substrate and analog power supplies, or try to minimize substrate noise that affects analog circuits.

With mixed analog-digital circuits, it is critical that different power-supply connections be used for analog circuits than for digital circuits. Ideally, these duplicate power supplies are connected only off the chip. Where a single I/O pin must be used for the power supply, it is still possible to use two different bonding wires extending from a single-package I/O pin to two separate bonding pads on the integrated circuit. At a very minimum, even if a single
image_name:Fig. 2.34
description:
[

]
extrainfo:The diagram illustrates the separation of analog and digital power-supply nets using a single I/O pad. The analog and digital nets are kept distinct to minimize interference from digital switching noise affecting the analog circuitry.

Fig. 2.34 Using separate nets for analog and digital power supplies.
bonding pad is used for both analog and digital circuitry, two separated nets from the bonding pad out should be used for the different types of circuitry, as Fig. 2.34 shows. The reason the power-supply interconnects must be separated is that the interconnect does not have zero impedance. Every time a digital gate or buffer changes state, a glitch is injected on the digital power supply and in the surrounding substrate. By having the analog power supplies separate, we prevent this noise from affecting the analog circuitry. In the ideal case, separate pins are used for the positive power supply and for ground in both the digital and analog circuits. In addition, another pair of pins may be used for the supply voltage and ground for digital output buffers, which can inject very large current spikes. Finally, sometimes multiple pins are used for additional supply and grounds for very large microcircuits.

Another common precaution is to lay out the digital and analog circuitry in different sections of the microcircuit. The two sections should be separated by guard rings and wells connected to the power-supply voltages, as Fig. 2.35 shows. The $\mathrm{p}^{+}$connections to ground help keep a low-impedance path between the substrate and
image_name:Fig. 2.35
description:The circuit diagram illustrates the separation of analog and digital regions using p+ guard rings and an n+ n-well to minimize noise injection. The depletion region acts as a bypass capacitor, providing a low-impedance path to ground.

Fig. 2.35 Separating analog and digital areas with guard rings and wells in an attempt to minimize the injection of noise from digital circuits into the substrate under the analog circuit.
ground. For modelling purposes, the substrate can be modelled as a number of series-connected resistors with the $\mathrm{p}^{+}$ground connections modelled as resistor-dividers having a small impedance to ground. These low-impedance ground connections help keep substrate noise from propagating through the resistive substrate. The use of the n well between $\mathrm{p}^{+}$connections helps to further increase the resistive impedance of the substrate between the analog and digital regions due to graded substrate doping. Specifically, the $\mathrm{p}^{-}$substrate often has 10 times higher doping at the surface of the microcircuit compared to the doping level below the n well, which leads to a tenfold increase in substrate resistivity between the two $\mathrm{p}^{+}$connections. Finally, the n well also operates as a bypass capacitor to help lower the noise on $V_{D D}$.

Another important consideration when laying out a circuit that includes both analog and digital circuits is the use of shields connected to either ground or to a separate power-supply voltage. Figure 2.36 shows examples of the use of shields. In this example, an n well is used to shield the substrate from the digital interconnect line. The well is also used to shield an analog interconnect line from any substrate noise. This shield is ideally connected to a ground net that is used only for shields. If this type of connection is not possible due to layout and space constraints, then the digital ground can be used for the shields, although this is not ideal. In the example, the shield ground is also connected to metal lines that separate the analog and digital lines from each other and from other interconnect lines. Finally, an additional metal shield might be placed above the lines as well. This final shield may be somewhat excessive, but it can often be easily realized in many parts of the microcircuit if ground and power-supply lines are distributed in metal 2, perpendicular to the metal-1 interconnect lines. It should also be mentioned that the n well shield also acts as a bypass capacitor; this helps minimize noise in the substrate, which is connected to $\mathrm{V}_{\mathrm{DD}}$. Additional layers that are often used as shields are the polysilicon layers.

Perhaps the most effective technique for minimizing the propagation of substrate noise in a mixed-mode microcircuit containing both analog and digital circuitry is the use of an epitaxial process. An epitaxial process places a conductive layer under all transistors. Any charge flowing through the substrate is attracted to this layer and does not propagate into sensitive analogs regions. Although this process is more expensive, it also helps prevent latch-up. For deep submicron technologies, this epitaxial process is common because of its reduced latch-up sensitivity.

Careful thought should go into the overall placement of different blocks in a mixed-mode analog-digital microcircuit. A possible arrangement for an analog section containing switched-capacitor circuits is shown in Fig. 2.37. Notice that an n well shield is being used under the capacitors. Notice also that the clock lines are not only as far from the opamps as possible, but are also separated by two wells and a $\mathrm{V}_{\mathrm{SS}}$ interconnect that is liberally connected to the substrate, two ground (Gnd) lines, and a $\mathrm{V}_{\mathrm{DD}}$ line. A well is placed under the clock lines as a shield. This shield is connected to a
image_name:Fig. 2.36
description:The image labeled "Fig. 2.36" depicts a cross-sectional view of a shielding technique used in analog circuits to minimize noise coupling. The diagram illustrates a layered structure with several key components:

1. **Ground Line for Shielding**: At the top of the diagram, a horizontal line is labeled "Ground line used for shielding." This line serves as a protective layer to prevent noise from affecting the underlying components.

2. **Analog and Digital Interconnects**: Below the ground line, two interconnects are shown, labeled "Analog interconnect" and "Digital interconnect." These interconnects are responsible for carrying analog and digital signals, respectively, and are separated to reduce interference between them.

3. **N Well**: The diagram shows an "n well" region, which is a semiconductor layer used to isolate components and reduce capacitive coupling. This well acts as a substrate for the circuit elements.

4. **N+ Regions**: Within the n well, there are several "n+" regions depicted as darker areas. These regions are highly doped to provide good electrical connectivity and are likely used for grounding or connecting other components.

5. **Substrate**: At the bottom of the diagram, a line represents the substrate, which is the base layer of the semiconductor device. It provides structural support and electrical grounding.

The diagram emphasizes the use of shielding to prevent noise from coupling into the substrate, which is critical in maintaining signal integrity in analog circuits. The separation of analog and digital interconnects, along with the use of n wells and n+ regions, illustrates a design focused on minimizing interference and ensuring reliable circuit operation.

$\mathrm{p}^{-}$substrate

Fig. 2.36 Using shields helps keep noise from being capacitively coupled into and out of the substrate.
image_name:Fig. 2.37 A possible floor plan for an analog section containing switched-capacitor circuits.
description:
[
name: Opamp 1, type: OpAmp, value: Opamp 1, ports: {InP: VDD, InN: Gnd, OutP: n well under p-channel devices, OutN: Region for n-channel devices}
name: Opamp 2, type: OpAmp, value: Opamp 2, ports: {InP: VDD, InN: Gnd, OutP: n well under p-channel devices, OutN: Region for n-channel devices}
name: Opamp 3, type: OpAmp, value: Opamp 3, ports: {InP: VDD, InN: Gnd, OutP: n well under p-channel devices, OutN: Region for n-channel devices}
name: Capacitors, type: Capacitor, value: Capacitors, ports: {Np: n well under capacitor region, Nn: Gnd}
name: Switches, type: Switch, ports: {N1: Region for n-channel switches, N2: n well under p-channel switch region}
]
extrainfo:The diagram illustrates a floor plan for an analog section containing switched-capacitor circuits. It emphasizes the use of n wells under various regions to minimize noise and interference. Separate VDD and Gnd lines indicate distinct power distribution for different sections, including opamps, capacitors, and switches. Clock lines are also shown, highlighting their role in controlling the circuit operation.

Fig. 2.37 A possible floor plan for an analog section containing switched-capacitor circuits.
separate ground line (perhaps digital ground) from the one used in the opamp region because this shield will likely have quite a bit of clock noise coupled into it. Also note that a separate $\mathrm{V}_{\mathrm{DD}}$ line is used to connect to the n wells under the switches, a region where digital interconnects exist, as is used in the critical opamp section.

One last technique for noise minimization in analog microcircuits should always be used: After layout has been finished, any unused space should be filled with additional contats to both the substrate and to the wells, which are used as bypass capacitors. In a typical microcircuit, this results in a significant increase in bypass capacitance.

Many other techniques have been developed by various companies, but the preceding techniques give the reader a good idea of the types of practical considerations necessary when realizing high-performance analog microcircuits.

## 2.5 KEY POINTS

- The first step in realizing an integrated circuit is to produce a single-crystalline silicon wafer from 10 to 30 cm in diameter and roughly 1 mm thick. The silicon is either lightly doped, or heavily doped with a thin lightlydoped epitaxial layer on top in which the transistors are made. [p. 74]
- Most features on integrated circuits are patterned using photolithography whereby light is passed through a mask to cast patterns onto the underlying silicon wafer, ultimately defining the circuit's physical features such as transistor sizes and wiring. [p. 75]
- Transistors are fabricated inside the "active" or "oxide definition" (OD) regions of the microcircuit. Over OD regions, only a very thin oxide separates the polysilicon gates from the transistor channel regions underneath, and additional dopants are introduced to control the threshold voltages. Surrounding the OD regions are isolation structures to prevent parasitic transistors from conducting leakage currents. [p. 81]
- The edge of transistor source and drain junctions are defined by the edge of the polysilicon gate above. This "self-alignment" of the gate and junctions was key in the development of small high-speed transistors. [p. 83]
- Up to 10 or even more layers of metal are patterned above the silicon surface, separated by insulating oxide, to provide interconnect between all the devices in a circuit. [p. 84]
- Finite tolerances during integrated circuit manufacturing impose constraints on the minimum sizes and spacing of transistor and interconnect features. These constraints may be expressed as multiples of $\lambda$, equal to one-half the minimum gate length. They influence parasitic capacitances, and ultimately the circuit bandwidth which an analog designer may expect. [p. 88]
- Systematic variations are those observed repeatedly and consistently, even when a circuit is being mass-produced. Generally, these may be avoided by proper layout techniques, although doing so may impose some penalty in terms of layout size or performance. Process variations are observed because the conditions of manufacture (temperature, concentration levels, etc.) can never be maintained precisely constant. These manifest as device parameters that differ from one sample of a circuit to the next. Random variations are statistical in nature and are present in every individual device. Hence, they may be observed as mismatch between two identically specified transistors fabricated under the same nominal conditions. [p. 96]
- The absolute sizes and electrical parameters of integrated circuit components can seldom be accurately determined. For best accuracy, larger objects are made out of several unit-sized components connected together, and the boundary conditions around all objects should be matched, even when this means adding extra unused components. [p. 98]
- Practical variations in transistor parameters, supply voltage, and temperature (PVT variations) can be a bane to analog designers trying to reliably meet specific performance criteria. [p. 99]
- The parameters of devices that are closely spaced with identical layout exhibit a random variance inversely proportional to device area. In practice, the most important random variations in most analog circuits are mismatch. [p. 100]
- In a common centroid layout, any linear gradient in electrical properties across the chip effects two or more devices equally. This is achieved by dividing each device into smaller equal-sized units, and arranging the units so that all devices have the same mean position ("centroid"). [p. 103]
