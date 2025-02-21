# 3. Simple Resistive Circuits

Our analytical toolbox now contains Ohm's law and Kirchhoff's laws. In Chapter 2 we used these tools in solving simple circuits. In this chapter we continue applying these tools, but on morecomplex circuits. The greater complexity lies in a greater number of elements with more complicated interconnections. This chapter focuses on reducing such circuits into simpler, equivalent circuits. We continue to focus on relatively simple circuits for two reasons: (1) It gives us a chance to acquaint ourselves thoroughly with the laws underlying more sophisticated methods, and (2) it allows us to be introduced to some circuits that have important engineering applications.

The sources in the circuits discussed in this chapter are limited to voltage and current sources that generate either constant voltages or currents; that is, voltages and currents that are invariant with time. Constant sources are often called dc sources. The $d c$ stands for direct current, a description that has a historical basis but can seem misleading now. Historically, a direct current was defined as a current produced by a constant voltage. Therefore, a constant voltage became known as a direct current, or dc, voltage. The use of $d c$ for constant stuck, and the terms $d c$ current and $d c$ voltage are now universally accepted in science and engineering to mean constant current and constant voltage.

CHAPTER CONTENTS

3.1 Resistors in Series p. 58
3.2 Resistors in Parallel p. 59
3.3 The Voltage-Divider and Current-Divider Circuits p. 61
3.4 Voltage Division and Current Division p. 64
3.5 Measuring Voltage and Current p. 66
3.6 Measuring Resistance-The Wheatstone Bridge p. 69
3.7 Delta-to-Wye (Pi-to-Tee) Equivalent Circuits p. 71

CHAPTER OBJECTIVES

1 Be able to recognize resistors connected in series and in parallel and use the rules for combining series-connected resistors and parallel-connected resistors to yield equivalent resistance.
2 Know how to design simple voltage-divider and current-divider circuits.
3 Be able to use voltage division and current division appropriately to solve simple circuits.
4 Be able to determine the reading of an ammeter when added to a circuit to measure current; be able to determine the reading of a voltmeter when added to a circuit to measure voltage.
5 Understand how a Wheatstone bridge is used to measure resistance.
6 Know when and how to use delta-to-wye equivalent circuits to solve simple circuits.


Practical Perspective

Resistive Touch Screens

Some mobile phones and tablet computers use resistive touch screens, created by applying a transparent resistive material to the glass or acrylic screens. Two screens are typically used, separated by a transparent insulating layer. The resulting touch screen can be modeled by a grid of resistors in the $x$-direction and a grid of resistors in the $y$-direction, as shown in the figure on the right.

A separate electronic circuit applies a voltage drop across the grid in the $x$-direction, between the points $a$ and $b$ in the circuit, then removes that voltage and applies a voltage drop across the grid in the $y$-direction (between points $c$ and $d$ ),
and continues to repeat this process. When the screen is touched, the two resistive layers are pressed together, creating a voltage that is sensed in the $x$-grid and another voltage that is sensed in the $y$-grid. These two voltages precisely locate the point where the screen was touched.

How is the voltage created by touching the screen related to the position where the screen was touched? How are the properties of the grids used to calculate the touch position? We will answer these questions in the Practical Perspective at the end of this chapter. The circuit analysis required to answer these questions uses some circuit analysis tools developed next.
image_name:Denis Semenchenko/Shutterstock
description:The image depicts a smartphone with a touchscreen interface. The screen is predominantly blue, indicating it is likely in a standby mode or displaying a simple background. At the top of the screen, there are typical smartphone status indicators such as time (12:53 AM), battery level, and signal strength, suggesting the device is operational and connected to a network.

The bottom of the screen features a navigation bar with three icons: 'Applications,' 'Phone,' and 'Messaging.' These icons are standard on many smartphones, providing quick access to the main functionalities of the device.

The device itself is encased in a white frame, with a front-facing camera and possibly a speaker or sensor located at the top. The design is typical of modern smartphones, emphasizing a large touch-sensitive display that covers most of the front surface. This type of display uses a grid of sensors to detect touch, allowing the device to register where on the screen the user is interacting.

Overall, the image highlights the interface and basic structure of a touchscreen smartphone, focusing on its interactive and communicative features.


