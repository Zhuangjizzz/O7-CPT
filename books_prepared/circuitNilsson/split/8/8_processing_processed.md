# 8. Natural and Step Responses of RLC Circuits

CHAPTER CONTENTS

8.1 Introduction to the Natural Response of a Parallel RLC Circuit p. 266
8.2 The Forms of the Natural Response of a Parallel RLC Circuit p. 270
8.3 The Step Response of a Parallel RLC Circuit p. 280
8.4 The Natural and Step Response of a Series RLC Circuit p. 285
8.5 A Circuit with Two Integrating Amplifiers p. 289

CHAPTER OBJECTIVES

1 Be able to determine the natural response and the step response of parallel $R L C$ circuits.
2 Be able to determine the natural response and the step response of series RLC circuits.

Natural and Step Responses of RLC Circuits

In this chapter, discussion of the natural response and step response of circuits containing both inductors and capacitors is limited to two simple structures: the parallel $R L C$ circuit and the series $R L C$ circuit. Finding the natural response of a parallel $R L C$ circuit consists of finding the voltage created across the parallel branches by the release of energy stored in the inductor or capacitor or both. The task is defined in terms of the circuit shown in Fig. 8.1 on page 266. The initial voltage on the capacitor, $V_{0}$, represents the initial energy stored in the capacitor. The initial current through the inductor, $I_{0}$, represents the initial energy stored in the inductor. If the individual branch currents are of interest, you can find them after determining the terminal voltage.

We derive the step response of a parallel $R L C$ circuit by using Fig. 8.2 on page 266. We are interested in the voltage that appears across the parallel branches as a result of the sudden application of a dc current source. Energy may or may not be stored in the circuit when the current source is applied.

Finding the natural response of a series $R L C$ circuit consists of finding the current generated in the series-connected elements by the release of initially stored energy in the inductor, capacitor, or both. The task is defined by the circuit shown in Fig. 8.3 on page 266. As before, the initial inductor current, $I_{0}$, and the initial capacitor voltage, $V_{0}$, represent the initially stored energy. If any of the individual element voltages are of interest, you can find them after determining the current.

We describe the step response of a series $R L C$ circuit in terms of the circuit shown in Fig. 8.4 on page 266. We are interested in the current resulting from the sudden application of the dc voltage source. Energy may or may not be stored in the circuit when the switch is closed.

If you have not studied ordinary differential equations, derivation of the natural and step responses of parallel and series $R L C$ circuits may be a bit difficult to follow. However, the results are important enough to warrant presentation at this time. We begin with the natural response of a parallel $R L C$ circuit and cover this material over two sections: one to discuss the solution of the differential equation that describes the circuit and one to present the three distinct forms that the solution can take.

Practical Perspective

Clock for Computer Timing

The digital circuits found in most computers require a timing signal that synchronizes the operation of the circuits. Consider a laptop computer whose processor speed is 2 GHz . This means that the central processing unit for this computer can perform about $2 \times 10^{9}$ simple operations every second.

The timing signal, produced by a clock generator chip, is typically a square wave with the required clock frequency. The square wave is obtained from a sinusoidal wave with the required clock frequency. Typically, the sinusoidal wave is
image_name:Scanrail / fotolia
description:The image shows a set of three electronic devices: a laptop, a smartphone, and a tablet, all displaying the same interface on their screens. The interface appears to be a financial or data analysis application, as indicated by the presence of graphs, charts, and numerical data.

1. **Identification of Components and Structure:**
- **Laptop:** Positioned on the left, it has a keyboard and a large screen displaying a graph that covers most of the screen area. The graph is overlaid on a world map background, suggesting global data tracking.
- **Smartphone:** Centrally placed, it has a smaller screen with the same interface as the laptop and tablet, indicating synchronization across devices.
- **Tablet:** On the right, it features a large screen similar to the laptop, also displaying the same graphical interface.

2. **Connections and Interactions:**
- The devices are likely connected via a network or cloud service, enabling them to display synchronized data in real-time. This suggests a seamless integration of data across multiple platforms, allowing users to access the same information regardless of the device.

3. **Labels, Annotations, and Key Features:**
- The screens display a graph with a timeline and numerical values, possibly representing stock market data or other financial metrics.
- A pie chart is visible, indicating data distribution or market shares.
- The top of the screens shows a date and time, possibly indicating the last update of the data.
- Additional icons and buttons are present, likely for navigation and interaction with the application, such as settings or refresh options.


Scanrail / fotolia
image_name:quartz crystal and analog to digital conversion
description:The system block diagram titled "quartz crystal and analog to digital conversion" consists of two primary components: a quartz crystal and an analog to digital conversion block.

1. **Main Components:**
- **Quartz Crystal:** This block is responsible for generating a stable frequency. The quartz crystal, when voltage is applied, oscillates at a precise frequency, producing a sinusoidal waveform. This stable frequency is crucial for synchronizing digital circuits.
- **Analog to Digital Conversion (ADC):** This block converts the analog sinusoidal signal produced by the quartz crystal into a digital signal. It processes the continuous waveform and outputs a series of discrete digital values.

2. **Flow of Information or Control:**
- The sinusoidal waveform generated by the quartz crystal is depicted as a wavy red line, indicating its analog nature. This signal flows from the quartz crystal block to the ADC block.
- The ADC then converts this analog signal into a digital format, represented by a square wave pattern in blue, showing the transition from analog to digital.

3. **Labels, Annotations, and Key Indicators:**
- The blocks are clearly labeled as "quartz crystal" and "analog to digital conversion," indicating their respective functions.
- The flow of the signal is visually represented by the red wavy line and the blue square wave, illustrating the transformation from analog to digital.

4. **Overall System Function:**
- The primary function of this system is to take a stable frequency generated by a quartz crystal and convert it into a digital signal. This conversion is essential for digital systems that require precise timing and synchronization, such as in clocks, computers, and communication devices. The arrangement of the blocks ensures that the analog signal is accurately transformed into a digital format suitable for further processing in digital circuits.

generated by precisely-cut quartz crystal with an applied voltage. The crystal produces a very stable frequency suitable for synchronizing digital circuits.

But we can also generate a sinusoidal wave using a circuit with an inductor and a capacitor. By choosing the values of inductance and capacitance, we can create a sinusoid with a specific frequency. We will examine such a design once we have presented the fundamental concepts of second-order circuits.
image_name:VLi120C
description:The image depicts a detailed view of a printed circuit board (PCB) featuring several electronic components. At the center of the image, there is a large integrated circuit (IC) chip labeled "VLi120C," manufactured by STMicroelectronics, with additional markings such as "J55IRBP," "A22AB605," "MALTA," and "NLBEDCT." This chip is likely a central processing unit or a specialized processor given its prominence and the number of pins.

Surrounding the main IC, there are numerous smaller components typical of a PCB, including resistors, capacitors, and other ICs. Notable among these is a metal-cased component labeled "CSC," which is likely a crystal oscillator used for generating a stable clock signal for the circuit.

The PCB is densely populated with surface-mounted components (SMCs), and traces are visible, indicating the connections between various components. There are also several labeled points and connectors, such as "CN3" and "CN2," which suggest points for external connections or testing.

Annotations and labels such as "R24," "C19," "R25," and "U6" are visible, indicating component references which are typically used for assembly and troubleshooting. The board also has a visible copyright marking, "COPYRIGHT © 2002," indicating the design's intellectual property rights.

Overall, the PCB appears to be a complex assembly likely used in computing or digital processing applications, with the VLi120C chip serving as a central element in its function.


David J. Green / Alamy

image_name:Figure 8.1
description:
[
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'V0', 'Nn': 'GND'
'name': 'L', 'type': 'Inductor', 'value': 'L', 'ports': {'N1': 'V0', 'N2': 'GND'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'V0', 'N2': 'GND'
]
extrainfo:The circuit illustrates the natural response of a parallel RLC circuit. The components are connected in parallel between the nodes VD and GND with a initial voltage source V0 applied across the capacitor C.
Figure $8.1 \triangle \mathrm{~A}$ circuit used to illustrate the natural response of a parallel RLC circuit.

image_name:Figure 8.2
description:
[
'name': 'I', 'type': 'CurrentSource', 'value': 'I', 'ports': {'Np': 'GND', 'Nn': 'V'
'name': 'Switch', 'type': 'Switch', 'ports': {'N1': 'V', 'N2': 'GND'
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'V', 'Nn': 'GND'
'name': 'L', 'type': 'Inductor', 'value': 'L', 'ports': {'N1': 'V', 'N2': 'GND'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'V', 'N2': 'GND'
]
extrainfo:The circuit represents the step response of a parallel RLC circuit with a current source I, a switch, and a voltage source v across the capacitor. All components are connected in parallel between node V and ground (GND).
Figure $8.2 \triangle \mathrm{~A}$ circuit used to illustrate the step response of a parallel RLC circuit.

image_name:Figure 8.3
description:
[
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': 'L', 'type': 'Inductor', 'value': 'L', 'ports': {'N1': 'X1', 'N2': 'Vo'
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'Vo', 'Nn': 'GND'
]
extrainfo:The circuit represents the natural response of a series RLC circuit. It includes a resistor R, an inductor L, and a capacitor C connected in series with a voltage source Vo across the capacitor. The current i flows clockwise through the circuit.
Figure $8.3 \triangle \mathrm{~A}$ circuit used to illustrate the natural response of a series RLC circuit.

image_name:Figure 8.4
description:
[
'name': 'V', 'type': 'VoltageSource', 'value': 'V', 'ports': {'Np': 'V', 'Nn': 'GND'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'V', 'N2': 'X1'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'X1', 'N2': 'X2'
'name': 'L', 'type': 'Inductor', 'value': 'L', 'ports': {'N1': 'X2', 'N2': 'X3'
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'X3', 'Nn': 'GND'
]
extrainfo:The circuit represents the natural response of a series RLC circuit with a voltage source V, resistor R, inductor L, and capacitor C. The switch SW1 is initially open and closes at t=0, allowing current i to flow clockwise.
Figure $8.4 \triangle \mathrm{~A}$ circuit used to illustrate the step response of a series RLC circuit.

After introducing these three forms, we show that the same forms apply to the step response of a parallel $R L C$ circuit as well as to the natural and step responses of series $R L C$ circuits.

## 8.1 Introduction to the Natural Response of a Parallel RLC Circuit

The first step in finding the natural response of the circuit shown in Fig. 8.1 is to derive the differential equation that the voltage $v$ must satisfy. We choose to find the voltage first, because it is the same for each component. After that, a branch current can be found by using the current-voltage relationship for the branch component. We easily obtain the differential equation for the voltage by summing the currents away from the top node, where each current is expressed as a function of the unknown voltage $v$ :

$$
\begin{equation*}
\frac{v}{R}+\frac{1}{L} \int_{0}^{t} v d \tau+I_{0}+C \frac{d v}{d t}=0 \tag{8.1}
\end{equation*}
$$

We eliminate the integral in Eq. 8.1 by differentiating once with respect to $t$, and, because $I_{0}$ is a constant, we get

$$
\begin{equation*}
\frac{1}{R} \frac{d v}{d t}+\frac{v}{L}+C \frac{d^{2} v}{d t^{2}}=0 \tag{8.2}
\end{equation*}
$$

We now divide through Eq. 8.2 by the capacitance $C$ and arrange the derivatives in descending order:

$$
\begin{equation*}
\frac{d^{2} v}{d t^{2}}+\frac{1}{R C} \frac{d v}{d t}+\frac{v}{L C}=0 \tag{8.3}
\end{equation*}
$$

Comparing Eq. 8.3 with the differential equations derived in Chapter 7 reveals that they differ by the presence of the term involving the second derivative. Equation 8.3 is an ordinary, second-order differential equation with constant coefficients. Circuits in this chapter contain both inductors and capacitors, so the differential equation describing these circuits is of the second order. Therefore, we sometimes call such circuits second-order circuits.

The General Solution of the Second-Order Differential Equation

We can't solve Eq. 8.3 by separating the variables and integrating as we were able to do with the first-order equations in Chapter 7. The classical approach to solving Eq. 8.3 is to assume that the solution is of exponential form, that is, to assume that the voltage is of the form

$$
\begin{equation*}
v=A e^{s t} \tag{8.4}
\end{equation*}
$$

where $A$ and $s$ are unknown constants.
Before showing how this assumption leads to the solution of Eq. 8.3, we need to show that it is rational. The strongest argument we can make in favor of Eq. 8.4 is to note from Eq. 8.3 that the second derivative of the
solution, plus a constant times the first derivative, plus a constant times the solution itself, must sum to zero for all values of $t$. This can occur only if higher order derivatives of the solution have the same form as the solution. The exponential function satisfies this criterion. A second argument in favor of Eq. 8.4 is that the solutions of all the first-order equations we derived in Chapter 7 were exponential. It seems reasonable to assume that the solution of the second-order equation also involves the exponential function.

If Eq. 8.4 is a solution of Eq. 8.3, it must satisfy Eq. 8.3 for all values of $t$. Substituting Eq. 8.4 into Eq. 8.3 generates the expression

$$
A s^{2} e^{s t}+\frac{A s}{R C} e^{s t}+\frac{A e^{s t}}{L C}=0
$$

or

$$
\begin{equation*}
A e^{s t}\left(s^{2}+\frac{s}{R C}+\frac{1}{L C}\right)=0 \tag{8.5}
\end{equation*}
$$

which can be satisfied for all values of $t$ only if $A$ is zero or the parenthetical term is zero, because $e^{s t} \neq 0$ for any finite values of $s t$. We cannot use $A=0$ as a general solution because to do so implies that the voltage is zero for all time-a physical impossibility if energy is stored in either the inductor or capacitor. Therefore, in order for Eq. 8.4 to be a solution of Eq. 8.3, the parenthetical term in Eq. 8.5 must be zero, or

$$
\begin{equation*}
s^{2}+\frac{s}{R C}+\frac{1}{L C}=0 \tag{8.6}
\end{equation*}
$$

Equation 8.6 is called the characteristic equation of the differential equation because the roots of this quadratic equation determine the mathematical character of $v(t)$.

The two roots of Eq. 8.6 are

$$
\begin{align*}
& s_{1}=-\frac{1}{2 R C}+\sqrt{\left(\frac{1}{2 R C}\right)^{2}-\frac{1}{L C}}  \tag{8.7}\\
& s_{2}=-\frac{1}{2 R C}-\sqrt{\left(\frac{1}{2 R C}\right)^{2}-\frac{1}{L C}} \tag{8.8}
\end{align*}
$$

If either root is substituted into Eq. 8.4, the assumed solution satisfies the given differential equation, that is, Eq. 8.3. Note from Eq. 8.5 that this result holds regardless of the value of $A$. Therefore, both

$$
\begin{aligned}
& v=A_{1} e^{s_{1} t} \text { and } \\
& v=A_{2} e^{s_{2} t}
\end{aligned}
$$

-Characteristic equation, parallel RLC circuit
satisfy Eq. 8.3. Denoting these two solutions $v_{1}$ and $v_{2}$, respectively, we can show that their sum also is a solution. Specifically, if we let

$$
\begin{equation*}
v=v_{1}+v_{2}=A_{1} e^{s_{1} t}+A_{2} e^{s_{2} t} \tag{8.9}
\end{equation*}
$$

then

$$
\begin{align*}
\frac{d v}{d t} & =A_{1} s_{1} e^{s_{1} t}+A_{2} s_{2} e^{s_{2} t}  \tag{8.10}\\
\frac{d^{2} v}{d t^{2}} & =A_{1} s_{1}^{2} e^{s_{1} t}+A_{2} s_{2}^{2} e^{s_{2} t} \tag{8.11}
\end{align*}
$$

Substituting Eqs. 8.9-8.11 into Eq. 8.3 gives

$$
\begin{equation*}
A_{1} e^{s_{1} t}\left(s_{1}^{2}+\frac{1}{R C} s_{1}+\frac{1}{L C}\right)+A_{2} e^{s_{2} t}\left(s_{2}^{2}+\frac{1}{R C} s_{2}+\frac{1}{L C}\right)=0 \tag{8.12}
\end{equation*}
$$

But each parenthetical term is zero because by definition $s_{1}$ and $s_{2}$ are roots of the characteristic equation. Hence the natural response of the parallel $R L C$ circuit shown in Fig. 8.1 is of the form

$$
\begin{equation*}
v=A_{1} e^{s_{1} t}+A_{2} e^{s_{2} t} \tag{8.13}
\end{equation*}
$$

Equation 8.13 is a repeat of the assumption made in Eq. 8.9. We have shown that $v_{1}$ is a solution, $v_{2}$ is a solution, and $v_{1}+v_{2}$ is a solution. Therefore, the general solution of Eq. 8.3 has the form given in Eq. 8.13. The roots of the characteristic equation ( $s_{1}$ and $s_{2}$ ) are determined by the circuit parameters $R, L$, and $C$. The initial conditions determine the values of the constants $A_{1}$ and $A_{2}$. Note that the form of Eq. 8.13 must be modified if the two roots $s_{1}$ and $s_{2}$ are equal. We discuss this modification when we turn to the critically damped voltage response in Section 8.2.

The behavior of $v(t)$ depends on the values of $s_{1}$ and $s_{2}$. Therefore the first step in finding the natural response is to determine the roots of the characteristic equation. We return to Eqs. 8.7 and 8.8 and rewrite them using a notation widely used in the literature:

$$
\begin{align*}
& s_{1}=-\alpha+\sqrt{\alpha^{2}-\omega_{0}^{2}}  \tag{8.14}\\
& s_{2}=-\alpha-\sqrt{\alpha^{2}-\omega_{0}^{2}} \tag{8.15}
\end{align*}
$$

where

Neper frequency, parallel RLC circuit

Resonant radian frequency, parallel RLC circuit

$$
\begin{equation*}
\alpha=\frac{1}{2 R C} \tag{8.16}
\end{equation*}
$$

$$
\begin{equation*}
\omega_{0}=\frac{1}{\sqrt{L C}} \tag{8.17}
\end{equation*}
$$

These results are summarized in Table 8.1.

TABLE 8.1 Natural Response Parameters of the Parallel RLC Circuit

| Parameter | Terminology | Value In <br> Natural Response |
| :--- | :--- | :--- |
| $s_{1}, s_{2}$ | Characteristic roots | $s_{1}=-\alpha+\sqrt{\alpha^{2}-\omega_{0}^{2}}$ |
|  |  | $s_{2}=-\alpha-\sqrt{\alpha^{2}-\omega_{0}^{2}}$ |
| $\alpha$ | Neper frequency | $\alpha=\frac{1}{2 R C}$ |
| $\omega_{0}$ | Resonant radian frequency | $\omega_{0}=\frac{1}{\sqrt{L C}}$ |

The exponent of $e$ must be dimensionless, so both $s_{1}$ and $s_{2}$ (and hence $\alpha$ and $\omega_{0}$ ) must have the dimension of the reciprocal of time, or frequency. To distinguish among the frequencies $s_{1}, s_{2}, \alpha$, and $\omega_{0}$, we use the following terminology: $s_{1}$ and $s_{2}$ are referred to as complex frequencies, $\alpha$ is called the neper frequency, and $\omega_{0}$ is the resonant radian frequency. The full significance of this terminology unfolds as we move through the remaining chapters of this book. All these frequencies have the dimension of angular frequency per time. For complex frequencies, the neper frequency, and the resonant radian frequency, we specify values using the unit radians per second ( $\mathrm{rad} / \mathrm{s})$. The nature of the roots $s_{1}$ and $s_{2}$ depends on the values of $\alpha$ and $\omega_{0}$. There are three possible outcomes. First, if $\omega_{0}^{2}<\alpha^{2}$, both roots will be real and distinct. For reasons to be discussed later, the voltage response is said to be overdamped in this case. Second, if $\omega_{0}^{2}>\alpha^{2}$, both $s_{1}$ and $s_{2}$ will be complex and, in addition, will be conjugates of each other. In this situation, the voltage response is said to be underdamped. The third possible outcome is that $\omega_{0}^{2}=\alpha^{2}$. In this case, $s_{1}$ and $s_{2}$ will be real and equal. Here the voltage response is said to be critically damped. As we shall see, damping affects the way the voltage response reaches its final (or steady-state) value. We discuss each case separately in Section 8.2.

Example 8.1 illustrates how the numerical values of $s_{1}$ and $s_{2}$ are determined by the values of $R, L$, and $C$.

#### Example 8.1 Finding the Roots of the Characteristic Equation of a Parallel RLC Circuit

a) Find the roots of the characteristic equation that governs the transient behavior of the voltage shown in Fig. 8.5 if $R=200 \Omega, L=50 \mathrm{mH}$, and $C=0.2 \mu \mathrm{~F}$.
b) Will the response be overdamped, underdamped, or critically damped?
c) Repeat (a) and (b) for $R=312.5 \Omega$.
d) What value of $R$ causes the response to be critically damped?

image_name:Figure 8.5
description:
[
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'Vo', 'Nn': 'GND'
'name': 'L', 'type': 'Inductor', 'value': 'L', 'ports': {'N1': 'Vo', 'N2': 'GND'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'Vo', 'N2': 'GND'
]
extrainfo:This is a parallel RLC circuit. The circuit is used to analyze the natural response of the system.
Figure 8.5 $\triangle$ A circuit used to illustrate the natural response of a parallel RLC circuit.

#### Solution

a) For the given values of $R, L$, and $C$,

$$
\begin{aligned}
\alpha & =\frac{1}{2 R C}=\frac{10^{6}}{(400)(0.2)}=1.25 \times 10^{4} \mathrm{rad} / \mathrm{s} \\
\omega_{0}^{2} & =\frac{1}{L C}=\frac{\left(10^{3}\right)\left(10^{6}\right)}{(50)(0.2)}=10^{8} \mathrm{rad}^{2} / \mathrm{s}^{2}
\end{aligned}
$$

From Eqs. 8.14 and 8.15,

$$
\begin{aligned}
s_{1} & =-1.25 \times 10^{4}+\sqrt{1.5625 \times 10^{8}-10^{8}} \\
& =-12,500+7500=-5000 \mathrm{rad} / \mathrm{s} \\
s_{2} & =-1.25 \times 10^{4}-\sqrt{1.5625 \times 10^{8}-10^{8}}
\end{aligned}
$$

b) The voltage response is overdamped because $\omega_{0}^{2}<\alpha^{2}$.
c) For $R=312.5 \Omega$,

