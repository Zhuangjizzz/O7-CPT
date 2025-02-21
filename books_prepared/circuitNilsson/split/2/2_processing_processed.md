# 2. Circuit Elements
CHAPTER

CHAPTER CONTENTS

2.1 Voltage and Current Sources p. 26
2.2 Electrical Resistance (Ohm's Law) p. 30
2.3 Construction of a Circuit Model p. 34
2.4 Kirchhoff's Laws p. 37
2.5 Analysis of a Circuit Containing Dependent Sources p. 42

CHAPTER OBJECTIVES

1 Understand the symbols for and the behavior of the following ideal basic circuit elements: independent voltage and current sources, dependent voltage and current sources, and resistors.
2 Be able to state Ohm's law, Kirchhoff's current law, and Kirchhoff's voltage law, and be able to use these laws to analyze simple circuits.
3 Know how to calculate the power for each element in a simple circuit and be able to determine whether or not the power balances for the whole circuit.



There are five ideal basic circuit elements: voltage sources, current sources, resistors, inductors, and capacitors. In this chapter we discuss the characteristics of voltage sources, current sources, and resistors. Although this may seem like a small number of elements with which to begin analyzing circuits, many practical systems can be modeled with just sources and resistors. They are also a useful starting point because of their relative simplicity; the mathematical relationships between voltage and current in sources and resistors are algebraic. Thus you will be able to begin learning the basic techniques of circuit analysis with only algebraic manipulations.

We will postpone introducing inductors and capacitors until Chapter 6, because their use requires that you solve integral and differential equations. However, the basic analytical techniques for solving circuits with inductors and capacitors are the same as those introduced in this chapter. So, by the time you need to begin manipulating more difficult equations, you should be very familiar with the methods of writing them.

Practical Perspective

Heating with Electric Radiators

You want to heat your small garage using a couple of electric radiators. The power and voltage requirements for each radiator are $1200 \mathrm{~W}, 240 \mathrm{~V}$. But you are not sure how to wire the radiators to the power supplied to the garage. Should you use the wiring diagram on the left, or the one on the right? Does it make any difference?

Once you have studied the material in this chapter, you will be able to answer these questions and determine how to heat the garage. The Practical Perspective at the end of this chapter guides you through the analysis of two circuits based on the two wiring diagrams shown below.
image_name:Radiator
description:The image depicts a typical panel radiator, commonly used for heating in residential and commercial settings. The radiator is rectangular with vertical panels running along its length, which are designed to increase the surface area for heat dissipation. At the top right corner, there is a valve, likely a thermostatic radiator valve (TRV), which controls the flow of hot water or steam into the radiator, allowing for temperature regulation. The radiator is mounted on small legs at the bottom, providing stability and ensuring it is slightly elevated from the floor. The overall design is functional, aimed at maximizing heat output while maintaining a compact and unobtrusive appearance.

style-photography.de/fotolia


image_name:(a)
description:
[
'name': 'vs', 'type': 'VoltageSource', 'value': 'vs', 'ports': {'Np': 'N1', 'Nn': 'N2'
]
extrainfo:The diagram shows two independent sources: (a) a voltage source labeled 'vs' and (b) a current source labeled 'is'. The voltage source has a positive terminal at N1 and a negative terminal at N2. The current source has current flowing in at N3 and out at N4.
image_name:(b)
description:
[
'name': 'i_s', 'type': 'CurrentSource', 'value': 'i_s', 'ports': {'Np': 'Np', 'Nn': 'Nn'
]
extrainfo:The diagram (b) shows an ideal independent current source labeled 'i_s' with the current flowing from the top port to the bottom port.


Figure 2.1 — The circuit symbols for (a) an ideal independent voltage source and (b) an ideal independent current source.

## 2.1 Voltage and Current Sources

Before discussing ideal voltage and current sources, we need to consider the general nature of electrical sources. An electrical source is a device that is capable of converting nonelectric energy to electric energy and vice versa. A discharging battery converts chemical energy to electric energy, whereas a battery being charged converts electric energy to chemical energy. A dynamo is a machine that converts mechanical energy to electric energy and vice versa. If operating in the mechanical-to-electric mode, it is called a generator. If transforming from electric to mechanical energy, it is referred to as a motor. The important thing to remember about these sources is that they can either deliver or absorb electric power, generally maintaining either voltage or current. This behavior is of particular interest for circuit analysis and led to the creation of the ideal voltage source and the ideal current source as basic circuit elements. The challenge is to model practical sources in terms of the ideal basic circuit elements.

An ideal voltage source is a circuit element that maintains a prescribed voltage across its terminals regardless of the current flowing in those terminals. Similarly, an ideal current source is a circuit element that maintains a prescribed current through its terminals regardless of the voltage across those terminals. These circuit elements do not exist as practical devices-they are idealized models of actual voltage and current sources.

Using an ideal model for current and voltage sources places an important restriction on how we may describe them mathematically. Because an ideal voltage source provides a steady voltage, even if the current in the element changes, it is impossible to specify the current in an ideal voltage source as a function of its voltage. Likewise, if the only information you have about an ideal current source is the value of current supplied, it is impossible to determine the voltage across that current source. We have sacrificed our ability to relate voltage and current in a practical source for the simplicity of using ideal sources in circuit analysis.

Ideal voltage and current sources can be further described as either independent sources or dependent sources. An independent source establishes a voltage or current in a circuit without relying on voltages or currents elsewhere in the circuit. The value of the voltage or current supplied is specified by the value of the independent source alone. In contrast, a dependent source establishes a voltage or current whose value depends on the value of a voltage or current elsewhere in the circuit. You cannot specify the value of a dependent source unless you know the value of the voltage or current on which it depends.

The circuit symbols for the ideal independent sources are shown in Fig. 2.1. Note that a circle is used to represent an independent source. To completely specify an ideal independent voltage source in a circuit, you must include the value of the supplied voltage and the reference polarity, as shown in Fig. 2.1(a). Similarly, to completely specify an ideal independent current source, you must include the value of the supplied current and its reference direction, as shown in Fig. 2.1(b).

The circuit symbols for the ideal dependent sources are shown in Fig. 2.2. A diamond is used to represent a dependent source. Both the
dependent current source and the dependent voltage source may be controlled by either a voltage or a current elsewhere in the circuit, so there are a total of four variations, as indicated by the symbols in Fig. 2.2. Dependent sources are sometimes called controlled sources.

To completely specify an ideal dependent voltage-controlled voltage source, you must identify the controlling voltage, the equation that permits you to compute the supplied voltage from the controlling voltage, and the reference polarity for the supplied voltage. In Fig. 2.2(a), the controlling voltage is named $v_{x}$, the equation that determines the supplied voltage $v_{s}$ is

$$
v_{s}=\mu v_{x}
$$

and the reference polarity for $v_{s}$ is as indicated. Note that $\mu$ is a multiplying constant that is dimensionless.

Similar requirements exist for completely specifying the other ideal dependent sources. In Fig. 2.2(b), the controlling current is $i_{x}$, the equation for the supplied voltage $v_{s}$ is

$$
v_{s}=\rho i_{x}
$$

the reference polarity is as shown, and the multiplying constant $\rho$ has the dimension volts per ampere. In Fig. 2.2(c), the controlling voltage is $v_{x}$, the equation for the supplied current $i_{s}$ is

$$
i_{s}=\alpha v_{x}
$$

the reference direction is as shown, and the multiplying constant $\alpha$ has the dimension amperes per volt. In Fig. 2.2(d), the controlling current is $i_{x}$, the equation for the supplied current $i_{s}$ is

$$
i_{s}=\beta i_{x}
$$

the reference direction is as shown, and the multiplying constant $\beta$ is dimensionless.

Finally, in our discussion of ideal sources, we note that they are examples of active circuit elements. An active element is one that models a device capable of generating electric energy. Passive elements model physical devices that cannot generate electric energy. Resistors, inductors, and capacitors are examples of passive circuit elements. Examples 2.1 and 2.2 illustrate how the characteristics of ideal independent and dependent sources limit the types of permissible interconnections of the sources.
image_name:(a)
description:
[
'name': 'vs', 'type': 'VoltageControlledVoltageSource', 'ports': {'Np': 'N1', 'Nn': 'N2'
]
extrainfo:The circuit diagram (a) represents an ideal dependent voltage-controlled voltage source with output voltage Vs = μVx.
image_name:(b)
description:
[
'name': 'vs', 'type': 'CurrentControlledVoltageSource', 'value': 'ρix', 'ports': {'Np': 'N1', 'Nn': 'N2'
]
extrainfo:The diagram depicts an ideal dependent current-controlled voltage source with voltage Vs = ρix.
image_name:(c)
description:
[
'name': 'is', 'type': 'VoltageControlledCurrentSource', 'ports': {'Np': 'N1', 'Nn': 'N2'
]
extrainfo:The circuit diagram (c) shows an ideal dependent voltage-controlled current source where the current is proportional to a controlling voltage Vx. The relationship is given by Is = αVx.
image_name:(d)
description:
[
'name': 'is', 'type': 'CurrentControlledCurrentSource', 'value': 'βix', 'ports': {'Np': 'N1', 'Nn': 'N2'
]
extrainfo:The circuit diagram shows a current-controlled current source with current gain β, where the output current is controlled by an input current ix.


Figure 2.2 $\triangle$ The circuit symbols for (a) an ideal dependent voltage-controlled voltage source, (b) an ideal dependent current-controlled voltage source, (c) an ideal dependent voltage-controlled current source, and (d) an ideal dependent current-controlled current source.

#### Example 2.1 $\quad$ Testing Interconnections of Ideal Sources

Using the definitions of the ideal independent voltage and current sources, state which interconnections in Fig. 2.3 are permissible and which violate the constraints imposed by the ideal sources.

#### Solution

Connection (a) is valid. Each source supplies voltage across the same pair of terminals, marked a,b. This requires that each source supply the same voltage with the same polarity, which they do.

Connection (b) is valid. Each source supplies current through the same pair of terminals, marked a,b. This requires that each source supply the same current in the same direction, which they do.

Connection (c) is not permissible. Each source supplies voltage across the same pair of terminals, marked a,b. This requires that each source supply the same voltage with the same polarity, which they do not.

Connection (d) is not permissible. Each source supplies current through the same pair of terminals, marked a,b. This requires that each source supply the same current in the same direction, which they do not.

Connection (e) is valid. The voltage source supplies voltage across the pair of terminals marked a,b. The current source supplies current through the same pair of terminals. Because an ideal voltage source supplies the same voltage regardless of the current, and an ideal current source supplies the same current regardless of the voltage, this is a permissible connection.
image_name:(a)
description:
[
'name': 'V1', 'type': 'VoltageSource', 'value': '10V', 'ports': {'Np': 'a', 'Nn': 'b'
'name': 'V2', 'type': 'VoltageSource', 'value': '10V', 'ports': {'Np': 'a', 'Nn': 'b'
]
extrainfo:The circuit (a) contains two voltage sources, each supplying 10V across the same pair of terminals a and b, which is an invalid connection as both sources supply voltage across the same terminals.
image_name:(b)
description:
[
'name': 'I1', 'type': 'CurrentSource', 'value': '5A', 'ports': {'Np': 'a', 'Nn': 'b'
'name': 'I2', 'type': 'CurrentSource', 'value': '5A', 'ports': {'Np': 'b', 'Nn': 'a'
]
extrainfo:The circuit (b) contains two current sources connected to the same pair of nodes a and b, but with opposite directions. This configuration is invalid as it violates the constraint that each source should supply the same current in the same direction.
image_name:(c)
description:
[
'name': 'V3', 'type': 'VoltageSource', 'value': '10V', 'ports': {'Np': 'a', 'Nn': 'b'
'name': 'V4', 'type': 'VoltageSource', 'value': '5V', 'ports': {'Np': 'a', 'Nn': 'b'
]
extrainfo:The circuit contains two voltage sources connected in parallel between nodes a and b. V3 provides 10V and V4 provides 5V across the same nodes.
image_name:(d)
description:
[
'name': 'I4', 'type': 'CurrentSource', 'value': '2A', 'ports': {'Np': 'a', 'Nn': 'b'
'name': 'I3', 'type': 'CurrentSource', 'value': '5A', 'ports': {'Np': 'b', 'Nn': 'a'
]
extrainfo:The circuit consists of two current sources: a 5A source flowing from node b to a, and a 2A source flowing from node a to b. This configuration might be used to test current source interactions or specific network theorems.
image_name:(e)
description:
[
'name': 'V3', 'type': 'VoltageSource', 'value': '10V', 'ports': {'Np': 'a', 'Nn': 'b'
'name': 'I3', 'type': 'CurrentSource', 'value': '5A', 'ports': {'Np': 'a', 'Nn': 'b'
]
extrainfo:The circuit diagram (e) contains a voltage source V3 supplying 10V across terminals a and b, and a current source I3 supplying 5A through the same terminals. This configuration is valid as the voltage source maintains its voltage regardless of the current, and the current source maintains its current regardless of the voltage.


Figure 2.3 $\boldsymbol{\Delta}$ The circuits for Example 2.1.

#### Example 2.2 Testing Interconnections of Ideal Independent and Dependent Sources

Using the definitions of the ideal independent and dependent sources, state which interconnections in Fig. 2.4 are valid and which violate the constraints imposed by the ideal sources.

#### Solution

Connection (a) is invalid. Both the independent source and the dependent source supply voltage across the same pair of terminals, labeled a,b. This requires that each source supply the same voltage with the same polarity. The independent source supplies 5 V , but the dependent source supplies 15 V .

Connection (b) is valid. The independent voltage source supplies voltage across the pair of terminals marked a,b. The dependent current source supplies current through the same pair of terminals. Because an ideal voltage source supplies the same voltage regardless of current, and an ideal current source supplies the same current regardless of voltage, this is an allowable connection.

Connection (c) is valid. The independent current source supplies current through the pair of terminals marked a,b. The dependent voltage source supplies voltage across the same pair of terminals. Because an ideal current source supplies the same current regardless of voltage, and an ideal voltage source supplies the same voltage regardless of current, this is an allowable connection.

Connection (d) is invalid. Both the independent source and the dependent source supply current through the same pair of terminals, labeled a,b. This requires that each source supply the same current in the same reference direction. The independent source supplies 2 A , but the dependent source supplies 6 A in the opposite direction.
image_name:(a)
description:
[
'name': 'Vx', 'type': 'VoltageSource', 'value': '5V', 'ports': {'Np': 'a', 'Nn': 'b'
'name': 'Vs', 'type': 'VoltageControlledVoltageSource', 'value': 'Vs=3Vx', 'ports': {'Np': 'a', 'Nn': 'b'
]
extrainfo:The circuit contains an independent voltage source Vx with 5V and a voltage-controlled voltage source Vs with value 3 times Vx. Both sources are connected between nodes a and b.

image_name:(b)
description:
[
'name': 'Vx', 'type': 'VoltageSource', 'value': '5V', 'ports': {'Np': 'a', 'Nn': 'b'
'name': 'Is', 'type': 'VoltageControlledCurrentSource', 'value': 'Is=3Vx', 'ports': {'Np': 'b', 'Nn': 'a'
]
extrainfo:The circuit contains an independent voltage source Vx with 5V connected between nodes a and b. It also includes a voltage-controlled current source Is with a value of 3 times Vx, flowing from node b to node a.


image_name:(c)
description:
[
'name': 'Ix', 'type': 'CurrentSource', 'value': '2A', 'ports': {'Np': 'b', 'Nn': 'a'
'name': 'Vs', 'type': 'CurrentControlledVoltageSource', 'value': 'Vs=4Ix', 'ports': {'Np': 'a', 'Nn': 'b'
]
extrainfo:The circuit contains a current source Ix with 2A flowing from node a to node b. There is also a voltage-controlled voltage source Vs with a value of 4 times Ix, connected between nodes a and b.

image_name:(d)
description:
[
'name': 'Ix', 'type': 'CurrentSource', 'value': '2A', 'ports': {'Np': 'b', 'Nn': 'a'
'name': 'Is', 'type': 'CurrentControlledCurrentSource', 'ports': {'Np': 'b', 'Nn': 'a'
]
extrainfo:The circuit contains a current source Ix with 2A flowing from node a to node b. A current-controlled current source Is with a value of 3 times Ix is also present, flowing from node b to node a.


Figure 2.4 $\Delta$ The circuits for Example 2.2.

ASSESSMENT PROBLEMS

Objective 1—Understand ideal basic circuit elements

2.1 For the circuit shown,
a) What value of $v_{g}$ is required in order for the interconnection to be valid?
b) For this value of $v_{g}$, find the power associated with the 8 A source.

Answer: (a) -2 V;
(b) -16 W (16 W delivered).
image_name:Figure
description:
[
'name': 'ib/4', 'type': 'CurrentControlledVoltageSource', 'value': 'ib/4', 'ports': {'Np': 'X1', 'Nn': 'X2'
'name': 'vg', 'type': 'VoltageSource', 'value': 'vg', 'ports': {'Np': 'X1', 'Nn': 'X2'
'name': '8A', 'type': 'CurrentSource', 'value': '8A', 'ports': {'Np': 'X1', 'Nn': 'X2'
]
extrainfo:The circuit contains a current-controlled voltage source with value ib/4, a voltage source vg, and a current source of 8A. The nodes are labeled X1 and X2.


NOTE: Also try Chapter Problems 2.6 and 2.7.
2.2 For the circuit shown,
a) What value of $\alpha$ is required in order for the interconnection to be valid?
b) For the value of $\alpha$ calculated in part (a), find the power associated with the 25 V source.

Answer: (a) $0.6 \mathrm{~A} / \mathrm{V}$;
(b) $375 \mathrm{~W}(375 \mathrm{~W}$ absorbed).
image_name:Figure
description:
[
'name': '15A', 'type': 'CurrentSource', 'value': '15A', 'ports': {'Np': 'X1', 'Nn': 'X2'
'name': 'Vx', 'type': 'VoltageSource', 'value': '25V', 'ports': {'Np': 'X2', 'Nn': 'X3'
'name': 'αvx', 'type': 'VoltageControlledCurrentSource', 'value': 'αvx', 'ports': {'Np': 'X1', 'Nn': 'X3'
]
extrainfo:The circuit contains a current source of 15A between nodes X1 and X2, a voltage source of 25V between nodes X3 and X2, and a voltage-controlled current source with value αvx between nodes X1 and X3.

image_name:Figure 2.5
description:
[
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'N1', 'N2': 'N2'
]
extrainfo:The circuit diagram is a simple resistor labeled with resistance R. It has two terminals, which are not specifically labeled with node names in the diagram.


Figure 2.5 $\Delta$ The circuit symbol for a resistor having a resistance $R$.
image_name:Figure 2.6
description:
[
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'N1', 'N2': 'N2'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'N1', 'N2': 'N2'
]
extrainfo:The diagram shows two configurations of a resistor with resistance R. The left configuration follows Ohm's Law with v = iR, while the right configuration shows a reversed current direction, resulting in v = -iR.



Figure 2.6 $\triangle$ Two possible reference choices for the current and voltage at the terminals of a resistor, and the resulting equations.

## 2.2 Electrical Resistance (Ohm's Law)

Resistance is the capacity of materials to impede the flow of current or, more specifically, the flow of electric charge. The circuit element used to model this behavior is the resistor. Figure 2.5 shows the circuit symbol for the resistor, with $R$ denoting the resistance value of the resistor.

Conceptually, we can understand resistance if we think about the moving electrons that make up electric current interacting with and being resisted by the atomic structure of the material through which they are moving. In the course of these interactions, some amount of electric energy is converted to thermal energy and dissipated in the form of heat. This effect may be undesirable. However, many useful electrical devices take advantage of resistance heating, including stoves, toasters, irons, and space heaters.

Most materials exhibit measurable resistance to current. The amount of resistance depends on the material. Metals such as copper and aluminum have small values of resistance, making them good choices for wiring used to conduct electric current. In fact, when represented in a circuit diagram, copper or aluminum wiring isn't usually modeled as a resistor; the resistance of the wire is so small compared to the resistance of other elements in the circuit that we can neglect the wiring resistance to simplify the diagram.

For purposes of circuit analysis, we must reference the current in the resistor to the terminal voltage. We can do so in two ways: either in the direction of the voltage drop across the resistor or in the direction of the voltage rise across the resistor, as shown in Fig. 2.6. If we choose the former, the relationship between the voltage and current is

$$
\begin{equation*}
v=i R \tag{2.1}
\end{equation*}
$$

where

$$
\begin{aligned}
v & =\text { the voltage in volts, } \\
i & =\text { the current in amperes, } \\
R & =\text { the resistance in ohms. }
\end{aligned}
$$

If we choose the second method, we must write

$$
\begin{equation*}
v=-i R \tag{2.2}
\end{equation*}
$$

where $v, i$, and $R$ are, as before, measured in volts, amperes, and ohms, respectively. The algebraic signs used in Eqs. 2.1 and 2.2 are a direct consequence of the passive sign convention, which we introduced in Chapter 1.

Equations 2.1 and 2.2 are known as Ohm's law after Georg Simon Ohm, a German physicist who established its validity early in the nineteenth century. Ohm's law is the algebraic relationship between voltage and current for a resistor. In SI units, resistance is measured in ohms. The Greek letter omega $(\Omega)$ is the standard symbol for an ohm. The circuit diagram symbol for an $8 \Omega$ resistor is shown in Fig. 2.7.

Ohm's law expresses the voltage as a function of the current. However, expressing the current as a function of the voltage also is convenient. Thus, from Eq. 2.1,

$$
\begin{equation*}
i=\frac{v}{R} \tag{2.3}
\end{equation*}
$$

or, from Eq. 2.2,

$$
\begin{equation*}
i=-\frac{v}{R} \tag{2.4}
\end{equation*}
$$

The reciprocal of the resistance is referred to as conductance, is symbolized by the letter $G$, and is measured in siemens (S). Thus,

$$
\begin{equation*}
G=\frac{1}{R} \mathrm{~S} \tag{2.5}
\end{equation*}
$$

An $8 \Omega$ resistor has a conductance value of 0.125 S . In much of the professional literature, the unit used for conductance is the mho (ohm spelled backward), which is symbolized by an inverted omega ( $($ ). Therefore we may also describe an $8 \Omega$ resistor as having a conductance of 0.125 mho, ( $\mho$ ).

We use ideal resistors in circuit analysis to model the behavior of physical devices. Using the qualifier ideal reminds us that the resistor model makes several simplifying assumptions about the behavior of actual resistive devices. The most important of these simplifying assumptions is that the resistance of the ideal resistor is constant and its value does not vary over time. Most actual resistive devices do not have constant resistance, and their resistance does vary over time. The ideal resistor model can be used to represent a physical device whose resistance doesn't vary much from some constant value over the time period of interest in the circuit analysis. In this book we assume that the simplifying assumptions about resistance devices are valid, and we thus use ideal resistors in circuit analysis.

We may calculate the power at the terminals of a resistor in several ways. The first approach is to use the defining equation and simply calculate

Figure 2.7 $\boldsymbol{\Delta}$ The circuit symbol for an $8 \Omega$ resistor.
the product of the terminal voltage and current. For the reference systems shown in Fig. 2.6, we write

$$
\begin{equation*}
p=v i \tag{2.6}
\end{equation*}
$$

when $v=i R$ and

$$
\begin{equation*}
p=-v i \tag{2.7}
\end{equation*}
$$

when $v=-i R$.
A second method of expressing the power at the terminals of a resistor expresses power in terms of the current and the resistance. Substituting Eq. 2.1 into Eq. 2.6, we obtain

$$
p=v i=(i R) i
$$

so

Power in a resistor in terms of current $\cdot$

Power in a resistor in terms of voltage

$$
\begin{equation*}
p=i^{2} R \tag{2.8}
\end{equation*}
$$

Likewise, substituting Eq. 2.2 into Eq. 2.7, we have

$$
\begin{equation*}
p=-v i=-(-i R) i=i^{2} R \tag{2.9}
\end{equation*}
$$

Equations 2.8 and 2.9 are identical and demonstrate clearly that, regardless of voltage polarity and current direction, the power at the terminals of a resistor is positive. Therefore, a resistor absorbs power from the circuit.

A third method of expressing the power at the terminals of a resistor is in terms of the voltage and resistance. The expression is independent of the polarity references, so

$$
\begin{equation*}
p=\frac{v^{2}}{R} \tag{2.10}
\end{equation*}
$$

Sometimes a resistor's value will be expressed as a conductance rather than as a resistance. Using the relationship between resistance and conductance given in Eq. 2.5, we may also write Eqs. 2.9 and 2.10 in terms of the conductance, or

$$
\begin{align*}
p & =\frac{i^{2}}{G}  \tag{2.11}\\
p & =v^{2} G \tag{2.12}
\end{align*}
$$

Equations 2.6-2.12 provide a variety of methods for calculating the power absorbed by a resistor. Each yields the same answer. In analyzing a circuit, look at the information provided and choose the power equation that uses that information directly.

Example 2.3 illustrates the application of Ohm's law in conjunction with an ideal source and a resistor. Power calculations at the terminals of a resistor also are illustrated.

#### Example 2.3 Calculating Voltage, Current, and Power for a Simple Resistive Circuit

In each circuit in Fig. 2.8, either the value of $v$ or $i$ is not known.
image_name:(a)
description:
[
'name': '1A', 'type': 'CurrentSource', 'value': '1A', 'ports': {'Np': 'GND', 'Nn': 'VA'
'name': '8Ω', 'type': 'Resistor', 'value': '8Ω', 'ports': {'N1': 'VA', 'N2': 'GND'
]
extrainfo:The circuit consists of a 1A current source in series with an 8Ω resistor. The voltage across the resistor is labeled as va.
image_name:(b)
description:
[
'name': '50V', 'type': 'VoltageSource', 'value': '50V', 'ports': {'Np': 'VB', 'Nn': 'GND'
'name': '0.2S', 'type': 'Resistor', 'value': '0.2S', 'ports': {'Np': 'VB', 'Nn': 'VD'
]
extrainfo:The circuit (b) consists of a 50V voltage source connected in series with a 0.2S Resistor. The nodes VB and VD are connected to the positive and negative terminals of the voltage source, respectively.
image_name:(c)
description:
[
'name': '1A', 'type': 'CurrentSource', 'value': '1A', 'ports': {'Np': 'VC', 'Nn': 'GND'
'name': '20Ω', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'VC', 'N2': 'GND'
]
extrainfo:The circuit diagram (c) consists of a current source and a resistor in series, and a voltage source and a resistor in parallel.
image_name:(d)
description:
[
'name': '50V', 'type': 'VoltageSource', 'value': '50 V', 'ports': {'Np': 'Vd', 'Nn': 'GND'
'name': '25 Ω', 'type': 'Resistor', 'value': '25 Ω', 'ports': {'N1': 'Vd', 'N2': 'GND'
]
extrainfo:The circuit diagram (d) consists of a 50 V voltage source and a 25 Ω resistor connected in parallel between node Vd and ground (GND). The current id flows from the ground to node Vd through the resistor.


Figure $2.8 \boldsymbol{\Delta}$ The circuits for Example 2.3.
a) Calculate the values of $v$ and $i$.
b) Determine the power dissipated in each resistor.

#### Solution

a) The voltage $v_{a}$ in Fig. 2.8(a) is a drop in the direction of the current in the resistor. Therefore,

$$
v_{\mathrm{a}}=(1)(8)=8 \mathrm{~V}
$$

The current $i_{b}$ in the resistor with a conductance of 0.2 S in Fig. 2.8(b) is in the direction of the voltage drop across the resistor. Thus

$$
i_{\mathrm{b}}=(50)(0.2)=10 \mathrm{~A}
$$

The voltage $v_{c}$ in Fig. 2.8(c) is a rise in the direction of the current in the resistor. Hence

$$
v_{\mathrm{c}}=-(1)(20)=-20 \mathrm{~V}
$$

The current $i_{\mathrm{d}}$ in the $25 \Omega$ resistor in Fig. 2.8(d) is in the direction of the voltage rise across the resistor. Therefore

$$
i_{\mathrm{d}}=\frac{-50}{25}=-2 \mathrm{~A}
$$

b) The power dissipated in each of the four resistors is

$$
\begin{aligned}
p_{8 \Omega} & =\frac{(8)^{2}}{8}=(1)^{2}(8)=8 \mathrm{~W} \\
p_{0.2 S} & =(50)^{2}(0.2)=500 \mathrm{~W} \\
p_{20 \Omega} & =\frac{(-20)^{2}}{20}=(1)^{2}(20)=20 \mathrm{~W} \\
p_{25 \Omega} & =\frac{(50)^{2}}{25}=(-2)^{2}(25)=100 \mathrm{~W}
\end{aligned}
$$

ASSESSMENT PROBLEMS

Objective 2—Be able to state and use Ohm's Law . . .

2.3 For the circuit shown,
a) If $v_{g}=1 \mathrm{kV}$ and $i_{g}=5 \mathrm{~mA}$, find the value of $R$ and the power absorbed by the resistor.
b) If $i_{g}=75 \mathrm{~mA}$ and the power delivered by the voltage source is 3 W , find $v_{g}, R$, and the power absorbed by the resistor.
c) If $R=300 \Omega$ and the power absorbed by $R$ is 480 mW , find $i_{g}$ and $v_{g}$.
image_name:For the circuit shown
description:
[
'name': 'vg', 'type': 'VoltageSource', 'value': 'vg', 'ports': {'Np': 'Vg', 'Nn': 'GND'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'Vg', 'N2': 'GND'
]
extrainfo:The circuit consists of a voltage source 'vg' and a resistor 'R' connected in parallel, with a current 'ig' flowing through the circuit.


Answer: (a) $200 \mathrm{k} \Omega, 5 \mathrm{~W}$;
(b) $40 \mathrm{~V}, 533.33 \Omega, 3 \mathrm{~W}$;
(c) $40 \mathrm{~mA}, 12 \mathrm{~V}$.

NOTE: Also try Chapter Problems 2.11 and 2.12.
2.4 For the circuit shown,
a) If $i_{g}=0.5 \mathrm{~A}$ and $G=50 \mathrm{mS}$, find $v_{g}$ and the power delivered by the current source.
b) If $v_{g}=15 \mathrm{~V}$ and the power delivered to the conductor is 9 W , find the conductance $G$ and the source current $i_{g}$.
c) If $G=200 \mu \mathrm{~S}$ and the power delivered to the conductance is 8 W , find $i_{g}$ and $v_{g}$.
image_name:figure
description:
[
'name': 'ig', 'type': 'CurrentSource', 'value': 'ig', 'ports': {'Np': 'GND', 'Nn': 'Vg'
'name': 'G', 'type': 'Resistor', 'value': 'G', 'ports': {'N1': 'Vg', 'N2': 'GND'
]
extrainfo:The circuit consists of a current source 'ig' connected in parallel with a resistor 'G'. The current source flows from ground to node Vg, and the resistor is connected between node Vg and ground. The voltage across the resistor is denoted as 'vg'.


Answer: (a) $10 \mathrm{~V}, 5 \mathrm{~W}$;
(b) $40 \mathrm{mS}, 0.6 \mathrm{~A}$;
(c) $40 \mathrm{~mA}, 200 \mathrm{~V}$.

Having introduced the general characteristics of ideal sources and resistors, we next show how to use these elements to build the circuit model of a practical system.

## 2.3 Construction of a Circuit Model

We have already stated that one reason for an interest in the basic circuit elements is that they can be used to construct circuit models of practical systems. The skill required to develop a circuit model of a device or system is as complex as the skill required to solve the derived circuit. Although this text emphasizes the skills required to solve circuits, you also will need other skills in the practice of electrical engineering, and one of the most important is modeling.

We develop circuit models in the next two examples. In Example 2.4 we construct a circuit model based on a knowledge of the behavior of the system's components and how the components are interconnected. In Example 2.5 we create a circuit model by measuring the terminal behavior of a device.

#### Example 2.4 Constructing a Circuit Model of a Flashlight

Construct a circuit model of a flashlight.

#### Solution

We chose the flashlight to illustrate a practical system because its components are so familiar. Figure 2.9 shows a photograph of a widely available flashlight.

When a flashlight is regarded as an electrical system, the components of primary interest are the batteries, the lamp, the connector, the case, and the switch. We now consider the circuit model for each component.

A dry-cell battery maintains a reasonably constant terminal voltage if the current demand is not excessive. Thus if the dry-cell battery is operating within its intended limits, we can model it with an ideal voltage source. The prescribed voltage then is constant and equal to the sum of two dry-cell values.

The ultimate output of the lamp is light energy, which is achieved by heating the filament in the lamp to a temperature high enough to cause radiation in the visible range. We can model the lamp with an ideal resistor. Note in this case that although the resistor accounts for the amount of electric energy converted to thermal energy, it does not predict how much of the thermal energy is converted to light energy. The resistor used to represent the lamp does predict the steady current drain on the batteries, a characteristic of the system that also is of interest. In this model, $R_{l}$ symbolizes the lamp resistance.

The connector used in the flashlight serves a dual role. First, it provides an electrical conductive path between the dry cells and the case. Second, it is
image_name:Figure 2.9 A
description:The image depicts a flashlight, highlighting its functional components and structure. The flashlight is shown with a metallic, cylindrical body, which is likely made of aluminum or a similar material for durability and lightweight properties. The head of the flashlight is prominent in the image, featuring a transparent lens through which a bright light is emitted. This light is depicted with a warm, orange hue, indicating the operational state of the flashlight.

1. **Identification of Components and Structure:**
- The flashlight consists of a cylindrical body, a head with a lens, and a light source inside.
- The body appears to have a textured grip, likely to prevent slipping and ensure ease of handling.
- The head of the flashlight is slightly wider than the body, which is typical for housing the light bulb and reflector.

2. **Connections and Interactions:**
- The light source inside the flashlight is powered by batteries housed within the cylindrical body.
- Electrical connections are made internally, likely involving a switch mechanism on the body (not visible in this image) to control the on/off state.
- The reflector inside the head focuses the light into a beam, as evidenced by the focused light emitted from the lens.

3. **Labels, Annotations, and Key Features:**
- The image does not contain any visible labels or annotations.
- The focus is on the emitted light and the design of the flashlight, emphasizing its role as an effective light-emitting device.
- The image captures the essence of the flashlight as an electrical system, converting electrical energy from the batteries into light energy effectively.


Figure 2.9 A A flashlight can be viewed as an electrical system.
formed into a springy coil so that it also can apply mechanical pressure to the contact between the batteries and the lamp. The purpose of this mechanical pressure is to maintain contact between the two dry cells and between the dry cells and the lamp. Hence, in choosing the wire for the connector, we may find that its mechanical properties are more
important than its electrical properties for the flashlight design. Electrically, we can model the connector with an ideal resistor, labeled $R_{1}$.

The case also serves both a mechanical and an electrical purpose. Mechanically, it contains all the other components and provides a grip for the person using it. Electrically, it provides a connection between other elements in the flashlight. If the case is metal, it conducts current between the batteries and the lamp. If it is plastic, a metal strip inside the case connects the coiled connector to the switch. Either way, an ideal resistor, which we denote $R_{c}$, models the electrical connection provided by the case.

The final component is the switch. Electrically, the switch is a two-state device. It is either on or OFF. An ideal switch offers no resistance to the current when it is in the on state, but it offers infinite resistance to current when it is in the OFF state. These two states represent the limiting values of a resistor; that is, the on state corresponds to a resistor with a numerical value of zero, and the off state corresponds to a resistor with a numerical value of infinity. The two extreme values have the descriptive names short circuit $(R=0)$ and open circuit ( $R=\infty$ ). Figure 2.10(a) and (b) show the graphical representation of a short circuit and an open circuit, respectively. The symbol shown in Fig. 2.10(c) represents the fact that a switch can be either a short circuit or an open circuit, depending on the position of its contacts.

We now construct the circuit model of the flashlight. Starting with the dry-cell batteries, the positive terminal of the first cell is connected to the negative terminal of the second cell, as shown in Fig. 2.11. The positive terminal of the second cell is connected to one terminal of the lamp. The other terminal of the lamp makes contact with one side of the switch, and the other side of the switch is connected to the metal case. The metal case is then connected to the negative terminal of the first dry cell by means of the metal spring. Note that the elements form a closed path or circuit. You can see the closed path formed by the connected elements in Fig. 2.11. Figure 2.12 shows a circuit model for the flashlight.
image_name:(a)
description:The diagram shows three basic circuit symbols: (a) a wire, (b) an open circuit, and (c) a switch with positions for ON and OFF.
image_name:(b)
description:The diagram represents a simple switch in an open state. This is a basic component often used to control the flow of electricity in a circuit.
image_name:(c)
description:The diagram represents a switch with positions labeled OFF and ON.


Figure $2.10 \boldsymbol{\Delta}$ Circuit symbols. (a) Short circuit. (b) Open circuit. (c) Switch.
image_name:Figure 2.11
description:The image illustrates the internal arrangement of a flashlight. It provides a cross-sectional view of the flashlight's components and their connections. The main components identified in the diagram are:

1. **Lamp**: Positioned at the top of the flashlight, the lamp is the light-emitting element. It is connected to the circuit via a filament terminal.

2. **Filament Terminal**: This is the connection point for the lamp, ensuring it receives electrical power from the battery cells.

3. **Sliding Switch**: Located on the side of the flashlight, the sliding switch controls the flow of electricity to the lamp. By sliding the switch, the circuit is either completed or broken, turning the lamp on or off.

4. **Dry Cells**: Two dry cells, labeled as Dry Cell #1 and Dry Cell #2, are stacked vertically within the flashlight. These cells provide the necessary power for the lamp. Each cell is marked with positive and negative terminals, indicating the direction of current flow.

5. **Case**: The outer casing of the flashlight holds all the components together and provides structural integrity.

Connections and Interactions:
- The dry cells are connected in series, meaning the positive terminal of Dry Cell #1 is connected to the negative terminal of Dry Cell #2. This series connection increases the total voltage supplied to the lamp.
- The sliding switch acts as a control mechanism to open or close the circuit, allowing current to flow from the dry cells to the lamp when the circuit is closed.

Labels and Annotations:
- The diagram includes clear labels for each component, such as "Lamp," "Filament terminal," "Sliding switch," "Dry cell #1," "Dry cell #2," and "Case," aiding in the understanding of the flashlight's internal structure and function.

Overall, the image effectively demonstrates the basic electrical circuit within a flashlight, highlighting how the components interact to produce light.


Figure $2.11 \boldsymbol{\Delta}$ The arrangement of flashlight components.
image_name:Figure 2.12 △ A circuit model for a flashlight
description:
[
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': 'Vs', 'Nn': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'GND', 'N2': 'X1'
'name': 'Rc', 'type': 'Resistor', 'value': 'Rc', 'ports': {'N1': 'X1', 'N2': 'X2'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'X2', 'N2': 'X3'
'name': 'Rl', 'type': 'Resistor', 'value': 'Rl', 'ports': {'N1': 'X3', 'N2': 'Vs'
]
extrainfo:The circuit represents a simple model of a flashlight with a voltage source, resistors, and a switch. The switch controls the current flow through the resistors, simulating the flashlight's on/off functionality.


Figure $2.12 \triangle \mathrm{~A}$ circuit model for a flashlight.

We can make some general observations about modeling from our flashlight example: First, in developing a circuit model, the electrical behavior of each physical component is of primary interest. In the flashlight model, three very different physical components - a lamp, a coiled wire, and a metal case-are all represented by the same circuit element (a resistor), because the electrical phenomenon taking place in each is the same. Each is presenting resistance to the current flowing through the circuit.

Second, circuit models may need to account for undesired as well as desired electrical effects. For example, the heat resulting from the resistance in the lamp produces the light, a desired effect. However, the heat
resulting from the resistance in the case and coil represents an unwanted or parasitic effect. It drains the dry cells and produces no useful output. Such parasitic effects must be considered or the resulting model may not adequately represent the system.

And finally, modeling requires approximation. Even for the basic system represented by the flashlight, we made simplifying assumptions in developing the circuit model. For example, we assumed an ideal switch, but in practical switches, contact resistance may be high enough to interfere with proper operation of the system. Our model does not predict this behavior. We also assumed that the coiled connector exerts enough pressure to eliminate any contact resistance between the dry cells. Our model does not predict the effect of inadequate pressure. Our use of an ideal voltage source ignores any internal dissipation of energy in the dry cells, which might be due to the parasitic heating just mentioned. We could account for this by adding an ideal resistor between the source and the lamp resistor. Our model assumes the internal loss to be negligible.

In modeling the flashlight as a circuit, we had a basic understanding of and access to the internal components of the system. However, sometimes we know only the terminal behavior of a device and must use this information in constructing the model. Example 2.5 explores such a modeling problem.

#### Example 2.5 Constructing a Circuit Model Based on Terminal Measurements

The voltage and current are measured at the terminals of the device illustrated in Fig. 2.13(a), and the values of $v_{t}$ and $i_{t}$ are tabulated in Fig. 2.13(b). Construct a circuit model of the device inside the box.
image_name:Fig. 2.13(a)
description:Fig. 2.13(a) depicts a simple schematic of a device enclosed within a box, connected to external circuitry. The diagram shows two terminals labeled with voltage ($v_t$) and current ($i_t$) indicators. The voltage is denoted by $v_t$ with a positive (+) and negative (-) sign, indicating the direction of potential difference across the device. The current $i_t$ is shown with an arrow pointing into the device, signifying the direction of current flow. This setup suggests a two-terminal device where voltage and current can be measured.

Fig. 2.13(b) presents a table with measured values of terminal voltage ($v_t$) and terminal current ($i_t$). The table lists five pairs of values: \(-40 \text{ V}, -10 \text{ A}\), \(-20 \text{ V}, -5 \text{ A}\), \(0 \text{ V}, 0 \text{ A}\), \(20 \text{ V}, 5 \text{ A}\), and \(40 \text{ V}, 10 \text{ A}\). These values indicate a linear relationship between voltage and current, suggesting that the device behaves like a resistor.

Overall, the illustration and data imply that the device can be modeled as a linear resistor, as confirmed by the proportional relationship between voltage and current. The device's behavior is consistent with Ohm's law, implying a resistance of \(4 \Omega\).
image_name:Fig. 2.13(b)
description:The image consists of two parts: (a) a diagram and (b) a table.

In part (a), there is a schematic representation of a device with two terminals. The device is shown as a box labeled 'Device,' with a positive voltage $v_t$ marked on one side and a negative voltage on the opposite side. An arrow labeled $i_t$ indicates the direction of current flow into the device.

Part (b) is a table with two columns. The left column is labeled $v_t$ (V) for voltage in volts, and the right column is labeled $i_t$ (A) for current in amperes. The table presents pairs of voltage and current measurements as follows:
- $v_t = -40$ V, $i_t = -10$ A
- $v_t = -20$ V, $i_t = -5$ A
- $v_t = 0$ V, $i_t = 0$ A
- $v_t = 20$ V, $i_t = 5$ A
- $v_t = 40$ V, $i_t = 10$ A

These measurements suggest a linear relationship between the terminal voltage and current of the device.


#### Solution

Plotting the voltage as a function of the current yields the graph shown in Fig. 2.14(a). The equation of the line in this figure illustrates that the terminal voltage is directly proportional to the terminal current, $v_{t}=4 i_{t}$. In terms of Ohm's law, the device inside the box behaves like a $4 \Omega$ resistor. Therefore, the circuit model for the device inside the box is a $4 \Omega$ resistor, as seen in Fig. 2.14(b).

We come back to this technique of using terminal characteristics to construct a circuit model after introducing Kirchhoff's laws and circuit analysis.

Figure 2.13 $\Delta$ The (a) device and (b) data for Example 2.5.
image_name:(a)
description:The graph in Figure 2.14(a) is a linear plot depicting the relationship between terminal voltage \( v_t \) and terminal current \( i_t \) for a device. The x-axis represents the terminal current \( i_t \) in amperes (A), ranging from \(-10\) to \(10\) A, while the y-axis represents the terminal voltage \( v_t \) in volts (V), ranging from \(-40\) to \(40\) V.

The graph is a straight line passing through the origin, indicating a direct proportionality between \( v_t \) and \( i_t \). The slope of the line is \(4\), corresponding to the resistance of the device, as given by Ohm's law \( v_t = 4i_t \). This implies that for every 1 ampere increase in \( i_t \), \( v_t \) increases by 4 volts.

Key features of the graph include:
- The line passes through points \((-10, -40)\), \((-5, -20)\), \((5, 20)\), and \((10, 40)\), confirming the consistent slope.
- The graph is symmetric about the origin, indicating that the proportionality holds for both positive and negative values of \( i_t \) and \( v_t \).

This linear relationship confirms that the device behaves like a \(4 \Omega\) resistor, as mentioned in the context.
image_name:(b)
description:
[
'name': '4Ω', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'VtP', 'N2': 'VtN'
]
extrainfo:The circuit diagram represents a 4Ω resistor model for the device, with terminal voltage Vt and current It. The voltage Vt is directly proportional to the current It, behaving like a 4Ω resistor.


Figure $2.14 \boldsymbol{\Delta}$ (a) The values of $v_{t}$ versus $i_{t}$ for the device in Fig. 2.13. (b) The circuit model for the device in Fig. 2.13.

NOTE: Assess your understanding of this example by trying Chapter Problems 2.14 and 2.15.

## 2.4 Kirchhoff's Laws

A circuit is said to be solved when the voltage across and the current in every element have been determined. Ohm's law is an important equation for deriving such solutions. However, Ohm's law may not be enough to provide a complete solution. As we shall see in trying to solve the flashlight circuit from Example 2.4, we need to use two more important algebraic relationships, known as Kirchhoff's laws, to solve most circuits.

We begin by redrawing the circuit as shown in Fig. 2.15, with the switch in the on state. Note that we have also labeled the current and voltage variables associated with each resistor and the current associated with the voltage source. Labeling includes reference polarities, as always. For convenience, we attach the same subscript to the voltage and current labels as we do to the resistor labels. In Fig. 2.15, we also removed some of the terminal dots of Fig. 2.12 and have inserted nodes. Terminal dots are the start and end points of an individual circuit element. A node is a point where two or more circuit elements meet. It is necessary to identify nodes in order to use Kirchhoff's current law, as we will see in a moment. In Fig. 2.15, the nodes are labeled a, b, c, and d. Node d connects the battery and the lamp and in essence stretches all the way across the top of the diagram, though we label a single point for convenience. The dots on either side of the switch indicate its terminals, but only one is needed to represent a node, so only one is labeled node c.

For the circuit shown in Fig. 2.15, we can identify seven unknowns: $i_{s}, i_{1}, i_{c}, i_{l}, v_{1}, v_{c}$, and $v_{l}$. Recall that $v_{s}$ is a known voltage, as it represents the sum of the terminal voltages of the two dry cells, a constant voltage of 3 V . The problem is to find the seven unknown variables. From algebra, you know that to find $n$ unknown quantities you must solve $n$ simultaneous independent equations. From our discussion of Ohm's law in Section 2.2, you know that three of the necessary equations are

$$
\begin{gather*}
v_{1}=i_{1} R_{1}  \tag{2.13}\\
v_{c}=i_{c} R_{c}  \tag{2.14}\\
v_{l}=i_{l} R_{l} \tag{2.15}
\end{gather*}
$$

What about the other four equations?
The interconnection of circuit elements imposes constraints on the relationship between the terminal voltages and currents. These constraints are referred to as Kirchhoff's laws, after Gustav Kirchhoff, who first stated them in a paper published in 1848. The two laws that state the constraints in mathematical form are known as Kirchhoff's current law and Kirchhoff's voltage law.

We can now state Kirchhoff's current law:

The algebraic sum of all the currents at any node in a circuit equals zero.

To use Kirchhoff's current law, an algebraic sign corresponding to a reference direction must be assigned to every current at the node. Assigning a positive sign to a current leaving a node requires assigning a negative sign to a current entering a node. Conversely, giving a negative sign to a current leaving a node requires giving a positive sign to a current entering a node.
image_name:Figure 2.15
description:
[
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': 'd', 'Nn': 'a'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'Rc', 'type': 'Resistor', 'value': 'Rc', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'Rl', 'type': 'Resistor', 'value': 'Rl', 'ports': {'N1': 'd', 'N2': 'c'
]
extrainfo:The circuit is a simple series circuit with a voltage source and three resistors. The nodes are labeled a, b, c, and d. Currents and voltages are assigned across each component.


Figure 2.15 $\triangle$ Circuit model of the flashlight with assigned voltage and current variables.

Kirchhoff's current law (KCL)

Kirchhoff's voltage law (KVL)

Applying Kirchhoff's current law to the four nodes in the circuit shown in Fig. 2.15, using the convention that currents leaving a node are considered positive, yields four equations:

$$
\begin{array}{cc}
\text { node } \mathrm{a} & i_{s}-i_{1}=0, \\
\text { node } \mathrm{b} & i_{1}+i_{c}=0, \\
\text { node } \mathrm{c} & -i_{c}-i_{l}=0 \\
\text { node } \mathrm{d} & i_{l}-i_{s}=0 \tag{2.19}
\end{array}
$$

Note that Eqs. 2.16-2.19 are not an independent set, because any one of the four can be derived from the other three. In any circuit with $n$ nodes, $n-1$ independent current equations can be derived from Kirchhoff's current law. ${ }^{1}$ Let's disregard Eq. 2.19 so that we have six independent equations, namely, Eqs. 2.13-2.18. We need one more, which we can derive from Kirchhoff's voltage law.

Before we can state Kirchhoff's voltage law, we must define a closed path or loop. Starting at an arbitrarily selected node, we trace a closed path in a circuit through selected basic circuit elements and return to the original node without passing through any intermediate node more than once. The circuit shown in Fig. 2.15 has only one closed path or loop. For example, choosing node a as the starting point and tracing the circuit clockwise, we form the closed path by moving through nodes $\mathrm{d}, \mathrm{c}, \mathrm{b}$, and back to node a. We can now state Kirchhoff's voltage law:

The algebraic sum of all the voltages around any closed path in a circuit equals zero.

To use Kirchhoff's voltage law, we must assign an algebraic sign (reference direction) to each voltage in the loop. As we trace a closed path, a voltage will appear either as a rise or a drop in the tracing direction. Assigning a positive sign to a voltage rise requires assigning a negative sign to a voltage drop. Conversely, giving a negative sign to a voltage rise requires giving a positive sign to a voltage drop.

We now apply Kirchhoff's voltage law to the circuit shown in Fig. 2.15. We elect to trace the closed path clockwise, assigning a positive algebraic sign to voltage drops. Starting at node d leads to the expression

$$
\begin{equation*}
v_{l}-v_{c}+v_{1}-v_{s}=0 \tag{2.20}
\end{equation*}
$$

which represents the seventh independent equation needed to find the seven unknown circuit variables mentioned earlier.

The thought of having to solve seven simultaneous equations to find the current delivered by a pair of dry cells to a flashlight lamp is not very appealing. Thus in the coming chapters we introduce you to analytical techniques that will enable you to solve a simple one-loop circuit by writing a single equation. However, before moving on to a discussion of these circuit techniques, we need to make several observations about the detailed analysis of the flashlight circuit. In general, these observations are true and therefore are important to the discussions in subsequent chapters. They also support the contention that the flashlight circuit can be solved by defining a single unknown.

[^0]First, note that if you know the current in a resistor, you also know the voltage across the resistor, because current and voltage are directly related through Ohm's law. Thus you can associate one unknown variable with each resistor, either the current or the voltage. Choose, say, the current as the unknown variable. Then, once you solve for the unknown current in the resistor, you can find the voltage across the resistor. In general, if you know the current in a passive element, you can find the voltage across it, greatly reducing the number of simultaneous equations to be solved. For example, in the flashlight circuit, we eliminate the voltages $v_{c}$, $v_{l}$, and $v_{1}$ as unknowns. Thus at the outset we reduce the analytical task to solving four simultaneous equations rather than seven.

The second general observation relates to the consequences of connecting only two elements to form a node. According to Kirchhoff's current law, when only two elements connect to a node, if you know the current in one of the elements, you also know it in the second element. In other words, you need define only one unknown current for the two elements. When just two elements connect at a single node, the elements are said to be in series. The importance of this second observation is obvious when you note that each node in the circuit shown in Fig. 2.15 involves only two elements. Thus you need to define only one unknown current. The reason is that Eqs. 2.16-2.18 lead directly to

$$
\begin{equation*}
i_{s}=i_{1}=-i_{c}=i_{l} \tag{2.21}
\end{equation*}
$$

which states that if you know any one of the element currents, you know them all. For example, choosing to use $i_{s}$ as the unknown eliminates $i_{1}, i_{c}$, and $i_{l}$. The problem is reduced to determining one unknown, namely, $i_{s}$.

Examples 2.6 and 2.7 illustrate how to write circuit equations based on Kirchhoff's laws. Example 2.8 illustrates how to use Kirchhoff's laws and Ohm's law to find an unknown current. Example 2.9 expands on the technique presented in Example 2.5 for constructing a circuit model for a device whose terminal characteristics are known.

#### Example 2.6 Using Kirchhoff's Current Law

Sum the currents at each node in the circuit shown in Fig. 2.16. Note that there is no connection $\operatorname{dot}(\bullet)$ in the center of the diagram, where the $4 \Omega$ branch crosses the branch containing the ideal current source $i_{\mathrm{a}}$.

#### Solution

In writing the equations, we use a positive sign for a current leaving a node. The four equations are
node a $\quad i_{1}+i_{4}-i_{2}-i_{5}=0$,
image_name:Figure 2.16
description:
[
'name': '1Ω', 'type': 'Resistor', 'value': '1Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '2Ω', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'b', 'N2': 'a'
'name': '3Ω', 'type': 'Resistor', 'value': '3Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': '4Ω', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': '5Ω', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'a', 'N2': 'd'
'name': 'Ia', 'type': 'CurrentSource', 'ports': {'Np': 'd', 'Nn': 'b'
'name': 'Ib', 'type': 'CurrentSource', 'ports': {'Np': 'c', 'Nn': 'b'
'name': 'Ic', 'type': 'CurrentSource', 'ports': {'Np': 'd', 'Nn': 'c'
]
extrainfo:The circuit is a mesh network with resistors forming loops between nodes a, b, c, and d. There are three current sources present, influencing the current distribution in the circuit.


Figure 2.16 $\triangle$ The circuit for Example 2.6.
node $\mathrm{b} i_{2}+i_{3}-i_{1}-i_{\mathrm{b}}-i_{\mathrm{a}}=0$,
node $\mathrm{c} \quad i_{\mathrm{b}}-i_{3}-i_{4}-i_{\mathrm{c}}=0$,
node d

$$
i_{5}+i_{\mathrm{a}}+\mathrm{i}_{\mathrm{c}}=0
$$

#### Example 2.7 Using Kirchhoff's Voltage Law

Sum the voltages around each designated path in the circuit shown in Fig. 2.17.

#### Solution

In writing the equations, we use a positive sign for a voltage drop. The four equations are

$$
\begin{array}{lr}
\text { path a } & -v_{1}+v_{2}+v_{4}-v_{\mathrm{b}}-v_{3}=0 \\
\text { path } \mathrm{b} & -v_{\mathrm{a}}+v_{3}+v_{5}=0 \\
\text { path c } & v_{\mathrm{b}}-v_{4}-v_{\mathrm{c}}-v_{6}-v_{5}=0 \\
\text { path d } & -v_{\mathrm{a}}-v_{1}+v_{2}-v_{\mathrm{c}}+v_{7}-v_{\mathrm{d}}=0
\end{array}
$$

image_name:Figure 2.17
description:
[
'name': '1Ω', 'type': 'Resistor', 'value': '1Ω', 'ports': {'N1': 'va1', 'N2': 'x1'
'name': '2Ω', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'x1', 'N2': 'vc2'
'name': '3Ω', 'type': 'Resistor', 'value': '3Ω', 'ports': {'N1': 'va1', 'N2': 'vb1'
'name': '4Ω', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'vb2', 'N2': 'vc2'
'name': '5Ω', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'va2', 'N2': 'vb1'
'name': '6Ω', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'vc1', 'N2': 'va2'
'name': '7Ω', 'type': 'Resistor', 'value': '7Ω', 'ports': {'N1': 'vd2', 'N2': 'vc1'
'name': 'va', 'type': 'VoltageSource', 'value': 'va', 'ports': {'Np': 'va1', 'Nn': 'va2'
'name': 'vb', 'type': 'VoltageSource', 'value': 'vb', 'ports': {'Np': 'vb1', 'Nn': 'vb2'
'name': 'vc', 'type': 'VoltageSource', 'value': 'vc', 'ports': {'Np': 'vc1', 'Nn': 'vc2'
'name': 'vd', 'type': 'VoltageSource', 'value': 'vd', 'ports': {'Np': 'va2', 'Nn': 'vd2'
]
extrainfo:The circuit contains four voltage sources and seven resistors. The paths a, b, c, and d are used to form loop equations to analyze the circuit using Kirchhoff's laws. Each path has a corresponding voltage equation that sums to zero, indicating the conservation of energy around the loop.


Figure 2.17 The circuit for Example 2.7.

#### Example 2.8 Applying Ohm's Law and Kirchhoff's Laws to Find an Unknown Current

a) Use Kirchhoff's laws and Ohm's law to find $i_{o}$ in the circuit shown in Fig. 2.18.
image_name:Figure 2.18
description:
[
'name': '120V', 'type': 'VoltageSource', 'value': '120V', 'ports': {'Np': 'c', 'Nn': 'b'
'name': '10Ω', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'c', 'N2': 'a'
'name': '50Ω', 'type': 'Resistor', 'value': '50Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '6A', 'type': 'CurrentSource', 'value': '6A', 'ports': {'Np': 'b', 'Nn': 'a'
]
extrainfo:The circuit consists of a voltage source of 120V, a 10Ω resistor, a 50Ω resistor, and a 6A current source. The nodes are labeled a, b, and c. The current io flows through the 10Ω resistor from node c to node a.


Figure 2.18 ■ The circuit for Example 2.8.
b) Test the solution for $i_{o}$ by verifying that the total power generated equals the total power dissipated.

#### Solution

a) We begin by redrawing the circuit and assigning an unknown current to the $50 \Omega$ resistor and unknown voltages across the $10 \Omega$ and $50 \Omega$ resistors. Figure 2.19 shows the circuit. The nodes are labeled $\mathrm{a}, \mathrm{b}$, and c to aid the discussion.
image_name:Figure 2.19
description:
[
'name': '120V', 'type': 'VoltageSource', 'value': '120V', 'ports': {'Np': 'a', 'Nn': 'c'
'name': '10Ω', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '50Ω', 'type': 'Resistor', 'value': '50Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': '6A', 'type': 'CurrentSource', 'value': '6A', 'ports': {'Np': 'c', 'Nn': 'b'
]
extrainfo:The circuit includes a 120V voltage source between nodes a and c, a 10Ω resistor between nodes a and b, a 50Ω resistor between nodes b and c, and a 6A current source from node b to node c. The circuit is analyzed by defining unknowns i1, vo, and v1, and applying Kirchhoff's current law at node b.


Figure 2.19 $\Delta$ The circuit shown in Fig. 2.18, with the unknowns $i_{1}, v_{o}$, and $v_{1}$ defined.

Because $i_{o}$ also is the current in the 120 V source, we have two unknown currents and
therefore must derive two simultaneous equations involving $i_{o}$ and $i_{1}$. We obtain one of the equations by applying Kirchhoff's current law to either node b or c . Summing the currents at node b and assigning a positive sign to the currents leaving the node gives

$$
i_{1}-i_{o}-6=0
$$

We obtain the second equation from Kirchhoff's voltage law in combination with Ohm's law. Noting from Ohm's law that $v_{o}$ is $10 i_{o}$ and $v_{1}$ is $50 i_{1}$, we sum the voltages around the closed path cabc to obtain

$$
-120+10 i_{o}+50 i_{1}=0
$$

In writing this equation, we assigned a positive sign to voltage drops in the clockwise direction. Solving these two equations for $i_{o}$ and $i_{1}$ yields

$$
i_{o}=-3 \mathrm{~A} \quad \text { and } \quad i_{1}=3 \mathrm{~A} .
$$

b) The power dissipated in the $50 \Omega$ resistor is

$$
p_{50 \Omega}=(3)^{2}(50)=450 \mathrm{~W}
$$

The power dissipated in the $10 \Omega$ resistor is

$$
p_{10 \Omega}=(-3)^{2}(10)=90 \mathrm{~W}
$$

The power delivered to the 120 V source is

$$
p_{120 \mathrm{~V}}=-120 i_{o}=-120(-3)=360 \mathrm{~W}
$$

The power delivered to the 6 A source is
$p_{6 \mathrm{~A}}=-v_{1}(6)$, but $\quad v_{1}=50 i_{1}=150 \mathrm{~V}$.

Therefore

$$
p_{6 \mathrm{~A}}=-150(6)=-900 \mathrm{~W}
$$

The 6 A source is delivering 900 W , and the 120 V source is absorbing 360 W . The total power absorbed is $360+450+90=900 \mathrm{~W}$. Therefore, the solution verifies that the power delivered equals the power absorbed.

#### Example 2.9 Constructing a Circuit Model Based on Terminal Measurements

The terminal voltage and terminal current were measured on the device shown in Fig. 2.20(a), and the values of $v_{t}$ and $i_{t}$ are tabulated in Fig. 2.20(b).
image_name:(a)
description:The diagram shows a two-terminal device with a voltage \( v_t \) and a current \( i_t \) flowing through it. The voltage is positive at the top terminal and negative at the bottom terminal.

(a)

| $v_{t}(\mathrm{~V})$ | $i_{t}(\mathrm{~A})$ |
| :---: | :---: |
| 30 | 0 |
| 15 | 3 |
| 0 | 6 |

(b)

Figure 2.20 A (a) Device and (b) data for Example 2.9.
a) Construct a circuit model of the device inside the box.
b) Using this circuit model, predict the power this device will deliver to a $10 \Omega$ resistor.

#### Solution

a) Plotting the voltage as a function of the current yields the graph shown in Fig. 2.21(a). The equation of the line plotted is

$$
v_{t}=30-5 i_{t}
$$

Now we need to identify the components of a circuit model that will produce the same relationship between voltage and current. Kirchhoff's voltage law tells us that the voltage drops across two components in series. From the equation, one of those components produces a 30 V drop regardless of the current. This component can be modeled as an ideal independent voltage source. The other component produces a positive voltage drop in the direction of the current $i_{t}$. Because the voltage drop is proportional to the current, Ohm's law tells us that this component can be modeled as an ideal resistor with a value of $5 \Omega$. The resulting circuit model is depicted in the dashed box in Fig. 2.21(b).
image_name:(a)
description:The graph in Fig. 2.21(a) is a linear plot depicting the relationship between the voltage \( v_t \) (in volts) and the current \( i_t \) (in amperes) for a particular device. The graph is a straight line with a negative slope, indicating a linear decrease in voltage as the current increases.

**Axes Labels and Units:**
- The vertical axis represents voltage \( v_t \) in volts (V), ranging from 0 to 30 V.
- The horizontal axis represents current \( i_t \) in amperes (A), ranging from 0 to 6 A.

**Overall Behavior and Trends:**
- The graph shows a linear decrease from 30 V at 0 A to 0 V at 6 A. This suggests that the device behaves like a combination of a voltage source and a resistor.

**Key Features and Technical Details:**
- The line intersects the vertical axis at 30 V, indicating the presence of an ideal voltage source in the circuit model.
- The slope of the line is negative, calculated as \(-5 \Omega\), which corresponds to the resistance value in the circuit model.
- At 3 A, the voltage is 15 V, which is a key point demonstrating the linear relationship.

**Annotations and Specific Data Points:**
- The graph has a significant point at \(i_t = 3\) A where \(v_t = 15\) V, showing a clear midpoint in the linear relationship.
- The linearity and endpoints of the graph are consistent with a series circuit model consisting of a 30 V independent voltage source and a 5 \(\Omega\) resistor.
image_name:(b)
description:
[
'name': '30V', 'type': 'VoltageSource', 'value': '30V', 'ports': {'Np': 'c', 'Nn': 'b'
'name': '5Ω', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'c', 'N2': 'a'
'name': '10Ω', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit consists of a 30V voltage source in series with a 5Ω resistor and a 10Ω resistor. The current through both resistors is the same.


Figure $2.21 \triangle$ (a) The graph of $v_{t}$ versus $i_{t}$ for the device in Fig. 2.20(a). (b) The resulting circuit model for the device in Fig. 2.20(a), connected to a $10 \Omega$ resistor.
b) Now we attach a $10 \Omega$ resistor to the device in Fig. 2.21(b) to complete the circuit. Kirchhoff's current law tells us that the current in the $10 \Omega$ resistor is the same as the current in the $5 \Omega$ resistor. Using Kirchhoff's voltage law and Ohm's law, we can write the equation for the voltage drops around the circuit, starting at the voltage source and proceeding clockwise:

$$
-30+5 i+10 i=0
$$

Solving for $i$, we get

$$
i=2 \mathrm{~A}
$$

Because this is the value of current flowing in the $10 \Omega$ resistor, we can use the power equation $p=i^{2} R$ to compute the power delivered to this resistor:

$$
p_{10 \Omega}=(2)^{2}(10)=40 \mathrm{~W}
$$

ASSESSMENT PROBLEMS

Objective 2-Be able to state and use Ohm's law and Kirchhoff's current and voltage laws
2.5 For the circuit shown, calculate (a) $i_{5}$; (b) $v_{1}$; (c) $v_{2}$; (d) $v_{5}$; and (e) the power delivered by the 24 V source.

Answer: (a) 2 A ;
(b) -4 V ;
(c) 6 V ;
(d) 14 V ;
(e) 48 W .
image_name:2.5
description:
[
'name': '24V', 'type': 'VoltageSource', 'value': '24V', 'ports': {'Np': 'Vin', 'Nn': 'GND'
'name': '3Ω', 'type': 'Resistor', 'value': '3Ω', 'ports': {'N1': 'Vin', 'N2': 'X1'
'name': '2Ω', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'GND', 'N2': 'X2'
'name': '7Ω', 'type': 'Resistor', 'value': '7Ω', 'ports': {'N1': 'X1', 'N2': 'X2'
]
extrainfo:The circuit is a simple resistive network with a 24V voltage source and three resistors (3Ω, 2Ω, and 7Ω). The circuit is used to calculate various voltages and currents using Ohm's Law and Kirchhoff's Laws.

2.6 Use Ohm's law and Kirchhoff's laws to find the value of $R$ in the circuit shown.

Answer: $R=4 \Omega$.
image_name:circuit shown
description:
[
'name': 'Vin1', 'type': 'VoltageSource', 'value': '200V', 'ports': {'Np': 'Vin1', 'Nn': 'GND'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'Vin1', 'N2': 'X1'
'name': '120 V', 'type': 'VoltageSource', 'value': '120V', 'ports': {'Np': 'X1', 'Nn': 'GND'
'name': '24 Ω', 'type': 'Resistor', 'value': '24 Ω', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': '8 Ω', 'type': 'Resistor', 'value': '8 Ω', 'ports': {'N1': 'X1', 'N2': 'GND'
]
extrainfo:The circuit consists of a 200V voltage source, a resistor of unknown resistance R, a 120V voltage source, and two resistors of 24Ω and 8Ω. The circuit is grounded at multiple points and is used to calculate voltages and currents using Ohm's Law and Kirchhoff's Laws.


NOTE: Also try Chapter Problems 2.18, 2.19, 2.29, and 2.31.
2.7 a) The terminal voltage and terminal current were measured on the device shown. The values of $v_{t}$ and $i_{t}$ are provided in the table. Using these values, create the straight line plot of $v_{t}$ versus $i_{t}$. Compute the equation of the line and use the equation to construct a circuit model for the device using an ideal voltage source and a resistor.
b) Use the model constructed in (a) to predict the power that the device will deliver to a $25 \Omega$ resistor.

Answer: (a) A 25 V source in series with a $100 \Omega$ resistor;
(b) 1 W .
image_name:Device
description:The diagram shows a device with a voltage across it labeled as vt and a current through it labeled as it. The positive terminal is at the top, and the negative terminal is at the bottom.

(a)

| $v_{t}(\mathrm{~V})$ | $i_{t}(\mathrm{~A})$ |
| :---: | :---: |
| 25 | 0 |
| 15 | 0.1 |
| 5 | 0.2 |
| 0 | 0.25 |

(b)
2.8 Repeat Assessment Problem 2.7 but use the equation of the graphed line to construct a circuit model containing an ideal current source and a resistor.

Answer: (a) A 0.25 A current source connected between the terminals of a $100 \Omega$ resistor;
(b) 1 W .

## 2.5 Analysis of a Circuit Containing Dependent Sources

image_name:Figure 2.22
description:
[
'name': '500 V', 'type': 'VoltageSource', 'value': '500 V', 'ports': {'Np': 'a', 'Nn': 'c'
'name': '5 Ω', 'type': 'Resistor', 'value': '5 Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '20 Ω', 'type': 'Resistor', 'value': '20 Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': '5iΔ', 'type': 'CurrentControlledCurrentSource', 'ports': {'Np': 'c', 'Nn': 'b'
]
extrainfo:The circuit contains a dependent current source controlled by the current iΔ through the 5 Ω resistor. The voltage source provides 500 V between nodes a and c. The dependent current source is 5 times the current iΔ.


Figure $2.22 \triangle \mathrm{~A}$ circuit with a dependent source.

We conclude this introduction to elementary circuit analysis with a discussion of a circuit that contains a dependent source, as depicted in Fig. 2.22.

We want to use Kirchhoff's laws and Ohm's law to find $v_{o}$ in this circuit. Before writing equations, it is good practice to examine the circuit diagram closely. This will help us identify the information that is known and the information we must calculate. It may also help us devise a strategy for solving the circuit using only a few calculations.

A look at the circuit in Fig. 2.22 reveals that

- Once we know $i_{o}$, we can calculate $v_{o}$ using Ohm's law.
- Once we know $i_{\Delta}$, we also know the current supplied by the dependent source $5 i_{\Delta}$.
- The current in the 500 V source is $i_{\Delta}$.

There are thus two unknown currents, $i_{\Delta}$ and $i_{o}$. We need to construct and solve two independent equations involving these two currents to produce a value for $v_{o}$.

From the circuit, notice the closed path containing the voltage source, the $5 \Omega$ resistor, and the $20 \Omega$ resistor. We can apply Kirchhoff's voltage law around this closed path. The resulting equation contains the two unknown currents:

$$
\begin{equation*}
500=5 i_{\Delta}+20 i_{o} \tag{2.22}
\end{equation*}
$$

Now we need to generate a second equation containing these two currents. Consider the closed path formed by the $20 \Omega$ resistor and the dependent current source. If we attempt to apply Kirchhoff's voltage law to this loop, we fail to develop a useful equation, because we don't know the value of the voltage across the dependent current source. In fact, the voltage across the dependent source is $v_{o}$, which is the voltage we are trying to compute. Writing an equation for this loop does not advance us toward a solution. For this same reason, we do not use the closed path containing the voltage source, the $5 \Omega$ resistor, and the dependent source.

There are three nodes in the circuit, so we turn to Kirchhoff's current law to generate the second equation. Node a connects the voltage source and the $5 \Omega$ resistor; as we have already observed, the current in these two elements is the same. Either node b or node c can be used to construct the second equation from Kirchhoff's current law. We select node b and produce the following equation:

$$
\begin{equation*}
i_{o}=i_{\Delta}+5 i_{\Delta}=6 i_{\Delta} \tag{2.23}
\end{equation*}
$$

Solving Eqs. 2.22 and 2.23 for the currents, we get

$$
\begin{align*}
i_{\Delta} & =4 \mathrm{~A} \\
i_{o} & =24 \mathrm{~A} \tag{2.24}
\end{align*}
$$

Using Eq. 2.24 and Ohm's law for the $20 \Omega$ resistor, we can solve for the voltage $v_{o}$ :

$$
v_{o}=20 i_{o}=480 \mathrm{~V}
$$

Think about a circuit analysis strategy before beginning to write equations. As we have demonstrated, not every closed path provides an opportunity to write a useful equation based on Kirchhoff's voltage law. Not every node provides for a useful application of Kirchhoff's current law. Some preliminary thinking about the problem can help in selecting the most fruitful approach and the most useful analysis tools for a particular
problem. Choosing a good approach and the appropriate tools will usually reduce the number and complexity of equations to be solved. Example 2.10 illustrates another application of Ohm's law and Kirchhoff's laws to a circuit with a dependent source. Example 2.11 involves a much more complicated circuit, but with a careful choice of analysis tools, the analysis is relatively uncomplicated.

#### Example 2.10 Applying Ohm's Law and Kirchhoff's Laws to Find an Unknown Voltage

a) Use Kirchhoff's laws and Ohm's law to find the voltage $v_{o}$ as shown in Fig. 2.23.
b) Show that your solution is consistent with the constraint that the total power developed in the circuit equals the total power dissipated.
image_name:Figure 2.23
description:
[
'name': '10 V', 'type': 'VoltageSource', 'value': '10 V', 'ports': {'Np': 'Vin', 'Nn': 'GND'
'name': '6 Ω', 'type': 'Resistor', 'value': '6 Ω', 'ports': {'N1': 'Vin', 'N2': 'X1'
'name': '3 is', 'type': 'CurrentControlledVoltageSource', 'value': '3is', 'ports': {'Np': 'X1', 'Nn': 'GND'
'name': '2 Ω', 'type': 'Resistor', 'value': '2 Ω', 'ports': {'N1': 'X1', 'N2': 'Vo'
'name': '3 Ω', 'type': 'Resistor', 'value': '3 Ω', 'ports': {'N1': 'Vo', 'N2': 'GND'
]
extrainfo:The circuit consists of a voltage source, resistors, and a voltage-controlled voltage source. Current is flows from the 10 V source through the 6 Ω resistor, controlled by the dependent source 3i_s, and through the 2 Ω and 3 Ω resistors. The voltage across the 3 Ω resistor is v_o.


Figure 2.23 $\boldsymbol{\Delta}$ The circuit for Example 2.10.

#### Solution

a) A close look at the circuit in Fig. 2.23 reveals that:

- There are two closed paths, the one on the left with the current $i_{s}$ and the one on the right with the current $i_{o}$.
- Once $i_{o}$ is known, we can compute $v_{o}$.

We need two equations for the two currents. Because there are two closed paths and both have voltage sources, we can apply Kirchhoff's voltage law to each to give the following equations:

$$
\begin{aligned}
& 10=6 i_{s} \\
& 3 i_{s}=2 i_{o}+3 i_{o}
\end{aligned}
$$

Solving for the currents yields

$$
\begin{aligned}
i_{s} & =1.67 \mathrm{~A} \\
i_{o} & =1 \mathrm{~A}
\end{aligned}
$$

Applying Ohm's law to the $3 \Omega$ resistor gives the desired voltage:

$$
v_{o}=3 i_{o}=3 \mathrm{~V}
$$

b) To compute the power delivered to the voltage sources, we use the power equation in the form $p=v i$. The power delivered to the independent voltage source is

$$
p=(10)(-1.67)=-16.7 \mathrm{~W}
$$

The power delivered to the dependent voltage source is

$$
p=\left(3 i_{s}\right)\left(-i_{o}\right)=(5)(-1)=-5 \mathrm{~W}
$$

Both sources are developing power, and the total developed power is 21.7 W .

To compute the power delivered to the resistors, we use the power equation in the form $p=i^{2} R$. The power delivered to the $6 \Omega$ resistor is

$$
p=(1.67)^{2}(6)=16.7 \mathrm{~W}
$$

The power delivered to the $2 \Omega$ resistor is

$$
p=(1)^{2}(2)=2 \mathrm{~W}
$$

The power delivered to the $3 \Omega$ resistor is

$$
p=(1)^{2}(3)=3 \mathrm{~W}
$$

The resistors all dissipate power, and the total power dissipated is 21.7 W , equal to the total power developed in the sources.

#### Example 2.11 Applying Ohm's Law and Kirchhoff's Law in an Amplifier Circuit

The circuit in Fig. 2.24 represents a common configuration encountered in the analysis and design of transistor amplifiers. Assume that the values of all the circuit elements $-R_{1}, R_{2}, R_{C}, R_{E}, V_{C C}$, and $V_{0}-$ are known.
a) Develop the equations needed to determine the current in each element of this circuit.
b) From these equations, devise a formula for computing $i_{B}$ in terms of the circuit element values.
image_name:Figure 2.24
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'b', 'N2': 'd'
'name': 'RC', 'type': 'Resistor', 'value': 'RC', 'ports': {'N1': 'a', 'N2': '1'
'name': 'RE', 'type': 'Resistor', 'value': 'RE', 'ports': {'N1': '3', 'N2': 'd'
'name': 'VCC', 'type': 'VoltageSource', 'value': 'VCC', 'ports': {'Np': 'a', 'Nn': 'd'
'name': 'betaIb', 'type': 'VoltageControlledCurrentSource', 'value': 'betaIb', 'ports': {'Np': '1', 'Nn': 'c'
'name':'V0', 'type':'VoltageSource', 'value':'V0','ports':{'Np':'2','Nn':'c'
]
extrainfo:The circuit is a transistor amplifier configuration with resistors R1, R2, RC, RE, a voltage source VCC, and a voltage-controlled current source V0. The circuit involves six unknown currents: i1, i2, iB, iC, iE, and iCC. The dependent current source is controlled by the base current iB.


Figure 2.24 The circuit for Example 2.11.

#### Solution

A careful examination of the circuit reveals a total of six unknown currents, designated $i_{1}, i_{2}, i_{B}, i_{C}, i_{E}$, and $i_{C C}$. In defining these six unknown currents, we used the observation that the resistor $R_{C}$ is in series with the dependent current source $\beta i_{B}$. We now must derive six independent equations involving these six unknowns.
a) We can derive three equations by applying Kirchhoff's current law to any three of the nodes $\mathrm{a}, \mathrm{b}, \mathrm{c}$, and d. Let's use nodes a, b, and c and label the currents away from the nodes as positive:
(1) $i_{1}+i_{C}-i_{C C}=0$,
(2) $i_{B}+i_{2}-i_{1}=0$,
(3) $i_{E}-i_{B}-i_{C}=0$.

A fourth equation results from imposing the constraint presented by the series connection of $R_{C}$ and the dependent source:
(4) $i_{C}=\beta i_{B}$.

We turn to Kirchhoff's voltage law in deriving the remaining two equations. We need to select two closed paths in order to use Kirchhoff's voltage law. Note that the voltage across the dependent current source is unknown, and that it cannot be determined from the source current $\beta i_{B}$. Therefore, we must select two closed paths that do not contain this dependent current source.

We choose the paths bcdb and badb and specify voltage drops as positive to yield
(5) $V_{0}+i_{E} R_{E}-i_{2} R_{2}=0$,
(6) $-i_{1} R_{1}+V_{C C}-i_{2} R_{2}=0$.
b) To get a single equation for $i_{B}$ in terms of the known circuit variables, you can follow these steps:

- Solve Eq. (6) for $i_{1}$, and substitute this solution for $i_{1}$ into Eq. (2).
- Solve the transformed Eq. (2) for $i_{2}$, and substitute this solution for $i_{2}$ into Eq. (5).
- Solve the transformed Eq. (5) for $i_{E}$, and substitute this solution for $i_{E}$ into Eq. (3). Use Eq. (4) to eliminate $i_{C}$ in Eq. (3).
- Solve the transformed Eq. (3) for $i_{B}$, and rearrange the terms to yield

$$
\begin{equation*}
i_{B}=\frac{\left(V_{C C} R_{2}\right) /\left(R_{1}+R_{2}\right)-V_{0}}{\left(R_{1} R_{2}\right) /\left(R_{1}+R_{2}\right)+(1+\beta) R_{E}} \tag{2.25}
\end{equation*}
$$

Problem 2.31 asks you to verify these steps. Note that once we know $i_{B}$, we can easily obtain the remaining currents.

ASSESSMENT PROBLEMS

Objective 3-Know how to calculate power for each element in a simple circuit

2.9 For the circuit shown find (a) the current $i_{1}$ in microamperes, (b) the voltage $v$ in volts, (c) the total power generated, and (d) the total power absorbed.

Answer: (a) $25 \mu \mathrm{~A}$;
(b) -2 V ;
(c) $6150 \mu \mathrm{~W}$;
(d) $6150 \mu \mathrm{~W}$.
image_name:2.9
description:
[
'name': '54 kΩ', 'type': 'Resistor', 'value': '54 kΩ', 'ports': {'N1': 'X3', 'N2': 'X2'
'name': '1 V', 'type': 'VoltageSource', 'value': '1 V', 'ports': {'Np': 'X1', 'Nn': 'X2'
'name': '6 kΩ', 'type': 'Resistor', 'value': '6 kΩ', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': '30 i₁', 'type': 'VoltageControlledCurrentSource', 'value': '30 i₁', 'ports': {'Np': 'X4', 'Nn': 'X1'
'name': '1.8 kΩ', 'type': 'Resistor', 'value': '1.8 kΩ', 'ports': {'N1': 'X4', 'N2': 'X5'
'name': '5 V', 'type': 'VoltageSource', 'value': '5 V', 'ports': {'Np': 'X3', 'Nn': 'GND'
'name': '8 V', 'type': 'VoltageSource', 'value': '8 V', 'ports': {'Np': 'X5', 'Nn': 'GND'
]
extrainfo:The circuit consists of resistors, independent voltage sources, and a voltage-controlled voltage source. The current i₁ flows through the 54 kΩ resistor, and the voltage v is across the voltage-controlled voltage source. The total power generated and absorbed is 6150 μW.

2.10 The current $i_{\phi}$ in the circuit shown is 2 A . Calculate
a) $v_{s}$,
b) the power absorbed by the independent voltage source,

NOTE: Also try Chapter Problems 2.32 and 2.33.
c) the power delivered by the independent current source,
d) the power delivered by the controlled current source,
e) the total power dissipated in the two resistors.

Answer: (a) 70 V ;
(b) 210 W ;
(c) 300 W ;
(d) 40 W ;
(e) 130 W .
image_name:2.10
description:
[
'name': '5 A', 'type': 'CurrentSource', 'value': '5 A', 'ports': {'Np': 'GND', 'Nn': 'X1'
'name': '30 Ω', 'type': 'Resistor', 'value': '30 Ω', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': '10 Ω', 'type': 'Resistor', 'value': '10 Ω', 'ports': {'N1': 'X1', 'N2': 'VS'
'name': '2iϕ', 'type': 'CurrentControlledCurrentSource', 'ports': {'Np': 'X1', 'Nn': 'VS'
'name': 'vs', 'type': 'VoltageSource', 'ports': {'Np': 'VS', 'Nn': 'GND'
]
extrainfo:The circuit contains a current source of 5 A connected to node X1 and ground. A 30 Ω resistor is connected in parallel with the current source. A 10 Ω resistor and a current-controlled voltage source (2iϕ) are connected in series between node X1 and VS. The voltage source v_s is connected between node VS and ground.


#Practical Perspective

Heating with Electric Radiators

Let's determine which of the two wiring diagrams introduced at the beginning of this chapter should be used to wire the electric radiators to the power supplied to the garage. We begin with the diagram shown in Fig. 2.25. We can turn this into a circuit by modeling the radiators as resistors. The resulting circuit is shown in Fig. 2.26. Note that each radiator has the same resistance, $R$, and is labeled with a voltage and current value.
image_name:Figure 2.26
description:
[
'name': '240 V', 'type': 'VoltageSource', 'value': '240 V', 'ports': {'Np': 'Vin', 'Nn': 'GND'
'name': 'Radiator1', 'type': 'Resistor', 'ports': {'N1': 'Vin', 'N2': 'GND'
'name': 'Radiator2', 'type': 'Resistor', 'ports': {'N1': 'Vin', 'N2': 'GND'
]
extrainfo:The circuit consists of a 240 V voltage source and two resistors connected in series. The voltage across each resistor is 240 V, and the current through the resistors is labeled as i1 and is.

Figure 2.25 A wiring diagram for two radiators.




Figure 2.26 A circuit based on Fig. 2.25.

To find the unknown voltages and currents for the circuit in Fig. 2.26, begin by writing a KVL equation for the left side of the circuit:

$$
-240+v_{1}=0 \quad \Rightarrow \quad v_{1}=240 \mathrm{~V}
$$

Now write a KVL equation for the right side of this circuit:

$$
-v_{1}+v_{2}=0 \quad \Rightarrow \quad v_{2}=v_{1}=240 \mathrm{~V}
$$

Remember that the power and voltage specifications for each radiator are 1200 W , 240 V . Therefore the configuration shown in Fig. 2.25 satisfies the voltage specification, since each radiator would have a supplied voltage of 240 V .

Next, calculate the value of resistance $R$ that will correctly model each radiator. We want the power associated with each radiator to be 1200 W. Use the equation for resistor power that involves the resistance and the voltage:

$$
P_{1}=\frac{v_{1}^{2}}{R}=\frac{v_{2}^{2}}{R}=P_{2} \quad \Rightarrow \quad R=\frac{v_{1}^{2}}{P_{1}}=\frac{240^{2}}{1200}=48 \Omega
$$

Each radiator can be modeled as a $48 \Omega$ resistor with a voltage drop of 240 V and power of 1200 W . The total power for two radiators is thus 2400 W .

Finally, calculate the power supplied by the 240 V source. To do this, calculate the current in the voltage source, $\mathrm{i}_{\mathrm{s}^{\prime}}$ by writing a KCL equation at the top node in Fig. 2.26, and use that current to calculate the power for the voltage source.

$$
\begin{gathered}
-i_{s}+i_{1}+i_{2}=0 \Rightarrow i_{s}=i_{1}+i_{2}=\frac{v_{1}}{R}+\frac{v_{2}}{R}=\frac{240}{48}+\frac{240}{48}=10 \mathrm{~A} \\
P_{s}=-(240)\left(i_{s}\right)=-(240)(10)=-2400 \mathrm{~W}
\end{gathered}
$$

Thus, the total power in the circuit is $-2400+2400=0$, so the power balances.

Now look at the other wiring diagram for the radiators, shown in Fig. 2.27. We know that the radiators can be modeled using $48 \Omega$ resistors, which are used to turn the wiring diagram into the circuit in Fig. 2.28.

Start analyzing the circuit in Fig. 2.28 by writing a KVL equation:

$$
-240+v_{x}+v_{y}=0 \quad \Rightarrow \quad v_{x}+v_{y}=240
$$

Next, write a KCL equation at the node labeled a:

$$
-i_{x}+i_{y}=0 \quad \Rightarrow \quad i_{x}=i_{y}=i
$$

The current in the two resistors is the same, and we can use that current in Ohm's Law equations to replace the two unknown voltages in the KVL equation:

$$
48 i=48 i=240=96 i \quad \Rightarrow \quad i=\frac{240}{96}=2.5 \mathrm{~A}
$$

Use the current in the two resistors to calculate the power for the two radiators.

$$
P_{x}=P_{y}=R i^{2}=(48)(2.5)^{2}=300 \mathrm{~W}
$$

Thus, if the radiators are wired as shown in Fig. 2.27, their total power will be only 600 W . This is insufficient to heat the garage.

Therefore, the way the radiators are wired has a big impact on the amount of heat that will be supplied. When they are wired using the diagram in Fig. 2.25, 2400 W of power will be available, but when they are wired using the diagram in Fig. 2.27, only 600 W of power will be available.

NOTE: Assess your understanding of the Practical Perspective by solving Chapter Problems 2.41-2.43.
image_name:Figure 2.27
description:
[
'name': '240 V', 'type': 'VoltageSource', 'value': '240 V', 'ports': {'Np': 'N1', 'Nn': 'N2'
'name': 'radiator1', 'type': 'Other', 'ports': {'N1': 'N1', 'N2': 'N3'
'name': 'radiator2', 'type': 'Other', 'ports': {'N1': 'N3', 'N2': 'N2'
]
extrainfo:The circuit consists of a 240 V voltage source connected in series with two radiators. This configuration results in a total power of 600 W being supplied.


Figure 2.27 Another way to wire two radiators.
image_name:Figure 2.28
description:
[
'name': 'Vin', 'type': 'VoltageSource', 'value': '240V', 'ports': {'Np': 'Vin', 'Nn': 'GND'
'name': '48Ω', 'type': 'Resistor', 'value': '48Ω', 'ports': {'N1': 'Vin', 'N2': 'a'
'name': '48Ω', 'type': 'Resistor', 'value': '48Ω', 'ports': {'N1': 'a', 'N2': 'GND'
]
extrainfo:The circuit consists of a 240 V voltage source connected in series with two 48Ω resistors. The currents through the resistors are labeled as ix and iy, and the voltages across them as vx and vy.


Figure 2.28 A circuit based on Fig. 2.27.

## Summary

- The circuit elements introduced in this chapter are voltage sources, current sources, and resistors:
- An ideal voltage source maintains a prescribed voltage regardless of the current in the device. An ideal current source maintains a prescribed current regardless of the voltage across the device. Voltage and current sources are either independent, that is, not influenced by any other current or voltage in the circuit; or dependent, that is, determined by some other current or voltage in the circuit. (See pages 26 and 27.)
- A resistor constrains its voltage and current to be proportional to each other. The value of the proportional constant relating voltage and current in a resistor is called its resistance and is measured in ohms. (See page 30.)
- Ohm's law establishes the proportionality of voltage and current in a resistor. Specifically,

$$
v=i R
$$

if the current flow in the resistor is in the direction of the voltage drop across it, or

$$
v=-i R
$$

if the current flow in the resistor is in the direction of the voltage rise across it. (See page 31.)

- By combining the equation for power, $p=v i$, with Ohm's law, we can determine the power absorbed by a resistor:

$$
p=i^{2} R=v^{2} / R
$$

(See page 32.)

- Circuits are described by nodes and closed paths. A node is a point where two or more circuit elements join. When just two elements connect to form a node, they are said to be in series. A closed path is a loop traced through connecting elements, starting and ending at the same node and encountering intermediate nodes only once each. (See pages 37-39.)
- The voltages and currents of interconnected circuit elements obey Kirchhoff's laws:
- Kirchhoff's current law states that the algebraic sum of all the currents at any node in a circuit equals zero. (See page 37.)
- Kirchhoff's voltage law states that the algebraic sum of all the voltages around any closed path in a circuit equals zero. (See page 38.)
- A circuit is solved when the voltage across and the current in every element have been determined. By combining an understanding of independent and dependent sources, Ohm's law, and Kirchhoff's laws, we can solve many simple circuits.



CHAPTER 3
