# 2. Basic Physics of Semiconductors

Microelectronic circuits are based on complex semiconductor structures that have been under active research for the past six decades. While this book deals with the analysis and design of circuits, we should emphasize at the outset that a good understanding of devices is essential to our work. The situation is similar to many other engineering problems, e.g., one cannot design a high-performance automobile without a detailed knowledge of the engine and its limitations.

Nonetheless, we do face a dilemma. Our treatment of device physics must contain enough depth to provide adequate understanding, but must also be sufficiently brief to allow quick entry into circuits. This chapter accomplishes this task.

Our ultimate objective in this chapter is to study a fundamentally important and versatile device called the "diode." However, just as we need to eat our broccoli before having dessert, we must develop a basic understanding of "semiconductor" materials and their current conduction mechanisms before attacking diodes.

In this chapter, we begin with the concept of semiconductors and study the movement of charge (i.e., the flow of current) in them. Next, we deal with the " $p n$ junction," which also serves as diode, and formulate its behavior. Our ultimate goal is to represent the device by a circuit model (consisting of resistors, voltage or current sources, capacitors, etc.), so that a circuit using such a device can be analyzed easily. The outline is shown below.

It is important to note that the task of developing accurate models proves critical for all microelectronic devices. The electronics industry continues to place greater demands
on circuits, calling for aggressive designs that push semiconductor devices to their limits. Thus, a good understanding of the internal operation of devices is necessary. ${ }^{1}$

## 2.1 SEMICONDUCTOR MATERIALS AND THEIR PROPERTIES

Since this section introduces a multitude of concepts, it is useful to bear a general outline in mind:
image_name:Figure 2.1 Outline of this section
description:The block diagram in Figure 2.1 provides an outline of the section on semiconductor materials and their properties, organized into three main components.

1. **Charge Carriers in Solids**: This block focuses on the fundamental aspects of charge carriers within solid materials. It highlights three key areas:
- **Crystal Structure**: Refers to the arrangement of atoms in a crystalline solid, which affects the movement and behavior of charge carriers.
- **Bandgap Energy**: The energy difference between the valence band and the conduction band in a semiconductor, crucial for determining its electrical properties.
- **Holes**: Represents the absence of an electron in a semiconductor, acting as a positive charge carrier.

2. **Modification of Carrier Densities**: This block deals with how the density of charge carriers can be altered to achieve desired electrical characteristics. It includes:
- **Intrinsic Semiconductors**: Pure semiconductors without any significant impurities, where the number of electrons equals the number of holes.
- **Extrinsic Semiconductors**: Semiconductors that have been doped with impurities to change their electrical properties, increasing either electron or hole concentration.
- **Doping**: The process of adding impurities to a semiconductor to modify its electrical properties, enhancing its conductivity.

3. **Transport of Carriers**: This block describes the mechanisms by which charge carriers move through a semiconductor:
- **Diffusion**: The movement of charge carriers from a region of higher concentration to a region of lower concentration.
- **Drift**: The movement of charge carriers under the influence of an electric field.

The diagram uses arrows to indicate the logical flow from understanding the nature of charge carriers in solids, to modifying their densities, and finally to understanding their transport mechanisms. This progression is essential for computing the current/voltage characteristics of diodes, which will be explored in subsequent sections.

Figure 2.1 Outline of this section.
This outline represents a logical thought process: (a) we identify charge carriers in solids and formulate their role in current flow; (b) we examine means of modifying the density of charge carriers to create desired current flow properties; (c) we determine current flow mechanisms. These steps naturally lead to the computation of the current/voltage (I/V) characteristics of actual diodes in the next section.

### 2.1.1 Charge Carriers in Solids

Recall from basic chemistry that the electrons in an atom orbit the nucleus in different "shells." The atom's chemical activity is determined by the electrons in the outermost shell, called "valence" electrons, and how complete this shell is. For example, neon exhibits a complete outermost shell (with eight electrons) and hence no tendency for chemical reactions. On the other hand, sodium has only one valence electron, ready to relinquish it, and chloride has seven valence electrons, eager to receive one more. Both elements are therefore highly reactive.

The above principles suggest that atoms having approximately four valence electrons fall somewhere between inert gases and highly volatile elements, possibly displaying interesting chemical and physical properties. Shown in Fig. 2.2 is a section of the periodic table containing a number of elements with three to five valence electrons. As the most popular material in microelectronics, silicon merits a detailed analysis. ${ }^{2}$

Covalent Bonds A silicon atom residing in isolation contains four valence electrons [Fig. 2.3(a)], requiring another four to complete its outermost shell. If processed properly, the silicon material can form a "crystal" wherein each atom is surrounded by exactly four others [Fig. 2.3(b)]. As a result, each atom shares one valence electron with its neighbors, thereby completing its own shell and those of the neighbors. The "bond" thus formed between atoms is called a "covalent bond" to emphasize the sharing of valence electrons.

The uniform crystal depicted in Fig. 2.3(b) plays a crucial role in semiconductor devices. But, does it carry current in response to a voltage? At temperatures near absolute zero,

[^3]image_name:Figure 2.2 Section of the periodic table
description:The image, labeled as "Figure 2.2 Section of the periodic table," displays a portion of the periodic table focusing on three groups: III, IV, and V. Each group is represented by a vertical column.

- **Group III** includes:
- Boron (B)
- Aluminum (Al)
- Gallium (Ga)

- **Group IV** includes:
- Carbon (C)
- Silicon (Si)
- Germanium (Ge)

- **Group V** includes:
- Phosphorus (P)
- Arsenic (As)

The elements are arranged in a grid format, with each element's name followed by its chemical symbol in parentheses. The image highlights elements commonly involved in semiconductor technology, such as Silicon (Si) from Group IV, which is emphasized in the context of covalent bonding in semiconductor devices.

Figure 2.2 Section of the periodic table.
the valence electrons are confined to their respective covalent bonds, refusing to move freely. In other words, the silicon crystal behaves as an insulator for $T \rightarrow 0 K$. However, at higher temperatures, electrons gain thermal energy, occasionally breaking away from the bonds and acting as free charge carriers [Fig. 2.3(c)] until they fall into another incomplete bond. We will hereafter use the term "electrons" to refer to free electrons.
image_name:(a)
description:The image labeled as "(a)" depicts a simplified representation of a silicon (Si) atom. At the center of the diagram is the chemical symbol "Si," indicating the element silicon. Surrounding the central symbol are four lines extending outward in a cross-like formation, representing the four valence electrons of the silicon atom. These lines symbolize the potential for forming covalent bonds with other atoms, consistent with silicon's tetravalent nature. The diagram is a conceptual illustration, focusing on the bonding capabilities of silicon rather than its detailed atomic structure.
image_name:(b)
description:The image labeled as "(b)" depicts a simplified diagram of covalent bonds between silicon atoms. At the center of the diagram is a symbol "Si," representing a silicon atom. Surrounding the central silicon atom are four lines extending outward, each representing a covalent bond with neighboring silicon atoms. These lines are evenly spaced, forming a cross-like structure, symbolizing the tetrahedral bonding arrangement typical in a silicon crystal lattice. This diagram illustrates how silicon atoms share electrons with adjacent atoms, forming a stable crystal structure. There are no additional labels, annotations, or numerical values in the diagram, emphasizing the conceptual representation of silicon's covalent bonding rather than detailed electronic properties or interactions.
image_name:(c)
description:The image labeled as "(c)" depicts a simplified diagram representing a silicon (Si) atom within a crystal lattice. At the center of the diagram is the chemical symbol "Si" denoting a silicon atom. Surrounding the silicon atom are four lines extending outward in a cross-like pattern, which symbolize the covalent bonds that silicon forms with neighboring atoms in a crystal lattice. These lines represent the shared valence electrons that constitute the covalent bonds, crucial for the structural integrity of the silicon crystal. The diagram is a conceptual representation, emphasizing the bonding structure rather than the physical appearance of the silicon atom or its lattice.

(a)
image_name:(b)
description:The diagram labeled (b) illustrates a conceptual representation of covalent bonds between silicon atoms in a crystal lattice. The structure is depicted using a grid-like pattern where each 'Si' represents a silicon atom. These silicon atoms are connected by lines, symbolizing the covalent bonds formed by shared valence electrons. This interconnected network is characteristic of the crystalline structure of silicon, where each silicon atom shares electrons with four neighboring atoms, creating a stable lattice.

Key features include:
1. **Silicon Atoms (Si):** Each labeled 'Si' represents a silicon atom.
2. **Covalent Bonds:** The lines between the silicon atoms indicate covalent bonds, emphasizing the sharing of electrons.
3. **Lattice Structure:** The arrangement forms a repetitive, grid-like pattern, typical of a crystal lattice.
4. **Labeling:** An arrow points to one of the bonds, labeled "Covalent Bond," highlighting the focus on the bonding structure.

This diagram serves as a simplified model to help visualize the atomic bonding in silicon, crucial for understanding its properties as a semiconductor material.

(b)
image_name:(c)
description:The image illustrates a section of a silicon crystal lattice, emphasizing the concept of free electrons. The lattice is composed of silicon (Si) atoms, each bonded to four neighboring silicon atoms, forming a repetitive grid-like pattern. The bonds between the atoms are depicted as lines, representing covalent bonds where electrons are shared between atoms.

In the diagram, one of the covalent bonds is broken, and an electron is shown as being freed from the lattice. This is indicated by an arrow pointing away from the bond, labeled "Free Electron." The freed electron is denoted by the symbol 'e⁻', highlighting its negative charge.

This image serves to illustrate the concept of electron-hole pairs in semiconductor physics, where the release of an electron from a covalent bond leaves behind a "hole." This is a fundamental concept in understanding the behavior of semiconductors, particularly in how they conduct electricity.

(c)

Figure 2.3 (a) Silicon atom, (b) covalent bonds between atoms, (c) free electron released by thermal energy.

Holes When freed from a covalent bond, an electron leaves a "void" behind because the bond is now incomplete. Called a "hole," such a void can readily absorb a free electron if one becomes available. Thus, we say an "electron-hole pair" is generated when an electron is freed, and an "electron-hole recombination" occurs when an electron "falls" into a hole.

Why do we bother with the concept of the hole? After all, it is the free electron that actually moves in the crystal. To appreciate the usefulness of holes, consider the time evolution illustrated in Fig. 2.4. Suppose covalent bond number 1 contains a hole after
image_name:Figure 2.4 Movement of electron through crystal
description:The diagram labeled "Figure 2.4 Movement of electron through crystal" illustrates the movement of electrons and the formation of holes in a silicon crystal lattice at a specific time, denoted as \( t = t_1 \). The diagram features a grid-like arrangement of silicon (Si) atoms, each connected by lines representing covalent bonds between the silicon atoms.

1. **Identification of Components and Structure:**
- The primary components are the silicon atoms, represented by the symbol "Si." These atoms are arranged in a repeating pattern, forming a lattice structure.
- Covalent bonds between the silicon atoms are depicted as double lines connecting neighboring atoms.
- A "Hole" is indicated at one of the silicon atoms, where an electron is missing, creating a positive charge in the lattice.

2. **Connections and Interactions:**
- The diagram shows the movement or potential movement of an electron, represented by an arrow pointing towards the hole in the lattice. This suggests that an electron from a neighboring atom can move to fill the hole, demonstrating the concept of electron-hole recombination.
- The movement of the electron is marked by an arrow, indicating the direction of electron flow towards the hole.

3. **Labels, Annotations, and Key Features:**
- The time \( t = t_1 \) is labeled at the top of the diagram, indicating the specific moment being represented.
- The hole is explicitly labeled, and an arrow is used to show the electron's potential movement towards the hole.
- The number "1" is associated with the silicon atom where the hole is located, indicating the initial bond number that lost an electron.

image_name:Figure 2.4 Movement of electron through crystal.
description:The image titled "Figure 2.4 Movement of electron through crystal" depicts a section of a silicon crystal lattice at a specific moment in time, labeled as \( t = t_2 \). The diagram shows a grid-like arrangement of silicon (Si) atoms, each represented by the symbol "Si". These atoms are connected by lines, indicating covalent bonds between them.

In the lattice, there is a notable feature: a circle representing a hole, which is a vacancy left by an absent electron. This hole is located near a silicon atom labeled with the number "2". The presence of this hole indicates that an electron has moved away from its original bond, creating a vacancy.

The arrangement suggests that at \( t = t_2 \), an electron has left bond number 2, moving towards the hole in bond number 1, as described in the context. This movement of electrons and the resulting holes are key aspects of semiconductor behavior, illustrating how electrical conduction occurs in materials like silicon.

image_name:Figure 2.4 Movement of electron through crystal
description:The image titled "Figure 2.4 Movement of electron through crystal" depicts a lattice structure representing a section of a silicon crystal at time \( t = t_3 \). The diagram illustrates several silicon (Si) atoms arranged in a grid-like pattern, each connected by lines that symbolize covalent bonds.

1. **Identification of Components and Structure:**
- The primary components are the silicon atoms, labeled as "Si," arranged in a diamond-like lattice structure, which is typical for crystalline silicon.
- Each silicon atom is connected to neighboring silicon atoms by lines indicating covalent bonds.

2. **Connections and Interactions:**
- At this moment \( t = t_3 \), an electron has vacated a bond, creating a hole. This hole is near a silicon atom labeled with the number "3," indicating that the electron has moved away from this bond.
- The movement of the electron from one bond to another illustrates the concept of electron flow and hole movement within the semiconductor material.

3. **Labels, Annotations, and Key Features:**
- The label "t = t_3" at the top of the diagram specifies the time snapshot being represented.
- The number "3" next to one of the bonds highlights the specific location where the electron has left, creating a hole.
- A shaded circle represents the hole, visually indicating the vacancy left by the electron.

This visual representation is a simplified model of how electrons move through a silicon crystal, contributing to electrical conduction by creating and filling holes, which are conceptualized as positive charge carriers moving in the opposite direction to the electrons.

Figure 2.4 Movement of electron through crystal.
losing an electron some time before $t=t_{1}$. At $t=t_{2}$, an electron breaks away from bond number 2 and recombines with the hole in bond number 1 . Similarly, at $t=t_{3}$, an electron leaves bond number 3 and falls into the hole in bond number 2. Looking at the three "snapshots," we can say one electron has traveled from right to left, or, alternatively, one hole has moved from left to right. This view of current flow by holes proves extremely useful in the analysis of semiconductor devices.

Bandgap Energy We must now answer two important questions. First, does any thermal energy create free electrons (and holes) in silicon? No, in fact, a minimum energy is required to dislodge an electron from a covalent bond. Called the "bandgap energy" and denoted by $E_{g}$, this minimum is a fundamental property of the material. For silicon, $E_{g}=1.12 \mathrm{eV}^{3}$

The second question relates to the conductivity of the material and is as follows. How many free electrons are created at a given temperature? From our observations thus far, we postulate that the number of electrons depends on both $E_{g}$ and $T$ : a greater $E_{g}$ translates to fewer electrons, but a higher $T$ yields more electrons. To simplify future derivations, we consider the density (or concentration) of electrons, i.e., the number of electrons per unit volume, $n_{i}$, and write for silicon:

$$
\begin{equation*}
n_{i}=5.2 \times 10^{15} T^{3 / 2} \exp \frac{-E_{g}}{2 k T} \text { electrons } / \mathrm{cm}^{3} \tag{2.1}
\end{equation*}
$$

where $k=1.38 \times 10^{-23} \mathrm{~J} / \mathrm{K}$ is called the Boltzmann constant. The derivation can be found in books on semiconductor physics, e.g., [1]. As expected, materials having a larger $E_{g}$ exhibit a smaller $n_{i}$. Also, as $T \rightarrow 0$, so do $T^{3 / 2}$ and $\exp \left[-E_{g} /(2 k T)\right]$, thereby bringing $n_{i}$ toward zero.

The exponential dependence of $n_{i}$ upon $E_{g}$ reveals the effect of the bandgap energy on the conductivity of the material. Insulators display a high $E_{g}$; for example, $E_{g}=2.5 \mathrm{eV}$ for diamond. Conductors, on the other hand, have a small bandgap. Finally, semiconductors exhibit a moderate $E_{g}$, typically ranging from 1 eV to 1.5 eV .

Example Determine the density of electrons in silicon at $T=300 \mathrm{~K}$ (room temperature) and
2.1 $T=600 \mathrm{~K}$.