$$
\begin{aligned}
\alpha & =\frac{10^{6}}{(625)(0.2)}=8000 \mathrm{rad} / \mathrm{s} \\
\alpha^{2} & =64 \times 10^{6}=0.64 \times 10^{8} \mathrm{rad}^{2} / \mathrm{s}^{2}
\end{aligned}
$$

As $\omega_{0}^{2}$ remains at $10^{8} \mathrm{rad}^{2} / \mathrm{s}^{2}$,

$$
\begin{aligned}
& s_{1}=-8000+j 6000 \mathrm{rad} / \mathrm{s} \\
& s_{2}=-8000-j 6000 \mathrm{rad} / \mathrm{s}
\end{aligned}
$$

(In electrical engineering, the imaginary number $\sqrt{-1}$ is represented by the letter $j$, because the letter $i$ represents current.)

In this case, the voltage response is underdamped since $\omega_{0}^{2}>\alpha^{2}$.
d) For critical damping, $\alpha^{2}=\omega_{0}^{2}$, so

$$
\left(\frac{1}{2 R C}\right)^{2}=\frac{1}{L C}=10^{8}
$$

or

$$
\frac{1}{2 R C}=10^{4}
$$

and

$$
R=\frac{10^{6}}{\left(2 \times 10^{4}\right)(0.2)}=250 \Omega
$$

ASSESSMENT PROBLEM

Objective 1—Be able to determine the natural response and the step response of parallel RLC circuits
8.1 The resistance and inductance of the circuit in Fig. 8.5 are $100 \Omega$ and 20 mH , respectively.
a) Find the value of $C$ that makes the voltage response critically damped.
b) If $C$ is adjusted to give a neper frequency of $5 \mathrm{krad} / \mathrm{s}$, find the value of $C$ and the roots of the characteristic equation.
c) If $C$ is adjusted to give a resonant frequency of $20 \mathrm{krad} / \mathrm{s}$, find the value of $C$ and the roots of the characteristic equation.

Answer: (a) 500 nF ;
(b) $C=1 \mu \mathrm{~F}$, $s_{1}=-5000+j 5000 \mathrm{rad} / \mathrm{s}$, $s_{2}=-5000-j 5000 \mathrm{rad} / \mathrm{s} ;$
(c) $C=125 \mathrm{nF}$,
$s_{1}=-5359 \mathrm{rad} / \mathrm{s}$,
$s_{2}=-74,641 \mathrm{rad} / \mathrm{s}$.

NOTE: Also try Chapter Problem 8.4.

## 8.2 The Forms of the Natural Response of a Parallel RLC Circuit

So far we have seen that the behavior of a second-order $R L C$ circuit depends on the values of $s_{1}$ and $s_{2}$, which in turn depend on the circuit parameters $R$, $L$, and $C$. Therefore, the first step in finding the natural response is to calculate these values and, relatedly, determine whether the response is over-, under-, or critically damped.

Completing the description of the natural response requires finding two unknown coefficients, such as $A_{1}$ and $A_{2}$ in Eq. 8.13. The method used to do this is based on matching the solution for the natural response to the initial conditions imposed by the circuit, which are the initial value of the current (or voltage) and the initial value of the first derivative of the current (or voltage). Note that these same initial conditions, plus the final value of the variable, will also be needed when finding the step response of a second-order circuit.

In this section, we analyze the natural response form for each of the three types of damping, beginning with the overdamped response. As we will see, the response equations, as well as the equations for evaluating the unknown coefficients, are slightly different for each of the three damping configurations. This is why we want to determine at the outset of the problem whether the response is over-, under-, or critically damped.

The Overdamped Voltage Response

When the roots of the characteristic equation are real and distinct, the voltage response of a parallel $R L C$ circuit is said to be overdamped. The solution for the voltage is of the form

$$
\begin{equation*}
v=A_{1} e^{s_{1} t}+A_{2} e^{s_{2} t} \tag{8.18}
\end{equation*}
$$

where $s_{1}$ and $s_{2}$ are the roots of the characteristic equation. The constants $A_{1}$ and $A_{2}$ are determined by the initial conditions, specifically from the values of $v\left(0^{+}\right)$and $d v\left(0^{+}\right) / d t$, which in turn are determined from the initial voltage on the capacitor, $V_{0}$, and the initial current in the inductor, $I_{0}$.

Next, we show how to use the initial voltage on the capacitor and the initial current in the inductor to find $A_{1}$ and $A_{2}$. First we note from Eq. 8.18 that $A_{1}$ and $A_{2}$. First we note from Eq. 8.18 that

$$
\begin{align*}
v\left(0^{+}\right) & =A_{1}+A_{2}  \tag{8.19}\\
\frac{d v\left(0^{+}\right)}{d t} & =s_{1} A_{1}+s_{2} A_{2} \tag{8.20}
\end{align*}
$$

With $s_{1}$ and $s_{2}$ known, the task of finding $A_{1}$ and $A_{2}$ reduces to finding $v\left(0^{+}\right)$and $d v\left(0^{+}\right) / d t$. The value of $v\left(0^{+}\right)$is the initial voltage on the capacitor $V_{0}$. We get the initial value of $d v / d t$ by first finding the current in the capacitor branch at $t=0^{+}$. Then,

$$
\begin{equation*}
\frac{d v\left(0^{+}\right)}{d t}=\frac{i_{C}\left(0^{+}\right)}{C} \tag{8.21}
\end{equation*}
$$

We use Kirchhoff's current law to find the initial current in the capacitor branch. We know that the sum of the three branch currents at $t=0^{+}$ must be zero. The current in the resistive branch at $t=0^{+}$is the initial voltage $V_{0}$ divided by the resistance, and the current in the inductive branch is $I_{0}$. Using the reference system depicted in Fig. 8.5, we obtain

$$
\begin{equation*}
i_{C}\left(0^{+}\right)=\frac{-V_{0}}{R}-I_{0} \tag{8.22}
\end{equation*}
$$

After finding the numerical value of $i_{C}\left(0^{+}\right)$, we use Eq. 8.21 to find the initial value of $d v / d t$.

We can summarize the process for finding the overdamped response, $v(t)$, as follows:

1. Find the roots of the characteristic equation, $s_{1}$ and $s_{2}$, using the values of $R, L$, and $C$.
2. Find $v\left(0^{+}\right)$and $d v\left(0^{+}\right) / d t$ using circuit analysis.
3. Find the values of $A_{1}$ and $A_{2}$ by solving Eqs. 8.23 and 8.24 simultaneously:

$$
\begin{align*}
v\left(0^{+}\right) & =A_{1}+A_{2}  \tag{8.23}\\
\frac{d v\left(0^{+}\right)}{d t} & =\frac{i_{C}\left(0^{+}\right)}{C}=s_{1} A_{1}+s_{2} A_{2} \tag{8.24}
\end{align*}
$$

4. Substitute the values for $s_{1}, s_{2}, A_{1}$, and $A_{2}$ into Eq. 8.18 to determine the expression for $v(t)$ for $t \geq 0$.
Examples 8.2 and 8.3 illustrate how to find the overdamped response of a parallel $R L C$ circuit.

4 Voltage natural response-overdamped parallel RLC circuit

#### Example 8.2 Finding the Overdamped Natural Response of a Parallel RLC Circuit

For the circuit in Fig. 8.6, $v\left(0^{+}\right)=12 \mathrm{~V}$, and $i_{L}\left(0^{+}\right)=30 \mathrm{~mA}$.
a) Find the initial current in each branch of the circuit.
b) Find the initial value of $d v / d t$.
c) Find the expression for $v(t)$.
d) Sketch $v(t)$ in the interval $0 \leq t \leq 250 \mathrm{~ms}$.

#### Solution

a) The inductor prevents an instantaneous change in its current, so the initial value of the inductor current is 30 mA :

$$
i_{L}\left(0^{-}\right)=i_{L}(0)=i_{L}\left(0^{+}\right)=30 \mathrm{~mA}
$$

The capacitor holds the initial voltage across the parallel elements to 12 V . Thus the initial current in the resistive branch, $i_{R}\left(0^{+}\right)$, is $12 / 200$, or 60 mA . Kirchhoff's current law requires the sum of the currents leaving the top node to equal zero at every instant. Hence

$$
\begin{aligned}
i_{C}\left(0^{+}\right) & =-i_{L}\left(0^{+}\right)-i_{R}\left(0^{+}\right) \\
& =-90 \mathrm{~mA}
\end{aligned}
$$

Note that if we assumed the inductor current and capacitor voltage had reached their dc values at the instant that energy begins to be released, $i_{C}\left(0^{-}\right)=0$. In other words, there is an instantaneous change in the capacitor current at $t=0$.
b) Because $i_{C}=C(d v / d t)$,

$$
\frac{d v\left(0^{+}\right)}{d t}=\frac{-90 \times 10^{-3}}{0.2 \times 10^{-6}}=-450 \mathrm{kV} / \mathrm{s}
$$

c) The roots of the characteristic equation come from the values of $R, L$, and $C$. For the values specified and from Eqs. 8.14 and 8.15 along with 8.16 and 8.17,

$$
\begin{aligned}
s_{1} & =-1.25 \times 10^{4}+\sqrt{1.5625 \times 10^{8}-10^{8}} \\
& =-12,500+7500=-5000 \mathrm{rad} / \mathrm{s} \\
s_{2} & =-1.25 \times 10^{4}-2 \overline{1.5625 \times 10^{8}-10^{8}} \\
& =-12,500-7500=-20,000 \mathrm{rad} / \mathrm{s}
\end{aligned}
$$