Denis Semenchenko/Shutterstock
image_name:Figure 3.1
description:
[
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': 'a', 'Nn': 'h'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'R4', 'type': 'Resistor', 'value': 'R4', 'ports': {'N1': 'd', 'N2': 'e'
'name': 'R5', 'type': 'Resistor', 'value': 'R5', 'ports': {'N1': 'e', 'N2': 'f'
'name': 'R6', 'type': 'Resistor', 'value': 'R6', 'ports': {'N1': 'f', 'N2': 'g'
'name': 'R7', 'type': 'Resistor', 'value': 'R7', 'ports': {'N1': 'g', 'N2': 'h'
]
extrainfo:The circuit is a combination of series and parallel resistors connected between nodes a, b, c, d, e, f, g, and h. It includes a voltage source Vs, and resistors R1 through R7. Currents i1 through i7 are indicated, showing the flow of current through the resistors.


Figure 3.1 $\triangle$ Resistors connected in series.
image_name:Figure 3.2 - Series resistors with a single unknown current i_{s}
description:
[
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': 'a', 'Nn': 'h'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'R4', 'type': 'Resistor', 'value': 'R4', 'ports': {'N1': 'd', 'N2': 'e'
'name': 'R5', 'type': 'Resistor', 'value': 'R5', 'ports': {'N1': 'e', 'N2': 'f'
'name': 'R6', 'type': 'Resistor', 'value': 'R6', 'ports': {'N1': 'f', 'N2': 'g'
'name': 'R7', 'type': 'Resistor', 'value': 'R7', 'ports': {'N1': 'g', 'N2': 'h'
]
extrainfo:The circuit is a series connection of resistors R1 to R7 and a voltage source Vs. The current i_s flows clockwise through the loop from node a to h.


Figure 3.2 - Series resistors with a single unknown current $i_{s}$.
image_name:Figure 3.3
description:
[
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': 'a', 'Nn': 'h'
'name': 'Req', 'type': 'Resistor', 'value': 'Req', 'ports': {'N1': 'a', 'N2': 'h'
]
extrainfo:The circuit consists of a voltage source Vs and an equivalent resistor Req in series. The current i_s flows clockwise from node a to h.


Figure 3.3 $\triangle$ A simplified version of the circuit shown in Fig. 3.2.

Combining resistors in series
image_name:Figure 3.4
description:The circuit diagram shows two representations of the same circuit: one with individual resistors R1 to R7 and a current source is, and the other with an equivalent resistor Req and a voltage source vs. The current is flows from node a to node h in both representations.
image_name:Figure 3.4
description:The circuit on the left is a network of resistors connected in series and parallel, forming a complex network between nodes a and h. The equivalent circuit on the right simplifies this network into a single equivalent resistor Req in series with the voltage source vs. The current is flows from node a to node h in both configurations.


Figure 3.4 $\triangle$ The black box equivalent of the circuit shown in Fig. 3.2.

## 3.1 Resistors in Series

In Chapter 2, we said that when just two elements connect at a single node, they are said to be in series. Series-connected circuit elements carry the same current. The resistors in the circuit shown in Fig. 3.1 are connected in series. We can show that these resistors carry the same current by applying Kirchhoff's current law to each node in the circuit. The series interconnection in Fig. 3.1 requires that

$$
\begin{equation*}
i_{s}=i_{1}=-i_{2}=i_{3}=i_{4}=-i_{5}=-i_{6}=i_{7}, \tag{3.1}
\end{equation*}
$$

which states that if we know any one of the seven currents, we know them all. Thus we can redraw Fig. 3.1 as shown in Fig. 3.2, retaining the identity of the single current $i_{s}$.

To find $i_{s}$, we apply Kirchhoff's voltage law around the single closed loop. Defining the voltage across each resistor as a drop in the direction of $i_{s}$ gives

$$
\begin{equation*}
-v_{s}+i_{s} R_{1}+i_{s} R_{2}+i_{s} R_{3}+i_{s} R_{4}+i_{s} R_{5}+i_{s} R_{6}+i_{s} R_{7}=0 \tag{3.2}
\end{equation*}
$$

or

$$
\begin{equation*}
v_{s}=i_{s}\left(R_{1}+R_{2}+R_{3}+R_{4}+R_{5}+R_{6}+R_{7}\right) \tag{3.3}
\end{equation*}
$$

The significance of Eq. 3.3 for calculating $i_{s}$ is that the seven resistors can be replaced by a single resistor whose numerical value is the sum of the individual resistors, that is,

$$
\begin{equation*}
R_{\mathrm{eq}}=R_{1}+R_{2}+R_{3}+R_{4}+R_{5}+R_{6}+R_{7} \tag{3.4}
\end{equation*}
$$

and

$$
\begin{equation*}
v_{s}=i_{s} R_{\mathrm{eq}} \tag{3.5}
\end{equation*}
$$

Thus we can redraw Fig. 3.2 as shown in Fig. 3.3.
In general, if $k$ resistors are connected in series, the equivalent single resistor has a resistance equal to the sum of the $k$ resistances, or

$$
\begin{equation*}
R_{\mathrm{eq}}=\sum_{i=1}^{k} R_{i}=R_{1}+R_{2}+\cdots+R_{k} \tag{3.6}
\end{equation*}
$$

Note that the resistance of the equivalent resistor is always larger than that of the largest resistor in the series connection.

Another way to think about this concept of an equivalent resistance is to visualize the string of resistors as being inside a black box. (An electrical engineer uses the term black box to imply an opaque container; that is, the contents are hidden from view. The engineer is then challenged to model the contents of the box by studying the relationship between the voltage and current at its terminals.) Determining whether the box contains $k$ resistors or a single equivalent resistor is impossible. Figure 3.4 illustrates this method of studying the circuit shown in Fig. 3.2.

## 3.2 Resistors in Parallel

When two elements connect at a single node pair, they are said to be in parallel. Parallel-connected circuit elements have the same voltage across their terminals. The circuit shown in Fig. 3.5 illustrates resistors connected in parallel. Don't make the mistake of assuming that two elements are parallel connected merely because they are lined up in parallel in a circuit diagram. The defining characteristic of parallel-connected elements is that they have the same voltage across their terminals. In Fig. 3.6, you can see that $R_{1}$ and $R_{3}$ are not parallel connected because, between their respective terminals, another resistor dissipates some of the voltage.

Resistors in parallel can be reduced to a single equivalent resistor using Kirchhoff's current law and Ohm's law, as we now demonstrate. In the circuit shown in Fig. 3.5, we let the currents $i_{1}, i_{2}, i_{3}$, and $i_{4}$ be the currents in the resistors $R_{1}$ through $R_{4}$, respectively. We also let the positive reference direction for each resistor current be down through the resistor, that is, from node a to node b. From Kirchhoff's current law,

$$
\begin{equation*}
i_{s}=i_{1}+i_{2}+i_{3}+i_{4} \tag{3.7}
\end{equation*}
$$

The parallel connection of the resistors means that the voltage across each resistor must be the same. Hence, from Ohm's law,

$$
\begin{equation*}
i_{1} R_{1}=i_{2} R_{2}=i_{3} R_{3}=i_{4} R_{4}=v_{s} \tag{3.8}
\end{equation*}
$$

Therefore,

$$
\begin{align*}
i_{1} & =\frac{v_{s}}{R_{1}} \\
i_{2} & =\frac{v_{s}}{R_{2}} \\
i_{3} & =\frac{v_{s}}{R_{3}}, \quad \text { and } \\
i_{4} & =\frac{v_{s}}{R_{4}} \tag{3.9}
\end{align*}
$$

Substituting Eq. 3.9 into Eq. 3.7 yields

$$
\begin{equation*}
i_{s}=v_{s}\left(\frac{1}{R_{1}}+\frac{1}{R_{2}}+\frac{1}{R_{3}}+\frac{1}{R_{4}}\right) \tag{3.10}
\end{equation*}
$$

from which

$$
\begin{equation*}
\frac{i_{s}}{v_{s}}=\frac{1}{R_{\mathrm{eq}}}=\frac{1}{R_{1}}+\frac{1}{R_{2}}+\frac{1}{R_{3}}+\frac{1}{R_{4}} \tag{3.11}
\end{equation*}
$$

Equation 3.11 is what we set out to show: that the four resistors in the circuit shown in Fig. 3.5 can be replaced by a single equivalent resistor. The circuit shown in Fig. 3.7 illustrates the substitution. For $k$ resistors connected in parallel, Eq. 3.11 becomes

$$
\begin{equation*}
\frac{1}{R_{\mathrm{eq}}}=\sum_{i=1}^{k} \frac{1}{R_{i}}=\frac{1}{R_{1}}+\frac{1}{R_{2}}+\cdots+\frac{1}{R_{k}} \tag{3.12}
\end{equation*}
$$

Note that the resistance of the equivalent resistor is always smaller than the resistance of the smallest resistor in the parallel connection. Sometimes,
image_name:Figure 3.5 A Resistors in parallel.
description:
[
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': 'a', 'Nn': 'b'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R4', 'type': 'Resistor', 'value': 'R4', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit consists of a voltage source Vs and four resistors R1, R2, R3, and R4 connected in parallel between nodes a and b.


Figure 3.5 A Resistors in parallel.
image_name:Figure 3.6 Nonparallel resistors
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'X1', 'N2': 'X2'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'X1', 'N2': 'X3'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'X3', 'N2': 'X2'
]
extrainfo:The circuit consists of three resistors R1, R2, and R3 connected in a triangle configuration. R1 is connected between nodes X1 and X2, R2 is connected between nodes X1 and X3, and R3 is connected between nodes X3 and X2. This forms a closed loop with nodes X1, X2, and X3.


Figure $3.6 \triangle$ Nonparallel resistors.
image_name:Figure 3.7
description:
[
'name': 'vs', 'type': 'VoltageSource', 'ports': {'Np': 'a', 'Nn': 'b'
'name': 'Req', 'type': 'Resistor', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit consists of a voltage source 'vs' and a resistor 'Req' connected in parallel between nodes 'a' and 'b'. A current 'is' flows from node 'a' through 'Req' towards node 'b'.


Figure 3.7 A Replacing the four parallel resistors shown in Fig. 3.5 with a single equivalent resistor.

Combining resistors in parallel
image_name:Figure 3.8
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit diagram shows two resistors, R1 and R2, connected in parallel between nodes 'a' and 'b'.


Figure 3.8 $\Delta$ Two resistors connected in parallel.
using conductance when dealing with resistors connected in parallel is more convenient. In that case, Eq. 3.12 becomes

$$
\begin{equation*}
G_{\mathrm{eq}}=\sum_{i=1}^{k} G_{i}=G_{1}+G_{2}+\cdots+G_{k} \tag{3.13}
\end{equation*}
$$

Many times only two resistors are connected in parallel. Figure 3.8 illustrates this special case. We calculate the equivalent resistance from Eq. 3.12:

$$
\begin{equation*}
\frac{1}{R_{\mathrm{eq}}}=\frac{1}{R_{1}}+\frac{1}{R_{2}}=\frac{R_{2}+R_{1}}{R_{1} R_{2}} \tag{3.14}
\end{equation*}
$$

or

$$
\begin{equation*}
R_{\mathrm{eq}}=\frac{R_{1} R_{2}}{R_{1}+R_{2}} \tag{3.15}
\end{equation*}
$$

Thus for just two resistors in parallel the equivalent resistance equals the product of the resistances divided by the sum of the resistances. Remember that you can only use this result in the special case of just two resistors in parallel. Example 3.1 illustrates the usefulness of these results.

#### Example 3.1 Applying Series-Parallel Simplification

Find $i_{s}, i_{1}$, and $i_{2}$ in the circuit shown in Fig. 3.9.

#### Solution

We begin by noting that the $3 \Omega$ resistor is in series with the $6 \Omega$ resistor. We therefore replace this series combination with a $9 \Omega$ resistor, reducing the circuit to the one shown in Fig. 3.10(a). We now can replace the parallel combination of the $9 \Omega$ and $18 \Omega$ resistors with a single resistance of $(18 \times 9) /(18+9)$, or $6 \Omega$. Figure 3.10(b) shows this further reduction of the circuit. The nodes x and y marked on all diagrams facilitate tracing through the reduction of the circuit.

From Fig. 3.10(b) you can verify that $i_{s}$ equals 120/10, or 12 A . Figure 3.11 shows the result at this point in the analysis. We added the voltage $v_{1}$ to help clarify the subsequent discussion. Using Ohm's law we compute the value of $v_{1}$ :

$$
\begin{equation*}
v_{1}=(12)(6)=72 \mathrm{~V} \tag{3.16}
\end{equation*}
$$

But $v_{1}$ is the voltage drop from node x to node y , so we can return to the circuit shown in Fig. 3.10(a) and again use Ohm's law to calculate $i_{1}$ and $i_{2}$. Thus,

$$
\begin{align*}
& i_{1}=\frac{v_{1}}{18}=\frac{72}{18}=4 \mathrm{~A}  \tag{3.17}\\
& i_{2}=\frac{v_{1}}{9}=\frac{72}{9}=8 \mathrm{~A} \tag{3.18}
\end{align*}
$$

We have found the three specified currents by using series-parallel reductions in combination with Ohm's law.
image_name:Figure 3.9
description:
[
'name': '120 V', 'type': 'VoltageSource', 'value': '120 V', 'ports': {'Np': 'b', 'Nn': 'y'
'name': '4 Ω', 'type': 'Resistor', 'value': '4 Ω', 'ports': {'N1': 'b', 'N2': 'x'
'name': '3 Ω', 'type': 'Resistor', 'value': '3 Ω', 'ports': {'N1': 'x', 'N2': 'a'
'name': '6 Ω', 'type': 'Resistor', 'value': '6 Ω', 'ports': {'N1': 'a', 'N2': 'y'
'name': '18 Ω', 'type': 'Resistor', 'value': '18 Ω', 'ports': {'N1': 'x', 'N2': 'y'
]
extrainfo:The circuit consists of a 120 V voltage source connected to a series of resistors forming a bridge circuit with nodes labeled a, b, x, and y. Currents i_s, i_1, and i_2 are flowing through the resistors.


Figure 3.9 $\triangle$ The circuit for Example 3.1.
image_name:Figure 3.10 (a)
description:
[
'name': '120 V', 'type': 'VoltageSource', 'value': '120 V', 'ports': {'Np': 'a', 'Nn': 'y'
'name': '4 Ω', 'type': 'Resistor', 'value': '4 Ω', 'ports': {'N1': 'a', 'N2': 'x'
'name': '18 Ω', 'type': 'Resistor', 'value': '18 Ω', 'ports': {'N1': 'x', 'N2': 'y'
'name': '9 Ω', 'type': 'Resistor', 'value': '9 Ω', 'ports': {'N1': 'x', 'N2': 'y'
]
extrainfo:The circuit is a bridge circuit with a 120 V voltage source and resistors forming a loop with nodes labeled a, x, and y. Currents i_s, i_1, and i_2 are flowing through the resistors.

image_name:Figure 3.10 (b)
description:
[
'name': '120 V', 'type': 'VoltageSource', 'value': '120 V', 'ports': {'Np': 'a', 'Nn': 'y'
'name': '4 Ω', 'type': 'Resistor', 'value': '4 Ω', 'ports': {'N1': 'a', 'N2': 'x'
'name': '6 Ω', 'type': 'Resistor', 'value': '6 Ω', 'ports': {'N1': 'x', 'N2': 'y'
]
extrainfo:The circuit is a series circuit with a 120 V voltage source and two resistors (4 Ω and 6 Ω) forming a loop with nodes labeled a, x, and y. The current i_s flows through the resistors from node a to node y.


Figure $3.10 \triangle$ A simplification of the circuit shown in Fig. 3.9.
image_name:Figure 3.11
description:
[
'name': '120V', 'type': 'VoltageSource', 'value': '120V', 'ports': {'Np': 'a', 'Nn': 'y'
'name': '4Ω', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'a', 'N2': 'x'
'name': '6Ω', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'x', 'N2': 'y'
]
extrainfo:The circuit is a series circuit with a 120 V voltage source and two resistors (4 Ω and 6 Ω) forming a loop with nodes labeled a, x, and y. The current i_s flows through the resistors from node a to node y.


Figure 3.11 \ The circuit of Fig. 3.10(b) showing the numerical value of $i_{s}$.

Before leaving Example 3.1, we suggest that you take the time to show that the solution satisfies Kirchhoff's current law at every node and Kirchhoff's voltage law around every closed path. (Note that there are three closed paths that can be tested.) Showing that the power delivered by the voltage source equals the total power dissipated in the resistors also is informative. (See Problems 3.1 and 3.2.)

ASSESSMENT PROBLEM

Objective 1-Be able to recognize resistors connected in series and in parallel
3.1 For the circuit shown, find (a) the voltage $v$, (b) the power delivered to the circuit by the current source, and (c) the power dissipated in the $10 \Omega$ resistor.

Answer: (a) 60 V ;
(b) 300 W ;
image_name:3.1
description:
[
'name': '5A', 'type': 'CurrentSource', 'value': '5A', 'ports': {'Np': 'GND', 'Nn': 'a'
'name': '7.2Ω', 'type': 'Resistor', 'value': '7.2Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '30Ω', 'type': 'Resistor', 'value': '30Ω', 'ports': {'N1': 'a', 'N2': 'GND'
'name': '64Ω', 'type': 'Resistor', 'value': '64Ω', 'ports': {'N1': 'b', 'N2': 'GND'
'name': '6Ω', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': '10Ω', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'c', 'N2': 'GND'
]
extrainfo:The circuit contains a current source and several resistors forming parallel and series combinations. The voltage across the current source is labeled as v.

(c) 57.6 W .

NOTE: Also try Chapter Problems 3.3-3.6.

## 3.3 The Voltage-Divider and Current-Divider Circuits

At times-especially in electronic circuits-developing more than one voltage level from a single voltage supply is necessary. One way of doing this is by using a voltage-divider circuit, such as the one in Fig. 3.12.

We analyze this circuit by directly applying Ohm's law and Kirchhoff's laws. To aid the analysis, we introduce the current $i$ as shown in Fig. 3.12(b). From Kirchhoff's current law, $R_{1}$ and $R_{2}$ carry the same current. Applying Kirchhoff's voltage law around the closed loop yields

$$
\begin{equation*}
v_{s}=i R_{1}+i R_{2}, \tag{3.19}
\end{equation*}
$$

or

$$
\begin{equation*}
i=\frac{v_{s}}{R_{1}+R_{2}} \tag{3.20}
\end{equation*}
$$

Now we can use Ohm's law to calculate $v_{1}$ and $v_{2}$ :

$$
\begin{align*}
& v_{1}=i R_{1}=v_{s} \frac{R_{1}}{R_{1}+R_{2}},  \tag{3.21}\\
& v_{2}=i R_{2}=v_{s} \frac{R_{2}}{R_{1}+R_{2}} . \tag{3.22}
\end{align*}
$$

Equations 3.21 and 3.22 show that $v_{1}$ and $v_{2}$ are fractions of $v_{s}$. Each fraction is the ratio of the resistance across which the divided voltage is defined to the sum of the two resistances. Because this ratio is always less than 1.0 , the divided voltages $v_{1}$ and $v_{2}$ are always less than the source voltage $v_{s}$.
image_name:(a)
description:
[
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': 'a', 'Nn': 'c'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'b', 'N2': 'c'
]
extrainfo:This is a simple voltage divider circuit with two resistors R1 and R2 connected in series across a voltage source Vs. The voltage across R1 is v1 and across R2 is v2, with v1 and v2 being fractions of the source voltage Vs.
image_name:(b)
description:
[
'name': 'vs', 'type': 'VoltageSource', 'value': 'vs', 'ports': {'Np': 'a', 'Nn': 'c'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'b', 'N2': 'c'
]
extrainfo:The circuit is a simple voltage divider consisting of a voltage source and two resistors. Node 'a' is connected to the positive terminal of the voltage source and one end of R1. Node 'b' is the junction between R1 and R2, where the divided voltage is measured. Node 'c' is connected to the negative terminal of the voltage source and one end of R2. The current 'i' flows from node 'a' through R1 to node 'b' and then through R2 to node 'c'.


Figure 3.12 A (a) A voltage-divider circuit and (b) the voltage-divider circuit with current $i$ indicated.
image_name:Figure 3.13
description:
[
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': 'Vin', 'Nn': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'Vin', 'N2': 'Vo'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'Vo', 'N2': 'GND'
'name': 'RL', 'type': 'Resistor', 'value': 'RL', 'ports': {'N1': 'Vo', 'N2': 'GND'
]
extrainfo:The circuit is a voltage divider with a load resistor RL connected across the output voltage Vo. The voltage source Vs provides the input voltage Vin, and the divided voltage Vo is measured across R2 and RL.


Figure 3.13 $\triangle$ A voltage divider connected to a load $R_{L}$.

If you desire a particular value of $v_{2}$, and $v_{s}$ is specified, an infinite number of combinations of $R_{1}$ and $R_{2}$ yield the proper ratio. For example, suppose that $v_{s}$ equals 15 V and $v_{2}$ is to be 5 V . Then $v_{2} / v_{s}=\frac{1}{3}$ and, from Eq.3.22, we find that this ratio is satisfied whenever $R_{2}=\frac{1}{2} R_{1}$. Other factors that may enter into the selection of $R_{1}$, and hence $R_{2}$, include the power losses that occur in dividing the source voltage and the effects of connecting the voltage-divider circuit to other circuit components.

Consider connecting a resistor $R_{L}$ in parallel with $R_{2}$, as shown in Fig. 3.13. The resistor $R_{L}$ acts as a load on the voltage-divider circuit. A load on any circuit consists of one or more circuit elements that draw power from the circuit. With the load $R_{L}$ connected, the expression for the output voltage becomes

$$
\begin{equation*}
v_{o}=\frac{R_{\mathrm{eq}}}{R_{1}+R_{\mathrm{eq}}} v_{s}, \tag{3.23}
\end{equation*}
$$

where

$$
\begin{equation*}
R_{\mathrm{eq}}=\frac{R_{2} R_{L}}{R_{2}+R_{L}} \tag{3.24}
\end{equation*}
$$

Substituting Eq. 3.24 into Eq. 3.23 yields

$$
\begin{equation*}
v_{o}=\frac{R_{2}}{R_{1}\left[1+\left(R_{2} / R_{L}\right)\right]+R_{2}} v_{s} \tag{3.25}
\end{equation*}
$$

Note that Eq. 3.25 reduces to Eq. 3.22 as $R_{L} \rightarrow \infty$, as it should. Equation 3.25 shows that, as long as $R_{L} \gg R_{2}$, the voltage ratio $v_{o} / v_{s}$ is essentially undisturbed by the addition of the load on the divider.

Another characteristic of the voltage-divider circuit of interest is the sensitivity of the divider to the tolerances of the resistors. By tolerance we mean a range of possible values. The resistances of commercially available resistors always vary within some percentage of their stated value. Example 3.2 illustrates the effect of resistor tolerances in a voltagedivider circuit.

#### Example 3.2 Analyzing the Voltage-Divider Circuit

The resistors used in the voltage-divider circuit shown in Fig. 3.14 have a tolerance of $\pm 10 \%$. Find the maximum and minimum value of $v_{o}$.
image_name:Figure 3.14
description:
[
'name': 'Vin', 'type': 'VoltageSource', 'value': '100V', 'ports': {'Np': 'Vin', 'Nn': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': '25kΩ', 'ports': {'N1': 'Vin', 'N2': 'Vo'
'name': 'R2', 'type': 'Resistor', 'value': '100kΩ', 'ports': {'N1': 'Vo', 'N2': 'GND'
]
extrainfo:The circuit is a voltage divider where R1 and R2 divide the input voltage Vin to produce an output voltage Vo. The resistors have a tolerance of ±10%.


Figure 3.14 A The circuit for Example 3.2.

#### Solution

From Eq. 3.22, the maximum value of $v_{o}$ occurs when $R_{2}$ is $10 \%$ high and $R_{1}$ is $10 \%$ low, and the minimum value of $v_{o}$ occurs when $R_{2}$ is $10 \%$ low and $R_{1}$ is 10\% high. Therefore

$$
\begin{aligned}
& v_{o}(\max )=\frac{(100)(110)}{110+22.5}=83.02 \mathrm{~V} \\
& v_{o}(\min )=\frac{(100)(90)}{90+27.5}=76.60 \mathrm{~V}
\end{aligned}
$$

Thus, in making the decision to use $10 \%$ resistors in this voltage divider, we recognize that the no-load output voltage will lie between 76.60 and 83.02 V .

The Current-Divider Circuit

The current-divider circuit shown in Fig. 3.15 consists of two resistors connected in parallel across a current source. The current divider is designed to divide the current $i_{s}$ between $R_{1}$ and $R_{2}$. We find the relationship between the current $i_{s}$ and the current in each resistor (that is, $i_{1}$ and $i_{2}$ ) by directly applying Ohm's law and Kirchhoff's current law. The voltage across the parallel resistors is

$$
\begin{equation*}
v=i_{1} R_{1}=i_{2} R_{2}=\frac{R_{1} R_{2}}{R_{1}+R_{2}} i_{s} \tag{3.26}
\end{equation*}
$$

From Eq. 3.26,

$$
\begin{align*}
& i_{1}=\frac{R_{2}}{R_{1}+R_{2}} i_{s}  \tag{3.27}\\
& i_{2}=\frac{R_{1}}{R_{1}+R_{2}} i_{s} \tag{3.28}
\end{align*}
$$

Equations 3.27 and 3.28 show that the current divides between two resistors in parallel such that the current in one resistor equals the current entering the parallel pair multiplied by the other resistance and divided by the sum of the resistors. Example 3.3 illustrates the use of the currentdivider equation.

#### Example 3.3 Analyzing a Current-Divider Circuit

Find the power dissipated in the $6 \Omega$ resistor shown in Fig. 3.16.

#### Solution

First, we must find the current in the resistor by simplifying the circuit with series-parallel reductions. Thus, the circuit shown in Fig. 3.16 reduces to the one shown in Fig. 3.17. We find the current $i_{o}$ by using the formula for current division:

$$
i_{o}=\frac{16}{16+4}(10)=8 \mathrm{~A}
$$

Note that $i_{o}$ is the current in the $1.6 \Omega$ resistor in Fig. 3.16. We now can further divide $i_{o}$ between the $6 \Omega$ and $4 \Omega$ resistors. The current in the $6 \Omega$ resistor is

$$
i_{6}=\frac{4}{6+4}(8)=3.2 \mathrm{~A}
$$

image_name:Figure 3.16
description:
[
'name': '10A', 'type': 'CurrentSource', 'value': '10A', 'ports': {'Np': 'a', 'Nn': 'b'
'name': 'R1', 'type': 'Resistor', 'value': '1.6Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'R2', 'type': 'Resistor', 'value': '16Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R3', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'c', 'N2': 'b'
'name': 'R4', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'c', 'N2': 'b'
]
extrainfo:The circuit consists of a current source and four resistors. The current source provides 10A between nodes a and b. The resistors are connected in a combination of series and parallel configurations. The 1.6Ω resistor is in series with the parallel combination of the 4Ω and 6Ω resistors. The 16Ω resistor is in parallel with the entire series-parallel combination.


Figure 3.16 $\boldsymbol{\Delta}$ The circuit for Example 3.3.
image_name:Figure 3.17
description:
[
'name': '10 A', 'type': 'CurrentSource', 'value': '10 A', 'ports': {'Np': 'GND', 'Nn': 'a'
'name': '16 Ω', 'type': 'Resistor', 'value': '16 Ω', 'ports': {'N1': 'a', 'N2': 'GND'
'name': '4 Ω', 'type': 'Resistor', 'value': '4 Ω', 'ports': {'N1': 'a', 'N2': 'GND'
]
extrainfo:The circuit consists of a 10 A current source connected between node a and GND, with two resistors (16 Ω and 4 Ω) connected in parallel between node a and GND. The current source is providing current into the parallel resistor network.


Figure 3.17 $\triangle$ A simplification of the circuit shown in Fig. 3.16.
and the power dissipated in the $6 \Omega$ resistor is $p=(3.2)^{2}(6)=61.44 \mathrm{~W}$.

ASSESSMENT PROBLEMS

Objective 2—Know how to design simple voltage-divider and current-divider circuits
3.2 a) Find the no-load value of $v_{o}$ in the circuit shown.
b) Find $v_{o}$ when $R_{L}$ is $150 \mathrm{k} \Omega$.
c) How much power is dissipated in the $25 \mathrm{k} \Omega$ resistor if the load terminals are accidentally short-circuited?
d) What is the maximum power dissipated in the $75 \mathrm{k} \Omega$ resistor?
image_name:3.2
description:
[
'name': 'Vin', 'type': 'VoltageSource', 'value': '200V', 'ports': {'Np': 'Vin', 'Nn': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': '25kΩ', 'ports': {'N1': 'Vin', 'N2': 'Vo'
'name': 'R2', 'type': 'Resistor', 'value': '75kΩ', 'ports': {'N1': 'Vo', 'N2': 'GND'
'name': 'RL', 'type': 'Resistor', 'value': 'RL', 'ports': {'N1': 'Vo', 'N2': 'GND'
]
extrainfo:The circuit is a voltage divider with a load resistor RL connected in parallel to the 75kΩ resistor. The input voltage is 200V.


Answer: (a) 150 V ;
(b) 133.33 V ;
(c) 1.6 W ;
(d) 0.3 W .

NOTE: Also try Chapter Problems 3.12, 3.14, and 3.16.
3.3 a) Find the value of $R$ that will cause 4 A of current to flow through the $80 \Omega$ resistor in the circuit shown.
b) How much power will the resistor $R$ from part (a) need to dissipate?
c) How much power will the current source generate for the value of $R$ from part (a)?
image_name:3.3
description:
[
'name': '20A', 'type': 'CurrentSource', 'value': '20A', 'ports': {'Np': 'GND', 'Nn': 'a'
'name': '60Ω', 'type': 'Resistor', 'value': '60Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': '40Ω', 'type': 'Resistor', 'value': '40Ω', 'ports': {'N1': 'c', 'N2': 'b'
'name': '80Ω', 'type': 'Resistor', 'value': '80Ω', 'ports': {'N1': 'b', 'N2': 'GND'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'c', 'N2': 'GND'
]
extrainfo:The circuit contains a current source and a set of resistors forming a parallel and series network. Node 'c' is a common node for the 60Ω, 40Ω, and R resistors.


Answer: (a) $30 \Omega$;
(b) 7680 W ;
(c) $33,600 \mathrm{~W}$.

## 3.4 Voltage Division and Current Division

image_name:Figure 3.18
description:The circuit is a series connection of resistors R1, R2, ..., Rj, Rn-1, and Rn. It demonstrates voltage division across the resistors with a current 'i' flowing through them. The voltage across Rj is marked as vj.


Figure 3.18 $\boldsymbol{\Delta}$ Circuit used to illustrate voltage division.

We can now generalize the results from analyzing the voltage divider circuit in Fig. 3.12 and the current-divider circuit in Fig. 3.15. The generalizations will yield two additional and very useful circuit analysis techniques known as voltage division and current division. Consider the circuit shown in Fig. 3.18.

The box on the left can contain a single voltage source or any other combination of basic circuit elements that results in the voltage $v$ shown in the figure. To the right of the box are $n$ resistors connected in series. We are interested in finding the voltage drop $v_{j}$ across an arbitrary resistor $R_{j}$ in terms of the voltage $v$. We start by using Ohm's law to calculate $i$, the current through all of the resistors in series, in terms of the current $v$ and the $n$ resistors:

$$
\begin{equation*}
i=\frac{v}{R_{1}+R_{2}+\cdots+R_{n}}=\frac{v}{R_{\mathrm{eq}}} \tag{3.29}
\end{equation*}
$$

The equivalent resistance, $R_{\text {eq }}$, is the sum of the $n$ resistor values because the resistors are in series, as shown in Eq. 3.6. We apply Ohm's
law a second time to calculate the voltage drop $v_{j}$ across the resistor $R_{j}$, using the current $i$ calculated in Eq. 3.29:

$$
\begin{equation*}
v_{j}=i R_{j}=\frac{R_{j}}{R_{\mathrm{eq}}} v \tag{3.30}
\end{equation*}
$$

Note that we used Eq. 3.29 to obtain the right-hand side of Eq. 3.30. Equation 3.30 is the voltage division equation. It says that the voltage drop $v_{j}$ across a single resistor $R_{j}$ from a collection of series-connected resistors is proportional to the total voltage drop $v$ across the set of seriesconnected resistors. The constant of proportionality is the ratio of the single resistance to the equivalent resistance of the series connected set of resistors, or $R_{j} / R_{\text {eq }}$.

Now consider the circuit shown in Fig. 3.19. The box on the left can contain a single current source or any other combination of basic circuit elements that results in the current $i$ shown in the figure. To the right of the box are $n$ resistors connected in parallel. We are interested in finding the current $i_{j}$ through an arbitrary resistor $R_{j}$ in terms of the current $i$. We start by using Ohm's law to calculate $v$, the voltage drop across each of the resistors in parallel, in terms of the current $i$ and the $n$ resistors:

$$
\begin{equation*}
v=i\left(R_{1}\left\|R_{2}\right\| \ldots \| R_{n}\right)=i R_{\mathrm{eq}} \tag{3.31}
\end{equation*}
$$

The equivalent resistance of $n$ resistors in parallel, $R_{\text {eq }}$, can be calculated using Eq. 3.12. We apply Ohm's law a second time to calculate the current $i_{j}$ through the resistor $R_{j}$, using the voltage $v$ calculated in Eq. 3.31:

$$
\begin{equation*}
i_{j}=\frac{v}{R_{j}}=\frac{R_{\mathrm{eq}}}{R_{j}} i \tag{3.32}
\end{equation*}
$$

Note that we used Eq. 3.31 to obtain the right-hand side of Eq. 3.32. Equation 3.32 is the current division equation. It says that the current $i$ through a single resistor $R_{j}$ from a collection of parallel-connected resistors is proportional to the total current $i$ supplied to the set of parallelconnected resistors. The constant of proportionality is the ratio of the equivalent resistance of the parallel-connected set of resistors to the single resistance, or $R_{\mathrm{eq}} / R_{j}$. Note that the constant of proportionality in the current division equation is the inverse of the constant of proportionality in the voltage division equation!

Example 3.4 uses voltage division and current division to solve for voltages and currents in a circuit.
image_name:Figure 3.19
description:The circuit consists of a set of parallel-connected resistors (R1, R2, Rj, Rn-1, Rn) connected to a voltage source. The current i is supplied to the parallel branches, with current division occurring among the resistors.


Figure 3.19 $\boldsymbol{\Delta}$ Circuit used to illustrate current division.

Voltage-division equation

### Voltage-division equation

#### Example 3.4 Using Voltage Division and Current Division to Solve a Circuit

Use current division to find the current $i_{o}$ and use voltage division to find the voltage $v_{o}$ for the circuit in Fig. 3.20.

#### Solution

We can use Eq. 3.32 if we can find the equivalent resistance of the four parallel branches containing resistors. Symbolically,

$$
\begin{aligned}
R_{\mathrm{eq}} & =(36+44)\|10\|(40+10+30) \| 24 \\
& =80\|10\| 80 \| 24=\frac{1}{\frac{1}{80}+\frac{1}{10}+\frac{1}{80}+\frac{1}{24}}=6 \Omega
\end{aligned}
$$

Applying Eq. 3.32,

$$
i_{o}=\frac{6}{24}(8 \mathrm{~A})=2 \mathrm{~A}
$$

We can use Ohm's law to find the voltage drop across the $24 \Omega$ resistor:

$$
v=(24)(2)=48 \mathrm{~V}
$$

image_name:Figure 3.20 Δ
description:
[
'name': '8A', 'type': 'CurrentSource', 'value': '8A', 'ports': {'Np': 'e', 'Nn': 'a'
'name': '36Ω', 'type': 'Resistor', 'value': '36Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': '44Ω', 'type': 'Resistor', 'value': '44Ω', 'ports': {'N1': 'b', 'N2': 'e'
'name': '10Ω', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'a', 'N2': 'e'
'name': '40Ω', 'type': 'Resistor', 'value': '40Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': '10Ω', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': '30Ω', 'type': 'Resistor', 'value': '30Ω', 'ports': {'N1': 'd', 'N2': 'e'
'name': '24Ω', 'type': 'Resistor', 'value': '24Ω', 'ports': {'N1': 'a', 'N2': 'e'
]
extrainfo:The circuit consists of a parallel network of resistors connected to a current source. The equivalent resistance is calculated as 6Ω. The current io through the 24Ω resistor is 2A, and the voltage drop across it is 48V. This voltage also appears across the series combination of 40Ω, 10Ω, and 30Ω resistors.


Figure $3.20 \boldsymbol{\Delta}$ The circuit for Example 3.4.

This is also the voltage drop across the branch containing the $40 \Omega$, the $10 \Omega$, and the $30 \Omega$ resistors in series. We can then use voltage division to determine the voltage drop $v_{o}$ across the $30 \Omega$ resistor given that we know the voltage drop across the seriesconnected resistors, using Eq. 3.30. To do this, we recognize that the equivalent resistance of the series-connected resistors is $40+10+30=80 \Omega$ :

$$
v_{o}=\frac{30}{80}(48 \mathrm{~V})=18 \mathrm{~V}
$$

ASSESSMENT PROBLEM

Objective 3-Be able to use voltage and current division to solve simple circuits

3.4 a) Use voltage division to determine the voltage $v_{o}$ across the $40 \Omega$ resistor in the circuit shown.
b) Use $v_{o}$ from part (a) to determine the current through the $40 \Omega$ resistor, and use this current and current division to calculate the current in the $30 \Omega$ resistor.
c) How much power is absorbed by the $50 \Omega$ resistor?
image_name:Circuit shown
description:
[
'name': 'V1', 'type': 'VoltageSource', 'value': '60V', 'ports': {'Np': 'a', 'Nn': 'd'
'name': 'R1', 'type': 'Resistor', 'value': '40Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': '70Ω', 'ports': {'N1': 'd', 'N2': 'e'
'name': 'R3', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'b', 'N2': 'e'
'name': 'R4', 'type': 'Resistor', 'value': '30Ω', 'ports': {'N1': 'b', 'N2': 'e'
'name': 'R5', 'type': 'Resistor', 'value': '50Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R6', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'c', 'N2': 'e'
]
extrainfo:The circuit is a combination of series and parallel resistors powered by a 60V voltage source. The voltage across the 40Ω resistor is labeled as vo.


Answer: (a) 20 V ;
(b) 166.67 mA ;
(c) 347.22 mW .

NOTE: Also try Chapter Problems 3.25 and 3.26.

## 3.5 Measuring Voltage and Current

When working with actual circuits, you will often need to measure voltages and currents. We will spend some time discussing several measuring devices here and in the next section, because they are relatively simple to analyze and offer practical examples of the current- and voltage-divider configurations we have just studied.

An ammeter is an instrument designed to measure current; it is placed in series with the circuit element whose current is being measured. A voltmeter is an instrument designed to measure voltage; it is placed in parallel with the element whose voltage is being measured. An ideal ammeter or voltmeter has no effect on the circuit variable it is designed to measure.

That is, an ideal ammeter has an equivalent resistance of $0 \Omega$ and functions as a short circuit in series with the element whose current is being measured. An ideal voltmeter has an infinite equivalent resistance and thus functions as an open circuit in parallel with the element whose voltage is being measured. The configurations for an ammeter used to measure the current in $R_{1}$ and for a voltmeter used to measure the voltage in $R_{2}$ are depicted in Fig. 3.21. The ideal models for these meters in the same circuit are shown in Fig. 3.22.

There are two broad categories of meters used to measure continuous voltages and currents: digital meters and analog meters. Digital meters measure the continuous voltage or current signal at discrete points in time, called the sampling times. The signal is thus converted from an analog signal, which is continuous in time, to a digital signal, which exists only at discrete instants in time. A more detailed explanation of the workings of digital meters is beyond the scope of this text and course. However, you are likely to see and use digital meters in lab settings because they offer several advantages over analog meters. They introduce less resistance into the circuit to which they are connected, they are easier to connect, and the precision of the measurement is greater due to the nature of the readout mechanism.

Analog meters are based on the d'Arsonval meter movement which implements the readout mechanism. A d'Arsonval meter movement consists of a movable coil placed in the field of a permanent magnet. When current flows in the coil, it creates a torque on the coil, causing it to rotate and move a pointer across a calibrated scale. By design, the deflection of the pointer is directly proportional to the current in the movable coil. The coil is characterized by both a voltage rating and a current rating. For example, one commercially available meter movement is rated at 50 mV and 1 mA . This means that when the coil is carrying 1 mA , the voltage drop across the coil is 50 mV and the pointer is deflected to its full-scale position. A schematic illustration of a d'Arsonval meter movement is shown in Fig. 3.23.

An analog ammeter consists of a d'Arsonval movement in parallel with a resistor, as shown in Fig. 3.24. The purpose of the parallel resistor is to limit the amount of current in the movement's coil by shunting some of it through $R_{A}$. An analog voltmeter consists of a d'Arsonval movement in series with a resistor, as shown in Fig. 3.25. Here, the resistor is used to limit the voltage drop across the meter's coil. In both meters, the added resistor determines the full-scale reading of the meter movement.

From these descriptions we see that an actual meter is nonideal; both the added resistor and the meter movement introduce resistance in the circuit to which the meter is attached. In fact, any instrument used to make physical measurements extracts energy from the system while making measurements. The more energy extracted by the instruments, the more severely the measurement is disturbed. A real ammeter has an equivalent resistance that is not zero, and it thus effectively adds resistance to the circuit in series with the element whose current the ammeter is reading. A real voltmeter has an equivalent resistance that is not infinite, so it effectively adds resistance to the circuit in parallel with the element whose voltage is being read.

How much these meters disturb the circuit being measured depends on the effective resistance of the meters compared with the resistance in the circuit. For example, using the rule of $1 / 10$ th, the effective resistance of an ammeter should be no more than $1 / 10$ th of the value of the smallest resistance in the circuit to be sure that the current being measured is nearly the same with or without the ammeter. But in an analog meter, the value of resistance is determined by the desired full-scale reading we wish to make, and it cannot be arbitrarily selected. The following examples illustrate the calculations involved in determining the resistance needed in an analog ammeter or voltmeter. The examples also consider the resulting effective resistance of the meter when it is inserted in a circuit.
image_name:Figure 3.21
description:
[
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': '1', 'Nn': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': '1', 'N2': '2'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': '2', 'N2': 'GND'
]
extrainfo:An ammeter is connected in series with R1 to measure the current, and a voltmeter is connected in parallel with R2 to measure the voltage across it.


Figure 3.21 $\triangle$ An ammeter connected to measure the current in $R_{1}$, and a voltmeter connected to measure the voltage across $R_{2}$.



Figure $3.22 \triangle$ A short-circuit model for the ideal ammeter, and an open-circuit model for the ideal voltmeter.
image_name:d'Arsonval meter movement
description:The image depicts a schematic diagram of a d'Arsonval meter movement, a fundamental component used in analog measuring instruments such as ammeters and voltmeters. The primary components visible in the diagram include:

1. **Permanent Magnet**: This is shown as a large, curved structure that creates a magnetic field. It is crucial for the operation of the meter by interacting with the moveable coil.

2. **Moveable Coil**: Positioned within the magnetic field of the permanent magnet, this coil is depicted as a wound wire around a cylindrical form. It is free to rotate and is responsible for moving the pointer when current flows through it.

3. **Pointer**: Attached to the moveable coil, the pointer moves across a scale to indicate the measurement. It is shown as a thin, elongated arrow pointing towards the scale.

4. **Scale**: A curved, marked surface over which the pointer moves, allowing the user to read the measurement. The scale is depicted with divisions or markings for measurement reference.

5. **Restoring Spring**: This component is connected to the moveable coil and is responsible for returning the pointer to the zero position when no current flows through the coil. It provides the necessary counter-torque to balance the coil’s movement.

6. **Magnetic Steel Core**: Located at the center of the moveable coil, this core enhances the magnetic field and improves the efficiency of the meter.

The diagram clearly labels each component, aiding in understanding the interactions and mechanical structure of the d'Arsonval meter movement. The flow of current through the coil generates a magnetic force that interacts with the permanent magnet, causing the coil (and thus the pointer) to rotate. The degree of rotation is proportional to the current, allowing for precise measurement.


Figure 3.23 $\triangle$ A schematic diagram of a d'Arsonval meter movement.
image_name:Figure 3.24 Δ Adc ammeter circuit
description:
[
'name': 'RA', 'type': 'Resistor', 'ports': {'N1': 'N1', 'N2': 'N2'
]
extrainfo:The circuit is an ammeter configuration using a d'Arsonval movement with a parallel resistor RA. The ammeter terminals are connected across the circuit.


Figure $3.24 \triangle \mathrm{Adc}$ ammeter circuit.
image_name:Figure 3.25 Δ A dc voltmeter circuit
description:
[
'name': 'Rv', 'type': 'Resistor', 'value': 'Rv', 'ports': {'N1': 'N1', 'N2': 'N2'
]
extrainfo:The circuit is a voltmeter configuration using a d'Arsonval movement with a series resistor Rv. The voltmeter terminals are connected across the circuit.


Figure $3.25 \Delta \mathrm{~A}$ dc voltmeter circuit.

#### Example 3.5 Using a d'Arsonval Ammeter

a) A $50 \mathrm{mV}, 1 \mathrm{~mA}$ d'Arsonval movement is to be used in an ammeter with a full-scale reading of 10 mA . Determine $R_{A}$.
b) Repeat (a) for a full-scale reading of 1 A .
c) How much resistance is added to the circuit when the 10 mA ammeter is inserted to measure current?
d) Repeat (c) for the 1 A ammeter.

#### Solution

a) From the statement of the problem, we know that when the current at the terminals of the ammeter is $10 \mathrm{~mA}, 1 \mathrm{~mA}$ is flowing through the meter coil, which means that 9 mA must be diverted through $R_{A}$. We also know that when the movement carries 1 mA , the drop across its terminals is 50 mV . Ohm's law requires that

$$
9 \times 10^{-3} R_{A}=50 \times 10^{-3},
$$

or

$$
R_{A}=50 / 9=5.555 \Omega
$$

b) When the full-scale deflection of the ammeter is $1 \mathrm{~A}, R_{A}$ must carry 999 mA when the movement carries 1 mA . In this case, then,

$$
999 \times 10^{-3} R_{A}=50 \times 10^{-3},
$$

or

$$
R_{A}=50 / 999 \approx 50.05 \mathrm{~m} \Omega
$$

c) Let $R_{m}$ represent the equivalent resistance of the ammeter. For the 10 mA ammeter,

$$
R_{m}=\frac{50 \mathrm{mV}}{10 \mathrm{~mA}}=5 \Omega
$$

or, alternatively,

$$
R_{m}=\frac{(50)(50 / 9)}{50+(50 / 9)}=5 \Omega
$$

d) For the 1 A ammeter

$$
R_{m}=\frac{50 \mathrm{mV}}{1 \mathrm{~A}}=0.050 \Omega
$$

or, alternatively,

$$
R_{m}=\frac{(50)(50 / 999)}{50+(50 / 999)}=0.050 \Omega
$$

#### Example 3.6 Using a d'Arsonval Voltmeter

a) A $50 \mathrm{mV}, 1 \mathrm{~mA}$ d'Arsonval movement is to be used in a voltmeter in which the full-scale reading is 150 V . Determine $R_{v}$.
b) Repeat (a) for a full-scale reading of 5 V .
c) How much resistance does the 150 V meter insert into the circuit?
d) Repeat (c) for the 5 V meter.

#### Solution

a) Full-scale deflection requires 50 mV across the meter movement, and the movement has a resistance of $50 \Omega$. Therefore we apply Eq. 3.22 with $R_{1}=R_{v}, R_{2}=50, v_{s}=150$, and $v_{2}=50 \mathrm{mV}$ :

$$
50 \times 10^{-3}=\frac{50}{R_{v}+50}(150)
$$

Solving for $R_{v}$ gives

$$
R_{v}=149,950 \Omega
$$

b) For a full-scale reading of 5 V ,

$$
50 \times 10^{-3}=\frac{50}{R_{v}+50}(5)
$$

or

$$
R_{v}=4950 \Omega
$$

c) If we let $R_{m}$ represent the equivalent resistance of the meter,

$$
R_{m}=\frac{150 \mathrm{~V}}{10^{-3} \mathrm{~A}}=150,000 \Omega
$$

or, alternatively,

$$
R_{m}=149,950+50=150,000 \Omega
$$

d) Then,

$$
R_{m}=\frac{5 \mathrm{~V}}{10^{-3} \mathrm{~A}}=5000 \Omega
$$

or, alternatively,

$$
R_{m}=4950+50=5000 \Omega .
$$

ASSESSMENT PROBLEMS

Objective 4-Be able to determine the reading of ammeters and voltmeters

3.5 a) Find the current in the circuit shown.
b) If the ammeter in Example 3.5(a) is used to measure the current, what will it read?
image_name:circuit shown
description:
[
'name': '1 V', 'type': 'VoltageSource', 'value': '1 V', 'ports': {'Np': 'a', 'Nn': 'b'
'name': '100 Ω', 'type': 'Resistor', 'value': '100 Ω', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit consists of a 1 V voltage source and a 100 Ω resistor connected in series. The current flows from the positive terminal of the voltage source through the resistor back to the negative terminal of the voltage source.


Answer:
(a) 10 mA ;
(b) 9.524 mA .

NOTE: Also try Chapter Problems 3.34 and 3.37.
3.6 a) Find the voltage $v$ across the $75 \mathrm{k} \Omega$ resistor in the circuit shown.
b) If the 150 V voltmeter of Example 3.6(a) is used to measure the voltage, what will be the reading?
image_name:Figure 3.6
description:
[
'name': 'VoltageSource1', 'type': 'VoltageSource', 'value': '60V', 'ports': {'Np': 'a', 'Nn': 'b'
'name': 'Resistor1', 'type': 'Resistor', 'value': '15kΩ', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'Resistor2', 'type': 'Resistor', 'value': '75kΩ', 'ports': {'N1': 'c', 'N2': 'b'
]
extrainfo:The circuit is a simple series circuit with a 60V voltage source connected to a 15kΩ resistor and a 75kΩ resistor. The voltage across the 75kΩ resistor is labeled as v.


Answer: (a) 50 V ;
(b) 46.15 V .

## 3.6 Measuring ResistanceThe Wheatstone Bridge

Many different circuit configurations are used to measure resistance. Here we will focus on just one, the Wheatstone bridge. The Wheatstone bridge circuit is used to precisely measure resistances of medium values, that is, in the range of $1 \Omega$ to $1 \mathrm{M} \Omega$. In commercial models of the Wheatstone bridge, accuracies on the order of $\pm 0.1 \%$ are possible. The bridge circuit consists of four resistors, a dc voltage source, and a detector. The resistance of one of the four resistors can be varied, which is indicated in Fig. 3.26 by the arrow through $R_{3}$. The dc voltage source is usually a battery, which is indicated by the battery symbol for the voltage source $v$ in Fig. 3.26. The detector is generally a d'Arsonval movement in the microamp range and is called a galvanometer. Figure 3.26 shows the circuit arrangement of the resistances, battery, and detector where $R_{1}, R_{2}$, and $R_{3}$ are known resistors and $R_{x}$ is the unknown resistor.

To find the value of $R_{x}$, we adjust the variable resistor $R_{3}$ until there is no current in the galvanometer. We then calculate the unknown resistor from the simple expression

$$
\begin{equation*}
R_{x}=\frac{R_{2}}{R_{1}} R_{3} \tag{3.33}
\end{equation*}
$$

The derivation of Eq. 3.33 follows directly from the application of Kirchhoff's laws to the bridge circuit. We redraw the bridge circuit as Fig. 3.27 to show the currents appropriate to the derivation of Eq. 3.33. When $i_{g}$ is zero, that is, when the bridge is balanced, Kirchhoff's current law requires that

$$
\begin{align*}
i_{1} & =i_{3}  \tag{3.34}\\
i_{2} & =i_{x} \tag{3.35}
\end{align*}
$$

image_name:Figure 3.26 The Wheatstone bridge circuit
description:
[
'name': 'V', 'type': 'VoltageSource', 'value': 'V', 'ports': {'Np': 'Vin', 'Nn': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'Vin', 'N2': 'a'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'Vin', 'N2': 'b'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'a', 'N2': 'GND'
'name': 'Rx', 'type': 'Resistor', 'value': 'Rx', 'ports': {'N1': 'b', 'N2': 'GND'
]
extrainfo:The circuit is a Wheatstone bridge configuration used for precise measurement of resistance. It is balanced when the voltage across the detector is zero, meaning no current flows through it.


Figure $3.26 \triangle$ The Wheatstone bridge circuit.
image_name:Figure 3.27
description:
[
'name': 'V', 'type': 'VoltageSource', 'value': 'v', 'ports': {'Np': 'Vin', 'Nn': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'Vin', 'N2': 'a'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'Vin', 'N2': 'b'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'a', 'N2': 'GND'
'name': 'Rx', 'type': 'Resistor', 'value': 'Rx', 'ports': {'N1': 'b', 'N2': 'GND'
]
extrainfo:The circuit is a Wheatstone bridge configuration used for precise measurement of resistance. It is balanced when the voltage across the detector is zero, meaning no current flows through it.


Figure $3.27 \triangle \mathrm{~A}$ balanced Wheatstone bridge $\left(i_{g}=0\right)$.

Now, because $i_{g}$ is zero, there is no voltage drop across the detector, and therefore points a and b are at the same potential. Thus when the bridge is balanced, Kirchhoff's voltage law requires that

$$
\begin{align*}
& i_{3} R_{3}=i_{x} R_{x}  \tag{3.36}\\
& i_{1} R_{1}=i_{2} R_{2} \tag{3.37}
\end{align*}
$$

Combining Eqs. 3.34 and 3.35 with Eq. 3.36 gives

$$
\begin{equation*}
i_{1} R_{3}=i_{2} R_{x} \tag{3.38}
\end{equation*}
$$

We obtain Eq. 3.33 by first dividing Eq. 3.38 by Eq. 3.37 and then solving the resulting expression for $R_{x}$ :

$$
\begin{equation*}
\frac{R_{3}}{R_{1}}=\frac{R_{x}}{R_{2}} \tag{3.39}
\end{equation*}
$$

from which

$$
\begin{equation*}
R_{x}=\frac{R_{2}}{R_{1}} R_{3} \tag{3.40}
\end{equation*}
$$

Now that we have verified the validity of Eq. 3.33, several comments about the result are in order. First, note that if the ratio $R_{2} / R_{1}$ is unity, the unknown resistor $R_{x}$ equals $R_{3}$. In this case, the bridge resistor $R_{3}$ must vary over a range that includes the value $R_{x}$. For example, if the unknown resistance were $1000 \Omega$ and $R_{3}$ could be varied from 0 to $100 \Omega$, the bridge could never be balanced. Thus to cover a wide range of unknown resistors, we must be able to vary the ratio $R_{2} / R_{1}$. In a commercial Wheatstone bridge, $R_{1}$ and $R_{2}$ consist of decimal values of resistances that can be switched into the bridge circuit. Normally, the decimal values are $1,10,100$, and $1000 \Omega$ so that the ratio $R_{2} / R_{1}$ can be varied from 0.001 to 1000 in decimal steps. The variable resistor $R_{3}$ is usually adjustable in integral values of resistance from 1 to $11,000 \Omega$.

Although Eq. 3.33 implies that $R_{x}$ can vary from zero to infinity, the practical range of $R_{x}$ is approximately $1 \Omega$ to $1 \mathrm{M} \Omega$. Lower resistances are difficult to measure on a standard Wheatstone bridge because of thermoelectric voltages generated at the junctions of dissimilar metals and because of thermal heating effects - that is, $i^{2} R$ effects. Higher resistances are difficult to measure accurately because of leakage currents. In other words, if $R_{x}$ is large, the current leakage in the electrical insulation may be comparable to the current in the branches of the bridge circuit.

ASSESSMENT PROBLEM

Objective 5-Understand how a Wheatstone bridge is used to measure resistance

3.7 The bridge circuit shown is balanced when $R_{1}=100 \Omega, R_{2}=1000 \Omega$, and $R_{3}=150 \Omega$. The bridge is energized from a 5 V dc source.
a) What is the value of $R_{x}$ ?
b) Suppose each bridge resistor is capable of dissipating 250 mW . Can the bridge be left in the balanced state without exceeding the power-dissipating capacity of the resistors, thereby damaging the bridge?
image_name:Wheatstone bridge circuit
description:
[
'name': 'V', 'type': 'VoltageSource', 'value': 'V', 'ports': {'Np': 'Vin', 'Nn': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'Vin', 'N2': 'a'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'Vin', 'N2': 'b'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'a', 'N2': 'GND'
'name': 'Rx', 'type': 'Resistor', 'value': 'Rx', 'ports': {'N1': 'b', 'N2': 'GND'
]
extrainfo:The Wheatstone bridge is balanced with R1 = 100 Ω, R2 = 1000 Ω, R3 = 150 Ω, and Rx = 1500 Ω. The bridge is powered by a 5 V DC source. All resistors can dissipate up to 250 mW without damage.


Answer: (a) $1500 \Omega$;
(b) yes.

NOTE: Also try Chapter Problem 3.51.

## 3.7 Delta-to-Wye (Pi-to-Tee) Equivalent Circuits

The bridge configuration in Fig. 3.26 introduces an interconnection of resistances that warrants further discussion. If we replace the galvanometer with its equivalent resistance $R_{m}$, we can draw the circuit shown in Fig. 3.28. We cannot reduce the interconnected resistors of this circuit to a single equivalent resistance across the terminals of the battery if restricted to the simple series or parallel equivalent circuits introduced earlier in this chapter. The interconnected resistors can be reduced to a single equivalent resistor by means of a delta-to-wye ( $\Delta$-to-Y) or pi-to-tee ( $\pi$-to-T) equivalent circuit. ${ }^{1}$

The resistors $R_{1}, R_{2}$, and $R_{m}$ ( or $R_{3}, R_{m}$ and $R_{x}$ ) in the circuit shown in Fig. 3.28 are referred to as a delta ( $\Delta$ ) interconnection because the interconnection looks like the Greek letter $\Delta$. It also is referred to as a pi interconnection because the $\Delta$ can be shaped into a $\pi$ without disturbing the electrical equivalence of the two configurations. The electrical equivalence between the $\Delta$ and $\pi$ interconnections is apparent in Fig. 3.29.

The resistors $R_{1}, R_{m}$, and $R_{3}$ (or $R_{2}, R_{m}$ and $R_{x}$ ) in the circuit shown in Fig. 3.28 are referred to as a wye ( $\mathbf{Y}$ ) interconnection because the interconnection can be shaped to look like the letter Y. It is easier to see the Y shape when the interconnection is drawn as in Fig. 3.30. The Y configuration also is referred to as a tee ( $\mathbf{T}$ ) interconnection because the Y structure can be shaped into a T structure without disturbing the electrical equivalence of the two structures. The electrical equivalence of the Y and the T configurations is apparent from Fig. 3.30.

Figure 3.31 illustrates the $\Delta$-to-Y (or $\pi$-to-T) equivalent circuit transformation. Note that we cannot transform the $\Delta$ interconnection into the Y interconnection simply by changing the shape of the interconnections. Saying the $\Delta$-connected circuit is equivalent to the Y-connected circuit means that the $\Delta$ configuration can be replaced with a Y configuration to make the terminal behavior of the two configurations identical. Thus if each circuit is placed in a black box, we can't tell by external measurements whether the box contains a set of $\Delta$-connected resistors or a set of Y-connected resistors. This condition is true only if the resistance between corresponding terminal pairs is the same for each box. For example, the resistance between terminals a and b must be the same whether we use the $\Delta$-connected set or the Y-connected set. For each pair of terminals in the $\Delta$-connected circuit, the equivalent resistance can be computed using series and parallel simplifications to yield

$$
\begin{gather*}
R_{\mathrm{ab}}=\frac{R_{c}\left(R_{a}+R_{b}\right)}{R_{a}+R_{b}+R_{c}}=R_{1}+R_{2},  \tag{3.41}\\
R_{\mathrm{bc}}=\frac{R_{a}\left(R_{b}+R_{c}\right)}{R_{a}+R_{b}+R_{c}}=R_{2}+R_{3},  \tag{3.42}\\
R_{\mathrm{ca}}=\frac{R_{b}\left(R_{c}+R_{a}\right)}{R_{a}+R_{b}+R_{c}}=R_{1}+R_{3} . \tag{3.43}
\end{gather*}
$$

[^1]image_name:Figure 3.28 Δ A resistive network generated by a Wheatstone bridge circuit
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'b', 'N2': 'd'
'name': 'Rm', 'type': 'Resistor', 'value': 'Rm', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'Rx', 'type': 'Resistor', 'value': 'Rx', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'v', 'type': 'VoltageSource', 'value': 'v', 'ports': {'Np': 'a', 'Nn': 'd'
]
extrainfo:The circuit is a Wheatstone bridge with resistors R1, R2, R3, Rm, and Rx. The voltage source v is connected between nodes a and d.


Figure $3.28 \triangle A$ resistive network generated by a Wheatstone bridge circuit.
image_name:Figure 3.29
description:
[
'name': 'Rc', 'type': 'Resistor', 'value': 'Rc', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'Rb', 'type': 'Resistor', 'value': 'Rb', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'Ra', 'type': 'Resistor', 'value': 'Ra', 'ports': {'N1': 'b', 'N2': 'c'
]
extrainfo:The diagram shows a Delta (Δ) configuration on the left and a Pi (π) configuration on the right. Both configurations are equivalent in terms of resistance between nodes a, b, and c.


Figure 3.29 A A $\Delta$ configuration viewed as a $\pi$ configuration.
image_name:Figure 3.30
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'd'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'b', 'N2': 'd'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'c', 'N2': 'd'
]
extrainfo: The left side shows a Y configuration with resistors R1, R2, and R3 connected to nodes a, b, and c. The right side shows a T configuration with the same resistors and nodes.


Figure $3.31 \triangle \mathrm{~A} Y$ structure viewed as a $T$ structure.
image_name:Figure 3.30
description:
[
'name': 'Ra', 'type': 'Resistor', 'value': 'Ra', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'Rb', 'type': 'Resistor', 'value': 'Rb', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'Rc', 'type': 'Resistor', 'value': 'Rc', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo: The left side shows a Δ configuration with resistors Ra, Rb, and Rc connected to nodes a, b, and c. The right side shows a Y configuration with resistors R1, R2, and R3 connected to the same nodes.


Figure $3.31 \Delta$ The $\Delta$-to- $Y$ transformation.

Straightforward algebraic manipulation of Eqs. 3.41-3.43 gives values for the Y-connected resistors in terms of the $\Delta$-connected resistors required for the $\Delta$-to-Y equivalent circuit:

$$
\begin{align*}
R_{1} & =\frac{R_{b} R_{c}}{R_{a}+R_{b}+R_{c}}  \tag{3.44}\\
R_{2} & =\frac{R_{c} R_{a}}{R_{a}+R_{b}+R_{c}}  \tag{3.45}\\
R_{3} & =\frac{R_{a} R_{b}}{R_{a}+R_{b}+R_{c}} \tag{3.46}
\end{align*}
$$

Reversing the $\Delta$-to-Y transformation also is possible. That is, we can start with the Y structure and replace it with an equivalent $\Delta$ structure. The expressions for the three $\Delta$-connected resistors as functions of the three Y-connected resistors are

$$
\begin{align*}
R_{a} & =\frac{R_{1} R_{2}+R_{2} R_{3}+R_{3} R_{1}}{R_{1}}  \tag{3.47}\\
R_{b} & =\frac{R_{1} R_{2}+R_{2} R_{3}+R_{3} R_{1}}{R_{2}}  \tag{3.48}\\
R_{c} & =\frac{R_{1} R_{2}+R_{2} R_{3}+R_{3} R_{1}}{R_{3}} \tag{3.49}
\end{align*}
$$

Example 3.7 illustrates the use of a $\Delta$-to-Y transformation to simplify the analysis of a circuit.

#### Example 3.7 Applying a Delta-to-Wye Transform

Find the current and power supplied by the 40 V source in the circuit shown in Fig. 3.32.
image_name:Figure 3.32
description:
[
'name': 'V1', 'type': 'VoltageSource', 'value': '40V', 'ports': {'Np': 'a', 'Nn': 'e'
'name': 'R1', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': '100Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R3', 'type': 'Resistor', 'value': '125Ω', 'ports': {'N1': 'b', 'N2': 'd'
'name': 'R4', 'type': 'Resistor', 'value': '25Ω', 'ports': {'N1': 'c', 'N2': 'd'
'name': 'R5', 'type': 'Resistor', 'value': '40Ω', 'ports': {'N1': 'c', 'N2': 'e'
'name': 'R6', 'type': 'Resistor', 'value': '37.5Ω', 'ports': {'N1': 'd', 'N2': 'e'
]
extrainfo:The circuit contains a Delta configuration of resistors between nodes b, c, and d. A Delta-to-Wye transformation can be applied to simplify the analysis.


Figure 3.32 $\triangle$ The circuit for Example 3.7.

#### Solution

We are interested only in the current and power drain on the 40 V source, so the problem has been solved once we obtain the equivalent resistance across the terminals of the source. We can find this equivalent resistance easily after replacing either the upper $\Delta(100,125,25 \Omega)$ or the lower $\Delta$ (40, $25,37.5 \Omega$ ) with its equivalent Y . We choose to replace the upper $\Delta$. We then compute the three

Y resistances, defined in Fig. 3.33, from Eqs. 3.44 to 3.46. Thus,

$$
\begin{aligned}
& R_{1}=\frac{100 \times 125}{250}=50 \Omega \\
& R_{2}=\frac{125 \times 25}{250}=12.5 \Omega \\
& R_{3}=\frac{100 \times 25}{250}=10 \Omega
\end{aligned}
$$

Substituting the Y-resistors into the circuit shown in Fig. 3.32 produces the circuit shown in Fig. 3.34. From Fig. 3.34, we can easily calculate the resistance across the terminals of the 40 V source by series-parallel simplifications:

$$
R_{\mathrm{eq}}=55+\frac{(50)(50)}{100}=80 \Omega
$$

The final step is to note that the circuit reduces to an $80 \Omega$ resistor across a 40 V source, as shown in Fig. 3.35, from which it is apparent that the 40 V source delivers 0.5 A and 20 W to the circuit.
image_name:Figure 3.33
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '100Ω', 'ports': {'N1': 'N1', 'N2': 'N2'
'name': '25Ω', 'type': 'Resistor', 'value': '25Ω', 'ports': {'N1': 'N2', 'N2': 'N3'
'name': '125Ω', 'type': 'Resistor', 'value': '125Ω', 'ports': {'N1': 'N3', 'N2': 'N1'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'N1', 'N2': 'N4'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'N3', 'N2': 'N4'
'name': 'R3', 'type': 'Resistor', 'value': 'R3', 'ports': {'N1': 'N2', 'N2': 'N4'
]
extrainfo:The circuit is a delta configuration with resistors R1, R2, and R3 forming a triangle.


Figure 3.33 $\Delta$ The equivalent $Y$ resistors.
image_name:Figure 3.34
description:
[
'name': 'V1', 'type': 'VoltageSource', 'value': '40V', 'ports': {'Np': 'a', 'Nn': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'b', 'N2': 'd'
'name': 'R3', 'type': 'Resistor', 'value': '50Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R4', 'type': 'Resistor', 'value': '40Ω', 'ports': {'N1': 'd', 'N2': 'GND'
'name': 'R5', 'type': 'Resistor', 'value': '12.5Ω', 'ports': {'N1': 'c', 'N2': 'e'
'name': 'R6', 'type': 'Resistor', 'value': '37.5Ω', 'ports': {'N1': 'e', 'N2': 'GND'
]
extrainfo:The circuit is a simplified version of a delta to wye transformation. It contains a voltage source and a network of resistors forming a bridge configuration.


Figure 3.35 A The final step in the simplification of the circuit shown in Fig. 3.32.

Figure 3.34 A A transformed version of the circuit shown in Fig. 3.32.

ASSESSMENT PROBLEM

Objective 6—Know when and how to use delta-to-wye equivalent circuits
3.8 Use a Y-to- $\Delta$ transformation to find the voltage $v$ in the circuit shown.

Answer: 35 V .
NOTE: Also try Chapter Problems 3.60, 3.62, and 3.63.
image_name:3.8
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '28Ω', 'ports': {'N1': 'a', 'N2': 'c'
'name': 'R2', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R3', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'b', 'N2': 'c'
'name': 'R4', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'b', 'N2': 'e'
'name': 'R5', 'type': 'Resistor', 'value': '105Ω', 'ports': {'N1': 'c', 'N2': 'e'
'name': 'I1', 'type': 'CurrentSource', 'value': '2A', 'ports': {'Np': 'e', 'Nn': 'a'
]
extrainfo:The circuit forms a resistive bridge network with a current source.


Practical Perspective

Resistive Touch Screens

Begin by analyzing the resistive grid in the $x$-direction. We model the resistance of the grid in the $x$-direction with the resistance $R_{x^{\prime}}$ as shown in Fig. 3.34. The $x$-location where the screen is touched is indicated by the arrow. The resulting voltage drop across the resistance $\alpha R_{x}$ is $V_{x}$. Touching the screen effectively divides the total resistance, $R_{x^{\prime}}$ into two separate resistances $\alpha R_{x}$ and $(1-\alpha) R_{x}$.

From the figure you can see that when the touch is on the far right side of the screen, $\alpha=0$, and $V_{x}=0$. Similarly, when the touch is on the far left side of the screen, $\alpha=1$, and $V_{x}=V_{s}$. If the touch is in between the two edges of the screen, the value of $\alpha$ is between 0 and 1 and the two parts of the resistance $R_{x}$ form a voltage divider. We can calculate the voltage $V_{x}$ using the equation for voltage division:

$$
V_{x}=\frac{\alpha R_{x}}{\alpha R_{x}+(1-\alpha) R_{x}} V_{s}=\frac{\alpha R_{x}}{R_{x}} V_{s}=\alpha V_{s} .
$$

We can find the value of $\alpha$, which represents the location of the touch point with respect the far right side of the screen, by dividing the voltage
image_name:Figure 3.36
description:
[
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': 'vs', 'Nn': 'GND'
'name': 'Rx', 'type': 'Resistor', 'value': 'Rx', 'ports': {'N1': 'vs', 'N2': 'GND'
]
extrainfo:The circuit diagram represents a resistive touch screen grid in the x-direction. The resistor Rx is divided into two parts: (1-α)Rx and αRx, forming a voltage divider. The voltage Vx across αRx is a fraction α of the source voltage Vs.


Figure $3.36 \triangle$ The resistive touch screen grid in the $x$-direction.
across the grid resistance starting at the touch point, $V_{x^{\prime}}$ by the voltage applied across the entire resistive grid in the $x$-direction, $V_{s}$ :

$$
\alpha=\frac{V_{x}}{V_{s}} .
$$

Now we want to use the value of $\alpha$ to determine the $x$-coordinate of the touch location on the screen. Typically the screen coordinates are specified in terms of pixels (short for "picture elements"). For example, the screen of a mobile phone would be divided into a grid of pixels with $p_{x}$ pixels in the $x$-direction, and $p_{y}$ pixels in the $y$-direction. Each pixel is identified by its $x$-location (a number between 0 and $p_{x}-1$ ) and its $y$-location (a number between 0 and $\left.p_{y}-1\right)$. The pixel with the location $(0,0)$ is in the upper left hand corner of the screen, as shown in Fig. 3.37.
image_name:Figure 3.37
description:The image, labeled as Figure 3.37, displays a rectangular grid representing a screen divided into pixels. The corners of the rectangle are marked with pixel coordinates. The top-left corner is labeled \((0,0)\), indicating the starting point of the grid. The top-right corner is labeled \((p_x-1, 0)\), showing the maximum x-coordinate at the top edge. The bottom-left corner is marked \((0, p_y-1)\), indicating the maximum y-coordinate at the left edge. Finally, the bottom-right corner is labeled \((p_x-1, p_y-1)\), representing the maximum x and y coordinates on the screen. This setup illustrates how pixel coordinates are structured on a screen, with \(p_x\) pixels in the x-direction and \(p_y\) pixels in the y-direction."}


Figure 3.37 $\Delta$ The pixel coordinates of a screen with $p_{x}$ pixels in the $x$-direction and $p_{y}$ pixels in the $y$-direction.

Since $\alpha$ represents the location of the touch point with respect to the right side of the screen, $(1-\alpha)$ represents the location of the touch point with respect to the left side of the screen. Therefore, the $x$-coordinate of the pixel corresponding to the touch point is

$$
x=(1-\alpha) p_{x}
$$

Note that the value of $x$ is capped at $\left(p_{x}-1\right)$.
Using the model of the resistive screen grid in the $y$-direction shown in Fig. 3.38, it is easy to show that the voltage created by a touch at the arrow is given by

$$
V_{y}=\beta V_{s} .
$$

image_name:Figure 3.38
description:
[
'name': 'Ry', 'type': 'Resistor', 'value': 'Ry', 'ports': {'N1': 'Vin', 'N2': 'GND'
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': 'Vin', 'Nn': 'GND'
]
extrainfo:The circuit represents a resistive touch screen grid model in the y-direction. The resistor Ry is split into two parts: (1-β)Ry and βRy, with a voltage Vy across the βRy section. The voltage source Vs is connected between Vin and GND.


Figure $3.38 \triangle$ The resistive touch screen grid in the $y$-direction.
Therefore, the $y$-coordinate of the pixel corresponding to the touch point is

$$
y=(1-\beta) p_{y}
$$

where the value of $y$ is capped at $\left(p_{y}-1\right)$. (See Problem 3.72.)
NOTE: Assess your understanding of the Practical Perspective by solving Chapter
Problems 3.72-3.75.

## Summary

- Series resistors can be combined to obtain a single equivalent resistance according to the equation

$$
R_{\mathrm{eq}}=\sum_{i=1}^{k} R_{i}=R_{1}+R_{2}+\cdots+R_{k}
$$

(See page 58.)

- Parallel resistors can be combined to obtain a single equivalent resistance according to the equation

$$
\frac{1}{R_{\mathrm{eq}}}=\sum_{i=1}^{k} \frac{1}{R_{i}}=\frac{1}{R_{1}}+\frac{1}{R_{2}}+\cdots+\frac{1}{R_{k}}
$$

When just two resistors are in parallel, the equation for equivalent resistance can be simplified to give

$$
R_{\mathrm{eq}}=\frac{R_{1} R_{2}}{R_{1}+R_{2}}
$$

(See pages 59-60.)

- When voltage is divided between series resistors, as shown in the figure, the voltage across each resistor can be found according to the equations

$$
\begin{aligned}
v_{1} & =\frac{R_{1}}{R_{1}+R_{2}} v_{s} \\
v_{2} & =\frac{R_{2}}{R_{1}+R_{2}} v_{s}
\end{aligned}
$$

(See page 61.)

- When current is divided between parallel resistors, as shown in the figure, the current through each resistor can be found according to the equations
$i_{1}=\frac{R_{2}}{R_{1}+R_{2}} i_{s}$.
$i_{2}=\frac{R_{1}}{R_{1}+R_{2}} i_{s}$.
(See page 63.)
image_name:Figure 2
description:
[
'name': 'is', 'type': 'CurrentSource', 'value': 'is', 'ports': {'Np': 'b', 'Nn': 'a'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit is a parallel configuration with a current source is feeding two resistors R1 and R2. The current divides between R1 and R2, with i1 flowing through R1 and i2 flowing through R2.

- Voltage division is a circuit analysis tool that is used to find the voltage drop across a single resistance from a collection of series-connected resistances when the voltage drop across the collection is known:

$$
v_{j}=\frac{R_{j}}{R_{\mathrm{eq}}} v
$$

where $v_{j}$ is the voltage drop across the resistance $R_{j}$ and $v$ is the voltage drop across the series-connected resistances whose equivalent resistance is $R_{\text {eq }}$. (See page 65.)

- Current division is a circuit analysis tool that is used to find the current through a single resistance from a collection of parallel-connected resistances when the current into the collection is known:

$$
I_{j}=\frac{R_{\mathrm{eq}}}{R_{j}} i
$$

where $i_{j}$ is the current through the resistance $R_{j}$ and $i$ is the current into the parallel-connected resistances whose equivalent resistance is $R_{\text {eq }}$. (See page 65. )

- A voltmeter measures voltage and must be placed in parallel with the voltage being measured. An ideal voltmeter has infinite internal resistance and thus does not alter the voltage being measured. (See page 66.)
- An ammeter measures current and must be placed in series with the current being measured. An ideal ammeter has zero internal resistance and thus does not alter the current being measured. (See page 66.)
- Digital meters and analog meters have internal resistance, which influences the value of the circuit variable being measured. Meters based on the d'Arsonval meter
movement deliberately include internal resistance as a way to limit the current in the movement's coil. (See page 67.)
- The Wheatstone bridge circuit is used to make precise measurements of a resistor's value using four resistors, a dc voltage source, and a galvanometer. A Wheatstone bridge is balanced when the resistors obey Eq. 3.33, resulting in a galvanometer reading of 0 A . (See page 69.)
- A circuit with three resistors connected in a $\Delta$ configuration (or a $\pi$ configuration) can be transformed into an equivalent circuit in which the three resistors are Y connected (or T connected). The $\Delta$-to-Y transformation is given by Eqs. 3.44-3.46; the Y-to- $\Delta$ transformation is given by Eqs. 3.47-3.49. (See page 72.)