Solution Since $E_{g}=1.12 \mathrm{eV}=1.792 \times 10^{-19} \mathrm{~J}$, we have

$$
\begin{align*}
& n_{i}(T=300 \mathrm{~K})=1.08 \times 10^{10} \text { electrons } / \mathrm{cm}^{3}  \tag{2.2}\\
& n_{i}(T=600 \mathrm{~K})=1.54 \times 10^{15} \text { electrons } / \mathrm{cm}^{3} \tag{2.3}
\end{align*}
$$

Since for each free electron, a hole is left behind, the density of holes is also given by (2.2) and (2.3).

Exercise Repeat the above exercise for a material having a bandgap of 1.5 eV .

The $n_{i}$ values obtained in the above example may appear quite high, but, noting that silicon has $5 \times 10^{22}$ atoms $/ \mathrm{cm}^{3}$, we recognize that only one in $5 \times 10^{12}$ atoms benefit from a

[^4]free electron at room temperature. In other words, silicon still seems a very poor conductor. But, do not despair! We next introduce a means of making silicon more useful.

### 2.1.2 Modification of Carrier Densities

Intrinsic and Extrinsic Semiconductors

The "pure" type of silicon studied thus far is an example of "intrinsic semiconductors," suffering from a very high resistance. Fortunately, it is possible to modify the resistivity of silicon by replacing some of the atoms in the crystal with atoms of another material. In an intrinsic semiconductor, the electron density, $n\left(=n_{i}\right)$, is equal to the hole density, p. Thus,

$$
\begin{equation*}
n p=n_{i}^{2} \tag{2.4}
\end{equation*}
$$

We return to this equation later.
Recall from Fig. 2.2 that phosphorus (P) contains five valence electrons. What happens if some P atoms are introduced in a silicon crystal? As illustrated in Fig. 2.5, each P atom shares four electrons with the neighboring silicon atoms, leaving the fifth electron "unattached." This electron is free to move, serving as a charge carrier. Thus, if $N$ phosphorus atoms are uniformly introduced in each cubic centimeter of a silicon crystal, then the density of free electrons rises by the same amount.
image_name:Figure 2.5
description:Figure 2.5 illustrates a silicon crystal lattice that has been doped with phosphorus atoms. In the diagram, several silicon (Si) atoms are arranged in a grid-like pattern, each represented by the symbol 'Si' and connected to neighboring silicon atoms by lines, indicating covalent bonds. The phosphorus (P) atom is centrally located, replacing one of the silicon atoms in the lattice. This phosphorus atom is depicted as sharing four of its five valence electrons with adjacent silicon atoms, forming covalent bonds similar to those between the silicon atoms.

However, unlike silicon, phosphorus has an extra valence electron, represented in the diagram by the symbol 'e⁻'. This electron is shown as being "unattached" or loosely bound, symbolizing its freedom to move throughout the crystal lattice. This free electron acts as a charge carrier, contributing to the electrical conductivity of the silicon crystal. The presence of this free electron is a key feature of n-type semiconductor behavior, where the doping with phosphorus increases the number of free electrons and thus enhances conductivity.

The diagram effectively highlights the concept of doping in semiconductors, showing how the introduction of phosphorus atoms into a silicon lattice alters its electronic properties by providing additional free electrons.

Figure 2.5 Loosely-attached electon with phosphorus doping.

The controlled addition of an "impurity" such as phosphorus to an intrinsic semiconductor is called "doping," and phosphorus itself a "dopant." Providing many more free electrons than in the intrinsic state, the doped silicon crystal is now called "extrinsic," more specifically, an " $n$-type" semiconductor to emphasize the abundance of free electrons.

As remarked earlier, the electron and hole densities in an intrinsic semiconductor are equal. But, how about these densities in a doped material? It can be proved that even in this case,

$$
\begin{equation*}
n p=n_{i}^{2} \tag{2.5}
\end{equation*}
$$

where $n$ and $p$ respectively denote the electron and hole densities in the extrinsic semiconductor. The quantity $n_{i}$ represents the densities in the intrinsic semiconductor (hence the subscript $i$ ) and is therefore independent of the doping level [e.g., Eq. (2.1) for silicon].

Solution Equation (2.5) reveals that $p$ must fall below its intrinsic level as more $n$-type dopants are added to the crystal. This occurs because many of the new electrons donated by the dopant "recombine" with the holes that were created in the intrinsic material.

Exercise Why can we not say that $n+p$ should remain constant?

Example A piece of crystalline silicon is doped uniformly with phosphorus atoms. The doping
2.3 density is $10^{16}$ atoms $/ \mathrm{cm}^{3}$. Determine the electron and hole densities in this material at the room temperature.

Solution The addition of $10^{16} \mathrm{P}$ atoms introduces the same number of free electrons per cubic centimeter. Since this electron density exceeds that calculated in Example 2.1 by six orders of magnitude, we can assume

$$
\begin{equation*}
n=10^{16} \text { electrons } / \mathrm{cm}^{3} \tag{2.6}
\end{equation*}
$$

It follows from (2.2) and (2.5) that

$$
\begin{align*}
p & =\frac{n_{i}^{2}}{n}  \tag{2.7}\\
& =1.17 \times 10^{4} \text { holes } / \mathrm{cm}^{3} \tag{2.8}
\end{align*}
$$

Note that the hole density has dropped below the intrinsic level by six orders of magnitude. Thus, if a voltage is applied across this piece of silicon, the resulting current consists predominantly of electrons.

Exercise At what doping level does the hole density drop by three orders of magnitude?

This example justifies the reason for calling electrons the "majority carriers" and holes the "minority carriers" in an $n$-type semiconductor. We may naturally wonder if it is possible to construct a " $p$-type" semiconductor, thereby exchanging the roles of electrons and holes.

Indeed, if we can dope silicon with an atom that provides an insufficient number of electrons, then we may obtain many incomplete covalent bonds. For example, the table in Fig. 2.2 suggests that a boron (B) atom-with three valence electrons-can form only three complete covalent bonds in a silicon crystal (Fig. 2.6). As a result, the fourth bond contains a hole, ready to absorb a free electron. In other words, $N$ boron atoms contribute $N$ boron holes to the conduction of current in silicon. The structure in Fig. 2.6 therefore exemplifies a $p$-type semiconductor, providing holes as majority carriers. The boron atom is called an "acceptor" dopant.
image_name:Figure 2.6 Available hole with boron doping
description:The image titled "Figure 2.6 Available hole with boron doping" depicts a schematic representation of a silicon crystal lattice doped with a boron atom, illustrating the concept of a $p$-type semiconductor.

1. **Identification of Components and Structure:**
- The diagram shows a grid-like structure where the majority of the elements are labeled as "Si," representing silicon atoms. These silicon atoms are arranged in a crystalline lattice, each forming covalent bonds with its neighboring silicon atoms.
- At the center of the diagram, a single atom is labeled "B," indicating a boron atom. This boron atom replaces one of the silicon atoms in the lattice.
- There is a noticeable circle near the boron atom, symbolizing a "hole" in the lattice. This hole represents the absence of an electron, which is a key feature of $p$-type semiconductors.

2. **Connections and Interactions:**
- The silicon atoms are connected by lines, representing covalent bonds formed by shared electrons. Each silicon atom typically forms four covalent bonds with its neighboring silicon atoms in the lattice.
- The boron atom, having only three valence electrons, forms three covalent bonds with adjacent silicon atoms. The absence of the fourth bond results in the creation of a hole, which can accept an electron from neighboring atoms, facilitating the conduction of electric current.

3. **Labels, Annotations, and Key Features:**
- The "Si" labels indicate silicon atoms, while the "B" label identifies the boron atom, which acts as an acceptor dopant.
- The circle near the boron atom is a crucial feature, representing the hole that is available for conduction. This hole acts as a positive charge carrier, making holes the majority carriers in this $p$-type semiconductor.
- The structure exemplifies how doping silicon with boron introduces holes into the lattice, enhancing its electrical conductivity by allowing holes to move through the lattice as charge carriers.

Figure 2.6 Available hole with boron doping.

Let us formulate our results thus far. If an intrinsic semiconductor is doped with a density of $N_{D}\left(\gg n_{i}\right)$ donor atoms per cubic centimeter, then the mobile charge densities are given by

$$
\begin{align*}
& \text { Majority Carriers: } n \approx N_{D}  \tag{2.9}\\
& \text { Minority Carriers: } p \approx \frac{n_{i}^{2}}{N_{D}} . \tag{2.10}
\end{align*}
$$

Similarly, for a density of $N_{A}\left(\gg n_{i}\right)$ acceptor atoms per cubic centimeter:

$$
\begin{align*}
& \text { Majority Carriers: } p \approx N_{A}  \tag{2.11}\\
& \text { Minority Carriers: } n \approx \frac{n_{i}^{2}}{N_{A}} . \tag{2.12}
\end{align*}
$$

Since typical doping densities fall in the range of $10^{15}$ to $10^{18}$ atoms $/ \mathrm{cm}^{3}$, the above expressions are quite accurate.

| Example <br> 2.4 | Is it possible to use other elements of Fig. 2.2 as semiconductors and dopants? |
| :---: | :--- |
| Solution | Yes, for example, some early diodes and transistors were based on germanium $(\mathrm{Ge})$ <br> rather than silicon. Also, arsenic (As) is another common dopant. |

Exercise
Can carbon be used for this purpose?

Figure 2.7 summarizes the concepts introduced in this section, illustrating the types of charge carriers and their densities in semiconductors.
image_name:Intrinsic Semiconductor
description:The image consists of two main sections, illustrating the concepts of intrinsic and extrinsic semiconductors using silicon as the base material.

**1. Intrinsic Semiconductor:**
- **Components and Structure:** The top part of the image shows a simple diagram of an intrinsic semiconductor, which is a pure silicon crystal. It highlights the silicon (Si) atoms arranged in a lattice structure, forming covalent bonds with each other.
- **Connections and Interactions:** Each silicon atom shares its valence electrons with neighboring silicon atoms, creating a stable lattice with no free charge carriers.
- **Labels and Annotations:** The diagram is labeled with 'Intrinsic Semiconductor,' and arrows point to 'Covalent Bond' and 'Valence Electron,' indicating the bonding and electron sharing between silicon atoms.

**2. Extrinsic Semiconductor:**
- **Components and Structure:** The lower part of the image is divided into two sections, representing n-type and p-type extrinsic semiconductors.
- **n-Type Semiconductor:**
- **Silicon Crystal:** Doped with donor atoms, such as phosphorus (P), which introduce additional electrons into the lattice.
- **Free Majority Carrier:** The presence of extra electrons (e-) is shown, which are the majority carriers in n-type semiconductors.
- **Labels and Annotations:** Labeled with 'n-Type Dopant (Donor)' and 'Free Majority Carrier,' showing the introduction of donor atoms.
- **p-Type Semiconductor:**
- **Silicon Crystal:** Doped with acceptor atoms, such as boron (B), which create holes in the lattice.
- **Free Majority Carrier:** These holes act as the majority carriers in p-type semiconductors.
- **Labels and Annotations:** Labeled with 'p-Type Dopant (Acceptor)' and 'Free Majority Carrier,' indicating the presence of acceptor atoms.
- **Connections and Interactions:** The diagrams show how doping alters the charge carrier balance in silicon, creating free electrons in n-type and holes in p-type semiconductors. These changes allow the material to conduct electricity more effectively.
image_name:Extrinsic Semiconductor
description:The image is a diagram illustrating the concepts of intrinsic and extrinsic semiconductors using silicon as the base material.

Identification of Components and Structure:
1. **Intrinsic Semiconductor:**
- The top section of the diagram shows a simple representation of an intrinsic silicon semiconductor. It highlights silicon (Si) atoms connected by covalent bonds, with each bond representing shared valence electrons. This section emphasizes the pure crystalline structure of silicon without any impurities.

2. **Extrinsic Semiconductor:**
- The lower section of the diagram is divided into two parts, representing n-type and p-type extrinsic semiconductors.
- **n-Type Semiconductor:**
- A silicon crystal lattice is shown with an n-type dopant, such as phosphorus (P), which donates extra electrons. The diagram marks the presence of a free majority carrier (electron, e-) resulting from the doping process.
- **p-Type Semiconductor:**
- Another silicon crystal lattice is depicted with a p-type dopant, such as boron (B), which creates holes as free majority carriers. The diagram indicates the presence of these holes (depicted as open circles) within the lattice.

Connections and Interactions:
- The intrinsic silicon structure shows covalent bonding between silicon atoms, indicating stable sharing of valence electrons.
- In the extrinsic semiconductors, the doping process introduces either additional electrons or holes, which act as charge carriers, facilitating electrical conduction.

Labels, Annotations, and Key Features:
- **Intrinsic Semiconductor:** Labeled with 'Si' for silicon atoms and arrows pointing to covalent bonds and valence electrons.
- **Extrinsic Semiconductor:**
- **n-Type Dopant (Donor):** Labeled with phosphorus (P) and an electron (e-) to signify extra electrons as majority carriers.
- **p-Type Dopant (Acceptor):** Labeled with boron (B) and open circles to signify holes as majority carriers.
- The terms \(N_D\) and \(N_A\) represent the concentration of donors and acceptors per cubic centimeter, respectively.

The diagram effectively communicates the difference between intrinsic and extrinsic semiconductors, focusing on the role of dopants in creating charge carriers that enable electrical conduction.

Figure 2.7 Summary of charge carriers in silicon.

### 2.1.3 Transport of Carriers

Having studied charge carriers and the concept of doping, we are ready to examine the movement of charge in semiconductors, i.e., the mechanisms leading to the flow of current.

Drift We know from basic physics and Ohm's law that a material can conduct current in response to a potential difference and hence an electric field. ${ }^{4}$ The field accelerates the charge carriers in the material, forcing some to flow from one end to the other. Movement of charge carriers due to an electric field is called "drift."5
image_name:Figure 2.8 Drift in a semiconductor
description:The image labeled "Figure 2.8 Drift in a semiconductor" illustrates the concept of drift in a semiconductor material. The diagram features a rectangular block representing the semiconductor, with an electric field (E) applied across it, indicated by a horizontal arrow pointing from left to right.

Inside the semiconductor, several zigzag arrows depict the path of charge carriers as they move through the material. These arrows suggest that the charge carriers are accelerated by the electric field but also experience collisions with the atoms in the crystal lattice, causing a zigzag or random walk pattern. This interaction leads to a net drift of carriers in the direction of the electric field.

The semiconductor block is connected to a battery, shown below the block, with the positive terminal on the left and the negative terminal on the right. This setup creates the potential difference that establishes the electric field across the semiconductor.

Overall, the diagram effectively demonstrates the drift process, where charge carriers are influenced by the electric field and their motion is characterized by both acceleration and scattering due to collisions within the crystal structure.

Figure 2.8 Drift in a semiconductor.

Semiconductors behave in a similar manner. As shown in Fig. 2.8, the charge carriers are accelerated by the field and accidentally collide with the atoms in the crystal, eventually reaching the other end and flowing into the battery. The acceleration due to the field and the collision with the crystal counteract, leading to a constant velocity for the carriers. ${ }^{6} \mathrm{We}$ expect the velocity, $v$, to be proportional to the electric field strength, $E$ :

$$
\begin{equation*}
v \propto E \tag{2.13}
\end{equation*}
$$

and hence

$$
\begin{equation*}
v=\mu E \tag{2.14}
\end{equation*}
$$

where $\mu$ is called the "mobility" and usually expressed in $\mathrm{cm}^{2} /(\mathrm{V} \cdot \mathrm{s})$. For example in silicon, the mobility of electrons, $\mu_{n}=1350 \mathrm{~cm}^{2} /(\mathrm{V} \cdot \mathrm{s})$, and that of holes, $\mu_{p}=480 \mathrm{~cm}^{2} /(\mathrm{V} \cdot \mathrm{s})$. Of course, since electrons move in a direction opposite to the electric field, we must express the velocity vector as

$$
\begin{equation*}
\overrightarrow{v_{e}}=-\mu_{n} \vec{E} \tag{2.15}
\end{equation*}
$$

For holes, on the other hand,

$$
\begin{equation*}
\overrightarrow{v_{h}}=\mu_{p} \vec{E} \tag{2.16}
\end{equation*}
$$

[^5]Example A uniform piece of $n$-type of silicon that is $1 \mu \mathrm{~m}$ long senses a voltage of 1 V . Determine the velocity of the electrons.

