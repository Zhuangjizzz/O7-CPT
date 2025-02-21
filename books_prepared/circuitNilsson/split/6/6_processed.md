# 6. Inductance, Capacitance, and Mutual Inductance

CHAPTER CONTENTS

6.1 The Inductor p. 176
6.2 The Capacitor p. 182
6.3 Series-Parallel Combinations of Inductance and Capacitance p. 187
6.4 Mutual Inductance p. 189
6.5 A Closer Look at Mutual Inductance p. 193

CHAPTER OBJECTIVES

1 Know and be able to use the equations for voltage, current, power, and energy in an inductor; understand how an inductor behaves in the presence of constant current, and the requirement that the current be continuous in an inductor.

2 Know and be able to use the equations for voltage, current, power, and energy in a capacitor; understand how a capacitor behaves in the presence of constant voltage, and the requirement that the voltage be continuous in a capacitor.
3 Be able to combine inductors with initial conditions in series and in parallel to form a single equivalent inductor with an initial condition; be able to combine capacitors with initial conditions in series and in parallel to form a single equivalent capacitor with an initial condition.
4 Understand the basic concept of mutual inductance and be able to write mesh-current equations for a circuit containing magnetically coupled coils using the dot convention correctly.

Inductance, Capacitance, and Mutual Inductance

We begin this chapter by introducing the last two ideal circuit elements mentioned in Chapter 2, namely, inductors and capacitors. Be assured that the circuit analysis techniques introduced in Chapters 3 and 4 apply to circuits containing inductors and capacitors. Therefore, once you understand the terminal behavior of these elements in terms of current and voltage, you can use Kirchhoff's laws to describe any interconnections with the other basic elements. Like other components, inductors and capacitors are easier to describe in terms of circuit variables rather than electromagnetic field variables. However, before we focus on the circuit descriptions, a brief review of the field concepts underlying these basic elements is in order.

An inductor is an electrical component that opposes any change in electrical current. It is composed of a coil of wire wound around a supporting core whose material may be magnetic or nonmagnetic. The behavior of inductors is based on phenomena associated with magnetic fields. The source of the magnetic field is charge in motion, or current. If the current is varying with time, the magnetic field is varying with time. A timevarying magnetic field induces a voltage in any conductor linked by the field. The circuit parameter of inductance relates the induced voltage to the current. We discuss this quantitative relationship in Section 6.1.

A capacitor is an electrical component that consists of two conductors separated by an insulator or dielectric material. The capacitor is the only device other than a battery that can store electrical charge. The behavior of capacitors is based on phenomena associated with electric fields. The source of the electric field is separation of charge, or voltage. If the voltage is varying with time, the electric field is varying with time. A time-varying electric field produces a displacement current in the space occupied by the field. The circuit parameter of capacitance relates the displacement current to the voltage, where the displacement current is equal to the conduction current at the terminals of the capacitor. We discuss this quantitative relationship in Section 6.2.

Practical Perspective

Capacitive Touch Screens

The Practical Perspective in Chapter 3 showed how a grid of resistors is used to create a touch screen for a phone or computer monitor. But resistive touch screens have some limitations, the most important of which is that the screen can only process a single touch at any instant in time (see Problem 3.75). For example, a resistive touch screen cannot process the "pinch" gesture used by many devices to enlarge or shrink the image on the screen.

Multi-touch screens use a different component within a grid below the screen - capacitors. As you are about to
discover in this chapter, a capacitor is a circuit element whose terminal characteristics are determined by electric fields. When you touch a capacitive touch screen, you produce a change in the value of a capacitor, causing a voltage change. Once you have learned the basic behavior of capacitors and have learned how they combine in series and in parallel, we will present two possible designs for a multi-touch screen using a grid of capacitors. These designs are presented in the Practical Perspective example at the end of this chapter.
image_name:cobalt88/Shutterstock
description:The image depicts a digital tablet with a capacitive touch screen, which is a common type of touchscreen technology used in modern devices. The screen displays a user interface with multiple application icons arranged in a grid pattern against a blue background. These icons represent different applications, such as a web browser, calculator, music player, and calendar, among others. The top of the screen shows a status bar with indicators for battery life, signal strength, and the current time (4:44 PM).

1. **Identification of Components and Structure:**
- The primary component is the capacitive touch screen of the tablet.
- The screen displays various colorful application icons, each representing a specific function or app.

2. **Connections and Interactions:**
- The capacitive touch screen operates by detecting changes in the electric field when a user touches the screen, allowing for interaction with the displayed applications.
- There are no visible physical connections or wiring in the image, as it focuses on the screen interface.

3. **Labels, Annotations, and Key Features:**
- The status bar at the top provides essential information such as time, battery status, and signal strength.
- The icons are visually distinct, each designed to represent its respective application clearly.
- The bottom of the screen features navigation arrows, suggesting the ability to scroll or switch between different screens or menus within the tablet interface.

cobalt88/Shutterstock
image_name:
description:The image illustrates three hand gestures commonly used on touch screen devices. Each gesture is demonstrated with a simple line drawing of a hand and directional arrows indicating movement.

1. **Top Right Gesture:** A hand is shown pinching with the thumb and index finger, moving closer together. This gesture is typically used for zooming out on a touch screen.

2. **Bottom Right Gesture:** The hand is depicted with the thumb and index finger moving apart. This gesture usually represents zooming in on a touch screen.

3. **Left Gesture:** A hand is shown with the thumb and index finger sliding downwards. This movement is often used for scrolling down or swiping on a touch interface.

The gestures are accompanied by red arrows that indicate the direction of the finger movements, and there are blue circles highlighting the points of contact on the screen. These illustrations help in understanding how to interact with a touch screen device using basic gestures.


The inductor $v-i$ equation
image_name:(a)
description:
[
'name': 'L', 'type': 'Inductor', 'value': 'L', 'ports': {'N1': 'N1', 'N2': 'N2'
]
extrainfo:The diagram shows an inductor with inductance L connected between two nodes labeled N1 and N2.

(a)
image_name:(a)
description:
[
'name': 'L', 'type': 'Inductor', 'value': 'L', 'ports': {'N1': 'N1', 'N2': 'N2'
]
extrainfo:The diagram shows an inductor with inductance L connected between two nodes labeled N1 and N2, following the passive sign convention with voltage v and current i directions indicated.

(b)

Figure 6.1 (a) The graphic symbol for an inductor with an inductance of $L$ henrys. (b) Assigning reference voltage and current to the inductor, following the passive sign convention.

Section 6.3 describes techniques used to simplify circuits with series or parallel combinations of capacitors or inductors.

Energy can be stored in both magnetic and electric fields. Hence you should not be too surprised to learn that inductors and capacitors are capable of storing energy. For example, energy can be stored in an inductor and then released to fire a spark plug. Energy can be stored in a capacitor and then released to fire a flashbulb. In ideal inductors and capacitors, only as much energy can be extracted as has been stored. Because inductors and capacitors cannot generate energy, they are classified as passive elements.

In Sections 6.4 and 6.5 we consider the situation in which two circuits are linked by a magnetic field and thus are said to be magnetically coupled. In this case, the voltage induced in the second circuit can be related to the time-varying current in the first circuit by a parameter known as mutual inductance. The practical significance of magnetic coupling unfolds as we study the relationships between current, voltage, power, and several new parameters specific to mutual inductance. We introduce these relationships here and then describe their utility in a device called a transformer in Chapters 9 and 10.

## 6.1 The Inductor

Inductance is the circuit parameter used to describe an inductor. Inductance is symbolized by the letter $L$, is measured in henrys $(\mathrm{H})$, and is represented graphically as a coiled wire-a reminder that inductance is a consequence of a conductor linking a magnetic field. Figure 6.1(a) shows an inductor. Assigning the reference direction of the current in the direction of the voltage drop across the terminals of the inductor, as shown in Fig. 6.1(b), yields

$$
\begin{equation*}
v=L \frac{d i}{d t} \tag{6.1}
\end{equation*}
$$

where $v$ is measured in volts, $L$ in henrys, $i$ in amperes, and $t$ in seconds. Equation 6.1 reflects the passive sign convention shown in Fig. 6.1(b); that is, the current reference is in the direction of the voltage drop across the inductor. If the current reference is in the direction of the voltage rise, Eq. 6.1 is written with a minus sign.

Note from Eq. 6.1 that the voltage across the terminals of an inductor is proportional to the time rate of change of the current in the inductor. We can make two important observations here. First, if the current is constant, the voltage across the ideal inductor is zero. Thus the inductor behaves as a short circuit in the presence of a constant, or dc, current. Second, current cannot change instantaneously in an inductor; that is, the current cannot change by a finite amount in zero time. Equation 6.1 tells us that this change would require an infinite voltage, and infinite voltages are not possible. For example, when someone opens the switch on an inductive circuit in an actual system, the current initially continues to flow in the air across the switch, a phenomenon called arcing. The arc across the switch prevents the current from dropping to zero instantaneously. Switching inductive circuits is an important engineering problem, because arcing and voltage surges must be controlled to prevent equipment damage. The first step to understanding the nature of this problem is to master the introductory material presented in this and the following two chapters. Example 6.1 illustrates the application of Eq. 6.1 to a simple circuit.

#### Example 6.1 Determining the Voltage, Given the Current, at the Terminals of an Inductor

The independent current source in the circuit shown in Fig. 6.2 generates zero current for $t<0$ and a pulse $10 t e^{-5 t} \mathrm{~A}$, for $t>0$.
image_name:Figure 6.2
description:
[
'name': 'i', 'type': 'CurrentSource', 'value': 'i', 'ports': {'Np': 'b', 'Nn': 'a'
'name': 'L1', 'type': 'Inductor', 'value': '100mH', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit consists of a current source and a 100 mH inductor connected in parallel. The current source generates a pulse of 10te^(-5t) A for t > 0. The voltage across the inductor is expressed as a function of time.


Figure 6.2 $\triangle$ The circuit for Example 6.1.
a) Sketch the current waveform.
b) At what instant of time is the current maximum?
c) Express the voltage across the terminals of the 100 mH inductor as a function of time.
d) Sketch the voltage waveform.
e) Are the voltage and the current at a maximum at the same time?
f) At what instant of time does the voltage change polarity?
g) Is there ever an instantaneous change in voltage across the inductor? If so, at what time?

#### Solution

a) Figure 6.3 shows the current waveform.
b) $d i / d t=10\left(-5 t e^{-5 t}+e^{-5 t}\right)=10 e^{-5 t}$
$(1-5 t) \mathrm{A} / \mathrm{s} ; d i / d t=0$ when $t=\frac{1}{5} \mathrm{~s}$. (See Fig. 6.3.)
c) $v=L d i / d t=(0.1) 10 e^{-5 t}(1-5 t)=e^{-5 t}$ $(1-5 t) \mathrm{V}, t>0 ; v=0, t<0$.
d) Figure 6.4 shows the voltage waveform.
e) No; the voltage is proportional to $d i / d t$, not $i$.
f) At 0.2 s , which corresponds to the moment when $d i / d t$ is passing through zero and changing sign.
g) Yes, at $t=0$. Note that the voltage can change instantaneously across the terminals of an inductor.
image_name:Figure 6.3
description:The graph depicted in Figure 6.3 is a time-domain waveform representing the current \( i(t) \) in amperes (A) as a function of time \( t \) in seconds (s). The horizontal axis is labeled \( t(s) \) and the vertical axis is labeled \( i(A) \). The scale on both axes is linear.

**Overall Behavior and Trends:**
The graph shows a transient response of current in an inductor. Initially, the current starts at zero at \( t = 0 \) and increases rapidly in a concave upward manner, reaching a peak value of approximately 0.736 A at around \( t = 0.2 \) seconds. After reaching this maximum, the current begins to decrease in a concave downward manner, indicating a decay.

**Key Features and Technical Details:**
- **Peak Current:** The maximum current of 0.736 A occurs at \( t = 0.2 \) seconds.
- **Zero Crossing:** The current starts at zero at \( t = 0 \).
- **Inflection Point:** The graph transitions from concave upward to concave downward at the peak.

**Annotations and Specific Data Points:**
The graph includes dashed lines to highlight the peak current value (0.736 A) and the corresponding time (0.2 s), providing a visual reference for these critical values.

This waveform illustrates the behavior of the current through an inductor in response to a change in voltage, highlighting the transient nature of inductive circuits where the current initially rises to a peak before decaying over time.


Figure 6.3 $\boldsymbol{\Delta}$ The current waveform for Example 6.1.
image_name:Figure 6.4
description:**Type of Graph and Function:** The graph is a time-domain waveform depicting the voltage across an inductor as a function of time.

**Axes Labels and Units:** The x-axis represents time in seconds (s), and the y-axis represents voltage in volts (V). The graph uses a linear scale for both axes, with time marked at intervals of 0.2 seconds and voltage marked at 0.5-volt intervals.

**Overall Behavior and Trends:** The waveform shows an exponential decay behavior starting from 1.0 V at time t = 0 s. The voltage decreases sharply at first and then levels off as time progresses, indicating a typical transient response of an inductive circuit. After reaching a minimum, the waveform shows a small oscillation around the time mark of 0.6 s, suggesting a damping effect.

**Key Features and Technical Details:**
- **Initial Voltage:** The waveform starts at 1.0 V at t = 0 s.
- **Decay:** The voltage decreases rapidly, following an exponential decay pattern.
- **Oscillation:** A slight oscillation is observed around the 0.6-second mark, indicating a damped response.
- **Asymptotic Behavior:** The waveform approaches zero volts as time increases but never quite reaches it, typical of a decaying exponential function.

**Annotations and Specific Data Points:**
- The graph does not include specific annotations or markers for critical values other than the initial voltage and time intervals. The decay and oscillation points are inferred from the graph's shape.


Figure 6.4 $\boldsymbol{\Delta}$ The voltage waveform for Example 6.1.

### Current in an Inductor in Terms of the Voltage Across the Inductor

Equation 6.1 expresses the voltage across the terminals of an inductor as a function of the current in the inductor. Also desirable is the ability to express the current as a function of the voltage. To find $i$ as a function of $v$, we start by multiplying both sides of Eq. 6.1 by a differential time $d t$ :

$$
\begin{equation*}
v d t=L\left(\frac{d i}{d t}\right) d t \tag{6.2}
\end{equation*}
$$

Multiplying the rate at which $i$ varies with $t$ by a differential change in time generates a differential change in $i$, so we write Eq. 6.2 as

$$
\begin{equation*}
v d t=L d i \tag{6.3}
\end{equation*}
$$

The inductor $i-v$ equation

We next integrate both sides of Eq. 6.3. For convenience, we interchange the two sides of the equation and write

$$
\begin{equation*}
L \int_{i\left(t_{0}\right)}^{i(t)} d x=\int_{t_{0}}^{t} v d \tau \tag{6.4}
\end{equation*}
$$

Note that we use $x$ and $\tau$ as the variables of integration, whereas $i$ and $t$ become limits on the integrals. Then, from Eq. 6.4,

$$
\begin{equation*}
i(t)=\frac{1}{L} \int_{t_{0}}^{t} v d \tau+i\left(t_{0}\right) \tag{6.5}
\end{equation*}
$$

where $i(t)$ is the current corresponding to $t$, and $i\left(t_{0}\right)$ is the value of the inductor current when we initiate the integration, namely, $t_{0}$. In many practical applications, $t_{0}$ is zero and Eq. 6.5 becomes

$$
\begin{equation*}
i(t)=\frac{1}{L} \int_{0}^{t} v d \tau+i(0) \tag{6.6}
\end{equation*}
$$

