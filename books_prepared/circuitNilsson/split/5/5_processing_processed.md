# 5. The Operational Amplifier

The electronic circuit known as an operational amplifier has

become increasingly important. However, a detailed analysis of this circuit requires an understanding of electronic devices such as diodes and transistors. You may wonder, then, why we are introducing the circuit before discussing the circuit's electronic components. There are several reasons. First, you can develop an appreciation for how the operational amplifier can be used as a circuit building block by focusing on its terminal behavior. At an introductory level, you need not fully understand the operation of the electronic components that govern terminal behavior. Second, the circuit model of the operational amplifier requires the use of a dependent source. Thus you have a chance to use this type of source in a practical circuit rather than as an abstract circuit component. Third, you can combine the operational amplifier with resistors to perform some very useful functions, such as scaling, summing, sign changing, and subtracting. Finally, after introducing inductors and capacitors in Chapter 6, we can show you how to use the operational amplifier to design integrating and differentiating circuits.

Our focus on the terminal behavior of the operational amplifier implies taking a black box approach to its operation; that is, we are not interested in the internal structure of the amplifier nor in the currents and voltages that exist in this structure. The important thing to remember is that the internal behavior of the amplifier accounts for the voltage and current constraints imposed at the terminals. (For now, we ask that you accept these constraints on faith.)

Practical Perspective

Strain Gages

How could you measure the amount of bending in a metal bar such as the one shown in the figure without physically contacting the bar? One method would be to use a strain gage. A strain gage is a type of transducer. A transducer is a device that measures a quantity by converting it into a more convenient form. The quantity we wish to measure in the metal bar is the bending angle, but measuring the angle directly is quite difficult and could even be dangerous. Instead, we attach a strain gage (shown in the line drawing here) to the metal bar. A strain gage is a grid of thin wires whose resistance changes when the wires are lengthened or shortened:

$$
\Delta R=2 R \frac{\Delta L}{L}
$$

where $R$ is the resistance of the gage at rest, $\Delta L / L$ is the fractional lengthening of the gage (which is the definition of "strain"), the constant 2 is typical of the manufacturer's gage factor, and $\Delta R$ is the change in resistance due to the bending of the bar. Typically, pairs of strain gages are attached to opposite sides of a bar. When the bar is bent, the wires in one pair of gages get longer and thinner, increasing the resistance, while the wires in the other pair of gages get shorter and thicker, decreasing the resistance.

But how can the change in resistance be measured? One way would be to use an ohmmeter. However, the change in resistance experienced by the strain gage is typically much smaller than could be accurately measured by an ohmmeter. Usually the pairs of strain gages are connected to form a Wheatstone bridge, and the voltage difference between two legs of the bridge is measured. In order to make an accurate
measurement of the voltage difference, we use an operational amplifier circuit to amplify, or increase, the voltage difference. After we introduce the operational amplifier and some of the important circuits that employ these devices, we will present the circuit used together with the strain gages for measuring the amount of bending in a metal bar.

The operational amplifier circuit first came into existence as a basic building block in analog computers. It was referred to as operational because it was used to implement the mathematical operations of integration, differentiation, addition, sign changing, and scaling. In recent years, the range of application has broadened beyond implementing mathematical operations; however, the original name for the circuit persists. Engineers and technicians have a penchant for creating technical jargon; hence the operational amplifier is widely known as the op amp.
image_name:Figure 5.1
description:The image depicts a graphical representation of a cylindrical object, likely a cable or a pipe, with an overlay of flexible, layered sheets. These sheets appear to be made of a material that can bend or flex along with the cylinder. The cylinder is shown in black, suggesting it might be an insulated wire or a conduit.

1. **Identification of Components and Structure:**
- **Cylinder:** A long, black cylindrical object is central to the image. It appears to be solid and consistent in diameter, possibly representing a wire or pipe.
- **Flexible Sheets:** There are multiple layered sheets shown in a light blue color. These sheets are aligned along the length of the cylinder and seem to be able to move or flex.

2. **Connections and Interactions:**
- The sheets are depicted as being able to bend along with the cylinder, suggesting that they are either attached to it or designed to move in tandem with its curvature.
- Red arrows are present, indicating the directional movement or flexibility of the sheets as the cylinder bends.

3. **Labels, Annotations, and Key Features:**
- **Red Arrows:** These are used to illustrate the direction of movement or the flexibility of the sheets. They emphasize that the sheets can conform to the shape of the cylinder as it bends.
- There are no specific labels or annotations on the image, but the visual elements suggest a focus on flexibility and adaptability of the materials involved.

image_name:Ron Chapple/Corbis
description:The image depicts a portion of an electrical substation silhouetted against a sunset or sunrise sky. The substation is composed of several key components:

1. **Identification of Components and Structure:**
- **High Voltage Transmission Lines:** Visible at the top of the image, these lines are supported by tall metal lattice structures. The lines are part of the power distribution network, carrying electricity across different regions.
- **Insulators:** These are mounted on the metal structures, appearing as stacked discs or cylinders. They are crucial for preventing electrical current from grounding through the supporting structures.
- **Metal Framework:** The substation structures are made of metal, forming a complex framework that supports the electrical equipment and transmission lines.

2. **Connections and Interactions:**
- The high voltage lines are interconnected through the metal framework, allowing for the distribution and regulation of electrical power. The insulators ensure that the lines do not conduct electricity to the metal supports, maintaining safety and efficiency.
- There are no visible control or feedback loops in this image, but the substation likely contains internal control systems for managing power flow.

3. **Labels, Annotations, and Key Features:**
- The image lacks specific labels or annotations. However, the silhouetted view emphasizes the structural complexity and the importance of insulators in the electrical grid.
- The setting sun or rising sun in the background adds a dramatic effect, highlighting the silhouette of the substation against the sky.

Overall, the image captures the essential features of an electrical substation, focusing on the transmission lines, insulators, and supporting metal structures, all set against a scenic backdrop.


Ron Chapple/Corbis
image_name:Figure 5.1
description:The image labeled "Figure 5.1" depicts an eight-lead Dual In-line Package (DIP) from a top view perspective. This package is commonly used for integrated circuits. The diagram highlights the arrangement and labeling of the pins, which are crucial for understanding the connections and functionalities of the device.

1. **Identification of Components and Structure:**
- The DIP package is shown as a rectangular block with eight metal leads extending from its sides. These leads are used for electrical connections to the circuit board.
- The leads are numbered from 1 to 8, starting from the top left and continuing counterclockwise.

2. **Connections and Interactions:**
- Each lead is labeled with its specific function:
- Pin 1: Offset null
- Pin 2: Inverting input
- Pin 3: Noninverting input
- Pin 4: V- (negative power supply)
- Pin 5: Offset null
- Pin 6: Output
- Pin 7: V+ (positive power supply)
- Pin 8: NC (No Connection)
- The inverting and noninverting inputs are used for signal input to the operational amplifier. The output pin provides the amplified signal.
- Offset null pins are used to adjust the offset voltage of the operational amplifier to zero.
- The V+ and V- pins are for connecting the positive and negative power supplies, respectively.

3. **Labels, Annotations, and Key Features:**
- The diagram clearly labels each pin with its function, aiding in the identification and connection of the operational amplifier within a circuit.
- The depiction emphasizes the importance of each pin's role in the operation of the device, particularly in ensuring the correct power supply and signal processing.