Solution Since the material is uniform, we have $E=V / L$, where $L$ is the length. Thus, $E=10,000 \mathrm{~V} / \mathrm{cm}$ and hence $v=\mu_{n} E=1.35 \times 10^{7} \mathrm{~cm} / \mathrm{s}$. In other words, electrons take $(1 \mu \mathrm{~m}) /\left(1.35 \times 10^{7} \mathrm{~cm} / \mathrm{s}\right)=7.4 \mathrm{ps}$ to cross the $1-\mu \mathrm{m}$ length.

Exercise What happens if the mobility is halved?
image_name:Figure 2.9 Current flow in terms of charge density.
description:The diagram illustrates the flow of current in terms of charge density within a semiconductor bar. It is divided into two parts, each representing a different time frame: \(t = t_1\) and \(t = t_1 + 1\) second.

Main Components:
1. **Semiconductor Bar**: The main body of the diagram is a bar-like structure, which represents a semiconductor material. It has dimensions labeled as \(W\) (width), \(L\) (length), and \(h\) (height).
2. **Voltage Source \(V_1\)**: A voltage \(V_1\) is applied across the semiconductor bar, indicated by a battery symbol with positive and negative terminals.
3. **Charge Density**: The shaded region within the semiconductor represents the area where charge carriers are present.

Flow of Information or Control:
- **Electron Movement**: Electrons move from the negative terminal to the positive terminal of the voltage source, as indicated by the direction of the arrow labeled \(x\).
- **Velocity \(v\)**: The velocity of the electrons is depicted by the arrow labeled \(v\), showing the direction and magnitude of the electron flow.
- **Change Over Time**: The two parts of the diagram show the position of the charge density at two different times, \(t = t_1\) and \(t = t_1 + 1\) second, illustrating the movement of charge carriers over time.

Labels, Annotations, and Key Indicators:
- **\(x_1\)**: A specific point on the x-axis, indicating the initial position of the charge density at \(t = t_1\).
- **Meters**: The diagram specifies the measurement of distance in meters, emphasizing the scale of the semiconductor bar.

Overall System Function:
The primary function of this system is to demonstrate how charge density, represented by the shaded area, moves through a semiconductor bar when a voltage is applied. The diagram shows how the position of the charge density shifts over time due to the applied voltage, resulting in current flow. This movement is quantified by the velocity \(v\), which is influenced by the applied voltage \(V_1\) and the properties of the semiconductor material.

Figure 2.9 Current flow in terms of charge density.

With the velocity of carriers known, how is the current calculated? We first note that an electron carries a negative charge equal to $q=1.6 \times 10^{-19} \mathrm{C}$. Equivalently, a hole carries a positive charge of the same value. Now suppose a voltage $V_{1}$ is applied across a uniform semiconductor bar having a free electron density of $n$ (Fig. 2.9). Assuming the electrons move with a velocity of $v \mathrm{~m} / \mathrm{s}$, considering a cross section of the bar at $x=x_{1}$ and taking two "snapshots" at $t=t_{1}$ and $t=t_{1}+1$ second, we note that the total charge in $v$ meters passes the cross section in 1 second. In other words, the current is equal to the total charge enclosed in $v$ meters of the bar's length. Since the bar has a width of $W$, we have:

$$
\begin{equation*}
I=-v \cdot W \cdot h \cdot n \cdot q, \tag{2.17}
\end{equation*}
$$

where $v \cdot W \cdot h$ represents the volume, $n \cdot q$ denotes the charge density in coulombs, and the negative sign accounts for the fact that electrons carry negative charge.

Let us now reduce Eq. (2.13) to a more convenient form. Since for electrons, $v=-\mu_{n} E$, and since $W \cdot h$ is the cross section area of the bar, we write

$$
\begin{equation*}
J_{n}=\mu_{n} E \cdot n \cdot q, \tag{2.18}
\end{equation*}
$$

where $J_{n}$ denotes the "current density," i.e., the current passing through a unit cross section area, and is expressed in $\mathrm{A} / \mathrm{cm}^{2}$. We may loosely say, "the current is equal to the charge velocity times the charge density," with the understanding that "current" in fact refers to current density, and negative or positive signs are taken into account properly.

In the presence of both electrons and holes, Eq. (2.18) is modified to

$$
\begin{align*}
J_{\text {tot }} & =\mu_{n} E \cdot n \cdot q+\mu_{p} E \cdot p \cdot q  \tag{2.19}\\
& =q\left(\mu_{n} n+\mu_{p} p\right) E . \tag{2.20}
\end{align*}
$$

This equation gives the drift current density in response to an electric field $E$ in a semiconductor having uniform electron and hole densities.

Example In an experiment, it is desired to obtain equal electron and hole drift currents. How
2.6 should the carrier densities be chosen?

Solution We must impose

$$
\begin{equation*}
\mu_{n} n=\mu_{p} p \tag{2.21}
\end{equation*}
$$

and hence

$$
\begin{equation*}
\frac{n}{p}=\frac{\mu_{p}}{\mu_{n}} \tag{2.22}
\end{equation*}
$$

We also recall that $n p=n_{i}^{2}$. Thus,

$$
\begin{align*}
& p=\sqrt{\frac{\mu_{n}}{\mu_{p}}} n_{i}  \tag{2.23}\\
& n=\sqrt{\frac{\mu_{p}}{\mu_{n}}} n_{i} \tag{2.24}
\end{align*}
$$

For example, in silicon, $\mu_{n} / \mu_{p}=1350 / 480=2.81$, yielding

$$
\begin{align*}
p & =1.68 n_{i}  \tag{2.25}\\
n & =0.596 n_{i} \tag{2.26}
\end{align*}
$$

Since $p$ and $n$ are of the same order as $n_{i}$, equal electron and hole drift currents can occur for only a very lightly doped material. This confirms our earlier notion of majority carriers in semiconductors having typical doping levels of $10^{15}-10^{18}$ atoms $/ \mathrm{cm}^{3}$.

Exercise How should the carrier densities be chosen so that the electron drift current is twice the hole drift current?

Velocity Saturation* We have thus far assumed that the mobility of carriers in semiconductors is independent of the electric field and the velocity rises linearly with $E$ according to $v=\mu E$. In reality, if the electric field approaches sufficiently high levels, $v$ no longer follows $E$ linearly. This is because the carriers collide with the lattice so frequently and the time between the collisions is so short that they cannot accelerate much. As a result, $v$ varies "sublinearly" at high electric fields, eventually reaching a saturated level, $v_{s a t}$ (Fig. 2.10). Called "velocity saturation," this effect manifests itself in some modern transistors, limiting the performance of circuits.

In order to represent velocity saturation, we must modify $v=\mu E$ accordingly. A simple approach is to view the slope, $\mu$, as a field-dependent parameter. The expression

[^6]image_name:Figure 2.10 Velocity saturation
description:The graph depicted is a plot illustrating the concept of velocity saturation in transistors, labeled as Figure 2.10. It is a two-dimensional graph with the x-axis representing the electric field, denoted as \( E \), and the y-axis representing velocity. The axes are not labeled with specific units, indicating a general conceptual representation rather than a precise quantitative one.

The graph shows a curve that begins at the origin and rises quickly at first, indicating a rapid increase in velocity with increasing electric field. This initial steep slope corresponds to the low-field mobility, \( \mu_0 \), where the velocity \( v \) is proportional to the electric field \( E \). As the electric field continues to increase, the curve begins to flatten, indicating a sublinear increase in velocity.

The graph features a horizontal dashed line labeled \( v_{sat} \), which represents the saturation velocity. This line indicates the maximum velocity that can be achieved regardless of further increases in the electric field. The curve asymptotically approaches this saturation velocity, demonstrating the effect of velocity saturation.

Two points along the curve are marked with dotted lines extending to the y-axis, labeled \( \mu_1 \) and \( \mu_2 \). These points represent different effective mobilities at specific electric field strengths, illustrating how mobility changes with increasing electric field.

Overall, the graph effectively conveys the relationship between electric field and velocity in the context of velocity saturation, highlighting the transition from linear to saturated behavior as the electric field increases.

Figure 2.10 Velocity saturation.
for $\mu$ must therefore gradually fall toward zero as $E$ rises, but approach a constant value for small $E$; i.e.,

$$
\begin{equation*}
\mu=\frac{\mu_{0}}{1+b E} \tag{2.27}
\end{equation*}
$$

where $\mu_{0}$ is the "low-field" mobility and $b$ a proportionality factor. We may consider $\mu$ as the "effective" mobility at an electric field $E$. Thus,

$$
\begin{equation*}
v=\frac{\mu_{0}}{1+b E} E \tag{2.28}
\end{equation*}
$$

Since for $E \rightarrow \infty, v \rightarrow v_{s a t}$, we have

$$
\begin{equation*}
v_{s a t}=\frac{\mu_{0}}{b} \tag{2.29}
\end{equation*}
$$

and hence $b=\mu_{0} / v_{s a t}$. In other words,

$$
\begin{equation*}
v=\frac{\mu_{0}}{1+\frac{\mu_{0} E}{v_{s a t}}} E \tag{2.30}
\end{equation*}
$$

A uniform piece of semiconductor $0.2 \mu \mathrm{~m}$ long sustains a voltage of 1 V . If the low-field 2.7 mobility is equal to $1350 \mathrm{~cm}^{2} /(\mathrm{V} \cdot \mathrm{s})$ and the saturation velocity of the carriers $10^{7} \mathrm{~cm} / \mathrm{s}$, determine the effective mobility. Also, calculate the maximum allowable voltage such that the effective mobility is only $10 \%$ lower than $\mu_{0}$.

Solution We have

$$
\begin{align*}
E & =\frac{V}{L}  \tag{2.31}\\
& =50 \mathrm{kV} / \mathrm{cm} \tag{2.32}
\end{align*}
$$

It follows that

$$
\begin{align*}
\mu & =\frac{\mu_{0}}{1+\frac{\mu_{0} E}{v_{s a t}}}  \tag{2.33}\\
& =\frac{\mu_{0}}{7.75}  \tag{2.34}\\
& =174 \mathrm{~cm}^{2} /(\mathrm{V} \cdot \mathrm{~s}) \tag{2.35}
\end{align*}
$$

If the mobility must remain within $10 \%$ of its low-field value, then

$$
\begin{equation*}
0.9 \mu_{0}=\frac{\mu_{0}}{1+\frac{\mu_{0} E}{v_{s a t}}} \tag{2.36}
\end{equation*}
$$

and hence

$$
\begin{align*}
E & =\frac{1}{9} \frac{v_{\text {sat }}}{\mu_{0}}  \tag{2.37}\\
& =823 \mathrm{~V} / \mathrm{cm} . \tag{2.38}
\end{align*}
$$

A device of length $0.2 \mu \mathrm{~m}$ experiences such a field if it sustains a voltage of $(823 \mathrm{~V} / \mathrm{cm}) \times\left(0.2 \times 10^{-4} \mathrm{~cm}\right)=16.5 \mathrm{mV}$.

This example suggests that modern (submicron) devices incur substantial velocity saturation because they operate with voltages much greater than 16.5 mV .

Exercise At what voltage does the mobility fall by 20\%?

Diffusion In addition to drift, another mechanism can lead to current flow. Suppose a drop of ink falls into a glass of water. Introducing a high local concentration of ink molecules, the drop begins to "diffuse," that is, the ink molecules tend to flow from a region of high concentration to regions of low concentration. This mechanism is called "diffusion."

A similar phenomenon occurs if charge carriers are "dropped" (injected) into a semiconductor so as to create a nonuniform density. Even in the absence of an electric field, the carriers move toward regions of low concentration, thereby carrying an electric current so long as the nonuniformity is sustained. Diffusion is therefore distinctly different from drift.
image_name:Figure 2.11 Diffusion in a semiconductor
description:The diagram illustrates the concept of diffusion in a semiconductor. It features a rectangular block labeled 'Semiconductor Material,' representing the medium through which charge carriers move. On the left side of the block, there is an arrow labeled 'Injection of Carriers,' indicating the introduction of charge carriers into the semiconductor.

Inside the semiconductor, there is a shaded area labeled 'Nonuniform Concentration,' depicting the gradient of carrier concentration. This gradient is shown as a sloping line from left to right, suggesting a decrease in carrier concentration along the x-axis. Small circles with arrows pointing to the right are distributed along this gradient, representing the movement of charge carriers from regions of high concentration (left) to regions of low concentration (right).

The diagram visually conveys how carriers naturally diffuse down the concentration gradient, even in the absence of an electric field, thus creating an electric current. This is a conceptual representation of diffusion, distinct from drift, which involves the movement of carriers under the influence of an electric field.

Figure 2.11 Diffusion in a semiconductor.

Figure 2.11 conceptually illustrates the process of diffusion. A source on the left continues to inject charge carriers into the semiconductor, a nonuniform charge profile is created along the $x$-axis, and the carriers continue to "roll down" the profile.

The reader may raise several questions at this point. What serves as the source of carriers in Fig. 2.11? Where do the charge carriers go after they roll down to the end of the profile at the far right? And, most importantly, why should we care?! Well, patience is a virtue and we will answer these questions in the next section.

Example A source injects charge carriers into a semiconductor bar as shown in Fig. 2.12. Explain
2.8 how the current flows.
image_name:Figure 2.12 Injection of carriers into a semiconductor
description:The diagram titled "Injection of Carriers into a Semiconductor" illustrates a semiconductor bar with a symmetrical profile. It shows a central point of carrier injection, indicated by a downward arrow labeled "Injection of Carriers." This arrow points to the top center of the semiconductor bar, suggesting the introduction of charge carriers at this point.

The bar is represented as a rectangular block positioned along the x-axis, with the injection point marked as "0" on this axis. From the injection point, two symmetrical triangular profiles extend along the bar in both positive and negative x-directions.

Within these profiles, arrows are drawn pointing away from the injection point, indicating the flow of carriers towards the ends of the bar. The arrows are accompanied by small circles, representing the charge carriers moving through the semiconductor material.

Overall, the diagram visually represents the concept of charge carrier diffusion in a semiconductor, where carriers are injected at a central point and diffuse symmetrically to either side, leading to current flow along the bar.

Figure 2.12 Injection of carriers into a semiconductor.

Solution In this case, two symmetric profiles may develop in both positive and negative directions along the $x$-axis, leading to current flow from the source toward the two ends of the bar.

Exercise Is KCL still satisfied at the point of injection?

Our qualitative study of diffusion suggests that the more nonuniform the concentration, the larger the current. More specifically, we can write:

$$
\begin{equation*}
I \propto \frac{d n}{d x} \tag{2.39}
\end{equation*}
$$

where $n$ denotes the carrier concentration at a given point along the $x$-axis. We call $d n / d x$ the concentration "gradient" with respect to $x$, assuming current flow only in the $x$ direction. If each carrier has a charge equal to $q$, and the semiconductor has a cross section area of $A$, Eq. (2.39) can be written as

$$
\begin{equation*}
I \propto A q \frac{d n}{d x} \tag{2.40}
\end{equation*}
$$

Thus,

$$
\begin{equation*}
I=A q D_{n} \frac{d n}{d x} \tag{2.41}
\end{equation*}
$$

where $D_{n}$ is a proportionality factor called the "diffusion constant" and expressed in $\mathrm{cm}^{2} / \mathrm{s}$. For example, in intrinsic silicon, $D_{n}=34 \mathrm{~cm}^{2} / \mathrm{s}$ (for electrons), and $D_{p}=12 \mathrm{~cm}^{2} / \mathrm{s}$ (for holes).

As with the convention used for the drift current, we normalize the diffusion current to the cross section area, obtaining the current density as

$$
\begin{equation*}
J_{n}=q D_{n} \frac{d n}{d x} \tag{2.42}
\end{equation*}
$$

Similarly, a gradient in hole concentration yields:

$$
\begin{equation*}
J_{p}=-q D_{p} \frac{d p}{d x} \tag{2.43}
\end{equation*}
$$

With both electron and hole concentration gradients present, the total current density is given by

$$
\begin{equation*}
J_{t o t}=q\left(D_{n} \frac{d n}{d x}-D_{p} \frac{d p}{d x}\right) \tag{2.44}
\end{equation*}
$$

Example Consider the scenario depicted in Fig. 2.11 again. Suppose the electron concentration is
2.9 equal to $N$ at $x=0$ and falls linearly to zero at $x=L$ (Fig. 2.13). Determine the diffusion current.
image_name:Figure 2.13
description:**Type of Graph and Function:**
The graph is a linear diffusion profile representing the electron concentration as a function of position along the x-axis.