image_name:Figure 8.6
description:
[
'name': 'C1', 'type': 'Capacitor', 'value': '0.2uF', 'ports': {'Np': 'Vo', 'Nn': 'GND'
'name': 'L1', 'type': 'Inductor', 'value': '50mH', 'ports': {'N1': 'Vo', 'N2': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': '200Ω', 'ports': {'N1': 'Vo', 'N2': 'GND'
]
extrainfo:The circuit is an RLC series circuit with a capacitor, inductor, and resistor all connected in parallel to the ground. The voltages across each component are labeled as Vo, and the currents through each component are labeled as iC, iL, and iR, respectively.
Figure 8.6 $\triangle$ The circuit for Example 8.2.

Because the roots are real and distinct, we know that the response is overdamped and hence has the form of Eq. 8.18. We find the co-efficients $A_{1}$ and $A_{2}$ from Eqs. 8.23 and 8.24. We've already determined $s_{1}, s_{2}, v\left(0^{+}\right)$, and $d v\left(0^{+}\right) / d t$, so

$$
\begin{gathered}
12=A_{1}+A_{2} \\
-450 \times 10^{3}=-5000 A_{1}-20,000 A_{2}
\end{gathered}
$$

We solve two equations for $A_{1}$ and $A_{2}$ to obtain $A_{1}=-14 \mathrm{~V}$ and $A_{2}=26 \mathrm{~V}$. Substituting these values into Eq. 8.18 yields the overdamped voltage response:

$$
v(t)=\left(-14 e^{-5000 t}+26 e^{-20,000 t}\right) \mathrm{V}, \quad t \geq 0
$$

As a check on these calculations, we note that the solution yields $v(0)=12 \mathrm{~V}$ and $d v\left(0^{+}\right) / d t$ $=-450,000 \mathrm{~V} / \mathrm{s}$.
d) Figure 8.7 shows a plot of $v(t)$ versus $t$ over the interval $0 \leq t \leq 250 \mathrm{~ms}$.
image_name:Figure 8.7
description:The graph is a time-domain waveform representing the voltage response \( v(t) \) over time \( t \). The x-axis is labeled \( t \) in microseconds (\( \mu s \)), ranging from 0 to 250 \( \mu s \). The y-axis is labeled \( v(t) \) in volts (V), with values ranging from -6 V to 12 V.

The graph displays an overdamped exponential response, starting at 12 V at \( t = 0 \). The voltage rapidly decreases, crossing the zero voltage line around 50 \( \mu s \), reaching a minimum of approximately -6 V. After reaching this minimum, the voltage begins to increase again but does not return to its initial value within the observed time frame. The overall behavior shows a rapid initial decrease followed by a gradual increase, characteristic of an overdamped response in an RLC circuit.

Key features include the initial voltage of 12 V, the zero-crossing point around 50 \( \mu s \), and the minimum voltage of approximately -6 V. The graph visually confirms the calculated response of the system as described in the context.

Figure 8.7 $\boldsymbol{\Delta}$ The voltage response for Example 8.2.

#### Example 8.3 Calculating Branch Currents in the Natural Response of a Parallel RLC Circuit

Derive the expressions that describe the three branch currents $i_{R}, i_{L}$, and $i_{C}$ in Example 8.2 (Fig. 8.6) during the time the stored energy is being released.

#### Solution

We know the voltage across the three branches from the solution in Example 8.2, namely,

$$
v(t)=\left(-14 e^{-5000 t}+26 e^{-20,000 t}\right) \mathrm{V}, \quad t \geq 0
$$

The current in the resistive branch is then
$i_{R}(t)=\frac{v(t)}{200}=\left(-70 e^{-5000 t}+130 e^{-20,000 t}\right) \mathrm{mA}, \quad t \geq 0$.

There are two ways to find the current in the inductive branch. One way is to use the integral relationship that exists between the current and the voltage at the terminals of an inductor:

$$
i_{L}(t)=\frac{1}{L} \int_{0}^{t} v_{L}(x) d x+I_{0}
$$

A second approach is to find the current in the capacitive branch first and then use the fact that $i_{R}+i_{L}+i_{C}=0$. Let's use this approach. The current in the capacitive branch is

$$
\begin{aligned}
i_{C}(t) & =C \frac{d v}{d t} \\
& =0.2 \times 10^{-6}\left(70,000 e^{-5000 t}-520,000 e^{-20,000 t}\right) \\
& =\left(14 e^{-5000 t}-104 e^{-20,000 t}\right) \mathrm{mA}, \quad t \geq 0^{+}
\end{aligned}
$$

Note that $i_{C}\left(0^{+}\right)=-90 \mathrm{~mA}$, which agrees with the result in Example 8.2.

Now we obtain the inductive branch current from the relationship

$$
\begin{aligned}
i_{L}(t) & =-i_{R}(t)-i_{C}(t) \\
& =\left(56 e^{-5000 t}-26 e^{-20,000 t}\right) \mathrm{mA}, \quad t \geq 0
\end{aligned}
$$

We leave it to you, in Assessment Problem 8.2, to show that the integral relation alluded to leads to the same result. Note that the expression for $i_{L}$ agrees with the initial inductor current, as it must.

ASSESSMENT PROBLEMS

Objective 1—Be able to determine the natural response and the step response of parallel RLC circuits
8.2 Use the integral relationship between $i_{L}$ and $v$ to find the expression for $i_{L}$ in Fig. 8.6.
Answer: $\quad i_{L}(t)=\left(56 e^{-5000 t}-26 e^{-20,000 t}\right) \mathrm{mA}, t \geq 0$.
8.3 The element values in the circuit shown are $R=2 \mathrm{k} \Omega, L=250 \mathrm{mH}$, and $C=10 \mathrm{nF}$. The initial current $I_{0}$ in the inductor is -4 A , and the initial voltage on the capacitor is 0 V . The output signal is the voltage $v$. Find (a) $i_{R}\left(0^{+}\right)$;
(b) $i_{C}\left(0^{+}\right)$;
; (c) $d v\left(0^{+}\right) / d t$;
(d) $A_{1}$;
(e) $A_{2}$; and
(f) $v(t)$ when $t \geq 0$.

description:
[
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'V0', 'Nn': 'GND'
'name': 'L', 'type': 'Inductor', 'value': 'L', 'ports': {'N1': 'V0', 'N2': 'GND'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'V0', 'N2': 'GND'
'name': 'V0', 'type': 'VoltageSource', 'value': 'V0', 'ports': {'Np': 'V0', 'Nn': 'GND'
]
extrainfo:The circuit is a parallel RLC circuit with a voltage source V0. It includes a capacitor C connected between V0 and GND, an inductor L connected between V0 and GND, and a resistor R connected between V0 and GND. The initial conditions are I0 = -4A for the inductor and 0V for the capacitor.


Answer: (a) 0;
(b) 4 A ;
(c) $4 \times 10^{8} \mathrm{~V} / \mathrm{s}$;
(d) 13,333 V;
(e) $-13,333 \mathrm{~V}$;
(f) $13,333\left(e^{-10,000 t}-e^{-40,000 t}\right) \mathrm{V}$.

NOTE: Also try Chapter Problems 8.5 and 8.13.

Damped radian frequency

Voltage natural response-underdamped parallel RLC circuits

The Underdamped Voltage Response

When $\omega_{0}^{2}>\alpha^{2}$, the roots of the characteristic equation are complex, and the response is underdamped. For convenience, we express the roots $s_{1}$ and $s_{2}$ as

$$
\begin{align*}
s_{1} & =-\alpha+\sqrt{-\left(\omega_{0}^{2}-\alpha^{2}\right)} \\
& =-\alpha+j \sqrt{\omega_{0}^{2}-\alpha^{2}} \\
& =-\alpha+j \omega_{d}  \tag{8.25}\\
s_{2} & =-\alpha-j \omega_{d} \tag{8.26}
\end{align*}
$$

where

$$
\begin{equation*}
\omega_{d}=\sqrt{\omega_{0}^{2}-\alpha^{2}} \tag{8.27}
\end{equation*}
$$

The term $\omega_{d}$ is called the damped radian frequency. We explain later the reason for this terminology.

The underdamped voltage response of a parallel $R L C$ circuit is

$$
\begin{equation*}
v(t)=B_{1} e^{-\alpha t} \cos \omega_{d} t+B_{2} e^{-\alpha t} \sin \omega_{d} t \tag{8.28}
\end{equation*}
$$

which follows from Eq. 8.18. In making the transition from Eq. 8.18 to Eq. 8.28, we use the Euler identity:

$$
\begin{equation*}
e^{ \pm j \theta}=\cos \theta \pm j \sin \theta \tag{8.29}
\end{equation*}
$$

Thus,

$$
\begin{aligned}
v(t) & =A_{1} e^{\left(-\alpha+j \omega_{d}\right) t}+A_{2} e^{-\left(\alpha+j \omega_{d}\right) t} \\
& =A_{1} e^{-\alpha t} e^{j \omega_{d} t}+A_{2} e^{-\alpha t} e^{-j \omega_{d} t} \\
& =e^{-\alpha t}\left(A_{1} \cos \omega_{d} t+j A_{1} \sin \omega_{d} t+A_{2} \cos \omega_{d} t-j A_{2} \sin \omega_{d} t\right) \\
& =e^{-\alpha t}\left[\left(A_{1}+A_{2}\right) \cos \omega_{d} t+j\left(A_{1}-A_{2}\right) \sin \omega_{d} t\right]
\end{aligned}
$$

At this point in the transition from Eq. 8.18 to 8.28, replace the arbitrary constants $A_{1}+A_{2}$ and $j\left(A_{1}-A_{2}\right)$ with new arbitrary constants denoted $B_{1}$ and $B_{2}$ to get

$$
\begin{aligned}
v & =e^{-\alpha t}\left(B_{1} \cos \omega_{d} t+B_{2} \sin \omega_{d} t\right) \\
& =B_{1} e^{-\alpha t} \cos \omega_{d} t+B_{2} e^{-\alpha t} \sin \omega_{d} t
\end{aligned}
$$

The constants $B_{1}$ and $B_{2}$ are real, not complex, because the voltage is a real function. Don't be misled by the fact that $B_{2}=j\left(A_{1}-A_{2}\right)$. In this underdamped case, $A_{1}$ and $A_{2}$ are complex conjugates, and thus $B_{1}$ and $B_{2}$ are real. (See Problems 8.12 and 8.13.) The reason for defining the underdamped response in terms of the coefficients $B_{1}$ and $B_{2}$ is that it yields a
simpler expression for the voltage, $v$. We determine $B_{1}$ and $B_{2}$ by the initial energy stored in the circuit, in the same way that we found $A_{1}$ and $A_{2}$ for the overdamped response: by evaluating $v$ at $t=0^{+}$and its derivative at $t=0^{+}$. As with $s_{1}$ and $s_{2}, \alpha$ and $\omega_{d}$ are fixed by the circuit parameters $R, L$, and $C$.

For the underdamped response, the two simultaneous equations that determine $B_{1}$ and $B_{2}$ are

$$
\begin{gather*}
v\left(0^{+}\right)=V_{0}=B_{1},  \tag{8.30}\\
\frac{d v\left(0^{+}\right)}{d t}=\frac{i_{c}\left(0^{+}\right)}{C}=-\alpha B_{1}+\omega_{d} B_{2} . \tag{8.31}
\end{gather*}
$$

Let's look at the general nature of the underdamped response. First, the trigonometric functions indicate that this response is oscillatory; that is, the voltage alternates between positive and negative values. The rate at which the voltage oscillates is fixed by $\omega_{d}$. Second, the amplitude of the oscillation decreases exponentially. The rate at which the amplitude falls off is determined by $\alpha$. Because $\alpha$ determines how quickly the oscillations subside, it is also referred to as the damping factor or damping coefficient. That explains why $\omega_{d}$ is called the damped radian frequency. If there is no damping, $\alpha=0$ and the frequency of oscillation is $\omega_{0}$. Whenever there is a dissipative element, $R$, in the circuit, $\alpha$ is not zero and the frequency of oscillation, $\omega_{d}$, is less than $\omega_{0}$. Thus when $\alpha$ is not zero, the frequency of oscillation is said to be damped.

The oscillatory behavior is possible because of the two types of energystorage elements in the circuit: the inductor and the capacitor. (A mechanical analogy of this electric circuit is that of a mass suspended on a spring, where oscillation is possible because energy can be stored in both the spring and the moving mass.) We say more about the characteristics of the underdamped response following Example 8.4, which examines a circuit whose response is underdamped. In summary, note that the overall process for finding the underdamped response is the same as that for the overdamped response, although the response equations and the simultaneous equations used to find the constants are slightly different.

#### Example 8.4 Finding the Underdamped Natural Response of a Parallel RLC Circuit

In the circuit shown in Fig. 8.8, $V_{0}=0$, and $I_{0}=-12.25 \mathrm{~mA}$.
a) Calculate the roots of the characteristic equation.
b) Calculate $v$ and $d v / d t$ at $t=0^{+}$.
c) Calculate the voltage response for $t \geq 0$.
d) Plot $v(t)$ versus $t$ for the time interval $0 \leq t \leq 11 \mathrm{~ms}$.
image_name:Figure 8.8
description:
[
'name': 'C1', 'type': 'Capacitor', 'value': '0.125uF', 'ports': {'Np': 'X', 'Nn': 'GND'
'name': 'L1', 'type': 'Inductor', 'value': '8H', 'ports': {'N1': 'X', 'N2': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': '20k', 'ports': {'N1': 'X', 'N2': 'GND'
]
extrainfo:The circuit is a parallel RLC circuit with initial conditions V0 = 0 and I0 = -12.25 mA. It is used to find the underdamped natural response.
Figure 8.8 $\triangle$ The circuit for Example 8.4.

#### Solution

a) Because

$$
\begin{aligned}
& \alpha=\frac{1}{2 R C}=\frac{10^{6}}{2(20) 10^{3}(0.125)}=200 \mathrm{rad} / \mathrm{s} \\
& \omega_{0}=\frac{1}{\sqrt{L C}}=\sqrt{\frac{10^{6}}{(8)(0.125)}}=10^{3} \mathrm{rad} / \mathrm{s}
\end{aligned}
$$

we have

$$
\omega_{0}^{2}>\alpha^{2}
$$

Therefore, the response is underdamped. Now,

$$
\begin{aligned}
\omega_{d} & =\sqrt{\omega_{0}^{2}-\alpha^{2}}=\sqrt{10^{6}-4 \times 10^{4}}=100 \sqrt{96} \\
& =979.80 \mathrm{rad} / \mathrm{s}, \\
s_{1} & =-\alpha+j \omega_{d}=-200+j 979.80 \mathrm{rad} / \mathrm{s} \\
s_{2} & =-\alpha-j \omega_{d}=-200-j 979.80 \mathrm{rad} / \mathrm{s}
\end{aligned}
$$

For the underdamped case, we do not ordinarily solve for $s_{1}$ and $s_{2}$ because we do not use them explicitly. However, this example emphasizes why $s_{1}$ and $s_{2}$ are known as complex frequencies.
b) Because $v$ is the voltage across the terminals of a capacitor, we have

$$
v(0)=v\left(0^{+}\right)=V_{0}=0
$$

Because $v\left(0^{+}\right)=0$, the current in the resistive branch is zero at $t=0^{+}$. Hence the current in the capacitor at $t=0^{+}$is the negative of the inductor current:

$$
i_{C}\left(0^{+}\right)=-(-12.25)=12.25 \mathrm{~mA}
$$

Therefore the initial value of the derivative is

$$
\frac{d v\left(0^{+}\right)}{d t}=\frac{(12.25)\left(10^{-3}\right)}{(0.125)\left(10^{-6}\right)}=98,000 \mathrm{~V} / \mathrm{s}
$$

c) From Eqs. 8.30 and $8.31, B_{1}=0$ and

$$
B_{2}=\frac{98,000}{\omega_{d}} \approx 100 \mathrm{~V}
$$

Substituting the numerical values of $\alpha, \omega_{d}, B_{1}$, and $B_{2}$ into the expression for $v(t)$ gives

$$
v(t)=100 e^{-200 t} \sin 979.80 t \mathrm{~V}, \quad t \geq 0
$$

