# 7 Response of First-Order RL and RC Circuits

CHAPTER CONTENTS

7.1 The Natural Response of an RL Circuit p. 214
7.2 The Natural Response of an RC Circuit p. 220
7.3 The Step Response of RL and RC Circuits p. 224
7.4 A General Solution for Step and Natural Responses p. 231
7.5 Sequential Switching p. 236
7.6 Unbounded Response p. 240
7.7 The Integrating Amplifier p. 241

CHAPTER OBJECTIVES

1 Be able to determine the natural response of both RL and RC circuits.
2 Be able to determine the step response of both $R L$ and $R C$ circuits.

3 Know how to analyze circuits with sequential switching.

4 Be able to analyze op amp circuits containing resistors and a single capacitor.

Response of First-Order RL and RC Circuits

In Chapter 6, we noted that an important attribute of inductors and capacitors is their ability to store energy. We are now in a position to determine the currents and voltages that arise when energy is either released or acquired by an inductor or capacitor in response to an abrupt change in a dc voltage or current source. In this chapter, we will focus on circuits that consist only of sources, resistors, and either (but not both) inductors or capacitors. For brevity, such configurations are called $\boldsymbol{R L}$ (resistorinductor) and $\boldsymbol{R C}$ (resistor-capacitor) circuits.

Our analysis of $R L$ and $R C$ circuits will be divided into three phases. In the first phase, we consider the currents and voltages that arise when stored energy in an inductor or capacitor is suddenly released to a resistive network. This happens when the inductor or capacitor is abruptly disconnected from its dc source. Thus we can reduce the circuit to one of the two equivalent forms shown in Fig. 7.1 on page 214. The currents and voltages that arise in this configuration are referred to as the natural response of the circuit, to emphasize that the nature of the circuit itself, not external sources of excitation, determines its behavior.

In the second phase of our analysis, we consider the currents and voltages that arise when energy is being acquired by an inductor or capacitor due to the sudden application of a dc voltage or current source. This response is referred to as the step response. The process for finding both the natural and step responses is the same; thus, in the third phase of our analysis, we develop a general method that can be used to find the response of $R L$ and $R C$ circuits to any abrupt change in a dc voltage or current source.

Figure 7.2 on page 214 shows the four possibilities for the general configuration of $R L$ and $R C$ circuits. Note that when there are no independent sources in the circuit, the Thévenin voltage or Norton current is zero, and the circuit reduces to one of those shown in Fig. 7.1; that is, we have a natural-response problem.

Practical Perspective

Artificial Pacemaker

The muscle that makes up the heart contracts due to rhythmical electrical impulses. The frequency of the impulses is controlled by pacemaker cells. In adults, the pacemaker cells establish a resting heart rate of about 72 beats per minutes. But sometimes the pacemaker cells are damaged and may produce a very low resting heart rate (a condition known as bradycardia) or a very high resting heart rate (a condition known as tachycardia). A normal heart rhythm can be restored by implanting an artificial pacemaker that delivers electrical impulses to the heart, mimicking the pacemaker cells. An example of an artificial
pacemaker both outside and inside the body is shown in the figures below.

Artificial pacemakers are very small and lightweight. They have a programmable microprocessor that monitors a few parameters and adjusts the heart rate, an efficient battery with a life of up to 15 years, and circuitry that generates the pulse. The simplest circuit consists of a resistor and a capacitor. Once we have introduced the first-order RC circuit, we will look at an RC circuit design for artificial pacemakers.
image_name:Pacemaker outside the body
description:The image consists of two diagrams illustrating a pacemaker both outside and inside the body.

1. **Identification of Components and Structure:**
- The first diagram shows a pacemaker device with labeled components. The pacemaker is depicted as a small, rounded device. Attached to it are wires that connect to an electrode. The wires are coiled, indicating flexibility and length to reach the heart.
- The second diagram shows the pacemaker implanted inside the human body. The pacemaker is placed in the chest area, just beneath the skin, with wires leading to the heart. The electrode is positioned at the heart, indicating its role in transmitting electrical impulses.

2. **Connections and Interactions:**
- The wires serve as conduits for electrical signals from the pacemaker to the heart. These signals help regulate the heart's rhythm by delivering electrical impulses to the electrode, which is in contact with the heart muscle.
- The placement of the pacemaker in the chest and the routing of the wires highlight the direct connection and interaction between the device and the heart, ensuring effective pacing.

3. **Labels, Annotations, and Key Features:**
- Key labels such as "Pacemaker," "Wires," and "Electrode" are used to identify the components in both diagrams.
- The anatomical illustration in the second diagram provides context for the pacemaker's placement in relation to the heart and major blood vessels, aiding in understanding how the device functions within the body.
image_name:Pacemaker inside the body
description:The image illustrates the placement and components of a pacemaker both outside and inside the body.

1. **Identification of Components and Structure:**
- **Pacemaker:** The device is shown as a small, rounded object placed under the skin of the chest. It is connected to the heart via leads.
- **Wires and Electrode:** The wires, also known as leads, extend from the pacemaker and are connected to an electrode. The electrode is placed inside the heart to deliver electrical impulses.

2. **Connections and Interactions:**
- The pacemaker is connected to the heart through the leads, which carry electrical signals. These signals are used to regulate the heart's rhythm by sending pulses to the electrode implanted in the heart muscle.
- The diagram shows the pacemaker positioned subcutaneously, with leads running through blood vessels to reach the heart.

3. **Labels, Annotations, and Key Features:**
- The image includes labels such as "Pacemaker," "Wires," and "Electrode" to identify the different components.
- The anatomical illustration shows the heart and major blood vessels, providing context for the placement of the pacemaker and its leads.