**Axes Labels and Units:**
- The horizontal axis (x-axis) represents position, labeled as \(x\), with units possibly in meters or centimeters, although not explicitly stated.
- The vertical axis represents electron concentration, starting from a value \(N\) at \(x = 0\) and decreasing linearly to zero at \(x = L\).

**Overall Behavior and Trends:**
The graph shows a linear decrease in electron concentration from \(N\) at \(x = 0\) to 0 at \(x = L\). This indicates a steady gradient in concentration, which is typical for diffusion processes. The linear trend suggests a constant diffusion rate.

**Key Features and Technical Details:**
- The graph starts at a point \((0, N)\) and ends at \((L, 0)\), forming a straight line with a negative slope.
- The arrows along the line indicate the direction of electron movement, pointing from high concentration to low concentration.
- The slope of the line represents the rate of change of concentration with respect to position, which is related to the diffusion current density.

**Annotations and Specific Data Points:**
- An arrow labeled "Injection" at \(x = 0\) suggests the point where electrons are introduced into the system.
- There are no specific numerical data points or additional annotations provided on the graph aside from the general shape and direction of diffusion.

Figure 2.13 Current resulting from a linear diffusion profile.

Solution We have

$$
\begin{align*}
J_{n} & =q D_{n} \frac{d n}{d x}  \tag{2.45}\\
& =-q D_{n} \cdot \frac{N}{I} \tag{2.46}
\end{align*}
$$

The current is constant along the $x$-axis; i.e., all of the electrons entering the material at $x=0$ successfully reach the point at $x=L$. While obvious, this observation prepares us for the next example.

Exercise Repeat the above example for holes.

Example
2.10 Repeat the above example but assume an exponential gradient (Fig. 2.14):
image_name:Figure 2.14
description:This graph is a plot illustrating an exponential diffusion profile, specifically depicting the concentration of particles as a function of position \(x\). The graph is a two-dimensional plot with the horizontal axis labeled \(x\), representing the position, and the vertical axis labeled with the concentration \(N\), indicating the number of particles.

Type of Graph and Function
- **Type**: Exponential decay graph.
- **Function**: \(n(x) = N \exp\left(-\frac{x}{L_d}\right)\), where \(L_d\) is a constant representing the diffusion length.

Axes Labels and Units
- **Horizontal Axis (x-axis)**: Represents position \(x\) with no specific units indicated.
- **Vertical Axis (y-axis)**: Represents concentration \(N\) with no specific units indicated.

Overall Behavior and Trends
- The graph shows an exponential decay from the initial concentration \(N\) at \(x = 0\) to a lower concentration as \(x\) increases.
- The concentration decreases rapidly near \(x = 0\) and tapers off as \(x\) approaches \(L\).

Key Features and Technical Details
- **Initial Value**: The concentration starts at a maximum of \(N\) at \(x = 0\).
- **Exponential Decay**: The concentration decreases exponentially as \(x\) increases.
- **Decay Rate**: The rate of decay is determined by the constant \(L_d\).

Annotations and Specific Data Points
- The graph is annotated with arrows indicating the direction of electron injection and movement along the \(x\)-axis.
- The curve is smooth, showing no abrupt changes or discontinuities, consistent with the exponential nature of the function.

Figure 2.14 Current resulting from an exponential diffusion profile.

$$
\begin{equation*}
n(x)=N \exp \frac{-x}{L_{d}} \tag{2.47}
\end{equation*}
$$

where $L_{d}$ is a constant. ${ }^{7}$

[^7]Solution We have

$$
\begin{align*}
J_{n} & =q D_{n} \frac{d n}{d x}  \tag{2.48}\\
& =\frac{-q D_{n} N}{L_{d}} \exp \frac{-x}{L_{d}} \tag{2.49}
\end{align*}
$$

Interestingly, the current is not constant along the $x$-axis. That is, some electrons vanish while traveling from $x=0$ to the right. What happens to these electrons? Does this example violate the law of conservation of charge? These are important questions and will be answered in the next section.

Exercise At what value of $x$ does the current density drop to $1 \%$ of its maximum value?

Einstein Relation Our study of drift and diffusion has introduced a factor for each: $\mu_{n}$ (or $\mu_{p}$ ) and $D_{n}\left(\right.$ or $\left.D_{p}\right)$, respectively. It can be proved that $\mu$ and $D$ are related as:

$$
\begin{equation*}
\frac{D}{\mu}=\frac{k T}{q} \tag{2.50}
\end{equation*}
$$

Called the "Einstein Relation," this result is proved in semiconductor physics texts, e.g., [1]. Note that $k T / q \approx 26 \mathrm{mV}$ at $T=300 \mathrm{~K}$.

Figure 2.15 summarizes the charge transport mechanisms studied in this section.
image_name:Drift Current
description:The diagram illustrates two mechanisms of charge transport in semiconductors: **Drift Current** and **Diffusion Current**.

Drift Current:
- **Main Components:**
- A semiconductor block is shown with an electric field (E) applied across it.
- Arrows inside the block indicate the movement of charge carriers (holes and electrons) in response to the electric field.
- **Flow of Information or Control:**
- The electric field (E) drives the charge carriers in a specific direction, causing a drift current.
- The drift current density for electrons \(J_n\) is given by the formula: \(J_n = qn\mu_nE\), where \(q\) is the charge of an electron, \(n\) is the electron concentration, and \(\mu_n\) is the electron mobility.
- Similarly, the drift current density for holes \(J_p\) is \(J_p = qp\mu_pE\), where \(p\) is the hole concentration, and \(\mu_p\) is the hole mobility.
- **Labels and Annotations:**
- The diagram includes equations for \(J_n\) and \(J_p\) indicating how drift current is calculated.

Diffusion Current:
- **Main Components:**
- Another semiconductor block is depicted with a gradient in carrier concentration.
- Arrows indicate the movement of charge carriers from regions of high concentration to low concentration.
- **Flow of Information or Control:**
- The concentration gradient causes charge carriers to move, resulting in a diffusion current.
- The diffusion current density for electrons \(J_n\) is given by: \(J_n = qD_n \frac{dn}{dx}\), where \(D_n\) is the electron diffusion coefficient and \(\frac{dn}{dx}\) is the gradient of electron concentration.
- For holes, the diffusion current density \(J_p\) is \(J_p = -qD_p \frac{dp}{dx}\), where \(D_p\) is the hole diffusion coefficient and \(\frac{dp}{dx}\) is the gradient of hole concentration.
- **Labels and Annotations:**
- The diagram includes equations for \(J_n\) and \(J_p\) indicating how diffusion current is calculated.

Overall System Function:
- The diagram serves to compare and contrast the two fundamental mechanisms of charge transport in semiconductors: drift and diffusion. Drift current is driven by an external electric field, while diffusion current results from concentration gradients within the material. These concepts are crucial for understanding the behavior of pn junctions and other semiconductor devices.
image_name:Diffusion Current
description:The diagram illustrates the two primary mechanisms of charge transport in semiconductors: **Drift Current** and **Diffusion Current**.

Drift Current:
- **Components:**
- A rectangular block representing the semiconductor material.
- An electric field (E) indicated by an arrow pointing in a specific direction.
- Arrows within the block showing the movement of charge carriers (electrons and holes) under the influence of the electric field.
- **Flow of Information:**
- The electric field causes charge carriers to move, resulting in a drift current.
- The current density for electrons \( J_n \) and holes \( J_p \) is given by the equations:
- \( J_n = q n \mu_n E \)
- \( J_p = q p \mu_p E \)
- Here, \( q \) is the charge, \( n \) and \( p \) are the electron and hole concentrations, and \( \mu_n \) and \( \mu_p \) are the mobilities of electrons and holes, respectively.

Diffusion Current:
- **Components:**
- Another rectangular block representing the semiconductor material.
- A concentration gradient shown by a shaded area with a slope.
- Arrows indicating the movement of charge carriers from high to low concentration.
- **Flow of Information:**
- Charge carriers move from regions of high concentration to low concentration, creating a diffusion current.
- The current density for electrons \( J_n \) and holes \( J_p \) is given by the equations:
- \( J_n = q D_n \frac{dn}{dx} \)
- \( J_p = -q D_p \frac{dp}{dx} \)
- Here, \( D_n \) and \( D_p \) are the diffusion coefficients for electrons and holes, and \( \frac{dn}{dx} \) and \( \frac{dp}{dx} \) represent the concentration gradients.

Overall System Function:
- The diagram summarizes how drift and diffusion currents operate in a semiconductor. Drift current is driven by an external electric field, while diffusion current results from concentration gradients within the material. These mechanisms are fundamental to understanding charge transport in semiconductor devices, such as the pn junction.

Figure 2.15 Summary of drift and diffusion mechanisms.

## 2.2 pn JUNCTION

We begin our study of semiconductor devices with the $p n$ junction for three reasons. (1) The device finds application in many electronic systems, e.g., in adaptors that charge the batteries of cellphones. (2) The $p n$ junction is among the simplest semiconductor devices, thus providing a good entry point into the study of the operation of such complex structures as transistors.

Did you know?

The pn junction was inadvertantly invented by Russel Ohl of Bell Laboratories in 1940. He melted silicon in quartz tubes to achieve a high purity. During the cooling process, the $p$-type and $n$-type impurities redistributed themselves, creating a pn junction. Ohl even observed that the pn junction produced a current when it was exposed to light. One wonders if Ohl ever predicted that this property would eventually lead to the invention of the digital camera.
(3) The $p n$ junction also serves as part of transistors. We also use the term "diode" to refer to $p n$ junctions.

We have thus far seen that doping produces free electrons or holes in a semiconductor, and an electric field or a concentration gradient leads to the movement of these charge carriers. An interesting situation arises if we introduce $n$-type and $p$-type dopants into two adjacent sections of a piece of semiconductor. Depicted in Fig. 2.16 and called a " $p n$ junction," this structure plays a fundamental role in many semiconductor devices. The $p$ and $n$ sides are called the "anode" and the "cathode," respectively.
image_name:(a)
description:The image consists of two parts labeled (a) and (b), representing a pn junction and its symbolic representation, respectively.

**Part (a): Physical Structure of a pn Junction**
1. **Components and Structure:**
- The diagram shows a block divided into two sections, labeled 'n' and 'p'. This represents the n-type and p-type regions of a semiconductor.
- The n-type region is doped with phosphorus (P), shown with a silicon (Si) lattice and an additional electron (e⁻), indicating the presence of free electrons.
- The p-type region is doped with boron (B), shown with a silicon lattice and a hole (depicted as an empty circle), indicating the presence of holes.

2. **Connections and Interactions:**
- The n and p regions are adjacent, forming a junction where the free electrons from the n-region can recombine with holes from the p-region.
- This junction creates an electric field that affects the movement of charge carriers, crucial for the diode's operation.

3. **Labels, Annotations, and Key Features:**
- Arrows point to the n and p regions, indicating the type of doping (phosphorus for n-type and boron for p-type).
- The structure is simplified to focus on the doping elements and their effects on the semiconductor lattice.

**Part (b): Symbolic Representation of a pn Junction**
1. **Components and Structure:**
- The diagram shows a diode symbol, with a triangle pointing towards a line.
- The triangle represents the anode (p-type region) and the line represents the cathode (n-type region).

2. **Connections and Interactions:**
- The diode symbol indicates the direction of conventional current flow, from anode to cathode, when forward biased.

3. **Labels, Annotations, and Key Features:**
- The cathode is labeled with 'k', and the anode with 'A'.
- The diode is labeled 'D', highlighting its function as a diode.
- The symbolic representation simplifies the understanding of current flow direction and diode orientation in circuits.
image_name:(b)
description:
[
name: D, type: Diode, ports: {Na: A, Nc: k}
]
extrainfo:The diagram shows a pn junction diode with an anode labeled 'A' and a cathode labeled 'k'. The diode is represented in the circuit diagram (b) with the correct orientation, where the anode is connected to 'A' and the cathode to 'k'.

Figure 2.16 pn junction.

In this section, we study the properties and I/V characteristics of pn junctions. The following outline shows our thought process, indicating that our objective is to develop circuit models that can be used in analysis and design.
image_name:Figure 2.17 Outline of concepts to be studied
description:The diagram titled "Figure 2.17 Outline of concepts to be studied" illustrates the study of pn junctions through a sequence of three main stages, each represented by a block.

1. **pn Junction in Equilibrium**:
- This block focuses on the pn junction with no external voltage applied, meaning the device is in equilibrium.
- Key concepts include the "Depletion Region," which is the area around the junction where mobile charge carriers are absent, and the "Built-in Potential," which is the electric potential that forms across the junction due to the difference in concentration of charge carriers in the p and n regions.

2. **pn Junction Under Reverse Bias**:
- This stage examines the junction when a reverse bias voltage is applied, meaning the p-type side is connected to a negative voltage relative to the n-type side.
- The primary focus is on "Junction Capacitance," which describes how the capacitance of the junction changes with the applied reverse bias, affecting the storage and release of charge across the junction.

3. **pn Junction Under Forward Bias**:
- This block addresses the condition where a forward bias is applied, with the p-type side connected to a positive voltage relative to the n-type side.
- The emphasis is on "I/V Characteristics," which refers to the current-voltage relationship and how the current through the junction increases exponentially with forward voltage.

Each block is connected sequentially with arrows, indicating the progression of study from equilibrium to reverse and then forward bias conditions. This flow represents a logical approach to understanding the behavior of pn junctions under different electrical conditions, contributing to the development of circuit models for analysis and design.

Figure 2.17 Outline of concepts to be studied.

### 2.2.1 pn Junction in Equilibrium

Let us first study the $p n$ junction with no external connections, i.e., the terminals are open and no voltage is applied across the device. We say the junction is in "equilibrium." While seemingly of no practical value, this condition provides insights that prove useful in understanding the operation under nonequilibrium as well.

We begin by examining the interface between the $n$ and $p$ sections, recognizing that one side contains a large excess of holes and the other, a large excess of electrons. The sharp concentration gradient for both electrons and holes across the junction leads to two large diffusion currents: electrons flow from the $n$ side to the $p$ side, and holes flow in the opposite direction. Since we must deal with both electron and hole concentrations on each side of the junction, we introduce the notations shown in Fig. 2.18.
image_name:Figure 2.18
description:The diagram in Figure 2.18 illustrates a pn junction, which is a fundamental concept in semiconductor physics. The diagram is divided into two main sections: the n-type semiconductor on the left and the p-type semiconductor on the right.

**Main Components:**
1. **n-type Region (Left Side):**
- Contains a high concentration of electrons (majority carriers), denoted as \( n_n \).
- Contains a low concentration of holes (minority carriers), denoted as \( p_n \).

2. **p-type Region (Right Side):**
- Contains a high concentration of holes (majority carriers), denoted as \( p_p \).
- Contains a low concentration of electrons (minority carriers), denoted as \( n_p \).

**Flow of Information or Control:**
- The diagram shows the concentration gradients of electrons and holes across the junction.
- Electrons flow from the n-type side to the p-type side, while holes flow from the p-type side to the n-type side, creating diffusion currents.

**Labels, Annotations, and Key Indicators:**
- The diagram is annotated with labels indicating the majority and minority carriers on each side.
- The concentrations \( n_n \), \( p_n \), \( p_p \), and \( n_p \) are marked to show the distribution of carriers across the junction.

**Overall System Function:**
- The primary function of this system is to illustrate the behavior of carriers in a pn junction. The sharp concentration gradient across the junction leads to diffusion currents, which are crucial for the operation of diodes and other semiconductor devices. The arrangement and flow of carriers contribute to the rectifying behavior of the pn junction, allowing it to conduct current primarily in one direction.

$\boldsymbol{n}_{\boldsymbol{n}}$ : Concentration of electrons on n side
$p_{n}$ : Concentration of holes on n side
$p_{p}$ : Concentration of holes on $p$ side
$\boldsymbol{n}_{p}$ : Concentration of electrons on $p$ side
Figure 2.18

Example A $p n$ junction employs the following doping levels: $N_{A}=10^{16} \mathrm{~cm}^{-3}$ and $N_{D}=$
2.11 $5 \times 10^{15} \mathrm{~cm}^{-3}$. Determine the hole and electron concentrations on the two sides.