Equations 6.1 and 6.5 both give the relationship between the voltage and current at the terminals of an inductor. Equation 6.1 expresses the voltage as a function of current, whereas Eq. 6.5 expresses the current as a function of voltage. In both equations the reference direction for the current is in the direction of the voltage drop across the terminals. Note that $i\left(t_{0}\right)$ carries its own algebraic sign. If the initial current is in the same direction as the reference direction for $i$, it is a positive quantity. If the initial current is in the opposite direction, it is a negative quantity. Example 6.2 illustrates the application of Eq. 6.5.

#### Example 6.2 Determining the Current, Given the Voltage, at the Terminals of an Inductor

The voltage pulse applied to the 100 mH inductor shown in Fig. 6.5 is 0 for $t<0$ and is given by the expression

$$
v(t)=20 t e^{-10 t} \mathrm{~V}
$$

for $t>0$. Also assume $i=0$ for $t \leq 0$.
a) Sketch the voltage as a function of time.
b) Find the inductor current as a function of time.
c) Sketch the current as a function of time.

#### Solution

a) The voltage as a function of time is shown in Fig. 6.6.
b) The current in the inductor is 0 at $t=0$. Therefore, the current for $t>0$ is

$$
i=\frac{1}{0.1} \int_{0}^{t} 20 \tau e^{-10 \tau} d \tau+0
$$

$$
\begin{aligned}
& =\left.200\left[\frac{-e^{-10 \tau}}{100}(10 \tau+1)\right]\right|_{0} ^{t}, \\
& =2\left(1-10 t e^{-10 t}-e^{-10 t}\right) \mathrm{A}, \quad t>0 .
\end{aligned}
$$

c) Figure 6.7 shows the current as a function of time.
image_name:Figure 6.5 The circuit for Example 6.2
description:
[
'name': 'V', 'type': 'VoltageSource','value':'V', 'ports': {'Np': 'a', 'Nn': 'b'
'name': 'L', 'type': 'Inductor', 'value': '100mH', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit consists of a voltage source V and an inductor L with a value of 100 mH. The voltage across the source is 0 for t < 0 and v = 20te^{-10t} V for t > 0. The current through the inductor is initially 0 at t=0 and changes over time as described by the given equations.


Figure 6.5 $\triangle$ The circuit for Example 6.2.
image_name:Figure 6.6
description:The graph in Figure 6.6 is a time-domain waveform depicting the voltage across a voltage source in a circuit. The x-axis represents time in seconds (s), and the y-axis represents voltage in volts (V). The scale for both axes is linear. \n\nThe waveform starts at the origin (0,0) and initially rises sharply, reaching a peak voltage of approximately 0.736 V at around 0.1 seconds. After reaching this peak, the voltage begins to decrease, following a smooth, exponential decay trend as time progresses. By around 0.3 seconds, the voltage approaches zero, indicating that the waveform is asymptotically decaying towards zero as time increases. \n\nKey features of this graph include the peak value of 0.736 V and the time at which this peak occurs, approximately 0.1 seconds. The graph also shows a characteristic exponential decay after the peak, consistent with the behavior of an inductor in response to a transient voltage source.


Figure 6.6 $\boldsymbol{\Delta}$ The voltage waveform for Example 6.2.
image_name:Figure 6.7 The current waveform for Example 6.2
description:Figure 6.7 is a time-domain waveform graph depicting the current \( i \) in amperes (A) over time \( t \) in seconds (s). The horizontal axis represents time, ranging from 0 to approximately 0.35 seconds, while the vertical axis represents current, ranging from 0 to 2.5 amperes.

The graph shows a gradual increase in current starting from zero, indicating an initial rise as time progresses. The curve is smooth and exhibits a decaying slope, suggesting that the rate of increase in current slows down over time. This behavior is typical of an inductor's response to a transient voltage source, where the current eventually approaches a steady state.

Key features of the graph include:
- The current starts at 0 A at \( t = 0 \) seconds.
- The current increases steadily, reaching approximately 2 A as time approaches 0.35 seconds.
- The curve's slope decreases over time, indicating an asymptotic approach towards a constant current value, which aligns with the context provided that \( i \) approaches a constant value of 2 A as \( t \) increases.

This graph visually represents the inductor current's behavior in Example 6.2, showing the transition from an initial transient state to a steady state.


Figure 6.7 $\boldsymbol{\Delta}$ The current waveform for Example 6.2.

Note in Example 6.2 that $i$ approaches a constant value of 2 A as $t$ increases. We say more about this result after discussing the energy stored in an inductor.

Power and Energy in the Inductor

The power and energy relationships for an inductor can be derived directly from the current and voltage relationships. If the current reference is in the direction of the voltage drop across the terminals of the inductor, the power is

$$
\begin{equation*}
p=v i \tag{6.7}
\end{equation*}
$$

Remember that power is in watts, voltage is in volts, and current is in amperes. If we express the inductor voltage as a function of the inductor current, Eq. 6.7 becomes

$$
\begin{equation*}
p=L i \frac{d i}{d t} \tag{6.8}
\end{equation*}
$$

Power in an inductor

We can also express the current in terms of the voltage:

$$
\begin{equation*}
p=v\left[\frac{1}{L} \int_{t_{0}}^{t} v d \tau+i\left(t_{0}\right)\right] \tag{6.9}
\end{equation*}
$$

Equation 6.8 is useful in expressing the energy stored in the inductor. Power is the time rate of expending energy, so

$$
\begin{equation*}
p=\frac{d w}{d t}=L i \frac{d i}{d t} \tag{6.10}
\end{equation*}
$$

Multiplying both sides of Eq. 6.10 by a differential time gives the differential relationship

$$
\begin{equation*}
d w=L i d i \tag{6.11}
\end{equation*}
$$

Both sides of Eq. 6.11 are integrated with the understanding that the reference for zero energy corresponds to zero current in the inductor. Thus

$$
\begin{gather*}
\int_{0}^{w} d x=L \int_{0}^{i} y d y \\
w=\frac{1}{2} L i^{2} \tag{6.12}
\end{gather*}
$$

As before, we use different symbols of integration to avoid confusion with the limits placed on the integrals. In Eq. 6.12, the energy is in joules, inductance is in henrys, and current is in amperes. To illustrate the application of Eqs. 6.7 and 6.12, we return to Examples 6.1 and 6.2 by means of Example 6.3.

#### Example 6.3 Determining the Current, Voltage, Power, and Energy for an Inductor

a) For Example 6.1, plot $i, v, p$, and $w$ versus time. Line up the plots vertically to allow easy assessment of each variable's behavior.
b) In what time interval is energy being stored in the inductor?
c) In what time interval is energy being extracted from the inductor?
d) What is the maximum energy stored in the inductor?
e) Evaluate the integrals

$$
\int_{0}^{0.2} p d t \quad \text { and } \quad \int_{0.2}^{\infty} p d t
$$

and comment on their significance.
f) Repeat (a)-(c) for Example 6.2.
g) In Example 6.2, why is there a sustained current in the inductor as the voltage approaches zero?

#### Solution

a) The plots of $i, v, p$, and $w$ follow directly from the expressions for $i$ and $v$ obtained in Example 6.1 and are shown in Fig. 6.8. In particular, $p=v i$, and $w=\left(\frac{1}{2}\right) L i^{2}$.
b) An increasing energy curve indicates that energy is being stored. Thus energy is being stored in the time interval 0 to 0.2 s . Note that this corresponds to the interval when $p>0$.
c) A decreasing energy curve indicates that energy is being extracted. Thus energy is being extracted in the time interval 0.2 s to $\infty$. Note that this corresponds to the interval when $p<0$.
d) From Eq. 6.12 we see that energy is at a maximum when current is at a maximum; glancing at the graphs confirms this. From Example 6.1, maximum current $=0.736$ A. Therefore, $w_{\max }=27.07 \mathrm{~mJ}$.
e) From Example 6.1,

$$
i=10 t e^{-5 t} \mathrm{~A} \quad \text { and } \quad v=e^{-5 t}(1-5 t) \mathrm{V}
$$

Therefore,

$$
p=v i=10 t e^{-10 t}-50 t^{2} e^{-10 t} \mathrm{~W}
$$

image_name:Figure 6.8
description:The graph in Figure 6.8 consists of two separate plots, each representing a function of time (t) in seconds.

1. **Current (i) vs. Time (t) Graph**:
- **Type of Graph**: Time-domain waveform.
- **Axes Labels and Units**:
- The vertical axis represents current (i) in milliamperes (mA).
- The horizontal axis represents time (t) in seconds (s).
- **Overall Behavior and Trends**:
- The current starts at 0 mA at t = 0 s and rises sharply to a peak of approximately 800 mA around t = 0.2 s.
- After reaching the peak, the current decreases gradually, approaching 0 mA as time approaches 1 s.
- **Key Features and Technical Details**:
- The peak current is a significant feature, indicating the maximum current reached during the interval.
- The curve exhibits an exponential decay after the peak.

2. **Voltage (v) vs. Time (t) Graph**:
- **Type of Graph**: Time-domain waveform.
- **Axes Labels and Units**:
- The vertical axis represents voltage (v) in volts (V).
- The horizontal axis represents time (t) in seconds (s).
- **Overall Behavior and Trends**:
- The voltage starts at approximately 1 V at t = 0 s and decreases rapidly, crossing the 0 V line at around t = 0.3 s.
- It reaches a minimum of approximately -0.5 V around t = 0.4 s and then gradually increases, approaching 0 V as time approaches 1 s.
- **Key Features and Technical Details**:
- The zero crossing point and the minimum voltage are important features.
- The voltage exhibits an initial rapid decay followed by a slight increase towards zero, indicating a damped oscillatory behavior.

image_name:Figure 6.8
description:The graph in Figure 6.8 is a time-domain waveform showing the power \( p \) in milliwatts (mW) as a function of time \( t \) in seconds (s). The horizontal axis represents time, ranging from 0 to 1 second, while the vertical axis represents power, with markings at 100 mW and 200 mW.

**Overall Behavior and Trends:**
- The graph begins at a power level slightly above 0 mW at \( t = 0 \) and rapidly increases to a peak of approximately 220 mW around \( t = 0.1 \) seconds.
- After reaching this peak, the power decreases sharply, crossing the 0 mW line at approximately \( t = 0.25 \) seconds.
- The power reaches a minimum of about -50 mW around \( t = 0.35 \) seconds, indicating a negative power value at this point.
- Following the minimum, the power gradually increases, crossing the 0 mW line again near \( t = 0.55 \) seconds, and continues to rise slowly towards 0 mW as \( t \) approaches 1 second.

**Key Features and Technical Details:**
- The graph exhibits a damped oscillatory behavior, characterized by an initial rapid increase and subsequent decrease, followed by a smaller oscillation.
- Important features include the initial peak at 220 mW, the zero crossing points at approximately 0.25 s and 0.55 s, and the minimum power value of -50 mW at 0.35 s.
- The graph indicates a system that initially stores energy rapidly and then releases it in a damped manner, typical of systems with transient responses.

**Annotations and Specific Data Points:**
- The peak power value is around 220 mW at 0.1 s.
- The minimum power value is approximately -50 mW at 0.35 s.
- The zero-crossing points occur at approximately 0.25 s and 0.55 s.

image_name:Figure 6.8
description:The graph in Figure 6.8 is a time-domain waveform depicting the behavior of energy stored in a system over time. The x-axis represents time \( t \) in seconds, ranging from 0 to 1 second, while the y-axis represents energy \( w \) in millijoules (mJ), with values ranging from 0 to 35 mJ.

**Overall Behavior and Trends:**
- The graph shows a rapid increase in energy stored, reaching a peak, followed by a gradual decrease, indicating a damped release of energy typical of transient responses in systems.
- The curve starts at the origin (0,0), indicating no initial stored energy, and rises steeply to a peak value.

**Key Features and Technical Details:**
- The peak energy value is approximately 30 mJ, occurring around 0.2 seconds.
- After reaching the peak, the energy decreases exponentially, approaching zero as time progresses towards 1 second.

**Annotations and Specific Data Points:**
- The rapid rise and subsequent decay suggest the system initially stores energy quickly and then releases it in a damped manner, aligning with transient response behavior.
- The graph does not explicitly show zero-crossing points or negative values, as it represents energy which is a non-negative quantity.

This waveform is characteristic of systems where energy is temporarily stored and then dissipated, such as in electrical circuits or mechanical systems with damping.


Figure 6.8 $\triangle$ The variables $i, v, p$, and $w$ versus $t$ for Example 6.1.

Thus

$$
\begin{aligned}
& \int_{0}^{0.2} p d t=10\left[\frac{e^{-10 t}}{100}(-10 t-1)\right]_{0}^{0.2} \\
& -50\left\{\frac{t^{2} e^{-10 t}}{-10}+\frac{2}{10}\left[\frac{e^{-10 t}}{100}(-10 t-1)\right]\right\}_{0}^{0.2} \\
& =0.2 e^{-2}=27.07 \mathrm{~mJ} \text {, } \\
& \int_{0.2}^{\infty} p d t=10\left[\frac{e^{-10 t}}{100}(-10 t-1)\right]_{0.2}^{\infty} \\
& -50\left\{\frac{t^{2} e^{-10 t}}{-10}+\frac{2}{10}\left[\frac{e^{-10 t}}{100}(-10 t-1)\right]\right\}_{0.2}^{\infty} \\
& =-0.2 e^{-2}=-27.07 \mathrm{~mJ} .
\end{aligned}
$$

Based on the definition of $p$, the area under the plot of $p$ versus $t$ represents the energy expended over the interval of integration. Hence the integration of the power between 0 and 0.2 s represents the energy stored in the inductor during this time interval. The integral of $p$ over the interval $0.2 \mathrm{~s}-\infty$ is the energy extracted. Note that in this time interval, all the energy originally stored is removed; that is, after the current peak has passed, no energy is stored in the inductor.
f) The plots of $v, i, p$, and $w$ follow directly from the expressions for $v$ and $i$ given in Example 6.2 and are shown in Fig. 6.9. Note that in this case the power is always positive, and hence energy is always being stored during the voltage pulse.
g) The application of the voltage pulse stores energy in the inductor. Because the inductor is ideal, this energy cannot dissipate after the voltage subsides to zero. Therefore, a sustained current circulates in the circuit. A lossless inductor obviously is an ideal circuit element. Practical inductors require a resistor in the circuit model. (More about this later.)
image_name:Figure 6.9
description:The graph in Figure 6.9 consists of four subplots, each representing the behavior of different electrical quantities over time for an inductor in a circuit. The x-axis of all subplots is time \( t \) measured in seconds, ranging from 0 to 0.6 seconds.

1. **Voltage \( v(t) \):**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The y-axis represents voltage \( v \) in volts (V).
- **Overall Behavior and Trends:** The voltage starts at 0 V, rises to a peak slightly above 1 V around 0.05 seconds, and then gradually decays back towards 0 V by 0.6 seconds. This represents a typical voltage pulse.
- **Key Features:** The peak voltage occurs around 0.05 seconds.

2. **Current \( i(t) \):**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The y-axis represents current \( i \) in amperes (A).
- **Overall Behavior and Trends:** The current starts at 0 A and increases steadily, reaching around 2.5 A by the end of the time period. This indicates continuous current flow as energy is stored in the inductor.
- **Key Features:** The current shows a continuous rise without any peaks or dips.