d) Figure 8.9 shows the plot of $v(t)$ versus $t$ for the first 11 ms after the stored energy is released. It clearly indicates the damped oscillatory nature of the underdamped response. The voltage $v(t)$ approaches its final value, alternating between values that are greater than and less than the final value. Furthermore, these swings about the final value decrease exponentially with time.
image_name:Figure 8.9
description:The graph in Figure 8.9 represents the time-domain waveform of voltage, $v(t)$, plotted against time, $t$, for the first 11 milliseconds after the stored energy is released in a system. The graph is a plot of the function \( v(t) = 100 e^{-200 t} \sin(979.80 t) \) volts, which describes a damped oscillatory behavior.

1. **Type of Graph and Function**:
- This is a time-domain waveform graph showing the voltage response over time.

2. **Axes Labels and Units**:
- The horizontal axis represents time, \( t \), measured in milliseconds (ms).
- The vertical axis represents the voltage, \( v(t) \), measured in volts (V).
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends**:
- The waveform shows an underdamped response, characterized by oscillations that decrease in amplitude over time.
- Initially, the voltage peaks at approximately 100 V before oscillating with decreasing amplitude.
- The oscillations alternate above and below the zero voltage line, with the amplitude decreasing exponentially.

4. **Key Features and Technical Details**:
- The first peak occurs slightly before 1 ms, reaching close to 100 V.
- The waveform crosses the zero voltage line around 1.5 ms, reaching a negative peak near -40 V around 2.5 ms.
- Subsequent oscillations continue with decreasing amplitude, with the next positive peak occurring around 4.5 ms and the next negative peak around 6.5 ms.
- The waveform approaches zero voltage as time progresses, indicating the damping effect.

5. **Annotations and Specific Data Points**:
- There are no explicit annotations or markers on the graph, but the critical points include the initial peak and subsequent zero crossings and peaks.
- The graph effectively demonstrates the exponential decay and oscillatory nature of the voltage response, typical of an underdamped system.

Figure 8.9 $\triangle$ The voltage response for Example 8.4.

Characteristics of the Underdamped Response

The underdamped response has several important characteristics. First, as the dissipative losses in the circuit decrease, the persistence of the oscillations increases, and the frequency of the oscillations approaches $\omega_{0}$. In other words, as $R \rightarrow \infty$, the dissipation in the circuit in Fig. 8.8 approaches zero because $p=v^{2} / R$. As $R \rightarrow \infty, \alpha \rightarrow 0$, which tells us that $\omega_{d} \rightarrow \omega_{0}$. When $\alpha=0$, the maximum amplitude of the voltage remains constant; thus the oscillation at $\omega_{0}$ is sustained. In Example 8.4, if $R$ were increased to infinity, the solution for $v(t)$ would become

$$
v(t)=98 \sin 1000 t \mathrm{~V}, \quad t \geq 0
$$

Thus, in this case the oscillation is sustained, the maximum amplitude of the voltage is 98 V , and the frequency of oscillation is $1000 \mathrm{rad} / \mathrm{s}$.

We may now describe qualitatively the difference between an underdamped and an overdamped response. In an underdamped system, the response oscillates, or "bounces," about its final value. This oscillation is also referred to as ringing. In an overdamped system, the response approaches its final value without ringing or in what is sometimes described as a "sluggish" manner. When specifying the desired response of a second order system, you may want to reach the final value in the shortest time possible, and you may not be concerned with small oscillations about that final value. If so, you would design the system components to achieve an underdamped response. On the other hand, you may be concerned that the response not exceed its final value, perhaps to ensure that components are not damaged. In such a case, you would design the system components to achieve an overdamped response, and you would have to accept a relatively slow rise to the final value.

ASSESSMENT PROBLEM

Objective 1—Be able to determine the natural and the step response of parallel RLC circuits

8.4 A 10 mH inductor, a $1 \mu \mathrm{~F}$ capacitor, and a variable resistor are connected in parallel in the circuit shown. The resistor is adjusted so that the roots of the characteristic equation are $-8000 \pm j 6000 \mathrm{rad} / \mathrm{s}$. The initial voltage on the capacitor is 10 V , and the initial current in the inductor is 80 mA . Find
a) $R$;
b) $d v\left(0^{+}\right) / d t$;
c) $B_{1}$ and $B_{2}$ in the solution for $v$; and
d) $i_{L}(t)$.
image_name:parallel RLC circuit
description:
[
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'X', 'Nn': 'GND'
'name': 'L', 'type': 'Inductor', 'value': 'L', 'ports': {'N1': 'X', 'N2': 'GND'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'X', 'N2': 'GND'
]
extrainfo:The circuit is a parallel RLC circuit with a capacitor, inductor, and resistor connected in parallel between X and ground. Initial conditions are given with a voltage V0 on the capacitor and a current I0 in the inductor.


Answer:
(a) $62.5 \Omega$;
(b) $-240,000 \mathrm{~V} / \mathrm{s}$;
(c) $B_{1}=10 \mathrm{~V}, B_{2}=-80 / 3 \mathrm{~V}$;
(d) $i_{L}(t)=10 e^{-8000 t}[8 \cos 6000 t$ $+(82 / 3) \sin 6000 t] \mathrm{mA}$ when $t \geq 0$.

NOTE: Also try Chapter Problems 8.6 and 8.11.

The Critically Damped Voltage Response

The second-order circuit in Fig. 8.8 is critically damped when $\omega_{0}^{2}=\alpha^{2}$, or $\omega_{0}=\alpha$. When a circuit is critically damped, the response is on the verge of oscillating. In addition, the two roots of the characteristic equation are real and equal; that is,

$$
\begin{equation*}
s_{1}=s_{2}=-\alpha=-\frac{1}{2 R C} \tag{8.32}
\end{equation*}
$$

When this occurs, the solution for the voltage no longer takes the form of Eq. 8.18. This equation breaks down because if $s_{1}=s_{2}=-\alpha$, it predicts that

$$
\begin{equation*}
v=\left(A_{1}+A_{2}\right) e^{-\alpha t}=A_{0} e^{-\alpha t} \tag{8.33}
\end{equation*}
$$

where $A_{0}$ is an arbitrary constant. Equation 8.33 cannot satisfy two independent initial conditions $\left(V_{0}, I_{0}\right)$ with only one arbitrary constant, $A_{0}$. Recall that the circuit parameters $R$ and $C$ fix $\alpha$.

We can trace this dilemma back to the assumption that the solution takes the form of Eq. 8.18. When the roots of the characteristic equation are equal, the solution for the differential equation takes a different form, namely

$$
\begin{equation*}
v(t)=D_{1} t e^{-\alpha t}+D_{2} e^{-\alpha t} \tag{8.34}
\end{equation*}
$$

4 Voltage natural response-critically damped parallel RLC circuit
Thus in the case of a repeated root, the solution involves a simple exponential term plus the product of a linear and an exponential term. The justification of Eq. 8.34 is left for an introductory course in differential equations. Finding the solution involves obtaining $D_{1}$ and $D_{2}$ by following the same pattern set in the overdamped and underdamped cases: We use the initial values of the voltage and the derivative of the voltage with respect to time to write two equations containing $D_{1}$ and/or $D_{2}$.

From Eq. 8.34, the two simultaneous equations needed to determine $D_{1}$ and $D_{2}$ are

$$
\begin{align*}
v\left(0^{+}\right) & =V_{0}=D_{2}  \tag{8.35}\\
\frac{d v\left(0^{+}\right)}{d t} & =\frac{i_{C}\left(0^{+}\right)}{C}=D_{1}-\alpha D_{2} \tag{8.36}
\end{align*}
$$

As we can see, in the case of a critically damped response, both the equation for $v(t)$ and the simultaneous equations for the constants $D_{1}$ and $D_{2}$ differ from those for over- and underdamped responses, but the general approach is the same. You will rarely encounter critically damped systems in practice, largely because $\omega_{0}$ must equal a exactly. Both of these quantities depend on circuit parameters, and in a real circuit it is very difficult to choose component values that satisfy an exact equality relationship.

Example 8.5 illustrates the approach for finding the critically damped response of a parallel $R L C$ circuit.

#### Example 8.5 Finding the Critically Damped Natural Response of a Parallel RLC Circuit

a) For the circuit in Example 8.4 (Fig. 8.8), find the value of $R$ that results in a critically damped voltage response.
b) Calculate $v(t)$ for $t \geq 0$.
c) Plot $v(t)$ versus $t$ for $0 \leq t \leq 7 \mathrm{~ms}$.

#### Solution

a) From Example 8.4, we know that $\omega_{0}^{2}=10^{6}$. Therefore for critical damping,

$$
\alpha=10^{3}=\frac{1}{2 R C}
$$

or

$$
R=\frac{10^{6}}{(2000)(0.125)}=4000 \Omega
$$

b) From the solution of Example 8.4, we know that $v\left(0^{+}\right)=0$ and $d v\left(0^{+}\right) / d t=98,000 \mathrm{~V} / \mathrm{s}$. From Eqs. 8.35 and $8.36, D_{2}=0$ and $D_{1}=98,000 \mathrm{~V} / \mathrm{s}$.

Substituting these values for a, $D_{1}$, and $D_{2}$ into Eq. 8.34 gives

$$
v(t)=98,000 t e^{-1000 t} \mathrm{~V}, \quad t \geq 0
$$

c) Figure 8.10 shows a plot of $v(t)$ versus $t$ in the interval $0 \leq t \leq 7 \mathrm{~ms}$.
image_name:Figure 8.10
description:The graph in Figure 8.10 is a time-domain waveform plot illustrating the voltage response \( v(t) \) over time \( t \). The x-axis represents time in milliseconds (ms), ranging from 0 to 7 ms. The y-axis represents voltage \( v(t) \) in volts (V), with markings at intervals of 8 V, ranging from 0 V to 40 V.

The graph shows an exponential decay behavior typical of a critically damped response in a parallel RLC circuit. Initially, the voltage rises sharply, reaching a peak slightly above 40 V at around 1 ms. After this peak, the voltage decreases exponentially towards zero, with no oscillations, indicating a critically damped system.

Key features include:
- A peak voltage of slightly over 40 V occurring at approximately 1 ms.
- A smooth, continuous decline in voltage from the peak, trending towards zero as time progresses.

This behavior is consistent with the voltage function \( v(t) = 98,000 t e^{-1000 t} \) V, as described in the context, where the initial derivative value \( \frac{dv}{dt}(0^+) = 98,000 \) V/s contributes to the sharp rise at the beginning.

Figure 8.10 $\Delta$ The voltage response for Example 8.5.

ASSESSMENT PROBLEM

Objective 1-Be able to determine the natural and the step response of parallel RLC circuits
8.5 The resistor in the circuit in Assessment Problem 8.4 is adjusted for critical damping. The inductance and capacitance values are 0.4 H and $10 \mu \mathrm{~F}$, respectively. The initial energy stored in the circuit is 25 mJ and is distributed equally between the inductor and capacitor. Find (a) $R$; (b) $V_{0}$; (c) $I_{0}$; (d) $D_{1}$ and $D_{2}$ in the solution for $v$; and (e) $i_{R}, t \geq 0^{+}$.

Answer: (a) $100 \Omega$;
(b) 50 V ;
(c) 250 mA ;
(d) $-50,000 \mathrm{~V} / \mathrm{s}, 50 \mathrm{~V}$;
(e) $i_{R}(t)=\left(-500 t e^{-500 t}+0.50 e^{-500 t}\right) \mathrm{A}$, $t \geq 0^{+}$。

NOTE: Also try Chapter Problems 8.7 and 8.12.

A Summary of the Results

We conclude our discussion of the parallel $R L C$ circuit's natural response with a brief summary of the results. The first step in finding the natural response is to calculate the roots of the characteristic equation. You then know immediately whether the response is overdamped, underdamped, or critically damped.

If the roots are real and distinct $\left(\omega_{0}^{2}<\alpha^{2}\right)$, the response is overdamped and the voltage is

$$
v(t)=A_{1} e^{s_{1} t}+A_{2} e^{s_{2} t}
$$

where

$$
\begin{aligned}
s_{1} & =-\alpha+\sqrt{\alpha^{2}-\omega_{0}^{2}}, \\
s_{2} & =-\alpha-\sqrt{\alpha^{2}-\omega_{0}^{2}}, \\
\alpha & =\frac{1}{2 R C}, \\
\omega_{0}^{2} & =\frac{1}{L C} .
\end{aligned}
$$

The values of $A_{1}$ and $A_{2}$ are determined by solving the following simultaneous equations:

$$
\begin{aligned}
v\left(0^{+}\right) & =A_{1}+A_{2} \\
\frac{d v\left(0^{+}\right)}{d t} & =\frac{i_{C}\left(0^{+}\right)}{C}=s_{1} A_{1}+s_{2} A_{2}
\end{aligned}
$$

If the roots are complex $\omega_{0}^{2}>\alpha^{2}$ the response is underdamped and the voltage is

$$
v(t)=B_{1} e^{-\alpha t} \cos \omega_{d} t+B_{2} e^{-\alpha t} \sin \omega_{d} t
$$

where

$$
\omega_{d}=\sqrt{\omega_{0}^{2}-\alpha^{2}}
$$

The values of $B_{1}$ and $B_{2}$ are found by solving the following simultaneous equations:

$$
\begin{aligned}
v\left(0^{+}\right) & =V_{0}=B_{1} \\
\frac{d v\left(0^{+}\right)}{d t} & =\frac{i_{C}\left(0^{+}\right)}{C}=-\alpha B_{1}+\omega_{d} B_{2}
\end{aligned}
$$

If the roots of the characteristic equation are real and equal $\left(\omega_{0}^{2}=\alpha^{2}\right)$, the voltage response is

$$
v(t)=D_{1} t e^{-\alpha t}+D_{2} e^{-\alpha t}
$$

where $\alpha$ is as in the other solution forms. To determine values for the constants $D_{1}$ and $D_{2}$, solve the following simultaneous equations:

$$
\begin{aligned}
v\left(0^{+}\right) & =V_{0}=D_{2} \\
\frac{d v\left(0^{+}\right)}{d t} & =\frac{i_{C}\left(0^{+}\right)}{C}=D_{1}-\alpha D_{2}
\end{aligned}
$$