Figure 5.1 $\triangle$ The eight-lead DIP package (top view).
image_name:Figure 5.2 - The circuit symbol for an operational amplifier (op amp)
description:
[
'name': 'OpAmp1', 'type': 'OpAmp', 'value': 'OpAmp1', 'ports': {'InP': 'Noninverting input', 'InN': 'Inverting input', 'OutP': 'Output', 'Vdd': 'Positive power supply', '-Vdd': 'Negative power supply'
]
extrainfo:The diagram shows a typical operational amplifier symbol with labeled inputs and power supply connections. The noninverting input is labeled with a plus sign, and the inverting input with a minus sign. The op amp has connections for a positive and negative power supply, as well as an output.


Figure 5.2 - The circuit symbol for an operational amplifier (op amp).
image_name:Figure 5.3
description:
[
'name': 'OpAmp', 'type': 'OpAmp', 'ports': {'InP': 'N1', 'InN': 'N2', 'OutP': 'N3', 'OutN': 'N4', 'Vdd': 'V+', '-Vdd': 'V-'
]
extrainfo:The diagram shows a typical operational amplifier symbol with labeled inputs and power supply connections. The noninverting input is labeled with a plus sign, and the inverting input with a minus sign. The op amp has connections for a positive and negative power supply, as well as an output.


Figure 5.3 A A simplified circuit symbol for an op amp.
image_name:Figure 5.4
description:
[
'name': 'Ao', 'type': 'OpAmp', 'value': 'Ao', 'ports': {'InP': 'Vp', 'InN': 'Vn', 'OutP': 'Vo',  'Vdd': 'V+', '-Vdd': 'V-'
'name': 'VCC1', 'type': 'VoltageSource', 'value': 'VCC', 'ports': {'Np': 'V+', 'Nn': 'GND'
'name': 'VCC2', 'type': 'VoltageSource', 'value': 'VCC', 'ports': {'Np': 'GND', 'Nn': 'V-'
]
extrainfo:The circuit diagram represents an operational amplifier with positive and negative power supply connections. The op amp has noninverting (Vp) and inverting (Vn) inputs, and an output (Vo). It is powered by a positive voltage source (V+) and a negative voltage source (V-), both referenced to a common ground (GND). The VCC voltage source is also connected between VCC and GND.


Figure 5.4 A Terminal voltage variables.

## 5.1 Operational Amplifier Terminals

Because we are stressing the terminal behavior of the operational amplifier ( op amp), we begin by discussing the terminals on a commercially available device. In 1968, Fairchild Semiconductor introduced an op amp that has found widespread acceptance: the $\mu \mathrm{A} 741$. (The $\mu \mathrm{A}$ prefix is used by Fairchild to indicate a microcircuit fabrication of the amplifier.) This amplifier is available in several different packages. For our discussion, we assume an eight-lead DIP. ${ }^{1}$ Figure 5.1 shows a top view of the package, with the terminal designations given alongside the terminals. The terminals of primary interest are

- inverting input,
- noninverting input,
- output,
- positive power supply $\left(V^{+}\right)$,
- negative power supply $\left(V^{-}\right)$.

The remaining three terminals are of little or no concern. The offset null terminals may be used in an auxiliary circuit to compensate for a degradation in performance because of aging and imperfections. However, the degradation in most cases is negligible, so the offset terminals often are unused and play a secondary role in circuit analysis. Terminal 8 is of no interest simply because it is an unused terminal; NC stands for no connection, which means that the terminal is not connected to the amplifier circuit.

Figure 5.2 shows a widely used circuit symbol for an op amp that contains the five terminals of primary interest. Using word labels for the terminals is inconvenient in circuit diagrams, so we simplify the terminal designations in the following way. The noninverting input terminal is labeled plus $(+)$, and the inverting input terminal is labeled minus $(-)$. The power supply terminals, which are always drawn outside the triangle, are marked $V^{+}$and $V^{-}$. The terminal at the apex of the triangular box is always understood to be the output terminal. Figure 5.3 summarizes these simplified designations.

## 5.2 Terminal Voltages and Currents

We are now ready to introduce the terminal voltages and currents used to describe the behavior of the op amp. The voltage variables are measured from a common reference node. ${ }^{2}$ Figure 5.4 shows the voltage variables with their reference polarities.

All voltages are considered as voltage rises from the common node. This convention is the same as that used in the node-voltage method of analysis. A positive supply voltage $\left(V_{C C}\right)$ is connected between $V^{+}$and the common node. A negative supply voltage $\left(-V_{C C}\right)$ is connected between $V^{-}$ and the common node. The voltage between the inverting input terminal and the common node is denoted $v_{n}$. The voltage between the noninverting input terminal and the common node is designated as $v_{p}$. The voltage between the output terminal and the common node is denoted $v_{o}$.

[^0]Figure 5.5 shows the current variables with their reference directions. Note that all the current reference directions are into the terminals of the operational amplifier: $i_{n}$ is the current into the inverting input terminal; $i_{p}$ is the current into the noninverting input terminal; $i_{o}$ is the current into the output terminal $; i_{c^{+}}$is the current into the positive power supply terminal; and $i_{c^{-}}$is the current into the negative power supply terminal.

The terminal behavior of the op amp as a linear circuit element is characterized by constraints on the input voltages and the input currents. The voltage constraint is derived from the voltage transfer characteristic of the op amp integrated circuit and is pictured in Fig. 5.6.

The voltage transfer characteristic describes how the output voltage varies as a function of the input voltages; that is, how voltage is transferred from the input to the output. Note that for the op amp, the output voltage is a function of the difference between the input voltages, $v_{p}-v_{n}$. The equation for the voltage transfer characteristic is

$$
v_{o}= \begin{cases}-V_{C C} & A\left(v_{p}-v_{n}\right)<-V_{C C}  \tag{5.1}\\ A\left(v_{p}-v_{n}\right) & -V_{C C} \leq A\left(v_{p}-v_{n}\right) \leq+V_{C C} \\ +V_{C C} & A\left(v_{p}-v_{n}\right)>+V_{C C}\end{cases}
$$

We see from Fig. 5.6 and Eq. 5.1 that the op amp has three distinct regions of operation. When the magnitude of the input voltage difference $\left(\left|v_{p}-v_{n}\right|\right)$ is small, the op amp behaves as a linear device, as the output voltage is a linear function of the input voltages. Outside this linear region, the output of the op amp saturates, and the op amp behaves as a nonlinear device, because the output voltage is no longer a linear function of the input voltages. When it is operating linearly, the op amp's output voltage is equal to the difference in its input voltages times the multiplying constant, or gain, $A$.

When we confine the op amp to its linear operating region, a constraint is imposed on the input voltages, $v_{p}$ and $v_{n}$. The constraint is based on typical numerical values for $V_{C C}$ and $A$ in Eq. 5.1. For most op amps, the recommended dc power supply voltages seldom exceed 20 V , and the gain, $A$, is rarely less than 10,000 , or $10^{4}$. We see from both Fig. 5.6 and Eq. 5.1 that in the linear region, the magnitude of the input voltage difference $\left(\left|v_{p}-v_{n}\right|\right)$ must be less than $20 / 10^{4}$, or 2 mV .

Typically, node voltages in the circuits we study are much larger than 2 mV , so a voltage difference of less than 2 mV means the two voltages are essentially equal. Thus, when an op amp is constrained to its linear operating region and the node voltages are much larger than 2 mV , the constraint on the input voltages of the op amp is

$$
\begin{equation*}
v_{p}=v_{n} \tag{5.2}
\end{equation*}
$$

Note that Eq. 5.2 characterizes the relationship between the input voltages for an ideal op amp; that is, an op amp whose value of $A$ is infinite.

The input voltage constraint in Eq. 5.2 is called the virtual short condition at the input of the op amp. It is natural to ask how the virtual short is maintained at the input of the op amp when the op amp is embedded in a circuit, thus ensuring linear operation. The answer is that a signal is fed back from the output terminal to the inverting input terminal. This configuration is known as negative feedback because the
image_name:Figure 5.5 A Terminal current variables
description:
[
'name': 'A0', 'type': 'OpAmp', 'value': 'A0', 'ports': {'InP': 'InP(A0)', 'InN': 'InN(A0)', 'OutP': 'Out(A0)', 'Vdd': 'V+', '-Vdd': 'V-'
'name': 'V_CC1', 'type': 'VoltageSource', 'value': 'V_CC', 'ports': {'Np': 'V+', 'Nn': 'GND'
'name': 'V_CC2', 'type': 'VoltageSource', 'value': 'V_CC', 'ports': {'Np': 'V-', 'Nn': 'GND'
]
extrainfo:The circuit diagram shows an ideal operational amplifier with dual power supply voltages V+ and V-. The op amp is configured with negative feedback. Current symbols i_p, i_n, i_o, i_c+, and i_c- are indicated, representing different currents flowing in the circuit.


Figure 5.5 A Terminal current variables.
image_name:Figure 5.6
description:The graph in Figure 5.6 illustrates the voltage transfer characteristic of an ideal operational amplifier (op amp). It is a plot showing the relationship between the output voltage \( v_o \) on the vertical axis and the input voltage difference \((v_p - v_n)\) on the horizontal axis.

1. **Type of Graph and Function:**
- The graph is a voltage transfer characteristic curve, typically used to describe how the output voltage of an op amp changes with respect to its input voltage difference.

2. **Axes Labels and Units:**
- The vertical axis is labeled \( v_o \) and represents the output voltage, with units of volts (V).
- The horizontal axis is labeled \( (v_p - v_n) \) and represents the difference between the non-inverting and inverting input voltages, also in volts (V).
- The graph does not specify the scale, but it is typically linear for such characteristics.

3. **Overall Behavior and Trends:**
- The graph shows a linear region in the center where the output voltage \( v_o \) is directly proportional to the input voltage difference \((v_p - v_n)\). This linear region is bounded by two points: \(-V_{CC}/A\) and \(V_{CC}/A\), where \(A\) is the open-loop gain of the op amp.
- Beyond these bounds, the op amp enters saturation, where the output voltage levels off to \( V_{CC} \) for positive saturation and \(-V_{CC} \) for negative saturation.

4. **Key Features and Technical Details:**
- The linear region is where the op amp operates ideally, and the output voltage is a scaled version of the input voltage difference.
- The saturation regions indicate the limits of the op amp's output voltage, constrained by the power supply voltages \( V_{CC} \).
- The transition from the linear region to saturation is sharp, reflecting the idealized nature of the op amp.

5. **Annotations and Specific Data Points:**
- The graph is annotated with regions labeled as "Positive saturation," "Linear region," and "Negative saturation."
- Specific markers are placed at \(-V_{CC}/A\) and \(V_{CC}/A\), indicating the boundaries of the linear region.
- The output voltage levels \( V_{CC} \) and \(-V_{CC} \) are marked on the vertical axis, showing the saturation limits.


Figure 5.6 $\triangle$ The voltage transfer characteristic of an op amp.

Input voltage constraint for ideal op amp

Input current constraint for ideal op amp
signal fed back from the output subtracts from the input signal. The negative feedback causes the input voltage difference to decrease. Because the output voltage is proportional to the input voltage difference, the output voltage is also decreased, and the op amp operates in its linear region.

If a circuit containing an op amp does not provide a negative feedback path from the op amp output to the inverting input, then the op amp will normally saturate. The difference in the input signals must be extremely small to prevent saturation with no negative feedback. But even if the circuit provides a negative feedback path for the op amp, linear operation is not ensured. So how do we know whether the op amp is operating in its linear region?

The answer is, we don't! We deal with this dilemma by assuming linear operation, performing the circuit analysis, and then checking our results for contradictions. For example, suppose we assume that an op amp in a circuit is operating in its linear region, and we compute the output voltage of the op amp to be 10 V . On examining the circuit, we discover that $V_{C C}$ is 6 V , resulting in a contradiction, because the op amp's output voltage can be no larger than $V_{C C}$. Thus our assumption of linear operation was invalid, and the op amp output must be saturated at 6 V .

We have identified a constraint on the input voltages that is based on the voltage transfer characteristic of the op amp integrated circuit, the assumption that the op amp is restricted to its linear operating region and to typical values for $V_{C C}$ and $A$. Equation 5.2 represents the voltage constraint for an ideal op amp, that is, with a value of $A$ that is infinite.

We now turn our attention to the constraint on the input currents. Analysis of the op amp integrated circuit reveals that the equivalent resistance seen by the input terminals of the op amp is very large, typically $1 \mathrm{M} \Omega$ or more. Ideally, the equivalent input resistance is infinite, resulting in the current constraint

$$
\begin{equation*}
i_{p}=i_{n}=0 \tag{5.3}
\end{equation*}
$$

Note that the current constraint is not based on assuming the op amp is confined to its linear operating region as was the voltage constraint. Together, Eqs. 5.2 and 5.3 form the constraints on terminal behavior that define our ideal op amp model.

From Kirchhoff's current law we know that the sum of the currents entering the operational amplifier is zero, or

$$
\begin{equation*}
i_{p}+i_{n}+i_{o}+i_{c^{+}}+i_{c^{-}}=0 \tag{5.4}
\end{equation*}
$$

Substituting the constraint given by Eq. 5.3 into Eq. 5.4 gives

$$
\begin{equation*}
i_{o}=-\left(i_{c^{+}}+i_{c^{-}}\right) \tag{5.5}
\end{equation*}
$$

The significance of Eq. 5.5 is that, even though the current at the input terminals is negligible, there may still be appreciable current at the output terminal.

Before we start analyzing circuits containing op amps, let's further simplify the circuit symbol. When we know that the amplifier is operating within its linear region, the dc voltages $\pm V_{C C}$ do not enter into the circuit equations.

In this case, we can remove the power supply terminals from the symbol and the dc power supplies from the circuit, as shown in Fig. 5.7. A word of caution: Because the power supply terminals have been omitted, there is a danger of inferring from the symbol that $i_{p}+i_{n}+i_{o}=0$. We have already noted that such is not the case; that is, $i_{p}+i_{n}+i_{o}+i_{c^{+}}+i_{c^{-}}=0$. In other words, the ideal op amp model constraint that $i_{p}=i_{n}=0$ does not imply that $i_{o}=0$.

Note that the positive and negative power supply voltages do not have to be equal in magnitude. In the linear operating region, $v_{o}$ must lie between the two supply voltages. For example, if $V^{+}=15 \mathrm{~V}$ and $V^{-}=-10 \mathrm{~V}$, then $-10 \mathrm{~V} \leq v_{o} \leq 15 \mathrm{~V}$. Be aware also that the value of $A$ is not constant under all operating conditions. For now, however, we assume that it is. A discussion of how and why the value of $A$ can change must be delayed until after you have studied the electronic devices and components used to fabricate an amplifier.

Example 5.1 illustrates the judicious application of Eqs. 5.2 and 5.3. When we use these equations to predict the behavior of a circuit containing an op amp, in effect we are using an ideal model of the device.
image_name:Figure 5.7
description:
[
'name': 'A0', 'type': 'OpAmp', 'value': 'A0', 'ports': {'InP': 'vp', 'InN': 'vn', 'OutP': 'vo'
]
extrainfo:This is a simple op amp circuit with labeled input and output nodes. The op amp is ideal and has its power supply terminals removed for simplicity. The input nodes are labeled vp and vn, and the output node is labeled vo with the ground referenced as GND.


Figure 5.7 A The op amp symbol with the power supply terminals removed.

#### Example 5.1 Analyzing an Op Amp Circuit

The op amp in the circuit shown in Fig. 5.8 is ideal.
a) Calculate $v_{o}$ if $v_{\mathrm{a}}=1 \mathrm{~V}$ and $v_{\mathrm{b}}=0 \mathrm{~V}$.
b) Repeat (a) for $v_{\mathrm{a}}=1 \mathrm{~V}$ and $v_{\mathrm{b}}=2 \mathrm{~V}$.
c) If $v_{\mathrm{a}}=1.5 \mathrm{~V}$, specify the range of $v_{\mathrm{b}}$ that avoids amplifier saturation.
image_name:Figure 5.8
description:
[
'name': 'Va', 'type': 'VoltageSource', 'value': 'Va', 'ports': {'Np': 'va', 'Nn': 'GND'
'name': 'Vb', 'type': 'VoltageSource', 'value': 'Vb', 'ports': {'Np': 'InP(A0)', 'Nn': 'GND'
'name': '25kΩ', 'type': 'Resistor', 'value': '25kΩ', 'ports': {'N1': 'va', 'N2': 'InN(A0)'
'name': '100kΩ', 'type': 'Resistor', 'value': '100kΩ', 'ports': {'N1': 'InN(A0)', 'N2': 'Out(A0)'
'name': 'A0', 'type': 'OpAmp', 'value': 'A0', 'ports': {'InP': 'InP(A0)', 'InN': 'InN(A0)', 'OutP': 'Out(A0)','Vdd':'10V','-Vdd':'-10V'
]
extrainfo:The circuit is an ideal operational amplifier configuration with negative feedback through a 100kΩ resistor. It has two input voltage sources, Va and Vb, and the output voltage is denoted as vo. The op amp is powered by ±10V.


Figure 5.8 $\triangle$ The circuit for Example 5.1.

#### Solution

a) Because a negative feedback path exists from the op amp's output to its inverting input through the $100 \mathrm{k} \Omega$ resistor, let's assume the op amp is confined to its linear operating region. We can write a node-voltage equation at the inverting input terminal. The voltage at the inverting input terminal is 0 , as $v_{p}=v_{\mathrm{b}}=0$ from the connected voltage source, and $v_{n}=v_{p}$ from the voltage constraint Eq. 5.2. The node-voltage equation at $v_{n}$ is thus

$$
i_{25}=i_{100}=i_{n}
$$

From Ohm's law,

$$
\begin{aligned}
i_{25} & =\left(v_{\mathrm{a}}-v_{n}\right) / 25=\frac{1}{25} \mathrm{~mA} \\
i_{100} & =\left(v_{o}-v_{n}\right) / 100=v_{o} / 100 \mathrm{~mA}
\end{aligned}
$$

The current constraint requires $i_{n}=0$. Substituting the values for the three currents into the node-voltage equation, we obtain

$$
\frac{1}{25}+\frac{v_{o}}{100}=0
$$

Hence, $v_{o}$ is -4 V . Note that because $v_{o}$ lies between $\pm 10 \mathrm{~V}$, the op amp is in its linear region of operation.
b) Using the same process as in (a), we get

$$
\begin{aligned}
v_{p} & =v_{\mathrm{b}}=v_{n}=2 \mathrm{~V} \\
i_{25} & =\frac{v_{\mathrm{a}}-v_{n}}{25}=\frac{1-2}{25}=-\frac{1}{25} \mathrm{~mA} \\
i_{100} & =\frac{v_{o}-v_{n}}{100}=\frac{v_{o}-2}{100} \mathrm{~mA} \\
i_{25} & =-i_{100}
\end{aligned}
$$

Therefore, $v_{o}=6 \mathrm{~V}$. Again, $v_{o}$ lies within $\pm 10 \mathrm{~V}$.
c) As before, $v_{n}=v_{p}=v_{\mathrm{b}}$, and $i_{25}=-i_{100}$. Because $v_{\mathrm{a}}=1.5 \mathrm{~V}$,

$$
\frac{1.5-v_{\mathrm{b}}}{25}=-\frac{v_{o}-v_{\mathrm{b}}}{100}
$$

Solving for $v_{\mathrm{b}}$ as a function of $v_{o}$ gives

$$
v_{\mathrm{b}}=\frac{1}{5}\left(6+v_{o}\right)
$$

Substituting these limits on $v_{o}$ into the expression for $v_{\mathrm{b}}$, we see that $v_{\mathrm{b}}$ is limited to

$$
-0.8 \mathrm{~V} \leq v_{\mathrm{b}} \leq 3.2 \mathrm{~V}
$$

Now, if the amplifier is to be within the linear region of operation, $-10 \mathrm{~V} \leq v_{o} \leq 10 \mathrm{~V}$.

ASSESSMENT PROBLEM

Objective 1-Use voltage and current constraints in an ideal op amp
5.1 Assume that the op amp in the circuit shown is ideal.
a) Calculate $v_{o}$ for the following values of $v_{s}$ : $0.4,2.0,3.5,-0.6,-1.6$, and -2.4 V .
b) Specify the range of $v_{s}$ required to avoid amplifier saturation.

Answer: (a) $-2,-10,-15,3,8$, and 10 V ;
(b) $-2 \mathrm{~V} \leq v_{s} \leq 3 \mathrm{~V}$.
image_name:Figure
description:
[
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': 'Vs', 'Nn': 'GND'
'name': '16 kΩ', 'type': 'Resistor', 'value': '16 kΩ', 'ports': {'N1': 'Vs', 'N2': 'InN(A0)'
'name': '80 kΩ', 'type': 'Resistor', 'value': '80 kΩ', 'ports': {'N1': 'InN(A0)', 'N2': 'Out(A0)'
'name': 'A0', 'type': 'OpAmp', 'value': 'A0', 'ports': {'InP': 'GND', 'InN': 'InN(A0)', 'OutP': 'Out(A0)', 'Vdd': '10V', '-Vdd': '-15V'
]
extrainfo:The circuit is an inverting amplifier with a gain of -5, determined by the ratio of the resistors (80 kΩ / 16 kΩ). The op-amp is powered by a dual supply of +10 V and -15 V.


NOTE: Also try Chapter Problems 5.1, 5.4, and 5.5.
image_name:Figure 5.9
description:
[
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': 'us', 'Nn': 'GND'
'name': 'Rs', 'type': 'Resistor', 'value': 'Rs', 'ports': {'N1': 'Us', 'N2': 'InN(A0)'
'name': 'Rf', 'type': 'Resistor', 'value': 'Rf', 'ports': {'N1': 'InN(A0)', 'N2': 'Vo'
'name': 'A0', 'type': 'OpAmp', 'value': 'A0', 'ports': {'InP': 'GND', 'InN': 'InN(A0)', 'OutP': 'Vo', 'Vdd': 'VCC', '+Vdd': '-VCC'
]
extrainfo:The circuit is an inverting amplifier with a gain of -5, determined by the ratio of the resistors (80 kΩ / 16 kΩ). The op-amp is powered by a dual supply of +10 V and -15 V.


Figure 5.9 $\triangle$ An inverting-amplifier circuit.

## 5.3 The Inverting-Amplifier Circuit

We are now ready to discuss the operation of some important op amp circuits, using Eqs. 5.2 and 5.3 to model the behavior of the device itself. Figure 5.9 shows an inverting-amplifier circuit. We assume that the op amp is operating in its linear region. Note that, in addition to the op amp, the circuit consists of two resistors $\left(R_{f}\right.$ and $\left.R_{s}\right)$, a voltage signal source $\left(v_{s}\right)$, and a short circuit connected between the noninverting input terminal and the common node.

We now analyze this circuit, assuming an ideal op amp. The goal is to obtain an expression for the output voltage, $v_{o}$, as a function of the source voltage, $v_{s}$. We employ a single node-voltage equation at the inverting terminal of the op amp, given as

$$
\begin{equation*}
i_{s}+i_{f}=i_{n} \tag{5.6}
\end{equation*}
$$

The voltage constraint of Eq. 5.2 sets the voltage at $v_{n}=0$, because the voltage at $v_{p}=0$. Therefore,

$$
\begin{align*}
i_{s} & =\frac{v_{s}}{R_{s}}  \tag{5.7}\\
i_{f} & =\frac{v_{o}}{R_{f}} \tag{5.8}
\end{align*}
$$

Now we invoke the constraint stated in Eq. 5.3, namely,

$$
\begin{equation*}
i_{n}=0 \tag{5.9}
\end{equation*}
$$

Substituting Eqs. 5.7-5.9 into Eq. 5.6 yields the sought-after result:

$$
\begin{equation*}
v_{o}=\frac{-R_{f}}{R_{s}} v_{s} \tag{5.10}
\end{equation*}
$$

Note that the output voltage is an inverted, scaled replica of the input. The sign reversal from input to output is, of course, the reason for referring to the circuit as an inverting amplifier. The scaling factor, or gain, is the ratio $R_{f} / R_{s}$.

The result given by Eq. 5.10 is valid only if the op amp shown in the circuit in Fig. 5.9 is ideal; that is, if $A$ is infinite and the input resistance is infinite. For a practical op amp, Eq. 5.10 is an approximation, usually a good one. (We say more about this later.) Equation 5.10 is important because it tells us that if the op amp gain $A$ is large, we can specify the gain of the inverting amplifier with the external resistors $R_{f}$ and $R_{s}$. The upper limit on the gain, $R_{f} / R_{s}$, is determined by the power supply voltages and the value of the signal voltage $v_{s}$. If we assume equal power supply voltages, that is, $V^{+}=-V^{-}=V_{C C}$, we get

$$
\begin{equation*}
\left|v_{o}\right| \leq V_{C C}, \quad\left|\frac{R_{f}}{R_{s}} v_{s}\right| \leq V_{C C}, \quad \frac{R_{f}}{R_{s}} \leq\left|\frac{V_{C C}}{v_{s}}\right| \tag{5.11}
\end{equation*}
$$

For example, if $V_{C C}=15 \mathrm{~V}$ and $v_{s}=10 \mathrm{mV}$, the ratio $R_{f} / R_{s}$ must be less than 1500.

In the inverting amplifier circuit shown in Fig. 5.9, the resistor $R_{f}$ provides the negative feedback connection. That is, it connects the output terminal to the inverting input terminal. If $R_{f}$ is removed, the feedback path is opened and the amplifier is said to be operating open loop. Figure 5.10 shows the open-loop operation.

Opening the feedback path drastically changes the behavior of the circuit. First, the output voltage is now

$$
\begin{equation*}
v_{o}=-A v_{n} \tag{5.12}
\end{equation*}
$$

assuming as before that $V^{+}=-V^{-}=V_{C C}$; then $\left|v_{n}\right|<V_{C C} / A$ for linear operation. Because the inverting input current is almost zero, the voltage drop across $R_{s}$ is almost zero, and the inverting input voltage nearly equals the signal voltage, $v_{s}$; that is, $v_{n} \approx v_{s}$. Hence, the op amp can operate open loop in the linear mode only if $\left|v_{s}\right|<V_{C C} / A$. If $\left|v_{s}\right|>V_{C C} / A$, the op amp simply saturates. In particular, if $v_{s}<-V_{C C} / A$, the op amp saturates at $+V_{C C}$, and if $v_{s}>V_{C C} / A$, the op amp saturates at $-V_{C C}$. Because the relationship shown in Eq. 5.12 occurs when there is no feedback path, the value of $A$ is often called the open-loop gain of the op amp.

Example 5.2 uses the inverting-amplifier equation to design an inverting amplifier using realistic resistor values.

#### Example 5.2 Designing an Inverting Amplifier

a) Design an inverting amplifier (see Fig. 5.9) with a gain of 12 . Use $\pm 15 \mathrm{~V}$ power supplies and an ideal op amp.
b) What range of input voltages, $v_{s}$, allows the op amp in this design to remain in its linear operating region?

#### Solution

a) We need to find two resistors whose ratio is 12 from the realistic resistor values listed in

Appendix H. There are lots of different possibilities, but let's choose $R_{s}=1 \mathrm{k} \Omega$ and $R_{f}=12 \mathrm{k} \Omega$. Use the inverting-amplifier equation (Eq. 5.10) to verify the design:

$$
v_{o}=-\frac{R_{f}}{R_{s}} v_{s}=-\frac{12,000}{1000} v_{s}=-12 v_{s}
$$

Thus, we have an inverting-amplifier with a gain of 12, as shown in Fig. 5.11.
image_name:Figure 5.11
description:
[
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': 'Vs', 'Nn': 'GND'
'name': '1 kΩ', 'type': 'Resistor', 'value': '1 kΩ', 'ports': {'N1': 'Vs', 'N2': 'InN'
'name': '12 kΩ', 'type': 'Resistor', 'value': '12 kΩ', 'ports': {'N1': 'InN', 'N2': 'Vo'
'name': 'A0', 'type': 'OpAmp', 'value': 'A0', 'ports': {'InP': 'GND', 'InN': 'InN', 'OutP': 'Vo', 'Vdd':'+15V', '-Vdd':'-15V'
]
extrainfo:The circuit is an inverting amplifier with a gain of 12. Input voltage Vs is connected through a 1 kΩ resistor to the inverting input of the op-amp A0, and feedback is provided by a 12 kΩ resistor from the output to the inverting input. The non-inverting input is grounded, and the op-amp is powered by ±15V supplies.


Figure 5.11 $\triangle$ Inverting amplifier for Example 5.2.
b) Solve two different versions of the invertingamplifier equation for $v_{s}$-first using $v_{o}=+15 \mathrm{~V}$ and then using $v_{o}=-15 \mathrm{~V}$ :

$$
\begin{aligned}
15 & =-12 v_{s} \text { so } \quad v_{s}=-1.25 \mathrm{~V} \\
-15 & =-12 v_{s} \text { so } \quad v_{s}=1.25 \mathrm{~V}
\end{aligned}
$$

Thus, if the input voltage is greater than or equal to -1.25 V and less than or equal to +1.25 V , the op amp in the inverting-amplifier will remain in its linear operating region.

ASSESSMENT PROBLEM

Objective 2-Be able to analyze simple circuits containing ideal op amps
5.2 The source voltage $v_{s}$ in the circuit in Assessment Problem 5.1 is -640 mV . The $80 \mathrm{k} \Omega$ feedback resistor is replaced by a variable resistor $R_{x}$. What range of $R_{x}$ allows the
inverting amplifier to operate in its linear region?

Answer: $0 \leq R_{x} \leq 250 \mathrm{k} \Omega$.

NOTE: Also try Chapter Problems 5.9 and 5.11.
image_name:Figure 5.12
description:
[
'name': 'Ra', 'type': 'Resistor', 'value': 'Ra', 'ports': {'N1': 'va', 'N2': 'vD'
'name': 'Rb', 'type': 'Resistor', 'value': 'Rb', 'ports': {'N1': 'vb', 'N2': 'vD'
'name': 'Rc', 'type': 'Resistor', 'value': 'Rc', 'ports': {'N1': 'vc', 'N2': 'vD'
'name': 'Rf', 'type': 'Resistor', 'value': 'Rf', 'ports': {'N1': 'vD', 'N2': 'vo'
'name': 'A0', 'type': 'OpAmp', 'value': 'A0', 'ports': {'InP': 'GND', 'InN': 'vD', 'OutP': 'vo','Vdd':'+VCC', '-Vdd':'-VCC'
]
extrainfo:This is a summing amplifier circuit with three input voltages va, vb, and vc. The output voltage vo is an inverted, scaled sum of these input voltages. The op-amp is powered by VCC and -VCC.


Figure $5.12 \triangle$ A summing amplifier.

Inverting-summing amplifier equation

## 5.4 The Summing-Amplifier Circuit

The output voltage of a summing amplifier is an inverted, scaled sum of the voltages applied to the input of the amplifier. Figure 5.12 shows a summing amplifier with three input voltages.

We obtain the relationship between the output voltage $v_{o}$ and the three input voltages, $v_{\mathrm{a}}, v_{\mathrm{b}}$, and $v_{\mathrm{c}}$, by summing the currents away from the inverting input terminal:

$$
\begin{equation*}
\frac{v_{n}-v_{\mathrm{a}}}{R_{\mathrm{a}}}+\frac{v_{n}-v_{\mathrm{b}}}{R_{\mathrm{b}}}+\frac{v_{n}-v_{\mathrm{c}}}{R_{\mathrm{c}}}+\frac{v_{n}-v_{o}}{R_{f}}+i_{n}=0 \tag{5.13}
\end{equation*}
$$

Assuming an ideal op amp, we can use the voltage and current constraints together with the ground imposed at $v_{p}$ by the circuit to see that $v_{n}=v_{p}=0$ and $i_{n}=0$. This reduces Eq. 5.13 to

$$
\begin{equation*}
v_{o}=-\left(\frac{R_{f}}{R_{\mathrm{a}}} v_{\mathrm{a}}+\frac{R_{f}}{R_{\mathrm{b}}} v_{\mathrm{b}}+\frac{R_{f}}{R_{\mathrm{c}}} v_{\mathrm{c}}\right) \tag{5.14}
\end{equation*}
$$

Equation 5.14 states that the output voltage is an inverted, scaled sum of the three input voltages.

If $R_{\mathrm{a}}=R_{\mathrm{b}}=R_{\mathrm{c}}=R_{s}$, then Eq. 5.14 reduces to

$$
\begin{equation*}
v_{o}=-\frac{R_{f}}{R_{s}}\left(v_{\mathrm{a}}+v_{\mathrm{b}}+v_{\mathrm{c}}\right) \tag{5.15}
\end{equation*}
$$

Finally, if we make $R_{f}=R_{s}$, the output voltage is just the inverted sum of the input voltages. That is,

$$
\begin{equation*}
v_{o}=-\left(v_{\mathrm{a}}+v_{\mathrm{b}}+v_{\mathrm{c}}\right) \tag{5.16}
\end{equation*}
$$

Although we illustrated the summing amplifier with just three input signals, the number of input voltages can be increased as needed. For example, you might wish to sum 16 individually recorded audio signals to form a single audio signal. The summing amplifier configuration in Fig. 5.12 could include 16 different input resistor values so that each of the input audio tracks appears in the output signal with a different amplification factor. The summing amplifier thus plays the role of an audio mixer. As with inverting-amplifier circuits, the scaling factors in summing-amplifier circuits are determined by the external resistors $R_{f}, R_{\mathrm{a}}, R_{\mathrm{b}}, R_{\mathrm{c}}, \ldots, R_{n}$.

ASSESSMENT PROBLEM

Objective 2-Be able to analyze simple circuits containing ideal op amps
5.3 a) Find $v_{o}$ in the circuit shown if $v_{\mathrm{a}}=0.1 \mathrm{~V}$ and $v_{\mathrm{b}}=0.25 \mathrm{~V}$.
b) If $v_{\mathrm{b}}=0.25 \mathrm{~V}$, how large can $v_{\mathrm{a}}$ be before the op amp saturates?
c) If $v_{\mathrm{a}}=0.10 \mathrm{~V}$, how large can $v_{\mathrm{b}}$ be before the op amp saturates?
d) Repeat (a), (b), and (c) with the polarity of $v_{\mathrm{b}}$ reversed.

Answer: (a) -7.5 V;
(b) 0.15 V ;

NOTE: Also try Chapter Problems 5.12-5.14.
(c) 0.5 V ;
(d) $-2.5,0.25$, and 2 V .
image_name:Figure
description:
[
'name': 'Va', 'type': 'VoltageSource', 'value': 'Va', 'ports': {'Np': 'Va', 'Nn': 'GND'
'name': 'Vb', 'type': 'VoltageSource', 'value': 'Vb', 'ports': {'Np': 'Vb', 'Nn': 'GND'
'name': '5 kΩ', 'type': 'Resistor', 'value': '5 kΩ', 'ports': {'N1': 'Va', 'N2': 'InN(A0)'
'name': '25 kΩ', 'type': 'Resistor', 'value': '25 kΩ', 'ports': {'N1': 'Vb', 'N2': 'InN(A0)'
'name': '250 kΩ', 'type': 'Resistor', 'value': '250 kΩ', 'ports': {'N1': 'Vo', 'N2': 'InP(A0)'
'name': 'A0', 'type': 'OpAmp', 'value': 'A0', 'ports': {'InP': 'GND', 'InN': 'InN(A0)', 'OutP': 'Vo'，'Vdd':'15V','-Vdd':'-10V'
]
extrainfo:This circuit is a non-inverting amplifier with feedback. The op-amp is powered by a dual supply of +15V and -10V. The input voltages are Va and Vb, and the output voltage is Vo. The resistors form a voltage divider network for the op-amp input.


## 5.5 The Noninverting-Amplifier Circuit

Figure 5.13 depicts a noninverting-amplifier circuit. The signal source is represented by $v_{g}$ in series with the resistor $R_{g}$. In deriving the expression for the output voltage as a function of the source voltage, we assume an ideal op amp operating within its linear region. Thus, as before, we use Eqs. 5.2 and 5.3 as the basis for the derivation. Because the op amp input current is zero, we can write $v_{p}=v_{g}$ and, from Eq. 5.2, $v_{n}=v_{g}$ as well. Now, because the input current is zero $\left(i_{n}=i_{p}=0\right)$, the resistors $R_{f}$ and $R_{s}$ form an unloaded voltage divider across $v_{o}$. Therefore,

$$
\begin{equation*}
v_{n}=v_{g}=\frac{v_{o} R_{s}}{R_{s}+R_{f}} \tag{5.17}
\end{equation*}
$$

Solving Eq. 5.17 for $v_{o}$ gives us the sought-after expression:

$$
\begin{equation*}
v_{o}=\frac{R_{s}+R_{f}}{R_{s}} v_{g} \tag{5.18}
\end{equation*}
$$

image_name:Figure 5.13
description:
[
'name': 'Rs1', 'type': 'Resistor', 'value': 'Rs', 'ports': {'N1': 'GND', 'N2': 'InN(Ao)'
'name': 'Rf', 'type': 'Resistor', 'value': 'Rf', 'ports': {'N1': 'Vo', 'N2': 'InN(Ao)'
'name': 'Vg', 'type': 'VoltageSource', 'value': 'Vg', 'ports': {'Np': 'Vg', 'Nn': 'GND'
'name': 'Ao', 'type': 'OpAmp', 'value': 'Ao', 'ports': {'InP': 'InP(Ao)', 'InN': 'InN(Ao)', 'OutP': 'Vo','Vdd':'+VCC','-Vdd':'-VCC'
'name': 'Rs2', 'type': 'Resistor', 'value': 'Rs', 'ports': {'N1': 'Vg', 'N2': 'InP(Ao)'
]
extrainfo:The circuit is a non-inverting amplifier configuration using an operational amplifier (Ao). The input voltage Vg is applied to the non-inverting input of the op-amp through a resistor Rs. The feedback resistor Rf and Rs form a voltage divider network that determines the gain of the amplifier. The output voltage Vo is taken from the op-amp's output. The amplifier is powered by a dual supply voltage VCC and -VCC.


Figure $5.13 \triangle \mathrm{~A}$ noninverting amplifier.

Operation in the linear region requires that

$$
\frac{R_{s}+R_{f}}{R_{s}}<\left|\frac{V_{C C}}{v_{g}}\right|
$$

Note again that, because of the ideal op amp assumption, we can express the output voltage as a function of the input voltage and the external resistors-in this case, $R_{s}$ and $R_{f}$.

Example 5.3 illustrates the design of a noninverting amplifier using realistic resistor values.

#### Example 5.3 Designing a Noninverting Amplifier

a) Design a noninverting amplifier (see Fig. 5.13) with a gain of 6 . Assume the op amp is ideal.
b) Suppose we wish to amplify a voltage $v_{\mathrm{g}}$, such that $-1.5 \mathrm{~V} \leq v_{g} \leq+1.5 \mathrm{~V}$. What are the smallest power supply voltages that could be used with the resistors selected in part (a) and still have the op amp in this design remain in its linear operating region?

#### Solution

a) Using the noninverting amplifier equation (Eq. 5.18),

$$
v_{o}=\frac{R_{s}+R_{f}}{R_{s}} v_{g}=6 v_{g} \quad \text { so } \quad \frac{R_{s}+R_{f}}{R_{s}}=6
$$

Therefore,

$$
R_{s}+R_{f}=6 R_{s}, \quad \text { so } \quad R_{f}=5 R_{s}
$$

We want two resistors whose ratio is 5 . Look at the realistic resistor values listed in Appendix H. Let's choose $R_{f}=10 \mathrm{k} \Omega$, so $R_{s}=2 \mathrm{k} \Omega$. But there is not a $2 \mathrm{k} \Omega$ resistor in Appendix H. We can create an equivalent $2 \mathrm{k} \Omega$ resistor by combining two $1 \mathrm{k} \Omega$ resistors in series. We can use a third $1 \mathrm{k} \Omega$ resistor as the value of the resistor $R_{g}$.
b) Solve two different versions of the noninverting amplifier equation for $v_{o}$-first using $v_{g}=+1.5 \mathrm{~V}$ and then using $v_{g}=-1.5 \mathrm{~V}$ :

$$
\begin{aligned}
& v_{o}=6(1.5)=9 \mathrm{~V} \\
& v_{o}=6(-1.5)=-9 \mathrm{~V}
\end{aligned}
$$

Thus, if we use $\pm 9 \mathrm{~V}$ power supplies for the noninverting amplifier designed in part (a) and $-1.5 \mathrm{~V} \leq v_{g} \leq+1.5 \mathrm{~V}$, the op amp will remain in its linear operating region. The circuit resulting from the analysis in parts (a) and (b) is shown in Fig. 5.14.
image_name:Figure 5.14
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '1kΩ', 'ports': {'N1': 'GND', 'N2': 'X1'
'name': 'R2', 'type': 'Resistor', 'value': '1kΩ', 'ports': {'N1': 'X1', 'N2': 'InN(A0)'
'name': 'R3', 'type': 'Resistor', 'value': '1kΩ', 'ports': {'N1': 'Vg', 'N2': 'InP(A0)'
'name': 'R4', 'type': 'Resistor', 'value': '10kΩ', 'ports': {'N1': 'InN(A0)', 'N2': 'Vo'
'name': 'Vg', 'type': 'VoltageSource', 'value': 'Vg', 'ports': {'Np': 'Vg', 'Nn': 'GND'
'name': 'A0', 'type': 'OpAmp', 'value': 'A0', 'ports': {'InP': 'InP(A0)', 'InN': 'InN(A0)', 'OutP': 'Vo','Vdd':'1.5V','-Vdd':'-1.5V'
]
extrainfo:The circuit is a non-inverting amplifier with a gain set by the resistors, using an ideal op-amp. The op-amp is powered by ±1.5 V supplies.


Figure 5.14 A The noninverting amplifier design of Example 5.3.

ASSESSMENT PROBLEM

Objective 2-Be able to analyze simple circuits containing ideal op amps
5.4 Assume that the op amp in the circuit shown is ideal.
a) Find the output voltage when the variable resistor is set to $60 \mathrm{k} \Omega$.
b) How large can $R_{x}$ be before the amplifier saturates?
Answer: (a) 4.8 V ;
(b) $75 \mathrm{k} \Omega$.
image_name:Figure
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '4.5kΩ', 'ports': {'N1': 'GND', 'N2': 'InN(A0)'
'name': 'R2', 'type': 'Resistor', 'value': '15kΩ', 'ports': {'N1': 'Vin', 'N2': 'InP(A0)'
'name': 'R3', 'type': 'Resistor', 'value': '63kΩ', 'ports': {'N1': 'Vo', 'N2': 'InN(A0)'
'name': 'Rx', 'type': 'Resistor', 'value': 'Rx', 'ports': {'N1': 'InP(A0)', 'N2': 'GND'
'name': 'Vin', 'type': 'VoltageSource', 'value': '400mV', 'ports': {'Np': 'Vin', 'Nn': 'GND'
'name': 'A0', 'type': 'OpAmp', 'value': 'A0', 'ports': {'InP': 'InP(A0)', 'InN': 'InN(A0)', 'OutP': 'Vo', 'Vdd': '+5V', '-Vdd': '-5V'
]
extrainfo:The circuit is a non-inverting amplifier using an ideal op-amp with ±5V supplies. The output voltage is dependent on the resistor values and the input voltage. The variable resistor Rx affects the gain and saturation point of the amplifier.


NOTE: Also try Chapter Problems 5.19 and 5.20.

## 5.6 The Difference-Amplifier Circuit

The output voltage of a difference amplifier is proportional to the difference between the two input voltages. To demonstrate, we analyze the differenceamplifier circuit shown in Fig. 5.15, assuming an ideal op amp operating in its linear region. We derive the relationship between $v_{o}$ and the two input voltages $v_{\mathrm{a}}$ and $v_{\mathrm{b}}$ by summing the currents away from the inverting input node:

$$
\begin{equation*}
\frac{v_{n}-v_{\mathrm{a}}}{R_{\mathrm{a}}}+\frac{v_{n}-v_{o}}{R_{\mathrm{b}}}+i_{n}=0 \tag{5.19}
\end{equation*}
$$

Because the op amp is ideal, we use the voltage and current constraints to see that

$$
\begin{align*}
& i_{n}=i_{p}=0  \tag{5.20}\\
& v_{n}=v_{p}=\frac{R_{\mathrm{d}}}{R_{\mathrm{c}}+R_{\mathrm{d}}} v_{\mathrm{b}} \tag{5.21}
\end{align*}
$$

Combining Eqs. 5.19, 5.20, and 5.21 gives the desired relationship:

$$
\begin{equation*}
v_{o}=\frac{R_{\mathrm{d}}\left(R_{\mathrm{a}}+R_{\mathrm{b}}\right)}{R_{\mathrm{a}}\left(R_{\mathrm{c}}+R_{\mathrm{d}}\right)} v_{\mathrm{b}}-\frac{R_{\mathrm{b}}}{R_{\mathrm{a}}} v_{\mathrm{a}} . \tag{5.22}
\end{equation*}
$$

Equation 5.22 shows that the output voltage is proportional to the difference between a scaled replica of $v_{\mathrm{b}}$ and a scaled replica of $v_{\mathrm{a}}$. In general the scaling factor applied to $v_{\mathrm{b}}$ is not the same as that applied to $v_{\mathrm{a}}$. However, the scaling factor applied to each input voltage can be made equal by setting

$$
\begin{equation*}
\frac{R_{\mathrm{a}}}{R_{\mathrm{b}}}=\frac{R_{\mathrm{c}}}{R_{\mathrm{d}}} \tag{5.23}
\end{equation*}
$$

When Eq. 5.23 is satisfied, the expression for the output voltage reduces to

$$
\begin{equation*}
v_{o}=\frac{R_{\mathrm{b}}}{R_{\mathrm{a}}}\left(v_{\mathrm{b}}-v_{\mathrm{a}}\right) \tag{5.24}
\end{equation*}
$$

Simplified difference-amplifier equation

Equation 5.24 indicates that the output voltage can be made a scaled replica of the difference between the input voltages $v_{\mathrm{b}}$ and $v_{\mathrm{a}}$. As in the previous ideal amplifier circuits, the scaling is controlled by the external resistors. Furthermore, the relationship between the output voltage and the input voltages is not affected by connecting a nonzero load resistance across the output of the amplifier.

Example 5.4 describes the design of a difference amplifier using realistic resistor values.
image_name:Figure 5.15
description:
[
'name': 'Va', 'type': 'VoltageSource', 'value': 'Va', 'ports': {'Np': 'va', 'Nn': 'GND'
'name': 'Vb', 'type': 'VoltageSource', 'value': 'Vb', 'ports': {'Np': 'vb', 'Nn': 'GND'
'name': 'Ra', 'type': 'Resistor', 'value': 'Ra', 'ports': {'N1': 'va', 'N2': 'InN(Ao)'
'name': 'Rb', 'type': 'Resistor', 'value': 'Rb', 'ports': {'N1': 'Vo', 'N2': 'InN(Ao)'
'name': 'Rc', 'type': 'Resistor', 'value': 'Rc', 'ports': {'N1': 'vb', 'N2': 'InP(A0)'
'name': 'Rd', 'type': 'Resistor', 'value': 'Rd', 'ports': {'N1': 'InP(A0)', 'N2': 'GND'
'name': 'Ao', 'type': 'OpAmp', 'value': 'Ao', 'ports': {'InP': 'InP(A0)', 'InN': 'InN(Ao)', 'OutP': 'Vo','Vdd': '+VCC', '-Vdd': '-VCC'
]
extrainfo:The circuit is a difference amplifier where the output voltage Vo is a scaled version of the difference between input voltages va and vb. The scaling factor is determined by the resistors Ra and Rb. The op-amp is powered by a dual supply of +VCC and -VCC. Resistors Rc and Rd are used to set the reference voltage for the op-amp.


Figure 5.15 $\triangle$ A difference amplifier.

#### Solution

a) Using the simplified difference-amplifier equation (Eq. 5.24),
$v_{o}=\frac{R_{\mathrm{b}}}{R_{\mathrm{a}}}\left(v_{\mathrm{b}}-v_{\mathrm{a}}\right)=8\left(v_{\mathrm{b}}-v_{\mathrm{a}}\right)$ so $\frac{R_{\mathrm{b}}}{R_{\mathrm{a}}}=8$.
We want two resistors whose ratio is 8 . Look at the realistic resistor values listed in Appendix H. Let's choose $R_{\mathrm{b}}=12 \mathrm{k} \Omega$, so $R_{\mathrm{a}}=1.5 \mathrm{k} \Omega$, although there are many other possibilities. Note that the simplified difference-amplifier equation requires that

$$
\frac{R_{\mathrm{a}}}{R_{\mathrm{b}}}=\frac{R_{\mathrm{c}}}{R_{\mathrm{d}}}
$$

A simple choice for $R_{\mathrm{c}}$ and $R_{\mathrm{d}}$ is $R_{\mathrm{c}}=R_{\mathrm{a}}=$ $1.5 \mathrm{k} \Omega$ and $R_{\mathrm{d}}=R_{\mathrm{b}}=12 \mathrm{k} \Omega$. The resulting circuit is shown in Fig. 5.16.
image_name:Figure 5.16
description:
[
'name': 'Va', 'type': 'VoltageSource', 'value': 'Va', 'ports': {'Np': 'Va', 'Nn': 'GND'
'name': 'Vb', 'type': 'VoltageSource', 'value': 'Vb', 'ports': {'Np': 'Vb', 'Nn': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': '1.5kΩ', 'ports': {'N1': 'Va', 'N2': 'InN(A2)'
'name': 'R2', 'type': 'Resistor', 'value': '1.5kΩ', 'ports': {'N1': 'Vb', 'N2': 'InP(A2)'
'name': 'R3', 'type': 'Resistor', 'value': '12kΩ', 'ports': {'N1': 'InN(A2)', 'N2': 'Vo'
'name': 'R4', 'type': 'Resistor', 'value': '12kΩ', 'ports': {'N1': 'InP(A2)', 'N2': 'GND'
'name': 'A1', 'type': 'OpAmp', 'value': 'OpAmp', 'ports': {'InP': 'InP(A2)', 'InN': 'InN(A2)', 'OutP': 'Vo','Vdd': '+8V', '-Vdd': '-8V'
]
extrainfo:The circuit is a difference amplifier with a gain of 8. It uses two voltage sources Va and Vb, and resistors to set the gain. The op-amp is powered by ±8V.


Figure 5.16 $\Delta$ The difference amplifier designed in Example 5.4.
b) Solve two different versions of the simplified difference-amplifier equation for $v_{o}$ in terms of $v_{\mathrm{b}}$-first using $v_{o}=+8 \mathrm{~V}$ and then using $v_{o}=-8 \mathrm{~V}$ :

$$
\begin{aligned}
& v_{o}=8\left(v_{\mathrm{b}}-1\right)=8 \mathrm{~V} \quad \text { so } v_{\mathrm{b}}=2 \mathrm{~V} \\
& v_{o}=8\left(v_{\mathrm{b}}-1\right)=-8 \mathrm{~V} \quad \text { so } v_{\mathrm{b}}=0 \mathrm{~V}
\end{aligned}
$$

Thus, if $v_{\mathrm{a}}=1 \mathrm{~V}$ in the difference amplifier from part (a), the op amp will remain in its linear region of operation if $0 \mathrm{~V} \leq v_{\mathrm{b}} \leq+2 \mathrm{~V}$.

ASSESSMENT PROBLEM

Objective 2-Be able to analyze simple circuits containing ideal op amps

5.5 a) In the difference amplifier shown, $v_{\mathrm{b}}=4.0 \mathrm{~V}$. What range of values for $v_{\mathrm{a}}$ will result in linear operation?
b) Repeat (a) with the $20 \mathrm{k} \Omega$ resistor decreased to $8 \mathrm{k} \Omega$.

Answer: (a) $2 \mathrm{~V} \leq v_{\mathrm{a}} \leq 6 \mathrm{~V}$;
(b) $1.2 \mathrm{~V} \leq v_{\mathrm{a}} \leq 5.2 \mathrm{~V}$.
image_name:Difference Amplifier
description:
[
'name': 'Va', 'type': 'VoltageSource', 'value': 'Va', 'ports': {'Np': 'Va', 'Nn': 'GND'
'name': 'Vb', 'type': 'VoltageSource', 'value': 'Vb', 'ports': {'Np': 'Vb', 'Nn': 'GND'
'name': '10kΩ', 'type': 'Resistor', 'value': '10kΩ', 'ports': {'N1': 'Va', 'N2': 'InN(A0)'
'name': '4kΩ', 'type': 'Resistor', 'value': '4kΩ', 'ports': {'N1': 'Vb', 'N2': 'InP(A0)'
'name': '20kΩ', 'type': 'Resistor', 'value': '20kΩ', 'ports': {'N1': 'InP(A0)', 'N2': 'GND'
'name': '50kΩ', 'type': 'Resistor', 'value': '50kΩ', 'ports': {'N1': 'Vo', 'N2': 'InN(A0)'
'name': 'A0', 'type': 'OpAmp', 'value': 'A0', 'ports': {'InP': 'InP(A0)', 'InN': 'InN(A0)', 'OutP': 'Vo', 'Vdd': '+10V', '-Vdd': '-10V'
]
extrainfo:The circuit is a difference amplifier with a configuration to amplify the difference between two input voltages, Va and Vb. The output voltage Vo is determined by the resistors and the input voltages. The op-amp is powered by a dual supply of +10V and -10V.


NOTE: Also try Chapter Problems 5.26, 5.27, and 5.30.

The Difference Amplifier—Another Perspective

We can examine the behavior of a difference amplifier more closely if we redefine its inputs in terms of two other voltages. The first is the differential mode input, which is the difference between the two input voltages in Fig. 5.15:

$$
\begin{equation*}
v_{\mathrm{dm}}=v_{\mathrm{b}}-v_{\mathrm{a}} \tag{5.25}
\end{equation*}
$$

The second is the common mode input, which is the average of the two input voltages in Fig. 5.15:

$$
\begin{equation*}
v_{\mathrm{cm}}=\left(v_{\mathrm{a}}+v_{\mathrm{b}}\right) / 2 \tag{5.26}
\end{equation*}
$$

Using Eqs. 5.25 and 5.26, we can now represent the original input voltages, $v_{\mathrm{a}}$ and $v_{\mathrm{b}}$, in terms of the differential mode and common mode voltages, $v_{\mathrm{dm}}$ and $v_{\mathrm{cm}}$ :

$$
\begin{align*}
& v_{\mathrm{a}}=v_{\mathrm{cm}}-\frac{1}{2} v_{\mathrm{dm}}  \tag{5.27}\\
& v_{\mathrm{b}}=v_{\mathrm{cm}}+\frac{1}{2} v_{\mathrm{dm}} \tag{5.28}
\end{align*}
$$

Substituting Eqs. 5.27 and 5.28 into Eq. 5.22 gives the output of the difference amplifier in terms of the differential mode and common mode voltages:

$$
\begin{align*}
v_{o}= & {\left[\frac{R_{\mathrm{a}} R_{\mathrm{d}}-R_{\mathrm{b}} R_{\mathrm{c}}}{R_{\mathrm{a}}\left(R_{\mathrm{c}}+R_{\mathrm{d}}\right)}\right] v_{\mathrm{cm}} } \\
& +\left[\frac{R_{\mathrm{d}}\left(R_{\mathrm{a}}+R_{\mathrm{b}}\right)+R_{\mathrm{b}}\left(R_{\mathrm{c}}+R_{\mathrm{d}}\right)}{2 R_{\mathrm{a}}\left(R_{\mathrm{c}}+R_{\mathrm{d}}\right)}\right] v_{\mathrm{dm}}  \tag{5.29}\\
= & A_{\mathrm{cm}} v_{\mathrm{cm}}+A_{\mathrm{dm}} v_{\mathrm{dm}} \tag{5.30}
\end{align*}
$$

where $A_{\mathrm{cm}}$ is the common mode gain and $A_{\mathrm{dm}}$ is the differential mode gain. Now, substitute $R_{\mathrm{c}}=R_{\mathrm{a}}$ and $R_{\mathrm{d}}=R_{\mathrm{b}}$, which are possible values for $R_{\mathrm{c}}$ and $R_{\mathrm{d}}$ that satisfy Eq. 5.23, into Eq. 5.29:

$$
\begin{equation*}
v_{o}=(0) v_{\mathrm{cm}}+\left(\frac{R_{\mathrm{b}}}{R_{\mathrm{a}}}\right) v_{\mathrm{dm}} \tag{5.31}
\end{equation*}
$$

Thus, an ideal difference amplifier has $A_{\mathrm{cm}}=0$, amplifies only the differential mode portion of the input voltage, and eliminates the common mode portion of the input voltage. Figure 5.17 shows a differenceamplifier circuit with differential mode and common mode input voltages in place of $v_{\mathrm{a}}$ and $v_{\mathrm{b}}$.

Equation 5.30 provides an important perspective on the function of the difference amplifier, since in many applications it is the differential mode signal that contains the information of interest, whereas the common mode signal is the noise found in all electric signals. For example, an electrocardiograph electrode measures the voltages produced by your body to regulate your heartbeat. These voltages have very small magnitudes compared with the electrical noise that the electrode picks up from sources such as lights and electrical equipment. The noise appears as the common mode portion of the measured voltage, whereas the heart rate voltages comprise the differential mode portion. Thus an ideal difference amplifier would amplify only the voltage of interest and would suppress the noise.

Measuring Difference-Amplifier PerformanceThe Common Mode Rejection Ratio

An ideal difference amplifier has zero common mode gain and nonzero (and usually large) differential mode gain. Two factors have an influence on the ideal common mode gain-resistance mismatches (that is, Eq. [5.23] is not satisfied) or a nonideal op amp (that is, Eq. [5.20] is not satisfied). We focus here on the effect of resistance mismatches on the performance of a difference amplifier.
image_name:Figure 5.17 A
description:
[
'name': 'Ra', 'type': 'Resistor', 'value': 'Ra', 'ports': {'N1': 'b', 'N2': 'InN(Ao)'
'name': 'Rb', 'type': 'Resistor', 'value': 'Rb', 'ports': {'N1': 'InN(Ao)', 'N2': 'Vo'
'name': 'Rc', 'type': 'Resistor', 'value': 'Rc', 'ports': {'N1': 'b', 'N2': 'InP(Ao)'
'name': 'Rd', 'type': 'Resistor', 'value': 'Rd', 'ports': {'N1': 'InP(Ao)', 'N2': 'GND'
'name': 'Ao', 'type': 'OpAmp', 'value': 'Ao', 'ports': {'InP': 'InP(Ao)', 'InN': 'InN(Ao)', 'OutP': 'Vo','Vdd': '+VCC', '-Vdd': '-VCC'
'name': 'Vcm', 'type': 'VoltageSource', 'value': 'Vcm', 'ports': {'Np': 'Vcm', 'Nn': 'GND'
'name': 'vdm/2', 'type': 'VoltageSource', 'value': 'vdm/2', 'ports': {'Np': 'b', 'Nn': 'Vcm'
]
extrainfo:The circuit is a difference amplifier with common mode and differential mode input voltages. It utilizes an operational amplifier with resistors Ra, Rb, Rc, and Rd to achieve the desired amplification. The diagram indicates the importance of resistor matching to minimize common mode gain and maximize differential mode gain.


Figure 5.17 A A difference amplifier with common mode and differential mode input voltages.

Suppose that resistor values are chosen that do not precisely satisfy Eq. 5.23. Instead, the relationship among the resistors $R_{\mathrm{a}}, R_{\mathrm{b}}, R_{\mathrm{c}}$, and $R_{\mathrm{d}}$ is

$$
\frac{R_{\mathrm{a}}}{R_{\mathrm{b}}}=(1-\epsilon) \frac{R_{\mathrm{c}}}{R_{\mathrm{d}}}
$$

so

$$
\begin{equation*}
R_{\mathrm{a}}=(1-\epsilon) R_{\mathrm{c}} \quad \text { and } \quad R_{\mathrm{b}}=R_{\mathrm{d}} \tag{5.32}
\end{equation*}
$$

or

$$
\begin{equation*}
R_{\mathrm{d}}=(1-\epsilon) R_{\mathrm{b}} \quad \text { and } \quad R_{\mathrm{a}}=R_{\mathrm{c}} \tag{5.33}
\end{equation*}
$$

where $\epsilon$ is a very small number. We can see the effect of this resistance mismatch on the common mode gain of the difference amplifier by substituting Eq. 5.33 into Eq. 5.29 and simplifying the expression for $A_{\mathrm{cm}}$ :

$$
\begin{align*}
A_{\mathrm{cm}} & =\frac{R_{\mathrm{a}}(1-\epsilon) R_{\mathrm{b}}-R_{\mathrm{a}} R_{\mathrm{b}}}{R_{\mathrm{a}}\left[R_{\mathrm{a}}+(1-\epsilon) R_{\mathrm{b}}\right]}  \tag{5.34}\\
& =\frac{-\epsilon R_{\mathrm{b}}}{R_{\mathrm{a}}+(1-\epsilon) R_{\mathrm{b}}}  \tag{5.35}\\
& \approx \frac{-\epsilon R_{\mathrm{b}}}{R_{\mathrm{a}}+R_{\mathrm{b}}} \tag{5.36}
\end{align*}
$$

We can make the approximation to give Eq. 5.36 because $\epsilon$ is very small, and therefore $(1-\epsilon)$ is approximately 1 in the denominator of Eq. 5.35. Note that, when the resistors in the difference amplifier satisfy Eq. 5.23, $\epsilon=0$ and Eq. 5.36 gives $A_{\mathrm{cm}}=0$.

Now calculate the effect of the resistance mismatch on the differential mode gain by substituting Eq. 5.33 into Eq. 5.29 and simplifying the expression for $A_{\mathrm{dm}}$ :

$$
\begin{align*}
A_{\mathrm{dm}} & =\frac{(1-\epsilon) R_{\mathrm{b}}\left(R_{\mathrm{a}}+R_{\mathrm{b}}\right)+R_{\mathrm{b}}\left[R_{\mathrm{a}}+(1-\epsilon) R_{\mathrm{b}}\right]}{2 R_{\mathrm{a}}\left[R_{\mathrm{a}}+(1-\epsilon) R_{\mathrm{b}}\right]}  \tag{5.37}\\
& =\frac{R_{\mathrm{b}}}{R_{\mathrm{a}}}\left[1-\frac{(\epsilon / 2) R_{\mathrm{a}}}{R_{\mathrm{a}}+(1-\epsilon) R_{\mathrm{b}}}\right]  \tag{5.38}\\
& \approx \frac{R_{\mathrm{b}}}{R_{\mathrm{a}}}\left[1-\frac{(\epsilon / 2) R_{\mathrm{a}}}{R_{\mathrm{a}}+R_{\mathrm{b}}}\right] \tag{5.39}
\end{align*}
$$

We use the same rationale for the approximation in Eq. 5.39 as in the computation of $A_{\mathrm{cm}}$. When the resistors in the difference amplifier satisfy Eq. 5.23, $\epsilon=0$ and Eq. 5.39 gives $A_{\mathrm{dm}}=R_{\mathrm{b}} / R_{\mathrm{a}}$.

The common mode rejection ratio (CMRR) can be used to measure how nearly ideal a difference amplifier is. It is defined as the ratio of the differential mode gain to the common mode gain:

$$
\begin{equation*}
\mathrm{CMRR}=\left|\frac{A_{\mathrm{dm}}}{A_{\mathrm{cm}}}\right| \tag{5.40}
\end{equation*}
$$

The higher the CMRR, the more nearly ideal the difference amplifier. We can see the effect of resistance mismatch on the CMRR by substituting Eqs. 5.36 and 5.39 into Eq. 5.40:

$$
\begin{align*}
\mathrm{CMRR} & \approx\left|\frac{\frac{R_{\mathrm{b}}}{R_{\mathrm{a}}}\left[1-\left(R_{\mathrm{a}} \epsilon / 2\right) /\left(R_{\mathrm{a}}+R_{\mathrm{b}}\right)\right]}{-\epsilon R_{\mathrm{b}} /\left(R_{\mathrm{a}}+R_{\mathrm{b}}\right)}\right|  \tag{5.41}\\
& \approx\left|\frac{R_{\mathrm{a}}(1-\epsilon / 2)+R_{\mathrm{b}}}{-\epsilon R_{\mathrm{a}}}\right|  \tag{5.42}\\
& \approx\left|\frac{1+R_{\mathrm{b}} / R_{\mathrm{a}}}{-\epsilon}\right| \tag{5.43}
\end{align*}
$$

From Eq. 5.43, if the resistors in the difference amplifier are matched, $\epsilon=0$ and $\mathrm{CMRR}=\infty$. Even if the resistors are mismatched, we can minimize the impact of the mismatch by making the differential mode gain $\left(R_{\mathrm{b}} / R_{\mathrm{a}}\right)$ very large, thereby making the CMRR large.

We said at the outset that another reason for nonzero common mode gain is a nonideal op amp. Note that the op amp is itself a difference amplifier, because in the linear operating region, its output is proportional to the difference of its inputs; that is, $v_{o}=A\left(v_{p}-v_{n}\right)$. The output of a nonideal op amp is not strictly proportional to the difference between the inputs (the differential mode input) but also is comprised of a common mode signal. Internal mismatches in the components of the integrated circuit make the behavior of the op amp nonideal, in the same way that the resistor mismatches in the difference-amplifier circuit make its behavior nonideal. Even though a discussion of nonideal op amps is beyond the scope of this text, you may note that the CMRR is often used in assessing how nearly ideal an op amp's behavior is. In fact, it is one of the main ways of rating op amps in practice.

NOTE: Assess your understanding of this material by trying Chapter
Problems 5.33 and 5.34.

## 5.7 A More Realistic Model for the Operational Amplifier

We now consider a more realistic model that predicts the performance of an op amp in its linear region of operation. Such a model includes three modifications to the ideal op amp: (1) a finite input resistance, $R_{i}$; (2) a finite open-loop gain, $A$; and (3) a nonzero output resistance, $R_{o}$. The circuit shown in Fig. 5.18 illustrates the more realistic model.

Whenever we use the equivalent circuit shown in Fig. 5.18, we disregard the assumptions that $v_{n}=v_{p}$ (Eq. 5.2) and $i_{n}=i_{p}=0$ (Eq. 5.3). Furthermore, Eq. 5.1 is no longer valid because of the presence of the nonzero output resistance, $R_{o}$. Another way to understand the circuit shown in Fig. 5.18 is to reverse our thought process. That is, we can see that the circuit reduces to the ideal model when $R_{i} \rightarrow \infty, A \rightarrow \infty$, and $R_{o} \rightarrow 0$. For the $\mu \mathrm{A} 741$ op amp, the typical values of $R_{i}, A$, and $R_{o}$ are $2 \mathrm{M} \Omega, 10^{5}$, and $75 \Omega$, respectively.

Although the presence of $R_{i}$ and $R_{o}$ makes the analysis of circuits containing op amps more cumbersome, such analysis remains straightforward.
image_name:Figure 5.18
description:
[
'name': 'Ri', 'type': 'Resistor', 'value': 'Ri', 'ports': {'N1': 'Vp', 'N2': 'Vn'
'name': 'Ro', 'type': 'Resistor', 'value': 'Ro', 'ports': {'N1': 'a', 'N2': 'Vo'
'name': 'VCVS', 'type': 'VoltageControlledVoltageSource', 'value': 'A(Vp-Vn)', 'ports': {'N1': 'a', 'N2': 'GND'
]
extrainfo:The circuit diagram is an equivalent model of an operational amplifier with input resistance Ri, output resistance Ro, and gain A. The input nodes are Vp and Vn, and the output node is Vo. The circuit illustrates the basic operation of an op-amp with finite input and output resistances.


Figure 5.18 A An equivalent circuit for an operational amplifier.
image_name:Figure 5.19
description:
[
'name': 'VS', 'type': 'VoltageSource', 'value': 'VS', 'ports': {'Np': 'VS', 'Nn': 'GND'
'name': 'RS', 'type': 'Resistor', 'value': 'RS', 'ports': {'N1': 'VS', 'N2': 'a'
'name': 'Rf', 'type': 'Resistor', 'value': 'Rf', 'ports': {'N1': 'Vn', 'N2': 'Vo'
'name': 'Ri', 'type': 'Resistor', 'value': 'Ri', 'ports': {'N1': 'Vp', 'N2': 'Vp'
'name': 'Ro', 'type': 'Resistor', 'value': 'Ro', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'VCVS', 'type': 'VoltageControlledVoltageSource', 'value': 'A(Vp-Vn)', 'ports': {'N1': 'c', 'N2': 'GND'
]
extrainfo:The circuit diagram is an equivalent model of an operational amplifier with input resistance Ri, output resistance Ro, and gain A. The input nodes are Vp and Vn, and the output node is Vo. The circuit illustrates the basic operation of an op-amp with finite input and output resistances.


Figure 5.19 A An inverting-amplifier circuit.
image_name:Figure 5.20
description:
[
'name': 'Rs', 'type': 'Resistor', 'value': 'Rs', 'ports': {'N1': 'GND', 'N2': 'a'
'name': 'Rf', 'type': 'Resistor', 'value': 'Rf', 'ports': {'N1': 'Vn', 'N2': 'Vo'
'name': 'Ri', 'type': 'Resistor', 'value': 'Ri', 'ports': {'N1': 'Vn', 'N2': 'Vp'
'name': 'Ro', 'type': 'Resistor', 'value': 'Ro', 'ports': {'N1': 'C', 'N2': 'Vo'
'name': 'Rg', 'type': 'Resistor', 'value': 'Rg', 'ports': {'N1': 'vg', 'N2': 'Vp'
'name': 'RL', 'type': 'Resistor', 'value': 'RL', 'ports': {'N1': 'Vo', 'N2': 'GND'
'name': 'vg', 'type': 'VoltageSource', 'value': 'vg', 'ports': {'Np': 'Vp', 'Nn': 'GND'
'name': 'VCVS', 'type': 'VoltageControlledVoltageSource', 'value': 'A(Vp-Vn)', 'ports': {'N1': 'c', 'N2': 'GND'
]
extrainfo:The circuit diagram is an equivalent model of an operational amplifier with input resistance Ri, output resistance Ro, and gain A. It represents an inverting amplifier configuration with feedback resistor Rf and input resistor Rs. The input voltage is connected to node Vn, and the output voltage is measured at node Vo. The circuit demonstrates the basic operation of an op-amp with finite input and output resistances, including the effects of feedback.


Figure $5.20 \triangle$ A noninverting-amplifier circuit.

To illustrate, we analyze both an inverting and a noninverting amplifier, using the equivalent circuit shown in Fig. 5.18. We begin with the inverting amplifier.

Analysis of an Inverting-Amplifier Circuit Using the More Realistic Op Amp Model

If we use the op amp circuit shown in Fig. 5.18, the circuit for the inverting amplifier is the one depicted in Fig. 5.19. As before, our goal is to express the output voltage, $v_{o}$, as a function of the source voltage, $v_{s}$. We obtain the desired expression by writing the two node-voltage equations that describe the circuit and then solving the resulting set of equations for $v_{o}$. In Fig. 5.19, the two nodes are labeled a and b. Also note that $v_{p}=0$ by virtue of the external short-circuit connection at the noninverting input terminal. The two node-voltage equations are as follows:

$$
\begin{align*}
& \text { node a: } \frac{v_{n}-v_{s}}{R_{s}}+\frac{v_{n}}{R_{i}}+\frac{v_{n}-v_{o}}{R_{f}}=0  \tag{5.44}\\
& \text { node b: } \frac{v_{o}-v_{n}}{R_{f}}+\frac{v_{o}-A\left(-v_{n}\right)}{R_{o}}=0 \tag{5.45}
\end{align*}
$$

We rearrange Eqs. 5.44 and 5.45 so that the solution for $v_{o}$ by Cramer's method becomes apparent:

$$
\begin{align*}
& \left(\frac{1}{R_{s}}+\frac{1}{R_{i}}+\frac{1}{R_{f}}\right) v_{n}-\frac{1}{R_{f}} v_{o}=\frac{1}{R_{s}} v_{s},  \tag{5.46}\\
& \left(\frac{A}{R_{o}}-\frac{1}{R_{f}}\right) v_{n}+\left(\frac{1}{R_{f}}+\frac{1}{R_{o}}\right) v_{o}=0 . \tag{5.47}
\end{align*}
$$

Solving for $v_{o}$ yields

$$
\begin{equation*}
v_{o}=\frac{-A+\left(R_{o} / R_{f}\right)}{\frac{R_{s}}{R_{f}}\left(1+A+\frac{R_{o}}{R_{i}}\right)+\left(\frac{R_{s}}{R_{i}}+1\right)+\frac{R_{o}}{R_{f}}} v_{s} \tag{5.48}
\end{equation*}
$$

Note that Eq. 5.48 reduces to Eq. 5.10 as $R_{o} \rightarrow 0, R_{i} \rightarrow \infty$, and $A \rightarrow \infty$.
If the inverting amplifier shown in Fig. 5.19 were loaded at its output terminals with a load resistance of $R_{L}$ ohms, the relationship between $v_{o}$ and $v_{s}$ would become

$$
\begin{equation*}
v_{o}=\frac{-A+\left(R_{o} / R_{f}\right)}{\frac{R_{s}}{R_{f}}\left(1+A+\frac{R_{o}}{R_{i}}+\frac{R_{o}}{R_{L}}\right)+\left(1+\frac{R_{o}}{R_{L}}\right)\left(1+\frac{R_{s}}{R_{i}}\right)+\frac{R_{o}}{R_{f}}} v_{s} \tag{5.49}
\end{equation*}
$$

Analysis of a Noninverting-Amplifier Circuit Using the More Realistic Op Amp Model

When we use the equivalent circuit shown in Fig. 5.18 to analyze a noninverting amplifier, we obtain the circuit depicted in Fig. 5.20. Here, the voltage source $v_{g}$, in series with the resistance $R_{g}$, represents the signal source. The resistor $R_{L}$ denotes the load on the amplifier. Our analysis
consists of deriving an expression for $v_{o}$ as a function of $v_{g}$. We do so by writing the node-voltage equations at nodes a and b . At node a ,

$$
\begin{equation*}
\frac{v_{n}}{R_{s}}+\frac{v_{n}-v_{g}}{R_{g}+R_{i}}+\frac{v_{n}-v_{o}}{R_{f}}=0 \tag{5.50}
\end{equation*}
$$

and at node b ,

$$
\begin{equation*}
\frac{v_{o}-v_{n}}{R_{f}}+\frac{v_{o}}{R_{L}}+\frac{v_{o}-A\left(v_{p}-v_{n}\right)}{R_{o}}=0 \tag{5.51}
\end{equation*}
$$

Because the current in $R_{g}$ is the same as in $R_{i}$, we have

$$
\begin{equation*}
\frac{v_{p}-v_{g}}{R_{g}}=\frac{v_{n}-v_{g}}{R_{i}+R_{g}} \tag{5.52}
\end{equation*}
$$

We use Eq. 5.52 to eliminate $v_{p}$ from Eq. 5.51 , giving a pair of equations involving the unknown voltages $v_{n}$ and $v_{o}$. This algebraic manipulation leads to

$$
\begin{align*}
& v_{n}\left(\frac{1}{R_{s}}+\frac{1}{R_{g}+R_{i}}+\frac{1}{R_{f}}\right)-v_{o}\left(\frac{1}{R_{f}}\right)=v_{g}\left(\frac{1}{R_{g}+R_{i}}\right)  \tag{5.53}\\
& \quad v_{n}\left[\frac{A R_{i}}{R_{o}\left(R_{i}+R_{g}\right)}-\frac{1}{R_{f}}\right]+v_{o}\left(\frac{1}{R_{f}}+\frac{1}{R_{o}}+\frac{1}{R_{L}}\right) \\
& \quad=v_{g}\left[\frac{A R_{i}}{R_{o}\left(R_{i}+R_{g}\right)}\right] \tag{5.54}
\end{align*}
$$

Solving for $v_{o}$ yields

$$
\begin{equation*}
v_{o}=\frac{\left[\left(R_{f}+R_{s}\right)+\left(R_{s} R_{o} / A R_{i}\right)\right] v_{g}}{R_{s}+\frac{R_{o}}{A}\left(1+K_{r}\right)+\frac{R_{f} R_{s}+\left(R_{f}+R_{s}\right)\left(R_{i}+R_{g}\right)}{A R_{i}}} \tag{5.55}
\end{equation*}
$$

where

$$
K_{r}=\frac{R_{s}+R_{g}}{R_{i}}+\frac{R_{f}+R_{s}}{R_{L}}+\frac{R_{f} R_{s}+R_{f} R_{g}+R_{g} R_{s}}{R_{i} R_{L}} .
$$

Note that Eq. 5.55 reduces to Eq. 5.18 when $R_{o} \rightarrow 0, A \rightarrow \infty$, and $R_{i} \rightarrow \infty$. For the unloaded $\left(R_{L}=\infty\right)$ noninverting amplifier, Eq. 5.55 simplifies to

$$
\begin{equation*}
v_{o}=\frac{\left[\left(R_{f}+R_{s}\right)+R_{s} R_{o} / A R_{i}\right] v_{g}}{R_{s}+\frac{R_{o}}{A}\left(1+\frac{R_{s}+R_{g}}{R_{i}}\right)+\frac{1}{A R_{i}}\left[R_{f} R_{s}+\left(R_{f}+R_{s}\right)\left(R_{i}+R_{g}\right)\right]} \tag{5.56}
\end{equation*}
$$

Note that, in the derivation of Eq. 5.56 from Eq. $5.55, K_{r}$ reduces to $\left(R_{s}+R_{g}\right) / R_{i}$ 。

ASSESSMENT PROBLEM

Objective 3-Understand the more realistic model for an op amp

5.6 The inverting amplifier in the circuit shown has an input resistance of $500 \mathrm{k} \Omega$, an output resistance of $5 \mathrm{k} \Omega$, and an open-loop gain of 300,000 . Assume that the amplifier is operating in its linear region.
a) Calculate the voltage gain $\left(v_{o} / v_{g}\right)$ of the amplifier.
b) Calculate the value of $v_{n}$ in microvolts when $v_{g}=1 \mathrm{~V}$.
c) Calculate the resistance seen by the signal source ( $v_{g}$ ).
d) Repeat (a)-(c) using the ideal model for the op amp.

Answer: (a) -19.9985;
(b) $69.995 \mu \mathrm{~V}$;
(c) $5000.35 \Omega$;
(d) $-20,0 \mu \mathrm{~V}, 5 \mathrm{k} \Omega$.
image_name:Op-amp Circuit
description:
[
'name': 'vg', 'type': 'VoltageSource', 'value': 'vg', 'ports': {'Np': 'vg', 'Nn': 'GND'
'name': '5 kΩ', 'type': 'Resistor', 'value': '5 kΩ', 'ports': {'N1': 'vg', 'N2': 'InN(Ao)'
'name': '100 kΩ', 'type': 'Resistor', 'value': '100 kΩ', 'ports': {'N1': 'Vo', 'N2': 'InN(Ao)'
'name': 'Ao', 'type': 'OpAmp', 'value': 'Ao', 'ports': {'InP': 'GND', 'InN': 'InN(Ao)', 'OutP': 'Vo', 'Vdd': '20 V', '-Vdd': '-20 V'
]
extrainfo:The circuit is an inverting amplifier using an op-amp with feedback resistors. The op-amp is powered by ±20 V supplies.


NOTE: Also try Chapter Problems 5.44 and 5.48.

Practical Perspective

Strain Gages

Changes in the shape of elastic solids are of great importance to engineers who design structures that twist, stretch, or bend when subjected to external forces. An aircraft frame is a prime example of a structure in which engineers must take into consideration elastic strain. The intelligent application of strain gages requires information about the physical structure of the gage, methods of bonding the gage to the surface of the structure, and the orientation of the gage relative to the forces exerted on the structure. Our purpose here is to point out that strain gage measurements are important in engineering applications, and a knowledge of electric circuits is germane to their proper use.

The circuit shown in Fig. 5.21 provides one way to measure the change in resistance experienced by strain gages in applications like the one
image_name:Figure 5.21
description:
[
'name': 'Vref', 'type': 'VoltageSource', 'value': 'Vref', 'ports': {'Np': 'Vref', 'Nn': 'GND'
'name': 'R-ΔR', 'type': 'Resistor', 'value': 'R-ΔR', 'ports': {'N1': 'Vref', 'N2': 'InP(A0)'
'name': 'R+ΔR', 'type': 'Resistor', 'value': 'R+ΔR', 'ports': {'N1': 'InP(A0)', 'N2': 'GND'
'name': 'R+ΔR', 'type': 'Resistor', 'value': 'R+ΔR', 'ports': {'N1': 'Vref', 'N2': 'InN(A0)'
'name': 'R-ΔR', 'type': 'Resistor', 'value': 'R-ΔR', 'ports': {'N1': 'InN(A0)', 'N2': 'GND'
'name': 'A0', 'type': 'OpAmp', 'value': 'A0', 'ports': {'InP': 'InP(A0)', 'InN': 'InN(A0)', 'OutP': 'Vo','Vdd':'+VCC', '-Vdd':'-VCC'
'name': 'Rf', 'type': 'Resistor', 'value': 'Rf', 'ports': {'N1': 'Vo', 'N2': 'InN(A0)'
'name': 'Rf', 'type': 'Resistor', 'value': 'Rf', 'ports': {'N1': 'Vo', 'N2': 'GND'
]
extrainfo:The circuit is a difference amplifier used to measure the change in resistance of strain gages. It uses a Wheatstone bridge configuration to provide input voltages to the op-amp. The op-amp amplifies the difference between the voltages from the strain gage bridge.


Figure $5.21 \triangle$ An op amp circuit used for measuring the change in strain gage resistance.
described in the beginning of this chapter. As we will see, this circuit is the familiar difference amplifier, with the strain gage bridge providing the two voltages whose difference is amplified. The pair of strain gages that are lengthened once the bar is bent have the values $R+\Delta R$ in the bridge
feeding the difference amplifier, whereas the pair of strain gages that are shortened have the values $R-\Delta R$. We will analyze this circuit to discover the relationship between the output voltage, $v_{o}$ and the change in resistance, $\Delta R$ experienced by the strain gages.

To begin, assume that the op amp is ideal. Writing the KCL equations at the inverting and noninverting input terminals of the op amp we see

$$
\begin{align*}
& \frac{v_{\mathrm{ref}}-v_{n}}{R+\Delta R}=\frac{v_{n}}{R-\Delta R}+\frac{v_{n}-v_{o}}{R_{f}}  \tag{5.57}\\
& \frac{v_{\mathrm{ref}}-v_{p}}{R-\Delta R}=\frac{v_{p}}{R+\Delta R}+\frac{v_{p}}{R_{f}} \tag{5.58}
\end{align*}
$$

Now rearrange Eq. 5.58 to get an expression for the voltage at the noninverting terminal of the op amp:

$$
\begin{equation*}
v_{p}=\frac{v_{\mathrm{ref}}}{(R-\Delta R)\left(\frac{1}{R+\Delta R}+\frac{1}{R-\Delta R}+\frac{1}{R_{f}}\right)} \tag{5.59}
\end{equation*}
$$

As usual, we will assume that the op amp is operating in its linear region, so $v_{p}=v_{n}$ and the expression for $v_{p}$ in Eq. 5.59 must also be the expression for $v_{n}$. We can thus substitute the right-hand side of Eq. 5.59 in place of $v_{n}$ in Eq. 5.57 and solve for $v_{o}$. After some algebraic manipulation,

$$
\begin{equation*}
v_{o}=\frac{R_{f}(2 \Delta R)}{R^{2}-(\Delta R)^{2}} v_{\mathrm{ref}} \tag{5.60}
\end{equation*}
$$

Because the change in resistance experienced by strain gages is very small, $(\Delta R)^{2} \ll R^{2}$, so $R^{2}-(\Delta R)^{2} \approx R^{2}$ and Eq. 5.60 becomes

$$
\begin{equation*}
v_{o} \approx \frac{R_{f}}{R} 2 \delta v_{\mathrm{ref}} \tag{5.61}
\end{equation*}
$$

where $\delta=\Delta R / R$.
NOTE: Assess your understanding of this Practical Perspective by trying Chapter Problem 5.49.

## Summary

- The equation that defines the voltage transfer characteristic of an ideal op amp is
$v_{o}= \begin{cases}-V_{C C}, & A\left(v_{p}-v_{n}\right)<-V_{C C}, \\ A\left(v_{p}-v_{n}\right), & -V_{C C} \leq A\left(v_{p}-v_{n}\right) \leq+V_{C C}, \\ +V_{C C}, & A\left(v_{p}-v_{n}\right)>+V_{C C},\end{cases}$
where $A$ is a proportionality constant known as the open-loop gain, and $V_{C C}$ represents the power supply voltages. (See page 147.)
- A feedback path between an op amp's output and its inverting input can constrain the op amp to its linear operating region where $v_{o}=A\left(v_{p}-v_{n}\right)$. (See page 147.)
- A voltage constraint exists when the op amp is confined to its linear operating region due to typical values of $V_{C C}$ and $A$. If the ideal modeling assumptions are made-meaning $A$ is assumed to be infinite-the ideal op amp model is characterized by the voltage constraint

$$
v_{p}=v_{n}
$$

(See page 147.)

- A current constraint further characterizes the ideal op amp model, because the ideal input resistance of the op amp integrated circuit is infinite. This current constraint is given by

$$
i_{p}=i_{n}=0
$$

(See page 148.)

- We considered both a simple, ideal op amp model and a more realistic model in this chapter. The differences between the two models are as follows:

| Simplified Model | More Realistic Model |
| :--- | :--- |
| Infinite input resistance | Finite input resistance |
| Infinite open-loop gain | Finite open-loop gain |
| Zero output resistance | Nonzero output resistance |

(See page 159.)

- An inverting amplifier is an op amp circuit producing an output voltage that is an inverted, scaled replica of the input. (See page 150.)
- A summing amplifier is an op amp circuit producing an output voltage that is a scaled sum of the input voltages. (See page 152.)
- A noninverting amplifier is an op amp circuit producing an output voltage that is a scaled replica of the input voltage. (See page 153.)
- A difference amplifier is an op amp circuit producing an output voltage that is a scaled replica of the input voltage difference. (See page 155.)
- The two voltage inputs to a difference amplifier can be used to calculate the common mode and difference mode voltage inputs, $v_{\mathrm{cm}}$ and $v_{\mathrm{dm}}$. The output from the difference amplifier can be written in the form

$$
v_{o}=A_{\mathrm{cm}} v_{\mathrm{cm}}+A_{\mathrm{dm}} v_{\mathrm{dm}}
$$

where $A_{\mathrm{cm}}$ is the common mode gain, and $A_{\mathrm{dm}}$ is the differential mode gain. (See page 157.)

- In an ideal difference amplifier, $A_{\mathrm{cm}}=0$. To measure how nearly ideal a difference amplifier is, we use the common mode rejection ratio:

$$
\mathrm{CMRR}=\left|\frac{A_{\mathrm{dm}}}{A_{\mathrm{cm}}}\right|
$$

An ideal difference amplifier has an infinite CMRR. (See page 159.)
