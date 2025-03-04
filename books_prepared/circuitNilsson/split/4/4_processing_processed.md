# 4.Techniques of Circuit Analysis
CHAPTER CONTENTS

4.1 Terminology p. 90
4.2 Introduction to the Node-Voltage Method p. 93
4.3 The Node-Voltage Method and Dependent Sources p. 95
4.4 The Node-Voltage Method: Some Special Cases p. 96
4.5 Introduction to the Mesh-Current Method p. 99
4.6 The Mesh-Current Method and Dependent Sources p. 102
4.7 The Mesh-Current Method: Some Special Cases p. 103
4.8 The Node-Voltage Method Versus the Mesh-Current Method p. 106
4.9 Source Transformations p. 109
4.10 Thévenin and Norton Equivalents p. 113
4.11 More on Deriving a Thévenin Equivalent p. 117
4.12 Maximum Power Transfer p. 120
4.13 Superposition p. 122

CHAPTER OBJECTIVES

1 Understand and be able to use the node-voltage method to solve a circuit.

2 Understand and be able to use the mesh-current method to solve a circuit.

3 Be able to decide whether the node-voltage method or the mesh-current method is the preferred approach to solving a particular circuit.
4 Understand source transformation and be able to use it to solve a circuit.
5 Understand the concept of the Thévenin and Norton equivalent circuits and be able to construct a Thévenin or Norton equivalent for a circuit.
6 Know the condition for maximum power transfer to a resistive load and be able to calculate the value of the load resistor that satisfies this condition.



So far, we have analyzed relatively simple resistive circuits

by applying Kirchhoff's laws in combination with Ohm's law. We can use this approach for all circuits, but as they become structurally more complicated and involve more and more elements, this direct method soon becomes cumbersome. In this chapter we introduce two powerful techniques of circuit analysis that aid in the analysis of complex circuit structures: the node-voltage method and the mesh-current method. These techniques give us two systematic methods of describing circuits with the minimum number of simultaneous equations.

In addition to these two general analytical methods, in this chapter we also discuss other techniques for simplifying circuits. We have already demonstrated how to use series-parallel reductions and $\Delta$-to-Y transformations to simplify a circuit's structure. We now add source transformations and Thévenin and Norton equivalent circuits to those techniques.

We also consider two other topics that play a role in circuit analysis. One, maximum power transfer, considers the conditions necessary to ensure that the power delivered to a resistive load by a source is maximized. Thévenin equivalent circuits are used in establishing the maximum power transfer conditions. The final topic in this chapter, superposition, looks at the analysis of circuits with more than one independent source.

Practical Perspective

Circuits with Realistic Resistors

In the last chapter we began to explore the effect of imprecise resistor values on the performance of a circuit; specifically, on the performance of a voltage divider. Resistors are manufactured for only a small number of discrete values, and any given resistor from a batch of resistors will vary from its stated value within some tolerance. Resistors with tighter tolerance, say $1 \%$, are more expensive than resistors with greater tolerance, say $10 \%$. Therefore, in a circuit that uses many resistors, it would be important to understand which resistor's value has the greatest impact on the expected performance of the circuit.
image_name:Resistor color code
description:The image depicts a collection of cylindrical resistors, each with colored bands encircling their bodies. These bands are part of the resistor color code system used to indicate the resistor's value and tolerance. Each resistor has four distinct colored bands:

1. **First Digit Band**: The first band represents the first significant digit of the resistor's value.
2. **Second Digit Band**: The second band indicates the second significant digit.
3. **Multiplier Band**: The third band acts as a multiplier, determining the power of ten by which the significant digits should be multiplied.
4. **Tolerance Band**: The fourth band specifies the tolerance, or the precision of the resistor's value, indicating how much the actual resistance can vary from the stated value.

The resistors are shown with metallic leads protruding from either end, which are used to connect them into an electrical circuit. The image is labeled to identify the function of each band, helping in the interpretation of resistor values and their precision in electronic circuits. This visual representation is essential for understanding how to read resistor values and selecting the appropriate components for circuit designs, especially when considering sensitivity analysis and the impact of resistor tolerance on circuit performance.


In other words, we would like to predict the effect of varying each resistor's value on the output of the circuit. If we know that a particular resistor must be very close to its stated value for the circuit to function correctly, we can then decide to spend the extra money necessary to achieve a tighter tolerance on that resistor's value.

Exploring the effect of a circuit component's value on the circuit's output is known as sensitivity analysis. Once we have presented additional circuit analysis techniques, the topic of sensitivity analysis will be examined.
image_name:Ocean/Corbis
description:The image shows a collection of axial-lead resistors. These resistors are cylindrical in shape with color bands painted around their bodies, which are used to indicate their resistance values, tolerance, and sometimes temperature coefficient. The color bands on one of the resistors, for example, are brown, black, red, and gold, which typically represent a resistance value of 1k ohms with a tolerance of ±5%. The resistors are made with a beige or light brown ceramic material, and each has two metallic leads extending from either end, which are used for electrical connections. The resistors are randomly oriented, showing a pile of components possibly used for electronic circuit assembly.