image_name:(a)
description:
[
'name': 'Leq', 'type': 'Inductor', 'value': 'Leq', 'ports': {'N1': 'A', 'N2': 'B'
'name': 'Req', 'type': 'Resistor', 'value': 'Req', 'ports': {'N1': 'A', 'N2': 'B'
]
extrainfo:The circuit diagram (a) shows an RL circuit with an inductor Leq and a resistor Req in series, connected to a current source I0. The nodes are labeled A and B.
image_name:(b)
description:
[
'name': 'Ceq', 'type': 'Capacitor', 'value': 'Ceq', 'ports': {'Np': 'A', 'Nn': 'B'
'name': 'Req', 'type': 'Resistor', 'value': 'Req', 'ports': {'N1': 'A', 'N2': 'B'
]
extrainfo:The circuit is a first-order RC circuit with a capacitor Ceq and a voltage source V0 in parallel with a resistor Req.


Figure $7.1 \triangle$ The two forms of the circuits for natural response. (a) $R L$ circuit. (b) $R C$ circuit.
image_name:(a)
description:
[
'name': 'V_Th', 'type': 'VoltageSource', 'value': 'V_Th', 'ports': {'Np': 'V_Th', 'Nn': 'GND'
'name': 'R_Th', 'type': 'Resistor', 'value': 'R_Th', 'ports': {'N1': 'V_Th', 'N2': 'V'
'name': 'L', 'type': 'Inductor', 'value': 'L', 'ports': {'N1': 'V', 'N2': 'GND'
]
extrainfo:The circuit is an RL circuit with a voltage source V_Th, a resistor R_Th, and an inductor L connected in series. The current i flows through the circuit, and the voltage across the inductor is v.
image_name:(b)
description:
[
'name': 'VTh/RTh', 'type': 'CurrentSource', 'value': 'VTh/RTh', 'ports': {'Np': 'GND', 'Nn': 'V'
'name': 'RTh', 'type': 'Resistor', 'value': 'RTh', 'ports': {'N1': 'V', 'N2': 'GND'
'name': 'L', 'type': 'Inductor', 'value': 'L', 'ports': {'N1': 'V', 'N2': 'GND'
]
extrainfo:This is a Norton equivalent RL circuit with a current source VTh/RTh in parallel with a resistor RTh and an inductor L. It represents a first-order RL circuit for analyzing natural response.
image_name:(c)
description:
[
'name': 'VTh', 'type': 'VoltageSource', 'value': 'VTh', 'ports': {'Np': 'VTh', 'Nn': 'GND'
'name': 'RTh', 'type': 'Resistor', 'value': 'RTh', 'ports': {'N1': 'VTh', 'N2': 'V'
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'V', 'Nn': 'GND'
]
extrainfo:The circuit is a first-order RC circuit with a voltage source VTh, a resistor RTh, and a capacitor C. The voltage source is connected in series with the resistor, and the capacitor is connected in parallel to the combination, forming a typical RC charging circuit.
image_name:(d)
description:
[
'name': 'VTh/RTh', 'type': 'CurrentSource', 'ports': {'Np': 'GND', 'Nn': 'V'
'name': 'RTh', 'type': 'Resistor', 'value': 'RTh', 'ports': {'N1': 'V', 'N2': 'GND'
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'V', 'Nn': 'GND'
]
extrainfo:The circuit is a first-order RC circuit with a capacitor C and a current source VTh/RTh in parallel with a resistor RTh. It demonstrates the natural response of a capacitor connected to a Norton equivalent.


Figure 7.2 A Four possible first-order circuits.
(a) An inductor connected to a Thévenin equivalent.
(b) An inductor connected to a Norton equivalent.
(c) A capacitor connected to a Thévenin equivalent.
(d) A capacitor connected to a Norton equivalent.
image_name:Figure 7.3
description:
[
'name': 'Is', 'type': 'CurrentSource', 'value': 'Is', 'ports': {'Np': 'SW1', 'Nn': 'GND'
'name': 'R0', 'type': 'Resistor', 'value': 'R0', 'ports': {'N1': 'SW1', 'N2': 'GND'
'name': 'L', 'type': 'Inductor', 'value': 'L', 'ports': {'N1': 'SW2', 'N2': 'GND'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'SW2', 'N2': 'GND'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'SW1', 'N2': 'sw1'
'name': 'L', 'type': 'Inductor', 'ports': {'N1': 'SW2', 'N2': 'GND'
]
extrainfo:The circuit is an RL circuit with a current source Is and two switches SW1 and SW2. It demonstrates the behavior of the circuit at t=0 when the switch SW1 is activated. The inductor L and resistor R are in parallel, connected to the ground.


Figure 7.3 $\triangle$ An $R L$ circuit.
image_name:Figure 7.4
description:
[
'name': 'L', 'type': 'Inductor', 'value': 'L', 'ports': {'N1': 'V', 'N2': 'GND'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'V', 'N2': 'GND'
]
extrainfo:The circuit is an RL parallel circuit with a current source Is. The inductor L and resistor R are both connected to the same node V and to ground. The circuit demonstrates behavior at t=0 when the current source is active.


Figure 7.4 $\triangle$ The circurt shown in Fig. 7.3, for $t \geq 0$.
$R L$ and $R C$ circuits are also known as first-order circuits, because their voltages and currents are described by first-order differential equations. No matter how complex a circuit may appear, if it can be reduced to a Thévenin or Norton equivalent connected to the terminals of an equivalent inductor or capacitor, it is a first-order circuit. (Note that if multiple inductors or capacitors exist in the original circuit, they must be interconnected so that they can be replaced by a single equivalent element.)

After introducing the techniques for analyzing the natural and step responses of first-order circuits, we discuss some special cases of interest. The first is that of sequential switching, involving circuits in which switching can take place at two or more instants in time. Next is the unbounded response. Finally, we analyze a useful circuit called the integrating amplifier.

## 7.1 The Natural Response of an RL Circuit

The natural response of an $R L$ circuit can best be described in terms of the circuit shown in Fig. 7.3. We assume that the independent current source generates a constant current of $I_{s} \mathrm{~A}$, and that the switch has been in a closed position for a long time. We define the phrase a long time more accurately later in this section. For now it means that all currents and voltages have reached a constant value. Thus only constant, or dc, currents can exist in the circuit just prior to the switch's being opened, and therefore the inductor appears as a short circuit $(L d i / d t=0)$ prior to the release of the stored energy.

Because the inductor appears as a short circuit, the voltage across the inductive branch is zero, and there can be no current in either $R_{0}$ or $R$. Therefore, all the source current $I_{s}$ appears in the inductive branch. Finding the natural response requires finding the voltage and current at the terminals of the resistor after the switch has been opened, that is, after the source has been disconnected and the inductor begins releasing energy. If we let $t=0$ denote the instant when the switch is opened, the problem becomes one of finding $v(t)$ and $i(t)$ for $t \geq 0$. For $t \geq 0$, the circuit shown in Fig. 7.3 reduces to the one shown in Fig. 7.4.

Deriving the Expression for the Current

To find $i(t)$, we use Kirchhoff's voltage law to obtain an expression involving $i, R$, and $L$. Summing the voltages around the closed loop gives

$$
\begin{equation*}
L \frac{d i}{d t}+R i=0 \tag{7.1}
\end{equation*}
$$

where we use the passive sign convention. Equation 7.1 is known as a firstorder ordinary differential equation, because it contains terms involving the ordinary derivative of the unknown, that is, $d i / d t$. The highest order derivative appearing in the equation is 1 ; hence the term first-order.

We can go one step further in describing this equation. The coefficients in the equation, $R$ and $L$, are constants; that is, they are not functions of either the dependent variable $i$ or the independent variable $t$. Thus the equation can also be described as an ordinary differential equation with constant coefficients.

To solve Eq. 7.1, we divide by $L$, transpose the term involving $i$ to the right-hand side, and then multiply both sides by a differential time $d t$. The result is

$$
\begin{equation*}
\frac{d i}{d t} d t=-\frac{R}{L} i d t \tag{7.2}
\end{equation*}
$$

Next, we recognize the left-hand side of Eq. 7.2 as a differential change in the current $i$, that is, $d i$. We now divide through by $i$, getting

$$
\begin{equation*}
\frac{d i}{i}=-\frac{R}{L} d t \tag{7.3}
\end{equation*}
$$

We obtain an explicit expression for $i$ as a function of $t$ by integrating both sides of Eq. 7.3. Using $x$ and $y$ as variables of integration yields

$$
\begin{equation*}
\int_{i\left(t_{0}\right)}^{i(t)} \frac{d x}{x}=-\frac{R}{L} \int_{t_{0}}^{t} d y \tag{7.4}
\end{equation*}
$$

in which $i\left(t_{0}\right)$ is the current corresponding to time $t_{0}$, and $i(t)$ is the current corresponding to time $t$. Here, $t_{0}=0$. Therefore, carrying out the indicated integration gives

$$
\begin{equation*}
\ln \frac{i(t)}{i(0)}=-\frac{R}{L} t \tag{7.5}
\end{equation*}
$$

Based on the definition of the natural logarithm,

$$
\begin{equation*}
i(t)=i(0) e^{-(R / L) t} \tag{7.6}
\end{equation*}
$$

Recall from Chapter 6 that an instantaneous change of current cannot occur in an inductor. Therefore, in the first instant after the switch has been opened, the current in the inductor remains unchanged. If we use $0^{-}$ to denote the time just prior to switching, and $0^{+}$for the time immediately following switching, then

$$
i\left(0^{-}\right)=i\left(0^{+}\right)=I_{0}
$$

where, as in Fig. 7.1, $I_{0}$ denotes the initial current in the inductor. The initial current in the inductor is oriented in the same direction as the reference direction of $i$. Hence Eq. 7.6 becomes

$$
\begin{equation*}
i(t)=I_{0} e^{-(R / L) t}, \quad t \geq 0 \tag{7.7}
\end{equation*}
$$

which shows that the current starts from an initial value $I_{0}$ and decreases exponentially toward zero as $t$ increases. Figure 7.5 shows this response.

We derive the voltage across the resistor in Fig. 7.4 from a direct application of Ohm's law:

$$
\begin{equation*}
v=i R=I_{0} R e^{-(R / L) t}, \quad t \geq 0^{+} \tag{7.8}
\end{equation*}
$$

Note that in contrast to the expression for the current shown in Eq. 7.7, the voltage is defined only for $t>0$, not at $t=0$. The reason is that a step change occurs in the voltage at zero. Note that for $t<0$, the derivative of the current is zero, so the voltage is also zero. (This result follows from $v=L d i / d t=0$.) Thus

$$
\begin{align*}
& v\left(0^{-}\right)=0  \tag{7.9}\\
& v\left(0^{+}\right)=I_{0} R \tag{7.10}
\end{align*}
$$

where $v\left(0^{+}\right)$is obtained from Eq. 7.8 with $t=0^{+} .{ }^{1}$ With this step change at an instant in time, the value of the voltage at $t=0$ is unknown. Thus we use $t \geq 0^{+}$in defining the region of validity for these solutions.

[^0]Initial inductor current

Natural response of an RL circuit
image_name:Figure 7.5
description:The graph in Figure 7.5 is a time-domain waveform representing the natural response of the current in an RL circuit. The horizontal axis is labeled \( t \), representing time, and the vertical axis is labeled \( i(t) \), representing the current in the circuit. The units for time and current are not specified, but the context suggests they are in seconds and amperes, respectively.

The graph begins at \( t = 0 \) with the current at its maximum value \( I_0 \). This initial condition is consistent with the current in an inductor at the moment a switch is opened or a sudden change occurs in the circuit.

The overall behavior of the graph shows an exponential decay of the current over time, characteristic of the natural response of an RL circuit. As time progresses, the current decreases gradually, approaching zero asymptotically. This indicates that the energy stored in the inductor is being dissipated through the resistor.

Key features of the graph include the initial current value \( I_0 \) at \( t = 0 \) and the exponential decay trend. There are no oscillations or fluctuations, which is typical for an RL circuit without additional reactive components. The decay rate is determined by the time constant \( \tau = \frac{L}{R} \), although this specific value is not marked on the graph.

There are no additional annotations or specific data points marked on the graph, but it visually represents the theoretical behavior described by the equation \( i(t) = I_0 e^{-\frac{R}{L} t} \).


Figure 7.5 $\boldsymbol{\Delta}$ The current response for the circuit shown in Fig. 7.4.

We derive the power dissipated in the resistor from any of the following expressions:

$$
\begin{equation*}
p=v i, \quad p=i^{2} R, \quad \text { or } \quad p=\frac{v^{2}}{R} \tag{7.11}
\end{equation*}
$$

Whichever form is used, the resulting expression can be reduced to

$$
\begin{equation*}
p=I_{0}^{2} R e^{-2(R / L) t}, \quad t \geq 0^{+} \tag{7.12}
\end{equation*}
$$

The energy delivered to the resistor during any interval of time after the switch has been opened is

$$
\begin{align*}
w & =\int_{0}^{t} p d x=\int_{0}^{t} I_{0}^{2} R e^{-2(R / L) x} d x \\
& =\frac{1}{2(R / L)} I_{0}^{2} R\left(1-e^{-2(R / L) t}\right) \\
& =\frac{1}{2} L I_{0}^{2}\left(1-e^{-2(R / L) t}\right), \quad t \geq 0 \tag{7.13}
\end{align*}
$$

Note from Eq. 7.13 that as $t$ becomes infinite, the energy dissipated in the resistor approaches the initial energy stored in the inductor.

The Significance of the Time Constant

The expressions for $i(t)$ (Eq. 7.7) and $v(t)$ (Eq. 7.8) include a term of the form $e^{-(R / L) t}$. The coefficient of $t$-namely, $R / L-$ determines the rate at which the current or voltage approaches zero. The reciprocal of this ratio is the time constant of the circuit, denoted

$$
\begin{equation*}
\tau=\text { time constant }=\frac{L}{R} \tag{7.14}
\end{equation*}
$$

Using the time-constant concept, we write the expressions for current, voltage, power, and energy as

$$
\begin{align*}
i(t) & =I_{0} e^{-t / \tau}, \quad t \geq 0  \tag{7.15}\\
v(t) & =I_{0} R e^{-t / \tau}, \quad t \geq 0^{+}  \tag{7.16}\\
p & =I_{0}^{2} R e^{-2 t / \tau}, \quad t \geq 0^{+}  \tag{7.17}\\
w & =\frac{1}{2} L I_{0}^{2}\left(1-e^{-2 t / \tau}\right), \quad t \geq 0 \tag{7.18}
\end{align*}
$$

The time constant is an important parameter for first-order circuits, so mentioning several of its characteristics is worthwhile. First, it is convenient to think of the time elapsed after switching in terms of integral multiples of $\tau$. Thus one time constant after the inductor has begun to release its stored energy to the resistor, the current has been reduced to $e^{-1}$, or approximately 0.37 of its initial value.

Table 7.1 gives the value of $e^{-t / \tau}$ for integral multiples of $\tau$ from 1 to 10. Note that when the elapsed time exceeds five time constants, the current is less than $1 \%$ of its initial value. Thus we sometimes say that five time constants after switching has occurred, the currents and voltages have, for most practical purposes, reached their final values. For single time-constant circuits (first-order circuits) with $1 \%$ accuracy, the phrase a long time implies that five or more time constants have elapsed. Thus the existence of current in the $R L$ circuit shown in Fig. 7.1(a) is a momentary event and is referred to as the transient response of the circuit. The response that exists a long time after the switching has taken place is called the steady-state response. The phrase a long time then also means the time it takes the circuit to reach its steady-state value.

Any first-order circuit is characterized, in part, by the value of its time constant. If we have no method for calculating the time constant of such a circuit (perhaps because we don't know the values of its components), we can determine its value from a plot of the circuit's natural response. That's because another important characteristic of the time constant is that it gives the time required for the current to reach its final value if the current continues to change at its initial rate. To illustrate, we evaluate $d i / d t$ at $0^{+}$and assume that the current continues to change at this rate:

$$
\begin{equation*}
\frac{d i}{d t}\left(0^{+}\right)=-\frac{R}{L} I_{0}=-\frac{I_{0}}{\tau} \tag{7.19}
\end{equation*}
$$

Now, if $i$ starts as $I_{0}$ and decreases at a constant rate of $I_{0} / \tau$ amperes per second, the expression for $i$ becomes

$$
\begin{equation*}
i=I_{0}-\frac{I_{0}}{\tau} t . \tag{7.20}
\end{equation*}
$$

Equation 7.20 indicates that $i$ would reach its final value of zero in $\tau$ seconds. Figure 7.6 shows how this graphic interpretation is useful in estimating the time constant of a circuit from a plot of its natural response. Such a plot could be generated on an oscilloscope measuring output current. Drawing the tangent to the natural response plot at $t=0$ and reading the value at which the tangent intersects the time axis gives the value of $\tau$.

Calculating the natural response of an $R L$ circuit can be summarized as follows:

1. Find the initial current, $I_{0}$, through the inductor.
2. Find the time constant of the circuit, $\tau=L / R$.
3. Use Eq. $7.15, I_{0} e^{-t / \tau}$, to generate $i(t)$ from $I_{0}$ and $\tau$.

All other calculations of interest follow from knowing $i(t)$. Examples 7.1 and 7.2 illustrate the numerical calculations associated with the natural response of an $R L$ circuit.

TABLE 7.1 Value of $e^{-t / \tau}$ For $t$ Equal to Integral Multiples of $\tau$

| $t$ | $e^{-t / \tau}$ | $t$ | $e^{-t / \tau}$ |
| :--- | :--- | :--- | :--- |
| $\tau$ | $3.6788 \times 10^{-1}$ | $6 \tau$ | $2.4788 \times 10^{-3}$ |
| $2 \tau$ | $1.3534 \times 10^{-1}$ | $7 \tau$ | $9.1188 \times 10^{-4}$ |
| $3 \tau$ | $4.9787 \times 10^{-2}$ | $8 \tau$ | $3.3546 \times 10^{-4}$ |
| $4 \tau$ | $1.8316 \times 10^{-2}$ | $9 \tau$ | $1.2341 \times 10^{-4}$ |
| $5 \tau$ | $6.7379 \times 10^{-3}$ | $10 \tau$ | $4.5400 \times 10^{-5}$ |

image_name:Figure 7.6
description:The graph in Figure 7.6 is a time-domain waveform illustrating the natural response of an RL circuit. It plots current \( i \) on the vertical axis against time \( t \) on the horizontal axis. The axes are labeled with \( i \) in amperes and \( t \) in seconds.

Type of Graph and Function:
The graph is an exponential decay curve representing the current \( i(t) \) in an RL circuit after a switch has been opened. It shows the behavior of the current over time as it decreases from its initial value \( I_0 \).

=Axes Labels and Units:
- **Vertical Axis (i):** Represents the current in amperes.
- **Horizontal Axis (t):** Represents time in seconds.
- The graph uses a linear scale on both axes.

Overall Behavior and Trends:
- The graph shows an exponential decay from an initial current \( I_0 \) at time \( t = 0 \).
- The curve follows the equation \( i = I_0 e^{-t/\tau} \), indicating an exponential decrease towards zero as time increases.
- The decay is characterized by the time constant \( \tau \), which is a measure of how quickly the current decreases.

Key Features and Technical Details:
- **Initial Value:** The current starts at \( I_0 \) when \( t = 0 \).
- **Time Constant (\( \tau \)):** The time at which the current has decayed to approximately 36.8% of \( I_0 \).
- **Linear Approximation:** A linear line is drawn from \( I_0 \) to intersect the time axis at \( \tau \), representing a linear approximation of the decay.
- **Equation Labels:** The graph is annotated with the exponential decay equation \( i = I_0 e^{-t/\tau} \) and its linear approximation \( i = I_0 - (I_0/\tau)t \).

### Annotations and Specific Data Points:
- The graph includes a marker at \( \tau \) on the time axis, highlighting the time constant.
- Annotations indicate the exponential decay behavior and the linear approximation for visual comparison.

This graph provides a clear visual representation of the current decay in an RL circuit, emphasizing the role of the time constant \( \tau \) in determining the rate of decay.


Figure 7.6 $\triangle \mathrm{A}$ graphic interpretation of the time constant of the $R L$ circuit shown in Fig. 7.4.

1 Calculating the natural response of RL circuit

#### Example 7.1 Determining the Natural Response of an RL Circuit

The switch in the circuit shown in Fig. 7.7 has been closed for a long time before it is opened at $t=0$. Find
a) $i_{L}(t)$ for $t \geq 0$,
b) $i_{o}(t)$ for $t \geq 0^{+}$,
c) $v_{o}(t)$ for $t \geq 0^{+}$,
d) the percentage of the total energy stored in the 2 H inductor that is dissipated in the $10 \Omega$ resistor.
image_name:Figure 7.7
description:
[
'name': 'Current Source', 'type': 'CurrentSource', 'value': '20 A', 'ports': {'Np': 'GND', 'Nn': 'X1'
'name': 'Resistor 1', 'type': 'Resistor', 'value': '0.1 Ω', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': 'Switch SW1', 'type': 'Switch', 'ports': {'N1': 'X1', 'N2': 'X2'
'name': 'Resistor 2', 'type': 'Resistor', 'value': '2 Ω', 'ports': {'N1': 'X2', 'N2': 'Vo'
'name': 'Inductor', 'type': 'Inductor', 'value': '2 H', 'ports': {'N1': 'X2', 'N2': 'GND'
'name': 'Resistor 3', 'type': 'Resistor', 'value': '10 Ω', 'ports': {'N1': 'Vo', 'N2': 'GND'
'name': 'Resistor 4', 'type': 'Resistor', 'value': '40 Ω', 'ports': {'N1': 'Vo', 'N2': 'GND'
]
extrainfo:The circuit is an RL circuit with a switch that opens at t=0. Initially, the current is 20 A through the inductor. The circuit includes a current source, resistors, an inductor, and a switch. The output voltage and current are measured across the 10 Ω resistor.


Figure $7.7 \triangle$ The circuit for Example 7.1.

#### Solution

a) The switch has been closed for a long time prior to $t=0$, so we know the voltage across the inductor must be zero at $t=0^{-}$. Therefore the initial current in the inductor is 20 A at $t=0^{-}$. Hence, $i_{L}\left(0^{+}\right)$also is 20 A , because an instantaneous change in the current cannot occur in an inductor. We replace the resistive circuit connected to the terminals of the inductor with a single resistor of $10 \Omega$ :

$$
R_{\mathrm{eq}}=2+(40 \| 10)=10 \Omega
$$

The time constant of the circuit is $L / R_{\mathrm{eq}}$, or 0.2 s , giving the expression for the inductor current as

$$
i_{L}(t)=20 e^{-5 t} \mathrm{~A}, \quad t \geq 0
$$

b) We find the current in the $40 \Omega$ resistor most easily by using current division; that is,

$$
i_{o}=-i_{L} \frac{10}{10+40}
$$

Note that this expression is valid for $t \geq 0^{+}$ because $i_{o}=0$ at $t=0^{-}$. The inductor behaves as a short circuit prior to the switch being opened, producing an instantaneous change in the current $i_{o}$. Then,

$$
i_{o}(t)=-4 e^{-5 t} \mathrm{~A}, \quad t \geq 0^{+}
$$

c) We find the voltage $v_{o}$ by direct application of Ohm's law:

$$
v_{o}(t)=40 i_{o}=-160 e^{-5 t} \mathrm{~V}, \quad t \geq 0^{+}
$$

d) The power dissipated in the $10 \Omega$ resistor is

$$
p_{10 \Omega}(t)=\frac{v_{o}^{2}}{10}=2560 e^{-10 t} \mathrm{~W}, \quad t \geq 0^{+}
$$

The total energy dissipated in the $10 \Omega$ resistor is

$$
w_{10 \Omega}(t)=\int_{0}^{\infty} 2560 e^{-10 t} d t=256 \mathrm{~J}
$$

The initial energy stored in the 2 H inductor is

$$
w(0)=\frac{1}{2} L i^{2}(0)=\frac{1}{2}(2)(400)=400 \mathrm{~J}
$$

Therefore the percentage of energy dissipated in the $10 \Omega$ resistor is

$$
\frac{256}{400}(100)=64 \%
$$

#### Example 7.2 Determining the Natural Response of an RL Circuit with Parallel Inductors

In the circuit shown in Fig. 7.8, the initial currents in inductors $L_{1}$ and $L_{2}$ have been established by sources not shown. The switch is opened at $t=0$.
a) Find $i_{1}, i_{2}$, and $i_{3}$ for $t \geq 0$.
b) Calculate the initial energy stored in the parallel inductors.
c) Determine how much energy is stored in the inductors as $t \rightarrow \infty$.
d) Show that the total energy delivered to the resistive network equals the difference between the results obtained in (b) and (c).

#### Solution

a) The key to finding currents $i_{1}, i_{2}$, and $i_{3}$ lies in knowing the voltage $v(t)$. We can easily find $v(t)$ if we reduce the circuit shown in Fig. 7.8 to the equivalent form shown in Fig. 7.9. The parallel inductors simplify to an equivalent inductance of 4 H , carrying an initial current of 12 A . The resistive network reduces to a single resistance of $8 \Omega$. Hence the initial value of $i(t)$ is 12 A and the time constant is $4 / 8$, or 0.5 s . Therefore

$$
i(t)=12 e^{-2 t} \mathrm{~A}, \quad t \geq 0
$$

Now $v(t)$ is simply the product $8 i$, so

$$
v(t)=96 e^{-2 t} \mathrm{~V}, \quad t \geq 0^{+}
$$

The circuit shows that $v(t)=0$ at $t=0^{-}$, so the expression for $v(t)$ is valid for $t \geq 0^{+}$. After obtaining $v(t)$, we can calculate $i_{1}, i_{2}$, and $i_{3}$ :

$$
\begin{aligned}
i_{1} & =\frac{1}{5} \int_{0}^{t} 96 e^{-2 x} d x-8 \\
& =1.6-9.6 e^{-2 t} \mathrm{~A}, \quad t \geq 0 \\
i_{2} & =\frac{1}{20} \int_{0}^{t} 96 e^{-2 x} d x-4
\end{aligned}
$$

$$
\begin{aligned}
& =-1.6-2.4 e^{-2 t} \mathrm{~A}, \quad t \geq 0 \\
i_{3} & =\frac{v(t)}{10} \frac{15}{25}=5.76 e^{-2 t} \mathrm{~A}, \quad t \geq 0^{+}
\end{aligned}
$$

Note that the expressions for the inductor currents $i_{1}$ and $i_{2}$ are valid for $t \geq 0$, whereas the expression for the resistor current $i_{3}$ is valid for $t \geq 0^{+}$.
image_name:Figure 7.9
description:
[
'name': '4H', 'type': 'Inductor', 'value': '4H', 'ports': {'N1': 'A', 'N2': 'GND'
'name': '8Ω', 'type': 'Resistor', 'value': '8Ω', 'ports': {'N1': 'A', 'N2': 'GND'
]
extrainfo:The circuit includes a 12A current source connected in parallel with a 4H inductor and an 8Ω resistor. The node A is the common connection point, and the ground node is labeled as GND. The voltage across these elements is denoted as v(t), and the current through the resistor is indicated by i.


Figure 7.9 $\triangle$ A simplification of the circuit shown in Fig. 7.8.
b) The initial energy stored in the inductors is

$$
w=\frac{1}{2}(5)(64)+\frac{1}{2}(20)(16)=320 \mathrm{~J}
$$

c) As $t \rightarrow \infty, \quad i_{1} \rightarrow 1.6 \mathrm{~A}$ and $i_{2} \rightarrow-1.6 \mathrm{~A}$. Therefore, a long time after the switch has been opened, the energy stored in the two inductors is

$$
w=\frac{1}{2}(5)(1.6)^{2}+\frac{1}{2}(20)(-1.6)^{2}=32 \mathrm{~J}
$$

d) We obtain the total energy delivered to the resistive network by integrating the expression for the instantaneous power from zero to infinity:

$$
\begin{aligned}
w & =\int_{0}^{\infty} p d t=\int_{0}^{\infty} 1152 e^{-4 t} d t \\
& =1152 \frac{e^{-4 t}}{-4} 2_{0}^{\infty}=288 \mathrm{~J}
\end{aligned}
$$

This result is the difference between the initially stored energy ( 320 J ) and the energy trapped in the parallel inductors ( 32 J ). The equivalent inductor for the parallel inductors (which predicts the terminal behavior of the parallel combination) has an initial energy of 288 J ; that is, the energy stored in the equivalent inductor represents the amount of energy that will be delivered to the resistive network at the terminals of the original inductors.
image_name:Figure 7.8
description:
[
'name': 'L1', 'type': 'Inductor', 'value': '5 H', 'ports': {'N1': 'A', 'N2': 'GND'
'name': 'L2', 'type': 'Inductor', 'value': '20 H', 'ports': {'N1': 'A', 'N2': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': '4 Ω', 'ports': {'N1': 'A', 'N2': 'B'
'name': 'R2', 'type': 'Resistor', 'value': '40 Ω', 'ports': {'N1': 'A', 'N2': 'GND'
'name': 'R3', 'type': 'Resistor', 'value': '15 Ω', 'ports': {'N1': 'B', 'N2': 'GND'
'name': 'R4', 'type': 'Resistor', 'value': '10 Ω', 'ports': {'N1': 'B', 'N2': 'GND'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'A', 'N2': 'B'
]
extrainfo:The circuit consists of two inductors L1 and L2 in parallel, powered by two current sources I1 and I2. The resistors R1, R2, R3, and R4 form a resistive network connected to nodes A and B. The switch opens at t=0, affecting the current distribution in the circuit.


Figure $7.8 \triangle$ The circuit for Example 7.2.

ASSESSMENT PROBLEMS

Objective 1-Be able to determine the natural response of both RL and RC circuits

7.1 The switch in the circuit shown has been closed for a long time and is opened at $t=0$.
a) Calculate the initial value of $i$.
b) Calculate the initial energy stored in the inductor.
c) What is the time constant of the circuit for $t>0$ ?
d) What is the numerical expression for $i(t)$ for $t \geq 0$ ?
e) What percentage of the initial energy stored has been dissipated in the $2 \Omega$ resistor 5 ms after the switch has been opened?
image_name:
description:
[
'name': '120 V', 'type': 'VoltageSource', 'value': '120 V', 'ports': {'Np': 'A', 'Nn': 'GND'
'name': '3 Ω', 'type': 'Resistor', 'value': '3 Ω', 'ports': {'N1': 'A', 'N2': 'B'
'name': '6 Ω', 'type': 'Resistor', 'value': '6 Ω', 'ports': {'N1': 'B', 'N2': 'X1'
'name': '30 Ω', 'type': 'Resistor', 'value': '30 Ω', 'ports': {'N1': 'B', 'N2': 'GND'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'X1', 'N2': 'X2'
'name': '8 mH', 'type': 'Inductor', 'value': '8 mH', 'ports': {'N1': 'X2', 'N2': 'GND'
'name': '2 Ω', 'type': 'Resistor', 'value': '2 Ω', 'ports': {'N1': 'X2', 'N2': 'GND'
]
extrainfo:The circuit is an RL circuit with a switch SW1 that has been closed for a long time and is opened at t=0. The initial current through the inductor is -12.5 A, and the initial energy stored in the inductor is 625 mJ. The time constant for t>0 is 4 ms, and the current i(t) for t ≥ 0 is -12.5 e^{-250 t} A. 91.8% of the initial energy is dissipated in the 2 Ω resistor 5 ms after the switch is opened.


NOTE: Also try Chapter Problems 7.3, 7.8, and 7.9.

Answer: (a) -12.5 A;
(b) 625 mJ ;
(c) 4 ms ;
(d) $-12.5 e^{-250 t} \mathrm{~A}, t \geq 0$;
(e) $91.8 \%$.
7.2 At $t=0$, the switch in the circuit shown moves instantaneously from position a to position b .
a) Calculate $v_{o}$ for $t \geq 0^{+}$.
b) What percentage of the initial energy stored in the inductor is eventually dissipated in the $4 \Omega$ resistor?
image_name:Figure 7.10
description:
[
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'c', 'N2': 'a','N3':'b'
'name': 'I1', 'type': 'CurrentSource', 'value': '6.4A', 'ports': {'Np': 'b', 'Nn': 'c'
'name': 'R1', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'a', 'N2': 'd'
'name': 'R2', 'type': 'Resistor', 'value': '10Ω', 'ports': {'N1': 'a', 'N2': 'b'
'name': 'L1', 'type': 'Inductor', 'value': '0.32H', 'ports': {'N1': 'd', 'N2': 'b'
'name': 'R3', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'd', 'N2': 'b'
]
extrainfo:The circuit is an RLC circuit with a 6.4A current source, a switch, and resistors of 6Ω, 10Ω, and 4Ω, and an inductor of 0.32H. The switch changes position at t=0, affecting the circuit's response.


Answer: (a) $-8 e^{-10 t} \mathrm{~V}, t \geq 0$;
(b) $80 \%$.
image_name:Figure 7.10 An RC circuit
description:
[
'name': 'Vg', 'type': 'VoltageSource', 'ports': {'Np': 'C', 'Nn': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'C', 'N2': 'a'
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'd', 'Nn': 'GND'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'd', 'N2': 'b','N3':'b'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'b', 'N2': 'GND'
]
extrainfo:The circuit is an RC circuit with a voltage source Vg, a switch SW1, a capacitor C, and resistors R1 and R. The switch changes position at t=0, affecting the circuit's response.


Figure 7.10 An $R C$ circuit.
image_name:Figure 7.11
description:
[
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'V', 'Nn': 'GND'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'V', 'N2': 'GND'
]
extrainfo:The circuit is an RC circuit with a voltage source Vg, a capacitor C, and a resistor R. The voltage source Vg is connected in parallel with the capacitor C and resistor R. The circuit is grounded at the bottom node.


Figure 7.11 — The circuit shown in Fig. 7.10, after switching.

## 7.2 The Natural Response of an RC Circuit

As mentioned in Section 7.1, the natural response of an $R C$ circuit is analogous to that of an $R L$ circuit. Consequently, we don't treat the $R C$ circuit in the same detail as we did the $R L$ circuit.

The natural response of an $R C$ circuit is developed from the circuit shown in Fig. 7.10. We begin by assuming that the switch has been in position a for a long time, allowing the loop made up of the dc voltage source $V_{g}$, the resistor $R_{1}$, and the capacitor $C$ to reach a steady-state condition. Recall from Chapter 6 that a capacitor behaves as an open circuit in the presence of a constant voltage. Thus the voltage source cannot sustain a current, and so the source voltage appears across the capacitor terminals. In Section 7.3, we will discuss how the capacitor voltage actually builds to the steady-state value of the dc voltage source, but for now the important point is that when the switch is moved from position a to position b (at $t=0$ ), the voltage on the capacitor is $V_{g}$. Because there can be no instantaneous change in the voltage at the terminals of a capacitor, the problem reduces to solving the circuit shown in Fig. 7.11.

#V# Deriving the Expression for the Voltage

We can easily find the voltage $v(t)$ by thinking in terms of node voltages. Using the lower junction between $R$ and $C$ as the reference node and summing the currents away from the upper junction between $R$ and $C$ gives

$$
\begin{equation*}
C \frac{d v}{d t}+\frac{v}{R}=0 \tag{7.21}
\end{equation*}
$$

Comparing Eq. 7.21 with Eq. 7.1 shows that the same mathematical techniques can be used to obtain the solution for $v(t)$. We leave it to you to show that

$$
\begin{equation*}
v(t)=v(0) e^{-t / R C}, \quad t \geq 0 \tag{7.22}
\end{equation*}
$$

As we have already noted, the initial voltage on the capacitor equals the voltage source voltage $V_{g}$, or

$$
\begin{equation*}
v\left(0^{-}\right)=v(0)=v\left(0^{+}\right)=V_{g}=V_{0}, \tag{7.23}
\end{equation*}
$$

where $V_{0}$ denotes the initial voltage on the capacitor. The time constant for the $R C$ circuit equals the product of the resistance and capacitance, namely,

$$
\begin{equation*}
\tau=R C \tag{7.24}
\end{equation*}
$$

Substituting Eqs. 7.23 and 7.24 into Eq. 7.22 yields

$$
\begin{equation*}
v(t)=V_{0} e^{-t / \tau}, \quad t \geq 0 \tag{7.25}
\end{equation*}
$$

which indicates that the natural response of an $R C$ circuit is an exponential decay of the initial voltage. The time constant $R C$ governs the rate of decay. Figure 7.12 shows the plot of Eq. 7.25 and the graphic interpretation of the time constant.

After determining $v(t)$, we can easily derive the expressions for $i, p$, and $w$ :

$$
\begin{align*}
i(t) & =\frac{v(t)}{R}=\frac{V_{0}}{R} e^{-t / \tau}, \quad t \geq 0^{+}  \tag{7.26}\\
p & =v i=\frac{V_{0}^{2}}{R} e^{-2 t / \tau}, \quad t \geq 0^{+}  \tag{7.27}\\
w & =\int_{0}^{t} p d x=\int_{0}^{t} \frac{V_{0}^{2}}{R} e^{-2 x / \tau} d x \\
& =\frac{1}{2} C V_{0}^{2}\left(1-e^{-2 t / \tau}\right), \quad t \geq 0 \tag{7.28}
\end{align*}
$$

Initial capacitor voltage

4 Time constant for RC circuit

Natural response of an RC circuit
image_name:Figure 7.12
description:The graph in Figure 7.12 represents the natural response of an RC circuit, specifically showing the voltage across the capacitor, \( v(t) \), as a function of time, \( t \).

1. **Type of Graph and Function:**
- This is a time-domain waveform graph depicting exponential decay.

2. **Axes Labels and Units:**
- The horizontal axis represents time, \( t \), typically in seconds.
- The vertical axis represents voltage, \( v(t) \), in volts.
- The graph uses a linear scale for both axes.

3. **Overall Behavior and Trends:**
- The voltage \( v(t) \) starts at an initial value \( V_0 \) at \( t = 0 \) and decays exponentially towards zero as time increases.
- The decay follows the equation \( v(t) = V_0 e^{-t/\tau} \), where \( \tau \) is the time constant of the circuit.
- The curve demonstrates a rapid decrease initially, which slows down as \( t \) increases, showing the characteristic exponential decay.

4. **Key Features and Technical Details:**
- The point \( \tau \) on the time axis is marked, indicating the time constant, which is a significant point where the voltage has dropped to approximately 36.8% of its initial value \( V_0 \).
- Another line on the graph, \( v(t) = V_0 - \frac{V_0}{\tau}t \), represents a linear approximation of the initial decay.

5. **Annotations and Specific Data Points:**
- The graph includes annotations for the exponential decay equation \( v(t) = V_0 e^{-t/\tau} \) and the linear approximation \( v(t) = V_0 - \frac{V_0}{\tau}t \).
- The initial voltage \( V_0 \) is clearly marked on the vertical axis at \( t = 0 \).


Figure 7.12 $\triangle$ The natural response of an $R C$ circuit.

Calculating the natural response of an $R C$ circuit

Calculating the natural response of an $R C$ circuit can be summarized as follows:

1. Find the initial voltage, $V_{0}$, across the capacitor.
2. Find the time constant of the circuit, $\tau=R C$.
3. Use Eq. 7.25, $v(t)=V_{0} e^{-t / \tau}$, to generate $v(t)$ from $V_{0}$ and $\tau$.

All other calculations of interest follow from knowing $v(t)$. Examples 7.3 and 7.4 illustrate the numerical calculations associated with the natural response of an $R C$ circuit.

#### Example 7.3 Determining the Natural Response of an RC Circuit

The switch in the circuit shown in Fig. 7.13 has been in position $x$ for a long time. At $t=0$, the switch moves instantaneously to position $y$. Find
a) $v_{C}(t)$ for $t \geq 0$,
b) $v_{o}(t)$ for $t \geq 0^{+}$,
c) $i_{o}(t)$ for $t \geq 0^{+}$, and
d) the total energy dissipated in the $60 \mathrm{k} \Omega$ resistor.
image_name:Figure 7.13
description:
[
'name': 'V1', 'type': 'VoltageSource', 'value': '100 V', 'ports': {'Np': 'a', 'Nn': 'GND'
'name': 'C1', 'type': 'Capacitor', 'value': '0.5 μF', 'ports': {'Np': 'd', 'Nn': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': '10 kΩ', 'ports': {'N1': 'a', 'N2': 'x'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'd', 'N2': 'y','N3':'x'
'name': 'R2', 'type': 'Resistor', 'value': '32 kΩ', 'ports': {'N1': 'y', 'N2': 'b'
'name': 'R3', 'type': 'Resistor', 'value': '240 kΩ', 'ports': {'N1': 'b', 'N2': 'b'
'name': 'R4', 'type': 'Resistor', 'value': '60 kΩ', 'ports': {'N1': 'b', 'N2': 'GND'
]
extrainfo:The circuit is an RC circuit with a switch that changes position at t=0, affecting the voltage across the capacitor and the current through the resistors. The initial voltage across the capacitor is 100 V, and the resistive network can be replaced by an equivalent resistance of 80 kΩ at t=0+.


Figure 7.13 $\triangle$ The circuit for Example 7.3.

#### Solution

a) Because the switch has been in position $x$ for a long time, the 0.5 mF capacitor will charge to 100 V and be positive at the upper terminal. We can replace the resistive network connected to the capacitor at $t=0^{+}$with an equivalent resistance of $80 \mathrm{k} \Omega$. Hence the time constant of the circuit is $\left(0.5 \times 10^{-6}\right)\left(80 \times 10^{3}\right)$ or 40 ms . Then,

$$
v_{C}(t)=100 e^{-25 t} \mathrm{~V}, \quad t \geq 0
$$

b) The easiest way to find $v_{o}(t)$ is to note that the resistive circuit forms a voltage divider across the terminals of the capacitor. Thus

$$
v_{o}(t)=\frac{48}{80} v_{C}(t)=60 e^{-25 t} \mathrm{~V}, \quad t \geq 0^{+}
$$

This expression for $v_{o}(t)$ is valid for $t \geq 0^{+}$ because $v_{o}\left(0^{-}\right)$is zero. Thus we have an instantaneous change in the voltage across the $240 \mathrm{k} \Omega$ resistor.
c) We find the current $i_{o}(t)$ from Ohm's law:

$$
i_{o}(t)=\frac{v_{o}(t)}{60 \times 10^{3}}=e^{-25 t} \mathrm{~mA}, \quad t \geq 0^{+}
$$

d) The power dissipated in the $60 \mathrm{k} \Omega$ resistor is
$p_{60 \mathrm{k} \Omega}(t)=i_{o}^{2}(t)\left(60 \times 10^{3}\right)=60 e^{-50 t} \mathrm{~mW}, \quad t \geq 0^{+}$.

The total energy dissipated is

$$
w_{60 \mathrm{k} \Omega}=\int_{0}^{\infty} i_{o}^{2}(t)\left(60 \times 10^{3}\right) d t=1.2 \mathrm{~mJ}
$$

#### Example 7.4 Determining the Natural Response of an RC Circuit with Series Capacitors

The initial voltages on capacitors $C_{1}$ and $C_{2}$ in the circuit shown in Fig. 7.14 have been established by sources not shown. The switch is closed at $t=0$.
a) Find $v_{1}(t), v_{2}(t)$, and $v(t)$ for $t \geq 0$ and $i(t)$ for $t \geq 0^{+}$.
b) Calculate the initial energy stored in the capacitors $C_{1}$ and $C_{2}$.
c) Determine how much energy is stored in the capacitors as $t \rightarrow \infty$.
d) Show that the total energy delivered to the $250 \mathrm{k} \Omega$ resistor is the difference between the results obtained in (b) and (c).

#### Solution

a) Once we know $v(t)$, we can obtain the current $i(t)$ from Ohm's law. After determining $i(t)$, we can calculate $v_{1}(t)$ and $v_{2}(t)$ because the voltage across a capacitor is a function of the capacitor current. To find $v(t)$, we replace the series-connected capacitors with an equivalent capacitor. It has a capacitance of $4 \mu \mathrm{~F}$ and is charged to a voltage of 20 V. Therefore, the circuit shown in Fig. 7.14 reduces to the one shown in Fig. 7.15, which reveals that the initial value of $v(t)$ is 20 V , and that the time constant of the circuit is $(4)(250) \times 10^{-3}$, or 1 s . Thus the expression for $v(t)$ is

$$
v(t)=20 e^{-t} \mathrm{~V}, \quad t \geq 0
$$

The current $i(t)$ is

$$
i(t)=\frac{v(t)}{250,000}=80 e^{-t} \mu \mathrm{~A}, \quad t \geq 0^{+}
$$

Knowing $i(t)$, we calculate the expressions for $v_{1}(t)$ and $v_{2}(t)$ :

$$
\begin{aligned}
v_{1}(t) & =-\frac{10^{6}}{5} \int_{0}^{t} 80 \times 10^{-6} e^{-x} d x-4 \\
& =\left(16 e^{-t}-20\right) \mathrm{V}, \quad t \geq 0 \\
v_{2}(t) & =-\frac{10^{6}}{20} \int_{0}^{t} 80 \times 10^{-6} e^{-x} d x+24 \\
& =\left(4 e^{-t}+20\right) \mathrm{V}, \quad t \geq 0
\end{aligned}
$$

b) The initial energy stored in $C_{1}$ is

$$
w_{1}=\frac{1}{2}\left(5 \times 10^{-6}\right)(16)=40 \mu \mathrm{~J}
$$

The initial energy stored in $C_{2}$ is

$$
w_{2}=\frac{1}{2}\left(20 \times 10^{-6}\right)(576)=5760 \mu \mathrm{~J}
$$

image_name:Figure 7.14 A
description:
[
'name': 'C1', 'type': 'Capacitor', 'value': '5uF', 'ports': {'Np': 'V1', 'Nn': 'V2'
'name': 'C2', 'type': 'Capacitor', 'value': '20uF', 'ports': {'Np': 'V2', 'Nn': 'GND'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'V1', 'N2': 'Vt'
'name': '250kΩ', 'type': 'Resistor', 'value': '250kΩ', 'ports': {'N1': 'Vt', 'N2': 'GND'
]
extrainfo:The circuit consists of two voltage sources, two capacitors, a switch, and a resistor. It analyzes the voltage across capacitors C1 and C2 as functions of time, v1(t) and v2(t), respectively. The initial energy stored in C1 is 40 μJ and in C2 is 5760 μJ. As time approaches infinity, v1 approaches -20 V and v2 approaches +20 V.


Figure 7.14 A The circuit for Example 7.4.
image_name:Figure 7.15
description:
[
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'X1', 'N2': 'Vt'
'name': '4 μF', 'type': 'Capacitor', 'value': '4 μF', 'ports': {'Np': 'X1', 'Nn': 'GND'
'name': '250 kΩ', 'type': 'Resistor', 'value': '250 kΩ', 'ports': {'N1': 'Vt', 'N2': 'GND'
]
extrainfo:The circuit consists of a 20 V voltage source, a 4 μF capacitor, a switch SW1, and a 250 kΩ resistor. The voltage across the capacitor is analyzed as a function of time, v(t). The initial energy stored in the capacitor is 40 μJ. As time approaches infinity, the voltage across the capacitor approaches -20 V. The total energy delivered to the resistor is analyzed.


Figure 7.15 A A simplification of the circuit shown in Fig. 7.14.

The total energy stored in the two capacitors is

$$
w_{o}=40+5760=5800 \mu \mathrm{~J}
$$

c) As $t \rightarrow \infty$,

$$
v_{1} \rightarrow-20 \mathrm{~V} \quad \text { and } \quad v_{2} \rightarrow+20 \mathrm{~V}
$$

Therefore the energy stored in the two capacitors is

$$
w_{\infty}=\frac{1}{2}(5+20) \times 10^{-6}(400)=5000 \mu \mathrm{~J}
$$

d) The total energy delivered to the $250 \mathrm{k} \Omega$ resistor is

$$
w=\int_{0}^{\infty} p d t=\int_{0}^{\infty} \frac{400 e^{-2 t}}{250,000} d t=800 \mu \mathrm{~J}
$$

Comparing the results obtained in (b) and (c) shows that

$$
800 \mu \mathrm{~J}=(5800-5000) \mu \mathrm{J}
$$

The energy stored in the equivalent capacitor in Fig. 7.15 is $\frac{1}{2}\left(4 \times 10^{-6}\right)(400)$, or $800 \mu \mathrm{~J}$. Because this capacitor predicts the terminal behavior of the original series-connected capacitors, the energy stored in the equivalent capacitor is the energy delivered to the $250 \mathrm{k} \Omega$ resistor.

ASSESSMENT PROBLEMS

Objective 1-Be able to determine the natural response of both RL and RC circuits

7.3 The switch in the circuit shown has been closed for a long time and is opened at $t=0$. Find
a) the initial value of $v(t)$,
b) the time constant for $t>0$,
c) the numerical expression for $v(t)$ after the switch has been opened,
d) the initial energy stored in the capacitor, and
e) the length of time required to dissipate $75 \%$ of the initially stored energy.
image_name:v(t)
description:
[
'name': 'Current Source', 'type': 'CurrentSource', 'value': '7.5 mA', 'ports': {'Np': 'GND', 'Nn': 'X2'
'name': 'Resistor1', 'type': 'Resistor', 'value': '20 kΩ', 'ports': {'N1': 'X2', 'N2': 'X1'
'name': 'Resistor2', 'type': 'Resistor', 'value': '80 kΩ', 'ports': {'N1': 'X2', 'N2': 'GND'
'name': 'Resistor3', 'type': 'Resistor', 'value': '50 kΩ', 'ports': {'N1': 'Vt', 'N2': 'GND'
'name': 'Capacitor', 'type': 'Capacitor', 'value': '0.4 μF', 'ports': {'Np': 'Vt', 'Nn': 'GND'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'X1', 'N2': 'Vt'
]
extrainfo:The circuit is an RC circuit with a current source, resistors, a capacitor, and a switch. The switch opens at t=0, initiating the natural response of the circuit. The circuit initially charges the capacitor through the resistors when the switch is closed.


Answer: (a) 200 V ;
(b) 20 ms ;
(c) $200 e^{-50 t} \mathrm{~V}, t \geq 0$;
(d) 8 mJ ;
(e) 13.86 ms .

NOTE: Also try Chapter Problems 7.23 and 7.25.
7.4 The switch in the circuit shown has been closed for a long time before being opened at $t=0$.
a) Find $v_{o}(t)$ for $t \geq 0$.
b) What percentage of the initial energy stored in the circuit has been dissipated after the switch has been open for 60 ms ?
image_name:Figure
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '15kΩ', 'ports': {'N1': 'X3', 'N2': 'X2'
'name': 'R2', 'type': 'Resistor', 'value': '20kΩ', 'ports': {'N1': 'Vo', 'N2': 'X1'
'name': 'R3', 'type': 'Resistor', 'value': '40kΩ', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': 'C1', 'type': 'Capacitor', 'value': '5μF', 'ports': {'Np': 'Vo', 'Nn': 'X1'
'name': 'C2', 'type': 'Capacitor', 'value': '1μF', 'ports': {'Np': 'X1', 'Nn': 'GND'
'name': 'V1', 'type': 'VoltageSource', 'value': '15V', 'ports': {'Np': 'X3', 'Nn': 'GND'
'name': 'S1', 'type': 'Switch', 'ports': {'N1': 'X2', 'N2': 'Vo'
]
extrainfo:The circuit is a first-order RC circuit with a switch that opens at t=0, affecting the voltage across the capacitor C1.


Answer: (a) $8 e^{-25 t}+4 e^{-10 t} \mathrm{~V}, t \geq 0$;
(b) $81.05 \%$.
image_name:Figure 7.16
description:
[
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': 'Vs', 'Nn': 'GND'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'Vs', 'N2': 'X1'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'X1', 'N2': 'V(t)'
'name': 'L', 'type': 'Inductor', 'value': 'L', 'ports': {'N1': 'V(t)', 'N2': 'GND'
]
extrainfo:The circuit is a first-order RL circuit with a switch SW1 that opens at t=0, affecting the voltage across the inductor L.


Figure $7.16 \boldsymbol{\Delta}$ A circuit used to illustrate the step response of a first-order $R L$ circuit.

## 7.3 The Step Response of RL and $R C$ Circuits

We are now ready to discuss the problem of finding the currents and voltages generated in first-order $R L$ or $R C$ circuits when either dc voltage or current sources are suddenly applied. The response of a circuit to the sudden application of a constant voltage or current source is referred to as the step response of the circuit. In presenting the step response, we show how the circuit responds when energy is being stored in the inductor or capacitor. We begin with the step response of an $R L$ circuit.

The Step Response of an RL Circuit

To begin, we modify the first-order circuit shown in Fig. 7.2(a) by adding a switch. We use the resulting circuit, shown in Fig. 7.16, in developing the step response of an $R L$ circuit. Energy stored in the inductor at the time the switch is closed is given in terms of a nonzero initial current $i(0)$. The task is to find the expressions for the current in the circuit and for the voltage across the inductor after the switch has been closed. The procedure is the same as that used in Section 7.1; we use circuit analysis to derive the
differential equation that describes the circuit in terms of the variable of interest, and then we use elementary calculus to solve the equation.

After the switch in Fig. 7.16 has been closed, Kirchhoff's voltage law requires that

$$
\begin{equation*}
V_{s}=R i+L \frac{d i}{d t} \tag{7.29}
\end{equation*}
$$

which can be solved for the current by separating the variables $i$ and $t$ and then integrating. The first step in this approach is to solve Eq. 7.29 for the derivative $d i / d t$ :

$$
\begin{equation*}
\frac{d i}{d t}=\frac{-R i+V_{s}}{L}=\frac{-R}{L}\left(i-\frac{V_{s}}{R}\right) \tag{7.30}
\end{equation*}
$$

Next, we multiply both sides of Eq. 7.30 by a differential time $d t$. This step reduces the left-hand side of the equation to a differential change in the current. Thus

$$
\begin{equation*}
\frac{d i}{d t} d t=\frac{-R}{L}\left(i-\frac{V_{s}}{R}\right) d t \tag{7.31}
\end{equation*}
$$

or

$$
d i=\frac{-R}{L}\left(i-\frac{V_{s}}{R}\right) d t
$$

We now separate the variables in Eq. 7.31 to get

$$
\begin{equation*}
\frac{d i}{i-\left(V_{s} / R\right)}=\frac{-R}{L} d t \tag{7.32}
\end{equation*}
$$

and then integrate both sides of Eq. 7.32. Using $x$ and $y$ as variables for the integration, we obtain

$$
\begin{equation*}
\int_{I_{0}}^{i(t)} \frac{d x}{x-\left(V_{s} / R\right)}=\frac{-R}{L} \int_{0}^{t} d y \tag{7.33}
\end{equation*}
$$

where $I_{0}$ is the current at $t=0$ and $i(t)$ is the current at any $t>0$. Performing the integration called for in Eq. 7.33 generates the expression

$$
\begin{equation*}
\ln \frac{i(t)-\left(V_{s} / R\right)}{I_{0}-\left(V_{s} / R\right)}=\frac{-R}{L} t \tag{7.34}
\end{equation*}
$$

from which

$$
\frac{i(t)-\left(V_{s} / R\right)}{I_{0}-\left(V_{s} / R\right)}=e^{-(R / L) t}
$$

or

$$
\begin{equation*}
i(t)=\frac{V_{s}}{R}+\left(I_{0}-\frac{V_{s}}{R}\right) e^{-(R / L) t} \tag{7.35}
\end{equation*}
$$

Step response of RL circuit

When the initial energy in the inductor is zero, $I_{0}$ is zero. Thus Eq. 7.35 reduces to

$$
\begin{equation*}
i(t)=\frac{V_{s}}{R}-\frac{V_{s}}{R} e^{-(R / L) t} \tag{7.36}
\end{equation*}
$$

Equation 7.36 indicates that after the switch has been closed, the current increases exponentially from zero to a final value of $V_{s} / R$. The time constant of the circuit, $L / R$, determines the rate of increase. One time
image_name:Figure 7.17
description:The graph in Figure 7.17 illustrates the step response of an RL circuit with the initial inductor current $I_0 = 0$. It is a time-domain waveform plot depicting the current $i(t)$ on the vertical axis and time $t$ on the horizontal axis. The vertical axis is labeled with current values, starting from 0 up to $\frac{V_s}{R}$, with a significant marker at $0.632\frac{V_s}{R}$. The horizontal axis is marked in terms of time constants, $\tau$, ranging from 0 to $5\tau$.

The graph shows an exponential increase in current from zero, asymptotically approaching its final steady-state value of $\frac{V_s}{R}$. At $t = \tau$, the current reaches approximately $63.2\%$ of its final value, which is a characteristic of first-order systems.

The curve is described by the function $i(t) = \frac{V_s}{R} - \frac{V_s}{R} e^{-t/\tau}$, showing an initial rapid increase that gradually slows as it approaches the final value. A dashed line at $\frac{V_s}{R}$ indicates the final steady-state current, and another dashed line at $0.632\frac{V_s}{R}$ highlights the current value at one time constant $\tau$.

A tangent line at $t=0$ with a slope of $\frac{V_s}{L}$ represents the initial rate of change of current, indicating how quickly the current begins to rise immediately after the switch is closed.


Figure $7.17 \triangle$ The step response of the $R L$ circuit shown in Fig. 7.16 when $I_{0}=0$.
image_name:Figure 7.18
description:The graph in Figure 7.18 is a time-domain waveform illustrating the voltage across an inductor in an RL circuit. The x-axis represents time, labeled \( t \), and is marked in increments of \( \tau \) (the time constant of the circuit). The y-axis represents voltage, labeled \( v \), with units in volts.

Overal Behavior and Trends:
The graph shows an exponential decay of the inductor voltage over time. Initially, at \( t = 0 \), the voltage is at its maximum value, \( V_s \). As time progresses, the voltage decreases exponentially towards zero.

Key Features and Technical Details:
- **Initial Voltage:** At \( t = 0 \), the voltage is \( V_s \).
- **Exponential Decay:** The voltage decays according to the equation \( v = V_s e^{-(R/L)t} \), showing a characteristic exponential decay behavior.
- **Tangent Line:** A tangent line at \( t = 0 \) with the equation \( v = V_s - \frac{R}{L}V_s t \) indicates the initial rate of change of the voltage.
- **Voltage at One Time Constant (\( \tau \)):** At \( t = \tau \), the voltage drops to approximately \( 0.368 V_s \), highlighted by a dashed horizontal line.

Annotations and Specific Data Points:
- **Equation Annotations:** The graph includes annotations showing the exponential decay equation \( v = V_s e^{-(R/L)t} \) and the tangent line equation.
- **Voltage Level at \( \tau \):** A dashed line marks the voltage level at \( 0.368 V_s \) at \( t = \tau \).

The graph effectively illustrates the transient response of the inductor voltage in an RL circuit, emphasizing the exponential decay and initial rate of change at the moment the switch is closed.


Figure 7.18 $\triangle$ Inductor voltage versus time.
constant after the switch has been closed, the current will have reached approximately $63 \%$ of its final value, or

$$
\begin{equation*}
i(\tau)=\frac{V_{s}}{R}-\frac{V_{s}}{R} e^{-1} \approx 0.6321 \frac{V_{s}}{R} \tag{7.37}
\end{equation*}
$$

If the current were to continue to increase at its initial rate, it would reach its final value at $t=\tau$; that is, because

$$
\begin{equation*}
\frac{d i}{d t}=\frac{-V_{s}}{R}\left(\frac{-1}{\tau}\right) e^{-t / \tau}=\frac{V_{s}}{L} e^{-t / \tau} \tag{7.38}
\end{equation*}
$$

the initial rate at which $i(t)$ increases is

$$
\begin{equation*}
\frac{d i}{d t}(0)=\frac{V_{s}}{L} \tag{7.39}
\end{equation*}
$$

If the current were to continue to increase at this rate, the expression for $i$ would be

$$
\begin{equation*}
i=\frac{V_{s}}{L} t \tag{7.40}
\end{equation*}
$$

from which, at $t=\tau$,

$$
\begin{equation*}
i=\frac{V_{s}}{L} \frac{L}{R}=\frac{V_{s}}{R} \tag{7.41}
\end{equation*}
$$

Equations 7.36 and 7.40 are plotted in Fig. 7.17. The values given by Eqs. 7.37 and 7.41 are also shown in this figure.

The voltage across an inductor is $L d i / d t$, so from Eq. 7.35 , for $t \geq 0^{+}$,

$$
\begin{equation*}
v=L\left(\frac{-R}{L}\right)\left(I_{0}-\frac{V_{s}}{R}\right) e^{-(R / L) t}=\left(V_{s}-I_{0} R\right) e^{-(R / L) t} \tag{7.42}
\end{equation*}
$$

The voltage across the inductor is zero before the switch is closed. Equation 7.42 indicates that the inductor voltage jumps to $V_{s}-I_{0} R$ at the instant the switch is closed and then decays exponentially to zero.

Does the value of $v$ at $t=0^{+}$make sense? Because the initial current is $I_{0}$ and the inductor prevents an instantaneous change in current, the current is $I_{0}$ in the instant after the switch has been closed. The voltage drop across the resistor is $I_{0} R$, and the voltage impressed across the inductor is the source voltage minus the voltage drop, that is, $V_{s}-I_{0} R$.

When the initial inductor current is zero, Eq. 7.42 simplifies to

$$
\begin{equation*}
v=V_{s} e^{-(R / L) t} \tag{7.43}
\end{equation*}
$$

If the initial current is zero, the voltage across the inductor jumps to $V_{s}$. We also expect the inductor voltage to approach zero as $t$ increases, because the current in the circuit is approaching the constant value of $V_{s} / R$. Figure 7.18 shows the plot of Eq. 7.43 and the relationship between the time constant and the initial rate at which the inductor voltage is decreasing.

If there is an initial current in the inductor, Eq. 7.35 gives the solution for it. The algebraic sign of $I_{0}$ is positive if the initial current is in the same direction as $i$; otherwise, $I_{0}$ carries a negative sign. Example 7.5 illustrates the application of Eq. 7.35 to a specific circuit.

#### Example 7.5 Determining the Step Response of an RL Circuit

The switch in the circuit shown in Fig. 7.19 has been in position a for a long time. At $t=0$, the switch moves from position a to position b . The switch is a make-before-break type; that is, the connection at position b is established before the connection at position a is broken, so there is no interruption of current through the inductor.
a) Find the expression for $i(t)$ for $t \geq 0$.
b) What is the initial voltage across the inductor just after the switch has been moved to position b ?
c) How many milliseconds after the switch has been moved does the inductor voltage equal 24 V ?
d) Does this initial voltage make sense in terms of circuit behavior?
e) Plot both $i(t)$ and $v(t)$ versus $t$.
image_name:Figure 7.19 A
description:
[
'name': 'Vi', 'type': 'VoltageSource', 'value': '24 V', 'ports': {'Np': 'Vi', 'Nn': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': '2 Ω', 'ports': {'N1': 'Vi', 'N2': 'b'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'V', 'N2': 'a','N3':'b'
'name': 'L1', 'type': 'Inductor', 'value': '200 mH', 'ports': {'N1': 'V', 'N2': 'GND'
'name': 'R2', 'type': 'Resistor', 'value': '10 Ω', 'ports': {'N1': 'X', 'N2': 'GND'
'name': 'I1', 'type': 'CurrentSource', 'value': '8 A', 'ports': {'Np': 'X', 'Nn': 'GND'
]
extrainfo:The circuit includes a switch SW1 that changes position at t=0 from 'a' to 'b', altering the path of current through the inductor L1. Initially, the inductor current is 8 A, opposing the reference direction for i. The final current value is 12 A, with a time constant of 100 ms.


Figure 7.19 A The circuit for Example 7.5.

#### Solution

a) The switch has been in position a for a long time, so the 200 mH inductor is a short circuit across the 8 A current source. Therefore, the inductor carries an initial current of 8 A . This current is oriented opposite to the reference direction for $i$; thus $I_{0}$ is -8 A . When the switch is in position b , the final value of $i$ will be $24 / 2$, or 12 A . The time constant of the circuit is $200 / 2$, or 100 ms . Substituting these values into Eq. 7.35 gives

$$
\begin{aligned}
i & =12+(-8-12) e^{-t / 0.1} \\
& =12-20 e^{-10 t} \mathrm{~A}, \quad t \geq 0
\end{aligned}
$$

b) The voltage across the inductor is

$$
\begin{aligned}
v & =L \frac{d i}{d t} \\
& =0.2\left(200 e^{-10 t}\right) \\
& =40 e^{-10 t} \mathrm{~V}, \quad t \geq 0^{+}
\end{aligned}
$$

The initial inductor voltage is

$$
v\left(0^{+}\right)=40 \mathrm{~V}
$$

c) Yes; in the instant after the switch has been moved to position b, the inductor sustains a current of 8 A counterclockwise around the newly formed closed path. This current causes a 16 V drop across the $2 \Omega$ resistor. This voltage drop adds to the drop across the source, producing a 40 V drop across the inductor.
d) We find the time at which the inductor voltage equals 24 V by solving the expression

$$
24=40 e^{-10 t}
$$

for $t$ :

$$
\begin{aligned}
t & =\frac{1}{10} \ln \frac{40}{24} \\
& =51.08 \times 10^{-3} \\
& =51.08 \mathrm{~ms} .
\end{aligned}
$$

e) Figure 7.20 shows the graphs of $i(t)$ and $v(t)$ versus $t$. Note that the instant of time when the current equals zero corresponds to the instant of time when the inductor voltage equals the source voltage of 24 V , as predicted by Kirchhoff's voltage law.
image_name:Figure 7.20
description:The graph in Figure 7.20 is a time-domain waveform illustrating the behavior of current \(i(t)\) and voltage \(v(t)\) across an inductor over time \(t\), measured in milliseconds (ms). The horizontal axis represents time, ranging from 0 to 500 ms, while the vertical axis has two scales: voltage \(v\) in volts (V) on the left, and current \(i\) in amperes (A) on the right.

The voltage \(v(t)\), depicted by the black curve, starts at a value of 40 V at \(t = 0\) and shows an exponential decay towards zero as time progresses. Notably, the voltage reaches 24 V at approximately 51.08 ms, which corresponds to the calculated time when the inductor voltage equals the source voltage.

The current \(i(t)\), shown by the blue curve, begins at -8 A at \(t = 0\) and increases exponentially towards zero as time increases. This behavior aligns with the step response of an RL circuit, where the current eventually stabilizes.

Key features include the zero-crossing point of the current, which coincides with the voltage reaching the source voltage of 24 V, as predicted by Kirchhoff's voltage law. The graph visually demonstrates the transient response of an RL circuit, highlighting the interplay between voltage and current over time.


Figure 7.20 A The current and voltage waveforms for Example 7.5.

ASSESSMENT PROBLEM

Objective 2-Be able to determine the step response of both RL and RC circuits

7.5 Assume that the switch in the circuit shown in Fig. 7.19 has been in position $b$ for a long time, and at $t=0$ it moves to position a. Find
(a) $i\left(0^{+}\right)$; (b) $v\left(0^{+}\right)$; (c) $\tau, t>0$
; (d) $i(t), t \geq 0$;
and (e) $v(t), t \geq 0^{+}$.

Answer: (a) 12 A ;
(b) -200 V ;
(c) 20 ms ;
(d) $-8+20 e^{-50 t} \mathrm{~A}, t \geq 0$;
(e) $-200 e^{-50 t} \mathrm{~V}, t \geq 0^{+}$.

NOTE: Also try Chapter Problems 7.35-7.37.

We can also describe the voltage $v(t)$ across the inductor in Fig. 7.16 directly, not just in terms of the circuit current. We begin by noting that the voltage across the resistor is the difference between the source voltage and the inductor voltage. We write

$$
\begin{equation*}
i(t)=\frac{V_{s}}{R}-\frac{v(t)}{R} \tag{7.44}
\end{equation*}
$$

where $V_{s}$ is a constant. Differentiating both sides with respect to time yields

$$
\begin{equation*}
\frac{d i}{d t}=-\frac{1}{R} \frac{d v}{d t} \tag{7.45}
\end{equation*}
$$

Then, if we multiply each side of Eq. 7.45 by the inductance $L$, we get an expression for the voltage across the inductor on the left-hand side, or

$$
\begin{equation*}
v=-\frac{L}{R} \frac{d v}{d t} \tag{7.46}
\end{equation*}
$$

Putting Eq. 7.46 into standard form yields

$$
\begin{equation*}
\frac{d v}{d t}+\frac{R}{L} v=0 \tag{7.47}
\end{equation*}
$$

You should verify (in Problem 7.38) that the solution to Eq. 7.47 is identical to that given in Eq. 7.42.

At this point, a general observation about the step response of an $R L$ circuit is pertinent. (This observation will prove helpful later.) When we derived the differential equation for the inductor current, we obtained Eq. 7.29. We now rewrite Eq. 7.29 as

$$
\begin{equation*}
\frac{d i}{d t}+\frac{R}{L} i=\frac{V_{s}}{L} \tag{7.48}
\end{equation*}
$$

Observe that Eqs. 7.47 and 7.48 have the same form. Specifically, each equates the sum of the first derivative of the variable and a constant times the variable to a constant value. In Eq. 7.47, the constant on the right-hand side happens to be zero; hence this equation takes on the same form as the natural response equations in Section 7.1. In both Eq. 7.47 and Eq. 7.48, the constant multiplying the dependent variable is the reciprocal of the time constant, that is, $R / L=1 / \tau$. We encounter a similar situation in the derivations for the step response of an $R C$ circuit. In Section 7.4, we will use these observations to develop a general approach to finding the natural and step responses of $R L$ and $R C$ circuits.

The Step Response of an RC Circuit

We can find the step response of a first-order $R C$ circuit by analyzing the circuit shown in Fig. 7.21. For mathematical convenience, we choose the Norton equivalent of the network connected to the equivalent capacitor. Summing the currents away from the top node in Fig. 7.21 generates the differential equation

$$
\begin{equation*}
C \frac{d v_{C}}{d t}+\frac{v_{C}}{R}=I_{s} \tag{7.49}
\end{equation*}
$$

Division of Eq. 7.49 by $C$ gives

$$
\begin{equation*}
\frac{d v_{C}}{d t}+\frac{v_{C}}{R C}=\frac{I_{s}}{C} \tag{7.50}
\end{equation*}
$$

Comparing Eq. 7.50 with Eq. 7.48 reveals that the form of the solution for $v_{C}$ is the same as that for the current in the inductive circuit, namely, Eq. 7.35. Therefore, by simply substituting the appropriate variables and coefficients, we can write the solution for $v_{C}$ directly. The translation requires that $I_{s}$ replace $V_{s}, C$ replace $L, 1 / R$ replace $R$, and $V_{0}$ replace $I_{0}$. We get

$$
\begin{equation*}
v_{C}=I_{s} R+\left(V_{0}-I_{s} R\right) e^{-t / R C}, \quad t \geq 0 \tag{7.51}
\end{equation*}
$$

A similar derivation for the current in the capacitor yields the differential equation

$$
\begin{equation*}
\frac{d i}{d t}+\frac{1}{R C} i=0 \tag{7.52}
\end{equation*}
$$

Equation 7.52 has the same form as Eq. 7.47 , hence the solution for $i$ is obtained by using the same translations used for the solution of Eq. 7.50. Thus

$$
\begin{equation*}
i=\left(I_{s}-\frac{V_{0}}{R}\right) e^{-t / R C}, \quad t \geq 0^{+} \tag{7.53}
\end{equation*}
$$

where $V_{0}$ is the initial value of $v_{C}$, the voltage across the capacitor.
We obtained Eqs. 7.51 and 7.53 by using a mathematical analogy to the solution for the step response of the inductive circuit. Let's see whether these solutions for the $R C$ circuit make sense in terms of known circuit behavior. From Eq. 7.51, note that the initial voltage across the capacitor is $V_{0}$, the final voltage across the capacitor is $I_{s} R$, and the time constant of the circuit is $R C$. Also note that the solution for $v_{C}$ is valid for $t \geq 0$. These observations are consistent with the behavior of a capacitor in parallel with a resistor when driven by a constant current source.

Equation 7.53 predicts that the current in the capacitor at $t=0^{+}$is $I_{s}-V_{0} / R$. This prediction makes sense because the capacitor voltage cannot change instantaneously, and therefore the initial current in the resistor is $V_{0} / R$. The capacitor branch current changes instantaneously from zero at $t=0^{-}$to $I_{s}-V_{0} / R$ at $t=0^{+}$. The capacitor current is zero at $t=\infty$. Also note that the final value of $v=I_{s} R$.

Example 7.6 illustrates how to use Eqs. 7.51 and 7.53 to find the step response of a first-order $R C$ circuit.
image_name:Figure 7.21
description:
[
'name': 'Is', 'type': 'CurrentSource', 'ports': {'Np': 'GND', 'Nn': 'X1'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'VC', 'Nn': 'GND'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'X1', 'N2': 'VC'
]
extrainfo:The circuit is a first-order RC circuit used to illustrate the step response when the switch SW1 changes position at t=0. The current source Is provides current to the circuit, and the resistor R and capacitor C form the RC network. Initially, the switch is open, and at t=0, it closes, changing the circuit dynamics.


Figure $7.21 \stackrel{A N D}{A}$ circuit used to illustrate the step response of a first-order RC circuit.

#### Example 7.6 Determining the Step Response of an RC Circuit

The switch in the circuit shown in Fig. 7.22 has been in position 1 for a long time. At $t=0$, the switch moves to position 2. Find
a) $v_{o}(t)$ for $t \geq 0$ and
b) $i_{o}(t)$ for $t \geq 0^{+}$.
image_name:Figure 7.22
description:
[
'name': 'R1', 'type': 'Resistor', 'value': '20k', 'ports': {'N1': '3', 'N2': '1'
'name': 'R2', 'type': 'Resistor', 'value': '60k', 'ports': {'N1': '1', 'N2': 'GND'
'name': 'C1', 'type': 'Capacitor', 'value': '0.25uF', 'ports': {'Np': 'V0', 'Nn': 'GND'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'V0', 'N2': '1','N3':'2'
'name': 'R3', 'type': 'Resistor', 'value': '8k', 'ports': {'N1': '2', 'N2': '4'
'name': 'R4', 'type': 'Resistor', 'value': '40k', 'ports': {'N1': '4', 'N2': '5'
'name': 'R5', 'type': 'Resistor', 'value': '160k', 'ports': {'N1': '4', 'N2': 'GND'
'name': 'V1', 'type': 'VoltageSource', 'value': '40V', 'ports': {'Np': '3', 'Nn': 'GND'
'name': 'V2', 'type': 'VoltageSource', 'value': '75V', 'ports': {'Np': 'GND', 'Nn': '5'
]
extrainfo:The circuit consists of a switch SW1 that changes the configuration of the circuit at t=0, affecting the voltage across the capacitor C1 and the current through resistor R3. Initially, the switch is in position 1, and at t=0 it moves to position 2, causing a step response in the RC network.


Figure 7.22 - The circuit for Example 7.6.

#### Solution

a) The switch has been in position 1 for a long time, so the initial value of $v_{o}$ is $40(60 / 80)$, or 30 V . To take advantage of Eqs. 7.51 and 7.53 , we find the Norton equivalent with respect to the terminals of the capacitor for $t \geq 0$. To do this, we begin by computing the open-circuit voltage, which is given by the -75 V source divided across the $40 \mathrm{k} \Omega$ and $160 \mathrm{k} \Omega$ resistors:

$$
V_{\mathrm{oc}}=\frac{160 \times 10^{3}}{(40+160) \times 10^{3}}(-75)=-60 \mathrm{~V}
$$

Next, we calculate the Thévenin resistance, as seen to the right of the capacitor, by shorting the -75 V source and making series and parallel combinations of the resistors:

$$
R_{\mathrm{Th}}=8000+40,000 \| 160,000=40 \mathrm{k} \Omega
$$

The value of the Norton current source is the ratio of the open-circuit voltage to the Thévenin resistance, or $-60 /\left(40 \times 10^{3}\right)=-1.5 \mathrm{~mA}$. The resulting Norton equivalent circuit is shown in Fig. 7.23. From Fig. 7.23, $I_{s} R=-60 \mathrm{~V}$ and $R C=10 \mathrm{~ms}$. We have already noted that $v_{o}(0)=30 \mathrm{~V}$, so the solution for $v_{o}$ is

$$
\begin{aligned}
v_{o} & =-60+[30-(-60)] e^{-100 t} \\
& =-60+90 e^{-100 t} \mathrm{~V}, \quad t \geq 0
\end{aligned}
$$

b) We write the solution for $i_{o}$ directly from Eq. 7.53 by noting that $I_{s}=-1.5 \mathrm{~mA}$ and $V_{o} / R=(30 / 40) \times 10^{-3}$, or 0.75 mA :

$$
i_{o}=-2.25 e^{-100 t} \mathrm{~mA}, \quad t \geq 0^{+}
$$

We check the consistency of the solutions for $v_{o}$ and $i_{o}$ by noting that

$$
\begin{aligned}
i_{o} & =C \frac{d v_{o}}{d t}=\left(0.25 \times 10^{-6}\right)\left(-9000 e^{-100 t}\right) \\
& =-2.25 e^{-100 t} \mathrm{~mA}
\end{aligned}
$$

Because $d v_{o}\left(0^{-}\right) / d t=0$, the expression for $i_{o}$ clearly is valid only for $t \geq 0^{+}$.
image_name:Figure 7.23
description:
[
'name': '0.25μF', 'type': 'Capacitor', 'value': '0.25μF', 'ports': {'Np': 'Vin', 'Nn': 'GND'
'name': '40kΩ', 'type': 'Resistor', 'value': '40kΩ', 'ports': {'N1': 'Vin', 'N2': 'GND'
'name': '1.5mA', 'type': 'CurrentSource', 'value': '1.5mA', 'ports': {'Np': 'Vin', 'Nn': 'GND'
]
extrainfo:The circuit consists of a voltage source, a capacitor, a resistor, and a current source all connected in parallel between Vin and GND.


Figure 7.23 $\triangle$ The equivalent circuit for $t>0$ for the circuit shown in Fig. 7.22.

ASSESSMENT PROBLEM

Objective 2-Be able to determine the step response of both RL and RC circuits

7.6 a) Find the expression for the voltage across the $160 \mathrm{k} \Omega$ resistor in the circuit shown in Fig. 7.22. Let this voltage be denoted $v_{A}$, and assume that the reference polarity for the voltage is positive at the upper terminal of the $160 \mathrm{k} \Omega$ resistor.

NOTE: Also try Chapter Problems 7.53 and 7.54.

## 7.4 A General Solution for Step and Natural Responses

The general approach to finding either the natural response or the step response of the first-order $R L$ and $R C$ circuits shown in Fig. 7.24 is based on their differential equations having the same form (compare Eq. 7.48 and Eq. 7.50). To generalize the solution of these four possible circuits, we let $x(t)$ represent the unknown quantity, giving $x(t)$ four possible values. It can represent the current or voltage at the terminals of an inductor or the current or voltage at the terminals of a capacitor. From Eqs. 7.47, 7.48, 7.50 , and 7.52 , we know that the differential equation describing any one of the four circuits in Fig. 7.24 takes the form

$$
\begin{equation*}
\frac{d x}{d t}+\frac{x}{\tau}=K \tag{7.54}
\end{equation*}
$$

where the value of the constant $K$ can be zero. Because the sources in the circuit are constant voltages and/or currents, the final value of $x$ will be constant; that is, the final value must satisfy Eq. 7.54, and, when $x$ reaches its final value, the derivative $d x / d t$ must be zero. Hence

$$
\begin{equation*}
x_{f}=K \tau \tag{7.55}
\end{equation*}
$$

where $x_{f}$ represents the final value of the variable.
We solve Eq. 7.54 by separating the variables, beginning by solving for the first derivative:

$$
\begin{equation*}
\frac{d x}{d t}=\frac{-x}{\tau}+K=\frac{-(x-K \tau)}{\tau}=\frac{-\left(x-x_{f}\right)}{\tau} \tag{7.56}
\end{equation*}
$$

b) Specify the interval of time for which the expression obtained in (a) is valid.

Answer:
(a) $-60+72 e^{-100 t} \mathrm{~V}$;
(b) $t \geq 0^{+}$.

General solution for natural and step responses of $R L$ and $R C$ circuits -

Calculating the natural or step response of $R L$ or $R C$ circuits

In writing Eq. 7.56 , we used Eq. 7.55 to substitute $x_{f}$ for $K \tau$. We now multiply both sides of Eq. 7.56 by $d t$ and divide by $x-x_{f}$ to obtain

$$
\begin{equation*}
\frac{d x}{x-x_{f}}=\frac{-1}{\tau} d t \tag{7.57}
\end{equation*}
$$

Next, we integrate Eq. 7.57. To obtain as general a solution as possible, we use time $t_{0}$ as the lower limit and $t$ as the upper limit. Time $t_{0}$ corresponds to the time of the switching or other change. Previously we assumed that $t_{0}=0$, but this change allows the switching to take place at any time. Using $u$ and $v$ as symbols of integration, we get

$$
\begin{equation*}
\int_{x\left(t_{0}\right)}^{x(t)} \frac{d u}{u-x_{f}}=-\frac{1}{\tau} \int_{t_{0}}^{t} d v \tag{7.58}
\end{equation*}
$$

Carrying out the integration called for in Eq. 7.58 gives

$$
\begin{equation*}
x(t)=x_{f}+\left[x\left(t_{0}\right)-x_{f}\right] e^{-\left(t-t_{0}\right) / \tau} \tag{7.59}
\end{equation*}
$$

The importance of Eq. 7.59 becomes apparent if we write it out in words:

$$
\begin{array}{lr}
\text { the unknown } & \text { the final } \\
\text { variable as a } & =\text { value of the } \\
\text { function of time } & \text { variable } \\
+\left[\begin{array}{rr}
\text { the initial } & \text { the final } \\
\text { value of the } & - \text { value of the } \\
\text { variable } & \text { variable }
\end{array}\right] \times e \frac{-[t-\text { (time of switching) }]}{\text { (time constant) }} \tag{7.60}
\end{array}
$$

In many cases, the time of switching-that is, $t_{0}$-is zero.
When computing the step and natural responses of circuits, it may help to follow these steps:

1. Identify the variable of interest for the circuit. For $R C$ circuits, it is most convenient to choose the capacitive voltage; for $R L$ circuits, it is best to choose the inductive current.
2. Determine the initial value of the variable, which is its value at $t_{0}$. Note that if you choose capacitive voltage or inductive current as your variable of interest, it is not necessary to distinguish between $t=t_{0}^{-}$and $t=t_{0}^{+}$. This is because they both are continuous variables. If you choose another variable, you need to remember that its initial value is defined at $t=t_{0}^{+}$.
3. Calculate the final value of the variable, which is its value as $t \rightarrow \infty$.
4. Calculate the time constant for the circuit.

With these quantities, you can use Eq. 7.60 to produce an equation describing the variable of interest as a function of time. You can then find equations for other circuit variables using the circuit analysis techniques introduced in Chapters 3 and 4 or by repeating the preceding steps for the other variables.

Examples 7.7-7.9 illustrate how to use Eq. 7.60 to find the step response of an $R C$ or $R L$ circuit.

[^1]
#### Example 7.7 Using the General Solution Method to Find an RC Circuit's Step Response

The switch in the circuit shown in Fig. 7.25 has been in position a for a long time. At $t=0$ the switch is moved to position b.
a) What is the initial value of $v_{C}$ ?
b) What is the final value of $v_{C}$ ?
c) What is the time constant of the circuit when the switch is in position b?
d) What is the expression for $v_{C}(t)$ when $t \geq 0$ ?
e) What is the expression for $i(t)$ when $t \geq 0^{+}$?
f) How long after the switch is in position b does the capacitor voltage equal zero?
g) Plot $v_{C}(t)$ and $i(t)$ versus $t$.

#### Solution

a) The switch has been in position a for a long time, so the capacitor looks like an open circuit. Therefore the voltage across the capacitor is the voltage across the $60 \Omega$ resistor. From the voltagedivider rule, the voltage across the $60 \Omega$ resistor is $40 \times[60 /(60+20)]$, or 30 V . As the reference for $v_{C}$ is positive at the upper terminal of the capacitor, we have $v_{C}(0)=-30 \mathrm{~V}$.
b) After the switch has been in position b for a long time, the capacitor will look like an open circuit in terms of the 90 V source. Thus the final value of the capacitor voltage is +90 V .
c) The time constant is

$$
\begin{aligned}
\tau & =R C \\
& =\left(400 \times 10^{3}\right)\left(0.5 \times 10^{-6}\right) \\
& =0.2 \mathrm{~s}
\end{aligned}
$$

d) Substituting the appropriate values for $v_{f}, v(0)$, and $t$ into Eq. 7.60 yields

$$
\begin{aligned}
v_{C}(t) & =90+(-30-90) e^{-5 t} \\
& =90-120 e^{-5 t} \mathrm{~V}, \quad t \geq 0
\end{aligned}
$$

e) Here the value for $\tau$ doesn't change. Thus we need to find only the initial and final values for the current in the capacitor. When obtaining the initial value, we must get the value of $i\left(0^{+}\right)$, because the current in the capacitor can change instantaneously. This current is equal to the current in the resistor, which from Ohm's law is $[90-(-30)] /\left(400 \times 10^{3}\right)=300 \mu \mathrm{~A}$. Note that when applying Ohm's law we recognized that the
image_name:Figure 7.25 A
description:
[
'name': 'Vi', 'type': 'VoltageSource', 'value': '90 V', 'ports': {'Np': 'Vi', 'Nn': 'GND'
'name': '400 kΩ', 'type': 'Resistor', 'value': '400 kΩ', 'ports': {'N1': 'Vi', 'N2': 'b'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'Vc', 'N2': 'b','N3':'a'
'name': 'Vc', 'type': 'Capacitor', 'value': '0.5 μF', 'ports': {'Np': 'Vc', 'Nn': 'GND'
'name': '60 Ω', 'type': 'Resistor', 'value': '60 Ω', 'ports': {'N1': 'a', 'N2': 'GND'
'name': '20 Ω', 'type': 'Resistor', 'value': '20 Ω', 'ports': {'N1': 'a', 'N2': 'Vx'
'name': 'Vx', 'type': 'VoltageSource', 'value': '40 V', 'ports': {'Np': 'Vx', 'Nn': 'GND'
]
extrainfo:This circuit includes a voltage source Vi of 90 V, a capacitor Vc of 0.5 μF, a switch SW1, and resistors of 400 kΩ, 60 Ω, and 20 Ω. The circuit is grounded at multiple points. The voltage source Vx is 40 V.


Figure 7.25 A The circuit for Example 7.7.
capacitor voltage cannot change instantaneously. The final value of $i(t)=0$, so

$$
\begin{aligned}
i(t) & =0+(300-0) e^{-5 t} \\
& =300 e^{-5 t} \mu \mathrm{~A}, \quad t \geq 0^{+}
\end{aligned}
$$

We could have obtained this solution by differentiating the solution in (d) and multiplying by the capacitance. You may want to do so for yourself. Note that this alternative approach to finding $i(t)$ also predicts the discontinuity at $t=0$.
f) To find how long the switch must be in position $b$ before the capacitor voltage becomes zero, we solve the equation derived in (d) for the time when $v_{C}(t)=0$ :

$$
120 e^{-5 t}=90 \quad \text { or } \quad e^{5 t}=\frac{120}{90}
$$

so

$$
\begin{aligned}
t & =\frac{1}{5} \ln \left(\frac{4}{3}\right) \\
& =57.54 \mathrm{~ms}
\end{aligned}
$$

Note that when $v_{C}=0, i=225 \mu \mathrm{~A}$ and the voltage drop across the $400 \mathrm{k} \Omega$ resistor is 90 V .
g) Figure 7.26 shows the graphs of $v_{C}(t)$ and $i(t)$ versus $t$.
image_name:Figure 7.26
description:The graph in Figure 7.26 presents two waveforms, the capacitor voltage \( v_C(t) \) in volts and the current \( i(t) \) in microamperes, both plotted against time \( t \) in milliseconds.

**Type of Graph and Function:**
This is a time-domain waveform graph illustrating the exponential decay of current and the corresponding rise of voltage across a capacitor over time.

**Axes Labels and Units:**
- The horizontal axis represents time \( t \) in milliseconds (ms).
- The left vertical axis represents the current \( i \) in microamperes (µA), ranging from -20 µA to 300 µA.
- The right vertical axis represents the capacitor voltage \( v_C \) in volts (V), ranging from -30 V to 120 V.

**Overall Behavior and Trends:**
- The current \( i(t) \) starts at a high value around 225 µA and exponentially decays towards zero as time progresses.
- The capacitor voltage \( v_C(t) \) starts at zero and increases exponentially, approaching a maximum value of 120 V.
- Both waveforms exhibit typical exponential behavior, characteristic of charging and discharging in RC circuits.

**Key Features and Technical Details:**
- The current \( i(t) \) crosses the zero line at approximately 57.54 ms, which is consistent with the time calculated for the capacitor voltage to reach zero.
- The voltage \( v_C(t) \) rises steadily and approaches its final value asymptotically, indicating the capacitor is charging over time.

**Annotations and Specific Data Points:**
- The graph includes reference lines for current and voltage, showing their respective scales.
- The intersection of the current line with the zero line is a critical point, marking the time when the capacitor voltage becomes zero, which is approximately 57.54 ms.


Figure 7.26 $\triangle$ The current and voltage waveforms for Example 7.7.

#### Example 7.8 Using the General Solution Method with Zero Initial Conditions

The switch in the circuit shown in Fig. 7.27 has been open for a long time. The initial charge on the capacitor is zero. At $t=0$, the switch is closed. Find the expression for
a) $i(t)$ for $t \geq 0^{+}$and
b) $v(t)$ when $t \geq 0^{+}$.
image_name:Figure 7.27
description:
[
'name': '7.5 mA', 'type': 'CurrentSource', 'value': '7.5 mA', 'ports': {'Np': 'GND', 'Nn': 'V(t)'
'name': '20 kΩ', 'type': 'Resistor', 'value': '20 kΩ', 'ports': {'N1': 'V(t)', 'N2': 'GND'
'name': '0.1 μF', 'type': 'Capacitor', 'value': '0.1 μF', 'ports': {'Np': 'V(t)', 'Nn': 'Vo'
'name': '30 kΩ', 'type': 'Resistor', 'value': '30 kΩ', 'ports': {'N1': 'Vo', 'N2': 'GND'
]
extrainfo:The circuit consists of a current source, a resistor, a capacitor, and another resistor connected in series. The switch closes at t=0, initiating the transient analysis of the circuit.


Figure 7.27 A The circuit for Example 7.8.

#### Solution

a) Because the initial voltage on the capacitor is zero, at the instant when the switch is closed the current in the $30 \mathrm{k} \Omega$ branch will be

$$
\begin{aligned}
i\left(0^{+}\right) & =\frac{(7.5)(20)}{50} \\
& =3 \mathrm{~mA}
\end{aligned}
$$

The final value of the capacitor current will be zero because the capacitor eventually will appear as an open circuit in terms of dc current. Thus $i_{f}=0$. The time constant of the circuit will equal the product of the Thévenin resistance (as seen from the capacitor) and the capacitance.

Therefore $\tau=(20+30) 10^{3}(0.1) \times 10^{-6}=5 \mathrm{~ms}$. Substituting these values into Eq. 7.60 generates the expression

$$
\begin{aligned}
i(t) & =0+(3-0) e^{-t / 5 \times 10^{-3}} \\
& =3 e^{-200 t} \mathrm{~mA}, \quad t \geq 0^{+}
\end{aligned}
$$

b) To find $v(t)$, we note from the circuit that it equals the sum of the voltage across the capacitor and the voltage across the $30 \mathrm{k} \Omega$ resistor. To find the capacitor voltage (which is a drop in the direction of the current), we note that its initial value is zero and its final value is (7.5)(20), or 150 V . The time constant is the same as before, or 5 ms . Therefore we use Eq. 7.60 to write

$$
\begin{aligned}
v_{C}(t) & =150+(0-150) e^{-200 t} \\
& =\left(150-150 e^{-200 t}\right) \mathrm{V}, \quad t \geq 0
\end{aligned}
$$

Hence the expression for the voltage $v(t)$ is

$$
\begin{aligned}
v(t) & =150-150 e^{-200 t}+(30)(3) e^{-200 t} \\
& =\left(150-60 e^{-200 t}\right) \mathrm{V}, \quad t \geq 0^{+}
\end{aligned}
$$

As one check on this expression, note that it predicts the initial value of the voltage across the $20 \Omega$ resistor as $150-60$, or 90 V . The instant the switch is closed, the current in the $20 \mathrm{k} \Omega$ resistor is $(7.5)(30 / 50)$, or 4.5 mA . This current produces a 90 V drop across the $20 \mathrm{k} \Omega$ resistor, confirming the value predicted by the solution.

#### Example 7.9 Using the General Solution Method to Find an RL Circuit's Step Response

The switch in the circuit shown in Fig. 7.28 has been open for a long time. At $t=0$ the switch is closed. Find the expression for
a) $v(t)$ when $t \geq 0^{+}$and
b) $i(t)$ when $t \geq 0$.
image_name:Figure 7.28
description:
[
'name': 'Vi', 'type': 'VoltageSource', 'value': '20V', 'ports': {'Np': 'Vi', 'Nn': 'GND'
'name': '1Ω', 'type': 'Resistor', 'value': '1Ω', 'ports': {'N1': 'Vi', 'N2': 'X1'
'name': '3Ω', 'type': 'Resistor', 'value': '3Ω', 'ports': {'N1': 'X1', 'N2': 'V(t)'
'name': '80mH', 'type': 'Inductor', 'value': '80mH', 'ports': {'N1': 'V(t)', 'N2': 'GND'
'name': 'SW', 'type': 'Switch', 'ports': {'N1': 'X1', 'N2': 'V(t)'
]
extrainfo:The circuit is an RL circuit with a switch that closes at t=0. The initial current in the inductor is 5 A, and it affects the voltage across the inductor. The time constant of the circuit is 80 ms.


Figure 7.28 ■ The circuit for Example 7.9.

#### Solution

a) The switch has been open for a long time, so the initial current in the inductor is 5 A , oriented from top to bottom. Immediately after the switch closes, the current still is 5 A , and therefore the initial voltage across the inductor becomes $20-5(1)$, or 15 V . The final value of the inductor voltage is 0 V . With the switch closed, the time constant is $80 / 1$, or 80 ms . We use Eq. 7.60 to write the expression for $v(t)$ :

$$
\begin{aligned}
v(t) & =0+(15-0) e^{-t / 80 \times 10^{-3}} \\
& =15 e^{-12.5 t} \mathrm{~V}, \quad t \geq 0^{+}
\end{aligned}
$$

b) We have already noted that the initial value of the inductor current is 5 A . After the switch has
been closed for a long time, the inductor current reaches $20 / 1$, or 20 A . The circuit time constant is 80 ms , so the expression for $i(t)$ is

$$
\begin{aligned}
i(t) & =20+(5-20) e^{-12.5 t} \\
& =\left(20-15 e^{-12.5 t}\right) \mathrm{A}, \quad t \geq 0
\end{aligned}
$$

We determine that the solutions for $v(t)$ and $i(t)$ agree by noting that

$$
\begin{aligned}
v(t) & =L \frac{d i}{d t} \\
& =80 \times 10^{-3}\left[15(12.5) e^{-12.5 t}\right] \\
& =15 e^{-12.5 t} \mathrm{~V}, \quad t \geq 0^{+}
\end{aligned}
$$

NOTE: Assess your understanding of the general solution method by trying Chapter Problems 7.51 and 7.53.

Example 7.10 shows that Eq. 7.60 can even be used to find the step response of some circuits containing magnetically coupled coils.

#### Example 7.10 Determining Step Response of a Circuit with Magnetically Coupled Coils

There is no energy stored in the circuit in Fig. 7.29 at the time the switch is closed.
a) Find the solutions for $i_{o}, v_{o}, i_{1}$, and $i_{2}$.
b) Show that the solutions obtained in (a) make sense in terms of known circuit behavior.

#### Solution

a) For the circuit in Fig. 7.29, the magnetically coupled coils can be replaced by a single inductor having an inductance of

$$
L_{\mathrm{eq}}=\frac{L_{1} L_{2}-M^{2}}{L_{1}+L_{2}-2 M}=\frac{45-36}{18-12}=1.5 \mathrm{H}
$$

(See Problem 6.41.) It follows that the circuit in Fig. 7.29 can be simplified as shown in Fig. 7.30.

By hypothesis the initial value of $i_{o}$ is zero. From Fig. 7.30 we see that the final value of $i_{o}$ will be $120 / 7.5$ or 16 A . The time constant of the circuit is $1.5 / 7.5$ or 0.2 s . It follows directly from Eq. 7.60 that

$$
i_{o}=16-16 e^{-5 t} \mathrm{~A}, \quad t \geq 0
$$

The voltage $v_{o}$ follows from Kirchhoff's voltage law. Thus,

$$
\begin{aligned}
v_{o} & =120-7.5 i_{o} \\
& =120 e^{-5 t} \mathrm{~V}, \quad t \geq 0^{+}
\end{aligned}
$$

To find $i_{1}$ and $i_{2}$ we first note from
Fig. 7.29 that

$$
3 \frac{d i_{1}}{d t}+6 \frac{d i_{2}}{d t}=6 \frac{d i_{1}}{d t}+15 \frac{d i_{2}}{d t}
$$

or

$$
\frac{d i_{1}}{d t}=-3 \frac{d i_{2}}{d t}
$$

image_name:Figure 7.29 A
description:
[
'name': 'Vi', 'type': 'VoltageSource', 'value': '120V', 'ports': {'Np': 'Vi', 'Nn': 'GND'
'name': '7.5 Ω', 'type': 'Resistor', 'value': '7.5 Ω', 'ports': {'N1': 'Vi', 'N2': 'X1'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'X1', 'N2': 'Vo'
'name': '3 H', 'type': 'Inductor', 'value': '3 H', 'ports': {'N1': 'Vo', 'N2': 'GND'
'name': '15 H', 'type': 'Inductor', 'value': '15 H', 'ports': {'N1': 'Vo', 'N2': 'GND'
]
extrainfo:The circuit consists of a voltage source, a resistor, a switch, and three inductors. The switch SW1 controls the connection between the resistor and the inductors. The inductors are arranged in parallel, sharing the same node Vo. The current io flows through the switch and into the node Vo, dividing into currents i1 and i2 through the inductors.


Figure 7.29 A The circuit for Example 7.10.
image_name:Figure 7.30 A
description:
[
'name': '120 V', 'type': 'VoltageSource', 'value': '120 V', 'ports': {'Np': 'Vi', 'Nn': 'GND'
'name': '7.5 Ω', 'type': 'Resistor', 'value': '7.5 Ω', 'ports': {'N1': 'Vi', 'N2': 'X1'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'X1', 'N2': 'Vo'
'name': '1.5 H', 'type': 'Inductor', 'value': '1.5 H', 'ports': {'N1': 'Vo', 'N2': 'GND'
]
extrainfo:The circuit consists of a 120 V voltage source connected to a 7.5 Ω resistor, which is in series with a switch (SW1). The switch controls the connection to a 1.5 H inductor. The inductor is connected in parallel to the ground. The current io flows through the switch into the node Vo.


Figure $7.30 \triangle$ The circuit in Fig. 7.29 with the magnetically coupled coils replaced by an equivalent coil.

It also follows from Fig. 7.29 that because $i_{o}=i_{1}+i_{2}$,

$$
\frac{d i_{o}}{d t}=\frac{d i_{1}}{d t}+\frac{d i_{2}}{d t}
$$

Therefore

$$
80 e^{-5 t}=-2 \frac{d i_{2}}{d t}
$$

Because $i_{2}(0)$ is zero we have

$$
\begin{aligned}
i_{2} & =\int_{0}^{t}-40 e^{-5 x} d x \\
& =-8+8 e^{-5 t} \mathrm{~A}, \quad t \geq 0
\end{aligned}
$$

Using Kirchhoff's current law we get

$$
i_{1}=24-24 e^{-5 t} \mathrm{~A}, \quad t \geq 0
$$

b) First we observe that $i_{o}(0), i_{1}(0)$, and $i_{2}(0)$ are all zero, which is consistent with the statement that
no energy is stored in the circuit at the instant the switch is closed.

Next we observe $v_{o}\left(0^{+}\right)=120 \mathrm{~V}$, which is consistent with the fact that $i_{o}(0)=0$.

Now we observe the solutions for $i_{1}$ and $i_{2}$ are consistent with the solution for $v_{o}$ by observing

$$
\begin{aligned}
v_{o} & =3 \frac{d i_{1}}{d t}+6 \frac{d i_{2}}{d t} \\
& =360 e^{-5 t}-240 e^{-5 t} \\
& =120 e^{-5 t} \mathrm{~V}, \quad t \geq 0^{+}
\end{aligned}
$$

or

$$
\begin{aligned}
v_{o} & =6 \frac{d i_{1}}{d t}+15 \frac{d i_{2}}{d t} \\
& =720 e^{-5 t}-600 e^{-5 t} \\
& =120 e^{-5 t} \mathrm{~V}, \quad t \geq 0^{+}
\end{aligned}
$$

The final values of $i_{1}$ and $i_{2}$ can be checked using flux linkages. The flux linking the 3 H coil $\left(\lambda_{1}\right)$ must be equal to the flux linking the 15 H coil $\left(\lambda_{2}\right)$, because

$$
\begin{aligned}
v_{o} & =\frac{d \lambda_{1}}{d t} \\
& =\frac{d \lambda_{2}}{d t}
\end{aligned}
$$

Now

$$
\lambda_{1}=3 i_{1}+6 i_{2} \mathrm{~Wb} \text {-turns }
$$

and

$$
\lambda_{2}=6 i_{1}+15 i_{2} \text { Wb-turns. }
$$

Regardless of which expression we use, we obtain

$$
\lambda_{1}=\lambda_{2}=24-24 e^{-5 t} \mathrm{~Wb} \text {-turns. }
$$

Note the solution for $\lambda_{1}$ or $\lambda_{2}$ is consistent with the solution for $v_{o}$.

The final value of the flux linking either coil 1 or coil 2 is 24 Wb -turns, that is,

$$
\lambda_{1}(\infty)=\lambda_{2}(\infty)=24 \text { Wb-turns. }
$$

The final value of $i_{1}$ is

$$
i_{1}(\infty)=24 \mathrm{~A}
$$

and the final value of $i_{2}$ is

$$
i_{2}(\infty)=-8 \mathrm{~A}
$$

The consistency between these final values for $i_{1}$ and $i_{2}$ and the final value of the flux linkage can be seen from the expressions:

$$
\begin{aligned}
\lambda_{1}(\infty) & =3 i_{1}(\infty)+6 i_{2}(\infty) \\
& =3(24)+6(-8)=24 \text { Wb-turns } \\
\lambda_{2}(\infty) & =6 i_{1}(\infty)+15 i_{2}(\infty) \\
& =6(24)+15(-8)=24 \mathrm{~Wb}-\text { turns. }
\end{aligned}
$$

It is worth noting that the final values of $i_{1}$ and $i_{2}$ can only be checked via flux linkage because at $t=\infty$ the two coils are ideal short circuits. The division of current between ideal short circuits cannot be found from Ohm's law.

NOTE: Assess your understanding of this material by using the general solution method to solve Chapter Problems 7.68 and 7.71.

## 7.5 Sequential Switching

Whenever switching occurs more than once in a circuit, we have sequential switching. For example, a single, two-position switch may be switched back and forth, or multiple switches may be opened or closed in sequence. The time reference for all switchings cannot be $t=0$. We determine the voltages and currents generated by a switching sequence by using the techniques described previously in this chapter. We derive the expressions for $v(t)$ and $i(t)$ for a given position of the switch or switches and then use these solutions to determine the initial conditions for the next position of the switch or switches.

With sequential switching problems, a premium is placed on obtaining the initial value $x\left(t_{0}\right)$. Recall that anything but inductive currents and capacitive voltages can change instantaneously at the time of switching. Thus solving first for inductive currents and capacitive voltages is even more pertinent in sequential switching problems. Drawing the circuit that pertains to each time interval in such a problem is often helpful in the solution process.

Examples 7.11 and 7.12 illustrate the analysis techniques for circuits with sequential switching. The first is a natural response problem with two switching times, and the second is a step response problem.

#### Example 7.11 Analyzing an RL Circuit that has Sequential Switching

The two switches in the circuit shown in Fig. 7.31 have been closed for a long time. At $t=0$, switch 1 is opened. Then, 35 ms later, switch 2 is opened.
a) Find $i_{L}(t)$ for $0 \leq t \leq 35 \mathrm{~ms}$.
b) Find $i_{L}$ for $t \geq 35 \mathrm{~ms}$.
c) What percentage of the initial energy stored in the 150 mH inductor is dissipated in the $18 \Omega$ resistor?
d) Repeat (c) for the $3 \Omega$ resistor.
e) Repeat (c) for the $6 \Omega$ resistor.
image_name:Figure 7.31
description:
[
'name': 'Vi', 'type': 'VoltageSource', 'value': '60 V', 'ports': {'Np': 'Vi', 'Nn': 'GND'
'name': '4 Ω', 'type': 'Resistor', 'value': '4 Ω', 'ports': {'N1': 'Vi', 'N2': 'X1'
'name': '12 Ω', 'type': 'Resistor', 'value': '12 Ω', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'X1', 'N2': 'X2'
'name': '3 Ω', 'type': 'Resistor', 'value': '3 Ω', 'ports': {'N1': 'X2', 'N2': 'VL'
'name': '6 Ω', 'type': 'Resistor', 'value': '6 Ω', 'ports': {'N1': 'X2', 'N2': 'GND'
'name': '150 mH', 'type': 'Inductor', 'value': '150 mH', 'ports': {'N1': 'VL', 'N2': 'GND'
'name': 'SW2', 'type': 'Switch', 'ports': {'N1': 'VL', 'N2': 'Vo'
'name': '18 Ω', 'type': 'Resistor', 'value': '18 Ω', 'ports': {'N1': 'Vo', 'N2': 'GND'
]
extrainfo:The circuit is an RL circuit with sequential switching involving two switches (SW1 and SW2). Initially, both switches are closed. At t=0, SW1 is opened, and 35 ms later, SW2 is opened. The circuit contains a 60 V voltage source, a 150 mH inductor, and resistors of various values (4 Ω, 12 Ω, 3 Ω, 6 Ω, and 18 Ω). The behavior of the inductor current iL(t) and energy dissipation in the resistors are analyzed over time.


Figure $7.31 \Delta$ The circuit for Example 7.11.

#### Solution

a) For $t<0$ both switches are closed, causing the 150 mH inductor to short-circuit the $18 \Omega$ resistor. The equivalent circuit is shown in Fig. 7.32. We determine the initial current in the inductor by solving for $i_{L}\left(0^{-}\right)$in the circuit shown in Fig. 7.32. After making several source transformations, we find $i_{L}\left(0^{-}\right)$to be 6 A . For $0 \leq t \leq 35 \mathrm{~ms}$, switch 1 is open (switch 2 is closed), which disconnects the 60 V voltage source and the $4 \Omega$ and $12 \Omega$ resistors from the circuit. The inductor is no longer behaving as a short circuit (because the dc source is no longer in the circuit), so the $18 \Omega$ resistor is no longer short-circuited. The equivalent circuit is shown in Fig. 7.33. Note that the equivalent resistance across the terminals of the inductor is the parallel combination of $9 \Omega$ and $18 \Omega$, or $6 \Omega$. The time constant of the circuit is $(150 / 6) \times 10^{-3}$, or 25 ms . Therefore the expression for $i_{L}$ is

$$
i_{L}=6 e^{-40 t} \mathrm{~A}, \quad 0 \leq t \leq 35 \mathrm{~ms}
$$

image_name:Figure 7.32
description:
[
'name': 'Vi', 'type': 'VoltageSource', 'value': '60V', 'ports': {'Np': 'Vi', 'Nn': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': '4Ω', 'ports': {'N1': 'Vi', 'N2': 'X1'
'name': 'R2', 'type': 'Resistor', 'value': '12Ω', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': 'R3', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': 'R4', 'type': 'Resistor', 'value': '3Ω', 'ports': {'N1': 'X1', 'N2': 'GND'
]
extrainfo:The circuit is a simple resistive network with a voltage source of 60V. The resistors R2, R3, and R4 are connected in parallel with the node X1, and the total resistance affects the inductor current i_L(0^-).


Figure 7.32 - The circuit shown in Fig. 7.31, for $t<0$.
image_name:Figure 7.33
description:
[
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'X1', 'N2': 'X2'
'name': '3Ω', 'type': 'Resistor', 'value': '3Ω', 'ports': {'N1': 'X2', 'N2': 'VL'
'name': '6Ω', 'type': 'Resistor', 'value': '6Ω', 'ports': {'N1': 'X2', 'N2': 'GND'
'name': '150 mH', 'type': 'Inductor', 'value': '150 mH', 'ports': {'N1': 'VL', 'N2': 'GND'
'name': 'SW2', 'type': 'Switch', 'ports': {'N1': 'VL', 'N2': 'X2'
'name': '18Ω', 'type': 'Resistor', 'value': '18Ω', 'ports': {'N1': 'X2', 'N2': 'GND'
]
extrainfo:The circuit is a resistive network with an inductor and two switches. Initially, the inductor current i_L(0^+) is 6A. The resistors and inductor form a loop with the switches controlling the current flow. The circuit operates within 0 ≤ t ≤ 35 ms.

b) When $t=35 \mathrm{~ms}$, the value of the inductor current is

$$
i_{L}=6 e^{-1.4}=1.48 \mathrm{~A}
$$

Thus, when switch 2 is opened, the circuit reduces to the one shown in Fig. 7.34, and the time constant changes to $(150 / 9) \times 10^{-3}$, or 16.67 ms . The expression for $i_{L}$ becomes

$$
i_{L}=1.48 e^{-60(t-0.035)} \mathrm{A}, \quad t \geq 35 \mathrm{~ms}
$$

Note that the exponential function is shifted in time by 35 ms .
image_name:Figure 7.34
description:
[
'name': 'Resistor1', 'type': 'Resistor', 'value': '6 Ω', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': 'Resistor2', 'type': 'Resistor', 'value': '3 Ω', 'ports': {'N1': 'X1', 'N2': 'VL'
'name': 'Inductor1', 'type': 'Inductor', 'value': '150 mH', 'ports': {'N1': 'VL', 'N2': 'GND'
]
extrainfo:The circuit consists of two resistors and one inductor forming an RL circuit. The inductor current iL(0.035) is approximately 1.48 A, and the voltage across the inductor is denoted as vL.


Figure $7.34 \boldsymbol{\Delta}$ The circuit shown in Fig. 7.31, for $t \geq 35 \mathrm{~ms}$.
c) The $18 \Omega$ resistor is in the circuit only during the first 35 ms of the switching sequence. During this interval, the voltage across the resistor is

$$
\begin{aligned}
v_{L} & =0.15 \frac{d}{d t}\left(6 e^{-40 t}\right) \\
& =-36 e^{-40 t} \mathrm{~V}, \quad 0<t<35 \mathrm{~ms}
\end{aligned}
$$

The power dissipated in the $18 \Omega$ resistor is

$$
p=\frac{v_{L}^{2}}{18}=72 e^{-80 t} \mathrm{~W}, \quad 0<t<35 \mathrm{~ms}
$$

Hence the energy dissipated is

$$
\begin{aligned}
w & =\int_{0}^{0.035} 72 e^{-80 t} d t \\
& =\left.\frac{72}{-80} e^{-80 t}\right|_{0} ^{0.035} \\
& =0.9\left(1-e^{-2.8}\right) \\
& =845.27 \mathrm{~mJ}
\end{aligned}
$$

The initial energy stored in the 150 mH inductor is

$$
w_{i}=\frac{1}{2}(0.15)(36)=2.7 \mathrm{~J}=2700 \mathrm{~mJ}
$$

Therefore $(845.27 / 2700) \times 100$, or $31.31 \%$ of the initial energy stored in the 150 mH inductor is dissipated in the $18 \Omega$ resistor.
d) For $0<t<35 \mathrm{~ms}$, the voltage across the $3 \Omega$ resistor is

$$
\begin{aligned}
v_{3 \Omega} & =\left(\frac{v_{L}}{9}\right)(3) \\
& =\frac{1}{3} v_{L} \\
& =-12 e^{-40 t} \mathrm{~V}
\end{aligned}
$$

Therefore the energy dissipated in the $3 \Omega$ resistor in the first 35 ms is

$$
\begin{aligned}
w_{3 \Omega} & =\int_{0}^{0.035} \frac{144 e^{-80 t}}{3} d t \\
& =0.6\left(1-e^{-2.8}\right) \\
& =563.51 \mathrm{~mJ}
\end{aligned}
$$

For $t>35 \mathrm{~ms}$, the current in the $3 \Omega$ resistor is

$$
i_{3 \Omega}=i_{L}=\left(6 e^{-1.4}\right) e^{-60(t-0.035)} \mathrm{A}
$$

Hence the energy dissipated in the $3 \Omega$ resistor for $t>35 \mathrm{~ms}$ is

$$
\begin{aligned}
w_{3 \Omega} & =\int_{0.035}^{\infty} i_{3 \Omega}^{2} \times 3 d t \\
& =\int_{0.035}^{\infty} 3(36) e^{-2.8} e^{-120(t-0.035)} d t \\
& =108 e^{-2.8} \times\left.\frac{e^{-120(t-0.035)}}{-120}\right|_{0.035} ^{\infty} \\
& =\frac{108}{120} e^{-2.8}=54.73 \mathrm{~mJ}
\end{aligned}
$$

The total energy dissipated in the $3 \Omega$ resistor is

$$
\begin{aligned}
w_{3 \Omega}(\text { total }) & =563.51+54.73 \\
& =618.24 \mathrm{~mJ}
\end{aligned}
$$

The percentage of the initial energy stored is

$$
\frac{618.24}{2700} \times 100=22.90 \%
$$

e) Because the $6 \Omega$ resistor is in series with the $3 \Omega$ resistor, the energy dissipated and the percentage of the initial energy stored will be twice that of the $3 \Omega$ resistor:

$$
w_{6 \Omega}(\text { total })=1236.48 \mathrm{~mJ}
$$

and the percentage of the initial energy stored is $45.80 \%$. We check these calculations by observing that

$$
1236.48+618.24+845.27=2699.99 \mathrm{~mJ}
$$

and

$$
31.31+22.90+45.80=100.01 \%
$$

The small discrepancies in the summations are the result of roundoff errors.

#### Example 7.12 Analyzing an RC Circuit that has Sequential Switching

The uncharged capacitor in the circuit shown in Fig. 7.35 is initially switched to terminal a of the three-position switch. At $t=0$, the switch is moved to position b, where it remains for 15 ms . After the 15 ms delay, the switch is moved to position c , where it remains indefinitely.
a) Derive the numerical expression for the voltage across the capacitor.
b) Plot the capacitor voltage versus time.
c) When will the voltage on the capacitor equal 200 V ?

#### Solution

a) At the instant the switch is moved to position b, the initial voltage on the capacitor is zero. If the switch were to remain in position b, the capacitor would eventually charge to 400 V . The time constant of the circuit when the switch is in position $b$ is 10 ms . Therefore we can use Eq. 7.59 with $t_{0}=0$ to write the expression for the capacitor voltage:

$$
\begin{aligned}
v & =400+(0-400) e^{-100 t} \\
& =\left(400-400 e^{-100 t}\right) \mathrm{V}, \quad 0 \leq t \leq 15 \mathrm{~ms}
\end{aligned}
$$

Note that, because the switch remains in position b for only 15 ms , this expression is valid only for the time interval from 0 to 15 ms . After the switch has been in this position for 15 ms , the voltage on the capacitor will be

$$
v(15 \mathrm{~ms})=400-400 e^{-1.5}=310.75 \mathrm{~V}
$$

Therefore, when the switch is moved to position c , the initial voltage on the capacitor is 310.75 V . With the switch in position c , the final value of the capacitor voltage is zero, and the time constant is 5 ms . Again, we use Eq. 7.59 to write the expression for the capacitor voltage:

$$
\begin{aligned}
v & =0+(310.75-0) e^{-200(t-0.015)} \\
& =310.75 e^{-200(t-0.015)} \mathrm{V}, \quad 15 \mathrm{~ms} \leq t
\end{aligned}
$$

image_name:Figure 7.35
description:
[
'name': 'Vi', 'type': 'VoltageSource', 'value': '400V', 'ports': {'Np': 'Vi', 'Nn': 'GND'
'name': 'Resistor1', 'type': 'Resistor', 'value': '100kΩ', 'ports': {'N1': 'Vi', 'N2': 'b'
'name': 'Resistor2', 'type': 'Resistor', 'value': '50kΩ', 'ports': {'N1': 'c', 'N2': 'GND'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'a', 'N2': 'b','N3':'c'
'name': 'Capacitor1', 'type': 'Capacitor', 'value': '0.1μF', 'ports': {'Np': 'V(t)', 'Nn': 'GND'
]
extrainfo:The circuit involves a voltage source Vi providing 400V, connected through a 100kΩ resistor to a switch SW1. The switch can connect node b to either node a or node c. When connected to node a, the circuit charges a 0.1μF capacitor through node V(t). When connected to node c, the capacitor discharges through a 50kΩ resistor to ground. The capacitor voltage expression is given for t ≥ 15 ms as 310.75e^{-200(t-0.015)} V.


Figure 7.35 A The circuit for Example 7.12.

In writing the expression for $v$, we recognized that $t_{0}=15 \mathrm{~ms}$ and that this expression is valid only for $t \geq 15 \mathrm{~ms}$.
b) Figure 7.36 shows the plot of $v$ versus $t$.
c) The plot in Fig. 7.36 reveals that the capacitor voltage will equal 200 V at two different times: once in the interval between 0 and 15 ms and once after 15 ms . We find the first time by solving the expression

$$
200=400-400 e^{-100 t_{1}}
$$

which yields $t_{1}=6.93 \mathrm{~ms}$. We find the second time by solving the expression

$$
200=310.75 e^{-200\left(t_{2}-0.015\right)}
$$

In this case, $t_{2}=17.20 \mathrm{~ms}$.
image_name:Figure 7.36
description:The graph in Figure 7.36 is a time-domain waveform showing the voltage across a capacitor, denoted as \( v \), plotted against time \( t \). The horizontal axis represents time in milliseconds (ms), ranging from 0 to 25 ms. The vertical axis represents voltage in volts (V), ranging from 0 to 400 V. The graph is linear in scale for both axes.

The waveform consists of two distinct exponential segments:

1. **First Segment (0 to 15 ms):**
- The voltage follows the function \( v = 400 - 400e^{-100t} \).
- This segment represents an exponential rise starting from 0 V at \( t = 0 \) and asymptotically approaching 400 V.
- The voltage reaches exactly 200 V at approximately \( t = 6.93 \) ms.
- The waveform peaks at 400 V at \( t = 15 \) ms.

2. **Second Segment (15 ms to 25 ms):**
- The voltage follows the function \( v = 310.75e^{-200(t - 0.015)} \).
- This segment represents an exponential decay starting from 400 V at \( t = 15 \) ms.
- The voltage decreases and crosses 200 V again at approximately \( t = 17.20 \) ms.

The graph indicates a sharp transition at \( t = 15 \) ms, where the behavior of the voltage changes from rising to falling. This is marked by a dashed vertical line at 15 ms, emphasizing the point of maximum voltage and the switch in the function governing the waveform. The annotations on the graph provide the equations for both segments, aiding in understanding the voltage behavior over time.


Figure 7.36 $\triangle$ The capacitor voltage for Example 7.12.

ASSESSMENT PROBLEMS

Objective 3-Know how to analyze circuits with sequential switching

7.7 In the circuit shown, switch 1 has been closed and switch 2 has been open for a long time. At $t=0$, switch 1 is opened. Then 10 ms later, switch 2 is closed. Find
a) $v_{c}(t)$ for $0 \leq t \leq 0.01 \mathrm{~s}$,
b) $v_{c}(t)$ for $t \geq 0.01 \mathrm{~s}$,
c) the total energy dissipated in the $25 \mathrm{k} \Omega$ resistor, and
d) the total energy dissipated in the $100 \mathrm{k} \Omega$ resistor.
image_name:
description:
[
'name': 'Current Source', 'type': 'CurrentSource', 'value': '10mA', 'ports': {'Np': 'GND', 'Nn': 'Vi'
'name': '40kΩ Resistor', 'type': 'Resistor', 'value': '40kΩ', 'ports': {'N1': 'Vi', 'N2': 'GND'
'name': '60kΩ Resistor', 'type': 'Resistor', 'value': '60kΩ', 'ports': {'N1': "Vi'", 'N2': 'Vc'
'name': '25kΩ Resistor', 'type': 'Resistor', 'value': '25kΩ', 'ports': {'N1': 'Vc', 'N2': 'GND'
'name': '1μF Capacitor', 'type': 'Capacitor', 'value': '1μF', 'ports': {'Np': 'Vc', 'Nn': 'GND'
'name': '100kΩ Resistor', 'type': 'Resistor', 'value': '100kΩ', 'ports': {'N1': 'GND', 'N2': 'X'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'Vi', 'N2': "Vi'"
'name': 'SW2', 'type': 'Switch', 'ports': {'N1': 'Vc', 'N2': 'X'
]
extrainfo:The circuit is a sequential switching circuit involving two switches, SW1 and SW2. Initially, SW1 is closed and SW2 is open. At t=0, SW1 opens, and 10 ms later, SW2 closes. The circuit includes resistors, a capacitor, and a current source. The voltage across the capacitor, Vc(t), is analyzed for different time intervals.


Answer: (a) $80 e^{-40 t} \mathrm{~V}$;
(b) $53.63 e^{-50(t-0.01)} \mathrm{V}$;
(c) 2.91 mJ ;
(d) 0.29 mJ .

NOTE: Also try Chapter Problems 7.72 and 7.80.
7.8 Switch a in the circuit shown has been open for a long time, and switch b has been closed for a long time. Switch a is closed at $t=0$ and, after remaining closed for 1 s , is opened again. Switch b is opened simultaneously, and both switches remain open indefinitely. Determine the expression for the inductor current $i$ that is valid when (a) $0 \leq t \leq 1 \mathrm{~s}$ and (b) $t \geq 1 \mathrm{~s}$.
image_name:7.8
description:
[
'name': 'Vi', 'type': 'VoltageSource', 'value': '10 V', 'ports': {'Np': 'Vi', 'Nn': 'GND'
'name': '2 Ω', 'type': 'Resistor', 'value': '2 Ω', 'ports': {'N1': 'Vi', 'N2': 'X1'
'name': '3 Ω', 'type': 'Resistor', 'value': '3 Ω', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': '0.8 Ω', 'type': 'Resistor', 'value': '0.8 Ω', 'ports': {'N1': 'X1', 'N2': 'X2'
'name': '2 H', 'type': 'Inductor', 'value': '2 H', 'ports': {'N1': 'X3', 'N2': 'GND'
'name': '9 Ω', 'type': 'Resistor', 'value': '9 Ω', 'ports': {'N1': 'X3', 'N2': 'X4'
'name': '6 Ω', 'type': 'Resistor', 'value': '6 Ω', 'ports': {'N1': 'X4', 'N2': 'GND'
'name': '3 Ω', 'type': 'Resistor', 'value': '3 Ω', 'ports': {'N1': 'X3', 'N2': 'GND'
'name': 'SW2', 'type': 'Switch', 'ports': {'N1': 'X2', 'N2': 'X3'
'name': 'SW3', 'type': 'Switch', 'ports': {'N1': 'X3', 'N2': 'X4'
'name': '8 A', 'type': 'CurrentSource', 'value': '8 A', 'ports': {'Np': 'X3', 'Nn': 'X4'
]
extrainfo:The circuit contains a voltage source, resistors, an inductor, switches, and a current source. Switch a (SW2) is closed at t=0 and opened at t=1s. Switch b (SW3) is opened at t=1s. The inductor current expression is given for two intervals: (a) 0 ≤ t ≤ 1 s, and (b) t ≥ 1 s.


Answer: (a) $\left(3-3 e^{-0.5 t}\right) \mathrm{A}, 0 \leq t \leq 1 \mathrm{~s}$;
(b) $\left(-4.8+5.98 e^{-1.25(t-1)}\right) \mathrm{A}, t \geq 1 \mathrm{~s}$.

## 7.6 Unbounded Response

A circuit response may grow, rather than decay, exponentially with time. This type of response, called an unbounded response, is possible if the circuit contains dependent sources. In that case, the Thévenin equivalent resistance with respect to the terminals of either an inductor or a capacitor may be negative. This negative resistance generates a negative time constant, and the resulting currents and voltages increase without limit. In an actual circuit, the response eventually reaches a limiting value when a component breaks down or goes into a saturation state, prohibiting further increases in voltage or current.

When we consider unbounded responses, the concept of a final value is confusing. Hence, rather than using the step response solution given in Eq. 7.59 , we derive the differential equation that describes the circuit containing the negative resistance and then solve it using the separation of variables technique. Example 7.13 presents an exponentially growing response in terms of the voltage across a capacitor.

#### Example 7.13 Finding the Unbounded Response in an RC Circuit

a) When the switch is closed in the circuit shown in Fig. 7.37, the voltage on the capacitor is 10 V . Find the expression for $v_{o}$ for $t \geq 0$.
b) Assume that the capacitor short-circuits when its terminal voltage reaches 150 V . How many milliseconds elapse before the capacitor shortcircuits?
image_name:Figure 7.37
description:
[
'name': '5μF', 'type': 'Capacitor', 'value': '5μF', 'ports': {'Np': 'Vo', 'Nn': 'GND'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'Vo', 'N2': 'X1'
'name': '10kΩ', 'type': 'Resistor', 'value': '10kΩ', 'ports': {'N1': 'GND', 'N2': 'X1'
'name': '7iΔ', 'type': 'CurrentControlledCurrentSource', 'ports': {'Np': 'GND', 'Nn': 'X1'
'name': '20kΩ', 'type': 'Resistor', 'value': '20kΩ', 'ports': {'N1': 'X1', 'N2': 'GND'
]
extrainfo:The circuit is an RC circuit with a voltage source of 10V, a capacitor of 5μF, and resistors of 10kΩ and 20kΩ. A switch (SW1) is present, and a current-controlled current source (7iΔ) is connected in parallel with the 20kΩ resistor. The voltage across the capacitor is initially 10V, and the circuit analyzes the unbounded response when the switch is closed at t = 0.


Figure 7.37 The circuit for Example 7.13.

#### Solution

a) To find the Thévenin equivalent resistance with respect to the capacitor terminals, we use the testsource method described in Chapter 4. Figure 7.38 shows the resulting circuit, where $v_{T}$ is the test voltage and $i_{T}$ is the test current. For $v_{T}$ expressed in volts, we obtain

$$
i_{T}=\frac{v_{T}}{10}-7\left(\frac{v_{T}}{20}\right)+\frac{v_{T}}{20} \mathrm{~mA}
$$

Solving for the ratio $v_{T} / i_{T}$ yields the Thévenin resistance:

$$
R_{\mathrm{Th}}=\frac{v_{T}}{i_{T}}=-5 \mathrm{k} \Omega
$$

With this Thévenin resistance, we can simplify the circuit shown in Fig. 7.37 to the one shown in Fig. 7.39.
image_name:Figure 7.38
description:
[
'name': '10kΩ', 'type': 'Resistor', 'value': '10kΩ', 'ports': {'N1': 'Vt', 'N2': 'GND'
'name': '20kΩ', 'type': 'Resistor', 'value': '20kΩ', 'ports': {'N1': 'Vt', 'N2': 'GND'
'name': '7iΔ', 'type': 'CurrentControlledCurrentSource', 'value': '7iΔ', 'ports': {'Np': 'GND', 'Nn': 'Vt'
]
extrainfo:The circuit in Figure 7.38 uses a test-source method to find the Thévenin resistance. The circuit in Figure 7.39 is a simplified version with a differential equation describing the voltage across the capacitor. The Thévenin resistance calculated is -5 kΩ.
image_name:Figure 7.39
description:
[
'name': 'C1', 'type': 'Capacitor', 'value': '5μF', 'ports': {'Np': 'V_o', 'Nn': 'GND'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'V_o', 'N2': 'X1'
'name': 'R3', 'type': 'Resistor', 'value': '-5kΩ', 'ports': {'N1': 'X1', 'N2': 'GND'
]
extrainfo:The circuit in Figure 7.39 is a simplified representation of the original circuit in Figure 7.37, incorporating a Thévenin equivalent resistance of -5kΩ. It consists of a voltage source, a capacitor, a switch, and a resistor. The differential equation for this circuit is \( \frac{d v_{o}}{d t} - 40 v_{o} = 0 \), and the solution using separation of variables is \( v_{o}(t) = 10 e^{40 t} \) V for \( t \geq 0 \).


Figure $7.39 \triangle$ A simplification of the circuit shown in Fig. 7.37.

For $t \geq 0$, the differential equation describing the circuit shown in Fig. 7.39 is

$$
\left(5 \times 10^{-6}\right) \frac{d v_{o}}{d t}-\frac{v_{o}}{5} \times 10^{-3}=0
$$

Dividing by the coefficient of the first derivative yields

$$
\frac{d v_{o}}{d t}-40 v_{o}=0
$$

We now use the separation of variables technique to find $v_{o}(t)$ :

$$
v_{o}(t)=10 e^{40 t} \mathrm{~V}, \quad t \geq 0
$$

b) $v_{o}=150 \mathrm{~V}$ when $e^{40 t}=15$. Therefore, $40 t=\ln 15$, and $t=67.70 \mathrm{~ms}$.

NOTE: Assess your understanding of this material by trying Chapter Problems 7.86 and 7.88.

The fact that interconnected circuit elements may lead to everincreasing currents and voltages is important to engineers. If such interconnections are unintended, the resulting circuit may experience unexpected, and potentially dangerous, component failures.

## 7.7 The Integrating Amplifier

Recall from the introduction to Chapter 5 that one reason for our interest in the operational amplifier is its use as an integrating amplifier. We are now ready to analyze an integrating-amplifier circuit, which is shown in Fig. 7.40. The purpose of such a circuit is to generate an output voltage proportional to the integral of the input voltage. In Fig. 7.40, we added the branch currents $i_{f}$ and $i_{s}$, along with the node voltages $v_{n}$ and $v_{p}$, to aid our analysis.
image_name:Figure 7.40 An integrating amplifier
description:
[
'name': 'Vs', 'type': 'VoltageSource', 'value': 'vs', 'ports': {'Np': 'Vs', 'Nn': 'GND'
'name': 'Rs', 'type': 'Resistor', 'value': 'Rs', 'ports': {'N1': 'Vs', 'N2': 'Vn'
'name': 'Cf', 'type': 'Capacitor', 'value': 'Cf', 'ports': {'Np': 'Vo', 'Nn': 'Vn'
'name': 'Ao', 'type': 'OpAmp', 'value': 'Ao', 'ports': {'InP': 'Vp', 'InN': 'Vn', 'OutP': 'Vo', 'Vdd':'VCC', '-Vdd':'-VCC'
]
extrainfo:The circuit is an integrating amplifier. The input voltage Vs is applied through resistor Rs to the inverting input of the operational amplifier Ao, with feedback provided by capacitor Cf. The non-inverting input is grounded. The output voltage Vo is proportional to the integral of the input voltage.


Figure $7.40 \triangle$ An integrating amplifier.
image_name:Figure 7.41
description:The graph in Figure 7.41 is a time-domain waveform representing an input voltage signal, denoted as \(v_s\). The horizontal axis is labeled \(t\), representing time, while the vertical axis is labeled \(v_s\), representing voltage. The voltage scale is linear, with key voltage levels marked at \(V_m\) and \(-V_m\).

The waveform is a square wave alternating between two levels, \(V_m\) and \(-V_m\). Starting at time \(t = 0\), the voltage \(v_s\) is at \(V_m\) and remains constant until time \(t_1\). At \(t_1\), the voltage abruptly drops to \(-V_m\) and stays constant at this level until time \(2t_1\). At \(2t_1\), the voltage returns to \(V_m\), completing one full cycle of the square wave.

The waveform exhibits a periodic behavior with a period of \(2t_1\). The transitions between voltage levels are instantaneous, characteristic of an ideal square wave. No intermediate values or slopes are present, indicating a perfect step change at each transition point. This input signal is used in the context of an integrating amplifier circuit, where the output will be proportional to the integral of this input waveform.


Figure 7.41 $\triangle$ An input voltage signal.
image_name:Figure 7.42
description:The graph in Figure 7.42 represents the output voltage \( v_o(t) \) of an integrating amplifier as a function of time \( t \). The graph is a time-domain waveform characterized by a linear descent and ascent, representing the integration of a square wave input.

1. **Type of Graph and Function:**
- The graph is a time-domain waveform showing the output of an integrating amplifier.

2. **Axes Labels and Units:**
- The horizontal axis is labeled \( t \) and represents time.
- The vertical axis is labeled \( v_o(t) \) and represents the output voltage.

3. **Overall Behavior and Trends:**
- The waveform starts at zero and linearly decreases to a minimum value at time \( t_1 \).
- After reaching the minimum, the waveform linearly increases back to zero at time \( 2t_1 \).
- This behavior is periodic, corresponding to the integration of a square wave input over one cycle.

4. **Key Features and Technical Details:**
- The minimum value of the output voltage is \( -\frac{V_m t_1}{R_s C_f} \), indicating the maximum negative integration of the input square wave.
- The waveform is symmetric about the time \( t_1 \), showing equal linear slopes during the descent and ascent.

5. **Annotations and Specific Data Points:**
- The point \( t_1 \) is marked on the time axis, indicating where the output voltage reaches its minimum.
- The point \( 2t_1 \) marks the end of one period of the waveform, where the output returns to zero.

This graph effectively illustrates the behavior of an integrating amplifier output when subjected to an ideal square wave input, with the output voltage being proportional to the integral of the input signal over time.


Figure $7.42 \triangle$ The output voltage of an integrating amplifier.

We assume that the operational amplifier is ideal. Thus we take advantage of the constraints

$$
\begin{align*}
i_{f}+i_{s} & =0  \tag{7.61}\\
v_{n} & =v_{p} \tag{7.62}
\end{align*}
$$

Because $v_{p}=0$,

$$
\begin{align*}
i_{s} & =\frac{v_{s}}{R_{s}}  \tag{7.63}\\
i_{f} & =C_{f} \frac{d v_{o}}{d t} \tag{7.64}
\end{align*}
$$

Hence, from Eqs. 7.61, 7.63, and 7.64,

$$
\begin{equation*}
\frac{d v_{o}}{d t}=-\frac{1}{R_{s} C_{f}} v_{s} \tag{7.65}
\end{equation*}
$$

Multiplying both sides of Eq. 7.65 by a differential time $d t$ and then integrating from $t_{0}$ to $t$ generates the equation

$$
\begin{equation*}
v_{o}(t)=-\frac{1}{R_{s} C_{f}} \int_{t_{0}}^{t} v_{s} d y+v_{o}\left(t_{0}\right) \tag{7.66}
\end{equation*}
$$

In Eq. 7.66, $t_{0}$ represents the instant in time when we begin the integration. Thus $v_{o}\left(t_{0}\right)$ is the value of the output voltage at that time. Also, because $v_{n}=v_{p}=0, v_{o}\left(t_{0}\right)$ is identical to the initial voltage on the feedback capacitor $C_{f}$.

Equation 7.66 states that the output voltage of an integrating amplifier equals the initial value of the voltage on the capacitor plus an inverted (minus sign), scaled $\left(1 / R_{s} C_{f}\right)$ replica of the integral of the input voltage. If no energy is stored in the capacitor when integration commences, Eq. 7.66 reduces to

$$
\begin{equation*}
v_{o}(t)=-\frac{1}{R_{s} C_{f}} \int_{t_{0}}^{t} v_{s} d y \tag{7.67}
\end{equation*}
$$

If $v_{s}$ is a step change in a dc voltage level, the output voltage will vary linearly with time. For example, assume that the input voltage is the rectangular voltage pulse shown in Fig. 7.41. Assume also that the initial value of $v_{o}(t)$ is zero at the instant $v_{s}$ steps from 0 to $V_{m}$. A direct application of Eq. 7.66 yields

$$
\begin{equation*}
v_{o}=-\frac{1}{R_{s} C_{f}} V_{m} t+0, \quad 0 \leq t \leq t_{1} \tag{7.68}
\end{equation*}
$$

When $t$ lies between $t_{1}$ and $2 t_{1}$,

$$
\begin{align*}
v_{o} & =-\frac{1}{R_{s} C_{f}} \int_{t_{1}}^{t}\left(-V_{m}\right) d y-\frac{1}{R_{s} C_{f}} V_{m} t_{1} \\
& =\frac{V_{m}}{R_{s} C_{f}} t-\frac{2 V_{m}}{R_{s} C_{f}} t_{1}, \quad t_{1} \leq t \leq 2 t_{1} \tag{7.69}
\end{align*}
$$

Figure 7.42 shows a sketch of $v_{o}(t)$ versus $t$. Clearly, the output voltage is an inverted, scaled replica of the integral of the input voltage.

The output voltage is proportional to the integral of the input voltage only if the op amp operates within its linear range, that is, if it doesn't saturate. Examples 7.14 and 7.15 further illustrate the analysis of the integrating amplifier.

#### Example 7.14 Analyzing an Integrating Amplifier

Assume that the numerical values for the signal voltage shown in Fig. 7.41 are $V_{m}=50 \mathrm{mV}$ and $t_{1}=1 \mathrm{~s}$. This signal voltage is applied to the integrating-amplifier circuit shown in Fig. 7.40. The circuit parameters of the amplifier are $R_{s}=100 \mathrm{k} \Omega$, $C_{f}=0.1 \mu \mathrm{~F}$, and $V_{C C}=6 \mathrm{~V}$. The initial voltage on the capacitor is zero.
a) Calculate $v_{o}(t)$.
b) Plot $v_{o}(t)$ versus $t$.

#### Solution

a) For $0 \leq t \leq 1 \mathrm{~s}$,

$$
\begin{aligned}
v_{o} & =\frac{-1}{\left(100 \times 10^{3}\right)\left(0.1 \times 10^{-6}\right)} 50 \times 10^{-3} t+0 \\
& =-5 t \mathrm{~V}, \quad 0 \leq t \leq 1 \mathrm{~s}
\end{aligned}
$$

For $1 \leq t \leq 2 \mathrm{~s}$,

$$
v_{o}=(5 t-10) \mathrm{V}
$$

b) Figure 7.43 shows a plot of $v_{o}(t)$ versus $t$.
image_name:Figure 7.43
description:The graph in Figure 7.43 is a time-domain waveform plot showing the output voltage \( v_o(t) \) in volts (V) against time \( t \) in seconds (s). The horizontal axis represents time, ranging from 0 to 2 seconds, while the vertical axis represents voltage, ranging from -5 V to 0 V.

Type of Graph and Function:
This is a linear piecewise function graph illustrating the behavior of the output voltage over time.

Axes Labels and Units:
- **Horizontal Axis (x-axis):** Time \( t \) in seconds (s).
- **Vertical Axis (y-axis):** Output Voltage \( v_o(t) \) in volts (V).

Overal Behavior and Trends:
- **For \( 0 \leq t \leq 1 \) s:** The graph shows a linear decrease in voltage from 0 V to -5 V. This indicates a negative slope, which matches the equation \( v_o(t) = -5t \) V.
- **For \( 1 \leq t \leq 2 \) s:** The graph shows a linear increase in voltage from -5 V back to 0 V. This indicates a positive slope, consistent with the equation \( v_o(t) = 5t - 10 \) V.

Key Features and Technical Details:
- **Zero Crossing:** The graph crosses the time axis at \( t = 0 \) and \( t = 2 \) seconds.
- **Minimum Point:** The minimum voltage of -5 V occurs at \( t = 1 \) second.

Annotations and Specific Data Points:
- The graph is marked with dashed lines at \( t = 1 \) second and at \( v_o(t) = -5 \) V, highlighting the minimum point of the waveform.

The graph effectively demonstrates the linear decrease and subsequent increase in output voltage over the specified time intervals, illustrating the behavior of the system described in the context.


Figure 7.43 A The output voltage for Example 7.14.

#### Example 7.15 Analyzing an Integrating Amplifier that has Sequential Switching

At the instant the switch makes contact with terminal a in the circuit shown in Fig. 7.44, the voltage on the $0.1 \mu \mathrm{~F}$ capacitor is 5 V . The switch remains at terminal a for 9 ms and then moves instantaneously to terminal b. How many milliseconds after making contact with terminal $b$ does the operational amplifier saturate?
image_name:Figure 7.44
description:
[
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'c', 'N2': 'a','N3':'b'
'name': '10V', 'type': 'VoltageSource', 'value': '10V', 'ports': {'Np': 'GND', 'Nn': 'a'
'name': '8V', 'type': 'VoltageSource', 'value': '8V', 'ports': {'Np': 'b', 'Nn': 'GND'
'name': '100kΩ', 'type': 'Resistor', 'value': '100kΩ', 'ports': {'N1': 'c', 'N2': 'InN(Ao)'
'name': '0.1μF', 'type': 'Capacitor', 'value': '0.1μF', 'ports': {'Np': 'InN(Ao)', 'Nn': 'Vo'
'name': 'Ao', 'type': 'OpAmp', 'ports': {'InP': 'GND', 'InN': 'InN(Ao)', 'OutP': 'Vo','Vdd':'6V', '-Vdd':'-6V'
]
extrainfo:The circuit is an integrating amplifier with sequential switching. The switch SW1 alternates between two voltage sources (10V and 8V) connected to a resistor and an op-amp, affecting the output voltage Vo. The capacitor initially has a voltage of 5V.


Figure $7.44 \boldsymbol{4}$ The circuit for Example 7.15.

#### Solution

The expression for the output voltage during the time the switch is at terminal a is

$$
\begin{aligned}
v_{o} & =-5-\frac{1}{10^{-2}} \int_{0}^{t}(-10) d y \\
& =(-5+1000 t) \mathrm{V}
\end{aligned}
$$

Thus, 9 ms after the switch makes contact with terminal a, the output voltage is $-5+9$, or 4 V .

The expression for the output voltage after the switch moves to terminal $b$ is

$$
\begin{aligned}
v_{o} & =4-\frac{1}{10^{-2}} \int_{9 \times 10^{-3}}^{t} 8 d y \\
& =4-800\left(t-9 \times 10^{-3}\right) \\
& =(11.2-800 t) \mathrm{V}
\end{aligned}
$$

During this time interval, the voltage is decreasing, and the operational amplifier eventually saturates at -6 V . Therefore we set the expression for $v_{o}$ equal to -6 V to obtain the saturation time $t_{s}$ :

$$
11.2-800 t_{s}=-6,
$$

or

$$
t_{s}=21.5 \mathrm{~ms}
$$

Thus the integrating amplifier saturates 21.5 ms after making contact with terminal b.

From the examples, we see that the integrating amplifier can perform the integration function very well, but only within specified limits that avoid saturating the op amp. The op amp saturates due to the accumulation of charge on the feedback capacitor. We can prevent it from saturating by placing a resistor in parallel with the feedback capacitor. We examine such a circuit in Chapter 8.

Note that we can convert the integrating amplifier to a differentiating amplifier by interchanging the input resistance $R_{s}$ and the feedback capacitor $C_{f}$. Then

$$
\begin{equation*}
v_{o}=-R_{s} C_{f} \frac{d v_{s}}{d t} \tag{7.70}
\end{equation*}
$$

We leave the derivation of Eq. 7.70 as an exercise for you. The differentiating amplifier is seldom used because in practice it is a source of unwanted or noisy signals.

Finally, we can design both integrating- and differentiating-amplifier circuits by using an inductor instead of a capacitor. However, fabricating capacitors for integrated-circuit devices is much easier, so inductors are rarely used in integrating amplifiers.

ASSESSMENT PROBLEMS

Objective 4-Be able to analyze op amp circuits containing resistors and a single capacitor

7.9 There is no energy stored in the capacitor at the time the switch in the circuit makes contact with terminal a. The switch remains at position a for 32 ms and then moves instantaneously to position b. How many milliseconds after making contact with terminal a does the op amp saturate?
image_name:7.9
description:
[
'name': 'Vi', 'type': 'VoltageSource', 'value': '10V', 'ports': {'Np': 'GND', 'Nn': 'Vi'
'name': 'R1', 'type': 'Resistor', 'value': '40kΩ', 'ports': {'N1': 'Vi', 'N2': 'a'
'name': 'R2', 'type': 'Resistor', 'value': '90kΩ', 'ports': {'N1': 'd', 'N2': 'b'
'name': 'VoltageSource1', 'type': 'VoltageSource', 'value': '5V', 'ports': {'Np': 'd', 'Nn': 'GND'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'c', 'N2': 'a','N3':'b'
'name': 'R3', 'type': 'Resistor', 'value': '160kΩ', 'ports': {'N1': 'c', 'N2': 'InN(Ao)'
'name': 'C1', 'type': 'Capacitor', 'value': '0.2μF', 'ports': {'Np': 'InN(Ao)', 'Nn': 'Vo'
'name': 'Ao', 'type': 'OpAmp', 'ports': {'InP': 'InN(Ao)', 'InN': 'GND', 'OutP': 'Vo', 'Vdd':'10V', '-Vdd':'-15V'
]
extrainfo:The circuit includes an operational amplifier configured with a feedback capacitor and resistors. The switch SW1 changes position after 32 ms, affecting the input to the op-amp.


Answer: 262 ms .
7.10 a) When the switch closes in the circuit shown, there is no energy stored in the capacitor. How long does it take to saturate the op amp?
b) Repeat (a) with an initial voltage on the capacitor of 1 V , positive at the upper terminal.
image_name:Fig
description:
[
'name': 'Vi', 'type': 'VoltageSource', 'value': '2V', 'ports': {'Np': 'GND', 'Nn': 'Vi'
'name': 'R1', 'type': 'Resistor', 'value': '10kΩ', 'ports': {'N1': 'InN(Ao)', 'N2': 'GND'
'name': 'R2', 'type': 'Resistor', 'value': '40kΩ', 'ports': {'N1': 'Vo', 'N2': 'InN(Ao)'
'name': 'R3', 'type': 'Resistor', 'value': '160kΩ', 'ports': {'N1': 'Vi', 'N2': 'X1'
'name': 'R4', 'type': 'Resistor', 'value': '6.8kΩ', 'ports': {'N1': 'Vo', 'N2': 'GND'
'name': 'C1', 'type': 'Capacitor', 'value': '0.01μF', 'ports': {'Np': 'InP(Ao)', 'Nn': 'GND'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'X1', 'N2': 'InP(Ao)'
'name': 'A0', 'type': 'OpAmp', 'ports': {'InP': 'InP(Ao)', 'InN': 'InN(Ao)', 'OutP': 'Vo', 'Vdd':'5V', '-Vdd':'-5V'
]
extrainfo:The circuit includes an operational amplifier configured with a feedback capacitor and resistors. The switch SW1 changes position after 32 ms, affecting the input to the op-amp.


Answer: (a) 1.11 ms ;
(b) 1.76 ms .

NOTE: Also try Chapter Problems 7.94 and 7.95.

Practical Perspective

Artificial Pacemaker

We are now ready to analyze a simple RC circuit, shown in Fig. 7.45, which can generate periodic electrical impulses. This RC circuit can be used in an artificial pacemaker to establish a normal heart rhythm. The box labeled "controller" behaves as an open circuit until the voltage drop across the capacitor reaches a pre-set limit. Once that limit is reached, the capacitor discharges its stored energy in the form of an electrical impulse to the heart and starts to recharge and the process repeats.

Before we develop the analytical expressions that describe the behavior of the circuit, let us develop a feel for how that circuit works. First, when the controller behaves as an open circuit, the dc voltage source will charge the capacitor via the resistor $R$, toward a value of $V_{s}$ volts. But once the capacitor voltage reaches $V_{\max }$, the controller behaves like a short circuit, enabling the capacitor to discharge. Once the capacitor discharge is complete, the controller once again acts as an open circuit and the capacitor starts to recharge. This cycle of charging and discharging the capacitor establishes the desired heart rhythm, as shown in Fig. 7.46.
image_name:Figure 7.45
description:
[
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': 'Vs', 'Nn': 'GND'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'Vs', 'N2': 'VC'
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'VC', 'Nn': 'GND'
'name': 'Controller', 'type': 'Other', 'ports': {'N1': 'VC', 'N2': 'GND'
]
extrainfo:The circuit is an artificial pacemaker, where the capacitor charges through the resistor and discharges via the controller to establish a heart rhythm.


Figure $7.45 \triangle$ An artificial pacemaker circuit.
image_name:Figure 7.46
description:The graph in Figure 7.46 is a time-domain waveform depicting the voltage across a capacitor, denoted as \( v_C(t) \), in an artificial pacemaker circuit. The x-axis represents time \( t \), while the y-axis represents the capacitor voltage \( v_C(t) \) in volts. The graph uses a linear scale for both axes.

The overall behavior of the graph shows a repetitive charging and discharging pattern of the capacitor. The voltage \( v_C(t) \) starts at zero and increases exponentially towards a maximum voltage \( V_{\text{max}} \). This charging phase occurs over a time period \( t_c \). Once the voltage reaches \( V_{\text{max}} \), it abruptly drops back to zero, indicating the rapid discharge of the capacitor through the controller in the circuit.

This cycle repeats, illustrating the periodic nature of the pacemaker's operation. The time to discharge the capacitor is negligible compared to the charging time, as indicated by the steep drop in voltage.

Key features include the exponential rise of the voltage during the charging phase and the sharp drop during the discharge phase. The graph marks \( V_{\text{max}} \) and \( t_c \) to denote the maximum voltage and the time it takes to charge the capacitor to this voltage, respectively. The annotation 'etc.' suggests that this pattern continues indefinitely, maintaining the established rhythm essential for the pacemaker's function.


Figure $7.46 \boldsymbol{\Delta}$ Capacitor voltage versus time for the circuit in Fig. 7.45.

In drawing Fig. 7.46 we have chosen $t=0$ at the instant the capacitor starts to charge. This figure also assumes that the circuit has reached the repetitive stage of its operation, and that the time to discharge the capacitor is negligible when compared to the recharge time. The design of this artificial pacemaker circuit requires an equation for $v_{C}(t)$ as a function of $V_{\text {max }}, R$, and $C$.

To begin the analysis, we assume that the circuit has been in operation for a long time. Let $t=0$ at the instant when the capacitor has completely discharged and the controller is acting as an open circuit. From the circuit we find

$$
\begin{aligned}
v_{C}(\infty) & =V_{s^{\prime}} \\
v_{C}(0) & =0 \\
\tau & =R C .
\end{aligned}
$$

Thus, while the capacitor is charging,

$$
v_{C}(t)=V_{s}\left(1-e^{-t / R C}\right)
$$

Suppose the controller has been programmed to fire an electrical pulse to stimulate the heart when $v_{C}=0.75 \mathrm{~V}_{s}$. Given values of $R$ and $C$ we can determine the resulting heart rate in beats per minute as follows:

$$
H=\frac{60}{-R C \ln 0.25}[\text { beats per minute }]
$$

A more realistic design problem requires you to calculate the value of resistance, $R$, given $V_{\max }$ as a percentage of $V_{s}, C$, and the desired heart rate in beats per minute. We leave you to develop an equation for resistance in Problem 7.106.
image_name:Figure 7.47
description:
[
'name': 'Vs', 'type': 'VoltageSource', 'value': 'Vs', 'ports': {'Np': 'Vs', 'Nn': 'GND'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'Vs', 'N2': 'Vc'
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'Vc', 'Nn': 'GND'
]
extrainfo:The circuit is an artificial pacemaker circuit with a voltage source Vs charging a capacitor C through a resistor R. The voltage across the capacitor is denoted as Vc.


Figure 7.47 $\boldsymbol{\square}$ The artificial pacemaker circuit at $t=0$, when the capacitor is charging.

NOTE: Assess your understanding of the Practical Perspective by solving Chapter Problems 7.104-7.107.

## Summary

- A first-order circuit may be reduced to a Thévenin (or Norton) equivalent connected to either a single equivalent inductor or capacitor. (See page 214.)
- The natural response is the currents and voltages that exist when stored energy is released to a circuit that contains no independent sources. (See page 212.)
- The time constant of an $R L$ circuit equals the equivalent inductance divided by the Thévenin resistance as viewed from the terminals of the equivalent inductor. (See page 216.)
- The time constant of an $R C$ circuit equals the equivalent capacitance times the Thévenin resistance as viewed from the terminals of the equivalent capacitor. (See page 221.)
- The step response is the currents and voltages that result from abrupt changes in dc sources connected to a circuit. Stored energy may or may not be present at the time the abrupt changes take place. (See page 224.)
- The solution for either the natural or step response of both $R L$ and $R C$ circuits involves finding the initial and final value of the current or voltage of interest and the time constant of the circuit. Equations 7.59 and 7.60 summarize this approach. (See page 232.)
- Sequential switching in first-order circuits is analyzed by dividing the analysis into time intervals corresponding to specific switch positions. Initial values for a particular interval are determined from the solution corresponding to the immediately preceding interval. (See page 236.)
- An unbounded response occurs when the Thévenin resistance is negative, which is possible when the first-order circuit contains dependent sources. (See page 240.)
- An integrating amplifier consists of an ideal op amp, a capacitor in the negative feedback branch, and a resistor in series with the signal source. It outputs the integral of the signal source, within specified limits that avoid saturating the op amp. (See page 241.)