3. **Power \( p(t) \):**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The y-axis represents power \( p \) in milliwatts (mW).
- **Overall Behavior and Trends:** The power starts at 0 mW, rises to a peak of around 600 mW at approximately 0.1 seconds, and then decreases back towards 0 mW as time progresses.
- **Key Features:** The peak power aligns with the peak voltage, indicating maximum energy transfer at this point.

4. **Energy \( w(t) \):**
- **Type of Graph:** Time-domain waveform.
- **Axes Labels and Units:** The y-axis represents energy \( w \) in millijoules (mJ).
- **Overall Behavior and Trends:** The energy starts at 0 mJ and increases steadily throughout the time period, reaching around 200 mJ by 0.6 seconds. This reflects the continuous storage of energy in the ideal inductor.
- **Key Features:** The energy curve is monotonically increasing, indicating no energy dissipation, consistent with an ideal inductor model.


Figure $6.9 \triangle$ The variables $v, i, p$, and $w$ versus $t$ for Example 6.2.

ASSESSMENT PROBLEM

Objective 1—Know and be able to use the equations for voltage, current, power, and energy in an inductor

6.1 The current source in the circuit shown generates the current pulse

$$
\begin{array}{ll}
i_{g}(t)=0, & t<0 \\
i_{g}(t)=8 e^{-300 t}-8 e^{-1200 t} \mathrm{~A}, & t \geq 0
\end{array}
$$

image_name:(a)
description:
[
'name': 'ig', 'type': 'CurrentSource', 'ports': {'Np': 'b', 'Nn': 'a'
'name': 'L1', 'type': 'Inductor', 'value': '4mH', 'ports': {'N1': 'a', 'N2': 'b'
]
extrainfo:The circuit consists of a current source and an inductor connected in parallel. The current source generates a current pulse, and the inductor has a value of 4 mH.


Answer: (a) 28.8 V ;
(b) 1.54 ms ;
(c) $-76.8 e^{-600 t}+384 e^{-1500 t}$
$-307.2 e^{-2400 t} \mathrm{~W}, t \geq 0$;
(d) $411.05 \mu \mathrm{~s}$;
(e) 32.72 W ;
(f) 1.54 ms ;
(g) 28.57 mJ .

NOTE: Also try Chapter Problems 6.2 and 6.8.
image_name:Figure 6.10 (a)
description:
[
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'X1', 'Nn': 'X2'
]
extrainfo:The diagram shows a capacitor 'C' connected between nodes X1 and X2.

(a)
image_name:Figure 6.10 (a)
description:
[
'name': 'C', 'type': 'Capacitor', 'value': 'C', 'ports': {'Np': 'X1', 'Nn': 'X2'
]
extrainfo:The diagram shows a capacitor 'C' connected between nodes X1 and X2, following the passive sign convention with voltage 'v' and current 'i'.

(b)

Figure 6.10 (a) The circuit symbol for a capacitor. (b) Assigning reference voltage and current to the capacitor, following the passive sign convention.

Capacitor $i-v$ equation

## 6.2 The Capacitor

The circuit parameter of capacitance is represented by the letter $C$, is measured in farads ( F ), and is symbolized graphically by two short parallel conductive plates, as shown in Fig. 6.10(a). Because the farad is an extremely large quantity of capacitance, practical capacitor values usually lie in the picofarad $(\mathrm{pF})$ to microfarad $(\mu \mathrm{F})$ range.

The graphic symbol for a capacitor is a reminder that capacitance occurs whenever electrical conductors are separated by a dielectric, or insulating, material. This condition implies that electric charge is not transported through the capacitor. Although applying a voltage to the terminals of the capacitor cannot move a charge through the dielectric, it can displace a charge within the dielectric. As the voltage varies with time, the displacement of charge also varies with time, causing what is known as the displacement current.

At the terminals, the displacement current is indistinguishable from a conduction current. The current is proportional to the rate at which the voltage across the capacitor varies with time, or, mathematically,

$$
\begin{equation*}
i=C \frac{d v}{d t} \tag{6.13}
\end{equation*}
$$

where $i$ is measured in amperes, $C$ in farads, $v$ in volts, and $t$ in seconds.
Equation 6.13 reflects the passive sign convention shown in Fig. 6.10(b); that is, the current reference is in the direction of the voltage drop across the capacitor. If the current reference is in the direction of the voltage rise, Eq. 6.13 is written with a minus sign.

Two important observations follow from Eq. 6.13. First, voltage cannot change instantaneously across the terminals of a capacitor. Equation 6.13 indicates that such a change would produce infinite current, a physical impossibility. Second, if the voltage across the terminals is constant, the capacitor current is zero. The reason is that a conduction current cannot be established in the dielectric material of the capacitor. Only a time-varying voltage can produce a displacement current. Thus a capacitor behaves as an open circuit in the presence of a constant voltage.

Equation 6.13 gives the capacitor current as a function of the capacitor voltage. Expressing the voltage as a function of the current is also useful. To do so, we multiply both sides of Eq. 6.13 by a differential time $d t$ and then integrate the resulting differentials:

$$
i d t=C d v \quad \text { or } \quad \int_{v\left(t_{0}\right)}^{v(t)} d x=\frac{1}{C} \int_{t_{0}}^{t} i d \tau
$$

Carrying out the integration of the left-hand side of the second equation gives

$$
\begin{equation*}
v(t)=\frac{1}{C} \int_{t_{0}}^{t} i d \tau+v\left(t_{0}\right) \tag{6.14}
\end{equation*}
$$

$\triangle$ Capacitor $v-i$ equation

In many practical applications of Eq. 6.14, the initial time is zero; that is, $t_{0}=0$. Thus Eq. 6.14 becomes

$$
\begin{equation*}
v(t)=\frac{1}{C} \int_{0}^{t} i d \tau+v(0) \tag{6.15}
\end{equation*}
$$

We can easily derive the power and energy relationships for the capacitor. From the definition of power,

$$
\begin{equation*}
p=v i=C v \frac{d v}{d t} \tag{6.16}
\end{equation*}
$$

Capacitor power equation
or

$$
\begin{equation*}
p=i\left[\frac{1}{C} \int_{t_{0}}^{t} i d \tau+v\left(t_{0}\right)\right] \tag{6.17}
\end{equation*}
$$

Combining the definition of energy with Eq. 6.16 yields

$$
d w=C v d v
$$

from which

$$
\int_{0}^{w} d x=C \int_{0}^{v} y d y
$$

or

Capacitor energy equation

$$
\begin{equation*}
w=\frac{1}{2} C v^{2} \tag{6.18}
\end{equation*}
$$

In the derivation of Eq. 6.18, the reference for zero energy corresponds to zero voltage.

Examples 6.4 and 6.5 illustrate the application of the current, voltage, power, and energy relationships for a capacitor.

#### Example 6.4 Determining Current, Voltage, Power, and Energy for a Capacitor

The voltage pulse described by the following equations is impressed across the terminals of a $0.5 \mu \mathrm{~F}$ capacitor:

$$
v(t)= \begin{cases}0, & t \leq 0 \mathrm{~s} \\ 4 t \mathrm{~V}, & 0 \mathrm{~s} \leq t \leq 1 \mathrm{~s} \\ 4 e^{-(t-1)} \mathrm{V}, & t \geq 1 \mathrm{~s}\end{cases}
$$

a) Derive the expressions for the capacitor current, power, and energy.
b) Sketch the voltage, current, power, and energy as functions of time. Line up the plots vertically.
c) Specify the interval of time when energy is being stored in the capacitor.
d) Specify the interval of time when energy is being delivered by the capacitor.
e) Evaluate the integrals

$$
\int_{0}^{1} p d t \quad \text { and } \quad \int_{1}^{\infty} p d t
$$

and comment on their significance.

#### Solution

a) From Eq. 6.13,

$$
i= \begin{cases}\left(0.5 \times 10^{-6}\right)(0)=0, & t<0 \mathrm{~s} \\ \left(0.5 \times 10^{-6}\right)(4)=2 \mu \mathrm{~A}, & 0 \mathrm{~s}<t<1 \mathrm{~s} \\ \left(0.5 \times 10^{-6}\right)\left(-4 e^{-(t-1)}\right)=-2 e^{-(t-1)} \mu \mathrm{A}, & t>1 \mathrm{~s}\end{cases}
$$

The expression for the power is derived from Eq. 6.16:

$$
p= \begin{cases}0, & t \leq 0 \mathrm{~s} \\ (4 t)(2)=8 t \mu \mathrm{~W}, & 0 \mathrm{~s} \leq t<1 \mathrm{~s} \\ \left(4 e^{-(t-1)}\right)\left(-2 e^{-(t-1)}\right)=-8 e^{-2(t-1)} \mu \mathrm{W}, & t>1 \mathrm{~s}\end{cases}
$$

The energy expression follows directly from Eq. 6.18:

$$
w= \begin{cases}0, & t \leq 0 \mathrm{~s} \\ \frac{1}{2}(0.5) 16 t^{2}=4 t^{2} \mu \mathrm{~J}, & 0 \mathrm{~s} \leq t \leq 1 \mathrm{~s} \\ \frac{1}{2}(0.5) 16 e^{-2(t-1)}=4 e^{-2(t-1)} \mu \mathrm{J}, & t \geq 1 \mathrm{~s}\end{cases}
$$

b) Figure 6.11 shows the voltage, current, power, and energy as functions of time.
c) Energy is being stored in the capacitor whenever the power is positive. Hence energy is being stored in the interval $0-1 \mathrm{~s}$.
d) Energy is being delivered by the capacitor whenever the power is negative. Thus energy is being delivered for all $t$ greater than 1 s .
e) The integral of $p d t$ is the energy associated with the time interval corresponding to the limits on the integral. Thus the first integral represents the energy stored in the capacitor between 0 and 1 s , whereas the second integral represents the energy returned, or delivered, by the capacitor in the interval 1 s to $\infty$ :

$$
\begin{aligned}
& \int_{0}^{1} p d t=\int_{0}^{1} 8 t d t=\left.4 t^{2}\right|_{0} ^{1}=4 \mu \mathrm{~J} \\
& \int_{1}^{\infty} p d t=\int_{1}^{\infty}\left(-8 e^{-2(t-1)}\right) d t=(-8)^{\left.\frac{e^{-2(t-1)}}{-2}\right|_{1} ^{\infty}=-4 \mu \mathrm{~J}}
\end{aligned}
$$

The voltage applied to the capacitor returns to zero as time increases without limit, so the energy returned by this ideal capacitor must equal the energy stored.
image_name:v, i, p, and w versus t for Example 6.4
description:The graph consists of four subplots, each representing different variables (voltage, current, power, and energy) versus time, corresponding to Example 6.4. The x-axis for all plots is time \( t \) in seconds, ranging from 0 to 6 seconds.

1. **Voltage \( v(t) \) vs. Time:**
- **Type of Graph:** Time-domain waveform.
- **Axes:** The y-axis represents voltage in volts (V), ranging from 0 to 4 volts.
- **Behavior:** The voltage increases linearly from 0 to a peak of 4 volts at 1 second, then decreases exponentially towards zero as time approaches infinity.
- **Key Features:** A peak at \( t = 1 \) second.

2. **Current \( i(t) \) vs. Time:**
- **Type of Graph:** Time-domain waveform.
- **Axes:** The y-axis represents current in microamperes (µA), ranging from -2 to 2 µA.
- **Behavior:** The current is initially 2 µA, drops to -2 µA at \( t = 1 \) second, and then approaches zero as time increases.
- **Key Features:** A sudden change in current at \( t = 1 \) second.

3. **Power \( p(t) \) vs. Time:**
- **Type of Graph:** Time-domain waveform.
- **Axes:** The y-axis represents power in microwatts (µW), ranging from -8 to 8 µW.
- **Behavior:** Power increases linearly to 8 µW at 1 second, then decreases exponentially to negative values, approaching zero as time increases.
- **Key Features:** A peak at \( t = 1 \) second.

4. **Energy \( w(t) \) vs. Time:**
- **Type of Graph:** Time-domain waveform.
- **Axes:** The y-axis represents energy in microjoules (µJ), ranging from 0 to 4 µJ.
- **Behavior:** Energy increases to a peak of 4 µJ at 1 second, then decreases exponentially towards zero.
- **Key Features:** A peak at \( t = 1 \) second, reflecting the energy stored and then returned by the capacitor.

Overall, the graphs depict the dynamic response of a capacitor to an input signal, with initial charging and subsequent discharging phases, characterized by exponential decay in voltage, power, and energy after reaching their respective peaks at 1 second.


Figure 6.11 $\triangle$ The variables $v, i, p$, and $w$ versus $t$ for Example 6.4.

#### Example 6.5 Finding $v, p$, and $w$ Induced by a Triangular Current Pulse for a Capacitor

An uncharged $0.2 \mu \mathrm{~F}$ capacitor is driven by a triangular current pulse. The current pulse is described by

$$
i(t)= \begin{cases}0, & t \leq 0 \\ 5000 t \mathrm{~A}, & 0 \leq t \leq 20 \mu \mathrm{~s} \\ 0.2-5000 t \mathrm{~A}, & 20 \leq t \leq 40 \mu \mathrm{~s} \\ 0, & t \geq 40 \mu \mathrm{~s}\end{cases}
$$

a) Derive the expressions for the capacitor voltage, power, and energy for each of the four time intervals needed to describe the current.
b) Plot $i, v, p$, and $w$ versus $t$. Align the plots as specified in the previous examples.
c) Why does a voltage remain on the capacitor after the current returns to zero?

#### Solution

a) For $t \leq 0, v, p$, and $w$ all are zero.

For $0 \leq t \leq 20 \mu s$,
$v=5 \times 10^{6} \int_{0}^{t}(5000 \tau) d \tau+0=12.5 \times 10^{9} t^{2} \mathrm{~V}$,
$p=v i=62.5 \times 10^{12} t^{3} \mathrm{~W}$,
$w=\frac{1}{2} C v^{2}=15.625 \times 10^{12} t^{4} \mathrm{~J}$.
For $20 \mu \mathrm{~s} \leq t \leq 40 \mu \mathrm{~s}$,

$$
v=5 \times 10^{6} \int_{20 \mu \mathrm{~s}}^{t}(0.2-5000 \tau) d \tau+5
$$

(Note that 5 V is the voltage on the capacitor at the end of the preceding interval.) Then,

$$
\begin{aligned}
v= & \left(10^{6} t-12.5 \times 10^{9} t^{2}-10\right) \mathrm{V} \\
p= & v i \\
= & \left(62.5 \times 10^{12} t^{3}-7.5 \times 10^{9} t^{2}+2.5 \times 10^{5} t-2\right) \mathrm{W} \\
w= & \frac{1}{2} C v^{2} \\
= & \left(15.625 \times 10^{12} t^{4}-2.5 \times 10^{9} t^{3}+0.125 \times 10^{6} t^{2}\right. \\
& \left.-2 t+10^{-5}\right) \mathrm{J} \\
\text { For } t \geq & 40 \mu \mathrm{~s} \\
v= & 10 \mathrm{~V} \\
p= & v i=0 \\
w= & \frac{1}{2} C v^{2}=10 \mu \mathrm{~J}
\end{aligned}
$$

b) The excitation current and the resulting voltage, power, and energy are plotted in Fig. 6.12.
c) Note that the power is always positive for the duration of the current pulse, which means that energy is continuously being stored in the capacitor. When the current returns to zero, the stored energy is trapped because the ideal capacitor offers no means for dissipating energy. Thus a voltage remains on the capacitor after $i$ returns to zero.
image_name:Figure 6.12 A
description:The graph in Figure 6.12 A is a time-domain waveform illustrating the current (i) over time (t). The x-axis represents time in microseconds (µs), ranging from 0 to 60 µs. The y-axis represents the current in milliamperes (mA), ranging from 0 to 100 mA.