image_name:Figure 8.11
description:
[
'name': 'I', 'type': 'CurrentSource', 'value': 'I', 'ports': {'Np': 'GND', 'Nn': 'A'
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'A', 'Nn': 'GND'
'name': 'L', 'type': 'Inductor', 'value': 'L', 'ports': {'N1': 'A', 'N2': 'GND'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'A', 'N2': 'GND'
]
extrainfo:The circuit is a parallel RLC circuit with a current source I. The voltage across the components is labeled as v(t), and the current through each component is labeled as i_C, i_L, and i_R respectively. The circuit describes the step response of a parallel RLC circuit.

Figure $8.11 \triangle \mathrm{~A}$ circuit used to describe the step response of a parallel RLC circuit.

## 8.3 The Step Response of a Parallel RLC Circuit

Finding the step response of a parallel $R L C$ circuit involves finding the voltage across the parallel branches or the current in the individual branches as a result of the sudden application of a dc current source. There may or may not be energy stored in the circuit when the current source is applied. The task is represented by the circuit shown in Fig. 8.11. To develop a general approach to finding the step response of a secondorder circuit, we focus on finding the current in the inductive branch $\left(i_{L}\right)$. This current is of particular interest because it does not approach zero as $t$ increases. Rather, after the switch has been open for a long time, the inductor current equals the dc source current $I$. Because we want to focus on the technique for finding the step response, we assume that the initial energy stored in the circuit is zero. This assumption simplifies the calculations and doesn't alter the basic process involved. In Example 8.10 we will see how the presence of initially stored energy enters into the general procedure.

To find the inductor current $i_{L}$, we must solve a second-order differential equation equated to the forcing function $I$, which we derive as follows. From Kirchhoff's current law, we have

$$
i_{L}+i_{R}+i_{C}=I
$$

or

$$
\begin{equation*}
i_{L}+\frac{v}{R}+C \frac{d v}{d t}=I \tag{8.37}
\end{equation*}
$$

Because

$$
\begin{equation*}
v=L \frac{d i_{L}}{d t} \tag{8.38}
\end{equation*}
$$

we get

$$
\begin{equation*}
\frac{d v}{d t}=L \frac{d^{2} i_{L}}{d t^{2}} \tag{8.39}
\end{equation*}
$$

Substituting Eqs. 8.38 and 8.39 into Eq. 8.37 gives

$$
\begin{equation*}
i_{L}+\frac{L}{R} \frac{d i_{L}}{d t}+L C \frac{d^{2} i_{L}}{d t^{2}}=I \tag{8.40}
\end{equation*}
$$

For convenience, we divide through by $L C$ and rearrange terms:

$$
\begin{equation*}
\frac{d^{2} i_{L}}{d t^{2}}+\frac{1}{R C} \frac{d i_{L}}{d t}+\frac{i_{L}}{L C}=\frac{I}{L C} \tag{8.41}
\end{equation*}
$$

Comparing Eq. 8.41 with Eq. 8.3 reveals that the presence of a nonzero term on the right-hand side of the equation alters the task. Before showing how to solve Eq. 8.41 directly, we obtain the solution indirectly. When we know the solution of Eq. 8.41, explaining the direct approach will be easier.

The Indirect Approach

We can solve for $i_{L}$ indirectly by first finding the voltage $v$. We do this with the techniques introduced in Section 8.2, because the differential equation that $v$ must satisfy is identical to Eq. 8.3. To see this, we simply return to Eq. 8.37 and express $i_{L}$ as a function of $v$; thus

$$
\begin{equation*}
\frac{1}{L} \int_{0}^{t} v d \tau+\frac{v}{R}+C \frac{d v}{d t}=I \tag{8.42}
\end{equation*}
$$

Differentiating Eq. 8.42 once with respect to $t$ reduces the right-hand side to zero because $I$ is a constant. Thus

$$
\frac{v}{L}+\frac{1}{R} \frac{d v}{d t}+C \frac{d^{2} v}{d t^{2}}=0
$$

or

$$
\begin{equation*}
\frac{d^{2} v}{d t^{2}}+\frac{1}{R C} \frac{d v}{d t}+\frac{v}{L C}=0 \tag{8.43}
\end{equation*}
$$

As discussed in Section 8.2, the solution for $v$ depends on the roots of the characteristic equation. Thus the three possible solutions are

$$
\begin{align*}
& v=A_{1} e^{s_{1} t}+A_{2} e^{s_{2} t}  \tag{8.44}\\
& v=B_{1} e^{-\alpha t} \cos \omega_{d} t+B_{2} e^{-\alpha t} \sin \omega_{d} t  \tag{8.45}\\
& v=D_{1} t e^{-\alpha t}+D_{2} e^{-\alpha t} \tag{8.46}
\end{align*}
$$

A word of caution: Because there is a source in the circuit for $t>0$, you must take into account the value of the source current at $t=0^{+}$when you evaluate the coefficients in Eqs. 8.44-8.46.

To find the three possible solutions for $i_{L}$, we substitute Eqs. 8.44-8.46 into Eq. 8.37. You should be able to verify, when this has been done, that the three solutions for $i_{L}$ will be

$$
\begin{align*}
& i_{L}=I+A_{1}^{\prime} e^{s_{1} t}+A_{2}^{\prime} e^{s_{2} t}  \tag{8.47}\\
& i_{L}=I+B_{1}^{\prime} e^{-\alpha t} \cos \omega_{d} t+B_{2}^{\prime} e^{-\alpha t} \sin \omega_{d} t  \tag{8.48}\\
& i_{L}=I+D_{1}^{\prime} t e^{-\alpha t}+D_{2}^{\prime} e^{-\alpha t} \tag{8.49}
\end{align*}
$$

where $A_{1}^{\prime}, A_{2}^{\prime}, B_{1}^{\prime}, B_{2}^{\prime}, D_{1}^{\prime}$, and $D_{2}^{\prime}$, are arbitrary constants.
In each case, the primed constants can be found indirectly in terms of the arbitrary constants associated with the voltage solution. However, this approach is cumbersome.

The Direct Approach

It is much easier to find the primed constants directly in terms of the initial values of the response function. For the circuit being discussed, we would find the primed constants from $i_{L}(0)$ and $d i_{L}(0) / d t$.

The solution for a second-order differential equation with a constant forcing function equals the forced response plus a response function
identical in form to the natural response. Thus we can always write the solution for the step response in the form

$$
i=I_{f}+\left\{\begin{array}{c}
\text { function of the same form }  \tag{8.50}\\
\text { as the natural response }
\end{array}\right\}
$$

or

$$
v=V_{f}+\left\{\begin{array}{r}
\text { function of the same form }  \tag{8.51}\\
\text { as the natural response }
\end{array}\right\}
$$

where $I_{f}$ and $V_{f}$ represent the final value of the response function. The final value may be zero, as was, for example, the case with the voltage $v$ in the circuit in Fig. 8.8.

Examples 8.6-8.10 illustrate the technique of finding the step response of a parallel $R L C$ circuit using the direct approach.

#### Example 8.6 Finding the Overdamped Step Response of a Parallel RLC Circuit

The initial energy stored in the circuit in Fig. 8.12 is zero. At $t=0$, a dc current source of 24 mA is applied to the circuit. The value of the resistor is $400 \Omega$.
a) What is the initial value of $i_{L}$ ?
b) What is the initial value of $d i_{L} / d t$ ?
c) What are the roots of the characteristic equation?
d) What is the numerical expression for $i_{L}(t)$ when $t \geq 0$ ?

image_name:Figure 8.12
description:
[
'name': 'I', 'type': 'CurrentSource', 'value': 'I', 'ports': {'Np': 'GND', 'Nn': 'V'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'V', 'N2': 'GND'
'name': 'C', 'type': 'Capacitor', 'value': '25nF', 'ports': {'Np': 'V', 'Nn': 'GND'
'name': 'L', 'type': 'Inductor', 'value': '25mH', 'ports': {'N1': 'V', 'N2': 'GND'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'V', 'N2': 'GND'
]
extrainfo:The circuit is a parallel RLC circuit with a DC current source. The switch SW1 is initially open. The initial energy stored in the circuit is zero. The resistor has a value of 400 Ω.
Figure 8.12 A The circuit for Example 8.6.

#### Solution

a) No energy is stored in the circuit prior to the application of the dc current source, so the initial current in the inductor is zero. The inductor prohibits an instantaneous change in inductor current; therefore $i_{L}(0)=0$ immediately after the switch has been opened.
b) The initial voltage on the capacitor is zero before the switch has been opened; therefore it will be zero immediately after. Now, because $v=L d i_{L} / d t$,

$$
\frac{d i_{L}}{d t}\left(0^{+}\right)=0
$$

c) From the circuit elements, we obtain

$$
\begin{aligned}
\omega_{0}^{2} & =\frac{1}{L C}=\frac{10^{12}}{(25)(25)}=16 \times 10^{8} \\
\alpha & =\frac{1}{2 R C}=\frac{10^{9}}{(2)(400)(25)}=5 \times 10^{4} \mathrm{rad} / \mathrm{s}
\end{aligned}
$$

or

$$
\alpha^{2}=25 \times 10^{8}
$$

Because $\omega_{0}^{2}<\alpha^{2}$, the roots of the characteristic equation are real and distinct. Thus

$$
\begin{aligned}
& s_{1}=-5 \times 10^{4}+3 \times 10^{4}=-20,000 \mathrm{rad} / \mathrm{s} \\
& s_{2}=-5 \times 10^{4}-3 \times 10^{4}=-80,000 \mathrm{rad} / \mathrm{s}
\end{aligned}
$$

d) Because the roots of the characteristic equation are real and distinct, the inductor current response will be overdamped. Thus $i_{L}(t)$ takes the form of Eq. 8.47, namely,

$$
i_{L}=I_{f}+A_{1}^{\prime} e^{s_{1} t}+A_{2}^{\prime} e^{s_{2} t}
$$
Inductor current in overdamped parallel RLC circuit step response

Hence, from this solution, the two simultaneous equations that determine $A_{1}^{\prime}$ and $A_{2}^{\prime}$ are

$$
\begin{aligned}
i_{L}(0) & =I_{f}+A_{1}^{\prime}+A_{2}^{\prime}=0 \\
\frac{d i_{L}}{d t}(0) & =s_{1} A_{1}^{\prime}+s_{2} A_{2}^{\prime}=0
\end{aligned}
$$

Solving for $A_{1}^{\prime}$ and $A_{2}^{\prime}$ gives

$$
A_{1}^{\prime}=-32 \mathrm{~mA} \quad \text { and } \quad A_{2}^{\prime}=8 \mathrm{~mA}
$$

The numerical solution for $i_{L}(t)$ is

$$
i_{L}(t)=\left(24-32 e^{-20,000 t}+8 e^{-80,000 t}\right) \mathrm{mA}, \quad t \geq 0
$$

#### Example 8.7 Finding the Underdamped Step Response of a Parallel RLC Circuit

The resistor in the circuit in Example 8.6 (Fig. 8.12) is increased to $625 \Omega$. Find $i_{L}(t)$ for $t \geq 0$.

#### Solution

Because $L$ and $C$ remain fixed, $\omega_{0}^{2}$ has the same value as in Example 8.6; that is, $\omega_{0}^{2}=16 \times 10^{8}$. Increasing $R$ to $625 \Omega$ decreases $\alpha$ to $3.2 \times 10^{4} \mathrm{rad} / \mathrm{s}$. With $\omega_{0}^{2}>\alpha^{2}$, the roots of the characteristic equation are complex. Hence

$$
\begin{aligned}
& s_{1}=-3.2 \times 10^{4}+j 2.4 \times 10^{4} \mathrm{rad} / \mathrm{s} \\
& s_{2}=-3.2 \times 10^{4}-j 2.4 \times 10^{4} \mathrm{rad} / \mathrm{s}
\end{aligned}
$$

The current response is now underdamped and given by Eq. 8.48:

$$
i_{L}(t)=I_{f}+B_{1}^{\prime} e^{-\alpha t} \cos \omega_{d} t+B_{2}^{\prime} e^{-\alpha t} \sin \omega_{d} t
$$

- Inductor current in underdamped parallel RLC circuit step response

Here, $\alpha$ is $32,000 \mathrm{rad} / \mathrm{s}, \omega_{d}$ is $24,000 \mathrm{rad} / \mathrm{s}$, and $I_{f}$ is 24 mA .

As in Example 8.6, $B_{1}^{\prime}$ and $B_{2}^{\prime}$ are determined from the initial conditions. Thus the two simultaneous equations are

$$
\begin{gathered}
i_{L}(0)=I_{f}+B_{1}^{\prime}=0 \\
\frac{d i_{L}}{d t}(0)=\omega_{d} B_{2}^{\prime}-\alpha B_{1}^{\prime}=0
\end{gathered}
$$

Then,

$$
B_{1}^{\prime}=-24 \mathrm{~mA}
$$

and

$$
B_{2}^{\prime}=-32 \mathrm{~mA}
$$

The numerical solution for $i_{L}(t)$ is

$$
\begin{aligned}
i_{L}(t)= & \left(24-24 e^{-32,000 t} \cos 24,000 t\right. \\
& \left.-32 e^{-32,000 t} \sin 24,000 t\right) \mathrm{mA}, \quad t \geq 0
\end{aligned}
$$

#### Example 8.8 Finding the Critically Damped Step Response of a Parallel RLC Circuit

The resistor in the circuit in Example 8.6 (Fig. 8.12) is set at $500 \Omega$. Find $i_{L}$ for $t \geq 0$.

#### Solution

We know that $\omega_{0}^{2}$ remains at $16 \times 10^{8}$. With $R$ set at $500 \Omega, \alpha$ becomes $4 \times 10^{4} \mathrm{~s}^{-1}$, which corresponds to critical damping. Therefore the solution for $i_{L}(t)$ takes the form of Eq. 8.49:

$$
i_{L}(t)=I_{f}+D_{1}^{\prime} t e^{-\alpha t}+D_{2}^{\prime} e^{-\alpha t}
$$

Again, $D_{1}^{\prime}$ and $D_{2}^{\prime}$ are computed from initial conditions, or

$$
i_{L}(0)=I_{f}+D_{2}^{\prime}=0
$$

$$
\frac{d i_{L}}{d t}(0)=D_{1}^{\prime}-\alpha D_{2}^{\prime}=0
$$

Thus

$$
D_{1}^{\prime}=-960,000 \mathrm{~mA} / \mathrm{s} \quad \text { and } \quad D_{2}^{\prime}=-24 \mathrm{~mA}
$$

The numerical expression for $i_{L}(t)$ is

$$
i_{L}(t)=\left(24-960,000 t e^{-40,000 t}-24 e^{-40,000 t}\right) \mathrm{mA}, t \geq 0
$$

#### Example 8.9 Comparing the Three-Step Response Forms

a) Plot on a single graph, over a range from 0 to $220 \mu \mathrm{~s}$, the overdamped, underdamped, and critically damped responses derived in Examples 8.6-8.8.
b) Use the plots of (a) to find the time required for $i_{L}$ to reach $90 \%$ of its final value.
c) On the basis of the results obtained in (b), which response would you specify in a design that puts a premium on reaching $90 \%$ of the final value of the output in the shortest time?
d) Which response would you specify in a design that must ensure that the final value of the current is never exceeded?

#### Solution

a) See Fig. 8.13.
b) The final value of $i_{L}$ is 24 mA , so we can read the times off the plots corresponding to $i_{L}=21.6 \mathrm{~mA}$. Thus $t_{o d}=130 \mu \mathrm{~s}, t_{c d}=97 \mu \mathrm{~s}$, and $t_{u d}=74 \mu \mathrm{~s}$.
c) The underdamped response reaches $90 \%$ of the final value in the fastest time, so it is the desired response type when speed is the most important design specification.
image_name:Figure 8.13
description:The graph shown is a time-domain waveform depicting the current, denoted as \( i_L \), measured in milliamperes (mA) over time \( t \), measured in microseconds (\( \mu s \)). The graph illustrates the response of an electrical circuit to different damping conditions: underdamped, critically damped, and overdamped.

1. **Axes Labels and Units:**
- The vertical axis represents the current \( i_L \) in milliamperes (mA), ranging from 0 to 26 mA.
- The horizontal axis represents time \( t \) in microseconds (\( \mu s \)), ranging from 0 to 180 \( \mu s \).

2. **Overall Behavior and Trends:**
- The graph shows three distinct curves, each representing a different damping condition of the circuit.
- **Underdamped Response (R = 625 Ω):** This curve exhibits an initial rapid increase, overshooting the final steady-state current value of 24 mA, before settling back down to the final value.
- **Critically Damped Response (R = 500 Ω):** This curve rises quickly to the final value without overshooting, reaching the final steady-state value more gradually compared to the underdamped response.
- **Overdamped Response (R = 400 Ω):** This curve shows a slower rise to the final steady-state value, without overshooting, and takes the longest time to reach the final value.

3. **Key Features and Technical Details:**
- The final steady-state current value is marked at 24 mA.
- For the underdamped response, the overshoot exceeds 24 mA, peaking slightly above this value before settling.
- The critically damped and overdamped responses do not exceed the final value of 24 mA.

4. **Annotations and Specific Data Points:**
- The plot includes dashed lines indicating specific time points where the responses reach significant portions of their final value. These are approximately at 74 \( \mu s \) for the underdamped, 97 \( \mu s \) for the critically damped, and 130 \( \mu s \) for the overdamped response.
- The annotations specify the resistance values (R) associated with each damping condition, highlighting how different resistances impact the circuit's response time and behavior.

Overall, the graph provides a clear comparison of how different damping conditions affect the transient response of the circuit, emphasizing the trade-offs between speed and overshoot in achieving the desired current level.

Figure 8.13 $\triangle$ The current plots for Example 8.9.

d) From the plot, you can see that the underdamped response overshoots the final value of current, whereas neither the critically damped nor the overdamped response produces currents in excess of 24 mA . Although specifying either of the latter two responses would meet the design specification, it is best to use the overdamped response. It would be impractical to require a design to achieve the exact component values that ensure a critically damped response.

#### Example 8.10 Finding Step Response of a Parallel RLC Circuit with Initial Stored Energy