Solution From Eqs. (2.11) and (2.12), we express the concentrations of holes and electrons on the $p$ side respectively as:

$$
\begin{align*}
p_{p} & \approx N_{A}  \tag{2.51}\\
& =10^{16} \mathrm{~cm}^{-3}  \tag{2.52}\\
n_{p} & \approx \frac{n_{i}^{2}}{N_{A}}  \tag{2.53}\\
& =\frac{\left(1.08 \times 10^{10} \mathrm{~cm}^{-3}\right)^{2}}{10^{16} \mathrm{~cm}^{-3}}  \tag{2.54}\\
& \approx 1.1 \times 10^{4} \mathrm{~cm}^{-3} \tag{2.55}
\end{align*}
$$

Similarly, the concentrations on the $n$ side are given by

$$
\begin{align*}
n_{n} & \approx N_{D}  \tag{2.56}\\
& =5 \times 10^{15} \mathrm{~cm}^{-3}  \tag{2.57}\\
p_{n} & \approx \frac{n_{i}^{2}}{N_{D}}  \tag{2.58}\\
& =\frac{\left(1.08 \times 10^{10} \mathrm{~cm}^{-3}\right)^{2}}{5 \times 10^{15} \mathrm{~cm}^{-3}}  \tag{2.59}\\
& =2.3 \times 10^{4} \mathrm{~cm}^{-3} \tag{2.60}
\end{align*}
$$

Note that the majority carrier concentration on each side is many orders of magnitude higher than the minority carrier concentration on either side.

The diffusion currents transport a great deal of charge from each side to the other, but they must eventually decay to zero. This is because if the terminals are left open (equilibrium condition), the device cannot carry a net current indefinitely.

We must now answer an important question: what stops the diffusion currents? We may postulate that the currents stop after enough free carriers have moved across the junction so as to equalize the concentrations on the two sides. However, another effect dominates the situation and stops the diffusion currents well before this point is reached.

To understand this effect, we recognize that for every electron that departs from the $n$ side, a positive ion is left behind, i.e., the junction evolves with time as conceptually shown in Fig. 2.19. In this illustration, the junction is suddenly formed at $t=0$, and the diffusion currents continue to expose more ions as time progresses. Consequently, the immediate vicinity of the junction is depleted of free carriers and hence called the "depletion region."
image_name:Figure 2.19 Evolution of charge concentrations in a pn junction
description:The image titled "Figure 2.19 Evolution of charge concentrations in a pn junction" illustrates the temporal evolution of charge distribution in a pn junction at three different time intervals: \( t = 0 \), \( t = t_1 \), and \( t = \infty \).

1. **Identification of Components and Structure:**
- The diagram is divided into three panels, each representing a different time stage in the formation of the pn junction.
- Each panel shows a horizontal rectangle divided into two regions: the left side labeled as \( n \) (n-type semiconductor) and the right side labeled as \( p \) (p-type semiconductor).
- At \( t = 0 \), the \( n \) side is filled with free electrons (depicted as negative signs), and the \( p \) side is filled with free holes (depicted as positive signs).

2. **Connections and Interactions:**
- At \( t = t_1 \), the diagram shows the beginning of charge depletion at the junction. Positive donor ions (depicted as circled plus signs) appear on the \( n \) side, and negative acceptor ions (depicted as circled minus signs) appear on the \( p \) side, indicating the start of the depletion region.
- At \( t = \infty \), the depletion region is fully formed and spans across the junction, with a clear separation of positive ions on the \( n \) side and negative ions on the \( p \) side, illustrating the absence of free charge carriers in this region.

3. **Labels, Annotations, and Key Features:**
- The depletion region is explicitly labeled in the final panel, highlighting the area devoid of free carriers.
- Arrows in the first panel indicate the presence of free electrons and holes on their respective sides.
- The progression from free carriers to a fully formed depletion region is central to understanding the pn junction's behavior over time.

Figure 2.19 Evolution of charge concentrations in a pn junction.
Now recall from basic physics that a particle or object carrying a net (nonzero) charge creates an electric field around it. Thus, with the formation of the depletion region, an electric field emerges as shown in Fig. 2.20. ${ }^{8}$ Interestingly, the field tends to force positive charge flow from left to right whereas the concentration gradients necessitate the flow of holes from right to left (and electrons from left to right). We therefore surmise that the junction reaches equilibrium once the electric field is strong enough to completely stop the diffusion currents. Alternatively, we can say, in equilibrium, the drift currents resulting from the electric field exactly cancel the diffusion currents due to the gradients.
image_name:Figure 2.20 Electric field in a pn junction
description:The image depicts a pn junction with an emphasis on the electric field and charge distribution across the junction. The diagram is divided into three main regions: the n-type region on the left, the depletion region in the center, and the p-type region on the right.

1. **Identification of Components and Structure:**
- **n-type Region:** This area on the left is marked by negative signs, indicating the presence of free electrons.
- **Depletion Region:** The central area is marked by a series of positive and negative charges. The positive charges are on the side closer to the n-type region, and the negative charges are on the side closer to the p-type region. This area represents the space charge region where mobile charge carriers have diffused away, leaving behind fixed ions.
- **p-type Region:** This area on the right is marked by positive signs, indicating the presence of holes.

2. **Connections and Interactions:**
- The electric field, denoted by the arrow labeled 'E', points from the n-type region towards the p-type region, indicating the direction of force exerted on positive charges. This field arises due to the separation of charges in the depletion region.
- The diagram illustrates the balance of forces at equilibrium, where the electric field counteracts the diffusion of electrons and holes.

3. **Labels, Annotations, and Key Features:**
- The regions are labeled as 'n' and 'p' to denote the n-type and p-type semiconductor materials, respectively.
- The arrow labeled 'E' indicates the direction and presence of the electric field across the junction.
- Dashed lines separate the depletion region from the n-type and p-type regions, highlighting the boundaries of the space charge region.

Figure 2.20 Electric field in a pn junction.

[^8]Example
2.12

In the junction shown in Fig. 2.21, the depletion region has a width of $b$ on the $n$ side and $a$ on the $p$ side. Sketch the electric field as a function of $x$.
image_name:Figure 2.20 Electric field in a pn junction
description:The image titled "Figure 2.20 Electric field in a pn junction" illustrates the electric field distribution across a pn junction. It consists of two main parts: a diagram of the pn junction and a graph showing the electric field profile.

1. **Identification of Components and Structure:**
- The top part of the image shows a schematic representation of a pn junction. The junction is divided into three regions: the n-type region on the left, the depletion region in the middle, and the p-type region on the right.
- The n-type region is labeled with "n" and contains negatively charged donor ions, represented by negative signs, and is marked with the symbol $N_D$.
- The p-type region is labeled with "p" and contains positively charged acceptor ions, represented by positive signs, and is marked with the symbol $N_A$.
- The depletion region, located between the n-type and p-type regions, contains both positive and negative charges, depicted as circles with plus and minus signs.
- A dashed line separates the depletion region from the n-type and p-type regions, indicating the boundaries of the space charge region.

2. **Connections and Interactions:**
- An arrow labeled 'E' above the junction indicates the direction of the electric field across the junction, pointing from the n-type to the p-type region.

3. **Labels, Annotations, and Key Features:**
- The x-axis is labeled with positions: $-b$, 0, and $a$, indicating the width of the depletion region on the n-side and p-side respectively.
- Below the schematic, a graph depicts the electric field (E) as a function of position (x). The electric field is zero outside the depletion region ($x < -b$ and $x > a$) and reaches a maximum at the junction center ($x = 0$).
- The electric field profile is triangular, rising from zero at $x = -b$, peaking at $x = 0$, and then falling back to zero at $x = a$. This illustrates how the electric field is strongest at the center of the depletion region and diminishes towards the edges.
image_name:Figure 2.21 Electric field profile in a pn junction
description:The graph in Figure 2.21 is a plot of the electric field (E) as a function of position (x) across a pn junction. The x-axis represents the position along the junction, with units likely in micrometers or nanometers, while the y-axis represents the electric field (E), possibly in units of volts per meter (V/m).

**Type of Graph and Function:**
This is a linear plot showing the variation of the electric field across the depletion region of a pn junction.

**Axes Labels and Units:**
- **X-axis:** Position (x) with specific markers at -b, 0, and a.
- **Y-axis:** Electric field (E), units not explicitly stated but typically in V/m.

**Overall Behavior and Trends:**
- For x < -b, the electric field is zero, indicating no net charge in this region.
- As x increases from -b to 0, the electric field increases linearly, reaching a peak at x = 0. This rise is due to the contribution of positive donor ions in the n-type region.
- For 0 < x < a, the electric field decreases linearly back to zero at x = a. This decline is due to the negative acceptor ions in the p-type region counteracting the field.
- For x > a, the electric field remains zero, indicating charge neutrality.

**Key Features and Technical Details:**
- The graph is symmetric about x = 0, with the peak at x = 0 representing the maximum electric field strength.
- The boundaries of the depletion region are marked at -b and a, where the electric field transitions from zero to a non-zero value and back to zero, respectively.

**Annotations and Specific Data Points:**
- The graph is annotated with dashed lines at x = -b and x = a to indicate the edges of the depletion region.
- The peak electric field occurs at x = 0, though the exact value is not specified in the graph.

Figure 2.21 Electric field profile in a pn junction.

Solution Beginning at $x<-b$, we note that the absence of net charge yields $E=0$. At $x>-b$, each positive donor ion contributes to the electric field, i.e., the magnitude of $E$ rises as $x$ approaches zero. As we pass $x=0$, the negative acceptor atoms begin to contribute negatively to the field, i.e., $E$ falls. At $x=a$, the negative and positive charge exactly cancel each other and $E=0$.

Exercise Noting that potential voltage is negative integral of electric field with respect to distance, plot the potential as a function of $x$.

From our observation regarding the drift and diffusion currents under equilibrium, we may be tempted to write:

$$
\begin{equation*}
\left|I_{\mathrm{drift}, p}+I_{\mathrm{drift}, n}\right|=\left|I_{\mathrm{diff}, p}+I_{\mathrm{diff}, n}\right| \tag{2.61}
\end{equation*}
$$

where the subscripts $p$ and $n$ refer to holes and electrons, respectively, and each current term contains the proper polarity. This condition, however, allows an unrealistic phenomenon: if the number of the electrons flowing from the $n$ side to the $p$ side is equal to that of the holes going from the $p$ side to the $n$ side, then each side of this equation is zero while electrons continue to accumulate on the $p$ side and holes on the $n$ side. We must therefore impose the equilibrium condition on each carrier:

$$
\begin{align*}
\left|I_{\mathrm{drift}, p}\right| & =\left|I_{\mathrm{diff}, p}\right|  \tag{2.62}\\
\left|I_{\mathrm{drift}, n}\right| & =\left|I_{\mathrm{diff}, n}\right| \tag{2.63}
\end{align*}
$$

Built-in Potential The existence of an electric field within the depletion region suggests that the junction may exhibit a "built-in potential." In fact, using (2.62) or (2.63), we can compute this potential. Since the electric field $E=-d V / d x$, and since (2.62) can be written as

$$
\begin{equation*}
q \mu_{p} p E=q D_{p} \frac{d p}{d x} \tag{2.64}
\end{equation*}
$$

we have

$$
\begin{equation*}
-\mu_{p} p \frac{d V}{d x}=D_{p} \frac{d p}{d x} . \tag{2.65}
\end{equation*}
$$

Dividing both sides by $p$ and taking the integral, we obtain

$$
\begin{equation*}
-\mu_{p} \int_{x_{1}}^{x_{2}} d V=D_{p} \int_{p_{n}}^{p_{p}} \frac{d p}{p} \tag{2.66}
\end{equation*}
$$

where $p_{n}$ and $p_{p}$ are the hole concentrations at $x_{1}$ and $x_{2}$, respectively (Fig. 2.22). Thus,

$$
\begin{equation*}
V\left(x_{2}\right)-V\left(x_{1}\right)=-\frac{D_{p}}{\mu_{p}} \ln \frac{p_{p}}{p_{n}} . \tag{2.67}
\end{equation*}
$$

image_name:Figure 2.22
description:The graph in Figure 2.22 is a schematic representation of carrier concentration profiles in a p-n junction. It is a type of graph that shows the spatial distribution of charge carriers across the junction.

**Axes Labels and Units:**
- The horizontal axis represents the position \(x\) across the junction, with no specific units provided. The axis is divided into three regions: the n-type region, the depletion region, and the p-type region, marked by two vertical dashed lines at \(x_1\) and \(x_2\).
- The vertical axis represents the concentration of carriers, though specific units are not mentioned. The concentrations are labeled for electrons and holes in both the n-type and p-type regions.

**Overall Behavior and Trends:**
- In the n-type region (left side of \(x_1\)), the electron concentration \(n_n\) is high and remains constant, while the hole concentration \(p_n\) is low and constant.
- In the p-type region (right side of \(x_2\)), the hole concentration \(p_p\) is high and constant, while the electron concentration \(n_p\) is low and constant.
- Within the depletion region (between \(x_1\) and \(x_2\)), the graph does not explicitly show the carrier concentrations, indicating a region depleted of free carriers.

**Key Features and Technical Details:**
- The graph clearly distinguishes between the n-type and p-type regions by the carrier concentrations.
- The depletion region is highlighted by the absence of carrier concentration lines, implying a significant drop or absence of free carriers in this region.

**Annotations and Specific Data Points:**
- The concentrations are labeled as \(n_n\), \(p_n\), \(p_p\), and \(n_p\) for the respective regions.
- The transition points at \(x_1\) and \(x_2\) are marked with dashed lines, indicating the boundaries of the depletion region.

Figure 2.22 Carrier profiles in a $p n$ junction.
The right side represents the voltage difference developed across the depletion region and will be denoted by $V_{0}$. Also, from Einstein's relation, Eq. (2.50), we can replace $D_{p} / \mu_{p}$ with $k T / q$ :

$$
\begin{equation*}
\left|V_{0}\right|=\frac{k T}{q} \ln \frac{p_{p}}{p_{n}} . \tag{2.68}
\end{equation*}
$$

Exercise Writing Eq. (2.64) for electron drift and diffusion currents, and carrying out the integration, derive an equation for $V_{0}$ in terms of $n_{n}$ and $n_{p}$.

Finally, using (2.11) and (2.10) for $p_{p}$ and $p_{n}$ yields

$$
\begin{equation*}
V_{0}=\frac{k T}{q} \ln \frac{N_{A} N_{D}}{n_{i}^{2}} . \tag{2.69}
\end{equation*}
$$

Expressing the built-in potential in terms of junction parameters, this equation plays a central role in many semiconductor devices.

Example

A silicon $p n$ junction employs $N_{A}=2 \times 10^{16} \mathrm{~cm}^{-3}$ and $N_{D}=4 \times 10^{16} \mathrm{~cm}^{-3}$. Determine 2.13 the built-in potential at room temperature ( $T=300 \mathrm{~K}$ ).

Solution Recall from Example 2.1 that $n_{i}(T=300 \mathrm{~K})=1.08 \times 10^{10} \mathrm{~cm}^{-3}$. Thus,

$$
\begin{align*}
V_{0} & \approx(26 \mathrm{mV}) \ln \frac{\left(2 \times 10^{16}\right) \times\left(4 \times 10^{16}\right)}{\left(1.08 \times 10^{10}\right)^{2}}  \tag{2.70}\\
& \approx 768 \mathrm{mV} \tag{2.71}
\end{align*}
$$

Exercise $\quad$ By what factor should $N_{D}$ be changed to lower $V_{0}$ by 20 mV ?

Example Equation (2.69) reveals that $V_{0}$ is a weak function of the doping levels. How much does 2.14 $V_{0}$ change if $N_{A}$ or $N_{D}$ is increased by one order of magnitude?

Solution We can write

$$
\begin{align*}
\Delta V_{0} & =V_{T} \ln \frac{10 N_{A} \cdot N_{D}}{n_{i}^{2}}-V_{T} \ln \frac{N_{A} \cdot N_{D}}{n_{i}^{2}}  \tag{2.72}\\
& =V_{T} \ln 10  \tag{2.73}\\
& \approx 60 \mathrm{mV}(\text { at } T=300 \mathrm{~K}) . \tag{2.74}
\end{align*}
$$

Exercise How much does $V_{0}$ change if $N_{A}$ or $N_{D}$ is increased by a factor of three?