The waveform shows a triangular pulse of current. It starts at 0 mA at 0 µs, rises linearly to a peak of 100 mA at 20 µs, and then decreases linearly back to 0 mA at 40 µs. After 40 µs, the current remains at 0 mA until 60 µs.

This behavior indicates a single triangular pulse of current, with the current increasing and decreasing symmetrically over a period of 40 µs. The peak current is 100 mA, occurring at the midpoint of the pulse duration.

image_name:Figure 6.12 A
description:The graph labeled "Figure 6.12 A" illustrates the voltage \( v \) in volts (V) as a function of time \( t \) in microseconds (µs). The horizontal axis represents time, ranging from 0 to 60 µs, while the vertical axis represents voltage, ranging from 0 to 10 V.

This is a time-domain waveform showing the behavior of voltage over time. The graph starts at 0 V at 0 µs and exhibits a smooth, increasing curve. The voltage rises gradually, reaching approximately 10 V by around 40 µs. From 40 µs to 60 µs, the voltage remains constant at 10 V, indicating that the system has reached a steady state.

Overall, the graph shows an initial exponential-like increase in voltage, which then stabilizes to a constant value. This behavior suggests a charging process, likely in a capacitive circuit, where the voltage across the capacitor increases over time until it reaches its maximum value and stabilizes.

image_name:Figure 6.12 A
description:The graph in Figure 6.12 A is a time-domain waveform depicting the power \( p \) in milliwatts (mW) versus time \( t \) in microseconds (µs). The horizontal axis represents time, ranging from 0 to 60 µs, while the vertical axis represents power, ranging from 0 to 600 mW.

Overall Behavior and Trends:
The graph shows a rise in power from 0 mW at 0 µs, reaching a peak of approximately 500 mW at around 25 µs. After this peak, the power decreases sharply, returning to 0 mW by 40 µs. From 40 µs to 60 µs, the power remains constant at 0 mW, indicating that the system has settled back to a state with no power output.

Key Features and Technical Details:
- **Initial Rise:** The power increases in a smooth, almost parabolic curve, suggesting a rapid increase in power consumption or output.
- **Peak Power:** The maximum power is approximately 500 mW, occurring at about 25 µs.
- **Sharp Decline:** After reaching its peak, the power decreases sharply back to 0 mW by 40 µs.
- **Steady State:** From 40 µs onwards, the power remains at 0 mW, indicating no power activity.

Annotations and Specific Data Points:
- The graph is annotated with clear axis labels and scales, helping to identify the critical points such as the peak at 25 µs and the return to zero power at 40 µs.

This graph likely represents a transient power event, such as the charging or discharging of a capacitor in an electrical circuit, where power is consumed rapidly and then dissipates back to zero.

image_name:Figure 6.12 A
description:This graph is a time-domain waveform representing energy storage in a capacitor over time. The x-axis is labeled as time \( t \) in microseconds (\( \mu s \)), ranging from 0 to 60 \( \mu s \). The y-axis is labeled as energy \( w \) in microjoules (\( \mu J \)), ranging from 0 to 12 \( \mu J \).

**Overall Behavior and Trends:**
- The graph shows a sigmoidal curve, indicating an initial rapid increase in energy storage, followed by a leveling off to a steady state.
- The energy stored in the capacitor begins at 0 \( \mu J \) and rises sharply between 10 \( \mu s \) and 30 \( \mu s \), reaching a maximum of approximately 11 \( \mu J \) by 40 \( \mu s \).
- After 40 \( \mu s \), the energy remains constant, indicating that the capacitor has reached its full charge and no further energy is being stored.

**Key Features and Technical Details:**
- The curve starts at the origin (0,0), representing no initial energy stored.
- The steepest part of the curve occurs between 10 \( \mu s \) and 30 \( \mu s \), which suggests this is the period of maximum energy transfer into the capacitor.
- Post 40 \( \mu s \), the curve flattens, indicating that the energy stored remains constant, consistent with the capacitor being fully charged.

**Annotations and Specific Data Points:**
- The graph is clearly annotated with axis labels and units, making it easy to identify critical points such as the rapid energy increase and the steady state.
- The maximum energy stored is approximately 11 \( \mu J \), and this value remains constant from 40 \( \mu s \) onwards.


Figure 6.12 A The variables $i, v, p$, and $w$ versus $t$ for Example 6.5.

ASSESSMENT PROBLEMS