Energy is stored in the circuit in Example 8.8 (Fig. 8.12, with $R=500 \Omega$ ) at the instant the dc current source is applied. The initial current in the inductor is 29 mA , and the initial voltage across the capacitor is 50 V . Find (a) $i_{L}(0)$; (b) $d i_{L}(0) / d t$; (c) $i_{L}(t)$ for $t \geq 0$; (d) $v(t)$ for $t \geq 0$.

#### Solution

a) There cannot be an instantaneous change of current in an inductor, so the initial value of $i_{L}$ in the first instant after the dc current source has been applied must be 29 mA .
b) The capacitor holds the initial voltage across the inductor to 50 V . Therefore

$$
\begin{aligned}
L \frac{d i_{L}}{d t}\left(0^{+}\right) & =50 \\
\frac{d i_{L}}{d t}\left(0^{+}\right) & =\frac{50}{25} \times 10^{3}=2000 \mathrm{~A} / \mathrm{s}
\end{aligned}
$$

c) From the solution of Example 8.8, we know that the current response is critically damped. Thus

$$
i_{L}(t)=I_{f}+D_{1}^{\prime} t e^{-\alpha t}+D_{2}^{\prime} e^{-\alpha t}
$$

where
$\alpha=\frac{1}{2 R C}=40,000 \mathrm{rad} / \mathrm{s} \quad$ and $\quad I_{f}=24 \mathrm{~mA}$.
Notice that the effect of the nonzero initial stored energy is on the calculations for the constants $D_{1}^{\prime}$ and $D_{2}^{\prime}$, which we obtain from the initial conditions. First we use the initial value of the inductor current:

$$
i_{L}(0)=I_{f}+D_{2}^{\prime}=29 \mathrm{~mA}
$$

from which we get

$$
D_{2}^{\prime}=29-24=5 \mathrm{~mA}
$$

The solution for $D_{1}^{\prime}$ is

$$
\frac{d i_{L}}{d t}\left(0^{+}\right)=D_{1}^{\prime}-\alpha D_{2}^{\prime}=2000
$$

or

$$
\begin{aligned}
D_{1}^{\prime} & =2000+\alpha D_{2}^{\prime} \\
& =2000+(40,000)\left(5 \times 10^{-3}\right) \\
& =2200 \mathrm{~A} / \mathrm{s}=2.2 \times 10^{6} \mathrm{~mA} / \mathrm{s}
\end{aligned}
$$

Thus the numerical expression for $i_{L}(t)$ is

$$
\begin{aligned}
i_{L}(t)= & \left(24+2.2 \times 10^{6} t e^{-40,000 t}\right. \\
& \left.+5 e^{-40,000 t}\right) \mathrm{mA}, \quad t \geq 0
\end{aligned}
$$

d) We can get the expression for $v(t), t \geq 0$ by using the relationship between the voltage and current in an inductor:
$v(t)=L \frac{d i_{L}}{d t}$

$$
\begin{aligned}
= & \left(25 \times 10^{-3}\right)\left[\left(2.2 \times 10^{6}\right)(-40,000) t e^{-40,000 t}\right. \\
& +2.2 \times 10^{6} e^{-40,000 t} \\
& \left.+(5)(-40,000) e^{-40,000 t}\right] \times 10^{-3} \\
= & -2.2 \times 10^{6} t e^{-40,000 t}+50 e^{-40,000 t} \mathrm{~V}, t \geq 0
\end{aligned}
$$

To check this result, let's verify that the initial voltage across the inductor is 50 V :

$$
v(0)=-2.2 \times 10^{6}(0)(1)+50(1)=50 \mathrm{~V}
$$

ASSESSMENT PROBLEM

Objective 1-Be able to determine the natural response and the step response of parallel RLC circuits

8.6 In the circuit shown, $R=500 \Omega, L=0.64 \mathrm{H}$, $C=1 \mu \mathrm{~F}$, and $I=-1 \mathrm{~A}$. The initial voltage drop across the capacitor is 40 V and the initial inductor current is 0.5 A . Find (a) $i_{R}\left(0^{+}\right)$;
(b) $i_{C}\left(0^{+}\right)$;
; (c) $d i_{L}\left(0^{+}\right) / d t$; (d)
(d) $s_{1}, s_{2}$; (e) $i_{L}(t)$ for
$t \geq 0$; and (f) $v(t)$ for $t \geq 0^{+}$.