An interesting question may arise at this point. The junction carries no net current (because its terminals remain open), but it sustains a voltage. How is that possible? We observe that the built-in potential is developed to oppose the flow of diffusion currents (and is, in fact, sometimes called the "potential barrier"). This phenomenon is in contrast to the behavior of a uniform conducting material, which exhibits no tendency for diffusion and hence no need to create a built-in voltage.

### 2.2.2 pn Junction Under Reverse Bias

Having analyzed the pn junction in equilibrium, we can now study its behavior under more interesting and useful conditions. Let us begin by applying an external voltage across the device as shown in Fig. 2.23, where the voltage source makes the $n$ side more positive than the $p$ side. We say the junction is under "reverse bias" to emphasize the connection of the positive voltage to the $n$ terminal. Used as a noun or a verb, the term "bias" indicates operation under some "desirable" conditions. We will study the concept of biasing extensively in this and following chapters.
image_name:Figure 2.23 pn junction under reverse bias
description:
[
name: VR, type: VoltageSource, value: VR, ports: {Np: n, Nn: p}
]
extrainfo:The diagram shows a pn junction under reverse bias, where the voltage source VR makes the n side more positive than the p side. This configuration increases the width of the depletion region, reducing the junction capacitance.

Figure 2.23 pn junction under reverse bias.
image_name:(a)
description:
[
name: VR1, type: VoltageSource, value: VR1, ports: {Np: n, Nn: p}
]
extrainfo:The diagram illustrates a pn junction under reverse bias with a voltage source VR1. This configuration increases the depletion region width, reducing the junction capacitance. The reverse bias enhances the built-in electric field from the n side to the p side.
image_name:(b)
description:
[
name: VR2, type: VoltageSource, value: VR2, ports: {Np: n, Nn: p}
]
extrainfo:Figure 2.23 illustrates a pn junction under reverse bias with voltage source VR2. This configuration increases the depletion region width, reducing junction capacitance. VR2 is more negative than VR1, enhancing the electric field from the n to p side.

Figure 2.24 Reduction of junction capacitance with reverse bias.

We wish to reexamine the results obtained in equilibrium for the case of reverse bias. Let us first determine whether the external voltage enhances the built-in electric field or opposes it. Since under equilibrium, $\vec{E}$ is directed from the $n$ side to the $p$ side, $V_{R}$ enhances the field. But, a higher electric field can be sustained only if a larger amount of fixed charge is provided, requiring that more acceptor and donor ions be exposed and, therefore, the depletion region be widened.

What happens to the diffusion and drift currents? Since the external voltage has strengthened the field, the barrier rises even higher than that in equilibrium, thus prohibiting the flow of current. In other words, the junction carries a negligible current under reverse bias. ${ }^{9}$

With no current conduction, a reverse-biased pn junction does not seem particularly useful. However, an important observation will prove otherwise. We note that in Fig. 2.23, as $V_{B}$ increases, more positive charge appears on the $n$ side and more negative charge on the $p$ side. Thus, the device operates as a capacitor [Fig. 2.24(a)]. In essence, we can view the conductive $n$ and $p$ sections as the two plates of the capacitor. We also assume the charge in the depletion region equivalently resides on each plate.

The reader may still not find the device interesting. After all, since any two parallel plates can form a capacitor, the use of a pn junction for this purpose is not justified. But, reverse-biased $p n$ junctions exhibit a unique property that becomes useful in circuit design. Returning to Fig. 2.23, we recognize that, as $V_{R}$ increases, so does the width of the depletion region. That is, the conceptual diagram of Fig. 2.24(a) can be drawn as in Fig. 2.24(b) for increasing values of $V_{R}$, revealing that the capacitance of the structure decreases as the two plates move away from each other. The junction therefore displays a voltage-dependent capacitance.

It can be proved that the capacitance of the junction per unit area is equal to

$$
\begin{equation*}
C_{j}=\frac{C_{j 0}}{\sqrt{1-\frac{V_{R}}{V_{0}}}} \tag{2.75}
\end{equation*}
$$

${ }^{9}$ As explained in Section 2.2.3, the current is not exactly zero.
where $C_{j 0}$ denotes the capacitance corresponding to zero bias $\left(V_{R}=0\right)$ and $V_{0}$ is the builtin potential [Eq. (2.69)]. (This equation assumes $V_{R}$ is negative for reverse bias.) The value of $C_{j 0}$ is in turn given by

$$
\begin{equation*}
C_{j 0}=\sqrt{\frac{\epsilon_{s i} q}{2} \frac{N_{A} N_{D}}{N_{A}+N_{D}} \frac{1}{V_{0}}} \tag{2.76}
\end{equation*}
$$

where $\epsilon_{s i}$ represents the dielectric constant of silicon and is equal to $11.7 \times$ $8.85 \times 10^{-14} \mathrm{~F} / \mathrm{cm} .{ }^{10}$ Plotted in Fig. 2.25, $C_{j}$ indeed decreases as $V_{R}$ increases.
image_name:Figure 2.25 Junction capacitance under reverse bias
description:The graph in Figure 2.25 is a plot of junction capacitance (C_j) versus reverse bias voltage (V_R) for a pn junction. It is a typical representation of how the capacitance of a junction diode changes with applied reverse bias voltage.

1. **Type of Graph and Function:**
- The graph is a two-dimensional plot showing the relationship between junction capacitance and reverse bias voltage.

2. **Axes Labels and Units:**
- The horizontal axis represents the reverse bias voltage (V_R). The units are typically volts (V), although not explicitly labeled in the provided image.
- The vertical axis represents the junction capacitance (C_j), which is measured in farads (F), though specific units are not shown in the image.

3. **Overall Behavior and Trends:**
- The graph shows a decreasing trend of capacitance with increasing reverse bias voltage. This is indicative of the depletion region widening as the reverse bias increases, thereby reducing the capacitance.
- The curve starts at a higher capacitance value when V_R is zero and gradually decreases as V_R increases, following an inverse relationship.

4. **Key Features and Technical Details:**
- The curve is non-linear and follows a hyperbolic-like decay, which is typical for junction capacitance versus reverse bias voltage plots.
- The capacitance decreases rapidly at lower reverse bias voltages and then tapers off, indicating a reduction in the rate of change of capacitance at higher voltages.

5. **Annotations and Specific Data Points:**
- There are no specific annotations or numerical values provided on the graph, but the general trend is clear: as V_R increases, C_j decreases.

Figure 2.25 Junction capacitance under reverse bias.

Example A pn junction is doped with $N_{A}=2 \times 10^{16} \mathrm{~cm}^{-3}$ and $N_{D}=9 \times 10^{15} \mathrm{~cm}^{-3}$. Determine 2.15 the capacitance of the device with (a) $V_{R}=0$ and $V_{R}=1 \mathrm{~V}$.

Solution We first obtain the built-in potential:

$$
\begin{align*}
V_{0} & =V_{T} \ln \frac{N_{A} N_{D}}{n_{i}^{2}}  \tag{2.77}\\
& =0.73 \mathrm{~V} . \tag{2.78}
\end{align*}
$$

Thus, for $V_{R}=0$ and $q=1.6 \times 10^{-19} \mathrm{C}$, we have

$$
\begin{align*}
C_{j 0} & =\sqrt{\frac{\epsilon_{s i} q}{2} \frac{N_{A} N_{D}}{N_{A}+N_{D}} \cdot \frac{1}{V_{0}}}  \tag{2.79}\\
& =2.65 \times 10^{-8} \mathrm{~F} / \mathrm{cm}^{2} . \tag{2.80}
\end{align*}
$$

In microelectronics, we deal with very small devices and may rewrite this result as

$$
\begin{equation*}
C_{j 0}=0.265 \mathrm{fF} / \mu \mathrm{m}^{2} \tag{2.81}
\end{equation*}
$$

[^9]where $1 \mathrm{fF}($ femtofarad $)=10^{-15} \mathrm{~F}$. For $V_{R}=1 \mathrm{~V}$,
\$\$

$$
\begin{align*}
C_{j} & =\frac{C_{j 0}}{\sqrt{1+\frac{V_{R}}{V_{0}}}}  \tag{2.82}\\
& =0.172 \mathrm{fF} / \mu \mathrm{m}^{2} \tag{2.83}
\end{align*}
$$

\$\$

Exercise Repeat the above example if the donor concentration on the $N$ side is doubled. Compare the results in the two cases.

The variation of the capacitance with the applied voltage makes the device a "nonlinear" capacitor because it does not satisfy $Q=C V$. Nonetheless, as demonstrated by the following example, a voltage-dependent capacitor leads to interesting circuit topologies.

Example A cellphone incorporates a 2-GHz oscillator whose frequency is defined by the resonance

frequency of an $L C \operatorname{tank}$ (Fig. 2.26). If the tank capacitance is realized as the $p n$ junction of Example 2.15, calculate the change in the oscillation frequency while the reverse voltage goes from 0 to 2 V . Assume the circuit operates at 2 GHz at a reverse voltage of 0 V , and the junction area is $2000 \mu \mathrm{~m}^{2}$.
image_name:Figure 2.26 Variable capacitor used to tune an oscillator
description:
[
name: C, type: Capacitor, value: C, ports: {Np: X2, Nn: X1}
name: L, type: Inductor, value: L, ports: {N1: X2, N2: X1}
name: VR, type: VoltageSource, value: VR, ports: {Np: VR, Nn: X1}
]
extrainfo:The circuit is an LC oscillator with a variable capacitor C, an inductor L, and a voltage source VR. The capacitor C is connected between nodes X2 and X1, and the inductor L is parallel to the capacitor. The voltage source VR is connected to node X1.

Figure 2.26 Variable capacitor used to tune an oscillator.

Solution Recall from basic circuit theory that the tank "resonates" if the impedances of the inductor and the capacitor are equal and opposite: $j L \omega_{\text {res }}=-\left(j C \omega_{\text {res }}\right)^{-1}$. Thus, the resonance frequency is equal to

$$
\begin{equation*}
f_{\text {res }}=\frac{1}{2 \pi} \frac{1}{\sqrt{L C}} \tag{2.84}
\end{equation*}
$$

At $V_{R}=0, C_{j}=0.265 \mathrm{fF} / \mu \mathrm{m}^{2}$, yielding a total device capacitance of

$$
\begin{align*}
C_{j, t o t}\left(V_{R}=0\right) & =\left(0.265 \mathrm{fF} / \mu \mathrm{m}^{2}\right) \times\left(2000 \mu \mathrm{~m}^{2}\right)  \tag{2.85}\\
& =530 \mathrm{fF} . \tag{2.86}
\end{align*}
$$

Setting $f_{\text {res }}$ to 2 GHz , we obtain

$$
\begin{equation*}
L=11.9 \mathrm{nH} \tag{2.87}
\end{equation*}
$$

If $V_{R}$ goes to 2 V ,

$$
\begin{align*}
C_{j, t o t}\left(V_{R}=2 \mathrm{~V}\right) & =\frac{C_{j 0}}{\sqrt{1+\frac{2}{0.73}}} \times 2000 \mu \mathrm{~m}^{2}  \tag{2.88}\\
& =274 \mathrm{fF} . \tag{2.89}
\end{align*}
$$

Using this value along with $L=11.9 \mathrm{nH}$ in Eq. (2.84), we have

$$
\begin{equation*}
f_{r e s}\left(V_{R}=2 \mathrm{~V}\right)=2.79 \mathrm{GHz} \tag{2.90}
\end{equation*}
$$

An oscillator whose frequency can be varied by an external voltage ( $V_{R}$ in this case) is called a "voltage-controlled oscillator" and used extensively in cellphones, microprocessors, personal computers, etc.

Exercise Some wireless systems operate at 5.2 GHz . Repeat the above example for this frequency, assuming the junction area is still $2000 \mu \mathrm{~m}^{2}$ but the inductor value is scaled to reach 5.2 GHz .

In summary, a reverse-biased $p n$ junction carries a negligible current but exhibits a voltage-dependent capacitance. Note that we have tacitly developed a circuit model for the device under this condition: a simple capacitance whose value is given by Eq. (2.75).

Another interesting application of reverse-biased diodes is in digital cameras (Chapter 1). If light of sufficient energy is applied to a pn junction, electrons are dislodged from their covalent bonds and hence electron-hole pairs are created. With a reverse bias, the electrons are attracted to the positive battery terminal and the holes to the negative battery terminal. As a result, a current flows through the diode that is proportional to the light intensity. We say the pn junction operates as a "photodiode."

### 2.2.3 pn Junction Under Forward Bias

Our objective in this section is to show that the $p n$ junction carries a current if the $p$ side is raised to a more positive voltage than the $n$ side (Fig. 2.27). This condition is called "forward bias." We also wish to compute the resulting current in terms of the applied voltage and the junction parameters, ultimately arriving at a circuit model.
image_name:Figure 2.27 pn junction under forward bias
description:
[
name: VF, type: VoltageSource, value: VF, ports: {Np: VFP, Nn: VFN}
]
extrainfo:The diagram shows a pn junction under forward bias, where the p-side is connected to a positive voltage (VFP) and the n-side to a negative voltage (VFN) through a voltage source VF. This configuration reduces the potential barrier, allowing current to flow through the junction.

Figure $2.27 p n$ junction under forward bias.

From our study of the device in equilibrium and reverse bias, we note that the potential barrier developed in the depletion region determines the device's desire to conduct. In forward bias, the external voltage, $V_{F}$, tends to create a field directed from the $p$ side toward the $n$ side-opposite to the built-in field that was developed to stop the diffusion currents. We therefore surmise that $V_{F}$ in fact lowers the potential barrier by weakening the field, thus allowing greater diffusion currents.

To derive the I/V characteristic in forward bias, we begin with Eq. (2.68) for the built-in voltage and rewrite it as

$$
\begin{equation*}
p_{n, e}=\frac{p_{p, e}}{\exp \frac{V_{0}}{V_{T}}} \tag{2.91}
\end{equation*}
$$

where the subscript $e$ emphasizes equilibrium conditions [Fig. 2.28(a)] and $V_{T}=k T / q$ is called the "thermal voltage" ( $\approx 26 \mathrm{mV}$ at $T=300 \mathrm{~K})$. In forward bias, the potential barrier is lowered by an amount equal to the applied voltage:

$$
\begin{equation*}
p_{n, f}=\frac{p_{p, f}}{\exp \frac{V_{0}-V_{F}}{V_{T}}} \tag{2.92}
\end{equation*}
$$

where the subscript $f$ denotes forward bias. Since the exponential denominator drops considerably, we expect $p_{n, f}$ to be much higher than $p_{n, e}$ (it can be proved that $p_{p, f} \approx p_{p, e} \approx N_{A}$ ). In other words, the minority carrier concentration on the $p$ side rises rapidly with the forward bias voltage while the majority carrier concentration remains relatively constant. This statement applies to the $n$ side as well.
image_name:(a)
description:Figure 2.28(a) depicts the carrier profiles in a semiconductor junction at equilibrium. The graph is a schematic representation showing the distribution of carrier concentrations across the junction. The horizontal axis represents the spatial position across the junction, with the left side labeled as the 'n' region and the right side as the 'p' region. The vertical axis represents carrier concentration, although specific units are not provided.

In this equilibrium state, two main curves are illustrated:

1. **Majority Carrier Concentrations:** The curve labeled \( n_{n,e} \) represents the electron concentration in the n-region, and \( p_{p,e} \) represents the hole concentration in the p-region. These curves are depicted as gradually decreasing as they approach the junction from their respective sides, indicating the expected drop in majority carrier concentration near the junction.

2. **Minority Carrier Concentrations:** The curve labeled \( p_{n,e} \) represents the hole concentration in the n-region, and \( n_{p,e} \) represents the electron concentration in the p-region. These curves are shown as increasing as they approach the junction, reflecting the diffusion of minority carriers.

Overall, the graph shows a symmetrical profile with the majority and minority carrier concentrations intersecting at the junction, illustrating the balance of carrier distributions in equilibrium.
image_name:(b)
description:The graph labeled as Figure 2.28(b) illustrates the carrier concentration profiles in a semiconductor junction under forward bias conditions. This is a schematic representation showing how the concentration of charge carriers changes when a forward voltage \( V_F \) is applied across the junction.

1. **Type of Graph and Function:**
- The diagram is a conceptual illustration rather than a numerical graph, depicting the variation in carrier concentrations across a PN junction under forward bias.