Ocean/Corbis
image_name:(a)
description:
[
'name': 'Vs', 'type': 'VoltageSource', 'ports': {'Np': 'a', 'Nn': 'f'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'c', 'N2': 'e'
'name': 'R4', 'type': 'Resistor', 'value': 'R4', 'ports': {'N1': 'd', 'N2': 'e'
'name': 'R5', 'type': 'Resistor', 'value': 'R5', 'ports': {'N1': 'd', 'N2': 'f'
'name': 'R6', 'type': 'Resistor', 'value': 'R6', 'ports': {'N1': 'b', 'N2': 'd'
'name': 'R7', 'type': 'Resistor', 'value': 'R7', 'ports': {'N1': 'b', 'N2': 'e'
'name': 'R8', 'type': 'Resistor', 'value': 'R8', 'ports': {'N1': 'c', 'N2': 'd'
]
extrainfo:The circuit diagram (a) is a planar circuit with multiple resistors and a voltage source arranged in a network. It includes a voltage source Vs and resistors R1 to R8. The resistors form a complex mesh with nodes labeled a to f.
image_name:(b)
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'R4', 'type': 'Resistor', 'value': 'R4', 'ports': {'N1': 'd', 'N2': 'e'
'name': 'R5', 'type': 'Resistor', 'value': 'R5', 'ports': {'N1': 'e', 'N2': 'f'
'name': 'R6', 'type': 'Resistor', 'value': 'R6', 'ports': {'N1': 'b', 'N2': 'e'
'name': 'R7', 'type': 'Resistor', 'value': 'R7', 'ports': {'N1': 'b', 'N2': 'd'
'name': 'R8', 'type': 'Resistor', 'value': 'R8', 'ports': {'N1': 'e', 'N2': 'c'
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': 'a', 'Nn': 'f'
]
extrainfo:The circuit diagram (b) is a redrawn version of a nonplanar circuit to verify its planarity. It contains resistors R1 to R8 and a voltage source Vs.


Figure 4.1 ( (a) A planar circuit. (b) The same circuit redrawn to verify that it is planar.
image_name:Figure 4.2
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'd', 'N2': 'f'
'name': 'R4', 'type': 'Resistor', 'value': 'R4', 'ports': {'N1': 'e', 'N2': 'f'
'name': 'R5', 'type': 'Resistor', 'value': 'R5', 'ports': {'N1': 'b', 'N2': 'e'
'name': 'R6', 'type': 'Resistor', 'value': 'R6', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R7', 'type': 'Resistor', 'value': 'R7', 'ports': {'N1': 'c', 'N2': 'e'
'name': 'R8', 'type': 'Resistor', 'value': 'R8', 'ports': {'N1': 'c', 'N2': 'f'
'name': 'R9', 'type': 'Resistor', 'value': 'R9', 'ports': {'N1': 'b', 'N2': 'd'
'name': 'R10', 'type': 'Resistor', 'value': 'R10', 'ports': {'N1': 'b', 'N2': 'f'
'name': 'R11', 'type': 'Resistor', 'value': 'R11', 'ports': {'N1': 'd', 'N2': 'e'
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': 'a', 'Nn': 'b'
]
extrainfo:The circuit is a nonplanar configuration with multiple resistors (R1 to R11) and a voltage source (Vs). It is a complex bridge-like network with intersecting branches, illustrating nonplanarity.


Figure 4.2 A A nonplanar circuit.

## 4.1 Terminology

To discuss the more involved methods of circuit analysis, we must define a few basic terms. So far, all the circuits presented have been planar circuits-that is, those circuits that can be drawn on a plane with no crossing branches. A circuit that is drawn with crossing branches still is considered planar if it can be redrawn with no crossover branches. For example, the circuit shown in Fig. 4.1(a) can be redrawn as Fig. 4.1(b); the circuits are equivalent because all the node connections have been maintained. Therefore, Fig. 4.1(a) is a planar circuit because it can be redrawn as one. Figure 4.2 shows a nonplanar circuit-it cannot be redrawn in such a way that all the node connections are maintained and no branches overlap. The node-voltage method is applicable to both planar and nonplanar circuits, whereas the mesh-current method is limited to planar circuits.

Describing a Circuit—The Vocabulary

In Section 1.5 we defined an ideal basic circuit element. When basic circuit elements are interconnected to form a circuit, the resulting interconnection is described in terms of nodes, paths, branches, loops, and meshes. We defined both a node and a closed path, or loop, in Section 2.4. Here we restate those definitions and then define the terms path, branch, and mesh. For your convenience, all of these definitions are presented in Table 4.1. Table 4.1 also includes examples of each definition taken from the circuit in Fig. 4.3, which are developed in Example 4.1.

#### Example 4.1 Identifying Node, Branch, Mesh and Loop in a Circuit

For the circuit in Fig. 4.3, identify
a) all nodes.
b) all essential nodes.
c) all branches.
d) all essential branches.
e) all meshes.
f) two paths that are not loops or essential branches.
g) two loops that are not meshes.

#### Solution

a) The nodes are a, b, c, d, e, f, and g.
b) The essential nodes are $\mathrm{b}, \mathrm{c}, \mathrm{e}$, and g .
c) The branches are $v_{1}, v_{2}, R_{1}, R_{2}, R_{3}, R_{4}, R_{5}, R_{6}$, $R_{7}$, and $I$.
d) The essential branches are $v_{1}-R_{1}, R_{2}-R_{3}$, $v_{2}-R_{4}, R_{5}, R_{6}, R_{7}$, and $I$.
e) The meshes are $v_{1}-R_{1}-R_{5}-R_{3}-R_{2}$, $v_{2}-R_{2}-R_{3}-R_{6}-R_{4}, \quad R_{5}-R_{7}-R_{6}$, and $R_{7}-I$.
image_name:Figure 4.3
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'd', 'N2': 'e'
'name': 'R4', 'type': 'Resistor', 'value': 'R4', 'ports': {'N1': 'f', 'N2': 'g'
'name': 'R5', 'type': 'Resistor', 'value': 'R5', 'ports': {'N1': 'b', 'N2': 'e'
'name': 'R6', 'type': 'Resistor', 'value': 'R6', 'ports': {'N1': 'e', 'N2': 'g'
'name': 'R7', 'type': 'Resistor', 'value': 'R7', 'ports': {'N1': 'b', 'N2': 'g'
'name': 'v1', 'type': 'VoltageSource', 'value': 'v1', 'ports': {'Np': 'a', 'Nn': 'c'
'name': 'v2', 'type': 'VoltageSource', 'value': 'v2', 'ports': {'Np': 'c', 'Nn': 'f'
'name': 'I', 'type': 'CurrentSource', 'value': 'I', 'ports': {'Np': 'g', 'Nn': 'b'
]
extrainfo:The circuit consists of two voltage sources (v1 and v2), a current source (I), and seven resistors (R1 to R7). The nodes are labeled as a, b, c, d, e, f, and g. The essential nodes are b, c, e, and g. The circuit includes multiple loops and paths, with three meshes identified. The current source I is connected between nodes b and g.


Figure 4.3 A A circuit illustrating nodes, branches, meshes, paths, and loops.
f) $R_{1}-R_{5}-R_{6}$ is a path, but it is not a loop (because it does not have the same starting and ending nodes), nor is it an essential branch (because it does not connect two essential nodes). $v_{2}-R_{2}$ is also a path but is neither a loop nor an essential branch, for the same reasons.
g) $v_{1}-R_{1}-R_{5}-R_{6}-R_{4}-v_{2}$ is a loop but is not a mesh, because there are two loops within it. $I-R_{5}-R_{6}$ is also a loop but not a mesh.

NOTE: Assess your understanding of this material by trying Chapter Problems 4.1 and 4.5 .

TABLE 4.1 Terms for Describing Circuits

| Name | Definition | Example From Fig. $\mathbf{4 . 3}$ |
| :--- | :--- | :--- |
| node | A point where two or more circuit elements join | a |
| essential node | A node where three or more circuit elements join | b |
| path | A trace of adjoining basic elements with no |  |
|  | elements included more than once | $v_{1}-R_{1}-R_{5}-R_{6}$ |
| branch | A path that connects two nodes | $R_{1}$ |
| essential branch | A path which connects two essential nodes without | $v_{1}-R_{1}$ |
|  | passing through an essential node | $v_{1}-R_{1}-R_{5}-R_{6}-R_{4}-v_{2}$ |
| loop | A path whose last node is the same as the starting node | $v_{1}-R_{1}-R_{5}-R_{3}-R_{2}$ |

Fig. 4.3 is a planar circuit
Fig. 4.2 is a nonplanar circuit

Simultaneous Equations-How Many?

The number of unknown currents in a circuit equals the number of branches, $b$, where the current is not known. For example, the circuit shown in Fig. 4.3 has nine branches in which the current is unknown. Recall that we must have $b$ independent equations to solve a circuit with $b$ unknown currents. If we let $n$ represent the number of nodes in the circuit, we can derive $n-1$ independent equations by applying Kirchhoff's current law to any set of $n-1$ nodes. (Application of the current law to the $n$th node does not generate an independent equation, because this equation can be derived from the previous $n-1$ equations. See Problem 4.5.) Because we need $b$ equations to describe a given circuit and because we can obtain $n-1$ of these equations from Kirchhoff's current law, we must apply Kirchhoff's voltage law to loops or meshes to obtain the remaining $b-(n-1)$ equations.

Thus by counting nodes, meshes, and branches where the current is unknown, we have established a systematic method for writing the necessary number of equations to solve a circuit. Specifically, we apply Kirchhoff's current law to $n-1$ nodes and Kirchhoff's voltage law to $b-(n-1)$ loops (or meshes). These observations also are valid in terms of essential nodes and essential branches. Thus if we let $n_{e}$ represent the number of essential nodes and $b_{e}$ the number of essential branches where the current is unknown, we can apply Kirchhoff's current law at $n_{e}-1$ nodes and Kirchhoff's voltage law around $b_{e}-\left(n_{e}-1\right)$ loops or meshes. In circuits, the number of essential nodes is less than or equal to the number of nodes, and the number of essential branches is less than or equal to the number of branches. Thus it is often convenient to use essential nodes and essential branches when analyzing a circuit, because they produce fewer independent equations to solve.

A circuit may consist of disconnected parts. An example of such a circuit is examined in Problem 4.3. The statements pertaining to the number of equations that can be derived from Kirchhoff's current law, $n-1$, and voltage law, $b-(n-1)$, apply to connected circuits. If a circuit has $n$ nodes and $b$ branches and is made up of $s$ parts, the current law can be
image_name:Figure 4.4
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'd', 'N2': 'e'
'name': 'R4', 'type': 'Resistor', 'value': 'R4', 'ports': {'N1': 'f', 'N2': 'g'
'name': 'R5', 'type': 'Resistor', 'value': 'R5', 'ports': {'N1': 'b', 'N2': 'e'
'name': 'R6', 'type': 'Resistor', 'value': 'R6', 'ports': {'N1': 'e', 'N2': 'g'
'name': 'R7', 'type': 'Resistor', 'value': 'R7', 'ports': {'N1': 'b', 'N2': 'g'
'name': 'v1', 'type': 'VoltageSource', 'value': 'v1', 'ports': {'Np': 'a', 'Nn': 'c'
'name': 'v2', 'type': 'VoltageSource', 'value': 'v2', 'ports': {'Np': 'c', 'Nn': 'f'
'name': 'I', 'type': 'CurrentSource', 'value': 'I', 'ports': {'Np': 'g', 'Nn': 'b'
]
extrainfo:The circuit contains two voltage sources and one current source. It is a multi-loop circuit with resistors forming several loops. The current directions are indicated for each resistor.


Figure 4.4 A The circuit shown in Fig. 4.3 with six unknown branch currents defined.
applied $n-s$ times, and the voltage law $b-n+s$ times. Any two separate parts can be connected by a single conductor. This connection always causes two nodes to form one node. Moreover, no current exists in the single conductor, so any circuit made up of $s$ disconnected parts can always be reduced to a connected circuit.

The Systematic Approach—An Illustration

We now illustrate this systematic approach by using the circuit shown in Fig. 4.4. We write the equations on the basis of essential nodes and branches. The circuit has four essential nodes and six essential branches, denoted $i_{1}-i_{6}$, for which the current is unknown.

We derive three of the six simultaneous equations needed by applying Kirchhoff's current law to any three of the four essential nodes. We use the nodes $b, c$, and e to get

$$
\begin{array}{r}
-i_{1}+i_{2}+i_{6}-I=0 \\
i_{1}-i_{3}-i_{5}=0 \\
i_{3}+i_{4}-i_{2}=0 \tag{4.1}
\end{array}
$$

We derive the remaining three equations by applying Kirchhoff's voltage law around three meshes. Because the circuit has four meshes, we need to dismiss one mesh. We choose $R_{7}-I$, because we don't know the voltage across $I .{ }^{1}$

Using the other three meshes gives

$$
\begin{align*}
R_{1} i_{1}+R_{5} i_{2}+i_{3}\left(R_{2}+R_{3}\right)-v_{1} & =0 \\
-i_{3}\left(R_{2}+R_{3}\right)+i_{4} R_{6}+i_{5} R_{4}-v_{2} & =0 \\
-i_{2} R_{5}+i_{6} R_{7}-i_{4} R_{6} & =0 \tag{4.2}
\end{align*}
$$

Rearranging Eqs. 4.1 and 4.2 to facilitate their solution yields the set

$$
\begin{array}{r}
-i_{1}+i_{2}+0 i_{3}+0 i_{4}+0 i_{5}+i_{6}=I, \\
i_{1}+0 i_{2}-i_{3}+0 i_{4}-i_{5}+0 i_{6}=0, \\
0 i_{1}-i_{2}+i_{3}+i_{4}+0 i_{5}+0 i_{6}=0, \\
R_{1} i_{1}+R_{5} i_{2}+\left(R_{2}+R_{3}\right) i_{3}+0 i_{4}+0 i_{5}+0 i_{6}=v_{1} \\
0 i_{1}+0 i_{2}-\left(R_{2}+R_{3}\right) i_{3}+R_{6} i_{4}+R_{4} i_{5}+0 i_{6}=v_{2} \\
0 i_{1}-R_{5} i_{2}+0 i_{3}-R_{6} i_{4}+0 i_{5}+R_{7} i_{6}=0 \tag{4.3}
\end{array}
$$

Note that summing the current at the $n$th node ( g in this example) gives

$$
\begin{equation*}
i_{5}-i_{4}-i_{6}+I=0 \tag{4.4}
\end{equation*}
$$

[^2]Equation 4.4 is not independent, because we can derive it by summing Eqs. 4.1 and then multiplying the sum by -1 . Thus Eq. 4.4 is a linear combination of Eqs. 4.1 and therefore is not independent of them. We now carry the procedure one step further. By introducing new variables, we can describe a circuit with just $n-1$ equations or just $b-(n-1)$ equations. Therefore these new variables allow us to obtain a solution by manipulating fewer equations, a desirable goal even if a computer is to be used to obtain a numerical solution.

The new variables are known as node voltages and mesh currents. The node-voltage method enables us to describe a circuit in terms of $n_{e}-1$ equations; the mesh-current method enables us to describe a circuit in terms of $b_{e}-\left(n_{e}-1\right)$ equations. We begin in Section 4.2 with the nodevoltage method.

NOTE: Assess your understanding of this material by trying Chapter Problems 4.2 and 4.3.

## 4.2 Introduction to the Node-Voltage Method

We introduce the node-voltage method by using the essential nodes of the circuit. The first step is to make a neat layout of the circuit so that no branches cross over and to mark clearly the essential nodes on the circuit diagram, as in Fig. 4.5. This circuit has three essential nodes $\left(n_{e}=3\right)$; therefore, we need two $\left(n_{e}-1\right)$ node-voltage equations to describe the circuit. The next step is to select one of the three essential nodes as a reference node. Although theoretically the choice is arbitrary, practically the choice for the reference node often is obvious. For example, the node with the most branches is usually a good choice. The optimum choice of the reference node (if one exists) will become apparent after you have gained some experience using this method. In the circuit shown in Fig. 4.5, the lower node connects the most branches, so we use it as the reference node. We flag the chosen reference node with the symbol $\boldsymbol{\nabla}$, as in Fig. 4.6.

After selecting the reference node, we define the node voltages on the circuit diagram. A node voltage is defined as the voltage rise from the reference node to a nonreference node. For this circuit, we must define two node voltages, which are denoted $v_{1}$ and $v_{2}$ in Fig. 4.6.

We are now ready to generate the node-voltage equations. We do so by first writing the current leaving each branch connected to a nonreference node as a function of the node voltages and then summing these currents to zero in accordance with Kirchhoff's current law. For the circuit in Fig. 4.6, the current away from node 1 through the $1 \Omega$ resistor is the voltage drop across the resistor divided by the resistance (Ohm's law). The voltage drop across the resistor, in the direction of the current away from the node, is $v_{1}-10$. Therefore the current in the $1 \Omega$ resistor is $\left(v_{1}-10\right) / 1$. Figure 4.7 depicts these observations. It shows the $10 \mathrm{~V}-1 \Omega$ branch, with the appropriate voltages and current.

This same reasoning yields the current in every branch where the current is unknown. Thus the current away from node 1 through the $5 \Omega$ resistor is $v_{1} / 5$, and the current away from node 1 through the $2 \Omega$ resistor is $\left(v_{1}-v_{2}\right) / 2$. The sum of the three currents leaving node 1 must equal zero; therefore the node-voltage equation derived at node 1 is

$$
\begin{equation*}
\frac{v_{1}-10}{1}+\frac{v_{1}}{5}+\frac{v_{1}-v_{2}}{2}=0 \tag{4.5}
\end{equation*}
$$

image_name:Figure 4.5
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '1Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R3', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'b', 'N2': 'd'
'name': 'R4', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'V1', 'type': 'VoltageSource', 'value': '10V', 'ports': {'Np': 'a', 'Nn': 'd'
'name': 'I1', 'type': 'CurrentSource', 'value': '2A', 'ports': {'Np': 'd', 'Nn': 'c'
]
extrainfo:The circuit consists of a voltage source, a current source, and four resistors arranged in a network. The node-voltage method is used for analysis.


Figure 4.5 $\triangle \mathrm{A}$ circuit used to illustrate the node-voltage method of circuit analysis.
image_name:Figure 4.6
description:
[
'name': '10V', 'type': 'VoltageSource', 'value': '10V', 'ports': {'Np': '3', 'Nn': 'GND'
'name': '1Ω', 'type': 'Resistor', 'value': '1Ω', 'ports': {'N1': '3', 'N2': '1'
'name': '2Ω', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': '1', 'N2': '2'
'name': '5Ω', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': '1', 'N2': 'GND'
'name': '10Ω', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': '2', 'N2': 'GND'
'name': '2A', 'type': 'CurrentSource', 'value': '2A', 'ports': {'Np': 'GND', 'Nn': '2'
]
extrainfo:The circuit consists of a voltage source, a current source, and four resistors arranged in a network. The node-voltage method is used for analysis. Node voltages v1 and v2 are defined at nodes 1 and 2 respectively. The node-voltage equation at node 2 is given by (v2-v1)/2 + v2/10 - 2 = 0.


Figure 4.6 $\triangle$ The circuit shown in Fig. 4.5 with a reference node and the node voltages.
image_name:Figure 4.7
description:
[
'name': '10 V', 'type': 'VoltageSource', 'value': '10 V', 'ports': {'Np': '1', 'Nn': 'GND'
'name': '1 Ω', 'type': 'Resistor', 'value': '1 Ω', 'ports': {'N1': '1', 'N2': '2'
]
extrainfo:The circuit consists of a 10 V voltage source and a 1 Ω resistor. The current i flows from node 1 to node 2 through the resistor. The voltage at node 1 is v1.


Figure 4.7 $\triangle$ Computation of the branch current $i$.

The node-voltage equation derived at node 2 is

$$
\begin{equation*}
\frac{v_{2}-v_{1}}{2}+\frac{v_{2}}{10}-2=0 \tag{4.6}
\end{equation*}
$$

Note that the first term in Eq. 4.6 is the current away from node 2 through the $2 \Omega$ resistor, the second term is the current away from node 2 through the $10 \Omega$ resistor, and the third term is the current away from node 2 through the current source.

Equations 4.5 and 4.6 are the two simultaneous equations that describe the circuit shown in Fig. 4.6 in terms of the node voltages $v_{1}$ and $v_{2}$. Solving for $v_{1}$ and $v_{2}$ yields

$$
\begin{aligned}
& v_{1}=\frac{100}{11}=9.09 \mathrm{~V} \\
& v_{2}=\frac{120}{11}=10.91 \mathrm{~V}
\end{aligned}
$$

Once the node voltages are known, all the branch currents can be calculated. Once these are known, the branch voltages and powers can be calculated. Example 4.2 illustrates the use of the node-voltage method.

#### Example 4.2 Using the Node-Voltage Method

a) Use the node-voltage method of circuit analysis to find the branch currents $i_{\mathrm{a}}, i_{\mathrm{b}}$, and $i_{\mathrm{c}}$ in the circuit shown in Fig. 4.8.
b) Find the power associated with each source, and state whether the source is delivering or absorbing power.

#### Solution

a) We begin by noting that the circuit has two essential nodes; thus we need to write a single nodevoltage expression. We select the lower node as the reference node and define the unknown node voltage as $v_{1}$. Figure 4.9 illustrates these decisions. Summing the currents away from node 1 generates the node-voltage equation

$$
\frac{v_{1}-50}{5}+\frac{v_{1}}{10}+\frac{v_{1}}{40}-3=0
$$

Solving for $v_{1}$ gives

$$
v_{1}=40 \mathrm{~V}
$$

Hence

$$
\begin{gathered}
i_{\mathrm{a}}=\frac{50-40}{5}=2 \mathrm{~A} \\
i_{\mathrm{b}}=\frac{40}{10}=4 \mathrm{~A} \\
i_{\mathrm{c}}=\frac{40}{40}=1 \mathrm{~A}
\end{gathered}
$$

image_name:Figure 4.8
description:
[
'name': '50V', 'type': 'VoltageSource', 'value': '50V', 'ports': {'Np': 'a', 'Nn': 'b'
'name': '5Ω', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': '10Ω', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'c', 'N2': 'b'
'name': '40Ω', 'type': 'Resistor', 'value': '40Ω', 'ports': {'N1': 'c', 'N2': 'b'
'name': '3A', 'type': 'CurrentSource', 'value': '3A', 'ports': {'Np': 'b', 'Nn': 'c'
]
extrainfo:The circuit consists of a 50V voltage source connected to a 5Ω resistor, which is in series with a parallel combination of a 10Ω resistor, a 40Ω resistor, and a 3A current source. The node voltage at 'c' is 40V.


Figure 4.8 $\triangle$ The circuit for Example 4.2.
image_name:Figure 4.9
description:
[
'name': 'V1', 'type': 'VoltageSource', 'value': '50V', 'ports': {'Np': '2', 'Nn': '3'
'name': 'R1', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': '2', 'N2': '1'
'name': 'R2', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': '1', 'N2': '3'
'name': 'R3', 'type': 'Resistor', 'value': '40Ω', 'ports': {'N1': '1', 'N2': '3'
'name': 'I1', 'type': 'CurrentSource', 'value': '3A', 'ports': {'Np': '3', 'Nn': '1'
]
extrainfo:The circuit consists of a 50V voltage source connected to a 5Ω resistor, which is in series with a parallel combination of a 10Ω resistor, a 40Ω resistor, and a 3A current source. The node voltage at 'c' is 40V. The power calculations show the 50V source delivers -100W and the 3A source delivers -120W, confirming the total delivered power is 220W.


Figure 4.9 $\boldsymbol{\Delta}$ The circuit shown in Fig. 4.8 with a reference node and the unknown node voltage $v_{1}$.
b) The power associated with the 50 V source is

$$
p_{50 \mathrm{~V}}=-50 i_{\mathrm{a}}=-100 \mathrm{~W} \text { (delivering) }
$$

The power associated with the 3 A source is $p_{3 \mathrm{~A}}=-3 v_{1}=-3(40)=-120 \mathrm{~W}$ (delivering).
We check these calculations by noting that the total delivered power is 220 W . The total power absorbed by the three resistors is 4(5) + 16(10) $+1(40)$, or 220 W , as we calculated and as it must be.

ASSESSMENT PROBLEMS

Objective 1-Understand and be able to use the node-voltage method

4.1 a) For the circuit shown, use the node-voltage method to find $v_{1}, v_{2}$, and $i_{1}$.
b) How much power is delivered to the circuit by the 15 A source?
c) Repeat (b) for the 5 A source
image_name:4.1
description:
[
'name': '15A', 'type': 'CurrentSource', 'value': '15A', 'ports': {'Np': 'b', 'Nn': 'a'
'name': '60Ω', 'type': 'Resistor', 'value': '60Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '15Ω', 'type': 'Resistor', 'value': '15Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '5Ω', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': '2Ω', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'c', 'N2': 'b'
'name': '5A', 'type': 'CurrentSource', 'value': '5A', 'ports': {'Np': 'c', 'Nn': 'b'
]
extrainfo:The circuit consists of two current sources and four resistors connected in a network. Node 'a' is connected to a 15A current source and two resistors (60Ω and 15Ω) in parallel. Node 'c' connects the 5Ω and 2Ω resistors, with a 5A current source connected between node 'c' and node 'b'. The node-voltage method is used to find voltages v1, v2, and current i1.


Answer: (a) $60 \mathrm{~V}, 10 \mathrm{~V}, 10 \mathrm{~A}$;
(b) 900 W ;
(c) -50 W .

NOTE: Also try Chapter Problems 4.6, 4.11, and 4.13.
4.2 Use the node-voltage method to find $v$ in the circuit shown.
image_name:circuit shown
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '1Ω', 'ports': {'N1': 'a', 'N2': 'e'
'name': 'R2', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R3', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R4', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'R5', 'type': 'Resistor', 'value': '12Ω', 'ports': {'N1': 'c', 'N2': 'e'
'name': 'I1', 'type': 'CurrentSource', 'value': '4.5A', 'ports': {'Np': 'e', 'Nn': 'a'
'name': 'V1', 'type': 'VoltageSource', 'value': '30V', 'ports': {'Np': 'd', 'Nn': 'e'
]
extrainfo:The circuit consists of a current source, a voltage source, and five resistors. The nodes are labeled a, b, c, d, and e, with node e being the ground. The voltage across nodes b and e is labeled as v.


## 4.3 The Node-Voltage Method and Dependent Sources

If the circuit contains dependent sources, the node-voltage equations must be supplemented with the constraint equations imposed by the presence of the dependent sources. Example 4.3 illustrates the application of the node-voltage method to a circuit containing a dependent source.

#### Example 4.3 Using the Node-Voltage Method with Dependent Sources

Use the node-voltage method to find the power dissipated in the $5 \Omega$ resistor in the circuit shown in Fig. 4.10.
image_name:Figure 4.10
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'R2', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'R3', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'd', 'N2': 'b'
'name': 'R4', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'c', 'N2': 'b'
'name': 'R5', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'd', 'N2': 'e'
'name': 'V1', 'type': 'VoltageSource', 'value': '20V', 'ports': {'Np': 'a', 'Nn': 'b'
'name': 'G1', 'type': 'CurrentControlledVoltageSource', 'value': '8iφ', 'ports': {'Np': 'e', 'Nn': 'b'
]
extrainfo:The circuit contains a dependent voltage source G1 controlled by the current iφ flowing through R2. The main goal is to find the power dissipated in the 5Ω resistor.


Figure 4.10 $\Delta$ The circuit for Example 4.3.

#### Solution

We begin by noting that the circuit has three essential nodes. Hence we need two node-voltage equations to describe the circuit. Four branches terminate
on the lower node, so we select it as the reference node. The two unknown node voltages are defined on the circuit shown in Fig. 4.11. Summing the currents away from node 1 generates the equation

$$
\frac{v_{1}-20}{2}+\frac{v_{1}}{20}+\frac{v_{1}-v_{2}}{5}=0
$$

Summing the currents away from node 2 yields

$$
\frac{v_{2}-v_{1}}{5}+\frac{v_{2}}{10}+\frac{v_{2}-8 i_{\phi}}{2}=0
$$

As written, these two node-voltage equations contain three unknowns, namely, $v_{1}, v_{2}$, and $i_{\phi}$. To eliminate $i_{\phi}$ we must express this controlling current in terms of the node voltages, or

$$
i_{\phi}=\frac{v_{1}-v_{2}}{5}
$$

Substituting this relationship into the node 2 equation simplifies the two node-voltage equations to

$$
\begin{aligned}
0.75 v_{1}-0.2 v_{2} & =10 \\
-v_{1}+1.6 v_{2} & =0
\end{aligned}
$$

Solving for $v_{1}$ and $v_{2}$ gives

$$
v_{1}=16 \mathrm{~V}
$$

and

$$
v_{2}=10 \mathrm{~V}
$$

Then,

$$
\begin{aligned}
i_{\phi} & =\frac{16-10}{5}=1.2 \mathrm{~A} \\
p_{5 \Omega} & =(1.44)(5)=7.2 \mathrm{~W}
\end{aligned}
$$

A good exercise to build your problem-solving intuition is to reconsider this example, using node 2 as the reference node. Does it make the analysis easier or harder?
image_name:Figure 4.11
description:
[
'name': '20V', 'type': 'VoltageSource', 'value': '20V', 'ports': {'Np': 'a', 'Nn': 'GND'
'name': '2Ω', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'a', 'N2': '1'
'name': '20Ω', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': '1', 'N2': 'GND'
'name': '5Ω', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': '1', 'N2': '2'
'name': '2Ω', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': '2', 'N2': 'b'
'name': '10Ω', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': '2', 'N2': 'GND'
'name': '8iϕ', 'type': 'CurrentControlledVoltageSource', 'value': '8iϕ', 'ports': {'Np': 'b', 'Nn': 'GND'
]
extrainfo:The circuit includes a 20V voltage source connected to node 'a', and a current-controlled voltage source '8iϕ' at node 'b'. Nodes '1' and '2' are intermediate nodes with resistors connected to ground. The current 'iϕ' flows from node '1' to node '2' through the 5Ω resistor.


Figure 4.11 $\Delta$ The circuit shown in Fig. 4.10, with a reference node and the node voltages.

ASSESSMENT PROBLEM

Objective 1-Understand and be able to use the node-voltage method

4.3 a) Use the node-voltage method to find the power associated with each source in the circuit shown.
b) State whether the source is delivering power to the circuit or extracting power from the circuit.

Answer: (a) $p_{50 \mathrm{~V}}=-150 \mathrm{~W}, p_{3 i_{1}}=-144 \mathrm{~W}$, $p_{5 \mathrm{~A}}=-80 \mathrm{~W}$;
(b) all sources are delivering power to the
image_name:4.3
description:
[
'name': '50V', 'type': 'VoltageSource', 'value': '50V', 'ports': {'Np': 'a', 'Nn': 'GND'
'name': '5A', 'type': 'CurrentSource', 'value': '5A', 'ports': {'Np': 'GND', 'Nn': 'c'
'name': '6Ω', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '2Ω', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': '8Ω', 'type': 'Resistor', 'value': '8Ω', 'ports': {'N1': 'b', 'N2': 'GND'
'name': '4Ω', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'c', 'N2': 'GND'
'name': '3i₁', 'type': 'CurrentControlledCurrentSource', 'ports': {'Np': 'c', 'Nn': 'b'
]
extrainfo:The circuit includes a voltage source of 50V at node 'a' and a current source of 5A at node 'c'. There are resistors of 6Ω, 2Ω, 8Ω, and 4Ω connecting nodes 'a', 'b', 'c', and GND. A current-controlled current source (3i₁) is connected between nodes 'b' and 'c'.

circuit.

NOTE: Also try Chapter Problems 4.18 and 4.19.
image_name:Figure 4.12
description:
[
'name': 'V1', 'type': 'VoltageSource', 'value': '100V', 'ports': {'Np': '1', 'Nn': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': '1', 'N2': '2'
'name': 'R2', 'type': 'Resistor', 'value': '25Ω', 'ports': {'N1': '1', 'N2': 'GND'
'name': 'R3', 'type': 'Resistor', 'value': '50Ω', 'ports': {'N1': '2', 'N2': 'GND'
'name': 'I1', 'type': 'CurrentSource', 'value': '5A', 'ports': {'Np': 'GND', 'Nn': '2'
]
extrainfo:The circuit consists of a 100V voltage source, a 5A current source, and resistors of 10Ω, 25Ω, and 50Ω. It forms a loop with nodes labeled 1 and 2, with the ground as a reference node. Node voltages v1 and v2 are across the 25Ω and 50Ω resistors respectively.


Figure 4.12 $\triangle \mathrm{A}$ circuit with a known node voltage.

## 4.4 The Node-Voltage Method: Some Special Cases

When a voltage source is the only element between two essential nodes, the node-voltage method is simplified. As an example, look at the circuit in Fig. 4.12. There are three essential nodes in this circuit, which means that two simultaneous equations are needed. From these three essential nodes, a reference node has been chosen and two other nodes have been labeled. But the 100 V source constrains the voltage between node 1 and the reference node to 100 V . This means that there is only one unknown node voltage $\left(v_{2}\right)$. Solution of this circuit thus involves only a single nodevoltage equation at node 2 :

$$
\begin{equation*}
\frac{v_{2}-v_{1}}{10}+\frac{v_{2}}{50}-5=0 \tag{4.7}
\end{equation*}
$$

But $v_{1}=100 \mathrm{~V}$, so Eq. 4.7 can be solved for $v_{2}$ :

$$
\begin{equation*}
v_{2}=125 \mathrm{~V} \tag{4.8}
\end{equation*}
$$

Knowing $v_{2}$, we can calculate the current in every branch. You should verify that the current into node 1 in the branch containing the independent voltage source is 1.5 A .

In general, when you use the node-voltage method to solve circuits that have voltage sources connected directly between essential nodes, the number of unknown node voltages is reduced. The reason is that, whenever a voltage source connects two essential nodes, it constrains the difference between the node voltages at these nodes to equal the voltage of the source. Taking the time to see if you can reduce the number of unknowns in this way will simplify circuit analysis.

Suppose that the circuit shown in Fig. 4.13 is to be analyzed using the node-voltage method. The circuit contains four essential nodes, so we anticipate writing three node-voltage equations. However, two essential nodes are connected by an independent voltage source, and two other essential nodes are connected by a current-controlled dependent voltage source. Hence, there actually is only one unknown node voltage.

Choosing which node to use as the reference node involves several possibilities. Either node on each side of the dependent voltage source looks attractive because, if chosen, one of the node voltages would be known to be either $+10 i_{\phi}$ (left node is the reference) or $-10 i_{\phi}$ (right node is the reference). The lower node looks even better because one node voltage is immediately known ( 50 V ) and five branches terminate there. We therefore opt for the lower node as the reference.

Figure 4.14 shows the redrawn circuit, with the reference node flagged and the node voltages defined. Also, we introduce the current $i$ because we cannot express the current in the dependent voltage source branch as a function of the node voltages $v_{2}$ and $v_{3}$. Thus, at node 2

$$
\begin{equation*}
\frac{v_{2}-v_{1}}{5}+\frac{v_{2}}{50}+i=0 \tag{4.9}
\end{equation*}
$$

and at node 3

$$
\begin{equation*}
\frac{v_{3}}{100}-i-4=0 \tag{4.10}
\end{equation*}
$$

We eliminate $i$ simply by adding Eqs. 4.9 and 4.10 to get

$$
\begin{equation*}
\frac{v_{2}-v_{1}}{5}+\frac{v_{2}}{50}+\frac{v_{3}}{100}-4=0 \tag{4.11}
\end{equation*}
$$

The Concept of a Supernode

Equation 4.11 may be written directly, without resorting to the intermediate step represented by Eqs. 4.9 and 4.10. To do so, we consider nodes 2 and 3 to be a single node and simply sum the currents away from the node in terms of the node voltages $v_{2}$ and $v_{3}$. Figure 4.15 illustrates this approach.

When a voltage source is between two essential nodes, we can combine those nodes to form a supernode. Obviously, Kirchhoff's current law must hold for the supernode. In Fig. 4.15, starting with the $5 \Omega$ branch and moving counterclockwise around the supernode, we generate the equation

$$
\begin{equation*}
\frac{v_{2}-v_{1}}{5}+\frac{v_{2}}{50}+\frac{v_{3}}{100}-4=0 \tag{4.12}
\end{equation*}
$$

image_name:Figure 4.13
description:
[
'name': '50V', 'type': 'VoltageSource', 'value': '50V', 'ports': {'Np': 'a', 'Nn': 'd'
'name': 'Resistor1', 'type': 'Resistor', 'value': '40Ω', 'ports': {'N1': 'a', 'N2': 'd'
'name': 'Resistor2', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '10iϕ', 'type': 'CurrentControlledVoltageSource', 'value': '10iϕ', 'ports': {'Np': 'c', 'Nn': 'b'
'name': 'Resistor3', 'type': 'Resistor', 'value': '50Ω', 'ports': {'N1': 'b', 'N2': 'd'
'name': 'Resistor4', 'type': 'Resistor', 'value': '100Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'Current Source', 'type': 'CurrentSource', 'value': '4A', 'ports': {'Np': 'd', 'Nn': 'c'
]
extrainfo:The circuit contains a dependent voltage source controlled by the current iϕ through the 5Ω resistor. Node 'd' is a common ground for the circuit.


Figure 4.13 $\triangle \mathrm{A}$ circuit with a dependent voltage source connected between nodes.
image_name:Figure 4.14
description:
[
'name': '50V', 'type': 'VoltageSource', 'value': '50V', 'ports': {'Np': '1', 'Nn': 'GND'
'name': '5Ω', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': '1', 'N2': '2'
'name': '40Ω', 'type': 'Resistor', 'value': '40Ω', 'ports': {'N1': '1', 'N2': 'GND'
'name': '10iϕ', 'type': 'CurrentControlledVoltageSource', 'value': '10iϕ', 'ports': {'Np': '3', 'Nn': '2'
'name': '50Ω', 'type': 'Resistor', 'value': '50Ω', 'ports': {'N1': '2', 'N2': 'GND'
'name': '100Ω', 'type': 'Resistor', 'value': '100Ω', 'ports': {'N1': '3', 'N2': 'GND'
'name': '4A', 'type': 'CurrentSource', 'value': '4A', 'ports': {'Np': 'GND', 'Nn': '3'
]
extrainfo:The circuit contains a dependent voltage source controlled by the current iϕ through the 5Ω resistor. Node 'd' is a common ground for the circuit. Node 2 and Node 3 form a supernode.


Figure 4.15 $\triangle$ Considering nodes 2 and 3 to be a supernode.
image_name:Figure 4.16
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'b', 'N2': 'd'
'name': 'RC', 'type': 'Resistor', 'value': 'RC', 'ports': {'N1': 'a', 'N2': 'e'
'name': 'RE', 'type': 'Resistor', 'value': 'RE', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'V0', 'type': 'VoltageSource', 'value': 'V0', 'ports': {'Np': 'b', 'Nn': 'c'
'name': 'VCC', 'type': 'VoltageSource', 'value': 'VCC', 'ports': {'Np': 'a', 'Nn': 'd'
'name': 'βiB', 'type': 'CurrentControlledCurrentSource', 'ports': {'Np': 'e', 'Nn': 'c'
]
extrainfo:This circuit is a transistor amplifier configuration with a dependent current source βiB controlled by the base current iB. Node 'd' serves as the common ground. The circuit includes a supernode formed by nodes 'b' and 'c', simplifying analysis.


Figure 4.16 $\boldsymbol{\Delta}$ The transistor amplifier circuit shown in Fig. 2.24.
image_name:Figure 4.17
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'b', 'N2': 'd'
'name': 'RC', 'type': 'Resistor', 'value': 'RC', 'ports': {'N1': 'a', 'N2': 'e'
'name': 'RE', 'type': 'Resistor', 'value': 'RE', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'VCC', 'type': 'VoltageSource', 'value': 'VCC', 'ports': {'Np': 'a', 'Nn': 'd'
'name': 'βiB', 'type': 'CurrentControlledCurrentSource', 'ports': {'Np': 'e', 'Nn': 'c'
]
extrainfo:This circuit is a transistor amplifier configuration with a dependent current source βiB controlled by the base current iB. Node 'd' serves as the common ground. The circuit includes a supernode formed by nodes 'b' and 'c', simplifying analysis.


Figure 4.17 $\boldsymbol{\Delta}$ The circuit shown in Fig. 4.16, with voltages and the supernode identified.
which is identical to Eq. 4.11. Creating a supernode at nodes 2 and 3 has made the task of analyzing this circuit easier. It is therefore always worth taking the time to look for this type of shortcut before writing any equations.

After Eq. 4.12 has been derived, the next step is to reduce the expression to a single unknown node voltage. First we eliminate $v_{1}$ from the equation because we know that $v_{1}=50 \mathrm{~V}$. Next we express $v_{3}$ as a function of $v_{2}$ :

$$
\begin{equation*}
v_{3}=v_{2}+10 i_{\phi} \tag{4.13}
\end{equation*}
$$

We now express the current controlling the dependent voltage source as a function of the node voltages:

$$
\begin{equation*}
i_{\phi}=\frac{v_{2}-50}{5} \tag{4.14}
\end{equation*}
$$

Using Eqs. 4.13 and 4.14 and $v_{1}=50 \mathrm{~V}$ reduces Eq. 4.12 to

$$
\begin{aligned}
v_{2}\left(\frac{1}{50}+\frac{1}{5}+\frac{1}{100}+\frac{10}{500}\right) & =10+4+1 \\
v_{2}(0.25) & =15 \\
v_{2} & =60 \mathrm{~V}
\end{aligned}
$$

From Eqs. 4.13 and 4.14:

$$
\begin{aligned}
& i_{\phi}=\frac{60-50}{5}=2 \mathrm{~A} \\
& v_{3}=60+20=80 \mathrm{~V}
\end{aligned}
$$

Node-Voltage Analysis of the Amplifier Circuit

Let's use the node-voltage method to analyze the circuit first introduced in Section 2.5 and shown again in Fig. 4.16.

When we used the branch-current method of analysis in Section 2.5, we faced the task of writing and solving six simultaneous equations. Here we will show how nodal analysis can simplify our task.

The circuit has four essential nodes: Nodes a and d are connected by an independent voltage source as are nodes b and c . Therefore the problem reduces to finding a single unknown node voltage, because $\left(n_{e}-1\right)-2=1$. Using d as the reference node, combine nodes b and c into a supernode, label the voltage drop across $R_{2}$ as $v_{\mathrm{b}}$, and label the voltage drop across $R_{E}$ as $v_{\mathrm{c}}$, as shown in Fig. 4.17. Then,

$$
\begin{equation*}
\frac{v_{\mathrm{b}}}{R_{2}}+\frac{v_{\mathrm{b}}-V_{C C}}{R_{1}}+\frac{v_{\mathrm{c}}}{R_{E}}-\beta i_{B}=0 \tag{4.15}
\end{equation*}
$$

We now eliminate both $v_{\mathrm{c}}$ and $i_{B}$ from Eq. 4.15 by noting that

$$
\begin{align*}
& v_{\mathrm{c}}=\left(i_{B}+\beta i_{B}\right) R_{E}  \tag{4.16}\\
& v_{\mathrm{c}}=v_{\mathrm{b}}-V_{0} \tag{4.17}
\end{align*}
$$

Substituting Eqs. 4.16 and 4.17 into Eq. 4.15 yields

$$
\begin{equation*}
v_{\mathrm{b}}\left[\frac{1}{R_{1}}+\frac{1}{R_{2}}+\frac{1}{(1+\beta) R_{E}}\right]=\frac{V_{C C}}{R_{1}}+\frac{V_{0}}{(1+\beta) R_{E}} . \tag{4.18}
\end{equation*}
$$

Solving Eq. 4.18 for $v_{\mathrm{b}}$ yields

$$
\begin{equation*}
v_{\mathrm{b}}=\frac{V_{C C} R_{2}(1+\beta) R_{E}+V_{0} R_{1} R_{2}}{R_{1} R_{2}+(1+\beta) R_{E}\left(R_{1}+R_{2}\right)} \tag{4.19}
\end{equation*}
$$

Using the node-voltage method to analyze this circuit reduces the problem from manipulating six simultaneous equations (see Problem 2.27) to manipulating three simultaneous equations. You should verify that, when Eq. 4.19 is combined with Eqs. 4.16 and 4.17, the solution for $i_{B}$ is identical to Eq. 2.25. (See Problem 4.30.)

ASSESSMENT PROBLEMS

Objective 1-Understand and be able to use the node-voltage method

4.4 Use the node-voltage method to find $v_{o}$ in the circuit shown.

Answer: 24 V.
image_name:4.4
description:
[
'name': '10 V', 'type': 'VoltageSource', 'value': '10 V', 'ports': {'Np': 'a', 'Nn': 'd'
'name': '10 Ω', 'type': 'Resistor', 'value': '10 Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '30 Ω', 'type': 'Resistor', 'value': '30 Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': '20 Ω', 'type': 'Resistor', 'value': '20 Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': '40 Ω', 'type': 'Resistor', 'value': '40 Ω', 'ports': {'N1': 'b', 'N2': 'd'
'name': '20iΔ', 'type': 'CurrentControlledVoltageSource', 'value': '20iΔ', 'ports': {'Np': 'd', 'Nn': 'c'
]
extrainfo:The circuit uses the node-voltage method to find the output voltage vo across the 40 Ω resistor. The voltage-controlled voltage source is dependent on the current iΔ flowing through the 10 V source.

4.5 Use the node-voltage method to find $v$ in the circuit shown.

Answer: 8 V .
image_name:4.5
description:
[
'name': '4.8A', 'type': 'CurrentSource', 'value': '4.8A', 'ports': {'Np': 'b', 'Nn': 'a'
'name': '7.5Ω', 'type': 'Resistor', 'value': '7.5Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '2.5Ω', 'type': 'Resistor', 'value': '2.5Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': '10Ω', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'c', 'N2': 'b'
'name': '2.5Ω', 'type': 'Resistor', 'value': '2.5Ω', 'ports': {'N1': 'b', 'N2': 'd'
'name': '1Ω', 'type': 'Resistor', 'value': '1Ω', 'ports': {'N1': 'd', 'N2': 'e'
'name': '12V', 'type': 'VoltageSource', 'value': '12V', 'ports': {'Np': 'e', 'Nn': 'b'
'name': 'ix', 'type': 'CurrentControlledVoltageSource', 'ports': {'N1': 'd', 'N2': 'c'
]
extrainfo:The circuit is analyzed using the node-voltage method to find the voltage v across the 7.5Ω resistor. The current-controlled voltage source ix is dependent on the current ix flowing through the 7.5Ω resistor. The circuit includes a 4.8A current source, a 12V voltage source, and multiple resistors.

4.6 Use the node-voltage method to find $v_{1}$ in the circuit shown.

Answer: 48 V .
NOTE: Also try Chapter Problems 4.22, 4.23, and 4.26.
image_name:4.6
description:
[
'name': 'Voltage Source', 'type': 'VoltageSource', 'value': '60V', 'ports': {'Np': 'a', 'Nn': 'd'
'name': 'Resistor1', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'Resistor2', 'type': 'Resistor', 'value': '3Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'Resistor3', 'type': 'Resistor', 'value': '24Ω', 'ports': {'N1': 'b', 'N2': 'd'
'name': 'Resistor4', 'type': 'Resistor', 'value': '3Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': '6iϕ', 'type': 'CurrentControlledVoltageSource', 'value': '6iϕ', 'ports': {'Np': 'c', 'Nn': 'a'
]
extrainfo:The circuit is analyzed using the node-voltage method to find the voltage v1 across the 24Ω resistor. The voltage-controlled voltage source is dependent on the current iϕ flowing through the 3Ω resistor between nodes b and c. The circuit includes a 60V voltage source and multiple resistors.


## 4.5 Introduction to the Mesh-Current Method

As stated in Section 4.1, the mesh-current method of circuit analysis enables us to describe a circuit in terms of $b_{e}-\left(n_{e}-1\right)$ equations. Recall that a mesh is a loop with no other loops inside it. The circuit in Fig. 4.1(b) is shown again in Fig. 4.18, with current arrows inside each loop to distinguish it. Recall also that the mesh-current method is applicable only to planar circuits. The
image_name:Figure 4.18
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'd'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'd', 'N2': 'e'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'e', 'N2': 'f'
'name': 'R4', 'type': 'Resistor', 'value': 'R4', 'ports': {'N1': 'c', 'N2': 'f'
'name': 'R5', 'type': 'Resistor', 'value': 'R5', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R6', 'type': 'Resistor', 'value': 'R6', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'R7', 'type': 'Resistor', 'value': 'R7', 'ports': {'N1': 'd', 'N2': 'f'
'name': 'R8', 'type': 'Resistor', 'value': 'R8', 'ports': {'N1': 'c', 'N2': 'e'
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': 'a', 'Nn': 'b'
]
extrainfo:The circuit is analyzed using the mesh-current method with defined mesh currents i1, i2, i3, and i4. The circuit is planar and consists of a single voltage source and multiple resistors connected in a complex network.


Figure 4.18 $\boldsymbol{\Delta}$ The circuit shown in Fig. 4.1(b), with the mesh currents defined.
image_name:Figure 4.19
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'c', 'N2': 'b'
'name': 'v1', 'type': 'VoltageSource', 'value': 'v1', 'ports': {'Np': 'a', 'Nn': 'b'
'name': 'v2', 'type': 'VoltageSource', 'value': 'v2', 'ports': {'Np': 'd', 'Nn': 'b'
]
extrainfo:The circuit is analyzed using the mesh-current method with mesh currents i1, i2, and i3. It is a planar circuit with two voltage sources and three resistors, forming a complex network with four essential nodes.


Figure 4.19 - A circuit used to illustrate development of the mesh-current method of circuit analysis.
image_name:Figure 4.20
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'b', 'N2': 'd'
'name': 'v1', 'type': 'VoltageSource', 'value': 'v1', 'ports': {'Np': 'a', 'Nn': 'd'
'name': 'v2', 'type': 'VoltageSource', 'value': 'v2', 'ports': {'Np': 'c', 'Nn': 'd'
]
extrainfo:The circuit uses the mesh-current method with mesh currents i_a and i_b. It is a planar circuit with two voltage sources and three resistors, forming a complex network with four essential nodes (a, b, c, d).


Figure 4.20 $\triangle$ Mesh currents $i_{\mathrm{a}}$ and $i_{\mathrm{b}}$.
circuit in Fig. 4.18 contains seven essential branches where the current is unknown and four essential nodes. Therefore, to solve it via the mesh-current method, we must write four [7 - (4 - 1)] mesh-current equations.

A mesh current is the current that exists only in the perimeter of a mesh. On a circuit diagram it appears as either a closed solid line or an almost-closed solid line that follows the perimeter of the appropriate mesh. An arrowhead on the solid line indicates the reference direction for the mesh current. Figure 4.18 shows the four mesh currents that describe the circuit in Fig. 4.1(b). Note that by definition, mesh currents automatically satisfy Kirchhoff's current law. That is, at any node in the circuit, a given mesh current both enters and leaves the node.

Figure 4.18 also shows that identifying a mesh current in terms of a branch current is not always possible. For example, the mesh current $i_{2}$ is not equal to any branch current, whereas mesh currents $i_{1}, i_{3}$, and $i_{4}$ can be identified with branch currents. Thus measuring a mesh current is not always possible; note that there is no place where an ammeter can be inserted to measure the mesh current $i_{2}$. The fact that a mesh current can be a fictitious quantity doesn't mean that it is a useless concept. On the contrary, the mesh-current method of circuit analysis evolves quite naturally from the branch-current equations.

We can use the circuit in Fig. 4.19 to show the evolution of the meshcurrent technique. We begin by using the branch currents $\left(i_{1}, i_{2}\right.$, and $\left.i_{3}\right)$ to formulate the set of independent equations. For this circuit, $b_{e}=3$ and $n_{e}=2$. We can write only one independent current equation, so we need two independent voltage equations. Applying Kirchhoff's current law to the upper node and Kirchhoff's voltage law around the two meshes generates the following set of equations:

$$
\begin{align*}
i_{1} & =i_{2}+i_{3},  \tag{4.20}\\
v_{1} & =i_{1} R_{1}+i_{3} R_{3}  \tag{4.21}\\
-v_{2} & =i_{2} R_{2}-i_{3} R_{3} \tag{4.22}
\end{align*}
$$

We reduce this set of three equations to a set of two equations by solving Eq. 4.20 for $i_{3}$ and then substituting this expression into Eqs. 4.21 and 4.22:

$$
\begin{align*}
v_{1} & =i_{1}\left(R_{1}+R_{3}\right)-i_{2} R_{3}  \tag{4.23}\\
-v_{2} & =-i_{1} R_{3}+i_{2}\left(R_{2}+R_{3}\right) \tag{4.24}
\end{align*}
$$

We can solve Eqs. 4.23 and 4.24 for $i_{1}$ and $i_{2}$ to replace the solution of three simultaneous equations with the solution of two simultaneous equations. We derived Eqs. 4.23 and 4.24 by substituting the $n_{e}-1$ current equations into the $b_{e}-\left(n_{e}-1\right)$ voltage equations. The value of the mesh-current method is that, by defining mesh currents, we automatically eliminate the $n_{e}-1$ current equations. Thus the mesh-current method is equivalent to a systematic substitution of the $n_{e}-1$ current equations into the $b_{e}-\left(n_{e}-1\right)$ voltage equations. The mesh currents in Fig. 4.19 that are equivalent to eliminating the branch current $i_{3}$ from Eqs. 4.21 and 4.22 are shown in Fig. 4.20. We now apply Kirchhoff's voltage law around the two meshes, expressing all voltages across resistors in terms of the mesh currents, to get the equations

$$
\begin{align*}
v_{1} & =i_{\mathrm{a}} R_{1}+\left(i_{\mathrm{a}}-i_{\mathrm{b}}\right) R_{3}  \tag{4.25}\\
-v_{2} & =\left(i_{\mathrm{b}}-i_{\mathrm{a}}\right) R_{3}+i_{\mathrm{b}} R_{2} \tag{4.26}
\end{align*}
$$

Collecting the coefficients of $i_{\mathrm{a}}$ and $i_{\mathrm{b}}$ in Eqs. 4.25 and 4.26 gives

$$
\begin{align*}
v_{1} & =i_{\mathrm{a}}\left(R_{1}+R_{3}\right)-i_{\mathrm{b}} R_{3}  \tag{4.27}\\
-v_{2} & =-i_{\mathrm{a}} R_{3}+i_{\mathrm{b}}\left(R_{2}+R_{3}\right) \tag{4.28}
\end{align*}
$$

Note that Eqs. 4.27 and 4.28 and Eqs. 4.23 and 4.24 are identical in form, with the mesh currents $i_{\mathrm{a}}$ and $i_{\mathrm{b}}$ replacing the branch currents $i_{1}$ and $i_{2}$. Note also that the branch currents shown in Fig. 4.19 can be expressed in terms of the mesh currents shown in Fig. 4.20, or

$$
\begin{align*}
& i_{1}=i_{\mathrm{a}}  \tag{4.29}\\
& i_{2}=i_{\mathrm{b}}  \tag{4.30}\\
& i_{3}=i_{\mathrm{a}}-i_{\mathrm{b}} \tag{4.31}
\end{align*}
$$

The ability to write Eqs. $4.29-4.31$ by inspection is crucial to the meshcurrent method of circuit analysis. Once you know the mesh currents, you also know the branch currents. And once you know the branch currents, you can compute any voltages or powers of interest.

Example 4.4 illustrates how the mesh-current method is used to find source powers and a branch voltage.

#### Example 4.4 Using the Mesh-Current Method

a) Use the mesh-current method to determine the power associated with each voltage source in the circuit shown in Fig. 4.21.
b) Calculate the voltage $v_{o}$ across the $8 \Omega$ resistor.

#### Solution

a) To calculate the power associated with each source, we need to know the current in each source. The circuit indicates that these source currents will be identical to mesh currents. Also, note that the circuit has seven branches where
image_name:Figure 4.21
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': '8Ω', 'ports': {'N1': 'b', 'N2': 'e'
'name': 'R3', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R4', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'c', 'N2': 'e'
'name': 'R5', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'V1', 'type': 'VoltageSource', 'value': '40V', 'ports': {'Np': 'a', 'Nn': 'e'
'name': 'V2', 'type': 'VoltageSource', 'value': '20V', 'ports': {'Np': 'd', 'Nn': 'e'
]
extrainfo:The circuit consists of two voltage sources (40V and 20V) and five resistors. The voltage across the 8Ω resistor is labeled as vo. The circuit is set up to analyze using the mesh-current method.


Figure 4.21 A The circuit for Example 4.4.
the current is unknown and five nodes. Therefore we need three $[b-(n-1)=7-(5-1)]$ mesh-current equations to describe the circuit. Figure 4.22 shows the three mesh currents used to describe the circuit in Fig. 4.21. If we assume that the voltage drops are positive, the three mesh equations are

$$
\begin{array}{r}
-40+2 i_{\mathrm{a}}+8\left(i_{\mathrm{a}}-i_{\mathrm{b}}\right)=0 \\
8\left(i_{\mathrm{b}}-i_{\mathrm{a}}\right)+6 i_{\mathrm{b}}+6\left(i_{\mathrm{b}}-i_{\mathrm{c}}\right)=0 \\
6\left(i_{\mathrm{c}}-i_{\mathrm{b}}\right)+4 i_{\mathrm{c}}+20=0 \tag{4.32}
\end{array}
$$

Your calculator can probably solve these equations, or you can use a computer tool. Cramer's method is a useful tool when solving three or more simultaneous equations by hand. You can review this important tool in Appendix A. Reorganizing Eqs. 4.32 in anticipation of using your calculator, a computer program, or Cramer's method gives

$$
\begin{align*}
10 i_{\mathrm{a}}-8 i_{\mathrm{b}}+0 i_{\mathrm{c}} & =40 \\
-8 i_{\mathrm{a}}+20 i_{\mathrm{b}}-6 i_{\mathrm{c}} & =0 \\
0 i_{\mathrm{a}}-6 i_{\mathrm{b}}+10 i_{\mathrm{c}} & =-20 \tag{4.33}
\end{align*}
$$

The three mesh currents are

$$
\begin{aligned}
i_{\mathrm{a}} & =5.6 \mathrm{~A} \\
i_{\mathrm{b}} & =2.0 \mathrm{~A} \\
i_{\mathrm{c}} & =-0.80 \mathrm{~A}
\end{aligned}
$$

image_name:Figure 4.22
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R3', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'R4', 'type': 'Resistor', 'value': '8Ω', 'ports': {'N1': 'b', 'N2': 'e'
'name': 'R5', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'c', 'N2': 'e'
'name': 'V1', 'type': 'VoltageSource', 'value': '40V', 'ports': {'Np': 'a', 'Nn': 'e'
'name': 'V2', 'type': 'VoltageSource', 'value': '20V', 'ports': {'Np': 'd', 'Nn': 'e'
]
extrainfo:The circuit consists of two voltage sources and five resistors arranged in a mesh configuration. Mesh currents ia, ib, and ic flow through the circuit as indicated in the diagram.


Figure 4.22 $\Delta$ The three mesh currents used to analyze the circuit shown in Fig. 4.21.

The mesh current $i_{\mathrm{a}}$ is identical with the branch current in the 40 V source, so the power associated with this source is

$$
p_{40 \mathrm{~V}}=-40 i_{\mathrm{a}}=-224 \mathrm{~W}
$$


[^0]:    $\overline{1}$ We say more about this observation in Chapter 4.

[^1]:    ${ }^{1} \Delta$ and Y structures are present in a variety of useful circuits, not just resistive networks. Hence the $\Delta$-to-Y transformation is a helpful tool in circuit analysis.

[^2]:    $\overline{1}$ We say more about this decision in Section 4.7.


The minus sign means that this source is delivering power to the network. The current in the 20 V source is identical to the mesh current $i_{\mathrm{c}}$; therefore

$$
p_{20 \mathrm{~V}}=20 i_{\mathrm{c}}=-16 \mathrm{~W}
$$

The 20 V source also is delivering power to the network.
b) The branch current in the $8 \Omega$ resistor in the direction of the voltage drop $v_{o}$ is $i_{\mathrm{a}}-i_{\mathrm{b}}$. Therefore

$$
v_{o}=8\left(i_{\mathrm{a}}-i_{\mathrm{b}}\right)=8(3.6)=28.8 \mathrm{~V}
$$

ASSESSMENT PROBLEM

#Objective 2—Understand and be able to use the mesh-current method

4.7 Use the mesh-current method to find (a) the power delivered by the 80 V source to the circuit shown and (b) the power dissipated in the $8 \Omega$ resistor.

Answer: (a) 400 W ;
(b) 50 W .
image_name:circuit shown
description:
[
'name': '80V', 'type': 'VoltageSource', 'value': '80V', 'ports': {'Np': 'a', 'Nn': 'd'
'name': '30Ω', 'type': 'Resistor', 'value': '30Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': '5Ω', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '90Ω', 'type': 'Resistor', 'value': '90Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': '26Ω', 'type': 'Resistor', 'value': '26Ω', 'ports': {'N1': 'b', 'N2': 'd'
'name': '8Ω', 'type': 'Resistor', 'value': '8Ω', 'ports': {'N1': 'c', 'N2': 'd'
]
extrainfo:The circuit consists of a voltage source and five resistors forming two loops. The nodes are labeled a, b, c, and d.


NOTE: Also try Chapter Problems 4.32 and 4.36.

## 4.6 The Mesh-Current Method and Dependent Sources

If the circuit contains dependent sources, the mesh-current equations must be supplemented by the appropriate constraint equations. Example 4.5 illustrates the application of the mesh-current method when the circuit includes a dependent source.

#### Example 4.5 Using the Mesh-Current Method with Dependent Sources

Use the mesh-current method of circuit analysis to determine the power dissipated in the $4 \Omega$ resistor in the circuit shown in Fig. 4.23.
image_name:Figure 4.23
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '1Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'R2', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R3', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R4', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'b', 'N2': 'd'
'name': 'V1', 'type': 'VoltageSource', 'value': '50V', 'ports': {'Np': 'a', 'Nn': 'd'
'name': 'G1', 'type': 'CurrentControlledVoltageSource', 'value': '15iφ', 'ports': {'Np': 'c', 'Nn': 'd'
]
extrainfo:The circuit includes a dependent voltage source controlled by the current iφ through the 20Ω resistor. The mesh-current method involves three mesh currents to analyze the circuit.


Figure 4.23 $\boldsymbol{\Delta}$ The circuit for Example 4.5.

#### Solution

This circuit has six branches where the current is unknown and four nodes. Therefore we need three mesh currents to describe the circuit. They are
defined on the circuit shown in Fig. 4.24. The three mesh-current equations are

$$
\begin{align*}
& 50=5\left(i_{1}-i_{2}\right)+20\left(i_{1}-i_{3}\right) \\
& 0=5\left(i_{2}-i_{1}\right)+1 i_{2}+4\left(i_{2}-i_{3}\right) \\
& 0=20\left(i_{3}-i_{1}\right)+4\left(i_{3}-i_{2}\right)+15 i_{\phi} \tag{4.34}
\end{align*}
$$

We now express the branch current controlling the dependent voltage source in terms of the mesh currents as

$$
\begin{equation*}
i_{\phi}=i_{1}-i_{3}, \tag{4.35}
\end{equation*}
$$

which is the supplemental equation imposed by the presence of the dependent source. Substituting Eq. 4.35 into Eqs. 4.34 and collecting the coefficients of $i_{1}, i_{2}$, and $i_{3}$ in each equation generates

$$
\begin{aligned}
50 & =25 i_{1}-5 i_{2}-20 i_{3} \\
0 & =-5 i_{1}+10 i_{2}-4 i_{3} \\
0 & =-5 i_{1}-4 i_{2}+9 i_{3}
\end{aligned}
$$

image_name:Figure 4.24
description:
[
'name': 'V1', 'type': 'VoltageSource', 'value': '50V', 'ports': {'Np': 'a', 'Nn': 'd'
'name': 'R1', 'type': 'Resistor', 'value': '1Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'R2', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'b', 'N2': 'a'
'name': 'R3', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R4', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'd', 'N2': 'd'
'name': 'G1', 'type': 'CurrentControlledVoltageSource', 'value': '15iϕ', 'ports': {'Np': 'c', 'Nn': 'd'
]
extrainfo:The circuit consists of a voltage source, resistors, and a voltage-controlled voltage source. Mesh currents i1, i2, and i3 are defined, with iϕ being a dependent current. The power dissipated in the 4Ω resistor is calculated to be 16W.


Figure 4.24 The circuit shown in Fig. 4.23 with the three mesh currents.

Because we are calculating the power dissipated in the $4 \Omega$ resistor, we compute the mesh currents $i_{2}$ and $i_{3}$ :

$$
\begin{aligned}
& i_{2}=26 \mathrm{~A} \\
& i_{3}=28 \mathrm{~A}
\end{aligned}
$$

The current in the $4 \Omega$ resistor oriented from left to right is $i_{3}-i_{2}$, or 2 A . Therefore the power dissipated is

$$
p_{4 \Omega}=\left(i_{3}-i_{2}\right)^{2}(4)=(2)^{2}(4)=16 \mathrm{~W}
$$

What if you had not been told to use the meshcurrent method? Would you have chosen the nodevoltage method? It reduces the problem to finding one unknown node voltage because of the presence of two voltage sources between essential nodes. We present more about making such choices later.

ASSESSMENT PROBLEMS

Objective 2-Understand and be able to use the mesh-current method

4.8 a) Determine the number of mesh-current equations needed to solve the circuit shown.
b) Use the mesh-current method to find how much power is being delivered to the dependent voltage source.
image_name:Figure 4.8
description:
[
'name': '25V', 'type': 'VoltageSource', 'value': '25V', 'ports': {'Np': 'a', 'Nn': 'f'
'name': '10V', 'type': 'VoltageSource', 'value': '10V', 'ports': {'Np': 'e', 'Nn': 'f'
'name': 'Resistor1', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'a', 'N2': 'd'
'name': 'Resistor2', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'd', 'N2': 'e'
'name': 'Resistor3', 'type': 'Resistor', 'value': '3Ω', 'ports': {'N1': 'd', 'N2': 'c'
'name': 'Resistor4', 'type': 'Resistor', 'value': '14Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'Resistor5', 'type': 'Resistor', 'value': '1Ω', 'ports': {'N1': 'c', 'N2': 'f'
'name': '-3vφ', 'type': 'VoltageControlledVoltageSource', 'value': '-3vφ', 'ports': {'Np': 'b', 'Nn': 'a'
]
extrainfo:The circuit contains two independent voltage sources, five resistors, and one dependent voltage source. The dependent voltage source is controlled by the voltage across the 5Ω resistor.


NOTE: Also try Chapter Problems 4.39 and 4.40.

Answer: (a) 3;
(b) -36 W .
4.9 Use the mesh-current method to find $v_{o}$ in the circuit shown.
image_name:circuit shown
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'R2', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R3', 'type': 'Resistor', 'value': '8Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R4', 'type': 'Resistor', 'value': '8Ω', 'ports': {'N1': 'b', 'N2': 'd'
'name': 'V1', 'type': 'VoltageSource', 'value': '25V', 'ports': {'Np': 'a', 'Nn': 'd'
'name': 'V2', 'type': 'VoltageControlledVoltageSource', 'value': '5iφ', 'ports': {'Np': 'c', 'Nn': 'd'
]
extrainfo:The circuit contains two independent voltage sources, five resistors, and one dependent voltage source. The dependent voltage source is controlled by the voltage across the 5Ω resistor.


## 4.7 The Mesh-Current Method: Some Special Cases

When a branch includes a current source, the mesh-current method requires some additional manipulations. The circuit shown in Fig. 4.25 depicts the nature of the problem.

We have defined the mesh currents $i_{\mathrm{a}}, i_{\mathrm{b}}$, and $i_{\mathrm{c}}$, as well as the voltage across the 5 A current source, to aid the discussion. Note that the circuit contains five essential branches where the current is unknown and four essential nodes. Hence we need to write two [5 - (4 - 1)] mesh-current
image_name:Figure 4.25
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'R2', 'type': 'Resistor', 'value': '3Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R3', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R4', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'd', 'N2': 'e'
'name': 'R5', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'e', 'N2': 'f'
'name': 'V1', 'type': 'VoltageSource', 'value': '100V', 'ports': {'Np': 'a', 'Nn': 'd'
'name': 'V2', 'type': 'VoltageSource', 'value': '50V', 'ports': {'Np': 'c', 'Nn': 'f'
'name': 'I1', 'type': 'CurrentSource', 'value': '5A', 'ports': {'Np': 'e', 'Nn': 'b'
]
extrainfo:The circuit illustrates mesh analysis with a supermesh due to the presence of a 5 A current source. The mesh currents are defined as ia, ib, and ic. The current source reduces the number of unknown mesh currents by one, simplifying the analysis.

Figure 4.25 $\triangle$ A circuit illustrating mesh analysis when a branch contains an independent current source.
image_name:Figure 4.26
description:
[
'name': 'V1', 'type': 'VoltageSource', 'value': '100V', 'ports': {'Np': 'a', 'Nn': 'e'
'name': 'V2', 'type': 'VoltageSource', 'value': '50V', 'ports': {'Np': 'c', 'Nn': 'd'
'name': 'R1', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'R2', 'type': 'Resistor', 'value': '3Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R3', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R4', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'e', 'N2': 'f'
'name': 'R5', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'f', 'N2': 'd'
]
extrainfo:The circuit features a supermesh due to the 5A current source between nodes b and e, reducing the number of independent mesh currents. The mesh currents are labeled as ia, ib, and ic for analysis. The presence of the current source constrains the difference between ia and ic to equal 5 A.


Figure 4.26 $\Delta$ The circuit shown in Fig. 4.25, illustrating the concept of a supermesh.
equations to solve the circuit. The presence of the current source reduces the three unknown mesh currents to two such currents, because it constrains the difference between $i_{\mathrm{a}}$ and $i_{\mathrm{c}}$ to equal 5 A . Hence, if we know $i_{\mathrm{a}}$, we know $i_{\mathrm{c}}$, and vice versa.

However, when we attempt to sum the voltages around either mesh a or mesh c, we must introduce into the equations the unknown voltage across the 5 A current source. Thus, for mesh a:

$$
\begin{equation*}
100=3\left(i_{\mathrm{a}}-i_{\mathrm{b}}\right)+v+6 i_{\mathrm{a}} \tag{4.36}
\end{equation*}
$$

and for mesh c:

$$
\begin{equation*}
-50=4 i_{\mathrm{c}}-v+2\left(i_{\mathrm{c}}-i_{\mathrm{b}}\right) \tag{4.37}
\end{equation*}
$$

We now add Eqs. 4.36 and 4.37 to eliminate $v$ and obtain

$$
\begin{equation*}
50=9 i_{\mathrm{a}}-5 i_{\mathrm{b}}+6 i_{\mathrm{c}} \tag{4.38}
\end{equation*}
$$

Summing voltages around mesh b gives

$$
\begin{equation*}
0=3\left(i_{\mathrm{b}}-i_{\mathrm{a}}\right)+10 i_{\mathrm{b}}+2\left(i_{\mathrm{b}}-i_{\mathrm{c}}\right) \tag{4.39}
\end{equation*}
$$

We reduce Eqs. 4.38 and 4.39 to two equations and two unknowns by using the constraint that

$$
\begin{equation*}
i_{\mathrm{c}}-i_{\mathrm{a}}=5 \tag{4.40}
\end{equation*}
$$

We leave to you the verification that, when Eq. 4.40 is combined with Eqs. 4.38 and 4.39, the solutions for the three mesh currents are

$$
i_{\mathrm{a}}=1.75 \mathrm{~A}, \quad i_{\mathrm{b}}=1.25 \mathrm{~A}, \quad \text { and } \quad i_{\mathrm{c}}=6.75 \mathrm{~A}
$$

The Concept of a Supermesh

We can derive Eq. 4.38 without introducing the unknown voltage $v$ by using the concept of a supermesh. To create a supermesh, we mentally remove the current source from the circuit by simply avoiding this branch when writing the mesh-current equations. We express the voltages around the supermesh in terms of the original mesh currents. Figure 4.26 illustrates the supermesh concept. When we sum the voltages around the supermesh (denoted by the dashed line), we obtain the equation

$$
\begin{equation*}
-100+3\left(i_{\mathrm{a}}-i_{\mathrm{b}}\right)+2\left(i_{\mathrm{c}}-i_{\mathrm{b}}\right)+50+4 i_{\mathrm{c}}+6 i_{\mathrm{a}}=0 \tag{4.41}
\end{equation*}
$$

which reduces to

$$
\begin{equation*}
50=9 i_{\mathrm{a}}-5 i_{\mathrm{b}}+6 i_{\mathrm{c}} \tag{4.42}
\end{equation*}
$$

Note that Eqs. 4.42 and 4.38 are identical. Thus the supermesh has eliminated the need for introducing the unknown voltage across the current source. Once again, taking time to look carefully at a circuit to identify a shortcut such as this provides a big payoff in simplifying the analysis.

Mesh-Current Analysis of the Amplifier Circuit

We can use the circuit first introduced in Section 2.5 (Fig. 2.24) to illustrate how the mesh-current method works when a branch contains a dependent current source. Figure 4.27 shows that circuit, with the three mesh currents denoted $i_{\mathrm{a}}, i_{\mathrm{b}}$, and $i_{\mathrm{c}}$. This circuit has four essential nodes and five essential branches where the current is unknown. Therefore we know that the circuit can be analyzed in terms of two [5-(4-1)] mesh-current equations. Although we defined three mesh currents in Fig. 4.27, the dependent current source forces a constraint between mesh currents $i_{\mathrm{a}}$ and $i_{\mathrm{c}}$, so we have only two unknown mesh currents. Using the concept of the supermesh, we redraw the circuit as shown in Fig. 4.28.

We now sum the voltages around the supermesh in terms of the mesh currents $i_{\mathrm{a}}, i_{\mathrm{b}}$, and $i_{\mathrm{c}}$ to obtain

$$
\begin{equation*}
R_{1} i_{\mathrm{a}}+v_{C C}+R_{E}\left(i_{\mathrm{c}}-i_{\mathrm{b}}\right)-V_{0}=0 \tag{4.43}
\end{equation*}
$$

The mesh $b$ equation is

$$
\begin{equation*}
R_{2} i_{\mathrm{b}}+V_{0}+R_{E}\left(i_{\mathrm{b}}-i_{\mathrm{c}}\right)=0 \tag{4.44}
\end{equation*}
$$

The constraint imposed by the dependent current source is

$$
\begin{equation*}
\beta i_{\mathrm{B}}=i_{\mathrm{a}}-i_{\mathrm{c}} \tag{4.45}
\end{equation*}
$$

The branch current controlling the dependent current source, expressed as a function of the mesh currents, is

$$
\begin{equation*}
i_{\mathrm{B}}=i_{\mathrm{b}}-i_{\mathrm{a}} \tag{4.46}
\end{equation*}
$$

From Eqs. 4.45 and 4.46,

$$
\begin{equation*}
i_{\mathrm{c}}=(1+\beta) i_{\mathrm{a}}-\beta i_{\mathrm{b}} \tag{4.47}
\end{equation*}
$$

We now use Eq. 4.47 to eliminate $i_{\mathrm{c}}$ from Eqs. 4.43 and 4.44:

$$
\begin{align*}
& {\left[R_{1}+(1+\beta) R_{E}\right] i_{\mathrm{a}}-(1+\beta) R_{E} i_{\mathrm{b}}=V_{0}-V_{C C}}  \tag{4.48}\\
& -(1+\beta) R_{E} i_{\mathrm{a}}+\left[R_{2}+(1+\beta) R_{E}\right] i_{\mathrm{b}}=-V_{0} \tag{4.49}
\end{align*}
$$

You should verify that the solution of Eqs. 4.48 and 4.49 for $i_{\mathrm{a}}$ and $i_{\mathrm{b}}$ gives

$$
\begin{align*}
i_{\mathrm{a}} & =\frac{V_{0} R_{2}-V_{C C} R_{2}-V_{C C}(1+\beta) R_{E}}{R_{1} R_{2}+(1+\beta) R_{E}\left(R_{1}+R_{2}\right)},  \tag{4.50}\\
i_{\mathrm{b}} & =\frac{-V_{0} R_{1}-(1+\beta) R_{E} V_{C C}}{R_{1} R_{2}+(1+\beta) R_{E}\left(R_{1}+R_{2}\right)} . \tag{4.51}
\end{align*}
$$

We also leave you to verify that, when Eqs. 4.50 and 4.51 are used to find $i_{\mathrm{B}}$, the result is the same as that given by Eq. 2.25 .
image_name:Figure 4.27
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'd'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'RC', 'type': 'Resistor', 'value': 'RC', 'ports': {'N1': 'd', 'N2': 'e'
'name': 'RE', 'type': 'Resistor', 'value': 'RE', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'V0', 'type': 'VoltageSource', 'value': 'V0', 'ports': {'Np': 'a', 'Nn': 'b'
'name': 'VCC', 'type': 'VoltageSource', 'value': 'VCC', 'ports': {'Np': 'd', 'Nn': 'c'
'name': 'βiB', 'type': 'CurrentControlledCurrentSource', 'ports': {'Np': 'e', 'Nn': 'b'
]
extrainfo:The circuit uses the mesh-current method with mesh currents i_a, i_b, and i_c. It includes resistors R1, R2, RC, and RE, voltage sources V0 and VCC, and a dependent current source βiB.


Figure 4.27 $\triangle$ The circuit shown in Fig. 2.24 with the mesh currents $i_{\mathrm{a}}, i_{\mathrm{b}}$, and $i_{\mathrm{c}}$.
image_name:Figure 4.28
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'c', 'N2': 'b'
'name': 'RC', 'type': 'Resistor', 'value': 'RC', 'ports': {'N1': 'a', 'N2': 'e'
'name': 'RE', 'type': 'Resistor', 'value': 'RE', 'ports': {'N1': 'd', 'N2': 'b'
'name': 'V0', 'type': 'VoltageSource', 'value': 'V0', 'ports': {'Np': 'c', 'Nn': 'd'
'name': 'VCC', 'type': 'VoltageSource', 'value': 'VCC', 'ports': {'Np': 'a', 'Nn': 'b'
]
extrainfo:The circuit employs the mesh-current method with mesh currents i_a, i_b, and i_c. The supermesh is created due to the presence of the dependent current source βiB.


Figure $4.28 \triangle$ The circuit shown in Fig. 4.27, depicting the supermesh created by the presence of the dependent current source.

ASSESSMENT PROBLEMS

Objective 2-Understand and be able to use the mesh-current method

4.10 Use the mesh-current method to find the power dissipated in the $2 \Omega$ resistor in the circuit shown.

Answer: 72 W.
4.11 Use the mesh-current method to find the mesh current $i_{\mathrm{a}}$ in the circuit shown.

Answer: 15 A.
4.12 Use the mesh-current method to find the power dissipated in the $1 \Omega$ resistor in the circuit shown.

Answer: 36 W .
image_name:4.10
description:
[
'name': '30V', 'type': 'VoltageSource', 'value': '30V', 'ports': {'Np': 'a', 'Nn': 'd'
'name': '3Ω', 'type': 'Resistor', 'value': '3Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '8Ω', 'type': 'Resistor', 'value': '8Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': '2Ω', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'b', 'N2': 'e'
'name': '5Ω', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'c', 'N2': 'f'
'name': '6Ω', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'd', 'N2': 'e'
'name': '4Ω', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'e', 'N2': 'f'
'name': '16A', 'type': 'CurrentSource', 'value': '16A', 'ports': {'Np': 'f', 'Nn': 'c'
]
extrainfo:The circuit diagram named '4.10' consists of multiple loops and uses both independent and dependent sources. It includes resistors, voltage sources, current sources, and a voltage-controlled current source. The circuit is designed to analyze the power dissipation in specific resistors using the mesh-current method.
image_name:4.11
description:
[
'name': '75V', 'type': 'VoltageSource', 'value': '75V', 'ports': {'Np': 'a', 'Nn': 'd'
'name': '10A', 'type': 'CurrentSource', 'value': '10A', 'ports': {'Np': 'c', 'Nn': 'a'
'name': '2Ω', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'b', 'N2': 'e'
'name': '5Ω', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'b', 'N2': 'd'
'name': '1Ω', 'type': 'Resistor', 'value': '1Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': '2vϕ/5', 'type': 'VoltageControlledCurrentSource', 'ports': {'N1': 'c', 'N2': 'd'
]
extrainfo:The circuit diagram consists of three sections with various voltage and current sources, resistors, and a voltage-controlled current source. The mesh-current method is used to analyze the circuit, focusing on finding mesh currents and power dissipation in specific resistors.
image_name:4.12
description:
[
'name': '10V', 'type': 'VoltageSource', 'value': '10V', 'ports': {'Np': 'a', 'Nn': 'd'
'name': '2A', 'type': 'CurrentSource', 'value': '2A', 'ports': {'Np': 'a', 'Nn': 'b'
'name': '2Ω', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': '2Ω', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': '6V', 'type': 'VoltageSource', 'value': '6V', 'ports': {'Np': 'e', 'Nn': 'c'
'name': '1Ω', 'type': 'Resistor', 'value': '1Ω', 'ports': {'N1': 'd', 'N2': 'e'
'name': '2Ω', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'd', 'N2': 'b'
]
extrainfo:The circuit consists of three parts, each with its own power sources and resistors. The mesh-current method is used to solve for currents and power dissipation in specific resistors. The circuit includes independent and dependent sources, and various resistors are connected in series and parallel configurations.


NOTE: Also try Chapter Problems 4.43, 4.47, 4.49, and 4.52.

## 4.8 The Node-Voltage Method Versus the Mesh-Current Method

The greatest advantage of both the node-voltage and mesh-current methods is that they reduce the number of simultaneous equations that must be manipulated. They also require the analyst to be quite systematic in terms of organizing and writing these equations. It is natural to ask, then, "When is the node-voltage method preferred to the mesh-current method and vice versa?" As you might suspect, there is no clear-cut answer. Asking a number of questions, however, may help you identify the more efficient method before plunging into the solution process:

- Does one of the methods result in fewer simultaneous equations to solve?
- Does the circuit contain supernodes? If so, using the node-voltage method will permit you to reduce the number of equations to be solved.
- Does the circuit contain supermeshes? If so, using the mesh-current method will permit you to reduce the number of equations to be solved.
- Will solving some portion of the circuit give the requested solution? If so, which method is most efficient for solving just the pertinent portion of the circuit?
Perhaps the most important observation is that, for any situation, some time spent thinking about the problem in relation to the various analytical approaches available is time well spent. Examples 4.6 and 4.7 illustrate the process of deciding between the node-voltage and mesh-current methods.


#### Example 4.6 Understanding the Node-Voltage Method Versus Mesh-Current Method

Find the power dissipated in the $300 \Omega$ resistor in the circuit shown in Fig. 4.29.
image_name:Figure 4.29
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '150 Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': '200 Ω', 'ports': {'N1': 'b', 'N2': 'f'
'name': 'R3', 'type': 'Resistor', 'value': '100 Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R4', 'type': 'Resistor', 'value': '250 Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'R5', 'type': 'Resistor', 'value': '300 Ω', 'ports': {'N1': 'b', 'N2': 'd'
'name': 'R6', 'type': 'Resistor', 'value': '400 Ω', 'ports': {'N1': 'd', 'N2': 'f'
'name': 'R7', 'type': 'Resistor', 'value': '500 Ω', 'ports': {'N1': 'd', 'N2': 'e'
'name': 'V1', 'type': 'VoltageSource', 'value': '256 V', 'ports': {'Np': 'a', 'Nn': 'f'
'name': 'V2', 'type': 'VoltageSource', 'value': '128 V', 'ports': {'Np': 'f', 'Nn': 'e'
'name': 'ICVS', 'type': 'CurrentControlledVoltageSource', 'value': '50 iΔ', 'ports': {'Np': 'c', 'Nn': 'f'
]
extrainfo:The circuit contains multiple resistors, two independent voltage sources, and one voltage-controlled voltage source. The current iΔ flows from node d to node b through the 300 Ω resistor.


Figure 4.29 $\triangle$ The circuit for Example 4.6.

#### Solution

To find the power dissipated in the $300 \Omega$ resistor, we need to find either the current in the resistor or the voltage across it. The mesh-current method yields the current in the resistor; this approach requires solving five simultaneous mesh equations, as depicted in Fig. 4.30. In writing the five equations, we must include the constraint $i_{\Delta}=-i_{b}$.

Before going further, let's also look at the circuit in terms of the node-voltage method. Note that, once we know the node voltages, we can calculate either the current in the $300 \Omega$ resistor or the voltage across it. The circuit has four essential nodes, and therefore only three node-voltage equations are required to describe the circuit. Because of the dependent voltage source between two essential nodes, we have to sum the currents at only two nodes. Hence the problem is reduced to writing two node-voltage equations and a constraint equation. Because the node-voltage method requires only three simultaneous equations, it is the more attractive approach.

Once the decision to use the node-voltage method has been made, the next step is to select a reference node. Two essential nodes in the circuit in Fig. 4.29 merit consideration. The first is the reference node in Fig. 4.31. If this node is selected, one of the unknown node voltages is the voltage across the
$300 \Omega$ resistor, namely, $v_{2}$ in Fig. 4.31. Once we know this voltage, we calculate the power in the $300 \Omega$ resistor by using the expression

$$
p_{300 \Omega}=v_{2}^{2} / 300
$$

image_name:Figure 4.30
description:
[
'name': '150 Ω', 'type': 'Resistor', 'value': '150 Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '100 Ω', 'type': 'Resistor', 'value': '100 Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': '250 Ω', 'type': 'Resistor', 'value': '250 Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': '300 Ω', 'type': 'Resistor', 'value': '300 Ω', 'ports': {'N1': 'b', 'N2': 'd'
'name': '500 Ω', 'type': 'Resistor', 'value': '500 Ω', 'ports': {'N1': 'd', 'N2': 'e'
'name': '200 Ω', 'type': 'Resistor', 'value': '200 Ω', 'ports': {'N1': 'b', 'N2': 'f'
'name': '400 Ω', 'type': 'Resistor', 'value': '400 Ω', 'ports': {'N1': 'd', 'N2': 'f'
'name': '256 V', 'type': 'VoltageSource', 'value': '256 V', 'ports': {'Np': 'a', 'Nn': 'f'
'name': '128 V', 'type': 'VoltageSource', 'value': '128 V', 'ports': {'Np': 'f', 'Nn': 'e'
'name': '50 i_Δ', 'type': 'CurrentControlledVoltageSource', 'ports': {'Np': 'c', 'Nn': 'f'
]
extrainfo:The circuit is a complex network involving resistors, independent voltage sources, and a voltage-controlled voltage source. Node f is used as the reference ground node. The mesh currents i_a, i_b, i_c, i_d, and i_e are indicated, suggesting a mesh analysis approach. The voltage across the 300 Ω resistor is crucial for calculating power dissipation.


Figure $4.30 \triangle$ The circuit shown in Fig. 4.29, with the five mesh currents.
image_name:Figure 4.31
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '150 Ω', 'ports': {'N1': 'a', 'N2': 'GND'
'name': 'R2', 'type': 'Resistor', 'value': '300 Ω', 'ports': {'N1': 'GND', 'N2': '2'
'name': 'R3', 'type': 'Resistor', 'value': '100 Ω', 'ports': {'N1': 'GND', 'N2': '1'
'name': 'R4', 'type': 'Resistor', 'value': '250 Ω', 'ports': {'N1': '1', 'N2': '2'
'name': 'R5', 'type': 'Resistor', 'value': '200 Ω', 'ports': {'N1': '3', 'N2': 'GND'
'name': 'R6', 'type': 'Resistor', 'value': '400 Ω', 'ports': {'N1': '2', 'N2': '3'
'name': 'R7', 'type': 'Resistor', 'value': '500 Ω', 'ports': {'N1': '2', 'N2': 'b'
'name': 'V1', 'type': 'VoltageSource', 'value': '256 V', 'ports': {'Np': 'a', 'Nn': '3'
'name': 'V2', 'type': 'VoltageSource', 'value': '128 V', 'ports': {'Np': '3', 'Nn': 'b'
'name': 'G1', 'type': 'CurrentControlledVoltageSource', 'value': '50iΔ', 'ports': {'Np': '1', 'Nn': '3'
]
extrainfo:The circuit is analyzed using mesh currents i_a, i_b, i_c, i_d, and i_e. Node 3 is the reference ground. The voltage across the 300 Ω resistor is important for calculating power dissipation. Nodes 1 and 3 form a super-node due to the voltage-controlled voltage source.


Figure $4.31 \Delta$ The circuit shown in Fig. 4.29, with a reference node.

Note that, in addition to selecting the reference node, we defined the three node voltages $v_{1}, v_{2}$, and $v_{3}$ and indicated that nodes 1 and 3 form a super-node, because they are connected by a dependent voltage source. It is understood that a node voltage is a rise from the reference node; therefore, in Fig. 4.31, we have not placed the node voltage polarity references on the circuit diagram.

The second node that merits consideration as the reference node is the lower node in the circuit, as shown in Fig. 4.32. It is attractive because it has the most branches connected to it, and the nodevoltage equations are thus easier to write. However, to find either the current in the $300 \Omega$ resistor or the voltage across it requires an additional calculation once we know the node voltages $v_{\mathrm{a}}$ and $v_{\mathrm{c}}$. For example, the current in the $300 \Omega$ resistor is $\left(v_{\mathrm{c}}-v_{\mathrm{a}}\right) / 300$, whereas the voltage across the resistor is $v_{\mathrm{c}}-v_{\mathrm{a}}$.
image_name:Figure 4.32
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '150Ω', 'ports': {'N1': 'e', 'N2': 'a'
'name': 'R2', 'type': 'Resistor', 'value': '200Ω', 'ports': {'N1': 'a', 'N2': 'GND'
'name': 'R3', 'type': 'Resistor', 'value': '100Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R4', 'type': 'Resistor', 'value': '300Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'R5', 'type': 'Resistor', 'value': '250Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R6', 'type': 'Resistor', 'value': '500Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'R7', 'type': 'Resistor', 'value': '400Ω', 'ports': {'N1': 'c', 'N2': 'GND'
'name': 'V1', 'type': 'VoltageSource', 'value': '256V', 'ports': {'Np': 'e', 'Nn': 'GND'
'name': 'V2', 'type': 'VoltageSource', 'value': '128V', 'ports': {'Np': 'GND', 'Nn': 'd'
'name': 'G1', 'type': 'CurrentControlledVoltageSource', 'value': '50iΔ', 'ports': {'N1': 'b', 'N2': 'GND'
]
extrainfo:The circuit includes two voltage sources (256V and 128V), a current-controlled voltage source (50iΔ), and several resistors. The nodes are labeled as e, a, b, c, and d. The 300Ω resistor carries a current iΔ from node c to node b.


Figure 4.32 $\triangle$ The circuit shown in Fig. 4.29 with an alternative reference node.

We compare these two possible reference nodes by means of the following sets of equations. The first set pertains to the circuit shown in Fig. 4.31, and the second set is based on the circuit shown in Fig. 4.32.

- Set 1 (Fig 4.31)

At the supernode,
$\frac{v_{1}}{100}+\frac{v_{1}-v_{2}}{250}+\frac{v_{3}}{200}+\frac{v_{3}-v_{2}}{400}+\frac{v_{3}-\left(v_{2}+128\right)}{500}$

$$
+\frac{v_{3}+256}{150}=0
$$

At $v_{2}$,

$\frac{v_{2}}{300}+\frac{v_{2}-v_{1}}{250}+\frac{v_{2}-v_{3}}{400}+\frac{v_{2}+128-v_{3}}{500}=0$.
From the supernode, the constraint equation is

$$
v_{3}=v_{1}-50 i_{\Delta}=v_{1}-\frac{v_{2}}{6}
$$

- Set 2 (Fig 4.32)

At $v_{\mathrm{a}}$,

$$
\frac{v_{\mathrm{a}}}{200}+\frac{v_{\mathrm{a}}-256}{150}+\frac{v_{\mathrm{a}}-v_{\mathrm{b}}}{100}+\frac{v_{\mathrm{a}}-v_{\mathrm{c}}}{300}=0
$$

At $v_{c}$,

$$
\frac{v_{\mathrm{c}}}{400}+\frac{v_{\mathrm{c}}+128}{500}+\frac{v_{\mathrm{c}}-v_{\mathrm{b}}}{250}+\frac{v_{\mathrm{c}}-v_{\mathrm{a}}}{300}=0
$$

From the supernode, the constraint equation is

$$
v_{\mathrm{b}}=50 i_{\Delta}=\frac{50\left(v_{\mathrm{c}}-v_{\mathrm{a}}\right)}{300}=\frac{v_{\mathrm{c}}-v_{\mathrm{a}}}{6} .
$$

You should verify that the solution of either set leads to a power calculation of 16.57 W dissipated in the $300 \Omega$ resistor.

#### Example 4.7 Comparing the Node-Voltage and Mesh-Current Methods

Find the voltage $v_{o}$ in the circuit shown in Fig. 4.33.

#### Solution

At first glance, the node-voltage method looks appealing, because we may define the unknown voltage as a node voltage by choosing the lower terminal of the dependent current source as the reference node. The circuit has four essential nodes and two voltage-controlled dependent sources, so the node-voltage method requires manipulation of three node-voltage equations and two constraint equations.

Let's now turn to the mesh-current method for finding $v_{o}$. The circuit contains three meshes, and we can use the leftmost one to calculate $v_{o}$. If we
let $i_{\mathrm{a}}$ denote the leftmost mesh current, then $v_{o}=193-10 i_{\mathrm{a}}$. The presence of the two current sources reduces the problem to manipulating a single supermesh equation and two constraint equations. Hence the mesh-current method is the more attractive technique here.
image_name:Figure 4.33
description:
[
'name': '4Ω', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '2.5Ω', 'type': 'Resistor', 'value': '2.5Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': '2Ω', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': '6Ω', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'e', 'N2': 'f'
'name': '7.5Ω', 'type': 'Resistor', 'value': '7.5Ω', 'ports': {'N1': 'f', 'N2': 'h'
'name': '8Ω', 'type': 'Resistor', 'value': '8Ω', 'ports': {'N1': 'h', 'N2': 'i'
'name': '193V', 'type': 'VoltageSource', 'value': '193V', 'ports': {'Np': 'a', 'Nn': 'e'
'name': '0.5A', 'type': 'CurrentSource', 'value': '0.5A', 'ports': {'Np': 'h', 'Nn': 'c'
'name': '0.4vΔ', 'type': 'VoltageControlledCurrentSource', 'value': '0.4vΔ', 'ports': {'Np': 'f', 'Nn': 'b'
'name': '0.8vθ', 'type': 'VoltageControlledVoltageSource', 'value': '0.8vθ', 'ports': {'Np': 'd', 'Nn': 'i'
]
extrainfo:The circuit contains two voltage-controlled voltage sources and one current source. It uses mesh currents to calculate the output voltage vo.


Figure 4.33 $\boldsymbol{\Delta}$ The circuit for Example 4.7.
image_name:Figure 4.34
description:
[
'name': '193 V', 'type': 'VoltageSource', 'value': '193 V', 'ports': {'Np': 'a', 'Nn': 'e'
'name': '4 Ω', 'type': 'Resistor', 'value': '4 Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '2.5 Ω', 'type': 'Resistor', 'value': '2.5 Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': '6 Ω', 'type': 'Resistor', 'value': '6 Ω', 'ports': {'N1': 'e', 'N2': 'f'
'name': '7.5 Ω', 'type': 'Resistor', 'value': '7.5 Ω', 'ports': {'N1': 'f', 'N2': 'h'
'name': '2 Ω', 'type': 'Resistor', 'value': '2 Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': '8 Ω', 'type': 'Resistor', 'value': '8 Ω', 'ports': {'N1': 'h', 'N2': 'i'
'name': '0.5 A', 'type': 'CurrentSource', 'value': '0.5 A', 'ports': {'Np': 'h', 'Nn': 'c'
'name': '0.4 v_Δ', 'type': 'VoltageControlledCurrentSource', 'value': '0.4 v_Δ', 'ports': {'Np': 'f', 'Nn': 'b'
'name': '0.8 v_θ', 'type': 'VoltageControlledVoltageSource', 'value': '0.8 v_θ', 'ports': {'Np': 'd', 'Nn': 'i'
]
extrainfo:The circuit contains two voltage-controlled voltage sources and one current source. It uses mesh currents to calculate the output voltage vo.


Figure 4.34 $\boldsymbol{\triangle}$ The circuit shown in Fig. 4.33 with the three mesh currents.
image_name:Figure 4.35
description:
[
'name': '193V', 'type': 'VoltageSource', 'value': '193V', 'ports': {'Np': 'a', 'Nn': 'i'
'name': 'Resistor1', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'Resistor2', 'type': 'Resistor', 'value': '2.5Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'Resistor3', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'Resistor4', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'i', 'N2': 'GND'
'name': 'Resistor5', 'type': 'Resistor', 'value': '7.5Ω', 'ports': {'N1': 'GND', 'N2': 'h'
'name': 'Resistor6', 'type': 'Resistor', 'value': '8Ω', 'ports': {'N1': 'h', 'N2': 'e'
'name': 'Current Source', 'type': 'CurrentSource', 'value': '0.5A', 'ports': {'Np': 'h', 'Nn': 'c'
'name': 'G', 'type': 'VoltageControlledCurrentSource', 'value': '0.4vΔ', 'ports': {'Np': 'GND', 'Nn': 'b'
'name': 'VCVS', 'type': 'VoltageControlledVoltageSource', 'value': '0.8vθ', 'ports': {'Np': 'd', 'Nn': 'e'
]
extrainfo:The circuit contains two voltage-controlled sources and one current source. It uses mesh currents to calculate the output voltage vo. The supermesh equation is given as 193=10ia+10ib+10ic+0.8vθ, with constraint equations ib-ia=0.


Figure 4.35 $\boldsymbol{\triangle}$ The circuit shown in Fig. 4.33 with node voltages.

To help you compare the two approaches, we summarize both methods. The mesh-current equations are based on the circuit shown in Fig. 4.34, and the node-voltage equations are based on the circuit shown in Fig. 4.35. The supermesh equation is

$$
193=10 i_{\mathrm{a}}+10 i_{\mathrm{b}}+10 i_{\mathrm{c}}+0.8 v_{\theta}
$$

and the constraint equations are

$$
\begin{aligned}
i_{\mathrm{b}}-i_{\mathrm{a}} & =0.4 v_{\Delta}=0.8 i_{\mathrm{c}} \\
v_{\theta} & =-7.5 i_{\mathrm{b}} ; \text { and } \\
i_{\mathrm{c}}-i_{\mathrm{b}} & =0.5
\end{aligned}
$$

We use the constraint equations to write the supermesh equation in terms of $i_{\mathrm{a}}$ :

$$
\begin{gathered}
160=80 i_{\mathrm{a}}, \quad \text { or } \quad i_{\mathrm{a}}=2 \mathrm{~A} \\
v_{o}=193-20=173 \mathrm{~V}
\end{gathered}
$$

The node-voltage equations are

$$
\begin{aligned}
\frac{v_{o}-193}{10}-0.4 v_{\Delta}+\frac{v_{o}-v_{\mathrm{a}}}{2.5} & =0 \\
\frac{v_{\mathrm{a}}-v_{o}}{2.5}-0.5+\frac{v_{\mathrm{a}}-\left(v_{\mathrm{b}}+0.8 v_{\theta}\right)}{10} & =0 \\
\frac{v_{\mathrm{b}}}{7.5}+0.5+\frac{v_{\mathrm{b}}+0.8 v_{\theta}-v_{\mathrm{a}}}{10} & =0
\end{aligned}
$$

The constraint equations are

$$
v_{\theta}=-v_{\mathrm{b}}, \quad v_{\Delta}=\left[\frac{v_{\mathrm{a}}-\left(v_{\mathrm{b}}+0.8 v_{\theta}\right)}{10}\right] 2
$$

We use the constraint equations to reduce the nodevoltage equations to three simultaneous equations involving $v_{o}, v_{\mathrm{a}}$, and $v_{\mathrm{b}}$. You should verify that the node-voltage approach also gives $v_{o}=173 \mathrm{~V}$.

ASSESSMENT PROBLEMS

Objective 3-Deciding between the node-voltage and mesh-current methods
4.13 Find the power delivered by the 2 A current source in the circuit shown.
image_name:4.13
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '15Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'b', 'N2': 'e'
'name': 'V1', 'type': 'VoltageSource', 'value': '20V', 'ports': {'Np': 'a', 'Nn': 'c'
'name': 'I1', 'type': 'CurrentSource', 'value': '2A', 'ports': {'Np': 'c', 'Nn': 'b'
'name': 'V2', 'type': 'VoltageSource', 'value': '25V', 'ports': {'Np': 'e', 'Nn': 'c'
]
extrainfo:This circuit contains two voltage sources (20V and 25V), two resistors (15Ω and 10Ω), and a 2A current source. The nodes are labeled as a, b, c, and e.


Answer: 70 W .
NOTE: Also try Chapter Problems 4.54 and 4.56.
4.14 Find the power delivered by the 4 A current source in the circuit shown.
image_name:Figure
description:
[
'name': '128V', 'type': 'VoltageSource', 'value': '128V', 'ports': {'Np': 'a', 'Nn': 'e'
'name': '4A', 'type': 'CurrentSource', 'value': '4A', 'ports': {'Np': 'a', 'Nn': 'b'
'name': '4Ω', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '3Ω', 'type': 'Resistor', 'value': '3Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': '6Ω', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'b', 'N2': 'd'
'name': '2Ω', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'e', 'N2': 'd'
'name': '5Ω', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'd', 'N2': 'h'
'name': '30i_x', 'type': 'CurrentControlledVoltageSource', 'value': '30i_x', 'ports': {'Np': 'c', 'Nn': 'h'
]
extrainfo:The circuit contains a 128V voltage source, a 4A current source, and a voltage-controlled voltage source with a gain of 30 times the current ix. The resistors are 4Ω, 3Ω, 6Ω, 2Ω, and 5Ω. The nodes are labeled as a, b, c, d, e, and h. The current ix flows through the 4Ω resistor between nodes a and b.


Answer: 40 W .

## 4.9 Source Transformations

Even though the node-voltage and mesh-current methods are powerful techniques for solving circuits, we are still interested in methods that can be used to simplify circuits. Series-parallel reductions and $\Delta$-to-Y transformations are
image_name:(a)
description:
[
'name': 'vs', 'type': 'VoltageSource', 'value': 'vs', 'ports': {'Np': '1', 'Nn': 'b'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'a', 'N2': '1'
]
extrainfo:The circuit diagram (a) shows a voltage source vs in series with a resistor R between nodes a and b. This can be transformed into a current source is in parallel with the same resistor R, as shown in diagram (b).
image_name:(b)
description:
[
'name': 'is', 'type': 'CurrentSource', 'value': 'is', 'ports': {'Np': 'a', 'Nn': 'b'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit diagram (b) shows a current source is in parallel with a resistor R between nodes a and b. This is a source transformation from a voltage source in series with a resistor.


Figure 4.36 $\boldsymbol{\Delta}$ Source transformations.
already on our list of simplifying techniques. We begin expanding this list with source transformations. A source transformation, shown in Fig. 4.36, allows a voltage source in series with a resistor to be replaced by a current source in parallel with the same resistor or vice versa. The double-headed arrow emphasizes that a source transformation is bilateral; that is, we can start with either configuration and derive the other.

We need to find the relationship between $v_{s}$ and $i_{s}$ that guarantees the two configurations in Fig. 4.36 are equivalent with respect to nodes a,b. Equivalence is achieved if any resistor $R_{L}$ experiences the same current flow, and thus the same voltage drop, whether connected between nodes a,b in Fig. 4.36(a) or Fig. 4.36(b).

Suppose $R_{L}$ is connected between nodes a,b in Fig. 4.36(a). Using Ohm's law, the current in $R_{L}$ is

$$
\begin{equation*}
i_{L}=\frac{v_{s}}{R+R_{L}} \tag{4.52}
\end{equation*}
$$

Now suppose the same resistor $R_{L}$ is connected between nodes a,b in Fig. 4.36(b). Using current division, the current in $R_{L}$ is

$$
\begin{equation*}
i_{L}=\frac{R}{R+R_{L}} i_{s} \tag{4.53}
\end{equation*}
$$

If the two circuits in Fig. 4.36 are equivalent, these resistor currents must be the same. Equating the right-hand sides of Eqs. 4.52 and 4.53 and simplifying,

$$
\begin{equation*}
i_{s}=\frac{v_{s}}{R} \tag{4.54}
\end{equation*}
$$

When Eq. 4.54 is satisfied for the circuits in Fig. 4.36, the current in $R_{L}$ is the same for both circuits in the figure for all values of $R_{L}$. If the current through $R_{L}$ is the same in both circuits, then the voltage drop across $R_{L}$ is the same in both circuits, and the circuits are equivalent at nodes a,b.

If the polarity of $v_{s}$ is reversed, the orientation of $i_{s}$ must be reversed to maintain equivalence.

Example 4.8 illustrates the usefulness of making source transformations to simplify a circuit-analysis problem.

#### Example 4.8 Using Source Transformations to Solve a Circuit

a) For the circuit shown in Fig. 4.37, find the power associated with the 6 V source.
b) State whether the 6 V source is absorbing or delivering the power calculated in (a).

#### Solution

a) If we study the circuit shown in Fig. 4.37, knowing that the power associated with the 6 V source is of interest, several approaches come to mind. The circuit has four essential nodes and six essential branches where the current is unknown. Thus we can find the current in the branch containing the 6 V source by solving either three $[6-(4-1)]$ mesh-current equations or three $[4-1]$ node-voltage equations. Choosing the mesh-current approach involves
image_name:Figure 4.37
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R3', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'R4', 'type': 'Resistor', 'value': '30Ω', 'ports': {'N1': 'b', 'N2': 'e'
'name': 'R5', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'e', 'N2': 'h'
'name': 'R6', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'c', 'N2': 'h'
'name': 'V1', 'type': 'VoltageSource', 'value': '6V', 'ports': {'Np': 'a', 'Nn': 'e'
'name': 'V2', 'type': 'VoltageSource', 'value': '40V', 'ports': {'Np': 'd', 'Nn': 'h'
]
extrainfo:The circuit consists of a combination of resistors and voltage sources. It has four essential nodes and six branches. The power associated with the 6V source is of interest. The circuit can be solved using mesh-current or node-voltage methods. Source transformations can simplify the analysis.


Figure 4.37 $\triangle$ The circuit for Example 4.8.
solving for the mesh current that corresponds to the branch current in the 6 V source. Choosing the node-voltage approach involves solving for the voltage across the $30 \Omega$ resistor, from which the branch current in the 6 V source can be calculated. But by focusing on just one branch current, we can first simplify the circuit by using source transformations.

We must reduce the circuit in a way that preserves the identity of the branch containing the 6 V source. We have no reason to preserve the identity of the branch containing the 40 V source. Beginning with
image_name:(a) First step
description:
[
'name': '6V', 'type': 'VoltageSource', 'value': '6V', 'ports': {'Np': 'a', 'Nn': 'd'
'name': '4Ω', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '30Ω', 'type': 'Resistor', 'value': '30Ω', 'ports': {'N1': 'b', 'N2': 'e'
'name': '6Ω', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': '10Ω', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'e', 'N2': 'f'
'name': '20Ω', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'c', 'N2': 'f'
'name': '5Ω', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'g', 'N2': 'h'
'name': '8A', 'type': 'CurrentSource', 'value': '8A', 'ports': {'Np': 'h', 'Nn': 'g'
]
extrainfo:The circuit consists of a combination of series and parallel resistors with a voltage source and a current source. The 6V voltage source is connected between nodes a and d, and the 8A current source is connected between nodes g and h. The resistors form a network allowing for analysis of current and voltage distribution across the circuit.
image_name:(b) Second step
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R3', 'type': 'Resistor', 'value': '30Ω', 'ports': {'N1': 'b', 'N2': 'e'
'name': 'R4', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'e', 'N2': 'f'
'name': 'R5', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'c', 'N2': 'g'
'name': 'V1', 'type': 'VoltageSource', 'value': '6V', 'ports': {'Np': 'a', 'Nn': 'e'
'name': '32V', 'type': 'VoltageSource', 'value': '32V', 'ports': {'Np': 'g', 'Nn': 'f'
'name': 'R1', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R3', 'type': 'Resistor', 'value': '30Ω', 'ports': {'N1': 'b', 'N2': 'e'
'name': 'R5', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'c', 'N2': 'f'
'name': 'V1', 'type': 'VoltageSource', 'value': '6V', 'ports': {'Np': 'a', 'Nn': 'e'
'name': 'I1', 'type': 'CurrentSource', 'value': '1.6A', 'ports': {'Np': 'f', 'Nn': 'c'
'name': 'R1', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': '12Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'V1', 'type': 'VoltageSource', 'value': '6V', 'ports': {'Np': 'a', 'Nn': 'd'
'name': 'V2', 'type': 'VoltageSource', 'value': '19.2V', 'ports': {'Np': 'c', 'Nn': 'd'
]
extrainfo:The circuit consists of two voltage sources and two resistors. The 6V source is connected between nodes a and d, and the 19.2V source is connected between nodes c and d. Resistors are connected between nodes a-b and b-c with resistances of 4Ω and 12Ω, respectively.

Figure 4.38 $\boldsymbol{\triangle}$ Step-by-step simplification of the circuit shown in Fig. 4.37.

Next, we can replace the parallel combination of the $20 \Omega$ and $5 \Omega$ resistors with a $4 \Omega$ resistor. This $4 \Omega$ resistor is in parallel with the 8 A source and therefore can be replaced with a 32 V source in series with a $4 \Omega$ resistor, as shown in Fig. 4.38(b). The 32 V source is in series with $20 \Omega$ of resistance and, hence, can be replaced by a current source of 1.6 A in parallel with $20 \Omega$, as shown in Fig. 4.38(c). The $20 \Omega$ and $30 \Omega$ parallel resistors can be reduced to a single $12 \Omega$ resistor. The parallel combination of the 1.6 A current source
and the $12 \Omega$ resistor transforms into a voltage source of 19.2 V in series with $12 \Omega$. Figure 4.38(d) shows the result of this last transformation. The current in the direction of the voltage drop across the 6 V source is $(19.2-6) / 16$, or 0.825 A . Therefore the power associated with the 6 V source is

$$
p_{6 \mathrm{~V}}=(0.825)(6)=4.95 \mathrm{~W}
$$

b) The voltage source is absorbing power.

A question that arises from use of the source transformation depicted in Fig. 4.38 is, "What happens if there is a resistance $R_{p}$ in parallel with the voltage source or a resistance $R_{s}$ in series with the current source?" In both cases, the resistance has no effect on the equivalent circuit that predicts behavior with respect to terminals a,b. Figure 4.39 summarizes this observation.

The two circuits depicted in Fig. 4.39(a) are equivalent with respect to terminals a,b because they produce the same voltage and current in any resistor $R_{L}$ inserted between nodes $\mathrm{a}, \mathrm{b}$. The same can be said for the circuits in Fig. 4.39(b). Example 4.9 illustrates an application of the equivalent circuits depicted in Fig. 4.39.
image_name:(a)
description:
[
'name': 'vs', 'type': 'VoltageSource', 'value': 'vs', 'ports': {'Np': 'c', 'Nn': 'b'
'name': 'Rp', 'type': 'Resistor', 'value': 'Rp', 'ports': {'N1': 'c', 'N2': 'b'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'c', 'N2': 'a'
]
extrainfo:The circuit (a) shows a voltage source 'vs' in parallel with a resistor 'Rp', both connected between nodes 'c' and 'b'. There is another resistor 'R' connected between nodes 'c' and 'a'. The equivalent circuit on the right simplifies this to a voltage source 'vs' connected between 'c' and 'b', with a resistor 'R' between 'c' and 'a'.
image_name:(b)
description:
[
'name': 'Is', 'type': 'CurrentSource', 'value': 'Is', 'ports': {'Np': 'b', 'Nn': 'c'
'name': 'Rs', 'type': 'Resistor', 'value': 'Rs', 'ports': {'N1': 'c', 'N2': 'a'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit demonstrates a source transformation where a current source in parallel with a resistor is converted to a current source in series with a resistor. This transformation maintains the same behavior with respect to terminals a and b.


Figure 4.39 $\triangle$ Equivalent circuits containing a resistance in parallel with a voltage source or in series with a current source.

#### Example 4.9 Using Special Source Transformation Techniques

a) Use source transformations to find the voltage $v_{o}$ in the circuit shown in Fig. 4.40.
b) Find the power developed by the 250 V voltage source.
c) Find the power developed by the 8 A current source.
image_name:Figure 4.40
description:
[
'name': '250 V', 'type': 'VoltageSource', 'value': '250 V', 'ports': {'Np': 'a', 'Nn': 'b'
'name': '25 Ω', 'type': 'Resistor', 'value': '25 Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': '125 Ω', 'type': 'Resistor', 'value': '125 Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '8 A', 'type': 'CurrentSource', 'value': '8 A', 'ports': {'Np': 'c', 'Nn': 'd'
'name': '10 Ω', 'type': 'Resistor', 'value': '10 Ω', 'ports': {'N1': 'd', 'N2': 'b'
'name': '5 Ω', 'type': 'Resistor', 'value': '5 Ω', 'ports': {'N1': 'c', 'N2': 'e'
'name': '100 Ω', 'type': 'Resistor', 'value': '100 Ω', 'ports': {'N1': 'c', 'N2': 'b'
'name': '15 Ω', 'type': 'Resistor', 'value': '15 Ω', 'ports': {'N1': 'e', 'N2': 'b'
]
extrainfo:The circuit involves source transformations and simplifications to find the voltage vo across the 8 A current source. It includes two parallel resistors connected to the voltage source and a series of resistors connected to the current source.


#### Solution

a) We begin by removing the $125 \Omega$ and $10 \Omega$ resistors, because the $125 \Omega$ resistor is connected across the 250 V voltage source and the $10 \Omega$ resistor is connected in series with the 8 A current source. We also combine the series-connected resistors into a single resistance of $20 \Omega$. Figure 4.41 shows the simplified circuit.
image_name:Figure 4.41
description:
[
'name': '250V', 'type': 'VoltageSource', 'value': '250V', 'ports': {'Np': 'a', 'Nn': 'c'
'name': '8A', 'type': 'CurrentSource', 'value': '8A', 'ports': {'Np': 'b', 'Nn': 'c'
'name': '25Ω', 'type': 'Resistor', 'value': '25Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '100Ω', 'type': 'Resistor', 'value': '100Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': '20Ω', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'b', 'N2': 'c'
]
extrainfo:The circuit consists of a 250V voltage source in series with a 25Ω resistor, connected to a parallel combination of an 8A current source, a 100Ω resistor, and a 20Ω resistor. All components share a common ground node 'c'.


Figure 4.41 $\triangle$ A simplified version of the circuit shown in Fig. 4.40.

We now use a source transformation to replace the 250 V source and $25 \Omega$ resistor with a 10 A source in parallel with the $25 \Omega$ resistor, as shown in Fig. 4.42. We can now simplify the circuit shown in Fig. 4.42 by using Kirchhoff's current law to combine the parallel current sources into a single source. The parallel resistors combine into a single resistor. Figure 4.43 shows the result. Hence $v_{o}=20 \mathrm{~V}$.
b) The current supplied by the 250 V source equals the current in the $125 \Omega$ resistor plus the current in the $25 \Omega$ resistor. Thus

$$
i_{s}=\frac{250}{125}+\frac{250-20}{25}=11.2 \mathrm{~A}
$$

Therefore the power developed by the voltage source is

$$
p_{250 \mathrm{v}}(\text { developed })=(250)(11.2)=2800 \mathrm{~W}
$$

c) To find the power developed by the 8 A current source, we first find the voltage across the source. If we let $v_{s}$ represent the voltage across the source, positive at the upper terminal of the source, we obtain

$$
v_{s}+8(10)=v_{o}=20, \quad \text { or } \quad v_{s}=-60 \mathrm{~V}
$$

and the power developed by the 8 A source is 480 W . Note that the $125 \Omega$ and $10 \Omega$ resistors do not affect the value of $v_{o}$ but do affect the power calculations.
image_name:Figure 4.42
description:
[
'name': 'I1', 'type': 'CurrentSource', 'value': '10A', 'ports': {'Np': 'b', 'Nn': 'a'
'name': 'R1', 'type': 'Resistor', 'value': '25Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'I2', 'type': 'CurrentSource', 'value': '8A', 'ports': {'Np': 'a', 'Nn': 'b'
'name': 'R2', 'type': 'Resistor', 'value': '100Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R3', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit consists of two parallel current sources (10A and 8A) and three resistors (25Ω, 100Ω, and 20Ω) all connected across nodes a and b.


Figure $4.42 \triangle$ The circuit shown in Fig. 4.41 after a source transformation.
image_name:Figure 4.43
description:
[
'name': '2A', 'type': 'CurrentSource', 'value': '2A', 'ports': {'Np': 'b', 'Nn': 'a'
'name': 'Resistor', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit consists of a 2A current source and a 10Ω resistor connected in parallel across nodes a and b. The voltage across the resistor is labeled as v_o.


Figure 4.43 $\Delta$ The circuit shown in Fig. 4.42 after combining sources and resistors.

ASSESSMENT PROBLEM

Objective 4-Understand source transformation

4.15 a) Use a series of source transformations to find the voltage $v$ in the circuit shown.
b) How much power does the 120 V source deliver to the circuit?
Answer: (a) 48 V;
(b) 374.4 W .
image_name:Figure
description:
[
'name': '120V', 'type': 'VoltageSource', 'value': '120V', 'ports': {'Np': 'd', 'Nn': 'c'
'name': '20Ω', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'a', 'N2': 'd'
'name': '60V', 'type': 'VoltageSource', 'value': '60V', 'ports': {'Np': 'e', 'Nn': 'a'
'name': '5Ω', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'e', 'N2': 'c'
'name': '36A', 'type': 'CurrentSource', 'value': '36A', 'ports': {'Np': 'c', 'Nn': 'a'
'name': '1.6Ω', 'type': 'Resistor', 'value': '1.6Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '6Ω', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': '8Ω', 'type': 'Resistor', 'value': '8Ω', 'ports': {'N1': 'b', 'N2': 'c'
]
extrainfo:The circuit consists of multiple sources and resistors connected between nodes a, b, and c. The voltage across the 8Ω resistor is labeled as v.


NOTE: Also try Chapter Problems 4.61 and 4.62.

## 4.10 Thévenin and Norton Equivalents

At times in circuit analysis, we want to concentrate on what happens at a specific pair of terminals. For example, when we plug a toaster into an outlet, we are interested primarily in the voltage and current at the terminals of the toaster. We have little or no interest in the effect that connecting the toaster has on voltages or currents elsewhere in the circuit supplying the outlet. We can expand this interest in terminal behavior to a set of appliances, each requiring a different amount of power. We then are interested in how the voltage and current delivered at the outlet change as we change appliances. In other words, we want to focus on the behavior of the circuit supplying the outlet, but only at the outlet terminals.

Thévenin and Norton equivalents are circuit simplification techniques that focus on terminal behavior and thus are extremely valuable aids in analysis. Although here we discuss them as they pertain to resistive circuits, Thévenin and Norton equivalent circuits may be used to represent any circuit made up of linear elements.

We can best describe a Thévenin equivalent circuit by reference to Fig. 4.44, which represents any circuit made up of sources (both independent and dependent) and resistors. The letters a and b denote the pair of terminals of interest. Figure 4.44(b) shows the Thévenin equivalent. Thus, a Thévenin equivalent circuit is an independent voltage source $V_{\mathrm{Th}}$ in series with a resistor $R_{\mathrm{Th}}$, which replaces an interconnection of sources and resistors. This series combination of $V_{\mathrm{Th}}$ and $R_{\mathrm{Th}}$ is equivalent to the original circuit in the sense that, if we connect the same load across the terminals a,b of each circuit, we get the same voltage and current at the terminals of the load. This equivalence holds for all possible values of load resistance.

To represent the original circuit by its Thévenin equivalent, we must be able to determine the Thévenin voltage $V_{\mathrm{Th}}$ and the Thévenin resistance $R_{\mathrm{Th}}$. First, we note that if the load resistance is infinitely large, we have an open-circuit condition. The open-circuit voltage at the terminals a,b in the circuit shown in Fig. 4.44(b) is $V_{\mathrm{Th}}$. By hypothesis, this must be
image_name:Figure 4.44 (a)
descriptionThe diagram shows a Thévenin equivalent circuit with a voltage source V_Th and a resistor R_Th connected between nodes a and b.
image_name:Figure 4.44 (b)
description:
[
'name': 'R_Th', 'type': 'Resistor', 'value': 'R_Th', 'ports': {'N1': 'a', 'N2': '1'
'name': 'V_Th', 'type': 'VoltageSource', 'value': 'V_Th', 'ports': {'Np': '1', 'Nn': 'b'
]
extrainfo:The circuit represents the Thévenin equivalent with a voltage source V_Th and a resistor R_Th connected between terminals a and b.


Figure 4.44 (a) A general circuit. (b) The Thévenin equivalent circuit.
image_name:Figure 4.45
description:
[
'name': '25V', 'type': 'VoltageSource', 'value': '25V', 'ports': {'Np': 'd', 'Nn': 'b'
'name': '5Ω', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'd', 'N2': 'c'
'name': '20Ω', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'c', 'N2': 'b'
'name': '3A', 'type': 'CurrentSource', 'value': '3A', 'ports': {'Np': 'b', 'Nn': 'c'
'name': '4Ω', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'c', 'N2': 'a'
]
extrainfo:The circuit in Figure 4.45 consists of a 25V voltage source, a 5Ω resistor, a 20Ω resistor, a 3A current source, and a 4Ω resistor. Nodes are labeled as a, b, c, and d. The circuit includes a voltage v1 across the 4Ω resistor and an output voltage vab between nodes a and b.


Figure 4.45 $\boldsymbol{\Delta}$ A circuit used to illustrate a Thévenin equivalent.
image_name:Figure 4.46
description:
[
'name': '25V', 'type': 'VoltageSource', 'value': '25V', 'ports': {'Np': 'c', 'Nn': 'b'
'name': '5Ω', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': '20Ω', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'd', 'N2': 'b'
'name': '3A', 'type': 'CurrentSource', 'value': '3A', 'ports': {'Np': 'b', 'Nn': 'd'
'name': '4Ω', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'd', 'N2': 'a'
]
extrainfo:The circuit in Figure 4.46 is used to illustrate a Thévenin equivalent. It consists of a 25V voltage source, a 5Ω resistor, a 20Ω resistor, a 3A current source, and a 4Ω resistor. Nodes are labeled as a, b, c, and d. The circuit includes a voltage v2 across the 4Ω resistor and a short-circuit current isc flowing from node a to node b.


Figure $4.46 \boldsymbol{\Delta}$ The circuit shown in Fig. 4.45 with terminals a and b short-circuited.
the same as the open-circuit voltage at the terminals $\mathrm{a}, \mathrm{b}$ in the original circuit. Therefore, to calculate the Thévenin voltage $V_{\mathrm{Th}}$, we simply calculate the open-circuit voltage in the original circuit.

Reducing the load resistance to zero gives us a short-circuit condition. If we place a short circuit across the terminals $a, b$ of the Thévenin equivalent circuit, the short-circuit current directed from $a$ to $b$ is

$$
\begin{equation*}
i_{\mathrm{sc}}=\frac{V_{\mathrm{Th}}}{R_{\mathrm{Th}}} \tag{4.55}
\end{equation*}
$$

By hypothesis, this short-circuit current must be identical to the short-circuit current that exists in a short circuit placed across the terminals a,b of the original network. From Eq. 4.55,

$$
\begin{equation*}
R_{\mathrm{Th}}=\frac{V_{\mathrm{Th}}}{i_{\mathrm{sc}}} \tag{4.56}
\end{equation*}
$$

Thus the Thévenin resistance is the ratio of the open-circuit voltage to the short-circuit current.

Finding a Thévenin Equivalent

To find the Thévenin equivalent of the circuit shown in Fig. 4.45, we first calculate the open-circuit voltage of $v_{\mathrm{ab}}$. Note that when the terminals $\mathrm{a}, \mathrm{b}$ are open, there is no current in the $4 \Omega$ resistor. Therefore the open-circuit voltage $v_{\mathrm{ab}}$ is identical to the voltage across the 3 A current source, labeled $v_{1}$. We find the voltage by solving a single node-voltage equation. Choosing the lower node as the reference node, we get

$$
\begin{equation*}
\frac{v_{1}-25}{5}+\frac{v_{1}}{20}-3=0 \tag{4.57}
\end{equation*}
$$

Solving for $v_{1}$ yields

$$
\begin{equation*}
v_{1}=32 \mathrm{~V} \tag{4.58}
\end{equation*}
$$

Hence the Thévenin voltage for the circuit is 32 V .
The next step is to place a short circuit across the terminals and calculate the resulting short-circuit current. Figure 4.46 shows the circuit with the short in place. Note that the short-circuit current is in the direction of the open-circuit voltage drop across the terminals $\mathrm{a}, \mathrm{b}$. If the short-circuit current is in the direction of the open-circuit voltage rise across the terminals, a minus sign must be inserted in Eq. 4.56.

The short-circuit current $\left(i_{\mathrm{sc}}\right)$ is found easily once $v_{2}$ is known. Therefore the problem reduces to finding $v_{2}$ with the short in place. Again, if we use the lower node as the reference node, the equation for $v_{2}$ becomes

$$
\begin{equation*}
\frac{v_{2}-25}{5}+\frac{v_{2}}{20}-3+\frac{v_{2}}{4}=0 \tag{4.59}
\end{equation*}
$$

Solving Eq. 4.59 for $v_{2}$ gives

$$
\begin{equation*}
v_{2}=16 \mathrm{~V} \tag{4.60}
\end{equation*}
$$

Hence, the short-circuit current is

$$
\begin{equation*}
i_{\mathrm{sc}}=\frac{16}{4}=4 \mathrm{~A} \tag{4.61}
\end{equation*}
$$

We now find the Thévenin resistance by substituting the numerical results from Eqs. 4.58 and 4.61 into Eq. 4.56:

$$
\begin{equation*}
R_{\mathrm{Th}}=\frac{V_{\mathrm{Th}}}{i_{\mathrm{sc}}}=\frac{32}{4}=8 \Omega \tag{4.62}
\end{equation*}
$$

Figure 4.47 shows the Thévenin equivalent for the circuit shown in Fig. 4.45.
You should verify that, if a $24 \Omega$ resistor is connected across the terminals a,b in Fig. 4.45, the voltage across the resistor will be 24 V and the current in the resistor will be 1 A , as would be the case with the Thévenin circuit in Fig. 4.47. This same equivalence between the circuit in Figs. 4.45 and 4.47 holds for any resistor value connected between nodes a,b.

The Norton Equivalent

A Norton equivalent circuit consists of an independent current source in parallel with the Norton equivalent resistance. We can derive it from a Thévenin equivalent circuit simply by making a source transformation. Thus the Norton current equals the short-circuit current at the terminals of interest, and the Norton resistance is identical to the Thévenin resistance.

Using Source Transformations

Sometimes we can make effective use of source transformations to derive a Thévenin or Norton equivalent circuit. For example, we can derive the Thévenin and Norton equivalents of the circuit shown in Fig. 4.45 by making the series of source transformations shown in Fig. 4.48. This technique is most useful when the network contains only independent sources. The presence of dependent sources requires retaining the identity of the controlling voltages and/or currents, and this constraint usually prohibits continued reduction of the circuit by source transformations. We discuss the problem of finding the Thévenin equivalent when a circuit contains dependent sources in Example 4.10.
image_name:Figure 4.47
description:
[
'name': '32V', 'type': 'VoltageSource', 'value': '32V', 'ports': {'Np': 'C', 'Nn': 'b'
'name': '8Ω', 'type': 'Resistor', 'value': '8Ω', 'ports': {'N1': 'C', 'N2': 'a'
]
extrainfo:The circuit consists of a 32V voltage source and an 8Ω resistor. Node 'C' is the positive terminal of the voltage source and one terminal of the resistor. Node 'b' is the negative terminal of the voltage source. Node 'a' is connected to the other terminal of the resistor.


Figure 4.47 $\boldsymbol{\triangle}$ The Thévenin equivalent of the circuit shown in Fig. 4.45.
image_name:Step 1
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'd', 'N2': 'c'
'name': 'R2', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'c', 'N2': 'b'
'name': 'R3', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'c', 'N2': 'a'
'name': 'V1', 'type': 'VoltageSource', 'value': '25V', 'ports': {'Np': 'd', 'Nn': 'b'
'name': 'I1', 'type': 'CurrentSource', 'value': '3A', 'ports': {'Np': 'b', 'Nn': 'c'
]
extrainfo:The circuit undergoes transformations to simplify it into its Thévenin and Norton equivalents. Initially, it consists of a 25V voltage source, a 5Ω resistor, a 20Ω resistor, a 4Ω resistor, and two current sources of 3A and 5A. Through transformations, the circuit is simplified to a Thévenin equivalent with a 32V voltage source and an 8Ω resistor, and a Norton equivalent with a 4A current source and an 8Ω resistor.
image_name:Step 2
description:
[
'name': 'I2', 'type': 'CurrentSource', 'value': '8A', 'ports': {'Np': 'b', 'Nn': 'c'
'name': 'R3', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'c', 'N2': 'a'
'name': 'R2', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'c', 'N2': 'b'
]
extrainfo:The circuit in 'Step 2' shows a parallel combination of an 8A current source and a 4Ω resistor between nodes C and b, and a 4Ω resistor between nodes C and a. This configuration is part of a step-by-step transformation to find the Thévenin and Norton equivalents.
image_name:Step 3
description:
[
'name': 'V1', 'type': 'VoltageSource', 'value': '32V', 'ports': {'Np': 'C', 'Nn': 'b'
'name': 'R1', 'type': 'Resistor', 'value': '8Ω', 'ports': {'N1': 'C', 'N2': 'a'
]
extrainfo:The circuit is the Thévenin equivalent of a more complex circuit. It consists of a 32V voltage source and an 8Ω resistor. Node 'C' is the positive terminal of the voltage source and one terminal of the resistor. Node 'b' is the negative terminal of the voltage source. Node 'a' is connected to the other terminal of the resistor.
image_name:Step 4
description:
[
'name': '4A', 'type': 'CurrentSource', 'value': '4A', 'ports': {'Np': 'b', 'Nn': 'a'
'name': '8Ω', 'type': 'Resistor', 'value': '8Ω', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit is the Norton equivalent, consisting of a 4A current source and an 8Ω resistor in parallel between nodes 'a' and 'b'.


Figure $4.48 \triangle$ Step-by-step derivation of the Thévenin and Norton equivalents of the circuit shown in Fig. 4.45.

#### Example 4.10 Finding the Thévenin Equivalent of a Circuit with a Dependent Source

Find the Thévenin equivalent for the circuit containing dependent sources shown in Fig. 4.49.
image_name:Figure 4.49
description:
[
'name': '5V', 'type': 'VoltageSource', 'value': '5V', 'ports': {'Np': 'd', 'Nn': 'b'
'name': '2kΩ', 'type': 'Resistor', 'value': '2kΩ', 'ports': {'N1': 'd', 'N2': 'c'
'name': '3v', 'type': 'VoltageControlledVoltageSource', 'value': '3v', 'ports': {'Np': 'c', 'Nn': 'b'
'name': '20i', 'type': 'CurrentControlledCurrentSource', 'value': '20i', 'ports': {'Np': 'a', 'Nn': 'b'
'name': '25Ω', 'type': 'Resistor', 'value': '25Ω', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit in Figure 4.49 is used to illustrate the Thévenin equivalent when the circuit contains dependent sources. The open-circuit voltage Vab is across the 25Ω resistor.


Figure 4.49 $\triangle$ A circuit used to illustrate a Thévenin equivalent when the circuit contains dependent sources.

#### Solution

The first step in analyzing the circuit in Fig. 4.49 is to recognize that the current labeled $i_{x}$ must be zero. (Note the absence of a return path for $i_{x}$ to enter the left-hand portion of the circuit.) The open-circuit, or Thévenin, voltage will be the voltage across the $25 \Omega$ resistor. With $i_{x}=0$,

$$
V_{\mathrm{Th}}=v_{\mathrm{ab}}=(-20 i)(25)=-500 i
$$

The current $i$ is

$$
i=\frac{5-3 v}{2000}=\frac{5-3 V_{\mathrm{Th}}}{2000}
$$

In writing the equation for $i$, we recognize that the Thévenin voltage is identical to the control voltage. When we combine these two equations, we obtain

$$
V_{\mathrm{Th}}=-5 \mathrm{~V}
$$

To calculate the short-circuit current, we place a short circuit across a, b. When the terminals a,b are shorted together, the control voltage $v$ is reduced to zero. Therefore, with the short in place, the circuit shown in Fig. 4.49 becomes the one shown in Fig. 4.50. With the short circuit shunting the $25 \Omega$ resistor, all the current from the dependent current source appears in the short, so

$$
i_{\mathrm{sc}}=-20 i
$$

image_name:Figure 4.50
description:
[
'name': '5V', 'type': 'VoltageSource', 'value': '5V', 'ports': {'Np': 'c', 'Nn': 'b'
'name': 'Resistor1', 'type': 'Resistor', 'value': '2kΩ', 'ports': {'N1': 'c', 'N2': 'b'
'name': 'ICIS', 'type': 'CurrentControlledCurrentSource', 'value': '20i', 'ports': {'Np': 'a', 'Nn': 'b'
'name': 'Resistor2', 'type': 'Resistor', 'value': '25Ω', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit includes a voltage source providing 5V, a 2kΩ resistor, a voltage-controlled current source with a gain of 20i, and a 25Ω resistor. Terminals a and b are short-circuited, resulting in a short-circuit current isc.


Figure $4.50 \boldsymbol{\Delta}$ The circuit shown in Fig. 4.49 with terminals a and b short-circuited.

As the voltage controlling the dependent voltage source has been reduced to zero, the current controlling the dependent current source is

$$
i=\frac{5}{2000}=2.5 \mathrm{~mA}
$$

Combining these two equations yields a short-circuit current of

$$
i_{\mathrm{sc}}=-20(2.5)=-50 \mathrm{~mA}
$$

From $i_{\mathrm{sc}}$ and $V_{\mathrm{Th}}$ we get

$$
R_{\mathrm{Th}}=\frac{V_{\mathrm{Th}}}{i_{\mathrm{sc}}}=\frac{-5}{-50} \times 10^{3}=100 \Omega
$$

Figure 4.51 illustrates the Thévenin equivalent for the circuit shown in Fig. 4.49. Note that the reference polarity marks on the Thévenin voltage source in Fig. 4.51 agree with the preceding equation for $V_{\mathrm{Th}}$.
image_name:Figure 4.51
description:
[
'name': '5V', 'type': 'VoltageSource', 'value': '5V', 'ports': {'Np': 'b', 'Nn': 'c'
'name': '100 Ω', 'type': 'Resistor', 'value': '100 Ω', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit is a simple series circuit with a 5V voltage source and a 100 Ω resistor connected between terminals a and b.


Figure 4.51 $\triangle$ The Thévenin equivalent for the circuit shown in Fig. 4.49.

ASSESSMENT PROBLEMS

Objective 5-Understand Thévenin and Norton equivalents

4.16 Find the Thévenin equivalent circuit with respect to the terminals $\mathrm{a}, \mathrm{b}$ for the circuit shown.

Answer: $\quad V_{\mathrm{ab}}=V_{\mathrm{Th}}=64.8 \mathrm{~V}, R_{\mathrm{Th}}=6 \Omega$.
image_name:Figure
description:
[
'name': 'V1', 'type': 'VoltageSource', 'value': '72V', 'ports': {'Np': 'c', 'Nn': 'b'
'name': 'R1', 'type': 'Resistor', 'value': '12Ω', 'ports': {'N1': 'c', 'N2': 'a'
'name': 'R2', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'R3', 'type': 'Resistor', 'value': '8Ω', 'ports': {'N1': 'd', 'N2': 'a'
'name': 'R4', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'd', 'N2': 'b'
]
extrainfo:The circuit is a combination of series and parallel resistors with a 72V voltage source. The resistors are connected in a bridge-like configuration between nodes a, b, and c.

4.17 Find the Norton equivalent circuit with respect to the terminals $\mathrm{a}, \mathrm{b}$ for the circuit shown.

Answer: $\quad I_{N}=6 \mathrm{~A}($ directed toward a $), R_{N}=7.5 \Omega$.
4.18 A voltmeter with an internal resistance of $100 \mathrm{k} \Omega$ is used to measure the voltage $v_{\mathrm{AB}}$ in the circuit shown. What is the voltmeter reading?

Answer: 120 V .
NOTE: Also try Chapter Problems 4.64, 4.68, and 4.72.

## 4.11 More on Deriving a Thévenin Equivalent

The technique for determining $R_{\mathrm{Th}}$ that we discussed and illustrated in Section 4.10 is not always the easiest method available. Two other methods generally are simpler to use. The first is useful if the network contains only independent sources. To calculate $R_{\mathrm{Th}}$ for such a network, we first deactivate all independent sources and then calculate the resistance seen looking into the network at the designated terminal pair. A voltage source is deactivated by replacing it with a short circuit. A current source is deactivated by replacing it with an open circuit. For example, consider the circuit shown in Fig. 4.52. Deactivating the independent sources simplifies the circuit to the one shown in Fig. 4.53. The resistance seen looking into the terminals $\mathrm{a}, \mathrm{b}$ is denoted $R_{\mathrm{ab}}$, which consists of the $4 \Omega$ resistor in series with the parallel combinations of the 5 and $20 \Omega$ resistors. Thus,

$$
\begin{equation*}
R_{\mathrm{ab}}=R_{\mathrm{Th}}=4+\frac{5 \times 20}{25}=8 \Omega . \tag{4.63}
\end{equation*}
$$

Note that the derivation of $R_{\text {Th }}$ with Eq. 4.63 is much simpler than the same derivation with Eqs. 4.57-4.62.
image_name:Figure 4.52
description:
[
'name': 'V1', 'type': 'VoltageSource', 'value': '25V', 'ports': {'Np': 'd', 'Nn': 'b'
'name': 'R1', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'd', 'N2': 'c'
'name': 'R2', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'c', 'N2': 'b'
'name': 'I1', 'type': 'CurrentSource', 'value': '3A', 'ports': {'Np': 'b', 'Nn': 'c'
'name': 'R3', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'c', 'N2': 'a'
]
extrainfo:The circuit is a series-parallel network used to determine the Thévenin equivalent resistance across terminals a and b. It consists of a voltage source, a current source, and resistors in series and parallel configurations.


Figure 4.52 - A circuit used to illustrate a Thévenin equivalent.
image_name:Figure 4.53
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R2', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'c', 'N2': 'b'
'name': 'R3', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'c', 'N2': 'a'
]
extrainfo:The circuit is a series-parallel network used to determine the Thévenin equivalent resistance across terminals a and b. It consists of resistors in series and parallel configurations. The resistors R1 and R2 form a parallel connection, and this combination is in series with R3.


Figure 4.53 $\triangle$ The circuit shown in Fig. 4.52 after deactivation of the independent sources.

If the circuit or network contains dependent sources, an alternative procedure for finding the Thévenin resistance $R_{\mathrm{Th}}$ is as follows. We first deactivate all independent sources, and we then apply either a test voltage source or a test current source to the Thévenin terminals a,b. The Thévenin resistance equals the ratio of the voltage across the test source to the current delivered by the test source. Example 4.11 illustrates this alternative procedure for finding $R_{\mathrm{Th}}$, using the same circuit as Example 4.10.

#### Example 4.11 Finding the Thévenin Equivalent Using a Test Source

Find the Thévenin resistance $R_{\mathrm{Th}}$ for the circuit in Fig. 4.49, using the alternative method described.

#### Solution

We first deactivate the independent voltage source from the circuit and then excite the circuit from the terminals a,b with either a test voltage source or a test current source. If we apply a test voltage source, we will know the voltage of the dependent voltage source and hence the controlling current $i$. Therefore we opt for the test voltage source. Figure 4.54 shows the circuit for computing the Thévenin resistance.
image_name:Figure 4.54
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '2kΩ', 'ports': {'N1': 'a', 'N2': 'C'
'name': 'V1', 'type': 'VoltageControlledVoltageSource', 'value': '3vT', 'ports': {'Np': 'C', 'Nn': 'a'
'name': 'G1', 'type': 'CurrentControlledCurrentSource', 'value': '20i', 'ports': {'Np': 'b', 'Nn': 'a'
'name': 'R2', 'type': 'Resistor', 'value': '25Ω', 'ports': {'N1': 'b', 'N2': 'a'
'name': 'V2', 'type': 'VoltageSource', 'value': 'vT', 'ports': {'Np': 'b', 'Nn': 'a'
]
extrainfo:The circuit is used to compute the Thévenin resistance by applying a test voltage source vT and measuring the current iT. The dependent current source is controlled by the current i through R1.


Figure $4.54 \triangle$ An alternative method for computing the Thévenin resistance.

The externally applied test voltage source is denoted $v_{T}$, and the current that it delivers to the circuit is labeled $i_{T}$. To find the Thévenin resistance, we simply solve the circuit shown in Fig. 4.54 for the ratio of the voltage to the current at the test source; that is, $R_{\mathrm{Th}}=v_{T} / i_{T}$. From Fig. 4.54,

$$
\begin{align*}
i_{T} & =\frac{v_{T}}{25}+20 i  \tag{4.64}\\
i & =\frac{-3 v_{T}}{2} \mathrm{~mA} \tag{4.65}
\end{align*}
$$

We then substitute Eq. 4.65 into Eq. 4.64 and solve the resulting equation for the ratio $v_{T} / i_{T}$ :

$$
\begin{gather*}
i_{T}=\frac{v_{T}}{25}-\frac{60 v_{T}}{2000}  \tag{4.66}\\
\frac{i_{T}}{v_{T}}=\frac{1}{25}-\frac{6}{200}=\frac{50}{5000}=\frac{1}{100} \tag{4.67}
\end{gather*}
$$

From Eqs. 4.66 and 4.67,

$$
\begin{equation*}
R_{\mathrm{Th}}=\frac{v_{T}}{i_{T}}=100 \Omega \tag{4.68}
\end{equation*}
$$

image_name:Figure 4.55
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'b', 'N2': 'd'
'name': 'RC', 'type': 'Resistor', 'value': 'RC', 'ports': {'N1': 'a', 'N2': 'e'
'name': 'RE', 'type': 'Resistor', 'value': 'RE', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'VCC', 'type': 'VoltageSource', 'value': 'VCC', 'ports': {'Np': 'a', 'Nn': 'd'
'name': 'V0', 'type': 'VoltageSource', 'value': 'V0', 'ports': {'Np': 'b', 'Nn': 'c'
'name': 'βiB', 'type': 'CurrentControlledCurrentSource', 'ports': {'Np': 'e', 'Nn': 'c'
]
extrainfo:The circuit is a typical amplifier configuration using a Thévenin equivalent approach. It consists of resistors, a voltage source, and a current-controlled current source. The nodes are labeled as a, b, c, and d, with node d being the ground reference. The current-controlled current source is controlled by the base current iB.


Figure 4.55 $\boldsymbol{\Delta}$ The application of a Thévenin equivalent in circuit analysis.

In general, these computations are easier than those involved in computing the short-circuit current. Moreover, in a network containing only resistors and dependent sources, you must use the alternative method, because the ratio of the Thévenin voltage to the short-circuit current is indeterminate. That is, it is the ratio $0 / 0$.

Using the Thévenin Equivalent in the Amplifier Circuit

At times we can use a Thévenin equivalent to reduce one portion of a circuit to greatly simplify analysis of the larger network. Let's return to the circuit first introduced in Section 2.5 and subsequently analyzed in Sections 4.4 and 4.7. To aid our discussion, we redrew the circuit and identified the branch currents of interest, as shown in Fig. 4.55.

As our previous analysis has shown, $i_{B}$ is the key to finding the other branch currents. We redraw the circuit as shown in Fig. 4.56 to prepare to replace the subcircuit to the left of $V_{0}$ with its Thévenin equivalent. You
image_name:Figure 4.56
description:
[
'name': 'VCC', 'type': 'VoltageSource', 'value': 'VCC', 'ports': {'Np': 'a', 'Nn': 'd'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'b', 'N2': 'd'
'name': 'RC', 'type': 'Resistor', 'value': 'RC', 'ports': {'N1': "a'", 'N2': 'e'
'name': 'RE', 'type': 'Resistor', 'value': 'RE', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'V0', 'type': 'VoltageSource', 'value': 'V0', 'ports': {'Np': 'b', 'Nn': 'c'
'name': 'βiB', 'type': 'CurrentControlledCurrentSource', 'ports': {'Np': 'e', 'Nn': 'c'
]
extrainfo:The circuit is a modified version with a Thévenin equivalent replacement. The branch currents i1, i2, iB, and iE remain unaffected by this modification.


Figure 4.56 $\triangle$ A modified version of the circuit shown in Fig. 4.55.
image_name:Figure 4.57
description:
[
'name': 'R_Th', 'type': 'Resistor', 'value': 'R_Th', 'ports': {'N1': 'e', 'N2': 'b'
'name': 'R_C', 'type': 'Resistor', 'value': 'R_C', 'ports': {'N1': 'a', 'N2': 'f'
'name': 'R_E', 'type': 'Resistor', 'value': 'R_E', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'V_Th', 'type': 'VoltageSource', 'value': 'V_Th', 'ports': {'Np': 'e', 'Nn': 'd'
'name': 'V_CC', 'type': 'VoltageSource', 'value': 'V_CC', 'ports': {'Np': 'a', 'Nn': 'd'
'name': 'V_0', 'type': 'VoltageSource', 'value': 'V_0', 'ports': {'Np': 'b', 'Nn': 'c'
'name': 'βi_B', 'type': 'CurrentControlledCurrentSource', 'ports': {'Np': 'f', 'Nn': 'c'
]
extrainfo:The circuit is a modified version with a Thévenin equivalent replacement. The branch currents i1, i2, iB, and iE remain unaffected by this modification.


Figure 4.57 $\triangle$ The circuit shown in Fig. 4.56 modified by a Thévenin equivalent.
should be able to determine that this modification has no effect on the branch currents $i_{1}, i_{2}, i_{B}$, and $i_{E}$.

Now we replace the circuit made up of $V_{C C}, R_{1}$, and $R_{2}$ with a Thévenin equivalent, with respect to the terminals b, d . The Thévenin voltage and resistance are

$$
\begin{align*}
V_{\mathrm{Th}} & =\frac{V_{C C} R_{2}}{R_{1}+R_{2}}  \tag{4.69}\\
R_{\mathrm{Th}} & =\frac{R_{1} R_{2}}{R_{1}+R_{2}} \tag{4.70}
\end{align*}
$$

With the Thévenin equivalent, the circuit in Fig. 4.56 becomes the one shown in Fig. 4.57.

We now derive an equation for $i_{B}$ simply by summing the voltages around the left mesh. In writing this mesh equation, we recognize that $i_{E}=(1+\beta) i_{B}$. Thus,

$$
\begin{equation*}
V_{\mathrm{Th}}=R_{\mathrm{Th}} i_{B}+V_{0}+R_{E}(1+\beta) i_{B} \tag{4.71}
\end{equation*}
$$

from which

$$
\begin{equation*}
i_{B}=\frac{V_{\mathrm{Th}}-V_{0}}{R_{\mathrm{Th}}+(1+\beta) R_{E}} . \tag{4.72}
\end{equation*}
$$

When we substitute Eqs. 4.69 and 4.70 into Eq. 4.72, we get the same expression obtained in Eq. 2.25. Note that when we have incorporated the Thévenin equivalent into the original circuit, we can obtain the solution for $i_{B}$ by writing a single equation.

ASSESSMENT PROBLEMS

Objective 5-Understand Thévenin and Norton equivalents

4.19 Find the Thévenin equivalent circuit with respect to the terminals $a, b$ for the circuit shown.

Answer: $\quad V_{\mathrm{Th}}=v_{\mathrm{ab}}=8 \mathrm{~V}, R_{\mathrm{Th}}=1 \Omega$.
image_name:Figure
description:
[
'name': '24V', 'type': 'VoltageSource', 'value': '24V', 'ports': {'Np': 'C', 'Nn': 'b'
'name': '2Ω', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'C', 'N2': 'a'
'name': '4A', 'type': 'CurrentSource', 'value': '4A', 'ports': {'Np': 'a', 'Nn': 'b'
'name': '8Ω', 'type': 'Resistor', 'value': '8Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '3ix', 'type': 'CurrentControlledVCurrentSource', 'ports': {'N1': 'a', 'N2': 'C'
]
extrainfo:This is a circuit with a voltage source, a current source, resistors, and a current-controlled voltage source. The circuit is used to find the Thévenin equivalent with respect to terminals a and b.


NOTE: Also try Chapter Problems 4.74 and 4.79.
4.20 Find the Thévenin equivalent circuit with respect to the terminals $\mathrm{a}, \mathrm{b}$ for the circuit shown. (Hint: Define the voltage at the leftmost node as $v$, and write two nodal equations with $V_{\mathrm{Th}}$ as the right node voltage.)

Answer: $\quad V_{\mathrm{Th}}=v_{\mathrm{ab}}=30 \mathrm{~V}, R_{\mathrm{Th}}=10 \Omega$.
image_name:Figure
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '60Ω', 'ports': {'N1': 'c', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'R3', 'type': 'Resistor', 'value': '80Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R4', 'type': 'Resistor', 'value': '40Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'I1', 'type': 'CurrentSource', 'value': '4A', 'ports': {'Np': 'b', 'Nn': 'c'
'name': 'V1', 'type': 'CurrentControlledVoltageSource', 'value': '160iΔ', 'ports': {'Np': 'd', 'Nn': 'a'
]
extrainfo:The circuit is used to find the Thévenin equivalent with respect to terminals a and b. The voltage controlled voltage source is controlled by the current iΔ flowing through the 40Ω resistor. The Thévenin equivalent voltage V_Th = 30V and resistance R_Th = 10Ω.

image_name:Figure 4.58
description:
[
'name': 'RL', 'type': 'Resistor', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit is used to analyze maximum power transfer with respect to terminals a and b. It includes a resistive network with independent and dependent sources. The load resistor RL is connected across terminals a and b.


Figure $4.58 \triangle$ A circuit describing maximum power transfer.
image_name:Figure 4.59
description:
[
'name': 'V_Th', 'type': 'VoltageSource', 'value': 'V_Th', 'ports': {'Np': 'c', 'Nn': 'b'
'name': 'R_Th', 'type': 'Resistor', 'value': 'R_Th', 'ports': {'N1': 'c', 'N2': 'a'
'name': 'R_L', 'type': 'Resistor', 'value': 'R_L', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit is used to analyze maximum power transfer with respect to terminals a and b. It includes a Thévenin equivalent voltage source (V_Th) and resistance (R_Th) connected in series with a load resistor (R_L). The current i flows from node a to node b through R_L.


Figure $4.59 \triangle \mathrm{~A}$ circuit used to determine the value of $R_{L}$ for maximum power transfer.

Condition for maximum power transfer

## 4.12 Maximum Power Transfer

Circuit analysis plays an important role in the analysis of systems designed to transfer power from a source to a load. We discuss power transfer in terms of two basic types of systems. The first emphasizes the efficiency of the power transfer. Power utility systems are a good example of this type because they are concerned with the generation, transmission, and distribution of large quantities of electric power. If a power utility system is inefficient, a large percentage of the power generated is lost in the transmission and distribution processes, and thus wasted.

The second basic type of system emphasizes the amount of power transferred. Communication and instrumentation systems are good examples because in the transmission of information, or data, via electric signals, the power available at the transmitter or detector is limited. Thus, transmitting as much of this power as possible to the receiver, or load, is desirable. In such applications the amount of power being transferred is small, so the efficiency of transfer is not a primary concern. We now consider maximum power transfer in systems that can be modeled by a purely resistive circuit.

Maximum power transfer can best be described with the aid of the circuit shown in Fig. 4.58. We assume a resistive network containing independent and dependent sources and a designated pair of terminals, a,b, to which a load, $R_{L}$, is to be connected. The problem is to determine the value of $R_{L}$ that permits maximum power delivery to $R_{L}$. The first step in this process is to recognize that a resistive network can always be replaced by its Thévenin equivalent. Therefore, we redraw the circuit shown in Fig. 4.58 as the one shown in Fig. 4.59. Replacing the original network by its Thévenin equivalent greatly simplifies the task of finding $R_{L}$. Derivation of $R_{L}$ requires expressing the power dissipated in $R_{L}$ as a function of the three circuit parameters $V_{\mathrm{Th}}, R_{\mathrm{Th}}$, and $R_{L}$. Thus

$$
\begin{equation*}
p=i^{2} R_{L}=\left(\frac{V_{\mathrm{Th}}}{R_{\mathrm{Th}}+R_{\mathrm{L}}}\right)^{2} R_{L} \tag{4.73}
\end{equation*}
$$

Next, we recognize that for a given circuit, $V_{\mathrm{Th}}$ and $R_{\mathrm{Th}}$ will be fixed. Therefore the power dissipated is a function of the single variable $R_{L}$. To find the value of $R_{L}$ that maximizes the power, we use elementary calculus. We begin by writing an equation for the derivative of $p$ with respect to $R_{L}$ :

$$
\begin{equation*}
\frac{d p}{d R_{L}}=V_{\mathrm{Th}}^{2}\left[\frac{\left(R_{\mathrm{Th}}+R_{L}\right)^{2}-R_{L} \cdot 2\left(R_{\mathrm{Th}}+R_{L}\right)}{\left(R_{\mathrm{Th}}+R_{L}\right)^{4}}\right] \tag{4.74}
\end{equation*}
$$

The derivative is zero and $p$ is maximized when

$$
\begin{equation*}
\left(R_{\mathrm{Th}}+R_{L}\right)^{2}=2 R_{L}\left(R_{\mathrm{Th}}+R_{L}\right) \tag{4.75}
\end{equation*}
$$

Solving Eq. 4.75 yields

$$
\begin{equation*}
R_{L}=R_{\mathrm{Th}} \tag{4.76}
\end{equation*}
$$

Thus maximum power transfer occurs when the load resistance $R_{L}$ equals the Thévenin resistance $R_{\mathrm{Th}}$. To find the maximum power delivered to $R_{L}$, we simply substitute Eq. 4.76 into Eq. 4.73:

$$
\begin{equation*}
p_{\max }=\frac{V_{\mathrm{Th}}^{2} R_{L}}{\left(2 R_{L}\right)^{2}}=\frac{V_{\mathrm{Th}}^{2}}{4 R_{L}} \tag{4.77}
\end{equation*}
$$

The analysis of a circuit when the load resistor is adjusted for maximum power transfer is illustrated in Example 4.12.

#### Example 4.12 Calculating the Condition for Maximum Power Transfer

a) For the circuit shown in Fig. 4.60, find the value of $R_{L}$ that results in maximum power being transferred to $R_{L}$.
image_name:Figure 4.60
description:
[
'name': 'Voltage Source', 'type': 'VoltageSource', 'value': '360V', 'ports': {'Np': 'C', 'Nn': 'b'
'name': 'Resistor1', 'type': 'Resistor', 'value': '30Ω', 'ports': {'N1': 'C', 'N2': 'a'
'name': 'Resistor2', 'type': 'Resistor', 'value': '150Ω', 'ports': {'N1': 'b', 'N2': 'a'
'name': 'RL', 'type': 'Resistor', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit is designed for maximum power transfer to the load resistor RL. The Thévenin equivalent voltage is calculated as 300V and the Thévenin resistance is 25Ω.


Figure 4.60 $\Delta$ The circuit for Example 4.12.
b) Calculate the maximum power that can be delivered to $R_{L}$.
c) When $R_{L}$ is adjusted for maximum power transfer, what percentage of the power delivered by the 360 V source reaches $R_{L}$ ?

#### Solution

a) The Thévenin voltage for the circuit to the left of the terminals $a, b$ is

$$
V_{\mathrm{Th}}=\frac{150}{180}(360)=300 \mathrm{~V}
$$

The Thévenin resistance is

$$
R_{\mathrm{Th}}=\frac{(150)(30)}{180}=25 \Omega
$$

Replacing the circuit to the left of the terminals a,b with its Thévenin equivalent gives us the circuit shown in Fig. 4.61, which indicates that $R_{L}$ must equal $25 \Omega$ for maximum power transfer.
image_name:Figure 4.61
description:
[
'name': '300V', 'type': 'VoltageSource', 'value': '300V', 'ports': {'Np': 'c', 'Nn': 'b'
'name': '25Ω', 'type': 'Resistor', 'value': '25Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'RL', 'type': 'Resistor', 'value': 'RL', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit is a Thévenin equivalent with a 300V voltage source, a 25Ω resistor, and a load resistor RL connected between nodes a and b.


Figure $4.61 \triangle$ Reduction of the circuit shown in Fig. 4.60 by means of a Thévenin equivalent.
b) The maximum power that can be delivered to $R_{L}$ is

$$
p_{\max }=\left(\frac{300}{50}\right)^{2}(25)=900 \mathrm{~W}
$$

c) When $R_{L}$ equals $25 \Omega$, the voltage $v_{\mathrm{ab}}$ is

$$
v_{\mathrm{ab}}=\left(\frac{300}{50}\right)(25)=150 \mathrm{~V}
$$

From Fig. 4.60, when $v_{\text {ab }}$ equals 150 V , the current in the voltage source in the direction of the voltage rise across the source is

$$
i_{s}=\frac{360-150}{30}=\frac{210}{30}=7 \mathrm{~A}
$$

Therefore, the source is delivering 2520 W to the circuit, or

$$
p_{s}=-i_{s}(360)=-2520 \mathrm{~W}
$$

The percentage of the source power delivered to the load is

$$
\frac{900}{2520} \times 100=35.71 \%
$$

ASSESSMENT PROBLEMS

Objective 6—Know the condition for and calculate maximum power transfer to resistive load

4.21 a) Find the value of $R$ that enables the circuit shown to deliver maximum power to the terminals a,b.
b) Find the maximum power delivered to $R$.
image_name:Circuit for Assessment Problem 4.21
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'R2', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'a', 'N2': 'e'
'name': 'R3', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'd', 'N2': 'a'
'name': 'R4', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'd', 'N2': 'f'
'name': 'R5', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'a', 'N2': 'e'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'V1', 'type': 'VoltageSource', 'value': '100V', 'ports': {'Np': 'c', 'Nn': 'b'
'name': 'V2', 'type': 'VoltageSource', 'value': '20V', 'ports': {'Np': 'f', 'Nn': 'b'
'name': 'Vφ', 'type': 'VoltageControlledVoltageSource', 'ports': {'Np': 'e', 'Nn': 'c'
]
extrainfo:The circuit contains two independent voltage sources and one dependent voltage source. The resistors are arranged in a network connecting nodes a, b, c, d, and e. The dependent voltage source is controlled by the voltage across node d.


Answer:
(a) $3 \Omega$;
(b) 1.2 kW .

NOTE: Also try Chapter Problems 4.88 and 4.90.
4.22 Assume that the circuit in Assessment Problem 4.21 is delivering maximum power to the load resistor $R$.
a) How much power is the 100 V source delivering to the network?
b) Repeat (a) for the dependent voltage source.
c) What percentage of the total power generated by these two sources is delivered to the load resistor $R$ ?

Answer: (a) 3000 W ;
(b) 800 W ;
(c) $31.58 \%$.

## 4.13 Superposition

A linear system obeys the principle of superposition, which states that whenever a linear system is excited, or driven, by more than one independent source of energy, the total response is the sum of the individual responses. An individual response is the result of an independent source acting alone. Because we are dealing with circuits made up of interconnected linear-circuit elements, we can apply the principle of superposition directly to the analysis of such circuits when they are driven by more than one independent energy source. At present, we restrict the discussion to simple resistive networks; however, the principle is applicable to any linear system.

Superposition is applied in both the analysis and the design of circuits. In analyzing a complex circuit with multiple independent voltage and current sources, there are often fewer, simpler equations to solve when the effects of the independent sources are considered one at a time. Applying superposition can thus simplify circuit analysis. Be aware, though, that sometimes applying superposition actually complicates the analysis, producing more equations to solve than with an alternative method. Superposition is required only if the independent sources in a circuit are fundamentally different. In these early chapters, all independent sources are dc sources, so superposition is not required. We introduce superposition here in anticipation of later chapters in which circuits will require it.

Superposition is applied in design to synthesize a desired circuit response that could not be achieved in a circuit with a single source. If the desired circuit response can be written as a sum of two or more terms, the response can be realized by including one independent source for each term of the response. This approach to the design of circuits with complex responses allows a designer to consider several simple designs instead of one complex design.

We demonstrate the superposition principle by using it to find the branch currents in the circuit shown in Fig. 4.62. We begin by finding the branch currents resulting from the 120 V voltage source. We denote those currents with a prime. Replacing the ideal current source with an open circuit deactivates it; Fig. 4.63 shows this. The branch currents in this circuit are the result of only the voltage source.

We can easily find the branch currents in the circuit in Fig. 4.63 once we know the node voltage across the $3 \Omega$ resistor. Denoting this voltage $v_{1}$, we write

$$
\begin{equation*}
\frac{v_{1}-120}{6}+\frac{v_{1}}{3}+\frac{v_{1}}{2+4}=0 \tag{4.78}
\end{equation*}
$$

from which

$$
\begin{equation*}
v_{1}=30 \mathrm{~V} \tag{4.79}
\end{equation*}
$$

Now we can write the expressions for the branch currents $i_{1}^{\prime}-i_{4}^{\prime}$ directly:

$$
\begin{align*}
& i_{1}^{\prime}=\frac{120-30}{6}=15 \mathrm{~A}  \tag{4.80}\\
& i_{2}^{\prime}=\frac{30}{3}=10 \mathrm{~A}  \tag{4.81}\\
& i_{3}^{\prime}=i_{4}^{\prime}=\frac{30}{6}=5 \mathrm{~A} \tag{4.82}
\end{align*}
$$

To find the component of the branch currents resulting from the current source, we deactivate the ideal voltage source and solve the circuit shown in Fig. 4.64. The double-prime notation for the currents indicates they are the components of the total current resulting from the ideal current source.

We determine the branch currents in the circuit shown in Fig. 4.64 by first solving for the node voltages across the 3 and $4 \Omega$ resistors, respectively. Figure 4.65 shows the two node voltages. The two node-voltage equations that describe the circuit are

$$
\begin{align*}
& \frac{v_{3}}{3}+\frac{v_{3}}{6}+\frac{v_{3}-v_{4}}{2}=0  \tag{4.83}\\
& \frac{v_{4}-v_{3}}{2}+\frac{v_{4}}{4}+12=0 \tag{4.84}
\end{align*}
$$

Solving Eqs. 4.83 and 4.84 for $v_{3}$ and $v_{4}$, we get

$$
\begin{align*}
& v_{3}=-12 \mathrm{~V}  \tag{4.85}\\
& v_{4}=-24 \mathrm{~V} \tag{4.86}
\end{align*}
$$

Now we can write the branch currents $i_{1}^{\prime \prime}$ through $i_{4}^{\prime \prime}$ directly in terms of the node voltages $v_{3}$ and $v_{4}$ :

$$
\begin{equation*}
i_{1}^{\prime \prime}=\frac{-v_{3}}{6}=\frac{12}{6}=2 \mathrm{~A} \tag{4.87}
\end{equation*}
$$

image_name:Figure 4.62
description:
[
'name': '120V', 'type': 'VoltageSource', 'value': '120V', 'ports': {'Np': 'a', 'Nn': 'd'
'name': '6Ω', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '2Ω', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': '3Ω', 'type': 'Resistor', 'value': '3Ω', 'ports': {'N1': 'b', 'N2': 'd'
'name': '4Ω', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': '12A', 'type': 'CurrentSource', 'value': '12A', 'ports': {'Np': 'c', 'Nn': 'd'
]
extrainfo:The circuit is a delta configuration with a 120V voltage source and a 12A current source. It includes resistors of 6Ω, 2Ω, 3Ω, and 4Ω. The nodes are labeled as a, b, c, and d, with current directions indicated for i1, i2, i3, and i4.


Figure 4.62 $\triangle \mathrm{A}$ circuit used to illustrate superposition.
image_name:Figure 4.63
description:
[
'name': '120V', 'type': 'VoltageSource', 'ports': {'Np': 'a', 'Nn': 'GND'
'name': '6Ω', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'a', 'N2': 'v1'
'name': '3Ω', 'type': 'Resistor', 'value': '3Ω', 'ports': {'N1': 'v1', 'N2': 'GND'
'name': '2Ω', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'v1', 'N2': 'V2'
'name': '4Ω', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'V2', 'N2': 'GND'
]
extrainfo:The circuit is a delta configuration with a 120V voltage source and a 12A current source. It includes resistors of 6Ω, 2Ω, 3Ω, and 4Ω. The nodes are labeled as a, b, c, and d, with current directions indicated for i1, i2, i3, and i4. The circuit illustrates superposition.


Figure 4.63 $\Delta$ The circuit shown in Fig. 4.62 with the current source deactivated.
image_name:Figure 4.63
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'a', 'N2': 'GND'
'name': 'R2', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'v1', 'N2': 'v2'
'name': 'R3', 'type': 'Resistor', 'value': '3Ω', 'ports': {'N1': 'v1', 'N2': 'GND'
'name': 'R4', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'v2', 'N2': 'GND'
]
extrainfo:The circuit is a delta configuration with a 12A current source. It includes resistors of 6Ω, 2Ω, 3Ω, and 4Ω connected between nodes a and b. The currents i1, i2, i3, and i4 are indicated in the diagram.


Figure 4.64 $\boldsymbol{\triangle}$ The circuit shown in Fig. 4.62 with the voltage source deactivated.
image_name:Figure 4.65
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'R2', 'type': 'Resistor', 'value': '2Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R3', 'type': 'Resistor', 'value': '3Ω', 'ports': {'N1': 'c', 'N2': 'a'
'name': 'R4', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'I1', 'type': 'CurrentSource', 'value': '12A', 'ports': {'Np': 'b', 'Nn': 'c'
]
extrainfo:The circuit is a delta configuration with a 12A current source. Node voltages v3 and v4 are indicated. The resistors are connected between nodes a, b, and c.


Figure 4.65 $\triangle$ The circuit shown in Fig. 4.64 showing the node voltages $v_{3}$ and $v_{4}$.

$$
\begin{align*}
& i_{2}^{\prime \prime}=\frac{v_{3}}{3}=\frac{-12}{3}=-4 \mathrm{~A},  \tag{4.88}\\
& i_{3}^{\prime \prime}=\frac{v_{3}-v_{4}}{2}=\frac{-12+24}{2}=6 \mathrm{~A},  \tag{4.89}\\
& i_{4}^{\prime \prime}=\frac{v_{4}}{4}=\frac{-24}{4}=-6 \mathrm{~A} . \tag{4.90}
\end{align*}
$$

To find the branch currents in the original circuit, that is, the currents $i_{1}, i_{2}, i_{3}$, and $i_{4}$ in Fig. 4.62, we simply add the currents given by Eqs. 4.87-4.90 to the currents given by Eqs. 4.80-4.82:

$$
\begin{align*}
& i_{1}=i_{1}^{\prime}+i_{1}^{\prime \prime}=15+2=17 \mathrm{~A}  \tag{4.91}\\
& i_{2}=i_{2}^{\prime}+i_{2}^{\prime \prime}=10-4=6 \mathrm{~A}  \tag{4.92}\\
& i_{3}=i_{3}^{\prime}+i_{3}^{\prime \prime}=5+6=11 \mathrm{~A}  \tag{4.93}\\
& i_{4}=i_{4}^{\prime}+i_{4}^{\prime \prime}=5-6=-1 \mathrm{~A} \tag{4.94}
\end{align*}
$$

You should verify that the currents given by Eqs. 4.91-4.94 are the correct values for the branch currents in the circuit shown in Fig. 4.62.

When applying superposition to linear circuits containing both independent and dependent sources, you must recognize that the dependent sources are never deactivated. Example 4.13 illustrates the application of superposition when a circuit contains both dependent and independent sources.

#### Example 4.13 Using Superposition to Solve a Circuit

Use the principle of superposition to find $v_{o}$ in the circuit shown in Fig. 4.66.
image_name:Figure 4.66
description:
[
'name': '10V', 'type': 'VoltageSource', 'value': '10V', 'ports': {'Np': 'a', 'Nn': 'd'
'name': '5Ω', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '0.4vΔ', 'type': 'VoltageControlledVoltageSource', 'value': '0.4vΔ', 'ports': {'Np': 'c', 'Nn': 'b'
'name': '20Ω', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'b', 'N2': 'd'
'name': '2iΔ', 'type': 'CurrentControlledVoltageSource', 'value': '2iΔ', 'ports': {'Np': 'e', 'Nn': 'd'
'name': '10Ω', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'c', 'N2': 'e'
'name': '5A', 'type': 'CurrentSource', 'value': '5A', 'ports': {'Np': 'e', 'Nn': 'c'
]
extrainfo:The circuit contains both independent and dependent sources, including a voltage-controlled voltage source and a current-controlled voltage source. The principle of superposition can be applied to analyze the circuit.


Figure 4.66 $\triangle$ The circuit for Example 4.13.

#### Solution

We begin by finding the component of $v_{o}$ resulting from the 10 V source. Figure 4.67 shows the circuit. With the 5 A source deactivated, $v_{\Delta}^{\prime}$ must equal
$\left(-0.4 v_{\Delta}^{\prime}\right)(10)$. Hence, $v_{\Delta}^{\prime}$ must be zero, the branch containing the two dependent sources is open, and

$$
v_{o}^{\prime}=\frac{20}{25}(10)=8 \mathrm{~V}
$$

image_name:Figure 4.67
description:
[
'name': '10V', 'type': 'VoltageSource', 'value': '10V', 'ports': {'Np': 'a', 'Nn': 'd'
'name': '5Ω', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '20Ω', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'b', 'N2': 'd'
'name': '10Ω', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'c', 'N2': 'e'
'name': "0.4v'", 'type': 'VoltageControlledCurrentSource', 'ports': {'Np': 'c', 'Nn': 'b'
'name': "2i'", 'type': 'CurrentControlledVoltageSource', 'ports': {'Np': 'e', 'Nn': 'd'
]
extrainfo:The circuit contains a voltage source, resistors, a voltage-controlled current source, and a current-controlled voltage source.


Figure 4.67 $\Delta$ The circuit shown in Fig. 4.66 with the 5 A source deactivated.

When the 10 V source is deactivated, the circuit reduces to the one shown in Fig. 4.68. We have added a reference node and the node designations $\mathrm{a}, \mathrm{b}$, and c to aid the discussion. Summing the currents away from node a yields

$$
\frac{v_{o}^{\prime \prime}}{20}+\frac{v_{o}^{\prime \prime}}{5}-0.4 v_{\Delta}^{\prime \prime}=0, \quad \text { or } \quad 5 v_{o}^{\prime \prime}-8 v_{\Delta}^{\prime \prime}=0
$$

Summing the currents away from node b gives

$$
\begin{aligned}
0.4 v_{\Delta}^{\prime \prime}+\frac{v_{\mathrm{b}}-2 i_{\Delta}^{\prime \prime}}{10}-5 & =0, \text { or } \\
4 v_{\Delta}^{\prime \prime}+v_{b}-2 i_{\Delta}^{\prime \prime} & =50
\end{aligned}
$$

We now use

$$
v_{\mathrm{b}}=2 \mathrm{i}_{\Delta}^{\prime \prime}+v_{\Delta}^{\prime \prime}
$$

to find the value for $v_{\Delta}^{\prime \prime}$. Thus,

$$
5 v_{\Delta}^{\prime \prime}=50, \quad \text { or } \quad v_{\Delta}^{\prime \prime}=10 \mathrm{~V}
$$

From the node a equation,

$$
5 v_{0}^{\prime \prime}=80, \quad \text { or } \quad v_{0}^{\prime \prime}=16 \mathrm{~V}
$$

The value of $v_{o}$ is the sum of $v_{o}^{\prime}$ and $v_{o}^{\prime \prime}$, or 24 V .
image_name:Figure 4.68 Δ
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'GND', 'N2': 'a'
'name': 'R2', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'a', 'N2': 'GND'
'name': 'R3', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'G1', 'type': 'VoltageControlledCurrentSource', 'value': '0.4vΔ"', 'ports': {'Np': 'b', 'Nn': 'a'
'name': 'G2', 'type': 'CurrentControlledVoltageSource', 'value': '2iΔ"', 'ports': {'Np': 'c', 'Nn': 'GND'
'name': 'I1', 'type': 'CurrentSource', 'value': '5A', 'ports': {'Np': 'c', 'Nn': 'b'
]
extrainfo:The circuit contains a voltage-controlled voltage source and a current-controlled voltage source, with resistors forming a loop between nodes a, b, and c. The current source provides 5A between nodes b and c. Voltage across R1 is vo" and across R3 is vΔ".


Figure $4.68 \boldsymbol{\Delta}$ The circuit shown in Fig. 4.66 with the 10 V source deactivated.

NOTE: Assess your understanding of this material by trying Chapter Problems 4.93 and 4.98.

#Practical Perspective

Circuits with Realistic Resistors

It is not possible to fabricate identical electrical components. For example, resistors produced from the same manufacturing process can vary in value by as much as $20 \%$. Therefore, in creating an electrical system the designer must consider the impact that component variation will have on the performance of the system. One way to evaluate this impact is by performing sensitivity analysis. Sensitivity analysis permits the designer to calculate the impact of variations in the component values on the output of the system. We will see how this information enables a designer to specify an acceptable component value tolerance for each of the system's components.

Consider the circuit shown in Fig. 4.69. To illustrate sensitivity analysis, we will investigate the sensitivity of the node voltages $v_{1}$ and $v_{2}$ to changes in the resistor $R_{1}$. Using nodal analysis we can derive the expressions for $v_{1}$ and $v_{2}$ as functions of the circuit resistors and source currents. The results are given in Eqs. 4.95 and 4.96:

$$
\begin{align*}
& v_{1}=\frac{R_{1}\left\{R_{3} R_{4} I_{g 2}-\left[R_{2}\left(R_{3}+R_{4}\right)+R_{3} R_{4}\right] I_{g 1}\right\}}{\left(R_{1}+R_{2}\right)\left(R_{3}+R_{4}\right)+R_{3} R_{4}}  \tag{4.95}\\
& v_{2}=\frac{R_{3} R_{4}\left[\left(R_{1}+R_{2}\right) I_{g 2}-R_{1} I_{g 1}\right]}{\left(R_{1}+R_{2}\right)\left(R_{3}+R_{4}\right)+R_{3} R_{4}} \tag{4.96}
\end{align*}
$$

The sensitivity of $v_{1}$ with respect to $R_{1}$ is found by differentiating Eq. 4.95 with respect to $R_{1}$, and similarly the sensitivity of $v_{2}$ with respect to $R_{1}$ is found by differentiating Eq. 4.96 with respect to $R_{1}$. We get

$$
\begin{equation*}
\frac{d v_{1}}{d R_{1}}=\frac{\left[R_{3} R_{4}+R_{2}\left(R_{3}+R_{4}\right)\right]\left\{R_{3} R_{4} I_{g 2}-\left[R_{3} R_{4}+R_{2}\left(R_{3}+R_{4}\right)\right] I_{g 1}\right\}}{\left[\left(R_{1}+R_{2}\right)\left(R_{3}+R_{4}\right)+R_{3} R_{4}\right]^{2}} \tag{4.97}
\end{equation*}
$$

$$
\begin{equation*}
\frac{d v_{2}}{d R_{1}}=\frac{R_{3} R_{4}\left\{R_{3} R_{4} I_{g 2}-\left[R_{2}\left(R_{3}+R_{4}\right)+R_{3} R_{4}\right] I_{g 1}\right\}}{\left[\left(R_{1}+R_{2}\right)\left(R_{3}+R_{4}\right)+R_{3} R_{4}\right]^{2}} \tag{4.98}
\end{equation*}
$$

image_name:Figure 4.69
description:
[
'name': 'Ig1', 'type': 'CurrentSource', 'value': 'Ig1', 'ports': {'Np': 'a', 'Nn': 'c'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R4', 'type': 'Resistor', 'value': 'R4', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'Ig2', 'type': 'CurrentSource', 'value': 'Ig2', 'ports': {'Np': 'c', 'Nn': 'b'
]
extrainfo:The circuit consists of two current sources (Ig1 and Ig2) and four resistors (R1, R2, R3, R4) connected in a bridge configuration. The voltages v1 and v2 are measured across R1 and R3 respectively. The circuit is used for sensitivity analysis.


Figure 4.69 - Circuit used to introduce sensitivity analysis.

We now consider an example with actual component values to illustrate the use of Eqs. 4.97 and 4.98.

#### Example

Assume the nominal values of the components in the circuit in Fig. 4.69 are: $R_{1}=25 \Omega ; \quad R_{2}=5 \Omega ; \quad R_{3}=50 \Omega ; \quad R_{4}=75 \Omega ; \quad I_{g 1}=12 \mathrm{~A}$ and $I_{g 2}=16 \mathrm{~A}$. Use sensitivity analysis to predict the values of $v_{1}$ and $v_{2}$ if the value of $R_{1}$ is different by $10 \%$ from its nominal value.

#### Solution

From Eqs. 4.95 and 4.96 we find the nominal values of $v_{1}$ and $v_{2}$. Thus

$$
\begin{equation*}
v_{1}=\frac{25\{3750(16)-[5(125)+3750] 12\}}{30(125)+3750}=25 \mathrm{~V} \tag{4.99}
\end{equation*}
$$

and

$$
\begin{equation*}
v_{2}=\frac{3750[30(16)-25(12)]}{30(125)+3750}=90 \mathrm{~V} \tag{4.100}
\end{equation*}
$$

Now from Eqs. 4.97 and 4.98 we can find the sensitivity of $v_{1}$ and $v_{2}$ to changes in $R_{1}$. Hence

$$
\begin{align*}
\frac{d v_{1}}{d R_{1}} & =\frac{[3750+5(125)]-\{3750(16)-[3750+5(125)] 12\}}{[(30)(125)+3750]^{2}} \\
& =\frac{7}{12} \mathrm{~V} / \Omega \tag{4.101}
\end{align*}
$$

and

$$
\begin{align*}
\frac{d v_{2}}{d R_{1}} & =\frac{3750\{3750(16)-[5(125)+3750] 12\}]}{(7500)^{2}} \\
& =0.5 \mathrm{~V} / \Omega \tag{4.102}
\end{align*}
$$

How do we use the results given by Eqs. 4.101 and 4.102? Assume that $R_{1}$ is $10 \%$ less than its nominal value, that is, $R_{1}=22.5 \Omega$. Then $\Delta R_{1}=-2.5 \Omega$ and Eq. 4.101 predicts $\Delta v_{1}$ will be

$$
\Delta v_{1}=\left(\frac{7}{12}\right)(-2.5)=-1.4583 \mathrm{~V}
$$

Therefore, if $R_{1}$ is $10 \%$ less than its nominal value, our analysis predicts that $v_{1}$ will be

$$
\begin{equation*}
v_{1}=25-1.4583=23.5417 \mathrm{~V} \tag{4.103}
\end{equation*}
$$

Similarly for Eq. 4.102 we have

$$
\begin{align*}
\Delta v_{2} & =0.5(-2.5)=-1.25 \mathrm{~V} \\
v_{2} & =90-1.25=88.75 \mathrm{~V} \tag{4.104}
\end{align*}
$$

We attempt to confirm the results in Eqs. 4.103 and 4.104 by substituting the value $R_{1}=22.5 \Omega$ into Eqs. 4.95 and 4.96. When we do, the results are

$$
\begin{align*}
& v_{1}=23.4780 \mathrm{~V}  \tag{4.105}\\
& v_{2}=88.6960 \mathrm{~V} \tag{4.106}
\end{align*}
$$

Why is there a difference between the values predicted from the sensitivity analysis and the exact values computed by substituting for $R_{1}$ in the equations for $v_{1}$ and $v_{2}$ ? We can see from Eqs. 4.97 and 4.98 that the sensitivity of $v_{1}$ and $v_{2}$ with respect to $R_{1}$ is a function of $R_{1}$, because $R_{1}$ appears in the denominator of both Eqs. 4.97 and 4.98. This means that as $R_{1}$ changes, the sensitivities change and hence we cannot expect Eqs. 4.97 and 4.98 to give exact results for large changes in $R_{1}$. Note that for a $10 \%$ change in $R_{1}$, the percent error between the predicted and exact values of $v_{1}$ and $v_{2}$ is small. Specifically, the percent error in $v_{1}=0.2713 \%$ and the percent error in $v_{2}=0.0676 \%$.

From this example, we can see that a tremendous amount of work is involved if we are to determine the sensitivity of $v_{1}$ and $v_{2}$ to changes in the remaining component values, namely $R_{2}, R_{3}, R_{4}, I_{g 1}$, and $I_{g 2}$. Fortunately, PSpice has a sensitivity function that will perform sensitivity analysis for us. The sensitivity function in PSpice calculates two types of sensitivity. The first is known as the one-unit sensitivity, and the second is known as the $1 \%$ sensitivity. In the example circuit, a one-unit change in a resistor would change its value by $1 \Omega$ and a one-unit change in a current source would change its value by 1 A . In contrast, $1 \%$ sensitivity analysis determines the effect of changing resistors or sources by $1 \%$ of their nominal values.

The result of PSpice sensitivity analysis of the circuit in Fig. 4.69 is shown in Table 4.2. Because we are analyzing a linear circuit, we can use superposition to predict values of $v_{1}$ and $v_{2}$ if more than one component's value changes. For example, let us assume $R_{1}$ decreases to $24 \Omega$ and $R_{2}$ decreases to $4 \Omega$. From Table 4.2 we can combine the unit sensitivity of $v_{1}$ to changes in $R_{1}$ and $R_{2}$ to get

$$
\frac{\Delta v_{1}}{\Delta R_{1}}+\frac{\Delta v_{1}}{\Delta R_{2}}=0.5833-5.417=-4.8337 \mathrm{~V} / \Omega
$$

Similarly,

$$
\frac{\Delta v_{2}}{\Delta R_{1}}+\frac{\Delta v_{2}}{\Delta R_{2}}=0.5+6.5=7.0 \mathrm{~V} / \Omega
$$

Thus if both $R_{1}$ and $R_{2}$ decreased by $1 \Omega$ we would predict

$$
\begin{aligned}
& v_{1}=25+4.8227=29.8337 \mathrm{~V} \\
& v_{2}=90-7=83 \mathrm{~V}
\end{aligned}
$$

TABLE 4.2 PSpice Sensitivity Analysis Results

| Element | Element | Element Sensitivity <br> (Volts/Unit) | Normalized Sensitivity <br> (Volts/Percent) |
| :--- | :--- | :--- | :--- |

(a) DC Sensitivities of Node Voltage V1

| R1 | 25 | 0.5833 | 0.1458 |
| :--- | ---: | :---: | :---: |
| R2 | 5 | -5.417 | -0.2708 |
| R3 | 50 | 0.45 | 0.225 |
| R4 | 75 | 0.2 | 0.15 |
| IG1 | 12 | -14.58 | -1.75 |
| IG2 | 16 | 12.5 | 2 |

(b) Sensitivities of Output V2

| R1 | 25 | 0.5 | 0.125 |
| :--- | ---: | :---: | :---: |
| R2 | 5 | 6.5 | 0.325 |
| R3 | 50 | 0.54 | 0.27 |
| R4 | 75 | 0.24 | 0.18 |
| IG1 | 12 | -12.5 | -1.5 |
| IG2 | 16 | 15 | 2.4 |

If we substitute $R_{1}=24 \Omega$ and $R_{2}=4 \Omega$ into Eqs. 4.95 and 4.96 we get

$$
\begin{aligned}
& v_{1}=29.793 \mathrm{~V} \\
& v_{2}=82.759 \mathrm{~V}
\end{aligned}
$$

In both cases our predictions are within a fraction of a volt of the actual node voltage values.

Circuit designers use the results of sensitivity analysis to determine which component value variation has the greatest impact on the output of the circuit. As we can see from the PSpice sensitivity analysis in Table 4.2, the node voltages $v_{1}$ and $v_{2}$ are much more sensitive to changes in $R_{2}$ than to changes in $R_{1}$. Specifically, $v_{1}$ is $(5.417 / 0.5833)$ or approximately 9 times more sensitive to changes in $R_{2}$ than to changes in $R_{1}$ and $v_{2}$ is (6.5/0.5) or 13 times more sensitive to changes in $R_{2}$ than to changes in $R_{1}$. Hence in the example circuit, the tolerance on $R_{2}$ must be more stringent than the tolerance on $R_{1}$ if it is important to keep $v_{1}$ and $v_{2}$ close to their nominal values.

NOTE: Assess your understanding of this Practical Perspective by trying Chapter Problems 4.105-4.107.

## Summary

- For the topics in this chapter, mastery of some basic terms, and the concepts they represent, is necessary. Those terms are node, essential node, path, branch, essential branch, mesh, and planar circuit. Table 4.1 provides definitions and examples of these terms. (See page 91.)
- Two new circuit analysis techniques were introduced in this chapter:
- The node-voltage method works with both planar and nonplanar circuits. A reference node is chosen from among the essential nodes. Voltage variables are assigned at the remaining essential nodes, and Kirchhoff's current law is used to write one equation per voltage variable. The number of equations is $n_{e}-1$, where $n_{e}$ is the number of essential nodes. (See page 93.)
- The mesh-current method works only with planar circuits. Mesh currents are assigned to each mesh, and Kirchhoff's voltage law is used to write one equation per mesh. The number of equations is $b-(n-1)$, where $b$ is the number of branches in which the current is unknown, and $n$ is the number of nodes. The mesh currents are used to find the branch currents. (See page 99.)
- Several new circuit simplification techniques were introduced in this chapter:
- Source transformations allow us to exchange a voltage source $\left(v_{s}\right)$ and a series resistor $(R)$ for a current source $\left(i_{s}\right)$ and a parallel resistor $(R)$ and vice versa. The combinations must be equivalent in terms of their terminal voltage and current. Terminal equivalence holds provided that

$$
i_{s}=\frac{v_{s}}{R}
$$

(See page 109.)

- Thévenin equivalents and Norton equivalents allow us to simplify a circuit comprised of sources and resistors into an equivalent circuit consisting of a voltage source and a series resistor (Thévenin) or a current source and a parallel resistor (Norton). The simplified circuit and the original circuit must be equivalent in terms of their terminal voltage and current. Thus keep in mind that (1) the Thévenin voltage ( $V_{\mathrm{Th}}$ ) is the open-circuit voltage across the terminals of the original circuit, (2) the Thévenin resistance $\left(R_{\mathrm{Th}}\right)$ is the ratio of the Thévenin voltage to the short-circuit current across the terminals of the original circuit; and (3) the Norton equivalent is obtained by performing a source transformation on a Thévenin equivalent. (See page 113.)
- Maximum power transfer is a technique for calculating the maximum value of $p$ that can be delivered to a load, $R_{L}$. Maximum power transfer occurs when $R_{L}=R_{\mathrm{Th}}$, the Thévenin resistance as seen from the resistor $R_{L}$. The equation for the maximum power transferred is

$$
p=\frac{V_{\mathrm{Th}}^{2}}{4 R_{L}}
$$

(See page 120.)

- In a circuit with multiple independent sources, superposition allows us to activate one source at a time and sum the resulting voltages and currents to determine the voltages and currents that exist when all independent sources are active. Dependent sources are never deactivated when applying superposition. (See page 122.)

CHAPTER CONTENTS

5.1 Operational Amplifier Terminals p. 146
5.2 Terminal Voltages and Currents p. 146
5.3 The Inverting-Amplifier Circuit p. 150
5.4 The Summing-Amplifier Circuit p. 152
5.5 The Noninverting-Amplifier Circuit p. 153
5.6 The Difference-Amplifier Circuit p. 155
5.7 A More Realistic Model for the Operational Amplifier p. 159

CHAPTER OBJECTIVES

1 Be able to name the five op amp terminals and describe and use the voltage and current constraints and the resulting simplifications they lead to in an ideal op amp.
2 Be able to analyze simple circuits containing ideal op amps, and recognize the following op amp circuits: inverting amplifier, summing amplifier, noninverting amplifier, and difference amplifier.
3 Understand the more realistic model for an op amp and be able to use this model to analyze simple circuits containing op amps.