Objective 2—Know and be able to use the equations for voltage, current, power, and energy in a capacitor
6.2 The voltage at the terminals of the $0.6 \mu \mathrm{~F}$ capacitor shown in the figure is 0 for $t<0$ and $40 e^{-15,000 t} \sin 30,000 t \mathrm{~V}$ for $t \geq 0$. Find (a) $i(0)$; (b) the power delivered to the capacitor at $t=\pi / 80 \mathrm{~ms}$; and (c) the energy stored in the capacitor at $t=\pi / 80 \mathrm{~ms}$.
image_name:figure
description:
[
'name': 'c', 'type': 'Capacitor', 'value': '0.6 µF', 'ports': {'Np': 'N1', 'Nn': 'N2'
]
extrainfo:The circuit consists of a single capacitor with a capacitance of 0.6 µF. The voltage across the capacitor is labeled as v, and the current through the capacitor is labeled as i. The positive and negative terminals are marked.


NOTE: Also try Chapter Problems 6.16 and 6.21.

Answer: (a) 0.72 A ;
(b) -649.2 mW ;
(c) $126.13 \mu \mathrm{~J}$.
6.3 The current in the capacitor of Assessment Problem 6.2 is 0 for $t<0$ and $3 \cos 50,000 t \mathrm{~A}$ for $t \geq 0$. Find (a) $v(t)$; (b) the maximum power delivered to the capacitor at any one instant of time; and (c) the maximum energy stored in the capacitor at any one instant of time.

Answer: (a) $100 \sin 50,000 t \mathrm{~V}, t \geq 0$;
(b) 150 W ; (c) 3 mJ .

## 6.3 Series-Parallel Combinations of Inductance and Capacitance

Just as series-parallel combinations of resistors can be reduced to a single equivalent resistor, series-parallel combinations of inductors or capacitors can be reduced to a single inductor or capacitor. Figure 6.13 shows inductors in series. Here, the inductors are forced to carry the same current; thus we define only one current for the series combination. The voltage drops across the individual inductors are

$$
v_{1}=L_{1} \frac{d i}{d t}, \quad v_{2}=L_{2} \frac{d i}{d t}, \quad \text { and } \quad v_{3}=L_{3} \frac{d i}{d t}
$$

The voltage across the series connection is

$$
v=v_{1}+v_{2}+v_{3}=\left(L_{1}+L_{2}+L_{3}\right) \frac{d i}{d t}
$$

from which it should be apparent that the equivalent inductance of seriesconnected inductors is the sum of the individual inductances. For $n$ inductors in series,

$$
\begin{equation*}
L_{\mathrm{eq}}=L_{1}+L_{2}+L_{3}+\cdots+L_{n} \tag{6.19}
\end{equation*}
$$

If the original inductors carry an initial current of $i\left(t_{0}\right)$, the equivalent inductor carries the same initial current. Figure 6.14 shows the equivalent circuit for series inductors carrying an initial current.

Inductors in parallel have the same terminal voltage. In the equivalent circuit, the current in each inductor is a function of the terminal voltage and the initial current in the inductor. For the three inductors in parallel shown in Fig. 6.15, the currents for the individual inductors are

$$
\begin{align*}
i_{1} & =\frac{1}{L_{1}} \int_{t_{0}}^{t} v d \tau+i_{1}\left(t_{0}\right) \\
i_{2} & =\frac{1}{L_{2}} \int_{t_{0}}^{t} v d \tau+i_{2}\left(t_{0}\right) \\
i_{3} & =\frac{1}{L_{3}} \int_{t_{0}}^{t} v d \tau+i_{3}\left(t_{0}\right) \tag{6.20}
\end{align*}
$$

The current at the terminals of the three parallel inductors is the sum of the inductor currents:

$$
\begin{equation*}
i=i_{1}+i_{2}+i_{3} \tag{6.21}
\end{equation*}
$$

Substituting Eq. 6.20 into Eq. 6.21 yields

$$
\begin{equation*}
i=\left(\frac{1}{L_{1}}+\frac{1}{L_{2}}+\frac{1}{L_{3}}\right) \int_{t_{0}}^{t} v d \tau+i_{1}\left(t_{0}\right)+i_{2}\left(t_{0}\right)+i_{3}\left(t_{0}\right) \tag{6.22}
\end{equation*}
$$

image_name:Figure 6.13
description:
[
'name': 'L1', 'type': 'Inductor', 'value': 'L1', 'ports': {'N1': 'N1', 'N2': 'N2'
'name': 'L2', 'type': 'Inductor', 'value': 'L2', 'ports': {'N1': 'N2', 'N2': 'N3'
'name': 'L3', 'type': 'Inductor', 'value': 'L3', 'ports': {'N1': 'N3', 'N2': 'N4'
]
extrainfo:The circuit consists of three inductors L1, L2, and L3 connected in series. The voltage across each inductor is labeled as v1, v2, and v3 respectively, with the total voltage v across the series combination. The current i flows through the series connection.


Figure 6.13 $\triangle$ Inductors in series.

Combining inductors in series

image_name:Figure 6.14
description:
[
'name': 'L1', 'type': 'Inductor', 'value': 'L1', 'ports': {'N1': '+', 'N2': 'N1'
'name': 'L2', 'type': 'Inductor', 'value': 'L2', 'ports': {'N1': 'N1', 'N2': 'N2'
'name': 'L3', 'type': 'Inductor', 'value': 'L3', 'ports': {'N1': 'N2', 'N2': '-'
'name': 'Leq', 'type': 'Inductor', 'value': 'Leq', 'ports': {'N1': '+', 'N2': '-'
]
extrainfo:The circuit shows three inductors L1, L2, and L3 connected in series, with an equivalent inductor Leq representing their series combination. The current i flows through the inductors, and the voltage v is across the series combination. The equivalent inductance Leq is given by the sum Leq = L1 + L2 + L3. The initial current through the inductors is i(t0).


Figure 6.14 $\triangle$ An equivalent circuit for inductors in series carrying an initial current $i\left(t_{0}\right)$.
image_name:Figure 6.14
description:
[
'name': 'v', 'type': 'VoltageSource', 'value': 'Vin', 'ports': {'Np': 'Vin', 'Nn': 'GND'
'name': 'L1', 'type': 'Inductor', 'value': 'L1', 'ports': {'N1': 'Vin', 'N2': 'GND'
'name': 'L2', 'type': 'Inductor', 'value': 'L2', 'ports': {'N1': 'Vin', 'N2': 'GND'
'name': 'L3', 'type': 'Inductor', 'value': 'L3', 'ports': {'N1': 'Vin', 'N2': 'GND'
]
extrainfo:The circuit consists of three inductors L1, L2, and L3 connected in series, each with its initial current i(t0). The equivalent inductance Leq is the sum of L1, L2, and L3. The voltage source Vin provides voltage across the series combination, and the current i flows through the inductors.


Figure 6.15 A Three inductors in parallel.
image_name:Figure 6.16
description:
[
'name': 'Leq', 'type': 'Inductor', 'value': 'Leq', 'ports': {'N1': 'V', 'N2': 'GND'
]
extrainfo:The circuit shows an equivalent inductance Leq for three inductors L1, L2, and L3 in parallel. The equivalent inductance is calculated as 1/Leq = 1/L1 + 1/L2 + 1/L3. The initial current i(t0) is the sum of the initial currents i1(t0), i2(t0), and i3(t0) of the individual inductors. A voltage source V is applied across the inductors, and a current i flows through the circuit.


Figure 6.16 An equivalent circuit for three inductors in parallel.

Combining inductors in parallel

Equivalent inductance initial current

Combining capacitors in series

Equivalent capacitance initial voltage

Combining capacitors in parallel

Now we can interpret Eq. 6.22 in terms of a single inductor; that is,

$$
\begin{equation*}
i=\frac{1}{L_{\mathrm{eq}}} \int_{t_{0}}^{t} v d \tau+i\left(t_{0}\right) \tag{6.23}
\end{equation*}
$$

Comparing Eq. 6.23 with (6.22) yields

$$
\begin{align*}
\frac{1}{L_{\mathrm{eq}}} & =\frac{1}{L_{1}}+\frac{1}{L_{2}}+\frac{1}{L_{3}}  \tag{6.24}\\
i\left(t_{0}\right) & =i_{1}\left(t_{0}\right)+i_{2}\left(t_{0}\right)+i_{3}\left(t_{0}\right) \tag{6.25}
\end{align*}
$$

Figure 6.16 shows the equivalent circuit for the three parallel inductors in Fig. 6.15.

The results expressed in Eqs. 6.24 and 6.25 can be extended to $n$ inductors in parallel:

$$
\begin{align*}
& \frac{1}{L_{\mathrm{eq}}}=\frac{1}{L_{1}}+\frac{1}{L_{2}}+\cdots+\frac{1}{L_{n}}  \tag{6.26}\\
& i\left(t_{0}\right)=i_{1}\left(t_{0}\right)+i_{2}\left(t_{0}\right)+\cdots+i_{n}\left(t_{0}\right) \tag{6.27}
\end{align*}
$$

Capacitors connected in series can be reduced to a single equivalent capacitor. The reciprocal of the equivalent capacitance is equal to the sum of the reciprocals of the individual capacitances. If each capacitor carries its own initial voltage, the initial voltage on the equivalent capacitor is the algebraic sum of the initial voltages on the individual capacitors. Figure 6.17 and the following equations summarize these observations:

$$
\begin{equation*}
\frac{1}{C_{\mathrm{eq}}}=\frac{1}{C_{1}}+\frac{1}{C_{2}}+\cdots+\frac{1}{C_{n}} \tag{6.28}
\end{equation*}
$$

$$
\begin{equation*}
v\left(t_{0}\right)=v_{1}\left(t_{0}\right)+v_{2}\left(t_{0}\right)+\cdots+v_{n}\left(t_{0}\right) \tag{6.29}
\end{equation*}
$$

We leave the derivation of the equivalent circuit for series-connected capacitors as an exercise. (See Problem 6.32.)

The equivalent capacitance of capacitors connected in parallel is simply the sum of the capacitances of the individual capacitors, as Fig. 6.18 and the following equation show:

$$
\begin{equation*}
C_{\mathrm{eq}}=C_{1}+C_{2}+\cdots+C_{n} \tag{6.30}
\end{equation*}
$$

Capacitors connected in parallel must carry the same voltage. Therefore, if there is an initial voltage across the original parallel capacitors, this same initial voltage appears across the equivalent capacitance $C_{\text {eq }}$. The derivation of the equivalent circuit for parallel capacitors is left as an exercise. (See Problem 6.33.)

We say more about series-parallel equivalent circuits of inductors and capacitors in Chapter 7, where we interpret results based on their use.
image_name:(a)
description:
[
'name': 'C1', 'type': 'Capacitor', 'value': 'C1', 'ports': {'Np': 'V', 'Nn': 'a'
'name': 'C2', 'type': 'Capacitor', 'value': 'C2', 'ports': {'Np': 'a', 'Nn': 'b'
'name': 'Cn', 'type': 'Capacitor', 'value': 'Cn', 'ports': {'Np': 'c', 'Nn': 'GND'
]
extrainfo:The circuit diagram (a) shows capacitors C1, C2, ..., Cn connected in series between a voltage source V and ground. The voltage across each capacitor is indicated as v1(t0), v2(t0), ..., vn(t0). The current i flows from the voltage source through the capacitors to ground.
image_name:(b)
description:
[
'name': 'Ceq', 'type': 'Capacitor', 'value': 'Ceq', 'ports': {'Np': 'V', 'Nn': 'GND'
]
extrainfo:Figure 6.18(b) shows an equivalent circuit for capacitors connected in series, represented by a single equivalent capacitor Ceq. The voltage across Ceq is the sum of individual voltages across the series capacitors, and the equivalent capacitance is determined by the reciprocal of the sum of the reciprocals of the individual capacitances. The current i flows from the positive terminal to the negative terminal, and the voltage v(t0) is the initial voltage across Ceq.


Figure 6.17 $\triangle$ An equivalent circuit for capacitors connected in series. (a) The series capacitors. (b) The equivalent circuit.
image_name:(a)
description:
[
'name': 'C1', 'type': 'Capacitor', 'value': 'C1', 'ports': {'Np': 'V', 'Nn': 'GND'
'name': 'C2', 'type': 'Capacitor', 'value': 'C2', 'ports': {'Np': 'V', 'Nn': 'GND'
'name': 'Cn', 'type': 'Capacitor', 'value': 'Cn', 'ports': {'Np': 'V', 'Nn': 'GND'
]
extrainfo:The circuit diagram (a) shows capacitors C1, C2, ..., Cn connected in parallel between a voltage source V and ground. The current i flows from the positive terminal of the voltage source to the capacitors.
image_name:(b)
description:
[
'name': 'Ceq', 'type': 'Capacitor', 'value': 'Ceq', 'ports': {'Np': 'V', 'Nn': 'GND'
]
extrainfo:The circuit diagram (b) shows an equivalent circuit of capacitors connected in parallel, represented by a single equivalent capacitor Ceq. The equivalent capacitance is the sum of the individual capacitances: Ceq = C1 + C2 + ... + Cn. The current i flows from the positive terminal to the negative terminal, and the voltage v is across the equivalent capacitor Ceq.


Figure 6.18 $\triangle$ An equivalent circuit for capacitors connected in parallel. (a) Capacitors in parallel. (b) The equivalent circuit.

ASSESSMENT PROBLEMS

Objective 3-Be able to combine inductors or capacitors in series and in parallel to form a single equivalent inductor
6.4 The initial values of $i_{1}$ and $i_{2}$ in the circuit shown are +3 A and -5 A , respectively. The voltage at the terminals of the parallel inductors for $t \geq 0$ is $-30 e^{-5 t} \mathrm{mV}$.
a) If the parallel inductors are replaced by a single inductor, what is its inductance?
b) What is the initial current and its reference direction in the equivalent inductor?
c) Use the equivalent inductor to find $i(t)$.
d) Find $i_{1}(t)$ and $i_{2}(t)$. Verify that the solutions for $i_{1}(t), i_{2}(t)$, and $i(t)$ satisfy Kirchhoff's current law.
image_name:circuit schematic
description:
[
'name': 'V', 'type': 'VoltageSource', 'value': 'V', 'ports': {'Np': 'V', 'Nn': 'GND'
'name': 'L1', 'type': 'Inductor', 'value': '60 mH', 'ports': {'N1': 'V', 'N2': 'GND'
'name': 'L2', 'type': 'Inductor', 'value': '240 mH', 'ports': {'N1': 'V', 'N2': 'GND'
]
extrainfo:The circuit contains a voltage source and two inductors in parallel. The voltage across the inductors for t ≥ 0 is given by v(t) = -30e^{-5t} mV. The initial currents through the inductors are i_1(t) and i_2(t), and the total current is i(t).


NOTE: Also try Chapter Problems 6.22, 6.24, 6.27, and 6.31.

Answer: (a) 48 mH ;
(b) 2 A, up;
(c) $0.125 e^{-5 t}-2.125 \mathrm{~A}, t \geq 0$;
(d) $i_{1}(t)=0.1 e^{-5 t}+2.9 \mathrm{~A}, t \geq 0$,

$$
i_{2}(t)=0.025 e^{-5 t}-5.025 \mathrm{~A}, t \geq 0
$$

6.5 The current at the terminals of the two capacitors shown is $240 e^{-10 t} \mu \mathrm{~A}$ for $t \geq 0$. The initial values of $v_{1}$ and $v_{2}$ are -10 V and -5 V , respectively. Calculate the total energy trapped in the capacitors as $t \rightarrow \infty$. (Hint: Don't combine the capacitors in series-find the energy trapped in each, and then add.)
image_name:Figure
description:
[
'name': 'C1', 'type': 'Capacitor', 'value': '2 µF', 'ports': {'Np': 'Vi', 'Nn': 'V2'
'name': 'C2', 'type': 'Capacitor', 'value': '8 µF', 'ports': {'Np': 'V2', 'Nn': 'GND'
]
extrainfo:The circuit contains two capacitors connected in series between the input voltage Vi and ground. The initial voltages across the capacitors are v1 = -10 V and v2 = -5 V. The current through the circuit is given by i(t) = 240 e^{-10t} µA for t >= 0.


Answer: $20 \mu \mathrm{~J}$.
image_name:Figure 6.19
description:
[
'name': 'Vg', 'type': 'VoltageSource', 'value': 'Vg', 'ports': {'Np': 'Vg', 'Nn': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'Vg', 'N2': 'X1'
'name': 'L1', 'type': 'Inductor', 'value': 'L1', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'X2', 'N2': 'GND'
'name': 'L2', 'type': 'Inductor', 'value': 'L2', 'ports': {'N1': 'X2', 'N2': 'GND'
]
extrainfo:The circuit consists of two magnetically coupled coils, L1 and L2, with mutual inductance M. The circuit is driven by a voltage source Vg, and each coil is connected in series with a resistor, R1 and R2, respectively.


Figure 6.19 ■ Two magnetically coupled coils.
image_name:Figure 6.20
description:
[
'name': 'vg', 'type': 'VoltageSource', 'value': 'vg', 'ports': {'Np': 'vg', 'Nn': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'vg', 'N2': 'X1'
'name': 'L1', 'type': 'Inductor', 'value': 'L1', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': 'L2', 'type': 'Inductor', 'value': 'L2', 'ports': {'N1': 'X2', 'N2': 'GND'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'X2', 'N2': 'GND'
'name': 'M', 'type': 'Transformer', 'ports': {'In1': 'X1', 'In2': 'GND', 'Out1': 'X2', 'Oou2': 'GND'
]
extrainfo:The circuit consists of two magnetically coupled coils, L1 and L2, with mutual inductance M. The circuit is driven by a voltage source Vg, and each coil is connected in series with a resistor, R1 and R2, respectively. The currents i1 and i2 flow through L1 and L2, indicating the direction of the current flow.


Figure 6.20 $\triangle$ Coil currents $i_{1}$ and $i_{2}$ used to describe the circuit shown in Fig. 6.19.
image_name:Figure 6.21
description:
[
'name': 'vg', 'type': 'VoltageSource', 'value': 'vg', 'ports': {'Np': 'vg', 'Nn': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'vg', 'N2': 'X1'
'name': 'L1', 'type': 'Inductor', 'value': 'L1', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': 'L2', 'type': 'Inductor', 'value': 'L2', 'ports': {'N1': 'X2', 'N2': 'GND'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'X2', 'N2': 'GND'
'name': 'T1', 'type': 'Transformer', 'ports': {'In1': 'X1', 'In2': 'GND', 'Out1': 'X2', 'Oou2': 'GND'
]
extrainfo:The circuit consists of two magnetically coupled coils, L1 and L2, with mutual inductance M. The circuit is driven by a voltage source Vg, and each coil is connected in series with a resistor, R1 and R2, respectively. The currents i1 and i2 flow through L1 and L2, indicating the direction of the current flow.


Figure $6.21 \triangle$ The circuit of Fig. 6.20 with dots added to the coils indicating the polarity of the mutually induced voltages.

Dot convention for mutually coupled coils

Dot convention for mutually coupled coils (alternate)
known as mutual inductance. The circuit shown in Fig. 6.19 represents two magnetically coupled coils. The self-inductances of the two coils are labeled $L_{1}$ and $L_{2}$, and the mutual inductance is labeled $M$. The doubleheaded arrow adjacent to $M$ indicates the pair of coils with this value of mutual inductance. This notation is needed particularly in circuits containing more than one pair of magnetically coupled coils.

The easiest way to analyze circuits containing mutual inductance is to use mesh currents. The problem is to write the circuit equations that describe the circuit in terms of the coil currents. First, choose the reference direction for each coil current. Figure 6.20 shows arbitrarily selected reference currents. After choosing the reference directions for $i_{1}$ and $i_{2}$, sum the voltages around each closed path. Because of the mutual inductance $M$, there will be two voltages across each coil, namely, a self-induced voltage and a mutually induced voltage. The selfinduced voltage is the product of the self-inductance of the coil and the first derivative of the current in that coil. The mutually induced voltage is the product of the mutual inductance of the coils and the first derivative of the current in the other coil. Consider the coil on the left in Fig. 6.20 whose self-inductance has the value $L_{1}$. The self-induced voltage across this coil is $L_{1}\left(d i_{1} / d t\right)$ and the mutually induced voltage across this coil is $M\left(d i_{2} / d t\right)$. But what about the polarities of these two voltages?

Using the passive sign convention, the self-induced voltage is a voltage drop in the direction of the current producing the voltage. But the polarity of the mutually induced voltage depends on the way the coils are wound in relation to the reference direction of coil currents. In general, showing the details of mutually coupled windings is very cumbersome. Instead, we keep track of the polarities by a method known as the dot convention, in which a dot is placed on one terminal of each winding, as shown in Fig. 6.21. These dots carry the sign information and allow us to draw the coils schematically rather than showing how they wrap around a core structure.

The rule for using the dot convention to determine the polarity of mutually induced voltage can be summarized as follows:

When the reference direction for a current enters the dotted terminal of a coil, the reference polarity of the voltage that it induces in the other coil is positive at its dotted terminal.
Or, stated alternatively,

When the reference direction for a current leaves the dotted terminal of a coil, the reference polarity of the voltage that it induces in the other coil is negative at its dotted terminal.

For the most part, dot markings will be provided for you in the circuit diagrams in this text. The important skill is to be able to write the appropriate circuit equations given your understanding of mutual inductance and the dot convention. Figuring out where to place the polarity dots if they are not given may be possible by examining the physical configuration of an actual circuit or by testing it in the laboratory. We will discuss these procedures after we discuss the use of dot markings.

In Fig. 6.21, the dot convention rule indicates that the reference polarity for the voltage induced in coil 1 by the current $i_{2}$ is negative at the dotted terminal of coil 1 . This voltage $\left(M d i_{2} / d t\right)$ is a voltage rise with respect to $i_{1}$. The voltage induced in coil 2 by the current $i_{1}$ is $M d i_{1} / d t$, and its reference polarity is positive at the dotted terminal of coil 2 . This voltage is a voltage rise in the direction of $i_{2}$. Figure 6.22 shows the self- and mutually induced voltages across coils 1 and 2 along with their polarity marks.
image_name:Figure 6.22
description:
[
'name': 'vg', 'type': 'VoltageSource', 'value': 'vg', 'ports': {'Np': 'vg', 'Nn': 'GND'
'name': 'R1', 'type': 'Resistor', 'value': 'R1', 'ports': {'N1': 'vg', 'N2': 'X1'
'name': 'L1', 'type': 'Inductor', 'value': 'L1', 'ports': {'N1': 'X1', 'N2': 'GND'
'name': 'L2', 'type': 'Inductor', 'value': 'L2', 'ports': {'N1': 'X2', 'N2': 'GND'
'name': 'R2', 'type': 'Resistor', 'value': 'R2', 'ports': {'N1': 'X2', 'N2': 'GND'
]
extrainfo:The circuit consists of two coupled inductors L1 and L2 with mutual inductance M. The dots indicate the polarity of the induced voltages. The voltage source vg drives the current i1 through R1 and L1, inducing a voltage in L2. Similarly, current i2 through R2 and L2 induces a voltage in L1.


Figure $6.22 \triangle$ The self- and mutually induced voltages appearing across the coils shown in Fig. 6.21.

Now let's look at the sum of the voltages around each closed loop. In Eqs. 6.31 and 6.32 , voltage rises in the reference direction of a current are negative:

$$
\begin{array}{r}
-v_{g}+i_{1} R_{1}+L_{1} \frac{d i_{1}}{d t}-M \frac{d i_{2}}{d t}=0 \\
i_{2} R_{2}+L_{2} \frac{d i_{2}}{d t}-M \frac{d i_{1}}{d t}=0 \tag{6.32}
\end{array}
$$

The Procedure for Determining Dot Markings

We shift now to two methods of determining dot markings. The first assumes that we know the physical arrangement of the two coils and the mode of each winding in a magnetically coupled circuit. The following six steps, applied here to Fig. 6.23, determine a set of dot markings:
a) Arbitrarily select one terminal-say, the D terminal-of one coil and mark it with a dot.
b) Assign a current into the dotted terminal and label it $i_{\mathrm{D}}$.
c) Use the right-hand rule ${ }^{1}$ to determine the direction of the magnetic field established by $i_{\mathrm{D}}$ inside the coupled coils and label this field $\phi_{\mathrm{D}}$.
d) Arbitrarily pick one terminal of the second coil-say, terminal A-and assign a current into this terminal, showing the current as $i_{\mathrm{A}}$.
e) Use the right-hand rule to determine the direction of the flux established by $i_{\mathrm{A}}$ inside the coupled coils and label this flux $\phi_{\mathrm{A}}$.
f) Compare the directions of the two fluxes $\phi_{\mathrm{D}}$ and $\phi_{\mathrm{A}}$. If the fluxes have the same reference direction, place a dot on the terminal of the second coil where the test current $\left(i_{\mathrm{A}}\right)$ enters. (In Fig. 6.23, the fluxes $\phi_{\mathrm{D}}$ and $\phi_{\mathrm{A}}$ have the same reference direction, and therefore a dot goes on terminal A.) If the fluxes have different reference directions, place a dot on the terminal of the second coil where the test current leaves.

The relative polarities of magnetically coupled coils can also be determined experimentally. This capability is important because in some situations, determining how the coils are wound on the core is impossible. One experimental method is to connect a dc voltage source, a resistor, a switch, and a dc voltmeter to the pair of coils, as shown in Fig. 6.24. The shaded box covering the coils implies that physical inspection of the coils is not possible. The resistor $R$ limits the magnitude of the current supplied by the dc voltage source.

The coil terminal connected to the positive terminal of the dc source via the switch and limiting resistor receives a polarity mark, as shown in Fig. 6.24. When the switch is closed, the voltmeter deflection is observed. If the momentary deflection is upscale, the coil terminal connected to the positive terminal of the voltmeter receives the polarity mark. If the
image_name:Figure 6.23
description:The image in Figure 6.23 shows a toroidal coil with several labeled components and steps for determining polarity markings. The coil is depicted as a circular, donut-shaped object with copper wire wrapped around it. There are four terminals labeled A, B, C, and D, each connected to the coil at different points.

1. **Identification of Components and Structure:**
- **Toroidal Coil:** The central component is a toroidal coil, which is a circular core around which the wire is wound.
- **Wire Windings:** Copper wire is wrapped around the toroid, creating multiple loops that are used to generate magnetic fields when current flows through them.
- **Terminals:** The coil has four terminals labeled A, B, C, and D, positioned at intervals around the coil.

2. **Connections and Interactions:**
- **Current Flow:** The current flow is indicated by arrows labeled with current symbols (i_A and i_D) at terminals A and D, respectively. This shows the direction of current through the windings.
- **Magnetic Flux:** Arrows inside the coil labeled Φ_A and Φ_D indicate the direction of magnetic flux generated by the current flowing through the coil.

3. **Labels, Annotations, and Key Features:**
- **Steps for Polarity Marking:** The diagram includes numbered steps (Step 1 to Step 5) to guide the process of determining polarity markings on the coil.
- **Polarity Dots:** Dots near terminals A and D indicate the polarity marking points, showing where the dots are applied based on the current direction and magnetic flux.
- **Annotations:** Annotations such as "Arbitrarily dotted terminal (Step 1)" provide guidance on how to start the process of marking the coil.

Overall, the diagram provides a visual method for understanding how to determine the polarity of the coil terminals using current direction and magnetic flux, with step-by-step instructions annotated on the image.


Figure 6.23 $\Delta \mathrm{A}$ set of coils showing a method for determining a set of dot markings.
image_name:Figure 6.24
description:
[
'name': 'VBB', 'type': 'VoltageSource', 'value': 'VBB', 'ports': {'Np': 'VBB', 'Nn': 'GND'
'name': 'R', 'type': 'Resistor', 'value': 'R', 'ports': {'N1': 'VBB', 'N2': 'SW1'
'name': 'SW1', 'type': 'Switch', 'ports': {'N1': 'SW1', 'N2': 'SW2'
'name': 'L1', 'type': 'Inductor', 'value':'L1','ports': {'N1': 'SW2', 'N2': 'GND'
'name': 'L2', 'type': 'Inductor', 'value':'L2', 'ports': {'N1': 'X1', 'N2': 'GND'
]
extrainfo:The circuit includes a voltage source VBB connected to a resistor R and two switches SW1 and SW2 in series, ending at ground. A dc voltmeter is connected across the node X1 and ground.


Figure 6.24 An experimental setup for determining polarity marks.

[^1]deflection is downscale, the coil terminal connected to the negative terminal of the voltmeter receives the polarity mark.

Example 6.6 shows how to use the dot markings to formulate a set of circuit equations in a circuit containing magnetically coupled coils.

#### Example 6.6 Finding Mesh-Current Equations for a Circuit with Magnetically Coupled Coils

a) Write a set of mesh-current equations that describe the circuit in Fig. 6.25 in terms of the currents $i_{1}$ and $i_{2}$.
b) Verify that if there is no energy stored in the circuit at $t=0$ and if $i_{\mathrm{g}}=16-16 e^{-5 t} \mathrm{~A}$, the solutions for $i_{1}$ and $i_{2}$ are

$$
\begin{aligned}
& i_{1}=4+64 e^{-5 t}-68 e^{-4 t} \mathrm{~A} \\
& i_{2}=1-52 e^{-5 t}+51 e^{-4 t} \mathrm{~A}
\end{aligned}
$$

image_name:Figure 6.25
description:
[
'name': 'ig', 'type': 'CurrentSource', 'value': 'ig', 'ports': {'Np': 'GND', 'Nn': 'X1'
'name': '5 Ω', 'type': 'Resistor', 'value': '5 Ω', 'ports': {'N1': 'X1', 'N2': 'X2'
'name': '20 Ω', 'type': 'Resistor', 'value': '20 Ω', 'ports': {'N1': 'X2', 'N2': 'X3'
'name': '60 Ω', 'type': 'Resistor', 'value': '60 Ω', 'ports': {'N1': 'X3', 'N2': 'GND'
'name': '4 H', 'type': 'Inductor', 'value': '4 H', 'ports': {'N1': 'X1', 'N2': 'X3'
'name': '16 H', 'type': 'Inductor', 'value': '16 H', 'ports': {'N1': 'X2', 'N2': 'GND'
]
extrainfo:The circuit includes two mesh currents, i1 and i2. The mesh equations account for the resistors, inductors, and the current source ig. The inductors are magnetically coupled, affecting the mesh current equations.


Figure 6.25 $\Delta$ The circuit for Example 6.6.

#### Solution

a) Summing the voltages around the $i_{1}$ mesh yields
$4 \frac{d i_{1}}{d t}+8 \frac{d}{d t}\left(i_{g}-i_{2}\right)+20\left(i_{1}-i_{2}\right)+5\left(i_{1}-i_{g}\right)=0$.

The $i_{2}$ mesh equation is

$$
20\left(i_{2}-i_{1}\right)+60 i_{2}+16 \frac{d}{d t}\left(i_{2}-i_{g}\right)-8 \frac{d i_{1}}{d t}=0
$$

Note that the voltage across the 4 H coil due to the current $\left(i_{g}-i_{2}\right)$, that is, $8 d\left(i_{g}-i_{2}\right) / d t$, is a voltage drop in the direction of $i_{1}$. The voltage induced in the 16 H coil by the current $i_{1}$, that is, $8 d i_{1} / d t$, is a voltage rise in the direction of $i_{2}$.
b) To check the validity of $i_{1}$ and $i_{2}$, we begin by testing the initial and final values of $i_{1}$ and $i_{2}$. We know by hypothesis that $i_{1}(0)=i_{2}(0)=0$. From the given solutions we have

$$
\begin{aligned}
& i_{1}(0)=4+64-68=0 \\
& i_{2}(0)=1-52+51=0
\end{aligned}
$$

Now we observe that as $t$ approaches infinity the source current $\left(i_{g}\right)$ approaches a constant value of 16 A , and therefore the magnetically coupled coils behave as short circuits. Hence at $t=\infty$ the circuit reduces to that shown in Fig. 6.26. From Fig. 6.26 we see that at $t=\infty$ the three resistors are in parallel across the 16 A source. The equivalent resistance is $3.75 \Omega$ and thus the voltage across the 16 A current source is 60 V . It follows that

$$
\begin{aligned}
& i_{1}(\infty)=\frac{60}{20}+\frac{60}{60}=4 \mathrm{~A} \\
& i_{2}(\infty)=\frac{60}{60}=1 \mathrm{~A}
\end{aligned}
$$

These values agree with the final values predicted by the solutions for $i_{1}$ and $i_{2}$.

Finally we check the solutions by seeing if they satisfy the differential equations derived in (a). We will leave this final check to the reader via Problem 6.37.
image_name:Figure 6.26 Δ
description:
[
'name': 'I1', 'type': 'CurrentSource', 'value': '16A', 'ports': {'Np': 'GND', 'Nn': 'A'
'name': 'R1', 'type': 'Resistor', 'value': '5Ω', 'ports': {'N1': 'A', 'N2': 'GND'
'name': 'R2', 'type': 'Resistor', 'value': '20Ω', 'ports': {'N1': 'GND', 'N2': 'A'
'name': 'R3', 'type': 'Resistor', 'value': '60Ω', 'ports': {'N1': 'A', 'N2': 'GND'
]
extrainfo:This circuit contains a current source of 16A and three resistors (5Ω, 20Ω, and 60Ω) connected in a loop. The current i1 flows through the 5Ω and 20Ω resistors, while i2 flows through the 60Ω resistor.


Figure $6.26 \Delta$ The circuit of Example 6.6 when $t=\infty$.

ASSESSMENT PROBLEM

Objective 4-Use the dot convention to write mesh-current equations for mutually coupled coils

6.6 a) Write a set of mesh-current equations for the circuit in Example 6.6 if the dot on the 4 H inductor is at the right-hand terminal, the reference direction of $i_{g}$ is reversed, and the $60 \Omega$ resistor is increased to $780 \Omega$.
b) Verify that if there is no energy stored in the circuit at $t=0$, and if $i_{g}=1.96-1.96 e^{-4 t} \mathrm{~A}$, the solutions to the differential equations derived in (a) of this Assessment Problem are

$$
\begin{aligned}
& i_{1}=-0.4-11.6 e^{-4 t}+12 e^{-5 t} \mathrm{~A} \\
& i_{2}=-0.01-0.99 e^{-4 t}+e^{-5 t} \mathrm{~A}
\end{aligned}
$$

NOTE: Also try Chapter Problem 6.39.

Answer: (a) $4\left(d i_{1} / d t\right)+25 i_{1}+8\left(d i_{2} / d t\right)-20 i_{2}$ $=-5 i_{g}-8\left(d i_{g} / d t\right)$ and
$8\left(d i_{1} / d t\right)-20 i_{1}+16\left(d i_{2} / d t\right)+800 i_{2}$
$=-16\left(d i_{g} / d t\right)$;
(b) verification.

## 6.5 A Closer Look at Mutual Inductance

In order to fully explain the circuit parameter mutual inductance, and to examine the limitations and assumptions made in the qualitative discussion presented in Section 6.4, we begin with a more quantitative description of self-inductance than was previously provided.

A Review of Self-Inductance

The concept of inductance can be traced to Michael Faraday, who did pioneering work in this area in the early 1800s. Faraday postulated that a magnetic field consists of lines of force surrounding the current-carrying conductor. Visualize these lines of force as energy-storing elastic bands that close on themselves. As the current increases and decreases, the elastic bands (that is, the lines of force) spread and collapse about the conductor. The voltage induced in the conductor is proportional to the number of lines that collapse into, or cut, the conductor. This image of induced voltage is expressed by what is called Faraday's law; that is,

$$
\begin{equation*}
v=\frac{d \lambda}{d t} \tag{6.33}
\end{equation*}
$$

where $\lambda$ is referred to as the flux linkage and is measured in weber-turns.
How do we get from Faraday's law to the definition of inductance presented in Section 6.1? We can begin to draw this connection using Fig. 6.27 as a reference.

The lines threading the $N$ turns and labeled $\phi$ represent the magnetic lines of force that make up the magnetic field. The strength of the magnetic field depends on the strength of the current, and the spatial orientation of the field depends on the direction of the current. The right-hand rule relates the orientation of the field to the direction of the current: When the fingers of the right hand are wrapped around the coil so that the fingers point in the direction of the current, the thumb points in the direction of that portion of the magnetic field inside the coil. The flux linkage is the product of the magnetic field $(\phi)$, measured in webers $(\mathrm{Wb})$, and the number of turns linked by the field $(N)$ :

$$
\begin{equation*}
\lambda=N \phi \tag{6.34}
\end{equation*}
$$

The magnitude of the flux, $\phi$, is related to the magnitude of the coil current by the relationship

$$
\begin{equation*}
\phi=\mathscr{P} N i \tag{6.35}
\end{equation*}
$$

where $N$ is the number of turns on the coil, and $\mathscr{P}$ is the permeance of the space occupied by the flux. Permeance is a quantity that describes the magnetic properties of this space, and as such, a detailed discussion of permeance is outside the scope of this text. Here, we need only observe that, when the space containing the flux is made up of magnetic materials (such as iron, nickel, and cobalt), the permeance varies with the flux, giving a nonlinear relationship between $\phi$ and $i$. But when the space containing the flux is comprised of nonmagnetic materials, the permeance is constant, giving a linear relationship between $\phi$ and $i$. Note from Eq. 6.35 that the flux is also proportional to the number of turns on the coil.

Here, we assume that the core material-the space containing the fluxis nonmagnetic. Then, substituting Eqs. 6.34 and 6.35 into Eq. 6.33 yields

$$
\begin{align*}
v & =\frac{d \lambda}{d t}=\frac{d(N \phi)}{d t} \\
& =N \frac{d \phi}{d t}=N \frac{d}{d t}(\mathscr{P} N i) \\
& =N^{2} \mathscr{P} \frac{d i}{d t}=L \frac{d i}{d t} \tag{6.36}
\end{align*}
$$

which shows that self-inductance is proportional to the square of the number of turns on the coil. We make use of this observation later.

The polarity of the induced voltage in the circuit in Fig. 6.27 reflects the reaction of the field to the current creating the field. For example, when $i$ is increasing, $d i / d t$ is positive and $v$ is positive. Thus energy is required to establish the magnetic field. The product $v i$ gives the rate at which energy is stored in the field. When the field collapses, $d i / d t$ is negative, and again the polarity of the induced voltage is in opposition to the change. As the field collapses about the coil, energy is returned to the circuit.

Keeping in mind this further insight into the concept of self-inductance, we now turn back to mutual inductance.
image_name:Figure 6.28
description:The circuit consists of two magnetically coupled coils with a current source is driving the primary coil N1. The secondary coil N2 is open and not energized. Mutual inductance effects are represented by the flux lines phi11 and phi21.


Figure $6.28 \triangle$ Two magnetically coupled coils.

The Concept of Mutual Inductance

Figure 6.28 shows two magnetically coupled coils. You should verify that the dot markings on the two coils agree with the direction of the coil windings and currents shown. The number of turns on each coil are $N_{1}$ and $N_{2}$, respectively. Coil 1 is energized by a time-varying current source that establishes the current $i_{1}$ in the $N_{1}$ turns. Coil 2 is not energized and is open. The coils are wound on a nonmagnetic core. The flux produced by the current $i_{1}$ can be divided into two components, labeled $\phi_{11}$ and $\phi_{21}$. The flux component $\phi_{11}$ is the flux produced by $i_{1}$ that links only the $N_{1}$ turns. The component $\phi_{21}$ is the flux produced by $i_{1}$ that links the $N_{2}$ turns and the $N_{1}$ turns. The first digit in the subscript to the flux gives the coil number, and the second digit refers to the coil current. Thus $\phi_{11}$ is a flux linking coil 1 and produced by a current in coil 1 , whereas $\phi_{21}$ is a flux linking coil 2 and produced by a current in coil 1.

The total flux linking coil 1 is $\phi_{1}$, the sum of $\phi_{11}$ and $\phi_{21}$ :

$$
\begin{equation*}
\phi_{1}=\phi_{11}+\phi_{21} \tag{6.37}
\end{equation*}
$$

The flux $\phi_{1}$ and its components $\phi_{11}$ and $\phi_{21}$ are related to the coil current $i_{1}$ as follows:

$$
\begin{align*}
\phi_{1} & =\mathscr{P}_{1} N_{1} i_{1},  \tag{6.38}\\
\phi_{11} & =\mathscr{P}_{11} N_{1} i_{1}  \tag{6.39}\\
\phi_{21} & =\mathscr{P}_{21} N_{1} i_{1} \tag{6.40}
\end{align*}
$$

where $\mathscr{P}_{1}$ is the permeance of the space occupied by the flux $\phi_{1}, \mathscr{P}_{11}$ is the permeance of the space occupied by the flux $\phi_{11}$, and $\mathscr{P}_{21}$ is the permeance of the space occupied by the flux $\phi_{21}$. Substituting Eqs. 6.38, 6.39, and 6.40 into Eq. 6.37 yields the relationship between the permeance of the space occupied by the total flux $\phi_{1}$ and the permeances of the spaces occupied by its components $\phi_{11}$ and $\phi_{21}$ :

$$
\begin{equation*}
\mathscr{P}_{1}=\mathscr{P}_{11}+\mathscr{P}_{21} \tag{6.41}
\end{equation*}
$$

We use Faraday's law to derive expressions for $v_{1}$ and $v_{2}$ :

$$
\begin{align*}
v_{1} & =\frac{d \lambda_{1}}{d t}=\frac{d\left(N_{1} \phi_{1}\right)}{d t}=N_{1} \frac{d}{d t}\left(\phi_{11}+\phi_{21}\right) \\
& =N_{1}^{2}\left(\mathscr{P}_{11}+\mathscr{P}_{21}\right) \frac{d i_{1}}{d t}=N_{1}^{2} \mathscr{P}_{1} \frac{d i_{1}}{d t}=L_{1} \frac{d i_{1}}{d t} \tag{6.42}
\end{align*}
$$

and

$$
\begin{align*}
v_{2} & =\frac{d \lambda_{2}}{d t}=\frac{d\left(N_{2} \phi_{21}\right)}{d t}=N_{2} \frac{d}{d t}\left(\mathscr{P}_{21} N_{1} i_{1}\right) \\
& =N_{2} N_{1} \mathscr{P}_{21} \frac{d i_{1}}{d t} \tag{6.43}
\end{align*}
$$

The coefficient of $d i_{1} / d t$ in Eq. 6.42 is the self-inductance of coil 1. The coefficient of $d i_{1} / d t$ in Eq. 6.43 is the mutual inductance between coils 1 and 2. Thus

$$
\begin{equation*}
M_{21}=N_{2} N_{1} \mathscr{P}_{21} \tag{6.44}
\end{equation*}
$$

The subscript on $M$ specifies an inductance that relates the voltage induced in coil 2 to the current in coil 1.

The coefficient of mutual inductance gives

$$
\begin{equation*}
v_{2}=M_{21} \frac{d i_{1}}{d t} \tag{6.45}
\end{equation*}
$$

Note that the dot convention is used to assign the polarity reference to $v_{2}$ in Fig. 6.28.

For the coupled coils in Fig. 6.28, exciting coil 2 from a time-varying current source $\left(i_{2}\right)$ and leaving coil 1 open produces the circuit arrangement
image_name:Figure 6.29
description:The circuit shows magnetically coupled coils with coil 2 excited by a current source, while coil 1 is open. The dot convention indicates the polarity of the induced voltages. The flux linkage equations are provided for mutual and self-inductance.


Figure 6.29 A The magnetically coupled coils of Fig. 6.28, with coil 2 excited and coil 1 open.
shown in Fig. 6.29. Again, the polarity reference assigned to $v_{1}$ is based on the dot convention.

The total flux linking coil 2 is

$$
\begin{equation*}
\phi_{2}=\phi_{22}+\phi_{12} \tag{6.46}
\end{equation*}
$$

The flux $\phi_{2}$ and its components $\phi_{22}$ and $\phi_{12}$ are related to the coil current $i_{2}$ as follows:

$$
\begin{align*}
& \phi_{2}=\mathscr{P}_{2} N_{2} i_{2},  \tag{6.47}\\
& \phi_{22}=\mathscr{P}_{22} N_{2} i_{2},  \tag{6.48}\\
& \phi_{12}=\mathscr{P}_{12} N_{2} i_{2} \tag{6.49}
\end{align*}
$$

The voltages $v_{2}$ and $v_{1}$ are

$$
\begin{gather*}
v_{2}=\frac{d \lambda_{2}}{d t}=N_{2}^{2} \mathscr{P}_{2} \frac{d i_{2}}{d t}=L_{2} \frac{d i_{2}}{d t}  \tag{6.50}\\
v_{1}=\frac{d \lambda_{1}}{d t}=\frac{d}{d t}\left(N_{1} \phi_{12}\right)=N_{1} N_{2} \mathscr{P}_{12} \frac{d i_{2}}{d t} . \tag{6.51}
\end{gather*}
$$

The coefficient of mutual inductance that relates the voltage induced in coil 1 to the time-varying current in coil 2 is the coefficient of $d i_{2} / d t$ in Eq. 6.51:

$$
\begin{equation*}
M_{12}=N_{1} N_{2} \mathscr{P}_{12} \tag{6.52}
\end{equation*}
$$

For nonmagnetic materials, the permeances $\mathscr{P}_{12}$ and $\mathscr{P}_{21}$ are equal, and therefore

$$
\begin{equation*}
M_{12}=M_{21}=M \tag{6.53}
\end{equation*}
$$

Hence for linear circuits with just two magnetically coupled coils, attaching subscripts to the coefficient of mutual inductance is not necessary.

Mutual Inductance in Terms of Self-Inductance

The value of mutual inductance is a function of the self-inductances. We derive this relationship as follows. From Eqs. 6.42 and 6.50,

$$
\begin{align*}
& L_{1}=N_{1}^{2} \mathscr{P}_{1}  \tag{6.54}\\
& L_{2}=N_{2}^{2} \mathscr{P}_{2} \tag{6.55}
\end{align*}
$$

respectively. From Eqs. 6.54 and 6.55,

$$
\begin{equation*}
L_{1} L_{2}=N_{1}^{2} N_{2}^{2} \mathscr{P}_{1} \mathscr{P}_{2} \tag{6.56}
\end{equation*}
$$

We now use Eq. 6.41 and the corresponding expression for $\mathscr{P}_{2}$ to write

$$
\begin{equation*}
L_{1} L_{2}=N_{1}^{2} N_{2}^{2}\left(\mathscr{P}_{11}+\mathscr{P}_{21}\right)\left(\mathscr{P}_{22}+\mathscr{P}_{12}\right) \tag{6.57}
\end{equation*}
$$

But for a linear system, $\mathscr{P}_{21}=\mathscr{P}_{12}$, so Eq. 6.57 becomes

$$
\begin{align*}
L_{1} L_{2} & =\left(N_{1} N_{2} \mathscr{P}_{12}\right)^{2}\left(1+\frac{\mathscr{P}_{11}}{\mathscr{P}_{12}}\right)\left(1+\frac{\mathscr{P}_{22}}{\mathscr{P}_{12}}\right) \\
& =M^{2}\left(1+\frac{\mathscr{P}_{11}}{\mathscr{P}_{12}}\right)\left(1+\frac{\mathscr{P}_{22}}{\mathscr{P}_{12}}\right) \tag{6.58}
\end{align*}
$$

Replacing the two terms involving permeances by a single constant expresses Eq. 6.58 in a more meaningful form:

$$
\begin{equation*}
\frac{1}{k^{2}}=\left(1+\frac{\mathscr{P}_{11}}{\mathscr{P}_{12}}\right)\left(1+\frac{\mathscr{P}_{22}}{\mathscr{P}_{12}}\right) \tag{6.59}
\end{equation*}
$$

Substituting Eq. 6.59 into Eq. 6.58 yields

$$
M^{2}=k^{2} L_{1} L_{2}
$$

or

$$
\begin{equation*}
M=k \sqrt{L_{1} L_{2}} \tag{6.60}
\end{equation*}
$$

where the constant $k$ is called the coefficient of coupling. According to Eq. $6.59,1 / k^{2}$ must be greater than 1 , which means that $k$ must be less than 1 . In fact, the coefficient of coupling must lie between 0 and 1 , or

$$
\begin{equation*}
0 \leq k \leq 1 \tag{6.61}
\end{equation*}
$$

The coefficient of coupling is 0 when the two coils have no common flux; that is, when $\phi_{12}=\phi_{21}=0$. This condition implies that $\mathscr{P}_{12}=0$, and Eq. 6.59 indicates that $1 / k^{2}=\infty$, or $k=0$. If there is no flux linkage between the coils, obviously $M$ is 0 .

The coefficient of coupling is equal to 1 when $\phi_{11}$ and $\phi_{22}$ are 0 . This condition implies that all the flux that links coil 1 also links coil 2. In terms of Eq. $6.59, \mathscr{P}_{11}=\mathscr{P}_{22}=0$, which obviously represents an ideal state; in reality, winding two coils so that they share precisely the same flux is physically impossible. Magnetic materials (such as alloys of iron, cobalt, and nickel) create a space with high permeance and are used to establish coefficients of coupling that approach unity. (We say more about this important quality of magnetic materials in Chapter 9.)

NOTE: Assess your understanding of this material by trying Chapter Problems 6.46 and 6.50.

Energy Calculations

We conclude our first look at mutual inductance with a discussion of the total energy stored in magnetically coupled coils. In doing so, we will confirm two observations made earlier: For linear magnetic coupling, (1) $M_{12}=M_{21}=M$, and (2) $M=k \sqrt{L_{1} L_{2}}$, where $0 \leq k \leq 1$.

4 Relating self-inductances and mutual inductance using coupling coefficient
image_name:Figure 6.30
description:
[
'name': 'L1', 'type': 'Inductor', 'value': 'L1', 'ports': {'N1': 'V1', 'N2': 'GND'
'name': 'L2', 'type': 'Inductor', 'value': 'L2', 'ports': {'N1': 'V2', 'N2': 'GND'
'name': 'M', 'type': 'Transformer', 'ports': {'In1': 'V1', 'In2': 'GND', 'Out1': 'V2', 'Out2': 'GND'
]
extrainfo:The circuit contains two inductors L1 and L2, coupled by mutual inductance M. The inductors are connected to voltage sources v1 and v2, and grounded at one end.


Figure $6.30 \triangle$ The cirund used to derive the basic energy relationships.

We use the circuit shown in Fig. 6.30 to derive the expression for the total energy stored in the magnetic fields associated with a pair of linearly coupled coils. We begin by assuming that the currents $i_{1}$ and $i_{2}$ are zero and that this zero-current state corresponds to zero energy stored in the coils. Then we let $i_{1}$ increase from zero to some arbitrary value $I_{1}$ and compute the energy stored when $i_{1}=I_{1}$. Because $i_{2}=0$, the total power input into the pair of coils is $v_{1} i_{1}$, and the energy stored is

$$
\begin{gather*}
\int_{0}^{W_{1}} d w=L_{1} \int_{0}^{I_{1}} i_{1} d i_{1} \\
W_{1}=\frac{1}{2} L_{1} I_{1}^{2} \tag{6.62}
\end{gather*}
$$

Now we hold $i_{1}$ constant at $I_{1}$ and increase $i_{2}$ from zero to some arbitrary value $I_{2}$. During this time interval, the voltage induced in coil 2 by $i_{1}$ is zero because $I_{1}$ is constant. The voltage induced in coil 1 by $i_{2}$ is $M_{12} d i_{2} / d t$. Therefore, the power input to the pair of coils is

$$
p=I_{1} M_{12} \frac{d i_{2}}{d t}+i_{2} v_{2}
$$

The total energy stored in the pair of coils when $i_{2}=I_{2}$ is

$$
\int_{W_{1}}^{W} d w=\int_{0}^{I_{2}} I_{1} M_{12} d i_{2}+\int_{0}^{I_{2}} L_{2} i_{2} d i_{2}
$$

or

$$
\begin{align*}
W & =W_{1}+I_{1} I_{2} M_{12}+\frac{1}{2} L_{2} I_{2}^{2} \\
& =\frac{1}{2} L_{1} I_{1}^{2}+\frac{1}{2} L_{2} I_{2}^{2}+I_{1} I_{2} M_{12} \tag{6.63}
\end{align*}
$$

If we reverse the procedure-that is, if we first increase $i_{2}$ from zero to $I_{2}$ and then increase $i_{1}$ from zero to $I_{1}$-the total energy stored is

$$
\begin{equation*}
W=\frac{1}{2} L_{1} I_{1}^{2}+\frac{1}{2} L_{2} I_{2}^{2}+I_{1} I_{2} M_{21} \tag{6.64}
\end{equation*}
$$

Equations 6.63 and 6.64 express the total energy stored in a pair of linearly coupled coils as a function of the coil currents, the self-inductances, and the mutual inductance. Note that the only difference between these equations is the coefficient of the current product $I_{1} I_{2}$. We use Eq. 6.63 if $i_{1}$ is established first and Eq. 6.64 if $i_{2}$ is established first.

When the coupling medium is linear, the total energy stored is the same regardless of the order used to establish $I_{1}$ and $I_{2}$. The reason is that in a linear coupling, the resultant magnetic flux depends only on the final values of $i_{1}$ and $i_{2}$, not on how the currents reached their final values. If the resultant flux is the same, the stored energy is the same. Therefore, for linear coupling, $M_{12}=M_{21}$. Also, because $I_{1}$ and $I_{2}$ are arbitrary values of $i_{1}$ and $i_{2}$, respectively, we represent the coil currents by their instantaneous values $i_{1}$ and $i_{2}$. Thus, at any instant of time, the total energy stored in the coupled coils is

$$
\begin{equation*}
w(t)=\frac{1}{2} L_{1} i_{1}^{2}+\frac{1}{2} L_{2} i_{2}^{2}+M i_{1} i_{2} \tag{6.65}
\end{equation*}
$$

We derived Eq. 6.65 by assuming that both coil currents entered polarity-marked terminals. We leave it to you to verify that, if one current enters a polarity-marked terminal while the other leaves such a terminal, the algebraic sign of the term $M i_{1} i_{2}$ reverses. Thus, in general,

$$
\begin{equation*}
w(t)=\frac{1}{2} L_{1} i_{1}^{2}+\frac{1}{2} L_{2} i_{2}^{2} \pm M i_{1} i_{2} \tag{6.66}
\end{equation*}
$$

We use Eq. 6.66 to show that $M$ cannot exceed $\sqrt{L_{1} L_{2}}$. The magnetically coupled coils are passive elements, so the total energy stored can never be negative. If $w(t)$ can never be negative, Eq. 6.66 indicates that the quantity

$$
\frac{1}{2} L_{1} i_{1}^{2}+\frac{1}{2} L_{2} i_{2}^{2}-M i_{1} i_{2}
$$

must be greater than or equal to zero when $i_{1}$ and $i_{2}$ are either both positive or both negative. The limiting value of $M$ corresponds to setting the quantity equal to zero:

$$
\begin{equation*}
\frac{1}{2} L_{1} i_{1}^{2}+\frac{1}{2} L_{2} i_{2}^{2}-M i_{1} i_{2}=0 \tag{6.67}
\end{equation*}
$$

To find the limiting value of $M$ we add and subtract the term $i_{1} i_{2} \sqrt{L_{1} L_{2}}$ to the left-hand side of Eq. 6.67. Doing so generates a term that is a perfect square:

$$
\begin{equation*}
\left(\sqrt{\frac{L_{1}}{2}} i_{1}-\sqrt{\frac{L_{2}}{2}} i_{2}\right)^{2}+i_{1} i_{2}\left(\sqrt{L_{1} L_{2}}-M\right)=0 \tag{6.68}
\end{equation*}
$$

The squared term in Eq. 6.68 can never be negative, but it can be zero. Therefore $w(t) \geq 0$ only if

$$
\begin{equation*}
\sqrt{L_{1} L_{2}} \geq M \tag{6.69}
\end{equation*}
$$

4 Energy stored in magnetically-coupled coils
which is another way of saying that

$$
M=k \sqrt{L_{1} L_{2}} \quad(0 \leq k \leq 1)
$$

We derived Eq. 6.69 by assuming that $i_{1}$ and $i_{2}$ are either both positive or both negative. However, we get the same result if $i_{1}$ and $i_{2}$ are of opposite sign, because in this case we obtain the limiting value of $M$ by selecting the plus sign in Eq. 6.66.

NOTE: Assess your understanding of this material by trying Chapter Problems 6.47 and 6.48.

Practical Perspective

Capacitive Touch Screens

Capacitive touch screens are often used in applications where two or more simultaneous touch points must be detected. We will discuss two designs for a multi-touch screen. The first design employs a grid of electrodes, as shown in Fig. 6.31. When energized, a small parasitic capacitance, $C_{p}$, exists between each electrode strip and ground, as shown in Fig. 6.32(a). When the screen is touched, say at the position $x, y$ on the screen, a second capacitance exists due to the transfer of a small amount of charge from the screen to the human body, which acts like a conductor. The effect is to introduce a second capacitance at the point of touch with respect to ground, as shown in Fig. 6.32(b).
image_name:Figure 6.31
description:The image labeled "Figure 6.31" depicts a schematic representation of a multi-touch screen with a grid of electrodes. The structure is shown in an isometric view, illustrating a grid layout on a rectangular plane. The grid consists of intersecting lines forming a matrix of squares, representing the electrode arrangement.

1. **Identification of Components and Structure:**
- The grid is composed of horizontal and vertical lines creating a matrix of smaller squares.
- The horizontal lines are labeled as X0, X1, X2, and X3, indicating different rows of the electrode grid.
- The vertical lines are labeled as Y0, Y1, Y2, and Y3, indicating different columns of the electrode grid.

2. **Connections and Interactions:**
- Each intersection of the horizontal and vertical lines represents a point where electrodes meet, forming a matrix of capacitive touch points.
- The grid allows for the detection of touch by monitoring changes in capacitance at each intersection point.
- The capacitive interaction occurs when a finger or conductive object touches the screen, altering the capacitance and allowing the controller to determine the touch location.

3. **Labels, Annotations, and Key Features:**
- The labeling of the rows and columns (X0 to X3 and Y0 to Y3) is crucial for identifying specific touch locations within the grid.
- The grid structure is a key feature, illustrating the organized layout necessary for multi-touch detection.

Overall, the image provides a clear representation of a capacitive multi-touch screen, highlighting the grid of electrodes essential for touch location detection.


Figure $6.31 \boldsymbol{\Delta}$ Multi-touch screen with grid of electrodes.

The touchscreen controller is continually monitoring the capacitance between the electrodes in the grid and ground. If the screen is not being touched, the capacitance between every electrode in the $x$-grid and ground is $C_{p}$; the same is true for the capacitance between every electrode in the $y$-grid and ground.

When the screen is touched at a single point, $C_{t}$ and $C_{p}$ combine in parallel. The equivalent capacitance between the $x$-grid electrode closest to the touch point and ground is now

$$
C_{t x}=C_{t}+C_{p}
$$

image_name:(a)
description:The image consists of two diagrams labeled (a) and (b), illustrating the concept of capacitance in a touch-sensitive screen.

1. **Identification of Components and Structure:**
- **Diagram (a):** Shows a single electrode embedded within a screen. The electrode is depicted as a blue rectangle. Above the electrode, there are dashed lines representing the electric field lines between the electrode and the ground. The capacitance between the electrode and the ground is labeled as \( C_{p} \), indicating parasitic capacitance when the screen is not touched.
- **Diagram (b):** Similar to diagram (a), but with an additional element: a hand approaching the screen, illustrating a touch event. The hand is pointing towards the screen, and additional electric field lines (dashed) are drawn between the finger and the electrode. The capacitance introduced by the touch is labeled as \( C_{t} \).

2. **Connections and Interactions:**
- In both diagrams, the electric field lines indicate the interaction between the electrode and the ground. In diagram (b), the presence of the finger introduces additional electric field lines, showing the increased capacitance due to the touch.
- The diagrams illustrate how the equivalent capacitance changes when the screen is touched, with the touch adding to the existing parasitic capacitance.

3. **Labels, Annotations, and Key Features:**
- Both diagrams are labeled with letters (a) and (b) to distinguish between the no-touch and touch scenarios.
- \( C_{p} \) is labeled next to the electrode in both diagrams, representing the parasitic capacitance.
- \( C_{t} \) is labeled in diagram (b) next to the finger, indicating the additional capacitance introduced by the touch.
- The electric field lines are shown with dashed lines, illustrating the concept of capacitance visually.
image_name:(b)
description:The image consists of two diagrams labeled (a) and (b), illustrating the concept of capacitance in a touch-sensitive screen.

1. **Identification of Components and Structure:**
- **Diagram (a):**
- Shows an electrode placed beneath a surface, with dashed lines indicating electric field lines extending from the electrode.
- The capacitance between the electrode and ground is labeled as \( C_{p} \), representing parasitic capacitance when there is no touch.
- **Diagram (b):**
- Similar to (a), but includes an additional element: a hand with a finger touching the surface above the electrode.
- The touch introduces an additional capacitance \( C_{t} \), shown in parallel with \( C_{p} \).
- The electric field lines in this diagram are altered, indicating the change in capacitance due to the touch.

2. **Connections and Interactions:**
- In both diagrams, the electrode is connected to the ground.
- Diagram (a) shows the natural parasitic capacitance \( C_{p} \) between the electrode and ground.
- Diagram (b) illustrates how the touch introduces additional capacitance \( C_{t} \), which combines with \( C_{p} \) to increase the total capacitance between the electrode and ground.

3. **Labels, Annotations, and Key Features:**
- Both diagrams clearly label the electrode and the capacitance values \( C_{p} \) and \( C_{t} \).
- The hand in diagram (b) is used to visually represent the touch interaction, which is key to understanding the change in capacitance.
- The dashed lines in both diagrams represent the electric field lines, showing the flow and interaction of electric fields in the presence and absence of a touch.


Figure 6.32 A (a) Parasitic capacitance between electrode and ground with no touch; (b) Additional capacitance introduced by a touch.

Likewise, the equivalent capacitance between the $y$-grid electrode closest to the touch point and ground is now

$$
C_{t y}=C_{t}+C_{p}
$$

Thus, a screen touch increases the capacitance between the electrodes and ground for the $x$ - and $y$-grid electrodes closest to the touch point.

Now consider what happens when there are two simultaneous points where the screen is touched. Assume that the first touch point has coordinates $x_{1}, y_{1}$ and the second touch point has coordinates $x_{2}, y_{2}$. Now there are four screen locations that correspond to an increase in capacitance: $x_{1}, y_{1} ; x_{1}, y_{2} ; x_{2}, y_{1}$; and $x_{2}, y_{2}$. Two of those screen locations match the two touch points, and the other two points are called "ghost" points, because the screen was not touched at those points. Therefore, this method for implementing a capacitive touch screen cannot accurately identify more than a single touch point.

Most modern capacitive touch screens do not use the "self-capacitance" design discussed above. Instead of measuring the capacitance between each $x$-grid electrode and ground, and each $y$-grid electrode and ground, the capacitance between each $x$-grid electrode and each $y$-grid electrode is measured. This capacitance is known as "mutual" capacitance and is shown in Fig. 6.33(a).

When the screen is touched, say at the position $x, y$ on the screen, a second capacitance again exists due to the transfer of a small amount of charge from the screen to the human body. A second capacitance exists at the point of touch with respect to ground, as shown in Fig. 6.33(b). Therefore, whenever there is a change in the mutual capacitance, $C_{m x y}$, the screen touch point can be uniquely identified as $x, y$. If the screen is touched at the points $x_{1}, y_{1}$ and $x_{2}, y_{2}$ then there will be precisely two mutual capacitances that change: $C_{m x_{1} y_{1}}$ and $C_{m x_{2} y_{2}}$. There are no "ghost"


[^0]:    ${ }^{1}$ DIP is an abbreviation for dual in-line package. This means that the terminals on each side of the package are in line, and that the terminals on opposite sides of the package also line up.
${ }^{2}$ The common node is external to the op amp. It is the reference terminal of the circuit in which the op amp is embedded.

[^1]:    ${ }^{1}$ See discussion of Faraday's law on page 193.


image_name:(a)
description:The image consists of two diagrams labeled (a) and (b), illustrating the concept of mutual capacitance in a touch screen system.

1. **Identification of Components and Structure:**
- **Diagram (a):** Shows two electrodes labeled as the 'x-grid electrode' and the 'y-grid electrode.' These are depicted as rectangular bars, with the x-grid electrode on the left (black) and the y-grid electrode on the right (blue).
- **Diagram (b):** Similar to diagram (a) but includes an additional element, a finger, indicating a touch interaction.

2. **Connections and Interactions:**
- **Diagram (a):** The mutual capacitance, denoted as \( C_{mxy} \), is illustrated by dashed lines curving between the x-grid and y-grid electrodes. This represents the electric field lines and the capacitive coupling between the two electrodes in the absence of a touch.
- **Diagram (b):** The presence of a finger introduces an additional capacitance, \( C_t \), depicted as an arrow pointing downwards from the finger to the x-grid electrode. Orange dashed lines represent the altered electric field lines due to the touch, showing the interaction between the finger and the electrodes.

3. **Labels, Annotations, and Key Features:**
- **Capacitance Labels:** \( C_{mxy} \) indicates the mutual capacitance between the x and y electrodes, while \( C_t \) represents the additional capacitance introduced by a touch.
- **Electric Field Lines:** Dashed lines in both diagrams represent the electric field lines, illustrating the interaction between components and the change when a touch occurs.
- **Finger Interaction (Diagram b):** The finger is shown interacting with the electrode grid, indicating how a touch affects the capacitance and alters the electric field configuration.

These diagrams effectively demonstrate how mutual capacitance is used in touch screen technology to detect and localize touch events by measuring changes in capacitance between electrodes when a conductive object, like a finger, interacts with the screen.
image_name:(b)
description:The image depicts two diagrams labeled (a) and (b), illustrating the concept of mutual capacitance in touch screen technology.

Diagram (a):
- **Components and Structure:**
- Two electrodes are shown: an **x-grid electrode** on the left and a **y-grid electrode** on the right.
- The electrodes are represented as rectangular blocks, with the x-grid electrode in black and the y-grid electrode in blue.
- **Connections and Interactions:**
- The mutual capacitance between these two electrodes is denoted as **C_{mxy}**.
- Dashed lines are used to represent the electric field lines between the electrodes, indicating the mutual capacitance.
- **Labels and Annotations:**
- The label **C_{mxy}** is placed between the two electrodes to signify the mutual capacitance.

Diagram (b):
- **Components and Structure:**
- Similar to diagram (a), it includes the **x-grid electrode** and **y-grid electrode**.
- An additional element is a hand with a pointing finger approaching the electrodes.
- **Connections and Interactions:**
- The presence of the finger introduces an additional capacitance, denoted as **C_t**.
- This additional capacitance is represented by dashed orange lines, showing the interaction with the electric field.
- The finger's proximity affects the mutual capacitance, illustrating how touch influences the capacitance.
- **Labels and Annotations:**
- The label **C_t** is next to the finger, indicating the touch-induced capacitance.
- The mutual capacitance **C_{mxy}** is still present between the electrodes.

Overall, the diagrams demonstrate how mutual capacitance between grid electrodes is altered by the introduction of a touch, a principle used in multi-touch screen technology.


Figure 6.33 (a) Mutual capacitance between an $x$-grid and a $y$-grid electrode; (b) Additional capacitance introduced by a touch.
points identified, as there were in the self-capacitance design, so the mutual capacitance design truly produces a multi-touch screen capable of identifying two or more touch points uniquely and accurately.

NOTE: Assess your understanding of the Practical Perspective by solving Chapter Problems 6.51-6.53.

## Summary

- Inductance is a linear circuit parameter that relates the voltage induced by a time-varying magnetic field to the current producing the field. (See page 176.)
- Capacitance is a linear circuit parameter that relates the current induced by a time-varying electric field to the voltage producing the field. (See page 182.)
- Inductors and capacitors are passive elements; they can store and release energy, but they cannot generate or dissipate energy. (See page 176.)
- The instantaneous power at the terminals of an inductor or capacitor can be positive or negative, depending on whether energy is being delivered to or extracted from the element.
- An inductor:
- does not permit an instantaneous change in its terminal current,
- does permit an instantaneous change in its teminal voltage, and
- behaves as a short circuit in the presence of a constant terminal current. (See page 188.)
- A capacitor:
- does not permit an instantaneous change in its terminal voltage,
- does permit an instantaneous change in its terminal current, and
- behaves as an open circuit in the presence of a constant terminal voltage. (See page 183.)
- Equations for voltage, current, power, and energy in ideal inductors and capacitors are given in Table 6.1.
- Inductors in series or in parallel can be replaced by an equivalent inductor. Capacitors in series or in parallel can be replaced by an equivalent capacitor. The equations are summarized in Table 6.2. See Section 6.3 for a discussion on how to handle the initial conditions for series and parallel equivalent circuits involving inductors and capacitors.
- Mutual inductance, $M$, is the circuit parameter relating the voltage induced in one circuit to a time-varying current in another circuit. Specifically,

$$
\begin{aligned}
& v_{1}=L_{1} \frac{d i_{1}}{d t}+M_{12} \frac{d i_{2}}{d t} \\
& v_{2}=M_{21} \frac{d i_{1}}{d t}+L_{2} \frac{d i_{2}}{d t}
\end{aligned}
$$

where $v_{1}$ and $i_{1}$ are the voltage and current in circuit 1, and $v_{2}$ and $i_{2}$ are the voltage and current in circuit 2. For coils wound on nonmagnetic cores, $M_{12}=M_{21}=\mathrm{M}$. (See page 190.)

- The dot convention establishes the polarity of mutually induced voltages:

When the reference direction for a current enters the dotted terminal of a coil, the reference polarity of the voltage that it induces in the other coil is positive at its dotted terminal.
Or, alternatively,

When the reference direction for a current leaves the dotted terminal of a coil, the reference polarity of the voltage that it induces in the other coil is negative at its dotted terminal.
(See page 190.)

- The relationship between the self-inductance of each winding and the mutual inductance between windings is

$$
M=k \sqrt{L_{1} L_{2}}
$$

The coefficient of coupling, $k$, is a measure of the degree of magnetic coupling. By definition, $0 \leq k \leq 1$. (See page 197.)

TABLE 6.1 Terminal Equations for Ideal Inductors and Capacitors

### Inductors

$\begin{aligned} v & =L \frac{d i}{d t} \\ i & =\frac{1}{L} \int_{t_{0}}^{t} v d \tau+i\left(t_{0}\right) \\ p & =v i=L i \frac{d i}{d t} \\ w & =\frac{1}{2} L i^{2}\end{aligned}$

Capacitors
$v=\frac{1}{C} \int_{t_{0}}^{t} i d \tau+v\left(t_{0}\right)$
$i=C \frac{d v}{d t}$
$p=v i=C v \frac{d v}{d t}$
$w=\frac{1}{2} C v^{2}$

TABLE 6.2 Equations for Series- and Parallel-Connected Inductors and Capacitors

Series-Connected
$L_{\mathrm{eq}}=L_{1}+L_{2}+\cdots+L_{n}$
$\frac{1}{C_{\text {eq }}}=\frac{1}{C_{1}}+\frac{1}{C_{2}}+\cdots+\frac{1}{C_{n}}$

### Parallel-Connected

$\frac{1}{L_{\mathrm{eq}}}=\frac{1}{L_{1}}+\frac{1}{L_{2}}+\cdots+\frac{1}{L_{n}}$
$C_{\text {eq }}=C_{1}+C_{2}+\cdots+C_{n}$

- The energy stored in magnetically coupled coils in a linear medium is related to the coil currents and inductances by the relationship

$$
w=\frac{1}{2} L_{1} i_{1}^{2}+\frac{1}{2} L_{2} i_{2}^{2} \pm M i_{1} i_{2}
$$

(See page 199.)