2. **Axes Labels and Units:**
- The diagram does not have traditional axes with numerical labels or units. Instead, it shows the qualitative relationship between carrier concentrations on the \( n \) and \( p \) sides of the junction.

3. **Overall Behavior and Trends:**
- Under forward bias, the minority carrier concentrations \( p_{n,f} \) and \( n_{p,f} \) increase significantly compared to their equilibrium values \( p_{n,e} \) and \( n_{p,e} \). This is depicted by the upward arrows and increased separation of the curves on both sides of the junction.
- The majority carrier concentrations \( n_{n,f} \) and \( p_{p,f} \) remain relatively stable, shown by the more horizontal and less varying lines.

4. **Key Features and Technical Details:**
- The diagram highlights the increase in minority carrier concentrations with forward bias, indicating enhanced diffusion currents across the junction.
- The forward voltage \( V_F \) is depicted as a battery connected across the junction, with the positive terminal connected to the \( p \) side and the negative terminal to the \( n \) side.

5. **Annotations and Specific Data Points:**
- The diagram is annotated with labels for the minority and majority carrier concentrations in both equilibrium and forward bias states (e.g., \( p_{n,e}, p_{n,f}, n_{p,e}, n_{p,f} \)).
- Arrows indicate the direction of increased minority carrier concentration under forward bias, providing a visual cue for the changes occurring at the junction.

Figure 2.28 Carrier profiles (a) in equilibrium and (b) under forward bias.
Figure 2.28(b) illustrates the results of our analysis thus far. As the junction goes from equilibrium to forward bias, $n_{p}$ and $p_{n}$ increase dramatically, leading to a proportional change in the diffusion currents. ${ }^{11}$ We can express the change in the hole concentration on the $n$ side as:

$$
\begin{align*}
\Delta p_{n} & =p_{n, f}-p_{n, e}  \tag{2.93}\\
& =\frac{p_{p, f}}{\exp \frac{V_{0}-V_{F}}{V_{T}}}-\frac{p_{p, e}}{\exp \frac{V_{0}}{V_{T}}}  \tag{2.94}\\
& \approx \frac{N_{A}}{\exp \frac{V_{0}}{V_{T}}}\left(\exp \frac{V_{F}}{V_{T}}-1\right) . \tag{2.95}
\end{align*}
$$

[^10]Similarly, for the electron concentration on the $p$ side:

$$
\begin{equation*}
\Delta n_{p} \approx \frac{N_{D}}{\exp \frac{V_{0}}{V_{T}}}\left(\exp \frac{V_{F}}{V_{T}}-1\right) . \tag{2.96}
\end{equation*}
$$

Note that Eq. (2.69) indicates that $\exp \left(V_{0} / V_{T}\right)=N_{A} N_{D} / n_{i}^{2}$.
The increase in the minority carrier concentration suggests that the diffusion currents must rise by a proportional amount above their equilibrium value, i.e.,

$$
\begin{equation*}
I_{t o t} \propto \frac{N_{A}}{\exp \frac{V_{0}}{V_{T}}}\left(\exp \frac{V_{F}}{V_{T}}-1\right)+\frac{N_{D}}{\exp \frac{V_{0}}{V_{T}}}\left(\exp \frac{V_{F}}{V_{T}}-1\right) . \tag{2.97}
\end{equation*}
$$

Indeed, it can be proved that [1]

$$
\begin{equation*}
I_{\text {tot }}=I_{S}\left(\exp \frac{V_{F}}{V_{T}}-1\right), \tag{2.98}
\end{equation*}
$$

where $I_{S}$ is called the "reverse saturation current" and given by

$$
\begin{equation*}
I_{S}=A q n_{i}^{2}\left(\frac{D_{n}}{N_{A} L_{n}}+\frac{D_{p}}{N_{D} L_{p}}\right) \tag{2.99}
\end{equation*}
$$

In this equation, $A$ is the cross section area of the device, and $L_{n}$ and $L_{p}$ are electron and hole "diffusion lengths," respectively. Diffusion lengths are typically in the range of tens of micrometers. Note that the first and second terms in the parentheses correspond to the flow of electrons and holes, respectively.

Determine $I_{S}$ for the junction of Example 2.13 at $T=300 \mathrm{~K}$ if $A=100 \mu \mathrm{~m}^{2}, L_{n}=20 \mu \mathrm{~m}$, and $L_{p}=30 \mu \mathrm{~m}$.

Solution Using $q=1.6 \times 10^{-19} \mathrm{C}, n_{i}=1.08 \times 10^{10}$ electrons $/ \mathrm{cm}^{3}$ [Eq. (2.2)], $D_{n}=34 \mathrm{~cm}^{2} / \mathrm{s}$, and $D_{p}=12 \mathrm{~cm}^{2} / \mathrm{s}$, we have

$$
\begin{equation*}
I_{S}=1.77 \times 10^{-17} \mathrm{~A} \tag{2.100}
\end{equation*}
$$

Since $I_{S}$ is extremely small, the exponential term in Eq. (2.98) must assume very large values so as to yield a useful amount (e.g., 1 mA ) for $I_{t o t}$.

Exercise What junction area is necessary to raise $I_{S}$ to $10^{-15} \mathrm{~A}$ ?

An interesting question that arises here is: are the minority carrier concentrations constant along the $x$-axis? Depicted in Fig. 2.29(a), such a scenario would suggest that electrons continue to flow from the $n$ side to the $p$ side, but exhibit no tendency to go beyond $x=x_{2}$ because of the lack of a gradient. A similar situation exists for holes, implying that the charge carriers do not flow deep into the $p$ and $n$ sides and hence no net current results! Thus, the minority carrier concentrations must vary as shown in Fig. 2.29(b) so that diffusion can occur.

This observation reminds us of Example 2.10 and the question raised in conjunction with it: if the minority carrier concentration falls with $x$, what happens to the carriers and how can the current remain constant along the $x$-axis? Interestingly, as the electrons enter
image_name:Figure 2.29
description:The diagram in Figure 2.29 illustrates the carrier concentration profiles in a forward-biased p-n junction. It consists of two parts, showing (a) constant and (b) variable majority carrier profiles outside the depletion region. The graph is a spatial profile of carrier concentrations along the x-axis, which is labeled as 'x'. The vertical axis represents the carrier concentrations, though it is not explicitly labeled with units.

In the diagram, the n-side and p-side of the junction are clearly marked. The graph shows two distinct curves representing the concentrations of electrons and holes. On the n-side, the electron concentration is labeled as \( n_{n,f} \), and the hole concentration is \( p_{n,f} \). Similarly, on the p-side, the hole concentration is \( p_{p,f} \), and the electron concentration is \( n_{p,f} \).

The graph shows a significant change in carrier concentration across the depletion region, which is marked between \( x_1 \) and \( x_2 \). The concentration of electrons decreases as they move from the n-side to the p-side, and the hole concentration decreases as they move from the p-side to the n-side, indicating recombination of carriers in the depletion region.

Arrows labeled 'Electron Flow' and 'Hole Flow' indicate the direction of movement for electrons and holes, respectively. The diagram also shows a forward bias voltage \( V_F \), which is applied across the p-n junction, enhancing the carrier flow across the junction. The voltage is depicted with a battery symbol, indicating the direction of positive and negative terminals.

Overall, the diagram provides a visual representation of how the majority and minority carrier concentrations vary across a p-n junction under forward bias, supporting the explanation of diffusion and recombination processes in the text.

(a)
image_name:Figure 2.29
description:
[
name: VF, type: VoltageSource, value: VF, ports: {Np: VFP, Nn: VFn}
]
extrainfo:The diagram illustrates the forward bias condition of a p-n junction. It shows the electron flow from the n-side to the p-side and the hole flow from the p-side to the n-side. The majority and minority carrier concentrations vary across the junction, with recombination occurring near the depletion region. The voltage source VF is applied across the junction to enhance carrier flow.

(b)

Figure 2.29 (a) Constant and (b) variable majority carrier profiles outside the depletion region.
the $p$ side and roll down the gradient, they gradually recombine with the holes, which are abundant in this region. Similarly, the holes entering the $n$ side recombine with the electrons. Thus, in the immediate vicinity of the depletion region, the current consists of mostly minority carriers, but towards the far contacts, it is primarily comprised of majority carriers (Fig. 2.30). At each point along the $x$-axis, the two components add up to $I_{t o t}$.
image_name:Figure 2.30 Minority and majority carrier currents
description:The diagram labeled "Figure 2.30 Minority and Majority Carrier Currents" depicts a semiconductor junction, specifically a p-n junction, illustrating the flow of minority and majority carrier currents. The key components and flow are described as follows:

1. **Main Components:**
- **n-region:** This area is on the left side of the junction and is characterized by an abundance of electrons (negative charge carriers).
- **p-region:** This area is on the right side of the junction and is characterized by an abundance of holes (positive charge carriers).
- **Depletion Region:** Located at the center between the n and p regions, indicated by a dashed line, where there is a lack of mobile charge carriers.
- **Voltage Sources:** Denoted as \(V_{Fn}\) and \(V_{Fp}\) at the n and p sides respectively, indicating the potential difference across the junction.
- **External Voltage Source (\(V_F\)):** Applied across the junction, influencing the carrier movement.

2. **Flow of Information or Control:**
- **Carrier Movement:**
- In the n-region, electrons are shown moving towards the p-region, represented by an arrow pointing right.
- In the p-region, holes are shown moving towards the n-region, represented by an arrow pointing left.
- **Current Flow:**
- The arrows within the n and p regions indicate the movement of minority carriers (holes in the n-region and electrons in the p-region) towards the junction, while the movement of majority carriers (electrons in the n-region and holes in the p-region) is towards the external contacts.
- **Direction of Current (x-axis):** The overall current flow is indicated by an arrow along the x-axis, showing the direction from the n-region to the p-region.

3. **Labels, Annotations, and Key Indicators:**
- The diagram is annotated with symbols indicating the type of carriers in each region ("-" for electrons and "+" for holes).
- The potential differences \(V_{Fn}\) and \(V_{Fp}\) are labeled at the respective contacts, indicating the forward bias condition.

4. **Overall System Function:**
- The primary function of the system is to illustrate the behavior of a p-n junction under forward bias conditions, where the external voltage \(V_F\) reduces the potential barrier, allowing increased diffusion of carriers across the junction. This results in a net current flow due to the movement of both minority and majority carriers, with the majority carriers contributing to the main current at the contacts.

Figure 2.30 Minority and majority carrier currents.

### 2.2.4 I/V Characteristics

Let us summarize our thoughts thus far. In forward bias, the external voltage opposes the built-in potential, raising the diffusion currents substantially. In reverse bias, on the other hand, the applied voltage enhances the field, prohibiting current flow. We hereafter write the junction equation as:

$$
\begin{equation*}
I_{D}=I_{S}\left(\exp \frac{V_{D}}{V_{T}}-1\right) \tag{2.101}
\end{equation*}
$$

where $I_{D}$ and $V_{D}$ denote the diode current and voltage, respectively. As expected, $V_{D}=0$ yields $I_{D}=0$. (Why is this expected?) As $V_{D}$ becomes positive and exceeds several $V_{T}$, the exponential term grows rapidly and $I_{D} \approx I_{S} \exp \left(V_{D} / V_{T}\right)$. We hereafter assume $\exp \left(V_{D} / V_{T}\right) \gg 1$ in the forward bias region.
image_name:Figure 2.31
description:The graph in Figure 2.31 represents the current-voltage (I/V) characteristic of a pn junction diode. It is a two-dimensional plot with the horizontal axis labeled as $V_D$, representing the diode voltage, and the vertical axis labeled as $I_D$, representing the diode current. The units for both axes are typically volts for $V_D$ and amperes for $I_D$, although specific units are not indicated on the graph.

Type of Graph and Function:
This is an exponential graph depicting the relationship between the diode current ($I_D$) and diode voltage ($V_D$) for a pn junction.

Axes Labels and Units:
- **Horizontal Axis ($V_D$):** Represents the diode voltage.
- **Vertical Axis ($I_D$):** Represents the diode current.

Overall Behavior and Trends:
- **Forward Bias Region:** When $V_D$ is positive, the graph shows an exponential increase in $I_D$. This is indicated by the curve rising steeply as $V_D$ becomes significantly larger than zero.
- **Reverse Bias Region:** For negative $V_D$, the current $I_D$ remains approximately constant at $-I_S$, illustrating the reverse saturation current. The graph is almost flat in this region, indicating very little change in current despite changes in voltage.

Key Features and Technical Details:
- **Forward Bias Behavior:** As $V_D$ increases, $I_D$ approximates $I_S \exp(V_D / V_T)$, indicating a rapid increase in current due to the exponential term.
- **Reverse Bias Behavior:** For negative $V_D$, $I_D$ is approximately $-I_S$, which is the reverse saturation current.

Annotations and Specific Data Points:
- The graph is divided into two main regions: "Reverse Bias" on the left and "Forward Bias" on the right.
- The point where $V_D = 0$ corresponds to $I_D = 0$.
- The annotation "\approx I_S \exp(V_D / V_T)" is shown in the forward bias region, highlighting the exponential growth of current.
- The line at $-I_S$ in the reverse bias region indicates the constant current level in reverse bias.

Overall, the graph effectively illustrates the diode's behavior in both forward and reverse bias, emphasizing the exponential increase in current in forward bias and the nearly constant reverse saturation current in reverse bias.

Figure 2.31 I/V characteristic of a pn junction.

It can be proved that Eq. (2.101) also holds in reverse bias, i.e., for negative $V_{D}$. If $V_{D}<0$ and $\left|V_{D}\right|$ reaches several $V_{T}$, then $\exp \left(V_{D} / V_{T}\right) \ll 1$ and

$$
\begin{equation*}
I_{D} \approx-I_{S} \tag{2.102}
\end{equation*}
$$

Figure 2.31 plots the overall I/V characteristic of the junction, revealing why $I_{S}$ is called the "reverse saturation current." Example 2.17 indicates that $I_{S}$ is typically very small. We therefore view the current under reverse bias as "leakage." Note that $I_{S}$ and hence the junction current are proportional to the device cross section area [Eq. (2.99)]. For example, two identical devices placed in parallel (Fig. 2.32) behave as a single junction with twice the $I_{S}$.
image_name:Figure 2.32 Equivalence of parallel devices to a larger device
description:The image illustrates the equivalence of two parallel semiconductor devices to a single larger device. On the left side, there are two identical semiconductor junctions placed in parallel. Each junction consists of an n-type and a p-type region, marked with 'n' and 'p', respectively. These regions are arranged horizontally, with the n-type on the left and the p-type on the right.

The parallel configuration is indicated by the connections at both ends of the junctions, where the anodes (labeled 'A') are connected together, and the cathodes are connected to a common point. This setup is powered by a voltage source labeled 'V_F', with the positive terminal connected to the p-type regions and the negative terminal connected to the n-type regions.

On the right side of the image, the two parallel junctions are represented as a single larger junction. This larger junction has a width labeled '2A', indicating that the effective cross-sectional area is doubled when the two devices are combined in parallel. The larger device also consists of n-type and p-type regions, similar to the individual devices but with a doubled area, signifying the equivalence in terms of current handling capability.

The diagram visually demonstrates how two smaller devices in parallel can be considered equivalent to a single larger device with twice the cross-sectional area, thereby doubling the reverse saturation current 'I_S' and enhancing the current handling capacity.

Figure 2.32 Equivalence of parallel devices to a larger device.

Example Each junction in Fig. 2.32 employs the doping levels described in Example 2.13. Deter2.18 mine the forward bias current of the composite device for $V_{D}=300 \mathrm{mV}$ and 800 mV at $T=300 \mathrm{~K}$.

Solution From Example 2.17, $I_{S}=1.77 \times 10^{-17} \mathrm{~A}$ for each junction. Thus, the total current is equal to

$$
\begin{align*}
I_{D, t o t}\left(V_{D}=300 \mathrm{mV}\right) & =2 I_{S}\left(\exp \frac{V_{D}}{V_{T}}-1\right)  \tag{2.103}\\
& =3.63 \mathrm{pA} \tag{2.104}
\end{align*}
$$

Similarly, for $V_{D}=800 \mathrm{mV}$ :

$$
\begin{equation*}
I_{D, t o t}\left(V_{D}=800 \mathrm{mV}\right)=82 \mu \mathrm{~A} \tag{2.105}
\end{equation*}
$$

Exercise How many of these diodes must be placed in parallel to obtain a current of $100 \mu \mathrm{~A}$ with a voltage of 750 mV ?