description:
[
'name': 'I', 'type': 'CurrentSource', 'ports': {'Np': 'GND', 'Nn': 'V'
'name': 'SW', 'type': 'Switch', 'ports': {'N1': 'V', 'N2': 'GND'
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'V', 'Nn': 'GND'
'name': 'L', 'type': 'Inductor', 'value': 'L', 'ports': {'N1': 'V', 'N2': 'GND'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'V', 'N2': 'GND'
]
extrainfo:The circuit is a parallel RLC circuit with a current source, switch, capacitor, inductor, and resistor all connected to the same node labeled 'V'. The ground node is labeled as 'GND'. The switch is initially open at t=0.

Answer: (a) 80 mA ;
(b) -1.58 A ;
(c) $62.5 \mathrm{~A} / \mathrm{s}$;
(d) $(-1000+j 750) \mathrm{rad} / \mathrm{s}$, $(-1000-j 750) \mathrm{rad} / \mathrm{s}$;
(e) $\left[-1+e^{-1000 t}[1.5 \cos 750 t\right.$ $+2.0833 \sin 750 t] \mathrm{A}$, for $t \geq 0$;
(f) $e^{-1000 t}(40 \cos 750 t-2053.33 \sin 750 t) \mathrm{V}$, for $t \geq 0^{+}$.

## 8.4 The Natural and Step Response of a Series RLC Circuit

The procedures for finding the natural or step responses of a series $R L C$ circuit are the same as those used to find the natural or step responses of a parallel $R L C$ circuit, because both circuits are described by differential equations that have the same form. We begin by summing the voltages around the closed path in the circuit shown in Fig. 8.14. Thus

$$
\begin{equation*}
R i+L \frac{d i}{d t}+\frac{1}{C} \int_{0}^{t} i d \tau+V_{0}=0 \tag{8.52}
\end{equation*}
$$

We now differentiate Eq. 8.52 once with respect to $t$ to get

$$
\begin{equation*}
R \frac{d i}{d t}+L \frac{d^{2} i}{d t^{2}}+\frac{i}{C}=0 \tag{8.53}
\end{equation*}
$$

image_name:Figure 8.14
description:
[
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'GND', 'N2': 'X'
'name': 'L', 'type': 'Inductor', 'value': 'L', 'ports': {'N1': 'X', 'N2': 'Vo'
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'Vo', 'Nn': 'GND'
]
extrainfo:This is a series RLC circuit. The circuit is used to illustrate the natural response of a series RLC circuit.

Figure 8.14 $\triangle \mathrm{A}$ circuit used to illustrate the natural response of a series RLC circuit.

Characteristic equation-series RLC circuit -

Neper frequency—series RLC circuit

Resonant radian frequency—series RLC circuit

Current natural response forms in series RLC circuits F

image_name:Figure 8.15
description:
[
'name': 'V', 'type': 'VoltageSource', 'value': 'V', 'ports': {'Np': 'V', 'Nn': 'GND'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'V', 'N2': 'X2'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'X2', 'N2': 'X1'
'name': 'L', 'type': 'Inductor', 'value': 'L', 'ports': {'N1': 'X1', 'N2': 'VC'
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'VC', 'Nn': 'GND'
]
extrainfo:This is a step response circuit for a series RLC circuit with a voltage source V, a switch SW1, a resistor R, an inductor L, and a capacitor C. The circuit is used to analyze the transient response when the switch is closed at t=0.
Figure $8.15 \triangle \mathrm{~A}$ circuit used to illustrate the step response of a series $R L C$ circuit.
which we can rearrange as

$$
\begin{equation*}
\frac{d^{2} i}{d t^{2}}+\frac{R}{L} \frac{d i}{d t}+\frac{i}{L C}=0 \tag{8.54}
\end{equation*}
$$

Comparing Eq. 8.54 with Eq. 8.3 reveals that they have the same form. Therefore, to find the solution of Eq. 8.54, we follow the same process that led us to the solution of Eq. 8.3.

From Eq. 8.54, the characteristic equation for the series $R L C$ circuit is

$$
\begin{equation*}
s^{2}+\frac{R}{L} s+\frac{1}{L C}=0 \tag{8.55}
\end{equation*}
$$

The roots of the characteristic equation are

$$
\begin{equation*}
s_{1,2}=-\frac{R}{2 L} \pm \sqrt{\left(\frac{R}{2 L}\right)^{2}-\frac{1}{L C}} \tag{8.56}
\end{equation*}
$$

or

$$
\begin{equation*}
s_{1,2}=-\alpha \pm \sqrt{\alpha^{2}-\omega_{0}^{2}} \tag{8.57}
\end{equation*}
$$

The neper frequency $(\alpha)$ for the series $R L C$ circuit is

$$
\begin{equation*}
\alpha=\frac{R}{2 L} \mathrm{rad} / \mathrm{s} \tag{8.58}
\end{equation*}
$$

and the expression for the resonant radian frequency is

$$
\begin{equation*}
\omega_{0}=\frac{1}{\sqrt{L C}} \mathrm{rad} / \mathrm{s} \tag{8.59}
\end{equation*}
$$

Note that the equation for neper frequency of the series $R L C$ circuit differs from that of the parallel $R L C$ circuit, but the equations for resonant and damped radian frequencies are the same.

The current response will be overdamped, underdamped, or critically damped according to whether $\omega_{0}^{2}<\alpha^{2}, \omega_{0}^{2}>\alpha^{2}$, or $\omega_{0}^{2}=\alpha^{2}$, respectively. Thus the three possible solutions for the current are as follows:

$$
\begin{align*}
& i(t)=A_{1} e^{s_{1} t}+A_{2} e^{s_{2} t} \text { (overdamped) }  \tag{8.60}\\
& i(t)=B_{1} e^{-\alpha t} \cos \omega_{d} t+B_{2} e^{-\alpha t} \sin \omega_{d} t \text { (underdamped) }  \tag{8.61}\\
& i(t)=D_{1} t e^{-\alpha t}+D_{2} e^{-\alpha t} \text { (critically damped). } \tag{8.62}
\end{align*}
$$

When you have obtained the natural current response, you can find the natural voltage response across any circuit element.

To verify that the procedure for finding the step response of a series $R L C$ circuit is the same as that for a parallel $R L C$ circuit, we show that the differential equation that describes the capacitor voltage in Fig. 8.15 has the same form as the differential equation that describes the inductor current in Fig. 8.11. For convenience, we assume that zero energy is stored in the circuit at the instant the switch is closed.

Applying Kirchhoff's voltage law to the circuit shown in Fig. 8.15 gives

$$
\begin{equation*}
V=R i+L \frac{d i}{d t}+v_{C} \tag{8.63}
\end{equation*}
$$

The current $(i)$ is related to the capacitor voltage $\left(v_{C}\right)$ by the expression

$$
\begin{equation*}
i=C \frac{d v_{C}}{d t} \tag{8.64}
\end{equation*}
$$

from which

$$
\begin{equation*}
\frac{d i}{d t}=C \frac{d^{2} v_{C}}{d t^{2}} \tag{8.65}
\end{equation*}
$$

Substitute Eqs. 8.64 and 8.65 into Eq. 8.63 and write the resulting expression as

$$
\begin{equation*}
\frac{d^{2} v_{C}}{d t^{2}}+\frac{R}{L} \frac{d v_{C}}{d t}+\frac{v_{C}}{L C}=\frac{V}{L C} \tag{8.66}
\end{equation*}
$$

Equation 8.66 has the same form as Eq. 8.41; therefore the procedure for finding $v_{C}$ parallels that for finding $i_{L}$. The three possible solutions for $v_{C}$ are as follows:

$$
\begin{align*}
& v_{C}=V_{f}+A_{1}^{\prime} e^{s_{1} t}+A_{2}^{\prime} e^{s_{2} t}(\text { overdamped })  \tag{8.67}\\
& v_{C}=V_{f}+B_{1}^{\prime} e^{-\alpha t} \cos \omega_{d} t+B_{2}^{\prime} e^{-\alpha t} \sin \omega_{d} t \text { (underdamped) }  \tag{8.68}\\
& v_{C}=V_{f}+D_{1}^{\prime} t e^{-\alpha t}+D_{2}^{\prime} e^{-\alpha t} \quad(\text { critically damped }) \tag{8.69}
\end{align*}
$$

$\triangle$ Capacitor voltage step response forms in series RLC circuits
where $V_{f}$ is the final value of $v_{C}$. Hence, from the circuit shown in Fig. 8.15, the final value of $v_{C}$ is the dc source voltage $V$.

Example 8.11 and 8.12 illustrate the mechanics of finding the natural and step responses of a series $R L C$ circuit.

#### Example 8.11 Finding the Underdamped Natural Response of a Series RLC Circuit

The $0.1 \mu \mathrm{~F}$ capacitor in the circuit shown in Fig. 8.16 is charged to 100 V . At $t=0$ the capacitor is discharged through a series combination of a 100 mH inductor and a $560 \Omega$ resistor.
a) Find $i(t)$ for $t \geq 0$.
b) Find $v_{C}(t)$ for $t \geq 0$.
image_name:Figure 8.16
description:
[
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'Vi', 'N2': 'Vc'
'name': 'C1', 'type': 'Capacitor', 'value': '0.1uF', 'ports': {'Np': 'Vi', 'Nn': 'GND'
'name': 'L1', 'type': 'Inductor', 'value': '100mH', 'ports': {'N1': 'Vc', 'N2': 'Vo'
'name': 'R1', 'type': 'Resistor', 'value': '560Ω', 'ports': {'N1': 'Vo', 'N2': 'GND'
]
extrainfo:The circuit is a series RLC circuit used to study the underdamped natural response. The capacitor is initially charged to 100V and then discharged through the inductor and resistor.


Figure 8.16 $\triangle$ The circuit for Example 8.11.

#### Solution

a) The first step to finding $i(t)$ is to calculate the roots of the characteristic equation. For the given element values,

$$
\begin{aligned}
\omega_{0}^{2} & =\frac{1}{L C} \\
& =\frac{\left(10^{3}\right)\left(10^{6}\right)}{(100)(0.1)}=10^{8}, \\
\alpha & =\frac{R}{2 L} \\
& =\frac{560}{2(100)} \times 10^{3} \\
& =2800 \mathrm{rad} / \mathrm{s}
\end{aligned}
$$

Next, we compare $\omega_{0}^{2}$ to $\alpha^{2}$ and note that $\omega_{0}^{2}>\alpha^{2}$, because

$$
\begin{aligned}
\alpha^{2} & =7.84 \times 10^{6} \\
& =0.0784 \times 10^{8} .
\end{aligned}
$$

At this point, we know that the response is underdamped and that the solution for $i(t)$ is of the form

$$
i(t)=B_{1} e^{-\alpha t} \cos \omega_{d} t+B_{2} e^{-\alpha t} \sin \omega_{d} t
$$

where $\alpha=2800 \mathrm{rad} / \mathrm{s}$ and $\omega_{d}=9600 \mathrm{rad} / \mathrm{s}$. The numerical values of $B_{1}$ and $B_{2}$ come from the initial conditions. The inductor current is zero before the switch has been closed, and hence it is zero immediately after. Therefore

$$
i(0)=0=B_{1}
$$

To find $B_{2}$, we evaluate $d i\left(0^{+}\right) / d t$. From the circuit, we note that, because $i(0)=0$ immediately after the switch has been closed, there will be no voltage drop across the resistor. Thus the initial voltage on the capacitor appears across the terminals of the inductor, which leads to the expression,

$$
L \frac{d i\left(0^{+}\right)}{d t}=V_{0}
$$

or

$$
\begin{aligned}
\frac{d i\left(0^{+}\right)}{d t}=\frac{V_{0}}{L} & =\frac{100}{100} \times 10^{3} \\
& =1000 \mathrm{~A} / \mathrm{s}
\end{aligned}
$$

Because $B_{1}=0$,
$\frac{d i}{d t}=400 B_{2} e^{-2800 t}(24 \cos 9600 t-7 \sin 9600 t)$.
Thus

$$
\begin{aligned}
\frac{d i\left(0^{+}\right)}{d t} & =9600 B_{2} \\
B_{2} & =\frac{1000}{9600} \approx 0.1042 \mathrm{~A} .
\end{aligned}
$$

The solution for $i(t)$ is

$$
i(t)=0.1042 e^{-2800 t} \sin 9600 t \mathrm{~A}, \quad t \geq 0
$$

b) To find $v_{C}(t)$, we can use either of the following relationships:

$$
\begin{aligned}
& v_{C}=-\frac{1}{C} \int_{0}^{t} i d \tau+100 \text { or } \\
& v_{C}=i R+L \frac{d i}{d t}
\end{aligned}
$$

Whichever expression is used (the second is recommended), the result is
$v_{C}(t)=(100 \cos 9600 t+29.17 \sin 9600 t) e^{-2800 t} \mathrm{~V}, \quad t \geq 0$.

#### Example 8.12 Finding the Underdamped Step Response of a Series RLC Circuit

No energy is stored in the 100 mH inductor or the $0.4 \mu \mathrm{~F}$ capacitor when the switch in the circuit shown in Fig. 8.17 is closed. Find $v_{C}(t)$ for $t \geq 0$.
image_name:Figure 8.17
description:
[
'name': 'Vi', 'type': 'VoltageSource', 'value': '48V', 'ports': {'Np': 'Vi', 'Nn': 'GND'
'name': 't=0', 'type': 'Switch', 'ports': {'N1': 'Vi', 'N2': 'X1'
'name': '0.1 H', 'type': 'Inductor', 'value': '0.1 H', 'ports': {'N1': 'X1', 'N2': 'X2'
'name': '280 Ω', 'type': 'Resistor', 'value': '280 Ω', 'ports': {'N1': 'X2', 'N2': 'Vc'
'name': '0.4 μF', 'type': 'Capacitor', 'value': '0.4 μF', 'ports': {'Np': 'Vc', 'Nn': 'GND'
]
extrainfo:This is an RLC series circuit with a voltage source, switch, inductor, resistor, and capacitor. The voltage across the capacitor is denoted as vC.
Figure 8.17 $\triangle$ The circuit for Example 8.12.

#### Solution

The roots of the characteristic equation are

$$
\begin{aligned}
s_{1} & =-\frac{280}{0.2}+\sqrt{\left(\frac{280}{0.2}\right)^{2}-\frac{10^{6}}{(0.1)(0.4)}} \\
& =(-1400+j 4800) \mathrm{rad} / \mathrm{s} \\
s_{2} & =(-1400-j 4800) \mathrm{rad} / \mathrm{s}
\end{aligned}
$$

The roots are complex, so the voltage response is underdamped. Thus

$$
\begin{aligned}
v_{C}(t)= & 48+B_{1}^{\prime} e^{-1400 t} \cos 4800 t \\
& +B_{2}^{\prime} e^{-1400 t} \sin 4800 t, \quad t \geq 0
\end{aligned}
$$

No energy is stored in the circuit initially, so both $v_{C}(0)$ and $d v_{C}\left(0^{+}\right) / d t$ are zero. Then,

$$
\begin{aligned}
v_{C}(0) & =0=48+B_{1}^{\prime} \\
\frac{d v_{C}\left(0^{+}\right)}{d t} & =0=4800 B_{2}^{\prime}-1400 B_{1}^{\prime}
\end{aligned}
$$

Solving for $B_{1}^{\prime}$ and $B_{2}^{\prime}$ yields

$$
\begin{aligned}
& B_{1}^{\prime}=-48 \mathrm{~V} \\
& B_{2}^{\prime}=-14 \mathrm{~V}
\end{aligned}
$$

Therefore, the solution for $v_{C}(t)$ is

$$
\begin{aligned}
v_{C}(t)= & \left(48-48 e^{-1400 t} \cos 4800 t\right. \\
& \left.-14 e^{-1400 t} \sin 4800 t\right) \mathrm{V}, \quad t \geq 0
\end{aligned}
$$

ASSESSMENT PROBLEMS

Objective 2-Be able to determine the natural response and the step response of series RLC circuits
8.7 The switch in the circuit shown has been in position a for a long time. At $t=0$, it moves to position b. Find (a) $i\left(0^{+}\right)$; (b) $v_{C}\left(0^{+}\right)$;
(c) $d i\left(0^{+}\right) / d t$; (d) $s_{1}, s_{2}$; and (e) $i(t)$ for $t \geq 0$.

Answer: (a) 0;
(b) 50 V ;
(c) $10,000 \mathrm{~A} / \mathrm{s}$;
(d) $(-8000+j 6000) \mathrm{rad} / \mathrm{s}$, $(-8000-j 6000) \mathrm{rad} / \mathrm{s}$;
(e) $\left(1.67 e^{-8000 t} \sin 6000 t\right) \mathrm{A}$ for $t \geq 0$.

image_name:Figure 8.7
The circuit initially has the switch in position a, charging the capacitor C1 through resistors R1 and R2. At t=0, the switch moves to position b, connecting the inductor L1 and resistor R3 in series with the capacitor C1, forming an RLC circuit. The analysis involves solving for transient responses of current and voltage across components.

8.8 Find $v_{C}(t)$ for $t \geq 0$ for the circuit in Assessment Problem 8.7.

Answer: $\left[100-e^{-8000 t}(50 \cos 6000 t\right.$ $+66.67 \sin 6000 t)] \mathrm{V}$ for $t \geq 0$.

NOTE: Also try Chapter Problems 8.49-8.51.

## 8.5 A Circuit with Two Integrating Amplifiers

A circuit containing two integrating amplifiers connected in cascade ${ }^{1}$ is also a second-order circuit; that is, the output voltage of the second integrator is related to the input voltage of the first by a second-order differential equation. We begin our analysis of a circuit containing two cascaded amplifiers with the circuit shown in Fig. 8.18.
image_name:Figure 8.18
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'Vg', 'N2': 'InN(A0)'
'name': 'C1', 'type': 'Capacitor', 'value': 'C1', 'ports': {'Np': 'Vo1', 'Nn': 'InN(A0)'
'name': 'A0', 'type': 'OpAmp', 'value': 'A0', 'ports': {'InP': 'GND', 'InN': 'InN(A0)', 'OutP': 'Vo1', 'OutN': 'GND', 'Vdd': 'VCC', '-Vdd': '-VCC'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'Vo1', 'N2': 'InN(A1)'
'name': 'C2', 'type': 'Capacitor', 'value': 'C2', 'ports': {'Np': 'Vo', 'Nn': 'InN(A1)'
'name': 'A1', 'type': 'OpAmp', 'value': 'A1', 'ports': {'InP': 'GND', 'InN': 'InN(A1)', 'OutP': 'Vo', 'OutN': 'GND', 'Vdd': 'VCC', '-Vdd': '-VCC'
]
extrainfo:The circuit consists of two cascaded integrating amplifiers using ideal op-amps. The input voltage Vg is integrated twice to produce the output voltage Vo, forming a second-order system.


Figure 8.18 $\triangle$ Two integrating amplifiers connected in cascade.

We assume that the op amps are ideal. The task is to derive the differential equation that establishes the relationship between $v_{o}$ and $v_{g}$. We begin the derivation by summing the currents at the inverting input terminal of the first integrator. Because the op amp is ideal,

$$
\begin{equation*}
\frac{0-v_{g}}{R_{1}}+C_{1} \frac{d}{d t}\left(0-v_{o 1}\right)=0 \tag{8.70}
\end{equation*}
$$

From Eq. 8.70,

$$
\begin{equation*}
\frac{d v_{o 1}}{d t}=-\frac{1}{R_{1} C_{1}} v_{g} \tag{8.71}
\end{equation*}
$$

[^2]Now we sum the currents away from the inverting input terminal of the second integrating amplifier:

$$
\begin{equation*}
\frac{0-v_{o 1}}{R_{2}}+C_{2} \frac{d}{d t}\left(0-v_{o}\right)=0 \tag{8.72}
\end{equation*}
$$

or

$$
\begin{equation*}
\frac{d v_{o}}{d t}=-\frac{1}{R_{2} C_{2}} v_{o 1} \tag{8.73}
\end{equation*}
$$

Differentiating Eq. 8.73 gives

$$
\begin{equation*}
\frac{d^{2} v_{o}}{d t^{2}}=-\frac{1}{R_{2} C_{2}} \frac{d v_{o 1}}{d t} \tag{8.74}
\end{equation*}
$$

We find the differential equation that governs the relationship between $v_{o}$ and $v_{g}$ by substituting Eq. 8.71 into Eq. 8.74:

$$
\begin{equation*}
\frac{d^{2} v_{o}}{d t^{2}}=\frac{1}{R_{1} C_{1}} \frac{1}{R_{2} C_{2}} v_{g} \tag{8.75}
\end{equation*}
$$

Example 8.13 illustrates the step response of a circuit containing two cascaded integrating amplifiers.

#### Example 8.13 Analyzing Two Cascaded Integrating Amplifiers

No energy is stored in the circuit shown in Fig. 8.19 when the input voltage $v_{g}$ jumps instantaneously from 0 to 25 mV .
a) Derive the expression for $v_{o}(t)$ for $0 \leq t \leq t_{\text {sat }}$.
b) How long is it before the circuit saturates?

#### Solution

a) Figure 8.19 indicates that the amplifier scaling factors are

$$
\begin{aligned}
& \frac{1}{R_{1} C_{1}}=\frac{1000}{(250)(0.1)}=40 \\
& \frac{1}{R_{2} C_{2}}=\frac{1000}{(500)(1)}=2
\end{aligned}
$$

Now, because $v_{g}=25 \mathrm{mV}$ for $t>0$, Eq. 8.75 becomes

$$
\frac{d^{2} v_{o}}{d t^{2}}=(40)(2)\left(25 \times 10^{-3}\right)=2
$$

To solve for $v_{o}$, we let

$$
g(t)=\frac{d v_{o}}{d t}
$$

then,

$$
\frac{d g(t)}{d t}=2, \quad \text { and } \quad d g(t)=2 d t
$$

image_name:Figure 8.19
description:
[
'name': '250 kΩ', 'type': 'Resistor', 'value': '250 kΩ', 'ports': {'N1': 'Vg', 'N2': 'InN(A0)'
'name': 'Ao', 'type': 'OpAmp', 'value': 'Ao', 'ports': {'InP': 'GND', 'InN': 'InN(A0)', 'OutP': 'vo1', 'OutN': 'GND', 'Vdd': '5V', '-Vdd': '-5V'
'name': '0.1 μF', 'type': 'Capacitor', 'value': '0.1 μF', 'ports': {'Np': 'InN(A0)', 'Nn': 'vo1'
'name': '500 kΩ', 'type': 'Resistor', 'value': '500 kΩ', 'ports': {'N1': 'InN(A1)', 'N2': 'vo1'
'name': 'A1', 'type': 'OpAmp', 'value': 'A1', 'ports': {'InP': 'GND', 'InN': 'InN(A1)', 'OutP': 'vo', 'OutN': 'GND', 'Vdd': '9V', '-Vdd': '-9V'
'name': '1 μF', 'type': 'Capacitor', 'value': '1 μF', 'ports': {'Np': 'InN(A0)', 'Nn': 'Vo'
]
extrainfo:The circuit consists of two operational amplifiers (A0 and A1) configured with feedback loops. The first stage is a differentiator with a resistor and capacitor creating a high-pass filter. The second stage is similar, providing further amplification and filtering. The capacitors and resistors set the time constants for the circuit's response.


Figure 8.19 $\boldsymbol{\Delta}$ The circuit for Example 8.13.

Hence

$$
\int_{g(0)}^{g(t)} d y=2 \int_{0}^{t} d x
$$

from which

$$
g(t)-g(0)=2 t
$$

However,

$$
g(0)=\frac{d v_{o}(0)}{d t}=0
$$

because the energy stored in the circuit initially is zero, and the op amps are ideal. (See Problem 8.57.) Then,

$$
\frac{d v_{o}}{d t}=2 t, \quad \text { and } \quad v_{o}=t^{2}+v_{o}(0)
$$

But $v_{o}(0)=0$, so the experssion for $v_{o}$ becomes

$$
v_{o}=t^{2}, \quad 0 \leq t \leq t_{\mathrm{sat}} .
$$

b) The second integrating amplifier saturates when $v_{o}$ reaches 9 V or $t=3 \mathrm{~s}$. But it is possible that the first integrating amplifier saturates before $t=3 \mathrm{~s}$. To explore this possibility, use Eq. 8.71 to find $d v_{o 1} / d t$ :

$$
\frac{d v_{o 1}}{d t}=-40(25) \times 10^{-3}=-1
$$

Solving for $v_{o 1}$ yields

$$
v_{o 1}=-t
$$

Thus, at $t=3 \mathrm{~s}, v_{o 1}=-3 \mathrm{~V}$, and, because the power supply voltage on the first integrating amplifier is $\pm 5 \mathrm{~V}$, the circuit reaches saturation when the second amplifier saturates. When one of the op amps saturates, we no longer can use the linear model to predict the behavior of the circuit.

NOTE: Assess your understanding of this material by trying Chapter Problem 8.63.

Two Integrating Amplifiers with Feedback Resistors

Figure 8.20 depicts a variation of the circuit shown in Fig. 8.18. Recall from Section 7.7 that the reason the op amp in the integrating amplifier saturates is the feedback capacitor's accumulation of charge. Here, a resistor is placed in parallel with each feedback capacitor ( $C_{1}$ and $C_{2}$ ) to overcome this problem. We rederive the equation for the output voltage, $v_{o}$, and determine the impact of these feedback resistors on the integrating amplifiers from Example 8.13.

We begin the derivation of the second-order differential equation that relates $v_{o 1}$ to $v_{g}$ by summing the currents at the inverting input node of the first integrator:

$$
\begin{equation*}
\frac{0-v_{g}}{R_{\mathrm{a}}}+\frac{0-v_{o 1}}{R_{1}}+C_{1} \frac{d}{d t}\left(0-v_{o 1}\right)=0 \tag{8.76}
\end{equation*}
$$

We simplify Eq. 8.76 to read

$$
\begin{equation*}
\frac{d v_{o 1}}{d t}+\frac{1}{R_{1} C_{1}} v_{o 1}=\frac{-v_{g}}{R_{\mathrm{a}} C_{1}} \tag{8.77}
\end{equation*}
$$

For convenience, we let $\tau_{1}=R_{1} C_{1}$ and write Eq. 8.77 as

$$
\begin{equation*}
\frac{d v_{o 1}}{d t}+\frac{v_{o 1}}{\tau_{1}}=\frac{-v_{g}}{R_{\mathrm{a}} C_{1}} \tag{8.78}
\end{equation*}
$$

The next step is to sum the currents at the inverting input terminal of the second integrator:

$$
\begin{equation*}
\frac{0-v_{o 1}}{R_{\mathrm{b}}}+\frac{0-v_{o}}{R_{2}}+C_{2} \frac{d}{d t}\left(0-v_{o}\right)=0 \tag{8.79}
\end{equation*}
$$

image_name:Figure 8.20
description:
[
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'Vo1', 'N2': 'InN(Ao)'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'Vo', 'N2': 'InN(Aj)'
'name': 'Ra', 'type': 'Resistor', 'value': 'Ra', 'ports': {'N1': 'Vg', 'N2': 'InN(Ao)'
'name': 'Rb', 'type': 'Resistor', 'value': 'Rb', 'ports': {'N1': 'Vo1', 'N2': 'InN(Aj)'
'name': 'C1', 'type': 'Capacitor', 'value': 'C1', 'ports': {'Np': 'Vo1', 'Nn': 'InN(Ao)'
'name': 'C2', 'type': 'Capacitor', 'value': 'C2', 'ports': {'Np': 'Vo', 'Nn': 'InN(Aj)'
'name': 'Ao', 'type': 'OpAmp', 'value': 'Ao', 'ports': {'InP': 'GND', 'InN': 'InN(Ao)', 'OutP': 'Vo1', 'OutN': 'GND', 'Vdd': 'VCC1', '-Vdd': '-VCC1'
'name': 'Aj', 'type': 'OpAmp', 'value': 'Aj', 'ports': {'InP': 'GND', 'InN': 'InN(Aj)', 'OutP': 'Vo', 'OutN': 'GND', 'Vdd': 'VCC2', '-Vdd': '-VCC2'
]
extrainfo:The circuit consists of two cascaded integrating amplifiers with feedback resistors. The first stage uses an op-amp Ao with feedback components R1 and C1, integrating the input signal Vg to produce output Vo1. The second stage uses an op-amp Aj with feedback components R2 and C2, integrating Vo1 to produce the final output Vo.


Figure 8.20 ⓐscaded integrating amplifiers with feedback resistors.

$$
\begin{equation*}
\frac{d v_{o}}{d t}+\frac{v_{o}}{\tau_{2}}=\frac{-v_{o 1}}{R_{\mathrm{b}} C_{2}} \tag{8.80}
\end{equation*}
$$

where $\tau_{2}=R_{2} C_{2}$. Differentiating Eq. 8.80 yields

$$
\begin{equation*}
\frac{d^{2} v_{o}}{d t^{2}}+\frac{1}{\tau_{2}} \frac{d v_{o}}{d t}=-\frac{1}{R_{\mathrm{b}} C_{2}} \frac{d v_{o 1}}{d t} \tag{8.81}
\end{equation*}
$$

From Eq. 8.78,

$$
\begin{equation*}
\frac{d v_{o 1}}{d t}=\frac{-v_{o 1}}{\tau_{1}}-\frac{v_{g}}{R_{\mathrm{a}} C_{1}} \tag{8.82}
\end{equation*}
$$

and from Eq. 8.80,

$$
\begin{equation*}
v_{o 1}=-R_{\mathrm{b}} C_{2} \frac{d v_{o}}{d t}-\frac{R_{\mathrm{b}} C_{2}}{\tau_{2}} v_{o} \tag{8.83}
\end{equation*}
$$

We use Eqs. 8.82 and 8.83 to eliminate $d v_{o 1} / d t$ from Eq. 8.81 and obtain the desired relationship:

$$
\begin{equation*}
\frac{d^{2} v_{o}}{d t^{2}}+\left(\frac{1}{\tau_{1}}+\frac{1}{\tau_{2}}\right) \frac{d v_{o}}{d t}+\left(\frac{1}{\tau_{1} \tau_{2}}\right) v_{o}=\frac{v_{g}}{R_{\mathrm{a}} C_{1} R_{\mathrm{b}} C_{2}} \tag{8.84}
\end{equation*}
$$

From Eq. 8.84, the characteristic equation is

$$
\begin{equation*}
s^{2}+\left(\frac{1}{\tau_{1}}+\frac{1}{\tau_{2}}\right) s+\frac{1}{\tau_{1} \tau_{2}}=0 \tag{8.85}
\end{equation*}
$$

The roots of the characteristic equation are real, namely,

$$
\begin{align*}
& s_{1}=\frac{-1}{\tau_{1}}  \tag{8.86}\\
& s_{2}=\frac{-1}{\tau_{2}} \tag{8.87}
\end{align*}
$$

Example 8.14 illustrates the analysis of the step response of two cascaded integrating amplifiers when the feedback capacitors are shunted with feedback resistors.

#### Example 8.14 Analyzing Two Cascaded Integrating Amplifiers with Feedback Resistors

The parameters for the circuit shown in Fig. 8.20 are $\quad R_{\mathrm{a}}=100 \mathrm{k} \Omega, \quad R_{1}=500 \mathrm{k} \Omega, \quad C_{1}=0.1 \mu \mathrm{~F}$, $R_{\mathrm{b}}=25 \mathrm{k} \Omega, R_{2}=100 \mathrm{k} \Omega$, and $C_{2}=1 \mu \mathrm{~F}$. The power supply voltage for each op amp is $\pm 6 \mathrm{~V}$. The signal voltage $\left(v_{g}\right)$ for the cascaded integrating amplifiers jumps from 0 to 250 mV at $t=0$. No energy is stored in the feedback capacitors at the instant the signal is applied.
a) Find the numerical expression of the differential equation for $v_{o}$.
b) Find $v_{o}(t)$ for $t \geq 0$.
c) Find the numerical expression of the differential equation for $v_{o 1}$.
d) Find $v_{o 1}(t)$ for $t \geq 0$.

#### Solution

a) From the numerical values of the circuit parameters, we have $\tau_{1}=R_{1} C_{1}=0.05 \mathrm{~s} ; \tau_{2}=R_{2} C_{2}$ $=0.10 \mathrm{~s}$, and $v_{g} / R_{\mathrm{a}} C_{1} R_{\mathrm{b}} C_{2}=1000 \mathrm{~V} / \mathrm{s}^{2}$. Substituting these values into Eq. 8.84 gives

$$
\frac{d^{2} v_{o}}{d t^{2}}+30 \frac{d v_{o}}{d t}+200 v_{o}=1000
$$

b) The roots of the characteristic equation are $s_{1}=-20 \mathrm{rad} / \mathrm{s}$ and $s_{2}=-10 \mathrm{rad} / \mathrm{s}$. The final value of $v_{o}$ is the input voltage times the gain of each stage, because the capacitors behave as open circuits as $t \rightarrow \infty$. Thus,
$v_{o}(\infty)=\left(250 \times 10^{-3}\right) \frac{(-500)}{100} \frac{(-100)}{25}=5 \mathrm{~V}$.

The solution for $v_{o}$ thus takes the form:

$$
v_{o}=5+A_{1}^{\prime} e^{-10 t}+A_{2}^{\prime} e^{-20 t}
$$

With $v_{o}(0)=0$ and $d v_{o}(0) / d t=0$, the numerical values of $A_{1}^{\prime}$ and $A_{2}^{\prime}$ are $A_{1}^{\prime}=-10 \mathrm{~V}$ and $A_{2}^{\prime}=5 \mathrm{~V}$. Therefore, the solution for $v_{o}$ is

$$
v_{o}(t)=\left(5-10 e^{-10 t}+5 e^{-20 t}\right) \mathrm{V}, \quad t \geq 0
$$

The solution assumes that neither op amp saturates. We have already noted that the final value of $v_{o}$ is 5 V , which is less than 6 V ; hence the second op amp does not saturate. The final value of $v_{o 1}$ is $\left(250 \times 10^{-3}\right)(-500 / 100)$, or -1.25 V . Therefore, the first op amp does not saturate, and our assumption and solution are correct.
c) Substituting the numerical values of the parameters into Eq. 8.78 generates the desired differential equation:

$$
\frac{d v_{o 1}}{d t}+20 v_{o 1}=-25
$$

d) We have already noted the initial and final values of $v_{o 1}$, along with the time constant $\tau_{1}$. Thus we write the solution in accordance with the technique developed in Section 7.4:

$$
\begin{aligned}
v_{o 1} & =-1.25+[0-(-1.25)] e^{-20 t} \\
& =-1.25+1.25 e^{-20 t} \mathrm{~V}, \quad t \geq 0
\end{aligned}
$$

NOTE: Assess your understanding of this material by trying Chapter Problem 8.64.

Practical Perspective

Clock for Computer Timing

Consider the circuit in Fig. 8.21, where the output is the voltage drop across the capacitor. For $t \geq 0$ this circuit looks like a series $R L C$ natural-response circuit of Fig. 8.3 without its resistor. When we analyze this $L C$ circuit, we will discover that its output is an undamped sinusoid, which could be used by a computer's clock generator instead of the typical quartz crystal oscillator. We will be able to specify the frequency of the clock by selecting appropriate values for the inductor and capacitor.
image_name:Figure 8.21
The circuit is an LC natural response circuit used to generate an undamped sinusoidal output. The switch SW1 connects node 'a' to 'Vo' at t=0, allowing the circuit to oscillate.


Figure 8.21 $\triangle$ An $L C$ natural response circuit.

Begin by writing the KVL equation for the circuit in Fig. 8.21, using the current $i$, for $t \geq 0$ :

$$
L \frac{d i(t)}{d t}+\frac{1}{C} \int_{0}^{t} i(x) d x=0
$$

To get rid of the integral term, integral both sides with respect to $t$ to get

$$
L \frac{d^{2} i(t)}{d t^{2}}+\frac{1}{C} i(t)=0
$$

The describing differential equation is thus

$$
\frac{d^{2} i(t)}{d t^{2}}+\frac{1}{L C} i(t)=0
$$

What mathematical function can be added to its second derivative to get zero? A sinusoid in the form $i(t)=A \cos \omega_{0} t$ will work:

$$
\frac{d^{2}}{d t^{2}} A \cos \omega_{0} t+\frac{1}{L C} A \cos \omega_{0} t=-\omega_{0}^{2} A \cos \omega_{0} t+\frac{1}{L C} A \cos \omega_{0} t=0
$$

This equation is satisfied when

$$
\omega_{0}^{2}=\frac{1}{L C} \quad \text { or when } \quad \omega_{0}=\sqrt{\frac{1}{L C}}
$$

The frequency $\omega_{0}$ is the familiar resonant radian frequency of both the series and parallel RLC circuits, whose units are radians/second. Note that the $L C$ circuit does not have a neper frequency, $\alpha$.

We choose the value of $A$ to satisfy the initial condition for the current in the inductor:

$$
i(0)=A \cos \omega_{0}(0)=\frac{V}{R} \quad \text { so } \quad A=\frac{V}{R}
$$

Therefore, the current for the circuit in Fig. 8.21 is

$$
i(t)=\frac{V}{R} \cos \omega_{0}(t), \quad \text { where } \omega_{0}=\sqrt{\frac{1}{L C}}
$$

We can now use the expression for the current in the circuit to find the voltage output by the capacitor:

$$
v_{C}(t)=\frac{1}{C} \int_{0}^{t} i(x) d x=\frac{1}{C} \int_{0}^{t} \frac{V}{R} \cos \omega_{0} x d x=\frac{V}{\omega_{0} R C} \sin \omega_{0} t
$$

By choosing values for $L$ and $C$ we can use the circuit in Fig. 8.21 to generate an undamped sinusoid for $t \geq 0$ for a computer's clock generator.

So why is a quartz crystal used to generate the sinusoid for the clock generator instead of the LC circuit of Fig. 8.21? Remember that our analysis of the $L C$ circuit assumed that the inductor and capacitor are ideal. But ideal inductors and capacitors do not exist - real inductors and capacitors have a small amount of resistance. We leave it to you to examine the effect of this small amount of resistance on the performance of an LC oscillator in the Chapter Problems.

NOTE: Assess your understanding of the Practical Perspective by solving Chapter Problems 8.66-8.68.

## Summary

- The characteristic equation for both the parallel and series $R L C$ circuits has the form

$$
s^{2}+2 \alpha s+\omega_{0}^{2}=0
$$

where $\alpha=1 / 2 R C$ for the parallel circuit, $\alpha=R / 2 L$ for the series circuit, and $\omega_{0}^{2}=1 / L C$ for both the parallel and series circuits. (See pages 267 and 286.)

- The roots of the characteristic equation are

$$
s_{1,2}=-\alpha \pm \sqrt{\alpha^{2}-\omega_{0}^{2}}
$$

(See page 268.)

- The form of the natural and step responses of series and parallel $R L C$ circuits depends on the values of $\alpha^{2}$ and $\omega_{0}^{2}$; such responses can be overdamped, underdamped, or critically damped. These terms describe the impact of the dissipative element $(R)$ on the response. The neper frequency, $\alpha$, reflects the effect of $R$. (See pages 268 and 269.)
- The response of a second-order circuit is overdamped, underdamped, or critically damped as shown in Table 8.2.
- In determining the natural response of a second-order circuit, we first determine whether it is over-, under-, or
critically damped, and then we solve the appropriate equations as shown in Table 8.3.
- In determining the step response of a second-order circuit, we apply the appropriate equations depending on the damping, as shown in Table 8.4.
- For each of the three forms of response, the unknown coefficients (i.e., the $A \mathrm{~s}, B \mathrm{~s}$, and $D \mathrm{~s}$ ) are obtained by evaluating the circuit to find the initial value of the response, $x(0)$, and the initial value of the first derivative of the response, $d x(0) / d t$.
- When two integrating amplifiers with ideal op amps are connected in cascade, the output voltage of the second integrator is related to the input voltage of the first by an ordinary, second-order differential equation. Therefore, the techniques developed in this chapter may be used to analyze the behavior of a cascaded integrator. (See pages 289 and 290.)
- We can overcome the limitation of a simple integrating amplifier-the saturation of the op amp due to charge accumulating in the feedback capacitor-by placing a resistor in parallel with the capacitor in the feedback path. (See page 291.)

TABLE 8.2 The Response of a Second-Order Circuit is Overdamped, Underdamped, or Critically Damped

| The Circuit is | When | Qualitative Nature of the Response |
| :--- | :--- | :--- |
| Overdamped | $\alpha^{2}>\omega_{0}^{2}$ | The voltage or current approaches its final value without oscillation |
| Underdamped | $\alpha^{2}<\omega_{0}^{2}$ | The voltage or current oscillates about its final value |
| Critically damped | $\alpha^{2}=\omega_{0}^{2}$ | The voltage or current is on the verge of oscillating about its final value |

TABLE 8.3 In Determining the Natural Response of a Second-Order Circuit, We First Determine Whether it is Over-, Under-, or Critically Damped, and Then We Solve the Appropriate Equations

| Damping | Natural Response Equations | Coefficient Equations |
| :--- | :--- | :--- |
| Overdamped | $x(t)=A_{1} e^{s_{1} t}+A_{2} e^{s_{2} t}$ | $x(0)=A_{1}+A_{2} ;$ |
|  |  | $d x / d t(0)=A_{1} s_{1}+A_{2} s_{2}$ |
| Underdamped | $x(t)=\left(B_{1} \cos \omega_{d} t+B_{2} \sin \omega_{d} t\right) e^{-\alpha t}$ | $x(0)=B_{1} ;$ |
|  |  | $d x / d t(0)=-\alpha B_{1}+\omega_{d} B_{2}$, |
|  |  | where $\omega_{d}=\sqrt{\omega_{0}^{2}-\alpha^{2}}$ |
| Critically damped | $x(t)=\left(D_{1} t+D_{2}\right) e^{-\alpha t}$ | $x(0)=D_{2}$, |
|  |  | $d x / d t(0)=D_{1}-\alpha D_{2}$ |

TABLE 8.4 In Determining the Step Response of a Second-Order Circuit, We Apply the Appropriate Equations Depending on the Damping

| Damping | Step Response Equations ${ }^{\mathbf{a}}$ | Coefficient Equations |
| :--- | :--- | :--- |
| Overdamped | $x(t)=X_{f}+A_{1}^{\prime} e^{s_{1} t}+A_{2}^{\prime} e^{s_{2} t}$ | $x(0)=X_{f}+A_{1}^{\prime}+A_{2}^{\prime} ;$ |
| Underdamped | $x(t)=X_{f}+\left(B_{1}^{\prime} \cos \omega_{d} t+B_{2}^{\prime} \sin \omega_{d} t\right) e^{-\alpha t}$ | $d x / d t(0)=A_{1}^{\prime} s_{1}+A_{2}^{\prime} s_{2}$ |
| Critically damped | $x(t)=X_{f}+D_{1}^{\prime} t e^{-\alpha t}+D_{2}^{\prime} e^{-\alpha t}$ | $x(0)=X_{f}+B_{1}^{\prime} ;$ |
|  | $d x / d t(0)=-\alpha B_{1}^{\prime}+\omega_{d} B_{2}^{\prime}$ |  |
| a where $X_{f}$ is the final value of $x(t)$. | $x(0)=X_{f}+D_{2}^{\prime} ;$ |  |
|  | $d x / d t(0)=D_{1}^{\prime}-\alpha D_{2}^{\prime}$ |  |

${ }^{a}$ where $X_{f}$ is the final value of $x(t)$.