Example A diode operates in the forward bias region with a typical current level [i.e., 2.19 $\left.I_{D} \approx I_{S} \exp \left(V_{D} / V_{T}\right)\right]$. Suppose we wish to increase the current by a factor of 10 . How much change in $V_{D}$ is required?

Solution Let us first express the diode voltage as a function of its current:

$$
\begin{equation*}
V_{D}=V_{T} \ln \frac{I_{D}}{I_{S}} \tag{2.106}
\end{equation*}
$$

We define $I_{1}=10 I_{D}$ and seek the corresponding voltage, $V_{D 1}$ :

$$
\begin{align*}
V_{D 1} & =V_{T} \ln \frac{10 I_{D}}{I_{S}}  \tag{2.107}\\
& =V_{T} \ln \frac{I_{D}}{I_{S}}+V_{T} \ln 10  \tag{2.108}\\
& =V_{D}+V_{T} \ln 10 \tag{2.109}
\end{align*}
$$

Thus, the diode voltage must rise by $V_{T} \ln 10 \approx 60 \mathrm{mV}$ (at $T=300 \mathrm{~K}$ ) to accommodate a tenfold increase in the current. We say the device exhibits a $60-\mathrm{mV} /$ decade characteristic, meaning $V_{D}$ changes by 60 mV for a decade (tenfold) change in $I_{D}$. More generally, an $n$-fold change in $I_{D}$ translates to a change of $V_{T} \ln n$ in $V_{D}$.

Exercise By what factor does the current change if the voltages changes by 120 mV ?

The cross section area of a diode operating in the forward bias region is increased by a 2.20 factor of 10. (a) Determine the change in $I_{D}$ if $V_{D}$ is maintained constant. (b) Determine the change in $V_{D}$ if $I_{D}$ is maintained constant. Assume $I_{D} \approx I_{S} \exp \left(V_{D} / V_{T}\right)$.

Solution (a) Since $I_{S} \propto A$, the new current is given by

$$
\begin{align*}
I_{D 1} & =10 I_{S} \exp \frac{V_{D}}{V_{T}}  \tag{2.110}\\
& =10 I_{D} \tag{2.111}
\end{align*}
$$

(b) From the above example,

$$
\begin{align*}
V_{D 1} & =V_{T} \ln \frac{I_{D}}{10 I_{S}}  \tag{2.112}\\
& =V_{T} \ln \frac{I_{D}}{I_{S}}-V_{T} \ln 10 . \tag{2.113}
\end{align*}
$$

Thus, a tenfold increase in the device area lowers the voltage by 60 mV if $I_{D}$ remains constant.

Exercise A diode in forward bias with $I_{D} \approx I_{S} \exp \left(V_{D} / V_{T}\right)$ undergoes two simultaneous changes: the current is raised by a factor of $m$ and the area is increased by a factor of $n$. Determine the change in the device voltage.

Constant-Voltage Model The exponential I/V characteristic of the diode results in nonlinear equations, making the analysis of circuits quite difficult. Fortunately, the above examples imply that the diode voltage is a relatively weak function of the device current and cross section area. With typical current levels and areas, $V_{D}$ falls in the range of $700-800 \mathrm{mV}$. For this reason, we often approximate the forward bias voltage by a constant value of 800 mV (like an ideal battery), considering the device fully off if $V_{D}<800 \mathrm{mV}$. The resulting characteristic is illustrated in Fig. 2.33(a) with the turn-on voltage denoted by $V_{D, o n}$. Note that the current goes to infinity as $V_{D}$ tends to exceed $V_{D, \text { on }}$ because we assume the forwardbiased diode operates as an ideal voltage source. Neglecting the leakage current in reverse bias, we derive the circuit model shown in Fig. 2.33(b). We say the junction operates as an open circuit if $V_{D}<V_{D, \text { on }}$ and as a constant voltage source if we attempt to increase $V_{D}$ beyond $V_{D, o n}$. While not essential, the voltage source placed in series with the switch in the off condition helps simplify the analysis of circuits: we can say that in the transition from off to on, only the switch turns on and the battery always resides in series with the switch.

A number of questions may cross the reader's mind at this point. First, why do we subject the diode to such a seemingly inaccurate approximation? Second, if we indeed intend to use this simple approximation, why did we study the physics of semiconductors and $p n$ junctions in such detail?

The developments in this chapter are representative of our treatment of all semiconductor devices: we carefully analyze the structure and physics of the device to understand its operation; we construct a "physics-based" circuit model; and we seek to approximate
image_name:(a)
description:The graph labeled '(a)' is a voltage-current characteristic graph for a diode using the constant-voltage model.

1. **Type of Graph and Function:**
- This is an I-V (current-voltage) characteristic graph for a diode.

2. **Axes Labels and Units:**
- The horizontal axis represents the diode voltage \( V_D \) with a specific point labeled as \( V_{D,on} \), which is the turn-on voltage.
- The vertical axis represents the diode current \( I_D \).
- Both axes are likely in linear scale, although units are not explicitly provided.

3. **Overall Behavior and Trends:**
- The graph shows that the diode current \( I_D \) remains at zero until the diode voltage \( V_D \) reaches \( V_{D,on} \).
- At \( V_{D,on} \), the current \( I_D \) abruptly increases, indicating the diode turns on and conducts current.
- This behavior represents the idealized constant-voltage model of a diode, where the diode behaves as a perfect switch.

4. **Key Features and Technical Details:**
- The graph features a sharp vertical rise at \( V_{D,on} \), representing the diode's turn-on threshold.
- There is no gradual slope; the transition from non-conducting to conducting is instantaneous in this model.

5. **Annotations and Specific Data Points:**
- The specific voltage \( V_{D,on} \) is a critical point, marking the transition from off to on state.
- No additional annotations or specific numerical values are provided, aside from the indication of \( V_{D,on} \).
image_name:(b)
description:
[
name: Reverse Bias Diode, type: Diode, ports: {Na: , Nc:}
name: Forward Bias Diode, type: Diode, ports: {Na: , Nc:}
]
extrainfo:The diagram illustrates the constant-voltage diode model for reverse and forward bias conditions. In reverse bias, the diode behaves like an open circuit until breakdown. In forward bias, the diode conducts with a voltage drop of V_D,on.

Figure 2.33 Constant-voltage diode model.
the resulting model, thus arriving at progressively simpler representations. Device models having different levels of complexity (and, inevitably, different levels of accuracy) prove essential to the analysis and design of circuits. Simple models allow a quick, intuitive understanding of the operation of a complex circuit, while more accurate models reveal the true performance.

Example Consider the circuit of Fig. 2.34. Calculate $I_{X}$ for $V_{X}=3 \mathrm{~V}$ and $V_{X}=1 \mathrm{~V}$ using 2.21 (a) an exponential model with $I_{S}=10^{-16} \mathrm{~A}$ and (b) a constant-voltage model with $V_{D, \text { on }}=800 \mathrm{mV}$.

Figure 2.34 Simple circuit using a diode.

Solution (a) Noting that $I_{D}=I_{X}$, we have

$$
\begin{align*}
V_{X} & =I_{X} R_{1}+V_{D}  \tag{2.114}\\
V_{D} & =V_{T} \ln \frac{I_{X}}{I_{S}} \tag{2.115}
\end{align*}
$$

This equation must be solved by iteration: we guess a value for $V_{D}$, compute the corresponding $I_{X}$ from $I_{X} R_{1}=V_{X}-V_{D}$, determine the new value of $V_{D}$ from $V_{D}=V_{T} \ln \left(I_{X} / I_{S}\right)$ and iterate. Let us guess $V_{D}=750 \mathrm{mV}$ and hence

$$
\begin{align*}
I_{X} & =\frac{V_{X}-V_{D}}{R_{1}}  \tag{2.116}\\
& =\frac{3 \mathrm{~V}-0.75 \mathrm{~V}}{1 \mathrm{k} \Omega}  \tag{2.117}\\
& =2.25 \mathrm{~mA} \tag{2.118}
\end{align*}
$$

Thus,

$$
\begin{align*}
V_{D} & =V_{T} \ln \frac{I_{X}}{I_{S}}  \tag{2.119}\\
& =799 \mathrm{mV} \tag{2.120}
\end{align*}
$$

With this new value of $V_{D}$, we can obtain a more accurate value for $I_{X}$ :

$$
\begin{align*}
I_{X} & =\frac{3 \mathrm{~V}-0.799 \mathrm{~V}}{1 \mathrm{k} \Omega}  \tag{2.121}\\
& =2.201 \mathrm{~mA} \tag{2.122}
\end{align*}
$$

We note that the value of $I_{X}$ rapidly converges. Following the same procedure for $V_{X}=1 \mathrm{~V}$, we have

$$
\begin{align*}
I_{X} & =\frac{1 \mathrm{~V}-0.75 \mathrm{~V}}{1 \mathrm{k} \Omega}  \tag{2.123}\\
& =0.25 \mathrm{~mA} \tag{2.124}
\end{align*}
$$

which yields $V_{D}=0.742 \mathrm{~V}$ and hence $I_{X}=0.258 \mathrm{~mA}$. (b) A constant-voltage model readily gives

$$
\begin{align*}
& I_{X}=2.2 \mathrm{~mA} \text { for } V_{X}=3 \mathrm{~V}  \tag{2.125}\\
& I_{X}=0.2 \mathrm{~mA} \text { for } V_{X}=1 \mathrm{~V} . \tag{2.126}
\end{align*}
$$

The value of $I_{X}$ incurs some error, but it is obtained with much less computational effort than that in part (a).

Repeat the above example if the cross section area of the diode is increased by a factor of 10 .

## 2.3 REVERSE BREAKDOWN*

Recall from Fig. 2.31 that the $p n$ junction carries only a small, relatively constant current in reverse bias. However, as the reverse voltage across the device increases, eventually "breakdown" occurs and a sudden, enormous current is observed. Figure 2.35 plots the device I/V characteristic, displaying this effect.
image_name:Figure 2.35 Reverse breakdown characteristic
description:The graph in Figure 2.35 illustrates the reverse breakdown characteristic of a diode. It is an I-V (current-voltage) characteristic curve, where the x-axis represents the diode voltage (V_D) and the y-axis represents the diode current (I_D). Both axes are typically in linear scale.

The graph shows the behavior of the diode under reverse bias conditions. Initially, as the reverse voltage (V_D) increases, the diode carries only a small, relatively constant reverse current, indicating a high resistance in the reverse direction. This is represented by a nearly horizontal line close to the x-axis.

At a certain point, labeled as V_BD (breakdown voltage), a sharp increase in current is observed despite further increases in voltage. This point marks the onset of breakdown, where the diode transitions from high resistance to low resistance, allowing a large current to flow. This sudden rise in current is depicted by a steep upward curve beyond the breakdown voltage.

The graph effectively demonstrates the diode's transition from blocking reverse current to conducting a large current once the breakdown voltage is reached, illustrating the breakdown phenomenon characteristic of a p-n junction diode.

Figure 2.35 Reverse breakdown characteristic.

The breakdown resulting from a high voltage (and hence a high electric field) can occur in any material. A common example is lightning, in which case the electric field in the air reaches such a high level as to ionize the oxygen molecules, thus lowering the resistance of the air and creating a tremendous current.

The breakdown phenomenon in $p n$ junctions occurs by one of two possible mechanisms: "Zener effect" and "avalanche effect."

[^11]
### 2.3.1 Zener Breakdown

The depletion region in a pn junction contains atoms that have lost an electron or a hole and, therefore, provide no loosely-connected carriers. However, a high electric field in this region may impart enough energy to the remaining covalent electrons to tear them from their bonds [Fig. 2.36(a)]. Once freed, the electrons are accelerated by the field and swept to the $n$ side of the junction. This effect occurs at a field strength of about $10^{6} \mathrm{~V} / \mathrm{cm}(1 \mathrm{~V} / \mu \mathrm{m})$.
image_name:(a)
description:
[
name: VR, type: VoltageSource, value: VR, ports: {Np: p, Nn: n}
]
extrainfo:The diagram illustrates the Zener effect in a pn junction under high electric field conditions, leading to electron release and acceleration towards the n side. This is depicted in image (a).
image_name:(b)
description:
[
name: VR, type: VoltageSource, value: VR, ports: {Np: n, Nn: p}
]
extrainfo:The diagram illustrates the avalanche effect in a pn junction under reverse bias. Electrons are accelerated by the electric field, causing impact ionization and creating additional electron-hole pairs, leading to a chain reaction.

Figure 2.36 (a) Release of electrons due to high electric field, (b) avalanche effect.
In order to create such high fields with reasonable voltages, a narrow depletion region is required, which from Eq. (2.76) translates to high doping levels on both sides of the junction (why?). Called the "Zener effect," this type of breakdown appears for reverse bias voltages on the order of 3-8 V.

### 2.3.2 Avalanche Breakdown

Junctions with moderate or low doping levels ( $<10^{15} \mathrm{~cm}^{3}$ ) generally exhibit no Zener breakdown. But, as the reverse bias voltage across such devices increases, an avalanche effect takes place. Even though the leakage current is very small, each carrier entering the depletion region experiences a very high electric field and hence a large acceleration, thus gaining enough energy to break the electrons from their covalent bonds. Called "impact ionization," this phenomenon can lead to avalanche: each electron freed by the impact may itself speed up so much in the field as to collide with another atom with sufficient energy, thereby freeing one more covalent-bond electron. Now, these two electrons may again acquire energy and cause more ionizing collisions, rapidly raising the number of free carriers.

An interesting contrast between Zener and avalanche phenomena is that they display opposite temperature coefficients (TCs): $V_{B D}$ has a negative TC for Zener effect and positive TC for avalanche effect. The two TCs cancel each other for $V_{B D} \approx 3.5 \mathrm{~V}$. For this reason, Zener diodes with $3.5-\mathrm{V}$ rating find application in some voltage regulators.

The Zener and avalanche breakdown effects do not damage the diodes if the resulting current remains below a certain limit given by the doping levels and the geometry of the junction. Both the breakdown voltage and the maximum allowable reverse current are specified by diode manufacturers.

## 2.4 CHAPTER SUMMARY

- Silicon contains four atoms in its last orbital. It also contains a small number of free electrons at room temperature.
- When an electron is freed from a covalent bond, a "hole" is left behind.
- The bandgap energy is the minimum energy required to dislodge an electron from its covalent bond.
- To increase the number of free carriers, semiconductors are "doped" with certain impurities. For example, addition of phosphorus to silicon increases the number of free electrons because phosphorus contains five electrons in its last orbital.
- For doped or undoped semiconductors, $n p=n_{i}^{2}$. For example, in an $n$-type material, $n \approx N_{D}$ and hence $p \approx n_{i}^{2} / N_{D}$.
- Charge carriers move in semiconductors via two mechanisms: drift and diffusion.
- The drift current density is proportional to the electric field and the mobility of the carriers and is given by $J_{t o t}=q\left(\mu_{n} n+\mu_{p} p\right) E$.
- The diffusion current density is proportional to the gradient of the carrier concentration and given by $J_{t o t}=q\left(D_{n} d n / d x-D_{p} d p / d x\right)$.
- A $p n$ junction is a piece of semiconductor that receives $n$-type doping in one section and $p$-type doping in an adjacent section.
- The $p n$ junction can be considered in three modes: equilibrium, reverse bias, and forward bias.
- Upon formation of the pn junction, sharp gradients of carrier densities across the junction result in a high current of electrons and holes. As the carriers cross, they leave ionized atoms behind, and a "depletion region" is formed. The electric field created in the depletion region eventually stops the current flow. This condition is called equilibrium.
- The electric field in the depletion results in a built-in potential across the region equal to $(k T / q) \ln \left(N_{A} N_{D}\right) / n_{i}^{2}$, typically in the range of 700 to 800 mV .
- Under reverse bias, the junction carries negligible current and operates as a capacitor. The capacitance itself is a function of the voltage applied across the device.
- Under forward bias, the junction carries a current that is an exponential function of the applied voltage: $I_{S}\left[\exp \left(V_{F} / V_{T}\right)-1\right]$.
- Since the exponential model often makes the analysis of circuits difficult, a constantvoltage model may be used in some cases to estimate the circuit's response with less mathematical labor.
- Under a high reverse bias voltage, pn junctions break down, conducting a very high current. Depending on the structure and doping levels of the device, "Zener" or "avalanche" breakdown may occur.
